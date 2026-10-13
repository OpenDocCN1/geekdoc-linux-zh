```
```text
# ls -l
-rwxrw-r--  1 dla      other       636 Jan 24 12:42 file1
# chmod g+s file1
# ls -l
-rwxrwsr--  1 dla      other       636 Jan 24 12:42 file1
#
```
```

Another special file permission is the sticky bit. Originally, it was used to indicate programs that should be left in memory after execution. When set for frequently used programs, the sticky bit saved time and CPU cycles by using the image left in memory instead of loading it from disk again.

When the sticky bit is set on a directory that allows write permission for everyone, only the user account that created files and subdirectories under the directory can remove those files and subdirectories. This restriction is especially useful for the /tmp directory, which is available from any user account.

The sticky bit permission has an absolute mode of 1000 and a symbolic mode of t when used with the chmod command. This permission is shown as t in the other account execution permission field in the output of an ls command, but it is considered a user account (owner) permission. The following example shows using the chmod command to remove the sticky bit permission and then add it to a directory:

```
```text
# ls -ld /tmp
drwxrwxrwt  7 sys      sys         410 Jan 28 03:30 /tmp
# chmod u-t /tmp
# ls -ld /tmp
drwxrwxrwx  7 sys      sys         410 Jan 28 03:30 /tmp
# chmod 1777 /tmp
# ls -ld /tmp
drwxrwxrwt  7 sys      sys         410 Jan 28 03:30 /tmp
#
```
```

# ## Extended File Permissions: Access Control Lists

Solaris 8 extends the standard Unix file permissions by adding an Access Control List (ACL) capability. ACLs enable you to add permissions for specific users and groups along with a default permission (mask).

In addition to supporting the standard read/write/execute permissions for the standard file user account (owner), ACLs can be used to set read/write/execute permissions for additional user accounts. Likewise, ACLs support read/write/execute permissions for the standard file group account and allow read/write/execute permissions for additional group accounts. In