
backup packages. Most of them are included with the main Linux distributions; the others can be downloaded from Internet sites.

## Tape Utilities

Tape utilities are programs that help manage tape access and usage. These aren't backup programs, in fact they often do not write to the tape at all; instead, they perform functions necessary to the backup process like finding a specific position on the tape or allowing you to re–tension the tape.

`mt`

The mt utility performs a number of tape operations, such as moving to or finding a specified position on the tape, setting or checking the tape's tension, setting or checking the tape's compression, setting or checking the block size or density, and erasing the tape. The mt command is used when you need to rewind the tape prior to writing to it, to erase the tape, to reposition the head before a write, or to auto–eject the tape when the backup has been completed.

If you are using QIC tapes, you should always re–tension the tape before you write to it. For some reason, QIC tapes are much more sensitive to tension than are other tapes. The command to do this with a nonrewinding tape drive is:

`# mt -f /dev/nftape reten`

**Note** This discussion uses /dev/nftape as the tape device. You may need to use another device file, as discussed shortly. In any event, mt is normally used with *nonrewinding* device files, which do not rewind the tape automatically after each access. *Rewinding* devices, by contrast, automatically rewind the tape after each access. The former are used when you want to store more than one backup per tape, and the latter are used when you want to write a single backup to a tape or access only the first backup that already exists on a tape.

The mt utility is also used to erase the tape. You'll usually need to do this before using ftpwrite with a tape that was preformatted since ftpwrite sometimes doesn't like the formatting that is on a new tape.

`# mt -f /dev/nftape erase`

The mt utility is useful when you want to move forward on the tape. The following sample command will move two files forward on the tape:

`# mt -f /dev/nftape fss 2`

**Note** In reference to a tape drive, a *file* is a single backup, which may contain many files from the disk. Think of it as a tarball stored on tape (which it may in fact be). You might store multiple backups on one tape, particularly when doing incremental or differential backups.

To put more than one backup on a single tape, you must use the mt utility with its eof keyword. The following command moves the tape just past the end of the written data, where the next backup can begin. Any attempt to read the tape after issuing this command will result in errors, but it's necessary if you want to write data to a tape without overwriting existing data.

`# mt -f /dev/nftape eof`

The rmt utility is used by the remote dump and restore utilities to manipulate a tape drive located on a remote backup server in the same way that mt does with local tape drives. The rmt utility accepts requests specific to the manipulation of magnetic tapes, performs the requested manipulation, and then responds with a status indicator. rmt is not usually started separately but is rather used with an rsh or rcmd call, both of which are used to execute a command on a remote server.

## Tape Device Names

Backup commands invariably require you to identify the tape device by name. The tape device name will vary depending upon the interface to which it is connected and the number of devices on that chain. There are IDE tape devices, SCSI tape devices, and ftape devices (both floppy–interfaced and parallel–interfaced), USB devices work like SCSI devices.

### IDE/ATAPI

Tape devices that use the IDE interface are accessed through the /dev/ht0 (rewinding) and /dev/nht0 (nonrewinding) device files. If you have more than one IDE/ATAPI drive, change the 0 to 1 or above to address the second and subsequent drives.

A modern computer motherboard usually will support two IDE chains, although they may not both be enabled in the system's BIOS. Each chain supports up to two devices (hard disks, tape drives, and so on). Historically, the motherboard did not provide the IDE connections itself but relied upon the existence of an IDE controller card. Few systems use separate IDE controllers now. Although it is possible to accommodate additional IDE devices by adding an IDE controller card to a system's existing IDE chains on the motherboard, the requirement for each controller to have a unique interrupt makes this difficult to configure. For this reason, you're better off using SCSI if you need more than four devices.

### SCSI

The first SCSI tape drive is attached to /dev/st0 if it is rewinding or /dev/nst0 if it is nonrewinding. To refer to subsequent drives, increment the number as needed. Because SCSI host adapters support 7 or 15 devices, depending upon the adapter type, and each adapter uses a single interrupt, SCSI is well–suited for systems with lots of disk and tape drives.

