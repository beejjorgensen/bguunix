# Foreword
<!-- Beej's guide to Using Unix
# vim: ts=4:sw=4:nosi:et:tw=72
-->

<!-- No hyphenation -->
<!-- [nh[scalbn]] -->

<!-- Index see alsos -->
<!--
[is[Git Log==>see Log]]
[is[Recursion==>see Recursion]]
-->

You just opened a "terminal", whatever that is, and you see something
like this with a blinking cursor:

``` {.default}
$ █
```

Wow. This ain't your parents' computer! (But it might be your
grandparents'!)

What do you do now? There are no windows and the mouse doesn't seem to
help. And yet this humble interface gives you _full control_
(_bwahahah_, well, for some definitions of "full control") over your
computer. Everything you can do with your mouse in terms of creating
folders, moving files, and changing settings can be done through this
text-based interface.

And here's the thing: after you get used to it, you might find that
using the computer from this terminal window is faster than using a GUI
and can afford even more control over the system.

We're going to talk about all this in the context of the Unix operating
system. But we're going to keep it general enough that it largely
applies to Unix, BSD, Linux, MacOS, WSL, Hurd, Ultrix, or whatever
flavor of Unix-like you're running. And if someone says you'll need to
use "Bash", then yes, you're in the right place!

## Audience

[i[Audience]]

Undergrad students just getting into programming are the people I had in
mind while writing this. So give-or-take a bit around that target
audience. People in high school or just looking to learn how to program
are also probably out there in the audience, as well.

## Official Homepage

[i[Home page]]

This official location of this document is:

[fl[`https://beej.us/guide/bguunix/`|https://beej.us/guide/bguunix/]].

## Corrections

[i[Corrections to the Guide]]

I make these guides available for free in the sincere hope that people
will find them maximally useful. If there's something that's not
maximally useful (or, you know, "wrong"), I'd love to hear about it so I
can fix it in furtherance of my mission.

* [fl[Email me|mailto:beej@beej.us]]
* [fl[Report an issue|https://github.com/beejjorgensen/bguunix/issues]]
* [fl[Submit a pull request|https://github.com/beejjorgensen/bguunix]]

Thank you!

## Email Policy

[i[Emailing Beej]]

I'm generally available to help out with email questions so feel free to
write in, but I can't guarantee a response. I lead a pretty busy life
and there are times when I just can't answer a question you have. When
that's the case, I usually just delete the message. It's nothing
personal; I just won't ever have the time to give the detailed answer
you require.

As a rule, the more complex the question, the less likely I am to
respond. If you can narrow down your question before mailing it and be
sure to include any pertinent information (like platform, compiler,
error messages you're getting, and anything else you think might help me
troubleshoot), you're much more likely to get a response.

If you don't get a response, hack on it some more, try to find the
answer, and if it's still elusive, then write me again with the
information you've found and hopefully it will be enough for me to help
out.

Now that I've badgered you about how to write and not write me, I'd just
like to let you know that I _fully_ appreciate all the praise the guide
has received over the years. It's a real morale boost, and it gladdens
me to hear that it is being used for good! `:-)` Thank you!

## Mirroring

[i[Mirroring]]

You are more than welcome to mirror this site, whether publicly or
privately. If you publicly mirror the site and want me to link to it
from the main page, drop me a line at
[`beej@beej.us`](mailto:beej@beej.us).

## Note for Translators

[i[Translations]]

If you want to translate the guide into another language, write me at
[`beej@beej.us`](mailto:beej@beej.us) and I'll link to your translation
from the main page. Feel free to add your name and contact info to the
translation.

Please note the license restrictions in the Copyright and Distribution
section, below.

## Copyright and Distribution

[i[Distributing the Guide]]

Beej's Guide to Using Unix is Copyright © 2025 Brian "Beej Jorgensen"
Hall.

With specific exceptions for source code and translations, below, this
work is licensed under the Creative Commons Attribution-Noncommercial-No
Derivative Works 3.0 License. To view a copy of this license, visit:

[`https://creativecommons.org/licenses/by-nc-nd/3.0/`](https://creativecommons.org/licenses/by-nc-nd/3.0/)

or send a letter to Creative Commons, 171 Second Street, Suite 300, San
Francisco, California, 94105, USA.

One specific exception to the "No Derivative Works" portion of the
license is as follows: this guide may be freely translated into any
language except English, provided the translation is accurate, and the
guide is reprinted in its entirety. The same license restrictions apply
to the translation as to the original guide. The translation may also
include the name and contact information for the translator.

The programming source code presented in this document is hereby granted
to the public domain, and is completely free of any license restriction.

Educators are freely encouraged to recommend or supply copies of this
guide to their students.

Contact [`beej@beej.us`](mailto:beej@beej.us) for more information.

## Dedication

The hardest things about writing these guides are:

* Learning the material in enough detail to be able to explain it
* Figuring out the best way to explain it clearly, a seemingly-endless
  iterative process
* Putting myself out there as a so-called _authority_, when really
  I'm just a regular human trying to make sense of it all, just like
  everyone else
* Keeping at it when so many other things draw my attention

A lot of people have helped me through this process, and I want to
acknowledge those who have made this book possible.

* Everyone on the Internet who decided to help share their knowledge in
  one form or another. The free sharing of instructive information is
  what makes the Internet the great place that it is.
* Everyone who submitted corrections and pull-requests on everything
  from misleading instructions to typos.

Thank you! ♥

UNIX® is a registered trademark of The Open Group.
