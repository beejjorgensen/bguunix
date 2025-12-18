<!-- ================================================================ -->

[[manbreak]]
## `date` {#man-date}

Print out the date and time.

^POSIX^ 
^SCRIPT^ 

### Synopsis {.unnumbered .unlisted}

``` {.default}
date [-u] [+format]
```

### Description {.unnumbered .unlisted}

This prints out the date and time. By default, it's the local time
printed in a semi-standard way.

You can get the Universal Time (UTC, which is basically GMT—forgive me,
time geeks), by giving it the `-u` switch.

The `format` string is more complicated, but it gives you full control
of what's printed. It does this by looking through the string looking
for `%` characters followed by a specific letter, called a _format
specifier_ (I stole that terminology from C). And then it does a
substitution for that specifier, putting something in its place. For
example, if it finds `%Y`, it prints out the current year at that point.
See the examples for more clarity.

Here are all the format specifiers, stolen directly out of the Single
Unix Specification:

|Specifier|Description|
|----|---------------------------------------------------------------------|
|`%a`|Locale's abbreviated weekday name.|
|`%A`|Locale's full weekday name.|
|`%b`|Locale's abbreviated month name.|
|`%B`|Locale's full month name.|
|`%c`|Locale's appropriate date and time representation.|
|`%C`|Century (a year divided by 100 and truncated to an integer) as a decimal number [00,99].|
|`%d`|Day of the month as a decimal number [01,31].|
|`%D`|Date in the format mm/dd/yy.|
|`%e`|Day of the month as a decimal number [1,31] in a two-digit field with leading space character fill.|
|`%h`|A synonym for %b.|
|`%H`|Hour (24-hour clock) as a decimal number [00,23].|
|`%I`|Hour (12-hour clock) as a decimal number [01,12].|
|`%j`|Day of the year as a decimal number [001,366].|
|`%m`|Month as a decimal number [01,12].|
|`%M`|Minute as a decimal number [00,59].|
|`%n`|A newline.|
|`%p`|Locale's equivalent of either AM or PM.|
|`%r`|12-hour clock time [01,12] using the AM/PM notation; in the POSIX locale, this shall be equivalent to %I : %M : %S %p.|
|`%S`|Seconds as a decimal number [00,60].|
|`%t`|A tab.|
|`%T`|24-hour clock time [00,23] in the format HH:MM:SS.|
|`%u`|Weekday as a decimal number [1,7] (1=Monday).|
|`%U`|Week of the year (Sunday as the first day of the week) as a decimal number [00,53]. All days in a new year preceding the first Sunday shall be considered to be in week 0.|
|`%V`|Week of the year (Monday as the first day of the week) as a decimal number [01,53]. If the week containing January 1 has four or more days in the new year, then it shall be considered week 1; otherwise, it shall be the last week of the previous year, and the next week shall be week 1.|
|`%w`|Weekday as a decimal number [0,6] (0=Sunday).|
|`%W`|Week of the year (Monday as the first day of the week) as a decimal number [00,53]. All days in a new year preceding the first Monday shall be considered to be in week 0.|
|`%x`|Locale's appropriate date representation.|
|`%X`|Locale's appropriate time representation.|
|`%y`|Year within century [00,99].|
|`%Y`|Year with century as a decimal number.|
|`%z`|Timezone numeric offset (non-standard).|
|`%:z`|Timezone numeric offset with colon between hours and minutes. (non-standard).|
|`%Z`|Timezone name, or no characters if no timezone is determinable.|
|`%%`|A percent-sign character.|

If you're superuser you can probably use this utility to set the time,
but that's something you should really never have to do on a modern
system.

### Example {.unnumbered .unlisted}

Standard printing of the date and time, both local and UTC:

``` {.default}
$ date
  Sat Oct 25 05:54:44 PM PDT 2025

$ date -u
  Sun Oct 26 12:54:46 AM UTC 2025
```

Using a format string:

