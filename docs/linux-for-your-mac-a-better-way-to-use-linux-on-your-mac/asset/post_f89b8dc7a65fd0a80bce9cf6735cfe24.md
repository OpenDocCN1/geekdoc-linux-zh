
graphics, and more than 1,000 fonts. Even considering the system's paltry 20GB hard drive with eight gigabytes dedicated to Mac OS 9.0.4, this still leaves nearly six gigabytes of free disk space after a huge Linux installation!

## Why Use Linux on Your Mac?

Although originally designed to run as a small desktop operating system, Linux now provides many features that rival or exceed those of other operating systems. For Mac users, Linux is a free, alternative operating system with features that were previously available only through ridiculously expensive and now outdated commercial software. Even with the availability of BeOS (except for G4 Macs), and the advent of Mac OS X, Linux still provides the following important features and advantages:

- Linux is licensed under the GNU GPL. This means that there are no royalty or licensing fees. Unlike other operating systems, you get the source code for the kernel and nearly every command, program, application, or client included in a distribution.
- Linux provides a feature-rich development platform with the world's best selection of programmer's tools. This means that you can use your Mac to develop programs that will run on a variety of computer platforms, including hand-held PDAs, embedded devices, and Intel-based PCs.
- Linux is unparalleled in its networking compatibility, and is able to support nearly every network protocol in existence. This means that you can use your Mac to provide network file system and printing support for Windows-based networks.
- Linux works well as a server platform, and when combined with the superior speed and capabilities of the PowerPC processor, your Mac provides quite a bit of punch for the task.
- Linux attracts nearly all GPL and open source programming projects. This means that if you are looking for a solution to a computing task, chances are someone has already started working on a possible solution.
- Linux is stable, robust, and reliable. You are the one in control of your operating system. When properly set up and used, Linux works reliably in production environments.
- Linux is well supported. Linux comes with more documentation and available support than any other operating system. You can even purchase commercial support. There are also several message boards and news groups dedicated to Linux and Linux for PowerPC computers.
- Linux uses X. X11 is a networking graphical interface. From the beginning, it was designed to support thousands of users on large networks. You will benefit from its capabilities as you learn to use Linux and X.
- Linux is constantly being upgraded. Although there are classic stable releases, Linux is constantly in a state of flux as new features are added nearly every day or week. If you need a specific new feature, you can always try the latest and newest version, or simply wait until the feature appears in a stable release.
- Get the best of both worlds. You can boot both Mac OS and Linux on your Macintosh computer. You can use either BootX or Yaboot to configure your Mac to start up with Mac OS, Mac OS X, or Linux. You can also share files between the Linux and Mac hard disk partitions.

## Features and Conventions of This Book

This book is designed in four parts. Part I, “Getting Linux on Your Mac,” expounds on the subject of learning about Linux, choosing a distribution, post-installation configurations, and booting Linux. Part II, “Using Linux and X11 on Your Mac” launches into detailed information concerning the Linux command line, text editors, and X11. Part III, “Administering Linux on Your Mac,” discusses the technical details of taking care of your system. This is an important task because you, in effect, become a system administrator when you install Linux! Part IV includes using Linux and various emulators, interacting with other operating systems, and playing games.

