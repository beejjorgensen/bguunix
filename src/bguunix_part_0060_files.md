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
stuff, and save it. See the [Vim appendix](#appendix-vim) if you want to
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

TODO

## Renaming and Moving Files

TODO

## Removing Files

TODO

## Removing Subdirectory Hierarchies

TODO
