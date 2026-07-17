![](Images/cover00141.jpeg)

Karnel Erickson

Linux for absolute beginners

First published by Karnel Erickson 2022

Copyright © 2022 by Karnel Erickson

All rights reserved. No part of this publication may be reproduced, stored or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning, or otherwise without written permission from the publisher. It is illegal to copy this book, post it to a website, or distribute it by any other means without permission.

First edition

This book was professionally typeset on Reedsy
Find out more at [reedsy.com](https://reedsy.com)

![Publisher Logo](Images/image00103.jpeg)

# Introduction

If you have spent much time in the world of computer technology, you have probably come across the name “Linux” several times. You may have heard that it is open source and available for free download, but that information doesn’t explain Linux.

**Linux as an Operating System**

Linux is just an operating system. “Operating system” is probably a word that you use regularly, but most people don’t understand what an OS is.

All of the software and hardware on your computer is run through the OS. That is why, if you have an Android phone, you have to download Android apps, and if you have an iPhone, you have to download Apple apps. Different operating systems have additional requirements for both their hardware and software, and you have to abide by these requirements for the programs on your computer to work. Most computers come with an OS already installed, which enables users to immediately begin to access the information and capabilities of their computers. Most other computers come with a Windows OS pre-installed. They allow you to get started with your computer right away.

An OS is an interface that allows you to interact with the information on the computer. The earliest operating systems used a command-line interface, which meant that users had to type out a code to access a program. The most common one was MS-DOS, which Microsoft released in the year 1981\. Operating systems today use a graphical user interface or GUI. This means that you can physically see, like images, the different applications, and programs that you want to access. You just have to click on the icons and they open up. Different operating systems use a different GUI, so switching from one OS to another can cause some confusion at first. The look and feel will be different and may take some getting used to.

Operating systems have to be continually updated to keep up with the ever-growing software and hardware improvements. You may have experienced this frustration if you have tried to use the newest version of Microsoft Word (or any other program) and found that it is incompatible with your computer. The problem isn’t that your computer has malfunctioned but that your operating system isn’t advanced enough to handle the latest version of the software. Updating an OS can take up a lot of memory, so having an up-to-date one may mean getting a computer that has more memory. You may have to choose between getting a new computer and working with an outdated OS.

The three most common operating systems are Windows, Mac, and Linux. Windows was created by Microsoft in the 1980s to replace MS-DOS. It was much more user-friendly because people no longer had to keep track of different codes necessary to access their programs.

# What Is Linux?

The kernel of an operating system based on UNIX concepts is known as Linux. The name comes from the first name of its Finnish creator, Linus Torvalds, and it is based on the same technique as other UNIX-based systems (the last letter is an x). Linux is now developed and maintained by tens of thousands of people all over the world.

An operating system’s kernel is its beating heart. It’s essential for communication between your computer’s hardware and you, the user. An operating system is made up of several software components, including a kernel, numerous tools, and libraries. It is software that extends your computer’s core operating system, known as the BIOS.

**From UNIX to Linux**

Linux has a long history dating back to the 1990s. However, to comprehend the origins behind Linux, we must first take a glance back at the early days of computers following World War II.

Computing devices occupied entire buildings at the time, and the transition from mechanical to electronic components, such as microprocessors and multi-layer circuits, was well underway.

Furthermore, hardware and software components were both expensive and non-standardized throughout the 1960s and 1970s. There were a variety of vendor-specific platforms, each with its own interface, data transfer and exchange protocols, and operating system. The communication between these single computing devices needs specialized knowledge and protocol comprehension. UNIX was created to overcome these barriers and simplify the use of computing devices on a greater scale.

**UNIX**

In January 1965, work on the Multiplexed Information and Computing Service (Multics) began.

Multics was developed in collaboration by the Massachusetts Institute of Technology (MIT), General Electric (GE), and Bell Labs/AT&T. The main product they developed was Unics, which was led by Ken Thompson and Dennis Ritchie. It was later renamed UNIX. The UNIX operating system was widely utilized at the University of California, Berkeley.

**UNIX Variants**

The concept of UNIX became licensed to several companies that developed and maintained their variant of UNIX. This included Solaris/SUN OS (SUN Microsystems nowadays owned by Oracle), AIX (IBM), Scenix (Siemens), SCO UNIX, Xenix (Microsoft), as well as HP-UX (Hewlett-Packard), NeXTSTEP, Mac OS (Apple), and Android (Google).

Open-source implementations comprised the Berkeley System Distribution (BSD) with its variants: NetBSD, OpenBSD, and FreeBSD. Today, Linux is the most popular free software among open-source developers. There is also solid commercial support for the systems mentioned above.

**The UNIX Philosophy**

UNIX is designed with several strict principles in mind. These principles cover portability, multi-tasking, and multi-user orientation combined with a time-sharing approach. Furthermore, it is based on network connectivity following the TCP/IP scheme.

The initial development in the C programming language resulted in independence from a hardware platform. Delivered with a selection of development tools and libraries, it allows you to effortlessly extend it to your specific needs. It is simple but powerful to automate tasks that support complex but maintainable scripts.

Similar to a toolbox, UNIX consists of a variety of tools. Each one has a certain function and is designed to fulfill that function. The idea is to use one device per task. To achieve more complex goals, you combine several tools into a chain. The following example incorporates the two commands ls and wc employing a pipe to count the number of Python files in the current directory.

$ ls *.py | wc -l

6

$

We will explain these commands and their usage in more detail later on in the guide.

**A Brief History of Linux**

Similar to UNIX, the Linux operating system has different roots and is based on the work of quite a few masterminds. This includes Richard M. Stallman, Andrew S. Tanenbaum, and Linus Torvalds.

Richard M. Stallman, a hacker and developer at MIT, is the first president of the Free Software Foundation (FSF) and the father of the GNU project. GNU abbreviates the slogan GNU is Not UNIX. The project’s purpose was to provide a free UNIX operating system. Until the 1990s, a collection of tools was available, but the kernel was still missing. The entire software was published under the GNU Public License (GPL) around 1983.

The next step for Linux came from Andrew S. Tanenbaum. At the time, he was a professor at the University of Amsterdam. He developed Minix, an operating system for educational purposes for his students to demonstrate and understand the UNIX principles. But, as he pointed out, Minix was not intended to be used in practice.

Linus Torvalds, a Finish student at the University of Helsinki, was a user of Minix and quite unhappy with its boundaries. In 1990, he began to develop a new operating system based on the ideas of Minix, the UNIX principles, and the POSIX standard. His motivation was to have his own system that was understandable and maximized to the boundaries of the hardware. He also wanted to have fun and had no commercial intent in mind. The entire story behind Linux is described in his autobiographical book titled Just for Fun. Today, Linus Torvalds oversees the development of the Linux kernel.

It needed a nice logo to make Linux attractive to the outside world. Based on a competition for mascots, many proposals were handed in. Larry Ewing sent in his idea for a penguin, as seen on the cover of this book, and his proposal won. Designed with a cheeky smile and a well-fed body, this penguin named Tux represents the image of a happy and satisfied user.

**Linux Range of Use**

Linux was originally built for Intel-based systems, although it now runs on a wide range of platforms. ARM architectures (arm and arm64), Motorola/68k Freescale’s architecture (m68k), Intel x86 (i386 and amd64), IBM s390 (s390), PowerPC (PowerPC), and SPARC (sparc) are just a few examples.

Linux was designed with server systems in mind from the start. As a web server, file server, mail and news server, internet gateway, wireless router, and firewall, it is widely used. Used as a computing unit, it helped render video sequences and entire films such as Titanic, Shrek, and Toy Story. Furthermore, Linux is used in automotive products, astronautics, military, logistics, and the engineering environment. All of the world’s stock exchanges have been run on Linux servers since 2006\. Almost all online search engines are also run by it.

Linux has also swept the desktop during the previous decade. It’s a solid configuration for text processing, graphic design, desktop publishing, spreadsheet computations, communication (email, chat, audio, and video), and user interfaces for your phone and television because of its high flexibility and reliability.

**Linux Certifications**

The rising adoption of Linux has boosted the demand for engineers and users who are well-versed in the operating system. A Linux certification becomes helpful at this time. There are two types of certifications: general (not specific to distribution) and targeted (specific to distribution) (specific to a Linux distribution). The tables below provide an overview of the most common certifications currently available.

**Non-specific Certifications**

*   Linux Essentials
*   LPIC-1: Linux Server Professional Certification
*   LPIC-2: Linux Engineer
*   Linux Foundation Certified System Administrator (LFCS)
*   Linux Foundation Certified Engineer (LFCE)
*   CompTIA A+
*   CompTIA Network+

**Distribution-specific Certifications**

*   RedHat Certified Engineer (RHCE)
*   RedHat Certified System Architect (RHCSA)
*   RedHat Certified Architect (RHCA)
*   SUSE Certified Administrator (SCA)
*   SUSE Certified Engineer (SCE)
*   SUSE Enterprise Architect (SEA)

**Installing Linux**

People think installing the Linux operating system is a very tough task. It is known to have the most uncomplicated installations compared to the other operating systems. Most of the Linux operating system versions offer you Live Distribution. It means that the installation can be done with the help of a CD or USB without making any considerable changes to your hardware. Isn’t this just amazing? These distribution options provide you with full functionality without installing it forever.

For example, the following are the steps for Ubuntu Linux that will guide you through the installation process:

*   Preparation

The first thing to ensure is that your machine meets the requirements. Next, it might ask you whether you want to install third-party software.

*   Wireless setup

When you install the system on the laptop, you will have to connect to a network to ensure that third-party software download is successful.

*   Hard drive allocation

It is the step where you need to choose the way you want the Linux operating system to be installed on your desktop or laptop. Are you going to go with dual booting? Then use the whole hard drive upgrade the present installation.

Choose the kind of installation you prefer and then click on install now.

*   **Location:** choose location from the map
*   **Keyboard setup:** choose the keyboard setup
*   **User setup:** type in your username and password to finish

the installation

After these steps are followed, reboot, and it is ready to go! Installing Linux is known to be the simplest, as well as the safest, software when compared to other operating systems.

**Important Considerations While Installing Linux**

Installing Linux is pretty easy as almost every distribution has its graphical install scheme. Nowadays, installation is a piece of cake, involving only a few clicks as the software data has grown enormously over the years. That is why most distributions only provide the primary material for running the Linux in the shape of CD and DVD. Distributions further provide links to the online repositories, which can be downloaded later after the primary installation from CD and DVD. Installation now is a mere setting of initial configuration, which can be enhanced later by downloading the specific drivers of your choice from the online repositories. Many distributions also provide you with the freedom of creating your install discs. You can install the software of your liking on your own CD/DVD.

Some important installation considerations include the following.

*   Software available on CDs and DVDs is prone to outdating.

Thus, the need for online repositories becomes critical as it helps

download and update the software.

*   Some distributions keep on updating their original releases

now and then. These updated versions are available on their re

spective sites and must be checked for their availability.

*   Hardware is mainly automatically detected nowadays. It inclu

des your monitor and graphic cards, etc.

*   Most distributions provide Parted (partition management

tool). It’s straightforward to use and helps you in setting up your

partitions.

*   Some sources can be utilized for installation purposes. For

instance, network methods like NFS, Hypertext Transfer Protocol

(HTTP, and File Transfer Protocol (FTP).

*   Boot managers like GRUB or Linux Loader (LILO) usually

support the dual-boot installation. These boot loaders can be ea

sily configured to boot Mac, Windows, and other Linux installa

tions on the same system.

*   Distributions deal 32-bit and 64-bit as separate entities and

provide their different releases. Newer computers support 64-bit

nowadays, whereas weaker systems support 32-bit.

*   Dynamic Configuration Protocol (DHCP) or IPv6 helps con

nect to a network router, and this network configuration usually is

automatic.

*   RAID and LVM file systems can be set up during installation,

as you have the option to customize your partitions using Parted.

*   It’s incredibly vital to have a separate boot partition if you are

using LVM and Raid file systems.

*   Most distributions also run a post-installation process. It helps

perform the basic configuration tasks like creating a user account,

setting the date and time, and configuring your firewall.

Linux system can be accessed in rescue mode, and most distributions provide this facility. If your system stops working, your install disc can access your files. Your install disc uses the command line interface and helps you access your installed file system. The configuration files can be edited and replaced, allowing you to fix your problem. This technique is helpful for X Window System.

A GRUB boot loader is prone to glitches, especially installing Windows on your system. It happens because Windows overwrite your boot manager. GRUB can be reinstalled utilizing the grub-install command, and once you have installed it, be sure to mark that for the Windows system. It should be noted that some distributions use alternative boot loaders like LILO.

What are the reasons to use the Linux operating system?

Why would you want to learn a computing program that is entirely different when the laptop, desktop, and other servers are shipped with the Operating System that works perfectly? This is the question that comes up in most users’ minds. But, before you get an answer to this, there is one more question, is the operating system you are working on really working as perfectly as you wanted? Are you frequently battling slowdowns, viruses, expensive repairs, and malware? If yes, then it is the right time to free yourself from the constant frustration, as well as fear of losing your important data. Linux is the best solution for you, and you need to start using this operating system at your earliest convenience.

Linux is known to be the most reliable operating system. You get a dedicated operating system by paying nothing, seriously. You can install Linux on as many laptops or desktops you want for free.

When Linux is compared to the other servers such as Windows Server, the latter costs around $1200 and does not include the basics like Client Access License and also additional licenses including mail server, web server, etc., the Linux Server is free, and you do not have to pay a cent to use its reliable programs. It is free and also simple to install. When you have Linux as the operating system, you do not have to do babysitting every day. One service needs restarting, upgrading, etc., and the other parts are not affected.

This operating system is distributed under the open-source license, and mentioned below is a list of ideas that follows:

*   The liberty to run any program.
*   The liberty to make changes to the programs according to your

preference.

*   You can even redistribute copies to help your loved ones.
*   Lastly, you can distribute the copies of the modified version

you created to your loved ones.

Thus, it is a community created by you, for you. It is known to be the most straightforward and user-friendly operating system. It is all about freedom. Complete Linux installation can be done on your desktop or laptop as it does not involve a lot of complexities.

**Development**

The Linux operating system includes some development languages. Most of the distribution codes are created in C or C++ Languages. The rest of the regulations are created with Perl, Java, as well as Lisp. One of the most important parts of the Linux operating system, The Kernel has a 95% C presence. The remaining part is used with other languages that make this part more diverse when compared to the other systems. There are a few developers that at present use text-based tools to develop the code. Linux is known to be the most versatile operating system and a strong integrated development environment. It is a platform that can help you generate money while being free of cost. Users can be sure that the Linux operating system can work best for them.

# Linux Directory Structure

Now that you can connect to the server and have been introduced to the interface you will be using, it’s time to learn about the directory layout. In addition, it can help you answer questions like:

*   Where are programs located?
*   Where do configuration files live?
*   Where might I find the log files for this application?

**Common Directories**

Here are the most common top-level directories you need to be aware of and interact with as an average user.

**Comprehensive Directory Listing**

Here is a comprehensive list of top-level directories that you may find on various Linux systems. Some subdirectories are included to help define the purpose of the top-level directory. You may never interact with many of these directories. These directories will be on every system you encounter, like /usr.

/cgroup—Control Groups hierarchy.

Operating system and the system administrators.

/lib64: System Libraries, 64 bit.

/media: Used to mount removable media like CD-ROMs.

/mnt: Used to mount external file systems.

/proc: Provides information about running processes.

/sbin: System administration binaries.

/selinux: Used to display information about SELinux.

/srv: Contains data that is served by the system.

/srv/www: Web server files.

/srv/ftp: FTP files.

/sys: The device and busses known to the Linux kernel are di

splayed and sometimes configured with this command.

/tmp: Temporary space, typically cleared on reboot. This direc

tory can be used by the OS and users alike.

/usr: User-related programs, libraries, and documentation. The

sub-directories in /usr relate to those described above and below.

/usr/bin: Binaries and other executable programs.

/usr/lib: Libraries.

/usr/local: Locally installed software not part of the base opera

ting system.

/usr/sbin: System administration binaries.

/var: Variable data, most notably log files.

/var/log: Log files.

**Unix: Specific Directories**

Linux is often found in environments with other Unix variants. If you ever need to log into a Unix server, you may see some of the following Unix-specific directories.

![Image](Images/image00104.gif)

Note that you may encounter other top-level directories that have not been listed above. However, those were most likely created by the system administrator

**Application Directory Structures**

Applications can follow the same conventions employed by the operating system. For example, here is a sample directory structure of Apache installed in /usr/local.

![Image](Images/image00105.gif)

Here is what it might look like if it was installed in /opt.

![Image](Images/image00106.gif)

A common alternative to placing all the application subdirectories in /opt/app-name is to also use /etc/opt/app-name and /var/opt/app-name.

![Image](Images/image00107.gif)

Sometimes applications that are not part of the standard operating system are installed in a shared manner and are not given their subdirectory. For example, if Apache were installed directly into /usr/local, its binaries would live in /usr/local/bin, and its configuration would live in /usr/local/etc. However, Apache may not be the only locally installed software, sharing that space with the other installed applications.

Another common practice is to create a directory structure based on a company, organization, or team name. For example, if you work at the Acme Corporation, you may find a directory named /opt/acme or /usr/local/acme. Sometimes scripts and utilities are installed directly in that structure, and other times there are segregated into their subdirectories. Here’s an example.

![Image](Images/image00108.gif)

Alternatively, you may see something like this.

![Image](Images/image00109.gif)

Here are variations on the same idea but based on a team within the company.

![Image](Images/image00110.gif)

**Example Top Level Directory Listings**

Here is a listing of the top-level directories for a few different Linux servers:

Red Hat Enterprise Linux 7 (RHEL)

[bob@rhel6 ~]$ ls -1 /

*   bin
*   boot
*   group
*   dev
*   etc
*   home
*   lib
*   lib64
*   lost+found
*   media
*   mnt
*   opt
*   proc
*   root
*   sbin
*   SELinux
*   srv
*   sys
*   top
*   usr
*   var
*   SUSE Linux Enterprise Server 11 (SLES)
*   [bob@sles11 ~]$ ls -1 /
*   bin
*   boot
*   dev
*   etc
*   home
*   lib
*   lib64
*   lost+found
*   media
*   mnt
*   opt
*   proc
*   root
*   sbin
*   SELinux
*   srv
*   sys
*   top
*   usr
*   Ubuntu 14.04 LTS
*   [bob@ubuntu12 ~]$ ls -1 /
*   bin
*   boot
*   dev
*   etc
*   home
*   lib
*   lib64
*   lost+found
*   media
*   mnt
*   opt
*   proc
*   root
*   run
*   sbin
*   SELinux
*   srv
*   sys
*   top
*   usr
*   varDeep Dive
*   Filesystem Hierarchy Standard
*   man hier
*   RedHat Enterprise Linux
*   SUSE Linux Enterprise Server
*   Ubuntu

One of the best features of Ubuntu is that it is free open-source GNU/Linux software. This means that the software may be freely used, copied, modified, and redistributed. Open-source software is developed, maintained, and distributed by a worldwide community of people. The software is owned by the community and the development process is transparent. This makes for more stable and reliable code that is practically malware-free, easy to install, and easy to use.

GNU is a set of Unix-like programs that provide basic functionality for the Linux system. Linux would not exist without the GNU tools and applications. This is why some people refer to the GNU/Linux operating system as opposed to just Linux. GNU is an acronym for GNU’s Not Unix. GNU is a FOSS (Free Open Source Software) implementation of basic Unix programs.

GNU/Linux has been under development for over twenty years and is a very mature operating system. The Linux kernel was designed by Linus Torvalds in 1991\. The GNU system was designed by Richard Stallman. GNU/Linux is now maintained by The Free Software Foundation. The design of GNU/Linux is based on Unix, which was created by AT&T Bell Labs starting in 1969\. So the heritage of GNU/Linux spans more than forty years. Unix and GNU/Linux have a well-defined file system and a simple modular software design which translates to smaller, simpler, and faster software. We are all beneficiaries of this elegant design concept.

The popular Linux logo, Tux the penguin, was created by Larry Ewing and it may be found on numerous stickers, decals, pins, tee shirts, and toys.

**Installing Ubuntu**

**New Features:**

**Brasero**

The Brasero CD/DVD burner is no longer part of the distribution. Instead, the file manager performs that function.

**Launcher Location**

The launcher may be moved to the bottom of the screen, if desired.

**Logout, Shutdown, and Reboot Icons**

Searching using Dash, Applications Lens for logout, shutdown, or reboot will display the icon that may be placed on the launcher.

**Online Search via the Dash**

The default value for online search is now OFF when using the Dash.

**LibreOffice 5**

LibreOffice 5 is now the default version for LibreOffice.

**Software Center**

The Ubuntu Software Center has been replaced with Ubuntu Software on the launcher.

**Installing .deb Packages**

Double-clicking on a .deb file activates Ubuntu Software to install the new software package; however, I recommend installing gdebi and using it to install packages because it is faster and more reliable.

**Cautions**

**OS Upgrade Problem**

The Software Updater will automatically check for available updates. The Software Updater may ask if you would like to upgrade to a newer release of Ubuntu. This is a long and error-prone process. The upgrade process has failed in the past but might work ok now. You may choose the upgrade option or install the new version of Ubuntu manually. It’s your choice.

**Upgrade Dialog**

**Installation Cautions**

You will need to be logged into your system administrator account to perform any of the pre-installation or post-installation steps that involve installing new software on your computer. You may need to install software to create a bootable USB stick, before performing the actual Linux installation. You will also need to install updates after performing the Linux installation.

You will be asked to enter a user name and password during the installation process. Since this user will be created with administrative privileges, you should enter a user name like Linux or SysAdmin. You will be able to create your own user account after the installation has finished. Your actual login name for Ubuntu will be Linux if you entered Linux during installation. Linux user names are historically all lower case. However, that is not the case for passwords.

You will be asked if you want to try Ubuntu before installing or install Ubuntu immediately. I recommend installing Ubuntu without trying it if you have already decided to install it. If you decide to try Ubuntu without installing it, there will be an Install icon on the desktop that will then allow you to install Ubuntu. This will not work on some older computers so I recommend that you do not install Ubuntu from the desktop.

**Updates during Installation**

Do not check the boxes:

[ ] Download updates while installing

[ ] Install third-party software

I strongly recommend installing updates and third-party software after the operating system installation has finished. If the updates fail, then the entire installation will fail.

**Disk Configuration**

You will be asked the following question if your hard drive has an installed operating system:

This computer currently has multiple operating systems on it. What would you like to do?

(•) Install Ubuntu alongside them

( ) Erase disk and install Ubuntu

The default option is Install Ubuntu alongside them. However, you may want to erase the disk and install Ubuntu as the only operating system by selecting the other option.

If you want to save the current data and operating system, then use disk imaging software like Clonezilla to save the current disk image.

Some of the installation dialog boxes may require the use of the keyboard for navigation. The navigation keys are the arrow keys, the Tab key, and the Enter key.

Downloading Ubuntu

Linux distributions are stored in ISO files, which may be described as a cd image file. Wikipedia has an excellent article on ISO image files if you would like more information about ISO files.

This book assumes that you are installing Ubuntu on a PC-type computer. To create a CD that will allow us to install Ubuntu, we need to find and download the ISO file from the internet first. This could be done by simply searching for Ubuntu download or by searching for a specific Ubuntu distribution like Ubuntu 16.04, for example.

The Ubuntu web page will have two basic selections:

*   Download 32 BIT
*   Download 64 BIT

The 32-bit version will work on any computer. If you have a 64-

bit computer and would like to try the 64-bit version, then select

Download 64 BIT.

Note that the ISO file may be too large to fit on a cd, so you may have to use a DVD. Once you have downloaded the cd image file, you may write it to a DVD. The image file must not be stored on the DVD as a file. It must be stored as an image. This is accomplished by storing the file as an image or burning the contents of the image file. Different CD/DVD burning programs may use other terminology for creating an image DVD. You cannot simply copy the image to a DVD as a file.

Ubuntu may also be installed from a USB memory stick. The process for creating the memory stick is a bit more complicated than creating the cd. First, you will need to download and install the UNetbootin application on a Linux or other computer. Then you will need to ensure that the UNetbootin application is executable by setting its file properties. The application may then be executed and it will create a bootable USB memory stick. Refer to the screenshot on the next page for setting the properties of the UNetbootin executable on a Linux computer.

**Screenshot – UNetbootin Properties**

Note that you may have to unblock the UNetbootin application if you are installing it on a non-Linux computer. Simply right-click on the UNetbootin icon and select Properties and then simply hit the Unblock button.

If you are installing UNetbootin on a Linux computer, you will also need to install the p7zip-full package using the command line or the Synaptic Package Manager guide.

Plug in a USB memory stick with at least 2 GB storage capacity. Launch the UNetbootin application. Use the Select Distribution plus the Select Version buttons to download the image file.

If the Linux distribution that you would like to install is not listed on the Select Distribution and Select Version UNetbootin menus, you will need to download the desired ISO file from the internet. Then choose the ISO file that you downloaded by selecting Diskimage and then click on the […] button to select the ISO file.

Select the USB stick that was just plugged into the computer with the Drive: selection menu. Once all of the options have been selected, simply hit the [OK] button to create the bootable USB stick. This could take about five minutes so don’t worry if the process seems to be stopped.

# Ubuntu First Approach

Ubuntu 16.04 is an LTS (Long Term Support) version of Ubuntu with a support duration of five years. It will run on older computers with an Intel Celeron or Core i3 processor and needs little memory or hard drive space. It also helps to have an SSD (Solid State Drive) in the computer because it is faster than a conventional hard drive. For example, I have Ubuntu Unity running on an older Dell E4200 laptop I purchased on eBay for about $100, and it boots in 17 seconds.

The Unity desktop has sparked a lot of debate, but I’m using it on numerous computers and laptops and really like it.

This edition of the Ubuntu User Manual covers Ubuntu 16.04, which will be the LTS version for five years. Which version to install remains your decision? It is easy enough to try different versions yourself.

Ubuntu will install and run on computers with one GB of memory and eight GB of hard drive space. Ubuntu Unity has a unique user interface system using the top panel and left sidebar launcher. Options to change the launcher, wallpaper, and themes are available. The user may also add or remove Linux applications as desired.

Ubuntu uses the Unity desktop. Unity requires more physical resources (memory and CPU) than some lighter-weight Linux desktop software. Therefore, it may appeal to people who like Apple computers and casual users. However, power users may not select the Unity user experience. There are more technical discussions of Unity in Wikipedia and elsewhere. I am only interested in how to use and customize Ubuntu.

# Linux Boot

**The BIOS**

BIOS stands for Basic Input/Output System. It’s a particular type of firmware used in the booting process, and it’s the first piece of software that is run when a computer is powered. The BIOS is an independent operating system.

Depending on the hardware, the BIOS provides a list of boot devices such as hard disks, DVD drives, USB devices, and others. But, again, the critical combination necessary to accomplish this will differ depending on the hardware manufacturer.

The BIOS will launch the boot loader after a bootable device has been discovered. Although you may come across older Linux systems that use the LILO boot loader, the GRUB boot loader is the most common.

The boot loader’s principal function is to start the operating system in any event. You will typically see a message or series of news from the boot loader, which will allow you to interrupt the boot process and interact with the boot loader. For example, you can tell the boot loader which operating system to execute if multiple operating systems are installed. You can also say to the boot loader to give the operating system different boot options.

**The Initial RAM Disk**

The initial RAM disk, abbreviated as “initrd,” is a temporary file system put into memory when the system boots. This file system may include helpers that conduct hardware detection and load the required modules, often known as drivers, to mount the existing file system. So, if the root file system is stored on an LVM (Logical Volume Manager) volume, the operating system continues loading from the natural root file system.

**Kernel and Initial RAM Disk Location**

/boot contains the Linux kernel, the initial RAM disk, and other files required to boot the operating system. The /boot directory for an Ubuntu system is listed below.

$ ls -1F /boot

abi-3.13.0-46-generic

config-3.13.0-46-generic

grub/

initrd.img-3.13.0-46-generic

System.map-3.13.0-46-generic

vmlinuz-3.13.0-46-generic

The Linux kernel is commonly referred to as vmlinux or vmlinuz. The vmlinuz format is used if the kernel is compressed. The kernel used in this example is vmlinuz-3.13.0-46-generic. In this example, the initial RAM disk is initrd.img-3.13.0-46-generic.

Previous messages are discarded when the pad is full to make room for new ones. Use the dmesg command to view the contents of the kernel ring buffer.

$ dmesg

[ 0.000000] Initializing cgroup subsys cpuset

[ 0.000000] Initializing cgroup subsys cpu

[ 0.000000] Initializing cgroup subsys cpuacct

[ 0.000000] Linux version 3.13.0-46-generic (buildd@orlo) (gcc

version 4.8.2 (Ubuntu 4.8.2-19ubuntu1) ) #79-Ubuntu SMP Tue

Mar 10 20:06:50 UTC 2015 (Ubuntu 3.13.0-46.79-generic 3.13.11-

ckt15)

[ 0.000000] Command line: BOOT_IMAGE=/boot/vmli

nuz-3.13.0-46-generic root=UUID=736134da-c6b8-4a97-911c-

650146a68b3c ro console=tty1 console=ttyS0

[ 0.000000] KERNEL supported cpus:

[ 0.000000] Intel GenuineIntel

[ 0.000000] AMD AuthenticAMD

[ 0.000000] Centaur CentaurHauls

[ 0.000000] e820: BIOS-provided physical RAM map:

…

On most Linux distributions, these messages are saved to disk in the /var/log/dmesg file. You can observe the messages the kernel is creating with the dmesg command and the /var/log/dmesg log file, even during the early phases of the boot process when those messages can fly by your screen.

**Runlevels and Targets**

Finally, runlevel 6 is used to reboot a system.

Runlevel Description

0Shuts down the system

1.  S, single-user mode. Used for maintenance.
2.  Multi-user mode with a graphical interface.

(Debian/Ubuntu)

3.Multi-user text mode (RedHat/CentOS)

4.Undefined

5.Multi-user mode with graphical interface.

(RedHat/CentOS)

6.Reboot

Previously, the init program was in charge of runlevels. /etc/inittab was used to hold the init configuration. You would modify the /etc/inittab file and adjust the runlevel number on the initdefault line to alter the default runlevel using init. As an example, here’s how to make runlevel 3 the default runlevel.

id:3:initdefault:

Init alternatives such as systemd and upstart, on the other hand, are quickly displacing init, with systemd currently being the most frequently adopted.

Systemd uses the concept of targets instead of runlevels. Runlevels are generally equal to these targets. Look at /lib/systemd/system for a list of accessible targets. The runlevel targets are essentially symlinks to the actual targets.

Runlevel5.target, for example, is a symlink to graphical.target.

# cd /lib/systemd/system

# ls -l runlevel*target

lrwxrwxrwx. 1 root 15 Jul 17 2014 runlevel0.target -> poweroff.

target

lrwxrwxrwx. 1 root root 13 Jul 17 2014 runlevel1.target -> rescue.

target

lrwxrwxrwx. 1 root root 17 Jul 17 2014 runlevel2.target -> multi-u

ser.target

lrwxrwxrwx. 1 root root 17 Jul 17 2014 runlevel3.target -> multi-u

ser.target

lrwxrwxrwx. 1 root root 17 Jul 17 2014 runlevel4.target -> multi-u

ser.target

lrwxrwxrwx. 1 root root 16 Jul 17 2014 runlevel5.target -> graphi

cal.target

lrwxrwxrwx. 1 root root 13 Jul 17 2014 runlevel6.target -> reboot.

target

To change the default runlevel or target using systemd, use the systemctl command, followed by set-default, and then the desired target. You can also manually establish a symlink from the /etc/systemd/system/default.target file to the desired destination. This example makes graphical the default target, which is equivalent to runlevel 5.

# set-default multi-user.target

rm ‘/etc/systemd/system/default.target’

ln -s ‘/usr/lib/systemd/system/multi-user.target’ ‘/etc/systemd/

system/default.target’

#

**Changing Runlevels or Targets**

With the init system, you can change runlevels using the telinit command. Simply supply the runlevel you want to switch to as an argument to the telinit command.

# telinit 5

To change the target, the runlevel equivalent for systemd, use the systemctl command followed by isolate and finally the desired target. For example, here is how to change to the graphical target.

systemctl isolate a graphical target

**Rebooting a System**

Even though there is a runlevel/target if you’re using systemd, you can also use the reboot or shutdown commands for rebooting.

Here’s how to reboot with init.

# telinit 6

To reboot using the systemd, use the systemctl command.

# systemctl isolate reboot. target

Simply type reboot into the command prompt to reboot.

# reboot

The format of the shutdown command is as follows.

shutdown [options] time [message]

The -r option instructs shutdown to do a reboot. Next, you can specify the time to shutdown using the “HH: MM” format. You can also use +N, where N represents the number of minutes to wait before acting. Finally, you can use the new keyword to start immediately. Optionally, you may specify a message broadcast to all users logged into the system.

# shutdown -r now

**Powering Off a System**

To power off a system, use runlevel 0, the poweroff target, or the poweroff command.

Here is how to issue a power-off with init.

# telinit 0

Here is how to power off a system with systemctl.

# systemctl isolate poweroff.target

Finally, you can use the poweroff command.

# poweroff

**Summary**

The BIOS’s job is to perform basic hardware checks and launch the boot loader from a bootable device, as you learned. You also learned about the two most commonly used bootloaders, LILO and Grub. The primary job of any boot loader is to start the operating system.

You also learned that the /boot directory contains the files required to boot a Linux system. The initial ramdisk, often known as initrd, is a memory-based file system. Its primary function is to mount the file system that contains the operating system. The Linux kernel is commonly referred to as vmlinux or, if compressed, vmlinuz.

Using the dmesg program or looking at the /var/log/dmesg file, you learned how to inspect the messages in the kernel ring buffer.

You also learned about run levels and how systemd has an equivalent concept known as targets. Next, you learned how to change the runlevel with the telinit command for the traditional init system and the systemctl management for systems that use the system. Finally, you learned about the shutdown, reboot, and poweroff commands.

**Quiz**

**1\. The BIOS begins the computer’s boot process and passes control to the boot loader.**

a.True

b.False

**2\. Which of the following are Linux boot loaders?**

a.LILO

b.GRUB

c.Both LILO and GRUB

d.BIOS

**3\. The following is a temporary file system loaded into memory when the system boots.**

a.kernel

b.vmlinux

c.vmlinuz

d.initrd

**4\. The /Linux directory contains the files required to boot Linux.**

a.True

b.False

**5\. Which command displays the contents of the kernel ring buffer?**

a.ringbuf

b.ringb

c.rmesg

d.dmesg

**Quiz Answers**

1.  A
2.  C
3.  D
4.  B
5.  D

**Searching and Extracting Data**

Objectives:

*   Understand how to redirect output using pipes
*   Be able to redirect operators using grep
*   Be able to search for patterns within data files

A command-line environment is a potent tool. This same concept can also search for data within a file or files.

But first, you must understand how to link multiple commands together using the images of command redirect and input/output redirection.

**Command Redirection**

Command redirection allows a user to reroute the standard input to a second program or command. This is performed using a pipeline or command line pipe. A pipe is created using a vertical bar (|) between the two commands. This key is usually found above the Enter key on the keyboard and accessed by pressing the Shift key down while pressing the Backslash key.

Pipelines can be helpful when applied in various ways. For example, the verbose output of the cat command (which displays the contents of a file to the screen) can be piped together with the less command to show only one page of content at a time. This avoids jumping to the last page of the file and not seeing the content in the rest of the file. The more command can also display one page of content when combined with the cat, but it operates differently than the less command. Please consult their dedicated man pages to learn more about a cat, trimmer, and more commands.

By using pipes, a user can perform two or more commands in sequence and run them consecutively. This allows for quick execution of commands and complex tasks, resulting in fewer pauses in performance since the system won’t have to wait for the user to input the following command.

The grep command is commonly used in pipelines to search for keywords within the output of a given command. This command searches for files containing a specified string and returns the file’s name, and if it is a text file, the line containing that string. The grep command can also search within a specified file for a specific string. To use grep, a user simply types the command’s name, grep, an optional set of switches and parameters, a regular expression, and an optional filename if desired.

If you plan to enter the world of system administration or cybersecurity, you will need to get comfortable using the grep command. This command is a security operation center analyst’s best friend for finding information from different log files in a Security Information and Event Management server. In-depth usage of the grep tool is beyond the scope of this book, but to learn more about the command, please consult its detailed man pages for the complete list of options it supports.

**Input/Output Redirection**

In addition to redirecting the output of one command into another by using the pipe, a user can also turn the input/output of a command to other locations. For example, if you need to save a program’s output for future reference, you can redirect that output to a file. Similarly, the input to a command can be shifted from a file instead of requiring the user to enter it using the keyboard.

Although input redirection may sound strange, some programs rely on this feature to process data. For instance, raw text files fed through a program search the text for specified patterns. In addition to all of this, a related technique involves the xargs command, which enables a user to generate command-line options from files or other programs’ output.

A Linux system has two types of output supported by default: standard output and standard error. The expected output is used for average program messages. For example, when you run the ls command, the output is sent to the standard output and, therefore, displayed on your screen. The standard error, on the other hand, outputs error messages. This also displays on the screen by default, but users can redirect these messages if desired.

Several redirection operators are available to more fully control where information is output to, displayed to, and saved to.

> creates a new file containing the standard output. If the specified file already exists, it will be overwritten. For example, if the command “ls > contents.txt” is executed, the output of the ls command will be saved to the contents.txt file and nothing would be displayed on the screen.

>> appends the standard output to an existing file. Just like the command above, we could redirect the output of the ls command to the file contents.txt, but instead of overwriting the file, we would simply add our output to the end of the current file.

2> creates a new file that will have the standard error redirected to the file. If the file already exists, its contents will be overwritten.

2>> appends the standard error to an existing file. If the file doesn’t exist, a new one is created. If it does exist, the standard error output will simply be added to the end of the file.

&> creates a new file that contains both the standard output and standard error output. If the file already exists, its contents will be overwritten.

There are also several redirection operators available to more fully control where information is input from in the shell.

< sends the contents of the specified file to the command in place of the standard input. For example, if I had a text file called input.txt that contained a single line of text that said b??l and entered the command “ls < input.txt”, the output would be equivalent to entering ls b??l at the command prompt.

<< enters a sort of interactive mode, where the following lines entered will be redirected to standard input. This will allow you to enter new information and redirect it to the same command, one line at a time.

<> specifies that a file will be used for both the standard input and standard output.

Now, while some of these, like the <> option, may seem like something you would never use, remember that Linux treats every device as a file that is mounted somewhere within its filesystem. So, an option like <> may be useful when reading or writing to an external hard disk, sending or receiving data to/from a sound card, or other such cases.

As a normal user, you likely won’t use <> very often, but if you go on to become a Linux developer, then it may become more useful to you at that time.

Let’s put these concepts into practice using the grep command. For example, if a system administrator on the root account wanted to search for data about a particular user (Jason) within every configuration file in the /etc directory, they may do so quite simply by typing “grep Jason /etc/*”. Running the command without redirection, though, the output of the grep search would simply be displayed to the screen and not stored for future reference. Also, since our system administrator was executing the command as the root user, grep is likely to return a long series of outputs to the screen, making it long and difficult to read.

Therefore, the system administrator should instead employ redirection. To accomplish this, the system administrator should use a redirection operator and specify the filename where the data will be redirected into and stored. For example, entering “grep Jason /etc/* > Jason.txt” would send the output of the grep search to the Jason.txt file in the present working directory.

Another reason for using redirection is to change where the standard error is sent. For example, if the system administrator entered “grep Jason /etc/*” as a normal user instead of as a root user, the files that contain the username will appear on the screen, but so will a lot of error messages. This is because a normal user lacks permission to read many of the files within the /etc directory. By default, the standard errors are also routed to the standard output (the screen).

To remove all the errors so the system administrator won’t have to see them cluttering up the screen, they can be redirected to a special device that exists on every Linux system, known as /dev/null. This null device is essentially an area where we can send garbage for the operating system to delete.

So, if the system administrator enters the command “grep Jason /etc/* 2> /dev/null”, then the grep command will search for the name Jason in every configuration file in the /etc folder, and redirect all of the errors messages to /dev/null so they are never displayed on the screen and are simply discarded.

**Regular Expressions**

While entering a search term like a username is useful, the real power of grep comes from combining it with regular expressions, also known as REGEX. Regular expressions are a way to describe patterns that a user might want to look for within a given data file or files. Many Linux programs allow for regular expressions, and this provides the user with the tools for expressing patterns within text. Similar in principle to wildcards, regular expressions can specify multiple filenames or other text-based content.

Regular expressions are divided into two types: basic and extended. Which regular expression form is assumed will depend upon the program that is being executed. Some programs accept just one expression form, while others can use both types.

The simplest type of REGEX is an alphabetic or alphanumeric string, such as HWaddr or Linux. These regular expressions match any string of the same size or longer that contains the regular expression. For instance, the HWaddr regular expression matches the following three phrases that might appear within a file being searched: “Hwaddr,” “This is the Hwaddr,” and “The HWaddr is unknown.” But it’s when a user inserts special characters that can signify patterns that regular expressions really shine.

Bracket expressions are commonly used when conducting searches in grep using REGEX. A bracket expression uses the square bracket characters ([ ]) to constitute a wildcard search that selects any one of the characters within the bracket. For example, the regular expression of b[aeiou]g represents five words: bag, beg, beg, bog, and bug.

A range expression also uses the square brackets, but, instead of listing every character within the brackets, it relies on using the starting and ending points of the range separated by a dash (–). Generally, using a range expression is easier than a normal bracket expression when searching for larger sets of data. Ranges can also be applied to alphabetic characters, like [g–t], which would represent all the letters g, h, i, j, k, l, m, n, o, p, q, r, s, and t. Remember that since Linux is case sensitive, the ranges [a–z] and [A–Z] are considered two different sets of ranges.

The single dot (.) is a wildcard that represents any single character except for the newline character, which is used when the return or Enter key is pressed on a keyboard. For example, if the user entered b.g, that would represent bAg, bag, bBg, bbG, b2g, and so on, where any letter, number, or character could be inserted between the b and g since the single dot can represent any character.

**Using Network to Transfer Files**

This might not be as hard as you might imagine. All it takes is a bit of practice and a little eye out for details.

We have established an understanding of what a network is and how to identify machines that are connected to the said network. We use their IP addresses unless they have specific domain names, in which case, we will use those instead. Now we wish to start moving data back and forth. We have quite a lot of files that need to be transferred and quite a few that we require from the remote servers or locations.

We start things off by learning a simple command that allows us to copy a file from our local system to a remote system.

If you recall, just moments ago, we mentioned you need to keep an eye out for details. See the colon (:) in the end? That is not a typographical error. That is done on purpose. If you do the command correctly, you will see a confirmation for that.

This is one of the most basic commands used in the world of Linux. While there are quite a few commands out there, which we will mention here for reference purposes, the “SCP” is rather easy to use and understand. Now let us try that the other way around.

Now, we used the same command but changed the order. Let us try to see what happened here by first understanding the syntax of this command.

scp source_file destination_file

As we see here, the source file this time was in the remote computer/server. We wanted a file named sample4 to be copied securely into our system (destination file). After the colon, we specified the file we wanted and then used a period (.), which indicated a local machine — i.e., your machine. After you press Enter, you will have that file copied in your system.

This will effectively rename the file to sample5 and place it within the local “test” directory. You can specify a path, and the rest will be done for you.

To get a full spectrum of the SCP command, have a look at the manual by using the man command.

This command is good if you have a few files, but what if you wish to transfer a whole bunch of files or maybe the complete directory? For that, we use another command called the “sync” command.

This command has multiple uses and can be used to move or copy (mirror) data and files across a single machine or the entire network. The command is terrific for backing up your data on remote machines or servers. To use the command, you need to follow the syntax below:

rsync [options] source destination

With over 50 options, you can easily and securely copy the entire directories or the content of the said directory across a single machine or the network itself. You might be asked for administrative permission to do that as this uses SSH to secure the entire connection and prevents anyone from “listening.” That is just another word to suggest someone is monitoring your activities.

There are far too many tools and applications that have come forth in recent times. Whether you decide to use the LUI as a medium of data transfer or GUI, you have your options with you. Be sure that you always use reliable sources and monitor activities and connections regularly to ensure safety for your data and for the network itself.

**Network Applications**

There are quite a few commands and diagnostic tools that can help you out on your journey as a network specialist or even as a secure home user. Knowing these is essential and can protect you from quite a lot of suspicious connections and hackers. These tools will also allow you to indulge deeper and create a better understanding of how the network operates and how other devices act when they are a part of the network. For now, let us proceed in getting ourselves acquainted with some important tools.

Let us clear the terminal by using the clear command and use an important command you should know as a part of your basic learning. It is called the “ifconfig.”

Windows users who may have used a command on their command prompt called “ipconfig” would find this familiar.

Go ahead and type in “ifconfig.” You will now be presented with quite a populated screen, full of information. This is your network information and shows exactly how the network is configured.

Note: For users who may face errors, you might need to install net-tools. The command for that is “sudo apt install net-tools.”

The information that you see here would allow you to take a closer look into what some of your network settings are. These will include your ethernet settings, your wireless settings, and information about your local host as well. Some of these are quite useful pieces of information and can come in handy should the situation call for it.

Most of the information displayed is easy to understand, but if you find any of the terms or columns hard to read, you can always rely on the trusty old Ubuntu community to acquire further insights.

Next stop, we will be looking at the command called the “tcpdump.” This is basically a packet sniffer—literally! It analyzes all the packets that come in or go out of your system. Why do we need this? We will learn that soon enough.

For us to have this, go ahead and install “tcpdump” by typing in the following command:

sudo apt-get install tcpdump

Once installed, go ahead and run the tool by typing this (requires sudo):

sudo tcpdump

Don’t be alarmed if you are not getting anything as of yet. Just open a browser window and go to any website of your choice. As soon as you press Enter on the browser, switch your window and come back to the terminal. Your terminal screen will now start an endless process of sniffing all the packets that are leaving or entering your system. You will need to bring this to a halt by pressing

Ctrl+C.

The problem with this command is that it never ends if you have a few network-based activities running in the background. What you can do, however, is to limit the data sniffing. Suppose you only want to capture a set number of packets (let’s say 20), you can slightly change the command to do exactly that.

sudo tcpdump -c 20

The command will execute the moment you hit Enter and will capture the next 20 packets sent out or received. We use the “tcpdump” command to find out where these packets are being sent to and where they are being received. In our example, you will notice that an outgoing packet will have your IP address, the domain, and the address, while the opposite will show accordingly.

This command is essential to analyze data and can track down any unknown addresses where information might be leaking to or coming from. Such suspicious addresses or domains can then be clocked accordingly to ensure the safety of the system and the network itself. The command also allows you to see the packets that are being sent out and received by a specific interface that is connected to your network.

Suppose you have a wireless router on your network and you wish to check the kind of activity that is taking place through it. You can do that simply by typing in the following command.

sudo tcpdump -c (number of packets) -i (device name)

This will start collecting results for the said device and capture the number of packets you have set—quite a sneaky way to check on what your co-workers or colleagues are doing.

Similarly, you can also use the same command to check up on your ports or have the packets shown in ASCII format or even hex format. The application for this tool is vast. You can always check the manual of this tool by typing in “man tcpdump” to get the complete options you have available with this command.

Before we go ahead and get into the basics of moving files and folders across the network, there is one more command you might find useful to determine who is connected to your network. It is called the “netstat” command, and it can provide you with a great helping hand to find out if someone is hidden yet connected to your network. To do this, type in the command in your terminal with the following option:

netstat -nr

Instead of showing domains, you will now be provided with the IP addresses and the IP routing table. You can also check the network interface statistics by using the command below:

netstat -i

This now shows us the usage of all of the devices. You can find out how many packets are being sent out or being received by individual devices.

Lastly, you can find out what active sockets are being used currently by your network, and to do that, you need to use another netstat command with a -ta option. This will list out active sockets with their address (local and foreign), their state, and some other useful information. This kind of information can be vital for anyone who is looking after the security of the entire network.

The netstat command is used to monitor the active connections with your network and helps you in blocking any unwanted or suspicious connections that may provide an entry for hackers and malware. You can also keep track of every packet that is delivered and received. This command is always a go-to command for most of the network and system administrators.

While your network is engaged and connected to various devices, all trying to access it and acquire or provide information, something needs to step in to keep an eye on the security here. This is where the Secure Shell (SSH) comes into play.

Before SSH came along, there was Telnet. This was initially seen as a revolution where a person could access another remote machine without being there physically. This caught the attention of all kinds of people, including some prying eyes too. Soon enough, people realized that these methods were not secure and anyone could practically “eavesdrop” on their exchange.

The SSH does what Telnet failed to do so; it encrypts all of your data of the session. It also allows clients of any operating system a secure way to transfer their files and folders without worrying about prying eyes in the middle. Understanding SSH is not a day’s job or even that of a book. Individuals interested in learning more about encryption, SSH, and SSHD can find a variety of information online. These are on an advanced level and hence would not suit the beginners at this point.

It takes time and practice to get the hang of things in the world of Linux, but once you start to understand how things work, you will soon be surfing over issues as if they mean nothing. It’s probably better to get used to the concept that the LUI is your best buddy in this situation.

**Scripting**

An exceptional ability of a computer is that it can do automated tasks for you. In a Linux system, you can control the function by writing a “program” according to your preferred automated activities.

This is where scripts enter the picture.

**What Is Scripting for?**

A script is a collection of data and commands that are stored in files. A shell is in charge of reading the collection, and as it reads data, it follows the instructions.

Scripts can handle basic tasks, as well as complicated ones. They can be used to perform powerful executions.

Scripting has many common uses including:

*   Retrieves updates
*   Maintains repositories of vital updates
*   Gathers up to thousands of files and transmits them to web

servers

*   Copy up to thousands of files to web servers
*   Builds a hierarchy of pages

**Writing and Editing a Script**

A script contains ASCII texts. Writing a script is done via a text editor. To write a functional script, you should remember that it has to contain three lines.

Sample:

#! python

# first ever script

echo “Hello World!”

As the sample shows, the script has three lines: (1) the first line contains “#! python”; it is an important line that indicates the program needed for the script’s interpretation (i.e., python), (2) the second line contains “# first ever script”; it is the preferred title for a script, and (3) the third line contains “echo “Hello World!”; it is the script.

After writing the script, the need to set permission follows. It enables the script’s execution. It can be done via the “chmod” command.

Sample:

chmod 700 first_ever_script

As the sample shows, “chmod” is used; chmod is the command in charge of granting permissions to files and directories. “700” is also used; it is a read and write permission to execute.

Editing a script is permitted. Let us say that instead of “700” (a private read and write permission), you prefer “755” (a public read and write permission). To do so, learn about two commands: (1) aliases and (2) shell functions.

Aliases are commands that can create sub-commands.

Sample:

alias tomorrow = ‘current date + “%A, %B, %Y”’

As the sample shows, the created alias is “tomorrow”. It is tasked to display tomorrow’s date with the provided information.

The other command for script editing is called shell functions. Shell functions are like aliases. The difference is in the complexity of execution. Aliases are for simple commands. Shell functions can handle instruction sets that are more complicated.

Shell functions are also called little sub-scripts. Due to their nature of managing scripts that can sometimes be difficult to comprehend, they are considered scripts within scripts.

Sample:

function tomorrow {

echo “Tomorrow’s date is:”

current date +”%A, %B %Y”

}

As the sample shows, the shell function is designed to display tomorrow’s date. It uses data from the current date. It is similar to the provided sample of an alias method. The difference is that it can display a custom statement (“Tomorrow’s date is:”), on top of the necessary data.

**Learning and Understanding Bash**

BASH, short for Bourne-again Shell is a command processor that reads scripts. It operates in a text window. There, the user inputs commands that cause particular actions.

BASH supports glob. Glob are patterns that specify a set of filenames. These filenames feature wildcard characters.

Some wildcard characters are:

*   ? – for matching a single character
*   – for matching none or several characters
*   [abc] – for matching one character that is present in a given

bracket

*   [!abc] – for matching one character that is absent in a given

bracket

*   [a – z] – for matching one character that is present in the ran

ge of a given bracket

*   [!a – z] – for matching one character that is absent in the ran

ge of a given bracket

When BASH is set in concurrent mode, the execution of two commands is allowed. For these commands to be executed properly, they have to be presented with the use of an ampersand (“&”).

Sample:

first command & second command

As the sample shows, the “first command” is executed. Once the execution is finished, the “second command” is processed.

Rules of BASH:

*   With the use of the ampersand, one command can be executed

in the “big” or background

*   Usually, a command’s execution is done in “fg” or foreground
*   A running process is subject to the system administrator’s

suspension by pressing “ctrl” + “z”

*   A background process might be suspended in favor of a run

ning process

Moreover, there exists a command called BASHBUG. Once it is invoked, the default text editor is launched. It comes with a form that a user can fill in. Once completed, the form is mailed to BASH maintainers.

**Substitutions, Variables, and Constants**

Substitutions are allowed in Linux programming. It is done for the modification of a file in favor of a preferred command.

Sample #1:

# create_page ! – A script for production of an HTML file

concatenate <<- _EOF_

<HTML>

<HEAD>

<TITLE>

User_System_Info

</TITLE>

</HEAD>

<BODY>

<H1>User_System_Info</H1>

</BODY>

</HTML>

_EOF_

Sample # 2:

# create_page ! – A script for production of an HTML file

title=”User_System_Info”

concatenate <<- _EOF_

<HTML>

<HEAD>

<TITLE>

System_Info_1

</TITLE>

</HEAD>

<BODY>

<H1>System_Info_1</H1>

</BODY>

</HTML>

_EOF_

As sample # 2 shows, the title of the HTML file in sample # 1, “User System Info”, was changed to “System Info 1”.

One of the commonly used concepts in substitutions is variables. Variables are one of the fundamentals in programming. They are elements that can store data, and they are referred to by a particular name.

Reminders when creating a variable name:

*   A variable’s name should start with a letter.
*   Punctuation marks are not allowed
*   Refrain from perusing embedded spaces; use underscores

Some variables are ready to use. They are already pre-defined in scripts every time a system administrator logs in. These variables in uppercase letters are called environment variables.

Sample:

# create_page ! – A script for production of an HTML file

title= “System_Information”

concatenate <<- _EOF_

<HTML>

<HEAD>

<TITLE>

“System_Information” $HOSTNAME

</TITLE>

</HEAD>

<BODY>

<H1> System_Information $HOSTNAME</H1>

</BODY>

</HTML>

_EOF_

Although substitutions are allowed in Linux, remember that some values should not be changed. Otherwise, the script will be non-functional. These values are referred to as constants.

Sample:

# create_page ! – A script for production of an HTML file

TITLE=”System Information for $HOSTNAME”

RIGHT_NOW=$(date +”%x %r %Z”)

TIME_STAMP=”Updated on $RIGHT_NOW by $USER”

cat <<- _EOF_

<HTML>

<HEAD>

<TITLE>

$TITLE

</TITLE>

</HEAD>

<BODY>

<H1>$TITLE</H1>

<P>$TIME_STAMP

</BODY>

</HTML>

_EOF_

**What Is the Use of Quoting?**

A factor that leads to a script’s successful execution is quoting. It is a technique of grouping data to avoid instances of misinterpretation. Usually, quoting’s primary objective is controlling substitutions.

Sample # 1:

TITLE=“My system info for $HOSTNAME”

CURRENT_DATE=$(current date “+%x %r %Z”)

TIME_STAMP=Last updated on “$CURRENT_DATE by $USER”

Sample # 2:

TITLE=My system info for $HOSTNAME

CURRENT_DATE=$(current date +%x %r %Z)

TIME_STAMP=Last updated on $CURRENT_DATE by $USER

As sample #1 shows, quotes surround particular groups of texts. If quotes were not used, as shown in sample #2, the script might interpret words as additional commands.

# Ubuntu Installation

On April 23, 2020, Ubuntu 20.04 (codenamed Focal Fossa) was launched. It’s a Long-Term Maintenance (LTS) version, which means support and updates will be provided until April 2025.

This tutorial will show you how to install Ubuntu 20.04 LTS on your computer.

**Ubuntu 20.04 LTS.**

*   Linux Kernel 5.4 — This Linux kernel version includes support

for a larger variety of CPUs. It also contains boot speed, power-sa

ving, and USB-C enhancements, as well as various security mea

sures.

*   Gnome 3.36 — The Gnome desktop environment has been

upgraded and enhanced. System animations should be smoother

and consume less CPU power.

*   Improved speed and native encryption in the ZFS 0.8.3 file

system.

*   Theme: gloomy

*   The login screen has been updated.

*   Python 3.8, OpenJDK 11, PHP 7.4, Glibc 2.31, Rustc 1.41, GCC

9.3, Ruby 2.7.0, Perl 5.30, Golang 1.13 are newer versions of

major programming languages.

**Installation prerequisites for Ubuntu 20.04LTS**

*   For storage, there is a total of 25GB accessible on the hard drive.

*   Memory: 4 GB

*   A dual-core CPU with a clock speed of 2 GHz

*   USB compatibility

Also, a 4GB USB flash drive is required to create the Ubuntu installation disc.

**Step 1: Save the installation media to your computer.**

1\. Open a web browser and go to the Ubuntu download page. Select the Ubuntu version that is appropriate for your machine. The following are the most common versions:

*   Ubuntu Desktop (Ubuntu)

*   Linux Servers (Ubuntu)

*   Derivatives of Ubuntu

![Image](Images/image00111.jpeg)

2\. When you’ve found the version you’re looking for, click the green Download button to get it. Your download should begin after you’ve been directed to a thank-you page. (For desktops, we’ll download and install Ubuntu 20.04.)

.iso file is available for download. It allows you to make a bootable USB device.

3\. Save the file to your preferred location.

Note: You may immediately mount the .iso image if you’re installing to a virtual computer (like VirtualBox).

**Step 2: Make a bootable USB drive**

You’ll need a USB disk with at least 4GB of storage. The data on the USB device will be erased as a result of this procedure. Ensure that any existing data on the USB device is backed up.

Option 1: Use Ubuntu to create a bootable USB drive.

Use the utility to create a startup disk:

*   Create a search dialog and put “create startup” into it.

*   If it isn’t already installed, the Software Center will prompt

you to do so – choose USB drive from the drop-down menu, then

start the utility.

*   Click Other in the top pane, then navigate to and pick the Ubuntu 20.04.iso file you downloaded.

*   Select your USB disk in the bottom pane.

*   Make a startup disk by clicking Make startup disk.

Option 2: Use Windows to create a bootable USB drive

To make a USB bootable drive, you’ll need to install Rufus, a third-party application.

1.Rufus is a program that may be downloaded. To get the current version of Rufus, scroll down to the download section and click the link.

![Image](Images/image00112.jpeg)

2\. Once the file has been downloaded, run it.

3\. A dialog box appears. If you wish to check for online updates, you’ll be asked. Select No.

![Image](Images/image00113.jpeg)

4\. The Rufus application starts. When you plug in the USB drive, it should appear in the device field.

*   Set the USB drive as the device to which you want to write.

*   Select Disk or ISO Image from the Boot Selection drop-down

menu.

*   Toggle the right-hand Select button.

*   Select the.iso Ubuntu file you obtained earlier in the process.

![Image](Images/image00114.jpeg)

5\. Press the Start button.

**Step 3: Install Ubuntu from a USB drive.**

4.Shut off your computer. Remove any additional USB devices, such as printers, memory cards, and so on.

2\. Turn on your computer and insert the Ubuntu USB drive into it.

There are two situations that might happen:

*   The USB disk is immediately booted by the computer.

*   In the Boot Menu, you must manually setup USB booting or

BIOS/UEFI.

3\. As soon as the computer turns on, hit the boot menu key roughly once or twice per second to manually adjust the boot sequence.

Depending on the manufacturer of your computer, the boot menu key may be different. The following is a list of frequent boot keys for each brand:

![Image](Images/image00115.gif)

4\. Select the Ubuntu media to boot from using the arrows after you’ve seen your boot menu. The name of the entry for a DVD is generally DVD or Optical. USB is commonly referred to as USB.

The Ubuntu live disc menu should begin to load on your PC.

Note: If you’re having trouble starting the USB from the boot menu, try booting it via BIOS/UEFI instead.

**Step 4: Install Ubuntu**

You may try out Ubuntu 20.04 before deciding to install it. A live mode is included in the .iso that only runs in memory.

Click Try Ubuntu to start this mode.

![Image](Images/image00116.jpeg)

**Step 5: Install Ubuntu 20.04 LTS Desktop**

Click Install Ubuntu to begin the installation process.

![Image](Images/image00117.jpeg)

**Select a Keyboard Layout**

The system will choose English and English by default.

You can choose a non-standard keyboard from the list if you have one. Alternatively, select Detect Keyboard Layout to have the system choose your keyboard for you. Use the to test your keyboard if you need to labeled field.

Click Continue when you’re ready.

![Image](Images/image00118.jpeg)

Select Applications to Begin With

*   Normal Installation — This gives you the whole Ubuntu

Desktop experience, including office applications, games, and

media players.

*   Minimal Installation — Select this option to preserve space on

your hard drive, especially if you won’t be utilizing media players

or office apps.

You’ll be prompted to confirm the following selections as well:

*   While installing Ubuntu, download updates — This automates the process of downloading huge package files. The packages will be available to apply as updates after the installation is complete.

*   Install third-party graphics and Wi-Fi hardware software, as well as new media formats –Some hardware, like as graphics cards and wireless devices, does not support open-source drivers. Furthermore, some media formats, such as.wmv, are not covered under the GPL. If you want assistance with them, you will be required to agree to extra terms of service.

![Image](Images/image00119.jpeg)

**Partitioning a Hard Drive**

After that, you’ll get a dialog box asking you to choose an installation type. By selecting Erase disk and install Ubuntu, you may wipe the hard drive clean before installing Ubuntu. If you choose this option, skip to the next stage.

Advanced users may choose to make changes to Advanced Features. Set your own disk partitions or other additional parameters using this command:

With the fresh Ubuntu installation, use LVM:

*   Logical Volume Management (LVM) is an acronym for Logical

Volume Management. This is a program that allows you to mana

ge many virtual disks on your computer in real time. It’s similar to

a more advanced version of the gparted utility.

*   To make the new Ubuntu installation more secure, encrypt it:

This will encrypt the contents of the disk. You’ll need to pick a

security key in order to decrypt and utilize the disk.

*   Experiment with erasing the drive and replacing it with ZFS:

ZFS stands for Zettabyte File System, but it has evolved into a

hybrid file system and volume manager. Avoid using this option

on mission-critical production systems while it is still being te

sted.

Click Something Else if you’d prefer make your own hard drive partitions. You can design your own partition table and logical disks on the following screen. This allows you to split a physical hard disk into many partitions. Partitions are treated as separate disks by the operating system.

Note: that some users build a second disk for their /home directory. The partition containing the /home directory remains unaffected if the operating system has to be reinstalled.

To apply your modifications to the disk partitions, click Continue.

You’ll be prompted to make disk changes? Until you click Continue on this screen, none of the selections you’ve chosen are permanent. To continue, click Continue.

**Choose a time zone**

The installation will ask, “Where are you?” once the machine has formatted the disk partitions.

Fill in the name of the nearest big city, and the system will calculate your local time zone.

Click Continue.

**Make a User Account**

After that, you’ll need to create a user account. Please complete the following fields:

*   Name: Your given name.

*   Hostname or network name: This is the name of the computer.

*   Username: The name of the user account you wish to utilize.

*   Enter and confirm a strong password; the installer will evalua

te your password strength automatically.

*   Automatically log in: This is not a good idea for servers that

are open to the public.

*   To log in, you’ll need my password: This is suggested for ser

vers that are open to the public.

To install Ubuntu, click Continue.

Remove the Ubuntu installation disc after the installer is finished. You’ll be asked to restart right away

![Image](Images/image00120.jpeg)

The machine should now boot into Ubuntu 20.04, which you just installed.

Conclusion

You should now have Ubuntu 20.04 installed successfully on your machine.

**Fixing Grub**

You probably don’t want Ubuntu to appear multiple times on the boot list if you are like me. You may want the Windows option to come first, especially if other family members use the computer and are used to using Windows.

Open a terminal window by opening the Dash and typing “Term.” Then, click on the terminal icon.

Type the following into the terminal window:

sudo gedit /etc/default/grub

# If you change this file, run ‘update-grub’ afterward to update

# /boot/grub/grub.cfg.

# for full documentation of the options in this file, see:

# info -f grub -n ‘Simple configuration’

GRUB_DEFAULT=”2”

#GRUB_HIDDEN_TIMEOUT=”0”

GRUB_HIDDEN_TIMEOUT_QUIET=”true”

GRUB_TIMEOUT=”10”

GRUB_DISTRIBUTOR=”`lsb_release -i -s 2> /dev/null || echo

Debian`”

GRUB_CMDLINE_LINUX_DEFAULT=”quiet splash”

GRUB_CMDLINE_LINUX=””

If you want Windows to be the default option, you can either edit the grub.cfg file (there is a comment in the file saying not to do this) or you can change the default to point to the Windows option first.

While editing the /etc/default/grub file won’t put Windows at the top of the list, it will make it the highlighted option when you start the computer.

To do this, change GRUB-DEFAULT to be the position in the Windows list when you start the computer.

On my computer Ubuntu is first, Ubuntu Advanced Options is next, and Windows is third.

Note that the numbering starts from position 0 so Ubuntu is 0, Ubuntu Advanced is 1, and Windows is 2.

Save the file when you have changed the default and run the following command:

sudo update-grub.

The Grub file will be updated and if you reboot, Windows will be selected automatically.

Regarding the extra Ubuntu entries, there are multiple entries because you will have more than one Linux kernel installed.

You can either edit the grub.cfg file directly to remove the extra entry (not recommended) or you can remove the additional kernels by running Synaptic and looking for older installed version numbers.

I would leave the duplicate entries there and just not select them.

**A Quick Tour of Ubuntu**

This quick tour is aimed at anyone who has never seen Ubuntu before and highlights the look and feel, the applications, and the functionality that comes as standard.

Ubuntu comes with the Unity desktop which has been part of Ubuntu since version 11.04\. The Unity desktop has matured and now provides a great user experience.

If you are a Windows user, the initial look and feel will be unfamiliar to you, but after a few weeks, you will appreciate the way Ubuntu and the Unity desktop work.

The first thing to note is the bar at the top of the screen.

The bar acts as a menu bar for any application that is loaded and this saves screen real estate leaving more room for the application itself.

Also on the bar is a series of icons giving access to the most common system settings such as adjusting your power management, connecting to the internet, toggling Bluetooth on and off, and adjusting audio settings. There is also a clock and a power button.

The left side of the screen is taken up by a launch bar which contains a list of icons for the most commonly used applications.

The launch bar makes it possible to get to your favorite applications with one mouse click.

Any application that you open appears at the bottom of the launch bar and if you connect an external device such as a USB drive or a portable hard drive, this will also appear.

Navigating Ubuntu is quick and easy. There are no fiddly menu systems to navigate and there is no tile insight. Navigate then click the Ubuntu icon at the top of the launch bar, but the easiest way to navigate is to press the super key (Windows icon) on your keyboard.

The screen that appears is called the Dash and from here you can accomplish any task with a minimum of mouse clicks and/or keystrokes.

To find an application, you can simply start typing in the search bar. More often than not this is effective enough to find what you need without further interaction.

The lenses provide applications, files and folders, music, photos, and videos.

As well as files and applications on your computer, the Dash also displays suggestions of applications that you might like to purchase. Some people deem this a bad thing, but there is an option to turn it off.

The videos lens enables you to filter your search so that you can search locally on your computer or via services such as the BBC and YouTube.

The music lens enables you to filter your music by sub-genres and age.

Ubuntu comes with an impressive set of applications installed by default. For example, LibreOffice is the default office suite and provides most of the functionality that you would get from Microsoft’s equivalent office suite.

For browsing the internet, Firefox is installed as standard and the Thunderbird email client provides many of the features of Microsoft Outlook. Other applications include instant messaging, a BitTorrent client, and remote desktop software. Ubuntu also comes with games, graphics applications, and an audio player (Rhythmbox) for playing your music.

Adding new applications is easy. Simply run the Ubuntu Software Center and search for the type or name of the application you want to install and a list of possible applications will appear.

The Ubuntu Software Center provides a list of free and non-free applications.

Hardware support in Ubuntu is excellent.

My all-in-one printer and scanner was easier to install in Ubuntu than it was on Windows. While using Windows, the printer required a driver CD that ran through a series of options and all in all it took about 10 minutes to install. On my laptop running Ubuntu I simply ran the add printer wizard and the setup took less than one minute.

I have a Sony Walkman for listening to music and this integrates seamlessly into Rhythmbox, which means I can synchronize my music between my laptop and MP3 player.

My external hard drive is picked up as soon as I plug it in and I have a series of USB pen drives that all work simply by plugging them in. My digital camera was also a breeze to set up.

Ubuntu provides a service called Ubuntu One, which you can use to backup all your important files and photos. The service is free (up to 5 GB) and all you have to do is fill in a form with your name, email address, and a password to use for Ubuntu One. Once your account has been created, you can choose the folders you wish to backup and synchronize between your computer and Ubuntu One.

If you wish to buy more music, then Ubuntu has its own music service called “Ubuntu One Music.” This is the Ubuntu equivalent of iTunes and the catalog and pricing are comparable to other similar services.

# Begin with Ubuntu

Now that you have installed Ubuntu, it is time to start using your Linux operating system. Unlike the paid operating systems such as Windows or macOS that require you to pay more to get additional software, Ubuntu already comes loaded with the software you need to get started. You will find everything in Ubuntu right from an office suite, a web browser, to email media tools. You are good to start using Ubuntu as soon as the installation is completed.

Everyone uses a computer in their unique way, and every user likes to customize the look and feel of their computer to their requirements. Keeping this in mind, Linux lets you use one of the many graphical interfaces that it has to offer. Thus, there are hundreds of graphical interfaces available on Linux to suit every user’s needs.

Although there are multiple graphical interfaces available for Linux, two of them are the most popular ones, GNOME and KDE. Each of these environments has a user-friendly and easy-to-use interface. They have a few differences concerning the look of the desktop and how they can be personalized further.

The KDE environment gives a user complete control and configuration options to personalize the desktop. The user can configure every aspect of the desktop and has the liberty to modify the desktop’s look and feel.

GNOME, on the other hand, is inspired by the desktops of Windows and macOS and prioritizes simplicity. GNOME can be customized easily too, but it hides certain options from the user.

Ubuntu users can choose either of these two desktop environments along with some more desktop environments as well.

The default desktop environment in Ubuntu 20.04 is GNOME 3.36, but this does not mean that you cannot install other desktop environments. Let us see what it has to offer to its users.

**Theme**

Ubuntu 20.04 LTS comes with a revamped Yaru theme, and you can see it right from the boot up to the desktop. Developers of operating systems like to have a distinctive look for their operating system, which helps establish their brand’s image. In January 2020, Canonical, the parent company of Ubuntu, had a design sprint in collaboration with the Yaru team and the Ubuntu design team. Yaru was introduced in Ubuntu 18.10.

![Image](Images/image00121.jpeg)

Yaru has three types of variations, and it also has a sound theme. During the design sprint, the designers and developers also identified some UI improvements that could benefit the desktop. You can switch your desktop theme between Light, Standard, and Dark colors using the Appearance settings. You can also use the default sound alert that Yaru provides.

![Image](Images/image00122.jpeg)

The revamped Yaru theme also lets you make changes to the boot splash screen and the installer windows. The Yaru team has now implemented the spinner that was available only on the desktop to appear even on the boot screen. If you have installed the system using the full-disk encryption option, then the boxes for the passphrase in the boot menu will match the desktop theme too.

Ubuntu has received a new animal mascot with each major release lately. This time too, a neatly designed creature has been integrated for the release. They have also given it a name. The Ubuntu 20.04 LTS mascot is called Felicity.

The default theme wallpaper features Felicity. The theme also has some more wallpaper in addition to the mascot wallpapers. All the images come from a copyright-free website, and every image is very focal.

**GNOME 3.36**

Ubuntu has defaulted to the GNOME desktop as the default desktop environment ever since the release of Ubuntu 17.10\. The Ubuntu team has worked deeply with the GNOME developers and the Ubuntu community to create a solid GNOME experience for Ubuntu users. Ubuntu also has ties with the developers at Debian to keep updating GNOME to the latest packages.

GNOME 3.36 has changes that are visible to the user for a beautiful user interface and hidden changes that improve the performance of the user interface and make the desktop experience very stable.

There is a new toggle for ‘do not disturb,’ which mutes all the notifications and helps users who want to stay focused on what they are doing. GNOME 3.36 also features simple and beautiful login and lock screens, resulting in a clean user interface. The login and lock screen blur the actual desktop background of the user.

The status menu features a quick suspend option. Also, users who like to be organized about the app grid can use a feature called ‘better app folder management’ with this release of GNOME.

Going by the tradition of every new GNOME release, desktop and system animations are now even smoother, and they do not put a lot of load on the CPU either.

**Big Applications**

Ubuntu now integrates easily with Microsoft Exchange and Google Gsuite. It ships with Firefox 75 as the default web browser that has continued features to protect a user’s privacy.

The default email client on Ubuntu is Thunderbird, which lets you access your emails from any provider quickly on your desktop. Irrespective of your email service provider, be it Gmail, Microsoft, other POP, or IMAP provider, you can easily configure your email account on Thunderbird. Ubuntu 20.04 LTS comes with Thunderbird 68.7.0 preloaded with it.

You also get LibreOffice 6.4 for all your productivity needs. This is a free but powerful office suite that lets you perform any office-related tasks with ease.

**Tier 1 OEM Support**

![Image](Images/image00123.jpeg)

Ubuntu is a very popular operating system and is used on a large scale in schools, enterprises, government, and public sectors. The Ubuntu team works closely with computer manufacturers like HP, Dell, and Lenovo to meet pre-loaded hardware requirements from these areas. Let us go through some examples where Ubuntu works with OEM partners to add value to desktop users’ Linux experience.

With the release of Ubuntu 20.04 LTS, you can get a certified device experience when you install the general release of Ubuntu. When you install Ubuntu on certified hardware from an OEM manufacturer, all the features of that specific hardware will be enabled automatically on the device, just as it would have been with factory images.

For example, if you have installed Ubuntu on a Dell device, the boot splash screen will automatically feature the Dell logo. Ubuntu also includes PulseAudio 14.0, BlueZ 5.53, and Sound Open Firmware to support SoundWire and SMIC, which is provided by OEM manufacturers on their hardware.

With security being critical, we can also see that many devices ship with a fingerprint reader and users prefer this way to unlock their systems to typing in a password. Ubuntu and the libfprint project are also making it possible to integrate this so that hardware vendors can be relieved for their devices that feature biometric authentication.

![Image](Images/image00124.jpeg)

![Image](Images/image00125.jpeg)

A feature called X11 fractional scaling has been a part of Ubuntu since Ubuntu 19.04 but was never exposed to users via the user interface. This has been exposed finally in Ubuntu 20.04 LTS so that Ubuntu users can enable fractional scaling easily through display settings. They can scale the display in increments of 25% from 100% to 200%.

![Image](Images/image00126.jpeg)

**Performance Computing and Gaming**

Machine Learning and Artificial Intelligence are the latest in data engineering, and enterprises are adopting these technologies rapidly. Ubuntu has taken note of this and is already integrating support for Artificial Intelligence for enterprises, from developer workstations to server racks, to the Edge and the cloud.

Ubuntu empowers data science on desktops and servers by providing the latest applications, libraries, and drivers needed for it. Data scientists can use Kubeflow on powerful Ubuntu systems to create AI models before deploying them on servers or public clouds. Ubuntu has become a standard for machine learning, from Wall Street to Silicon Valley. It is the first choice for both startups and fortune 50 companies.

If you also have a GPU on your system that you use for entertainment and gaming, Ubuntu 20.04 LTS has new features that will make you very happy. Ubuntu 20.04 LTS has an updated Steam package that supports new controllers and virtual reality peripherals if you are a gamer. You will also have Feral Interactive GameMode installed by default in Ubuntu. GameMode is a daemon that optimizes the operating system and the game process temporarily to have a rich gaming experience. At present, GameMode optimizes the CPU governor, process niceness, Input-Output priority, kernel scheduler, GPU performance mode, screensaver inhibiting, GPU overclocking, and custom scripts. If you have hybrid graphics for your system, you can now launch applications through the discrete GPU available in the GNOME shell. This can be done by using the ‘Launch on Discrete GPU’ item on the menu. This is supported for both NVIDIA and AMD GPUs.

Ubuntu also supports VA-API and nvenc through FFmpeg if you are a live streamer or a video content creator. These are features that are integrated into GPUs for encoding, decoding, filtering, etc. These features also offload intensive tasks from the CPU such that they are processed by the GPU instead. Applications such as Shotcut and OBG Studio use nvenc to benefit greatly from these hardware-encoding features.

**ZFS and ZSYS**

The ZFS file system was introduced as an experiment on Ubuntu 19.10. ZFS is shipped by default on Ubuntu 20.04 LTS that features encryption through hardware, pool trim, device removal, and improved performance. As mentioned earlier, ZFS is still in its experimental stages.

Zsys is an integration tool for Ubuntu and ZFS. Zsys takes an automatic snapshot of the system state whenever new software is installed, or the whole operating system is updated. You will be able to find these snapshots in the boot menu. This can also be used to create backups for the future.

**Changes since Ubuntu 18.04 LTS**

It is a known fact that Ubuntu users like to stick to Long Term Support releases. Users who are upgrading from Ubuntu 18.04 LTS to 20.04 LTS will see a huge number of changes as Ubuntu 20.04 gathers all the features that have been rolled through Ubuntu 18.10, 19.04, and 19.10. Let us highlight the most interesting changes.

GNOME Disks now support open-source disk encryption when you are formatting any disk. The performance for window previews and desktop zoom has been improved. Crash reports are now sent automatically by the bug-reporting tool whenever an application crashes. This is helpful, as the user is not interrupted anymore while doing their work. Support for microphones and speakers has been improved by tuning the sound panel in the GNOME Settings. The file search on the desktop has been improved by adding a tracker. Application switching has been made smoother by improving the Alt+Tab feature and the window preview feature. Unexpected errors on the system can be investigated with the introduction of the ‘Safe Graphics Mode.’

The CPU usage has been optimized, leading to better Desktop performance. The input and output latency has also been optimized for most graphics cards. This means that users will not enjoy faster and smoother frame rates. Ubuntu also allows DLNA sharing to share media to a smart TV or any other devices that support DLNA. Graphic drivers for NVIDIA GPUs are inbuilt into the Ubuntu install media now. This allows users to install drivers directly. We urge you to explore more features so that you customize the look and feel of Ubuntu as per your needs and enjoy the Ubuntu desktop to the fullest.

# Linux Using Vim

We will learn about the three modes of Vim. In addition, we will learn to edit and save text files in Vim and use the shortcuts available in Vim.

**Introduction to Vim**

As a Linux system administrator, editing files will be one of the tasks you end up regularly doing. There are many text editors available for Linux systems. One of the older text editors, which was widely used, is vi. Vi stands for the visual interface, as it was one of the first text editors that showed the document while it was being edited. Before vi, there were only line-based editors such as ed and ex. Vim is an improved version of vi.

Vim is highly extensible. It supports scripts in multiple languages, various text completion modes, file type plugins, and many other options. It can adapt to any role. There are third-party macros and extensions available for Vim on the internet for any purpose, from editing a particular type of file, completion, and introspection for all available programming languages, to simple tasks such as to-do lists.

**Is it Necessary to Learn Vim?**

As a system administrator, you will prefer a text editor. Some people use nano, others use gedit, and some even use emacs. Even if you already have a choice for an editor, it still makes sense to learn the basics of vi or Vim because, by default, vi and Vim are installed on every Linux distribution.

**Different Versions of Vim**

The Red Hat Enterprise Linux supports three different versions of Vim. There are use cases for every version, but all three versions can be used and run side by side. The following three variations are available:

*   Vim-minimal: This package only contains vi and related com

mands. The minimal installation of Red Hat Enterprise Linux

comes with this version of Vim.

*   Vim-enhanced: This package comes with Vim, providing fe

atures such as spell check, syntax highlighting, and file type plu

gins.

*   Vim-X11: This package comes with gvim, a Vim version with a

graphical window instead of running on the terminal. The best

feature of gvim is the menu bar, which is useful for new learners

of Vim who can’t remember specific commands. Depending on

the type of terminal and the user’s configuration, it is also possible

to use a mouse inside a regular Vim session.

**Modes of Vim**

Vim is not exactly a straightforward editor. The commands available in Vim aim at efficiency and speed and not exactly ease of remembrance. This is because Vim has many modes. This means that the function of keys and commands change based on the vim mode that is currently active.

Vim has the following three modes.

**Function**

**Mode**

**Command mode:** In this mode, you can do file navigation, cut, copy and paste functions, and other simple commands. Commands like undo and redo can also be performed in this mode.

**Insert mode:** Normal text editing can be performed in this mode. In addition, there is a variation of insert mode known as replacing mode, in which you can replace text instead of inserting it.

**Ex mode:** Functions such as opening a file, saving it, or quitting Vim can be performed in this mode. It also supports a few other complex functions. For example, the output of programs can be inserted into the current file using this mode. Vim configurations can be done from this mode as well. Everything that one can perform in ex can be done in this mode of Vim.

**Vim Workflow**

**Editor Basics**

Irrespective of the editor being used, you should always be able to perform these primary tasks.

1.  Make changes to the file or add new text to a file
2.  Save the changes and exit

**Opening Files**

Vim allows you to open files easily on the command line by specifying the filename as an argument. For example, you may use the following command to open a file at /var/log/maillog, where maillog is the file.

[root@server~]# vim /var/log/maillog

Note: If the file specified as an argument does not exist, but the directory is valid, Vim will create a new file with the filename specified and inform you that you are editing a new file.

Vim will open in the command mode by default. The filename, amount of characters, number of lines, and other details about the open file are displayed in the bottom left corner of the screen. It also displays information about the part of the file being shown, such as All for all, Top for the lines at the top, Bot for the last lines of the file, or a percentage that shows what part of the file you are at. The last line is called the ruler in Vim terminology.

**Editing Text**

If you have already used vi or Vim, you will know that keys do not work the way they should when you are in command mode. This is because command mode is not used to insert text but rather to perform functions based on the characters you type, such as copy and paste or cursor movements.

You can switch to insert mode by using a set of commands that correspond to different functions. Let’s go through them one by one.

The key and result for the same in as mentioned:

![Image](Images/image00127.gif)

You will know that you are in insert mode or replace mode by the indicator below, which shows —INSERT— or —REPLACE—

You can use the Esc key on the keyboard to return to command mode.

The version of vi or Vim that comes with Red Hat Enterprise Linux is preconfigured to identify normal movements of the cursor and even PgUp and End while you are in both command mode and insert mode. This is not the default setting for all variations of vi but is specific to Red Hat Enterprise Linux. Older versions of vi did not recognize these commands, and you could only move the cursor while in command mode using keyboard keys h, j, k, l.

The following table lists down some common keys that can be used to move the cursor while you are in command mode.

![Image](Images/image00128.gif)

Note: Pressing the Esc key on the keyboard will always cancel the current command or return you to the command mode of Vim. A good practice is to press the Esc key twice or more to make sure that you have returned to the command mode.

**Saving Files**

The Ex mode is used to save files in Vim. To enter the Ex mode, you need to press the colon (:) key on the keyboard while you are in the command mode. So if you are in the insert mode, first press the Esc key to switch to command mode and then press the colon to enter the Ex mode. When you switch to the Ex mode, you will see the ‘:’ symbol on the ruler, where you can proceed with typing a command. Once you are done typing a command, press Enter to complete the command.

The following table gives a list of commands that will help you save your changes and quit Vim in the Ex mode.

![Image](Images/image00129.gif)

![Image](Images/image00130.gif)

In the table above, w stands for write, implying saving changes, q stands for quit, and ! indicates an action is to be forced.

**Getting Help in Vim**

There is extensive online help for Vim, which is available through the editor itself. You can switch to command mode and type ‘: help’, and the help screen will be launched with the help needed to navigate through the help document. You can find help for a specific subject or topic by typing ‘: help subject’ from the command mode.

The help screen will open in a new split window. You can close the help screen by typing :q. To get help with split windows, you can type: help windows.

A semi-interactive tutor is also available. While in the command mode, you can type the command vimtutor. This will launch a guided tour of Vim, and a new user can learn the basics almost within an hour.

**Movement in Vim**

Most editors have navigation support with the limitation that you can move through only a single character or a single line. These single movement options are available in the command mode of Vim as well. Additionally, there are some advanced commands in Vim, which will help you navigate through a document more efficiently. These command shortcuts in Vim will help you move through a document per word, sentence, or even a paragraph. However, do note that these movements for the cursor will only work in the command mode and not in the insert mode of Vim.

![Image](Images/image00131.gif)

# Users and Permissions

When discussing user management, we have three important terms to understand:

*   Users
*   Groups
*   Permissions

Interactive accounts: Usually assigned to a user for accessing system resources.

The main difference between the two user types is:

*   Daemons use system accounts to access files and directories.

These will usually be disallowed from interactive login via shell or

physical console login.

*   End-users use interactive reports accessing computing resour

ces from either a shell or physical console login.

With this basic understanding of users, let’s now create a new user for Bob Jones in the Accounting Department. A new user is added with the adduser command.

Following are some adduser common switches:

![Image](Images/image00132.gif)

When creating a new user, use the -c, -m, -g, -n switches as follows:

[root@localhost Downloads]# useradd -c “Bob Jones Accounting Dept Manager.”

-m -g accounting -n bjones

Now let’s see if our new user has been created:

[root@localhost Downloads]# id bjones

(bjones) gid = 1001(accounting) groups = 1001(accounting)

[root@localhost Downloads]# grep bjones /etc/passwd

[root@localhost Downloads]# passwd bjones

Changing password for user bjones.

New password:

Retype new password:

passwd: all authentication tokens updated successfully.

[root@localhost Downloads]#

The user account is not enabled, allowing the user to log into the

system.

**Disabling User Accounts**

There are several methods to disable accounts on a system. These range from editing the /etc/passwd file by hand. Or even using the passwd command with the -lswitch. However, both of these methods have one big drawback: if the user has ssh access and uses an RSA key for authentication, they can still log in using this method.

Also, it may be good to note on the account why we disabled it.

[root@localhost Downloads]# chage -E 2005-10-01 bjones

[root@localhost Downloads]# usermod -c “Disabled Account whi

le Bob out of the country for five months” bjones

[root@localhost Downloads]# grep bjones /etc/passwd

bjones:x:1001:1001:Disabled Account while Bob out of the coun

try for four

months:/home/bjones:/bin/bash

[root@localhost Downloads]#

**Manage Groups**

Managing groups in Linux makes it convenient for an administrator to combine the users within containers applying permission-sets applicable to all group members. For example, all users in Accounting may need access to the same files. Thus, we make an accounting group, adding Accounting users.

For the most part, anything requiring special permissions should be done in a group. This approach will usually save time over applying special permissions to just one user. For example, Sally is in charge of reports and only Sally needs access to certain files for reporting. However, what if Sally is sick one day and Bob does report? Or does the need for reporting grow? When a group is made, an Administrator only needs to do it once. The add users is applied as needs change or expand.

Following are some common commands used for managing groups:

*   chgrp
*   groupadd
*   groups
*   usermod

chgrp: Changes the group ownership for a file or directory.

Let’s make a directory for people in the accounting group to store

files and create directories for files.

[root@localhost Downloads]# mkdir /home/accounting

[root@localhost Downloads]# ls -ld /home/accounting

[root@localhost Downloads]#

Next, let’s give group ownership to the accounting group.

[root@localhost Downloads]# chgrp -v accounting /home/ac

counting/

changed group of ‘/home/accounting/’ from root to accounting

[root@localhost Downloads]# ls -ld /home/accounting/

drwxr-xr-x. 2 root accounting 6 Jan 13 10:18 /home/accounting/

[root@localhost Downloads]#

Now, everyone in the accounting group has read and executed

permissions to /home/accounting. They will need write permis

sions as well.

[root@localhost Downloads]# chmod g+w /home/accounting/

[root@localhost Downloads]# ls -ld /home/accounting/

drwxrwxr-x. 2 root accounting 6 Jan 13 10:18 /home/accounting/

[root@localhost Downloads]#

Since the accounting group may deal with sensitive documents,

we need to apply some restrictive permissions for others or the

world.

[root@localhost Downloads]# chmod o-rx /home/accounting/

[root@localhost Downloads]# ls -ld /home/accounting/

drwxrwx—-. 2 root accounting 6 Jan 13 10:18 /home/accounting/

p.

![Image](Images/image00133.gif)

Let’s make a new group called secret. We will add a password to the group, allowing the users to add themselves with a known password.

[root@localhost]# groupadd secret

[root@localhost]# gpasswd secret

Changing the password for group secret:

New Password:

Re-enter new password:

[root@localhost]# exit

exit

[centos@localhost ~]$ newgrp secret

Password:

[centos@localhost ~]$ groups

secret wheel rdc

[centos@localhost ~]$

In practice, passwords for groups are not used often. Secondary groups are excellent and sharing passwords amongst other users is not a great security practice.

The groups command is used to show which group a user belongs to. Next, we will use this, after making some changes to our current user.

usermod is used to update account attributes.

Following are the common usermod switches.

![Image](Images/image00134.gif)

[root@localhost]# groups centos

centos : accounting secret

[root@localhost]#

[root@localhost]# usermod -a -G wheel centos

[root@localhost]# groups centos

centos : accounting wheel secret

[root@localhost]#

**Removing Users**

We have learned how to create users, but what if there are just too many of them? What if someone has decided to leave and his or her credentials are still on the system? How do you remove those?

Again, we will resort to both the GUI and the LUI methods. We do this to ensure everyone gets an idea of how things are done within the thrilling world of Linux. Whatever suits you best, later on, is yours to decide.

First, we use the graphical user interface:

1.  Go to the user menu on the top right side of the screen.
2.  Click on Settings.
3.  Select Details (the last option).
4.  Click on users.
5.  Click the unlock button.
6.  Enter the root password.
7.  Use the red button named “Remove user.”
8.  Decide whether you would like to keep the files or delete them.

Once done, click the appropriate choice. And that is it!

When you delete a user, you can delete the user settings, but if you believe the files could still be useful, ensure that you keep the files created by this user saved and accessible. The user, once deleted, will no longer have access to the system or his or her created files.

Now, let us take another look at this using the line user interface (LUI) method.

1.  Open the terminal.
2.  Type in: sudo deluser (username).
3.  Hit Enter, and that is it!

**Changing Passwords for Users**

This is rather easily done on the graphical user interface. However, we will only be focusing on the terminal here and how we can use it to change the password. To do that, punch in the following command:

sudo passwd (username)

You can change any account’s password without logging into these as long as you are the super-user/root user.

**Creating Groups**

We initially touched upon the term “group” when we were doing the permissions. We did not dive deeper to know what exactly a group is. Let us shed some light on this now as it is relevant to both the topic at hand and to you, the Linux user.

For every file or directory, permissions are set out for the owner, group, and others in that specific order.

A group is literally where a few users are found. For example, you may have a file that is relevant to the IT group. This group will have users who have everything to do with IT. Instead of assigning permissions to read and write to individual users, you can simply create a group and add the relevant users to this group. Now, when you share your file with the group, everyone within it will have access.

To create a new group, simply type in the following command:

sudo groupadd (groupname)

**Changing Permissions for Group**

Now we have created a group, let us now share a file with it for ‘read’ and ‘write’ accessibility. Don’t worry, all of these commands are already covered by us.

touch file123

mkdir test123

mv file123 test123

cd test123

ls -l

We started out with the “touch” command to create a file named “file123.” We followed by creating a directory using the make-directory (mkdir) command, and we named it “test123.” We then moved the file using the “mv” command into the directory we created. Lastly, we entered the newly created directory and used the listing command (long) to show us the permissions, owner, and group information.

Yet again, the mighty terminal saves us time. Imagine doing that without the terminal. It would have taken a little longer to pull all that off. Anyways, enough with praising the terminal; let us move forward.

As a test, let us wait here while you change the ownership to “group” to give them read and write permissions by using the “chown” commands. A tip: if it doesn’t go smoothly, use the sudo command!

Is everything done? Bravo! You have just changed the ownership of the file and provided the group with the required permission.

“But we don’t have a user added to the group yet.”

Right you are! That is why our next step is to ensure we learn how to add users to our newly created group. For the sake of an example, let us call this group “learners.”

Use the following command to add the user within this group:

sudo adduser (username) learners

If you switch to the username you just added to the group and try to access “file123,” you will also be able to access it without any issues. The reason why that happened is that we have allowed the entire group to have ownership over the file and have the necessary permissions to view and edit them. Now, since your new user is a part of this group, the user will have similar access as well.

To verify, use the Nano command without the sudo, and you should now be able to write the file and edit the same as you please.

This is something that can be seen in effect throughout major organizations and industries where thousands of employees and managers are added into groups and provided uniform access to files and directories that serve them some purpose.

We will also be looking at some other commands and examples further on. For now, let us get a little deeper into system configuration—what it is, why we need to configure the system, and what can it do for us in return. These are some of the questions that you should be able to answer at a beginner level. For advanced usage of the system and its configurations, you can refer to great books and browse through the Ask Ubuntu community for further guidance.

**Comparison of Linux with other Mainstream Operating Systems and Versions of Linux**

**Linux OS vs. Windows OS**

**Users**

There are three types of users on Linux (General users, administrators (root), and service), and, for Windows, there are four types of user accounts (Administrator, Standard, Child, and Guest).

**Usage**

According to market research data, on 92.63% of the world’s PCs, Windows is running, while at least 1% of PC users are using Linux. Many users say that it is difficult to use Linux compared to Windows, so the Linux complaint is limited to home use. It is intended for deep use as a server program. Therefore, organizational servers run on Linux, regardless of GUI.

Also, thanks to a license agreement with Microsoft, various PC vendors have the right to integrate Windows OS with their PC, making Windows gain market popularity with Linux. Although many PC vendors like Dell and HP have started offering Linux as a pre-installed OS, Windows still dominates the market.

**Kernel**

Linux uses a monolithic kernel that uses more efficient space, and Windows uses a micro-kernel that takes up less space than Linux but reduces system efficiency.

**File Programs**

In Microsoft Windows, files are stored in directories/folders in different data drives such as C: D: E: but, on Linux, one-order files in a tree structure that starts with the root directory are exported without other sub-records.

In the Linux OS, everything is treated as a file. The references are files, file files, and externally connected devices (like Printer, mouse, keyboard) that are also files.

**Security**

Every Windows user has experienced security and stability issues from time to time. Since Microsoft Windows is the most used Operating System, hackers and spam frequently target Windows. Windows (consumer types) was originally designed for easy use on a single-user PC without a network connection and had no built-in security features. Microsoft often removes spots of security with its Windows Update service. This comes out once a month, even if critical updates are made available regularly or when needed.

Most of the time, Windows OS users experience BLUE SCREEN OF DEATH. This is due to the system’s failure to respond. Finally, the user must put aside his worries and restart the PC manually.

On the other hand, Linux is based on multi-user builds, making it more stable than a single-user OS like Windows. Furthermore, since the public runs Linux with standard monitoring by developers worldwide, any new proposed issue can be resolved within a few hours, and the required pool can be ready to be delivered.

**Compatibility**

Windows Shoots. Windows scores. That’s when Redmond’s offer wipes the floor with Linux. Despite the recent software development or installation of Linux, Windows is still the master of collaboration.

Windows users can be sure that almost any software (even the most obscure, outdated) will work or be abandoned by developers. This is because Windows has good asset support. Plain and simple.

On the other hand, Linux had a problem with the basics that Windows users take for granted.

**Ease of Use**

Linux, in recent years, has gone too far and limited when it comes to usability. Distributors, such as Linux Mint and Ubuntu, have gone so far as to make their installation and setup easier for non-tech users to continue their day-to-day operations with greater ease.

Due to its growing market share, Windows is the default OS for most devices. Buy a new laptop or PC, and of course, the opportunity comes with Windows 10 installed. Unfortunately, users are used to clicking on the toolbar and opening their favorite programs for so many years now that it makes it very difficult to make the change.

**Privacy**

If you are a Linux user, you have an operating system that does not test you. Having Linux means that the program is your own. You can also add to the mix that most Linux programs come with a built-in encryption option. As a user, you can ensure that device theft does not cause a real problem with your data.

On the contrary, Windows has received a lot of advertising in the last few years. Users are given the opportunity to opt-out and help smart registry hacks are part of Redmond’s program. Windows can monitor user activity, offer synchronization with the Microsoft OneDrive service, or learn how to improve Cortana (Microsoft’s assistant). To be honest, I don’t like these tools because they are so disruptive. Or, some users like these features. A view of humility.

**Source Code**

Linux is an active operating system, and Windows OS is commercially viable. Linux has access to the source code and modifies the code at the user’s request, and Windows cannot access the source code.

In Linux, the user can access the kernel’s source code and change the code according to his or her need. It has its advantages. Bugs in the OS will be fixed as soon as possible, but developers may apply any weaknesses to the OS if available.

In windows, only members are selected to access the source code.

**License**

In most offers, the Linux kernel (along with GNU resources and accompanying libraries) is free and completely open-source. Companies offer paid support for their distros, but the resulting software is still available for download and installation.

**Linux OS vs. Mac OS**

Although both Linux and Mac are computer hardware applications, Linux is an open operating system that can be used on any device. The Mac is an operating system that can only be used on Mac devices. Linux works as an application, a platform for running other applications, and a server unit. At the same time, Mac is an operating system that allows other operating systems to run on it.

**Mac OS X vs. Linux: Hardware Support**

Both the system, Linux and Mac OS, shine in this field. However, since Mac OS is only used on Apple made of hardware, it offers a combination of robust and well-integrated software to give you the highest performance.

As for Linux, it has a variety of driver support software. Then, or before, it was a problem Linux could offer; no, instead, I should say; the hardware manufacturer did not provide driver support for its hardware in the Linux system. But now the timing has changed. Linux is the most widely used OS on both desktop and server devices. So now all major retailers are providing compatible Hardware drivers for Linux distros as soon as they get other applications such as Mac OS or Windows OS.

**Linux vs. Mac: Identified User Group**

If you can afford a lot of money and want a system ready to go, then I would prefer you to choose Mac OS. This app will give you a nice cool desktop environment with solid performance. Mac OS is an excellent choice for beginners and other advanced users who want to do the job of high-quality audio editing or video recording and graphic design.

Linux has both targeted user groups. If you are a noob to the world of Linux, go to Ubuntu, Linux Mint, or Elementary OS, but choose Arch Linux or Kali if you are looking for high quality or customized work environment. In addition, there is a Terminal or line interface that serves as a great tool for doing any tech-savvy level work.

**Linux OS vs. FreeBSD OS**

Both FreeBSD and Linux are open-source sources separate from their license and have the same environment as Unix. FreeBSD appeared in the Unix operating system years ago after many modifications and updates. Otherwise, Linux was developed from scratch as an alternative to Unix. Both Linux and FreeBSD split the file management category. Also, both of the same types of Shell sites serve as the primary means of communication. Apart from this, they share similar API programs. Due to various similarities, Linux and FreeBSD can share multiple tools and apps.

**Variation of License**

*   The licensing differences for Linux and FreeBSD are major

differences between them.

*   All Linux distributions, Linux Kernel, Linux programs,

GNU-based applications are licensed under the GNU General

Public or GNU GPL license.

*   The GNU GPL is also called copy-left.
*   The BSD license is almost identical to the GNU GPL, but work

from the BSD License is not required to maintain the terms of the

license.

*   Anyone can easily access, share, or modify their source code

without rewriting or modifying the revised source code.

*   The original BSD license and copyright certificate must be

included, and the updated source code is the only requirement.

*   The cost of each license depends entirely on the user’s needs

and philosophy.

*   The GNU GPL license promotes an open and free environment

and sharing.

*   Related software should be careful about relying on GNU-ba

sed software.

*   On the other hand, BSD-licensed software can be installed

easily and freely on closed source software.

*   This makes BSD software more attractive to businesses and

developers, hoping to sell their software as they can directly sell

software that stores their resources.

**Basic Differences**

*   History and genealogy of programs is another major difference

between Linux and FreeBSD.

*   Linus Torvalds developed the Linux kernel to replace MINIX,

which was barred from further study purposes at the University of

Helsinki.

*   It then integrates an advanced Linux kernel with multiple

components from GNU to create a complete system similar to

Unix.

*   Linux was completely upgraded from scratch without using

anything from the existing Unix system.

*   Linux differs from Unix in many ways.
*   On the other hand, FreeBSD has a close relationship with the

Unix app.

*   Berkeley Software Distributions or BSD was developed at the

University of California.

*   BSD later rewrites all original licenses with a full BSD licen

se, and the operating system was later fully integrated into all

other open-source channels.

**Versions of Linux**

**Gentoo**

Gentoo is a highly flexible meta distribution that allows users to use character authentication and software editing. Gentoo can be customized. The project was launched by Daniel Robbins in 2000\. Although it offers flexibility, it requires the technology to use it. In other words, this is not good for inexperienced users, as it can take a lot of time to get used to. Renewal can be time-consuming.

**Arch Linux**

Arch Linux was launched by Judd Vinet in 2002\. Initially, it was regarded as a separate project that existed between middle and advanced users. Later, it was raised using a device called “rolling-release.” Rolling release means the app has the ability to keep itself up to date. Arch Linux has an excellent software management infrastructure. It is installed to be able to install software from source code. Another misconception is the risk of deterioration due to occasional instability.

**Ubuntu**

Personality transforms Linux for desktop users. It was famous for a long time. It was launched in the early 2000s and is still popular with Linux users. Personality is based on DEB packages. It has long-term support with Canonical and supports business now with its own server type. Some of the special features of Ubuntu include the live DVD, supporting new technologies where the novice can easily use Ubuntu, and different desktop environments. One of the most important problems for Ubuntu is its incompatibility.

**MX Linux**

MX Linux has been introduced as a MEPIS Linux site. This is for personal and business purposes. The most popular feature of MX Linux is its graphical control tools, known as MX-Tools. It also has different platform support, different compatibility with graphics drivers, and ease of management. MX Linux may not be as friendly to novices as compared to Mint and Ubuntu. It takes time to get used to its installer, and some tools may appear different.

**Mint**

Linux Mint was launched in 2006 and made based on Ubuntu. This distribution is best for beginners. Mint has a variety of enhancements that make it easy to use. It provides interaction with other applications. Therefore, it is really suitable not only for personal but also for business use. The developers offer three types of releases, namely official (December), point releases (as required, e.g., bug fixes), and monthly summary releases. This makes Mint more stable.

**Going Back with Kali**

There are other special Linux programs designed for system security and access. Kali Linux is the most popular login testing platform right now. It all started with the creation of BackTrack from WHAX integration (WHAX was a Linux-based Slax distribution. The company behind it was Offensive Security. BackTrack 5 was based on Ubuntu Lucid LTS. It supports 32-bit and 64-bit formats with ARM.

In 2013, the company rebuilt the platform based on Debian and was released under the name Kali.

Kali Linux is very stable and advanced with its capabilities and a set of advanced entry-level testing tools.

# Commands Basics

You can now open the terminal. Right-click on the Desktop and choose ‘Open Terminal.’

If you don’t see this option, look for ‘Applications’ at the top of the window. Click on ‘Applications’ and go to ‘Accessories.’ Choose ‘Open terminal’ and open the text editor, that is, ‘Gedit.’ Just click on the search and type “text editor”. Add some text of your choice to the file and save it, maybe on the desktop. I have saved my file with the name first with the following text:

I am a Linux Guru

I am enjoying reading this book

Now go to the terminal and type the following:

cat first

After pressing the Enter key, the file’s contents will be displayed in the window. For example, to list the content contained in a short file.

**Changing Directories**

You might also want to navigate or change directories via the terminal. Use the command ‘cd’ to achieve this, which stands for “change directory.”

Example:

cd /home

The use of a forward slash (/) means relative to the root, meaning that this command will be executed regardless of the directory you are in. Now type the following command:

cd httpd

The directory will be changed to ‘httpd’ but relative to the ‘/home’ directory. So the full working directory will be ‘/home/httpd’. Now type the following command: In our case, we will move from ‘/home/httpd’ to the ‘/home’ directory. Type the following command:

cd ~

This command changes the user’s home directory ‘/home/(username)’. The “username” will be the name you have used on the computer. The symbol “~” is called the tilde and it is used in Linux to represent the user’s home directory.

**Copying Files**

The command ‘cp,’ which stands for “copy files,” is used for copying files. Note that the file is not deleted from its initial location and a duplicate of the same is made at the specified location. Type the following command:

cp first me

The command above will duplicate the file first at the same directory but with a new name, that is ‘me.’ If the file ‘me’ exists in the directory, it will be overwritten and you will not be warned before this command is executed. Consider the command below:

cp –i first me

Notice that we have added the ‘–i’ option in the above command. If the file ‘me’ exists in the directory, you will be notified before it is overwritten. Next, try the following command:

cp –i /d/file

The file ‘/d/file’ will be copied into the same current directory and then named ‘file’ with the above command. Note that we have used the ‘–i’ option so if it already exists, we will be notified before it is overwritten.

You might also need to copy all the files in a particular directory to another. This can be achieved as follows:

cp -dpr sourcedirectory destinationdirectory

All the files in the ‘sourcedirectory’ directory will be copied to the ‘destinationdirectory’ directory. Notice that we have used the option ‘–dpr’. This means the following:

-d – means that links will be preserved

-p – file attributes will be preserved

-r – copying will be done recursively

It is good to specify those options if needed while copying all the files from a directory, otherwise, the default settings will be applied, which might produce an unwanted result.

To show the amount of space on a disk used on each mounted file system, use the command ‘df’.

**‘Less’ Command**

The less command is the same as the more command. The difference comes in that the user can page up or down through the file with this command. Consider the example below:

**less first**

The above command will display the contents of the file ‘first.’

**‘Ln’ Command**

This command creates a symbolic link to a certain file. Write and run the following command:

ln –s first slink

The command above will create a symbolic link named ‘slink’ to link to the file ‘first.’ For example, the command ls ‘–i first slink’ will show that the two files are different and have different “inodes.”

**‘Locate’ Command**

This is used for searching in the database. Run the following com

mand:

slocate –u

A database named ‘slocate’ will be created. Before you can search for a file, this command must be run first. However, ‘cron’ will run this command on a periodical basis on most systems. Again, run the following command:

locate whois

This command will look for files in your system whose name contains the string “whois.”

**‘Logout’ Command**

The command is used to log out the user who is currently logged into the system. Just go to the terminal and type this command:

logout

You will then be logged out and returned to the login screen.

**‘Ls’ Command**

‘Ls’ stands for list. It is used for listing files in a directory. However, it comes with many options that need to be known as well, otherwise, you will become confused. If you need to list all the files in the current directory except for those starting with “.” then just type in the command:

ls

Note that only the file names will be listed. You might need to show more details about the files in the directory such as the ownership permissions, their size, time and date stamp, etc. This can be achieved with the following command:

ls –al

**‘More’ Command**

Send contents of a file one page at a time to the screen. It can also work on piped output. Let us list the contents of the file ‘/etc/profile’ to the screen. This is an in-built file, meaning that it comes with the operating system and it contains the profiles for the users of the system:

more /etc/profile

Note that the contents of the file will be displayed one page at a time. This is because the content is too big to be displayed on a single page. Consider the command below:

ls –al | more

The command will list all files in the directory and output will be piped through ‘more.’ If the output from the directory can’t fit on one page, it will be listed on an additional page.

**‘Mv’ Command**

This command stands for “move” and is used for renaming or moving files. Consider the command below:

mv –i first first2

The file will be moved from ‘first’ to ‘first2,’ meaning it will be renamed ‘firts2’ rather than ‘first.’

mv /d/first

The above command will move the file ‘first’ from the directory ‘/d’ to the current working directory. So now you have seen how the ‘mv’ command is a powerful tool.

Now that we have been talking of working directories, what are they exactly? And how can we know in which directory they currently are? Just type the command:

pwd

After pressing the Enter key, you notice that the output is a directory. This shows the directory which you are currently in. The abbreviation ‘pwd’ stands for “print working directory” and shows the current working directory.

**‘Shutdown’ Command**

This command is used for shutting down the system. The purpose of this command is to halt the current process and shut down the system immediately. To do this, use the following code:

shut down –h now –.

The next command is used to reboot the system, meaning that it will immediately shut down and then restart the system. To do this, use the command below:

shut down –r now-

**‘Whereis’ Command**

This command is used for showing the manual, source, and binary files for a command. Consider the command below:

whereis ls

This command will show the manual and binary files for the command ‘ls’.

Above is the list of commands that have been run on my system. You can try on your system and observe the output.

**‘Sudo’ Command**

This stands for “superuser do.” It has the purpose of allowing a permitted user to execute commands as a “superuser.” This is usually defined in the ‘sudo’-er’s list. It is important to ensure security by ensuring that the correct people only execute sensitive commands. Another command, the ‘su’ command, enables you to log in to the system as a superuser. The purpose of ‘sudo’ is to borrow privileges from the superuser. This explains the difference between these two commands, the ‘su’ and the ‘sudo’ commands. The ‘sudo’ command is normally used in commands that will change the system files, such as when updating or upgrading the OS. This shows how secure the command is compared to the ‘su’ command.

**‘Mkdir’ Command**

This command stands for “make directory.” It creates a new directory and names its path. If this path already exists, an error saying that the folder cannot be created will be outputted.

I have made a directory named “m.” Once I list the available directories after creating the directory, I find that it has been created. Notice that I have run the command as ‘sudo’. Without this, the command won’t run. This is for security purposes. Once you use the ‘sudo’ command for the first time, you will be prompted to provide the superuser’s password. It is good to note that you can only create a directory inside a folder and you must have a “write permission” on that folder.

Otherwise, you will be unable to do so.

**‘Uname’ Command**

It stands for “Unix name.” With this command, you can get detai

led information about the operating system, kernel, and machine.

Information about the OS, the kernel, and the machine have been

shown.

Ubuntu – the name of the kernel of the machine

SMP – the machine’s node name

I686 – processor configuration

GNU/Linux – the name of the operating system

You can see how the command gives detailed information.

**‘Touch’ Command**

This command is used to create a file only if it does not exist. It stands for Update the access and modification times of each file to the current time. If the file already exists, its timestamp will be changed but its contents will remain the same. It is possible to use the command to create a file with a “write permission” if the file does not exist. To create a file named ‘touchfile:’

touch touchfile

If the file does not exist in the directory, it will be created.

**‘Cal’ Command**

It can be used to display the month of the current date or the month of a past or advancing year.

**‘Date’ Command**

Used for displaying both the current date and time on the terminal as shown below:

If the current date of your system is wrong, you can set it to the correct date and time as follows:

Date –set=’21 march 2015 18:50’

We have set both the date and the time in the above command.

**Advanced Commands in Linux**

**The ‘grep’ Command**

This command is used to find a string or a specific pattern in a file. It is available in all distros of Linux. However, if you find it uninstalled in your system, it can still be installed separately. On Debian and Ubuntu you can install it by doing the following:

sudo apt-get install grep

In Red Hat Linux, install it using this command:

sudo yum install grep

From our file ‘first,’ let us perform the ‘grep’ command. Remem

ber the contents of the file:

Let us use the ‘grep’ to search for the word Linux in the file first:

Notice the output, the line with the word ‘Linux,’ and that it makes the search word red to differentiate it from the rest. However, this search is case-sensitive. If we could have searched for the word ‘linux,’ with a lower case “L,” rather than Linux, then it won’t be found.

Notice also that the output is null, meaning that no word matched the search word. To make the search case insensitive, so that it won’t differentiate the two words, use the ‘–i’ option.

The ‘grep’ command can also be used to perform multiple searches, meaning that we are going to search for more than one word in the file. This is a good feature and you might need to use it someday. To use it, do the following:

Notice that we have used the command:

grep –ie ‘am’ –e ‘linux’ first

Where the ‘–i’ is for case insensitive search while ‘–e’ specifies that it is multiple searches.

As shown below, the grep command can also be used to do the opposite of what you’ve provided:

grep -iv ‘linux’ first

The above command should return all the lines without the word Linux once it has been run. In the specified file, that is, ‘first,’ this should be the second line.

Note the ‘–i’ is for case insensitive search whereas the ‘–v’ has the purpose of returning the opposite of the search criteria. The ‘–in’ option when used with the ‘grep’ command returns the line number. To show the line number of the sentence containing the word ‘enjoying,’ the following command can be used:

grep –in ‘enjoying’ first

You can also return the number of lines above the search criteria.

grep –iB1 ‘enjoying’ first

This will return the line immediately above the line with the search criteria which is ‘enjoying’.

**‘Tail’ Command**

This is a very common command in Linux. It is used to output the last part of files. The last 10 lines of the file are printed on the command window. A header is used to precede each set of outputs. A dash (–) will be displayed on the standard output if you don’t specify the file name. To print the last ten lines of a file, use the following command:

tail filename

Let us print the last 10 lines of the file first.

tail first

Notice that the file first contains only two lines. This is why the command is outputting only the two lines. Try with a file containing more than two lines and observe the output. It will only print the last ten lines of the file. Another important thing to be keen on is the extension of the file. It is a ‘.c’ file, specify that it is a ‘.c’ file and the rest.

In my case, the file ‘first’ is just a normal file created using the normal text editor, so the extension is of no importance. However, the last ten lines printed on the standard output are just the default value if you don’t specify the number of lines to be outputted. This value can be set to any number of lines. Consider the example shown below:

tail filename –n 120

The command above will output the last 120 lines of the file that you specify. It is easy to set the number of these lines. With this command, one can monitor live updates on his file. This means that he will be able to see any new lines that are added to the file. Consider the example shown below:

tail -f first | grep 24.12.162.11

The above can be used to monitor the file ‘first’ in real time. It is a combination of both the ‘tail’ and the ‘grep’ commands. This shows how different Linux commands can be combined to achieve a very useful functionality.

The ‘tail’ command will monitor the file ‘first’ in real time. The grep command will receive the last 10 lines of the file, as well as any new lines added to it. The command ‘grep’ will then read the output of the files from ‘tail’ and print to the standard output only the lines with the address 24.12.162.11\. The other lines will not be printed.

To print the last six bytes of the file ‘first’, use the following command:

tail –c6 first

That is why it is the only word printed on the standard output. Now we can combine the ‘–c’ option and the ‘+’ symbol. This will print from the byte that we specify. Consider the command shown below:

tail –c+7 first

This will print all the characters from the seventh byte of the file.

To conclude with this command, consider the following options:

1\. The last “n” bytes of a file are printed. When this is preceded by

a ‘+’ symbol, the bytes to the right of byte ‘n’ will be printed.

2\. It prints the lines that are appended on the file as it grows. This

means that it starts by outputting the last ten lines of the file to

the standard output and then waits for new lines to be added to

the same file. As new lines are added, they will also be printed on

the standard output. This is useful for those debugging applica

tions. Error messages will be printed to the log files.

3\. It prints the last ‘n’ lines of the file. If a ‘+’ precedes this, the last

from the ‘nth‘ line will be printed on the standard output.

**‘Wc’ Command**

The ‘wc’ command, which stands for “wall count,” is one of the Linux commands. It can be used to count how many lines are in a file. For instance, if you want to know the number of lines in a file such as ‘first,’ do the following:

wc –l <first

The above command shows our file has only two lines, which is true. To get both the number of lines and the name of the file, do the following:

wc –l first

wc first

The command will output the number of lines in the file, the number of words in the file, and the total bytes of the file. The file name will also be shown. Note that these will be shown in the order mentioned above so don’t get confused.

This is all true. These have been displayed in the order that we mentioned above; again, that’s line number, word number, byte number, and file name. The above command can be split so that you can view the details one at a time.

Once you run each of the above commands, you will get the values. Replace the word ‘filename’ with the name of the file you want while running the above commands.

**‘Last’ Command**

Sometimes, you might need to see the list of logins for your system. This is good for those using Linux in production environments, especially for security purposes. Someone cannot deny having logged into the system. Just go to the command line and type in ‘last.’ You will be shown the users who have logged into your system, the terminal they used, and the date and time of login. If these users are still logged in, you will be notified of this as well.

Run the command shown below:

last -100

The program above will display your system’s latest 100 logins. The difference between the login and the logout time is also shown.

Other options for the last command include the following:

1.  –R: this will suppress the display of the hostname.
2.  –a: displays the name of the host in the last column.
3.  –d: this is for remote logins. Linux stores the IP address of the

remote machine and then translates it into a hostname.

4.–F: full login and logout dates and times are printed.

5.–i: shows the IP address of the remote host. The IP address is

in numbers and dots form.

6.–w: displays domain and full user names as outputs.

7.–x: shows the shutdown entries as well as run level changes of

the system.

It is good to note that the last command searches through the file ‘var/log/wtmp’. This file is responsible for storing the names of users who have logged into the system. The command will then display the logins and logouts for users since the time this file was created, so you can always consult this file at any time. If you need to display all the users who have ever logged into the system, run the following command:

Last | more or last | less

The command above will again search through the file ‘var/log/wtmp’ to find these users. Since the output might be too much to fit in a single screen, use the ‘more’ or ‘less’ command so that the output will display one page at a time.

Rather than knowing about the login and logout times for all users, you might only be interested in knowing about a particular user. With the ‘last’ command, this can easily be achieved as follows:

last username

last username | less

last username | grep ‘Fri Feb 24’

You might also not be interested in knowing the hostname. This can be hidden using the ‘–R’ option as mentioned above. To use this option, do the following:

Last –R -or- last –R username

The year is the default login and login time. You might be interested in knowing these times in full. This can be done as follows:

Last –F

As you can see, the time has been shown in full rather than showing the year alone. This shows how powerful the ‘last’ command is.

Below are a few other options for using the ‘last’ command. To see the reboot history of the machine since the creation of the file:

last reboot -or- last –x reboot

To see when the machine was last shutdown:

last –x shutdown -or- last

**Listing Files and Understanding ls Output**

Here is the output from an ls command using the -l option. The -l flag tells ls to display output in a long format. If you need to see what files or directories exist, use ls. However, if you need detailed information use ls -l.

$ ls -l

-rw-rw-r— 1 bob users 10400 Sep 27 08:52 sales.data

On the far left of the ls output is a series of characters that represent the file permissions. The number that follows the permissions represents the number of links to the file. The next bit of information is the owner of the file followed by the group name. Next, the file size is displayed followed by the date and time when the file was last modified. Finally, the name of the file or directory is displayed. Here is the information displayed by the ls -l command in table form:

![Image](Images/image00135.gif)

**Listing All Files, Including Hidden Files**

Files and folders with a period (.) in their names are considered hidden and are not displayed by default. Use the -a option to reveal these hidden files and directories.

$ ls -a

.

..

.profile

.bash_history

sales-lecture.mp3

sales.data

tpsreports

Up until this point when you have used options, you have preceded each option with a hyphen (-). Examples are -l and -a. It is possible to combine options that do not require arguments. Only one hyphen is required followed by the options. If you want to show a long ls listing with hidden files, you could run ls -l -a or ls -la. You can even change the order of the flags, so ls -al works too. They are all equivalent.

$ ls -l

total 2525

-rw-r—r— 1 bob sales 2562856 Sep 27 08:54 sales-lecture.mp3

-rw-r—r— 1 bob users 10400 Sep 27 08:52 sales.data

drwxr-xr-x 2 bob users 512 Sep 28 14:49 tpsreports

$ ls -l -a

total 2532

drwxr-xr-x 4 bob sales 512 Sep 28 14:56 .

drwxr-xr-x 14 root root 512 Sep 27 08:43 ..

-rw-r—r— 1 bob users 28 Sep 28 14:22 .profile

-rw———- 1 bob users 3314 Sep 28 14:56 .bash_history

-rw-r—r— 1 bob sales 2562856 Sep 27 08:54 sales-lecture.mp3

-rw-r—r— 1 bob users 10400 Sep 27 08:52 sales.data

drwxr-xr-x 2 bob users 512 Sep 28 14:49 tpsreports

$ ls -la

total 2532

drwxr-xr-x 4 bob sales 512 Sep 28 14:56 .

drwxr-xr-x 14 root root 512 Sep 27 08:43 ..

-rw-r—r— 1 bob users 28 Sep 28 14:22 .profile

-rw———- 1 bob users 3314 Sep 28 14:56 .bash_history

-rw-r—r— 1 bob sales 2562856 Sep 27 08:54 sales-lecture.mp3

-rw-r—r— 1 bob users 10400 Sep 27 08:52 sales.data

drwxr-xr-x 2 bob users 512 Sep 28 14:49 tpsreports

$ ls -al

total 2532

drwxr-xr-x 4 bob sales 512 Sep 28 14:56 .

drwxr-xr-x 14 root root 512 Sep 27 08:43 ..

-rw-r—r— 1 bob users 28 Sep 28 14:22 .profile

-rw———- 1 bob users 3314 Sep 28 14:56 .bash_history

-rw-r—r— 1 bob sales 2562856 Sep 27 08:54 sales-lecture.mp3

-rw-r—r— 1 bob users 10400 Sep 27 08:52 sales.data

drwxr-xr-x 2 bob users 512 Sep 28 14:49 tpsreports

$

**Listing Files by Type**

When you use the -F option for ls, a character is appended to the file name that reveals what type it is.

$ ls

dir1 link program regFile

$ ls -F

dir1/ link@ program* regFile

$ ls -lF

total 8

drwxr-xr-x 2 bob users 117 Sep 28 15:31 dir1/

lrwxrwxrwx 1 bob users 7 Sep 28 15:32 link@ -> regFile

-rwxr-xr-x 1 bob users 10 Sep 28 15:31 program*

-rw-r—r— 1 bob users 750 Sep 28 15:32 regFile

![Image](Images/image00136.gif)

A link is sometimes called a symlink, short for symbolic link. A link points to the location of the actual file or directory. You can operate on the link as if it were the actual file or directory. Symbolic links can be used to create shortcuts to long directory names. Another common use is to have a symlink point to the latest version of installed software as in this example.

bob@linuxsvr:~$ cd /opt/apache

bob@linuxsvr:/opt/apache ~$ ls -F

2.4.5/ 2.4.7/ current@ README

bob@linuxsvr:/opt/apache$ ls -l

drwxr-xr-x 2 root root 4096 Sep 14 12:21 2.4.5

drwxr-xr-x 2 root root 4096 Nov 27 15:43 2.4.7

lrwxrwxrwx 1 root root 5 Nov 27 15:43 current -> 2.4.7

-rw-r—r— 1 root root 1048 Sep 14 12:58 README

**Listing Files by Time and in Reverse Order**

If you would like to sort the ls listing by time, use the -t option.

$ ls -t

tpsreports

sales-lecture.mp3

sales.data

$ ls -lt

total 2532

drwxr-xr-x 2 bob users 512 Sep 28 14:49 tpsreports

-rw-r—r— 1 bob sales 2562856 Sep 27 08:54 sales-lecture.mp3

-rw-r—r— 1 bob users 10400 Sep 27 08:52 sales.data

When you have a directory that contains many files, it can be convenient to sort them by time, but in reverse order. This will put the latest modified files at the end of the ls output. The old files will scroll off the top of your display, but the most recent files will be right above your prompt.

$ ls -latr

total 2532

drwxr-xr-x 14 root root 512 Sep 27 08:43 ..

-rw-r—r— 1 bob users 10400 Sep 27 08:52 sales.data

-rw-r—r— 1 bob sales 2562856 Sep 27 08:54 sales-lecture.mp3

-rw-r—r— 1 bob users 28 Sep 28 14:22 .profile

drwxr-xr-x 2 bob users 512 Sep 28 14:49 tpsreports

drwxr-xr-x 4 bob sales 512 Sep 28 14:56 .

-rw———- 1 bob users 3340 Sep 28 15:04 .bash_history

**Listing Files Recursively**

Using the -R option with ls causes files and directories to be displayed recursively.

$ ls -R

.:

Fred John old

Jane.doc

$

You can also use the tree command for more visually appealing outputs. If you only want to see the directory structure, use tree -d.

tree: List contents of directories in a tree-like format.

tree - d: List directories only.

tree - C: Colorize output.

$ tree

.

│ ├── Fred

│ ├── John

│ └── old

│ └── Jane.doc

├── sales.data

├── sales-lecture.mp3

└── tpsreports

2 directories, 6 files

$ tree -d

.

└── old

2 directories

$

**List Directories, Not Contents**

Normally when you run ls against a directory the contents of that directory are displayed. Use the -d option to ensure that you only get the directory name.

total 3

-rw-r—r— 1 bob users 36 Sep 27 08:49 Fred

-rw-r—r— 1 bob users 36 Sep 28 09:21 John

drwxr-xr-x 2 bob users 512 Sep 27 12:40 old

**Listing Files with Color**

Earlier you used ls -F to help differentiate file types by adding a character to the end of their names in the ls output. You can also use color to distinguish file types by using ls —color.

picture alt

**Commonly Used ls Options**

Here is a recap of the ls options you have learned:

![Image](Images/image00137.gif)

**Working with Spaces in Names**

If you want to make your life easier when working from the command line, do not use spaces in file and directory names. Hyphens (-) or underscores (_) can be good substitutes for spaces. CamelCase, the practice of capitalizing each word, is another good option. For example, instead of naming your latest literary attempt “the next great american novel.txt” you could use “the-next-great-american-novel.txt,” “the_next_great_american_novel.txt,” or even “TheNextGreatAmericanNovel.txt.”

Sooner or later you will encounter a file or directory that contains a space in the name. There are two ways to deal with this. The first is to use quotation marks. Even though the file name is a file, operate on it using “a file.” The second option is to escape the space. Escaping is like using quotes, but for single characters. The escape symbol is \, also known as a backslash. To escape a space, precede the space with the backslash (\) character.

$ ls -l

-rw-r—r— 1 bob users 18 Oct 2 05:03 a file

$ ls -l a file

ls: a: No such file or directory

ls: file: No such file or directory

$ ls -l “a file”

-rw-r—r— 1 bob users 18 Oct 2 05:03 a file

$ ls -l a\ file

-rw-r—r— 1 bob users 18 Oct 2 05:03 a file

$ ls -lb a*

-rw-r—r— 1 bob users 18 Oct 2 05:03 a\ file

$

The -b option to ls causes it to print escape codes. Note that quoting and escaping not only applies to spaces but with other special characters as well including | & ‘ ; ( ) < > space tab.

**Deep Dive**

*   Escaping Special Characters in Linux and Unix: With 7 Practi

cal Examples: An article that takes an in-depth look at escaping.

*   man ls: To learn about all of the available options to ls refer to

the man page.

**Deleting, Copying, Moving, and Renaming Files**

**Removing Files**

Eventually, you will get tired of all the old files you created just laying around, cluttering up your home directory, and taking up precious space. To delete them, use the rm command.

rm file: Remove file.

rm -r directory: Remove the directory and its contents recursively. If you want to remove a directory with rm, you have to supply the -r argument.

rm -f file: Force removal and never prompt for confirmation.

Search patterns can be used to delete multiple files at once. It’s a good idea to double-check what you are going to remove with ls before you execute rm.

$ ls s*

sales-lecture.mp3 sales.data secret secret.bak

$ rm s*

$ ls -d .*

. .. .profile .bash_history

$ rm .*

rm: cannot remove ‘.’: Is a directory

rm: cannot remove ‘..’: Is a directory

$ ls -d .*

. ..

Note that rm .* will not remove . (this directory) and .. (the parent directory).

**Copying Files**

To copy files, use the cp command. If you want to create a copy of a file, you can run cp source_file destination_file. You can also copy a file, or a series of files, to a directory by using cp file(s) dir.

cp source_file destination_file: Copy source_file to destination_

file.

cp source_file1 [source_fileN …] destination_directory: Copy

source_files to destination_directory.

cp -i source_file destination_file: Run cp in interactive mode. If

the destination file already exists, cp will ask you before overwri

ting it.

cp -r source_directory destination: Copy source_directory recur

sively to destination. If destination exists, copy source_directory

into destination, otherwise create destination with the contents of

directory.

$ cp file1 file2

$ mkdir dir

$ cp file1 file2 dir/

$ ls dir

file1 file2

$ rm dir/*

$ cp file1 file2 dir

$ cp -i file1 file2

overwrite file2? (y/n [n]) n

not overwritten

$ cp -r dir dir2

$ ls dir2

file1 file2

$ cp dir dir3

cp: dir is a directory (not copied).

$ mkdir dir3

$ cp -r dir dir2 dir3

$ ls dir3

dir dir2

$ tree dir3

dir3

├── dir

│ ├── file1

│ └── file2

└── dir2

├── file1

└── file2

**Moving and Renaming Files**

The way to rename files or directories in Linux is to use the mv command. The mv command moves files from one location to another. This can be used to relocate files or directories and it can be used to rename them too.

mv source destination: Move files or directories. If the destination is a directory, the source will be moved into the destination. Otherwise, the source will be renamed to the destination.

mv -i source destination: Run mv in interactive mode. If the destination exists, mv will prompt you before it overwrites the file.

Look at the following examples. They should make it clear how the mv command behaves in various situations.

$ ls -F

dir/ dir2/ dir3/ file1 file2

$ mv dir firstdir

$ ls -F

dir2/ dir3/ file1 file2 firstdir/

$ mv file1 file1.renamed

$ ls -F

dir2/ dir3/ file1.renamed file2 firstdir/

$ mv file1.renamed firstdir/

$ ls -F

dir2/ dir3/ file2 firstdir/

$ ls -F firstdir/

file1 file1.renamed file2

$ cat firstdir/file1

This text started out in file1.

$ cat firstdir/file2

This text started out in file2.

$ mv firstdir/file1 firstdir/file2

$ cat firstdir/file2

This text started out in file1.

$ ls -F firstdir/

file1.renamed file2

$ mv -i firstdir/file1.renamed firstdir/file2

overwrite firstdir/file2? (y/n [n]) n

not overwritten

$

In the above example, a directory was renamed with mv dir firstdir. Next, a file was renamed with mv file file1.renamed. Next file1.renamed was relocated to the firstdir directory with the mv file1.renamed firstdir/ command. A file was overwritten with the mv firstdir/file1 firstdir/file2 command. The -i option allows you to be prompted before a file is rewritten.

**Sorting Data**

You have already seen the sort command in use. In the simplest form, it sorts lines of text alphabetically.

sort file: Sort text in file.

sort -k F file: Sort by key. The F following -k is the field number.

sort -r file: Sort in reverse order.

sort -u file: Sort text in file, removing duplicate lines.

$ cat more-secrets

tags: credentials

user: bob

pass: Abee!

tags: credentials

$ sort more-secrets

pass: Abee!

tags: credentials

tags: credentials

user: bob

$ sort -u more-secrets

pass: Abee!

tags: credentials

user: bob

$ sort -ru more-secrets

user: bob

tags: credentials

pass: Abee!

$ sort -u -k2 more-secrets

pass: Abee!

user: bob

tags: credentials

**Creating a Collection of Files**

To generate an archive from a collection of files and/or directories, use the tar command. You might want to make a backup or duplicate of a set of files. You might want to transmit numerous files at once or in a batch. In these situations, tar can help.

tar [-] c|x|t f tarfile [pattern]: Create, extract, or list contents of a

tar archive using a pattern, if supplied.

You will notice that tar does not require a hyphen (-) to precede its arguments. Traditionally, the hyphen is not allowed, but tar allows it. It’s the same as tar -cf file.tar if you see tar cf file.tar. Here’s a rundown of some of the most popular tar alternatives.

c: Create a tar archive.

x: Extract files from the archive.

t: Display the table of contents (list).

v: Causes tar to be verbose.

f file: The tar archive file to perform operations against.

In the following example, tar is used to create (tar cf tps.tar) an archive, list the contents of the archive (tar tf tps.tar), and extract the contents (tar xf tps.tar).

$ tar cf tps.tar tpsreports/

$ tar tf tps.tar

tpsreports/

tpsreports/sales-report.txt

tpsreports/coversheet.doc

$ cd /tmp

$ tar xf /home/bob/tps.tar

$ ls tpsreports/

coversheet.doc sales-report.txt

$

If you would like to see the files that are getting placed into the archive or extracted from the archive, use -v to enable verbose mode.

$ tar cvf misc.tar sec* tpsreports

secret

secret.bak

tpsreports/

tpsreports/sales-report.txt

tpsreports/coversheet.doc

$ tar xvf /home/bob/misc.tar

secret

secret.bak

tpsreports/

tpsreports/sales-report.txt

tpsreports/coversheet.doc

**Compressing Files to Save Space**

Compress a file with a gzip file. file.gz is the name of the compressed file that results.

Uncompress files with a gunzip file.

Concatenates and displays compressed files with gzcat or zcat.

The command du can be used to see how much space a file takes up.

du: Estimates file usage.

du - k: Display sizes in Kilobytes.

du -h: Display sizes in a human-readable format. For example,

1.2M, 3.7G, etc.

Here are some simple examples of how to compress and uncom

press files:

$ du -k data

15360 data

$ gzip data

$ du -k data.gz

26 data.gz

$ ls data*

data.gz

$ gunzip data.gz

$ ls data*

data

$ du -k misc.tar

10 misc.tar

$ gzip misc.tar

$ du -k misc.tar*

misc.tar.gz

$

**Compressing Archives**

In modern versions of the tar command, gzip compression is built-in. If you want to create, extract, or list the contents of a compressed archive, use the -z argument. As a matter of convention compressed tar files will end in either .tar.gz or .tgz. Here is how this looks:

$ tar zcf tps.tgz tpsreports

$ ls *.tgz

tps.tgz

$ tar ztf tps.tgz

tpsreports/

tpsreports/sales-report.txt

tpsreports/coversheet.doc

$

If you run across an older version of tar without gzip compression built-in, you can use pipes to create compressed archives. When a hyphen (-) is used in place of a file name, that means to use standard output. Running the command tar cf - pattern will create an archive of “pattern” and send the output to standard output which is normally your screen. If you follow the command with a pipe, that standard output will be used as the input for the next command following the pipe. To force gunzip to send its output to standard out, use the -c argument. With this in mind, here is how you can create, list, and extract a compressed archive using tar, gzip, and pipes:

$ tar cf - tpsreports | gzip > tps.tgz

$ ls *.tgz

tps.tgz

$ gunzip -c tps.tgz | tar tf -

tpsreports/

tpsreports/sales-report.txt

tpsreports/coversheet.doc

$ cd /tmp

$ gunzip -c /home/bob/tps.tgz | tar xf -

$ ls tpsreports/

coversheet.doc sales-report.txt

$

**Introduction to Terminals and Shells**

Working with the Linux operating system requires knowledge about the terminal and the command line. Therefore, it is essential to know these and be slightly familiar with their usage and the available standard commands. But don’t fear, we will describe each in detail. These terms sound much more intimidating than they are in reality.

The ability to communicate with the system in a text-based format is why programmers have a soft spot for Linux, as this is the standard way for programmers to give instructions to computers. Another reason is the absolute control over the system that other operating systems cannot provide, even with their command-line interpreters.

Some beginners have even reported that using and becoming familiar with issuing commands in this text-based format has made the transition to program development much easier and quicker.

Inside a terminal, runs a command-line interpreter that is called a shell. The airport is your way of interacting with the shell via a GUI.

Debian supports a long list of terminal software. This includes the Aterm and the GNOME terminal, the Kterm, the Mate Terminal, the Rxvt, the Xterm, and the Pvt.

This book will use the GNOME terminal because of its stability, simplicity, and adjustability. For example, to increase and decrease the content size that is displayed inside the terminal window, use the two-key combinations CTRL+ and CTRL-.

The shell reads your commands, modifies them under certain conditions, and executes the result.

The table below displays the available special characters:

![Image](Images/image00138.gif)

Purely for interest, the shell divides the command-line into single words to determine the commands, through the following process:

![Image](Images/image00139.gif)

In steps 1 and 2, tagging happens for steps 5 to 7 only, and no further action occurs. Steps 5 to 7 are executed if tagging is completed. Next, the shell removes all the special characters. In step 10, the command line contains only the arguments needed to achieve the command. The shell interprets the first word as the name of the order to be executed, and the remaining terms are its arguments:

command arg1 arg2 arg3 …

**Available Shells**

Your Linux system allows the usage of various shells. Each shell is available as a separate software package through the Debian package manager, Aptitude, and we installed earlier. The list of shells is quite long, so we list only a selection of the available shells that are the most popular:

*   Almquist Shell (ash)
*   Bourne Again Shell (Bash)
*   Debian Almquist Shell (dash)
*   Z Shell (zsh)
*   C Shell (csh)
*   Korn Shell (ksh)
*   Tenex C Shell (tcsh)

At the time of writing, this is the default shell on Debian.

Which other shells are allowed in your Linux system are set up in the configuration file /etc/shells. Using the cat command, you can see the list of allowed shells. For now, know that the command simply outputs the contents of a file to the screen.

$ cat /etc/shells

# /etc/shells: valid login shells

/bin/sh

/bin/dash

/bin/bash

/bin/rbash

/usr/bin/screen

$

The name of the shell that is currently in use in the terminal is kept in the shell variable named $0\. The following simple command outputs the shell’s name:

$ echo $0

bash

$

**Shell Scripting**

At first glance, a shell script may sound daunting, but it is pretty straightforward. In the simplest form, it is just a sequence of UNIX/Linux commands stored in a file and executed line-by-line by the command line interpreter. A shell script is similar to single typing commands in the terminal but is performed as a batch. This makes it much faster and helps to automate tasks. We will not be delving into the programming intricacies of shell scripting for this guide. But it is worth noting the recommended structure of a shell script.

*   Shebang line: defines which program will be used to process

the instructions that follow the shebang line properly. The line

starts with a #! a two-byte number indicating that the following

lines are an executable shell script. The shebang is followed by the

path to the interpreter or program to process the instructions.

*   Docstring: a short description of what the script does and the

software license of the code. This can be a single line but also an

extensive description. Such lines start with a # and are treated as

comments by the shell.

*   Commands: the combination of single commands to be exe

cuted by the shell. As mentioned, this can be as little as a one-line

instruction, such as what we have in our example below, to a ful

ly-fledged program.

*   Exit state: defines the script’s return value(s). Unless explicitly

stated otherwise, the exit state of the last command executed in

the script will be returned. For example, it is common to return 0

on success and a value between 1 and 255 in the event of an error.

The following basic script contains all the single elements we mentioned above. The purpose of the script is to determine the uptime of the computer.

#!/bin/bash

# determine the uptime of the system

# Released under GNU Public License (GPL)

uptime

# define exit state: no error

exit 0

There are two ways to execute a shell script. We can either call a shell such as Bash to run it or set the executable flag for the script and run it afterward. The first option uses Bash and looks as follows:

$ bash uptime.sh

12:20:31 up 7 days, 2:09, 6 users, load average: 0,74, 0,40, 0,27

$

The second method is based on two steps. First, we set the executable flag for the script using the chmod command as follows:

$ chmod u+x uptime.sh

$

Then we can run the script:

$ ./uptime.sh

12:26:07 up 7 days, 2:14, 6 users, load average: 0,23, 0,34, 0

,28

$

**About the Shell**

The shell or shell interpreter is a program that allows users to interact with the system, processing the orders indicated. Commands invoked from the shell can be classified as internal (they actually correspond to orders interpreted by the shell itself) and external (they correspond to executable files external to the shell). In addition to commands, shells offer other elements to improve their functionality, such as variables, functions, or control structures. The set of internal commands and available elements, as well as their syntax, will depend on the specific shell used.

**Users**

In addition to using the shell from the command line (based on the prompt as the indication of the shell to announce that it expects a user order), it can be used to interpret shell scripts. A shell script or “command script” is a text file that contains a set of commands and commands interpretable by the shell.

The shell is an executable file that must interpret the commands, transmit them to the system, and yield the result. There are several shells. The most common is sh (called Bourne shell), bash (Bourne again shell), csh (C Shell), Tcsh (Tenex C shell), ksh (Korn shell), and zsh (Zero shell). Generally, their names match the name of the executable.

Each user has a default shell, which will be activated when a command prompt is opened. The default shell is specified in the configuration file /etc/passwd in the last field of the line that corresponds to the user. It is possible to change shell during a session. For this, you only have to execute the corresponding executable file, for example:

/bin/bash

**System Indicator**

The shell starts when reading its complete configuration (in a file in the / etc / directory) and then reading the user’s own configuration (in a hidden file whose name begins with a period and is located in the user’s basic directory, that is /home/user_name/.configuration_file). Then the following indicator appears:

team: /directory/current $

By default, for most shells, the indicator consists of the name of the computer, followed by a colon (:), the current directory, and then a character indicating the type of user connected:

$ specifies a normal user;

# specifies the administrator, called root.

**The Command Line Concept**

A command line is a string of characters formed by a command that corresponds to an executable file of the system or, rather, a shell command as well as optional arguments (parameters):

ls -al /home/jf/

The arguments that start with - are called options. Usually, for each command, there are a certain number of options that can be detailed when entering one of the following commands:

command —help command -? man command

**Redirects**

Like any Unix system, Linux has mechanisms that allow redirecting standard input-output to files. Therefore, if the> character is used, the standard output of a command on the left can be redirected to a file on the right:

ls -al /home/jf/ > toto.txt echo “Toto” > /etc/myconfigurationfile

The following command is equivalent to a copy of the files:

cat toto> toto2

The purpose of redirection> is to create a new file. If a file already exists with the same name, it must be deleted. The following command simply creates an empty file:

>file

Using the double character >> allows you to add the standard output to the file, that is, it allows you to add the output after the file without deleting it.

Similarly, the <character indicates a redirection of the standard input. The following command sends the contents of the toto.txt file with the cat command, whose sole purpose is to display the content in the standard output (the example is not useful, but it is instructive):

cat<toto.txt

Finally, the use of the redirection << allows reading, in the standard input, until the chain located to the right is found. In the following example, the standard input is read until the word STOP is found. Then, the result is displayed:

cat<<STOP

**Communication Pipes**

Pipes are specific communication mechanisms for all UNIX systems. A pipe, symbolized by a vertical bar (character |), allows you to assign the standard output of one command to the standard input of another, in the same way that a pipe allows communication between the standard input of a command and the standard output of other.

In the following example, the standard output of the ls -al command is sent to the sort program, which must extract the result in alphabetical order:

ls -al | sort

This allows connecting a certain amount of commands through successive pipes. In the following example, the command will show all files in the current directory, select the lines that contain the zip element (using the grep command), and count the total number of lines:

ls -l | grep zip | wc –l

**Shell Script in Linux**

**Invocation**

In its most basic form, a shell script can be a simple text file that contains one or more commands. To help identify the content from the file name, it is common for shell scripts to have the extension “.sh”, so we will follow this criterion (but remember that it is merely informative and optional). For example, the following file would be a shell script:

Script.sh

echo “ Personal folder content:”

ls ~/

Exercises:

1.Verify that the “script.sh” file has general execution permis

sions (if not, it would be sufficient to execute “chmod + x script.

sh”).

2.Invoke the script to be interpreted, using for example the com

mand:

cd ./script.sh

In addition to commands, shell scripts may contain other elements, provided by the shell to improve the functionality of the scripts. In summary, the basic structure of a shell script is as follows:

script_ejemplo.sh

#!/bin/dash

# This is not interpreted

echo Hello

ps w

echo “ Process read the script: $$”

<— Shebang

<— Comments (not interpreted)

<— Script Content

The “shebang” allows you to specify the command interpreter with which you want the rest of the script to be interpreted when implicit invocation is used. The syntax of this line is the sequence #! followed by the executable of the desired shell, on which the following warnings should be made:

It must be the first line of the script, since, otherwise, it would be interpreted as a comment (starts with the # character).

There may be spaces between #! and the shell executable.

The shebang is not mandatory (when implicit invocation is used, if it is not indicated, an attempt will be made to use the same type of shell from which the script was invoked).

The use of the shebang is conditioned by the way the shell script is invoked, there are 3 options:

**Explicit:** explicitly writing which shell you want to invoke and passing the script name as an argument, loading a new process for that shell (subshell or child shell process of the parent shell responsible for the command line from which the script was invoked). In this case, the shebang is ignored.

**Implicit:** invoking the script as if it were an executable, which requires assigning execution permissions to the script. The shebang is read to determine which shell should be used to read the script, loading a child process (subshell) for that shell (if the script does not have shebang, for the subshell the same type of shell will be used as the one in charge of the command line from which the invocation was made). Note that shell scripts are text files read by the command interpreter, that is, they are interpreted. They are NOT executed. The assignment of the execution permission to a shell script is a file system utility to accelerate the invocation of scripts, but its internal function is to load a new shell process (subshell) so that it interprets the script.

**Implicit with. (equivalent to import):** the script will be interpreted by the same shell process responsible for the command line from which the script is being invoked. Consequently, in this case, the shebang is also ignored.

In cases where subshells are created, unless otherwise forced (with su -c for example), the subshell will belong to the same user to which the parent shell that created it belonged. The user to whom the shell process that interprets a script belongs determines the operations that can be done from within the script (for example, if the shell belongs to the user dit, the script cannot modify the file /etc/passwd, while if the shell belongs to the root superuser, yes you can do it). Consider this aspect to determine what operations you can perform within a script, and with which user you should invoke it.

Exercises:

1.In a command console, execute the command ps w and locate

the process associated with the shell responsible for the command

line from which you are working.

2.Invoke that script using the different invocation methods. For

each of them, analyze the output obtained to determine in each

case what is the shell process that is interpreting the script, the

user to which that process belongs and if a subshell has been ope

ned or not:

Explicit:

/bin/sh script_example.sh

/bin/dash script_example.sh

/bin/bash script_example.sh

Implicit with “.”:

. script_example.sh

Implicit: check that the script has execute permission and execute it with:

./script_example.sh

While both bash and dash follow the POSIX standard, especially bash adds multiple particular extensions, not supported by other shells such as dash. Consequently, every time we design a script we must take into account the shell or shells that support it, ensuring that it is invoked by one of them. To get an idea of the importance of this aspect, consider the following two scripts, based on the use of the structure for (to be used later):

script_estandar.sh

#!/bin/sh for VAR in 0 1 2 3

do

echo $VAR

done

script_estandar.sh

#!/bin/bash

for ((VAR=0 ; VAR<4 ; VAR++ ))

do

echo $VAR

done

Both scripts perform the same functionality, but script_estandar.sh is written under the POSIX syntax, while script_bash.sh uses a non-standard syntax supported by bash.

Exercises:

1.Invoke the script script_standar.sh (remember that you must

have them already created in the scripts/directory) using the

following commands, having to verify that they all work correct

ly and with the same result (the first and second calls are the

same, using the shell dash):

/bin/sh script_estandar.sh

/bin/dash script_estandar.sh

/bin/bash script_estandar.sh

2.Now invoke the script script_bash.sh using the following com

mands:

/bin/dash script_bash.sh

/bin/bash script_bash.sh

You can see how, due to the non-standard script syntax, the second invocation works, but the first one (which uses dash) gives a syntax error.

**General Shell Operation**

The shell language is an interpreted language, in which lines of text (ending in \n) are read, analyzed, and processed. The lines to be interpreted are read from:

*   The standard input (default keyboard). In this case, the shell is

said to be an interactive shell.

*   A shell script file.
*   The arguments, with the option when running the shell. Exam

ple: bash –c “ls –l”

With the lines read, the shell performs the following steps (in this order):

1.The lines are divided into different elements: words and ope

rators. The elements are separated using spaces, tabs, and opera

tors. The # character is used to include a comment, which is re

moved from the processing.

2.A distinction is made between simple commands, compound

commands, and function definitions.

3.Different expansions and substitutions are made. The com

mand to be executed and the arguments to be passed are detected.

4.Inbound /outbound redirects are performed and items asso

ciated with redirects are removed from the argument list.

**Using the Shell**

It’s impossible to be an effective Linux professional without knowing how to use the command line.

A shell prompt signifies that the system is ready to take a user command. This is referred to as a user-system dialogue. For each command entered, the user receives a response from the system:

1.Another invitation, indicating that the command has been

carried out and that you may go to the next step.

2.An error message is a statement from the system to the user

regarding happenings in the system.

Users who are accustomed to dealing with systems that have a graphical interface may find working with the command line cumbersome. This form of interface, on the other hand, has always been basic in Linux and hence extensively developed. There are many techniques to save effort, that is, keystrokes when completing the most common activities in the Linux command shells:

*   Automatic addition of long command names or file names
*   Searching and re-executing a command that was once perfor

med before

*   Substitution of file name lists by some pattern, and much more

When you need to conduct comparable operations on a variety of objects, the command line’s advantages become clear. In a graphical interface system, you’ll need as many mice dragging as there are items; on the command line, one command will suffice.

**Shells**

A command shell, sometimes known as a command interpreter, is software that sends your commands to the operating system and application programs, as well as receiving their responses. Scripts are short programs written in the command shell language that conduct a series of consecutive operations with files and the data they contain.

You will see a command line prompt—a line ending in $—after you have registered in the system by entering a username and password. This symbol will be used to represent the command line in the future. You can go to the command line on any virtual text console if a graphical user interface was specified to start at system boot during the installation. You may do this by pressing Ctrl-Alt-F1 - Ctrl-Alt-F6 or by using a terminal emulator program like xterm.

The shells listed below are available. Depending on the distributor, they may differ:

bash

The most popular Linux shell. It can add to the names of commands and files, preserves a command history, and allows you to alter them.

pdkdh

On UNIX shell platforms, the korn shell clone is well-known.

sash

This shell is unique in that it does not rely on any shared libraries and provides simpler versions of several of the most often used utilities, such as al, dd, and gzip. As a result, the sash comes in handy when it comes to recovering from system crashes or updating the versions of the most crucial shared libraries.

tcsh

Improved version of C shell.

zsh

This is the most recent shell on the list. It has advanced capabilities such as command argument autocompletion and a slew of other features that make working with the shell even more convenient and efficient. However, because all zsh extensions are disabled by default, you must study the documentation and enable the capabilities that you require before using this command shell.

Bash Bourne Again Shell is the default shell. Use the command echo $ SHELL to see which shell you’re using.

Shells differ not only in terms of capability but also in terms of command syntax. If you are a new user, we recommend that you start with bash; further examples demonstrate the work in this area.

**Bash Shell**

The command line in bash consists of the command’s name followed by keys (options), which are instructions that change the program’s behavior. Keys usually start with the character —or—and consist of just one letter. After the command, arguments (parameters)—the names of the objects on which the command must be executed—can be added (often the names of files and directories).

After pressing the Enter key to finish entering a command, the command is sent to the shell for execution. There may emerge notifications concerning the command execution or failures as a result of the command execution on the user’s terminal, and the arrival of the next command line prompt (ending with the $ character) signals that the command has completed and you can input the next one.

In bash, various strategies make typing and editing the command line easier. You can, for example, use the keyboard to:

Ctrl-A: go to the beginning of the line. The same can be done by pressing the Home key;

Ctrl-u: delete current line;

Ctrl-C: abort the current command’s execution.

To identify a specific command among those that have previously been run without having to go through the entire story, press Ctrl-R and enter a term that was used in the command you’re looking for.

Commands that appear in history are numbered. To run a specific command, type:

! command number

If you participate !! , the command you just typed begins.

On Linux, application and command names might be too long at times. Fortunately, bash can finish the names for you. You can complete the name of a command, program, or directory by using the Tab key. Let’s say you wish to utilize the bunzip2 decompression application as an example. To do so, start typing:

bu

Then press the Tab key. If nothing happens, there are a few other possibilities for finishing the instruction. By pressing the Tab key once again, you’ll get a list of names that begin with the letter bu. The system, for example, includes the following programs: buildhash, builtin, and bunzip2:

$ bu

buildhash builtin bunzip2

$ bu

Press Tab after typing n> (bunzip is the only name with the letter n as the third letter). The shell will complete the name for you, and all you have to do now is hit Enter to execute the command!

Bash searches folders defined in the PATH system variable for programs invoked from the command line. By default, the current directory, denoted by ./, is not included in this directory listing (dot slash). As a result, you must use the command ./prog to launch the prog program from the current directory.

**Basic Commands**

Working with data (typically stored in files) and managing programs (processes) operating on the system are the primary activities that must be completed in any system. The commands listed below allow you to conduct the most common tasks while working with files and processes. Only the first, cd, is included in the shell itself; the others are supplied separately but are always available on every Linux system. All of the commands listed below can be used in both text and graphical mode (xterm, KDE console). Use the man command to learn more about each command, for example:

man ls

cd

Allows you to change the current directory (travel through the file system) (navigate through the file system). It works with both absolute and relative paths. Let’s say you’re in your home directory and wish to access the tmp / subdirectory. To do so, type in the following relative path:

cd tmp /

To change to the / usr / bin directory, type (absolute path):

cd / usr / bin /

Some options for using the command are:

cd ..

Allows you to make the current parent directory (note the space between cd and ..).

cd -

With no parameters, the cd command returns the shell to the home directory.

ls

ls (list) lists the files in the current directory. Two main options: -a—view all files, including hidden, -l—display more detailed information.

rm

This command is used to delete files. Warning: deleting the file, you cannot restore it! Syntax: rm filename.

This program has several parameters. The most frequently used ones are: -i—file deletion request, -r—recursive deletion (i.e., deletion, including subdirectories and hidden files). Example:

rm -i ~ / html / *. html

Removes all .html files in your html directory.

mkdir, rmdir

The mkdir command allows you to create a directory, while rmdir deletes a directory, provided it is empty. Syntax:

mkdir dir_name

rmdir dir_name

The rmdir command is frequently superseded with the rm -rf command, which deletes directories even if they are not empty.

less

less allows you to page by page. Syntax:

less filename

grep

This command allows you to search the file for a certain string of characters. Please keep in mind that grep searches use a regular expression, which means you can specify a template for searching a complete group of terms at once. Regular expressions allow you to create patterns that describe string classes such as “four digits in a row, surrounded by spaces” and “four digits in a row, surrounded by spaces.” Obviously, such an expression may be used to find all the years written in numbers in the text. Regular expressions have a wide range of search capabilities. You can get additional information about grep in the on-screen documentation (man grep). Syntax:

grep search_file

ps

Shows a list of active processes. The process name is shown in the command column, and the PID (process identifier) is the process number (which is needed for activities with the process, such as sending signals with the kill command). Syntax:

arguments ps

Argument u provides extra information, while ax allows you to observe processes that are not yours.

kill

If the program stops responding or hangs, use this command to complete it. Syntax:

kill PID_number

The PID number refers to the process identification number. The ps command can be used to get the process number for each executable application. The kill command normally delivers a regular completion signal to the process, however, it may not function in some cases, in which case you must use kill -9 PID number. The system will immediately end the command in this scenario, with no chance of saving data (abnormal). The command kill -l can be used to get a list of the signals that the kill command can deliver to a process.

# Command-Lines

**The Bash Shell**

The command-line utility available on Linux operating systems is known as BASH, which is short for Bourne-Again Shell. The command-line utility is basically an interface, which allows you to give instructions in text mode to the computer and its operating system. There are different types of shell interfaces that are available in the many Unix0-ike systems that have been developed over the years, but Red Hat Enterprise Linux 7 uses the bash shell. The bash shell is an evolved and improved version of the former popular shell known as Bourne Shell.

The bash shell displays a string, which implies that it is waiting for a command to be input by the user. This string that you see is called the shell prompt. For a user that is not a root user, the shell prompt ends with a $ symbol.

[student@desktop ~]$

If the root user is logged into the system, the shell prompt ends with a # symbol. The change in this symbol quickly lets the user know if he is logged in as a root or a regular user so that mistakes and accidents can be avoided.

[root@desktop ~]#

If you need an easy comparison, the bash shell in Linux operating systems is similar to the command prompt utility that is available in Windows operating systems, but you can say that the scripting language used in bash is far more sophisticated compared to the scripting that can be done in command prompt. Bash is also comparable to the power shell utility, which was made available from Windows 7 and Windows Server 2008 R2\. The bash shell has been called a very powerful tool for administration by many professionals. You can automate a lot of tasks on your Linux system using the scripting language that is provided by the bash shell. Additionally, the bash shell also has the option to perform many other tasks, which are complicated or even impossible if tried via a graphical interface.

The bash shell is accessed through a tool known as the terminal. The input to the terminal is your keyboard and the output device is your display monitor. Linux operating systems also provide something known as virtual consoles, which can be used to access the bash shell as well. So, you will have multiple virtual consoles on the base physical console and each virtual console can act as a separate terminal. Also, you can use each virtual console to create login sessions for different users.

**Basics of Shell**

There are three parts to commands that are entered on the shell prompt:

1.  Command that you want to run
2.  Options that will define the behavior of the command
3.  Arguments, which are the command’s targets

The command basically defines the program that you want to execute. The options that follow the command can be none, one, or more. The options govern the behavior of the command and define what the command will do. Options are usually used with one hyphen or two hyphens. This is done so that we can differentiate options from arguments. Example: -a or —all

Arguments also follow the command on the command line and can be one or more like options. Arguments indicate the target on which a command is supposed to operate.

Let us take an example command:

usermod -L John

The command in this example is usermod

The option is -L

The argument is John

What this command does is lock the password of the user John on

the system.

To be effective with the commands on the command line, a user needs to know what options can be used with a particular command. If you run the —help option with any command, you will get a set of options, which can be passed with that particular command. So, it’s not really necessary that you know by heart all the options that will be used by all the commands. The list will also tell you what each option does.

The use of statements can sometimes seem very difficult and complicated to read. Once you get used to certain conventions, reading the statement becomes much easier.

*   Options are surrounded by square brackets [ ]
*   If a command is followed by … it specifies the arbitrary length

list of items belonging to that type

*   If there are multiple items and if the pipe separates them | it

implies that you can specify only one of them

*   Variables are represented using text, which is in angle brackets

<>. So if you see <filename>, you have to replace it with the file

name that you wish to pass

For example, check the below command:

[student@desktop ~]$ date —help

date [OPTION]… [+FORMAT]

This indicates that the command date takes the options represented by [OPTION]… with another option [FORMAT], which will be prefixed with the + symbol.

**Executing Commands on the Bash Shell**

The Bourne Again Shell, known as bash, does the job of interpreting commands that are input by the user on the shell prompt. We have already learned how the string that you type in a shell prompt is divided into three parts, command, options, and arguments. Every word that you type into the shell is separated using blank space. The program that is already installed on the system is defined by every command that you type, and every command has options and arguments that are associated with it.

When you have typed a command on the shell prompt along with the options and arguments and are ready to run it, you can press the Enter key on the keyboard, which will execute that command. If you wish to type more than one command on a single line, you can use a semicolon to separate the commands.

Let us go through some simple commands that are used on a daily routine on the command line in Red Hat Enterprise Linux 7 and other Linux-based operating systems.

The date command will display the current date and time of the system. You can also use this command to set the time of the system. If you are passing an argument with the + sign for the date command, it indicates the format in which you want the date to be displayed on the output.

[student@desktop ~]$ date

Sat Aug 5 08:15:30 GMT 2019

[student@desktop ~]$ date +%R

08:15

[student@desktop ~]$ date +%x

08/05/2019

The passwd command can be used to change the password of a user. You will, however, need to specify the original password for the given user before you can set a new password. The command requires you to specify a strong password, which makes it necessary to include letters belonging to lowercase and uppercase, numbers, and symbols. You also need to ensure that the password being specified is not a word in the dictionary. The root user has the option to change the password of any other user on the system.

[student@desktop ~]$ passwd

Changing password for user student.

Changing password for student.

(current) UNIX password: type old password here:

New password: Specify the new password here

Retype new password: Type the new password again

passwd: all authentication tokens updated successfully.

File types and extensions are not specified in a Linux operating system. The file command can scan any file and tell you the kind of file it is. The file you want to classify needs to be passed as an argument to the file command.

[student@desktop ~]$ file /etc/passwd

/etc/passwd: ASCII text

If you are passing a folder/directory as an argument to the file command, it will tell you that it is a directory.

[student@desktop ~]$ file /home

/home: directory

The next set of commands is head and tail, which print the first ten lines and the last ten lines of a file respectively. Both these commands can be combined with the option -n, which can be used to specify the number of lines that you want to be displayed.

[student@desktop ~]$ head /etc/passwd

This will print the first 10 lines that are there in the passwd file.

[student@desktop ~]$ tail - n /etc/passwd

This will print the last 3 lines that are there in the passwd file.

The wc command is used to count lines, words, and characters in a file that is passed as an argument. It supports options such as -l, -w, -c, which stand for lines, words, and characters respectively.

[student@desktop ~]$ wc /etc/passwd

30 75 2009 /etc/passwd

This shows that there are 30 lines, 75 words, and 2009 characters in the file passwd.

If you pass the -l, -c, -w options along with the wc command, it will only display the count of lines, words, or characters based on which option you have passed.

You can use the ! mark along with the command number to expand what was typed in that command along with the output.

[student@desktop ~]$ history

1 clear

2 who

3 pwd

[student@desktop ~]$ !3

/home/student

This shows that we used !3 to expand the pwd command, which shows the present working directory for which the output was /home/student, which was the home directory of the student user.

You can use the arrow keys to navigate through the output given by the history command. Up Arrow will take you to the commands on top and Down Arrow will take you to the commands below. Using the Right Arrow and the Left Arrow keys, you can move around in the current command and edit it.

**Shortcuts to Edit the Command Line**

There is an editing feature available on the command line in bash when you are interacting with bash. This helps you to move around the current command that you are typing so that you can make edits. We have already seen how we can use the arrow keys with the history command to move through commands. The following list will help you use edits when you are working on a particular command.

Ctrl+a: This will take your cursor to the start of the command line

Ctrl+e: This will take your cursor to the end of the command line

Ctrl+u: Clear the line from where the cursor is to the start of the

command line

Ctrl+k: Clear the line from where the cursor is to the end of the

command line

Ctrl+Right Arrow: Take the cursor to the start of the next word

Ctrl+r: Search for patterns in the history list of commands used

# Shell Scripting

**Shell Scripting**

The shell is a command interpreter in an operating system like Unix or GNU.

Linux is a program that uses other programs. It provides a computer user interface to the Unix/GNU Linux system to use different commands or resources/tools with specific installation details. When the shell has finished making the program, it sends the output to the user on the screen, a standard output device. The shell is more than just interpreting a command. Its system’s language has a complete language structure such as conditional performance, constraints, flexibility, tasks, and much more. That is why the Unix/GNU Linux shell is more powerful than the Windows shell.

Now, we may take a look at some of the most widely used open-source shells in Unix/GNU Linux.

**Bash Shell**

Bash represents Bourne Again Shell and is the default shell in most Linux distributions today. It also has a sh-associated shell and provides more efficient development over sh of the system and use that includes:

*   Editing the command line
*   Performance Management
*   Unlimited size command history
*   Shell Services & Nicknames
*   Unlimited size approximate layout
*   Integer arithmetic on any basis from two to sixty-four

**Tcsh / Csh shell**

Tcsh developed with C-shell, can be used as a compatible login shell and Shell script command processor.

Tcsh has the following features:

*   C as syntax
*   Command-line editor
*   Word and word file completion
*   Spelling correction
*   Performance management

**The Shell of Zsh**

Zsh is designed to work with and integrate many other Unix/GNU Linux shells, such as bash, tcsh, and Ksh.

And a strong writing language like other shells available. Although it has some unique features that include:

*   File name generation
*   Getting started files
*   Login / login
*   Concluding ideas
*   Conceptual guide
*   Flexible index

**The Fish**

The fish is in full swing “friendly interactive shell” and was recorded in 2005\. It was designed to be fully functional and easy to use, like other shells, with excellent features including:

*   Completion of personal page
*   Web-based configuration
*   Automatic suggestions
*   Can be written entirely in clean scripts
*   Term256 technology terminal support

**Advantages of Using Linux**

Most computer novices say things like “Linux is complicated,” or “Linux is a gееk thing.” If there are, of course, Linux distributions that only passionate experts can operate, there are also some that are intended explicitly for the general public: Linux Mint, Ubuntu, and its derivatives.

You will discover that GNU/Linux is straightforward to use and much more user-frіеndly than most people think.

**Hands-on Your Stееring Whееl**

With this software, you are the master of the board. GNU/Linux will do absolutely nothing unless you ask it explicitly, unlike a proprietary system that decides nearly everything instead of the user.

You’re not mandated to install what you do not want to install, nor will a completely new system be imposed on you while the one you paid is still working very well. Conversely, you will probably not have anything to uninstall from the start; no antivirus trial for a month, no key, and no locks, in short, no bloatware.

After years of relying on Windows, the freedom that Linux grants can be scary. However, it should be understood that GNU/Linux allows you to manipulate your operating system to make it a space arranged to your taste, your needs, as much as it gives you the right to do anything at all.

**Security**

There is no need for antivirus when you are on Linux. This seems inconvincible, but it is true because this operating system is built primarily to be as safe as possible. It is part of the DNA of Unіx-lіkе systems (Linux, BSD) where security is such an essential еlеmеnt as other components of the system.

Despite this claim, most computer operators have tried to explain the security build-up of Linux. On the one hand, some operators suggest that there are viruses on Linux, and therefore, it is crucial to protect yourself. The others argue that this antivirus only detects those intended for Windows. Moreover, the Linux world’s diversity means that a virus that affects one distribution may not affect the other.

The most common security requirement for a Linux system is that a password is requested as soon as you log in or when you want to perform a potentially dangerous system modification operation (update, installation of new software, etc.). The password will also be required when you want to access some files, as this will prevent some people from searching your data when you’re not around.

As far as updates are concerned, they seem much less frequent and, in most cases, much faster to perform. We sometimes hear that Windows was designed for one thing: to work. Initially, security was not even a primary concern, an aspect so little taken into consideration that it was delegated to third-party software.

Hence, the very lucrative industry of antivirus and antimalware. Even if one can argue that, nowadays, Microsoft takes a grave account of security problems. The continuous and frequent flow of security updates should encourage all users to ask serious questions about the Microsoft operating system’s reliability.

**Serenity and Efficiency**

Even though some distributions are complicated, some GNU/Linux distributions are very suitable for beginners. Everything is, therefore, designed to make life easier for beginners. This means that you will not need a master’s degree in computer science to operate Linux. Moreover, GNU/Linux offers a reliable environment, technically and humanly.

When you’re done installing a distribution for the first time, the most striking thing about it is its barebones look. Usually, only two icons are present on the desktop: the “workstation” and a personal folder. Not even the trash! It may seem austere, but it is also the symbol of the GNU/Linux experience: simplicity and the choice to add things according to your needs.

This simplicity is immediately visible when you go around the interface. Unlike Windows, most people who have not yet mastered the system waste time uninstalling useless software and disabling imposed functions; under GNU/Linux, you don’t have to do this. No need to uninstall a useless bunch of software. Instead, you choose the software to add yourself.

Precisely, nothing is more accessible than installing software chosen among the thousands available in a software library. Do not surf the net for the desired application that could just as easily contain a virus or corrupt files in your system.

The most eloquent feature of GNU/Linux is that no restart is necessary after installing the software. This is so for updates that are operational instantly without rebooting the system.

**Bash Features**

Bash, which is the default GNU shell on most Linux systems that you will use, will make it easier to use specific combinations of keys to perform a task easily and quickly. Some features of the Bash shell are:

Tab: this will complete the command or the filename. If there is more than an option, the system will use a visual or audio notification to tell you. If the system detects a lot of possibilities, it will ask you whether you would like to check all of them.

Tab: this is going to show the completion possibilities for a filename or command.

Ctrl + A: will move the cursor over to the start of the current com

mand line.

Ctrl + C: this one will end your computer program and then show

the Linux prompt.

Ctrl + D: this one is going to log you out of your current session.

This is a key combination that is similar to typing exit or logout.

Ctrl + E: This will move the cursor to the end of your current com

mand line.

Ctrl + H: this is going to work similarly to pressing the backspace

key on the keyboard.

Ctrl + L: this one is going to clear out the current terminal.

Ctrl + R: this is going to search through the history of commands

Ctrl + Z: this is going to allow you to suspend your computer.

**Programs**

**Arrow right/arrow left:** these keys will make it easier to move the cursor along the command line that you are currently on. You may find it useful to add in more characters or make some changes to the program.

**Arrow up/arrow down:** these are the keys that will make it easier to browse the system’s history. You can access any lines that you want to repeat, change some of the data when needed, and then press Enter to quickly execute these new commands.

**Shift + Page Up/Shift + Page Down:** using these key combinations will allow you to check the terminal buffer.

As you get a bit more familiar with the Linux system, you will begin to understand better how these commands work and learn other commands, which will make it easier to use the Linux system. These are just a few of the initial commands that you should learn how to use because they will make navigating through the system much easier for you. Give them a try and practice logging in and out of your system so that you can get a feel for how it works before moving on.

**A New Version in a Snap of Fingers**

On Linux, if you want to change the version, for example, to have a most recent operating system, most distributions are to be reinstalled in full. Under Windows, this operation causes stress and takes a lot of time. To change the GNU/Linux version is so easy that it can quickly become a routine.

To perform this in Linux Mint, go to the update manager to install the latest version available. It is worth noticing that installing a recent version does not mean changing the whole software. GNU/Linux offers operating systems light enough to run on computers with less than 4 GB of RAM.

Generally, consider that with the present Linux distribution, an entry-level computer with 4 GB of RAM is almost oversized for everyday uses. The minimum system recommended for installing Linux Mint is 9 GB of disk space and 256 MB of RAM (1GB for comfort). Obviously, some software will probably require a little more than 1 GB of RAM. But between 1 and 4 (or 8 GB of RAM), space is enough.

The different versions of the distributions are often proposed in “long cycles,” commonly called LTS (Long Term Support). For example, Linux Mint 18 available since spring 2016 will be supported until spring 2021\. For the rest, if you know how to copy and paste, you will reinstall your software and replace it with the recent versions. Above all, it is possible to restore all the software configuration of the old system, which includes, for example, your email, your settings, as well as the complete parameters of your browser with extensions included.

How is this magic possible? The advantage of a GNU/Linux distribution is that all the personal files are deposited in a single named folder. This folder also contains hidden directories, and these are the ones that contain all the settings of your software. GNU/Linux does not violate the user.

GNU/Linux is an operating system that does not exploit you. The default installation does not include much more than the most commonly used and fully functional software. The Linux community and free software developers do not care what you do with your computer for which you are solely responsible.

A GNU/Linux distribution does not hint, analyze, or transmit any of your actions to “third parties,” which may breach users’ privacy.

**Linux Tips and Tricks**

There are thousands of command lines, which makes it possible to execute tasks in no time. Rather than flipping through pages one after the other, a single command can help you get what you want in a few seconds.

On Linux, you must note that some Windows shortcut keys may perform different functions entirely. Hence, don’t expect Ctrl + S to help you save items on Linux.

ls

This command is used to list the files in a folder. You can use “afor” to list hidden files, “-lfor” detailed list, and “Rallows” to view subfolfilename change directory; the command is used to navigate within the existing file system. For example, cd /var/loggo to the logs folder. This is effective regardless of where you are since we put the start slash, which indicates that it is an absolute address.

pwd

Print working directory. This command displays the absolute path of the folder you’re presently in.

Clear

This is used to clean your terminal window, relegating all the text above, and leaving you with a clean window. The keyboard shortcut Ctrl+ l does the same thing.

Ctrl + s

Stop the display; this is very useful when you mistakenly input a wrong command.

# Conclusion

To conclude, you have enough basic information to get started and begin to dabble in the usage of your own Linux distribution that you have chosen, installed, and begun to program. Hopefully, you found the process of reading informative and valuable to you as you made your way through it.

As a beginner, you should familiarize yourself with the Linux commands. This is the most exciting thing with Linux.

One enjoys running the commands on the terminal, which gives different results. The exciting thing with Linux is that it comes with various distributions, and the majority of the commands are universal in all of these distributions. This provides one with ease of transition from one transition to another.

However, it is good for you to know that each Linux distribution is developed for a group of targeted users, and it is designed and developed so that it can meet the demands of those users. This calls for you to determine the tasks you want to perform with your Linux and then choose the best distribution! For sure, however, when you begin to utilize Linux, you are developing a series of essential skills to learning.

It can be beneficial to know how to work with computers. You may even decide to take this from a project to a hobby and eventually even a career if it has interested you enough to keep exploring. First, however, no matter what is important to remember, you should make sure you stay up-to-date on your knowledge. From here, you may be ready to install your iteration of Linux if you have not done so yet.

It is exciting when you begin this process, and you will surely enjoy it.

If you are unsure whether you are ready to take the plunge into downloading a distribution for yourself, maybe you would find interest in running a few different distros to test first, using the steps listed for you earlier.

You can play around with the system, learning which you prefer and which you would rather avoid altogether, which may help you make your decision sooner. However, no matter what you decide, remember that this was an introduction to the subject.

This reading focused on providing you with the essentials to understanding what Linux is and how it works. From here, you may choose to research the specialized distribution you are interested in. You may begin to look into Linux’s uses and what you can do with the program.

No matter what you choose to do next, if you are willing to put in the time and energy, you will find yourself successful in your endeavors.

I wish you the best of luck!