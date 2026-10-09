The modification time has changed since the \-m option to the touch changed the modification time (atime). We also notice that as with the cat > command, the ctime also changed. We pause for a minute and execute the commands below:

```
$ touch -a time.txt
$ ls -l time.txt; ls -l --time=atime time.txt; ls -l --time=ctime time.txt
-rwxr--r--	1 deepakt users	14 Jan 20 03:54 time.txt
-rwxr--r--	1 deepakt users	14 Jan 20 03:55 time.txt
-rwxr--r--	1 deepakt users	14 Jan 20 03:55 time.txt
```

As seen above, using the -a option to touch, we can modify the access time (atime) of the file. Consequently, the ctime also has changed.

The difference between using touch and cat (or a text editor) is clearer when it comes to modifying the access time. When changing the atime with touch, the ctime is also modified whereas it is unchanged when using the cat > command.

# **File Size**

The size of a file is indicated in the file listing with the -l option in bytes:

```
$ ls -al dissectme.txt
-rw-r--r--	1 deepakt users	21 Jan 19 18:40 dissectme.txt
```

To obtain the size of the contents of a directory, we could use the du command. The -h option prints the size in a human-readable format, i.e. in bytes, kilobytes, megabytes, etc. The -s option summarizes the output rather than list the sizes of each of the files and directories in each of the subdirectories:

```
$ du -sh /home/deepakt/
153M /home/deepakt
```

# **File Names**

The ls command always displays file names, regardless of what options you choose. The -F option indicates the various file types with symbols, such as:

+   - A slash (/) next to a directory
+   - An asterisk (*) next to an executable file
+   - A pipe (|) next to a FIFO
+   - An @ next to a symbolic link