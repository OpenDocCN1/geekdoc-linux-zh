
![](img/5d4d3092919d1d16884788127447cc6d_345_0.png)

## FIGURE 13.2

X-CD-Roast lets you select a directory for backup, then creates an image file and burns a CD from the image file.

You can use tar to create your image file. When you need to restore the file, you issue the same commands as if you were restoring from tape, except that you specify the CD-ROM or CD-R drive’s device file rather than a tape device file, and the mt commands would not work. Such a CD would be unreadable in Windows or most non-Linux/non-UNIX OSs. Alternatively, you can use the mkisofs or mkhybrid programs to create a standard ISO-9660 image file that can be mounted and read normally. This provides for easier random access to all files on the archive, but you might lose important information. One particularly important problem with creating an ISO-9660 image (even with Rock Ridge extensions) is that all the files on that image are read-only, which can cause serious problems after restoration.

The mkisofs package comes with Red Hat Linux, but you need to look elsewhere for the others. mkhybrid can be found at http://www.ps.ucl.ac.uk/~jcpearso/mkhybrid.html, and provides the ability to create Macintosh HFS CD-ROMs, in addition to the ISO-9660, Rock Ridge, and Joliet support by mkisofs. The cdrecord package is available from http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html. Both are also on the CD-ROM that accompanies this book, in the sams-extras/backup directory.

## Tip

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
