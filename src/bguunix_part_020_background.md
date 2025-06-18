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

[^428a] Modem is short for _modulator/demodulator_ which is a device
that could turn data into sound (for transmitting over a phone line) and
sound back into data (for receiving data over a phone line). Search the
Internet for "modem sounds" videos if you want to hear it.

The computers you communicated with over the modem back then were
commonly either mainframes or BBSes[^6b34]. But in any case, your
computer was acting as a terminal. Of course, your computer could do a
lot of other things besides be a terminal because it was a
general-purpose computer, unlike the hardware terminals of the 1970s.
But you could run a _terminal emulator program_ that pretended to be a
hardware terminal. From the mainframe's perspective, it was
none-the-wiser.

[^6b34] A _bulletin board system_ (BBS) was a computer running software
you could connect to with a modem. They typically had ways to post
public messages for people to see, ways to read those messages, and ways
to send email to other users. BBSes were almost exclusively accessed via
phone.

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
2. Read the user input
3. If the user wants to quit the shell, exit and we're done
4. Otherwise try to execute the program the user requested
5. If it fails, print an error
6. If it succeeds, wait for it to complete
7. Go to step 1

TODO

## Unix and Linux and BSD and...

TODO

