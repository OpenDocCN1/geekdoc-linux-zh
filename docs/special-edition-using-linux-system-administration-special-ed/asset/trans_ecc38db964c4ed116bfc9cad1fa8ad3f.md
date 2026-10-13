
备份类型通过转储级别（dump levels）指定。转储级别以数字指定。转储级别 0 表示完整备份，转储级别 1-9 表示应执行增量备份，其中自上次运行（其级别小于或等于指定的转储级别）以来修改的所有文件都将被归档。

要使用 dump 执行备份，请使用以下语法：

```
dump <dump level>usf <tape length> <tape device> <partition to back up>
```

u 标志表示 dump 应更新 `/etc/dumpdates`，以便可以进行增量备份。将在 `/etc/dumpdates` 文件中创建如下格式的条目：

```
<partition> <dump level> <date and time>
```

例如，以下条目表示 `/dev/sdb2` 分区已在 12 月 27 日进行了备份，并执行了完整备份（转储级别 0）：

```
/dev/sdb2     0 Mon Dec 27 22:18:47 1999
```

s 标志与磁带长度值结合使用，用于指定所用磁带的长度（以英尺为单位）。如果你不知道磁带的长度，可以使用任意大的数字，例如 650,000，因为默认长度仅为 2,300 英尺，这意味着 dump 会在磁带完全填满之前就提示你更换磁带。最后，f 标志与磁带设备结合使用，用于指示备份应存储的位置。

例如，考虑以下命令：

```
# dump 9usf 650000 /dev/tape /opt
```

此命令表示，挂载在 /opt 的分区应使用级别 9 增量备份备份到磁带设备。

dump 命令生成的输出指示正在备份的分区、备份每个阶段的成功情况以及完成备份所花费的时间，如下例所示：

```
# dump 0usf 650000 /dev/tape /opt
DUMP: Date of this level 0 dump: Tue Dec 28 22:14:04 1999
DUMP: Date of last level 0 dump: The epoch
DUMP: Dumping /dev/sda6 (/opt) to /dev/tape
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 14685 tape blocks on 0.34 tape(s).
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: 14852 tape blocks on 1 volumes(s)
DUMP: finished in 11 seconds, throughput 1350 KBytes/sec
DUMP: Closing /dev/tape
DUMP: DUMP IS DONE
```

## 恢复文件和文件系统

restore 命令允许你从使用 dump 命令创建的备份中恢复文件和目录。restore 命令可用于从级别 0 转储及其后的增量转储中恢复整个文件系统层次结构，也可用于从一个或多个转储磁带中恢复一个或多个文件。

![](img/6c13bcf02a08ad7923caab46f051d96a_183_0.png)

restore 命令必须由 root 用户运行，以便文件属主、模式和修改时间能够还原为与原始文件一致。

以下命令将恢复整个文件系统层次结构：

```sh
# restore rf /dev/tape
```

r 标志表示你要恢复整个文件系统，f 标志与 /dev/tape 一起指定备份数据的来源。

restore 命令可以使用 i 标志以交互方式恢复文件。当使用 i 标志调用时，restore 命令会提供一个交互式 shell，你可以在其中更改备份集内的目录、列出目录内容以及提取文件。

考虑以下示例，其中文件 `/opt/src/amanda-2.4.1p1.tar.gz` 被恢复到临时 `/restore` 目录：

```text
# cd /restore
# mt rewind
# restore if /dev/tape
restore > ls
.:
lost+found/  src/
restore > cd src
restore > ls
./src:
README                  amanda-2.4.1p1.tar.gz  glibc22.patch
amanda-2.4.1p1/         glibc21.patch
restore > add amanda-2.4.1p1.tar.gz
restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you should start
with the last volume and work towards the first.
Specify next volume #: 1
set owner/mode for './'? [yn] n
restore > quit
# ls
lost+found  src
# cd src
# ls -l
total 697
-rw-r--r-- 1 root root 709624 Nov 21 1998 amanda-2.4.1p1.tar.gz
```

在交互式 restore shell 中，有两个命令至关重要：

- `add <filename>`：将文件添加到要恢复的文件集合中
- `extract`：将指定的文件集合从备份恢复到当前位置

## 使用 AMANDA 进行备份

Amanda 是一个免费提供的备份软件程序，由马里兰大学开发。AMANDA 这个名称代表 Advanced Maryland Automated Network Disk Archiver（高级马里兰自动化网络磁盘归档器）。其主要作者是马里兰大学的 James da Silva。

