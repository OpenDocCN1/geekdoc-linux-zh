
在某些情况下，访问权限可能过于严格。因此，Linux 提供了额外的设置来临时更改当前的用户和组身份。例如，`cdrecord` 程序通常需要 root 权限来访问用于刻录光盘（或 DVD）的写入器。因此，普通用户无法创建光盘，因为授予所有用户直接访问所有设备是太危险的。解决此问题的办法是 `setuid` 机制。`setuid`（用户 ID）是一种特殊属性，指示系统在特定的用户 ID 下执行程序。考虑 `/usr/bin/cdrecord` 命令：

```
-rwx------ 1 root root 281356 2004-03-12 21:30 cdrecord
```

使用 `chmod u+s /usr/bin/cdrecord` 设置 setuid 位。然后，通过 `chgrp users /usr/bin/cdrecord` 命令将 `cdrecord` 程序分配给 `users` 组。授予以下访问权限：

```
-rws------ 1 root users 281356 2004-03-12 21:30 cdrecord
```

通过 setuid 位，所有属于 `users` 组的用户都可以该程序。实际上，这意味着程序是以 root 身份运行的。

# 25 与 Shell 交互

## 注意事项

为程序设置 setuid 位会使你的计算机更容易受到攻击。只有在你非常了解该程序并且意识到潜在风险的特殊情况下，方才执行此操作。

### 25.2.4 setuid 位

setuid 属性适用于用户。然而，对于组也有一个等效的属性 —— setgid 属性。设置了此属性的程序将在其保存时所在的组 ID（group ID）下运行，无论由哪个用户启动它。因此，在设置了 setgid 位的目录中，所有新创建的文件和子目录都被分配给该目录所属组。考虑以下示例目录：

```
drwxwxr-x  2 root archive  48 Nov 19 17:12 backup
```

使用命令 `chmod g+s /test` 设置 setuid 位。随后，访问权限显示如下：

```
drwxrxr-x  2 root archive  48 Nov 19 17:12 backup
```

### 25.2.5 粘滞位 Sticky Bit

还有粘滞位。它属于可执行程序还是目录会有所不同。以此方式标记的文件将被加载到 RAM 中，以避免每次使用时都从硬盘中获取它。此属性很少使用，因为现代硬盘已经足够快了。如果将此属性分配给目录，它可以防止用户删除彼此的文件。典型示例包括 `/tmp` 和 `/var/tmp` 目录：

```
drwxrwxrwt  2 root root  1160 2002-11-19 17:15 /tmp
```

### 25.2.6 访问控制列表 ACLs

Linux 文件系统对象（如文件或目录）的传统权限概念可以通过 ACL（访问控制列表）进行扩展。它们允许为文件系统对象原始所有者或所属组之外的单个用户或组分配权限。

带有扩展访问权限的文件或目录可以通过简单的 `ls -l` 命令检测到：

```
-rw-r---- 1 tux project3 14197 Jun 21 15:03 Roadmap
```

与没有 ACL 的文件执行 `ls` 相比，`ls` 的输出并没有太大变化。Roadmap 属于 tux，属于组 project3 ；tux 对此文件拥有写和读访问权限，他的组以及所有其他人都有读取权限。区分此文件与无 ACL 文件的唯一区别是第一列持有权限位的地方有一个 `+`。

通过执行 `getfacl Roadmap` 获取有关 ACL 的详细信息：

```
# file: Roadmap
# owner: tux
# group: project3
user:rw-
user:jane-rw effective:r--
group:r---
group:django-rw effective:r--
mask:r---
other:-
```

输出的前三行不包含 `ls -l` 无法提供的信息。这几行仅说明文件名、所有者和所属组。第 4 到第 9 行包含 ACL 条目。传统的访问权限是使用 ACL 时可能权限的子集。我们的示例 ACL 为文件所有者以及用户 jane（第 4 和第 5 行）授予了读取和写入权限。传统概念已扩展到额外的用户。对组访问的处理上也是如此。所属组拥有读取权限（第 6 行），而组 django 拥有读取和写入权限。第 8 行中的掩码（mask）条目将用户 jane 和组 django 的有效权限降低为读取权限。其他用户和组无法获得对文件的任何访问权限（第 9 行）。

