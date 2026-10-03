swap partition, make an entry in the /etc/vfstab file so that the swap space is activated at bootup. The process is described next.

# STEP BY STEP

# 14.2 Creating a Secondary Swap File

1. You need to add an additional 175MB of swap space to your system. You don’t have any more room on the disk for more swap space, but the /data directory (currently mounted on slice 5) is 200MB in size. Move all the data in /data to another server to free up the partition so you can use it as a swap partition. You can use any one of the methods described in Chapter 11, “Backup and Recovery,” to do this.

2. After freeing up the /data directory and unmounting /dev/dsk/c0t0d0s5, use the format utility to set the tag name to swap and the permission flag to wu (writable and unmountable) as follows:

```
partition> 5
```

```
Part    Tag        Flag  Cylinders  Size     Block
5    unassigned  wm    3400 - 3833  200.26MB \
(434/0/0)  410130
```

```
Enter partition id tag[unassigned]: swap
Enter partition permission flags[wm]: wu
Enter new starting cyl[3400]: <return>
Enter partition size[410130b, 434c, 200.26mb, \
0.20gb]: <return>
```

I then label the disk as follows:

```
Partition> la
Ready to label disk? y
```

3. Run the newfs command on that partition to remove all data and create a fresh file system on slice 5 as follows:

```
newfs /dev/rdsk/c0t0d0s5
```