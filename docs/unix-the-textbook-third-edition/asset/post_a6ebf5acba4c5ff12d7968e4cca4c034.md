
root@solaris_11_3:~# chmod A2- file.2
root@solaris_11_3:~# ls -V file.2
-rw-r-----+ 1 root root        0 Nov  4 12:09 file.2
    owner@:r-w-p-aARWcCos:------:allow
    group@:r-----a-R-c-s:------:allow

In the next example, the ACL is replaced with just read_data/write_data permissions for everyone@ on file.2. No owner@ or group@ ACL entry exists to override the permissions for owner and group. So the permission bits become 666.

```
root@solaris_11_3:~# chmod A=everyone@:rw::allow file.2
root@solaris_11_3:~# ls -V file.2
-rw-rw-rw+ 1 root root        0 Nov  4 12:09 file.2
    everyone@:rw:----------:------:allow
```

Notice that all other ACL entries have been removed.

In the next example, the ACL is replaced with read permissions just for user mansoor. The command, however, leaves no trivial ACL entries. Consequently, the permission bits are set to 000, which denies mansoor access to file.2. The file effectively becomes inaccessible.

```
root@solaris_11_3:~# chmod A=user:mansoor:r::allow file.2
root@solaris_11_3:~# ls -V file.2
--------- + 1 root root        0 Nov  4 12:09 file.2
    user:mansoor:r:--------:------:allow
```

Notice in the ls -V output that no trivial ACL entries exist.

The next example shows how setting permission bits also updates the ACL. The bits for file.2 are set to 655. Automatically, default trivial ACL permissions are set.

```
root@solaris_11_3:~# chmod 655 file.2
root@solaris_11_3:~# ls -V file.2
-rw-r-xr-x 1 root root        0 Nov  4 12:09 file.2
    owner@:---x:----------:------:deny
    owner@:rw-p-aARWcCos:------:allow
    group@:r-x---a-R-c-s:------:allow
    everyone@:r-x---a-R-c-s:------:allow
```

```
root@solaris_11_3:~# ls -lV file.1
-rw-rw-r--+ 1 root root 0 Nov 4 11:58 file.1
user:mansoor:r-x----------:--------:allow
user:bob:r-----a-R-c--:--------:allow
owner@:rw-p--aARWcCos:--------:allow
group@:rw----------:--------:allow
everyone@:r-----a-R-c-s:--------:allow
```

A chown operation changes file.1's ownership to bob and the group staff.

```
root@solaris_11_3:~# chown bob:staff file.1
```

Bob then changes file.1's permission bits to 640. Because of the ACL properties that were previously set, the permissions for the groups in the ACL are reduced in order to not exceed the permissions of the owning group staff. Please notice how bob drops out of the superuser role to accomplish the following:

```
root@solaris_11_3:~# su - bob
Oracle Corporation SunOS 5.11 11.3 September 2015
bob@solaris_11_3:~$ ls -lV file.1
-rw-rw-r--+ 1 bob staff 0 Nov 4 11:58 file.1
user:mansoor:r-x----------:--------:allow
user:bob:r-----a-R-c--:--------:allow
owner@:rw-p--aARWcCos:--------:allow
group@:rw----------:--------:allow
everyone@:r-----a-R-c-s:--------:allow
bob@solaris_11_3:~$ chmod 640 file.1
```

```
bob@solaris_11_3:~$ ls -lV file.1
-rw-r-----+ 1 bob staff 0 Nov 4 11:58 file.1
user:mansoor:r-x----------:--------:allow
user:bob:r-----a-R-c--:--------:allow
owner@:rw-p--aARWcCos:--------:allow
group@:r-----a-R-c-s:--------:allow
everyone@:------a-R-c-s:--------:allow
```

Bob then changes the permission bits to 770. Consequently, the permissions of the groups in the ACL are also changed to match the permission of the owning group staff.

```
bob@solaris_11_3:~$ chmod 770 file.1
bob@solaris_11_3:~$ ls -lV file.1
-rwxrwx---+ 1 bob staff 0 Nov 4 11:58 file.1
user:mansoor:r-x----------:--------:allow
user:bob:r-----a-R-c--:--------:allow
owner@:rwxp--aARWcCos:--------:allow
group@:rwxp--aARWc--s:--------:allow
everyone@:------a-R-c-s:--------:allow
```

## 24.5.3 Setting ACL Inheritance on ZFS Files

You can determine how ACLs are inherited on files and directories. The aclinherit property can be set globally on a file system. By default, aclinherit is set to restricted.

### 24.5.3.1 Granting ACLs That Are Inherited by Files

This section identifies the file ACEs that are applied when the file_inherit flag is set.

In the following example, read_data/write_data permissions are added for files in the test2.dir directory for user mansoor so that he has read access on any newly created files. Also notice the switch back to superuser.

```
bob@solaris_11_3:~$ su
Password:xxx
root@solaris_11_3:# mkdir test2.dir
root@solaris_11_3:# chmod A=user:mansoor:rw:f:allow test2.dir
root@solaris_11_3:# ls -dV test2.dir
drwxr-xr-x+ 2 root root 2 Nov 4 12:23 test2.dir
    user:mansoor:rw-------:f------:allow
    owner@:rwxp--DaARWcCos:------:allow
    group@:r-x---a-R-c-s:------:allow
    everyone@:r-x---a-R-c-s:------:allow
```

In the following example, user mansoor's permissions are applied on the newly created test2.dir/file.2 file. The ACL inheritance granted, read_data:file_inherit:allow, means user mansoor can read the contents of any newly created file.

```
root@solaris_11_3:# touch test2.dir/file.2
root@solaris_11_3:# ls -V test2.dir/file.2
-rw-r--r--+ 1 root root 0 Nov 4 12:26 test2.dir/file.2
    user:mansoor:r--------:------:I:allow
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s:------:allow
    everyone@:r-----a-R-c-s:------:allow
```

Because the aclinherit property for this file system is set to the default mode, restricted, user mansoor does not have write_data permission on file.2 because the group permission of the file does not allow it.

The inherit_only permission, which is applied when the file_inherit or dir_inherit flags are set, is used to propagate the ACL through the directory structure. As such, user mansoor is granted or denied permission from everyone@ permissions only if he is the file owner or is a member of the file's group owner. For example:

```
root@solaris_11_3:# mkdir test2.dir/subdir.2
root@solaris_11_3:# ls -dV test2.dir/subdir.2
drwxr-xr-x+ 2 root root 2 Nov 4 12:27 test2.dir/subdir.2
user:mansoor:rw----------:f-i--I:allow
    owner@:rwxp--DaARWcCos:------:allow
```
