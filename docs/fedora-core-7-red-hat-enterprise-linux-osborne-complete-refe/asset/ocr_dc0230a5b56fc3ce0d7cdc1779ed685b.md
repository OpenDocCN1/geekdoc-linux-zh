mounting, are required. With mtools, you needn't mount an MS-DOS partition to access it. For an MS-DOS floppy disk, place the disk in your floppy drive, and you can then use mtool commands to access those files. For example, to copy a file from an MS-DOS floppy disk to your Linux system, use the `mcopy` command. You specify the MS-DOS disk with `a:` for the A drive. Unlike normal DOS pathnames, pathnames used with mtool commands use forward slashes instead of backslashes. The directory `docs` on the A drive would be referenced by the pathname `a:/docs`, not `a:\docs`. Unlike MS-DOS, which defaults the second argument to the current directory, you always need to supply the second argument for `mcopy`. The next example copies the file `mydata` to the MS-DOS disk and then copies the `preface` file from the disk to the current Linux directory.

```
$ mcopy mydata a:
$ mcopy a:/preface .
```

> You can use mtools to copy data to Windows-formatted floppy disks or to a Windows FAT32 partition, which can also be read or written to by Windows XP, but you cannot access Windows XP, NT, or 2000 hard disk file systems (NTFS) with mtools. The NTFS partitions require a different tool, the NTFS kernel module (see Chapter 4).

You can use the `mdir` command to list files on your MS-DOS disk, and you can use the `mcd` command to change directories on it. The next example lists the files on the MS-DOS disk in your floppy drive and then changes to the `docs` directory on that drive:

```
$ mdir a:
$ mcd a:/docs
```

Access to MS-DOS or Windows 95, 98, or ME partitions by mtools is configured by the `/etc/mtools.conf` file. This file lists several different default MS-DOS or Windows partitions and disk drives. Each drive or partition is identified with a particular device name.

# Archiving and Compressing Files

Archives are used to back up files or to combine them into a package, which can then be transferred as one file over the Internet or posted on an FTP site for easy downloading. The standard archive utility used on Linux and Unix systems is `tar`, for which several GUI front ends exist. You have several compression programs to choose from, including GNU zip (gzip), Zip, bzip, and compress.

# Archiving and Compressing Files with File Roller

Red Hat and Fedora provide the File Roller tool (accessible from the Accessories menu, labeled Archive Manager) that operates as a GUI front end to archive and compress files, letting you perform Zip, gzip, tar, and bzip2 operation using a GUI interface (see Figure 10-4). You can examine the contents of archives, extract the files you want, and create new compressed archives. When you create an archive, you determine its compression method by specifying its filename extension, such as `.gz` for gzip or `.bz2` for bzip2. You can select the different extensions from the File Type menu or enter the extension yourself. To both archive and