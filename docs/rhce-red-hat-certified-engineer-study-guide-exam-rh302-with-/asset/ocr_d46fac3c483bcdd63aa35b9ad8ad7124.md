```
image=/boot/vmlinuz-2.2.12-20b1
label=linux
root=/dev/hda4
read-only
```

```
other=/dev/hda1
label=dos
```

This configuration file includes stanzas. The first, consisting of the first six lines, specifies global parameters. Table 8.1 describes the global parameters that appear in the same configuration. Each remaining stanza describes a boot image LILO will offer for booting. The first two boot images are associated with Linux, and the final boot image is associated with Microsoft Windows. Table 8.2 describes the parameters used to specify a boot image.

Note that both Linux images refer to the same partition. This arrangement lets you choose the kernel to boot the system and is helpful when installing a new kernel. If the new kernel fails to work properly, you can use the LILO prompt to load the old kernel.

# TABLE 8.1 LILO Global Parameters

| LILO Global Parameter | Description |
| --- | --- |
| boot | Specifies the device or partition to which boot information will be written. To install LILO to the MBR, where it will act as the primary boot loader, specify a device (for example, /dev/hda). Alternatively, to install Linux to the boot sector of the partition, where it will act as a secondary boot loader, specify a partition (for example, /dev/hda3). |
| default | Specifies the default boot image |
| delay | Specifies the amount of time (in tenths of a second) that LILO will wait before booting the default boot image. |
| install | Specifies the file installed as the new boot sector. |