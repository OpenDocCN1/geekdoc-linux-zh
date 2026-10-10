
`[root@server1 ~]# ls -l Desktop`
total 16
-rw-------    1 user1   root    163 Mar 29 09:58 Floppy
-rw-r--r--    1 user1   root   3578 Mar 29 09:58 Home
-rw-f--r--    1 user1   root   1791 Mar 29 09:58 Start Here
drwx------    2 user1   root   4096 Mar 29 09:58 Trash
[root@server1 ~]# _

Recall that the owner of a file or directory and the root user have the ability to change ownership of a particular file or directory. If a regular user changes the ownership of a file or directory that he owns, that user cannot gain back the ownership. Instead, the new owner of that file or directory must change it to the original user. However, the root user always has the ability to regain the ownership:

```
[root@server1 ~]# chown root file1
[root@server1 ~]# chown -R root Desktop
[root@server1 ~]# ls -1
```
total 4
drwx------    3 root     root   4096 Apr 8 07:12 Desktop
-rw-r--r--    1 root     root     0 Apr 29 15:40 file1
[root@server1 ~]# ls -l Desktop
total 16
-rw-------    1 root     root    163 Mar 29 09:58 Floppy
-rw-f--r--    1 root     root   3578 Mar 29 09:58 Home
-rw-f--r--    1 root     root   1791 Mar 29 09:58 Start Here
drwx------    2 root     root   4096 Mar 29 09:58 Trash
[root@server1 ~]# _

Just as the chown (change owner) command can be used to change the owner of a file or directory, you can use the chgrp (change group) command to change the group owner of a file or directory. The chgrp command takes two arguments at minimum: the new group owner and the files or directories to change. As with the chown command, the chgrp command also accepts the -R option to change group ownership recursively throughout the directory tree. To change the group owner of file1 and the Desktop directory recursively throughout the directory tree, you can execute the following commands:

```
[root@server1 ~]# chgrp sys file1
[root@server1 ~]# chgrp -R sys Desktop
[root@server1 ~]# ls -1
```
total 4
drwx------    3 root     sys    4096 Apr 8 07:12 Desktop
-rw-f--r--    1 root     sys      0 Apr 29 15:40 file1
[root@server1 ~]# ls -l Desktop
total 16
-rw-------    1 root     sys     163 Mar 29 09:58 Floppy
-rw-f--r--    1 root     sys    3578 Mar 29 09:58 Home
-rw-f--r--    1 root     sys    1791 Mar 29 09:58 Start Here
drwx------    2 root     sys    4096 Mar 29 09:58 Trash
[root@server1 ~]# _

Regular users can change the group of a file or directory only to a group to which they belong.

Normally, you change both the ownership and group ownership on a file when that file needs to be maintained by someone else. As a result, you can change both the owner and the group owner at the same time using the `chown` command. To change the owner to user1 and the group owner to root for file1 and the directory Desktop recursively, you can enter the following commands:

```
[root@server1 ~]# chown user1.root file1
[root@server1 ~]# chown -R user1.root Desktop
[root@server1 ~]# ls -1
total 4
drwx------  3 user1 root  4096 Apr  8 07:12 Desktop
-rw-f--r--  1 user1 root    0 Apr 29 15:40 file1
[root@server1 ~]# ls -l Desktop
total 16
-rw-------  1 user1 root    163 Mar 29 09:58 Floppy
-rw-f--r--  1 user1 root   3578 Mar 29 09:58 Home
-rw-f--r--  1 user1 root   1791 Mar 29 09:58 Start Here
drwx------  2 user1 root  4096 Mar 29 09:58 Trash
[root@server1 ~]# _
```

Note that there must be no spaces before and after the . character in the chown commands shown in the preceding output.

You can also use the : character instead of the . character in the chown command to change both the owner and group ownership (e.g., chown -R user1:root Desktop).

To protect your system’s security, you should ensure that most files residing in a user’s home directory are owned by that user; some files in a user’s home directory (especially the hidden files and directories) require this to function properly. To change the ownership back to the root user for file1 and the Desktop directory to avoid future problems, you can type the following:

