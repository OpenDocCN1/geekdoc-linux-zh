# 6.3.4 Determining File Size

You can determine the size of a file by using one of several UNIX commands. The two commands commonly used for this purpose that are available in all UNIX versions are ls -l and wc. We described the ls -l command in Chapter 5, where we use it to determine the access permissions for files. We revisit this command here in the context of determining file size.

As we mentioned before, the ls -l command displays a long list of the files and directories in the directory (or directories) specified as its argument. You must have the read and execute permissions for a directory to be able to run the ls command on it successfully; no permissions are needed on the files in the directory to be able to see the list. The command gives output for the current directory if none is specified as an argument. The output of this command has nine fields, and the fifth field gives file sizes in bytes (see Section 5.5). In the following command, the size of the lab2 file is 709 bytes.

```
$ ls -l lab2
-rw-r--r-- 1 sarwar faculty 709 Apr 5 11:23 lab2
$
```

This command also displays the size of directory files. You can also use it to get the sizes of multiple files by specifying them in the command line and separating them by spaces. For example, the following command shows that sizes of the lab1 and lab2 files are 163 bytes and 709 bytes, respectively.

```
$ ls -l lab1 lab2
-rw-r--r-- 1 sarwar faculty 163 Jul 9 16:47 lab1
-rw-r--r-- 1 sarwar faculty 709 Apr 5 11:23 lab2
$
```

The following command uses the shell metacharacter * to display the long listings for all the files in the ~/courses/ee446 directory.

```
$ ls -l ~/courses/ee446/*
... output of the command ...
$
```

Whereas ls -l is a general-purpose command that can be used to determine many of the attributes of one or more files, including their sizes in bytes/characters, wc is a special purpose command that displays only file sizes. The following is a brief description of the wc command.

# SYNTAX

```
wc [options] file-list
```

Purpose: Display sizes of the files in file-list as number of lines, words, and characters

Commonly used options/features:

+   - -c Display only the number of characters
+   - -l Display only the number of lines
+   - -w Display only the number of words