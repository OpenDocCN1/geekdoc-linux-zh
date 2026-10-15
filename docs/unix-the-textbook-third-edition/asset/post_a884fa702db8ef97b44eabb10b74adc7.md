
![](img/02e070097d401d3bf7de4bf1c470b267_1143_0.png)

## FIGURE 23.15 Directory structure.

In the examples presented in this chapter, we use the directory structure shown in Figure 23.15. The following session shows that there are two directories under the unixbook directory called current and final. In addition, each of these directories contains six files (see Figure 23.15), displayed by the ls -l command.

```
$ cd unixbook
$ pwd
/users/sarwar/unixbook
$ ls -l
drwx------ 2 sarwar 512 Jul 22 13:21 current
drwx------ 2 sarwar 512 Jul 22 13:21 final
$ cd current
$ ls -l
-rw------- 1 sarwar 204288 Jul 19 13:06 ch07.doc
-rw------- 1 sarwar 87552 Jul 19 13:06 ch08.doc
-rw------- 1 sarwar 86016 Jul 19 13:06 ch09.doc
-rw------- 1 sarwar 121344 Jul 19 13:06 ch10.doc
-rw------- 1 sarwar 152576 Jul 19 13:06 ch11.doc
-rw------- 1 sarwar 347648 Jul 19 13:06 ch12.doc
$ cd ..
$ cd final
$ ls -l
-rw------- 1 sarwar 41984 Jul 19 13:06 ch1.doc
-rw------- 1 sarwar 54272 Jul 19 13:06 ch2.doc
-rw------- 1 sarwar 142848 Jul 19 13:06 ch3.doc
-rw------- 1 sarwar 86528 Jul 19 13:06 ch4.doc
-rw------- 1 sarwar 396288 Jul 19 13:06 ch5.doc
-rw------- 1 sarwar 334848 Jul 19 13:06 ch6.doc
$
```

If you want to create an archive of the unixbook directory on a tape drive /dev/rmt/t0 (the name might be different on your system), you can use the following command after changing the directory to unixbook. The v (verbose) option is used to view the files and directories that are being archived. Unless you are the system administrator, in all likelihood you do not have access permission to use (read or write) the tape drive. Thus, the shell will give you the following error message:

```
$ tar cvf /dev/rmt/t0 .
tar: /dev/rmt/t0: Permission denied
$
```

However, if you do have proper access permissions for the tape drive, an archive of the unixbook directory is created on the tape. Not only do you need access privileges to /dev/rmt/t0, but you also need to mount it first.

However, you can also create an archive on a disk file—in a directory that you have the write permission for—by using the following command. Here we made ~/unixbook our current directory and created a tar archive of this directory in a file called unixbook.tar. Note that .tar is not an extension required by the tar utility. We have used this extension because it allows us to identify tar archives by looking at the file name. With no such extension, we have to use the file command to identify our tar archive files, as shown in the last command line in the session (in case you need reminding what the file command does).

```
$ cd ~/unixbook
$ tar cvf unixbook.tar .
tar: ./unixbook.tar same as archive file
a ./final/0K
a ./final/ch1.doc 41K
a ./final/ch2.doc 53K
a ./final/ch3.doc 140K
a ./final/ch4.doc 85K
a ./final/ch5.doc 387K
a ./final/ch6.doc 327K
a ./current/0K
a ./current/ch07.doc 200K
a ./current/ch08.doc 86K
a ./current/ch09.doc 84K
a ./current/ch10.doc 119K
a ./current/ch11.doc 149K
a ./current/ch12.doc 340K
$ ls -l
drwx------  2 sarwar  512 Jul 22 13:21 current
drwx------  2 sarwar  512 Jul 22 13:21 final
-rw-------  1 sarwar 2064896 Jul 22 13:47 unixbook.tar
$ file unixbook.tar
unixbook.tar:          USTAR tar archive
$
```

You can also create the tar archive of the current directory by using the following command. The - argument informs tar that the archive is to be sent to standard output, which is redirected to the unixbook.tar file. As we discussed in Chapter 12, the back quotes (grave accents) are used for command substitution—that is, to execute the find command and substitute its output for the command, including the back quotes. The output of the find . -print command (the names of all the files and directories in the current directory) are passed to the tar command as its parameters. These file and directory names are taken as the list of files to be archived by the tar command. Thus, the net effect of the command line is that a tar archive of the current directory is created in unixbook.tar.

```
$ tar cvf - `find . -print` > unixbook.tar
$
```

In the following in-chapter exercise, you will use the tar command with the c option to create an archive of a directory.

## EXERCISE 23.13

Create a tar archive of a subdirectory hierarchy of your choosing under your own home directory on your UNIX system. What command line(s) did you use? What is the name of your archive file?

### 23.6.2.3 Restoring Archived Files

You can restore (unpack) an archive by using the function option x of the tar command. To restore the archive created in Section 23.6.2.2 and place it in a directory called ~/backups, you can run the following command sequence. The cp command copies the archive file, assumed to be in your home directory, to the directory ~/backups where the archived files are to be restored. The cd command is used to make the destination directory the current directory. Finally, the tar command is used to do the restoration. Notice that the destination directory is the current directory.

```
$ cp unixbook.tar ~/backups
$ cd ~/backups
$ tar xvf unixbook.tar
x . , 0 bytes, 0 tape blocks
```
