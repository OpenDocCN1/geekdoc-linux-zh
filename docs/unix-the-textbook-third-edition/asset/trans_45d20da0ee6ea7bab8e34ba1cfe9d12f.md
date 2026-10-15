
用户 sarwar 可以在此主机上运行以下命令：

```
(root) ALL
(admin) ALL
(root) /usr/sbin/visudo
```

这是 Solaris 系统 sudoers 文件中的一条条目；其中 dgb 可以是在 sudoers 文件中定义的、包含多个用户的别名，指定用户 dgb 可以运行 /bin/ls、/bin/kill 和 /usr/bin/lprm——但仅能以 operator 用户的身份在主机 solaris11_2 上运行。

```
dgb solaris11_2 = (operator) /bin/ls, /bin/kill, /usr/bin/lprm
```

在 Solaris 上使用组名的示例：在服务器 solaris11_2 上，man 组中的所有成员都可以以 database 用户的身份运行 /opt/bin 中的所有命令：

```
%man solaris11_2 = (database) /opt/bin/*
```

在 sudoers 文件中使用用户 ID 号，允许 PC-BSD 系统上 ID 为 1002 的用户运行 /usr/local/sbin 目录中的所有内容：

```
#1002 ALL = /usr/local/sbin/*
```

要查看更多示例，并获取 sudo 命令的完整参考，请在您的系统上使用 sudo 的手册页。

## 23.9.3 在 PC-BSD 中使用访问控制列表（ACL）

与传统的 UNIX 权限模型（通过 read、write、execute 等权限来定义对文件或目录等对象的安全访问）不同，访问控制列表（ACL）模型让用户群体能够对对象安全进行更细粒度的控制。

在权限模型中，组权限是文件所有者将访问权限委派给用户群中不同群体的唯一方式。这是因为任何文件只能属于一个组。因此，为了服务不同的群体，必须存在许多不同的组。只有管理员才能创建和分配组成员资格。而且，在使用权限模型时，协作项目团队之间的文件共享变得难以为继。

ACL 提供了更大的自主裁量权，但代价是更高的复杂性、更大的存储需求，以及底层文件系统（无论是 UFS 还是 ZFS）性能的下降。我们的两个基于 UNIX 的系统，PC-BSD 和 Solaris，都使用 ZFS，支持权限模型和 ACL 模型（此处称为 NFSv4）。由于存在多种 ACL 模型，这里值得指出的是，ZFS 仅支持 NFSv4 ACL。

我们在第 5 章 5.4 节中展示了权限模型。本节展示的方法适用于 PC-BSD 的 ZFS 文件。在第 24 章第 5 节中，我们展示了在 Solaris 系统上管理 ZFS 文件和目录 ACL 的更高级、更详细的方法。

一个非平凡的条目可能如下例所示，其中权限被专门授予用户 mansoor：

```
0:user:mansoor:read_data/write_data:file_inherit:allow
```

### 23.9.3.1.2 ACL 条目描述：NFSv4 ACL 命令条目描述的组成部分

下面描述应用于文件和目录的 setfacl 命令的语法组成部分（包括一般和特定部分）。我们还将展示执行示例后 getfacl 命令输出的一般形式：

| | 命令 | 授予对象 | 权限 | 作用对象 |
| --- | --- | --- | --- | --- |
| 文件 | setfacl -a 0 | user:bob | rwx------:----:allow | 文件名 |
| 目录 | setfacl -a 0 | user:bob | r------:fd--:allow | 目录名 |

图例：

- a - 命令
- b - 选项
- c - 位置选项参数，从 0 开始，不能是末尾的数字！
- d - ACL 标记
- e - ACL 限定符，在这些情况下为用户
- f - 14 项权限，使用短格式，连字符（-）可选
- g - 6 个继承标志，仅用于目录，连字符（-）可选
- h - ACL 类型，允许或拒绝
- i - 命令参数，即文件名或目录名规范

前一个文件命令的 getfacl 输出格式：

```
%getfacl filename
#file: filename
#owner: owner name
#group: group name
position 0 user:bob:rwx------:-----:allow
position 1 owner@-----------------------------------------
position 2 group@-----------------------------------------
position 3 everyone@-------------------------------------
```

使用下面附加的示例条目作为组成 ACL 条目的各元素的参考。这些元素同时适用于简单和复杂的 ACL。

```
user:mansoor:read_data/write_data:file_inherit:allow
```

