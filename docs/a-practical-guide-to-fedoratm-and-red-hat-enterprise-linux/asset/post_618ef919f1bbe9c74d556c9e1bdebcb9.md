
## FEATURES OF THIS BOOK

This book is designed and organized so you can get the most out of it in the least amount of time. You do not have to read this book straight through in page order. Instead, once you are comfortable using Linux, you can use this book as a reference: Look up a topic of interest in the table of contents or in an index and read about it. Or think of the book as a catalog of Linux topics: Flip through the pages until a topic catches your eye. The book includes many pointers to Web sites where you can obtain additional information: Consider the Internet to be an extension of this book. A Practical Guide to Fedora™ and Red Hat® Enterprise Linux®, Seventh Edition, is structured with the following features

- In this book, the term “Fedora/RHEL” refers to both Fedora and Red Hat Enterprise Linux. Features that apply to only one of these operating systems are marked as such.
- Optional sections enable you to read the book at different levels, returning to more difficult material when you are ready to delve into it.
- Caution boxes highlight procedures that can easily go wrong, giving you guidance before you run into trouble.
- Tip boxes highlight ways you can save time by doing something differently or situations when it may be useful or just interesting to have additional information.
- Security boxes point out places where you can make a system more secure. The security appendix presents a quick background in system security issues and includes a tutorial on GPG.
- Concepts are illustrated by practical examples throughout the book.
- Each chapter starts with a list of chapter objectives—a list of important tasks you should be able to perform after reading the chapter.
- Chapter summaries review the important points covered in each chapter.
- Review exercises are included at the end of each chapter for readers who want to further hone their skills. Answers to even-numbered exercises are posted at www.sobell.com.
- The Glossary defines more than 500 commonly encountered terms.
- The chapters covering servers include JumpStart sections that get you off to a quick start using clients and setting up servers. Once a server is up and running, you can test and modify its configuration, as is explained in the rest of each of these chapters.
- This book provides resources for **finding software** on the Internet. It also explains how to **download** and **install** software using *yum*, the Software window, and BitTorrent. It details controlling automatic updates using the Software Update Preferences window.
- This book describes in detail many important **GNU tools**, including the Gnome 3 desktop, the Nautilus File Browser, the *parted* and **gnome-disks** partition editors, the **gzip** compression utility, and many command-line utilities that come from the GNU Project.
- Pointers throughout the text provide help in obtaining **online documentation** from many sources, including the local system, the Fedora/RHEL Web sites, and other locations on the Internet.
- Multiple **comprehensive indexes** help you locate topics quickly and easily.

## Key Topics Covered in This Book

This section distills and summarizes the information covered by this book. In addition, “Details” (starting on page 1) describes what each chapter covers. Finally, the Table of Contents (starting on page xvii) provides more detail. This book:

- Describes how to download Fedora installation images from the Internet and write/burn the Fedora Live or Install Image to a USB flash drive or DVD.
- Helps you plan the layout of the system’s hard disk. It includes a discussion of partitions, partition tables, and mount points, and assists you in using Anaconda or the **gnome-disks** disk utility to examine and partition the hard disk.
- Explains how to set up a dual-boot system so you can install Fedora/RHEL on a Windows system and boot either operating system.
- Discusses booting into a live Fedora session and installing Fedora from that session.
- Describes in detail how to use the new version of **Anaconda**, Fedora/RHEL’s installation program, to install Fedora/RHEL from an Install Image.
- Covers testing installation media for defects, setting boot command-line parameters (boot options), and creating a RAID array.
- Describes how to set up a VM (virtual machine) and install Fedora on the VM.
- Explains how to use the Logical Volume Manager (LVM2) to set up, grow, and migrate logical volumes, which are similar in function to traditional disk partitions.
- Introduces the GNOME 3 Standard and Classic desktops (GUIs), and explains how to use desktop tools, including application and context menus, the Settings window, the Nautilus File Browser, and the GNOME terminal emulator.
- Covers the Bourne Again Shell (bash) in three chapters, including an entire chapter on shell programming, which includes many sample shell scripts. These chapters provide clear explanations and extensive examples of how bash works both from the command line in day-to-day work and as a programming language in which to write shell scripts.
- Explains the textual (command-line) interface and introduces more than 32 command-line utilities.
- Presents a tutorial on the vim and nano textual editors.
- Covers types of networks, network protocols (including IPv6), and network utilities.
- Explains hostnames, IP addresses, and subnets, and explores how to use host and dig to look up domain names and IP addresses on the Internet.
- Covers distributed computing and the client/server model.
- Explains how to use ACLs (Access Control Lists) to fine-tune user access permissions.
- Describes CentOS by virtue of that operating system’s compatibility with RHEL. CentOS (www.centos.org) is a free Linux distribution that has more long-term stability than Fedora.
- Explains how to use the Fedora/RHEL graphical and textual (command-line) tools to configure the display, DNS, NFS, Samba, Apache, a firewall, a network interface, and more. You can also use these tools to add users and manage local and remote printers.
- Describes how to use su to work with root privileges (become Superuser), and the advantages and dangers of working with escalated privileges.
- Goes into detail about using sudo to allow specific users to work with root privileges and customizing the way sudo works by editing the sudoers configuration file.
- Describes how to use the following tools to download and install software to keep a system up-to-date and to install new software:
    - The **yum** utility downloads and installs software packages from repositories on the Internet, keeping a system up-to-date and resolving dependencies as it processes the packages.
    - **BitTorrent** is a good choice for distributing large amounts of data such as the Fedora/RHEL Install Image. The more people who use BitTorrent to download a file, the faster it works.
- Covers graphical system administration tools, including the many tools available from the GNOME desktop.
- Explains system operation, including the boot process, rescue (single-user) and multiuser modes, and steps to take if the system crashes.
- Details the workings of the **systemd init daemon**, which replaces both the Upstart and System V init daemons.
- Explains how to set up and use the **Cacti** network monitoring tool to graph system and network information over time, including installing and setting up the **LAMP** (Linux, Apache, MariaDB/MySQL, and PHP) stack.
- Provides instructions on installing, setting up, and using a **MariaDB/MySQL** relational database.
- Discusses setting up and repairing an **XFS** filesystem.
- Describes files, directories, and filesystems, including types of files and filesystems, **fstab** (the filesystem table), and automatically mounted filesystems, and explains how to fine-tune and check the integrity of filesystems.
- Covers backup utilities, including **tar** and **cpio**.
- Describes compression/archive utilities, including **xz, gzip, bzip2, compress,** and **zip**.
- Explains how to customize and build a Linux kernel.
- Helps you manage basic system security issues using **ssh** (secure shell), **vsftpd** (secure FTP server), **Apache** (Web server), **firewalld** and **iptables** (firewalls), and more.
- Includes a tutorial on using **GPG** (GNU Privacy Guard) to provide identification, secrecy, and message integrity in email and file sharing.
- Describes how to use the graphical **firewall-config** utility to protect the system.
- Provides instructions on using **iptables** to share an Internet connection over a **LAN** and to build advanced firewalls.
- Presents a complete section on **SELinux** (Security-Enhanced Linux), including instructions for using **system-config-selinux** to configure SELinux.
- Describes how to set up a **chroot** jail to help protect a server system.
