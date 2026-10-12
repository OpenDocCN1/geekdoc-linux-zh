
## What You Need

To follow along with this book, you need to install the software that comes with the accompanying CDs. To do that, you need a PC with the following general configuration:

- An Intel 80386, 80486, Pentium, or compatible CPU.
- At least 32MB of RAM, although 64MB or more is recommended. To run the GNOME or KDE desktop, Red Hat recommends at least 64MB.
- At least 350MB of hard disk space (you have to deselect some packages during installation to get down to the 350MB limit and you don’t get a graphical interface). You need 1.5GB of hard disk space for a typical workstation installation or at least 1GB of space for a server installation. To install everything, you need about 3.5GB of space.
- A CD-ROM drive. This is recommended for installation, although you can install over a network or from a local hard disk instead. For those types of installs, you need at least a 3.5-inch floppy disk drive and either an extra hard disk partition or another computer (that can be reached over the network) that has images of the Red Hat Linux CDs on it.

Not every piece of PC hardware works with Red Hat Linux. You can find a list of computer hardware that will work with Red Hat at www.redhat.com/hardware. You will probably want to use other types of hardware (also on that list) with your Red Hat Linux system, including video cards, mice, sound cards, modems, printers, scanners, joysticks, PCMCIA devices, and tape drives.

> **CROSS-REFERENCE:** I describe hardware requirements in more detail during descriptions of Red Hat Linux installation in Chapter 2.

## Conventions Used in this Book

Throughout the book, special typefaces indicate code or commands. I also use icons to set apart certain pieces of information. Commands and code are shown in monospace type, such as the following:

```
This is how code looks.
```

On the occasion that an example includes both input and output, monospace is still used, but input is presented in bold type to distinguish the two. Here is an example:

```
$ **ftp ftp.hands-onhistory.com**
Name (home:jake): **jake**
Password: ******
```

The following icons are used to call your attention to points that are particularly important.

> **NOTE:** A Note icon provides extra information to which you need to pay special attention.

**TIP:** A Tip icon shows a special way of performing a particular task.

**CAUTION:** A Caution icon alerts you that you need to take special care when executing a procedure, or damage to your computer hardware or software could result.

**CROSS-REFERENCE:** A Cross-Reference icon is used to refer to further information on a subject that you can find outside the current chapter.

## How this Book Is Organized

The book is organized into four parts.

## Part I: Getting Started in Red Hat Linux

Part I consists of Chapters 1 and 2, which contain brief descriptions of the Linux technology and tell you what you need in order to get the operating system installed. Chapter 1 serves as an introduction to the Linux OS and to Red Hat Linux in particular. Chapter 2 discusses what you need to install Red Hat Linux and then how to make the decisions you are faced with during installation. It includes procedures for installing from CD-ROM, hard disk, or network connection (NFS, FTP, or HTTP servers).

## Part II: Using Red Hat Linux

Part II consists of Chapters 3 through 9, which include information for the average user who needs to use Linux to run applications and access the Internet. Chapter 3 describes ways of exploring and understanding Red Hat Linux, primarily from the Linux shell command interpreter. You learn how to use the bash shell, the vi text editor, and the commands for moving around the Linux file system. In Chapter 4, you learn about the GNOME desktop environment, the KDE desktop environment, and the X Window System. These GUIs provide graphical means of using Red Hat Linux.

Chapter 5 contains information on obtaining, installing, and running Linux applications. It also helps you run applications from other operating systems in Linux. Chapter 6 describes both old-time (free) publishing tools and new, graphical word processors that are available with Red Hat Linux. Old tools include the troff and TeX text processing tools, whereas newer, commercially available publishing software includes StarOffice and WordPerfect.

Graphical and character-based games that run in Red Hat Linux are described in Chapter 7. This chapter also describes game console emulators and commercial games, such as "Civilization: Call to Power" and "Myth II," some of which have demo versions available. Chapter 8 describes how to use audio and video players, as well as how to configure sound cards and CD burners and set up your Internet browser to play multimedia. Chapter 9 describes tools for browsing the Web (such as Netscape's browser) and related tools (such as e-mail clients and newsreaders).

## Part III: Administering Red Hat Linux

Part III consists of Chapters 10 through 14, which cover general setup and system maintenance tasks, including how to set up user accounts, automate system tasks, and back up your data. Chapter 10, in which you learn what you need to know about basic system administration, describes the root login, administrative commands, configuration files, and log files. Chapter 11 describes how to set up and provide support for multiple users on your Red Hat Linux system.

In Chapter 12 you learn to create shell scripts and to use the cron facility to automate a variety of tasks on your Red Hat Linux system. Techniques for backing up your system and restoring files from backup are described in Chapter 13. Chapter 14 describes issues related to securing your computing assets in Red Hat Linux.

## Part IV: Red Hat Linux Network and Server Setup

Part IV consists of Chapters 15 through 25, which describe step-by-step procedures for setting up a variety of server types. Simple configurations for what might otherwise be complex tasks are contained in each chapter. Learn to arrange, address, and connect your Linux computers to a local area network (LAN) in Chapter 15. Chapter 16 describes techniques for connecting your Linux computer and LAN to the Internet, using features such as Point-to-Point Protocol (PPP), IP forwarding, IP masquerading, and proxy servers.

Chapter 17 describes how to set up different types of print server interfaces, including Samba (to share with Windows systems), NetWare, and native Linux printing. Chapter 18 describes file servers, such as Network File System (NFS) servers, Samba file servers, and NetWare file servers. Chapter 19 describes how to configure an e-mail server.

Chapter 20 describes how to configure and secure an FTP server, as well as how to access the server using FTP client programs. Chapter 21 teaches you how to set up Red Hat Linux as a Web server, focusing on the popular Apache server software. Chapter 22 describes how to set up an INN news server, including determining how to set up news feeds, choosing news storage methods, and enabling access to your INN server. Chapter 23 describes how to set up both DHCP and NIS services to distribute information to client workstations on the network.

Chapter 24 describes how to setup and use a MySQL database in Linux. Chapter 25 takes you through the process of making the servers you configured in the other chapters available on the public Internet. Setting up a Domain Name System (DNS) server is also described in Chapter 25.

## Appendixes

This book also has three appendices. Appendix A describes the contents of the companion CD-ROMs, and Appendix B lists the hundreds of RPMs (software packages) that come with the Red Hat Linux distribution. Appendix C contains an overview of setting up and running network services.

## About the Companion CD-ROMs

The CD-ROMs that come with this book provide the software that you need to have a working Red Hat Linux system. With this software, you can set up a Red Hat Linux workstation or server as described throughout this book. See Appendix A for a description of the contents of the Red Hat Linux CD-ROMs.

## Reach out

Of course, if you have any questions or comments about Red Hat Linux 7.3 Bible, feel free to contact me by e-mail at this address: chris.negus@iname.com
