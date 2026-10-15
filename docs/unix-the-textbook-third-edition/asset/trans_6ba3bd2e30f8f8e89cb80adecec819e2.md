

root@solaris_11_3:~# chmod A2- file.2
root@solaris_11_3:~# ls -V file.2
-rw-r-----+ 1 root root        0 Nov  4 12:09 file.2
    owner@:r-w-p-aARWcCos:------:allow
    group@:r-----a-R-c-s:------:allow

在下一个示例中，file.2 上的 ACL 被替换为仅针对 everyone@ 的 read_data/write_data 权限。不存在用于覆盖所有者和组权限的 owner@ 或 group@ ACL 条目。因此权限位变为 666。

```
root@solaris_11_3:~# chmod A=everyone@:rw::allow file.2
root@solaris_11_3:~# ls -V file.2
-rw-rw-rw+ 1 root root        0 Nov  4 12:09 file.2
    everyone@:rw:----------:------:allow
```

请注意，所有其他 ACL 条目都已被移除。

在下一个示例中，ACL 被替换为仅针对用户 mansoor 的读取权限。但是，该命令没有留下任何普通 ACL 条目。因此，权限位被设置为 000，这拒绝了 mansoor 对 file.2 的访问。该文件实际上变得无法访问。

```
root@solaris_11_3:~# chmod A=user:mansoor:r::allow file.2
root@solaris_11_3:~# ls -V file.2
--------- + 1 root root        0 Nov  4 12:09 file.2
    user:mansoor:r:--------:------:allow
```

请注意，在 `ls -V` 输出中不存在任何普通 ACL 条目。

下一个示例展示了设置权限位如何同时更新 ACL。file.2 的权限位被设置为 655。自动设置了默认的普通 ACL 权限。

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

一次 `chown` 操作将 file.1 的所有权更改为 bob，组更改为 staff。

```
root@solaris_11_3:~# chown bob:staff file.1
```

然后 Bob 将 file.1 的权限位更改为 640。由于之前设置的 ACL 属性，ACL 中组的权限被降低，以不超过所属组 staff 的权限。请注意 bob 如何退出超级用户角色来完成以下操作：

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

然后 Bob 将权限位更改为 770。因此，ACL 中组的权限也随之更改，以匹配所属组 staff 的权限。

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

## 24.5.3 在 ZFS 文件上设置 ACL 继承

您可以确定 ACL 如何在文件和目录上继承。`aclinherit` 属性可以在文件系统上全局设置。默认情况下，`aclinherit` 设置为 `restricted`。

### 24.5.3.1 授予由文件继承的 ACL

本节介绍在设置了 `file_inherit` 标志时应用的文件 ACE。

在以下示例中，为 test2.dir 目录中的文件添加了用户 mansoor 的 read_data/write_data 权限，以便他对任何新创建的文件具有读取权限。另请注意切换回超级用户。

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

在以下示例中，用户 mansoor 的权限被应用于新创建的 test2.dir/file.2 文件。所授予的 ACL 继承 `read_data:file_inherit:allow` 意味着用户 mansoor 可以读取任何新创建文件的内容。

```
root@solaris_11_3:# touch test2.dir/file.2
root@solaris_11_3:# ls -V test2.dir/file.2
-rw-r--r--+ 1 root root 0 Nov 4 12:26 test2.dir/file.2
    user:mansoor:r--------:------:I:allow
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s:------:allow
    everyone@:r-----a-R-c-s:------:allow
```

由于此文件系统的 `aclinherit` 属性设置为默认模式 `restricted`，用户 mansoor 对 file.2 没有 write_data 权限，因为文件的组权限不允许这样做。

`inherit_only` 权限在设置了 `file_inherit` 或 `dir_inherit` 标志时应用，用于通过目录结构传播 ACL。因此，用户 mansoor 仅当他是文件所有者或属于文件组所有者时，才会被授予或拒绝来自 everyone@ 的权限。例如：

```
root@solaris_11_3:# mkdir test2.dir/subdir.2
root@solaris_11_3:# ls -dV test2.dir/subdir.2
drwxr-xr-x+ 2 root root 2 Nov 4 12:27 test2.dir/subdir.2
user:mansoor:rw----------:f-i--I:allow
    owner@:rwxp--DaARWcCos:------:allow
```

