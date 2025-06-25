# Running Programs

We've already been running programs like `ls`, `rm`, and `mkdir`. That
was easy!

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
a way to modify the behavior of the command.

The general pattern is:

``` {.default}
$ command options arguments
```

When the command runs, it processes the options and arguments (which,
collectively, are referred to as the _command line arguments_) and
decides what to do based on them.

TODO


## Directory Listings

TODO


## The Manual
