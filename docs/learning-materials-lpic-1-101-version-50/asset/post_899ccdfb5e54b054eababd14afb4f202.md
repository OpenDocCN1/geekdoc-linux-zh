
## Directories

which contain other files.

## Special files

which are used for input and output.

Of course, other kinds of files exist but are beyond the scope of this lesson. Later, we shall discuss how to identify these different file types.

# Manipulating Files

## Using ls to List Files

The ls command is one of the most important command line tools you should learn in order to navigate the file system.

In its basic form, ls will list file and directory names only:

```
$ ls
Desktop Downloads emp_salary file1 Music Public Videos
Documents emp_name examples.desktop file2 Pictures Templates
```

When used with -1, referred to as “long listing” format, it shows file or directory permissions, owner, size, modified date, time and name:

```
$ ls -l
total 60
drwxr-xr-x 2 frank frank 4096 Apr 1 2018 Desktop
drwxr-xr-x 2 frank frank 4096 Apr 1 2018 Documents
drwxr-xr-x 2 frank frank 4096 Apr 1 2018 Downloads
-rw-r--r-- 1 frank frank 21 Sep 7 12:59 emp_name
-rw-r--r-- 1 frank frank 20 Sep 7 13:03 emp_salary
-rw-r--r-- 1 frank frank 8980 Apr 1 2018 examples.desktop
-rw-r--r-- 1 frank frank 10 Sep 1 2018 file1
-rw-r--r-- 1 frank frank 10 Sep 1 2018 file2
drwxr-xr-x 2 frank frank 4096 Apr 1 2018 Music
drwxr-xr-x 2 frank frank 4096 Apr 1 2018 Pictures
drwxr-xr-x 2 frank frank 4096 Apr 1 2018 Public
drwxr-xr-x 2 frank frank 4096 Apr 1 2018 Templates
drwxr-xr-x 2 frank frank 4096 Apr 1 2018 Videos
```

The first character in the output indicates the file type:

- `-` for a regular file.
- `d` for a directory.
- `c` for a special file.

To show the file sizes in a human readable format add the option `-h`:

```
$ ls -lh
total 60K
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Desktop
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Documents
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Downloads
-rw-r--r-- 1 frank frank 21 Sep 7 12:59 emp_name
-rw-r--r-- 1 frank frank 20 Sep 7 13:03 emp_salary
-rw-r--r-- 1 frank frank 8.8K Apr 1 2018 examples.desktop
-rw-r--r-- 1 frank frank 10 Sep 1 2018 file1
-rw-r--r-- 1 frank frank 10 Sep 1 2018 file2
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Music
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Pictures
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Public
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Templates
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Videos
```

To list all files including hidden files (those starting with .) use the option `-a`:

```
$ ls -a
.                .dbus     file1      .profile
..               Desktop   file2      Public
.bash_history    .dmrc     .gconf     .sudo_as_admin_successful
```

Configuration files such as `.bash_history` which are by default hidden are now visible.

In general, the `ls` command syntax is given by:

```
ls OPTIONS FILE
```

Where OPTIONS are any of the options shown previously (to view all the possible options run man ls), and FILE is the name of the file or directory’s details you wish to list.

**NOTE** When FILE is not specified, the current directory is implied.

## Creating, Copying, Moving and Deleting Files

### Creating files with touch

The touch command is the easiest way to create new, empty files. You can also use it to change the timestamps (i.e., modification time) of existing files and directories. The syntax for using touch is:

```
touch OPTIONS FILE_NAME(S)
```

Without any options, touch would create new files for any file names that are supplied as arguments, provided that files with such names do not already exist. touch can create any number of files simultaneously:

```
$ touch file1 file2 file3
```

This would create three new empty files named file1, file2 and file3.

Several touch options are specifically designed to allow the user to change the timestamps for files. For example, the -a option changes only the access time, while the -m option changes only the modification time. The use of both options together changes the access and also the modification times to the current time:

```
$ touch -am file3
```

### Copying Files with cp

As a Linux user, you will often copy files from one location to another. Whether it is moving a music file from one directory to another or a system file, use cp for all copy tasks:

```
$ cp file1 dir2
```

This command can be literally interpreted as copy `file1` into directory `dir2`. The result is the presence of `file1` inside `dir2`. For this command to be executed successfully `file1` should be existent in the user’s current directory. Otherwise, the system reports an error with the message No such file or directory.

```
$ cp dir1/file1 dir2
```

In this case, observe that the path to `file1` is more explicit. The source path can be expressed either as a relative or absolute path. Relative paths are given in reference to a specific directory, while absolute paths are not given with a reference. Below we shall further clarify this notion.

For the moment, just observe that this command copies `file1` into the directory `dir2`. The path to `file1` is given with more detail since the user is currently not located in `dir1`.

```
$ cp /home/frank/Documents/file2 /home/frank/Documents/Backup
```

In this third case, `file2` located at `/home/frank/Documents` is copied into the directory `/home/frank/Documents/Backup`. The source path provided here is absolute. In the two examples above, the source paths are relative. When a path starts with the character / it is an absolute path, otherwise it is a relative path.

The general syntax for cp is:

```
cp OPTIONS SOURCE DESTINATION
```

SOURCE is the file to copy and DESTINATION the directory into which the file would be copied. SOURCE and DESTINATION can be specified either as absolute or relative paths.

### Moving Files with mv

Just like cp for copying, Linux provides a command for moving and renaming files. It is called mv.

The move operation is analogous to the cut and paste operation you generally perform through a Graphical User Interface (GUI).

If you wish to move a file into a new location, use mv in the following way:

```
mv FILENAME DESTINATION_DIRECTORY
```

Here is an example:

```
$ mv myfile.txt /home/frank/Documents
```

The result is that myfile.txt is moved into destination /home/frank/Documents.

To rename a file, mv is used in the following way:

```
$ mv old_file_name new_file_name
```

This changes the name of the file from old_file_name to new_file_name.

By default, mv would not seek your confirmation (technically said “would not prompt”) if you wish to overwrite (rename) an existing file. However, you can allow the system to prompt, by using the option -i:

```
$ mv -i old_file_name new_file_name
mv: overwrite 'new_file_name'?
```

This command would ask the user’s permission before overwriting old_file_name to new_file_name.

Conversely, using the -f:

```
$ mv -f old_file_name new_file_name
```

would forcefully overwrite the file, without asking any permission.

### Deleting Files with rm

rm is used to delete files. Think of it as an abbreviated form of the word “remove”. Note that the action of removing a file is usually irreversible thus this command should be used with caution.

```
$ rm file1
```

This command would delete file1.

```
$ rm -i file1
```

```
rm: remove regular file 'file1'?
```

This command would request the user for confirmation before deleting `file1`. Remember, we saw the `-i` option when using `mv` above.

```
$ rm -f file1
```

This command forcefully deletes `file1` without seeking your confirmation.

Multiple files can be deleted at the same time:

```
$ rm file1 file2 file3
```

In this example `file1`, `file2` and `file3` are deleted simultaneously.

The syntax for `rm` is generally given by:

```
rm OPTIONS FILE
```

## Creating and Deleting Directories

### Creating Directories with `mkdir`

Creating directories is critical to organizing your files and folders. Files may be grouped together in a logical way by keeping them inside a directory. To create a directory, use `mkdir`:

```
mkdir OPTIONS DIRECTORY_NAME
```

where `DIRECTORY_NAME` is the name of the directory to be created. Any number of directories can be created simultaneously:

```
$ mkdir dir1
```

would create the directory `dir1` in the user's current directory.

```
$ mkdir dir1 dir2 dir3
```
