You'll notice that the first file was identified as compressed data created on a Unix system, and modified Wed May 12 06:20:20 1999. If the file is a text file, the file command tries to determine its computer language as in the second example, where some code written in the C language was correctly identified.

# # The ls Command

The ls command is one of the most often used Linux commands. ls provides information about a file, including its type. The name ls means listing because the command lists all of the files in a directory. The syntax for ls is simple:

```
`ls [options] [file or directory name]`
```

The ls command without arguments produces output like that in Listing 3.2.

# ## 3.2 The Output of the ls Command Entered without Arguments

```
$ ls
sshd sshd.old sshd1 sshd1.old visudo
```

If no arguments are specified, you get a listing of file names, which by default not include any file names that begin with a d. You can use arguments to further define what the listing will include. The -l option which stands for "long listing" allows you to examine the permission string, the owner, the file size, the date it was last modified, and the filename in Listing 3.3.

# ## 3.3 The Output of the ls -l Command

```
$ -l
1rwxrxr-wx 1 root 5 May 3 18:24 sshd->sshd1
1rwxrxr-wx 1 root 5 May 3 18:20 sshd.old->sshd1
--rw-xr-x-X 1 root 649246 May 3 18:24 sshd1
-rw-rw--X 1 root 649246 May 3 18:20 sshd1.old
-xr-xr-x-X 1 root 56712 Sep 2 11:00 visudo
```

You'll remember that directories, symbolic links, devices, and text files are all files under Linux. The first character in the permission string located in column 1 of the ls -l output indicates the file type. It only differentiates between regular files (-), directories (d), links (l), special files (c), block special files (b), pipes (p), and sockets (s). These file types are discussed further in the "File Types Defined" section later in this chapter.