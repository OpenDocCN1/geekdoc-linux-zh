4. Use the fdisk command to create partitions on the new disk. For example, if you are
formatting the second hard disk (sdb), you could type the following:

```
# fdisk /dev/sdb
```

5. If the disk had existing partitions on it, you can change or delete those partitions now. Or,
y can simply reformat the whole disk to blow everything away. Use p to view all
partitions and d to delete a partition.

6. To create a new partition, type the following:

```
n
```

You are asked to choose an extended or primary partition.

7. To choose a primary partition, type the following:

```
p
```

You are asked to the partition number.

8. If you are creating the first partition (or for only one partition), type the number 1:

```
1
```

You are asked to enter the first cylinder number (with 1 being the default).

9. To begin the second cylinder, type the number 2 as follows:

```
2
```

You are asked to enter the last cylinder.

10. If you are using the entire hard disk, use the last cylinder number shown. Otherwise,
choose the ending cylinder number or indicate how many megabytes the partition should
have.

11. To create more partitions on the hard disk, repeat Steps 6 through 10 for each partition.
You will need to change the partition number, cylinder numbers, and so on as
appropriate.

12. Type w to write changes to the hard disk. At this point, you should be back at the shell.

13. To make a file system on the new disk, use the mkfs command. By default, this
command creates an ext2 file system, which is usable by Linux. To create an ext3 file
system on the first partition of the second hard disk, type the following:

```
# mkfs -t ext3 /dev/sdb1
```

If you created multiple partitions, repeat this step for each partition (such as
/dev/sdb2, /dev/sdb3, and so on).