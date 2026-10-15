
```
[localhost]$ dd if=datafile of=outfile.bak

0+1 records in

0+1 records out
```

![](img/b5f7722b7c2983a215c7726aaada19f9_309_0.png)

# 启动软盘

制作启动软盘是一个好习惯，因为计算机问题（如硬盘故障）可能会阻止你从硬盘启动 UNIX。制作启动软盘（在此情况下为 Red Hat Linux），你需要使用四个实用程序：`rdev`、`mkfs`、`fdformat` 和 `dd` 命令。`rdev` 命令查询并设置根设备，根设备是 UNIX 的根文件系统。根文件系统反过来包含 UNIX 内核（核心操作系统），启动 UNIX 所需的。（在 Red Hat Linux 下，内核存储在以 `vmlinuz` 开头的文件中。该文件通常存储在 `/boot` 目录下：）

## 制作可引导软盘

使用 `mkfs` 命令在软磁盘或硬盘分区等设备上构建 UNIX 或 Linux 文件系统。该命令通常如下所示执行，其中 `-t` 选项标识文件类型，`filesystem` 标识设备名称：

语法 `mkfs [-t option] [filesystem]`

文件系统类型决定了 UNIX 如何在设备上读写信息，存储在文件 `/etc/fstab`（文件系统表）中，如图 8–1 所示。

![](img/b5f7722b7c2983a215c7726aaada19f9_310_0.png)

图 8-1 `/etc/fstab` 中的文件系统类型

`fdformat` 命令对软磁盘进行低级格式化，以确保介质无缺陷且可写。与高级格式化（检查并验证磁盘记录表面并设置分配表/文件系统，如在 Microsoft 操作系统上执行的操作）不同，低级格式化准备记录表面，但不建立文件系统。（后者是 `mkfs` 工具的功能，因此这两个程序 `fdformat` 和 `mkfs` 必须协同工作以准备软磁盘使用。）低级格式化比高级格式化更彻底地检查记录表面。格式化软磁盘的命令行输入遵循以下用法，其中 `-n` 选项禁用格式化后进行的验证。A 驱动器（第一个软磁盘驱动）通常指示为 `/dev/fd0`，B 驱动器（第二个软磁盘驱动）为 `/dev/fd1`：

语法 `fdformat [-n] [filesystem]`

默认格式类型适用于 1.44MB（高密度）软磁盘。文件系统也可以指示为 A 驱动器上的高密度软磁盘 `/dev/fd0H1440`，以及 B 驱动器上的高密度软磁盘 `/dev/fd1H1440`。

# 第8章 A 探索 UNIX 工具

你现在准备好制作一个可引导磁盘了。

接下来的步骤假设以下条件：
- 你拥有系统级权限。也就是说，你使用的是 root 账户登录；有关如何访问此账户的信息，请咨询你的导师。
- 你登录到了主机控制台。如果你通过 telnet 会话访问 Linux 计算机，则无法执行这些步骤。

## 要制作可引导磁盘：

1. 确定 `vmlinuz`（持有 Linux 内核的文件）的位置（最可能在 `/boot` 中）。

> 如果查找该文件遇到困难，请使用 `find` 命令：输入 `find / -name vmlinux\*` 并按回车。

2. 输入 `rdev` 然后按回车验证 `/boot` 分区的位置。你的屏幕应该看起来如下：
```
[root@localhost root]# rdev

/dev/hda5
```

3. 在 A 驱动器中插入一张空白软磁盘。

4. 输入 `mkfs -t ext2 /dev/fd0 1440` 并按回车在磁盘上创建 Linux 文件系统。（注意，尽管你的系统可能格式化为支持日志的 Linux ext3 文件系统，但你需要使用 ext2 来格式化软磁盘。）你的屏幕现在应该类似于图 8-2。

5. 输入 `fdformat /dev/fd0` 并按回车对磁盘进行低级格式化。该工具在执行操作时会显示进度。格式化完成后，你的屏幕应该类似于：
```
[root@localhost root]# fdformat /dev/fd0

Double-sided, 80 tracks, 18 sec/track. Total capacity 1400 kB.

Formatting ... done

Verifying ... done
```

图 8-2 `mkfs` 命令的结果结果

6. 输入 `dd if=/boot/vmlinux-2.4.7-10 of=/dev/fd0` 并按回车使软磁盘可引导。（对于 Red Hat Linux 7.2 使用 `/boot/vmlinux-2.4.7-10`。如果你使用的是早期或更晚版本的 Linux，输入 `ls /boot` 来确定 `vmlinux-x.x.x-xx` 文件的确名称，使用步骤 1 中描述的技术。）`dd` 命令的结果应显示在你的屏幕上：
```bash
root@localhost root# dd if=/boot/vmlinux-2.4.7-10 of=/dev/fd0

1566 records in

1566 records out
```
