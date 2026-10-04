# 542 Protecting Files and Directories

with dashes in place of letters for disallowed operations. Think of rwxrwxrwx as three occurrences of the string rwx. Assign the values r=4, w=2, and x=1. To get the value of the sequence rwx, simply add the values of r, w, and x. Thus, rwx = 7. Using this formula, you can assign a three-digit value to any permission setting. For example, if you can read and write the file but everyone else can only read the file, the permission is rw-r----(that is how it appears in the listing), and the value is 644. Thus, if you want all files in a directory to be readable by everyone but writable only by you, use the following command:

```
chmod 644 *
```

# Setting default permission

What permission does a file get when you (or a program) create a new file? The answer is in what is known as the user file-creation mask that you can see and set using the `umask` command.

**Type umask**, and it prints out a number showing the current file-creation mask. The default setting is for the `root` user and other normal users. The `root` user mask is set to 022, whereas the mask for normal users is 002. To see the effect of this file-creation mask and to interpret the meaning of the mask, follow these steps:

+   1. Log in as root and type the following command:

```
touch junkfile
```

This command creates a file named `junkfile` with nothing in it.

+   2. Type `-l` to see the file's permissions.

You see a line similar to the following:

```
-rw-r--r--  1 root root  00 Aug 24 10:56 junkfile
```

Interpret the numerical value of the permission setting by converting each three-letter permission in the first field (excluding the very first) into a number from 0 to 7. For each letter the second letter is 4, and the third is 1. For example, `rw-` translates to 4+2+0 (because the third letter is missing) or 6. Similarly, `r--` is 4+0+0=4. The permission string `-rw-r--r--` becomes 644.

+   3. Subtract the numerical setting from 666 and what you get is the umask setting.

In this case, 666-644 results in an `umask` of 022.

Thus an umask of 022 results in a default permission setting of 666-022=644. When you rewrite 644 in terms of a permission string, it becomes `rw-r--r--`.