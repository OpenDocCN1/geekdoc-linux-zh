
```
/dev/hdd /mnt/dvd iso9660 ro,noauto,user 0 0
```

Once you have the fstab file set up, you can use the mount command with only the device name or mount point. The mount command looks in the fstab file for all of the additional information needed to mount the file system. This is why you can mount a CD-ROM with only the name of the mount point:

```
# mount /mnt/cdrom
```

No additional information is needed on the command line because mount retrieves everything else from the fstab file. If you use the mount command without sufficient information (and the information is not contained in the fstab file), mount displays an error message and the file system is not mounted.

## Using the autofs Mounting Service

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

## Managing Swap Space

The swap space that you set up when you installed Linux is a special file system that you don’t directly manage—only the kernel accesses that space, and it is only used while the system is running. That is, nothing in swap space is reused the next time the system is started.

You can, however, affect the performance of your system by making certain that you have sufficient swap space and that the swap space is located efficiently. For example, if you have multiple hard disks, having the swap space on a separate hard disk from where commonly used data is stored lets both hard drives work at the same time, increasing the speed of the system. Conversely, if you have the swap space on the same hard drive with all of your data, the hard disk must “take turns” accessing the swap space for the kernel and the data partitions for your programs. Many system administrators use multiple swap partitions on large systems to give the kernel plenty of fast-access disk storage. Some even focus on things such as locating the swap partition near the center of each hard disk, where average access times are shorter.

If you decide to add a swap partition to your system, you can use the mkswap command to format a partition that you have set up using fdisk (and marked as type 82). This is similar to using the mke2fs command to format an ext2 or ext3 partition. Just use a command such as this one to format the partition as swap space:

```
# mkswap /dev/hda2
```

Once you have formatted a partition as swap space, you can add a line to /etc/fstab to tell Linux how to activate the swap space at boot time. The example file shown previously includes this line:

```
/dev/hda3  swap  swap  defaults  0 0
```

Swap space is activated by the swapon command within the system initialization scripts in /etc/rc.d.

You can also create swap space as a special file within another file system. This is much less efficient, but makes an interesting exercise. You create a swap file in Project 10-3.

## Setting Quotas on Disk Usage

Another way you can manage file systems is by imposing a limit on the amount of hard disk space that any user or group can use. These limits are called disk quotas. For example, if you have defined a quota of 100 MB for a user and that user tries to create a new file (of which he is the owner) after using 100 MB of disk space, the system does not permit him to create that file.

Setting up quotas requires four steps:

- 1. Enable quotas on a file system by including the usrquota or grpquota option when the file system is mounted (for example, include it within the /etc/fstab file).
- 2. Use the `edquota` command to establish a quota for one or more users or groups.
- 3. Activate the quota system using the `quotaon` command.
- 4. Review current disk usage for a file system using the `repquota` command, or for a particular user or group using the `quota` command.

Quotas are not often used in business offices (except perhaps on e-mail servers), but may be very helpful in schools or other institutions where many users share a Linux system. You can learn more about disk quotas by reviewing the man pages for the commands described in this section.

A similar feature lets you impose additional limits on the actions of users. The `ulimit` command is part of the bash shell. By adding this command to a user's startup script (for example, in `/home/nwells/.profile`), you can limit the system resources that the user can access from that shell. Resources that you can control via the `ulimit` command include the number of processes running concurrently, the amount of virtual memory used, the amount of file system storage consumed, and the number of seconds of CPU time that can be used.

To see the current state of these values use this command:

```
$ ulimit -a
```

You can change your own values using additional `ulimit` commands, so this method is not appropriate to restrict the activities of advanced users, but it is sufficient to set basic resource limits for regular users. As an example, the following command sets a limit on the file system space that can be consumed (new files created) by the shell to one megabyte (1024 blocks):

```
$ ulimit -f 1024
```

Using disk quotas and the `ulimit` command is a type of file system accounting. These features let you control and monitor usage of file system resources by users.

## CHAPTER SUMMARY

- Software packages are single files that contain all the files and instructions needed to install an application or collection of utilities. The most popular formats for software packages on Linux are the Red Hat Package Manager format (which use .rpm file extensions) and the Debian package format (which use .deb file extensions).
- The `dpkg` utility is used to manage Debian packages via the command line.
- The `system-config-packages` utility is used to manage rpm packages graphically on Red Hat Linux or Fedora systems. The `rpm` command is used to manage rpm packages via the command line. It includes options to verify, query, install, and erase packages. The `rpm` command maintains a database of information about the packages that are currently installed.
- The Red Hat Network service permits automatic updating of operating system files over the Internet for Red Hat Linux and Fedora distributions. This service is managed through the up2date graphical utility and an icon on the GNOME Panel.
- Advanced services of Red Hat Network are available for a fee and provide updating services suitable for large organizations with many Linux servers that need to be managed collectively.
- Linux supports many file systems types by using a virtual file system model. Popular journaling file systems used by default on Linux include ext3, ReiserFS, and JFS.
- Information about an ext3 file system is stored in the superblock. You can view or alter the superblock parameters using the tune2fs command.
- The mount command attempts to use information stored in /etc/fstab to determine how to mount a file system if all the needed parameters are not supplied on the command line.
- The /etc/fstab file contains a list of all file systems that the system mounts at boot time, as well as those that might be mounted later on.
- The df and du commands are helpful in watching how disk space is being used on a busy Linux system. The df command displays information for an entire file system; du displays the disk space used by directories.
- Each file and directory can be assigned attributes such as "immutable." Most of these are not used regularly, but they can be viewed and set with lsattr and chattr, respectively.
- The fsck utility examines a file system to see that its contents have not been corrupted. If errors are found, fsck can also repair them.
- You can add new file systems to Linux by setting up partitions using the fdisk utility, then formatting the newly created partition using mke2fs or a similar utility. New file systems can be manually mounted directly using the mount command, or they can be listed in /etc/fstab with options that cause them to be mounted automatically each time the system is started.
- The fdisk utility configures partition data on a hard disk. It should be used with great care.
- Linux supports networked file systems using protocols such as NFS and SMB. These are accessed using the mount command and a server name as a parameter.
- The autofs service, once configured using /etc/auto.master, can automatically mount file systems whenever a user enters a named directory that is a mount point for a file system not yet mounted.
- Swap space is created much like regular file systems, using the mkswap and swapon commands, though it is used only by the kernel.
- Disk quotas are configured using the edquota command for any file system on which the usrquota or grpquota options have been specified. These quotas restrict how much disk space a user is permitted to consume. The ulimit command, a part of the bash shell, also allows you to limit the system resources that users can access.
