```
myprog.c.gz
-rwxr-xr-x    1 rich     rich          5178 Sep   6 13:43
myprog.gz
-rw-r--r--    1 rich     rich             59 Sep   6 13:46
my script.gz
-rw-r--r--    1 rich     rich             60 Sep   6 13:44
my script2.gz
$
```

The gzip command compresses every file in the directory that matches the wildcard pattern.

# Archiving data

Although the zip command works great for compressing and archiving data into a single file, it's not the standard utility used in the Unix and Linux worlds. By far the most popular archiving tool used in Unix and Linux is the tar command.

The tar command was originally used to write files to a tape device for archiving. However, it can also write the output to a file, which has become a popular way to archive data in Linux.

Here is the format of the tar command:

tar function [options] object1 object2 ...

The function parameter defines what the tar command should do, as shown in Table 4-8.

**TABLE 4-8 The tar Command Functions**
| Function | Long Name | Description |
| :------- | :-------- | :---------- |
| -A | --concatenate | Append an existing tar archive file to another existing tar archive file. |
| -c | --create | Create a new tar archive file. |
| -d | --diff | Check the differences between a tar archive file and the filesystem. |
| | --delete | Delete from an existing tar archive file. |
| -r | --append | Append files to the end of an existing tar