# Files

We've explored a bit of how directories work, but let's talk about the
files that are in those directories and what we can do with them.

Let's look at:

* Creating files
* Viewing files
* Renaming files
* Moving files
* Removing files

## Creating Files

The usual way to create a file is to open some editor, type in some
stuff, and save it. See the [Vim appendix](#vim-tutorial) if you want to
tackle that editor.

But that's a bit out of scope for the moment, so we're going to give you
a couple ways to create files on the command line so that we have some
to play with.

Here I'm creating a file called `foo.txt` (assuming it doesn't yet
exist) with nothing in it:

``` {.default}
$ touch foo.txt
$ ls foo.txt
  foo.txt
```

Another way to do it is to redirect the output of the `echo` command
into the file. You don't need to know what that means yet—we'll cover it
all later. This example will create a file `foo.txt` with the content
"Hello, world!" within it:

``` {.default}
$ echo 'Hello, world!' > foo.txt
$ ls foo.txt
  foo.txt
```

Finally, a third way that allows multiple lines of input is to use the
`cat` utility. Enter as many lines as you want, and then at the
beginning of the last line, hit `CTRL-d` which is Unix's end-of-file
indicator. That'll get you back out to the prompt.

``` {.default}
$ cat > foo.txt
  I'm typing this line
  and this one, too.
  And at the start of the next line, I'll hit ^D to end
$ █
```

(See that `^D`? in Unix you read this as "control D", i.e. hit `CTRL-d`.
Any time you see a caret in front of a capital letter, it means hold
down `CTRL` and hit that letter.)

**None of these are typically how files are created.** But I want to be
able to create some files so we can test out the other file-oriented
commands.

## Viewing files

Again, the usual way to view files is in your editor, or with a viewer
for whatever type of file you're trying to open (like a JPEG image or
whatever).

But so we have something to play with in this tutorial, we're going to
look at some ways of viewing plain text files.

The first is `cat`. This is short for "concatenate", meaning to join
together in sequence. That might seem to have nothing to do with viewing
files, but what `cat` basically does is show all the files you give in
on the command line one after another. And if there's only one file, it
only shows you that file.

Let's make a file and view it.

``` {.default}
$ echo 'Hi, there' > hi.txt
$ cat hi.txt
  Hi, there
```

Easy enough. And like I said, if you have multiple files, it'll output
them all:

``` {.default}
$ echo 'Hi, there' > hi.txt
$ echo 'Bye!' > bye.txt
$ cat hi.txt bye.txt
  Hi, there
  Bye!
```

Now bear with me through this next example. Run these two commands, and
don't worry about how the second one works, keeping in mind that this
will overwrite `foo.txt`:

``` {.default}
$ rm -f foo.txt
$ for i in $(seq 100); do echo "Line $i" >> foo.txt; done
```

That will create a file `foo.txt` with 100 lines in it.

What happens when you `cat` it? It likely scrolls off your screen!
Your terminal emulator probably has a scrollback buffer and you can back
up with your mouse.

What if you want to view it a page at a time? You can use the `more`
command.

``` {.default}
$ more foo.txt
```

And that'll show you a page at once. Depending on the version of `more`
you have, you can hit `RETURN` to go down a line, or hit `SPACE` to go
down a page. And the arrow keys might work for moving forward and
backward.

There's also more-capable non-standard utilities called `less` and
`most` that you might have installed on your system.

We'll come back to `more` later and see some other tricks it can do.

## Renaming and Moving Files

If you read the [Renaming Directories]{#mv-dir} section, this will be
very familiar to you, since it's basically the same. In fact, if you
haven't read that section, read it now.

We'll use the `mv` ("move") utility to rename files. Or move them to
different directories. This is how it works.

If we have this command:

``` {.default}
$ mv source destination
```

one of three different things can happen depending on whether or not the
destination is a directory, or if it's a regular or non-existent file.

* **Normal rename**: If `destination` does not exist, `source` is
  renamed `destination`.
* **Overwrite rename**: If `destination` does exist and is a regular
  file, `destination` is deleted and `source` is renamed `destination`.
  Yes, you can overwrite files if you're not careful!
* **Move**: If `destination` is a directory, `source` is *moved* into
  the `destination` directory.

You can also simultaneously move and rename if you specify a new
file name in the destination directory.

Some examples:

``` {.default}
$ mv foo.txt bar.txt    # Rename foo.txt to bar.txt
$ mkdir someplace
$ mv bar.txt someplace  # Move bar.txt into the someplace directory

$ mv baz.txt someplace/frotz.txt  # Move and rename
```

## Removing Files

We're going to remove files with the `rm` command (pronounced "R-M",
short for remove).

TODO

## Removing Subdirectory Hierarchies

TODO
