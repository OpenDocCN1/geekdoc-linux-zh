# NUMERIC ARGUMENTS to chmod

You can also use numeric arguments to specify permissions used in the previous examples, instead of letters and symbols specifying permissions. numeric arguments comprise three octal digits. (A fourth, leading digit controls setuid and setgid permissions is discussed next.) The first digit specifies permissions for the owner, the second for the group, and the third for other users. A 1 gives the user(s) execute permission, a 2 write permission, and a 4 gives read permission. Construct the digit representing the permissions for the owner, group or by ORing (adding) the appropriate values as shown in the following examples. Using numeric arguments sets file permissions absolutely; it does not modify existing permissions as symbolic arguments.

In the following example, chmod changes permissions only the owner of the file can read from and write to the file, regardless of how permissions were previously set. The 6 in the first position gives the owner read (4) and write (2) permissions. The 0 removes all permissions for the group and other users.

```
$ chmod 600 letter.0610
$ ls -1 letter.0610
--rw------- - 1 max 3355 2010-06-22 12:44 letter.0610
```

Next, 7 (4 + 2 + 1) gives the owner read, write, and execute permissions. The 5 (4 + 1) gives the group and other users read and execute permissions:

```
$ chmod 755 check_spell
$ ls -1 check_spell
-rwxr-xr-x 1 max 852 2010-07-31 13:47 check_spell
```

Refer to Table 6-2 for more examples of numeric permissions.

# Table 6-2 Examples of numeric permission specifications

| Mode | Meaning |
|---|---|
| 777 | Owner, group, and others can read, write, and execute file |
| 755 | Owner can read, write, and execute file; group and others can read and execute file |
| 711 | Owner can read, write, and execute file; group and others can execute file |
| 644 | Owner can read and write file; group and others can read file |
| 640 | Owner can read and write file, group can read, and cannot access file |

Refer to page 300 for more information on using chmod to make a file executable and to the chmod man page for information on absolute arguments and chmod in general. Refer to page 492 for more information on groups.

# SETUID AND SETGID PERMISSIONS

When you execute a file that has setuid (user ID) permission, the process executing the file takes on the privileges of the file's owner. For example, if you run a