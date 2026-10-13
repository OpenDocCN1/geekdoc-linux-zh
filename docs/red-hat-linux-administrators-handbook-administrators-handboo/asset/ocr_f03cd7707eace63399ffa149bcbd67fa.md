The output that locate produces will contain the keyword “foo” in the absolute path or will not have any output at all.

# ls

Syntax:

```
ls [-laRl] file or directory
```

The ls command allows you to list files (and subdirectories) in a directory. It is one of the most commonly used programs. When used with the -l option, the ls command displays only the file and directory names in the current directory. When the -l option is used, a long listing containing file/directory permission information, size, modification date, and so on is displayed. Using the -a option enables you to view all files and directories (including the ones that have a leading period in their names) within the current directory. The -R option allows the command to recursively display contents of the subdirectories (if any).

# mkdir

Syntax:

```
mkdir directory . . .
```

To make a directory, use the mkdir command. Only two restrictions apply when choosing a directory name: filenames can be up to 255 characters long; and directory names can contain any character except /.

The following example creates three directories, all in the current directory, provided write permission is granted in the current directory:

```
mkdir dir1 dir2 dir3
```

# mv

Syntax:

```
mv [-if]sourcefile targetfile
```