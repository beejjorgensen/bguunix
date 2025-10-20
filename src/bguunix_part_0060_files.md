# Files

We've explored a bit of how directories work, but let's talk about the
files that are in those directories and what we can do with them.

First let's look at some supporting stuff:

* Wildcards and referring to files
* Tab completion

Then let's look at:

* Creating files
* Viewing files
* Renaming files
* Moving files
* Removing files

## Referring to Files and Directories

We've already seen that you can just refer to a file or directory by
name. If you have a directory named `blorple`, you can remove it simply
by name.

``` {.default}
$ rmdir blorple
```

But let's increase our power. We're going to learn a new term here:
_globbing_.

This is a way to describe many files using just a few _wildcard_
characters.

For example, in my home directory, I have a zillion files that start
with `foo.`:

``` {.default}
foo.c
foo.py
foo.sh
foo.pdf
foo.txt
foo.md
```

and I lose track of how many I have and what they are. I want to see an
`ls` of just those files, and no other files. I can tell `ls` on the
command line exactly what files I want to see...

``` {.default}
$ ls foo.c foo.py foo.sh ...
```

But (A) how do I know what files I have before I look, and (B) even if I
did, that's a *metric ton* of typing I'll have to do. I have like 40
`foo` files in there. No thanks!

What I want is a way to say, "Hey, show me all the files that begin with
`foo.`, please."

And we can do that, like this:

``` {.default}
$ ls foo.*
```

(This is pronounced "foo dot star", typically, though some old Unix
hackers call `*` a "splat".)

And that does it! All the files that start with `foo.` are shown!

> **Some behind-the-scenes footage** shows us what is happening here:
> the shell looks at `foo.*` and _substitutes_ all the matching files on
> the command line _before `ls` even sees it_.
> 
> So I say `ls foo.*` and `ls` thinks I typed:
>
> ``` {.default}
> ls foo.c foo.py foo.sh foo.pdf foo.txt   # etc etc etc
> ```
>
> <!-- ` -->
> It can be helpful to remember that it's not the `ls` program (or any
> external program) that contains the smarts about expanding the `*`;
> the shell takes care of that dirty work before the program sees it.

The `*` can go anywhere in the file name, and you can have multiple ones
in there at the same time.

For example, "Show me all files that begin with "abc" followed by any
sequence of characters followed by "def" followed by any other
characters."

``` {.default}
$ ls abc*def*
```

Be careful when deleting files with wildcards! You can easily delete
more than you wanted.

There are more wildcard characters that have additional meaning for
globbing, but we'll save those for later.

## Tab Completion

I'm going to give you one more hint about a non-standard, **very**
powerful feature that's common in modern shells: _tab completion_.

Let's say you downloaded two images from the Internet, and they're
named:

``` {.default}
IMG_20250624_032123277.jpg
IMG_20250624_032123312.jpg
```

You wish to edit the second of these photos with the
[fl[GIMP|https://www.gimp.org/]] image editor.

So that would be:

``` {.default}
$ gimp IMG_20250624_032123312.jpg
```

but who wants to type all that?

Your first thought might be, can I use a wildcard? You _could_, but both
of these files start with the same prefix for a lot of characters.

So great, you could type the whole name out, or maybe copy and paste
with the mouse... but that's slow.

Let's do the magic. If I type at the prompt `gimp IMG` and then hit the
`TAB` key, this is what I see:

``` {.default}
$ gimp IMG_20250624_032123█
```

It filled out all those prefix characters for me! Basically the shell
saw me type `IMG` and then hit `TAB`, and it went and looked for all
files that started with `IMG` and it filled in as much of the common
prefix as it could. It stopped when it found an ambiguous character
because it doesn't know what to do from there.

Bonus feature: if I hit `TAB` again immediately, I see this:

``` {.default}
$ gimp IMG_20250624_032123█
  IMG_20250624_032123277.jpg  IMG_20250624_032123312.jpg
