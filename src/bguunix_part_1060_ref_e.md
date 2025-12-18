<!-- ================================================================ -->

[[manbreak]]
## `echo` {#man-echo}

Display some text on the screen.

^POSIX^ 
^BUILT-IN^
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
echo [string [string ...]]
echo [-n] [string [string ...]]   # Non-standard
```

### Description {.unnumbered .unlisted}

I said `echo` displays text on the screen, but more accurately it writes
text to standard output, which is usually the screen. This is commonly
done in scripts to let the user know things are happening.

In general, you are better off using the more capable and standardized
[`printf`](#man-printf) function for your output needs rather than the
venerable old `echo` command. Use of `echo` in very simple cases is
fine, however, e.g. you just want to print a couple words followed by a
newline.

Enclose the arguments in quotes if you need to preserve spaces,
otherwise `echo` will collapse spaces between arguments. (More
accurately, the shell will do that before `echo` sees it.)

And you might need to escape other special shell characters in there, as
well. Be extra wary of `!`, a common shell history invoker.

`echo` writes a newline at the end of the string. On many systems this
can be prevented with `-n`. But that's non-standard.

Your system might also support or not support the following escape
sequences:

* `\n`: print a newline.
* `\t`: print a tab.
* `\\`: print a backslash.
* `\c`: chops everything after it, and prevents a final newline.

You'll need to escape that backslash from the shell with single quotes,
double quotes, or an additional backslash—see the examples. Or, in some
shells, you might need to encase the escaped character in `$''`, e.g.
`$'\n'`.

Finally, on many shells, `echo` is a built-in command. But it likely
also exists as the `/bin/echo` external command, as well.

### Example {.unnumbered .unlisted}

The classic:

``` {.default}
$ echo Hello, world
  Hello, world
```

A blank line (just a newline):

``` {.default}
$ echo
  
```

Collapsing and preserving spaces:

``` {.default}
$ echo Big           space
  Big space

$ echo "Big           space"
  Big           space
```

Some newlines (non-standard):

``` {.default}
$ echo 'Hello,\nworld!'
  Hello,
  world!

$ echo $'Hello,\nworld!'
  Hello,
  world!
```

Suppressing newlines (non-standard):

``` {.default}
$ echo 'Hello, \c'; echo 'world!'
  Hello, world!

$ echo -n 'Hello, '; echo 'world!'
  Hello, world!
```

Forgetting to escape `!!` (which substitutes the last command on many
shells):

``` {.default}
$ echo Some random text
  Some random text
$ echo Hello, world!!
  Hello, worldecho Some random text

$ echo 'Hello, world!!'    # Fixed!
  Hello, world!!
```

### See Also {.unnumbered .unlisted}

[`printf`](#man-printf)

<!-- ================================================================ -->

[[manbreak]]
## `exec` {#man-exec}

Replace this shell with another program.

^BUILT-IN^
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
exec [command [argument...]]
```

### Description {.unnumbered .unlisted}

This takes the currently-running process and replaces it with another
one. Commonly used in wrapper shell scripts that do some setup and then
launch another program.

Take this example shell script called `myls`:

``` {.bash}
#!/bin/sh

args="-l -a"

ls $args $1
```

It effectively does `ls -l -a` on whatever you pass in as an argument.
 
``` {.default}
$ ./myls hello.txt
  -rw-r--r-- 1 beej beej 13 Dec 18 10:12 hello.txt
```

But the way it works is like this:

1. A new shell process for `myls` is created.
2. It sets its `args` variable.
3. A new process is created to run `ls`.
4. `myls` pauses execution to wait for `ls`.
5. `ls` exits.
6. `myls` resumes.
7. `myls` exits.

So the whole time `ls` is running, `myls` is just sitting there doing
nothing, and, worse, when `ls` is done, `myls` just goes on to quit. So
`myls` was using resources it didn't need to use that whole time.

Admittedly, this simple example doesn't seem like such an abuse, and
it's not. But imagine instead of `ls` we were running some program that
was going to live for... a _year_. You'll just have that `myls` sitting
there doing nothing except wasting resources for no reason.

What you want is, since `ls` is the last thing `myls` will do, is to
replace the `myls` process with the `ls` one entirely. `myls` (the
process) will be gone at that point so we'll have this:

1. A new shell process for `myls` is created.
2. It sets its `args` variable.
3. `myls` runs `exec ls`, replacing itself with `ls`.
4. `ls` exits.

That's what `exec` does. Less overhead, less resource use.

And you can only use it as the last thing the shell script does since
the shell script process ceases to exist the moment it `exec`s
something.

I'm also going to mention that `exec` can also be used to open and close
files in shell scripts. It can also be used to duplicate file
descriptors. These are less common, but are quite powerful.

### Example {.unnumbered .unlisted}

This modifies the above example to use `exec`:

``` {.bash}
#!/bin/sh

args="-l -a"

exec ls $args $1

echo This line never executes
```

When you run that, the `exec` line replaces `myls` with `ls`. The `myls`
program that was running is overwritten and so that last `echo` line
never runs.

``` {.default}
$ ./myls hello.txt
-rw-r--r-- 1 beej beej 13 Dec 18 10:12 hello.txt
```

### See Also {.unnumbered .unlisted}

[`exit`](#man-exit)

<!-- ================================================================ -->

[[manbreak]]
## `exit` {#man-exit}

One line description.

^POSIX^ 
^BUILT-IN^
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
exit [n]
```

### Description {.unnumbered .unlisted}

Exits this shell (or shell script). Optionally, you can give it an exit
status value. By very strong convention, an exit status of `0` means
"success" and a positive number means "failure".

### Example {.unnumbered .unlisted}

Here I'll launch a new Bourne shell (from my Zsh prompt), and then exit
it to get back to Zsh:

``` {.default}
/home/beej % sh
sh-5.3$ echo Bourne shell!
Bourne shell!
sh-5.3$ exit
exit
/home/beej % █
```

And here's a shell script `foo.sh` that exits with a non-zero status:

``` {.bash}
printf "I'm exiting with status 2\n"
exit 2
```

Here I run it and check the exit status from the launching shell with
the `$?` variable:

``` {.default}
$ sh foo.sh
  I'm exiting with status 2
$ echo $?
  2
```

### See Also {.unnumbered .unlisted}

[`exec`](#man-exec)

<!-- ================================================================ -->

<!--

[[manbreak]]
## `x` {#man-x}

One line description.

^POSIX^ 
^BUILT-IN^
^SCRIPT^
^NON-STANDARD^

### Synopsis {.unnumbered .unlisted}

``` {.default}
```

### Description {.unnumbered .unlisted}

### Example {.unnumbered .unlisted}

``` {.default}
```

### See Also {.unnumbered .unlisted}

[`x`](#man-x)

-->
