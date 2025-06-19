# Some Background

Before we launch into it, we need to define what _it_ actually is. I
think it's beneficial to hear a little bit of backstory. This will help
you understand why things are they way they are (we're looking at a
modern extension of some very old technology, after all) and allow you
to be more comfortable operating in the medium. I hope. At least it
sounds good.

## In the Beginning

A tiny fraction of moment after the Big Bang, cosmic inflation [_tape
fast-forwarding sounds_] called the _Late Heavy Bombardment_, the Earth
[_more fast-forwarding_] off the Yucatan peninsula was responsible for
[_fast-forwarding_] which allowed data to be stored on inexpensive
cassette tapes [_more fast-forwarding_] finally decoded the first
transmission from intelligent aliens from another world [..._rewinding
noises_] several computer terminals all connected to a single [_STOP
button pressed_].

Great! There we go! Let's start there.

Back in the 1970s, computers were _expensive_. I dug around for some
pricing, and it seems like a basic Digital Equipment Corporation (known
by the acronym _DEC_, or later just _Digital_) PDP-11/40 computer in
1973 cost about $17,000, which is equivalent to $128,000 in 2025
dollars. If you wanted to get all the serious bells and whistles
attached, you could easily push that 2025 cost north of $300K. And don't
forget the $2000/month in maintenance costs on top of that.

(And, yes, your cellphone is 1.21 zillion times more powerful than a
PDP-11/40.)

As such, it made no sense to buy a computer for all your employees.
T'would be madness!

What if we could instead hook up a bunch of cheap screens and keyboards
to that one big _mainframe_ computer? That way we just need to buy the
cheap screen and keyboard for all our employees and they can share the
mainframe. The users could type keystrokes on the keyboard and those
would be transmitted to the mainframe, and anything the mainframe sent
back could be shown on the screen.

The name for the cheap screen and keyboard? It was called a _computer
terminal_, or just a _terminal_ for short.

Keep in mind this is back in the day when virtually no one had their own
personal computer. Apple was just starting out.

> **I could go back farther** before the terminal had a screen. There
> were terminals that used a roll of paper as the "screen" and whatever
> you typed appeared on the paper, as well as the output of any commands
> you requested. These were _teletype terminals_.
>
> These churned through a lot of paper, and were slow, noisy, and prone
> to mechanical failure. They were replaced by screens on so-called
> _video terminals_. Since teletype terminals are now museum pieces,
> saying "video" has become redundant.

These terminals came in a couple varieties: _dumb terminals_ and _smart
terminals_. The dumb ones would just print like a typewriter, a
character at a time, a line at a time, off to infinity. The smart ones
had special control sequences of characters that, once received, would
perform special actions like clearing the screen or moving the cursor to
a specific row and column.

If we just let ourselves roll forward a few years into the 1980s, home
computers were becoming more prevalent. And a lot of them had
modems[^428a] that would allow the computer to communicate with other
computers over the phone network.

[^428a]: Modem is short for _modulator/demodulator_ which is a device
    that could turn data into sound (for transmitting over a phone line)
    and sound back into data (for receiving data over a phone line).
    Search the Internet for "modem sounds" videos if you want to hear
    it.

The computers you communicated with over the modem back then were
commonly either mainframes or BBSes[^6b34]. But in any case, your
computer was acting as a terminal. Of course, your computer could do a
lot of other things besides be a terminal because it was a
general-purpose computer, unlike the hardware terminals of the 1970s.
But you could run a _terminal emulator program_ that pretended to be a
hardware terminal. From the mainframe's perspective, it was
none-the-wiser.

[^6b34]: A _bulletin board system_ (BBS) was a computer running software
    you could connect to with a modem. They typically had ways to post
    public messages for people to see, ways to read those messages, and
    ways to send email to other users. BBSes were almost exclusively
    accessed via phone.

