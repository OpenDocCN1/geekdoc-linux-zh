
`disable printer-name`
禁用新作业的队列。如果打印机正在运行，它将继续打印队列中剩余的作业。超级用户（`root`）始终可以提交作业，即使是对禁用的队列。
此命令在你测试新打印机或安装过滤器程序时非常有用：禁用队列并以 `root` 身份提交作业。在测试完成测试并使用 `enable` 命令重新启用队列之前，其他用户将无法提交作业。

`down printer-name message`
关闭打印机。等同于先执行 `disable` 后执行 `stop`。每当用户使用 `lpc(1)` 检查打印队列或使用 `lpc status` 状态时，消息将作为打印机的状态显示。

`enable printer-name`
启用打印机的队列。用户可以提交作业，但在打印机启动之前它不会打印任何内容。

`help command-name`
打印命令 `command-name` 的帮助信息。如果没有 `command-name`，则打印可用命令的摘要。

`restart printer-name`
启动打印机。如果在特殊情况下 LPD 挂起，普通用户可以使用此命令，但他们无法通过 `stop` 或 `down` 命令启动已停止的打印机。`restart` 命令等同于先执行 `abort` 后执行 `start`。

`start printer-name`
启动打印机。打印机将打印队列中的作业。

`stop printer-name`
停止打印机。打印机将完成当前作业不再打印队列中的其他内容。尽管打印机已停止，用户仍然可以向启用的队列提交作业。

`topq printer-name job-of-username`
通过重新排列 `printer-name` 的队列，将列出的作业号或属于 `username` 的作业置于队列顶部。对于此命令，你不能使用 `all` 作为 `printer-name`。

`up printer-name`
启动打印机；是 `down` 命令的相反操作。等同于先执行 `start` 后执行 `enable`，`lpc(8)` 接受在命令行输入上述命令。如果你不输入任何命令，`lpc(8)` 将进入交互模式，你可以在其中输入命令，直到退出、终止或遇到文件结束符。

## 9.6 标准打印池生成器的替代方案

如果你一直在阅读本手册，到目前为止你已经学习了关于 FreeBSD 自带的 LPD 打印系统的所有知识。你可能已经发现了它的许多缺点，这自然引出了我们一个问题：“还有哪些打印池系统？”

### LPRng

LPRng 是 LPD 的替代品，是对 LPR 守护进程的重写。LPRng 的主页为 http://www.lprng.org。

### CUPS

CUPS（通用打印系统）为管理打印机提供了一个可移植的层。CUPS 的主页为 http://www.cups.org。

## 9.7 故障排除

在使用 `lpstest(1)` 进行简单测试后，你可能会得到以下结果之一：

你成了阶梯效应的另一个受害者，这是由于对什么字符应该指示新行的解释冲突引起的。Unix 风格的操作系统使用单个字符：ASCII 10 和换行符（LF）。MS-DOS、OS/2 以及其他使用一对字符，ASCII 10 和 ASCII 13（回车或 CR）。许多打印机使用 MS-DOS 约定表示新行。

当你使用 FreeBSD 打印时，你的文本使用了换行符。打印机看到换行符后，向上移动一行，但保持下一个打印字符的水平位置不变。这就是回车的作用：将下一个打印字符的位置移动到纸张的左边缘。

这里是 FreeBSD 希望你的打印机做的：

| 打印机接收 | 打印机打印 |
| :--- | :--- |
| CR | CR |
| LF | CR + LF |

这里是实现此目标的方法：

- 使用打印机的配置开关或控制面板来更改其对这些字符的解释。

> 注意：如果你从 FreeBSD 之外的其他操作系统启动系统，你可能需要重新配置打印机，以使用其他操作系统使用的 CR 和 LF 字符解释。你可能更倾向于下面的其他解决方案。

## 第 9 章 打印

- 让 FreeBSD 的串口驱动程序自动将 LF 转换为 CR+LF。注意，此功能仅适用于带有串口的打印机。要启用此功能，请使用 `ms#` 属性并在 `/etc/printcap` 文件中为打印机设置 `oncr` 模式。

