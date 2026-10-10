general directory location for most Linux systems is the `/mnt` and `/media` directories. The `/media` directory, typically, is used for the mounting of removable media (for example, floppy disks, CD/DVD drives, and USB/thumb drives). In addition, prior to mounting any storage device, a mount point directory needs to exist before executing the `mount` command.

```
mount /dev/sdb1 /mnt/morestorage
```

The Linux `mount` command includes extra arguments (for example, `sb` for superblock, `no log` for turning off journaling) that can be used, if necessary. To execute the additional arguments, the `-o` argument must be specified first. To specify a specific filesystem type, the `-t` argument should be used. In most cases, the `-t` option is not necessary. The Linux kernel, typically, will detect the type of filesystem of the storage device that you are attaching.

Depending on the type of device you are mounting, at some point of time in the future, you may wish to disconnect the mounted device from the local mount point. To perform this operation, the Linux `umount` command is used. To perform this operation, only one additional argument is required. This argument, where you attached the device, is the mount point.

```
umount /mnt/morestorage
```

> **Note**  
> The Linux `umount` command is spelled without the letter (n). Even though its purpose is to unmount the storage device, the actual command omits the letter n.

# /etc/fstab

To automatically mount a filesystem, the Linux professional needs to become very familiar with the `/etc/fstab` file, as shown in Figure 3.3. This text-based file contains the filesystems defined during the installation of the Linux distribution (for example, *root partition*, *swap partition*) and any new filesystems that you would like to mount on a permanent basis whenever the system is booted. Most Linux systems automatically mount removable devices such as CD/DVD, floppy disks, and USB devices.

The structure for adding a filesystem to the `/etc/fstab` file so that it can be mounted automatically at boot up contains the disk partition you want to mount, the directories mount point, the filesystem type, and other filesystem options (for example, *nolog*, *noatime*, and *noauto*).