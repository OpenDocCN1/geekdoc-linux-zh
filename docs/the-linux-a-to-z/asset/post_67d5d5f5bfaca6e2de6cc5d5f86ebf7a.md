
- **F** A collection of all the HOWTO documents plus the frequently asked questions (FAQ) documents.
- **K** This set contains the source code for the Linux kernel (this was in the D set in early Slackware distributions).
- **I** A collection of user and system manuals for many of the GNU software development packages.
- **IV** InterViews X-windows library, including the sample applications doc and idraw.
- **N** Networking packages (TCP/IP, ppp, UUCP), mail packages (mailx, deliver, elm, pine and sendmail) and network news packages (cnews, tin, trn and nn).
- **OOP** Object-oriented programming. Contains the GNU version of smalltalk and STIX, the smalltalk interface to X-windows.
- **Q** Lots of extra pre-built kernels for various hardware configurations. Frankly, provided you have the disk space available (up to 20 Mb) it is better to build your own, because then it will be exactly right.
- **T** TeX and LaTeX. A document formatting system, with professional typesetting rules built in. This book was formatted with LaTeX.
- **TCL** The Tcl scripting language and the Tk toolkit for rapid development of X-windows applications.
- **X** XFree86. The base X-windows system with the fvwm window manager.
- **XAP** Extra applications for X-windows, including: a paint package (xpaint), an image processing package (xv -- Note that xv is currently unregistered shareware and not free software!), a spreadsheet xspread, several X-windows games, as well as a postscript previewer and print program (ghostview) and a modem communications program (seyon).
- **XD** Packages required to develop your own X-servers.
- **XV** The Xview libraries and the Open Look window managers and an X-windows audio CD player (workman).

- **Y** Games that do not require X-windows including versions of asteroids, tetris and doom.

From this list you can see that you will end up with a fairly powerful and general system if you choose to install the: A, AP, D, F, K, N, X, XAP and Y disk sets.

In addition to the software packages to install, you will also need to obtain the associated software with which to install them. In the case of the Slackware distribution this is supplied on two extra disks along with the rest of the software. You should always read any README type files available with your distribution as these will often contain the very latest updates or changes to more general documentation.

## 7.3 Installing Linux

During the installation and configuration of your Linux system it is a good idea to write a log which records everything you did. In particular, you need to record the choices that you made whenever you needed to make a decision. You are bound to make some choices, which, when you appreciate all their implications, will turn out to have been the wrong ones. There are so many choices that you need to make, some of which will be quite arbitrary, that it is not always easy, when you repeat the exercise, to work out what selections you actually made – unless you write them down.

Once you have your distribution, the next step is to plan its installation. This is especially important if you expect Linux to co-exist with another operating system on the same machine – DOS for example. The biggest problem is going to be to decide how much of your disk space to set aside for each system. If you get this wrong then it can only really be solved by taking all the software off the machine, so that you can move the boundary between the two systems, and then re-installing it all again, with the new disk space sizes. Either that, or you will need to add an extra disk drive to cope with the overflow.

### 7.3.1 Disk Partitions

Assuming that you want DOS and Linux to co-exist on your machine when it is finished, the best starting point is from a machine with empty disks. If the machine is already given over entirely to DOS, then this will mean making a backup (surely you do this already???) of everything you can’t replace from master disks, so that you can repartition the hard disk space to make room for the Linux software.

Under DOS, each disk can be split up into partitions. Up to four primary partitions can be created on each drive. For a simple installation on a single hard disk, this will usually be enough. For example, with a single 320 Mb disk, you might partition the space into three pieces, as in Figure 7.1.

![](img/ad36c2db45661d7b3b68db09c8eea0a1_144_0.png)

### Figure 7.1 Partitioning a 320 Mb hard disk.

Here, the first partition has been set aside for DOS use as the C: drive, the second partition will be used as swap space under Linux and the third partition will be used to hold the Linux root filesystem. Each separate filesystem under Linux will have its own disk partition.

Sometimes you will want to use more than four partitions on a hard drive, especially if it is a rather large drive. In this case, one of the four primary disk partitions can be used as an extended partition. The extended partition is then used like a container to hold a set of logical disk partitions (up to 23 of them under DOS).

In addition to considering extended and logical disk partitions, for really large disk drives, a new problem pops into the frame. Due to a design oversight (the designers couldn’t imagine hard drives becoming available that would be big enough to break their design limits...) you cannot generally boot a PC from a disk partition that uses disk cylinder numbers greater than 1023 (unless you have a modern motherboard whose BIOS supports large drives). For Linux, this means that its root filesystem must lie entirely in a partition under the 1024 cylinder boundary. Linux can hold data and programs in partitions above the boundary; you just can’t boot Linux from these partitions. For an IDE disk, the 1024 cylinder limit comes at 504 Mb.

Suppose, then, that you have a 720 Mb IDE disk and you want to partition it to give a 150 Mb DOS C: drive, a 200 Mb DOS D: drive (probably to use as a compressed drive), a 16 Mb Linux swap partition and then the rest of the disk (354 Mb) for Linux filesystem space. Figure 7.2 shows one possible disk partitioning arrangement which takes all the constraints into account.

Notice that the Linux space has been split into two parts, so that the partition holding the root filesystem can fit below the 504 Mb boundary. This leaves the problem of where in the Linux directory tree the other Linux filesystem/partition can usefully be mounted. One obvious division, and the one shown here, is to split the Linux space into a system partition and a user partition. All of the Linux installation will then be made into the root partition, which leaves the other partition initially empty and allows it to be used as user home directory and working space, by mounting it as /home. Many other arrangements are possible and you may need to experiment until you find the one that suits your own particular circumstances best.

![](img/ad36c2db45661d7b3b68db09c8eea0a1_145_0.png)

### Figure 7.2 Partitioning a 720 Mb hard disk.

The program used to partition disks is called fdisk, both under DOS and under Linux. In general, you should only create the partitions to be used within a particular operating system using that system’s own fdisk command. So the first task in our example is to install DOS from the master disks, using the DOS fdisk command to create just the required DOS partitions, leaving the rest of the disk space unallocated.

Most Linux distributions supply a one- or two-disk set, which you need to use to boot Linux on your machine initially. With the Slackware distribution there are two disks required, called the boot and root disks. In fact, there are several different versions of each of them, and you will need to select an appropriate one of each. The choice is based on what type of hard disk you will be installing to (SCSI or not) and what medium you will be using as the source of the files to install from (CD-ROM, floppy disk, hard disk or network).

You should consult the release notes supplied with your distribution (probably as a README file or a thin paper leaflet) to help you make the appropriate choice and to tell you how to create the boot and root disks from the files available.
