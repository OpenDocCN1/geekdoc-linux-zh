# Configuring /etc/fstab to Allow Users to Mount Remote Volumes

You can add NFS exports to /etc/fstab just as if they were normal partitions. This includes the ability to use the user option to allow users to mount remote partitions. Here’s a sample /etc/fstab file illustrating this:

```
/dev/hda10   /          ext2   defaults   1 1
none         /proc      proc   defaults   0 0
speaker:/home /speaker/home nfs defaults 0 0
speaker:/mnt  /speaker/mnt nfs noauto,user 0 0
```

In addition to mounting the root and /proc partitions, this /etc/fstab file gives access to two NFS exports from the computer speaker: /home and /mnt. The system mounts speaker:/home at boot time, so it will always be available—assuming that speaker is always available! The noauto parameter in the fourth column of the speaker:/mnt entry prevents the export from being mounted at system boot, and the user parameter allows users to mount and unmount the exports by typing mount /speaker/home or mount /speaker/mnt.

# Automounting Remote Volumes

You can add NFS exports to an automount configuration, as discussed in Chapter 9, "Basic Principles of File Sharing." As with adding an NFS export to /etc/fstab, you specify nfs as the filesystem type and use the NFS machine:directory specification as the device in the automounter configuration file. There is one difference, though: When you create the entry for the NFS export, you omit the leading colon (:) on the device name. Here’s a sample /etc/auto.misc configuration:

```
floppy       -fstype=auto      :/dev/fd0
cdrom        -fstype=iso9660   :/dev/scd0
teela        -fstype=nfs       teela:/home
```

If the automounter is configured to mount these devices in the /misc directory, you could then access teela’s /home directory by going to /misc/teela. The computer automatically unmounts the NFS export after the delay interval specified in the /etc/auto.master file unless there’s continued access to that directory.