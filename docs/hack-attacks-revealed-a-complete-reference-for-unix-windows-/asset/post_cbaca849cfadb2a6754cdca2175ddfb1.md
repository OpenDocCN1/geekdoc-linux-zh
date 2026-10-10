
## Comments

The copy command accepts the following switches:

- /v Causes DOS to verify that the sectors written on the target disk are recorded properly.
- /a Lets you copy ASCII files. This switch applies to the filename preceding it and to all remaining filenames in the command, until copy encounters another /a or /b switch.
- /b Lets you copy binary files. This switch applies to the filename preceding it and to all remaining filenames in the command, until copy encounters another /a or /b switch. This switch tells the command processor to read the number of bytes specified by the file size in the directory.

## Examples

To copy a file called *letter.doc* from your working drive directory to a directory on drive C called *docs*, type:

```
copy letter.doc c:\docs
```

You can also combine several files into one by:

```
copy *.doc combine.doc
```

This takes all the files with an extension .doc and combines them into one file named *combine.doc*.

## Ctty

Ctty lets you change the device from which you issue commands.

### Syntax

```
ctty device
```

Where *device* specifies the device from which you are giving commands to DOS.

### Comments

Ctty is useful if you want to change the device on which you are working. The letters tty represent your terminal—that is, your computer screen and keyboard.

### Examples

The following command moves all command I/O from the current device (the console) to an AUX port, such as another terminal:

```
ctty aux
```

The next command moves I/O back to the console screen and keyboard:

```
ctty con
```

## Date

Date enters or changes the date.

### Syntax

```
date [mm-dd-yy]
```

### Comments

Remember to use only numbers when you type the date. The allowed numbers are:

- mm = 1–12
- dd = 1–31
- yy = 80–79 or 1980–2079

The date, month, and year entries may be separated by hyphens (-) or slashes (/).

### Example

To display the current date type:

```
date
```

The current date will appear with the option to change the date. If you do not want to change the date shown, simply press Return.

## Del(Erase)

This command deletes (or erases) all files specified by the drive and pathname.

### Syntax

```
del [drive:]pathname
erase [drive:]pathname
```

### Comment

Once you have deleted a file from your disk, you cannot easily recover it.

### Examples

The following deletes a file named report:

```
del report
```

Suppose you have files named report.jan, report.feb, report.mar, report.apr, report.may, and so on. To erase them all type:

```
del report.*
```

## Dir

Dir lists the files in a directory.

### Syntax

```
dir [drive:][pathname][/p][/w]
```

### Comments

The dir command, typed by itself, lists all directory entries in the working directory on the default drive. If you include a drive name, such as dir b:, all entries in the default directory of the disk in the specified drive will be listed.

The dir command accepts the following switches:

- /p Page mode; causes the directory display to pause once the screen is filled. To resume, press any key.
- /w Wide mode; causes the directory display to fill the screen, up to five files per line. This does not pause if the whole screen is filled.

Dir lists all files with their size in bytes and the time and date of the last modification.

### Example

If your directory contains more files than you can see on the screen at one time, type:

```
dir /p
```

## Diskcomp

Diskcomp compares the contents of one disk to another.

### Syntax

```
diskcomp [drive1:] [drive2:] [/1] [/8]
```

### Comments

Diskcomp performs a track-by-track comparison of the disks. It automatically determines the number of sides and sectors per track, based on the format of the source disk.

The diskcomp command accepts the following switches:

- /1 Causes diskcomp to compare just the first side of the disk.
- /8 Causes diskcomp to compare just the first eight sectors per track.

### Example

If your computer has only one floppy disk drive, and you want to compare two disks, type:

```
diskcomp a:
```

## Diskcopy

Diskcopy copies the contents of one disk to another.

### Syntax

```
diskcopy [drive1] [drive2:][ /1]
```

Where drive1 is the source drive, and drive2 is the target drive.

### Comments

Drive1 and Drive2 may be the same drive; simply omit the drive options. If the target disk is not formatted, diskcopy formats it exactly as the source disk.

