
## Chapter 2: Installing Fedora Core

### In This Chapter

- Making a list of your PC's hardware
- Setting aside disk space for Fedora Core
- Starting the Fedora Core installation
- Creating hard disk partitions for Fedora Core
- Setting up key system partitions
- Selecting packages to install

comes with Microsoft Windows preinstalled. If you want to use Fedora Core, first you have to install it. This book comes with the Fedora Core DVD-ROM — all you have to do to install it is follows the steps in this chapter.

You may feel worried about installing a new operating system on your PC. You may feel that it is like brain surgery —, rather, more grafting on a new brain because you can install Fedora Core in addition to Microsoft Windows. When you install two operating systems like that, you can choose to start one or the other as you power up the PC. The biggest headache in adding Fedora Core to a PC with Windows is creating a new partition — basically setting aside a part of the disk — for Fedora Core. The rest of the installation is fairly routine — just a matter of following the instructions. I explain everything in this chapter.

## Following the Installation Steps

Installing Fedora Core involves a number of steps — and I want to walk you through them briefly, without the details. Then you can follow the details and install Fedora Core from this book's companion DVD-ROM.

The very first step is to make sure that your PC and its peripheral components are Linux-friendly and you can successfully install Fedora Core on the PC. Linux installation has come a long way from the old days when you had to manually load drivers for your specific brand of components such as CD-ROM drive and network card. Nowadays the Fedora Core installation program (called Anaconda) can detect and work with most PC peripherals.

If you run into a problem installing Fedora Core mailing lists at Red Hat's Web site (www.redhat.com/mailman/listinfo) and look through the archives. Chances someone else has the same problem and a solution has been suggested in the mailing list. You may also get good results by searching Google (www.google.com) with the words Fedora Core and make the model of the peripheral that's giving you a problem.

![](img/d9230b719dc0efd80851f363d8c6f571_58_0.png)

The second step is to make sure that your PC can boot from the DVD/CD-ROM drive. This book comes with Fedora Core on a DVD. If you don't have a DVD-ROM drive, you can order the CDs by using the coupon at the back of the book.

![](img/d9230b719dc0efd80851f363d8c6f571_58_1.png)

Prior to Fedora Core 2, you could prepare a Fedora Core installer disk — a floppy disk you could use to boot the PC when you start the installation. Unfortunately, the Linux kernel used during the Fedora Core installation is too big to fit on a 1.44MB floppy disk. Therefore, in order to install Fedora Core, you need a PC with a DVD/CD drive and the ability to boot from that DVD/CD drive. If your PC has a CD drive only (no DVD drive), you have to get the Fedora Core CDs (see the back page of this article for more information).

The third step is to make room for Fedora Core on your PC's hard disk. If you're running Windows, this step can be easy or hard, depending on whether you want to replace Windows with Fedora Core or keep both Windows and Fedora Core.

If you want to install Fedora Core without removing (or disturbing) Windows, remember that your existing operating system — which is, I assume, Windows 95, 98, NT, 2000, or XP — is currently using the entire hard disk. That means you have to partition (divide) the hard disk so Windows can live on one part of it and Fedora Core live on the other. Doing so can be a scary step because you run the risk of ruining the hard disk and wiping out whatever is inside.

Before you create a new place on your hard drive that the Fedora Core installation program, you may use to preserve your peace of mind by using a program to create the partition. If your version of Windows is NT, 2000, or XP, consider investing in a commercial hard-drive partitioning product such as PartitionMagic. For Windows 95/98 systems, you can use a program FIPS (included in this book's DVD-ROM).

After you set up a hard-drive partition for Fedora Core, you can begin the final step — boot the PC from your Fedora Core installer disk and start the Fedora Core installation. Quite a few steps occur during installation, but when you've come this far, it should be smooth sailing. Just go through the installation screens and you are done in an hour or two. The Fedora Core installer brings up a graphical user interface (GUI) and guides you through all the steps. One key step involves partitioning the hard disk, but this you simply split the extra partition you created earlier. Before a few configuration steps, such as setting up the network and the time zone, you select the software packages to install and then let the installer complete the remaining installation chores.

## Checking Your PC's Hardware

When you are thinking about Linux-compatible hardware, here are some of the components in your PC that you need to consider before you start Fedora Core installation:

- A 400 MHz Pentium II or better is. The processor speed, expressed in MHz (megahertz) or GHz (gigahertz), is not that important as long as it is over 400 MHz, the faster the better. Fedora Core can run on other Intel-compatible processors as AMD, Cyrix, and VIA processors.

- RAM is the amount of your system has. With processing speed, the more RAM, the better. You need 256MB to install Fedora Core and comfortably run a GUI desktop.

- DVD/CD-ROM: You must have a DVD/CD-ROM drive and the PC must be able to boot from that. The exact model doesn't matter. What matters is how the DVD/CD-ROM drive connects to the PC. Most new PCs have DVD/CD-ROM drives that connect to the hard disk controller (called IDE for integrated drive or ATA for Attachment), which most likely connects to the USB port. If you add an extra DVD/CD drive, it any IDE/ATA or USB DVD/CD-ROM works in Fedora Core.

- Hard drives: Any IDE disk works in Fedora Core. Another type of hard disk controller is SCSI (Small Computer Interface), which Fedora Core also supports. To comfortably install and work with Fedora Core, you need about 5GB of disk space.

- Keyboard: All keyboards work with Fedora Core and X Window System.

- Mouse: The installation program can detect the mouse. All types of mouse (such as PS/2 or USB) work with Fedora Core and X Window System.

- Video card: Fedora Core works in text mode, but de known as display adapters) if you want the GUI, you need a video card that works with the X Window System. The installer can detect a supported video card and configure X Window System correctly.

- Monitor: The kind of monitor is not particularly critical that the video card must be capable of displaying the screen resolutions that the video resolution is expressed in terms of the number of elements (pixels), horizontally and vertically (for, 1024 x 768). The installer can detect most modern monitors. If it does not, you can select a generic monitor type with a specific resolution such as 1024 x 768. You can also specify the monitor by its name and model (which you can find on the back of the monitor).

- Network card: Not all PCs have network cards, the installer can probably detect and use it. If you have problems, try to find the model and model (such as Linsys LNE00TX Fast Ethernet Adapter) so that you can search for information whether Linux supports that card or not.

- SCSI controller: Some high-performance PCs have SCSI controllers that connect drives and other peripherals to a PC. If your PC happens to have a SCSI controller, you might want to find out the make and model of the controller.

- Sound card: If you have a sound card and you have to sound in Fedora Core, you have to make sure it's compatible. You can configure the sound card after successfully installing Fedora Core.

- Modem: If you plan to dial out to the Internet, you need a modem that Linux supports. For software-based modems, called soft modems or winmods, you may have to download a driver from the manufacturer (it may or not be freely available).

In addition to this hardware, you need to find out the make and model of any printer you use in Fedora Core.

## Setting Aside Space for Fedora Core

In a typical Windows PC, Windows is sitting on a big partition, taking over the whole disk. You want to shrink partition and create room for Linux. During Linux installation, the installation program uses free space for the Linux partitions.

The challenge is to resize the current partition without destroying anything on the hard disk. I cover tools that help you resize the partition, but first you have to make sure that all used areas of the disk are contiguous, or as tightly packed as possible. This is where defragmenting comes in.

## Defragmenting your hard disk

"Defrag your disk" is the magic chant of many help desk. It's the help desk's prescription for all PC ailments. Well, for once they're right —
