
- For the DVD, choose whether you want to install or upgrade an existing system.
- For the install/live CD, let the boot screen time out. When the CD boots up to a GNOME desktop, double-click the Install to Hard Drive icon to begin the installation.

During installation, you are asked questions about your computer hardware and the network connections. After you have completed each answer, click Next. The following list describes the information you will need to enter. (If you need help, all of these topics are explained later in this chapter.)

- **Install or Upgrade** — If you are installing from DVD and have an earlier version of Fedora installed, you can choose Upgrade to upgrade your system without losing data files. Otherwise, you can continue with a new installation by selecting **Install Fedora**. (Upgrades are not supported when you are installing from the live CD.)
- **Media Check** — If you are installing from the DVD, you can optionally check the DVD to be sure it is not damaged or corrupted. This choice is not on the live CD.
- **Language Selection** — Choose the language used during the install (you can add other languages later). This choice is not on the live CD.
- **Keyboard Configuration** — Choose your keyboard type from a list of international keyboard types.
- **Select Hostname** — Choose a hostname for your system.
- **Time Zone Selection** — Identify the time zone in which you are located. Uncheck the System Clock uses UTC box if you are booting multiple operating systems from this machine because most operating systems expect the BIOS clock to match local time.
- **Set Root Password** — Add the root user account password.
- **Disk Partitioning Setup** — Choose to remove Linux partitions, all partitions, or no partitions (and use existing free space) to have space to install Fedora. Because repartitioning can result in lost data, I recommend that you refer to descriptions on repartitioning your hard disk later in this chapter.
- **Boot Loader Configuration** — Add the GRUB boot manager to control the boot process. (GRUB is described later in this chapter.) With multiple operating systems on the computer, select which one to boot by default.
- **Choose Software** — If you are installing from DVD, choose from several preset installation classes, such as Desktop and Productivity (for laptop, home, or desktop use), Software Development (desktop plus software development), or Web Server (file, print, Web, and other server software). I suggest you also select Customize now so that you can see exactly which packages you have selected (and add others if you want to). If you are installing from the live CD, you won’t be able to choose the software to install (in this or the next step) because the entire contents of the CD are installed to hard disk.
- **Installation Categories** — If you are installing from DVD, select each category that appears to see which groups of software packages are installed. Then select the Optional packages button to add or subtract packages from each group.
- **Installation** — Up to this point, you can quit the install process without having written anything to disk. When you select Next from the installation categories, the selected packages are installed.

> **NOTE:** After answering the questions, the actual installation of packages from the DVD takes between 20 and 60 minutes, depending on the number of packages and the speed of the computer hardware. For the live CD, the installation process is typically much faster because the contents of the CD are simply copied to hard disk. Upgrades can take much longer.

When installation is done, remove the Fedora DVD and click Exit to reboot your computer. If you installed from the live CD, reboot your computer and remove the live CD before it’s time for the installed system to boot. Linux should boot by default. After Linux boots for the first time, Firstboot runs to let you read the license information, set the system date and time, add a user account, and optionally, send the Fedora Project details of your system hardware. On subsequent reboots, you will see a login prompt. You can log in and begin using your Linux system.

If you need more information than this procedure provides, go to the detailed installation instructions just ahead.

## Detailed Installation Instructions

This section provides more detail on installation. Besides expanding on the installation procedure, this section also provides information on different installation types and on choosing computer hardware.

If anything goes wrong during installation and you get stuck, go to the section “Troubleshooting Installation” at the end of this chapter. It gives suggestions for solving common installation problems.

> **CAUTION:** If, when installing Windows or Fedora, you find that the other operating system is no longer available on your boot screen, don’t panic and don’t immediately reinstall. You can usually recover from the problem by booting the live CD that comes with this book, and then using the grub-install command to reinsert the proper master boot record. Refer to the section “Using the GRUB boot loader” later in this chapter. If you are uncomfortable working in emergency mode, seek out an expert to help you.

# Installing Fedora 12

This chapter details how to install Fedora 12 from the DVD that comes with this book. If you don’t have a DVD drive, you can use the Fedora live/install CD that comes with this book to do a basic desktop install. If you are installing Fedora from those media, you can simply follow the instructions in this chapter.

## Choosing an installation method

Fedora offers very flexible ways of installing the operating system. This book comes with the following installation media (described in Appendix A):

- **Fedora 12 DVD** — Contains the entire Fedora 12 operating system, including all binary packages that are associated with a software group.
- **Fedora 12 Desktop Live CD** — If you don’t have a DVD drive, you can install from the included official Fedora 12 Desktop Live/install CD. The CD lets you run a live version of Fedora 12 that includes the GNOME desktop environment. From the running live CD system, you can launch an install process that copies the entire contents of the live CD to your hard disk. Once you have Fedora installed, you can download any missing packages later.

If your computer has a DVD drive, I recommend installing Fedora from the DVD that comes with this book after testing your computer with the live CD. However, if you don’t have a DVD drive, you also have the option of installing a desktop Fedora system from the CD with this book or from any of several different types of media. There are also several special types of installation, described fully in the section “Special Installation Procedures.”

## Install or upgrade?

First you should determine if you are doing a new install or an upgrade. If you are upgrading an existing Fedora system to the latest version, the installation process will try to leave your data files and configuration files intact as much as possible. You also need to do the upgrade from the DVD because upgrades are not available from the Fedora live CD.

An upgrade installation takes longer than a new install. A new install will simply erase all data on the Linux partitions (or entire hard disk) that you choose. (You can optionally select which partitions to format.)

> **NOTE:** While you can upgrade to Fedora 12 from previous Fedora releases, you cannot upgrade to Fedora 12 from a Red Hat Enterprise Linux or CentOS system. The older the Fedora release you are upgrading from, however, the more likely you are to have problems upgrading.

If you choose to upgrade, you can save yourself some time (and disk space) by removing software packages you don’t need. An upgrade will just skip packages that are not installed and not try to upgrade them. Here are a few other tips related to upgrades:

- **Conflicting packages** — If you upgrade a system on which you installed packages from sources outside of the Fedora project that conflict with Fedora packages, those features may no longer work. For example, if you replaced GNOME with Ximian GNOME or used a third-party KDE package set, you can’t upgrade those packages to Fedora 12 (it’s probably best to remove those packages before upgrading, and then apply them again later if you like.)
