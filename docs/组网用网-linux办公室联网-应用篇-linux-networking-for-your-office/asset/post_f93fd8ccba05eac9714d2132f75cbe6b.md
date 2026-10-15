
## Case-Sensitivity in Linux and Other OSs

In addition to ownership and permissions, Linux treats filename case differently than do most desktop OSs. Once again, this means that file-sharing systems such as Samba and Netatalk must make compromises in handling situations where Linux’s and the client OS’s case assumptions differ.

There are three types of systems when it comes to handling case in filesystems:

- Case-insensitive—In a case-insensitive filesystem, only one case (uppercase or lowercase) is used. Typically, case-insensitive systems match your filename entries, whether or not they match the case of the file on the disk. Examples of case-insensitive systems include DOS with FAT and the ISO-9660 filesystem used on CD-ROMs.

- Case-retentive—A case-retentive filesystem records the case of filenames, but doesn’t care about case when matching files. For instance, a file might appear on disk as Monthly-Report.wpd, but you can access it by typing the filename monthly-report.wpd or mOnTHLy-RePorT.wPd. Windows 95 and above with VFAT or NTFS, OS/2 with its HPFS, and MacOS with HFS are all case-retentive systems.

- Case-sensitive—In a case-sensitive filesystem, case is both retained and significant. Thus, to access the file Monthly-Report.wpd, you must type precisely that; neither monthly-report.wpd nor mOnTHLy-RePorT.wPd will do. What’s more, all three of these filenames could exist in the same directory because their case distinguishes them from one another. UNIX flavors, including Linux, normally sport case-sensitive filesystems such as ext2fs.

Because Linux is a case-sensitive filesystem but the usual clients of Samba and Netatalk are either case-insensitive or case-retentive, the servers normally do extra work to try to match filenames and make the Linux filesystem appear to be case-retentive. Occasionally there are conflicts, though, as when two files in a directory differ only in case. In such situations, you need to log in to Linux and rename one file in order to gain access to both of them. If you don’t do that, only one of the files is available to the client.

When Linux accesses media from case-insensitive or case-retentive OSs, Linux normally treats the medium in a case-sensitive way. Exporting such a filesystem then undoes this, returning case-retentive properties to the medium. Details of how this is done differ somewhat from one filesystem to another, though, so check the options in Table 9.2 or in the mount manpage for further information.

## Serving Removable Media

Although most computers these days have floppy, CD-ROM, and even Zip or LS-120 drives, it's sometimes desirable to let a Linux computer serve removable media. Sometimes this is because the client computer lacks a particular type of drive, as is the case in my home network, where my iMac has no floppy drive, and I share a single Zip drive between all my computers. Other times Linux's great flexibility with filesystems can be a boon. For instance, if you use Windows computers exclusively except for a Linux server, but a client or colleague gives you a Zip disk created on a Macintosh, your Linux box can serve the Zip disk and you can read it on your Windows machines.

## Supported Filesystems

The four filesystems you're most likely to encounter in removable media are

- FAT for DOS, Windows, and OS/2 disks—Linux supports FAT using three different filesystem names: msdos, vfat, and umsdos. The umsdos filesystem is normally used to install Linux on a FAT partition, so you're not likely to encounter it on a removable-media device. The difference between the msdos and vfat filesystems is that the former enforces the 8.3 filename length limits of DOS, whereas the latter supports VFAT-style long filenames. Today, you'll probably want to support vfat on most or all FAT disks because if you choose vfat, you'll still be able to read and write older DOS disks. If you write a file with a long filename to such a disk, though, and then read it on a DOS computer, you'll see a truncated version of the filename. This is no different from writing a disk with Windows 95 or above and then reading it with DOS.

> NOTE
> Linux normally converts 8.3-style filenames to lowercase when it reads them from FAT floppies. This contrasts with DOS and Windows, which read these filenames entirely in uppercase. (The Windows GUI environment usually converts them to lowercase with a leading uppercase letter, though.) This fact means that your filenames can shift in case if you swap them between Linux and Windows computers via removable disks, but because Windows is a case-retentive OS, this shift normally has few or no practical consequences.

- HFS for Macintosh disks—Macintoshes use a filesystem known as HFS, both for removable media such as floppies and Zip disks and often for CD-ROMs. With the 2.2-series kernel, Linux has added support for HFS, so you can read and write these disks. Linux
