To set the `suid` with the character system, you execute the following command:

```
$ chmod u+s <filename>$
```

To set the `sgid` with the character system, you execute the following command:

```
$ chmod g+s filename$
```

To set the `suid` and the `sgid` using the numeric system, use these two commands:

```
$ chmod 2### filename$
$ chmod 4### filename$
```

In both instances, you replace `###` with the rest of the values for the permissions. The additive process is used to combine permissions; therefore, the following command adds `suid` and `sgid` to a file:

```
$ chmod 6### filename$
```

# **Note**

> A sticky bit is set by using chmod `1###` `<filename>`. If a sticky bit is set, the executable is kept in memory after it has finished executing. The display for a sticky bit is a `t`, placed in the last field of the permissions. Therefore, a file that has been set to 7777 would have the following permissions: -rwxrwxrwt.

# ## The Default Mode for a File or Directory

The default mode for a file or directory is set with the `umask`, which uses the numeric system to define its value. To set the `umask`, you must first determine the value you want the files to have. For example, a common file permission set is `644`, with which the owner has read and write permission and the rest of the world has read permission. After the value is determined, you subtract it from `777`. Keeping the same example of `644`, the value would be `133`. This value is the `umask` value. Typically, this value is placed in a system file that is read when a user first logs on. After the value is set, all files created will set their permissions automatically, using this value.

# ## Passwords—A Second Look

The system stores the user’s encrypted password in the `/etc/passwd` file. If the system is using a shadow password system, the value placed in this field is x. A value of * blocks login access to the account, as * is not a valid character for an encrypted field. This field should never be edited by hand (after it is set up). Instead, a program such as passwd