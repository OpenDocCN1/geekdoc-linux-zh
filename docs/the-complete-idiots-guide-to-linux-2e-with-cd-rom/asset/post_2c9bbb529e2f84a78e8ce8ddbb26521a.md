
## Boot Manager Configuration
## Chapter 22—System Monitoring: Keeping an Eye on Your System
## Monitoring Memory
## How Much Memory: free
## Procinfo
## Monitoring Processes
## Listing the Current Top Processes: top
## Process Status: ps
## "Nicing" a process: nice and renice
## Monitoring Your Disk
## Finding out How Much Disk Files Consume: du
## Finding the Amount of Free Disk Space: df
## Log Files
## Monitoring Logins: last
## Monitoring Bad Logins: lastb
## Chapter 23—Sharing Files over the Network
## NFS
## Exporting an NFS Volume
## Mounting an NFS Volume
## FTP
## Connecting to an FTP Site
## Hosting an FTP Service
## HTTP
## Configuring an Apache Server
## Controlling Access
## SMB: Sharing Disks and Printers to PCs
## Accessing a PC Network Drive from Linux: smbclient
## Chapter 24—Customizing Your Linux Kernel
## Customizing Your Linux Kernel with LISA
## Customizing Your Linux Kernel by Recompiling
## Getting Started
## Configuring the New Kernel
## Compiling the Kernel and Necessary Modules
## Installing the New Kernel
## Installing the New Modules
## Configuring LILO
## Configuring the New Modules and Rebooting
## Appendix A
## Appendix B
## Index

Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions. Copyright © 1996-2000 EarthWeb Inc.
All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## 1, 2, 3 Go!

Welcome to Linux! It’s the software that is grabbing the world’s attention as a reliable and powerful operating system (OS). At the time of this writing, Linux and Windows NT are the only OSs gaining market share. Most other OSs are either stagnant or are losing their share to Linux or Windows NT.

## How to Use This Book

This book is a gentle introduction to Linux, and as such, it is not intended as a comprehensive guide. On the contrary, great effort has gone into this book to keep it from becoming yet another comprehensive reference guide. I’ve been selective about covering the topics you are most likely to use early in your Linux hacking career.

One of the interesting things about Linux, and UNIX in general, is that learning new ways and tools is almost an endless task. There are many tools—too many to cover even in several “comprehensive” volumes. Much of the comprehensive and exhaustive reference for Linux is readily available in various forms, some of which will be installed into your computer as part of the installation process.

In contrast, this book focuses on how to make you self-sufficient. It teaches you two ways of working with Linux: using the X graphical environment (with KDE) and using the shell, the command line interpreter so closely associated with UNIX. And, if you are managing your own Linux computer, there are some administrative tasks that you need to learn how to do.

So how is this book organized? Installation and first-time configuration instructions are located in Appendix A, “Linux Installation.” Appendix B, “OpenLinux Compatibility Guide,” provides you with an up-to-date list of the ever-growing and ever-changing list of hardware that is known to be compatible with Linux. While mapping your installation plan, you should verify that your hardware is listed and known to be compatible with OpenLinux.

After your initial Linux installation and configuration, start with Part 1, “Working with Linux in a Graphical Environment—The KDE Desktop,” and read the chapters in order. (We’ve structured the chapters counting on you doing so.) Part 2, “Working on the Command Line,” introduces similar concepts as Part 1, this time using a shell instead of a graphical user interface. Last, Part 3, “Essential System Tasks Under Linux,” focuses on various administration tasks that you’ll need to do occasionally. Keep in mind that while you are learning Linux, you are also learning UNIX. What you learn here will transfer with little modification into other UNIX environments.

Have fun getting to know your new operating system!

## Why Linux?

So why all the attention? UNIX has been around for a number of years, and although believed by some to be the only choice among real OSs, it has remained in the vertical market arena until very recently. But what does this mean? UNIX (or Linux, which is based on UNIX) provides a very robust environment in which to run and deploy applications. By design, it offers the following features:

- Multiuser support
- Security
- Full multitasking
- Networking support for client and server applications
- Source code

These are features that some of the PC OSs available today don’t offer, or they have been added as an afterthought. These are all very important features, especially in the context of today’s networked environments where computers share information.

Unlike Windows-based systems, UNIX is able to support multiple users concurrently. A single UNIX/Linux computer can have multiple users working on it (running programs, accessing files, and other services) at the same time, either seamlessly across a network or through a directly attached console (a screen and keyboard).

As a result, UNIX and Linux offer an environment where many (hundreds) of users can simultaneously access a system, if the system has enough resources. With so many potential users, how do you protect important files from unauthorized access? Linux’s UNIX roots handle security transparently, not as an afterthought, but as part of the Linux way of life. In order for you to work on the computer, you have to sign in.

Security isn’t Linux’s only kudo. It’s also an expert juggler! How else could you simultaneously support multiple users? Linux is a multitasking OS. It juggles multiple programs and users at the same time, creating the illusion that each user is working on his or her own computer. Obviously, only a little tiny bit of work can be done in a slice of time, but the illusion is well maintained. Other OSs that claim to be multitasking usually don’t scale well. When a few users are accessing the services, performance rapidly decreases. The juggling illusion becomes reality for platforms that support multiple processors. The computer can, in fact, juggle multiple things at the same time. The Linux OS takes advantage of these hardware configurations and makes use of the additional processing power to increase performance to new levels—usually with better results than the original OS the hardware was designed for.

Many of today’s computers rely on a networked environment. “The network is the computer”℠ is the famous slogan for Sun Microsystems, a large UNIX vendor. The network is indeed the computer. Information exchange via email, the Web, and other mechanisms is an everyday fact. Linux can not only participate as a client for such services, but it can also offer them to other PCs and workstations. Linux, in fact, powers many Internet service providers (ISPs) and the users who access the ISP’s services. It is well tested and reliable.

Not many commercial environments provide the source code to how they work, and then do so freely. That’s where Linux steps out from the crowd! Having the source code allows information service (IS) departments, or hackers as well, to customize the particular behavior of the OS or a program distributed with it to fit a particular need. Companies concerned about security issues can examine how the software really works and make their own evaluations and adjustments. In the event of a problem, someone with the right background can generate a fix, usually within hours of a problem or security issue being discovered. Compare that to waiting for days, weeks, or months for bug fixes—the norm that most of us have come to expect with other OSs. For the student, having access to the source code provides insight into how systems are made and built.

On the downside, UNIX and UNIX-like OSs have lacked ergonomics on the surface, providing confusing interfaces that vary from program to program and vendor to vendor, and generally aren’t intuitive for nonexpert-type users. Mainstream application developers not seeing profitability with these environments have chosen to keep their wares on other, more profitable OS platforms. But that attitude is rapidly changing in the Linux market.

With its newfound popularity, Linux has encouraged big software developers such as Oracle, Sybase, Corel, and many others to develop versions of their applications for Linux systems. The world is beginning to take Linux seriously—and a little sponsoring goes a long way! This in itself has generated additional media interest, and Linux coverage has changed from a curiosity in obscure publications to a viable business option and alternative to heavyweight products from other companies. This is great news, because the more developers entering the Linux arena, the more popular and accessible this OS environment becomes!
