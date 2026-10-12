
drive. These physical devices are mounted at specific mount points on the Linux file system. For example, the DVD/CD-ROM drive, `/dev/cdrom`, is mounted on `/mnt/cdrom` in the file system. After mounting the CD-ROM in this way, the Fedora directory on a CD-ROM or DVD-ROM appears as `/mnt/cdrom/Fedora` in the Linux file system.

![](img/9f89727199836b0f871f1745838aa8b2_467_0.png)

You can use the `mount` command to manually mount a device on the Linux file system at a specified directory. That directory is the *mount point*. For example, to mount the DVD/CD-ROM drive at `/mnt/cdrom` directory, you type the following command (after logging in as `root`):

```
mount /dev/cdrom /mnt/cdrom
```

The `mount` command reports an error if the DVD/CD-ROM device is mounted already or if no CD or DVD media is in the drive. Otherwise, the `mount` operation succeeds, and you can access the DVD or CD’s contents through the `/mnt/cdrom` directory.

You can use any directory as the mount point. If you mount a device on a nonempty directory, however, you cannot access the files in that directory until you unmount the device by using the `umount` command. Therefore, always use an empty directory as the mount point.

Fedora Core comes with the `/mnt/cdrom` directory for mounting DVDs or CDs and `/mnt/floppy` for mounting floppy drives.

To unmount a device when you no longer need it, use the **umount** command. For example, to unmount the DVD/CD-ROM device, type

```
umount /dev/cdrom
```

The **umount** command succeeds as long as no one is using the DVD/CD-ROM. If you get an error when trying to unmount the DVD/CD-ROM, check to see whether the current working directory is on the DVD or CD. If you’re currently working in one of the DVD/CD-ROM’s directories, that also qualifies as a use of the DVD/CD-ROM.

## Examining the */etc/fstab* file

The **mount** command has the following general format:

```
mount *device-name* *mount-point*
```

However, you can mount the CD-ROM by typing one of the following commands:

```
mount /dev/cdrom
mount /mnt/cdrom
```

![](img/9f89727199836b0f871f1745838aa8b2_468_0.png)

You can mount by specifying only the CD-ROM device name or the mount-point name because of what’s in a file named **/etc/fstab**. A line in the **/etc/fstab** file for the **/mnt/cdrom** mount **point**. That entry specifies the CD-ROM device name and the **file-system type**. That’s why you can mount the CD-ROM with a shorter **mount** command.

The **/etc/fstab** file is a *configuration file* — a text file containing information that the **mount** and **umount** commands use. Each line in the **/etc/fstab** file provides information about a device and its mount point in the Linux file system. Essentially, the **/etc/fstab** file associates various mount points within the file system with specific devices, which enables the **mount** command to work from the command line with only the mount point or the device as argument.

Here is a **/etc/fstab** file from a Fedora Core system:

| File system | Mount point | Type | Options | Dump | Pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| LABEL=/ | /boot | ext3 | defaults | 1 | 1 |
| /dev/p | /dev/pts | devpts | gid=5,mode=620 | 0 | 0 |
| none | /dev/shm | tmpfs | defaults | 0 | 0 |
| none | /proc | proc | defaults | 0 | 0 |
| none | /sys | sysfs | defaults | 0 | 0 |
| /dev/hda6 | swap | swap | defaults | 0 | 0 |
| /dev/cdrom | /mnt/cdrom | udf,iso9660 | noauto,owner,kudzu,ro | 0 | 0 |
| /dev/fd0 | /dev/floppy | auto | noauto,owner,kudzu | 0 | 0 |
| /dev/cdrom1 | /mnt/cdrom1 | udf,iso9660 | noauto,owner,kudzu,ro | 0 | 0 |

The first field on each line shows a device name, such as a hard-drive partition (or it identifies a partition by a LABEL keyword). The second field is the mount point, and the third field indicates the type of file system on the device. You can ignore the last three fields for now.

This /etc/fstab file shows that the /dev/hda6 device (the second logical partition on the first IDE hard drive) functions as a swap device for virtual memory, which is why both the mount point and the file-system type are set to swap.

![](img/9f89727199836b0f871f1745838aa8b2_469_0.png)

The Linux operating system uses the contents of the /etc/fstab file to mount various file systems automatically. During Fedora Core startup, the init process executes a shell script that runs the `mount -a` command. That command reads the /etc/fstab file and mounts all listed file systems (except those with the `noauto` option). The third field on each line of /etc/fstab specifies the type of file system on that device and the fourth field shows a comma-separated list of options that the `mount` command uses when mounting that device on the file system. Typically, you find the `defaults` option in this field. The `defaults` option implies — among other things — that the device mounts at boot time; that only the `root` user can mount the device; and that the device mounts for both reading and writing. If the options include `noauto`, the device doesn't mount automatically as the system boots.

![](img/9f89727199836b0f871f1745838aa8b2_469_1.png)

The `kudzu` option in the fourth field of /etc/fstab entries indicates that these lines were added to the fstab file by the kudzu hardware-detection utility — kudzu runs the `udpfstab` command to add an entry in the /etc/fstab file for each removable drive it detects. You typically find that the entries for DVD/CD-ROM drives (/dev/cdrom and /dev/cdrom1) and the floppy drive (/dev/fd0) have the `kudzu` option in the fourth field. On a PC with an IDE Zip drive, for instance, the /etc/fstab file has another entry set up by kudzu that associates the /mnt/zip mount point with the Zip drive device (/dev/hdd4), as follows:

```
    /dev/hdd4 /mnt/zip auto noauto,owner,kudzu 0 0
```

## Sharing Files with NFS

Sharing files through the Network File System (NFS) is simple and involves two basic steps:

-   On the NFS server, export one or more directories by listing them in the `/etc/exports` file and by running the `/usr/sbin/exportfs` command. In addition, you must run the NFS server (you can do so by logging in as `root` and typing `service nfs start`).
-   On each client system, use the `mount` command to mount the directories the server has exported.

The only problem in using NFS is that each client system must support it. Most PCs don't come with NFS — that means you have to buy NFS software separately if you want to share files by using NFS. If, however, all systems on your LAN run Linux (or other variants of UNIX with built-in NFS support), using NFS makes sense.

![](img/9f89727199836b0f871f1745838aa8b2_470_0.png)

Note: NFS has security vulnerabilities. Therefore do not set up NFS on systems directly connected to the Internet.

In the upcoming section, I walk you through an NFS setup, using an example of two Linux PCs on a LAN.

### Exporting a file system with NFS

Start with the server system that exports — makes available to the client systems — the contents of a directory. On the server, you must run the NFS service and also designate one or more file systems to be exported, or made available to the client systems.

To export a file system, you have to add an appropriate entry to the `/etc/exports` file. For example, suppose you want to export the `/home` directory and you want to enable the host named LNB75 to mount this file system for read-and-write operations (you can use a host's IP address in place of the host name). You can do so by adding the following entry to the `/etc/exports` file:

```
/home LNB75(rw)
```

After adding the entry in the `/etc/exports` file, manually export the file system by typing `/usr/sbin/exportfs -a` in a terminal window. This command exports all file systems defined in the `/etc/exports` file.

Now start the NFS server — log in as `root` and type the following command in a terminal window:

```
service nfs start
```

To restart the NFS service, type `service nfs restart`.

When the NFS service is up, the server side of NFS is ready. Now you can try to mount the exported file system from a client system and access the exported file system.

![](img/9f89727199836b0f871f1745838aa8b2_470_1.png)

If you ever make any changes to the exported file systems listed in the `/etc/exports` file, remember to restart the NFS service. To do so, type `service nfs restart` in a terminal window.
