```
```
-bash-sh-2.05b is /usr/sbin
arp                     c2label                ifconfig             mke2fs                 modinfo                  restore
badblocks               fdisk                  insmod                 mkfs.ext2              modprobe                 sfdisk
fsck                   sfsck                  jfs_fsck               mknod                  mount                  trace
fsck.ext2              load_policy              mkfs.jfs                 mdev                 tune2fs
grep                   task_ext3                insmod                 mfs.mfsdos               predisk                  xfs_check
fsck.jfs               lsvfs                    mkfs.vfat                reisenfsck                 xfs_cpy
fsck.reiserfs          lvm                      mkfs.xfs                 resize2fs                  xfs_db
antisqueee             lvs.static               mfs.xfs                  restore                xfs_repair
dump                   hdmv                     mknod                  rmmod
dump                     lock                   mkdosfs                mkswap
route
-bash-sh-2.05b _
```
```

**FIGURE 13-7** *The command-line shell used in rescue mode*

Some Linux administrators prefer to download a bootable CD-based Linux distribution that contains more filesystem repair utilities than the first Red Hat Fedora installation CD-ROM. Many small Linux distributions are available on the Internet that are designed for this purpose; two examples are **Knoppix Linux** (http://www.knoppix.org) and **BBC Linux** (http://www.lnx-bbc.org). Simply download the ISO image for the Linux distribution and burn the image to a CD-ROM using burning software. Following this, you can boot the computer using this CD-based Linux distribution and use the utilities on it to repair your filesystem and restore the files from backup.

Another common problem encountered on Linux systems is improper serial port configuration. Modem devices are identified as serial devices to the system; however, many modems use the same IRQ and I/O address settings as a serial port that is connected to the mainboard of the computer, which results in parameter conflicts. In addition, some serial devices such as serial printers and terminal stations require communication at a set speed, rather than the default speed of 115 KB/s for most serial ports. To remedy these problems, you can use keyword arguments to the `setserial` command to set the IRQ I/O address, and speed of a specified serial device. For example, to set the IRQ of the first serial port (/dev/ttyS0) to 11 and the I/O address to 0x03F8, and view the results, you can use the following commands:

```
```
[root@server1 root]# setserial /dev/ttyS0 irq 11 port 0x03F8
[root@server1 root]# setserial /dev/ttyS0
/dev/ttyS0, UART: 16550A, Port: 0x03F8, IRQ: 11
[root@server1 root]# _
```
```

Table 13-1 lists other keywords that can be used with the setserial command.