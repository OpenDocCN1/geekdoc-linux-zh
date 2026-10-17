
user:mansoor:r--------:------:I:allow

owner@:rw-p--aARWcCos:------:allow

group@:r-x---a-R-c-s:------:allow

everyone@:r----a-R-c-s:------:allow

在这些示例中，由于父目录对 `group@` 和 `everyone@` 的权限位拒绝了写和执行权限，因此用户 `mansoor` 被拒绝写和执行权限。默认的 `aclinherit` 属性为 `restricted`，这意味着 `write_data` 和 `execute` 权限不会被继承。

在以下示例中，用户 `mansoor` 被授予对新创建的文件进行继承的读、写和执行权限，但不会传播到目录的后续内容。

```
root@solaris_11_3:~# mkdir test4.dir
root@solaris_11_3:~# chmod A+user:mansoor:rwX:fn:allow test4.dir
root@solaris_11_3:~# ls -dV test4.dir
```

drwxr-xr-x+ 2 root root 2 Nov 4 12:33 test4.dir

user:mansoor:rwX---------:f--n--:allow

owner@:rwxp--DaARWcCos:------:allow

group@:r-x---a-R-c-s:------:allow

everyone@:r-x---a-R-c-s:------:allow

如下例所示，`mansoor` 的 `read_data`/`write_data`/`execute` 权限会根据拥有组权限而降低。

```
root@solaris_11_3:~# touch test4.dir/file.4
root@solaris_11_3:~# ls -V test4.dir/file.4
```

-rw-r--r--+ 1 root root 0 Nov 4 12:35 test4.dir/file.4

user:mansoor:r-----:------:------:------:allow

owner@:rw-p-aARWcCos:------:allow

group@:r--a-R-c-s-:------:allow

everyone@:r-----a-R-c-s:------:allow

## 24.5.3.3 使用 ACL 继承模式修改 ACL 继承

本节描述了 `aclinherit` 属性值。

### ACL 继承模式设置为 discard 时的 ACL 继承

如果文件系统的 `aclinherit` 属性设置为 `discard`，则在目录权限位更改时 ACL 可能会被丢弃。例如：

```
root@solaris_11_3:~# zfs set aclinherit=discard rpool/export/home/bob
root@solaris_11_3:~# mkdir test5.dir
root@solaris_11_3:~# chmod A+user:mansoor:rwX:d:allow test5.dir
root@solaris_11_3:~# ls -dV test5.dir
```

drwxr-xr-x+ 2 root root 2 Nov 4 12:37 test5.dir

user:mansoor:rwX------:------:d-----:allow

owner@:rwxp-DAARWcCos:------:allow

group@:r-x---a-R-c-s-:------:allow

everyone@:r-x---a-R-c-s:------:allow

如果在稍后时间决定收紧目录的权限位，则非平凡 ACL 将被丢弃。例如：

```
root@solaris_11_3:~# chmod 744 test5.dir
root@solaris_11_3:~# ls -dV test5.dir
```

drwxr--r--+ 2 root root 2 Nov 4 12:37 test5.dir

user:mansoor:r-----:------:d-----:allow

owner@:rwxp-DAARWcCos:------:allow

group@:r---a--R-c-s-:------:allow

everyone@:r-----a-R-c-s:------:allow

### ACL 继承模式设置为 noallow 时的 ACL 继承

在以下示例中，设置了两个具有文件继承的非平凡 ACL。一个 ACL 允许 `read_data` 权限，一个 ACL 拒绝 `read_data` 权限。此示例还说明了如何在一个 `chmod` 命令中指定两个 ACE。

```
root@solaris_11_3:~# zfs set aclinherit=noallow rpool/export/home/bob
```

```
root@solaris_11_3:# mkd test6.dir
root@solaris_11_3:# chmod A+user:mansoor:r:f:deny,user:bob:r:f:allow test6.dir
root@solaris_11_3:# ls -dV test6.dir
```

drwx--xr-x 2 root root 2 Nov 4 12:45 test6.dir

user:mansoor:r----------------:f------:deny

owner@rwxp:DaARwcCos:------:allow

group@r-x---a-R-c-s:------:allow

everyone@r-x---a-R-c-s:------:allow

正如以下示例所示，当创建新文件时，允许读取数据权限的 ACL 会被丢弃。

```
root@solaris_11_3:# touch test6.dir/file.6
root@solaris_11_3:# ls -V test6.dir/file.6
```

-rw-r--r-- 1 root root 0 Nov 4 12:49 test6.dir/file.6

user:mansoor:r----------------:f------:deny

owner@rw-p--aARwcCos:------:allow

group@r-x---a-R-c-s:------:allow

everyone@r-x---a-R-c-s:------:allow
