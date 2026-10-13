> Another useful option is -i, which enables interruptibility. Normally, if you have mounted an NFS share and the server becomes unresponsive or unreachable, any filesystem calls you make (commands that deal with the shared files, such as ls) can hang in such a way that even pressing Ctrl+C won't stop them. The -i option makes it so that Ctrl+C (the termination signal) will force the command to fail, returning control to you.

As with other filesystem types, you can add NFS mounts to /etc/fstab to set up predefined mount points, simplifying the mount process. Place any options you would otherwise pass to mount_nfs in the Options column, separated by commas:

# Device | Mountpoint | FStype | Options | Dump | Pass#
spots:/home | /home2 | nfs | rw,-T,-i,noauto | 0 | 0

With a table entry like this, you can mount an NFS filesystem with the mount command:

```
# mount /home2
```

# Mounting Remote Filesystems Automatically at System Boot

All filesystems in /etc/fstab are automatically mounted at boot time unless the noauto option is present. You can specify that remote NFS shares should be mounted at startup by simply adding them to /etc/fstab, as you just saw. However, there are a few things to watch out for.

Most notably, NFS has an extremely long default timeout period, and the phase during startup when filesystems are mounted is a synchronous, blocking process. If your NFS server or servers cannot be found—for instance, if the server machine isn't running, or if your own machine's network connection is not configured properly—the boot process can hang for an intolerably long period before giving up and finishing the boot procedure.

You can solve this problem by placing the noauto option in /etc/fstab, as you saw in our earlier example. However, this means that you have to mount each NFS share manually after the system is fully booted. There's a better way to handle this: the -b option.

# Device | Mountpoint | FStype | Options | Dump | Pass#
spots:/home | /home2 | nfs | rw,-b | 0 | 0