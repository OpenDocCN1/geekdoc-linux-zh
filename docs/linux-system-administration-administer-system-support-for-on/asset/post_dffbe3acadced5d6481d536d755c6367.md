
## Part I: Basics of Linux System Administration

- **CHAPTER 1:** Slackware Linux Installation
- **CHAPTER 2:** A System Administrator’s Responsibilities
- **CHAPTER 3:** File System and Disk Management
- **CHAPTER 4:** Devices and Peripherals

### IN THIS PART

Part 1 explains how to get started with Slackware Linux. Chapter 1 shows you how to set up Linux and use compatible hardware; Chapter 2 outlines your probable responsibilities as a system administrator – including the orderly growth of your system as well as your day-to-day general tasks – and Chapters 3 and 4 explain setup and usage procedures for disks, peripherals, and other devices on a Linux system.

Mastering the fundamental system-administration skills outlined in this part of the book should help you feel more comfortable as you work with Slackware Linux. Once you have these skills, you can start tackling more advanced topics, and you may also want to take a look at Part 2.

## Chapter 1: Slackware Linux Installation

### IN THIS CHAPTER

- Installing Slackware
- Understanding some basic configurations
- Upgrading Slackware
- Exploring maintenance issues
- Monitoring performance
- Securing your system

### Installing Slackware

Your PC is all fired up and you're ready to install Slackware. You've done the hardest part: You purchased or borrowed a PC. The first step after that is to check your system requirements.

Basic hardware requirements for installing Linux include a monitor, a keyboard, at least eight megabytes of RAM, at least 250 megabytes of hard drive space, 3.5-inch or 1.25-inch floppy drive, and a compatible CD-ROM drive. You can get away with a 386 processor; however, I recommend at least a 486 because it does improve performance.

You’ll also need at least four blank diskettes for the boot disk and root disk used for installing Slackware, a boot disk (which may or may not be necessary), and a rescue disk for emergencies (such as the file system going south).

You’ll also need patience. If you're working with a standard desktop or tower environment, you shouldn't have too many problems — but be aware of what can go wrong, and exercise your patience on such surprises as kernel panic and boot problems.

In addition to all the system basics, some highly recommended stuff can get your system to run Linux as smoothly as possible. You need a serial mouse, especially if you want to run X. (A PS/2 or bus mouse uses a little round port to plug into the back of your computer; it also is a headache to configure.) Have a known, compatible video card (such as an S3 model) to use X. Any compatible tape drive, external removable disks such as Jaz or Zip, or a CD-R would be great for doing backups. Doing a backup with floppies is impractical, time-consuming, and humorous if you’re not the one doing it. (One other quality that I highly recommend for system administrators is a sense of humor.)

Sometimes installing Linux may become a “character-building experience” – meaning the beast won’t work quite right – as I can attest. After you go through enough uninformative README files, you learn that hosing your system is only one small part of being a system administrator.

![](img/8ad518fddafc7f5e73715a2604b61d50_31_0.png)

> Laptop installations can be tricky. Many of the video chips and hardware, such as drive types and CD-ROMs, can be difficult to get working properly.
>
> Please refer to *Linux Installation and Configuration*, 4E for more information on configuring and installing Linux on laptops.

### Examining the Slackware CD-ROM

Now that you have your PC set up, examine the contents of the Slackware CD-ROM included with this book. You can use the computer you’re going to install Slackware Linux on, provided it has another operating system such as Windows 95 or Windows 98 already installed. Keep in mind that you can view the CD-ROM on any type of operating system that supports the ISO 9660 CD-ROM standard.

After you load the Slackware CD-ROM accompanying this book, you’ll notice the files `README.TXT`, `README34.TXT`, and `CD_INST.TXT`. If you’re on a DOS or Windows operating system, you can use `VIEW.EXE` to view these files. Also, you’ll notice a few directories listed. If you’re using Windows 95 or NT Explorer, your CD-ROM directory looks something like Figure 1-1.

