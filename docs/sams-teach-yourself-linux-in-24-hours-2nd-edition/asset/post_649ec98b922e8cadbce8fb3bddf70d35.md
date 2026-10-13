
Now, copy a file onto another file, and then check the file sizes and the contents of the new file, as follows:

```
# cp file1 file2
# ls -l file*
-rw-r--r-- 1 bball users 14 Jan 5 13:29 file1
-rw-r--r-- 1 bball users 14 Jan 5 13:31 file2
-rw-r--r-- 1 bball users 23 Jan 5 13:29 file3
# cat file2
this is file1
```

It should be obvious that file1 replaces file2. To avoid this problem (unless you really want to overwrite the file), you can use the -b or -i options, which work like mv. Here's an example:

```
# cp -i file1 file2
cp: overwrite 'file2'? n
# cp -bi file1 file2
cp: overwrite 'file2'? y
# ls file*
file1 file2 file2- file3
```

Note that file2, which is overwritten, is backed up.

The cp command can also copy a number of files at one time. The following example shows how to copy all the files in directory tempdir1 to directory tempdir2:

```
# cp tempdir1/* tempdir2
# tree tempdir2
tempdir2
|-- tempfile1
|-- tempfile2
|-- tempfile3

0 directories, 3 files
```

Like the rm command, cp also has an -r, or recursive, option. You can use this option to copy one directory into another. For example, to copy the tempdir1 directory and its files into tempdir2, use this syntax:

```
# cp -r tempdir1 tempdir2
# tree tempdir2
tempdir2
|-- tempfile1
|-- tempfile2
|-- tempfile3
|-- tempdir1
    |-- tempfile1
    |-- tempfile2
    |-- tempfile3

1 directory, 6 files
```

Finally, the cp command has the -p option, which is similar to mkdir's -p option. Normally, when you copy a file inside several directories into another directory, only the file is copied. The following example only copies tempfile1 into tempdir3:

```
# tree tempdir2
tempdir2
|-- tempfile1
|-- tempfile2
|-- tempfile3
|-- tempdir1
    |-- tempfile1
    |-- tempfile2
    |-- tempfile3
1 directory, 6 files
# cp tempdir2/tempdir1/tempfile1 tempdir3
```

However, what if you want to copy a file along with its directory structure? To do this, you can use the -P option:

```
# cp -P tempdir2/tempdir1/tempfile1 tempdir3
# tree tempdir3
tempdir3
|-- tempdir2
    |-- tempdir1
        |-- tempfile1
2 directories, 1 file
```

Not only does cp copy the single file, but it has also created the subdirectory structure.

## Creating Hard and Symbolic Links with the ln Command

Linux supports both hard and symbolic links. Although it is not important that you understand how links in Linux work, you need to understand the difference between these two types of links, and how to use links while you use Linux. To create hard or symbolic links, use the ln, or link, command.

**New Term** The ln command creates both types of links and links files with other files (including directories, which under OpenLinux are simply files, too). The important difference is that hard links directly link two files on only the same file system. On the other hand, you can use a symbolic link between directories or files that span different file systems. Hard links also have other advantages. If you use the ln command to create a hard link, you specify a second file on the command line you can use to reference the original file, as in the following example:

```
# cat > file1
This is file1
# ln file1 file2
# ls -l file*
-rw-r--r-- 2 bball users 14 Jan 5 13:32 file1
-rw-r--r-- 2 bball users 14 Jan 5 13:32 file2

# cat file2
This is file1
```

You can see that file2 is exactly the same as file1. If you delete file1, file2 remains. If you make changes to file1, such as adding text, these changes appear in file2, and if you make changes to file2, file1 is also updated. Although you can see two files, each 14 characters in size, only 14 characters of hard drive space are used for the original file (okay, technically more than that, but it depends on the block size of the partition or type of hard drive).

On the other hand, although symbolic links are useful, they have a drawback. The next examples show you why. First, to create a symbolic link, use the ln command's -s option:

```
# cat >file1
This is file1
# ln -s file1 file2
# ls -l file*
-rw-r--r-- 1 bball users 14 Jan 5 13:48 file1
lrwxrwxrwx 1 bball users 5 Jan 5 13:48 file2 -> file1
```

Note the arrow pointing from file2 to file1. This tells you that file2 is a symbolic link to file1. Also note that file2 is smaller in length than file1. Symbolic links are different from hard links in that a symbolic link is merely an alias for the original file. Nothing happens to the original file if you delete the symbolic link. However, if you delete the original file, your symbolic link can't help you at all:

```
# rm -f file1
# cat file2
cat: file2: No such file or directory
```

Because the original file, file1, no longer exists, you can't access its contents through the symbolic link, file2. However, symbolic links do have an advantage over hard links. You can use a symbolic link to point to a directory on your OpenLinux file system or even another file system. In the following example, if you try to create a hard link to the /usr/local/games directory, the ln command complains and quits:

```
# ln /usr/local/games play
ln: /usr/local/games: hard link not allowed for directory
```

But you can use a symbolic link, as follows:

```
# ln -s /usr/local/games play
```

```
# ls -l play
lrwxrwxrwx 1 bball users 16 Jan 5 14:12 play -> /usr/local/games
```

Now, instead of typing a long command like

```
# cd /usr/local/games
```

you can use

```
# cd play
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_125_0.png)

> Symbolic links to other directories on other file systems, such as a DOS or Windows partition, can be handy. For example, having a directory called dos in your home directory that is linked to /mnt/dos/windows/desktop makes copying or moving files to and from Linux and Windows a lot easier. For example, if you want to have a linked directory named dos in your home directory and your DOS file system is mounted under the /mnt/dos directory, first make sure that the DOS file system is mounted, and then use the ln command to create a symbolic link, like so:
> 
> # ln -s /mnt/dos/windows/desktop dos
> 
> See Hour 22 for details about mounting other file systems.

So far, you've learned about using the command line. If you're familiar with more graphical interfaces for manipulating files, you'll like the next program, mc.

## Handling Files with the Midnight Commander Program

The mc program, called Midnight Commander, is a graphical interface for handling files (see Figure 5.1). It is a visual shell (you'll learn more about shells in the next hour, "Using the Shell"). To start mc, type the following at the command line:

```
# mc
```

This section does not cover all the details of the mc program. Here are the highlights of its features:

- Provides a visual interface to two directories at a time
- Enables directory browsing with mouse clicks
- Enables menu-driven file operations with dialog boxes, mouse, keyboard and function key support
- Has an open command line to your shell
- Runs commands through mouse clicks
- Has extensive, built-in hypertext help screens
- Emulates and supports the ls, cp, ln, mv, mkdir, rmdir, rm, cd, pwd, find, chown, chgrp, and tree commands
- Compares directory contents
- Uses customized menus so you can build your own commands
- Can use network links for telnet or FTP operations (see Hour 13)
- Offers mouse-click decompression of files (see the section “Compressing Files with the gzip Command” later this hour)
- Can undelete files if your Linux file system is configured to support this capability

Midnight Commander is a handy and convenient tool to use for file handling and directory navigation. You have to invest some time learning how to use this program, but if you've used similar file-management interfaces, you'll feel right at home.

FIGURE 5.1
The Midnight Commander visual shell displays a graphical interface to Linux file commands.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_126_0.png)

## Searching Files

This section introduces you to the use of sophisticated wildcards, or regular expressions, along with short examples of file searches using the grep family of programs. If you understand and use these expressions, you can create refined search techniques you can use again and again. You'll save time and effort during your work, and your learning investment will pay big dividends throughout your Linux experience.
