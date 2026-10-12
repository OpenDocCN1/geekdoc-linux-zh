
## What You Need

To follow along with this book, you must install the software found on the accompanying CDs. To do that, you need a PC with the following general configuration:

- An Intel Pentium or compatible CPU, 200 MHz or better (for text mode); 400 MHz or better (for GUI mode). (Some Intel 486 computers may work, but it's hit-or-miss.)
- At least 64MB of RAM. To run the GNOME or KDE desktop 128MB are needed, although Red Hat recommends 256MB.
- At least 510MB of hard disk space (you have to select a minimal install). You need 2.1GB of hard disk space for a personal desktop install, 2.6GB for a typical workstation installation, or at least 920MB of space for a server installation. To install everything, you need about 5.8GB of space.
- A CD-ROM drive. This is recommended for installation, although you can install over a network or from a local hard disk instead. For those types of installs, you need at least a 3.5-inch floppy disk drive and either an extra hard disk partition or another computer that can be reached over the network that has packages or images of the Red Hat Linux CDs on it. (I tell you how to do that later, in case you're interested.)

Not every piece of PC hardware works with Red Hat Linux. You can find a list of computer processors that will work with Red Hat at www.redhat.com/hardware. You will probably want to use other types of hardware (also on that list) with your Red Hat Linux system, including video cards, mice, sound cards, modems, printers, scanners, joysticks, PCMCIA devices, and tape drives.

> **CROSS-REFERENCE**: I describe hardware requirements in more detail during descriptions of Red Hat Linux installation in Chapter 2.

## Red Hat Linux Bible Improvements

Although this edition of Red Hat Linux Bible has Fedora and Enterprise Edition as the subtitle, you can think of it as reflecting a step further in the progression of Red Hat Linux. Until the name of the Linux distribution on the three CDs in this book was changed to Fedora Core, the distribution they reflected was just the next Red Hat Linux (Red Hat Linux 7.3, 8, 9, ... Fedora).

That said, going forward Red Hat, Inc. has made a more definitive split between the Fedora Project and Red Hat Linux Enterprise Product. For that reason, Chapter 1 is devoted to describing the differences between Fedora Core and Red Hat Enterprise Linux.

Because most of the technologies in Fedora and Enterprise have not drifted so far, most of the descriptions in this book will still work for both (with Enterprise including fewer of the bells, whistles, and toys you get with Fedora and more features that scale up to large servers.)

As this book, too, is meant to reflect a progression of Red Hat Linux, I have included a variety of enhancements from the previous Red Hat Linux 9 Bible. Many of those enhancements are detailed below:

- **Correcting Red Hat Linux** — I adapted the installation procedure to match the Fedora Core CDs that come with this book, and noted where the installation process differs for Red Hat Enterprise Linux. I also noted that the LILO boot loader was removed from Fedora, although it is still in Enterprise for the time being.
- **Configuring RAID** — I noted the ability to configure RAID disks during the installation process (Chapter 2). In Chapter 10, I go into more detail about how, and why, you would set up RAID disks in Red Hat Linux.
- **GNOME 2.4** — Although there are important changes for developers in GNOME 2.4, changes for end users are mostly reflected in a few new applications. In Chapter 9 I describe Epiphany, which replaces Galeon as the default Web browser for GNOME.
- **More text editors** — For those who find the vi text editor challenging, in Chapter 4 I noted several other text editors you can try.
- **Using yum to get software** — I added a description of the yum command and `yum.conf` file to Chapter 5. Yum is a great tool for downloading and installing add-on software packages in RPM format that are compiled specifically for each Red Hat Linux distribution (with dependent packages downloaded and installed as well).
- **Shift to ssh tools** — Throughout this edition, I've tried to shift from old UNIX networking tools (`ftp`, `rlogin`, `rsh`, and the like) to more recent, more secure commands based on the OpenBSD secure shell protocol (`ssh`, `sftp`, and so on). Descriptions of `rlogin`, `rsh`, and other "r" commands have moved to the Wiley companion Web site for this book.
- **Using WineX 3.1 Point2Play** — In Chapter 7, I added a description of the new Point2Play feature of WineX 3.1. Although not part of Red Hat Linux, this add-on can help you get Windows games running in Linux.
- **Cool Mozilla Web browsing tricks** — Because we spend so much time browsing the Web these days, I like to add extra tips on using Mozilla to each edition. For this edition, I added some descriptions of tabbed browsing, the DOM inspector, and keystrokes for resizing Web pages to Chapter 9. Mozilla also has a new Junk Mail feature to help you build your own anti-spam rules in Mozilla Mail.
- **Improving laptop performance** — A new section in Chapter 10 describes how to manage power better and generally improve laptop performance with Red Hat Linux.
- **Using up2date for software updates** — I added some information on how to configure the new feature of `up2date` that lets you use apt and yum repositories to do software updates of Red Hat Linux software in the Fedora Core.
- **Removing temp files** — I added a description to Chapter 11 about how `tmpwatch` automatically cleans up temporary files in Red Hat Linux.
- **Writing shell scripts** — I pulled in my friend, and shell script expert, Kevin Pedigo to completely overhaul the section on writing shell scripts in Chapter 12. Along with new examples, Kevin added descriptions of how to use grep, cut, tr and sed in scripts.
- **Improving security** — For Chapter 14, I had security expert Chuck Wolber add new sections on detecting and responding to denial-of-service, intrusion, and other attacks.
- **Creating certificates** — Another major enhancement Chuck made to Chapter 14 was a section on creating and obtaining SSL certificates to enable your Red Hat Linux system to provide secure communications.
- **A few new options** — As I go through the book, I try to add new descriptions of options to old commands. A couple of note in this edition are the description of `rpm -F` in Chapter 5 (a convenient option to update many packages at once without installing new ones) and `mount -l` in Chapter 10 (to do lazy unmounts when resources are busy).
- **Using Linux NFS file sharing from the MAC** — I added a procedure for configuring NFS in Linux (Chapter 26) so that a MAC OS X computer can use a shared NFS directory from the Linux machine.

Besides these sections, procedures throughout the book have been tested and corrected to match changes that have occurred to Red Hat Linux software in this version.

## Conventions Used in This Book

Throughout the book, special typefaces indicate code or commands. Commands and code are shown in monospace type:

```
This is how code looks.
```

In the event that an example includes both input and output, monospace is still used, but input is presented in bold type to distinguish the two. Here is an example:

```
$ **ftp ftp.hansonhistory.com**
Name (home:jake): **jake**
Password: ****
```

The following boxes are used to call your attention to points that are particularly important.

> **NOTE:** A Note box provides extra information to which you need to pay special attention.

> **TIP:** A Tip box shows a special way of performing a particular task.

> **CAUTION:** A Caution box alerts you to take special care when executing a procedure, or damage to your computer hardware or software could result.

> **CROSS-REFERENCE:** A Cross-Reference box refers you to further information on a subject that you can find outside the current chapter.

## How This Book Is Organized

The book is organized into four parts.

### Part I: Getting Started in Red Hat Linux

Part I consists of Chapters 1 and 2, which contain brief descriptions of the Linux technology and tell you what you need in order to get the operating system installed. Chapter 1 serves as an introduction to the Linux OS and to Red Hat Linux in particular. I also pay special attention to Red Hat, Inc.'s division between the Fedora Project and Red Hat Enterprise Linux. Chapter 2 discusses what you need in order to install Red Hat Linux (Fedora Core or Enterprise) and how to make the decisions you are faced with during installation. It includes procedures for installing from CD-ROM, hard disk, or network connection (NFS, FTP, or HTTP servers).

### Part II: Using Red Hat Linux

Part II consists of Chapters 3 through 9, which include information for the average user who must use Linux to run applications and access the Internet. In Chapter 3, you learn about the GNOME desktop environment, the KDE desktop environment, and the X Window System. These GUIs provide graphical means of using Red Hat Linux. Chapter 4 describes ways of exploring and understanding Red Hat Linux, primarily from the Linux shell command interpreter. You learn how to use the *bash* shell, the *vi* text editor, and the commands for moving around the Linux file system.

Chapter 5 contains information on obtaining, installing, and running Linux applications. It also helps you run applications from other operating systems in Linux. Chapter 6 describes both old-time publishing tools and new, graphical word processors that are available with Red Hat Linux. Old tools include the *troff* and *TeX* text processing tools, whereas newer publishing software includes *OpenOffice* (included on the CDs) and *StarOffice* (commercially available).

Graphical and character-based games that run in Red Hat Linux are described in Chapter 7. This chapter also describes how to run commercial Windows games using *WineX*, and commercial Linux games, such as "Civilization: Call to Power" and "Myth II," some of which have demo versions available. Chapter 8 describes how to use audio and video players, as well as how to configure sound cards and CD burners. Chapter 9 describes tools for browsing the Web (such as the *Mozilla* browser) and related tools (such as e-mail clients and newsreaders).

### Part III: Administering Red Hat Linux

Part III consists of Chapters 10 through 14, which cover general setup and system maintenance tasks, including how to set up user accounts, automate system tasks, and back up your data. Chapter 10, in which you learn what you need to know about basic system administration,
