
在下面的示例中，该命令取消用户 bcal... 在所有打印机上提交的所有打印请求：

```
cancel -u bcal... 
request "asteroid-3" cancelled
request "luna-8" cancelled
```

## 更改打印请求的优先级

使用以下 lp 命令更改打印请求的优先级：

```
lp -i <request-id> -H <change-priority>
```

lp 命令的选项在表 10.12 中描述。

表 10.12
lp 选项

| 选项 | 描述 |
|---|---|
| -i <request-id> | 您想要更改的打印请求的请求 ID。您可以使用此命令指定多个请求 ID。用空格或逗号分隔请求 ID。如果使用空格，请用引号将请求 ID 列表括起来。 |
| -H <change-priority> | 更改打印请求优先级的三种方式之一：hold、resume 或 immediate：hold 将打印请求置于保留状态，直到您取消它或指示 LP 打印服务恢复打印该请求。resume 将已在队列中保留的打印请求放入队列。它将根据其优先级和在队列中的位置进行打印。如果您对正在打印的打印作业设置了保留，resume 会将打印请求置于队列头部，使其成为下一个打印的请求。immediate 将打印请求置于队列头部。如果请求正在打印，您可以将其置于保留以允许下一个请求立即打印。 |
| -q < priority-level > | 为打印请求分配打印队列中的优先级。将 <priority-level> 指定为 0–39 的整数。使用 0 表示最高优先级，使用 39 表示最低优先级。 |

在下面的示例中，命令将请求 ID 为 eps1-29 的打印请求更改为优先级级别 1：

```
lp -i eps1-29 -q 1
```

## 重新启动打印调度程序

打印调度程序 lpsched 处理打印服务器上的打印请求。如果打印机没有输出，则可能需要重新启动打印调度程序。要重新启动打印调度程序，请使用 lpsched 命令。如果打印调度程序停止运行时正在打印打印请求，则在重新启动打印调度程序时，该请求将完整打印。

首先，通过键入以下内容停止调度程序：

/usr/lib/lp/lpshut

要重新启动调度程序，请键入以下内容：

/usr/lib/lp/lpsched

lp 系统由名为 lp 的 /etc/init.d 脚本启动。此文件到 /etc/rc2.d 目录的链接可确保 lp 服务在系统每次启动时自动启动。可以使用以下命令使用同一脚本重置整个 lp 服务：

/etc/init.d/lp stop

lp 服务将被停止。您可以使用以下命令重新启动 lp 服务：

/etc/init.d/lp start

> NOTE
/etc/init.d/lp 脚本启动和停止整个打印服务，而不仅仅是调度程序。使用 lpshut 和 lpsched 仅停止和重新启动调度程序。

## 设置用户的默认打印机

当您添加打印机时，您可以选择将该打印机设为该特定系统的默认打印机。您可能希望在用户级别设置默认打印机，以便在特定系统上，用户可以指定自己的默认打印机。如果用户在发送打印作业时未提供打印机名称，打印命令将按以下顺序搜索默认打印机：

1. LPDEST 变量
2. PRINTER 变量
3. 系统的默认打印机

这些变量可以在用户的 .profile 文件中设置。lp 命令检查 LPDEST，然后检查 PRINTER。如果未设置任何变量，则将在以下文件中检查名为 _default 的变量：

$HOME/.printers

在此文件中将 printer1 命名为默认打印机的条目如下所示：

```
default printer1
```

如果 $HOME/.printers 文件不存在，则会检查 /etc/printers.conf 文件。此文件中的条目如下所示：

```
_default|lp:
:use=system1:
:bsdaddr=system1,printer1
```

如果在 /etc/printers.conf 文件中未设置 _default 变量，则如果您正在运行名称服务，则会检查名称服务数据库，如第 18 章“名称服务”所述。如果无法在这些文件中找到目标打印机名称，则无法处理打印请求。

## 使用 Admintool 修改打印机

在将打印机添加到系统后，可以使用 Solaris Admintool 修改打印机。可以通过 Admintool 对打印机进行的修改包括以下内容：

- 给打印机描述
- 指示打印机端口
- 列出文件内容
- 提供故障通知
- 选择默认打印机
- 打印横幅
- 接受和处理打印请求
- 提供用户访问列表

