# ## Formatting magnetic tapes

The flape-tools package also includes a tool for formatting tapes as well. Most tapes now come preformatted. In the event that you have an older floppy controller tape drive that uses unformatted tapes, use the `ftformat` command to format them:

```
$ /usr/local/bin/ftformat -f /dev/qft0
```

Usually, the -f parameter with the device name is the only parameter that you need to supply. Nevertheless, you are encouraged to read the online man page for ftformat to learn more about its options and capabilities.

# ## Writable CD-ROM drives

Another backup medium that is gaining popularity is the writable CD-ROM drive. Writable CD-ROM drives have several advantages over tape, the primary one being that CDs are a random access medium. This means that the CD drive can quickly locate a particular file on the CD without sequentially scanning through the entire disc. This is useful when you need to keep a revision history of frequently changing data files (such as source code for a software project or drafts of legal documents).

Another advantage is the extremely long life span of CDs. If you wish to archive your backups for a very long time, a writable CD drive is a good choice. If your backups are intended for short-term storage, you should probably consider a rewritable CD drive. A rewritable CD (unlike plain writable CDs) can be reformatted and used to store new backups.

The biggest drawback is that a CD can store at most about 650MB of data. In contrast, DVDs can store 4.7GB of data and many tape drives can store multiple gigabytes of data. For example, DAT DDS-3 tapes can hold up to 24GB of compressed data, while 8mm AIT-2 tapes can hold up to 100GB of compressed data.

# ## Getting cdrecord for writable CDs

To write CDs with Red Hat Linux you need to install the cdrecord package. This package contains components such as the cdrecord, devdump, isodump, isoinfo, isovfy, and readcd commands. The cdrecord package is included with the Red Hat Linux distribution.

> NOTE: The cdrecord package requires that you use a SCSI CD drive. If you have an IDE/ATAPI CD drive, which is a very popular device, you may need to configure that drive to do SCSI emulation. For the latest versions of Red Hat Linux, however, SCSI emulation is usually taken care of automatically. See Chapter 8 for a description of how to configure an IDE/ATAPI CD drive for SCSI emulation.

# ## Writing to CDs

Because the data written to a CD becomes permanent once it is written, you need to format the CD and copy files to it all in one step. If you formatted it first, you would end up with an empty file system on a CD that can no longer be written to.