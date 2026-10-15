
You can list multiple filesystem entries on the command line to check. Filesystems can be referenced using the device name, the mount point in the virtual directory, or a special UUID value assigned to the filesystem.

## Tip

Although journaling filesystems users do need the `fsck` command, it is arguable as whether COW filesystems users do. In fact, the ZFS filesystem does not even have an interface to the `fsck` utility.

The `fsck` command uses the `/etc/fstab` file to automatically determine the filesystem on a storage device that isn't normally mounted. As just if you created a filesystem on a new storage device, you need to use the `-t` command line option to specify the filesystem type. Table 8.4 lists the other command line options.

Table 8.4 The `fsck` Command Options

| Option | Description |
| --- | --- |
| `-a` | Automatically repairs the filesystem if errors are detected |
| `-A` | Checks all the filesystems listed in the `/etc/fstab` file |
| `-C` | Displays a progress bar for filesystems that support that feature (only ext2 and ext3) |
| `-N` | Doesn't run the check, only displays what checks would be performed |
| `-r` | Prompts to fix if errors found |
| `-R` | Skips the root filesystem using the `-A` option |
| `-s` | If checking multiple filesystems, performs the checks one a time |
| `-t` | Specifies the filesystem type to check |
| `-T` | Doesn't show the header |
| `-V` | Produces verbose output |
| `-y` | Automatically repairs the filesystem |

## Tip

This method of mounting a filesystem only temporarily mounts the filesystem. When you reboot your Linux system, the filesystem doesn’t automatically mount. To force Linux to automatically mount the new filesystem at boot time, add the new filesystem to the `/etc/fstab` file.

Now that the filesystem is mounted within the virtual directory system, it can start to be used on a regular basis. Unfortunately, with regular use comes the potential for serious problems, such as filesystem corruption. The next section looks at how to deal with these issues.

### Checking and repairing a filesystem

Even with modern filesystems, things can go wrong if power is unexpectedly lost, or if a wayward application locks the system while file access is in. Fortunately, some command line tools are available to help you make an attempt to restore the filesystem back to order.

Each filesystem has its own recovery command for interacting with the filesystem. That has the potential of getting ugly, because more and more filesystems are available in the Linux environment, making for lots of individual commands you have to know. Fortunately, a common front-end program available can determine the filesystem on the storage device and use the appropriate filesystem recovery command based on the filesystem being recovered.

The `fsck` command is used to check and repair most Linux filesystem types, including ones discussed earlier in this chapter — ext, ext2, ext3, ext4, Reiser4, JFS, and XFS. The format of the command is:

```
fsck options filesystem
```
