| mtools Utility | MS-DOS Command (If Any) | Action |
|---|---|---|
| mren | REN or RENAME | Renames an existing MS-DOS file |
| mtype | TYPE | Displays the contents of an MS-DOS file |
| xcopy | XCOPY | Recursively copies a DOS directory into another |

You can use the mtools commands just as you use the corresponding DOS command. For example, the mdir command works like the DIR command in DOS. The same goes for all the other mtools commands shown in Table 16-1.

Formatting a DOS/Windows floppy disk

Suppose you have to copy some files on an MS-DOS/Windows floppy disk. If you already have a formatted MS-DOS/Windows floppy, you can simply mount that floppy and copy the files to the floppy using the Linux cp command. What if you do not have a formatted DOS floppy? The mtools package again comes to the rescue.

The mtools package provides the mformat utility, which can format a floppy disk for use under MS-DOS. Unlike the DOS format command that formats a floppy in a single step, the mformat command requires you to follow a two-step process:

+   1. Use the fdformat Linux command to low-level format a floppy disk. The fdformat command expects the floppy device name to be the argument; the device name includes all the parameters necessary for formatting the floppy disk. To format a 3.5-inch high-density floppy disk in your system's A: drive, type `fdformat /dev/fd0H1440`.
+   2. Use the mformat command to put an MS-DOS file system on the low-level formatted floppy disk. If the floppy is in drive A:, type the following command:
+      `mformat a:`

![](bbox=[0.01, 0.62, 0.11, 0.71])

# REVIEW

This session showed you how to access and mount the DOS/Windows file systems from Red Hat Linux and how to mount a DOS/Windows file system with the mount command. You also learned how to use the mtools utility programs to format and access a DOS/Windows floppy disk directly from Red Hat Linux without first having to mount the floppy disk.