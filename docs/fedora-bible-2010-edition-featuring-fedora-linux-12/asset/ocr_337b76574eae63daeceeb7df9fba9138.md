| Command | Function |
| :-- | :-- |
| mcopy | The DOS `copy` command, which is used to copy files from one location to another. |
| mdel | The DOS `del` command, which is used to delete files. |
| mdeltree | The DOS `deltree` command, which deletes an MS-DOS directory along with the files and subdirectories it contains. |
| mdir | The DOS `dir` command, which lists a directory's contents. |
| mdu | The Linux `du` command, which is used to show the amount of disk space used by a DOS directory. |
| mformat | The DOS `format` command, which is used to format a DOS floppy disk. |
| minfo | This command is used to print information about a DOS device, such as a floppy disk. |
| mkmanifest | This command is used to create a shell script that restores Linux filenames that were truncated by DOS commands. |
| mlabel | The DOS `label` command, which is used to make a DOS volume label. |
| mmd | The DOS `md` command, which is used to create a DOS directory. |
| mmount | This command is used to mount a DOS disk in Linux. |
| mmove | The DOS `move` command, which is used to move a file to another directory and/or rename it. |
| mrd | The DOS `rd` command, which is used to remove a DOS directory. |
| mren | The DOS `ren` command, which is used to rename a DOS file. |
| mshowfat | This command is used to show the FAT entry for a file in a DOS file system. |
| mtoolstest | This command is used to test the `mtools` configuration files. |
| mtype | The DOS `type` command, which is used to display the contents of a DOS text file. |
| mzip | This command is used to perform operations with Zip disks, including eject, write protect, and query. |

You can use `mtools` utilities to copy files between your Linux system and a Windows system that is not on your network. You can use `mcopy`, which lets you copy files using drive letters instead of device names. In other words, to copy the file `vi.exe` from floppy drive A: to the current directory in Linux, you would type:

```
`# mcopy a:/vi.exe .`
```