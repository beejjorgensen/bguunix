# First Steps

All right! You've launched the terminal window and it's sitting there
with the prompt waiting for you to type _literally anything_.

(I'm going to use a `$` to represent the prompt even though you might
have a different prompt on your system.)

``` {.default}
$ █
```

So what can you type? We're going to start with the easiest command:

``` {.default}
$ ls
```

(Don't type the `$`; just type `ls` (pronounced "ell-ess") and hit
`RETURN`.)

This is short for "list" and it's the command that tells you what files
are in the "current" directory (remember directories are "folders").
More on that in a moment.

Depending on your system, you'll see a variety of things printed out. If
you see nothing, type `ls -a` instead (`-a` for "all") and you'll see at
least a couple things.

So `ls` tells you what's in the current directory. I use it a lot.

But what do I mean by "current directory"?

## Intro to Directories

What is the current directory? The shell keeps track of "where you are"
at all times. With a GUI, you might have several file explorer windows
open at the same time, each showing a different folder. Shell windows
are the same. You might have many shell windows open at once all in
their current directories.

How do I get the current directory? Let's issue a command to tell us,
the "print working directory" command.

(In this guide, anything prefaced with the shell prompt `$` is something
you should type (but don't type the `$`). Lines not prefaced with `$`
are the output of that command.)

``` {.default}
$ pwd
  /home/beej
```

Your output may vary—I'm on a Linux machine. On a Mac you might see
`/Users/beej` or on WSL `/mnt/c/Users/Beej`.

What's that mean? Remember that with the GUI we have folders, and
folders can contain folders which can contain folders. Well, it has to
start somewhere, right? There must be a super-grandparent folder that
starts it all. In Unix, we call this the _root directory_.

You can imagine all those folders forming a tree-like hierarchy. The
root directory is at the base of this tree.

In Unix, the root directory is indicated by a leading `/` (pronounced
"slash").

Since I'm currently in `/home/beej`, we can read this as, "From the root
directory, which is `/`, go to the subdirectory called `home`. From
there, go to the subdirectory called `beej`. And that's where we are."

The other `/` between `home` and `beej` doesn't refer to the root
directory; it's just a directory name separator. Only the first, leading
`/` means the root.

The output of `pwd` shows us how to get from the root directory to where
we are now. That output is called a _path_ or _pathname_.

Compare this to file explorer windows in a GUI. There's a folder that is
the "bottom-most" folder in the hierarchy—that's the root folder. Inside
that, there's a `home` folder and inside _that_ folder is a `beej`
folder.

So how do we move around? With a GUI, we might click on a folder name to
open it. Or there might be a "parent" folder button to go "up" a level.
But we can't do that here because this is text land!

## Changing Directories

The "change directory" command is `cd`. This is how we move around
between folders.

> **Keyboards used to be bad.** I mean, *really* bad compared to modern
> keyboards. You really didn't want to type more than you had to.
> Furthermore on old teletype terminals, it used ink. And who wants to
> waste that? So lots of Unix commands are quite terse, which, while
> confusing at first, ultimately is a blessing. By contrast, the VMS
> operating system from DEC had the `SET DEFAULT` command. Which would
> you rather type?
>
> Yes, I'm still bitter about my VMS experience in 1992. At least DEC
> also gave us [flw[Ultrix|Ultrix]]!

Let's try it.

``` {.default}
$ pwd
  /home/beej
$ ls
  bar     foo.txt     src      tmp
```

I have four files. Some of them are files with data in them (like
`foo.txt` is probably a text file), and some are directories. How can I
tell which is which?

(Your system might already be configured to do some of this, but bear
with me.)

Some versions of `ls` support color, and you can run:

``` {.default}
$ ls --color=auto
```

to get some colorful output. And then directories might be a different
color.

You can also run `ls -F` and that will append a `/` to the end of all
files that are directories. And it also appends a `*` to the end of all
files that are executable (i.e. programs you can run):

``` {.default}
$ ls -F
  bar*    foo.txt     src/     tmp/
```

Aha! Now we see `bar` is a program we can run, `foo.txt` is a regular
file, and `src` and `tmp` are _subdirectories_ out of our current
directory.

Finally, let's change to one!

``` {.default}
$ cd bar
  cd: not a directory: bar
```

What? Oh, wait. `bar` is an executable program, not a directory. Let's
try going to `src`:


``` {.default}
$ cd src
$ █
```

...And there's no output and we're back to the prompt. Did anything
happen?

Yes! In Unix, _no news is good news_. It worked! Let's be sure. What
should our current directory be? If we were in `/home/beej` and we went
into the `src` subdirectory, we should now be in `/home/beej/src`.

``` {.default}
$ pwd
  /home/beej/src
```

And we are!

What's in this folder?

``` {.default}
$ ls
  advent  bguunix   dnd     vants
  bgnet   conquest  perlin
```

Now because I wrote all these, I know they're all subdirectories,
themselves. But I could always `ls -F` to be sure. And I could `cd` into
any of them to get my current working directory to
`/home/beej/src/vants`, for example. But you get the idea.

## The Parent Directory

Let's flashback to something I said earlier about the GUI—that there's
often a button to take you to the parent folder or "up" a level. We can
do that with `cd`, too.

But first, let's examine the `ls -a` ("all") command again. Turns out
that in Unix, `ls` will not show you "hidden" files by default. You have
to specify `-a` to also see all the hidden files. What makes a file
hidden? If the file name begins with a period. That's it. That makes it
hidden. A file called, say, `.bashrc` ("dot-bash-R-C") will not show up
in a directory listing unless you use `-a`.

``` {.default}
$ ls -a
  .   advent  bguunix   dnd     vants
  ..  bgnet   conquest  perlin
```

Hmmm! We have two more files there, `.` and `..`. They both start with a
period, so they're hidden. What are they?

``` {.default}
$ ls -aF
  ./   advent  bguunix   dnd     vants
  ../  bgnet   conquest  perlin
```

Oh! They're directories! (Also see how I did `-a` and `-F` in that
`ls`?)

