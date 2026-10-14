```
/dev/hdd /mnt/dvd iso9660 ro,noauto,user 0 0
```

Once you have the fstab file set up, you can use the mount command with only the device name or mount point. The mount command looks in the fstab file for all of the additional information needed to mount the file system. This is why you can mount a CD-ROM with only the name of the mount point:

```
# mount /mnt/cdrom
```

No additional information is needed on the command line because mount retrieves everything else from the fstab file. If you use the mount command without sufficient information (and the information is not contained in the fstab file), mount displays an error message and the file system is not mounted.

# Using the autofs Mounting Service

You sometimes will want users to be able to access a file system without having it mounted continuously. At the same time, you may not want users to be able to (or have to) mount a file system when they need to access it. The solution to this dilemma is the autofs service. This service is a daemon that watches for users to change directories into a directory that is configured as an autofs mount point. When a user enters that directory, the autofs daemon mounts the needed file system in the background so that the user can access data on it.

The autofs service is operated by a script in the /etc/rc.d/init.d directory, so you can use the service and chkconfig commands to manage it. By default, no file systems are automounted by autofs, but you can configure as many automounting file systems as you need. You should configure the file /etc/auto.master with a list of all mount points that autofs should watch for users to enter. For example, if you want autofs to mount a file system whenever a user enters /misc, add this line to the /etc/auto.master file:

```
/misc      /etc/auto.misc
```

You then must create a file called /etc/auto.misc that contains the options to use when autofs mounts a file system to /misc. These basically mirror the options contained in the /etc/fstab file; they are described in the man pages for autofs, automount, and auto.master.

After making changes to the /etc/auto.master file, you must restart the autofs server so that it knows about the mount points it should watch for. Use this command the first time you add an entry to /etc/auto.master:

```
# service autofs start
```

Use this command if you add more mount points or remove mount points from the file /etc/auto.master:

```
# service autofs reload
```