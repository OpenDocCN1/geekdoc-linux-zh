

## 访问确定

当上一个示例中的 ACL 扩展到包含特定用户和组的条目时，setfac 会自动提供一个合适的掩码：

```
$ ls -l /tmp/example
-rw-r-- 1 garth 0 Jun 14 15:57 /tmp/example
$ setfac -m user:trent:rwx,group:admin:rw /tmp/example
$ ls -l /tmp/example
-rw-r----+ 1 garth 0 Jun 14 15:57 /tmp/example
$ setfac --omit-header /tmp/example
```

在此处，Linux 版本的 setfac 生成的掩码允许 ACL 中授予的所有权限生效。如果你想手动设置掩码，可以将其包含在传递给 setfac 的 ACL 列表中，或者使用 `-n` 选项防止 setfac 重新生成它。（Solaris 版本的 setfac 默认不重新计算掩码条目；使用 `-r` 标志可以重新生成。）

请注意，在执行 `setfac` 命令后，`ls -l` 在文件模式末尾显示一个 `+` 号，表示它现在关联了一个真实的 ACL。第一个 `ls -l` 没有显示 `+`，是因为在那个点 ACL 是“最小化”的，它完全由 9 位模式描述，不需要单独存储。

如果你使用 `chmod` 命令对带有 ACL 的文件操作权限，请注意你的更改仅影响掩码。继续上上的示例：

```
$ chmod 770 /tmp/example
$ ls -l /tmp/example
-rwxrwx----+ 1 garth staff 0 Jun 14 15:57 /tmp/example
$ setfac --omit-header /tmp/example
```

`ls` 的输出具有误导性。尽管组权限看起来很慷慨，但由于组成员身份的原因，实际上没有人有权执行该文件。要授予此类权限，你必须编辑 ACL 本身。

## 访问确定

当进程尝试访问文件时，其有效 UID 将与文件的所有 UID 进行比较。如果它们相同，访问由 ACL 的 `user::` 权限决定。否则，如果存在匹配的特定用户 ACL 条目，权限将由该条目结合 ACL 掩码决定。

如果没有可用的特定用户条目，文件系统将尝试查找提供请求访问的有效组条目；这些条目与 ACL 掩码结合处理。如果未找到匹配的条目，则由 `other::` 条目生效。

## ACL 继承

除了表 6.8 列出的 ACL 条目类型外，目录的 ACL 还可以包含默认条目，这些条目会传播到其中新创建的文件和子目录的 ACL 中。子目录以活动 ACL 条目和默认条目的形式同时接收这两种条目。因此，原始默认条目可能会最终通过多层目录层次结构。

一旦默认条目被复制，父子 ACL 之间的连接就不会继续。如果父默认条目发生变化，更改不会反映在子目录的 ACL 中。

## NFSv4 ACL

在本节中，我们将讨论 NFSv4 ACL 的特性，并简要回顾用于检查它们的 Solaris 语法。AIX 也支持 NFSv4 ACL，但它使用不同的命令（`acget`, `aclpt`, `aclited` 等）来实现此目的。我们不将详述任何特定命令集的细节，而是专注于系统背后的理论。一旦熟悉理论，特定的命令很容易上手。

从结构角度来看，NFSv4 ACL 与 Windows ACL 相似。它们之间的主要区别在于访问控制条目所指实体的规范。

在两个系统中，ACL 都将此存储为字符串。对于 Windows ACL，该字符串通常包含 Windows 安全标识符 (SID)，而对于 NFSv4，字符串通常采用 `user:username` 或 `group:groupname` 的形式。它可以是特殊标记 `owner@`、`group@` 或 `everyone` 之一。这些条目是最常见的，因为它们对应每个文件中存在的模式位。

像 Samba 等在 UNIX 和 Windows 系统之间共享文件的系统提供了 Windows 和 NFSv4 主体之间的某种映射方法。

Windows 和 NFSv4 权限比传统的 UNIX 读执行模型更通用。主要改进如下：

- NFSv4 区分了在目录内创建文件的权限与创建子目录的权限。
- NFSv4 有一个独立的“追加”（append）权限位。
- NFSv4 对数据、文件属性、扩展属性和 ACL 分别有独立的读取和写入权限。
- NFSv4 通过标准控制用户更改文件所有权的能力。

表 6.9 显示了可以分配的各种权限：

| 代码 | 冗长名称 | 权限 |
| :--- | :--- | :--- |
| r | read_data | 数据 (文件) |
| w | write_data | 数据 (文件) |
| p | append_data | 数据 (文件) |
| R | read_xattr | 扩展属性 |
| W | write_xattr | 扩展属性 |
| D | delete | 扩展属性 |
| a | audit | 扩展属性 |
| A | alarm | 扩展属性 |
| d | delete child | 访问列表 |
| C | read_acl | 访问列表 |
| o | write_acl | 访问列表 |
| s | synchronize | 所有权 |

某些权限有多个名称，因为它们由传统系统表示。例如，传统系统中的 `x` 表示执行。

扩展属性是与文件一起存储的具命名数据块；大多数现代文件系统都支持此类属性，尽管它们并没有被广泛使用。

