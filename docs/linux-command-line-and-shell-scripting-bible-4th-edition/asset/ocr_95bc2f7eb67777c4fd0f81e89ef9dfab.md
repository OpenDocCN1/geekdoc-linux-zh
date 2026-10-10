```
$
```

Notice that the `-i` command parameter prompts you to make sure that you're serious about removing the file. The shell has no recycle bin or trashcan. After you remove a file, it's gone forever. Therefore, a good habit is to always tack on the `-i` parameter to the `rm` command. You can also use wildcard metacharacters to remove groups of files. However, again, use that `-i` option to protect yourself:

```
```
$ rm -i f?ll
rm: remove regular empty file 'fell'? y
rm: remove regular empty file 'fill'? y
rm: remove regular empty file 'full'? y
$ ls f?ll
ls: cannot access 'f?ll': No such file or directory
$ ```
```

One other feature of the `rm` command, if you're removing lots of files and don't want to be bothered with the prompt, is to use the `-f` parameter to force the removal. Just be careful!

# # Managing Directories

Linux has a few commands that work for both files and directories (such as the `cp` command) and some that work only for directories. To create a new directory, you need to use a specific command, which is covered in this section. Removing directories can get interesting, so that is covered in this section as well.

# ## Creating directories

Creating a new directory in Linux is easy — just use the `mkdir` command:

```
```
$ mkdir New_Dir
$ ls -ld New_Dir
drwxrwxr-x. 2 christine christine 6 Mar 6 14:40 New_Dir
$ ```
```

The system creates a new directory named `New_Dir` . Notice in the new directory's long listing that the directory's record begins with a d . This indicates that `New_Dir` is a directory.