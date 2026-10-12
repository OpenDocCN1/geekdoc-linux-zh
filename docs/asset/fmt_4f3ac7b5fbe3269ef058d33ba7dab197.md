
```
Printer: printer@linux 1pdfilter drv=upp method=auto color=yes\Queue: 2 printable jobs
Server: pid 7855 active
Unspool: pid 7859 active
Status: cannot open '192.168.0.101:9100' - 'Connection refused', attempt 160, sleeping 10 at 14:49:57.897
Rank Owner/ID Class Job Files Size Time
stalled(172sec) root@linux+242 A 242 edul.txt 57486 07:31:01
2 root@linux+707 A 707 edul.txt 57486 14:17:08
```

# Novell 认证 Linux 专业人员学习指南

> 注意

`lpstat` 是一个与 `lpq` 具有相同基本旧旧实用程序。该工具用于检查 `lp` 服务和队列的状态。它适用于 LPRng，但不支持 CUPS。

`lprm` 工具用于从队列中删除打印作业。使用它时，它会根据作业号发送删除作业的请求。如果没有给出作业号，它将尝试删除你提交的最后一个作业。该工具的运行示例如图 9.11 所示。

## 图 9.11

`lprm` 实用程序删除池化的打印作业。

![](img/38aae1e03db8863dab67582599f6fc83_309_0.png)

在这种情况下，用户提交的最近作业已被删除。`lprm` 工具可以使用用户名作为选项来删除该用户提交的作业。

`lpadmin` 工具允许你从命令行执行大部分在 YaST 中可以完成的配置。图 9.12 显示了它可用的所有选项。

该工具的补充是 `lpoptions`，它用于从命令行修改网络打印机。可以使用它的的一些选项包括：

- `-d` 设置默认打印机
- `-h` 指定 CUPS 服务器
- `-p` 设置目标和实例

## 打印 第 9 章

## 图 9.12

使用 `lpadmin`，你可以从命令行修改打印机设置。

![](img/38aae1e03db8863dab67582599f6fc83_310_0.png)

如果你在网络上共享打印机，还有其他几点可能有用，尽管它们不是实用程序：

- `/etc/hosts.lpd`——此文件包含允许访问打印机的主机名。
- `/etc/hosts.equiv`——此文件包含允许访问此机器（而不仅仅是打印机）的主机名。

从命令行启用和禁用打印可以使用 `/usr/bin/enable` 和 `/usr/bin/disable` 命令。每个命令必须后跟你要启用/禁用的打印机名称。如果你希望打印机在接受额外作业之前完成队列中的任务，可以使用 `/usr/sbin/reject`（其反操作是 `/usr/sbin/accept`）。

CUPS 服务有两种方式停止：使用命令 `/etc/init.d/cups stop` 或 `service cups stop`。这些操作的反操作是通过使用 `start` 完成的。

`lpadmin` 实用程序用于为 CUPS Web 管理工具添加密码。如果你在命令行输入该命令，将提示输入密码。你提供的密码必须要有 6 个字符长，且必须包含至少一个字母和一个数字。在命令行可以提供的选项有 `-g` 指定组，以及 `-a` 或 `-x` 指定用户名。对于 Web 管理工具，你需要运行：

```
passwd -g sys -a root
```

访问 Web 管理工具只需访问服务器上的端口 631。图 9.13 显示了当你访问此端口时出现的屏幕。这些工具允许你远程管理打印机和作业，以及添加/管理类、管理作业和添加/管理打印机等任务。

## 图 9.13

可以通过端口 631 访问 Web 管理工具。

![](img/38aae1e03db8863dab67582599f6fc83_311_0.png)

最后一点注意的是 `/var/log/cups/error` 文件是写入 CUPS 守护进程错误信息的地方。`access` 显示所有访问。在需要确定打印机不可用的故障排除情况下，两者都很有用。

## 摘要

本章重点关注考试所需的关于打印和通用打印管理的主。

## 命令摘要

表 9 列出了本章讨论的命令。

| 实用程序 | 用途 |
| --- | --- |
| lp | 向打印服务提交作业的原始工具 |
| lpadmin | 从命令行处理打印机配置 |
| lpc | 管理打印服务的主要工具 |
| lpoptions | 从命令行修改网络打印机的工具 |
| lpasswd | 为 Web 管理工具配置身份验证选项的工具 |
| lpq | 查看打印队列内容和状态的主要工具 |
| lpr | lp 的副本，允许你提交打印作业 |
| lprm | 删除打印作业的工具 |
| pr | 在将文件发送到打印机之前进行处理的工具 |

## 回顾管理任务

RPM 系统管理最早出现在本书的第 5 章“基础 Linux 管理”。说实话，系统管理主题贯穿本书。你学习的是管理员考试——而不是程序员或开发者。

本章查看了许多主题，包括包管理和安全。它涵盖了以下课程目标：

1. 执行 RPM 包相关操作 (3036)
2. 使用基础 Linux 命令 (3036)
3. 监控你的 SLE 9 系统 (3037)
4. 管理 RPM 软件包 (3037)
5. 验证并更新软件库 (3037)
6. 管理内核 (3037)
7. 创建安全概念 (3038)
8. 限制对服务器系统的物理访问 (3038)
9. 限制已安装的软件包 (3038)
10. 确保文件系统安全 (3038)
11. 使用 ACL 进行高级访问控制 (3038)
12. 安全问题 (3038)
13. 应用安全更新 (3038)
14. 为 SLES 9 系统添加新硬件 (3038)

## 安装软件

涵盖课程目标

6. 管理内核 (3037)

Linux 社区有几种主要的软件发行方法。一种是使用包管理系统，我们稍后查看。另一种是使用压缩的“tarball”文件。tarball 是包含一组文件 tar 镜像的单个文件。

你知正在处理的是 tarball 或压缩 tarball，是因为文件名结尾有 `.tar` 或 `.tar.gz`。例如，以下文件是 tarballs：

```
program-1-2-3.tar.gz
program-1-2-3.tar
```

但下面的示例不是：

```
program-1.2.3.rpm
```

要安装 tarball，你必须首先识别要安装的软件并从提供者获取。例如，从 ftp.ccil.org 获取 wumpus，我们使用示例所示的 ftp：

```
ftp> bin
200 Type set to I.
ftp> get wumpus-1.3.tar.gz
local: wumpus-1.3.tar.gz remote: wumpus-1.3.tar.gz
227 Entering Passive Mode (192,190,237,102,124,145)
150 Opening BINARY mode data connection for wumpus-1.3.tar.gz
--> (9293 bytes).
226 Transfer complete.
9293 bytes received in 0.20 secs (44 Kbytes/sec)
ft>
```

这在你的系统中产生了 `wumpus-1.3.tar.gz`，它必须被压缩并解压。你可以分一步或两步完成。传统使用的两步方法涉及解压缩文件然后解压文件。这是使用以下命令的：

```
# gzip -d FILE
# tar xvf FILE
```

## 301

回顾管理任务

第 10 章

这些命令中的第一个是解压缩文件，第二个是执行提取。由于这是一种非常常见的软件发布方式，Linux 自带的 GNU 版本的 `tar` 包含一个解压缩归包并提取文件的功能。使用以下命令完成：

```bash
# tar xvzf FILE
```

> `z` 选项用于通过 gzip 过滤归包。

`tar` 的 `v` 选项会在提取文件时列出归包中的所有文件。如果你不想看到文件列表，只需省略 `v` 即可。`x` 告诉 `tar` 提取文件，而 `f` 则标识要提取的文件：
