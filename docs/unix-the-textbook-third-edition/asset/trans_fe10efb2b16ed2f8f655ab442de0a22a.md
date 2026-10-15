

## 表 24.2 ACL 访问权限

| 访问权限 | 紧凑访问权限 | 描述 |
|---|---|---|
| add_file | w | 允许向目录添加新文件的权限 |
| add_subdirectory | p | 在目录上，创建子目录的权限 |
| append_data | p | 仅从 EOF 开始修改文件的权限 |
| delete | d | 删除文件的权限 |
| delete_child | D | 删除目录内文件或目录的权限 |
| execute | x | 执行文件或搜索目录内容的权限 |
| list_directory | r | 列出目录内容的权限 |
| read_acl | c | 读取 ACL 的权限（ls） |
| read_attributes | a | 读取文件的基本属性（非 ACL）的权限 |
| read_data | r | 读取文件内容的权限 |
| read_xattr | R | 读取文件的扩展属性的权限 |
| synchronize | s | 以同步的读写操作在服务器本地访问文件的权限 |
| write_xattr | W | 创建扩展属性或写入扩展属性目录的权限 |
| write_data | w | 修改或替换文件内容的权限 |
| write_attributes | A | 将文件或目录的时间更改为任意值的权限 |
| write_acl | C | 写入 ACL 或使用 chmod 命令修改 ACL 的权限 |
| write_owner | o | 更改文件的所有者或组；或在文件上执行 chown 或 chgrp 命令的能力 |

## 表 24.3 ACL delete 和 delete_child 权限行为

| 父目录权限 | 目标对象权限 | |
|---|---|---|
| ""（空） | ACL 允许 Delete | ACL 拒绝 Delete | Delete 权限未指定 |
| ACL 允许 delete_child | 允许 | 允许 | 允许 |
| ACL 拒绝 delete_child | 允许 | 拒绝 | 拒绝 |
| ACL 仅允许写和执行 | 允许 | 允许 | 允许 |
| ACL 拒绝写和执行 | 允许 | 拒绝 | 拒绝 |

表 24.3 提供了有关 ACL delete 和 delete_child 行为的更多详细信息。

### 24.5.1.2.1 ZFS ACL 集合

ACL 集合由 ACL 权限的组合组成。这些 ACL 集合是预定义的，不能修改。

ACL 集合名称    包含的 ACL 权限
full_set        所有权限

```
modify_set  All permissions except write_acl and write_owner
read_set    read_data,read_attributes,read_xattr,read_acl
write_set   write_data,append_data,write_attributes,write_xattr
```

你可以应用一个 ACL 集合，而不必分别设置各个权限。例如，授予 mansoor read_set ACL 集合的权限可让他读取 ACL 以及文件内容及其基本和扩展属性。

```
# chmod A=user:mansoor:read_set:allow file.0
# ls -V file.0
-r--r--r-- 1 root root 206695 Jul 20 13:43 file.0
0:user:mansoor:read_data/read_xattr/read_attributes/read_acl:allow
...
```

### 24.5.1.3 ACL 继承

ACL 继承意味着新创建的文件或目录可以继承它们 intended 要继承的 ACL，而不会忽略父目录上现有的权限位。默认情况下，ACL 不会传播。如果你在一个目录上设置了非平凡的 ACL，它不会被任何后续目录继承。你必须指定文件或目录上 ACL 的继承。

表 24.4 描述了可选的继承标志。

此外，你还可以使用 ZFS aclinherit 文件系统属性在文件系统上设置更严格或更宽松的默认 ACL 继承策略。有关此属性的更多信息，请参阅第 24.5.1.4 节，“ACL 属性”。

有关在 ZFS 文件上设置 ACL 继承的更多信息，请参阅第 24.5.3 节，“在 ZFS 文件上设置 ACL 继承”。

## 表 24.4 ACL 继承标志

| 继承标志 | 紧凑继承标志 | 描述 |
|---|---|---|
| file_inherit | f | 仅将 ACL 从父目录继承到目录的文件 |
| dir_inherit | d | 仅将 ACL 从父目录继承到目录的子目录 |
| inherit_only | I | 继承父目录的 ACL |
| no_propagate | n | 仅将 ACL 从父目录继承到目录的第一级内容 |
| - | n/a | 未授予权限 |
| successful_access | S | 指示在成功访问时是否应启动警报或审计记录；与 audit 或 alarm ACE 类型一起使用 |
| failed_access | F | 指示在访问失败时是否应启动警报或审计记录；与 audit 或 alarm ACE 类型一起使用 |
| inherited | I | 指示 ACE 是继承的 |

