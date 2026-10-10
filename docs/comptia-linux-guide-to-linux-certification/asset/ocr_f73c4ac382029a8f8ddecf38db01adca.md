Although the `ls -F` command is a quick way of getting file type information in an easy-to-read format, at times you need to obtain more detailed information about each file. The `ls -l` command can be used to provide a long listing for each file in a certain directory.

```
[root@server1 -]# pwd
/root
[root@server1 -]# ls -l
total 548
lrwxrwxrwx 1 root root 9 Apr 7 09:56 current -> >project12
drwx------ 3 root root 4096 Mar 29 10:01 Desktop
-rwxr-xr-x 1 root root 519964 Apr 7 09:59 myprogram
-rwxr-xr-x 1 root root 20 Apr 7 09:58 myscript
-rw-r--r-- 1 root root 71 Apr 7 09:58 project
-rw-r--r-- 1 root root 71 Apr 7 09:59 project1
-rw-r--r-- 1 root root 71 Apr 7 09:59 project12
-rw-r--r-- 1 root root 0 Apr 7 09:56 project13
-rw-r--r-- 1 root root 71 Apr 7 09:59 project2
-rw-r--r-- 1 root root 90 Apr 7 10:01 project3
-rw-r--r-- 1 root root 99 Apr 7 10:01 project4
-rw-r--r-- 1 root root 108 Apr 7 10:01 project5
[root@server1 -]#_
```

Each file listed in the preceding example has eight components of information listed in columns from left to right:

+   1. A file type character
+      \- The d character represents a directory.
+      \- The l character represents a symbolically linked file (discussed in Chapter 4).
+      \- The b or c characters represent special device files (discussed in Chapter 5).
+      \- The n character represents a named pipe.
+      \- The s character represents a socket.
+      \- The \- character represents all other file types (text files, binary data files).
+   2. A list of permissions on the file (also called the mode of the file)
+   3. A hard links count (discussed in Chapter 5)
+   4. The owner of the file (discussed in Chapter 5)
+   5. The group owner of the file (discussed in Chapter 5)
+   6. The file size
+   7. The most recent modification time of the file
+   8. The filename (Some files are shortcuts or pointers to other files and indicated with an arrow ->, as with the file called “current” in the preceding output; these are known as symbolic links and are discussed in Chapter 5.)

For the file named “project” in the previous example, you can see that this file is a regular file because the long listing of it begins with a \- character, the permissions on the file are rw-r---r--, the hard link count is 1, the owner of the file is root user, the group owner of