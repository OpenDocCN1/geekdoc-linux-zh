
```
/etc/fstab
```

```
quicksilver:/home   /home   nfs bg,hard,intr,nosuid,rw,no_root_squash 1 0
quicksilver:/usr/local /usr/local nfs bg,hard,intr,rw,no_root_squash 1 0
```

As you can see, these entries differ from a normal entry in that instead of specifying a device file where the filesystem resides, you specify the server, followed by a colon and the directory that is exported. Other than this, the only other differences are the specified type of nfs, and the mount options, which for local filesystems are usually set to the keyword defaults.

Having created these entries, you must now create the directories to serve as mount points for the network filesystems. The final step is to actually mount the filesystems. This is performed by issuing the mount command as in the startup script, /etc/rc.d/init.d/netfs. This mount command is

```
mount -a -t nfs
```

This mount command says to mount all filesystems described in the /etc/fstab file with a filesystem type of nfs.

## AFS and Coda

In addition to the NFS network filesystem, there are alternatives for sharing filesystems under Linux. Two of these alternatives are AFS, a commercial filesystem from Transarc, and Coda, a freely available filesystem that supports many of the features of AFS. Both of these are distributed filesystems that differ significantly from NFS, but that share with NFS the goal of sharing data across networks.

AFS was originally developed as part of the Andrew project at MIT and was later commercialized by Transarc. Information regarding AFS for Linux is available from http://www.umiug.umd.edu/linuxafs, which is the home of the Linux AFS FAQ. This FAQ explains the status of the Linux port of AFS, discusses the terms under which you may use the Linux client, provides information on setting it up, and provides troubleshooting tips. In addition, there is a mailing list dedicated to AFS on Linux. To subscribe to this mailing list, you can issue the following command:

```
echo "subscribe linux-afs" | mail linux-afs-request@mit.edu
```

Coda Howto, which covers everything you need to set up Coda on your Linux system. Unfortunately, Coda is not quite ready for prime time and it is not recommended for use in production environments. Its primary use at this time is to test out the available features and improve them through testing.

Now that we have covered some of the distributed filesystem options available for Linux, let's take a look at ways to make accessing them from client systems easier.

## The Automount Daemon and Autofs

One of the features of modern UNIX systems is support for the automatic mounting of filesystems as the result of attempts to access them. This capability is available in two different forms for Linux systems—through use of the BSD automounter or through use of the Linux autofs. This section takes a look at setting up both of these systems and comparing the features of each, starting with the older of the two, the BSD automount daemon.

### The BSD Automount Daemon

If you have never used the automount daemon before, you may wonder what it is and why you might want to implement it on your network. In a large network environment, there are often many filesystems that need to be shared among the systems on the network. In addition, some of these filesystems are not needed all of the time or the system from which the filesystem is served is not available all of the time. To help remedy this situation, the automount daemon, or amd, was implemented to provide a mechanism by which filesystems could be mounted when someone tries to access them and unmounted when the connection becomes idle. This is a major advantage of using amd because it reduces overhead and increases performance. In addition to providing this capability for NFS filesystems, amd can also be used to automatically mount and unmount filesystems on removable media devices, such as floppies or CD-ROM drives.

### Configuring the Automount Daemon

Now that you have an understanding of what the automount daemon does, let's take a look at how to configure and use it. The first step in setting up the automount daemon is to make sure that the filesystems that you want to have access to are properly exported. This is done using the procedure for exporting filesystems discussed earlier in this chapter in the section on NFS server configuration. Again, we'll use the example we have used throughout the chapter and verify that the filesystems are exported using the showmount command.

```
[tschenk@wizard chapter15]$ showmount -e quicksilver
Export list for quicksilver:
/usr/local      *.alchemy.net
/mnt/cdrom 192.168.56.0/255.255.255.0
/home          wizard.alchemy.net
```

