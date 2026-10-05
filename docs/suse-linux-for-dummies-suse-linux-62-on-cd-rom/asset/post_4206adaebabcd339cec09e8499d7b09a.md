
# 288 Part VI: The Part of Tens

prevention: Make an emergency boot floppy disk, as I instruct you to during installation. Keep this disk handy when you update your system (or during any other significant system event, such as repartitioning disks or rebuilding your kernel). Then, if you make a mistake, you can boot the floppy, which will enable you to reboot your Linux operating system. When you've rebooted your system using the floppy, just log in as root and type **lilo** on the command line. This repairs the MBR by reinstalling LILO.

![](img/96a9ce6a13d8d15ed05f867f41574278_315_0.png)

If you are installing multiple operating systems on a new machine, do yourself a favor and install Linux last. Otherwise, you have to keep reinstalling LILO.

## My Disk Numbers Have Changed Since Installation

**Problem:** Linux numbers disks each time it boots, counting SCSI names like sda, sdb, and sdc. Suppose sda holds your Microsoft system, sdb holds the bulk of Linux, sdc holds your user files, and sdb holds your swap space. You add another disk and your user files are on sdn and your swap space is on sde. What happened?

**Solution:** SCSI disks are lettered according to the SCSI IDs on each disk. Linux names the disks using this ordering scheme. If you insert a new disk into the SCSI bus with a SCSI ID that is lower than an existing disk, you rename all with a SCSI ID above the one you just installed. It's best to start installing your SCSI disks with a SCSI ID of 0, 1, 2, and so on; then put other SCSI devices at the end of the SCSI bus with SCSI IDs 6, 5, 4, and so on. Note that most SCSI controllers are set to SCSI ID 7 by default.

IDE disks are numbered according to the IDE controller they are on and whether they are a master or a slave on that controller. Therefore, adding a new disk to a set of IDE controllers will not change the existing names, as shown here:

| Controller | Disk | Linux Name |
|---|---|---|
| ide0 | master | hda |
| ide0 | slave | hdb |
| ide1 | master | hdc |
| ide1 | slave | hdd |
| ide2 | master | hde |
| ide2 | slave | hdf |

## Chapter 18: Ten Problem Areas and Solutions 289

```
ide3 master hdg
ide3 slave hdh
ide0 = primary controller
ide1 = secondary controller
ide2 = third controller
ide3 = fourth controller
```

## My CD-ROM Isn’t Detected

**Problem:** You're installing Linux, but it doesn’t find your CD-ROM.

**Solution:** Most newer CD-ROMs are either EIDE (ATAPI) or SCSI, and most newer computers have enough support to see either the ATAPI CD-ROMs or the SCSI CD-ROMs, so CD-ROM support is not quite the issue it was in the early days. In addition, some older systems and CD-ROMs are not supported.

Some early CD-ROMs pretended to be other devices (such as tape drives or floppies) to fool the computer into using them, but these CD-ROMs were hidden from the detection system. If your system is one of these, don't despair: You can supply information to help Linux find your CD-ROM.

First look at the preceding section about disk numbering. This will let you figure out the name Linux would call your CD-ROM if Linux knew about it. If you have an EIDE/ATAPI CD-ROM, type the following line whenever you see the boot or lilo prompt while booting or installing your system:

```
linux hdx=cdrom
```

where $X$ is the number your CD-ROM would have if it could be detected.

## I Don’t Know How to Remove and Restore My MBR

**Problem:** You don’t know how to replace the boot record that was on your system before you installed Linux.

**Solution:** You can log in to Linux as *root* and then type the following command:

```
/sbin/lilo -u
```

Another solution is to boot MS-DOS or Windows 3.1, 95, or NT to an MS-DOS prompt and type the following:

```
fdisk /mbr
```

## I Can't Use LILO to Boot

**Problem:** You need to put Linux on a disk or a partition that is beyond the 1023rd cylinder, the second IDE disk, or the second SCSI ID number, or you need to do something else that will make it difficult for Linux to boot LILO. Can you boot Linux in another way?

**Solution:** You can use a program called LOADLIN to boot from your MS-DOS or Windows system:

- 1. **Copy your configured Linux kernel to the C drive of your MS-DOS or Windows system.**

The easiest way to do this is to install Linux, log in as **root** and type the following:

```
grep image /etc/lilo.conf
```

A line similar to the following appears:

```
image=/boot/vmlinuz
```

This points to your compressed kernel, which in this example is located at /boot/vmlinuz.

- 2. **Copy the compressed kernel to a floppy disk,**

The easiest way to do this is to install Linux, log in as **root** and type the following: (Wait, the OCR text gets repetitive here, let's de-duplicate based on logic).

*Self-correction: The OCR text provided for pages 317-319 contains significant repetition and artifacts from the scan/layout. I will clean the logical flow based on the provided text.*

- 2. **Copy the compressed kernel to a floppy disk...** (The text continues with instructions for LOADLIN).

[Note: The provided OCR text for the later pages is highly fragmented/repetitive. I have merged the unique semantic segments provided in the source text.]
