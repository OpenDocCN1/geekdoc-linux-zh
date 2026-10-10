the first IDE drive (/dev/hda1). If you have other DOS drives (D, for example), you can add another line that defines drive D as the appropriate disk partition.

If your system's A drive is a high-density, 3.5-inch drive, you don't need to change anything in the default /etc/mtools.conf file to access the floppy drive. If you also want to access any DOS partition in the hard drive, uncomment and edit an appropriate line for the C drive.

You also can access Iomega Zip drives through mtools. Simply specify a drive letter and the appropriate device's filename. For built-in IDE (ATAPI) Zip drives, try /dev/hdd4 as the device file and add the following line in the /etc/mtools.conf file:

```
drive e: file="/dev/hdd4"
```

After that, you can use mtools commands to access the Zip drive (refer to it as the E drive). For example, to see the directory listing, place the Zip disk in the Zip drive and type:

```
mdir e:
```

# Learning the mtools commands

The mtools package is a collection of utilities. So far, I have been using mdir — the mtools counterpart of the DIR command in DOS. The other mtools commands are fairly easy to use.

If you know MS-DOS commands, using the mtools commands is easy. Type the DOS command in lowercase letters and remember to add m in front of each command. Because the Linux commands and filenames are case-sensitive, you must use all lowercase letters as you type mtools commands.

Table 3-4 summarizes the commands available in mtools.

| Table 3-4 | The mtools Commands |
| mtools Utility | MS-DOS Command (If Any) | Changes MS-DOS file-attributeflags |
| mattrb | ATTRIB | Tests a floppy disk and marks the badblocks in the file allocation table (FAT) |
| mbadblocks | CD | Changes an MS-DOS directory |
| mcd | COPY | Copies files between MS-DOS and Linux |
| mcopy | DEL or ERASE | Deletes an MS-DOS file |
| mdel | DELTREE | Recursively deletes an MS-DOS directory |
| mdeltree | | |