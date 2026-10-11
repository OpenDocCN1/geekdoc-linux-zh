```
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
[root@server1 root]# _
```

![](bbox=[0.16, 0.34, 0.22, 0.38])

# **NOTE**

Alternatively, you can specify the filesystem mount point when using the dump command; the command `dump -0uf /dev/st0 /boot` is equivalent to the one used in the preceding example.

The contents of the `/etc/dumpdates` file now indicates that a full backup has taken place:

```
[root@server1 root]# cat /etc/dumpdates
/dev/hda2 0 Sat Jul 23 16:43:09 2005
[root@server1 root]# _
```

To perform the first incremental backup and view the contents of the `/etc/dumpdates` file, you can place a new tape into the SCSI tape drive and issue the following commands:

```
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
```