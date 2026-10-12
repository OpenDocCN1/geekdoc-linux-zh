+   2.  Configure the directory to be visible to everyone but editable only by the administrator. Using the `chmod` command, set permissions on the `/export` directory to allow read permissions for everyone, but restricting write permissions to the directory owner alone.
+   
+   3.  Within the export directory, create directories for the executives, researchers, applications staff, and sales staff to share their files internally.
+   
+   4.  Set group ownership on each directory to the corresponding user group (see the groups defined in Project 5-2). Use the `chgrp` command.
+   
+   5.  Set the permissions on the directories so that the executives alone can read and write in their shared directory, and so that members of all four groups can read the contents of the other directories, but only each group's members can write to each group's directory.
+   
+   6.  Test access by using the `su` - command to log in as another user temporarily. See if you can create files in directories in which the user has write permission. Make sure you can't create files in directories in which the user lacks write permission.

# Project Summary

Real-world file access rules can be much more complicated than this, but changing group ownership and membership and changing directory permissions is key to managing data directories. Be sure that you create your export area on a disk partition that has ample space for the files you expect to be sharing with others. Once the area is set up the way you want it, with only a little more work (described in later modules), you'll be able to have local users, NFS access, FTP access, or HTTP access provided as needed.

# Finding a File: find

The `find` command lets you search for files according to various criteria. Like the tools you have already considered, `find` has a large number of options that you can read about on its man page. Here is the general format of `find`:

```
[michael@workbox michael]$ find start_dir [options]
```

where `start_dir` is the directory from which the search should start. Table 6-3 shows the most common options used with `find`.

To find all files in `/tmp` that have not been accessed in at least seven days, use the following command:

```
[root@workbox /tmp]# find /tmp -atime 7 -print
```