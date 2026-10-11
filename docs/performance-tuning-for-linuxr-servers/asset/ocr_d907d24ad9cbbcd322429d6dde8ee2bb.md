```
# fdisk /dev/sda
Command (m for help): p
Device boot Start End Blocks Id System
/dev/sd1a 1 523 420097 83 Linux
/dev/sda5 524 1106 4682947 83 Linux
Disk /dev/sda: 255 heads, 63 sectors, 1106 cylinders
Units = cylinders of 16065 * 512 bytes
Command (m for help): q
# Table 1. Linux raw I/O calculations.
The number of pages in /dev/sda5 is
num_pages = ((1106-524+1)*16065*512)/4096
num_pages = 11170736
```

2. Bind an unused raw device node to this partition. This step needs to be done every time the machine is rebooted, and it requires root access. Use `raw -a` to see which raw device nodes are already in use:

```
# raw /dev/raw/raw1 /dev/sda5
/dev/raw/raw1: bound to major 8, minor 5
```

3. Set the appropriate read permissions on the raw device controller and the disk partition. Set the appropriate read and write permissions on the raw device. The raw device is now ready to be used.