Consider the root user's home directory listing, shown in the following example:

```
[root@server1 ~]# ls -l
total 28
drwx------    3 root     root     4096 Apr  8 07:12 Desktop
-r--w--x     1 bob      proj       282 Apr 29 22:06 file1
----------    1 root     root        82 Apr 29 22:06 file2
-rwxrwxrwx    1 root     root        82 Apr 29 22:06 file3
----------    1 root     root        82 Apr 29 22:06 file4
-rw-r--r--    1 root     root       282 Apr 29 22:06 file5
-rw-r--r--    1 user1    sys        282 Apr 29 22:06 file6
[root@server1 ~]# _
```

Note from the preceding output that all permissions (as shown in Figure 4-3) need not be on a file or directory; if the permission is unavailable, a dash (the hyphen character on your keyboard, - ) replaces its position in the mode. Be certain not to confuse the character to the left of the mode (which determines the file type) with the mode, as it is unrelated to the permissions on the file or directory. From the preceding output, the Desktop directory gives the user or owner of the directory (the root user) read, write, and execute permission, yet members of the group (the root group) do not receive any permissions to the directory. Note that other (everyone on the system) does not receive permissions to this directory either.

Permissions are not additive; the system assigns the first set of permissions that are matched in the mode order: user, group, other. Let us assume that the bob user is a member of the proj group. In this case, the file called file1 in the preceding output gives the user or owner of the file (the bob user) read permission, gives members of the group (the proj group) write permission, and gives other (everyone else on the system) execute permission only. Because permissions are not additive, the bob user will only receive read to file1 from the system.

Linux permissions should not be assigned to other only. Although file2 in our example does not give the user or group any permissions, all other users receive read, write, and execute permission via the other category. Thus, file2 should not contain sensitive data because many users have full access to it. For the same reason, it is bad form to assign all permissions to a file that contains sensitive data, as shown with file3 in the preceding example.

On the contrary, it is also possible to have a file that has no permissions assigned to it, as shown in the preceding example with respect to file4. In this case, the only user who has permissions to the file is the root user.

The permission structure that you choose for a file or directory might result in too few or too many permissions. You can follow some general guidelines to avoid these situations. The owner of a file or directory is typically the person who maintains it; members of the group are typically users in the same company department and must have limited access to the file or directory. As a result, most files and directories that you find on a Linux file system have more permissions assigned to the user of the file/directory than to the group of the file/directory, and the other category has either the same permissions or less than the group of the file/directory, depending on how private that file or directory is. The file file5 in the previous output depicts this common permission structure. In addition, files in a user's home directory are typically owned by that user; however, you might occasionally find files that are not. For these files, their permission definition changes, as shown in the previous example with respect to file1 and file6. The user or owner of file6 is user1, who