#### ftape

An ftape device uses one of four methods of access depending upon the floppy tape drive itself. The /dev/rft0 (rewinding) and /dev/nrft0 (nonrewinding) devices provide access to the first device; incrementing the number provides access to additional ftape–driven drives. For compatibility, /dev/ftape and /dev/nftape are symbolic links to /dev/rft0 and /dev/nft0, respectively. These device filenames work for both floppy–interfaced and parallel–port–interfaced drives driven via ftape.

Old 3.0x versions of ftape supported driver–level compression via the /dev/zqft0 and /dev/nzqft0 device files. This feature was removed from the 4.0 and later releases of the software, however, in order to provide improved error–recovery features.

## CD–R and CD–RW Backup Tools

Archiving data to CD–R or CD–RW (subsequently referred to collectively as CD–R for brevity's sake) is an option if you have a small amount of data to store, but isn't really helpful when you're backing up an entire network. If you are doing incremental backups on a system that doesn’t have many large files changing, CD–R might be an option. Sometimes, CD–R is useful for the archival backups mentioned earlier in this chapter. The long shelf life of CD–R media makes them a good choice for long–term archival storage, in fact. For larger backup jobs, though, tape is generally superior.

## CD–R Commands

Writing to a CD–R is a two–step process:

- The data (whether data files or audio files) must be accumulated and assembled into an image, which also includes any required formatting information.
- The created files must be written to the CD–R, usually with the utility cdrecord.

**Note** You’ll see later in this chapter that some GUI–based utilities perform these two functions without clearly identifying them as separate steps.

A certain amount of the free space on a CD–R must be reserved for storing the ISO–9660 filesystem (usually a few megabytes). This format, the standard filesystem for CD–ROMs, exists in three levels. Level 1 uses the 8+3 file naming convention and requires that the data be contiguous. Directory trees must not be nested more than eight levels deep under Level 1. The filenames on these discs can be viewed under both Linux and DOS. Level 2 allows longer filenames, and as a result, DOS may not be able to read all the files on a Level 2 disc. Level 3 does away with the requirement that the data be contiguous, keeping the less restrictive file naming convention, and again DOS may not be able to read all its files. In order to make the ISO–9660 format more useful in the Unix world, Rock Ridge extensions were added. These extensions define a way to handle mixed–case filenames and symbolic links. If this disc is read on a system that doesn’t have the Rock Ridge extensions, the filenames won’t display in their long format. Microsoft developed a different way of storing long filenames on CD–ROM and CD–R discs, known as Joliet. You can create a Joliet CD–R from Linux, but for storing Linux files, Rock Ridge is superior, because Joliet doesn’t support Linux file ownership or permissions. Creating a mixed Rock Ridge/Joliet CD–R is possible and useful in a mixed–OS environment.

## mkisofs

The mkisofs command creates the ISO–9660 filesystem image to be written to the CD by the cdrecord utility. This image includes the data files as well as the formatting information. The mkisofs utility does not, however, contain any CD–R driver code and therefore does not write the image to the CD–R. The developers chose this approach mainly to allow users to test an image from the hard drive before writing it to the CD–ROM. Historically, writing an image as it is being created was also potentially unreliable on slower computers.

To create a CD–R image file, you must pass mkisofs the name of a directory to be turned into a CD–R, the name of an output file, and any of a large number of optional parameters. A fairly basic example is:

`$ mkisofs -r -J -o cd_image.iso /source/directory`

This example creates an image file called cd_image.iso from the contents of /source/directory. The -r parameter adds Rock Ridge extensions (with some changes to permissions and ownership to help make the disc portable), and the -J parameter adds a Joliet filesystem. The mkisofs man page includes extensive discussion of the many additional parameters available for this utility.
