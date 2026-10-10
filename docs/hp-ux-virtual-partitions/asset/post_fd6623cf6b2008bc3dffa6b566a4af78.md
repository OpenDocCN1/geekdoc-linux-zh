
Next is an example of running **lsdev** on the same Series 800 on which **ioscan** was run:

(on Series 800)

```bash
$ /usr/sbin/lsdev
```

| Character | Block | Driver | Class |
| :--- | :--- | :--- | :--- |
| 0 | -1 | cn | pseudo |
| 1 | -1 | asio0 | tty |
| 3 | -1 | mm | pseudo |
| 16 | -1 | ptym | ptym |
| 17 | -1 | ptys | ptys |
| 28 | -1 | diag0 | diag |
| 46 | -1 | netdiag1 | unknown |
| 52 | -1 | lan2 | lan |
| 64 | 64 | lv | lvm |
| 69 | -1 | dev_config | pseudo |
| 72 | -1 | clone | pseudo |
| 73 | -1 | strlog | pseudo |
| 74 | -1 | sad | pseudo |
| 75 | -1 | telm | strtelm |
| 76 | -1 | tels | strtels |
| 77 | -1 | t1ctl1s | pseudo |
| 78 | -1 | t1cots | pseudo |
| 79 | -1 | t1cotsod | pseudo |
| 114 | -1 | ip | pseudo |
| 116 | -1 | echo | pseudo |
| 119 | -1 | dlpi | pseudo |
| 130 | -1 | rawip | pseudo |
| 136 | -1 | 1pr0 | unknown |
| 137 | -1 | udp | pseudo |
| 138 | -1 | stcpgmap | pseudo |
| 139 | -1 | nuls | pseudo |
| 140 | -1 | netga | pseudo |
| 141 | -1 | tun | pseudo |
| 142 | -1 | btlani3 | unknown |
| 143 | -1 | fddil3 | unknown |
| 144 | -1 | fddi0 | unknown |
| 156 | -1 | pttm | strpttm |
| 157 | -1 | ptm | strptys |
| 159 | -1 | ps2 | ps2 |
| 164 | -1 | pipedev | unknown |
| 168 | -1 | beep | graf_pseudo |
| 174 | -1 | framebuffer | graf_pseudo |
| 188 | 31 | sdisk | disk |
| 189 | -1 | klog | pseudo |
| 193 | -1 | mux2 | tty |
| 203 | -1 | sctl | ctl |
| 205 | -1 | tape | tape |
| 207 | -1 | sy | pseudo |
| 216 | -1 | CentIF | ext_bus |
| 227 | -1 | kept | pseudo |
| 229 | -1 | ite | graf_pseudo |

And last, here is an example of running **lsdev** on the same V-class server on which the first **ioscan** was run:

```bash
$ /usr/sbin/lsdev
                              (on V-Class)
```

| Character | Block | Driver | Class |
| :--- | :--- | :--- | :--- |
| 0 | -1 | cn | pseudo |
| 3 | -1 | mm | pseudo |
| 16 | -1 | pty0m | pty0m |
| 17 | -1 | pty1e | pty1e |
| 27 | -1 | dmem | pseudo |
| 28 | -1 | diag0 | diag |
| 46 | -1 | netdiag1 | unknown |
| 64 | 64 | lv | lvm |
| 69 | -1 | dev_config | pseudo |
| 72 | -1 | clone | pseudo |
| 73 | -1 | strlog | pseudo |
| 74 | -1 | sad | pseudo |
| 75 | -1 | telm | strtelm |
| 76 | -1 | tels | strtels |
| 77 | -1 | ticlts | pseudo |
| 78 | -1 | tlcots | pseudo |
| 79 | -1 | tlcootad | pseudo |
| 114 | -1 | ip | pseudo |
| 115 | -1 | arp | pseudo |
| 116 | -1 | echo | pseudo |
| 119 | -1 | dlpi | pseudo |
| 130 | -1 | rawip | pseudo |
| 136 | -1 | tcp | pseudo |
| 137 | -1 | udp | pseudo |
| 138 | -1 | stopmap | pseudo |
| 139 | -1 | nuls | pseudo |
| 140 | -1 | netgq | pseudo |
| 141 | -1 | tun | pseudo |
| 142 | -1 | fddi4 | unknown |
| 143 | -1 | fc71_ctl | lan |
| 144 | -1 | fcgsc_lan | lan |
| 145 | -1 | lpr0 | unknown |
| 156 | -1 | ptm | strptym |
| 157 | -1 | pts | strptys |
| 164 | -1 | pipedev | unknown |
| 169 | -1 | conspl | tty |
| 170 | -1 | btlam6 | lan |
| 171 | -1 | fcp | fcp |
| 188 | 31 | sdisk | disk |
| 189 | -1 | klog | pseudo |
| 203 | -1 | sctl | ctl |
| 205 | -1 | stape | tape |
| 207 | -1 | sy | pseudo |
| 227 | -1 | kepd | pseudo |
| 232 | -1 | diag2 | diag |

