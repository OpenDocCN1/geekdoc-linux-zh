
# v:4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

![](img/993644c785d68ca888a5ade02ca8088d_25_0.png)

Illustration 1: XFCE Removable Media Handling Configuration

v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

## II. Linux Disks, Partitions and the File System

As you go through the following pages, please pay attention to your userid...you'll need to be root for most of this.

## Disks

Linux treats devices as files. This is an important concept for forensic examiners. It means, as we will see later on, that many of the commands we can use on regular files, we can also use on disks "files". We can list them, hash and search them in the same way we do files in any standard user directory. The special directory where these device "files" are maintained is /dev. Older IDE disks were detected and assigned hd. We rarely see them anymore.

As we saw earlier, with the adoption of Udev, disks are not assigned device names dynamically, meaning that the names do not exist until the device (a thumb drive, for example) is connected to the system. Of when you boot a normally configured computer, you have at least one "boot" drive already connected. Under some circumstances, this will be named sda. These device nodes are populated by the /dev directory. The partitions (primary) are simply numbered.

When referring to the entire device, use /dev/sda. When referring to a partition on that disk, we use the disk name and the name of the partition, /dev/sda1 for example.

| DEVICE | FILE NAME |
| :--- | :--- |
| 1st disk (SATA, USB, etc.) | /dev/sda |
| - 1st Primary partition | /dev/sda1 |
| - 2nd partition | /dev/sda2, etc. |
| 2nd disk (SATA, USB, etc.) | /dev/sdb |
| - 1st Primary partition | /dev/sdb1 |
| - 2nd partition | /dev/sdb2, etc. |
| CDROM Drive | /dev/sr0 |

The pattern described above is fairly easy to follow. If you are using a standard SATA disk, it will be referred to as sdx where the x is replaced with an a for the first detected device and b for the second. In the same way, the CDROM or DVD drives connected via the SATA bus will be detected as /dev/sr0 and then /dev/sr1.

Note that the /dev/sdx device will include USB and Firmware devices. For example, a primary SATA disk will be assigned sda. It normally be detected as sdb, and so on.

A simple way to see the disks and partitions that are attached to your system is to use the lsblk command:

root@forensic1:~# lsblk

| NAME | MAJ:MIN | SIZE | RO | TYPE | MOPOINT |
| :--- | :--- | :--- | :--- | :--- | :--- |
| sda | 8:0 | 931.5G | 0 | disk | |
| - sda1 | 8:1 | 256M | 0 | part | /boot |
| - sda2 | 8:2 | 32G | 0 | part | [SWAP] |
| - sda3 | 8:3 | 899.3G | 0 | part | / |
| sdb | 8:16 | 238.5G | 0 | disk | |
| sdc | 8:32 | 931.5G | 0 | disk | |
| - sdc1 | 8:33 | 931.5G | 0 | disk | |
| sdi | 8:128 | 931.5G | 0 | disk | |
| - sdiil | 8:129 | 931.5G | 0 | part | /run/media/berry/Evid |
| sdj | 8:144 | 29.3G | 1 | disk | |
| - sdjj | 8:145 | 29.3G | 1 | part | /run/media/berry/Kingston |
| sr0 | 11:0 | 2.6G | 0 | rom | |

You can see from the output that disks and partitions are listed, and if any of the partitions are mounted, lsblk will also give you the current mount point. In this case /dev/sda1 is mounted on /boot, /dev/sda2 is our swap partition, /dev/sda3 is our root partition, and we /dev/sddi is mounted as /run/media/berry/Evid and /dev/sdjj mounted as /run/media/berry/Kingston. The last two are from external devices, plugged in via the desktop.

Another useful command that we use is lscsi. I prefer it because although it does not show partitions, it gives a better idea of what the values are

root@forensic1:~# lscsi
[1:0:0] disk ATA ST1000DM003-1ER16 CC45 /dev/sda
[2:0:0] cd/vda HD-LT-BD-RE WH16NS40 1.00 /dev/sr0
[11:0:0] disk ATA SAMSUNG MHPV25 500 /dev/sdb
[23:0:0] disk EX5 CF Kingston Reader 055 /dev/vdd
[23:0:1] disk EX5 SD Kingston Reader 055 /dev/sde
[23:0:2] disk EX5 MS Kingston Reader 055 /dev/sdf
[23:0:3] disk EX5 MSD Kingston Reader 055 /dev/sdg
[23:0:4] disk EX5 XD Kingston Reader 055 /dev/sdh
[28:0:0] disk ST1000DM003-1ER16 6207 /dev/sdc
[28:0:1] disk ST1000DM003-1ER16 6207 /dev/sddi
[32:0:0] disk DataTravel 3.0 PMAP /dev/sdj

