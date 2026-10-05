removed (erased) only the owner of the file, or a member of the group that owns the file, or the root.
Yet other users may be able to modify or erase the content of the file if they are given the permission
to do so--read on. The owner and group that owns the file will be shown in the output from the ls
-1 command ("=list in the long format"). For example, the command:

```
ls -1 junk
```

produced this output on my screen:

```
-rwx------ 1 yogin inca 27 Apr 24 14:12 junk
```

This shows the file "junk," belonging to the owner "yogin" and to the group "inca".

The ownership of a file can be changed using the commands chown (change owner) and chgrp
(change group), which are normally executed by root:

```
chown peter junk
chgrp peter junk
ls -1 junk
```

After executing the above 3 lines, the command ls-l junk produces this output on my screen:

```
-rwx------ 1 peter 27 Apr 25 20:27 junk
```

Changing the file ownership comes if you move/copy files as root for use by other\users. At the end of your housekeeping you typically want to hand-in the file ownership to the user.

**File Permissions.** Now, an owner of a file can make the file accessible in three modes: read (r),
write (w) and execute (x) to three classes of users: owner (u), members of the group (g), others on the
system (o). You can check the current access permissions:

```
ls -l filename
```

If the file is accessible to all users (owner, group, others) in all three modes (read, write, execute) it
will show:

```
-rwx-xr-x
```

Skip the first "-\ (it shows "d" for directories, "-" for normal files, "l" for links, "c" for character
dev, "b" for block devices). After this initial character, the first triplet shows the file permission
for the owner of the file, the third triplet shows the permissions for other users. A "no" permission is shown as "-". Here is
output from the ls -1 command on a file that is owned by root, for which the owner (root) has all
permissions, but the group and other can read and execute:

```
drwxr-xr-x 2 root root 21504 Apr 24 19:27 dev
```