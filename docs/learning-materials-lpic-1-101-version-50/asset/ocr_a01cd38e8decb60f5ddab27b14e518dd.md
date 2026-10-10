You can get a list of all block devices connected to your system using `print devices`:

```
```
(parted) print devices
/dev/sdb (1999MB)
/dev/sda (120GB)
/dev/sdc (320GB)
/dev/mapper/cryptswap (4294MB)
```
```

To get information about all connected devices at once, you can use `print all`. If you wish to know how much free space there is in each one of them, you can use `print free`:

```
```
(parted) print free
Model: ATA CT120BX500SSD1 (scsi)
Disk /dev/sda: 120GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:
Number Start End Size Type File system Flags
      1 32.3kB 2097kB 2065kB Free Space
      2 2097kB 116GB 116GB primary ext4
        116GB 116GB 512B Free Space
      3 116GB 120GB 4295MB primary linux-swap(v1)
        120GB 120GB 2098kB Free Space
```
```

# ## Creating a Partition Table on an Empty Disk

To create a partition table on an empty disk, use the `mklabel` command, followed by the partition table type that you want to use.

There are many supported partition table types, but the main types you should know of are `msdos` which is used here to refer to an MBR partition table, and `gpt` to refer to a GPT partition table. To create an MBR partition table, type:

```
```
(parted) mklabel msdos
```
```

And to create a GPT partition table, the command is:

```
```
(parted) mklabel gpt
```
```