You can see in the output above that this system has a number of USB devices and external media attached. This is a useful way of finding out what storage media are attached to the interface. You will also notice that there are "disks" identified by lscsi that are not listed by lsblk. This is because lscsi is actually looking what is attached, not the actual media readers that have media inserted. lscsi does not show on most platforms by default (although it does on Slackware).

If your system does not have it by default, check your distribution's package manager and install it. There are other names, using links, that can access these device nodes. If you explore the /dev directory you will find links that provide access to devices through volume labels, kernel path, etc. These names are useful to use because they can access a particular disk in a repeatable manner without having to know device node (/dev/sdc or /dev/sdf for example). For now, be aware that some assigned nodes might not yet have media. In many cases media readers can be detected and assigned nodes before media is inserted. No found.

Now that we have an idea of what disks are named, we can look at partitions. The fdisk program can be used to create or list partitions on a supported device. This is an example of the output of fdisk on a Linux workstation using the "list" option (-l):

```
root@forensic1:~# fdisk -l /dev/sda
Disk /dev/sda: 111.8 GiB, 1200341276 bytes, 234441648 sectors
Units of sectors: 512 = 512 bytes
Size (logical/physical): 111.8 GiB/111.8 GiB
Size (minimum/optimal): 111.8 GiB
label type: gpt
Disk identifier 6F8042E-B5CF-A974-28ADC65
```

| Device | Start | End | Size | Type |
| :--- | :--- | :--- | :--- | :--- |
| /dev/sda1 | 2048 | 206847 | 204800 | 100M Linux filesystem |
| /dev/sda2 | 206848 | 859545 | 652698 | 4G Linux swap |
| /dev/sda3 | 859545 | 234441614 | 233582070 | 107.7G Linux filesystem |

fdisk -l shows you list of partitions available on a particular drive. Each partition is identified by its name. The beginning and ending sectors for partition is displayed. The number of sectors per partition is displayed. Finally, the partition type is displayed. Note that the output of fdisk will change depending on Disk label queried. The above output shows a disk with a GPT label. If you have a standard DOS MBR, the output will show different fields. For native handling of GPT labels, you can use gdisk. Do not confuse fdisk with the older OS fdisk (for of us old enough to remember things). They are very different. The Linux version of fdisk provides for greater control partitioning.

BEFORE FILE SYSTEMS ON DEVICES CAN BE USED, THEY MUST BE MOUNTED Any file systems on partitions you define during installation will be mounted every time you boot. We will cover the mounting of file systems in the section that deals with Linux commands, after you have gained some navigation experience.

Keep in mind, that when not mounted, devices can be written to. Simply mounting a file system does not protect it from being changed by your actions or via mechanisms under your control.

## Device Node Assignment – Looking closer

Another common question arises when a user plugs a device in a Linux box and receives no feedback on how (or even if) the device was recognized. One easy method for determining how and if an inserted device is registered to use the dmesg command. For example, if I plug a USB drive into a Linux computer I may see an icon after the desktop for the disk. I might even see a folder open on the desktop allowing me to access the files automatically. If I'm at a terminal and there is no X desktop, I may get feedback at all. I plug the disk in and see nothing. I, of course, run the ls command to see my list of media refreshed. But I may want more than that.

So where can we look to see what node was assigned to our disk (/dev/sdc, /dev/sdd,etc?) How do we know if it was detected? Again, this question is particularly pertinent to the forensic examiner, since we may likely configure our system to be a little less "helpful" in automatically opening folders,

Plugging in the thumb drive and immediately running the dmesg command provides me with the following (abbreviated for readability):

```
root@forensic1:~# dmesg
usb 2-4.2: new SuperSpeed device number 4 using xhci_hcd
usb 2-4.2: new USB device found, idvendor=00781,idProduct=5583
usb 2-4.2: new USB device strings: Mfr=1,Product=2, SerialNumber=3
usb 2-4.2: Product: Ultra Fit
usb 2-4.2: Manufacturer: SanDisk
usb 2-4.2: SerialNumber: 4C5300010900827122100
us-storage 4-2:1.0: USB Mass device detected
scsi us-storage 4-2:1.0: 4-2,1.0
sd 19:0:0:0: Direct-Access SanDisk Ultra Fit 1.00 PQ: ANSI: 6
sd 19:0:0.0: [sd] 242614272 512-byte logical blocks:(124 GB/116 GiB)
sd 19:0:0:0: [sd] Write Protected is off
sd 19:0:0:0: [sd] Mode Set: 43 00 00 00
sd 19:0:0:0: [sd] Write cache: disabled, read cache: enabled, doesn't show
DPO or FUA
```