要通过 Admintool 修改打印机，请从 Printers 窗口中选择 Edit、Modify，如图 10.7 所示。

Modify Printer 窗口出现，如图 10.8 所示。

![](img/df66a0e1cd473c73297ad9cbd0cb0cb8_444_0.png)

图 10.7
Printers 窗口。

![](img/df66a0e1cd473c73297ad9cbd0cb0cb8_444_1.png)

图 10.8
Modify Printer 窗口。

通过在 Modify Printer 窗口中选择或填写适当的字段来修改所选打印机。

## 章节摘要

### 关键术语

- Spool
- Print daemon
- Network printer
- Print queue
- Local printer
- Lpsched
- Lpd
- Print server
- Print client
- Default printer
- Terminfo database
- Printer class
- Print scheduler

我们可以用大量时间描述 LP 打印服务。我们可以更深入地讨论配置打印机过滤器、创建 terminfo 数据库和排除打印问题，但这超出了本培训指南的范围。为了准备认证考试和基本系统管理，您需要了解 LP 打印服务的基础知识。这包括打印 spooler、打印守护进程和打印机配置文件。此外，您还需要知道这些文件和程序在 Solaris 8 目录结构中的存储位置。

除了了解 LP 打印服务之外，您还需要知道如何使用所有用于管理 LP 打印服务的实用程序和程序。

我响应的大多数系统问题都与打印机有关。您还应该熟悉第三方应用程序以及它们如何准备打印作业以发送到 spooler。我遇到的许多问题并非 Solaris 打印服务的问题，而是在应用程序格式化打印作业的方式。本章向您介绍了 Solaris 打印系统和 lpsched 守护进程。打印机也可以在网络环境中使用 Solstice AdminSuite 进行管理，见第 19 章“ Solaris Management Console 和 Solstice AdminSuite”。第 9 章“进程控制”探讨了所有 Solaris 进程。有关 lpsched 守护进程的更详细讨论，请参阅 Answerbook2 在线手册中的 Solaris 8 System Administration Guide, Volume II。

## 应用你的知识

### 练习

#### 10.1 使用 lpadmin 配置打印机（命令行）

本练习将向您展示如何在打印服务器上添加和删除本地 LaserJet 5M 打印机。此示例中的命令必须在打印机连接的打印服务器上执行。安装可用的信息如下：

- Printer name: hp1
- Port device: /dev/ecpp0
- System type: Ultra5
- Printer type: HP LaserJet5M
- File content type: PostScript/PCL

预计时间：10 分钟

1. 以 root 身份，使用 lpadmin 命令将名为 hp1 的打印机添加到并行端口（在 ultra 系统上为 /dev/ecpp0，在 sparc 系统上为 /dev/bpp0），将打印机类型设为 hplaser，并将文件内容类型指定为 any：

```
lpadmin -p hp1 -v /dev/ecpp0 -T hplaser -I \
any
```

现在，开始接受打印机的打印请求并启用打印机。

```
enable hp1
accept hp1
```

2. 验证打印机是否已设置并准备就绪：

```
lpstat -p hp1 -l
```

3. 现在发送打印作业到打印机以测试它：

```
lp -d hp1 /etc/hosts
```

4. 删除打印机：

```
lpadmin -x hp1
```

5. 验证是否已删除：

```
lpstat -t
```

#### 10.2 使用 AdminTool 配置打印机（GUI）

在本练习中，使用 Admintool 将 LaserJet 5M 打印机添加到打印服务器。

预计时间：5 分钟

1. 以 root 身份启动 Admintool。

```
admintool &
```

2. 从 Admintool 窗口顶部的 Browse 按钮中，从下拉菜单中选择 Printers。

3. 从 Admintool 窗口顶部的 Edit 按钮中，选择 Add，然后从下拉菜单中选择 Local Printer。按如下方式填写字段：

- Printer Name: hp1
- Description: Hplaser 5M
- Printer Port: /dev/ecpp0 (/dev/bpp0 on a Sparc system)
- Printer Type: HP Printer
- File Contents: Any

完成后单击 OK，然后退出 Admintool。

4. 通过键入以下内容验证打印机是否已设置并准备就绪：

```
lpstat -p hp1 -l
```
