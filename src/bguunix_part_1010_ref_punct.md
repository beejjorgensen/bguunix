<!-- ================================================================ -->

[[manbreak]]
## `!` (history) {#man-bang-history}

Look up commands in history.

^BUILT-IN^

### Synopsis {.unnumbered .unlisted}

``` {.default}
!!
!*
!$
!n         # Some integer n
```

### Description {.unnumbered .unlisted}

*Note: stolen from typesetters, Unix folks pronounce "!" as "bang".*

If you use the [`history`]{#man-history} command, you can look back at
previous commands and substitute them into current commands, or just run
them directly.

* `!!`: substitute the previous command here.
* `!*`: substitute all of the arguments to the previous command here.
* `!$`: substitute the last argument from the previous command here.
* `!-n`: substitute the _n_^th^ previous command here.
* `!n`: substitute the command at history index _n_ here.

These are substitutions, i.e. the `!` portion of the command is
completely replaced by whatever it refers to:

``` {.default}
$ echo foo
  foo
$ echo one !* three
  one foo three
```

In that example, `echo` is completely unaware that the substitution took
place; the shell does it before `echo` is run.

Also, after the substitution the shell typically prints out the command
it is running before it runs it. So the previous example would more
typically appear on the terminal as:

``` {.default}
$ echo one !* three
  echo one foo three
  one foo three
```

### Example {.unnumbered .unlisted}

Running the previous command:

``` {.default}
$ ls
  foo   bar   baz
$ !!
  ls
  foo   bar   baz
$ !! ba*
  ls ba*
  bar   baz
```

Running specific commands in the history by index number:

``` {.default}
$ history
   1027  ls /etc
   1028  cd ..
   1030  echo "fun"
   1029  man ls
$ !1030
  echo "fun"
  fun
```

Or you can run them by negative index numbers, referring to the
_n_^th^-previous command:


``` {.default}
$ history
   1027  ls /etc
   1028  cd ..
   1030  echo "fun"
   1029  man ls
$ !-4
  ls /etc
  [omitted]
```

You can also substitute all the previous command's arguments in to this
command with `!*`:

``` {.default}
$ echo foo bar
  foo bar
$ ls -l !*
  ls -l foo bar
  ls: cannot access 'bar': No such file or directory
  -rwxr-xr-x 1 beej beej 3975856 Jun 17 16:40 foo
```

In that example, the `!*` was replaced by the shell with the arguments
to the previous (`echo`) command. It had two arguments `foo` and `bar`,
and so the new command (which the shell printed out for us was:

``` {.default}
ls -l foo bar
```

Then it tried to run it, and `ls` complained that there was no `bar`
file, but showed me the `foo` file without hassle.

### See Also {.unnumbered .unlisted}

[`!` (negation)](#man-bang),
[`history`](#man-history)

<!-- ================================================================ -->

[[manbreak]]
## `!` (negation) {#man-bang}

Negate the exit status of a command.

^POSIX^ 
^BUILT-IN^
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
! command
```

### Description {.unnumbered .unlisted}

*Note: stolen from typesetters, Unix folks pronounce "!" as "bang".*

If the command has a non-zero (failure) exit status, make it so it has a
zero (success) exit status.

If it has a zero (success) exit status, make it so it has a non-zero
(failure) exit status.

Basically we're just being difficult.

This is most commonly used with `if` statements to check if something
hasn't happened. The modified exit status will also appear in the `$?`
environment variable.

**NOTE:** the space after this `!` is very important! It's how the shell
can differentiate it from [`!` (history)](#man-bang-history).

### Example {.unnumbered .unlisted}

Usage with `if`:

``` {.default}
if ! grep foo bar.txt; then
    echo "couldn't find foo in bar.txt"
fi

if ! [ 1 -eq 2 ]; then
    echo "thankfully 1 still does not equal 2"
fi
```

Checking exit status:

``` {.default}
$ ls nonexistent_file
  ls: cannot access 'nonexistent_file': No such file or directory
$ echo $?
  2
$ ! ls nonexistent_file
  ls: cannot access 'nonexistent_file': No such file or directory
$ echo $?
  0
$ ls foo
  foo
$ echo $?
  0
$ ! ls foo
  foo
$ echo $?
  1
```

### See Also {.unnumbered .unlisted}

[`!` (history)](#man-bang-history),
[`if`](#man-if),
[Variables](#man-variables),
[`until`](#man-until),
[`while`](#man-while)

