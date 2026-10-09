Sparse files never shrink. They can only grow. If you erase a bunch of files from your disk image, the image file still needs that space.

Also, not all filesystems support sparse files. UFS and ZFS do. If you're trying to create a sparse file on a FAT32 filesystem, you're probably solving the wrong problem.

# Creating the Filesystem on the File

To get a filesystem on the file, first associate the file with a device with a vnode-backed memory disk. We did exactly this in the last section:

```
```
# mdconfig -a -t vnode -f filesystem.file
md0
```
```

Now, let's make a filesystem on this device. This is much like creating a UFS filesystem on a thumb disk with the newfs(8) command. Soft updates journaling is exactly as useful on file-backed filesystems as on disk-backed ones, so enable them with -j.

```
```
# newfs -j /dev/md0
/dev/md0: 1024.0MB (2097152 sectors) block size 32768, fragment size 4096
        using 4 cylinder groups of 256.03MB, 8193 blks, 32896 inodes.
          with soft updates
super-block backups (for fsck_ffs -b #) at:
 192, 524544, 1048896, 1573248
Using inode 4 in cg 0 for 8388608 byte journal
newfs: soft updates journaling set
```
```

The newfs(8) program prints out basic information about the disk, such as its size, block and fragment sizes, and the inode count.

Now that you have a filesystem, mount it:

```
```
# mount /dev/md0 /mnt
```
```

Congratulations! You now have a 1GB file-backed filesystem. Copy files to it, dump it to tape, or use it in any way you would use any other filesystem. But in addition to that, you can move it just like any other file.

# File-Backed Filesystems and /etc/fstab