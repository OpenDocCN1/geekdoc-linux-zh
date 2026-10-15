
There are some upstarts, though, notably the Debian Package Manager, DBM, which offers a simpler interface and a more flexible package creation environment. If you’ve bumped into the Fink package manager on Mac OS X, you might be surprised to know that it’s based on DBM.

In case you’d like to learn more about the package management system on your own version of Unix or Linux (or Mac, for that matter), Table 19.3 provides a handy list.

| Distribution | Package Management System(s) |
|---|---|
| Debian Linux | dpkg |
| Red Hat Linux | RPM |
| Slackware Linux | tgz |
| GNU/Linux | upkg |
| Mac OS X | Fink and MacPorts |
| Microsoft Windows | Cygwin |
| Solaris Unix | pkgadd |
| AIX Unix | install |
| HP-UX Unix | Software Distributor |

TABLE 19.3 Package Management Systems

## Summary

Whether it’s to assuage your anxiety about unstable servers, to avoid possible problems with poor backups and inattentive administrators, or simply to help you package up and move large sets of files around, tar and its partner programs are a great help. Every time I have to move from one system to another, I invariably use tar, compress, and ftp as a power trio.

Further, while you can download tar archives or similar from the Internet, the ability to use the RPM or a similar package management system makes it incredibly easy to browse through and install just about any open source application that’s compatible with your version of Unix or Linux.

## Workshop

The Workshop poses some questions about the topics presented in this hour.

## Exercises

- 1. What’s the key difference between tar and cpio?
- 2. What’s wrong with this command?
  - tar cvf OUTPUT.tar *
- 3. Try both compress and zip on a few large files to see which produces better results. Try zip on a very small file, too, and see what happens.
- 4. Build, move, and then unpack a directory tree using zip. Is it easier or harder to use than tar for this task?
- 5. Using your native package management system, find and install bzip2 and then use that on the same large files you used for question 4 to see if it does a better job with compression.

## Preview of the Next Hour

In the next hour you’ll learn about the ability to communicate with other users on your computer through electronic mail.

## Hour 20. Using Email to Communicate

## Goals for This Hour

In this hour, you will learn

- ► How to read email with `mailx`
- ► How to send email with `mailx`
- ► About sending mail to the rest of the digital universe

It’s time to learn about what’s arguably the lifeblood of any operating system in today’s connected world: the ability to communicate with other users on your computer and elsewhere through electronically transmitted mail, or email. You’ve probably been using email for years through graphical interfaces—perhaps Gmail in a browser, or Microsoft Outlook or Apple Mail. Turns out that just as with so many other Internet tools, email got its start on the Unix command line, and that’s still a place where it’s very much at home—and what this lesson is all about.

Of all the places in Unix where there is variety, most of it surely is found in electronic mail, or email. At least 15 programs are available from various vendors to accomplish two tasks: to read mail from and send mail to other folks. In this hour, you’ll learn about the standard electronic mail system, Berkeley Mail. As it happens, I wrote an email system of my own that you can often find on Linux and other Unix-like systems called the Elm Mail System. It’s a full-screen alternative mail program that’s widely distributed. We’ll stick with Berkeley Mail for this hour, however, because like a number of different screen-oriented email programs (Mush, Pine), Elm works identically from the command line.

There are, of course, graphically oriented email programs, too, in the Unix world, most notably Thunderbird, a fully featured email application that’s part of the Mozilla browser suite. We’ll look at Thunderbird in Hour 24, “GNOME and the GUI Environment,” when we peek at the X11 graphical interface atop Unix.

## Interacting with the World

Much of what you’ve learned in this book has been about how you can exploit Unix to be more productive. Now it’s time to learn how to communicate with others, to learn about what I consider the “killer app” of Unix and of the Internet overall: electronic mail.

## Task 20.1: Reading Electronic Mail with mailx

Of all the capabilities of Unix, one of the most popular is undoubtedly the ability to send electronic mail to another user—even on another computer system—with a few keystrokes. In this section, you’ll learn how to work with other users on your own computer, and later in this hour you’ll learn how to send mail to folks who are on different computers, anywhere in the world.

Various programs for reading mail can be used on Unix systems, but the two most
