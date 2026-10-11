
## Do You Need Rewritable Functionality?

The first question you should ask yourself is whether you need the ability to handle rewritable discs. In some cases, you might not need this ability. For example, if your main goal is to create audio CDs from your collection of 78 rpm albums, you don’t need rewritable functionality, because most audio CD players can’t read CR-RW discs, and you presumably won’t be changing these discs after you create them. Similarly, if you want to archive accounting or scientific data for long-term storage, a CD-R drive is quite adequate. On the other hand, if you want to create disks that you’re likely to erase or modify in the near future, such as collections of updated packages for your Linux distribution, then the rewritable feature can be beneficial.

All CD-RW drives can also create CD-R discs, so you need not sacrifice compatibility with older CD-ROM drives and audio CD players in order to gain rewritable functionality. In fact, because CD-RW drives cost little more than otherwise equivalent CD-R drives, there’s very little reason to favor a CD-R drive. The main exception would be if you saw a CD-R drive on sale for a particularly good price.

In the DVD realm, DVD-R drives are still quite expensive, but they produce DVDs that can be played on ordinary DVD drives. If you have the need to store more than 650MB of data on media that are at least somewhat commonly readable, DVD-R is the way to go. If you only need to read the media back on your own system, however, DVD-RAM drives cost much less. DVD-RW drives are still quite rare, but might become less so in the future. It is as of yet unclear where they and DVD+RW drives will fit into the marketplace.

## Disk-at-Once Versus Track-at-Once

Another characteristic of recordable drives that bears mentioning is the distinction between disk-at-once (DAO) and track-at-once (TAO) recording modes. In DAO recording, the recording laser is turned on at the start of the disc and turned off only after the entire disc has been recorded. In TAO mode, the laser is turned on at the start of each track, turned off at the end of the track, and turned on again at the start of the next track. The laser is also turned on and off to write specialized control regions, such as the table of contents, lead-in, and lead-out—areas that control access to individual tracks and the CD as a whole. Most data CD-ROMs contain only a single track, so the difference between the two modes is minor (although using separate laser burns for the control areas does cause problems on a small number of CD-ROM drives and for some purposes such as mass duplication). Most audio CDs contain several tracks, so DAO and TAO modes produce slightly different results. On rare occasions, TAO CDs can’t be played on some audio CD players, or produce peculiar effects such as causing a player to pause or stop between tracks. TAO also produces a very slight snap noise at the start and end of each track, although it’s soft enough that you’re not likely to notice it. Perhaps most important, most CD-R drives produce a minimum gap of two seconds between tracks in TAO mode, so you can’t easily create a CD with no gap between tracks, as is desirable when creating a CD from concert performances.

For both audio and data CDs, most CD duplication services require original CD-R discs mastered in DAO mode. Therefore, if you plan to create CD-R masters for mass production, you should be sure to get a drive that can create DAO discs.

Fortunately, most modern CD-R and CD-RW drives can produce both DAO and TAO discs. A few older models support only TAO mode. If you think you’ll want to produce concert-style audio CDs, or if you intend to send a CD to a duplicator for mass production, be sure the drive you purchase has DAO capability.

![](img/860d0c38bd76c9ded976e9d1e179ef25_235_0.png)

### Checking Compatibility with Linux CD-Creation Tools

The most important feature of any recordable CD technology for Linux is its compatibility with Linux CD-creation tools. Unlike most other recordable media (such as Zip disks, floppies, and tape drives), the command set for handling CD-R and CD-RW drives isn’t quite completely standardized. The *multimedia* command (MMC) standard represents an attempt to change this state of affairs. Even drives that claim to be MMC drives aren’t always 100% compatible, however, because they might contain bugs or deliberate deviations from the MMC standard. Nonetheless, your single best bet for compatibility is to purchase an MMC drive, which shouldn’t be difficult because MMC has become nearly universal since 1999.

If you’re considering a used or closeout non-MMC drive or if you want to further increase your chances of trouble-free operation under Linux, you should check these drive compatibility listings for Linux CD recording packages:

