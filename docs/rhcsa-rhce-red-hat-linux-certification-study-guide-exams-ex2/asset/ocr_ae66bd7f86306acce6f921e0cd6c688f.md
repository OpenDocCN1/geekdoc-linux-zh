# Removable Media and /etc/fstab

In general, removable media should not be mounted automatically during the boot process. That's possible in the /etc/fstab configuration file with an option like noauto. But in general, it's not standard in RHEL to set up removable media in /etc/fstab.

To read removable media such as smart cards and CD/DVDs, RHEL somewhat automates the mounting of such media in the GNOME or KDE Desktop Environments. While the details of this process are not part of the Red Hat Exam Prep guide, the process is based on configuration files in the /etc/udev/rules.d directory. If RHEL detects your hardware, click Places; in the menu that appears, select the entry for the removable media. If multiple removable media options are loaded, you can select the media to mount in the Removable Media submenu.

If that doesn't work for some reason, you can use the mount command directly. For example, the following command mounts a CD/DVD in a drive.

```
# mount -t iso9660 /dev/sr0 /mnt
```

The -t switch specifies the type of filesystem (iso9660). The device file /dev/sr0 represents the first CD/DVD drive; /mnt/ is the directory through which you can access the files from the CD/DVD after mounting. But /dev/sr0? How is anyone supposed to remember that?

Linux addresses that in a couple of ways. First, it sets up links from more sensibly named files such as /dev/cdrom, which you can confirm with the ls -l /dev/cdrom command. Second, try the blkid command. If removable media (other than a CD/DVD) are connected, you'll see it in the output to the command, including the associated device file.

Just remember that it is important to unmount removable media such as USB keys before removing them. Otherwise, the data that you thought was written to the disk might still be in the unwritten RAM cache. In that case, you would lose that data.

Given these examples of how removable media can be mounted, you should have a better idea on how such media can be configured in the /etc/fstab configuration file. The standard defaults option is inappropriate in most cases, as it mounts a system in read-write mode (even for read-only DVDs), attempts to mount automatically during the boot process, and limits access to the root administrative user. But that can be changed with the right options. For example, to configure a CD drive that can be mounted by regular users, you could add the following line to /etc/fstab:

```
/dev/sr0 /cdrom auto ro,noauto,users 0 0
```