![](images/cover.jpg)

![Cover](images/cover.jpg)

Copyright © 2024 BPB Online

*All rights reserved.* No part of this book may be reproduced, stored in a retrieval system, or transmitted in any form or by any means, without the prior written permission of the publisher, except in the case of brief quotations embedded in critical articles or reviews.

Every effort has been made in the preparation of this book to ensure the accuracy of the information presented. However, the information contained in this book is sold without warranty, either express or implied. Neither the author, nor BPB Online or its dealers and distributors, will be held liable for any damages caused or alleged to have been caused directly or indirectly by this book.

BPB Online has endeavored to provide trademark information about all of the companies and products mentioned in this book by the appropriate use of capitals. However, BPB Online cannot guarantee the accuracy of this information.

First published: 2024

Published by BPB Online

WeWork

119 Marylebone Road

London NW1 5PU

**UK | UAE | INDIA | SINGAPORE**

ISBN 978-93-55515-735

[www.bpbonline.com](https://www.bpbonline.com)

**Dedicated to**

My Creator:

GOD Almighty

&

My loving Son **Matthew Zach Inshanally**

# About the Author

Philip Inshanally is a consultant with over 22+ years in the IT/ICT/OT industry and the first Guyanese IT Author to have written a US-based IT certification book (CompTIA Linux +, released in 2018). He is also the first Guyanese to have created international IT training video courses for various companies such as INE ([www.ine.com](https://www.ine.com)) and Cybrary (cybrary.it), to name a few. Furthermore, Philip is the only Cisco Certified Internetwork Expert (CCIE#61204) residing in Guyana, South America.

He has extensive experience in IT/ICT/OT consulting, Cybersecurity, Wireless technologies, Designing, Planning, Implementing, and Documenting various IT/ICT/OT environments.

As one of the industry’s leading IT/ICT/OT experts, he has a competitive edge due to his ongoing development and acquired excellent skills, which have helped him deal with customers locally and internationally.

He has always been methodical, detail-oriented, and production environment sensitive.

# About the Reviewer

Vijay Gaikwad is an accomplished Linux enthusiast with a diverse skill set. He has a keen focus on Linux security, hardening, command line, diagnostic, and troubleshooting aspects, ensuring the accuracy and relevance of technical content related to Linux. His passion for Linux and dedication to the IT community make him a reliable resource for individuals and teams seeking guidance on Linux systems, security, and cloud integration. Moreover, as an AWS Cloud Practitioner, he possesses a strong understanding of cloud concepts and services. Vijay's well-rounded personality and commitment to continuous growth and learning are evident in his love for music, particularly the guitar. When not immersed in complex technical challenges, he can often be found strumming his guitar strings, showcasing his dedication to technology and the arts.

# Acknowledgement

I want to express my gratitude to my Creator for bestowing his choicest blessings upon me. Also, my family and friends for their unwavering support and encouragement throughout this book's writing, especially my loving son Matthew Zach Inshanally.

I am also grateful to BPB Publications for their guidance and expertise in bringing this book to fruition. It was a long journey of revising this book, with valuable participation and collaboration of reviewers, technical experts, and editors.

I would also like to acknowledge the valuable contributions of my colleagues and co-worker during many years working in the tech industry, who have taught me so much and provided valuable feedback on my work.

Finally, I would like to thank all the readers who have taken an interest in my book and for their support in making it a reality. Your encouragement has been invaluable.

# Preface

The CompTIA Linux+ is a certification program offered by CompTIA, a non-profit trade association that provides vendor-neutral IT certifications. The Linux+ certification is designed to validate the skills and knowledge of IT professionals who work with the Linux operating system.

The Linux+ certification is suitable for individuals who want to demonstrate their proficiency in Linux administration, system configuration, maintenance, and basic networking. It is often pursued by those seeking to build a career in Linux system administration or other IT roles that involve working with Linux-based systems.

With this book, you will gain the necessary knowledge and skillset required for achieving the CompTIA Linux+ certification. I hope you will find this book informative and helpful.

[Chapter 1: Introduction to Linux Environment](#ch01.xhtml) - This chapter explains everything needed for the reader to understand the Linux File Hierarchy System (FHS), navigating between the directories, viewing configuration files, etc. It introduces various methods of identifying and locating hardware information from within the terminal environments. Furthermore, this chapter also explains and illustrates the Grand Unified Bootloader 2.

[Chapter 2: Files, Directories, and Storage](#ch02.xhtml) - This chapter presents various methods of file compression and focuses on various ways to manipulate files and directories from within the terminal environment. Furthermore, this chapter explains various ways of managing storage.

[Chapter 3: Processes, Services and Network Configuration](#ch03.xhtml) - This chapter covers various ways for identifying and managing process(s). Next, this chapter focuses on handling services from within the terminal environment, such as: starting and stopping process(s) / daemon(s), and the service vs systemctl command. Furthermore, this chapter covers network configuration both from within the Desktop and terminal environment.

[Chapter 4: Managing Modules and Software](#ch04.xhtml) - This chapter allows the reader to learn various methods of managing modules from within the terminal environment. Furthermore, this chapter places heavy emphasis on software management.

[Chapter 5: User and Password Management](#ch05.xhtml) - The reader will learn various methods for managing users, such as adding, removing, and updating user properties, etc. Next, this chapter focuses on group management and password management.

[Chapter 6: Firewall, Remote Access and SELinux](#ch06.xhtml) - The reader will learn to configure various methods of TCP wrappers, firewalld, and iptables, among others. Next, this chapter focuses on remote access, and the reader will learn to configure remote access. Furthermore, the reader will learn to configure SELinux, which provides an extra layer of access control and enforcement.

[Chapter 7: Shell Scripting and Containers](#ch07.xhtml) - This chapter explains shell scripting in detail, starting with the basic structure of a script, then moving on to the for loop, while loop, and conditionals. Furthermore, this chapter covers containers in depth, such as Linux containers (LXC), Docker.

[Chapter 8: Configuration Management with YAML, JSON and Ansible](#ch08.xhtml) - This chapter is dedicated to configuration management. First, this chapter focuses on YAML or YAML Ain’t Markup Language. Next, the reader will learn to manage configuration using JavaScript Object Notation (JSON). Furthermore, the reader will learn Ansible for configuration management.

[Chapter 9: Troubleshooting Network and System Issues](#ch09.xhtml) - This chapter explains various methods of troubleshooting. First, this chapter focuses on network troubleshooting, tools such as ping, ping6, traceroute, traceroute6, to name a few. Next, the reader will learn to troubleshoot common memory issues using tools such as free, top, among others. Following this, the reader will learn to troubleshoot hard disk problems using commands such as smartctl, iotop, to name a few. Furthermore, the reader will learn how to troubleshoot common boot issues by examining various log files and using commands such as fsck, mount, and many more.

[Chapter 10: Mock Exams](#ch10.xhtml) - The reader will be presented with two mock exams. The format of the questions is multiple choice in both mock exams. Furthermore, the questions cover materials learned throughout this book.

# Code Bundle and Coloured Images

Please follow the link to download the

***Code Bundle*** and the ***Coloured Images*** of the book:

[https://rebrand.ly/6dbjtst](https://rebrand.ly/6dbjtst)

The code bundle for the book is also hosted on GitHub at [https://github.com/bpbpublications/CompTIA-LinuxPlus-XK0-005-Reference-Guide](https://github.com/bpbpublications/CompTIA-LinuxPlus-XK0-005-Reference-Guide). In case there’s an update to the code, it will be updated on the existing GitHub repository.

We have code bundles from our rich catalogue of books and videos available at [**https://github.com/bpbpublications**](https://github.com/bpbpublications). Check them out!

Errata

We take immense pride in our work at BPB Publications and follow best practices to ensure the accuracy of our content to provide with an indulging reading experience to our subscribers. Our readers are our mirrors, and we use their inputs to reflect and improve upon human errors, if any, that may have occurred during the publishing processes involved. To let us maintain the quality and help us reach out to any readers who might be having difficulties due to any unforeseen errors, please write to us at :

**[errata@bpbonline.com](mailto:errata@bpbonline.com)**

Your support, suggestions and feedbacks are highly appreciated by the BPB Publications’ Family.

**Join our book’s Discord space**

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 1Introduction to Linux Environment](#contents.xhtml_ch01a)

[Introduction](#contents.xhtml_sc1a)

In this chapter, we will learn about the Linux Filesystem Hierarchy Standard (FHS) directories. Next, we will look for ways to obtain hardware information from the terminal environment. Finally, we will wrap this chapter with GRUB2.

[Structure](#contents.xhtml_sc2a)

This chapter will discuss the following topics:

*   Filesystem hierarchy standard
*   Finding hardware information
*   Grand Unified Bootloader 2

[Objectives](#contents.xhtml_sc3a)

By the end of this chapter, you will be able to understand filesystem structure. You will become accustomed to directories and how they are used. It will be easier for you to locate hardware. Grand Unified Bootloader 2 will also be introduced to you through this chapter.

[Filesystem hierarchy standard](#contents.xhtml_sc4a)

When the term FHS is referenced, think of directory structure. You will find on almost all the Linux distributions, the FHS is identical. It defines the directory structure and content in UNIX-like operating systems such as Linux distros.

The need for a standardized filesystem hierarchy arose from the diverse nature of early Unix systems, where file organization varied significantly across different implementations. The FHS project was initiated in the early 1990s by the Free Standards Group (now the Linux Foundation) to address this issue. Its primary objective was to establish a typical structure simplifying software development, administration, and package management across Linux distributions.

[Key principles of the FHS](#contents.xhtml_sc5a)

The FHS is guided by several fundamental principles that shape its design and implementation. These principles include:

*   Filesystem hierarchy: The FHS defines a consistent structure for organizing files and directories. It categorizes them based on purpose, ensuring each component has a specific role within the hierarchy.
*   Compatibility: The FHS aims to maintain compatibility across different Linux distributions. By adhering to the standard, software developers and administrators can create and manage applications that work seamlessly across various systems.
*   Compliance: Linux distributions seeking FHS compliance must adhere to specific guidelines to ensure consistent placement of files and directories. This promotes portability and simplifies the packaging and installation of software.

Across the various Linux Distros, the configuration files will usually be in the exact location regardless of Linux distribution (the /etc directory). This makes developing software for Linux much more accessible since software developers do not have to write different versions of applications for each distribution.

In the FHS environment, the files and directories appear under the root directory (/); this root directory is the parent of all other directories and sits at the top of the FHS.

A list of the commonly used directories across Linux distros is as follows:

*   /: The root directory, this is the top-level directory. It is the parent for all other directories.
*   /root/: The home directory of the root user.
*   /boot: It contains files relating to system boot, such as the bootloader configurations, kernel images, and initial RAM disk (initram) files.
*   /bin: The critical executable files that are necessary for system operations.
*   /dev: It contains device files like hard disks or CD-ROMs.
*   /sbin: It is similar to /bin but contains programs generally run by the root user.
*   /etc: It contains configuration files.
*   /home: This is the user’s home directory.
*   /lib: It contains libraries on 32-bit systems.
*   /lib64: It contains libraries on 64-bit systems.
*   /media: It is the mount point for removable media, usually used for auto-mounting external media.
*   /mnt: It is the mount point for removable media manually.
*   /usr: It contains most user utilities (/usr/bin/, /usr/lib/, etc.).
*   /var: This contains the various files such as logs (auth, syslog), web server content, and package cache.
*   /tmp: This contains temporary files created by programs.
*   /proc: A virtual filesystem containing various runtime information such as devices, bus, interrupts, CPU, RAM, etc.

Now, let us look at the directories at the terminal using Ubuntu and Centos distributions.

The root (/) directory resides at the top of the directory structure. Using Ubuntu, let us check out our current working directory using the pwd command. Consider [Figure 1.1](#ch01.xhtml_fig1-1):

![](images/Figure_1.1.png)

Figure 1.1: Present working directory

Now, let us check the content of the root (/) directory using the ls command.

Consider [Figure 1.2](#ch01.xhtml_fig1-2):

![](images/Figure_1.2.png)

Figure 1.2: Output of the ls command

We can see that the root (/) directory contains a range of other directories. For a hierarchical view, let us leverage the tree with the -d option (directory) command.

Consider [Figure 1.3](#ch01.xhtml_fig1-3):

![](images/Figure_1.3.png)

Figure 1.3: Output of the tree command with -d option

Switch to our Centos system and check the root (/) directory.

Consider [Figure 1.4](#ch01.xhtml_fig1-4):

![](images/Figure_1.4.png)

Figure 1.4: Output of the ls command with a similar structure

As shown above, the structure is similar. Let us use the tree command with the -d option for a hierarchical view. Consider [Figure 1.5](#ch01.xhtml_fig1-5):

![](images/Figure_1.5.png)

Figure 1.5: Output of the tree command with the -d option for a hierarchical view

Now, look at the content of the /bin directory using the ls command. We will see a variety of commands which are a part of the operating system. Consider [Figure 1.6](#ch01.xhtml_fig1-6):

![](images/Figure_1.6.png)

Figure 1.6: Output of ls command with the bin directory

In contrast, in the /usr directory, you will notice some similarities inside the /usr/bin directory. However, the /bin is part of the core operating system and must be accessible before the /usr directory gets mounted. Consider [Figure 1.7](#ch01.xhtml_fig1-7):

![](images/Figure_1.7.png)

Figure 1.7: Contents of the /usr/bin directory

Another commonly used directory for configuration files is the /etc directory. To change between directories, we would use the cd command, as illustrated in [Figure 1.8](#ch01.xhtml_fig1-8):

![](images/Figure_1.8.png)

Figure 1.8: Contents of the /etc directory

We can leverage the cat command and look at the /etc/resolv.conf to view any of these files containing configurations relating to DNS settings. Consider [Figure 1.9](#ch01.xhtml_fig1-9):

![](images/Figure_1.9_(1).png)

Figure 1.9: Content of the /etc/resolv.conf

Now, look at the /var directory. Here, we are going to see the various log files as shown in [Figure 1.10](#ch01.xhtml_fig1-10):

![](images/Figure_1.10_(1).png)

Figure 1.10: Content of the /var/log/auth.log

The /var/log/auth.log contains system authorization information, user logins, and authentication mechanisms.

Another popular log file is the /var/log/syslog, and we will use the head command as the output of the file that will usually run off the screen. Consider [Figure 1.11](#ch01.xhtml_fig1-11):

![](images/Figure_1.11.png)

Figure 1.11: Output of the /var/syslog

Over on our Centos machine, there is no log file named syslog, but instead, it is called messages, as shown in [Figure 1.12](#ch01.xhtml_fig1-12):

![](images/Figure_1.12.png)

Figure 1.12: Content of the /var/log directory

The contents of the /var/log/messages in the Centos machine are like that of the /var/log/syslog. Consider [Figure 1.13](#ch01.xhtml_fig1-13):

![](images/Figure_1.13.png)

Figure 1.13: Content of the /var/log/messages

To view the contents of the /var/log/messages on the Centos machine, you will require administrative privileges or be the root user. We will discuss more on this in [Chapter 6](#ch06.xhtml), Firewall remote access and SELinux.

When we are looking for kernel messages, there is /var/log/kern.log file; like the syslog  file, the output of this file is lengthy, so we will use the head command once again for illustration, as shown in [Figure 1.14](#ch01.xhtml_fig1-14):

![](images/Figure_1.14.png)

Figure 1.14: Content of the /var/log/kern.log

Another commonly used directory is the /lib directory which holds essential libraries, as shown in [Figure 1.15](#ch01.xhtml_fig1-15):

![](images/Figure_1.15_(1).png)

Figure 1.15: Content of the /lib directory

Each user also has their home directory; in our case, only one user exists. Let us check out the /home directory for our existing users. Consider [Figure 1.16](#ch01.xhtml_fig1-16):

![](images/Figure_1.16.png)

Figure 1.16: Content of the /home/philip directory

We can also leverage the tree command by itself to view all the directories and files in a hierarchical structure, as shown in [Figure 1.17](#ch01.xhtml_fig1-17):

![](images/Figure_1.17.png)

Figure 1.17: Directory displayed using the tree command

We will look at user creation in [Chapter 5](#ch05.xhtml), User and password management.

We can also view hidden files within a directory by using the ls command with the -a option, as shown in [Figure 1.18](#ch01.xhtml_fig1-18):

![](images/Figure_1.18.png)

Figure 1.18: Viewing hidden file(s) using the ls command with -a option

Note: The hidden files are prepended with a period (.).

[Finding hardware information](#contents.xhtml_sc6a)

In Linux, you can use various command-line tools to obtain hardware information from the terminal. Here are some commonly used commands:

*   lscpu: This command displays detailed information about the CPU (processor) on your system, including the number of cores, architecture, clock speed, and more.
*   lsblk: It lists information about block devices attached to your system, such as hard drives and SSDs. It shows details like device names, sizes, and mount points.
*   blkid: It provides block device attributes.
*   lspci: It provides information about Peripheral Component Interconnect (PCI) devices connected to your system, including graphics cards, network adapters, and sound cards.
*   lsusb: This command lists USB devices attached to your system, such as keyboards, mice, printers, and USB storage devices.
*   Lsmod: View modules that are in use for free-view RAM information.
*   Hwinfo: It is a comprehensive hardware tool that provides detailed information about various hardware components, including CPU, memory, storage, network adapters, and more.
*   dmidecode: This command retrieves information from the system's Desktop Management Interface (DMI) table, which contains details about the hardware components, BIOS, and system manufacturer.
*   Inxi: It is a versatile command that provides detailed information about various hardware components and system configurations in a user-friendly format. It can display details about the CPU, memory, storage, graphics, and more.
*   df: Displays the disk space usage of file systems.
*   du: This command retrieves the disk usage of directories and files.

Note. You can also leverage the /proc/ directory to obtain various information about hardware, such as the CPU, RAM, interrupts, etc.

Let us look at the lscpu command in our Centos system. Consider [Figure 1.19](#ch01.xhtml_fig1-19):

![](images/Figure_1.19.png)

Figure 1.19: Output of the lscpu command

From the above output, information regarding the CPU is displayed such as the architecture, vendor, core(s) per socket, etc.

Now, let us look at the lsblk command in our Ubuntu system, as shown in [Figure 1.20](#ch01.xhtml_fig1-20):

![](images/Figure_1.20.png)

Figure 1.20: Output of the lsblk command

We can see various block devices' respective mount points, sizes, and types.

Continuing our journey with block devices, we will use the blkid command to view attributes as shown on our CentOS system in [Figure 1.21](#ch01.xhtml_fig1-21):

![](images/Figure_1.21.png)

Figure 1.21: Output of the blkid command

The UUID and the label are exposed for the block device(s).

Now, let us look at our PCI information, such as host, PCI, ISA, etc. using the lspci command as shown in [Figure 1.22](#ch01.xhtml_fig1-22):

![](images/Figure_1.22.png)

Figure 1.22: Output of the lspci command

To view information about USB devices, we can leverage the lsusb command, as shown in [Figure 1.23](#ch01.xhtml_fig1-23):

![](images/Figure_1.23.png)

Figure 1.23: Output of the lsusb command

When we would like to view the currently loaded modules, we can take advantage of the lsmod command, as shown in [Figure 1.24](#ch01.xhtml_fig1-24):

![](images/Figure_1.24.png)

Figure 1.24: Output of the lsmod command

The free command can be used to view RAM in the system. The default will be displayed in Kibibytes (in Linux and most operating systems) if used without any option. A kibibyte is equal to 1024, or 2^10, bytes. A kilobyte is also 1024 bytes, but there are exceptions. As defined by the International System of Units, the prefix kilo refers to 1000 or 10^3. Most storage manufacturers measure and label capacity in base 10 (1 kilobyte = 1000 bytes; 1 megabyte = 1000 kilobytes; 1 gigabyte = 1000 megabytes; 1 terabyte = 1000 gigabytes). However, RAM vendors and most operating systems use base 2 (1 kilobyte = 1024 bytes; 1 megabyte = 1024 kilobytes; 1 gigabyte = 1024 megabytes; 1 terabyte = 1024 gigabytes). We can use the -g option to consider in Gibibytes or the -m option, which will display the RAM in Mebibytes as shown in [Figure 1.25](#ch01.xhtml_fig1-25):

![](images/Figure_1.25.png)

Figure 1.25: Output of the free command

To get more information regarding the hardware in the system, there is yet another helpful command, the hwinfo command, as shown in [Figure 1.26](#ch01.xhtml_fig1-26):

![](images/Figure_1.26.png)

Figure 1.26: Output of the hwinfo command with the --short option

As shown above, the output will run off the screen. Using the --short option displays an overview of the hardware.

We can view specific hardware using keywords like disk, memory, network, etc.

This example displays hard disk information as shown in [Figure 1.27](#ch01.xhtml_fig1-27):

![](images/Figure_1.27.png)

Figure 1.27: Output of the hwinfo command with the --disk option

The following figure shows memory-specific hardware information:

![](images/Figure_1.28.png)

Figure 1.28: Output of the hwinfo command with the --memory option

We can utilize the df command to view the disk space usage of the filesystem. Using the -h displays in a human-readable format as shown in [Figure 1.29](#ch01.xhtml_fig1-29):

![](images/Figure_1.29.png)

Figure 1.29: Output of the df command with the -h option

If we would like to see disk usage for a directory, we can utilize the du command; adding the -h option will display the values in the human-readable format, as shown in [Figure 1.30](#ch01.xhtml_fig1-30):

![](images/Figure_1.30.jpg)

Figure 1.30: Output of the du command with the -h option

[Grand Unified Bootloader 2](#contents.xhtml_sc7a)

Grand Unified Bootloader 2 (GRUB2) is an open-source bootloader widely used in Linux-based operating systems. It plays a crucial role in the boot process, allowing users to select and launch their preferred computer operating systems.

The primary purpose of GRUB2 is to load the operating system kernel into memory and transfer control to it. The boot menu provides a user-friendly interface where users can choose from multiple installed operating systems or different boot options. GRUB2 supports various operating systems, including Linux distributions, BSD, and Windows.

One of the critical improvements of GRUB2 over its predecessor, GRUB Legacy, is its enhanced flexibility and compatibility. GRUB2 supports Basic Input/Output System (BIOS) and Unified Extensible Firmware Interface (UEFI) boot modes, making it compatible with various hardware platforms. It also supports multiple filesystems, such as ext4, Btrfs, XFS, and NTFS, allowing it to handle different storage configurations.

GRUB2 has a modular architecture consisting of a core image and dynamically loadable modules. The core image contains the essential functionality required for bootings, such as disk access, filesystem drivers, and menu handling. Additional modules can be loaded at runtime to provide extra features and support for specific filesystems or hardware devices. This modular design allows it to be flexible and easily extensible.

The installation and configuration of GRUB2 may vary slightly depending on the Linux distribution. Typically, the installation process involves installing the GRUB2 package and configuring it as the default boot loader. During installation, it copies the core image and necessary modules to the boot partition or the EFI system partition in the case of UEFI systems.

GRUB2's main configuration file is grub.cfg, located in the /boot/grub directory. This file contains the boot menu entries, which specify the location of the kernel, initial RAM disk, and other boot parameters for each operating system. Users can modify this file manually to customize the boot menu, change default options, set timeout values, and implement advanced features like password protection.

Customization options in GRUB2 go beyond the configuration file. Users can customize the appearance of the boot menu by modifying themes and adding background images. It also supports scripting, allowing users to automate boot tasks, create conditional statements, and perform advanced configurations. In addition, users can add/remove other Linux kernels and Operating Systems, such as Microsoft Windows, to the GRUB2 boot menu.

In addition to the basic functionality, GRUB2 offers advanced features and functionality. It provides a command-line interface allowing users to interact directly with the boot loader. This interface can help troubleshoot boot issues, modify boot options on the fly, and perform system maintenance tasks.

It also supports secure boot, a feature in UEFI systems that verifies the boot process's integrity to protect against unauthorized code execution. GRUB2 can be configured to work seamlessly with secure boot, ensuring the safe and trustworthy booting of the system.

Troubleshooting GRUB2-related issues is facilitated by features such as rescue mode and recovery options. In case of misconfigurations or boot failures, users can enter the rescue mode to access a command-line interface and attempt to fix the issues manually. GRUB2 also provides tools for reinstalling or restoring the bootloader in case of critical failures.

Furthermore, GRUB2 supports advanced topics like network booting, which allows booting an operating system over the network, and virtualization, enabling the launch of virtual machines directly from the boot menu.

GRUB2 continues to evolve with ongoing development and enhancements. The GNU Project maintains it and benefits from contributions from the open-source community. New features, bug fixes, and improvements are regularly introduced to address emerging technologies, hardware advancements, and user requirements.

We can look at the GRUB2 configuration file on our Ubuntu system. Consider [Figure 1.31](#ch01.xhtml_fig1-31):

![](images/Figure_1.31.png)

Figure 1.31: Contents of the /boot/grub/grub.cfg

Some of the above output has been omitted for brevity. Each entry has BEGIN and END comments. The menu entry represents the boot options (kernel, Windows OS version) which are displayed on the boot screen upon system boot, as shown in [Figure 1.32](#ch01.xhtml_fig1-32):

![](images/Figure_1.32.png)

Figure 1.32: Contents of the /boot/grub/grub.cfg

Over on our CentOS system, the grub configuration file resides in the /boot/grub2/grub.cfg as shown in [Figure 1.33](#ch01.xhtml_fig1-33):

![](images/Figure_1.33.png)

Figure 1.33: Contents of the /boot/grub2/grub.cfg

[Working with GRUB2](#contents.xhtml_sc8a)

We can add our custom boot entry, and we will first create a custom boot file and save it in the /etc/grub.d/40_custom configuration file. We will use the Ubuntu system for this demo, as shown in [Figure 1.34](#ch01.xhtml_fig1-34):

![](images/Figure_1.34.png)

Figure 1.34: Contents of the /etc/grub.d/40_custom configuration file

We will edit this file using a text editor, add our entry at the bottom and save the changes.

Consider [Figure 1.35](#ch01.xhtml_fig1-35):

![](images/Figure_1.35.png)

Figure 1.35: Editing /etc/grub.d/40_custom configuration file

Based on the above output, the entry defines the boot entry parameters. The next step is to run the grub-mkconfig command, which will write the changes so that the /boot/grub/grub.cfg knows of the existence of our custom entry. Refer to [Figure 1.36](#ch01.xhtml_fig1-36):

![](images/Figure_1.36.png)

Figure 1.36: Output of the grub-mkconfig command

Some output was omitted for brevity. Finally, we will increase the timer value inside the /etc/default/grub configuration file to see the boot screen upon reboot. The GRUB_TIMEOUT is currently set to 0, as shown in [Figure 1.37](#ch01.xhtml_fig1-37):

![](images/Figure_1.37.png)

Figure 1.37: Contents of the /etc/default/grub configuration file

We will change the GRUB_TIMEOUT=0 to GRUB_TIMEOUT=10 and change the value of GRUB_TIMEOUT_STYLE=hidden to GRUB_TIMEOUT_STYLE=menu as shown in [Figure 1.38](#ch01.xhtml_fig1-38):

![](images/Figure_1.38.png)

Figure 1.38: Contents of the /etc/default/grub configuration file with changed values

Now let us run the update-grub command as shown in [Figure 1.39](#ch01.xhtml_fig1-39):

![](images/Figure_1.39.png)

Figure 1.39: Output of the update-grub command

Upon reboot, we can see our new boot entry listed as shown in [Figure 1.40](#ch01.xhtml_fig1-40):

![](images/Figure_1.40.png)

Figure 1.40: Output of the GRUB2 boot menu

In conclusion, GRUB2 is a powerful and versatile boot loader critical to the boot process in Linux-based operating systems. Its flexible architecture, compatibility with various hardware platforms, extensive customization options, and advanced features make it the preferred choice for boot management in the Linux ecosystem.

[Conclusion](#contents.xhtml_sc9a)

In this chapter, we covered the Linux filesystem hierarchy standard, locating hardware information, and we finished off this chapter by working with GRUB2.

In the next chapter, we will cover files, directories, and storage.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 2Files, Directories, and Storage](#contents.xhtml_ch02a)

[Introduction](#contents.xhtml_sc10a)

In the previous chapter, we covered various directories that comprise the Linux Filesystem Hierarchy Standard (FHS). After that, we looked at ways to obtain hardware information from the terminal environment. Finally, we wrapped it with GRUB2.

In this chapter, we will focus on Files, Directories, and Storage. First, we will look at file compression and then cover file and directory operations. Following this, we will cover filesystem management. Finally, we will wrap this chapter with Logical Volume Management (LVM).

[Structure](#contents.xhtml_sc11a)

We will discuss the following topics in this chapter:

*   File compression
*   File and directory operations
*   Pipes and redirects
*   Filesystem management
*   Using the parted utility
*   Steps to format a hard disk
*   Mounting and unmounting a partition
*   Logical volume management

[Objectives](#contents.xhtml_sc12a)

This chapter will teach us to manipulate and manage files and directories. We will learn about file compression and files and directory operations in detail. We will also focus on configuring the storage.

[File compression](#contents.xhtml_sc13a)

File compression is the process of reducing the size of files and directories to save storage space, enhance transfer speed, and simplify file management. In Linux, there are various compression algorithms and tools available to accomplish this task.

[Compression algorithms](#contents.xhtml_sc14a)

Linux offers several compression algorithms, each with its own characteristics and trade-offs. Here are some commonly used ones:

*   Gzip: It uses the DEFLATE algorithm and is widely supported on Linux. It compresses files into a single archive with the .gz extension. To compress a file using gzip, use the following command:

gzip file.txt

This creates a compressed file named file.txt.gz.

*   Bzip2: It utilizes the Burrows-Wheeler Transform and Run-Length Encoding algorithms. It provides higher compression ratios than gzip but requires more processing time. To compress a file using bzip2, use the command:

bzip2 file.txt

This creates a compressed file named file.txt.bz2.

*   Xz: It employs the LZMA/LZMA2 algorithm and offers better compression ratios than bzip2. It is particularly suitable for compressing large files. To compress a file using xz, use the command:

xz file.txt

This creates a compressed file named file.txt.xz.

*   Zip: It is a popular compression format compatible with various operating systems. It supports compressing multiple files and directories into a single archive. To create a zip archive, use the command:

zip archive.zip file1.txt file2.txt

This creates an archive named archive.zip containing file1.txt and file2.txt.

[Compressing files](#contents.xhtml_sc15a)

To compress files using Linux compression tools, you need to use specific commands. Here are some examples:

*   gzip

gzip file.txt: compresses file.txt using gzip and creates file.txt.gz.

*   bzip2

bzip2 file.txt: compresses file.txt using bzip2 and creates file.txt.bz2.

*   xz

xz file.txt: compresses file.txt using xz and creates file.txt.xz.

*   zip

zip archive.zip file1.txt file2.txt: creates a zip archive named archive.zip containing file1.txt and file2.txt.

[Compressing directories](#contents.xhtml_sc16a)

Linux allows you to compress entire directories while preserving their structure. Here are examples of compressing directories:

*   gzip

tar -czf archive.tar.gz directory/: creates (-c) a tarball called archive.tar.gz by compressing the directory (-f) using (-z) gzip.

*   bzip2

tar -cjf archive.tar.bz2 directory/: creates a tarball called archive.tar.bz2 by compressing the directory using (-j) bzip2.

*   xz

tar -cJf archive.tar.xz directory/: creates a tarball called archive.tar.xz by compressing the directory using (-J) xz.

*   zip

zip -r archive.zip directory/: creates a zip archive named archive.zip by recursively (-r) compressing the directory and its contents.

[Decompressing files and directories](#contents.xhtml_sc17a)

Once files or directories are compressed, they can be decompressed to their original state. Here are examples of decompression:

*   gzip

gunzip file.txt.gz decompresses file.txt.gz using gzip.

*   bzip2

bunzip2 file.txt.bz2 decompresses file.txt.bz2 using bzip2.

*   xz

unxz file.txt.xz decompresses file.txt.xz using xz.

*   zip

unzip archive.zip decompresses archive.zip and extracts its contents.

[Advanced compression techniques](#contents.xhtml_sc18a)

Linux provides additional options and techniques for file compression. Some notable ones include:

*   Archive: Combining compression and archiving in one step, you can create compressed tarballs directly.

For example, tar -czf archive.tar.gz file1.txt file2.txt.

*   Compression levels: Compression tools often offer different levels of compression, allowing you to prioritize either compression ratio or processing speed.

For example, gzip -9 file.txt sets the maximum compression level for gzip.

*   Parallel compression: Some compression tools support parallel compression, utilizing multiple processor cores to speed up compression and decompression.

For example, pigz file.txt is a parallel implementation of gzip.

*   Stream compression: Linux allows compressing data streams on-the-fly, which is useful for efficient transfer or backup scenarios.

For example, tar cf - directory/ | gzip > archive.tar.gz creates a compressed tarball of directory directly to archive.tar.gz without creating an intermediate file.

[Compression with compression libraries](#contents.xhtml_sc19a)

Linux also provides compression libraries that can be utilized in programming languages such as C, C++, and Python. Some popular libraries include zlib, libbz2, and lzma-sdk. These libraries allow developers to integrate compression capabilities into their own software applications.

[File and directory operations](#contents.xhtml_sc20a)

To begin with, we need to be familiar with working at the CLI. Throughout the previous chapter, we have been interacting with the shell. Now we want to become efficient in our CLI skills. When we first open a terminal, we are placed into the user’s home directory.

As can be seen here:

[philip@localhost ~]$

From the above output, we are placed into the home directory of the user Philip. This can be confirmed by issuing the pwd command:

[philip@localhost ~]$ pwd

/home/philip

[philip@localhost ~]$

From the above output, we have confirmed that we are indeed in the /home/philip directory. However, it gets even more interesting. There are various directories inside the /home/philip. We can confirm this by using the ls command:

[philip@localhost ~]$ ls

Desktop Documents Downloads Music Pictures Public Templates Videos

[philip@localhost ~]$

From the above output, the directories, also known as folders listed, are created for each user in the system. Now the way the directories are displayed does not really tell us a lot. To dig deeper, we can issue the ls command once again, but this time, we will pass the -l option:

[philip@localhost ~]$ ls -l

total 32

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Desktop

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Documents

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Downloads

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Music

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Pictures

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Public

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Templates

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Videos

[philip@localhost ~]$

From the above output, we get some useful info. For instance, there are permissions for each directory; also, we can see ownership and size, to name a few. Adding to this, in Linux, we have what are known as hidden files/folders. By default, they are not displayed when we do a listing; we would need to also tag on the -a option:

[philip@localhost ~]$ ls -al

drwx------. 15 philip philip 4096 Aug 2 10:28 .

drwxr-xr-x. 3 root root 4096 Jul 31 14:58 ..

-rw-r--r--. 1 philip philip 18 Mar 15 09:56 .bash_logout

-rw-r--r--. 1 philip philip 193 Mar 15 09:56 .bash_profile

-rw-r--r--. 1 philip philip 231 Mar 15 09:56 .bashrc

drwx------. 14 philip philip 4096 Jul 31 14:59 .cache

drwx------. 14 philip philip 4096 Jul 31 14:59 .config

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Desktop

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Documents

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Downloads

-rw-------. 1 philip philip 16 Jul 31 14:58 .esd_auth

-rw-------. 1 philip philip 620 Aug 2 10:28 .ICEauthority

drwx------. 3 philip philip 4096 Jul 31 14:59 .local

drwxr-xr-x. 4 philip philip 4096 Apr 25 02:33 .mozilla

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Music

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Pictures

drwxrw----. 3 philip philip 4096 Jul 31 14:59 .pki

[philip@localhost ~]$

The way we can tell whether a file or directory is hidden is that they begin with a period in front of the name of the file or folder. To move between directories, we would use the cd command. Change Director (CD) allows us to navigate the Linux file system. So, let us move to the /home/philip/Documents. We would use the following code:

[philip@localhost ~]$ cd /home/philip/Documents

[philip@localhost Documents]$

There is also another way to move between directories. The first method which we used is known as the absolute path, meaning we specified the complete path to the directory. The next method to move between the directories would be to specify the relative path:

[philip@localhost ~]$ cd Documents/

[philip@localhost Documents]$

Note: You would need to be in the parent directory of the child directory for the relative method to work.

Once we are in the child directory, we can run the ls command:

[philip@localhost Documents]$ ls

[philip@localhost Documents]$

Currently, there is no content in this directory. To move back up to the parent directory, we can use the cd command in this manner:

[philip@localhost Documents]$ cd /home/philip

[philip@localhost ~]$ pwd

/home/philip

[philip@localhost ~]$

From the above output, we specified the path. This method will always work. We can also use the cd command in this manner:

[philip@localhost Documents]$ cd ..

[philip@localhost ~]$

Using the above method, we used a double period. The double period means the parent directory. If we specified a single period, then this would be the outcome:

[philip@localhost Documents]$ cd .

[philip@localhost Documents]$

The single period references the current directory itself. The last method can be used in a directory regardless of where you are:

[philip@localhost Documents]$ cd ~

[philip@localhost ~]$

The tilde (~) character will always bring us back to the home directory of the user. To illustrate this, we will go to the /etc directory:

[philip@localhost ~]$ cd /etc

[philip@localhost etc]$ pwd

/etc

[philip@localhost etc]$

Now we will issue the cd command once again and pass the tilde (~):

[philip@localhost etc]$ cd ~

[philip@localhost ~]$ pwd

/home/philip

[philip@localhost ~]$

We can see the power of the tilde (~) character. At the very top of the file system hierarchy lies the root. We usually refer to the root as /; this is not to be confused with the /root directory. The latter is the home directory of the root user. From the /, every other directory is created. We can go to the / by:

[philip@localhost ~]$ cd /

[philip@localhost /]$ pwd

/

[philip@localhost /]$

From the above, we are placed at the root of the file system. We can view this directory like the other directories:

[philip@localhost /]$ ls

bin dev home lib64 media opt root sbin sys usr

boot etc lib lost+found mnt proc run srv tmp var

[philip@localhost /]$

You will notice that we have some familiar directories here, such as /home, /dev, to name a few. Interestingly, we see the /root directory listed. We can change to that directory and do a listing:

[philip@localhost /]$ cd /root

bash: cd: /root: Permission denied

[philip@localhost /]$

The reason that we got this error is because we do not have permission to view the /root directory. Let us authenticate as the root and retry:

[root@localhost /]# cd /root

[root@localhost ~]#

We are placed into the /root directory. This time when we do a listing, we will notice right off the bat that this is not the / directory:

[root@localhost ~]# ls

anaconda-ks.cfg

[root@localhost ~]#

Based on the above output, navigating the directory structure is intuitive.

[Creating, copying, moving, renaming, removing files](#contents.xhtml_sc21a)

This section sounds like a mouthful. Not to worry; we work with files on a daily basis. We can use the ls command on the /home/philip/Documents/NewTest directory:

philip@localhost Documents]$ cd NewTest/

[philip@localhost NewTest]$ ll -a

total 8

drwxrwxr-x. 2 philip philip 4096 Aug 6 12:04 .

drwxr-xr-x. 3 philip philip 4096 Aug 6 13:45 ..

[philip@localhost NewTest]$

Currently, they are not any files inside this directory. In Linux we can create a file from a shell; we would use the touch command to accomplish this:

[philip@localhost NewTest]$ touch OurFile

[philip@localhost NewTest]$ ll

total 0

-rw-rw-r--. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

When we created the file, it was created using some default permissions. Notably, the section where there are (-rw-rw-r--) means the user (-rw), the group (-rw), and the other (-r--). The first dash (-) references the file type. In this case, it is a regular file. The (rw-) means that the user/owner has read and write permissions. The second set of (rw-) means that the group also has read and executed. Lastly, the (r--) means that other/everyone else has read permission. Also, the part which states philip philip refers to the owner of the file and the group to which the file belongs. We change these permissions for this file; we would use the chmod command. Let us say that we want to give others/everyone else the (read and write) permissions. This would be:

[philip@localhost NewTest]$ chmod o+w OurFile

[philip@localhost NewTest]$ ll

total 0

-rw-rw-rw-. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

We can now see that the other permissions are (rw-). There is also another way to change the permission rather than using the (o+w). We could use the numerical value. We will change back the other to (r--) using the numerical format:

[philip@localhost NewTest]$ chmod 664 OurFile

[philip@localhost NewTest]$ ll

total 0

-rw-rw-r--. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

The way we read this, the (644) means: (6 -read and write, 6 -read and write, 4 -read). The first digit is a placeholder for the user. The second digit is a placeholder for the group and the last digit is a placeholder for the other. To further illustrate this, we can take off the (read) and leave the (write) for the group:

[philip@localhost NewTest]$ chmod 624 OurFile

[philip@localhost NewTest]$ ll

total 0

-rw--w-r--. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

Similarly, we can add permission by increasing the value. Let us pick others; we will give others the (read and execute) permissions:

[philip@localhost NewTest]$ chmod 625 OurFile

[philip@localhost NewTest]$ ll

total 0

-rw--w-r-x. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

We can even give all the permissions (read, write, and execute) for either the user, group or others in a single command. Let us start with the user:

[philip@localhost NewTest]$ ll

total 0

-rwx-w-r-x. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

Now we can see that the user has (read, write and execute) permissions. We got the value of 7 by adding (read =4, write=2, execute=1). We will now give the group all the permissions:

[philip@localhost NewTest]$ chmod 775 OurFile

[philip@localhost NewTest]$ ll

total 0

-rwxrwxr-x. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

We can also take off all the permissions for the user, group, or others in a single command. Let us take off the permissions (read, write, and execute) for the others:

[philip@localhost NewTest]$ chmod 770 OurFile

[philip@localhost NewTest]$ ll

total 0

-rwxrwx---. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

By placing a zero (0), this negates all permissions for the section (user, group, others). We can see the power of permissions. Similarly, we can use letters, as seen earlier. The (u) means user, (g) means group, and (o) means others. We could take the (execute) permission off the group like this:

[philip@localhost NewTest]$ chmod g-x OurFile

[philip@localhost NewTest]$ ll

total 0

-rwxrw----. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

We would use either a plus (+) symbol to add permission or a minus (-) symbol to remove permission. We can also copy a file from one location to another or inside the same location. A different name would need to be given if the destination for the file is inside the same location as the source. The cp command is used for copying. We will make a copy of the file created and place it in /home/philip/Documents/:

[philip@localhost NewTest]$ cp OurFile /home/philip/Documents/NewFile

[philip@localhost NewTest]$ ll /home/philip/Documents/

-rwxrw----. 1 philip philip 0 Aug 6 14:34 NewFile

drwxrwxr-x. 2 philip philip 4096 Aug 6 13:52 NewTest

[philip@localhost NewTest]$

Note: Directories all have a (d) in front of the permissions.

We can also move a file; the mv command would be used for moving files. Let us move the /home/philip/Documents/NewFile and place it inside the /home/philip/Documents/NewTest:

[philip@localhost NewTest]$ mv /home/philip/Documents/NewFile .

[philip@localhost NewTest]$ ll

-rwxrw----. 1 philip philip 0 Aug 6 14:34 NewFile

-rwxrw----. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

Now the method we used here was to specify a period (.) for the location. This means the current working directory; so instead of typing out the full destination path, we simply use the period (.)

We can also rename a file by using the mv command. Let us rename the NewFile:

[philip@localhost NewTest]$ mv NewFile RenameFile

[philip@localhost NewTest]$ ll

total 0

-rwxrw----. 1 philip philip 0 Aug 6 13:52 OurFile

-rwxrw----. 1 philip philip 0 Aug 6 14:34 RenameFile

[philip@localhost NewTest]$

We can also rename a file and place it in another directory; we would:

[philip@localhost NewTest]$ mv RenameFile /home/philip/Documents/

[philip@localhost NewTest]$ ll

-rwxrw----. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$

The file is no longer inside the present directory, but instead it is inside the /home/philip/Documents directory:

[philip@localhost NewTest]$ ll /home/philip/Documents/

total 4

drwxrwxr-x. 2 philip philip 4096 Aug 6 14:57 NewTest

-rwxrw----. 1 philip philip 0 Aug 6 14:34 RenameFile

[philip@localhost NewTest]$

We can also remove a file by using the rm command. Let us remove the /home/philip/Documents/NewTest/OurFile:

[philip@localhost NewTest]$ ll

total 0

-rwxrw----. 1 philip philip 0 Aug 6 13:52 OurFile

[philip@localhost NewTest]$ rm OurFile

[philip@localhost NewTest]$ ll

total 0

[philip@localhost NewTest]$

[Creating and removing directories](#contents.xhtml_sc22a)

We can create directories using another popular command. The mkdir command will be used to create a directory. Let us do a listing using the ls command:

[philip@localhost ~]$ ls

Desktop Documents Downloads Music Pictures Public Templates Videos

[philip@localhost ~]$

Now, let’s create our own directory inside the /home/philip:

[philip@localhost ~]$ mkdir NewTest

[philip@localhost ~]$ ll

total 36

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Desktop

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Documents

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Downloads

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Music

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Pictures

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Public

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Templates

drwxrwxr-x. 2 philip philip 4096 Aug 6 12:04 NewTest

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Videos

[philip@localhost ~]$

From the above, our new directory is listed at the bottom. You will also notice that we used the ll command; this is just an alias to the ls -l command. This can quickly be verified by using the which command:

philip@localhost ~]$ which ll

alias ll='ls -l --color=auto'

/usr/bin/ls

[philip@localhost ~]$

Great job! We can move in to our newly created directory using the “cd” command:

[philip@localhost ~]$ cd NewTest/

[philip@localhost NewTest]$ ls

[philip@localhost NewTest]$ pwd

/home/philip/NewTest

[philip@localhost NewTest]$

Next, suppose we created a directory and made a typo; well, not to worry because we can leverage the mv command once again, which has the ability to rename a directory. Let us attempt to rename the /home/Test directory:

[philip@localhost NewTest]$ pwd

/home/philip/Documents/NewTest

[philip@localhost NewTest]$ mv /home/philip/Documents/NewTest/ /home/philip/

[philip@localhost NewTest]$ pwd

/home/philip/Documents/NewTest

[philip@localhost NewTest]$

The reason we are encountering this error is because we are inside the directory. Let us try the command with the -v option:

[philip@localhost NewTest]$ mv -v /home/philip/Documents/NewTest/ /home/philip/

mv: cannot stat '/home/philip/Documents/NewTest/'

[philip@localhost NewTest]$

To get around this, we need to navigate out of the directory and then retry the mv command:

[philip@localhost ~]$ mv /home/philip/Documents/NewTest/ .

[philip@localhost ~]$ ll

total 36

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Desktop

drwxr-xr-x. 2 philip philip 4096 Aug 6 15:12 Documents

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Downloads

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Music

drwxrwxr-x. 2 philip philip 4096 Aug 6 15:00 NewTest

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Pictures

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Public

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Templates

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Videos

[philip@localhost ~]$

Now the NewTest file no longer exists inside the /home/philip/Documents/; this can be shown by executing:

[philip@localhost ~]$ ll Documents/

total 0

-rwxrw----. 1 philip philip 0 Aug 6 14:34 RenameFile

[philip@localhost ~]$

We can also rename a directory using the mv command. The trick is to specify a directory name when we call the mv command. Here is how this would look:

[philip@localhost ~]$ mv NewTest/ ReName

[philip@localhost ~]$ ll

total 36

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Desktop

drwxr-xr-x. 2 philip philip 4096 Aug 6 15:12 Documents

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Downloads

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Music

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Pictures

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Public

drwxrwxr-x. 2 philip philip 4096 Aug 6 15:00 ReName

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Templates

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Videos

[philip@localhost ~]$

It is that simple to rename a directory. We can also change the permissions on a directory. Let us take off the (read, write, and execute) from the group:

[philip@localhost ~]$ chmod -R 705 ReName/

[philip@localhost ~]$ ll

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Desktop

drwxr-xr-x. 2 philip philip 4096 Aug 6 15:12 Documents

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Downloads

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Music

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Pictures

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Public

drwx---r-x. 2 philip philip 4096 Aug 6 15:00 ReName

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Templates

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Videos

[philip@localhost ~]$

The -R option tells the chmod command to apply the permissions to everything that resides inside the /home/philip/ReName directory. Once finished with a directory, we can remove it if no longer needed. The rmdir command is used for removing directories. Let us remove the /home/philip/ReName directory:

[philip@localhost ~]$ rmdir ReName/

[philip@localhost ~]$ ll

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Desktop

drwxr-xr-x. 2 philip philip 4096 Aug 6 15:12 Documents

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Downloads

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Music

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Pictures

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Public

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Templates

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Videos

[philip@localhost ~]$

Based on the above, no error(s) were encountered. This might not be the case in your environment. Often you will have either files or other directories that reside in the directory which you are attempting to remove. Let us quickly create a directory and place 3 files inside the directory. Then we will attempt to remove the directory:

[philip@localhost ~]$ mkdir TempDir

[philip@localhost ~]$ ll

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Desktop

drwxrwxr-x. 2 philip philip 4096 Aug 6 15:46 TempDir

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Templates

drwxr-xr-x. 2 philip philip 4096 Jul 31 14:59 Videos

[philip@localhost ~]$ touch TempDir/File1

[philip@localhost ~]$ touch TempDir/File2

[philip@localhost ~]$ touch TempDir/File3

[philip@localhost ~]$ ll TempDir/

total 0

-rw-rw-r--. 1 philip philip 0 Aug 6 15:47 File1

-rw-rw-r--. 1 philip philip 0 Aug 6 15:47 File2

-rw-rw-r--. 1 philip philip 0 Aug 6 15:47 File3

[philip@localhost ~]$

Now, we will retry the rm command and see the differences:

[philip@localhost ~]$ rmdir TempDir/

rmdir: failed to remove 'TempDir/': Directory not empty

[philip@localhost ~]$

Now, we encounter an error. This is common when a directory is not empty. We can work around it easily; this time, we will use the rm command with the -r, which means to delete everything that follows. Adding to this, we can also add the -v option, which will show the details of any potential permission(s) issues:

[philip@localhost ~]$ ll TempDir/

total 0

-rw-rw-r--. 1 philip philip 0 Aug 6 15:53 File1

-rw-rw-r--. 1 philip philip 0 Aug 6 15:53 File2

-rw-rw-r--. 1 philip philip 0 Aug 6 15:53 File3

[philip@localhost ~]$ rm -rv TempDir/

removed 'TempDir/File3'

removed 'TempDir/File1'

removed 'TempDir/File2'

removed directory 'TempDir/'

[philip@localhost ~]$ ll TempDir/

ls: cannot access 'TempDir/': No such file or directory

[philip@localhost ~]$

Note: You can use the -f to delete an entire directory without being prompted for confirmation.

[Finding files and directories](#contents.xhtml_sc23a)

Often, we are searching for files and directories from the GUI. We can also perform searches at the shell. First, we can use the find command; let us look for files that have a .conf extension. The search function would be:

[philip@localhost ~]$ find /etc -iname "*.cfg"

find: ‘/etc/grub.d’: Permission denied

find: ‘/etc/cups/ssl’: Permission denied

/etc/libblockdev/conf.d/00-default.cfg

find: ‘/etc/audit’: Permission denied

find: ‘/etc/dhcp’: Permission denied

find: ‘/etc/sssd’: Permission denied

/etc/grub2.cfg

find: ‘/etc/audisp’: Permission denied

find: ‘/etc/polkit-1/rules.d’: Permission denied

find: ‘/etc/polkit-1/localauthority’: Permission denied

find: ‘/etc/openvpn/server’: Permission denied

find: ‘/etc/openvpn/client’: Permission denied

[philip@localhost ~]$

Now if you encounter these errors then it is an indication that we need some advance permissions. Let us try the search once again as the root user:

[philip@localhost ~]$ su

Password:

[root@localhost philip]# find /etc -iname "*.cfg"

/etc/libblockdev/conf.d/00-default.cfg

/etc/grub2-efi.cfg

/etc/vdpau_wrapper.cfg

/etc/grub2.cfg

[root@localhost philip]#

We can even broaden where we want to perform a search. Let us say the entire file system:

[root@localhost philip]# find / -iname "*.cfg"

/home/philip/.config/yelp/yelp.cfg

/run/media/philip/Fedora-WS-Live-28-1-1/EFI/BOOT/grub.cfg

/run/media/philip/Fedora-WS-Live-28-1-1/isolinux/isolinux.cfg

find: ‘/run/user/1000/gvfs’: Permission denied

/usr/lib64/libreoffice/share/config/soffice.cfg

/usr/lib64/libreoffice/help/en-US/schart.cfg

/usr/lib64/libreoffice/help/en-US/smath.cfg

/usr/lib64/libreoffice/help/en-US/sbasic.cfg

grub2.cfg

/boot/grub2/grub.cfg

[root@localhost philip]

Some output omitted for brevity. We can also search based on part of a name. Let us look for any file that begins with gru:

[root@localhost philip]# find /boot -iname "gru*"

/boot/efi/EFI/fedora/grubia32.efi

/boot/efi/EFI/fedora/grubenv

/boot/efi/EFI/fedora/grubx64.efi

/boot/grub2

/boot/grub2/grub.cfg

/boot/grub2/grubenv

[root@localhost philip]#

Based on the above output, we searched inside the /boot directory. Empty files are often just sitting inside a directory without being used. We can search for empty files using the find command. The -type option is passed to specify what we are searching for:

[root@localhost philip]# find /home/philip/Documents -empty

/home/philip/Documents/RenameFile

[root@localhost philip]#

However, we can do some housekeeping by passing the -delete option to remove any files which the find command has returned from our search. Here is how we would do this:

[root@localhost philip]# find /home/philip/Documents -empty -delete

[root@localhost philip]# ll /home/philip/Documents

ls: cannot access '/home/philip/Documents': No such file or directory

[root@localhost philip]# ll

Note: Be careful when using the -delete option as it will remove the files and even the directories in some cases. Always back up your data before running find with the -delete option.

From the above output, you will notice that the /home/philip/Documents/RenameFile, in addition to the /home/philip/Documents directory, has been removed. Be very cautious whenever passing the -delete option. In our case, this is a lab environment, but keep that in mind in your real systems. Perform a backup before attempting to pass the -delete option.

We can also search for file or directories based on permissions. We would pass the -readable, -writable, -executable options with the find command. Here is how this would look:

[root@localhost philip]# find /etc/yum.repos.d/ -readable

/etc/yum.repos.d/

/etc/yum.repos.d/fedora-updates.repo

/etc/yum.repos.d/fedora.repo

/etc/yum.repos.d/fedora-cisco-openh264.repo

/etc/yum.repos.d/fedora-updates-testing.repo

[root@localhost philip]# ll /etc/yum.repos.d/

total 16

-rw-r--r--. 1 root root 707 Apr 23 13:03 fedora-cisco-openh264.repo

-rw-r--r--. 1 root root 1331 Apr 23 13:03 fedora.repo

-rw-r--r--. 1 root root 1392 Apr 23 13:03 fedora-updates.repo

-rw-r--r--. 1 root root 1450 Apr 23 13:03 fedora-updates-testing.repo

[root@localhost philip]#

We can clearly see that the result from the find command matches the listing for files with the read permission. Likewise, we can search for the files and directories with execute permissions:

[root@localhost philip]# ll /etc/init.d/

total 52

-rw-r--r--. 1 root root 18561 Jan 2 2018 functions

-rwxr-xr-x. 1 root root 7288 Apr 25 02:39 livesys

-rwxr-xr-x. 1 root root 1054 Apr 25 02:39 livesys-late

-rwxr-xr-x. 1 root root 4334 Jan 2 2018 netconsole

-rwxr-xr-x. 1 root root 7613 Jan 2 2018 network

-rw-r--r--. 1 root root 1161 Apr 18 17:59 README

[root@localhost philip]# find /etc/init.d/ -perm -o+x

/etc/init.d/

/etc/init.d/livesys

/etc/init.d/livesys-late

/etc/init.d/netconsole

/etc/init.d/network

[root@localhost philip]#

Based on the above output, only the files with the execute permissions for others are displayed.

Adding to this, we can also search for files and directories with write permissions:

[root@localhost philip]# find /etc/init.d/ -perm -o+w

[root@localhost philip]#

The results came back empty because none of the files or directories have write permissions for others. Similarly, we can search using numbers. We could look for execute permissions like:

[root@localhost philip]# find /etc/init.d/ -perm -005

/etc/init.d/

/etc/init.d/livesys

/etc/init.d/livesys-late

/etc/init.d/netconsole

/etc/init.d/network

[root@localhost philip]#

Based on the above output, we can only see directories with execute displayed. We can search for files and directories with write permissions:

[root@localhost philip]# find /etc/init.d/ -perm -002

[root@localhost philip]#

The results came back as expected because the others do not have write permissions. Likewise, we can search for write permissions for groups; we would:

[root@localhost philip]# ll /etc/init.d/

total 52

-rw-r--r--. 1 root root 18561 Jan 2 2018 functions

-rwxr-xr-x. 1 root root 7288 Apr 25 02:39 livesys

-rwxr-xr-x. 1 root root 1054 Apr 25 02:39 livesys-late

-rwxr-xr-x. 1 root root 4334 Jan 2 2018 netconsole

-rwxr-xr-x. 1 root root 7613 Jan 2 2018 network

-rw-r--r--. 1 root root 1161 Apr 18 17:59 README

[root@localhost philip]# find /etc/init.d/ -perm -020

[root@localhost philip]#

The results are empty because the groups do not have the write permissions. Lastly, we can search for write permissions for the user; this would give us:

[root@localhost philip]# find /etc/init.d/ -perm -200

/etc/init.d/

/etc/init.d/functions

/etc/init.d/livesys

/etc/init.d/README

/etc/init.d/livesys-late

/etc/init.d/netconsole

/etc/init.d/network

[root@localhost philip]#

The syntax is -perm followed by first digit=user, second digit=group, and last digit=others.

Another popular method for searching files and directories is to use the locate command. The locate utility is faster in terms of results when compared to the find utility; this is because the locate command uses a database to perform lookups. The database is called mlocate; we can perform a simple search of a file that we created:

[philip@localhost ~]$ locate TestFile

[philip@localhost ~]$

Based on the above output, the locate command is unaware of the specified file. Not to worry, we simply must update the database:

[philip@localhost ~]$ updatedb

updatedb: can not open a temporary file for `/var/lib/mlocate/mlocate.db'

[philip@localhost ~]$

If you run in to this error, then it simply means that you need to run the command as root:

[philip@localhost ~]$ su

Password:

[root@localhost philip]# updatedb

[root@localhost philip]#

Now, let’s retry the locate command for the given file:

[root@localhost philip]# locate TestFile

/home/philip/Documents/TestFile1

[root@localhost philip]#

We can also search by extensions. We would use a wildcard:

[root@localhost philip]# locate *.key

/etc/brlapi.key

/etc/trusted-key.key

/usr/lib64/libreoffice/help/en-US/sbasic.key

/usr/lib64/libreoffice/help/en-US/scalc.key

/usr/lib64/libreoffice/help/en-US/schart.key

/usr/lib64/libreoffice/help/en-US/sdatabase.key

/usr/lib64/libreoffice/help/en-US/sdraw.key

/usr/lib64/libreoffice/help/en-US/simpress.key

/usr/lib64/libreoffice/help/en-US/smath.key

/usr/lib64/libreoffice/help/en-US/swriter.key

/usr/share/doc/openssh/PROTOCOL.key

/usr/share/doc/python3-pycurl/tests/certs/server.key

[root@localhost philip]#

Based on the above output, only results with lowercase names are displayed; we can fix this by passing the -i, which tells the locate command to ignore the case:

[root@localhost philip]# locate -i *.key

/etc/brlapi.key

/etc/trusted-key.key

/usr/lib64/libreoffice/help/en-US/sbasic.key

/usr/lib64/libreoffice/help/en-US/scalc.key

/usr/lib64/libreoffice/help/en-US/schart.key

/usr/lib64/libreoffice/help/en-US/sdatabase.key

/usr/lib64/libreoffice/help/en-US/sdraw.key

/usr/lib64/libreoffice/help/en-US/simpress.key

/usr/lib64/libreoffice/help/en-US/smath.key

/usr/lib64/libreoffice/help/en-US/swriter.key

/usr/share/doc/openssh/PROTOCOL.key

/usr/share/doc/python3-pycurl/tests/certs/server.key

[root@localhost philip]#

In this case, the results are the same since the files are in lowercase. We can also control how the output is displayed; we would pass the --null option:

[root@localhost philip]# locate --null *types

/etc/ethertypes/etc/mime.types/etc/firewalld/icmptypes/etc/selinux/targeted/contexts/customizable_types/etc/selinux/targeted/contexts/securetty_types/usr/include/bits/types/usr/lib/firewalld/icmptypes/usr/lib64/libreoffice/program/types/usr/lib64/libreoffice/share/filter/vml-shape-types/usr/lib64/perl5/bits/types/usr/lib64/python2.7/ctypes/usr/lib64/python2.7/ctypes/macholib/REAshare/icons/hicolor/512x512/mimetypes/usr/share/icons/hicolor/64x64/mimetypes/usr/share/icons/hicolor/72x72/mimetypes/usr/share/icons/hicolor/96x96/mimetypes/usr/share/icons/hicolor/scalable/mimetypes/usr/share/icons/locolor/16x16/mimetypes/usr/share/icons/locolor/32x32/mimetypes/usr/share/mime/types

[root@localhost philip]#

Based on the above output, we see the desired results. Finally, we can view information about the database; we would use the -S option:

[root@localhost philip]# locate -S

Database /var/lib/mlocate/mlocate.db:

12,517 directories

162,475 files

8,292,135 bytes in file names

3,883,960 bytes used to store database

[root@localhost philip]#

In addition to the size, we can also see the location of the database.

[Pipes and redirects](#contents.xhtml_sc24a)

Often when we are viewing output from various commands, it gets a bit fuzzy to read. Fear no more, and we have what are known as pipes and redirects. Basically, when working with pipes |, we take the output of a command and pass it as an input to another command. Redirects >, <, >>, >&, like taking the output from a command, but this time, we send it to a location such as a file or another location, to name a few.

To begin with, let us pick the ls command; we can do this:

[root@localhost philip]# ls /etc

abrt default gdbinit.d kernel networks rc4.d subuid-

adjtime depmod.d gdm krb5.conf nfs.conf rc5.d sudoers

aliases dhcp geoclue krb5.conf.d nfsmount.conf rc6.d sudoers.d

alsa DIR_COLORS glvnd ld.so.cache nsswitch.conf rc.d sysconfig

alternatives DIR_COLORS.256color gnupg ld.so.conf nsswitch.conf.bak rdma sysctl.conf

[root@localhost philip]#

Some output omitted for brevity. We can view the output one page at a time by bringing in yet another powerful command; the less command:

[root@localhost philip]# ls /etc | less

cron.daily

cron.deny

cron.hourly

cron.monthly

crontab

cron.weekly

crypto-policies

crypttab

csh.cshrc

csh.login

cups

cupshelpers

:

[root@localhost philip]#

To exit out of the less command, we would use the q on the keyboard. The benefit of using the less command is the fact that we can move back and forward as opposed to the more command which can only move forward. We can also use the pipe | character to pass values that another command is expecting. We can use the wc command to illustrate this:

[root@localhost philip]# ls /etc | wc -w

263

[root@localhost philip]#

Based on the above output, we took the output from the ls command and passed it as input to the wc command. The wc command is used for word count; the -w option is used to display the total words.

Next, we can use redirects in several ways. In Linux, we have 3 types of streams:

STDIN =input “<”, STDOUT =output “>” , STDERR =standard error “2>”

Also, we can mix and match the streams, as you will see later in this section. Let us start with STDIN; we can use the wc command and call the input from a file:

[root@localhost philip]# wc -w < /boot/grub2/grub.cfg

435

[root@localhost philip]#

The word count of the /boot/grub2/grub.cfg is passed to the wc command. Moving on to STDOUT, we can redirect the output of a command and store it in a file. Let us use the ls command:

[root@localhost philip]# ls /etc/init.d/ > /home/philip/Documents/ls.txt

[root@localhost philip]#

Based on the above output, we did a listing of the /etc/init.d/ and saved the output to /home/philip/Documents/ls.txt. This can be verified by:

[root@localhost philip]# cat /home/philip/Documents/ls.txt

functions

livesys

livesys-late

netconsole

network

README

[root@localhost philip]#

Now, let us say we use the ls command for another directory. This will overwrite the existing content of the /home/philip/Documents/ls.txt, let us try:

[root@localhost philip]# ls /boot/grub2/ > /home/philip/Documents/ls.txt

[root@localhost philip]# cat /home/philip/Documents/ls.txt

device.map

fonts

grub.cfg

grubenv

i386-pc

locale

themes

[root@localhost philip]#

As we can see, the proof is in the pudding. A way around this would be to tell the STDOUT that we want to append the output instead of overwriting:

[root@localhost philip]# ls /var/ >> /home/philip/Documents/ls.txt

[root@localhost philip]# cat /home/philip/Documents/ls.txt

device.map

fonts

grub.cfg

grubenv

i386-pc

locale

themes

account

adm

cache

crash

db

empty

ftp

games

gopher

kerberos

lib

spool

tmp

www

yp

[root@localhost philip]#

So, we use >> for appending data to an existing file. Next, we can combine the results of the STDIN of a command and send it to the STDOUT. Here is how this would look:

[root@localhost philip]# wc -w < /var/log/boot.log > /home/philip/Documents/STDIN_STDOUT.txt

[root@localhost philip]# cat /home/philip/Documents/STDIN_STDOUT.txt

2021

[root@localhost philip]#

We can also redirect STDERR to a file. Let us use the file command:

[root@localhost philip]# ls -l /tmp TestFileWithError 2> /home/philip/Documents/STDERR.txt

/tmp:

drwx------. 3 root root 60 Aug 2 10:23 systemd-private-a7a23120abff44c8bca6807f1711c1c2-bolt.service-7uNmVr

drwx------. 3 root root 60 Aug 2 10:22 systemd-private-a7a23120abff44c8bca6807f1711c1c2-chronyd.service-LPD8zu

drwx------. 3 root root 60 Aug 2 10:23 systemd-private-a7a23120abff44c8bca6807f1711c1c2-colord.service-13Vcs8

drwx------. 3 root root 60 Aug 2 10:28 systemd-private-a7a23120abff44c8bca6807f1711c1c2-fwupd.service-XOnyvf

drwx------. 3 root root 60 Aug 2 10:22 systemd-private-a7a23120abff44c8bca6807f1711c1c2-rtkit-daemon.service-ZD5mO7

drwx------. 2 philip philip 40 Aug 2 10:31 tracker-extract-files.1000

drwx------. 2 root root 40 Aug 2 10:22 vmware-root

[root@localhost philip]#

Based on the above output, it appears as though the command worked. Well, the truth of the matter is that the listing for /tmp worked, but the error for the file TestFileWithError was not displayed. The error was sent to the /home/philip/Documents/STDERR.txt. This can be verified by:

[root@localhost philip]# cat /home/philip/Documents/STDERR.txt

ls: cannot access 'TestFileWithError': No such file or directory

[root@localhost philip]#

We can also combine the STDDOUT with the STDERR into a single file. This is accomplished by telling the shell that we would like to store the STDERR along with the STDOUT inside the same file 2>&1. Here is how this would be accomplished:

[root@localhost philip]# ls -l /tmp TestFileWithError > /home/philip/Documents/STDERR.txt 2>&1

[root@localhost philip]# cat /home/philip/Documents/STDERR.txt

ls: cannot access 'TestFileWithError': No such file or directory

/tmp:

total 0

drwx------. 3 root root 60 Aug 2 10:23 systemd-private-a7a23120abff44c8bca6807f1711c1c2-bolt.service-7uNmVr

drwx------. 3 root root 60 Aug 2 10:22 systemd-private-a7a23120abff44c8bca6807f1711c1c2-chronyd.service-LPD8zu

drwx------. 3 root root 60 Aug 2 10:23 systemd-private-a7a23120abff44c8bca6807f1711c1c2-colord.service-13Vcs8

drwx------. 3 root root 60 Aug 2 10:28 systemd-private-a7a23120abff44c8bca6807f1711c1c2-fwupd.service-XOnyvf

drwx------. 3 root root 60 Aug 2 10:22 systemd-private-a7a23120abff44c8bca6807f1711c1c2-rtkit-daemon.service-ZD5mO7

drwx------. 2 philip philip 40 Aug 7 14:45 tracker-extract-files.1000

drwx------. 2 root root 40 Aug 2 10:22 vmware-root

[root@localhost philip]#

Based on the above output, we can see the error at the beginning of the file, followed by the listing of the /tmp. Finally, it is possible to display the output of a command and simultaneously redirect the output to a file; this is made possible by yet another powerful command, the tee command. Here is the tee command in action:

[root@localhost philip]# cat /etc/hosts.allow | tee /home/philip/Documents/The_Tee_command.txt

#

# hosts.allow This file contains access rules which are used to

# allow or deny connections to network services that

# either use the tcp_wrappers library or that have been

# started through a tcp_wrappers-enabled xinetd.

#

# See 'man 5 hosts_options' and 'man 5 hosts_access'

# for information on rule syntax.

# See 'man tcpd' for information on tcp_wrappers

[root@localhost philip]#

[root@localhost philip]# cat /home/philip/Documents/The_Tee_command.txt

#

# hosts.allow This file contains access rules which are used to

# allow or deny connections to network services that

# either use the tcp_wrappers library or that have been

# started through a tcp_wrappers-enabled xinetd.

#

# See 'man 5 hosts_options' and 'man 5 hosts_access'

# for information on rule syntax.

# See 'man tcpd' for information on tcp_wrappers

[root@localhost philip]#

From the above output, we can see the power of the tee command.

[Filesystem management](#contents.xhtml_sc25a)

The Linux operating system supports various file system types on the hard disk, each designed to address different requirements and provide specific features. Here are the common file system types:

[Fourth extended file system](#contents.xhtml_sc26a)

Fourth Extended File System (ext4) is the default and most widely used file system in Linux distributions. It offers backward compatibility with ext2 and ext3, journaling for data consistency, support for large file sizes and file systems, and efficient performance. The ext4 is suitable for general-purpose usage, ranging from personal computers to enterprise servers.

[XFS file system](#contents.xhtml_sc27a)

XFS is a high-performance, scalable file system originally developed by silicon graphics, Inc. It is known for its ability to handle large-scale storage systems. The XFS file system provides high scalability, parallel I/O operations, fast crash recovery, efficient space allocation, and support for advanced features like snapshots and online defragmentation. It is well-suited for large-scale storage environments, including file servers, database servers, and multimedia applications.

[B-tree file system](#contents.xhtml_sc28a)

B-tree file system (Btrfs) is a next-generation file system designed to address the limitations of traditional file systems. The Btrfs file system offers features like snapshots, copy-on-write, data compression, built-in RAID support, online resizing, and checksum for data integrity. It is ideal for scenarios that require advanced features like snapshots for backups, data deduplication, and flexible disk management.

[ZFS file system](#contents.xhtml_sc29a)

Although not natively part of the Linux kernel, ZFS is a powerful and feature-rich file system widely used in other operating systems. The ZFS file system provides features such as data integrity checks, pooled storage with dynamic striping, snapshots, compression, deduplication, and advanced RAID functionality. It is commonly used in storage servers, high-performance computing clusters, and environments where data integrity and advanced storage capabilities are crucial.

[New technology file system](#contents.xhtml_sc30a)

New Technology File System (NTFS) is the default file system used in Microsoft Windows operating systems. Linux supports read and write access to NTFS partitions, allowing data interchangeability between Linux and Windows systems. The NTFS support in Linux is useful for dual-boot systems or when accessing Windows-formatted storage devices.

We have various utilizes to manage Linux file system. Let us now look at some of the commonly used tools for managing the hard disk ranging from creating partitions all the way to mounting the partition, that are available in the Linux terminal.

[Using the fdisk utility](#contents.xhtml_sc31a)

In Linux, whenever we are working with hard disks, chances are we will, at some point in time, have to partition it. It means that we must separate the hard disk. This empowers us to have varying sizes of partitions and gives us the ability to satisfy various software installation requirements. Furthermore, when we partition a hard disk, each partition is treated as an entirely separate hard disk by the operating system. The fdisk (fixed disk or format disk) is a command-line-based utility that can be used for manipulating a hard disk. With fdisk, you can view, create, delete, change a partition type, to name a few.

To begin with, let us expose the hard disk within our Ubuntu distribution:

philip@ubuntu:~$ ls /dev/ | grep sd

sda

sda1

sda2

sda5

philip@ubuntu:~$

From the above, the hard disk in the system is represented by /dev/sda. The first partition is /dev/sda1, and the second partition is /dev/sda2, etc. For us to see the partition information, we will:

philip@ubuntu:~$ fdisk -l /dev/sda

fdisk: cannot open /dev/sda: Permission denied

philip@ubuntu:~$

From the above, we get a permission denied error. The reason is that we require root privileges to view or change the partition of a hard disk. Let us retry as the root user:

philip@ubuntu:~$ sudo su

[sudo] password for philip:

root@ubuntu:/home/philip#

root@ubuntu:/home/philip# fdisk -l /dev/sda

Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0xf54f42a0

Device Boot Start End Sectors Size Id Type

/dev/sda1 * 2048 39845887 39843840 19G 83 Linux

/dev/sda2 39847934 41940991 2093058 1022M 5 Extended

/dev/sda5 39847936 41940991 2093056 1022M 82 Linux swap / Solaris

root@ubuntu:/home/philip#

From the above, the way to read this would be:

Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors: This is the actual physical hard disk.

Device Boot Start End Sectors Size Id Type

/dev/sda1 * 2048 39845887 39843840 19G 83 Linux: First partition is 19GB

/dev/sda2 39847934 41940991 2093058 1022M 5 Extended: Second partition is 1022MB

/dev/sda5 39847936 41940991 2093056 1022M 82 Linux swap / Solaris: Fifth partition is 1022MB

Now, for us to be able to make any changes, we will use the fdisk command once again. This time we will leave out the -l option:

root@ubuntu:/home/philip# fdisk /dev/sda

Welcome to fdisk (util-linux 2.27.1).

Changes will remain in memory only, until you decide to write them.

Be careful before using the write command.

Command (m for help):

From the above, we are now inside of the fdisk utility.

Note: Do not commit any changes before making sure you understand the dangers surrounding removing the partition; the system could become unstable if you remove a partition that stores system files, such as: /boot/, /, to name a few.

For us to view the two available options, we can press the m key:

Command (m for help): m

Help:

DOS (MBR)

a toggle a bootable flag.

b edit nested BSD disk label.

c toggle the dos compatibility flag.

Generic

d delete a partition.

F list free unpartitioned space.

l list known partition types.

n add a new partition.

p print the partition table.

t change a partition type.

v verify the partition table.

i print information about a partition.

Misc

m print this menu.

u change display/entry units.

x extra functionality (experts only).

Script

I load disk layout from sfdisk script file

dump disk layout to sfdisk script file

Save and exit

w write table to disk and exit

q quit without saving changes

Create a new label

g create a new empty GPT partition table

G create a new empty SGI (IRIX) partition table

create a new empty DOS partition table

s create a new empty Sun partition table

Command (m for help):

From the above output, we can see a variety of options to choose from. We can even use l to see the known partition types. Consider [Figure 2.1](#ch02.xhtml_fig2-1):

![](images/Figure_2.1_.png)

Figure 2.1: Types of partition available with the fdisk utility

From the above, there is a range of different partition types available for usage. The common types would be: 5 (Extended), 7 NTFS (Windows), 82 (Linux swap), 83 (Linux), a5 (FreeBSD), ee (GPT), ef (EFI), to name a few.

Now, to view the partitions created, we can use p, as shown in [Figure 2.2](#ch02.xhtml_fig2-2):

![](images/Figure_2.2_.png)

Figure 2.2: Partition table of the /dev/sda

A second hard disk has been added to this system, so let us verify:

root@ubuntu:/home/philip# ls /dev/ | grep sd

sda

sda1

sda2

sda5

sdb

root@ubuntu:/home/philip#

We can now see /dev/sdb. We will use fdisk with this new hard disk:

root@ubuntu:/home/philip# fdisk /dev/sdb

Welcome to fdisk (util-linux 2.27.1).

Changes will remain in memory only, until you decide to write them.

Be careful before using the write command.

Device does not contain a recognized partition table.

Created a new DOS disklabel with disk identifier 0x0079e169.

Command (m for help):

Now, let us press p, which will print the current partition(s) on the /dev/sdb:

Command (m for help): p

Disk /dev/sdb: 15 GiB, 16106127360 bytes, 31457280 sectors

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabeltype: dos

Disk identifier: 0x0079e169

Command (m for help):

As you can see, there is no partition on the /dev/sdb. For us to create a partition, we will see the n key:

Command (m for help): n

Partition type

p primary (0 primary, 0 extended, 4 free)

e extended (container for logical partitions)

Select (default p):

This will ask us to declare the type of partition. There are primary and extended partition types available with the fdisk utility. There is also a logical partition type. For us to install an operating system, we will choose the p, which stands for primary partition type.

Note: You would not install an operating system on a logical partition type.

As soon as we press p, the fdisk utility will prompt us to define the partition number (starting partition):

Command (m for help): n

Partition type

p primary (0 primary, 0 extended, 4 free)

e extended (container for logical partitions)

Select (default p): p

Partition number (1-4, default 1):

Now, we will need to specify the starting size and ending size of this partition:

Partition number (1-4, default 1): 1

First sector (2048-31457279, default 2048):

Last sector, +sectors or +size{K,M,G,T,P} (2048-31457279, default 31457279):

If we simply press Enter, the partition will use up the entire hard disk; In our case, we will create 5GB partition:

Last sector, +sectors or +size{K,M,G,T,P} (2048-31457279, default 31457279): +5G

Created a new partition 1 of type 'Linux' and of size 5 GiB.

Command (m for help):

Now in order to view the newly created partition, we will press p:

Command (m for help): p

Disk /dev/sdb: 15 GiB, 16106127360 bytes, 31457280 sectors

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x2584b986

Device Boot Start End Sectors Size Id Type

/dev/sdb1 2048 10487807 10485760 5G 83 Linux

Command (m for help):

Now, we have roughly 10GB of free space, and we got that information from the above output. We will create 2 more partitions:

Command (m for help): p

Disk /dev/sdb: 15 GiB, 16106127360 bytes, 31457280 sectors

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x2584b986

Device Boot Start End Sectors Size Id Type

/dev/sdb1 2048 10487807 10485760 5G 83 Linux

/dev/sdb2 10487808 18876415 8388608 4G 83 Linux

/dev/sdb3 18876416 31457279 12580864 6G 83 Linux

Command (m for help):

Note: You would not install an operating system on a logical partition type.

As you can see, we use the n to create new partitions. An important point to note is the fact that the partitions which we have created thus far are all Linux type of partition. If for some reason, we would want to change the partition type; We can use t to change a partition(s) type. Let us change the /dev/sdb2 to an HPFS/NTFS/exFAT partitions; We will use type 7 in the fdisk utility:

Command (m for help): t

Partition number (1-3, default 3): 2

Partition type (type L to list all types): l

0 Empty 24 NEC DOS 81 Minix / old Lin bf Solaris

1 FAT12 27 Hidden NTFS Win 82 Linux swap / So c1 DRDOS/sec (FAT-

2 XENIX root 39 Plan 9 83 Linux c4 DRDOS/sec (FAT-

3 XENIX usr 3c PartitionMagic 84 OS/2 hidden or c6 DRDOS/sec (FAT-

4 FAT16 <32M 40 Venix 80286 85 Linux extended c7 Syrinx

5 Extended 41 PPC PReP Boot 86 NTFS volume set da Non-FS data

6 FAT16 42 SFS 87 NTFS volume set db CP/M / CTOS / .

7 HPFS/NTFS/exFAT

Now we can see the partition type as type 7:

Partition type (type L to list all types): 7

Changed type of partition 'Empty' to 'HPFS/NTFS/exFAT'.

Command (m for help): p

Disk /dev/sdb: 15 GiB, 16106127360 bytes, 31457280 sectors

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x2584b986

Device Boot Start End Sectors Size Id Type

/dev/sdb1 2048 10487807 10485760 5G 83 Linux

/dev/sdb2 10487808 18876415 8388608 4G 7 HPFS/NTFS/exFAT

/dev/sdb3 18876416 31457279 12580864 6G 0 Empty

Also, we will change /dev/sdb3 partition to type ef:

Now, when we rerun the p command, we can see our newly created partition type set to ef:

Device Boot Start End Sectors Size Id Type

/dev/sdb1 2048 10487807 10485760 5G 83 Linux

/dev/sdb2 10487808 18876415 8388608 4G 7 HPFS/NTFS/exFAT

/dev/sdb3 18876416 31457279 12580864 6G ef EFI (FAT-12/16/32)

Now, if we decide to install an operating system then we will have to make one of these partitions bootable. We will make the third partition /dev/sdb3 bootable:

Command (m for help): a

Partition number (1-3, default 3): 3

The bootable flag on partition 3 is enabled now:

Command (m for help): p

Disk /dev/sdb: 15 GiB, 16106127360 bytes, 31457280 sectors

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x2584b986

Device Boot Start End Sectors Size Id Type

/dev/sdb1 2048 10487807 10485760 5G 83 Linux

/dev/sdb2 10487808 18876415 8388608 4G 7 HPFS/NTFS/exFAT

/dev/sdb3 * 18876416 31457279 12580864 6G ef EFI (FAT-12/16/32)

From the above output, the /dev/sdb3 is now marked as bootable.

Finally, to change/write our changes, we will press w to save and exit:

Command (m for help): w

The partition table has been altered.

Calling ioctl() to re-read partition table.

Syncing disks.

[Using the parted utility](#contents.xhtml_sc32a)

The parted utility is geared towards situations where we have a hard disk(s) larger than 2TB. Additionally, we can resize a partition; The fdisk utility cannot resize a partition. Almost all newer Linux distributions support the parted utility. Parted comes from GNU, a text-based partitioning utility that works with a variety of disk types, such as MBR, GPT, BSD, to name a few.

Note: Always backup your data before doing any partitioning.

To begin with, we will use the parted command on the /dev/sdb:

root@ubuntu:/home/philip# parted /dev/sdb

GNU Parted 3.2

Using /dev/sdb

Welcome to GNU Parted! Type 'help' to view a list of commands.

(parted)

From here, we are placed into the parted utility. Similar to the fdisk utility, the parted utility is interactive. Now let us say we want to view the help menu; we can enlist the help at the cli:

(parted) help

align-check TYPE N check partition N for TYPE(min|opt) alignment

help [COMMAND] print general help, or help on COMMAND

mklabel,mktable LABEL-TYPE create a new disklabel (partition table)

mkpart PART-TYPE [FS-TYPE] START END make a partition

name NUMBER NAME name partition NUMBER as NAME

print [devices|free|list,all|NUMBER] display the partition table, available devices, free space, all found

partitions, or a particular partition

quit exit program

rescue START END rescue a lost partition near START and END

resizepart NUMBER END resize partition NUMBER

rm NUMBER delete partition NUMBER

select DEVICE choose the device to edit

disk_set FLAG STATE change the FLAG on selected device

disk_toggle [FLAG] toggle the state of FLAG on selected device

set NUMBER FLAG STATE change the FLAG on partition NUMBER

toggle [NUMBER [FLAG]] toggle the state of FLAG on partition NUMBER

unit UNIT set the default unit to UNIT

version display the version number and copyright information of GNU Parted

(parted)

From the above output, we have a long list of commands at our disposal.

Note: Remember to do a backup before making any change(s) to your partition

Now, to view to current partition table for the /dev/sdb, we would type print:

Model: VMware, VMware Virtual S (scsi)

Disk /dev/sdb: 16.1GB

Sector size (logical/physical): 512B/512B

Partition Table: msdos

Disk Flags:

Number Start End Size Type File system Flags

1 1049kB 5370MB 5369MB primary

2 5370MB 9665MB 4295MB primary

3 9665MB 16.1GB 6441MB primary boot, esp

(parted)

This will print out the partition table for the /dev/sdb. However, we can use the print command with the list option to view all the hard disks available in this system. Let us give it a try:

(parted) print list

Model: VMware, VMware Virtual S (scsi)

Disk /dev/sdb: 16.1GB

Sector size (logical/physical): 512B/512B

Partition Table: msdos

Disk Flags:

Number Start End Size Type File system Flags

1 1049kB 5370MB 5369MB primary

2 5370MB 9665MB 4295MB primary

3 9665MB 16.1GB 6441MB primary boot, esp

Model: VMware, VMware Virtual S (scsi)

Disk /dev/sda: 21.5GB

Sector size (logical/physical): 512B/512B

Partition Table: msdos

Disk Flags:

Number Start End Size Type File system Flags

1 1049kB 20.4GB 20.4GB primary ext4 boot

2 20.4GB 21.5GB 1072MB extended

5 20.4GB 21.5GB 1072MB logical linux-swap(v1)

(parted)

As you can see, the /dev/sda is now also listed. Next, let us look at how we would resize a partition. To accomplish this, we are going to leverage another powerful command, the resizepart command, which is appropriately named.

We will choose the second partition for this exercise; we will say resizepart 2. We will reduce it to 2GB:

(parted) resizepart

Partition number? 2

End? [5370MB]? 7518

(parted) print

Disk /dev/sdb: 16.1GB

Sector size (logical/physical): 512B/512B

Partition Table: msdos

Disk Flags:

Number Start End Size Type File system Flags

1 1049kB 5370MB 5369MB primary

2 5370MB 7518MB 2148MB primary

3 9665MB 16.1GB 6441MB primary boot, esp

(parted)

From the above output, you can see that the parted utility is very powerful. We have effectively taken away 2GB (roughly) from the second partition. Now, if you think about it, we have 2GB of free space to use at our disposal.

Note: Hard disk space is critical in large data centers, so keep that in mind when provisioning your servers.

Now, for the purpose of demonstrating how we would use the 2GB of free space, let us create another partition. The parted utility is powerful that it can recognize partitions that were created from another disk utility, such as fdisk. In parted, we would use the mkpart command to create a partition:

(parted)

(parted) mkpart

Partition type? primary/extended?

As you can see by now, the similarities between fdisk and parted, they both ask whether the partition is going to be a primary or an extended partition. This is vital whenever we are working with operating system installations. For our purposes, we are going to create yet another primary partition:

Partition type? primary/extended? primary

File system type? [ext2]?

Start?

Now, at this point, we will have to specify the starting size of the partition we are about to create. We will use the size where the second partition ends:

File system type? [ext2]?

Start? 7518

End? 9665

(parted)

Now let us rerun the print command:

(parted) print

Model: VMware, VMware Virtual S (scsi)

Disk /dev/sdb: 16.1GB

Sector size (logical/physical): 512B/512B

Partition Table: msdos

Disk Flags:

Number Start End Size Type File system Flags

1 1049kB 5370MB 5369MB primary

2 5370MB 7518MB 2148MB primary

4 7518MB 9665MB 2146MB primary ext2 lba

3 9665MB 16.1GB 6441MB primary boot, esp

(parted)

From the above output, we can now see our newly created partition at 2GB (roughly).

Now, we can change the boot flag from its present partition 3 /dev/sdb3 to part partition 4 /dev/sdb4. We would use the set command:

(parted) set

Partition number? 4

Flag to Invert?

From here, we must tell the parted utility that we want to move the boot flag:

Flag to Invert? boot

New state? [on]/off?

Now, we need to confirm our changes, on is the default, so we press Enter:

New state? [on]/off?

(parted) print

Model: VMware, VMware Virtual S (scsi)

Disk /dev/sdb: 16.1GB

Sector size (logical/physical): 512B/512B

Partition Table: msdos

Disk Flags:

Number Start End Size Type File system Flags

1 1049kB 5370MB 5369MB primary

2 5370MB 7518MB 2148MB primary

4 7518MB 9665MB 2146MB primary ext2 boot, lba

3 9665MB 16.1GB 6441MB primary esp

(parted)

Now we can see that the boot flag has been shifted to the fourth partition /dev/sdb4.

Finally, to save our changes, we would simply type quit:

(parted) quit

Information: You may need to update /etc/fstab.

root@ubuntu:/home/philip#

Note: You would add entries as needed in the /etc/fstab to automount your partitions to their respective mount points

[Steps to format a hard disk](#contents.xhtml_sc33a)

After we would have created our partitions, the next step would be to make the partitions accessible by way of a file system. In Linux, when we format a partition(s), the system wipes the partition, and this enables the system to store data on the partition.

We have a number of file system types available in a Linux system. We use the mkfs command in combination with the desired file system type to format a desired partition. To see the available file systems, we can use the mkfs command followed by a period (.) as follows:

![](images/Figure_2.3_.png)

Figure 2.3: mkfs file system

From the above output, in this Ubuntu distribution, there are various ext file systems available. In addition, there are also Microsoft Windows file system types such as FAT, NTFS, etc.. We can also use the lsblk command with the -f option to view the file systems in use:

root@ubuntu:/home/philip# lsblk -f

NAME FSTYPE LABEL UUID MOUNTPOINT

sda

├─sda1 ext4 adb5d090-3400-4411-aee2-dd871c39db38 /

├─sda2

└─sda5 swap 025b1992-80ba-46ed-8490-e7aa68271e7b [SWAP]

sdb

├─sdb1

├─sdb2

├─sdb3

└─sdb4

sr0

root@ubuntu:/home/philip#

From the above output, we can see both hard disks, /dev/sda and /dev/sdb. Additionally, we see a column FSTYPE. This identifies which file system is currently in use. We can see that the FSTYPE is blank for the entire /dev/sdb(1-4).

We can also use the blkid command to view the UUIDs and file systems in use by the system, as shown in [Figure 2.4](#ch02.xhtml_fig2-4):

![](images/Figure_2.4_.png)

Figure 2.4: The UUIDs and file system of the various hard disks

From the output given, the part that says TYPE= displays the file system in use. Due note that the TYPE= is missing for the /dev/sdb(1-4). This simply means that we have not formatted any of the partitions that reside on the /dev/sdb.

Now, let us start formatting our partitions. We will use the ext4 file system on the /dev/sdb1:

root@ubuntu:/home/philip# mkfs.ext4 /dev/sdb1

mke2fs 1.42.13 (17-May-2015)

Creating filesystem with 1310720 4k blocks and 327680 inodes

Filesystem UUID: fc51dddf-c23d-4160-8e49-f8a275c9b2f0

Superblock backups stored on blocks:

32768, 98304, 163840, 229376, 294912, 819200, 884736

Allocating group tables: done

Writing inode tables: done

Creating journal (32768 blocks): done

Writing superblocks and filesystem accounting information: done

root@ubuntu:/home/philip#

From the above output, the mkfs utility, particularly mkfs.ext4 creates the file system on the raw partition; then, it assigns a UUID to uniquely identify the /dev/sdb1 partition.

Note: You need to have root privilege before you can format a partition(s).

Next, let us use the ext3 file system for the /dev/sdb2:

root@ubuntu:/home/philip# mkfs.ext3 /dev/sdb2

mke2fs 1.42.13 (17-May-2015)

Creating filesystem with 524288 4k blocks and 131328 inodes

Filesystem UUID: fd6aab0f-0f16-4922-86c1-11fcb54fc466

Superblock backups stored on blocks:

32768, 98304, 163840, 229376, 294912

Allocating group tables: done

Writing inode tables: done

Creating journal (16384 blocks): done

Writing superblocks and filesystem accounting information: done

root@ubuntu:/home/philip#

Now, we will use the ext2 for the /dev/sdb3 and the ntfs for the /dev/sdb4:

root@ubuntu:/home/philip# mkfs.ext2 /dev/sdb3

mke2fs 1.42.13 (17-May-2015)

Creating filesystem with 1572608 4k blocks and 393216 inodes

Filesystem UUID: b7e075df-541d-468d-ab16-e3ec2e5fb5f8

Superblock backups stored on blocks:

32768, 98304, 163840, 229376, 294912, 819200, 884736

Allocating group tables: done

Writing inode tables: done

Writing superblocks and filesystem accounting information: done

root@ubuntu:/home/philip# mkfs.ntfs /dev/sdb4

Cluster size has been automatically set to 4096 bytes.

Initializing device with zeroes: 100% - Done.

Creating NTFS volume structures.

mkntfs completed successfully. Have a nice day.

root@ubuntu:/home/philip#

Note: You can also use the mke2fs to create an ext2 file system.

Now we have just formatted the /dev/sdb1, /dev/sdb2, dev/sdb3 and the /dev/sdb4. If we now rerun the lsblk command with the -f option, we will now see the file system type (FSTYPE) populated for the two respective partitions:

root@ubuntu:/home/philip# lsblk -f

NAME FSTYPE LABEL UUID MOUNTPOINT

sda

├─sda1 ext4 adb5d090-3400-4411-aee2-dd871c39db38 /

├─sda2

└─sda5 swap 025b1992-80ba-46ed-8490-e7aa68271e7b [SWAP]

sdb

├─sdb1 ext4 fc51dddf-c23d-4160-8e49-f8a275c9b2f0

├─sdb2 ext3 fd6aab0f-0f16-4922-86c1-11fcb54fc466

├─sdb3 ext2 b7e075df-541d-468d-ab16-e3ec2e5fb5f8

└─sdb4 ntfs 1D9E4A6D4088D79A

sr0

root@ubuntu:/home/philip#

From the above output, we can see that the file system type (FSTYPE) reflects the changes which we made.

We can also rerun the blkid command to view the UUIDs created for the /dev/sdb1 and /dev/sdb2:

root@ubuntu:/home/philip# blkid

/dev/sda1: UUID="adb5d090-3400-4411-aee2-dd871c39db38" TYPE="ext4" PARTUUID="f54f42a0-01"

/dev/sda5: UUID="025b1992-80ba-46ed-8490-e7aa68271e7b" TYPE="swap" PARTUUID="f54f42a0-05"

/dev/sdb1: UUID="fc51dddf-c23d-4160-8e49-f8a275c9b2f0" TYPE="ext4" PARTUUID="7e707ac0-01"

/dev/sdb2: UUID="fd6aab0f-0f16-4922-86c1-11fcb54fc466" SEC_TYPE="ext2" TYPE="ext3" PARTUUID="7e707ac0-02"

/dev/sdb3: UUID="2a8a5768-1a7f-4ab4-8aa1-f45d30df5631" TYPE="ext2" PARTUUID="7e707ac0-03"

/dev/sdb4: UUID="1D9E4A6D4088D79A" TYPE="ntfs" PARTUUID="7e707ac0-04"

root@ubuntu:/home/philip#

As you can see, the system can now store information on the respective partitions.

[Mounting and unmounting a partition](#contents.xhtml_sc34a)

The final step after formatting a partition is to mount the partition. We use the mount command to mount a partition, and the umount command to unmount a partition. The mount command is also used for viewing the current mount points in our system. However, after a reboot, all partitions are unmounted unless we created entries into the /etc/fstab directory.

Note: You need root privilege to save any change in the /etc/fstab. Also, back up any configuration file(s) before making any change(s).

[The mount command](#contents.xhtml_sc35a)

We can issue the mount command without any arguments to view the current mount points:

root@ubuntu:/home/philip# mount

sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)

proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)

udev on /dev type devtmpfs (rw,nosuid,relatime,size=478356k,nr_inodes=119589,mode=755)

devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)

tmpfs on /run type tmpfs (rw,nosuid,noexec,relatime,size=99764k,mode=755)

/dev/sda1 on / type ext4 (rw,relatime,errors=remount-ro,data=ordered)

securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)

tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)

tmpfs on /run/lock type tmpfs (rw,nosuid,nodev,noexec,relatime,size=5120k)

tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)

cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/lib/systemd/systemd-cgroups-agent,name=systemd)

pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)

cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)

cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)

cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup

(rw,relatime,user_id=0,group_id=0,default_permissions,allow_other)

tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,size=99764k,mode=700,uid=1000,gid=1000)

gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=1000)

root@ubuntu:/home/philip#

Some output omitted for brevity.

From the above output, we can see several mount points (a mount point is simply associating a partition/drive to a folder/directory). We can filter the mount command to only display the /dev/:

root@ubuntu:/home/philip# mount | grep /dev

udev on /dev type devtmpfs (rw,nosuid,relatime,size=478356k,nr_inodes=119589,mode=755)

devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)

/dev/sda1 on / type ext4 (rw,relatime,errors=remount-ro,data=ordered)

tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)

cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)

mqueue on /dev/mqueue type mqueue (rw,relatime)

hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime)

root@ubuntu:/home/philip#

Based on the filter, we can see the /dev/sda1 is currently mounted on the / directory. As you are aware, the / directory is the root directory. All other directories fall under the / directory.

We can also use the df command with the -h option to view a more concise output:

root@ubuntu:/home/philip# df -h

Filesystem Size Used Avail Use% Mounted on

udev 468M 0 468M 0% /dev

tmpfs 98M 6.2M 92M 7% /run

/dev/sda1 19G 5.1G 13G 29% /

tmpfs 488M 212K 487M 1% /dev/shm

tmpfs 5.0M 4.0K 5.0M 1% /run/lock

tmpfs 488M 0 488M 0% /sys/fs/cgroup

tmpfs 98M 44K 98M 1% /run/user/1000

root@ubuntu:/home/philip#

Now this is presented in a structured format and easier to read. Based on the output, only the /dev/sda1 partition is currently mounted.

We can now go ahead and mount the /dev/sdb1 on /mnt. The /mnt is an empty directory, which we would use whenever we want to mount a partition.

Note: Only one partition can be mounted at any given time.

We will run the mount command as follows:

root@ubuntu:/# mount /dev/sdb1 /mnt

root@ubuntu:/#

Note, without any options, the mount command worked without an error. Now, let us rerun the mount command and filter for only the /dev:

root@ubuntu:/# mount | grep /dev

udev on /dev type devtmpfs (rw,nosuid,relatime,size=478356k,nr_inodes=119589,mode=755)

devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)

/dev/sda1 on / type ext4 (rw,relatime,errors=remount-ro,data=ordered)

tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)

cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)

mqueue on /dev/mqueue type mqueue (rw,relatime)

hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime)

/dev/sdb1 on /mnt type ext4 (rw,relatime,data=ordered)

root@ubuntu:/#

Based on the above output, we can see that the /dev/sdb1 is currently mounted on the /mnt.

We can also leverage the df command with the h option to see similar results:

root@ubuntu:/# df -h

Filesystem Size Used Avail Use% Mounted on

udev 468M 0 468M 0% /dev

tmpfs 98M 6.2M 92M 7% /run

/dev/sda1 19G 5.1G 13G 29% /

tmpfs 488M 212K 487M 1% /dev/shm

tmpfs 5.0M 4.0K 5.0M 1% /run/lock

tmpfs 488M 0 488M 0% /sys/fs/cgroup

tmpfs 98M 44K 98M 1% /run/user/1000

/dev/sdb1 4.8G 10M 4.6G 1% /mnt

root@ubuntu:/#

From the above output, we can see the size of the partition along with the mount point associated with the partition.

Let us now create two directories to be used for the /dev/sdb2 and the /dev/sdb4 partitions:

root@ubuntu:/# mkdir /folder1

root@ubuntu:/# mkdir /folder2

root@ubuntu:/# ls

bin dev folder2 initrd.img.old lost+found opt run srv usr vmlinuz.old

boot etc home lib media proc sbin sys var

cdrom folder1 initrd.img lib64 mnt root snap tmp vmlinuz

root@ubuntu:/#

Now we will mount the /dev/sdb2 and the /dev/sdb4 on the /folder1 and /folder2 directories, respectively:

root@ubuntu:/# mount /dev/sdb2 /folder1

root@ubuntu:/# mount /dev/sdb4 /folder2

root@ubuntu:/#

root@ubuntu:/# mount | grep /dev

/dev/sda1 on / type ext4 (rw,relatime,errors=remount-ro,data=ordered)

/dev/sdb1 on /mnt type ext4 (rw,relatime,data=ordered)

/dev/sdb2 on /folder1 type ext3 (rw,relatime,data=ordered)

/dev/sdb4 on /folder2 type fuseblk (rw,relatime,user_id=0,group_id=0,allow_other,blksize=4096)

root@ubuntu:/#

Now we can see our mount points being displayed with the mount command. Likewise, we can use the df command with the -h option for a readable format:

root@ubuntu:/# df -h

Filesystem Size Used Avail Use% Mounted on

udev 468M 0 468M 0% /dev

tmpfs 98M 6.2M 92M 7% /run

/dev/sda1 19G 5.1G 13G 29% /

tmpfs 488M 212K 487M 1% /dev/shm

tmpfs 5.0M 4.0K 5.0M 1% /run/lock

tmpfs 488M 0 488M 0% /sys/fs/cgroup

tmpfs 98M 44K 98M 1% /run/user/1000

/dev/sdb1 4.8G 10M 4.6G 1% /mnt

/dev/sdb2 2.0G 3.1M 1.9G 1% /folder1

/dev/sdb4 2.0G 11M 2.0G 1% /folder2

root@ubuntu:/#

As you can see, the steps involved in mounting a partition are straight forward. However, on some distributions, you will have to specify the file system type. In a network, mounting a share is something commonly done. An example to mount a share would be:

root@ubuntu:/#mount //172.16.175.144/share /netshare -t cifs -o user=philip,password=pass123,uid=1000,gid=1000,rw

[The umount command](#contents.xhtml_sc36a)

After we would have mounted our partitions, made changes, it is always a good idea to clean up and unmount our partitions. We use the umount command to unmount a partition.

Note: Always change/move out of a directory before running the umount command.

Let us unmount the /dev/sdb1. The format would be:

root@ubuntu:/# umount /dev/sdb1

root@ubuntu:/#

root@ubuntu:/# mount | grep /dev

udev on /dev type devtmpfs (rw,nosuid,relatime,size=478356k,nr_inodes=119589,mode=755)

devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)

/dev/sda1 on / type ext4 (rw,relatime,errors=remount-ro,data=ordered)

tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)

cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)

mqueue on /dev/mqueue type mqueue (rw,relatime)

hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime)

/dev/sdb2 on /folder1 type ext3 (rw,relatime,data=ordered)

/dev/sdb4 on /folder2 type fuseblk (rw,relatime,user_id=0,group_id=0,allow_other,blksize=4096)

root@ubuntu:/#

Now, we can see that the /dev/sdb1 is no longer mounted, we can also confirm by using the df command:

root@ubuntu:/# df -h

Filesystem Size Used Avail Use% Mounted on

udev 468M 0 468M 0% /dev

tmpfs 98M 7.5M 91M 8% /run

/dev/sda1 19G 5.2G 13G 30% /

tmpfs 488M 212K 487M 1% /dev/shm

tmpfs 5.0M 4.0K 5.0M 1% /run/lock

tmpfs 488M 0 488M 0% /sys/fs/cgroup

tmpfs 98M 48K 98M 1% /run/user/1000

/dev/sdb2 2.0G 3.1M 1.9G 1% /folder1

/dev/sdb4 2.0G 11M 2.0G 1% /folder2

root@ubuntu:/#

We can also use the lsblk command to confirm same:

root@ubuntu:/# lsblk -f

NAME FSTYPE LABEL UUID MOUNTPOINT

sda

├─sda1 ext4 adb5d090-3400-4411-aee2-dd871c39db38 /

├─sda2

└─sda5 swap 025b1992-80ba-46ed-8490-e7aa68271e7b [SWAP]

sdb

├─sdb1 ext4 fc51dddf-c23d-4160-8e49-f8a275c9b2f0

├─sdb2 ext3 fd6aab0f-0f16-4922-86c1-11fcb54fc466 /folder1

├─sdb3 ext2 2a8a5768-1a7f-4ab4-8aa1-f45d30df5631

└─sdb4 ntfs 1D9E4A6D4088D79A /folder2

sr0

root@ubuntu:/#

Let us also unmount the /dev/sdb2:

root@ubuntu:/# umount /folder1

root@ubuntu:/# lsblk -f

NAME FSTYPE LABEL UUID MOUNTPOINT

sda

├─sda1 ext4 adb5d090-3400-4411-aee2-dd871c39db38 /

├─sda2

└─sda5 swap 025b1992-80ba-46ed-8490-e7aa68271e7b [SWAP]

sdb

├─sdb1 ext4 fc51dddf-c23d-4160-8e49-f8a275c9b2f0

├─sdb2 ext3 fd6aab0f-0f16-4922-86c1-11fcb54fc466

├─sdb3 ext2 2a8a5768-1a7f-4ab4-8aa1-f45d30df5631

└─sdb4 ntfs 1D9E4A6D4088D79A /folder2

sr0

root@ubuntu:/#

From the above, you will notice that instead of the partition /dev/sdb2, we used the directory /folder1, this is entirely up to you, they both are accepted.

Now, let us say that you want your mount points to persist during a system reboot. Well rest assured we can make this happen by creating entries in the /etc/fstab.

Let us create an entry for the /dev/sdb4 inside the /etc/fstab. We will use the UUID for the /dev/sdb4 to assist us. Let us run blkid and save the UUID for the /dev/sdb4:

root@ubuntu:/# blkid

/dev/sdb4: UUID="1D9E4A6D4088D79A" TYPE="ntfs" PARTUUID="7e707ac0-04"

root@ubuntu:/#

Now, let us edit the /etc/fstab file:

# /etc/fstab: static file system information.

#

# Use 'blkid' to print the universally unique identifier for a

# device; this may be used with UUID= as a more robust way to name devices

# that works even if disks are added and removed. See fstab(5).

#

# <file system> <mount point> <type> <options> <dump> <pass>

# / was on /dev/sda1 during installation

UUID=adb5d090-3400-4411-aee2-dd871c39db38 / ext4 errors=remount-ro 0 1

# swap was on /dev/sda5 during installation

UUID=025b1992-80ba-46ed-8490-e7aa68271e7b none swap sw 0 0

/dev/fd0 /media/floppy0 auto rw,user,noauto,exec,utf8 0 0

UUID=1D9E4A6D4088D79A /folder2 ntfs 0 0

Now, the last entry is referencing the /dev/sdb4. The format starts with the partition, represented by the UUID, followed by the mount point, file system, dump, and pass.

When the system reboots, the /dev/sdb4 will be mounted onto the /folder2. This saves us from repetitive typing.

[Logical volume management](#contents.xhtml_sc37a)

Logical Volume Management (LVM) is a flexible and powerful disk management framework in Linux that allows for dynamic allocation, resizing, and management of logical storage volumes. LVM provides an abstraction layer between physical storage devices (such as hard drives or solid-state drives) and the file systems that use them. This allows for more efficient utilization of storage space and simplified storage management. Let us explore the key components and concepts of LVM:

*   Physical Volumes (PVs): A physical volume is a storage device, such as a hard drive or a partition, that is recognized and managed by LVM. It combines multiple physical volumes into a single pool of storage. PVs can be created using the pvcreate command.
*   Volume Groups (VGs): A volume group is a collection of physical volumes that function as a unified storage pool. VGs enable the aggregation of storage space from multiple physical volumes. You can create volume groups using the vgcreate command.
*   Logical Volumes (LVs): A logical volume represents a flexible partition that resides within a volume group. LVs are created from the available space in volume groups and can be resized dynamically. They are like traditional partitions but offer more flexibility. The lvcreate command is used to create logical volumes.
*   Extents: Extents are fixed-size blocks of data used by LVM. They represent the smallest unit of allocation in a volume group and are typically 4 MB in size. Logical volumes are composed of one or more extents.
*   Striping: Striping is a technique used to distribute data across multiple physical volumes to improve performance. LVM allows you to stripe data across multiple logical volumes, which in turn can be distributed across different physical volumes.
*   Mirroring: LVM supports mirroring, which provides data redundancy by maintaining multiple copies of data. Mirroring enhances data reliability and availability. You can create mirrored logical volumes using the lvcreate command with the --mirrors option.
*   Snapshot volumes: LVM allows the creation of snapshot volumes, which are temporary copies of logical volumes at a specific point in time. Snapshot volumes enable data backup, testing, and other operations without affecting the original logical volume.
*   LVM tools: Linux provides a set of command-line tools for managing LVM. Some commonly used commands include pvcreate for creating physical volumes, vgcreate for creating volume groups, lvcreate for creating logical volumes, and lvresize for resizing logical volumes.
*   LVM file system support: LVM works seamlessly with various file systems such as ext4, XFS, and Btrfs. After creating logical volumes, you can format them with a file system of your choice using tools like mkfs.
*   LVM snapshots and backups: LVM snapshots can be used for creating point-in-time backups of logical volumes. By taking a snapshot, you can capture the state of a logical volume and back it up without interrupting ongoing operations.

LVM provides a flexible and scalable approach to disk management in Linux, allowing for dynamic allocation, resizing, and efficient utilization of storage space. It offers features like striping, mirroring, snapshots, and simplified management of logical volumes. With LVM, you can adapt your storage configuration to changing needs without disrupting data availability or requiring extensive manual disk management operations.

We can setup LVM by using the following examples:

*   Creating physical volumes:

# pvcreate /dev/sdb1 /dev/sdc1

*   Creating a volume group:

# vgcreate myvg /dev/sdb1 /dev/sdc1

*   Creating and managing logical volumes:
    *   Creating a logical volume:

        # lvcreate -L 10G -n mylv myvg

*   LVM file system operations:
    *   Formatting a logical volume with ext4:

# mkfs.ext4 /dev/myvg/mylv

*   Mounting a logical volume:

# mount /dev/myvg/mylv /mnt/mylv

Optionally, we can resize, extend, reduce, create striping and mirroring, snapshots, backup, and restore using the following examples:

*   Resizing or extending a logical volume:

# lvextend -L +25G /dev/myvg/mylv

The -L +25G specifies the new size of the logical volume. In this case, it is increasing the volume by 25GB.

*   Reducing a logical volume:

# lvreduce -L -10G /dev/myvg/mylv

The -L -10G shrinks the size of the logical volume, in this case, to 10G.

*   Striping and mirroring:
    *   Creating striped logical volumes

        # lvcreate -L 20G -i 2 -I 64 -n stripedlv myvg

    *   Creating mirrored logical volumes

        # lvcreate -L 20G -m 1 -n mirroredlv myvg

*   Creating and managing LVM snapshots:
    *   Creating a snapshot volume

        # lvcreate -L 15G -s -n snapshotlv /dev/myvg/mylv

    *   Taking a snapshot

        # lvcreate -s -n snapshot2lv -L 15G /dev/myvg/mylv

*   LVM backup and restore:
    *   Backing up a logical volume using snapshot

        # lvcreate -L 15G -s -n backupsnapshotlv /dev/myvg/mylv

    *   Restoring a logical volume from a snapshot

        # lvconvert --merge /dev/myvg/backsnapshotlv

[Conclusion](#contents.xhtml_sc38a)

In this chapter, we looked at ways of manipulating files and directories. We touched on creating, removing, to name a few. Next, we looked at ways to navigate between directories, creating and removing directories. Finally, we focused on various ways to configure storage devices from within the Linux terminal. In the next chapter, we will cover processes, services, and network configuration.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 3Processes, Services and Network Configuration](#contents.xhtml_ch03a)

[Introduction](#contents.xhtml_sc39a)

In the previous chapter, we covered various files, directories, and storage.

In this chapter, we will focus on processes, services, and network configuration.

First, we will focus on processes, and then we will cover services. Finally, we will wrap up this chapter by looking at network configuration.

[Structure](#contents.xhtml_sc40a)

In this chapter, we will discuss the following topics:

*   Processes
*   Services
*   Network configuration

[Objectives](#contents.xhtml_sc41a)

In this chapter, we will delve into the management of processes. We will explore the concept of systemd, a system and service manager that plays a crucial role in controlling and supervising processes in a Linux environment. Additionally, we will dive into IP addresses, understanding their significance in networking and how they facilitate communication between devices. Furthermore, we will delve into configuring network settings, equipping ourselves with the knowledge and skills to set up and customize network configurations to suit specific requirements.

[Processes](#contents.xhtml_sc42a)

In Linux, a process is an instance of a program being executed. It represents the execution of a specific task or a program in the operating system. Processes are fundamental to the multitasking capability of Linux, allowing multiple programs to run concurrently and share system resources.

Here are some key points to understand about Linux processes:

*   Each process is assigned a unique Process ID (PID) identifier. PIDs are integers that are used by the operating system to keep track of and manage processes.
*   Processes in Linux can be in various states, including:
    *   Running: The process is currently executing on the CPU.
    *   Sleeping: The process is waiting for an event or resource to become available.
    *   Stopped: The process has been stopped by a user or a signal.
    *   Zombie: A process that has completed execution but still has an entry in the process table until its parent acknowledges its termination.
*   Process Control Block (PCB): The operating system maintains a PCB data structure for each process. The PCB contains information about the process, including its PID, state, register values, memory allocation, open files, and other relevant details.
*   Parent and child processes: In Linux, a process can create child processes. The process that creates a new process is called the parent process, and the newly created process is called the child process. Parent and child processes can communicate with each other and share resources.
*   Process scheduling: The Linux kernel is responsible for managing the execution of processes on the CPU. It uses scheduling algorithms to determine which process gets to run and for how long. The scheduler ensures fair access to system resources and efficient CPU utilization.
*   Interprocess communication (IPC): Processes in Linux can communicate with each other through various mechanisms known as IPC. IPC mechanisms include pipes, shared memory, message queues, sockets, and signals. These mechanisms enable processes to exchange data and synchronize their actions.
*   Process termination: A process can terminate voluntarily by calling the exit system call or involuntarily due to an error or a signal received. When a process terminates, it releases the resources it was using and notifies its parent process.

[The ps command](#contents.xhtml_sc43a)

The ps command, which stands for Process Status, is one of today's most popular commands. It displays the current processes running within a system. Often, we work within a Linux environment and overlook the underlying processes that make it all possible. All the information the ps command displays comes from a popular directory, the /proc file system. The /proc is not a real file system per se; it is, in fact, a virtual file system. It is loaded upon boot time, and you will find the /proc in almost every Linux distribution available today. Let us dive into the ps command.

To begin, we can display any process(s) that have started in the current shell:

[philip@localhost ~]$ ps

PID TTY TIME CMD

2220 pts/0 00:00:00 bash

95677 pts/0 00:00:00 ps

[philip@localhost ~]$

Based on the above output, we have not started any other process(s) in the current shell except for the ps command and bash shell. We can also list all the processes currently current within a system using the ps command; we would pass the -A option:

[philip@localhost ~]$ ps -A

PID TTY TIME CMD

1 ? 00:00:31 systemd

2 ? 00:00:00 kthreadd

3 ? 00:00:02 ksoftirqd/0

5 ? 00:00:00 kworker/0:0H

7 ? 00:00:00 migration/0

8 ? 00:00:00 rcu_bh

9 ? 00:00:12 rcu_sched

10 ? 00:00:11 watchdog/0

12 ? 00:00:00 kdevtmpfs

13 ? 00:00:00 netns

14 ? 00:00:00 khungtaskd

15 ? 00:00:00 writeback

95730 ? 00:00:00 kworker/0:3

95747 ? 00:00:00 sleep

95748 pts/0 00:00:00 ps

[philip@localhost ~]$

Some output was omitted for brevity. When we run the ps command with either the -A or -e option, it will only print out the process IDs and the names of each process. However, we can expand this output even further. We can pass the -a option along with the -u. This will print out processes for the current user who opened the terminal:

[philip@localhost ~]$ ps -au

USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND

root 1042 0.0 2.5 306324 25956 tty1 Rsl+ Aug08 0:25 /usr/bin/X :0 -background none -noreset -audit 4 -verbose -auth /run/gdm/auth-for-gd

philip 2220 0.0 0.1 116304 1332 pts/0 Ss Aug08 0:00 bash

philip 95843 0.0 0.1 151064 1816 pts/0 R+ 06:19 0:00 ps -au

[philip@localhost ~]$

To see all processes owned by the current user in the system, we would pass the -x option:

[philip@localhost ~]$ ps -x

PID TTY STAT TIME COMMAND

1487 ? Sl 0:00 /usr/bin/gnome-keyring-daemon --daemonize --login

1491 ? Ssl 0:01 /usr/libexec/gnome-session-binary --session gnome-classic

1498 ? S 0:00 dbus-launch --sh-syntax --exit-with-session

1499 ? Ssl 0:00 /bin/dbus-daemon --fork --print-pid 4 --print-address 6 --session

1567 ? Sl 0:00 /usr/libexec/gvfsd

1572 ? Sl 0:00 /usr/libexec/gvfsd-fuse /run/user/1000/gvfs -f -o big_writes

1664 ? Ss 0:00 /usr/bin/ssh-agent /bin/sh -c exec -l /bin/bash -c "env GNOME_SHELL_SESSION_MODE=classic gnome-session --session gnome-cla

1683 ? Sl 0:00 /usr/libexec/at-spi-bus-launcher

1688 ? Sl 0:00 /bin/dbus-daemon --config-file=/usr/share/defaults/at-spi2/accessibility.conf --nofork --print-address 3

Some output was omitted for brevity. We can also specify a user as part of the argument with the -u:

[philip@localhost ~]$ ps -au root

PID TTY TIME CMD

1 ? 00:00:31 systemd

2 ? 00:00:00 kthreadd

3 ? 00:00:02 ksoftirqd/0

5 ? 00:00:00 kworker/0:0H

Some output was omitted for brevity. We can also see all the users in addition to the path to the executable for each daemon; we would use the -aux or aux- (this is the bind syntax):

[philip@localhost ~]$ ps -aux

USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND

root 1 0.0 0.4 193700 4216 ? Ss Aug08 0:31 /usr/lib/systemd/systemd --switched-root --system --deserialize 21

root 2 0.0 0.0 0 0 ? S Aug08 0:00 [kthreadd]

root 3 0.0 0.0 0 0 ? S Aug08 0:02 [ksoftirqd/0]

root 5 0.0 0.0 0 0 ? S< Aug08 0:00 [kworker/0:0H]

dbus 570 0.0 0.2 36524 2236 ? Ssl Aug08 0:14 /bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activati

chrony 571 0.0 0.0 115640 672 ? S Aug08 0:00 /usr/sbin/chronyd

avahi 585 0.0 0.0 30072 28 ? S Aug08 0:00 avahi-daemon: chroot helper

philip 2209 0.0 0.0 313472 644 ? Sl Aug08 0:00 /usr/libexec/gvfsd-metadata

philip 2213 0.0 1.0 720692 10608 ? Sl Aug08 0:05 /usr/libexec/gnome-terminal-server

Some output was omitted for brevity. Based on the above output, we can see various user accounts. Some accounts are actual system accounts, such as the dbus account. We can also specify a user account ID:

[philip@localhost ~]$ ps -ux 1000

USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND

philip 1487 0.0 0.0 462496 996 ? Sl Aug08 0:00 /usr/bin/gnome-keyring-daemon --daemonize --login

philip 1491 0.0 0.1 761348 1512 ? Ssl Aug08 0:01 /usr/libexec/gnome-session-binary --session gnome-classic

philip 1498 0.0 0.0 13976 0 ? S Aug08 0:00 dbus-launch --sh-syntax --exit-with-session

philip 1499 0.0 0.1 36284 1276 ? Ssl Aug08 0:00 /bin/dbus-daemon --fork --print-pid 4 --print-address 6 --session

philip 1567 0.0 0.0 386352 0 ? Sl Aug08 0:00 /usr/libexec/gvfsd

philip 1572 0.0 0.0 415548 52 ? Sl Aug08 0:00 /usr/libexec/gvfsd-fuse /run/user/1000/gvfs -f -o big_writes

Some output omitted for brevity. Adding to this, displaying processes owned by a particular group is also possible. It is possible by passing either the group name or ID. If we are passing the group name, then we would use the -g option:

[philip@localhost ~]$ ps -fg postfix

UID PID PPID C STIME TTY TIME CMD

postfix 1110 1108 0 Aug08 ? 00:00:00 qmgr -l -t unix -u

postfix 95714 1108 0 06:12 ? 00:00:00 pickup -l -t unix -u

[philip@localhost ~]$

Then to pass the group ID, we would pass the -G option:

[philip@localhost ~]$ ps -fg 89

UID PID PPID C STIME TTY TIME CMD

[philip@localhost ~]$

[philip@localhost ~]$ ps -fG 89

UID PID PPID C STIME TTY TIME CMD

postfix 1110 1108 0 Aug08 ? 00:00:00 qmgr -l -t unix -u

postfix 95714 1108 0 06:12 ? 00:00:00 pickup -l -t unix -u

[philip@localhost ~]$

We can also search for a process by specifying the Process ID (PID). We would pass the -f, which will print a long listing, along with the -p, which expects a numerical value:

[philip@localhost ~]$ ps -fp 1982

UID PID PPID C STIME TTY TIME CMD

philip 1982 1 0 Aug08 ? 00:00:00 /usr/libexec/tracker-store

[philip@localhost ~]$

We can even specify multiple processes on the same line; we would separate the processes by a comma:

[philip@localhost ~]$ ps -fp 1982,2001,2219

UID PID PPID C STIME TTY TIME CMD

philip 1982 1 0 Aug08 ? 00:00:00 /usr/libexec/tracker-store

philip 2001 1730 0 Aug08 ? 00:00:00 /usr/libexec/ibus-engine-simple

philip 2219 2213 0 Aug08 ? 00:00:00 gnome-pty-helper

[philip@localhost ~]$

It is also possible to find a command by specifying the process ID by passing the -o option:

[philip@localhost ~]$ ps -fp 955 -o comm=

sshd

[philip@localhost ~]$

Based on the above output, only the actual executable for the respective PID is displayed.

It is also possible to get memory and CPU information using the ps command; we would pass the -e along with the -o. Then we would need to specify the column names which interest us. Here is how we would accomplish this:

[philip@localhost ~]$ ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head -14

PID PPID CMD %MEM %CPU

1710 1491 /usr/bin/gnome-shell 17.9 0.0

1926 1491 /usr/bin/gnome-software --g 7.1 0.0

1042 989 /usr/bin/X :0 -background n 2.5 0.0

95581 633 /sbin/dhclient -d -q -sf /u 1.3 0.0

2213 1 /usr/libexec/gnome-terminal 1.1 0.0

605 1 /usr/lib/polkit-1/polkitd - 1.1 0.0

1872 1491 /usr/libexec/gnome-settings 0.8 0.0

633 1 /usr/sbin/NetworkManager -- 0.8 0.0

1890 1491 nautilus-desktop --force 0.7 0.0

2050 1915 /usr/libexec/evolution-cale 0.6 0.0

1291 1 /usr/libexec/packagekitd 0.6 0.0

632 1 /usr/bin/python -Es /usr/sb 0.4 0.0

1990 1915 /usr/libexec/evolution-cale 0.4 0.0

[philip@localhost ~]$

Based on the above output, we have specified the pid, ppid, cmd, %mem, %cpu. Adding to this, the --sort option was added. This looks for the processes that have used most of the system RAM and displays those first, starting from highest to lowest. In addition, we have added the head command; this will only display the top portion of the content. We specified the number of lines (-14) with the head command, and this will limit the output to the first 14 lines. However, the output from the ps command is not refreshed in real-time; we can use yet another popular command to see the output refresh in real time instead of us having to rerun the command. We would use the watch command to accomplish this task:

[philip@localhost ~]$ watch -n 1 'ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head'

Based on the above output, we have sorted the output to view the processes taking up most of the CPU within the system. To view the output of the ps command in a hierarchical view, we would pass the -f along with --forest options:

[philip@localhost ~]$ ps -af --forest

UID PID PPID C STIME TTY TIME CMD

philip 99053 2220 0 07:29 pts/0 00:00:00 ps -af --forest

[philip@localhost ~]$ ps -axf --forest

PID TTY STAT TIME COMMAND

2 ? S 0:00 [kthreadd]

3 ? S 0:02 \_ [ksoftirqd/0]

517 ? S<sl 0:00 /sbin/auditd

519 ? S<sl 0:01 \_ /sbin/audispd

521 ? S< 0:00 \_ /usr/sbin/sedispatch

543 ? SNsl 0:04 /usr/libexec/rtkit-daemon

1664 ? Ss 0:00 \_ /usr/bin/ssh-agent /bin/sh -c exec -l /bin/bash -c "env GNOME_SHELL_SESSION_MODE=classic gnome-session --sessi

1710 ? Sl 5:01 \_ /usr/bin/gnome-shell

1730 ? Sl 0:00 | \_ ibus-daemon --xim --panel disable

1743 ? Sl 0:00 | \_ /usr/libexec/ibus-dconf

2001 ? Sl 0:00 | \_ /usr/libexec/ibus-engine-simple

1872 ? Sl 0:18 \_ /usr/libexec/gnome-settings-daemon

Some output was omitted for brevity.

[The kill command](#contents.xhtml_sc44a)

The kill command is used for terminating processes. We can leverage the ps command we just covered to identify a process, then call the kill command to end the process. Here is how we would stop a process using the kill command:

[philip@localhost ~]$ ps -p 1788

PID TTY TIME CMD

1788 ? 00:00:00 goa-daemon

[philip@localhost ~]$

[philip@localhost ~]$ kill -9 1788

[philip@localhost ~]$ ps -fp 1788

UID PID PPID C STIME TTY TIME CMD

[philip@localhost ~]$

We used the number 9,  which means to send a SIGKILL. To see the various signals we can pass, we can use the -l option with the kill command:

[philip@localhost ~]$ kill -l

1) SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGILL 5) SIGTRAP

6) SIGABRT 7) SIGBUS 8) SIGFPE 9) SIGKILL 10) SIGUSR1

11) SIGSEGV 12) SIGUSR2 13) SIGPIPE 14) SIGALRM 15) SIGTERM

16) SIGSTKFLT 17) SIGCHLD 18) SIGCONT 19) SIGSTOP 20) SIGTSTP

21) SIGTTIN 22) SIGTTOU 23) SIGURG 24) SIGXCPU 25) SIGXFSZ

26) SIGVTALRM 27) SIGPROF 28) SIGWINCH 29) SIGIO 30) SIGPWR

31) SIGSYS 34) SIGRTMIN 35) SIGRTMIN+1 36) SIGRTMIN+2 37) SIGRTMIN+3

38) SIGRTMIN+4 39) SIGRTMIN+5 40) SIGRTMIN+6 41) SIGRTMIN+7 42) SIGRTMIN+8

43) SIGRTMIN+9 44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13

48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12

53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9 56) SIGRTMAX-8 57) SIGRTMAX-7

58) SIGRTMAX-6 59) SIGRTMAX-5 60) SIGRTMAX-4 61) SIGRTMAX-3 62) SIGRTMAX-2

63) SIGRTMAX-1 64) SIGRTMAX

[philip@localhost ~]$

To stop a process using the signal name, we would pass the -s option:

[philip@localhost ~]$ ps -fp 1990

UID PID PPID C STIME TTY TIME CMD

philip 1990 1915 0 Aug08 ? 00:00:00 /usr/libexec/evolution-calendar-factory-subprocess --factory contacts --bus-name org.gnome.evolution

[philip@localhost ~]$ kill -s SIGKILL 1915

[philip@localhost ~]$ ps -fp 1915

UID PID PPID C STIME TTY TIME CMD

[philip@localhost ~]$

Note: Caution should be taken whenever stopping process(s) with the SIGTERM while calling the kill command.

[The pstree command](#contents.xhtml_sc45a)

Another flavor of the ps command can be used to view processes within a system. The pstree command; will present all processes in a hierarchical layout. This is what it would look like:

[philip@localhost ~]$ pstree

systemd─┬─ModemManager───2*[{ModemManager}]

├─NetworkManager─┬─dhclient

│ └─3*[{NetworkManager}]

├─VGAuthService

├─2*[abrt-watch-log]

├─abrtd

├─accounts-daemon───2*[{accounts-daemon}]

├─alsactl

├─at-spi-bus-laun─┬─dbus-daemon───{dbus-daemon}

│ └─3*[{at-spi-bus-laun}]

├─at-spi2-registr───2*[{at-spi2-registr}]

├─atd

[philip@localhost ~]$

Some output was omitted for brevity. We can also highlight a specific process by passing the -H option:

[root@localhost Desktop]# pstree -h 1735

rsyslogd───3*[{rsyslogd}]

[root@localhost Desktop]#

We can also display processes specific only to a user; we would pass the username:

[root@localhost Desktop]# pstree philip

bonobo-activati───{bonobo-activat}

clock-applet

gnome-session─┬─bluetooth-apple

├─gdu-notification

├─gnome-panel

├─gnome-power-man

├─gnome-volume-co

├─gpk-update-icon───{gpk-update-ico}

├─metacity───{metacity}

├─nautilus

├─nm-applet

├─polkit-gnome-au

├─python

├─restorecond

└─{gnome-session}

gdm-user-switch

gnome-keyring-d───2*[{gnome-keyring-}]

wnck-applet

[root@localhost Desktop]#

Some output was omitted for brevity.

[The pgrep command](#contents.xhtml_sc46a)

The Process Grep, commonly known as pgrep is another popular method for finding process IDs at the shell. If we know the process name, then we can specify it with the pgrep command:

[root@localhost Desktop]# pgrep rsyslogd

545

[root@localhost Desktop]#

We can see the PID for the rsyslogd based on the above output. We can also find processes for a particular user. We would pass the -u option:

[root@localhost Desktop]# pgrep -u root rsyslogd

545

[root@localhost Desktop]#

[The pkill command](#contents.xhtml_sc47a)

The pkill command is another known method used for terminating processes. It empowers us to use the process name when terminating a given process. In its simplest form, we would:

[philip@localhost ~]$ pgrep rsyslogd

545

[philip@localhost ~]$ pkill rsyslogd

pkill: killing pid 545 failed: Operation not permitted

[philip@localhost ~]$ su

Password:

[root@localhost philip]# pkill rsyslogd

[root@localhost philip]# pgrep rsyslogd

[root@localhost philip]#

Based on the above output, we can see the effectiveness of the pkill command.

The top command, a table of processes, is similar to Windows Task Manager. You will find a wide variety of Linux distributions that support the top command. The top command is essentially used to derive the system’s CPU and memory utilization. The output is structured by creating a list of running processes selected by user-specified criteria; the output is in real-time. The PID for each process is listed in the first column. Let us have a look at it:

[philip@localhost ~]$ top

top - 12:50:44 up 5 days, 11:44, 2 users, load average: 0.01, 0.02, 0.05

Tasks: 165 total, 1 running, 164 sleeping, 0 stopped, 0 zombie

%Cpu(s): 12.1 us, 1.4 sy, 0.0 ni, 86.1 id, 0.0 wa, 0.0 hi, 0.4 si, 0.0 st

KiB Mem : 999696 total, 95804 free, 633636 used, 270256 buff/cache

KiB Swap: 2097148 total, 1852900 free, 244248 used. 137728 avail Mem

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND

1710 philip 20 0 1943720 175920 15680 S 9.3 17.6 5:32.99 gnome-shell

1042 root 20 0 306324 26188 1864 S 5.6 2.6 1:13.99 X

2213 philip 20 0 721204 11976 5992 S 2.7 1.2 0:15.04 gnome-terminal-

1934 philip 20 0 389192 6308 1952 S 0.3 0.6 5:25.10 vmtoolsd

103282 philip 20 0 157716 2260 1540 R 0.3 0.2 0:00.28 top

1 root 20 0 193700 4248 2484 S 0.0 0.4 0:33.67 systemd

2 root 20 0 0 0 0 S 0.0 0.0 0:00.21 kthreadd

Some output was omitted for brevity. To the far right is a COMMAND column, which shows the executable's name. We can filter and display their corresponding processes; we would pass the -u option with top:

[philip@localhost ~]$ top -u philip

top - 12:55:24 up 5 days, 11:49, 2 users, load average: 0.25, 0.08, 0.06

Tasks: 164 total, 2 running, 162 sleeping, 0 stopped, 0 zombie

%Cpu(s): 55.4 us, 6.8 sy, 0.0 ni, 36.5 id, 1.4 wa, 0.0 hi, 0.0 si, 0.0 st

KiB Mem : 999696 total, 73184 free, 641804 used, 284708 buff/cache

KiB Swap: 2097148 total, 1856364 free, 240784 used. 128952 avail Mem

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND

1710 philip 20 0 1943720 177568 16612 S 42.7 17.8 5:39.32 gnome-shell

2213 philip 20 0 721204 12256 6228 S 2.6 1.2 0:15.61 gnome-terminal-

1934 philip 20 0 389192 6308 1952 S 0.3 0.6 5:25.37 vmtoolsd

103360 philip 20 0 157716 2260 1544 R 0.3 0.2 0:00.06 top

1487 philip 20 0 462496 1504 1004 S 0.0 0.2 0:00.08 gnome-keyring-d

1491 philip 20 0 761348 2140 1220 S 0.0 0.2 0:01.77 gnome-session-b

1498 philip 20 0 13976 0 0 S 0.0 0.0 0:00.00 dbus-launch

1499 philip 20 0 36284 1600 600 S 0.0 0.2 0:00.72 dbus-daemon

1567 philip 20 0 386352 864 592 S 0.0 0.1 0:00.02 gvfsd

Some output was omitted for brevity. Based on the above output, only the user philip is displayed with the processes. We can view the absolute path for all processes by pressing c inside the top command:

[philip@localhost ~]$ top -u philip

top - 12:57:58 up 5 days, 11:51, 2 users, load average: 0.04, 0.07, 0.06

Tasks: 164 total, 1 running, 163 sleeping, 0 stopped, 0 zombie

%Cpu(s): 7.5 us, 1.0 sy, 0.0 ni, 91.5 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st

KiB Mem : 999696 total, 74376 free, 640628 used, 284692 buff/cache

KiB Swap: 2097148 total, 1856512 free, 240636 used. 130144 avail Mem

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND

1710 philip 20 0 1943720 177580 16612 S 5.3 17.8 5:41.28 /usr/bin/gnome-shell

2213 philip 20 0 721204 12256 6228 S 1.0 1.2 0:15.85 /usr/libexec/gnome-terminal-server

1693 philip 20 0 205848 1124 824 S 0.3 0.1 0:00.32 /usr/libexec/at-spi2-registryd --use-gnome-session

1487 philip 20 0 462496 1504 1004 S 0.0 0.2 0:00.08 /usr/bin/gnome-keyring-daemon --daemonize --login

1491 philip 20 0 761348 2140 1220 S 0.0 0.2 0:01.77 /usr/libexec/gnome-session-binary --session gnome-classic

1498 philip 20 0 13976 0 0 S 0.0 0.0 0:00.00 dbus-launch --sh-syntax --exit-with-session

1499 philip 20 0 36284 1600 600 S 0.0 0.2 0:00.72 /bin/dbus-daemon --fork --print-pid 4 --print-address 6 --session

1567 philip 20 0 386352 864 592 S 0.0 0.1 0:00.02 /usr/libexec/gvfsd

1572 philip 20 0 415548 52 52 S 0.0 0.0 0:00.00 /usr/libexec/gvfsd-fuse /run/user/1000/gvfs -f -o big_writes

1664 philip 20 0 51332 48 0 S 0.0 0.0 0:00.90 /usr/bin/ssh-agent /bin/sh -c exec -l /bin/bash -c "env GNOME_SHELL_SESSION_MODE+

1683 philip 20 0 344520 136 136 S 0.0 0.0 0:00.00 /usr/libexec/at-spi-bus-launcher

Some output omitted for brevity. Now we can see the location for each process. We can also change how often the output is refreshed; the default is every 3 seconds. We would press d from within the top command:

top - 13:00:16 up 5 days, 11:54, 2 users, load average: 0.07, 0.06, 0.05

Tasks: 165 total, 2 running, 163 sleeping, 0 stopped, 0 zombie

%Cpu(s): 1.3 us, 1.3 sy, 0.0 ni, 97.3 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st

KiB Mem : 999696 total, 74112 free, 640884 used, 284700 buff/cache

KiB Swap: 2097148 total, 1856512 free, 240636 used. 129888 avail Mem

Change delay from 3.0 to

We will type 2 here so the updates will refresh every 2 seconds. Now when we press d once again, we will notice the difference in the prompt:

op - 13:01:21 up 5 days, 11:55, 2 users, load average: 0.02, 0.04, 0.05

Tasks: 165 total, 2 running, 163 sleeping, 0 stopped, 0 zombie

%Cpu(s): 10.6 us, 2.0 sy, 0.0 ni, 87.4 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st

KiB Mem : 999696 total, 73864 free, 641052 used, 284780 buff/cache

KiB Swap: 2097148 total, 1856512 free, 240636 used. 129720 avail Mem

Change delay from 2.0 to

[philip@localhost ~]$

To see help with top, we can press h:

Help for Interactive Commands - procps-ng version 3.3.10

Window 1:Def: Cumulative mode Off. System: Delay 3.0 secs; Secure mode Off.

Z,B,E,e Global: 'Z' colors; 'B' bold; 'E'/'e' summary/task memory scale

l,t,m Toggle Summary: 'l' load avg; 't' task/cpu stats; 'm' memory info

0,1,2,3,I Toggle: '0' zeros; '1/2/3' cpus or numa node views; 'I' Irix mode

f,F,X Fields: 'f'/'F' add/remove/order/sort; 'X' increase fixed-width

L,&,<,> . Locate: 'L'/'&' find/again; Move sort column: '<'/'>' left/right

R,H,V,J . Toggle: 'R' Sort; 'H' Threads; 'V' Forest view; 'J' Num justify

c,i,S,j . Toggle: 'c' Cmd name/line; 'i' Idle; 'S' Time; 'j' Str justify

x,y . Toggle highlights: 'x' sort field; 'y' running tasks

z,b . Toggle: 'z' color/mono; 'b' bold/reverse (only if 'x' or 'y')

u,U,o,O . Filter by: 'u'/'U' effective/any user; 'o'/'O' other criteria

n,#,^O . Set: 'n'/'#' max tasks displayed; Show: Ctrl+'O' other filter(s)

C,... . Toggle scroll coordinates msg for: up,down,left,right,home,end

k,r Manipulate tasks: 'k' kill; 'r' renice

d or s Set update interval

W,Y Write configuration file 'W'; Inspect other output 'Y'

q Quit

(commands shown with '.' require a visible task display window )

Press 'h' or '?' for help with Windows,

Type q or <Esc> to continue

We can change how the memory is displayed inside the top utility; depending on the current memory output, the display will toggle when we would press m:

top - 13:09:50 up 5 days, 12:03, 2 users, load average: 0.00, 0.04, 0.05

Tasks: 164 total, 1 running, 163 sleeping, 0 stopped, 0 zombie

%Cpu(s): 4.1 us, 0.7 sy, 0.0 ni, 95.2 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st

Based on the above output, the section for the memory is hidden. When we press m once again, this will change:

top - 13:10:41 up 5 days, 12:04, 2 users, load average: 0.00, 0.04, 0.05

Tasks: 163 total, 1 running, 162 sleeping, 0 stopped, 0 zombie

%Cpu(s): 12.1 us, 1.7 sy, 0.0 ni, 86.2 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st

KiB Mem : 999696 total, 73648 free, 641204 used, 284844 buff/cache

KiB Swap: 2097148 total, 1856528 free, 240620 used. 129568 avail Mem

Now when we press m, we will see a graphical design:

top - 13:11:39 up 5 days, 12:05, 2 users, load average: 0.00, 0.03, 0.05

Tasks: 163 total, 1 running, 162 sleeping, 0 stopped, 0 zombie

%Cpu(s): 27.4 us, 4.1 sy, 0.0 ni, 68.2 id, 0.0 wa, 0.0 hi, 0.3 si, 0.0 st

KiB Mem : 87.0/999696 [||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||| ]

KiB Swap: 11.5/2097148 [||||||||||| ]

Now we have the nice bars indicating the memory usage for both RAM and Swap. Similarly, we can change the display of the output by CPU; we would press t:

top - 13:19:23 up 5 days, 12:13, 2 users, load average: 0.30, 0.11, 0.07

Tasks: 163 total, 3 running, 160 sleeping, 0 stopped, 0 zombie

2 sleeping, 0 stopped, 0 zombie

%Cpu(s): 9.6/1.4 11[||||||||||| ]

KiB Mem : 999696 total, 73524 free, 641328 used, 284844 buff/cache

KiB Swap: 2097148 total, 1856532 free, 240616 used. 129444 avail Mem

Note: When we press t it will then turn the bars into a shaded output.

Adding to this, the processes can also be displayed in a hierarchical output; we would press Shift+v:

KiB Mem : 999696 total, 72064 free, 646164 used, 281468 buff/cache

KiB Swap: 2097148 total, 1856764 free, 240384 used. 124676 avail Mem

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND

1491 philip 20 0 761348 2132 1220 S 0.0 0.2 0:01.77 `- gnome-session-b

1664 philip 20 0 51332 48 0 S 0.0 0.0 0:00.91 `- ssh-agent

1710 philip 20 0 1943720 178948 16836 S 1.0 17.9 6:28.95 `- gnome-shell

1730 philip 20 0 450876 632 0 S 0.0 0.1 0:00.04 `- ibus-daemon

1743 philip 20 0 373544 116 116 S 0.0 0.0 0:00.00 `- ibus-dconf

2001 philip 20 0 299880 64 0 S 0.0 0.0 0:00.00 `- ibus-engine-sim

Some output was omitted for brevity. To turn off the forest view, we would simply toggle the Shift+v once again:

1498 philip 20 0 13976 0 0 S 0.0 0.0 0:00.00 dbus-launch

1499 philip 20 0 36284 1600 600 S 0.0 0.2 0:00.72 dbus-daemon

1567 philip 20 0 386352 864 592 S 0.0 0.1 0:00.02 gvfsd

1572 philip 20 0 415548 52 52 S 0.0 0.0 0:00.00 gvfsd-fuse

1664 philip 20 0 51332 48 0 S 0.0 0.0 0:00.91 ssh-agent

Some output omitted for brevity. We can also stop a process using the top command; we would press k which is for killing process(s) inside of the top command:

Tasks: 164 total, 1 running, 163 sleeping, 0 stopped, 0 zombie

%Cpu(s): 3.0/0.5 4[ ]

KiB Mem : 999696 total, 76468 free, 641756 used, 281472 buff/cache

KiB Swap: 2097148 total, 1856800 free, 240348 used. 129084 avail Mem

PID to signal/kill [default pid = 1710]

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND

1710 philip 20 0 1944552 176788 16840 S 1.5 17.7 6:36.40 gnome-shell

2213 philip 20 0 721724 16020 8740 S 0.5 1.6 0:22.60 gnome-terminal-

Based on the above output, we would need to specify a process ID:

KiB Swap: 2097148 total, 1856800 free, 240348 used. 129084 avail Mem

Send pid 1718 signal [15/sigterm]

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND

1710 philip 20 0 1944552 176788 16840 S 1.5 17.7 6:36.40 gnome-shell

2213 philip 20 0 721724 16020 8740 S 0.5 1.6 0:22.60 gnome-terminal-

We need to specify the signal to send to the process; the default is 15 SIGTERM. We will accept the default; this will terminate the process without having us exit the top utility.

[Services](#contents.xhtml_sc48a)

The service command was initially used to run SysV init scripts on early Linux distributions before 17ystem. Depending on what you are trying to accomplish, the method you use to start, stop or restart a service will depend upon whether your distribution uses ystem or init. The positive coming out of the service command is that most Linux engineers prefer to use it as opposed to the newer method of handling processes in system environments. Thus, in most newer distributions the service command is supported. The syntax for the service command is:

service <process> <status>

To view all services on a system that rus SysV scripts, we will use the CentOS6.5 system:

[philip@localhost Desktop]$ service --status-all

abrt-ccpp hook is installed

abrtd (pid 2254) is running...

abrt-dump-oops is stopped

acpid (pid 1964) is running...

atd (pid 2273) is running...

auditd (pid 1710) is running...

Usage: /etc/init.d/bluetooth {start|stop}

cpuspeed is stopped

crond (pid 2262) is running...

cupsd (pid 1874) is running...

dnsmasq (pid 2087) is running...

firstboot is not scheduled to run

hald (pid 1975) is running...

htcacheclean is stopped

httpd is stopped

winbindd is stopped

wpa_supplicant (pid 1875) is running...

[philip@localhost Desktop]$

Some output was omitted for brevity. The scripts which the service command reads start with an rc. We can quickly view all related scripts by:

[philip@localhost Desktop]$ ls -l /etc | grep rc.

lrwxrwxrwx. 1 root root 11 Jun 20 01:37 init.d -> rc.d/init.d

lrwxrwxrwx. 1 root root 7 Jun 20 01:40 rc -> rc.d/rc

lrwxrwxrwx. 1 root root 10 Jun 20 01:40 rc0.d -> rc.d/rc0.d

lrwxrwxrwx. 1 root root 10 Jun 20 01:40 rc1.d -> rc.d/rc1.d

lrwxrwxrwx. 1 root root 10 Jun 20 01:40 rc2.d -> rc.d/rc2.d

lrwxrwxrwx. 1 root root 10 Jun 20 01:40 rc3.d -> rc.d/rc3.d

lrwxrwxrwx. 1 root root 10 Jun 20 01:40 rc4.d -> rc.d/rc4.d

lrwxrwxrwx. 1 root root 10 Jun 20 01:40 rc5.d -> rc.d/rc5.d

lrwxrwxrwx. 1 root root 10 Jun 20 01:40 rc6.d -> rc.d/rc6.d

drwxr-xr-x. 10 root root 4096 Jun 20 05:50 rc.d

lrwxrwxrwx. 1 root root 13 Jun 20 01:40 rc.local -> rc.d/rc.local

lrwxrwxrwx. 1 root root 15 Jun 20 01:40 rc.sysinit -> rc.d/rc.sysinit

[philip@localhost Desktop]$

To control the status of a process, we can do this:

[philip@localhost Desktop]$ service crond status

crond (pid 4457) is running...

[philip@localhost Desktop]$

From the above output, this process is currently running. We can change this. Let us say we wanted to stop the crond process; we would simply replace status with stop:

[philip@localhost Desktop]$ service crond stop

User has insufficient privilege.

[philip@localhost Desktop]$

Based on the above output, we run into a roadblock; this can easily be remedied by becoming the root user:

[root@localhost Desktop]# service crond stop

Stopping crond: [ OK ]

[root@localhost Desktop]#

Awesome job! Now we can rerun the service command; this time using the “status” option:

[root@localhost Desktop]# service crond status

crond is stopped

[root@localhost Desktop]#

And there we have it. The service has been stopped. To start back up this process, we would simply replace stop with a start:

[root@localhost Desktop]# service crond start

Starting crond: [ OK ]

[root@localhost Desktop]#

Now let’s try to start the process once again:

[root@localhost Desktop]# service crond status

crond (pid 6606) is running...

[root@localhost Desktop]#

If we have changes to the process and need to restart it, we can do it in several ways. We can stop the process and then start it again:

[root@localhost Desktop]# service crond stop

Stopping crond: [ OK ]

[root@localhost Desktop]# service crond start

Starting crond: [ OK ]

[root@localhost Desktop]#

Also, we can use the restart option:

[root@localhost Desktop]# service crond restart

Stopping crond: [ OK ]

Starting crond: [ OK ]

[root@localhost Desktop]#

Lastly, we can use the reload option; this last option will re-read the configuration files for any changes that have been made:

[root@localhost Desktop]# service crond reload

Reloading crond: [ OK ]

[root@localhost Desktop]# service crond status

crond (pid 6703) is running...

[root@localhost Desktop]#

[Managing services with the systemctl command](#contents.xhtml_sc49a)

On most newer distributions that use systemd, we manage processes using the systemctl command. However, Linux developers have also left support for the service command; if we try to terminate a process using it, we will see that it redirects our request to the systemctl command. Let us try this:

[root@localhost philip]# service crond status

Redirecting to /bin/systemctl status crond.service

*   crond.service - Command Scheduler

    Loaded: loaded (/usr/lib/systemd/system/crond.service; enabled; vendor preset: enabled)

    Active: active (running) since Thu 2018-08-02 07:13:38 PDT; 1 weeks 5 days ago

    Main PID: 991 (crond)

    CGroup: /system.slice/crond.service

    └─991 /usr/sbin/crond -n

    Aug 02 07:13:38 localhost.localdomain systemd[1]: Started Command Scheduler.

    Aug 02 07:13:38 localhost.localdomain systemd[1]: Starting Command Scheduler...

    Aug 02 07:13:38 localhost.localdomain crond[991]: (CRON) INFO (RANDOM_DELAY will be scaled with factor 15% if used.)

    Aug 02 07:13:43 localhost.localdomain crond[991]: (CRON) INFO (running with inotify support)

    [root@localhost philip]#

    Based on the output, we can see that the service command is being redirected:

    [root@localhost philip]# service crond status

    Redirecting to /bin/systemctl status crond.service

*   crond.service - Command Scheduler

    Let us use the newer approach for managing processes; we will use the systemctl command. The format is:

    Systemctl <action><process>

    We can use this at the shell:

    [root@localhost philip]# systemctl status atd

*   atd.service - Job spooling tools

    Loaded: loaded (/usr/lib/systemd/system/atd.service; enabled; vendor preset: enabled)

    Active: active (running) since Thu 2018-08-02 07:13:38 PDT; 1 weeks 5 days ago

    Main PID: 993 (atd)

    CGroup: /system.slice/atd.service

    └─993 /usr/sbin/atd -f

    Aug 02 07:13:38 localhost.localdomain systemd[1]: Started Job spooling tools.

    Aug 02 07:13:38 localhost.localdomain systemd[1]: Starting Job spooling tools...

    [root@localhost philip]#

    To start a process using systemctl, we would pass the start option:

    [root@localhost philip]# systemctl start rsyslog.service

    [root@localhost philip]#

    We can check on the status of a process by passing the status option:

    [root@localhost philip]# systemctl status rsyslog.service

*   rsyslog.service - System Logging Service

    Loaded: loaded (/usr/lib/systemd/system/rsyslog.service; enabled; vendor preset: enabled)

    Active: active (running) since Tue 2018-08-14 08:29:22 PDT; 5s ago

    Docs: man:rsyslogd(8)

    http://www.rsyslog.com/doc/

    Main PID: 117499 (rsyslogd)

    CGroup: /system.slice/rsyslog.service

    └─117499 /usr/sbin/rsyslogd -n

    Aug 14 08:29:22 localhost.localdomain systemd[1]: Starting System Logging Service...

    Aug 14 08:29:22 localhost.localdomain rsyslogd[117499]: [origin software="rsyslogd" swVersion="8.24.0" x-pid="117499" x-info="http://www.rs...] start

    Aug 14 08:29:22 localhost.localdomain systemd[1]: Started System Logging Service.

    Hint: Some lines were ellipsized, use -l to show in full.

    [root@localhost philip]#

    You will notice that the output from the systemctl command is much more intuitive than the older service command in early Linux distributions. We can also stop a process using the systemctl command; we would pass the stop option:

    [root@localhost philip]# systemctl stop rsyslog.service

    [root@localhost philip]# systemctl status rsyslog.service

*   rsyslog.service - System Logging Service

    Loaded: loaded (/usr/lib/systemd/system/rsyslog.service; enabled; vendor preset: enabled)

    Active: inactive (dead) since Tue 2018-08-14 08:38:38 PDT; 8s ago

    Docs: man:rsyslogd(8)

    http://www.rsyslog.com/doc/

    Process: 117499 ExecStart=/usr/sbin/rsyslogd -n $SYSLOGD_OPTIONS (code=exited, status=0/SUCCESS)

    Main PID: 117499 (code=exited, status=0/SUCCESS)

    Aug 14 08:29:22 localhost.localdomain systemd[1]: Starting System Logging Service...

    Aug 14 08:29:22 localhost.localdomain rsyslogd[117499]: [origin software="rsyslogd" swVersion="8.24.0" x-pid="117499" x-info="http://www.rs...] start

    Aug 14 08:29:22 localhost.localdomain systemd[1]: Started System Logging Service.

    Aug 14 08:38:38 localhost.localdomain rsyslogd[117499]: [origin software="rsyslogd" swVersion="8.24.0" x-pid="117499" x-info="http://www.rs...nal 15.

    Aug 14 08:38:38 localhost.localdomain systemd[1]: Stopping System Logging Service...

    Aug 14 08:38:38 localhost.localdomain systemd[1]: Stopped System Logging Service.

    Hint: Some lines were ellipsized, use -l to show in full.

    [root@localhost philip]#

    Also, we can restart or reload a process:

    [root@localhost philip]# systemctl restart rsyslog.service

    [root@localhost philip]# systemctl status rsyslog.service

*   rsyslog.service - System Logging Service

    Loaded: loaded (/usr/lib/systemd/system/rsyslog.service; enabled; vendor preset: enabled)

    Active: active (running) since Tue 2018-08-14 08:39:37 PDT; 2s ago

    Docs: man:rsyslogd(8)

    http://www.rsyslog.com/doc/

    Main PID: 117730 (rsyslogd)

    CGroup: /system.slice/rsyslog.service

    └─117730 /usr/sbin/rsyslogd -n

    Aug 14 08:39:37 localhost.localdomain systemd[1]: Starting System Logging Service...

    Aug 14 08:39:37 localhost.localdomain rsyslogd[117730]: [origin software="rsyslogd" swVersion="8.24.0" x-pid="117730" x-info="http://www.rs...] start

    Aug 14 08:39:37 localhost.localdomain systemd[1]: Started System Logging Service.

    Hint: Some lines were ellipsized, use -l to show in full.

    [root@localhost philip]#

Based on the above output, it simply started the process when we passed the restart option. The processes that systemctl handles are considered as units when using the systemctl command. We can view the units by passing list-unit-files:

[root@localhost philip]# systemctl list-units --all --state=active

UNIT LOAD ACTIVE SUB DESCRIPTION

proc-sys-fs-binfmt_misc.automount loaded active waiting Arbitrary Executable File Formats File System Automount Point

dev-cdrom.device loaded active plugged VMware_Virtual_IDE_CDROM_Drive

dev-disk-by\x2did-ata\x2dVMware_Virtual_IDE_CDROM_Drive_10000000000000000001.device loaded active plugged VMware_Virtual_IDE_CDROM_Drive

dev-disk-by\x2dpath-pci\x2d0000:00:07.1\x2data\x2d2.0.device loaded active plugged VMware_Virtual_IDE_CDROM_Drive

dev-disk-by\x2dpath-pci\x2d0000:00:10.0\x2dscsi\x2d0:0:0:0.device loaded active plugged VMware_Virtual_S

dev-disk-by\x2dpath-pci\x2d0000:00:10.0\x2dscsi\x2d0:0:0:0\x2dpart1.device loaded active plugged VMware_Virtual_S 1

dev-disk-by\x2dpath-pci\x2d0000:00:10.0\x2dscsi\x2d0:0:0:0\x2dpart2.device loaded active plugged VMware_Virtual_S 2

dev-disk-by\x2dpath-pci\x2d0000:00:10.0\x2dscsi\x2d0:0:0:0\x2dpart3.device loaded active plugged VMware_Virtual_S 3

dev-disk-by\x2duuid-16e2de7b\x2db679\x2d4a12\x2d888e\x2d55081af4dad8.device loaded active plugged VMware_Virtual_S 3

sys-devices-virtual-net-virbr0\x2dnic.device loaded active plugged /sys/devices/virtual/net/virbr0-nic

[root@localhost philip]#

Some output was omitted for brevity. The various processes are stored in /usr/lib/systemd/system:

[root@localhost philip]# ls /usr/lib/systemd/system

abrt-ccpp.service iscsiuio.socket shutdown.target

abrtd.service kdump.service shutdown.target.wants

abrt-oops.service kexec.target sigpwr.target

abrt-pstoreoops.service kexec.target.wants sleep.target

abrt-vmcore.service kmod-static-nodes.service -.slice

abrt-xorg.service kpatch.service slices.target

accounts-daemon.service ksm.service smartcard.target

alsa-restore.service ksmtuned.service smartd.service

alsa-state.service libstoragemgmt.service sockets.target

alsa-store.service libvirtd.service sockets.target.wants

[root@localhost philip]#

Some output was omitted for brevity. As you can see, a wide variety of processes are managed using the systemctl command.

[Network configuration](#contents.xhtml_sc50a)

Let us first look at IP addressing and then move into network configuration.

[IPv4](#contents.xhtml_sc51a)

An Internet Protocol or IP version 4 is the fourth version of the Internet protocol. It plays a vital role in the internet as we know it. IPv4 is the most used protocol for addressing various devices within a network and out on the internet. Another interesting fact about IP is that it is not connection-oriented, as is the case for TCP. Instead, IP is connectionless. An IPv4 address is made of 32 bits or 4 bytes in length. We calculate the addresses in base 2; this gives us 2^32, which equals 4,294,967,296 addresses. It may seem as though there are plenty of IPv4 addresses. However, the reality differs because there is currently an IPv4 shortage. An IPv4 address is represented in dotted decimal format. An example of an IPv4 address is:

192.168.1.1

Based on the above, we can see that an IPv4 address is indeed represented in a dotted decimal format. The dot (.)  acts as a separator between the address. The numbers can be between 0 and 255, including 0 and 255. Each portion of an IPv4 address is known as an octet. Thus, the four numbers make up 4 octets. Various types of IPv4 addresses are available in today’s environment, particularly within a Local Area Network (LAN). You may see one of the following:

10.0.0.0/8

172.16.0.0/12

192.16.0.0/16

Based on the above, the addresses may look familiar. These three addresses can be further explained by the RFC 1918; which specifies certain addresses to be used within a private network such as a LAN.

We have five classes of address space; the first four are commonly used in various types of environments. These are the following classes of addresses:

Class A 0-127

Class B 128-191

Class C 192-223

Class D 224-239

Class E 240-255

Based on the above, the number range represents the placeholder in the first octet. We can break down an IPv4 address to gain a better understanding. We will use the first octet as the reference. First, we will build a table. Every octet of an IPv4 address represents 1 Byte; 1 Byte = 8 bits. We can then use this information to form our table. Consider [Table 3.1](#ch03.xhtml_tab3-1):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | = 8-bit positions |
| 128 | 64 | 32 | 16 | 18 | 4 | 2 | 1 | = 255 |

Table 3.1: 8-bit positions which make up a byte

Based on the above, we counted from 7 to 0 because we always start at 0 when calculating a value for an octet inside an IPv4 address and move from right to left when adding. Now, the way we got the value above was a result of multiplying 2^x where x = the last character to the right; so, it would be as shown in [Table 3.2](#ch03.xhtml_tab3-2):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | = 8-bit position |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | = 1 means that the bit is turned on |
| 2^ | 2^ | 2^ | 2^ | 2^ | 2^ | 2^ | 2^ | =base 2 |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =Result of base 2 for each bit position |

Table 3.2: Calculations of the 8-bit positions using base 2

Using all the values inside the 8 bits, we get 128+64+32+16+8+4+2+1=255.

Based on the above, we now see how the table is built using base 2 for calculation. Hence, only values between 0-255, including 0 and 255, are legal at any given time.

[Class A](#contents.xhtml_sc52a)

The class A address space, 0-127, looks at the leading bit position (position 7 because we count from 0 to 7) in the first octet, known as the most significant bit position. The 127-address space is reserved, known as the loopback address space. Hence, we only use the values 0-126\. Moreover, the 0 is reserved for network use. We will discuss it later when we cover subnetting. For now, to calculate the first values for a class A, we would do the following as shown in [Table 3.3](#ch03.xhtml_tab3-3):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | = 8-bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =255 |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = 0-127 |

Table 3.3: Calculation of class A addresses

Based on the above, we have all 8 bits turned off in the first octet. Therefore, this gives us the class A address space between 0-126 in the first octet, 0 being reserved and 127 being the loopback space. Hence, the real usable IPv4 addresses in the first octet are 1-126\. This is then followed by the three remaining octets being all zeros. So, the class A address space would be as shown in [Table 3.4](#ch03.xhtml_tab3-4):

| Class A | 0-126.0.0.0/8 where the leading bit is 0 in the 8^(th) bit position |
| Class A reserved address space | 127.0.0.0/8 |
| Class A Automatic Private IP Addressing (APIPA) | 169.0.0.0/8 reserved |

Table 3.4: Class A valid network addresses

Based on the above, we are given a maximum of up to 126 networks we can define. The remaining 3 octets of the Class A address 0.0.0 comprise the host portion; each octet comprises 8 bits. A host is any device that can be assigned an IPv4 address(s). The maximum number of hosts allowed in class A is 16,777,214 per network defined. The host portion results from 2^3 octets (8 bits per octet x 3 =24 bits) - 2 =1677216-2=16777214 hosts per class A network.

[Class B](#contents.xhtml_sc53a)

The class B address spaces 128-191, look at the leading bits position 7 and 6 (remember that we start counting from 0 moving from left to right); the first most significant bit, position 7, is turned on in binary. This is set to 1, and the second most significant bit, position 6, is set to 0; this can be seen using the table we created earlier. Consider [Table 3.5](#ch03.xhtml_tab3-5):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | = 8-bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =255 |
| 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = 128 |

Table 3.5: Class B bit positions

Based on the above, the most significant bit is turned on, and the second most significant bit is turned off; this gives us the address space of 128-191, where 128 is reserved for network use, and 191 is reserved as the broadcast address. We will discuss broadcast addresses later in this chapter when we cover subnetting. In a class B address space, the first 16 bits are reserved for network use; however, 2 bits are reserved, giving us 2^14 = 16384 networks per class B address. Consider [Table 3.6](#ch03.xhtml_tab3-6):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | = 8-bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =255 |
| 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | = 128 |

Table 3.6: Class B valid network addresses

We must skip the first 2 bits, positions 7 and 6, giving us 2^14 = 163864 networks.

Based on the above, we see the maximum number of networks available but not the maximum number of hosts. We use the last 2 octets for the hosts to calculate the hosts for a class B address; we would do 2^2 octets (8 bits per octets x 2 =16 bits), 2 bits for network and broadcast= 65536 -2 = 65534 hosts per class B network.

[Class C](#contents.xhtml_sc54a)

The class C address space 192-223, considers the first 3 most significant bits, namely positions 7,6 and 5\. The first 2 most significant bits are turned on and set to 1 in binary. The third bit, position 5 in binary, is turned off; this is set to 0\. The first 24 bits are reserved for network use in a class C address space. We can then construct our table using this information. Consider [Table 3.7](#ch03.xhtml_tab3-7):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | = 8-bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =255 |
| 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | = 128+64 =>192 |

Table 3.7: Class C bit positions

Based on the above, we can see that the class C address space starts at 192 and ends at 223; 192 is reserved for the network, and 223 is reserved as the broadcast address. We can then calculate the number of networks using 2^21 = 2,097,152 networks. This can be represented in [Table 3.8](#ch03.xhtml_tab3-8):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | = 8-bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =255 |
| 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | = first 3 bits total 192 |

Table 3.8: Class C network addresses

24 bits reserved for Class C, 24 bits - 3 most significant bits = 21, then 2^21 bits = 2,097,152 networks.

The last octet .0 (8 bits), is reserved for the host addresses. This means 2^1 octet (8 bits) -2 bits for network and broadcast = 256 -2 = 254 hosts per class C address.

[Class D](#contents.xhtml_sc55a)

The class D 224-239 address space is reserved for multicast use. The first 3 most significant bits are turned on and set to 1\. The fourth most significant bit is set to 0\. The class D address space is not used for IP addressing as in the previous address classes. Instead, the class D address space assigns an IP address to a multicast group. The hosts then are part of a group that shares a group address. [Table 3.9](#ch03.xhtml_tab3-9) illustrates the bits used for the class D address space:

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | = 8-bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =255 |
| 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | = total 224 |

Table 3.9: Class D bit positions

Based on the above, the class D address space starts at 224.0.0.0 and ends at 239.255.255.255.

[Class E](#contents.xhtml_sc56a)

The class E 240-255 address space is reserved for future use. As such, it is not implemented as the previous address space. The first 4 most significant bits are turned on; there are set to 1\. The only address used in class E is 255.255.255.255; this is known as the all-broadcast address. [Table 3.10](#ch03.xhtml_tab3-10) illustrates the bits which are used for the class E address space:

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | = 8-bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =255 |
| 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | = total 240 |

Table 3.10: Class E bit positions

Based on the above, the class E address space starts at 240.0.0.0 and ends at 255.255.255.255, where all 255.255.255.255 is reserved for all broadcast addresses.

[Subnet mask](#contents.xhtml_sc57a)

We have just covered the various classes of IPv4 address space, but sometimes using those classes of address space might not be appropriate. The fact is that classes A, B, and C are classful address spaces if we use the default subnet mask for those classes of IPs. For instance, class A uses a subnet mask of 255.0.0.0 address space. However, let us discuss what is a subnet mask. To begin with, a subnet mask identifies the network and host portions of a given IP address. This includes both IPv4 and IPv6\. A subnet mask enables us to easily find the network address for a given IP address. It is often written in dotted decimal format; however, it is possible to represent a subnet mask in a slash notation, namely the CIDR notation. Classless Inter Domain Routing (CIDR) represents a subnet mask by appending the number of network bits in a slash format to an IP address. For a class, A address, a subnet mask will be:

255.0.0.0

Based on the above, the value 255.0.0.0 means that all the bits in the first octets are turned on; they are set to 1\. We can present this using the table which we created earlier. Consider [Table 3.11](#ch03.xhtml_tab3-11):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | =bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =2^ bit position |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | = bits turned on |

Table 3.11: Class A subnet mask

128+64+32+16+8+4+2+1=255 bits

Based on the above, the value of 255 is derived from the sum of all 8 bits being turned on. Adding to this, the subnet mask can also be represented in binary format. Using the class A address, the subnet mask could be written as shown in [Table 3.12](#ch03.xhtml_tab3-12):

| Class A subnet mask in decimal | 255.0.0.0 |
| Class A subnet mask in binary | 11111111.00000000.00000000.00000000 |

Table 3.12: Class A subnet mask in decimal and binary representation

Now, we can see that a subnet mask can be represented in either decimal formal using values between 0-255 or in binary format using values of either 0 or 1\. Furthermore, it is possible to represent a subnet mask in CIDR notation. We would represent a class A address in CIDR format using the following table:

| Class A subnet mask in decimal | 255.0.0.0 |
| Class A subnet mask in binary | 11111111.00000000.00000000.00000000 |
| Class A subnet mask in CIDR | /8 |

Table 3.13: Class A subnet mask in CIDR notation

Based on the above, the /8 means that 8 bits are turned on for the network portion of an address.

We would represent a class B address in the following format using the dotted decimal format:

255.255.0.0

Based on the above, the value 255.255.0.0 means that all the bits in the first and second octets are turned on and set to 1\. We can present this using [Table 3.14](#ch03.xhtml_tab3-14):

| First octet |
| 7 6 5 4 3 2 1 0 =bit position |
| 128 64 32 16 8 4 2 1 =2^ bit position |
| 1 1 1 1 1 1 1 1 = bits turned on |
| 128+64+32+16+8+4+2+1=255 bits |
| Second octet |
| 7 6 5 4 3 2 1 0 =bit position |
| 128 64 32 16 8 4 2 1 =2^ bit position |
| 1 1 1 1 1 1 1 1 = bits turned on |
| 128+64+32+16+8+4+2+1=255 bits |

Table 3.14: Class B subnet mask calculation

Based on the above, the value of 255.255.0.0 is derived from the sum of all 16 bits being turned on. Adding to this, the subnet mask can also be represented in binary format. Using the class B address, the subnet mask could be written as shown in [Table 3.15](#ch03.xhtml_tab3-15):

| Class B subnet mask in decimal | 255.255.0.0 |
| Class B subnet mask in binary | 11111111.11111111.00000000.00000000 |

Table 3.15: Class B in decimal and binary representation

Now, we can see that a subnet mask can be represented in either decimal format using values between 0-255 or in binary format using values of either 0 or 1\. Furthermore, it is possible to represent a subnet mask in CIDR notation. We would represent a class B address in CIDR format, as shown in [Table 3.16](#ch03.xhtml_tab3-16):

| Class B subnet mask in decimal | 255.255.0.0 |
| Class B subnet mask in binary | 11111111.11111111.00000000.00000000 |
| Class B subnet mask in CIDR | /16 |

Table 3.16: Class B in CIDR notation

Based on the above, the /16 means that 16 bits are turned on for the network portion of an address.

Using a class C address, we would represent a class C address in the following format using the dotted decimal format:

255.255.255.0

Based on the above, the value 255.255.255.0 means that all the bits in the first and second octets are turned on and set to 1\. We can present this using [Table 3.17](#ch03.xhtml_tab3-17):

| First octet |
| 7 6 5 4 3 2 1 0 =bit position |
| 128 64 32 16 8 4 2 1 =2^ bit position |
| 1 1 1 1 1 1 1 1 = bits turned on |
| 128+64+32+16+8+4+2+1=255 bits |
| Second octet |
| 7 6 5 4 3 2 1 0 =bit position |
| 128 64 32 16 8 4 2 1 =2^ bit position |
| 1 1 1 1 1 1 1 1 = bits turned on |
| 128+64+32+16+8+4+2+1=255 bits |
| Third octet |
| 7 6 5 4 3 2 1 0 =bit position |
| 128 64 32 16 8 4 2 1 =2^ bit position |
| 1 1 1 1 1 1 1 1 = bits turned on |
| 128+64+32+16+8+4+2+1=255 bits |

Table 3.17: Calculation of class C subnet mask

Based on the above, the value of 255.255.255.0 is derived from the sum of all 24 bits being turned on. Adding to this, the subnet mask can also be represented in binary format. Using the class C address, the subnet mask could be written as shown in [Table 3.18](#ch03.xhtml_tab3-18):

| Class C subnet mask in decimal | 255.255.255.0 |
| Class C subnet mask in binary | 11111111.11111111.11111111.00000000 |

Table 3.18: Class C subnet mask in decimal and binary representation

Now, we can see that a subnet mask can be represented in either decimal format using values between 0-255 or binary format using values of either 0,1\. Furthermore, it is possible to represent a subnet mask in CIDR notation. We would represent a class C address in CIDR format, as shown in [Table 3.19](#ch03.xhtml_tab3-19):

| Class C subnet mask in decimal | 255.255.255.0 |
| Class C subnet mask in binary | 11111111.11111111.11111111.00000000 |
| Class C subnet mask in CIDR | /24 |

Table 3.19: Class C subnet mask in CIDR notation

Based on the above, the /24 means that 24 bits are turned on for the network portion of an address.

[Subnetting](#contents.xhtml_sc58a)

As we have seen with the class A, B, and C, their subnet masks are /8, 16, and 24, respectively, using CIDR notation. In most environments today, these default subnet masks are known as classful, meaning if we use them as they are, we would not be able to perform any traffic engineering. This becomes an issue when we want to control the broadcast domain; we should try to minimize the broadcast to a given room, office, or department. This ensures that in the event of any type of network broadcast, the entire network does not start to experience latency. We can leverage subnetting to overcome the limitation of classful networks. For instance, let us pick a class C IP address:

192.168.0.0/24

Based on the above, we can have up to 254 hosts per network address; we might be in a situation where we only have 8 systems that require IP connectivity. We are losing those remaining IP addresses because we have used a default class C subnet. The requirement in this scenario is for 8 IP addresses and not wasting the remaining IPs; we can achieve this requirement by subnetting. Subnetting is made possible by borrowing bits from the host portion. Let us write out the subnet mask for the given IP address. Consider [Table 3.20](#ch03.xhtml_tab3-20):

| 192.168.0.0/24 Network |
| 255.255.255.0  Subnet mask in decimal |
| 11111111.11111111.11111111.00000000 Subnet mask in binary |

Table 3.20: Class C address with subnet mask

Based on the above, the first 24 bits are turned on. We can subnet this address to gain more control over our IP address space; we want 8 IPs. The way we borrow bits is by taking bits from the host bits. We can use [Table 3.21](#ch03.xhtml_tab3-21) for assistance:

| 7 6 5 4 3 2 1 0 =bit position |
| 128 64 32 16 8 4 2 1 =2^ bit position |
| 1 1 1 1 0 0 0 0 =4 bits borrowed |
| 2^4bits = 16 network networks can be created |
| 2^4 -2 =14 hosts per network |

Table 3.21: Class C network and host address calculation

Based on the above, we have borrowed 4 bits from the host portion of the network; this enables us to create 4 smaller subnets/networks. Each network created would then have 14 hosts per network. This allows us to save on the number of lost IPs instead of using a standard class C /24 network. So, we have borrowed 4 bits for the network portion, and we would represent this in decimal and CIDR notation. The way we represent the newly created subnet is by a process of adding the network bits. Consider [Table 3.22](#ch03.xhtml_tab3-22):

| 7 6 5 4 3 2 1 0 =bit position |
| 128 64 32 16 8 4 2 1 =2^ bit position |
| 1 1 1 1 0 0 0 0 =4 bits |
| 128+64+32+16=240 |
| Old subnet in decimal = 255.255.255.0 |
| Old subnet in CIDR = /24 |
| New subnet in decimal = 255.255.255.240 |
| New subnet in CIDR = /28 |
| Network address = 192.168.0.0/28 |

Table 3.22: Subnetting a Class C /24 to /28

Based on the above, we can see the new subnet mask in decimal and CIDR notation. The next step would be identifying the usable subnets/networks using this new subnet mask. We can calculate the usable subnets by using [Table 3.23](#ch03.xhtml_tab3-23):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | =bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =2^ bit position |
| 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | =4 bits |

Table 3.23: Usable networks of /28 subnet

The bit position base two value increments the networks:

First network 192.168.0.0/28

Second network 192.168.0.16/28

Third network 192.168.0.32/28

Forth network 192.168.0.48/28

….

Sixteen network 192.168.0.240/28

Based on the above, we can see that the fourth octet is where the increments occur. In particular, for a /28, the subnets are increments by 16 because the fourth-bit position is 16 when calculated as 2^4 bit position =16\. The last step would be to identify the usable IPs which can be assigned to hosts within the network. We will use the following as a breakdown:

First subnet/network:  192.168.0.0/28

First usable IP address: 192.168.0.1/28

Last usable IP address:  192.168.0.14/28

Broadcast IP address:  192.168.0.15/28

Second subnet/network: 192.168.0.16/28

Based on the above, we see that 2 IPs are not usable; these are what we have been taking into consideration earlier while we were calculating the host's IPs. Similarly, we can get the usable IPs for the second subnet 192.168.0.16/28, by using the following breakdown:

Second subnet/network:  192.168.0.16/28

First usable IP address:  192.168.0.17/28

Last usable IP address:  192.168.0.30/28

Broadcast IP address:   192.168.0.31/28

Third subnet/network:  192.168.0.32/28

Based on the above, we can see the pattern; we always end up with 14 usable IP addresses. Also, we can subnet a Class B address and use host bits to better manage our network. Let us use the following class B address:

172.16.0.0/16

Subnet mask 255.255.0.0

Based on the above, we have over 65000 host IPs per network; this is not ideal in most environments. For instance, we want to subnet this IP to have 500 host IPs. This can be achieved by borrowing some host bits from the host portion of the address. We can use the following breakdown to assist us:

255.255.0.0

11111111.11111111.00000000.00000000 =/16 bits being used

The way we calculate the host is by moving from right to left. Consider [Table 3.24](#ch03.xhtml_tab3-24):

| Fourth octet |  |
| 7 6 5 4 3 2 1 0 | =bit position |
| 128 64 32 16 8 4 2 1 | =2^ bit position |
| 1 1 1 1 1 1 1 1 | =8 bits total 255 |
| 2^8 =255-2 = 254 hosts per network |  |
| Third octet |  |
| 7 6 5 4 3 2 1 0 | =bit position |
| 128 64 32 16 8 4 2 1 | =2^ bit position |
| 0 0 0 0 0 0 0 1 | = 9-bit turned on |
| 2^9 =512 -2 =510 hosts per network |  |

Table 3.24: Class B network address subnet to /23

Based on the above, it will take 9 bits to achieve the requirements; we will have to borrow 8 bits from the third octets to meet the requirements. We can break this down using the following:

255.255.0.0

11111111.11111111.11111110.00000000 =/23 bits being used.

Consider [Table 3.25](#ch03.xhtml_tab3-25):

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | =bit position |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | =2^ bit position |
| 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | =7 bits turned on |

Table 3.25: Class B address subnet to /23

8 bits in first octet + 8 bits in second octet + 7 bits in third octet =23 bits

The sum of the bits turned on in the third octet 128+64+32+16+8+4+2 =254

The new subnet mask in decimal = 255.255.254.0

Based on the above calculations, the new network would be written in the following:

172.16.0.0/23

The total number of subnets = 2 ^ 7 = 128 subnets created.

The total number of hosts per subnet/network =2^9 - 2 = 512 -2 = 510 hosts per subnet/network.

Subnets = 172.16.0.0/23 , 172.16.2.0/23, 172.16.4.0/23, 172.16.6.0/23 - 172.16.254.0/23

We have the total subnet and hosts per subnet based on the above. Now, we need to calculate the usable IP addresses per subnet. This can be done using the following breakdown:

First subnet/network:    172.16.0.0/23

First usable IP:       172.16.0.1/23

Last usable IP:       172.16.2.254/23

Broadcast IP:       172.16.2.255

Second subnet/network: 172.16.2.0/23

Based on the above, we can see the usable IP addresses. The IP address 172.16.2.255 is valid when using a /23 subnet. Also, the IP address 172.16.1.0/23 is valid. In some operating systems, such Windows, you may encounter an error if you try to assign either of these 2 IPs. However, in Linux, everything is fair game. We increment the subnets by 2 because that is where the last network bit position ends.

We can even subnet a class A address. For instance, we want to create 100 subnets from a single class A address. We will use the following:

10.0.0.0/8

255.0.0.0

Consider [Table 3.26](#ch03.xhtml_tab3-26):

| Second octet |
| 7 6 5 4 3 2 1 0 =bit position |
| 128 64 32 16 8 4 2 1 =2^ bit position |
| 1 1 1 1 1 1 1 0 = 7 bits turned on |

Table 3.26: Class A address subnet to /15

Based on the above, we can quickly derive that we need to borrow 7 bits from the second octet to create 100 subnets. We will have 128 subnets. This is because we are calculating 2^7 bits in the second octet. Then we can write out our subnets in the following format:

11111111.11111110.00000000.00000000

Subnet 255.254.0.0 /15

Subnets  10.0.0.0/15, 10.2.0.0/15, 10.4.0.0/15, 10.6.0.0/15 - 10.254.0.0/15

It is easy to subnet a class A; now, we must calculate the total hosts per subnet. We can use the following:

Subnet in binary

11111111.11111110.00000000.00000000

Network bits are represented by n

Host bits are represented by h

nnnnnnnn.nnnnnnnh.hhhhhhhh.hhhhhhhh

2^17 -2 = 131072 - 2 = 131070 hosts per subnet/network

Based on the above, we can see we garner a few hosts per subnet using a /15\. We can use the following to derive the usable IPs per subnet:

First subnet/network: 10.0.0.0/15

First usable IP: 10.0.0.1/15

Last usable IP: 10.2.255.254/15

Broadcast IP: 10.2.255.255

Second subnet/network:  10.2.0.0/15

The easiest way to calculate the subnets is to multiply the network bits by 2\. For calculating the total number of hosts, always multiply the host's bits by 2 and then subtract 2 (for the network and broadcast address).

[IPv6 addressing](#contents.xhtml_sc59a)

IP version 6, or IPv6, was developed by the Internet Engineering Task Force (IETF). The IPv6 address was meant to address the shortage of IPv4 address space. IPv4 has been completely exhausted, and companies are now willing to trade their IPv4 block of addresses for huge sums of money. An IPv6 address is 128-bit or 16 bytes in length. This gives us a total number of 2^128 IPv6 addresses. An IPv6 address is represented in hexadecimal format. There are three types of IPv6 addresses:

*   Unicast: A unicast address specifies an identifier for a single interface on a device, similar to an IPv4 address. Using IPv6, it is likely that all IPv6 traffic will be mostly unicast-based.
*   Multicast: The concept of an IPv6 multicast address is like an IPv4 address. Packets are sent to an IPv6 multicast address, and receivers of a multicast group will receive the multicast packet.
*   Anycast: This address type was introduced in IPv6\. The concept of anycast works by assigning the same IPv6 address to multiple devices. When a sender sends a packet to an anycast IPv6 address, the anycast packet is routed via a routing protocol to the nearest host from the sender.

Here is an example of an IPv6 address:

2001:0db8:0000:0000:0000:ff00:0042:8329

Based on the above, we can see that an IPv6 address comprises 8 sets of 16-bit or 2-byte values separated by colons. This is how we derive 128 bits or 16 bytes in length. It may seem lengthy to write an IPv6 address, but we can use different methods to make an IPv6 address concise. We can do the following:

Remove leading zeros

We can remove the leading zeros from an IPv6 address, thus making it more readable:

2001:0db8:0000:0000:0000:ff00:0042:8329

2001:db8:0:0:0:ff00:42:8329

Based on the above, we made the IPv6 address much more presentable. However, we can also make it even smaller by using the following technique below:

Removing consecutive zeros

We can remove zeros that are contiguous in an IPv6 address and replace the zeros with a double colon; this can only be done once, as seen below:

2001:db8::ff0:42:8329

As we can see, the IPv6 address is now much more readable. Also, when entering an IPv6 address in a browser, we would visit the following link:

http://[ 2001:db8::ff0:42:8329]/

We would enclose an IPv6 address in square brackets based on the above. In addition, some special types of unicast IPv6 addresses are worth mentioning. These are as follows:

*   Global unicast address: These addresses begin with 2000::/3 as specified in RFC 4291; they are publicly routable, similar to public IPv4 addresses.
*   Link-local address: These addresses begin with fe80::/10; they are only valid on the local physical link.
*   Site-local address: These addresses begin with fec::/10; they are valid only within a single site. They have been discouraged by the RFC body.
*   Unique-local address: These addresses begin with fc00::/7; they are meant to be routed within a set of cooperating sites. There were meant to replace the site-local addresses. An interesting feature of the unique-local addresses is that they reduce the risk of addressing conflict.

There are some special IPv6 addresses, like IPv4\. Here are some reserved IPv6 addresses:

*   2000::/3: Global unicast
*   ::/128:  Unspecified address
*   ::/0:  Default route
*   ::1/128: Loopback address
*   FF00::/8: Multicast addresses

To identify the subnet, we would have to dissect an IPv6 address. We can break it down using the following:

2001:db8:0000:0000:0000:ff0:42:8329

Consider [Table 3.27](#ch03.xhtml_tab3-27):

| Global routing prefix | Subnet | Host ID |
| 2001:db8:0000: | 0000: | 0000:ff0:42:8329 |
| 48 bits or 3bytes | 16 bits or 2bytes | 64 bits or 8 bytes |

Table 3.27: IPv6 address

Based on the above, the global routing prefix consists of 48 bits. The subnet is made of the next 16 bits. The host identifier is made up of the last 64 bits.

[IPv4 configuration](#contents.xhtml_sc60a)

There are various ways of configuring an IPv4 address within a Linux system. First, we can use a GUI utility to perform IPv4 configuration. We can select the Network icon and then select the drop-down arrow and select Wired Settings, as shown in [Figure 3.1](#ch03.xhtml_fig3-1):

![](images/Figure3._1_.png)

Figure 3.1: Network settings

Based on the above, when we select Wired Settings, it will open the Settings dialog box; after this, we will select the gear icon. This would then open Network  Settings. To configure the IPv4 settings, we would select the IPv4 tab, as shown in [Figure 3.2](#ch03.xhtml_fig3-2):

![](images/Figure3._2_.png)

Figure 3.2: IP, DNS, routes settings

Based on the above, the default method for IPv4 addressing is Automatic (DHCP); this means that the system will acquire its IPv4 addressing information via a server out on the network configured to issue IPv4 addressing information dynamically. We want to assign our IPv4 address for demonstration using the manual method. After we would have selected Manual, an Addresses field will appear, allowing us to enter the IPv4 addressing information, as can be seen in [Figure 3.3](#ch03.xhtml_fig3-3):

![](images/Figure3._3_.png)

Figure 3.3: Manual IP address configuration

Based on the above, we are allowed to enter the IPv4 information. We have entered an IPv4 address; additionally, we see a text box titled netmask, another subnet mask name. Once we had finished entering the IPv4 address information, we would select the Apply button. An important thing to keep in mind is the fact that we are allowed to configure multiple IPv4 addresses on an interface. We would simply click inside the text box in the second row and enter an IPv4 address of our choice, as seen in [Figure 3.4](#ch03.xhtml_fig3-4):

![](images/Figure3._4_.png)

Figure 3.4: Secondary IP configuration

Based on the above, as we enter the second IPv4 address, another text box appears in the third row; this would happen again if we entered an IPv4 address in the third row. Once we are satisfied with our configuration, we select the Apply button to save our changes.

Another way to manage IPv4 addresses is through the shell; we can add and remove IPv4 addresses using commands at the command prompt.

[ifconfig](#contents.xhtml_sc61a)

The ifconfig command can manage IPv4 addressing information at the command line. We can run the ifconfig command without any options, and it will display only active interfaces, as seen below:

root@philip-virtual-machine:/home/philip# ifconfig

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.16.175.132 netmask 255.255.255.0 broadcast 172.16.175.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

RX packets 75738 bytes 57194615 (57.1 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 35446 bytes 3084763 (3.0 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING> mtu 65536

inet 127.0.0.1 netmask 255.0.0.0

inet6 ::1 prefixlen 128 scopeid 0x10<host>

loop txqueuelen 1000 (Local Loopback)

RX packets 17102 bytes 1274792 (1.2 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 17102 bytes 1274792 (1.2 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

root@philip-virtual-machine:/home/philip#

Based on the above, we get a wealth of information; particularly, the IPv4 addressing is in the inet section. We can filter through to only display the IPv4 addressing information as shown below:

root@philip-virtual-machine:/home/philip# ifconfig | grep inet

inet 172.16.175.132 netmask 255.255.255.0 broadcast 172.16.175.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

inet 127.0.0.1 netmask 255.0.0.0

inet6 ::1 prefixlen 128 scopeid 0x10<host>

root@philip-virtual-machine:/home/philip#

We can see the IPv4 addressing information and some IPv6 based on the above. We had previously configured 2 more IPv4 addresses; however, they are not displayed because only the primary IPv4 address will be displayed by default. We will see in the next command how we can easily view those additional IPv4 addresses. In addition to viewing only active interfaces, we can also view inactive interfaces; we would pass the -a option as shown below:

root@philip-virtual-machine:/home/philip# ifconfig -a

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.16.175.132 netmask 255.255.255.0 broadcast 172.16.175.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

RX packets 75817 bytes 57204880 (57.2 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 35485 bytes 3087793 (3.0 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING> mtu 65536

inet 127.0.0.1 netmask 255.0.0.0

inet6 ::1 prefixlen 128 scopeid 0x10<host>

loop txqueuelen 1000 (Local Loopback)

RX packets 17110 bytes 1275456 (1.2 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 17110 bytes 1275456 (1.2 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

root@philip-virtual-machine:/home/philip#

Based on the above, only one physical interface is on this system, so the output is the same as running the ifconfig command without any option. Furthermore, we can choose which interface we want to be displayed using the ifconfig command; we would specify the interface as shown below:

root@philip-virtual-machine:/home/philip# ifconfig ens33

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.16.175.132 netmask 255.255.255.0 broadcast 172.16.175.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

RX packets 75825 bytes 57205574 (57.2 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 35493 bytes 3088408 (3.0 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

root@philip-virtual-machine:/home/philip#

This is useful in situations where the system may have a lot of interfaces, and you are only interested in a particular interface. We can assign an IPv4 address using the ifconfig command; we would simply pass the interface and the IPv4 address as the following:

root@philip-virtual-machine:/home/philip# ifconfig ens33 172.10.1.1

root@philip-virtual-machine:/home/philip# ifconfig ens33

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.10.1.1 netmask 255.255.0.0 broadcast 172.10.255.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

RX packets 76407 bytes 57564515 (57.5 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 35550 bytes 3099266 (3.0 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

root@philip-virtual-machine:/home/philip#

Based on the above, the primary IPv4 address has been changed to the IPv4 address we specified. So, what if we did not want to remove the previous IPv4 address? We can satisfy this requirement by creating an alias interface; it is merely logical. We would then assign the second IPv4 address to the alias interface. Here is how we would accomplish this:

root@philip-virtual-machine:/home/philip# ifconfig ens33 172.16.175.132/24

root@philip-virtual-machine:/home/philip# ifconfig ens33:0 172.10.1.1

root@philip-virtual-machine:/home/philip# ifconfig ens33

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.16.175.132 netmask 255.255.255.0 broadcast 172.16.175.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

RX packets 76902 bytes 57781395 (57.7 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 35579 bytes 3104505 (3.1 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

root@philip-virtual-machine:/home/philip# ifconfig ens33:0

ens33:0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.10.1.1 netmask 255.255.0.0 broadcast 172.10.255.255

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

root@philip-virtual-machine:/home/philip#

Based on the above, we can now see that we have the original IPv4 on the physical interface in addition to creating an alias interface with the secondary IPv4 address. A point to note is that when we specified the IPv4 address for the alias interface, we did not specify any subnet mask. The system auto detected the subnet mask based on the first octet; the subnet mask was set to a class B subnet mask of 255.255.0.0 or /16\. We can remedy this by either removing the IPv4 address and then add the IPv4 address with the subnet mask in CIDR notation as shown below:

root@philip-virtual-machine:/home/philip# ifconfig ens33:0 down

root@philip-virtual-machine:/home/philip# ifconfig ens33:0

ens33:0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

root@philip-virtual-machine:/home/philip# ifconfig ens33:0 172.10.1.1/23

root@philip-virtual-machine:/home/philip# ifconfig ens33:0

ens33:0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.10.1.1 netmask 255.255.254.0 broadcast 172.10.1.255

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

root@philip-virtual-machine:/home/philip#

Based on the above, if we want to remove the IPv4 address, we could either disable the interface by typing down; then we can add the IPv4 address with a subnet mask in CIDR notation. Adding to this, the broadcast address was set, and the system calculated the broadcast address based on the subnet mask. However, we can set the broadcast using the ifconfig command, and we would pass the broadcast option as shown below:

root@philip-virtual-machine:/home/philip# ifconfig ens33:0 broadcast 172.10.20.255

root@philip-virtual-machine:/home/philip# ifconfig ens33:0

ens33:0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.10.0.1 netmask 255.255.254.0 broadcast 172.10.20.255

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

root@philip-virtual-machine:/home/philip#

Based on the above, the broadcast address was changed using our supplied address. Let us fix this by changing it back to its correct broadcast address:

root@philip-virtual-machine:/home/philip# ifconfig ens33:0 broadcast 172.10.1.255

root@philip-virtual-machine:/home/philip# ifconfig ens33:0

ens33:0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.10.0.1 netmask 255.255.254.0 broadcast 172.10.1.255

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

root@philip-virtual-machine:/home/philip#

Another way to remove the IPv4 address is to pass the del option with the ifconfig command, as shown below:

root@philip-virtual-machine:/home/philip# ifconfig ens33:0 del 172.10.0.1

root@philip-virtual-machine:/home/philip# ifconfig ens33:0

ens33:0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

root@philip-virtual-machine:/home/philip#

Based on the above, the IPv4 address was removed successfully. When we are finished working with the alias, we can remove its configuration by passing the down option, as seen below:

root@philip-virtual-machine:/home/philip# ifconfig ens33:0 down

root@philip-virtual-machine:/home/philip# ifconfig -a

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.16.175.132 netmask 255.255.255.0 broadcast 172.16.175.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

RX packets 77475 bytes 57962754 (57.9 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 35781 bytes 3140240 (3.1 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING> mtu 65536

inet 127.0.0.1 netmask 255.0.0.0

inet6 ::1 prefixlen 128 scopeid 0x10<host>

loop txqueuelen 1000 (Local Loopback)

RX packets 17311 bytes 1289908 (1.2 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 17311 bytes 1289908 (1.2 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

root@philip-virtual-machine:/home/philip#

Based on the above, the interface is no longer recognized with the ifconfig command.

[ifup](#contents.xhtml_sc62a)

The ifup command is used to bring up or enable an interface. The interface is then able to send and receive packets. However, only interfaces listed in /etc/network/interfaces are recognized by the ifup command. Let us shut down the ens33 interface and use the ifup command to bring back up the ens33 interface. Here is how we would do this:

root@philip-virtual-machine:/home/philip# ifconfig ens33 down

root@philip-virtual-machine:/home/philip# ifup ens33

Unknown interface ens33

root@philip-virtual-machine:/home/philip# cat /etc/network/interfaces

# interfaces(5) file used by ifup(8) and ifdown(8)

auto lo

iface lo inet loopback

root@philip-virtual-machine:/home/philip#

Based on the above, the ifup does not recognize the ens33 interface. It is not listed in the /etc/network/interfaces. We can add this entry, and it will work with the ifup command. This can be seen below:

root@philip-virtual-machine:/home/philip# cat /etc/network/interfaces

# interfaces(5) file used by ifup(8) and ifdown(8)

auto lo

iface lo inet loopback

auto ens33

iface ens33 inet manual

root@philip-virtual-machine:/home/philip# ifup ens33

root@philip-virtual-machine:/home/philip# ifconfig

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.16.170.1 netmask 255.255.255.0 broadcast 172.16.170.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

RX packets 77776 bytes 58152478 (58.1 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 35893 bytes 3155908 (3.1 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING> mtu 65536

inet 127.0.0.1 netmask 255.0.0.0

inet6 ::1 prefixlen 128 scopeid 0x10<host>

loop txqueuelen 1000 (Local Loopback)

RX packets 17323 bytes 1290784 (1.2 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 17323 bytes 1290784 (1.2 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

root@philip-virtual-machine:/home/philip#

We can see the if-up command successfully brought up the ens33 interface. Moreover, the IPv4 address assigned was the IPv4 address that we configured via the GUI network settings. In most modern Linux distributions, all network settings are handled by the network-manager service; whenever we change via the command prompt, if the system is restarted or the network-manager service is restarted, all of the changes via the command prompt are lost. The changes that reside only in the network-manager service are used. The workaround would be to stop the network-manger service and disable it. Doing this could leave your system without connectivity if you do not save the changes for your network settings in the /etc/network/interfaces (these include the IP, subnet mask default gateway, and DNS IPs) for the system.

Note: Do not stop the network-manager service unless you are sure that you have saved the network configuration in the /etc/network/interfaces file.

[ifdown](#contents.xhtml_sc63a)

The ifdown command can bring down or disable an interface; only interfaces listed in the /etc/network/interfaces are recognized. Let us bring down the ens33 interface using the ifdown command. This can be shown below:

root@philip-virtual-machine:/home/philip# ifdown ens33

root@philip-virtual-machine:/home/philip# ifconfig

lo: flags=73<UP,LOOPBACK,RUNNING> mtu 65536

inet 127.0.0.1 netmask 255.0.0.0

inet6 ::1 prefixlen 128 scopeid 0x10<host>

loop txqueuelen 1000 (Local Loopback)

RX packets 17323 bytes 1290784 (1.2 MB)

RX errors 0 dropped 0 overruns 0 frame 0

TX packets 17323 bytes 1290784 (1.2 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

root@philip-virtual-machine:/home/philip#

Based on the above, the ifdown command successfully brought down the ens33 interface because we added the ens33 interface inside the /etc/network/interfaces file.

[ip](#contents.xhtml_sc64a)

The ip command is by far more scalable than the ifconfig command. For instance, we can view all the secondary IPv4 addresses configured on every interface with the ip command. Without any option, the ip command will display the options which can be used; this can be seen below:

root@philip-virtual-machine:/home/philip# ip

Usage: ip [ OPTIONS ] OBJECT { COMMAND | help }

ip [ -force ] -batch filename

where OBJECT := { link | address | addrlabel | route | rule | neigh | ntable |

tunnel | tuntap | maddress | mroute | mrule | monitor | xfrm |

netns | l2tp | fou | macsec | tcp_metrics | token | netconf | ila |

vrf | sr }

OPTIONS := { -V[ersion] | -s[tatistics] | -d[etails] | -r[esolve] |

-h[uman-readable] | -iec |

-f[amily] { inet | inet6 | ipx | dnet | mpls | bridge | link } |

-4 | -6 | -I | -D | -B | -0 |

-l[oops] { maximum-addr-flush-attempts } | -br[ief] |

-o[neline] | -t[imestamp] | -ts[hort] | -b[atch] [filename] |

-rc[vbuf] [size] | -n[etns] name | -a[ll] | -c[olor]}

root@philip-virtual-machine:/home/philip#

Based on the above, we can see several options which can be passed; one such option is the a option. This displays all the addressing information as seen below:

root@philip-virtual-machine:/home/philip# ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000

link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00

inet 127.0.0.1/8 scope host lo

valid_lft forever preferred_lft forever

inet6 ::1/128 scope host

valid_lft forever preferred_lft forever

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

link/ether 00:0c:29:32:fc:d5 brd ff:ff:ff:ff:ff:ff

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

root@philip-virtual-machine:/home/philip#

We see multiple IPv4 addresses for the ens33 interface right away. We can add an IPv4 address using the ip command; we would pass the add option. This can be seen below:

root@philip-virtual-machine:/home/philip# ip a add 172.16.20.2/24 dev ens33

root@philip-virtual-machine:/home/philip# ip a | grep ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

inet 172.16.20.2/24 scope global ens33

root@philip-virtual-machine:/home/philip#

We can see the IPv4 address has been added. Similarly, we can remove an IPv4 address; we would pass the del option, as can be seen below:

root@philip-virtual-machine:/home/philip# ip a del 172.16.20.2/24 dev ens33

root@philip-virtual-machine:/home/philip# ip a show ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

link/ether 00:0c:29:32:fc:d5 brd ff:ff:ff:ff:ff:ff

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

root@philip-virtual-machine:/home/philip#

We can see that the IPv4 address we specified with the del option was removed. Also, we used  the show option, which enabled us to specify the interface we were interested in seeing. It is also possible to specify a broadcast address like the ifconfig command; we would pass either the brd or broadcast option as shown below:

root@philip-virtual-machine:/home/philip# ip a add 172.16.20.2/22 brd 255.255.252.0 dev ens33

root@philip-virtual-machine:/home/philip# ip a show ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

link/ether 00:0c:29:32:fc:d5 brd ff:ff:ff:ff:ff:ff

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

inet 172.16.20.2/22 brd 255.255.252.0 scope global ens33

valid_lft forever preferred_lft forever

root@philip-virtual-machine:/home/philip#

We can see the broadcast address being assigned for the IPv4 address. Adding to this, it is possible to shut down or enable an interface with the ip command. We would use pass the link option of the ip command. This can be seen below:

root@philip-virtual-machine:/home/philip# ip link set dev ens33 down

root@philip-virtual-machine:/home/philip# ip a show ens33 | grep DOWN

2: ens33: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000

root@philip-virtual-machine:/home/philip#

We can see that the link has been brought down. Similarly, we can bring up an interface by passing the up option, as seen below:

root@philip-virtual-machine:/home/philip# ip link set dev ens33 up

root@philip-virtual-machine:/home/philip# ip a show ens33 | grep UP

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

root@philip-virtual-machine:/home/philip#

We can see that the interface was brought back up. We can work with an alias using the IP command; we would pass the a or add option with the ip command. This can be seen below.

The first a is a shorthand for the word address, and the second a is a shorthand for the word add:

root@philip-virtual-machine:/home/philip# ip a a 172.50.5.1/24 brd + dev ens33 label ens33:1

Note: This can also be written as: root@philip-virtual-machine:/home/philip# ip address add 172.50.5.1/24 brd + dev ens33 label ens33:1

root@philip-virtual-machine:/home/philip# ip a show ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

link/ether 00:0c:29:32:fc:d5 brd ff:ff:ff:ff:ff:ff

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

inet 172.50.5.1/24 brd 172.50.5.255 scope global ens33:1

valid_lft forever preferred_lft forever

inet6 fe80::d5a6:db57:33f4:7285/64 scope link noprefixroute

valid_lft forever preferred_lft forever

root@philip-virtual-machine:/home/philip#

root@philip-virtual-machine:/home/philip# ifconfig

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.16.170.1 netmask 255.255.255.0 broadcast 172.16.170.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

RX packets 79421 bytes 58846078 (58.8 MB)

RX errors 0 dropped 1 overruns 0 frame 0

TX packets 36124 bytes 3191485 (3.1 MB)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

ens33:1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.50.5.1 netmask 255.255.255.0 broadcast 172.50.5.255

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

root@philip-virtual-machine:/home/philip#

We can see the alias being listed under ens33 with the ip command. However, when we use the ifconfig command, we see the ens33:1 listed as a separate logical interface. Once we are finished using the alias, we can remove the alias by passing the del option with the ip command, as shown below:

root@philip-virtual-machine:/home/philip# ip a del 172.50.5.1/24 brd + dev ens33 label ens33:1

root@philip-virtual-machine:/home/philip# ip a show ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

link/ether 00:0c:29:32:fc:d5 brd ff:ff:ff:ff:ff:ff

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

valid_lft forever preferred_lft forever

inet6 fe80::d5a6:db57:33f4:7285/64 scope link noprefixroute

valid_lft forever preferred_lft forever

root@philip-virtual-machine:/home/philip# ifconfig

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 172.16.170.1 netmask 255.255.255.0 broadcast 172.16.170.255

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

ether 00:0c:29:32:fc:d5 txqueuelen 1000 (Ethernet)

root@philip-virtual-machine:/home/philip#

Some output omitted for brevity. The alias interface has been removed. In environments where the network uses Virtual LANs (VLANs), it is possible to create sub-interfaces that can map to a VLAN, effectively enabling the Linux system to handle tagged VLANs traffic. You would need to configure the network switch to tag the traffic, which will send the traffic inside the VLAN to the Linux system; the link between the Linux system and the switch is then treated as a trunk port because it can send multiple VLANs across its physical link and the Linux system can handle the traffic because it is aware of the VLANs which we create. We would use the ip link with the add option. Here is how we would create a sub-interface and map it to a VLAN:

root@philip-virtual-machine:/home/philip# ip link add link ens33 name ens33.100 type vlan id 100

root@philip-virtual-machine:/home/philip# ip a | grep ens

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

3: ens33.100@ens33: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000

root@philip-virtual-machine:/home/philip#

The interface was created, and it is being treated as a separate interface. We can assign an IPv4 address as we would a physical interface, as shown below:

root@philip-virtual-machine:/home/philip# ip a a 172.16.5.5/24 dev ens33.100

root@philip-virtual-machine:/home/philip# ip a | grep ens

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

3: ens33.100@ens33: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000

inet 172.16.5.5/24 scope global ens33.100

root@philip-virtual-machine:/home/philip#

The last step would be to bring up the interface. We would pass the up option to the ip link command as shown below:

root@philip-virtual-machine:/home/philip# ip link set dev ens33.100 up

root@philip-virtual-machine:/home/philip# ip a | grep ens

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

3: ens33.100@ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000

inet 172.16.5.5/24 scope global ens33.100

root@philip-virtual-machine:/home/philip#

The sub-interface, which maps to VLAN 100, is now up. We can add and remove IP addressing information like a physical interface. When we are finished working with the sub-interface, we can remove it by passing the del option to the ip link command, as shown below:

root@philip-virtual-machine:/home/philip# ip link del ens33.100

root@philip-virtual-machine:/home/philip# ip a | grep ens

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

inet 172.16.170.1/24 brd 172.16.170.255 scope global noprefixroute ens33

inet 172.16.30.1/24 brd 172.16.30.255 scope global noprefixroute ens33

root@philip-virtual-machine:/home/philip#

The sub-interface is no longer present. Another useful purpose of the ip command is the ability to view the statistics of an interface. We would pass the -s and the ls option with the ip link command as shown below:

root@philip-virtual-machine:/home/philip# ip -s link ls ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

link/ether 00:0c:29:32:fc:d5 brd ff:ff:ff:ff:ff:ff

RX: bytes packets errors dropped overrun mcast

58851742 79482 0 1 0 0

TX: bytes packets errors dropped carrier collsns

3199078 36174 0 0 0 0

root@philip-virtual-machine:/home/philip#

The statistics regarding packets received and transmitted; we can even see the frame, missed, CRC errors by adding another -s option. This section -s adds more detailed statistics to the current command, as shown below:

root@philip-virtual-machine:/home/philip# ip -s -s link ls ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

link/ether 00:0c:29:32:fc:d5 brd ff:ff:ff:ff:ff:ff

RX: bytes packets errors dropped overrun mcast

58852018 79485 0 1 0 0

RX errors: length crc frame fifo missed

0 0 0 0 0

TX: bytes packets errors dropped carrier collsns

3199078 36174 0 0 0 0

TX errors: aborted fifo window heartbeat transns

0 0 0 0 20

root@philip-virtual-machine:/home/philip#

We see counters pertaining to CRC, frames, etc.

[Configure IPv4 routing](#contents.xhtml_sc65a)

So far, we have been assigning IPv4 addressing information, but we have not specified any type of routing information. We can view the current routing table by using a few commands. For instance, we can use the route command to display the routing table as shown below:

root@philip-virtual-machine:/home/philip# route

Kernel IP routing table

Destination Gateway Genmask Flags Metric Ref Use Iface

link-local 0.0.0.0 255.255.0.0 U 1000 0 0 ens33

172.16.30.0 0.0.0.0 255.255.255.0 U 100 0 0 ens33

172.16.170.0 0.0.0.0 255.255.255.0 U 100 0 0 ens33

root@philip-virtual-machine:/home/philip#

Only connected routes which map to the configured IPv4 addresses are displayed. It is also possible to display the routing table using the ip command; we would pass the route option as shown below:

root@philip-virtual-machine:/home/philip# ip route

169.254.0.0/16 dev ens33 scope link metric 1000

172.16.30.0/24 dev ens33 proto kernel scope link src 172.16.30.1 metric 100

172.16.170.0/24 dev ens33 proto kernel scope link src 172.16.170.1 metric 100

root@philip-virtual-machine:/home/philip#

We see similar information to that of route command. Another command which can be used to print the routing table is the netstat command; we would pass the -r option as shown below:

root@philip-virtual-machine:/home/philip# netstat -r

Kernel IP routing table

Destination Gateway Genmask Flags MSS Window irtt Iface

link-local 0.0.0.0 255.255.0.0 U 0 0 0 ens33

172.16.30.0 0.0.0.0 255.255.255.0 U 0 0 0 ens33

172.16.170.0 0.0.0.0 255.255.255.0 U 0 0 0 ens33

root@philip-virtual-machine:/home/philip#

The routing table is printed once again. We have not configured a default route; a default route is used for reaching hosts not on the same subnet or residing outside the LAN. We will use the ip route command with the add and default options to define a default route. Here is how this would look below:

root@philip-virtual-machine:/home/philip# ip route add default via 172.16.175.1

root@philip-virtual-machine:/home/philip# ip route | grep def

default via 172.16.175.1 dev ens33

root@philip-virtual-machine:/home/philip#

root@philip-virtual-machine:/home/philip# route | grep UG

default _gateway 0.0.0.0 UG 0 0 0 ens33

root@philip-virtual-machine:/home/philip#

We can see that a default route has been added. When we ran the route command, we saw the word _gateway instead of the IPv4 address; we can pass the -n option to view the numerical value of the default gateway as shown below:

root@philip-virtual-machine:/home/philip# route -n | grep UG

0.0.0.0 172.16.175.1 0.0.0.0 UG 0 0 0 ens33

root@philip-virtual-machine:/home/philip#

We can also create a static route by specifying the subnet we are trying to reach. Here is how we would accomplish this:

root@philip-virtual-machine:/home/philip# ip route add 10.20.0.0/24 via 172.16.30.1

root@philip-virtual-machine:/home/philip# ip route | grep via

default via 172.16.175.1 dev ens33

10.20.0.0/24 via 172.16.30.1 dev ens33

root@philip-virtual-machine:/home/philip#

root@philip-virtual-machine:/home/philip# route -n | grep UG

0.0.0.0 172.16.175.1 0.0.0.0 UG 0 0 0 ens33

10.20.0.0 172.16.30.1 255.255.255.0 UG 0 0 0 ens33

root@philip-virtual-machine:/home/philip#

We now see the static route added for the 10.20.0.0/24 subnet via 172.16.30.1. When we no longer desire a route, we can remove it using the ip route command with the del option as shown below:

root@philip-virtual-machine:/home/philip# ip route del 10.20.0.0/24 via 172.16.30.1

root@philip-virtual-machine:/home/philip# ip route | grep via

default via 172.16.175.1 dev ens33

root@philip-virtual-machine:/home/philip# route -n | grep UG

0.0.0.0 172.16.175.1 0.0.0.0 UG 0 0 0 ens33

root@philip-virtual-machine:/home/philip#

Based on the above, the static route for 10.20.0.0/24 is no longer in our routing table.

[IPv6 configuration](#contents.xhtml_sc66a)

We can configure IPv6 addressing information like those used for IPv4\. To only view IPv6 addresses, we can use the ip command and pass -6 option as shown below:

root@philip-virtual-machine:/home/philip# ip -6 a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 state UNKNOWN qlen 1000

inet6 ::1/128 scope host

valid_lft forever preferred_lft forever

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP qlen 1000

inet6 fe80::d5a6:db57:33f4:7285/64 scope link noprefixroute

valid_lft forever preferred_lft forever

root@philip-virtual-machine:/home/philip#

Based on the above, we see only IPv6 information, particularly the link-local address which starts with fe80. We can add an IPv6 address using the ip command. Here is how we would add an IPv6 address:

root@philip-virtual-machine:/home/philip# ip -6 a a 2001:0db8:0:f101::1/64 dev ens33

root@philip-virtual-machine:/home/philip# ip -6 a show ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP qlen 1000

inet6 2001:db8:0:f101::1/64 scope global

valid_lft forever preferred_lft forever

inet6 fe80::d5a6:db57:33f4:7285/64 scope link noprefixroute

valid_lft forever preferred_lft forever

root@philip-virtual-machine:/home/philip#

We can see that the IPv6 address was assigned to the ens33 interface. Also, we could use the ifconfig command to display the IPv6 addressing information as shown below:

root@philip-virtual-machine:/home/philip# ifconfig | egrep 'ens|inet6'

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet6 2001:db8:0:f101::1 prefixlen 64 scopeid 0x0<global>

inet6 fe80::d5a6:db57:33f4:7285 prefixlen 64 scopeid 0x20<link>

inet6 ::1 prefixlen 128 scopeid 0x10<host>

root@philip-virtual-machine:/home/philip#

We see the IPv6 information in the inet6 section. It is also possible to configure multiple IPv6 addresses; we would simply use the ip with the -6 command, as shown below:

root@philip-virtual-machine:/home/philip# ip -6 a a 2001:0db8:0:f102::2/64 dev ens33

root@philip-virtual-machine:/home/philip# ip -6 a show ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP qlen 1000

inet6 2001:db8:0:f102::2/64 scope global

valid_lft forever preferred_lft forever

inet6 2001:db8:0:f101::1/64 scope global

valid_lft forever preferred_lft forever

inet6 fe80::d5a6:db57:33f4:7285/64 scope link noprefixroute

valid_lft forever preferred_lft forever

root@philip-virtual-machine:/home/philip#

We can see the second IPv6 address has been added. When we no longer need an IPv6 address, we can pass the del option with the ip command as shown below:

root@philip-virtual-machine:/home/philip# ip -6 a del 2001:0db8:0:f102::2/64 dev ens33

root@philip-virtual-machine:/home/philip# ip -6 a show ens33

2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP qlen 1000

inet6 2001:db8:0:f101::1/64 scope global

valid_lft forever preferred_lft forever

inet6 fe80::d5a6:db57:33f4:7285/64 scope link noprefixroute

valid_lft forever preferred_lft forever

root@philip-virtual-machine:/home/philip#

The IPv6 address was removed, which we specified with the del option.

[Configure IPv6 routing](#contents.xhtml_sc67a)

We have looked at the IPv4 routing table but there is also an IPv6 routing table. We can use the same ip route command with the -6 option as shown below:

root@philip-virtual-machine:/home/philip# ip -6 route

2001:db8:0:f101::/64 dev ens33 proto kernel metric 256 pref medium

fe80::/64 dev ens33 proto kernel metric 100 pref medium

fe80::/64 dev ens33 proto kernel metric 256 pref medium

root@philip-virtual-machine:/home/philip#

Based on the above, only the IPv6 routing information is displayed. There is currently no default gateway configured for IPv6 in this system. We can fix this by using the ip route command and passing the -6 and add option as shown below:

root@philip-virtual-machine:/home/philip# ip -6 route add ::/0 via 2001:db8:0:f101::2

root@philip-virtual-machine:/home/philip# ip -6 route

2001:db8:0:f101::/64 dev ens33 proto kernel metric 256 pref medium

fe80::/64 dev ens33 proto kernel metric 100 pref medium

fe80::/64 dev ens33 proto kernel metric 256 pref medium

default via 2001:db8:0:f101::2 dev ens33 metric 1024 pref medium

root@philip-virtual-machine:/home/philip#

We can see a default route was added for IPv6\. We can also see the IPv6 routing information using the route command; we would pass the -6 option as shown below:

root@philip-virtual-machine:/home/philip# route -6 | grep UG

[::]/0 _gateway UG 1024 1 0 ens33

root@philip-virtual-machine:/home/philip#

root@philip-virtual-machine:/home/philip# route -6 -n | grep UG

::/0 2001:db8:0:f101::2 UG 1024 1 0 ens33

root@philip-virtual-machine:/home/philip#

We see the IPv6 address of the default gateway. Configuring a static route for an IPv6 subnet on a different IPv6 subnet or outside the LAN is also possible. Here is how we would add a static route for an IPv6 subnet, as shown below:

root@philip-virtual-machine:/home/philip# ip -6 route add 2001:db8:2222:1::/64 via 2001:db8:0:f101::2

root@philip-virtual-machine:/home/philip# ip -6 route | grep via

2001:db8:2222:1::/64 via 2001:db8:0:f101::2 dev ens33 metric 1024 pref medium

default via 2001:db8:0:f101::2 dev ens33 metric 1024 pref medium

root@philip-virtual-machine:/home/philip# route -6 | grep UG

2001:db8:2222:1::/64 _gateway UG 1024 1 0 ens33

[::]/0 _gateway UG 1024 1 0 ens33

root@philip-virtual-machine:/home/philip# route -6 -n | grep UG

2001:db8:2222:1::/64 2001:db8:0:f101::2 UG 1024 1 0 ens33

::/0 2001:db8:0:f101::2 UG 1024 1 0 ens33

root@philip-virtual-machine:/home/philip#

We have added a static route for an IPv6 subnet. Similarly, we can remove a static route for an IPv6 subnet by passing the del option with the ip route command, as shown below:

root@philip-virtual-machine:/home/philip# ip -6 route del 2001:db8:2222:1::/64 via 2001:db8:0:f101::2

root@philip-virtual-machine:/home/philip# route -6 -n | grep UG

::/0 2001:db8:0:f101::2 UG 1024 1 0 ens33

root@philip-virtual-machine:/home/philip#

[Client-side DNS](#contents.xhtml_sc68a)

Up to this point, we have been assigning various IPv4 and IPv6 addressing information, but this does not mean we can browse the internet. For that, we will need to configure the DNS information; particularly, we need to tell the Linux system which DNS server to use when attempting to go out to the internet. As we have seen earlier in this chapter, there are various text boxes that we can fill out for IPv4, IPv6, gateway, and DNS information using a GUI utility. Here, we will look at configuring the DNS information at the command prompt, particularly the /etc/resolv.conf file. Here is the content of the /etc/resolv.conf file is shown below:

root@philip-virtual-machine:/home/philip# cat /etc/resolv.conf

# This file is managed by man:systemd-resolved(8). Do not edit.

nameserver 127.0.0.53

root@philip-virtual-machine:/home/philip#

Some output omitted for brevity. As can be seen above, the format for defining DNS server is:

nameserver <DNS IP>

This entry below is what we want to put in:

root@philip-virtual-machine:/home/philip# cat /etc/resolv.conf | grep name

nameserver 8.8.8.8

root@philip-virtual-machine:/home/philip#

We can also create local DNS entries for local name resolution inside the /etc/hosts file. Here is the content of the /etc/hosts file:

root@philip-virtual-machine:/home/philip# cat /etc/hosts

127.0.0.1 localhost

127.0.1.1 philip-virtual-machine

# The following lines are desirable for IPv6 capable hosts

::1 ip6-localhost ip6-loopback

fe00::0 ip6-localnet

ff00::0 ip6-mcastprefix

ff02::1 ip6-allnodes

ff02::2 ip6-allrouters

root@philip-virtual-machine:/home/philip#

[Conclusion](#contents.xhtml_sc69a)

In this chapter, we looked at processes, and then covered services. Next, we switched gears and dealt with IPv6 and IPv6\. Finally, we wrapped this chapter by looking at network configuration.

In the next chapter, we will focus on software management.

[References](#contents.xhtml_sc70a)

*   This site gives useful information about the IP: [https://tools.ietf.org](https://tools.ietf.org)
*   This site gives useful information about subnetting: [https://www.quora.com](https://www.quora.com)
*   This site gives useful information about IPv6: [https://www.ipv6.com](https://www.ipv6.com)
*   This site gives useful information about configuring IPv4 and IPv6: [https://superuser.com](https://superuser.com)
*   This site gives useful information about configuring client-side DNS: [https://unix.stackexchange.com](https://unix.stackexchange.com)
*   This site gives useful information about troubleshooting: [https://www.computernetworkingnotes.com](https://www.computernetworkingnotes.com)
*   This website gives you a lot of useful tips and best practices from users in the Linux community, particularly for the Debian distributions such as Ubuntu: [https://askubuntu.com](https://askubuntu.com)
*   This last link gives you the information in general, you can post your questions there, and other community members will respond: [https://www.linuxquestions.org](https://www.linuxquestions.org)

# [CHAPTER 4Managing Modules and Software](#contents.xhtml_ch04a)

[Introduction](#contents.xhtml_sc71a)

In the previous chapter, we covered processes, services, and network configuration.

In this chapter, our focus will be software management. First, it will cover modules, followed by localization. Next, it will be managing software. Finally, we will wrap this chapter with Rsyslog.

[Structure](#contents.xhtml_sc72a)

In this chapter, we will discuss the following topics:

*   Modules
*   Localization
*   Managing software
*   Rsyslog

[Objectives](#contents.xhtml_sc73a)

This chapter focuses on essential aspects of Linux proficiency. It effectively provides guidance on using Linux modules, configuring localization, managing software installations, updates, and dependencies, and setting up remote logging for centralized system monitoring. These topics are crucial for optimizing your Linux environment and improving your system administration skills.

[Modules](#contents.xhtml_sc74a)

In the world of Linux, the kernel serves as the core component responsible for managing system resources and providing essential functionalities. However, the kernel itself cannot fulfill every requirement of every user. To address this limitation, Linux introduced kernel modules, allowing developers to dynamically extend the kernel’s capabilities. This chapter explores the fundamentals of Linux modules and their benefits and provides examples to demonstrate their usage.

[Understanding Linux modules](#contents.xhtml_sc75a)

Linux modules are pieces of code that can be dynamically loaded and unloaded into the kernel at runtime without recompiling or rebooting the system. Modules allow developers to add or remove functionalities from the kernel without modifying the core source code. They enable the Linux kernel to be modular, flexible, and scalable.

[Module types](#contents.xhtml_sc76a)

Linux modules can be categorized into Loadable Kernel Modules (LKM) and built-in modules. They are as follows:

*   LKMs: These modules are stored as separate files on disk and can be dynamically loaded or unloaded into the kernel. They offer flexibility, allowing users to add or remove functionality on demand.
*   Built-in modules: Built-in modules are compiled directly into the kernel image during the build process. They are loaded automatically at system boot and cannot be unloaded. Built-in modules are suitable for essential functionalities that almost every system requires.

[Module management](#contents.xhtml_sc77a)

Before diving into the examples, let us explore the tools and commands used for managing Linux modules:

*   Viewing modules

When we would like to view the currently loaded modules, we can take advantage of the lsmod command, as shown in [Figure 4.1](#ch04.xhtml_fig4-1):

![](images/Figure_4.1.png)

Figure 4.1: Output of the lsmod command modprobe

The modprobe command is used to handle module loading and unloading. It resolves dependencies and automatically loads any required modules. For example, to load the usb-storage module, use the command:

$ modprobe usb-storage

*   insmod

The insmod command inserts a module into the running kernel manually. Unlike modprobe, insmod does not resolve dependencies automatically. You need to ensure that all dependencies are already loaded. To load a module using insmod, run the following command:

$ insmod module_name.ko

*   rmmod

The rmmod command is used to unload a module from the running kernel. It removes the module and any associated resources. To unload a module, use the command:

$ rmmod module_name

[Localization](#contents.xhtml_sc78a)

Linux is a globally used operating system serving diverse communities around the world. To cater to the needs of users from different regions and cultures, Linux provides localization support. Localization involves adapting the operating system to specific languages, cultural norms, and regional requirements. This chapter explores the concept of Linux localization, its importance, and the tools available for achieving localization.

[Understanding Linux localization](#contents.xhtml_sc79a)

Localization refers to adapting software, such as the Linux operating system, to meet a specific target market or locale’s linguistic, cultural, and functional requirements. It involves translating the user interface, messages, and documentation into different languages, adapting date and time formats, currency symbols, and number formats, and accommodating cultural norms.

[The importance of localization](#contents.xhtml_sc80a)

Localization plays a crucial role in ensuring the usability and accessibility of an operating system for users across the globe. Localizing Linux makes it more user-friendly, allowing non-English speakers to navigate and interact with the system more effectively. It also promotes inclusivity, enabling users to work comfortably in their native language and cultural context.

[Linux localization tools](#contents.xhtml_sc81a)

Linux provides a range of tools and libraries to facilitate the localization process. Let us explore some of the commonly used tools.

[GNU gettext](#contents.xhtml_sc82a)

GNU gettext is a widely used localization framework in Linux. It provides a set of tools and libraries for managing message translations. The core utility, gettext, extracts translatable strings from the source code and generates translation templates (POT files). Translators then use the msgmerge tool to merge translations into the templates. Finally, the msgfmt utility compiles the translated files into machine-readable MO files, which the system uses to display localized messages.

[Localization files and directories](#contents.xhtml_sc83a)

In Linux, localization files are stored in specific directories following a standard structure. The main directories related to localization include:

*   /usr/share/locale: Contains the language-specific directories with translation files.
*   /usr/share/locale-langpack: Contains language packs for additional language support.
*   /usr/share/man/locale: Contains localized manual pages.

[Language environment variables](#contents.xhtml_sc84a)

Linux uses environment variables to determine each user’s language and locale settings. The key environment variables include:

*   LANG: Specifies the default language and locale.
*   LC_MESSAGES: Defines the language for displaying system messages.
*   LC_TIME, LC_NUMERIC, LC_MONETARY, LC_COLLATE, LC_CTYPE, and LC_ALL: Control specific aspects of localization, such as date/time formats, number formats, collation rules, character classification, and override settings.

[Localization configuration example](#contents.xhtml_sc85a)

Let us take a practical example to demonstrate the localization configuration process in Linux.

*   Install language support:

Use the package manager specific to your distribution to install language support packages. For example, in Ubuntu, you can install language packs using the following command:

$ sudo apt-get install language-pack-<language_code>

*   Configure language environment variables:

Open the .bashrc or .bash_profile file in your home directory using a text editor and add the following lines to set the desired language environment variables:

export LANG=<language_code>.<encoding>

export LC_MESSAGES=<language_code>.<encoding>

*   Update language environment variables:

Run the following command to update the environment variables:

$ source ~/.bashrc

[Managing software](#contents.xhtml_sc86a)

Software management in Linux involves installing, updating, and removing software packages on a Linux operating system. Linux distributions typically provide package management systems that handle these tasks, ensuring efficient and reliable software management. Let us explore the key components and processes involved in software management in Linux:

*   Package repository: A package repository is a collection of software packages hosted on a server. It is the source for obtaining software packages to install or update a Linux system. Each Linux distribution typically maintains its official repository, which contains packages the distribution’s developers maintain. There are also third-party repositories that provide additional software packages.
*   Package formats: Linux distributions often software management in Linux involve installing, updating, and removing software packages on a Linux operating system. Linux distributions typically provide package management systems that handle these tasks, ensuring efficient and reliable software management. Let us explore the key components and processes involved in software management in Linux.
*   Package manager: A package manager is a software tool responsible for managing software packages on a Linux system. It uses specific package formats to bundle software and related metadata for easy distribution and installation. Common package formats include package operations as follows:
    *   Installation: To install software, you specify the package name or file to the package manager, fetching the package from a repository or local source. It resolves dependencies (other packages required for proper functioning) and installs all necessary components.
    *   Update/Upgrade: Updating software involves fetching and installing the latest version of installed packages from repositories. Upgrading, on the other hand, typically consists in upgrading the entire operating system to a new major version.
    *   Removal/Uninstallation: Packages can be removed using the package manager, which deletes the software and its associated files from the system. Dependencies that are no longer required may also be removed.
    *   Dependency resolution: Package managers automatically handle dependency resolution, ensuring that all required packages are installed before installing a specific package. This avoids manual tracking of dependencies and simplifies the installation process.
    *   Searching and querying: Package managers provide commands to search for packages by name or keywords and query package information such as version, description, and installation status.
    *   Repository management: Package managers allow managing repositories by adding or removing them from the system. This enables users to access additional software packages from third-party sources.
    *   Package verification: Package managers often verify the integrity of downloaded packages using cryptographic checksums to ensure they have not been tampered with.
    *   System updates: In addition to managing individual software packages, package managers are responsible for updating the entire Linux system. This includes updating the kernel, core system libraries, and other essential components. Regular system updates ensure security patches, bug fixes, and new features are applied to the operating system.
    *   Graphical package managers: Linux distributions provide graphical frontends to package managers, making software management more user-friendly. These tools offer intuitive interfaces to browse available packages, update software, and handle other package operations.

[Debian package management](#contents.xhtml_sc87a)

We begin by looking at the Debian style of package management. First, we start with the dpkg command, looking at the various methods of using the dpkg command. Also, the various options can be passed with the dpkg command. Next, we turn our attention towards the apt-get utility. This is another popular command for installing applications within a Debian environment. We pay close attention to the options which can be passed with the apt-get command. Finally, we focus on aptitude. Like the previous commands, we focus on the syntax for deploying software within a Debian environment. All the utilities discussed in this chapter are commonly used for managing software within a Debian environment.

[The dpkg command](#contents.xhtml_sc88a)

The dpkg utility is a low-level system tool to extract, analyze, unpack, and install or remove packages with a .deb extension. The scripts read by dpkg inside each .deb file are important as they give information to the program regarding the packages’ installation, removal, and configuration. The dpkg utility resides at the base of the package management system in Debian-based distributions. The Debian package dpkg provides the dpkg utility, as well as several other programs necessary for the run-time functioning of the packaging system, namely: dpkg-deb, dpkg-split, dpkg-query, dpkg-statoverride, dpkg-divert, and dpkg-trigger. We can take a glance at the /var/log/dpkg.log file. There are a lot of verbose details about triggers and packages going through varying stages of unpacking and configuration. 

Let us take a look at the /var/log/dpkg.log:

philip@ubuntu:~$ cat /var/log/dpkg.log

2023-07-02 06:43:57 startup archives unpack

2023-07-02 06:44:01 install linux-image-4.4.0-130-generic:amd64 <none> 4.4.0-130.156

2023-07-02 06:44:01 status half-installed linux-image-4.4.0-130-generic:amd64 4.4.0-130.156

2023-07-02 06:44:09 status unpacked linux-image-4.4.0-130-generic:amd64 4.4.0-130.156

2023-07-02 06:44:09 status unpacked linux-image-4.4.0-130-generic:amd64 4.4.0-130.156

2023-07-02 06:44:09 install linux-image-extra-4.4.0-130-generic:amd64 <none> 4.4.0-130.156

2023-07-02 06:44:09 status half-installed linux-image-extra-4.4.0-130-generic:amd64 4.4.0-130.156

2023-07-02 06:44:20 status unpacked linux-image-extra-4.4.0-130-generic:amd64 4.4.0-130.156

2023-07-02 06:44:20 status unpacked linux-image-extra-4.4.0-130-generic:amd64 4.4.0-130.156

2023-07-02 06:44:21 upgrade linux-generic:amd64 4.4.0.128.134 4.4.0.130.136

2023-07-02 06:44:21 status half-configured linux-generic:amd64 4.4.0.128.134

2023-07-02 06:44:21 status unpacked linux-generic:amd64 4.4.0.128.134

2023-07-02 06:44:21 status half-installed linux-generic:amd64 4.4.0.128.134

2023-07-02 06:44:21 status half-installed linux-generic:amd64 4.4.0.128.134

2023-07-02 06:44:21 status unpacked linux-generic:amd64 4.4.0.130.136

2023-07-02 06:44:21 status unpacked linux-generic:amd64 4.4.0.130.136

2023-07-02 06:44:21 upgrade linux-image-generic:amd64 4.4.0.128.134 4.4.0.130.136

2023-07-02 06:44:21 status half-configured linux-image-generic:amd64 4.4.0.128.134

2023-07-02 06:44:21 status unpacked linux-image-generic:amd64 4.4.0.128.134

2023-07-02 06:44:21 status half-installed linux-image-generic:amd64 4.4.0.128.134

From the above output, we learn about various packages the dpkg utility manages. If we want to see a list of packages on this system, we can use the l option:

philip@ubuntu:~$ dpkg -l

Desired=Unknown/Install/Remove/Purge/Hold

| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend

|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)

||/ Name Version Architecture Description

+++-=============================-===================-===================-================================================================

ii a11y-profile-manager-indicato 0.1.10-0ubuntu3 amd64 Accessibility Profile Manager - Unity desktop indicator

ii account-plugin-facebook 0.12+16.04.20160126 all GNOME Control Center account plugin for single signon - facebook

ii account-plugin-flickr 0.12+16.04.20160126 all GNOME Control Center account plugin for single signon - flickr

ii account-plugin-google 0.12+16.04.20160126 all GNOME Control Center account plugin for single signon

ii accountsservice 0.6.40-2ubuntu11.3 amd64 query and manipulate user account information

ii activity-log-manager 0.9.7-0ubuntu23.16\. amd64 blacklist configuration user interface for Zeitgeist

ii adduser 3.113+nmu3ubuntu4 all add and remove users and groups

ii adium-theme-ubuntu 0.3.4-0ubuntu1.1 all Adium message style for Ubuntu

ii app-install-data 15.10 all Ubuntu applications (data files)

ii app-install-data-partner 16.04 all Application Installer (data files for partner applications/repos

ii apparmor 2.10.95-0ubuntu2.9 amd64 user-space parser utility for AppArmor

ii appmenu-qt:amd64 0.2.7+14.04.2014030 amd64 application menu for Qt

ii appmenu-qt5 0.3.0+16.04.2017021 amd64 application menu for Qt5

ii apport 2.20.1-0ubuntu2 all automatically generate crash reports for debugging

ii apport-gtk 2.20.1-0ubuntu2 all GTK+ frontend for the apport crash report system

Some output omitted for brevity. From the above output, we read the output from left to right. We should focus our attention on the far right of the output. This is the description section; the packages are presented in a human-readable summary for each currently installed on this system.

We can also narrow down our output by filtering the dpkg command; let us just look for the xterm program:

philip@ubuntu:~$ dpkg -l xterm

Desired=Unknown/Install/Remove/Purge/Hold

| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend

|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)

||/ Name Version Architecture Description

+++-=============================-===================-===================-================================================================

ii xterm 322-1ubuntu1 amd64 X terminal emulator

philip@ubuntu:~$

We can verify whether a package is installed or not with the "--get-selections":

philip@ubuntu:~$ dpkg --get-selections

a11y-profile-manager-indicator install

account-plugin-facebook install

account-plugin-flickr install

account-plugin-google install

accountsservice install

acl install

acpi-support install

acpid install

activity-log-manager install

adduser install

adium-theme-ubuntu install

adwaita-icon-theme install

aisleriot install

alsa-base install

alsa-utils install

amd64-microcode install

anacron install

apg install

app-install-data install

app-install-data-partner install

apparmor install

appmenu-qt:amd64 install

appmenu-qt5 install

apport install

Some output omitted for brevity.

We can view files owned by a package by using the L option. Let us continue with our example:

philip@ubuntu:~$ dpkg -L xterm

/.

/etc

/etc/X11

/etc/X11/app-defaults

/etc/X11/app-defaults/UXTerm-color

/etc/X11/app-defaults/UXTerm

/etc/X11/app-defaults/KOI8RXTerm-color

/etc/X11/app-defaults/KOI8RXTerm

/etc/X11/app-defaults/XTerm-color

/usr/share/man/man1/koi8rxterm.1.gz

/usr/share/man/man1/resize.1.gz

/usr/share/man/man1/xterm.1.gz

/usr/share/man/man1/lxterm.1.gz

philip@ubuntu:~$

Some output was omitted for brevity. We can search for a particular package in this system by using the s option:

philip@ubuntu:~$ dpkg -s apache

dpkg-query: package 'apache' is not installed and no information is available

Use dpkg --info (= dpkg-deb --info) to examine archive files,

and dpkg --contents (= dpkg-deb --contents) to list their contents.

philip@ubuntu:~$ dpkg --info apache

dpkg-deb: error: failed to read archive 'apache': No such file or directory

philip@ubuntu:~$

In this case, apache is not installed by default on this system.

We will download a tftp client for this demonstration. Let us verify that tftp client is not installed on this system:

philip@ubuntu:~/Downloads$ dpkg -l tftp

dpkg-query: no packages found matching tftp

philip@ubuntu:~/Downloads$

Now we will install a package using the dpkg command. Let us try to install the tftp client package using the i option:

philip@ubuntu:~/Downloads$ dpkg -i tftp_0.178_i386.deb

dpkg: error: requested operation requires superuser privilege

philip@ubuntu:~/Downloads$

We would need root privileges from the above output to install and remove a package. Let us retry as root:

root@ubuntu:/home/philip/Downloads# ls -l | grep tftp

-rw-rw-r-- 1 philip philip 17208 Jul 18 08:15 tftp_0.17-18_i386.deb

root@ubuntu:/home/philip/Downloads#

root@ubuntu:/home/philip/Downloads# dpkg -i tftp_0.17-18_i386.deb

Selecting previously unselected package tftp:i386.

(Reading database ... 241431 files and directories currently installed.)

Preparing to unpack tftp_0.17-18_i386.deb ...

Unpacking tftp:i386 (0.17-18) ...

Setting up tftp:i386 (0.17-18) ...

Processing triggers for man-db (2.7.5-1) ...

root@ubuntu:/home/philip/Downloads#

Now, let us retry the dpkg command with the l option:

root@ubuntu:/home/philip/Downloads# dpkg -l tftp

Desired=Unknown/Install/Remove/Purge/Hold

| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend

|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)

||/ Name Version Architecture Description

+++-=============================-===================-===================-================================================================

ii tftp:i386 0.17-18 i386 Trivial file transfer protocol client

root@ubuntu:/home/philip/Downloads#

We can now see tftp client listed. We can also run the dpkg with the —get-selections to verify the same:

root@ubuntu:/home/philip/Downloads# dpkg --get-selections | grep tftp

tftp:i386 install

root@ubuntu:/home/philip/Downloads#

| Note: | When use “dpkg” to install a package, sometime(s) you may run in to dependency issue(s). The work around is to download and install each dependency before you install your package using “dpkg”. |

We can also remove a package using the dpkg command. Let us remove the tftp package we installed in the previous demo. We will use the -r option:

root@ubuntu:/home/philip/Downloads# dpkg -r tftp

(Reading database ... 241438 files and directories currently installed.)

Removing tftp:i386 (0.17-18) ...

Processing triggers for man-db (2.7.5-1) ...

root@ubuntu:/home/philip/Downloads#

Now, let's verify that the tftp package has indeed been uninstalled:

root@ubuntu:/home/philip/Downloads# dpkg -l tftp

dpkg-query: no packages found matching tftp

root@ubuntu:/home/philip/Downloads#

However, using the -r option does not remove the configuration file(s). We would use the -P (purge) option to remove the package along with the configuration files. Here is how that would work:

root@ubuntu:/home/philip/Downloads# dpkg -P tftp

(Reading database ... 241438 files and directories currently installed.)

Removing tftp:i386 (0.17-18) ...

Processing triggers for man-db (2.7.5-1) ...

root@ubuntu:/home/philip/Downloads#

We can also extract the content of a package without installing it. We would use the -x option:

root@ubuntu:/home/philip/Downloads# dpkg -x tftp_0.17-18_i386.deb ./tftp_0.17-18_i386

root@ubuntu:/home/philip/Downloads# ls

root@ubuntu:/home/philip/Downloads# ls tftp_0.17-18_i386

usr

root@ubuntu:/home/philip/Downloads# ls tftp_0.17-18_i386/usr/

bin share

root@ubuntu:/home/philip/Downloads#

root@ubuntu:/home/philip/Downloads# ls tftp_0.17-18_i386/usr/bin/

tftp

root@ubuntu:/home/philip/Downloads# ls tftp_0.17-18_i386/usr/share/

doc/ man/

root@ubuntu:/home/philip/Downloads# ls tftp_0.17-18_i386/usr/share/

doc man

root@ubuntu:/home/philip/Downloads#

Before we download any package(s) and install using the dpkg utility, we would need to know correct hardware architecture of the system. Fortunately, we can use the dpkg-architecture command:

root@ubuntu:/home/philip/Downloads# dpkg-architecture

DEB_BUILD_ARCH=amd64

DEB_BUILD_ARCH_BITS=64

DEB_BUILD_ARCH_CPU=amd64

DEB_BUILD_ARCH_ENDIAN=little

DEB_BUILD_ARCH_OS=linux

DEB_BUILD_GNU_CPU=x86_64

DEB_BUILD_GNU_SYSTEM=linux-gnu

DEB_BUILD_GNU_TYPE=x86_64-linux-gnu

DEB_TARGET_ARCH_CPU=amd64

DEB_TARGET_ARCH_ENDIAN=little

DEB_TARGET_ARCH_OS=linux

DEB_TARGET_GNU_CPU=x86_64

DEB_TARGET_GNU_SYSTEM=linux-gnu

DEB_TARGET_GNU_TYPE=x86_64-linux-gnu

DEB_TARGET_MULTIARCH=x86_64-linux-gnu

root@ubuntu:/home/philip/Downloads#

Some output omitted for brevity. Based on the above output, this system supports 32- or 64bit package(s). We can also garner useful information regarding the purpose of a package. We would use the dpkg-query command with the -s option:

root@ubuntu:/home/philip/Downloads# dpkg-query -s tftp

Package: tftp

Status: install ok unpacked

Priority: optional

Section: net

Installed-Size: 80

Maintainer: Alberto Gonzalez Iniesta <agi@inittab.org>

Architecture: i386

Source: netkit-tftp

Version: 0.17-18

Config-Version: 0.17-18

Replaces: netstd

Depends: netbase, libc6 (>= 2.3)

Description: Trivial file transfer protocol client

Tftp is the user interface to the Internet TFTP (Trivial File Transfer

Protocol), which allows users to transfer files to and from a remote machine.

The remote host may be specified on the command line, in which case tftp uses

host as the default host for future transfers.

root@ubuntu:/home/philip/Downloads#

From the above output, we are described at the bottom regarding using the tftp package.

[The apt-get command](#contents.xhtml_sc89a)

Advanced Package Tool (APT) is a command line tool used for easy interaction with the dpkg packaging system. APT is the ideal method for managing software Debian based Linux distributions such as Ubuntu. It manages dependencies effectively, maintains large configuration files, and properly handles upgrades and downgrades to ensure system stability. The dpkg on its own does not handle dependencies properly. The apt-get performs installations, package searches, updates, and many other operations for packages available to your system. Keeping packages up to date is extremely important, as using out-of-date packages can lead to security issues on your system. The apt-get utility requires root privileges, like the dpkg utility.

First, before we make perform any software installation, it is always best practice to update the package database. We would run apt-get update:

root@ubuntu:/home/philip/Downloads# apt-get update

Get:1 http://security.ubuntu.com/ubuntu xenial-security InRelease [107 kB]

Hit:2 http://us.archive.ubuntu.com/ubuntu xenial InRelease

Get:3 http://security.debian.org/debian-security wheezy/updates InRelease [54.0 kB]

Get:4 http://us.archive.ubuntu.com/ubuntu xenial-updates InRelease [109 kB]

Ign:3 http://security.debian.org/debian-security wheezy/updates InRelease

Get:5 http://us.archive.ubuntu.com/ubuntu xenial-backports InRelease [107 kB]

Get:6 http://security.debian.org/debian-security wheezy/updates/main amd64 Packages [589 kB]

Get:21 http://us.archive.ubuntu.com/ubuntu xenial-updates/multiverse amd64 DEP-11 Metadata [5,964 B]

Get:22 http://us.archive.ubuntu.com/ubuntu xenial-backports/main amd64 DEP-11 Metadata [3,328 B]

Get:23 http://us.archive.ubuntu.com/ubuntu xenial-backports/universe amd64 DEP-11 Metadata [5,096 B]

Fetched 6,189 kB in 6s (1,031 kB/s)

Reading package lists... Done

root@ubuntu:/home/philip/Downloads#

Some output was omitted for brevity. Based on the above output, the first section will be: Hit, Get, Ign. The lines which start with Hit indicate that there is no change in the package version. The Get means that there is a new version available. The Ign implies that the package is being ignored; there are various reasons why you see an Ign, ranging from a package being too recent to an error in retrieving the file. Usually, the error(s) are harmless.

Before installing an application, we can search for it using the apt-cache command. Let us say that we want to install a messenger application, well we can do this:

root@ubuntu:/home/philip/Downloads# apt-cache search messenger

adium-theme-ubuntu - Adium message style for Ubuntu

totem-plugins - Plugins for the Totem media player

ayttm - Universal instant messaging client

banshee-extension-telepathy - Telepathy extension for Banshee

droopy - mini web server to let others upload files to your computer

dsniff - Various tools to sniff network traffic for cleartext insecurities

ekg2 - instant messenger and IRC client for UNIX systems

ekg2-api-docs - instant messenger and IRC client for UNIX systems - API documentation

ekg2-core - instant messenger and IRC client for UNIX systems - main program

yate-qt4 - YATE-based universal telephony client

yowsup-cli - command line tool that acts as WhatsApp client

empathy-skype - Skype plugin for libpurple messengers (Empathy-specific files)

pidgin-skype - Skype plugin for libpurple messengers (Pidgin-specific files)

pidgin-skype-common - Skype plugin for libpurple messengers (common files)

pidgin-skype-dbg - Skype plugin for libpurple messengers (debug symbols)

root@ubuntu:/home/philip/Downloads#

Some output was omitted for brevity. Based on the above output, we can see a wide range of messenger packages are available to be installed. If, for some reason we want to see all the available packages, we can use the pkgnames option:

root@ubuntu:/home/philip/Downloads# apt-cache pkgnames | less

libdatrie-doc

libfstrcmp0-dbg

librime-data-sampheng

xxdiff-scripts

globus-xioperf

edenmath.app

libghc-ansi-wl-pprint-doc

libjson0

zathura-cb

root@ubuntu:/home/philip/Downloads#

Some output was omitted for brevity. We can see a variety of packages that we can install onto this system. We can see a brief description of a package by specifying the correct package name:

root@ubuntu:/home/philip/Downloads# apt-cache search zathura-cb

zathura-cb - comic book archive support for zathura

root@ubuntu:/home/philip/Downloads# apt-cache search virtaal

virtaal - graphical localisation editor

root@ubuntu:/home/philip/Downloads# apt-cache search python-logbook

python-logbook - logging system for Python that replaces the standard library's module

python-logbook-doc - logging system for Python that replaces the standard library's module (doc)

root@ubuntu:/home/philip/Downloads#

Based on the above output, we can see the descriptions for various packages which we passed with the search option. We can also check the details of a package by using the show option:

root@ubuntu:/home/philip/Downloads# apt-cache show python-logbook

Package: python-logbook

Priority: optional

Section: universe/python

Source: logbook

Version: 0.12.3-1

Depends: python:any (<< 2.8), python:any (>= 2.7.5-5~)

Suggests: python-logbook-doc

Filename: pool/universe/l/logbook/python-logbook_0.12.3-1_all.deb

Size: 47896

MD5sum: 865ee97095b97f74e362ce3d93a26a9e

SHA1: 812b08f4e4e4dbcd40264a99fa4cd4dff4f62961

SHA256: 3091d5c491e54007da8b510a6f2e463b63f62364938c4f371406cb4511b6232c

Origin: Ubuntu

root@ubuntu:/home/philip/Downloads#

Some output omitted for brevity. We can even filter this information to only look for dependencies. We would use the showpkg option:

root@ubuntu:/home/philip/Downloads# apt-cache showpkg python-logbook

Package: python-logbook

Versions:

0.12.3-1 (/var/lib/apt/lists/us.archive.ubuntu.com_ubuntu_dists_xenial_universe_binary-amd64_Packages) (/var/lib/apt/lists/us.archive.ubuntu.com_ubuntu_dists_xenial_universe_binary-i386_Packages)

Dependencies:

0.12.3-1 - python:any (3 2.8) python:any (2 2.7.5-5~) python-logbook-doc (0 (null))

Provides:

0.12.3-1 -

Reverse Provides:

root@ubuntu:/home/philip/Downloads#

We can also view the statistics for the cache on this system. We would use the stats option:

root@ubuntu:/home/philip/Downloads# apt-cache stats

Total package names: 73419 (1,468 k)

Total package structures: 113356 (4,988 k)

Normal packages: 84328

Total buckets in PkgHashTable: 50503

Unused: 11792

Used: 38711

Utilization: 76.6509%

Average entries: 2.92826

Longest: 15

Shortest: 1

Total buckets in GrpHashTable: 50503

Unused: 11792

Used: 38711

Utilization: 76.6509%

Average entries: 1.89659

Longest: 8

Shortest: 1

root@ubuntu:/home/philip/Downloads#

Some output was omitted for brevity.

Now, we can download a package without installing it. We would use the download option with apt-get:

root@ubuntu:/tmp# apt-get download zathura-cb

Get:1 http://us.archive.ubuntu.com/ubuntu xenial/universe amd64 zathura-cb amd64 0.1.5-1 [8,812 B]

Fetched 8,812 B in 0s (40.0 kB/s)

root@ubuntu:/tmp# ls | grep zathura

zathura-cb_0.1.5-1_amd64.deb

root@ubuntu:/tmp#

We can install a package that has been downloaded. We would specify the path with the apt-get command:

root@ubuntu:/tmp# apt-get install ./zathura-cb_0.1.5-1_amd64.deb

Reading package lists... Done

Building dependency tree

Reading state information... Done

You might want to run 'apt-get -f install' to correct these.

The following packages have unmet dependencies:

openssh-server:i386 : Depends: openssh-client:i386 (= 1:6.0p1-4+deb7u7)

Recommends: ncurses-term:i386

Recommends: openssh-blacklist:i386 but it is not installable

Recommends: openssh-blacklist-extra:i386 but it is not installable

openssh-sftp-server:i386 : Breaks: openssh-server (< 1:6.5p1-5)

Breaks: openssh-server:i386 (< 1:6.5p1-5)

E: Unmet dependencies. Try using -f.

root@ubuntu:/tmp#

Now, sometimes you may run into the problem above. The easiest way to fix this would be to rerun the apt-get command with the -f option leaving out the package name:

root@ubuntu:/tmp# apt-get -f install

Reading package lists... Done

Building dependency tree

Reading state information... Done

Correcting dependencies... Done

The following packages were automatically installed and are no longer required:

Do you want to continue? [Y/n] y

Preconfiguring packages ...

(Reading database ... 241439 files and directories currently installed.)

Preparing to unpack .../openssh-server_1%3a7.2p2-4ubuntu2.4_i386.deb ...

Unpacking openssh-server:i386 (1:7.2p2-4ubuntu2.4) over (1:6.0p1-4+deb7u7) ...

Processing triggers for ufw (0.35-0ubuntu2) ...

Processing triggers for systemd (229-4ubuntu21.2) ...

Processing triggers for ureadahead (0.100.0-19) ...

Processing triggers for man-db (2.7.5-1) ...

Setting up openssh-server:i386 (1:7.2p2-4ubuntu2.4) ...

Setting up tftp:i386 (0.17-18) ...

root@ubuntu:/tmp#

Some output was omitted for brevity.

As we can see, the installation was successful. This is what is so great about the apt-get utility. The fact is that it finds the dependencies that are needed and offers to install them to fix the problem being reported. We can also install multiple applications simultaneously. We would simply place each package name on the same line separated by a space:

root@ubuntu:/tmp# apt-get install virtaal vsftpd

Reading package lists... Done

Building dependency tree

Reading state information... Done

The following packages were automatically installed and are no longer required:

libllvm3.8 libpango1.0-0 libpangox-1.0-0 libqmi-glib1 linux-headers-4.4.0-21 linux-headers-4.4.0-21-generic linux-image-4.4.0-21-generic

linux-image-extra-4.4.0-21-generic

Use 'sudo apt autoremove' to remove them.

The following additional packages will be installed:

javascript-common libglade2-0 libjs-jquery libjs-sph

Do you want to continue? [Y/n] y

Get:1 http://us.archive.ubuntu.com/ubuntu xenial/main amd64 libglade2-0 amd64 1:2.6.4-2 [44.6 kB]

Get:2 http://us.archive.ubuntu.com/ubuntu xenial/main amd64 javascript-common all 11 [6,066 B]

Get:3 http://us.archive.ubuntu.com/ubuntu xenial/main amd64 libjs-jquery all 1.11.3+dfsg-4 [161 kB]

Get:4 http://us.archive.ubuntu.com/ubuntu xenial/main amd64 libjs-underscore all 1.7.0~dfsg-1ubuntu1 [46.7 kB]

Get:5 http://us.archive.ubuntu.com/ubuntu xenial-updates/main amd64 libjs-sphinxdoc all 1.3.6-2ubuntu1.1 [57.6 kB]

Get:6 http://us.archive.ubuntu.com/ubuntu xenial-updates/main amd64 libpq5 amd64 9.5.13-0ubuntu0.16.04 [78.7 kB]

Setting up virtaal (0.7.1-1) ...

Setting up python-iniparse (0.4-2.2) ...

Setting up vsftpd (3.0.3-3ubuntu2) ...

Processing triggers for libc-bin (2.23-0ubuntu10) ...

Processing triggers for systemd (229-4ubuntu21.2) ...

Processing triggers for ureadahead (0.100.0-19) ...

root@ubuntu:/tmp#

So, you can see the power of the apt-get utility in action. We can also upgrade all the packages that are currently installed. We would use the upgrade option:

root@ubuntu:/tmp# apt-get upgrade

Reading package lists... Done

Building dependency tree

Reading state information... Done

Calculating upgrade... Done

The following packages were automatically installed and are no longer required:

libllvm3.8 libpango1.0-0 libpangox-1.0-0 libqmi-glib1 linux-headers-4.4.0-21 linux-headers-4.4.0-21-generic linux-image-4.4.0-21-generic

linux-image-extra-4.4.0-21-generic

Use 'sudo apt autoremove' to remove them.

The following packages have been kept back:

libegl1-mesa libgbm1 libgl1-mesa-dri libwayland-egl1-mesa libxatracker2

The following packages will be upgraded:

apt apt-transport-https apt-utils base-files cups cups-bsd cups-client cups-common cups-core-drivers cups-daemon cups-ppdc

63 upgraded, 0 newly installed, 0 to remove and 5 not upgraded.

Need to get 67.1 MB/160 MB of archives.

After this operation, 1,333 kB disk space will be freed.

Do you want to continue? [Y/n] y

root@ubuntu:/tmp#

Some output was omitted for brevity.

We can also remove some previously used packages to ensure a particular package(s) was installed correctly. In our case, should we rerun the upgrade option, we would see this:

root@ubuntu:/tmp# apt-get upgrade

Reading package lists... Done

Building dependency tree

Reading state information... Done

Calculating upgrade... Done

The following packages were automatically installed and are no longer required:

libllvm3.8 libpango1.0-0 libpangox-1.0-0 libqmi-glib1 linux-headers-4.4.0-21 linux-headers-4.4.0-21-generic linux-image-4.4.0-21-generic

linux-image-extra-4.4.0-21-generic

Use 'sudo apt autoremove' to remove them.

The following packages have been kept back:

libegl1-mesa libgbm1 libgl1-mesa-dri libwayland-egl1-mesa libxatracker2

0 upgraded, 0 newly installed, 0 to remove and 5 not upgraded.

root@ubuntu:/tmp#

We would use the "autoremove" option as suggested to free up some disk space:

root@ubuntu:/tmp# apt-get autoremove

Reading package lists... Done

Building dependency tree

Reading state information... Done

The following packages will be REMOVED:

libllvm3.8 libpango1.0-0 libpangox-1.0-0 libqmi-glib1 linux-headers-4.4.0-21 linux-headers-4.4.0-21-generic linux-image-4.4.0-21-generic

linux-image-extra-4.4.0-21-generic

0 upgraded, 0 newly installed, 8 to remove and 5 not upgraded.

After this operation, 339 MB disk space will be freed.

Do you want to continue? [Y/n] y

(Reading database ... 244059 files and directories currently installed.)

Removing libllvm3.8:amd64 (1:3.8-2ubuntu4) ...

Removing libpango1.0-0:amd64 (1.38.1-1) ...

Removing libpangox-1.0-0:amd64 (0.0.2-5) ...

done

Processing triggers for libc-bin (2.23-0ubuntu10) ...

root@ubuntu:/tmp#

Some output omitted for brevity. We can also free up disk space by using the "clean" option:

root@ubuntu:/tmp# apt-get clean

root@ubuntu:/tmp#

As we can see, the command ran very quickly.

Note: It is always best practice to clean up disk space regularly.

We can also remove an application using the remove option. This would remove the application but not the configuration:

root@ubuntu:/tmp# apt-get remove virtaal

Reading package lists... Done

Building dependency tree

Reading state information... Done

The following packages were automatically installed and are no longer required:

javascript-common libglade2-0 libjs-jquery libjs-sphinxdoc libjs-underscore libpq5 libtidy-0.99-0 python-babel python-babel-localedata

python-bs4 python-cairo python-chardet python-dateutil python-diff-match-patch python-egenix-mxdatetime python-egenix-mxtools

python-enchant python-gi python-glade2 python-gobject python-gobject-2 python-gtk2 python-html5lib python-iniparse python-levenshtein

python-lxml python-pkg-resources python-psycopg2 python-pycurl python-simplejson python-six python-tz python-utidylib python-vobject

python-xapian translate-toolkit

Use 'sudo apt autoremove' to remove them.

The following packages will be REMOVED:

virtaal

0 upgraded, 0 newly installed, 1 to remove and 5 not upgraded.

After this operation, 3,496 kB disk space will be freed.

Do you want to continue? [Y/n] y

root@ubuntu:/tmp#

We would then run the "autoremove" option to clean up unneeded packages:

root@ubuntu:/tmp# apt-get autoremove virtaal

Reading package lists... Done

Building dependency tree

Reading state information... Done

Package 'virtaal' is not installed, so not removed

The following packages will be REMOVED:

javascript-common libglade2-0 libjs-jquery libjs-sphinxdoc libjs-underscore libpq5 libtidy-0.99-0 python-babel python-babel-localedata

python-bs4 python-cairo python-chardet python-dateutil python-diff-match-patch python-egenix-mxdatetime python-egenix-mxtools

python-enchant python-gi python-glade2 python-gobject python-gobject-2 python-gtk2 python-html5lib python-iniparse python-levenshtein

python-lxml python-pkg-resources python-psycopg2 python-pycurl python-simplejson python-six python-tz python-utidylib python-vobject

python-xapian translate-toolkit

0 upgraded, 0 newly installed, 36 to remove and 5 not upgraded.

After this operation, 34.6 MB disk space will be freed.

Do you want to continue? [Y/n] y

Processing triggers for libc-bin (2.23-0ubuntu10) ...

Processing triggers for man-db (2.7.5-1) ...

Processing triggers for doc-base (0.10.7) ...

Processing 4 removed doc-base files...

root@ubuntu:/tmp#

Awesome! We can remove the package and its configuration by using the "purge" option:

root@ubuntu:/tmp# apt-get purge virtaal

Reading package lists... Done

Building dependency tree

Reading state information... Done

The following packages will be REMOVED:

virtaal*

0 upgraded, 0 newly installed, 1 to remove and 5 not upgraded.

After this operation, 0 B of additional disk space will be used.

Do you want to continue? [Y/n] y

Removing virtaal (0.7.1-1) ...

Purging configuration files for virtaal (0.7.1-1) ...

root@ubuntu:/tmp#

| Note: | Always a good idea to run the “apt-get” command with the “clean” option regularly. |

Whenever we install a package(s) using the apt utility, it uses repositories to download the packages into the cache. By default, when we install a Debian distribution, the installation comes with official repositories. These are stored in the /etc/apt/sources.list file. We can take a look at that file:

root@ubuntu:/tmp# cat /etc/apt/sources.list

#deb cdrom:[Ubuntu 16.04 LTS _Xenial Xerus_ - Release amd64 (20160420.1)]/ xenial main restricted

# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to

# newer versions of the distribution.

deb http://us.archive.ubuntu.com/ubuntu/ xenial main restricted

# deb-src http://us.archive.ubuntu.com/ubuntu/ xenial main restricted

## Major bug fix updates produced after the final release of the

## distribution.

deb http://us.archive.ubuntu.com/ubuntu/ xenial-updates main restricted

# deb-src http://us.archive.ubuntu.com/ubuntu/ xenial-updates main restricted

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu

## team, and may not be under a free licence. Please satisfy yourself as to

## your rights to use the software. Also, please note that software in

## universe WILL NOT receive any review or updates from the Ubuntu security

## team.

deb http://us.archive.ubuntu.com/ubuntu/ xenial universe

# deb-src http://us.archive.ubuntu.com/ubuntu/ xenial universe

# deb-src http://security.ubuntu.com/ubuntu xenial-security universe

deb http://security.ubuntu.com/ubuntu xenial-security multiverse

# deb-src http://security.ubuntu.com/ubuntu xenial-security multiverse

root@ubuntu:/tmp#

Some output omitted for brevity. The entries that start with deb refer to where to search for packages. The entries that start with deb-src refer to source packages.

[The aptitude command](#contents.xhtml_sc90a)

Aptitude is a front-end to Apt which is the Debian package manager. It is best suited in shell environments where a GUI is not present. The aptitude command allows users to view the list of packages and perform package management tasks such as installing, removing, or upgrading packages. There is an interactive mode; also, it could be used as a command-line tool, similar to apt-get.

We can see this in action by simply entering the aptitude command without passing any option(s), refer to [Figure 4.2](#ch04.xhtml_fig4-2):

![aptitude1.png](images/Figure_4._2_.png)

Figure 4.2: The aptitude utility

From the above output, we can navigate by using our keyboard or mouse. At the top, there is a menu, and we can select Actions from the menu and see the available options. Refer to [Figure 4.3](#ch04.xhtml_fig4-3):

![aptitude2.png](images/Figure_4._3_.jpg)

Figure 4.3: Available options under the actions menu

We can also go directly to the Package from the menu and see options similar to package management from the command line. Refer to [Figure 4.4](#ch04.xhtml_fig4-4):

![aptitude3.png](images/Figure_4._4_.png)

Figure 4.4: Available options under the package menu

As we can see, aptitude is very intuitive when we use this method for package management.

We can also manage package(s) using the command line. This will require us to pass options with the aptitude command if we prefer typing commands over a menu environment. The aptitude command supports most of the options we would pass with the apt-get command. Let us start with the search option:

root@ubuntu:/home/hilip# aptitude search vlc

p browser-plugin-vlc - multimedia plugin for web browsers based on VLC

p browser-plugin-vlc:i386 - multimedia plugin for web browsers based on VLC

p libvlc-dev - development files for libvlc

p libvlc-dev:i386 - development files for libvlc

p libvlc5 - multimedia player and streamer library

p vlc - multimedia player and streamer

p vlc:i386 - multimedia player and streamer

root@ubuntu:/home/hilip#

Some output omitted for brevity. Based on the output, we see similar patterns of the aptitude command to that of apt. We can also install and update the package list by passing the update option:

root@ubuntu:/home/hilip# aptitude update

Hit [http://us](http://us).archive.ubuntu.com/ubuntu xenial InRelease

Get: 1 [http://security](http://security).ubuntu.com/ubuntu xenial-security InRelease [107 kB]

Get: 2 [http://us](http://us).archive.ubuntu.com/ubuntu xenial-updates InRelease [109 kB]

Get: 3 [http://us](http://us).archive.ubuntu.com/ubuntu xenial-backports InRelease [107 kB]

Get: 4 [http://us](http://us).archive.ubuntu.com/ubuntu xenial-updates/main amd64 Packages [809 kB]

Get: 5 [http://security](http://security).ubuntu.com/ubuntu xenial-security/main amd64 Packages [524 kB]

Get: 6 [http://us](http://us).archive.ubuntu.com/ubuntu xenial-updates/main i386 Packages [738 kB]

Get: 7 [http://security](http://security).ubuntu.com/ubuntu xenial-security/main i386 Packages [461 kB]

root@ubuntu:/home/hilip#

Some output omitted for brevity.

After we would have updated the package list, we can upgrade the packages by passing the safe-upgrade option:

root@ubuntu:/home/hilip# aptitude safe-upgrade

Resolving dependencies…

The following NEW packages will be installed:

libllvm6.0{a}

The following packages will be REMOVED:

libllvm5.0{u}

The following packages will be upgraded:

libegl1-mesa libgbm1 libgl1-mesa-dri libwayland-egl1-mesa libxatracker2

5 packages upgraded, 1 newly installed, 1 to remove and 0 not upgraded.

Need to get 21.6 MB of archives. After unpacking 14.1 MB will be used.

Do you want to continue? [Y/n/?] y

Installing new version of config file /etc/drirc ...

Setting up libegl1-mesa:amd64 (18.0.5-0ubuntu0~16.04.1) ...

Setting up libwayland-egl1-mesa:amd64 (18.0.5-0ubuntu0~16.04.1) ...

Processing triggers for libc-bin (2.23-0ubuntu10) ...

Current status: 0 (-5) upgradable.

root@ubuntu:/hohiliplip#

Some output omitted for brevity. We can also install a package by passing the "install" option:

root@ubuntu:/hohiliplip# aptitude install vlc

The following NEW packages will be installed:

i965-va-driver{a} liba52-0.7.4{a} libaacs0{a} libass5{a} libavcodec-ffmpeg56{a} libavformat-ffmpeg56{a}

libavutil-ffmpeg54{a} libbasicusageenvironment1{a} libbdplus0{a} libbluray1{a} libcddb2{a} libchromaprint0{a}

libcrystalhd3{a} libdc1394-22{a} libdca0{a} libdirectfb-1.2-9{a} libdvbpsi10{a} libdvdnav4{a} libdvdread4{a}

vlc-plugin-notify{a} vlc-plugin-samba{a}

0 packages upgraded, 73 newly installed, 0 to remove and 0 not upgraded.

Need to get 23.7 MB of archives. After unpacking 119 MB will be used.

Do you want to continue? [Y/n/?] y

Setting up va-driver-all:amd64 (1.7.0-1ubuntu0.1) ...

Processing triggers for libc-bin (2.23-0ubuntu10) ...

Processing triggers for vlc-nox (2.2.2-5ubuntu0.16.04.4) ...

root@ubuntu:/hohiliplip#

We can also remove a package. We would simply pass the remove option:

root@ubuntu:/hohiliplip# aptitude remove vlc

The following packages will be REMOVED:

i965-va-driver{u} liba52-0.7.4{u} libaacs0{u} libass5{u} libavcodec-ffmpeg56{u} libavformat-ffmpeg56{u}

libzvbi-common{u} libzvbi0{u} mesa-va-drivers{u} va-driver-all{u} vlc vlc-data{u} vlc-nox{u} vlc-plugin-notify{u} vlc-plugin-samba{u}

Do you want to continue? [Y/n/?] y

Processing triggers for desktop-file-utils (0.22-1ubuntu5.2) ...

Processing triggers for libc-bin (2.23-0ubuntu10) ...

Processing triggers for hicolor-icon-theme (0.15-0ubuntu1) ...

root@ubuntu:/hohiliplip#

Some output omitted for brevity. The aptitude command is handy for any Linux administrator.

[YUM](#contents.xhtml_sc91a)

The YUM utility is an open-source command-line method for package management for systems using a Red Hat distribution. YUM enables us as Linux administrators to perform automatic updates, package, and dependency management, on RPM-based distributions. Yum is similar to its Debian counterpart APT. The YUM utility makes use of various software repositories. A software repo, as it is commonly called, stores a variety of packages. One of the main reasons for using YUM is that it detects if any dependency file(s) are needed for a particular package. It then prompts the user of the needed file(s) and offers to install them as part of the package installation, which the user would have initiated from the get-go.

| Note: | An interesting point to note is the fact that YUM works with RPM packages. |

To begin with, we can view the available packages in the YUM database by using the list option:

[philip@localhost ~]$ yum list | less

Repodata is over 2 weeks old. Install yum-cron? Or run: yum makecache fast

Loading mirror speeds from cached hostfile

Installed Packages

GConf2.x86_64 3.2.6-8.el7 @anaconda

GeoIP.x86_64 1.5.0-11.el7 @anaconda

ModemManager.x86_64 1.6.0-2.el7 @anaconda

ModemManager-glib.x86_64 1.6.0-2.el7 @anaconda

NetworkManager.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-adsl.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-glib.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-libnm.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-libreswan.x86_64 1.2.4-2.el7 @anaconda

NetworkManager-libreswan-gnome.x86_64 1.2.4-2.el7 @anaconda

NetworkManager-ppp.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-team.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-tui.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-wifi.x86_64 1:1.8.0-9.el7 @anaconda

PackageKit.x86_64 1.1.5-1.el7 @anaconda

Some output omitted for brevity. From the above output, the repo data is old, precisely two weeks. This can be solved by running the makecache fast with YUM:

[philip@localhost ~]$ yum makecache fast

Loaded plugins: fastestmirror, langpacks

Existing lock /var/tmp/yum-philip-FdEYSO/x86_64/7/yum.pid: another copy is running as pid 2322.

Another app is currently holding the yum lock; waiting for it to exit...

The other application is: yum

Memory : 24 M RSS (415 MB VSZ)

Started: Tue Jul 31 05:49:03 2023 - 00:11 ago

State : Traced/Stopped, pid: 2322

Another app is currently holding the yum lock; waiting for it to exit...

The other application is: yum

Memory : 24 M RSS (415 MB VSZ)

Started: Tue Jul 31 05:49:03 2023 - 00:13 ago

State : Traced/Stopped, pid: 2322

Another app is currently holding the yum lock; waiting for it to exit...

The other application is: yum

Memory : 24 M RSS (415 MB VSZ)

Started: Tue Jul 31 05:49:03 2023 - 00:15 ago

State : Traced/Stopped, pid: 2322

^C

Exiting on user cancel.

[philip@localhost ~]$

If you are faced with this message while attempting to update the cache, then we can remove the lock file, which will remedy this:

[philip@localhost ~]$ rm /var/tmp/yum-philip-FdEYSO/x86_64/7/yum.pid

[philip@localhost ~]$ yum makecache fast

Loaded plugins: fastestmirror, langpacks

http://ftp.jaist.ac.jp/pub/Linux/os/x86_64/repodata/repomd.xml: [Errno 14] curl#6 - "Could not resolve host: ftp.jaist.ac.jp; Name or service not known"

Trying other mirror.

base | 3.6 kB 00:00:00

extras | 3.4 kB 00:00:00

http://.mirror.iweb.ca/7/updates/x86_64/repodata/repomd.xml: [Errno 14] curl#6 - "Could not resolve host:mirror.iweb.ca; Name or service not known"

Trying other mirror.

updates | 3.4 kB 00:00:00

(1/2): extras/7/x86_64/primary_db | 172 kB 00:00:10

(2/2): updates/7/x86_64/primary_db | 4.3 MB 00:00:13

Loading mirror speeds from cached hostfile

* base: mirror.iweb.ca

* extras: mirror.iweb.ca

* updates:mirror.iweb.ca

Metadata Cache Created

[philip@localhost ~]$

We can see that the cache has been updated. We can further narrow down the packages being displayed by Yum; we would use the installed option:

[philip@localhost ~]$ yum list installed | less

Loaded plugins: fastestmirror, langpacks

Installed Packages

GConf2.x86_64 3.2.6-8.el7 @anaconda

GeoIP.x86_64 1.5.0-11.el7 @anaconda

ModemManager.x86_64 1.6.0-2.el7 @anaconda

ModemManager-glib.x86_64 1.6.0-2.el7 @anaconda

NetworkManager.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-adsl.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-glib.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-libnm.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-libreswan.x86_64 1.2.4-2.el7 @anaconda

NetworkManager-libreswan-gnome.x86_64 1.2.4-2.el7 @anaconda

NetworkManager-ppp.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-team.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-tui.x86_64 1:1.8.0-9.el7 @anaconda

NetworkManager-wifi.x86_64 1:1.8.0-9.el7 @anaconda

PackageKit.x86_64 1.1.5-1.el7 @anaconda

PackageKit-command-not-found.x86_64 1.1.5-1.el7 @anaconda

PackageKit-glib.x86_64 1.1.5-1.el7 @anaconda

PackageKit-gstreamer-plugin.x86_64 1.1.5-1 @anaconda

Some output omitted for brevity. The packages are displayed by package name, version, and installer from the output. We can also view packages in a group format. We would use the grouplist option:

[philip@localhost ~]$ yum grouplist

Loaded plugins: fastestmirror, langpacks

There is no installed groups file.

Maybe run: yum groups mark convert (see man yum)

Loading mirror speeds from cached hostfile

* base: mirror.iweb.ca

* extras: mirror.iweb.ca

* updates: mirror.iweb.ca

Available Environment Groups:

Minimal Install

Compute Node

Infrastructure Server

File and Print Server

Basic Web Server

Virtualization Host

Server with GUI

GNOME Desktop

KDE Plasma Workspaces

Development and Creative Workstation

Available Groups:

Compatibility Libraries

Console Internet Tools

Development Tools

Graphical Administration Tools

Legacy UNIX Compatibility

Scientific Support

Security Tools

Smart Card Support

System Administration Tools

System Management

Done

[philip@localhost ~]$

To view information about a particular package, we can use the info option:

[philip@localhost ~]$ yum info firefox

Installed Packages

Name : firefox

Arch : x86_64

Version : 52.2.0

Release : 2.el7

Size : 149 M

Repo : installed

From repo : anaconda

Summary : Mozilla Firefox Web browser

URL : http://www.mozilla.org/projects/firefox/

License : MPLv1.1 or GPLv2+ or LGPLv2+

Description : Mozilla Firefox is an open-source web browser, designed for standards

: compliance, performance and portability.

Available Packages

Name : firefox

Arch : i686

Version : 60.1.0

Name : firefox

Arch : x86_64

Version : 60.1.0

Description : Mozilla Firefox is an open-source web browser, designed for standards

: compliance, performance and portability.

[philip@localhost ~]$

From the above output, there are a lot of useful information pertaining to the package.

We can identify a package for a file by using the "provides" option:

[philip@localhost ~]$ yum provides /etc/my.cnf

Loaded plugins: fastestmirror, langpacks

1:mariadb-libs-5.5.56-2.el7.i686 : The shared libraries required for MariaDB/MySQL clients

Repo : base

Matched from:

Filename : /etc/my.cnf

1:mariadb-libs-5.5.56-2.el7.x86_64 : The shared libraries required for MariaDB/MySQL clients

Repo : base

Matched from:

Filename : /etc/my.cnf

1:mariadb-libs-5.5.56-2.el7.x86_64 : The shared libraries required for MariaDB/MySQL clients

Repo : @anaconda

Matched from:

Filename : /etc/my.cnf

[philip@localhost ~]$

Based on the output, the /etc/my.cnf belongs to the mariadb-libs-5.5.56-2.el7.x86_64. We can also search for a package. We would use the search option:

[philip@localhost ~]$ yum search gedit

Loaded plugins: fastestmirror, langpacks

* updates: mirror.iweb.ca

================================================================= N/S matched: gedit =================================================================

gedit-devel.i686 : Support for developing plugins for the gedit text editor

gedit-devel.x86_64 : Support for developing plugins for the gedit text editor

gedit-plugins-data.x86_64 : Common data required by plugins

Name and summary matches only, use "search all" for everything.

[philip@localhost ~]$

Some output omitted for brevity. Now for us to update our system, we would first use the clean all options:

| Note: | You would need root privilege before doing package maintenance. |

[root@localhost philip]# yum clean all

Loaded plugins: fastestmirror, langpacks

Repodata is over 2 weeks old. Install yum-cron? Or run: yum makecache fast

Cleaning repos: base extras updates

Cleaning up everything

Cleaning up list of fastest mirrors

[root@localhost philip]#

Next, we would use the check-update option:

[root@localhost philip]# yum check-update

Loaded plugins: fastestmirror, langpacks

http://ftp.hosteurope.de/mirror.org/7/os/x86_64/repodata/repomd.xml: [Errno 14] curl#6 - "Could not resolve host: ftp.hosteurope.de; Name or service not known."

Trying other mirror.

base |

3.6 kB 00:00:00

extras |

3.4 kB 00:00:00

updates |

3.4 kB 00:00:00

(1/4): base/7/x86_64/group_gz |

166 kB 00:00:09

(2/4): extras/7/x86_64/primary_db |

172 kB 00:00:08

(3/4): updates/7/x86_64/primary_db |

4.3 MB 00:00:14

(4/4): base/7/x86_64/primary_db |

5.9 MB 00:00:16

Determining fastest mirrors

* base: mirror.us.leaseweb.net

* extras: mirror.us.leaseweb.net

* updates: mirror.us.leaseweb.net

ModemManager.x86_64 1.6.10-1.el7 base

accountsservice.x86_64 0.6.45-7.el7 base

accountsservice-libs.x86_64 0.6.45-7.el7 base

acl.x86_64 2.2.51-14.el7 base

base

attr.x86_64 2.4.46-13.el7 base

avahi-gobject.x86_64 0.6.31-19.el7 base

avahi-libs.x86_64 0.6.31-19.el7

yum.noarch 3.4.3-158.el7 base

yum-plugin-fastestmirror.noarch 1.1.31-45.el7 base

yum-utils.noarch 1.1.31-45.el7 base

Obsoleting Packages

grub2.x86_64 1:2.02-0.65.el7.2 base

grub2-tools.x86_64 1:2.02-0.64.el7 @anaconda

grub2-tools-minimal.x86_64 1:2.02-0.65.el7.2 base

[root@localhost philip]#

Some output omitted for brevity. We can also install a package; we would use the install option:

[root@localhost philip]# yum install talk.x86_64

Loaded plugins: fastestmirror, langpacks

* updates: mirror.us.leaseweb.net

Resolving Dependencies

--> Running transaction check

Dependencies Resolved

=====================================================================

Package Arch Version Repository Size

=====================================================================

Installing:

talk x86_64 0.17-46.el7 base 24 k

Transaction Summary

=====================================================================

Install 1 Package

Total download size: 24 k

Installed size: 31 k

Is this ok [y/d/N]: y

Downloading packages:

talk-0.17-46.el7.x86_64.rpm | 24 kB 00:00:04

Running transaction check

Running transaction test

Transaction test succeeded

Running transaction

Installing : talk-0.17-46.el7.x86_64 1/1

Verifying : talk-0.17-46.el7.x86_64 1/1

Installed:

talk.x86_64 0:0.17-46.el7

Complete!

[root@localhost philip]#

We can also remove a package in the opposite order. We would use the remove option:

[root@localhost philip]# yum remove talk.x86_64

Loaded plugins: fastestmirror, langpacks

Resolving Dependencies

--> Running transaction check

---> Package talk.x86_64 0:0.17-46.el7 will be erased

--> Finished Dependency Resolution

Dependencies Resolved

=====================================================================

Package Arch Version Repository Size

=====================================================================

Removing:

talk x86_64 0.17-46.el7 @base 31 k

Transaction Summary

=====================================================================

Remove 1 Package

Installed size: 31 k

Is this ok [y/N]: y

Downloading packages:

Transaction test succeeded

Running transaction

Erasing : talk-0.17-46.el7.x86_64 1/1

Verifying : talk-0.17-46.el7.x86_64 1/1

Removed:

talk.x86_64 0:0.17-46.el7

Complete!

[root@localhost philip]#

If, for some reason, we want to update all packages on the system, we would use the update option:

[root@localhost philip]# yum update

Loaded plugins: fastestmirror, langpacks

Loading mirror speeds from cached hostfile

* base: mirror.us.leaseweb.net

* extras: mirror.us.leaseweb.net

* updates: mirror.us.leaseweb.net

Resolving Dependencies

---> Package python-gobject.x86_64 0:3.22.0-1.el7_4.1 will be an update

---> Package python-gobject-base.x86_64 0:3.22.0-1.el7 will be updated

---> Package python-libs.x86_64 0:2.7.5-58.el7 will be updated

---> Package python-libs.x86_64 0:2.7.5-69.el7_5 will be an update

---> Package python-netaddr.noarch 0:0.7.5-7.el7 will be updated

libwayland-server x86_64 1.14.0-2.el7 base 38 k

unbound-libs x86_64 1.6.6-1.el7 base 405 k

volume_key-libs x86_64 0.3.9-8.el7 base 140 k

Transaction Summary

======================================================================================================================================================

Install 6 Packages (+20 Dependent packages)

Upgrade 586 Packages

Total download size: 691 M

Is this ok [y/d/N]: y

Some output omitted for brevity. Finally, we can view the YUM repo by passing " repolist" option:

[root@localhost philip]# yum repolist

Loaded plugins: fastestmirror, langpacks

Loading mirror speeds from cached hostfile

* base: mirror.us.leaseweb.net

repo id repo name status

repolist: 11,278

[root@localhost philip]#

[dnf](#contents.xhtml_sc92a)

Dandified YUM or dnf is the name of the package management utility. DNF is the next-generation version of the Yellowdog Updater, Modified (YUM). It is used in rpm-based distributions. DNF was introduced in Fedora 18\. DNF has been the default package manager for Fedora since version 22\. When we run YUM commands in newer releases of Fedora, we are running dnf in the background. The dnf utility offers performance, memory usage, dependency resolution, to name a few.

To get started, we can check the version of dnf on our Fedora system, and we would use the --version option:

[root@localhost philip]# dnf --version

2.7.5

Installed: dnf-0:2.7.5-12.fc.noarch at Wed 25 Apr 2023 06:35:34 AM GMT

Built : Fedora Project at Wed 18 Apr 2023 02:29:51 PM GMT

Installed: rpm-0:4.14.1-7.fcx86_64 at Wed 25 Apr 2023 06:34:14 AM GMT

Built : Fedora Project at Mon 19 Feb 2023 09:29:01 AM GMT

[root@localhost philip]#

Based on the above output, we have version 2.7.5 of the dnf utility installed. We can even view the repositories on our system by passing the "repolist" option:

[root@localhost philip]# dnf repolist

Last metadata expiration check: 0:01:09 ago on Tue 31 Jul 2023 03:10:57 PM EDT.

repo id repo name status

*fedora Fedora - x86_64 57,327

*updates Fedora - x86_64 - Updates 16,337

[root@localhost philip]#

Adding to this, we can even expose the YUM command in Fedora to prove that it is an alias to the dnf utility. We would do a listing of the /usr/bin and search for YUM:

[root@localhost philip]# ll /usr/bin | grep yum

lrwxrwxrwx. 1 root root 5 Apr 18 10:29 yum -> dnf-3

[root@localhost philip]#

Based on the above output, indeed, YUM is an alias inside the Fedora system. We can also check to see whether repositories are enabled or not. We would use the repolist all option:

[root@localhost philip]# dnf repolist all

Last metadata expiration check: 0:05:10 ago on Tue 31 Jul 2023 03:10:57 PM EDT.

repo id repo name status

*fedora Fedora 28 - x86_64 enabled: 57,327

fedora-cisco-openh264 Fedora openh264 (From Cisco) - x86_64 disabled

fedora-cisco-openh264-debuginfo Fedora openh264 (From Cisco) - x86_64 - Debug

updates-testing-debuginfo Fedora - x86_64 - Test Updates Debug disabled

updates-testing-source Fedora 28 - Test Updates Source disabled

[root@localhost philip]#

Now to view all the available packages on our system, we would use the list option:

[root@localhost philip]# dnf list

Last metadata expiration check: 0:06:37 ago on Tue 31 Jul 2023 03:10:57 PM EDT.

Installed Packages

GConf2.x86_64 3.2.6-20.fc @anaconda

GeoIP.x86_64 1.6.12-3.fc @anaconda

GeoIP-GeoLite-data.noarch 2023.04-1.fc @anaconda

ImageMagick.x86_64 1:6.9.9.38-1.fc @anaconda

ImageMagick-libs.x86_64 1:6.9.9.38-1.fc @anaconda

LibRaw.x86_64 0.18.8-1.fc @anaconda

ModemManager.x86_64 1.6.12-3.fc @anaconda

ModemManager-glib.x86_64 1.6.12-3.fc @anaconda

NetworkManager.x86_64 1:1.10.6-1.fc @anaconda

NetworkManager-adsl.x86_64 1:1.10.6-1.fc @anaconda

NetworkManager-bluetooth.x86_64 1:1.10.6-1.f @anaconda

NetworkManager-config-connectivity-fedora.noarch

1:1.10.6-1.fc @anaconda

NetworkManager-libnm.x86_64 1:1.10.6-1.fc @anaconda

NetworkManager-openconnect.x86_64 1.2.4-9.fc @anaconda

NetworkManager-openconnect-gnome.x86_64 1.2.4-9.fc @anaconda

zziplib-utils.x86_64 0.13.68-1.fc fedora

zzuf.x86_64 0.15-5.fc fedora

[root@localhost philip]#

Some output omitted for brevity. We can perform searches like YUM; the search option would be used:

[root@localhost philip]# dnf search firefox

Last metadata expiration check: 0:11:22 ago on Tue 31 Jul 2023 03:10:57 PM EDT.

============================================ Summary & Name Matched: firefox =============================================

firefox.x86_64 : Mozilla Firefox Web browser

================================================ Summary Matched: firefox ================================================

icecat.x86_64 : GNU version of Firefox browser

mozilla-ublock-origin.noarch : An efficient blocker for Firefox

mozilla-https-everywhere.noarch : HTTPS enforcement extension for Mozilla Firefox

mozilla-requestpolicy.noarch : Firefox and Seamonkey extension that gives you control over cross-site requests

python-mozrunner.noarch : Reliable start/stop/configuration of Mozilla Applications (Firefox, Thunderbird)

[root@localhost philip]#

Furthermore, to view which package provides a particular utility, we would use the provides option:

[root@localhost philip]# dnf provides /bin/ksh

Last metadata expiration check: 0:14:22 ago on Tue 31 Jul 2023 03:10:57 PM EDT.

ksh-20120801-247.fc.x86_64 : The Original ATT Korn Shell

Repo : updates

Matched from:

Provide : /bin/ksh

ksh-20120801-245.fcx86_64 : The Original ATT Korn Shell

Repo : fedora

Matched from:

Provide : /bin/ksh

[root@localhost philip]#

Adding to this, we can view information for a specific package; we would use the info option:

root@localhost philip]# dnf info libreoffice

Available Packages

Name : libreoffice

Epoch : 1

Version : 6.0.6.1

Summary : Free Software Productivity Suite

URL : http://www.libreoffice.org/

License : (MPLv1.1 or LGPLv3+) and LGPLv3 and LGPLv2+ and BSD and (MPLv1.1 or GPLv2 or LGPLv2 or Netscape) and Public

: Domain and ASL 2.0 and MPLv2.0 and CC0

Description : LibreOffice is an Open Source, community-developed, office productivity suite.

: It includes the key desktop applications, such as a word processor,

: spreadsheet, presentation manager, formula editor and drawing program, with a

: user interface and feature set similar to other office suites. Sophisticated

: and flexible, LibreOffice also works transparently with a variety of file

: formats, including Microsoft Office File Formats.

[root@localhost philip]#

Based on the above output, we can see a lot of useful information for a given package. We can also check for system updates. We would use the check-update option:

[root@localhost philip]# dnf check-update

Last metadata expiration check: 0:18:17 ago on Tue 31 Jul 2023 03:10:57 PM EDT.

GeoIP-GeoLite-data.noarch 2023.06-1.fc updates

LibRaw.x86_64 0.18.13-1.fc updates

rkManager-openvpn.x86_64 1:1.8.4-1.fc updates

NetworkManager-openvpn-gnome.x86_64 1:1.8.4-1.fc updates

grub2-tools-extra.x86_64 1:2.02-38.fc updates

grub2-tools.x86_64 1:2.02-34.fc @anaconda

grub2-tools-minimal.x86_64 1:2.02-38.fc updates

grub2-tools.x86_64 1:2.02-34.fc @anaconda

kernel-headers.x86_64 4.17.9-200.fc updates

kernel-headers.x86_64 4.16.3-301.fc @anaconda

[root@localhost philip]#

Some output omitted for brevity. To install a package, we would use the install option:

[root@localhost philip]# dnf install HexChat.x86_64

Last metadata expiration check: 0:20:30 ago on Tue 31 Jul 2023 03:10:57 PM EDT.

Dependencies resolved.

==========================================================================================================================

Package Arch Version Repository Size

==========================================================================================================================

Installing:

HexChat x86_64 1.2.1-15.fc fedora 1.6 M

Transaction Summary

==========================================================================================================================

Install 1 Package

Total download size: 1.6 M

Installed size: 3.3 M

Is this ok [y/N]: y

Installed:

HexChat.x86_64 1.2.1-15.fc

Complete!

[root@localhost philip]#

The options are similar to its older counterpart YUM. Similarly, to remove a package, we would use the remove option:

[root@localhost philip]# dnf remove HexChat.x86_64

Dependencies resolved.

==========================================================================================================================

Package Arch Version Repository Size

==========================================================================================================================

Removing:

HexChat x86_64 1.2.1-15.fc @fedora 3.3 M

Transaction Summary

==========================================================================================================================

Remove 1 Package

Freed space: 3.3 M

Is this ok [y/N]: y

Running transaction check

Preparing : 1/1

Erasing : HexChat-1.2.1-15.fc.x86_64 1/1

Verifying : HexChat-1.2.1-15.fc.x86_64 1/1

Removed:

HexChat.x86_64 1.2.1-15.fc

Complete!

[root@localhost philip]#

We can also remove packages that were only needed to satisfy dependencies. We would use the autoremove option:

[root@localhost philip]# dnf autoremove

Last metadata expiration check: 0:25:12 ago on Tue 31 Jul 2023 03:10:57 PM EDT.

Dependencies resolved.

Nothing to do.

Complete!

[root@localhost philip]#

If we would like to see the various dnf commands which were executed, we can use the "history" option:

[root@localhost philip]# dnf history

ID | Command line | Date and time | Action(s) | Altered

-------------------------------------------------------------------------------

3 | remove HexChat.x86_64 | 2023-07-31 15:33 | Erase | 1

2 | install HexChat.x86_64 | 2023-07-31 15:31 | Install | 1

1 | | 2023

-04-25 02:33 | Install | 1596 EE

[root@localhost philip]#

This is very useful when tracking what has changed in our system. Before we update our system, it is always a good idea to do some housekeeping. We would use the clean all option:

[root@localhost philip]# dnf clean all

18 files removed

[root@localhost philip]#

Finally, to update all packages on the system, we would use the "update" option:

[root@localhost philip]# dnf update

Last metadata expiration check: 0:11:49 ago on Tue 31 Jul 2023 03:48:23 PM EDT.

Dependencies resolved.

==========================================================================================================================

Package Arch Version Repository Size

==========================================================================================================================

Upgrading:

GeoIP-GeoLite-data noarch 2023.06-1.fc updates 551 k

LibRaw x86_64 0.18.13-1.fc updates

libkcapi x86_64 1.1.1-6.fc updates 44 k

libkcapi-hmaccalc x86_64 1.1.1-6.fc updates 26 k

libnice x86_64 0.1.14-7.20180504git34d6044.fc updates 173 k

libvirt-daemon-config-network x86_64 4.1.0-3.fc updates 10 k

rpm-sign-libs x86_64 4.14.1-9.fc updates 73 k

xmlsec1-nss x86_64 1.2.25-4.fc updates 79 k

Transaction Summary

==========================================================================================================================

Install 11 Packages

Upgrade 736 Packages

Total download size: 1.0 G

Is this ok [y/N]: y

Some output omitted for brevity. We can also pass the "upgrade" option which is newer:

[root@localhost philip]# dnf upgrade

Last metadata expiration check: 0:11:49 ago on Tue 31 Jul 2023 03:48:23 PM EDT.

Dependencies resolved.

==========================================================================================================================

Package Arch Version Repository Size

==========================================================================================================================

Upgrading:

GeoIP-GeoLite-data noarch 2023.06-1.fc updates 551 k

LibRaw x86_64 0.18.13-1.fc updates

libkcapi x86_64 1.1.1-6.fc updates 44 k

libkcapi-hmaccalc x86_64 1.1.1-6.fc updates 26 k

libnice x86_64 0.1.14-7.20180504git34d6044.fc updates 173 k

libvirt-daemon-config-network x86_64 4.1.0-3.fc updates 10 k

rpm-sign-libs x86_64 4.14.1-9.fc updates 73 k

xmlsec1-nss x86_64 1.2.25-4.fc updates 79 k

Transaction Summary

==========================================================================================================================

Install 11 Packages

Upgrade 736 Packages

Total download size: 1.0 G

Is this ok [y/N]: y

Some output omitted for brevity. As we can see, the process is identical.

[Red-hat package manager](#contents.xhtml_sc93a)

Red-hat Package Manager (RPM) is a program for installing, uninstalling, and managing software packages in rpm-based distributions Linux. Various utilities make use of the rpm utility in the backend, YUM and dnf,  to name a few. It is similar to its counterpart, the dpkg utility. Whenever there are dependencies requirements, you would usually have to manually go out, find the necessary files, and install them. The packages that rpm manages all end with an rpm extension.

To begin with, we can check for an rpm signature against a package. We would use the —check-sig option:

[root@localhost Downloads]# rpm --checksig gnome-calculator-3.22.3-1.el7.x86_64.rpm

gnome-calculator-3.22.3-1.el7.x86_64.rpm: rsa sha1 (md5) pgp md5 OK

[root@localhost Downloads]#

Based on the above output, the signatures have passed the checks using the rpm utility. We can also check for dependencies for a particular package. We would use the qpR options:

[root@localhost Downloads]# rpm -qpR gnome-calculator-3.22.3-1.el7.x86_64.rpm

/bin/sh

/bin/sh

libatk-1.0.so.0()(64bit)

libc.so.6()(64bit)

libc.so.6(GLIBC_2.14)(64bit)

libc.so.6(GLIBC_2.2.5)(64bit)

libc.so.6(GLIBC_2.3.4)(64bit)

libgmp.so.10()(64bit)

rtld(GNU_HASH)

rpmlib(PayloadIsXz) <= 5.2-1

[root@localhost Downloads]#

Some output omitted for brevity. The q means to query, the p means to list capabilities this package provides, and the R means list capabilities on which this package depends.

To view all packages which were recently installed, we can use the qa in combination with —last:

[root@localhost Downloads]# rpm -qa --last

gpg-pubkey-f4a80eb5-53a7ff4b Tue 31 Jul 2023 08:30:07 AM PDT

words-3.0-22.el7.noarch Wed 20 Jun 2023 09:29:01 AM PDT

iwl6000-firmware-9.221.4.1-56.el7.noarch Wed 20 Jun 2023 09:29:01 AM PDT

iwl6050-firmware-41.28.5.1-56.el7.noarch Wed 20 Jun 2023 09:29:00 AM PDT

iwl6000g2b-firmware-17.168.5.2-56.el7.noarch Wed 20 Jun 2023 09:29:00 AM PDT

iwl4965-firmware-228.61.2.24-56.el7.noarch Wed 20 Jun 2023 09:29:00 AM PDT

iwl3945-firmware-15.32.2.9-56.el7.noarch Wed 20 Jun 2023 09:29:00 AM PDT

iwl100-firmware-39.31.5.1-56.el7.noarch Wed 20 Jun 2023 09:29:00 AM PDT

iwl7265-firmware-22.0.7.0-56.el7.noarch Wed 20 Jun 2023 09:28:59 AM PDT

fontpackages-filesystem-1.44-8.el7.noarch Wed 20 Jun 2023 09:15:44 AM PDT

centos-release-7-4.1708.el7.centos.x86_64 Wed 20 Jun 2023 09:15:44 AM PDT

[root@localhost Downloads]#

Some output omitted for brevity. We can also search for a specific package by passing the package name:

[root@localhost Downloads]# rpm -qa ntp

ntp-4.2.6p5-25.el7.centos.2.x86_64

[root@localhost Downloads]#

In this case, we search for the ntp package. We can get more information about a particular package. We can pass the qi options:

[root@localhost Downloads]# rpm -qi ntp

Name : ntp

Version : 4.2.6p5

Vendor : CentOS

URL : http://www.ntp.org

Summary : The NTP daemon and utilities

Description :

The Network Time Protocol (NTP) is used to synchronize a computer's

time with another reference time source. This package includes ntpd

(a daemon which continuously adjusts system time) and utilities used

to query and configure the ntpd daemon.

[root@localhost Downloads]#

Some output omitted for brevity. Interestingly, before we install a package, we can get information on the said package and then decide whether to abort or continue installation:

[root@localhost Downloads]# rpm -qa gnome-calculator

gnome-calculator-3.22.3-1.el7.x86_64

[root@localhost Downloads]# rpm -e gnome-calculator

[root@localhost Downloads]# rpm -qa gnome-calculator

[root@localhost Downloads]#

We queried for the gnome calculator because it came pre-installed in this CentOS7 system. We then removed the package and queried once again. Now let us pass the qip on the rpm package which we downloaded:

[root@localhost Downloads]# rpm -qip gnome-calculator-3.22.3-1.el7.x86_64.rpm

Name : gnome-calculator

Version : 3.22.3

Release : 1.el7

Architecture: x86_64

Install Date: (not installed)

Group : Unspecified

Size : 5053847

Summary : A desktop calculator

Description :

gnome-calculator is a powerful graphical calculator with financial,

logical and scientific modes. It uses a multiple precision package

to do its arithmetic to give a high degree of accuracy.

[root@localhost Downloads]#

The rpm utility is potent. To install a package, we would use the -i or --install option:

[root@localhost Downloads]# rpm --install gnome-calculator-3.22.3-1.el7.x86_64.rpm

[root@localhost Downloads]# rpm -qa gnome-calculator

gnome-calculator-3.22.3-1.el7.x86_64

[root@localhost Downloads]#

From the above output, we can see that our package was successfully installed using the rpm utility. We can view all of the files for a particular package:

[root@localhost Downloads]# rpm -ql gnome-calculator

/usr/bin/gcalccmd

/usr/bin/gnome-calculator

/usr/lib64/gnome-calculator

/usr/share/applications/gnome-calculator.desktop

/usr/share/man/man1/gnome-calculator.1.gz

[root@localhost Downloads]#

Some output omitted for brevity. Likewise, we can remove a package by passing the -e option. We can also view the process of removing a package by adding the -v option:

[root@localhost Downloads]# rpm -ev gnome-calculator

Preparing packages...

gnome-calculator-3.22.3-1.el7.x86_64

[root@localhost Downloads]#

Finally, we can determine which package a particular configuration file belongs to. We would use the -qf options:

[root@localhost Downloads]# rpm -qf /etc/rsyslog.conf

rsyslog-8.24.0-12.el7.x86_64

[root@localhost Downloads]#

[yumex](#contents.xhtml_sc94a)

YUM extender, or yumex for short, is a front-end to the YUM and dnf utility. By default, yumex does not come pre-installed with Fedora 28\. This can quickly be addressed by installing the yumex utility at the shell:

[root@localhost philip]# dnf install yumex-dnf

Last metadata expiration check: 0:01:38 ago on Thu 02 Aug 2023 10:30:42 AM EDT.

Dependencies resolved.

==========================================================================================================================

Package Arch Version Repository Size

==========================================================================================================================

Installing:

dnfdragora noarch 1.0.1-10.git20180108.b0e8a66.fc fedora 364 k

Installing dependencies:

checkpolicy x86_64 2.8-1.fc updates 336 k

dnfdaemon noarch 0.3.18-6.fc fedora 64 k

python3-dnfdaemon noarch 0.3.18-6.fc fedora 23 k

python3-libsemanage x86_64 2.7-12.fc fedora 125 k

Transaction Summary

==========================================================================================================================

Install 23 Packages

Total download size: 5.6 M

Installed size: 17 M

Is this ok [y/N]: y

Some output omitted for brevity. As you can see, installing the yumex on Fedora 28 is simple. For CentOS7, we would first install the Extra Packages for Enterprise Linux (EPEL):

[root@localhost philip]# yum install epel-release

Loaded plugins: fastestmirror, langpacks

Loading mirror speeds from cached hostfile

* base: mirror.as24220.net

* extras: mirror.as24220.net

* updates: mirror.as24220.net

Resolving Dependencies

--> Running transaction check

---> Package epel-release.noarch 0:7-11 will be installed

--> Finished Dependency Resolution

Dependencies Resolved

================================================================================

Package Arch Version Repository Size

================================================================================

Installing:

epel-release noarch 7-11 extras 15 k

Transaction Summary

================================================================================

Install 1 Package

Total download size: 15 k

Installed size: 24 k

Is this ok [y/d/N]: y

Downloading packages:

epel-release-7-11.noarch.rpm | 15 kB 00:03

Installing : epel-release-7-11.noarch 1/1

Verifying : epel-release-7-11.noarch 1/1

Installed:

epel-release.noarch 0:7-11

Complete!

[root@localhost philip]#

Next, we would then install the actual yumex utility:

[root@localhost philip]# yum install yumex

Loaded plugins: fastestmirror, langpacks

epel/x86_64/metalink | 4.0 kB 00:00

epel | 3.2 kB 00:00

(1/3): epel/x86_64/group_gz | 88 kB 00:01

(2/3): epel/x86_64/updateinfo | 927 kB 00:02

(3/3): epel/x86_64/primary | 3.6 MB 00:00:16

Loading mirror speeds from cached hostfile

* base: mirror.as24220.net

.net

epel 12639/12639

Resolving Dependencies

--> Running transaction check

---> Package yumex.noarch 0:3.0.17-1.el7 will be installed

--> Processing Dependency: pexpect for package: yumex-3.0.17-1.el7.noarch

---> Package python2-pyxdg.noarch 0:0.25-6.el7 will be installed

--> Finished Dependency Resolution

Dependencies Resolved

============

Package Arch Version Repository Size

===========

Installing:

yumex noarch 3.0.17-1.el7 epel 444 k

Installing for dependencies:

pexpect noarch 2.3-11.el7 base 142 k

python2-pyxdg noarch 0.25-6.el7 epel 89 k

Transaction Summary

======================================================================================================================================================

Install 1 Package (+2 Dependent packages)

Total download size: 675 k

Installed size: 2.7 M

Is this ok [y/d/N]: y

Downloading packages:

warning: /var/cache/yum/x86_64/7/epel/packages/python2-pyxdg-0.25-6.el7.noarch.rpm: Header V3 RSA/SHA256 Signature, key ID 352c64e5: NOKEY-:--:-- ETA

------------------------------------------------------------------------------------------------------------------------------------------------------

Total 167 kB/s | 675 kB 00:00:04

Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7

Importing GPG key 0x352C64E5:

Userid : "Fedora EPEL (7) <epel@fedoraproject.org>"

Fingerprint: 91e9 7d7c 4a5e 96f1 7f3e 888f 6a2f aea2 352c 64e5

Package : epel-release-7-11.noarch (@extras)

From : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7

Is this ok [y/N]: y

Transaction test succeeded

Running transaction

Installing : yumex-3.0.17-1.el7.noarch 3/3

warning: /etc/yumex.conf created as /etc/yumex.conf.rpmnew

Verifying : yumex-3.0.17-1.el7.noarch 1/3

Verifying : pexpect-2.3-11.el7.noarch 3/3

Installed:

yumex.noarch 0:3.0.17-1.el7

Dependency Installed:

pexpect.noarch 0:2.3-11.el7 python2-pyxdg.noarch 0:0.25-6.el7

Complete!

[root@localhost philip]#

Some output omitted for Brevity. The steps illustrated for installing yumex on CentOS7 are similar to that of Fedora28\. Finally, we can launch the yumex utility at the shell or via the GUI. We will demonstrate the shell method:

[root@localhost philip]# yumex &

[1] 2884

[root@localhost philip]# Don't run yumex as root it is unsafe (Use --root to force)

From the above output, it is a clear indication that we should not run the yumex utility as root. Instead, we will run the yumex utility as a non-root user:

root@localhost philip]# exit

exit

[philip@localhost ~]$ yumex &

[1] 2937

[philip@localhost ~]$ 07:48:33 : INFO - Using config file : /home/philip/.config/yumex/yumex.conf

07:48:33 : INFO - Using config file : /home/philip/.config/yumex/yumex.conf

(<class 'dbus.exceptions.DBusException'>, DBusException('Rejected send message, 2 matched rules; type="method_call", sender=":1.115" (uid=1000 pid=2937 comm="/usr/bin/python -tt /usr/bin/yumex ") interface="(unset)" member="GetDevices" error name="(unset)" requested_reply="0" destination=":1.8" (uid=0 pid=633 comm="/usr/sbin/NetworkManager --no-daemon ")',), <traceback object at 0x2ac5ef0>)(<class 'dbus.exceptions.DBusException'>, DBusException('Rejected send message, 2 matched rules; type="method_call", sender=":1.115" (uid=1000 pid=2937 comm="/usr/bin/python -tt /usr/bin/yumex ") interface="(unset)" member="GetDevices" error name="(unset)" requested_reply="0" destination=":1.8" (uid=0 pid=633 comm="/usr/sbin/NetworkManager --no-daemon ")',), <traceback object at 0x2ac6ef0>)

Refer to [Figure 4.5](#ch04.xhtml_fig4-5):

![yumexprompt.png](images/Figure_4.5.png)

Figure 4.5: Authentication required for the root user

Ironically, we are being prompted for the root password, and it may seem confusing for some but not for us. So, we will authenticate, and then be greeted with the nifty yumex utility. Refer to [Figure 4.6](#ch04.xhtml_fig4-6):

![yumex1.png](images/Figure_4.6.png)

Figure 4.6: The yumex utility

We will notice right off the bat that we have a nice user-friendly GUI with which we can work. There is a menu bar at the top, and a search field for finding a particular package. We would simply type the name for a package, for instance. Refer to [Figure 4.7](#ch04.xhtml_fig4-7):

![yumex2.png](images/Figure_4.7.png)

Figure 4.7: Search option of the yumex utility

We get a nice description for a given package, we can then select the check box and click Apply, and the package will be installed.

[Rsyslog](#contents.xhtml_sc95a)

It is possible to configure a Linux system to perform remote logging. We would install (if already not installed) the logging software. For this demonstration, we will use the Fedora as the logging client and the Ubuntu system as the logging server. Also, we will use Rsyslog as the logging software.

First, let s install the Rsyslog software in Fedora. We will use the dnf command as illustrated below:

[root@localhost philip]# dnf search rsyslog

Last metadata expiration check: 1:38:20 ago on Mon 10 Jun 2023 10:41:18 AM EDT.

============================================= Name Exactly Matched: rsyslog ==============================================

rsyslog.x86_64 : Enhanced system logging and kernel message trapping daemon

============================================ Summary & Name Matched: rsyslog =============================================

rsyslog-mysql.x86_64 : MySQL support for rsyslog

rsyslog-hiredis.x86_64 : Redis support for rsyslog

rsyslog-doc.noarch : HTML documentation for rsyslog

[root@localhost philip]#

Some output omitted for brevity. Based on the above, we have found the rsyslog package. Next, we will pass the install option to install the rsyslog package:

[root@localhost philip]# dnf install rsyslog.x86_64

Last metadata expiration check: 2:42:37 ago on Mon 10 Jun 2023 10:41:18 AM EDT.

Dependencies resolved.

==========================================================================================================================

Package Arch Version Repository Size

==========================================================================================================================

Installing:

rsyslog x86_64 8.37.0-1.fc updates 697 k

Installing dependencies:

libestr x86_64 0.1.9-10.fc fedora 26 k

libfastjson x86_64 0.99.8-2.fc fedora 36 k

Transaction Summary

==========================================================================================================================

Install 3 Packages

Total download size: 759 k

Installed size: 2.2 M

Is this ok [y/N]: y

Installed:

rsyslog.x86_64 8.37.0-1.fc libestr.x86_64 0.1.9-10.fc libfastjson.x86_64 0.99.8-2.fc

Complete!

[root@localhost philip]#

Some output omitted for brevity. Based on the above, we have successfully installed the rsyslog package. Now, we would need to edit the /etc/rsyslog.conf in a text editor such as vi or nano; we would need to specify the remote logging server’s IP address. Here is how we would do that:

[root@localhost philip]# cat /etc/rsyslog.conf

# rsyslog configuration file

# For more information see /usr/share/doc/rsyslog-*/rsyslog_conf.html

# or latest version online at http://www.rsyslog.com/doc/rsyslog_conf.html

# If you experience problems, see http://www.rsyslog.com/doc/troubleshoot.html

#queue.maxdiskspace="1g" # 1gb space limit (use as much as possible)

#queue.saveonshutdown="on" # save messages to disk on shutdown

#queue.type="LinkedList" # run asynchronously

#action.resumeRetryCount="-1" # infinite retries if host is down

# # Remote Logging (we use TCP for reliable delivery)

# # remote_host is: name/ip, e.g. 192.168.0.1, port optional e.g. 10514

#Target="remote_host" Port="XXX" Protocol="tcp")

*.* @172.16.175.132:514

[root@localhost philip]#

Some output omitted for brevity. Based on the above output, we added the last entry.

*.* @172.16.175.132:514

This is informing the local system to send all log facilities *. messages with all the severity .* to a remote system 172.16.175.132 using protocol UDP and port number 514. We can also be more specific; for instance, we can only send emergency messages from every facility by specifying the keyword emerg:

[root@localhost philip]# cat /etc/rsyslog.conf

# rsyslog configuration file

#queue.maxdiskspace="1g" # 1gb space limit (use as much as possible)

#queue.saveonshutdown="on" # save messages to disk on shutdown

#queue.type="LinkedList" # run asynchronously

#action.resumeRetryCount="-1" # infinite retries if host is down

# # Remote Logging (we use TCP for reliable delivery)

# # remote_host is: name/ip, e.g. 192.168.0.1, port optional e.g. 10514

#Target="remote_host" Port="XXX" Protocol="tcp")

*.emerg @172.16.175.132:514

[root@localhost philip]#

Based on the above, every facility with emergency messages will be sent to the remote server via UDP. Up to this point, we have been using UDP to send the logs, but sending them using TCP is possible. We would need to add another @ in front of the first @ to use TCP as transport. This can be shown below. We are going to change the message type from emerg to info and use TCP as the transport protocol:

[root@localhost philip]# cat /etc/rsyslog.conf

# rsyslog configuration file

#queue.saveonshutdown="on" # save messages to disk on shutdown

#queue.type="LinkedList" # run asynchronously

#action.resumeRetryCount="-1" # infinite retries if host is down

# # Remote Logging (we use TCP for reliable delivery)

# # remote_host is: name/ip, e.g. 192.168.0.1, port optional e.g. 10514

#Target="remote_host" Port="XXX" Protocol="tcp")

*.info @@172.16.175.132:514

[root@localhost philip]#

Some output omitted for brevity. The last step would be to restart the rsyslog daemon so that the new changes can take effect. We would use the systemctl command as shown below to restart the rsyslog daemon:

[root@localhost philip]# systemctl restart rsyslog

Refer to [Figure 4.8](#ch04.xhtml_fig4-8):

![rsyslog status.png](images/Figure_4.8.png)

Figure 4.8: The systemctl command with the status option

Based on the above, we can see that the rsyslog daemon is running. Note at the bottom of the systemctl status. There are some logs about connecting to the 172/16.175.132, and this is because we have not configured the remote server to accept the logs coming from the Fedora system. Now we will head over to the Ubuntu system and edit the /etc/rsyslog.conf and add the following:

root@philip-virtual-machine:/var/log# cat /etc/rsyslog.conf

# provides UDP syslog reception

#module(load="imudp")

#input(type="imudp" port="514")

# provides TCP syslog reception

module(load="imtcp")

input(type="imtcp" port="514")

root@philip-virtual-machine:/var/log#

Some output omitted for brevity. Based on the above, we have taken off the comments in the TCP section. The last step would be to restart the rsyslog daemon; this can be done using the systemctl command as shown in [Figure 4.9](#ch04.xhtml_fig4-9):

![rsyslogserver.png](images/Figure_4.9.png)

Figure 4.9: The systemctl command with the status option

Based on the above, the rsyslog daemon is running without error. To test, we will check the /var/log/syslog for the Fedora logging client logs. We can use another powerful command to generate a test log; the logger command. Here is how we would use the logger command as shown below:

On the Fedora 28 Rsyslog client, we issue the following:

[root@localhost philip]# logger This is the Fedora Logging client 172.16.175.129

[root@localhost philip]# logger This is another Logging test from the Fedora client 172.16.175.129

[root@localhost philip]#

Over on the Ubuntu Rsyslog  server we will see the following:

root@philip-virtual-machine:/home/philip# tail -f /var/log/syslog

Jun 10 14:20:46 localhost dbus-daemon[720]: [system] Successfully activated service 'net.reactivated.Fprint'

Jun 10 14:20:46 localhost systemd[1]: Started Fingerprint Authentication Daemon.

Jun 10 14:20:50 localhost kscreenlocker_greet[58309]: QObject::disconnect: No such signal QObject::screenChanged(QScreen*)

Jun 10 14:22:25 localhost philip[58396]: This is the Fedora Logging client 172.16.175.129

Jun 10 14:23:04 localhost philip[58403]: This is another Logging test from the Fedora client 172.16.175.129

^C

root@philip-virtual-machine:/home/philip#

Based on the above, we can see that the Rsyslog client is sending the logs across the network to the Ubuntu Rsyslog server.

[Conclusion](#contents.xhtml_sc96a)

In this chapter, we covered modules, and this was then followed by localization. After this, we looked at Debian and Red Hat ways of managing software. Finally, we wrapped up this chapter with Rsyslog.

In the next chapter, we focus on user and password management.

Join our book’s Discord space

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 5User and Password Management](#contents.xhtml_ch05a)

[Introduction](#contents.xhtml_sc97a)

In the previous chapter, we focused on software management.

In this chapter, we will cover user and password management. First, we will focus on user accounts. Next, the focus will be on groups. Finally, we will wrap this chapter with password management.

[Structure](#contents.xhtml_sc98a)

In this chapter, we will discuss the following topics:

*   User accounts
*   Managing groups
*   Password management

[Objectives](#contents.xhtml_sc99a)

In this chapter, we will delve into the essentials of user management. This includes acquiring the skills to create user accounts, modify their properties, and create and modify groups. Additionally, we will explore the techniques for effectively managing passwords. By the end of this chapter, you will have a comprehensive understanding of these key aspects, enabling you to efficiently handle user accounts, groups, and passwords within a system.

[User accounts](#contents.xhtml_sc100a)

Several events occur whenever we create a new user using the useradd command in a system. To begin with, there is a structure in place regarding the respected directories that will be generated for a new user. The structure is stored in the skeleton directory in the /etc/skel directory. The /etc/skel directory contains files and folders copied into the new user’s home directory. We can look at the skeleton directory using our Ubuntu system:

root@ubuntu:/home/philip# ls -a /etc/skel/

. .. .bash_logout .bashrc examples.desktop .profile

root@ubuntu:/home/philip#

Each new user pulls its structure from here. The dot (.) indicates a hidden file. There the /etc/skel/.logout, /etc/.skel/.bashrc, and the /etc/skel/.profile.

Let us explore essential bash files in Linux, including .bash_logout, .bashrc, .profile, and .bash_history, and use the /etc/skel directory for user creation.

The .bash_logout

In Linux, the bash_logout file is a script executed by the Bash shell when a user logs out of the system. It allows users to customize their logout process by specifying commands or actions to be performed automatically before they are logged out.

The bash_logout file is typically located in the user’s home directory, and its name is .bash_logout, with a leading dot indicating that it is a hidden file. If the file does not exist, the shell will simply ignore it.

It clears the screen to ensure privacy upon logout. As can be seen:

root@ubuntu:/home/philip# cat /home/philip/.bash_logout

# ~/.bash_logout: executed by bash(1) when login shell exits.

# when leaving the console clear the screen to increase privacy

if [ "$SHLVL" = 1 ]; then

[ -x /usr/bin/clear_console ] && /usr/bin/clear_console -q

fi

root@ubuntu:/home/philip#

*   The .bashrc

The /etc/skel/.bashrc is usually used for storing alias for various. This can be seen by looking at the /etc/skel/.bashrc:

root@ubuntu:/home/philip# cat /etc/skel/.bashrc

# colored GCC warnings and errors

#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases

alias ll='ls -alF'

alias la='ls -A'

alias l='ls -CF'

root@ubuntu:/home/philip#

Some output was omitted for brevity. Based on the above, some aliases have been defined for us; one example is the alias ll='ls -af'.

*   The .profile

The /etc/skel/.profile does several tasks; one of which is to check for the existence of the $Home/.bashrc.

This is evident by looking at the /etc/skel/.profile :

root@ubuntu:/home/philip# cat /etc/skel/.profile

#umask 022

# if running bash

if [ -n "$BASH_VERSION" ]; then

# include .bashrc if it exists

if [ -f "$HOME/.bashrc" ]; then

. "$HOME/.bashrc"

fi

fi

# set PATH so it includes user's private bin directories

PATH="$HOME/bin:$HOME/.local/bin:$PATH"

root@ubuntu:/home/philip#

Some output was omitted for brevity. Based on the above output, we can see the section #if running bash. Another way to see that these directories are copied over is by looking at an existing user. We will use the ls command in combination with the egrep command:

root@ubuntu:/home/philip# ls -a ~ | egrep '.bash|.profile'

.bash_history

.bashrc

.profile

root@ubuntu:/home/philip#

Based on the above output, we can see the .bash_history, .bashrc and .profile.

*   The .bash_history

The .bash_history stores every command executed at the command prompt. The .bash_history is only created after we start running commands at the command prompt. Here is a brief look at the /home/philip/.bash_history:

root@ubuntu:/home/philip# cat /home/philip/.bash_history

ls /etc/grub.d/

cat /var/log/Xorg.0.log | less

startx

sudo su

Xorg -configure

rm /tmp/.X0-lock

sudo su

su

sudo su

root@ubuntu:/home/philip#

Some output was omitted for brevity.

Also, we can check another user for the existence of the various .bash files:

root@ubuntu:/home/philip# ls -a /home/philip | egrep '.bash|.profile'

.bash_history

.bash_logout

.bashrc

.profile

root@ubuntu:/home/philip#

We can see the .bash_history, .bash_logout., .bashrc, and the .profile.

Another way to identify that the /etc/skel directory is being used when creating a new user with the useradd command, we could call the useradd command and pass the -D option:

root@ubuntu:/home/philip# useradd -D

GROUP=100

HOME=/home

INACTIVE=-1

EXPIRE=

SHELL=/bin/sh

SKEL=/etc/skel

CREATE_MAIL_SPOOL=no

root@ubuntu:/home/philip#

Based on the above output, we are given a wealth of information. Particularly, the SKEL=/etc/skel, indicates which directory to use when creating a new user.

[The w command](#contents.xhtml_sc101a)

The w command displays the currently logged-in users in the system. We can look at the w command:

root@ubuntu:/home/philip# w

08:00:03 up 22:14, 4 users, load average: 0.04, 0.01, 0.00

USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT

philip tty2 :1 Mon13 7days 1:35 0.29s /sbin/upstart --user

root@ubuntu:/home/philip#

Based on the above, the fields start from the user moving from left to right. Some interesting fields are the FROM, which shows where the user logged in from (if it is over a network, it will show an IP address), and the LOGIN@, which shows which date the user logged in. We can see the available options by passing the --help option:

root@ubuntu:/home/philip# w --help

Usage:

w [options]

Options:

-h, --no-header do not print header

-u, --no-current ignore current process username

-s, --short short format

-f, --from show remote hostname field

-o, --old-style old style output

-i, --ip-addr display IP address instead of hostname (if possible)

--help display this help and exit

-V, --version output version information and exit

For more details see w(1).

root@ubuntu:/home/philip#

[The who command](#contents.xhtml_sc102a)

The who command is another popular command for displaying currently logged-in users. We simply do who command without any options:

root@ubuntu:/home/philip# who

philip tty2 2023-09-03 13:29 (:1)

root@ubuntu:/home/philip#

We can identify the date and time when the system booted up. We would pass the -a option:

root@ubuntu:/home/philip# who -a

system boot 2023-08-27 12:33

LOGIN tty1 2023-09-03 13:29 13792 id=tty1

run-level 5 2023-08-27 12:33

tty2 2023-08-30 06:34 1434 id= term=0 exit=0

tty2 2023-08-30 06:35 9661 id= term=0 exit=0

tty2 2023-09-03 13:17 10231 id= term=0 exit=0

philip + tty2 2023-09-03 13:29 old 13815 (:1)

root@ubuntu:/home/philip#

The first entry system boot, displays the date and time the system booted up. We can see the available options by passing the --help option:

root@ubuntu:/home/philip# who --help

Usage: who [OPTION]... [ FILE | ARG1 ARG2 ]

Print information about users who are currently logged in.

-a, --all same as -b -d --login -p -r -t -T -u

-b, --boot time of last system boot

-d, --dead print dead processes

-H, --heading print line of column headings

--ips print ips instead of hostnames. with --lookup,

canonicalizes based on stored IP, if available,

rather than stored hostname

-l, --login print system login processes

--lookup attempt to canonicalize hostnames via DNS

-m only hostname and user associated with stdin

-p, --process print active processes spawned by init

-q, --count all login names and number of users logged on

-r, --runlevel print current runlevel

-s, --short print only name, line, and time (default)

-t, --time print last system clock change

-T, -w, --mesg add user's message status as +, - or ?

-u, --users list users logged in

--message same as -T

--writable same as -T

--help display this help and exit

--version output version information and exit

root@ubuntu:/home/philip#

[The last command](#contents.xhtml_sc103a)

The last is another popular command for displaying the users who have recently logged in. We would simply say last:

root@ubuntu:/home/philip# last

tom pts/18 172.16.175.129 Tue Sep 4 08:31 still logged in

wtmp begins Tue Sep 4 08:31:36 2023

root@ubuntu:/home/philip#

Based on the above output, the user tom has logged in over the network. We can see the available options by passing the --help option:

root@ubuntu:/home/philip# last --help

Usage:

last [options] [<username>...] [<tty>...]

Show a listing of last logged in users.

Options:

-<number> how many lines to show

-a, --hostlast display hostnames in the last column

-d, --dns translate the IP number back into a hostname

-f, --file <file> use a specific file instead of /var/log/wtmp

-F, --fulltimes print full login and logout times and dates

-i, --ip display IP numbers in numbers-and-dots notation

-n, --limit <number> how many lines to show

-R, --nohostname don't display the hostname field

-s, --since <time> display the lines since the specified time

-t, --until <time> display the lines until the specified time

-p, --present <time> display who were present at the specified time

-w, --fullnames display full user and domain names

-x, --system display system shutdown entries and run level changes

--time-format <format> show timestamps in the specified <format>:

notime|short|full|iso

-h, --help display this help and exit

-V, --version output version information and exit

root@ubuntu:/home/philip#

[The whoami command](#contents.xhtml_sc104a)

We can quickly view information about the current user by using the whoami command. The whoami command displays the owner of the current login session. We would say:

root@ubuntu:/home/philip# whoami

root

root@ubuntu:/home/philip#

We can view the available options of the whoami command by passing the --help option:

root@ubuntu:/home/philip# whoami --help

Usage: whoami [OPTION]...

Print the user name associated with the current effective user ID.

Same as id -un.

--help display this help and exit

--version output version information and exit

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>

Full documentation at: <http://www.gnu.org/software/coreutils/whoami>

or available locally via: info '(coreutils) whoami invocation'

root@ubuntu:/home/philip#

We can create a user account in Linux via a GUI utility or the command line. We use the useradd command in the shell to create a new user account. In more recent distributions, there is also the adduser command. In some distributions, adduser is a symbolic link. This can be seen here:

[root@localhost philip]# ll /usr/sbin/adduser

lrwxrwxrwx. 1 root root 7 Jun 20 09:19 /usr/sbin/adduser -> useradd

[root@localhost philip]#

On Ubuntu, the adduser command is separate from the useradd command:

root@ubuntu:/home/philip# ll /usr/sbin/adduser

-rwxr-xr-x 1 root root 37276 Jul 2 2023 /usr/sbin/adduser*

root@ubuntu:/home/philip#

The basic syntax when using the useradd command is:

useradd <option> username

By default, a standard user cannot create a user account. This can be seen as follows:

philip@ubuntu:~$ useradd tom

useradd: Permission denied.

useradd: cannot lock /etc/passwd; try again later.

philip@ubuntu:~$

Based on the above output, we are greeted with a Permission denied message.

Note: Standard users cannot create user accounts.

To create a new user, we will continue as root. Using the root user to create a user would look like this:

root@ubuntu:/home/philip# useradd tom

root@ubuntu:/home/philip#

Based on the above output, we are not given any indication to verify whether the new user was created. Rest assured; we can confirm by looking at the /home directory:

root@ubuntu:/home/philip# cat /etc/passwd

rtkit:x:118:126:RealtimeKit,,,:/proc:/bin/false

saned:x:119:127::/var/lib/saned:/bin/false

usbmux:x:120:46:usbmux daemon,,,:/var/lib/usbmux:/bin/false

philip:x:1000:1000:philip,,,:/home/philip:/bin/bash

gdm:x:121:129:Gnome Display Manager:/var/lib/gdm3:/bin/false

geoclue:x:122:130::/var/lib/geoclue:/bin/false

tom:x:1001:1001::/home/tom:

root@ubuntu:/home/philip#

Some output was omitted for brevity. The last entry displays the new user information. The way we read this is:

tom=user

x=password placeholder

1001=UID

1001=GID

/home/tome=home directory for Tom

However, if we compare entries for another user:

philip:x:1000:1000:philip,,,:/home/philip:/bin/bash

Based on the above, the last part:/bin/bash, defines the shell for the user. The user which we created has not shell assigned. Also, we need to see a password for the user. To set a password, we will use the passwd command:

root@ubuntu:/home/philip# passwd tom

Enter new UNIX password:

Retype new UNIX password:

passwd: password updated successfully

root@ubuntu:/home/philip#

Now, let us log out and try to log in using the tom account. Refer to [Figure 5.1](#ch05.xhtml_fig5-1):

![new user.png](images/Figure_5.1.png)

Figure 5.1: The Linux login screen

We can see the new user appearing, but when we try to log in, the system keeps bouncing us out because we have defined a shell for the user. Let us fix this by removing and adding the user again. We will use the userdel command to remove the user:

root@ubuntu:/home/philip# userdel -r tom

userdel: tom mail spool (/var/mail/tom) not found

userdel: tom home directory (/home/tom) not found

root@ubuntu:/home/philip#

root@ubuntu:/home/philip# cat /etc/passwd

philip:x:1000:1000:philip,,,:/home/philip:/bin/bash

gdm:x:121:129:Gnome Display Manager:/var/lib/gdm3:/bin/false

geoclue:x:122:130::/var/lib/geoclue:/bin/false

root@ubuntu:/home/philip#

Now, let us create the user and pass the -s option. This will define the shell for the user to be used with the useradd command:

root@ubuntu:/home/philip# useradd -s /bin/bash tom

root@ubuntu:/home/philip# cat /etc/passwd:

philip:x:1000:1000:philip,,,:/home/philip:/bin/bash

gdm:x:121:129:Gnome Display Manager:/var/lib/gdm3:/bin/false

geoclue:x:122:130::/var/lib/geoclue:/bin/false

tom:x:1001:1001::/home/tom:/bin/bash

root@ubuntu:/home/philip#

Now we can see in the last entry that the user tom, has been assigned a shell /bin/bash. Another interesting part of the/etc/passwd is the x in each account listed. We said it represents the password, but we have not set x as the password. Let us determine x. It simply denotes that the password is encrypted and stored in a separate location. Namely, the /etc/shadow directory stores the password. We can look at the /etc/shadow directory for reference:

root@ubuntu:/home/philip# cat /etc/shadow

messagebus:*:16911:0:99999:7:::

uuidd:*:16911:0:99999:7:::

lightdm:*:16911:0:99999:7:::

whoopsie:*:16911:0:99999:7:::

avahi-autoipd:*:16911:0:99999:7:::

avahi:*:16911:0:99999:7:::

dnsmasq:*:16911:0:99999:7:::

colord:*:16911:0:99999:7:::

gdm:*:17770:0:99999:7:::

geoclue:*:17770:0:99999:7:::

tom:!:17778:0:99999:7:::

root@ubuntu:/home/philip#

Some output was omitted for brevity. Based on the above output, we can see the actual encrypted password for each account.

[Managing groups](#contents.xhtml_sc105a)

So far, we have been creating user accounts within our system; now, let us talk about group accounts. When we create an account using the useradd command, we are also indirectly creating a group account using the same name as the user. To prove this, let us look at the /etc/login.def:

root@ubuntu:/home/philip# cat /etc/login.defs |grep GRO

# TTYGROUP Login tty will be assigned this group ownership.

# which owns the terminals, define TTYGROUP to the group number and

# TTYPERM to 0620\. Otherwise leave TTYGROUP commented out and assign

TTYGROUP tty

# If USERGROUPS_ENAB is set to "yes", that will modify this UMASK default value

USERGROUPS_ENAB yes

#CONSOLE_GROUPS floppy:audio:cdrom

root@ubuntu:/home/philip#

Based on the above, the variable USERGROUPS_ENAB yes, enables the creation of a group using the same name specified for the username. We can also look at the available groups by looking at the /etc/group:

root@ubuntu:/home/philip# cat /etc/group

pulse-access:x:125:

rtkit:x:126:

saned:x:127:

philip:x:1000:

sambashare:x:128:philip

gdm:x:129:

geoclue:x:130:

tom:x:1001:

root@ubuntu:/home/philip#

Some output was omitted for brevity. Based on the above, a group, tom was created when we created the tom user. However, we can also create a group using another powerful command; the groupadd command. We would:

root@ubuntu:/home/philip# groupadd Hacki

root@ubuntu:/home/philip# cat /etc/group

philip:x:1000:

sambashare:x:128:philip

gdm:x:129:

geoclue:x:130:

tom:x:1001:

Hacki:x:1002:

root@ubuntu:/home/philip#

Now we see our newly created group Hacki being displayed. Likewise, we can remove a group using the groupdel command. We would:

root@ubuntu:/home/philip# groupdel Hacki

root@ubuntu:/home/philip# cat /etc/group

philip:x:1000:

sambashare:x:128:philip

gdm:x:129:

geoclue:x:130:

tom:x:1001:

root@ubuntu:/home/philip#

Great! Now, let's create recreate a group "Hacki":

root@ubuntu:/home/philip# groupadd Hacki

root@ubuntu:/home/philip# cat /etc/group

tom:x:1001:

Hacki:x:1002:

root@ubuntu:/home/philip#

Adding a user to another group is possible using the usermod command. Let us use the user tom. We would:

root@ubuntu:/home/philip# usermod -G Hacki,tom tom

root@ubuntu:/home/philip# cat /etc/group

tom:x:1001:tom

Hacki:x:1002:tom

root@ubuntu:/home/philip#

Now, we can see that the user tom is part of the tom and Hacki groups. Another way to group(s) for a user would be to use the id command. We would say:

root@ubuntu:/home/philip# id tom

uid=1001(tom) gid=1001(tom) groups=1001(tom),1002(Hacki)

root@ubuntu:/home/philip#

Additionally, we can make a group the primary group for a user by passing the -g with the usermod command:

root@ubuntu:/home/philip# usermod -g Hacki tom

root@ubuntu:/home/philip# id tom

uid=1001(tom) gid=1002(Hacki) groups=1002(Hacki) ,1001(tom)

root@ubuntu:/home/philip# cat /etc/group | grep tom

tom:x:1001:

Hacki:x:1002:tom

root@ubuntu:/home/philip#

Based on the above, the only group which the user tom belongs to is the Hacki group. It is also possible to add a password to a group; we would use the gpasswd command. The /etc/gshadow stores each group password. We can look at it:

root@ubuntu:/home/philip# cat /etc/gshadow

philip:!::

sambashare:!::philip

gdm:!::

geoclue:!::

tom:!::tom

Hacki:!::

root@ubuntu:/home/philip#

Some output was omitted for brevity. The exclamation ! means that no password has been set for the respective groups. Let us set a password for the Hacki group:

root@ubuntu:/home/philip# gpasswd Hacki

Changing the password for group Hacki

New Password:

Re-enter new password:

root@ubuntu:/home/philip# cat /etc/gshadow

geoclue:!::

tom:!::tom

Hacki:$6$eOvgO//4tAi/0C$v/FxkZyQLE0BLJ9jfrQ3sElm3kyNbhThl8DFXokZmAWzK1AKQFztSLOBpNsvOESOsWIz6DXKt4Erg.J7ElZut1::tom

root@ubuntu:/home/philip#

Now we can see that hashed version of the password has replaced the exclamation !.

Another command that can be used to create or change a group’s password; the groupmod command. Let us use the groupmod command to assign a password to the tom group:

root@ubuntu:/home/philip# groupmod -p password tom

root@ubuntu:/home/philip# cat /etc/gshadow

gdm:!::

geoclue:!::

tom:password::tom

Hacki:$6$eOvgO//4tAi/0C$v/FxkZyQLE0BLJ9jfrQ3sElm3kyNbhThl8DFXokZmAWzK1AKQFztSLOBpNsvOESOsWIz6DXKt4Erg.J7ElZut1::tom

root@ubuntu:/home/philip#

Based on the above, as opposed to the gpasswd command, it expects an encrypted password when we use the groupmod command. We specified a plain password; hence, we see the password being exposed.

[Password management](#contents.xhtml_sc106a)

Let us take another look at the /etc/passwd file:

root@ubuntu:/home/philip# cat /etc/passwd:

philip:x:1000:1000:philip,,,:/home/philip:/bin/bash

gdm:x:121:129:Gnome Display Manager:/var/lib/gdm3:/bin/false

geoclue:x:122:130::/var/lib/geoclue:/bin/false

tom:x:1001:1001::/home/tom:/bin/bash

root@ubuntu:/home/philip#

Now we can see in the last entry that the user, tom, has been assigned a shell /bin/bash. Another interesting part of the/etc/passwd is the x in each account listed. We said it represents the password, but we have not set x as the password, so the x here simply says that the password is encrypted and stored in a separate location. Namely, the /etc/shadow directory keeps the password. We can look at the /etc/shadow directory for reference:

root@ubuntu:/home/philip# cat /etc/shadow

messagebus:*:16911:0:99999:7:::

uuidd:*:16911:0:99999:7:::

lightdm:*:16911:0:99999:7:::

whoopsie:*:16911:0:99999:7:::

avahi-autoipd:*:16911:0:99999:7:::

avahi:*:16911:0:99999:7:::

dnsmasq:*:16911:0:99999:7:::

colord:*:16911:0:99999:7:::

gdm:*:17770:0:99999:7:::

geoclue:*:17770:0:99999:7:::

tom:!:17778:0:99999:7:::

root@ubuntu:/home/philip#

Some output was omitted for brevity. Based on the above output, we can see the actual encrypted password for each account. Some default information comes from a special configuration file, the /etc/login.def. We can look at the /etc/login.def:

root@ubuntu:/home/philip# cat /etc/login.defs

# /etc/login.defs - Configuration control definitions for the login package.

# Three items must be defined: MAIL_DIR, ENV_SUPATH, and ENV_PATH.

# If unspecified, some arbitrary (and possibly incorrect) value will

SU_NAME su

PASS_MAX_DAYS 99999

PASS_MIN_DAYS 0

PASS_WARN_AGE 7

root@ubuntu:/home/philip#

Some output omitted for brevity. We can see settings for the su and chage commands based on the above.

[The usermod command](#contents.xhtml_sc107a)

Earlier, we saw in order to make any changes we would have to remove the user with the useradd command. This can be cumbersome every time we decide on a change; instead, we can leverage another powerful command, the usermod command. The basic syntax of the usermod command is:

usermod <option> username

Using our test user tom, we can change several parameters with the usermod command. For example, we can lock the account for the user tom, this will prevent the user tom from being able to logging in to the system. To lock an account, we would use the -L option:

root@ubuntu:/home/philip# cat /etc/passwd

philip:x:1000:1000:philip,,,:/home/philip:/bin/bash

gdm:x:121:129:Gnome Display Manager:/var/lib/gdm3:/bin/false

geoclue:x:122:130::/var/lib/geoclue:/bin/false

tom:x:1001:1001::/home/tom:

root@ubuntu:/home/philip# usermod -L tom

root@ubuntu:/home/philip#

Refer to [Figure 5.2](#ch05.xhtml_fig5-2):

![lockaccount.png](images/Figure_5.2.png)

Figure 5.2: Switching users using the su command

The user tom is unable to log in. An interesting point to note is the entry for the user tom inside the /etc/shadow shows an ! in front of the password in the second field, which represents the password.

root@ubuntu:/home/philip# cat /etc/shadow | grep tom

tom:!$6$uJ52BA2n$SWGisIpNTTOSygIX6swWdkS/gLPGZacEzCz2Ht6qfUHIr7ZIxkJyUjEyqN9ncb1yIFIXYnePz4HVzrwqJA1DZ0:17778:0:99999:7:::

root@ubuntu:

root@ubuntu:/home/philip# cat /etc/shadow | grep philip

philip:$1$8gQrKziP$v6Uv6

root@ubuntu:/home/philip#

There is no ! in front of the password for the user philip. Another way to verify whether an account has been locked is to use the passwd command. We would pass the --status option:

root@ubuntu:/home/philip# passwd --status tom

tom L 09/04/2023 0 99999 7 -1

root@ubuntu:/home/philip#

The L indicates that the user account is currently locked. We can unlock the user account by using the usermod command and passing the -U option:

root@ubuntu:/home/philip# usermod -U tom

root@ubuntu:/home/philip# passwd --status tom

tom P 09/04/2023 0 99999 7 -1

root@ubuntu:/home/philip#

The P indicates that the user tom has a usable password; this implies that the account is unlocked. Refer to [Figure 5.3](#ch05.xhtml_fig5-3):

![accountunlocked.png](images/Figure_5.3.png)

Figure 5.3: The passwd command with the --status option

Now, when we look at the /etc/shadow once again, we will no longer see the ! in front of the hashed password:

root@ubuntu:/home/philip# cat /etc/shadow | grep tom

tom:$6$uJ52BA2n$SWGisIpNTTOSygIX6swWdkS/gLPGZacEzCz2Ht6qfUHIr7ZIxkJyUjEyqN9ncb1yIFIXYnePz4HVzrwqJA1DZ0:17778:0:99999:7:::

root@ubuntu:/home/philip#

We can also define a shell for a user if we add a user without specifying a shell; we would pass the -s option with the usermod command:

root@ubuntu:/home/philip# cat /etc/passwd

gdm:x:121:129:Gnome Display Manager:/var/lib/gdm3:/bin/false

geoclue:x:122:130::/var/lib/geoclue:/bin/false

tom:x:1001:1001::/home/tom:

root@ubuntu:/home/philip# usermod -s /bin/bash tom

root@ubuntu:/home/philip# cat /etc/passwd

gdm:x:121:129:Gnome Display Manager:/var/lib/gdm3:/bin/false

geoclue:x:122:130::/var/lib/geoclue:/bin/false

tom:x:1001:1001::/home/tom:/bin/bash

root@ubuntu:/home/philip#

Another method for locking an account would be to use the passwd command; we would pass the -l option. Let us lock the user tom:

root@ubuntu:/home/philip# passwd -l tom

passwd: password expiry information changed.

root@ubuntu:/home/philip# passwd --status tom

tom L 09/04/2023 0 99999 7 -1

root@ubuntu:/home/philip#

Once again, when we try to log in as the user tom, we will get the result as depicted in [Figure 5.4](#ch05.xhtml_fig5-4):

![tomunable.png](images/Figure_5.4.png)

Figure 5.4: Locking a user account using the passwd command with the -l option

Also, we can unlock an account using the passwd command; we would pass the -u option:

root@ubuntu:/home/philip# passwd -u tom

passwd: password expiry information changed.

root@ubuntu:/home/philip# passwd --status tom

tom P 09/04/2023 0 99999 7 -1

root@ubuntu:/home/philip#

Please note that the root user can still log in using the tom user. We can illustrate this by locking the user tom once again:

root@ubuntu:/home/philip# passwd -l tom

passwd: password expiry information changed.

root@ubuntu:/home/philip# passwd --status tom

tom L 09/04/2023 0 99999 7 -1

root@ubuntu:/home/philip# cat /etc/shadow | grep tom

tom:!$6$uJ52BA2n$SWGisIpNTTOSygIX6swWdkS/gLPGZacEzCz2Ht6qfUHIr7ZIxkJyUjEyqN9ncb1yIFIXYnePz4HVzrwqJA1DZ0:17778:0:99999:7:::

root@ubuntu:/home/philip#

Based on the above, from all indications, it seems that the user tom account has been disabled, but let us consider [Figure 5.5](#ch05.xhtml_fig5-5):

![rootcantom.png](images/Figure_5.5.png)

Figure 5.5: Locking a user account using the passwd command with the -l option

Here is what happened, when someone tries to log in as the user tom, they will be prevented unless they first become the root user because the lock does not prevent the root from accessing the locked account.

| Note: | The root user can access any account. |

[Chage](#contents.xhtml_sc108a)

Another interesting aspect regarding user accounts involves the aging time for a password, and the expiration for a password. We can view the expiration for a given user by using the chage command. Let us create a password for the user tom and then check the password aging settings for the new user:

| Note: | You must have root privileges to change the password aging parameters. |

root@ubuntu:/home/philip# passwd tom

Enter new UNIX password:

Retype new UNIX password:

passwd: password updated successfully

root@ubuntu:/home/philip#

Refer to [Figure 5.6](#ch05.xhtml_fig5-6):

![chage.png](images/Figure_5.6.png)

Figure 5.6: The chage command with the -l option

We can see several valuable pieces of information. Notably, Last password change, Password expires, and Account expires. We can change these values by passing various options. For instance, let us change the Account expires. We would use the -E option:

root@ubuntu:/home/philip# chage -E 2023-09-04 tom

root@ubuntu:/home/philip# chage -l tom

Last password change : Sep 04, 2023

Password expires : never

Password inactive : never

Account expires : Sep 04, 2023

Minimum number of days between password change : 0

Maximum number of days between password change : 99999

Number of days of warning before password expires : 7

root@ubuntu:/home/philip#

We have set the account to expire at the current time of this demo. Now, to see the effects of this change, we will open another terminal and try to log in as the user tom.

Refer to [Figure 5.7](#ch05.xhtml_fig5-7):

![chageautherror.png](images/Figure_5.7.png)

Figure 5.7: The chage command with the -E option

Based on the above, we see the message returned while attempting to log in as the user tom. To remove this expiration for the user tom, we would use a -1 as the value:

root@ubuntu:/home/philip# chage -E -1 tom

root@ubuntu:/home/philip# chage -l tom

Last password change : Sep 04, 2023

Password expires : never

Password inactive : never

Account expires : never

Minimum number of days between password change : 0

Maximum number of days between password change : 99999

Number of days of warning before password expires : 7

root@ubuntu:/home/philip#

Now, we will be able to log in as the user tom.

Refer to [Figure 5.8](#ch05.xhtml_fig5-8):

![chagelogin.png](images/Figure_5.8.png)

Figure 5.8: The chage command with the -E option

We can see the effectiveness of using the chage command. To see the available options which can be passed with the chage command, we can do:

root@ubuntu:/home/philip# chage

Refer to [Figure 5.9](#ch05.xhtml_fig5-9):

![chageoptions.png](images/Figure_5.9.png)

Figure 5.9: The chage command with available options

[Conclusion](#contents.xhtml_sc109a)

In this chapter, our focus was user and password management. We covered various ways to manage users, groups, and passwords.

In the next chapter, we continue our journey in security, particularly, Firewalls, remote access, and SELinux.

[References](#contents.xhtml_sc110a)

*   This site gives helpful information about /etc/skel: [https://unix.stackexchange.com](https://unix.stackexchange.com)
*   This site gives useful information about user account creation: [http://www.linfo.org](http://www.linfo.org)
*   This site gives useful information about various groups: [http://www.linuxguide.it](http://www.linuxguide.it)

Join our book’s Discord space

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 6Firewall, Remote Access and SELinux](#contents.xhtml_ch06a)

[Introduction](#contents.xhtml_sc111a)

In the last chapter, we focused on user and password management. This chapter will continue looking at security, emphasizing Firewalls, remote access, and SELinux. First, we will focus on TCP wrappers; also known as hosts.allow and hosts.deny, which are access control mechanisms that provide an additional layer of security for network services running on a Linux system. Next, our focus will be setting remote access with ssh; It allows users to establish encrypted and authenticated connections over a network, enabling secure command-line access, remote administration, file transfers, and other services. Finally, the focus will be SELinux, a security framework and access control mechanism implemented in the Linux kernel.

[Structure](#contents.xhtml_sc112a)

In this chapter, we will discuss the following topics:

*   Firewalls
*   iptables
*   Remote access
*   SELinux

[Objectives](#contents.xhtml_sc113a)

In this chapter, we will focus on learning various security configurations. Firstly, we will explore the configuration of TCP wrappers, which enables us to control access to different services by allowing or restricting it. Additionally, we will delve into the process of configuring firewalld and iptables, both of which are essential tools for managing network access and controlling different levels of access. Furthermore, we will cover the configuration of SSH, an important protocol for remote management. Lastly, we will discuss the configuration of SELinux, a powerful security mechanism for enforcing access controls and preventing unauthorized activities.

[Firewalls](#contents.xhtml_sc114a)

A Linux firewall is a software-based network security system that monitors and controls network traffic based on predefined rules. It acts as a barrier between a computer or network and the external world, protecting the system from unauthorized access and potential threats. Theoretically, a Linux firewall follows principles and mechanisms to provide network security. Let us explore these aspects in detail:

*   Packet filtering: The fundamental function of a Linux firewall is packet filtering, which involves inspecting individual network packets and deciding whether to allow or block them based on predefined rules. Each packet contains information such as source and destination IP addresses, port numbers, and protocol type. Using this information, the firewall can make filtering decisions.
*   Rules: Firewall rules are the instructions that dictate how packets should be handled. The system administrator defines these rules and can be modified as needed. Each rule typically specifies certain criteria, such as source and destination IP addresses, port numbers, and protocol types, and defines an action to be taken, such as allow or block. Rules are processed in sequential order, and the first matching rule is applied to the packet.
*   Rule chains: To organize and manage firewall rules effectively, Linux firewalls use rule chains. Rule chains are logical groups of rules applied in a specific order. Commonly used chains include the input chain (for incoming packets), the output chain (for outgoing packets), and the forward chain (for packets being routed between interfaces). Each chain can have multiple rules processed in the order defined within the chain.
*   Stateful inspection: Besides packet filtering, Linux firewalls often employ stateful inspection. This mechanism allows the firewall to track the state of network connections and make decisions based on the context of the traffic flow. By maintaining a record of established connections, the firewall can permit incoming packets that are part of an existing, legitimate connection while blocking unsolicited connection attempts.
*   Network Address Translation (NAT): NAT is a technique firewalls use to modify IP addresses and port numbers in network packets. It allows multiple devices within a private network to share a single public IP address. Linux firewalls can perform various types of NAT, such as Source NAT (SNAT) and Destination NAT (DNAT), to translate addresses and facilitate communication between network segments.
*   Logging and auditing: Linux firewalls often provide logging and auditing capabilities to monitor and analyze network activity. These features allow administrators to record relevant information about packets allowed or blocked by the firewall. Logs can include details like source and destination IP addresses, port numbers, timestamps, and firewall rule matches. Administrators can identify potential security incidents or troubleshoot network issues by reviewing logs.
*   Additional security mechanisms: Linux firewalls can incorporate additional security mechanisms to enhance network protection. Some examples include Intrusion Detection Systems (IDS) or Intrusion Prevention Systems (IPS) that detect and block suspicious network traffic, and Virtual Private Network (VPN) support for secure remote access.
*   Firewall zones and interfaces: Linux firewalls often implement the concept of zones and interfaces to define network segments and their associated firewall rules. A zone represents a group of network interfaces that have similar security requirements. Each zone has its rules, allowing fine-grained control over traffic between different zones. Interfaces are associated with specific zones, and packets are processed based on the rules defined for the respective zone.
*   Application-level filtering: Besides packet filtering, Linux firewalls can perform application-level filtering, also known as Deep Packet Inspection (DPI). This technique involves inspecting the contents of network packets at the application layer to identify and block specific protocols, applications, or content types. DPI can provide more granular control and protection against application-level threats.

Overall, a Linux firewall combines packet filtering, stateful inspection, network address translation, and other security mechanisms to create a barrier between networks and control traffic flow. A Linux firewall helps protect systems and networks from unauthorized access, network attacks, and other security risks by defining and enforcing rules.

[TCP wrappers](#contents.xhtml_sc115a)

We can add another layer of security within a Linux system by using the TCP wrappers. They provide traffic filtering as it enters the system; the TCP wrappers check traffic against 2 files: the /etc/hosts.allow and /etc/hosts.deny. The rules are applied from a top-down approach; meaning the first rule always applied above all other rules. We can view the contents of the /etc/hosts.allow as shown below:

| Note: | You will require administrative privileges or become the root user to access the TCP wrappers configuration file. |

[philip@localhost ~]$ cat /etc/hosts.allow

#

# hosts.allow This file contains access rules which are used to

# allow or deny connections to network services that

# either use the tcp_wrappers library or that have been

# started through a tcp_wrappers-enabled xinetd.

# See 'man 5 hosts_options' and 'man 5 hosts_access'

# for information on rule syntax.

# See 'man tcpd' for information on tcp_wrappers

#

[philip@localhost ~]$

Based on the above, the file only contains comments which start with #. The basic syntax for creating a rule is as follows:

<daemon>: <client list> [:<option>: <option>:…]

Based on the above, we could add a rule using a text editor such as vi or nano as shown below:

[philip@localhost ~]$ sudo cat /etc/hosts.allow

#

vsftpd: 172.16.175.

[philip@localhost ~]$

Based on the above, we have added a rule for the vsftpd; this is a secure version of FTP. We then specified the client list; in this case, we specified the subnet 172.16.175., the . means any IP addresses within that subnet can access the vsftpd. Another way to define the rule is by specifying a domain as shown below:

[philip@localhost ~]$ sudo cat /etc/hosts.allow

#

vsftpd: .bpbonline.com

[philip@localhost ~]$

Anyone within the .bpbonline.com can access the vsftpd on the local system. Adding to this, we can use the keyword ALL inside a rule; this match everything, it could be placed at the daemon, or the client list section as shown below:

[philip@localhost ~]$ sudo cat /etc/hosts.allow

vsftpd: .bpbonline.com

in.telnetd: ALL

[philip@localhost ~]$

Everyone can access the telnet service on the local system. It is also possible to execute another command by passing the spawn option. This is useful when we want to log who attempts to access a service on the local system. This is how we would use the spawn option:

[philip@localhost ~]$ sudo cat /etc/hosts.allow

vsftpd: .bpbonline.com: spawn /bin/echo `/bin/date` from %h>>/var/log/vsftp.log : allow

in.telnetd: ALL

[philip@localhost ~]$

We use the spawn option; this then creates a message containing the current date (/bin/date) which is then appended with the hostname (%h) of the system attempting to access the vsftpd; this then gets appended inside the /var/log/vsftp.log. We can then look at the /etc/hosts.deny file as shown below:

[philip@localhost ~]$ sudo cat /etc/hosts.deny

# hosts.deny This file contains access rules which are used to

# deny connections to network services that either use

# the tcp_wrappers library or that have been

# The rules in this file can also be set up in

# /etc/hosts.allow with a 'deny' option instead.

# See 'man 5 hosts_options' and 'man 5 hosts_access'

# for information on rule syntax.

# See 'man tcpd' for information on tcp_wrappers

[philip@localhost ~]$

Based on the above, the /etc/hosts.deny only contains comments #. It is recommended to deny everything in this file as shown below:

[philip@localhost ~]$ sudo cat /etc/hosts.deny

ALL:ALL

[philip@localhost ~]$

We have specified ALL:ALL:,  this means to deny everything except the rules which are listed in the /etc/hosts.allow.

[firewalld](#contents.xhtml_sc116a)

firewalld is a dynamic firewall management tool designed for Linux distributions. It provides an easy-to-use interface for configuring and managing firewall rules and network zones. In this chapter, we will explore the details of firewalld, its features, components, and usage examples. It is a firewall management solution that replaces the traditional iptables framework in many Linux distributions. It offers a higher-level abstraction for managing firewall rules and simplifies the process of configuring network zones and services.

[firewalld features](#contents.xhtml_sc117a)

firewalld offers several key features that make it a valuable tool for firewall management. They are as follows:

*   Dynamic updates: It allows real-time updates to firewall rules without restarting the firewall service or disrupting existing connections.
*   Network zones: It categorizes networks into different zones, such as public, internal, and trusted, allowing different firewall rules to be applied based on network trust levels.
*   Rich rule set: It supports a rich set of predefined rules for various services and protocols, simplifying the configuration of common firewall rules.
*   Interface management: It allows the assignment of network interfaces to specific zones, providing granular control over network access.
*   D-Bus interface: It provides a D-Bus interface that allows other applications and tools to interact, making it easily extensible and integrable with other system components.

[firewalld components](#contents.xhtml_sc118a)

Let us discuss the firewalld components in detail.

*   firewalld service: The firewalld service is the core component of firewalld. It manages the firewall rules, network zones, and interfaces. The service can be controlled using the firewall-cmd command-line tool or graphical interfaces like firewall-config.
*   Zones: firewalld organizes networks into different zones based on their trust levels. Each zone has its own set of firewall rules. Some common predefined zones include public, internal, trusted, and block. Administrators can also create custom zones to suit their specific network configurations.
*   Services: firewalld defines services as predefined configurations that allow or block network traffic for specific services or applications. Services can be enabled or disabled, and they automatically set the appropriate firewall rules to allow or deny the associated traffic.
*   Network interfaces: firewalld associates network interfaces with specific zones to control network traffic. Administrators can define the firewall rules that apply to different networks and interfaces by assigning interfaces to zones.

[firewalld usage examples](#contents.xhtml_sc119a)

Let us explore some practical examples to understand how firewalld can be used:

*   Enabling and disabling firewalld
    *   To start the firewalld service, use the following command:

        $ sudo systemctl start firewalld

    *   To stop the firewalld service, use:

        $ sudo systemctl stop firewalld

*   Listing available zones

    *   To list the available zones in firewalld, execute the following command:

        $ sudo firewall-cmd --get-zones

    This command displays a list of zones defined in firewalld, such as public, internal, and trusted.

*   Assigning an interface to a zone
    *   To associate a network interface with a specific zone, use the --zone option with the --change-interface flag:

        $ sudo firewall-cmd --zone=public --change-interface=INTERFACE_NAME

Note: Replace INTERFACE_NAME with the actual interface name.

[iptables](#contents.xhtml_sc120a)

In the world of Linux, iptables is a powerful tool for network traffic control and firewall configuration. Understanding iptables is essential for securing network connections, managing packet filtering, and implementing network address translation. This chapter explains iptables, its components, and practical examples to illustrate its usage.

[Understanding iptables](#contents.xhtml_sc121a)

iptables is a command-line utility in Linux that allows administrators to configure the Linux kernel’s packet filtering rules and Network Address Translation (NAT). It provides a robust framework for managing network traffic, implementing firewall rules, and securing the network.

[iptables components](#contents.xhtml_sc122a)

iptables consists of several components, including:

*   Tables: iptables uses different tables to organize and categorize rules. The commonly used tables are filtered for packet filtering, NAT for network address translation, and mangle for specialized packet alterations.
*   Chains: Chains are a sequence of rules within a table that packets traverse. They define the processing flow for incoming and outgoing packets. The three built-in chains are INPUT (incoming packets to the local system), OUTPUT (outgoing packets from the local system), and FORWARD (packets routed through the system).
*   Rules: Rules define the criteria for packet matching and the corresponding actions to be taken. They specify conditions such as source/destination IP addresses, port numbers, protocols, and the action to be performed, such as accepting, dropping, or forwarding packets.

[iptables rule syntax](#contents.xhtml_sc123a)

The syntax for an iptables rule follows the general format:

iptables -A <chain> -p <protocol> --source <source> --destination <destination> --dport <port> -j <action>

Below are the various options which can be passed to iptables:

*   -A: Appends the rule to the specified chain.
*   -p: Specifies the protocol (for example, TCP, UDP).
*   --source: Specifies the source IP address or network.
*   --destination: Specifies the destination IP address or network.
*   --dport: Specifies the destination port number.
*   -j: Specifies the action to be taken (for example, ACCEPT, DROP, LOG).

[iptables examples](#contents.xhtml_sc124a)

Let us explore some practical examples to understand how iptables can be used:

*   Blocking Incoming HTTP Traffic:

To block incoming HTTP traffic (port 80), use the following command:

$ sudo iptables -A INPUT -p tcp --dport 80 -j DROP

This rule appends a DROP action to the INPUT chain, preventing TCP traffic on port 80.

*   Setting up NAT

To configure NAT and enable internet connection sharing, execute the following commands:

$ sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

$ sudo echo 1 > /proc/sys/net/ipv4/ip_forward

The first command appends a rule to the POSTROUTING chain in the NAT table, enabling masquerading. The second command enables IP forwarding.

*   Managing iptables rules

    *   Listing iptables rules:

    To view the current iptables rules, use the following command:

    $ sudo iptables -L

    This command lists all the rules in each chain of the filter table.

    *   Clearing iptables rules:

    To remove all iptables rules, execute the following commands:

    $ sudo iptables -F

    $ sudo iptables -X

    $ sudo iptables -t nat -F

    $ sudo iptables -t nat -X

    $ sudo iptables -t mangle -F

    $ sudo iptables -t mangle -X

    These commands flush (-F) and delete (-X) all rules in each table, ensuring a clean slate.

iptables is a powerful tool for managing network traffic, implementing firewall rules, and securing Linux systems. This chapter provided a detailed explanation of iptables, its components, and syntax. By mastering iptables, administrators can effectively control network traffic, enhance network security, and implement various network-related configurations.

[Remote access](#contents.xhtml_sc125a)

Remote access with Secure Shell (SSH) in Linux allows users to establish secure and encrypted connections to manage and access Linux systems remotely. SSH provides a secure command-line interface and enables secure file transfers, remote administration, and tunneling of network connections. Remote access with SSH in Linux provides a secure and efficient method for remotely managing and accessing Linux systems. SSH ensures the confidentiality and integrity of data transmitted over the network by employing encryption, authentication, and secure communication protocols.

[SSH](#contents.xhtml_sc126a)

Let us discuss the SSH protocol and its security measures in detail:

*   SSH protocol: SSH is a cryptographic network protocol that provides secure client and server communication. It uses strong encryption algorithms to protect the confidentiality and integrity of data transmitted over the network. SSH ensures secure authentication, secure remote command execution, and secure file transfers.
*   SSH client and server: SSH operates using the SSH client and the SSH server. The SSH client is the program the user uses to initiate a connection to a remote server. The SSH server is installed on the remote Linux system and listens for incoming SSH connection requests. It provides authentication, encryption, and other services required for secure remote access.
*   Authentication methods: SSH supports various authentication methods to verify the client’s identity connecting to the remote server. These methods include:
*   Password authentication: The client provides a username and password to authenticate with the SSH server. This method is commonly used but can be less secure if weak passwords are used.
*   Public key authentication: Public key authentication uses asymmetric cryptography. The client generates a key pair consisting of a public and private key. The public key is uploaded to the remote server, while the private key is securely stored on the client. During authentication, the client proves ownership of the private key by signing a challenge from the server using the corresponding public key. This method offers stronger security and is often preferred.
*   Two-Factor Authentication (2FA): SSH can integrate with additional authentication mechanisms, such as one-time passwords or hardware tokens, to provide an extra layer of security. This requires the user to provide a password and a secondary authentication factor.
*   Connection encryption: SSH ensures the confidentiality and integrity of data transmitted between the client and server by encrypting the entire SSH connection. Encryption prevents unauthorized access to sensitive information and protects against eavesdropping and tampering. SSH supports various encryption algorithms, and the client and server negotiate the encryption algorithm and parameters during the connection establishment.
*   Terminal and command execution: Once the SSH connection is established, the client can interact with the remote server’s Command-Line Interface (CLI). The client sends commands to the server, which executes them and returns the output to the client. This allows users to manage Linux systems remotely, run administrative tasks, and execute commands as if physically on the server.
*   File transfer: SSH also provides secure file transfer capabilities. The most common tool for SSH-based file transfer is the Secure Copy (SCP) command, which allows users to copy files between local and remote systems securely. Another popular tool is the Secure File Transfer Protocol (SFTP), which provides a more feature-rich and interactive file transfer experience.
*   Port forwarding: SSH supports port forwarding, also known as SSH tunneling, which enables users to securely tunnel network connections over an SSH connection. Port forwarding allows accessing services on remote systems as if running locally, bypassing network restrictions and enhancing security. It can be used for various purposes, such as accessing remote databases, securing remote VNC or RDP connections, or creating VPN-like tunnels.
*   Security measures: To enhance the security of SSH remote access, it is recommended to follow best practices such as:
*   Regularly updating the SSH server and client software to address security vulnerabilities.
*   Disabling SSH protocol versions (for example, SSHv1) that are less secure.
*   Using strong, unique passwords or employing public key authentication for user authentication.
*   Limiting SSH access to trusted networks or specific IP addresses through firewall rules or TCP wrappers.
*   Monitoring SSH logs for suspicious activities or unauthorized access attempts.

Most Linux distribution comes with the SSH package installed by default. To verify whether SSH is currently running or not, we can use the systemctl command; we would pass the status option as shown below in [Figure 6.1](#ch06.xhtml_fig6-1):

![A screenshot of a computer Description automatically generated](images/Figure_6.1.png)

Figure 6.1: systemctl command with the status option

Based on the above, the ssh daemon ssh.service is running, particularly the secure shell server. Another method we can use to verify that the SSH service is running using the netstat command; we would pass the ntlp options (n-display port numbers, t-TCP protocol, l-currently listening, p- program ID/program name) as shown below:

root@Linuxplus:/home/philip# netstat -ntlp

Active Internet connections (only servers)

Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name

tcp 0 0 0.0.0.0:514 0.0.0.0:* LISTEN 519/rsyslogd

tcp 0 0 127.0.0.53:53 0.0.0.0:* LISTEN 431/systemd-resolve

tcp 0 0 0.0.0.0:22 0.0.0.0:* LISTEN 1152/sshd

tcp 0 0 127.0.0.1:631 0.0.0.0:* LISTEN 2638/cupsd

tcp6 0 0 :::514 :::* LISTEN 519/rsyslogd

tcp6 0 0 :::22 :::* LISTEN 1152/sshd

tcp6 0 0 ::1:631 :::* LISTEN 2638/cupsd

root@Linuxplus:/home/philip#

The SSH server daemon is running on TCP port 22 based on the above. The basic syntax for establishing a connection to a remote system is:

ssh <remote system>

Based on the above, we can simply run the ssh command and pass only the remote system; we will use the ssh command from the Fedora system and try to connect to the Ubuntu system as shown below:

[philip@localhost ~]$ ssh 172.16.175.130

The authenticity of host '172.16.175.130 (172.16.175.130)' can't be established.

ECDSA key fingerprint is SHA256:SfI3vfS3yRRWSGN2jgAG7K5aQc65c/zVt/lz+D8mQBQ.

ECDSA key fingerprint is MD5:a2:03:c5:38:b3:83:88:fa:85:b5:5f:e6:91:eb:87:c1.

Are you sure you want to continue connecting (yes/no)?yes

Warning: Permanently added '172.16.175.130' (ECDSA) to the list of known hosts.

philip@172.16.175.130's password:

Welcome to Ubuntu LTS

* Documentation: https://help.ubuntu.com

* Management: https://landscape.canonical.com

* Support: https://ubuntu.com/advantage

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by

applicable law.

philip@Linuxplus:~$

Some output was omitted for brevity. Based on the above, without specifying any option, the SSH program used the current user philip; adding to this, a fingerprint identifying the server was presented. This added the server to user’s philip ~/.ssh/known_hosts in the Fedora system. We can look at this file as shown below:

[philip@localhost ~]$ cat .ssh/known_hosts

172.16.175.130 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBPhEHNo6YSOE+ZZ9vHVmQqBPFQd8WtAUFoGYAJe3VPQJlhjhc9bxy+vwsetQiEIKTyMgnfrOC7LNbhxxmJ4IX8w=

[philip@localhost ~]$

Based on the above, we the Ubuntu’s system information inside the ~/.ssh/known_hosts for the user philip on the Fedora system. It is also possible to use a different username with the ssh command; we would specify the -l option as shown below:

[philip@localhost ~]$ ssh -l hacker 172.16.175.130

hacker@172.16.175.130's password:

Welcome to Ubuntu LTS

$ exit

Connection to 172.16.175.130 closed.

[philip@localhost ~]$

Based on the above, we could log in using a different user via SSH. Also, notice we were presented with the earlier message identifying the server’s fingerprint. The information was previously stored in the ~/.ssh/known_hosts. If we were to remove the contents using a text editor such as vi or nano then we would be presented with the identity message once again as shown below:

[philip@localhost ~]$ cat .ssh/known_hosts

[philip@localhost ~]$

[philip@localhost ~]$ ssh -l hacker 172.16.175.130

The authenticity of host '172.16.175.130 (172.16.175.130)' can't be established.

ECDSA key fingerprint is SHA256:SfI3vfS3yRRWSGN2jgAG7K5aQc65c/zVt/lz+D8mQBQ.

ECDSA key fingerprint is MD5:a2:03:c5:38:b3:83:88:fa:85:b5:5f:e6:91:eb:87:c1.

Are you sure you want to continue connecting (yes/no)? yes

Warning: Permanently added '172.16.175.130' (ECDSA) to the list of known hosts.

hacker@172.16.175.130's password:

Welcome to Ubuntu LTS

[philip@localhost ~]$

We removed the contents and were once again presented with the identity message. So far, we have been prompted to enter a password whenever we attempt to start an SSH session. However, bypassing the password prompt and logging in to the system successfully without any hindrance is possible. We would use SSH keys to authenticate, known as key-based authentication. The key-based authentication involves the creation of a pair of keys, a private key, and a public key. The private key is stored on the client’s system, and the public key is stored on the destination system(s). We would generate an SSH key using the ssh-keygen command on the destination system. Next, we would need to copy over the client system; we can use the ssh-copy-id command to copy the keys. When you first connect using key-based authentication, the servers transmit a message using the public key over to the client’s system, which then can be read and interpreted using the private key which resides on the client’s system. Let us first generate the SSH keys using the ssh-keygen command on the client system from where we want to login in; it will be the Fedora for us, as shown below:

[philip@localhost ~]$ ssh-keygen

Generating public/private rsa key pair.

Enter file in which to save the key (/home/philip/.ssh/id_rsa):

Based on the above, by default, the algorithm is rsa, and the location to store the key pair is inside the current user’s home directory (~/.ssh/id_rsa). We will accept the defaults and press Enter as shown below:

[philip@localhost ~]$ ssh-keygen

Generating public/private rsa key pair.

Enter file in which to save the key (/home/philip/.ssh/id_rsa):

Enter passphrase (empty for no passphrase):

Enter same passphrase again:

Based on the above, we would need to specify a passphrase. We will use a super-secret passphrase and then press Enter  as shown below:

[philip@localhost ~]$ ssh-keygen

Generating public/private rsa key pair.

Enter file in which to save the key (/home/philip/.ssh/id_rsa):

Enter passphrase (empty for no passphrase):

Enter same passphrase again:

Your identification has been saved in /home/philip/.ssh/id_rsa.

Your public key has been saved in /home/philip/.ssh/id_rsa.pub.

The key fingerprint is:

SHA256:BwdFiHu2iEyvnnXhnY+1tNpZmlaZZdL1Zugwda9PJ7g philip@localhost.localdomain

The key's randomart image is:

+---[RSA 2048]----+

| ..+o |

| . .. . o|

| .. . . ++|

| . . oo o o O|

| o o +S.. = X |

| o o..+ .. B o|

| .. o o oo.+.|

| .o . *EB .|

| .o ooO |

+----[SHA256]-----+

[philip@localhost ~]$

Based on the above, the key was generated using a key size of 2048 bits. Now, we can run the ls command on the user’s home directory and look inside the ~/.ssh as shown below:

[philip@localhost ~]$ ls -a .ssh

. .. id_rsa id_rsa.pub known_hosts

[philip@localhost ~]$

Apart from the known_hosts file, which we covered earlier, we now have two dditional files; the id_rsa, this is the private key and the id_rsa.pub, this is the public key. We can look at the content cat using the cat command:

[philip@localhost ~]$ cat ~/.ssh/id_rsa.pub

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDNvsCDZaUs6mralW+c1QnQ9cMeUqW0c/4IF8DThVK0Bi4CPnQApafJZrOyeQeJbLxORCJf+YlkE+DWREwJw0EU21PkiZeij0DEIlspqToo6BkKDPfXXCl35OQxSUXERlAhGQQpVSbEJLy0WZsbs6iAy4ohmKcCWeEdHLz/3p0Vuyd3NhvXaLsyno/Qa2ZOBOOZgwUeHUA/p0zykUff7M4kIyGYatt1/vYKDH+UOC5fyB/nLtvrq7P1MrlfMGyEjtc7nFDEHz4VeAP1iUItKEzsyrqEH/KbAa3/ZeSoSfaFxoKvEtSKF5tnICyVp6uiUTNfi/cN74dmiDfG+vtcF0nt philip@localhost.localdomain

[philip@localhost ~]$

The next step would be to copy the public key from the client’s system over to the destination server using the ssh-copy id command; in our case the server is the Ubuntu system as below:

Before we run the ssh-copy-id command, let us check the ~/.ssh directory on the Ubuntu system:

philip@Linuxplus:~$ ls -a ~/.ssh

. ..

philip@Linuxplus:~$

Based on the above, the ~/.ssh is currently empty. Now let us execute the ssh-copy-id command on the client system:

[philip@localhost ~]$ ssh-copy-id philip@172.16.175.130

/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/philip/.ssh/id_rsa.pub"

/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed

/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys

philip@172.16.175.130's password:

Number of key(s) added: 1

Now try logging into the machine, with: "ssh 'philip@172.16.175.130'"

and check to make sure that only the key(s) you wanted were added.

[philip@localhost ~]$

Based on the above, the public key ~/.ssh/id_rsa.pub was successfully transferred to the server’s system. Now let us check the ~/.ssh directory on the Ubuntu system once again:

philip@Linuxplus:~$ ls -a ~/.ssh

. .. authorized_keys

philip@Linuxplus:~$

We now have an authorized_keys file located in the ~/.ssh directory. We can use the cat command and verify that the public key is indeed the same as the public key on the client’s system:

philip@Linuxplus:~$ cat ~/.ssh/authorized_keys

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDNvsCDZaUs6mralW+c1QnQ9cMeUqW0c/4IF8DThVK0Bi4CPnQApafJZrOyeQeJbLxORCJf+YLkE+DWREwJw0EU21PkiZeij0DEIlspqToo6BkKDPfXXCl35OQxSUXERlAhGQQpVSbEJLy0WZsbs6iAy4ohmKcCWeEdHLz/3p0VUyd3NHvXaLsyno/Qa2ZOBOOZgwUeHUA/p0zykUff7M4kIyGYatt1/vYKDH+UOC5fyB/nLtvrq7P1MrlfMGyEjtc7nFDEHz4VeAP1iUItKEzsyrqEH/KbAa3/ZeSoSfaFxoKvEtSKF5tnICyVp6uiUTNfi/cN74dmiDfG+vtcF0nt philip@localhost.localdomain

philip@Linuxplus:~$

The last step would be to run the ssh command on the client system (Fedora) and verify that we can log in to the server (Ubuntu) without using a password, as shown below:

[philip@localhost ~]$ ssh 172.16.175.130

Enter passphrase for key '/home/philip/.ssh/id_rsa':

Welcome to Ubuntu LTS

Last login: Thu Sep 13 16:47:50 2023 from 172.16.175.129

philip@Linuxplus:~$

Based on the above, we were asked for the passphrase,  not the user’s password. Furthermore, storing the passphrase inside an agent would allow us to log in seamlessly in the future without having to provide the passphrase each time we attempt to login; this is possible by using the ssh-agent and ssh-add commands. The ssh agent stores the passphrase after we would have used the ssh-add command. This creates what is known as a Single Sign-on (SSO). Here is how we would use the ssh-add command as shown below:

[philip@localhost ~]$ ssh-agent

SSH_AUTH_SOCK=/tmp/ssh-qLovqqH69q1D/agent.79449; export SSH_AUTH_SOCK;

SSH_AGENT_PID=79450; export SSH_AGENT_PID;

echo Agent pid 79450;

[philip@localhost ~]$

We started the ssh agent, which created the necessary variables and started the process. Next, we will run the ssh-add command with the -l option; this will list all the identities which the ssh agent is aware of as shown below:

[philip@localhost ~]$ ssh-add -l

The agent has no identities.

[philip@localhost ~]$

Based on the above, there are no identity known by the agent; we will now add the identity which we created earlier by using the ssh-add command without any option, as shown below:

[philip@localhost ~]$ ssh-add

Enter passphrase for /home/philip/.ssh/id_rsa:

Identity added: /home/philip/.ssh/id_rsa (/home/philip/.ssh/id_rsa)

[philip@localhost ~]$ ssh-add -l

2048 SHA256:BwdFiHu2iEyvnnXhnY+1tNpZmlaZZdL1Zugwda9PJ7g /home/philip/.ssh/id_rsa (RSA)

[philip@localhost ~]$

We can now see the identity of our private key, which we generated earlier. Now we will try to initiate an SSH session as shown below:

[philip@localhost ~]$ ssh 172.16.175.130

Welcome to Ubuntu LTS

Last login: Fri Sep 14 10:06:44 2023 from 172.16.175.129

philip@Linuxplus:~$ exit

[philip@localhost ~]$

We logged in successfully without entering the user’s password or the passphrase. The SSH configuration is stored in the /etc/ssh/ssh_config as shown below:

philip@localhost ~]$ cat /etc/ssh/ssh_config

# $OpenBSD: ssh_config,v 1.33 2017/05/07 23:12:57 djm Exp $

# IdentityFile ~/.ssh/id_dsa

# IdentityFile ~/.ssh/id_ecdsa

# IdentityFile ~/.ssh/id_ed25519

# Port 22

# Protocol 2

# Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc

# MACs hmac-md5,hmac-sha1,umac-64@openssh.com

# EscapeChar ~

# Tunnel no

# TunnelDevice any:any

# To modify the system-wide ssh configuration, create a *.conf file under

# /etc/ssh/ssh_config.d/ which will be automatically included below

Include /etc/ssh/ssh_config.d/*.conf

[philip@localhost ~]$

dSome output was omitted for brevity. Based on the above, all the settings are using their defaults. Another location where the known_hosts are kept is in the /etc/ssh/known_hosts; this allows administrators to add identities of all servers inside a LAN. This method prevents the identity message from appearing everyone a new user attempts to initiate an SSH session to a server. We can copy the content of ~./ssh/known_hosts to /etc/ssh/known_hosts, and if we try to log in as another user, we will not see the identity message as shown below:

[philip@localhost ~]$ cat ~/.ssh/known_hosts

172.16.175.130 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBPhEHNo6YSOE+ZZ9vHVmQqBPFQd8WtAUFoGYAJe3VPQJlhjhc9bxy+vwsetQiEIKTyMgnfrOC7LNbhxxmJ4IX8w=

[philip@localhost ~]$ cat /etc/ssh/ssh_known_hosts

172.16.175.130 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBPhEHNo6YSOE+ZZ9vHVmQqBPFQd8WtAUFoGYAJe3VPQJlhjhc9bxy+vwsetQiEIKTyMgnfrOC7LNbhxxmJ4IX8w=

[philip@localhost ~]$

[philip@localhost ~]$ ssh hacker@172.16.175.130

hacker@172.16.175.130's password:

Welcome to Ubuntu LTS

$ exit

Connection to 172.16.175.130 closed.

[philip@localhost ~]$ ssh teddy@172.16.175.130

teddy@172.16.175.130's password:

[philip@localhost ~]$

Based on the above, neither user was presented with the identity message. Note that they were prompted for their respective passwords because we only set up the key-based authentication for the philip user alone; we would need to generate the keys for each user.

[SELinux](#contents.xhtml_sc127a)

Security-Enhanced Linux (SELinux) is a security framework integrated into the Linux kernel that provides an additional access control and enforcement layer. In this chapter, we will delve into the details of SELinux, its purpose, components, and practical examples to illustrate its usage.

[Understanding SELinux](#contents.xhtml_sc128a)

SELinux is a Mandatory Access Control (MAC) mechanism that enhances the Linux kernel’s default Discretionary Access Control (DAC) model. It enforces fine-grained access policies, allowing administrators to define strict rules governing the actions and interactions of processes and users within the system.

[Advantages of SELinux](#contents.xhtml_sc129a)

SELinux provides several key benefits for system security:

*   Least privilege: SELinux follows the principle of least privilege by limiting the permissions and access levels of processes and users, reducing the potential impact of compromised or malicious code.
*   MAC: SELinux enforces access control policies that cannot be overridden by discretionary access control mechanisms, providing an additional layer of security.
*   Process isolation: SELinux isolates processes from each other, preventing unauthorized access to resources and reducing the risk of privilege escalation attacks.
*   Audit and accountability: SELinux generates detailed audit logs, allowing administrators to monitor and investigate security-related events.

[SELinux components](#contents.xhtml_sc130a)

Let us discuss the components of SELinux in detail:

*   Security contexts

SELinux uses security contexts to label and identify various system resources, such as files, directories, processes, and network ports. Security contexts consist of three elements: user, role, and type. They are represented as <user>:<role>:<type>.

*   SELinux modes

    SELinux operates in three modes:

    *   Enforcing: SELinux actively enforces access control policies, denying unauthorized actions and generating audit logs for policy violations.
    *   Permissive: SELinux does not enforce access control policies but logs policy violations for analysis and debugging purposes.
    *   Disabled: SELinux is completely disabled, and the kernel returns to the default DAC model.
*   SELinux policy

SELinux policies define the rules and constraints for access control. Policies specify the permissions and actions allowed or denied for various security contexts and interactions. Policies can be customized or extended to meet specific system requirements.

[SELinux usage examples](#contents.xhtml_sc131a)

Let us explore some practical examples to understand how SELinux can be used:

*   Checking SELinux status

To check the current SELinux mode and status, use the following command:

$ sestatus

This command displays the SELinux status, mode, and other relevant information.

*   Enabling and disabling SELinux

To enable SELinux in enforcing mode, modify the /etc/selinux/config file and set the SELINUX parameter to enforcing. To disable SELinux, set it to disabled. After making changes, restart the system.

To switch between permissive mode and enforcing mode, we can use setenforce command. The setenforce 0 command is used to put SELinux in permissive mode, and setenforce 1 command is used to put the SELinux in enforcing mode.

Let us put SELinux in permissive mode.

We will use the setenforce command and pass 0 as the argument, which will change SELinux from enforcing to permissive mode, as shown below:

#setenforce 0

To confirm the switch, we can use sestatus command again or the getenforce command (The getenforce command prints only the name of the current mode).

We will use the getenforce command to verify the selinux mode has been changed from enforcing to permissive, as shown below:

getenforce

Refer to [Figure 6.2](#ch06.xhtml_fig6-2):

![A screenshot of a computer Description automatically generated](images/Figure_6.2_.png)

Figure 6.2: Output of the getenforce and setenforce commands

Let us put SELinux in enforcing mode again. This will change the selinux modem from permissive to enforcing, as shown below:

#setenforce 1

Refer to [Figure 6.3](#ch06.xhtml_fig6-3):

![A screenshot of a computer Description automatically generated](images/Figure_6.3_.png)

Figure 6.3: Output of the getenforce and setenforce commands (enforcing mode)

*   Viewing and modifying security contexts

    *   To view the security context of a file or directory, we can use the ls command with the -Z option, as shown below:

    $ ls -Z /path/to/file

Refer to [Figure 6.4](#ch06.xhtml_fig6-4):

![A screen shot of a computer Description automatically generated with low confidence](images/Figure_6.4.png)

Figure 6.4: Output of the ls command with the -Z option

*   To modify the security context of a file or directory, we can use the chcon command, as shown below:

$ sudo chcon -t <type> /path/to/file

Refer to [Figure 6.5](#ch06.xhtml_fig6-5):

![A screenshot of a computer Description automatically generated](images/Figure_6.5.png)

Figure 6.5: Output of the chcon command with the -u option

SELinux audit logs and generates policy modules to allow previously denied actions. SELinux adds an extra layer of security to Linux systems through mandatory access control. This chapter provided a detailed explanation of SELinux, its purpose, components, and practical examples. By understanding and adequately configuring SELinux, administrators can enhance the security of their Linux systems and protect against various security threats.

[Conclusion](#contents.xhtml_sc132a)

In this chapter, we delve further into security topics, specifically firewalls, remote access, and SELinux. You will gain insights into enhancing network security through firewall configurations and remote access management. Additionally, we will explore the benefits and functionality of SELinux, a security framework for Linux systems. In the upcoming chapter, we will shift gears and delve into shell scripting and containers, expanding your knowledge and skills in these areas.

# [CHAPTER 7Shell Scripting and Containers](#contents.xhtml_ch07a)

[Introduction](#contents.xhtml_sc133a)

In the last chapter, we emphasized firewalls. A Linux firewall is a software-based network security system that protects computer systems or networks by monitoring and controlling traffic based on predefined rules, ensuring security against unauthorized access and potential threats. This chapter is dedicated to the integration of shell scripting and containers. We will explore the essential elements of shell scripting and topics like structures, looping mechanisms, and more. We will delve into the realm of containers, specifically focusing on LXC and Docker. Throughout this journey, we will gain insights into the power of shell scripting and the versatility of containerization.

[Structure](#contents.xhtml_sc134a)

In this chapter, we will learn the following topics:

*   Shell scripting
    *   for loop
    *   while loop
    *   if statements
*   Containers
    *   Linux containers
    *   Docker

[Objectives](#contents.xhtml_sc135a)

This chapter covers the fundamental aspects of shell scripting, including script structure, using the echo command, storing user input, utilizing for and while loops, working with if statements, making scripts executable, and running them. Additionally, it explores defining variables and deploying images using Linux containers and Docker. By mastering these concepts, you will gain the necessary skills to create efficient shell scripts and deploy containerized applications.

[Shell scripting](#contents.xhtml_sc136a)

In this section, we will cover shell scripting, starting with the basics and then moving on to writing scripts using loops and if statements; we will discuss the basics of shell scripting, writing scripts using for loops, while loops, and if statements.

[Basics of shell scripting](#contents.xhtml_sc137a)

We often work with a series of commands regularly at the command line. It would be ideal if we could somehow bundle these commands and simplify the process of executing a single command or script and accomplishing the overall objectives, which would usually take longer if we were to type out every single command repetitively. This is where shell scripting shines; we can place our commands, regardless of their length, store them in a single file, giving it an appropriate name, and execute the script as needed. Here is the basic syntax for creating a shell script as shown below:

#! /bin/sh

Based on the above, this is the first line in a script; it is used to define the shell interpreter. The first characters #! are often known as shebang, sha-bang, hashbang, pound-bang, or hash-pling. The /bin/sh defines which interpreter should be used for this script; in this case, it is the Shell Command Language or sh. Another popular interpreter you are bound to face is the following:

#!/bin/bash

Based on the above, it is like the previous declaration in that we have the #!,  which indicates that we will define the shell interpreter to be used; in this case, we are using the Bourne Again Shell or bash. This shell offers more extensions than the regular sh shell. Most newer Linux distributions are ported with bash as its de facto shell. We can easily identify which shell is in play by issuing the following command in the terminal as shown below:

[philip@localhost Documents]$ echo $SHELL

/bin/bash

[philip@localhost Documents]$

The environment variable SHELL stores the current shell; the value returned indicates that we are running the bash shell. Another way to identify the shell is by doing the following:

[philip@localhost Documents]$ echo $0

bash

[philip@localhost Documents]$

The bash shell is being used. Also, we can use the ps command to display the current shell, as shown below:

[philip@localhost Documents]$ ps

PID TTY TIME CMD

74972 pts/1 00:00:03 bash

75678 pts/1 00:00:39 dnf

92796 pts/1 00:00:00 ps

[philip@localhost Documents]$

For our purposes, we will use the #!/bin/bash for the scripts written. To begin writing our very first script, open a text editor such as vi or nano and enter the following:

philip@localhost Documents]$ vi myFirstScript.sh

Based on the above, we first have our declaration in the first line; we have defined the /bin/bash shell. Next, we have two lines beginning with a # symbol. Any line except the first line at the top is referred to as a comment. The last two lines are comments. We can prove this by saving our script; we would do a: wq which will save and exit our script:

[philip@localhost Documents]$ cat myFirstScript.sh

#!/bin/bash

#This is a comment

#echo 'This is also a comment'

[philip@localhost Documents]$

Based on the above, we can see the contents of our script. The next step would be to make our script executable, meaning running a script would need to become executable. This can be done using the chmod command as shown below:

[philip@localhost Documents]$ chmod +x myFirstScript.sh

[philip@localhost Documents]$

We have used the +x to turn on the execute bit for the user, group and other. Also, the script’s name has been changed to green to indicate that this file is now executable. To run this script, we would simply do the following:

[philip@localhost Documents]$ ./myFirstScript.sh

[philip@localhost Documents]$

The script was executed; however, the contents were not displayed. This is because we have only defined comments thus far and nothing else inside our script. Let us make our script display a short message, open back the script using either vi or nano, and enter the following:

[philip@localhost Documents]$ cat myFirstScript.sh

#!/bin/bash

#This is a comment

#echo 'This is also a comment'

echo 'Hello world'

[philip@localhost Documents]$

We have added our first command to be executed, the echo command; this will simply output whatever is passed, as can be seen below:

[philip@localhost Documents]$ ./myFirstScript.sh

Hello world

[philip@localhost Documents]$

We have just successfully written our very first script. Let us add another command to illustrate the effectiveness of scripting; we will add the date command, which will output the date whenever we execute our script. This can be shown below:

[philip@localhost Documents]$ cat myFirstScript.sh

#!/bin/bash

#This is a comment

#echo 'This is also a comment'

echo 'Hello world'

date

[philip@localhost Documents]$ ./myFirstScript.sh

Hello world

Mon Jun 17 10:04:48 EDT 2023

[philip@localhost Documents]$

Based on the above, two commands are executed every time our script is run. In addition to sending output to the display, we can carry out other tasks. For instance, we can create an archive file. We will create a tar file of the /home/philip/Downloads directory as shown below:

[philip@localhost Documents]$ cat myFirstScript.sh

#!/bin/bash

#This is a comment

#echo 'This is also a comment'

echo 'Hello world'

date

tar -cvf mytar.tar /home/philip/Downloads

[philip@localhost Documents]$

We have used the tar command to create an archive of the /home/philip/Downloads directory. Now we can run this script to see the results as shown below:

[philip@localhost Documents]$ ./myFirstScript.sh

Hello world

Mon Jun 17 10:35:37 EDT 2023

tar: Removing leading `/' from member names

/home/philip/Downloads/

/home/philip/Downloads/home/

/home/philip/Downloads/home/philip/

/home/philip/Downloads/home/philip/Downloads/

/home/philip/Downloads/home/philip/Downloads/song.mp3

[philip@localhost Documents]$ ls | grep tar

mytar.tar

[philip@localhost Documents]$

Our script was successful, and an archive was created with the .tar extension. We can also create a script that takes input from the user; we would use the read command. Let us create another script and name it input.sh using vi or nano as shown below:

[philip@localhost Documents]$ ls -l input.sh

-rw-rw-r--. 1 philip philip 75 Sep 17 10:42 input.sh

[philip@localhost Documents]$ cat input.sh

#!/bin/bash

echo 'Whats your name?'

read name

echo 'your name is $name'

[philip@localhost Documents]$ chmod +x input.sh

[philip@localhost Documents]$

We have created an input.sh script; we have used the read command to store the input from the user. The value stored in the name is called a variable. It is then displayed in the last line by adding a $ in front of the variable’s names. Here is the result of this script as shown below:

[philip@localhost Documents]$ ./input.sh

Whats your name?

Based on the above, the prompt is paused until we enter something; we will enter a name and see the results as shown below:

[philip@localhost Documents]$ ./input.sh

Whats your name?

Philip

your name is: Philip

[philip@localhost Documents]$

The name which we entered was appended to the last line. Another way we can define a variable is by using the following syntax:

<variable name> = <value>

We would give the variable a name and then specify a value based on the above. Let us create a new script using either vi or nano named myvar.sh. Here is how we can define a variable using a new script:

[philip@localhost Documents]$ vi myvar.sh

[philip@localhost Documents]$ cat myvar.sh

#!/bin/bash

OUR_VAR="Philip Inshanally"

echo "The variable which we defined is $OUR_VAR"

[philip@localhost Documents]$ chmod +x myvar.sh

[philip@localhost Documents]$ ./myvar.sh

The variable which we defined is Philip Inshanally

[philip@localhost Documents]$

We defined a variable OUR_VAR and gave it the value Philip Inshanally; this was then called inside the echo command by placing a $ symbol in front of the variable name. As you can see, there are various ways of defining a variable. The variable value must be enclosed in parenthesis whenever there is a space between the words. If there is only a single word or, in the case of numbers, then we would not enclose the value in parenthesis.

Note: Do not enclose a single word or number in parenthesis.

[Writing scripts using for loops](#contents.xhtml_sc138a)

It is possible to write out each command line by line in a script which could be cumbersome at times, or we could achieve the same objective by using loops that would execute based on an expression being met, generating the commands for us. The basic syntax for a for loop is as follows:

for <condition>

do

<command1>

<command2>

…

<commandN>

done

Based on the above, the first line defines a condition then once the condition is met, we have a series of commands. To see this in action, let us create a script called myForLoop.sh using either vi or nano, as shown below:

[philip@localhost Documents]$ vi myForLoop.sh

[philip@localhost Documents]$ chmod +x myForLoop.sh

[philip@localhost Documents]$ cat myForLoop.sh

#!/bin/bash

echo 'This script displays how a for loop works'

for o in {1..10}

do

echo "The loop is running for the: $o time"

done

[philip@localhost Documents]$

The line that begins with for o in {1..10} defines how many times we would like to execute the for loop; it will be executed ten times. The command under the do section is the command which will be executed; the $o is the variable that was defined in the for section. The result will be the following:

[philip@localhost Documents]$ ./myForLoop.sh

This script displays how a for loop works

The loop is running for the: 1 time

The loop is running for the: 2 time

The loop is running for the: 3 time

The loop is running for the: 4 time

The loop is running for the: 5 time

The loop is running for the: 6 time

The loop is running for the: 7 time

The loop is running for the: 8 time

The loop is running for the: 9 time

The loop is running for the: 10 time

[philip@localhost Documents]$

Excellent! This condition can also be written in the format shown below:

[philip@localhost Documents]$ cat myForLoop.sh

#!/bin/bash

echo 'This script displays how a for loop works'

#for o in {1..10}

for p in 1 2 3 4 5 6 7 8 9 10 11 12

do

echo "The loop is running for the: $p time"

done

[philip@localhost Documents]$

[philip@localhost Documents]$ ./myForLoop.sh

This script displays how a for loop works

The loop is running for the: 1 time

The loop is running for the: 2 time

The loop is running for the: 3 time

The loop is running for the: 4 time

The loop is running for the: 5 time

The loop is running for the: 6 time

The loop is running for the: 7 time

The loop is running for the: 8 time

The loop is running for the: 9 time

The loop is running for the: 10 time

The loop is running for the: 11 time

The loop is running for the: 12 time

[philip@localhost Documents]$

We wrote the values separated by space, and the script was successful. Furthermore, another method to specify a condition is by defining the variable, then specifying a test condition using the <= operator. Finally, the variable can be incremented using the ++ operator, similar to the C programming language, as shown below:

[philip@localhost Documents]$ cat myForLoop.sh

#!/bin/bash

echo 'This script displays how a for loop works'

#for o in {1..10}

#for p in 1 2 3 4 5 6 7 8 9 10 11 12

for ((p=1; p<=6; p++))

do

echo "The loop is running for the: $p time"

done

[philip@localhost Documents]$

[philip@localhost Documents]$ ./myForLoop.sh

This script displays how a for loop works

The loop is running for the: 1 time

The loop is running for the: 2 time

The loop is running for the: 3 time

The loop is running for the: 4 time

The loop is running for the: 5 time

The loop is running for the: 6 time

[philip@localhost Documents]$

Based on the above, the line for ((p=1; p<=6; p++)) defines a variable and assigns it a value of p=1; the p<=6 checks for the condition, and the p++ means to increment the value of the variable if the condition is met.

[The while loop](#contents.xhtml_sc139a)

Another popular loop that can be used in scripting is the while loop. The basic syntax of the while loop is:

while <condition>

do

<command1>

<command2>

…

<commandN>

done

Based on the above, we would specify a condition, and if the condition is met, the loop will be executed. Create a script named myWhile.sh using either vi or nano as shown below:

[philip@localhost Documents]$ vi myWhile.sh

[philip@localhost Documents]$ chmod +x myWhile.sh

[philip@localhost Documents]$ cat myWhile.sh

#!/bin/bash

d=1

while (( $d <= 8 ))

do

echo "The number is $d times"

d=$(( d+1 ))

done

[philip@localhost Documents]$

We have first defined a variable d=1, and we then specified a condition (( $d <= 8 )), which means to check if the variable d is less than or equal to 8; following this, we are using the echo command to output the text based on the condition. The last part d=$(( d+1 )) will increment the variable after each condition is met, as can be shown below:

[philip@localhost Documents]$ ./myWhile.sh

The number is 1 times

The number is 2 times

The number is 3 times

The number is 4 times

The number is 5 times

The number is 6 times

The number is 7 times

The number is 8 times

[philip@localhost Documents]$

Another technique that can be used for a condition is the : after the while statement. The : would always be True, meaning that the loop would not end until we end the script using Ctrl+C. Let us create another script named infinite.sh using either vi or nano, as shown below:

[philip@localhost Documents]$ vi infinite.sh

[philip@localhost Documents]$ chmod +x infinite.sh

[philip@localhost Documents]$ cat infinite.sh

#!/bin/bash

while :

do

echo "You can enter text and press Enter as many times (exit using CTRL+c)"

read someText

echo "You typed $someText"

done

[philip@localhost Documents]$

Based on the above script, a prompt will appear, allowing us to type anything, and then as soon we press the Enter key, another message will be displayed with whatever we typed. This will continue infinitely until we exit the script using CTRL+C, as shown below:

[philip@localhost Documents]$ ./infinite.sh

You can enter text and press Enter as many times (exit using CTRL+c)

Hi

You typed Hi

You can enter text and press Enter as many times (exit using CTRL+c)

How are you?

You typed How are you?

You can enter text and press Enter as many times (exit using CTRL+c)

I can keep typing

You typed I can keep typing

You can enter text and press Enter as many times (exit using CTRL+c)

and typing

You typed and typing

You can enter text and press Enter as many times (exit using CTRL+c)

I can exit by using the keystroke as shown in the message above

You typed I can exit by using the keystroke as shown in the message above

You can enter text and press Enter as many times (exit using CTRL+c)

^C

[philip@localhost Documents]$

Based on the above, the script did not quit until we used the Ctrl+C combination. Another way to illustrate the effectiveness of the while loop is to look for a string before the script exits. Create another script named whileString.sh using either vi or nano as shown below:

[philip@localhost Documents]$ vi whileString.sh

[philip@localhost Documents]$ chmod +x whileString.sh

[philip@localhost Documents]$ cat whileString.sh

#!/bin/bash

someString=begin

while [ "$someString" != "quit" ]

do

echo "Enter some text (type quit to exit)"

read someString

echo "You entered: $someString"

done

[philip@localhost Documents]$

We declared a variable someString=begin, which could be any value you choose. Next, we checked for a condition [ "$someString" != "quit" ], which looks for the string quit; as long as the string is not quit, the script will keep running infinitely until we type quit or press Ctrl+C which will exit the script as shown below:

[philip@localhost Documents]$ ./whileString.sh

Enter some text (type quit to exit)

Hi

You entered: Hi

Enter some text (type quit to exit)

my name is Philip

You entered: my name is Philip

Enter some text (type quit to exit)

How are you

You entered: How are you

Enter some text (type quit to exit)

quit

You entered: quit

[philip@localhost Documents]$

Based on the above, we could keep entering any text, and the script would continue to run unless we entered quit or pressed Ctrl+C, which would exit the script. Notice we used square brackets [] to enclose the text. The script would not work with the regular brackets () when testing for a string value.

[Writing scripts using if statements](#contents.xhtml_sc140a)

We can use if statements in scripting to test a condition. The basic syntax of an if statement is:

if [[some condition]]; then

execute something

fi

or

if [[some condition]]; then

execute something

fi

Based on the above, we can create a simple if script using the above as guidance. Sometimes, we may need to use double square brackets, which offer more enhancements over the older single bracket style. Let us create a script using vi or nano named myif.sh as shown below:

[philip@localhost Documents]$ vi myif.sh

[philip@localhost Documents]$ cat myif.sh

#!/bin/bash

echo "Welcome to our if statement script"

if [[ $1 == 4 ]]; then

echo "You're very smart"

fi

echo "See you soon!"

[philip@localhost Documents]$ chmod +x myif.sh

[philip@localhost Documents]$ ./myif.sh

Welcome to our if statement script

See you soon!

[philip@localhost Documents]$

Based on the above, we used the echo command to display a welcome message; we then used the if [[ $1 == 4 ]]; this statement is checking for a 4. The script executed; however, we did not see the echo command inside the if statement executed. To see the message inside the if statement, we would need to type a value when we run our script, as shown below:

[philip@localhost Documents]$ ./myif.sh 4

Welcome to our if statement script

You're very smart

See you soon!

[philip@localhost Documents]$

Wonderful, the statement inside of the if construct was executed but if we passed any value other than "4", here is what we would see:

[philip@localhost Documents]$ ./myif.sh 3

Welcome to our if statement script

See you soon!

[philip@localhost Documents]$

Based on the above, the command inside the if statement was not executed because the value we passed does not equal the value being checked against. We can add another bit to the if statement to handle an alternate response; we would use the else clause. Here is the syntax of the else being injected into the if statement:

if [[some condition]]; then

execute something

else

execute something else

fi

Based on the above, we can edit our my.sh script using either vi or nano and add an else clause to handle any alternate response, as shown below:

[philip@localhost Documents]$ vi myif.sh

[philip@localhost Documents]$ cat myif.sh

#!/bin/bash

echo "Welcome to our if statement script"

if [[ $1 == 4 ]]; then

echo "You're very smart"

else

echo " Better luck next time"

fi

echo "See you soon!"

[philip@localhost Documents]$

We can run our script with the else clause injected, and we will see the following:

[philip@localhost Documents]$ ./myif.sh 3

Welcome to our if statement script

Better luck next time

See you soon!

[philip@localhost Documents]$ ./myif.sh 2

Welcome to our if statement script

Better luck next time

See you soon!

[philip@localhost Documents]$ ./myif.sh 4

Welcome to our if statement script

You're very smart

See you soon!

[philip@localhost Documents]$

We are shown a different message whenever the user enters any value other than 4. Furthermore, we can nest an if statement inside another if statement. The basic syntax for nesting if statements are as follows:

if [[first condition]]; then

execute something

elif [[second condition]]; then

execute something else

elif [[third condition]]; then

execute something else

else

execute_a_last_resort_command

fi

Based on the above, we can edit our myif.sh script using either vi or nano and add a second elif statement as shown below:

[philip@localhost Documents]$ cat myif.sh

#!/bin/bash

echo "Welcome to our if statement script"

if [[ $1 == 4 ]]; then

echo "You're very smart"

elif [[ $1 == 2 ]]; then

echo "You've got your elseif value correct!"

else

echo "Reach for the sky"

fi

echo "See you soon!"

[philip@localhost Documents]$

Based on the above, we have added the elif [[ $1 == 2 ]]; then, which is checking for the value 2. Once this condition is met, then a message will be displayed as shown below:

[philip@localhost Documents]$ ./myif.sh 2

Welcome to our if statement script

You've got your elseif value correct!

See you soon!

[philip@localhost Documents]$ ./myif.sh 3

Welcome to our if statement script

Reach for the sky

See you soon!

[philip@localhost Documents]$ ./myif.sh 4

Welcome to our if statement script

You're very smart

See you soon!

[philip@localhost Documents]$

When we enter a value that matches the elif condition, we can see that the command under the elif condition is executed. Adding to this, a catch-all message was displayed when we entered a value that did not match either the if or elif condition. Testing multiple conditions on a single if or elif statement is also possible. Let us edit our myif.sh using vi or nano and enter the following:

[philip@localhost Documents]$ cat myif.sh

#!/bin/bash

echo "Welcome to our if statement script"

if [[ $1 == 4 ]] || [[ $1 == 3 ]] ; then

echo "You're very smart"

elif [[ $1 == 2 ]]; then

echo "You've got your elseif value correct!"

else

echo "Reach for the sky"

fi

echo "See you soon!"

[philip@localhost Documents]$

Based on the above, we have added a second condition in the if statement, namely, if [[ $1 == 4 ]] || [[ $1 == 3 ]] ; then, the || means or. This is checking for either condition to be met, and the command will be executed under the if statement as shown below:

[philip@localhost Documents]$ ./myif.sh 4

Welcome to our if statement script

You're very smart

See you soon!

[philip@localhost Documents]$ ./myif.sh 3

Welcome to our if statement script

You're very smart

See you soon!

[philip@localhost Documents]$

Once either condition was met in the if clause, the command was executed under the if clause. Adding to this, there is also the && used for comparing conditions; this means that both conditions must be met. We can quickly edit our myif.sh script and add in the && as shown below:

[philip@localhost Documents]$ cat myif.sh

#!/bin/bash

echo "Welcome to our if statement script"

if [[ $1 == 4 ]] || [[ $1 == 3 ]] ; then

echo "You're very smart"

elif [[ $1 == 2 ]] && [[ $1 != 1 ]] ; then

echo "You've got your elseif value correct!"

else

echo "Reach for the sky"

fi

echo "See you soon!"

[philip@localhost Documents]$

Based on the above, when the user enters a 2 the elif condition will be met; this is because both the conditions need to be true. If the user enters any value other than 2, then the catch-all else clause will be executed as shown below:

[philip@localhost Documents]$ ./myif.sh 1

Welcome to our if statement script

Reach for the sky

See you soon!

[philip@localhost Documents]$ ./myif.sh 2

Welcome to our if statement script

You've got your elseif value correct!

See you soon!

[philip@localhost Documents]$

Both conditions were met in the elif clause resulting in the command being executed under the elif clause.

[Containers](#contents.xhtml_sc141a)

In Linux, containers are a lightweight form of virtualization that allows for the isolation and independent execution of applications and services. Containers provide an environment where an application and its dependencies can run consistently across different systems, regardless of the underlying infrastructure.

At the core of containerization in Linux is a technology called container engines or container runtimes. These engines, such as LXC or Docker, leverage Linux kernel features like control groups (cgroups) and namespaces to create and manage containers.

[Linux containers](#contents.xhtml_sc142a)

Linux Containers (LXC) is an operating system-level virtualization technology that enables the creation and management of lightweight containers on Linux systems.

[Understanding Linux containers](#contents.xhtml_sc143a)

LXC is a set of tools, libraries, and kernel features that enable the creation and management of lightweight, isolated containers on Linux systems. LXC leverages kernel namespaces, cgroups, and other features to isolate processes and resources, allowing multiple containers to run on a single host.

[Key concepts in Linux containers](#contents.xhtml_sc144a)

Let us look at the key concepts in Linux containers:

*   Container: A container is an isolated environment that encapsulates an application and its dependencies. Containers are lightweight, share the host kernel, and have their own filesystem, network, and process space.
*   LXC tools: LXC provides command-line tools, such as lxc-create, lxc-start, and lxc-stop, for creating, starting, and managing containers.
*   Configuration files: LXC uses configuration files, typically located in the /var/lib/lxc directory, to define the properties and settings of containers, including networking, storage, and resource limits.

[Linux containers components](#contents.xhtml_sc145a)

LXC provides a set of user-space tools that facilitate container management. Some commonly used LXC tools include:

lxc-create: Creates a new container from a template.

lxc-start: Starts a container.

lxc-stop: Stops a running container.

lxc-attach: Attaches to a running container’s namespace.

lxc-info: Displays information about a container.

[Linux containers templates](#contents.xhtml_sc146a)

LXC templates are used to create container root file systems. Templates define the base image and initial filesystem layout for containers. Examples of LXC templates include lxc-download (downloads pre-built images) and lxc-local (uses a local filesystem directory as the container’s root).

[Kernel features](#contents.xhtml_sc147a)

LXC relies on various kernel features to provide isolation and resource management. Some key kernel features used by LXC include:

Namespaces: Kernel namespaces provide process-level isolation by creating separate instances of resources like process IDs, network interfaces, file systems, and more.

Control groups (cgroups): They allow fine-grained resource allocation and management, enabling administrators to limit and control CPU, memory, disk I/O, and other container resources.

[Some Linux containers usage](#contents.xhtml_sc148a)

Let us explore some practical examples to understand how LXC can be used:

*   Creating a new container

To create a new container using LXC, you can use the lxc-create command with a specified template and container name. For example:

$ sudo lxc-create -t download -n mycontainer

This command creates a new container named mycontainer using the download template, which downloads a pre-built image.

*   Starting and stopping a container

    *   To start a container, use the lxc-start command followed by the container name:

    $ sudo lxc-start -n mycontainer

    *   To stop a running container, use the lxc-stop command:

    $ sudo lxc-stop -n mycontainer

*   Attaching to a container’s namespace
*   To access a running container’s namespace, you can use the lxc-attach command followed by the container name. For example, to enter a container’s shell:

$ sudo lxc-attach -n mycontainer

This command attaches to the container’s namespace and accesses its processes and filesystem.

*   Configuring container networking

LXC allows you to configure networking for containers. You can define network interfaces, bridges, and IP addresses for containers. The configuration is specified in the container’s configuration file in /var/lib/lxc.

[Docker](#contents.xhtml_sc149a)

Docker is a popular platform that simplifies the process of creating, deploying, and managing applications using containerization.

It is an open-source platform that automates the deployment of applications inside software containers. It utilizes containerization technology to encapsulate applications and their dependencies into portable, lightweight units called Docker containers. Docker provides an ecosystem of tools and services for building, distributing, and running containers.

[Key concepts in Docker](#contents.xhtml_sc150a)

Let us have a look at the key concepts in Docker:

*   Docker images: Docker images are read-only templates that contain everything needed to run an application, including the code, runtime, libraries, and system tools. Images are built using Dockerfiles, which define the image’s steps.
*   Docker containers: Docker containers are lightweight, isolated, and runnable instances of images. Containers run in an isolated environment, using the host kernel but with separate file systems and network interfaces.
*   Docker engine: The Docker engine is the core component of Docker that enables the creation and execution of containers. It includes a server that runs in the background, handling container management, and a CLI for interacting with Docker.
*   Docker registry: Docker registries are repositories for storing and distributing Docker images. Docker Hub is the most widely used registry, but private registries can also be set up for internal use.

[Docker components](#contents.xhtml_sc151a)

Let us discuss Docker components in detail:

*   Docker engine

    The Docker engine consists of three main components:

    *   Docker daemon: The Docker daemon, dockerd, runs as a background service on the host system. It listens for Docker API requests and manages container lifecycle, networking, and storage.
    *   Docker CLI: The Docker CLI interacts with the Docker daemon. It provides a set of commands for building, managing, and running containers.
    *   Docker compose: Docker compose is a tool for defining and managing multi-container applications. It allows you to define a set of services, networks, and volumes in a YAML file and easily deploy and manage the entire application stack.
*   Docker images

Docker images are the building blocks of containers. They are created using Dockerfiles, text files containing instructions to build an image. Docker images are stored in repositories called registries, and they can be shared, versioned, and distributed across different environments.

[Docker containers](#contents.xhtml_sc152a)

Docker containers are instances of Docker images. They are isolated and lightweight, providing a consistent environment for running applications. Containers can be started, stopped, restarted, and removed using Docker commands. Multiple containers can run simultaneously on the same host, each with its isolated environment.

[Docker usage examples](#contents.xhtml_sc153a)

Let us explore some practical examples to understand how Docker can be used:

*   Running a container with Docker

    To run a container using Docker, use the docker run command followed by the image name. For example:

    $ docker run ubuntu:latest

    This command pulls the latest Ubuntu image from the Docker Hub registry and starts a container based on that image.

*   Building a custom container image

    To build a custom container image with Docker, create a Dockerfile that defines the image configuration and build instructions. For example:

    # Dockerfile

    FROM ubuntu:latest

    RUN apt-get update && apt-get install -y nginx

    CMD ["nginx", "-g", "daemon off;"]

    Use the docker build command to build the image:

    $ docker build -t my-nginx-image

    This command builds an image based on the Dockerfile in the current directory and tags it with my-nginx-image.

*   Container networking using Docker

    Linux containers can be connected to networks to enable communication with other containers or the host system. Docker provides a built-in networking feature that allows containers to be attached to different network interfaces or networks. For example:

    $ docker network create my-network

    $ docker run --network=my-network my-nginx-image

    This creates a custom network called my-network and starts a container based on the my-nginx-image image connected to that network.

[Conclusion](#contents.xhtml_sc154a)

In this chapter, we delved into shell scripting, covering topics such as structures, looping mechanisms, and more. Finally, we wrapped up this chapter with containers, focusing on LXC and Docker.

In the next chapter, our focus will shift toward automation.

# [CHAPTER 8Configuration Management with YAML, JSON and Ansible](#contents.xhtml_ch08a)

[Introduction](#contents.xhtml_sc155a)

In the last chapter, we covered shell scripting: focusing on the structure of a shell script, the for and while loop, and testing condition(s) using if statements. We then finished the chapter with containers. In this chapter, we continue along that path by looking at automation. We will first look at YAML, and then we will touch JSON. Finally, we will wrap up with Ansible. This chapter highlights the significance of scripting, task scheduling, and command-line tools to automate repetitive tasks and enhance efficiency. These topics will give you valuable insights into automation techniques and tools.

[Structure](#contents.xhtml_sc156a)

In this chapter, we will cover the following topics:

*   YAML
*   JSON
*   Ansible

[Objectives](#contents.xhtml_sc157a)

In this chapter, we will explore YAML’s structure, including defining key-value pairs, nested structures, scalars, and multiline scalars. Additionally, we will cover YAML features like anchors and aliases, directives, JSON structure and data types, JSON arrays, Ansible structure, Ansible inventory, and Ansible playbook. Studying these concepts, you will gain a comprehensive understanding of YAML and its applications in configuration management and automation with Ansible.

[YAML](#contents.xhtml_sc158a)

YAML or YAML Ain’t Markup Language is a human-readable data serialization format commonly used in Linux and other programming languages. Its simplicity and readability stand out, making it easy to create and understand configuration files, data structures, and settings. This explanation will provide an overview of YAML’s syntax and features.

[Basic structure](#contents.xhtml_sc159a)

YAML uses indentation and whitespace to define its structure. It uses a combination of lines, indentation, and special characters to represent data. Key-value pairs and lists are the primary building blocks of YAML.

[Comments](#contents.xhtml_sc160a)

Comments in YAML begin with the # symbol and can be used to provide additional information or annotations. They are ignored during parsing.

[Key-value pairs](#contents.xhtml_sc161a)

Key-value pairs consist of a key, followed by a colon, and the associated value. The key provides a unique identifier for the value. Here is an example:

key: value

Keys can be strings, numbers, or Booleans, and values can be any YAML data type.

[Lists](#contents.xhtml_sc162a)

Lists in YAML are represented using hyphens (-) followed by a space. They allow you to define sequences of values. Here is an example:

- item1

- item2

- item3

Lists can contain any YAML data type, including other lists and key-value pairs.

[Nested structures](#contents.xhtml_sc163a)

YAML supports nesting, allowing you to create complex data structures. Indentation is used to represent nested elements. Here is an example:

key1:

subkey1: value1

subkey2: value2

key2:

- item1

- item2

In the above example, key1 and key2 are at the root level, while subkey1, subkey2, and the list are nested under key1 and key2.

[Scalars](#contents.xhtml_sc164a)

Scalars represent single values and can be strings, numbers, Booleans, or null. They can be written directly as values or as part of key-value pairs. Examples:

string: Hello, YAML!

number: 42

boolean: true

null_value: null

[Multiline scalars](#contents.xhtml_sc165a)

YAML supports multiline scalars, allowing you to represent strings or text that span multiple lines. Here is an example:

multiline: |

This is a multiline

string in YAML.

The | symbol followed by a newline indicates a literal block scalar, preserving newlines and indentation.

[Anchors and aliases](#contents.xhtml_sc166a)

YAML provides a way to reference a value defined elsewhere in the document using anchors and aliases. An anchor is defined using the & symbol, and an alias is created using the * symbol. For example:

original: &ref 123

alias: *ref

In the above example, original has the value 123, and the alias refers to the same value.

[Directives](#contents.xhtml_sc167a)

YAML supports directives at the beginning of a document to specify processing instructions. A commonly used directive is %YAML to indicate the version of YAML being used:

%YAML 1.2

---

# YAML content goes here

[Use case scenarios of YAML](#contents.xhtml_sc168a)

These are the fundamental concepts of YAML. It is important to note that proper indentation is crucial in YAML syntax, as it determines the structure and nesting of the data. YAML files are often used for configuration files, such as in Linux-based systems, or for defining data structures in various programming languages.

In Linux, YAML is commonly used for configuration files, particularly in applications and systems that require human-readable and easily maintainable configuration settings. Here are a few examples of how YAML is used in Linux:

*   Configuration files: Many Linux applications use YAML for their configuration files. These files store settings and options that define the behavior of the application. For instance, web servers like Nginx and Apache often utilize YAML-based configuration files to specify server properties, virtual hosts, and other settings.
*   Docker compose: Docker compose, a tool for defining and running multi-container Docker applications, employs YAML files to describe the containers, their configurations, and the network connections between them. Docker compose files specify services, volumes, ports, environment variables, and other Docker-related settings.
*   Kubernetes configurations: Kubernetes, an orchestration platform for containerized applications, utilizes YAML for defining various resources, including deployments, services, pods, and ingress rules. YAML files describe the desired state of the Kubernetes cluster and its components, enabling easy management and scalability of applications.
*   Package managers: Some Linux package managers, such as Snap and Flatpak, use YAML files for package metadata and configurations. These files specify information about the package, dependencies, permissions, application metadata, and other relevant details.

By utilizing YAML in these contexts, Linux applications and systems benefit from a structured, human-readable format that allows easy modification and understanding of configuration settings. YAML’s simplicity and ability to represent complex data structures make it a versatile choice for configuration files and other data serialization needs in the Linux ecosystem.

Some common configurations which use YAML:

*   Nginx configuration (nginx.conf):

http:

server:

listen: 80

server_name: example.com

location:

*   path: /
*   proxy_pass: http://localhost:3000

*   Docker compose (docker-compose.yml):

version: '3'

services:

web:

build: .

ports:

*   8080:80

volumes:

*   ./app:/var/www/html

environment:

*   MYSQL_HOST=db
*   MYSQL_USER=root
*   MYSQL_PASSWORD=secret

db:

image: mysql:5.7

environment:

*   MYSQL_ROOT_PASSWORD=secret

*   Kubernetes deployment (deployment.yaml):

apiVersion: apps/v1

kind: Deployment

metadata:

name: myapp-deployment

spec:

replicas: 3

selector:

matchLabels:

app: myapp

template:

metadata:

labels:

*   app: myapp

spec:

containers:

*   name: myapp
    *   ![](images/sqr.png) image: myapp:latest
    *   ![](images/sqr.png) ports:
*   containerPort: 8080

These are just a few examples of YAML files used in Linux for different purposes, including web server configuration, automation with Ansible, container orchestration with Docker compose, and managing deployments in Kubernetes. The actual content and structure of YAML files can vary depending on the specific requirements and applications.

YAML is not a separate package that must be installed in Linux. Instead, YAML is a data serialization format, and libraries and tools are available in various programming languages for parsing and working with YAML files. If you need to work with YAML files in Linux, here are a few options:

*   Python: Python provides a popular YAML library called PyYAML. You can install it using pip, the Python package manager:

$ pip install pyyaml

*   Ruby: Ruby has a YAML library called Psych that is included in the standard library, so no additional installation is required.
*   Node.js: For working with YAML in Node.js, you can use the js-yaml library. Install it using the Node.js package manager:

$ npm install js-yaml

*   Command-line tools: There are several command-line tools available for working with YAML files in Linux, such as yaml-cli, yq, or jq (with YAML support). These tools allow you to parse, manipulate, and query YAML files from the command line. You can usually install them using package managers like apt or yum:

$ sudo apt install yaml-cli

The installation process may vary depending on your Linux distribution and package manager. It is recommended to consult the documentation or search for the installation instructions specific to your Linux distribution if the above instructions do not work.

Once you have installed a YAML library or tool, you can read, write, and manipulate YAML files using the programming language or command-line interface provided by that library or tool.

[JSON](#contents.xhtml_sc169a)

JavaScript Object Notation (JSON) is a lightweight data-interchange format widely used for representing structured data. It is human-readable and easy for humans and machines to parse and generate. JSON is extensively used in web applications, APIs, configuration files, and data storage. JSON is widely supported in various programming languages. Most languages provide libraries or built-in functions to parse JSON strings into native data structures and serialize objects into JSON format. This allows seamless integration between systems using JSON as a common data format.

[JSON schema](#contents.xhtml_sc170a)

JSON Schema is a specification that defines the structure, validation rules, and documentation for JSON data. It provides a way to describe the expected structure and properties of JSON objects, ensuring data consistency and integrity.

[JSON APIs](#contents.xhtml_sc171a)

Many web APIs use JSON as the data format for request and response payloads. JSON is commonly used to exchange data between the client and server when interacting with web services.

JSON’s simplicity, readability, and versatility have made it a popular choice for data interchange in various applications. Programming languages widely support it, are compatible with web technologies, and are straightforward for humans and machines to work with.

[Data storage and exchange](#contents.xhtml_sc172a)

JSON is commonly used for storing and exchanging data between different Linux applications and systems. It provides a structured and human-readable format that various programming languages can easily process. JSON is often used in log files, databases, message queues, and other data storage or communication mechanisms.

For example, when working with databases like MongoDB in Linux, data is often stored and queried in JSON-like Binary JSON (BSON) format. This allows seamless integration between the database and applications running on Linux.

JSON’s simplicity, flexibility, and compatibility have made it a popular choice for data representation and interchange in Linux systems. Its widespread adoption and support across programming languages and tools make it a versatile format for configuration files, API communication, data processing, and data storage in the Linux ecosystem.

[Syntax](#contents.xhtml_sc173a)

JSON syntax is based on JavaScript object notation, but various programming languages are language-independent and widely support it. JSON data consists of key-value pairs enclosed in curly braces ({}) or arrays enclosed in square brackets ([]). Here is an example of a simple JSON object:

{

"name": "John",

"age": 30,

"city": "New York"

}

In the above example, name, age, and city are keys, and John, 30, and New York are the corresponding values.

[Data types](#contents.xhtml_sc174a)

JSON supports several data types; they are as follows:

*   Strings: Enclosed in double quotes ("").
*   Numbers: Integer or floating-point numbers.
*   Booleans: True or false.
*   Arrays: Ordered collections of values enclosed in square brackets ([]).
*   Objects: Unordered collections of key-value pairs enclosed in curly braces ({}).
*   Null: A special value representing empty or null data.
*   Nested structures: JSON allows the nesting of objects and arrays to create complex data structures. Objects can contain other objects or arrays as values. Here is an example of a nested JSON object:

{

"name": "John",

"age": 30,

"address": {

"street": "123 Main St",

"city": "New York"

},

"hobbies": ["reading", "hiking", "cooking"]

}

In the above example, the address key contains an object with nested key-value pairs, and the hobbies key contains an array of values.

[JSON arrays](#contents.xhtml_sc175a)

JSON arrays allow you to store ordered lists of values. Each value in the array can be of any valid JSON data type. Here is an example of a JSON array:

["apple", "banana", "orange"]

Arrays can also contain objects or nested arrays:

[

{"name": "John", "age": 30},

{"name": "Jane", "age": 25},

["apple", "banana", "orange"]

]

In the below example, name, age, and city are keys, and John, 30, and New York are the corresponding values:

{

"name": "John",

"age": 30,

"city": "New York"

}

[Configuration files](#contents.xhtml_sc176a)

Many Linux applications and services use JSON for their configuration files. These files store settings, options, and parameters that define the application’s behavior. Examples of applications that use JSON for configuration include web servers like Nginx, databases like MongoDB, and other software services.

Here is an example of a JSON configuration file for a hypothetical application:

{

"server": {

"port": 8080,

"max_connections": 100,

"log_level": "debug"

},

"database": {

"host": "localhost",

"port": 27017,

"username": "admin",

"password": "secretpassword"

}

}

In the above example, the JSON configuration file defines server and database settings, including port numbers, connection limits, logging levels, and authentication details.

[API communication](#contents.xhtml_sc177a)

JSON is commonly used for communication between Linux applications and APIs. Many web services expose APIs that accept and return data in JSON format. Linux applications can send HTTP requests to these APIs, passing JSON payloads as request bodies or receiving JSON responses. This enables seamless integration and data exchange between different systems.

For example, when using the cURL command-line tool in Linux to interact with a RESTful API, you can send a POST request with a JSON payload like this:

$ curl -X POST -H "Content-Type: application/json" -d '{"name": "John", "age": 30}' https://api.example.com/users

In this example, a JSON object representing user data is sent as the request payload to the specified API endpoint.

[Data processing and manipulation](#contents.xhtml_sc178a)

Linux provides various command-line tools that can process and manipulate JSON data. Tools like jq allow you to filter, transform, and extract specific data from JSON documents. These tools are useful for scripting, automation, and data processing tasks in Linux.

Here is an example of using jq to filter and extract specific data from a JSON file:

$ cat data.json | jq '.users[] | select(.age > 25) | .name'

This command reads a JSON file (data.json), filters the array of users based on the age condition (> 25), and extracts the names of users matching the criteria.

[Ansible](#contents.xhtml_sc179a)

Ansible is an open-source automation tool that simplifies the management and configuration of systems, applications, and networks. It follows a declarative approach, allowing you to define the desired state of your infrastructure, and Ansible takes care of the necessary steps to achieve that state. Let us have a detailed explanation of Ansible and its key concepts.

[Architecture](#contents.xhtml_sc180a)

Ansible operates in a client-server model, where the controlling machine (often called the control node) manages and orchestrates the managed hosts. The control node can be any machine, typically a Linux server, where Ansible is installed and used to define and execute automation tasks. The managed hosts are the machines or devices Ansible manages and configures.

[Inventory](#contents.xhtml_sc181a)

Ansible uses an inventory file defining the managed hosts and categorizing them. The inventory file is written in INI or YAML format and can be customized to match your infrastructure. It allows you to specify information about hosts, such as IP addresses, hostnames, connection details, and group associations.

[Playbooks](#contents.xhtml_sc182a)

Playbooks are the heart of Ansible automation. They are written in YAML format and define a set of tasks that Ansible executes on the managed hosts. Playbooks allow you to describe the desired state of your systems, including configuration, deployment, and management tasks. Each playbook consists of one or more plays, which consist of tasks to be executed on a group of hosts.

[Modules](#contents.xhtml_sc183a)

Ansible provides a wide range of modules that enable you to perform specific actions on managed hosts. Modules are pre-written scripts or programs that Ansible executes to carry out tasks. They cover a broad spectrum of operations, including system administration, configuration management, network management, file manipulation, package installation, and more. Ansible ships with a large collection of built-in modules, and you can create custom modules.

[Tasks and plays](#contents.xhtml_sc184a)

A task is a single action Ansible performs, defined within a playbook. Tasks typically map to a specific module and its parameters. For example, a task might use the apt module to install a package or the file module to manage files and directories. Tasks can also include conditionals, loops, and handlers to handle specific scenarios and manage changes efficiently.

A play is a collection of related tasks executed on a specific group of hosts. Plays allow you to group tasks logically and define the target hosts for those tasks.

[Roles](#contents.xhtml_sc185a)

Roles are a way to organize and encapsulate related tasks, files, templates, and variables into reusable units. Roles provide a modular and reusable approach to organizing complex automation tasks. They allow you to create structured and reusable components that can be shared across multiple playbooks and projects.

[Ad-hoc commands](#contents.xhtml_sc186a)

Ansible provides ad-hoc commands that allow you to perform quick tasks on managed hosts without writing a full playbook. Ad-hoc commands are useful for one-off tasks, troubleshooting, or performing simple tasks directly from the command line.

[Ansible galaxy](#contents.xhtml_sc187a)

Ansible galaxy is a community-driven platform where you can find and share pre-built roles, playbooks, and collections. It offers a vast collection of reusable automation content created by the Ansible community, allowing you to leverage existing solutions and accelerate your automation efforts.

[Installing and configuring Ansible](#contents.xhtml_sc188a)

The following steps for installing and configuring Ansible are as follows:

Step 1: Installing Ansible

Ensure you have a Linux machine (such as Ubuntu, CentOS, or Fedora) where you want to install Ansible. Open a terminal or SSH into the Linux machine.

Install Ansible using the package manager specific to your Linux distribution. For example, if you are using Ubuntu or Debian, run the following command:

sudo apt install ansible

If you are using CentOS or Fedora, use the following command:

sudo yum install ansible

Step 2: Configuring the inventory

The inventory file specifies the managed hosts and groups. By default, Ansible looks for the inventory file at /etc/ansible/hosts. You can create this file manually or use an existing file.

Open the inventory file using a text editor:

sudo nano /etc/ansible/hosts

Add the IP addresses or hostnames of the machines you want to manage. For example:

[webservers]

192.168.11.10

192.168.11.11

[databases]

192.168.11.12

Step 3: Running ad-hoc commands

Ad-hoc commands are useful for quick tasks without creating a playbook. Let us try running a simple command on all the managed hosts. For example, to check the uptime of all the machines, use the following command:

ansible all -m command -a "uptime"

The all parameter refers to all the hosts defined in the inventory.

Step 4: Creating a playbook

Playbooks are written in YAML format. They allow you to define the desired state of your systems. Create a new file, such as webserv.yaml, using a text editor:

nano webserv.yaml

In the playbook, define the hosts, tasks, and actions. For example, the following playbook installs the Apache web server on the specified hosts:

---

- name: Install Apache

hosts: webservers

become: true

tasks:

- name: Install Apache

apt:

name: apache2

state: present

become: true

In this example, the playbook specifies that the tasks should run on the hosts belonging to the webservers group. The become: true directive allows the task to run with escalated privileges.

Step 5: Running the playbook

To execute the playbook, use the ansible-playbook command followed by the playbook file name:

ansible-playbook webserver.yaml

[Real-world examples of Ansible in network environment](#contents.xhtml_sc189a)

We can also use Ansible to configure network equipment such as routers, switches, etc.

To configure network switches using Ansible, you must ensure that your switches support remote management via SSH or an API with which Ansible can interact. Here is an overview of the steps involved:

Step 1: Create an inventory file

Create an inventory file (our example uses the name host-file) that lists the network switches you want to configure. Specify the hostnames or IP addresses of the switches and assign them to a group if needed. For example:

[switches]

AUR-K-Dorms ansible_host=10.160.55.9

AUR-PHS-APS ansible_host=10.160.55.18

Refer to [Figure 8.1](#ch08.xhtml_fig8-1):

![A picture containing text, screenshot, font Description automatically generated](images/Figure_8.1.jpg)

Figure 8.1: Output of the /etc/ansible/inventory/host-file configuration file

Another way to define a list of switches is by using the following syntax, as shown in [Figure 8.2](#ch08.xhtml_fig8-2):

![A screen shot of a computer Description automatically generated with medium confidence](images/Figure_8.2.jpg)

Figure 8.2: Output of the /etc/ansible/inventory/hostfile_1 and hostfile_2, respectively

Note: Specific details in the above text, as well as [Figure 8.1](#ch08.xhtml_fig8-1) and [Figure 8.2](#ch08.xhtml_fig8-2) have been intentionally concealed to prevent any inadvertent disclosure of sensitive information.

Ensure that Ansible can connect to the switches via SSH or other supported connection methods. You may need to configure SSH key-based authentication or provide login credentials in the inventory file.

Step 2: Create a playbook

Create a playbook (for example, switch_config.yaml) to define the configuration tasks you want to perform on the switches. Here is an example playbook that configures a VLAN on the switches:

---

- name: Configure VLAN on switches

hosts: switches

gather_facts: false

tasks:

- name: Configure VLAN 500

ios_command:

commands:

- vlan 500

- name MyVLAN

register: vlan_output

- name: Save configuration

ios_command:

commands: write memory

In this example, the playbook uses the ios_command module to send configuration commands to the switches. Modify the tasks based on the specific commands required for your switches.

Step 3: Run the playbook

Execute the playbook using the ansible-playbook command:

ansible-playbook switch_config.yaml -i host-file

Ansible will connect to the switches, execute the tasks defined in the playbook, and apply the desired configurations. It will report any changes made or errors encountered during the process.

You can create more complex playbooks to configure additional settings on the switches, such as interfaces, routing protocols, ACLs, and more. Ansible provides various modules and plugins specific to different network vendors, allowing you to interact with multiple switches.

| Note: | Consult the documentation and specific network vendor modules to understand the options and requirements for configuring your switches. Exercise caution and thoroughly test any configuration changes before applying them to production environments. |

Ansible will connect to the managed hosts, execute the tasks defined in the playbook, and report the results.

These steps provide a basic understanding of installing Ansible, configuring the inventory, running ad-hoc commands, and creating and executing a simple playbook. The official Ansible documentation and tutorials are excellent resources to deepen your knowledge of Ansible and its capabilities.

[Conclusion](#contents.xhtml_sc190a)

This chapter explored the automation concept in a Linux environment, delving into the various tools and techniques available. We discussed the importance of scripting, scheduling tasks, and using command-line tools to automate repetitive tasks and improve efficiency. In the next chapter, we will focus on addressing common challenges and troubleshooting within a Linux environment, equipping you with the knowledge and strategies to overcome issues that may arise.

Join our book’s Discord space

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 9Troubleshooting Network and System Issues](#contents.xhtml_ch09a)

[Introduction](#contents.xhtml_sc191a)

In the last chapter, we covered automation, firstly looking at YAML, followed up with JSON, and finally wrapped with Ansible. In this chapter, we will focus on common issues found within a Linux environment. Here, we will delve into the challenges that often arise and explore effective strategies to resolve them. Throughout this chapter, we will delve into a wide range of essential commands that are instrumental in diagnosing network issues and monitoring system performance. From commands like ping, traceroute, and netstat to tools like Nmap, dig, and vmstat, you will gain mastery over these powerful tools. By gaining insights into these common issues and learning the troubleshooting techniques, you will be equipped with the knowledge and skills to overcome obstacles and maintain a robust Linux environment.

[Structure](#contents.xhtml_sc192a)

In this chapter, we will discuss the following topics:

*   Network troubleshooting
*   Memory troubleshooting
*   Hard disk troubleshooting
*   Troubleshooting boot issues

[Objectives](#contents.xhtml_sc193a)

In this chapter, we will explore various essential commands for network diagnostics and system monitoring. This includes learning how to use commands like ping, ping6, traceroute, traceroute6, netstat, tracepath, nmap, dig, whois, hostname, free, vmstat, swapon, smartctl, fsck, and update-grub. Mastering these commands, you will be equipped with the necessary tools to diagnose network issues, monitor system performance, and manage various aspects of your Linux environment.

[Network troubleshooting](#contents.xhtml_sc194a)

We can use several tools to aid us in troubleshooting a network connection issue ranging from GUI utilities to command-line tools. Our focus will be troubleshooting using the command-line tools available to us.

[The ping command](#contents.xhtml_sc195a)

The ping utility uses the ICMP protocol to send requests and receive replies. We can use the ping utility to test basic reachability between systems locally or out on the internet. The basic syntax for the ping utility is:

ping <DNS name or IPv4>

Based on the above, we can try out the ping utility as shown below:

root@philip-virtual-machine:/home/philip# ping Fedora

PING Fedora (172.16.175.129) 56(84) bytes of data.

64 bytes from Fedora (172.16.175.129): icmp_seq=1 ttl=64 time=0.299 ms

64 bytes from Fedora (172.16.175.129): icmp_seq=2 ttl=64 time=0.341 ms

64 bytes from Fedora (172.16.175.129): icmp_seq=3 ttl=64 time=0.733 ms

64 bytes from Fedora (172.16.175.129): icmp_seq=4 ttl=64 time=0.957 ms

64 bytes from Fedora (172.16.175.129): icmp_seq=5 ttl=64 time=0.224 ms

^C

--- Fedora ping statistics ---

6 packets transmitted, 6 received, 0% packet loss, time 5064ms

rtt min/avg/max/mdev = 0.224/0.564/0.957/0.287 ms

root@philip-virtual-machine:/home/philip#

The ping utility will run until it is stopped by the user using Ctrl+C; this is different in a Windows environment where only 4 ICMP echo requests/replies are seen.

[The ping6 command](#contents.xhtml_sc196a)

It is also possible to test for potential connectivity issues for IPv6\. We would use the ping6 command; the syntax for the ping6 command is:

ping6 <DNS name or IPv6>

Based on the above, we would simply need to specify the target system’s DNS name or IPv6 address. Here is how we use the ping6 command as shown below:

root@philip-virtual-machine:/home/philip# ping6 2001:db8:0:f101::3

PING 2001:db8:0:f101::3(2001:db8:0:f101::3) 56 data bytes

64 bytes from 2001:db8:0:f101::3: icmp_seq=1 ttl=64 time=0.355 ms

64 bytes from 2001:db8:0:f101::3: icmp_seq=2 ttl=64 time=0.289 ms

64 bytes from 2001:db8:0:f101::3: icmp_seq=3 ttl=64 time=0.222 ms

64 bytes from 2001:db8:0:f101::3: icmp_seq=4 ttl=64 time=0.596 ms

^C

--- 2001:db8:0:f101::3 ping statistics ---

4 packets transmitted, 4 received, 0% packet loss, time 3052ms

rtt min/avg/max/mdev = 0.222/0.365/0.596/0.142 ms

root@philip-virtual-machine:/home/philip#

[The traceroute command](#contents.xhtml_sc197a)

We can use the traceroute command to test for potential connectivity issues. The traceroute command displays each device in the path to the destination system; each device is considered a hop. The basic syntax for the traceroute is:

traceroute <DNS name or IPv4>

We would simply need to specify either the DNS name or IPv4 address of the target system, as shown below:

root@philip-virtual-machine:/home/philip# traceroute Fedora

Command 'traceroute' not found, but can be installed with:

apt install inetutils-traceroute

apt install traceroute

root@philip-virtual-machine:/home/philip# apt-install inetutils-traceroute

update-alternatives: using /usr/bin/inetutils-traceroute to provide /usr/bin/traceroute (traceroute) in auto mode

Processing triggers for man-db (2.8.3-2) ...

root@philip-virtual-machine:/home/philip#

The traceroute utility is not installed by default in Ubuntu 18; we quickly remedied this by installing the inetutils-traceroute package. Now let us try to run the traceroute command once again, as shown below:

root@philip-virtual-machine:/home/philip# traceroute Fedora

traceroute to Fedora (172.16.175.129), 64 hops max

1 172.16.175.129 0.199ms 0.199ms 0.251ms

root@philip-virtual-machine:/home/philip#

We can see that the device is one hop away from the Ubuntu system.

[The traceroute6 command](#contents.xhtml_sc198a)

It is also possible to test for potential bottlenecks between systems for IPv6 using the traceroute6 command. The basic syntax for the traceroute6 command is:

traceroute6 <DNS name or IPv6>

We would simply specify the target system’s DNS name or IPv6 address. Here is how we would use the traceroute6 command as shown below:

root@philip-virtual-machine:/home/philip# traceroute6 2001:db8:0:f101::2

traceroute to 2001:db8:0:f101::2 (2001:db8:0:f101::2) from 2001:db8:0:f101::1, 30 hops max, 24 byte packets

sendto: Invalid argument

1 traceroute: wrote 2001:db8:0:f101::2 24 chars, ret=-1

^C

root@philip-virtual-machine:/home/philip#

We see the traceroute6 command works similarly to that of the traceroute command.

[The netstat command](#contents.xhtml_sc199a)

We can use the netstat command to troubleshoot a number of different issues. Earlier in this chapter, we saw that we would pass the -r option to view the routing table when we covered routing. Well, we can also use the netstat command to view active connections. This is especially useful in server environments when we run various programs utilizing various ports; these ports could be either TCP or UDP ports. We can pass the -n option, which shows numerical address(s), the -t option, which offers TCP connections, the -l, which shows what sockets are listening, and the -p option, which shows the program ID and program name. These options work well together when trying to narrow down your TCP ports. Here is how this would look for TCP:

root@philip-virtual-machine:/home/philip# netstat -ntlp

Active Internet connections (only servers)

Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name

tcp 0 0 0.0.0.0:514 0.0.0.0:* LISTEN 26840/rsyslogd

tcp 0 0 127.0.0.53:53 0.0.0.0:* LISTEN 418/systemd-resolve

tcp 0 0 0.0.0.0:22 0.0.0.0:* LISTEN 26189/sshd

tcp 0 0 127.0.0.1:631 0.0.0.0:* LISTEN 6548/cupsd

tcp6 0 0 :::514 :::* LISTEN 26840/rsyslogd

tcp6 0 0 :::22 :::* LISTEN 26189/sshd

tcp6 0 0 ::1:631 :::* LISTEN 6548/cupsd

root@philip-virtual-machine:/home/philip#

We see several programs running, including dns, sshd, and ryslogd, to name a few. Similarly, we can view UDP connections; we would pass the nulp options, the -u means UDP, as shown below:

root@philip-virtual-machine:/home/philip# netstat -nulp

Active Internet connections (only servers)

Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name

udp 8448 0 127.0.0.53:53 0.0.0.0:* 418/systemd-resolve

udp 0 0 0.0.0.0:631 0.0.0.0:* 6550/cups-browsed

udp 34112 0 0.0.0.0:5353 0.0.0.0:* 607/avahi-daemon: r

udp 0 0 0.0.0.0:48456 0.0.0.0:* 607/avahi-daemon: r

udp6 0 0 :::59636 :::* 607/avahi-daemon: r

udp6 33152 0 :::5353 :::* 607/avahi-daemon: r

root@philip-virtual-machine:/home/philip#

We see many services listening for a connection, systemd-resolve (port 53) being one of them.

[The tracepath command](#contents.xhtml_sc200a)

The tracepath command is another method for testing potential bottlenecks between systems. It works similar to the traceroute command. The basic syntax for the tracepath command is:

tracepath <DNS name or IPv4>

We simply need to specify the DNS name or IPv4 address to use the tracepath command. This can be shown below:

root@philip-virtual-machine:/home/philip# tracepath Fedora

1?: [LOCALHOST] pmtu 1500

1: Fedora 0.309ms reached

1: Fedora 0.201ms reached

Resume: pmtu 1500 hops 1 back 1

root@philip-virtual-machine:/home/philip#

The pmtu or Path MTU is shown in addition to number of hop(s) to the destination device.

[The tracepath -6 command](#contents.xhtml_sc201a)

Like the tracepath command, the tracepath with the -6 option is another method for testing potential bottlenecks between systems using IPv6 addressing. The basic syntax for the tracepath with the -6 option is:

tracepath -6 <DNS name or IPv6>

We must specify the DNS name or IPv6 address to use the tracepath with the -6 option. This can be shown below:

root@philip-virtual-machine:/home/philip# tracepath -6 2001:db8:0:f101::3

1?: [LOCALHOST] 0.012ms pmtu 1500

1: 2001:db8:0:f101::3 0.384ms reached

1: 2001:db8:0:f101::3 0.352ms reached

Resume: pmtu 1500 hops 1 back 1

root@philip-virtual-machine:/home/philip#

We can see that the tracepath with the -6 option works like the tracepath command for IPv4.

[The nmap command](#contents.xhtml_sc202a)

The Network Mapper (nmap) can also troubleshoot potential connection issues using the nmap command; this command scans a given system and displays services and their respective port numbers, which are open for the system specified with the nmap command. The basic syntax for the nmap command is:

nmap <option> <IP of destination>

We would specify the option and the IP of the destination system, which we are troubleshooting as shown below:

root@Linuxplus:/home/philip# nmap -A -T4 172.16.175.129

Nmap scan report for Fedora (172.16.175.129)

Host is up (0.00066s latency).

Not shown: 845 closed ports, 154 filtered ports

PORT STATE SERVICE VERSION

22/tcp open ssh OpenSSH 7.7 (protocol 2.0)

| ssh-hostkey:

| 2048 b8:02:f8:79:f4:d8:77:b4:26:de:70:93:e8:66:94:69 (RSA)

| 256 9b:e0:d1:33:3b:08:02:bf:fd:c6:48:c1:47:7d:9c:9e (ECDSA)

|_ 256 cd:f8:47:d1:75:95:e3:59:f3:b6:c0:12:a0:8b:d1:0e (EdDSA)

MAC Address: 00:0C:29:04:35:BD (VMware)

Device type: general purpose

Running: Linux 3.X|4.X

OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4

OS details: Linux 3.10 - 4.8

Network Distance: 1 hop

TRACEROUTE

HOP RTT ADDRESS

1 0.66 ms Fedora (172.16.175.129)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .

Nmap done: 1 IP address (1 host up) scanned in 49.30 seconds

root@Linuxplus:/home/philip#

We can see which service and their respective port number is running on the destination system. The -A option is to display OS and version detection; the -T4 option is used for faster execution. You should seek permission from the owner or administrator of the destination system or network before running the nmap command; this is true, especially in corporate environments where they are policies governing the use of a given network.

| Note: | Always seek permission before performing any kind of port scans in a network. |

The dig command

So far, we have been looking at ways of troubleshooting connectivity issues, but DNS issues could pose a risk too. We can use the dig utility to perform a domain’s DNS lookups. The basic syntax for the dig command is:

dig <domain>

We would simply specify the domain we want to perform a lookup against.

Here is how we would perform a simple look-up:

root@philip-virtual-machine:/home/philip# dig www.ding.com

; <<>> DiG 9.11.3-1ubuntu1-Ubuntu <<>> www.ding.com

;; global options: +cmd

;; Got answer:

;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39472

;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:

; EDNS: version: 0, flags:; udp: 512

;; QUESTION SECTION:

;www.ding.com. IN A

;; ANSWER SECTION:

www.ding.com. 14037 IN CNAME car.ding.com.

car.ding.com. 14049 IN A 88.166.179.231

;; Query time: 77 msec

;; SERVER: 8.8.8.8#53(8.8.8.8)

;; WHEN: Wed Mar 06 16:21:23 -04 2023

;; MSG SIZE rcvd: 83

root@philip-virtual-machine:/home/philip#

We can see the DNS record for the given domain; particularly the A records. The server which answered our query is the 8.8.8.8, which we configured in the /etc/resolv.conf. However, we can use a different DNS server by passing the @ with the dig command, as shown below:

root@philip-virtual-machine:/home/philip# dig @8.8.4.4 ding.com

; <<>> DiG 9.11.3-11-Ubuntu <<>> @8.8.4.4 ding.com

; (1 server found)

;; global options: +cmd

;; Got answer:

;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16754

;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:

; EDNS: version: 0, flags:; udp: 512

;; QUESTION SECTION:

;ding.com. IN A

;; ANSWER SECTION:

ding.com. 21599 IN A 88.166.179.239

;; Query time: 116 msec

;; SERVER: 8.8.4.4#53(8.8.4.4)

;; WHEN: Wed Mar 06 16:25:29 -04 2023

;; MSG SIZE rcvd: 57

root@philip-virtual-machine:/home/philip#

We have specified a different DNS server to answer our query. Adding to this, we can also look for a particular DNS information such as the name server or NS, by passing NS with the dig command as shown below:

root@philip-virtual-machine:/home/philip# dig @8.8.4.4 ding.com NS

; <<>> DiG 9.11.3-1ubuntu1-Ubuntu <<>> @8.8.4.4 ding.com NS

; (1 server found)

;; global options: +cmd

;; Got answer:

;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 40936

;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:

; EDNS: version: 0, flags:; udp: 512

;; QUESTION SECTION:

;ding.com. IN NS

;; ANSWER SECTION:

ding.com. 21599 IN NS dns2.easydns.net.

ding.com. 21599 IN NS dns3.easydns.org.

ding.com. 21599 IN NS dns4.easydns.info.

ding.com. 21599 IN NS dns1.easydns.com.

;; Query time: 105 msec

;; SERVER: 8.8.4.4#53(8.8.4.4)

;; WHEN: Wed Mar 06 16:26:06 -04 2023

;; MSG SIZE rcvd: 159

root@philip-virtual-machine:/home/philip#

We see the name servers for the given domain.

[The whois command](#contents.xhtml_sc203a)

It is also possible to gain information for a domain using the whois command. The basic syntax for the whois command is:

whois <domain>

Based on the above, we can simply pass a domain name with the whois command and get valuable information for a given domain, as shown below:

root@Linuxplus:/home/philip# whois ding.com

Domain Name: DING.COM

Registry Domain ID: 97706392_DOMAIN_COM-VRSN

Registrar WHOIS Server: whois.easydns.com

Registrar URL: http://www.easydns.com

Updated Date: 2015-08-10T20:01:35Z

Creation Date: 2003-05-09T14:34:02Z

Registry Expiry Date: 2024-05-09T14:34:02Z

Registrar: easyDNS Technologies, Inc.

Registrar IANA ID: 469

Registrar Abuse Contact Email:

Registrar Abuse Contact Phone:

Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited

Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited

Name Server: DNS1.EASYDNS.COM

Name Server: DNS2.EASYDNS.NET

Name Server: DNS3.EASYDNS.ORG

Name Server: DNS4.EASYDNS.INFO

You have 20 lookups left today

root@Linuxplus:/home/philip#

Some output was omitted for brevity. Based on the above, we are given a wealth of information for the given domain.

[The hostname command](#contents.xhtml_sc204a)

This command is simply used for setting or returning the DNS name of the system and the IP address of the system. The basic syntax is:

hostname <options> <new hostname>

If we simply enter the hostname command, it will yield the following:

root@philip-virtual-machine:/home/philip# hostname

philip-virtual-machine

root@philip-virtual-machine:/home/philip#

Based on the above, we can see the DNS name of the system. We can also pass the -i option to view the IP associated with the hostname,  as shown below:

root@philip-virtual-machine:/home/philip# hostname -i

127.0.1.1

root@philip-virtual-machine:/home/philip#

We see an IP from the loopback range of 127.0.0.0/8. We can change the hostname by passing a new hostname value, as shown below:

root@philip-virtual-machine:/home/philip# hostname Linuxplus

root@philip-virtual-machine:/home/philip# hostname

Linuxplus

root@philip-virtual-machine:/home/philip#

We see that the hostname command indicates that the hostname has been changed, but it has not updated the prompt. We can exit out of root and sign back in and will see the changes as shown below:

root@philip-virtual-machine:/home/philip# exit

exit

philip@philip-virtual-machine:~$ sudo su

[sudo] password for philip:

root@Linuxplus:/home/philip#

We can see that the hostname was changed to reflect the name we specified. However, when we rebooted the system, the hostname was set back to the value specified in the /etc/hostname file, as shown below:

root@Linuxplus:/home/philip# cat /etc/hostname

philip-virtual-machine

root@Linuxplus:/home/philip#reboot

root@philip-virtual-machine:/home/philip# cat /etc/hostname

philip-virtual-machine

root@philip-virtual-machine:/home/philip# hostname Linuxplus

We can fix this by editing the /etc/hostname file using a text editor such as vi or nano and placing the value, as shown below:

root@philip-virtual-machine:/home/philip#cat /etc/hostname

Linuxplus

root@philip-virtual-machine:/home/philip# reboot

root@Linuxplus:/home/philip#

[Memory troubleshooting](#contents.xhtml_sc205a)

When troubleshooting memory issues in Linux, the following steps can help you identify and resolve potential problems:

1.  Checking memory usage:

Start by checking the overall memory usage of your system. Use the free command to display information about available and used memory:

free -h

This command provides an overview of the total, used, free memory, and swap usage. Look for any significant memory consumption or low available memory.

2.  Identifying memory-hungry processes:

Use the top or htop command to identify processes that consume significant memory. Sort the processes by memory usage to see the most memory-hungry ones at the top:

top

or

htop

Take note of any processes using a large amount of memory, as they may contribute to memory issues.

3.  Analyzing memory usage per process:

To get a detailed breakdown of memory usage per process, use the ps command with the --sort and --size options:

ps aux --sort -rss

This command lists processes in descending order based on their Resident Set Size (RSS), representing the non-swapped physical memory used by a process. Look for processes with unusually high RSS values.

4.  Checking system logs:

Examine the system logs for any relevant information about memory-related issues. The main log file to check is /var/log/syslog or /var/log/messages. Use the grep command to filter the log file based on relevant keywords:

grep -i "memory" /var/log/syslog

Look for any error messages, warnings, or events related to memory.

5.  Monitoring memory in real-time:

Use tools like vmstat or sar to monitor memory usage in real-time and track changes over time. For example, to monitor memory statistics at regular intervals, use the following command:

vmstat 1

This provides a snapshot of memory usage, including information about free memory, used memory, swap activity, and more. Monitor the output for any abnormalities or trends that might indicate memory issues.

6.  Checking swap space:

Insufficient swap space can also lead to memory-related problems. Use the swapon command to check the current swap usage:

swapon –show

If you notice high swap usage or lack of space, you may need to adjust your swap configuration or investigate further to identify memory-hungry processes.

7.  Optimizing memory usage:

Consider optimizing memory usage by reviewing and adjusting system settings, such as adjusting the swappiness value, tuning kernel parameters, or optimizing applications and services running on your system. It may be helpful to consult relevant documentation and resources specific to your Linux distribution.

Following these steps, you can gather information about memory usage, identify memory-hungry processes, analyze memory usage per process, check system logs, monitor memory in real time, and optimize memory settings to troubleshoot and resolve memory-related issues in Linux.

[Hard disk troubleshooting](#contents.xhtml_sc206a)

To troubleshoot hard disk issues in Linux using the terminal, you can follow these steps:

1.  Checking disk health:

Start by checking the health of your hard disk. Linux provides several tools for this purpose. One commonly used tool is smartctl, which interacts with the Self-Monitoring, Analysis, and Reporting Technology (SMART) system built into most modern hard drives. Install the smartmontools package if it is not already installed:

sudo apt install smartmontools

Then, use the smartctl command to check the disk’s overall health status:

sudo smartctl -a /dev/sdX

Replace /dev/sdX with the appropriate device name for your hard disk (for example, /dev/sda). Look for attributes indicating disk health, such as SMART overall-health self-assessment test result or SMART overall-health self-assessment test status. If there are any warnings or errors, it may indicate a potential issue with the disk.

2.  Checking disk partitions:

Verify the disk partitions using the lsblk or fdisk command. Run the following command to list the available block devices and their partitions:

lsblk

or

sudo fdisk -l

Review the output to ensure the disk and its partitions are detected correctly. Look for any anomalies or unexpected disk states.

3.  Verifying disk mounts:

Check if the disk is properly mounted and accessible. Use the mount command to list all mounted filesystems:

mount

Ensure that the disk’s filesystem is mounted correctly and that there are no read-only mounts or other errors. If the disk is not mounted, you can mount it manually using the mount command.

4.  Analyzing disk usage:

Disk space issues can cause performance problems. Use the df command to check the disk space usage:

df -h

This command displays the disk usage for all mounted filesystems. Pay attention to the Used and Available columns to identify potential disk space constraints.

5.  Checking filesystem integrity:

Filesystem errors can lead to disk-related issues. Run a filesystem check using the appropriate tool for your filesystem type. For example, to check an ext4 filesystem, use the e2fsck command:

sudo e2fsck -f /dev/sdX

Replace /dev/sdX with the appropriate device name. If errors are detected, the command will attempt to fix them. Note that you may need to unmount the filesystem before running the filesystem check.

6.  Analyzing system logs:

Review the system logs for any disk-related error messages or warnings. The main log file to check is /var/log/syslog or /var/log/messages. Use the grep command to filter the log file based on relevant keywords:

grep -i "disk" /var/log/syslog

Look for any error messages, I/O errors, or events related to disk issues.

7.  Monitoring disk I/O:

To monitor disk I/O activity in real-time, use tools like iotop or iostat. Install the iotop package if it is not already installed:

sudo apt install iotop

Then, run the following command to monitor disk I/O:

sudo iotop

This command displays a live view of processes and their disk I/O usage. It helps identify processes causing high disk utilization or excessive read/write operations.

8.  Troubleshooting hardware connections:

If you suspect a hardware issue, ensure the disk is correctly connected to your system. Check the cables and connections to ensure they are secure and properly seated. You may also consider trying a different cable or connecting the disk to a different port.

Following these steps, you can check the disk health, verify disk partitions and mounts, analyze disk usage, check filesystem integrity, review system logs, monitor disk I/O, and troubleshoot hardware connections. Remember to take appropriate precautions when working with disks and regularly back up your important data to avoid loss.

[Troubleshooting boot issues](#contents.xhtml_sc207a)

When troubleshooting boot problems in Linux using the terminal, you can follow these steps:

1.  Analyzing error messages:

    When encountering boot issues, carefully read any error messages displayed on the screen. Take note of specific error codes or messages that can provide clues about the problem.

2.  Grub bootloader issues:

    If you encounter issues with the GRUB bootloader, try the following steps:

    1.  Check if the GRUB menu is displayed during boot. If not, try pressing the Shift or Esc key repeatedly after powering your computer to access the GRUB menu.
    2.  If you see the GRUB menu but the system fails to boot, select the recovery or fallback option if available. This can help bypass potential issues.
    3.  If the bootloader configuration is corrupted, you may need to manually edit the GRUB configuration file. In Ubuntu-based distributions, the file is located at /etc/default/grub.
    4.  After modifying the configuration, update GRUB using the following command:

         sudo update-grub

3.  Checking disk issues:

    Disk problems can prevent the system from booting. Use the fsck command to check the filesystem integrity and repair any errors. For example, to check the root filesystem:

    sudo fsck /dev/sda1

    Replace /dev/sda1 with the appropriate device and partition for your root filesystem.

4.  Verifying filesystem mounts:

    Ensure that all necessary filesystems are correctly mounted. Use the mount command to check the mounted filesystems. Look for any errors or missing mounts:

    mount

5.  Analyzing system logs:

    Examine the system logs for error messages or warnings related to the boot process. The main log file to check is /var/log/syslog or /var/log/messages. Use the grep command to filter the log file based on relevant keywords:

    grep -i "error" /var/log/syslog

    Look for any messages indicating disk errors, service failures, or other issues during the boot process.

6.  Verbose boot logging:

    Enable verbose boot logging to get more detailed information about the boot process. Edit the GRUB configuration file (for example, /etc/default/grub) and add the quiet splash parameters to the GRUB_CMDLINE_LINUX_DEFAULT line. Remove the quiet option and add debug to get additional debug information. After saving the changes, update GRUB:

    sudo update-grub

7.  Checking system services:

    Ensure that critical system services are running correctly. Use the systemctl command to check the status of services. For example, to check the status of the networking service:

    systemctl status networking

    Look for any failed services or services that are not running.

8.  Booting into single user mode:

    If the system fails to boot, you can try booting into single-user mode to diagnose and fix the issue. During the GRUB boot menu, select the Linux kernel entry and press the e key to edit the boot parameters. Add single or init=/bin/bash at the end of the line, starting with linux or linuxefi. Press Ctrl+X or F10 to boot with the modified parameters. This will boot the system into a root shell, allowing you to perform troubleshooting steps or make necessary repairs.

9.  Hardware issues:

    If you suspect hardware problems, check hardware connections and ensure all components function properly. Use appropriate diagnostic tools to test your hardware, such as RAM or hard drives.

Following these steps, you can analyze error messages, address GRUB bootloader issues, check disk integrity, verify filesystem mounts, analyze system logs, enable verbose boot logging, check system services, boot into single-user mode, and identify potential hardware issues. Remember to exercise caution and make backups before repairing or modifying critical system files.

[Conclusion](#contents.xhtml_sc208a)

In this chapter, we covered various issues commonly faced and methods of dealing with each issue encountered within a Linux environment.

In the next chapter, we will wrap up our journey with two mock exams.

Join our book’s Discord space

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 10Mock Exams](#contents.xhtml_ch10a)

[Introduction](#contents.xhtml_sc209a)

In the previous chapter, we covered various issues commonly faced and methods of dealing with each issue encountered within a Linux environment. In this chapter, we will wrap up our journey with two mock exams.

[Mock exam 1](#contents.xhtml_sc210a)

1.  Which letter lists the partitions of a hard disk without going into the fdisk utility?

    1.  fdisk –a /dev/sda
    2.  fdisk –c /dev/sda
    3.  fdisk –l /dev/sda
    4.  fdisk –r /dev/sda

    Answer: C

2.  Which letter is used to create a partition inside the fdisk utility?

    1.  b
    2.  c
    3.  r
    4.  n

    Answer: D

3.  Which letter is used to toggle a boot flag inside the fdisk utility?

    1.  b
    2.  a
    3.  d
    4.  c

    Answer: B

4.  Which letter prints the known partition types inside the fdisk utility?

    1.  l
    2.  r
    3.  n
    4.  b

    Answer: A

5.  What letter is used to create a partition inside the fdisk utility?

    1.  p
    2.  n
    3.  c
    4.  d

    Answer: B

6.  Which letter is used to write changes inside the fdisk utility?

    1.  q
    2.  c
    3.  d
    4.  w

    Answer D

7.  Which command is used to start the parted utility?

    1.  part -ad
    2.  parted
    3.  part -ed
    4.  part

    Answer: B

8.  Which option is used to display the partition table inside the parted utility?

    1.  display
    2.  parted
    3.  print
    4.  console

    Answer: C

9.  Which option is used to mount a partition from the cli?

    1.  mount /dev/sdb1
    2.  mnt /dev/sdb1
    3.  mt /dev/sdb1
    4.  mont /dev/sdb1

    Answer: A

10.  Which command displays the UUID of the known partitions on the cli?

    1.  blkid
    2.  df -h
    3.  du -h
    4.  mount

    Answer: A

11.  Which directory is the root directory?

    1.  /root/
    2.  /root
    3.  /home/root
    4.  /

    Answer: D

12.  Which command is used to change to another directory?

    1.  pwd
    2.  chage
    3.  cd
    4.  change dir

    Answer: C

13.  Which command can print the current working directory?

    1.  print dir
    2.  pwd
    3.  display
    4.  cd

    Answer: B

14.  Which command is used to print the content of a directory?

    1.  ls
    2.  which
    3.  whereis
    4.  cat

    Answer: A

15.  Which option can display files and directories permissions using the ls command?

    1.  -r
    2.  -b
    3.  -a
    4.  -l

    Answer: D

16.  Which option can display hidden files and directories with the ls command?

    1.  -l
    2.  -b
    3.  -a
    4.  -u

    Answer: C

17.  Which command removes a directory even though it is not empty?

    1.  rmdir
    2.  rm
    3.  remove
    4.  mv

    Answer: B

18.  Which options are used to find and remove empty files and directories with the find command?

    1.  -empty -remove
    2.  -empty -clean
    3.  -empty -delete
    4.  -empty -cycle

    Answer: C

19.  Which command is used to update the database which the locate command uses?

    1.  updatelocate
    2.  updatedatabase
    3.  locateupdate
    4.  updatedb

    Answer: D

20.  Which command displays a command’s output and simultaneously saves the results to a file?

    1.  less
    2.  more
    3.  wc
    4.  tee

    Answer: D

21.  In network testing, a Linux administrator seeks to verify the connectivity between two IP addresses: 10.0.2.15 and 192.168.1.40\. Which of the provided commands below will effectively accomplish this specific task?

    1.  route -e get to 192.168.1.40 from 10.0.2.15
    2.  ip route get 192.163.1.40 from 10.0.2.15
    3.  ip route 192.169.1.40 to 10.0.2.15
    4.  route -n 192.168.1.40 from 10.0.2.15

    Answer: B

22.  To enhance the security of one of the servers, the administrator aims to prevent remote administrative login via the SSH service. Which action should the administrator take from the following options?

    1.  To restrict remote administrative login via SSH, include the line DenyUsers root in the /etc/hosts.deny file.
    2.  For hardening the server’s security, configure PermitRootLogin to no in the /etc/ssh/sshd_config file.
    3.  To prevent remote administrative login, add the line account required pam_nologin.so to the /etc/pam.d/sshd file.
    4.  Disable PubKeyAuthentication by setting it to no in the /etc/ssh/ssh_config file.

    Answer: B

23.  A Linux administrator is examining a collection of log output files and needs to identify files that contain any instance of the word denied. The administrator wants to include log files with term occurrences in uppercase and lowercase letters. Which of the following commands should the administrator use to achieve this objective?

    1.  find . -type f -print | xrags grep -ln denied
    2.  find . -type f -print | xrags grep -nv denied
    3.  find . -type f -print | xrags grep -wl denied
    4.  find . -type f -print | xrags grep -li denied

    Answer: C

24.  An engineer is facing difficulties in terminating a process. Which commands should the administrator use to forcefully stop the process?

    1.  kill -1
    2.  kill -9
    3.  kill -15
    4.  kill -HUP

    Answer: B

25.  A Linux engineer is required to confirm the presence of the app.go file in the root directory of a built container. Which options can the administrator use to check if the root directory contains this file?

    1.  docker image inspect
    2.  docker container inspect
    3.  docker exec <container_name> ls
    4.  docker ps <container_name>

    Answer: B

26.  What command is used to set the default permissions for new files?

    1.  Setenforce
    2.  sudo
    3.  umask
    4.  chmod

    Answer: C

27.  A help-desk engineer rebooted a server. Users then reported some of their files were missing. After troubleshooting, the administrator found one of the filesystems was missing. The filesystem was not listed in /etc/fstab and might have been mounted manually by someone before reboot. Which of the following would prevent this issue from reoccurring in the future?

    1.  Sync the mount units.
    2.  Mount the filesystem manually.
    3.  Create a mount unit and enable it to be started at boot.
    4.  Remount all the missing filesystems.

    Answer: C

28.  An engineering administrator needs to test the route between the IP address 10.0.20.40 and the IP address 192.168.20.100\. Which of the following commands will accomplish this task?

    1.  route -e get to 192.168.1.40 from 10.0.2.15
    2.  ip route get 192.168.20.100 from 10.0.20.40
    3.  ip route 192.169.1.40 to 10.0.2.15
    4.  route -n 192.168.1.40 from 10.0.2.15

    Answer: B

29.  A Linux administrator has the task of verifying if the service systemd-resolved.service is running smoothly without any errors. Which of the following commands will display this relevant information?

    1.  To view information about the status of the systemd-resolved.service and check for any errors, use the command: systemctl status systemd-resolved.service
    2.  To enable the systemd-resolved.service and have it start at boot, use the command: systemctl enable systemd-resolved.service
    3.  To mask the systemd-resolved.service and prevent it from starting, use the command: systemctl mask systemd-resolved.service
    4.  To display detailed information about the systemd-resolved.service, use the command: systemctl show systemd-resolved.service

    Answer: A

30.  Which of the passwords listed below is considered secured?

    1.  password123
    2.  t%h@)_14!*!
    3.  12345678
    4.  abcdefgh

    Answer: B

31.  Which environment variable stores the current shell?

    1.  SHELL
    2.  BASH
    3.  SH
    4.  TCSH

    Answer: A

32.  Which mount point hold system configuration files?

    1.  /boot
    2.  /home
    3.  /etc
    4.  /var

    Answer: C

33.  Which command is used to update GRUB2 in Ubuntu?

    1.  update-grub2
    2.  make-grub
    3.  update-grub-gfxpayload
    4.  grub2-update

    Answer: A

34.  Which directory is the GRUB configuration files located in recent Ubuntu distributions?

    1.  /boot/grub2/
    2.  /var
    3.  /etct/grub2/grub/
    4.  /boot/grub/

    Answer: D

35.  Which characters can be used to test 2 conditions and return TRUE if both conditions are true?

    1.  &&
    2.  ||
    3.  //
    4.  ==

    Answer: A

36.  Which character is used in front an equal sign = to ensure a condition is not TRUE in an if clause?

    1.  +
    2.  !
    3.  >
    4.  <

    Answer: B

37.  Which bit must be turned on for a script to be able to run?

    1.  execute
    2.  read
    3.  write
    4.  read & write

    Answer: A

38.  After making changes to the ~/.bashrc file and adding new aliases for certain commands, a help-desk technician encountered issues with the aliases not working. What action should the technician take as the first step to address this problem?

    1.  source ~/.bashrc
    2.  read ~/.bashrc
    3.  touch ~/.bashrc
    4.  echo ~/.bashrc

    Answer: A

39.  Which value represents rwx permissions for a file?

    1.  5
    2.  4
    3.  7
    4.  1

    Answer: C

40.  Which value represents rw permissions for a file?

    1.  6
    2.  4
    3.  7
    4.  1

    Answer: A

41.  If it exists, which file is a symbolic link to the /boot/grub/grub.conf?

    1.  /boot/grub/grub2.cfg
    2.  /boot/grub2/grub.cfg
    3.  /boot/grub.d/menu.lst
    4.  /boot/grub/menu.lst

    Answer: D

42.  Which option with the timedatectl command can display all the available timezones?

    1.  --list-timezones
    2.  --list-time-zones
    3.  list-timezones
    4.  list-timezone

    Answer: C

43.  Which character must be placed in front the H when setting the hour using the date command?

    1.  #
    2.  @
    3.  $
    4.  %

    Answer: D

44.  Which list option is used to query a given package using the rpm command?

    1.  -a
    2.  -q
    3.  -e
    4.  r

    Answer: B

45.  Which command can be used to reconfigure a package in an Ubuntu system?

    1.  dpkg—update
    2.  dpkg -r
    3.  dpkg -e
    4.  dpkg-reconfigure

    Answer: D

46.  What is the command used to change ownership for a file?

    1.  chmod
    2.  chown
    3.  chwn
    4.  chmd

    Answer: B

47.  Which directory would be used for adding a custom boot entry for GRUB2?

    1.  /etc/default/grub
    2.  /etc/grub.d/
    3.  /etc/grub/default/custom
    4.  /etc/default/grub-custom

    Answer: B

48.  Which of the following command can be used to execute a job 5minutes from the present?

    1.  at now + 5 minutes
    2.  at 5 minutes
    3.  at tomorrow 5 minutes
    4.  at next 5minutes

    Answer: A

49.  Which option with the at command can be used to print the job queue?

    1.  -q
    2.  -a
    3.  -l
    4.  -e

    Answer: B

50.  What is the name of the cron service in recent Fedora distributions?

    1.  crond.service
    2.  cron.service
    3.  cron-daemon.service
    4.  crond.daemon.service

    Answer: A

51.  Which directory can we place a script if we would like to script to be executed every hour?

    1.  /etc/crond.hourly
    2.  /etc/cron.hourly/
    3.  /etc/crond/hourly/jobs
    4.  /etc/cron/hourly/

    Answer: B

52.  Which command should be used when editing the /etc/sudoers file?

    1.  visudo
    2.  visualdo
    3.  nano
    4.  vim.tiny

    Answer: A

53.  Which of the following timer values would enable a command to execute every 5 minutes?

    1.  0/5 * * * *
    2.  * 5 * * *
    3.  * * 5 * *
    4.  * * * 5 *

    Answer: A

54.  Which option can view the crontab file for the current user?

    1.  -a
    2.  -b
    3.  -d
    4.  -l

    Answer: D

55.  Which timer values would enable a command to execute at 5:00 AM daily?

    1.  0/5 * * * *
    2.  * 5 * * *
    3.  * * 5 * *
    4.  * * * 5 *

    Answer: B

56.  Which of the following statements is correct about the /proc/?

    1.  Changes to files in /proc/ are not implemented in any way
    2.  The files in the /proc/ are meant to be used as comments
    3.  Any change done in the /proc/ is implemented in real-time
    4.  Files within the /proc/ cannot be edited

    Answer: C

57.  Which character must be placed before a variable to use it?

    1.  #
    2.  $
    3.  !
    4.  &

    Answer: B

58.  Which choice allows you to synchronize the system time with the hardware clock?

    1.  –hctosys
    2.  --systohc
    3.  –systohc
    4.  –hctohc

    Answer: A

59.  Which number can be used to restart a system using the init command?

    1.  1
    2.  0
    3.  6
    4.  2

    Answer: C

60.  Which option can be used to reboot a system using the shutdown command?

    1.  -a
    2.  -s
    3.  -c
    4.  -r

    Answer: D

61.  Which number can be used to enter rescue mode using the init command?

    1.  6
    2.  1
    3.  7
    4.  2

    Answer: B

62.  Which shell scripting keyword enables the user to test for other condition(s) if the condition(s) in the if clause were not met?

    1.  elif
    2.  elseif
    3.  else
    4.  fi

    Answer: A

63.  Which command can be used to display messages generated during boot-up?

    1.  echo
    2.  anacron
    3.  message
    4.  dmesg

    Answer: D

64.  What is a common setting that is found in the BIOS?

    1.  Boot options
    2.  Kernel options
    3.  initram options
    4.  GRUB2 options

    Answer: A

65.  Which command can display shared library information for a given command?

    1.  ldconfig
    2.  ld
    3.  ldd
    4.  libconfig

    Answer: C

66.  Which of the following defines the /bin/sh at the beginning of a shell script?

    1.  @!/bin/sh
    2.  #!/bin/sh
    3.  #%/bin/sh
    4.  @#/bin/sh

    Answer: B

67.  Which of the following is used to compare whether one condition is equivalent to another?

    1.  ==
    2.  !=
    3.  =
    4.  =!

    Answer: A

68.  Which keyword is used to end an if statement?

    1.  if
    2.  endif
    3.  fi
    4.  elif

    Answer: C

69.  Which option is used to remove a package using the rpm command?

    1.  -e
    2.  -a
    3.  -r
    4.  -d

    Answer: A

70.  Which option is used to remove a package and its configuration files using the dpkg command?

    1.  -R
    2.  -r
    3.  -p
    4.  -P

    Answer: D

71.  Which command can be used to search for a package in a Debian distribution?

    1.  apt-cache
    2.  apt-get
    3.  dpkg
    4.  rpm

    Answer: A

72.  As a junior administrator, how can you set the sticky bit on a directory named my_scripts with file permissions set to 755?

    1.  chown -s 755 my_scripts
    2.  chown 1755 my_scripts
    3.  chmod -s 755 my_scripts
    4.  chmod 1755 my_scripts

    Answer: D

73.  Which option can be used to display statistics about a package using the apt-cache

    1.  command?
    2.  statistics
    3.  stats
    4.  stat

    Answer: B

74.  Which character can be used to start a program in the background?

    1.  #
    2.  !
    3.  %
    4.  &

    Answer: D

75.  What are the two most helpful commands for troubleshooting a storage capacity issue on a server with no specific mount point or directory reported to the help-desk technician?

    1.  lvdisplay
    2.  df
    3.  mount
    4.  du

    Answer: B and D

76.  Which of the following port does FTP use for command traffic?

    1.  TCP 21
    2.  UDP 21
    3.  ICMP 21
    4.  HSRP 21

    Answer: A

77.  Which of the following represents a /23 in binary?

    1.  11111111.11111000.11111111.00000000
    2.  11111110.00000000.00000001.00000000
    3.  11111111.11111110.00000000.00000001
    4.  11111111.11111111.11111110.00000000

    Answer: D

78.  Which of the following represents a Classful C subnet mask?

    1.  255.255.255.0
    2.  255.255.0.0
    3.  255.254.255.0
    4.  255.253.255.0

    Answer: A

79.  Which option views hidden files and directories using the ls command?

    1.  -l
    2.  -s
    3.  -a
    4.  -r

    Answer: C

80.  Which character is used to switch to the current user’s home directory?

    1.  ~
    2.  `
    3.  '
    4.  !

    Answer: A

81.  Which option can be used to search for permissions using the find command?

    1.  –permissions
    2.  -perm
    3.  –perms
    4.  --view-permissions

    Answer: B

82.  Which command can be used to update the mlocate database?

    1.  update-locate
    2.  update-database
    3.  updated
    4.  updated

    Answer: C

83.  Which option can be used to ignore case when searching with the locate command?

    1.  –ignore
    2.  -i
    3.  --no-case
    4.  -c

    Answer B

84.  Which option displays the total number of words using the wc command?

    1.  -c
    2.  -a
    3.  -w
    4.  -l

    Answer: C

85.  Which characters can be used when appending data to a file?

    1.  >
    2.  <
    3.  <<
    4.  >>

    Answer: D

86.  Which command can be used to display the output and simultaneously send the output to a file?

    1.  tee
    2.  cat
    3.  echo
    4.  pause

    Answer: A

[Mock exam 2](#contents.xhtml_sc211a)

1.  After initiating the top command inside a terminal window, a help-desk technician pressed Ctrl+Z, resulting in the presentation of the shell prompt. Which of the following commands should the administrator use to return to the program?

    1.  fg
    2.  su
    3.  bg
    4.  ed

    Answer: A

2.  As a Linux administrator frequently connecting to a remote host via SSH with a non-standard port, you wish to avoid passing the port parameter on the command line every time. Which files can be used to set a different port value specifically for that host?

    1.  To set a different port value specifically for the remote host, use the file: /etc/ssh/sshd_config.
    2.  To achieve the desired effect, you should modify the file: /etc/ssh/moduli
    3.  Customize the port value for the remote host by utilizing the file: ~/.ssh/config
    4.  To handle authorized keys for authentication, access the file: ~/.ssh/authorized_keys

    Answer: C

3.  The help-desk technician intends to verify the link status of a network interface named eth0 in a Linux server. Which of the following commands can assist in achieving this objective?

    1.  ifconfig hw eth0
    2.  netstat -r eth0
    3.  ss -ti eth0
    4.  ip link show eth0

    Answer: D

4.  The help-desk technician has a ticket to create a new user named pinshanally. However, the user needs to pinshanally to have a different home directory located under /Linux_plus/certification. Which of the following commands will fulfill this task?

    1.  useradd -d /Linux_plus/certification pinshanally
    2.  useradd -m /Linux_plus/certification pinshanally
    3.  useradd -b /Linux_plus/certification pinshanally
    4.  useradd -s /Linux_plus/certification pinshanally

    Answer: A

5.  Which command adds a tag named my_tag when creating a new Docker image called my_image?

    1.  docker image save my_image:my_tag
    2.  docker image build -t my_image:my_tag
    3.  docker image tag my_image:my_tag
    4.  docker image version my_image:my_tag

    Answer: C

6.  Which of the following languages should an Ansible playbook be written?

    1.  SQL
    2.  YAML
    3.  HTML
    4.  JSON

    Answer: B

7.  Which of the following is a valid JSON string?

    1.  ["Ford", "BMW", "Toyota]
    2.  ["Ford", "BMW", 'Toyota"]
    3.  ["Ford", "BMW", "Toyota"]
    4.  ["Ford", BMW', "Toyota"]

    Answer: C

8.  Which of the following is a valid object in JSON?

    1.  var my_object= ["age": 39 , Location: "Guyana", "City":" Georgetown"]
    2.  var my_object = ["age": 39 , "Location": "Guyana", "City": "Georgetown"]
    3.  var my_object = ["age": 39 , "Location: Guyana", "City": " Georgetown"]
    4.  var my_object = ["age": 39 , "Location": "Guyana", City": Georgetown"]

    Answer: B

9.  To run a command in the background of a terminal, which of the following commands would be the most appropriate choice for the help-desk technician?

    1.  /run_application &
    2.  /run_application +$
    3.  /run_application
    4.  /run_application $

    Answer: A

10.  If the command echo $ outputs 1, which of the following statements is true?

    1.  The displayed value is the process ID of the echo command.
    2.  The displayed value is the process ID of the current shell.
    3.  The displayed value is the exit value of the command executed immediately before echo.
    4.  The displayed value is the exit value of the echo command.

    Answer: C

11.  Which command makes the shell variable named VARIABLE visible to subshells?

    1.  export $VARIABLE
    2.  export VARIABLE
    3.  set $VARIABLE
    4.  set VARIABLE

    Answer: B

12.  What will be the output of the command seq 10?

    1.  A continuous stream of numbers increasing in increments of 10 until stopped
    2.  The numbers 1 through 10 with one number per line
    3.  The numbers 0 through 9 with one number per line
    4.  The number 10 to standard output

    Answer: B

13.  Which command among the following stores the output of the date command into the shell variable mydate?

    1.  Save the output of the date command into the shell variable mydate using: mydate="$(date)"
    2.  Assign the string exec date to the shell variable mydate
    3.  Store the result of the arithmetic expression date into the shell variable mydate
    4.  Set the value of the shell variable mydate to the string date

    Answer: A

14.  A Linux administrator plans to set up a cron job that will copy hundreds of files from a remote directory on a scheduled basis. The file contents should retain their original permissions, including group ownership, and the cron job should run for the least amount possible. Which of the following is the best program to use in this situation?

    1.  curl
    2.  scp
    3.  rsync
    4.  rpm

    Answer: C

15.  Which command from the options below sets the permissions of /bin/my_file to be executable by everyone but writable only by its owner?

    1.  chmod 557 /bin/my_file
    2.  chmod o+rw /bin/my_file
    3.  chown 557 /bin/my_file
    4.  chmod 755/bin/my_file

    Answer: D

16.  Which command can you use to update Id.so.cache after installing new shared libraries?

    1.  ld_config
    2.  Idconfig
    3.  libpath
    4.  newlibs

    Answer: B

17.  To enable running a shell script like a regular command from anywhere in the filesystem, you need to meet the following requirements (Choose three correct answers.):

    1.  The user executing the command should belong to the script group
    2.  The script file must be located within the $PATH environment variable
    3.  The script file must have the executable permission (chmod +x) set
    4.  The script should begin with a shebang-line (#!) specifying the correct interpreter

    Answer: B, C, and D

18.  Which shell built-in command can create a shortcut or pseudonym for a longer command?

    1.  shortcut
    2.  alias
    3.  sudo
    4.  link

    Answer: B

19.  Which of the following list all the running containers using the lxc command?

    1.  lxc storage list
    2.  lxc containers list
    3.  lxc list
    4.  lxc image list

    Answer: C

20.  Which configuration file would be edited to change the default options for outbound SSH sessions?

    1.  /etc/ssh/sshd_config
    2.  /etc/ssh/ssh
    3.  /etc/ssh/client
    4.  /etc/ssh/ssh_config

    Answer: D

21.  Which of the following is used to view the network adapters using the lxc command?

    1.  lxc network display
    2.  lxc network -a
    3.  lxc network -display
    4.  lxc network list

    Answer: D

22.  Which option is used to skip mounted file systems when using the fsck command?

    1.  -m
    2.  -mount /dev/sda1
    3.  -A
    4.  -M

    Answer: D

23.  Which of the following programs uses the /etc/hosts.deny file to check for access restrictions to system services?

    1.  tcpd
    2.  inetd
    3.  fingerd
    4.  mountd

    Answer: A

24.  Which of the following commands lists the process(s) actively using a file system?

    1.  debug
    2.  lsof
    3.  ifconfig
    4.  traceroute

    Answer: B

25.  Which of the following command is used to copy ssh keys from one machine to another?

    1.  ssh_keygen
    2.  ssh_copy
    3.  ssh-copy-id
    4.  ssh_generate_keys

    Answer: C

26.  Which of the following is used to list the contents of a my_file.tar archive file?

    1.  tar -cvf my_file.tar
    2.  tar -tvf my_file.tar
    3.  tar -avf my_file.tar
    4.  tar -bvf my_file.tar

    Answer: B

27.  In what way do shadow passwords enhance password security compared to the traditional way of storing passwords?

    1.  Password hashes of shadow passwords are stored in plain text, allowing for checking weak passwords
    2.  Each shadow password remains valid for 45 days and must be changed after that period.
    3.  The system’s host key is utilized to strongly encrypt all shadow passwords.
    4.  Shadow passwords move encrypted password hashes from the world-readable /etc/passwd to the /etc/shadow, which only readable by the root user.

    Answer: D

28.  Which commands would enable the security administrator to list and inspect the SELinux context of files?

    1.  ls –D
    2.  ls –a
    3.  ls –Z
    4.  ls -1

    Answer: C

29.  Which option can display the routing table with the netstat command?

    1.  -s
    2.  -a
    3.  -r
    4.  -d

    Answer: C

30.  Which address family is the IP information located using either ifconfig or ip a command?

    1.  inet
    2.  inet6
    3.  int
    4.  int6

    Answer: A

31.  Which of the following is the correct method to shutdown an interface?

    1.  ifconfig down ens33
    2.  ifconfig ens33 down
    3.  ifconfig ens33 shutdown
    4.  ifconfig shutdown ens33

    Answer: B

32.  Which file does the ifup command checks whenever the command is issued?

    1.  /etc/network/sysconfig
    2.  /etc/networking/interfaces
    3.  /etc/network/interfaces
    4.  /etc/sysconfig/network/interfaces

    Answer: C

33.  Which is the correct way to remove an IP using the ip command?

    1.  ip a del 10.10.10.1/24 dev ens33
    2.  ip a 10.10.10.1/24 del dev ens33
    3.  ip a 10.10.10.1/24 dev ens33 del
    4.  ip del a 10.10.10.1/24 dev ens33

    Answer: A

34.  What does the * represents in the output of the fdisk -l command?

    1.  The device’s partition is marked as unbootable
    2.  The device’s partition is marked as bootable
    3.  The device’s partition is marked as read-only
    4.  The device’s partition is inaccessible

    Answer: B

35.  Which option is used to change the partition type using the fdisk utility?

    1.  l
    2.  n
    3.  t
    4.  d

    Answer: C

36.  Which number type represents an NTFS partition using the fdisk utility?

    1.  7
    2.  8
    3.  6
    4.  5

    Answer: A

37.  Which option is used to change partition size using the parted utility?

    1.  changesizepart
    2.  sizechangepart
    3.  resizepart
    4.  sizeresizepart

    Answer: C

38.  Which option can be used to display information such as the UUIDs of drives using the lsblk command?

    1.  -a
    2.  -f
    3.  -l
    4.  -i

    Answer: B

39.  Which option is used to display information in a human readable format using the df command?

    1.  -a
    2.  -c
    3.  -r
    4.  -h

    Answer: D

40.  Which of the following is the correct for defining a variable?

    1.  a=1
    2.  a=Loop Free
    3.  a= 1 2 3
    4.  a=#1

    Answer: A

41.  Which option allows the user to define the user, uid,gid with the mount command?

    1.  -v
    2.  -t
    3.  -u
    4.  -o

    Answer: D

42.  Which command can be used to switch the display manager in Fedora distributions?

    1.  system-displaymanager
    2.  system-switch-displaymanager
    3.  switch-displaymanager
    4.  system-switch-display

    Answer B

43.  Which option with the usermod command is used to lock a user account?

    1.  -l
    2.  –lock
    3.  L
    4.  -lock

    Answer: C

44.  Which file holds the commands execute for a given user?

    1.  ~/.bash_history
    2.  /etc/.bash_history
    3.  /var/bash/.bash_history
    4.  /bash_history

    Answer: A

45.  Which option is used with the useradd command to display the defaults for a new user?

    1.  -d
    2.  -c
    3.  -D
    4.  -s

    Answer: C

46.  Which option with the passwd command is used for locking a user account?

    1.  -L
    2.  -l
    3.  -a
    4.  -A

    Answer: B

47.  Which option defines a shell for a new user with the useradd command?

    1.  -s
    2.  -S
    3.  -shell
    4.  -Shell

    Answer: A

48.  Which option defines an expiration date for a user with the chage command?

    1.  -e
    2.  -l
    3.  -a
    4.  -E

    Answer: D

49.  Which option displays information regarding an account’s current state using the passwd command?

    1.  -a
    2.  –status
    3.  -s
    4.  --list-status

    Answer: B

50.  Which letter indicates an account’s current state is unlocked with the passwd command?

    1.  U
    2.  L
    3.  P
    4.  A

    Answer: C

51.  Which option displays the date the system booted up with the who command?

    1.  -b
    2.  -c
    3.  -r
    4.  -e

    Answer: A

52.  Which command displays users who have recently logged in?

    1.  which
    2.  whois
    3.  last
    4.  recent

    Answer: C

53.  Which command is used to create a group?

    1.  add-group
    2.  groupadd
    3.  add -G
    4.  group -G

    Answer: B

54.  Which option defines a user to use a group as its primary group?

    1.  -G
    2.  –group
    3.  --group-new
    4.  -g

    Answer: D

55.  Which option is used to display only TCP connection using the netstat command?

    1.  -t
    2.  -u
    3.  -r
    4.  -c

    Answer: A

56.  Which port does HTTPS uses?

    1.  80
    2.  21
    3.  443
    4.  69

    Answer: C

57.  Which command handles the system log files in recent Fedora distributions?

    1.  log
    2.  journalctl
    3.  log.service
    4.  logging.service

    Answer: B

58.  Which classful range does the IP 192.168.20.1 belong?

    1.  Class B
    2.  Class C
    3.  Class D
    4.  Class A

    Answer: B

59.  Which port does TFTP uses?

    1.  21
    2.  53
    3.  69
    4.  443

    Answer: C

60.  Which option prints the program ID and program name with the netstat command?

    1.  -r
    2.  -a
    3.  -l
    4.  -p

    Answer: D

61.  Which option is used to list only the targets with the systemctl command?

    1.  -t
    2.  -r
    3.  -type
    4.  -M

    Answer: A

62.  Which command can be used to generate a test log message?

    1.  log-test
    2.  test-log
    3.  logger
    4.  log

    Answer: C

63.  Which port does DNS uses?

    1.  139
    2.  110
    3.  143
    4.  53

    Answer: D

64.  Which option changes rsyslog to use TCP for reception?

    1.  module(load="tcp")
    2.  module(load="imtcp")
    3.  module("imtcp"=load)
    4.  module("tcp"=load)

    Answer: B

65.  Which of the following files is the configuration file for rsyslog?

    1.  /etc/rsyslog.d/rsyslog.conf
    2.  /etc/rsyslog/rsyslog.conf
    3.  /etc/rsyslog.conf
    4.  /etc/rsyslog.d/rsyslog.service

    Answer: C

66.  Which of the following specifies only the informational messages should be sent to the rsyslog server?

    1.  *.info
    2.  info.*
    3.  *.message-type=informational
    4.  message*.type=information

    Answer: A

67.  Which configuration file should mount points be placed so they are auto mounted upon system boot?

    1.  /etc/mounts.conf
    2.  /etc/auto.mount.cfg
    3.  /etc/fstab
    4.  /etc/mn.conf

    Answer: C

68.  What shell scripting keyword defines the end of a while loop?

    1.  loop end
    2.  fi
    3.  else
    4.  done

    Answer: A

69.  Which command updates the grub configuration file in an Ubuntu distribution?

    1.  grub-update2
    2.  update-grub2
    3.  update-grub
    4.  grub-update

    Answer: C

70.  Which of the following represents the link-local IPv6 range?

    1.  fe80::/10
    2.  fd80::/7
    3.  fc00::/7
    4.  ff00::/10

    Answer: A

71.  Which character is used when no password has been set for a group in the /etc/gshadow?

    1.  #
    2.  %
    3.  !
    4.  &

    Answer: C

72.  Which command is used to change a group ID of a given group?

    1.  groupmod
    2.  groupadd
    3.  gidmod
    4.  usermod

    Answer: A

73.  Which of the following is used to kill the sudo authentication timer immediately?

    1.  -l
    2.  -k
    3.  -a
    4.  -r

    Answer: B

74.  Which of the following must be placed in front of a group inside the /etc/sudoers?

    1.  #
    2.  @
    3.  %
    4.  &

    Answer: C

75.  Which option displays only a particular interface with the ip command?

    1.  s
    2.  d
    3.  v
    4.  i

    Answer: A

76.  Which option is used to define a type using the ip link command?

    1.  –type
    2.  type
    3.  --link-type
    4.  --type-id

    Answer: B

77.  Which of the following IP address falls under 10.20.16.0/21?

    1.  10.20.16.256
    2.  10.20.15.255
    3.  10.20.16.2
    4.  10.20.16.258

    Answer: C

78.  Which of the following represents a subnet mask of /28 in dotted decimal format?

    1.  255.255.255.240
    2.  255.255.252.240
    3.  255.255.254.240
    4.  255.255.253.240

    Answer: A

79.  Which is correct for displaying statistics and other information like CRC counters using the ip command?

    1.  ip a -s link ls ens33
    2.  ip a -a link ls ens33
    3.  ip a -s -s link ens33
    4.  ip a -a -s link ls ens33

    Answer: C

80.  Which option displays the files owned by a package using the dpkg command?

    1.  -a
    2.  -s
    3.  -l
    4.  -L

    Answer: D

81.  If it exists, which file is a symbolic link to the /boot/grub/grub.conf?

    1.  /boot/grub/grub2.cfg
    2.  /boot/grub2/grub.cfg
    3.  /boot/grub.d/menu.lst
    4.  /boot/grub/menu.lst

    Answer: D

82.  Which directory would be used for adding a custom boot entry for GRUB2?

    1.  /etc/default/grub
    2.  /etc/grub.d/
    3.  /etc/grub/default/custom
    4.  /etc/default/grub-custom

    Answer: B

[Conclusion](#contents.xhtml_sc212a)

In this chapter, we wrapped this book with two mock exams with questions surrounding the various chapters covered throughout this book.

Join our book’s Discord space

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# Index

Symbols

/home directory [11](#ch01.xhtml_page11)

/lib directory [10](#ch01.xhtml_page10)

/var directory [8](#ch01.xhtml_page8), [9](#ch01.xhtml_page9)

A

advanced compression techniques [30](#ch02.xhtml_page30)

Advanced Package Tool (APT) [171](#ch04.xhtml_page171)

Ansible

about [318](#ch08.xhtml_page318)

ad-hoc commands [319](#ch08.xhtml_page319)

configuring [320](#ch08.xhtml_page320), [321](#ch08.xhtml_page321)

example, in network environment [321](#ch08.xhtml_page321)-[323](#ch08.xhtml_page323)

galaxy [320](#ch08.xhtml_page320)

installing [320](#ch08.xhtml_page320), [321](#ch08.xhtml_page321)

inventory [318](#ch08.xhtml_page318)

modules [319](#ch08.xhtml_page319)

playbooks [319](#ch08.xhtml_page319)

roles [319](#ch08.xhtml_page319)

tasks and plays [319](#ch08.xhtml_page319)

anycast address [127](#ch03.xhtml_page127)

apt-get command [171](#ch04.xhtml_page171)-[185](#ch04.xhtml_page185)

aptitude command [185](#ch04.xhtml_page185)-[190](#ch04.xhtml_page190)

architecture [318](#ch08.xhtml_page318)

Automatic Private IP Addressing (APIPA) [115](#ch03.xhtml_page115)

B

Basic Input/Output System (BIOS) [20](#ch01.xhtml_page20)

Binary JSON (BSON) format [315](#ch08.xhtml_page315)

boot issues troubleshooting [339](#ch09.xhtml_page339)-[341](#ch09.xhtml_page341)

B-tree file system (Btrfs) [57](#ch02.xhtml_page57)

C

Centos system

directories [5](#ch01.xhtml_page5)-[7](#ch01.xhtml_page7)

chage command [250](#ch05.xhtml_page250)-[253](#ch05.xhtml_page253)

child process [88](#ch03.xhtml_page88)

class A [115](#ch03.xhtml_page115)

Classless Inter Domain Routing (CIDR) [118](#ch03.xhtml_page118)

client-side DNS [152](#ch03.xhtml_page152), [153](#ch03.xhtml_page153)

Command-Line Interface (CLI) [265](#ch06.xhtml_page265)

compressing directories

about [29](#ch02.xhtml_page29)

examples [29](#ch02.xhtml_page29), [30](#ch02.xhtml_page30)

compressing files

about [29](#ch02.xhtml_page29)

examples [29](#ch02.xhtml_page29)

compression algorithms

about [28](#ch02.xhtml_page28)

characteristics [28](#ch02.xhtml_page28), [29](#ch02.xhtml_page29)

compression libraries [31](#ch02.xhtml_page31)

containers [304](#ch07.xhtml_page304)

D

Debian package management [161](#ch04.xhtml_page161)

decompressing files and directories

about [30](#ch02.xhtml_page30)

examples [30](#ch02.xhtml_page30)

Deep Packet Inspection (DPI) [257](#ch06.xhtml_page257)

Desktop Management Interface (DMI) [13](#ch01.xhtml_page13)

Destination NAT (DNAT) [257](#ch06.xhtml_page257)

dig command [332](#ch09.xhtml_page332), [333](#ch09.xhtml_page333)

Discretionary Access Control (DAC) [275](#ch06.xhtml_page275)

dnf utility [204](#ch04.xhtml_page204)-[212](#ch04.xhtml_page212)

Docker

about [306](#ch07.xhtml_page306)

key concepts [306](#ch07.xhtml_page306)

usage example [307](#ch07.xhtml_page307)

Docker components [307](#ch07.xhtml_page307)

Docker containers [306](#ch07.xhtml_page306), [307](#ch07.xhtml_page307)

Docker engine [306](#ch07.xhtml_page306)

Docker images [306](#ch07.xhtml_page306)

Docker registry [306](#ch07.xhtml_page306)

dpkg command [161](#ch04.xhtml_page161)-[171](#ch04.xhtml_page171)

F

fdisk utility

using [57](#ch02.xhtml_page57)-[66](#ch02.xhtml_page66)

file and directories

finding [44](#ch02.xhtml_page44)-[50](#ch02.xhtml_page50)

file and directory operations

about [31](#ch02.xhtml_page31)-[35](#ch02.xhtml_page35)

directories, creating [39](#ch02.xhtml_page39)-[42](#ch02.xhtml_page42)

directories, removing [42](#ch02.xhtml_page42), [43](#ch02.xhtml_page43)

file and directories, finding [44](#ch02.xhtml_page44)-[50](#ch02.xhtml_page50)

files, copying [37](#ch02.xhtml_page37)

files, creating [35](#ch02.xhtml_page35), [36](#ch02.xhtml_page36)

files, moving [38](#ch02.xhtml_page38)

files, removing [39](#ch02.xhtml_page39)

files, renaming [38](#ch02.xhtml_page38)

file compression

about [28](#ch02.xhtml_page28)

advanced compression techniques [30](#ch02.xhtml_page30)

compressing directories [29](#ch02.xhtml_page29)

compressing files [29](#ch02.xhtml_page29)

compression algorithms [28](#ch02.xhtml_page28)

decompressing files and directories [30](#ch02.xhtml_page30)

filesystem hierarchy standard (FHS)

about [1](#ch01.xhtml_page1), [2](#ch01.xhtml_page2), [27](#ch02.xhtml_page27)

key principles [2](#ch01.xhtml_page2)

filesystem management

about [56](#ch02.xhtml_page56)

B-tree file system (Btrfs) [57](#ch02.xhtml_page57)

fdisk utility, using [57](#ch02.xhtml_page57)-[66](#ch02.xhtml_page66)

Fourth Extended File System (ext4) [56](#ch02.xhtml_page56)

New Technology File System (NTFS) [57](#ch02.xhtml_page57)

XFS file system [57](#ch02.xhtml_page57)

ZFS file system [57](#ch02.xhtml_page57)

firewall

about [256](#ch06.xhtml_page256)

firewalld [260](#ch06.xhtml_page260)

TCP wrappers [258](#ch06.xhtml_page258)-[260](#ch06.xhtml_page260)

firewall, aspects

application-level filtering [257](#ch06.xhtml_page257)

firewall zones and interfaces [257](#ch06.xhtml_page257)

logging and auditing [257](#ch06.xhtml_page257)

Network Address Translation (NAT) [257](#ch06.xhtml_page257)

packet filtering [256](#ch06.xhtml_page256)

rule chains [256](#ch06.xhtml_page256)

rules [256](#ch06.xhtml_page256)

security mechanisms [257](#ch06.xhtml_page257)

stateful inspection [256](#ch06.xhtml_page256)

firewalld

about [260](#ch06.xhtml_page260)

components [261](#ch06.xhtml_page261)

features [260](#ch06.xhtml_page260)

usage examples [261](#ch06.xhtml_page261)

Fourth Extended File System (ext4) [56](#ch02.xhtml_page56)

G

GNU gettext [158](#ch04.xhtml_page158)

Grand Unified Bootloader 2 (GRUB2)

about [19](#ch01.xhtml_page19)-[22](#ch01.xhtml_page22)

working with [23](#ch01.xhtml_page23)-[26](#ch01.xhtml_page26)

group management [242](#ch05.xhtml_page242)-[245](#ch05.xhtml_page245)

H

hard disk

formatting [72](#ch02.xhtml_page72)-[75](#ch02.xhtml_page75)

hard disk troubleshooting [337](#ch09.xhtml_page337)-[339](#ch09.xhtml_page339)

hardware information

commands [12](#ch01.xhtml_page12), [13](#ch01.xhtml_page13)

finding [12](#ch01.xhtml_page12)-[19](#ch01.xhtml_page19)

hostname command [334](#ch09.xhtml_page334), [335](#ch09.xhtml_page335)

I

ifconfig command [131](#ch03.xhtml_page131)-[136](#ch03.xhtml_page136)

ifdown command [138](#ch03.xhtml_page138)

ifup command [137](#ch03.xhtml_page137), [138](#ch03.xhtml_page138)

Internet Engineering Task Force (IETF) [127](#ch03.xhtml_page127)

interprocess communication (IPC) [88](#ch03.xhtml_page88)

Intrusion Detection Systems (IDS) [257](#ch06.xhtml_page257)

Intrusion Prevention Systems (IPS) [257](#ch06.xhtml_page257)

ip command [139](#ch03.xhtml_page139)-[146](#ch03.xhtml_page146)

iptables

about [262](#ch06.xhtml_page262)

components [262](#ch06.xhtml_page262)

examples [263](#ch06.xhtml_page263), [264](#ch06.xhtml_page264)

rule syntax [262](#ch06.xhtml_page262)

IPv4 configuration

about [129](#ch03.xhtml_page129)-[131](#ch03.xhtml_page131)

ifconfig command [131](#ch03.xhtml_page131)-[136](#ch03.xhtml_page136)

ifdown command [138](#ch03.xhtml_page138)

ifup command [137](#ch03.xhtml_page137), [138](#ch03.xhtml_page138)

ip command [139](#ch03.xhtml_page139)-[146](#ch03.xhtml_page146)

IPv4 routing

configuring [146](#ch03.xhtml_page146)-[148](#ch03.xhtml_page148)

IPv6 addressing

about [127](#ch03.xhtml_page127)-[129](#ch03.xhtml_page129)

anycast address [127](#ch03.xhtml_page127)

consecutive zeros, removing [128](#ch03.xhtml_page128)

multicast address [127](#ch03.xhtml_page127)

unicast address [127](#ch03.xhtml_page127)

IPv6 configuration [149](#ch03.xhtml_page149), [150](#ch03.xhtml_page150)

IPv6 routing

client-side DNS [152](#ch03.xhtml_page152), [153](#ch03.xhtml_page153)

configuring [151](#ch03.xhtml_page151), [152](#ch03.xhtml_page152)

IP version 4 (IPv4) [113](#ch03.xhtml_page113)-[115](#ch03.xhtml_page115)

J

JavaScript Object Notation (JSON)

about [314](#ch08.xhtml_page314)

API communication [317](#ch08.xhtml_page317)

APIs [315](#ch08.xhtml_page315)

arrays [316](#ch08.xhtml_page316)

configuration files [317](#ch08.xhtml_page317)

data processing and manipulation [318](#ch08.xhtml_page318)

data storage and exchange [315](#ch08.xhtml_page315)

data types [316](#ch08.xhtml_page316)

schema [315](#ch08.xhtml_page315)

syntax [315](#ch08.xhtml_page315)

K

kill command [95](#ch03.xhtml_page95), [96](#ch03.xhtml_page96)

L

language environment variables [159](#ch04.xhtml_page159)

last command [238](#ch05.xhtml_page238), [239](#ch05.xhtml_page239)

Linux Containers (LXC)

about [304](#ch07.xhtml_page304)

components [305](#ch07.xhtml_page305)

kernel features [305](#ch07.xhtml_page305)

key concepts [304](#ch07.xhtml_page304)

templates [305](#ch07.xhtml_page305)

usage [305](#ch07.xhtml_page305), [306](#ch07.xhtml_page306)

Linux distros

directories [2](#ch01.xhtml_page2), [3](#ch01.xhtml_page3)

Linux localization

about [158](#ch04.xhtml_page158)

tools [158](#ch04.xhtml_page158)

Linux module [156](#ch04.xhtml_page156)

Linux processes

about [88](#ch03.xhtml_page88)

key points [88](#ch03.xhtml_page88)

kill command [95](#ch03.xhtml_page95), [96](#ch03.xhtml_page96)

pgrep command [98](#ch03.xhtml_page98)

pkill command [98](#ch03.xhtml_page98)-[105](#ch03.xhtml_page105)

ps command [89](#ch03.xhtml_page89)-[95](#ch03.xhtml_page95)

pstree command [96](#ch03.xhtml_page96), [97](#ch03.xhtml_page97)

Loadable Kernel Modules (LKM) [156](#ch04.xhtml_page156)

Local Area Network (LAN) [114](#ch03.xhtml_page114)

localization

about [157](#ch04.xhtml_page157)

importance [158](#ch04.xhtml_page158)

Linux localization [158](#ch04.xhtml_page158)

localization configuration process

example [159](#ch04.xhtml_page159)

localization directories [158](#ch04.xhtml_page158)

localization files [158](#ch04.xhtml_page158)

Logical Volume Management (LVM)

about [27](#ch02.xhtml_page27), [83](#ch02.xhtml_page83)-[85](#ch02.xhtml_page85)

key components [83](#ch02.xhtml_page83), [84](#ch02.xhtml_page84)

loopback address space [115](#ch03.xhtml_page115)

M

Mandatory Access Control (MAC) [275](#ch06.xhtml_page275)

memory troubleshooting [335](#ch09.xhtml_page335), [337](#ch09.xhtml_page337)

module

about [156](#ch04.xhtml_page156)

Linux module [156](#ch04.xhtml_page156)

management [156](#ch04.xhtml_page156), [157](#ch04.xhtml_page157)

types [156](#ch04.xhtml_page156)

mount command [76](#ch02.xhtml_page76)-[80](#ch02.xhtml_page80)

multicast address [127](#ch03.xhtml_page127)

multiline scalars

about [311](#ch08.xhtml_page311)

anchors and aliases [311](#ch08.xhtml_page311)

directives [312](#ch08.xhtml_page312)

YAML use case scenario [312](#ch08.xhtml_page312)-[314](#ch08.xhtml_page314)

N

netstat command [328](#ch09.xhtml_page328), [329](#ch09.xhtml_page329)

Network Address Translation (NAT) [262](#ch06.xhtml_page262)

network configuration

about [113](#ch03.xhtml_page113)

class A addresses [115](#ch03.xhtml_page115), [116](#ch03.xhtml_page116)

class B addresses [116](#ch03.xhtml_page116)

class C addresses [117](#ch03.xhtml_page117)

class D addresses [117](#ch03.xhtml_page117)

class E addresses [118](#ch03.xhtml_page118)

IPv4 configuration [129](#ch03.xhtml_page129)-[131](#ch03.xhtml_page131)

IPv6 addressing [127](#ch03.xhtml_page127)-[129](#ch03.xhtml_page129)

IP version 4 (IPv4) [113](#ch03.xhtml_page113)-[115](#ch03.xhtml_page115)

subnet mask [118](#ch03.xhtml_page118)-[121](#ch03.xhtml_page121)

subnetting [121](#ch03.xhtml_page121)-[126](#ch03.xhtml_page126)

Network Mapper (nmap) [330](#ch09.xhtml_page330)

network troubleshooting

about [326](#ch09.xhtml_page326)

dig command [332](#ch09.xhtml_page332), [333](#ch09.xhtml_page333)

hostname command [334](#ch09.xhtml_page334), [335](#ch09.xhtml_page335)

netstat command [328](#ch09.xhtml_page328), [329](#ch09.xhtml_page329)

nmap command [331](#ch09.xhtml_page331)

ping6 command [326](#ch09.xhtml_page326), [327](#ch09.xhtml_page327)

ping command [326](#ch09.xhtml_page326)

tracepath -6 command [330](#ch09.xhtml_page330)

tracepath command [329](#ch09.xhtml_page329)

traceroute6 command [328](#ch09.xhtml_page328)

traceroute command [327](#ch09.xhtml_page327)

whois command [333](#ch09.xhtml_page333)

New Technology File System (NTFS) [57](#ch02.xhtml_page57)

nmap command [331](#ch09.xhtml_page331)

P

parent process [88](#ch03.xhtml_page88)

parted utility

using [66](#ch02.xhtml_page66)-[71](#ch02.xhtml_page71)

partition

mounting [75](#ch02.xhtml_page75)

unmounting [75](#ch02.xhtml_page75)

password management

about [245](#ch05.xhtml_page245), [246](#ch05.xhtml_page246)

chage command [250](#ch05.xhtml_page250)-[253](#ch05.xhtml_page253)

usermod command [246](#ch05.xhtml_page246)-[250](#ch05.xhtml_page250)

pgrep command [98](#ch03.xhtml_page98)

ping6 command [326](#ch09.xhtml_page326), [327](#ch09.xhtml_page327)

ping command [326](#ch09.xhtml_page326)

pipes and redirects [51](#ch02.xhtml_page51)-[56](#ch02.xhtml_page56)

pkill command [98](#ch03.xhtml_page98)-[105](#ch03.xhtml_page105)

Process Control Block (PCB) [88](#ch03.xhtml_page88)

Process Grep (pgrep) [98](#ch03.xhtml_page98)

Process ID (PID) identifier [88](#ch03.xhtml_page88)

process scheduling [88](#ch03.xhtml_page88)

Process Status (ps) [89](#ch03.xhtml_page89)

process termination [89](#ch03.xhtml_page89)

ps command [89](#ch03.xhtml_page89)-[95](#ch03.xhtml_page95)

pstree command [96](#ch03.xhtml_page96), [97](#ch03.xhtml_page97)

R

Red-hat Package Manager (RPM) [215](#ch04.xhtml_page215)-[219](#ch04.xhtml_page219)

remote access [264](#ch06.xhtml_page264)

rsyslog [226](#ch04.xhtml_page226)-[232](#ch04.xhtml_page232)

S

scalars [311](#ch08.xhtml_page311)

Secure Copy (SCP) [265](#ch06.xhtml_page265)

Secure File Transfer Protocol (SFTP) [265](#ch06.xhtml_page265)

Secure Shell (SSH)

about [264](#ch06.xhtml_page264)-[275](#ch06.xhtml_page275)

security measures [264](#ch06.xhtml_page264), [265](#ch06.xhtml_page265)

security contexts [276](#ch06.xhtml_page276)

Security-Enhanced Linux (SELinux)

about [275](#ch06.xhtml_page275)

advantages [276](#ch06.xhtml_page276)

components [276](#ch06.xhtml_page276)

usage examples [277](#ch06.xhtml_page277)-[279](#ch06.xhtml_page279)

SELinux modes [276](#ch06.xhtml_page276)

SELinux policy [276](#ch06.xhtml_page276)

service command

about [105](#ch03.xhtml_page105)-[108](#ch03.xhtml_page108)

syntax [106](#ch03.xhtml_page106)

services

managing, with systemctl command [108](#ch03.xhtml_page108)-[113](#ch03.xhtml_page113)

shell scripting

about [282](#ch07.xhtml_page282)

basics [282](#ch07.xhtml_page282)-[288](#ch07.xhtml_page288)

scripts, writing with for loops [288](#ch07.xhtml_page288)-[291](#ch07.xhtml_page291)

scripts, writing with if statement [296](#ch07.xhtml_page296)-[304](#ch07.xhtml_page304)

while loop [292](#ch07.xhtml_page292)-[296](#ch07.xhtml_page296)

software management

about [159](#ch04.xhtml_page159)

apt-get command [171](#ch04.xhtml_page171)-[185](#ch04.xhtml_page185)

aptitude command [185](#ch04.xhtml_page185)-[190](#ch04.xhtml_page190)

Debian package management [161](#ch04.xhtml_page161)

dnf utility [204](#ch04.xhtml_page204)-[212](#ch04.xhtml_page212)

dpkg command [161](#ch04.xhtml_page161)-[171](#ch04.xhtml_page171)

software management, key components

package formats [160](#ch04.xhtml_page160)

package manager [160](#ch04.xhtml_page160), [161](#ch04.xhtml_page161)

package repository [159](#ch04.xhtml_page159)

Source NAT (SNAT) [257](#ch06.xhtml_page257)

subnet mask [118](#ch03.xhtml_page118)-[121](#ch03.xhtml_page121)

subnetting [121](#ch03.xhtml_page121)-[126](#ch03.xhtml_page126)

systemctl command

used, for managing services [108](#ch03.xhtml_page108)-[113](#ch03.xhtml_page113)

T

TCP wrappers [258](#ch06.xhtml_page258)-[260](#ch06.xhtml_page260)

tracepath -6 command [330](#ch09.xhtml_page330)

tracepath command [329](#ch09.xhtml_page329)

traceroute6 command [328](#ch09.xhtml_page328)

traceroute command [327](#ch09.xhtml_page327)

U

Ubuntu

directories [3](#ch01.xhtml_page3), [4](#ch01.xhtml_page4)

umount command [80](#ch02.xhtml_page80)-[83](#ch02.xhtml_page83)

unicast address

about [127](#ch03.xhtml_page127)

global unicast address [128](#ch03.xhtml_page128)

link-local unicast address [128](#ch03.xhtml_page128)

site-local unicast address [128](#ch03.xhtml_page128)

unique-local unicast address [128](#ch03.xhtml_page128)

Unified Extensible Firmware Interface (UEFI) [20](#ch01.xhtml_page20)

user accounts

about [234](#ch05.xhtml_page234)-[236](#ch05.xhtml_page236)

last command [238](#ch05.xhtml_page238), [239](#ch05.xhtml_page239)

w command [237](#ch05.xhtml_page237)

whoami command [239](#ch05.xhtml_page239)-[242](#ch05.xhtml_page242)

who command [237](#ch05.xhtml_page237), [238](#ch05.xhtml_page238)

usermod command [246](#ch05.xhtml_page246)-[250](#ch05.xhtml_page250)

V

Virtual LANs (VLANs) [144](#ch03.xhtml_page144)

Virtual Private Network (VPN) [257](#ch06.xhtml_page257)

W

w command [237](#ch05.xhtml_page237)

while loop [292](#ch07.xhtml_page292)-[296](#ch07.xhtml_page296)

whoami command [239](#ch05.xhtml_page239)-[242](#ch05.xhtml_page242)

who command [237](#ch05.xhtml_page237), [238](#ch05.xhtml_page238)

whois command [333](#ch09.xhtml_page333)

X

XFS file system [57](#ch02.xhtml_page57)

Y

YAML Ain't Markup Language (YAML)

about [310](#ch08.xhtml_page310)

basic structure [310](#ch08.xhtml_page310)

comments [310](#ch08.xhtml_page310)

key-value pairs [310](#ch08.xhtml_page310)

lists [310](#ch08.xhtml_page310)

multiline scalars [311](#ch08.xhtml_page311)

nested structure [311](#ch08.xhtml_page311)

scalars [311](#ch08.xhtml_page311)

YAML example

configuration file [312](#ch08.xhtml_page312)

Docker compose [312](#ch08.xhtml_page312)

Kubernetes configuration [312](#ch08.xhtml_page312)

package managers [312](#ch08.xhtml_page312)

Yellowdog Updater, Modified (YUM) [204](#ch04.xhtml_page204)

YUM extender (yumex) [219](#ch04.xhtml_page219)-[226](#ch04.xhtml_page226)

YUM utility [190](#ch04.xhtml_page190)-[202](#ch04.xhtml_page202)

Z

ZFS file system [57](#ch02.xhtml_page57)