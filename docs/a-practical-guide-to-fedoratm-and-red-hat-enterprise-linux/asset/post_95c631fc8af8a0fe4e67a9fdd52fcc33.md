
- RAID level 6 (disk stripping with double parity)—Improves upon level 5 RAID by protecting data when two disks fail at once. Level 6 RAID is inefficient with a small number of drives.
- RAID level 10 (mirroring and stripping)—A combination of RAID 1 and RAID 0 (also called RAID 1+0). RAID 10 uses mirroring to improve fault tolerance and stripping to improve performance. Multiple RAID 1 arrays (mirroring) are overlaid with a RAID 0 array (stripping). The storage capacity of the RAID device is equal to one-half that of the member partitions or disks. You must use at least four partitions or disks.

For more information see raid.wiki.kernel.org/index.php/Linux_Raid.

## LVM: Logical Volume Manager

The Logical Volume Manager (LVM2, which this book refers to as LVM) allows you to change the size of logical volumes (LVs, the LVM equivalent of partitions) on the fly. With LVM, if you make a mistake in setting up LVs or if your needs change, you can make LVs either smaller or larger without affecting user data. You must choose to use LVM at the time you install the system or add a hard disk; you cannot retroactively apply it to a disk full of data. LVM supports IDE and SCSI drives as well as multiple devices such as those found in RAID arrays.

LVM groups disk components (partitions, hard disks, or storage device arrays), called physical volumes (PVs), into a storage pool, or virtual disk, called a volume group (VG). See Figure 2-1. You allocate a portion of a VG to create a logical volume (LV).

An LV is similar in function to a traditional disk partition in that you can create a filesystem on an LV. It is much easier, however, to change and move LVs than partitions: When you run out of space on a filesystem on an LV, you can grow (expand) the LV and its filesystem into empty or new disk space, or you can move the filesystem to a larger LV. For example, you can add a hard disk to a system and incorporate it into an LV to expand the capacity of that LV. LVM's disk space manipulation is transparent to users; service is not interrupted.

LVM also eases the burden of storage migration. When you outgrow the PVs or need to upgrade them, LVM can move data to new PVs. To read more about LVM, refer to the resources listed on page 28.

![](img/243613168ac865b539f12460d966088e_101_0.png)

Figure 2-1 LVM: Logical Volume Manager

## The Installation Process

The following steps outline the process of installing Fedora/RHEL from an Install Image. Installation from other installation images follows similar steps. See Chapter 3 for specifics.

1. Make sure the BIOS is set to boot from a DVD or USB flash drive (page 31). Insert the installation medium holding an Install Image in the system, and reset the computer. The computer boots and displays the Install Image Boot menu (Figure 3-4, page 61).
2. You can make a selection from the Install Image Boot menu, press the TAB key to display the boot command line (which you can modify), and begin installing Fedora/RHEL when you are ready. One of the menu items checks the installation medium. If you do nothing, Anaconda starts installing the system after 60 seconds.
3. As part of the process of bringing up a live session or installing Fedora/RHEL, Anaconda creates RAM disks (page 1269) that it uses in place of the hard disk used for a normal boot operation. Anaconda copies tools required for the installation or to bring up a system from a Live or Install Image to the RAM disks. The use of RAM disks allows the installation process to run through the specification and design phases without writing to the hard disk and enables you to opt out of the installation at any point before the last step of the installation. If you opt out before this point, the system is left in its original state. The RAM disks also allow a live session to leave the hard disk untouched.
4. You give Anaconda information about how you want to configure the system.
5. When Anaconda is finished collecting information, it writes the operating system files to the hard disk.
6. When you reboot the system, gnome-initial-setup asks questions that are required to set up the first user (page 68).
7. The system is ready for you to log in and use.

### Downloading an Installation Image File and Writing to/Burning the Installation Medium

There are several ways to obtain or create installation media (a CD, DVD, or USB flash drive). Fedora/RHEL makes available releases of Linux as CD/DVD ISO image files (named after the ISO 9660 standard that defines the CD/DVD filesystem). Even though they are referred to as CD/DVD ISO images, you can write these files to a USB flash drive and then boot from that drive.

This section describes how to download one of these installation images and burn a DVD or write to a USB drive. You can also purchase an installation DVD from a Web site. If you cannot obtain Fedora/RHEL by any other means, you can point a browser to fedoraproject.org/wiki/FreeMedia to display a Web page with links that enable you to request a free Fedora DVD.

#### The Easy Way to Download an Installation Image File

This section explains the easiest way to download an installation (ISO) image file. This technique works in most situations; it is straightforward but limited. For example, it does not allow you to use BitTorrent to download the file.

To begin, point a browser to fedoraproject.org and click **Download Now!**. The download should start shortly. If the browser gives you a choice of what to do with the file, save it to the hard disk. The browser saves the installation (ISO) image file to the hard disk. Continue reading at “Verifying an Installation (ISO) Image File” on page 49.

> **You can find installation (ISO) image files for all supported architectures here**
>
> tip: If you cannot find an installation image file that supports the type of hardware you want to install Fedora on, visit mirrors.fedoraproject.org/publist. For RHEL visit access.redhat.com and select Downloads.

#### Other Ways to Download an ISO Image File

This section explains how to download an installation (DVD/ISO) image file or a release that is not downloaded automatically, and how to download a torrent that enables you to use BitTorrent to download an installation (ISO) image file. See “Download Fedora/RHEL” on page 29 for other locations you can download Fedora/RHEL from.

- **Browser**: When you use a Web browser to download a file, the browser contacts a Web (HTTP) or FTP server and downloads the file from that server. If too many people download files from a server at the same time, the downloads become slower.
- **BitTorrent**: BitTorrent efficiently distributes large amounts of static data, such as installation (ISO) image files. Unlike using a browser to download a file from a single server, BitTorrent

![](img/243613168ac865b539f12460d966088e_103_0.png)

**Figure 2-2** The mirrors.fedoraproject.org Web page

distributes the functions of a server over its clients. As each client downloads a file, it becomes a server for the parts of the file it has downloaded. To use BitTorrent, you must download a small file called a *torrent* (or have a Web browser do it for you). This file, which holds information that allows clients to communicate with one another, has a filename extension of `.torrent`. As more people use a torrent to download a file at the same time, the downloads become faster. Downloading an installation (ISO) image file using BitTorrent is covered later in this section.

Many sites mirror (hold copies of) the Fedora installation (ISO) image files and BitTorrent torrent files. Some mirrors use HTTP, while others use FTP; you can use a browser to download files from either type of site. FTP and HTTP sites appear slightly different.

Locate a mirror site by pointing a browser at `mirrors.fedoraproject.org`. Below the heading information, the page displays Public Active Mirrors. Narrow your choices by clicking a selection in the Mirror list filter at the upper-right corner of the page (Figure 2-2). For example, click **19** to list sites from which you can download Fedora 19 or click **i386** in the row that starts with **19** to list sites from which you can download the i386 version of Fedora 19.

The list on the newly displayed Web page is in country code order. For example, FR is France and US is the United States. To conserve network bandwidth, scroll to and download from a mirror site close to you. Look at the Content, Bandwidth, and Comments columns. Pick the row of an appropriate site and click the protocol you want to use in the Content column. From a browser there is little difference between the FTP and HTTP protocols, although accessing a site using FTP might be a bit faster.
