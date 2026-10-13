
| `exit` | 退出 LAN Manager 服务器 |

| `get` `rfile` `lfile` | 将远程文件 (`rfile`) 复制到本地文件 (`lfile`) |

| `help` `cmd` | 提供命令帮助（或显示命令列表） |

| `lcd` `newdir` | 切换本地目录（在 Linux PC 上） |

| `lowercase` | 切换文件名自动小写转换 |

| `ls` `files` | 列出服务器上的文件 |

| `mask` `name` | 对文件操作应用掩码（如 `*`） |

| `md` `dirname` | 在服务器上创建目录 |

| `mget` `name` | 获取所有匹配名称的文件（如 `*.doc`） |

| `mkdir` `dirname` | 创建目录 |

| `mput` `file` | 将文件从 Linux PC 复制到服务器 |

| `newer` `file` | 获取比指定文件更新的文件 |

| `print` `name` | 打印命名文件 |

| `printmode` `mode` | 设置打印模式（模式必须是文本或图形） |

| `prompt` | 切换提示关闭（类似于 ftp 中的命令） |

| `put` `lfile` `rfile` | 将本地文件 (`lfile`) 复制到远程文件 (`rfile`) |

| `queue` | 显示打印队列 |

| `quit` | 退出 LAN Manager 服务器 |

| `rd` `dir` | 删除服务器上的指定目录 |

| `recurse` | 在文件 `get` 和 `put` 操作期间切换目录递归 |

| `rm` `name` | 删除所有指定名称的文件 |

| `rmdir` `dirname` | 删除指定的目录 |

| `translate` | 切换文本翻译（将换行符转换为回车-换行符对） |

### LAN Manager

如果你将一台 Linux PC 引入现有的 LAN Manager 环境，你可能需要将该 Linux PC 作为 LAN Manager 客户端，因为可能已经存在一个服务器。如前几节所述，Samba 软件包包包含了 `smbclient` 程序，它允许你的 Linux PC 成为 LAN Manager 网络中的客户端。

在本节中，我将向你展示如何在 Linux PC 上设置打印机，以便通过 `smbclient` 程序将打印作业发送到指定的 LAN Manager 服务器。第 14 章描述了 Linux 打印系统的工作原理。如果你在阅读本节时对打印有任何疑问，请参考该章节。

### 分两步设置打印机

基本思想是在你的 Linux PC 上定义一个新的打印机，这样当你使用 `lpr` 命令向该打印机打印时，输出实际上出现在指定的网络打印机上（由 LAN Manager 服务器管理）。这个过程涉及两个步骤：

- 1. 在 `/etc/printcap` 文件中为打印机添加条目，并指定输入过滤器（一个处理正在打印文件的脚本）。
- 2. 编写运行 `smbclient` 指定的 LAN Manager 服务器上打印文件的脚本。

### 添加 printcap 条目

在准备打印到 LAN Manager 打印机的 `printcap` 条目时，请注意两个关键点：

- 指定 `/dev/null` 为打印机设备名称，因为实际打印发生在网络打印机上。
- 指定一个输入过滤器，将输入数据复制到文件中，然后使用 `smbclient` 将该文件发送到选定的 LAN Manager 服务器。

以下是我在 PC 上指定此打印机的 `printcap` 条目（在 `/etc/printcap` 文件中）：

```
|smbprint|在 LAN Manager 打印机上打印:
:sd=/var/spool/lpd/lpd:
:lpr=/dev/null:
:if=/var/spool/lpd/lp/smbprint.tcl:
:lf=/var/spool/lpd/lp/smbprint.log:
:mx#0:
:sh:
:sf:
```

为了记录错误，我使用以下命令（以 root 身份登录时）创建了 `/var/spool/lpd/lp/smbprint.log` 文件：

![](img/a5afb9ccf4a412511e9fcfa4280141e3_677_0.png)

![](img/a5afb9ccf4a412511e9fcfa4280141e3_677_1.png)

## 第 21 章：使用 Linux 经营

