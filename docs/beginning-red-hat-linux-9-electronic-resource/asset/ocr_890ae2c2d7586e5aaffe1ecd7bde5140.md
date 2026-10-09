This is how to read the line:

+   - The first field (/dev/hde1) is the device to be mounted
+   - The second field (/mnt/flash) is the mount point
+   - The third field (auto) will try to detect automatically the **file system type** on the device, for example *vfat* (very likely) or *ext3*
+   - In the fourth field, *noauto* prevents the device from being mounted automatically when the system is started. Also, *user* is the *crucial* option: it is this setting that allows normal users to mount the device

The rest of the line is not relevant to our example and can be ignored. You can find out more with man fstab.

+   4. Congratulations! Now the CompactFlash card can be mounted and unmounted by normal users without root’s intervention. To test this out, log in as a normal user and select Main Menu | System Tools | Disk Management. The User Mount Tool dialog will appear with the newly added device:

![](bbox=[0.3, 0.41, 0.7, 0.58])

At this point you can mount or unmount it pressing the appropriate button and browse its contents through the file manager.

+   5. You can try from a normal user terminal as well:

```
$ mount /mnt/flash
$ ls -l /mnt/flash
total 2
drwxrwx-x    4 eziodm     eziodm         2048 Nov  9 12:35 dcm
$ umount /mnt/flash
```

As an extra bonus, files stored in the CompactFlash card are owned by the user who mounted the device.