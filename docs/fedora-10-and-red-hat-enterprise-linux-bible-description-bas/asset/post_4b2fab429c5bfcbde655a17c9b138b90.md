
# Part I: Getting Started in Fedora RHEL

# Quick Installation

It can be a little intimidating to see a thick chapter on installation. But the truth is, if you have a little bit of experience with computers and a computer with common hardware, you can possibly install Fedora or RHEL easily. The procedure in this section will get you going quickly if you have:

- *Media* - The Fedora installation DVD or live/install CD that comes with this book.
- *PC* - A Pentium-class PC (at least 200 MHz for text mode; 400 MHz Pentium II for GUI) with a built-in bootable DVD or CD drive, at least 128MB of RAM (for text mode) or 192MB of RAM (for GUI mode; although 256MB is the recommended minimum).
- *Disk Space* - If you are installing the live CD, you need at least 3GB of disk space. Keep in mind that the live CD only copies the CD files to your hard disk. You don't get to select individual packages, as you do when installing from the DVD (The fact that files are compressed on the CD accounts for the need for more disk space than the 700MB CD image would indicate)

With the DVD, there are no preset install sets in Fedora 10, essentially every installation is a custom installation (although you can go with a default package set). Depending on which packages you choose to install, the disk space you need can range from 600MB (for a minimal space with no GUI) to 10GB (to install all packages). I would recommend from 2GB to 3GB minimum if you are installing a desktop system. (The Fedora Project recommends at least 5 percent of free space, plus any disk space you require for user data.)

For this quick procedure, you must either dedicating your entire hard disk to Linux, have a preconfigured Linux partition, or have sufficient free space on your hard disk outside any existing Windows partition.

> CAUTION: If you are not dedicating your hard disk to Linux and you don't understand partitioning, skip to the "Detailed Installation Instructions" in this chapter. That section describes choices for having both Linux and Windows on the same computer.

Here's how you started:

- 1 Insert the Fedora 10 installation DVD or CD into your computer's drive.
- 2 Reboot your computer.
- 3 The next step depends on whether you are using the live CD or DVD that come with this book:
    - For the DVD, select to install or upgrade an existing system.
    - For the install/live CD, let the boot screen time out. When the CD boots up to a KDE desktop, double-click the Install to Hard Drive icon to begin the installation.

# Chapter 2: Installing Fedora 27

During installation, you are asked questions about your computer hardware and the network connections. After you have completed each answer, click Next. The following list describes the information you will need to enter. (If you need help, all of these topics are explained later in this chapter.)

- Media Check — If you are installing from the DVD, you can optionally check the DVD to be sure it is not damaged or corrupted. This choice is not on the Live CD.
- Language Selection — Choose the language used during the install (you can add other languages).
- Keyboard Configuration — If you are installing from DVD, choose your keyboard type.
- Install or Upgrade — If you are installing from DVD and have an earlier version of Fedora, you can choose Upgrade to upgrade your system without losing data files. Otherwise, you can continue with a new installation by Reinstall System. (Upgrades are not supported when you are installing from the live CD.)
- Select Hostname — Choose a hostname for your system.
- Time Zone Selection — Identify the time zone in which you are located. Uncheck the System Clock box if you are booting multiple operating systems from this machine because most operating systems use the BIOS clock to match time.
- Set Root Password — Add the root user account password.
- Disk Partitioning Setup — Choose to remove Linux partitions, all partitions, or no partitions (using free space) to have install to Fedora. Because repartitioning can result in lost data, I recommend that you refer to descriptions on repartitioning your hard disk in this chapter.
- Boot Loader Configuration — Add the GRUB boot manager to control the boot process. (described in this chapter). With multiple operating systems on the computer, select one to boot by default.
- Choose Software — If you are installing from DVD, choose from several preset installation classes, as Office and Productivity (laptop, home, or desktop use), Software Development (desktop plus software development), or Web Server (file, print, Web, and other server software). I suggest you Customize now that you can see exactly what you have selected (and add others if you want). If you are installing from the live CD, you won't be able to choose the software to install (in this or the next step) because the entire contents of the CD are installed to hard disk.
- Installation Categories — If you are installing from DVD, select each category that appears to see which groups of software packages are installed. Then select the Optional packages button to add or subtract packages from each group.
- About to Install — Up to this point, you can quit the install process without having written to disk. When you select Next, the disk is formatted (as you chose) and selected packages are installed.

> NOTE: After answering the questions, the actual installation of packages from the DVD takes between 20 and 60 minutes. If you are using the live CD, the installation is typically faster. When installation is done, you can reboot. After Linux boots for the first time, you can log in.

If you need more information, go to the Detailed Installation Instructions. This section provides more detail on installation. Linux and Windows. If you don't understand partitioning, skip to the "Detailed Installation Instructions" in this chapter. That section describes choices for having both Linux and Windows on the same computer.

> CAUTION: If you are not dedicating your hard disk to Linux and you don't understand partitioning, skip to the "Detailed Installation Instructions" in this chapter. That section describes choices for having both Linux and Windows on the same computer.

# Part I: Getting Started in Fedora and RHEL

# Chapter 2: Installing Fedora 29

# Choosing an installation method

Fedora offers very flexible ways of installing the operating system. This book comes with the following media:

- Fedora 10 DVD — Contains nearly the Fedora 10 operating system, including all packages.
- Fedora 10 KDE Desktop Live — If you don't have a DVD drive, you can install from the included Fedora 10 that includes the Desktop Environment (KDE).

# Install or upgrade?

First you should determine if you are doing a new install or an upgrade. If you are upgrading an existing Fedora system to the latest version, the installation process will try to leave your data files and configuration files as much as possible. You also need to do the upgrade from the DVD because upgrades are not available from the live CD.

An upgrade installation takes longer than a new install. A new install will simply erase all data on the Linux partitions (or entire hard disk) that you choose.

> NOTE: While you upgrade to Fedora 10 from previous Fedora releases, you cannot upgrade to Fedora 10 from a Red Hat Enterprise Linux or CentOS OS. The Fedora release you are upgrading from, however, the more likely you are to have problems upgrading.

If you choose to upgrade, you can save some time (and disk space) by removing software packages you don't need. An upgrade will just skip packages that are not installed and not try to upgrade them. Here are a few other tips to upgrades:

- Conflicting packages — If you upgrade a system on which you installed packages from sources outside of the Fedora project that conflict, those features may no longer work. For example, if you replaced GNOME with Xian GNOME or used a third-party KDE package set, you can't upgrade those packages to Fedora 10.
