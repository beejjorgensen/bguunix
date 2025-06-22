[[manbreak]]
## `alias` {#man-alias}

Make an alias for a command.

^POSIX^ 
^BUILT-IN^

### Synopsis {.unnumbered .unlisted}

``` {.default}
alias [ alias-name[=string] ... ]
```

### Description {.unnumbered .unlisted}

Let's say you're always running `ls -la`. And you're tired of typing it.
And you wish that you could just type `lla` instead.

Well, let `alias` make your life easier! It allows you to make up a new
command that runs the old complex one instead.

Aliases are substitutions to the command line that take place before any
programs are run. So with an `lla` alias that meant `ls -la`, running
this:

``` {.default}
$ lla foo.txt
```

would have the alias substituted in to be:

``` {.default}
$ ls -la foo.txt
```

If the alias has a space at the end, something special happens: the next
word is examined to see if it is also an alias, and it is expanded, too.
Putting a space at the end is a way to indicate that the next word might
be a macro in a sequence.

If you leave off the part after the `=`, you'll be shown the value of
the alias.

And if you give no arguments, you'll be shown all the aliases.

Aliases are commonly written using single quotes to prevent the shell
from expanding them when they're defined; that said, they just follow
the normal quoting rules.

Finally, aliases are very commonly defined in your RC file so that they
persist after the shell exits.

### Example {.unnumbered .unlisted}

Some straightforward aliases:

``` {.default}
alias lla='ls -la'
alias server='ssh beej@some.long.name.server.example.com'
```

A continuation alias (note the space at the end):

``` {.default}
alias ll='ls -l '
alias all='-a '
```

This allows you to run:

``` {.default}
$ ll all foo.* bar.txt
```

Without the continuation, it would just look for the file called `all`.

Viewing alias values:

``` {.default}
$ alias ll       # View single alias
  ll='ls -l'

$ alias          # View all aliases
  all='-a '
  ll='ls -l'
```

### See Also {.unnumbered .unlisted}

[set](#man-set)

<!-- ================================================================ -->

[[manbreak]]
## `ar` {#man-ar}

Manipulate library archives.

^POSIX^ 

### Synopsis {.unnumbered .unlisted}

``` {.default}
ar -rc archive file ...
```

### Description {.unnumbered .unlisted}

This is actually a pretty powerful tool for maintaining static libraries
for linking to executables. It's mainly of use to C and C++ devs.

If that's Greek to you, then you probably don't need this.

It actually does way more than I'm letting on in the synopsis, above,
but that's how you create a basic static library. Check out the `man`
page if you need more power.

### Example {.unnumbered .unlisted}

This example builds a static library made up a number of object files
and then links it to a `main.o` object file with `gcc`.

``` {.default}
$ ar -rc mylib.a add.o sub.o mult.o div.o  # Make the library
$ gcc -o mycalc main.o mylib.a             # Link to it
```

### See Also {.unnumbered .unlisted}

[gcc](#man-gcc),
[cc](#man-cc)

<!-- ================================================================ -->

[[manbreak]]
## `awk` {#man-awk}

Run the AWK programming language.

^POSIX^ 

### Synopsis {.unnumbered .unlisted}

``` {.default}
awk '[AWK program]' [ file [ file ... ] ]
awk -f program.awk [ file [ file ... ] ]
```

### Description {.unnumbered .unlisted}

AWK is a full-blown language that I can't possibly do justice to here.
It's very fast and powerful for processing text.

But the main thing people use it for is extracting columns of data from
files.

You can write AWK scripts and have it run those, as well, but that's
beyond the scope of what I want to get into here.

The quick and dirty way is to throw a script on the command line

You can set the field separator with `-F`. Multiple separators are
turned into a single separator when the file is processed; that is, if
there are a bunch of spaces between fields, it's the same as if there
were only one space. The separator can be multiple characters, too. The
field separator is whitespace by default.

Also, if you have your AWK program in another file, you can tell `awk`
to use it with `-f`.

This reference page just scratches the surface. If you're doing a lot of
structured data processing, definitely learn more about what AWK can do
for you.

### Example {.unnumbered .unlisted}

Take a simple CSV file and output just the first and third fields with a
space between them:

``` {.default}
$ awk -F, '{ print $1 " " $3 }' foo.csv
  a1 a3
  b1 b3
  c1 c3
```

Add up the total number of bytes in all files outputted by `ls -la`:

``` {.default}
$ ls -la | awk '{ t += $5 } END { print t " bytes" }'
  969002 bytes
```

Or the same thing if you have the AWK program in the file `foo.awk`:

``` {.default}
$ ls -la | awk -f foo.awk
  969002 bytes
```

### See Also {.unnumbered .unlisted}

[cut](#man-cut)

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
