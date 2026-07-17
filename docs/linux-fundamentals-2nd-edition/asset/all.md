![](images/9781284254891_FChigh.jpg)

![The title of the book reads Linux Fundamentals, second edition. Author: Richard Blum. A splash of yellow liquid is shown on the page. The name of the publisher in landscape on the left reads Jones and Bartlett Learning.](images/9781284254891_FChigh.jpg)

![The Jones and Bartlett Learning logo features a lighthouse.](images/pub.jpg)
*World Headquarters*
Jones & Bartlett Learning
25 Mall Road
Burlington, MA 01803
978-443-5000
[info@jblearning.com](mailto:info@jblearning.com)
[www.jblearning.com](http://www.jblearning.com)

Jones & Bartlett Learning books and products are available through most bookstores and online booksellers. To contact Jones & Bartlett Learning directly, call 800-832-0034, fax 978-443-8000, or visit our website, [www.jblearning.com](http://www.jblearning.com).

Substantial discounts on bulk quantities of Jones & Bartlett Learning publications are available to corporations, professional associations, and other qualified organizations. For details and specific discount information, contact the special sales department at Jones & Bartlett Learning via the above contact information or send an email to [specialsales@jblearning.com](mailto:specialsales@jblearning.com).

Copyright © 2023 by Jones & Bartlett Learning, LLC, an Ascend Learning Company

All rights reserved. No part of the material protected by this copyright may be reproduced or utilized in any form, electronic or mechanical, including photocopying, recording, or by any information storage and retrieval system, without written permission from the copyright owner.

The content, statements, views, and opinions herein are the sole expression of the respective authors and not that of Jones & Bartlett Learning, LLC. Reference herein to any specific commercial product, process, or service by trade name, trademark, manufacturer, or otherwise does not constitute or imply its endorsement or recommendation by Jones & Bartlett Learning, LLC and such reference shall not be used for advertising or product endorsement purposes. All trademarks displayed are the trademarks of the parties noted herein. Linux Fundamentals, Second Edition is an independent publication and has not been authorized, sponsored, or otherwise approved by the owners of the trademarks or service marks referenced in this product.

There may be images in this book that feature models; these models do not necessarily endorse, represent, or participate in the activities represented in the images. Any screenshots in this product are for educational and instructive purposes only. Any individuals and scenarios featured in the case studies throughout this product may be real or fictitious but are used for instructional purposes only.

25580-5

Production Credits

Vice President, Product Management: Marisa R. Urbano

Vice President, Content Strategy and Implementation: Christine Emerton

Director, Content Management: Donna Gridley

Manager, Content Strategy: Carolyn Pershouse

Technical Editor: Ric Messier

Content Strategist: Melissa Duffy

Content Coordinator: Mark Restuccia

Director, Project Management and Content Services: Karen Scott

Manager, Project Management: Jackie Reynen

Project Manager: Dan Stone

Senior Digital Project Specialist: Angela Dooley

Marketing Manager: Mark Adamiak

Content Services Manager: Colleen Lamy

VP, Manufacturing and Inventory Control: Therese Connell

Product Fulfillment Manager: Wendy Kilborn

Composition: Straive

Project Management: Straive

Cover Design: Briana Yates

Text Design: Kristin E. Parker

Media Development Editor: Faith Brosnan

Rights & Permissions Manager: John Rusk

Rights Specialist: James Fortney

Cover Image (Title Page, Part Opener, Chapter Opener): © Picsfive/Shutterstock

Printing and Binding: Gasch Printing

Library of Congress Cataloging-in-Publication Data

Names: Blum, Richard, 1962- author.

Title: Linux fundamentals / Richard Blum.

Description: Second edition. | Burlington, Massachusetts : Jones & Bartlett Learning, [2023] | Includes bibliographical references and index.

Identifiers: LCCN 2022023562 | ISBN 9781284254884 (paperback)

Subjects: LCSH: Linux. | Operating systems (Computers)

Classification: LCC QA76.774.L46 B66 2023 | DDC 005.4/46--dc23/eng/20220714

LC record available at [https://lccn.loc.gov/2022023562](https://lccn.loc.gov/2022023562)

6048

Printed in the United States of America

26 25 24 23 22 10 9 8 7 6 5 4 3 2 1

To all the teachers, coworkers, students, friends, and Internet posters who continue to teach me new things every day.

“An intelligent heart acquires knowledge, and the ear of the wise seeks knowledge.” Proverbs 18:15 (ESV)

![An abstract image shows a texture in the form of smoke.](images/FM-opener.jpg)

© Picsfive/Shutterstock

# Preface

The Linux world is constantly changing, requiring new knowledge and skills to work as a Linux system administrator. This second edition of *Linux Fundamentals* not only updates the first edition with new material, but also changes the book’s focus a bit, from a basic approach to Linux to a more advanced server-oriented look at using Linux. While the first edition tracked the skills needed to meet the LPI Linux Fundamentals exam requirements, this edition tracks the more advanced CompTIA Linux+ exam requirements.

The CompTIA Linux+ exam is oriented toward having the skills needed to work as a Linux system administrator in a commercial Linux server environment. Thus, this edition dives deeper into the Linux server environment, covering the commands you are expected to know for the Linux+ exam. In the examples I use both Red Hat and Debian-based Linux distributions so you will have experience working in both of those Linux server environments.

The updated chapters provide expanded coverage on how to manage users, files, devices, and filesystems in a multi-user networked server environment. In these dangerous times, nothing is more important than having a secure Linux system. This edition adds a new chapter focusing on Linux security. It covers the popular SELinux and AppArmor tools for implementing mandatory access control to files, as well as providing tips on using encryption and firewalls to keep your data safe both on and off the network.

Finally, this second edition ends with a brief look at the popular topics of virtualization, containers, and orchestration. These have become hot topics in the IT world, and Linux has played an important role in each of these technologies. The final chapter provides an overview of just how to use these technologies in a Linux environment.

![An abstract image shows a texture in the form of smoke.](images/FM-opener.jpg)

© Picsfive/Shutterstock

# Acknowledgments

First, all glory and praise go to God, who through His Son, Jesus Christ, makes all things possible and gives us the gift of eternal life.

Many thanks go to the fantastic team of people at Jones & Bartlett Learning for their outstanding work on this project. Thanks to Ned Hinman for offering me the opportunity to update the first edition of this book, and to Melissa Duffy, the Content Strategist, for her skills in guiding this book through the entire process. It’s been a pleasure working with you and your team! Also, special thanks goes to Ric Messier, fellow Linux author, for taking the time out of his schedule to be the book’s Tech Editor. I am grateful for your excellent suggestions to help make this a better book. I would also like to thank Carole Jelen at Waterside Productions, Inc., for arranging this opportunity for me and helping me out with my writing career.

Finally, I would like to thank my wife Barbara for her patience and the life-sustaining baked goods she prepared to help me keep up my energy while writing!

![An abstract image shows a texture in the form of smoke.](images/FM-opener.jpg)

© Picsfive/Shutterstock

# About the Author

RICHARD BLUM, Linux+ ce, has worked in the IT industry for more than 35 years as both a systems and a network administrator. During that time he’s had the opportunity to work with lots of different computer products, including many different flavors of UNIX, and of course, Linux. Over the years he’s also volunteered for several nonprofit organizations to help support small networks that had little financial support. Rich is the author of many Linux-based books for total Linux geeks, and teaches online courses in Linux and web programming. When he’s not busy being a computer nerd, Rich enjoys playing piano and bass guitar and spending time with his wife, Barbara, and two daughters, Katie and Jessica.

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 1
Linux Basics

THE LINUX OPERATING SYSTEM HAS become one of the most widely used operating systems, popular among researchers, application developers, and hobbyists alike. These days, the Linux operating system can be found in a variety of computer environments, from mobile phones to satellites.

This chapter examines just what the Linux operating system is and why there are so many different Linux distributions available to choose from. With this information, you can select the right Linux distribution for your environment.

## What Is Linux?

If you’ve never worked with Linux before, you may be confused as to why there are so many different versions of it available. You’ve most likely heard terms such as distribution, LiveDVD, and GNU when looking at Linux packages and may have been confused. This section takes some of the mystery out of the Linux system before you start working on diving into Linux commands and features.

Although people usually refer to the Linux operating system as just “Linux,” in ­reality quite a few parts make up a complete Linux system. The Linux system has four main parts:

*   The Linux kernel

*   The GNU utilities

*   A user interface

*   Application software

Each of these four parts has a specific job in the Linux system. Although each of the parts by itself isn’t very useful, put together, they all create what people refer to as “Linux.” [FIGURE 1-1](#9781284254884_CH01_01.xhtml_C1fig001) shows the basic diagram of how these parts fit together to create the overall Linux system.

![A chart shows four main parts of a complete Linux system.](images/9781284255805_CH01_FIGF01.jpg)

FIGURE 1-1 The Linux system.

[Description](9781284254884_Alt.xhtml_summary-fig1-1)

The following sections describe these four parts in detail and give you an overview of how they work together to create a complete Linux system.

## The Linux Kernel

The core of the Linux system is the [kernel](#9781284254884_Glossary.xhtml_GLOS-164). The kernel controls all of the hardware and software on the computer system, providing access to hardware when necessary, and executing software when required.

If you’ve been following the Linux world at all, no doubt you’ve heard the name Linus Torvalds. Linus is the person responsible for creating the first Linux kernel software while he was a student at the University of Helsinki. He intended it to be a copy of the Unix system, at the time a popular operating system used at many universities.

After developing the Linux kernel, Linus released it to the Internet community and solicited suggestions for improving it. This simple process started a revolution in the world of computer operating systems. Soon Linus was receiving suggestions from students as well as professional programmers from around the world.

Allowing anyone to change programming code in the kernel would result in complete chaos. To simplify things, Linus acted as a central point for all improvement suggestions. It was ultimately Linus’s decision whether or not to incorporate suggested code in the kernel. This same concept is still in place with the Linux kernel code, except that instead of just Linus controlling the kernel code, a team of developers has taken on the task.

The kernel is primarily responsible for four main functions:

*   System memory management

*   Software program management

*   Hardware management

*   Filesystem management

The following sections explore each of these functions in more detail.

### System Memory Management

One of the primary functions of the operating system kernel is [memory management](#9781284254884_Glossary.xhtml_GLOS-202). Memory management is the ability to control how programs and utilities run within the memory restrictions of the system. Not only does the kernel manage the physical memory available on the server, it can also create and manage [virtual memory](#9781284254884_Glossary.xhtml_GLOS-358), or memory that doesn’t actually exist but is created on the hard drive and treated as real memory.

It does this by using space on the hard disk called the [swap space](#9781284254884_Glossary.xhtml_GLOS-324). The kernel swaps the contents of virtual memory locations back and forth from the swap space to the actual physical memory. This allows applications to think there is more memory available than what physically exists (as shown in [FIGURE 1-2](#9781284254884_CH01_02.xhtml_C1fig002)).

![Three boxes labeled virtual memory, physical memory, and swap space all lead to the kernel box. Swap space box is placed in a cylinder.](images/9781284255805_CH01_FIGF02.jpg)

FIGURE 1-2 The Linux system memory map.

The memory locations are grouped into blocks called [pages](#9781284254884_Glossary.xhtml_GLOS-243). The kernel locates each page of memory either in the physical memory or the swap space. The kernel then maintains a table of the memory pages that indicates which pages are in physical memory and which pages are swapped out to disk.

The kernel keeps track of which memory pages are in use and automatically copies memory pages that have not been accessed for a period of time to the swap space area (called swapping out)—even if there’s other memory available. When a program wants to access a memory page that has been swapped out, the kernel must make room for it in physical memory by swapping out a different memory page and swapping in the required page from the swap space. Obviously, this process takes time and can slow down a running process. The process of swapping out memory pages for running applications continues for as long as the Linux system is running.

You can see the current status of the virtual memory on your Linux system by viewing the special /proc/meminfo file. Here’s an example of a sample /proc/meminfo entry:

![An example of a sample slash proc slash mem info entry is shown.](images/9781284255805_CH01_CUM01.jpg)

![An example of a sample slash proc slash mem info entry is shown.](images/9781284255805_CH01_CUM02.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd1-1)

The MemTotal and MemFree lines show that this Linux server has 20 GB of ­physical memory and that there is about 14 GB not currently being used (free). The output also shows that there is about 2 GB of swap space memory available on this system. The kernel continually updates the meminfo file to show exactly what’s going on in memory at that moment in time, so you can always get a picture of what’s happening on the system.

### Software Program Management

With the Linux operating system, a running program is called a [process](#9781284254884_Glossary.xhtml_GLOS-265). A process can run in the foreground, displaying output on a display, or it can run in the background, behind the scenes. The kernel controls how the Linux system manages all the processes running on the system.

The kernel creates the first process, called the [init process](#9781284254884_Glossary.xhtml_GLOS-143), to start all other processes on the system. When the kernel starts, it loads the init process into virtual memory. As the kernel starts each additional process, it gives it a unique area in virtual memory to store the data and code that the process uses.

There are a few different types of init process implementations available in Linux, but these days, two are most popular:

*   SysVinit—The [SysVinit](#9781284254884_Glossary.xhtml_GLOS-331) initialization method was the original method used by Linux and was based on the Unix System V initialization method. Though it is not used by many Linux distributions these days, you still may find it around in older Linux distributions

*   Systemd—The systemd initialization method was created in 2010 and has become the most popular initialization and process management system used by Linux distributions.

#### The SysVinit method

The SysVinit initialization method used a concept called [run levels](#9781284254884_Glossary.xhtml_GLOS-296) to determine what processes to start. The run level defines the state of the running Linux system, and what processes should run in each state. [TABLE 1-1](#9781284254884_CH01_02.xhtml_C1tab001) shows the different run levels associated with the SysVinit initialization method.

TABLE 1-1 SysVinit initialization methods.

| RUN LEVEL | DESCRIPTION |
| --- | --- |
| 0 | Shut down the system |
| 1 | Single-user mode used for system maintenance |
| 2 | Multi-user mode without networking services enabled |
| 3 | Multi-user mode with networking services enabled |
| 4 | Custom |
| 5 | Multi-user mode with GUI enabled |
| 6 | Reboot the system |

The /etc/inittab file defines the default run level for the system. The processes that start for specific run levels are defined in subdirectories of the /etc/rc.d directory. You can view the current run level at any time using the runlevel command:

![Line 1: dollar space run level. Line 2: N space 5\. Line 3: dollar.](images/9781284255805_CH01_CUM03.jpg)

This output shows the system is currently at run level 5, which is the default used for graphical desktops.

#### The systemd method

The systemd initialization method has become popular because it has made several improvements over the original init method. One of those improvements is that it has the ability to start processes based on different events:

*   When the system boots

*   When a particular hardware device is connected

*   When a service is started

*   When a network connection is established

*   When a timer has expired

The systemd method determines what processes to run by linking events to [unit files](#9781284254884_Glossary.xhtml_GLOS-346). Each unit file defines the programs to start when the specified event occurs. The ­systemctl program allows you to start, stop, and list the unit files currently running on the system.

The systemd method also groups unit files together into [targets](#9781284254884_Glossary.xhtml_GLOS-334). A target defines a specific running state of the Linux system, similar to the SysVinit run level concept. At system startup, the [default.target](#9781284254884_Glossary.xhtml_GLOS-64) target defines all of the unit files to start. You can view the current default target using the systemctl command:

![Line 1: dollar space system c t l space get hyphen default. Line 2: graphical dot target. Line 3: dollar.](images/9781284255805_CH01_CUM04.jpg)

The graphical.target target defines the processes to start when a multi-user graphical environment is running, similar to the old SysVinit run level 5.

#### Viewing processes

The ps command allows you to view the processes currently running on the Linux ­system. Here’s an example of what you’ll see using the ps command:

![An output of the p s command is shown.](images/9781284255805_CH01_CUM05.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd1-2)

![Continuation](images/9781284255805_CH01_CUM06.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd1-3)

There are lots of processes running on a Linux system at any time; I’ve abbreviated the output to show just a few of the listed processes. The first column in the output shows the process ID (or PID). Notice that the first process is the friendly init process, and the Linux system assigns it PID 1\. All other processes that start after the init process are assigned PIDs in numerical order. No two processes can have the same PID.

The third column shows the current status of the process (I for idle, S for sleeping, and R for running). The last column shows the process name. The process names that appear in brackets mean that the ps command couldn’t determine the command line parameters used to start the process.

### Hardware Management

Still another of the kernel’s responsibilities is hardware management. Any device that the Linux system must communicate with needs [driver code](#9781284254884_Glossary.xhtml_GLOS-79). The driver code allows the kernel to pass data back and forth to the device, acting as a middleman between ­applications and the hardware. Two methods are used for interfacing device driver code with the Linux kernel:

*   Compiling the device driver code with the kernel code

*   Compile the device driver code into a separate module, which then interfaces with the kernel during runtime

In the very early days of Linux, the only way to insert device driver code was to ­recompile the kernel. Each time you added a new device to the system, you had to ­recompile the kernel code. This process became even more inefficient as Linux kernels supported more hardware and as removable storage devices (such as USB sticks) became more popular. Fortunately, Linux developers devised a better method to insert driver code into the running kernel.

Programmers developed the concept of [kernel modules](#9781284254884_Glossary.xhtml_GLOS-165) to allow you to insert device driver code into a running kernel without having to recompile the kernel. Also, a kernel module could be removed from the kernel when the system had finished using the device. This greatly simplified using hardware with Linux.

The Linux system represents hardware devices as special files, called [device files](#9781284254884_Glossary.xhtml_GLOS-67). There are three different classifications of device files:

*   Character

*   Block

*   Network

A [character device file](#9781284254884_Glossary.xhtml_GLOS-39) is for a device that can only handle data one character at a time. Most types of modems and terminals are created as character files. A [block device file](#9781284254884_Glossary.xhtml_GLOS-31) is for a device such as a disk drive that can handle data in large blocks at a time.

The [network device file](#9781284254884_Glossary.xhtml_GLOS-218) types (also called socket files) are used for devices that use packets to send and receive data. This includes temporary files used to send network data between programs running on the same physical host and a special loopback device that allows the Linux system to communicate with itself using common network ­programming protocols.

Linux creates special files, called [nodes](#9781284254884_Glossary.xhtml_GLOS-226), for each device on the system. All communication with the device is performed through the device node. Each node has a unique number pair that identifies it to the Linux kernel. The number pair includes a major and a minor device number. Similar devices are grouped into the same major device number. The minor device number is used to identify a specific device within the major device group. Here is an example of a few device files on a Linux server:

![An example of a few device files on a Linux server is shown.](images/9781284255805_CH01_CUM07.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd1-4)

Different Linux distributions handle devices using different device names. In this ­distribution, the sda device is the first solid state drive (SSD) on the system.

The fifth column is the major device node number. Notice that all of the sda devices have the same major device node, 8\. The sixth column is the minor device node number. Each device within a major number has its own unique minor device node number.

The first column indicates the permissions for the device file. The first character of the permissions indicates the type of file. Notice that the SSD files are all marked as block (b) devices.

### Filesystem Management

A [filesystem](#9781284254884_Glossary.xhtml_GLOS-101) defines how the operating system stores data on storage devices. Unlike some other operating systems, the Linux kernel can support different types of ­filesystems to read and write data to and from hard drives, CD or DVD devices, and USB flash drives. Besides having over a dozen filesystems of its own, Linux can read and write to and from filesystems used by other operating systems, such as Microsoft Windows. The kernel must be compiled with support for all types of filesystems that the system will use, or device driver modules must be built and installed to support the filesystem. [TABLE 1-2](#9781284254884_CH01_02.xhtml_C1tab002) lists the standard filesystems that a Linux system can use to read and write data.

TABLE 1-2 Linux filesystems.

| FILESYSTEM | DESCRIPTION |
| --- | --- |
| ext | Linux extended filesystem—the original Linux filesystem |
| ext2 | Second extended filesystem, provided advanced features over ext |
| ext3 | Third extended filesystem, supports journaling |
| ext4 | Fourth extended filesystem, supports advanced journaling |
| btrfs | A newer, high performance filesystem that supports journaling and large files |
| exfat | The extended Windows filesystem, used for SD cards and USB sticks |
| hpfs | OS/2 high‐performance filesystem |
| jfs | IBM’s journaling filesystem |
| iso9660 | ISO 9660 filesystem (CD-ROMs) |
| minix | MINIX filesystem |
| msdos | Microsoft FAT16 |
| nfs | Network File System |
| ntfs | Support for Microsoft NT file system |
| proc | Access to system information |
| smb | Samba SMB filesystem for network access |
| sysv | Older Unix filesystem |
| ufs | BSD filesystem |
| umsdos | Unix—like filesystem that resides on top of MS-DOS |
| vfat | Windows 95 file system (FAT32) |
| XFS | High‐performance 64‐bit journaling filesystem |

Any hard drive that a Linux system accesses must be formatted using one of the ­filesystem types listed in Table 1-1.

The Linux kernel interfaces with each filesystem using the [Virtual File System (VFS)](#9781284254884_Glossary.xhtml_GLOS-357).  This provides a standard interface for the kernel to communicate with any type of ­filesystem. VFS caches information in memory as each filesystem is mounted and used.

## The GNU Utilities

Besides having a kernel to control hardware devices, a computer operating system needs utilities to perform standard functions, such as handling files and programs. Although Linus created the Linux system kernel, he had no system utilities to run on it. Fortunately for him, at the same time he was working, a group of people on the Internet were working together trying to develop a standard set of computer system utilities that mimicked the popular Unix operating system.

The GNU organization ([GNU](#9781284254884_Glossary.xhtml_GLOS-118) stands for [GNU’s Not Unix](#9781284254884_Glossary.xhtml_GLOS-118), a clever recursive acronym) developed a complete set of Unix-like utilities but had no kernel system to run them on. These utilities were developed under a software philosophy called [open source ­software (OSS)](#9781284254884_Glossary.xhtml_GLOS-232).

The concept of OSS allows programmers to develop software and then release it to the world for use, often with no licensing fees attached. Anyone can use the software, modify it, or incorporate it into his or her own system without having to pay a license fee. Uniting Linus’s Linux kernel with the GNU operating system utilities created a complete, ­functional, free operating system.

Although the bundling of the Linux kernel and GNU utilities is often just called Linux, you will see some Linux purists on the Internet refer to it as the GNU/Linux system to give credit to the GNU organization for its contributions to the cause.

The GNU Project was mainly designed for Unix system administrators to have a ­Unix-like environment available. This focus resulted in the project porting many common Unix system command­line utilities. The core bundle of utilities supplied for Linux systems is called the [coreutils](#9781284254884_Glossary.xhtml_GLOS-58) package.

The GNU coreutils package consists of three parts:

*   Utilities for handling files

*   Utilities for manipulating text

*   Utilities for managing processes

Each of these three main groups of utilities contains several utility programs that are invaluable to the Linux system administrator and programmer.

## Linux User Interfaces

Having a world-class operating system that can manage your computer hardware and software is great, but you need some way to communicate with it. With the popularity of Microsoft Windows, desktop computer users expect some type of graphical display to interact with their system. This spurred more development in the OSS community, and the Linux graphical desktops emerged.

Linux is famous for being able to do things in more than one way, and no place is this more relevant than in graphical desktops. There are a plethora of graphical desktops you can choose from in Linux. The following sections describe a few of the more popular ones.

### The X Window System

Two basic elements control your video environment—the video card in your workstation and your monitor. To display fancy graphics on your computer, the Linux software needs to know how to talk to both of them.

The [X Window](#9781284254884_Glossary.xhtml_GLOS-366) software is a low­level program that works directly with the video card and monitor in the workstation and controls how Linux applications can present fancy windows and graphics on your computer.

Linux isn’t the only operating system that uses X Window; there are versions ­written for many different operating systems. In the Linux world, a few different software ­packages can implement X Window, but two are most commonly used:

*   X.org

*   Wayland

The [X.org](#9781284254884_Glossary.xhtml_GLOS-367) package is the older of the two, based on the original Unix X Window System version 11 (often called X11). More Linux distributions are migrating to the newer ­[Wayland](#9781284254884_Glossary.xhtml_GLOS-361) software, which is more versatile and easier to maintain.

When you first install a Linux distribution, it attempts to detect your video card and monitor, and then creates an X Window configuration file that contains the required information. During installation, you may notice a time when the installation program scans your monitor for supported video modes. Sometimes this causes your monitor to go blank for a few seconds. Because there are lots of different types of video cards and monitors out there, this process can take a little while to complete.

The core X Window software produces an interface for running graphical ­applications, but nothing else. While this is fine for running individual applications, it is not too ­useful for day-to-day computer use. There is no desktop environment allowing users to ­manipulate files or launch programs. To do that, you need a desktop environment on top of the X Window system software.

### The KDE Plasma Desktop

The [K Desktop Environment (KDE)](#9781284254884_Glossary.xhtml_GLOS-162) was first released in 1996 as an open source project to produce a graphical desktop similar to the Microsoft Windows environment. The  KDE desktop incorporates all of the features you are probably familiar with if you are a Windows user. [FIGURE 1-3](#9781284254884_CH01_04.xhtml_C1fig003) shows the current version, called [KDE Plasma](#9781284254884_Glossary.xhtml_GLOS-163), running in the openSUSE Linux distribution.

![A screenshot shows the K D E Plasma desktop in open S U S E.](images/9781284255805_CH01_FIGF03.jpg)

FIGURE 1-3 The KDE Plasma desktop in openSUSE.

Courtesy of KDE.

[Description](9781284254884_Alt.xhtml_summary-fig1-3)

The KDE Plasma desktop allows you to place both application and file icons in a ­special area on the desktop. If you click an application icon, the Linux system starts the ­application. If you click on a file icon, the KDE desktop attempts to determine which ­application to start to handle the file.

The bar at the bottom of the desktop is called the Panel. The Panel consists of four parts:

*   The K menu—Similar to the Windows Start menu, the K menu contains links to start installed applications.

*   Program shortcuts—These are quick links to start applications directly from the Panel.

*   The taskbar—The taskbar shows icons for applications currently running on the desktop.

*   Applets—These are small applications that have an icon in the Panel that can change depending on information from the application.

All of the Panel features are similar to what you would find in Microsoft Windows. Besides the desktop features, the KDE project has produced a wide assortment of ­applications that run in the KDE environment. These applications are shown in [TABLE 1-3](#9781284254884_CH01_04.xhtml_C1tab003). (You may notice the trend of using a capital K in KDE application names.)

TABLE 1-3 KDE applications.

| APPLICATION | DESCRIPTION |
| --- | --- |
| Amarok | Audio file player |
| digiKam | Digital camera software |
| Dolphin | File manager |
| K3b | CD-burning software |
| Kaffeine | Video player |
| KMail | Email client |
| KOffice | Office applications suite |
| Konqueror | File and web browser |
| Kontact | Personal information manager |
| Kopete | Instant messaging client |

This is only a partial list of applications produced by the KDE project. Many more ­applications are included with the KDE ­desktop.

### The GNOME Desktop

The GNU Network Object Model Environment (GNOME) is another popular Linux desktop environment. First released in 1999, GNOME has become the default desktop environment for many Linux ­distributions (the most popular being Red Hat Enterprise Linux).

[FIGURE 1-4](#9781284254884_CH01_04.xhtml_C1fig004) shows the standard GNOME 3 desktop used in the Ubuntu Linux distribution.

![A screenshot shows a GNOME 3 desktop. Rich and trash icons are at top left of the desktop. Several icons are listed in the left ribbon from top to bottom under Activities.](images/9781284255805_CH01_FIGF04.jpg)

FIGURE 1-4 A GNOME 3 desktop on an Ubuntu Linux system.

Courtesy of GNOME Project.

Not to be outdone by KDE, the GNOME developers have also produced a host of ­graphical applications that integrate with the GNOME desktop, as shown in [TABLE 1-4](#9781284254884_CH01_04.xhtml_C1tab004).

TABLE 1-4 GNOME applications.

| APPLICATION | DESCRIPTION |
| --- | --- |
| Epiphany | Web browser |
| Evince | Document viewer |
| Gcalctool | Calculator |
| Gedit | GNOME text editor |
| GNOME Panel | Desktop panel for launching applications |
| GNOME Nettool | Network diagnostics tool |
| GNOME Terminal | Terminal emulator |
| Nautilus | Graphical file manager |
| Nautilus CD Burner | CD-burning tool |
| Sound Juicer | Audio CD–ripping tool |
| Tomboy | Notetaking software |
| Totem | Multimedia player |

As you can see, quite a few applications are also available for the GNOME desktop. Besides all of these applications, most Linux distributions that use the GNOME ­desktop also incorporate the KDE libraries, allowing you to run KDE applications on your GNOME desktop.

### Other Linux Desktops

One of the main features of Linux is choice, and nowhere is that more evident than in the graphical desktop world. A plethora of different types of graphical desktops are available in the Linux world. If you’re not happy with the default desktop in your Linux ­distribution, it usually doesn’t take much effort to change it to something else!

When the GNOME desktop project radically changed its interface in version 3, many Linux developers who preferred the look-and-feel of GNOME version 2 created spin-off versions based on GNOME 2\. Of these, two became somewhat popular:

*   [Cinnamon](#9781284254884_Glossary.xhtml_GLOS-44) The Cinnamon desktop was developed in 2011 by the Linux Mint ­distribution in an attempt to continue development of the original GNOME 2 ­desktop. It’s now available as an option in several Linux distributions, including Ubuntu, Fedora, and openSUSE.

*   [MATE](#9781284254884_Glossary.xhtml_GLOS-200) The MATE desktop was also developed in 2011 by an Arch Linux user who disliked the switch to GNOME 3\. However, it incorporates a few features of GNOME 3 (such as replacing the taskbar) but maintains the overall look-and-feel of GNOME 2.

[FIGURE 1-5](#9781284254884_CH01_04.xhtml_C1fig005) shows the Cinnamon desktop as it appears in the Linux Mint distribution.

![A screenshot shows the Cinnamon desktop from Linux Mint.](images/9781284255805_CH01_FIGF05.jpg)

FIGURE 1-5 The Cinnamon desktop from Linux Mint.

Courtesy of Linux Mint.

[Description](9781284254884_Alt.xhtml_summary-fig1-5)

The downside to these fancy graphical desktop environments is that they require a fair amount of system resources to operate properly. In the early days of Linux, a hallmark and selling feature of Linux was its ability to operate on older, less powerful PCs that the newer Microsoft desktop products couldn’t run on. However, with the popularity of KDE Plasma and GNOME 3 desktops, this has changed because it takes just as much memory to run a KDE Plasma or GNOME 3 desktop as the latest Microsoft desktop environment.

If you have an older PC, don’t be discouraged. The Linux developers have banded together to take Linux back to its roots. They’ve created several low-memory–oriented graphical desktop applications that provide basic features that run perfectly fine on older PCs.

While these graphical desktops don’t have a plethora of applications designed around them, they still run many basic graphical applications that support features such as word processing, spreadsheets, databases, drawing, and, of course, multimedia support.

[TABLE 1-5](#9781284254884_CH01_04.xhtml_C1tab005) shows some of the smaller Linux graphical desktop environments that can be used on lower-powered PCs and laptops.

TABLE 1-5 Other Linux graphical desktops.

| DESKTOP | DESCRIPTION |
| --- | --- |
| Fluxbox | A bare-bones desktop that doesn’t include a Panel, only a pop-up menu to launch applications |
| Xfce | A desktop that’s similar to the GNOME 2 desktop, but with fewer graphics for low-memory environments |
| JWM | Joe’s Window Manager, a very lightweight desktop ideal for  low-memory and low-disk space environments |
| fvwm | Supports some advanced desktop features such as virtual desktops and Panels, but runs in low-memory environments |
| fvwm95 | Derived from fvwm, but made to look like a Windows 95 desktop |

These graphical desktop environments are not as fancy as the KDE Plasma and GNOME 3 desktops, but they provide basic graphical functionality just fine. [FIGURE 1-6](#9781284254884_CH01_04.xhtml_C1fig006) shows what the Xfce desktop used in the MX Linux distribution looks like.

![A screenshot shows the X f c e desktop used in the M X Linux distribution.](images/9781284255805_CH01_FIGF06.jpg)

FIGURE 1-6 The Xfce desktop as seen in the MX Linux distribution.

Courtesy of Linux Foundation.

[Description](9781284254884_Alt.xhtml_summary-fig1-6)

If you are using an older PC, try a Linux distribution that uses one of these desktops and see what happens. You may be pleasantly surprised.

### The Command Line Interface

While having a fancy graphical desktop interface is nice, there are drawbacks. The extra processing power required to interact with the graphics card takes away crucial CPU time that can be used for other programs. Nowhere is this more important than in a server environment.

Because of that, many Linux servers don’t install a graphical desktop by default and instead rely on a text-based interface, called the [command line interface (CLI)](#9781284254884_Glossary.xhtml_GLOS-49). The CLI provides a way for users to start programs, manage files on the filesystem, and manage processes running on the Linux system using simple text commands. The CLI is produced by a program called a [shell](#9781284254884_Glossary.xhtml_GLOS-306). The shell allows you to enter text commands, and then it ­interprets the commands and executes them in the kernel.

The shell contains a set of internal commands that you use to control things such as copying files, moving files, renaming files, displaying the programs currently ­running on the system, and stopping programs running on the system. Besides the internal ­commands, the shell also allows you to enter the name of a program at the [command prompt](#9781284254884_Glossary.xhtml_GLOS-50). The shell passes the program name off to the kernel to start it.

You can also group shell commands into files to execute as a program. Those files are called [shell scripts](#9781284254884_Glossary.xhtml_GLOS-307). Any command that you can execute from the command line can be placed in a shell script and run as a group of commands. This provides great ­flexibility in creating utilities for commonly run commands or processes that require several ­commands grouped together.

Quite a few Linux shells are available to use on a Linux system. Different shells have ­different characteristics, some being more useful for creating scripts and others more ­useful for managing processes. The default shell used in many Linux distributions is the [Bash](#9781284254884_Glossary.xhtml_GLOS-27) shell. The Bash shell was developed by the GNU project as a replacement for the ­standard Unix shell, called the Bourne shell (after its creator). The bash shell name is a play on this wording, referred to as the “Bourne again shell.”

In addition to the Bash shell, there are several other popular shells you could run into in a Linux environment. [TABLE 1-6](#9781284254884_CH01_04.xhtml_C1tab006) lists the more popular ones.

TABLE 1-6 Popular Linux shells

| SHELL | DESCRIPTION |
| --- | --- |
| ash | A simple, lightweight shell that runs in low-memory environments but has full ­compatibility with the bash shell |
| ksh | A programming shell compatible with the Bourne shell but supporting advanced programming features like associative arrays and floating-point arithmetic |
| tcsh | A shell that incorporates elements from the C programming language into shell scripts |
| zsh | An advanced shell that incorporates features from bash, tcsh, and korn, providing advanced programming features, shared history files, and themed prompts |

Most Linux distributions include more than one shell, although usually they pick one of them to be the default. If your Linux distribution includes multiple shells, feel free to experiment with different shells and see which one fits your needs.

## Linux Distributions: Why So Many?

Now that you have seen the main components required for a complete Linux system, you may be wondering how you are going to get them all put together to make a Linux system. Fortunately, there are people who have already done that.

A complete Linux system package is called a [distribution](#9781284254884_Glossary.xhtml_GLOS-73). Lots of different Linux ­distributions are available to meet just about any computing requirement you could have. Most distributions are customized for a specific user group, such as business users, multimedia enthusiasts, software developers, or typical home users. Each customized ­distribution includes the software packages required to support specialized functions, such as audio­ and video­editing software for multimedia enthusiasts, or compilers and integrated development environments (IDEs) for software developers.

The different Linux distributions are often divided into two categories:

*   Full core Linux distributions

*   Specialized distributions

The following sections describe these different types of Linux distributions and show some examples of Linux distributions in each category.

### Core Linux Distributions

A [core Linux distribution](#9781284254884_Glossary.xhtml_GLOS-57) contains a kernel, one or more graphical desktop environments, and just about every Linux application that is available. It provides one­stop shopping for a complete Linux installation. Often other Linux distributions derive from a core Linux distributions, using a subset of applications available. [TABLE 1-7](#9781284254884_CH01_05.xhtml_C1tab007) shows some of the more popular core Linux distributions.

TABLE 1-7 Core Linux distributions.

| DISTRIBUTION | DESCRIPTION |
| --- | --- |
| Slackware | One of the original Linux distribution sets, popular with Linux geeks |
| Red Hat Enterprise | A commercial business distribution used mainly for Internet servers |
| Gentoo | A distribution designed for advanced Linux users, containing only Linux source code |
| openSUSE | Different distributions for business and home use |
| Debian | Popular with Linux experts and commercial Linux products |

In the early days of Linux, a distribution was released as a set of floppy disks. You had to download groups of files and then copy them onto disks. It would usually take 20 or more disks to make an entire distribution! Needless to say, this was a painful experience.

Nowadays, Linux distributions are released as an [ISO image file](#9781284254884_Glossary.xhtml_GLOS-157). The ISO image file is a complete disk image of a DVD as a single file. You use a software application to either burn the ISO image file onto a DVD or create a bootable USB stick. You then just boot your workstation from the DVD or USB stick to install Linux. This makes installing Linux much easier.

However, beginners still often run into problems when they install one of the core Linux distributions. To cover just about any situation in which someone might want to use Linux, a single distribution has to include lots of application software. This includes everything from high­end Internet database servers to common games.

Although having lots of options available in a distribution is great for Linux geeks, it can become a nightmare for beginning Linux users. Most distributions ask a series of questions during the installation process to determine which ­applications and features to load by default. Beginners often find these questions confusing. As a result, they often either load way too many programs on their computer or don’t load enough and later discover that their computer won’t do what they want it to.

Fortunately for beginners, there’s a much simpler way to  install Linux.

### Derivative Linux Distributions

A new subgroup of Linux distributions was started aimed specifically at beginning Linux users. These derivative distributions are typically based on one of the core distributions but contain only a subset of applications that would make sense for a specific area of use.

Besides providing specialized software (such as only office products for business users), derivative Linux distributions also attempt to help beginning Linux users by automatically detecting and configuring common hardware devices. This makes installing Linux a much more enjoyable process.

[TABLE 1-8](#9781284254884_CH01_05.xhtml_C1tab008) shows some of the specialized Linux distributions available and what they specialize in.

TABLE 1-8 Derivative Linux distributions.

| DISTRIBUTION | DESCRIPTION |
| --- | --- |
| Fedora | A free distribution used as a testing ground for Red Hat Enterprise Linux |
| Ubuntu | A free distribution for school and home use |
| MX Linux | A free distribution for home use |
| Mint | A free distribution for home entertainment use |
| Puppy Linux | A free, small distribution that runs well on older PCs |

That’s just a small sampling of specialized Linux distributions. There are literally ­hundreds of specialized Linux distributions, and more are popping up all the time on the Internet. No matter what your specialty, you’ll ­probably find a Linux distribution made for you.

Many of the specialized Linux distributions are based on the Debian Linux ­distribution. They use the same installation files as Debian but package only a small fraction of a ­full-blown Debian system.

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 2
Linux and Software

APPLICATIONS MAKE OR BREAK AN operating system. Many good-intentioned operating systems have died due to lack of software support. Fortunately, Linux has benefited from a wide assortment of open source applications, both on the desktop and on the server.

This chapter discusses the most popular desktop and server applications available in Linux. It shows how applications are installed by default and how to add new applications to your Linux system. The chapter finishes up by discussing the different ways Linux distributions keep the installed software updated and patched for security vulnerabilities. These days those features are just as important as the initial installation of the software.

## Popular Linux Applications

Thanks to various open source projects, there are applications available in Linux for just about everything you currently do in Microsoft Windows, Apple macOS, or even Unix desktops and servers. The downside to such a wide assortment of applications, though, is that sometimes it can be difficult to know just which ones to use for your environment. This section walks through some of the more popular desktop and server applications available for Linux to give you an idea of where to start.

### Desktop Applications

If you’re running a Linux graphical desktop environment, most likely you’ll want it to be able to run similar applications that you can find in the Microsoft Windows or Apple macOS desktop environments. That includes features such as office productivity (word processing, spreadsheets, and presentation graphics), web browsing, email, and file management. This section walks through the most common Linux applications used for each of these areas.

#### Office Productivity

At one time the [OpenOffice.org](#9781284254884_Glossary.xhtml_GLOS-233) software package was the most common office suite package in Linux. It provides programs for word processing (Writer), spreadsheet (Calc), presentation graphics (Impress), drawing (Draw), math formulas (Math), and a desktop database interface (Base). However, the OpenOffice.org [software package](#9781284254884_Glossary.xhtml_GLOS-315) ran into some controversy of its own a few years back when the Oracle software company purchased the copyright to it as part of the acquisition of Sun Microsystems, the previous owner.

While Oracle kept the OpenOffice.org project open source, a group of open source developers decided to branch off an alternative package, called [LibreOffice](#9781284254884_Glossary.xhtml_GLOS-172). The LibreOffice branch includes the exact same packages as OpenOffice.org, using the exact same source code. However, it’s maintained as a separate branch package, so the two packages have now diverged somewhat with various features.

Since then, Oracle has donated the OpenOffice.org package to the Apache foundation, a large open source organization. This has appeased most open source enthusiasts, but unfortunately the damage had already been done. With the popularity of LibreOffice, most of the popular Linux desktop distributions have migrated to it. [FIGURE 2-1](#9781284254884_CH02_01.xhtml_c2-fig001) shows running the Writer application from an Ubuntu desktop. There’s hope that the two packages will merge back into one package someday, but until then the open source community will have to live with both versions.

![A screenshot shows the LibreOffice Writer program in Ubuntu.](images/9781284255805_CH02_FIGF01.jpg)

FIGURE 2-1 The LibreOffice Writer program in Ubuntu.

Courtesy of The Document Foundation and Mozilla.

[Description](9781284254884_Alt.xhtml_summary-fig2-1)

Besides the OpenOffice.org and LibreOffice packages, both the GNOME and KDE desktop projects have created their own office software suites (called Gnome Office and KOffice). These packages tend not to be as advanced as OpenOffice.org, but they’re great if you’re using an older, low-powered workstation!

#### Web Browsing

[Firefox](#9781284254884_Glossary.xhtml_GLOS-105) is by far the most common default web browser software in the Linux platform. The version available for Linux provides the same basic interface and features as the Windows and Mac versions. [FIGURE 2-2](#9781284254884_CH02_01.xhtml_c2-fig002) shows running Firefox on an Ubuntu desktop.

![A screenshot shows the Firefox browser in Ubuntu depicting the webpage of h t t p s colon slash slash Ubuntu dot com. The tab on the top represents Enterprise Open Source.](images/9781284255805_CH02_FIGF02.jpg)

FIGURE 2-2 The Firefox browser in Ubuntu.

Courtesy of Mozilla Corporation and Canonical Ltd.

You may run into a distribution that uses the [GNU IceCat](#9781284254884_Glossary.xhtml_GLOS-119) browser. This is a derivative of the Firefox browser, but without the Firefox logos. A few years back, there was some controversy about the Firefox browser. While the program code was open source, the Firefox logo was trademarked and licensed. To retaliate, open source developers created the Iceweasel (get the play on the name?) browser using the original Firefox source code but with a new logo, bypassing the trademark restrictions. That issue has since been resolved, but the GNU Project kept up development on Iceweasel, now calling it IceCat, and some Linux distributions still like to keep using the IceCat release instead of Firefox.

Besides Firefox and IceCat, other popular Linux browsers are [Chromium](#9781284254884_Glossary.xhtml_GLOS-42) (the open-source version of the Google Chrome browser) and [Opera](#9781284254884_Glossary.xhtml_GLOS-235), a commercial (but free) browser. There’s also a text-based browser called [Lynx](#9781284254884_Glossary.xhtml_GLOS-190). Since Lynx is a text-based browser, it isn’t used in the standard graphical desktop environment, but it’s popular in the scripting world for scraping data off of webpages without having to download all the graphics elements from the pages

#### Email Client

Most Linux distributions that use the GNOME desktop environment (such as Red Hat) support the [Evolution](#9781284254884_Glossary.xhtml_GLOS-88) email client. Similarly, many KDE Plasma desktop distributions use the [KMail](#9781284254884_Glossary.xhtml_GLOS-169) email client. Both of these packages provide basic email client capabilities, but nothing too fancy.

By default, the Ubuntu distribution uses the [Thunderbird](#9781284254884_Glossary.xhtml_GLOS-337) email client (as shown in [FIGURE 2-3](#9781284254884_CH02_01.xhtml_c2-fig003)), created by the same development team as the Firefox browser (Mozilla). Thunderbird provides a simple setup that supports most common email servers (including Gmail and Yahoo), as well as interfacing with the local email system in Linux.

![A screenshot shows the Thunderbird email client in Ubuntu.](images/9781284255805_CH02_FIGF03.jpg)

FIGURE 2-3 The Thunderbird email client in Ubuntu.

Courtesy of Mozilla Corporation and Canonical Ltd.

[Description](9781284254884_Alt.xhtml_summary-fig2-3)

You can manage multiple mailboxes with both Evolution and Thunderbird as well as create local mail folders for sorting your messages.

#### File Management

File management software allows you to graphically peruse through your stored files and folders, creating, copying, moving, and deleting them. The file manager that your Linux distribution uses usually depends on the desktop manager. GNOME desktops use the [Files](#9781284254884_Glossary.xhtml_GLOS-103) file manager software (previously called Nautilus), while KDE Plasma desktops use the [Dolphin](#9781284254884_Glossary.xhtml_GLOS-76) file manager package. [FIGURE 2-4](#9781284254884_CH02_01.xhtml_c2-fig004) shows the Files file manager in Ubuntu.

![A screenshot shows the Files file manager in Ubuntu.](images/9781284255805_CH02_FIGF04.jpg)

FIGURE 2-4 The Files file manager in Ubuntu.

Courtesy of Canonical Ltd.

[Description](9781284254884_Alt.xhtml_summary-fig2-4)

Both Files and Dolphin allow you to navigate through the directory levels in the Linux system with simple clicks, similar to Windows Explorer in Windows, and the Finder on the Mac. The action of copying or moving files is as simple as dragging-and-dropping icons between folders in the graphical interface.

### Server Applications

One of the more popular uses of Linux these days is as a server platform. Linux server systems can be cheaper and easier to manage than their Windows counterparts, and they can often run for months without requiring a reboot. The Linux platform supports a robust assortment of server applications that can seamlessly fit into any server environment. This section takes a look at the more popular Linux server applications.

#### Web Server

The original web server software for Linux is the [Apache](#9781284254884_Glossary.xhtml_GLOS-16) server. The Apache server software started out as a fork of the original NCSA web server package that started the World Wide Web. The Apache name is a play on the phrase “a patchy server,” due to the large number of software patches that were applied to the NCSA software.

A newer web server package that’s gaining popularity in the Linux world is [Nginx](#9781284254884_Glossary.xhtml_GLOS-222) (pronounced “engine-X”). The claim to fame of the Nginx package is that it can implement load balancing across multiple web servers. This has become popular in high-volume websites on the Internet.

The Apache and Nginx web servers are the Swiss army knives of Linux web servers. They do everything and then some. Sometimes, you’ll have an application that doesn’t require such a sophisticated web server, or you may be running your application on a low-powered system. There are a few alternatives to these packages that just provide basic web server services. [Lighttpd](#9781284254884_Glossary.xhtml_GLOS-173) is one popular no-frills web server that you might run into in smaller Linux setups.

#### Database Server

The Internet runs on data. Every application needs some type of data management system. Linux servers have quite a few different options for database servers. The [MySQL](#9781284254884_Glossary.xhtml_GLOS-215) (with its clone [MariaDB](#9781284254884_Glossary.xhtml_GLOS-198)) and [PostgreSQL](#9781284254884_Glossary.xhtml_GLOS-258) software packages are the two most popular choices for relational database servers.

The MySQL package is known for its speed, but it doesn’t support some of the more advanced database features found in commercial database packages. PostgreSQL, on the other hand, does support lots of advanced database features, but it can be somewhat slower. Many popular online stores forgo advanced features in favor of speed and use the MySQL database server.

A new trend has started toward [NoSQL](#9781284254884_Glossary.xhtml_GLOS-230) databases. NoSQL databases can handle large quantities of data by forgoing the structured database tables of SQL relational databases and instead store data as structureless [collections](#9781284254884_Glossary.xhtml_GLOS-47). Each collection consists of documents, which contain the individual data elements. The key to NoSQL is that unlike relational databases, in a collection each document can contain different data! Queries are structured to look for individual data elements among the varying document types in the collection. Currently the [MongoDB](#9781284254884_Glossary.xhtml_GLOS-207) database is the tool of choice to set up a document-based NoSQL environment in Linux.

#### Email Server

The [sendmail](#9781284254884_Glossary.xhtml_GLOS-302) package is the original email server software for the Unix environment. It has carried over to the Linux environment but shows its age. It’s notoriously complicated to [configure](#9781284254884_Glossary.xhtml_GLOS-54), making it difficult to set up even a basic email server, and developers are constantly finding security holes in it to patch.

Because of that, a few other email server packages have risen in popularity. Of these, the three most popular packages are [Postfix](#9781284254884_Glossary.xhtml_GLOS-257), [eXim](#9781284254884_Glossary.xhtml_GLOS-90), and [qMail](#9781284254884_Glossary.xhtml_GLOS-270). All three of these packages use simpler configuration files that allow the server administrator to easily fine-tune how the server handles email both internally and with remote hosts.

#### Network File Sharing

Most local networks require some type of file sharing between clients. Linux supports two main file sharing applications. The [Network File Sharing (NFS)](#9781284254884_Glossary.xhtml_GLOS-219) software is the original Unix software for sharing directories between Unix systems. That package works great for Linux-to-Linux file sharing.

With the popularity of Microsoft Windows workstations, though, many networks require interacting with Windows servers to share files and printers. The [Samba](#9781284254884_Glossary.xhtml_GLOS-297) software package can emulate a Microsoft Windows server environment on a Linux server, including the Active Directory authentication system. This allows you to seamlessly incorporate a Linux server running Samba into a Microsoft network to communicate with both Microsoft servers and clients to provide print and file sharing features.

## Exploring Package Management

Trying to keep track of just what software is installed on a Linux system can be somewhat of a challenge. To make life easier, each of the major Linux distributions utilizes some form of a [package management system](#9781284254884_Glossary.xhtml_GLOS-242) to control installing software applications and libraries. The package management system bundles each application into a separate [package](#9781284254884_Glossary.xhtml_GLOS-241) that can be installed, modified, or uninstalled as a single bundle. The package management system utilizes a database that keeps track of the following:

*   What software packages are installed on the Linux system

*   What files have been installed for each package

*   What versions of each of the software packages are installed

Software packages are stored on servers, called repositories, and are accessed across the Internet via package management system utilities running on your local Linux system. You can use the package management system utilities to search for new software packages or even updates and security patches to software packages already installed on the system.

A software package will often have [dependencies](#9781284254884_Glossary.xhtml_GLOS-65), or other packages that must be installed first for the software to run properly. The package management system utilities detect these dependencies and offer to install any additionally needed software packages before installing the desired package.

The downside to package management system is that there isn’t a single standard utility. The package management system utilities and their associated commands are vastly different between the various Linux distributions. However, two primary package management system utilities have become popular and are commonly used in the Linux world. These are [dpkg](#9781284254884_Glossary.xhtml_GLOS-77) and [rpm](#9781284254884_Glossary.xhtml_GLOS-295).

Debian-based distributions such as Ubuntu and Linux Mint use, at the base of their package management system utilities, the dpkg command. This command interacts directly with the package management system on the Linux system and is used for installing, managing, and removing software packages.

The Red Hat–based distributions, such as Fedora, CentOS, openSUSE, and Rocky, use the rpm command at the base of their package management system. Similar to the dpkg command, the rpm command can list installed packages, install new packages, and remove existing software.

Note that these two commands are the core of their respective package management system, not the entire package management system itself. Many Linux distributions that use the dpkg or rpm methods have built additional specialty package management system utilities upon these base commands to help make your life much easier. The following sections walk through various package management system utility commands you’ll run into in the popular Linux distributions.

### Exploring the Debian-Based Systems

The dpkg command is at the core of the Debian-based family of package management system tools. It provides options to install, update, and remove .deb package files on your Linux system.

The dpkg command assumes you have the .deb package file downloaded onto your local Linux system. More often than not that’s not the case. Usually you’ll want to install an application package from the repository for your Linux distribution. To do that you’ll want to use the [apt](#9781284254884_Glossary.xhtml_GLOS-20) suite of tools:

*   apt-cache

*   apt-get

*   apt

The apt tool is essentially a front-end for both the apt-cache and apt-get tools. The nice thing about apt is that you don’t need to remember which tool to use when; it covers everything you need to do with package management. The apt tool has a basic format:

![apt space open bracket options close bracket space command.](images/9781284255805_CH02_CUM01.jpg)

The command defines the action for the apt tool to take. If needed, you can specify one or more options to fine-tune what happens. This section looks at how to use the apt command line tool to work with the software packages on your Linux system.

#### Managing packages with apt

A common task faced by Linux system administrators is to determine what packages are already installed on the system. The apt list command displays all the packages available in the repository, but by adding the --installed option, you can limit the output to only those packages already installed on your system:

![The apt list installed option shows the packages already installed on a system.](images/9781284255805_CH02_CUM02.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-1)

As you can guess, the list of installed packages will be very long, I’ve abbreviated the output just to show a sample of what the output looks like. Next to the package name is some additional information about the package, such as the version name and whether the package is installed and flagged for automatic upgrades.

If you already know the packages on your system and want to quickly display detailed information about a particular package, use the show command:

![apt space show space package underscore name.](images/9781284255805_CH02_CUM03.jpg)

Here’s an example of displaying the details of the package zsh:

![An output displays the details of the package z s h.](images/9781284255805_CH02_CUM04.jpg)

![An output displays the details of the package z s h.](images/9781284255805_CH02_CUM05.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-2)

One detail you cannot get with apt is a listing of all the files associated with a particular software package. To get this list, you will need to go to the dpkg tool itself:

![d p k g space hyphen L space package underscore name.](images/9781284255805_CH02_CUM06.jpg)

Here’s an example of using dpkg to list all of the files installed as part of the acl package:

![An output shows a list of all files installed as part of the a c l package.](images/9781284255805_CH02_CUM07.jpg)

![An output shows a list of all files installed as part of the a c l package.](images/9781284255805_CH02_CUM08.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-3)

You can also do the reverse—find what package a particular file belongs to:

![d p k g space double hyphen search space absolute underscore file underscore name.](images/9781284255805_CH02_CUM09.jpg)

Note that you need to use an absolute file reference for this to work:

![Line 1: dollar space d p k g space double hyphen search space slash bin slash get f a c l. Line 2: a c l colon space slash bin slash get f a c l. Line 3: dollar.](images/9781284255805_CH02_CUM10.jpg)

The output shows the getfacl file was installed as part of the acl package.

#### Installing software packages with apt

Now that you know more about listing software package information on your system, this section walks you through a software package install. First, you’ll want to determine the package name to install. How do you find a particular software package? Use apt with the search command:

![apt space search space package underscore name.](images/9781284255805_CH02_CUM11.jpg)

The beauty of the search command is that you do not need to insert wildcards around package_name; wildcards are implied. By default, the search command displays packages that contain the search term in either the package name or the package description, which can be misleading at times. If you want to limit the output to only package names, include the --names-only option:

![An output limited to only package names is shown.](images/9781284255805_CH02_CUM12.jpg)

![An output limited to only package names is shown.](images/9781284255805_CH02_CUM13.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-4)

Once you find the package you’d like to install, installing it using apt is as easy as this:

![apt space install space package underscore name.](images/9781284255805_CH02_CUM14.jpg)

The output will show some basic information about the package and ask you if you want to proceed with the installation:

![An output shows basic information about the package.](images/9781284255805_CH02_CUM15.jpg)

![An output shows basic information about the package.](images/9781284255805_CH02_CUM16.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-5)

To check if the installation processed properly, just use the list command with the --installed option again. You should see the package appear, indicating it is installed.

Notice that when installing the requested package, apt asked to install other packages as well. This is because apt automatically resolved any necessary package dependencies for us and installs the needed additional library and software packages. This is a wonderful feature included in many package management systems.

#### Upgrading software with apt

While apt helps protect you from problems installing software, trying to coordinate a multiple-package update with dependencies can get tricky. To safely upgrade all the software packages on a system with any new versions in the repository, use the upgrade command:

![apt space upgrade.](images/9781284255805_CH02_CUM17.jpg)

Notice that this command doesn’t take any software package names as an argument. That’s because the upgrade option will upgrade all the installed packages to the most recent version available in the repository, which is safer for system stabilization.

Here’s a sample output from running the apt upgrade command:

![An output of the apt upgrade command is shown.](images/9781284255805_CH02_CUM18.jpg)

![An output of the apt upgrade command is shown.](images/9781284255805_CH02_CUM19.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-6)

In the output notice that apt lists not only the packages that will be upgraded but also any new packages that are required to be installed because of upgrades.

The upgrade command won’t remove any packages as part of the upgrade process. If a package needs to be removed as part of an upgrade, use the following command:

![apt space full hyphen upgrade.](images/9781284255805_CH02_CUM20.jpg)

While this may seem like an odd thing, sometimes it’s required to remove packages to keep things synchronized between distribution upgrades.

#### Uninstalling software with apt

Getting rid of software packages with apt is as easy as installing and upgrading them. The only real choice you have to make is whether or not to keep the software’s data and configuration files around afterward.

To remove a software package, but not the data and configuration files, use the remove command of apt. To remove a software package and the related data and configuration files, use the purge option:

![An output shows the usage of the purge option.](images/9781284255805_CH02_CUM21.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-7)

Notice though as part of the purge output apt warns us that the zsh-common package that was installed as a dependency wasn’t removed automatically, just in case it might be required for some other package. If you’re sure the dependency package isn’t required by anything else, you can remove it using the autoremove command:

![An output shows the usage of the autoremove command.](images/9781284255805_CH02_CUM22.jpg)

![An output shows the usage of the autoremove command.](images/9781284255805_CH02_CUM23.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-8)

The autoremove command will check for all packages that are marked as dependencies and no longer required.

The front-end interface, apt, provides intelligent command line options for working with the Debian-based dpkg utility. Now it’s time to take a look at the Red Hat–based distribution’s rpm utility and its various front-end interfaces.

### The Red Hat–Based Systems

Like the Debian-based distributions, the Red Hat–based systems have several different frontend tools that are available. Following are the common ones:

*   [yum](#9781284254884_Glossary.xhtml_GLOS-372): Used in Red Hat, CentOS, and Rocky

*   [zypper](#9781284254884_Glossary.xhtml_GLOS-374): Used in openSUSE

*   [dnf](#9781284254884_Glossary.xhtml_GLOS-75): An updated version of yum with some additional features

These frontends are all based on the rpm command line tool. The following section discusses how to manage software packages using these various rpm-based tools. The focus will be on dnf, but the other packages use similar commands and formats.

#### Listing installed packages

To find out what is currently installed on your system, at the shell prompt type the following command:

![d n f space list space installed.](images/9781284255805_CH02_CUM24.jpg)

The information will probably whiz by you on the display screen, so it’s best to redirect the installed software listing into a file. You can then use the more or less command (or a GUI editor) to look at the list in a controlled manner.

![d n f space list space installed space greater than space installed underscore software.](images/9781284255805_CH02_CUM25.jpg)

To find out detailed information for a particular software package, dnf really shines. Not only will it give you a very verbose description of the package, but with another simple command, you can see if the package is installed:

![An output shows the usage of the d n f command.](images/9781284255805_CH02_CUM26.jpg)

![An output shows the usage of the d n f command.](images/9781284255805_CH02_CUM27.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-9)

Finally, if you need to find out what software package provides a particular file on your filesystem, the versatile dnf can do that, too! Just enter the following command:

![d n f space provides space file underscore name.](images/9781284255805_CH02_CUM28.jpg)

Here’s an example of trying to find what software provided the file /usr/bin/gzip:

![An example is shown to find what software provided the file slash u s r slash bin slash g zip.](images/9781284255805_CH02_CUM29.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-10)

dnf checked two separate repositories: the local system, and the default Fedora repository.

#### Installing software with dnf

Installation of a software package using dnf is incredibly easy. The following is the basic command for installing a software package, all its needed libraries, and package dependencies from a repository:

![d n f space install space package underscore name.](images/9781284255805_CH02_CUM30.jpg)

Here’s an example of installing the zsh package, which provides an alternative command line shell:

![An output shows an example of installing the z s h package.](images/9781284255805_CH02_CUM31.jpg)

![An output shows an example of installing the z s h package.](images/9781284255805_CH02_CUM32.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-11)

You can begin to see that one of dnf’s strengths is that it uses very logical and user-friendly commands.

#### Upgrading software with dnf

In most Linux distributions, when you’re working away in the GUI, you get those nice little notification icons telling you a software upgrade to a new version is needed. Here at the command line, it takes a little more work.

To see the list of all the available upgrades for your installed packages, type the following command:

![d n f space list space upgrades.](images/9781284255805_CH02_CUM33.jpg)

It’s always nice to get no response to this command because it means you have nothing to upgrade! However, if you do discover a particular software package needs upgrading, then type in the following command:

![d n f space upgrade space package underscore name.](images/9781284255805_CH02_CUM34.jpg)

If you’d like to upgrade all the packages listed in the upgrade list, just enter the following command:

![d n f space upgrade.](images/9781284255805_CH02_CUM35.jpg)

#### Uninstalling software with dnf

The dnf tool also provides an easy way to uninstall software you no longer want on your system:

![d n f space remove space package underscore name.](images/9781284255805_CH02_CUM36.jpg)

Unfortunately at the time of this writing, there isn’t an option or command to remove the application files but keep any configuration or data files.

While life is considerably easier with package management system packages, it’s not always problem free. Occasionally things do go wrong. Fortunately, there’s help.

## Managing Software Using Containers

While package management systems have certainly made software installation in the Linux world much easier, they do have their drawbacks. To start out with, as you’ve already seen in this chapter, there are multiple competing package management systems. So for application developers to distribute an application that can be installed in all Linux distributions, they must create multiple versions to distribute.

But there’s even more complexity than that. Every application has some type of library functions that it depends on to run. When developers create a Linux application, they must take into consideration what library files are available in most Linux distributions, and not only that, but also what versions of the library files. While package management systems can track dependencies, as you can guess, this can quickly turn into a nightmare for software developers trying to get their applications working in most Linux distributions.

With cloud computing came a new paradigm in how applications can be packaged—[application containers](#9781284254884_Glossary.xhtml_GLOS-18). An application container creates an environment where all of the files required for an application to run are bundled together, including runtime library files. The developer can then release the application container as a single package and be guaranteed that it’ll run just fine on any Linux system.

While still relatively new, there are already several competing application container standards that are starting to emerge. The following sections take a look at two of the more popular ones—snap and flatpak.

### Using Snap Containers

Canonical, the creators of the Ubuntu Linux distribution, have developed an application container format called [snap](#9781284254884_Glossary.xhtml_GLOS-312). The snap packaging system bundles all the files required for an application into a single snap distribution file. The [snapd](#9781284254884_Glossary.xhtml_GLOS-313) application runs in background, and you use the snap command line tool to query the snap database to display installed snap packages as well as to install, upgrade, and remove snap packages.

To check if snap is running on your system, use the snap version command:

![An output shows the usage of the snap version command.](images/9781284255805_CH02_CUM37.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-12)

If snap is running, you can see a list of the currently installed snap applications by using the snap list command:

![An output shows a list of the currently installed snap applications by using the snap list command.](images/9781284255805_CH02_CUM38.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-13)

To search the snap repository for new applications, use the snap find command:

![An output shows the usage of the snap find command to search the snap repository for new applications.](images/9781284255805_CH02_CUM39.jpg)

![An output shows the usage of the snap find command to search the snap repository for new applications.](images/9781284255805_CH02_CUM40.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-14)

To view more information about a snap, use the snap info command:

![An output shows the usage of the snap info command to view more information about a snap.](images/9781284255805_CH02_CUM41.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-15)

To install a new snap application, use the snap install command:

![An output shows the usage of the snap install command to install a new snap application.](images/9781284255805_CH02_CUM42.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-16)

Notice that you must have root user privileges to install snaps. In Ubuntu, that means using the sudo command.

If you need to remove a snap, just use the snap remove command:

![Line 1: dollar sudo snap remove solitaire. Line 2: solitaire removed. Line 3: dollar.](images/9781284255805_CH02_CUM43.jpg)

As the snap is removed, you’ll see some messages about the progress of the removal. Instead of removing a snap, you can just disable it without removing it. Just use the snap disable command. To re-enable the snap, use the snap enable command.

### Using Flatpak Containers

The [flatpak](#9781284254884_Glossary.xhtml_GLOS-107) application container format was created as an independent open source project with no direct ties to any specific Linux distribution. That said, battle lines have already been drawn, with Red Hat-based distributions oriented toward using flatpak instead of Canonical’s snap container format.

If you’re using a Linux distribution that supports flatpak, you can list the installed application containers using the flatpak list command:

![An output shows the list of the installed application containers using the flatpak list command.](images/9781284255805_CH02_CUM44.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-17)

To find an application in the flatpak repository, you use the flatpak search command:

![An output shows the usage of the flatpak search command to find an application in the flatpak repository.](images/9781284255805_CH02_CUM45.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-18)

I edited out some of the information in the output to help simplify things. When working with a container, you must use its Application ID value and not its name. To install the application, use the flatpak install command:

![An output shows the usage of the flatpak install command to install the application.](images/9781284255805_CH02_CUM46.jpg)

![An output shows the usage of the flatpak install command to install the application.](images/9781284255805_CH02_CUM47.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-19)

To check if the installation went well, you can use the flatpak list command again:

![An output shows the usage of the flatpak list command to check if the installation went well.](images/9781284255805_CH02_CUM48.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-20)

And finally, to remove an application container, use the flatpak uninstall command:

![An output shows the usage of the flatpak uninstall command to remove an application container.](images/9781284255805_CH02_CUM49.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-21)

While using application containers is similar to using package management systems, what goes on behind the scenes is fundamentally different. However, the end result is that you have an application installed on your Linux system that can be easily maintained and upgraded.

## Installing from Source Code

Before package management systems and application containers, open source application developers had to distribute their software as source code and allow users to compile the applications on their own systems. Source code packages were commonly released as a [tarball](#9781284254884_Glossary.xhtml_GLOS-333). The tarball package uses the [tar](#9781284254884_Glossary.xhtml_GLOS-332) command to archive multiple files into a single file (either with or without compression).

If you develop or work with open source software source code much, there’s a good chance you will still find software packed up as a tarball. This section walks you through the process of unpacking and installing a tarball software package.

For this example, the software package sysstat will be used. The sysstat utility is a very nice software package that provides a variety of system monitoring tools.

First, you will need to download the sysstat tarball to your Linux system. While you can often find the sysstat package available on different Linux sites, it’s usually best to go straight to the source of the program. In this case, it’s the website sebastien.godard.pagesperso-orange.fr/.

When you click the Download link, you’ll go to the page that contains the files for downloading. The current version at the time of this writing is 12.5.4, and the distribution file name is sysstat-12.5.4.tar.xz.

Click the link to download the file to your Linux system. Once you have downloaded the file, you can unpack it.

To unpack a software tarball, use the standard tar command. Since the file is compressed using the xz program, you must include the -J switch, along with the -x switch to extract the tarball, the -v switch to use verbose mode, and the -f switch to specify the filename:

![An output shows the usage of the standard tar command to unpack a software tarball.](images/9781284255805_CH02_CUM50.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-22)

Now that the tarball is unpacked and the files have neatly put themselves into a directory called sysstat-12.5.4, you can dive down into that directory and continue.

First, use the cd command to get into the new directory and then list the contents of the directory:

![An output uses the c d command to get into the new directory and then list the contents of the directory.](images/9781284255805_CH02_CUM51.jpg)

![none](images/9781284255805_CH02_CUM52.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-23)

In the listing out of the directory, you should typically see a README or INSTALL file. It is very important to read this file. In the file will be the actual instructions you will need to finish the software’s installation.

Following the advice contained in the INSTALL file, the next step is to run the configure utility for your system. This checks your Linux system to ensure it has the proper library dependencies, in addition to the proper compiler to compile the source code:

![An output shows the result of running the configure utility for the system.](images/9781284255805_CH02_CUM53.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-24)

Since the configure utility is located in the local directory, you must use the ./ relative path symbol to run it. If anything does go wrong, the configure step will display an error message explaining what’s missing.

The next stage is to build the various binary files using the make command. The make command compiles the source code and then the linker to create the final executable files for the package. As with the configure command, the make command produces lots of output as it goes through the steps of compiling and linking all of the source code files:

![An output shows the results of the make command.](images/9781284255805_CH02_CUM54.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-25)

When make is finished, you’ll have the actual sysstat software program available in the directory! However, it’s somewhat inconvenient to have to run it from that directory. Instead, you’ll want to install it in a common location on your Linux system. To do that, you’ll need to use the sudo command to obtain root privileges and then use the install option of the make command:

![An output shows the result of using the sudo command and then using the install option of the make command.](images/9781284255805_CH02_CUM55.jpg)

![An output shows the result of using the sudo command and then using the install option of the make command.](images/9781284255805_CH02_CUM56.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd2-26)

Now the sysstat package is installed on the system! While not quite as easy as installing a software package via a package management system, installing software using tarballs is not that difficult.

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 3
Linux and Hardware

ONE OF THE JOBS OF THE OPERATING SYSTEM kernel is to interface with hardware connected to your computer. These days you can connect lots of different types of hardware to a computer, everything from external disk drives to mobile phones. Trying to get Linux working with all of them can be somewhat tricky.

This chapter explores the tools available to get your Linux system to interface with different types of hardware devices. The chapter first explores how the Linux kernel handles the software required to interface with hardware devices. It shows how the idea of modules became invaluable in working with the latest removable devices. Next, the chapter examines how to work with various types of hardware settings, such as interrupts and I/O ports, used in both desktop and server environments to identify hardware. Following that is a section on how Linux works with hotplug devices, especially those using the popular USB interface. With the popularity of the USB interface, it’s crucial that your Linux system can work with them and that you know where to find the utilities on your system.

## Device Driver Modules

One of the main jobs of the Linux operating system is to provide a standard interface for applications to work with hardware. Lots of different types of hardware devices are available, making it impossible for each application to include software to interact with all of them.

Instead, the Linux operating system provides a generic interface to all the different types of hardware that applications can face. Application programmers just need to know how to interface with the Linux system and then Linux takes over from there. This makes tasks such as printing to a printer or writing to a DVD drive much easier for application developers.

Similar to the Microsoft Windows world, the Linux kernel interfaces with hardware devices using what’s called a [device driver](#9781284254884_Glossary.xhtml_GLOS-66). A device driver is a small piece of software written to interact with a specific hardware device. Each device that connects to the Linux system must have a Linux device driver. Fortunately, with the growing popularity of Linux, most hardware manufacturers provide device drivers for their own devices so that Linux users can use the hardware on their Linux systems. There are also a few open source projects for creating device drivers for specific devices where the manufacturer has failed to produce a Linux device driver. This is especially true with printers.

Once you obtain the device driver necessary for the hardware you want to install on your Linux system, there are two ways to include it in the Linux kernel:•

*   Compile it into the kernel software

*   Plug a module into the kernel software

[Compiled device drivers](#9781284254884_Glossary.xhtml_GLOS-52) are device driver software that you must compile directly into the Linux kernel software. This method requires the source code for the device driver as well as the source code for the kernel. When the kernel program is recompiled, you must specify the additional device driver software to include in the kernel.

The downside to compiling device drivers into the kernel is that every time you need to add a new hardware device to your Linux system, you must recompile the entire kernel software program. That can get old after a while, not to mention it’s a great way to introduce bugs into the running kernel!

As a solution, Linux developers created Linux kernel [modules](#9781284254884_Glossary.xhtml_GLOS-206). A kernel module can be inserted into a running kernel at any time without affecting the system operation. Similarly, you can also remove a module from the kernel at any time without affecting other operations of the kernel. This provides the flexibility to install only the device drivers that you need for your system to interact with exactly the hardware you use, without the ugliness of having to recompile the kernel for each device.

Device driver modules are now pretty much the default way of handling hardware devices. Linux systems provide a few different utilities for working with device driver modules from the command line. The following sections walk through the commands that you can use to manage hardware modules in your Linux system.

### Listing Installed Modules

Before you get too far with your Linux system, you may need to determine just what devices it can support by default. Most Linux distributions include a set of pre-installed device driver modules for most common hardware.

You can take a peek at what device modules are already loaded in the Linux kernel by using the lsmod command line command:

![An output shows device modules already loaded in the Linux kernel by using the l s mod command line command.](images/9781284255805_CH03_CUM01.jpg)

![An output shows device modules already loaded in the Linux kernel by using the l s mod command line command.](images/9781284255805_CH03_CUM02.jpg)

![An output shows device modules already loaded in the Linux kernel by using the l s mod command line command.](images/9781284255805_CH03_CUM03.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-1)

The output of the lsmod command has three columns. The Module column shows the name of the module. The Used by column shows the number of other modules or processes that use the module, and what their names are. This helps you determine module dependencies in case you try to remove a module without knowing just what other modules or processes rely on it.

Knowing what device modules your Linux distribution pre-installs can help with troubleshooting hardware issues, as well as giving you an idea of what drivers you’ll need to track down for your specific hardware.

### Installing New Modules

Once you obtain a device driver module file for your hardware you can install it in your Linux system kernel using one of two common commands:

*   insmod

*   modprobe

While each of these commands can insert a module, they each work a little differently. The following sections describe what you’ll need to know to use each command.

#### Using insmod

The [insmod](#9781284254884_Glossary.xhtml_GLOS-150) command inserts a single device module file into the kernel. You must have the device module file copied onto your Linux system to use this command. Most Linux distributions use the /lib/modules folder structure to store module files. If you look in that folder on your Linux system, you’ll see a folder tree structure that separates the device drivers for each kernel version as well as the different types of hardware.

For example, on my Ubuntu Linux server system I have the following folder for Bluetooth hardware drivers:

![Slash lib slash modules slash 5 dot 4 dot 0 hyphen 80 hyphen generic slash kernel slash drivers slash bluetooth.](images/9781284255805_CH03_CUM04.jpg)

This folder is for the currently installed Linux kernel on my system—5.4.0-80\. Inside that folder are lots of different device driver module files for various types of Bluetooth systems:

![An output shows lots of different device driver module files for various types of Bluetooth systems.](images/9781284255805_CH03_CUM05.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-2)

Each .ko file is a separate device driver module file that you can install into the 5.4.0-80 kernel. To install the module, just specify the filename on the insmod command line. Some modules also require parameters, which you must specify on the command line as well:

![Codes show filename specified on the ins mod command line.](images/9781284255805_CH03_CUM06.jpg)

![Codes show filename specified on the ins mod command line.](images/9781284255805_CH03_CUM07.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-3)

To install a module you must have root user privileges on the system, which for most Linux systems that’s done using the sudo command. After you install the module you can check for it using the lsmod program.

#### Using modprobe

The downside to using the insmod program is that you may run into modules that depend on other modules, and the insmod program will fail if those other modules aren’t already installed. To make the process easier, the modprobe command helps resolve module dependencies for you.

Another nice feature of the modprobe command is that it understands module names and will search the module library for the module file that provides the driver for the module name.

Because of this versatility there are lots of options available for the modprobe command. [TABLE 3-1](#9781284254884_CH03_01.xhtml_c3-tab001) shows the command line options that you can use.

TABLE 3-1 The modprobe command options.

| Option | Description |
| --- | --- |
| -a | Insert all modules listed on the command line |
| -b | Apply the blacklist commands specified in the configuration file |
| -C | Specify a different configuration file other than the default |
| -c | Display the current configuration used |
| -d | Specify the root directory to use for installing modules. The default is / |
| -f | Force the module installation even if there are version issues |
| -i | Ignore the install and remove commands specified in the configuration file for the module |
| -n | Perform a dry run of the module install to see if it will work, without actually installing it |
| -q | Quiet mode—doesn’t display any error messages if the module installation or removal fails |
| -r | Remove the module listed |
| -s | Send any error messages to the syslog facility on the system |
| -V | Display the program version and exit |
| -v | Provide additional information (verbose) as the module is processed |

As you can see, the modprobe command is a full-featured tool all by itself. Perhaps the handiest feature is that it allows you to handle modules based on the module name and not have to list the full module filename:

![Codes show the usage of the mod probe command.](images/9781284255805_CH03_CUM08.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-4)

Notice that by adding the –v option for verbose mode the output shows the insmod command automatically generated by the modprobe command. The insmod command shows the specific module file used to install the module.

### Removing Modules

Normally it does no harm to install a module in the system even if the hardware device is not present. The kernel ignores unused modules. However, some Linux administrators prefer to keep the kernel as lightweight as possible, so the Linux developers created a method for removing unnecessary modules—the rmmod command.

However, our friend the modprobe command can also remove modules for us, so you don’t really need to memorize another command. Instead, just use the –r option with the modprobe command:

![Line 1: dollar sudo mod probe hyphen r v b t u s b. Line 2: r m mod b t u s b. Line 3: dollar.](images/9781284255805_CH03_CUM09.jpg)

The modprobe –r command invokes the rmmod command automatically, removing the module by name. You can verify that the module has been removed by using the lsmod command.

## Communicating with Linux Devices

After the kernel module is installed, the kernel must know how to communicate with the device. Linux supports several different types of hardware interfaces and methods for communicating with devices. This section discusses how Linux interacts with different types of devices.

### Device Interfaces

Each device you connect to your Linux system uses some type of standard protocol to communicate with the system hardware. The kernel module software must know how to send data to and receive data from the hardware device using those protocols. Currently, three popular standards are used to connect devices.

#### PCI boards

The [Peripheral Component Interconnect (PCI)](#9781284254884_Glossary.xhtml_GLOS-249) standard was developed in 1993 as a method for connecting hardware boards to PC motherboards. The standard has been updated a few times to accommodate faster interface speeds as well as increase data bus sizes on motherboards. The PCI Express (PCIe) standard is currently used on most server and desktop workstations to provide a common interface for external hardware cards.

Lots of different client devices use PCI boards to connect to a server or desktop workstation:

*   Internal Hard Drives: Hard drives using the older Serial Advanced Technology Attachment (SATA) and the Small Computer System Interface (SCSI) connectors often use PCI boards to connect with workstations or servers. The Linux kernel automatically recognizes both SATA and SCSI hard drives connected to PCI boards. Also, the Linux kernel can automatically recognize the newer Non-Volatile Memory (NvMe) controllers, which are used to connect Solid State Drive (SSD) storage devices.

*   External Hard Drives: Network hard drives using the Fiber Channel standard provide a high-speed shared drive environment for server environments. To communicate on a fiber channel network, the server usually uses PCI boards that support the Host Bus Adapter (HBA) standard.

*   Network Interface Cards: Hard-wired network cards allow you to connect the workstation or server to a local area network using the common RJ-45 cable standard. These types of connections are mostly found in high-speed network environments that require high throughput to the network.

*   Wireless Network Cards: There are PCI boards available that support the IEEE 802.11standard for wireless connections to local area networks. While these are not commonly used in server environments, they are very popular in workstation environments.

*   Bluetooth Devices: The Bluetooth technology allows for short distance wireless communication with other Bluetooth devices in a peer-to-peer network setup. These are most commonly found in workstation environments.

*   Video Accelerators: Applications that require advanced graphics often use video accelerator cards, which offload the video processing requirements from the CPU to provide faster graphics. While these are popular in gaming environments, you’ll also find video accelerator cards used in video processing applications for editing and processing movies.

*   Audio Cards: Similarly, applications that require high-quality sound often use specialty audio cards to provide advanced audio processing and play, such as handling Dolby surround sound to enhance the audio quality of movies.

#### The USB interface

The [Universal Serial Bus (USB)](#9781284254884_Glossary.xhtml_GLOS-348) interface has become increasingly popular due to its ease of use and its increasing support for high-speed data communication. Since the USB interface uses serial communications, it requires fewer connectors with the motherboard, allowing for smaller interface plugs.

The USB standard has evolved over the years. The original version (1.0) only supported data transfer speeds up to 12Mbps. The 2.0 standard increased the data transfer speed to 480Mbps. The current USB standard, 4.0, allows for data transfer speeds up to 40Gbps, making it useful for high-speed connections to external storage devices.

There are a myriad of devices that can connect to systems using the USB interface. You can find hard drives, printers, digital cameras and camcorders, keyboards, mice, and network cards that have versions that connect using the USB interface.

#### The GPIO Interface

The [general purpose input/output](#9781284254884_Glossary.xhtml_GLOS-113) (GPIO) interface has become popular with small utility Linux systems designed for controlling external devices for automation projects. This includes popular hobbyist Linux systems such as the Raspberry Pi and BeagleBone kits.

The GPIO interface provides multiple digital input and output lines that you can control individually, down to the single-bit level. The GPIO function is normally handled by a specialty integrated circuit (IC) chip, which is mapped into memory on the Linux system.

The GPIO interface is ideal for supporting communications to external devices such as relays, lights, sensors, and motors. Applications can read individual GPIO lines to determine the status of switches, turn relays on or off, or read digital values returned from any type of analog-to-digital sensors such as temperature or pressure sensors.

With the GPIO interface, you have a wealth of possibilities for using Linux to control objects and environments. You can write programs that control the temperature in a room, sense when doors or windows are opened or closed, sense motion in a room, or even control the operation of a robot.

### The /dev Directory

After the Linux kernel can communicate with a device on an interface, it must be able to transfer data to and from the device. For many devices, this is done using device files. Device files are files that the Linux kernel creates in the special /dev directory to interface with hardware devices.

To retrieve data from a specific device, a program just needs to read the Linux device file associated with that device. The Linux operating system handles all the unsightliness of interfacing with the actual hardware. Likewise, to send data to the device, the program just needs to write to the Linux device file.

As you add hardware devices such as USB drives, network cards, or hard drives to your system, Linux creates a file in the /dev directory representing that hardware device. Application programs can then interact directly with that file to store and retrieve data on the device. This is a lot easier than requiring each application to know how to directly interact with a device.

There are two types of device files in Linux, based on how Linux transfers data to the device:

*   [Character device files:](#9781284254884_Glossary.xhtml_GLOS-39) Transfer data one character at a time. This method is often used for serial devices such as terminals and USB devices.

*   [Block device files:](#9781284254884_Glossary.xhtml_GLOS-31) Transfer large blocks of data. This method is often used for high-speed data transfer devices such as hard drives and network cards.

Besides device files, Linux also provides a system called the device mapper. The device mapper function is performed by the Linux kernel. It maps physical block devices to virtual block devices. These virtual block devices allow the system to intercept the data written to or read from the physical device and perform some type of operation on them. Mapped devices are used by the Logical Volume Manager (LVM) for creating logical drives and by the Linux Unified Key Setup (LUKS) for encrypting data on hard drives.

### The /proc Directory

The /proc directory is one of the most important tools you can use when troubleshooting hardware issues on a Linux system. It’s not a physical directory on the filesystem but instead a virtual directory that the kernel dynamically populates to provide access to information about the system hardware settings and status.

The Linux kernel changes the files and data in the /proc directory as it monitors the status of hardware on the system. To view the status of the hardware devices and settings, you just need to read the contents of the virtual files using standard Linux text commands.

There are different /proc files available for different system features, including the IRQs, I/O ports, and DMA channels in use on the system by hardware devices. The following sections discuss the files used to monitor these features and how you can access them.

#### Interrupt Requests

[Interrupt requests](#9781284254884_Glossary.xhtml_GLOS-153) (called IRQs) allow hardware devices to indicate when they have data to send to the CPU. The PnP system must assign each hardware device installed on the system a unique IRQ address. You can view the current IRQs in use on your Linux system by looking at the /proc/interrupts file using the Linux cat command:

![An output shows the current interrupt requests using the Linux cat command.](images/9781284255805_CH03_CUM10.jpg)

![An output shows the current interrupt requests using the Linux cat command.](images/9781284255805_CH03_CUM11.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-5)

The first column indicates the IRQ assigned to the device. Some IRQs are reserved by the system for specific hardware devices, such as 0 for the system timer and 1 for the system keyboard. Other IRQs are assigned by the system as devices are detected at boot time.

#### I/O Ports

The system [I/O ports](#9781284254884_Glossary.xhtml_GLOS-138) are locations in memory where the CPU can send data to and receive data from the hardware device. As with IRQs, the system must assign each device a unique I/O port. This is yet another feature handled by the PnP system.

You can monitor the I/O ports assigned to the hardware devices on your system by looking at the /proc/ioports file:

![An output shows the input output ports assigned to the hardware devices.](images/9781284255805_CH03_CUM12.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-6)

There are lots of different I/O ports in use on the Linux system at any time, so your output will most likely differ from this example. With PnP, I/O port conflicts aren’t very common, but it is possible that two devices are assigned the same I/O port. In that case, you can manually override the settings automatically assigned by using the setpci command.

#### Direct memory access

Using I/O ports to send data to the CPU can be somewhat slow. To speed things up, many devices use [direct memory access (DMA)](#9781284254884_Glossary.xhtml_GLOS-71) channels. DMA channels do what the name implies: They send data from a hardware device directly to memory on the system, without having to wait for the CPU. The CPU can then read those memory locations to access the data when it’s ready.

As with I/O ports, each hardware device that uses DMA must be assigned a unique channel number. To view the DMA channels currently in use on the system, just display the /proc/dma file:

![Line 1: dollar cat slash proc slash d m a. Line 2: 4 colon cascade. Line 3: dollar.](images/9781284255805_CH03_CUM13.jpg)

This output indicates that only DMA channel 4 is in use on the Linux system.

### The /sys Directory

Yet another tool available for working with devices is the /sys directory. The /sys directory is another virtual directory, similar to the /proc directory. It provides additional information about hardware devices that any user on the system can access.

There are lots of information files available within the /sys directory. They are broken down into subdirectories based on the device and function in the system. You can take a look at the subdirectories and files available within the /sys directory on your system using the ls command-line command:

![An output shows the subdirectories and files using the l s command line command.](images/9781284255805_CH03_CUM14.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-7)

Notice the different categories of information available. You can obtain information about the system bus, devices, kernel, and even kernel modules installed.

## Working with Devices

Linux provides a wealth of command-line tools for using the devices connected to your system as well as monitoring and troubleshooting the devices if there are problems. The following sections walk through some of the more popular tools you’ll want to know about when working with Linux devices.

### Finding Devices

One of the first tasks for a new Linux administrator is to find the different devices installed on the Linux system. Fortunately there are a few command-line tools to help out with that.

#### The lsdev command

The lsdev command-line command displays information about the hardware devices installed on the Linux system. It retrieves information from the /proc/interrupts, /proc/ioports, and /proc/dma virtual files and combines them in one output:

![An output displays information about the hardware devices using the l s dev command line command.](images/9781284255805_CH03_CUM15.jpg)

![An output displays information about the hardware devices using the l s dev command line command.](images/9781284255805_CH03_CUM16.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-8)

This provides you with one place to view all of the important information about the devices running on the system, making it easier to pick out any conflicts that can be causing problems.

#### The lsblk command

The lsblk command-line command displays information about the block devices installed on the Linux system. By default, the lsblk command displays all the block devices:

![An output displays information about the block devices using the l s b l k command.](images/9781284255805_CH03_CUM17.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-9)

If you notice at the end of output the lsblk command also indicates blocks that are related, as with the device-mapped LVM volumes and the associated physical hard drive. You can modify the lsblk output to see additional information about the blocks by adding command-line options. The -S option displays only information about SCSI block devices on the system:

![An output displays information about S C S I block devices on the system.](images/9781284255805_CH03_CUM18.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-10)

This is a quick way to view the different SCSI drives installed on the system.

#### The dmesg command

The kernel ring buffer records kernel-level events as they occur. In a ring buffer, the buffer area stays the same, so event messages overwrite after the buffer area fills up. You can view the current messages in the kernel ring buffer by using the dmesg command. It helps to monitor it whenever you install a new device:

![An output shows the current messages in the kernel ring buffer by using the d m e s g command.](images/9781284255805_CH03_CUM19.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-11)

The output from the dmesg command shows the steps the kernel took to recognize the new USB device that was plugged into the system.

Because the kernel is responsible for detecting devices and installing the correct modules, the dmesg command is a great troubleshooting tool to use when a device isn’t working correctly. It can help you determine if a hardware device module didn’t load correctly.

### Working with PCI Cards

The lspci command allows you to view the currently installed and recognized PCI and PCIe cards on the Linux system. There are lots of command-line options you can include with the lspci command to display information about the PCI and PCIe cards installed on the system. [TABLE 3-2](#9781284254884_CH03_03.xhtml_c3-tab002) shows the more common ones that come in handy.

TABLE 3-2 The lspci command-line options.

| Option | Description |
| --- | --- |
| -A | Defines the method to access the PCI information |
| -b | Displays connection information from the card point of view |
| -k | Displays the kernel driver modules for each installed PCI card |
| -m | Displays information in machine-readable format |
| -n | Displays vendor and device information as numbers instead of text |
| -q | Queries the centralized PCI database for information about the installed PCI cards |
| -t | Displays a tree diagram that shows the connections between cards and buses |
| -v | Displays additional information (verbose) about the cards |
| -x | Displays a hexadecimal output dump of the card information |

The output from the lspci command without any options shows all devices connected to the system:

![An output shows all devices connected to the system using the l s p c i command.](images/9781284255805_CH03_CUM20.jpg)

![An output shows all devices connected to the system using the l s p c i command.](images/9781284255805_CH03_CUM21.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-12)

You can use the output from the lspci command to troubleshoot PCI card issues, such as if a card isn’t recognized by the Linux system.

### Working with USB Devices

You can view the basic information about USB devices connected to your Linux system by using the lsusb command. [TABLE 3-3](#9781284254884_CH03_03.xhtml_c3-tab003) shows the options that are available with that command.

TABLE 3-3 The lsusb command options.

| Option | Description |
| --- | --- |
| -d | Displays only devices from the specified vendor ID |
| -D | Displays information only from devices with the specified device file |
| -s | Displays information only from devices using the specified bus |
| -t | Displays information in a tree format, showing related devices |
| -v | Displays additional information about the devices (verbose mode) |
| -V | Displays the version of the lsusb program |

Here’s an example of the basic lsusb program output:

![An output of the basic l s u s b program is shown.](images/9781284255805_CH03_CUM22.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd3-13)

Most systems incorporate a standard USB hub for connecting multiple USB devices to the USB controller. Fortunately there are only a handful of USB hubs on the market, so all Linux distributions include the device drivers necessary to communicate with each of these USB hubs. That guarantees that your Linux system will at least detect when a USB device is connected.

## Using Hot Pluggable Devices

Computer hardware is generally categorized into two types:

*   Cold pluggable devices

*   Hot pluggable devices

[Cold pluggable](#9781284254884_Glossary.xhtml_GLOS-46) devices are hardware that can be connected to the system only when the system is completely powered down. These usually include things commonly found inside the computer case, such as memory, PCI cards, and hard drives. You can’t remove any of these things while the system is running.

Conversely, you can usually add and remove [hot pluggable](#9781284254884_Glossary.xhtml_GLOS-136) devices at any time. These are often external components, such as network connections, monitors, and USB devices. The trick with hot pluggable devices is that somehow the Linux kernel needs to know when the device is connected and automatically load the correct device driver module to support the device.

Linux provides an entire subsystem that interacts with hot pluggable devices, making them accessible to users. This subsystem is described in the following sections.

### Detecting Dynamic Devices

The udev device manager is a program that is automatically started at boot time by the init process (usually at run level 5 via the /etc/rc5.d/udev script) or the Systemd systems, and runs in the background at all times. It listens to kernel notifications about hardware devices. As new hardware devices are plugged into the running system, or existing hardware devices removed, the kernel sends out notification event messages.

The udev program listens to these notification messages and compares the messages against rules defined in a set of configuration files, normally stored under the /etc/udev/rules.d directory. If a device matches a defined rule, udev acts on the event notification as defined by the rule.

Each Linux distribution defines a standard set of rules for udev to follow. Rules define actions such as mounting USB memory sticks under the /media folder when they’re installed or disabling network access when a USB network card is removed. You can modify the rules defined, but it’s usually not necessary.

### Working with Dynamic Devices

While the udev program runs in the background on your Linux system, you can still interact with it using the udevadm command-line tool. The udevadm command allows you to send commands to the udev program. The format of the udevadm command is as follows:

![u d e v a d m command open bracket options close bracket.](images/9781284255805_CH03_CUM23.jpg)

[TABLE 3-4](#9781284254884_CH03_04.xhtml_c3-tab004) shows the commands available to send to the udevadm program.

TABLE 3-4 The udevadm commands.

| Command | Description |
| --- | --- |
| control | Modifies the internal state of udev |
| info | Queries the udev database for device information |
| monitor | Listens for kernel events and display them |
| settle | Watches the udev event queue |
| test | Simulates a udev event |
| test-builtin | Runs a built-in device command for debugging |
| trigger | Requests device events from the kernel |

The control command allows you to change the currently running udev program. For example, by adding the -R option, you can force udev to reload the rules defined in the /etc/udev/rules.d directory.

## References

Egidio Docile, “Tutorial on how to write basic udev rules in Linux,” LinuxConfig.org, August 2018, Retrieved October 14, 2021 from [https://linuxconfig.org/tutorial-on-how-to-write-basic-udev-rules-in-linux](https://linuxconfig.org/tutorial-on-how-to-write-basic-udev-rules-in-linux).

Jon Masters, Robby Workman, and Lucas De Marchi, “modprobe,” Ubuntu Manuals, retrieved October 14, 2021 from [http://manpages.ubuntu.com/manpages/trusty/man8/modprobe.8.xhtml](http://manpages.ubuntu.com/manpages/trusty/man8/modprobe.8.xhtml).

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 4
Booting Linux

BEFORE YOU CAN LOG IN AND START using your Linux system, a complicated process of booting the operating system must take place. A lot happens behind the scenes in the Linux boot process. It helps to know just what all goes on in case something goes wrong.

This chapter examines the boot and start up processes in Linux systems. It first takes a look at the role the computer firmware plays in getting the process started. After that, it discusses Linux boot loaders and examines how to configure them. Finally the chapter ends with a discussion about the Linux initialization process, showing how Linux decides which background applications to start at bootup.

## The Linux Boot Process

When you turn on the power to your Linux system, it triggers a series of events that eventually leads to the login prompt. Normally you don’t worry about what happens behind the scenes of those events; you just log in and start using your applications.

However, there may be times when your Linux system doesn’t boot quite correctly, or perhaps an application that you expected to be running in background mode isn’t. In those cases, it helps to have a basic understanding of just how Linux boots the operating system and starts programs so you can troubleshoot the problem.

### Following the Boot Process

The Linux boot process can be split into three steps:

1.  The workstation firmware starts, performing a quick check of the hardware (called a [power-on self-test [POST])](#9781284254884_Glossary.xhtml_GLOS-261), and then looks for a boot loader program to run from a bootable device.

2.  The boot loader runs and determines what Linux kernel program to load.

3.  The kernel program loads into memory and starts the necessary background programs required for the system to operate (such as a graphical desktop manager for desktops, or web and database servers for servers).

While on the surface these three steps may seem simple, there’s a somewhat complicated ballet of operations that happen behind the scenes to keep the boot process working. Each step performs several actions as they prepare your system to run Linux.

### Viewing the Boot Process

You can monitor the Linux boot process by watching the system console screen as the system boots. You’ll see lots of informative messages scroll by as the system detects hardware and loads software.

Sometimes the boot messages scroll by somewhat quickly, and it’s hard to see just what’s happening. If you need to troubleshoot boot problems, you can review the boot time messages using the dmesg command. Most Linux distributions copy the boot kernel messages into a special ring buffer in memory, called the [kernel ring buffer](#9781284254884_Glossary.xhtml_GLOS-166). The buffer is circular, and set to a predetermined size. As new messages are logged in the buffer, older messages are rotated out.

You use the dmesg command displays boot messages currently stored in the kernel ring buffer:

![An output displays boot messages currently stored in the kernel ring buffer using the d m e s g command.](images/9781284255805_CH04_CUM01.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd4-1)

![An output displays boot messages currently stored in the kernel ring buffer using the d m e s g command.](images/9781284255805_CH04_CUM02.jpg)

Most Linux distributions also store the boot messages in a log file, usually in the /var/log folder.

While it helps to be able to see the different messages generated during boot time, it is also helpful to know just what generates those messages. This chapter discusses each of these three boot steps and goes through some examples showing just how they work.

## The Firmware Startup

All workstations and servers utilize some type of built-in firmware to control just how the installed operating system starts. On older workstations and servers this firmware was called the [Basic Input/Output System (BIOS)](#9781284254884_Glossary.xhtml_GLOS-28). On newer workstations and servers, a new method, called the [Unified Extensible Firmware Interface (UEFI)](#9781284254884_Glossary.xhtml_GLOS-344) is responsible for maintaining the system hardware status and launching an installed operating system.

Both methods launch the Linux boot loader but use different methods for doing that. This section walks through the basics of both BIOS and UEFI methods, showing just how they participate in the Linux boot process.

### The BIOS Startup

The BIOS firmware found in older workstations and servers was somewhat limited in what it could do. The BIOS firmware had a simplistic menu interface that allowed you to change some settings to control just how the system found hardware and define what device the BIOS should use to start the operating system.

The BIOS firmware itself could only read one sector’s worth of data from a hard drive into memory to run. As you can probably guess, that’s not enough space to load an entire operating system. This caused most operating systems (including Linux and Microsoft Windows) to split the boot process into two parts.

First, the BIOS runs a [boot loader](#9781284254884_Glossary.xhtml_GLOS-33) program. The boot loader program is a small program that initializes the necessary hardware to find and run the full operating system program, usually located at another location on the same hard drive, but sometimes on a separate internal or external storage device.

The boot loader program usually has a configuration file, so you can tell it just where to look to find the actual operating system file to run, or even to produce a small menu allowing the user to boot between multiple operating systems.

To get things started, the BIOS must know where to find the boot loader program on an installed storage device. Most BIOS setups allow you to load the boot loader program from several locations:

*   An internal hard drive

*   An external hard drive

*   A CD/DVD drive

*   A USB memory stick

*   A network server

When booting from a hard drive, you must designate which hard drive, and partition on the hard drive, the BIOS should load the boot loader program from. This is done by defining a [Master Boot Record (MBR)](#9781284254884_Glossary.xhtml_GLOS-199).

The MBR is the first sector on the first hard drive partition on the system. There is only one MBR for the computer system. The BIOS looks for the MBR and reads the program stored there into memory. When it runs the boot loader program, that program then points to the location of the actual operating system kernel file, stored in a boot sector of a separate partition installed on the system. There are no size limitations on the kernel boot file.

### The UEFI Startup

While there were extreme limitations with BIOS, computer manufacturers learned to live with them, so BIOS became the default standard for workstations and servers for many years. However, as operating systems and hardware became more complicated, it eventually became clear that a new method needed to be developed.

Intel created the [Extensible Firmware Interface (EFI)](#9781284254884_Glossary.xhtml_GLOS-95) in 1998 to address some of the limitations of BIOS. By 2005, the idea caught on with other vendors, and the UEFI specification was adopted as a standard. These days just about all desktop and server systems can support the UEFI firmware standard.

The UEFI firmware can work with MBR formatted hard disks, but also uses a newer format, called GUID Partition Table (GPT). Instead of relying on a single boot sector on a hard drive to hold the boot loader program, GPT specifies a special disk partition, called the [EFI System Partition (ESP)](#9781284254884_Glossary.xhtml_GLOS-84) to store boot loader programs. This allows for any size of boot loader program, plus the ability to store multiple boot loader programs for multiple operating systems.

The ESP setup utilizes the old Microsoft [File Allocation Table (FAT)](#9781284254884_Glossary.xhtml_GLOS-100) filesystem to store the boot loader programs, which restricts the size of the filesystem. On Linux systems, the ESP is typically mounted in the /boot/efi folder, and the boot loader files are typically stored using the .efi filename extension.

The UEFI firmware utilizes a built-in mini boot loader (sometimes referred to as a [boot manager](#9781284254884_Glossary.xhtml_GLOS-34)) that allows you to configure just which boot loader program file to launch.

With UEFI you need to register each individual boot loader file you want to appear at boot time in the boot manager interface menu. You can then select the boot loader to run each time you boot the system.

Once the firmware finds and runs the boot loader, its job is done. The boot loader step in the boot process can be somewhat complicated; the next section dives into covering that.

## Linux Boot Loaders

The boot loader program helps bridge the gap between the system firmware and the full Linux operating system kernel. In Linux there are several choices of boot loaders to use. However, the most popular ones that you’ll run across are the following:

*   [Linux Loader (LILO)](#9781284254884_Glossary.xhtml_GLOS-177)

*   [Grand Unified Boot Loader (GRUB) Legacy](#9781284254884_Glossary.xhtml_GLOS-123)

*   [GRUB2](#9781284254884_Glossary.xhtml_GLOS-126)

In the original versions of Linux the LILO boot loader was the only boot loader program available. It was extremely limited in what it could do, but it accomplished its purpose—loading the Linux kernel from the BIOS startup. LILO became the default boot loader used by Linux distributions in the 1990s. Unfortunately, LILO doesn’t work with GPT disks, so it has limited use on modern systems and is quickly fading into history.

The first version of the GRUB boot loader (now called GRUB Legacy) was created in 1999 to provide a more robust and configurable boot loader to replace LILO. GRUB quickly became the default boot loader for all Linux distributions, whether they were run on BIOS or UEFI systems.

GRUB2 was created in 2005 as a total rewrite of the GRUB Legacy system. It supports advanced features, such as the ability to load hardware driver modules and using logic statements to dynamically alter the boot menu options, depending on conditions detected on the system (such as if an external hard drive is connected).

This section walks through the basics of both the GRUB Legacy and GRUB2 boot loaders, which should cover just about every Linux distribution that you’ll run into these days.

### GRUB Legacy

The GRUB Legacy boot loader was designed to simplify the process of creating boot menus and passing options to kernels. GRUB Legacy allows you to select multiple kernels and/or operating systems using both a menu interface as well as an interactive shell. You configure the menu interface to provide options for each kernel or operating system you want to boot with. The interactive shell provides a way for you to customize boot commands on the fly.

Both methods utilize a set of commands that control features of the boot loader. This section walks through how to configure the GRUB Legacy bootloader, how to install it, and how to interact with it at boot time.

#### Configuring GRUB Legacy

When you use the GRUB Legacy interactive menu, you need to tell it just what options to show. You do that using special GRUB commands.

The GRUB Legacy system stores the menu commands in a standard text file. The configuration file used by GRUB Legacy is called menu.lst and is stored in the /boot/grub folder (while not a requirement, some Linux distributions create a separate /boot partition on the hard drive). Red Hat–derived Linux distributions (such as CentOS and Fedora) use grub.conf instead of menu.lst for the configuration file.

The GRUB Legacy configuration file consists of two sections:

*   Global definitions

*   Operating system boot definitions

The global definitions section defines commands that control the overall operation of the GRUB Legacy boot menu. The global definitions must appear first in the configuration file. There are only a handful of global settings that you can make; [TABLE 4-1](#9781284254884_CH04_03.xhtml_c4-tab001) shows these settings.

TABLE 4-1 GRUB Legacy global commands.

| Setting | Description |
| --- | --- |
| color | Specifies the foreground and background colors to use in the boot menu |
| default | Defines the default menu option to select |
| fallback | A secondary menu selection to use if the default menu option fails |
| hiddenmeu | Don’t display the menu selection options |
| splashimage | Points to an image file to use as the background for the boot menu |
| timeout | Specifies the amount of time to wait for a menu selection before using the default |

For GRUB Legacy, to define a value for a command you just list the value as a command line parameter:

![Line 1: default 0\. Line 2: timeout 10\. Line 3: color white slash blue yellow slash blue.](images/9781284255805_CH04_CUM03.jpg)

The color command defines the color scheme for the menu. The first pair define the foreground/background pair for normal menu entries, while the second pair define the foreground/background pair for the selected menu entry.

After the global definitions, you place definitions for the individual operating systems that are installed on the system. Each operating system should have its own definition section. There are a lot of boot definition settings that you can use to customize how the boot loader finds the operating system kernel file. Fortunately, just a few commands are required to define the operating system. The ones to remember are the following:

*   title—the first line for each boot definition section, this is what appears in the boot menu

*   root—defines the disk and partition where the GRUB /boot folder partition is on the system

*   kernel—defines the kernel image file stored in the /boot folder to load

*   initrd—defines the initial RAM Disk file, which contains hardware drivers necessary for the kernel to interact with the system hardware

*   rootnoverify—defines non-Linux boot partitions, such as Windows

The root command defines the hard drive and partition that contains the /boot folder for GRUB Legacy. Unfortunately, GRUB Legacy uses a somewhat odd way of referencing those values:

![Open parenthesis h d drive comma partition close parenthesis.](images/9781284255805_CH04_CUM04.jpg)

GRUB Legacy doesn’t refer to hard drives the way Linux does; it uses a number system to reference both disks and partitions, starting at 0 instead of 1\. For example, to reference the first partition on the first hard drive on the system, you’d use (hd0,0). To reference the second partition on the first hard drive, you’d use (hd0,1).

Here’s a sample GRUB configuration file that defines both a Windows and a Linux partition for booting:

![A sample G R U B configuration file is shown.](images/9781284255805_CH04_CUM05.jpg)

This example shows two boot options—one for an Ubuntu Linux system and one for a Windows system. The Ubuntu system is installed on the first partition of the second hard drive, while the Windows system is installed on the first partition of the first hard drive.

#### Installing GRUB Legacy

Once you build the GRUB Legacy configuration file (as either menu.lst or grub.conf, depending on your Linux distribution), you must install GRUB in the MBR. The command to do this is grub-install.

The grub-install command uses a single parameter—the partition to install GRUB on. You can specify the partition using either Linux or GRUB Legacy format. For example, to use Linux format you’d use

![Hash space g r u b hyphen install space slash dev slash s d a.](images/9781284255805_CH04_CUM06.jpg)

to install GRUB on the MBR of the first hard drive. To use GRUB Legacy format, you must enclose the hard drive format in quotes:

![Hash space g r u b hyphen install space single quote open parenthesis h d 0 close parenthesis single quote.](images/9781284255805_CH04_CUM07.jpg)

If you’re using the chainloading method and prefer to install a copy of GRUB Legacy on the boot sector of a partition instead of to the MBR of a hard drive, you must specify the partition, again using either Linux or GRUB format:

![Line 1: hash space g r u b hyphen install space slash dev slash s d a 1\. Line 2: hash space g r u b hyphen install space single quote h d open parenthesis 0 comma 0 close parenthesis single quote.](images/9781284255805_CH04_CUM08.jpg)

You don’t need to reinstall GRUB Legacy in the MBR after making changes to the configuration file — GRUB Legacy reads the configuration file each time it runs.

#### Interacting with GRUB Legacy

When you boot a system that uses the GRUB Legacy boot loader you’ll see a menu that shows the boot options you defined in the configuration file. If you wait for the timeout to expire, the default boot option will process. Alternatively, you can use the arrow keys to select one of the boot options, then press the ENTER key to select it.

You can also edit boot options on the fly from the GRUB menu. First, arrow to the boot option you want to modify, then press the E key. A new screen will appear, showing the currently configured options for that entry. Use the arrow key to move the cursor to the line you need to modify, then press the E key to edit it. Press the B key to boot the system using the new values. You can also press the C key at any time to enter an interactive shell mode, allowing you to submit commands on the fly.

### GRUB2

Since the GRUB2 system was intended to be an improvement over GRUB Legacy, many of the features are the same, with just a few twists. For example, the GRUB2 system changes the configuration file name to grub.cfg, and stores it in the /boot/grub/ folder. (This allows you to have both GRUB Legacy and GRUB2 installed at the same time.)

#### Configuring GRUB2

There are also a few changes to the commands used in GRUB2\. For example, instead of the title command, GRUB uses the menuentry command, and you must also enclose each individual boot section with braces immediately following the menuentry command. Here’s an example of a sample GRUB2 configuration file:

![A sample G R U B 2 configuration file is shown.](images/9781284255805_CH04_CUM09.jpg)

![A sample G R U B 2 configuration file is shown.](images/9781284255805_CH04_CUM10.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd4-2)

Notice that GRUB2 uses the set command to assign values to the root keyword as well as uses an equal sign to assign the device. GRUB2 utilizes environment variables to configure settings instead of commands.

To make things more confusing, GRUB2 changes the numbering system for partitions. While it still uses 0 for the first hard drive, the first partition is set to 1\. So to define the /boot folder on the first partition of the first hard drive, you now need to use:

![Set space root space equals space h d open parenthesis 0 comma 1 close parenthesis.](images/9781284255805_CH04_CUM11.jpg)

Also, notice that the rootnoverify and kernel commands are not used in GRUB2. Non-Linux boot options are now defined the same as Linux boot options using the root environment variable, and you define the kernel location using the linux command.

The configuration process for GRUB2 is also somewhat different. While the /boot/grub/grub.cfg file is the configuration file that GRUB2 uses, you should never modify that file. Instead, separate configuration files are stored in the /etc/grub.d folder. This allows you (or the system) to create individual configuration files for each boot option installed on your system (for example, one configuration file for booting Linux, and another for booting Windows).

For global commands, use the /etc/default/grub configuration file. You’ll notice that the format for some of the global commands has changed from the GRUB Legacy commands, such as GRUB_TIMEOUT instead of just timeout.

Most Linux distributions generate the new grub.cfg configuration file automatically after certain events, such as upgrading the kernel.

#### Installing GRUB2

Unlike GRUB Legacy, you don’t need to install GRUB2; all you need to do is rebuild the main installation file. This is done by running the grub-mkconfig program.

The grub-mkconfig program reads configuration files stored in the /etc/grub.d folder and assembles the commands into the single grub.cfg configuration file.

You can update the configuration file manually by running the grub-mkconfig command:

![Hash space g r u b hyphen m k config space greater than space slash boot slash g r u b slash g r u b dot c f g.](images/9781284255805_CH04_CUM12.jpg)

Notice that you must manually redirect the output of the grub-mkconfig program to the grub.cfg configuration file. By default the grub-mkconfig program outputs the new configuration file commands to standard output.

#### Interacting with GRUB2

The GRUB2 boot loader produces a boot menu similar to the GRUB Legacy method. You can use arrow keys to switch between boot options, the E key to edit a boot entry, or the C key to bring up the GRUB2 command line to submit interactive boot commands.

### Alternative Bootloaders

While GRUB Legacy and GRUB2 are the most popular Linux bootloader programs in use, there are still a few others that you may run into, depending on which Linux distributions you use.

The Syslinux project includes five separate bootloader programs that have special uses in Linux:

*   SYSLINUX—a bootloader for systems that use the Microsoft FAT filesystem (popular for booting from USB memory sticks)

*   EXTLINUX—a mini bootloader for booting from an ext2, ext3, ext4, or btrfs filesystem

*   ISOLINUX—a bootloader for booting from a LiveCD or LiveDVD

*   PXELINUX—a bootloader for booting from a network server

*   MEMDISK—a utility to boot older DOS operating systems from the other Syslinux bootloaders

The ISOLINUX bootloader is popular for use in distributions that release a LiveDVD version. The bootloader requires two files: isolinux.bin, which contains the bootloader program image, and isolinux.cfg, which contains the configuration settings.

The PXELINUX bootloader is somewhat complicated. It uses the Pre-boot eXecution Environment (PXE) standard, which defines how a network workstation can boot and load an operating system from a central network server. PXE uses DHCP to assign a network address to the workstation and BOOTP and TFTP to load the bootloader image from the server.

To utilize PXELINUX the TFTP server needs to have the PXELINUX bootloader program, commonly stored as /tftpboot/pxelinux.0, available for the workstations to download. Each workstation must also have a configuration file available in the /tftpboot/pxelinux.cfg folder. The files are named based on the MAC address of the workstation and contain specific configuration settings required for that workstation.

## Process Initialization

A Linux system includes lots of programs running in background to provide services for the system. It’s the [init](#9781284254884_Glossary.xhtml_GLOS-142) program’s job to start all of those programs when the Linux system starts up. This is called the [initialization process](#9781284254884_Glossary.xhtml_GLOS-144).

You must configure the initialization process to start programs based on the desired features you want running in your Linux system. For example, a Linux server doesn’t necessarily need to start a graphical desktop environment, or a Linux desktop doesn’t necessarily need to start the Apache web server service.

While several initialization methods are available in Linux, two have risen to the top and are the most popular used in Linux distributions:

*   Unix System V (also called SysVinit)

*   Systemd

The original Linux init program was based off of the Unix System V init program, and became commonly called [SysVinit](#9781284254884_Glossary.xhtml_GLOS-331). The init program uses a series of shell scripts, divided into separate [runlevels](#9781284254884_Glossary.xhtml_GLOS-296), to determine what programs run at what times. Each program uses a separate shell script to start and stop the program. The system administrator sets which runlevel the Linux system starts in, which in turn determines which set of programs are running. The system administrator can also change the runlevel at any time while the system is running.

The init program had served the Linux community well for many years, but as Linux systems became more complicated and required more services, the runlevel shell scripts have become more complicated. This has caused Linux developers to look for other solutions.

The [systemd](#9781284254884_Glossary.xhtml_GLOS-330) program was developed by the Red Hat Linux distribution to handle dynamic Linux environments. Instead of runlevels it uses targets and units to control what applications run at any time on the system. It uses separate configuration files that determine this behavior.

To find out which method your Linux system uses, use the ps command to display the program assigned process ID (PID) 1:

![An output displays the program assigned process I D using the p s command.](images/9781284255805_CH04_CUM13.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd4-3)

The output from this Ubuntu system shows that it’s running the systemd program. The following sections take a closer look at each of these initialization process methods to help you get comfortable in any Linux environment.

### The SysVinit Method

The key to the SysVinit initialization process is runlevels. The init program determines which programs to start, based on the runlevel of the system.

Runlevels are numbered from 0 to 6, and each one is assigned a set of programs that should be running for that runlevel. When the Linux kernel starts, it determines which runlevel to start by a configuration file. It’s important to know how to manage runlevels and how to determine when each runlevel is used by the kernel. The following sections show how to do just that.

#### Runlevels

While each Linux distribution defines applications that should be running at specific runlevels, you can use some general guidelines. [TABLE 4-2](#9781284254884_CH04_04.xhtml_c4-tab002) shows the general use of the Linux runlevels.

TABLE 4-2 Linux runlevels.

| Runlevel | Description |
| --- | --- |
| 0 | Shut down the system |
| 1 | Single-user mode. Used for system maintenance. |
| 2 | On Debian-based systems, multi-user graphical mode |
| 3 | On Red Hat-based systems, multi-user text mode |
| 4 | Undefined |
| 5 | On Red Hat–based systems, multi-user graphical mode |
| 6 | Reboot the system |

Most Linux distributions use the Red-Hat runlevel method of using runlevel 3 for multi-user text mode and runlevel 5 for multi-user graphical mode.

#### Starting applications in a runlevel

There are two ways to start applications in runlevels:

*   Using the /etc/inittab file

*   Using startup scripts

The /etc/inittab file defines what applications start at which runlevel. Each line in the /etc/inittab file defines an application and uses the following format:

![I d colon run levels colon action colon process.](images/9781284255805_CH04_CUM14.jpg)

The id field contains one to four characters that uniquely defines the process. The runlevels field contains a list of runlevels in which the application should be running. The list is not comma separated, so the value 345 indicates the application should be started in runlevels 3, 4, and 5.

The action field contains a keyword that tells the kernel what to do with the application for that runlevel Possible values are shown in [TABLE 4-3](#9781284254884_CH04_04.xhtml_c4-tab003).

TABLE 4-3 The SysV inittab action values.

| Action | Description |
| --- | --- |
| boot | The process is started at boot time. |
| bootwait | The process is started at boot time and the system will wait for it to finish. |
| initdefault | The runlevel to enter after the system boots is specified. |
| kbrequest | The process is started after a special key combination is pressed. |
| once | The process is started once when the runlevel is entered. |
| powerfail | The process is started when the system is powered down. |
| powerwait | The process is started when the system is powered down, and the system will wait for it to finish. |
| respawn | The process is started when the runlevel is entered and restarted whenever it terminates. |
| sysinit | The process is started at boot time before any boot or bootwait items. |
| wait | The process is started once and the system will wait for it to finish. |

The initdefault line specifies the runlevel that the system normally runs in after boot:

![I d colon 3 colon init default colon.](images/9781284255805_CH04_CUM15.jpg)

Besides the runlevels, the SysVinit method also specifies startup scripts to control how applications start and stop. The /etc/init.d/rc or /etc/rc.d/rc script runs all scripts with a specified runlevel. The scripts themselves are stored in the /etc/init.d/rcx.d or /etc/rcx.d folders, where x is the runlevel number.

Scripts are stored with a specific filename that specifies whether they start or stop at the runlevel. Scripts that start with an S start the program, and scripts that start with a K stop it. The script filenames also contain a number, which indicates the order the rc program runs the scripts. This allows you to specify which scripts get started before others to control any dependency issues.

#### Checking the runlevel

You’ve seen that the /etc/inittab file indicates the default runlevel with the initdefault action; however, there’s no guarantee that’s the runlevel your Linux system is currently running at. The runlevel command displays both the current runlevel and the previous runlevel for the system:

![Line 1: dollar run level. Line 2: N 2\. Line 3: dollar.](images/9781284255805_CH04_CUM16.jpg)

The first character is the previous runlevel. The N character means the system is in the original boot runlevel. The second character is the current runlevel.

#### Changing Runlevels

You can change the current runlevel of your Linux system using either the init or telinit command. Just specify the runlevel number as the command line parameter. For example, to reboot your system you can enter the command:

![Hash space init space 6.](images/9781284255805_CH04_CUM17.jpg)

The downside to using the init command is that it immediately changes the system to the specified runlevel. That may not be an issue if you’re the only person on your Linux system, but in a multi-user Linux environment that can have adverse effects for the other users.

A kinder way to change the runlevel on multi-user systems is to use one of a handful of special commands used just for that purpose:

*   shutdown—Gracefully changes the runlevel to 1, or single-user mode

*   halt—Gracefully changes the runlevel to 0 to stop the system

*   poweroff—Gracefully changes the runlevel to 0 to stop the system

*   reboot—Gracefully changes the runlevel to 6 to restart the system

Each of these commands also allow you to specify a message to send to any other users on the system before it changes the runlevel. You can also specify a time for the change, such as +15 for 15 minutes, along with a message to send to other users.

### The Systemd Method

The systemd initialization process method has quickly become a standard. While it started out as a Red Hat feature, now most Linux distributions have adopted it as their default initialization method.

The systemd initialization process introduced a major paradigm shift in how Linux systems handle services, which has also caused some controversy in the Linux world. Instead of lots of small initialization shell scripts, the systemd method uses one monolithic program that uses individual configuration files for each service. This is somewhat of a departure from earlier Linux philosophy.

This section walks through the basics of how the systemd initialization process works.

#### Units and targets

Instead of using shell scripts and runlevels, the systemd method uses [units](#9781284254884_Glossary.xhtml_GLOS-345) and [targets](#9781284254884_Glossary.xhtml_GLOS-334). A unit defines a service or action on the system. It consists of a name, a type, and a configuration file. There are currently 12 different types of systemd units:

*   automount

*   device

*   mount

*   path

*   scope

*   service

*   slice

*   snapshot

*   socket

*   swap

*   target

*   timer

The systemd program identifies units by their name and type using the format name.type. You use the systemctl command when working with units. To list the units currently loaded in your Linux system, use the list-units parameter:

![An output shows the units currently loaded in Linux system using the list hyphen units parameter.](images/9781284255805_CH04_CUM18.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd4-4)

Linux distributions can have hundreds of different units loaded and active, this listing shows just a few from the output to show you what they look like. The systemd method uses service type units to manage the daemons on the Linux system. The target type units are important in that they group multiple units together so they can be started at the same time. For example, the network.target unit groups all the units required to start the network interfaces for the system.

The systemd initialization process uses targets similar to the way SysV runlevels. Each target represents a different group of services that should be running on the system. Instead of changing runlevels to alter what’s running on the system, you just change targets.

To make the transition from SysV to systemd smoother, there are targets that mimic the standard 0 through 6 SysV runlevels, called runlevel0.target through runlevel6.target.

#### Configuring units

Each unit requires a configuration file that defines what program it starts and how it should start the program. The systemd system stores unit configuration files in the /usr/lib/systemd/system folder. Here’s an example of the cron.service unit configuration file used in Ubuntu:

![An example of the cron dot service unit configuration file used in Ubuntu.](images/9781284255805_CH04_CUM19.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd4-5)

The cron.service configuration file defines the program to start (/usr/sbin/cron), along with some other features, such as what services should run before the cron service starts (the After line), what target level the system should be in (the WantedBy line), and how to reload the program (the Restart line).

Target units also use configuration files. They don’t define programs but, instead, define which service units to start. Here’s an example of the graphical.target unit configuration file used in CentOS:

![An example of the graphical dot target unit configuration file used in Cent O S.](images/9781284255805_CH04_CUM20.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd4-6)

The target configuration defines what targets should be loaded first (the After line), what targets are required for this target to start (the Requires line), what targets conflict with this target (the Conflicts line), and what targets or services the target requires to be running (the Wants line).

#### Setting the default target

The default target used when the Linux system boots is defined as the file default.target, located in the /usr/lib/systemd/system folder. This is the file the systemd program looks for when it starts up. This file is normally set as a link to a standard target file also in the /usr/lib/systemd/system folder:

![Code for setting a file as a link to a standard target file is shown.](images/9781284255805_CH04_CUM21.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd4-7)

On this Ubuntu system, the default target is set to the graphical.target unit.

You can also see the default target for the system by using the systemctl command:

![Line 1: dollar system c t l get hyphen default. Line 2: graphical dot target. Line 3: dollar.](images/9781284255805_CH04_CUM22.jpg)

This again shows that the graphical.target target is the default.

#### The systemctl program

You use the systemctl program to also control services and targets. The systemctl program uses options to define what action to take, as shown in [TABLE 4-4](#9781284254884_CH04_04.xhtml_c4-tab004).

TABLE 4-4 The systemctl commands.

| Command name | Explanation |
| --- | --- |
| get-default | Displays the default target configured for the system |
| list-units | Displays the current status of all configured units |
| default name | Changes to the default target unit |
| isolate name | Starts the named unit and stops all others |
| start name | Starts the named unit |
| stop name | Stops the named unit |
| reload name | Causes the named unit to reload its configuration file |
| restart name | Causes the named unit to shut down and restart |
| status name | Displays the status of the named unit (You can pass a PID value rather than a name, if you like.) |
| enable name | Configures the unit to start when the computer next boots |
| disable name | Configures the unit to not start when the computer next boots |

Instead of using shell scripts to start and stop services, you use the start and stop commands:

![An output shows the usage of the system c t l commands.](images/9781284255805_CH04_CUM23.jpg)

![An output shows the usage of the system c t l commands.](images/9781284255805_CH04_CUM24.jpg)

![An output shows the usage of the system c t l commands.](images/9781284255805_CH04_CUM25.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd4-8)

To change the target that is currently running, you must use the isolate command. For example, to enter single-user mode you’d use:

![Hash space system c t l space isolate space rescue dot target.](images/9781284255805_CH04_CUM26.jpg)

To go back to the default target for the system, you just use the default command.

One of the more controversial features of the systemd initialization process is that it doesn’t use the standard Linux syslogd log file system. Instead, it has its own log files, and those log files are not stored in text format. To view the systemd log files, you need to use the journalctl program.

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 5
Disk Management

SOME PEOPLE ARE AFRAID to use Linux because they do not understand how to use or find their drives. With some of the earlier versions of Linux, people would insert an external disk such as a USB thumb drive and it wouldn’t pop up on the screen like it does in Microsoft Windows. This caused a great deal of frustration for novice Linux users. If people cannot find or use their storage, they will not feel comfortable using the operating system.

There have been many enhancements to the Linux operating system over the years that make it much easier to work with disks. Linux has an extensive number of command-line and graphical user interface tools for managing disks. Though having experience with Linux disks gives you an advantage; you don’t have to be an expert in Linux to use these tools. An extensive development of disk management tools for Linux makes it easy for even the most novice user.

The control, reliability, and predictability of the way Linux handles disks have made the operating system one of the primary choices of people performing computer forensic acquisitions, which involves making an image of a disk. After reading this chapter, you will have a better understanding of how Linux assigns drive device names and what all of the [drive letters](#9781284254884_Glossary.xhtml_GLOS-78) and number destinations, such as sdb2 and sde3, mean. The drive letter designations may initially seem more difficult to understand, but as you will learn, the process by which the Linux operating system assigns them is logical and predictable.

The Linux operating system supports many different filesystem types. Linux has its own filesystems, such as ext2, ext3, ext4, and btrfs, and it can support a large number of other filesystems including FAT32 and [New Technology File System (NTFS)](#9781284254884_Glossary.xhtml_GLOS-231), the primary filesystems used by Microsoft Windows operating systems. The versatility of Linux and its support for a large number of filesystems have helped contribute to the increase in overall market share.

If you want to use the Linux operating system effectively, you need to have an understanding of how disks are accessed and managed. This chapter will explore the various aspects of disk management in Linux. Understanding the convention that Linux uses for disks and knowing the commands that are used to interact with storage devices are critical knowledge for anyone who wants to use  Linux effectively.

## Storage Basics

The most common way to persistently store data on computer systems is using a [hard disk drive (HDD)](#9781284254884_Glossary.xhtml_GLOS-129). Hard disk drives are physical devices that store data using a set of disk platters that spin around, storing data magnetically on the platters with a moveable read/write head that writes and retrieves magnetic images on the platters.

These days another popular type of persistent storage is called a [solid-state drive (SSD)](#9781284254884_Glossary.xhtml_GLOS-316). These drives use integrated circuits to store data electronically. There are no moving parts contained in SSDs, making them faster and more resilient than HDDs. While currently SSDs are more expensive than HDDs, technology is quickly changing that, and it may not be long before HDDs are a thing of the past.

Linux handles both HDD and SSD storage devices the same way. It mostly depends on the connection method used to connect the drives to the Linux system. This section describes the different methods that Linux uses in connecting and using both HDD and SSD devices.

### Drive Connections

While HDDs and SSDs differ in the way they store data, they both interface with the Linux system using the same methods. There are three main types of drive connections that you’ll run into with Linux systems:

*   [Parallel Advanced Technology Attachment (PATA)](#9781284254884_Glossary.xhtml_GLOS-244) connects drives using a parallel interface, which require a wide connector. PATA supports two devices per adapter.

*   [Serial Advanced Technology Attachment (SATA)](#9781284254884_Glossary.xhtml_GLOS-303) connects drives using a serial interface, but at a much faster speed than PATA. SATA supports up to four devices per adapter.

*   [Small Computer System Interface (SCSI)](#9781284254884_Glossary.xhtml_GLOS-310) connects drives using a parallel interface, but with the speed of SATA. SCSI supports up to eight devices per adapter.

*   Non-Volatile Memory Express (NVMe) connects solid state drives using a parallel interface for maximum data transfer speeds. The NVMe standard supports up to 12 devices per adapter.

When you connect a drive to a Linux system, the Linux kernel assigns the drive device a file in the /dev directory. That file is called a [raw device](#9781284254884_Glossary.xhtml_GLOS-279), as it provides a path directly to the drive from the Linux system. Any data written to the file is written to the drive, and reading the file reads data directly from the drive.

For PATA devices, this file is named /dev/hdx, where x is a letter representing the individual drive, starting with a. For SATA and SCSI devices, Linux uses /dev/sdx,  where x is a letter representing the individual drive, again, starting with a. Thus, to reference the first SATA device on the system, you’d use /dev/sda, then for the second device /dev/sdb, and so on.

### Partitioning Drives

Most storage devices allow you to partition the device into multiple sections. A [partition](#9781284254884_Glossary.xhtml_GLOS-246) is a self-contained section within the drive that the operating system treats as a separate storage space.

Partitioning drives can help you better organize your data, such as segmenting ­operating system data from user data. If a rogue user fills up her /home disk space with data, the operating system will still have room to operate on the separate partition.

Partitions must be tracked by some type of indexing system on the drive. Systems that use the old BIOS boot loader method (see Chapter 4) use the [Master Boot Record (MBR)](#9781284254884_Glossary.xhtml_GLOS-199) method for managing disk partitions. This method only supports up to four [primary ­partitions](#9781284254884_Glossary.xhtml_GLOS-262) on a drive. Alternatively, you can create one or more [extended partitions](#9781284254884_Glossary.xhtml_GLOS-94), which can be split into multiple partitions.

Systems that use the UEFI boot loader method (see Chapter 4) use the more advanced [GUID Partition Table (GPT)](#9781284254884_Glossary.xhtml_GLOS-127) method for managing partitions, which supports up to 128 partitions on a drive. Linux assigns the partition numbers in the order that the partition appears on the drive, starting with number 1.

Linux creates /dev files for each separate disk partition. It attaches the partition number to the end of the device name, and numbers the primary partitions starting at 1, so the first primary partition on the first SATA drive would be /dev/sda1. MBR extended partitions are numbered starting at 5, so the first extended partition is assigned the file /dev/sda5.

### Automatic Drive Detection

Linux systems detect drives and partitions at boot time and assigns each one a unique device file name. However, with the invention of removable USB drives (such as memory sticks), which can be added and removed at will while the system is running, that method needed to be modified.

Most Linux systems now use the udev application. The udev program runs in the background at all times and automatically detects new hardware connected to the ­running Linux system. As you connect new drives, USB devices, or optical drives (such as CD and DVD devices), udev will detect them and assign each one a unique device file name in the /dev directory.

Another feature of the udev application is that it also creates [persistent device files](#9781284254884_Glossary.xhtml_GLOS-250) for storage devices. When you add or remove a removable storage device, the /dev name assigned to it may change, depending on what devices are connected at any given time. That can make it difficult for applications to find the same storage device each time.

To solve that problem, the udev application uses the /dev/disk directory to create links to the /dev storage device files based on unique attributes of the drive. There are four separate directories udev creates for storing links:

*   /dev/disk/by-id—Links storage devices by their manufacturer make, model, and serial number

*   /dev/disk/by-label—Links storage devices by the label assigned to them

*   /dev/disk/by-path—Links storage devices by the physical hardware port they are connected to

*   /dev/disk/by-uuid—Links storage devices by the 128-bit Universal Unique Identifier (UUID) assigned to the device.

With the udev device links you can specifically reference a storage device by a ­permanent identifier rather than were or when it was plugged into the Linux system.

## Partitioning Tools

After you connect a drive to your Linux system, you’ll need to create partitions on it (even if there’s only one partition). Linux provides several tools for working with raw storage devices to create partitions. This section covers the most popular partitioning tools you’ll run across in Linux.

### Working with fdisk

The most common command line partitioning tool is the fdisk utility. The fdisk ­program allows you to create, view, delete, and modify partitions on any drive that uses the MBR method of indexing partitions; it can’t work with GPT indexed partitions.

To use the fdisk program, you must specify the drive device name (not the partition name) of the device you want to work with:

![Codes show the usage of the f disk program.](images/9781284255805_CH05_CUM01.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd5-1)

The fdisk program uses its own command line that allows you to submit commands to work with the drive partitions. [TABLE 5-1](#9781284254884_CH05_02.xhtml_c5-tab001) shows the common commands you have ­available to work with.

Table 5-1 Common fdisk commands.

| COMMAND | DESCRIPTION |
| --- | --- |
| a | toggle a bootable flag |
| b | edit bsd disklabel |
| c | toggle the DOS compatibility flag |
| d | delete a partition |
| g | create a new empty GPT partition table |
| G | create an IRIX (SGI) partition table |
| l | list known partition types |
| m | print this menu |
| n | add a new partition |
| o | create a new empty DOS partition table |
| p | print the partition table |
| q | quit without saving changes |
| s | create a new empty Sun disklabel |
| t | change a partition’s system id |
| u | change display/entry units |
| v | verify the partition table |
| w | write table to disk and exit |
| x | extra functionality (experts only) |

The p command displays the current partition scheme on the drive:

![An output shows the current partition scheme on the drive using the p command.](images/9781284255805_CH05_CUM02.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd5-2)

In this example, the /dev/sda drive is sectioned into two partitions, sda1 and sda2. The Id and System columns refer to the type of [file system](#9781284254884_Glossary.xhtml_GLOS-101) the partition is formatted to handle. Both partitions are formatted to support a Linux file system. The first partition is allocated about 1GB of space, while the second is allocated a little over 9GB of space.

The fdisk command is somewhat rudimentary in that it doesn’t allow you to alter the size of an existing partition; all you can do is delete the existing partition and rebuild it from scratch.

To be able to boot the system from a partition the boot flag must be set for the partition. You do that with the a command. The bootable partitions are indicated in the output ­listing with an asterisk.

If you make any changes to the drive partitions, you must exit using the w command to write the changes to the drive.

### Working with gdisk

If you’re working with drives that use the GPT indexing method, you’ll need to use the gdisk program:

![An output works with drives that use the G P T indexing method using the g disk program.](images/9781284255805_CH05_CUM03.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd5-3)

The gdisk program identifies the type of formatting used on the drive. If the drive doesn’t currently use the GPT method, gdisk offers you the option to convert it to a  GPT drive.

The gdisk program also uses its own command prompt, allowing you to enter ­commands to manipulate the drive layout, as shown in [TABLE 5-2](#9781284254884_CH05_02.xhtml_c5-tab002).

TABLE 5-2 Common gdisk commands.

| COMMAND | DESCRIPTION |
| --- | --- |
| b | back up GPT data to a file |
| c | change a partition’s name |
| d | delete a partition |
| i | show detailed information on a partition |
| l | list known partition types |
| n | add a new partition |
| o | create a new empty GUID partition table (GPT) |
| p | print the partition table |
| q | quit without saving changes |
| r | recovery and transformation options (experts only) |
| s | sort partitions |
| t | change a partition’s type code |
| v | verify disk |
| w | write table to disk and exit |
| x | extra functionality (experts only) |
| ? | print this menu |

You’ll notice that many of the gdisk commands are similar to those in the fdisk program, making it easier to switch between the two programs.

### The GNU parted Command

The GNU parted program provides yet another command line interface for working with drive partitions:

![An output provides command line interface for working with drive partitions using the G N U parted command.](images/9781284255805_CH05_CUM04.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd5-4)

![An output provides command line interface for working with drive partitions using the G N U parted command.](images/9781284255805_CH05_CUM05.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd5-5)

One of the selling features of the parted program is that it allows you to modify ­existing partition sizes, so you can easily shrink or grow partitions on the drive.

### Graphical Tools

There are also some graphical tools available to use if you’re working from a graphical desktop environment. The most common of these is the GNOME Partition Editor, called gparted. [FIGURE 5-1](#9781284254884_CH05_02.xhtml_c5-fig001) shows an example of running gparted in an Ubuntu desktop ­environment.

![A screenshot shows the g parted interface.](images/9781284255805_CH05_FIGF01.jpg)

FIGURE 5-1 The gparted interface.

Courtesy of Gparted.

[Description](9781284254884_Alt.xhtml_summary-fig5-1)

The gparted window displays each of the drives on a system one at a time, showing all of the partitions contained in the drive in a graphical layout. You right-click a partition to select options for [mounting](#9781284254884_Glossary.xhtml_GLOS-210) or unmounting, formatting, deleting, or resizing the partition.

While it’s certainly possible to interact with a drive as a raw device, that’s not usually how Linux applications work. There’s a lot of work trying to read and write data to a raw device. Instead, Linux provides a method for handling all of the dirty work for us, which is covered in the next section.

## Understanding File Systems

Just like a storing stuff in a closet, storing data in a Linux system requires some method of organization for it to be efficient. Linux utilizes file systems to manage data stored on ­storage devices. A file system utilizes a method of maintaining a map to locate each file placed in the storage device. This section describes the Linux file system and shows how you can locate files and directories contained within it.

The Linux file system can be one of the most confusing aspects of working with Linux. Locating files on drives, CDs, and USB memory sticks can be a challenge at first.

If you’re familiar with how Windows manages files and directories, you know that Windows assigns drive letters to each storage device you connect to the system. For example, Windows uses C: for the main drive on the system, or E: for a USB memory stick plugged into the system.

In Windows, you’re used to seeing file paths such as:

![C colon backslash Users backslash rich backslash Documents backslash test dot doc x.](images/9781284255805_CH05_CUM06.jpg)

This path indicates the file is located in the Documents directory for the rich user account, which is stored on the disk partition assigned the letter C (usually the first drive on the system).

The Windows path tells you exactly what physical device the file is stored on. ­Unfortunately, Linux doesn’t use this method to reference files. It uses a virtual directory structure. The virtual directory contains file paths from all the storage devices installed on the system, consolidated into a single directory structure.

### The Virtual Directory

The Linux virtual directory structure is a way of organizing files and directories ­regardless of their physical location. It contains a single base directory, called the [root directory](#9781284254884_Glossary.xhtml_GLOS-292), which lists files and directories beneath it based on the directory path used to get to them, similar to the way Windows does it.

For example, a Linux file path could look like this:

![Slash home slash rich slash Documents slash test dot doc.](images/9781284255805_CH05_CUM07.jpg)

First, note that the Linux path uses forward slashes instead of the backward slashes that Windows uses. That’s an ­important difference that trips many novice Linux ­administrators. As for the path itself, also notice that there’s no drive letter. The path only indicates that the file test.doc is stored in the Documents directory for the user rich; it doesn’t give you any clues as to which physical device contains the file.

Linux places physical devices in the virtual directory using mount points. A [mount point](#9781284254884_Glossary.xhtml_GLOS-209) is a directory placeholder within the virtual directory that points to a specific ­physical device. [FIGURE 5-2](#9781284254884_CH05_03.xhtml_c5-fig002) demonstrates how this works.

![A chart shows the Linux virtual directory structure divided between two drives.](images/9781284255805_CH05_FIGF02.jpg)

FIGURE 5-2 The Linux virtual directory structure divided between two drives.

[Description](9781284254884_Alt.xhtml_summary-fig5-2)

In [Figure 5-2](#9781284254884_CH05_03.xhtml_c5-fig002), there are two partitions used on the Linux system. One partition is ­associated with the root of the virtual directory (indicated by the single forward slash). The second partition is mounted at the location /home, which is where the user ­directories are located. Once the second partition is mounted to the virtual directory, files and directories stored on the partition are available under the /home directory.

Since Linux stores everything within the virtual directory, it can get somewhat complicated. Fortunately, there’s a standard format defined for the Linux virtual directory, called the Linux [file system hierarchy standard (FHS)](#9781284254884_Glossary.xhtml_GLOS-102). The FHS defines core directory names and locations that should be present on every Linux system and what type of data they should contain. [TABLE 5-3](#9781284254884_CH05_03.xhtml_c5-tab003) shows just a few of the more common directories defined in the FHS.

TABLE 5-3 Common Linux FHS directories.

| DIRECTORY | DESCRIPTION |
| --- | --- |
| /boot | Contains bootloader files used to boot the system |
| /home | Contains user data files |
| /media | Used as a mount point for removable devices |
| /mnt | Also used as a mount point for removable devices |
| /opt | Contains data for optional third-party programs |
| /tmp | Contains temporary files created by system users |
| /usr | Contains data for standard Linux programs |
| /usr/bin | Contains local user programs and data |
| /usr/local | Contains data for programs unique to the local installation |
| /usr/sbin | Contains data for system programs and data |

### Maneuvering Around the File System

Using the virtual directory makes it a breeze to move files from one physical device to another. You don’t need to worry about drive letters, just the locations within the ­virtual directory:

![Dollar space c p space slash home slash rich slash Documents slash my file dot t x t space slash media slash u s b.](images/9781284255805_CH05_CUM08.jpg)

The full path to a file lists each directory within the virtual directory structure to walk your way down to find the file. This format is called an [absolute path](#9781284254884_Glossary.xhtml_GLOS-13). The absolute path to a file always starts at the root directory (/), and includes every directory along the virtual directory tree to the file.

Alternatively, you can use a [relative path](#9781284254884_Glossary.xhtml_GLOS-284) to specify a file location. The relative path to a file denotes the location of a file relative to your current location within the virtual ­directory tree structure. If you were already in the Documents directory, you’d just need to type the following:

![Dollar space c p space my file dot t x t space slash media slash u s b.](images/9781284255805_CH05_CUM09.jpg)

When Linux sees that the path doesn’t start with a forward slash, it assumes the path is relative to the current directory.

## Formatting File Systems

Before you can assign a drive partition to a mount point in the virtual directory, you must format it using a file system. Linux supports a myriad of different file system types, with each having different features and capabilities. This section discusses the different file systems that Linux supports and how to format a drive partition for the file systems.

### Common File System Types

Each operating system utilizes its own file system type for storing data on drives. Linux not only supports several of its own file system types, but it also supports file systems of other operating systems. This section covers the most common Linux and non-Linux file systems that you can use in your Linux partitions.

#### Linux file systems

When you create a file system specifically for use on a Linux system, you can choose from four main file systems:

*   [btrfs](#9781284254884_Glossary.xhtml_GLOS-35)—A newer, high-performance file system that supports files up to 16 EiB in size, and a total file system size of 16 EiB. It also can perform its own form of [Redundant Array of Independent Disks (RAID)](#9781284254884_Glossary.xhtml_GLOS-281) as well as [logical volume management (LVM)](#9781284254884_Glossary.xhtml_GLOS-183). It includes additional advanced features such as built-in snapshots for backup, improved fault-tolerance, and data compression on the fly.

*   [ecryptfs](#9781284254884_Glossary.xhtml_GLOS-83)—The Enterprise Cryptographic File System (eCryptfs) applies a POSIX-compliant encryption protocol to data before storing it on the device. This provides a layer of protection for data stored on the device. Only the operating system that created the file system can read data from it.

*   [ext3](#9781284254884_Glossary.xhtml_GLOS-92)—Also called ext3fs, this is a descendant of the original Linux ext file system. It supports files up to 2TiB, with a total file system size of 16TiB. It supports [journaling](#9781284254884_Glossary.xhtml_GLOS-161) as well as faster startup and recovery.

*   [ext4](#9781284254884_Glossary.xhtml_GLOS-93)—Also called ext4fs, it’s the current version of the original Linux file system. It supports files up to 16TiB, with a total file system size of 1EiB. It also supports journaling, and utilizes improved performance features.

*   [reiserFS](#9781284254884_Glossary.xhtml_GLOS-282)—Created before the Linux ext3fs file system and commonly used on older Linux systems, it provides features now found in ext3fs and ext4fs. Linux has dropped support for the most recent version, reiser4fs.swap: The [swap](#9781284254884_Glossary.xhtml_GLOS-323) file system allows you to create virtual memory for your system using space on a physical drive. The system can then swap data out of normal memory into the swap space, ­providing a method of adding additional memory to your system. This is not intended for storing persistent data.

The default file system used by many Linux distributions these days is ext4fs. The ext4fs file system provides journaling, which is a method of tracking data not yet written to the drive in a log file, called the journal. If the system fails before the data can be written to the drive, the journal data can be recovered and stored upon the next system boot.

#### Non-Linux file systems

One of the great features of Linux that makes it so versatile is its ability to read data stored on devices formatted for other operating systems, such as Apple and Microsoft. This ­feature makes it a breeze to share data between different systems running different ­operating systems.

Here’s a list of the more common non-Linux file systems that Linux can handle:

*   HFS—The [Hierarchical File System (HFS)](#9781284254884_Glossary.xhtml_GLOS-133) was developed by Apple for its macOS systems. Linux can also interact with the more advanced HFS+ file system.

*   ISO-9660—The [ISO-9660](#9781284254884_Glossary.xhtml_GLOS-158) standard is used for creating file systems on CD-ROM devices.

*   NTFS—The New Technology File System (NTFS) is the file system used by the Microsoft NT operating system and subsequent versions of Windows. Linux can read and write data on an NTFS partition as of kernel 2.6.x.

*   UDF—The [Universal Disc Format (UDF)](#9781284254884_Glossary.xhtml_GLOS-347) is commonly used on DVD-ROM devices for storing data. Linux can both read data from a DVD and write data to a DVD using this file system.

*   VFAT—The Virtual File Allocation Table (VFAT) is an extension of the original Microsoft File Allocation Table (FAT) file system. It’s not commonly used on drives but is commonly used for removable storage devices such as USB memory sticks.

*   XFS—The X File System (XFS) was created by Silicon Graphics for their (now defunct) advanced graphical workstations. The file system provided some advanced high-performance features that makes it still popular in Linux.

*   ZFS—The Zettabyte File System (ZFS) was created by Sun Microsystems (now part of Oracle) for its Unix workstations and servers. Another high-performance file system, it has features similar to the btrfs Linux file system.

While these are all filesystems that originated outside of Linux, many are commonly used in Linux distributions, such as the xfs and zfs filesystems.

### Creating File Systems

The Swiss army knife for creating file systems in Linux is the mkfs program. The mkfs program is actually a frontend to several individual tools for creating specific file systems, such as the mkfs.ext4 program for creating ext4 file systems. Fortunately, you don’t need to remember all the individual programs; just specify the filesystem type in the mkfs command, and it automatically runs the correct program.

The beauty of the mkfs program is that you only need to remember one program name to create any type of file system on your Linux system. Just use the -t option to specify the file system type:

![An output shows the usage of the m k f s program with hyphen t option to specify the file system type.](images/9781284255805_CH05_CUM10.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd5-5)

Just specify the partition device file name for the partition you want to format on the command line. Notice that the mkfs ­program does a lot of things behind the scenes when formatting the file system. Each file system has its own method for indexing files and directories and tracking file access. The mkfs program creates all of the index files and tables necessary for the specific file system.

## Mounting File Systems

Once you’ve formatted a drive partition with a file system, you can add it to the [virtual directory](#9781284254884_Glossary.xhtml_GLOS-356) file system on your Linux system. This process is called mounting the file system.

You can either manually mount the partition within the virtual directory structure from the command line, or you can allow Linux to automatically mount the partition at boot time. This section walks through both of these methods.

### Manually Mounting Devices

To temporarily mount a file system to the Linux virtual directory, use the mount ­command. The basic format for the mount command is:

![mount space hyphen f space f s type space device space mountpoint.](images/9781284255805_CH05_CUM11.jpg)

Use the -f command line option to specify the file system type of the device:

![Line 1: dollar sudo mount hyphen t e x t 4 space slash dev slash s d b 1 space space media space u s b 1\. Line 2: dollar.](images/9781284255805_CH05_CUM12.jpg)

If you specify the mount command with no parameters, it displays all the devices ­currently mounted on the Linux system. Be prepared for a long output though, as most Linux distributions mount lots of virtual devices in the virtual directory to provide ­information about system resources. Here’s a partial output from a mount command:

![A partial output from a mount command is shown.](images/9781284255805_CH05_CUM13.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd5-6)

To save space I trimmed down the output from the mount command to show only the physical devices on the system. The main hard drive device (/dev/sda) contains two partitions, and the USB memory stick device (/dev/sdb) also contains two partitions.

The downside to the mount command is that it only ­temporarily mounts the device in the virtual directory. When you reboot the system, you have to manually mount the devices again. This is usually fine for removable devices, such as USB memory sticks, but for more permanent devices, it would be nice if Linux could mount them for us automatically. Fortunately for us, Linux can do just that.

To remove a mounted drive from the virtual directory, use the umount command (note the missing “n”). You can remove the mounted drive by specifying either the device file name or the mount point directory.

### Automatically Mounting Devices

For permanent storage devices, Linux maintains the /etc/fstab file to indicate which drive devices should be mounted to the virtual directory at boot time. The  /etc/fstab file is a table that indicates the drive device file (either the raw file or one of its permanent udev file names), the mount point location, the file system type, and any additional options required to mount the drive. Here’s an example of the /etc/fstab file from an Ubuntu workstation:

![An example of the slash e t c slash f s tab file from an Ubuntu workstation is shown.](images/9781284255805_CH05_CUM14.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd5-7)

This /etc/fstab file references the devices by their udev UUID value, ensuring the correct drive partition is accessed no matter what order it appears in the raw device table. The first partition is mounted at the /boot/efi mount point in the virtual directory. The second ­partition is mounted at the root (/) of the virtual ­directory, and the third partition is mounted as a swap area for ­virtual ­memory.

You can manually add devices to the /etc/fstab file so that they are mounted automatically when the Linux ­system boots. However, if they don’t exist at boot time, that will ­generate a boot error.

## Managing File Systems

Once you’ve created a file system and mounted it to the virtual directory you may have to manage and maintain it to keep things running smoothly. This section walks through some of the Linux utilities available for managing the file systems on your Linux system.

### Retrieving File System Stats

As you use your Linux system, there’s no doubt that at some point you’ll need to monitor disk performance and usage. There are a few different tools available to help you do that:

*   df—Displays disk usage by partition

*   du—Displays disk usage by directory; good for finding users or applications that are taking up the most disk space

*   iostat—Displays a real-time chart of disk statistics by partition

*   lsblk—Displays current partition sizes and mount points

In addition to these tools, the /proc and /sys directories are special file systems that the kernel uses for recording system statistics. Two directories that can be useful when working with file systems are the /proc/partitions and /proc/mounts ­directories, which provide information on system partitions and mount points, respectively. Additionally, the /sys/block directory contains separate directories for each mounted drive, showing ­partitions and kernel-level stats.

Some file systems, such as ext3 and ext4, allocate a specific number of inodes when created. An inode is an entry in the index table that tracks files stored on the file system. If the file system runs out of inode entries in the table, you can’t create any more files, even if there’s available space on the drive. Using the -i option with the df command will show you the percentage of inodes used on a file system and can be a lifesaver.

### File System Tools

Linux uses the e2fsprogs package of tools to provide utilities for working with ext file systems (such as ext3 and ext4). The following are the most popular tools in the e2fsprogs package:

*   blkid—Display information about block devices, such as storage drives

*   chattr—Change file attributes on the file system

*   debugfs—Manually view and modify the file system structure, such as undeleting a file or extracting a corrupt file

*   dumpe2fs—Displays block and superblock group information

*   e2label—Change the label on the file system

*   resize2fs—Expand or shrink a file system

*   tune2fs—Modify file system parameters

These tools help you fine-tune parameters on an ext file system, but if corruption occurs on the file system, you’ll need the fsck program.

The XFS file system also has a set of tools available for tuning the file system. You’ll most likely run across the following two:

*   xfs_admin—Display or change file system parameters such as the label or UUID assigned

*   xfs_info—Display information about a mounted file system, including the block sizes and sector sizes, as well as label and UUID information

While these ext and XFS tools are useful, they can’t help fix things if the file system itself has errors. For that, the fsck program is the tool to use:

![An output shows the usage of the f s c k program.](images/9781284255805_CH05_CUM15.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd5-8)

The fsck program is a front end to several different programs that check the ­ ­various file systems to match the index against the actual files stored in the file system. If any ­discrepancies occur, run the fsck program and it will attempt to reconcile the ­discrepancies and fix the file system.

## Storage Alternatives

Standard partition layouts on storage devices do have their limitations. Once you create and format a partition, it’s not easy making it larger or smaller. Individual partitions are also susceptible to disk failures, in which case all of the data stored in the partition will be lost.

To accommodate more dynamic storage options, as well as fault-tolerance features, Linux has incorporated a few advanced storage management techniques. This section covers three of the more popular techniques you’ll run into.

### Multipath

The Linux kernel now supports Device Mapper Multipathing (DM-multipathing), which allows you to configure multiple paths between the Linux system and storage devices. With Multipathing the kernel can either combine the paths, providing for increased throughput while all of the paths are active, or use a path for fault-tolerance if one of the paths becomes inactive.

The Linux DM-multipathing tools include the following:

*   dm-multipath—The kernel module that provides multipath support

*   multipath—A command line command for viewing multipath devices

*   multipathd—A background process for monitoring paths and activating/deactivating paths

*   kpartx—A command line tool for creating device entries for multipath storage devices

The dm-multipath feature uses the dynamic /dev/mapper device file directory in Linux. Linux creates a /dev/mapper device file named mpathN for each new ­multipath storage device you add to the system, where N is the number of the multipath drive. That file acts as a normal device file to the Linux system, allowing you to create partitions and file systems on the multipath device just as you would a normal drive partition.

### Logical Volume Manager

The Linux Logical Volume Manager (LMV) also utilizes the /dev/mapper dynamic device directory to allow you to create virtual drive devices. You can aggregate multiple ­physical drive partitions into virtual volumes, which you then treat as a single partition on your system.

The benefit of LVM is that you can add and remove physical partitions as needed to a logical volume, expanding and shrinking the logical volume as needed.

Using LVM is somewhat complicated. [FIGURE 5-3](#9781284254884_CH05_07.xhtml_c5-fig003) demonstrates the layout for an LVM environment.

![An illustration shows the layout for the Linux L V M environment.](images/9781284255805_CH05_FIGF03.jpg)

FIGURE 5-3 The Linux LVM layout.

[Description](9781284254884_Alt.xhtml_summary-fig5-3)

In the example shown in [Figure 5-3](#9781284254884_CH05_07.xhtml_c5-fig003), three physical drives each contain three ­partitions. The first logical volume consists of the first two partitions of the first drive. The second logical volume spans drives, combining the third partition of the first drive, with the first and second partitions of the second drive to create one volume. The third logical volume consists of the third partition of the second drive, and the first two partitions of the third drive. The third partition of the third drive is left ­unassigned, and can be added later to any of the logical volumes when needed.

For each physical partition, you must mark the partition type as the Linux LVM file ­system type in fdisk or gdisk. Then, you must use several LVM tools to create and manage the logical volumes:

*   pvcreate—Creates a physical volume

*   vgcreate—Groups physical volumes into a volume group

*   lvcreate—Creates a logical volume from partitions in each physical volume

The logical volumes create entries in the /dev/mapper directory, which represent the LVM device you can format with a file system and use like a normal partition.

While the initial setup of a LVM is complicated, it does provide great benefits. If you run out of space in a logical volume, just add a new disk partition to the volume.

### Using RAID Technology

RAID technology allows you to improve data access performance and reliability as well as implement data redundancy for fault-tolerance by combining multiple drives into one virtual drive. Several versions of RAID are commonly used:

*   [RAID 0](#9781284254884_Glossary.xhtml_GLOS-273)—Disk striping, spreads data across multiple disks for faster access

*   [RAID 1](#9781284254884_Glossary.xhtml_GLOS-274)—Disk mirroring, duplicates data across two drives

*   [RAID 10](#9781284254884_Glossary.xhtml_GLOS-275)—Disk mirroring and striping: provides striping for performance, and mirroring for fault-tolerance

*   [RAID 4](#9781284254884_Glossary.xhtml_GLOS-276)—Disk striping with parity, adds a parity bit stored on a separate disk so that data on a failed data disk can be recovered

*   [RAID 5](#9781284254884_Glossary.xhtml_GLOS-277)—Disk striping with distributed parity, adds a parity bit to the data stripe so that it appears on all of the disks so that any failed disk can be recovered

*   [RAID 6](#9781284254884_Glossary.xhtml_GLOS-278)—Disk striping with double parity stripes both the data and the parity bit so two failed drives can be recovered

If your storage hardware doesn’t support RAID, Linux has implemented a software RAID system that can implement RAID features on any disk system.

The mdadm utility allows you to specify multiple partitions to be used in any type of RAID environment. The RAID device appears as a single device in the /dev/mapper directory, which you can then partition and format to a specific file system.

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 6
Command Line Basics

IF YOU’RE USING A LINUX desktop distribution that uses a graphical desktop, it’s easy to launch programs, view files and folders, and manage system programs, all from the graphical desktop interface. However, the real power of Linux comes from working directly with the Linux kernel. To do that, you’ll need to learn about the Linux command line interface (CLI).

The CLI provides an interactive way for a user on the Linux system to access the Linux kernel. It prompts you for commands and then sends the commands to the Linux kernel for processing. Of course there are plenty of security restrictions in place, so that you’re only allowed to do what the system administrator allows you to do (unless of course you are the system administrator, in which case you can do everything).

This chapter walks through the basic features of the command line. First it shows just how to get to the command line. There are different ways to get to the command line, depending on whether you’re using a graphical desktop environment or a server console. Next the chapter discusses the basics of finding your way around the shell, such as getting help for commands, and recovering previously entered commands. After that, the chapter presents a brief discussion on redirecting input and output in the [shell](#9781284254884_Glossary.xhtml_GLOS-306)—a popular topic for storing data to a file or reading data from a file. After a brief discussion on using variables in the Linux shell, the chapter finishes up by walking through how to create shell scripts to help automate your everyday administration tasks.

## The Linux Shell

A Linux [shell](#9781284254884_Glossary.xhtml_GLOS-306) is a special program that is the middleman between the user and the Linux kernel. It uses an interactive [command line interface (CLI)](#9781284254884_Glossary.xhtml_GLOS-49) that allows you to send commands to the Linux kernel, load applications to run, and receive messages from both the kernel and applications.

There are basically two actions that the shell allows users to perform from the CLI:

*   Run internal shell commands

*   Launch external programs

The shell itself has a set of built-in commands that provide different types of information to the user. These [internal commands](#9781284254884_Glossary.xhtml_GLOS-151) range from allowing you to log out from the system to controlling how your user account creates files on the system. The shell is an integral part of working with the Linux kernel, and it comes in handy knowing how to use it.

[External commands](#9781284254884_Glossary.xhtml_GLOS-96) include the GNU utilities that are included with Linux systems as well as any application programs, such as desktop and server programs.

This section takes a closer look at the Linux shell and how the CLI provides a basic interface for you to use to communicate with the Linux kernel.

### Types of Shells

As with everything else in the Linux world, there are multiple types of shells available for you to use on your Linux system. Some Linux distributions only install one shell by default, while others install multiple shells, allowing you to experiment with which ones you like best.

The most common Linux shells that you’ll run into are the following:

*   bash—The original Linux shell, created to duplicate the Unix Bourne shell

*   dash—An improvement of bash, created by the Debian developers, used in Ubuntu Linux

*   ash—A simplified version of bash for low-powered desktops

*   tcsh—An improvement over the original csh shell that supports C-style programming

*   ksh—The Korn shell, popular in many Unix distributions, but not as popular in Linux

*   zsh—The Z shell, which provides plugin modules for advanced network and math features

As you can see, the different shells provide different features for users and programmers. For example, tcsh is a programming-oriented shell, providing C program language features that help programmers create scripts to automatically process data and control programs from the shell. Another popular shell used by script programmers is zsh, which uses separate plugin modules to provide advanced mathematical equation processing, and even network communication support!

By far the most common shell in Linux is bash. It’s available in all Linux distributions and is what all Linux certification exams focus on. That’s the shell that this book focuses on.

### Starting the Shell

The shell that the system starts for your session depends on your user account configuration. The /etc/passwd file contains a list of all the system user accounts, along with some basic configuration information about each user. Here’s a sample entry from a /etc/passwd file:

![rich colon x colon 501 colon 501 colon Rich Blum colon slash home slash rich colon slash bin slash bash.](images/9781284255805_CH06_CUM01.jpg)

Each entry has seven data fields, with each field separated by a colon. The system uses the data in these fields to assign specific features for the user:

*   The username

*   The user’s password (or a placeholder if the password is stored in another file)

*   The user’s system user ID number

*   The user’s system group ID number

*   The user’s full name

*   The user’s default home directory

*   The user’s default shell program

Most Linux systems use bash as the default shell when starting a CLI environment for the user.

The bash program also uses command line parameters to modify the type of shell you can start. [TABLE 6-1](#9781284254884_CH06_01.xhtml_c6-tab001) lists the command line parameters available in bash that define what type of shell to use.

Table 6-1 The bash command line parameters.

| PARAMETER | DESCRIPTION |
| --- | --- |
| -c string | Read commands from the specified string and process them |
| -r | Start a restricted shell, limiting the user to only the default directory |
| -i | Start an interactive shell, allowing input from the user |
| -s | Read commands from the standard input |

By default, when bash starts, it automatically processes commands in the .bashrc file, located in the user’s home directory. Many Linux distributions use this file to also load a common file that contains commands and settings for everyone on the system. This common file is normally located in the file /etc/bashrc. This file often sets environment variables (described later in this chapter) used in various applications.

### The Shell Command Prompt

Once you start a shell the CLI displays a [command prompt](#9781284254884_Glossary.xhtml_GLOS-50). The command prompt is your interactive gateway to the shell. This is the place where you enter shell commands.

The default prompt symbol for the bash shell is the dollar sign ($). This symbol indicates that the shell is waiting for you to enter text. However, you can change the format of the prompt used by your shell. The different Linux distributions use different formats for the prompt. In the Ubuntu Linux system, the command prompt looks like this:

![rich at ubuntu 02 space tilde dollar.](images/9781284255805_CH06_CUM02.jpg)

You can configure the prompt to provide basic information about your environment. The first example above shows three pieces of information in the prompt:

*   The username that started the shell (rich)

*   The hostname of the system (ubuntu02)

*   The current directory (the tilde sign is shorthand for the home directory)

There are two environment variables that control the format of the command line prompt:

*   PS1—Controls the format of the default command line prompt

*   PS2—Controls the format of the second-tier command line prompt

The shell uses the default PS1 prompt for initial data entry into the shell. If you enter a command that requires additional information, the shell displays the second-tier prompt specified by the PS2 environment variable.

To display the current settings for your prompts, use the echo command:

![Line 1: dollar echo dollar P S 1\. Line 2: backslash u at backslash h space backslash W dollar. Line 3: dollar echo dollar P S 2\. Line 4: greater than. Line 5: dollar.](images/9781284255805_CH06_CUM03.jpg)

The format of the prompt environment variables can look pretty odd. The shell uses special characters to signify elements within the command line prompt. [TABLE 6-2](#9781284254884_CH06_01.xhtml_c6-tab002) shows the special characters that you can use in the prompt string.

TABLE 6-2 bash shell prompt characters.

| CHARACTER | DESCRIPTION |
| --- | --- |
| \a | The bell character |
| \d | The date in the format “Day Month Date” |
| \e | The ASCII escape character |
| \h | The local hostname |
| \H | The fully qualified domain hostname |
| \j | The number of jobs currently managed by the shell |
| \l | The basename of the shell’s terminal device name |
| \n | The ASCII newline character |
| \r | The ASCII carriage return |
| \s | The name of the shell |
| \t | The current time in 24-hour HH:MM:SS format |
| \T | The current time in 12-hour HH:MM:SS format |
| \@ | The current time in 12-hour am/pm format |
| \u | The username of the current user |
| \v | The version of the bash shell |
| \V | The release level of the bash shell |
| \w | The current working directory |
| \W | The basename of the current working directory |
| \! | The bash shell history number of this command |
| \# | The command number of this command |
| \$ | A dollar sign if a normal user, or a pound sign if the root user |
| \nnn | The character corresponding to the octal value nnn |
| \\ | A backslash |
| \[ | Begins a control code sequence |
| \] | Ends a control code sequence |

Notice that all of the special prompt characters begin with a backslash (\). This is what delineates a prompt character from normal text in the prompt. In the earlier example, the prompt contained both prompt characters and a normal character (the “at” sign and the square brackets). You can create any combination of prompt characters in your prompt. To create a new prompt, just assign a new string to the PS1 variable:

![A new string is assigned to the P S 1 variable.](images/9781284255805_CH06_CUM04.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-1)

This new shell prompt now shows the current time, along with the username. The new PS1 definition only lasts for the duration of the shell session. When you start a new shell, the default shell prompt definition is reloaded. For the change to be permanent, you can place the PS1 assignment in the .bashrc file in your home directory.

## Accessing the Command Line

In the early days of Linux, the only way to access the system was via a hard-wired text-based terminal, called a console. All interaction with the Linux system had to be through the console device. Not only was that the only way to interact with the Linux system, it was also the only way for the system to display any system error messages.

Modern-day Linux systems use virtual terminals and terminal emulators to interact with users and administrators. This section describes both methods for getting to the CLI on your Linux system.

### Using Virtual Terminals

With modern Linux systems, when the Linux system starts it automatically creates several virtual terminals, also called virtual consoles. A virtual terminal is a CLI session that runs in memory on the Linux system. Instead of having several dumb terminals connected to the computer, most Linux distributions start seven (or sometimes even more) virtual terminals that you can access from the single keyboard and monitor.

In most Linux distributions, you can access the virtual terminals using a simple keystroke combination. Usually you must hold down either the Alt key, or the Ctrl+Alt key combination, and then press a function key (F1 through F8) for the virtual terminal session you want to use. Function key F1 produces virtual terminal 1, key F2 produces virtual terminal 2, and so on. [FIGURE 6-1](#9781284254884_CH06_02.xhtml_c6-fig001) shows a virtual terminal used in the Rocky Linux distribution.

![A screenshot shows the full screen text login in virtual terminal 1 for Rocky Linux.](images/9781284255805_CH06_FIGF01.jpg)

FIGURE 6-1 The full-screen text login in virtual terminal 1 for Rocky Linux.

Courtesy of Rocky Enterprise Software Foundation.

[Description](9781284254884_Alt.xhtml_summary-fig6-1)

The virtual terminal prompts you for your user account and password. After logging in with your user ID and password, you are taken to the Linux bash shell CLI. In the Linux virtual terminal, you do not have the ability to run any graphical programs directly. You can only run text programs that display output on the Linux text console.

After logging in to a virtual terminal, you can switch to another virtual terminal session without losing your existing active session. You can switch between all of the virtual terminals, with multiple active sessions running.

With Linux server systems, all you have available are the text-oriented virtual terminal console sessions. However, with Linux desktop distributions, usually the first or the last virtual terminals is reserved for an X Window graphical desktop. You may have to test which virtual terminal runs the graphical desktop on your Linux system by trying Ctrl+Alt+F1 and Ctrl+Alt+F7 to see which one your particular distribution uses.

Most distributions automatically switch to one of the graphical virtual consoles after the boot sequence completes, providing a complete graphical login and desktop experience.

If you log into a desktop virtual terminal and want to switch to a graphical desktop, often you can run the startx command to start the X Window system and the graphical desktop environment. Logging in to a text virtual terminal session and then switching over to a graphical one can get tedious though.

Fortunately, there’s a better way to jump between graphical and text mode on the Linux system. Terminal emulation packages are a popular way to access the shell CLI from within a graphical desktop session.

### Terminal Emulation

A terminal emulation package provides a CLI contained within a window in a graphical desktop environment. You don’t need to switch to a separate virtual terminal to access the CLI. The terminal emulation package emulates the console operation within the window, allowing you to enter data into the CLI using the keyboard, and displaying the output from the CLI in the window.

There are three basic terminal emulation packages used in Linux:

*   xterm

*   Konsole

*   GNOME Terminal

The Konsole package is created specifically for KDE desktop environments, and the GNOME Terminal package is created (obviously) for the GNOME desktop environment. The xterm package is a generic package that doesn’t have as many features as the other two but is popular with Linux distributions designed to run on older hardware, such as LUbuntu.

In the Rocky Linux GNOME desktop you can launch the GNOME Terminal program by selecting the Terminal menu entry from the System application area. In Ubuntu, to start GNOME Terminal you’ll need to use the Dash interface and search for it by name. Once you start Terminal, you can right-click on it and add it to the Launcher on the left-hand side of the desktop for easier access.

[FIGURE 6-2](#9781284254884_CH06_02.xhtml_c6-fig002) shows the GNOME Terminal program running on an Ubuntu desktop.

![A screenshot shows the Terminal program running on an Ubuntu desktop.](images/9781284255805_CH06_FIGF02.jpg)

FIGURE 6-2 The Terminal program running on an Ubuntu desktop.

Courtesy of Canonical Ltd.

[Description](9781284254884_Alt.xhtml_summary-fig6-2)

Terminal allows you to run multiple terminal emulation sessions using tabs. You can have multiple tabs open, each one being a separate virtual session. You can right-click in the tab window to see the quick menu. This quick menu provides a few actions for your use in the tab session:

*   Copy—Copy highlighted text in the current session tab to the clipboard

*   Paste—Paste data in the clipboard into the current session tab at the current cursor location

*   Read-Only—Sets the tab so that no input is accepted

*   Preferences—Allows you to set features of the terminal, such as color scheme, fonts, and scrolling

*   New Window—Starts a new Terminal session in a new window

*   New Tab—Starts a new Terminal session in another tab in the same window

*   Show Menubar—Toggles on/off the menu bar display

Now that you can get to the shell CLI, you’re ready to get started with some commands. First, let’s take a look at how to enter commands into the CLI and how you can modify commands.

## Shell Basics

Now that you’ve seen what the shell is, and how to interact with it, let’s take a look at some of the shell features. This section walks through some of the features available in most Linux shells.

### Commands

As mentioned earlier, the Linux shell allows you to perform two types of functions—run a built-in command and launch an external program. The external programs that you can launch must be accessible from the Linux system—either installed directly on a hard drive or removable media device or available on a network shared drive.

If you’re ever in doubt about a program, you can use the type shell built-in program. The type program provides quick information about a command or application, such as whether or not it’s a shell builtin command or an external program:

![Line 1: dollar type c d. Line 2: c d is a shell builtin. Line 3: dollar.](images/9781284255805_CH06_CUM05.jpg)

That’s a handy way to get basic information about a file.

If you launch a text-based application, the virtual terminal from where you launched the program becomes the interface with the program. Output from the program appears on the virtual terminal monitor, and input for the program is taken from the keyboard. These are called the [standard output](#9781284254884_Glossary.xhtml_GLOS-319) and [standard input](#9781284254884_Glossary.xhtml_GLOS-318) for the shell. You can run multiple programs from different virtual terminals, each one using the input and output for its respective virtual terminal. Later on you’ll see how to redirect input and output with other sources, which can come in handy when you run programs in background mode.

You can launch a graphics-based application from the CLI, but the results depend on how the CLI was started. When you launch a graphics-based application, it looks for a graphical desktop environment to run in. In a text-mode console environment, no graphical desktop environment is available, so usually the program will terminate and complain. If you’re using a terminal emulation package from inside a graphical desktop, the graphical program you launch will appear in the graphical desktop, just as if you had launched it directly from the desktop.

### Getting Help

The Linux shell has several layers of [help](#9781284254884_Glossary.xhtml_GLOS-131) available to help make things easier for you. The first layer is the help command. The help command displays information about the built-in shell commands. You can get a list of the available built-in commands in your shell by typing help itself at the command prompt, as shown in [FIGURE 6-3](#9781284254884_CH06_03.xhtml_c6-fig003).

![An output shows a list of the available built in commands using the help command.](images/9781284255805_CH06_FIGF03.jpg)

FIGURE 6-3 The help command output.

[Description](9781284254884_Alt.xhtml_summary-fig6-3)

You can get help on a specific built-in command by entering the command name after the help command in the CLI:

![Help space c p.](images/9781284255805_CH06_CUM06.jpg)

The next layer of help is the [man](#9781284254884_Glossary.xhtml_GLOS-196) program. The man program displays canned documentation provided by the application developers, as long as the documentation is installed on your Linux system. There’s an official format for man pages, which helps you quickly find the information you’re looking for. The information in the man page is divided into separate headings. While there are some standard headings defined, there’s no requirement for each man page to include information in all of the headings. You may see any of these common headings in a man page:

*   Name—Provides the programs name, and any aliases that it may have

*   Synopsis—Provides a quick review of what the program does

*   Description—Provides a longer explanation of how the program works

*   Options—Describes any command line options available

*   Arguments—Describes any option arguments required

*   Files—Lists the files required for the program, including configuration files

*   Examples—Shows an example of how to use the program

*   See Also—Refers to similar programs

*   History—Provides details on when the program was created and the different versions

*   Copyright—Lists the copyright status of the program

*   Bugs—Lists any known bugs

The man pages are also organized into separate sections, numbered from 1 through 8\. Each section stores man pages for different types of programs. The main sections to know are section 1, which stores user-level program pages, section 2 for system calls, section 3 for library functions, and section 8 for administrator-level program pages. To specify a section, just list it in the man command:

![Dollar space man space 1 space grep.](images/9781284255805_CH06_CUM07.jpg)

A command related to the man command is [apropos](#9781284254884_Glossary.xhtml_GLOS-19). This fancy-named command looks up the specified term in all of the man pages and returns the man pages that reference the term.

The third layer of help available is the [info](#9781284254884_Glossary.xhtml_GLOS-140) program. The info program is the replacement for the man program, and has advanced features, such as linked pages. It displays information in a tree-like structure, allowing you to peruse through separate branches in the information tree. Each article can have links to related info pages for other commands, similar to browsing webpages. Implementation of info pages has been somewhat slow, so you may not find any information in the info pages for some applications. [FIGURE 6-4](#9781284254884_CH06_03.xhtml_c6-fig004) shows the example of the info page for the Linux grep command.

![A screenshot shows the info page for the Linux grep command.](images/9781284255805_CH06_FIGF04.jpg)

FIGURE 6-4 The info page for the Linux grep command.

[Description](9781284254884_Alt.xhtml_summary-fig6-4)

### Shell Features

A few features that are built into the shell can help out with your command line operations. One is the [history file](#9781284254884_Glossary.xhtml_GLOS-134). The history file keeps track of the commands you enter into the shell.

You can recover, modify, and use commands from the history file using the arrow keys. The Up arrow key retrieves the most recently used command from the history file. Hitting the Up arrow key again retrieves the second-most recently used command. If you continue hitting the Up arrow key, the shell continues retrieving commands from the history file in reverse order from when you entered them. Likewise, you can use the Down arrow to go back up through the history file list.

Once you enter a command or retrieve a previous command in the command line, you can modify the command using several different key combinations. Numerous editing commands are available in bash; [TABLE 6-3](#9781284254884_CH06_03.xhtml_c6-tab003) shows the more popular ones to remember:

TABLE 6-3 Shell command line editing commands.

| COMMAND | DESCRIPTION |
| --- | --- |
| Left arrow | Move the cursor to the left in the command text |
| Right arrow | Move the cursor to the right in the command text |
| Ctrl+a | Move the cursor to the beginning of the command text |
| Ctrl+e | Move the cursor to the end of the command text |
| Delete | Remove the character at the cursor location |
| Backspace | Remove the character before the cursor location |
| Ctrl+t | Transpose two characters |
| Ctrl+k | Remove (kill) the characters from the cursor position to the end of the command text into a buffer |
| Ctrl+y | Yank the characters from the buffer back into the command text |

You can also jump directly to a specific previously entered command if you know what position it has in the history file using the history command. Just specify the command location as a number after the history command. For example, to retrieve the command you ran three commands ago, use:

![Dollar space history space 3.](images/9781284255805_CH06_CUM08.jpg)

Finally, [command completion](#9781284254884_Glossary.xhtml_GLOS-48) is another handy shell feature. It searches for commands that match the text that you’re already typed in the command prompt interface. For example, if you’re not sure about the spelling of a command or program, you can type in a few letters and then just hit the Tab key. The shell searches the matching commands and programs and displays them, allowing you to select the command you want to use.

### Running Multiple Commands

One exciting feature of the Linux command line is that you can enter multiple commands on the same command line and Linux will process them all! Just place semicolons between each command you enter:

![Semicolon is entered between multiple commands.](images/9781284255805_CH06_CUM09.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-2)

The Linux shell runs the first command (date) and displays the output, then it runs the second command (who) and displays the output from that command, immediately following the output from the first command. While this may seem trivial, that is the basis of how [shell scripts](#9781284254884_Glossary.xhtml_GLOS-307) work and can be a very powerful tool to have!

## Redirecting Input and Output

There are times when you’d like to save the output from a command instead of just having it displayed on the monitor. The shell provides a few different operators that allow you to redirect the output of a command to an alternative location (such as a file). Redirection can be used for input as well as output, redirecting a file to a command for input. This section describes what you need to use redirection in the CLI.

### Output Redirection

The most basic type of redirection is sending output from a command to a file; this is called [output redirection](#9781284254884_Glossary.xhtml_GLOS-239). Bash uses the greater-than symbol for this:

![Command space greater than space output file.](images/9781284255805_CH06_CUM10.jpg)

Anything that would appear on the monitor from the command instead is stored in the output file specified:

![An output from a command is stored in the output file specified.](images/9781284255805_CH06_CUM11.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-3)

The redirect operator created the file test1 and redirected the output from the date command to the file. If the output file already exists, the redirect operator overwrites the existing file with the new file data:

![The redirect operator overwrites the existing file with the new file data.](images/9781284255805_CH06_CUM12.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-4)

Now the contents of the test1 file contain the output from the who command.

Sometimes, instead of overwriting the file’s contents, you may need to append output from a command to an existing file, for example if you’re creating a log file to document an action on the system. In this situation, you can use the double greater-than symbol (>>) to append data:

![Codes show the usage of the double greater than symbol to append data.](images/9781284255805_CH06_CUM13.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-5)

The test2 file still contains the original data from the who command processed earlier, plus now it contains the new output from the date command.

### Input Redirection

[Input redirection](#9781284254884_Glossary.xhtml_GLOS-149) is the opposite of output redirection. Instead of taking the output of a command and redirecting it to a file, input redirection takes the content of a file and redirects it to a command.

The input redirection symbol is the less-than symbol (<):

![Command space less than space input file.](images/9781284255805_CH06_CUM14.jpg)

The easy way to remember this is that the command is always listed first in the command line, and the redirection symbol “points” to the way the data are flowing. The less-than symbol indicates that the data are flowing from the input file to the command.

Here’s an example of using input redirection with the wc command:

![Line 1: dollar space w c space less than space test 2\. Line 2: double indent, 2 space 11 space 75\. Line 3: dollar.](images/9781284255805_CH06_CUM15.jpg)

The wc command provides a count of text in the data. By default it produces three values:

*   The number of lines in the text

*   The number of words in the text

*   The number of bytes in the text

By redirecting a text file to the wc command, you can get a quick count of the lines, words, and bytes in the file. The example shows that there are 2 lines, 11 words, and 75 bytes in the test2 file.

There’s another method of input redirection, called [inline input redirection](#9781284254884_Glossary.xhtml_GLOS-145). This method allows you to specify the data for input redirection on the command line instead of in a file. This may seem somewhat odd at first, but there are a few applications for this process, such as providing interactive scripts.

The inline input redirection symbol is the double less-than symbol (<<). Besides this symbol, you must specify a text marker that delineates the beginning and end of the data used for input. You can use any string value for the text marker, but it must be the same at the beginning of the data and the end of the data:

![Line 1: command space double less than space marker. Line 2: data. Line 3: marker.](images/9781284255805_CH06_CUM16.jpg)

When using inline input redirection on the command line, the shell will prompt for data using the secondary prompt, defined in the PS2 environment variable. Here’s how this looks when you use it:

![Codes show the usage of inline input redirection on the command line.](images/9781284255805_CH06_CUM17.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-6)

The secondary prompt continues to prompt for more data until you enter the text marker. The wc command performs the line, word, and byte counts of the data supplied by the inline input redirection.

### Pipes

There are times when you need to send the output of one command to the input of another command. This is possible using redirection, but is somewhat clunky:

![Codes show the output of one command being sent to the input of another command.](images/9781284255805_CH06_CUM18.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-7)

The rpm command manages the software packages installed on systems using the Red Hat Package Management system (RPM), such as the Rocky Linux system as shown. When used with the -qa parameters, it produces a list of the existing packages installed, but not necessarily in any specific order. If you’re looking for a specific package, or group of packages, it can be difficult to find it using the output of the rpm command.

Using the standard output redirection, you can redirect the output from the rpm command to a file, called rpm.list. After the command finishes, the rpm.list file contains a list of all the installed software packages on the system. Next, you must use input redirection to send the contents of the rpm.list file to the sort command to sort the package names alphabetically.

That was useful, but again, a somewhat clunky way of producing the information. Instead of redirecting the output of a command to a file, you can redirect the output directly to another command. This process is called [piping](#9781284254884_Glossary.xhtml_GLOS-253). The pipe symbol is the bar operator (|):

![command 1 space vertical bar space command 2.](images/9781284255805_CH06_CUM19.jpg)

Piping provides a way to link commands to provide more detailed output. Don’t think of piping as running two commands back to back though. The Linux system actually runs both commands at the same time, linking them together internally in the system. As the first command produces output, it’s sent immediately to the second command. No intermediate files or buffer areas are used to transfer the data.

Now, using piping, you can easily pipe the output of the rpm command directly to the sort command to produce your results:

![The output of the r p m command is piped directly to the sort command.](images/9781284255805_CH06_CUM20.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-8)

![Continuation](images/9781284255805_CH06_CUM21.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-9)

Unless you’re a (very) quick reader, you probably couldn’t keep up with the output generated by this command. Since the piping feature operates in real time, as soon as the rpm command produces data, the sort command gets busy sorting it. By the time the rpm command finishes outputting data, the sort command already has the data sorted and starts displaying it on the monitor.

There’s no limit to the number of pipes you can use in a command (up to the 255 character limit on the line length). You can continue piping the output of commands to other commands to refine your operation.

In this case, since the output of the sort command zooms by so quickly, we can use one of the text paging commands (such as less or more) to force the output to stop at every screen of data:

![Dollar space r p m space hyphen q a space vertical bar space sort space vertical bar space more.](images/9781284255805_CH06_CUM22.jpg)

This command sequence runs the rpm command, pipes the output to the sort command, then pipes that output to the more command to display the data, stopping after every screen of information. This now lets you pause and read what’s on the display before continuing.

To get even fancier, you can use redirection along with piping, to save your output to a file:

![Codes use redirection along with piping to save the output.](images/9781284255805_CH06_CUM23.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-10)

As expected, the data in the rpm.list file is now sorted!

## Linux Environment Variables

The shell uses a feature called [environment variables](#9781284254884_Glossary.xhtml_GLOS-85) to store information about the shell session and the working environment (thus the name environment variables). This feature also allows you to store data in memory that can be easily accessed by any program or script running from the shell. This is a handy way to store persistent data that identifies features of the user account, system, shell, or anything else you need to store during the login session.

There are two types of environment variables in the bash shell:

*   Global variables

*   Local variables

This section describes each type of environment variable, and shows how to see and use them.

### Global Environment Variables

[Global environment variables](#9781284254884_Glossary.xhtml_GLOS-115) are visible from the shell session and any child processes that the shell spawns. Local variables are only available in the shell that creates them. This makes global environment variables useful in applications that spawn child processes that require information from the parent process.

The Linux system sets several global environment variables when you start your bash session. The system environment variables always use all capital letters to differentiate them from normal user environment variables.

To view the global environment variables, use the printenv command:

![An output shows the global environment variables using the print e n v command.](images/9781284255805_CH06_CUM24.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-11)

![Continuation](images/9781284255805_CH06_CUM25.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-12)

As you can see, lots of global environment variables get set in the shell. Most of them are set by the system during the login process.

To display the value of an individual environment variable, use the echo command. When referencing an environment variable, you must place a dollar sign before the environment variable name:

![Line 1: dollar space echo space dollar HOME. Line 2: slash home slash rich. Line 3: dollar.](images/9781284255805_CH06_CUM26.jpg)

As mentioned, global environment variables are also available to child processes running under the current shell session:

![Line 1: dollar space bash. Line 2: dollar space echo space dollar HOME. Line 3: slash home slash rich. Line 4: dollar.](images/9781284255805_CH06_CUM27.jpg)

In this example, after starting a new shell using the bash command, the echo command is used to display the current value of the HOME environment variable, which the system sets when I log into the main shell. As seen in the example, the value is also available from the child shell process.

### Local Environment Variables

[Local environment variables](#9781284254884_Glossary.xhtml_GLOS-180), as their name implies, can be seen only in the local process in which they are defined. Don’t get confused though about local environment variables, they are just as important as global environment variables. In fact, the Linux system also defines standard local environment variables for you by default.

Trying to see the list of local environment variables is a little tricky. Unfortunately there isn’t a command that displays only local environment variables. The set command displays all of the environment variables set for a specific process, including the global environment variables. This produces a very long list (too long to show here).

When you run the set command, notice that there are several bash-related entries that don’t appear in the global listing produced by the printenv command:

![An output shows a list of environment variables.](images/9781284255805_CH06_CUM28.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-13)

These document different features of the current bash shell, including any command line parameters or arguments that were used when the shell started. These can often come in handy if you need to determine the shell version or features from inside your shell scripts.

### Setting Environment Variables

Besides the system-created environment variables, you can also create your own. The shell allows you to create both global and local environment variables for your shell session. This section shows just how to do that.

#### Setting local environment variables

Once you start a bash shell (or spawn a shell script), you’re allowed to create local variables that are visible within your shell process. You can assign either a numeric or a string value to an environment variable by assigning the variable to a value using the equal sign:

![Line 1: dollar space test equals testing. Line 2: dollar space echo space dollar test. Line 3: testing. Line 4: dollar.](images/9781284255805_CH06_CUM29.jpg)

Once you assign the value to the environment variable, you can reference it at any time in the shell session by using the dollar sign: $test.

If you need to assign a string value that contains spaces, you’ll need to use a single quotation mark to delineate the beginning and the end of the string:

![Codes use a single quotation mark to delineate the beginning and the end of the string.](images/9781284255805_CH06_CUM30.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-14)

Without the single quotation marks, the shell assumes that the next character is another command to process. Notice that for the local environment variable defined, we used lowercase letters, while the system environment variables we’ve seen so far have all used uppercase letters.

This is a standard convention in bash. If you create new environment variables, it is recommended (but not required) that you use lowercase letters. This helps distinguish your personal environment variables from the scores of system environment variables.

Once you set a local environment variable, it’s available for use anywhere within your shell process. However, if you spawn another shell, it’s not available in the child shell:

![Line 1: dollar space test 2 space equals space test. Line 2: hyphen bash colon space test 2 colon. Line 3: command not found. Line 4: dollar.](images/9781284255805_CH06_CUM31.jpg)

This example starts a child shell with the bash command. The test environment variable is not available in the child shell (it contains a blank value). After exiting the child shell and returning to the original shell, the local environment variable was available.

Similarly, if you set a local environment variable in a child process, once you leave the child process the local environment variable is no longer available:

![The test environment variable is set in the child shell.](images/9781284255805_CH06_CUM32.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-16)

The test environment variable set in the child shell doesn’t exist in the parent shell.

#### Setting global environment variables

Global environment variables are visible from any child processes created by the process that sets the global environment variable. The method used to create a global environment variable is to create a local environment variable, then [export](#9781284254884_Glossary.xhtml_GLOS-91) it to the global environment.

This is done by using the export command:

![Codes show the usage of the export command.](images/9781284255805_CH06_CUM33.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-17)

After exporting the local environment variable test, a child shell processed and viewed the value of the test environment variable. This time, the environment variable kept its value, as the export command made it global.

### Removing Environment Variables

Of course, if you can create a new environment variable, it makes sense that you can also remove an existing environment variable. This is done by using the unset command:

![Line 1: dollar space echo space dollar test. Line 2: testing. Line 3: dollar space unset space test. Line 4: dollar space echo space dollar test. Line 5: dollar.](images/9781284255805_CH06_CUM34.jpg)

When referencing the environment variable in the unset command, remember not to use the dollar sign.

When working with global environment variables, things can get a little tricky. If you’re in a child process and remove a global environment variable, it only applies to the child process. The global environment variable is still available in the parent process:

![Codes show the global environment variable still available in the parent process.](images/9781284255805_CH06_CUM35.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-18)

This example sets a local environment variable called test, and then exports it to make it a global environment variable. It then starts a child shell process and checks to make sure that the global environment variable test is still available. Next, while still in the child shell, it uses the unset command to remove the global environment variable test, then exits the child shell. Now back in the original parent shell, it checks the test environment variable value, and it is still valid.

## Writing Shell Scripts

Placing multiple commands on a single line, either by using the semicolon or piping, is a great way to process data, but it can still get rather tedious. Each time you want to run a set of commands, you need to type them all at the command prompt.

However, Linux also allows us to place multiple commands in a text file, then run the text file as a program from the command line. This is called a shell script, because we’re scripting out commands for the Linux shell to run.

Shell script files are plain text files. To create a shell script file, you just need to use any text editor that you’re comfortable with. If you’re working from a KDE-based graphical desktop, you can use the KWrite or Kate programs, or if you’re using a GNOME-based desktop, you can use the Gedit program.

If you’re working directly in a command-line environment, you still have some options. Many Linux distributions include either the pico or nano text editors, which provide a graphical text editing environment using ASCII control characters to create a full-screen window. If your Linux distribution doesn’t include one of these programs, there is still one last resort—the vi editor. The vi editor is a text-based editor that uses simple single-letter commands. It’s the oldest editor in the Linux environment and is not overly user-friendly.

Once you’ve chosen your text editor, you’re ready to create your shell scripts. This section walks through the basics on how to do that.

### Getting Started

The first line in a shell script file identifies the file as being a shell script. It tells Linux what shell to use the process the commands contained in the shell script:

![Hash exclamation slash bin slash bash.](images/9781284255805_CH06_CUM36.jpg)

The combination of the pound sign and the exclamation symbol (#!) is commonly called the shebang. It signals to the operating system which shell to use to run the shell script. Most Linux distributions support multiple Linux shells, but the most common is the bash shell. You can run shell scripts written for other shells, as long as that shell is installed on the Linux distribution.

After you specify the shell, you’re ready to start listing the commands in your script. You don’t need to enter all of the commands on a single line; Linux allows you to place them on separate lines. Also, the Linux shell assumes each line is a new command in the shell script, so you don’t need to use semicolons to separate the commands. Here’s an example of a simple shell script file.

![Line 1: dollar space cat space script 1 dot s h. Line 2: hash exclamation slash bin slash bash. Line 3: hash This script displays the date and who’s logged in. Line 4: date. Line 5: who. Line 6: dollar.](images/9781284255805_CH06_CUM37.jpg)

The script1.sh script file starts out with the shebang line identifying the bash shell, the standard shell in Linux. The second line in the code demonstrates another feature in shell scripts. Lines that start with a pound sign are called comment lines. They allow you to embed comments into the shell script program to help you remember what the code is doing. The shell skips comment lines when processing the shell script. You can place comment lines anywhere in your shell script file, after the opening shebang line.

After you save your new shell script file, you’ll want to run it. However, there’s a step you’ll need to take before you can do that. By default text files aren’t marked as program files, so the shell won’t be able to run them. To fix that you’ll need to use the chmod command:

![c h mod space u plus x space script 1 dot s h.](images/9781284255805_CH06_CUM38.jpg)

This command format will make much more sense after you’ve read Chapter 10, “Linux Server Administration,” which walks through the different permissions you can set for a file. Basically, this command adds the execute (run) permission to the file for the owner of the file. Now you can run the command from the command line:

![The command is run from the command line.](images/9781284255805_CH06_CUM39.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-19)

The ./ symbol is required because current directory where the script is located is not included in the PATH environment variable. It tells the shell to look in the current directory for the file.

### Displaying Messages

When you string commands together in a shell script file, the output may be somewhat confusing to look at. It would help to be able to customize the output by separating the output and adding our own text between the output from the listed commands.

The echo command allows you to display text messages from the command line. When used at the command line, it’s not too exciting:

![Line 1: dollar space echo space This is a test. Line 2: This is a test. Line 3: dollar.](images/9781284255805_CH06_CUM40.jpg)

But now you have the ability to insert messages anywhere in the output from the shell script file. Just modify the test1.sh shell script program by adding a couple of echo commands:

![test 1 dot s h shell script program is modified by adding a couple of echo commands.](images/9781284255805_CH06_CUM41.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-20)

When you run the script now, you should see the following output:

![An output shows the result of running the script.](images/9781284255805_CH06_CUM42.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-21)

The shell script you created adds three echo commands to the script1.sh script. Notice that the first echo command doesn’t use any quotes, but the third one does. The reason for that is the text output from the third echo command contains single quotes. The single quote is also a metacharacter in the shell, which will confuse the echo command, so you need to place double quotes around the text. Also notice that the second echo command doesn’t have any text on the line. That outputs a blank line, which is useful when you want to separate output from multiple commands.

### Using Variables

Shell scripts can also tap into the global and local environment variables set in the shell. Just remember to place the dollar sign in front of the environment variable name when you reference it in the script:

![The dollar sign is placed in front of the environment variable name in the script.](images/9781284255805_CH06_CUM43.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-22)

The $USER, $UID, and $HOME environment variables are commonly used to display information about the logged-in user. When you run the shell script, you should see the information related to the user who runs the script:

![An output shows the result of running the shell script.](images/9781284255805_CH06_CUM44.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-23)

The values you see should be related to your user account. This allows you to dynamically retrieve information about the user account running your shell script to customize the output.

You can also set local environment variables inside your shell scripts:

![Local environment variables are set inside shell scripts.](images/9781284255805_CH06_CUM45.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-24)

Running the script3.sh script produces the following output:

![Line 1: dollar space c h mod space u + x space script 3 dot s h. Line 2: dollar space dot slash script 3 dot s h. Line 3: Rich checked in 10 days ago. Line 4: dollar.](images/9781284255805_CH06_CUM46.jpg)

Once you store the data in a user variable you can reference it anywhere in your shell script!

### Command Line Arguments

One of the most versatile features of shell scripts is the ability to pass data into the script when you run it. This allows you to customize the script with new data each time you run it.

One method of passing data into a shell script is to use command line arguments. Command line arguments are data you include on the command line when you run the command. Just start listing them after the command, separating each data value with a space, in this format:

![command space argument 1 space argument 2 space ellipsis.](images/9781284255805_CH06_CUM47.jpg)

You retrieve the values in your shell script code using special numeric positional variables. Use the variable $1 to retrieve the first command line argument, $2 the second argument, and so on. Here’s an example that shows how to use positional variables in your shell script:

![An example shows how to use positional variables in the shell script.](images/9781284255805_CH06_CUM48.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-25)

The script4.sh shell script uses two command line arguments. The $1 variable holds the name of the person, and the $2 variable holds the number of days ago they checked in. When you run the scsript4.sh shell script be sure to include both data values in the command line. The shell won’t produce an error message if a positional variable doesn’t exist; you just won’t get the results you expected:

![Line 1: dollar space dot slash script 4 dot s h space rich. Line 2: rich checked in days ago. Line 3: dollar.](images/9781284255805_CH06_CUM49.jpg)

It’s up to you to check if the positional variable exists within your program code.

### Command Substitution

Quite possibly one of the most useful features of shell scripts is the ability to store and process data. So far I’ve discussed how to use output redirection to store output from a command to a file and piping to redirect the output of a command to another command. There’s another technique, however, that can give you more flexibility in storing and using data in your scripts.

Command substitution allows you to assign the output of a command to a local variable in the shell script. Once the output is stored in a variable, you can use standard Linux string manipulation commands (such as sort) to manipulate the data before displaying it.

To redirect the output of a command to a variable you need to use one of two command substitution formats:

*   Placing backticks (`) around the command

*   Using the command within the $() function

Both methods produce the same result—redirecting the output from the command into a user variable. Here’s an example that demonstrates using both methods:

![An example shows how to use positional variables in the shell script.](images/9781284255805_CH06_CUM50.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-26)

The output from the command substitutions is stored in the appropriate variables. You can then use those variables anywhere in your script program as a standard string value.

### Logic Statements

So far all of the shell scripts presented process commands in a linear fashion—one command after another. However, not all programming is linear. There are times when you’d like your program to test for certain conditions, such as if a file exists or if a mathematical expression is 0, and perform different commands based on the results of the test. For that, the bash shell provides logic statements.

Logic statements allow you to test for a specific condition, then branch to different sections of code based on whether the condition evaluates to a True or False logical value. The most basic logic statement is the if-then condition statement. The format for the if-then condition statement is as follows:

![Line 1: dollar space dot slash script 4 dot s h space rich. Line 2: rich checked in days ago. Line 3: dollar.](images/9781284255805_CH06_CUM51.jpg)

If the condition you specify evaluates to a True logical value, the shell runs the commands in the then section of code. If the condition evaluates to a False logical value, the shell script skips the commands in the then section of code.

The condition expression has quite a few different formats in the bash shell programming. There are built-in tests for numerical values, string values, and even files and directories. [TABLE 6-4](#9781284254884_CH06_06.xhtml_c6-tab004) lists the different built-in tests that are available.

TABLE 6-4 Condition tests.

| TEST | TYPE | DESCRIPTION |
| --- | --- | --- |
| n1 -eq n2 | Numeric | Checks if n1 is equal to n2 |
| n1 -ge n2 | Numeric | Checks if n1 is greater than or equal to n2 |
| n1 -gt n2 | Numeric | Checks if n1 is greater than n2 |
| n1 -le n2 | Numeric | Checks if n1 is less than or equal to n2 |
| n1 -lt n2 | Numeric | Checks if n1 is less than n2 |
| n1 -ne n2 | Numeric | Checks if n1 is not equal to n2 |
| str1 = str2 | String | Checks if str1 is the same as str2 |
| str1 != str2 | String | Checks if str1 is not the same as str2 |
| str1 < str2 | String | Checks if str1 is less than str2 |
| str1 > str2 | String | Checks if str1 is greater than str2 |
| -n str1 | String | Checks if str1 has a length greater than zero |
| -z str1 | String | Checks if str1 has a length of zero |
| -d file | File | Check if file exists and is a directory |
| -e file | File | Checks if file exists |
| -f file | File | Checks if file exists and is a file |
| -r file | File | Checks if file exists and is readable |
| -s file | File | Checks if file exists and is not empty |
| -w file | File | Checks if file exists and is writable |
| -x file | File | Checks if file exists and is executable |
| -O file | File | Checks if file exists and is owned by the current user |
| -G file | File | Checks if file exists and the default group is the same as the current user |
| file1 -nt file2 | File | Checks if file1 is newer than file2 |
| file1 -ot file2 | File | Checks if file1 is older than file2 |

Here’s an example of using an if-then statement in a script:

![An example shows the usage of two command substitution formats.](images/9781284255805_CH06_CUM52.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-27)

![Line 1: if open bracket condition close bracket. Line 2: then. Line 3: single indent, commands. Line 4: f i.](images/9781284255805_CH06_CUM53.jpg)

The script compares the first two command line parameters ($1 and $2) and determines which one is larger or if they’re equal. After setting the permissions to run the script, you can test it out:

![An example of using an if then statement in a script is shown.](images/9781284255805_CH06_CUM54.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-28)

Only the command from the if-then statement that evaluated to a True logical value is processed by the shell script.

### Looping

When you’re writing scripts, you’ll often find yourself in a situation where it would come in handy to repeat the same commands multiple times, such as applying a command against all of the files in a directory. The bash shell provides some basic looping commands to accommodate that.

The for statement iterates through every element in a series, such as files in a directory, or lines in a text document. The format of the for command is:

![Continuation](images/9781284255805_CH06_CUM55.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-29)

The variable becomes a placeholder, taking on the value of each element in the series in each iteration. The commands can use the variable just like any other variable that you define in the script. Here’s an example that shows how to use a for loop to iterate through all of the files in a directory.

![Line 1: dollar c h mod u plus x script 5 dot s h. Line 2: dollar dot slash script 5 dot s h 10 5\. Line 3: The first value is greater than the second. Line 4: dollar.](images/9781284255805_CH06_CUM56.jpg)

![Line 1: for variable in series semicolon do. Line 2: single indent, commands. Line 3: done.](images/9781284255805_CH06_CUM57.jpg)

If you run the script6.sh shell script you should see a listing of the files and directories in your Home directory:

![A script shows how to use a for loop to iterate through all of the files in a directory.](images/9781284255805_CH06_CUM58.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-30)

That saves a lot of coding from having to check each file manually in a bunch of if-then or case statements!

Another useful loop statement is the while command. This is its format:

![Continuation](images/9781284255805_CH06_CUM59.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-31)

The while loop keeps looping as long as the condition specified evaluates to a True logical value. When the condition evaluates to a False logical value, the looping stops. The condition used in the while loop is the same as that for the if-then statement, so you can test numbers, strings, and files. Here’s an example that demonstrates using the while loop to calculate the factorial of a number:

![An output shows a listing of the files and directories in the Home directory.](images/9781284255805_CH06_CUM60.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd6-32)

The shell script retrieves the first parameter passed to the script and uses it in the while loop. The while loop continues looping as long as the value stored in the $number variable is greater than 0\. In each loop iteration that value is decreased by 1, so at some point the while condition becomes False. When that occurs the $factorial variable contains the final calculation. When you run the script7.sh program, you should get the following results:

![Line 1: while open bracket condition close bracket semicolon do. Line 2: single indent, commands. Line 3: done.](images/9781284255805_CH06_CUM61.jpg)

The while loop took all of the hard work of iterating through the series of numbers. Now you can plug any number as the command line parameter and calculate the factorial value!

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 7
File Management

ONE OF THE MOST IMPORTANT FUNCTIONS of working in the Linux command line interface is handling files and directories. Just about every administrative task you perform on your Linux system requires working with some type of file. This chapter dives into the topic of handling files and directories from the Linux command line.

The chapter first discusses how Linux handles files and directories using the virtual directory and some of the rules you’ll need to follow when naming files and directories on your Linux system. After that it shows the command line commands you’ll need to become familiar with to work with files and directories, such as listing, copying, moving, and deleting them.

The chapter next shows how to use the popular commands to find files on Linux systems. There are several different commands that you can use, each one with slightly different features. It finishes by discussing the Linux file and archiving process, which allows you to compress files and directories into a single archive file to make distributing and storing files much easier.

## Filesystem Navigation

For most Linux distributions, when you start a shell session you are placed in your user home directory. Most often, you will need to break out of your home directory to get to other areas in the Linux system. This section describes how to do that using command line commands. Before that, though, is a short tour of just what the Linux filesystem looks like.

### The Linux Filesystem

If you’re new to the Linux system, you may be confused by how it references files and directories, especially if you’re used to the way that the Microsoft Windows operating system does that. Before exploring the Linux system, it helps to have an understanding of how it’s laid out.

The first difference you’ll notice is that Linux does not use drive letters in pathnames. In the Windows world, the physical drives installed on the PC determine the pathname of the file. Windows assigns a letter to each physical disk drive, and each drive contains its own directory structure for accessing files stored on it.

For example, in Windows you may be used to seeing the file paths such as:

![c colon backslash Users backslash Rich backslash My Documents backslash test dot doc.](images/9781284255805_CH07_CUM01.jpg)

This indicates that the file test.doc is located in the directory My Documents, which itself is located in the directory Rich. The Rich directory is contained under the directory Users, which is located on the hard disk partition assigned the letter C (usually the first hard drive on the PC).

The Windows file path tells you exactly which physical disk partition contains the file named test.doc. If you wanted to save a file on a USB memory stick, you would click the icon for the drive assigned to the memory stick, such as E:, which automatically uses the file path e:\test.doc. This path indicates that the file is located at the root of the drive assigned the letter E, which is usually assigned to the first USB storage device plugged into the PC.

This is not the method used by Linux. Linux stores files within a single directory structure, called a [virtual directory](#9781284254884_Glossary.xhtml_GLOS-356). The virtual directory contains file paths from all the storage devices installed on the PC, merged into a single directory structure.

The Linux virtual directory structure contains a single base directory, called the [root](#9781284254884_Glossary.xhtml_GLOS-291). Directories and files beneath the root directory are listed based on the directory path used to get to them, similar to the way Windows does it.

For example, the Linux file path /home/rich/Documents/test.doc only indicates that the file test.doc is in the directory Documents, under the directory rich, which is contained in the directory home. It doesn’t provide any information as to which physical disk on the PC the file is stored on.

The tricky part about the Linux virtual directory is how it incorporates each storage device. The first hard drive installed in a Linux PC is called the [root drive](#9781284254884_Glossary.xhtml_GLOS-293). The root drive contains the core of the virtual directory. Everything else builds from there.

On the root drive, Linux creates special directories called [mount points](#9781284254884_Glossary.xhtml_GLOS-209). Mount points are directories in the virtual directory where you assign additional storage devices.

The virtual directory causes files and directories to appear within these mount point directories, even though they are physically stored on a different drive.

Often the system files are physically stored on the root drive, while user files are stored on a different drive, as shown in [FIGURE 7-1](#9781284254884_CH07_01.xhtml_c7-fig001).

![A chart shows the Linux file structure divided between two disks.](images/9781284255805_CH07_FIGF01.jpg)

FIGURE 7-1 The Linux file structure.

[Description](9781284254884_Alt.xhtml_summary-fig7-1)

In [Figure 7-1](#9781284254884_CH07_01.xhtml_c7-fig001), there are two hard drives on the PC. One hard drive is associated with the root of the virtual directory (indicated by a single forward slash). Other hard drives can be mounted anywhere in the virtual directory structure. In this example, the second hard drive is mounted at the location /home, which is where the user directories are located.

The Linux filesystem structure has evolved from the Unix file structure. Unfortunately, the Unix file structure has been somewhat convoluted over the years by different flavors of Unix. To help remedy this problem in the Linux world, the Linux Foundation has developed the Linux Filesystem Hierarchy Standard (FHS). It defines a standard structure for the virtual directory on a Linux system. While not a requirement, most Linux distributions now follow this structure. [TABLE 7-1](#9781284254884_CH07_01.xhtml_c7-tab001) lists some of the more common Linux virtual directory names contained in the FHS.

TABLE 7-1 The linux filesystem hierarchy standard.

| DIRECTORY | USAGE |
| --- | --- |
| / | The root of the virtual directory. Normally, no files are placed here. |
| /bin | The binary directory, where essential user-level utilities are stored. |
| /boot | The boot directory, where boot files are stored. |
| /dev | The device directory, where Linux creates device nodes. |
| /etc | The system configuration files directory. |
| /home | The home directory, where Linux creates user directories. |
| /lib | The library directory, where system and application library files are stored. |
| /media | The media directory, a common place for mount points used for removable media. |
| /mnt | The mount directory, another common place for mount points used for temporarily mounted media. |
| /opt | The optional directory, often used to store optional application software packages. |
| /proc | The process directory, a virtual filesystem that provides process and kernel information as individual files, generated by the system. |
| /root | The root user account’s home directory. |
| /run | The run-time directory contains information about the system since the last boot. |
| /sbin | The system binary directory, where many admin-level utilities are stored. |
| /sys | The system directory, contains information files about devices, drivers, and some kernel features. |
| /tmp | The temporary directory, where temporary work files can be created and destroyed. This directory is usually cleared after each reboot of the system. |
| /usr | The user-installed software directory, this directory is normally set as read-only to protect the integrity of the installed software. |
| /var | The variable directory, for files that change frequently, such as log files. |

When you start a new shell prompt, your session starts in your home directory, which is a unique directory assigned to your user account. When you create a user account, the system normally assigns a unique directory for the account.

In the Windows world, you’re probably used to moving around the directory structure using a graphical interface. To move around the virtual directory from a command line interface (CLI) prompt, you’ll need to learn to use the cd command.

### Traversing Directories

The change directory command ([cd](#9781284254884_Glossary.xhtml_GLOS-36)) is what you’ll use to move your shell session to another directory in the Linux filesystem. The format of the cd command is pretty simplistic:

![c d space destination.](images/9781284255805_CH07_CUM02.jpg)

The cd command may take a single parameter, destination, which specifies the directory name you want to go to. If you don’t specify a destination on the cd command, it will take you to your home directory.

The destination parameter, though, can be expressed using two different methods:

*   An absolute filepath

*   A relative filepath

The following sections describe the differences between these two methods.

#### Absolute Filepaths

You can reference a directory name within the virtual directory using an [absolute filepath](#9781284254884_Glossary.xhtml_GLOS-12). The absolute filepath defines exactly where the directory is in the virtual directory structure, starting at the root of the virtual directory, sort of like a full name for a directory.

Thus, to reference the apache directory, that’s contained within the lib directory, which in turn is contained within the usr directory, you would use the absolute filepath:

![Slash u s r slash lib slash apache.](images/9781284255805_CH07_CUM03.jpg)

With the absolute filepath, there’s no doubt as to exactly where you want to go. To move to a specific location in the filesystem using the absolute filepath, you just specify the full pathname in the cd command:

![Line 1: rich at Ubuntu 02 space tilde dollar space c d space slash u s r slash lib slash apache. Line 2: rich at Ubuntu 02 space apache dollar.](images/9781284255805_CH07_CUM04.jpg)

On most Linux distributions the prompt shows the current directory for the shell (the tilde represents your user home directory). You can move to any level within the entire Linux virtual directory structure using the absolute filepath.

However, if you’re just working within your own home directory structure, often using absolute filepaths can get tedious. For example, if you’re already in the directory /home/rich, it seems somewhat cumbersome to have to type the command:

![c d space slash home slash rich slash Documents.](images/9781284255805_CH07_CUM05.jpg)

just to get to your Documents directory. Fortunately, there’s a simpler solution.

#### Relative Filepaths

[Relative filepaths](#9781284254884_Glossary.xhtml_GLOS-283) allow you to specify a destination directory relative to your current location, without having to start at the root. A relative filepath doesn’t start with a forward slash, indicating the root directory.

Instead, a relative filepath starts with either a directory name (if you’re traversing to a directory under your current directory) or a special character indicating a relative location to your current directory location. Two special characters are used for this:

*   The dot (.) to represent the current directory

*   The double dot (..) to represent the parent directory

The double dot character is extremely handy when trying to traverse a directory hierarchy. For example, if you are in the Documents directory under your home directory and need to go to your Desktop directory, also under your home directory, you can do this:

![Line 1: rich at Ubuntu 02 space Documents dollar space c d space double dot slash Desktop. Line 2: rich at ubunut 02 space Desktop dollar.](images/9781284255805_CH07_CUM06.jpg)

The double dot character takes you back up one level to your home directory, then the /Desktop portion takes you back down into the Desktop directory. You can use as many double dot characters as necessary to move around. For example, if you are in your home directory (/home/rich) and want to go to the /etc directory, you could type:

![Line 1: rich at ubunut 02 space tilde dollar space c d space double dot slash double dot slash e t c. Line 2: rich at Ubuntu 02 space e t c dollar.](images/9781284255805_CH07_CUM07.jpg)

Of course, in a case like this, you actually have to do more typing to use the relative filepath rather than just typing the absolute filepath, /etc!

## Linux Files

One of the things that made the Unix operating system unique when it was first created back in the 1970s was that it treats everything on the computer system as a file: hardware devices, data, network connections, everything. That simplified the way programs interact with hardware, and with each other, because no matter where your data comes from, the Unix operating system handles it the same way. While that may seem odd, it’s what revolutionized the computer world and made the Unix operating system so popular.

However, because everything is a file, there are some issues that you’ll run into. One of those issues is trying to identify file types. This section walks through how Linux handles file names and shows some hints on how you can determine file types on a Linux system.

### Determining File Types

Linux data files cover a pretty wide range of file types—everything from text data to executable programs. Because Linux files aren’t required to use a file extension, it can sometimes be difficult to tell what files are programs, what files are text data, and what files are binary data. Fortunately there’s a command line utility that can help.

The [file](#9781284254884_Glossary.xhtml_GLOS-99) command returns the type of the file specified. If the file is a data file, it also attempts to detect just what the file contains:

![An output of the file command is shown.](images/9781284255805_CH07_CUM08.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-1)

In this example, the myprog.c file is a C program text file, and the myprog file is a binary executable program.

### File Names

The first thing you’ll notice as you peruse through the directories on your Linux system is that Linux has a different file naming standard than Windows. In the Windows world, you’re probably used to seeing a three- or four-character file extension added onto each file (such as .docx for Word documents). Linux doesn’t require file extensions to identify file types on the system (although they’re allowed if you like to use them).

Linux file names can be any length of characters, although 255 is a practical limit for file names (when file names get longer than that some programs have trouble handling them). Linux file names can contain upper and lower case letters, numbers, and most special characters (the only characters not allowed are the forward slash and the NULL character). Linux file names can contain spaces, as well as foreign language characters. However, the file name should always start with a letter or number.

Here’s an example of some valid Linux file names:

![Line 1: testing. Line 2: A space test space file dot t x t. Line 3: 4 underscore data underscore points. Line 4: my dot long dot program dot name.](images/9781284255805_CH07_CUM09.jpg)

### Hidden Files

Another feature of Linux file names that is different from Windows is [hidden files](#9781284254884_Glossary.xhtml_GLOS-132). Hidden files don’t appear in normal file listings. In the Windows world, you use file properties to make a file hidden from normal viewing. When a normal user displays the directory listing, the hidden files don’t appear, but when an administrator displays the directory listing, the hidden files magically appear in the output. This feature helps protect important system files from being accidentally deleted or overwritten.

Linux doesn’t use file properties to make a file hidden. Instead, it uses the file name. File names that start with a period are considered hidden files, in that they don’t appear in a normal listing when you use the ls command or displayed when using a graphical file manager tool. You can however use options to display hidden files in the ls command or the file manager tools. [FIGURE 7-2](#9781284254884_CH07_02.xhtml_c7-fig002) shows setting the Files graphical file manager tool in Ubuntu to display hidden files.

![A screenshot displays hidden files using Files in Ubuntu.](images/9781284255805_CH07_FIGF02.jpg)

FIGURE 7-2 Displaying hidden files using Files in Ubuntu.Courtesy of Canonical Ltd.

[Description](9781284254884_Alt.xhtml_summary-fig7-2)

To display hidden files with the ls command, you need to include the –a command line parameter:

![An output shows hidden files using the l s command with the hyphen a command line parameter.](images/9781284255805_CH07_CUM10.jpg)

![An output shows hidden files using the l s command with the hyphen a command line parameter.](images/9781284255805_CH07_CUM11.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-2)

In this example, the ls command by itself only shows a few directories in the Home directory. Adding the –a parameter shows all of the hidden files in the directory. Many Linux programs store any settings that you make as a hidden file in each users’ Home directory.

### File Inodes

Linux has to keep track of a lot of information for each file on the system. The way it does that is by using index nodes, also called [inodes](#9781284254884_Glossary.xhtml_GLOS-146). The Linux operating system creates an inode for each file on the system to store the file properties. The inodes are hidden from view; only the operating system can access them. Each inode is also assigned a number, called the [inode number](#9781284254884_Glossary.xhtml_GLOS-147). This is what Linux uses to reference the file, not the file name. The inode numbers are unique on each physical disk partition.

Linux also creates a table on each disk partition, called the [inode table](#9781284254884_Glossary.xhtml_GLOS-148). The inode table contains a listing that matches each inode number assigned to each file on the disk partition. As you create and delete files, Linux automatically updates the inode table behind the scenes. However, if the system should abruptly shut down (such as due to a power failure) the inode table can become corrupt. Fortunately for us, there are utilities that can help reorganize the inode table and help prevent data loss. Unfortunately though, if the inode table does become unrepairable, you won’t be able to access the files on the disk partition, even if the actual files are still there!

To view the inode number for files, use the -i option in the ls command. You can combine it with the -l option to produce a long listing to show more details about the file:

![An output shows the result of using the l s command with the hyphen i l option.](images/9781284255805_CH07_CUM12.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-3)

The first number displayed in the long listing is the inode number for each file. Notice that the inode number for the myprog.c file is the same as the copy.c file. That means there is a hard link between those two files. The hard link points to the same physical disk location as the original file, so the inode numbers are the same.

## File and Directory Listing

The most basic feature of the shell is the ability to see what files are available on the system. The list command ([ls](#9781284254884_Glossary.xhtml_GLOS-184)) is the tool that helps do that. This section describes the ls command and all of the options available to format the information it can provide.

### Basic Listing

The ls command at its most basic form displays the files and directories located in your current directory:

![An output displays the files and directories located in the current directory using the l s command.](images/9781284255805_CH07_CUM13.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-4)

Notice that the ls command produces the listing in alphabetical order (in columns rather than rows). If you’re using a terminal emulator that supports color, the ls command may also show different types of entries in different colors. The LS_COLORS environment variable controls this feature. Different Linux distributions set this environment variable depending on the capabilities of the terminal emulator.

If you don’t have a color terminal emulator, you can use the -F parameter with the ls command to easily distinguish files from directories. Using the -F parameter produces the following output:

![An output distinguishes files from directories using the l s command with hyphen F parameter.](images/9781284255805_CH07_CUM14.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-5)

The -F parameter now flags the directories with a forward slash, to help identify them in the listing. Similarly, it flags executable files (like the test,sh file above) with an asterisk, to help you find the files that can be run on the system easier.

The -R parameter is another command ls parameter to use. It shows files that are contained within directories in the current directory. If you have lots of directories, this can be quite a long listing. Here’s a simple example of what the -R parameter produces:

![An output shows files that are contained within directories in the current directory using the l s command with hyphen F and hyphen R parameters.](images/9781284255805_CH07_CUM15.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-6)

Notice that first, the -R parameter shows the contents of the current directory, which is a file (file1) and two directories (test1 and test2). Following that, it traverses each of the two directories, showing if any files are contained within each directory. The test1 directory shows two files (myprog1 and myprog2), while the test2 directory doesn’t contain any files. If there had been further subdirectories within the test1 or test2 directories, the -R parameter would have continued to traverse those as well. As you can see, for large directory structures this can become quite a large output listing.

### Modifying Listing Information

As you can see in the basic listings, the ls command doesn’t produce a whole lot of information about each file. For listing additional information, another popular parameter is -l. The -l parameter produces a long listing format, providing more information about each file in the directory:

![An output shows more information about each file in the directory using the l s command with hyphen l parameter.](images/9781284255805_CH07_CUM16.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-7)

The long listing format lists each file and directory contained in the directory on a single line. Besides the file name, it shows additional useful information. The first line in the output shows the total number of blocks contained within the directory. Following that, each line contains the following information about each file (or directory):

*   The file type (such as directory (d), file (-), character device (c), or block device (b)

*   The permissions string for the file, indicting permissions for the user, group, and other users

*   The number of hard links to the file

*   The username of the owner of the file

*   The group name of the group the file belongs to

*   The size of the file in bytes

*   The time the file was modified last

*   The file or directory name

The -l parameter is a powerful tool to have. Armed with this information you can see just about any information you need to for any file or directory on the system.

### The Complete Parameter List

There are lots of parameters for the ls command that can come in handy as you do file management. If you use the man command for ls, you’ll see several pages of available parameters for you to use to modify the output of the ls command.

The ls command uses two types of command line parameters:

*   Single-letter parameters

*   Full-word (long) parameters

The [single-letter parameters](#9781284254884_Glossary.xhtml_GLOS-309) are always preceded by a single dash. [Full-word parameters](#9781284254884_Glossary.xhtml_GLOS-110) are more descriptive and are preceded by a double dash. Many parameters have both a single-letter and full-word version, while some have only one type. [TABLE 7-2](#9781284254884_CH07_03.xhtml_c7-tab002) lists some of the more popular parameters that’ll help you out with using the bash ls command.

TABLE 7-2 Some popular ls command parameters.

| Single Letter | Full Word | Description |
| --- | --- | --- |
| -a | --all | Don’t ignore entries starting with a period. |
| -A | --almost-all | Don’t list the . and .. files. |
|  | --author | Print the author of each file. |
| -b | --escape | Print octal values for nonprintable characters. |
|  | --block-size=size | Calculate the block sizes using size-byte blocks. |
| -B | ~ | Don’t list entries with the tilde (~) symbol (used to denote backup copies). |
| -c |  | Sort by time of last modification. |
| -C |  | List entries by columns. |
|  | --color=when | When to use colors (always, never, or auto). |
| -d | --directory | List directory entries instead of contents and don’t dereference symbolic links. |
| -F | --classify | Append file-type indicator to entries. |
|  | --file-type | Only append file-type indicators to some file types (not executable files). |
|  | --format=word | Format output as either across, commas, horizontal, long, single-column, verbose, or vertical. |
| -g |  | List full file information except for the file’s owner. |
|  | --group-directories-first | List all directories before files. |
| -G | --no-group | In long listing don’t display group names. |
| -h | --human-readable | Print sizes using K for kilobytes, M for megabytes, and G for gigabytes. |
|  | --si | Same as -h, but use powers of 1000 instead of 1024. |
| -i | --inode | Display the index number (inode) of each file. |
| -l |  | Display the long listing format. |
| -L | --dereference | Show information for the original file for a linked file. |
| -n | --numeric-uid-gid | Show numeric userid and groupid instead of names. |
| -o |  | In long listing don’t display owner names. |
| -r | --reverse | Reverse the sorting order when displaying files and directories. |
| -R | --recursive | List subdirectory contents recursively. |
| -s | --size | Print the block size of each file. |
| -S | --sort=size | Sort the output by file size. |
| -t | --sort=time | Sort the output by file modification time. |
| -u |  | Display file last access time instead of last modification time. |
| -U | --sort=none | Don’t sort the output listing. |
| -v | --sort=version | Sort the output by file version. |
| -x |  | List entries by line instead of columns. |
| -X | --sort=extension | Sort the output by file extension. |

You can use more than one parameter at a time if you want to. The double dash parameters must be listed separately, but the single dash parameters can be combined together into a string behind the dash. A common combination to use is the -a parameter to list all files, the -i parameter to list the inode for each file, the -l parameter to produce a long listing, and the -s parameter to list the block size of the files. The inode of a file or directory is a unique identification number the kernel assigns to each object in the filesystem. Combining all of these parameters creates the easy-to-remember -sail parameter:

![An output is shown using the l s command with hyphen sail parameter.](images/9781284255805_CH07_CUM17.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-8)

Besides the normal -l parameter output information, you’ll see two additional numbers added to each line. The first number in the listing is the file or directory inode number. The second number is the block size of the file.

## Directory Handling

In Linux there are a few commands that work for both files and directories and some that only work for directories. This section discusses the commands that can only work with directories.

### Creating Directories

There’s not much to creating a new directory in Linux; just use the [mkdir](#9781284254884_Glossary.xhtml_GLOS-203) command:

![An output shows the usage of the m k d i r and l s hyphen i l commands.](images/9781284255805_CH07_CUM18.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-9)

![An output shows the usage of the m k d i r and l s hyphen i l commands.](images/9781284255805_CH07_CUM19.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-10)

The system creates a new directory and assigns it a new inode number.

### Deleting Directories

Removing directories can be tricky, but there’s a reason for that. There are lots of opportunities for bad things to happen when you start deleting directories. Bash tries to protect us from accidental catastrophes as much as possible. The basic command for removing a directory is [rmdir](#9781284254884_Glossary.xhtml_GLOS-289):

![Line 1: dollar space r m d i r space d i r 3\. Line 2: dollar space r m d i r space d i r 1\. Line 3: r m d i r colon d i r 1 colon Directory not empty. Line 4: dollar.](images/9781284255805_CH07_CUM20.jpg)

By default, the rmdir command only works for removing empty directories. Since there is a file in the dir1 directory, the rmdir command refuses to remove it. You can remove nonempty directories using the --ignore-fail-on-non-empty parameter.

You can also use the rm command when handling directories.

If you try using it without parameters, as with files, you’ll be somewhat disappointed:

![Line 1: dollar space r m space d i r 1\. Line 2: r m colon space d i r 1 colon space is a directory. Line 3: dollar.](images/9781284255805_CH07_CUM21.jpg)

However, if you really want to remove a directory, you can use the -r parameter to recursively remove the files in the directory, then the directory itself:

![An output shows the removal of files in the directory, then the directory itself, using the r m command with hyphen r parameter.](images/9781284255805_CH07_CUM22.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-11)

While this works, it’s somewhat awkward. Notice that you still must verify every file that gets removed. For a directory with lots of files and subdirectories, this can become tedious.

The ultimate solution for throwing caution to the wind and removing an entire directory, contents and all, is the rm command with both the -r and -f parameters:

![Line 1: dollar space r m space hyphen r f space d i r 2\. Line 2: dollar.](images/9781284255805_CH07_CUM23.jpg)

That’s it. No warnings, no fanfare, just another shell prompt. This, of course, is an extremely dangerous tool to have, especially if you’re logged in as the root user account. Use it sparingly and only after triple checking to make sure that you’re doing exactly what you want to do.

## File Handling

Bash provides lots of commands for manipulating files on the Linux filesystem. This section walks through the basic commands you will need to work with files from the CLI for all your file-handling needs.

### Creating Files

Every once in a while you will run into a situation where you need to create an empty file. Sometimes applications expect a log file to be present before they can write to it. In these situations, you can use the [touch](#9781284254884_Glossary.xhtml_GLOS-338) command to easily create an empty file:

![An output shows the creation of an empty file using the touch command.](images/9781284255805_CH07_CUM24.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-12)

The touch command creates the new file you specify and assigns your username as the file owner.

Notice that the file size is zero, since the touch command just created an empty file. The touch command can also be used to change the access and modification times on an existing file without changing the file contents:

![An output using the touch command is shown.](images/9781284255805_CH07_CUM25.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-13)

The modification time of test1 is now updated from the original time. If you want to change only the access time, use the -a parameter. To change only the modification time, use the -m parameter.

By default, touch uses the current time. You can specify the time by using the -t parameter with a specific timestamp value:

![An output uses the touch command with the hyphen t parameter.](images/9781284255805_CH07_CUM26.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-14)

Now the modification time for the file is set to a date in the future from the current time.

### Copying Files

Copying files and directories from one location in the filesystem to another is a common practice for system administrators. The [cp](#9781284254884_Glossary.xhtml_GLOS-59) command provides this feature.

In its most basic form, the cp command uses two parameters: the source object and the destination object:

![c p space source space destination.](images/9781284255805_CH07_CUM27.jpg)

When both the source and destination parameters are filenames, the cp command copies the source file to a new file with the filename specified as the destination. The new file acts like a brand new file, with an updated file creation and last modified times:

![An output shows the usage of the c p command to copy the source file to a new file.](images/9781284255805_CH07_CUM28.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-15)

The new file test2 shows a different inode number, indicating that it’s a completely new file. You’ll also notice that the modification time for the test2 file shows the time that it was created. If the destination file already exists, the cp command will prompt you to answer whether or not you want to overwrite it:

![Line 1: dollar space c p space test 1 space test 2\. Line 2: c p colon space overwrite space single quote test 2 single quote question mark space y. Line 3: dollar.](images/9781284255805_CH07_CUM29.jpg)

If you don’t answer y, the file copy will not proceed. You can also copy a file to an existing directory:

![An output shows the usage of the c p command to copy a file to an existing directory.](images/9781284255805_CH07_CUM30.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-16)

The new file is now under the dir1 directory, using the same filename as the original. These examples all used relative pathnames, but you can just as easily use the absolute pathname for both the source and destination objects.

To copy a file to the current directory you’re in, you can use the dot symbol:

![Line 1: dollar space c p space slash home slash rich slash d i r 1 slash test 1 dot. Line 2: c p colon space overwrite space single quote dot slash test 1 single quote question mark.](images/9781284255805_CH07_CUM31.jpg)

As with most commands, the cp command has a few command line parameters to help you out. These are shown in [TABLE 7-3](#9781284254884_CH07_05.xhtml_c7-tab003).

TABLE 7-3 The cp command parameters.

| Parameter | Description |
| --- | --- |
| -a | Archive files by preserving their attributes. |
| -b | Create a backup of each existing destination file instead of overwriting it. |
| -d | Preserve. |
| -f | Force the overwriting of existing destination files without prompting. |
| -i | Prompt before overwriting destination files. |
| -l | Create a file link instead of copying the files. |
| -p | Preserve file attributes if possible. |
| -r | Copy files recursively. |
| -R | Copy directories recursively. |
| -s | Create a symbolic link instead of copying the file. |
| -S | Override the backup feature. |
| -u | Copy the source file only if it has a newer date and time than the destination (update). |
| -v | Verbose mode, explaining what’s happening. |
| -x | Restrict the copy to the current filesystem. |

Use the -p parameter to preserve the file access or modification times of the original file for the copied file.

![An output preserves the file access or modification times of the original file for the copied file.](images/9781284255805_CH07_CUM32.jpg)[Description](9781284254884_Alt.xhtml_summary-cd7-17)

![An output preserves the file access or modification times of the original file for the copied file.](images/9781284255805_CH07_CUM33.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-18)

Now, even though the test3 file is a completely new file, it has the same timestamps as the original test1 file.

The -R parameter is extremely powerful. It allows you to recursively copy the contents of an entire directory in one command:

![An output copies the contents of an entire directory using the c p command with hyphen R parameter.](images/9781284255805_CH07_CUM34.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-19)

Now dir2 is a complete copy of dir1.

You can also use wildcard characters in your cp commands:

![An output shows the usage of the c p command to copy all of the files that started with test to d i r 2.](images/9781284255805_CH07_CUM35.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-20)

This command copied all of the files that started with test to dir2. The -f parameter forces the overwrite of the test1 file that was already in the directory without asking.

### Linking Files

You may have noticed a couple of the parameters for the cp command referred to linking files. This is a pretty cool option available in the Linux filesystems. If you need to maintain two (or more) copies of the same file on the system, instead of having separate physical copies, you can use one physical copy and multiple virtual copies, called [links](#9781284254884_Glossary.xhtml_GLOS-176). A link is a placeholder in a directory that points to the real location of the file. There are two different types of file links in Linux:

*   A [symbolic link](#9781284254884_Glossary.xhtml_GLOS-325) or soft link

*   A [hard link](#9781284254884_Glossary.xhtml_GLOS-130)

The hard link creates a separate file, but it points to the same inode number as the original file, so no physical file is created in the filesystem. The hard link file contains information about the original file just like a normal file. When you reference the hard link file, it’s just as if you’re referencing the original file:

![An output shows details of four files using the c p command with hyphen l parameter.](images/9781284255805_CH07_CUM36.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-21)

The -l parameter created a hard link for the test1 file called test4. The file listing shows that the inode numbers of both the test1 and test4 files are the same, indicating that, in reality, they are both the same file. Also notice that the link count (the third item in the listing) now shows that both files have two links.

On the other hand, the -s parameter creates a symbolic, or soft, link:

![An output shows details of five files using the c p command with hyphen s parameter.](images/9781284255805_CH07_CUM37.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-22)

There are a couple of things to notice in the file listing. First, you’ll notice that the new test5 file has a different inode number than the test1 file, indicating that the Linux system treats it as a separate file. Second, the file size is different. A linked file needs to store only information about the source file, not the actual data in the file. The filename area of the listing shows the relationship between the two files.

Be careful when copying linked files. If you use the cp command to copy a file that’s linked to another source file, all you’re doing is making another copy of the source file. This can quickly get confusing.

Instead of copying the linked file, you can create another link to the original file. You can have many links to the same file with no problems. However, you also don’t want to create soft links to other soft-linked files. This creates a chain of links that can not only be confusing but also be easily broken, causing all sorts of problems.

### Renaming Files

In the Linux world, renaming files is called moving. The [mv](#9781284254884_Glossary.xhtml_GLOS-214) command is available to move both files and directories to another location:

![An output shows details of five files and uses the m v command.](images/9781284255805_CH07_CUM38.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-23)

Notice that moving the file changed the filename but kept the same inode number and the timestamp value. Moving a file with soft links is a problem:

![An output shows details of five files and uses the m v command.](images/9781284255805_CH07_CUM39.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-24)

![An output shows details of five files and uses the m v command.](images/9781284255805_CH07_CUM40.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-25)

The test4 file that uses a hard link still uses the same inode number, which is perfectly fine. However, the test5 file now points to an invalid file, and it is no longer a valid link. If your terminal uses colors to identify file types, the test5 file will appear in red, indicating that it’s an invalid file. If you move the file back to the test1 file name (or create another file using the test1 file name) the test5 file link will become valid.

You can also use the mv command to move directories:

![Line 1: dollar space m v space d i r 2 space d i r 4.](images/9781284255805_CH07_CUM41.jpg)

The entire contents of the directory are unchanged. The only thing that changes is the name of the directory.

### Deleting Files

Most likely at some point in your Linux career you’ll want to be able to delete existing files. Whether it’s to clean up a filesystem or to remove a software package, there’s always opportunities to delete files.

In the Linux world, deleting is called removing. The command to remove files in Bash is [rm](#9781284254884_Glossary.xhtml_GLOS-288). The basic format of the rm command is pretty simple:

![An output uses the r m command and shows the details of four files.](images/9781284255805_CH07_CUM42.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-26)

Notice that the command prompts you to make sure that you’re serious about removing the file. There’s no trashcan in the CLI like there often is in the graphical desktop environment. Once you remove a file, it’s gone forever.

Now, here’s an interesting tidbit about deleting a file that has links to it:

![An output uses r m, l s, and cat commands and shows the details of three files.](images/9781284255805_CH07_CUM43.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-27)

![An output uses r m, l s, and cat commands and shows the details of three files.](images/9781284255805_CH07_CUM44.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-28)

In this example the test1 file was removed, which had both a hard link with the test4 file and a soft link with the test5 file. Noticed what happened. Both of the linked files still appear, even though the test1 file is now gone (although on my color terminal the test5 filename now appears in red). If you look at the contents of the test4 file that was a hard link, it still shows the contents of the file. If you try to look at the contents of the test5 file that was a soft link, Bash indicates that it doesn’t exist anymore.

Remember that the hard link file uses the same inode number as the original file. The hard link file maintains that inode number until you remove the last linked file, preserving the data! All the soft link file knows is that the underlying file is now gone, so it has nothing to point to. This is an important feature to remember when working with linked files.

One other feature of the rm command, if you’re removing lots of files and don’t want to be bothered with the prompt, is to use the -f parameter to force the removal. Just be careful!

## File Features

A few features are unique to Linux and you’ll need to be aware of them when working with files. This section walks through these features.

### Using Wildcards

The ls, cp, mv, and rm commands are handy, but specifying single file or directory names in the commands makes them somewhat clunky to work with on the Linux command line. If you want to work with more than one file or directory, you need to use a technique the Linux world calls [globbing](#9781284254884_Glossary.xhtml_GLOS-116).

Globbing is basically the use of wildcard characters to represent one or more characters in a file or directory name. That feature allows us to specify a pattern for Linux to match multiple files or directories against. There are two basic globbing characters that you can use:

*   The [question mark](#9781284254884_Glossary.xhtml_GLOS-271)—represents a single character

*   The [asterisk](#9781284254884_Glossary.xhtml_GLOS-21)—represents zero or more characters

The question mark is a stand-in character to represent any single character to match in the filename. For example, you can specify the filename file?.txt in a rm command to remove any file that starts with “file”, then has one character, then ends in “.txt”. Here’s an example:

![An output shows information about several files using the r m and l s commands.](images/9781284255805_CH07_CUM45.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-29)

![An output shows information about several files using the r m and l s commands.](images/9781284255805_CH07_CUM46.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-30)

The rm command uses the glob “file?.txt” as the parameter. Linux looks for any file in the directory that matches the pattern to remove. Two files, file1.txt and file2.txt, match the pattern. However, the file10.txt file doesn’t match the pattern because there are two characters between the “file” and “.txt” parts of the filename, and the file.txt file doesn’t match the pattern because there aren’t any characters between the “file” and “.txt” parts of the filename.

You use the asterisk glob character to match zero or more characters in the filename:

![An output shows details about four files using r m command with file asterisk dot t x t parameter.](images/9781284255805_CH07_CUM47.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-31)

By using the asterisk, Linux matched all of the files that started with “file” and ended with “.txt”, even the file.txt file! You can use the asterisk in any list, copy, move, or delete operation in the command line.

### Quoting

Another issue you may run into with Linux is files or directories that contain spaces in their names. This is perfectly legal in Linux but can cause headaches when working from the command line.

If you try to reference a file or directory that contains a space in the filename, you’ll get an error message:

![An output shows the usage of l s and r m commands.](images/9781284255805_CH07_CUM48.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-32)

![An output shows the usage of l s and r m commands.](images/9781284255805_CH07_CUM49.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-33)

The problem is that by default, the rm command uses a space to indicate the end of a filename, so it thinks you’re trying to remove three separate files – “long”, “file”, and “name.txt”!

There are two ways to get around that. One way is to use [quoting](#9781284254884_Glossary.xhtml_GLOS-272), which places quotes around any filenames that contain spaces:

![Line 1: dollar space r m space double quote long space file space name dot t x t double quote. Line 2: dollar space l s space hyphen l. Line 3: total space 0\. Line 4: dollar.](images/9781284255805_CH07_CUM50.jpg)

You can use either single or double quotes around the filename, as long as you use the same type on both ends of the filename.

The other method is to use [escaping](#9781284254884_Glossary.xhtml_GLOS-86), which places a backslash character in front of the character you want the Linux shell to interpret as a data character and not a shell character:

![Dollar space r m space long backslash space file backslash space name dot t x t.](images/9781284255805_CH07_CUM51.jpg)

Either method works just fine when working with spaces in file names.

### Case Sensitivity

One last thing to watch out for when using the Linux file handling command line commands is the case of any file or directory names that you’re working with. Linux is a case-sensitive operating system, so files and directories can have both upper and lower case letters in the names. Likewise, as you’re working with the files, make sure you reference the correct format of the files or directory names:

![An output shows the usage of r m command against files with similar names but with different cases.](images/9781284255805_CH07_CUM52.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-34)

This is a good example of when using filename globbing can come in handy. If you’re not sure of the case of a character, you can use the question mark to represent any character of any case:

![Line 1: dollar space r m space question mark i l e 1 dot t x t. Line 2: dollar.](images/9781284255805_CH07_CUM53.jpg)

This command will remove both the file1.txt and File1.txt files.

## Finding Files

With so many files stored on the Linux system, it can often become difficult to find the files you’re looking for. Fortunately, Linux provides a few different file-searching features for us to help out. This chapter takes a look at the ones you’ll most likely use and run into on the Linux Essentials exam.

### The which Command

You can use the [which](#9781284254884_Glossary.xhtml_GLOS-363) command to find where programs and utilities are stored. This can come in handy if you have two versions of a program installed on your system, or if you’re not sure if a command is built into the Linux shell, or supplied as a separate utility. The format for using the which command is pretty simple:

![Line 1: dollar space which space touch. Line 2: slash u s r slash bin slash touch. Line 3: dollar.](images/9781284255805_CH07_CUM54.jpg)

The output of the which command shows the full path to where the command is stored on the system. If you have two versions of a program on the system, the which command shows which one will run when you type it at the command line. If you need to use a different version, you have to use the full path to the program file.

### The locate Command

Most Linux distributions contain the [locate](#9781284254884_Glossary.xhtml_GLOS-182) command by default. The locate command uses a database that keeps track of the location of files on the system. When you use the locate command, it searches the database to find the requested file. This process is often quicker than trying to search through all of the files on the filesystem.

The key to the locate command is the information in the database. It can only find files that have been indexed into the database. The information in the database is updated by the appropriately named [updatedb](#9781284254884_Glossary.xhtml_GLOS-349) program. The Linux system runs the updatedb program in background mode on a regular basis to update the file database with any new files stored on the system.

Be careful when using the locate command though; you may get more than you bargained for! Here’s an example:

![An output of the locate command is shown.](images/9781284255805_CH07_CUM55.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd7-35)

The locate command returns any file that contains the word “touch” in the filename! You’ll need to filter through the results to find the file that you’re looking for.

Another downside to the locate command is that it can’t find any newly added files until the next running of the updatedb program. Some Linux systems run the updatedb program on a regular basis, every few minutes, while others only schedule it to run only once or twice a day. How often you need to run it depends on how often you get new files on your Linux system and how quickly you’d need to find them.

### The whereis Command

The [whereis](#9781284254884_Glossary.xhtml_GLOS-362) command is similar to the which command, in that it looks for a specific occurrence of the file you’re searching for. However, it only looks in binary file directories, library directories, and documentation directories, so that helps speed up the search process some. This is great for finding not only commands, but the documentation files that go along with them.

![Line 1: dollar space whereis space touch. Line 2: touch colon space slash u s r slash bin slash touch space slash u s r slash share slash man slash man 1 slash touch dot 1 dot g z. Line 3: dollar.](images/9781284255805_CH07_CUM56.jpg)

In this example, the whereis command retuned the location of the touch program file, and the location of the manual page associated with the touch program.

### The find Command

The last resort to finding files on your Linux system is the [find](#9781284254884_Glossary.xhtml_GLOS-104) command. It does a physical search through the virtual directory tree looking for the specified file. As you can imagine, the wider the search area, the longer it will take for the find command to return an answer. You specify the search area as the first parameter on the find command line:

![Line 1: dollar space find space slash home slash r b l u m space hyphen name space hello space hyphen print. Line 2: slash home slash r b l u m slash test slash hello. Line 3: dollar.](images/9781284255805_CH07_CUM57.jpg)

This example restricts the find command to looking in the /home/rblum directory structure for the file named hello. The -name option specifies the filename to look for, and the -print command tells the find command to display the results.

What makes the find command so versatile is that it can find files based on lots of different criteria besides just the file name, such as the creation time, the file owner, the file size, or even file permissions. For example, you can use the find command to look for all files over 1MB on your filesystem. [TABLE 7-4](#9781284254884_CH07_07.xhtml_c7-tab004) shows some of the options you can use in the find command.

TABLE 7-4 Useful find command options.

| Option | Description |
| --- | --- |
| -amin n | File was last accessed n minutes ago. |
| -atime n | File was last accessed n days ago. |
| -ctime n | File was last changed n minutes ago. |
| -inum n | Match the file inode number to the number specified. |
| -name | Match the file name to the pattern specified. |
| -perm | Match the file permissions to the pattern specified. |
| -size n | Match the file size to the amount specified. |
| -user | Match the file owner to the name specified. |

You can also use special modifiers on the find options, such as a plus sign for “greater than” or a minus sign for “less than.” For example, to list all of the files larger than 5000 characters, you’d use:

![Line 1: dollar space find space dot space hyphen size space plus 5000 c space hyphen print. Line 2: dot slash hello. Line 3: dollar.](images/9781284255805_CH07_CUM58.jpg)

The +5000c parameter tells the find command to look for files in the current directory that are more than 5,000 characters in size.

## Archiving Files

Storing data can get ugly. The more data you need to store, the more disk space it requires. While disk sizes are getting larger these days, there is still a limit to how much space you have. To help with that, you can use some Linux file archiving tools to help compress data files for storage and sharing. This section takes a look at how Linux handles compressing and archiving both files and directories.

### Compressing Files

If you’ve done any work in the Microsoft Windows world, no doubt you’ve used zip files. The PKZip compression utility became the de facto way to compress data and executable files in Windows, so much so that Microsoft eventually incorporated it into the Windows operating system starting with XP as the [compressed directories](#9781284254884_Glossary.xhtml_GLOS-53) feature. Compressed directories allow you to easily compress large files or a large group of files into smaller file that takes up less space and is easier to copy to another location.

Linux provides a few different tools you can use to compress files to save space. While this may sound great, it can sometimes lead to confusion and chaos when trying to download and extract Linux files from the Internet. [TABLE 7-5](#9781284254884_CH07_08.xhtml_c7-tab005) lists the different file compression utilities available in Linux.

TABLE 7-5 Linux file compression utilities.

| Utility | File extension | Description |
| --- | --- | --- |
| bzip2 | .bz2 | Uses the Burrows-Wheeler block sorting text compression algorithm and Human coding |
| compress | .Z | Original Unix file compression utility, but starting to fade away into obscurity |
| gzip | .gz | The GNU Project’s compression utility, uses the open source Lempel-Ziv coding |
| zip | .zip | The Unix version of the PKZip program for Windows |

The compress utility can work with files compressed on standard Unix systems but is not often installed by default on Linux systems. If you download a file with a .Z extension you can usually install the compress package from the distribution software repository. The zip utility creates compressed directories that can be extracted on Windows systems but is not the best compression algorithm to use if you’re keeping the files on a Linux system.

The [gzip](#9781284254884_Glossary.xhtml_GLOS-128) utility is the most popular compression tool used in Linux. It is a creation of the GNU Project, in their attempt to create a free version of the original Unix compress utility. This package includes three main files:

*   gzip for compressing files

*   gzcat for displaying the contents of compressed text files

*   gunzip for uncompressing files

The gzip command compresses the file you specify on the command line. You can also specify more than one filename, or even use wildcard characters to compress multiple files at once:

![Line 1: dollar space g zip space my asterisk. Line 2: dollar.](images/9781284255805_CH07_CUM59.jpg)

This gzip command compresses every file in the directory that starts with “my”.

### Creating Archive Files

Although the gzip command can not only compresses data, but also archive the data into a single file, it’s not the standard utility used for archiving large amounts of data in the Unix and Linux worlds. By far the most popular archiving tool used in Unix and Linux is the [tar](#9781284254884_Glossary.xhtml_GLOS-332) command.

The tar command was originally used to backup files to a tape device for archiving. However, it can also write the output to a file, which has become a popular way to bundle data for distribution in Linux. You can also then apply compression to the archive file, making it a compact way to store large quantities of files. It’s very common to see source code files bundled into a tar archive file (affectionately called a tarball) for distribution.

The following is the format of the tar command:

![tar space function space open bracket options close bracket space object 1 space object 2.](images/9781284255805_CH07_CUM60.jpg)

The function parameter defines what the tar command should do, as shown in [TABLE 7-6](#9781284254884_CH07_08.xhtml_c7-tab006).

TABLE 7-6 The tar command functions.

| Function | Description |
| --- | --- |
| -a | Appends an existing tar archive file to another tar archive file |
| -c | Creates a new tar archive file |
| -d | Checks the differences between a tar archive file and the filesystem files |
| -r | Appends files to an existing tar archive file |
| -t | Lists the contents of an existing tar archive file |
| -u | Appends files to an existing tar archive file that are newer than a file with the same in the archive |
| -x | Extract files from an existing tar archive file |

Each function uses one or more options to define a specific behavior for the tar archive file. [TABLE 7-7](#9781284254884_CH07_08.xhtml_c7-tab007) shows the options that you can use with the tar command:

TABLE 7-7 The tar command options.

| Option | Description |
| --- | --- |
| -C dir | Changes to the specified directory |
| -f file | Outputs results to the file (or device) specified. |
| -j | Redirects output to the bzip2 command for compression |
| -P | Preserves all file permissions |
| -v | Lists files as they are processed |
| -z | Redirects the output to the gzip command for compressions |

While the combination of several functions along with several options seems like an impossible task to remember, in reality you’ll find yourself just using a handful of combinations to do common tasks. The following section takes a look at the more common archiving scenarios that you’ll run into.

### Archiving Scenarios

Normally there are just three basic things you’ll need to do with the tar command:

*   Archive files to create a tarball

*   List the files contained in a tarball

*   Extract the files from a tarball

This helps narrow down the function and option features that you need to remember for the tar command.

To start off, you can create a new archive file using this command:

![tar space hyphen c v f space test dot tar space test slash space test 2 slash.](images/9781284255805_CH07_CUM61.jpg)

This command creates an archive file called test.tar containing the contents of both the test directory and the test2 directory. The -v option is a nice feature, in that it displays the files as they’re added to the archive file.

Next, to display the contents of a tarball file, you just use this command:

![tar space hyphen t f space test dot tar.](images/9781284255805_CH07_CUM62.jpg)

The -t function lists the contents of the tarball to the standard output by default, which is your monitor. The files aren’t extracted, just listed out.

Finally, to extract the files contained in a tarball, you’ll use this command:

![tar space hyphen x v f space test dot tar.](images/9781284255805_CH07_CUM63.jpg)

It extracts the contents of the tar file test.tar into the current directory. If the tar file was created from a directory structure, the entire directory structure is recreated starting at the current directory.

As you can see, using the tar command is a simple way to create archive files of entire directory structures. That’s why this has become a common method for distributing source code files for open source applications in the Linux world!

## Resources

Linux Documentation Project, “The Linux Filesystem Hierarchy,” Accessed on Oct. 17, 2015, from [http://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/](http://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/).

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 8
Networking Concepts

THESE DAYS IT’S ALMOST A NECESSITY to have your Linux system connected to some type of network. Whether it’s because of the need to share files and printers on a local network or the need to connect to the Internet to download updates and security patches, most Linux systems have some type of network connection.

This chapter looks at how to configure your Linux system to connect to a network as well as how to troubleshoot network connections if things go wrong. There are a few different methods for configuring network settings in Linux. First, the chapter covers the common locations for the configuration files in Linux distributions. Next, it examines the different tools you have at your disposal that help make configuring the network settings easier. After that, the chapter shows some simple network troubleshooting techniques you can use to help find the problem if anything goes wrong.

## Configuring Network Features

You need five main pieces of information to configure your Linux system to interact on a network:

*   The [host](#9781284254884_Glossary.xhtml_GLOS-135) address

*   The network subnet address

*   The default router (sometimes called gateway)

*   The system hostname

*   A Domain Name System (DNS) server address for resolving hostnames

There are three different ways to configure this information in Linux systems:

*   Manually editing network configuration files

*   Using a graphical tool included with your Linux distribution

*   Using command-line tools

The following sections walk through each of these methods.

### Network Configuration Files

Every Linux distribution uses network configuration files to define the network settings required to communicate on the network. Unfortunately, there’s not a single standard configuration file that all distributions use.

Instead, different distributions use different configuration files to define the network settings. [Table 8-1](#9781284254884_CH08_01.xhtml_c8-tab001) shows the most common network configuration files that you’ll run into.

Table 8-1 Linux network configuration files.

| Distribution | Network Configuration Location |
| --- | --- |
| Debian based | /etc/network/interfaces file |
| Red Hat based | /etc/sysconfig/network-scripts directory |
| openSUSE | /etc/sysconfig/network file |

While each of the Linux distributions uses a different method of defining the network settings, they all have similar features. Most configuration files define each of the required network settings as separate values in the configuration file. [LISTING 8-1](#9781284254884_CH08_01.xhtml_c8-list001) shows an example from a Debian-based Linux system.

The example shown in [Listing 8-1](#9781284254884_CH08_01.xhtml_c8-box001) assigns both an IP and an IPv6 address to the wired network interface designated as eth0.

[LISTING 8-2](#9781284254884_CH08_01.xhtml_c8-list002) shows how to define the IP network settings automatically using a DHCP server on the network.

If you just want to assign an IPv6 [link local address](#9781284254884_Glossary.xhtml_GLOS-175), which uniquely identifies the device on the local network, but not retrieve an IPv6 address from a DHCP server, replace the inet6 line with this:

![i face space eth 0 space i net 6 space auto.](images/9781284255805_CH08_CUM03.jpg)

The auto attribute tells Linux to assign the link local address, which allows the Linux system to communicate with any other IPv6 device on the local network but not a global address.

For Red Hat–based systems, you’ll need to define the network settings in multiple files, one for each network interface. The format of each file is:

![i f c f g hyphen interface.](images/9781284255805_CH08_CUM04.jpg)

where interface is the device name for the network adapter, such as ifcfg-enp0s3. [Listing 8-3](#9781284254884_CH08_01.xhtml_c8-list003) shows an example from a Rocky Linux system.

This configuration indicates that the workstation is using the DHCP process to automatically retrieve network information from a network server. For static IP addresses, you can set the IP address, default gateway, and subnet mask in the configuration file.

Most Linux distributions use the /etc/hostname file to store the local hostname of the system, however, some use /etc/HOSTNAME instead. You will also need to define a DNS server so that the system can resolve DNS hostnames. Fortunately, this is a standard that all Linux systems follow and is handled in the /etc/resolv.conf configuration file:

![Line 1: domain space my domain dot com. Line 2: search space my test dot com. Line 3: name server space 192 dot 168 dot 1 dot 1.](images/9781284255805_CH08_CUM06.jpg)

The domain entry defines the domain name assigned to the network. By default the system will append this domain name to any hostnames you specify. The search entry defines any additional domains used to search for hostnames. The nameserver entry is where you specify the DNS server assigned to your network. Some networks can have more than one DNS server; just add multiple nameserver entries in the file.

### Using Graphical Tools

The [Network Manager](#9781284254884_Glossary.xhtml_GLOS-220) tool is a popular program used by many Linux distributions to provide a graphical interface for defining network connections. The Network Manager tool starts automatically at boot time and appears in the system tray area of the desktop as an icon.

If your system detects a wired network connection, the icon appears as a mini-network with blocks connected together. If your system detects a wireless network connection, the icon appears as an empty radio signal. When you click the icon, you’ll see a list of the available wireless networks detected by the network card (as shown in [FIGURE 8-1](#9781284254884_CH08_01.xhtml_c8-fig001)).

![A screenshot shows Network Manager showing a wireless network connection.](images/9781284255805_CH08_FIGF01.jpg)

FIGURE 8-1 Network Manager showing a wireless network connection.Courtesy of Linux Foundation.

Courtesy of Linux Foundation.

[Description](9781284254884_Alt.xhtml_summary-fig8-1)

Click your access point to select it from the list. If your access point is encrypted, you’ll be prompted to enter the password to gain access to the network.

Once your system is connected to a wireless access point, the icon appears as a radio signal. Click the icon, and then select Edit Connections to edit the network connection settings for the system, shown in [FIGURE 8-2](#9781284254884_CH08_01.xhtml_c8-fig002).

![A screenshot shows the Network Connections window.](images/9781284255805_CH08_FIGF02.jpg)

FIGURE 8-2 The Network Connections window.Courtesy of Linux Foundation.

Courtesy of Linux Foundation.

[Description](9781284254884_Alt.xhtml_summary-fig8-2)

You can select the network connection to configure (either wireless or wired) and then click the Edit button to change the current configuration.

The Network Manager tool allows you to specify all four of the network configuration values by using the manual configuration option or to set the configuration to use DHCP to determine the settings. The Network Manager tool automatically updates the appropriate network configuration files with the updated settings.

### Using Command-Line Tools

If you’re not working with a graphical desktop client environment, you’ll need to use the Linux command-line tools to set the network configuration information. Quite a few command-line tools are at your disposal. The following sections cover the ones you’re most likely to run into.

#### Network Manager Command-Line Tools

The Network Manager tool also provides two different types of command-line tools:

*   nmtui provides a simple text-based menu tool.

*   nmcli provides a text-only command-line tool.

Both tools help guide you through the process of setting the required network information for your Linux system. The [nmtui](#9781284254884_Glossary.xhtml_GLOS-225) tool displays a stripped-down version of the graphical tool where you can select a network interface and assign network properties to it, as shown in [FIGURE 8-3](#9781284254884_CH08_01.xhtml_c8-fig003).

![A screenshot shows the Network Manager n m t u i command line tool.](images/9781284255805_CH08_FIGF03.jpg)

FIGURE 8-3 The Network Manager nmtui command-line tool.Courtesy of nmtui.

Courtesy of nmtui.

[Description](9781284254884_Alt.xhtml_summary-fig8-3)

The [nmcli](#9781284254884_Glossary.xhtml_GLOS-224) tool doesn’t attempt to use any type of graphics capabilities; it just provides a command-line interface where you can view and change the network settings. By default, the command displays the current network devices and their settings, as shown in [LISTING 8-4](#9781284254884_CH08_01.xhtml_c8-list004).

The nmcli command uses command-line options to allow you to set the network settings:

![The n m c l i command uses command line options.](images/9781284255805_CH08_CUM08.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-4)

This allows you to set all of the necessary network configuration features in a single nmcli command.

#### The iproute2 Utilities

The [iproute2](#9781284254884_Glossary.xhtml_GLOS-156) package is a newer open-source project that contains a set of command-line utilities for managing network connections. While the package contains several different programs, the ip program is the most used.

The [ip](#9781284254884_Glossary.xhtml_GLOS-155) command is the Swiss army knife of network programs and is becoming the more popular method for defining network settings from the command line. It uses several command options to display the current network settings or define new network settings. [Table 8-2](#9781284254884_CH08_01.xhtml_c8-tab002) shows these commands.

Table 8-2 The ip utility command options.

| Parameter | Description |
| --- | --- |
| address | Display or set the IPv4 or IPv6 address on the device. |
| addrlabel | Define configuration labels. |
| l2tp | Tunnel Ethernet over IP. |
| link | Define a network device. |
| maddress | Define a multicast address for the system to listen to. |
| monitor | Watch for netlink messages. |
| mroute | Define an entry in the multicast routing cache. |
| mrule | Define a rule in the multicast routing policy database. |
| neighbor | Manage ARP or NDISC cache entries. |
| netns | Manage network namespaces. |
| ntable | Manage the neighbor cache operation. |
| route | Manage the routing table. |
| rule | Manage entries in the routing policy database. |
| tcpmetrics | Mange TCP metrics on the interface. |
| token | Manage tokenized interface identifiers. |
| tunnel | Tunnel over IP. |
| tuntap | Manage TUN/TAP devices. |
| xfrm | Manage IPSec policies for secure connections. |

Each command option utilizes parameters to define what to do, such as display network settings or modify existing network settings. [LISTING 8-5](#9781284254884_CH08_01.xhtml_c8-list005) demonstrates how to display the current network settings using the show parameter.

This example shows two network interfaces on the Linux system:

*   lo is the local loopback interface.

*   enp0s3 is a wired network interface.

The [local loopback interface](#9781284254884_Glossary.xhtml_GLOS-181) is a special virtual network interface. Any local program can use it to communicate with other programs on the system just as if they were across a network. That can simplify transferring data between programs.

The enp0s3 network interface is the wired network connection for the Linux system. The ip command shows the IP address assigned to the interface (there’s both an IP and an IPv6 link local address assigned), the netmask value, and some basic statistics about the packets on the interface.

If the output doesn’t show a network address assigned to the interface, you can use the ip command to specify the host address and netmask values for the interface:

![Hash space i p space address space add space 10 dot 0 dot 2 dot 15 slash 24 space dev space e n p 0 s 3.](images/9781284255805_CH08_CUM11.jpg)

Then use the ip command with the route option to set the default router for the network interface:

![Hash space i p space route space add space default space via space 192 dot 168 dot 1 dot 254 space dev space e n p 0 s 3.](images/9781284255805_CH08_CUM12.jpg)

Then finally, make the network interface active by using the link option:

![Hash space i p space link space set space e n p 0 s 3 space up.](images/9781284255805_CH08_CUM13.jpg)

With the single ip command you can manage just about everything you need for your network connections.

#### The net-tools Legacy Tool

If you need to work on an older Linux distribution, the [net-tools](#9781284254884_Glossary.xhtml_GLOS-217) package may be all you have to work with. The net-tools package was the original method in Linux for managing individual aspects of the network configuration. You need to use four main command-line tools:

*   [ethtool](#9781284254884_Glossary.xhtml_GLOS-87) displays Ethernet settings for a network interface.

*   [ifconfig](#9781284254884_Glossary.xhtml_GLOS-139) displays or sets the IP address and netmask values for a network interface.

*   iwconfig sets the SSID and encryption key for a wireless interface.

*   route sets the default router address.

The ethtool command allows you to peek inside the network interface card Ethernet settings and change any properties that you may need to communicate with a network device, such as a switch.

By default, the ethtool command displays the current configuration settings for the network interface, as shown in [LISTING 8-6](#9781284254884_CH08_01.xhtml_c8-list006).

You can change features such as speed, duplex, and whether or not the network interface attempts to auto-negotiate features with the switch.

The ifconfig command is a legacy command that allows you to set the network address and subnet mask for a network interface:

![Dollar space sudo space if config space e n p 0 s 3 space down space 10 dot 0 dot 2 dot 10 space net mask space 255 dot 255 dot 255 dot 0.](images/9781284255805_CH08_CUM15.jpg)

You can also use the ifconfig command to view the current statistics for a network interface, as shown in [LISTING 8-7](#9781284254884_CH08_01.xhtml_c8-list007).

Using the ifconfig command you can see the link status of a network interface, whether it is receiving or transmitting packets and whether there were any dropped packets or collisions. This can be a handy network troubleshooting tool.

With the net-tools package you must set the default router using the separate route command:

![Hash space route space add space default space g w space 192 dot 168 dot 1 dot 254.](images/9781284255805_CH08_CUM17.jpg)

You can also use the route command by itself to view the current default router configured for the system.

![An output shows the current default router configured for the system using the route command.](images/9781284255805_CH08_CUM18.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-8)

![Continuation](images/9781284255805_CH08_CUM19.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-9)

The default router defined for the Linux system is 192.168.1.254 and is available from the enp0s3 network interface. The output also shows that to get to the 192.168.1.0 network, you don’t need a gateway because that’s the local network the Linux system is connected to.

If your network is connected to multiple networks via multiple routers, you can manually create the routing table in the system by using the add or del command-line option for the route command. The format for that is

![route space open bracket add close bracket space open bracket del close bracket space target space g w space gateway.](images/9781284255805_CH08_CUM20.jpg)

where target is the target host or network and gateway is the router address.

If you’re working with a wireless network card, you must assign the wireless SSID and encryption key values using the iwconfig command:

![Line 1: hash space i w config space w l p 6 s 0 space e s s i d space double quote My Network double quote space key. Line 2: s colon my password.](images/9781284255805_CH08_CUM21.jpg)

The essid parameter specifies the access point SSID name, and the key parameter specifies the encryption key required to connect to it. Notice that the encryption key is preceded by an s:. That allows you to specify the encryption key in ASCII text characters; otherwise you’ll need to specify the key using hexadecimal values.

If you don’t know the name of a local wireless connection, you can use the iwlist command to display all of the wireless signals your wireless card detects. Just specify the name of the wireless device and use the scan option:

![Dollar space sudo space i w list space w l p 6 s 0 space scan.](images/9781284255805_CH08_CUM22.jpg)

Once you’ve set the wireless network card configuration, you can proceed to assign it an IP address and default route the same as you would a wired network card.

#### Additional Network Features

If your network uses Dynamic Host Configuration Protocol (DHCP), you’ll need to ensure that a proper DHCP client program is running on your Linux system. The DHCP client program communicates with the network DHCP server in the background and assigns the necessary Internet Protocol (IP) address settings as directed by the DHCP server. Three common DHCP programs are available for Linux systems:

*   dhcpcd

*   dhclient

*   pump

The dhcpcd program is becoming the most popular of the three, but you’ll still see the other two used in some Linux distributions.

When you use your Linux system’s software package manager utility to install the DHCP client program, it sets the program to automatically launch at boot time and handle the IP address configuration needed to interact on the network.

## Basic Network Troubleshooting

Once you have a Linux kernel installed, you can do a few things to check to make sure things are operating properly. The following sections walk through the commands you should know to monitor the network activity, including watching what processes are listening on the network and what connections are active from your system.

### Sending Test Packets

One way to test network connectivity is to send test packets to known hosts. Linux provides the [ping](#9781284254884_Glossary.xhtml_GLOS-251) and [ping6](#9781284254884_Glossary.xhtml_GLOS-252) commands to do that. The ping and ping6 commands send [Internet Control Message Protocol (ICMP)](#9781284254884_Glossary.xhtml_GLOS-152) packets to remote hosts using either the IP (ping) or IPv6 (ping6) protocol. ICMP packets work behind the scenes to track connectivity and provide control messages between systems. If the remote host supports ICMP, it will send a reply packet back when it receives a ping packet.

The basic format for the ping command is to specify the IP address of the remote host:

![An output shows the usage of the ping command with a specific I P address.](images/9781284255805_CH08_CUM24.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-11)

![An output shows the usage of the ping command with a specific I P address.](images/9781284255805_CH08_CUM25.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-12)

The ping command continues sending packets until you press Ctrl+C. You can also use the -c command-line option to specify a set number of packets to send and then stop.

For the ping6 command, things get a little more complicated. If you’re using an IPv6 link local address, you also need to tell the command which interface to send the packets out on:

![An output shows the usage of the ping 6 command.](images/9781284255805_CH08_CUM26.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-13)

The %enp0s3 part tells the system to send the ping packets out the enp0s3 network interface for the link local address.

Yet another useful tool is the traceroute command. The traceroute command utilizes a feature of ICMP packets that restrict the number of network routers packets can traverse (called “hops”) before reaching their destination. By manipulating that value in the packet, the traceroute command allows you to see the network routers used to get the packets from the client to the server.

Finally, the mtr program is a package that utilizes data retrieved from ping and traceroute commands to document network availability and latency in a real-time chart. [FIGURE 8-4](#9781284254884_CH08_02.xhtml_c8-fig004) shows the output of the mtr command tracing the connectivity to the linux.org server.

![A screenshot shows the usage of the m t r to monitor network connectivity to a server.](images/9781284255805_CH08_FIGF04.jpg)

FIGURE 8-4 Using mtr to monitor network connectivity to a server.Courtesy of BitWizard.

Courtesy of BitWizard.

[Description](9781284254884_Alt.xhtml_summary-fig8-4)

### Finding Host Information

Sometimes the problem isn’t with network connectivity but with the DNS hostname system. You can test a hostname using the host command:

![An output tests a hostname using the host command.](images/9781284255805_CH08_CUM27.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-14)

The host command queries the DNS server to determine the IP addresses assigned to the specified hostname. By default it returns all IP addresses associated with the hostname. Some hosts are supported by multiple servers in a load balancing configuration. The host command will show all of the IP addresses associated with those servers:

![An output shows all of the I P addresses associated with servers using the host command.](images/9781284255805_CH08_CUM28.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-15)

You can also specify an IP address for the host command, and it will attempt to find the hostname associated with it:

![An output attempts to find the hostname associated with an I P address using the host command.](images/9781284255805_CH08_CUM29.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-16)

Notice, though, that often an IP address will resolve to a generic server hostname that hosts the website and not the website alias, as is the case here with the www.linux.org IP address.

Another great tool to use is the [dig](#9781284254884_Glossary.xhtml_GLOS-70) command. The dig command displays all the DNS data records associated with a specific host or network. For example, you can look up the information for a specific hostname:

![An output displays all the D N S data records associated with a specific host using the dig command.](images/9781284255805_CH08_CUM30.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-17)

Or you can look up DNS data records associated with a specific network service, such as a mail server:

![An output shows D N S data records associated with a specific network service.](images/9781284255805_CH08_CUM31.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-18)

![An output shows D N S data records associated with a specific network service.](images/9781284255805_CH08_CUM32.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-19)

If you need to look up DNS information for multiple servers or domains, the nslookup command provides an interactive interface where you can enter commands:

![An output shows D N S information for multiple domains using the n s lookup command.](images/9781284255805_CH08_CUM33.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-20)

You can also dynamically specify the address of another DNS server to use for the name lookups, which is a handy way to determine if your default DNS server is at fault if a name resolution fails.

One final tool that can be useful is the [whois](#9781284254884_Glossary.xhtml_GLOS-364) command. The whois command attempts to connect to the centralized Internet domain registry at whois.networksolutions.com and retrieve information about who registered the requested domain name. [LISTING 8-8](#9781284254884_CH08_02.xhtml_c8-list008) shows a partial output from the whois command.

Theoretically the registry contains complete contact information for the owner of the domain, but these days, due to privacy concerns, that information is usually blocked. There is usually though a contact email address for the domain in case you need to report suspected abuse from the domain.

## Advanced Network Troubleshooting

Besides the simple network tests shown in the previous section, Linux has some more advanced programs that can provide more detailed information about the network environment. Sometimes it helps to be able to see just what network connections are active on a Linux system. There are two ways to troubleshoot that issue: the [netstat](#9781284254884_Glossary.xhtml_GLOS-216) command and the [ss](#9781284254884_Glossary.xhtml_GLOS-317) command.

### The netstat Command

The netstat command is part of the net-tools package and can provide a wealth of network information for you. By default, it lists all the open network connections on the system:

![An output lists all the open network connections on the system using the net stat command.](images/9781284255805_CH08_CUM35.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-22)

![An output lists all the open network connections on the system using the net stat command.](images/9781284255805_CH08_CUM36.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-23)

The netstat command produces lots of output because there are normally lots of programs that use network services on Linux systems. You can limit the output to just TCP or UDP connections by using the –t command-line option for TCP connections or –u for UDP connections:

![An output shows T C P connections using the net stat command with the hyphen t command line option.](images/9781284255805_CH08_CUM37.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-24)

You can also get a list of what applications are listening on which network ports by using the –l option:

![An output shows a list of what applications are listening on which network ports using the hyphen l option.](images/9781284255805_CH08_CUM38.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-25)

![An output shows a list of what applications are listening on which network ports using the hyphen l option.](images/9781284255805_CH08_CUM39.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-26)

As you can see, just a standard Linux workstation still has lots of things happening in the background, waiting for connections.

Yet another great feature of the netstat command is that the –s option displays statistics for the different types of packets the system has used on the network:

![An output displays statistics for the different types of packets the system has used on the network using the net stat command with hyphen s option.](images/9781284255805_CH08_CUM40.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-27)

![An output displays statistics for the different types of packets the system has used on the network using the net stat command with hyphen s option.](images/9781284255805_CH08_CUM41.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-28)

The netstat statistics output can give you a rough idea of how busy your Linux system is on the network or if there’s a specific issue with one of the protocols installed.

### Examining Sockets

The netstat tool provides a wealth of network information, but it can often be hard to determine just which program is listening on which open port. The ss command can come to your rescue for that.

A program connection to a port is called a socket. The ss command can link which system processes are using which network sockets that are active:

![An output links which system processes are using which network sockets that are active using the s s command.](images/9781284255805_CH08_CUM42.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd8-29)

The -anpt option displays both listening and established Transmission Control Protocol (TCP) connections and the process they’re associated with. This output shows that the SSH port (port 22) has an established connection and is controlled by process ID 15176, the ssh program.

## Resources

Linux Kernel Project, “Linux Networking Documentation,” Accessed on Dec. 22, 2021, from [https://www.kernel.org/doc/html/v5.8/networking/index.xhtml](https://www.kernel.org/doc/html/v5.8/networking/index.xhtml).

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 9
Managing Processes

LINUX SERVERS HAVE to keep track of lots of different applications running on the system. Your goal as the Linux administrator is to make sure everything runs smoothly and at the correct time! This chapter shows just how Linux keeps track of all the active programs and how you can manage that information.

## Looking at Processes

At any given time lots of active programs are running on the Linux system. Linux calls each running program a [process](#9781284254884_Glossary.xhtml_GLOS-265). A process can run in the foreground, displaying output on a console display or graphical desktop window, or it can run in background, working on data behind the scenes. The Linux system assigns each process a process id (or PID) and manages how the process uses memory and CPU time based on that PID.

When a Linux system first boots, it starts a special process called the init process. The init process is the core of the Linux system; it runs scripts that start all of the other processes running on the system, including the processes that start any text consoles or graphical windows you use to log in.

You can watch just which processes are currently running on your Linux system by using the [ps](#9781284254884_Glossary.xhtml_GLOS-267) command. The default output of the ps command looks like this:

![An output shows the processes currently running on the Linux system using the p s command.](images/9781284255805_CH09_CUM01.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-1)

By default the ps command only shows the processes that are running in the current user shell. In this example, I only had the command prompt shell running (bash), and of course, the ps command itself.

The basic output of the ps command shows the PID assigned to each process, the terminal (TTY) that they were started from, and the CPU time that the process has used.

The tricky feature of the ps command (and what makes it so complicated) is that at one time there were two versions of it in Linux. Each version had its own set of command-line parameters controlling the information it displayed. That made switching between systems somewhat complicated.

The GNU developers decided to merge the two versions into a single ps program and, of course, added some additional parameters of their own. Thus, the current ps program used in Linux supports three different styles of command-line parameters:

*   Unix style parameters, which are preceded by a dash

*   BSD style parameters, which are not preceded by a dash

*   GNU long parameters, which are preceded by a double dash

This makes for lots of possible parameters and options to use with the ps command. You can consult the ps manual page to see all of the possible parameters that are available. Most Linux administrators have their own set of commonly used parameters that they remember for extracting pertinent information. For example, if you need to see every process running on the system, use the Unix-style -ef parameter combination, like this:

![An output shows every process running on the system using the p s command with hyphen e f parameter.](images/9781284255805_CH09_CUM02.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-2)

This format provides some useful information about the processes running:

*   UID—The user responsible for running the process

*   PID—The process ID of the process

*   PPID—The process ID of the parent process (if the process was started by another process)

*   C—The processor utilization over the lifetime of the process

*   STIME—The system time when the process was started

*   TTY—The terminal device from which the process was started

*   TIME—The cumulative CPU time required to run the process

*   CMD—The name of the program that was started in the process

Also notice in the -ef output that some process command names are shown in brackets. By default the ps output will show the complete command line used to start the program, including any command-line parameters. If it can’t determine the command-line parameters, it places brackets around the main program name.

Processes that are swapped into virtual memory are called sleeping. Often the Linux kernel places a process into sleep mode while the process is waiting for an event. When the event triggers, the kernel sends the process a signal. If the process is in interruptible sleep mode, it will receive the signal immediately and wake up. If the process is in uninterruptible sleep mode, it only wakes up based on an external event, such as hardware becoming available. It will accumulate any other signals sent while it was sleeping and act on them once it wakes up.

## Monitoring Processes in Real Time

The ps command is a great way to get a snapshot of the processes running on the system, but sometimes you need to see more information to get an idea of just what’s going on in your Linux system. If you’re trying to find trends about processes that are frequently swapped in and out of memory, it’s hard to do that with the ps command.

Instead, the [top](#9781284254884_Glossary.xhtml_GLOS-339) command can solve this problem. The top command displays process information similar to the ps command, but it does it in real-time mode. [FIGURE 9-1](#9781284254884_CH09_02.xhtml_c9-fig001) shows a snapshot of the top command in action.

![A screenshot shows the output of the top command.](images/9781284255805_CH09_FIGF01.jpg)

FIGURE 9-1 The output of the top command.Courtesy of Linux Foundation.

Courtesy of Linux Foundation.

[Description](9781284254884_Alt.xhtml_summary-fig9-1)

The first section of the top output shows general system information. The first line shows the current time, how long the system has been up, the number of users logged in, and the load average on the system.

The load average appears as three numbers: the 1-minute, 5-minute, and 15-minute load averages. The higher the values, the more load the system is experiencing. It’s not uncommon for the 1-minute load value to be high for short bursts of activity. If the 15-minute load value is high, your system may be in trouble.

The second line shows general process information (called tasks in top): how many processes are running, sleeping, stopped, or in a zombie state.

The next line shows general CPU information. The top display breaks down the CPU utilization into several categories depending on the owner of the process (user versus system processes) and the state of the processes (running, idle, or waiting).

Following that are two lines that detail the status of the system memory. The first line shows the status of the physical memory in the system, how much total memory there is, how much is currently being used, and how much is free. The second memory line shows the status of the swap memory area in the system (if any is installed), with the same information.

Finally, the next section shows a detailed list of the currently running processes, with some information columns that should look familiar from the ps command output:

*   PID—The process ID of the process

*   USER—The user name of the owner of the process

*   PR—The priority of the process

*   NI—The nice value of the process

*   VIRT—The total amount of virtual memory used by the process

*   RES—The amount of physical memory the process is using

*   SHR—The amount of memory the process is sharing with other processes

*   S—The process status (D = interruptible sleep, R = running, S = sleeping, T = traced or stopped, or Z = zombie)

*   %CPU—The share of CPU time that the process is using

*   %MEM—The share of available physical memory the process is using

*   TIME+—The total CPU time the process has used since starting

*   COMMAND—The command line name of the process (program started)

By default, when you start top, it sorts the processes based on the %CPU value. You can change the sort order by using one of several interactive commands while top is running. Each interactive command is a single character you can press while top is running and changes the behavior of the program. These commands are shown in [TABLE 9-1](#9781284254884_CH09_02.xhtml_c9-tab001).

TABLE 9-1 The top interactive commands.

| Command | Description |
| --- | --- |
| 1 | Toggle the single CPU and Symmetric Multiprocessor (SMP) state. |
| b | Toggle the bolding of important numbers in the tables. |
| I | Toggle Irix/Solaris mode. |
| z | Configure color for the table. |
| l | Toggle the displaying of the load average information line. |
| t | Toggle the displaying of the CPU information line. |
| m | Toggle the displaying of the MEM and SWAP information lines. |
| f | Add or remove different information columns. |
| o | Change the display order of information columns. |
| F or O | Select a field on which to sort the processes (%CPU by default). |
| < or > | Move the sort field one column left (<) or right (>). |
| r | Toggle the normal or reverse sort order. |
| h | Toggle the showing of threads. |
| c | Toggle the showing of the command name or the full command line (including parameters) of processes. |
| i | Toggle the showing of idle processes. |
| S | Toggle the showing of the cumulative CPU time or relative CPU time. |
| x | Toggle highlighting of the sort field. |
| y | Toggle highlighting of running tasks. |
| z | Toggle color and mono mode. |
| u | Show processes for a specific user. |
| n or # | Set the number of processes to display. |
| k | Kill a specific process (only if process owner or if root user). |
| r | Change the priority (renice) of a specific process (only if process owner or if root user). |
| d or s | Change the update interval (default three seconds). |
| W | Write current settings to a configuration file. |
| q | Exit the top command. |

You have lots of control over the output of the top command. Use the F or O command to toggle which field the sort order is based on. You can also use the r interactive command to reverse the current sorting. Using this tool, you can often find offending processes that have taken over your system.

## Managing Processes

One of the jobs of a Linux system administrator is to be on the watch for runaway processes that can take down the Linux system. You’ve already seen how to use the ps and top commands (or the System Monitor graphical tool) to monitor how processes are doing on the system, the next step is to see how to stop a runaway process.

### Setting Priorities

By default, all processes running on the Linux system are created equal, that is, they all have the same priority to obtain CPU time and memory resources. However, you may run some applications that either don’t need to have the same level of priority or that may need a higher level of priority.

The [nice](#9781284254884_Glossary.xhtml_GLOS-223) and [renice](#9781284254884_Glossary.xhtml_GLOS-285) commands allow you to set and change the priority level assigned to an application process. The nice command allows you to start an application with a non-default priority setting. The format looks like this:

![nice space hyphen n space value space command.](images/9781284255805_CH09_CUM03.jpg)

The value parameter is a numeric value from –20 to 19\. The lower the number, the higher priority the process receives. The default priority is zero. The command parameter specifies the program to start at the specified priority.

To change the priority of a process that’s already running, use the renice command:

![renice space priority space open bracket hyphen p space pids close bracket space open bracket hyphen u space users close bracket space open bracket hyphen g space groups close bracket.](images/9781284255805_CH09_CUM04.jpg)

The renice command allows you to change the priority of multiple processes based on a list of PID values, all of the processes started by one or more users, or all of the processes started by one or more groups. Only the root user account can set a priority value less than 0 or decrease the priority value (increase the priority) of a running process.

### Stopping Processes

Sometimes a process gets hung up and just needs a gentle nudge to either get going again or stop. Other times, a process runs away with the CPU and refuses to give it up. In both cases, you need a command that will allow you to control a process. To do that, Linux follows the Unix method of inter-process communication.

In Linux, processes communicate with each other using process signals. A process signal is a predefined message that processes recognize and may choose to ignore or act on. The developers program how a process handles signals. Most well-written applications have the ability to receive and act on the standard Unix process signals. These signals are shown in [TABLE 9-2](#9781284254884_CH09_03.xhtml_c9-tab002).

TABLE 9-2 Linux process signals.

| Number | Name | Description |
| --- | --- | --- |
| 1 | HUP | Hang up. |
| 2 | INT | Interrupt. |
| 3 | QUIT | Stop running. |
| 9 | KILL | Unconditionally terminate. |
| 11 | SEGV | Segment violation. |
| 15 | TERM | Terminate if possible. |
| 17 | STOP | Stop unconditionally, but don’t terminate. |
| 18 | TSTP | Stop or pause, but continue to run in background. |
| 19 | CONT | Resume execution after STOP or TSTP. |

While a process can send a signal to another process, two commands are available in Linux that allow you to send process signals to running processes.

#### The kill Command

The [kill](#9781284254884_Glossary.xhtml_GLOS-168) command allows you to send signals to processes based on their process ID (PID). By default, the kill command sends a TERM signal to all the PIDs listed on the command line. Unfortunately, you can only use the process PID instead of its command name, making the kill command difficult to use sometimes.

To send a process signal, you must either be the owner of the process or be logged in as the root user.

![Line 1: dollar kill space 3940\. Line 2: hyphen bash colon space kill colon space open parenthesis 3940 close parenthesis hyphen Operation not permitted. Line 3: dollar.](images/9781284255805_CH09_CUM05.jpg)

The TERM signal only asks the process to kindly stop running. Unfortunately, if you have a runaway process, most likely it will ignore the request. When you need to get forceful, the ‐s parameter allows you to specify other signals (either using their name or signal number).

The generally accepted procedure is to first try the TERM signal. If the process ignores that, try the INT or HUP signals. If the program recognizes these signals, it will try to gracefully stop doing what it was doing before shutting down. The most forceful signal is the KILL signal. When a process receives this signal, it immediately stops running. Use this as a last resort, as it can lead to corrupt files.

One of the scary things about the kill command is that there’s no output from it:

![Line 1: dollar space sudo space kill space hyphen s space H U P space 3 9 4 0\. Line 2: dollar.](images/9781284255805_CH09_CUM06.jpg)

To see if the command was effective, you’ll have to perform another ps or top command to see if the offending process stopped.

#### The pkill Command

The [pkill](#9781284254884_Glossary.xhtml_GLOS-254) command is a powerful way to stop processes by using their names rather than the PID numbers. The pkill command allows you to use wildcard characters as well, making it a very useful tool when you’ve got a system that’s gone awry:

![Line 1: dollar space sudo space p kill space h t t p asterisk. Line 2: dollar.](images/9781284255805_CH09_CUM07.jpg)

This example will kill all of the processes that start with http, such as the httpd services for the Apache web server. Be careful with the search capability of the pkill command. It’s usually a good idea to check the search term against the currently running processes to make sure you don’t accidentally kill any other processes that match the search. The pgrep command allows you to display all processes that match the search term.

## Running Programs in Background Mode

There are times when running a program directly from the command-line interface is inconvenient. Some programs can take a long time to process, and you may not want to tie up the command-line interface waiting. While the program is running, you can’t do anything else in your terminal session. Fortunately, there’s a simple solution to that problem.

When you use the ps command, you see a whole bunch of different processes running on the Linux system. Obviously, all of these processes are not running on your terminal monitor. This is called running processes in the background. In background mode, a process runs without being associated with a terminal session.

You can exploit this feature with your programs as well, allowing them to run behind the scenes and not lock up your terminal session. The following sections describe how to run programs in background mode on your Linux system.

### Running in the Background

Running a program or script in background mode is a fairly easy thing to do. To run something in background mode from the command-line interface, just place an ampersand symbol after the command:

![A script shows ampersand symbol placed after the command to run the program in background mode.](images/9781284255805_CH09_CUM08.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-3)

When you place the ampersand symbol after a command, it separates the command from the Bash shell and runs it as a separate background process on the system. The first thing that displays is the line:

![Open bracket 1 close bracket space 1976.](images/9781284255805_CH09_CUM09.jpg)

The number in the square brackets is the job number assigned to the background process by the shell. The next number is the PID assigned to the process.

As soon as the system displays these items, a new command-line interface prompt appears. You are returned back to the shell, and the command you executed runs safely in background mode.

At this point, you can enter new commands at the prompt (as shown in the example). However, while the background process is still running, it still uses your terminal monitor for messages. You’ll notice from the example that the output from the test1.sh script appears in the output intermixed with any other commands that are run from the shell.

When the background process finishes, it displays a message on the terminal:

![Open bracket 1 close bracket plus space Done space dot slash test 1 dot s h.](images/9781284255805_CH09_CUM10.jpg)

This shows the job number and the status of the job (Done), along with the command used to start the job.

### Running Multiple Background Jobs

You can start any number of background jobs at the same time from the command-line prompt:

![A script starts multiple background jobs at the same time from the command line prompt.](images/9781284255805_CH09_CUM11.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-4)

Each time you start a new job, the Linux system assigns it a new job number and PID. You can see that all of the scripts are running using the ps command:

![An output shows running processes using the p s command.](images/9781284255805_CH09_CUM12.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-5)

![An output shows running processes using the p s command.](images/9781284255805_CH09_CUM13.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-6)

Each of the background processes you start appears in the ps command output listing of running processes. If all of the processes display output in your terminal session, things can get pretty messy pretty quickly. The next section walks through a solution.

## Running Programs Without a Console

There will be times when you want to start a shell script from a terminal session and then let the script run in background mode until it finishes, even if you exit the terminal session. You can do this by using the [nohup](#9781284254884_Glossary.xhtml_GLOS-227) command.

The nohup command runs another command blocking any SIGHUP signals that are sent to the process. This prevents the process from exiting when you exit your terminal session.

The format used for the nohup command is as follows:

![The format used for the no hup command is shown.](images/9781284255805_CH09_CUM14.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-7)

As with a normal background process, the shell assigns the command a job number, and the Linux system assigns a PID number. The difference is that when you use the nohup command, the script ignores any SIGHUP signals sent by the terminal session if you close the session.

Because the nohup command disassociates the process from the terminal, the process loses the output links to the terminal. To accommodate any output generated by the command, the nohup command automatically redirects any output messages to a file, called nohup.out.

The nohup.out file contains all of the output that would normally be sent to the terminal monitor. After the process finishes running, you can view the nohup.out file for the output results:

![The no hup dot out file is shown for the output results.](images/9781284255805_CH09_CUM15.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-8)

![The no hup dot out file is shown for the output results.](images/9781284255805_CH09_CUM16.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-9)

The output appears in the nohup.out file just as if the process ran on the command line! Be careful though; if you run multiple programs using nohup, they all send their output to the same nohup.out file.

## Job Control

The function of starting, stopping, killing, and resuming jobs is called job control. With job control, you have full control over how processes run in your shell environment. This section describes the commands to use to view and control jobs running in your shell.

### Viewing Jobs

The key command for job control is the [jobs](#9781284254884_Glossary.xhtml_GLOS-159) command. The jobs command allows you to view the current jobs being handled by the shell:

![An output shows the current jobs being handled by the shell using the jobs command.](images/9781284255805_CH09_CUM17.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-10)

![An output shows the current jobs being handled by the shell using the jobs command.](images/9781284255805_CH09_CUM18.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-11)

The script uses the $$ variable to display the PID that the Linux system assigns to the script; then it goes into a loop, sleeping for 10 seconds at a time for each iteration. In the example, the first script is started from the command-line interface and then paused using the Ctrl+Z key combination. Next, another job is started as a background process, using the ampersand symbol. To make life a little easier, the output of that script is redirected to a file so that it doesn’t appear on the screen.

After the two jobs were started, use the jobs command to view the jobs assigned to the shell. The jobs command shows both the stopped and the running jobs, along with their job numbers and the commands used in the jobs.

The jobs command uses a few different command line parameters, as shown in [TABLE 9-3](#9781284254884_CH09_06.xhtml_c9-tab003).

TABLE 9-3 The jobs command parameters.

| Parameter | Description |
| --- | --- |
| -l | List the PID of the process along with the job number. |
| -n | List only jobs that have changed their status since the last notification from the shell. |
| -p | List only the PIDs of the jobs. |
| -r | List only the running jobs. |
| -s | List only stopped jobs. |

You probably noticed the plus and minus signs in the jobs command output. The job with the plus sign is considered the default job. It would be the job referenced by any job control commands if a job number isn’t specified in the command line. The job with the minus sign is the job that would become the default job when the current default job finishes processing. There will only be one job with the plus sign and one job with the minus sign at any time, no matter how many jobs are running in the shell.

The following is an example showing how the next job in line takes over the default status, when the default job is removed:

![An output shows how the next job in line takes over the default status, when the default job is removed.](images/9781284255805_CH09_CUM19.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-12)

![An output shows how the next job in line takes over the default status, when the default job is removed.](images/9781284255805_CH09_CUM20.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-13)

In this example, three separate scripts were started and then stopped. The jobs command listing shows the three processes and their status. Note that the default process (the one listed with the plus sign) is the last process started.

Then the kill command was issued to send a SIGHUP signal to the default process. In the next jobs listing, the job that previously had the minus sign is now the default job.

### Restarting Stopped Jobs

You can restart any stopped job as either a background process or a foreground process. A foreground process takes over control of the terminal you’re working on, so be careful about using that feature.

To restart a job in background mode, use the [bg](#9781284254884_Glossary.xhtml_GLOS-29) command, along with the job number:

![An output restarts a job in background mode using the b g command.](images/9781284255805_CH09_CUM21.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-14)

![An output restarts a job in background mode using the b g command.](images/9781284255805_CH09_CUM22.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-15)

Because the job was restarted in background mode, the command-line interface prompt appears, allowing other commands to be entered. The output from the jobs command now shows that the job is indeed running (as you can tell from the output now appearing on the monitor).

To restart a job in foreground mode, use the [fg](#9781284254884_Glossary.xhtml_GLOS-98) command, along with the job number:

![An output restarts a job in foreground mode using the f g command.](images/9781284255805_CH09_CUM23.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-16)

Since the job is running in foreground mode, the command-line interface prompt does not appear until the job finishes.

## Scheduling Jobs

There will be situations in which you will want to run a program or script at a preset time, usually at a time when you’re not there. The Linux system provides a couple of ways to run a script at a preselected time: the at command and the cron table. Each method uses a different technique for scheduling when and how often to run scripts. The following sections describe each of these methods.

### Scheduling a Job Using the at Command

The [at](#9781284254884_Glossary.xhtml_GLOS-23) command allows you to specify a time when the Linux system will run a script. The at command submits a job to a queue with directions on when the shell should run the job. The at daemon, atd, runs in the background and checks the job queue for jobs to run. Most Linux distributions start this daemon automatically at boot time.

The atd daemon checks a special directory on the system (usually /var/spool/at) for jobs submitted using the at command. By default, the atd daemon checks this directory every 60 seconds. When a job is present, the atd daemon checks the time the job is set to be run. If the time matches the current time, the atd daemon runs the job.

The following sections describe how to use the at command to submit jobs to run and how to manage jobs.

#### The at Command Format

The basic at command format is pretty simple:

![at space open bracket hyphen f space filename close bracket space time.](images/9781284255805_CH09_CUM24.jpg)

By default, the at command submits input from the terminal to the queue. You can specify a file name used to read commands from using the -f parameter.

The time parameter specifies when you want the Linux system to run the job. You can get pretty creative with how you specify the time. The at command recognizes lots of different time formats:

*   A standard hour and minute, such as 10:15

*   An ~AM/~PM indicator, such as 10:15~PM

*   A specific named time, such as now, noon, midnight, or teatime (4~PM)

If you specify a time that has already past, the at command runs the job at that time on the next day.

In addition to specifying the time to run the job, you can also include a specific date, using a few different date formats:

*   A standard date format, such as MMDDYY, MM/DD/YY, or DD.MM.YY

*   A text date, such as Jul 4 or Dec 25, with or without the year

*   You can also specify a time increment:

    *   Now + 25 minutes

    *   10:15~PM tomorrow

    *   10:15 + 7 days

When you use the at command, the job is submitted into a job queue. The job queue holds the jobs submitted by the at command for processing. There are 26 different job queues available for different priority levels. Job queues are referenced using lowercase letters, a through z.

The higher alphabetically the job queue, the lower the priority (higher nice value) the job will run under. By default, at jobs are submitted to the a job queue. If you want to run a job at a higher priority, you can specify a different queue letter using the -q parameter.

#### Retrieving Job Output

When the job runs on the Linux system, there’s no monitor associated with the job. Instead, the Linux system uses the email address of the user who submitted the job for any output messages. Any output destined to the terminal is mailed to the user via the mail system.

Here’s a simple example of using the at command to schedule a job to run:

![An example of using the at command to schedule a job to run is shown.](images/9781284255805_CH09_CUM25.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-17)

![An example of using the at command to schedule a job to run is shown.](images/9781284255805_CH09_CUM26.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-18)

The at command produces a warning message, indicating what shell the system uses to run the script, /bin/sh, along with the job number assigned to the job and the time the job is scheduled to run.

When the job completes, nothing appears on the monitor, but the system generates an email message. The email message shows the output generated by the script. If the script doesn’t produce any output, it won’t generate an email message, by default. You can change that by using the -m option in the at command. This generates an email message, indicating the job completed, even if the script doesn’t generate any output.

#### Listing Pending Jobs

The [atq](#9781284254884_Glossary.xhtml_GLOS-24) command allows you to view what jobs are pending on the system:

![An output shows the jobs pending on the system using the a t q command.](images/9781284255805_CH09_CUM27.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-19)

![An output shows the jobs pending on the system using the a t q command.](images/9781284255805_CH09_CUM28.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-20)

The job listing shows the job number, the date and time the system will run the job, and the job queue the job is stored in.

#### Removing Jobs

Once you know the information about what jobs are pending in the job queues, you can use the [atrm](#9781284254884_Glossary.xhtml_GLOS-25) command to remove a pending job:

![An output shows removal of a pending job using the a t r m command.](images/9781284255805_CH09_CUM29.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-21)

Just specify the job number you want to remove. You can only remove jobs that you submit for execution. You can’t remove jobs submitted by others.

### Scheduling Recurring Programs

Using the at command to schedule a program or script to run at a preset time is great, but what if you need it to run at the same time every day, or once a week, or once a month? Instead of having to continually submit at jobs, you can use another feature of the Linux system.

The Linux system uses the [cron](#9781284254884_Glossary.xhtml_GLOS-60) program to allow you to schedule jobs that need to run on a regular basis. The cron program runs in the background and checks special tables, called cron tables, for jobs that are scheduled to run.

#### The cron Table

Each individual user account has a separate cron table for scheduling programs. The user cron table uses a special format for allowing you to specify when a job should be run. The format for the cron table is:

![min space hour space day of month space month space day of week space command.](images/9781284255805_CH09_CUM30.jpg)

The cron table allows you to specify entries as specific values, ranges of values (such as 1–5) or as a wildcard character (the asterisk). For example, if you want to run a command at 10:15 on every day, you would use the cron table entry of:

![15 space 10 space asterisk space asterisk space asterisk space command.](images/9781284255805_CH09_CUM31.jpg)

The wildcard character used in the dayofmonth, month, and dayofweek fields indicates that cron will execute the command every day of every month at 10:15\. To specify a command to run at 4:15 PM every Monday, you would use the following:

![15 space 16 space asterisk space asterisk space 1 space command.](images/9781284255805_CH09_CUM32.jpg)

You can specify the dayofweek entry as either a three-character text value (mon, tue, wed, thu, fri, sat, sun) or as a numeric value, with 0 being Sunday and 6 being Saturday.

Here’s another example: to execute a command at 12 noon on the first day of every month, you would use the following format:

![0 0 space 12 space 1 space asterisk space asterisk space command.](images/9781284255805_CH09_CUM33.jpg)

The dayofmonth entry specifies a date value (1–31) for the month.

The command list must specify the full pathname of the command to run. You can add any command line parameters or redirection symbols you like, as a regular command line:

![15 space 10 space asterisk space asterisk space asterisk space slash home slash sys admin slash test 4 dot s h space greater than space test 4 out.](images/9781284255805_CH09_CUM34.jpg)

The cron program runs the script using the user account that submitted the job. Thus, you must have the proper permissions to access the command and output files specified in the command listing.

#### Building the cron Table

Each system user can have their own cron table (including the root user) for running scheduled jobs. Linux provides the crontab command for handling the cron table. To list an existing cron table, use the -l parameter:

![Line 1: dollar space crontab space hyphen l. Line 2: no crontab for rich. Line 3: dollar.](images/9781284255805_CH09_CUM35.jpg)

By default, each user’s cron table file doesn’t exist. To add entries to your cron table, use the -e parameter. When you do that, the crontab command starts a text editor with the existing cron table (or an empty file if it doesn’t yet exist).

#### cron Directories

When you create a script that has less precise execution time needs, it is easier to use one of the preconfigured cron script directories. There are four basic directories: hourly, daily, monthly, and weekly.

![A script shows the usage of preconfigured cron script directories.](images/9781284255805_CH09_CUM36.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd9-22)

Thus, if you have a script that needs to be run one time per day, just copy the script to the daily directory and cron executes it each day.

## Resources

Linux Documentation Project, “Chapter 4: Processes,” Accessed on January 4, 2022, from https://tldp.org/LDP/tlk/kernel/processes.xhtml.

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 10
Advanced Administration

MANAGING A LINUX SERVER in a multi-user environment can be somewhat different from a personal graphical desktop. There are lots of new things you need to worry about, such as protecting user files, creating shared folder areas, and providing network services such as email and remote login. This chapter discusses some of the advanced administration tools required to manage a Linux server in a multi-user environment.

The chapter starts out by walking through user account management. With multiple users, you’ll need to ensure each user has his or her own user account and can be assured that their files are safe from other users. This chapter also describes how to manage file permissions for shared folder environments in such a way that multiple users can share the same files.

Next, the chapter discusses some of the odds-and-ends of managing a multi-user Linux server and multiple servers. First, methods for managing the date and time on the server, and ensuring multiple servers in an environment are all synchronized with the proper date and time. Following that, the chapter provides information on how to devise a printer strategy in your Linux environment. Printing from the command line is a little different from the graphical desktop world, so you’ll need to be aware of the commands available.

After discussing printers, the chapter walks through how Linux handles email. There are a few different email server packages available in the Linux world, and knowing how each one works will help with your decision on which one to use.

The chapter finishes up with sections on remote connecting to Linux servers using a secure shell and how to manage the system log files generated on the Linux system. Both of these topics are crucial to running a Linux server in a multi-user environment.

## User Management

The Linux operating system was designed to be a [multi-user operating system](#9781284254884_Glossary.xhtml_GLOS-213). That means it can support multiple users logged into the system at the same time, all doing different things. The problem with having multiple users though is that you need to keep track of who’s doing what and who’s allowed to do what!

This is where [user accounts](#9781284254884_Glossary.xhtml_GLOS-350) come into play. Linux uses user accounts to uniquely identify individual users and control their access to the devices, files, and folders on the system. Linux also uses the user accounts as identifiers when logging activity on the system. That way you can track just who deleted that important file! As the system administrator, you can control what all of the Linux users are allowed to do and then monitor what they’re doing from the system log files.

This section discussed the types of user account used in Linux, how to use them, and how to manage them.

### Examining User Accounts

There are three types of user accounts available on Linux systems:

*   Normal user accounts

*   Service accounts (sometimes called pseudo users)

*   Administration user accounts

[Normal user accounts](#9781284254884_Glossary.xhtml_GLOS-229) are assigned to each person who uses the Linux system. By default, normal user accounts don’t have any special privileges on the Linux system. Normal users only have access to run applications and access files and folders contained in their own home folder. Typically, one user account won’t have access to files and folders owned by another user account (although as you’ll see in a bit, you can change to enable groups of users to share files and folders).

[Service accounts](#9781284254884_Glossary.xhtml_GLOS-304) are used by applications that must run continually in the background, such as email servers, database servers, and web servers. This type of account is often referred to as a pseudo user account because these applications must run continually, require access to files and folders on the system, and it’s not possible to have a normal user account logged in to run the programs.

For security reasons, service accounts can’t log into an interactive desktop or command-line prompt, they can only run in background on the system. It’s common to assign a unique system account to each application, and that account would only have access to the files and folders required for that specific application. In this way the application is isolated so that if one application is compromised by an attacker (such as if someone breaks into the web server application), the attacker can’t get to other parts of the Linux system, only the files related to that application.

[Administration user accounts](#9781284254884_Glossary.xhtml_GLOS-14) are used by system administrators who need complete control of the system. These accounts have access to all files and folders on the Linux system and can modify permissions on any file and folder. In Linux, the main administration user account is assigned the special name [root](#9781284254884_Glossary.xhtml_GLOS-291).

Since the root user account has full permissions to all files, folders, and devices on the Linux system, you must use the root user account when performing most system-related work, such as adding new devices, partitioning new filesystems, or creating new user accounts.

Because of the complete power that the root user account possesses, logging in as the root user account is a very dangerous thing. A small typo in the wrong place in a command can result in a completely unusable Linux system! Usually, Linux system administrators only log in as the root user account when absolutely necessary. They will use a normal user account to do their normal activities such as checking email and browsing the web.

### Accessing Administrator Privileges

Because of the importance of the administration user account, there are three ways for a Linux system administrator to become the root user account:

*   Log in as the root user account directly from a login prompt

*   Use the [su](#9781284254884_Glossary.xhtml_GLOS-320) command as a normal user account

*   Use the [sudo](#9781284254884_Glossary.xhtml_GLOS-321) command as a normal user account

In the previous section you learned about the dangers of logging in directly as the root user account. It’s generally not a good idea to log in directly as the root user account unless you absolutely must. In fact, some Linux distributions even prevent you from logging in directly as the root user account.

The su Linux command is a great alternative. It allows us to change the user account that we’re logged in as to any other user account on the system, including the root user account. To switch to another user account, you specify that user name on the su command line. For example, if I’m currently logged in with my user account rich and want to switch to the user account barbara, you’d enter the command:

![Line 1: dollar space s u space hyphen space barbara. Line 2: password colon. Line 3: dollar.](images/9781284255805_CH10_CUM01.jpg)

The su command prompts you for the password for the user account you’re trying to switch to. The dash in the command tells Bash to emulate an actual login, running any login shell scripts created for the user account, including changing the home directory. If you don’t use the dash, you’ll be logged in as the user account but still be accessing your own user account’s shell environment.

When you type the su command by itself, Linux will assume you want to switch to be the root user account. When you enter the su command, the Linux system will prompt you for the root user account’s password, ensuring that you have authorization to act as the root user account.

Knowing the capabilities of the root user account, you may be wondering how you will remember which account you are logged in as. Most Linux systems use the command prompt to indicate your permission level. When you’re logged in as a normal user account, the command prompt is a dollar sign ($); when you use the su command to gain root privileges, the command prompt changes to a pound sign (#), as in this example:

![Line 1: dollar space s u. Line 2: password colon. Line 3: hash space exit. Line 4: dollar.](images/9781284255805_CH10_CUM02.jpg)

After you enter the password for the root user account, the command prompt changes to the pound sign, indicating that you’re now the root user account. While at the pound sign command prompt, any command you enter has root privileges. When you’ve completed your administrator tasks, just use the exit command to exit the root user account and switch back to your normal user account (and the dollar sign prompt).

The sudo command gives you yet another alternative to logging in as the root user account. Instead of gaining access to the root user account directly to enter multiple commands, the sudo command allows you to run individual commands as the root user account, essentially granting you temporary user of the accounts privileges. Just enter the command you need to run as the parameter of the sudo command:

![An output shows the usage of the sudo command with cat as the parameter.](images/9781284255805_CH10_CUM03.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-1)

Notice that the command prompt didn’t change at all. The example began as a normal user account, submitted the sudo command with a system command, then when that command completed, it reverted back to the normal user account dollar sign prompt.

Also notice that the sudo command prompted me for my password, not the password of the root user account. This is not a mistake; it’s a security feature. Only specific user accounts are allowed to use the sudo command. You must validate who you are to be able to use the command. The system will maintain your authentication for a period of time, so any subsequent use of the sudo command within that timespan (which you can configure) won’t require the password.

The /etc/sudoers file lists the user accounts that have privileges to run the sudo command, along with restricting just what commands they can run with root privileges. You must use the visudo program (a special version of the vi editor program) to edit the /etc/sudoers file.

### Working with Groups

Often in a multi-user environment you’ll run into a situation where you want multiple user accounts to have access to the same files and folders (such as a sales team working on the same project). In a Linux environment, file permissions set to individual user accounts won’t work when trying to share files.

To solve that problem, Linux supports groups. A [group](#9781284254884_Glossary.xhtml_GLOS-124) is a collection of user accounts that are treated as a single account for permissions. You can assign file and folder permissions to a group, granting all of the user accounts in that group access to the shared files and folders.

Linux stores information about the group accounts in the /etc/groups file. Each group is defined on a separate line in the file, which includes the group name, a unique group ID value, and the list of user accounts that are members of the group. To add a new group, use the groupadd command.

By default, when you create a new user account in Linux, the system assigns that user to a default user group. Most Linux distributions create separate user groups for each user account, that way you can’t unintentionally create shared files or folders

### Managing User Accounts

You’ll use five basic commands to manage user accounts in Linux:

*   [useradd](#9781284254884_Glossary.xhtml_GLOS-351)—Create a new user account

*   [userdel](#9781284254884_Glossary.xhtml_GLOS-352)—Delete an existing user account

*   [usermod](#9781284254884_Glossary.xhtml_GLOS-353)—Modify the settings of an existing user account

*   [passwd](#9781284254884_Glossary.xhtml_GLOS-247)—Change the password of an existing user account

*   [chage](#9781284254884_Glossary.xhtml_GLOS-37)—Change the password aging properties of an existing user account

The useradd command has lots of parameters that you can use to customize just how Linux creates the new user account. These are shown in [TABLE 10-1](#9781284254884_CH10_01.xhtml_c10-tab001).

TABLE 10-1 The useradd command parameters.

| Parameter | Description |
| --- | --- |
| -c comment | The user account comment field value |
| -d home | The location of the user’s Home folder (the default is /home/username) |
| -e date | The date the account will expire automatically |
| -g group | The default group for the user account |
| -m | Create a Home folder and copy the contents of the /etc/skel folder into it |
| -s shell | The shell for the user account |
| -u UID | Use a specific UID value instead of allowing Linux to assign one |

For example, to create a new user account named test1, and give it a home folder for the account, use this command:

![Line 1: dollar space sudo space user add space hyphen m space test 1\. Line 2: open bracket sudo close bracket space password for rich colon. Line 3: dollar.](images/9781284255805_CH10_CUM04.jpg)

After you create the user account, use the passwd command to assign a default password for the account:

![A default password is assigned for the account using the pass w d command.](images/9781284255805_CH10_CUM05.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-2)

Now you can log into either the command line or the desktop environment using the test1 user account and password you just created!

You can use the usermod command to change any of these settings for an existing user account. For example, to change the comment field for the user account, just use:

![Line 1: dollar sudo space user mod space hyphen c space double quote Ima space Test double quote space test 1\. Line 2: open bracket sudo close bracket space password for rich colon. Line 3: dollar.](images/9781284255805_CH10_CUM06.jpg)

When you want to remove a user account, just use the userdel command:

![Line 1: dollar space sudo space user del space test 1\. Line 2: open bracket sudo close bracket space password for rich colon. Line 3: dollar.](images/9781284255805_CH10_CUM07.jpg)

## Linux File and Directory Permissions

The core security feature of Linux is file and directory permissions. Linux accomplishes that by assigning each file and directory an owner and allowing that owner to set the basic security settings to control access to the file or directory. The following sections walk through how Linux handles ownership of files and directories as well as the basic permissions settings that you can assign to any file or directory on your Linux system.

### Understanding Ownership

Linux uses a three-tiered approach to protecting files and directories:

*   Owner—Within the Linux system, each file and directory is assigned to a single owner. The Linux system administrator can assign the owner specific privileges to the file or directory.

*   Group—The Linux system also assigns each file and directory to a single group of users. The administrator can then assign that group privileges that are specific to the file or directory and that differ from the owner privileges.

*   Others—This category of permissions is assigned to any user account that is not the owner nor in the assigned user group.

You can view the assigned owner and group for a file or directory by adding the -l option to the ls command, as shown in [LISTING 10-1](#9781284254884_CH10_02.xhtml_c10-list001).

The first column, -rw-rw-r--, defines the access permissions assigned to the owner, group, and others. That will be discussed later in the chapter in the section “Controlling Access Permissions.” The third column, the rich or barbara value, shows the user account assigned as the owner of the file. The fourth column, sales, shows the group assigned to the file.

When a user creates a file or directory, by default the Linux system automatically assigns that user as the owner and uses the primary group the user belongs to as the group for the file or directory. You can change the default owner and group assigned to files and directories using Linux commands. The following sections show how to do that.

### Changing File or Directory Ownership

The root user account can change the owner assigned to a file or directory by using the chown command. The chown command format looks like this:

![chown space open bracket options close bracket space new owner space filenames.](images/9781284255805_CH10_CUM09.jpg)

The newowner parameter is the user name of the new owner to assign to the file or directory, and filenames is the name of the file or directory to change. You can specify more than one file or directory by placing a space between each file or directory name:

![An output displays file ownership using the l s command with hyphen l option, and sudo and chown commands.](images/9781284255805_CH10_CUM10.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-4)

There are a few command-line options available for the chown command, but they are mostly obscure and not used much. One that may be helpful for you is the -R option, which recursively changes the owner of all files and directories under the specified directory.

### Changing the File or Directory Group

The file or directory owner, or the root user account, can change the group assigned to the file or directory by using the chgrp command. The chgrp command uses this format:

![c h g r p space open bracket options close bracket space new group space filenames.](images/9781284255805_CH10_CUM11.jpg)

The newgroup parameter is the name of the new user group assigned to the file or directory, and the filenames parameter is the name of the file or directory to change. If you’re the owner of the file, you can only change the group to a group that you belong to. The root user account can change the group to any group on the system:

![An output changes the group assigned to the file or directory by using the c h g r p command.](images/9781284255805_CH10_CUM12.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-5)

The chown command allows you to change both the owner and group assigned to a file or directory at the same time using this format:

![chown space new owner colon new group space filenames.](images/9781284255805_CH10_CUM13.jpg)

This is often preferred over using the separate chgrp command.

### Controlling Access Permissions

After you’ve established the file or directory owner and group, you can assign specific permissions to each. Linux uses three types of permission controls:

*   [Read](#9781284254884_Glossary.xhtml_GLOS-280)—The ability to access the data stored within the file or directory

*   [Write](#9781284254884_Glossary.xhtml_GLOS-365)—The ability to modify the data stored within the file or directory

*   [Execute](#9781284254884_Glossary.xhtml_GLOS-89)—The ability to run the file on the system, or the ability to list the files contained in the directory

You can assign each tier of protection (owner, group, and other) different read, write, and execute permissions. This creates a set of nine different permissions that are assigned to each file and directory on the Linux system. The nine permissions appear in the ls output as the first column of information when you use the -l option as shown in [LISTING 10-1](#9781284254884_CH10_02.xhtml_c10-list001). [FIGURE 10-1](#9781284254884_CH10_02.xhtml_c10-fig001) shows the order in which the permissions are displayed in the ls output.

![A chart shows the order in which the file and directory permissions are displayed in the l s output.](images/9781284255805_CH10_FIGF01.jpg)

FIGURE 10-1 File and directory permissions as displayed in the ls output.

[Description](9781284254884_Alt.xhtml_summary-fig10-1)

In [Figure 10-1](#9781284254884_CH10_02.xhtml_c10-fig001), the first character denotes the object type. A dash indicates a file, while a d indicates a directory.

The next three characters denote the [owner permissions](#9781284254884_Glossary.xhtml_GLOS-240) in the order of read, write, and execute. A dash indicates the permission is not set, while the r, w, or x indicate the read, write, or execute permission is set. In the example in [LISTING 10-1](#9781284254884_CH10_02.xhtml_c10-list001), all three files use rw- for the owner permissions, which means the owner has permission to read and write to the file but cannot execute, or run, the file. This is common with data files.

The second set of three characters denotes the [group permissions](#9781284254884_Glossary.xhtml_GLOS-125) for the file or directory. Again, this uses the read, write, and execute order, with a dash indicating the permission is not set. After making the change to the customers.txt file for the marketing group, the sales group can only write to the research.txt and salesdata.txt files, and the marketing group can only write to the customers.txt file.

Finally, the third set of three characters denotes the permissions assigned to user accounts that are not the owner or a member of the group assigned to the file or directory. The same order of read, write, and execute is used. In the [Listing 10-1](#9781284254884_CH10_02.xhtml_c10-list001) examples, other user accounts on the system can read the files but not write or execute them.

Either the root user account or the owner of the file or directory can change the assigned permissions by using the chmod command.

The format of the chmod command can be somewhat confusing. It uses two different modes for denoting the read, write, and execute permission settings for the owner, group, and other. Both modes allow you to define the same sets of permissions, so there’s no reason to use one mode over the other.

In [symbolic mode](#9781284254884_Glossary.xhtml_GLOS-326), you denote permissions by using a letter code for the owner (u), group (g), others (o), or all (a) and another letter code for the read (r), write (w), or execute (x) permission. The two codes are separated with a plus sign (+) if you want to add the permission, a minus sign (-) to remove the permission, or an equal sign (=) to set the permission as the only permission. [LISTING 10-2](#9781284254884_CH10_02.xhtml_c10-list002) shows an example of this.

In [Listing 10-2](#9781284254884_CH10_02.xhtml_c10-list002), the g-w code in the chmod command indicates to remove the write permission for the group from the customers.txt file. Now members of the marketing group can only read the file.

You can combine letter codes for both to make multiple changes in a single chmod command, as shown in [LISTING 10-3](#9781284254884_CH10_02.xhtml_c10-list003).

The ug code assigns the change to both the owner and the group, while the rwx code assigns the read, write, and execute permissions. The equal sign indicates to set those permissions.

The second mode available in chmod is called octal mode. With octal mode, the nine permission bits are represented as three octal numbers, one each for the owner, group, and [other permissions](#9781284254884_Glossary.xhtml_GLOS-238). [TABLE 10-2](#9781284254884_CH10_02.xhtml_c10-tab002) shows how the octal number matches the three symbolic mode permissions.

TABLE 10-2 Octal mode permissions.

| Octal Value | Permission | Meaning |
| --- | --- | --- |
| 0 | --- | No permissions |
| 1 | --x | Execute only |
| 2 | -w- | Write only |
| 3 | -wx | Write and execute |
| 4 | r-- | Read only |
| 5 | r-x | Read and execute |
| 6 | rw- | Read and write |
| 7 | rwx | Read, write, and execute |

You must specify the three octal values in the owner, group, and other in the correct order, as shown in [LISTING 10-4](#9781284254884_CH10_02.xhtml_c10-list004).

The 664 octal mode set the owner and group permissions to read and write (6) but the others permission to read only (4). You can see the results from the ls output. This is a handy way to set all of the permissions for a file or directory in a single command.

### Exploring Special Permissions

Linux uses three special permission bits for controlling the advanced behavior of files and directories.

The Set User ID (SUID) bit is used with executable files. It tells the Linux kernel to run the program with the permissions of the file owner and not the user account actually running the file. This feature is most commonly used in server applications that must run as the root user account to have access to all files on the system, even if the user launching the process is a standard user.

The SUID bit is indicated by an s in place of the execute permission letter for the file owner: rwsr-xr-x. The execute permission is assumed for the system to run the file. If the SUID bit is set on a file that doesn’t have execute permission for the owner, it’s indicated by an uppercase S.

To set the SUID bit for a file, in symbolic mode add s to the owner permissions, or in octal mode include a 4 at the start of the octal mode setting:

![Line 1: hash space c h mod space u plus s space my app. Line 2: hash space c h mod space 4 7 5 0 space my app.](images/9781284255805_CH10_CUM17.jpg)

The Set Group ID (SGID, also called GUID) bit works differently in files and directories. For files, it tells Linux to run the program file with the file’s group permissions. It’s indicated by an s in the group execute position: rwxrwsr--.

For directories, the SGID bit helps us create an environment where multiple users can share files. When a directory has the SGID bit set, any files users create in the directory are assigned the group of the directory and not that of the user. That way all users in that group can have the same permissions as all of the files in the shared directory.

To set the SGID bit, in symbolic mode add s to the group permissions, or in octal mode include a 2 at the start of the octal mode setting:

![Line 1: hash space c h mod space g plus s space slash sales. Line 2: hash space c h mod space 2 6 6 0 space slash sales.](images/9781284255805_CH10_CUM18.jpg)

Finally, the sticky bit is used to protect a file from being deleted by those who don’t own it, even if they belong to the group that has write permissions to the file. The sticky bit is denoted by a t in the execute bit position for others: rwxrw-r-t.

The sticky bit is often used on directories shared by groups. The group members have read and write access to the data files contained in the directory, but only the file owners can remove files from the shared directory.

To set the sticky bit, in symbolic mode add t to the owner permissions, or in octal mode include a 1 at the start of the octal mode setting:

![Line 1: hash space c h mod space o plus t space slash sales. Line 2: hash space c h mod space 1 7 7 7 space slash sales.](images/9781284255805_CH10_CUM19.jpg)

### Managing Default Permissions

When a user creates a new file or directory, the Linux system assigns it a default owner, group, and permissions. The default owner, as expected, is the user who created the file. The default group is the owner’s primary group.

The user mask feature defines the default permissions Linux assigns to the file or directory. The user mask is an octal value that represents the bits to be removed from the octal mode 666 permissions for files or the octal mode 777 permissions for directories.

The user mask value is set with the umask command. You can view your current umask setting by simply entering the command by itself on the command line:

![Line 1: dollar space u mask. Line 2: 0 0 2 2\. Line 3: dollar.](images/9781284255805_CH10_CUM20.jpg)

The output of the umask command shows four octal values. The first octal value represents the mask for the SUID (4), GUID (2), and sticky (1) bits assigned to files and directories you create. The next three octal values mask the owner, group, and other permission settings.

The mask is a bitwise mask applied to the permission bits on the file or directory. Any bit that’s set in the mask is removed from the permissions for the file or directory. If a bit isn’t set, the mask doesn’t change the setting. [TABLE 10-3](#9781284254884_CH10_02.xhtml_c10-tab003) demonstrates how the umask values work in practice when creating files and directories on your Linux system.

TABLE 10-3 Results from common umask values for files and directories.

| Umask | Created Files | Created Directories |
| --- | --- | --- |
| 000 | 666 (rw-rw-rw-) | 777 (rwxrwxrwx) |
| 002 | 664 (rw-rw-r--) | 775 (rwxrwxr-x) |
| 022 | 644 (rw-r--r--) | 755 (rwxr-xr-x) |
| 027 | 640 (rw-r-----) | 750 (rwxr-x---) |
| 077 | 600 (rw-------) | 700 (rwx------) |
| 277 | 400 (r--------) | 500 (r-x------) |

You can test this by creating a new file and directory on your Linux system:

![An output shows the creation of a new file and directory on the Linux system.](images/9781284255805_CH10_CUM21.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-9)

The umask value of 0022 created the default file permissions of rw-r--r-- , or octal 644, on the test2 file, and rwx-r-xr-x, or octal 755, on the test1 directory, as expected (note that the directory entry starts with a d in the permissions list).

You can change the default umask setting for your current shell session by using the umask command from the command line:

![An output changes the default u mask setting for the current shell session.](images/9781284255805_CH10_CUM22.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-10)

The default permissions for the new file have changed to match the umask setting.

## Advanced Access Control Lists

The basic Linux method of permissions has one drawback in that it’s somewhat limited. You can only assign permissions for a file or directory to a single group or user account. In a complex business environment with different groups of people needing different permissions to files and directories, that doesn’t work.

Linux developers have devised a more advanced method of file and directory security called an access control list (ACL). The ACL allows you to specify a list of multiple users or groups and the permissions that are assigned to them. Just like the basic security method, ACL permissions use the same read, write, and execute permission bits, but now they can be assigned to multiple users and groups.

To use the ACL feature in Linux, you use the setfacl and getfacl commands. The getfacl command allows you to view the ACLs assigned to a file or directory, as shown in [LISTING 10-5](#9781284254884_CH10_03.xhtml_c10-list005).

If you’ve only assigned basic security permissions to the file, those still appear in the getfacl output, as shown in [Listing 10-5](#9781284254884_CH10_03.xhtml_c10-list005).

To assign permissions for additional users or groups, you use the setfacl command:

![set f a c l space open bracket options close bracket space rule space filenames.](images/9781284255805_CH10_CUM24.jpg)

The setfacl command allows you to modify the permissions assigned to a file or directory using the -m option or remove specific permissions using the -x option. You define the rule with three formats:

![Line 1: u open bracket s e r close bracket colon u i d colon perms. Line 2: g open bracket r o u p close bracket colon g i d colon perms. Line 3: o open bracket t h e r close bracket double colon perms.](images/9781284255805_CH10_CUM25.jpg)

To assign permissions for additional user accounts, use the user format; for additional groups, use the group format; and for others, use the other format. For the uid or gid values, you can use either the numerical user identification number or group identification number or the names. Here’s an example:

![An output shows the usage of the set f a c l command.](images/9781284255805_CH10_CUM26.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-12)

This example adds read and write permissions for the sales group to the test file. Notice that there’s no output from the setfacl command. When you list the file, only the standard owner, group, and other permissions are shown, but a plus sign (+) is added to the permissions list. This indicates that the file has additional ACLs applied to it. To view the additional ACLs, use the getfacl command again:

![An output shows the additional A C Ls using the get f a c l command.](images/9781284255805_CH10_CUM27.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-13)

The getfacl output now shows that there are permissions assigned to two groups. The default file group (rich) is assigned read permissions, but now the sales group has read and write permissions to the file. To remove the permissions, use the -x option:

![An output shows the removal of permissions using the set f a c l command with hyphen x option.](images/9781284255805_CH10_CUM28.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-14)

Linux also allows you to set a default ACL on a directory that is automatically inherited by any file created in the directory. This feature is called inheritance.

To create a default ACL on a directory, start the rule with a d: followed by the normal rule definition. That looks like this:

![Dollar space sudo space set f a c l space hyphen m space d colon g colon sales colon r w space slash shared slash sales.](images/9781284255805_CH10_CUM29.jpg)

This example assigns the read and write permissions to the sales group for the /shared/sales directory. Now all files created in that folder will automatically be assigned read and write permissions for the sales group.

## Managing the Date and Time

In our global society, it’s common to have systems located around the world that need to interact with one another. It’s important that files and folders created and accessed on these systems use proper date and time stamps to indicate file times. There are two commands that you can use to view the current system date and time:

*   date

*   time

The [date](#9781284254884_Glossary.xhtml_GLOS-62) command also allows you to customize the output using format operators. There are lots of customized formats available for the date command. Use the main date command to view the different formats available for the date command. For example, to view the year, month, and date as YYYYMMDD, use the format:

![Line 1: dollar space date space plus percentage Y percentage m percentage d. Line 2: 2022 0 1 1 5\. Line 3: dollar.](images/9781284255805_CH10_CUM30.jpg)

There are two ways to set the date and time on Linux systems:

*   Manual settings

*   Automatic settings

This section shows how to use each of these methods to change the time and date on your Linux system.

### Setting the Date and Time Manually

The date command not only allows you to view the current system date and time, it also allows administrators to set them. You set the date and time by specifying it in the date command line using the following format:

![date space Y Y Y Y M M D D h h m m s s.](images/9781284255805_CH10_CUM31.jpg)

If you just need to set the date, you can omit the time values. However, if you need to set the time, you must also specify the date. Only the root user account (or an account that has sudo access) can change the date and time on the system.

### Synching the Time Automatically

Trying to manually set the time for dozens or hundreds of Linux systems can be quite a challenge. To avoid this scenario, you can use the [Network Time Protocol (NTP)](#9781284254884_Glossary.xhtml_GLOS-221). NTP allows you to point all Linux systems on the network to a single time source and always synchronize the system date and time with the time source.

There are several NTP programs available in Linux, but currently the two most popular are the ntpd and the system-timesyncd programs.

The ntpd program runs in the background, communicating with a remote time source and continually synchronizing the system date and time to the time source. You set one or more remote time sources in the /etc/ntp.conf configuration file. Just specify each time source on a separate line in the configuration file:

![server space host name.](images/9781284255805_CH10_CUM32.jpg)

The systemd-timesyncd program is part of the Systemd family of utilities. You can check if that’s running on your Linux system by using the systemctl command, as shown in [LISTING 10-6](#9781284254884_CH10_04.xhtml_c10-list006):

The output in [Listing 10-6](#9781284254884_CH10_04.xhtml_c10-list006) shows that the system is using the systemd-timesyncd program to synchronize time. You define NTP servers in the /etc/systemd/timesyncd.conf configuration file.

Many networks utilize a local time source to which all systems are synchronized. However, there are also public time sources on the Internet that you can use if you wish. For example, the special address pool.ntp.org provides a cluster of time source servers that are available 24/7.

### Setting the Time Zone

Along with the date and time, another important time feature for Linux systems is the time zone. Most Linux distributions use the /etc/localtime file to define the time zone for the server; however, some older Linux distributions use the /etc/timezone file.

The localtime and timezone files themselves are somewhat cryptic, but fortunately for us, we don’t need to mess directly with them. Instead, Linux distributions store time zone template files (one for each time zone in the world) in the /usr/share/zoneinfo folder. The time zone files are divided into folders representing geographical locations, making it easier to find the time zone file for your area. All you need to do is use the ln command to link the appropriate time zone template file for your area to the actual time zone file location for your system:

![l n space hyphen s space slash u s r slash share slash zone info slash U S slash Eastern space slash e t c slash local time.](images/9781284255805_CH10_CUM34.jpg)

This sets the system time zone to the Eastern time zone in the United States.

## Printer Administration

For years, printing had been the bane of Linux systems. In the Windows world, printer manufacturers just create customized printer drivers for each printer model they produce, making connecting to just about any printer a breeze, but it’s not that easy in the Linux world.

Linux uses two different systems for managing printers:

*   Berkeley Software Distribution (BSD) Line Printer Daemon (LPD)

*   Common Unix Print System (CUPS)

The [Line Printer Daemon (LPD)](#9781284254884_Glossary.xhtml_GLOS-174) print method is the older of the two, as it had its origins in the BSD Unix world. With LPD, each printer is defined in a /etc/printcap configuration file, specifying the connection port, rules for how the printer handles text and special characters, and rules that define the print queue (usually stored in the /var/spool/lpd directory structure). The LPD printing system is somewhat complicated and is anything but plug and play.

Because of this complexity, Unix developers created the [Common Unix Printing System (CUPS)](#9781284254884_Glossary.xhtml_GLOS-51). CUPS is a simplified way of handling printers for Unix (and Linux) systems. It includes a webbased interface to define printers and manage print jobs. Because of its ease, it has become the de facto printing method for all Linux distributions. This section focuses on the details on how to implement CUPS in your Linux system.

### Configuring CUPS

The CUPS setup consists of a program that runs in background mode (called cupsd) and two configuration files that define the system parameters and printers. These printers are normally defined using the CUPS web interface, so you never even need to touch the configuration files, but it’s important to understand how they are used.

The /etc/cups/cupsd.conf file defines the system parameters that control the overall operations of the CUPS server. Individual printers are defined in the /etc/cups/printers.conf configuration file. CUPS also utilizes the Internet Printing Protocol (IPP), which allows network printers to advertise on the network, so CUPS servers can automatically detect them.

To set up a new printer using the CUPS web interface, open a browser and navigate to the URL: [http://localhost:631](http://localhost:631). The main CUPS web interface is shown in [FIGURE 10-2](#9781284254884_CH10_05.xhtml_c10-fig002).

![A screenshot shows the CUPS main web interface.](images/9781284255805_CH10_FIGF02.jpg)

FIGURE 10-2 The CUPS main web interface.Screen shot reprinted with permission from Apple Inc. © 2009 Apple Inc. All rights reserved.

Screen shot reprinted with permission from Apple Inc. © 2009 Apple Inc. All rights reserved.

[Description](9781284254884_Alt.xhtml_summary-fig10-2)

The CUPS web interface listens for both clients as well as other CUPS servers on TCP Port 631, the basic CUPS web interface.

Click the Administration tab to define a new printer. You’ll first be prompted to enter an administrator user account and password, then you can go through a simple wizard to select the printer to add. Once you add a printer using CUPS, that printer will be available in all of the graphical desktop applications running on the system. If you need to use the printer from the command-line prompt, there are programs to help with that.

### Using LPD Commands

To support command-line print methods, CUPS also contains programs that emulate the standard programs used in the LPD system. [TABLE 10-4](#9781284254884_CH10_05.xhtml_c10-tab004) shows the available print commands.

TABLE 10-4 CUPS command-line commands.

| COMMAND | DESCRIPTION |
| --- | --- |
| lpc | Start, stop, or reorder a print job. |
| lpr | Send a jobs to the print queue. |
| lprm | Remove a jobs from the print queue. |
| lpq | Display the print queue. |

Each command uses the –P parameter to specify the printer used:

![Line 1: dollar space l p q space hyphen P h p 6 4 0 0\. Line 2: h p 6 4 0 0 is ready. Line 3: no entries. Line 4: dollar.](images/9781284255805_CH10_CUM35.jpg)

While CUPS helps make installing and managing printers easy, there’s still one more problem: How to send data to the printer that it can understand and print. That’s where the Linux PPD files come into play.

### Using Linux Printer Drivers

The original Unix solution for handling printing was to devise a standard printer protocol that was used to format text and graphics sent to a printer. The Postscript protocol is the result of that work. The [Postscript protocol](#9781284254884_Glossary.xhtml_GLOS-260) defines a formatting language that controls how the printer displays the text and graphics.

Unfortunately, though, not many lower cost consumer printers support the Postscript protocol, as it is somewhat complicated to implement. That set Linux users back to relying on individual printer manufacturers to create Linux drivers for their specific printers.

That problem has been solved with the development of the [Ghostscript](#9781284254884_Glossary.xhtml_GLOS-114) program. Ghostscript converts Postscript data into the commands recognized by specific printers. It uses a [Postscript Printer Definition (PPD)](#9781284254884_Glossary.xhtml_GLOS-259) file to define the rules that filter the Postscript commands and convert them into commands recognized by the printer. Each printer just needs a single PPD file for the Ghostscript program to convert the Postscript data for printing on the printer.

This has opened the door for both printer manufacturers and Linux user groups to generate PPD files for a myriad of common printers. The CUPS package itself includes PPD files for thousands of different printers, plus there are entire websites devoted to Linux users sharing their own custom PPD files. Now, the Linux world finally has a reasonable printing solution.

## Email Administration

In this day of instantaneous communication, email servers have become a necessity not only in the business world, but also for personal computer systems. Most Linux systems install some type of mail system by default, either a desktop client program that allows users to connect to a remote email server or an internal email server for handling email onsite.

This section describes how Linux handles email and the different options available to you for working with email in a Linux environment.

### Describing Linux Email Architecture

In the early days of email, it was standard to create a single monolithic program that handled all aspects of email:

*   Sending messages to users on remote systems

*   Receiving messages from remote systems

*   Allowing clients to read their messages

*   Allowing clients to send messages

The idea behind the Unix operating system was to modularize as many functions as possible, and email was no different. Unix developers devised a modular approach to handling email functions. Instead of having a single monolithic email program, Unix systems split the email functions into three subsystems:

*   [Mail Transport Agent (MTA)](#9781284254884_Glossary.xhtml_GLOS-193)—Send messages to remote servers and receive messages from remote servers.

*   [Mail Delivery Agent (MDA)](#9781284254884_Glossary.xhtml_GLOS-191)—Receive incoming mail messages from an MTA and ensure they go to the correct local user mailbox.

*   [Mail User Agent (MUA)](#9781284254884_Glossary.xhtml_GLOS-194)—Provide an interface for users to read their messages and send new messages.

By modularizing each function, Unix developers could create more advanced programs that specialized in each feature of the mail process. [FIGURE 10-3](#9781284254884_CH10_06.xhtml_c10-fig003) demonstrates how these modules fit together to receive and deliver a message between users on separate systems.

![A chart shows the Linux modular email programs.](images/9781284255805_CH10_FIGF03.jpg)

FIGURE 10-3 The Linux modular email programs.

[Description](9781284254884_Alt.xhtml_summary-fig10-3)

Linux developers continued with this process and have developed several new modular programs for implementing email systems. This section walks through the programs now available for both client and server functions.

### Identifying Linux Email Servers

Email servers require both MTA and MDA programs to accept and deliver mail to users on the system. A few different MTA programs are available for the Linux environment, and [TABLE 10-5](#9781284254884_CH10_06.xhtml_c10-tab005) describes the most popular ones.

TABLE 10-5 Popular Linux email server programs.

| Server | Description |
| --- | --- |
| Sendmail | The original Unix email server program, Sendmail is very versatile but extremely complicated to configure. |
| Exim | Created as a monolithic email program, Exim is easy to configure. |
| Postfix | Postfix was created as a set of modular programs to simplify handling incoming and outgoing mail. |
| qMail | qMail is a modular set of programs that focus on guaranteed mail delivery. |

The [Postfix](#9781284254884_Glossary.xhtml_GLOS-257) email server program has become the very popular in Linux environments. Most Linux distributions install it by default. However, many experienced email administrators prefer the robustness and reliability of the qMail package.

Email servers use the Simple Mail Transfer Protocol (SMTP) to send messages to each other. Each email server can both send messages to remote servers as well as accept incoming messages for local email users.

One popular MDA program in the Linux world is [Procmail](#9781284254884_Glossary.xhtml_GLOS-266). The Procmail program allows the mail administrator to customize mail delivery to users. Not only can you send mail to a specific user account, but Procmail allows users to direct mail to specific folders based on filtering commands.

### Using Linux Email Clients

The Linux environment includes a multitude of email client packages. For the graphical desktop environment, the Thunderbird and Evolution packages are the most common. The Thunderbird email client is shown in the [FIGURE 10-4](#9781284254884_CH10_06.xhtml_c10-fig004).

![A screenshot shows the Thunderbird email client.](images/9781284255805_CH10_FIGF04.jpg)

FIGURE 10-4 The Thunderbird email client.Courtesy of Mozilla Foundation.

Courtesy of Mozilla Foundation.

[Description](9781284254884_Alt.xhtml_summary-fig10-4)

Graphical email client packages provide configuration options for both receiving email from your local user account and from remote email servers. This makes them a complete MUA package.

You can also configure both Thunderbird and Evolution to send outbound mail messages to an email servers. The email server accepts email messages from both clients and servers, and if they aren’t addressed to a local user account on the host, forwards them as necessary. It uses SMTP to forward the message to the appropriate destination email server. This feature is referred to as a [Mail Submission Agent (MSA)](#9781284254884_Glossary.xhtml_GLOS-192) and is usually part of the MTA software on an email server.

There are also email client programs available for the Linux command line. The mailx program is the most popular and is often installed by default in Linux distributions. The mailx program allows you to both send email messages as well as check your local user account mailbox using the simple mail command line command:

![An output checks local user account mailbox using the simple mail command line command.](images/9781284255805_CH10_CUM36.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-16)

The question mark prompt allows you to submit commands to read, delete, store, and respond to messages.

You can also send mail using the mail command:

![Line 1: dollar space mail space hyphen s space double quote Test double quote space rich space C c colon. Line 2: This is a test message. Line 3: dollar.](images/9781284255805_CH10_CUM37.jpg)

To end the message text hit the Ctrl+D key combination.

### Redirecting Email

There are two common methods for redirecting mail delivery within the Linux email systems:

*   Forwarding

*   Aliases

[Forwarding](#9781284254884_Glossary.xhtml_GLOS-108) allows each individual user to forward messages to an alternative location. You just create a .forward file in your home folder (since the file name starts with a period, Linux considers it a hidden file) and define the locations where you want all of your mail forwarded to. These locations can be alternative email addresses, files, or even programs.

The email system administrator can also set up [aliases](#9781284254884_Glossary.xhtml_GLOS-15) to redirect email messages. The /etc/aliases file allows you to create a list of aliases using the format:

![alias colon space address 1 comma space address 2 comma space ellipsis.](images/9781284255805_CH10_CUM38.jpg)

The alias name acts like a local user account; the email server will accept incoming mail messages destined to the alias name. However, instead of delivering it to the alias name, it redirects the message to one or more alternative addresses specified.

After defining the aliases in the /etc/aliases file, the administrator must run the newaliases command, which converts the aliases file into a separate binary file used by the MTA software.

## Secure Login

In a multiserver Linux environment, there’s a good chance that you won’t be physically located near any of the Linux servers. To access the servers, you need to utilize some type of remote access software.

In years past, the [Telnet](#9781284254884_Glossary.xhtml_GLOS-335) protocol provided the simplest way to interact with the server using a command prompt across the network. Unfortunately, this protocol sends data as plain, unencrypted text, making it easy for an attacker to snoop on your connection and gain valuable information.

These days, all systems support the Secure Shell (SSH) login for remote access. The SSH login uses encryption keys to encrypt the network session traffic between the client and the server, making it more difficult for attackers to snoop.

The most popular software package for SSH is [OpenSSH](#9781284254884_Glossary.xhtml_GLOS-234), an open source implementation of the SSH protocol.

The OpenSSH package provides both client and server software in the same package, so you only need to install one package to have both. The OpenSSH package contains programs that support:

*   Interactive command prompt sessions

*   Remote file copying

*   Tunneling of any type of data between two servers

[Tunneling](#9781284254884_Glossary.xhtml_GLOS-341) provides an encrypted connection between two servers that any application can use to send data. This creates an easy way to encrypt data from just about any application, even if it doesn’t directly support encrypted connections.

This section walks through the basics of using OpenSSH in a Linux environment to provide secure communication between servers and clients.

### Using OpenSSH

The OpenSSH package consists of four main programs:

*   sshd—The secure server

*   ssh—The secure client

*   [scp](#9781284254884_Glossary.xhtml_GLOS-298)—A secure copy command

*   [sftp](#9781284254884_Glossary.xhtml_GLOS-305)—A fullfeatured secure file transfer program

The OpenSSH sshd server program listens for network connections on TCP port 22, and launches either the interactive shell or a file transfer application depending on the client request. It utilizes the /etc/ssh/sshd_config configuration file that allows you to customize its behavior. There are four main configuration settings that you’ll most likely need to look at:

*   Protocol—Set to either 1 (for version 1) or 2 (for version 2) encryption protocol. Version 1 is not considered secure anymore, so use version 2 whenever possible.

*   PermitRootLogin—When set to yes, it allows the root user account to log in from an interactive SSH connection.

*   AllowTcpForwarding—When set to yes, it allows you to create encrypted tunnel connections between two servers that any application can use to send and receive data.

*   X11Forwarding—When set to yes, it allows you to send the X Window desktop session to a remote server using an encrypted tunnel.

The ssh client program allows you to connect to a remote server using the SSH protocol. It uses the /etc/ssh/ssh_config configuration file to define application settings. For normal use, you shouldn’t have to define any of these settings.

The SSH protocol uses the [asymmetric encryption](#9781284254884_Glossary.xhtml_GLOS-22) (also called public key encryption) method. This method generates two encryption keys:

*   A [public key](#9781284254884_Glossary.xhtml_GLOS-268) that you keep in your home folder on the remote server in the file ~/.ssh/authorized_keys.

*   A [private key](#9781284254884_Glossary.xhtml_GLOS-263) that only you have access to on your local server or workstation, usually stored in the ~/.ssh/id_rsa file.

The SSH session uses your private key to both validate your login against the public key stored on the server and encrypt the data you send in the connection. The following section walks through how to generate the public and private keys used.

### Using SSH Keys

The OpenSSH package includes the ssh-keygen program that can generate both public and private encryption keys. It can be used to create encryption keys to identify both servers and clients.

Servers maintain an encryption key pair so that clients can ensure they’re communicating with the real server and not an imposter created to intercept data. The server maintains the private key, and the client places the server’s public key in their key folder.

While this is often done automatically when installing a server, you can also manually generate the server encryption key pair using the commands:

![Commands used to generate the server encryption key pair are shown.](images/9781284255805_CH10_CUM39.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-17)

These commands generate the three most common types of encryption keys: RSA version 1, RSA version 2, and DSA. The private keys are stored in the /etc/ssh folder as ssh_host_rsa1_key, ssh_host_rsa_key, ssh_host_dsa_key. The public keys use the same filenames, but with the .pub file extension.

### Using SSH for Logins

When you use the ssh program to log into a remote host, there are two modes that you can use:

*   [Password mode](#9781284254884_Glossary.xhtml_GLOS-248) —Enter your normal user account password.

*   [Key mode](#9781284254884_Glossary.xhtml_GLOS-167)—Enter a private key to authenticate your connection.

In password mode, the ssh program prompts you for the user account password:

![A script shows the s s h program prompting for the user account password.](images/9781284255805_CH10_CUM40.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-18)

The first time you connect to a server you’ll be prompted to accept the public key for the server. Subsequent connections to the server compare the stored public key against the server’s private key. If they don’t match, the ssh program will warn you of the change.

After you successfully connect, the prompt results in the command-line prompt for the remote server. It is helpful to customize the PS1 shell prompt to display the hostname in the prompt so that you can keep track of just which system shell prompt you’re working from.

Instead of using your user account password, you can configure SSH to use your private key to log you into the remote system. To do that, you must first generate a public and private keypair:

![A public and private key pair is generated.](images/9781284255805_CH10_CUM41.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-19)

Then you must copy the public key from file ~/.ssh/id_rsa_pub to the authorized_keys file in the ~/.ssh folder for your user account on the remote server. You can either manually do this or use the ssh-copy-id command.

### Encrypting Files

Sometimes you may need a little more security than just encrypting the network connection. If you work with sensitive files, you may want to encrypt the actual file before sending it to a remote location. Unfortunately, the OpenSSH package can only be used for encrypted network sessions and can’t encrypt individual files. Instead, you can use the [GNU Privacy Guard (GPG)](#9781284254884_Glossary.xhtml_GLOS-121) package.

The GPG package provides a way for you to both encrypt a file to protect the data and digitally sign a file to verify that it came from you. It does this all using the gpg program.

The gpg program maintains a keychain that contains the public keys of individuals you exchange files with. To use GPG, you’ll first need to create your own public/private keypair to add to your keychain:

![g p g space gen key.](images/9781284255805_CH10_CUM42.jpg)

To export your public key into a file that you can send to others, use the export parameter:

![g p g space double hyphen export space name space greater than space my key dot pub.](images/9781284255805_CH10_CUM43.jpg)

You must specify a unique name for yourself that identifies your public key in the gpg keychain. You can then email the public key file to anyone who you exchange encrypted files with.

Likewise, you must also import the public keys for others to read the encrypted files they send to you. You do that using the ‐‐import parameter:

![g p g space double hyphen import space their key dot pub.](images/9781284255805_CH10_CUM44.jpg)

If you’d like to list the public keys contained in your keychain, use the ‐‐list‐keys parameter, or use the ‐‐gen‐ revoke parameter to remove individual keys from your keychain.

Once you have the recipient’s key in your keychain you can encrypt a file to send to them using the command:

![g p g space double hyphen out space encrypted file space double hyphen recipient space user space double hyphen encrypt space input file.](images/9781284255805_CH10_CUM45.jpg)

You must specify the user name that matches the public key user name in your keychain. By default, GPG generates a binary encrypted file. If you prefer to email the encrypted file as a text message, add the ‐‐armor parameter.

To decrypt an encrypted file sent to you, use the command:

![g p g space double hyphen out space decrypted file space double hyphen decrypt space input file.](images/9781284255805_CH10_CUM46.jpg)

Besides encrypting files, GPG also allows you to digitally sign a file to validate it came from you. To do that, use the command:

![g p g space double hyphen clear sign space file.](images/9781284255805_CH10_CUM47.jpg)

To validate a file digitally signed by another person, use:

![g p g space double hyphen verify space file.](images/9781284255805_CH10_CUM48.jpg)

By combining both GPG and OpenSSH, you can help increase the security of your files as they are transmitted between hosts.

## Log Files

In a multiuser Linux system, it’s important to keep track of what users as well as background programs are doing. You can accomplish that by utilizing the system log files. Just about all Linux systems store system log files in the /var/log directory structure.

There are two common logging systems used in Linux. For Linux systems that use the SysVinit startup script method, the [syslogd](#9781284254884_Glossary.xhtml_GLOS-328) program (or its cousin rsyslogd) is the most common logging program. For systems that use the Systemd startup script method, the systemd‐journald program is used.

The following sections describe each of these methods in more detail.

### Using syslogd

The syslogd program uses the /etc/syslog.conf configuration file (or /etc/rsyslog.conf for the rsyslogd program) to control what system events are logged and how they get logged. The configuration files define three items: the facility that logs the event (such as mail system or the kernel), the priority of the event (such as a critical issue or just a warning), and the action to take when the event occurs. The format of the log entry is:

![facility dot priority space action.](images/9781284255805_CH10_CUM49.jpg)

[TABLE 10-6](#9781284254884_CH10_08.xhtml_c10-tab006) shows the facility types available.

TABLE 10-6 The syslogd facility types.

| Facility | Description |
| --- | --- |
| authpriv | Use for security and authorization messages. |
| cron | Use for cron daemon messages. |
| daemon | Use for various system daemon messages. |
| kern | Use for kernel messages. |
| lpr | Use for printing system messages. |
| mail | Use for mail system messages. |
| news | Use for news daemon messages. |
| syslog | Use for internally generated syslog messages. |
| user | Use for user-level messages. |
| uucp | Use for Unix-to-Unix copy program (uucp) daemon messages. |
| local0 through local7 | Use for locally defined application messages. |

The priorities are shown in [TABLE 10-7](#9781284254884_CH10_08.xhtml_c10-tab007) from the most import priority to the least important.

TABLE 10-7 The syslogd priority values.

| Priority | Description |
| --- | --- |
| emerg | A panic message, indicating the system is unusable. |
| alert | Indicates an urgent failure/error message concerning primary systems. |
| crit | Indicates an urgent failure/error message concerning secondary systems. |
| err | Indicates a non-urgent failure/error message. |
| warning | This message indicates an error will occur if action is not taken. |
| notice | Identifies an abnormal messages that is not a concern. |
| info | Identifies messages about normal operation. |
| debug | Identifies debugging-level messages for application development. |

For the action parameter, you can specify one or more filenames to log the message to, one or more user accounts, or even a remote host logging system. You can also use the asterisk wildcard character to cover all facilities, priorities, or user accounts for actions.

For example, to send all mailrelated messages to the /var/log/mail log file, use the entry:

![mail dot asterisk space slash var slash log slash mail.](images/9781284255805_CH10_CUM50.jpg)

To send all emergency messages to all users on the system, use:

![Asterisk dot emerg space asterisk.](images/9781284255805_CH10_CUM51.jpg)

Finally, to send all critical priority messages to a remote server, use:

![Asterisk dot crit space at remote host.](images/9781284255805_CH10_CUM52.jpg)

You can also manually log messages to the syslogd system using the logger program:

![Messages are manually logged to the sys log d system using the logger program.](images/9781284255805_CH10_CUM53.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd10-20)

Finally, the logrotate program is used to split (or rotate) log files so that they don’t get too large. You can start a new log file based on file size or date. The /etc/logrotate.conf configuration file sets how each logging type is rotated.

### Using Systemd‐journald

The [systemdjournald](#9781284254884_Glossary.xhtml_GLOS-330) logging system uses the /etc/system/journald.conf configuration file to define how events are logged. The configuration file includes all of the possible settings commented out. To change a setting from its default, just remove the comment character, and change the value to what you require. For most systems the default values work just fine.

Viewing the log files generated by systemdjournald is somewhat tricky. Unfortunately, the journald program logs event messages in a binary log file instead of a text log file. Because of that you can’t just view the log files generated by journald using text tools. Instead, you must use the journalctl program.

The [journalctl](#9781284254884_Glossary.xhtml_GLOS-160) program by itself displays the journald log file entries, starting from the first entry. You can use some command-line parameters to alter its behavior:

*   ‐a—Display all data fields.

*   ‐e—Jump to the end of the file and use the pager program to display it.

*   ‐l—Display only printable data fields.

*   ‐n number—Show the most recent journal data and limit it to a specific number of lines (10 if no number value specified).

*   ‐r—Reverse the output of the journal data so that the newest entries show first.

There are many more features of the journalctl program that you can use to filter just what log messages you view. Refer to the journalctl man page to see all of them.

## Resources

Red Hat Documentation, “Managing Users Vias Command-Line Tools,” Accessed on Jan. 15, 2022, from [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/s2-users-cl-tools.](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/s2-users-cl-tools)

Ubuntu Documentation “CUPS—Print Server,” Accessed on Jan. 15, 2022, from [https://ubuntu.com/server/docs/service-cups](https://ubuntu.com/server/docs/service-cups).

OpenSSH, “OpenSSH,” Accessed on Jan. 15, 2022, from [https://openssh.com](https://openssh.com).

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 11
Linux Security

THESE DAYS IT’S A MUST to know how to run a secure Linux system. Fortunately, several tools are available in the Linux world to help make that job easier. This chapter discusses some of the security features of Linux that you may need to use depending on your specific environment.

The chapter starts out by discussing the importance of keeping track of the administrative account in Linux. The root user account has access to change everything on the Linux system. Controlling who can use that account, how they use it, and logging when they use it is the first step in Linux security. The section discusses some Linux tools and common techniques for controlling and monitoring root access on your system.

Next the chapter discusses implementing advanced security permissions in Linux. While Linux provides basic file protection, it lacks the ability to manage security of processes. There are, however, two common packages utilized to provide context-based security permissions to other Linux objects, such as processes. [SELinux](#9781284254884_Glossary.xhtml_GLOS-301) and [AppArmor](#9781284254884_Glossary.xhtml_GLOS-17) are two popular packages that provide advanced security in the Linux world.

The chapter then moves on to talk about encrypting partitions. Linux has a few different ways to encrypt files stored on the system. The chapter discusses the cryptsetup utility, which allows you to encrypt an entire partition so  you don’t need to encrypt individual files. The chapter then finishes up with  a brief introduction to using firewalls in Linux by exploring the popular firewalld utility.

## Working with Root Access

Linux systems control access to files, directories, and applications by using user accounts. Linux has three types of user accounts:

*   Root—the administrator account with full privileges to all files, directories, and services

*   Standard—normal user accounts

*   Service—application accounts

Because of its power, the [root user](#9781284254884_Glossary.xhtml_GLOS-294) account can be somewhat dangerous to have active on your Linux system. By default, the Ubuntu distribution blocks the ability to log in or change to the root user account to help manage the security environment. However, that’s not the case in Red Hat-based distributions.

If you check in a Red Hat environment, the root user account exists:

![Line 1: dollar space get ent space pass w d space root. Line 2: root colon x colon 0 colon 0 colon root colon slash root colon slash bin slash bash. Line 3: dollar.](images/9781284255805_CH11_CUM01.jpg)

and should have been assigned a password at the time of installation:

![An output shows the existence of root user account.](images/9781284255805_CH11_CUM02.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-1)

Because the root user account is active in the Red Hat system, you should be careful about a few things when using a Red Hat desktop or server. This section walks through a few security practices related to the root user account you should consider when working on a Red Hat system.

### Gaining Super User Privileges

The easiest way to gain super user privileges on a Linux system is to log in as the root user account. However, that can be a dangerous practice because it’s difficult to track just who is logging in as the root user account. To help avoid that issue, many Linux distributions (such as Ubuntu) are configured by default to prevent you from logging in directly as the root user account. Instead, you must use one of two command-line commands to gain super user privileges when logged in as a normal user account:

*   su starts a new command-line shell as another user account. If no user account is specified, it defaults to the root user account.

*   sudo runs a single command with root user privileges.

When you use these commands, the Linux system logs exactly what user account gained super user privileges and when they did it (called nonrepudiation).

The [sudo](#9781284254884_Glossary.xhtml_GLOS-321) command is short for “substitute user do,” though many still refer to its older name, “super user do,” because of its ability to provide super user privilege access. It lets a standard user account run any preauthorized command as another preauthorized user account, including the root user account. The use of the sudo command provides the following benefits and features:

*   When used, sudo prompts users for their own password to validate who they are.

*   Once validated to use sudo, accounts do not have to re-enter their password until after a time period of not using the sudo command.

*   Actions taken with the sudo command are logged.

*   Groups of users can be configured to use sudo instead of listing individual account authorized access.

*   Properly configured, sudo provides a least privilege and nonrepudiation environment contributing to a system’s security.

The /etc/sudoers configuration file defines what users are allowed to run the sudo command along with what they have access to do. The [sudoers](#9781284254884_Glossary.xhtml_GLOS-322) file may contain a list of user accounts, aliases, and/or groups whose users are allowed to escalate privileges. By default, the sudoers file on an Ubuntu system looks like this:

![An output shows an illustration of the sudoers file.](images/9781284255805_CH11_CUM03.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-2)

Linux distributions create a separate user account to designate who can access full super user privileges. Ubuntu uses the group sudo, while Red Hat-based distributions use wheel. Usually the initial account created at installation time is assigned to this group. You can determine if your account is a member of one of those groups through the groups command:

![Line 1: dollar space groups. Line 2: sys admin space a d m space c d rom space sudo space dip space plug dev space l x d. Line 3: dollar.](images/9781284255805_CH11_CUM04.jpg)

If you’d like to modify the sudo configuration, you’ll need to use the visudo command. It’s a special script that prevents multiple admins from making changes at the same time, causing file corruption, and checks for proper syntax.

However, instead of directly adding your configuration in the /etc/sudoers file, it’s a good idea to create your sudo command configuration file(s) in the /etc/sudoers.d/ directory. If you do this, be sure to uncomment the includedir operation located at the bottom of the sudoers file to load your configuration.

There is another nice command that provides privilege escalation. The sudoedit command allows a standard user to open a file in a text editor with privileges of another preauthorized user account, including the root user account. Similar to the sudo command, sudoedit also prompts the user for their own password to validate who they are.

### Determining Your Privilege Elevation Status

On Ubuntu the common method for escalating privileges is to use the sudo command. However, you must either belong to a group listed for accessing higher privileges in the /etc/sudoers file or have a record authorizing the privileges within the file.

To determine your privilege elevation status, you’ll need to determine if your user id is either directly in the /etc/sudoers file or a member of a group that is. First, validate your account name by using the whoami command:

![Line 1: dollar space whoami. Line 2: rich. Line 3: dollar.](images/9781284255805_CH11_CUM05.jpg)

Next, determine the groups to which this account belongs by using the groups command:

![Line 1: dollar space groups. Line 2: rich space a d m space c d rom space sudo space dip space plug dev space l p admin space l x d space samba share. Line 3: dollar.](images/9781284255805_CH11_CUM06.jpg)

Typically, Ubuntu Linux allows those users who belong to the group sudo to access full super user privileges. To check that on your system, display the /etc/sudoers file using the cat command (you’ll need to have root privilege to display it):

![An output displays user privileges of a file using the cat command.](images/9781284255805_CH11_CUM07.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-3)

![An output displays user privileges of a file using the cat command.](images/9781284255805_CH11_CUM08.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-4)

You should see one of the group names your account belongs to in the /etc/sudoers file. In this example, my username is in the sudo group, which is listed in the sudoers file, allowing me to have administrative privileges on the system.

### Keeping Track of Root Logins

If the root user account is active on your Linux server, it’s always a good idea to monitor the times it’s used on your server. You can do that using the [aulast](#9781284254884_Glossary.xhtml_GLOS-26) command. The aulast command displays a list of users who have logged into the system as found in the system audit logs. A sample output is shown in [LISTING 11-1](#9781284254884_CH11_01.xhtml_c11-list001).

The second column in the aulast output shows the terminal the root user account logged in from. If the terminal was a remote terminal (such as an SSH connection), the third column shows the IP address of the remote device. It’s a good idea to monitor this on a regular basis to watch for unknown login activity.

### Disabling Root Access from SSH

The openSSH software package includes an SSH server, which allows connections from remote clients using the secure SSH protocol. The /etc/ssh/sshd_config file controls the behavior of the SSH server. By default, the configuration used in Red Hat servers allows the root user account to login from a remote device. To prevent the root user account from logging from a remote device using the SSH protocol, you’ll need to modify the configuration file.

The line in the configuration file that allows this feature is:

![Permit Root Login space yes.](images/9781284255805_CH11_CUM10.jpg)

To block access for the root user account, edit the line to:

![Permit Root Login space no.](images/9781284255805_CH11_CUM11.jpg)

Then restart the openSSH service for the change to take effect:

![Dollar space sudo space system c t l space restart space s s h d.](images/9781284255805_CH11_CUM12.jpg)

After restarting openSSH you should now be denied access as the root user account in a remote SSH connection:

![Line 1: login as colon root. Line 2: root at 192 dot 168 dot 1 dot 81 apostrophe s password colon. Line 3: Access denied. Line 4: root at 192 dot 168 dot 1 dot 81 apostrophe s password colon.](images/9781284255805_CH11_CUM13.jpg)

Now the root user account can only login from a console device on the server.

### Enabling Automatic Logout

If you allow administrators on the Linux server to login using the root user account, it’s a good idea to set a timeout for the Bash shell. An unattended Bash shell prompt with the root login is a huge security risk for your Linux server environment.

The timeout feature in the Bash shell is controlled by the TMOUT environment variable. To implement a shell timeout you just need to set the TMOUT environment variable to the number of seconds you want an idle session to terminate.

For the setting to apply to all logins, you should enable it in the /etc/profile script, which the Bash shell runs at each login. However, to make adding login scripts easier, Red Hat systems also look for scripts in the /etc/profile.d directory. You can create a file in the /etc/profile.d directory that sets the TMOUT environment variable, and it will run each time a user account logs into the system and opens a Bash shell. It’s also a good idea to make the TMOUT environment variable read-only so users can’t override that feature. You do that with the readonly command.

So to implement this feature, all you need to do is create the file  /etc/profile.d/timeout.sh and include these two lines:

![Line 1: T M OUT equals 300\. Line 2: read only space T M OUT.](images/9781284255805_CH11_CUM14.jpg)

In this example we set the timeout to 300 seconds (5 minutes). Now if any user account session on the server sits idle for 5 minutes (300 seconds) the server will terminate the session.

### Blocking Root Access

If you prefer for your Red Hat server to block all access to the root user account similar to what Ubuntu does, you can do that as well. There are a couple of ways to do that:

*   Similar to the Ubuntu method, you can use an asterisk as the password value for the root user account.

*   You can assign the root user account the special no-login shell.

While Ubuntu’s method of using the asterisk as a password is perfectly valid, it’s not typically the preferred way of blocking access from a user account. The [/sbin/nologin](#9781284254884_Glossary.xhtml_GLOS-228) file is a special program that displays a message to the user, then exits. To activate it, just set it as the default shell for the root user account in the /etc/passwd file:

![root colon x colon 0 colon 0 colon root colon slash root colon slash s bin slash no login.](images/9781284255805_CH11_CUM15.jpg)

Then when you try to login using the root user account, you’ll see the default warning message and be disconnected:

![An output shows the default warning message using the s s h command.](images/9781284255805_CH11_CUM16.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-6)

You can customize the message that appears by creating the /etc/nologin.txt file and entering the text message:

![Hash echo double quote The root account not available. Please use sudo to gain root Privileges. double quote greater than slash e t c slash no login dot t x t.](images/9781284255805_CH11_CUM17.jpg)

Now when you attempt to login using the root user account, you’ll see the custom message:

![An output shows the custom message using the s s h command.](images/9781284255805_CH11_CUM18.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-7)

## Context-Based Permissions

Both the original Linux permissions method and the advanced ACL method of assigning permissions to files and directories are called [discretionary access control (DAC)](#9781284254884_Glossary.xhtml_GLOS-72) methods. The permission is set at the discretion of the file or directory owner. There’s nothing an administrator can do to prevent users from granting full permission to others on all the files in their directories.

To provide complete protection of your Linux system, it helps to utilize some type of [mandatory access control (MAC)](#9781284254884_Glossary.xhtml_GLOS-197) method. MAC methods allow the system administrator to define security based on the context of an object in the Linux system to override permissions set by file and directory owners. MAC methods provide rules for administrators to restrict access to files and directories not only to users, but also to applications running on the system.

There are currently two popular MAC implementations in Linux:

*   SELinux for Red Hat–based systems

*   AppArmor for the Ubuntu system

The following sections provide more detail on using SELinux and AppArmor in your Linux environment.

### Using SELinux

The Security-Enhanced Linux (SELinux) application is a project of the U.S. National Security Agency (NSA) and has been integrated into the Linux kernel since version 2.6.x. It is now a standard part of Red Hat–based Linux distributions, such as Fedora, Rocky, and CentOS, and an optional install for Debian-based distributions.

SELinux implements MAC security by allowing you to set policy rules for controlling access between various types of objects on the Linux system, including users, files, directories, memory, network ports, and processes. Each time a user or process attempts to access an object on the Linux system, SELinux intercepts the attempt and evaluates it against the defined policy rules.

#### Enabling SELinux

The /etc/selinux/config file controls the basic operation of SELinux. You need to set two primary settings:

*   SELINUX determines the operation of SELinux. Set this to enforcing to enable the policy rules on the system and block any unauthorized access. When you set this to permissive, SELinux monitors policy rules and logs any policy violations but doesn’t enforce them. The disabled setting value completely disables SELinux from monitoring actions on the system.

*   SELINUXTYPE determines which policy rules are enforced. The targeted setting is the default and only enforces network daemon policy rules. The minimum setting only enforces policy rules on specified processes. The mls setting uses multilayer security, providing advanced policies following the Bell-LaPadula model of security control, which is mandated by most U.S. government and military environments that require high security. It uses security classifications such as top secret, unclassified, and public. The strict setting enforces policy rules for all daemons but is not recommended for use anymore.

To change the state of SELinux, you can also use the setenforce utility from the command line. However, you can only use the utility to change SELinux between enforcing and permissive modes. To disable SELinux, you must make the change in the SELinux configuration file. To see the current mode of SELinux, use the getenforce utility:

![Line 1: dollar space sudo space get enforce. Line 2: Enforcing. Line 3: dollar.](images/9781284255805_CH11_CUM19.jpg)

For a more detailed listing of the SELinux status, use the sestatus utility:

![An output shows a more detailed listing of the S E Linux status using the s e status utility.](images/9781284255805_CH11_CUM20.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-8)

After you’ve enabled SELinux, it starts enforcing access rules on the objects defined in a set of policies. The next sections explain how SELinux policies work.

#### Understanding Security Context

SELinux labels each object on the system with a security context. The [security context](#9781284254884_Glossary.xhtml_GLOS-300) defines what policies SELinux applies to the object. The security content format is as follows:

![user colon role colon type colon level.](images/9781284255805_CH11_CUM21.jpg)

The user and role attributes are used only in the multi-layer security mode and can get quite complex. Systems running in the default targeted security mode only use the type attribute to set the object security type and control access based on that. The level attribute sets the security sensitivity level and clearance level. It is optional under the targeted security mode and is mostly used in highly secure environments.

To view the security context assigned to objects, add the -Z option to common Linux commands such as id, ls, ps, and netstat. For example, to view your user security context, use the following command:

![An output shows the user security context using the i d command with hyphen Z option.](images/9781284255805_CH11_CUM22.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-9)

The unconfined_u user security context means the user account is not assigned to a specific security policy; likewise is unconfined_r for the role and the unconfined_t for the type. The level security context of s0-s0:c0.c1023 means the security and clearance levels for the object are also not set.

To view the security context for a file use, use this:

![An output shows the security context for a file use using the l s command with hyphen Z option.](images/9781284255805_CH11_CUM23.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-10)

Again, the user and role attributes are unconfined, but now the type attribute is set to user_home_t. You can use this attribute in a security policy to set the access for files in each user account’s $HOME directory.

To examine the security context assigned to a process, use the following command:

![An output shows the security context assigned to a process.](images/9781284255805_CH11_CUM24.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-11)

The process required for the sshd application is set to the system_u user security context and system_r role security context. These indicate the process is system related. The type security context for the process is different, which means it can each be controlled with separate policies.

The semanage utility allows you to view and set the security context for user accounts on the system. For files and directories, the Linux system sets their security context when they are created, based on the security context of the parent directory. You can change the default security context assigned to a file by using the chcon or restorecon utilities.

The chcon format is as follows:

![c h con space hyphen u space new user space hyphen r space new role space hyphen t space new type space filename.](images/9781284255805_CH11_CUM25.jpg)

The newuser, newrole, and newtype values define the new user, role, and type security contexts you want assigned to the specified file.

The restorecon utility restores the security context of a file or directory back to the default settings as defined in the policies. You can use the -R option to recursively restore the security context on all files under a specified directory.

#### Using Policies

SELinux controls access to system objects based on policies. In the targeted security mode, each policy defines what objects within a specific type security context can access objects within another type security context. This is called type enforcement.

For example, an application labeled with the type security context sshd_t is only allowed to access files labeled with the type security context sshd_t. This restricts access from the application to only certain files on the system.

SELinux maintains policies as text files within the /etc/selinux directory structure. For example, all policies for the targeted security mode are under the /etc/selinux/targeted directory.

Creating your own policies can be somewhat complicated. Fortunately, SELinux includes policy groups, called modules, that you can install as standard RPM packages. Use the semodule utility to list, install, and remove policy modules in your system.

To make things even easier, SELinux uses a method of enabling and disabling individual policies without having to modify a policy file. A Boolean is a switch that allows you to enable or disable a policy rule from the command line based on its policy name. To view the current setting of a policy, use the getsebool command:

![An output shows the current setting of a policy using the getsebool command.](images/9781284255805_CH11_CUM26.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-12)

To view all of the policies for the system, include the -a option, as shown in [LISTING 11-2](#9781284254884_CH11_02.xhtml_c11-list002).

[Listing 11-2](#9781284254884_CH11_02.xhtml_c11-list002) just shows a partial output from the getsebool command; lots of different policies are installed by default in most Red Hat Linux environments.

To change the Boolean setting, use the setsebool command:

![An output shows change in Boolean setting using the setsebool command.](images/9781284255805_CH11_CUM28.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-14)

This setting only applies to your current session. To make the change permanent, you must add the -P option to the command. This gives you full control over the policy settings defined for SELinux.

### Using AppArmor

Debian-based Linux distributions commonly use the AppArmor MAC system. AppArmor isn’t as complex or versatile as SELinux; it only controls the files and network ports applications have access to.

AppArmor also defines access based on policies but calls them profiles. Profiles are defined for each application in the /etc/apparmor.d directory structure. Normally, each application package installs its own profiles.

Each profile is a text file that defines the files and network ports the application is allowed to communicate with and the access permissions allowed for each. The name of the profile usually references the path to the application executable file, replacing the slashes with periods. For example, the profile name for the mysqld application program is called usr.sbin.mysqld.

To determine the status of AppArmor on your Linux system, use the aa-status command, as shown in [LISTING 11-3](#9781284254884_CH11_02.xhtml_c11-list003).

The output from the aa-status command in [Listing 11-3](#9781284254884_CH11_02.xhtml_c11-list003) shows all of the profiles in enforce, complain, or disabled status. You can view a listing of active network ports on your system that don’t have a profile defined by using the aa-unconfined command:

![An output shows a listing of active network ports on the system that don’t have a profile defined using the a a hyphen unconfined command.](images/9781284255805_CH11_CUM31.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-16)

![An output shows a listing of active network ports on the system that don’t have a profile defined using the a a hyphen unconfined command.](images/9781284255805_CH11_CUM32.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-17)

![Line 1: dollar space sudo space a a hyphen complain space slash u s r slash s bin slash t c p dump. Line 2: Setting space slash u s r slash s bin slash t c p dump to complain mode. Line 3: dollar.](images/9781284255805_CH11_CUM33.jpg)

To turn off a specific profile, use the aa-complain command, which places the profile in complain mode:

![Line 1: dollar space sudo space a a hyphen disable space slash u s r slash s bin slash t c p dump. Line 2: Disabling space slash u s r slash s bin slash t c p dump. Line 3: dollar.](images/9781284255805_CH11_CUM34.jpg)

In complain mode, any violations of the profile will be logged but not blocked. If you want to completely disable an individual profile, use the aa-disable command:

![Line 1: dollar space sudo space a a hyphen enforce space slash u s r slash s bin slash t c p dump. Line 2: Setting space slash u s r slash s bin slash t c p dump to enforce mode. Line 3: dollar.](images/9781284255805_CH11_CUM35.jpg)

To turn a profile back on, use the aa-enforce command:

![An output shows formatting of a partition to use for encryption, using the luks Format option.](images/9781284255805_CH11_CUM36.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-18)

While not quite as versatile as SELinux, the AppArmor system provides a basic level of security protection against compromised applications on your Linux system.

## Encrypting Partitions

These days data security is a must in most business environments. With the popularity of portable laptops and external storage devices, often sensitive corporate (and sometimes personal) data are easily available for thieves to steal.

One line of defense to help protect data is encryption. Linux provides utilities to encrypt individual files, but that can get tedious. A better solution is to encrypt the entire partition where the data are stored. A popular tool for that is the [Linux Unified Key Setup (LUKS)](#9781284254884_Glossary.xhtml_GLOS-178). The LUKS system was created in 2004 by Clemens Fruhwirth specifically for encrypting Linux partitions.

The core utility in LUKS is the [cryptsetup](#9781284254884_Glossary.xhtml_GLOS-61) utility. It allows you to create encrypted partitions, then open them to make them available for formatting and mounting in the Linux virtual directory.

The first step is to format a partition to use for encryption, using the luksFormat option:

![An output shows formatting of a partition to use for encryption, using the luks Format option.](images/9781284255805_CH11_CUM37.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-19)

![An output shows formatting of a partition to use for encryption, using the luks Format option.](images/9781284255805_CH11_CUM38.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-20)

In this step you must specify the passphrase required to open the encrypted partition.

After you create the encrypted partition, you can make it available for use by using the luksOpen option:

![An output shows the encrypted partition made available for use by using the luks Open option.](images/9781284255805_CH11_CUM39.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-21)

The luksOpen option requires that you know the passphrase used to encrypt the partition. The first parameter after the luksOpen option specifies the physical partition, and the second parameter defines a name used to map the opened partition to a virtual device in the /dev/mapper directory:

![An output of l s command is shown.](images/9781284255805_CH11_CUM40.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-22)

The /dev/mapper/safedata device file now references the opened encrypted partition and can be handled as a normal Linux partition:

![The slash dev slash mapper slash safe data device file references the opened encrypted partition and is handled as a normal Linux partition.](images/9781284255805_CH11_CUM41.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-23)

After you create the filesystem and mount the partition, you can create, modify, and delete files and directories in the /mnt/mydata directory just as you would any other Linux filesystem.

To close an encrypted partition so that it can’t be accessed, use the luksClose command option:

![An output closes an encrypted partition so that it can’t be accessed using the luks Close command option.](images/9781284255805_CH11_CUM42.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-24)

When you close the encrypted partition, Linux removes it from the /dev/mapper directory, making it inaccessible. To mount the partition again you would need to use the luksOpen option in the cryptsetup command and provide the passphrase.

## Network Security Using Firewalls

Firewall software helps protect your Linux server from unwanted network access. They use access control lists (ACLs) to define what network connections can be allowed and which ones should be blocked.

The core system of creating and maintaining firewall ACLs in Linux is iptables. With iptables you define chains of rules that the kernel follows to determine if an inbound or outbound packet should be allowed or denied. However, defining rules in iptables can get a bit complicated, as it uses a somewhat arcane method of defining hosts and ports. To make life easier for administrators, a few different Linux firewall programs use easy-to-read commands to create the rules needed for the kernel to allow or deny packets. The two most popular seem to be the following:

*   firewalld—Installed by default on Red Hat-based distributions

*   ufw—Installed but not activated on Ubuntu distributions

Firewall protection is especially important when running Linux servers. You need the ability to block unwanted intruders from accessing the server applications while allowing your customers to access them freely. This section describes the firewalld program and shows how you can use it to help protect your Red Hat server on different types of networks.

### Red Hat Firewall Concepts

The [firewalld](#9781284254884_Glossary.xhtml_GLOS-106) software uses the concept of zones to define protection for the network interfaces on your Red Hat server. A zone defines the type of network the interface is connected to and what type of network traffic should be allowed or blocked. Different types of network connections require different levels of protection. For example, take the network shown in [FIGURE 11-1](#9781284254884_CH11_04.xhtml_c11-fig001).

![A box represents Red Hat Linux server in which network interface A is connected to an oval representing home network and network interface B is connected to a cloud, the Internet.](images/9781284255805_CH11_FIGF01.jpg)

FIGURE 11-1 A Linux server connected to two networks.

In [Figure 11-1](#9781284254884_CH11_04.xhtml_c11-fig001), the Linux server has two network interfaces. Network card A is connected to a home network, which includes other network devices that need to connect to the Linux system. Network card B in the server is connected to the Internet. You most likely will want to define different ACL rules for each network interface, Network card A should allow the local clients to connect to server resources, such as shared files, printers, and possibly even establish SSH connections to login.

However, Network card B needs extra security protections so that unknown attackers lurking on the Internet can’t gain access to your server. With a myriad of different network applications and protocols, you can see how it would quickly become difficult to keep things straight on the system.

The solution is to implement zone-based ACL rules. The firewalld program allows you to define multiple zones and assign each zone a different set of rules to control network access. Typically, each network interface on the server is assigned to a specific zone, based on the network requirements. The firewalld program applies the zone rules to the network interface.

By default, the Red Hat server defines ten zones. You can list the currently defined zones using the firewall-cmd command:

![Line 1: dollar space firewall hyphen c m d space double hyphen get hyphen zones. Line 2: block d m z drop external home internal n m hyphen shared public trusted work. Line 3: dollar.](images/9781284255805_CH11_CUM43.jpg)

[TABLE 11-1](#9781284254884_CH11_04.xhtml_c11-tab001) provides a basic description of what each these default zones are used for.

TABLE 11-1 The default firewalld zones.

| ZONE | DESCRIPTION |
| --- | --- |
| block | Rejects all incoming network connections and sends an ICMP prohibited message. Only outgoing network connections are allowed |
| dmz | Only selected incoming connections are accepted. |
| drop | Rejects all incoming network connections with no reply message. Only outgoing network connections are allowed. |
| external | Enables masquerading feature to hide the server’s true IP address. Only specified incoming connections are accepted. |
| home | Allows only specified incoming connections, but all outgoing connects are allowed. |
| internal | Allows only specified incoming connections are accepted. |
| nm-shared | Special zone defined for sharing on the network. |
| public | For use on untrusted networks, only select incoming connections are accepted. |
| trusted | All network connections are accepted. |
| work | For use on mostly trusted networks, only select incoming ­connections are accepted. |

Each zone has a different set of default rules assigned to it, controlling what network traffic can come in or go out from network interfaces assigned to that zone. To manage the access on a network interface you just assign it to a specific zone.

Besides zones, firewalld uses ACL rules. The ACL rules define what network connections should be allowed or blocked. With firewalld you can define the rules using two different methods:

*   Defining the service name

*   Defining the protocol port

By using service names, you can allow or block connections by application, such as FTP, SSH, or HTTP. By using ports you can allow or block connections based on TCP or UDP port numbers.

The following sections show how to use firewalld in your Red Hat server environment.

### Checking the Firewall Status

While the firewalld program uses standard text configuration files, you can use the firewall-cmd command-line command for most of the things you need to do. To check if firewalld is running, just use the --state option:

![Line 1: dollar space sudo space firewall hyphen c m d space double hyphen state. Line 2: running. Line 3: dollar.](images/9781284255805_CH11_CUM44.jpg)

You can check what zone a specific interface is currently in by using the --get-zone-of-interface option:

![Line 1: dollar space sudo space firewall hyphen c m d space double hyphen get hyphen zone hyphen of hyphen interface equals e n p 0 s 8\. Line 2: public. Line 3: dollar.](images/9781284255805_CH11_CUM45.jpg)

Or if you have multiple network interface cards you can use the --get-active-zones option to list all zones that are currently active on network interfaces:

![An output lists all zones that are currently active on network interfaces.](images/9781284255805_CH11_CUM46.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-25)

You can see the current configuration for a zone by using the --list-all option and specifying the zone name using the --zone option:

![An output shows the current configuration for a zone by using the double hyphen list hyphen all option.](images/9781284255805_CH11_CUM47.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-26)

The output shows the features and what items are allowed through the firewall for that zone. The target feature defines the action for the zone:

*   default—Rejects all packets not matching the zone rules, but sends an ICMP packet to the client indicating why

*   ACCEPT—Accepts packets not matching the zone rules

*   DROP—Drop packets not matching the zone rules

*   %%REJECT%%—Rejects all packets not matching the zone rules

The sources, services, ports, and protocols features define the rule items that are either allowed or blocked, based on the target setting. In this example, the Red Hat web cockpit service, the DHCPv6 client service, and the openSSH service are all allowed. Likewise, traffic on TCP port 631 (the CUPS application, used for printing) is allowed.

### Working with Zones

Besides the default zones you can create your own zones to help customize your server’s network environment. The --new-zone option of the firewall-cmd command defines the zone name:

![Line 1: dollar space sudo space firewall hyphen c m d space double hyphen permanent space double hyphen new hyphen zone equals my test. Line 2: Success. Line 3: dollar.](images/9781284255805_CH11_CUM48.jpg)

The --permanent option is required to make the change permanent in the configuration files. Before you can use the zone, you must tell firewalld to reload the configuration file so it knows about the new zone:

![Line 1: dollar space sudo space firewall hyphen c m d space double hyphen reload. Line 2: Success. Line 3: dollar.](images/9781284255805_CH11_CUM49.jpg)

Then you can list the zones to see if the new zone exists:

![An output lists the zones to see if the new zone exists.](images/9781284255805_CH11_CUM50.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-27)

Once you’ve created the zone you can move a network interface to the zone using the --add-interface option:

![Line 1: dollar space sudo space firewall hyphen c m d space hyphen zone equals my test space double hyphen add hyphen interface equals e n p 0 s 8\. Line 2: Success. Line 3: dollar.](images/9781284255805_CH11_CUM51.jpg)

Be careful though, as the new zone doesn’t have any ACL rules applied to it:

![An output shows the current configuration for a zone by using the double hyphen list hyphen all option.](images/9781284255805_CH11_CUM52.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-28)

If you add the network interface that you’re currently connected to the server through, this will cause your connection to drop, and possibly be a problem! The next section shows how you can add rules to the zones.

### Working with Firewall Rules

ACL rules are the core of the firewall. They define what type of network traffic is allowed or blocked by the network interface. Mistakes when adding or removing rules can be costly, especially if you’re remotely connected to the server!

The firewalld program is very robust in how it allows you to define rules. You can define rules to allow or block access based on a well-known application service name by using the --add-service option:

![An output defines rules to allow or block access based on an application service name by using the double hyphen add hyphen service option.](images/9781284255805_CH11_CUM53.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-29)

Notice again that you should add the --permanent option to ensure the new rule applies when the system reloads.

You can also specify rules as TCP or UDP port values:

![An output shows the addition of the double hyphen permanent option with rules specified as T C P port values.](images/9781284255805_CH11_CUM54.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-30)

![A script shows commands to customize a rule to specify a specific object.](images/9781284255805_CH11_CUM55.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-31)

The firewalld program also uses what it calls rich rules, which allow you to customize a rule to specify a specific object, such as a single IP address and a port or service:

![An output shows the rich rule applied to the my test zone.](images/9781284255805_CH11_CUM56.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-32)

This rich rule example accepts SSH packets (port 22) coming from a specific source address, 192.168.1.70\. The command applies this rich rule to the mytest zone. You can then check if the rule was applied:

![An output shows the rich rule applied to the my test zone.](images/9781284255805_CH11_CUM57.jpg)
[Description](9781284254884_Alt.xhtml_summary-cd11-33)

With the firewalld program you can lock down your Red Hat server as tight as you need, only opening it up to specific network clients.

![An abstract image shows a texture in the form of smoke.](images/Chapter-opener.jpg)

© Picsfive/Shutterstock

## CHAPTER 12
Linux in the Cloud

CLOUD TECHNOLOGY HAS GREATLY CHANGED the landscape of the computer world. Moving computer resources and applications into a shared network environment changes how many companies do business and provide services to customers.

This chapter introduces the main concepts of just what a cloud is and the role that Linux plays in cloud computing. The chapter starts out by defining what cloud computing is and what the different types of cloud computing environments are. Next is a discussion of how virtualization plays an important role in cloud computing and how that is implemented in Linux.

Following that is an explanation of how containers fit into cloud computing and how they have changed how developers do their jobs. A hot topic in the container world these days is orchestration. The chapter discusses how orchestration is used to manage containers and helps automate deploying them. Finally, the chapter takes a peek at a common use for containers—DevOps.

## Taking a Look at the Cloud

Before diving into how Linux participates in cloud computing, it’s a good idea to define just what a cloud is and what type of resources it provides. This section covers the basics of cloud computing.

### What Is Cloud Computing?

The term [cloud](#9781284254884_Glossary.xhtml_GLOS-45) computing relates to the ability to obtain computing resources from a remote provider. Most cloud computing providers have large data centers with excess computing power that allow them to share that computing power (or rather, lease it) with customers.

The backbone of most cloud computing data centers is Linux, operating in a distributed computing environment. In distributed computing resources are combined among two or more servers to accomplish a single task, such as run an application. Companies such as Amazon Web Services (AWS), Google Cloud Platform, and Microsoft Azure utilize large numbers of Linux servers to provide cloud computing services to their customers.

Cloud computing provides the ability to share and deliver computing resources across networks. That network can be a corporate internal network or even the public Internet. With cloud computing, customers can purchase computing resources as needed from cloud computing vendors, including servers, storage space, databases, networks, operating systems, and even individual applications.

[FIGURE 12-1](#9781284254884_CH12_01.xhtml_c12-fig001) demonstrates the three different methods for providing cloud computing services. As seen in [Figure 12-1](#9781284254884_CH12_01.xhtml_c12-fig001), there are three primary methods for providing cloud computing environments:

*   Public—In the public cloud computing environments, a third-party provides all of the computing resources outside of the organization. These resources are usually shared between multiple organizations.

*   Private—In the private cloud computing environments, each individual organization builds its own cloud computing resources to provide resources internally.

*   Hybrid—In hybrid cloud computing environments, computing resources are provided internally within the organization, but also connected to an external public cloud to help supplement resources when needed.

![A chart shows three primary methods for providing cloud computing services.](images/9781284255805_CH12_FIGF01.jpg)

FIGURE 12-1 Cloud computing methods.

[Description](9781284254884_Alt.xhtml_summary-fig12-1)

The following sections take a closer look at the different components of a cloud computing environment.

### What Are the Cloud Services?

Cloud computing environments have the ability to customize the level of resources provided to customers, depending on each customer’s needs. This section describes the three most popular models for providing resource levels that you’ll find from cloud computing vendors.

#### Infrastructure as a Service (IaaS)

In the [Infrastructure as a Service (IaaS)](#9781284254884_Glossary.xhtml_GLOS-141) model, the cloud computing vendor provides low-level server resources to host applications for organizations. These low-level resources include all of the physical components you’d need for a physical server, including CPU time, memory space, storage space, and network resources, as shown in [FIGURE 12-2](#9781284254884_CH12_01.xhtml_c12-fig002).

The server resources provided may be on a single server, or they may be distributed among several servers. In a distributed environment, the servers may be co-located in a single facility, or they may be separated into multiple facilities located in separate cities. This helps provide for increased availability.

![The I a a S cloud model is shown.](images/9781284255805_CH12_FIGF02.jpg)

FIGURE 12-2 The IaaS cloud model.

[Description](9781284254884_Alt.xhtml_summary-fig12-2)

As seen in [Figure 12-2](#9781284254884_CH12_01.xhtml_c12-fig002), in an IaaS model the customer supplies the operating system and any applications that it needs to run. Most IaaS environments support a multitude of different operating systems, including Linux, Windows, and macOS. The customer is responsible for any system administration work required for the operating system as well as any application administration. The cloud computing vendor takes responsibility for maintaining the physical infrastructure environment.

#### Software as a Service (SaaS)

In the [Software as a Service (SaaS)](#9781284254884_Glossary.xhtml_GLOS-314) model the cloud computing vendor provides both the physical server environment as well as the operating system environment to the customer, as shown in [FIGURE 12-3](#9781284254884_CH12_01.xhtml_c12-fig003).

![The S a a S cloud model is shown.](images/9781284255805_CH12_FIGF03.jpg)

FIGURE 12-3 The SaaS cloud model.

[Description](9781284254884_Alt.xhtml_summary-fig12-3)

With the SaaS model, the cloud computing vendor takes responsibility for both the physical components as well as the operating system administration. It provides system administration support to ensure the operating system is properly patched and updated to keep up with current releases and security features. This allows the customer to focus mainly on the applications running within the SaaS environment.

#### Platform as a Service (PaaS)

In the [Platform as a Service (PaaS)](#9781284254884_Glossary.xhtml_GLOS-255) model, the cloud computing vendor provides a complete computing environment for software development and deployment. The vendor provides the server environment, the operating system, and any programming tools and libraries required to develop and run applications. This is shown in [FIGURE 12-4](#9781284254884_CH12_01.xhtml_c12-fig004).

![The P a a S cloud model is shown.](images/9781284255805_CH12_FIGF04.jpg)

FIGURE 12-4 The PaaS cloud model.

[Description](9781284254884_Alt.xhtml_summary-fig12-4)

With the PaaS model, the customer can focus on developing software and deploying it to customers, often through the cloud computing environment. Clients can remotely connect to the application as it runs in the cloud computing environment to run the application. This model helps make migrating an application seamlessly through the development, test, and production phases without having to worry about changes in the server or operating system environments.

## Understanding Virtualization

The technology that made cloud computing possible is [virtualization](#9781284254884_Glossary.xhtml_GLOS-360), and this is also what has made Linux a popular choice for cloud computing vendors. Virtualization allows you to run multiple servers on a single hardware platform, sharing resources as needed between the servers.

In a normal physical server environment, the operating system may only utilize hardware resources for a fraction of the time. This results in “wasted” resources sitting idle. Virtualization takes advantage of this situation by allowing multiple servers to share the hardware resources, providing a huge cost savings. This section describes what virtualization is, the different types of virtualization available, and how to implement virtualization in a Linux environment.

### Hypervisors

For organizations that run applications that support lots of clients, a standard performance model dictates that you should separate the different functions of an application onto separate servers, as shown in [FIGURE 12-5](#9781284254884_CH12_02.xhtml_c12-fig005).

![An illustration shows different functions of an application separated onto separate servers.](images/9781284255805_CH12_FIGF05.jpg)

FIGURE 12-5 Separating application resources.

[Description](9781284254884_Alt.xhtml_summary-fig12-5)

As seen in [Figure 12-5](#9781284254884_CH12_02.xhtml_c12-fig005), the application software, the web server, and the database server are located on separate physical servers. From a performance standpoint, this model makes sense as you dedicate separate computing resources to each element. Also, from a security standpoint this helps compartmentalize access, making the job of any potential attackers a little more difficult.

However, with the increased capacity of servers, this model becomes somewhat inefficient. Dedicating an entire physical server to just running a web server, another physical server to just running the database server, and yet a third physical server to just running the application software doesn’t utilize the full power of the servers and becomes costly.

This is where virtualization comes in. With virtualization, you can run multiple virtual smaller server environments on a single physical server. [FIGURE 12-6](#9781284254884_CH12_02.xhtml_c12-fig006) demonstrates this concept.

![An illustration shows multiple virtual smaller server environments running on a single physical server.](images/9781284255805_CH12_FIGF06.jpg)

FIGURE 12-6 Server virtualization concept.

[Description](9781284254884_Alt.xhtml_summary-fig12-6)

Each virtual server operates as a stand-alone server running on the physical server hardware. This is called a virtual machine, or vm. Each server acts just as if it was located on a separate physical server. However, there needs to be a way for each virtual server to share the physical resources on the host server fairly, so they don’t conflict with one another.

This is where the hypervisor comes into play. The [hypervisor](#9781284254884_Glossary.xhtml_GLOS-137), also called a virtual machine monitor (vmm), acts as the traffic cop for the physical server resources shared among the virtual machines. It provides a virtual environment of CPU time, memory space, and storage space to each virtual machine running on the server. As far as each virtual machine is concerned, it has direct access to the server resources; it has no idea that the hypervisor is in the middle controlling access to resources.

Since each virtual machine is a separate entity on the server, you can run different operating systems within the different virtual machines. This allows you to easily experiment running applications in different operating systems, or just different versions of the same operating system. All without having to purchase additional servers.

### Types of Hypervisors

There are two different methods for implementing hypervisors. This section discusses what they are, and how they differ.

#### Type I Hypervisors

Type I hypervisors are commonly called bare-metal hypervisors. The hypervisor system runs directly on the server hardware, with no middleman. The hypervisor software interacts directly with the CPU, memory, and storage on the system, allocating them to each virtual machine as needed. [FIGURE 12-7](#9781284254884_CH12_02.xhtml_c12-fig007) illustrates this setup.

![An illustration shows the setup of Type 1 hypervisors.](images/9781284255805_CH12_FIGF07.jpg)

FIGURE 12-7 Type I hypervisors.

[Description](9781284254884_Alt.xhtml_summary-fig12-7)

In the Linux world, two popular Type I hypervisor packages are used:

*   KVM—The Linux Kernel-based Virtual Machine (KVM) utilizes a standard Linux kernel along with a special hypervisor module, depending on the CPU used (Intel or AMD). Once installed it can host any type of guest operating systems.

*   XEN—The XEN Project is an open source standard for hardware virtualization. Not only does it support Intel and AMD CPUs, but there’s also a version for Arm CPUs. The XEN Project includes additional software besides the hypervisor software, including an API stack for managing the hypervisor from a guest operating system.

#### Type II Hypervisors

Type II hypervisors are commonly called hosted hypervisors because they run on top of an existing operating system install. The hypervisor software runs like any other application on the host operating system. [FIGURE 12-8](#9781284254884_CH12_02.xhtml_c12-fig008) shows how a Type II hypervisor works.

![An illustration shows the setup of Type 2 hypervisors.](images/9781284255805_CH12_FIGF08.jpg)

FIGURE 12-8 Type II hypervisors.

[Description](9781284254884_Alt.xhtml_summary-fig12-8)

The Type II hypervisor software runs guest virtual machines as separate processes on the host operating system. The guest virtual machines support guest operating systems, which are completely separated from the host operating system. Thus, you can use a Linux host operating system and still run Windows or macOS guest operating systems.

### Hypervisor Templates

The virtual machines that you create to run in the hypervisor must be configured to determine the resources they need and how they interact with the hardware. These configuration settings can be saved to template files so that you can easily duplicate a virtual machine environment either on the same hypervisor, or on a separate hypervisor server.

The open source standard for virtual machine configurations is called the Open Virtualization Format (OVF). The OVF format creates a distribution package consisting of multiple files. The package uses a single XML configuration file to define the virtual machine hardware environment requirements. Along with that file are additional files that define the virtual machine requirements for network access, virtual drive requirements, and any operating system requirements.

The downside to OVF templates is that they are cumbersome to distribute. The solution to that is the Open Virtualization Appliance (OVA) format. The OVA template bundles all of the OVF files into a single tar archive file for easy distribution.

## Exploring Containers

While utilizing virtual machines is a great way to spin up multiple servers in a server environment, they’re still somewhat clunky for working with and distributing applications. There’s no need to duplicate an entire operating system environment to distribute an application. The solution to this problem is containers. This section explores what containers are and how they are changing the way developers manage and distribute applications in the cloud environment.

### What Are Containers?

Developing applications requires lots of files. Besides the application runtime files, there are often additional library files that are required for interfacing the application to databases, desktop management software, or built-in operating system functions. These files are usually located in various hard-to-find places scattered around the Linux virtual directory.

Because of all the ancillary files required to run an application, all too often an application will work just fine in development, then come crashing down when deployed to a production environment that doesn’t accurately reproduce the development environment. In the Windows world this is commonly referred to as DLL hell, as different applications overwrite common DLL library files, breaking other applications. However, this isn’t limited to just the Windows world; it can also apply to the Linux world.

A [container](#9781284254884_Glossary.xhtml_GLOS-56) gathers all of the files necessary to run an application—the runtime files, library files, database files, and any operating system-specific files. The container becomes self-sufficient for the application to run—everything the application needs is stored within the container.

If you run multiple applications on a server, you can install multiple containers. Each container is still a self-contained environment for each particular application, as shown in [FIGURE 12-9](#9781284254884_CH12_03.xhtml_c12-fig009).

![An illustration shows each container as a self contained environment for each particular application.](images/9781284255805_CH12_FIGF09.jpg)

FIGURE 12-9 Running an application in a container.

[Description](9781284254884_Alt.xhtml_summary-fig12-9)

The application containers are portable. You can run the same container in any host environment and expect the exact same behavior for the application. This is ideal for application developers. The developer can develop the application container in one environment, copy it to a test environment, then deploy the application container to a production environment all without worrying about missing files.

By packaging and distributing an application as a container, the developer is ensured the application will work for customers the exact same way it worked in the development environment.

Since containers don’t contain the entire operating system, they’re more lightweight than trying to distribute a full virtual machine, making them easier to distribute. The following section describes two of the most common container packaging systems used in Linux.

### Container Software

Linux has been in the forefront of container development, making it a popular choice for developers. Two main container packages are commonly used in Linux:

*   LXC—The LXC package was developed as an open source standard for creating containers. Each container in LXC is a little more involved than just a standard lightweight application container, but not quite as heavy as a full virtual machine, placing it somewhere in the middle. LXC containers include their own bare-bones operating system that interfaces with the host system hardware directly, without requiring a host operating system. Because the LXC containers contain their own mini-operating system, they are sometimes referred to as virtual machines, although that term isn’t quite correct as the LXC containers require the host operating system to operate.

*   Docker—The Docker package was developed by Docker Inc. and released as an open source project. Docker is extremely lightweight, allowing several containers to run on the same host Linux system. Docker uses a separate daemon that runs on the host Linux system that manages the Docker images installed. The daemon listens for requests from the individual containers as well as a Docker command-line interface that allows you to control the container environments.

### Container Templates

Just like virtual machines, containers allow you to create templates to use to easily duplicate container environments. The different types of Linux containers utilize different methods for distributing templates.

The LXC package uses a separate utility called LXD to manage containers. LXD uses system images of the container

Docker uses Docker image files to store container configurations. The Docker image file is a read-only container image that you can use to store and distribute application containers.

## Using Containers

When implemented correctly, containers provide a way to increase the speed and agility of application deployment. Whether your company’s data center is local or in the cloud, you can use container concepts to quickly set up your app’s required infrastructure. A few important infrastructure provisioning concepts are covered in the following sections.

### Creating the Container

Much like a physical data center, a container needs to be managed and controlled. In most environments, the container’s configuration is treated in a manner similar to how software revisions are treated. The following sections outline the basic ideas in creating a container environment for an application.

#### Design the Container

Along with the app requirements, the environment on which the app is executed must be preplanned. This activity is a mutual one between software development and tech ops. In this mutual activity, the container’s operating system, libraries, services, security configuration, and any other supporting software or networking utilities are chosen.

The determined infrastructure is frozen to provide a non-changing environment for development and then production. Typically, this app container infrastructure is only accessible via the app’s or developer’s API. Remote access services such as OpenSSH are not provided in order to protect its environment.

#### Document the Container

The preset app container is typically documented to ensure the container can be accurately duplicated. While there are plenty of ways to document containers, these days this is often done using an [orchestration](#9781284254884_Glossary.xhtml_GLOS-236) tool. Orchestration tools allow you to easily automate the configuration, management, and coordination of containers. The configuration settings are loaded in a process called automated configuration management. The data are later used to deploy and replicate the app containers through build automation.

#### Provide Revision Control

The configuration management information is not just documented, it is also inserted into an orchestration tool registry, providing version control. Every time a change occurs in the container image infrastructure, its modifications are tracked in the version control system. This ensures any bugs introduced into the process can easily be “backed out” to a prior version of the app.

#### Troubleshoot the Container

If an app container is deployed into production and problems occur, tech ops, software developers, or both handle the troubleshooting process. One item to check is the production container’s documented configuration (as well as its revisions) to determine if any infrastructure items may be to blame.

This provides an easier method for tracking down any new software libraries that could cause problems. Various orchestration tools allow a quick determination of modified infrastructure components and quicker problem resolution.

Handling the application’s infrastructure in this manner increases the agility of your app container deployment. It also improves the time to production speed. The basic life cycle of an orchestrated app container image is shown in [FIGURE 12-10](#9781284254884_CH12_04.xhtml_c12-fig010).

![A flow diagram shows life cycle of basic app container.](images/9781284255805_CH12_FIGF10.jpg)

FIGURE 12-10 Basic app container life cycle.

[Description](9781284254884_Alt.xhtml_summary-fig12-10)

Notice in [Figure 12-10](#9781284254884_CH12_04.xhtml_c12-fig010) that at the end of container’s life cycle (typically when the new app container image is ready), the container image is removed. However, the old app container image’s configuration should be stored within a version control system (or backup storage) and thus redeployed if any problems occur with the new app container image.

### Automating the Container

With automated configuration management, not only can you troubleshoot the infrastructure more easily and roll the environment back to an earlier version, container deployment is automated. Often more than one app container is used to help load balance user requests. A high-volume web environment may require hundreds of running production app containers.

Manually configuring this infrastructure is tedious and certainly not fast or cost effective. With orchestration tools, such as Chef and Puppet, and automated configuration management, you can easily replicate the production app container and don’t even have to be involved in the process (build automation). You simply let your orchestration tool know that you need X number of production app container images running at any one time.

### Agent and Agentless Containers

Orchestration monitoring, logging, and reporting tools let you track app containers’ health (how well they are performing, and if each one is still alive). Concerns over how these tools may adversely affect an app container’s health gave rise to the agent versus agentless dispute.

Agent monitoring tools are orchestration utilities that require software (an agent) to be installed in the app container being monitored. These agents collect the data and transmit it to another location, such as a monitor server. The monitor server manages the information, provides analysis reporting, and also sends alerts for events, such as a container crashing.

Agentless monitoring tools are also orchestration utilities. In this case, an agent is not installed in the app container being monitored. Instead, the tool uses preexisting and/or embedded software in the container or the container’s external environment to conduct its monitoring activity.

Whether to use an agent-based or an agentless orchestration utility is hotly debated. Some people feel that an agent is detrimental to an app container’s performance, while others see only minor effects. Some tech ops insist that agentless tools are inflexible, while others believe installing and maintaining an agent in their containers is an unnecessary hassle. Whatever side you choose, realize that most companies use a combination of agent and agentless orchestration tools.

### Monitoring Containers

Orchestration monitoring utilities can automatically deal with an app container’s untimely demise. When an app container shuts down, this triggers an event, and the desired state is no longer met. A desired state is a predetermined setting that declares how many containers should be deployed and running.

For example, imagine that your software application needs to have 10 production app containers running to efficiently handle the workload. If one of those containers crashes, the container inventory now switches to nine. This triggers an event in the monitoring utility that the desired state is no longer being met.

Many orchestration utilities employ self-healing. With self-healing, if the desired state is not currently being achieved, the orchestration tool can automatically deploy additional production app containers. In the previous example, this means that the orchestration tool would immediately start up an additional production app container using the container’s stored configuration settings (build automation). No human involvement is needed.

When a new production app container is first deployed, the self-healing orchestration property will cause containers to be deployed automatically until the desired state is met. That’s handy.

## Container Orchestration Engines

Whether the containers are on your local servers or in the cloud, properly maintaining them requires some type of orchestration engine (also called orchestration systems). No one system can do it all. The best combination is a set of general and specialized orchestration tools.

### Kubernetes

Originally designed and used by Google, Kubernetes is an open-source orchestration system that is considered by many to be the de facto standard. Not only is Kubernetes very popular and free, it also is highly scalable, fault tolerant, and easy to learn.

This system contains years of Google’s orchestration experience, and because it is open source, additional community-desired features have been added. This is one reason so many companies have adopted its use for container orchestration.

Each Kubernetes managed service or application has the following primary components:

*   Cluster service—Uses a YAML file to deploy and manage app pods

*   Pod—Contains one or more running app containers

*   Worker—Pod host system that uses a kubelet (agent) to communicate with cluster services

*   YAML file—Contains a particular app container’s automated configuration management and desired state settings

This distributed component configuration allows high scalability and great flexibility. It also works very well for continuous software delivery desired by companies employing the DevOps model.

### Docker Swarm

Docker, the popular app container management utility, created its own orchestration system, called Docker Swarm (also called Swarm). A group of Docker containers is referred to as a cluster, which appears to a user as a single container. To orchestrate a Docker cluster, you can employ Swarm.

With the Swarm system, you can monitor the cluster’s health and return the cluster to the desired state should a container within the cluster fail. You can also deploy additional Docker containers if the desired app performance is not currently being met. Swarm is typically faster than Kubernetes when it comes to deploying additional containers.

While not as popular as the Kubernetes orchestration system, Docker Swarm has its place. It is often used by those who are new to orchestration and already familiar with Docker tools.

### Mesos and Marathon

Mesos (also called Apache Mesos) is not a container orchestration system. Instead, Apache Mesos, created at the University of California, Berkeley, is a distributed systems kernel. It is similar to the Linux kernel, except it operates at a higher construct level. One of its features is the ability to create containers. The bottom line is that Apache Mesos combined with another product, Marathon, does provide a type of container orchestration system framework. You could loosely compare Mesos with Marathon to Docker with Swarm.

Mesos with Marathon provides high availability and health monitoring integration and can support both Mesos and Docker containers. This orchestration framework has a solid history for large container deployment environments.

## Understanding DevOps Concepts

One particular place where containers and orchestration have made an impact in the IT world is DevOps, which is getting a lot of attention these days. [DevOps](#9781284254884_Glossary.xhtml_GLOS-68) defines a methodology for creating and deploying applications by melding the functions of both software developers and IT operations. While not required, containers can help this process by providing a platform to automate deployment of applications from the development to production environments. This section provides an overview of what DevOps is all about.

### DevOps Procedures

In DevOps, the main goal is to quickly and continually provide new software features, bug fixes, and desired modifications to the customer. The focus is on continual small changes to the app as opposed to large monolithic updates. Doing that involves several steps, as outlined in this section.

#### Continual App Processing

One DevOps layer involves the process of developers making software revisions in a controlled centralized repository. The centralized repository makes it easier to quickly integrates app changes into the main software branch (continuous integration) using an automated method. In addition, these changes undergo automated testing to avoid breaking the app when the branch merges (continuous testing). With the help of the two previous components, software is delivered to the customer on a continual basis (continuous delivery).

#### Controlling the App Environment

To support this continuous app processing layer, it is helpful in DevOps that the development and production environments match. This includes equivalent hardware, device drivers, operating system versions, software libraries, and so on. The requirement provides a software development environment that produces production code free from bugs and complications due to mismatched environments.

In addition, environment changes must be controlled and tested in a manner similar to how software revisions are orchestrated. For example, if a controlled update to the Linux kernel in the development environment introduces an unforeseen app bug, the environment can be rolled back to its previous version until the bug is addressed. Environment updates are typically done in small chunks, much like app revisions are handled, so that each environment modification can be properly and discretely managed. Tested new environments are added to a registry where older environments are also maintained in case a rollback to an earlier environment is needed.

#### Defining the App Environment

In DevOps, the development and production environments (infrastructure) have predefined specifications, such as what hardware devices are required, the essential operating system, and any needed software packages as well as critical code libraries. The non-hardware specifications are typically implemented into the environment via automated code (configuration management).

Besides an environment’s configuration, security measures, such as firewall configurations and authentication policies, must also be orchestrated. This too is implemented into the environment via automated code (policy as code).

Configuration management and policy as code fall under the umbrella term infrastructure as code. A benefit of using infrastructure as code is that the environments are repeatable. Also, they can be versioned, which is needed to implement revision control in the app environments for both policies and configuration. This DevOps component is covered more in depth later in this chapter.

#### Deploying the App Environment

The app and its development environment are often moved to a production status (production environment) in a continual manner. The “continual manner” can be hourly, daily, weekly or whatever meets the app’s business requirements.

The benefit of employing infrastructure as code techniques is that the process of deploying the app and its environment can be easily automated (infrastructure automation). Red Hat’s Ansible product is one tool used for this DevOps deployment.

#### Monitoring the App Environment

When the app is operating in its production environment, it needs to be monitored and logged. Software metrics, infrastructure resource usage, and performance statistics are just a few of the items to monitor and log. The goal is to track the app environment and ensure that it is meeting predetermined conditions (environment health). Often this monitoring is automated as well.

As business needs change, the logged data can be valuable for future desired environment states. It provides threshold and performance measurements that make much easier decisions as to what app or environment infrastructure modifications are needed.

In addition, monitoring can provide alerts to potential failures or resource depletion events. If a particular preset limit is crossed, the monitoring software can issue an alert or even handle the event itself using predefined event rules.

Orchestration is the key to agile DevOps. Besides the methodology, various orchestration tools provide additional speed needed to succeed in the continual software delivery business setting.

### DevOps Container Attributes

Virtualization, and more specifically containers, greatly assists in the DevOps process. Containers in DevOps provide the following.

#### Static Environment

Containers provide a predetermined app environment (also called a container image) that does not change through time (immutable). The container is created with preset library and operating system versions and security settings. All these settings are recorded. No software updates using the standard operating system upgrade packages are issued within the image.

#### Version Control

After the software development process and prior to moving a modified app container image into production, the container and its recorded configuration are registered with a version control system. The version control system can contain previous app container images, including the one currently in production. Some companies use a manual version control system implemented via backups.

#### Replace Not Update

After registration, the app container is ready to move into production. Instead of the production app container image being updated to match the development image, the production container is stopped. The development app container image then replaces the production container and starts as the production environment. Thus, an environment switch occurs.

#### High Availability

Replication is the process of creating multiple copies of the production app container image and running them. This allows you to stop old currently unused production app containers and replace them with the new production app containers, which provides continual uptime for your app users. With containers and replication, the old method of shutting down your production environment to update it during a time period in the wee hours of the morning is gone.

To accomplish these tasks with container images, you need orchestration. Orchestration principles provide the tools, utilities, and guidance for implementing app container images in a fast-paced environment, such as one that uses DevOps. So in the end, the cloud, containers, orchestration, and DevOps all interact together to create the ideal application environment for today’s high-demand web world.

## Resources

Docker Documentation, “What is a Container?” Accessed on Jan. 29, 2022, from [https://www.docker.com/resources/what-container](https://www.docker.com/resources/what-container).

Red Hat Documentation, “Understanding Cloud Computing,” Accessed on Jan. 29, 2022 from [https://www.redhat.com/en/topics/cloud](https://www.redhat.com/en/topics/cloud).

Red Hat Documentation, “Understanding DevOps,” Accessed on Jan. 29, 2022, from [https://www.redhat.com/en/topics/devops](https://www.redhat.com/en/topics/devops).

![An abstract image shows a texture in the form of smoke.](images/FM-opener.jpg)

© Picsfive/Shutterstock

## APPENDIX A
Answer Key

## CHAPTER 1 Linux Basics

1\. A  2\. B  3\. C  4\. A  5\. C  6\. A  7\. D  8\. A  9\. B  10\. D

## CHAPTER 2 Linux and Software

1\. A  2\. B  3\. B, C  4\. C  5\. A  6\. D  7\. A  8\. C  9\. D  10\. A

## CHAPTER 3 Linux and Hardware

1\. B  2\. D  3\. A, C  4\. B  5\. B  6\. A  7\. A  8\. C  9\. D  10\. A

## CHAPTER 4 Booting Linux

1\. A  2\. C  3\. B  4\. A  5\. D  6\. A  7\. C  8\. B  9\. D  10\. A

## CHAPTER 5 Disk Management

1\. A  2\. B  3\. E  4\. C  5\. B  6\. A  7\. D  8\. B  9\. B  10\. A

## CHAPTER 6 Command Line Basics

1\. D  2\. A  3\. B  4\. A  5\. C  6\. A  7\. A  8\. B  9\. C  10\. A

## CHAPTER 7 File Management

1\. B  2\. C  3\. A  4\. A  5\. A  6\. B  7\. A  8\. D  9\. B  10\. A

## CHAPTER 8 Networking Concepts

1\. A  2\. E  3\. A  4\. E  5\. B  6\. B  7\. A  8\. B  9\. E  10\. C

## CHAPTER 9 Managing Processes

1\. B  2\. E  3\. C  4\. A  5\. C  6\. B  7\. C  8\. D  9\. E  10\. C

## CHAPTER 10 Advanced Administration

1\. C  2\. A  3\. D  4\. B  5\. A  6\. A  7\. A  8\. B  9\. B  10\. A

## CHAPTER 11 Linux Security

1\. A  2\. C  3\. B  4\. C  5\. A  6\. C  7\. B  8\. B  9\. A  10\. A

## CHAPTER 12 Linux in the Cloud

1\. B  2\. C  3\. A  4\. C  5\. D  6\. C  7\. C  8\. A  9\. C  10\. D

![](images/FM-opener.jpg)

© Picsfive/Shutterstock

# Glossary

/dev/disk/by-id A directory that contains persistent links to storage device partitions based on their manufacturer information.

/dev/disk/by-label A directory that contains persistent links to storage device partitions based on their label.

/dev/disk/by-path A directory that contains persistent links to storage device partitions based on their hardware connection.

/dev/disk/by-uuid A directory that contains persistent links to storage device partitions based on their Universal Unique ID.

/dev/mapper A directory that contains raw device files that point to dynamic and virtual partitions created by LVM and multipath.

/etc/crypttab A configuration file that contains entries identifying encrypted storage device partitions Linux should mount at boot time.

/etc/fstab A configuration file that contains entries identifying the storage device partitions Linux should mount at boot time.

/etc/mstab A dynamic file that identifies the currently mounted partitions on the Linux system.

/proc/mounts A kernel-generated file that contains information about the currently mounted partitions and their location in the virtual directory.

/proc/partitions A kernel-generated file that contains information about the currently mounted partitions on the Linux system.

/sys/block A kernel-generated file that contains information about the block devices on the Linux system, including any mounted partitions.

Absolute filepath A filepath that contains the full path to a file, starting at the root directory.

Absolute path A directory or file path name that represents the location of the directory or file based on the root directory of the virtual directory.

Administration user account A user account that has full privileges on a Linux system.

Aliases Alternative names that can be used to receive email for a user account on an email server.

Apache Open-source web server commonly used in the Linux environment.

AppArmor A package used mostly in Ubuntu distributions for applying MAC-based permissions to files.

Application container Creates an environment where all of the files required for an application to run are bundled together, including runtime library files.

apropos A program that displays application documentation using advanced features such as links.

apt Command-line package manager program for Debian-based systems that can automatically install packages from the repository.

Asterisk A globbing character that matches zero or more characters in the file name.

Asymmetric encryption Applies encryption to files by utilizing a secret private key and a public key that can be made known to others.

at A command that allows you to schedule when a program should start.

atq A command that lists the jobs scheduled to start.

atrm A command that removes jobs scheduled to start.

aulast A utility for displaying the login activity for user accounts on the system.

Bash The most common Linux shell.

Basic Input/Output System (BIOS) A firmware that controls how an IBM-compatible system starts.

bg a command that restarts a stopped job in background mode.

blkid A utility in the e2fsprogs package that displays information about block devices, such as storage drives.

Block device file A type of device file that sends and receives data in multi-byte blocks.

Block devices Hardware devices that send data in block chunks to the system.

Boot loader A small program that launches the operating system at startup.

Boot manager A small boot loader program built into UEFI that controls which boot loader program to run.

btrfs A Linux file system that utilizes journaling and has increased performance.

cd A command to change the current directory for the command line.

chage Changes password properties for user accounts.

Chainloading The process of running a secondary boot loader from a primary boot loader.

Character device file A type of device file that sends and receives data 1 byte at a time.

Character devices Hardware devices that send data one character at a time to the system.

Chattr A utility in the e2fsprogs package that allows you to change attributes of files.

Chromium The open-source version of the Google Chrome browser.

CIFS The Common Internet File System, provides a protocol for accessing shared drives on a network.

Cinnamon A Linux desktop project started by the Linux Mint distribution.

Cloud A network of distributed applications running on separate servers.

Cold pluggable A hardware device that must be installed or removed when the system is powered off.

Collection Consists of documents which contain the individual data elements.

Command completion Allows you to begin typing a command or program and hit the Tab key to view commands and programs that match.

Command line interface (CLI) Provides an interactive interface for submitting commands to the kernel and displaying output from programs.

Command prompt A symbol used to prompt you to enter commands to the shell.

Common Unix Print System (CUPS) A program for providing a common interface for printing in Linux environments.

Compiled device driver Software compiled into the kernel software for hardware devices.

Compressed directory A Windows feature for creating zip files.

configure Program to run that determines the requirements for compiling an application.

Console A text-based interface to the Linux system.

Container An environment where all of the files necessary to run an application are bundled together in a single package to install as a whole.

Core Linux distribution A bundle of the Linux kernel, one or more graphical desktop environments, and most Linux applications.

Coreutils A GNU software package that contains utilities for file handling, text manipulation, and managing processes.

Cp Command to copy a file on the Linux system.

Cron A program that runs jobs at a pre-defined time and date

cryptsetup The utility used in LUKS For formatting, opening, and closing encrypted partitions.

date Display or change the time and/or date on a Linux system.

debugfs A utility in the e2fsprogs package that allows you to manually view and modify a file system structure.

Default.target A Systemd target that defines what unit files to start when the system boots.

Dependencies Packages that are required for another application package to run.

Device driver Small piece of software written to interact with a specific hardware device.

Device files Special files used by the Linux system to send and receive data with a hardware device.

DevOps A methodology for creating, deploying, and maintaining applications.

df A utility for displaying the utilization of drive partitions currently mounted on the Linux system.

dig A Linux command that displays DNS records for a servers in a domain.

Direct memory access (DMA) A system that allows hardware devices to store data directly in memory locations for the CPU to read.

Discretionary access control (DAC) The ability of users to define their own permissions to files and directories.

Distribution The bundling of a kernel, graphical desktop, and multiple applications into one package.

dm-multipath A Linux kernel module that supports multipath storage device access.

Dnf An updated version of yum with some additional features documents that contain the individual data elements.

Dolphin A graphical file manager program used in KDE desktops.

Dpkg Low-level command line package manager program for Debian-based distributions.

Drive letters An alphabetic letter designation used by Microsoft to indicate the device a file or directory is stored on.

Driver code Low-level programming code designed for the kernel to pass data back and forth with a device.

du A utility that displays the current files and space used by directories in the virtual directory structure.

dumpe2fs A utility in the e2fsprogs package that displays low-level block and superblock information about a storage device.

e2label A utility in the e2fsprogs package that allows you to modify the label assigned to a partition formatted with the ext file system.

ecryptfs A Linux file system that supports real-time file encryption.

EFI System Partition (ESP) The disk partition that stores boot loader files on a UEFI system.

Environment variables Memory locations in the shell that allow you to store values.

Escaping Placing a backslash (\) in front of a character so the shell interprets it as data and not a special command or character.

ethtool A Linux command that displays or sets Ethernet parameters on a network interface.

Evolution Graphical email client program used in GNOME desktop distributions.

Execute The permission that allows user accounts to run an application file.

eXim An open-source email server application that uses a simplified configuration file.

export Convert a local environment variable to a global environment variable.

ext3 The third version of the original Linux ext file system. It provides journaling capabilities for minimizing data loss after a server crash.

ext4 The current version of the original Linux ext file system. It incorporates journaling and additional performance enhancements.

Extended partition A partition method used by MBR drives to expand the number of partitions available on a storage device.

Extensible Firmware Interface (EFI) Created by Intel in 1998 to replace the BIOS.

External commands External programs and utilities that run on the Linux system.

fdisk A utility that allows you to partition MBR drives.

fg A command that restarts a stopped job in foreground mode.

File A command that displays the file type of the specified file.

File Allocation Table (FAT) A disk filesystem created by Microsoft.

File system A method of organizing files and directories on a Linux partition to help with storage and retrieval.

File system hierarchy standard (FHS) A Linux standard that specifies a virtual directory structure for organizing system and user files.

Files An open-source file manager program used in GNOME desktop distributions.

Find A versatile command that can search for files based on various file properties.

Firefox Graphical browser application available for multiple operating systems.

firewalld A package used mostly in Red Hat-based distributions for creating network firewalls.

Flatpack Application container format was created as an independent open source project with no direct ties to any specific Linux distribution.

Forwarding The ability to redirect email messages to another location.

Fsck A utility for analyzing and repairing Linux file systems.

Full-word parameters A word option used to modify the behavior of a command.

gcc A C and C++ program compiler for Linux created by the GNU project.

Gdisk A utility that allows you to partition GPT drives.

General purpose I/O Provides multiple digital input and output lines for receiving digital data and sending digital signals.

Ghostscript An open-source project to read and manage postscript files.

Global environment variable Stored data that can be accessed by any child process the shell spawns.

Globbing Using a wildcard character to specify one or more-character patterns to match in a filename.

GNOME Terminal The terminal emulation package used in GNOME desktops.

GNU (GNU’s Not Unix) An open-source project for porting Unix utilities for other operating systems.

GNU IceCat An open-source browser derived from the Firefox graphical browser.

GNU Network object model environment (gnome).

GNU Privacy Guard (GPG) A program for encrypting files.

gparted A graphical tool for easily viewing and modifying the partition on MBR and GPT drives.

Grand Unified Boot Loader (GRUB) Legacy An updated Linux boot loader that provided more robust features than LILO.

Group A set of user accounts that are granted the same permissions to files and folders.

Group permissions Set of access permissions applied to a file or directory for a specific user group.

GRUB2 An improved version of GRUB Legacy that can load hardware device drivers and use logic to dynamically alter the boot menu options.

GUID Partition Table (GPT) A system for organizing storage device partitions on a UEFI system.

gzip The Linux utility to compress files and directories.

Hard disk drive (HDD) A storage device that utilizes multiple disk platters and a read/write arm for magnetically storing persistent data.

Hard link Two files or more files that point to the same inode number

help A command to display information about shell built-in commands.

Hidden files Files that don’t appear in a standard directory listing.

Hierarchical File System (HFS) The default file system used for Apple macOS.

History file A file that stores each command entered into the command line from a session.

host A Linux command that displays the IP address of a specified host name, or the host name for a specified IP address.

Hot pluggable A hardware device that can be installed or removed while the system is powered on and running.

Hypervisor Manages the host physical resources between multiple virtual machines.

I/O ports Sections in memory where hardware devices can send and receive data from the CPU.

ifconfig A Linux command for displaying or setting the network address information for a network interface.

info A newer program to display application documentation.

Infrastructure as a Service (IaaS) The cloud provides low-level server resources to host applications.

init The initial program started by Linux that starts all other programs running on the system.

Init process|The first process started by the kernel at boot time, which is responsible for starting all other processes on the system.

Initialization process The process of starting background programs on the Linux system.

Inline input redirection Changes the input to an application to the command line.

Inode A special file that contains properties of a file on the Linux system.

Inode number A number assigned to each inode, unique for each disk partition.

Inode table A listing that matches inodes to each file on the disk partition.

Input redirection Changing the input to an application to a file.

insmod Installs a device module file into the kernel.

Internal commands Commands built into the shell for interacting with the kernel.

Internet Control Message Protocol (ICMP) A standard protocol for sending control packets to a remote device for testing and network information.

Interrupt requests Signals the CPU that a hardware device wants to send data.

iostat A utility to display a real-time chart of drive statistics based on partitions.

ip (command) A Linux command for displaying or setting IP network information on a network interface.

iproute2 An open-source collection of command-line tools for displaying and managing network configuration settings.

ISO image file |A copy of all the files contained on a DVD stored as a single file.

ISO-9660 A file system used for storing data on optical CD ROM devices.

jobs A command that controls processes running in background.

journalctl The systemd program for reading the log files created by the systemd-journald program.

Journaling A file system method that logs transactions separately so that any uncommitted transactions can be recovered in case of a system crash.

K Desktop Environment (KDE) A Linux graphical desktop released in 1996, similar to the Microsoft Windows environment.

KDE Plasma The branding of the current version of the K desktop environment.

Kernel The core Linux software that controls all of the hardware and software on a computer system.

Kernel modules Allows you to insert device driver code into a running kernel without having to recompile the kernel.

Kernel ring buffer A circular buffer in memory that contains boot messages.

Key mode The ability to log into a remote server using a public/private key pair.

kill sends a signal to a running process to pause or stop it.

KMail An email client designed by the KDE project.

Konsole The terminal emulation package used in KDE desktops.

kpartx A utility that configures multipath access to storage devices.

LibreOffice An open-source office productivity application common in Linux distributions.

Lighttpd A lightweight web server used in Linux distributions intended for low-power workstations.

Line Printer Daemon (LPD) A legacy printing method used in BSD Unix and implemented in Linux.

Link local address An ipv6 address assigned automatically to a device on a local network so it can communicate with other local devices without requiring to obtain a network address.

Links Virtual copies of a physical file.

Linux Loader (LILO) The original Linux boot loader program.

Linux Unified Key Setup (LUKS) A tool created for applying encryption to Linux partitions.

LiveDVD A self-contained ISO image file that can be burned onto a DVD disk or USB stick to boot up a Linux system directly.

Local environment variable Stored data that can only be accessed by the shell that defines them.

Local loopback interface A virtual network interface provided to allow applications to communicate internally using network protocols.

Locate A command that uses a database to quickly locate programs on the Linux system.

Logical volume manager (LVM) A method of creating and maintaining virtual storage volumes from one or more physical partitions. It allows you to dynamically add or remove partitions within the file system.

ls The list command, used to list files and folders on the system.

lsblk A command line utility that displays current partition sizes and mount points.

lsmod Command to list device modules installed in the kernel.

lspci A Linux program to displaying PCI boards connected to a system.

lsusb Lists information about the USB devices connected to the Linux system.

lvcreate A command line utility that creates logical volumes.

Lynx A command line text-based browser often used in screen-scraping text from websites in scripts.

Mail Delivery Agent (MDA) Receive incoming mail messages from an MTA and ensure they go to the correct local user mailbox.

Mail Submission Agent (MSA) Accept email messages from local users and submit them to the MTA for delivery to the proper user.

Mail Transport Agent (MTA) Send messages to remote servers and receive messages from remote servers.

Mail User Agent (MUA) Provide an interface for users to read their messages and send new messages.

Make A command line program used to compile application source code.

man A program that displays documentation about installed applications.

Mandatory access control (MAC) The ability of the system administrator to assign permissions to files and directories.

MariaDB An open-source relational database that supports advanced database features.

Master Boot Record (MBR) A system for organizing storage device partitions on a BIOS system. The first sector on a hard drive partition that contains the boot loader program.

MATE A Linux graphical desktop environment created in 2011 for Arch Linux.

mdadm A command line utility for working with multipath storage devices.

Memory management The ability to control how programs and utilities run within the memory restrictions of the system.

mkdir Command to create a new directory.

mkfs A command line utility for creating file systems.

modprobe Installs and removes device module files into the kernel.

Modules Device software that can be inserted into a running kernel.

MongoDB An open-source database that uses the nosql database format.

mount A command line utility for mounting partitions within the virtual directory structure at a mount point.

Mount points A directory within the virtual directory used as a mount point for partition file systems. Directories in the virtual directory where you assign additional storage devices

Mounting The process of adding the file system contained on a partition to the Linux system’s virtual directory structure.

Multipath The ability to define multiple paths to a storage device. The multiple paths can be aggregated to provide more bandwidth, and provide fault-tolerance if one path goes down.

multipathd A background process that monitors connections for multipath storage devices.

Multi-user operating system A computer systems that allows multiple users to log in simultaneously and submit programs.

mv Command to move (rename) a file on the Linux system.

MySQL An open-source relational database that is fast but doesn’t support many advanced features.

netstat A Linux command for displaying open network ports on the system, as well as network statistics.

Net-tools A legacy open-source collection of command-line tools for displaying and managing network configuration settings.

Network device file Also called a socket file, used to easily send packets of data to devices, usually network cards.

Network File Sharing (NFS) An open-source application used to share files from a Linux server with other Linux servers.

Network Manager A set of both graphical and command-line tools for defining network interface settings.

Network Time Protocol (NTP) A standard protocol for sharing the time across multiple devices on a network.

NginX An open-source web server for Linux commonly used in environments that require load balancing between multiple servers.

nice A command to specify the priority of a program when started.

nmcli A command line tool for defining network interface settings.

nmtui A text-based menu tool for defining network interface settings.

Nodes A special file in Linux for communicating with a device on the system.

nohup A program that runs a command and blocks any SIGHUP signals sent to it.

nologin A utility used as the default shell for user accounts that shouldn’t log into a command line.

Normal user account A user account that does not have permissions to system files and folders, but only to the user files and applications.

NoSQL Databases can handle large quantities of data by foregoing the structured database tables of SQL relational databases and instead store data as structure-less collections.

New Technology File System (NTFS) The file system used by Microsoft workstations and servers.

Open-source software (OSS) A licensing concept for programmers to release software with no restrictions attached on its use.

OpenOffice.org The original open-source office productivity application for Linux and other operating systems.

OpenSSH An Open-source program for securely sending data across a network.

Opera A commercial (but free) web browser program for Linux.

Orchestration Tools that allow you to automate configuration, management, and coordination of containers.

Orphan file A file whose owner user account no longer exists on the system.

Other permissions The set of file or folder permissions that apply to all other user accounts on the system that aren’t the owner or in the default group for the file or folder.

Output redirection Changing the output of an application from the standard output to a file.

Owner permissions The set of file or folder permissions that apply to the owner of the file or folder.

Package A bundle of files required for an application. The package allows users developers to distribute an application as a single file.

Package management system A system for tracking which applications are installed on a Linux system.

Pages Blocks of memory that are allocated by the kernel.

Parallel Advanced Technology Attachment (PATA) An older storage device connection method that utilizes parallel connections.

Parted A command-line utility for partitioning storage devices, supported by the GNU project.

Partition A subsection of a hard drive that can be formatted to support a file system.

passwd A command-line utility for changing the password for a user account.

Password mode The method of using a password to log into a remote system.

Peripheral Component Interface (PCI) A standard for communicating with hardware boards.

Persistent device files Files located in the /dev/ disk directory that always point to the same storage device, based on manufacturer id, system label, connection path, or UUID value.

ping A command line tool for testing connectivity to remote systems using the ipv4 protocol.

ping6 A command line tool for testing connectivity to remote systems using the ipv6 protocol.

Piping Redirecting the output of one command to the input of another.

pkill sends a signal to a running process, specified by name, to pause or stop it.

Platform as a Service (PaaS) The cloud provides a complete computer environment for software development and deployment.

Plug-and-Play System for automatically configuring hardware on IBM-compatible PCs.

Postfix An open-source email server application that uses simplified configuration files.

PostgreSQL An open-source relational database that supports advanced database features.

Postscript Printer Definition (PPD) A set of rules that define how Linux should handle a Postscript file for a printer.

Postscript protocol A formatting language that defines how the printer displays text and graphics.

Power-on self-test (POST) The firmware performs a quick check of the hardware.

Primary partition One of four main partitions that you can create on an MBR drive.

Private key The part of an asymmetric encryption key pair that you must keep and not share with others.

proc directory Virtual directory that displays information about the kernel.

Process a running program on the Linux system.

Procmail An MDA program that allows the mail administrator to customize mail delivery to users.

ps A command to display a snapshot of the running processes at a specific time.

Public key The part of an asymmetric key pair that you share with others who need to send you encrypted files.

pvcreate A command line utility for defining physical volumes in an LVM setup.

qMail An open-source email server that is maintains high-reliability in case of system crashes.

Question mark A globbing character that matches one character in the file name.

Quoting Placing quotes around a filename that contains spaces.

RAID 0 A data storage method that utilizes disk striping to spread data across multiple drives to increase performance.

RAID 1 A data storage method that utilizes mirroring by duplicating data across two drives.

RAID 10 A data storage method that utilizes mirroring and striping of data across multiple drives.

RAID 4 A data storage method that utilizes striping with a parity bit on a separate drive, allowing the system to recover if a single data drive fails.

RAID 5 A data storage method that utilizes data striping with distributed parity, allowing the system to recover if any of the drives fails.

RAID 6 A data storage method that utilizes striping with double parity, allowing the system to recover if two drives fail.

Raw device A file created by the Linux kernel to directly reference data stored on a storage device.

Read The ability to access the data in a file or folder.

Redundant Array of Inexpensive Disks (RAID) A method of utilizing multiple drives to store data for fault tolerance and increased performance.

reiserFS An advanced Linux file system that utilizes journaling and advanced performance techniques. No longer supported by the Linux kernel.

Relative filepath A filepath that points to a file or directory relative to the current location.

Relative path A method of referencing file and directory names based on the current location of the shell.

renice a command to change the priority of a running program.

Repository A collection of software packages for a specific Linux distribution.

resize2fs A utility in the e2fsprog package for resizing ext file systems.

rm Command to remove a file from the Linux system.

rmdir Command to delete an existing empty directory.

rmmod Removes a device module from the kernel.

Root The base directory in the virtual directory.

Root directory The base of the Linux virtual directory.

Root drive The physical device that contains the core of the virtual directory.

Root user The default administrator account for Linux systems.

rpm The core Red Hat package manager program.

runlevels Administrative levels used by Linux systems to control which programs should be running.

Samba An open-source file sharing server that can interface with Windows workstations and servers.

scp The secure copy program which copies a file between systems using an encrypted protocol.

Secure Shell (SSH) A protocol for encrypting communication between two network servers.

Security context A policy for defining who or what has permissions to an object.

SELinux A package used mostly in Red Hat-based distributions for applying MAC-based permissions to users, files, and processes.

Sendmail The original Unix email server, sometimes used in the Linux environment.

Serial Advanced Technology Attachment (SATA) A storage device connection method that utilizes high speed serial data transfer.

Service account A user account that can run programs in background, but not log in at a command line or graphical desktop.

sftp A standard protocol for sending and receiving files from a remote server using encryption.

Shell The middleman between the kernel and the user.

Shell script A series of shell commands saved in a file that can be run as a program from the command line.

Simple Mail Transport Protocol (SMTP) A standard protocol for exchanging mail between two email servers.

Single-letter parameter A single letter option used to modify the behavior of a command.

Small Computer System Interface (SCSI) An advanced storage device connection method that allows multiple storage devices to connect to a single serial data connection.

SMB The Server Message Block, a network protocol developed by Microsoft and used for accessing network devices.

Snap Packaging system bundles all the files required for an application into a single snap distribution file.

snapd Application runs in background, and you use the snap command line tool to query the snap database to display installed snap packages, as well as to install, upgrade, and remove snap packages.

Software as a Service (SaaS) The cloud provides both a physical server and operating system environment.

Software package A collection of an application's executable files, library files, and configuration files bundled into one archive file.

Solid-state drive (SSD) A storage device that utilizes an integrated circuit to persistently store data.

ss A command line tool for displaying open network ports on the system, as well as the processes that are using them.

Standard input The default input device (usually the keyboard) in a virtual terminal.

Standard output The default output device (usually the monitor) in a virtual terminal.

su A program for changing your current login account to another account on the system. Commonly used for gaining root privileges on the system.

Sudo A program for running an application with root permissions.

sudoers A file for defining what users, aliases, or groups have the ability to use the sudo command.

Swap A Linux file system type that allows the system to utilize the drive partition as additional memory space.

Swap space Space on a hard disk allocated for storing the contents of virtual memory.

Symbolic link Two or more files that reference a single physical file.

Symbolic mode The method of specifying permissions using characters for files and folders.

sys directory Virtual directory that displays information about hardware connected to the system.

syslogd The legacy Linux program for logging events in log files.

system An initialization process created by Red Hat Linux that uses targets instead of runlevels.

systemd-journald The Systemd program for logging events in log files.

SysVinit The original Unix initialization process program ported to the Linux environment.

tar The Linux utility to archive files and directories.

Tarball Package uses the tar command to archive multiple files into a single file (either with or without compression).

Target Represents a group of services that should be running in the systemd initialization method.

Telnet A legacy program for connecting to a remote system using plain text that can be captured and viewed on the network.

Terminal emulation Provides a CLI contained within a window in a graphical desktop environment.

Thunderbird An open-source email client created by Mozilla.

touch Command to create an empty file or modify the access time on an existing file.

top A real-time display of running processes.

tune2fs A utility in the e2fsprogs package that allows you to change parameters of ext file systems.

Tunneling The ability to provide an encrypted connection between two servers that any application can use to send data.

udev A background process that monitors for connected devices and automatically generates /dev raw devices for them.

umount A command line utility for removing a partition file system from the Linux virtual directory structure.

Unified Extensible Firmware Interface (UEFI) Newer firmware to control how an IBM-compatible system starts.

Unit A service or action defined on a Systemd initialization system.

Unit files A configuration file that defines the programs to start when a specific event occurs.

Universal Disc Format (UDF) The Universal Disc Format, a file system used for storing data on optical DVD Rom drives.

Universal Serial Bus (USB) A protocol and hardware standard for connecting hardware to a computer system.

updated A command that runs in background to populate the locate database.

User accounts Uniquely identify individual users on the Linux system.

useradd A utility for adding new user accounts.

userdel A utility for deleting existing user accounts.

usermod A utility for modifying existing user accounts.

VFAT The Virtual File Allocation Table, a file system developed by Microsoft for use on Windows systems.

vgcreate A command line utility for creating volume groups as part of an LVM setup.

Virtual directory The method utilized by Linux systems to combine file systems from one or more partitions into a single directory structure.

Virtual File System (VFS) Provides a standard interface used by the Linux kernel to interface with different filesystems.

Virtual memory Memory reserved on a hard drive and treated as real memory.

Virtual terminal A CLI session that runs in memory on the Linux system.

Virtualization The ability to run multiple servers on a single hardware platform.

Wayland A modern X Window implementation for Linux that is more secure than the original X.org and easier to maintain.

whereis A command that looks for commands in specific folders on the system.

which A command that finds both external and built-in programs on the Linux system.

whois A command-line tool that connects to the centralized Internet registry to display information about a registered domain.

Write The permission for being able to modify a file or folder.

X Window A low-level program that works directly with the video card and monitor on a workstation, and controls how Linux applications interact with them.

X.org An older X Window implementation for Linux.

XFS The X File System, a file system developed by Silicon Graphics for use on their workstations and servers.

xfs_admin A command line utility for displaying and modifying information in an xfs file system.

xfs_info A command line utility for displaying information from an xfs file system.

xterm A generic terminal emulation package that works in multiple desktop environments.

Yum A command line package manager program used by Red Hat-based Linux distributions.

ZFS The Zettabyte File System, a file system developed by Sun Microsystems for its Unix workstations and servers.

Zypper The package management system used by openSUSE.

![An abstract image shows a texture in the form of smoke.](images/FM-opener.jpg)

© Picsfive/Shutterstock

# Index

NOTE: Page numbers followed by f and t indicate material in figures and tables respectively.

A

aa-complain command, [279](#9781284254884_CH11_02.xhtml_page_279)

aa-disable command, [279](#9781284254884_CH11_02.xhtml_page_279)

aa-enforce command, [279](#9781284254884_CH11_02.xhtml_page_279)

aa-status command, [277](#9781284254884_CH11_02.xhtml_page_277)–[278](#9781284254884_CH11_02.xhtml_page_278)

aa-unconfined command, [278](#9781284254884_CH11_02.xhtml_page_278)–[279](#9781284254884_CH11_02.xhtml_page_279)

absolute filepaths, [157](#9781284254884_CH07_01.xhtml_page_157)–[158](#9781284254884_CH07_01.xhtml_page_158)

absolute path, [106](#9781284254884_CH05_03.xhtml_page_106)

access control list (ACL), [244](#9781284254884_CH10_02.xhtml_page_244)–[246](#9781284254884_CH10_03.xhtml_page_246)

firewalls, [281](#9781284254884_CH11_03.xhtml_page_281)–[287](#9781284254884_CH11_04.xhtml_page_287)

administration user accounts, [233](#9781284254884_CH10_01.xhtml_page_233)–[234](#9781284254884_CH10_01.xhtml_page_234)

aliases, [255](#9781284254884_CH10_06.xhtml_page_255)

AllowTcpForwarding configuration, [256](#9781284254884_CH10_07.xhtml_page_256)

Apache web server, [28](#9781284254884_CH02_01.xhtml_page_28)

AppArmor MAC system, [265](#9781284254884_CH11.xhtml_page_265)

application containers, [41](#9781284254884_CH02_02.xhtml_page_41)–[42](#9781284254884_CH02_03.xhtml_page_42)

flatpak container, [44](#9781284254884_CH02_03.xhtml_page_44)–[45](#9781284254884_CH02_03.xhtml_page_45)

snap container, [42](#9781284254884_CH02_03.xhtml_page_42)–[43](#9781284254884_CH02_03.xhtml_page_43)

apropos, [129](#9781284254884_CH06_03.xhtml_page_129)

ash shell, [121](#9781284254884_CH06_01.xhtml_page_121)

asterisk glob character, [174](#9781284254884_CH07_05.xhtml_page_174), [175](#9781284254884_CH07_06.xhtml_page_175)

asymmetric encryption, [256](#9781284254884_CH10_07.xhtml_page_256)

at command, [223](#9781284254884_CH09_06.xhtml_page_223)–[226](#9781284254884_CH09_07.xhtml_page_226)

atq command, [225](#9781284254884_CH09_07.xhtml_page_225)–[226](#9781284254884_CH09_07.xhtml_page_226)

atrm command, [226](#9781284254884_CH09_07.xhtml_page_226)

audio cards, [59](#9781284254884_CH03_02.xhtml_page_59)

aulast command, [270](#9781284254884_CH11_01.xhtml_page_270)

B

bash shell, [17](#9781284254884_CH01_04.xhtml_page_17), [121](#9781284254884_CH06_01.xhtml_page_121)

Basic Input/Output System (BIOS), [76](#9781284254884_CH04_01.xhtml_page_76)–[77](#9781284254884_CH04_02.xhtml_page_77)

Berkeley Software Distribution (BSD), [249](#9781284254884_CH10_04.xhtml_page_249)

style parameters, [210](#9781284254884_CH09_01.xhtml_page_210)

bg command, [222](#9781284254884_CH09_06.xhtml_page_222)–[223](#9781284254884_CH09_06.xhtml_page_223)

BIOS. [Basic Input/Output System](#9781284254884_Index.xhtml_ie0026)

blkid tool, [111](#9781284254884_CH05_06.xhtml_page_111)

block device files, [8](#9781284254884_CH01_02.xhtml_page_8), [61](#9781284254884_CH03_02.xhtml_page_61)

bluetooth devices, [59](#9781284254884_CH03_02.xhtml_page_59)

boot loader program, [76](#9781284254884_CH04_01.xhtml_page_76), [77](#9781284254884_CH04_02.xhtml_page_77)

EXTLINUX, [83](#9781284254884_CH04_03.xhtml_page_83)

GRUB2, [78](#9781284254884_CH04_02.xhtml_page_78), [81](#9781284254884_CH04_03.xhtml_page_81)–[82](#9781284254884_CH04_03.xhtml_page_82)

GRUB Legacy, [78](#9781284254884_CH04_02.xhtml_page_78)–[81](#9781284254884_CH04_03.xhtml_page_81), [79](#9781284254884_CH04_03.xhtml_page_79)t

ISOLINUX, [83](#9781284254884_CH04_03.xhtml_page_83)

Linux Loader, [78](#9781284254884_CH04_02.xhtml_page_78)

MEMDISK, [83](#9781284254884_CH04_03.xhtml_page_83)

PXELINUX, [83](#9781284254884_CH04_03.xhtml_page_83)

SYSLINUX, [83](#9781284254884_CH04_03.xhtml_page_83)

boot manager, [77](#9781284254884_CH04_02.xhtml_page_77)

boot process

boot loader [(boot loader program)](#9781284254884_Index.xhtml_ie0033)

firmware startup

BIOS, [76](#9781284254884_CH04_01.xhtml_page_76)–[77](#9781284254884_CH04_02.xhtml_page_77)

UEFI, [77](#9781284254884_CH04_02.xhtml_page_77)–[78](#9781284254884_CH04_02.xhtml_page_78)

initialization process, [83](#9781284254884_CH04_03.xhtml_page_83)–[84](#9781284254884_CH04_04.xhtml_page_84)

systemd, [84](#9781284254884_CH04_04.xhtml_page_84), [87](#9781284254884_CH04_04.xhtml_page_87)–[92](#9781284254884_CH04_04.xhtml_page_92)

SysVinit, [84](#9781284254884_CH04_04.xhtml_page_84)–[87](#9781284254884_CH04_04.xhtml_page_87)

kernel ring buffer, [74](#9781284254884_CH04_01.xhtml_page_74)–[76](#9781284254884_CH04_01.xhtml_page_76)

procedural steps, [74](#9781284254884_CH04_01.xhtml_page_74)

Bourne shell, [17](#9781284254884_CH01_04.xhtml_page_17)

btrfs Linux file system, [106](#9781284254884_CH05_03.xhtml_page_106)

C

cat command, [61](#9781284254884_CH03_02.xhtml_page_61)

chage command, [236](#9781284254884_CH10_01.xhtml_page_236)

chainloading method, [77](#9781284254884_CH04_02.xhtml_page_77), [81](#9781284254884_CH04_03.xhtml_page_81)

change directory (cd) command, [157](#9781284254884_CH07_01.xhtml_page_157)

character device files, [8](#9781284254884_CH01_02.xhtml_page_8), [61](#9781284254884_CH03_02.xhtml_page_61)

chattr tool, [111](#9781284254884_CH05_06.xhtml_page_111)

chmod command, [142](#9781284254884_CH06_06.xhtml_page_142)

Chromium browser, [25](#9781284254884_CH02_01.xhtml_page_25)

Cinnamon desktop, [15](#9781284254884_CH01_04.xhtml_page_15), [15](#9781284254884_CH01_04.xhtml_page_15)f

CLI. [command line interface](#9781284254884_Index.xhtml_ie0051)

cloud computing, [292](#9781284254884_CH12_01.xhtml_page_292)–[293](#9781284254884_CH12_01.xhtml_page_293), [293](#9781284254884_CH12_01.xhtml_page_293)f

containers [(containers)](#9781284254884_Index.xhtml_ie0060)

IaaS model, [293](#9781284254884_CH12_01.xhtml_page_293), [294](#9781284254884_CH12_01.xhtml_page_294)f

PaaS model, [294](#9781284254884_CH12_01.xhtml_page_294)–[295](#9781284254884_CH12_01.xhtml_page_295), [295](#9781284254884_CH12_01.xhtml_page_295)f

SaaS model, [294](#9781284254884_CH12_01.xhtml_page_294), [294](#9781284254884_CH12_01.xhtml_page_294)f

virtualization, [295](#9781284254884_CH12_01.xhtml_page_295)–[298](#9781284254884_CH12_02.xhtml_page_298)

cold pluggable devices, [69](#9781284254884_CH03_04.xhtml_page_69)

command completion, [130](#9781284254884_CH06_03.xhtml_page_130)–[131](#9781284254884_CH06_03.xhtml_page_131)

command line interface (CLI), [17](#9781284254884_CH01_04.xhtml_page_17)–[18](#9781284254884_CH01_04.xhtml_page_18), [119](#9781284254884_CH06.xhtml_page_119), [120](#9781284254884_CH06_01.xhtml_page_120)

console, [123](#9781284254884_CH06_01.xhtml_page_123)

shell [(shells)](#9781284254884_Index.xhtml_ie0453)

terminal emulation package, [126](#9781284254884_CH06_02.xhtml_page_126)–[127](#9781284254884_CH06_02.xhtml_page_127), [127](#9781284254884_CH06_02.xhtml_page_127)f

virtual terminals, [124](#9781284254884_CH06_02.xhtml_page_124)–[126](#9781284254884_CH06_02.xhtml_page_126), [125](#9781284254884_CH06_02.xhtml_page_125)f

command-line tools

for network connections

DHCP client program, [196](#9781284254884_CH08_01.xhtml_page_196)–[197](#9781284254884_CH08_01.xhtml_page_197)

iproute2 package, [191](#9781284254884_CH08_01.xhtml_page_191)–[193](#9781284254884_CH08_01.xhtml_page_193), [192](#9781284254884_CH08_01.xhtml_page_192)t

net-tools package, [193](#9781284254884_CH08_01.xhtml_page_193)–[196](#9781284254884_CH08_01.xhtml_page_196)

Network Manager tool, [190](#9781284254884_CH08_01.xhtml_page_190)–[191](#9781284254884_CH08_01.xhtml_page_191), [190](#9781284254884_CH08_01.xhtml_page_190)f

command prompt, [17](#9781284254884_CH01_04.xhtml_page_17), [122](#9781284254884_CH06_01.xhtml_page_122)–[123](#9781284254884_CH06_01.xhtml_page_123), [124](#9781284254884_CH06_02.xhtml_page_124)t

command substitution, [145](#9781284254884_CH06_06.xhtml_page_145)–[146](#9781284254884_CH06_06.xhtml_page_146)

Common Unix Printing System (CUPS)

configuration, [249](#9781284254884_CH10_04.xhtml_page_249)–[250](#9781284254884_CH10_05.xhtml_page_250)

defined, [249](#9781284254884_CH10_04.xhtml_page_249)

LPD commands, [250](#9781284254884_CH10_05.xhtml_page_250), [251](#9781284254884_CH10_05.xhtml_page_251)t

web interface, [250](#9781284254884_CH10_05.xhtml_page_250), [250](#9781284254884_CH10_05.xhtml_page_250)f

compiled device driver, [52](#9781284254884_CH03_01.xhtml_page_52)

compressed directories, [179](#9781284254884_CH07_07.xhtml_page_179)

configuration, [29](#9781284254884_CH02_01.xhtml_page_29)

console, [123](#9781284254884_CH06_01.xhtml_page_123)

running programs without, [219](#9781284254884_CH09_04.xhtml_page_219)–[220](#9781284254884_CH09_05.xhtml_page_220)

containers

agent and agentless, [302](#9781284254884_CH12_04.xhtml_page_302)–[303](#9781284254884_CH12_04.xhtml_page_303)

application, [41](#9781284254884_CH02_02.xhtml_page_41)–[42](#9781284254884_CH02_03.xhtml_page_42)

flatpak container, [44](#9781284254884_CH02_03.xhtml_page_44)–[45](#9781284254884_CH02_03.xhtml_page_45)

snap container, [42](#9781284254884_CH02_03.xhtml_page_42)–[43](#9781284254884_CH02_03.xhtml_page_43)

application in, [299](#9781284254884_CH12_03.xhtml_page_299), [299](#9781284254884_CH12_03.xhtml_page_299)f

automated configuration management, [302](#9781284254884_CH12_04.xhtml_page_302)

creating, [300](#9781284254884_CH12_03.xhtml_page_300)

defined, [299](#9781284254884_CH12_03.xhtml_page_299)

design, [301](#9781284254884_CH12_04.xhtml_page_301)

DevOps, [304](#9781284254884_CH12_05.xhtml_page_304)–[306](#9781284254884_CH12_06.xhtml_page_306)

document, [301](#9781284254884_CH12_04.xhtml_page_301)

life cycle, [301](#9781284254884_CH12_04.xhtml_page_301), [302](#9781284254884_CH12_04.xhtml_page_302)f

monitoring, [303](#9781284254884_CH12_04.xhtml_page_303)

orchestration engines, [303](#9781284254884_CH12_04.xhtml_page_303)–[304](#9781284254884_CH12_05.xhtml_page_304)

software, [300](#9781284254884_CH12_03.xhtml_page_300)

templates, [300](#9781284254884_CH12_03.xhtml_page_300)

troubleshooting process, [301](#9781284254884_CH12_04.xhtml_page_301)

version control, [301](#9781284254884_CH12_04.xhtml_page_301)

control command, [69](#9781284254884_CH03_04.xhtml_page_69)

core Linux distribution, [18](#9781284254884_CH01_04.xhtml_page_18)–[19](#9781284254884_CH01_05.xhtml_page_19), [18](#9781284254884_CH01_04.xhtml_page_18)t

coreutils package, [11](#9781284254884_CH01_03.xhtml_page_11)

cp command, [168](#9781284254884_CH07_04.xhtml_page_168)–[171](#9781284254884_CH07_05.xhtml_page_171), [170](#9781284254884_CH07_05.xhtml_page_170)t

cron program, [226](#9781284254884_CH09_07.xhtml_page_226)–[228](#9781284254884_CH09_07.xhtml_page_228)

cron.service configuration file, [88](#9781284254884_CH04_04.xhtml_page_88)–[89](#9781284254884_CH04_04.xhtml_page_89)

crontab command, [227](#9781284254884_CH09_07.xhtml_page_227)

cryptsetup command, [279](#9781284254884_CH11_02.xhtml_page_279), [281](#9781284254884_CH11_03.xhtml_page_281)

CUPS. [Common Unix Printing System](#9781284254884_Index.xhtml_ie0055)

D

dash shell, [121](#9781284254884_CH06_01.xhtml_page_121)

database server, [28](#9781284254884_CH02_01.xhtml_page_28)

data collections, [28](#9781284254884_CH02_01.xhtml_page_28)

date and time management, [247](#9781284254884_CH10_04.xhtml_page_247)–[249](#9781284254884_CH10_04.xhtml_page_249)

date command, [132](#9781284254884_CH06_04.xhtml_page_132), [247](#9781284254884_CH10_04.xhtml_page_247)

Debian-based package management system, [30](#9781284254884_CH02_02.xhtml_page_30)

apt tool, [30](#9781284254884_CH02_02.xhtml_page_30)

installing software packages with, [33](#9781284254884_CH02_02.xhtml_page_33)–[35](#9781284254884_CH02_02.xhtml_page_35)

managing packages with, [31](#9781284254884_CH02_02.xhtml_page_31)–[33](#9781284254884_CH02_02.xhtml_page_33)

uninstalling software with, [37](#9781284254884_CH02_02.xhtml_page_37)–[38](#9781284254884_CH02_02.xhtml_page_38)

upgrading software with, [35](#9781284254884_CH02_02.xhtml_page_35)–[36](#9781284254884_CH02_02.xhtml_page_36)

dpkg command, [30](#9781284254884_CH02_02.xhtml_page_30)

debugfs tool, [111](#9781284254884_CH05_06.xhtml_page_111)

default command, [92](#9781284254884_CH04_04.xhtml_page_92)

default.target target, [7](#9781284254884_CH01_02.xhtml_page_7), [90](#9781284254884_CH04_04.xhtml_page_90)

dependencies, [29](#9781284254884_CH02_01.xhtml_page_29)

desktop applications, [24](#9781284254884_CH02_01.xhtml_page_24)

email client, [25](#9781284254884_CH02_01.xhtml_page_25)–[26](#9781284254884_CH02_01.xhtml_page_26), [27](#9781284254884_CH02_01.xhtml_page_27)f

file management, [26](#9781284254884_CH02_01.xhtml_page_26), [27](#9781284254884_CH02_01.xhtml_page_27)f

office productivity, [24](#9781284254884_CH02_01.xhtml_page_24), [25](#9781284254884_CH02_01.xhtml_page_25)f

web browser, [25](#9781284254884_CH02_01.xhtml_page_25), [26](#9781284254884_CH02_01.xhtml_page_26)f

/dev directory, [60](#9781284254884_CH03_02.xhtml_page_60)–[61](#9781284254884_CH03_02.xhtml_page_61)

/dev/disk/by-id directory, [98](#9781284254884_CH05_01.xhtml_page_98)

/dev/disk/by-label directory, [98](#9781284254884_CH05_01.xhtml_page_98)

/dev/disk/by-path directory, [98](#9781284254884_CH05_01.xhtml_page_98)

/dev/disk/by-uuid directory, [99](#9781284254884_CH05_01.xhtml_page_99)

device driver

compiled, [52](#9781284254884_CH03_01.xhtml_page_52)

defined, [52](#9781284254884_CH03_01.xhtml_page_52)

modules, [53](#9781284254884_CH03_01.xhtml_page_53)

installing new, [55](#9781284254884_CH03_01.xhtml_page_55)–[58](#9781284254884_CH03_01.xhtml_page_58)

listing installed, [53](#9781284254884_CH03_01.xhtml_page_53)–[55](#9781284254884_CH03_01.xhtml_page_55)

removing modules, [58](#9781284254884_CH03_01.xhtml_page_58)

device files, [8](#9781284254884_CH01_02.xhtml_page_8)–[9](#9781284254884_CH01_02.xhtml_page_9)

device interfaces

GPIO interface, [59](#9781284254884_CH03_02.xhtml_page_59)–[60](#9781284254884_CH03_02.xhtml_page_60)

PCI, [58](#9781284254884_CH03_01.xhtml_page_58)–[59](#9781284254884_CH03_02.xhtml_page_59)

USB, [59](#9781284254884_CH03_02.xhtml_page_59)–[60](#9781284254884_CH03_02.xhtml_page_60)

Device Mapper Multipathing (DM-multipathing), [112](#9781284254884_CH05_06.xhtml_page_112)–[113](#9781284254884_CH05_07.xhtml_page_113)

/dev/mapper device file directory, [112](#9781284254884_CH05_06.xhtml_page_112)

DevOps, [304](#9781284254884_CH12_05.xhtml_page_304)–[306](#9781284254884_CH12_06.xhtml_page_306)

df tool, [111](#9781284254884_CH05_06.xhtml_page_111)

dig command, [200](#9781284254884_CH08_02.xhtml_page_200)–[201](#9781284254884_CH08_02.xhtml_page_201)

direct memory access (DMA) channels, [63](#9781284254884_CH03_02.xhtml_page_63)

directory handling, in files, [166](#9781284254884_CH07_03.xhtml_page_166)–[168](#9781284254884_CH07_04.xhtml_page_168)

discretionary access control (DAC) methods, [272](#9781284254884_CH11_01.xhtml_page_272)

disk management

automatic drive detection, [98](#9781284254884_CH05_01.xhtml_page_98)–[99](#9781284254884_CH05_01.xhtml_page_99)

drive connections, [97](#9781284254884_CH05_01.xhtml_page_97)

file system [(file system)](#9781284254884_Index.xhtml_ie0151)

overview of, [95](#9781284254884_CH05.xhtml_page_95)–[96](#9781284254884_CH05.xhtml_page_96)

partitioning drives, [98](#9781284254884_CH05_01.xhtml_page_98)

partitioning tools

fdisk command, [99](#9781284254884_CH05_01.xhtml_page_99)–[100](#9781284254884_CH05_02.xhtml_page_100), [100](#9781284254884_CH05_02.xhtml_page_100)t

gdisk program, [101](#9781284254884_CH05_02.xhtml_page_101), [102](#9781284254884_CH05_02.xhtml_page_102)t

GNU parted program, [101](#9781284254884_CH05_02.xhtml_page_101)–[102](#9781284254884_CH05_02.xhtml_page_102)

graphical tools, [103](#9781284254884_CH05_02.xhtml_page_103)

storage devices

Logical Volume Manager, [113](#9781284254884_CH05_07.xhtml_page_113)–[114](#9781284254884_CH05_07.xhtml_page_114), [113](#9781284254884_CH05_07.xhtml_page_113)f

multipath device, [112](#9781284254884_CH05_06.xhtml_page_112)–[113](#9781284254884_CH05_07.xhtml_page_113)

RAID technology, [114](#9781284254884_CH05_07.xhtml_page_114)

distribution

core Linux distribution, [18](#9781284254884_CH01_04.xhtml_page_18)–[19](#9781284254884_CH01_05.xhtml_page_19), [18](#9781284254884_CH01_04.xhtml_page_18)t

defined, [18](#9781284254884_CH01_04.xhtml_page_18)

derivative Linux, [19](#9781284254884_CH01_05.xhtml_page_19)–[20](#9781284254884_CH01_05.xhtml_page_20), [19](#9781284254884_CH01_05.xhtml_page_19)t

DLL hell, [299](#9781284254884_CH12_03.xhtml_page_299)

dmesg command, [74](#9781284254884_CH04_01.xhtml_page_74)–[76](#9781284254884_CH04_01.xhtml_page_76)

dm-multipath tool, [112](#9781284254884_CH05_06.xhtml_page_112)

Docker container package, [300](#9781284254884_CH12_03.xhtml_page_300)

Docker Swarm, [304](#9781284254884_CH12_05.xhtml_page_304)

document container, [301](#9781284254884_CH12_04.xhtml_page_301)

documents, [28](#9781284254884_CH02_01.xhtml_page_28)

Dolphin file manager, [26](#9781284254884_CH02_01.xhtml_page_26)

dpkg package management system, [30](#9781284254884_CH02_02.xhtml_page_30)

drive letters, [95](#9781284254884_CH05.xhtml_page_95)

driver code, [8](#9781284254884_CH01_02.xhtml_page_8)

dumpe2fs tool, [111](#9781284254884_CH05_06.xhtml_page_111)

du tool, [111](#9781284254884_CH05_06.xhtml_page_111)

Dynamic Host Configuration Protocol (DHCP) client program, [196](#9781284254884_CH08_01.xhtml_page_196)–[197](#9781284254884_CH08_01.xhtml_page_197)

E

echo command, [137](#9781284254884_CH06_05.xhtml_page_137), [138](#9781284254884_CH06_05.xhtml_page_138), [143](#9781284254884_CH06_06.xhtml_page_143)–[144](#9781284254884_CH06_06.xhtml_page_144)

ecryptfs Linux file system, [106](#9781284254884_CH05_03.xhtml_page_106)–[107](#9781284254884_CH05_04.xhtml_page_107)

EFI System Partition (ESP), [77](#9781284254884_CH04_02.xhtml_page_77)

e2fsprogs package, [111](#9781284254884_CH05_06.xhtml_page_111)

e2label tool, [111](#9781284254884_CH05_06.xhtml_page_111)

email administration, [251](#9781284254884_CH10_05.xhtml_page_251)

architecture, [252](#9781284254884_CH10_06.xhtml_page_252)–[253](#9781284254884_CH10_06.xhtml_page_253), [253](#9781284254884_CH10_06.xhtml_page_253)f

client packages, [253](#9781284254884_CH10_06.xhtml_page_253)–[254](#9781284254884_CH10_06.xhtml_page_254), [254](#9781284254884_CH10_06.xhtml_page_254)f

redirecting mail delivery, [255](#9781284254884_CH10_06.xhtml_page_255)

server programs, [253](#9781284254884_CH10_06.xhtml_page_253), [253](#9781284254884_CH10_06.xhtml_page_253)t

email client, [25](#9781284254884_CH02_01.xhtml_page_25)–[26](#9781284254884_CH02_01.xhtml_page_26), [27](#9781284254884_CH02_01.xhtml_page_27)f, [253](#9781284254884_CH10_06.xhtml_page_253)–[254](#9781284254884_CH10_06.xhtml_page_254), [254](#9781284254884_CH10_06.xhtml_page_254)f

email server, [29](#9781284254884_CH02_01.xhtml_page_29), [253](#9781284254884_CH10_06.xhtml_page_253), [253](#9781284254884_CH10_06.xhtml_page_253)t

environment variables, [136](#9781284254884_CH06_05.xhtml_page_136)

global, [136](#9781284254884_CH06_05.xhtml_page_136)–[138](#9781284254884_CH06_05.xhtml_page_138), [140](#9781284254884_CH06_05.xhtml_page_140)

local, [138](#9781284254884_CH06_05.xhtml_page_138)–[140](#9781284254884_CH06_05.xhtml_page_140)

removing, [140](#9781284254884_CH06_05.xhtml_page_140)–[141](#9781284254884_CH06_05.xhtml_page_141)

escaping files, [176](#9781284254884_CH07_06.xhtml_page_176)

/etc/bashrc file, [122](#9781284254884_CH06_01.xhtml_page_122)

/etc/crypttab file, [110](#9781284254884_CH05_05.xhtml_page_110)

/etc/fstab file, [109](#9781284254884_CH05_05.xhtml_page_109)–[110](#9781284254884_CH05_05.xhtml_page_110)

/etc/mstab file, [110](#9781284254884_CH05_05.xhtml_page_110)

/etc/passwd file, [121](#9781284254884_CH06_01.xhtml_page_121)

ethtool command, [193](#9781284254884_CH08_01.xhtml_page_193)–[194](#9781284254884_CH08_01.xhtml_page_194)

Evolution email client, [25](#9781284254884_CH02_01.xhtml_page_25)

execute permission, [239](#9781284254884_CH10_02.xhtml_page_239), [240](#9781284254884_CH10_02.xhtml_page_240), [242](#9781284254884_CH10_02.xhtml_page_242)

eXim, [29](#9781284254884_CH02_01.xhtml_page_29)

export command, [140](#9781284254884_CH06_05.xhtml_page_140)

extended partitions, [98](#9781284254884_CH05_01.xhtml_page_98)

Extensible Firmware Interface (EFI), [77](#9781284254884_CH04_02.xhtml_page_77)

external commands, [120](#9781284254884_CH06_01.xhtml_page_120)

external hard drives, [59](#9781284254884_CH03_02.xhtml_page_59)

EXTLINUX boot loader program, [83](#9781284254884_CH04_03.xhtml_page_83)

ext3 Linux file system, [107](#9781284254884_CH05_04.xhtml_page_107)

ext4 Linux file system, [107](#9781284254884_CH05_04.xhtml_page_107)

F

FAT32, [95](#9781284254884_CH05.xhtml_page_95)

fdisk command, [99](#9781284254884_CH05_01.xhtml_page_99)–[100](#9781284254884_CH05_02.xhtml_page_100), [100](#9781284254884_CH05_02.xhtml_page_100)t

fg command, [223](#9781284254884_CH09_06.xhtml_page_223)

FHS. [file system hierarchy standard (FHS)](#9781284254884_Index.xhtml_ie0152)

File Allocation Table (FAT), [77](#9781284254884_CH04_02.xhtml_page_77)

file command, [159](#9781284254884_CH07_02.xhtml_page_159)

file compression, [179](#9781284254884_CH07_07.xhtml_page_179)–[180](#9781284254884_CH07_08.xhtml_page_180), [180](#9781284254884_CH07_08.xhtml_page_180)t

file handling

copying files, [168](#9781284254884_CH07_04.xhtml_page_168)–[171](#9781284254884_CH07_05.xhtml_page_171)

creating files, [168](#9781284254884_CH07_04.xhtml_page_168)

deleting files, [173](#9781284254884_CH07_05.xhtml_page_173)–[174](#9781284254884_CH07_05.xhtml_page_174)

links, [171](#9781284254884_CH07_05.xhtml_page_171)–[172](#9781284254884_CH07_05.xhtml_page_172)

renaming files, [172](#9781284254884_CH07_05.xhtml_page_172)–[173](#9781284254884_CH07_05.xhtml_page_173)

file links, [171](#9781284254884_CH07_05.xhtml_page_171)–[172](#9781284254884_CH07_05.xhtml_page_172)

file management, [26](#9781284254884_CH02_01.xhtml_page_26), [27](#9781284254884_CH02_01.xhtml_page_27)f

archiving files, [179](#9781284254884_CH07_07.xhtml_page_179)–[182](#9781284254884_CH07_08.xhtml_page_182)

directory handling, [166](#9781284254884_CH07_03.xhtml_page_166)–[168](#9781284254884_CH07_04.xhtml_page_168)

directory listing and, [162](#9781284254884_CH07_03.xhtml_page_162)–[166](#9781284254884_CH07_03.xhtml_page_166)

directory structure, [154](#9781284254884_CH07_01.xhtml_page_154)

features

case sensitivity, [176](#9781284254884_CH07_06.xhtml_page_176)

quoting, [175](#9781284254884_CH07_06.xhtml_page_175)–[176](#9781284254884_CH07_06.xhtml_page_176)

wildcards, [174](#9781284254884_CH07_05.xhtml_page_174)–[175](#9781284254884_CH07_06.xhtml_page_175)

file type determination, [158](#9781284254884_CH07_01.xhtml_page_158)–[159](#9781284254884_CH07_02.xhtml_page_159)

find command, [178](#9781284254884_CH07_07.xhtml_page_178)–[179](#9781284254884_CH07_07.xhtml_page_179), [179](#9781284254884_CH07_07.xhtml_page_179)t

hidden files, [159](#9781284254884_CH07_02.xhtml_page_159)–[161](#9781284254884_CH07_02.xhtml_page_161), [160](#9781284254884_CH07_02.xhtml_page_160)f

inodes, [161](#9781284254884_CH07_02.xhtml_page_161)

Linux filesystem hierarchy standard, [156](#9781284254884_CH07_01.xhtml_page_156), [156](#9781284254884_CH07_01.xhtml_page_156)t

locate command, [177](#9781284254884_CH07_07.xhtml_page_177)–[178](#9781284254884_CH07_07.xhtml_page_178)

names, [159](#9781284254884_CH07_02.xhtml_page_159)

structure, [155](#9781284254884_CH07_01.xhtml_page_155)f, [155](#9781284254884_CH07_01.xhtml_page_155)f

traversing directories, [157](#9781284254884_CH07_01.xhtml_page_157)–[158](#9781284254884_CH07_01.xhtml_page_158)

whereis command, [178](#9781284254884_CH07_07.xhtml_page_178)

which command, [177](#9781284254884_CH07_07.xhtml_page_177)

Files file manager, [26](#9781284254884_CH02_01.xhtml_page_26), [27](#9781284254884_CH02_01.xhtml_page_27)f

file system, [100](#9781284254884_CH05_02.xhtml_page_100), [103](#9781284254884_CH05_02.xhtml_page_103)–[104](#9781284254884_CH05_03.xhtml_page_104)

creating, [108](#9781284254884_CH05_04.xhtml_page_108)

defined, [9](#9781284254884_CH01_02.xhtml_page_9)

Linux, [106](#9781284254884_CH05_03.xhtml_page_106)–[107](#9781284254884_CH05_04.xhtml_page_107)

management, [9](#9781284254884_CH01_02.xhtml_page_9), [10](#9781284254884_CH01_03.xhtml_page_10)t, [110](#9781284254884_CH05_05.xhtml_page_110)–[112](#9781284254884_CH05_06.xhtml_page_112)

mounting, [108](#9781284254884_CH05_04.xhtml_page_108)–[110](#9781284254884_CH05_05.xhtml_page_110)

non-Linux, [107](#9781284254884_CH05_04.xhtml_page_107)–[108](#9781284254884_CH05_04.xhtml_page_108)

virtual directory, [104](#9781284254884_CH05_03.xhtml_page_104)–[106](#9781284254884_CH05_03.xhtml_page_106), [105](#9781284254884_CH05_03.xhtml_page_105)f

file system hierarchy standard (FHS), [105](#9781284254884_CH05_03.xhtml_page_105), [105](#9781284254884_CH05_03.xhtml_page_105)t, [156](#9781284254884_CH07_01.xhtml_page_156), [156](#9781284254884_CH07_01.xhtml_page_156)t

find command, [178](#9781284254884_CH07_07.xhtml_page_178)–[179](#9781284254884_CH07_07.xhtml_page_179), [179](#9781284254884_CH07_07.xhtml_page_179)t

Firefox, [25](#9781284254884_CH02_01.xhtml_page_25)

firewalld program, [281](#9781284254884_CH11_03.xhtml_page_281)–[287](#9781284254884_CH11_04.xhtml_page_287), [283](#9781284254884_CH11_04.xhtml_page_283)t

firewalls, network security using, [281](#9781284254884_CH11_03.xhtml_page_281)

ACL rules, [285](#9781284254884_CH11_04.xhtml_page_285)–[287](#9781284254884_CH11_04.xhtml_page_287)

Red Hat server, [281](#9781284254884_CH11_03.xhtml_page_281)–[283](#9781284254884_CH11_04.xhtml_page_283), [282](#9781284254884_CH11_04.xhtml_page_282)f

status, [283](#9781284254884_CH11_04.xhtml_page_283)–[284](#9781284254884_CH11_04.xhtml_page_284)

zones, [284](#9781284254884_CH11_04.xhtml_page_284)–[285](#9781284254884_CH11_04.xhtml_page_285)

flatpak application container, [44](#9781284254884_CH02_03.xhtml_page_44)–[45](#9781284254884_CH02_03.xhtml_page_45)

Fluxbox desktops, [16](#9781284254884_CH01_04.xhtml_page_16)t

for command, [148](#9781284254884_CH06_06.xhtml_page_148)

forwarding email, [255](#9781284254884_CH10_06.xhtml_page_255)

fsck program, [111](#9781284254884_CH05_06.xhtml_page_111)–[112](#9781284254884_CH05_06.xhtml_page_112)

full-word parameters, [164](#9781284254884_CH07_03.xhtml_page_164), [164](#9781284254884_CH07_03.xhtml_page_164)t–165t

fvwm desktop, [16](#9781284254884_CH01_04.xhtml_page_16)t

fvwm95 desktop, [16](#9781284254884_CH01_04.xhtml_page_16)t

G

gcc package, [48](#9781284254884_CH02_04.xhtml_page_48)

gdisk command, [101](#9781284254884_CH05_02.xhtml_page_101), [102](#9781284254884_CH05_02.xhtml_page_102)t

general purpose input/output (GPIO) interface, [60](#9781284254884_CH03_02.xhtml_page_60)

getfacl command, [245](#9781284254884_CH10_03.xhtml_page_245)

getsebool command, [276](#9781284254884_CH11_02.xhtml_page_276), [277](#9781284254884_CH11_02.xhtml_page_277)

Ghostscript program, [251](#9781284254884_CH10_05.xhtml_page_251)

global environment variable, [136](#9781284254884_CH06_05.xhtml_page_136)–[138](#9781284254884_CH06_05.xhtml_page_138), [140](#9781284254884_CH06_05.xhtml_page_140)

globbing technique, [174](#9781284254884_CH07_05.xhtml_page_174)

GNOME desktop. [GNU Network Object Model Environment desktop](#9781284254884_Index.xhtml_ie0176)

GNOME Terminal package, [126](#9781284254884_CH06_02.xhtml_page_126)

GNU IceCat browser, [25](#9781284254884_CH02_01.xhtml_page_25)

GNU Network Object Model Environment (GNOME) desktop, [13](#9781284254884_CH01_04.xhtml_page_13)–[15](#9781284254884_CH01_04.xhtml_page_15), [14](#9781284254884_CH01_04.xhtml_page_14)f, [14](#9781284254884_CH01_04.xhtml_page_14)t

GNU Privacy Guard (GPG) package, [258](#9781284254884_CH10_07.xhtml_page_258)–[259](#9781284254884_CH10_07.xhtml_page_259)

GNU's Not Unix (GNU) utilities, [10](#9781284254884_CH01_03.xhtml_page_10)–[11](#9781284254884_CH01_03.xhtml_page_11)

long parameters, [210](#9781284254884_CH09_01.xhtml_page_210)

parted program, [101](#9781284254884_CH05_02.xhtml_page_101)–[102](#9781284254884_CH05_02.xhtml_page_102)

gparted window, [103](#9781284254884_CH05_02.xhtml_page_103), [103](#9781284254884_CH05_02.xhtml_page_103)f

Grand Unified Boot Loader (GRUB) Legacy, [78](#9781284254884_CH04_02.xhtml_page_78)–[81](#9781284254884_CH04_03.xhtml_page_81), [79](#9781284254884_CH04_03.xhtml_page_79)t

graphical desktops, [16](#9781284254884_CH01_04.xhtml_page_16)t

graphical.target target, [7](#9781284254884_CH01_02.xhtml_page_7), [90](#9781284254884_CH04_04.xhtml_page_90)

grep command, [129](#9781284254884_CH06_03.xhtml_page_129), [130](#9781284254884_CH06_03.xhtml_page_130)f

group permissions, [240](#9781284254884_CH10_02.xhtml_page_240)

groups, [235](#9781284254884_CH10_01.xhtml_page_235)–[236](#9781284254884_CH10_01.xhtml_page_236)

groups command, [268](#9781284254884_CH11_01.xhtml_page_268), [269](#9781284254884_CH11_01.xhtml_page_269)

GRUB2 boot loader, [78](#9781284254884_CH04_02.xhtml_page_78), [81](#9781284254884_CH04_03.xhtml_page_81)–[82](#9781284254884_CH04_03.xhtml_page_82)

grub-install command, [80](#9781284254884_CH04_03.xhtml_page_80)–[81](#9781284254884_CH04_03.xhtml_page_81)

GRUB Legacy. [Grand Unified Boot Loader Legacy](#9781284254884_Index.xhtml_ie0180)

GUID Partition Table (GPT) method, [77](#9781284254884_CH04_02.xhtml_page_77), [98](#9781284254884_CH05_01.xhtml_page_98)

gzip command, [180](#9781284254884_CH07_08.xhtml_page_180)

H

halt command, [87](#9781284254884_CH04_04.xhtml_page_87)

hard disk drive (HDD), [97](#9781284254884_CH05_01.xhtml_page_97)

hard link, [171](#9781284254884_CH07_05.xhtml_page_171)

hardware devices, [58](#9781284254884_CH03_01.xhtml_page_58)

/dev directory, [60](#9781284254884_CH03_02.xhtml_page_60)–[61](#9781284254884_CH03_02.xhtml_page_61)

device driver [(device driver)](#9781284254884_Index.xhtml_ie0086)

direct memory access, [63](#9781284254884_CH03_02.xhtml_page_63)

dmesg command, [66](#9781284254884_CH03_03.xhtml_page_66)–[67](#9781284254884_CH03_03.xhtml_page_67)

GPIO interface, [59](#9781284254884_CH03_02.xhtml_page_59)–[60](#9781284254884_CH03_02.xhtml_page_60)

hot pluggable devices, [69](#9781284254884_CH03_04.xhtml_page_69)–[70](#9781284254884_CH03_04.xhtml_page_70)

interrupt requests, [61](#9781284254884_CH03_02.xhtml_page_61)–[62](#9781284254884_CH03_02.xhtml_page_62)

I/O ports, [62](#9781284254884_CH03_02.xhtml_page_62)–[63](#9781284254884_CH03_02.xhtml_page_63)

lsblk command, [65](#9781284254884_CH03_03.xhtml_page_65)

lsdev command, [64](#9781284254884_CH03_02.xhtml_page_64)–[65](#9781284254884_CH03_03.xhtml_page_65)

PCI, [58](#9781284254884_CH03_01.xhtml_page_58)–[59](#9781284254884_CH03_02.xhtml_page_59), [67](#9781284254884_CH03_03.xhtml_page_67)–[68](#9781284254884_CH03_03.xhtml_page_68)

/proc directory, [61](#9781284254884_CH03_02.xhtml_page_61)

/sys directory, [63](#9781284254884_CH03_02.xhtml_page_63)–[64](#9781284254884_CH03_02.xhtml_page_64)

USB devices, [59](#9781284254884_CH03_02.xhtml_page_59)–[60](#9781284254884_CH03_02.xhtml_page_60), [68](#9781284254884_CH03_03.xhtml_page_68)

hardware management, [8](#9781284254884_CH01_02.xhtml_page_8)–[9](#9781284254884_CH01_02.xhtml_page_9)

help command, [128](#9781284254884_CH06_03.xhtml_page_128)–[129](#9781284254884_CH06_03.xhtml_page_129), [128](#9781284254884_CH06_03.xhtml_page_128)f

hidden files, [159](#9781284254884_CH07_02.xhtml_page_159)–[161](#9781284254884_CH07_02.xhtml_page_161), [160](#9781284254884_CH07_02.xhtml_page_160)f

Hierarchical File System (HFS), [107](#9781284254884_CH05_04.xhtml_page_107)

history file, [130](#9781284254884_CH06_03.xhtml_page_130)

/home directory, [104](#9781284254884_CH05_03.xhtml_page_104)

host address, [186](#9781284254884_CH08_01.xhtml_page_186)

host command, [199](#9781284254884_CH08_02.xhtml_page_199)–[200](#9781284254884_CH08_02.xhtml_page_200)

hot pluggable devices, [69](#9781284254884_CH03_04.xhtml_page_69)–[70](#9781284254884_CH03_04.xhtml_page_70)

hybrid cloud computing, [292](#9781284254884_CH12_01.xhtml_page_292)

hypervisor, [296](#9781284254884_CH12_02.xhtml_page_296)–[297](#9781284254884_CH12_02.xhtml_page_297)

templates, [298](#9781284254884_CH12_02.xhtml_page_298)

Type I, [297](#9781284254884_CH12_02.xhtml_page_297), [297](#9781284254884_CH12_02.xhtml_page_297)f

Type II, [297](#9781284254884_CH12_02.xhtml_page_297)–[298](#9781284254884_CH12_02.xhtml_page_298), [298](#9781284254884_CH12_02.xhtml_page_298)f

I

IaaS model. [Infrastructure as a Service model](#9781284254884_Index.xhtml_ie0211)

ifconfig command, [194](#9781284254884_CH08_01.xhtml_page_194)–[195](#9781284254884_CH08_01.xhtml_page_195)

if-then condition statement, [146](#9781284254884_CH06_06.xhtml_page_146)–[148](#9781284254884_CH06_06.xhtml_page_148)

info program, [129](#9781284254884_CH06_03.xhtml_page_129)

Infrastructure as a Service (IaaS) model, [293](#9781284254884_CH12_01.xhtml_page_293), [294](#9781284254884_CH12_01.xhtml_page_294)f

initialization process

defined, [83](#9781284254884_CH04_03.xhtml_page_83)

systemd, [84](#9781284254884_CH04_04.xhtml_page_84), [87](#9781284254884_CH04_04.xhtml_page_87)–[92](#9781284254884_CH04_04.xhtml_page_92)

SysVinit, [84](#9781284254884_CH04_04.xhtml_page_84)–[87](#9781284254884_CH04_04.xhtml_page_87)

init process, [6](#9781284254884_CH01_02.xhtml_page_6), [210](#9781284254884_CH09_01.xhtml_page_210)

init program, [83](#9781284254884_CH04_03.xhtml_page_83)

initrd command, [80](#9781284254884_CH04_03.xhtml_page_80)

inline input redirection, [133](#9781284254884_CH06_04.xhtml_page_133)

inode number, [161](#9781284254884_CH07_02.xhtml_page_161)

inodes, [161](#9781284254884_CH07_02.xhtml_page_161)

inode table, [161](#9781284254884_CH07_02.xhtml_page_161)

input redirection, [132](#9781284254884_CH06_04.xhtml_page_132)–[133](#9781284254884_CH06_04.xhtml_page_133)

insmod command, [55](#9781284254884_CH03_01.xhtml_page_55)–[57](#9781284254884_CH03_01.xhtml_page_57)

internal commands, [120](#9781284254884_CH06_01.xhtml_page_120)

internal hard drives, [59](#9781284254884_CH03_02.xhtml_page_59)

Internet Control Message Protocol (ICMP), [197](#9781284254884_CH08_01.xhtml_page_197)

Internet Printing Protocol (IPP), [249](#9781284254884_CH10_04.xhtml_page_249)

interrupt requests (IRQs), [61](#9781284254884_CH03_02.xhtml_page_61)–[62](#9781284254884_CH03_02.xhtml_page_62)

I/O ports, [62](#9781284254884_CH03_02.xhtml_page_62)–[63](#9781284254884_CH03_02.xhtml_page_63)

iostat tool, [111](#9781284254884_CH05_06.xhtml_page_111)

ip command, [191](#9781284254884_CH08_01.xhtml_page_191)–[193](#9781284254884_CH08_01.xhtml_page_193), [192](#9781284254884_CH08_01.xhtml_page_192)t

iproute2 package, [191](#9781284254884_CH08_01.xhtml_page_191)–[193](#9781284254884_CH08_01.xhtml_page_193), [192](#9781284254884_CH08_01.xhtml_page_192)t

IRQs. [interrupt requests](#9781284254884_Index.xhtml_ie0226)

ISO image file, [19](#9781284254884_CH01_05.xhtml_page_19)

isolate command, [92](#9781284254884_CH04_04.xhtml_page_92)

ISOLINUX boot loader program, [83](#9781284254884_CH04_03.xhtml_page_83)

ISO-9660 standard, [107](#9781284254884_CH05_04.xhtml_page_107)

iwconfig command, [196](#9781284254884_CH08_01.xhtml_page_196)

J

job control, [220](#9781284254884_CH09_05.xhtml_page_220)–[223](#9781284254884_CH09_06.xhtml_page_223)

jobs command, [220](#9781284254884_CH09_05.xhtml_page_220)–[223](#9781284254884_CH09_06.xhtml_page_223), [221](#9781284254884_CH09_06.xhtml_page_221)t

Joe's Window Manager (JWM) desktop, [16](#9781284254884_CH01_04.xhtml_page_16)t

journalctl program, [261](#9781284254884_CH10_08.xhtml_page_261)

journaling, [107](#9781284254884_CH05_04.xhtml_page_107)

K

KDE Plasma desktop, [12](#9781284254884_CH01_04.xhtml_page_12)–[13](#9781284254884_CH01_04.xhtml_page_13), [12](#9781284254884_CH01_04.xhtml_page_12)f, [13](#9781284254884_CH01_04.xhtml_page_13)t, [15](#9781284254884_CH01_04.xhtml_page_15)

K Desktop Environment (KDE), [12](#9781284254884_CH01_04.xhtml_page_12)

applications, [13](#9781284254884_CH01_04.xhtml_page_13)t

Plasma desktop, [12](#9781284254884_CH01_04.xhtml_page_12)–[13](#9781284254884_CH01_04.xhtml_page_13), [12](#9781284254884_CH01_04.xhtml_page_12)f, [13](#9781284254884_CH01_04.xhtml_page_13)t, [15](#9781284254884_CH01_04.xhtml_page_15)

kernel, [3](#9781284254884_CH01_02.xhtml_page_3)

filesystem management, [9](#9781284254884_CH01_02.xhtml_page_9), [10](#9781284254884_CH01_03.xhtml_page_10)t

GNU utilities, [10](#9781284254884_CH01_03.xhtml_page_10)–[11](#9781284254884_CH01_03.xhtml_page_11)

hardware management, [8](#9781284254884_CH01_02.xhtml_page_8)–[9](#9781284254884_CH01_02.xhtml_page_9)

memory management, [3](#9781284254884_CH01_02.xhtml_page_3)–[5](#9781284254884_CH01_02.xhtml_page_5), [4](#9781284254884_CH01_02.xhtml_page_4)f

software program management, [6](#9781284254884_CH01_02.xhtml_page_6)–[8](#9781284254884_CH01_02.xhtml_page_8)

Kernel-based Virtual Machine (KVM), [297](#9781284254884_CH12_02.xhtml_page_297)

kernel command, [80](#9781284254884_CH04_03.xhtml_page_80)

kernel module, [8](#9781284254884_CH01_02.xhtml_page_8), [53](#9781284254884_CH03_01.xhtml_page_53)

installing new, [55](#9781284254884_CH03_01.xhtml_page_55)–[58](#9781284254884_CH03_01.xhtml_page_58)

listing installed, [53](#9781284254884_CH03_01.xhtml_page_53)–[55](#9781284254884_CH03_01.xhtml_page_55)

removing modules, [58](#9781284254884_CH03_01.xhtml_page_58)

kernel ring buffer, [74](#9781284254884_CH04_01.xhtml_page_74)–[76](#9781284254884_CH04_01.xhtml_page_76)

key mode, [257](#9781284254884_CH10_07.xhtml_page_257), [258](#9781284254884_CH10_07.xhtml_page_258)

kill command, [215](#9781284254884_CH09_03.xhtml_page_215)–[216](#9781284254884_CH09_03.xhtml_page_216)

KMail email client, [25](#9781284254884_CH02_01.xhtml_page_25)–[26](#9781284254884_CH02_01.xhtml_page_26)

Konsole package, [126](#9781284254884_CH06_02.xhtml_page_126)

kpartx tool, [112](#9781284254884_CH05_06.xhtml_page_112)

ksh shell, [121](#9781284254884_CH06_01.xhtml_page_121)

Kubernetes, [303](#9781284254884_CH12_04.xhtml_page_303)–[304](#9781284254884_CH12_05.xhtml_page_304)

L

LibreOffice, [24](#9781284254884_CH02_01.xhtml_page_24), [25](#9781284254884_CH02_01.xhtml_page_25)

Lighttpd web server, [28](#9781284254884_CH02_01.xhtml_page_28)

Line Printer Daemon (LPD) print method, [249](#9781284254884_CH10_04.xhtml_page_249), [250](#9781284254884_CH10_05.xhtml_page_250), [251](#9781284254884_CH10_05.xhtml_page_251)t

link local address, [187](#9781284254884_CH08_01.xhtml_page_187)

links, [171](#9781284254884_CH07_05.xhtml_page_171)–[172](#9781284254884_CH07_05.xhtml_page_172)

Linux file and directory permissions, [237](#9781284254884_CH10_01.xhtml_page_237)

default permissions, [243](#9781284254884_CH10_02.xhtml_page_243)–[244](#9781284254884_CH10_02.xhtml_page_244)

group, [237](#9781284254884_CH10_01.xhtml_page_237), [239](#9781284254884_CH10_02.xhtml_page_239)

ownership, [237](#9781284254884_CH10_01.xhtml_page_237)–[239](#9781284254884_CH10_02.xhtml_page_239)

permission controls, [239](#9781284254884_CH10_02.xhtml_page_239)–[241](#9781284254884_CH10_02.xhtml_page_241), [240](#9781284254884_CH10_02.xhtml_page_240)f

special permissions, [241](#9781284254884_CH10_02.xhtml_page_241)–[243](#9781284254884_CH10_02.xhtml_page_243)

Linux file system. [file management](#9781284254884_Index.xhtml_ie0149)

Linux Loader (LILO), [78](#9781284254884_CH04_02.xhtml_page_78)

Linux Logical Volume Manager (LMV), [113](#9781284254884_CH05_07.xhtml_page_113)–[114](#9781284254884_CH05_07.xhtml_page_114), [113](#9781284254884_CH05_07.xhtml_page_113)f

Linux system, block diagram of, [2](#9781284254884_CH01_01.xhtml_page_2), [2](#9781284254884_CH01_01.xhtml_page_2)f

Linux Unified Key Setup (LUKS), [61](#9781284254884_CH03_02.xhtml_page_61), [279](#9781284254884_CH11_02.xhtml_page_279)

list-units parameter, [88](#9781284254884_CH04_04.xhtml_page_88)

LiveDVD version, [19](#9781284254884_CH01_05.xhtml_page_19)

local environment variables, [138](#9781284254884_CH06_05.xhtml_page_138)–[140](#9781284254884_CH06_05.xhtml_page_140)

local loopback interface (lo), [191](#9781284254884_CH08_01.xhtml_page_191)–[193](#9781284254884_CH08_01.xhtml_page_193)

locate command, [177](#9781284254884_CH07_07.xhtml_page_177)–[178](#9781284254884_CH07_07.xhtml_page_178)

log files

syslogd program, [259](#9781284254884_CH10_07.xhtml_page_259)–[260](#9781284254884_CH10_08.xhtml_page_260), [260](#9781284254884_CH10_08.xhtml_page_260)t, [261](#9781284254884_CH10_08.xhtml_page_261)t

systemdjournald logging system, [261](#9781284254884_CH10_08.xhtml_page_261)

logical volume management (LVM), [61](#9781284254884_CH03_02.xhtml_page_61), [106](#9781284254884_CH05_03.xhtml_page_106)

logic statements, [146](#9781284254884_CH06_06.xhtml_page_146)–[148](#9781284254884_CH06_06.xhtml_page_148), [147](#9781284254884_CH06_06.xhtml_page_147)t

lsblk tool, [111](#9781284254884_CH05_06.xhtml_page_111)

ls command, [63](#9781284254884_CH03_02.xhtml_page_63), [160](#9781284254884_CH07_02.xhtml_page_160)–[161](#9781284254884_CH07_02.xhtml_page_161)

listing, [162](#9781284254884_CH07_03.xhtml_page_162)–[163](#9781284254884_CH07_03.xhtml_page_163)

modifying listing information, [163](#9781284254884_CH07_03.xhtml_page_163)–[164](#9781284254884_CH07_03.xhtml_page_164)

parameter list, [164](#9781284254884_CH07_03.xhtml_page_164), [164](#9781284254884_CH07_03.xhtml_page_164)t–165t, [166](#9781284254884_CH07_03.xhtml_page_166)

lsmod command, [53](#9781284254884_CH03_01.xhtml_page_53)–[55](#9781284254884_CH03_01.xhtml_page_55)

lspci command, [67](#9781284254884_CH03_03.xhtml_page_67)–[68](#9781284254884_CH03_03.xhtml_page_68), [67](#9781284254884_CH03_03.xhtml_page_67)t

lsusb command, [68](#9781284254884_CH03_03.xhtml_page_68), [68](#9781284254884_CH03_03.xhtml_page_68)t

lvcreate tool, [113](#9781284254884_CH05_07.xhtml_page_113)

LXC container package, [300](#9781284254884_CH12_03.xhtml_page_300)

Lynx, [25](#9781284254884_CH02_01.xhtml_page_25)

M

MAC method. [mandatory access control method](#9781284254884_Index.xhtml_ie0290)

mail command, [254](#9781284254884_CH10_06.xhtml_page_254)

Mail Delivery Agent (MDA), [252](#9781284254884_CH10_06.xhtml_page_252), [253](#9781284254884_CH10_06.xhtml_page_253)

Mail Submission Agent (MSA), [254](#9781284254884_CH10_06.xhtml_page_254)

Mail Transport Agent (MTA), [252](#9781284254884_CH10_06.xhtml_page_252), [253](#9781284254884_CH10_06.xhtml_page_253)

Mail User Agent (MUA), [252](#9781284254884_CH10_06.xhtml_page_252)

make package, [48](#9781284254884_CH02_04.xhtml_page_48)

mandatory access control (MAC) method, [273](#9781284254884_CH11_02.xhtml_page_273)

AppArmor, [277](#9781284254884_CH11_02.xhtml_page_277)–[279](#9781284254884_CH11_02.xhtml_page_279)

SELinux, [273](#9781284254884_CH11_02.xhtml_page_273)–[277](#9781284254884_CH11_02.xhtml_page_277)

man program, [129](#9781284254884_CH06_03.xhtml_page_129)

Marathon, [304](#9781284254884_CH12_05.xhtml_page_304)

MariaDB, [28](#9781284254884_CH02_01.xhtml_page_28)

Master Boot Record (MBR), [77](#9781284254884_CH04_02.xhtml_page_77), [98](#9781284254884_CH05_01.xhtml_page_98)

MATE desktop, [15](#9781284254884_CH01_04.xhtml_page_15)

MDA. [Mail Delivery Agent](#9781284254884_Index.xhtml_ie0285)

mdadm utility, [114](#9781284254884_CH05_07.xhtml_page_114)

MEMDISK boot loader program, [83](#9781284254884_CH04_03.xhtml_page_83)

memory management, [3](#9781284254884_CH01_02.xhtml_page_3)–[5](#9781284254884_CH01_02.xhtml_page_5), [4](#9781284254884_CH01_02.xhtml_page_4)f

memory pages, [3](#9781284254884_CH01_02.xhtml_page_3)–[4](#9781284254884_CH01_02.xhtml_page_4)

menuentry command, [81](#9781284254884_CH04_03.xhtml_page_81)–[82](#9781284254884_CH04_03.xhtml_page_82)

Mesos, [304](#9781284254884_CH12_05.xhtml_page_304)

mkdir command, [166](#9781284254884_CH07_03.xhtml_page_166)–[167](#9781284254884_CH07_04.xhtml_page_167)

mkfs program, [108](#9781284254884_CH05_04.xhtml_page_108)

modprobe command, [57](#9781284254884_CH03_01.xhtml_page_57)–[58](#9781284254884_CH03_01.xhtml_page_58), [57](#9781284254884_CH03_01.xhtml_page_57)t

modules, [53](#9781284254884_CH03_01.xhtml_page_53)

installing new, [55](#9781284254884_CH03_01.xhtml_page_55)–[58](#9781284254884_CH03_01.xhtml_page_58)

listing installed, [53](#9781284254884_CH03_01.xhtml_page_53)–[55](#9781284254884_CH03_01.xhtml_page_55)

removing modules, [58](#9781284254884_CH03_01.xhtml_page_58)

MongoDB database, [28](#9781284254884_CH02_01.xhtml_page_28)

more command, [135](#9781284254884_CH06_04.xhtml_page_135)

mount command, [109](#9781284254884_CH05_05.xhtml_page_109)

mounting file system, [103](#9781284254884_CH05_02.xhtml_page_103), [108](#9781284254884_CH05_04.xhtml_page_108)–[110](#9781284254884_CH05_05.xhtml_page_110)

mount points, [104](#9781284254884_CH05_03.xhtml_page_104), [155](#9781284254884_CH07_01.xhtml_page_155)

MSA. [Mail Submission Agent](#9781284254884_Index.xhtml_ie0286)

MTA. [Mail Transport Agent](#9781284254884_Index.xhtml_ie0287)

mtr command, [198](#9781284254884_CH08_02.xhtml_page_198), [199](#9781284254884_CH08_02.xhtml_page_199)f

MUA. [Mail User Agent](#9781284254884_Index.xhtml_ie0288)

multipathd tool, [112](#9781284254884_CH05_06.xhtml_page_112)

multipath tool, [112](#9781284254884_CH05_06.xhtml_page_112)

multi-user operating system, [232](#9781284254884_CH10_01.xhtml_page_232)

mv command, [172](#9781284254884_CH07_05.xhtml_page_172)–[173](#9781284254884_CH07_05.xhtml_page_173)

MySQL database server, [28](#9781284254884_CH02_01.xhtml_page_28)

N

netstat command, [202](#9781284254884_CH08_02.xhtml_page_202)–[205](#9781284254884_CH08_03.xhtml_page_205)

net-tools legacy tool, [193](#9781284254884_CH08_01.xhtml_page_193)–[196](#9781284254884_CH08_01.xhtml_page_196)

network device file, [9](#9781284254884_CH01_02.xhtml_page_9)

Network File Sharing (NFS), [29](#9781284254884_CH02_01.xhtml_page_29)

network interface cards, [59](#9781284254884_CH03_02.xhtml_page_59)

Network Manager tool

command-line tool, [190](#9781284254884_CH08_01.xhtml_page_190)–[191](#9781284254884_CH08_01.xhtml_page_191), [190](#9781284254884_CH08_01.xhtml_page_190)f

graphical tool, [188](#9781284254884_CH08_01.xhtml_page_188)–[190](#9781284254884_CH08_01.xhtml_page_190), [190](#9781284254884_CH08_01.xhtml_page_190)f

networks

command-line tools

DHCP client program, [196](#9781284254884_CH08_01.xhtml_page_196)–[197](#9781284254884_CH08_01.xhtml_page_197)

iproute2 package, [191](#9781284254884_CH08_01.xhtml_page_191)–[193](#9781284254884_CH08_01.xhtml_page_193), [192](#9781284254884_CH08_01.xhtml_page_192)t

net-tools package, [193](#9781284254884_CH08_01.xhtml_page_193)–[196](#9781284254884_CH08_01.xhtml_page_196)

Network Manager tool, [190](#9781284254884_CH08_01.xhtml_page_190)–[191](#9781284254884_CH08_01.xhtml_page_191), [190](#9781284254884_CH08_01.xhtml_page_190)f

configuration files, [186](#9781284254884_CH08_01.xhtml_page_186)–[188](#9781284254884_CH08_01.xhtml_page_188), [186](#9781284254884_CH08_01.xhtml_page_186)t

information to configure, [186](#9781284254884_CH08_01.xhtml_page_186)

Network Manager tool, [188](#9781284254884_CH08_01.xhtml_page_188)–[190](#9781284254884_CH08_01.xhtml_page_190), [190](#9781284254884_CH08_01.xhtml_page_190)f

troubleshooting

host information, [199](#9781284254884_CH08_02.xhtml_page_199)–[202](#9781284254884_CH08_02.xhtml_page_202)

netstat command, [202](#9781284254884_CH08_02.xhtml_page_202)–[205](#9781284254884_CH08_03.xhtml_page_205)

ss command, [205](#9781284254884_CH08_03.xhtml_page_205)–[206](#9781284254884_CH08_03.xhtml_page_206)

test packets, [197](#9781284254884_CH08_01.xhtml_page_197)–[198](#9781284254884_CH08_02.xhtml_page_198), [199](#9781284254884_CH08_02.xhtml_page_199)f

Network Time Protocol (NTP), [247](#9781284254884_CH10_04.xhtml_page_247)

New Technology File System (NTFS), [95](#9781284254884_CH05.xhtml_page_95), [107](#9781284254884_CH05_04.xhtml_page_107)

Nginx web server, [28](#9781284254884_CH02_01.xhtml_page_28)

nice command, [215](#9781284254884_CH09_03.xhtml_page_215)

nmcli command-line tool, [190](#9781284254884_CH08_01.xhtml_page_190)–[191](#9781284254884_CH08_01.xhtml_page_191)

nmtui command-line tool, [190](#9781284254884_CH08_01.xhtml_page_190), [190](#9781284254884_CH08_01.xhtml_page_190)f

nodes, [9](#9781284254884_CH01_02.xhtml_page_9)

nohup command, [219](#9781284254884_CH09_04.xhtml_page_219)

nohup.out file, [219](#9781284254884_CH09_04.xhtml_page_219)–[220](#9781284254884_CH09_05.xhtml_page_220)

non-Linux file system, [107](#9781284254884_CH05_04.xhtml_page_107)–[108](#9781284254884_CH05_04.xhtml_page_108)

Non-Volatile Memory Express (NVMe), [97](#9781284254884_CH05_01.xhtml_page_97)

normal user accounts, [233](#9781284254884_CH10_01.xhtml_page_233)

NoSQL databases, [28](#9781284254884_CH02_01.xhtml_page_28)

nslookup command, [201](#9781284254884_CH08_02.xhtml_page_201)

ntpd program, [247](#9781284254884_CH10_04.xhtml_page_247)–[248](#9781284254884_CH10_04.xhtml_page_248)

O

octal mode permissions, [241](#9781284254884_CH10_02.xhtml_page_241)–[243](#9781284254884_CH10_02.xhtml_page_243), [242](#9781284254884_CH10_02.xhtml_page_242)t

office productivity, [24](#9781284254884_CH02_01.xhtml_page_24), [25](#9781284254884_CH02_01.xhtml_page_25)f

OpenOffice.org software package, [24](#9781284254884_CH02_01.xhtml_page_24)

open source software (OSS), [10](#9781284254884_CH01_03.xhtml_page_10)–[11](#9781284254884_CH01_03.xhtml_page_11)

OpenSSH, [255](#9781284254884_CH10_06.xhtml_page_255), [256](#9781284254884_CH10_07.xhtml_page_256)

Open Virtualization Format (OVF), [298](#9781284254884_CH12_02.xhtml_page_298)

Opera browser, [25](#9781284254884_CH02_01.xhtml_page_25)

orchestration tool, [301](#9781284254884_CH12_04.xhtml_page_301)

orphan file, [237](#9781284254884_CH10_01.xhtml_page_237)

output redirection, [132](#9781284254884_CH06_04.xhtml_page_132)

owner permissions, [240](#9781284254884_CH10_02.xhtml_page_240)

P

PaaS model. [Platform as a Service model](#9781284254884_Index.xhtml_ie0372)

package, defined, [29](#9781284254884_CH02_01.xhtml_page_29)

package management system, [29](#9781284254884_CH02_01.xhtml_page_29)–[30](#9781284254884_CH02_02.xhtml_page_30)

debian-based distributions, [30](#9781284254884_CH02_02.xhtml_page_30)–[38](#9781284254884_CH02_02.xhtml_page_38)

Red Hat-based systems, [30](#9781284254884_CH02_02.xhtml_page_30), [38](#9781284254884_CH02_02.xhtml_page_38)–[41](#9781284254884_CH02_02.xhtml_page_41)

Parallel Advanced Technology Attachment (PATA), [97](#9781284254884_CH05_01.xhtml_page_97)

partition, defined, [98](#9781284254884_CH05_01.xhtml_page_98)

passwd command, [236](#9781284254884_CH10_01.xhtml_page_236), [237](#9781284254884_CH10_01.xhtml_page_237)

password mode, [257](#9781284254884_CH10_07.xhtml_page_257)–[258](#9781284254884_CH10_07.xhtml_page_258)

PCI. [Peripheral Component Interconnect](#9781284254884_Index.xhtml_ie0364)

PCI Express (PCIe) standard, [59](#9781284254884_CH03_02.xhtml_page_59), [67](#9781284254884_CH03_03.xhtml_page_67)

p command, [99](#9781284254884_CH05_01.xhtml_page_99)

Peripheral Component Interconnect (PCI), [58](#9781284254884_CH03_01.xhtml_page_58)–[59](#9781284254884_CH03_02.xhtml_page_59), [67](#9781284254884_CH03_03.xhtml_page_67)–[68](#9781284254884_CH03_03.xhtml_page_68)

PermitRootLogin configuration, [256](#9781284254884_CH10_07.xhtml_page_256)

persistent device files, [98](#9781284254884_CH05_01.xhtml_page_98)

pgrep command, [217](#9781284254884_CH09_03.xhtml_page_217)

ping command, [197](#9781284254884_CH08_01.xhtml_page_197)–[198](#9781284254884_CH08_02.xhtml_page_198)

ping6 command, [197](#9781284254884_CH08_01.xhtml_page_197)–[198](#9781284254884_CH08_02.xhtml_page_198)

piping process, [134](#9781284254884_CH06_04.xhtml_page_134)–[135](#9781284254884_CH06_04.xhtml_page_135)

pkill command, [216](#9781284254884_CH09_03.xhtml_page_216)–[217](#9781284254884_CH09_03.xhtml_page_217)

Platform as a Service (PaaS) model, [294](#9781284254884_CH12_01.xhtml_page_294)–[295](#9781284254884_CH12_01.xhtml_page_295), [295](#9781284254884_CH12_01.xhtml_page_295)f

PnP system, [61](#9781284254884_CH03_02.xhtml_page_61)

Postfix, [29](#9781284254884_CH02_01.xhtml_page_29), [253](#9781284254884_CH10_06.xhtml_page_253)

PostgreSQL database server, [28](#9781284254884_CH02_01.xhtml_page_28)

Postscript Printer Definition (PPD) file, [251](#9781284254884_CH10_05.xhtml_page_251)

Postscript protocol, [251](#9781284254884_CH10_05.xhtml_page_251)

poweroff command, [87](#9781284254884_CH04_04.xhtml_page_87)

power-on self-test (POST), [74](#9781284254884_CH04_01.xhtml_page_74)

Pre-boot eXecution Environment (PXE) standard, [83](#9781284254884_CH04_03.xhtml_page_83)

primary partitions, [98](#9781284254884_CH05_01.xhtml_page_98)

printenv command, [136](#9781284254884_CH06_05.xhtml_page_136)–[138](#9781284254884_CH06_05.xhtml_page_138)

printer administration, [249](#9781284254884_CH10_04.xhtml_page_249)–[251](#9781284254884_CH10_05.xhtml_page_251)

private cloud computing, [292](#9781284254884_CH12_01.xhtml_page_292)

private key, [256](#9781284254884_CH10_07.xhtml_page_256), [257](#9781284254884_CH10_07.xhtml_page_257)

/proc directory, [61](#9781284254884_CH03_02.xhtml_page_61)

process

defined, [6](#9781284254884_CH01_02.xhtml_page_6), [210](#9781284254884_CH09_01.xhtml_page_210)

init process, [210](#9781284254884_CH09_01.xhtml_page_210)

job control, [220](#9781284254884_CH09_05.xhtml_page_220)–[223](#9781284254884_CH09_06.xhtml_page_223)

job scheduling

cron program, [226](#9781284254884_CH09_07.xhtml_page_226)–[228](#9781284254884_CH09_07.xhtml_page_228)

using at command, [223](#9781284254884_CH09_06.xhtml_page_223)–[226](#9781284254884_CH09_07.xhtml_page_226)

management, [213](#9781284254884_CH09_02.xhtml_page_213)

priority setting, [213](#9781284254884_CH09_02.xhtml_page_213), [215](#9781284254884_CH09_03.xhtml_page_215)

process signals, [215](#9781284254884_CH09_03.xhtml_page_215)–[217](#9781284254884_CH09_03.xhtml_page_217), [216](#9781284254884_CH09_03.xhtml_page_216)t

monitoring in real time, [212](#9781284254884_CH09_02.xhtml_page_212)–[214](#9781284254884_CH09_03.xhtml_page_214)

running on system, [211](#9781284254884_CH09_01.xhtml_page_211)

running programs

in background mode, [217](#9781284254884_CH09_03.xhtml_page_217)–[219](#9781284254884_CH09_04.xhtml_page_219)

without console, [219](#9781284254884_CH09_04.xhtml_page_219)–[220](#9781284254884_CH09_05.xhtml_page_220)

sleep mode, [211](#9781284254884_CH09_01.xhtml_page_211)

process initialization. [initialization process](#9781284254884_Index.xhtml_ie0212)

process signals, [215](#9781284254884_CH09_03.xhtml_page_215)–[217](#9781284254884_CH09_03.xhtml_page_217), [216](#9781284254884_CH09_03.xhtml_page_216)t

Procmail program, [253](#9781284254884_CH10_06.xhtml_page_253)

/proc/mounts directory, [111](#9781284254884_CH05_06.xhtml_page_111)

/proc/partitions directory, [111](#9781284254884_CH05_06.xhtml_page_111)

Protocol configuration, [256](#9781284254884_CH10_07.xhtml_page_256)

ps command, [7](#9781284254884_CH01_02.xhtml_page_7)–[8](#9781284254884_CH01_02.xhtml_page_8), [210](#9781284254884_CH09_01.xhtml_page_210), [212](#9781284254884_CH09_02.xhtml_page_212), [213](#9781284254884_CH09_02.xhtml_page_213), [217](#9781284254884_CH09_03.xhtml_page_217)–[219](#9781284254884_CH09_04.xhtml_page_219)

PS1 command line prompt, [123](#9781284254884_CH06_01.xhtml_page_123)

PS2 command line prompt, [123](#9781284254884_CH06_01.xhtml_page_123)

public cloud computing, [292](#9781284254884_CH12_01.xhtml_page_292)

public key, [256](#9781284254884_CH10_07.xhtml_page_256), [257](#9781284254884_CH10_07.xhtml_page_257)

pvcreate tool, [113](#9781284254884_CH05_07.xhtml_page_113)

PXELINUX boot loader program, [83](#9781284254884_CH04_03.xhtml_page_83)

Q

qMail, [29](#9781284254884_CH02_01.xhtml_page_29)

question mark glob character, [174](#9781284254884_CH07_05.xhtml_page_174)–[175](#9781284254884_CH07_06.xhtml_page_175)

quoting files, [175](#9781284254884_CH07_06.xhtml_page_175)–[176](#9781284254884_CH07_06.xhtml_page_176)

R

RAID 0, [114](#9781284254884_CH05_07.xhtml_page_114)

RAID 1, [114](#9781284254884_CH05_07.xhtml_page_114)

RAID 4, [114](#9781284254884_CH05_07.xhtml_page_114)

RAID 5, [114](#9781284254884_CH05_07.xhtml_page_114)

RAID 6, [114](#9781284254884_CH05_07.xhtml_page_114)

RAID 10, [114](#9781284254884_CH05_07.xhtml_page_114)

RAID. [Redundant Array of Independent Disks](#9781284254884_Index.xhtml_ie9415)

raw device, [97](#9781284254884_CH05_01.xhtml_page_97)

read permission, [239](#9781284254884_CH10_02.xhtml_page_239), [240](#9781284254884_CH10_02.xhtml_page_240)

reboot command, [87](#9781284254884_CH04_04.xhtml_page_87)

Red Hat package management system (RPM), [30](#9781284254884_CH02_02.xhtml_page_30), [134](#9781284254884_CH06_04.xhtml_page_134)

dnf tool, [38](#9781284254884_CH02_02.xhtml_page_38)

installing software with, [39](#9781284254884_CH02_02.xhtml_page_39)–[40](#9781284254884_CH02_02.xhtml_page_40)

listing installed packages, [38](#9781284254884_CH02_02.xhtml_page_38)–[39](#9781284254884_CH02_02.xhtml_page_39)

uninstalling software with, [41](#9781284254884_CH02_02.xhtml_page_41)

upgrading software with, [40](#9781284254884_CH02_02.xhtml_page_40)–[41](#9781284254884_CH02_02.xhtml_page_41)

yum tool, [38](#9781284254884_CH02_02.xhtml_page_38)

zypper tool, [38](#9781284254884_CH02_02.xhtml_page_38)

Redundant Array of Independent Disks (RAID), [106](#9781284254884_CH05_03.xhtml_page_106), [114](#9781284254884_CH05_07.xhtml_page_114)

reiserFS Linux file system, [107](#9781284254884_CH05_04.xhtml_page_107)

relative filepaths, [158](#9781284254884_CH07_01.xhtml_page_158)

relative path, [106](#9781284254884_CH05_03.xhtml_page_106)

renice command, [215](#9781284254884_CH09_03.xhtml_page_215)

repositories, [29](#9781284254884_CH02_01.xhtml_page_29)

resize2fs tool, [111](#9781284254884_CH05_06.xhtml_page_111)

rm command, [173](#9781284254884_CH07_05.xhtml_page_173)–[176](#9781284254884_CH07_06.xhtml_page_176)

rmdir command, [167](#9781284254884_CH07_04.xhtml_page_167)

rmmod command, [58](#9781284254884_CH03_01.xhtml_page_58)

root administrator, [233](#9781284254884_CH10_01.xhtml_page_233)

root command, [80](#9781284254884_CH04_03.xhtml_page_80)

root directory, [104](#9781284254884_CH05_03.xhtml_page_104), [155](#9781284254884_CH07_01.xhtml_page_155)

root drive, [155](#9781284254884_CH07_01.xhtml_page_155)

rootnoverify command, [80](#9781284254884_CH04_03.xhtml_page_80)

root user account, [266](#9781284254884_CH11_01.xhtml_page_266)–[267](#9781284254884_CH11_01.xhtml_page_267)

route command, [195](#9781284254884_CH08_01.xhtml_page_195)–[196](#9781284254884_CH08_01.xhtml_page_196)

rpm command, [134](#9781284254884_CH06_04.xhtml_page_134)–[135](#9781284254884_CH06_04.xhtml_page_135)

rpm package management system, [30](#9781284254884_CH02_02.xhtml_page_30)

runlevels, [6](#9781284254884_CH01_02.xhtml_page_6), [84](#9781284254884_CH04_04.xhtml_page_84), [85](#9781284254884_CH04_04.xhtml_page_85)t

changing current, [86](#9781284254884_CH04_04.xhtml_page_86)–[87](#9781284254884_CH04_04.xhtml_page_87)

checking, [86](#9781284254884_CH04_04.xhtml_page_86)

start applications in, [85](#9781284254884_CH04_04.xhtml_page_85), [86](#9781284254884_CH04_04.xhtml_page_86)t

S

SaaS model. [Software as a Service model](#9781284254884_Index.xhtml_ie0461)

Samba software package, [29](#9781284254884_CH02_01.xhtml_page_29)

/sbin/nologin file, [272](#9781284254884_CH11_01.xhtml_page_272)

scp program, [256](#9781284254884_CH10_07.xhtml_page_256)

secure shell (SSH) login, [255](#9781284254884_CH10_06.xhtml_page_255)

disabling root access from, [270](#9781284254884_CH11_01.xhtml_page_270)–[271](#9781284254884_CH11_01.xhtml_page_271)

encrypting files, [258](#9781284254884_CH10_07.xhtml_page_258)–[259](#9781284254884_CH10_07.xhtml_page_259)

key mode, [257](#9781284254884_CH10_07.xhtml_page_257), [258](#9781284254884_CH10_07.xhtml_page_258)

OpenSSH package, [255](#9781284254884_CH10_06.xhtml_page_255)–[257](#9781284254884_CH10_07.xhtml_page_257)

password mode, [257](#9781284254884_CH10_07.xhtml_page_257)–[258](#9781284254884_CH10_07.xhtml_page_258)

security context, [274](#9781284254884_CH11_02.xhtml_page_274)–[275](#9781284254884_CH11_02.xhtml_page_275)

Security-Enhanced Linux (SELinux), [265](#9781284254884_CH11.xhtml_page_265), [273](#9781284254884_CH11_02.xhtml_page_273)–[274](#9781284254884_CH11_02.xhtml_page_274)

policies, [275](#9781284254884_CH11_02.xhtml_page_275)–[277](#9781284254884_CH11_02.xhtml_page_277)

security context, [274](#9781284254884_CH11_02.xhtml_page_274)–[275](#9781284254884_CH11_02.xhtml_page_275)

security features, of Linux

encrypting partitions, [279](#9781284254884_CH11_02.xhtml_page_279)–[281](#9781284254884_CH11_03.xhtml_page_281)

firewalls, [281](#9781284254884_CH11_03.xhtml_page_281)–[287](#9781284254884_CH11_04.xhtml_page_287)

mandatory access control (MAC) method, [273](#9781284254884_CH11_02.xhtml_page_273)

AppArmor, [277](#9781284254884_CH11_02.xhtml_page_277)–[279](#9781284254884_CH11_02.xhtml_page_279)

SELinux, [273](#9781284254884_CH11_02.xhtml_page_273)–[277](#9781284254884_CH11_02.xhtml_page_277)

root user account, [266](#9781284254884_CH11_01.xhtml_page_266)–[267](#9781284254884_CH11_01.xhtml_page_267)

aulast command, [270](#9781284254884_CH11_01.xhtml_page_270)

automatic logout, [271](#9781284254884_CH11_01.xhtml_page_271)

blocking root access, [271](#9781284254884_CH11_01.xhtml_page_271)–[272](#9781284254884_CH11_01.xhtml_page_272)

privilege elevation status, [269](#9781284254884_CH11_01.xhtml_page_269)–[270](#9781284254884_CH11_01.xhtml_page_270)

SSH server, [270](#9781284254884_CH11_01.xhtml_page_270)–[271](#9781284254884_CH11_01.xhtml_page_271)

super user privileges, [267](#9781284254884_CH11_01.xhtml_page_267)–[269](#9781284254884_CH11_01.xhtml_page_269)

SELinux. [Security-Enhanced Linux](#9781284254884_Index.xhtml_ie0440)

sendmail package, [29](#9781284254884_CH02_01.xhtml_page_29)

Serial Advanced Technology Attachment (SATA), [97](#9781284254884_CH05_01.xhtml_page_97)

server applications, [28](#9781284254884_CH02_01.xhtml_page_28)

database server, [28](#9781284254884_CH02_01.xhtml_page_28)

email server, [29](#9781284254884_CH02_01.xhtml_page_29)

Network File Sharing, [29](#9781284254884_CH02_01.xhtml_page_29)

web server, [28](#9781284254884_CH02_01.xhtml_page_28)

service accounts, [233](#9781284254884_CH10_01.xhtml_page_233), [266](#9781284254884_CH11_01.xhtml_page_266)

set command, [138](#9781284254884_CH06_05.xhtml_page_138)

setfacl command, [245](#9781284254884_CH10_03.xhtml_page_245)

Set Group ID (SGID), [242](#9781284254884_CH10_02.xhtml_page_242), [243](#9781284254884_CH10_02.xhtml_page_243)

setsebool command, [277](#9781284254884_CH11_02.xhtml_page_277)

Set User ID (SUID) bit, [242](#9781284254884_CH10_02.xhtml_page_242)

sftp program, [256](#9781284254884_CH10_07.xhtml_page_256)

shells, [17](#9781284254884_CH01_04.xhtml_page_17), [17](#9781284254884_CH01_04.xhtml_page_17)t

command completion, [130](#9781284254884_CH06_03.xhtml_page_130)–[131](#9781284254884_CH06_03.xhtml_page_131)

command line

editing commands, [131](#9781284254884_CH06_03.xhtml_page_131)t

parameters, [122](#9781284254884_CH06_01.xhtml_page_122)t

command prompt, [122](#9781284254884_CH06_01.xhtml_page_122)–[123](#9781284254884_CH06_01.xhtml_page_123), [124](#9781284254884_CH06_02.xhtml_page_124)t

commands, [127](#9781284254884_CH06_02.xhtml_page_127)–[130](#9781284254884_CH06_03.xhtml_page_130)

defined, [120](#9781284254884_CH06_01.xhtml_page_120)

environment variables, [136](#9781284254884_CH06_05.xhtml_page_136)

global, [136](#9781284254884_CH06_05.xhtml_page_136)–[138](#9781284254884_CH06_05.xhtml_page_138), [140](#9781284254884_CH06_05.xhtml_page_140)

local, [138](#9781284254884_CH06_05.xhtml_page_138)–[140](#9781284254884_CH06_05.xhtml_page_140)

removing, [140](#9781284254884_CH06_05.xhtml_page_140)–[141](#9781284254884_CH06_05.xhtml_page_141)

external commands, [120](#9781284254884_CH06_01.xhtml_page_120)

history file, [130](#9781284254884_CH06_03.xhtml_page_130)

input redirection, [132](#9781284254884_CH06_04.xhtml_page_132)–[133](#9781284254884_CH06_04.xhtml_page_133)

internal commands, [120](#9781284254884_CH06_01.xhtml_page_120)

multiple commands, [131](#9781284254884_CH06_03.xhtml_page_131)

output redirection, [132](#9781284254884_CH06_04.xhtml_page_132)

redirection

input, [132](#9781284254884_CH06_04.xhtml_page_132)–[133](#9781284254884_CH06_04.xhtml_page_133)

output, [132](#9781284254884_CH06_04.xhtml_page_132)

pipes, [134](#9781284254884_CH06_04.xhtml_page_134)–[135](#9781284254884_CH06_04.xhtml_page_135)

scripts [(shell scripts)](#9781284254884_Index.xhtml_ie0454)

starting shell, [121](#9781284254884_CH06_01.xhtml_page_121)–[122](#9781284254884_CH06_01.xhtml_page_122)

types of, [121](#9781284254884_CH06_01.xhtml_page_121)

shell scripts, [17](#9781284254884_CH01_04.xhtml_page_17), [131](#9781284254884_CH06_03.xhtml_page_131), [141](#9781284254884_CH06_05.xhtml_page_141)–[142](#9781284254884_CH06_06.xhtml_page_142)

command line arguments, [145](#9781284254884_CH06_06.xhtml_page_145)

command substitution, [145](#9781284254884_CH06_06.xhtml_page_145)–[146](#9781284254884_CH06_06.xhtml_page_146)

displaying messages, [143](#9781284254884_CH06_06.xhtml_page_143)–[144](#9781284254884_CH06_06.xhtml_page_144)

getting started, [142](#9781284254884_CH06_06.xhtml_page_142)–[143](#9781284254884_CH06_06.xhtml_page_143)

logic statements, [146](#9781284254884_CH06_06.xhtml_page_146)–[148](#9781284254884_CH06_06.xhtml_page_148), [147](#9781284254884_CH06_06.xhtml_page_147)t

looping commands, [148](#9781284254884_CH06_06.xhtml_page_148)–[150](#9781284254884_CH06_07.xhtml_page_150)

variables, [144](#9781284254884_CH06_06.xhtml_page_144)

shutdown command, [87](#9781284254884_CH04_04.xhtml_page_87)

Simple Mail Transfer Protocol (SMTP), [253](#9781284254884_CH10_06.xhtml_page_253)

single-letter parameters, [164](#9781284254884_CH07_03.xhtml_page_164), [164](#9781284254884_CH07_03.xhtml_page_164)t–165t

Small Computer System Interface (SCSI), [97](#9781284254884_CH05_01.xhtml_page_97)

snap application container, [42](#9781284254884_CH02_03.xhtml_page_42)–[43](#9781284254884_CH02_03.xhtml_page_43)

snapd application, [42](#9781284254884_CH02_03.xhtml_page_42)

Software as a Service (SaaS) model, [294](#9781284254884_CH12_01.xhtml_page_294), [294](#9781284254884_CH12_01.xhtml_page_294)f

software package, [24](#9781284254884_CH02_01.xhtml_page_24)

software program management, [6](#9781284254884_CH01_02.xhtml_page_6)–[8](#9781284254884_CH01_02.xhtml_page_8)

solid state drive (SSD), [9](#9781284254884_CH01_02.xhtml_page_9), [97](#9781284254884_CH05_01.xhtml_page_97)

sort command, [135](#9781284254884_CH06_04.xhtml_page_135)

source code packages, [45](#9781284254884_CH02_03.xhtml_page_45)–[49](#9781284254884_CH02_04.xhtml_page_49)

ss command, [205](#9781284254884_CH08_03.xhtml_page_205)–[206](#9781284254884_CH08_03.xhtml_page_206)

sshd program, [256](#9781284254884_CH10_07.xhtml_page_256)

SSH login. [secure shell login](#9781284254884_Index.xhtml_ie0438)

ssh program, [256](#9781284254884_CH10_07.xhtml_page_256)

standard input, for shell, [128](#9781284254884_CH06_03.xhtml_page_128)

standard output, for shell, [128](#9781284254884_CH06_03.xhtml_page_128)

standard user account, [266](#9781284254884_CH11_01.xhtml_page_266)

start command, [90](#9781284254884_CH04_04.xhtml_page_90)

stop command, [90](#9781284254884_CH04_04.xhtml_page_90)

su command, [234](#9781284254884_CH10_01.xhtml_page_234), [267](#9781284254884_CH11_01.xhtml_page_267), [269](#9781284254884_CH11_01.xhtml_page_269)

sudo command, [234](#9781284254884_CH10_01.xhtml_page_234), [235](#9781284254884_CH10_01.xhtml_page_235), [267](#9781284254884_CH11_01.xhtml_page_267)–[269](#9781284254884_CH11_01.xhtml_page_269)

sudoedit command, [269](#9781284254884_CH11_01.xhtml_page_269)

sudoers file, [268](#9781284254884_CH11_01.xhtml_page_268)

super user privileges, [267](#9781284254884_CH11_01.xhtml_page_267)–[269](#9781284254884_CH11_01.xhtml_page_269)

swap file system, [107](#9781284254884_CH05_04.xhtml_page_107)

swap space, [3](#9781284254884_CH01_02.xhtml_page_3)

symbolic link, [171](#9781284254884_CH07_05.xhtml_page_171)

symbolic mode permissions, [240](#9781284254884_CH10_02.xhtml_page_240)–[241](#9781284254884_CH10_02.xhtml_page_241)

/sys/block directory, [111](#9781284254884_CH05_06.xhtml_page_111)

/sys directory, [63](#9781284254884_CH03_02.xhtml_page_63)–[64](#9781284254884_CH03_02.xhtml_page_64)

SYSLINUX boot loader program, [83](#9781284254884_CH04_03.xhtml_page_83)

syslogd program, [259](#9781284254884_CH10_07.xhtml_page_259)–[260](#9781284254884_CH10_08.xhtml_page_260), [260](#9781284254884_CH10_08.xhtml_page_260)t, [261](#9781284254884_CH10_08.xhtml_page_261)t

systemctl program, [90](#9781284254884_CH04_04.xhtml_page_90)–[92](#9781284254884_CH04_04.xhtml_page_92), [91](#9781284254884_CH04_04.xhtml_page_91)t

systemd initialization process method, [6](#9781284254884_CH01_02.xhtml_page_6), [7](#9781284254884_CH01_02.xhtml_page_7), [84](#9781284254884_CH04_04.xhtml_page_84), [87](#9781284254884_CH04_04.xhtml_page_87)

systemctl program, [90](#9781284254884_CH04_04.xhtml_page_90)–[92](#9781284254884_CH04_04.xhtml_page_92), [91](#9781284254884_CH04_04.xhtml_page_91)t

units and targets, [87](#9781284254884_CH04_04.xhtml_page_87)–[90](#9781284254884_CH04_04.xhtml_page_90)

systemdjournald logging system, [261](#9781284254884_CH10_08.xhtml_page_261)

systemd-timesyncd program, [248](#9781284254884_CH10_04.xhtml_page_248)

SysVinit

initialization method, [6](#9781284254884_CH01_02.xhtml_page_6)–[7](#9781284254884_CH01_02.xhtml_page_7), [6](#9781284254884_CH01_02.xhtml_page_6)t, [84](#9781284254884_CH04_04.xhtml_page_84)–[87](#9781284254884_CH04_04.xhtml_page_87)

startup script method, [259](#9781284254884_CH10_07.xhtml_page_259)

T

tarball package, [45](#9781284254884_CH02_03.xhtml_page_45), [46](#9781284254884_CH02_04.xhtml_page_46)

tar command, [45](#9781284254884_CH02_03.xhtml_page_45), [46](#9781284254884_CH02_04.xhtml_page_46), [180](#9781284254884_CH07_08.xhtml_page_180)–[182](#9781284254884_CH07_08.xhtml_page_182), [181](#9781284254884_CH07_08.xhtml_page_181)t

targets, [7](#9781284254884_CH01_02.xhtml_page_7), [87](#9781284254884_CH04_04.xhtml_page_87)–[90](#9781284254884_CH04_04.xhtml_page_90)

tcsh shell, [121](#9781284254884_CH06_01.xhtml_page_121)

Telnet protocol, [255](#9781284254884_CH10_06.xhtml_page_255)

terminal emulation package, [126](#9781284254884_CH06_02.xhtml_page_126)–[127](#9781284254884_CH06_02.xhtml_page_127), [127](#9781284254884_CH06_02.xhtml_page_127)f

Thunderbird email client, [26](#9781284254884_CH02_01.xhtml_page_26), [27](#9781284254884_CH02_01.xhtml_page_27)f, [253](#9781284254884_CH10_06.xhtml_page_253), [254](#9781284254884_CH10_06.xhtml_page_254)f

title command, [80](#9781284254884_CH04_03.xhtml_page_80)

top command, [212](#9781284254884_CH09_02.xhtml_page_212), [212](#9781284254884_CH09_02.xhtml_page_212)f, [213](#9781284254884_CH09_02.xhtml_page_213), [214](#9781284254884_CH09_03.xhtml_page_214)t

Torvalds, Linus, [3](#9781284254884_CH01_02.xhtml_page_3)

touch command, [168](#9781284254884_CH07_04.xhtml_page_168)

traceroute command, [198](#9781284254884_CH08_02.xhtml_page_198)

Transmission Control Protocol (TCP), [206](#9781284254884_CH08_03.xhtml_page_206)

traversing directories, Linux filesystem, [157](#9781284254884_CH07_01.xhtml_page_157)–[158](#9781284254884_CH07_01.xhtml_page_158)

tune2fs tool, [111](#9781284254884_CH05_06.xhtml_page_111)

tunneling, [256](#9781284254884_CH10_07.xhtml_page_256)

Type I hypervisor, [297](#9781284254884_CH12_02.xhtml_page_297), [297](#9781284254884_CH12_02.xhtml_page_297)f

Type II hypervisor, [297](#9781284254884_CH12_02.xhtml_page_297)–[298](#9781284254884_CH12_02.xhtml_page_298), [298](#9781284254884_CH12_02.xhtml_page_298)f

type shell built-in program, [127](#9781284254884_CH06_02.xhtml_page_127)

U

udevadm command, [69](#9781284254884_CH03_04.xhtml_page_69), [70](#9781284254884_CH03_04.xhtml_page_70)t

udev program, [69](#9781284254884_CH03_04.xhtml_page_69), [98](#9781284254884_CH05_01.xhtml_page_98)–[99](#9781284254884_CH05_01.xhtml_page_99)

UEFI. [Unified Extensible Firmware Interface](#9781284254884_Index.xhtml_ie0518)

umask command, [243](#9781284254884_CH10_02.xhtml_page_243), [244](#9781284254884_CH10_02.xhtml_page_244), [244](#9781284254884_CH10_02.xhtml_page_244)t

umount command, [109](#9781284254884_CH05_05.xhtml_page_109)

Unified Extensible Firmware Interface (UEFI), [76](#9781284254884_CH04_01.xhtml_page_76)–[78](#9781284254884_CH04_02.xhtml_page_78)

unit files, [7](#9781284254884_CH01_02.xhtml_page_7)

units, [87](#9781284254884_CH04_04.xhtml_page_87)–[90](#9781284254884_CH04_04.xhtml_page_90)

Universal Disc Format (UDF), [107](#9781284254884_CH05_04.xhtml_page_107)

Universal Serial Bus (USB) interface, [59](#9781284254884_CH03_02.xhtml_page_59)–[60](#9781284254884_CH03_02.xhtml_page_60), [68](#9781284254884_CH03_03.xhtml_page_68)

Unix style parameters, [210](#9781284254884_CH09_01.xhtml_page_210)

unmounting, [103](#9781284254884_CH05_02.xhtml_page_103)

unset command, [140](#9781284254884_CH06_05.xhtml_page_140)–[141](#9781284254884_CH06_05.xhtml_page_141)

updatedb program, [177](#9781284254884_CH07_07.xhtml_page_177)–[178](#9781284254884_CH07_07.xhtml_page_178)

USB interface. [Universal Serial Bus interface](#9781284254884_Index.xhtml_ie0522)

user accounts, [232](#9781284254884_CH10_01.xhtml_page_232)

commands to manage, [236](#9781284254884_CH10_01.xhtml_page_236)–[237](#9781284254884_CH10_01.xhtml_page_237)

types of, [233](#9781284254884_CH10_01.xhtml_page_233)–[234](#9781284254884_CH10_01.xhtml_page_234), [266](#9781284254884_CH11_01.xhtml_page_266)

useradd command, [236](#9781284254884_CH10_01.xhtml_page_236), [236](#9781284254884_CH10_01.xhtml_page_236)t

userdel command, [236](#9781284254884_CH10_01.xhtml_page_236), [237](#9781284254884_CH10_01.xhtml_page_237)

user management, [232](#9781284254884_CH10_01.xhtml_page_232)

accessing administrator privileges, [234](#9781284254884_CH10_01.xhtml_page_234)–[235](#9781284254884_CH10_01.xhtml_page_235)

groups, [235](#9781284254884_CH10_01.xhtml_page_235)–[236](#9781284254884_CH10_01.xhtml_page_236)

user accounts, [233](#9781284254884_CH10_01.xhtml_page_233)–[234](#9781284254884_CH10_01.xhtml_page_234), [236](#9781284254884_CH10_01.xhtml_page_236)–[237](#9781284254884_CH10_01.xhtml_page_237)

usermod command, [236](#9781284254884_CH10_01.xhtml_page_236), [237](#9781284254884_CH10_01.xhtml_page_237)

V

VFS. [Virtual File System](#9781284254884_Index.xhtml_ie0538)

vgcreate tool, [113](#9781284254884_CH05_07.xhtml_page_113)

video accelerators, [59](#9781284254884_CH03_02.xhtml_page_59)

virtual directory, [104](#9781284254884_CH05_03.xhtml_page_104)–[106](#9781284254884_CH05_03.xhtml_page_106), [105](#9781284254884_CH05_03.xhtml_page_105)f, [108](#9781284254884_CH05_04.xhtml_page_108), [155](#9781284254884_CH07_01.xhtml_page_155)

Virtual File Allocation Table (VFAT), [107](#9781284254884_CH05_04.xhtml_page_107)

Virtual File System (VFS), [9](#9781284254884_CH01_02.xhtml_page_9)

virtualization

defined, [295](#9781284254884_CH12_01.xhtml_page_295)

hypervisor, [296](#9781284254884_CH12_02.xhtml_page_296)–[297](#9781284254884_CH12_02.xhtml_page_297)

templates, [298](#9781284254884_CH12_02.xhtml_page_298)

Type I, [297](#9781284254884_CH12_02.xhtml_page_297), [297](#9781284254884_CH12_02.xhtml_page_297)f

Type II, [297](#9781284254884_CH12_02.xhtml_page_297)–[298](#9781284254884_CH12_02.xhtml_page_298), [298](#9781284254884_CH12_02.xhtml_page_298)f

separating application resources, [295](#9781284254884_CH12_01.xhtml_page_295), [296](#9781284254884_CH12_02.xhtml_page_296)f

server concept, [295](#9781284254884_CH12_01.xhtml_page_295), [296](#9781284254884_CH12_02.xhtml_page_296)f

virtual machine monitor (vmm). [hypervisor](#9781284254884_Index.xhtml_ie0206)

virtual memory, [3](#9781284254884_CH01_02.xhtml_page_3)

virtual terminals, [124](#9781284254884_CH06_02.xhtml_page_124)–[126](#9781284254884_CH06_02.xhtml_page_126), [125](#9781284254884_CH06_02.xhtml_page_125)f

visudo command, [269](#9781284254884_CH11_01.xhtml_page_269)

W

Wayland software, [12](#9781284254884_CH01_04.xhtml_page_12)

wc command, [133](#9781284254884_CH06_04.xhtml_page_133)

web browser, [25](#9781284254884_CH02_01.xhtml_page_25), [26](#9781284254884_CH02_01.xhtml_page_26)f

web server, [28](#9781284254884_CH02_01.xhtml_page_28)

whereis command, [178](#9781284254884_CH07_07.xhtml_page_178)

which command, [177](#9781284254884_CH07_07.xhtml_page_177)

while loop, [149](#9781284254884_CH06_06.xhtml_page_149)–[150](#9781284254884_CH06_07.xhtml_page_150)

whoami command, [269](#9781284254884_CH11_01.xhtml_page_269)

who command, [132](#9781284254884_CH06_04.xhtml_page_132)

whois command, [201](#9781284254884_CH08_02.xhtml_page_201)–[202](#9781284254884_CH08_02.xhtml_page_202)

wired network interface (enp0s3), [193](#9781284254884_CH08_01.xhtml_page_193)

wireless network cards, [59](#9781284254884_CH03_02.xhtml_page_59)

write permission, [239](#9781284254884_CH10_02.xhtml_page_239), [240](#9781284254884_CH10_02.xhtml_page_240)

X

XEN Project, [297](#9781284254884_CH12_02.xhtml_page_297)

Xfce desktops, [16](#9781284254884_CH01_04.xhtml_page_16)f, [16](#9781284254884_CH01_04.xhtml_page_16)t

X File System (XFS), [107](#9781284254884_CH05_04.xhtml_page_107), [111](#9781284254884_CH05_06.xhtml_page_111)

X11Forwarding configuration, [256](#9781284254884_CH10_07.xhtml_page_256)

XFS. [X File System](#9781284254884_Index.xhtml_ie0559)

xfs_admin tool, [111](#9781284254884_CH05_06.xhtml_page_111)

xfs_info tool, [111](#9781284254884_CH05_06.xhtml_page_111)

X.org package, [12](#9781284254884_CH01_04.xhtml_page_12)

xterm package, [126](#9781284254884_CH06_02.xhtml_page_126)

X Window software, [11](#9781284254884_CH01_03.xhtml_page_11)–[12](#9781284254884_CH01_04.xhtml_page_12)

Z

Zettabyte File System (ZFS), [108](#9781284254884_CH05_04.xhtml_page_108)

zsh shell, [121](#9781284254884_CH06_01.xhtml_page_121)