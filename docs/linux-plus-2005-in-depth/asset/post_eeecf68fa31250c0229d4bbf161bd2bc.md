
up the data that has been changed since the last backup. In the case of a system failure, you can restore the information from the full backup and then restore the information from all subsequent incremental backups in sequential order. You can perform up to nine different incremental backups using the *dump/restore* utility; number 0 represents a full backup, whereas numbers 1 through 9 represent incremental backups.

Suppose, for example, that you perform a full backup of the */dev/hda3* filesystem on Sunday, perform incremental backups from Monday to Wednesday, and on Thursday the */dev/hda3* filesystem becomes corrupted, as depicted in Figure 12-1.

![](img/09bf13b782f71165e17bb3839040c96a_483_0.png)

After the filesystem has been re-created, you should restore the full backup (0) followed by the first incremental backup (1), the second incremental backup (2), and the third incremental backup (3) to ensure that data has been properly recovered.

The *dump/restore* utility has many options available to it, as do the *tar* and *cpio* utilities. Table 12-7 provides a list of these options.

**Table 12-7 Common options used with the dump/restore utility**

| Option | Description |
| --- | --- |
| -# | Specifies the type of backup when used with the dump command; if # is 0, a full backup is performed. If # is 1 through 9, the appropriate incremental backup is performed. |
| -b NUM | Specifies a certain block size to use in Kilobytes; the default block size is 10 Kilobytes. |
| -i *FILENAME* | Specifies the pathname to the archive; the *FILENAME* can be a file on a filesystem or a device file. |
| -u | Specifies to update the */etc/dumpdates* file after a successful backup. |
| -n | Notifies the user if any errors occur and when the backup has completed. |
| -r | Extracts an entire archive when used with the restore command. |
| -x *FILENAME* | Extracts a certain file or files represented by *FILENAME* when used with the restore command. |
| -i | Restores files interactively, prompting the user for confirmation for all actions, when used with the restore command. |
| -t | Lists the filename contents (table of contents) of an existing archive when used with the restore command. |
| -v | Displays verbose output (file and directory information) when manipulating archives. |

Take, for example, the output from the following df command:

```bash
[root@server1 root]# df
Filesystem            1K-blocks     Used Available Use% Mounted on
/dev/hda3               4032124  2840560    986736   75% /
/dev/hda2                10107    10550     85336  12% /boot
none                    192232       0    192232   0% /dev/shm
[root@server1 root]# 
```

To perform a full backup of the /boot partition (/dev/hda2) to the first rewinding SCSI tape device and update the */etc/dumpdates* file when completed, you can issue the following command:

```bash
[root@server1 root]# dump -0uf /dev/st0 /dev/hda2
DUMP: Date of this level 0 dump: Sat Jul 23 16:43:09 2005
DUMP: Dumping /dev/hda2 (/boot) to /dev/st0
DUMP: Excluding ext3 journal inode 8
DUMP: Label: /boot
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 6485 tape blocks.
DUMP: Volume 1 started with block 1 at: Sat Jul 23 16:43:10 2005
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: Closing /dev/st0
DUMP: Volume 1 completed at: Sat Jul 23 16:43:11 2005
DUMP: Volume 1 6470 tape blocks (6.32MB)
DUMP: Volume 1 took 0:00:01
DUMP: Volume 1 transfer rate: 6470 kB/s
DUMP: 6470 tape blocks (6.32MB) on 1 volume(s)
DUMP: finished in 1 seconds, throughput 6470 kB/bytes/sec
DUMP: Date of this level 0 dump: Sat Jul 23 16:43:09 2005
DUMP: Date this dump completed: Sat Jul 23 16:43:11 2005
DUMP: Average transfer rate: 6470 kB/s
DUMP: DUMP IS DONE
[root@server1 root]# 
```

![](img/09bf13b782f71165e17bb3839040c96a_485_0.png)

**NOTE**

Alternatively, you can specify the filesystem mount point when using the dump command; the command `dump -0uf /dev/st0 /boot` is equivalent to the one used in the preceding example.

The contents of the `/etc/dumpdates` file now indicates that a full backup has taken place:

```bash
[root@server1 root]# cat /etc/dumpdates
/dev/hda2 0 Sat Jul 23 16:43:09 2005
[root@server1 root]# 
```

