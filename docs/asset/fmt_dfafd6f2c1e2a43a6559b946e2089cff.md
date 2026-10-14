
## `:rm=some_host:` 和 `:rp=some_printer:`

这些表示远程打印机名称和主机。这些选项告诉 `lpd` 打印机未本地连接，并且应将作业发送到 `some_host` 在 `some_printer` 上打印。（LPRng 提供了一个更简洁的替代方案——见下文 LPRng Enhancements。）

相关手册页：`printcap`(5)、`lpd`(8)、`lpq`(1)、`lpr`(1)

## 网络打印机访问

要允许网络上的其他机器（Linux、Unix 或其他）访问你计算机上的打印机，你需要启用访问控制。Berkeley `lpd` 有一个非常简单的系统，允许 `/etc/hosts.lpd` 或 `/etc/hosts.equiv` 中列出的任何主机进行打印。（请记住 `/etc/hosts.equiv` 是一个更通用的文件，用于可以无需密码使用 `rlogin` 的主机。）

## LPRng 增强功能

Berkeley `lpd` 是古老的软件，它之所以能存活下来，仅仅是因为没有人有太多改进它的动力。然而时代在变，打印机也在变，尤其是网络，这就是 Patrick Powell 开发了 LPRng 的原因。它的许可证与 `perl` 类似——GNU 风格的通用公共许可证和艺术许可证。除 CD-ROM 上包含的版本外，你也可以在 http://www.astart.com/ 上获取它（AStart 还提供商业支持）。在本节中，我们将看到 LPRng 相对于 `lpd` 的一些更值得注意的改进。

### `/etc/printcap` 中的 `:lp=some_printer@some_host:`

这是一种轻松引用远程打印机的方式。

### 对打印机选项的更好用户控制

当你使用 Berkeley `lpd` 设置不同的打印机选项时，每个选项都需要 `/etc/printcap` 中的额外条目。例如，双面打印机有两个 `/etc/printcap` 条目（和两个不同的 spool 目录），其中一个的名称以 `-simplex` 结尾（用于单面输出）。使用 LPRng 时，不同打印选项的多重条目是不必要的；相反，用户可以使用 `-Z` 指定选项（如 `-Zsimplex`）。

### System V `lpsched` 仿真

某些程序是用 System V 的 `lp` 命令编写的打印程序，你可能很难将它们改编为 BSD 风格的程序。LPRng 提供了 `lp`、`lpstat` 和 `cancel` 程序，它们的行为与 System V 程序非常相似，但使用 LPRng 进行排队。

### 灵活配置

LPRng 中的 `/etc/lpd.conf` 允许许多配置选项，包括打印机数据库的位置（而不是将其放在 `/etc/printcap` 中）。

### 更好的身份验证和安全性

LPRng 允许使用 Kerberos，并且可以根据用户组和 netgroup 映射支持基于选择的打印权限。

## 使用 `lpc` 控制 `lpd`

一旦你的打印 spooling 系统运行起来，你就需要定期杀掉作业、禁用打印和 spooling 等。`lpc` 程序通常以 root 身份运行，完成这项工作，尽管它只操作队列和 spool。对于诊断，请查看 `lps`。

你可以交互式运行 `lpc` 或以命令行模式运行。要进入交互模式，请在不带任何参数的情况下运行 `lpc`，然后在提示符下输入 `status all` 等命令。你也可以通过将命令作为参数添加到 shell 来运行某些命令。因此，如果你在 shell 提示符下输入 `lpc status all`，你将得到与先输入 `lpc` 然后输入 `status all` 相同的结果，但 `lpc` 会立即终止，你将返回到 shell。

### `lpc` 命令

一些更有用的 `lpc` 命令包括：

- `clean all|printer` 删除本地打印机队列中的所有文件。当打印机停机一段时间且作业在队列中堆积时，这非常有用。当你使用 LPRng 时，`clean` 命令对 `lpc` 不可用；请改用 `lprm` 的 `clean` 参数。

- `disable all|printer` 禁用打印机的队列，使其无法接收文件。

- `abort all|printer` 禁用打印，但允许用户排队作业。如果你要对打印机进行快速修复，这很有用。

> 相关手册页：`lpc`(1)

