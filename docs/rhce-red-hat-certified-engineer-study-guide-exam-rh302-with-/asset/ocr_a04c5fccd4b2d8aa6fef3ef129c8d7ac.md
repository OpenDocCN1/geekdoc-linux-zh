/dev/cdrom /cdrom1 iso9660 noauto,ro 0 0
/dev/hdd /cdrom2 iso9660 noauto,ro 0 0
none /proc defaults 0 0
none /dev/pts devpts mode=0622 0 0

Each line in the file describes a file system. The fields are as follows:

+   - The device file.

+   - The mount point.

+   - The file system type. Table 15.5 summarizes the file system types supported by Linux.

+   - The mount options. Table 15.6 summarizes the available options.

+   - The dump flag. The value 1 indicates a file system that is automatically included in a system dump; the value 0 indicates a file system that should not be included.

+   - The file system check sequence. The value 1 indicates the root file system; the value 2 indicates a non-root file system that should be automatically checked; the value 0 indicates a file system that should not be checked.

# TABLE 15.5 Linux File System Types

| File System Type | Description |
| adfs | Acorn RiscOS file system |
| affs | AmigaOS file system |
| coda | Coda, an advanced network file system similar to NFS |
| devpts | A virtual file system for pseudo terminals |
| ext2 | The standard Linux file system |
| hfs | Apple Macintosh file system |
| hfs | IBM OS/2 file system |
| iso9660 | The standard CD-ROM file system |
| minix | Tanbaum’s MINIX file system |