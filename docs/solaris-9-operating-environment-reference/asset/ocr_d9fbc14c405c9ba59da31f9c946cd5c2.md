# 350

# fdformat

+   -t nec Install an NEC-DOS file system and boot sector on the disk after formatting. Use this option only with the -M-option. (This feature is not available on all systems.)

+   -U Unmount any file systems and then format.

+   -v Verify each block of the diskette after the format.

+   -x Skip the format, and write only a SunOS label or an MS-DOS file system.

The following options are provided for compatibility with previous versions of fdformat; their use is discouraged.

+   -d Format an MS-DOS diskette or PCMC memory card (same as -t). This option is equivalent to the MS-DOS format.

+   -l Format a 720-kilobyte (3.5-inch) or 360-kilobyte (5.25-inch) double-density diskette (same as -D or -L). This option is the default for double-density type drives; use it only if the drive is high- or extended-density type.

+   -L Format a 720-kilobyte (3.5-inch) or 360-kilobyte (5.25-inch) double-density diskette (same as -l or -D). This option is the default for double-density type drives; use it only if the drive is the high- or extended-density type.

+   -m Write a 1.2-megabyte (3.5-inch) medium-density format on a high-density diskette (use only with the -t nec option). This option is the same using -M. (This feature is not available on all systems.)

# Operands

devname Replace devname with rdiskette0 (systems with Volume Management) or floppy0 (systems with Volume Management) to use the first drive or rdisk1 (systems without Volume Management) or floppy1 (systems with Volume Management) to use the second drive. If you omit devname, use the first drive, if one exists.

For PCMCIA memory cards, replace devname with the device name for the PCMCIA memory card that resides in /dev/rdsk/cM.NMsN/for /dev/disk/cM.NMsN.

If you omit devname, use the default disk drive, if one exists. N represents a decimal number and can be specified as follows:

```
Controller N
tN Technology type N
01 ROM.
02 OTPROM.
03 EPROM.
04 EEPROM.
05 FLASH.
```