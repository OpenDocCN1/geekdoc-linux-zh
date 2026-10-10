
# Working with the LVM

In the previous section, you learned how to create standard hard disk partitions on a MBR or GPT hard disk. You also learned how to create filesystems on those partitions and mount the filesystems to a directory within the Linux filesystem hierarchy.

Instead of creating and mounting filesystems that reside on standard partitions, you can use the **Logical Volume Manager (LVM)** to create volumes. These volumes can contain a filesystem and be mounted to directories within the Linux filesystem hierarchy. Using volumes to host filesystems is far more flexible than using standard partitions since it allows you to select free space from unused partitions across multiple hard disks in your computer. This free space is then pooled together into a single group from which volumes can be created. These volumes can then be formatted with a filesystem and mounted to a directory on the Linux filesystem hierarchy. Furthermore, additional hard disks can easily be added to the LVM, where existing volumes can take advantage of the additional storage space.

The LVM consists of several different components:

- **Physical Volumes (PVs)** are unused partitions on hard disks that the LVM can use to store information.
- **Volume Groups (VGs)** contain one or more PVs. They represent the pools of hard disk storage space that are available to the LVM for creating logical volumes. Additional PVs can easily be added to a VG after creation.
- **Logical Volumes (LVs)** are the usable volumes that are created by the LVM from the available storage space within a VG. LVs contain a filesystem and are mounted to a directory in the Linux filesystem hierarchy. In addition, LVs can be resized easily by the LVM to use more or less storage space.

The LVM subsystem in Linux manages the storage of all data that is saved to the LVM. The physical location of the data is transparent to the user. Furthermore, the LVM has error correction abilities that minimize the chance that data will become corrupted or lost. **Figure 5-8** illustrates the relationships among LVM components in a sample LVM configuration that creates four different PVs from the standard partitions on three different hard disks. These PVs are added to a VG that is divided into three LVs that are each mounted to a directory on the Linux filesystem hierarchy (*directory1, /directory2, and* directory3).

To configure the LVM, you must first create one or more PVs that reference an unused partition on a hard disk in your computer. Say, for example, that you recently created a new partition called /dev/sda4. Rather than placing a filesystem on /dev/sda4, you could instead allow the LVM to use the /dev/sda4 partition using the **pvcreate command**, as shown here:

```text
[root@server1 ~]# pvcreate /dev/sda4
Physical volume "/dev/sda4" successfully created
[root@server1 ~]# _
```

You should use the *pvcreate* command to create PVs for each unused partition that you wish to be used by the LVM. For simplicity in code output, we will only create a single PV in this section to demonstrate the configuration of LVM.

![](img/c27875544958897d817484d558c208c8_251_0.png)

The **pvdisplay** command can be used to display detailed information about each PV. The following pvdisplay command indicates that /dev/sda4 has 32 GB of available space:

```text
[root@server1 ~]# pvdisplay
"/dev/sda4" is a new physical volume of "32.00 GiB"
--- NEW Physical volume ---
PV Name                     /dev/sda4
VG Name
PV Size                     32.00 GiB
Allocatable                 NO
PE Size                     0
Total PE                    0
Free PE                     0
Allocated PE                0
PV UUID                     YZDmIG-0qFU-54AT-i0B6-bjKa-sHCc-i8IJo0
[root@server1 ~]# _
```

Once you have created PVs, you can create a VG that uses the space in the PVs using the **vgcreate command**. For example, to create a VG called *vg00* that uses the /dev/sda4 PV, you could use the following vgcreate command:

```text
[root@server1 ~]# vgcreate vg00 /dev/sda4
Volume group "vg00" successfully created
[root@server1 ~]# _
```

To create a VG that uses multiple PVs, simply add multiple device arguments to the **vgcreate command**. For example, the *vgcreate vg00 /dev/sda5 /dev/sdb1 /dev/sdc3* command would create a VG called *vg00* that uses three PVs (/dev/sda5, /dev/sdb1, and /dev/sdc3).

When creating a VG, it is important to choose the block size for saving data since it cannot be safely changed later. This is called the **physical extent (PE) size** of the VG. A large PE size results in larger write operations and a larger maximum filesystem size for LVs. For example, a PE size of 32MB will allow for a maximum LV size of 2TB.

