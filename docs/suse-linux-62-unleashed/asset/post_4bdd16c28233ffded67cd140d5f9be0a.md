
# NFS CHAPTER 15 471

If you are familiar with the export file configurations of other flavors of UNIX, you know that this process is not similar. Whether one is better than the other is a holy war discussion best left to Usenet newsgroups.

After you set up your /etc/exports file, restart the NFS server: /sbin/init.d/nserver restart

This sends the appropriate signals to the rpc.nfsd and rpc.mountd daemons to reread the /etc/exports file and update their internal tables.

> Tip
> It is considered a good convention to place all the directories you want to export in the /export hierarchy. This makes the intent clear and self-documenting. If you need the directory to also exist elsewhere in the directory tree, use symbolic links. For example, if your server is exporting its /usr/local hierarchy, you should place the directory in /export, thereby creating /export/usr/local. Because the server itself will need access to the /export/usr/local directory, you should create a symbolic link from /usr/local that points to the real location, /export/usr/local.

> Tip
> If you have an error in your /etc/exports file, it is reported when NFS starts up in syslog. Read the section on syslog in this book to find out more about this wonderful debugging tool.

# Using mount to Mount an Exported Filesystem

To mount a filesystem, use the mount command:
mount servername:exported/dir dir/to/mount

servername is the name of the server from which you want to mount a filesystem, /exported/dir is the directory listed in /etc/exports file, and /dir/to/mount is the location on your local machine where you want to mount the filesystem. For example, to mount /export/home from the NFS server denon to the directory /home, use

mount denon:/export/home /home

![](img/cbac72550c7126a22162e94d91a0c360_506_0.png)

Remember that the directory must exist in your local filesystem before anything can be mounted. You can use the mkdir command to create directories.

You can pass options to the mount command. The most important characteristics are specified in the -o options. These characteristics follow:

- - rw/write.
- - Read-only.
- - bg Background mount. Should the mount initially fail (the server is down, for instance), the mount process will place itself in the background and continue until it is successful. This is useful for filesystems mounted at boot time because it keeps the system from hanging at that mount if the server is down.
- - intr Interruptible mount. If a process is pending I/O on a mounted partition, it will allow the process to be interrupted and the I/O call to be dropped.
- - soft By default, NFS operations are hard, meaning that they require the server to acknowledge completion before returning to the calling process. The soft option allows the NFS client to return a failure to the calling process after retrans number of retries.
- - retrans Specifies the maximum number of retried transmissions to a soft-mounted filesystem.
- - vsize Specifies the number of bytes written across the network at once. The default is 8192 (for example, size=2048). You shouldn't change this value unless you are sure of what you are doing. Setting this value too low or too high can have a negative impact on your system's performance.
- - rsize Specifies the number of bytes read across the network at once. Like vsize, the default is 8192. The same warning applies as well: Changing the value without understanding its effect can have a negative impact on your system's performance.

The following is an example of these parameters in use:

```
mount -o rw,bg,intr,soft,retrans=6 :/export/home/home
```

There are many more options to the mount command, but you will rarely see them. See the man page for mount for additional details.

# NFS
CHAPTER 15 473

# Caution

Solaris NFS clients talking to Linux NFS servers to bring out a bug in the Linux NFS implementation. If you suddenly notice normal files being treated as directories or other unusual behavior, change the wsize and rsize to 2048 when mounting the directory. This appears to fix the problem without hurting performance too drastically.

# Unmounting a Filesystem

To unmount the filesystem, use the unmount command:

```
unmount /home
```

This will unmount the /home filesystem.

There is a caveat, of course. If users are using files on a mounted filesystem, you cannot unmount it. All files must be closed before the unmount can happen, which can be tricky on a large system. There are three ways to handle this:

- Use the lsof command (available at http://man.pages/tools/lsof) to list the users and their open files on a given filesystem. Then wait until they are done, or kill their processes. Then you can unmount the filesystem. This is not the most desirable way.
- Use unmount with the -f option to fix the filesystem to unmount. This is often a bad idea because it confuses the programs (and users) who are accessing the filesystem. Files in memory that have not been committed to disk might be lost.
- Bring the system to single-user mode and then mount the filesystem. Although this is the greatest inconvenience of the three, it is the safest way because no one loses any work. (Welcome to system administration.)

![](img/cbac72550c7126a22162e94d91a0c360_508_0.png)

# Configuring the /etc/fstab File to Mount Filesystems Automatically

At boot time, the system will automatically mount the root filesystem with read-only privileges. However, after the system has bootstrapped, it is possible for you to jump in and mount all the filesystems yourself. Even worse, the system might not come back online by itself. To get around this, Linux uses a special file called /etc/fstab. This file lists all the partitions that need to be mounted at boot time and the directory where they need to be mounted. Along with that information you can pass parameters to the mount command.

> Note: NFS servers can also be clients. For example, an NFS server can mount home directories at the same time.

Each filesystem to be mounted is listed in fstab file in the following format:

```
/dev/device dir/to/mount type parameters fs_freq fs_passno
```

An example of that would look like:

```
server:/usr/local /export nfs rsize=8192,wsize=8192,timeout=intr
```

The following items make up this line:

- /dev/device: The device to be mounted. In the case of mounting NFS filesystems, this comes in the form of servername:/exported, where servername is the name of the NFS server and /exported is the directory exported from the NFS server. For example, denon:/export/home, where denon is the hostname of your NFS server and /export/home is the directory specified in the /etc/exports as being shared.
- /dir/to/mount: The location at which the filesystem should be mounted on your directory tree.
- type: The filesystem type. Usually, this is ext2 for your local filesystems. However, NFS mounts should use the NFS filesystem type.

# NFS CHAPTER 15

| parameters | These are the parameters you passed to mount using the -o option. They follow the comma-delimited format. A sample entry looks like rw,intr,bg. |
| fs_freq | This is used by dump to determine whether a filesystem needs to be dumped. |
| fs_passno | This is used by the fsck program to determine the order to check disks at boot. The root filesystem should be set to 1, and other filesystems should have a 2. Filesystems on the same drive will be checked sequentially, but filesystems on different drives will be checked at the same time. |

Any lines in the fstab file that start with the pound symbol (#) are considered comments and ignored.

If you need to mount a new filesystem while the machine is live, you must perform the mount by hand. If you want this to be mounted automatically the next time the system is rebooted, you should add it to the fstab file.

There are two notable partitions that don't follow the same set of rules as normal partitions. They are the swap partition and /proc, which use filesystem types swap and proc, respectively.

You do not mount the swap partition using the mount command. It is instead managed by the swapon command. For a swap partition to be mounted, you must list it in the fstab file. Once it is there, use swapon with the -a parameter, followed by the partition on which you've allocated swap space.

The /proc filesystem is even stranger; it really isn't a filesystem. It is an interface to the kernel abstracted into a filesystem format. Take a peek into it for a large amount of useful information regarding the inner workings of the kernel.

> Tip
> If you need to remount a filesystem that already has an entry in the fstab file, you don't need to type the mount command with all the parameters. Instead, simply pass the directory to mount as the parameter, as in

```
mount /dir/to/mount
```

where /dir/to/mount is the directory that needs to be mounted. mount will automatically look to the fstab file for all the details, such as which partition to mount and which options to use.
