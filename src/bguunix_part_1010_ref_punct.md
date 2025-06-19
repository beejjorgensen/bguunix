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
!3490
!-2
```

### Description {.unnumbered .unlisted}

*Note: stolen from typesetters, Unix folks pronounce "!" as "bang".*

If you use the nonstandard [`history`]{#man-history} command, you can
look back at previous commands and substitute them into current
commands, or just run them directly.

You can run the previous command again with:

``` {.default}
$ !!
```

Really, though, what this does is just replace the `!!` with whatever
command you ran last and then process it as normal when you hit
`RETURN`.

You can run specific commands from your past. For example, if I have
this in my history:

``` {.default}
$ history
 1027  ls /etc
 1028  cd ..
 1030  echo "fun"
 1029  man ls
```

I can rerun the `echo` command in one of two ways:

``` {.default}
$ !1030       # Run specifically history index 1030
$ !-2         # Run the command from two commands ago
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

Similarly you can substitute `!$` which is just replaced with the final
argument from the previous command.

### See Also {.unnumbered .unlisted}

[`!` (negation)](#man-bang)

<!-- ================================================================ -->

[[manbreak]]
## `!` (negation) {#man-bang}

Negate the sense of a conditional.

^POSIX^ 
^BUILT-IN^
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
if ! grep foo bar.txt; then
    echo "couldn't find foo in bar.txt"
fi

if ! [ 1 -eq 2 ]; then
    echo "thankfully 1 still does not equal 2"
fi
```

### Description {.unnumbered .unlisted}

*Note: stolen from typesetters, Unix folks pronounce "!" as "bang".*

### See Also {.unnumbered .unlisted}
[`!` (history)](#man-bang-history)

