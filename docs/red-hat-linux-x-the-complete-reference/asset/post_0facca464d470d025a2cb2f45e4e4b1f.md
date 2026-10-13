
Then create your RAID devices with `mkraid`.

```
mkraid md0 md1 md2
```

Activate the RAID devices with `raidstart`.

```
raidstart md0 md1 md2
```

Create your file systems on the raid devices.

```
mkfs.ext3 md0 md1 md2
```

You can then migrate the `/boot`, `/`, and `/home` files from your current hard disk to your RAID devices. Install your boot loader on the first RAID device, `md0`, and load the root file system from the second RAID device, `md1`.

## Logical Volume Manager

For easier hard disk storage management, you can set up your system to use the Logical Volume Manager (LVM), creating LVM partitions that are organized into logical volumes to which free space is automatically allocated. Logical Volumes provide a more flexible and powerful way of dealing with disk storage, organizing physical partitions into logical volumes in which you can easily manage disk space. Disk storage for a logical volume is treated as one pool of memory, though the volume may in fact contain several hard disk partitions spread across different hard disks. Adding a new LVM partition merely increases the pool of storage accessible to the entire system.

### LVM Structure

In an LVM structure, LVM physical partitions, also known as extents, are organized into logical groups, which are in turn used by logical volumes. In effect, you are dealing with three different levels of organization. At the lowest level, you have physical volumes. These are physical hard disk partitions that you create with partition creation tools such as parted or fdisk. The partition type can be any standard Linux partition type, such as ext3 or ext2. These physical volumes are organized into logical groups, known as volume groups, that operate much like logical hard disks. You assign collections of physical volumes to different logical groups. For example, if you have physical volumes consisting of the hard disk partitions hda2, hda3, hdb1, hdb2, and hdb3 on two hard disks, hda and hdb, you could assign some of them to one logical group and others to another logical group. The partitions making up the different logical groups can be from different physical hard drives. For example, hda2 and hdb3 could belong to the logical group turtle and hda3, hdb2, and hdb3 could make up a different logical group, say rabbit. The logical group name could be any name you want to give it. It is much like naming a hard drive.

Once you have your logical groups, you can then create logical volumes. Logical volumes function much like hard disk partitions on a standard setup. For example, on the turtle group volume, you could create a /var logical volume, and on the rabbit logical group, you could create a /home and a /projects logical volume. You can have several logical volumes on one logical group, just as you can have several partitions on one hard disk.

You treat the logical volumes as you would any ordinary hard disk partition. You create a file system on it with the mkfs command, and then you can mount the file system to use it with the mount command.

Storage on logical volumes is managed using what are known as extents. A logical group defines a standard size for an extent, say 4MB, and then divides each physical volume in its group into extents of that size. Logical volumes are, in turn, divided into extents of the same size, which are then mapped to those on the physical volumes.

There is one restriction and recommendation for logical volumes. The boot partition cannot be part of a logical volume. You still have to create a separate hard disk partition as your boot partition with the /boot mount point in which your kernel and all needed boot files are installed. In addition, it is recommended that you not place your / (root) partition on a logical volume. Doing so can complicate any needed data recovery.

### Creating LVMs with Disk Druid

Creating logical volumes involves several steps. First, you create physical LVM partitions, then the volume groups you place these partitions in, and then from the volume groups you create the logical volumes for which you then specify mount points and file system types. On Red Hat, you can create LVM partitions during the installation process using Disk Druid. In Disk Druid, click New and select 'physical volume (LVM)' for the File System Type. Create an LVM physical partition for each partition you want on your hard disks. Once you have created LVM physical partitions, you click the LVM button to create your logical volumes. You first need to assign the LVM physical partitions to volume groups. Volume groups are essentially logical hard drives. You could assign LVM physical partitions from different hard disks to the same volume group, letting the volume group span different hard drives. Once the volume groups are created, you are ready to create your logical volumes. You can create several logical volumes within each group. The logical volumes function like partitions. You will have to specify a file system type and mount point for each logical volume you create.

