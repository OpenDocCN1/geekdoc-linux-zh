+   ▶ `/usr`—This directory holds nearly all the software on a Fedora system and can become quite large if additional software is added, especially on a workstation configuration. Using a separate partition can make sense. A full install requires at least 6GB for this directory or more if additional software is added.

+   ▶ `/var`—Placing this directory (or perhaps some of its subdirectories) on a separate partition can be a good idea, especially because security logs, mail, and print spooling take place under this tree. You should reserve at least 1GB of storage for `/var`, especially if using Fedora as a print server (as spooled documents reside under `/var/spool`).

# **TIP**

> As a *general rule*, it is a good idea to segregate user and system data. Although a Linux system can be restored quickly, user data has a much greater value and can be much more difficult to replace. Segregating data can make the job of backing up and restoring much easier. If you ever have a problem accessing your partition, we recommend that you get the excellent Knoppix distribution that boots and runs entirely from CD. This will enable you to access your partitions and make any necessary repairs.

# Using Fedora’s kickstart Installation Method

Automating the installation process can save system administrators a lot of time and effort during an initial deployment, upgrade, or maintenance cycle by managing multiple computers at one time. Fedora offers a highly automated installation technique called *kickstart*, developed by Red Hat, which can be used for unattended installation of Linux.

Fedora’s *kickstart* installation uses a single configuration file with a special, extensive syntax on a server, boot floppy, or other medium to install Fedora via CD/DVD, a hard drive partition, or a network connection. Using *kickstart* is easy and involves passing a kernel argument to the Fedora Linux boot kernel. The various arguments tell the boot kernel to look for a configuration file on floppy, a designated server, via a network, specific file, or CD/DVD.

You can use *kickstart* to install Fedora on one or more computers at the same time. First, set up a web or FTP server with Fedora’s installation files. Next, create a network boot floppy, using the techniques described in the next section. Follow the directions given here (choosing an FTP install), and then copy the custom *kickstart* file to the network boot floppy. You can then use this floppy (and copies) to boot one or more PCs to a network boot install, using your FTP server.

# **TIP**

> Fedora does not automatically install `system-config-kickstart`, the utility used to create and customize `system-config-kickstart` files. Be sure that you install it, using either yum or the Add/Remove Programs tool.