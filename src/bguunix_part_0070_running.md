# Running Programs

We've already been running programs like `ls`, `rm`, and `mkdir`. That
was easy! You just type the name of the program to run and maybe some
things after that.

Let's dig into those details a bit more to see some common patterns that
Unix has.

## Options/Flags/Switches

We saw earlier that we could do this to remove a file:

``` {.default}
$ rm foo
```

And we could do this to override permissions in some circumstances:

``` {.default}
$ rm -f foo
```

The `-f` is an _option_. Or a _flag_. Or, more rarely, a _switch_. It's
a way to modify the behavior of the command. (In this case, `-f` means
"force". That is, if `rm` was going to try to stop you for some reason,
this means you really meant to do it, and it should just go for it.)

The general pattern is:

``` {.default}
$ command options arguments
```

When the command runs, it processes the options and arguments (which,
collectively, are referred to as the _command line arguments_) and
decides what to do based on them.

As the name implies, options are optional (usually). And actually
arguments are also optional (sometimes). For instance, these are all
valid invocations of `ls`:

``` {.default}
$ ls
$ ls -l
$ ls -l foo.*
```

## What Programs Exist?

Holy cow, there are a lot of them.

Here's a quick overview of some POSIX standard programs (and some
nonstandard ones, tagged with "‡") that come installed on Unix systems.

Don't worry about the details now; just skim it for the back of your
brain.

(Technically, some of the following commands aren't external programs at
all, but are instead built into the shell. Don't worry about this
distinction for now.)

|Command|Description|
|--------|--------------------------------------------------------|
|`alias`|Define a new command that is an alias of an existing one|
|`awk`|Invoke the AWK programming language|
|`basename`|Print the name of a file without the path part|
|`bash`‡|Run a Bash shell|
|`bc`|Calculator for arbitrary-precision math|
|`c99`|Run a C language compiler, more commonly `cc`, `gcc`, or `clang`|
|`cal`|Show a calendar|
|`cat`|Concatenate files|
|`cd`|Change directory|
|`chgrp`|Switch the group ownership of a file|
|`chmod`|Change permissions on a file|
|`chown`|Change user ownership of a file|
|`chsh`‡|Change your default shell|
|`cksum`|Compute the checksum of a file|
|`cp`|Copy a file|
|`cut`|Cut fields out of lines of text|
|`date`|Print the date and time|
|`dd`|Dump or copy data from one file to another|
|`df`|Show how much disk space is free|
|`diff`|Show the difference between two files|
|`du`|Show how much disk space is used by a file or directory tree|
|`echo`|Print a message on the screen|
|`exit`|Exit the shell
|`expr`|Do simple math|
|`false`|Does nothing, unsuccessfully|
|`file`|Tries to identify the contents of a file|
|`find`|Locate files|
|`free`‡|Tells you how much memory is used and free|
|`grep`|Search for patterns in files|
|`hash`|Tells you where programs are located in the system|
|`head`|Shows you the first lines of a file|
|`hexdump`‡|Dumps byte values for a given file|
|`history`‡|Tells you what commands you've typed earlier|
|`hostname`‡|Tells you the name of this computer|
|`id`|Shows your username and any groups you're in|
|`kill`|Terminate another program|
|`less`‡|Show a program a page at a time|
|`ln`|Make a link to an existing program|
|`ls`|Display directory contents|
|`make`|Build tool usually used for C programs|
|`man`|Bring up manual pages for given commands|
|`md5sum`‡|Compute the MD5 hash of the given files|
|`mkdir`|Create a directory|
|`more`|View data a page at a time|
|`most`‡|View data a page at a time|
|`mv`|Move and/or rename a file|
|`nl`|Number lines of a given input file|
|`od`|Dump byte data of files|
|`paste`|Horizontally concatenate files|
|`printf`|Print output to the screen|
|`ps`|List all programs currently in operation|
|`pstree`‡|Like `ps`, except as a more readable hierarchy|
|`pwd`|Print the working (current) directory|
|`read`|Read a line of input from the keyboard|
|`reset`‡|Try to return the terminal to a sane state if it's hosed|
|`rm`|Delete files or directory hierarchies|
|`rmdir`|Delete directories|
|`scp`‡|Secure copy—usually used to copy from one computer to another|
|`sed`|Stream editor to edit text files in scripts|
|`sh`|Run a Bourne shell|
|`shasum`‡|Compute the SHA hash of the given files|
|`sleep`|Do nothing for a given number of seconds|
|`sort`|Sort a file|
|`split`|Split long files into chunks|
|`ssh`‡|Connect to a remote machine securely and bring up a shell|
|`strings`|Extract printable strings from binary data|
|`stty`|Control the terminal at a low level|
|`su`‡|Change to a different user|
|`sudo`‡|Run a program as administrator|
|`tail`|Show the last lines of a file|
|`tar`‡|Manage file archives|
|`tee`|Split output so that it goes to the screen and to a file|
|`test`|Compute the result of a Boolean expression|
|`time`|Measure how long it takes a program to run|
|`touch`|Create a file, or update its "last modified" time to now|
|`tput`|Often used to change output colors in scripts|
|`tr`|Translate characters from one value to another value|
|`true`|Do nothing, successfully|
|`type`|Tells you if a command is a real command or an alias|
|`umask`|Set default permissions for new files|
|`unalias`|Remove an alias|
|`uname`|Print the OS name and other information|
|`unzip`‡|Extract files from a ZIP archive|
|`uptime`‡|Show how long the system has been up|
|`vi`|Launch the `vi` editor, more commonly `vim`|
|`w`‡|See who else is on the system|
|`who`‡|See who else is on the system|
|`wc`|Count characters, words, and lines in a file|
|`zip`‡|Create a ZIP file archive|

Whew! That's a lot. Again, don't worry about memorizing all that—just
remember the ones that look _extra_ fun.

But do go ahead and run some of them! If you end up with just a taunting
cursor and no output, try typing something and hitting `RETURN`. If
still nothing happens, you can try `CTRL-c` (interrupt) or `CTRL-d` (end
of input) to get back to your shell prompt.

If you want to explore _even more_, the commands on your system can be
found by running:

```
$ ls /bin /usr/bin | sort -u
```

That will give you a directory listing of all the commands in the two
common directories that hold them. Usefulness is questionable; on my
system there are 5,661 programs across those two directories and I
probably only know 200 of them.

(And what's that `|` symbol? We'll find out later!)

## Directory Listings

TODO


## The Manual
