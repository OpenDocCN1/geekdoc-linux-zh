# **MDeltree** The *mdeltree* command is used to delete an MS-DOS file. Its syntax is

```
mdeltree [-v] msdosdirectory [msdosdirectories...]
```

**Mdeltree** removes a directory and all the files and subdirectories it contains from an MS-DOS filesystem. An error occurs if the directory to be removed does not exist.

# **Mdir** The *mdir* command is used to display an MS-DOS directory. Its syntax is

```
mdir [-w] msdosdirectory
mdir [-f] [-w] [-a] msdosfile [msdosfiles...]
```

**Mdir** displays the contents of an MS-DOS directory.

**Mdir** supports the following command line options:

+   - **w**	Wide output. With this option, **mdir** prints the filenames across the page without displaying the file size or creation date.
+   - **a**	Also list hidden files.
+   - **f**	Fast. Do not try to find free space. On larger disks, finding out the amount of free space takes up some non trivial amount of time, as the whole FAT must be read in and scanned. The *-f* flag bypasses this step. This flag is not needed on FAT32 filesystems, which store the size explicitly.

An error occurs if a component of the path is not a directory.

# **Mformat** The *mformat* command is used to add an MS-DOS filesystem to a low-level formatted diskette. Its syntax is

```
mformat [-t cylinders] [-h heads] [-s sectors] [-l volume_label]
[-F] [-1 fsVersion] [-S sizetode] [-2 sectors_on_track_0]
[-M software_sector_size] [-a] [-X] [-C] [-H hidden_sectors]
[+- root_sectors] drive:
```

**Mformat** adds a minimal MS-DOS filesystem (boot sector, FAT, and root directory) to a diskette that has already been formatted by a Unix low-level format.