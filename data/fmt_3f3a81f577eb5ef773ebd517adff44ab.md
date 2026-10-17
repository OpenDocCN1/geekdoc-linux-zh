
```
$yyang@fedora-serverA~$ cat /etc/passwd
```

要显示`/etc/passwd`文件和`/etc/group`文件，执行此命令：

```
$yyang@fedora-serverA~$ cat /etc/passwd /etc/group
```

# Linux 管理：入门指南

输入此命令将`/etc/passwd`与`/etc/group`合并，并将输出发送到`users-and-groups.txt`文件中。

```
yyang@fedora-serverA ~$ cat /etc/passwd /etc/group > users-and-groups.txt
```

要将`/etc/hosts`文件的内容追加到刚刚创建的`users-and-groups.txt`文件中，请输入

```
yyang@fedora-serverA ~$ cat /etc/hosts >> users-and-groups.txt
```

> 提示 如果你想反向查看一个文件，可以使用`tac`命令。

# 一次显示一屏文件：more

`more`命令的工作方式与 DOS 版本的程序相同。它接收输入文件并一次显示屏。输入文件可以来自标准输入 `stdin`，也可以来自命令行参数。尽管很少使用，但额外的命令行参数可以在手册页（`man page`）中找到。

要一次显示一次`/etc/passwd`文件，请使用此命令：

```
yyang@fedora-serverA ~$ more /etc/passwd
```

要一次显示一次`ls`命令生成的目录列表，请输入

```
yyang@fedora-serverA ~$ ls | more
```

## 磁盘利用率：du

你需要确定磁盘空间是在哪里以及被谁消耗的，尤其是当你正在其上运行程序时！`du`命令允许你按目录确定磁盘利用率。

以下是一些可用的选项。

| du 选项 | 说明 |
| :--- | :--- |
| `-c` | 在运行结束时产生总计。 |
| `-h` | 以人类可读的格式打印大小。 |
| `-k` | 以千字节而非块大小打印大小。（注意：在 Linux 下，块等于 1KB，这在所有形式的 UNIX 中并不成立。） |
| `-s` | 摘要。仅为每个参数打印总计。 |

# 第 5 章：命令行

要以人类可读的格式显示`PWD`中所有文件和目录使用的总空间，请使用此命令：

```
yyang@fedora-serverA ~$ du -sh .
2.2M
```

# 显示文件的目录位置：which

`which`命令会在整个路径中搜索行中指定的可执行文件名称。如果找到了该文件，命令将输出该文件的实际路径。

使用以下命令查找`rm`命令的二进制文件所在的目录：

```
yyang@fedora-serverA ~$ which rm
/bin/rm
```

你可能会发现这与`find`命令相似。这里的区别是`which`只搜索目录，它的速度快得多。当然，它的限制也比`find`大得多，但如果你正在寻找一个程序，你会发现它是更好的命令选择。

## 查找命令：whereas

`whereas`工具搜索你的路径并显示程序名称、绝对目录、源文件（如果可用）以及该命令的手册页（同样，如果可用）。要查找`grep`命令的程序、源码和手册页的位置，请使用：

```
yyang@fedora-serverA ~$ whereas grep
grep: /bin/grep /usr/share/man/man1/grep.1.gz /usr/share/man/man1p/grep.lp.gz
```

## 磁盘剩余：df

`df`程序显示按分区（或卷）的剩余空间。驱动器/分区必须挂载才能获取此信息。也可以收集网络文件系统 `NFS` 的信息。这里列出了`df`的一些参数；（很少使用的）选项列在`df`手册页中。

| df 选项 | 说明 |
| :--- | :--- |
| `-h` | 生成人类可读的剩余空间而非剩余块 |
| `-l` | 仅列出本地挂载的文件系统。不显示任何关于网络挂载文件系统的信息。 |

# Linux 管理：入门指南

要显示所有本地挂载驱动器的剩余空间，请使用此命令：

```
yyang@fedora-serverA ~$ df -l
```

要以人类可读的格式显示当前工作目录所在文件系统的剩余空间，请输入

```
yyang@fedora-serverA ~$ df -h
```

要以人类可读的格式显示`/tmp`所在文件系统的剩余空间，请输入此命令：

```
yyang@fedora-serverA ~$ df -h /tmp
```

## 同步磁盘：sync

与其他操作系统一样，Linux 维护着一个磁盘缓存以提高效率。缺点是，你想要写入磁盘的内容在任何给定时刻并不都已写入。

要调度缓存写入磁盘，请使用`sync`命令。如果`sync`检测到写入磁盘的缓存已经调度，则指示内核立即刷新缓存。这需要命令行参数来确保磁盘缓存已刷新：

```
yyang@fedora-serverA ~$ sync ; sync
```

> 注意 手动执行此命令现在已很少必要了，因为 Linux 内核本身就能很好地完成这项工作。

# 移动用户及其主目录

本节节将演示如何整合本章中涵盖的一些主题和工具。Linux 优雅的设计允许你组合简单命令来执行高级操作。在管理过程中，你可能需要移动用户及其文件。本节将涵盖将用户`project5`从其默认主目录`/home/project5`移动的过程。你还必须为用户的文件和目录设置适当的权限和所有权，以便用户可以访问它们。与之前作为普通用户执行的练习不同，你需要超级用户权限来执行这些步骤。

# 第 5 章：命令行

- 1. 以 root 身份登录系统并启动终端。
- 2. 创建将用于此项目的用户。用户名为`project5`。

```
root@fedora-serverA ~$ useradd project5
```

- 3. 使用`grep`命令查看`/etc/passwd`文件中创建的用户条目。

```
root@fedora-serverA ~$ grep project5 /etc/passwd
project5:x:502:503::/home/project5:/bash
```

- 4. 使用`ls`命令显示用户主目录的列表。

```
root@fedora-serverA ~$ ls -al /home/project5
total 48
dr------ 3 project5 4096 Jan 10 12:00 .
drwxr-xr-x 7 root project5 4096 Jan 10 12:00 ..
-rw-r---- 1 project5 33 Jan 10 12:00 .bash_logout
-rw-r---- 1 project5 176 Jan 10 12:00 .bash_profile
-rw-r---- 1 project5 124 Jan 10 12:00 .bashrc
```

（注：日期/时间的 OCR 生成文本已根据标准输出格式进行了清理）

- 5. 检查用户使用的总磁盘空间。

```
root@fedora-serverA ~$ du -sh /home/project5
56K /home/project5
```

- 6. 使用`su`临时变为该用户。

```
root@fedora-serverA ~$ su - project5
[project5@fedora-serverA ~]$
```

- 7. 作为`project5`，查看你的工作目录。

```
project5@fedora-serverA ~]# pwd
/home/project5
```

- 8. 作为用户`project5`，创建一些空文件。

```
project5@fedora-serverA ~]# touch a b c d e
```

- 9. 通过退出`project5`的配置回到 root 用户。

```
project5@fedora-serverA ~]# exit
```

- 10. 创建存放用户新主目录的`/export`目录。

```
root@fedora-serverA ~$ mkdir -p /export
```

- 11. 使用`tar`命令归档压缩`project5`当前的主目录（`/home/project5`），并解压到其新位置。

```
root@fedora-serverA ~$ tar czf - /home/project5 | (cd /export ; tar -xvf -)
```

> 提示 在此处配合`tar`命令使用的横杠 `--` 强制其先将输出到 stdout，然后从 stdin 接收输入。

- 12. 使用`ls`命令确保新主目录在`/export`目录下已正确创建。
