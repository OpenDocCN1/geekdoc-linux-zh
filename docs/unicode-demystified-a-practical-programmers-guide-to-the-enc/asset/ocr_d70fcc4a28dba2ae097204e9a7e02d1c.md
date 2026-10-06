# 1020 Chapter 17 Red Hat Linux System Administration

If you will be mounting the systems frequently, it is more convenient to edit the /etc/fstab file (page 978). The following /etc/fstab entries mount the same directories automatically whenever the machine is booted.

| donald:/export/home | /myhome nfs 0 0 |
| donald:/export/home | /apps nfs r,nosuid 0 |
| donald:/export/apps/oracle | /apps/oracle nfs r 0 |

# Exporting Symbolic Links and Device Files

When you export a symbolic link, make sure that the object of the link is available on the client (remote) machine. Either, the object of the link must exist on a client machine, or you must export and mount it along with the exported link, otherwise it will not point to the file it points to on server.

A device file refers to a Linux kernel interface. When you export a device file, you export that interface. If the client machine does not have the same type of device, the exported device will not work.

A file is mounted using NFS is always type nfs on the local machine, regardless of what it is on the remote machine. Typically you never need fsck on or back up an NFS filesystem. The entries in the third, fifth, and sixth columns of fstab are usually nfs, 0, and 0. Also, the options for mounting an NFS filesystem differ from those from an ext2 or ext3 filesystem. Refer to the mount and nfs man pages for details.

# umount: Unmounts a Remote Filesystem

Use unmount to un a remote filesystem the same way you unmount a local one (page 977).

# showmount: Displays NFS Status Information

The showmount utility provides NFS status information. Call showmount with an argument of the hostname of the machine that you want information about. No argument or argument of localhost causes showmount to report on your local machine. An argument of the name of a remote machine reports on that machine. Without any options, showmount displays a list of machines that are allowed to mount local directories. In the following example, kudos and bravo can mount local directories, but you do not know which ones:

```
# /usr/sbin/showmount localhost
Hosts on localhost:
kudos.tcorp.com
vo.tcorp.com
```