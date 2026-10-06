
# Starting with Linux Shells

The concept of OSS allows programmers to develop software and release it to the world with no licensing fees attached. Anyone can use the software, modify it, or incorporate it into his or own system without having to pay a license fee. Uniting Linux's Linux kernel with the GNU operating system utilities created a complete, functional, free operating system.

While the bundling of the Linux kernel and GNU utilities is often just called Linux, you will see Linuxists on the Internet refer to it as the GNU/Linux system to give credit to the GNU organization for its contributions to the cause.

# The core GNU utilities

The GNU project was mainly designed for Unix system administrators to have a Unix-like environment. This focus resulted in the project portant many common Unix system command line utilities. The core bundle of utilities supplied for Linux is called the coreutils package.

The GNU coreutils package consists of three parts:

- Utilities for handling files
- Utilities for manipulating files
- Utilities for managing processes

These three main groups of utilities each contain several utility programs that are invaluable to the Linux system administrator and programmer. This book covers each of the utilities contained in the GNU coreutils package in detail.

# The shell

The GNU/Linux shell is a special interactive utility. It provides a way for users to start programs, manage files on the filesystem, and manage processes running on the Linux system. The core of the shell is the command prompt. The command prompt is the interactive part of the shell. It allows you to enter text commands, interprets the commands, executes the commands in the kernel.

The shell contains a set of internal commands that you use to control things such as copying files, moving files, renaming files, displaying the programs running on the system, and stopping programs running on the system. Besides the internal commands, the shell also allows you to enter the name of a program at the command prompt. The shell passes the program name off to the kernel to start it.

There are quite a few Linux shells available to use on a Linux system. Different shells have different characteristics, some being more useful for creating scripts and some being more useful for managing processes. The default shell used in all Linux distributions is the bash shell. The shell was developed by the GNU project as a replacement for the standard Unix shell, called the Bourne shell (after its creator). The bash shell name is a play on this wording, referred to as "Bourne again shell".

# Part I The Linux Command Line

## TABLE 1-2 Linux Shells

| Shell | Description |
| :--- | :--- |
| ash | A simple, lightweight shell that runs in low-memory environments but has full compatibility with the bash shell |
| korn | A programming shell compatible with the Bourne shell but supporting advanced programming features like associative arrays and floating-point arithmetic |
| tcsh | A shell that incorporates elements from the C programming language into shell scripts |
| zsh | An advanced shell that incorporates features from bash, tcsh, and korn, providing advanced programming features, shared history files, and themed prompts |

Besides the bash shell we will cover several other popular shells in this book. Table 1-2 lists the different shells we will examine.

Most Linux distributions include more than one shell, although usually they pick one of them to be the default. If your Linux distribution includes multiple shells, feel free to experiment with different shells and see which one fits your needs.

# The Linux desktop environment

In the early days of Linux (the early 1990s) all that was available was a simple text interface to the Linux operating system. This text interface allowed administrators to start programs, control program operations, and move files around the system.

With the popularity of Microsoft Windows, computer users expected more than the old text interface to work. This sparked further development in the OSS community, and the Linux graphical desktops emerged.

Linux is famous for being able to do things in more than one way, and no place is this more relevant than in graphical desktops. There are a plethora of graphical desktops you can choose from Linux. The following sections describe a few of the more popular ones.

# The X Windows system

There are two basic elements that control your video environment — the video card in your PC and your monitor. To display fancy graphics on your computer, the Linux software needs to know how to talk to both of them. The X Windows software is the core element in presenting graphics.

The X Windows software is a low-level program that works directly with the video card and monitor in the PC, and controls how Linux applications can present fancy windows and graphics on your computer.

Linux isn't the only operating system that uses X Windows, there are versions written for many different operating systems. In the Linux world, there are only two software packages that can implement it.

The XFree86 software package is the older of the two, and for a long time was the only X Windows package available for Linux. As its name implies, it's a free open source version of the X Windows software.

Recently, a new package called Xorg has come onto the Linux scene. it provides an open source software implementation of the X Windows system. It is becoming increasingly popular, with many Linux distributions starting to use it instead of the older XFree86 software.

Both packages work the same way, controlling Linux uses your video card to display content on your monitor. To do that, they have to be configured for your specific system. That is supposed to happen automatically when you install Linux.

When you first install a Linux distribution, it attempts to detect your video card and monitor and creates an X Windows configuration file that contains the required information. During installation you may notice a time when the installation program scans your monitor for supported video modes. Sometimes this causes your monitor to go blank for a few seconds. Because there are lots of different types of video cards and monitors out there, this process can take a little while to complete.

This is where many of the customized distributions can be lifesavers. Most of them take great effort to automatically detect video hardware and settings without asking you any technical questions.

Unfortunately, sometimes the installation can't autodetect which video settings to use, especially with some of the newer, more complicated video cards. Unfortunately, some distributions will fail to install if they can't find your specific video card settings. Others will ask you a few questions during installation to help manually get the necessary information. Since others default to the lowest common denominator and produce a screen image that is not customized for your video environment.

To complicate matters more, many PC users have fancy video cards, such as 3-D accelerator cards, so they can play high-resolution games. In the past, this caused a lot of problems if you tried to install Linux. But lately, video companies are helping to solve this problem by providing Linux drivers. And many of the customized distributions now include drivers for specialty video cards.

The core X Windows software produces a graphical display environment, but nothing else. While this is fine for running individual applications, it is not too useful for day-to-day computer use. There is no desktop environment allowing users to manipulate files or launch programs. To do that, you need a desktop environment on top of the X Windows system.

# The Command Line

## The KDE desktop

The KDE Desktop Environment (KDE) was first released in 1996 as an open source project to produce a graphical desktop similar to the Microsoft Windows environment. The KDE desktop incorporates all the features you are probably familiar with if you are a Windows user. Figure 1-3 shows a sample KDE desktop running on Linux.

The KDE desktop allows you to place both application and file icons on the desktop area. If you single-click on an application icon, the Linux system starts the application. If you single-click on a file icon, the KDE desktop attempts to determine what application to start to handle the file.

The bar at the bottom of the desktop is called the Panel. The Panel consists of four parts:

- The menu: Similarly to the Windows start menu, the K menu contains links to start installed applications.
- Program shortcuts: These are quick links to start applications directly from the Panel.
- The taskbar: The taskbar shows icons for applications currently running on the desktop.
- Applets: These are small applications that have an icon in the Panel that often can change depending on information from the application.

# FIGURE 1-3

The KDE desktop on a SimplyMEPIS Linux system

![](/adcbcf1053b52dbf22f3aa187738232f_47_0.png)
