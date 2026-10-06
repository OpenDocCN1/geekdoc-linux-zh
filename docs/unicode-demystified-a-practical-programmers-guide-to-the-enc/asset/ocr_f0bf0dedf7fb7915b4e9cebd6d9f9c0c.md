# cp

Copies one or more files

```
cp [options] source-file destination-file
cp [options] source-file-list destination-directory
```

The cp utility copies one or more files and has two modes of operation. The first copies one each of the files to another; the second copies one or more files to a directory. The cp utility copies directories only with the -r or -R options.

# Arguments

The source-file is the pathname of the file that cp is going to copy. The destination-file is the pathname that cp assigns to the resulting copy of the file.

The source-file-list is one or more pathnames of files that cp is going to copy. The destination-directory is the pathname of the directory in which cp places the copied files.

When you specify a destination-directory, cp gives each of the copied files the same filename as its source-file. For example, when you copy /home/jenny/memo.416 to the /home/jenny/archives directory, the copy has simple filename memo.416, but the new pathname is /home/jenny/archives/memo.416.

When you use the -r option, the source-file or source-file-list can contain directories.

# Options

+   -backup -b If copying a file would overwrite an existing file, this option makes a backup copy of the file that would be overwritten. The cp utility gives the backup copy the same name as the destination file but with a tilde (~) appended to it.

+   -force -f When the destination-file exists and cannot be opened for writing, cp tries to move it before starting to copy the source-file. This option is useful when the user copying a file does not have write permission to an existing, destination-file but has write permission to the directory containing the destination-file.

+   -interactive -i Prompts the user whenever cp would overwrite an existing file. If you enter anything other than y, cp does not make the copy.

+   -preserve -p Preserves each file's owner, group, permissions, and modification dates when copying it.

+   -recursive -R Recursively copies directories as well as ordinary files.

+   -update -u Copies only when the destination-file does not exist or when it is older than the source-file.

+   -verbose -v Explains what cp is doing.