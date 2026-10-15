
## 23.9.3.3 使用 ACL 继承模式修改 ACL 继承

本节介绍`aclinherit`属性的值，以下命令行示例演示了将 ACL 继承模式设置为`discard`时的 ACL 继承情况。如果将文件系统上的 ZFS `aclinherit`属性设置为`discard`，则在目录权限位更改时，ACL 可能会被丢弃。

```
# zfs set aclinherit=discard tank/usr/home/bob
# mkdir test5.dir
# setfacl -m user:bob:read_data/write_data/execute:dir_inherit:allow test5.dir
# getfacl test5.dir
# file: test5.dir
# owner: bob
# group: bob
user:bob:rwx------------d----:allow
owner@:rwxp--aARWcCos:------:allow
group@:r-x---a-R-c-s:------:allow
everyone@:r-x---a-R-c-s:------:allow
```

如果之后您决定收紧目录上的权限位，则非平凡 ACL 将被丢弃。例如：

```
# chmod 744 test5.dir
# getfacl test5.dir
# file: test5.dir
# owner: bob
# group: bob
owner@:rwxp--aARWcCos:------:allow
group@:r-x---a-R-c-s:------:allow
everyone@:r-x---a-R-c-s:------:allow
```

最后，我们将演示将 ACL 继承模式设置为`noallow`时的 ACL 继承。

在下面的 ACL 中（允许`read_data`），设置了两个带有文件继承的非平凡 ACL。一个 ACL 允许`read_data`权限，另一个 ACL 拒绝`read_data`权限。同样，您必须将数据集名称从`tank/usr/home/bob`更改为您系统中正在使用的任何 ZFS 数据集，并以超级用户身份执行`zfs set`命令。

```
# zfs set aclinherit=noallow tank/usr/home/bob
# mkdir test6.dir
# setfacl -m user:bob:read_data:file_inherit:deny test6.dir
# setfacl -m user:mansoor:read_data:file_inherit:allow test6.dir
# getfacl test6.dir
# file: test6.dir
# owner: bob
# group: bob
user:mansoor:r-----------------:f----:allow
user:bob:r-----------------:f----:deny
owner@:rwxp--aARWcCos:------:allow
group@:r-x---a-R-c-s:------:allow
everyone@:r-x---a-R-c-s:------:allow
```

如下示例所示，当创建新文件时，允许用户`mansoor`具有读取数据权限的 ACL 被丢弃。

```
% touch test6.dir/file.6
% getfacl test6.dir/file.6
# file: test6.dir/file.6
# owner: bob
# group: bob
user:bob:r----:------:------:deny
owner@:rw-p--aARWcCos:------:allow
group@:r----a-R-c-s:------:allow
everyone@:r----a-R-c-s:------:allow
```
