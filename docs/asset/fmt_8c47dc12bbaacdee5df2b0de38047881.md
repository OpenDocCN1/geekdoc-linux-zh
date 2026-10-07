
`groups:x:1234:root,bozoette`

这向系统添加了一个 GID 为 1234，成员为 root 和 bozoette 的组。完成后，

3. 按下 `Ctrl+Alt+F6` 切换到另一个命令终端 (`tty6`)，并使用用户名 `bozoette` 和密码 `LINUXrocks` 登录终端。

4. 在命令提示符符下，输入 `groups` 并按回车。`bozoette` 是哪些组的成员？

5. 在命令提示符下，输入 `id` 并按回车。用户 `bozoette` 的主组是哪一个？

6. 在命令提示符下，输入 `touch file1` 并按回车，在当前目录下创建一个新文件 `file1`。

7. 在命令提示符下，输入 `ls -l` 并按回车。`file1` 的所有者和所属组分别是谁？为什么？

8. 在命令提示符下，输入 `newgrp groups` 并按回车，临时将 `bozoette` 的主组更改为 `groups`。

9. 在命令提示符下，输入 `touch file2` 并按回车，在当前目录下创建一个新文件 `file2`。

10. 在命令提示符下，输入 `ls -l` 并按回车。`file2` 的所有者和所属组分别是谁？为什么？

11. 输入 `exit` 并按回车退出使用 `newgrp` 命令创建的 shell。接着，输入 `exit` 并按回车退出你的 shell。

12. 按下 `Ctrl+Alt+F5` 切换回 `tty`。

13. 在命令提示符下，输入 `groupdel groups` 并按回车，从系统中删除该组。`groupdel` 命令编辑了哪一个文件？

14. 输入 `exit` 并按回车退出你的 shell。

## 探索练习 10-1

**预计时间：** 20 分钟

**目标：** 配置 `rsyslogd`。

**描述：** 写出你要添加到 `/etc/rsyslog.conf` 的条目以实现：

- a. 将来自内核的所有关键消息记录到 `/var/log/alert`
- b. 将来自用户进程的消息记录到 `/var/log/userlog`
- c. 将守护进程的所有调试消息和更严重的消息记录到 `/var/log/printer`
- d. 将守护进程的所有非通知（notice）消息记录到 `/var/log/mailman`
- e. 将所有警报（alert）和严重错误消息记录到 `/var/log/serious`
- f. 将内核守护的所有警告和错误记录到 `/var/log/shared`

## 探索练习 10-2

**预计时间：** 15 分钟

**目标：** 研究 `useradd` 选项。

**描述：** 使用手册（man pages）查找 `useradd` 命令中 `-d` 选项的描述。该选项的作用是什么？它编辑哪个文件？如何配合 `useradd` 命令设置使所有新账户在 2005 年 3 月 5 日之前创建？你使用了什么命令？

## 探索练习 10-3

**预计时间：** 40 分钟

**目标：** 配置 CUPS 打印机共享。

**描述：** 在项目 10-2 中，你在 Fedora Linux 虚拟机上的 CUPS 远程管理工具中启用远程管理和 IPP 打印共享选项。然而，为了远程访问 CUPS 打印共享打印机，你必须在 Fedora 默认启用的防火墙中允许 HTTP (TCP端口80)、HTTPS (TCP端口443) 和 IPP (TCP端口631) 端口运行以下命令启用这些端口：

```
firewall-cmd --add-service http

firewall-cmd --add-service https

firewall-cmd --add-service ipp
```

接下来，使用 `ip addr show` 命令确定你的 Fedora Linux 机器 IP 地址。通过这种方式，你可以在 Windows 或 macOS 电脑的浏览器中访问 `http://IPaddress:631` 来使用 CUPS 管理，其中 *IPaddress* 是 Fedora 虚拟机的 IP 地址。最后，在 Windows 的设置或 macOS 的系统偏好设置中添加新打印机，打印到 URL `http://IPaddress:631/printers`。

## 探索练习 10-4

**预计时间：** 40 分钟

**目标：** 配置 CUPS。

**描述：** 在项目 10-2 中，你在 Fedora Linux 虚拟机上的 CUPS 远程管理工具中启用远程管理和 IPP 打印共享选项。然而，为了远程访问 CUPS 打印共享打印机，你必须在 Fedora 默认启用的防火墙中允许 HTTP (TCP端口80)、HTTPS (TCP端口443) 和 IPP (TCP端口631) 端口运行以下命令启用这些端口：