```
cd /var/spool/lpd/lp
touch smbprint.log
chmod ug=rw-r smbprint.log
```

## 编写使用 smbclient 打印的脚本

下一个重要步骤是编写输入过滤器 `--var/spool/lpd/lp/smbprint.tcl`，它执行实际打印。作为扩展，我使用 Tcl 来编写输入过滤器。你也可以用 Perl 或 bash 编写脚本。

在 `smbprint.tcl` 脚本中，我决定将打印作业复制到临时文件中，然后运行 `smbclient` 打印该文件。以下是完整的 `/var/spool/lpd/lp/smbprint.tcl` tcl 脚本：

```tcl
#!/usr/bin/tcl
# 使用 smbclient 在 LAN manager 打印机上打印的 Tcl 脚本
# 放置在打印机队列目录并对所有人可执行

# 打开文件 /tmp/smbprint.out
set outfile [open /tmp/smbprint.out w]

# 从 stdin 读取并写入 outfile
while {[gets stdin line] != -1} {
  puts outfile $line
}
close outfile

# 现在准备一个脚本运行 smbclient 并打印文件
set server "inb486"
set printer "hplj4m"
set password "mypassword"

set outfile [open /tmp/printit w]
puts outfile "#!/bin/sh"
puts outfile "echo print /tmp/smbprint.out | /usr/bin/smbclient \\\$server \\\$printer \$password N -p\*"
close outfile

# 使脚本变为可执行
exec chmod +x /tmp/printit

# 现在执行脚本
exec /tmp/printit
# 删除脚本
exec rm /tmp/printit
```

## 第四部分：使用 Linux 享乐与盈利

我以一种简单的方式编写了该脚本：将打印作业复制到临时文件，创建一个运行 `smbclient` 打印该文件的脚本，然后运行该脚本。我已使用这种打印机设置直接从 Linux 程序（如 Netscape）打印到该网络打印机。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_679_0.png)

本章提供了 Samba 的概述，但没有足够的空间提供所有可用信息。关于如何使用 Samba 的更多信息，请参阅 John Blair 的 *Samba: Integrating UNIX and Windows*, SSC, 1998。

### 特定业务中的 Linux

在特定章节中，我描述了若干项适合作为 Linux 选择的具体任务。接下来的几节将关注 Linux 最有意义的特定业务。当我描述在业务中使用 Linux 时，我也会提到你可能考虑使用 Linux 执行哪些任务。

### 互联网服务提供商

互联网服务提供商（ISP）是一种相对新的业务类型，随着越来越多的个人和企业想要连接互联网，这种业务应运而生。在 20 世纪 90 年代初，许多 ISP 为个人用户提供拨号调制器账户。然后，随着互联网变得流行，ISP 开始提供基于 ISDN（综合业务数字网络）的 SLIP 和 PPP，以及提供完整 TCP/IP 网络的其他高速连接。（有关 SLIP 和 PPP 的更多信息请参阅第 18 章。）

如今，大多数 ISP 维护到 Sprint 和 MCI 等大型电信公司的 T1 链路。（T1 链路每秒能够传输 154 万比特数据——比 28800 bps 调制器的传输速度快 50 多倍）。客户通常通过高速拨号调制器使用 SLIP/PPP。

除了各种电信设备（包括调制器），ISP 还需要处理 SLIP/PPP 的服务器以及拨号连接。这正是 Linux 发挥用场的地方。

## 第四部分：为了乐趣和利润使用 Linux

### UNIX 软件人员

如果你的业务为 UNIX 和 X Window 系统开发应用程序，那么你应该拥有在 PC 上安装和设置 Linux 的内部技术知识。由于 Linux 自带有一整套软件开发工具，Linux PC 可以作为每位软件开发人员的工作站。

尽管 Linux 软件发行版包含许多编程语言，但 Linux PC 是开发 UNIX 应用程序的理想选择。如今，大多数应用程序都是图形化的，在 Linux 上，你会使用 XFree86 X Window 系统处理图形。配套 CD-ROM 包含了开发 X 应用程序所需的所有头文件和库。
