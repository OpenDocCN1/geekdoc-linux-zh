# Managing Filesystems
CHAPTER 18

| brw-rw---- | root | disk | 8, 13 Sep 12 | 1994 /dev/sda1 |
| brw-rw---- | root | disk | 8, 14 Sep 12 | 1994 /dev/sda14 |
| brw-rw---- | root | disk | 8, 15 Sep 12 | 1994 /dev/sda15 |
| brw-rw---- | root | disk | 8, 16 Sep 12 | 1994 /dev/sdb |

The obscure option (--sort-none) with only 1 command ensures that the devices are presented in correct order. If you use only 1, the entries are sorted alphabetically, and /dev/sda10 comes before /dev/sda2.

The b at the far left of the output of this command indicates that each of these entries is indicated by a c.) block device. (Character devices) The major and minor device numbers appear just before the time field, separated by commas.

# # Block Devices

If you had just one file of data to store, you could put it directly on a block device and read it back. Block devices have some fixed capacity, however, and you would need some method of marking the end of your data. Block devices behave in most respects just like ordinary files, except although an ordinary file has a length determined by how much data is in, the “length” of a block device is its total capacity. If you write a megabyte to a 100MB block device and read back its contents. In mind this restriction, several UNIX utilities encode the amount of data available in the file's data rather than the file's total length and, hence, are suitable for storing data directly on block devices—for example, tar and cpio, which are suitable for everybody, and dump, which is suitable only for the system administrator (because it requires access the block device using the data to be backed up). To back up the entire contents of your home directory to floppy disk, you type one of the following:

```
$ tar /dev/fd0 HOME
$ find HOME -print@ | cpio --create --format=crc >/dev/fd0
```

The tar command's cMF options are used to create a multiple-volume archive on the /dev/fd0, or floppy device. The -print@ and -0 options for find and cpio ensure that the names of the files to be backed up that find sends to cpio are separated by ASCII NULs, rather than newlines. This ensures that any filenames with a newline are correctly backed up.

![](bbox=[0.885, 0.455, 0.933, 0.595])