From these three **lsdev** outputs, you can observe some minor differences in the devices. The Series 700, for instance, has such classes as audio and floppy, the Series 800 has a multiplexer, and the V-Class has a BaseTen network card.

You can use **ioscan** to show the device files for a particular peripheral. Going back to the Series 800 that had four disks and a CD-ROM attached to it, you could issue the following **ioscan** command to see the device files associated with *disk*:

(on Series 800)

```bash
$ /usr/sbin/ioscan -fn -C disk
```

| Class | I H/W Path | Driver | S/W State | H/W Type | Description |
| :---- | :--------- | :----- | :-------- | :------- | :---------- |
| disk | 0 10/0.3.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t3d0 | | /dev/rdisk/c0t3d0 | |
| disk | 1 10/0.4.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t4d0 | | /dev/rdisk/c0t4d0 |
| disk | 2 10/0.5.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t5d0 | | /dev/rdisk/c0t5d0 |
| disk | 3 10/0.6.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t6d0 | | /dev/rdisk/c0t6d0 |
| disk | 3 10/12/5/2.0 | sdisk | CLAIMED | DEVICE | CD-ROM |
|      |              | /dev/dsk/c1t2d0 | | /dev/rdisk/c1t2d0 |

You can see from this **ioscan** all of the device files associated with *disk*, including the CD-ROM.

You could find out more information about one of these devices with the **diskinfo** command. Specify the character device you want to know more about, as shown below (using the *-v* option for verbose provides more detailed information).

```bash
$ diskinfo /dev/rdsk/c0t5d0
SCSI describe of /dev/rdsk/c0t5d0
    vendor: HP
    product id: C2490WD
    type: direct access
    size: 2082636 bytes
bytes per sector: 512
```

## An Example of Adding a Peripheral

In this section, we'll construct a device file for a tape drive. Chapter 9 covers the process of using device files and all Logical Volume Manager commands for adding disk devices that you may want to view as well. Before we construct a device file, let's view two existing device files on the Series 700 and see where some of this information appears. The first long listing is that of the tape drive, and the second is the disk, both of which are on the Series 700 in the earlier listings.

```bash
$ ll /dev/rmt/0m
(on Series 700)
crw-rw-rw-  2 bin bin  205 0x003000 Feb 12 03:00 /dev/rmt/0m
```

```bash
$ ll /dev/dsk/c0t1d0
(on Series 700)
brw-r-----  1 bin sys  31 0x001000 Feb 12 03:01 /dev/dsk/c0t1d0
```

The tape drive device file, **/dev/rmt/0m**, shows a major number of 205, corresponding to that shown for the character device driver *stape* from `lsdev`. The disk drive device file, **/dev/dsk/c0t6d0**, shows a major number of 31, corresponding to the *block* device driver *fsdisk* from `lsdev`. Since the tape drive requires only a character device file, and no major number exists for a block *stape* device, as indicated by the - *I* in the block column of `lsdev`, this file is the only device file that exists for the tape drive. The disk, on the other hand, may be used as either a block device or a character device (also referred to as the *raw device*). Therefore, we should see a character device file, /dev/rdsk/c0t6d0, with a major number of 188, as shown in `lsdev` for *fsdisk*.

(on Series 700)

```bash
$ ll /dev/rdsk/c0t6d0

crw-r----- 1 root sys 188 0x001000 Feb 12 03:01 /dev/rdsk/c0t6d0
```

We can now create a device file for a second tape drive, this time at SCSI address 2, and a disk device file for a disk drive at SCSI address 5, using the `mksf` command. You can run `mksf` two different ways. The first form of `mksf` requires you to include less specific information, such as the minor number. The second form requires you to include more of this specific information. Some of these arguments relate only to the specific form of `mksf` you use.

- `-d`
    Use the device driver specified. A list of device drivers is obtained with the `lsdev` command.
- `-C`
    The device specified belongs to this class. The class is also obtained with the `lsdev` command.
- `-H`
    Use the hardware path specified. Hardware paths are obtained with the `ioscan` command.
- `-m`
    The minor number of the device is supplied.
- `-r`
    Create a character, also known as a raw device file. The default is to create a block file.
- `-v`
    Use verbose output, which prints the name of each special file as it is created.

We will now create the device files for a disk drive. Both a block and a character device file are required. The 0x005000 in the example corresponds to the address of 5 on the disk drive. This number, used in both the block and character device files, is unique for every disk drive created.

We can now create a block device file for a disk at SCSI address 5 using the following `mksf` command:

(on Series 700)

```bash
$ /sbin/mksf -v -C disk -m 0x005000 /dev/dsk/c0t5d0
making /dev/dsk/c0t5d0 b 31 0x005000
```

Similarly, we can now create a character device file for a disk at SCSI address 5 using form two of `mksf`:

(on Series 700)

```bash
$ /sbin/mksf -v -r -C disk -m 0x005000 /dev/dsk/c0t5d0
making /dev/rdsk/c0t5d0 c 188 0x005000
```
