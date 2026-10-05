# PLANNING THE INSTALLATION 27

RAID: help.ubuntu.com/community/Installation/SoftwareRAID,
en.wikipedia.org/wiki/RAID, and raid.kernel.org/index.php/Linux_Read
VM Resource Page (includes many links): sourceage.com/lvm2
LVM HOWTO: www.tld.org/HOWTO/LVM-HOWTO
BitTorrent: help.ubuntu.com/community/BitTorrent and azure.sources.net
ARM: wiki.ubuntu.com/ARM/LinuxReleaseNotes
X release information: wki.org

Default Ubuntu E easiest download: www.ubuntu.com/getubuntu
Released versions: releases.ubuntu.com
Minimal CD: help.ubuntu.com/community/Installation/MinimalCD
Older versions: old-releases.ubuntu.com
Development images and unsupported releases: cdiimage.ubuntu.com
Mac (PowerPC): wiki.ubuntu.com/PowerCDDownloads
BitTorrent torrent files: torrent.ubuntu.com/releases

# PLANNING THE INSTALLATION

The major decision when planning an installation is determining how to divide the
hard disk into partitions or, in the case of a dual-boot system, where to put the
Linux partitions. Once you have installed Ubuntu, you can decide which software
packages you want to add to the base system (or whether you want to remove
some). In addition to these topics, this section discusses hardware requirements for
Ubuntu Linux and fresh upgrades.

# CONSIDERATIONS

GUI On most systems, except for servers, you probably want to install a graphical user
interface (desktop). Ubuntu installs GNOME by default. See page 75 for informa-
out installing KDE.

As you install more software packages on a system, the number of updates and the
interactions between the packages increase. Server packages that listen for network
connections make the system more vulnerable by increasing the number of ways the
system can be attacked. Including additional services can also slow the system.
If you want to learn on or a development system, additional packages and
ervices may be useful. For a more secure production system, it is best to install and
maintain the minimum number of packages required and to enable only needed-
vices. See page 432 for information on the Upstart it daemon, which starts and
stops services.

The Minimal CD is small and provides a quick installation (page 32).

# REQUIREMENTS

This chapter and Chapter 3 cover installing Ubuntu on 32-bit Intel and compatible
processor architectures such as AMD and as 64-bit architectures such as
AMD64 processors and Intel processors with Intel EM64T technology. Within these
processor architectures, Ubuntu Linux runs on much of the available hardware. You