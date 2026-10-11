You also can have anyone running the script inherit the privileges of the group instead of the owner by issuing the command

```
chmod gs MyScript
```

or

```
chmod 2755 MyScript
```

The permission block, after making this change, would be -rwxr-sr-x.

An example of using this permission is when a user changes her password. For a password change to become effective, the new password must be written to the /etc/passwd file. However, the permissions on the /etc/passwd file are

```
-rw-r--r-- 1 root root 876 Oct 20 11:32 passwd
```

Only the owner, root, has the permission to write to this file. Neither the group nor others have been granted the write permission to this file.

Users can change their passwords because the SUID bit has been set on the /usr/bin/passwd command as

```
-r-sr-xr-x 1 root bin 15613 Apr 27 1998 /usr/bin/passwd
```

Notice the s where the bit is set for execute by owner. This means that when the file is executed, the user gets the same privileges as root-the capability to write to the /etc/passwd file. This is considered a significant security risk and should be used only if absolutely necessary.

# Key Concept

Setting SUID and GUID enables a user to run a command or application with the permissions of another. Therefore, the use of these two special permissions can be a significant security risk.

# Sticky Bit

The sticky bit enables you to manage shared directories more efficiently. The most common use of the sticky bit is on world writable directories where you want only the owner to be able to delete a file.