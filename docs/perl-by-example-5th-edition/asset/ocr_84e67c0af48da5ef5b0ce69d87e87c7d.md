# EXAMPLE 16.13

```
```
(UNIX)

1   $ perl -e '$count=chmod 0755, "foo.p", "boo.p" ;print "$count
    files changed.\n"'
2   2 files changed.
3   $ ls -l foo.p boo.p
    -rwxx-xx-x  1 ellie     0 Mar  7 12:52 boo.p*
    -rwxx-xx-x  1 ellie     0 Mar  7 12:52 foo.p*
```
```

# EXPLANATION

+   1. The first argument is the octal value 0755. It turns on rwx for the user, r and x for the group and others. The next two arguments, foo.p and boo.p, are the files affected by the change. The scalar $count contains the number of files that were changed.
+   2. The value of $count is 2 because both files were changed to 0755.
+   3. The output of the UNIX is -l command is printed, demonstrating that the permissions on files foo.p and boo.p have been changed to 0755.

**The chown Function (UNIX).** The _chown_ function changes the owner and group of a list of files. Only the owner or superuser can invoke it.⁶ The first two elements of the list must be a numerical uid and gid. Each authorized UNIX user is assigned a uid (user identification number) and a gid (group identification number) in the password file.⁷ The function returns the number of files successfully changed.

# FORMAT

```
```
chown( LIST );
chown( LIST );
```
```

# EXAMPLE 16.14

```
```
(The Script)
1   $ uid=9496;
2   $ gid=40;
3   $number=chown($uid, $gid, 'foo.p', 'boo.p');
4   print "The number of files changed is $number.\n";

(Output)
4   The number of files changed is 2.
```
```

# EXPLANATION

+   1. The user identification number 9496 is assigned.
+   2. The group identification number 40 is assigned.
+   3. The _chown_ function changes the ownership on files foo.p and boo.p and returns the number of files changed.

> 6. On BSD UNIX and some POSIX-based UNIX, only the superuser can change ownership.
> 7. To get the uid or gid for a user, use the getpwnam or getgrgid functions.