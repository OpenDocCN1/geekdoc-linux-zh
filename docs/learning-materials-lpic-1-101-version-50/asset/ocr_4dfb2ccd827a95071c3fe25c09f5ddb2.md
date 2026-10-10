Of course, this will not solve the problem of files created *after* the last database update not showing up. For this you will have to update the database with the command updatedb. How long this will take will depend on the amount of files of your disk.

# **Controlling the Behavior of updatedb**

The behavior of updatedb can be controlled by the file */etc/updatedb.conf*. This is a text file where each line controls one variable. Blank lines are ignored and lines that start with the # character are treated as comments.

+   **PRUNEFS=**
+   
+   Any filesystem types indicated after this parameter will not be scanned by updatedb. The list of types should be separated by spaces, and the types themselves are case-insensitive, so NFS and nfs are the same.

+   **PRUNENAMES=**
+   
+   This is a space-separated list of directory names that should not be scanned by updatedb.

+   **PRUNEAPTHS=**
+   
+   This is a list of path names that should be ignored by updatedb. The path names must be separated by spaces and specified in the same way they would be shown by updatedb (for example, */var/spool* */media*)

+   **PRUNE_BIND_MOUNTS=**
+   
+   This is a simple *yes* or *no* variable. If set to yes bind mounts (directories mounted elsewhere with the mount --bind command) will be ignored.

# **Finding Binaries, Manual Pages and Source Code**

which is a very useful command that shows the full path to an executable. For example, if you want to locate the executable for bash, you could use:

```
```
$ which bash
/usr/bin/bash
```
```

If the -a option is added the command will show all pathnames that match the executable. Observe the difference:

```
```
$ which mkfs.ext3
/usr/sbin/mkfs.ext3
```
```