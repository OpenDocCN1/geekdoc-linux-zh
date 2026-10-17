
# tar cvf etc.tar /etc

## 第 11 章 备份、恢复与恢复

在这里，选项使用 `tar` 创建归档，在消息输出中详细显示，并使用文件名 `etc.tar` 作为 `/etc` 目录内容的归档名称。

> 注意
> 在历史上，`tar` 一直不受欢迎因为它无法关闭设备文件：对于 Fedora Core 提供的 `tar` 的 GNU 版本 `GNutar` 来说，这不再是事实。`GNutar` 还能处理 UNIX tar 无法处理 gzip 和 bzip 压缩。不要听那些警告不要使用 `tar` 的旧 UNIX 黑客的话。

或者，如果 `tar` 的输出发送到标准输出并重定向到文件，命令显示如下：

```
# tar cv /etc etc.tar
```

结果是：`/etc` 目录中的所有文件都将保存到名为 `etc.tar` 的文件中。凭借大量的选项（见手册页），`tar` 在结合 shell 脚本时非常灵活且强大。通过 `-z` 选项，它可以创建和恢复 gzip 压缩的归档，而 `-j` 选项可与 bzipped 文件配合。

> 提示
> 你是否有用 MTF 制作的废弃磁带想要从中提取文件？微软磁带格式（MTF）用于备份 Windows NT 文件，并可以使用名为 `mtf` 的 Linux 工具读取。此 Linux 程序适用于 SCSI 磁带驱动器。不支持软件压缩和跨磁带的归档。请从 `http://www.layton-graphics.com/mtf` 下载源代码。

### 使用 tar 创建全备份和增量备份

如果你想创建一个全备份，

```
# tar cjvf backup.tar.bz2
```

将创建一个整个系统的 bzip2 压缩 tar 包（使用 `j` 选项）。

要执行增量备份，你必须找到自上次备份以来更改的所有文件。（为了简单起见，假设你每天进行增量备份。）要查找文件，请使用 `find` 命令：

```
# find / -newer name_of_last_backup_file ! -type f -print
```

单独运行时，`find` 将生成文件系统列表并将其打印到屏幕上。`! -type f` 删除了列表中普通文件以外的所有内容；否则，即使内容没有更改，整个目录也会被发送 `tar`。

按如下方式将 `find` 命令的输出传递给 `tar`：

```
# find / -newer name_of_last_backup_file ! -type d -print | \
tar czT backup_file_name_of_device_name
```

在这里，`-T` 选项从缓冲区获取文件名（其中 `-` 是缓冲区的简写）。

> `tar` 可以备份到原始设备（没有文件系统的设备），也可以备份到格式化分区。例如，
> `# tar cvzf /dev/hdd /boot /etc /home`
> 将这些目录备份到 `/dev/hdd`（不是 `/dev/hda1`，而是未格式化的设备本身）。

`tar` 命令还可以备份到多个软磁盘上：

```
# tar czvmf /fd0 /home
```

将备份 `/home` 的内容并将文件分布在多个软带上，并向你提示此消息：
准备卷 #2 对于 `/dev/fd0/` 并按回车：

*(注：原文后续存在大量重复和 OCR 错误，此处已提取核心内容。)*

要还原一个 cpio 归包，

```
# cpio -imd federatest.cpio
```

列出 cpio 文件的内容，

```
# cpio -otv federatest.cpio
drwx-rw-r-x hoy/hoyt      2003-09-04 18:15:00 federatest/
-rw-rw-r-- hoyt/hoyt      163 2003-09-03 22:30:49
-rw-rw-r-- hoyt/hoyt      840 2003-09-01 19:27:55
-rw-rw-r-- hoyt/hoyt     1485 2003-09-01 18:14:23 federatest/style-sheet.txt
-rw-rw-r-- hoyt/hoyt      931 2003-09-01 19:02:00 federatest/fedora_toc.txt
```
