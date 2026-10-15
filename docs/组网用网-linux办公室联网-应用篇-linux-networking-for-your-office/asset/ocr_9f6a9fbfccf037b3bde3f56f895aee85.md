# Tip

If you're using a Linux computer to serve Macintosh files, you can use mkhybrid, in conjunction with its -hfs and --netatalk options, to create a CD-ROM that, when read on a Macintosh, displays the contents of the CD-ROM as they appeared on the Linux server via Netatalk. This can be a very convenient way to distribute Macintosh files from a server. You can also use Apple's Disk Copy utility to accomplish the same goals, but a CD-ROM created with Disk Copy contains only HFS structures, so it can't be read on computers that don't understand HFS. If you use mkhybrid, the CD-ROM will also contain ISO-9660 data structures, so you can access the files on PCs or other systems. (Disk Copy is discussed later in this chapter, in the section "Backing Up to Disk.")

As an example, here's how you might back up the /home directory tree to CD-R by using mkisofs and cdrecord:

```
mkisofs -R -J -o outfile.iso /home/
cdrecord -pad dev=6,0 outfile.iso
```

You can eliminate the intermediate file outfile.iso by piping the mkisofs output directly into cdrecord:

```
mkisofs -R -J /home/ | cdrecord -pad dev=6,0 -
```

The problem with this approach is that, because CD recording is very timing-sensitive and because both the CD image creation and burning occur simultaneously, the image creation process is more likely to fail. You're generally safer creating an intermediate file, but if you're short on disk space or have a fast system, you might give the piped solution a try.

The mkisofs command specifies that both Rock Ridge (-R) and Joliet (-J) extensions be used, so you'll be able to read long filenames on the CD in Linux, in other UNIX flavors, and in Windows. The uppercase form of the Rock Ridge switch tells mkisofs to preserve file ownership and permissions, as much as possible. When creating CD-ROMs for distribution, you probably want to use the lowercase form (-r), which changes ownership to root and permissions to -r--r--r-- (with execute bits added when appropriate). This makes the CD readable by all users. For backup, though, preserving the original ownership and permissions is generally more desirable.

To use cdrecord, you must have SCSI generic support selected in the SCSI support section of the kernel configuration. If you're using an EIDE/ATAPI CD-R drive, you should specify SCSI emulation support in the Block devices area; this allows you to access the EIDE/ATAPI CD-R drive as if it were a SCSI device. The dev=6,0 option to cdrecord specifies the device ID—device 6, logical unit (LUN) 0 in this case (most SCSI CD-R drives use a LUN of 0).