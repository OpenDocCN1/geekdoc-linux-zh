# Setup for automatic mounting

By default, ZFS filesystems mount themselves automatically and do not require **vfstab** entries. However, you can change this behavior by setting ZFS filesystem properties. Swap areas and nonfilesystem mounts should still appear in **vfstab**.

**mount**, **umount**, **swapon**, and **fsck** all read the filesystem catalog, so it is helpful if the data presented there is correct and complete. You might also want to use the catalog to figure out what you want done if you specify only a partition name or mount point on the command line. For example, with the Linux **fstab** configuration shown on page 262, the command

```
$ sudo mount /media/cdrom0
```

would have the same effect as typing

```
$ sudo mount -t udf -o user,noauto,exec,utf8 /dev/scd0 /media/cdrom0
```

The command **mount -a** mounts all regular filesystems listed in the filesystem catalog; it is usually executed from the startup scripts at boot time.²⁰ The **-t**, **-F**, or **-v** flag (**-t** for Linux, **-F** for Solaris and HP-UX, **-v** for AIX) with an *fstype* argument constrains the operation to filesystems of a certain type. For example,

```
$ sudo mount -at ext4
```

mounts all local ext4 filesystems. The **mount** command reads **fstab** sequentially. Therefore, filesystems that are mounted beneath other filesystems must follow their parent partitions in the **fstab** file. For example, the line for **/var/log** must follow the line for **/var** if **/var** is a separate filesystem.

The **umount** command for unmounting filesystems accepts a similar syntax. You cannot unmount a filesystem that a process is using as its current directory or on which files are open. There are commands to identify the processes that are interfering with your **umount** attempt; see page 144.

The HP-UX **fstab** file is the most traditional of our example systems. Here are entries for a system that has only a single volume group:

| # Device | Mount point | Type | Options | Seq |
|---|---|---|---|---|
| /dev/vg00/lvol3 | / | vxfs | delaylog | 0 1 |
| /dev/vg00/lvol1 | /stand | vxfs | tranflush | 0 1 |
| /dev/vg00/lvol4 | /tmp | vxfs | delaylog | 0 2 |
| /dev/vg00/lvol5 | /home | vxfs | delaylog | 0 2 |
| /dev/vg00/lvol6 | /opt | vxfs | delaylog | 0 2 |
| /dev/vg00/lvol7 | /usr | vxfs | delaylog | 0 2 |
| /dev/vg00/lvol8 | /var | vxfs | delaylog | 0 2 |

There are six fields per line, separated by whitespace. Each line describes a single filesystem. The fields are traditionally aligned for readability, but alignment is not required.