To perform the first incremental backup and view the contents of the `/etc/dumpdates` file, you can place a new tape into the SCSI tape drive and issue the following commands:

```bash
[root@server1 root]# dump -1uf /dev/st0 /dev/hda2
DUMP: Date of this level 1 dump: Sat Jul 23 16:50:57 2005
DUMP: Date of last level 0 dump: Sat Jul 23 16:43:09 2005
DUMP: Dumping /dev/hda2 (/(boot)) to /dev/st0
DUMP: Exclude ext3 journal inode 8
DUMP: Label: /boot
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 21 tape blocks.
DUMP: Volume 1 started with block 1 at: Sat Jul 23 16:50:58 2005
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: Closing /dev/st0
DUMP: Volume 1 completed at: Sat Jul 23 16:50:58 2005
DUMP: Volume 1 20 tape blocks (0.02MB)
DUMP: 20 tape blocks (0.02MB) on 1 volume(s)
DUMP: finished in less than a second
DUMP: Date of this level 1 dump: Sat Jul 23 16:50:57 2005
DUMP: Date this dump completed: Sat Jul 23 16:50:58 2005
DUMP: Average transfer rate: 0 kB/s
DUMP: DUMP IS DONE
[root@server1 root]# 
```

To view the contents of an archive, you can specify the -t option to the restore command followed by the archive information. To view the contents of the full backup performed earlier, you can place the appropriate tape into the tape drive and execute the following command:

```bash
[root@server1 root]# restore -tf /dev/st0
Dump   date: Sat Jul 23 16:43:09 2005
Dumped from: the epoch
Level 0 dump of /boot on localhost.localdomain:/dev/hda2
Label: /boot
  2               .
 11              ./lost+found
4033             ./. grub
4035             ./grub/grub.conf
4034             ./grub/splash.xpm.gz
4036             ./grub/menu.lst
4037             ./grub/device.map
4038             ./grub/stage1
4039             ./grub/stage2
4040             ./grub/e2fs_stage1_5
4041             ./grub/fat_stage1_5
4042             ./grub/ffs_stage1_5
4043             ./grub/reiserfs_stage1_5
4044             ./grub/vstafs_stage1_5
4045             ./grub/xfs_stage1_5
 12              ./boot.b
 13              ./chain.b
 14              ./config-2.6.5-1.358
 15              ./initrd-2.6.5-1.358.img
 17              ./memtest86+-1.11
 19              ./os2_d.b
 22              ./System.map-2.6.5-1.358
 20              ./vmlinuz-2.6.5-1.358
[root@server1 root]# 
```

To extract the full backup shown in the preceding output, you can specify the `-r` option to the `restore` command followed by the archive information. In addition, you can specify the `-v` option to list the filenames restored, as shown in the following example:

```bash
[root@server1 root]# restore -vrf /dev/st0
Verify tape and initialize maps
Input is from file/pipe
Input block size is 32
Dump date: Sat Jul 23 16:43:09 2005
Dumped from: the epoch
Level 0 dump of /boot on localhost.localdomain:/dev/hda2
Label: /boot
Begin level 0 restore
Initialize symbol table.
Extract directories from tape
Calculate extraction list.
restore: ../lost+found: File exists
restore: ../grub: File exists
Extract new leaves.
Check pointing the restore
extract file ./.boot.b
extract file ./.chain.b
extract file ./.config-2.6.5-1.358
extract file ./.initrd-2.6.5-1.358.img
extract file ./.mtemtest86+-1.11
extract file ./.os2_d.b
extract file ./.System.map-2.6.5-1.358
extract file ./.vmlinuz-2.6.5-1.358
extract file ./.grub/grub.conf
extract file ./.grub/splash.xpm.gz
extract file ./.grub/menu.lst
extract file ./.grub/device.map
extract file ./.grub/stage1
extract file ./.grub/stage2
extract file ./.grub/e2fs_stage1_5
extract file ./.grub/fat_stage1_5
extract file ./.grub/ffs_stage1_5
extract file ./.grub/reiserfs_stage1_5
extract file ./.grub/vstafs_stage1_5
extract file ./.grub/xfs_stage1_5
Add links
Set directory mode, owner, and times.
Check the symbol table.
Check pointing the restore
[root@server1 root]# 
```
