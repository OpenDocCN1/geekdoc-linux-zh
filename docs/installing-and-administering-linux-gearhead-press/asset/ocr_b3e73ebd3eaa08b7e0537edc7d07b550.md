confining his inquiry to the *test1* file only by specifying its filename as an argument to the `ls` command:

```
$ ls -li test1<Enter>
187018 -rw-rw-r-- 1 quixoted knighte01 257 Mar 17 13:29 test1
```

Although typically, ordinary users are not usually interested in inode numbers, the functions of various file manipulation commands (such as *mv* and *cp*) are better understood if inode tables and the information in them are understood first.

# Displaying Directory Information: The `ls` and `stat` Commands

The `ls` (list) and `stat` (statistics) commands can be used to display information about files and directories, because Linux treats directories as files for these purposes. In Example 4.11, the `ls` command displays inode table information. As shown in the example, the options `-l`, `-d`, and `-i` result in a long listing with inode information and the inode number in the first displayed field.

# Example 4.11 Listing Directory Contents with `ls`

To get a long listing with inode information and the inode number in the first displayed field, Don Quixote enters

```
$ ls -ldi expired<Enter>
109096 drwxr-xr-x 5 quixoted knights01 4096 May 18 15:22 expired
```

Linux systems maintain three timestamps for files and directories. The following are additional options you can use with `ls` to display each of these timestamps:

+   ■ `ls -lu` displays the access time.
+   ■ `ls -l` displays the modification time.
+   ■ `ls -lc` displays the updated time.

The `stat` command displays inode information for a specified file or directory. The syntax is as follows:

```
$ stat directoryname<Enter>
```

To explain the results of the command, let’s provide an example.