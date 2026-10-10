Lisp already; the few exceptions could have been written in Lisp but were written in C for efficiency. Although only a programmer can write an extension, anybody can use it afterward.

When run under the X Window System (started as **emacs**) Emacs provides its own menus and convenient bindings to mouse buttons. But Emacs can provide many of the benefits of a window system on a text-only terminal. For instance, you can look at or edit several files at once, move text between files, and edit files while running shell commands.

# 6.1.2.3 Vi(m)

Vim stands for "Vi IMproved". It used to be "Vi IMitation", but there are so many improvements that a name change was appropriate. Vim is a text editor which includes almost all the commands from the UNIX program **vi** and a lot of new ones.

Commands in the **vi** editor are entered using only the keyboard, which has the advantage that you can keep your fingers on the keyboard and your eyes on the screen, rather than moving your arm repeatedly to the mouse. For those who want it, mouse support and a GUI version with scrollbars and menus can be activated.

We will refer to **vi** or **vim** throughout this book for editing files, while you are of course free to use the editor of your choice. However, we recommend to at least get the **vi** basics in the fingers, because it is the standard text editor on almost all UNIX systems, while **emacs** can be an optional package. There may be small differences between different computers and terminals, but the main point is that if you can work with **vi**, you can survive on any UNIX system.

Apart from the **vim** command, the **vim** packages may also provide **gvim**, the Gnome version of **vim**. Beginning users might find this easier to use, because the menus offer help when you forgot or don't know how to perform a particular editing task using the standard **vim** commands.

# 6.2 Using the Vim editor

# 6.2.1 Two modes

The **vi** editor is a very powerful tool and has a very extensive built-in manual, which you can activate using the **help** command when the program is started (instead of using **man** or **info**, which don't contain nearly as much information). We will only discuss the very basics here to get you started.

What makes **vi** confusing to the beginner is that it can operate in two modes: command mode and insert mode. The editor always starts in command mode.