# 78 Part II: Installing SuSE Linux

If you plan to have more than four partitions on your hard drive, you need to create an extended partition. Inside the extended partition, you can create multiple logical partitions. The need for this arrangement of creating one large, extended partition with multiple logical partitions inside it is not a limitation of Linux, but rather a limitation of modern hardware. As far as Linux is concerned, the logical partitions do not function any differently than primary partitions.

Next you are prompted with a list of the available partitions, and you should select the one on the top of the list. This is example, in Figure 5-10, the first available partition is /dev/hda2 If you were creating a logical partition, it would be /dev/hda6. When you have selected the partition you want to create, press Enter.

In the Location of Partition dialog box (see Figure 5-10), you need to enter the size of the partition that you are creating. The starting and ending values that appear automatically are the first and last cylinders of the unpartitioned portion of your hard drive.

In Figure 5-11, you can see that we have created a 750MB partition by specifying that value (750 MB) in the ending cylinder field. After you have specified the size of the partition that you are creating, press Enter and the partition that you just created in the list of current partitions. You create each of your partitions in this fashion. Note that, by default, the partition type is set to Linux native.

```
-EDITING THE PARTITION TABLE-
Fdisk detected the following hard drive geometry:
Disk /dev/hda 64 cylinders
One cylinder has 63 sectors The following primary partitions are:
table start end size in your partition
Message here you can see Please type the size you want.
/dev/hda2
/dev/hda1
Current partition
Device name
/dev/hda1
< Continue >          Abort
```
```

Figure 5-10: Location of partition.

If you make a mistake, don't worry! You have not committed (saved) the partition information yet, and you can easily delete the partitions that you have created. Read on . . .