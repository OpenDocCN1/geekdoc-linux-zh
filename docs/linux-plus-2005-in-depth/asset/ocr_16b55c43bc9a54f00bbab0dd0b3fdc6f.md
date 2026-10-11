Thus, to mount the first floppy device (/dev/fd0) to the /mnt/floppy directory and automatically detect the type of filesystem on the device, simply specify enough information for the mount command to find the appropriate line in the /etc/fstab file:

```
```text
[root@server1 root]# mount /dev/fd0
[root@server1 root]# mount
/dev/hda1 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
none on /dev/shm type tmpfs (rw)
/dev/fd0 on /mnt/floppy type ext2 (rw,nosuid,nodev)
[root@server1 root]# umount /dev/fd0
[root@server1 root]#
```
```

The mount command in the preceding output succeeded because there existed a line in /etc/fstab that described the mounting of the /dev/fd0 device.

Alternatively, you could specify the mount point as an argument to the mount command to mount the same device via the correct entry in /etc/fstab:

```
```text
[root@server1 root]# mount /mnt/floppy
[root@server1 root]# umount
/dev/hda1 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
none on /dev/shm type tmpfs (rw)
/dev/fd0 on /mnt/floppy type ext2 (rw,nosuid,nodev)
[root@server1 root]# umount /mnt/floppy
[root@server1 root]#
```
```

Table 6–4 lists commands that are useful when mounting and unmounting floppy disks.

Although the commands listed in Table 6–4 allow a user complete control over the mounting process, floppy disks are typically mounted automatically to the /mnt/floppy directory when you access the floppy disk using a GUI environment. From the GNOME desktop, simply double-click the Computer icon and then double-click the Floppy icon, as shown in Figure 6–3. From the KDE desktop, you can double-click the Start Here icon, select Devices, and double-click the Floppy icon, as shown in Figure 6–4.

Mounting a floppy in the GUI environment places an icon representing the floppy on the desktop. You can then double-click the floppy icon to open a listing of the files on the floppy, or right-click the floppy icon to obtain a menu from which you can unmount the floppy by selecting Unmount Volume.