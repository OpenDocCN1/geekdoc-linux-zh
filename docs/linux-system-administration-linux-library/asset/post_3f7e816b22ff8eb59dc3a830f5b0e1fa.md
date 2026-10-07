
# Chapter 11 Backing Up and Restoring

To create a CD-R image file, you must pass mkisof the name of a directory to be turned into a CD-R, the name of an output file, and any of a large number of optional parameters. A fairly basic example is:

```
$ mkisof -r -J -o output-file.iso /source/directory
```

This example creates an image file called output-file.iso from the contents of /source/directory. The -r parameter adds Ridge extensions (with some changes to permissions and ownership to help make the disk portable), and the -J parameter adds a Joliet filesystem. The mkisof page includes extensive discussion of the many additional parameters available for this utility.

You may use the loopback capability of Linux to check whether the image created by mkisof has a directory structure and permissions that match the original files. Loopback is the capability that allows you to mount a file if it were a disk partition. To do this, use the following command, inserting the correct name for the created image and the correct path to the mount point you wish to mount the image on:

```
# mount -o iso9660 -o loop cd_image /mnt/tmp
```

> TIP We typically create a /mnt/tmp for mounting partitions or files that are not so permanently mounted as CD-ROM drives and floppy drives. You can use it to mount anything temporarily, regardless of device.

Compare /mnt/tmp wherever your original files are located until you are convinced that the contents are the same. Then use the following command to unmount the CD-R image you've created:

```
# unmount /mnt/tmp
```

cdrecord Once you've made and tested an image file, you'll use cdrecord utility to actually write the CD-ROM image to the blank CD-R. cdrecord was designed for use with SCSI or ATAPI CD-recorders. It can write data, audio, media, and multisession disks and supports most CD recorders available. cdrecord is run from the command line and has a great many options. The main page is quite helpful, but the process is not simple. The simplest case, a pure data image copied to it with an ISO-9660 filesystem on a sufficiently quick system using the device at SCSI target ID 6 as its target, allows you to run the command as:

```
# cdrecord -v speed=2dev/0,6 cd_image
```

For better readability, the SCSI settings of the writer are stored in three environment variables: SCSI_BUS, SCSI_ID, and SCSI_LUN.

If you use cdrecord to overwrite a CD-RW, you must add the option blank=blanktype to erase the old content. The program can blank the CD-RW in several different ways, as summarized in Table 11.4.

### Table 11.4 Options for Blanking a CD-RW Disc with cdrecord

| blanktype | Description |
|---|---|
| help | Displays a list of possible blanking types. |
| all | Completely erases the entire disc. This may take a long time. |
| fast | Erases key data structures on the disc; fast but incomplete. |
| track | Erases a single track. |
| unreserve | Unreserves a reserved track. |
| trtail | Erases the tail of a track. |
| unclose | Uncloses last session; allows writing additional information to a previously finished writing session. |
| session | Erases the last session. |

On a sufficiently speedy machine, the output of mkisof can be directed into cdrecord using a pipe. You first need to obtain the image size. To do this, use this form of the mkisof command:

```
$ mkisof -R -q -print-size cd_image
```

Next, pipe the mkisof command into the cdrecord command, passing the image size to cdrecord as shown:

```
$ mkisof -R cd_image | cdrecord -v fs=6m speed=2 dev=0,6,0 - X-CD-Roast
```

CD-Roast, illustrated in Figure 11.4, is an X-based front end for CD programs like mkisof, paranoia, and cdrecord. It gives a nice interface from which to run these programs, which are usually command-driven. This program is growing quite popular among Linux users and is available from http://www.ertfur.thur.de/ak/xcdroast.html.

Figure 11.4 The X-CD-Roast main screen

![](img/4fb617eb648f87def380ef5d92052d01_389_0.png)

# Device Access

You may have noticed the example of cdrecord the command didn't take a conventional device filename. Instead, this utility takes a SCSI device specification in the form bus,id,1un

where bus is the SCSI bus (0 on systems with just one SCSI host adapter), id is the SCSI ID number of the CD-R drive, and 1un is the logical unit (LUN) of the drive (almost 0). This identification ultimately leads to the SCSI generic devices (/dev/sgx, x is a letter from a forward). Unlike SCSI devices for tape drives, disks, and so on, the SCSI generic devices are designed to allow access to any type of SCSI device, which is why cdrecord uses them—these devices allow the sort of low-level access that's required for writing to a CD-R drive. You must be sure the SCSI generic support is compiled into your kernel (or available as a kernel module). This option is called SCSI Generic Support in the SCSI Support kernel configuration menu.

This all works for SCSI devices, but what IDE/ATAPI CD-R drives? For these, you must turn on a Linux kernel feature that allows an IDE device to masquerade

as a SCSI device. The option is in the Block Devices kernel configuration menu and is called SCSI Emulation Support. Once this is compiled and active, your CD-R drive will turn up as a SCSI generic device.

NOTE Chapter 8 covers kernel compilation in more detail.

Most CD-R drives can be accessed as ordinary CD-ROM drives for read-only access. For SCSI devices, the appropriate device filenames are /dev/sd0 (or higher numbers), and for IDE/ATAPI devices, the device filenames are /dev/hda through /dev/hdd or above, depending upon the chain to which the device is attached and its master/slave status. The read-only CD-ROM access does not help in making backups, but it can be useful in restoring data from a CD-R you've created.

# Linux Backup and Restore Tools

Linux provides several tools you can use to back up: dump, tar, cpio, and afio. We'll look at dump first.

# dump

The incremental dump backs up a file if it has changed since the previously recorded backup. A standard incremental scheme begins at level 0 and extends to level 9, 0 being a full dump and 1–9 being incremental. Each incremental level backs up all files changed since the last backup of a lower incremental level. If you perform a series of dump operations (say, one per day) using the non-0 dump level, the result is a series of incremental backups, as described earlier in this chapter. If you increase the dump level with each backup (say, 1 on Monday, 2 on Tuesday, and so on), the result is a series of differential backups,

The dump utility (which comes with most Linux distributions) looks at the specified filesystem. The standard Linux dump handles ext2 filesystems, but not FAT filesystems or the journaling filesystems described in Chapter 10. Trying to use dump on such filesystems won't cause problems, neither will it work.

![](img/4fb617eb648f87def380ef5d92052d01_390_0.png)

# Chapter 11 Backing Up and Restoring

> **NOTE** Because dump operates on a lower level of access than most backup utilities, any dump must have explicit support for any filesystem you use.

# Basic dump Operation

The dump command's basic syntax is this:

```
dump [-level] [-b blocksize] [-B records] [-f file] [-u] directory
```

The meanings of these parameters are as follows:

- **level**: The incremental level.
- **blocksize**: The size (in bytes) of a dump block. Combined, blocksize and **records** The size of the tape in dump blocks allow dump to handle tapes that are smaller than the data to be; if dump must back more than blocksize records it pauses when it reaches this limit and prompts you to change tapes.
- **file**: The file to which the backup should be written—normally a tape device file, as described earlier.
- **u**: This parameter causes dump to store data about its backup history in /etc/dumpdays. Without this parameter, incremental backups won't work correctly.
- **directory**: The directory or filesystem device to be backed up.

Suppose you want to implement an incremental backup strategy in which you would backup on Sundays and back up all files changed since Sunday every other day of the