```
firewall-cmd --add-service http

firewall-cmd --add-service https

firewall-cmd --add-service ipp
```

接下来，使用 `ip addr show` 命令确定你的 Fedora Linux 机器 IP 地址。通过这种方式，你可以在 Windows 或 macOS 电脑的浏览器中访问 `http://IPaddress:631` 来使用 CUPS 管理，其中 *IPaddress* 是 Fedora 虚拟机的 IP 地址。最后，在 Windows 的设置或 macOS 的系统偏好设置中添加新打印机，打印到 URL `http://IPaddress:631/printers`。

# 第11章 压缩、系统备份与软件安装

对于实用工具的压缩率，从 100% 中减去压缩百分比。如果一个压缩工具将文件压缩到原始大小的 52%，则其压缩比为 48%。

Linux 用户有许多压缩工具可用；本节将介绍五种最常用的工具：

- `compress`
- GNU `zip`
- `xz`
- `zip`
- `bzip2`

### 使用 `compress` 命令

`compress` 命令是 UNIX 和 Linux 系统上最老的压缩工具之一。它的算法是自适应 Lempel-Ziv (LZW)，平均压缩比较为 40-50%。

使用 `compress` 压缩文件时，你需要指定要压缩的文件作为参数。每个文件都会被重命名为带有 `.z` 扩展名的文件，以表示它已压缩。此外，你可以使用 `compress` 命令的 `-v`（详细）选项来显示压缩率。最终输出将显示示例 `samplefile` 在压缩前后的名称和大小：

```
[@server ~]# ls -l

total 28

drwx------ 3 root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root 27298 Jul 21 08:15 samplefile

-rw-r--r-- 1 root 540 Jul 21 08:18 samplefile2

[@server ~]# compress -v samplefile samplefile2

samplefile: replaced with samplefile.Z Compression: 59.65%

samplefile2: replaced with samplefile.Z Compression: 37.22%

total 20

drwx------ 3 root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root 339 Jul 21 08:15 samplefile2.Z

-rw-r--r-- 1 root 11013 Jul 21 08:15 samplefile2.Z

[@server ~]#
```

> 注意 1
大多数 Linux 发行版默认没有安装 `compress` 命令。若要从互联网上的软件仓库安装它，你可以在 Fedora 上以 root 用户运行 `yum install ncompress` 命令，或者在 Ubuntu Linux 上以 root 用户运行 `apt install ncompress` 命令。

> 注意 2
`compress` 命令会保留每个被压缩文件的原始所有者、修改时间和访问时间。

> 注意 3
默认情况下，`compress` 不会压缩符号链接、硬链接或极小文件，除非你使用 `-f` 选项。

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

> 注意 4
你可以使用 `-r` 选项并将指定目录作为 `compress` 命令的参数，压缩该目录下的所有文件。

压缩后，可以使用 `zcat` 命令显示压缩文件的内容，如下输出所示：

```
[root@server1 ~]# zcat samplefile.Z

Hi there, I hope this day finds you well.

```

遗憾的是，今年在阿冈昆比公园（Algonquin Park）度假期间，我们未能前往你的餐厅——我特别想看到餐厅里 Highland Inn 酒店的模型和火车站模型。

我一直在阅读关于阿冈昆比公园的历史，但在哪处都没有找到关于 Highland Inn 最初位于凯奇湖（Cache Lake）的描述。

如果不麻烦的话，能否请你告诉我是否不需要等到明年拜访你的木屋了？

诚挚的问候，
Mackenzie Elizabeth

> 注意 5
你也可以使用 `zmore` 命令和 `zless` 命令分页查看压缩文件的内容，或者使用 `zgrep` 命令搜索压缩文件的内容。

要解压用 `compress` 命令压缩的文件，请使用 `uncompress` 命令后跟要解压的文件名。这将恢复原始文件。`uncompress` 命令会输出并显示创建的 `samplefile.Z` 和 `samplefile.2` 文件名：

