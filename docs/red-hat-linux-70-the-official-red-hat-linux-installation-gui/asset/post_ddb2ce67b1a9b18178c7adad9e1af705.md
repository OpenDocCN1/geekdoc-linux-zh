
## 3.4 Step 4 - Do You Have Enough Disk Space?

Nearly every modern-day operating system uses disk partitions, and Red Hat Linux is no exception. When installing Red Hat Linux, it may be necessary to work with disk partitions. If you have not worked with disk partitions before (or would like a quick review of the basic concepts) please read *An Introduction to Disk Partitions* in the appendix of the *Official Red Hat Linux Reference Guide* on the Documentation CD before proceeding.

If Red Hat Linux will share your system with another OS, you will need to make sure you have enough available disk space on your hard drive(s) for this installation.

This disk space must be separate from the disk space used by other OSes you may have installed on your system, such as Windows, OS/2, or even a different version of Linux. This is done by dedicating one or more partitions to Red Hat Linux.

Before you start the installation process, one of the following conditions must be met:

-   Your computer must have enough unpartitioned disk space.
-   You must have one or more partitions that may be deleted, thereby freeing up enough disk space to install Red Hat Linux.
-   You must have a preexisting, formatted FAT (DOS) partition with sufficient disk space, and install using the partitionless installation method (Appendix B, *Installing Without Partitioning*).

> **Please Note**
> To perform a partitionless installation, you also must choose the class of installation you want to perform. However, unlike a typical installation, you will not have to worry about losing any information on your system. A partitionless installation will not remove existing partitions. For more information, turn to Appendix B, *Installing Without Partitioning*.

A workstation-class installation requires at least 900MB of free space. This installation size requirement is the same for partitionless installations.

> **Please Note**
> To use the automatic partitioning feature of Red Hat Linux you must have enough free disk space available (900MB or more), otherwise this option will not appear during your installation.

If you are not sure that you meet these conditions or want to know how to free up more space for your Red Hat Linux installation, please refer to the partitioning appendix in the *Official Red Hat Linux Reference Guide* on the Documentation CD.

## 3.5 Step 5 - Can You Install Using the Red Hat Linux CD-ROM?

Although there are several methods that can be used to install Red Hat Linux, this manual only focuses on installing from the CD-ROM. For instructions on alternative installation methods, refer to the *Official Red Hat Linux Reference Guide* on the Documentation CD.

Installing from a CD requires that you have purchased a Red Hat Linux 7.0 boxed set (or have a Red Hat Linux CD-ROM) and have a CD-ROM drive. Most new computers will allow booting from the CD-ROM. With this method, you can easily use the Red Hat Linux CD-ROM to boot the installation program and perform a local CD-ROM installation.

### 3.5.1 Alternative Boot Methods

There are alternative boot methods available, if you cannot boot from the CD-ROM drive.

#### Local Boot Disk

-   You may need a **local boot disk** or a **PCMCIA boot disk**, if you cannot boot from the CD-ROM drive.
-   Included in your *Official Red Hat Linux 7.0* boxed set is a local boot disk. However, if you do not have a local boot disk (for example, you downloaded Red Hat Linux rather than purchasing an official boxed set) you can make one. Refer to Section 3.5.2, *Making Installation Diskettes* for those instructions.

#### PCMCIA Boot Disk

You may need a PCMCIA boot disk if you are using a PCMCIA device to install Red Hat Linux. If you need a PCMCIA boot disk, you must create one. Refer to Section 3.5.2, *Making Installation Diskettes* for those instructions.

Here’s a checklist to help you determine if you’ll need to create a PCMCIA boot disk:

-   You will install Red Hat Linux from a CD-ROM, and your CD-ROM drive is attached to your computer through a PCMCIA card.
-   You will use a PCMCIA network adapter during the installation.

The PCMCIA boot disk image file is **pcmcia.img**, and is located in the **images** directory on your Red Hat Linux/Intel CD. Refer to Section 3.5.2, *Making Installation Diskettes* for more information.

