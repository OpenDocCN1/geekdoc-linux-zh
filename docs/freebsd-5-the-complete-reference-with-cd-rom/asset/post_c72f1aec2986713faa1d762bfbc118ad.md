
the early part of the disk, leaving nothing but empty space at the end, in the area you want to devote to FreeBSD. It’s also a very good idea to perform a check of the partition’s integrity (by clicking Check Now in Figure 2-3). Note that some disk utilities place files that cannot be moved at the end of the disk. You may need to temporarily disable such utilities and delete their data files before proceeding.

- 2. Boot to DOS. Ensure that you have CD-ROM drivers available on your DOS floppy, or copy the PIPS.EXE program from the FreeBSD CD-ROM’s TOOLS directory to a floppy disk or hard disk partition you can read from DOS. If you don’t have a DOS boot floppy, you can use FreeDOS (http://www.freedos.org), an open source re-implementation of DOS.

> **Caution**  
> Do not *run FIPS from a multitasking OS such as OS/2 or Windows*. (The Windows 9x DOS boot works, but don’t *run FIPS* from a DOS window in the Windows desktop.) Doing so can confuse the OS and cause file corruption.

![](img/f34d37e3abe9f4517128e54f80ab2616_78_0.png)

Figure 2-3. Click *Defragment Now* to defragment a hard disk in Windows.

- 3. Change to the directory in which FIPS resides and type **fips** to run the program. The program displays some introductory text.

- 4. Press a key. FIPS displays information on the hard disk’s partition table. This information applies only to primary partitions; FIPS can’t operate on logical partitions, and so displays no information on them. Partitions are defined in terms of their starting and ending cylinders, heads, and sectors. These so-called **CHS numbers** are used by the BIOS for addressing the disk, and you’ll subsequently modify the ending cylinder number to shrink the DOS or Windows partition.

- 5. Press a key. FIPS displays information on your C: partition. If you’re familiar with FAT data structures, you can check that this information is correct, or at least reasonable; otherwise you can ignore it. FIPS also asks if you want to make a backup copy of the root and boot sectors. I recommend you respond **y** to do so, allowing you to back out of the operation if something goes wrong.

- 6. FIPS asks if a bootable floppy disk is in the A: drive. If necessary, insert a floppy disk and type **y**. FIPS will then save the root and boot sectors to the floppy disk.

- 7. FIPS computes the minimum size it can make the existing C: partition and displays this size, along with the size of the new primary partition it will create. If you want to make a larger C: partition (which is advisable in most cases, so you have room for new files on your DOS or Windows installation), use the right arrow key to increase the size of C: at the expense of the new FreeBSD slice. FIPS modifies partition sizes by one cylinder at a time; so, depending upon the size of your disk, you may see your partitions change in size by several megabytes with each arrow keypress. When the system displays the division you want, press Enter to continue.

- 8. FIPS displays summary information on the new partition layout similar to what it showed in Step 4. If you approve of the new layout, type **c** to have FIPS continue with the changes. If not, type **r** to redo the changes (going back to Step 7).

- 9. FIPS displays summary information on the new C: partition’s FAT filesystem, similar to what it showed in Step 5. Type **y** to continue, and FIPS writes its changes to the disk.

At this point, you’ll have two partitions in place of one. When you install FreeBSD, you can tell the installer to delete the second partition and create a new FreeBSD slice in its place.

Unfortunately, FIPS is limited in its features. If you want to resize logical or NTFS partitions, move partitions, or perform other actions, FIPS won’t do. For that, you’ll need a more sophisticated tool, such as the commercial PartitionMagic.

## Using PartitionMagic

PartitionMagic is a much more flexible tool than FIPS. Using PartitionMagic, you can create, delete, move, or resize FAT, NTFS, High-Performance File System (HPFS), or Second Extended File System (ext2fs) partitions. (HPFS support was removed from version 7.0 of the software, however, so if you need HPFS support you should get version 6.0 or earlier. Versions prior to 4.0 didn't support Linux's ext2fs.) You also need not defragment a hard disk before running PartitionMagic, although checking the disk integrity beforehand is a good idea.

PartitionMagic can run from either a DOS boot floppy or from a fully booted Windows system. The user interface is similar in either case, although the DOS version lacks some features, such as the ability to automatically design layouts for various combinations of OSs. Once the system is booted, it presents a graphical view of the disk, including both a bar chart showing your partitions and a textual partition list. You can click on a partition in either area and select Partitions | Resize to resize the partition. The result is a dialog box like the one shown in Figure 2-4, in which you can enter the new partition size by dragging the right end of the existing partition or entering a new size in the numeric data entry fields.

For FreeBSD use, it's simplest if you leave the space for FreeBSD unallocated; PartitionMagic can't create a FreeBSD slice, so you'll have to create that within the FreeBSD installer. Be sure this unallocated FreeBSD space is *not* within an extended partition; FreeBSD needs to create a primary partition for itself, and if the only free space is within an extended partition, FreeBSD won't be able to use it. (PartitionMagic displays extended partitions as light blue boxes within which logical partitions reside. If necessary, you can shrink an extended partition just as you would any other partition type.)

When you're done with entering changes, click the Apply button in the main PartitionMagic window. The program will then commit the changes you've entered, ultimately making space available for FreeBSD.

![](img/f34d37e3abe9f4517128e54f80ab2616_80_0.png)

Figure 2-4. *PartitionMagic lets you resize partitions using GUI controls.*

## Beginning the Installation

Once you've cleared away space for FreeBSD, you can begin the installation process. This involves booting a FreeBSD installer, setting some initial configuration options, and creating a FreeBSD slice and partitions within that slice for your FreeBSD installation.

### Booting an Installer

To install FreeBSD, you must boot its installer. This is a special stripped-down FreeBSD system that includes software to copy FreeBSD files from an installation medium to your hard disk. The two types of FreeBSD boot media are

- **CD-ROMs** Most FreeBSD installation CD-ROMs, including the one that comes with this book, are bootable. To boot, you must configure your BIOS to try to boot from the CD-ROM drive before booting from the hard disk, insert the FreeBSD CD-ROM in the computer, and exit from the BIOS utility. If you can't find a boot-from-CD-ROM option in the BIOS, if it doesn't work, or if you don't have a FreeBSD CD-ROM, you may need to use a boot floppy.

- **Floppies** The earlier section, "Boot Disks," described how to create FreeBSD installation floppy disks. The first of these is bootable. If your BIOS is configured to try to boot from a floppy disk before trying the hard disk (as most are by default), you can insert the FreeBSD boot floppy and start the computer. It will eventually ask for the second disk, which you should insert when prompted, and load up the FreeBSD installation program.

The FreeBSD installation procedure is the same whether you boot from a CD-ROM or a floppy disk. Indeed, even the boot process is very similar. In both cases, you'll see a large number of messages scroll by on the screen. These relate to internal kernel checks and hardware driver installation. Some of these messages may scroll past so quickly that you won't be able to read them. Don't worry about this unless you have problems using some vital hardware component. In such a case, you may need to temporarily work around the problem and then perform troubleshooting, as described in Chapter 32. For instance, if the installer doesn't recognize your CD-ROM drive, you may need to perform a network installation or temporarily use another CD-ROM drive, then work on fixing the problem once FreeBSD is fully installed.

Once the installer has booted, it displays a menu similar to the one shown in Figure 2-5. This program is the sysinstall utility, which, as the name suggests, installs a FreeBSD system. You can also use it after installing FreeBSD to add or delete software, upgrade the system, and make some modifications to the OS.

You may want to take some time to experiment with the sysinstall user interface, particularly if you're not used to text-based menu systems. The arrow keys move selection points around. In most menus, the up and down arrows move up and down the list of options (such as Usage, Standard, Express, and so on in Figure 2-5), while the left and right arrows select between the action buttons at the bottom of the
