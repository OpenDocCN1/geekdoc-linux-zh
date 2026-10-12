
## /etc/init.d/nfs start
## /etc/init.d/nfslock start

The NFS service should now be running and ready to share directories with other computers on your network.

## Using NFS file systems

After a server exports a directory over the network using NFS, a client computer connects that directory to its own file system using the mount command. The mount command is the same one used to mount file systems from local hard disks, CDs, and floppies. Only the options to give to mount are slightly different.

Mount can automatically mount NFS directories that are added to the /etc/fstab file, just as it does with local disks. NFS directories can also be added to the /etc/fstab file in such a way that they are not automatically mounted. With a noauto option, an NFS directory listed in /etc/fstab is inactive until the mount command is used, after the system is up and running, to mount the file system.

### Manually mounting an NFS file system

If you know that the directory from a computer on your network has been exported (that is, made available for mounting), you can mount that directory manually using the mount command. This is a good way to make sure that it is available and working before you set it up to mount permanently. Here’s an example of mounting the /tmp directory from a computer named maple on your local computer:

```
# mkdir /mnt/maple
# mount maple:/tmp /mnt/maple
```

The first command (mkdir) creates the mount point directory (/mnt is a common place to put temporarily mounted disks and NFS file systems). The mount command then identifies the remote computer and shared file system separated by a colon (maple:/tmp). Then, the local mount point directory follows (/mnt/maple).

> **NOTE:** If the mount failed, make sure the NFS service is running on the server and that the server's firewall rules don't deny access to the service. From the server, type `ps ax | nfsd`. You should see a list of nfsd server processes. If you don't, try to start your NFS daemons as described in the previous section. To view your firewall rules, type `iptables -L` (see Chapter 14 for a description of firewalls). By default, the nfsd daemon listens for NFS requests on port 2049. Your firewall must accept udp requests on ports 2049 (nfs) and 111 (rpc).

To ensure that the mount occurred, type `mount`. This command lists all mounted disks and NFS file systems. Here is an example of the mount command and its output:

```
# mount
/dev/hda3 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
/dev/hda1 on /boot type ext3 (rw)
none on /dev/shm type tmpfs (rw)
maple:/tmp on /mnt/maple type nfs (rw,addr=10.0.0.11)
```

The output from the mount command shows your mounted disk partitions, special file systems, and NFS file systems. The first output line shows you hard disk (/dev/hda3), mounted on the root file system (/), with read/write permission (rw), with a file system type of ext3 (the standard Linux file system type). The small /boot file system is also of type ext3. The /proc, /sys, /dev/shm, /dev/pts, and usbdevfs mount points represent special file system types. The just-mounted NFS file system is the /tmp directory from maple (maple:/tmp). It is mounted on /mnt/maple and its mount type is nfs. The file system was mounted read/write (rw) and the IP address of maple is 10.0.0.11 (addr=10.0.0.11).

What I just showed is a simple case of using mount with NFS. The mount is temporary and is not remounted when you reboot your computer. You can also add options to the mount command line for NFS mounts:

- **-a** — Mount all file systems in /etc/fstab (except those indicated as noauto).
- **-f** — This goes through the motions of (fakes) mounting the file systems on the command line (or in /etc/fstab). Used with the -v option, -f is useful for seeing what mount would do before it actually does it.
- **-r** — Mounts the file system as read-only.
- **-w** — Mounts the file system as read/write. (For this to work, the shared file system must have been exported with read/write permission.)

The next section describes how to make the mount more permanent (using the /etc/fstab file) and how to select various options for NFS mounts.

### Automatically mounting an NFS file system

To set up an NFS file system to mount automatically each time you start your Fedora system, you need to add an entry for that NFS file system to the /etc/fstab file. The /etc/fstab file contains information about all different kinds of mounted (and available to be mounted) file systems for your Fedora system.

The format for adding an NFS file system to your local system is the following:

```
host:directory    mountpoint    nfs    options    0    0
```

The first item (host:directory) identifies the NFS server computer and shared directory. mountpoint is the local mount point on which the NFS directory is mounted, followed by the file system type (nfs). Any options related to the mount appear next in a comma-separated list. (The last two zeros just tell Fedora not to dump the contents of the file system and not to run fsck on the file system.)