```

It printed out the candidate file names for me! What I have to do is
choose one.

And I choose it by typing the next unique character to differentiate
between them. Looks like the first one has a `2` at the point, and the
second a `3`. Since I want the second one, I type the `3`:

``` {.default}
$ gimp IMG_20250624_0321233█
  IMG_20250624_032123277.jpg  IMG_20250624_032123312.jpg
```

and then I hit `TAB` again:

``` {.default}
$ gimp IMG_20250624_032123312.jpg█
  IMG_20250624_032123277.jpg  IMG_20250624_032123312.jpg
```

And the name is completed for me! So to get that big file name loaded up
in GIMP, I typed:

``` {.default}
gimp IMG[TAB]3[TAB]
```

and that's not many keystrokes. If there had been a subsequent ambiguity
in the file name, I'd have had to type another character and hit `TAB`
again, but in this case there wasn't.

And like I said before, this isn't a standard feature. Your mileage may
vary depending on your shell, but you might find that some shells are so
adept at tab completion that they'll even complete Git commands and
other things.

## Creating Files

All right! Let's see some action!

The usual way to create a file is to open some editor, type in some
stuff, and save it. See the [Vim appendix](#vim-tutorial) if you want to
tackle that editor.

But that's a bit out of scope for the moment, so we're going to give you
a couple ways to create files on the command line so that we have some
to play with.

Here I'm creating a file called `foo.txt` using the `touch` command
(assuming it doesn't yet exist) with nothing in it:

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

(See that `^D`? In Unix you read this as "control D", i.e. hit `CTRL-d`.
Any time you see a caret in front of a letter, it means hold down `CTRL`
and hit that letter. Don't hold the `SHIFT` key even if the letter is
capitalized. If you are meant to hold the `SHIFT` key, the instructions
will be explicit about it: `CTRL-SHIFT-D`.)

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

If you read the [Renaming Directories](#mv-dir) section, this will be
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

The only thing that's tough about this command is that ***you can't undo
an `rm`!***

Once you `rm` a file, it's really just gone[^99af].

[^99af]: Technically, it's probably still there in some undead,
    very-difficult-to-recover form. Most filesystems don't offer a
    temporary "Trash" folder or anything like that. But some do have
    features that can help you undelete things. Best thing to do is just
    triple check before you hit `RETURN`, though!

And for something this dangerous, it's really easy to use!

``` {.default}
$ echo 'Hi, there' > hi.txt       # Create a file
$ cat hi.txt                      # Examine it
  Hi, there
$ rm hi.txt                       # Remove it
$ ls hi.txt                       # Look for it
  ls: cannot access 'hi.txt': No such file or directory
```

See the output from `rm`? That's right—there is none. No news is good
news, so it must have worked.

## Removing Subdirectory Hierarchies

Ready to get *really* dangerous?

Remember how we could remove directories with `rmdir`? Well, what if you
have a big subdirectory tree that you want to remove? That is, you want
to remove the directory `foo/` and everything under it, including all
the subdirectories.

Since `rmdir` requires the directory to be empty, that's a lot of
work.

But `rm` offers us something more powerful: the ability to _recursively_
remove directory trees all in one go.

This is very dangerous, as you might imagine. Get it wrong and you could
accidentally blow away **all** your stuff!

If you give the `-r` option to `rm`, that means delete recursively. The
argument is expected to be a directory name in that case.

Sometimes `rm` might balk at deleting certain files for permission
reasons, but you can (if you own the directory the file is in) still
delete it. In that case you might also need to pass the `-f` flag
("force").

So the killer, hazardous command to remove the entire `foo/`
subdirectory hierarchy is:

``` {.default}
$ rm -rf foo/
```

And it'll chug for a moment and then, hopefully, give you no news.

If you start running one of these and realize it's a horrible, horrible
mistake, hit `CTRL-c` as quickly as possible to interrupt it and
minimize the damage. If you get the chance.

Finally, mandatory reading on this front is the delightful [fl[UNIX
Recovery Legend|https://www.ecb.torontomu.ca/~elf/hack/recovery.html]]
that has been circulating for decades. Check it out.
