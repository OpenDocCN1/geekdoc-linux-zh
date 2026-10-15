# 6.3.3 Removing/Deleting Files

When files are not needed anymore, they should be removed from a file structure to free up disk space to be reused for new files and directories. The UNIX command for removing (deleting) files is rm. The following is a brief description of the command.

SYNTAX
rm [options] file-list

Purpose: Removes the files in file-list from the file structure (and disk)
Commonly used options/features:
- f Force remove regardless of the permissions for file-list
- i Prompt the user before removing the files in file-list
- r Recursively remove the files in the directory, which is passed as an argument. This removes everything under the directory, so be sure you want to do so before using this option.

If files in file-list are pathnames, you need the read and execute permissions for all the directory components in the pathnames and the read, write, and execute permissions for the last directory (that contains the file or files to be deleted). You must also have write permission for the files themselves for their removal without prompting you. If you run the command from a terminal and do not have write permission for the file to be removed, the command displays your access permissions for the file and prompts you for your permission to remove it.

The following command lines illustrate use of the rm command to remove one or more files from various directories.

```
$ rm temp
$ rm temp backups/temp.old
$ rm -f phones grades ~/letters/letter.john
$ rm ~/dir1/*
$
```

The first command removes temp from your current directory. The second command removes the temp file from your current directory and the temp.old file from the backups directory in your current directory. Figure 6.4 shows the semantics of this command. The third command removes the phones, grades, and ~/letters/letter.john files, regardless of their access permissions. The fourth command removes all the files from the ~/dir1 directory; the directories are not removed.

Now, consider the following commands that use some shell metacharacter features (see Chapter 7).

```
$ rm [kK]*.prn
$ rm [a-kA-Z]*.prn
$
```