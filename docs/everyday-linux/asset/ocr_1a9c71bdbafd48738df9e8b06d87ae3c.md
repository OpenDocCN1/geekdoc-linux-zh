# ## What Is a Terminal?

The terminal is sometimes called the “console.” (When we installed Linux, there was a component called “console multimedia.” This component contains programs that will play sound files and movies from the command line.) You will find that both of these terms, that is, terminal and console, are used imprecisely.

Precisely speaking, defining a terminal isn’t the easiest of tasks. Monitors connected to a computer through a network are called terminals. Your library probably makes use of these terminals to hold its card-catalog database.

The word *terminal* is also often used as shorthand for *terminal emulation*. Terminal emulation is essentially a keyboard “map” that a remote computer uses to ensure that what you type on the keyboard is what you see on the screen. (It’s called a *map* because it maps out the keys on the keyboard so that the terminal knows how to react when you press a button like the tab key, for instance.) Examples of such terminal emulations are VT-xxx (52, -100, -202, -220, and so on), ANSI, and others. The most commonly used text-based terminal is VT-100.

We have been using the word “terminal” in the context of a window that allows you access to the command-line interface. This is sometimes called a *virtual terminal*, since you aren’t actually on a physical terminal on a network, like the terminals on our library network we described above.

You should assume that we use the final definition of terminal, a virtual terminal, when the word is used unless otherwise indicated.

# ## What Is the Command Line?

Before you use the command line, it is helpful to know conceptually what it is and what it can do for you. It is relatively simple to give you a list of commands and say, “This is what they do, now go have fun.” But you will probably learn little from that kind of an example, and it is usually more comfortable to know a little bit about what you’re getting into before you go about doing so.

So what we’d like to do now is point out a few things about the command line, such as what it actually is and what we do with it. Later we’ll look at why you’d even want it, if it seems so esoteric and scary.

The term *command line* is given to describe the interface between you and the computer. It is called a “command-line interface” because you input *com-*