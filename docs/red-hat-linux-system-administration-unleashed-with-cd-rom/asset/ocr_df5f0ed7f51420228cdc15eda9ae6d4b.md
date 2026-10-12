Now that the driver is loaded and the disk has been recognized, it is time to start actually using the disk. There are three scenarios here. The first is that you will be using Zip disks preformatted for Windows. In this case, you must create a mount point and then mount the disk and begin using it with the following commands:

```
mkdir /mnt/zip; mount -t vfat /dev/sda4 /mnt/zip
```

The filesystem on the disk is now mounted and you access it like any other mount vfat partition, with standard Linux commands such as ls, cp, mv, and rm. In the event that you prefer to have a Linux filesystem on the Zip disk, you can use the following commands to create a Linux partition and filesystem on the disk:

```
echo ",," | /sbin/sfdisk /dev/sda ; mk2fs /dev/sda1
```

This has the effect of creating a single Linux partition, /dev/sda1, on the disk that takes up the entire disk and then creating a filesystem on it. Once this is done, you can mount the newly created extended type 2 filesystem and treat it as you would any other disk.

# Parallel Port ATAPI/IDE Devices

Other devices that connect to the parallel port of your system, such as the Imation SuperDisk LS-120 or any of the MicroSolutions backpack devices, are also supported.

These devices make use of the paride drivers that are part of the Linux 2.2.x kernel. Just as with the Zip drive support, using these devices is just a matter of loading the appropriate modules and then accessing the devices via the appropriate device names, assuming that you have configured your kernel to support them. In this case, the modules to be loaded are broken into three categories:

+   - The paride module, which provides a registry and basic control of the parallel port.
+   - The protocol module for the devices you have attached.
+   - The high-level modules for the specific device types, such as disk drives, CD drives, or floppy drives.

For example, if you have a SyQuest EZ135A drive connected to your system, the modules you need are the paride module, the epat protocol module, and the pd disk module. In this case, the output resulting from installing these modules might look like this:

```
[root@wizard etc] insmod paride
paride: version 1.0 installed

[root@wizard etc] insmod epat
paride: epat registered as protocol 0

[root@wizard etc] insmod pd
```