Amanda 非常适合备份中大型网络。它允许你将多台机器的网络备份到中央备份服务器。Amanda 使用 GNU tar 或大多数 Linux 系统自带的原生 dump 程序来执行备份。与 Samba 结合使用时，Amanda 还可以备份 Windows 95 和 NT 机器。

Amanda 背后的理念是将多台机器的备份集中到一个主磁带服务器上，该服务器拥有一个或多个磁带驱动器和一个大容量暂存磁盘。许多系统的备份可以通过网络完成，备份到备份服务器上的暂存磁盘。多个网络备份也可以并行进行。一旦数据备份到暂存磁盘，就会以连续流模式写入快速磁带驱动器。这可以确保高效地写入磁带，而无需中断磁带。

> **注意**
>
> Amanda 可以在没有暂存磁盘的情况下运行：来自网络客户端的数据可以直接写入磁带，但性能会下降，总备份时间可能会增加数倍。

Amanda 备份软件由一套客户端和服务器软件组成。Amanda 提供自己的网络协议，这些协议运行在标准 UDP 和 TCP 协议之上。目前，Amanda 使用 UDP 端口 10080 以及 TCP 端口 10082 和 10083 在 Amanda 客户端和服务器之间进行通信。Amanda 提供了一种非常灵活的数据压缩方案，可以配置为在磁带服务器上压缩数据以减少客户端机器的负载，也可以配置为在客户端上压缩数据以减少客户端与磁带服务器之间的网络流量。

Amanda 是一个功能强大的软件；要完全理解并掌握它需要时间。可以考虑向 `amanda-users-request@amanda.org` 发送消息来订阅 Amanda 邮件列表。这是了解更多关于 Amanda 的信息以及从运行 Amanda 的其他管理员那里获得帮助的好资源。

## 从源代码构建 AMANDA

你可以从 `http://www.amanda.org` 下载 Amanda 源代码。撰写本文时最新的稳定版本是 2.4.1p1。在编译该软件之前，Amanda 要求系统上存在某些其他软件包：

- GNU tar 1.12 或更高版本
- Perl 5.004 或更高版本
- GNU readline 2.2.1 或更高版本
- GNU awk 3.0.3 或更高版本
- Gnuplot 3.5 或更高版本

如果你打算使用 Amanda 备份 Windows 95、98、NT 或 2000 客户端系统，还需要在 Amanda 备份服务器上安装 Samba 1.9.18p10 或更高版本。

### 构建过程

使用以下步骤从源代码安装 Amanda：

1. 下载 Amanda 归档文件并将其保存到方便的位置，例如 `/usr/local/src`。在撰写本文时，源代码归档的当前版本是 `amanda-2.4.1p1.tar.gz`。

2. 将当前目录更改为 `/usr/local/src`：

   ```
   # cd /usr/local/src
   ```

3. 解压源代码归档：

   ```
   # tar xzf amanda-2.4.1p1.tar.gz
   ```

   源代码将被解压到子目录 `amanda-2.4.1p1` 中。

4. 将当前目录更改为新的子目录：

   ```
   # cd amanda-2.4.1p1
   ```

5. 使用以下命令配置软件：

   ```
   # ./configure --with-user=bin --with-group=backup \
   --with-tape-device=/dev/nst0 --with-amandahosts
   ```

   `with-user` 选项指定软件将以哪个用户身份运行，`with-group` 选项指定软件将以哪个组身份运行，`with-tape-device` 选项指示默认磁带设备，`with-amandahosts` 选项指示在配置 Amanda 时将使用 `.amandahosts` 文件而不是 `.rhosts` 文件。运行 Amanda 的用户需要拥有足够的权限来读写你将使用的任何磁带驱动器；为此，典型的选择是 bin、amanda 或 backup。常见的组选择包括 backup、disk 或 operator。

   此命令将使用名为 Daily 的默认备份配置来配置 Amanda。如果你想要使用不同的配置名称，请在 configure 命令中添加 `--with-config=<your configuration name>`。如果你仅是为了在客户端上运行而编译 Amanda，而不需要提供 Amanda 服务器功能，请在 configure 命令中添加 `--without-server` 选项。

   默认情况下，Amanda 将被配置为安装在表 10.1 中列出的目录中。

**表 10.1 — Amanda 安装目录**

| 目录 | 描述 |
|---|---|
| `/usr/local/sbin` | 包含服务器端二进制的目录。 |
| `/usr/local/libexec` | 包含客户端二进制的目录。 |
| `/usr/local/lib` | 包含 Amanda（共享）库的目录。 |
| `/usr/local/man` | 包含手册页的目录。 |
| `/usr/local/etc/amanda` | 存放运行时文件的目录。Amanda 支持每个站点多个配置；这些配置包含在此目录的子目录中。 |

