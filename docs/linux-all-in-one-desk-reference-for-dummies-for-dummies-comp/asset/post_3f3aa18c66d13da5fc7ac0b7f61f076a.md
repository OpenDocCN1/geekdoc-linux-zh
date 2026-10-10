
## DVD Installation Instructions

To install a Linux distribution from the companion DVD, follow these steps. (Consult Book I, Chapter 2 for details.)

- 1. Gather information about your PC's hardware, such as graphics card, network card, and SCSI card, before you install Linux.

- 2. Use a partitioning program such as PartitionMagic or the FIPS program to create room on your hard drive for Linux.

Skip this step if you plan to use Linux as the sole operating system on your PC or if you plan to install it on an empty second hard drive.

- 3. Burn CDs for your distribution. (Skip this step if you are installing Fedora Core.)

Consult Book I, Chapter 2 for instructions specific to each distribution.

- 4. Boot your PC with the DVD (for Fedora Core and Knoppix) or the first CD (for Debian, MEPIS, SUSE, Ubuntu, and Xandros).

Knoppix is a Live CD distribution, so this step should get you the Knoppix desktop. For other distributions, this step runs that distribution's installation program. From this point on, respond to the questions and choices as the installation program takes you through the steps. Here are some of the typical installation steps:

- Prepare the hard drive partitions for Linux. If you have created space by reducing the size of an existing Windows partition, this step enables you to create the partitions for Linux.
- Configure the Ethernet network, if any. Typically, you configure the network automatically by using DHCP.
- Specify the local time zone and set the `root` password.
- Install a boot loader program on your hard drive so that you can boot Linux when you power up your PC after shutting it down.
- Select the specific software packages that you want to install, such as the X Window System and the GNOME or KDE graphical desktop.

### What You'll Find on the DVD

This section provides a summary of the software and other goodies you find on the DVD. If you need help with installing the items provided on the DVD, refer back to the installation instructions in the preceding section.

![](img/11709a8f88c8cd03868a929dc94c0e2b_798_0.png)

*Shareware programs* are fully functional, free, trial versions of copyrighted programs. If you like particular programs, register with their authors for a nominal fee and receive licenses, enhanced versions, and technical support.

*Freeware programs* are free, copyrighted games, applications, and utilities. You can copy them to as many PCs as you like — for free — but they offer no tech support.

*Trial, demo, or evaluation versions* of software are usually limited by time or functionality (such as not letting you save a project after you create it).

*GNU software* is governed by its own license, which is included in the folder of the GNU software. There are no restrictions on distribution of GNU software. See the GNU license at the root of the DVD or back of this book for details. As required by the GNU license, this book includes the source code for Fedora Core. As for the source code for Debian, Knoppix, SUSE, and Xandros, here’s how to get the source code from the Internet for each application:

