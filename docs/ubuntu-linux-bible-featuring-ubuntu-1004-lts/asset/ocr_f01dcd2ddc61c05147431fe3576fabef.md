# Part II: Ubuntu for Desktop Users

```
fuseblk
nodev fusectl
nodev mqueue
nodev rpc_pipefs
nodev nfs
nodev nfs4
nodev nfsd
nodev cifs
nodev binfmt_misc
```

+   - Filesystems whose types are preceded by a nodev entry are not associated with physical devices, but are used internally by applications and the operating system.
- The fourth field contains a comma-separated list of options to the mount command that should be used when the filesystem is mounted. Many mount options are filesystem-specific, but some common ones are the following:
  - async: Writes to the filesystem should be done asynchronously.
  - auto: The filesystem should be automatically mounted when detected or when a command as mount -a is executed.
  - defaults: The default options -async, auto, dev, exec, nouser, rw, suid are used.
  - dev: The character or block device containing the filesystem is local to the system.
  - exec: You can execute programs, scripts, or anything else whose permissions indicate that it is executable—from that filesystem.
  - gid-value: Set the group ID of the mounted filesystem to the specified numeric group ID when the filesystem is mounted.
  - noatime: Do not update file timestamps in the inode for a file when the file is simply being accessed. Not updating this timestamp can provide significant performance improvements.
  - noauto: Don't automatically mount when a filesystem is detected or when the command mount -a is issued. Usually with removable media such as floppies and CD-ROMs.
- nouser: You must be root to mount the filesystem — the filesystem can't be mounted by any non-root user.
- owner: The ownership of the filesystem is set to the user who mounted it — usually if root the filesystem is automatically mounted by the system.
- ro: Mount the filesystem read-only.
- rw: Mount the filesystem read-write.
- suid: Allow programs on the filesystem to change the user's or group ID when they are executed if their permission bits indicate that they should do. Be very careful when using this option with imported filesystems that you don't actually

120