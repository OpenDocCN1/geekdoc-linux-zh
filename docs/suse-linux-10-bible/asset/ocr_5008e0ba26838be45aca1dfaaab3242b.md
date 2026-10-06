# Chapter 3 ✦ Partitions, Filesystems, and Files 99

The filesystems you can access from a Linux system can be grouped into two general types—local and remote. Local filesystems are filesystems that are located on storage devices that are directly connected to a particular Linux system. Remote filesystems are those that are attached to other Linux systems that you can access from your system by using a networked protocol such as the Network File System (NFS), which is the most common network filesystem on Linux and Unix systems.

![](bbox=[0.18, 0.263, 0.203, 0.298])

For more information about NFS, see Chapter 22.

Filesystems can be mounted either manually or automatically when your system boots. Mounting filesystems automatically is discussed later in this chapter, in the section "Mounting Filesystems Automatically." Filesystems are mounted manually using the mount command. The mount command attaches a filesystem to the filesystem hierarchy and allows you to pass parameters to the filesystem driver that specify how it should use the filesystem. Using the mount command with no arguments lists all the filesystems that are currently mounted on your system, as shown in Listing 3-10.

# Listing 3-10: Mounting an EXT2 Filesystem

```
mount: # mount -t ext2 /dev/hda5 /mnt
mount: # mount
/dev/hda3 on / type reiser (rw,acl,user_xattr)
proc on /proc type proc
tmpfs on /dev/shim type tmpfs
devpts on /dev/pts type devpts (rw,mode=0620,gid=5)
/dev/hda2 on /home type filesystems (rw,acl,user_xattr)
/dev/hdc on /media/dev type subfs
(rw,nosuid,nodev,sync,fs=floppy,procuid,charset=utf8)
/dev/db1 on /media/floppy type subfs
usbfs on /proc/bus/usb type usbfs
/dev/hda5 on /mnt type ext2 (rw)
```

As commonly used, the mount command takes two arguments, the block device where the filesystem resides and the directory you want to mount it. The /mnt directory is a general-purpose directory that is present on most Linux systems and is used for mounting filesystems that you want to use for a single session. For filesystems you want to use regularly, it is custom to create a directory under /mnt if you want to mount a filesystem or follow the procedure to mount a filesystem on a regular basis discussed later in this chapter in the section entitled "Mounting Filesystems Automatically." If you want to filesystems permanently for specific purposes, it is a good idea to create or identify