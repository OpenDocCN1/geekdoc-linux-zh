
要安装远程（网络或远程主机连接）打印机，你需要在打印机主机和打印机的 `/etc/printcap` 文件条目中放置条目。`rm` 条目识别控制远程打印机主机，`rp` 条目指定远程打印机的设备名称。在以下示例中，远程打印机位于 `rabbit.mytrek.com`，并称为 `lp1`：

```
:rm=rabbit.mytrek.com
:rp=lp1
```

### 配置远程打印机

要安装远程（网络或远程主机连接）打印机，你需要在打印机主机和打印机的 `/etc/printcap` 文件条目中放置条目。`rm` 条目识别控制远程打印机主机，`rp` 条目指定远程打印机的设备名称。在以下示例中，远程打印机位于 `rabbit.mytrek.com`，并称为 `lp1`：

```
:rm=rabbit.mytrek.com
:rp=lp1
```

### 配置远程打印机

要安装远程（网络或远程主机连接）打印机，你需要在打印机主机和打印机的 `/etc/printcap` 文件条目中放置条目。`rm` 条目识别控制远程打印机主机，`rp` 条目指定远程打印机的设备名称。在以下示例中，远程打印机位于 `rabbit.mytrek.com`，并称为 `lp1`：

```
:rm=rabbit.mytrek.com
:rp=lp1
```

### 配置远程打印机

要安装远程（网络或远程主机连接）打印机，你需要在打印机主机和打印机的 `/etc/printcap` 文件条目中放置条目。`rm` 条目识别控制远程打印机主机，`rp` 条目指定远程打印机的设备名称。在以下示例中，远程打印机位于 `rabbit.mytrek.com`，并称为 `lp1`：

```
:rm=rabbit.mytrek.com
:rp=lp1
```

### 配置远程打印机

要安装远程（网络或远程主机连接）打印机，你需要在打印机主机和打印机的 `/etc/printcap` 文件条目中放置条目。`rm` 条目识别控制远程打印机主机，`rp` 条目指定远程打印机的设备名称。在以下示例中，远程打印机位于 `rabbit.mytrek.com`，并称为 `lp1`：

```
:rm=rabbit.mytrek.com
:rp=lp1
```

### 配置远程打印机

要安装远程（网络或远程主机连接）打印机，你需要在打印机主机和打印机的 `/etc/printcap` 文件条目中放置条目。`rm` 条目识别控制远程打印机主机，`rp` 条目指定远程打印机的设备名称。在以下示例中，远程打印机位于 `rabbit.mytrek.com`，并称为 `lp1`：

```
:rm=rabbit.mytrek.com
:rp=lp1
```

### 配置远程打印机

要安装远程（网络或远程主机连接）打印机，你需要在打印机主机和打印机的 `/etc/printcap` 文件条目中放置条目。`rm` 条目识别控制远程打印机主机，`rp` 条目指定远程打印机的设备名称。

### 远程连接打印机是远程打印机。

```
:rm=rabbit.mytrek.com
:rp=lp1
```

## 第 30 章：设备与打印机

`lpr`、`lpq`、`lprm` 和 `lpc` 等打印客户端会发出各种服务请求。`lpq` 会请求队列信息，其 `SERVICE` 键值为 `Q`。`lprm` 会发出由键值 `M` 指定删除请求。`SERVICE` 键的不同服务值所示：

| 键值 | 服务请求 |
| --- | --- |
| X | 连接请求 |
| R | 任务暂存 (Job spool) |
| P | 打印 |
| Q | 队列状态信息 (lpq) |
| M | 删除请求 (lprm) |
| C | 打印机控制 (lpc) |
| S | 打印机状态 (lpc) |

对于引用打印作业控制文件中键以及由 `lpr` 或 `lpq` 等命令提供的键进行了进一步的区分。例如，`HOST` 键引用打印作业控制文件中的主机名，允许你拒绝或接受打印请求。对于除 `lpr` 外的所有类型请求，`REMOTEHOST` 将直接引用从远程连接派生的主机。检查 `lpd.perm` 或 `lpd` 手页中的键表，可以获得请求及其接收信息类型的详细说明。另一个示例是，`SAMEUSER` 将打印作业请求（如状态或删除）中指定的用户与该作业控制中的用户进行对比，以确保他们是同一个人。

`/etc/lpd.perms` 文件的设置所示。该文件本身包含详细文档以及若干条注释推荐条目。

