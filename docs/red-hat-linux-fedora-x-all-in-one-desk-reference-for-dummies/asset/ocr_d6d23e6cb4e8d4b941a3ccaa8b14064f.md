# 452 Accessing DOS/Windows File Systems

Next, submit this job schedule by using the following crontab command:

crontab backups

Now you are set for an automated backup. All you need to do is place a new tape in the tape drive everyday. Remember to also give each tape an appropriate label.

# Accessing DOS/Windows File Systems

If you have Microsoft Windows 95/98/Me installed on your hard drive, you've probably already mounted the DOS partition under Fedora Core. If not, you can easily mount DOS partitions in Fedora Core. Mounting makes the DOS directory appear as part of the Linux file system. To identify the DOS partitions easily, you may want to mount the first DOS partition as /dosc, the second and so on.

To determine whether your DOS hard drive partitions are set up to mount automatically, type the grep command to look for the string vfat in the file /etc/fstab:

```
grep vfat /etc/fstab
```

If the output shows one or more lines that contain vfat, your Fedora system mounts DOS/Windows hard-drive partitions automatically.

If the grep command doesn't show any lines that contain the string vfat in /etc/fstab, your system doesn't mount any DOS/Windows hard-drive partitions automatically. Of course, a very good reason for this situation may be that your hard drive has any DOS partitions.

![](bbox=[0.153, 0.663, 0.223, 0.725])

Even if you don't have any DOS partitions on your hard drive, you should learn how to access a DOS file system from Fedora Core because you may have access to a DOS floppy disk on your Fedora system.

# Mounting a DOS disk partition

To mount a hard drive partition or floppy, use the mount command but include the option -t vfat to indicate the file system type as DOS. For example, if your DOS partition happens to be the first partition on your IDE (Integrated Drive Electronics) drive and you want to mount it on /dosc, use the following mount command:

```
mount -t vfat /dev/hdal /dosc
```

TIP