The following are two examples of NFS entries in /etc/fstab:

```text
maple:/tmp     /mnt/maple      nfs      rsize=8192,wsize=8192   0  0
oak:/apps       /oak/apps       nfs      noauto,ro               0  0
```

In the first example, the remote directory /tmp from the computer named maple (maple:/tmp) is mounted on the local directory /mnt/maple (the local directory must already exist). The file system type is nfs, and read (rsize) and write (wsize) buffer sizes are set at 8192 to speed data transfer associated with this connection. In the second example, the remote directory is /apps on the computer named oak. It is set up as an NFS file system (nfs) that can be mounted on the /oak/apps directory locally. This file system is not mounted automatically (noauto), however, and can be mounted only as read only (ro) using the mount command after the system is already running.

> **TIP:** The default is to mount an NFS file system as read/write. However, the default for exporting a file system is read-only. If you are unable to write to an NFS file system, check that it was exported as read/write from the server.

### Mounting noauto file systems

In your /etc/fstab file are devices for other file systems that are not mounted automatically (probably /dev/cdrom and /dev/fd0, for your CD-ROM and floppy disk devices, respectively). A noauto file system can be mounted manually. The advantage is that when you type the mount command, you can type less information and have the rest filled in by the contents of the /etc/fstab file. So, for example, you could type:

```bash
# mount /oak/apps
```

With this command, mount knows to check the /etc/fstab file to get the file system to mount (oak:/apps), the file system type (nfs), and the options to use with the mount (in this case ro for read-only). Instead of typing the local mount point (/oak/apps), you could have typed the remote file system name (oak:/apps) instead, and had other information filled in.

> **TIP:** When naming mount points, including the name of the remote NFS server in that name can help you remember where the files are actually being stored. This may not be possible if you are sharing home directories (/home) or mail directories (/var/spool/mail).

### Using mount options

You can add several mount options to the /etc/fstab file (or to a mount command line itself) to impact how the file system is mounted. When you add options to /etc/fstab, they must be separated by commas. The following are some options that are valuable for mounting NFS file systems:

- **hard** — With this option on, if the NFS server disconnects or goes down while a process is waiting to access it, the process will hang until the server comes back up. This option is helpful if it is critical that the data you are working with not get out of sync with the programs that are accessing it. (This is the default behavior.)
- **soft** — If the NFS server disconnects or goes down, a process trying to access data from the server will time out after a set period of time when this is on.
- **rsize** — The number of bytes of data read at a time from an NFS server. The default is 1024. Using a larger number (such as 8192) will get you better performance on a network that is fast (such as a LAN) and is relatively error-free (that is, one that doesn’t have a lot of noise or collisions).
- **wsize** — The number of bytes of data written at a time to an NFS server. The default is 1024. Performance issues are the same as with the rsize option.
- **timeo=#** — Sets the time after an RPC timeout occurs that a second transmission is made, where # represents a number in tenths of a second. The default value is seven-tenths of a second. Each successive timeout causes the timeout value to be doubled (up to 60 seconds maximum). You should increase this value if you believe that timeouts are occurring because of slow response from the server or a slow network.
- **retrans=#** — Sets the number of minor retransmission timeouts that occur before a major timeout. When a major timeout occurs, the process is either aborted (soft mount) or a Server Not Responding message appears on your console.
- **retry=#** — Sets how many minutes to continue to retry failed mount requests, where # is replaced by the number of minutes to retry. The default is 10,000 minutes (which is about one week).
- **bg** — If the first mount attempt times out, try all subsequent mounts in the background. This option is very valuable if you are mounting a slow or sporadically available NFS file system. By placing mount requests in the background, Fedora can continue to mount other file systems instead of waiting for the current one to complete.
- **fg** — If the first mount attempt times out, try subsequent mounts in the foreground. This is the default behavior. Use this option if it is imperative that the mount be successful before continuing (for example, if you were mounting /usr).

> **NOTE:** If a nested mount point is missing, a timeout to allow for the needed mount point to be added occurs. For example, if you mount /usr/trip and /usr/trip/extra as NFS file systems, if /usr/trip is not yet mounted when /usr/trip/extra tries to mount, /usr/trip/extra will time out. Hopefully, /usr/trip will come up and /usr/trip/extra will mount on the next retry.
