
## The Getting Started Guide for Red Hat Linux 6.0

(there will be several numbers after 2.2, as in 2.2.2-0.1 or 2.2.5-1).

Now that you've found the kernel version, you can tell the mkbootdisk command which kernel to copy to your floppy. (If you don't tell mkbootdisk where to copy the kernel, it will default to copying to the floppy in /dev/fd0.)

Just type:

```
mkbootdisk --device /dev/fd0 2.2.5-1
```

Then press [Enter].

- Tip: If your screen becomes a little crowded with commands and "command not founds," you can always start with a clean slate by typing clear at the prompt.

You're done.

- Summary: As root, in a terminal window, cd /lib/modules; choose kernel number; then type mkbootdisk --device /dev/fd0 kernel.number. To clean the display, type clear.

## A Good “Man” Is Easy to Find

As you investigate your new system, you’re bound to have questions about commands and system services. One of the easiest ways to find out about how to use many commands or some applications is through the man command. The word man stands for “manual”, a series of online “pages” which can tell you the purpose of many commands. In a highly condensed format, man pages provide a summary of a command’s purpose, the options available and the syntax which is used to issue the command. If you count yourself among the “newbies” to Linux, you might not find man pages as useful as someone who’s more accustomed to their terse delivery of information. But man pages can help steer you toward the proper way to use commands on your system. Even at this point, you can gain insight into your system by familiarizing yourself with the man pages. You’ll certainly want to know how to use them eventually. There are several ways to view the man pages: from GNOME’s Help Browser, from an application called xman or from the shell prompt.

![](img/46f4935125ba89e12897afbe9d77a097_688_0.png)

Figure 15-18: Man page index in GNOME’s Help Browser

GNOME's Help browser: To start GNOME's Help Browser, go to Panel Help system. The GNOME Help Browser will start. On the first page, you'll find links to the man pages and to other helpful documentation.

- Tip: Read about how to get more from GNOME in the GNOME User's Guide, which you'll find at the official GNOME website: www.gnome.org. For more information about man pages, take a look at the Finding Documentation chapter in the Red Hat Linux Installation Guide.

From xman: Depending on your window manager, there will be different ways to access the graphical presentation of the man pages through the menus. (Window managers literally manage how the windows in your X session are presented.) A quick way to start the manual browser, however, is to go to a shell prompt and type:

```
xman
```

which will start the X Window System manual browser. When the menu appears, click on Manual Page. From here, you'll have a number of options from which to find a man page: You can alphabetically display all the man pages on your system; search for them by command or by the section in which they appear. To see the scope of help available, bring up your manual browser, then click on Manual Page then, under Options, click on Display Directory. Here, you'll find the complete list of man pages available to you. From the shell prompt: If you're not in an X session, you can still read the man pages by typing

```
man pagename
```

at the shell prompt. To scroll forward through the document, press [Space]; to scroll back, press [B]. To quit the document, press [Q].

![](img/46f4935125ba89e12897afbe9d77a097_690_0.png)

### Figure 15-19: Reading a man page at the shell prompt

Of course, like any good help system, the man command has its own man page. At the prompt, type

```
man man
```

to display the manual page (as shown in Figure 19).

If you want to print:

Sometimes, just viewing the man page on the screen isn’t enough; you may want to have a printed copy in front of you. Although you could send the page to a printer, because of certain text formatting in the man pages, you’d likely end up with a document filled with “garbage,” symbols which didn’t translate from your screen to the printer.
