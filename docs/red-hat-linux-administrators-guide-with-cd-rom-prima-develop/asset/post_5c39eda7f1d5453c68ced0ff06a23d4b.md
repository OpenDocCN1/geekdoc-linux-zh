
On some older machines, only the floppy or hard drive is available for booting the OS. If this is the case, then you must make, borrow, or purchase a boot floppy. Red Hat usually provides a boot floppy with its commercial release along with the CD and manual. However, if one is not available, then you can easily make a boot floppy from software located on the CD. Only two files are needed: rawrite.exe and boot.img. The rawrite (sometimes pronounced *raw write*) file is usually located in a utility directory on the CD. Under the Red Hat release, it is located in a directory called dosutil. The boot.img file is usually found in a directory titled images.

> **CAUTION**
>
> Trying to install one version of a Linux distribution using another version’s image will cause problems. Be sure to label the floppy clearly with the correct version. The same is true of mixing bootable images among distributions.

It may be necessary to use additional images located in this same directory, depending upon what type of installation routine you are attempting to use. You can create these images just as readily by using the same process that creates the boot floppy. Other bootable image names are bootnet.img and pcmcia.img. The former is used for booting off a network connection, and the latter is used when installing via a PCMCIA card or a laptop connection. The purpose of each of these files is to create a boot disk.

# Creating a Boot Floppy under Windows

The rawrite.exe file should be copied onto another machine, preferably one that is running either Windows or DOS. It operates by copying the raw image of a file or the information sector by sector onto a floppy disk. The boot.img file is the bootable image of Linux that brings up the CD or installs the drivers for additional installation options such as an NFS or FTP install. The same applies to the other two image files. In addition to providing some programs, this floppy contains a very basic Linux kernel and provides only the necessary drivers to make the CD-ROM functional under Linux so that the rest of the install can proceed normally. The bootnet.img file brings up some basic FTP drivers and allows your machine to recognize either a network or modem connection through which it can then download additional files. The pcmcia.img driver allows for connectivity via the PCMCIA slot on a laptop. When connected to that slot, the pcmcia.img driver recognizes the basic drivers for most Ethernet PCMCIA cards.

You might prefer installing rawrite in the root directory of your Windows machine when creating a boot floppy. The bootimg file goes in the same location. To use rawrite, simply start a DOS window and change into the root directory. Type rawrite, and then when prompted type the filename you wish to copy to the floppy. In most cases, you would type boot.img. You will need to type the target diskette drive as well. Nearly all Windows machines use a:\ as their primary floppy drive specification. Figure 1.3 shows a sample session.

Once rawrite is done copying the file to the floppy sector by sector, you will get your prompt back. You can now use this floppy on most PCs to boot up the Linux installation program.

# Creating a Boot Floppy Using Linux

The boot image can just as easily be made on a Linux machine. You must have root or superuser permission in order to write to the floppy drive or the /dev/fd0 device. For most users, this is the 1.44 megabyte floppy drive. You may also need to be more specific when listing this device if you have more than one type of floppy drive. A definitive path would be the following: /dev/fd0H11440. This path specifies the initial floppy drive or a:\ drive. If a second floppy drive, or b:\, exists, then the assignment would be /dev/fd1H11440.

![](img/a0884097af3186d9b4f616aaa3f065b0_54_0.png)

![](img/a0884097af3186d9b4f616aaa3f065b0_54_1.png)

> **TIP**
>
> Under UNIX and Linux variants, counting begins with 0. The number **1** is the second number.

To copy over the boot image from the distribution CD, mount the CD itself in Linux and then change to the directory where boot.img is stored. Insert a blank, formatted diskette and type the following:

```
# dd if=boot.img of=/dev/fdH1440 bs=1440k
```

Additional information about the dd command, which copies over files, can be verified by consulting the *man* or manual pages. To refer to the man pages on dd type **man dd** at any command line.

