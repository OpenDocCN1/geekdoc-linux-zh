# **Sticky Bit Permission Using Symbols**

The sticky bit permission symbol is **t**. The sticky bit shows up as a **t** in the execute position of the other permissions. A program with read and execute permission with the sticky bit would have its permissions displayed as **r\-t**.

```
# chmod +t /home/dylan/myreports
# ls -l /home/dylan/myreports
-rwxr-xr-t 1 root root 4096 /home/dylan/myreports
```

# **Sticky Bit Permissions**

One other special permission provides for greater security on directories, the *sticky bit*. Originally the sticky bit was used to keep a program in memory after it finished execution to increase efficiency. Current Linux systems ignore this feature. Instead, it is used for directories to protect files within them. Files in a directory with the sticky bit set can only be deleted or renamed by the root user or the owner of the directory.

# **Sticky Bit Permission Using the Binary Method**

As with ownership, for sticky bit permissions, you add another octal number to the beginning of the octal digits. The octal digit for the sticky bit is 1 (001). The following example sets the sticky bit for the **myreports** directory:

```
# chmod 1755 /home/dylan/myreports
```

The next example sets both the sticky bit and the User ID permission on the **newprogs** directory. The permission 5755 has the binary equivalent of 101 111 101:

```
# chmod 5755 /usr/bin/newprogs
# ls -l /usr/bin/newprogs
lrwxr-xr-t 1 root root 4096 /usr/bin/newprogs
```

# **Permission Defaults: umask**

Whenever you create a file or directory, it is given default permissions. You can display the current defaults or change them with the **umask** command. The permissions are displayed in binary or symbolic format as described in the following sections. The default permissions include any execute permissions that would be applied to a directory. Execute permission for a file is turned off by default when you create it. This is because standard data files do not use the executable permissions (for a file that you want to be executable like a script, you will have to manually set its execute permission). To display the current default permissions, use the **umask** command with no arguments. The **-S** option uses the symbolic format.

```
$ umask -S
u=rwx,g=rx,o=rx
```

This default umask provides rw-r\-r-- permission for standard files and adds execute permission for directories, rwxr-xr-x.

You can set a new default by specifying permissions in either symbolic or binary format. To specify the new permissions, use the **-S** option. The following example denies others