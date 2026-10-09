
In previous books, including earlier editions of this one, I've discussed the importance of proper data placement on the disk, but all of that knowledge is completely obsolete. If you still retain any of that knowledge, discard it in favor of something more useful, like the complete biographies of all the actors who appeared in any role in classic Doctor Who.

As far as disk design goes, the only thing you need to know about is logical block addressing (LBA). Each sector on a disk is assigned a number. Filesystems call disk sectors by number. That's it. Anything beneath LBA is pure guesswork on your part.

Unfortunately, disks now have a new category of lies they tell: sector size.

Up through the 1990s, disk sector sizes varied from 128 bytes to 2KB. Even the original IBM PC could understand different sector sizes on floppy disks.

In the early 2000s, though, manufacturers settled on 512-byte sectors. Today's hard drives are much larger, and the files are similarly larger. In the last few years, the 512-byte sectors have mostly been replaced with 4,096-byte sectors, called 4K drives. This sector size makes more sense for the type of data we store today.

The problem is, operating systems like Windows XP know that a disk sector always has been, and always will be, 512 bytes. These operating systems won't tolerate hard drives that reported having 4KB sectors because everybody knows there's no such thing. If you manufacture 4K drives, what do you do?

The same thing you always do.

You teach the hard drive to lie.

Best of all, different 4K drives lie in different ways. If the OS asks a drive its sector size, most drives state that they have 512-byte sectors. Drives that claim to have both 512-byte and 4KB sectors are probably 4K drives, struggling to tell the truth. Very few admit to having solely 4KB sectors. To complicate matters even more, some solid state drives have sectors as large as 8KB or 16KB, or they support multiple sector sizes.

Both of FreeBSD’s main filesystems must know the sector size of the underlying disk and the logical block address of that sector. If you use the wrong sector size on your disk, performance suffers. I could go into long detailed discussions of how this happens, but to keep it simple, always align partitions on even megabyte boundaries. You might waste a few bytes here and there, but that’s trivial compared to the truly appalling performance you’ll get from having a filesystem misaligned with the disk.

## Device Nodes

We touched briefly on device nodes in Chapter 4, but let’s consider them in more detail here. Device nodes are special files that represent a hardware device or an operating system feature. They’re used as logical interfaces to provide features to user programs. By using a command on a device node, sending information to a device node, or reading data from a device node, you’re telling the kernel to perform an action. If the device node represents a physical device, you’re acting on that device. These actions can be very different for different devices—writing data to disk is very different than writing data to a sound card. While you can expose device nodes anywhere, the standard device nodes exist in /dev.

Before you can work with a disk or disk partition, you must know its device name. FreeBSD disk device nodes come from the names of the device driver for that type of hardware. Device driver names, in turn, often come from the type of device and not the device’s role or function.

Table 10-1 shows the most common disk device nodes.

**Table 10-1: Storage Device Nodes and Types**

| Device node | Man page | Description |
| :--- | :--- | :--- |
| /dev/ada* | ada(4) | ATA-style direct access disks (SATA, IDE, etc.) |
| /dev/cd* | cd(4) | Optical media drives (CD, Blu-Ray, etc.) |
| /dev/da* | da(4) | SCSI-style direct access disks (USB storage, SAS, etc.) |
| /dev/md* | md(4) | Memory disks |
| /dev/mmcsd* | mmcsd(4) | MMC and SD memory cards |
| /dev/nvd* | nvd(4) | NVM express drives |
| /dev/vtbd* | virtio_blk(4) | Virtio-based virtual machine disk |
| /dev/xbd* | xen(4) | Xen virtual disks |

Many RAID controllers present their RAID containers as SCSI devices, so they show up as `/dev/da` device nodes. Others present their disks as “SCSI plus special vendor topping,” so they get special device node names such as `/dev/raid` (ATA RAID), `/dev/mfid` (certain LSI MegaRAID cards), and so on. Check the man page for your RAID controller to see the device node it presents.

## The Common Access Method

The *Common Access Method* (*CAM*) is a standardized device driver architecture originally written to support the complex command set of 20th-century SCSI-2 disks. The idea was that standardizing based on this architecture would simplify writing device drivers. Only FreeBSD and DEC OSF/1 actually shipped with CAM, however, and each filled in the specification’s gaps differently.

FreeBSD 9 and later consolidates management of all physical disks that support CAM in the CAM interface. Use `camcontrol(8)` to gather information from disks and issue commands to them. The `camcontrol(8)` command has a variety of subcommands that let you issue instructions to hard drives.

### What Disks Do You Have?

To identify a host's storage devices, you can crawl `/var/run/dmesg.boot` looking for disk device nodes or see which filesystems are mounted and backtrack from there. But the easiest way to identify your storage is to have camcontrol(8) ask the CAM system what disks it sees. Let's look at one of my test systems:

```
# camcontrol devlist
<ATA WDC WD1003FBYZ-0 1V03>       at scbus0 target 0 lun 0 (pass0,da0)
<ATA WDC WD1003FBYZ-0 1V03>       at scbus0 target 1 lun 0 (pass1,da1)
<ATA WDC WD1003FBYZ-0 1V03>       at scbus0 target 2 lun 0 (pass2,da2)
<ATA WDC WD1003FBYZ-0 1V03>       at scbus0 target 3 lun 0 (pass3,da3)
```

This output is broken up into three fields. The first gives the name of the device, as reported by the device itself. This is usually a vendor and the vendor's model number.

The second section gives SCSI connection information. These drives aren’t actually SCSI drives—they’re SATA connections managed via CAM. But you now know which disk devices are plugged into which port on the SATA controller.

Finally, in parentheses, we have the SCSI device and what we probably want, the storage device node. This host has four disks, named da0, da1, da2, and da3.

## Non-CAM Devices

Generally speaking, everything except proprietary RAID controllers and virtual disks support CAM.

RAID controllers have usually embraced and extended the CAM protocol, for what the manufacturer thought was a good reason at the time. A protocol written in the early 1990s wasn’t sufficient for a 2010 RAID controller. These controllers usually have their own control programs. The RAID containers show up in devlist and some other camcontrol(8) subcommands.

Similarly, virtual disks don’t respond to CAM commands. There’s no disk to command there—you’re just writing blocks to a file. You can view the disk with camcontrol devlist, but that’s about it. For most applications, I recommend using FreeBSD’s RAIDZ or GEOM RAID, rather than a hardware RAID controller.

# The GEOM Storage Architecture

FreeBSD has an incredibly flexible storage infrastructure system called GEOM (short for “disk geometry”). GEOM lives between device driver nodes and the underlying hardware, handling data exchanged between them. From this position, GEOM can arbitrarily transform input/output requests.

# DEVICE CONTROL PROGRAMS

Some storage devices have special features that aren’t addressed in the generic CAM framework. RAID controllers often have vendor-specific features, and FreeBSD includes many small programs to individually manage these controllers. You’ll find programs like mfuitl(8) and mptutil(8) for older LSI controllers, mpsutil(8) for newer LSI controllers, and so on. If you have a nonvolatile memory express (NVMe) drive, check out nvmecontrol(8).

GEOM is built out of kernel modules, called GEOM classes, that let you perform specific types of transformation or management. Disks have a GEOM class that lets the kernel put data on the disk. But if you want to encrypt your disks, that’s a GEOM class. Software-based RAID? A GEOM class. FreeBSD implements all storage modifications as GEOM classes.

GEOM classes are stackable. They use the output of one class as the input for another. You want to encrypt your hard drive and then mirror
