In Example 3-16 the file smilepic shows -rwxrwx-rw-, which indicates that: the owner has read, write, and excute access; the group has read and write access; and other users have read and write access.

# Example 3-16 Sample of file permissions

```
lnxken:~/Desktop/MyDocs/MyPictures # ls -l
total 8
-rwxrwx-rw- 1 ken student 83 May 19 17:20 smilepic
-rw-r--r-- 1 ken student 83 May 19 17:18 smilepic.bak
lnxken:~/Desktop/MyDocs/MyPictures #
```

> Note: Although a user might have permission for a certain action for a file, that user still might not have access to that action based on the permission of the directory in which the file is located.

# Changing permissions

Users can change their own file permissions but cannot change permissions of other users. Note that the root user ID does have the power to change permissions on all files.

The Linux command to change a file permission is chmod, which can be used in two ways: with the octal system or with symbols.

# Octal system

The octal system uses numbers to change the permission of the file. After a user understands the octal system, using it is generally faster than using symbols.

Table 3-3 lists the combinations of octal numbers for giving permissions.

# Table 3-3 Permission combinations

| Value | Permission |
| --- | --- |
| 1 | --- |
| 2 | --x |
| 3 | -wx |
| 4 | r-- |
| 5 | r-x |
| 6 | rw- |
| 7 | rwx |