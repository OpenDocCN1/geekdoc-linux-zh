# Ownership and Permissions

2. If I now try to change the ownership back, it fails:

```
% chown taylor test
chown: test: Not owner
```

Most modern UNIX systems prevent users from changing the ownership of a file due to the inherent dangers. If you try to chown, and it returns Command not found or Permission denied, that means you are barred from making any file ownership changes.

3. On of the systems I use, chown always reports Not owner when I try to change a file regardless of whether I am the owner or not:

```
% ls -l mytest
-rwxrwxrwx 1 taylor      0 Oct 12 15:17 mytest
% chown root mytest Not owner
```

This is needlessly confusing—a message like “you’re not allowed to change file ownership” would be better. But, alas, like so of UNIX, it's up to the user to figure out what's going on.

To change the ownership of a file or directory, you can use the chown command to have the appropriate access on your system. It's a huge superantanker, though: you cannot change order once underway, so be cautious!

# Task 5.9: Change the Group of a File or Directory

Changing the membership of a file or directory is quite analogous to the steps required for file ownership. Almost all UNIX systems enable users to use the chgrp command to accomplish this task.

1. Usage of chgrp is almost identical to chown, too. Specify the name of the group, followed by the list of files or directories to reassign:

```
% ls -lg
-rwxrwxrwx 1 taylor ci      0 Oct 12 15:17 mytest
% chgrp ftp mytest
% ls -lg
-rwxrwxrwx 1 taylor ftp      0 Oct 12 15:17 mytest
```

The caveat on this command, however, is that you must be a member of the group you're assigning for the file, or it fails:

```
% ls -lg
-rwxrwxrwx 1 taylor ftp      0 Oct 12 15:17 mytest
% chgrp root mytest
chgrp: You are not a member of the root group
```