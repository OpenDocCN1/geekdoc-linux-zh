```
# fsck -y -C /dev/sda5
```

The -y option will automatically answer Yes to repair file system errors. Otherwise, if you do have any errors, you will find yourself hitting Y over and over again. The -c option gives you a nice progress bar so you can see how far along fsck is. A complete fsck can take some time on a large file system, so the progress bar can be handy.

Sometimes file systems are so corrupted that the primary superblock cannot be found. Luckily, file systems create backup superblocks in case this happens, so you can tell fsck to use this superblock instead. Now I don't expect you to automatically know the location of your backup superblock. You can use the mke2fs tool with the -n option to list all of the superblocks on a file system.

> NOTE Warning
> Be sure to use the -n option here! Otherwise mke2fs will simply format your file system and erase all of your old data.

```
# mke2fs -n /dev/sda5
```

Once you see the list of superblocks in the output, choose one and pass it as an argument to the -b option for fsck:

```
# fsck -b 8193 -y -C /dev/sda5
```

When you specify an alternate superblock, fsck will automatically update your primary superblock after it completes the file system check.

# Fstab Mistakes or UUID Changed

Another common problem you might face is that a file system won't mount because of a mistake in your /etc/fstab file. It might be that you migrated a file system from one partition to another and forgot to update its UUID in /etc/fstab. If this happens for the root partition, the same steps apply, but you will likely have to either run the commands from a rescue CD or edit the GRUB prompt at