- 发送转义码以临时区别对待 LF 字符。请咨询您的打印机手册了解您的打印机可能支持的内容。找到正确的转义码后，修改文本以发送该代码，然后打印。

这是一个适用于支持惠尔-太平洋 PCL 转义码打印机的示例过滤器。该过滤器让打印机将 LF 字符视为 LF 和 CR；然后合并作业；然后发送格式以进纸作业的最后一页。它应该适用于所有惠尔-太平洋打印机。

```
#!/bin/sh

# hpif - 适用于 HP-PCL 打印机的 lpdpd文本过滤器
# 安装在 /usr/local/libexec/hpif

# 简单的将 stdin 复制到 stdout。忽略所有过滤器参数。
# 告诉打印机将 LF 视为 CR+LF。完成后出纸页。

printf "\033\K2G" %% cat %% printf "\033\KG" %% exit 2
```

以下是一个名为 `orchid` 的主机的示例 `/etc/printcap`。它在并行端口上连接了一个打印机，是一台名为 `teak` 的惠尔-太平洋 LaserJet 35i。它使用上述脚本作为其文本过滤器：

```
# 主机 orchid 的 /etc/printcap
# teak|hp|laserjet Hewlett Packard LaserJet 35Si:
:ip=/dev/lpt0:sh=/var/spool/lpd/teak:mx0:\n:if=/usr/local/libexec/hpif
```

每行都重叠打印（Overprinted each line）。

打印机从未向下移动。所有行都重叠打印在同一行上。

这个问题是上述描述的“阶梯效应”的“相反”面，且罕见得多。在某些地方，FreeBSD 用于定义换行的 LF 字符被视为 CR，将打印位置返回到打印机的左边缘，但没有换行。

使用打印机的配置开关或控制面板强制执行以下对 LF 和 CR 字符的解释：

| 打印机接收 | 打印机打印 |
|---|---|
| CR | CR |
| LF | CR + LF |

打印机丢失字符（The printer lost characters）。

在打印过程中，打印机在每行中漏掉了几个字符。问题可能会随着打印机的运行而恶化，丢失的字符越来越多。

244

问题是打印机的速度无法跟上计算机通过串口发送数据的速度（使用并行端口的打印机不应出现这个问题）。有两种方法可以解决这个问题：

- 如果打印机支持 XON/XOFF 流控，通过在 `ms#` 属性中指定 `ixon` 模式让 FreeBSD 使用它。

- 如果打印机支持硬件流控（carry），请在 `ms#` 属性中指定 `crtscts` 模式。确保连接到打印机的电缆已为硬件流控正确接线。

打印出乱码（It printed garbage）。

打印机打印出的随机乱码，而不是所需的内容。

这通常是串口打印机通信参数错误的另一个症状。双击 `br` 属性中的 `bps` 波特率以及 `ms#` 属性中的校验设置；确保打印机使用的设置与 `/etc/printcap` 文件中指定的设置相同。

什么都没有发生（Nothing happened）。

如果什么都没有发生，问题可能在 FreeBSD 内部而不是硬件上。在 `/etc/printcap` 文件中为你正在调试的打印机条目添加日志文件（`lf`）属性。例如，这里是 `rattan` 的条目，带有 `lf` 属性：

```
rattan|line|diablo|lp|diablo 630 Line Printer:\nsh=/dev/var/lpd/rattan:
  if=/dev/lpt0:
  if=/usr/local/libexec/if-simple:\n  if=/var/log/rattan.log
```

然后再次尝试打印。检查日志文件（在我们的示例中为 `/var/log/rattan.log`）查看可能出现的任何错误信息。根据这些信息尝试修正问题。

如果你没有指定 `lf` 属性，LPD 将使用 `/dev/console` 作为默认值。

## 第 10 章 Linux 二进制兼容

由 Jim Mock 重构并更新了部分内容。最初由 Brian N. Handy 和 Rich Murphy 贡献。

### 10.1 概述
