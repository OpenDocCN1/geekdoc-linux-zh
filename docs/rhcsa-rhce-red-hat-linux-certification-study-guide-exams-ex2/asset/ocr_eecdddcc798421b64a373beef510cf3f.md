When the GRUB configuration file is changed, no additional commands are required. The pointer from the MBR automatically reads the current version of the /boot/grub/grub.conf file.

# Effects of GRUB Errors

An error in the GRUB configuration file can result in an unbootable system. For example, identifying the wrong volume as the root partition (/) can lead to a kernel panic. Other configuration errors in /boot/grub/grub.conf can also cause a kernel panic during the boot process.

Now that you've analyzed the GRUB configuration file, you can probably visualize some of the effects of errors in this file. If some of the filenames or partitions are wrong, GRUB won't be able to find critical files such as the Linux kernel.

First, if the root (hdX,Y) directive does not point to the /boot directory, you'll see one of three possible error messages, described in Table 5-1.

If the GRUB configuration file is completely missing, you'll see a prompt similar to this:

```
grub>
```

![](bbox=[0.07, 0.58, 0.2, 0.7])

> It's possible to get to a grub> prompt from within Linux with the grub command. However, that option does not include command completion features; and some commands provide different information when Linux is running.

**TABLE 5-1 GRUB Error Messages**

| Message | Description |
|---|---|
| Error 15: File not found | The partition was mounted; the kernel was not found on that partition. Cause: root (hdX,Y) directive does not point to the partition with the /boot directory. |
| Error 17: Cannot mount selected partition | The partition is not formatted to a filesystem with files. Cause: The root (hdX,Y) directive points to a partition formatted to a system such as Linux swap. |
| Error 22: No such partition | There is no partition specified by the root (hdX,Y) directive. |