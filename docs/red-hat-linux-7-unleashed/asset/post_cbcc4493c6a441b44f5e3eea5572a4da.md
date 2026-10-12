
Additional OSS either installed or to be installed on system: 

Desired location for installation of LILO (if used): 

Installed on master boot record (required if you want LILO to be your boot manager): 

Installed on Linux partition (if you want to use a different bootloader, this would be where to install LILO):

## Note

If you are running OS/2, you must create your disk partitions with the OS/2 partitioning software; otherwise, OS/2 might not recognize the disk partitions. Do not create any new partitions during the installation, but do use the Linux `fdisk` to set the proper partition types for your Linux partitions.

After you have answered these questions, the rest of the installation is fairly easy. The entire process is menu-driven, which means you don’t have to remember all the configuration information you have to remember for other Linuxes you might want to install.

## Choosing an Installation Method

There are a number of different ways in which you can install your system. They are all documented further later in the chapter. They are as follows:

- CD-ROM—This method needs a boot floppy, bootable CD, or a PCMCIA boot disk. This is the most common way to install your system.
- Hard Drive—This method requires you to have the Red Hat installation files on your hard drive. To install Red Hat Linux from a hard drive, you need the same startup and supplemental disks used by the FTP install. You must first create a Red Hat directory called `RedHat` at the top level of your directory tree. Everything you install should be placed in that directory. Copy the base subdirectory and then copy the packages you want to install to another subdirectory called `RPMS` (Red Hat Package Manager). Basically, these are your program installation files. You can use available space on an existing DOS partition or a Linux partition that is not required in the install procedure (for example, a partition that would be used for data storage on the installed system). With Red Hat 7 being a 3-CD install, there is going to be the overhead of having enough space free to store these files.
  - If you are using a DOS filesystem, you might not be able to use the full Linux filenames for the RPM (Red Hat Package Manager) packages. The installation process does not care what the filesystem looks like, but it is a good idea to keep track of it so you will know what you are installing.
- **NFS (Network File System) Image**—You can install from an NFS server that has the install files exported. This requires a network or PCMCIA boot disk. You should either have nameservices configured or know the NFS server's IP address and the path to the exported CD-ROM. This method is only advisable if the NFS server is on a local network. It will take a long time to install using this, the FTP, and the HTTP install method. There is the possibility of the connection timing out.
- **FTP (File Transfer Protocol) and HTTP**—Comparable to an NFS image install. This also requires a network or PCMCIA boot disk. You must have a startup disk and a supplemental disk for an FTP install. You need to have a valid nameserver configured or the IP address of the FTP or HTTP server you will be using. You also need the root path of the Red Hat Linux directory on the site.
- **SMB Image**—Again comparable to NFS and FTP installs. This requires a network or PCMCIA boot disk. Select this option if you want to install over a network from a disk shared by a Windows system (or a Linux system running the Samba SMB connectivity suite). This is similar to installing from a hard drive except that in this case, the hard drive is on another system.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_64_0.png)

The rest of the installation procedures presented here are for a CD-ROM installation. As you can tell from the preceding descriptions, using other methods is not much different. As a matter of fact, the installation is the same; the difference is just a matter of the installation's origin. For example, if you are installing from a shared volume on a Windows 95/98/ME or Windows NT/2000 server, you have to supply the name of the server, the name of the shared volume, and the account name and password for the volume.

Because you have purchased this book, it is highly likely that you will be installing your system with the CDs provided in the back of this book. This is the simplest and generally the quickest method of installation.

## GUI Versus Text-Based Installation

Red Hat gives you two choices for installation: GUI or text-based. If you have installed Linux before you can choose either. The graphical install is better for you if you are a new user because you are guided through every step with help in the side pane. The text-based install allows you more control over what is going on during the install. This, however, requires some experience with installing Linux. All choices will be the same in the GUI installation, but they may come in different order and you'll have mouse support and a more familiar interface. The only benefit, if you want to call it that, is the ability to click through options instead of having to tab through a list and press Enter. Pressing Enter at the wrong time could cause serious problems, so this can be awkward. You navigate through the installation dialogs using a simple set of keystrokes. To move the cursor, use the arrow keys. Use Tab and Alt+Tab to cycle forward or backward through each widget on the screen. A summary of available cursor positioning keys displays along the bottom of most screens.

To “press” a button, position the cursor over the button (using Tab, for instance) and press the spacebar (or Enter). To select an item from a list of items, move the cursor to the item you want to select and press Enter. To select an item with a check box, move the cursor to the check box and press the spacebar to select the item. To deselect, press the spacebar a second time.

## Partitioning

Linux looks at hard drives differently than DOS/Windows. Instead of calling the first partition C:, the second one D:, and so on, it will usually be a combination of characters that signify the BUS and hard drive number. It works like this:

- hda—First IDE controller, Master
- hdb—First IDE controller, Slave
- hdc—Second IDE controller, Master
- hdd—Second IDE controller, Slave
- sda—First SCSI drive on the SCSI BUS

This is only the name of the devices as Linux sees them. The actual way Linux views your partitions is:

- hda1—Primary partition on first hard drive.
- hda5—Extended partition on first hard drive. The extended partition will always have the number 5 as its partition number.
- hda6+—First logical partition inside the extended partition on the first hard drive.

This is the same for partitions on SCSI devices. Generally, your CD-ROM will be hdc because there are no partitions on a CD.

Two tools that come with Red Hat Linux can be used to set up Linux partitions: the old standby, fdisk, and a graphical partitioning tool, Disk Druid. Both are acceptable methods for configuring your partitions, but Disk Druid is easier. That is what is used here. There is another tool that can be used to resize and move around partitions. It is called fips.exe. It is in the dosutils directory on the CD. This is a DOS-based program, generally used to make room for Linux when crafting a dual-boot system. Extreme caution must be exercised when using this.

## Automatic Partitioning

If you choose a workstation or server install, you'll have the opportunity to select Automatic Partitioning. However, automatic partitioning will remove any existing Linux partitions on all your computer's hard drivers, and will install the LILO boot loader into your primary volume's Master Boot Record (MBR). Do not choose automatic partitioning if you have data you'd like to preserve, or if you want to configure a custom partitioning scheme.

## Partitioning Using fdisk

For you old-timers out there, here are some pointers for fdisk. Again, Disk Druid is the recommended (and safer) way of partitioning the disks. If you want to use the fdisk partitioning program during installation, start the install program in Expert mode.

### Caution

This is the most volatile step of the entire procedure. If you mess up here, you could delete your entire hard drive. I highly recommend that you make a backup of your current system before proceeding with the disk partitioning.

Table 2.1 lists some commands and a walkthrough of fdisk.

**TABLE 2.1**
**fdisk Key Commands**

| Key | What It Does |
| :--- | :--- |
| m | Provides a listing of the available commands |
| p | Provides a listing of the current partition information |
| n | Adds a new partition |
| t | Sets or changes the partition type |
| l | Provides a listing of the different partition types and their ID numbers |
| w | Saves your information and quits fdisk |
| q | Exits without saving any changes (handy when you make a mistake) |

Use p to check the current partition information, but add your root partition beforehand. Use n to create a new partition and then select either e or p for extended or primary partition. Most likely you want to create a primary partition. You are asked what partition
