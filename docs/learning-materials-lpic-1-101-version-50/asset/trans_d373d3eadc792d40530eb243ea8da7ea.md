

# 探索练习解答

- **1. 考虑 /etc/fstab 中的以下条目：** `/dev/sdc1 /backup ext4 noatime,nouser,async`。用户能否使用命令 `mount /backup` 来挂载此文件系统？为什么？
  - 不能，参数 `nouser` 将不允许普通用户挂载此文件系统。

- **2. 考虑一个挂载在 /mnt/server 的远程文件系统，由于网络连接中断而无法访问。如何强制将其卸载，或者如果无法卸载，如何将其挂载为只读？**
  - 传递 `-f` 和 `-r` 参数进行卸载。命令应为 `umount -f -r /mnt/server`。请记住，你可以将参数组合在一起，因此 `umount -fr /mnt/server` 也可以正常工作。

- **3. 编写一个 /etc/fstab 条目，以将标签为 Backup 的 btrfs 卷挂载到 /mnt/backup，使用默认选项，并且不允许从中执行二进制文件。**
  - 该行应为 `LABEL=Backup /mnt/backup btrfs defaults,noexec`

- **4. 考虑以下 systemd 挂载单元：**
  ```ini
  [Unit]
  Description=External data disk
  
  [Mount]
  What=/dev/disk/by-uuid/56C11DCC5D2E1334
  Where=/mnt/external
  Type=ntfs
  Options=defaults
  
  [Install]
  WantedBy=multi-user.target
  ```
  - 对于此文件系统，等效的 /etc/fstab 条目是什么？
  - 该条目应为：`UUID=56C11DCC5D2E1334 /mnt/external ntfs defaults`

- **5. 为了使 systemd 能够使用上述单元，文件名应该是什么？它应该放在哪里？**
  - 文件名必须与挂载点相同，因此应为 `mnt-external.mount`，放置在 `/etc/systemd/system` 中。

![](img/824749d5fc1d265354d0e66a01af9ced_490_0.png)

## 104.5 管理文件权限和所有权

### LPI 目标参考

LPIC-1 版本 5.0，考试 101，目标 104.5

### 权重

3

### 关键知识领域

- 管理普通文件、特殊文件以及目录的访问权限。
- 使用 suid、sgid 和粘滞位等访问模式来维持安全性。
- 了解如何更改文件创建掩码。
- 使用组字段授予组成员文件访问权限。

### 使用的文件、术语和实用工具的部分列表

- chmod
- umask
- chown
- chgrp

![](img/824749d5fc1d265354d0e66a01af9ced_491_0.png)

### 104.5 课程 1

| 证书 | LPIC-1 |
| :--- | :--- |
| 版本 | 5.0 |
| 主题 | 104 设备、Linux 文件系统、文件系统层次标准 |
| 目标 | 104.5 管理文件权限和所有权 |
| 课程 | 1 / 1 |

#### 简介

作为一个多用户系统，Linux 需要某种方式来追踪每个文件的所有者，以及用户是否被允许对文件执行操作。这是为了确保希望保持文件内容私密性的用户的隐私，同时也通过让某些文件对多个用户可访问来促进协作。

这是通过三级权限系统实现的。磁盘上的每个文件都归属于一个用户和一个用户组，并拥有三组权限：一组用于其所有者，一组用于拥有该文件的组，还有一组用于其他所有人。在本课程中，您将学习如何查询文件的权限，这些权限的含义以及如何操作它们。

#### 查询文件和目录的信息

命令 `ls` 用于获取任何目录内容的列表。在这种基本形式中，你只能看到文件名：

```
$ ls
Another_Directory  picture.jpg  text.txt
```

但每个文件都有更多可用的信息，包括其类型、大小、所有权等。要查看这些信息，你必须使用 `-l` 参数请求 `ls` 提供“长格式”列表：

```
$ ls -l
total 536
drwxrwxr-x 2 carol carol   4096 Dec 10 15:57 Another_Directory
-rw------- 1 carol carol  539663 Dec 10 10:43 picture.jpg
-rw-rw-r-- 1 carol carol    1881 Dec 10 15:57 text.txt
```

上述输出中的每一列都有特定含义。让我们看看与本课程相关的列。

- 列表中的 `第一` 列显示文件类型和权限。例如，在 `drwxrwxr-x` 中：
  - 第一个字符 `d` 表示文件类型。
  - 接下来的三个字符 `rwx` 表示文件 `所有者` 的权限，也被称为 `user` 或 `u`。
  - 接下来的三个字符 `rwx` 表示拥有该文件的 `组` 的权限，也被称为 `g`。
  - 最后三个字符 `r-x` 表示其他所有人的权限，也被称为 `others` 或 `o`。
    > 也很常见听到将 `others` 权限集称为 `world` 权限，意为“世界上其他所有人都有这些权限”。

- `第三` 和 `第四` 列显示所有权信息：分别是拥有该文件的用户和组。
- `第七` 列也就是最后一列显示文件名。

`第二` 列指示指向该文件的硬链接数量。`第五` 列显示文件大小。`第六` 列显示文件最后修改的日期和时间。但这些列与当前主题无关。

#### 目录呢？

如果你尝试使用 `ls -l` 查询目录的信息，它会显示目录内容的列表而不是目录本身的信息：

```
$ ls -l Another_Directory/
total 0
-rw-r-- 1 carol carol 0 Dec 10 17:59 another_file.txt
```

为了避免这种情况并查询目录本身的信息，请向 `ls` 添加 `-d` 参数：

```
$ ls -l -d Another_Directory/
drwxrwxr-x 2 carol carol 4096 Dec 10 17:59 Another_Directory/
```

#### 查看隐藏文件

我们之前使用 `ls -l` 获取的目录列表是不完整的：

```
$ ls -l
total 544
drwxrwxr-x 2 carol carol 4096 Dec 10 17:59 Another_Directory
-rw------- 1 carol carol 539663 Dec 10 10:43 picture.jpg
-rw-rw-r-- 1 carol carol 1881 Dec 10 15:57 text.txt
```

该目录中还有三个其他文件，但它们是隐藏的。在 Linux 中，以句点 (.) 开头的文件名会自动被隐藏。要查看它们，我们需要向 `ls` 添加 `-a` 参数：

```
$ ls -la
total 544
drwxrwxr-x 3 carol carol 4096 Dec 10 16:01 .
drwxrwxr-x 4 carol carol 4096 Dec 10 15:56 ..
drwxrwxr-x 2 carol carol 4096 Dec 10 17:59 Another_Directory
-rw------- 1 carol carol 539663 Dec 10 10:43 picture.jpg
-rw-rw-r-- 1 carol carol 1881 Dec 10 15:57 text.txt
-rw-r-r-- 1 carol carol 0 Dec 10 16:01 .thisIsHidden
```

文件 `.thisIsHidden` 仅仅因为其名称以 `.` 开头而被隐藏。

然而，目录 `.` 和 `..` 是特殊的。`.` 是指向当前目录的指针。`..` 是指向父目录的指针，即包含当前目录的那一个。在 Linux 中，每个目录至少包含这两个目录。

> **提示**：你可以组合 `ls`（以及许多其他 Linux 命令）的多个参数。例如，`-l -a` 可以写为 `ls -la`。

#### 理解文件类型

我们之前已经提到，`ls -l` 输出的第一个字母描述了文件的类型。三种最常见的文件类型是：

- **普通文件**

  文件可以包含任何类型的数据，并有助于管理这些数据。文件可以被修改、移动、复制和删除。

- **d (目录)**

  目录包含其他文件或目录，并有助于组织文件系统。从技术上讲，目录是一种特殊的文件。

- **l (符号链接)**

  这个“文件”是指向文件系统中其他位置的文件或目录的指针。

除了这些之外，还有三种其他文件类型，你至少应该知道它们，但它们超出了本课程的范围：

- **b (块设备)**

  此文件代表虚拟或物理设备，通常是磁盘或其他类型的存储设备，例如第一个硬盘可能由 `/dev/sda` 表示。

- **c (字符设备)**

  此文件代表虚拟或物理设备。终端（如 `/dev/ttyS0` 上的主终端）和串行端口是字符设备的常见示例。

- **s (套接字)**

  套接字充当两个程序之间传递信息的“管道”。

> **警告**：除非你知道自己在做什么，否则不要更改块设备、字符设备或套接字的任何权限。这可能会导致你的系统无法工作！

#### 理解权限

在 `ls -l` 的输出中，文件权限紧跟在文件类型之后显示，表现为三组各三个字符，顺序为 `r`、`w` 和 `x`。以下是它们的含义。请记住，破折号 `-` 代表缺少某项权限。