仅提供了非常基础的信息。在《管理指南》中查找有关 ACL 的更多背景信息。

# 25.3 重要的 Linux 命令

本节介绍了你的 SUSE LINUX 系统中最重要的命令。除了单个命令外，还列出了参数，并在适当的情况下引入了典型的示例应用。要了解更多关于各种命令的信息，请使用 man 页面，通过 `man` 后接命令名称访问，例如 `man ls`。

在页面中，使用 `(PgUp)` 和 `(PgDn)` 上下移动。使用 `(Home)` 和 `(End)` 在文档的开头和结尾之间移动。按 `(Q)` 退出视图模式。通过 `man man` 学习更多关于 `man` 命令本身的信息。

命令比列出的多。有关其他命令或更详细的信息，推荐阅读 O'Reilly 出版的《Linux in a Nutshell》。在下面的概述中，各个命令元素使用了不同的字体。

- 实际的命令始终以 `command` 形式打印。没有它，任何功能都无法运行。
- 没有对应程序的选项可以使用 *斜体* 表示。
- 进一步的细节，例如必须传递给命令才能正确运行的文件名，使用 Courier 字体编写。
- 不需要的规范或参数放置在 `[方括号]` 中。

根据你的需求调整设置。如果实际上不存在文件名，编写 `ls file(s)` 是没有意义的。你通常组合多个参数，例如编写 `ls -la` 而不是 `ls -l -a`。

## 25.3.1 文件命令

文件管理

`ls [option(s)] [file(s)]`

如果你在不带额外参数的情况下运行 `ls`，程序将以短格式列出当前目录的内容。

- 详细列表
- `-a` 显示隐藏文件

`cp [option(s)] sourcefile targetfile`

将 `sourcefile` 复制到 `targetfile`。

- `-i` 在需要覆盖现有的 `targetfile` 之前等待确认
- `-r` 递归复制（包括子目录）

`mv [option(s)] sourcefile targetfile`

将 `sourcefile` 移动到 `targetfile` 然后删除原始的 `sourcefile`。

- `-b` 在移动之前为 `sourcefile` 创建备份副本
- `-i` 在需要覆盖现有的 `targetfile` 之前等待确认

`rm [option(s)] file(s)`

从文件系统中删除指定的文件。除非使用选项 `-r`，否则 `rm` 不会删除目录。

- `-r` 删除任何存在的子目录
- `-i` 在删除每个文件之前等待确认。

`ln [option(s)] sourcefile link`

创建一个从 `sourcefile` 到 `targetfile` 的内部链接。通常，这种链接直接指向同一文件系统上的 `sourcefile`。然而，如果使用 `-s` 选项执行 `ln`，则会创建一个符号链接，它仅指向 `sourcefile` 所在的目录，从而跨文件系统链接。

- `-s` 创建符号链接

`cd [option(s)] [directory]`

更改当前目录。不带任何参数的 `cd` 将切换到用户的家目录。

`mkdir [option(s)] directoryname`

创建一个新目录。

`rmdir [option(s)] directoryname`

删除指定的目录，前提是它是空的。

`chown [option(s)] username.group file(s)`

将文件的所有权转移给指定的用户名。组名。`-R` 更改所有子目录的文件和目录。

`chgrp [option(s)] groupname`

将给定文件的组所有权转移给指定的组。所有者必须是当前组和新组的成员才能更改组。

`chmod [options] mode file(s)`

更改访问权限。模式参数有三部分：组、访问和访问类型。组接受以下字符：

- `u` 用户
- `g` 组
- `o` 其他

对于访问，使用 `+` 授予，使用 `-` 拒绝。访问类型由以下选项控制：

- `r` 读取
- `w` 写入
- `x` 执行 —— 执行文件或进入目录
- `s` 设置位 —— 程序或程序的运行就像是由所有者启动一样。
