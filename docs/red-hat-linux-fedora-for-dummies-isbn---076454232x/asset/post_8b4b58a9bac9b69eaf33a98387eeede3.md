
## Part III
## Linux, Huh! What Is It Good For? Absolutely Everything!

### The 5th Wave

By Rich Tennant

![](img/8c094d1b36276212c03d10d898508a6e_132_0.png)

> “Think of our relationship as a version of Red Hat Linux – I will not share a directory on the love-branch of your life.”

## In this part...

One thing you can do with your computer is put up your feet and wait for the screen saver to kick in. You can confide to all your friends at the next party you attend that you have a “Red Hat Linux box.” (That will make you popular as they clamor to know when your stock options will mature.) Or, you can use your new Red Hat Linux workstation to get things done.

To that end, Chapter 9 introduces the friendly world of the GNOME windows environment. GNOME, a friendly lil’ guy who likes to put a friendly face on Linux, can help you set up the “look and feel” of Linux so that you feel comfortable and at home. Chapter 10 goes further and introduces cool things you can do with GNOME applications.

In Chapter 11, the fun starts. Can you say “Par-tay”? (Sorry.) Find out how to use the Mozilla browser and how to use multimedia players to listen to audio CDs and Ogg or MP3 files. We show you how to record music from CDs and how to become your own recording studio by recording audio (and data, if you’re a nerd) to CD.

Chapter 12 takes the audio thing one step further. It describes how to use the open source multimedia players XMMS and MPlayer to listen to flowing streams — no, not water streams, but, rather, audio and video streams flowing from the Internet. You can listen to radio and audio clips and watch video too. With this knowledge, you never have to leave your couch again.

Lucky Chapter 13 describes how to get work done with OpenOffice. Sorry — reality bites and personal productivity suites (word processors and spreadsheets, for example) are a necessary evil. Gotta make the doughnuts.

Chapter 14 describes how to use WINE and VMware. The WINE system lets you run Windows applications, like Word 2000, directly from your Linux workstation! VMware creates virtual computers that run both Windows and Linux.

## Chapter 9
## Gnowing GNOME

**In This Chapter**

- Introducing the X Window System
- Introducing and exploring the GNOME desktop environment
- Exploring the GNOME desktop
- Using GNOME windows
- Making GNOME icons
- Exploring the GNOME Panel
- Adding GNOME Panels
- Exiting from GNOME and X
- Modifying the look of your desktop
- Introducing GNOME applications
- Configuring MIME types

The Red Hat Linux operating system provides two interactive interfaces for you to work from: the text-based command-line interface (CLI), as we describe in Chapter 4, and the graphical X Window System. The command-line interface is similar to the old Microsoft Disk Operating System (MS-DOS) environment, which requires you to feed individual commands to the operating system; you can use the GNOME Terminal (emulator) as your CLI. The X Window System, also known simply as $X$, provides a graphical “point-and-click” environment from which most people prefer to work.

Red Hat Linux provides two desktop environments for you to use: GNOME and KDE, or the K Desktop Environment. Both GNOME and KDE run on top of X, and both environments include a menu system to access utilities, applications, and shortcuts in the form of icons and numerous other enhancements. Using either of these desktop environments makes using Red Hat Linux as your workstation easy and pleasurable.

GNOME is the default desktop environment for Red Hat Linux. Red Hat also gives you the option of installing KDE, an excellent system that many people prefer. However, because of limited space in this book, we discuss only GNOME.

![](img/8c094d1b36276212c03d10d898508a6e_135_0.png)

The excellent Red Hat Linux “minibook” describes KDE in more detail.

In this chapter, you find out a little about X and the basics for working with GNOME. You also get to mess around with the GNOME Panel and desktop (the GNOME Panel is similar to the taskbar in Windows computers). We show you some simple but effective maneuvers to manage your desktop and describe some applications.

### Introducing the X Window System

