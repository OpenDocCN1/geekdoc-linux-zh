# Chapter 7

Here the \-S option prints out the default file mask in rw\_ form. This mask allows owners to read, write, and execute files; it allows the group and others read and write permissions, but no execute permissions.

Now, let's modify the file mask:

```
$ umask u=rwx,g=r,o=r
$ umask \-S
u=rwx,g=r,o=r
```

We do this using the umask command supplying the desired file mask. Our new mask allows the owner read, write, and execute, while the group and others have just read permissions. A newly created file reflects the current file mask:

```
$ mkdir widgets
$ ls \-ld widgets
drwxr\-r\-\-  2 deepakt users    4096 Jan 20 01:05 widgets
$ cd widgets
$ touch foowidget
$ ls \-al
total 8
drwxr\-r\-\-  2 deepakt users    4096 Jan 20 01:05 widgets
drwx\-\-\-\-\-\-\- 13 deepakt users    4096 Jan 20 01:05 .
\-rw\-r\-r\-\-  1 deepakt users      0 Jan 20 01:05 foowidget
```

Here we should notice that (as intended) the foowidget file has just read permissions for the group and others: However, you may note that while the file mask reads u=rwx, g=r, o=r, the owner of this file does *not* have execute permissions! This is because foowidget is interpreted by the shell as a text file, and execute permission does not make sense for text files in general. Shell scripts or other text files of scripting languages such as Perl are therefore treated as text files but need to be manually assigned execute permissions for them to run. (If we were to compile a program to create an executable, we would notice that execute permission for the owner is enabled. Execute permissions are also enabled by default for the owner when creating a directory since the execute permissions for a directory is necessary to allow users to execute the cd command to enter the directory.)

Now, let's modify the files permissions again:

```
$ chmod u=rwx,g=rw,o=rw foowidget
$ ls \-al foowidget
\-rwxrw\-rw\-  1 deepakt users    0 Jan 20 01:05 foowidget
```

This command modifies the permissions of the foowidget file such that the group and others are now allowed to both read and write the file and the owner is allowed to read, write, and execute it. The file list confirms that the permissions have indeed changed.

Now, let's switch to the root user and change the ownership of the file: