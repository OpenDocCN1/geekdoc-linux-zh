
## Table 13-1: Comparison of Common Backup Media

| Backup Medium | Advantages | Disadvantages |
| --- | --- | --- |
| Magnetic tape | High capacity, low cost for archiving massive amounts of data. | Sequential access medium, so recovery of individual files can be slow. |
| Writable CDs | Random access medium, so recovery of individual files is easier. Backups can be restored from any CD-ROM drive. | Limited storage space (up to 700MB per CD). |
| Writable DVDs | Random access medium (such as CDs). Large capacity (4.7GB, although the actual capacity you can achieve is less). DVD-9 and DVD-5 DVDs store up to 8.5GB of data. | DVD drives and DVD-R disks are relatively expensive (although they are coming in down). More manufacturers DVD writers to their PCs, DVD will eventually replace CDs as the most common removable media drives. |
| Additional hard drive | Allows faster and more frequent backups. Fast recovery from crashes. No media to load. Data can be recovered quickly. You can configure the second disk to be a virtual clone of the first disk, so that you can boot off the second disk if the first disk crashes. | Data cannot be stored off; there is a risk of data loss if the server is destroyed. This method is not well suited to keeping historical versions of many removable files. The hard drive will eventually fill up. By using removable drives you removing the backup drive when it is full and moving to a secure location. |

## Magnetic tape

Magnetic tape was for years the most common medium used for backing up large amounts of computer data. Today's high-capacity tape drives can back many gigabytes of data on an amazingly small tape, allowing vast amounts of information to be safely stored. Tapes are also easy to transport offsite so that data will be secure in case of fires, hurricanes, or other disasters.

The primary disadvantage of magnetic tape is that it is a sequential access medium. This means that tapes are reading or writing from end, and searching for a particular file can be time-consuming. For this reason, tape is a good choice for backing up and restoring entire systems, but not the ideal to recover individual files on a regular basis.

Fedora and RHEL use a wide variety of tape drives. Most SCSI tape drives will work without loading special modules. Even IDE tape drives are now supported natively, without requiring the drive to operate in a “SCSI emulation” mode. Some drives, however, require installation of additional software.

## Using tape tools for magnetic tape

If your tape is attached to the IDE floppy drive cable, you will need to use the ftape driver to access it. Fortunately, the loadable module is bundled with the Linux 2.6 kernel. When your Linux system boots, it autodetect the tape drive and load the tape drive. To verify that your system loaded the tape drive, type the following command shortly after you boot your computer:

```
dmesg | grep ftape
```

This searches the most recent kernel messages for lines containing the word ftape. If the ftape module was loaded, you would see something like this:

```
ftape v4.04d 25/11/97
[000] ftape-init.c (ftape_init) - installing QIC-117 floppy tape
hard drive...
[001] ftape-init.c (ftape_init) - ftape_init @ 0xd0b0060.
[002] ftape-buffer.c (add_one_buffer) - buffer nr #1 @ c1503c44, dma
area @ 0c2c0000.
[003] ftape-buffer.c (add_one_buffer) - buffer nr #2 @ c1503c44, dma
area @ 0c298000.
[004] ftape-buffer.c (add_one_buffer) - buffer nr #3 @ c50abaac, dma
area @ 0c328000.
[005] ftape-calibr.c (time_inh) - ini(): 1109 nsec.
[006] ftape-calibr.c (ftape_calibrate) - TC for 'ftape_udelay()' = 310
nsec (at 20479 counts).
[007] ftape-calibr.c (ftape_calibrate) - TC for 'fdc_wait()' = 2208 nsec
(at 2559 counts).
```

If the module was not loaded, then you should check whether your kernel is compiled with support for the tape module and your particular tape drive. It should be available and ready to include as a loadable module.

In most cases, an ftape device can be accessed like a SCSI device. The primary difference is that an ftape device file lists qft (for QIK Floppy Tape) as a SCSI device contains st. For example, the device file for the first SCSI tape on your system will probably be /dev/st; the device file for the first floppy tape will likely be /dev/qft0.

All of the standard tape- and archiving-related programs should work fine with both types of hardware. Nevertheless, there are a few extra programs you might find useful when working with a floppy tape drive. These programs can be found in the mt-st package in Fedora. The mt command is used to control magnetic tape operation. The stint command can initialize SCSI tape drives.

## Chapter 13: Backing Up and Restoring Files 545

## Testing the magnetic tape drive

With the mt-st package installed, you should now be ready to test your tape drive. Insert a blank tape into the tape drive and type the following commands:

```
$ mt -f /dev/qft0 status
$ mt -f /dev/qft0 rewind
```

The first command will present a status of the tape drive. After the second command, you should hear the tape spin as the system rewinds the tape. This will be a very short process if the tape is already rewound. The mt command provided with mt-st package is used to scan, rewind, and eject magnetic tapes in a tape drive.

## Writable CD drives

Another backup medium is gaining popularity the writable CD drive. Writable CD drives have several advantages over tape, the primary one being that CDs are random access medium. This means that the CD can quickly locate a particular file on the CD without sequentially scanning through the entire drive. This is useful when you need to keep a revision history of frequently changing data files (as source for a software project or drafts of legal documents).

Although people believe that CDs have a very long life, that belief comes into question. CDs are still a good choice for people who believe they have a long life, but for short-term storage, they are fine. If you need them to last longer, you should consider DVDs.

The storage space of CDs is limited to 700MB per CD. DVDs have a larger capacity (4.7GB, although the actual capacity you can achieve is less). DVD-9 and DVD-5 DVDs store up to 8.5GB of data. DVD drives and DVD-R disks are relatively expensive (although they are coming in down). More manufacturers DVD writers to their PCs, DVD will eventually replace CDs as the most common removable media drives.

## Writing to CDs

To write to CDs, you would typically use the `mkisofs` command. This command creates an ISO9660 file system image. Once the image is created, you can use a tool like `cdrecord` or `wodim` to burn the image to a CD or DVD.
