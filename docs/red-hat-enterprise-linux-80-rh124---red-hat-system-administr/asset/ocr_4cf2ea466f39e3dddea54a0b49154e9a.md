makes it harder for an attacker to compromise a network service so that it creates a new file and
immediately executes it as a program.

However, the session will also set a umask to further restrict the permissions that are initially
set. This is an octal bit used to clear the permissions of new files and directories created by
a process. If a bit is set in the umask, then the corresponding permission is cleared on new files.
For example, umask 0002 clears the write bit for others. The leading zeros indicate the
special, user, and group permissions are not cleared. A umask of 0077 clears all the group and
other permissions of newly created files.

The umask command without arguments will display the current value of the shell's umask:

```
[user@host ~]$ umask
0002
```

Use the mask command with a single numeric argument to change the umask of the current shell.
The numeric argument should be an octal value corresponding to the new umask value. You can
omit any leading zeros in the umask.

The system's default umask values for Bash users are defined in the /etc/profile and /
/etc/bashrc. Users can override the system defaults in the .bash_profile and .bashrc
files in their directories.

# umask Example

The following example explains how the umask affects the permissions of files and directories.
Look at the umask permissions for both files and directories in the current shell. The owner
and group have both read and write permission on files, and other is set to read. The owner and
group have both read, write, and execute permissions on directories. The only permission for other
is read.

```
[user@host ~]$ umask
0002
[user@host ~]$ touch default
[user@host ~]$ ls -1 default.txt
-rw-rw-r--. 1 user owner May 9 01:54 default.txt
[user@host ~]$ mkdir default
[user@host ~]$ ls -1d default
drwxwxrxr-x. 2 user owner May 9 01:54 default
```

By setting the umask value to 0, the permissions for other change from read to read and write.
The directories permissions for other changes and execute to read, write, and execute.

```
[user@host ~]$ umask 0
[user@host ~]$ touch zero.txt
[user@host ~]$ ls -1 zero.txt
-rw-rw-rw-.. 1 user owner May 9 01:54 zero.txt
[user@host ~]$ mkdir zero
[user@host ~]$ ls -1d zero
drwxrwxr-x. 2 user owner May 9 01:54 zero
```

To mask all file and directory permissions for other, set the umask value to 007.