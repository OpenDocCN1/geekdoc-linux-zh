> CAUTION: Before using fdisk to change your partitions, I strongly recommend running the df -h command to see how your partitions are currently being defined. This will help reduce the risk of changing or deleting the wrong partition.

To use fdisk to change your partitions, begin (as root user) by typing:

```
# fdisk device
```

where device is replaced by the name of the device you want to work with. For example, here are some of your choices:

+   - `/dev/hda`: For the first IDE hard disk; hdb, hdc, and so on for other IDE disks.
+   - `/dev/sda`: For the first SCSI hard disk; sdb, sdc, and so on for other SCSI disks.
+   - `/dev/rd/c0d0`: For a RAID device.
+   - `/dev/ida/c0d0`: Also for a RAID device.

After you have started fdisk, type m to see the options. Here is what you can do with fdisk:

+   - **Delete a partition** — Type d and you are asked to enter a partition number on the current hard disk. Type the partition number and press Enter. For example, /dev/sda2 would be partition number 2. (The deletion won’t take effect until you write the change. Until then, it’s not too late to back out.)
+   
+   - **Create a partition** — If you have free space, you can add a new partition. Type n and you are asked to enter 1 for a logical partition (5 or over) or p for a primary partition (1–4). Enter a partition number from the available range. Then choose the first cylinder number from those available. (The output from fdisk -1 shown earlier will show you cylinders being used under the Start and End columns.)
+   
+   Next, enter the cylinder number the partition will end with (or type the specific number of megabytes or kilobytes you want: for example, +50M or +1024k). You just created an ext3 Linux partition. Again, this change isn’t permanent until you write the changes.
+   
+   - **Change the partition type** — Press t to choose the type of file system. Enter the partition number of the partition number you want to change. Type the number representing the file system type you want to use in hexadecimal code. (Type L at this point to see a list of file system types and codes.) For a Linux file system, use the number 83; use 82 for a Linux swap partition. For a windows FAT32 file system, you can use the letter b.
+   
+   - **Display the partition table** — Throughout this process, feel free to type p to display (print on the screen) the partition table as it now stands.
+   
+   - **Saving and quitting** — If you don’t like a change you make to your partitions, press q to exit without saving. Nothing will have changed on your partition table.