The diskcopy command accepts the following switch:

- **/1** Allows you to copy only one side of a disk.

### Example

To copy the disk in drive A to the disk in drive B, type:

```
diskcopy a: b:
```

## Exe2bin

Exe2bin converts executable files to a binary format.

### Syntax

```
exe2bin [drive:]pathname1 [drive:]pathname2
```

Where pathname1 is the input file, and pathname2 is the output file.

### Comments

This command converts .exe files to binary format. If you do not specify an extension for pathname1, it defaults to .exe. The input file is converted to a .bin file format (a memory image of the program) and placed in the output file pathname2.

If you do not specify a drive name, exe2bin uses the drive of the input file. Similarly, if you do not specify an output filename, exe2bin uses the input filename. Finally, if you do not specify a filename extension in the output filename, exe2bin gives the new file the extension .bin.

### Restrictions

The input file must be in valid .exe format produced by the linker. The resident or actual code and data part of the file must be less than 64 KB, and there must be no STACK segment.

## Exit

This command exits the command.com program, and returns to a previous level, if one exists.

### Syntax

```
exit
```

### Comment

If you use the DOS command program to start a new command processor, you can use the exit command to return to the old command processor.

## Fastopen

Fastopen decreases the amount of time it takes to open frequently used files and directories.

### Syntax

```
fastopen [drive:[=nnn][... ]]
```

Where nnn is the number of files per disk.

### Comments

Fastopen tracks the location of files and directories on a disk for fast access. Every time a file or directory is opened, fastopen records its name and location. Then, if a file or directory recorded by fastopen is reopened, the access time is greatly reduced.

Note that fastopen needs 40 bytes of memory for each file or directory location it tracks.

### Example

If you want DOS to track the location of up to 100 files on drive C, type:

```
fastopen c:=100
```

## Fc

Fc compares two files or two sets of files, and displays the differences between them.

### Syntax

For ASCII comparisons:

```
fc [/a] [/c] [/L] [/LB n] [/n] [/t] [/w] [/nnnn][drive:] pathname1[drive:]pathname2
```

For binary comparisons:

```
fc [/b] [/nnnn] [drive:]pathname1[drive:]pathname2
```

Where pathname1 is the first file that you want to compare, and pathname2 is the second file that you want to compare.

### Comments

The fc command accepts the following switches:

- */a* Shows the output of an ASCII comparison. Instead of displaying all the lines that are different, fc displays only the lines that begin and end each set of differences.
- */b* Forces a binary comparison of both files. Fc compares the two files byte by byte, with no attempt to resynchronize after a mismatch. The mismatches are printed as follows:
  - `xxxxxxxx: yy zz`
  - where xxxxxxxx is the relative address from the beginning of the file of the pair of bytes. Addresses start at 00000000; yy and zz are the mismatched bytes from pathname1 and pathname2. The */b* switch is the default when you compare *.exe*, *.com*, *.sys*, *.obj*, *.lib*, or *.bin* files.
- */c* Causes the matching process to ignore the case of letters. Fc then considers all letters in the files as uppercase letters.
- */L* Compares the files in ASCII mode. This switch is the default when you compare files that do not have extensions of *.exe*, *.com*, *.sys*, *.obj*, *.lib*, or *.bin*.
- */LB* Sets the internal line buffer to *n* lines. The default length is 100 lines. Files that have more than this number of consecutive, differing lines will abort the comparison.
- */n* Displays the line numbers of an ASCII compare.
- */t* Does not expand tabs to spaces. The default is to treat tabs as spaces to eight-column positions.
- */w* Causes fc to compress white space (tabs and spaces) during the comparison.
- */nnnn* Specifies the number of lines that must match after fc finds a difference between files.

### Example

To compare two text files, called *report.jan* and *report.feb*, type:

```
fc /a report.jan report.feb
```

## Fdisk

Fdisk configures a hard disk for use with DOS.

### Syntax

```
fdisk
```

### Comments
