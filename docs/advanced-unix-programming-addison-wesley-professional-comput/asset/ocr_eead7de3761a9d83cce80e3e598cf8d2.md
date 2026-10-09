# 2.3 Symbols for File Permission Bits

Recall from Section 1.1.5 that a file has 9 permission bits: read, write, and execute for owner, group, and others. We see them all the time in the output of the `ls` command:

```
-rwxr-xr-x 1 marc users 29808 Aug 4 13:45 hello
```

Everyone thinks of the 9 bits as being together and in a certain order (owner, group, others), but that’s not a requirement—only that there be 9 individual bits. So, from POSIX1988 on there have been symbols for the bits that are supposed to be used instead of octal numbers, which had been the traditional way to refer to them. The symbols have the form $s_{-}$ pww where **p** is the permission (R, W, or X) and **www** is for whom (USR, GRP, or OTH). This gives 9 symbols in all.

For instance, for the previous file, instead of octal 755, we write

```
s_IRUSR | s_IWUSR | s_IXUSR | s_IRGRP | s_IXGRP | s_IROTH | s_IXOTH
```

There are separate symbols for when a USR, GRP, or OTH has all three permissions, which are of the form $s_{-}$ IRWww. This time **w** is just the first letter of the “whom,” either U, G, or O. So the permissions could instead be written like this:

```
s_IRWXU | s_IRGRP | s_IXGRP | s_IRWXO
```

The symbols are necessary to give implementors the freedom to do what they will with the bit positions, even if they’re less readable and much more error-prone than just octal.² As any application you write is likely to use only a few combinations (e.g., one or two for data files it creates, and maybe another if it creates directories), it’s a good idea to define macros for them just once, rather than using