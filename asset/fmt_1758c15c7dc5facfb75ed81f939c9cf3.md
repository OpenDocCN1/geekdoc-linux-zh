
`done`

# cpio -v o --format=newc backup.list | ssh user@host "cat > > backup_device"

其中 `directory_list` 是你想要备份的目录列表，`user@host` 是执行备份的用户/主机名组合，`backup_device` 是写入备份的位置（`./dev/nsa0`）。

## 17.12.4 pax

`pax(1)` 是 IEEE POSIX 对 `tar` 和 `cpio` 的响应。随着各个版本的发展，`tar` 和 `cpio` 已经变得略微不兼容。因此，POSIX 并没有完全标准化它们，而是创建了一个归档工具。`pax` 尝试读取和写入许多不同的 `cpio` 和 `tar` 格式，以及它自己的新格式。它的命令集看起来比 `tar` 更像 `cpio`。

## 17.12.5 Amanda

`Amanda`（高级网络磁盘归档器）是一个客户端/服务器备份系统，而不是单一程序。`Amanda` 服务器可以将任何数量通过 `Amanda` 客户端连接到 `Amanda` 服务器的计算机备份到单个磁带驱动器。对于拥有许多大磁盘的站点，一个常见问题是直接备份到磁带所需的时间超过了任务可用时间。`Amanda` 解决了这个问题。`Amanda` 可以使用“临时磁盘”同时备份文件系统。`Amanda` 创建“归档集”——一组在一段时间内使用的磁带，用于创建 `Amanda` 配置文件列出的所有文件系统的完整备份。“归档集”还包含最近的备份和增量备份。

配置文件提供了对备份以及 `Amanda` 生成的网络流量的精细控制。`Amanda` 将使用上述任何备份程序将数据写入磁带。`Amanda` 以端口或软件包的形式提供，默认不安装。

## 17.12.6 什么都不做

“什么都不做”并不是一个计算机程序，但它是最广泛使用的备份策略。它没有初始成本。没有需要遵循的备份计划。只需说不。。如果你的数据出了问题，那就忍受吧！

如果你的时间和数据价值乎其微或忽略不计，那么“什么都不做”就是你计算机最合适的备份程序。但要注意，UNIX 是一个非常有用的工具，你可能会在六个月内发现自己拥有一组对你来说很有价值的文件。

“什么都不做”对于 `/usr/obj` 和其他可以通过你的计算机精确重建的目录树是正确的备份方法。例如，构成本手册 HTML 或 PostScript 版本的文件。这些文档格式是从 SGML 输入创建的。没有必要对 HTML 或 PostScript 文件进行备份。SGML 文件会定期备份。

## 17.12 哪种备份程序最好？

`dump(8)` 话又怎么说。Elizabeth D. Zwicky 测试了这里讨论的所有备份程序。要保留你所有数据和 UNIX 系统的所有复杂性，明确的选择是 `dump`。Elizabeth 创建了包含各种异常情况（以及一些不寻常的情况）的文件系统，并通过对这些文件进行备份和恢复来测试每个程序。备份内容包括：带有空洞的文件和带有空块的文件、文件名中带有特殊字符的文件、不可读和不可写的文件、备份期间大小改变的文件、备份期间创建/删除的文件等。她在 1991 年 10 月的 LISA V 上展示了结果。参见[备份压力测试和 归档程序](http://berdmann.dyndns.org/zwicky/testdump.doc.html)。

## 17.12.8 紧急恢复程序

### 17.12.8.1 灾难发生前

对于可能发生的任何灾难，你只需要执行四个步骤。

首先，从每个磁盘中打印 `bsdlabel`（例如 `bsdlabel da0 | lpr`）、你的文件系统（`/etc/fstab`）以及所有启动信息，每个两个副本。

其次，断开所有设备上的启动软盘（`boot.flip` 和 `fixit.flip`）。最简单的检查方法是在软驱放入启动软盘的情况下重启，并检查启动信息。如果所有设备都能重启并正常工作，请跳到第三步。

否则，你必须创建两个启动软盘，其包含一个可以挂载你所有磁盘并访问你磁带驱动器的内核。无论你使用哪种备份程序，这些程序必须是静态链接。如果你使用 `dump`，软盘必须包含 `restore`。

第三，创建备份磁带。你在最后备份之后做的任何更改都将不可挽回地丢失。对备份磁带进行写保护。

第四，测试软盘（无论是 `boot.flip` 和 `fixit.flip` 或你在第二步中制作的两个启动软盘）以及备份磁带。记录该过程。这些笔记连同备份，可以防止你破坏备份磁带（如何做到呢？在恢复磁带时，你可能会不小心输入 `tar cvf /dev/sa0` 并覆盖掉你的磁带备份）。

为了增加安全措施，每次都制作启动软盘和两块备份磁带。每种各一个放在远程位置。远程位置**不是**办公大楼的地下室。世界贸易中心的一些公司为此付出了惨痛的教训。远程位置在物理上应与你的计算机和磁盘驱动器保持相当距离。

## 示例 17-3. 创建启动软盘的脚本

```bash
#!/bin/sh

#
# 创建恢复软盘
#
# 格式化软盘
#
PATH=/bin:/sbin:/sbin:/usr/bin
format -q fd0
if [ $? -ne 0 ];
then
echo "软盘损坏，请使用新的"
exit 1
fi
# 在软盘上放置启动块
# \absdlabel -w -B /dev/fd0c fd1440
#
# 对唯一的分区进行 newfs 操作
#
newfs -t 2 -u
#
# 在软盘上放置启动块
# \absdlabel -w -B /dev/fd0c fd1440
#
# 对唯一的分区进行 newfs 操作
#
newfs -t 2 -u
```

# 第 17 章 存储

```bash
cp -f /dev/MAKEDEV /mnt/dev
chmod 755 /mnt/dev/MAKEDEV
chmod 500 /mnt/sbin/init
chmod 555 /mnt/sbin/fsck /mnt/sbin/mount /mnt/sbin/halt
chmod 555 /mnt/bin/sh /mnt/bin/sync
chmod 6555 /mnt/sbin/restore
```

```bash
#
# 创建设备节点
#
cd /mnt/dev
./MAKEDEV std
./MAKEDEV da0
./MAKEDEV da1
./MAKEDEV da2
./MAKEDEV pty0
cd /
```

```bash
#
# 创建最小文件系统表
cat > /mnt/etc/fstab <<EOM
/dev/fd0a / ufs rw 1 1
EOM
```

```bash
#
# 创建最小密码文件
#
cat > /mnt/etc/passwd <<EOM
root:0:0:Charlie&:/root:/bin/sh
EOM
```

```bash
cat > /mnt/etc/master.passwd <<EOM
root:0:0:0:0:Charlie&:/root:/bin/sh
EOM
```

```bash
chmod 600 /mnt/etc/passwd
chmod 644 /mnt/etc/passwd
/usr/sbin/pwd_mkdb -d /mnt/etc /mnt/etc/master.passwd
```

```bash
#
# 卸载软盘并通知用户
#
/sbin/umount /mnt
echo "The Floppy has been unmounted and is now ready."
```
