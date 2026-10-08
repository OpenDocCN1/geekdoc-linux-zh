
A password length of 32 bytes (maximum) is allowed for Iomega products that support this feature. This option is applicable only for Iomega products. Iomega products do not allow read/write protection without a password. On the devices that do not have such a software read/write protect facilities, warnings indicating the nonavailability of this feature are provided.

```
-s filename
```

Enable the layout of partition information in the SUNOS label. Provide filename as input with information about each slice in a format providing byte offset, size required, tags, and flags, in the following format.

```
slices: n = offset, size [, flags, tags]
where nis is the slice number, offset is the byte offset at the slice nstarts, and size the required size for slice n Both offset and size must be a multiple of 512 bytes. You can represent these numbers as decimal, hexadecimal, or octal. No floating-point numbers are accepted. You can obtain details about the maximum number of slices from the System Administration Guide: Basic Administration.
```

To specify the size offset in kilobytes, megabytes, or gigabytes, add KB, MB, or GB. A number without a suffix is assumed to be a byte offset. The flags are described below.

```
wm = read-write, mountable.
wu = read-write, unmountable.
ru = read-only, unmountable.
```

The tags are unassigned, boot, root, swap, usr, backup, stand, var, home, alternates.
You can omit tags and flags from the four tuple when you do not require finer control on those values. You must either omit or include both. If you omit tags and flags from the tuple for a particular slice, a default value for each is assumed. The default value for flags is wm, and for tags is unassigned.

You can use either full tag names or an abbreviation for the tags. The abbreviations can be the first two or more letters from the standard tag names. rmformat is case insensitive in handling the defined tags and flags.

Slice specifications are separated by a colon (:), as shown in the following example.

```
slices: 0 = 0, 30MB, "wm", "home" :
1 = 30MB, 51MB :
2 = 0, 100MB, "wm", "backup" :
3 = 81MB, 19MB
```

rmformat does the necessary checking to detect any overlapping partitions or illegal requests to addresses beyond the capacity of the medium under consideration. Only one slice of information entry is permitted for each slice n. If you provide multiple slice information entries for the same slice n, an appropriate error message is displayed. Slice 2 is the backup slice covering the whole disk capacity. You can use the pound-sign (#) to describe a line of comments in the input file. If the line starts with #, then rmformat ignores all the characters following # until the end of the line.

You can partition some media with very small capacity, but be cautious in using this option on some devices.

- -U amount on any file systems, and then format. See mount(1M). This option unmounts all mounted slices and issues a long format on the device requested.

- -V read write
Verify each block of medium after format. The write verification is a destructive mechanism. You are queried for confirmation before the verification is started. The output of this option is a list of numbers that are identified as bad.

The read verification verifies only the blocks and reports the blocks that are prone to errors.

You can use the list of block numbers with the -c option for repairing.

- -w enable disable
Enable or disable the write protection on medium. On devices that do not have a software write-protect facility, a message indicating nonavailability of this feature is displayed.

- -W enable disable
Enable or disable write protection with password. This option always works in interactive mode because a password is requested to maintain security.

A maximum password length of 32 bytes is allowed for Iomega products that support this feature. On devices that do not have the write protection with password, the software displays appropriate messages indicating the nonavailability of such features.

# Operands

- - devname
An absolute or relative device path name for the device from the current working directory or the nickname as exported by the System Volume manager. See void(1M).

# rmformat

# 1177

For diskette devices, you can use /dev/rdiskette(for systems without volume management) or floppy0 (systems with volume management) to use the first drive. Specify /dev/rdiskettel (for systems without volume management), or floppy1 (systems with volume management) to use the second drive.

For systems without volume management running, you can also provide the absolute device path name as /dev/rdsk/c?t?d?s? or the appropriate relative device path name from the current working directory.

# Examples

The following example formats a diskette on a system with volume management.

```
rmopoke% rmformat -F quick /dev/rdiskette
Formatting will erase all the data on the disk.
Do you want to continue? (y/n) y
rmopoke%
```

The following example formats a diskette on a system running volume management.

```
rmopoke% rmformat -F quick floppy0
Formatting will erase all the data on the disk.
Do you want to continue? (y/n) y
rmopoke%
```

Note that running the rmformat with volume management takes substantially longer than running it without volume management.

# Files

- /dev/dev/diskette0
  Directory providing block device access for the diskette in drive 0.
/vol/dev/rdiskette0
  Directory providing character device access for the diskette in drive 0.
/vol/dev/aliases
  Directory providing symbolic links to the character devices for the different medium under the control of volume management using appropriate aliases.
/vol/dev/aliases/floppy0
  Symbolic link to the character device for the diskette drive 0.
/vol/dev/aliases/zip0
  Symbolic link to the character device for the medium in Zip drive 0.
/vol/dev/aliases/jaz0
  Symbolic link to the character device for the medium in Jaz drive 0.

/dev/rdiskette Symbolic link providing character device access for the diskette in the primary diskette drive, usually drive 0.

/vol/dev/dsk Directory providing block device access for the PCMCIA memory and ata cards and removable media devices.

/vol/dev/rdsk Directory providing character device access for the PCMCIA memory and ata cards and removable media devices.

/vol/dev/aliases/dskS Symbolic link to character device for the diskette drive 0, where S represents the number.
/vol/dev/aliases/disk0 Symbolic link to the character device for the medium in Zip drive 0, CD-ROM, and so forth.
/vol/dev/rdsk Directory providing character device access for the PCMCIA memory and ata cards and removable media devices.
/dev/dsk Directory providing block device access for the PCMCIA memory and ata cards and removable media devices.

# Attributes

See attributes(5) for descriptions of the following:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwc |

# See Also

cpio(1), eject(1), fdformat(1), tar(1), volcancel(1), volmissing(1), formattoc(1), mkfs(1), newfs(1), prtvoc(1), rmmount(1), sortbib(1), void(1)

# ### ### roffbib — Format and Print a Bibliographic Database

# Synopsis

```
/usr/bin/roffbib [-e] [-h] [-m filename] [-np] [-olist] [-Q] [-raN] [-sN] [-Tterm] [-V] [-x] [filename]
```

# Description

roffbib command to print all records in bibliographic format instead of footnotes or endnotes. Generally, roffbib is used in conjunction with sortbib(1).

# Options

roffbib accepts all options understood by nroff(1) except -i and -q.

- -e
Produce equally spaced words in aligned lines,

- -h
Use Tabs during horizontal spacing to speed output and reduce character count. Tab settings are assumed to be 8 nominal character widths.

- -m filename
Prepend the macro file /usr/share/lib/tmac/tmac.name to the input files. Leave a space between the -m and macro filename. This set of macros replaces the ones defined in /usr/share/lib/tmac/tmac.bib.

- -np
Number the first generated page p.

- -olist
Print only page numbers that appear in the comma-separated list of numbers and ranges. Range M-N means through M from N to end.

- -Q
Queue output for the typesetetter. Set page offset to 1 inch.

- -raN
Set register (single character) to M The command-line argument -rM numbers the references starting at 1.

- -sN
Halt every Npages for paper loading or changing (default N=1). To resume, press newline or Return.

- -Tterm
Specify term as terminal type.

- -V
Send output to the Versatec printer. Set page offset to 1 inch.

- -x
If abstracts or comments are entered following the %x field, roffbib formats them into paragraphs for an annotated bibliography. You can use several %x fields if you want several annotation
