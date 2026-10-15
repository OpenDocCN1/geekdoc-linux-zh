working directory, with everything below your **$HOME** shortened to a "~" character. That’s a lot easier than some of the ways you have to accomplish this in other shells.

We’ll revisit this topic again in the X Windows section to show you a neat trick you can do with your terminal display windows and your shell prompt as well.

# TEXT EDITORS

# What text editors does a standard Linux system offer me?

Linux does not ship with vi. What it has instead is a value-added replacement called **vim**. **vim** adds a lot to vi such as an optional graphical interface, multiple subwindows, multiple levels of undo, and lots of other nifty features. On most normal Linux installations, vi is just a symbolic link to **vim**, so typing vi will get you vim anyway.

You probably won’t notice the difference unless you really push the limits of vi, in which case you’ll probably really like the added capabilities of **vim**. Just in case you don’t, you can can lobotomize **vim** to operate in strict vi mode. Take a few minutes to explore vim’s online help by typing **:h** once you’re in it.

Most Linux distributions also include **emacs**, and some even come with **Xemacs**. Both the GNU version of **emacs** and the graphically (and functionally) enhanced **Xemacs** are fully supported under Linux with little or no change in functionality.

# LINUX AND X WINDOWS

# Can I have a graphical user interface on Linux?

Yes. As you’ve already seen, UNIX has its very own graphical interface, X Windows, which, while very powerful and very customizable, can also be very confusing. Some of the confusion arises because of the disconnection between the graphics subsystem and the window manager. PC-based graphical interfaces such as Windows95, the Macintosh OS,