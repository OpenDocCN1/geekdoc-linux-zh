```
MILO> help var
Variables that MILO cares about:
MEMORY_SIZE  - System memory size in megabytes
BOOT_DEV     - Specifies the default boot device
BOOT_FILE    - Specifies the default boot file
BOOT_STRING  - Specifies the boot string to pass to the kernel
SCSI0_HOSTID - Specifies the host id of the n-th SCSI controller
AUTOBOOT     - If set, MILO attempts to boot on powerup
              and enters command loop only on failure.
AUTOBOOT_TIMEOUT - Seconds to wait before auto-booting on powerup.
```

# E.6.2 Booting Linux

The boot command boots a linux kernel from a device. You will need to have a linux kernel image on an EXT2 formatted disk (SCSI, IDE or floppy) or an ISO9660 formatted CD available to Milo. The image can be gzip'd and in this case Milo will recognise that it is gzip'd by the .gz suffix.

You should note that the version of Milo does not usually have to match the version of the Linux kernel that you are loading. You boot Linux using the following command syntax:

```
MILO> boot [-t file-system] device-name:file-name [boot-option(s)]
```

Where device-name is the name of the device that you wish to use and file-name is the name of the file containing the Linux kernel. All arguments supplied after the file name are passed directly to the Linux kernel.

If you are installing Red Hat, then you will need to specify a root device and so on. So you would use:

```
MILO> boot fd0:vmlinux.gz root=/dev/fd0 load_ramdisk=1
```

Milo will automatically contain the block devices that you configure into your vmlinux. I have tested the floppy driver, the IDE driver and the NCR SCSI driver, these work fine. Also, it is important to set the host id of the SCSI controller to a reasonable value. By default, MILO will initialize it to the highest possible value (7) which should normally work just fine.