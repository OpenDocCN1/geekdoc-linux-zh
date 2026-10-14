
uhelper=hal,uid=500,utf8,shortname=lower)
twin4:/musicbox on /misc/musicbox type nfs4 (rw,addr=192.168.1.4)

The format of the listing is: device on mount_point type file_system_type (options). For example, the first line shows that device /dev/sda2 is mounted as the root file system, is of type ext3, and is both readable and writable (the option “rw”). This listing also has two interesting entries at the bottom of the list. The next-to-last entry shows a 2 gigabyte SD memory card in a card reader mounted at /media/disk, and the last entry is a network work drive mounted at /misc/musicbox.

For our first experiment, we will work with a CD-ROM. First, let's look at a system before a CD-ROM is inserted:

```
[me@linuxbox ~]$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext3 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/hda1 on /boot type ext3 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
```

This listing is from a CentOS 5 system, which is using LVM (Logical Volume Manager) to create its root file system. Like many modern Linux distributions, this system will attempt to automatically mount the CD-ROM after insertion. After we insert the disc, we see the following:

```
[me@linuxbox ~]$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext3 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/hda1 on /boot type ext3 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/hdc on /media/live-1.0.10-8 type iso9660 (ro,noexec,nosuid,
nodev,uid=500)
```

After we insert the disc, we see the same listing as before with one additional entry. At the end of the listing we see that the CD-ROM (which is device /dev/hdc on this system) has been mounted on `/media/live-1.0.10-8`, and is type iso9660 (a CD-ROM). For purposes of our experiment, we're interested in the name of the device. When you conduct this experiment yourself, the device name will most likely be different.

> **Warning:** In the examples that follow, it is vitally important that you pay close attention to the actual device names in use on your system and **do not use the names used in this text!**

Also note that audio CDs are not the same as CD-ROMs. Audio CDs do not contain file systems and thus cannot be mounted in the usual sense.

Now that we have the device name of the CD-ROM drive, let's unmount the disc and remount it at another location in the file system tree. To do this, we become the superuser (using the command appropriate for our system) and unmount the disc with the `umount` (notice the spelling) command:

```
```shell
[me@linuxbox ~]$ su -
Password:
[root@linuxbox ~]# umount /dev/hdc
```
```

The next step is to create a new *mount point* for the disk. A mount point is simply a directory somewhere on the file system tree. Nothing special about it. It doesn't even have to be an empty directory, though if you mount a device on a non-empty directory, you will not be able to see the directory's previous contents until you unmount the device. For our purposes, we will create a new directory:

```
```shell
[root@linuxbox ~]# mkdir /mnt/cdrom
```
```

Finally, we mount the CD-ROM at the new mount point. The `-t` option is used to specify the file system type:

```
```shell
[root@linuxbox ~]# mount -t iso9660 /dev/hdc /mnt/cdrom
```
```

Afterward, we can examine the contents of the CD-ROM via the new mount point:

```
```shell
[root@linuxbox ~]# cd /mnt/cdrom
```
```

```
```bash
[root@linuxbox cdrom]# ls
```
```

Notice what happens when we try to unmount the CD-ROM:

```
```bash
[root@linuxbox cdrom]# umount /dev/hdc
umount: /mnt/cdrom: device is busy
```
```

Why is this? The reason is that we cannot unmount a device if the device is being used by someone or some process. In this case, we changed our working directory to the mount point for the CD-ROM, which causes the device to be busy. We can easily remedy the issue by changing the working directory to something other than the mount point:

```
```bash
[root@linuxbox cdrom]# cd
[root@linuxbox ~]# umount /dev/hdc
```
```

Now the device unmounts successfully.

## Why Unmounting Is Important

If you look at the output of the free command, which displays statistics about memory usage, you will see a statistic called “buffers.” Computer systems are designed to go as fast as possible. One of the impediments to system speed is slow devices. Printers are a good example. Even the fastest printer is extremely slow by computer standards. A computer would be very slow indeed if it had to stop and wait for a printer to finish printing a page. In the early days of PCs (before multi-tasking), this was a real problem. If you were working on a spreadsheet or text document, the computer would stop and become unavailable every time you printed. The computer would send the data to the printer as fast as the printer could accept it, but it was very slow since printers don't print very fast. This problem was solved by the advent of the printer buffer, a device containing some RAM memory that would sit between the computer and the printer. With the printer buffer in place, the computer would send the printer output to the buffer and it would quickly be stored in the fast RAM so the computer could go back to work without waiting. Meanwhile, the printer buffer would slowly spool the data to the printer from the buffer's memory at the speed at which the printer could accept it.
