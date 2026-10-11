
![](img/860d0c38bd76c9ded976e9d1e179ef25_296_0.png)

## Figure 9.7

*The list of SCSI host adapters is mostly alphabetical, although there are some exceptions.*

In order to determine what chipset your product uses, you might need to examine the board closely. Look at the largest chip on the board and examine it for a logo or identifying number. In some cases you might need to peel back a sticker that the board manufacturer placed over the main chip in order to obscure the chipset manufacturer's name.

**CAUTION**

Board manufacturers occasionally change the chipsets used on their products, sometimes without altering the product name or packaging. Therefore, the fact that you've used a product in the past doesn't guarantee that you'll be able to do so in the future.

## BIOS Support

The SCSI *basic input/output system* (BIOS) serves as a supplement to the motherboard's BIOS. The most important function of the BIOS is to enable the computer to boot from a SCSI device—primarily a hard disk, but also sometimes a removable disk or CD-ROM drive. In addition, most SCSI BIOSes provide services that enable you to configure various aspects of SCSI host adapter operation, including features such as

- **Host adapter termination** Most modern host adapters let you set termination, using the keyboard. This can be extremely convenient if you have an external SCSI device that you regularly move between two or more computers.

- **Host adapter SCSI ID** The host adapter needs its own SCSI ID, and the BIOS utility usually lets you set the ID to be used.

- **Disk geometry options** SCSI uses a single linear address mode for its hard disks, but the x86 BIOS, and hence many programs, requires a CHS triplet. There are many ways to convert from one to the other, and some SCSI host adapter BIOSes support multiple translation methods, which you can set using the SCSI BIOS.

**CAUTION**

If you partition a disk using one SCSI host adapter and subsequently use the disk with another host adapter, it’s possible that the second adapter won’t support the first one’s CHS mapping mode. If this happens, it might be impossible to recover data from the disk using the second host adapter. Your only choice in a case like this might be to back up the disk using the first host adapter, and then re-partition the disk and restore the data using the second host adapter. Most modern host adapters can recognize a wide range of CHS mappings, however, and adapt themselves automatically on a disk-by-disk basis.

- **Boot options** You can often tell the SCSI BIOS to allow or forbid booting from non-hard disk devices such as removable disks and CD-ROM drives. Similarly, some host adapters allow you to set a limit on the number of potentially bootable hard disks (typically between 1 and 4), or specify which hard disk is the boot device.

- **Low-level disk formatting** Most modern SCSI BIOSes include an option to perform a low-level format on hard disks. Such a format wipes out all data on the drive, and there’s usually no need to perform such a format. If you do need to do so, the option is there.

**TIP**

If you’ve used a hard disk on one host adapter or computer and want to use it on another, but don’t need the disk’s data, doing a low-level format is one way to ensure that the disk’s CHS geometry mapping won’t cause problems on the new host adapter. You can accomplish the same goal more simply, however, by wiping out the hard disk’s Master Boot Record (MBR). You can do this in Linux by issuing the command `dd if=/dev/zero of=/dev/sda bs=512 count=1` (Change /dev/sda to the identifier for another disk, if desired.) When a format wipes out the data on the drive, the host adapter assigns a new disk geometry to the drive based on whatever algorithms the host adapter favors.

You can enter most host adapters' SCSI BIOSes by entering a keystroke at some point during the computer's boot process. You usually need to enter this keystroke shortly after the motherboard's BIOS has done its memory check. Most host adapters provide a prompt for the appropriate keystroke during the boot process, so watch carefully.

Some SCSI host adapters, particularly models from the mid-1990s and earlier, include BIOSes but lack keyboard-accessible BIOS utilities. You can often use options similar to those I’ve just described on such boards using jumpers. These boards also often include utility programs (typically run from DOS) that let you check the SCSI bus, low-level format a hard disk, and so on.

Very low-end host adapters lack BIOS support. Such a lack does *not* mean that you can’t use the host adapter with SCSI hard disks; however, *it does* mean that you can’t boot from a SCSI hard disk attached to that host adapter. You can still use these host adapters for SCSI hard drives on a system that contains an EIDE boot disk, or a boot disk on another SCSI host adapter. You can even boot Linux using a Linux boot floppy on such systems, but you must ensure that the boot floppy contains a kernel with the appropriate SCSI driver compiled in, as opposed to compiled as a module. (The same is true when booting from a hard disk connected to a host adapter that has a BIOS.)

Some Symbios-based host adapters reside in a limbo land with respect to the boot BIOS. These host adapters don’t contain BIOSes themselves, but some motherboards do include the Symbios SCSI BIOS. When mated with such a motherboard, the SCSI host adapter acts as if it had a boot BIOS installed. In some cases it’s possible to add the Symbios SCSI boot BIOS to your motherboard’s BIOS, even if it wasn’t present to begin with. I only recommend trying this if you’re familiar with flashing motherboard BIOSes and if you have a backup BIOS of one form or another. A mistake can render your system unbootable. Many modern motherboard flash BIOS utilities include options to add a Symbios boot BIOS image, which you can obtain from the Symbios Web site. You should check the documentation that came with your motherboard’s flash BIOS utilities for details. Some motherboard EEPROM chips aren’t large enough to support the Symbios boot BIOS in addition to the regular BIOS, however. On these boards you have little choice but to do without the SCSI BIOS.

### Summary

SCSI can be a confusing subject for those who haven’t dealt with it before. The various levels of SCSI, along with issues such as termination, SCSI IDs, and SCSI BIOSes, can be intimidating. The rewards of using SCSI devices can be considerable, however, particularly in a high-performance server environment. Today’s fastest SCSI devices are faster than today’s fastest EIDE devices. SCSI is inherently better suited than EIDE to communicating with several devices simultaneously, and to use a large number of different SCSI devices. These benefits can be mitigated by the need to mix modern, high-speed hard disks with older, lower-speed SCSI devices such as removable disks or scanners. Such a mixture might necessitate the use of two host adapters or shorter SCSI cables and lower transfer rates.

Fortunately, Linux support for SCSI host adapters is quite good. Aside from a few just-introduced models, most major SCSI host adapters and chipsets are supported by Linux, some with official support from the SCSI host adapter manufacturer. Support is actually worse at the low end of the scale, among bottom-of-the-line PIO ISA SCSI host adapters, particularly those from small manufacturers. Fortunately, you can usually replace such boards with better low-end PCI host adapters for under $100, and get a performance boost in the bargain.

# Audio/Video

PART III

### IN THIS PART

- 10 Sound Cards 281
- 11 Audio Input/Output 313
- 12 Video Cards 335
- 13 Video Capture and AV Input Hardware 357
- 14 Monitors 377

# Sound Cards

CHAPTER 10

### IN THIS CHAPTER

- Board Busses 282
- Sound Card Bitness and Sample Rates 284
- MIDI Sound Production 289
- Sound Card Chipsets 296
- Linux Audio Drivers 299
- Linux Audio Utilities and Applications 305
