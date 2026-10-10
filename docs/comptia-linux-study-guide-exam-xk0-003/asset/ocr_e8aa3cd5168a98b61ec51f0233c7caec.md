This output shows the device name associated with each partition, the start and end cylinder numbers, the number of 1024-byte blocks in each partition, each partition’s hexadecimal (base 16) ID code, and the partition or OS type associated with that code. The fdisk program creates a similar display for GPT disks.

If Linux boots, you can also use the df utility (described later in “Using df”) to identify the partitions your system is using. This tool won’t identify partitions that aren’t mounted, though, including swap partitions and partitions you simply aren’t using (such as those for non-Linux OSs, unless they’re currently mounted).

# # Mounting and Unmounting Partitions

Linux provides the mount command to mount a filesystem to a mount point—that is, to make the filesystem available as files and directories in the specified mount point, which is an ordinary directory. The umount command reverses this process. (Yes, umount is spelled correctly; it’s missing the first n.) In practice, using these commands is usually not too difficult, but they support a large number of options.

# ## Syntax and Parameters for mount

The syntax for mount is as follows:

```
`mount [-alrsw] [-t fstype] [-o options] [device] [mountpoint]`
```

Common parameters for mount support a number of features, as summarized in Table 6.6. device is the device filename associated with the partition or disk device, and mountpoint is the directory from which you want to access your files. Both parameters are normally required, but you may omit one of them under certain circumstances, as described shortly.

**TABLE 6.6 mount Options**

| Option | Description |
| :----- | :--------------------------------------------------------- |
| –a       | This parameter causes mount to mount all the filesystems listed in the `/etc/fstab` file, which specifies the most-used partitions and devices. The upcoming section “Defining Standard Filesystems” describes this file’s format. |
| –r       | This parameter causes Linux to mount the filesystem read-only, even if it’s normally a read/write filesystem. |
| –v       | As with many commands, this option produces verbose output—the program provides comments on operations as they occur. |
| –w       | This parameter causes Linux to attempt to mount the filesystem for both read and write operations. This is the default for most filesystems, but some experimental drivers default to read-only operation. |