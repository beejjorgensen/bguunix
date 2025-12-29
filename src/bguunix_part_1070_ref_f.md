<!-- ================================================================ -->

[[manbreak]]
## `false` {#man-false}

Exit with a failure status.

^POSIX^ 
^BUILT-IN^
^SCRIPT^

### Synopsis {.unnumbered .unlisted}

``` {.default}
false
```

### Description {.unnumbered .unlisted}

Programs exit with a status code indicating success (`0`) or failure
(non-`0`). This program always exits with a non-zero status.

Generally, the only reason to use this is in scripts when you need
something false-y in Boolean logic.

### Example {.unnumbered .unlisted}

Testing from the command line:

``` {.default}
$ false
$ echo $?      # Print the exit status
  1
```

In scripting, temporarily disable some command:

``` {.default}
false && start_production_database
```

Disable a bunch of lines of code:

``` {.default}
if false; then
    # 50 commands in here are now disabled
fi
```

Force an `else` block:

``` {.default}
if false && grep -q foo bar; then
    # some commands
else
    # this is now forced
fi
```

### See Also {.unnumbered .unlisted}

[`true`](#man-true)

<!-- ================================================================ -->

[[manbreak]]
## `fg` {#man-fg}

Run jobs in the foreground

^POSIX^ 
^BUILT-IN^

### Synopsis {.unnumbered .unlisted}

``` {.default}
fg [job]
```

### Description {.unnumbered .unlisted}

You can run jobs in the background by launching them with an `&` at the
end of the command. You can also suspend jobs by hitting `CTRL-z`.

In any case, if you have a job that's not in the foreground, you can
bring it into the foreground with `fg`. Being "in the foreground" means
that its running as if you just launched it directly from the command
line.

Use the `jobs` command to get a list of jobs, and then identify the job
by a `%` sign followed by the job number.

Or just run `fg` with no arguments to bring the most-recently
backgrounded or suspended job into the foreground.

### Example {.unnumbered .unlisted}

Here I've accidentally hit `CTRL-z` while editing something in Vim,
thereby suspending it. And I want to get back into the editor and get
back to work!

``` {.default}
  zsh: suspended  vim foo.txt
$ jobs
  [1]  + suspended  vim foo.txt
$ fg
```

And then I'm back in Vim as if I'd never left.

Here I'm running a long-lived job (well, faking it by sleeping for 60
seconds). I want to put it in the foreground. Since I have two jobs, I
can be explicit and say I want to foreground job #2.

``` {.default}
$ sleep 60 &
  [2] 16448
$ jobs
  [1]  + suspended  vim foo.txt
  [2]  - running    sleep 60
$ fg %2
  [2]  - running    sleep 60
```

And then I have to wait the remainder of the 60 seconds before I get my
prompt back. (Or I could hit `CTRL-z` to suspend it, then run `bg` to
put it back in the background.)

### See Also {.unnumbered .unlisted}

[`bg`](#man-bg),
[`jobs`](#man-jobs)

<!-- ================================================================ -->

[[manbreak]]
## `file` {#man-file}

Describe what a file is and/or contains.

^POSIX^ 

### Synopsis {.unnumbered .unlisted}

``` {.default}
file filename
```

### Description {.unnumbered .unlisted}

Do you have a file and you want to know what kind of file it is? "Well,
sure, Beej. I just look at the extension, right?"

Sure. But what if the extension is wrong? What if it's missing? What if
you want to know more details than the file name and extension can
provide? The `file` command (probably) has you covered.

This command actually digs into the file a bit to see if it can identify
what it is.

### Example {.unnumbered .unlisted}

What's this mystery file?

``` {.default}
% file sdfhi3i46iosdgoh34iwohiohweosi3o
  sdfhi3i46iosdgoh34iwohiohweosi3o: OpenPGP Public Key Version 4,
  Created Tue Dec  6 15:04:56 2022, RSA (Encrypt or Sign, 4096
  bits); User ID; Signature; OpenPGP Certificate
```

It's a PGP public key!

Here are some straightforward ones:

``` {.default}
$ file some_file.doc
  some_file.doc: Microsoft Word 2007+

$ file susv4-2018.zip
  susv4-2018.zip: Zip archive data, at least v1.0 to extract,
  compression method=store
```

And what about this file that's masquerading as a GIF image?

```
$ file foo.gif
  foo.gif: JPEG image data, JFIF standard 1.01, resolution (DPI),
  density 72x72, segment length 16, comment: "Processed By eBay
  with ImageMagick, z1.1.0. ||B2", baseline, precision 8,
  1440x1080, components 3
```

Surprise, it's a JPEG! Look at all that excellent metadata.

<!--
### See Also {.unnumbered .unlisted}

[`x`](#man-x)
-->

-->
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