The next step is to make sure that the automount daemon software is installed. The package name for your Red Hat system is am-utils, which you must install if it is not already installed. A quick method to do this is to use the rpm command: rpm -q am-utils, which will return the package name if it is installed or a message indicating that it is not installed. If it is not installed, you must install it from your installation media or from a Red Hat ftp site.

Now that you have ensured that the automount daemon is installed, you must configure it. Configuration information for the automount daemon is contained in the file /etc/amd.conf. This is a line-oriented configuration file in which each line is a configuration parameter, a comment, or a section heading with no provisions for line continuation. Here's a look at the default amd.conf that comes with Red Hat:

```
/etc/amd.conf

/defaults fs=${autodir}/$(rhost)/root/$(rfs);opts=nosuid,nodev
* rhost=${key};type=host;rfs:-/
```

This amd.conf file is quite simplistic, and allows you to automount any exported filesystem to which you have permissions by changing directory to /net/<hostname>/exported_filesystem. For example, given the mount points exported from quicksilver as shown earlier by the showmount command, you can access the files in /usr/local on quicksilver by simply accessing /net/quicksilver/usr/local. For example, if the afio command was installed in /usr/local/bin on quicksilver, you could run it from wizard by invoking the command as /net/quicksilver/usr/local/bin/afio. This mount would remain as long as the filesystem was being accessed and would be unmounted after some period of inactivity or until you specifically caused an unmount using the umount command. Having seen this simplistic amd.conf file, here's a more complicated one:

```
/etc/amd.conf

# Set the default mount options is not overridden by another entry.
# This entry also specifies the default path on the local machine to
# access in order to mount the remote filesystem.
```

```
/defaults   fs=${autodir}/$(host)/root/$(rfs);opts=nosuid,nodev
```

```
# This entry is for manual pages. All manual pages for all architectures
# are stored on a file server, dumptruck, which stores them in a platform
# specific directory under /usr/share.
```

```
man
    arch=pa-risc;fs:=/usr/share/man;type=nfs; \
    rhost=dumptruck;rfs:=/usr/share/$(arch) \
    arch=sunos;fs:=/usr/share/man;type=nfs; \
    rhost=dumptruck;rfs:=/usr/share/$(arch) \
    arch=linux;fs:=/usr/share/man;type=nfs; \
    rhost=dumptruck;rfs:=/usr/share/$(arch) \
    arch=freebsd;fs:=/usr/share/man;type=nfs; \
    rhost=dumptruck;rfs:=/usr/share/$(arch) \
    arch=solaris;fs:=/usr/share/man;type=nfs; \
    rhost=dumptruck;rfs:=/usr/share/$(arch)
```

```
# This final entry is for a replicated database, that is available on three
# different servers. The database is identical on each server so that if 1
# of them is unavailable, we simply connect to one of the others.
```

```
inventory   fs:=/data/inventory;type=nfs;rfs=/inventory; \
    rhost=invdb1;rhost=invdb2;rhost=invdb3
```

Please note that as stated earlier there is no continuation character allowed in the /etc/amd.conf file. The \ character in the preceding listing is simply used for readability. In the actual file, the entire entry would need to be entered on a single line. These examples show you some of what you can accomplish with the automount daemon. For a more complete description of the amd.conf file syntax, refer to the amd.conf manual page in section 5 of the Linux manual pages.

### Starting the automount Daemon

Now that you have the /etc/amd.conf file set up to your satisfaction, you are ready to start the automount daemon. This daemon, amd, is located in /usr/sbin in a standard Red Hat installation and it is normally started by running the /etc/rc.d/init.d/amd script. This script first sources a configuration file located in /etc/sysconfig called, surprisingly enough, amd, which defines some variables used by the script. There are three variables that may be set in this file. The first is ADIR, which defines the temporary directory on which to cache mounts to remote filesystems. By default this is set to /.automount on Red Hat systems. The next variable is MOUNTPOINTS, which specifies the directory, /net by default on Red Hat, that serves as the root for all automounted filesystems, and the map name, which is another name for the /etc/amd.conf file. The final variable that can be set is the
