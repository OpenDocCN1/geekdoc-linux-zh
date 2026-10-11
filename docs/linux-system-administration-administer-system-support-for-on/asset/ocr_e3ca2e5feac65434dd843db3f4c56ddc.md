For a convenient example, let's use the following directory listing to see the current files in the directory.

```
$ ls
dump
ext2fs
info.txt
info2.txt
ls.txt
mknod
moreinfo
morestuff
```

If you wanted to ignore the file info.txt you would include it with the -ignore option.

```
$ ls -ignore=info.txt
dump
ext2fs
info2.txt
ls.txt
mknod
moreinfo
morestuff
```

You can get more information from a directory listing by using the long listing options. The most common one is -l, which can tell you a great deal about a file - including permissions, user, group, file size, modification date and time, and file-name. The l option also provides information on symbolic links, directories, and other special files.

```
$ ls -l
-rw-r--r--    1 stripes    users      15908  Aug 10 17:39  dump
-rw-r--r--    1 stripes    users      17944  Aug 10 17:55  ext2fs
-rw-xr-xr-x    1 stripes    users       1452  Aug 11 14:12  info.txt
-rw-r--r--    1 stripes    users       1557  Aug 11 14:15  info2.txt
-rw-r--r--    1 stripes    users       4464  Aug 11 21:42  ls.txt
-rw-r--r--    1 stripes    users       2524  Aug 10 17:25  mknod
drwxr-xr-x    2 stripes    users       1024  Aug 6 17:06  moreinfo
drwxr-xr-x    2 stripes    users       1024  Aug 6 17:07  morestuff
```

You can also get a long listing without the group information by using the -0 option. If you want to have trailing characters to define file type in your listing, use the -F option. From the following listing, you can see executable files identified by asterisks (*); the names of directories appear with forward slashes (/).