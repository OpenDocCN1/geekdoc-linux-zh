more permission than what's listed here, but this should describe what these minimum permissions on files do:

```
-r----- Allow read access to the file by owner
-w----- Allow the owner to modify or delete the file
    (Note that anyone with write permission to the directory the file is in can overwrite it and thus delete it)
--x--- The owner can execute this program, and not shell scripts, which still need read permission
-5----- Will execute with effective User ID - to owner
-w----- Will execute with effective Group ID - to group
-rw----T No update of 'Last modified time'. Usually used for swap files
---t--- No effect. (formerly sticky bit)
```

**Directory Example:**

```
drwxr-xr-x 3 kevin users        512 Sep 19 13:47
.public_html/
1st bit - directory?       (yes, it contains many files)
2nd bit - read by owner?   (yes, by kevin)
3rd bit - write by owner?  (yes, by kevin)
4th bit - execute by owner? (yes, by kevin)
5th bit - read by group?   (yes, by users)
6th bit - write by group?  (no)
7th bit - execute by group? (yes, by users)
8th bit - read by everyone? (yes, by everyone)
9th bit - write by everyone? (no)
10th bit - execute by everyone? (yes, by everyone)
```

The following lines are examples of the minimum sets of permissions that are required to perform the access described. You may want to give more permission than what's listed, but this should describe what these minimum permissions on directories do:

```
dr------- The contents can be listed, but file attributes can't be read
d-x------ The directory can be entered, and used in full execution paths
dr-x----- File attributes can be read by owner
d-wx----- Files can be created/deleted, even if the directory isn't the current one
d-------x-t Prevents files from deletion by others with write access. Used on /tmp
d---s-S--- No effect
```

System configuration files (usually in /etc) are usually mode 640 (-rw-r-----), and owned by root. Depending on your site's security