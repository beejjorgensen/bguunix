<!-- ================================================================ -->

[[manbreak]]
## `c99`, `cc`, `gcc`, `clang` {#man-cc}

Run the C compiler.

^POSIX^ 

### Synopsis {.unnumbered .unlisted}

``` {.default}
c99 [-cgo] file [file ... ]
gcc [-cgo] [-Wall] [-Wextra] file [file ... ]
clang [-cgo] [-Wall] [-Wextra] file [file ... ]
```

### Description {.unnumbered .unlisted}

This is the POSIX standard way to run the C compiler. It probably works
on your system. If not, try `gcc`, `clang`, or `cc`.

POSIX says that you'll have the `c99` command at your disposal to do
this, but I don't know anyone who types that. (The "99" means to compile
to the C99 standard from 1999. This sounds old, but in C terms, it's a
relative newcomer.

There are a zillion compiler options, but I'll just name a few.

Use `-o` to specify an output file. By default, the compiler will create
an executable called `a.out`, named for an [flw[ancient binary format no
longer in use|A.out]]—a little bit of history there.

Use `-g` to add debugging symbols to the executable. Do this if you're
going to be running it with a debugger.

Use `-c` to "compile only", that is, don't build an executable, but just
compiler this source to an object file, usually with a `.o` extension.

Use `-Wall` to turn on all warnings. Both `clang` and `gcc` support
this. Highly recommended since warnings are almost always critical
errors in C.

Use `-Wextra` to turn on _even more_ warnings. Also highly recommended
in conjunction with `-Wall`.

### Example {.unnumbered .unlisted}

``` {.default}
$ c99 -o foo foo.c
$ c99 -o foo -g foo.c
$ c99 -c foo.c
$ gcc -o foo -Wall -Wextra foo.c
$ clang -o foo -Wall -Wextra foo.c bar.c baz.c
```

### See Also {.unnumbered .unlisted}