But since hardware terminals are now museum pieces themselves, no one
says the "emulator program" part any longer since it would be redundant.
So we just say "terminal" or "terminal window".

And that's what we have today. When you "open a terminal", you're just
running a terminal emulator program that's pretending to be a hardware
terminal from days of yore.

Also nowadays the terminal doesn't connect to a mainframe by default.
Since your laptop is 3.14 bazillion times more powerful than a PDP-11,
the terminal just connects to the operating system running on your
laptop. And you can open a bunch of terminal windows and they all
connect to your laptop.

> **You can also connect terminal windows to other computers** just like
> the good old days. It's pretty common, actually.

But that's not all there is to the story. It turns out there's one big
piece we still have to talk about: _the shell_.

## The Shell

So the terminal connects to your laptop when you launch the terminal
window, but remember that the terminal just sends your keystrokes to
some program on the laptop and the terminal window just displays
whatever that program sends back.

What is that program?

It can be anything, but by default on every common system is to bring up
a type of program called a _shell_.

The shell is the program that interprets your text commands into things
the system must do. Like a command to move that file from the desktop to
a different folder. Or show me what files are in a folder. Or delete
some files. Or, importantly, run another program.

> **From now on, I'm going to say _directory_ instead of "folder".** In
> this world, folders are called _directories_. And on virtually all
> modern systems, they're the same thing.

Here's how a shell works:

1. Print a prompt, commonly a `$` or a `%`, so that we know it's waiting
   for us to type something
2. Read the user input (i.e. the thing you typed and hit `RETURN` after)
3. If the user wants to quit the shell, exit and we're done; the
   terminal window closes
4. Otherwise try to execute the program the user requested
5. If it fails, print an error
6. If it succeeds, wait for it to complete
7. Go to step 1

That's the core of a shell in a... nutshell.

So you know how with a windowing system like Windows or a Mac or
X[^eb82], you point at things with your mouse and click to get stuff
done? Imagine if you had to type instructions to someone of how to move
the mouse and what to click on. It would still work, right?

[^eb82]: The X Window System is a venerable GUI that's still extremely
    popular on Unix-based systems. I'm using it right now, typing in a
    terminal window. Yes, I'm writing the book in a terminal.

We're going to do the same thing in the shell except the commands we
type are going to be very concise. The drawback is that in order to use
the shell, you must learn the commands and how they work. The good news
is that just a few commands will get you 90% of the way there.

So the story so far is that we have a program called the _terminal_ and
when you launch it you see the output of another program within it
called the _shell_. And the shell is where you type commands that affect
the system. And when the shell exits, the terminal window closes.

You might be wondering if this shell program has a name, and yes, they
are named. And yes, that means there are a lot of shells. In this guide
I'm going to talk about shells that are generally compatible with the
_Bourne Shell_ (the command for which is `sh`). The most popular
variant of this shell used today is the _Bourne Again Shell_ (`bash`).
But also of particular note is the default shell on Macs called the _Z
Shell_ (`zsh`).

In general, everything in this guide will be compatible with all three
of those shells unless otherwise noted.

## Unix and Linux and BSD and...

I've been talking about Unix a lot, but haven't really discussed what it
is.

The short of it is that Unix is an _operating system_ (OS), a sibling to
Windows (running on PCs) and MacOS (running on Macs). The OS is very,
very basically the layer of software between you the user and the
hardware. And I really should say "layers", plural, because it's more
complex than that.

> **The original authors of Unix disliked another OS they were forced to
> use called _Multics_.** So Unix is a bit of a multi-way pun.
> Programmers like puns.

UNIX® is a registered trademark of AT&T, if you can believe it. AT&T has
had its hands in a lot of different businesses over the decades. Unix
was created at [flw[Bell Labs|Bell_Labs]] circa 1970, making it over 50
years old at this point, a testament to its fundamental strength.

