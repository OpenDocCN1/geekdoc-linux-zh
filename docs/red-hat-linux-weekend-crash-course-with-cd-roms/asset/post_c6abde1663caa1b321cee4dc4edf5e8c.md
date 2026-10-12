
- StarOffice Mail for electronic mail
- StarOffice Discussion for participating in Internet newsgroups

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_258_0.png)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_258_1.png)

You can download a copy of StarOffice for free from http://www.sun.com/staroffice/. You can also find the details of Sun’s StarOffice licensing policy at the same URL.

## REVIEW

This session introduced you to office applications for Linux. You tried out a few common office tools — spreadsheets, calendars, calculators, and spelling checkers — that come with Red Hat Linux. You also learned about several commercially available office application suites for Linux — WordPerfect Office 2000 for Linux, Applixware Office, and StarOffice. These commercial applications are not part of Red Hat Linux, but you learned how to find out more about each product in case you need a Linux office suite for your home or business.

## QUIZ YOURSELF

1. What is the default file format and file extension of the Gnumeric spreadsheet? (See “Using the Gnumeric Spreadsheet”.)
2. How do you add an appointment in the GNOME Calendar? (See “GNOME Calendar”.)
3. What choice of calculators do you have to work with Red Hat Linux? (See “Using Calculators”.)
4. What utility do you use to check the spellings in a text file? (See “Using the Spelling Checker”.)
5. What are some commercially available office applications for Linux? (See “Commercially Available Office Applications”.)

## PART

## IV

## Saturday Evening
Part Review

1. Describe how the look and feel of the GNOME desktop is similar to that of Windows 95/98/NT.
2. How do you customize the look and feel of the GNOME desktop? Name some of the features that you can customize.
3. What is Sawfish? What role does it play in GNOME? How do you configure Sawfish?
4. Explain how you can change your default desktop from GNOME to KDE and vice versa.
5. Describe how you would customize the look and feel of the KDE desktop.
6. Describe how to select and configure a screen saver for the GNOME desktop.
7. What does it mean to “lock the screen?” How do you lock the screen in GNOME?
8. How do you select and configure a screen saver in KDE?
9. What are some of the games available in GNOME? What kind of a game is AisleRiot?
10. Name some of the games that come with the KDE desktop.
11. Describe how you would configure the sound card in Red Hat Linux.
12. What are some of the CD player applications that you can use to play audio CDs in Red Hat Linux? What must you do so that you can play audio CDs as a normal user?

13. The GNOME CD player displays the title of the audio CD and a list of the song titles. How does the CD player find this information?
14. Name two image manipulation programs that come with Red Hat Linux. What can you do with these programs?
15. Suppose you have a PostScript document. Which application would you use to view that document on your Red Hat Linux system?
16. What are some of the office utilities that are included on this book’s Red Hat Linux CD-ROM? Is any complete office productivity suite included?
17. What is the name of the spreadsheet application that comes with the GNOME desktop? What is the default file format of that application? Can you exchange files with Microsoft Excel?
18. Show the command line you’d type to check the spelling in a text file names report.txt.
19. Name a few commercial office application suites — word processor, spreadsheet, presentation graphics, and database — for Linux. How can you find out more information about these commercial applications?
20. Which one of the office application suites is a cross-platform solution — works on many different operating systems? Mention the major components of this office application suite.

☑ Sunday

## Part V–Sunday Morning

## Session 21

*Configuring the X Window System*

## Session 22

*Understanding How Red Hat Linux Boots*

## Session 23

*Installing Software Packages*

## Session 24

*Building a New Kernel*

## Session 25

*Scheduling Jobs in Red Hat Linux*

## Session 26

*Backing Up and Restoring Files*

## Part VI–Sunday Afternoon

## Session 27

*Building Software Packages from Source Files*

## Session 28

*Monitoring System Performance*

## Session 29

*Maintaining System Security*

## Session 30

*Getting Help from Available Resources*

## PART

## V

## Sunday
Morning

Session 21
Configuring the X Window System

Session 22
Understanding How Red Hat Linux Boots

Session 23
Installing Software Packages

Session 24
Building a New Kernel

Session 25
Scheduling Jobs in Red Hat Linux

Session 26
Backing Up and Restoring Files

## SESSION

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_264_0.png)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_264_1.png)

## Configuring the X Window System

## Session Checklist

- ✓ Setting up the X Window System
- ✓ Running and controlling the X Window System

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_264_2.png)

This morning’s sessions focus on various system administration tasks such as configuring X, learning the Red Hat Linux boot sequence, installing new software packages from RPM and tar files, building a new kernel, scheduling jobs to run at specific times, and performing system backups. This session shows you the steps involved in configuring the X Window System, or X for short. It’s important to learn how to configure X because graphical desktops such as GNOME and KDE require X to work.

## Setting the X Window System Up

The term X Window System, or X for short, is loosely applied to several components that facilitate window-based graphics output (or a graphical interface) on a variety of bitmapped displays. A bitmapped display has two distinct components: a video monitor on which the graphics output appears and a video card (or graphics card) — either a plug-in card or some circuitry built into the system’s motherboard — that causes the output to appear on the monitor.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_265_0.png)

The X Window System for Red Hat Linux comes from the XFree86 project — a cooperative project of programmers who bring X to the PC. (You can access the XFree86 home page at http://www.xfree86.org/.) As a result, the Linux version of X is called XFree86.

## Understanding the X server

At the heart of X is the X server — a process (computer program) running on a computer that has a bitmapped display, a keyboard, and a mouse. Applications (X clients) that need to display output do so by communicating with the X server via one of several possible interprocess communication mechanisms.

When you run X on your system, the X server runs on your computer and controls the monitor, keyboard, and mouse. The server responds to commands sent by X clients that open windows and draw in those windows. The X clients may run locally or on remote systems.

The X server configures the display (number of colors, resolution in terms of number of pixels horizontally and vertically), mouse, and keyboard based on information stored in a configuration file. Red Hat Linux comes with two versions of XFree86 — 3.3.6 and 4.0.1. Depending on your video card, the installation program selects an X server from one of these versions of XFree86. Each version has a different configuration file. For XFree86 3.3.6, the configuration file is `/etc/X11/XF86Config`. For XFree86 4.0.1, the configuration file is `/etc/XFree86Config-4`.

Configuring X requires you to prepare the configuration file. The configuration file contains information about your video card, monitor, keyboard, and mouse. Red Hat Linux comes with a utility program called `xf86config` (same name as the configuration file, but in lower case) that enables you to create the `XF86Config` working configuration file.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_265_1.png)

You don’t need to create the X configuration file with the `xf86config` program if when you install Red Hat Linux (following the instructions outlined in Sessions 1 through 3), the installation program automatically detects your system’s video chipset and enables you to configure X through a number of dialog boxes. Additionally, Session 4 shows you how to run the `Xconfigurator` utility to create the X configuration file.
