# 1464

# umask

ksh

```
ulimit [-HSacdfnstv] [limit]
```

# Description

Set limit(1).

# umask — Get or Set the File Mode Creation Mask

# Synopsis

```
/usr/bin/umask [-S] [mask]
```

```
sh, csh
```

```
umask [ooo]
```

```
ksh
```

```
umask [-S] [mask]
```

# Description

When you create a file or directory, the default file permissions assigned to the file or directory with the mask are controlled by the user mask. You set the user mask with the umask command in a user initialization file such as /etc/profile or .cshrc. You can display the current value of the user mask by typing umask and pressing Return.

You set the user mask with a three-digit octal value such as 022. The first digit permissions for the user, the second for the group, and the third for others. To set the umask to 022, type

File permissions of 666 read and write permissions to the user, group, and others. Directory permissions of 777 grant read, write, and execute permissions to the user, group, and umask. The value assigned is subtracted from these values. To determine the umask value you want to set, subtract the permissions you want from 666 (for a file) or 777 (for a directory). The remainder is the value to use with the umask command. For example: suppose you want to change the default mode for files to 644 (rw-r----). The difference between 666 and 644 is 022, which is the value to use as an argument to the umask command.

Setting the umask value denies permissions in the same way that the chmod command grants them. For example, the chmod 022 grants write permission to group and others, umask 022 denies permission for group and others.

```
/usr/bin/umask
```

The umask command sets the file-mode creation mask of the current shell execution environment to the value specified by the umask oper. This mask affects the initial value of the file permission bits of subsequently created files. If umask is called in a subshell or separate command execution environment, as one of the following,