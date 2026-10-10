
is intentional, in the tradition of Windows, as a way of discouraging “average users” from messing around with their systems.

Difficulty in configuration will become an issue in Chapter 4. The host development environment, when we have to change some network parameters. I don’t recommend Ubuntu unless it’s your favorite distribution, and you’re very comfortable with it.

Ubuntu was the third most popular distribution in 2015.

## Red Hat Enterprise Linux

Red Hat Enterprise Linux (RHEL) is specifically targeted at the commercial market, including mainframes. There are server versions for x86, x86-64, Itanium, PowerPC, and IBM System z, and desktop versions for x86 and x86-64. While RHEL derives many of its features from Fedora, it has a more conservative release schedule, with major releases appearing about every 2 years. As of late 2016, the latest stable release is 7.2.

Even though RHEL is a commercial product, it is based entirely on Open Source code. Consequently, Red Hat makes the entire source code base available for download. Several groups have taken advantage of this to rebuild their own versions of RHEL. One of the best known of these is CentOS, said to be the 8th most popular distribution, as of late 2015. These rebuilds remove any reference to Red Hat’s trademarks, and point the update systems at non-Red Hat servers. Otherwise, they are functionally identical.

While the rebuilds are free, they are of course not eligible for any kind of Red Hat support.

## Fedora

The Fedora Project was started in late 2003 when Red Hat discontinued its retail line of Linux distributions to focus on enterprise software. The original Fedora release was based on Red Hat Linux 9. Red Hat continues to sponsor the Fedora Project, which serves as a launching point for releases of RHEL.

Fedora prides itself on being on the leading edge of open source software development and, as a result, it has a relatively aggressive release schedule, about every 6 months. As of July 2016, the current release is 24. Having started with Red Hat, Fedora was my favorite Linux distribution up to version 17. I tend to stay one or two major releases behind the leading edge, and only update about every two or three releases. I don’t have to have the absolute latest and greatest. Hey, if it works, stick with it.

> 2 And neither do you, by the way. The basic functionality doesn’t change that much from one release to the next. Much of it is cosmetic. If you’re just starting out, pick a fairly recent release and stick with it for a while.

Fedora only runs on Intel/AMD platforms.

I have two basic complaints about new releases. This may also apply to distros other than Fedora:

- Features tend to “move around.” I’m perhaps sensitive to this, because I’m inclined to use the graphical dialogs for configuration and setup. It seems like with each new release, the path to these dialogs changes.
- Each successive release seems to get more “Windows-like.” That is, more menus turn into cute icons rather than simple, straightforward text selections. This no doubt reflects a desire to appeal to a more “consumer” audience, but as a computer professional, I find it off-putting. Fortunately, at least for now, there are ways to revert back to the classical menu styles.

I stuck with Fedora 17 long after it was officially obsolete, because I ran into problems with later versions that I never could adequately solve. I subsequently shifted over to CentOS.

## CentOS

CentOS is an abbreviation for Community Enterprise Operating System. It is a free and open source version of RHEL. It is derived from the same open source code as RHEL, with Red Hat’s branding and logos changed.

In January 2014, Red Hat announced that it would sponsor the CentOS project, “helping to establish a platform well-suited to the needs of open source developers that integrate technologies in and around the operating system.” As a result of these changes, ownership of CentOS trademarks was transferred to Red Hat, which now employs most of the CentOS head developers; however, they work as part of the Red Hat’s Open Source and Standards team, which operates separately from the RHEL team.

The latest release is 7.2-1511, December 2015. As of release 7.0, CentOS only officially supports the x86-64 architecture. Unofficial ports are available for alternate architectures. Version 7 will have 10 years of support until 2024.

In July 2010, CentOS overtook Debian to become the most popular Linux distribution for web servers, with almost 30% of all Linux web servers using it, according to w3techs.com. Debian subsequently regained the lead in January 2012.

While just about everything in this book is “distribution-agnostic,” one area where distros tend to differ is in setup and configuration. We’ll confront that issue in Chapter 4, The host development environment, when we need to make some changes to networking. The descriptions there will emphasize CentOS. With that in mind, if you haven’t yet settled on a favorite Linux distribution, I would recommend CentOS, at least while you're working through the book.

## SUSE

SuSE was originally developed in Germany, with the initial release in 1994 making it the oldest existing commercial distribution. The name is a German acronym for Software und System Entwicklung (Software and Systems Development). The name was subsequently changed to SUSE, and is no longer considered an acronym.

Novell acquired SUSE Linux AG in 2003, and in 2005 announced the openSUSE project to allow outside developers to participate. SUSE Linux is available in two forms: openSUSE, driven by the openSUSE project; and SUSE Linux Enterprise, a commercial version. Much like Fedora, openSUSE is on the “bleeding edge” of Linux development with an aggressive release schedule, while SUSE Linux Enterprise sticks to a more conservative schedule.

## Hardware Requirements

Having selected a distribution, you need something to run it on. Any modern PC will work just fine as a development host. Minimum requirements are: a Pentium class processor, 1 GB of RAM for graphical operation, and at least 20 Gbytes of disk for a “workstation” class Linux installation. Of course, more RAM and disk is always better.

While you can “get by” with 20 GB of disk, later we’ll be building the Yocto project, which requires more like 50 GB. I do most of my Linux work on a “virtual” machine (more about that later) running under Windows 7 on an HP laptop. The virtual machine gets 1 GB of RAM and has a 65 GB disk. I currently run CentOS 7.

You will need at least one asynchronous serial port. A USB-to-serial converter should work fine. You will also need a network interface. We’ll use a combination of serial and network ports to communicate with the target, as well as to debug target code.

## Installation Scenarios

The next decision then is how you want to install Linux. There are basically three installation scenarios.

### Stand-Alone

This is the obvious choice if you can dedicate a machine to Linux. You will let the installation process format the entire disk.

### Dual-Booting

In many cases, though, you’ll probably want to install Linux on a machine that already runs some variant of Windows. There are a couple of approaches to that. This section describes dual-booting, the next one describes virtualization.

In the dual-boot scenario, you select at boot time which operating system to boot. That OS takes full control of the machine. The Linux installation will replace the standard Windows boot loader with GRUB, the GRand Unified Bootloader. GRUB then offers the option of selecting the OS to boot, as shown in Fig. 2.1.

While historically dual-booting has been the most popular installation scenario for average users, it is also the most complicated, because it requires reconfiguring your hard disk. The most common case is you already have a version of Windows installed on the machine, and you want to add Linux.

At this point Windows probably occupies the entire disk, and so you have to make space available for Linux. Fundamentally, this requires reducing the size of the disk partition holding Windows so you can create unallocated space for Linux. Remember that you’ll need on the order of 20 GB of disk space for Linux, so your disk must have at least that

![](img/f03d6fa2c5faefc793771df52bbb2ef9_33_0.png)

Figure 2.1 GRUB boot menu.
