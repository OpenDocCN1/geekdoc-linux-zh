If you are moving a large number of files, you might want to use the `-v` option. This causes the name of each file to be displayed before it is moved. Because metacharacters can give you big problems, you should consider using the `-v` or `-i` options to specify which files are to be moved.

A powerful option is `-f`, which will force the move/copy operation no matter what. Use this only when you are sure you know that you will not lose anything you want to keep; you will not be prompted no matter what file is overwritten.

The `mv` command also can be used to move directories. If the target directory does not exist, the directory is renamed. However, if the target directory does exist, the source directory will be moved to be a subdirectory of the existing directory.

# rm

The `rm` command can be used to remove individual or multiple files and directories. After a file has been deleted, it is gone, so use it cautiously.

Use the `-i` option to require confirmation before files are deleted. The `-i` option is an excellent safety feature when using metacharacters with `rm`, especially if working as the superuser. Otherwise, you might be left with a nonbootable system. The `-f` option will force deletion of write-protected files.

The `-r` option will recursively delete files and directories. You will be asked to confirm each deletion. To recursively delete files and directories without confirmation use `-fr`. You cannot use `rm` to delete directories, even empty ones, without the `-r` option.

You must have write permission to the directory containing the file you want to delete, but you do not need to have permission to the file you want to delete. If you do not have permission to the file you are trying to delete, you will be prompted to confirm the deletion.

# mkdir

The `mkdir` command is used to create one or more directories. If no options are used, the parent directory must exist to create a child directory, as in the following examples

```
```
mkdir testing
mkdir testing/child
```
```

It also can create the parent and child directories in a single command by using the `-p` option.

```
```
mkdir -p testing/parent/child
```
```