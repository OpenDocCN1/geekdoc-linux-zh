2. At the command prompt, type `fdisk device_file` and press **Enter**, where `device_file` is the device file for your first hard disk (`/dev/sda` if you have a SCSI or SATA hard disk, or `/dev/hda` if you have a PATA hard disk). At the `fdisk` prompt, type **m** and press **Enter** to view the various `fdisk` commands.

3. At the `fdisk` prompt, type **p** and press **Enter** to view the partition table on your hard disk. Which three partitions are present? When were they created? What are their `types`?

4. At the `fdisk` prompt, type **n** and press **Enter** to create a new partition. Next, type **p** to select a primary partition and press **Enter**. When prompted for the start sector, observe the valid range within the brackets and press **Enter** to select the default (the first available sector). When prompted for the end cylinder, observe the valid range within the brackets and press **Enter** to select the default (the last available sector).

5. At the `fdisk` prompt, type **p** and press **Enter** to view the partition table on your hard disk. How many partitions are present? What type of partition is `/dev/sda4` or `/dev/sda4`?

6. At the `fdisk` prompt, type **n** and press **Enter** to create a new partition. Note that logical drive is automatically selected as the partition type since all available primary partitions have been used and there is already an extended partition. When prompted for the start sector, observe the valid range within the brackets and press **Enter** to select the default (the first available sector). When prompted for the end cylinder, type **+1GB** and press **Enter**.

7. At the `fdisk` prompt, type **p** and press **Enter** to view the partition table on your hard disk. How many partitions are present? What type of partition is `/dev/sda5` or `/dev/sda5`?

8. At the `fdisk` prompt, type **l** and press **Enter** to view the different partition types. What type is used for Linux swap? Which character would you type at the `fdisk` prompt to change the type of partition?

9. At the `fdisk` prompt, type **w** and press **Enter** to save the changes to the hard disk and exit the `fdisk` utility.

10. At the command prompt, type **reboot** and press **Enter** to reboot your machine and ensure that the partition table was read into memory correctly. After your Linux system has been loaded, switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of **root** and the password of LNXrocks!

11. At the command prompt, type `mkfs -t ext4 device_file` and press **Enter**, where `device_file` is the device file for the first logical drive on your first hard disk (`/dev/sda5` if you have a SCSI or SATA hard disk, or `/dev/hda5` if you have a PATA hard disk).

12. At the command prompt, type **mkdir /newmount** and press **Enter** to create a mount point directory underneath the / directory for mounting the third partition on your first hard disk.

13. At the command prompt, type `mount -t ext4 device_file /newmount` and press **Enter**, where `device_file` is the device file for the first logical drive on your first hard disk (`/dev/sda5` if you have a SCSI or SATA hard disk, or `/dev/hda5` if you have a