# The Linux Boot Process

The first step in the Linux boot process is loading the kernel. The kernel is generally found in the /boot directory and will be referenced by the boot loader. Modern Linux distributions will usually use the Grand Unified Boot Loader (GRUB), some (notably Slackware) will still use the Linux Loader (LILO). Both serve the same purpose: loading the kernel and initiating system boot up. Let's look at some relevant entries from a sample grub.conf file:

```
default=
timeout=5
```

This indicates that the default grub entry that will be booted after a 5-second delay is 0 (the first, and in our case, only).

```
title Fedora (2.6.23.1-42.fc8)
```

This is the title that will be displayed at the boot menu for this particular GRUB entry (also known as a *stanza*)

```
root (hd0,0)
```

This tells GRUB which physical device to look for the following data on; hd0, is the first hard drive and the first partition. A dual boot or multi-drive system may have different values, but this is the norm:

```
kernel /vmlinuz-2.6.23.1-42.fc8 root=/dev/VolGroup00/LogVol00 rhgb quiet
```

This line provides the kernel that will be booted if this stanza is selected, and the appropriate kernel boot options. You may recognize the boot options from /proc/cmdline in Chapter 6. If the output of /proc/cmdline from the running system differed from what was listed here, this would indicate that someone manually edited the boot options start up.

```
initrd /initrd-2.6.23.1-42.fc8.img
```

This provides the location of the initial ramdisk (initrd) that will be used at boot. A ramdisk will generally contain modules that are necessary for boot (device drivers, file system modules, logical volume modules, and so forth) that are required for boot but are not built directly into the kernel.

Once the boot loader loads the kernel, the kernel proceeds to initialize the system hardware before starting process 1, /sbin/init.