Red Hat has an added feature that makes installing Linux even easier. The Kick-Start method allows a user to set up a specific configuration and then have Linux run the rest of the install process automatically. This is convenient for those users who need to set up multiple Linux machines but who don’t have the time to configure each and every option manually.

> **NOTE**
>
> If you know the specific programs you want to install on all machines, you can create a default configuration on the initial machine. You can save this format to a floppy. By simply transferring the same floppy from one computer to the next, you can bypass much of the typing and decision-making.

# Partitioning the Drives

In preparation for any sort of Linux install, you will need to sit down and sketch out some idea of what you want your Linux box to do and where to place each file. Linux is quite versatile in that you can set up separate partitions for different directories. A *partition* is the method by which a single physical disk is divided into multiple logical disks. Each partition is a contiguous section of blocks that is then treated like a separate and distinct physical drive. Although you may have only one drive, you can have several partitions, thus making your computer appear to have several drives. Computers with only a few physical hard drives can have several partitions.

> **NOTE**
>
> Though you may have only one physical hard drive in your machine; if you divide it into four separate partitions, your machine will then treat all four partitions like individual drives, renaming them under Windows as drives C, D, E, and F. Linux will recognize them as devices and will refer to them respectively as `/dev/hda1`, `/dev/hda2`, `/dev/hda3`, and `/dev/hda4`.

Most operating systems allow for this method of sectioning off blocks of information into separate partitions. Some of the basic rules for partitions are:

- They cannot overlap.
- You cannot mount the same directory on different partitions.
- You don't have to partition all the available space on a hard drive. Some space can be left for later to be used with other operating systems or for other partitions.

Once you have decided how you want to set up your system, it is prudent to write down the physical parameters of your configuration. Documenting the setup of your computer cannot be stressed enough. Many people have saved themselves painful hours of stressful reinstallation and retrying by documenting the layout of all the systems. I still have three binders full of notes that I have collected over the years. Though I don't consult them much now, I do occasionally refer to them for specific instructions. Knowing which physical drive holds its respective logical partitions or directories can save you much time and money.

> **TIP**
>
> You can have a partition dedicated entirely to the `/home` directory or the directory where you keep your own local files. In the case of a reinstall, this allows you to retain all your data while reformatting the other partitions.

If you are not used to breaking up directories into different partitions, this can be a bit intimidating, but with a little practice it can prove to be beneficial. Though there may not be much space on some of the older, smaller drives, you can opt to install all your files and directories into one main root or / directory. The root directory is the highest level of all Linux partitions.

# Selecting Mount Points

Red Hat Linux utilizes two different tools for partitioning drives. The one currently touted by Red Hat as being the most dynamic is *Disk Druid*. This tool allows the user to create multiple partitions for each directory. Unlike its predecessor, *fdisk*, Disk Druid is not limited to only four partitions. During the installation phase, you will most likely see Disk Druid as your default partitioning tool. In the latest release of Red Hat, you may opt to use fdisk as well to give the partitions added functionality. Disk Druid can set the partition to only a limited number of partition types.

> **CAUTION**
>
> If you decide to set aside a portion of your Windows partition for Linux, be sure to defragment the drive first so that all files are located in one section of the drive. The remaining space can then be turned over to Linux by using the tools *Tips*, included on the CD.

For those unfamiliar with the partitioning schema associated with Linux, Red Hat offers sample mount points for each partition. Rather than attempting to guess at what partition might be needed, Red Hat lists directories — such as //boot, /home, /opt, /usr, /usr/local, and /var — as possible mount points for each partition. Though many regard fdisk as the superior tool, Red Hat offers both tools during the install process. To optimize the partitioning schema, you should use a combination of both tools.

There are advantages to command-line tools that allow for the toggling of partition identities such as alternative file system types or formats. The Linux fdisk tool is much more robust than the Microsoft counterpart and can create partitions compliant for a variety of other operating systems, including Windows NT, OS/2, and other operating systems.
