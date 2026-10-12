```
# key [ -mount-options-separated-by-comma ] location
# Details may be found in the autofs(5) manpage.
kernel    -ro,soft,intr      ftp.kernel.org:/pub/linux
cd          -fstype=iso9660,ro      :/dev/cdrom
# the following entries are samples to pique your imagination
#floppy     -fstype=auto      :/dev/fd0
#floppy     -fstype=ext2      :/dev/fd0
#e2floppy   -fstype=ext2      :/dev/fd0
#jaz        -fstype=ext2      :/dev/sdc1
```

Here, the first column is the key, the second column holds the **mount** options, and the last column is the location from which to mount. If the location entry begins with a colon, it’s a signal to the system that the mount is local. Thus, /misc/ cd would mount /dev/ cdrom with the following **mount** options:

```
-fstype=iso9660,ro
```

![](bbox=[0.15, 0.5, 0.25, 0.57])

Unlike NFS, which requires that the directory already exist in order for you to mount it, the autofs service does not. In the case of the /misc mount point, all that needs to exist is the /misc directory. All subdirectories would be created by the autofs daemon as needed.

If you change any of the map files while autofs is running, you’ll need to restart the autofs service so that it can reread the configuration files. This is done by using autofs as follows:

```
[root@edford /root]# /etc/init.d/autofs reload
```

# CRITICAL SKILL 7.5 Managing Quotas

In any multiuser environment, you’re bound to run across users who—either refusing to play fair or because they’re oblivious to common courtesy—practice the fine art of disk hogging, taking up more than a reasonable amount of disk space.

This problem can be managed in several ways. The first and most obvious solution is to beg and plead. This rarely works. The second approach is peer pressure: You regularly and publicly post the amounts of disk space being hogged by those users. If people are at all sensitive to what others think of them, this may work. The final and most successful technique is to institute disk quotas, allowing each user to consume a certain amount of disk space and no more. Enforcement is done by the operating system.

Disk quotas are usually the best option for system administrators, because the quotas are automated and don’t require that you confront the offending users. However, technical and/or political barriers may be standing in the way of using them. (For instance, the CEO may not