# ACCESS PERMISSIONS 219

setuid program that removes all files in a directory, you can remove files in any of the file owner's directories, even if you do not have permission to do so. In a similar manner, setgid (set group ID) permission gives the process executing the file privileges of the group it is associated with.

# Minimize use of setuid and setgid programs by root

security executable files that are setuid and owned by root have privileges when they run, even if they are not run by root. This type of program is very powerful it can do anything that root can do (and that the program is designed to). Similarly executable files that are setgid and belonging to the group root have extensive privileges.

Because of the power they hold and their potential for destruction, it is wise to avoid indiscriminately creating and using using programs owned by root and setgid programs belonging to the group root. Because of their inherent dangers, many minimize the use of these programs over systems. No necessary setuid program is passed. See page 421 for a tip on setuid files owned by root and page 454 for a command that lists files on the local system.

The following example shows a user working with root privileges and using symbolic arguments to chmod to give one program setuid privileges and another program setgid privileges. The -l output (page 215) shows setuid permission by displaying an s in the owner's executable position and setgid permission by displaying an s in the group's executable position

```
$ ls -1 myprog*
-rwxr-xr-x 1 root puts 1974 2010-07-31 14:30 myprog1
-rwxr-sr-x 1 root puts 1974 2010-07-31 14:30 myprog2
$ sudo chmod u+s myprog1
$ sudo chmod g+s myprog2
```

```
$ ls -1 myprog*
-rwxr-xr-x 1 root puts 1974 2010-07-31 14:30 myprog1
-rwxr-sr-x 1 root puts 1974 2010-07-31 14:30 myprog2
```

The next example uses numeric arguments to chmod to make the same changes. When you use four digits to specify permissions, setting the first digit to 1 sets the sticky bit (page 1174), setting it to 2 specifies setgid permissions, and setting it to 4 specifies setuid permissions:

```
$ ls -1 myprog*
-rwxr-xr-x 1 root puts 1974 2010-07-31 14:30 myprog1
-rwxr-sr-x 1 root puts 1974 2010-07-31 14:30 myprog2
```

```
$ sudo chmod 4755 myprog1
$ sudo chmod 2755 myprog2
```

```
$ ls -1 myprog*
-rwxr-xr-x 1 root puts 1974 2010-07-31 14:30 myprog1
-rwxr-sr-x 1 root puts 1974 2010-07-31 14:30 myprog2
```

# Do not write setuid shell scripts

security Never give shell scripts permission. Several techniques for subverting them are well known.