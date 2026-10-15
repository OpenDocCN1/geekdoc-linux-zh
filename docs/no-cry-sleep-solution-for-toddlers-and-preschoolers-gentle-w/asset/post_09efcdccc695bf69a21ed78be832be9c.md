
To initialize a physical volume on an entire hard disk, you use the hard disk device name, as shown here.

```
pvcreate /dev/hdc
```

Then use the vgextend command to add the partition to a logical group, in this case, rabbit. In effect, you are extending the size of the logical group by adding a new physical partition.

```
vgextend rabbit /dev/hda3
```

To remove a physical partition, first remove it from its logical volume. You may have to use the pmove command to move any data off the physical partition. Then use the vgreduce command to remove it from its logical group.

## Managing LVM Groups

You can manually create a volume group using the vgcreate command and the name of the group along with a list of physical partitions you want in the group. The following example creates a group called rabbit consisting of three physical partitions, /dev/hda3, /dev/hdb4, and /dev/hdb4.

```
vgcreate rabbit /dev/hda3 /dev/hdb2 /dev/hdb4
```

You can remove a volume group by first deactivating it with the vgchange -a n operation and then using the vgreduce command.

## Activating Volume Groups

Whereas in a standard file system structure, you mount and unmount hard disk partitions, with an LVM structure, you activate and deactivate entire volume groups. The group volumes are accessible until you activate them with the vgchange command with the -a option. To activate a group, first reboot your system, and then enter the vgchange command with the -a option and the y argument to activate the logical group (an n argument will deactivate the group).

```
vgchange -a y rabbit
```

## Managing LVM Logical Volumes

To create logical volumes, you use the lvcreate command. With the -n option you specify the volume's name, which functions like a hard disk partition's label. You use the -L option to specify the size of the volume. The following example creates a logical volume named projects on the rabbit logical group with a size of 20GB.

```
lvcreate -n projects -L 20000M rabbit
```

You can remove a logical volume with the lvremove command. With lvextend, you can increase the size of the logical volume, and lvreduce will reduce its size.

## LVM Example

Using the example in Figure 31-2, the steps involved in creating and accessing logical volumes are described in following commands. First use a partition creation tool like fdisk or parted to create the physical partitions on the hard disks hda and hdb. In this example, you create the partitions hda1, hda2, hda3, hdb1, hdb2, hdb3, and hdb4.

Then you initialize the physical volumes with the pvcreate command. The hda1 and hda2 partitions are reserved for the boot and root partitions and are not initialized.

```
pvcreate /dev/hda3 /dev/hdb1 /dev/hdb2
pvcreate /dev/hdb3 /dev/hdb4
```

You then create the logical groups you want using the vgcreate command. In this case, there are two logical groups, turtle and rabbit. The turtle group uses hdb1 and hdb3, and rabbit uses hda3, hdb2, and hdb4. If you create a physical volume later and want to add it to a volume group, you would use the vgextend command.

```
vgcreate turtle  /dev/hdb1 /dev/hdb3
vgcreate rabbit  /dev/hda3 /dev/hdb2 /dev/hdb4
```

### FIGURE 31-2
Logical Volume Management

![](img/6c226e8ba1efd427dec3bf582418d33f_647_0.png)

You can now create the logical volumes in each volume group, using the lvcreate command.

```
lvcreate -n var      -l 2000M  turtle
lvcreate -n home      -l 5000M  rabbit
lvcreate -n projects  -l 2000M  rabbit
```

Then you can activate the logical volumes. Reboot and use vgchange with the -a y option to activate the logical volumes.

```
vgchange -a y turtle rabbit
```

You can now make file systems for each logical volume.

```
mkfs.ext3 var
mkfs.ext3 home
mkfs.ext3 projects
```

Then you can mount the logical volumes.

```
mount var /var
mount home /home
mount projects /mnt/myprojects
```

## CHAPTER

## Devices and Modules

All devices, such as printers, terminals, and CD-ROMs, are connected to your Linux operating system through special files called device files. Such a file contains all the information your operating system needs to control the specified device. This design introduces great flexibility. The operating system is independent of the specific details for managing a particular device; the specifics are all handled by the device file. The operating system simply informs the device what task it is to perform, and the device file tells it how. If you change devices, you have to change only the device file, not the whole system.

To install a device on your Linux system, you need a device file for it, software configuration such as that provided by a configuration tool, and kernel support—usually supplied by a module or support that is already compiled and built into the kernel. An extensive number of device files are already set up for different kinds of devices. Usually you need only one, which is specific to your device. When you add new hardware devices, Kudzu, the Red Hat hardware probing tool, checks for the new hardware when your system boots. The Kudzu tool automatically detects a new device and lets you configure it. A profile of your hardware configurations is saved by Kudzu in the /etc/sysconfig/hwconf file. For more specialized kernel support, you may have to load a kernel module or recompile the kernel, both simple procedures (see Chapter 33). In most cases, support is already built into the kernel.

## Device Files

The name of a device file is designed to reflect the task of the device. Printer device files begin with lp for “line print.” Because you could have more than one printer connected to your system, the particular printer device files are distinguished by two or more numbers or letters following the prefix lp, such as lp0, lp1, lp2. The same is true for terminal device files. They begin with the prefix tty, for “teletype,” and are further distinguished by numbers or letters such as tty0, tty1, tty50, and so on. You can obtain a complete listing of the current device filenames and the devices for which they are used from the kernel.org Web site at www.kernel.org/pub/linux/docs/device-list/devices.txt.
