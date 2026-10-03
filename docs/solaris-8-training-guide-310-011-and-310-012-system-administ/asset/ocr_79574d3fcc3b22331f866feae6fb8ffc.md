| Option | Description |
|---|---|
| -m | Shows the command line that was used to create the specified file system. No changes are made to the file system. |
| -v | Verbose. Shows the command line, but does not execute anything. |
| -o <specific options> | A list of options specific to the type of file system. The list must have the following format: -o followed by a space, followed by a series of keyword [=value] pairs, separated by commas, with no intervening spaces. |
| apc=<n> | Reserved space for bad block replacement on SCSI devices. The default is 0. |
| N | Prints the file system parameters without actually creating the file system. |
| nsect=<n> | The number of sectors per track on the disk. The default is 32. |
| ntrack=<n> | The number of tracks per cylinder on the disk. The default is 16. |
| bsize=<n> | Logical block size, either 4096 (4KB) or 8192 (8KB). The default is 8192. The sun4u architecture does not support the 4096-block size. |
| fragsize=<bytes> | The smallest amount of disk space, in bytes, to allocate to a file. The value must be a power of 2 selected from the range 512 to the logical block size. If the logical block size is 4096, legal values are 512, 1024, 2048, and 4096. If the logical block size is 8192, 8192 is also a legal value. The default is 1024. |
| cgsize=<cyls> | The number of cylinders per cylinder group. The default is 16. |
| free=<n> | The minimum percentage of free space to maintain in the file system. This space is off-limits to normal users. After the file system is filled to this threshold, only the superuser can continue writing to the file system. This parameter can be subsequently changed using the tunefs command. The default is 10 percent, however, on large file systems; the minfree value is determined automatically. |
| rps=<rps> | The rotational speed of the disk, specified in revolutions per second. The default is 60. |

continues