Also, **boldface** text is used throughout the book to help you better understand some of the command lines and code listings. In each example in which you would type or enter text, the text has been *formatted in boldface*. Additionally, if a command only works for the system superuser, known as the **root** operator, the command is shown on a command line prefixed with a pound sign (#). Normal user operations on the command line are prefaced with a dollar sign ($).

I hope you enjoy reading and using *Linux for Your Mac*. Consider this book a companion guide to your favorite PowerPC Linux distribution, and let me know if you have comments, criticisms, or suggestions (flames will be sent to /dev/null).

Billy Ball  
bball@tux.org

# PART 1

## Getting Linux on Your Mac

1. Introduction to Linux on the Mac
2. Installing Linux on Your Mac
3. Post-Installation Configuration
4. All about Booting

![](img/1ea833f5a3e3c1547e3dd2891f52804a_30_0.png)

## Chapter 1: Introduction to Linux on the Mac

- Features of Linux
- Choosing a PPC Linux Distribution
- Choosing Workstation or Server
- Alternatives

Welcome to *Linux for Your Mac!* You have started at the right place, especially if you are new to Linux or want to use Linux on the Apple PowerPC platform. This chapter discusses some of the great features of Linux and provides a brief historical background about Linux and the Linux port for the PowerPC. You will learn about the different PPC Linux distributions, and how to decide which type of Linux installation to pursue.

### Features of Linux

Linux has a lot going for it. The historical strengths of Linux as an operating system become evident as you assess its performance, security, and reliability. Other strengths include how Linux is licensed, the portability of its source code language, how Linux is distributed, the volume of contributed works, and its rich inheritance of legacy software. In order to understand why Linux has become so popular, one should look at the last 25 years of personal computing viewed in conjunction with the events of only a year or so ago.

The communal gasping sound you may have heard over the last several years was the sound of computer manufacturers, value-added re-sellers, computer consultants, and consumers being choked and caught in the monopolistic vise of the software industry. Proprietary software reigned king and aided in creating an empire that seemed omnipresent and overwhelming. Events, which have occurred over the last year and up to the present, have begun to loosen the empire's grip. The year of Linux's Coming Out Party was 1999, and the celebration is just getting started.

For the first time in history, you hold in your hands the collective energy and power of software developed by thousands of programmers from around the world. This power is just waiting to be unleashed. When you install Linux on your Mac you will see why Linux really is the greatest thing since sliced bread. This software is free. You do not have to pay for a license or royalties. If you want to use it to build and distribute new software (even for a profit), go ahead. You do not have to pay for upgrades again. You can now step off the expensive software-update treadmill and enjoy the full luxuries and benefits of software that not only works, but also comes with full source code!

In the early days of personal computing (the late 1970s), computers did not come with a lot of software. At that time many PCs ran Gary Kildall's CP/M operating system. Users routinely shared source code, bug fixes, and programs across an incredible variety of platforms in order to help each other spread collective knowledge and power across the user base. Other operating systems such as FLEX and OS9 enjoyed a similar philosophy of sharing source code and utilities. This type of sharing was a benefit to all computer users.

This sharing philosophy did not last long. In the intervening two and a half decades, the personal computer hardware and software industry lost its spirit of openness and sharing. It seemed gone forever, until the advent of Linux. Since its first release in 1991, Linux has grown tremendously by offering more features and in expanding its user base. Armed with a truly righteous licensing scheme (the GNU GPL) and a high speed method of distribution (the Internet), Linux is poised to take over various tiers of the software industry. Linux is forcing the computer industry to recognize and deal with a major paradigm shift in business transaction and customer relation management.

Linux can be owned by anyone, but is controlled by no one. It has inherited the very best features and free software from the world’s oldest and most reliable operating system, UNIX, and now controls an estimated four percent of the base of installed desktops, with a presence that is perhaps five to six times larger in the mid-range server market. Linux has empowered the computer user and freed the consumer from the shackles of proprietary software (and increasingly, proprietary hardware), thus creating a new generation of users who are more wary and astute regarding intellectual freedom.

Choosing Linux makes sense; the following list demonstrates why:

- Linux is free. There are no royalty or licensing fees.
- Linux works with nearly any CPU, and has been ported to nearly every computer platform in existence.
- Linux is portable, and comes with source code. Upgrading is as simple as compiling a new kernel.
- Linux runs well on legacy hardware. This means that you can extend the life span of older computers by installing and using Linux.
- Linux performs well as a server platform, and can host many of the free, popular, and powerful server software packages, such as Apache, PostgreSQL, FTP, etc.
- Linux provides multi-tasking and can handle many different processes.
- Linux comes with an overwhelming number of computer languages and software development tools, including C, C++, Java, Python, assembler, BASIC, Pascal, Fortran, and Tcl/Tk.
- Linux is documented, not only through its completely open source code, but also through thousands of additional documents distributed by mail or over the Internet.
- Linux supports the X Window System, a graphical networking interface providing a platform for advanced graphical user interfaces.
