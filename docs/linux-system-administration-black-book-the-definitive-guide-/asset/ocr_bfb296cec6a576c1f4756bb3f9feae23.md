# # Scripting Tips For KickStart

When putting together a script to handle post-installation information in KickStart, keep the following items in mind:

+   - Use the **echo** command to print out explanations of each step. This lets you see at a glance where the installation is and relieves you from having to go back through and do this later if you need to debug the post-installation section.
+   - If you have particularly complex routines to execute, have the KickStart script call other scripts. Just remember to include these scripts on the boot disk\-if they will fit\-or in the same network directory as the KickStart script.
+   - Remember that if you are having a hard time debugging a complex script, you can comment out sections by starting each line with a hash mark (#) to isolate pieces of code.

# # Making A KickStart Boot Disk

To make a Red Hat boot disk that also contains a KickStart installation automation file, do the following:

+   1. Log in as root.
+   2. Use the **df** command to see whether the Red Hat CD-ROM is mounted. If not, place it in the drive and type “mount /mnt/cdrom” to add it to the file system.
+   3. Place the floppy disk that you intend to use as the boot disk for your automated install into the floppy drive.

> **WARNING!** *All data on this disk will be erased.*

+   4. Type “dd if=/mnt/cdrom/images/boot.img of=/dev/fd0” to create a new Red Hat boot install disk. Use bootnet.img if you are doing an NFS install.

> **NOTE:** Do not use the **mkbootdisk** command. This command creates a customized boot disk for the machine in question. You need a boot disk that handles the installation process.

+   5. After the drive light goes off, the copying is done. Now, type “mount -t vfat /dev/fd0 /mnt/floppy” to add this disk to your file system.

> **NOTE:** *The installation disk is in MS-DOS format, not ext2.*