# EXPLANATION

Shows how each line of file1 and file2 differs. The first file is represented by the < symbol, and the second file by the > symbol. Each line is preceded by an ed command indicating the editing command that would be used to make the files the same.

# dos, xdos, dosexec, dosdebug—a Linux DOS emulator that runs MS-DOS and MS-DOS programs under Linux

(See Linux man page for a complete description. It's long ...)

# df—summarizes free disk space

```
df [-aikPv] [-t fstype] [-x fstype] [--all][--inodes][--type=fstype]
[--exclude-type=fstype][--kilobytes] [--portability] [--print-type]
[--help] [--version] [filename...]
```

The df command shows information about the filesystem on which each file resides, or all filesystems by default.

# EXAMPLE A.21

```
df
Filesystem      1024-blocks Used Available Capacity Mounted on
/dev/hda5       1787160 1115587 579141 66% /
```

# du—summarizes disk usage

```
du [-arskod] [name ...]
```

The du command reports the number of 512-byte blocks contained in all files and (recursively) directories within each directory and file specified.

# EXAMPLE A.22

```
1  du -s /desktop
2  du -a
```

# EXPLANATION

+   1. Displays a summary of the block usage for all the files in /desktop and its subdirectories.
+   2. Displays block usage for each file in this directory and subdirectories.