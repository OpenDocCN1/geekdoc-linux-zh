> **Note**  
> The rescue disk cannot be mounted, because it is not a file system. It only contains the compressed images of one. Directions for reading the file system are in the following paragraph.

To read the image, you will need to decompress the image file then mount the decompressed image as user root. If your Linux kernel support the loop device, the procedure is as follows:

```
earth:  # cp /media/cdrom/disks/rescue /root/rescue.gz
earth:  # gunzip /root/rescue.gz
earth:  # mount -t ext2 -o loop /root/rescue /mnt
```

# Starting the Rescue System

The rescue system is launched by the SuSE boot disk you created or by your bootable CD or DVD. It is required that the disk and CD-ROM or DVD drives are bootable. If necessary, change the boot series in the CMOS setup. Following are the steps for starting the rescue system:

+   1. Start your system with the SuSE boot disk created yourself or with the first SuSE Linux CD or DVD inserted into the corresponding drive.
+   2. Launch the entire system or choose ‘Manual Installation’ so that ‘boot options’ can be entered and kernel modules to load can be defined.
+   3. Make the respective settings for language and keyboard.
+   4. Select the item ‘Installation/Start system’ in the main menu.
+   5. If you started with the boot disk, now insert the installation CD or the rescue disk with the compressed image of the rescue system.
+   6. In the menu ‘Start installation/system’ select the item ‘Start rescue system’ (see Figure 3.3 on page 36) then specify the desired source medium (Figure 11.6 on the following page).

Subsequently, we will introduce a few tips on selection options:

> ‘CD-ROM’: When loading the rescue system, the path `/cdrom` is exported. This makes the installation from *this* CD possible.