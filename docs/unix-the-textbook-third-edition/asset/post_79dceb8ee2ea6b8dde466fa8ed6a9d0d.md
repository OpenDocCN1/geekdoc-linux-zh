
![](img/02e070097d401d3bf7de4bf1c470b267_260_0.png)

FIGURE 6.2 Current directory before and after the cp -r ~/courses ~/backups command.

operation is equivalent to creating a hard link (see Chapter 8) to the file, followed by removing/deleting (see Section 6.3.3) the original file. If the source and destination files are on different file systems, the move operation results in a physical copy of the source file to the destination, followed by removal of the source file. The command for moving files is mv. The following is a brief description of the command.

```
SYNTAX
mv [options] file1 file2
mv [options] file-list directory

Purpose: First syntax: Move file1 to file2 or rename file1 to file2
Second syntax: Move all the files in file-list to directory

Commonly used options/features:
- -f Force move regardless of the permissions of the destination file
- -i Prompt the user before overwriting the destination file
```

You must have the write and execute access permissions for the directory that contains the source file (file1 in the description), but you do not need to have the read, write, or execute permissions for the file itself. Similarly, you must have the write and execute permissions for the directory that contains the target/destination file (file2 in the description), execute permission for every directory in the pathname for the destination file, and write permission for the destination file if it already exists. If the destination file exists, by default, it is overwritten without informing you. If you use the -i option, you are prompted before the destination file is overwritten.

The following command moves temp to temp.moved. In this case, the temp file is renamed temp.moved. The mv command returns an error message if temp does not exist, or if you do not have the execute permission for the directory it is in. The command

prompts you for moving the file if temp.moved already exists, but you do not have write permission for it.

```
$ mv temp temp.moved
$
```

The following command moves temp to the backups directory as the temp.old file. Figure 6.3 shows the state of your current directory before and after the temp file is moved.

```
$ mv temp backups/temp.old
$
```

The following command is a sure move; you can use it to force the move, regardless of the permissions for the target file, temp.moved.

```
$ mv -f temp temp.moved
$
```

The following command moves all the files and directories (excluding hidden files) in dir1 to the dir2 directory. The command fails, and an error message appears on your screen, if dir2 is not a directory, if it does not exist, or if you do not have the write and execute permissions for it.

```
$ mv dir1/* dir2
$
```

After the command is executed, dir1 contains the hidden files only. You can use the ls -a command to confirm the status of dir1.

![](img/02e070097d401d3bf7de4bf1c470b267_261_0.png)

FIGURE 6.3 Current directory before and after the mv temp backups/temp.old command.

## 6.3.3 Removing/Deleting Files

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
