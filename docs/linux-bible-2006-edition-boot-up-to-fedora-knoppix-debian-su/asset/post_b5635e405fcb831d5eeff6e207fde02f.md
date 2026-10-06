
using the Gentoo CD to install Gentoo on your computer. The procedure described in that chapter has you building much of the Gentoo operating system from scratch, specifically for your computer hardware, and downloading needed packages from the Internet.

## Damn Small Linux

Damn Small Linux is set to boot directly from the CD that accompanies this book. We have also included an ISO image of Damn Small Linux on the same CD that can fit on a mini-CD (less than 50MB). This distribution illustrates how a useful desktop Linux, which includes full network connectivity and some useful productivity applications, can fit in a very small space.

Information on burning the Damn Small Linux distribution to CD appears later in this appendix. See Chapter 19 for information on using Damn Small Linux.

## Inside Rescue Toolkit

Inside Rescue Toolkit (INSERT is a small, bootable Linux distribution that contains a variety of useful tools for checking, repairing, and recovering networks. INSERT is small enough to fit on a bootable business card CD or mini-CD. While many of its tools are text-based, INSERT includes a simple graphical interface (using X and Fluxbox window manager) and a few graphical tools.

An ISO image of INSERT is on the CD that comes with this book. Information on burning INSERT to CD appears later in this appendix. Refer to Chapter 19 for descriptions of what's inside INSERT.

## System Rescue CD

Like INSERT, System Rescue CD is a bootable Linux that includes a variety of tools for checking and fixing your installed computer systems. It includes tools for managing and fixing file systems, checking for viruses, monitoring the network, and checking whether a machine has been hacked.

Find the System Rescue CD image on the CD that comes with this book. Descriptions later in this appendix provide information about burning CDs from the images with this book. Refer to Chapter 19 for further information about.

## Coyote Linux

Although not considered a major Linux distribution, Coyote Linux is an excellent illustration of a useful Linux distribution that fits on a floppy disk (1.4MB). You can copy the tar file of Coyote Linux on the DVD to a Linux system, configure Linux to suit your needs, and copy the resulting boot image to floppy disk. See Chapter 18 for information on how to configure and use Coyote Linux as firewall.

## Slax

The SlackKill bootable CD image is included on the CD that comes with this book. This bootable image contains a bunch of tools that let you test Windows applications to see if they can run in Linux. SlackKill is described in Chapter 19.

## Linux Distributions Not on the DVD or CD

Not all of the Linux distributions featured in this book are included on the DVD. Some of them did not encourage redistribution of the products, while others were simply too large to include in their entirety and were not available on a single install CD. The following Linux distributions described in the book are not on the DVD. The link after each distribution's name identifies the Internet site where you can find out or otherwise obtain it:

- Yellow Dog Linux (www.yellowdog.org)
- Linspire Linux (www.linspire.com)
- Mandriva (www.mandriva.com/)
- Red Hat Enterprise Linux (www.redhat.com/rhel/)
- DistroWatch (www.distrowatch.com)

Some of these distributions have downloadable versions available on the Internet. I recommend that you try a Linux distribution such as DistroWatch to see if there is a free version of any of these.

## Creating Linux CDs

You can use several tools to create bootable CDs for either installing or just running Linux from CD images on the DVD or CD. Before you begin, you need to have:

- **DVD or CD drive:** You need a drive from which to copy the ISO image of the CD you want from the DVD or CD that come with this book, depending on which medium. If you don't have a DVD drive, download and verify Linux installation CD images yourself as described in Chapter 7. Then those images to CD as explained later in this appendix.
- **Linux Bible 2006 Edition DVD or CD:** The DVD contains several CD images that you can burn to CD and use with Linux. The CD contains several live CD images and install images you can burn to CD.
- **Blank CDs:** You need blank CDs to burn.
- **CD burner:** You can use a different drive from DVD/CD to burn CDs. Or you can copy a CD to hard disk, remove the DVD/CD, and burn the new CD in the same drive. Unless you have two DVD/CD drives, you must copy the CD image to your hard disk before you can burn it (If you have two drives, simply skip the steps for copying the CD image to hard disk).

Here is how to create bootable Linux CDs from a running Linux system (such as Fedora Core):

1. With a Linux desktop system running, insert the disk into the Linux Bible 2006 Edition disk that contains the ISO you want to burn.
2. If an icon appears on the desktop, open it (double-click). If an icon doesn't appear, mount the disk by manually typing the following as root user: `mount /dev/cdrom` or `/dev/hdc`, depending on the location of your DVD CD drive. Then browse to where that image is located from your desktop window manager. It's probably mounted to `/mnt/cdrom` or something like `/media/recorder/`.
3. Open the directory and select the Linux ISO image you want to burn to CD. Your choices are:
   - dams-1.5.iso: Contains the complete Damn Small Linux distribution. You can burn to a regular CD, mini-CD, or bootable card-size CD.
   - slax-killbill-5.0.6.iso: Contains the SlackBill image that can be used to test Windows applications in Linux.
   - Gentoo-install-x86-minimal-2005.1.iso: Contains the network install CD image for starting a Gentoo installation. It requires 633MB of space.
   - INSERT-1.3.5_en.iso: Contains the Inside Rescue Tools CD image. This is a bootable Linux CD image that requires only about 50MB of disk space. It can be burned to a regular CD, mini-CD, or bootable business card-size CD.
   - ubuntu-5.10-install-i386.iso: Contains the CD image to install a nicely stocked Ubuntu desktop system.
   - systemrescuecd-x86-0.2.15.iso: Contains the System Rescue CD image. This bootable Linux CD can be used to help recover a damaged system or network.
   - slackware-10.1-install-d2.iso: Represents the two Slack CDs contained on the DVD (replace with 1 or 2). The images can be used to install Slackware with a basic X desktop, server packages, and programming tools.
   - SUSE-10.0-CD-i386-GM-?.iso: Represents the five-CD SUSE Linux 10.0 (replace the ? with a number from 1 to 5). You can use this CD to install a workable desktop SUSE and server Linux system with KDE desktop and a set of desktop applications.

## Appendix A Media