Red Hat gives you the option of using the GNOME and KDE desktop environments. GNOME and KDE, however, run on top of X, and X runs on Linux. *X* is the software that provides the low-level graphical tools that systems like GNOME use. X is the middleware that makes building complex systems like GNOME possible.

![](img/8c094d1b36276212c03d10d898508a6e_135_1.png)

The version of X that comes with Red Hat Linux is both sophisticated and simple to use. That wasn't always the case, though; in fact, it took lots of natural — dare we say Darwinian? — selection to arrive at the current arrangement of X, and the result works well.

X is composed of three main parts:

- The X server
- Numerous graphics libraries
- A set of X client graphics applications

The *X server* is a program that talks to the human-interactive hardware on your computer — such as the video card, keyboard, and mouse — and runs interference between this hardware and other graphics software. It uses the graphics libraries to work properly with the graphics hardware.

*X clients* are graphical programs, such as Mozilla and xclock. X clients display their graphical output through the X server; they also get their keyboard and mouse input through the X server. X clients can be run on the same computer that the X server runs on or across a network to any computer running an X server. For example, by using X, you can run an X client on a computer on the other side of the world and view it on the X server running on your home computer.

Suppose that you're logged in to a computer in Australia and you want to see what time it is there. You could run the *date* command (from a command line) to see the date and time, but that would be boring. Instead, you could run the *xclock* program on the remote machine and see a graphical clock displayed on your local computer. You can then verify that the Aussies use clocks that run clockwise and have 24-hour days.

![](img/8c094d1b36276212c03d10d898508a6e_136_0.png)

The X server program, often called simply *X*, isn't part of the operating system, as it is in some other operating systems. Instead, the X server is a *user-level* program — although it's special and complex.

The X Window System provides the foundation for these graphical-based systems:

- **Desktop environment:** GNOME and KDE provide a desktop environment that makes using your computer easy. Desktop environments provide high-level functions like menu systems, icons, and backgrounds. A desktop environment is equivalent to a house where X is the foundation.
- **Graphical applications:** Red Hat installs numerous applications, such as games, system administration utilities, Mozilla, and Ximian Evolution to provide the functionality that helps you use your computer and the Internet. Graphical applications are equivalent to the appliances in a house.

### Introducing the GNOME Desktop Environment

GNOME stands for GNU Network Object Model Environment. (GNU itself stands for GNU's Not UNIX, a recursive acronym designed by guys who probably never went to their prom but did change the world.) If you have trouble remembering acronyms, just think of GNOME as *great graphics for nada money.* However you remember it, GNOME is an open source graphical desktop environment. It provides a platform for completing your everyday tasks, such as word processing and Internet browsing, on your Red Hat Linux computer.

Log in to your Red Hat Linux computer and check out the GNOME interface. It should look something like Figure 9-1 and consists of these three major elements:

![](img/8c094d1b36276212c03d10d898508a6e_137_0.png)

- **The desktop**: Quite simply, the desktop is what you see on your computer screen. It’s the space where you do your work and is equivalent — ta-da! — to the top of a desk. The desktop comes preconfigured with a background and several icons that include links to such places as your home directory and the trash bin. Icons are equivalent to the junk you pile on your desk: Some is useful and some isn’t.

When you double-click the home directory (or right-click and choose Open), a Nautilus window opens and displays the contents of those directories. *Nautilus* is a graphical system for working with not only files and directories but also administration utilities and Web pages. See Chapter 10 for more information about Nautilus.

- **The Panel**: The menu bar that runs across the bottom edge of your GNOME screen is the Panel. You can access every GNOME function and Red Hat or third-party application from the GNOME Panel. It represents the drawers in a desk.

- **Applications**: These elements include user system and GNOME-level applications. User programs include applications such as Mozilla, Evolution, XIMS, and Xine. System applications include the Red Hat Linux system administration utilities, such as network configuration and user management utilities, and GNOME utilities, such as the Help browser. Applications are equivalent to the toys and work to be done on and in your desk.
