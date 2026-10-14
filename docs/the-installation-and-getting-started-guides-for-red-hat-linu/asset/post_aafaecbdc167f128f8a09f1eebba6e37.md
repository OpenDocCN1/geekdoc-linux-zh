
Windows System when you reboot. If you choose to have X run, GNOME will be the default desktop manager you see.

## Finishing Up...

After you have configured the X Windows System, the installation program will prompt you to prepare your system for reboot (see Figure 6-22). Don't forget to remove any diskette that might be in the diskette drive, or CD that might be in the CD-ROM drive if your system is able to boot from the CD-ROM (unless you decided to skip the standard LILO installation, in which case you'll need to use the boot diskette created during the installation).

![](img/46f4935125ba89e12897afbe9d77a097_161_0.png)

## Figure 6-22: Ready for Reboot

After your computer's normal power-up sequence has completed, you should see LILO's standard prompt, which is boot:. At the boot: prompt, you can do any of the following things:

Pressing [Enter] — Causes LILO’s default boot entry (as defined by the dialog box shown in Figure 6-21) to be booted.

Entering a Boot Label, followed by [Enter] — Causes LILO to boot the operating system corresponding to the entered boot label.

Doing Nothing — After LILO’s timeout period, (which, by default, is five seconds) LILO will automatically boot the default boot entry.

Do whatever is appropriate to boot Red Hat Linux. You should see one or more screens worth of messages scroll by. Eventually, you should see a login: prompt.

Congratulations! Your Red Hat Linux installation is complete!

If you’re not sure what to do next, we suggest you begin with the Red Hat Linux Getting Started Guide as an introduction to using Linux. The Red Hat Linux Getting Started Guide covers topics such as “learning the basics of your system” to “navigating your system” and much more.

## 7 Finding Documentation

Red Hat Linux includes thousands of pages of online documentation to help you learn how to use the system. The man pages, info documents, and plain text files included provide information on almost every aspect of Linux. If you've installed it, Red Hat Linux also includes documentation produced by the Linux Documentation Project.

### Online Help

When you are looking for general help on commands and error messages, the best place to start is right on your system. There are several different sources of information at your fingertips:

- Man Pages — Authoritative reference material for commands, file formats, and system calls.
- Package Documentation — Many packages include additional documentation; RPM can help you find it.
- HOWTOs and FAQs — Helpful information from the Linux Documentation Project.
- The locate Command — A command that can help bridge the gap between a command and its documentation.
- info Pages — Hypertext documentation without the Web.

Let's take a look at each information source.

### Man Pages

Almost every command on your system has an associated "man" page. This is documentation that you can get to instantly should you have questions or problems. For example, if you were having trouble with the ls command, you could use man to get more information by entering man ls. This will bring up the man page for ls. The man page is viewed through the less program (which makes it easy to page forward and backward screen by screen), so all of the options to less will work while in a man page. The more important keystrokes for less are:

- [q] to quit
- [Enter] to page down line by line
- [Space] to page down page by page
- [b] to page back up by one page
- [/] followed by a string and [Enter] to search for a string
- [n] to find the next occurrence of the previous search

There are times when it’s just a lot more convenient to read something from a sheet of paper. Providing you have a working printer, you can print man pages as well. If you don’t have PostScript printing capability and just want to print ASCII, you can print man pages with:

```
man COMMAND | lpr
```

If you do have a PostScript printer, you will probably want to print with:

```
man -t COMMAND | lpr
```

In both of those commands substitute “COMMAND” for the command you are trying to get help for.

Sometimes you’ll find that certain system components have more than one man page. Here is a table showing the sections that are used to divide man pages:
