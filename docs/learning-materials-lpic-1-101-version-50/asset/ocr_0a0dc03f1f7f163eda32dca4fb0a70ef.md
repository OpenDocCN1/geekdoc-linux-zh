# # Explorational Exercises

1. Try this on a terminal: create an empty file called `emptyfile` with the command `touch emptyfile`. Now “zero out” the permissions for the file with `chmod 000 emptyfile`. What will happen if you change the permissions for `emptyfile` by passing only *one* value for `chmod` in octal mode, like `chmod 4 emptyfile`? And if you use two, as in `chmod 44 emptyfile`? What can we learn about the way `chmod` reads the numerical value?

2. Consider the permissions for the temporary directory on a Linux system, `/tmp`:

```
$ ls -l /tmp
drwxrwxrwt 19 root root 16K Dec 21 18:58 tmp
```

User, group and others have full permissions. But can a regular user delete *any* files inside this directory? Why is this the case?

3. A file called `test.sh` has the following permissions: `–rwsr-xr-x`, meaning the SUID bit is set. Now, run the following commands:

```
$ chmod u-x test.sh
$ ls -l test.sh
-rwsr-xr-x 1 carol carol 33 Dec 11 10:36 test.sh
```

What did we do? What does the uppercase S mean?

4. How would you create a directory named Box where all the files are automatically owned by the group users, and can only be deleted by the user who created them?