> **Please Note**
> Although not required to boot your installation, you may occasionally find that a driver disk is needed for you to continue with the installation. The **Driver Disks** appendix in the *Official Red Hat Linux Reference Guide* (on the Documentation CD) explains why a driver disk may be necessary for your installation, and how to obtain one if needed.

### 3.5.2 Making Installation Diskettes

It is sometimes necessary to create a diskette from an **image file**; for example, you may need to use updated image files obtained from the Red Hat Linux errata page or you may need to create a boot disk.

An image file contains an exact copy (or image) of a diskette’s contents. Since a diskette contains filesystem information in addition to the data contained in files, the image file is not usable until it has been written to a diskette.

To start, you’ll need a blank, formatted, high-density (1.44MB), 3.5-inch diskette. You’ll need access to a computer with a 3.5-inch diskette drive, and capable of running an MS-DOS program, or the **dd** utility found on most Linux-based operating systems.

The **images** directory on your Red Hat Linux CD contains the boot images for Red Hat Linux/Intel. Once you’ve selected the proper image, transfer the image file onto a diskette.

#### Making a Diskette Under MS-DOS

To make a diskette under MS-DOS, use the `rawrite` utility included on the Red Hat Linux CD in the `dosutils` directory. First, label a blank, formatted 3.5-inch diskette appropriately (such as "Boot Disk" or "Updates Disk"). Insert it into the diskette drive. Then, use the following commands (assuming your CD is drive d:):

```text
C:\> d:
D:\> cd \dosutils
D:\dosutils> rawrite
Enter disk image source file name: ..\images\boot.img
Enter target diskette drive: a:
Please insert a formatted diskette into drive A: and
press --ENTER-- : [Enter]
D:\dosutils>
```

First, `rawrite` asks you for the `filename` of a diskette image; enter the directory and name of the image you wish to write (for example, `..\images\boot.img`). Then `rawrite` asks for a diskette drive to write the image to; enter `a:`. Finally, `rawrite` asks for confirmation that a formatted diskette is in the drive you've selected. After pressing [Enter] to confirm, `rawrite` copies the image file onto the diskette. If you need to make another diskette, label that diskette, and run `rawrite` again, specifying the appropriate image file.

#### Making a Diskette Under a Linux-Like OS

To make a diskette under Linux (or any other Linux-like operating system), you must have permission to write to the device representing a 3.5-inch diskette drive (known as `/dev/fd0` under Linux).

First, label a blank, formatted diskette appropriately (such as "Boot Disk" or "Updates Disk"). Insert it into the diskette drive (but don't issue a `mount` command). After mounting the Red Hat Linux CD, change directory to the directory containing the desired image file, and use the following command (changing the name of the image file and diskette device as appropriate):

```bash
# dd if=boot.img of=/dev/fd0 bs=1440k
```

To make another diskette, label that diskette, and run `dd` again, specifying the appropriate image file.

## 3.6 Step 6 - Is a Workstation-Class Installation Best For You?

Although Red Hat Linux includes four different classes, or types of installations, this manual only discusses workstation-class installations.

### 3.6.1 What a Workstation-Class Installation Will Do

In choosing automatic partitioning, a workstation-class installation removes all Linux-related partitions on all installed hard drives (and uses all free unpartitioned disk space) to create the following partitions:

-   A 64MB swap partition.
-   A variable-sized root partition (mounted as /) in which all other files are stored (the exact size of this partition is dependent on your available disk space).
-   A 16MB partition (mounted as /boot) in which the Linux kernel and related files reside.

> **Please Note**
> You'll need at least 900MB of free disk space in order to perform a workstation-class installation.

This installation will remove *all* existing Linux partitions on *all* hard drives in your system; non-Linux partitions will not be removed.

A workstation-class installation will install your choice of a GNOME or KDE (or both) desktop environment, and the X Window System.

### 3.6.2 What a Workstation-Class Installation Will Not Do

A workstation-class installation will not erase your Windows 3.1/95/98 configuration. Instead, it will automatically configure your system to dual-boot using LILO (the Linux Loader).

A workstation-class installation will not allow you to customize your group package selection. If you do not want the installation program to select packages for you, please choose a custom-class installation and refer to the *Official Red Hat Linux Reference Guide* on the Documentation CD.