In the mid-1970s, hackers in Berkeley started adding features to their
copy of Unix which ultimately resulted in a new fork called the Berkeley
Software Distribution (BSD). They couldn't call it "Unix" because of the
trademark, you see.

Both Unix and BSD branched out into a multitude of subflavors. In fact,
MacOS is a BSD variant! (Windows, is not. While Microsoft did acquire a
license to a Unix variant called Xenix in the late 70s, they chose not
to pursue it and kept us stuck with crappy MSDOS-based operating systems
for years.)

Then from left field, upstart computer science student Linus Torvalds
("LEE-nus") of Finland decided he wanted to run two processes at once on
his brand new 386 PC and started hacking on that. After declaring, upon
initial release of his tiny OS, that it would never amount to anything
big, it grew into the most installed OS in the known Universe[^f6ea].

[^f6ea]: I know I'm going to catch some flak for that, but I'm going to
    throw the Android OS in as a Linux variant. Android has 46% of the
    global market share according to Wikipedia in 2025.

Now, Linux came out of nothing—it's not based on Unix or BSD code. But
it is still a Unix variant. That is, if you're used to using a shell on
Unix or BSD, you're going to feel at home (with minor differences) using
a shell on Linux.

Before we go on, check out [flw[this Unix family tree|History_of_Unix]]
on Wikipedia. (Notably, the impressive tree is incomplete.) Your
impression should be that there are a _lot_ of Unix variants out there,
and they've been morphing since the 1970s. How is it remotely possible
that they still behave in remotely the same way?

This was a big problem—big enough to earn it the name [flw[The Unix
Wars|Unix_wars]]. But finally, after years of waging all out committee,
a standard known as the Portable Operating System Interface (POSIX,
"PAWS-icks", you get the "X" for free) was created. This defines the
minimum possible set of Unix-like functionality an OS must possess in
order to be labeled "POSIX-compliant".

POSIX also defines the minimum set of features a shell must have. `sh`,
`bash`, and `zsh` are POSIX-compliant shells, but have non-POSIX
extensions. Other shells like `csh` and `fish` can also do the same
shell-like things (i.e. you can control the system with them), but their
command language is different and not POSIX.

The one OS you've heard of that is _bona fide_ POSIX-certified is MacOS.
The rest of the Unix variants are mostly POSIX-compliant; when you poke
around in the corners, you'll find minor incompatibilities.

Last and least, let's talk about Windows. After failing to do the right
thing and use Xenix, Microsoft pushed forward with their Windows NT OS
which eventually grew into a respectable beast on its own. But Microsoft
had a problem: software developers liked to use Mac and Unix-like
machines predominantly. As such, a lot of popular software packages were
written specifically for POSIX-like OSes, and Windows couldn't run them.

Microsoft tried a bunch of stuff was tried to add POSIX compatibility
layers, and there was some success. But what they have now landed on is
the _Windows Subsystem for Linux_ (WSL). This system basically runs a
lightweight Linux virtual machine, which means you can open a terminal
window and get a true `bash` shell.

## Distributions

One final optional note on terminology for those thinking of installing
their own Unix-like on their computers: _distributions_. A distribution
is a collection of software that a person or team has put together
around a particular OS core. Yeah, that's vague.

For example, a group of people who like Linux and want it to be more
user-friendly might take a Linux _kernel_ (the core piece of the OS) and
add a bunch of utility programs, a GUI, and other software, bundle it
together with an installation program, and release it to the world.

Here are some Linux distributions, all with different strengths. Ubuntu
and LinuxMint are popular beginner distros. Arch Linux and Gentoo are
popular advanced Linux distros.

* Ubuntu
* LinuxMint
* Debian
* Arch Linux
* OpenSuse
* Gentoo
* Slackware
* Fedora
* Redhat
* Alpine Linux

BSD doesn't really have distributions in quite the same way as Linux.
But the most popular complete BSD OSes you can install are:

* FreeBSD
* OpenBSD
* NetBSD
* DragonFly BSD