![](img/8ad518fddafc7f5e73715a2604b61d50_31_1.png)

Figure 1-1: Slackware LINUX CD-ROM directory, viewed from Windows 95 Explorer.

If you’re on a UNIX system, the directories and files look like this:

```bash
# ls
BOOTING.TXT INSTALL.GER UPGRADE.TXT install slackware
COPYING INSTALL.TXT bootdsks.12 kernels source
COPYRIGHT.TXT LOWER.TXT bootdsks.144 live zipslack
ChangeLog.txt MIRRORS.TXT contents modules
FAQ.TXT README.TXT contrib rootdsks
FILELIST.TXT README35.TXT docs slaktest
```

You can read the text files directly from a UNIX-based operating system. If you try to use the Windows executable view.exe to view them from UNIX, you get an error message like this one:

```bash
# ./view.exe
./view.exe: cannot execute binary file
```

The following list summarizes the Slackware CD-ROM directories.

- **Bootdsks.12** – 1.2MB boot disk images
- **Bootdsks.144** – 1.44MB boot-disk images
- **Contents** – Shows where the files are installed for each package
- **Contrib** – Extra Slackware packages that are not supported
- **Docs** – Various HOWTOs, FAQs, and other useful documents
- **Install** – Information and executables necessary for FIPS
- **Kernels** – Precompiled kernels
- **Live** – Live file system
- **Modules** – Dynamically loadable modules that provide additional hardware support
- **Rootdsks** – Disks for installing, configuring, or rescuing your Linux system
- **Slaktest** – Package that lets you run Slackware from a CD-ROM with minimal use of your hard drive
- **Slackware** – Primary Slackware packages
- **Source** – Source code for Slackware
- **ZipSlack** – Utility for installing an up-to-date Slackware Linux system on a DOS partition

### Creating Installation Disks

Now that you know the contents of your CD-ROM, make two installation disks: a root disk and a boot disk. A boot disk has a small kernel that enables you to boot your hardware, and a root disk contains the installation program with a minimal Linux file system.

#### MAKING THE BOOT DISK

To make your computer recognize Linux, create a boot disk. This disk functions similarly to a boot disk for DOS or Windows. In fact, you can create your Linux boot and root disks from Windows or DOS, as well as from Linux.

To create your boot disk, first look at the file /cdrom/bootdsks.144/WHICH.ONE or /cdrom/bootdsks.12/WHICH.ONE and match your installation media with the correct kernel. Kernels for IDE drives end in .i, and kernels for SCSI controllers end in .s. For example, I have a Sanyo IDE/ATAPI CD-ROM drive from which I'm installing the software, so I want a kernel that supports IDE drives; I'd look for one that ends in .i.

To create your boot disk, you can use the Windows batch file in the directory bootdsks to create the batch file that corresponds to the boot-disk file.

In the file WHICH.ONE, the first column represents the installation media, the second column is the IDE kernel, and the third column shows the SCSI kernel.

For my CD-ROM, WHICH.ONE shows the following:

| Drive Model | IDE Kernel | SCSI Kernel |
| :--- | :--- | :--- |
| Sanyo CDR-H94A | sanyo.i | sanyo.s |

Because it's an IDE drive, I use sanyo.i. To get this kernel to a bootable disk (thus a boot disk), use RAWRITE.EXE in a Windows-based system. What are even better are the batch files, which do most of the work for you.

To create a 1.44MB boot disk using the batch file, go to the directory D:\Bootdsks.000\ide-bat. (You can read the text files directly from a UNIX-based operating system.) From there, double click the file sanyo.bat. The following message appears:

```text
"This option makes the sanyo.i disk."
"Please insert a formatted high-density diskette, and press"
"a key to make the disk, or CTRL-C to abort..."
Press any key to continue . . .
```

After you press any key, the next message appears:

```text
Number of sectors per track for this disk is 18
Writing image to drive A: Press ^C to abort.
Track: 07 Head: 1 Sector: 16
```