- **cdrecord**: The README file for cdrecord (at ftp://ftp.fokus.gmd.de/pub/unix/cdrecord/) includes a list of supported drives.
- **cdrdao**: Check http://www.ping.de/sites/danqb/drives.html for drive compatibility.

Linux GUI CD-creation tools generally use one or the other of these programs to do the “dirty work” of recording a CD, so even if you want to use a GUI tool, you should check the compatibility of these text-mode utilities.

### Accessing Optical Media in Linux

Those who are new to Linux frequently have difficulty using a CD-ROM drive, simply because Linux’s methods of CD access are foreign to them. Even experienced users can have trouble when installing a new CD-ROM of a different type (say, replacing an EIDE/ATAPI CD-ROM with a SCSI model), or when using a new type of device (say, adding a CD-RW drive). This section presents some tips relating to locating your optical devices and using the data on these devices.

#### Accessing Optical Devices

You access the vast majority of Linux hardware through *device files*—special files that are typically located in the */dev* directory. In most cases, though, you don’t access the device file for an optical drive directly; instead, you pass the name of the device file to a program such as mount, which uses it to make the device accessible in some way.

#### Locating the Appropriate Device File

If you installed Linux from an optical drive, chances are it created a link to the appropriate device file under the name */dev/cdrom*. In such a case, you can use that name or examine the link to find what the underlying device is. For instance:

```bash
$ ls -l /dev/cdrom 
lrwxrwxrwx 1 root root 8 Dec 29 02:12 /dev/cdrom -> /dev/hda
```

This transaction indicates that the */dev/cdrom* file is a symbolic link to */dev/hda*, which is the true device file.

If for some reason your Linux distribution didn’t create an appropriate symbolic link, or if you have replaced a drive of one type with another or reconfigured your EIDE bus, you might need to locate the device file in some other way. Each interface style has its own associated device files, as follows:

- **SCSI devices**
  SCSI CD-ROMs are assigned device names of the form */dev/sdc*n*, where *n* is a number from 0 up. A computer with a single SCSI CD-ROM drive uses */dev/sdc0*, whereas a system with two optical drives also has a */dev/sdc1*. Typically, the device with the lower SCSI ID acquires the */dev/sdc0* designation. Most SCSI CD-R drives can be accessed for reading using this same designation, but some don’t show up as CD-ROM devices. Some drives have a jumper or switch you can set to alter the way they report themselves to the computer; you can change this jumper setting to make the drive appear or disappear as a /dev/sdcn device. For write purposes, SCSI CD-R and CD-RW drives are accessed through the generic SCSI interfaces, /dev/sr*n*, where n is either a number from 0-15 or a letter from a-n, corresponding to the SCSI ID number. Do not attempt to use the generic SCSI identifier to mount a CD for reading. The /dev/sdcn devices use major number 11 and minor numbers starting from 0. The /dev/srn device files use major number 21 and minor numbers starting from 0.

- **IDE/ATAPI devices**
  IDE/ATAPI drives are accessed through device files named in the /dev/hd*a* pattern, where n is a letter from a-d (or occasionally higher). The letter is an indication of the IDE chain and position on the chain. a is for the primary chain's master device, b for the primary chain's slave device, c for the secondary chain's master, and so on. Note that these identifiers are the same as those used for other disk devices. Therefore, you can't tell from the device filename alone whether a device is a CD-ROM, a removable disk, or a hard disk. In the case of recordable drives, it's best to compile SCSI emulation support into your kernel. You can then access the drive for writing using the generic SCSI device files. /dev/hda devices use major numbers 3, 22, 33, and 34 for the primary and subsequent controllers, with minor numbers 0 and 64 for master and slave devices, respectively.

- **Proprietary devices**
  Old proprietary interfaces are assigned unique identifiers depending upon the specific device. For instance, /dev/magn, where n is a number from 0-1, represents Mitsumi drives; and /dev/aztecdo is the device file for Aztec CD-ROM drives. Check the appropriate documentation files in /usr/src/linux/Documentation/cdrom for further details.

- **Parallel-port devices**
  Most of these devices use the parallel-port IDE drivers, and acquire device identifiers of the form /dev/pcd*n*, where n is a number from 0-4. These devices use major number 46 and minor numbers starting at 0.

- **USB devices**
  The USB support for CD-ROM drives, such as it is, maps these drives into the SCSI device tree, so USB CD-ROM drives use SCSI identifiers.

**NOTE**

Device files aren't created automatically by the device's driver; they're created by scripts run during system installation. You'll therefore find device files for devices that aren't present on your computer. All modern Linux distributions create appropriate device files for all CD-ROM device types, and, if you accidentally delete a device file, most include a script in the /dev directory to create the device files anew. Alternatively, you can use the mknod command to create a single device file manually, but you must know the identifying characteristics-the major and minor device numbers mentioned in the interface descriptions earlier.

![](img/860d0c38bd76c9ded976e9d1e179ef25_237_0.png)