``` {.default}
$ date +'The time is %I:%M %p. The year is %Y.'
  The time is 05:39 PM. The year is 2025.
```

Your version of `date` might have a switch to print the time in
[flw[ISO-8601|ISO_8601]] format, but let's do it the hard way for UTC.

``` {.default}
$ date -u +'%Y-%m-%dT%H:%M:%SZ'
  2025-10-26T01:01:20Z
```

Some version of `date` support a timezone extension `%:z` that gives us
what we need to do ISO-8601 for local time:

``` {.default}
$ date +'%Y-%m-%dT%H:%M:%S%:z'
  2025-10-25T18:02:58-07:00
```

<!--
### See Also {.unnumbered .unlisted}

[x](#man-x)
-->

<!-- ================================================================ -->

[[manbreak]]
## `dd` {#man-dd}

Copy and convert files.

^POSIX^ 

### Synopsis {.unnumbered .unlisted}

``` {.default}
dd [operand...]
```

### Description {.unnumbered .unlisted}

This is a rarely used utility, but it is good for copying data a block
at a time. Normally you'd just use `cp`, but `dd` gives you more control
over the input and output. When in doubt, use `cp`.

`dd` also copies a _block_ at a time. The default size of a block is 512
bytes, but you can change it.

The operands that you can use are below, but note that this isn't a
typical command line format for Unix. For example, to copy `foo` to
`bar`, we could run the following, setting the input file name with
`if=` and the output file name with `of=`. That makes a copy, and notice
that `dd` also prints out some accounting information:

``` {.default}
$ dd if=foo.sh of=bar.sh
  0+1 records in
  0+1 records out
  66 bytes copied, 5.4194e-05 s, 1.2 MB/s
```

The output `0+1` means that zero full blocks were read and one partial
block was read (or written). (This was a small file.) It also prints out
the total bytes copied, how long it took, and the throughput.

|Operand|Description|
|--------------|-------------------------------------------------------|
|`if=file`|Set the input file.|
|`of=file`|Set the output file.|
|`ibs=expr`|Set the input block size.|
|`obs=expr`|Set the output block size.|
|`bs=expr`|Set both input and output block size.|
|`cbs=expr`|Set conversion block size (for use with `block`, below).|
|`skip=n`|Skip _n_ blocks of input before copying.|
|`seek=n`|Skip _n_ blocks of output before copying.|
|`count=n`|Copy only _n_ input blocks.|
|`conv=value[,value]`|Set the conversion type.|

If the input file is omitted, standard input is used. If the output file
is omitted—guess what—standard output is used.

Block sizes can be specified in bytes (no suffix), kilobytes (`k`
suffix), or multiples of 512 bytes ("blocks") (`b` suffix, because they
want to make this confusing. `b` means "512-byte blocks", not "bytes").

``` {.default}
bs=4096     # 4096 bytes
bs=4k       # 4 kilobytes, 4096 bytes
bs=8b       # 8 blocks of 512 bytes, 4096 bytes
```

And also as the product of two numbers separated by a literal `x`. I'll
bet only 5% of Unix hackers knew about this. I didn't.

``` {.default}
bs=4x1024   # 4 times 1024 = 4096 bytes
bs=4x1k     # 4 times 1 kilobyte = 4096 bytes
bs=2x4b     # 2 times 4 blocks (2048 bytes) = 4096 bytes
```

Some versions of `dd` support other units besides just `k` and `b`.

Finally, that crazy conversion stuff. This gives you more control over
the output, some of it in a very dated way.

|`conv=` operand|Description|
|------|---------------------------------------------------------------|
|`block`|Turn newline-delimited records into flat records, length given by `cbs=`.|
|`unblock`|Turn flat records into newline-delimited records, length given by `cbs=`.|
|`lcase`|Map uppercase letters in input to lowercase in output. Capitalize it!|
|`ucase`|Map lowercase letters in input to uppercase in output. Lowercasize it!|
|`noerror`|Don't give up on error. If `sync` is specified, fill the error block with null bytes. Otherwise, just skip it.|
|`notrunc`|Don't nuke the output file before writing.|
|`sync`|Pad every input block out to the input block size with null bytes (or with spaces if used with `block` or `unblock`).|
|`ascii`|Convert [flw[EBCDIC|EBCDIC]] to ASCII. You won't need this.|
|`ebcdic`|Convert ASCII to EBCDIC. You won't need this.|
|`ibm`|Convert ASCII to IBM EBCDIC. You **will** need this. Just kidding—you won't.|
|`swab`|Swap every pair of bytes. Good for [flw[endianness|Endianness]] swaps, I guess.|

`block` and `unblock` are particularly interesting if you need to
generate flat files (where each record is the same number of bytes). It
pads with spaces, which apparently is how [flw[Fortran|Fortran]] likes
things.

This is an *old* program.

And `ucase` and `lcase` are fun.

And `notrunc` would allow you to "paste" blocks in place in an existing
file. Using `seek` and `skip` allow you to position where you want the
block exactly.

A common use of this is to copy entire raw disks a block at a time. Or
to slice and dice files.

Another use is to create big files full of null bytes by using
`/dev/zero` as the input file.

### Example {.unnumbered .unlisted}

Copy a file:

``` {.default}
$ dd if=input.txt of=output.txt
```

Copy a file specifying block size:

``` {.default}
$ dd if=input.txt of=output.txt bs=4096
```

Convert a file to uppercase, printing it on standard output:

``` {.default}
$ dd if=input.txt conv=ucase
```

Create a 8 KB file (made up of two 4 KB blocks) of null bytes from
`/dev/zero`

``` {.default
$ dd if=/dev/zero of=foo.txt bs=4k count=2
```

Convert a file with newline-delimited TODO

### See Also {.unnumbered .unlisted}

[cp](#man-cp)

<!-- ================================================================ -->

[[manbreak]]
## `df` {#man-df}

Tell you how much free disk you have.

^POSIX^ 

### Synopsis {.unnumbered .unlisted}

``` {.default}
df [-k] [-P] [directory...]
df [-h] [directory...]      # Non-standard
```

### Description {.unnumbered .unlisted}

Do you want to know how much space you have left on this disk before you
download the latest Hollywood movie rip from your favorite pirate
website? `df` has you covered.

By default, it reports the used and free space on all mounted volumes,
which might be more than you're interested in. You can specify a
directory and it'll tell you the information for the volume that
directory is in.

Use `-k` to specify "kilobytes" as the unit. This might or might not be
your default on your system. If it's not, the units are probably
512-byte blocks or 4 kilobyte blocks.

Use the non-standard `-h` for "human" units in the output. It will
automatically select units that are most useful, like "`G`" for
gigabytes or "`T`" for terabytes. Or "`P`" for petabytes if you're
trying to show off.

Lastly, `-P` will show the output in "POSIX-compliance mode" which is a
well-defined standard output format that your system might or might not
use by default.

The output shows several things (any sizes are system- or
option-dependent):

* **Filesystem**: the device file that represents the disk. This might
  be something in `/dev` or it might be a virtual entity like `tmpfs`
  (which is a RAM disk under Linux).
* **Disk size**: Size of the disk.
* **Used space**: Space used. This counts not only file data but also
  the metadata used to store the files.
* **Free space**
* **Percentage in use**: used space over total space.
* **Mount point**: Where in the directory hierarchy this disk is
  mounted, i.e. everything under that directory is stored on this
  particular disk.

### Example {.unnumbered .unlisted}

Example default output on a Linux system:

``` {.default}
$ df
  Filesystem     1K-blocks     Used Available Use% Mounted on
  /dev/nvme0n1p3 470471976 30134004 416365828   7% /
  tmpfs            8116976       12   8116964   1% /tmp
  /dev/nvme0n1p1   1046272    64892    981380   7% /boot
```

Showing the space in kilobytes on the drive `/home` is mounted on:

``` {.default}
$ df -k /home
  Filesystem     1K-blocks     Used Available Use% Mounted on
  /dev/nvme0n1p3 470471976 30134004 416365828   7% /
```

Showing space in (non-standard) human-readable form for the drive the
current directory is mounted on.

``` {.default}
$ df -h .
  Filesystem      Size  Used Avail Use% Mounted on
  /dev/nvme0n1p3  449G   29G  398G   7% /
```

POSIX mode output:

``` {.default}
$ df -P
  Filesystem     1024-blocks     Used Available Capacity Mounted on
  /dev/nvme0n1p3   470471976 30134004 416365828       7% /
  tmpfs              8116976       12   8116964       1% /tmp
  /dev/nvme0n1p1     1046272    64892    981380       7% /boot
```

### See Also {.unnumbered .unlisted}

[du](#man-du),
[free](#man-free)

<!-- ================================================================ -->

[[manbreak]]
## `diff` {#man-diff}

Compare files.

^POSIX^ 

### Synopsis {.unnumbered .unlisted}

``` {.default}
diff [-b] [-c|-C n] [-u|-U n] file1 file2
diff [-q] file1 file2              # Non-standard
```

### Description {.unnumbered .unlisted}

This tells you if two files have identical contents. And, if not, it can
tell you, rather concisely, what the differences are.

`diff` answers the question, "What would I have to change in `file1` in
order to make it look identical to `file2`?"

`-b` ignores whitespace changes and only looks for other text changes.

`-c` gives lines of context, and changes the output format. `-C n`
outputs `n` lines of context (default is 3).

`-u` also gives lines of context, and changes to "unified" output mode.
`-U n` outputs `n` lines of context (default is 3). This is the same
mode that [fl[Git|https://git-scm.com/]] uses.

The non-standard `-q` only checks to see if the files differ. If they
do, a message is printed saying so. This is useful for comparing binary
files where difference output wouldn't be useful to human eyes. The exit
status is also set to non-zero if they differ, which is great in scripts
that have to look for changes in files.

The output format is _interesting_ to say the least. You eventually get
used to it and are able to read it handily. It's line-oriented; it will
basically tell you which lines you'd have to change to turn `file1` into
`file2`.

Oh, wait. Did I say "output _format_"? I mean _formats_. There are three
of them you might encounter.

#### Classic Output

This is the default mode.

Here are two files—see the differences?

``` {.default}
$ cat foo.txt
  This is a test
  And this is file foo
  And a third line
$ cat bar.txt
  This is a test
  And this is file bar
```

In order to edit `foo` and turn it into `bar`, you'd have to change the
second line to read `And this is file bar`. Then `foo` would be the
same.

Let's see `diff` tell us that:

``` {.default}`
$ diff foo.txt bar.txt
  2,3c2
  < And this is file foo
  < And a third line
  ---
  > And this is file bar
```

You can read that as "Line 2 of foo.txt is changed in line 2 of bar.txt"
(that's the `2c2` part).

And anything with a less than is the left file `foo.txt` and a greater
than is the right file `bar.txt`.

So it uses `c` to indicate a changed line, and it also uses `d` for
deleted lines and `a` for added lines.

#### Copied Context Output

You get into this mode by specifying `-c` on the command line. It will
show you differences _in context_, that is, surrounded by lines that are
not different. It gives you a better idea, at a glance, the part of the
file where the diffs are.

Using the same files from the classic format example, above:

``` {.default}
$ diff -c foo.txt bar.txt
  *** foo.txt   2025-12-17 16:39:45.794478870 -0800
  --- bar.txt   2025-12-17 16:30:56.783306931 -0800
  ***************
  *** 1,3 ****
    This is a test
  ! And this is file foo
  ! And a third line
  --- 1,2 ----
    This is a test
  ! And this is file bar
```

It indicates changed lines with `!`, added lines with `+`, and removed
lines with `-`. And we have the line numbers in `foo.txt` and `bar.txt`
shown, as well.

#### Unified Output

As mentioned previously, this is the mode that Git uses.

It's basically the same information as the copied context output, but in
a different format.

Using the same files from the classic format example, above:

``` {.default}
$ diff -u foo.txt bar.txt
  --- foo.txt   2025-12-17 16:39:45.794478870 -0800
  +++ bar.txt   2025-12-17 16:30:56.783306931 -0800
  @@ -1,3 +1,2 @@
   This is a test
  -And this is file foo
  -And a third line
  +And this is file bar
```

Unified mode shows changed lines as a combination of a line delete and
line add. In general, lines prefaced with a `-` are lines you'd have to
delete in `foo.txt` to make it line `bar.txt`, and lines that start with
`+` are lines you'd have to add.

### Example {.unnumbered .unlisted}

Here's a more complex example in classic output:

``` {.default}
$ diff foo2.txt bar2.txt
  1c1,2
  < Paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1
  ---
  > Changed this line. And deleted two lines from the second
  > paragraph.
  8,9d8
  < paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2
  < paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2
  19a19
  > And added this line in paragraph 4
```

``` {.default}
% diff -c foo2.txt bar2.txt
*** foo2.txt	2025-12-17 17:23:08.856329098 -0800
--- bar2.txt	2025-12-17 17:22:47.690559025 -0800
***************
*** 1,12 ****
! Paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1
  paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1
  paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1
  paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1

  Paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2
  paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2
- paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2
- paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2

  Paragraph 3 paragraph 3 paragraph 3 paragraph 3 paragraph 3
  paragraph 3 paragraph 3 paragraph 3 paragraph 3 paragraph 3
--- 1,11 ----
! Changed this line. And deleted two lines from the second
! paragraph.
  paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1
  paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1
  paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1

  Paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2
  paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2

  Paragraph 3 paragraph 3 paragraph 3 paragraph 3 paragraph 3
  paragraph 3 paragraph 3 paragraph 3 paragraph 3 paragraph 3
***************
*** 17,19 ****
--- 16,19 ----
  paragraph 4 paragraph 4 paragraph 4 paragraph 4 paragraph 4
  paragraph 4 paragraph 4 paragraph 4 paragraph 4 paragraph 4
  paragraph 4 paragraph 4 paragraph 4 paragraph 4 paragraph 4
+ And added this line in paragraph 4
```

``` {.default}
% diff -u foo2.txt bar2.txt
--- foo2.txt	2025-12-17 17:23:08.856329098 -0800
+++ bar2.txt	2025-12-17 17:22:47.690559025 -0800
@@ -1,12 +1,11 @@
-Paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1
+Changed this line. And deleted two lines from the second
+paragraph.
 paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1
 paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1
 paragraph 1 paragraph 1 paragraph 1 paragraph 1 paragraph 1

 Paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2
 paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2
-paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2
-paragraph 2 paragraph 2 paragraph 2 paragraph 2 paragraph 2

 Paragraph 3 paragraph 3 paragraph 3 paragraph 3 paragraph 3
 paragraph 3 paragraph 3 paragraph 3 paragraph 3 paragraph 3
@@ -17,3 +16,4 @@
 paragraph 4 paragraph 4 paragraph 4 paragraph 4 paragraph 4
 paragraph 4 paragraph 4 paragraph 4 paragraph 4 paragraph 4
 paragraph 4 paragraph 4 paragraph 4 paragraph 4 paragraph 4
+And added this line in paragraph 4
```

``` {.default}
$ diff -q foo2.txt bar2.txt
  Files foo2.txt and bar2.txt differ
```

### See Also {.unnumbered .unlisted}

[patch](#man-patch)

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

[x](#man-x)

-->
