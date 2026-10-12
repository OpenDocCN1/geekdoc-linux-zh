If we check our new file command, we see this:

```
```
# file /tmp/fedoratest.img
/tmp/fedoratest.img: data
```
```

# ## Step 2—Make a File System

Now we need to make the system think that the file is a block device instead of an ASCII file, so we use losetup, a utility that associates loop devices with regular files or block devices; we will be using the loopback device, /dev/loop0.

```
```
# losetup /dev/loop0 /tmp/fedoratest.img
```
```

Now we can format the file as an ext2 file system:

```
```
# mkext2fs /dev/loop0
```
```

We see the computer respond as follows:

```
```
mke2fs 1.27 (8-Mar-2003)
File System label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
2512 inodes, 10000 blocks
500 blocks (5.00%) reserved for the super user
First data block=1
2 block groups
8192 blocks per group, 8192 fragments per group
1256 inodes per group
Superblock backups stored on blocks:
	8193

Writing inode tables: done
Writing superblocks and file system accounting information: done

This file system will be automatically checked every 21 mounts or 180 days, whichever comes first. Use tune2fs -c or -i to override.
```
```

# ## Step 3—Mount Our Test File System

After your test file system has been created, you can experiment with the different options for the formatting commands you will be using. It will be useful to make a mount point for our image file

```
```
# mkdir /mnt/image
```
```

and then mount it

```
```
# mount /dev/loop0 /mnt/image
```
```