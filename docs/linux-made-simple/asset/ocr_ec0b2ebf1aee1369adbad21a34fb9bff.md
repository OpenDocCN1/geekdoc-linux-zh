# Back it all up!

Stick with us – before migrating to Linux, make a fail-safe backup.

The simplest way to back up your system is to use the built-in Windows Backup tool in Windows 7 or later – select 'System Image Backup' and follow the prompts. It's not very exciting and it's a little scary, but it is essential. For a pure Linux back-up solution, use SystemRescueCD, which is on the cover disc. Here's how... Reboot your PC with the disc in your drive, access the boot menu if necessary (usually [F11]) and choose your DVD drive, then 'SystemRescueCD'. Problems booting could be caused by your PC's UEFI (see over the page to fix them). Otherwise, pick the default boot options entry. Type uk when prompted for the keyboard layout, and type startx at the final command prompt to access the graphical environment. Once this loads, click the 'Menu' button in the bottom-left and select 'System > Show Filesystems' to identify each partition. The Disk entries identify each physical drive (sda, sdb and so on) and the Device identifies the partitions. In most cases, sda will be your Windows drive, so you'll need to back up sda1 (a small boot partition) and sda2 (the actual Windows partition). You'll also need to note the partition you intend to back up to and make sure it has enough free space. Now switch to the terminal window. To mount the back-up partition, type the following command, changing ntfs to FAT if your back-up drive is FAT32, and replacing sdc2 with the drive's actual partition name:

```
Mount -t ntfs /dev/sdc2 /mnt/backup
```

Now re-open the menu and select 'System > Partimage'. This tool lets you back up partitions, so start with /dev/sda1, then press [Tab]. Next, type /mnt/backup/sda1-backup.gz into the 'Image file to create/use' box. Leave 'Save partition into a new image file' selected and press [F5]. Verify 'Gzip' is selected under 'Compression level', then click [F5] again. Enter a description if you wish, then press [Tab] to select 'OK' and hit [Enter]. Make a note about experimental NTFS support, then click 'OK' twice, noting the drive statistics. If this successfully completes, repeat to back up your Windows partition, naming it sda2-backup.gz instead.

To back up your computer's Master Boot Record, open a terminal window and type the following commands

```
cd mnt/backup
mkdir partition-backup
cd partition-backup
dd if=/dev/sda of=backup-sda.mbr count=1 bs=512
to back up MBR. Now back up your partition table with:
sfdisk -d /dev/sda > backup-sda.sf
```

If you get a warning about sfdisk not supporting GPT partitions, type sgdisk --backup=backup-sda.sg /dev/sda instead. If disaster strikes, either boot from your Windows rescue disc and follow the prompts, or boot back into SystemRescueCD. If you got as far as Ubuntu resizing your Windows partitions, you'll first need to launch the Gparted partitioning tool from its Taskbar shortcut. It should display your main hard drive (/dev/sda), so identify the extended partition. Right-click each volume inside it and choose 'Delete', then right-click the extended partition and delete that too. Next, right-click your Windows partition and choose 'Resize/Move'. Allocate it all available space, click 'Resize/Move' then 'Apply'. To complete the partition restore process, follow the step-by-step guide (below). The final step is restoring the MBR. Open another terminal window and type:

```
cd /mnt/backup/partition-backup
dd if=backup-sda.mbr of=/dev/sda
```

If you backed up your partition using sfdisk, type sfdisk /dev/sda < backup-sda.sf into the command prompt; if you used sgdisk, type sgdisk --load-backup=backup-sda.sg /dev/sda instead to complete the restore.

# Restore your original setup

![](bbox=[0.12, 0.7, 0.36, 0.81])

# 1 Select backup

Boot into SystemRescueCD as before. Follow the steps in the main text (above) up to identifying your partitions. Next, mount the back-up partition in the /mnt/backup directory. Once done, open Partimage. Leave 'sda1' selected, type the back-up path and name from before into the 'Image file' box.

![](bbox=[0.37, 0.7, 0.62, 0.81])

# 2 Restore boot partition

Press [Tab] twice to highlight the asterisk by 'Save partition', then press the down arrow then [Space] to select 'Restore partition from an image file'. Press [F5]. Note the description and press [Enter]. Press [F5] to restore the partition, working through the warnings until the files are copied back.

![](bbox=[0.63, 0.7, 0.88, 0.81])

# 3 Restore main partition

Partimage will close once the partition has been restored, so launch it again but this time select your main Windows partition (typically 'sda2'). Then it's a case of repeating the previous steps, only this time using the first back-up file. Note: the restoration relies on your Windows partition being the same size.