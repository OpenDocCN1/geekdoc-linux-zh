shell programs, and the permissions control the access that others will have to these programs. **umask** is used to specify permission settings for new files and directories.

![](bbox=[0.87, 0.08, 0.98, 0.19])

![](bbox=[0.87, 0.2, 0.98, 0.32])

Let's start with an example of a long listing of a file. We'll use ls -l in the following examples:

```
sys1 1: ls -l script1
-rwxr-xr-x 1 marty users 120 Jul 26 10:20 script1
```

The access rights for this file are defined by the position of read (r), write (w), and execute (x) when the ll command is issued. Figure 6-5 shows the three groups of three access rights for this file.

![](bbox=[0.07, 0.48, 0.91, 0.81])

# Figure 6-5 Example of File Permissions

The owner of this file has read, write, and execute permissions on the file. The group to which the user belongs has read and execute permissions, and others also have read and execute permissions. The