| Disk Partition | Size (MB/GB) | Size (512-byte blocks) | File System Type | File System |
|---|---|---|---|---|
| a | 512 MB | 1048576 | AdvFS | / |
| b | 4.5 GB | 9437184 | swap | swap |
| e | 3.9 GB | 8302104 | unused | unused |
| f | 2 GB | 4194304 | AdvFS | /tmp* |
| g | 4 GB | 8388608 | AdvFS | /usr |
* - See Chapter 21 on configuring a separate /tmp file system.

# Table 4-2: Example Disk Partition Sizes

clicking on the "Edit Partitions..." button on the Custom File System Layout box to open the Disk Configuration application. See Figure 4-1 for an example.

The Disk Configuration application can also be run outside of the Tru64 UNIX Installation program by executing the command /usr/sbin/diskconfig. For more information on the diskconfig(8) command, please see its reference page.

# 4.2.1.2.3 The Disk Label After the Tru64 UNIX Installation

Using our example, after the Full Installation of Tru64 UNIX, the disk label for our new system disk should look something like this:

```
# disklabel dak0 | grep -p "8 part"
# partitions:
# size offset fstype fsize bsize cpg # -Cyl values
 a: 1048576 0 AdvFS 0 0 # 0 - 206*
 b: 9437184 1048576 swap 0 0 # 206* - 1857*
 c: 35565080 0 unused 0 0 # 0 - 7000
 d: 0 0 unused 0 0 # 0 - 0
 e: 8302104 10485760 unused 0 0 # 1857* - 3491*
 f: 4194304 18787864 unused 0 0 # 3491* - 4316*
 g: 8388608 22982168 AdvFS 0 0 # 4316* - 5967*
 h: 4194304 31370776 AdvFS 0 0 # 5967* - 7000
```

Notice that disk partitions "e" and "f" still have an fstype of unused. At this time, we have only "prepared" the disk to have a separate /tmp file system. See Chapter 21 on creating a cluster member's /tmp as a separate file system.