```
[root@server1 ~]# uncompress -v samplefile.Z samplefile.2

samplefile.Z: replaced with samplefile

samplefile.2: replaced with samplefile2

[root@server1 ~]# ls -l

total 28

3 root root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root root 27298 Jul 21 08:15 samplefile

-rw-r--r-- 1 root root 540 Jul 21 08:18 samplefile2

[root@server1 ~]#
```

> 注意 6
如果在解压过程中有任何文件被覆盖，`uncompress` 命令会提示你确认。为了防止此提示，你可以使用 `uncompress` 命令的 `-r` 选项。

# 第11章 压缩、系统备份与软件安装

在使用 `uncompress` 命令时，可以省略 `.z` 扩展名。`uncompress -v samplefile sample2` 命令的效果与上述输出中显示的命令相同。

此外，压缩工具是一种过滤器，可以从标准输入（Standard Input）接收信息并发送到标准输出（Standard Output）。例如，要将 `who` 命令的输出发送压缩工具并将压缩结果保存为 `file.Z`，你可以执行以下命令：

```
[root@server1]# who | compress -v file.Z

Compression: 17.0%

[root@server1]# _
```

之后，你可以使用 `zcat` 命令显示 `file.Z` 的内容，或使用 `uncompress` 命令将其解压，如下输出所示：

```
[root@server1]# zcat file.Z

root pts/1 Jul 20 19:22 (3.0.0.2)

root tty5 Jul 15 19:03

root pts/2 Jul 17 19:58

[root@server1]# uncompress -v file.Z

file.Z - replaced with file

[root@server1]# _
```

表 11-1 压缩工具常用选项摘要

| 选项 | 描述 |
| :--- | :--- |
| -c | 与 `uncompress` 命令配合使用时，将压缩文件的内容显示到标准输出（与 `zcat` 功能相同）。 |
| -f | 与 `compress` 命令配合使用时，用于压缩链接文件。与 `uncompress` 命令配合使用时，将覆盖现有文件而不提示用户。 |
| -r | 指定压缩或解压指定目录内的所有文件。 |
| -v | 在压缩和解压期间显示详细输出（压缩率和文件名）。 |

### GNU zip

`zip` 是一种 Lempel-Ziv (LZ7) 压缩算法，与 `compress` 使用的略有不同。通常，它比 `compress` 使用的具有更好的压缩效果。和 `compress` 一样，`gzip` 使用 `.gz` 扩展名。此外，除非指定 `-f` 选项，否则会保留文件的所有者、修改时间和访问时间。

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

`gzip` 相比 `compress` 的优势之一是可以通过数字选项控制压缩级别。另一种，`-9` 选项被称为“最佳压缩”，以牺牲时间为代价获得更低的压缩率。如果没有指定压缩级别，`gzip` 命令假设使用 `-6` 选项。
以下命令使用快速压缩压缩先前的 `samplefile` 并显示压缩率：

### GNU zip

CompTIA Linux+ 和 LPIC-1：Linux 认证指南

或者，在解压文件时你可以使用 `.gz` 扩展名，如下输出所示：

```
[root@server1 ~]# gzip -v samplefile sample2

samplefile.gz:

  82.2% -- replaced with sample

samplefile.gz:

  65.0% -- replaced with sample2

[root@server1 ~]#
```

要解压上述输出中的文件，可以使用 `gzip` 的 `-d` 选项或 `gunzip` 命令，如下输出所示：

```
[root@server1 ~]# gunzip -v file.gz

file.gz:

  6.9% -- replaced with file

[root@server1]#
```

`uncompress` 命令在解压过程中有任何文件被覆盖时会提示你。除非指定 `-f` 选项，否则会覆盖现有文件。在解压文件时你可以使用 `.gz` 扩展名，如下例所示：

```
[root@server1 ~]# ls -l

total 20

drwxr-xr-x 3 root root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root root 219 Jul 21 08:15 sample2.gz

-rw-r--r-- 1 root root 4898 Jul 21 08:15 samplefile.gz

[root@server1 ~]# gzip -v samplefile sample2

samplefile.gz:

  82.2% -- replaced with sample

samplefile.gz:

  65.0% -- replaced with sample2

[root@server1 ~]# ls -l

total 28

drwxr-xr-x 3 root root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root root 27288 Jul 21 08:15 samplefile

-rw-r--r-- 1 root root 540 Jul 21 08:18 samplefile2

[root@server1 ~]#
```
