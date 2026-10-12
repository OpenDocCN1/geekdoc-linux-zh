
## Running a DNS Server
For Fedora Core 3, the BIND DNS service (named daemon) was configured to run in a chrooted environment. Chapter 25 was updated to describe how the chrooted environment changes how you configure your own DNS server.

## Using the 2.6 Kernel
To the description of the 2.6 kernel in Chapter 27, I've added a description of how to get the kernel source code that is used with Fedora Core 3. (It's no longer available in the kernel-sources package, as it was in previous Fedora releases.)

## Getting into Rescue Mode
I've added to Appendix A a description of how to make and use the Fedora rescue CD from an image contained on the DVD that comes with this book.

Besides new features just described, procedures throughout the book have been tested and corrected to match changes that have occurred to Fedora Core software in this version.

# Conventions Used in This Book

Throughout the book, commands and code are shown in a monospaced font:

```
This is how code looks.
```

In the event that an example includes both input and output, the monospaced font is still used, but input is presented in bold type to distinguish the two. Here's an example:

```
$ ftp ftp.handsonhistory.com
Name (home: Jake): jake
Password: ********
```

The following boxes are used to call your attention to points that are particularly important.

> **NOTE:** A Note box provides extra information to which you need to pay special attention.

> **TIP:** A Tip box shows a special way of performing a particular task.

> **CAUTION:** A Caution box alerts you to take special care when executing a procedure, or damage to your computer hardware or software could result.

> **CROSS-REFERENCE:** A Cross-Reference box points you to further information on a subject that you can find outside the current chapter.

# How This Book Is Organized

The book is organized into five parts.

# Part I: Getting Started in Fedora

Part I consists of Chapters 1 through 4. Chapters 1 and 2 contain brief descriptions of the Linux technology and tell you what you need in order to get the operating system installed. Chapter 1 serves as an introduction to the Linux OS and to Fedora in particular. I also pay special attention to the division Red Hat, Inc., makes between the Fedora Project and Red Hat Enterprise Linux. Chapter 2 discusses what you need in order to install Fedora and how to make the decisions you'll be faced with during installation. It includes procedures for installing from DVD, CD-ROM, hard disk, or network connection (NFS, FTP, or HTTP servers).

In Chapter 3, you learn about the GNOME desktop environment, the KDE desktop environment, and the X Window system. These GUIs provide graphical means of using Fedora. Chapter 4 describes ways of exploring and understanding Fedora, primarily from the Linux shell command interpreter. You learn how to use the bash shell, the vi text editor, and the commands for moving around the Linux file system.

# Part II: Using Fedora

Part II consists of Chapters 5 through 9, which include information for the average user who wants to use Linux to run applications and access the Internet.

Chapter 5 contains information on obtaining, installing, and running Linux applications. It also helps you run applications from other operating systems in Linux. Chapter 6 describes both old-time publishing tools and new, graphical word processors that are available with Fedora. Old tools include the troff and TeX text processing tools, whereas newer publishing software includes OpenOffice.org utilities (included on the DVD) and StarOffice (commercially available).

Graphical and character-based games that run in Fedora are described in Chapter 7. This chapter also describes how to run commercial Windows games using Cedega, and commercial Linux games, such as Civilization: Call to Power and Myth II, some of which have demo versions available. Chapter 8 describes how to use audio and video players, as well as how to configure sound cards and CD burners. Chapter 9 describes tools for browsing the Web (such as the Mozilla browser) and related tools (such as e-mail clients and newsreaders).

# Part III: Administering Fedora

Part III consists of Chapters 10 through 14, which cover general setup and system maintenance tasks, including how to set up user accounts, automate system tasks, and back up your data. Chapter 10, in which you learn what you need to know about basic system administration, describes the root login, administrative commands, configuration files, and log files. Chapter 11 describes how to set up and provide support for multiple users on your Fedora system.

In Chapter 12 you learn to create shell scripts and to use the cron facility to automate a variety of tasks on your Fedora system. Techniques for backing up your system and restoring files from backup are described in Chapter 13. Chapter 14 describes issues related to securing your computing assets in Fedora.

# Part IV: Fedora Network and Server Setup

Part IV consists of Chapters 15 through 26, which describe step-by-step procedures for setting up a variety of server types. Simple configurations for what might otherwise be complex tasks are contained in each chapter. Learn to arrange, address, and connect your Linux computers to a local area network (LAN) in Chapter 15. Chapter 16 describes techniques for connecting your Linux computer and LAN to the Internet, using features such as Point-to-Point Protocol (PPP), IP forwarding, IP masquerading, routing, virtual private networks, and proxy servers.

Chapter 17 describes how to set up different types of print server interfaces, including Samba (to share with Windows systems) and native Linux printing. Chapter 18 describes file servers, such as Network File System (NFS) servers and Samba file servers. Chapter 19 describes how to configure sendmail or postfix e-mail servers.

Chapter 20 describes how to configure and secure an FTP server, as well as how to access the server using FTP client programs. Chapter 21 teaches you how to set up Fedora as a Web server, focusing on the popular Apache server software. Chapter 22 explains how to use LDAP to create a shared address book. Chapter 23 describes how to set up both DHCP and NIS services to distribute information to client workstations on the network.

Chapter 24 describes how to set up and use a MySQL database server in Linux. Chapter 25 takes you through the process of making the servers you configured in the other chapters available on the public Internet. Setting up a Domain Name System (DNS) server is also described in Chapter 25. Chapter 26 describes how to set up Fedora to be a Macintosh file and printer server.

# Part V: New Technology

Part V contains Chapter 27, which describes the Linux 2.6 kernel, and Chapter 28, which describes Security Enhanced Linux.

# Appendices

This book contains three appendices. Appendix A describes the contents of the companion DVD, Appendix B lists the hundreds of RPMs (software packages) that come with the Fedora Core 3 distribution, and Appendix C provides an overview of setting up and running network services.

# About the Companion DVD

The Fedora Core 3 DVD that accompanies this book provides the software you need for a complete working Fedora system. The software includes not only the binary installation packages but also the full set of Fedora Core 3 source code packages. With this software, you can install sets of software packages that result in personal desktop, workstation, or server configurations. This book describes how to configure and use the software for those different configurations.

# About the Companion Web Site

Even in a book that pushes the 1,000-page boundary, a few topics don't seem to make the cut. After you have gone through the book, you can visit the companion Web site at www.wiley.com/go/fedora3bible for some bonus material on topics such as using the X Window system, finding neat add-on software, and exploring alternative administrative interfaces.

Software moved to the Web site from previous editions of this book includes information on using legacy UNIX remote commands (rlogin, rcp, and the like), running Tripwire to manage system security, running a NetWare server in Linux (mars_nwe) and using crack and other password protection tools. Features moved from the immediately preceding edition include descriptions of the wu-FTpd FTP server, INN news server, and the sendmail.cf file.

# Reach Out

If you have any questions or comments about this book, feel free to contact me by e-mail at chris@linuxtoys.net.
