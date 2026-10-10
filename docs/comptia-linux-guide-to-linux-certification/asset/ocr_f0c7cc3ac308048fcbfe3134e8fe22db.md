```
[root@server1 ~]# ls -l
total 12
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root root 4096 May 3 21:39 dir1
drwx------ 2 root root 4096 May 3 21:41 dir2
-rw-r--sr-x 1 root root 0 May 3 21:40 file1
-rw------- 1 root root 0 May 3 21:41 file2
[root@server1 ~]# chmod 1777 dir1
[root@server1 ~]# ls -l
total 12
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
drwxrwxrwt 2 root root 4096 May 3 21:39 dir1
drwx------ 2 root root 4096 May 3 21:41 dir2
-rw-r--sr-x 1 root root 0 May 3 21:40 file1
-rw------- 1 root root 0 May 3 21:41 file2
[root@server1 ~]#_
```

Also, remember that assigning special permissions without execute renders those permissions useless. For example, you may forget to give execute permission to either user, group, or other, and the long listing covers the execute permission with a special permission. In that case, the special permission is capitalized, as shown in the following example when dir2 is not given execute underneath the position in the mode that indicates the sticky bit (t):

```
[root@server1 ~]# ls -l
total 12
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
drwxrwxrwt 2 root root 4096 May 3 21:39 dir1
drwx------ 2 root root 4096 May 3 21:41 dir2
-rw-r--sr-x 1 root root 0 May 3 21:40 file1
-rw------- 1 root root 0 May 3 21:41 file2
[root@server1 ~]# chmod 1770 dir2
[root@server1 ~]# ls -l
total 12
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
drwxrwxrwt 2 root root 4096 May 3 21:39 dir1
drwxrwx--T 2 root root 4096 May 3 21:41 dir2
-rw-r--sr-x 1 root root 0 May 3 21:40 file1
-rw------- 1 root root 0 May 3 21:41 file2
[root@server1 ~]#
```

# Setting Custom Permissions in the Access Control List (ACL)

An access control list (ACL) is a list of users or groups that you can assign permissions to. As discussed earlier, the default ACL used in Linux consists of three entities: user, group, and other. However, there may be situations where you need to assign a specific set of permissions on a file or directory to an individual user or group.