- **Debian**: Go through the list of mirror sites at www.debian.org/mirror/list and click the URL for the site nearest you. After the site loads, go to the pool directory and then look for source code files in one of the three directories — main, contrib, and non-free. The files are further organized into separate directories according to the first letter of the package’s name. For example, the source code for the sendmail package is in the s directory. (See www.debian.org/doc/FAQ/ch-ftarchives.en.html#s-pools for more information about the pool directory.)

- **Knoppix**: Many packages for Knoppix are from the Debian project and their source code is available from the Debian Web site. (See the previous bullet for information on downloading Debian source code.) Download the Knoppix-specific source code from www.knopper.net/download/knoppix.

- **MEPIS**: Most packages in MEPIS are from the Debian project and their source code is available from the Debian Web site. (See the description of Debian for information on downloading Debian source code.) MEPIS-unique components such as MEPIS OS Center are proprietary and their source code is not available.

- **SUSE**: Download the source package for SUSE Linux from the server at http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/inst-source/suse/src/.

- **Ubuntu**: You can find the Ubuntu source code at http://archive.ubuntu.com/ubuntu/ and it’s organized similar to the way Debian source code is organized (see the description of Debian). While running Ubuntu, you can download the source code for a package by typing the following commands: **sudo apt-get build-dep packagename** followed by **sudo apt-get source packagename**, where *packagename* is the name of the package. For example, to download the source code of the **samba** package, you type **sudo apt-get build-dep samba** followed by **sudo apt-get source samba**.

- **Xandros**: Download the source code for the free and open-source components of Xandros by following the instructions at www.xandros.com/support/source_code.html.

If you want the source code sent to you, fill out and send in the coupon that appears in the back of this book.

The DVD includes the Linux distributions in several different formats:

- **Full distribution:** You can boot from the DVD and install a full distribution. With a full distribution, you don't have to do anything special other than boot from the DVD. You can then simply proceed to install the Linux distribution.

- **Ready-to-run Live CD:** You can boot a Live CD by booting your PC from the DVD. After you boot a ready-to-run Live CD, you should get a Linux GUI desktop that you can begin using immediately without having to install anything on the hard drive.

- **ISO images:** You have to burn CDs from the ISO images and then install from the CDs. Although you can download ISO images yourself, the files are quite big --- each ISO image is about 700MB --- and having them on the DVD eliminates the hassles of downloading huge files from the Internet. Some of the ISO images are Live CD images. After you burn a CD from a Live CD ISO, you can boot from the CD and get a Linux system without having to install anything on the hard drive.

Here are the Linux distributions that the DVD includes:

- **Debian:** Provided in the form of a network-install ISO image. Burn the CD and you are ready to install Debian over the network from a server on the Internet (you need Internet access to perform this installation).

- **Fedora Core:** Included as a full distribution. Simply boot from the DVD and you get the option of installing Fedora Core. Use the graphical installer to complete the installation steps.

- **Knoppix:** Included as a ready-to-run Live CD. Boot from the DVD and you get the option to start Knoppix. After it starts, you get the Knoppix desktop without having to install anything on the hard drive.

- **MEPIS:** Provided as a Live CD ISO image that also serves as an installation CD. Burn the CD and boot from it to try MEPIS. You can also proceed to install it from the same CD.

- **SUSE**: Provided as a single Live DVD ISO image file. Burn the ISO file on a DVD and then boot from the DVD to run SUSE Linux directly from the DVD. (Limited space on the DVD precludes us from providing the full SUSE Linux distribution. To download the full SUSE Linux distribution, please visit http://ftp.opensuse.org/pub/opensuse/distribution/SLE-OSS-stable/.)

- **Ubuntu**: Provided as a single installation CD ISO image. Burn the CD and boot from it to begin the installation.

- **Xandros Open Circulation Edition**: Provided as a single CD ISO image. Burn the CD and then install Xandros.

The detailed software list for each Linux distribution varies somewhat, but most of the distributions include the following (typical version numbers shown):

- Linux kernel 2.6.x with driver modules for major PC hardware configurations, including IDE/IDE and SCSI drives, PCMCIA devices, CD drives and DVD drives
- A complete set of installation and configuration tools for setting up devices and services
- A graphical user interface based on the X Window System, with GNOME 2.12 and KDE 3.4 graphical desktops
- Full TCP/IP networking for Internet, LANs, and intranets
- Tools for connecting your PC to your Internet Service Provider (ISP) using PPP, DSL, or dial-up serial communications programs
- A complete suite of Internet applications, including electronic mail (sendmail, mail), news (INN), TELNET, FTP, DNS, and NPS
- Xiaman Evolution or equivalent e-mail and calendar application
- OpenOffice.org 1.9 office suite with word processor, spreadsheet, presentation software, and more
- Apache Web server (to turn your PC into a Web server) and Mozilla Firefox Web browser (to surf the Net)
- Samba 3.0.20 LAN Manager software for Microsoft Windows connectivity
- Several text editors (for example, GNU Emacs 21.3; vim)
- Graphics and image manipulation software, such as The GIMP, Xfig, Gnuplot, Ghostscript, Ghostview, and ImageMagick
- Programming languages (GNU C and C++ 4.0, Perl 5.8.7, Tcl/Tk 8.4.11, Python 2.4.1, Ruby 1.8.2, GNU AWK 3.1.4) and software development tools (GNU Debugger 6.3, CVS 1.12, RCS 5.7, GNU Bison 1.875, flex 2.5.4a, TIFF, and JPEG libraries)
