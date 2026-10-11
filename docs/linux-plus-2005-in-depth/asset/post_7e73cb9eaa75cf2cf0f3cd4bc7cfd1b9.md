
and continue the boot process. The mkbootdisk command can be used to create a boot disk after installation; to create a boot disk with the 2.6.5-1.358 kernel on it, you can use the command mkbootdisk 2.6.5-1.358 at the command prompt and insert a blank floppy disk when prompted. This boot disk can then be used to boot into a system such that the boot loader can be repaired.

Because the operating system transfers data to and from the hard disk frequently, the file-system can become corrupted over time; a corrupted filesystem can be identified by very slow write requests, errors printed to the console, or failure to mount. If the filesystem on a partition mounted to a noncritical directory, such as /home or /var, becomes corrupted, you should perform the following troubleshooting steps:

-   1.  Unmount the filesystem if mounted.
-   2.  Run the fsck command with the -f (full) option on the filesystem device.
-   3.  If the fsck command cannot repair the filesystem, use the mkfs command to re-create the filesystem.
-   4.  Restore the original data for the filesystem using a back-up utility.

![](img/09bf13b782f71165e17bb3839040c96a_517_0.png)

> **NOTE**
>
> Do not restore data onto a damaged filesystem; ensure that the filesystem has been re-created first.

If the / filesystem becomes corrupted, the system is unstable and must be turned off. Following this, you can use a copy of Linux on the installation media to remedy the problem using the following troubleshooting steps:

-   1.  Place the first Red Hat Fedora installation CD-ROM in the CD-ROM drive and turn on the computer.
-   2.  At the welcome screen shown in Figure 13-5, type linux rescue and press Enter. When prompted for language and keyboard layout, choose English and US (us), respectively. When prompted to start the network, choose No.
-   3.  At the screen depicted in Figure 13-6, choose Skip to enter a shell for the Linux system on the CD-ROM, as shown in Figure 13-7. This system contains utilities in the /usr/bin and /usr/sbin directories that can restore the filesystem on the hard disk.
-   4.  Use the mkfs command on the CD-ROM Linux system to create a new / filesystem on the appropriate partition on the hard disk.
-   5.  Use a back-up utility on the CD-ROM Linux system (tar, dump, or cpio) to restore the original data to the re-created / filesystem.
-   6.  Type exit at the shell prompt to reboot the system.

![](img/09bf13b782f71165e17bb3839040c96a_518_0.png)

FIGURE 13-5 The Red Hat Fedora Linux installation welcome screen

![](img/09bf13b782f71165e17bb3839040c96a_518_1.png)

FIGURE 13-6 Obtaining a shell in rescue mode

```bash
bash-2.05b# cd /usr/sbin
-bash-2.05b: cd: /usr/sbin: No such file or directory
-bash-2.05b# ls
arp                 c2label             ifconfig          mke2fs            modinfo           restore
badblocks           fdisk             insmod            mkfs.ext2         modprobe          sfdisk
fsck                fsck.ext2         jfs_fsck          mknod             mount           trace
fsck.jfs            load_policy        mkfs.jfs          mdev              tune2fs
fsck.reiserfs       lsvfs             mkfs.vfat         reiserfsck        xfs_check
fsck.xfs            lvm               mkfs.xfs          resize2fs         xfs_db
antiqq              lvs.static        mfs.xfs           restore           xfs_repair
dump                hdmv              mknod             rmmod
dump                lock              mkdosfs           mkswap
route
-bash-2.05b#
```

**FIGURE 13-7** *The command-line shell used in rescue mode*

Some Linux administrators prefer to download a bootable CD-based Linux distribution that contains more filesystem repair utilities than the first Red Hat Fedora installation CD-ROM. Many small Linux distributions are available on the Internet that are designed for this purpose; two examples are **Knoppix Linux** (http://www.knoppix.org) and **BBC Linux** (http://www.lnx-bbc.org). Simply download the ISO image for the Linux distribution and burn the image to a CD-ROM using burning software. Following this, you can boot the computer using this CD-based Linux distribution and use the utilities on it to repair your filesystem and restore the files from backup.

Another common problem encountered on Linux systems is improper serial port configuration. Modem devices are identified as serial devices to the system; however, many modems use the same IRQ and I/O address settings as a serial port that is connected to the mainboard of the computer, which results in parameter conflicts. In addition, some serial devices such as serial printers and terminal stations require communication at a set speed, rather than the default speed of 115 KB/s for most serial ports. To remedy these problems, you can use keyword arguments to the `setserial` command to set the IRQ I/O address, and speed of a specified serial device. For example, to set the IRQ of the first serial port (/dev/ttyS0) to 11 and the I/O address to 0x03F8, and view the results, you can use the following commands:

```bash
[root@server1 root]# setserial /dev/ttyS0 irq 11 port 0x03F8
[root@server1 root]# setserial /dev/ttyS0
/dev/ttyS0, UART: 16550A, Port: 0x03F8, IRQ: 11
[root@server1 root]#
```

Table 13-1 lists other keywords that can be used with the setserial command.

### **Performance Monitoring**

Table 13-1 **Common keywords used with the setserial utility**

| Option | Description |
| :--- | :--- |
| port n | Sets the I/O address to n for a serial device |
| irq n | Sets the IRQ to n for a serial device |
| auto_irq | Attempts to automatically detect the IRQ setting for a serial device |
| spd_hi | Sets the speed of a serial port to 56KB/s |
| spd_vhi | Sets the speed of a serial port to 115KB/s |
| spd_normal | Sets the speed of a serial port to 38.4KB/s |

Some problems that you will encounter on a Linux system are not as noticeable as those discussed in the previous section; such problems affect the overall performance of the Linux system. Like the problems discussed earlier, performance problems can be caused by software or hardware or a combination of the two.

Hardware that is improperly configured might still work, but at a slower speed. In addition, when hardware ages, it might start to malfunction and send large amounts of information to the CPU when not in use; this process is known as **jabbering** and can slow down a CPU and, hence, the rest of the Linux system. To avoid this hardware malfunction, most companies retire computer equipment after two to three years of use.

Software can also affect the overall performance of a system; software that requires too many system resources monopolizes the CPU, memory, and peripheral devices. Poor performance can also be the result of too many processes running on a computer, processes that make a great deal of read/write requests to the hard disk (such as databases), or rogue processes. To remedy most software performance issues, you can remove software from the system to free up system resources; if this software is needed for business activity, you can instead choose to move the software to another Linux system that has more free system resources.

Software performance problems can also sometimes be remedied by altering the hardware. Upgrading or adding another CPU allows the Linux system to execute processes faster and reduce the number of processes running concurrently on the CPU. Alternatively, some peripheral devices can perform a great deal of processing that is normally performed by the CPU; this is known as **bus mastering**. Using bus mastering peripheral components reduces the amount of processing the CPU must perform and, hence, increases system speed.

Adding RAM to the computer also increases system speed as processes will have more working space in memory and the system will swap much less information to and from the hard disk. Because the operating system, peripheral components, and all processes use RAM constantly, adding RAM to any system often has a profound impact on system performance.
