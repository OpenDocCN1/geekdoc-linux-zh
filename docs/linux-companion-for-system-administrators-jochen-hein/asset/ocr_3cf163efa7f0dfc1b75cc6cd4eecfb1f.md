# THE LINUX BOOT LOADER 49

+   - be installed as the boot sector in arbitrary primary partitions (except for swap) of the first hard disk.

In contrast, it cannot

+   - be installed on an MS-DOS floppy disk (or any other non-LINUX floppy disk),¹
- be installed in a logical partition, or
- be installed on another disk which is not the first hard disk.

This limitation is, however, not a real restriction for the design of a boot configuration, where LILO can load a kernel image from another disk which is not the first hard disk; it can also use arbitrary partitions, including logical drives, on another hard disks as the root file system.
The installation of LILO into the MBR or the boot sector evidently requires privileges. LILO is configured via the file /etc/lilo.conf. Before a final installation, you should first use /sbin/lilo -t to check whether the commands contained in the configuration file are known and syntactically correct, and whether the specified kernel files be found and the specified partitions exist.

# Configuring lilo

True, LILO also accepts parameters entered at the boot prompt, but in the normal case of a readily configured system, permanently required settings are passed via the configuration file /etc/lilo.conf. An example of this file is shown in Listing 3.1.

```
boot = /dev/hda2
compact
image = vmlinuz
image = vmlinuz.old
other = /dev/hda1
table = /dev/hda
label = mdsos
```

Listing 3.1 A very simple LILO configuration.

The LILO options can be divided into global and image-specific options. Global options concern all kernel files and function independently of the selected configuration; the other options only concern one of several bootable

1. Syslinux can be used for this purpose.