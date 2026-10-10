# Mounting noauto File Systems

In your /etc/fstab file there can also be devices for other file systems that are not mounted automatically. For example, you might have multiple disk partitions on your hard disk or an NFS shared file system that you might want to mount only occasionally. A noauto file system can be mounted manually. The advantage is that when you type the mount command, you can type less information and have the rest filled in by the contents of the /etc/fstab file. So, for example, you could type:

```
# mount /zarkov/apps
```

With this command, mount knows to check the /etc/fstab file to get the file system to mount (zarkov:/apps), the file system type (nfs), and the options to use with the mount (in this case, ro for Read Only). Instead of typing the local mount point (/zarkov/apps), you could have typed the remote file system name (zarkov:/apps) instead and had other information filled in.

> TIP When naming mount points, including the name of the remote NFS server in that name can help you remember where the files are actually being stored. This may not be possible if you are sharing home directories (/home/) or mail directories (./var/spool/mail:)

# Using mount Options

You can add several mount options to the /etc/fstab file (or to a mount command line itself) to affect how the file system is mounted. When you add options to /etc/fstab, they must be separated by commas. The following are some options that are valuable for mounting NFS file systems:

+   - hard — With this option on, if the NFS server disconnects or goes down while a process is waiting to access it, the process will hang until the server comes back up. This option is helpful if it is critical that the data you are working with not get out of sync with the programs that are accessing it. (This is the default behavior.)

+   - soft — If the NFS server disconnects or goes down, a process trying to access data from the server will time out after a set period of time when this is on.

+   - rsize— The number of bytes of data read at a time from an NFS server. The default is 1,024. Using a larger number (such as 8,192) will get you better performance on a network that is fast (such as a LAN) and is relatively error-free (i.e., one that doesn't have a lot of noise or collisions).

+   - wsize— The number of bytes of data written at a time to an NFS server. The default is 1,024. Performance issues are the same as with the rsize option.

+   - timeo=# — Sets the time after an RPC time-out occurs that a second transmission is made, where # represents a number in tenths of a second. The default value is seven-tenths (0.7) of a second. Each successive time-out causes the time-out value to be doubled (up to 60 seconds maximum). You should increase this value if you believe that time-outs are occurring because of slow response from the server or a slow network.