> **CAUTION**
> Remember to leave any NFS-mounted directory before you try to unmount it with umount! You will get a “device busy” error if you try to unmount a filesystem while you’re still inside it.

NFS shares can be mounted in a great variety of ways, and the options are laid out in the man mount_nfs page. Some of the more useful are the -T option, which forces TCP transport rather than UDP (useful for mounts done over WAN links), and the -s and -x <seconds> flags, which allow the mount to time out and disappear after a specified period and then fail (a “soft” mount). Here’s an example:

```
# mount_nfs -s -x 60 spots:/home /home2
```

> **TIP**
> Another useful option is -i, which enables interruptibility. Normally, if you have mounted an NFS share and the server becomes unresponsive or unreachable, any filesystem calls you make (commands that deal with the shared files, such as ls can hang in such a way that even pressing Ctrl+C (the termination signal) won’t stop them. The -i option makes it so that Ctrl+C will force the command to fail, returning control to you.

As with other filesystem types, you can add NFS mounts to /etc/fstab to set up pre- defined mount points, thus simplifying the mount process. Place any options you would otherwise pass to mount_nfs in the Options column, separated by commas, as shown here:

| Device      | Mountpoint  | Fstype | Options          | Dump | Pass# |
|-------------|-------------|--------|------------------|------|-------|
| spots:/home | /home2      | nfs    | rw,-T,-i,noauto  | 0    | 0     |

With a table entry like this, you can mount an NFS filesystem with the mount command:

```
# mount /home2
```

# Mounting Remote Filesystems Automatically at System Boot

All filesystems in /etc/fstab are automatically mounted at boot time, unless the noauto option is present. You can specify that remote NFS shares should be mounted at startup by simply adding them to /etc/fstab, as you just saw. However, there are a few things to watch out for.

Most notably, NFS has an extremely long default timeout period, and the phase during startup when filesystems are mounted is a synchronous, blocking process. If your NFS server or servers cannot be found—for instance, if the server machine isn’t running, or if your own machine’s network connection is not configured properly—the boot process can hang for an intolerably long period before NFS gives up and allows the system to finish the boot procedure.