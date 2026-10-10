MILO> help var
Variables that MILO cares about:
`MEMORY_SIZE` - System memory size in megabytes
`BOOT_DEV` - Specifies the default boot device
`BOOT_FILE` - Specifies the default boot file
`BOOT_STRING` - Specifies the boot string to pass to the kernel
`SCSIn_HOSTID` - Specifies the host id of the n-th SCSI controller.
`PCI_LATENCY` - Specifies the PCI master device latency
`AUTOBOOT` - If set, MILO attempts to boot on powerup and enters command loop only on failure.
`AUTOBOOT_TIMEOUT` - Seconds to wait before auto-booting on powerup.

**BEWARE** of setting AUTOBOOT without setting the timeout, you can end up automatically booting after a timeout of 0 seconds which may not be what you want.

PCILLATENCY is the number of PCI bus cycles that PCI bus mastering device hangs onto the PCI bus for once it has control. The default value for this is 32 and the maximum value is 255. Setting a high value means that each time a device gets control of the PCI bus it can transfer more data. However, setting it high also means that devices may have to wait longer to get control.

# D.6.2 Booting Linux

The boot command boots a linux kernel from a device. You will need to have a linux kernel image on an EXT2 formatted disk (SCSI, IDE or floppy) or an ISO9660 formatted CD available to MILO. The image can be gzip’d and in this case MILO will automatically gunzip it. Early versions of MILO recognised a gzip’d file by the .gz suffix but later MILOs look for magic numbers in the image.

You should note that the version of MILO does not usually have to match the version of the Linux kernel that you are loading. You boot Linux using the following command syntax:

```
MILO> boot [-t file-system] device-name:file-name \
[[boot-option] [boot-option] ...]
```

Where `device-name` is the name of the device that you wish to use and