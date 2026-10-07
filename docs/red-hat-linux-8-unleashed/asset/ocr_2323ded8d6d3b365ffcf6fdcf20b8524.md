To use the recovery filesystem, you must cd in one of the panels to the special filename formed by combining the prefix #undel: with the partition name where your deleted file resides. For example, to attempt to recover a deleted file on /dev/hda1, do this:

```
# cd #undel:/hda1
```

Be patient because it will take a while for the deleted files to be displayed. You will see a list of nodes that you can examine with the text editor (using the F4 key); then use the F12 key to perform a Save As operation, renaming the file to something appropriate for your use. Repeat this process until you have named and saved all the files. Press the F10 key to exit when done. Note that you might be able to recover only pieces of files and might not be able to recover any at all.

# NOTE

If you need to know what is on a drive or disk that can be easily mounted (it could be a non-Linux format, or contain un-formatted, raw data), use

```
# dd if=/dev/hda1 count=1 bs=512 | -
```

which produces output similar to the following:

```
1+0 records in
1+0 records out
```

```
standard input: x86 boot sector, system MSWIN4.1, FAT (16 bit)
```

To discover what an unknown floppy disk is, use this

```
# dd if=/dev/fd0 count=1 bs=512 | -
```

which produces output similar to the following:

```
1+0 records in
1+0 records out
```

```
standard input: x86 boot sector, system )_3oEIHC, FAT (12 bit)
```

# System Rescue

There will come a time when you need to engage in system rescue efforts. This arises when the system will not start Linux so you can recover any files. This is frequently a problem with the bootloader program or partition table (discussed in Chapter 8), but it could be critical system files have been inadvertently deleted or corrupted. If you have been making backups properly, these kinds of system failures are easily, though not quickly, recoverable through a full restore. Some, valuable current data might not have been backed up since the last scheduled backup, and the backup archives are found to be corrupt, incomplete, or missing. If the problem causing the system failure is simply a