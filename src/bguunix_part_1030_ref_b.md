[[manbreak]]
## `basename` {#man-basename}

Return only the file name part of a path, optionally stripping the
extension.

^POSIX^ 
^BUILT-IN^
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
basename string [suffix]
```

### Description {.unnumbered .unlisted}

Given a path like `/foo/bar/baz.gif`, the `basename` utility allows you
to strip away the leading path part and optionally some trailing part
like the extension.

The path can be absolute or relative.

### Example {.unnumbered .unlisted}

Example of stripping off the path:

``` {.default}
$ basename /foo/bar/baz.gif
  baz.gif

$ basename bar/baz.gif
  baz.gif
```

Example stripping off paths and suffixes:

``` {.default}
$ basename /foo/bar/baz.gif .gif
  baz

$ basename footwear wear
  foot
```

Example script to convert a bunch of GIFs to JPEGs with [fl[Image
Magick|https://imagemagick.org/]]:

``` {.default}
for f in *.gif; do
    magick "$f" "$(basename "$f" .gif).jpg"
done
```

A risky way to depluralize a string:

```
$ gimme=treats          # What my dog wants
$ basename "$gimme" s   # What my dog gets
  treat
```

### See Also {.unnumbered .unlisted}

[`dirname`](#man-dirname)

<!-- ================================================================ -->

[[manbreak]]
## `bash` {#man-bash}

The Bourne Again Shell

### Synopsis {.unnumbered .unlisted}

``` {.default}
bash
bash [-x] scriptname
```

### Description {.unnumbered .unlisted}

Runs a new instance of the Bash shell. This reference page barely tells
you anything about what the shell can do because that's a book in
itself. Such as this one.

It can also run the given Bash script. The `-x` option causes each line
of the script to be outputted before execution, which can be used for
quick-and-dirty debugging.

You can exit the shell with `CTRL-D` or `exit`.

### Example {.unnumbered .unlisted}

Run another bash shell:

``` {.default}
$ bash
```

Run a shell script 
``` {.default}
$ bash scriptname
$ bash -x scriptname
```

### See Also {.unnumbered .unlisted}

[`sh`](#man-sh),
[`zsh`](#man-zsh)

<!-- ================================================================ -->

[[manbreak]]
## `bc` {#man-x}

Arbitrary-precision calculator.

^POSIX^ 
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
bc [-l] [file]
```

### Description {.unnumbered .unlisted}

This is a neat calculator in that in can do arbitrary-precision
arithmetic and other functions.

(It's actually a full-fledged language, amazingly, and is more than I
want to get into here. But [fl[Bosko Marijan has a good
tutorial|https://phoenixnap.com/kb/linux-bc]].)

And yes, the shell can do math with the `$(())` substitution, but that's
not guaranteed to be anything other than integer. If you want to be
portable and do floating point math, do it with `bc`.

The `-l` option sets the precision to 20 (instead of 0) decimal places
and loads up some math libraries. `bc -l` is probably what you want.

You can set the scale (precision) with the `scale` variable, e.g.
`scale=100`.

Expected operators for arithmetic all work (`+`, `-`, `/`, `*`, `%`,
parentheses) and a variety of other math functions are also available
when run with `-l`. Check out the `man` page for details.

### Example {.unnumbered .unlisted}

You can just get answers by typing on standard input and it'll print to
standard output:

``` {.default}
$ bc -l
  5-3
  2
  4*(1+3)
  16
```

If I have a file `foo.bc` that contains the following:

``` {.default}
1+2*3
1/2+3
```

I can run it and get the results like so:

``` {.default}
$ bc -l foo.bc < /dev/null
  7
  3.50000000000000000000
```

(If we don't redirect input from `/dev/null` there, it keeps waiting for
standard input after doing the work instead of exiting.)

In a script, computing a floating point result of $327.79\times 123.4$:

``` {.default}
input=327.79
result=$(echo $input '*' 123.4 | bc -l)
printf "result is %f\n" "$result"   # 40449.286000
```

First 1000 digits of $\pi$, which is $4\cdot\arccos(1)$:

``` {.default}
$ bc -l
  scale=1000
  4*a(1)
  3.141592653589793238462643383279502884197169399375105820974944592\
  30781640628620899862803482534211706798214808651328230664709384460\
  95505822317253594081284811174502841027019385211055596446229489549\
  30381964428810975665933446128475648233786783165271201909145648566\
  92346034861045432664821339360726024914127372458700660631558817488\
  15209209628292540917153643678925903600113305305488204665213841469\
  51941511609433057270365759591953092186117381932611793105118548074\
  46237996274956735188575272489122793818301194912983367336244065664\
  30860213949463952247371907021798609437027705392171762931767523846\
  74818467669405132000568127145263560827785771342757789609173637178\
  72146844090122495343014654958537105079227968925892354201995611212\
  90219608640344181598136297747713099605187072113499999983729780499\
  51059731732816096318595024459455346908302642522308253344685035261\
  93118817101000313783875288658753320838142061717766914730359825349\
  04287554687311595628638823537875937519577818577805321712268066130\
  019278766111959092164201988
```

### See Also {.unnumbered .unlisted}

[Variables](#man-variables)

<!-- ================================================================ -->

[[manbreak]]
## `bg` {#man-bg}

Move a stopped job into the background.

^POSIX^ 
^BUILT-IN^

### Synopsis {.unnumbered .unlisted}

``` {.default}
bg [ job_id ... ]
```

### Description {.unnumbered .unlisted}

If you have a job running in the foreground, like something long-lived
that you don't want to wait for called `foo`, you can temporarily stop
that job by hitting `CTRL-Z`. When I do this in Zsh, it says `zsh:
suspended  foo` and drops me back at a shell prompt. The `foo` program
still exists, but it's effectively paused at the moment.

To continue that job in the background, you can use the `bg` command.

This allows you to specify a job number (prefaced by `%`) to put in the
background or, if you leave that out, it will just background the most
recently stopped job.

### Example {.unnumbered .unlisted}

Given this set of jobs:

``` {.default}
$ jobs
  [1]  - suspended  ./foo
  [2]  + suspended  ./bar
```

Either of these would continue `./bar` in the background:

``` {.default}
$ bg
$ bg %2
```

And this would continue `./foo` in the background:

``` {.default}
$ bg %1
```

### See Also {.unnumbered .unlisted}

[`fg`](#man-fg),
[`jobs`](#man-jobs)

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

[`x`](#man-x)

-->
