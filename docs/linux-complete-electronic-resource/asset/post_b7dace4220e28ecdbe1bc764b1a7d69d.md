
## CHAPTER 4

### INSTALLING LINUX

This chapter describes how to install Linux software. It is the first document a new user should read in order to get started using Linux. It covers hardware and software requirements, preliminary steps to take before installation, and specifics on hard drive repartitioning and booting a Linux system.

This chapter is reprinted from the Linux Installation HOWTO, version 4.15 of November 20, 1998, by Eric S. Raymond.

### INTRODUCTION

This document assumes that you have heard of and know about Linux and now want to get it running. The document focuses on the Intel base version, which is the most popular, but much of the advice applies on Power PCs, Sparcs, and Alphas, as well.

### Other Sources of Information

If you are new to Linux, there are several sources of basic information about the system. The best place to find these is at the Linux Documentation Project home page at `http://MetaLab.unc.edu/LDP/linux.html`. You can find the latest version of this chapter here, as `http://MetaLab.unc.edu/LDP/HOWTO/Installation-HOWTO.html`.

You should probably start by browsing the resources under General Linux Information: the Linux INFO-SHEET (`http://MetaLab.unc.edu/LDP/HOWTO/INFO-SHEET.html`) and the Linux META-FAQ (`http://MetaLab.unc.edu/LDP/HOWTO/LINUX-FAQ.html`). The Linux Frequently Asked Questions document contains many common questions (and answers!) about Linux–it is a must read for new users.

You can find help for common problems on the USENET newsgroups comp.os.linux.help and comp.os.linux.announce.

The Linux Documentation Project is writing a set of manuals and books about Linux, all of which are freely distributable on the Net and available from the LDP home page.

The book *Linux Installation and Getting Started* is a complete guide to getting and installing Linux, as well as how to use the system once you've installed it. The book contains a complete tutorial to using and running the system and much more information than is contained here. You can browse it, or download a copy, from the LDP home page (`http://MetaLab.unc.edu/LDP/`).

Finally, there is a rather technical Guide to x86 Bootstrapping (`http://www.paranoia.com/~vax/boot.html`). This document is NetBSD, rather than Linux, oriented but contains useful material on disk configuration and boot managers for multi-OS setups.

### New Versions of This Document

New versions of the Linux Installation HOWTO will be periodically posted to comp.os.linux.help, comp.os.linux.announce, and news.answers. They will also be uploaded to various Linux WWW and FTP sites, including the LDP home page.

You can also view the latest version of this on the World Wide Web at http://MetaLab.unc.edu/LDP/HOWTO/Installation-HOWTO.html.

### Feedback and Corrections

If you have questions or comments about this document, please feel free to mail Eric S. Raymond at esr@thyrus.com. I welcome any suggestions or criticisms. If you find a mistake with this document, please let me know so I can correct it in the next version. Thanks.

Please do not mail me questions about how to solve hardware problems encountered during installation. Consult Linux Installation and Getting Started, buy your vendor, or consult the Linux newsgroup comp.os.linux.setup. This HOWTO is intended to be a rapid, painless guide to normal installation–a separate HOWTO on hardware problems and diagnosis is in preparation.

## THE EASIEST OPTION: BUY, DON’T BUILD

Linux has matured enough that there are now system integrators who will assemble a workstation for you, install and configure Linux, and do an intensive burn-in to test it before it’s shipped to you. If you have more money than time, or you have stringent reliability or performance requirements, these integrators provide a valuable service by making sure you won’t get hardware that’s flaky or dies two days out of the box.

