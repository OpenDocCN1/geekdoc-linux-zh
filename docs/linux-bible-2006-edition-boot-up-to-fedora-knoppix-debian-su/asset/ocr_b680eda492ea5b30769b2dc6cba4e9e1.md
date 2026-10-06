# 726 Part V ✦ Running Servers

# Mounting noauto/fstab File Systems

Your /etc/fstab file contains devices for other file systems that are not mounted automatically (possibly /dev/cdrom and /dev/fd0, for your CD-ROM and floppy disk devices, respectively). The noauto option for these devices is what prevents them from being mounted at boot time. A noauto file system can be mounted when you need it. The advantage is when you type the mount command, you can type less information and have the rest filled in by the /etc/fstab file. For example you can:

```
# mount /oak/apps
```

With this command, mount knows to check the /etc/fstab file to get the file system to mount (oak:/apps), the file system type (nfs), and the options to use with (in this case ro for read-only). Instead of typing you could have typed the remote system name (oak:/apps) and had other information filled in:

![](bbox=[0.125, 0.413, 0.168, 0.458])

When naming mount points, including the name of the NFS server in that can help you remember where the files are being stored. This might not be possible if you are sharing home directories (/home) or mail directories (/var/spool/mail). For example you might mount a file system from a machine called duck on the directory /mnt/duck.

# Using Mount Options

You can add special mount options to the /etc/fstab file (or to a mount command line itself) to influence how the file system is mounted. When you add options to /etc/fstab, they must be separated by commas. For example, here the noauto, ro, and hard options are used when oak is mounted:

```
oak:/apps /oak/apps nfs noauto,ro,hard 0 0
```

The following are some options that are valuable for NFS file systems:

+   - hard—If this is used and the NFS server disconnects or goes down while a process is waiting to access it, the server will hang until the server comes back up. This is helpful if it is critical that the data you are working with not out of sync with the programs that are accessing it. (This is the default behavior).

+   - soft—If the NFS server disconnects or goes down, a process trying to access data from the server will time out after a period of time when this option is on. An input/output error is delivered to the process trying to access the NFS server.

+   - rsize—The number of bytes of data read at a time from an NFS server. The default is 1024. A larger number (such 8192) will get you better performance on a network that is fast (such as a LAN) and is relatively error-free (that is, one that doesn't have a lot of noise or collisions).