
```
Files      chmod A0+user:bob:rwx---------:-----:allow filename

Directories chmod A0+user:bob:r--------:fd----:allow dirname
```

图例：

- a. 设置 ACL 条目的`chmod`命令
- b. 选项`A`
- c. 位置选项参数，从`0`开始；也作为条目的索引
- d. 操作符选项参数，`+`表示添加，`=`表示替换
- e. ACL 标记，在这些情况下是`user`，即 ACL 条目类型的第一部分
- f. ACL 限定符，在这些情况下是`bob`，即 ACL 条目类型的第二部分
- g. 14 个权限，以短形式显示，其余可选
- h. 7 个继承标志，仅用于目录，其余可选
- i. ACL 类型，`allow`或`deny`
- j. 命令参数，文件名或目录名规范

### 上述文件命令的 `ls -V` 输出格式

```
%ls -V filename

traditional permissions header

    user:bob:rw-------:-------:allow filename

    owner@ ----------default------------------

    group@ ----------default------------------

    everyone@ ----------default------------------
```

使用以下示例条目作为参考，以理解构成 ACL 条目的各个元素。这些元素同时适用于平凡 ACL 和非平凡 ACL。

```
0:user:mansoor:read_data/write_data:file_inherit:allow
```

**索引：** 条目开头的数字，例如示例中的数字零 (`0`)。索引标识特定条目，并将其与 ACL 中的其他条目区分开来。索引出现在 `ls -V` 命令给出的 ACL 条目长格式输出中。

**ACL 条目类型：** 用户类别。在平凡 ACL 中，仅设置 `owner@`、`group@` 和 `everyone@` 的条目。在非平凡 ACL 中，会添加 `user:username` 和 `group:groupname`。在示例中，条目类型是 `user:mansoor`。

**访问权限：** 授予或拒绝给该条目类型的权限。在示例中，用户 `mansoor` 的权限是 `read_data` 和 `write_data`。

**继承标志：** 可选的 ACL 标志列表，用于控制权限在目录结构中向下传播的方式。在示例条目中，`file_inherit` 也被授予用户 `mansoor`。

**权限控制类型：** 决定条目中的权限是允许还是拒绝。在示例中，`mansoor` 的权限是允许的。

表 24.1 描述了每种 ACL 条目类型。表 24.2 描述了 ACL 访问权限。

### 表 24.1 ACL 条目类型

| ACL 条目类型 | 描述 |
|---|---|
| `owner@` | 指定授予对象所有者的访问权限 |
| `group@` | 指定授予对象所属组的访问权限 |
| `everyone@` | 指定授予不匹配任何其他 ACL 条目的任何用户或组的访问权限 |
| `user` | 带有用户名时，指定授予对象附加用户的访问权限 |
| `group` | 带有组名时，指定授予对象附加组的访问权限 |

### 表 24.2 ACL 访问权限

| 访问权限 | 紧凑访问权限 | 描述 |
|---|---|---|
| `add_file` | `w` | 允许向目录添加新文件的权限 |
| `add_subdirectory` | `p` | 在目录上，创建子目录的权限 |
| `append_data` | `p` | 仅从 EOF 开始修改文件的权限 |
| `delete` | `d` | 删除文件的权限 |
| `delete_child` | `D` | 删除目录内文件或目录的权限 |
| `execute` | `x` | 执行文件或搜索目录内容的权限 |
| `list_directory` | `r` | 列出目录内容的权限 |
| `read_acl` | `c` | 读取 ACL 的权限（`ls`） |
| `read_attributes` | `a` | 读取文件的基本属性（非 ACL）的权限 |
| `read_data` | `r` | 读取文件内容的权限 |
| `read_xattr` | `R` | 读取文件的扩展属性的权限 |
| `synchronize` | `s` | 以同步的读写操作在服务器本地访问文件的权限 |
| `write_xattr` | `W` | 创建扩展属性或写入扩展属性目录的权限 |
| `write_data` | `w` | 修改或替换文件内容的权限 |
| `write_attributes` | `A` | 将文件或目录的时间更改为任意值的权限 |
| `write_acl` | `C` | 写入 ACL 或使用 `chmod` 命令修改 ACL 的权限 |
| `write_owner` | `o` | 更改文件的所有者或组；或在文件上执行 `chown` 或 `chgrp` 命令的能力 |

### 表 24.3 ACL `delete` 和 `delete_child` 权限行为

| 父目录权限 | 目标对象权限 | | |
|---|---|---|---|
| ""（空） | ACL 允许 `delete` | ACL 拒绝 `delete` | `delete` 权限未指定 |
| ACL 允许 `delete_child` | 允许 | 允许 | 允许 |
| ACL 拒绝 `delete_child` | 允许 | 拒绝 | 拒绝 |
| ACL 仅允许写和执行 | 允许 | 允许 | 允许 |
| ACL 拒绝写和执行 | 允许 | 拒绝 | 拒绝 |

表 24.3 提供了有关 ACL `delete` 和 `delete_child` 行为的更多详细信息。

### 24.5.1.2.1 ZFS ACL 集合

ACL 集合由 ACL 权限的组合组成。这些 ACL 集合是预定义的，不能修改。

| ACL 集合名称 | 包含的 ACL 权限 |
|---|---|
| `full_set` | 所有权限 |
| `modify_set` | All permissions except `write_acl` and `write_owner` |
| `read_set` | `read_data`, `read_attributes`, `read_xattr`, `read_acl` |
| `write_set` | `write_data`, `append_data`, `write_attributes`, `write_xattr` |

你可以应用一个 ACL 集合，而不必分别设置各个权限。例如，授予 `mansoor` `read_set` ACL 集合的权限可让他读取 ACL 以及文件内容及其基本和扩展属性。

```
# chmod A=user:mansoor:read_set:allow file.0
# ls -V file.0
-r--r--r-- 1 root root 206695 Jul 20 13:43 file.0
0:user:mansoor:read_data/read_xattr/read_attributes/read_acl:allow
...
```
