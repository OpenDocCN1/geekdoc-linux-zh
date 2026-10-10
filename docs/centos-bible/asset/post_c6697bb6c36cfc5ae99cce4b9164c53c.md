
**Install or Upgrade** — If you have an earlier version of CentOS installed, you can choose “Upgrade” to upgrade your system without losing data files. Otherwise, you can continue with a new installation by selecting “Reinstall System.”

**Disk Partitioning Setup** — Choose to remove Linux partitions, all partitions, or no partitions (and use existing free space) to have space to install CentOS. Because repartitioning can result in lost data, I recommend that you refer to descriptions on repartitioning your hard disk later in this chapter.

**Boot Loader Configuration** — Add the GRUB boot manager to control the boot process. (GRUB is described later in this chapter.) With multiple operating systems on the computer, select which one to boot by default.

**Select Hostname** — Choose a hostname for your system.

**Time Zone Selection** — Identify the time zone in which you are located. Uncheck the “System Clock uses UTC” box if you are booting multiple operating systems from this machine because most operating systems expect the BIOS clock to match local time.

**Set Root Password** — Add the root user account password.

**Choose Software** — You can choose from several pre-set installation classes, such as “Desktop” (for laptop, home, or desktop use), “Server” (file, print, Web and other server software), or “Virtualization,” or “Clustering.” I suggest you also select “Customize” now so that you can see exactly which packages you have selected (and add others if you want).

**About to Install** — Up to this point, you can quit the install process without having written anything to disk. When you select Next, the disk is formatted (as you chose) and selected packages are installed.

> **NOTE**
>
> After answering the questions, the actual installation of packages from the DVD takes between 20 and 60 minutes, depending on the number of packages and the speed of the computer hardware. Upgrades can take much longer.

When installation is done, remove the CentOS DVD and click Reboot to reboot your computer. After Linux boots for the first time, the Firstboot runs to let you read the license agreement, set system date and time, configure your display, check your hardware, add a user account, configure your sound card, and install additional CDs. On subsequent reboots, you will see a login prompt. You can log in and begin using your Linux system.

If you need more information than this procedure provides, go to the detailed installation instructions just ahead.

## Detailed Installation Instructions

This section provides more detail on installation. Besides expanding on the installation procedure, this section also provides information on different installation types and on choosing computer hardware.

If anything goes wrong during installation and you get stuck, go to the "Troubleshooting Installation" section at the end of this chapter. It gives suggestions for solving common installation problems.

> **CAUTION** If, when installing Windows or CentOS, you find that the other operating system is no longer available on your boot screen, don't panic; don't immediately reinstall. You can usually recover from the problem by booting the live CD that comes with this book and then using the `grub-install` command to reinsert the proper master boot record. Refer to the "Using the GRUB Boot Loader" section later in this chapter. If you are uncomfortable working in emergency mode, seek out an expert to help you.

### Installing CentOS 5

This chapter details how to install CentOS 5 from the DVD that comes with this book. The DVD that comes with this book and the installation procedures presented here are specific to 32-bit PCs.

### Install or Upgrade?

First, you should determine if you are doing a new install or an upgrade. If you are upgrading an existing CentOS system to the latest version, the installation process will try to leave your data files and configuration files intact as much as possible.

An upgrade installation takes longer than a new install. A new install will simply erase all data on the Linux partitions (or entire hard disk) that you choose. (You can optionally select which partitions to format.)

> **NOTE** While you can upgrade to CentOS from previous CentOS releases, you cannot upgrade in CentOS from a Red Hat Enterprise Linux or Fedora system. The older the CentOS release you are upgrading from, however, the more likely you are to have problems upgrading.

If you choose to upgrade, you can save yourself some time (and disk space) by removing software packages that you don't need. An upgrade will just skip packages that are not installed and not try to upgrade them. Here are a few other tips related to upgrades:

- **Conflicting Packages** — If you upgrade a system on which you installed packages from sources outside of the CentOS Project that conflict with CentOS packages, those features may no longer work. For example, if you replaced GNOME with Xiamin GNOME or used a third-party KDE package set, you can't upgrade those packages to CentOS 5. (It's probably best to remove those packages before upgrading and then apply them again later if you like.)
- **Third-Party Packages** — If you have installed packages from third-party repositories that are specific to your current kernel (such as drivers for NVIDIA video cards or wireless LAN cards), you will need to get new versions of those packages that match your upgraded kernel.

## Part I Getting Started

- **Kernel Requirements** — To upgrade, you must have at least a Linux 2.0 kernel installed on the system you are upgrading.
- **Configuration Files** — With an upgrade, your configuration files that are replaced are saved as *filename.rpmsave* (e.g., the hosts file is saved as *hosts.rpmsave*). More often, however, your old configuration files will remain in place, while the system copies new configuration files to *filename.rpnew*. The location of those files, as well as other upgrade information, is written to */root/upgrade.log*. The upgrade installs the new kernel, any changed software packages, and any packages that the installed packages depend on being there. Your data files and configuration information should remain intact.
- **Digital Certificates** — If you are using digital certificates on your system, you must relocate them to the */etc/pki* directory after the upgrade. (See Chapter 13 for information on setting up digital certificates.)
- **Java** — If you used the Java RPM from Sun Microsystems to provide Java support, conflicts with that package may cause it to be erased during an upgrade. If that occurs, you can install the Java RPM from *jpackage.org* or install the Java tarball from Sun Microsystems into your */opt* directory. You can also consider removing that version of Java from your system and instead using the Open Source Java IcedTea packages.

### From DVD, Network, or Hard Disk?

When you install CentOS, the distribution doesn't have to come from the installation DVD. After booting the installation DVD, type **linux askmethod** at the boot prompt. You are offered the choice of installing CentOS from the following locations:

- **Local DVD or CDROM** — This is the most common method of installing CentOS and the one you get by simply pressing [Enter] from the installation boot prompt. All packages needed to complete the installation are on the DVD that comes with this book.
- **Hard Drive** — If you can place a copy of the CentOS distribution on your hard drive, you can install it from there. (Presumably, the distribution is on a hard drive partition to which you are *not* installing.)
- **NFS Directory** — Allows you to install from any shared directory on another computer on your network using the Network File System (NFS) facility.
- **FTP** — Lets you install from an FTP site (ftp://).
- **HTTP** — Lets you install from a web page address (http://).

If your computer doesn't have a DVD drive, you can use the **boot.iso** CD image that comes on the DVD with the book (see below) to start a network install (HTTP, FTP, or NFS). Just type **linux askmethod** at the boot prompt to begin the installation process.

If you don't have a bootable DVD or CD drive, there are other ways to start the CentOS installation. If you don't have a bootable DVD or CD drive, you need to start the install process from some other medium (such as a PXE server or hard drive, as described later in this chapter).
