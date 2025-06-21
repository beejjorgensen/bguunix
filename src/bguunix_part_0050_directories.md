# Directories

We've seen a bit of how directories work, but we're going to look a bit
more into how they're created and removed.

## Refresher

In an earlier section, we learned a bunch of things:

* A _path_ is a sequence of directories separated by slashes, like
  `/foo/bar`.
* `cd` is used to change directories.
  * `cd` by itself takes you to the home directory.
    * The home directory is the part of the file system that you
      control.
* `~` also refers to the home directory.
* `..` refers to the parent directory.
  * `cd ..` takes you there.
* `.` refers to the current directory.
* `/` at the front of a path means the root directory, the ancestor of
  all other directories on the system.

## Creating directories

Assuming you're in a place where you have permission to create
directories, you can make them with the `mkdir` ("make dir") command.

Let's try to do this by first going to the root directory and making a
new one there.

``` {.default}
$ cd /
$ mkdir foo
  mkdir: cannot create directory ‘foo’: Permission denied
```

Yeah, I don't have permission to do that. Remember that really I only
have permission to make subdirectories out of my home directory (or from
any subdirectories that I've made).

``` {.default}
$ cd      # go home
$ mkdir foo
$ █
```

Remember that no news is good news.

Can you specify a longer path when creating directories? Let's say the
directory `foo/` does not yet exist. Let's try this to make a `foo`
directory and then a `bar` subdirectory within it:

``` {.default}
$ mkdir foo/bar
  mkdir: cannot create directory ‘foo/bar’: No such file or
         directory
```

Hmm. It's telling us it can't make `bar` because `foo` doesn't exist.

We *could* do this:

``` {.default}
$ mkdir foo
$ mkdir foo/bar
```

And that would work!

But there's a shortcut; if we specify `-p` to `mkdir` it will create all
the subdirectories along the way for us.

``` {.default}
$ mkdir -p foo/bar
```

Success!

## Removing Directories

It's pretty easy. Use `rmdir` ("R-M dir") to remove one.

``` {.default}
$ mkdir foo     # Create it
$ rmdir foo     # Then destroy it! The power!
```

What if the directory has something in it? Can you remove it?

``` {.default}
$ mkdir foo
$ cd foo
$ touch bar.txt   # Create a file here
$ cd ..
$ rmdir foo
  rmdir: failed to remove 'foo': Directory not empty
```

Nope! Later we'll see how we can do this, but if you want to use
`rmdir`, you have to remove everything from the directory first.

## Relative Paths

Time to learn a new term! Ready?

I've been showing you paths like `/foo/bar/baz` that start with a
leading slash. That leading slash, as we've discussed means "the root
directory".

So that path is starting from the root, then going to `foo`, then `bar`,
then `baz`.

When a path starts at the root (has a `/` on the left) it is an
*absolute path*.

When it does not start with a `/`, it is a *relative path*. A relative
path means "from here", whatever your current directory is right now.

If you noticed in that earlier example, we did this:

``` {.default}
$ cd      # go home
$ mkdir foo
```

and it worked. I didn't have to do this:

``` {.default}
$ mkdir /home/beej/foo
```

But I *could* have; it would have worked just fine, because in this case
the two are equivalent.

The relative path version is me saying, "Switch to `/home/beej` then
make a `foo` directory right there."

The absolute path version is me saying, "Make `/home/beej/foo` and where
were are now doesn't matter."

The absolute path version doesn't care what our current directory is
because we're specifying the full path from the root—there's no
ambiguity.

People mostly deal with relative paths. It's really common for me to
use the relative path command:

``` {.default}
$ cd src/bguunix/src
```

from my home directory to get to the source for this book, for example.

> **Directory versus subdirectory—which is it?**
>
> * A *directory* is a place where you can store files and other
>   directories, analogous to a folder in a GUI.
> * A *subdirectory* is a directory inside another directory.
>
> Since all directories that aren't the root are inside another directory,
> they're technically all subdirectories.
>
> But in conversation, people tend to use them like this:
>
> * "Directory" when speaking in general terms or talking about absolute
>   paths.
>   * "Make a new directory."
>   * "You can find the password file in the `/etc` directory."
> 
> * "Subdirectory" when talking about two relative directories.
>   * "The user home directories are subdirectories of `/home`."
>   * "Make a `foo` subdirectory under `~/src`."
>
> There's no laws about this, so don't worry about the subdirectory
> police knocking on your door no matter which term you choose. The only
> thing that will get you weird looks is if you call the root directory
> a subdirectory.

## Renaming Directories {#mv-dir}

You rename them using the `mv` ("move") command.

What?

Yeah, it might seem weird at first. But then we'll look at what else
`mv` can do and it'll be *awesome*.

``` {.default}
$ mkdir foob     # Oops!
$ mv foob foo    # Rename it to `foo`
$ cd foo
```

As we'll see later, this is the same command you use to rename regular
files. There's a hint there that subdirectories are just a special type
of file in a Unix system, but you don't need to know that.

So why "move"? Turns out renaming a directory is a special case of
relocating it. You can move a subdirectory from one place to another.
Think of it like dragging a folder out of one folder and dropping it in
another.

Example. Let's make two subdirectories:

``` {.default}
$ mkdir foo
$ mkdir bar
```

But wait! I actually wanted to make `foo/bar`; that is, I wanted `bar`
to be a subdirectory of `foo`. I *could* `rmdir` it and remake it, but
let's say for the sake of example that I already put a bunch of files in
there and I don't want to remove all those and start again.

We can move it easily with `mv`!

``` {.default}
$ mv bar foo
```

And now we have `foo/bar` like we wanted.

I'm hearing you say something... what it is... "You're trying to pull a
fast one on me. How could I rename `bar` to `foo` if there's already a
directory called `foo`?"

Keen eye! It turns out _if the second argument to `mv` is a directory,
the first argument is moved_ ***into*** _that directory_.

If, when renaming a directory, the second argument doesn't exist, then
the directory is simply renamed. (And if the second argument exists and
is not a directory, it's an error.)

But I could have also done this for the same effect:

``` {.default}
$ mv bar foo/bar
```

Which means, "Move `bar` to a file in `foo` called `bar`."

And that hints that would could move and rename at once. Assuming
`foo/baz` does not exist, we could do this:

``` {.default}
$ mv bar foo/baz
```

And that would move `bar` into `foo`, and rename it to `baz` at the same
time.

Okay! We now have the power to create, destroy, rename, and relocate
directories. But that's not much use without being able to put files in
them. Let's look at some file operations next!

