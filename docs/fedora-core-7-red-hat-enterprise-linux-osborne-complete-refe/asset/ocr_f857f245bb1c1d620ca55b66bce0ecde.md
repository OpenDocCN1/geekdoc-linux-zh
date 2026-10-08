| Option | Description |
| --- | --- |
| async | Indicates that all I/O to the file system should be done asynchronously. |
| auto | Indicates that the file system can be mounted with the -a option. A mount -a command executed when the system boots, in effect, mounts file systems automatically. |
| defaults | Uses default options: rw, suid, dev, exec, auto, nouser, and async. |
| dev | Interprets character or block special devices on the file system. |
| fscontext | Sets SELinux file system context. |
| noauto | Indicates that the file system can only be mounted explicitly. The -a option does not cause the file system to be mounted. |
| exec | Permits execution of binaries. |
| managed | Removable device that is managed by HAL. Options for this device have to be specified in the HAL configuration files. |
| nouser | Forbids an ordinary (that is, nonroot) user to mount the file system. |
| owner | Allows only the owner to mount or unmount the device. |
| remount | Attempts to remount an already-mounted file system. This is commonly used to change the mount flags for a file system, especially to make a read-only file system wrtable. |
| ro | Mounts the file system as read-only. |
| rw | Mounts the file system as read/write. |
| suid | Allows set-user-identifier or set-group-identifier bits to take effect. |
| sync | Indicates that all I/O to the file system should be done synchronously. |
| user | Enables an ordinary user to mount the file system. Ordinary users always have the following options activated: noexec, nosuid, and nodev. |
| nodev | Does not interpret character or block special devices on the file system. |
| noexec | Does not allow execution of binaries on the mounted file systems. |
| nosuid | Does not allow set-user-identifier or set-group-identifier bits to take effect. |

Table 30-8 Mount Options for File Systems

# Partition Labels: e2label

Red Hat Enterprise Linux and Fedora use file system labels for ext2 and ext3 file systems on hard disk partitions. Thus in the/etc/fstab file previously shown, the first entry would use a label for its device name, as shown here. In this case, the label is the slash, /, indicating the root partition. You could change this device's label with e2label, but be sure to also change the/etc/fstab entry for it.

```
LABEL=/ / ext3 defaults 0 1
```