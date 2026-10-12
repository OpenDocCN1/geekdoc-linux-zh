If you're setting up a dual-boot system where /dev/hda1 contains the Windows NT/2000 operating system and /dev/hda2 contains the Linux operating system, make sure your /etc/lilo.conf looks like the above. After you've edited the lilo.conf file, make sure that you run /sbin/lilo to find out if LILO likes the configuration file.

If you get an error message stating a problem with the “liner” line, change that line to lba32, which is used to use logical block addressing to access disk, and then rerun /sbin/lilo. When LILO is happy it will show a line such as the following:

```
* Added linux
* Added win2k
```

Now you should reboot your system by running /sbin/shutdown -r now and choosing one of the operating systems from the boot menu. Make sure that you test-boot into both operating systems to ensure that you are able to successfully dual-boot your system to either Linux or Windows.

# Dual-booting by using NTLoader

There is no technical advantage to dual-booting by using the Windows NT/2000 boot loader – NTLoader – over LILO. However, if you're using Linux as a secondary operating system and want to keep it under a low profile, you might want to use NTLoader instead of LILO. NTLoader is often used in Windows NT/2000 environments where users are already familiar with NTLoader. Before you can dual-boot Linux and Windows NT/2000 with NTLoader, you must ensure that the following prerequisites are met:

+   - Windows NT/2000 must be installed on the first partition of the first disk. Here I assume that you are using an IDE disk and that Windows NT/2000 therefore is installed on /dev/hda1 (for SCSI, the equivalent is /dev/sda1).
+   - Windows NT/2000 has installed the NTLoader in MBR, which is what the Windows NT/2000 installer does by default.
+   - You have Windows NT/2000 recovery disk set.
+   - Linux is installed on any partition of any disk other than the first partition of the first disk. Here I will assume that you have installed Linux on /dev/hda2. Note that you could also have Linux installed