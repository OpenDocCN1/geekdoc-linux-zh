```
/dev/hdc1 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
none on /dev/shm type tmpfs (rw)
[root@server1 root]#
```

Notice from the preceding output that you were still using the /mnt/floppy directory because it was the current working directory. The fuser command also indicated that the root user had a process using the directory. After the current working directory was changed, the umount command was able to unmount the floppy from the /mnt/floppy directory, and the output of the mount command indicated that the floppy disk was no longer mounted.

Recall that mounting simply attaches a disk device to the Linux directory tree so that you can treat the device like a directory full of files and subdirectories. A device can be mounted to any existing directory. However, if the directory contains files, those files are inaccessible until the device is unmounted. Suppose, for example, that you create a directory called /flopper for mounting floppy disks and a file inside called samplefile, as shown in the following output:

```
[root@server1 root]# mkdir /flopper
[root@server1 root]# touch /flopper/samplefile
[root@server1 root]# ls -F /flopper
samplefile
[root@server1 root]#
```

If the floppy disk used earlier is mounted to the /flopper directory, a user who uses the /flopper directory will be using the floppy disk; however, when nothing is mounted to the /flopper directory, the previous contents are available for use:

```
[root@server1 root]# mount -t ext2 /dev/fd0 /flopper
[root@server1 root]# mount
/dev/hda1 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
none on /dev/shm type tmpfs (rw)
/dev/fd0 on /flopper type ext2 (rw)
[root@server1 root]# ls -F /flopper
hosts   lost+found/  workfiles/
[root@server1 root]# umount /flopper
[root@server1 root]# ls -F /flopper
samplefile
[root@server1 root]#
```