# Working with the LVM

In the previous section, you learned how to create standard hard disk partitions on a MBR or GPT hard disk. You also learned how to create filesystems on those partitions and mount the filesystems to a directory within the Linux filesystem hierarchy.

Instead of creating and mounting filesystems that reside on standard partitions, you can use the **Logical Volume Manager (LVM)** to create volumes. These volumes can contain a filesystem and be mounted to directories within the Linux filesystem hierarchy. Using volumes to host filesystems is far more flexible than using standard partitions since it allows you to select free space from unused partitions across multiple hard disks in your computer. This free space is then pooled together into a single group from which volumes can be created. These volumes can then be formatted with a filesystem and mounted to a directory on the Linux filesystem hierarchy. Furthermore, additional hard disks can easily be added to the LVM, where existing volumes can take advantage of the additional storage space.

The LVM consists of several different components:

+   *   **Physical Volumes (PVs)** are unused partitions on hard disks that the LVM can use to store information.

+   *   **Volume Groups (VGs)** contain one or more PVs. They represent the pools of hard disk storage space that are available to the LVM for creating logical volumes. Additional PVs can easily be added to a VG after creation.

+   *   **Logical Volumes (LVs)** are the usable volumes that are created by the LVM from the available storage space within a VG. LVs contain a filesystem and are mounted to a directory in the Linux filesystem hierarchy. In addition, LVs can be resized easily by the LVM to use more or less storage space.

The LVM subsystem in Linux manages the storage of all data that is saved to the LVM. The physical location of the data is transparent to the user. Furthermore, the LVM has error correction abilities that minimize the chance that data will become corrupted or lost. **Figure 5-8** illustrates the relationships among LVM components in a sample LVM configuration that creates four different PVs from the standard partitions on three different hard disks. These PVs are added to a VG that is divided into three LVs that are each mounted to a directory on the Linux filesystem hierarchy (*directory1, /directory2, and* directory3).

To configure the LVM, you must first create one or more PVs that reference an unused partition on a hard disk in your computer. Say, for example, that you recently created a new partition called /dev/sda4. Rather than placing a filesystem on /dev/sda4, you could instead allow the LVM to use the /dev/sda4 partition using the **pvcreate command**, as shown here:

```
```text
[root@server1 ~]# # pvcreate /dev/sda4
Physical volume "/dev/sda4" successfully created
[root@server1 ~]# _
```
```

You should use the *pvcreate* command to create PVs for each unused partition that you wish to be used by the LVM. For simplicity in code output, we will only create a single PV in this section to demonstrate the configuration of LVM.