These are special directories, and every directory contains them. They
always mean the same things.

* `..` is the parent directory from here. You `cd ..` to go to the
  parent, i.e. to go "up" a level.

* `.` is the current directory that you're in right now. You `cd .` to
  change to exactly where you already are. That seems pointless, but
  we'll find good uses for it later.

Let's go up a directory.

``` {.default}
$ pwd
  /home/beej/src
$ cd ..
$ pwd
  /home/beej
```

And we're home. Can we keep going? Sure!

``` {.default}
$ pwd
  /home/beej
$ cd ..
$ pwd
  /home
$ cd ..
$ pwd
  /
$ cd ..
$ pwd
  /
```

Looks like we bottom out at the root directory. The root directory does
have a `..` "subdirectory" so it's not an error to go there, but it just
sends you back to the root.

Let's go home by `cd`'ing to the full path of my home directory:

``` {.default}
$ cd /home/beej
$ pwd
  /home/beej
```

But what is the "home directory"?

## The Home Directory

All users on a Unix system have a "home" directory. Generally speaking,
this is your domain. You can create files here, make subdirectories,
etc. and other users generally don't have permission to view those files
or subdirectories.

> **Other users on your system might be able to see your stuff!**
> Depends on how you have permissions set up, something we'll talk about
> later. But in this modern day and age, it's very common that you are
> the **only** user on your system (unless you made accounts for other
> people, something you'd remember having done). So there's no one else
> to try to see your files. File permissions are local to your system;
> people over the Internet can't generally see them no matter what your
> permission settings are.
>
> Now, if you're logged into a shared server, this becomes more
> important because there are multiple users on that same system. One
> server I have an account on has 58 other people logged into it at the
> moment I'm writing this sentence. I have my home directory there
> locked down so no one else can peek into it.

But directories above your directory, e.g. `/home` or the root directory
`/` don't belong to you and you don't have permission to change things
there. Here I am, a regular user, trying to remove my system's password
file. This would be a significant disaster if it were allowed:

``` {.default}
$ rm /etc/passwd
  rm: cannot remove '/etc/passwd': Permission denied
```

But I can't. I don't have permission.

When you first log in with a terminal, you're typically dumped in your
home directory. (WSL users most definitely should read the next section
about this because you have *two* home directories! And there's a
section for you Git Bash users, too.) Some terminals will put you in the
same directory as your previous terminal window, so watch for that.

There are multitude of ways to change back to your home directory.

Here is my favorite:

``` {.default}
$ cd
```

Just `cd` by itself will take you home.

There's one more thing to note: `~` expands to be your home directory.
So I could also do this to get home:

``` {.default}
$ cd ~
```

This is more useful when you're buried somewhere in the hierarchy and
you want to go someplace relative to home.

``` {.default}
$ pwd
  /usr/local/share/lib/wumpus
$ cd ~/src
$ pwd
  /home/beej/src
```

## Home Directories in WSL

This section is just for Windows users.

WSL is interesting. First of all, let's just go to Windows land,
forgetting about WSL for a moment.

In Windows, you also a home directory. For me, it's at this path:

```
C:\Users\beej
```

That's a Windows-style path. They use `\` for a separator, and the root
is prefixed by a "drive letter". Doesn't matter.

What does matter is that in WSL, which is a little Linux virtual machine
on top of Windows, you get *another* home directory, one specifically
for Linux.

So you'll have these two home directories, assuming your name is `beej`,
which it probably isn't, but I trust you can do the necessary
substitutions in this example:

* `/home/beej` in WSL
* `C:\Users\beej` in Windows

***And they are different places.*** Files you put in one are not
visible in the other. In fact, they don't even have to have the same
user name. I could be `/home/beej` in WSL and `C:\Users\brian` in
Windows. (But I'm not.)

If you open Windows file explorer and go into your left sidebar, you'll
see "Linux" with a cute little [flw[Tux|Tux_(mascot)]] icon. Click on
that and you'll see an "Ubuntu" folder (or whatever distro you
installed). Opening that, you'll see a bunch of folders and files. This
is the root directory in WSL! See `home` in there? I can follow that to
the `beej` folder and see what files I have in WSL.

It might be worth bookmarking that if you go there frequently.

And the reverse is true! If you're in a WSL shell, you can `cd` out into
your Windows disk. Your Windows disk starts at path `/mnt/c` ("slash
mount slash see"). Here I am in WSL switching to my Windows home
directory:

``` {.default}
$ cd /mnt/c/Users/beej
```

This all gets extra confusing because sometimes when you first launch a
WSL shell, it dumps you in your Windows home directory. And so you can
do this:

``` {.default}
$ pwd
  /mnt/c/Users/beej
$ cd
$ pwd
  /home/beej
```

I was in my Windows home directory, then I typed `cd` to go home, and
that landed me in my WSL Linux home directory.

It is best to be clear to yourself which "world" you're operating in at
all times: Windows or WSL?

**Here's my recommendation:** if you're doing Unix-style development for
work or school, do it 100% from inside WSL and use your Linux home
directory (e.g. `/home/beej`) as your base. Ignore `/mnt/c` unless you
have to go there to transfer files from Windows land to Unix land. Use
WSL Bash for all your Unix work and ignore PowerShell unless you need
it. Part of the reason for this is differences in how Windows treats
file permissions in `/home` versus `/mnt/c/Users` or anything that maps
to a OneDrive directory; it can be a pain to deal with.

Conversely, if you're doing Windows development, well, why are you using
WSL at all? `:)`

## Home Directories in Git Bash

This section is just for Windows users; even if you're not running WSL,
I recommend you read that section, above, to get more backstory.

Your home directory in Git Bash is the same as your home directory on
Windows. Of course the path looks different, though.

My home directory path is:

* `/c/Users/beej` in Git Bash
* `C:\Users\beej` in other Windows shells

Importantly, and unlike WSL, ***these are the same place***. A file you
add to one will be immediately visible in the other. Changes you make in
a File Explorer window will be immediately reflected in Git Bash.

Also, there is no `/home` in Git Bash.

Git Bash exists to make it easier to run Git commands on the command
line as well as Bash scripts. You can use it to practice with the Unix
command line, too!

## Home Directories on the Mac

Congratulations! Your GUI-land home and your terminal shell home are the
exact same directory. You can navigate to your `/Users` directory in
Finder and see everything there. My home directory on my Mac is
`/Users/beej`.

You can even:

``` {.default}
$ cd ~/Desktop
```

and `ls` the files that are on your Mac desktop right
now[^ea79].

[^ea79]: Your mileage may vary on Linux or other Unices (yes, that's
    plural). I think it's common to have the GUI desktop there, but
    there's no law about it.

I don't say it often, but well done, Apple!

## Home Directories in Unix-likes

They tend to be under `/home` these days, but they don't have to be.
Sometimes they're under `/usr/home`. On my Linux machines, I'm in
`/home/beej`.

In any case, `cd` will take you there, and `pwd` will tell you the path.
For the most part, people don't care _where_ their home directory is, as
long as they can easily get there.