[cc](#man-cc),
[clang](#man-clang),
[gcc](#man-gcc)

<!-- ================================================================ -->

[[manbreak]]
## `cal` {#man-cal}

Print a calendar.

^POSIX^ 

### Synopsis {.unnumbered .unlisted}

``` {.default}
cal [[month] year]
```

### Description {.unnumbered .unlisted}

Prints out a calendar for the month or year (or both) specified. Your
version might do a neat thing like highlight the current day.

### Example {.unnumbered .unlisted}

``` {.default}
$ cal
      July 2025     
Su Mo Tu We Th Fr Sa
       1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30 31      

$ cal 2024
[Output is the calendar for the entire year. Omitted. You'll just
have to trust me on this one. Or try it yourself.]

$ cal 12 1945
    December 1945   
Su Mo Tu We Th Fr Sa
                   1
 2  3  4  5  6  7  8
 9 10 11 12 13 14 15
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30 31               

$ cal 9 1752
   September 1752
Su Mo Tu We Th Fr Sa
       1  2 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29 30
```

You can do some research to see what's going on with that last one,
which might depend on your locale.

### See Also {.unnumbered .unlisted}

[date](#man-date)

<!-- ================================================================ -->

[[manbreak]]
## `cat` {#man-cat}

Concatenate and display files.

^POSIX^ 
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
cat [-u] [file ...]
```

### Description {.unnumbered .unlisted}

The common use case for this is to show a file on the terminal. "Cat the
file," you'll hear it verbed.

You can also use it to concatenate multiple files and show them on the
screen one after another.

It's also used with redirection to take a lot of files and turn them
into a single file.

Use `-u` to cause `cat` to use fast, unbuffered output. This is, in
fact, rarely used, if ever. The GNU `cat` manual page says it's
ignored. I didn't even know about it until I read the spec to put this
page together.

### Example {.unnumbered .unlisted}

Displaying files on the terminal:

``` {.default}
$ cat file1.txt
  This is the content of file 1!

$ cat file1.txt file2.txt file3.txt
  This is the content of file 1!
  This is the content of file 2!
  This is the content of file 3!
```

Making a new file consisting of two other files:

``` {.default}
$ cat file1.txt file2.txt > newfile.txt

$ cat newfile.txt
  This is the content of file 1!
  This is the content of file 2!
```

Catting terminal input back out to the terminal; this is pretty
pointless, but here for demonstration purposes. The user types the first
visible line, and `cat` parrots it back. And then the user types
`CTRL-d` at the end to end the file.

``` {.default}
$ cat
  Hey
  Hey
  Stop copying me
  Stop copying me
  I mean it stop
  I mean it stop
  Gaaah!
  Gaaah!
```

The above example is more useful if you redirect to a file, again
hitting `CTRL-d` on a blank line to end it:

``` {.default}
$ cat > loveletter.txt
  Hey,
  This is a letter I'm typing to demonstrate how cat can save 
  things to a file.
  Love, Beej
```

And then viewing the result:

``` {.default}
$ cat loveletter.txt
  Hey,
  This is a letter I'm typing to demonstrate how cat can save 
  things to a file.
  Love, Beej
```

### See Also {.unnumbered .unlisted}

[grep](#man-grep),
[more](#man-more)

<!-- ================================================================ -->

[[manbreak]]
## `case` {#man-case}

Run one or more commands depending on a value.

^POSIX^ 
^BUILT-IN^
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
case word in
    [(] pattern1 ) compound-list ;;
    [[(] pattern[ | pattern] ... ) compound-list ;;] ...
    [[(] pattern[ | pattern] ... ) compound-list]
esac
```

### Description {.unnumbered .unlisted}

This is a powerful scripting primitive that you can use instead of a
block of `if`-`elif` statements. Basically if a word matches some
pattern, then the corresponding collection of commands is executed. The
collection of commands is terminated with `;;`.

(A non-POSIX Bash extension allows you to terminate the commands with
`;&` to fall through to the next pattern.)

You can have multiple patterns match (as if a Boolean OR) by separating
them with `|` symbols. (This is not to be confused with a pipe! _Ceci
n'est pas une pipe_ in this context!)

The patterns are basically the same as the file globbing rules, with `*`
to match a number of any character, a `?` to match a single of any
character, or `[...]` to match any of a set of characters. The inverse
set can be formed with `[\!...]`.

The first pattern matched will be executed.

And that's a hard to read synopsis; you might just want to jump to the
easier example and then going back to decipher it.

### Example {.unnumbered .unlisted}

[This is likely to appear in a script, not on the command line.]

Read a word from the keyboard and assess it:

``` {.default}
read -r word
case "$word" in
    foo)
        echo "You entered exactly foo"
        ;;

    z*)
        echo "You entered a word that started with z"
        ;;

    x* | *y*)
        echo "Your word starts with x or has a y"
        echo "in it somewhere"
        ;;

    a?t)
        echo "If English, your word is almost certainly"
        echo "act, aft, ant, or art."

    *[aeiou]*)
        echo "Your word contains a vowel."
        ;;

    *[!aeiou])
        echo "Your word does not end with a vowel."
        ;;

    *)
        echo "You entered something else and"
        echo "hit the default case."
esac
```

And you can use the leading optional paren on the patterns which might
make it more readable, though this is less common in my humble
experience:

``` {.default}
case $word in
    (foo)
        echo "You entered exactly foo"
        ;;

    (z*)
        echo "You entered a word that started with z"
        ;;

    (x* | *y*)
        echo "Your word starts with x or has a y"
        echo "in it somewhere"
        ;;

    # etc.
```

### See Also {.unnumbered .unlisted}

[if](#man-if)

<!-- ================================================================ -->

[[manbreak]]
## `cc` {#man-cc}

Run the C compiler.

### Synopsis {.unnumbered .unlisted}

``` {.default}
cc [-cgo] file [file ... ]
```

### Description {.unnumbered .unlisted}

This is the more historic, non-standard way to run the C compiler. It
probably works on your system. If not, try `gcc`, `clang`, or `c99`.

There are a zillion compiler options, but I'll just name a few.

Use `-o` to specify an output file. By default, the compiler will create
an executable called `a.out`, named for an [flw[ancient binary format no
longer in use|A.out]]—a little bit of history there.

Use `-g` to add debugging symbols to the executable. Do this if you're
going to be running it with a debugger.

Use `-c` to "compile only", that is, don't build an executable, but just
compiler this source to an object file, usually with a `.o` extension.

### Example {.unnumbered .unlisted}

``` {.default}
$ cc -o foo foo.c
$ cc -o foo -g foo.c
$ cc -c foo.c
```

### See Also {.unnumbered .unlisted}

[c99](#man-c99),
[clang](#man-clang),
[gcc](#man-gcc)

<!-- ================================================================ -->

[[manbreak]]
## `cd` {#man-cd}

Set the current directory.

^POSIX^ 
^BUILT-IN^

### Synopsis {.unnumbered .unlisted}

``` {.default}
cd [-L|-P] [directory]
cd -
```

### Description {.unnumbered .unlisted}

Instead of being stuck in the same old directory your whole life, why
not try changing directories to another one with `cd`?

You can specify an absolute or relative path, and, provided the named
directory is legit, your new current working directory will be set to
it! High excitement. Think of how boring the world would be without
this. It'd be [flw[CP/M|CP/M]].

One neat special case is that if you just type `cd` and hit `RETURN`,
it'll take you to your home directory. (More specifically, it'll take
you wherever the `HOME` environment variable is set to.)

Another neat special case is if you type `cd -` and hit `RETURN`. This
switches to your previous directory. (More specifically, it'll take you
to whatever the `OLDPWD` environment variable is set to.)

The `-P` and `-L` options are two sides of the same coin. If you use
`-P`, any symbolic links to directories that are encountered will be
expanded to their physical paths. If you use `-L`, they'll be left as
symlinks in the path. The shell defaults to one or the other (usually
`-L`) and you can override that with these switches.

If the directory has spaces in the name, escape or quote them.

What if you find yourself always going to a specific subdirectory, but
it's buried deep in some hierarchy that you're getting tired of typing?
You can set a colon-separated list of parent directories to search in
the `CDPATH` variable.

If your current working directory gets removed by another process while
you're in it, you won't be able to do much. But you can still `cd ..`
(and `cd .`) even though those entries don't technically exist.

### Example {.unnumbered .unlisted}

Basics:

``` {.default}
cd               # Change to home
cd ~             # Change to home with more work
cd -             # Change to previous directory
cd .             # Change to current directory
cd -P .          # Change to current directory, replacing symlinks
cd -L .          # Change to current directory, using symlinks
cd ..            # Change to parent directory
cd /var/spool    # Change to absolute path
cd foo           # Change to relative path
cd foo/bar       # Change to deeper relative path

cd "some directory with spaces in the name"
```

Searching with `CDPATH` in the following example, first `cd` looks in
the current directory for the `foo` subdirectory. If it can't find it
there, it then looks for `~/some/dir/foo`, and if not there, then
`~/some/other/dir/foo`.

``` {.default}
export CDPATH=~/some/dir:~/some/other/dir
cd foo
```

### See Also {.unnumbered .unlisted}

[popd](#man-popd),
[pushd](#man-pushd)

<!-- ================================================================ -->

<!--

[[manbreak]]
## `x` {#man-x}

One line description.

^POSIX^ 
^BUILT-IN^
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
```

### Description {.unnumbered .unlisted}

### Example {.unnumbered .unlisted}

``` {.default}
```

### See Also {.unnumbered .unlisted}

[x](#man-x)

-->