```
# 允许服务器上的 root 控制打印作业
ACCEPT SERVICE=C SERVER REMOTEUSER=root
# 允许任何人获取服务器、状态和打印能力
ACCEPT SERVICE=C LPC=lpd, status, printcap
# 拒绝所有其他
REJECT SERVICE=C
#
# 允许源主机上的相同用户删除用户
ACCEPT SERVICE=M SAMEHOST SAMEUSER
# 允许服务器上的 root 删除作业
ACCEPT SERVICE=M SERVER REMOTEUSER=root
REJECT SERVICE=M
# 允许所有其他操作
DEFAULT ACCEPT
```

## 打印队列客户端

如前所述，系统的打印由一个名为 `lpd` 的打印守护进程处理，该进程一直在运行，等待打印作业并管理它们的打印程序。`lpd` 守护进程将其作业放在打印队列中。一旦进入队列，你可以使用几个客户端来管理打印作业，例如 `lpq`（列出队列）、`lpc`（可以重新排序）以及 `lprm`（可以删除打印作业，实际上是取消）。文档最初通过 `lpr` 打印命令提交给 `lpd`。

`lpr` 提交作业，然后 `lpd` 轮流处理并在相应的打印队列上运行它。`lpr` 以文件名作为参数。你也可以通过标准输入向 `lpr` 提供数据，将从其他源管道打印的数据。`-p` 选项允许你指定特定的打印机。在下一个示例中，用户打印第一个文件 `preface`，然后使用 `cat` 命令生成文件和摘要的合并输出，然后打印。最后，用户将文件 `report` 打印到名为 `mySocket` 的打印机。

```
$ lpr preface
$ cat intro digest | lpr
$ lpr -P myreport report
```

如果 `lpr` 命令没有指定打印机，则使用默认打印机。这由 `lpd.conf` 中的 `default_printer` 属性、`PRINTER` 变量以及 `/etc/printcap` 文件中的第一个条目决定。

你也可以将输出重定向到打印机的设备文件来打印。这不会在打印队列中放置任何内容。打印操作变成立即执行的命令。然而，在文件完成打印之前，你的系统会被占用。以下示例使用此技术将 `report` 文件打印到连接到设备 `lpr1` 的打印机：

```
$ cat report > /dev/lp1
```

要管理打印机上的打印作业，你可以使用 `Klpq` 或 LPR 客户端 `lpc`、`lpq` 和 `lprm`。`Klpq` 是一个 KDE 桌面工具，标记为打印作业管理工具（见图 30-1）。通过 `Klpq`，你可以列出打印机的打印作业、删除作业并将打印作业移动到队列顶部。你还可以禁用打印机的打印功能。为了让打印队列列表更新，你可以在选项（Options）菜单中设置更新频率。

你可以使用 `lpc` 启用或禁用打印机、重新排序并删除打印作业。

# 使用 CUPS 安装和管理打印机

通用打印系统（CUPS）是 LPRng 的替代方案，提供打印服务。它在 GNU 公共许可证下免费提供。虽然现在它已包含在大多数发行版中，但你也可以从其网站 `www.cups.org` 下载最新版本的 CUPS 源码版本。该网站还提供了关于安装和管理打印机的详细文档。LPRng 衍生自旧的伯克利打印守护进程（LPD），而 CUPS 基于较新的互联网打印协议（IPP）。互联网打印协议旨在为互联网建立一种标准（更多信息，请访问 `www.pwg.org/`）。旧的基于 LPD 的打印系统主要关注行式打印机，而基于 IPP 的系统提供了网络、Postscript 和 Web 支持。CUPS 的工作方式类似于 Apache 服务器，并采用与 Apache 服务器非常类似的配置设置，而无需配置打印机本身。配置只需要在打印服务器上维护。

要安装 CUPS，你必须卸载 LPRng。对于像 Mandrake、Caldera 和 Red Hat 这种使用 RPM 的发行版，请使用 `rpm -e` 命令删除这些应用程序。请记住，在删除 LPRng 之前你可能需要备份所有内容。你可能想要保存 `/etc/cups` 文件，因此可以使用 `rpm -i` 命令安装 CUPS。

在 Mandrake 和 Red Hat 的 RPM 版本中，cups 启动脚本被安装在 `/etc/rc/init.d` 目录中。你可以使用 `service` 命令和 `cups` 脚本来启动、停止和重新启动 CUPS。当你做出更改或安装打印机时，请务必重启 CUPS 以使更改生效。在 Mandrake 和 Red Hat 上，你可以使用以下：

```
service cups restart
```
