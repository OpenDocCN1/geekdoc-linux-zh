5. There are a variety of different options to the mke2fs command worth exploring in Table 10.1.

# TABLE 10.1 Useful Flags to mke2fs

| Flag | Meaning |
|---|---|
| `-b blocks` | Specify a different block size than the default. Valid sizes are 1024, 2048, and 4096 bytes. |
| `-c` | Check the disk for bad blocks before formatting the filesystem. |
| `-j` | Enable a journaling option on an ext3 disk. |
| `-L label` | Set the volume label for the disk. |
| `-N i` | Specify that the disk should have i inodes rather than the default. |
| `-v` | Verbose output, showing you more of what's going on. |

![](bbox=[0.15, 0.64, 0.25, 0.74])

> > To learn more about the cool new ext3 filesystem and its disk journaling capability, please visit http://www.redhat.com/support/wpapers/redhat/ext3/.

Before we leave this section, let's use the command flags to rebuild the filesystem on the new drive to support lots more tiny files by upping the inodes available. While we're at it, we'll also specify a volume label.

```
# mke2fs -l 'Little Guy' -v -N 128000 /dev/hdb
mke2fs 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
/dev/hdb is entire device, not just one partition!
Proceed anyway? (y,n) y
Filesystem label=Little Guy
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
128000 inodes, 255528 blocks
12776 blocks (5.00%) reserved for the super user
First data block=1
32 block groups
8192 blocks per group, 8192 fragments per group
4000 inodes per group
Superblock backups stored on blocks:
8193, 24577, 40961, 57345, 73729, 204801, 221185

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 37 mounts or 100 days, whichever comes first. Use tune2fs -c or -i to override.
```