# Launching the Terminal

## MacOS

This is the easiest.

1. Hit `CMD-SPACE`.
2. Type `terminal`.
3. Choose "Terminal" from the command list and run it.

You should also drag it down to the dock since you'll be running it
frequently.

And you're in! There's the shell prompt. Jump to [exiting the
terminal](#exiting1), below.

## Windows

This is the hardest, but we'll cover it in more detail as we need to.

If you're going to learn Unix on Windows, I recommend one of two things:

1. [fl[Install
   WSL|https://learn.microsoft.com/en-us/windows/wsl/install]]
   (**Recommended**).
2. [fl[Install Git Bash|https://git-scm.com/downloads/win]], part of the
   Git version control system.

If you're ever going to have to do a Unix or OS programming class in
school, you're going to need WSL anyway, so do that even though it's the
harder of the two ways.

Git Bash will get you enough to get back when learning about the
terminal and the shell.

You can easily install them both, but later we'll see they live in
different worlds.

To launch WSL:

1. Hit the Windows key.
2. Type "ubuntu".
3. Launch "Ubuntu (app)". If you installed another distro besides the
   default Ubuntu, type that instead.

To launch Git Bash:

1. Hit the Windows key.
2. Type "git".
3. Launch "Git Bash (app)".

## Unix-likes

These vary depending on how you have them configured, so it's hard to
give the definitive set of instructions. But it's common that you can
right-click on the desktop and there will be a shell option in the
context menu.

And certainly there are more ways to open them than that. I open shells
so frequently I bound `SHIFT-F1` to that action to make it as effortless
as possible.

## Exiting the terminal {#exiting1}

At the shell prompt, hit `CTRL-d` or type `exit` and hit `RETURN`.
Either one will cause the shell to exit.

Depending on your configuration, the terminal window might instantly
close, or it might need to be manually closed.