By default, the *vgcreate* command chooses an appropriate PE size according to the current sizes of the PVs that are associated with the VG, but you can use the -s or -physicalextent size options to the *vgcreate* command to select a different PE size during VG creation.

The **vgdisplay** command can be used to display detailed information about each VG. The following *vgdisplay* example indicates that /dev/sda4 has over 31 GB of available space:

```text
[root@server1 ~]# vgdisplay
--- Volume group ---
VG Name                     vg00
System ID
Format                      lvm2
Metadata Areas              1
Metadata Sequence No        1
VG Access                   read/write
VG Status                   enabled
MAX LV                      0
Cur LV                      0
Open LV                     0
Max PV                      0
Cur PV                      1
Act PV                      1
VG Size                     32.00 GiB
PE Size                     4.00 MiB
Total PE                    8192
Alloc PE / Size             0 / 0
Free PE / Size              8192 / 32.00 GiB
VG UUID                     C2jrUC-LZmR-0tSX-bLqj-4350-8U7l-0ajugP
[root@server1 ~]# _
```

Next, you can create LVs from the available space in your VG using the *lvcreate* command and view your results using the *lvdisplay* command. The following commands

![](img/c27875544958897d817484d558c208c8_252_0.png)

## Chapter 5 Linux Filesystem Administration

create an LV called "data" that uses 15GB of space from vg00 as well as an LV called "extras" that uses 16GB of space from vg00, and it displays the results.

```text
[root@server1 ~]# lvcreate -L 15GB -n data vg00
Logical volume "data" created
[root@server1 ~]# lvcreate -L 16GB -n extras vg00
Logical volume "extras" created
[root@server1 ~]# lvdisplay

--- Logical volume ---
LV Path                     /dev/vg00/data
LV Name                     data
VG Name                     vg00
LV UUID                     hMCr4Z-JNr0-lVCf-5S2K-8Ujg-B0ri-Am3isi
LV Write Access             read/write
LV Creation host, time      localhost.localdomain, 2015-11-25 07:42:30
LV Status                   available
# open                  0
LV Size                     15.00 GiB
Current LE                  3840
Segments                    1
Allocation                  inherit
Read ahead sectors          auto
- currently set to 256
Block device                253:0

--- Logical volume ---
LV Path                     /dev/vg00/extras
LV Name                     extras
VG Name                     vg00
LV UUID                     yUH5xW-U8lB-CD3t-N22K-70gD-xHpm-TTHQca
LV Write Access             read/write
LV Creation host, time      localhost.localdomain, 2015-11-25 07:42:44
LV Status                   available
# open                  0
LV Size                     16.00 GiB
Current LE                  4096
Segments                    1
Allocation                  inherit
Read ahead sectors          auto
- currently set to 256
Block device                253:1
[root@server1 ~]#
```

Notice from the preceding output that the new VGs can be accessed using the device files /dev/vg00/data and /dev/vg00/extras. You can also refer to your new VGs using the device files /dev/mapper/vg00-data and /dev/mapper/vg00-extras, which are typically used by the system when accessing the filesystems on your VGs.

You can work with these files as you would normally work with any other hard disk partition device file. For example, to create an ext4 filesystem on these devices and mount them to the appropriate directories on the filesystem, you could use the following commands:

```text
[root@server1 ~]# mke2fs -t ext4 /dev/vg00/data
mke2fs 1.42.8 (20-Jun-2013)
Filesystem label=
OS type:            Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
983040 inodes, 3932160 blocks
196608 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=4026531840
120 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208

Writing inode tables:     done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information:     done
```

```text
[root@server1 ~]# mke2fs -t ext4 /dev/vg00/extras
mke2fs 1.42.8 (20-Jun-2013)
Filesystem label=
OS type:            Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
1048576 inodes, 4194304 blocks
209715 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=4194304
128 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 4096000

Writing inode tables:     done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information:     done
```

```text
[root@server1 ~]# mkdir /data
[root@server1 ~]# mkdir /extras
[root@server1 ~]# mount /dev/vg00/data /data
```