![](img/8131acdd754b0d26c380a2035b509e34_127_0.png)

## 5.3 PostScript 打印机

如果你的打印机支持 PostScript，要打印 PostScript 作业，你只需将其发送到打印机即可。然而，可能会出现一些复杂情况。

### 问题 54

症状：作业消失。连接被拒绝。

问题：网络 PostScript 打印机的 spooler 处理排队不太好。

解决方法：虽然大多数网络打印机直接支持 Berkeley `lpd` 协议，允许你将每台打印机视为远程机器上的打印机，但通常应避免这种方法，因为可能会导致排队不佳、记账困难和缺乏选项。

许多网络打印机支持在专用端口上的直接连接（对于 HP 打印机，是端口 9100）。对于这种情况，你可以使用 `ifhp`（LPRng 的打印过滤器，我们稍后会描述）。如果你的打印机不支持直接连接，你需要做出选择。在较小的网络上，你可能可以使用打印机的内置 `lpd` 服务器。否则，你可能需要找到其他方式与之通信——听起来可能令人害怕，但使用 Netatalk 的 AppleTalk 连接可能是解决方案。

### HP、类似 HP 的打印机和其他 PostScript 打印机

HP 的激光打印机非常受欢迎，市场上许多其他打印机（如 Lexmark 的）也与之类似。无论你是通过并行端口、网络还是其他方式连接，使用 LPRng 的 `ifhp` 过滤器都是一个不错的选择。`ifhp` 的一个优秀功能是为打印机生成适当的 PCL 命令以用于选项，例如备用纸盘和双面打印。

> 注意
>
> 这里所有的 `printcap` 示例都仅与 LPRng 相关。通过一点努力，你可以让它们与常规 `lpd` 一起工作；请参阅下面的简单包装器以帮助你实现。

`ifhp` 提供了许多不同的指定选项的方式——通过文件、命令行和 `printcap`——但你不需要全部使用。记住，最佳配置是可预测的，而这通常是最简单的配置。

使用你喜欢的任何前缀安装 `ifhp` 包（它在 CD-ROM 的 `support/printing` 中；有关从源代码安装的信息，请参阅第 6 章）。我们将使用 `/usr/local` 作为示例，因此过滤器将最终位于 `/usr/local/lib/filters`。

### LPRng `ifhp` `printcap`

让我们直接看一个用于 `ifhp` 的 LPRng `printcap` 示例——这个示例用于 HP 网络打印机：

```
myprinter|MyPrinter|Printer on my desk:\
:lP=myprinter.mydomain.com#9100:sD=/var/spool/lpd/myprinter:\
:lf=/var/spool/lpd/myprinter/log:\
:mx#0:sF:sh:\
:if=/usr/local/lib/filters/ifhp:\
:of=/usr/local/lib/filters/ofhp:
```

这里，`myprinter.mydomain.com` 是打印机的网络主机名，9100 是要连接的 TCP 端口。我们已完全抑制了页眉页（使用 `:sh:`）。

### PROBLEM 55

症状：`lpd` 抱怨 `myprinter.example.com#9100` 不是一个设备。

问题：你在使用 `ifhp` 与 Berkeley `lpd`，而该设备不受支持。

修复：推荐的修复方法是放弃旧的 `lpd` 并安装 LPRng。否则，你可以伪造一个设备并为 `ifhp` 编写一个 shell 脚本包装器。为此，首先将设备更改为 `null` 设备，使用 `:lp=/var/spool/lpd/name/null:` [请参阅本章后面关于 AppleTalk 打印机的部分，了解如何创建 `null` 设备的说明]。然后编写一个类似这样的 `/var/spool/lpd/name/ifhp.wrapper` 脚本：

```
#!/bin/sh
/usr/local/lib/filters/ifhp -Tdev=myprinter.example.com#9100 $@
```

现在更改 `printcap` 以反映新的过滤器，使用 `:if=/var/spool/lpd/name/ifhp.wrapper:`：

如果打印机没有主机名，你可以使用 IP 地址；如果尚未设置，你需要设置。你有几种设置方法——可以通过打印机控制面板手动设置，或使用 RARP/ARP、`bootp`、DHCP、`tftp` 或其他方法。你最好查看打印机手册，因为打印机可能有非常不同的要求。
