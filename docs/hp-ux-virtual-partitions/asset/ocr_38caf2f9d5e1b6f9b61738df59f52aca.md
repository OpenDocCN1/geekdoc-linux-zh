| disk | 125 | 2/0/0.8.5.0.0.9.6 | sdisks | CLAIMED | DEVICE | HP OPEN-8 |
|---|---|---|---|---|---|---|
| disk | 178 | 2/0/0.8.0.0.9.7 | sdisks | CLAIMED | DEVICE | HP OPEN-8 |
| target | 22 | 2/0/0.8.0.0.0.10 | tgt | CLAIMED | DEVICE | HP |
| disk | 22 | 2/0/0.8.0.0.0.10.0 | sdisks | CLAIMED | DEVICE | HP OPEN-8 |
| disk | 179 | 2/0/0.8.0.0.0.11 | sdisks | CLAIMED | DEVICE | HP OPEN-8 |
| target | 23 | 2/0/0.8.0.0.0.11 | tgt | CLAIMED | DEVICE | HP DISK-SUBSYSTEM |
| disk | 23 | 2/0/0.8.0.0.0.11.0 | sdisks | CLAIMED | DEVICE | HP DISK-SUBSYSTEM |
| target | 24 | 2/0/0.8.0.0.0.12 | tgt | CLAIMED | DEVICE | HP DISK-SUBSYSTEM |
| disk | 23 | 2/0/0.8.0.0.0.12.0 | sdisks | CLAIMED | DEVICE | HP DISK-SUBSYSTEM |
| target | 25 | 2/0/0.8.0.0.0.13 | tgt | CLAIMED | DEVICE | HP DISK-SUBSYSTEM |
| disk | 23 | 2/0/0.8.0.0.0.13.0 | sdisks | CLAIMED | DEVICE | HP DISK-SUBSYSTEM |
| target | 26 | 2/0/0.8.0.0.0.14 | tgt | CLAIMED | DEVICE | HP DISK-SUBSYSTEM |
| disk | 24 | 2/0/0.8.0.0.0.14.0 | sdisks | CLAIMED | DEVICE | HP DISK-SUBSYSTEM |

| memory | 0 | 8 | memory | CLAIMED | MEMORY | Memory I/O Adapter |
|---|---|---|---|---|---|---|
| bus_adapter | 8 | 15 | bus_adapter | CLAIMED | BUS_XBUS | Core I/O Adapter |
| congapl | 0 | 15/2 | congapl | CLAIMED | INTERFACE | Built-in Serial Port DUART |
| tty | 1 | 15/2 | congapl | CLAIMED | INTERFACE | Built-in Serial Port DUART |
| unknown | -1 | 15/3 | unknown | UNCLAIMED | UNKNOWN | Built-in Ethernet |
| processor | 0 | 16 | processor | UNCLAIMED | PROCESSOR | Processor |
| processor | 1 | 18 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 2 | 21 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 3 | 23 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 4 | 24 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 5 | 26 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 6 | 29 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 7 | 32 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 8 | 34 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 9 | 37 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 10 | 39 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 11 | 40 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 12 | 42 | processor | CLAIMED | PROCESSOR | Processor |
| processor | 13 | 45 | processor | CLAIMED | PROCESSOR | Processor |

The next command that helps you when creating device files is `lsdev`. `lsdev` lists the drivers configured into your system. When adding a device file, you need to have the driver for the device configured into the system. If it is not configured into the system, you can use SAM to configure it, or you can use the manual kernel configuration process covered earlier. There are columns for the major number for a character device and block device, the driver name, and the class of the driver. The major number, character device, and other parameters are defined later. The following is an example of running `lsdev` on the same Series 700 on which `ioscan` was run:

(on Series 700)

```
```
$ /usr/sbin/lsdev
```

```

| Character | Block | Driver | Class |
|---|---|---|---|
| 0 | -1 | cn | pseudo |
| 1 | -1 | ansi0 | tty |