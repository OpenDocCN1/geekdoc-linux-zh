250 Chapter 5 Linux Filesystem Administration

+   4. At the parted prompt, type mkpart and press Enter to accept the default of logical drive. Press Enter again to accept the default partition type (Linux ext2). When prompted for the Start of the new partition, enter the (A) value you recorded in Step 3 and press Enter. When prompted for the End of the new partition, enter the (B) value you recorded in Step 3 and press Enter.

+   5. At the parted prompt, type p and press Enter to view the partition table on your hard disk. How many partitions are present? What type of partition is /dev/sda6 or /dev/hda6?

+   6. At the parted prompt, type quit and press Enter to save the changes to the hard disk and exit the GNU Parted utility.

+   7. At the command prompt, type reboot and press Enter to reboot your machine and ensure that the partition table was read into memory correctly. After your Linux system has been loaded, switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of root and the password of LNXrocks!.

+   8. At the command prompt, type pvcreate device_file and press Enter, where device_file is the device file for your new partition (/dev/sda6 if you have a SCSI or SATA hard disk, or /dev/hda6 if you have a PATA hard disk). What does this command do?

+   9. At the command prompt, type vgcreate vg00 device_file and press Enter, where device_file is the device file for your new partition (/dev/sda6 if you have a SCSI or SATA hard disk, or /dev/hda6 if you have a PATA hard disk). What does this command do?

+   10. At the command prompt, type lvc create -L 2GB -n vq00 vg00 and press Enter to create a 2GB logical volume called volumel from the vg00 volume group.

+   11. At the command prompt, type lvcreate -L 2.5GB -n volum2 vg00 and press Enter to create a 2.5GB logical volume called volum2 from the vg00 volume group.

+   12. At the command prompt, type mkfs -t ext4 /dev/vg00/voluml and press Enter to format the volume1 logical volume using the ext4 filesystem. Next, type mkfs -t ext4 /dev/vg00/volum2 and press Enter to format the volum2 logical volume using the ext4 filesystem.

+   13. At the command prompt, type mkdir /voluml and press Enter to create a mount point for the volume1 logical volume. Next, type mkdir /volum2 and press Enter to create a mount point for the volum2 logical volume.

+   14. At the command prompt, type mount -t ext4 /dev/vg00/voluml /voluml and press Enter to mount the voluml logical volume to the /voluml directory. Next, type mount -t ext4 /dev/vg00/volum2 /volum2 and press Enter to mount the volum2 logical volume to the /volum2 directory. When finished, type mount and press Enter to verify that both filesystems are mounted.

+   15. At the command prompt, type ls -F /voluml /volum2 and press Enter. Is there a lost+found directory underneath each directory? Why?