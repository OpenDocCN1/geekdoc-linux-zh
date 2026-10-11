**WARNING!** It is important not to physically remove any temporary media from your PC until after the media has been properly unmounted. Not all information is written to disk right away—some is held in memory until the next time it is necessary to write to it. Part of the process of unmounting a device is making sure those last pieces of information are included.

+   2. Type “umount *mountpoint*” or “umount *device*”. For example, **umount /dev/fd0** and **umount /mnt/floppy** both unmount a disk from the first floppy drive.

+   3. Physically remove the media.

# Adding Permanent Media

On a day-to-day basis you likely will not be pulling hard drives in and out of a machine—unless you use removable rack drives—but there are times when you may need to add one. When this occurs, do the following:

+   1. Make a note of what kind of device this is. For example, is it a SCSI or IDE hard drive?

+   2. Physically add the media to the system.

+   3. Make a note of where the media is in the system. Is it the third SCSI drive, for example, or is it the second IDE drive?

+   4. Log in as root.

+   5. Type “cp /etc/fstab /etc/fstab.backup” to create a backup of the master file system controller.

+   6. Type “vi /etc/fstab” to open the master file system controller for editing.

+   7. Type “G” to go to the end of the file.

+   8. Type “o” to open a new line at the end.

+   9. A line in */etc/fstab* is presented in the following manner:

```
device  mountpoint  type  options  dump  order
```

Determine which device the new portion of the file system resides on. For example, if you just added a new drive to the SCSI chain and it’s the third hard drive on the chain, then it is */dev/sdc*. However, that is not specific enough. Once you have partitioned and made a file system on the device, you will know which partition you want to mount. For example, to mount the second partition on the third SCSI drive, the device would be */dev/sdc2*.

+   10. The mount point for a permanent segment of the file system does not tend to be within the */mnt* hierarchy. Instead, the device fits seamlessly into the file system. For example, if you created a */boot* partition during the installation process, that partition looks like a directory to anyone who does a file