Change to the /mnt/cdrom directory, where you can then peruse the directory structure on the CD as easily as you can on the host box. If necessary, copy the files from their remote location onto another location on the hard drive.

When you are finished with that particular drive or device, unmounting the host drive from the client side is as simple as unmounting other local devices. Be certain you are not currently accessing any files from the remote location or have a terminal session pointing to any of the files within the mounted location. If that happens, you will be unable to mount the partition.

To unmount the device, simply enter the following:

```
umount /mnt/cdrom
```

For more complex mounting, such as mounting formatted file systems, you can enter the following setting into your host’s /etc/exports file:

```
# sample /etc/exports file
/home                 sequitur(rw) nihil(o,rw,no_root_squash)
/usr/local/gnu         *.fortuna.edu(rw)
```

The first line allows users on the clients sequitur and nihil to access the /home directory. You can place this directory anywhere on the client computer, but the mounted directory must be located on the local subnet. The no_root_squash option denies access to setuid root commands. This prevents users from executing a command that might be harmful to your system. The next line allows any host from the domain fortuna.org to have read-write access to the /usr/local/gnu directory.

To make sure that a system mounts an NFS file system upon boot, you need only edit the /etc/fstab file. As with the other entries listed in /etc/fstab, you can accomplish an NFS mount automatically simply by adding another entry, as shown in Listing 15.6.

# Listing 15.6 A Sample /etc/fstab File that Provides Automatic Mounting of Directories via NFS

| /dev/hda1 | / | ext2 | defaults | 1 1 |
| /dev/hda5 | /home | ext2 | defaults | 1 2 |
| /dev/cdrom | /mnt/cdrom | iso9660 | nouauto,owner,ro | 0 0 |
| /dev/hda8 | /opt | ext2 | defaults | 1 2 |
| /dev/hda7 | /usr | ext2 | defaults | 1 2 |