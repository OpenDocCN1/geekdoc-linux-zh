group, other. For example, the permissions rw-r----- would be specified as 640. The following chmod command uses the numbers to specify file permissions:

chmod 640 file
This command sets the permissions of the file file to rw-r----.
The chmod command supports an alternative way of specifying permissions, which associates letters with the users, as listed in Table 3.4.

# TABLE 3.4 User Designations Used to Specify Permissions

| User | Designation |
|---|---|
| owner | u |
| group owner | g |
| other | o |

These designations are used with the letters shown in Table 3.2 to add or subtract permissions from a file or directory. For example, to ensure that group members can read a file, issue a command such as

```
chmod g+r file
```

This command enables the owner of the file and the members of the group who owns the file to read the file. To assure that others cannot access the file, issue a command such as

```
chmod o-rwx file
```

This command disables the read, write, execute permissions of users other than the owner and members of the group that own the.
When you create a file, its access permissions are set to the complement of the value specified by the umask command. You can compute the complement by subtracting each digit from 7. For example, if you issue the

```
umask 027
```

the complement of the umask value is 750. However, a newly created file is never automatically set to executable, the effective value is 640. Thus, given a umask value of 027, you will be able to read and write any files that you create, members of your group will be able to read the files, and others won't