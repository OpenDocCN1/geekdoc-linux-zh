```
drwx------  2 sarwar  512 Jul  22 13:21 current
drwx------  2 sarwar  512 Jul  22 13:21 final
-rw-------  1 sarwar 2064896 Jul  22 13:47 unixbook.tar
$ file unixbook.tar
unixbook.tar:          USTAR tar archive
$
```

You can also create the tar archive of the current directory by using the following command. The - argument informs tar that the archive is to be sent to standard output, which is redirected to the unixbook.tar file. As we discussed in Chapter 12, the back quotes (grave accents) are used for command substitution—that is, to execute the find command and substitute its output for the command, including the back quotes. The output of the find . -print command (the names of all the files and directories in the current directory) are passed to the tar command as its parameters. These file and directory names are taken as the list of files to be archived by the tar command. Thus, the net effect of the command line is that a tar archive of the current directory is created in unixbook.tar.

```
$ tar cvf - 'find . -print' > unixbook.tar
$
```

In the following in-chapter exercise, you will use the tar command with the c option to create an archive of a directory.

# EXERCISE 23.13

Create a tar archive of a subdirectory hierarchy of your choosing under your own home directory on your UNIX system. What command line(s) did you use? What is the name of your archive file?

# 23.6.2.3 Restoring Archived Files

You can restore (unpack) an archive by using the function option x of the tar command. To restore the archive created in Section 23.6.2.2 and place it in a directory called ~/backups, you can run the following command sequence. The cp command copies the archive file, assumed to be in your home directory, to the directory ~/backups where the archived files are to be restored. The cd command is used to make the destination directory the current directory. Finally, the tar command is used to do the restoration. Notice that the destination directory is the current directory.

```
$ cp unixbook.tar ~/backups
$ cd ~/backups
$ tar xvf unixbook.tar
x . , 0 bytes, 0 tape blocks
```