```
[root@server1 ~]# chown root.root file1
[root@server1 ~]# chown -R root.root Desktop
[root@server1 ~]# ls -1
total 4
drwx------  3 root  root  4096 Apr  8 07:12 Desktop
-rw-f--r--  1 root  root    0 Apr 29 15:40 file1
[root@server1 root]# ls -l Desktop
total 16
-rw-------  1 root  root    163 Mar 29 09:58 Floppy
-rw-f--r--  1 root  root   3578 Mar 29 09:58 Home
-rw-f--r--  1 root  root   1791 Mar 29 09:58 Start Here
drwx------  2 root  root   4096 Mar 29 09:58 Trash
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_182_0.png)

You can override who is allowed to change ownership and permissions using a system setting. Many Linux distributions, including Fedora 20 Linux, use this system setting by default to restrict regular (non-root) users from changing the ownership and group ownership of files and directories. This prevents these users from bypassing disk quota restrictions, which rely on the ownership of files and directories to function properly. Disk quotas are discussed in Chapter 5.

## Managing File and Directory Permissions

Every file and directory file on a Linux filesystem contains information regarding permissions in its inode. The section of the inode that stores permissions is called the **mode** of the file and is divided into three sections based on the user(s) who receive(s) the permissions to that file or directory:

- User (owner) permissions
- Group (group owner) permissions
- Other (everyone else on the Linux system) permissions

Furthermore, you can assign to each of these users the following regular permissions:

- Read
- Write
- Execute

## Interpreting the Mode

Recall that the three sections of the mode and the permissions that you can assign to each section are viewed when you perform an ls -l command; a detailed depiction of this is shown in Figure 4-3. It is important to note that the root user supersedes all file and directory permissions; in other words, the root user has all permissions to every file and directory regardless of what the mode of the file or directory indicates.

![](img/c27875544958897d817484d558c208c8_182_1.png)

**Figure 4-3 The structure of a mode**

Consider the root user's home directory listing, shown in the following example:

```
[root@server1 ~]# ls -l
total 28
drwx------    3 root     root     4096 Apr  8 07:12 Desktop
-r--w--x     1 bob      proj       282 Apr 29 22:06 file1
----------    1 root     root        82 Apr 29 22:06 file2
-rwxrwxrwx    1 root     root        82 Apr 29 22:06 file3
----------    1 root     root        82 Apr 29 22:06 file4
-rw-f--r--    1 root     root       282 Apr 29 22:06 file5
-rw-f--r--    1 user1    sys        282 Apr 29 22:06 file6
[root@server1 ~]# _
```

Note from the preceding output that all permissions (as shown in Figure 4-3) need not be on a file or directory; if the permission is unavailable, a dash (the hyphen character on your keyboard, - ) replaces its position in the mode. Be certain not to confuse the character to the left of the mode (which determines the file type) with the mode, as it is unrelated to the permissions on the file or directory. From the preceding output, the Desktop directory gives the user or owner of the directory (the root user) read, write, and execute permission, yet members of the group (the root group) do not receive any permissions to the directory. Note that other (everyone on the system) does not receive permissions to this directory either.

Permissions are not additive; the system assigns the first set of permissions that are matched in the mode order: user, group, other. Let us assume that the bob user is a member of the proj group. In this case, the file called file1 in the preceding output gives the user or owner of the file (the bob user) read permission, gives members of the group (the proj group) write permission, and gives other (everyone else on the system) execute permission only. Because permissions are not additive, the bob user will only receive read to file1 from the system.

Linux permissions should not be assigned to other only. Although file2 in our example does not give the user or group any permissions, all other users receive read, write, and execute permission via the other category. Thus, file2 should not contain sensitive data because many users have full access to it. For the same reason, it is bad form to assign all permissions to a file that contains sensitive data, as shown with file3 in the preceding example.

On the contrary, it is also possible to have a file that has no permissions assigned to it, as shown in the preceding example with respect to file4. In this case, the only user who has permissions to the file is the root user.

The permission structure that you choose for a file or directory might result in too few or too many permissions. You can follow some general guidelines to avoid these situations. The owner of a file or directory is typically the person who maintains it; members of the group are typically users in the same company department and must have limited access to the file or directory. As a result, most files and directories that you find on a Linux file system have more permissions assigned to the user of the file/directory than to the group of the file/directory, and the other category has either the same permissions or less than the group of the file/directory, depending on how private that file or directory is. The file file5 in the previous output depicts this common permission structure. In addition, files in a user's home directory are typically owned by that user; however, you might occasionally find files that are not. For these files, their permission definition changes, as shown in the previous example with respect to file1 and file6. The user or owner of file6 is user1, who
