This command creates a new file called neighbor-copy that is identical to my-copy in every respect except for its name, owner, group, and timestamp—the new file has a timestamp that shows the time when it was copied. The file my-copy is not altered.

Use the -v ("verbose") option to list files as they are copied. This is useful for large copies, where a lot of files are being copied, so you can monitor the progress.

⇒ To copy all the files in the ~/workgroup/final directory to the ~/workgroup/backup directory, specifying verbose output so each file is listed as it is copied, type:

```
$ cp -v ~/workgroup/final/* ~/workgroup/backup [RET]
```

# 5.4.1 Copying Files with Their Attributes

When you copy a file, the attributes such as timestamp and file ownership will differ between the original and the copy. Use cp with the -p option to preserve all of the attributes of the original, whenever possible, including its timestamp, owner, group, and permissions.

⇒ To copy the file my-copy to the file neighbor-copy, preserving all of the attributes of the source file in the target file, type:

```
$ cp -p my-copy neighbor-copy [RET]
```

This command copies the file my-copy to a new file called neighbor-copy that is identical to my-copy in every respect except for its name.

While -p does not copy any subdirectories a directory may contain, you can use the -a ("archive") option instead, which preserves attributes whenever possible but also copies any subdirectories as well as symbolic links (see Recipe 5.7 [Giving a File More than One Name], page 152). This is good for making archival backups of one directory tree to another.

⇒ To make an archival copy of the contents of /cdrom to the current directory, type:

```
$ cp -a /cdrom . [RET]
```

This command makes a copy of /cdrom, including any subdirectories it may contain, to the current directory. Original file attributes are preserved in the copy.

NOTES: A snapshot is a copy of a directory tree that shows what it looked like at a particular time. Snapshots are usually made in software development projects upon each release—to "take a snapshot of the current version" means to make an archival copy of the directory tree containing the sources.