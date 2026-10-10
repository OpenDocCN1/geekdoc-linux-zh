FOSS

# Disk tools

Keep your hard drive in top-top shape, recover lost data or delete it safely.

# FOG

The constant barrage of repetitive tasks such as running checks, troubleshooting errors, swapping out dead hard disks, doing fresh installations over and over again can sap the energy out of any system admin, irrespective of the size of their network. Using *FOG* you can image and clone machines from the comforts of the admin HQ.

*FOG* is a complex piece of software and offers plenty of options, with various fields to describe the host images. It can also arrange them into groups for easier management. There are also several options to schedule the imaging process. *FOG* can also be used to debug imaged computers, remotely wipe hosts and more. The server also handles regular admin tasks such as installing software and can even manage printers on the network. The *FOG* server is scalable and can manage large networks spread over multiple locations in the same building or on the other side of the planet. One of the most useful features of the *FOG* server, especially for admins of larger networks, is the multicast ability. Using this feature you can deploy multiple machines in one go. To supplement it on such large networks, you can have multiple *FOG* installations configured as storage servers that help take the load of the main *FOG* server when imaging computers. https://fogproject.org

# DUPLICATI

An easy-to-use backup application, *Duplicati* enables you to fine-tune the list of locations you want to preserve by either defining filters or toggling one of the predefined options to exclude certain types of files. You can manage the tool via a browser-based interface. The program breaks down critical tasks into wizards and also exposes just the right number of features for the job in hand, while advanced options are just a pull-down menu away. Files are encrypted with AES-256 and you can also use GPG before sending the backups to their destination. *Duplicati* also compresses all data before it's encrypted. It supports Zip and 7Z compression, and can skip compression of already compressed files such as MP3 and JPG. www.duplicati.com

# PHOTOREC

*Photorec* is a nifty little command-line based tool that can restore accidentally deleted files. When you delete a file, the file system just marks it as deleted, and makes the space the file occupies available to other files. *Photorec* works by recovering such files that are missing regular metadata such as a filename. Despite its name, the CLI utility can sniff files in various formats. www.cgsecurity.org/wiki/PhotoRec

![](bbox=[0.37, 0.63, 0.58, 0.73])

Photorec is part of almost every recovery distro and ships along with TestDisk.

# GPARTED

One of the best graphical utilities to manage partitions, you can use *GParted* to create, delete, resize, move and copy partitions while preserving the data they house. The program works with all kinds of hard disks, SSDs, and RAID devices and supports all the filesystem in vogue. https://gparted.org

# SECURE-DELETE

The secure-delete package contains various utilities to securely delete files and wipe all traces of data in the free space on the disk. There's *shred* that make it impossible to remove any deleted files, *sfill* to wipe all data from the free space on the disk, and *sswap* to wipe data from the swap partition. https://smr.sourceforge.net

# CDEMU

The *CDEmu* tool enables you to mount disc images in various formats including ISO, bin and img. The *CL tool* also has several graphical front-ends for Gnome and KDE desktops. https://cdemo.sourceforge.io

# DUC

If you're looking to free up some disk space, use *Duc* in the first instance to gain a better idea of the files occupying the space. The tool does a better job in inspecting your hard disk than the file manager. https://duc.zew.nl

# DDRESUE

Try image a failing drive with *ddrescue* before attempting recovery. The utility doesn't write zeros to bad sectors, and tries to fill in the gaps without wiping out the data already rescued. www.gnu.org/software/ddrescue

# PYDF

A replacement for *df, pydf* is a Python script that highlights the different types of filesystems. It has an large set of configurable parameters and various options to control its output. https://pypi.org/project/pydf

# SMARTCTL

Bundled as part of the smartmontools package, the *smartctl* utility controls and monitors the SMART system built into hard disks. Use the tool periodically to run self-assessment health checks on the disks. www.smartmontools.org

170