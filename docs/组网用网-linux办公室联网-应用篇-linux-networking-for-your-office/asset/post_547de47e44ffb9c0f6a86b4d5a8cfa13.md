
5. The program asks you to insert a floppy in the A: drive. Do so. Note that the floppy must have no bad sectors, or it won’t work correctly. After you insert a floppy, press the Enter key.
6. Your CD-ROM and floppy indicator lights should flicker for a while as the computer makes a copy of the disk image.

## NOTE

The CD-ROM that accompanies this book includes a Windows NT version of the RAWRITE utility, in the directory rawriteNT, so you can create a Linux boot floppy from Windows NT or 2000. (The normal RAWRITE doesn’t run from Windows NT.)

If you don’t have access to a DOS or Windows system, you can create a disk image on a Linux or UNIX system by following these steps:

- 1. Mount the CD-ROM drive by typing mount /mnt/cdrom or something similar (details vary from system to system).
- 2. Insert a formatted floppy disk in the computer’s floppy drive. This floppy must have no bad sectors, or it won’t work correctly.
- 3. Type
  dd if=/mnt/cdrom/images/boot.img of=/dev/fd0
  to create a Red Hat boot floppy. The path to boot.img might be different if you used a different mount point, and the device file might not be /dev/fd0 on all systems, particularly if you’re using a UNIX system that’s not Linux. You might need to be root to issue this command.

After you’ve created a floppy, you can use it to boot the computer into the Red Hat Linux installer. The first screen you’ll see is the Red Hat installation boot: prompt, shown in Figure 5.2. You can press the Enter key here to continue the boot process. In rare cases, you might need to track down special parameters to type at this prompt in order to get Linux to recognize your hardware. If, after you press Enter, the system displays some text and hangs, you should consult Red Hat’s documentation (in the doc/rhmanual1/manual1 directory on the Red Hat CD-ROM) for help.

![](img/5d4d3092919d1d16884788127447cc6d_138_0.png)

## FIGURE 5.2

The Linux boot prompt lets you enter parameters to tell the Linux kernel how to handle unusual hardware configurations.

## NOTE

If you want to do a network installation because your target system lacks a CD-ROM or because you want to install a more recent version of Red Hat, you need to create a floppy disk image from the bootnet.img file for the version of Red Hat Linux you want to install. You do this much as I’ve just described. The CD-ROM that accompanies this book includes the Red Hat 6.0 bootnet.img file, but if you want to install a more recent version of Red Hat, you need to obtain an appropriate image file for it. You can install Red Hat 6.0 from the CD-ROM that accompanies this book by using a network install with a Linux or Windows computer serving the CD-ROM’s files.

## Starting the Installation

After you press Enter at the boot: prompt, a number of messages appear on the screen. These are status reports from the Linux kernel about your hardware, the drivers being installed, and so on. After these messages are finished, the Red Hat installer welcome screen greets you.

When you press the Enter key at the installer screen, Red Hat prompts you for a number of pieces of information, using prompts similar to those shown in Figure 5.3. At each prompt, you’ll see a list of selections. Use the arrow keys to move through the list, and then press Enter when you’ve reached your selection. You’ll be asked about the language, keyboard, and installation source you want to use.

## FIGURE 5.3

You navigate installation menus by using the Spacebar and the arrow, Tab, Alt+Tab, and Enter keys.

The installer accesses the CD-ROM, and then asks you more questions, some of which use a multiple-choice format. Use the arrow keys or Tab and Alt+Tab to switch between choices. The installer asks if you want to do a new installation or upgrade an existing one; whether to perform a workstation, server, or custom install; and what type of SCSI host adapter you have. I recommend doing a custom install because this gives you the greatest control over the installation process.

Red Hat gives you a choice of using either of two tools for partitioning your disk: Disk Druid or fdisk. Disk Druid is easier to use, but it has a distressing tendency to produce unusable partitions. I therefore recommend that you use fdisk. When you’re in Linux fdisk, you can type single-letter commands and then press the Enter key. The most important command to remember is h, which lists the available commands. I recommend starting with the p command, which displays the existing partition table, as shown in Figure 5.4. You can then use n to create new partitions. By default, Linux’s fdisk creates partitions of type 83—Linux native. You should change your swap partition to type 82 with the t command after you create it. When you’ve created all your partitions to your satisfaction, use the w command to write the partition table and exit. You’ll then return to the Partition Disks screen. If you’re done, select Done.

## NOTE

If you created partitions for Linux with DOS FDISK or most other programs, you can leave them in place, but you must change the partition types using the t command in Linux fdisk.
