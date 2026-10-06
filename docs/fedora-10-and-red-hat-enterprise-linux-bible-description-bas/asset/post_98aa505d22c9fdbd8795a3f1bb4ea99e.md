
## Chapter 1: An Overview of Fedora and Red Hat Enterprise Linux 19

system that has replaced the Red Hat-developed Package Updater (pup) and Package Manager (pirit) applications.

With PackageKit, the icon on the top panel alerts you when software updates are available. Or you can use the PackageKit Manager for GNOME to search for install additional packages. PackageKit is described in Chapter 5.

## Firefox 3 Web browser

This new release of Firefox Web browser offers improvements in security, ease-of-use, personalization and performance. There is one-click to a site's security information (via a favicon in location bar) when a site uses Extended Validation (EV) SSL certificates. With EV SSL certificates, certificate authorities validate that you are visiting the one it claims to be. Password information bars reveals the previous password.

For personalization, bookmarks have been improved by adding tags to them so they can be sorted by topic. You can use smart bookmarks to immediately access bookmarks that were recently tagged or created. In the location bar, auto-completion is improved to display frequent and recently visited locations as you type a URL.

## Preupgrade

A preupgrade feature lets you install and run a preupgrade application that prepares a Fedora 9 system to be upgraded to Fedora 10. This feature lets do much of the time-consuming download and dependency checking that takes place during upgrades while you are still using the existing system. Preupgrade is described in Chapter 2. While you can run preupgrade with Fedora 8.1, I recommend upgrading fully to Fedora 9 before trying to use preupgrade.

## Ext4 file systems

Support was added so that Fedora can handle the ext4 file system type. The ext4 file system was designed to provide better performance and scalability than ext3 systems. While there should be no differences in how people use ext4 file systems, a set of tools for creating, checking and maintaining ext4 file systems is included with Fedora 10.

## Encrypted file systems

Using the cryptsetup and LUKS features in Fedora 10, you can encrypt file systems other than your root (/) /boot partitions. Encrypted file systems can be particularly important to secure your data on laptop systems.

## Identity management with freeIPA

The freeIPA framework for managing identity, policy, and audit features across an enterprise has been added to Fedora Linux. The long-term goal of freeIPA is to provide an open source mechanism for centrally maintaining this critical security and monitoring features. Chapter 14 contains a description of freeIPA.

## Part I: Getting Started in Fedora and RHEL

## NetworkManager

To simplify the process of setting up connections to wired and wireless networks, NetworkManager is providing continuous improvements. In Fedora 10, it is the default method of connecting to and managing wired and wireless interfaces.

## Getting Custom spins

Fedora used to be released as a set of CDs or a DVD containing all the Fedora packages could be installed from those media. The result of new tools first added in Fedora 7 for creating custom software repositories (Pungi) and custom live CDs (livecd-creator) have continued to improve in the form of a growing set of custom spins.

A custom spin is a CD, DVD, or USB flash drive image that can run as a live CD andor Fedora install. Official spins include:

- **Fedora DVD**: Contains at least 4GB with a cross-section of desktop, server, and software development packages that you can install to hard disk. The contents of this disk are similar to what you use in Fedora Core.
- **Fedora CD Set**: This six-CD set contains everything from the Fedora install DVD. This is for those who don't have a DVD drive on their computer.
- **Fedora Desktop Live CD (GNOME)**: From this single, 700MB DVD you can run Gnome desktop live/install CD of Fedora 10. An install icon on the desktop then you install that desktop system to your hard disk.
- **Fedora Desktop Live CD (KDE)**: Fedora is showing KDE by offering a DE desktop live/install CD of Fedora 10. With the GNOME desktop, you can select t install icon to install the KDE desktop system to your hard disk. This CD is included with this book.
- **Everything DVD**: An “Everything” 2-DVD set contains the entire Fedora 10 repository (11GB) is expected to be produced shortly after Fedora 10 is released. This set is for people who want every installable software package with Fedora 10. The DVD that comes with this set contains most of the contents of the two Everything DVDs, respon upon a high-capacity DVD-9.

The KDE desktop and Nearly-Everything DVD included with this book are for standard 32-bit PCs (i386). If you need media to install Fedora on PowerPC (PPC) or 64-bit PC (X86, 64) computer architectures, you can download ISO images for those media either using Bittorrent (http://spin.fedoraproject.org) or an official Fedora public mir site (http://mirrors.fedoraproject.org). Refer to Chapter 2 for information of using and installing Fedora from these different media.

Unofficial custom spins are also available from the Custom Spins page So far there are already Fedora (http://fedoraproject.org/wiki/CustomSpins) Live Developer, Games, Xfce desktop, and Electronic Lab. (The term spin means a

## Chapter 1: An Overview of Fedora and Red Hat Enterprise Linux 21

Compilation of software from the Fedora software repository, combined into the form of one more bootable images (typically to fit on CD or DVD), that lets you either run or install.

## Creating your own spins

The same tools that the Project uses to build packages and create live CDs are distributed with Fedora. That means that anyone can use those tools to create their own installation CDs, and then turn those package sets into their own repositories. Using those repositories, you could install or run.

Pungi (hosted.fedaproject.org/projects/pungi) is the project created for Fedora to build the system itself. The pungi package contains the pungi command and related configuration files. You can use the pungi command to fashion your own installation trees that result in installable images.

The Fedora Live CD project (http://fedaproject.org/wiki/FedoraLiveCD) has produced tools for building your own live CDs from Fedora software repositories. The primary tool for creating these live CDs is lived-creator. Refer to the Live CD HOWTO (http://fedaproject.org/wiki/FedoraLiveCD/LiveCDHowTo) for information using lived-creator.

A recent addition to lived-creator is that you can kickstart files (described in Chapter 2) to direct the creation of live CDs. This means the same format you use to automate installs with anaconda be used to save the package list and other settings you use to create your live CDs.

## Firewall Configuration

The Firewall Configuration window was enhanced to provide several features that previously needed to be added manually to iptables. In particular, you can select ports to do port forwarding (for example, if you wanted to have a Web server on a private address behind your firewall). You can also indicate which ICMP types you support, such as the commonly used echo `ping` and echo `pong`.

## The Culture of Free Software

I would be to say nothing about the culture of free software development from Linux has thrived and will continue to thrive. The copyright for Fedora and Red Hat Enterprise Linux systems is covered under the GNU public license. That license, which most free software falls under, provides the following:

- **Author rights**: The original author retains the rights to his or her software.
- **Free distribution**: People can use the GNU software in their own software, changing and redistributing it as they please. They do, however, to include the source code with their distribution (or make it easily available).
- **Copyright maintained**: Even if you were to repack and resell the software, the original GNU agreement must be maintained with the software. This means that all