### LVM Tools

On Red Hat, you can create logical volumes either during the installation process, or later use a collection of LVM tools to manage your LVM volumes, adding new LVM physical partitions and removing current ones. LVM maintains configuration information in the /etc/lvmconf directory.

### Displaying LVM Information

You can use the pvdisplay, vgdisplay, and lvdisplay commands to show detailed information about a physical partition, volume groups, and logical volumes. pvscan, vgscan, and lvscan list your physical, group, and logical volumes.

### Managing LVM Physical Volumes

A physical volume can be any hard disk partition or RAID device. A RAID device is seen as a single physical volume. You can create physical volumes either from a single hard disk or from partitions on a hard disk. On very large systems with many hard disks, you would more likely use an entire hard disk for each physical volume.

To create a new physical volume, you initialize it with the pvcreate command with the partition's device name, as shown here.

```
pvcreate /dev/hda3
```

To initialize a physical volume on an entire hard disk, you use the hard disk device name, as shown here.

```
pvcreate /dev/hdc
```

Then use the vgextend command to add the partition to a logical group, in this case, rabbit. In effect, you are extending the size of the logical group by adding a new physical partition.

```
vgextend rabbit /dev/hda3
```

To remove a physical partition, first remove it from its logical volume. You may have to use the pvmove command to move any data off the physical partition. Then use the vgreduce command to remove it from its logical group.

### Managing LVM Groups

You can manually create a volume group using the vgcreate command and the name of the group along with a list of physical partitions you want in the group. The following example creates a group called rabbit consisting of three physical partitions, /dev/hda3, /dev/hdb4, and /dev/hdb4.

```
vgcreate rabbit /dev/hda3 /dev/hdb2 /dev/hdb4
```

You can remove a volume group by first deactivating it with the vgchange -a n operation and then using the vgreduce command.

### Activating Volume Groups

Whereas in a standard file system structure, you mount and unmount hard disk partitions, with an LVM structure, you activate and deactivate entire volume groups. The group volumes are accessible until you activate them with the vgchange command with the -a option. To activate a group, first reboot your system, and then enter the vgchange command with the -a option and the y argument to activate the logical group (an n argument will deactivate the group).

```
vgchange -a y rabbit
```

### Managing LVM Logical Volumes

To create logical volumes, you use the lvcreate command. With the -n option you specify the volume's name, which functions like a hard disk partition's label. You use the -L option to specify the size of the volume. The following example creates a logical volume named projects on the rabbit logical group with a size of 20GB.

```
lvcreate -n projects -L 2000M rabbit
```

You can remove a logical volume with the lvremove command. With lvextend, you can increase the size of the logical volume, and lvreduce will reduce its size.

### LVM Example

Using the example in Figure 31-2, the steps involved in creating and accessing logical volumes are described in following commands. First use a partition creation tool like fdisk or parted to create the physical partitions on the hard disks hda and hdb. In this example, you create the partitions hda1, hda2, hda3, hdb1, hdb2, hdb3, and hdb4.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_759_0.png)

Figure 31-2: Logical Volume Management

Then you initialize the physical volumes with the pvcreate command. The hda1 and hda2 partitions are reserved for the boot and root partitions and are not initialized.

```
pvcreate /dev/hda3 /dev/hdb1 /dev/hdb2
pvcreate /dev/hdb3 /dev/hdb4
```

You then create the logical groups you want using the vgcreate command. In this case, there are two logical groups, turtle and rabbit. The turtle group uses hdb1 and hdb3, and rabbit uses hda3, hdb2, and hdb4. If you create a physical volume later and want to add it to a volume group, you would use the vgextend command.

```
vgcreate turtle /dev/hdb1 /dev/hdb3
vgcreate rabbit /dev/hda3 /dev/hdb2 /dev/hdb4
```

You can now create the logical volumes in each volume group, using the lvcreate command.

```
lvcreate -n var -L 2000M turtle
lvcreate -n home -L 50000M rabbit
lvcreate -n projects -L 2000M rabbit
```
