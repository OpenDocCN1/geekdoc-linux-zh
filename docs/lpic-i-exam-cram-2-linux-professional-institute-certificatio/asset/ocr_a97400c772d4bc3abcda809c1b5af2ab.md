Redirect this output to a file and keep that file on a disk or in some safe place off the system. Every so often, you should run the same find command and then compare the results to the original with the diff command, such as

```
diff /root/latestfindperm /mnt/floppy/findperm.orig
> -rw-xr-xr-t 1 root root 700108 Aug 25 21:17 /usr/bin/align
```

If you ran the previous command and got the output shown, that would mean that something or someone had set the align command to have the sticky bit set. Use your imagination, improvise, adapt, script!

You also need to understand the files the various -perm operators bring back. Make a new directory named /root/test; then change to that directory. Create a set of four files with the following permissions:

```
-rwxrwxrwx 1 root root 0 Dec 8 08:30 file1
-rwxrwsrwx 1 root root 0 Dec 8 21:14 file2
-rwxrwxrwt 1 root root 0 Dec 8 21:16 file3
-rw-r-s-rw- 1 root root 0 Dec 8 21:19 file4
```

Run the following queries and see what you get:

+   find /dir -perm 4000 FILES:
+   find /dir -perm -4000 FILES:
+   find /dir -perm +6000 FILES:
+   find /dir -perm +1000 FILES:

Answers:

```
Query 4000 FILES: No Files Found
Query +4000 FILES: file1 file4
Query +6000 FILES: file1 file2 file4
Query +1000 FILES: file3
```

# Default Permissions

If your system is a default Linux system, a single value is set in the /etc/bashrc or ~/.bashrc file for users and governs the permissions any created object has. This value is known as the umask, and there is only one for both directories and files.

The default permissions for directories and files are different. The default permissions with no umask set are

+   - rw-rw-rw- 666—Used for files
+   - rwxrwxrwx 777—Used for directories

Check the umask on the system you have handy with the following command:

```
umask
0022
```