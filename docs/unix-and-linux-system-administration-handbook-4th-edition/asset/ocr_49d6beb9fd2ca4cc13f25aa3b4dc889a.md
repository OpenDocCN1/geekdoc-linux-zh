For matching rules, the assignment_clauses specify the actions udevd should take to handle the event. Their format is similar to that for match clauses.

The most important assignment key is NAME, which indicates what udev should name the device. The optional SYMLINK assignment key creates a symbolic link to the device through its desired path in /dev.

Let's put these components together with an example: a USB flash drive. Suppose that we want to make the drive's device name persist across insertions and that we want the drive to be mounted and unmounted automatically.

To start with, we insert the flash drive and check to see how the kernel identifies it. There are a couple of ways to do this. By running the lsusb command, we can inspect the USB bus directly:

```
ubuntu$ lsusb
Bus 001 Device 007: ID 1307:0163 Transcend, Inc. USB Flash Drive
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
```

Alternatively, we can check for log entries submitted to /var/log/messages. In our case, the attachment leaves an extensive audit trail:

```
Aug  9 19:50:03 ubuntu kernel: [42689.253554] scsi 8:0:0:0: Direct-Access
Ut163 USB2FlashStorage 0.00 PQ: 0 ANSI: 2
Aug 9 19:50:03 ubuntu kernel: [42689.292226] sd 8:0:0:0: [sdb] 1974271 512-byte hardware sectors: (1.01 GB/963 MiB)
...
Aug 9 19:50:03 ubuntu kernel: [42689.304749] sd 8:0:0:0: [sdb] 1974271 512-byte hardware sectors: (1.01 GB/963 MiB)
Aug 9 19:50:03 ubuntu kernel: [42689.307182] sdb: sdb1
Aug 9 19:50:03 ubuntu kernel: [42689.427785] sd 8:0:0:0: [sdb] Attached SCSI removable disk
Aug 9 19:50:03 ubuntu kernel: [42689.428405] sd 8:0:0:0: Attached scsi generic sg3 type 0
```

The log messages above indicate that the drive was recognized as sdb, which gives us an easy way to identify the device in /sys. We can now examine the /sys filesystem with udevadm in search of some rule snippets that are characteristic of the device and might be usable in udev rules.

```
ubuntu$ udevadm info -a -p /block/sdb1
looking at device '/devices/pci0000:00/0000:00:11.0/0000:02:03.0/usb1/1-1/1-1:1.0/host30/target30:0:0/30:0:0:0/block/sdb/sdb1':
  KERNEL=="sdb1"
  SUBSYSTEM=="block"
  DRIVER==""
  ATTR{partition}=="1"
  ATTR{start}=="63"
  ATTR{size}=="1974208"
  ATTR{stat}==""
  0    512    808    792    1857    808    0    0    0    0
```