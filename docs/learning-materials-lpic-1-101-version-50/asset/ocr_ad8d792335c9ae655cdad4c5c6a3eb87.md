This command can be literally interpreted as copy `file1` into directory `dir2`. The result is the presence of `file1` inside `dir2`. For this command to be executed successfully `file1` should be existent in the user’s current directory. Otherwise, the system reports an error with the message No such file or directory.

```
```
$ cp dir1/file1 dir2
```
```

In this case, observe that the path to `file1` is more explicit. The source path can be expressed either as a relative or absolute path. Relative paths are given in reference to a specific directory, while absolute paths are not given with a reference. Below we shall further clarify this notion.

For the moment, just observe that this command copies `file1` into the directory `dir2`. The path to `file1` is given with more detail since the user is currently not located in `dir1`.

```
```
$ cp /home/frank/Documents/file2 /home/frank/Documents/Backup
```
```

In this third case, `file2` located at `/home/frank/Documents` is copied into the directory `/home/frank/Documents/Backup`. The source path provided here is absolute. In the two examples above, the source paths are relative. When a path starts with the character / it is an absolute path, otherwise it is a relative path.

The general syntax for cp is:

```
```
cp OPTIONS SOURCE DESTINATION
```
```

SOURCE is the file to copy and DESTINATION the directory into which the file would be copied. SOURCE and DESTINATION can be specified either as absolute or relative paths.

# Moving Files with mv

Just like cp for copying, Linux provides a command for moving and renaming files. It is called mv.

The move operation is analogue to the cut and paste operation you generally perform through a Graphical User Interface (GUI).

If you wish to move a file into a new location, use mv in the following way:

```
```
mv FILENAME DESTINATION_DIRECTORY
```
```