There are several firms of this kind. The only such outfit I know about personally is VA Research (http://www.varesearch.com).

These good people build high-end, high-quality Linux workstations with a nifty Tux-the-penguin logo on the front. They have intimate ties to the Linux community (the Debian project, http://www.debian.org, lives on a machine in their back room, Linus owns one of their boxes, and they even throv resources at your humble HOWTO maintainer occassionally).

For those of us without a champagne budget, the rest of this HOWTO is about how to install Linux ourselves.

![](img/a3584dae761d2e3abed8bf40d7637389_108_0.png)

## BEFORE YOU BEGIN

Before you can install Linux, you'll need to be sure your machine is Linux-capable, and choose a Linux to install. The Linux Pre-installation checklist (http://members.tripod.com/~alogog/lnxchk.htm) may help you organize configuration data before you begin.

### Hardware Requirements

What kind of system is needed to run Linux? This is a good question; the actual hardware requirements for the system change periodically. The Linux Hardware-HOWTO, http://Metalab.unc.edu/LDP/HOWTO/Hardware-HOWTO.html, gives a (more or less) complete listing of hardware supported by Linux. The Linux INFO-SHEET, http://Metalab.unc.edu/LDP/HOWTO/INFO-SHEET.html, provides another list.

For the Intel versions of Linux, any 80386, 80486, Pentium or Pentium II processor will do. Non-Intel clones of the 80386 and up will generally work. You do not need a math coprocessor, although it is nice to have one.

The ISA, EISA, VESA Local Bus, and PCI bus architectures are supported. The MCA bus architecture (found on IBM PS/2 machines) is supported in the newest development (2.1.x) kernels but may not be ready for prime time yet.

You need at least 4 megabytes of memory in your machine. Technically, Linux will run with only 2 megs, but most installations and software require 4. The more memory you have, the happier you'll be. I suggest 8 or 16 megabytes if you're planning to use X-Windows.

Of course, you'll need a hard drive and an AT-standard drive controller. All MFM, RLL, and IDE drives and controllers should work. Many SCSI drives and adaptors are supported as well; the Linux SCSI-HOWTO contains more information on SCSI. If you are assembling a system from scratch to run Linux, the small additional cost of SCSI is well worth it for the extra performance and reliability it brings.

You will need a 3.5 floppy drive. While 5.25 floppies are supported under Linux, they are so rarely used that you should not count on disk images necessarily fitting on them. (A stripped-down Linux can actually run on a single floppy, but that's only useful for installation and certain troubleshooting tasks.)

You also need an MDA, Hercules, CGA, EGA, VGA, or Super VGA video card and monitor. In general, if your video card and monitor work under MS-DOS, it should work under Linux. However, if you wish to run X-Windows, there are other restrictions on the supported video hardware. The Linux XFree86-HOWTO, http://MetaLab.unc.edu/LDP/HOWTO/XFree86-HOWTO.html, contains more information about running X and its requirements.

You’ll want a CD-ROM drive. If it’s ATAPI, SCSI, or true IDE you should have no problem making it work (but watch for cheap drives advertising “IDE” interfaces that aren’t true IDE). If your CD-ROM uses a proprietary interface card, it’s possible the installation kernel you’re going to boot from a floppy won’t be able to see it—and an inaccessible CD-ROM is an installation showstopper. Also, CD-ROMs that attach to your parallel port won’t work at all. If you’re in doubt, consult the Linux CD-ROM HOWTO, http://MetaLab.unc.edu/LDP/HOWTO/CDROM-HOWTO.html, for a list and details of supported hardware.

So-called Plug’n’Play jumperless cards can be a problem. Support for these is under active development but not there yet in the 2.0.25 kernel. Fortunately this is only likely to be a problem with sound or Ethernet cards.

If you’re running a box that uses one of the Motorola 68k processors (including pre-PowerPC Macintosh, Amiga, Atari, or VMEbus machines), see the Linux m68k FAQ at http://www.clark.net/pub/1awrencec/linux/faq/Faq.html for information on minimum requirements and the state of the port. The FAQ now says m68k Linux is as stable and usable as the Intel versions.

### Space Requirements and Coexistence

You’ll need free space for Linux on your hard drive. The amount of space needed depends on how much software you plan to install. Most installations require somewhere in the ballpark of 200 to 500 megs. This includes space for the software, swap space (used as virtual RAM on your machine), free space for users, and so on.

It’s conceivable that you could run a minimal Linux system in 80 megs or less (this used to be common when Linux distributions were smaller), and it’s conceivable that you could use well over 500 megs or more for all of your Linux software. The amount varies greatly depending on the amount of software you install and how much space you require. I’ll discuss this in more detail later.

Part I
