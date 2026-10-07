
打印机。输出中的其他信息包括 `/etc/printcap` 定义、关于每个打印机溢出目录的诊断信息（位于 `/var/spool/lpd/printername` 下）以及所有打印过滤器的权限。

你使用 `lpr` 命令来打印文件（文档或图像），并指定指定的打印机和文件名。例如，要使用名为 `1pr` 的打印机打印文件 `mydoc.txt`，请使用 `lpr` 命令及其 `-P` 命令行选项以及打印机名称，如下：

```
# 1pr -Plp mydoc.txt
```

`lpr` 命令使用默认打印机名称，该名称取决于（优先级顺序）：命令行、`PRINTER`、`LPDEST`、`NPRINTER` 或 `NGPRINTER` 环境变量、系统 `/etc/printcap` 中的第一个条目，或者 `/etc/lpd.conf` 中指定的默认打印机。

## 管理打印作业

你也可以从命令行打印多个文档。例如，像如下所示将多个文件一次打印到 `lpr` 打印机：

```
# 1pr -Plp *.txt
```

这种方法利用 shell 的通配符功能将当前目录下所有以 `.txt` 结尾的文件传递给 `lpr` 命令打印。使用 `lpq` 命令查看打印机队列，如下：

```
# 1lpq
Printer: 1lp@thinkpad
Queue: 1 printable job
Server: pid 9531 active
Unsporer: pid 9532 active
Status: IF filter 'wrapper' filter msg - \
<</HW/Resolution[300 300]>>setageddevice at 12:29:03.569
```

| Rank | Owner/ID | Class | Job | Files | Size | Time |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | root@thinkpad+530 | A | 530 | CHANGES | 251703 | 10:29:02 |

`lprq` 报告打印机情况、作业数量、`lpd` PID、来自过滤器的信息（如每英寸点数，即 `dpi`）以及格式化的打印作业列表——每个作业都有一个作业编号（此示例中为 `530`）、所有者、文件名、大小以及作业开始时间。LPRng 使用作业编号来跟踪等待打印的文档，每个作业将有一个唯一的作业编号。要停止示例中的打印作业，请使用 `lpr-rm` 命令，后跟作业编号，如下：

## 第 12 章 打印服务

```
# lpm 530
Printer lp@thinkpad:
checking perms 'root@thinkpad+530'
dequueued 'root@thinkpad+530'
```

`lpm` 命令从打印机队列中移除溢出文件并杀死作业。打印作业所有者（如普通用户）只能删除他们拥有的溢出作业。作为 root 操作员，你可以杀死任何作业。

只有 root 操作员才能使用 `lpc` 命令。该命令用于打印机和队列控制。你可以用它来重新排列打印作业的顺序，并可以显示任何系统打印机的状态。在命令行中启动 `lpc` 如下：

```
# lpc
```

`lpc` 命令对命令关键字和语法有内置帮助。要显示帮助文本，请使用 `help` 关键字或按 `:` ：：

```
lpc> help
```

几页帮助文本将回显到你的显示器上。另一个有用的命令是 `lpstat`，用法如下：

```
# lpstat
Printer: lp1@shuttle2
Queue: no printable jobs in queue
Status: job 'root@cello+301' removed at 17:47:07:633
```

此命令列出等待中的打印作业，以及与 `lprpm` 返回类似的信息。

## 使用通用 Unix 打印系统 (CUPS)

Red Linux 还包含通用 Unix 打印系统的版本，称为 CUPS。此打印系统支持互联网打印协议（即 IPP），并提供许多独特功能，例如网络打印机目录（打印机浏览）服务、对加密的支持以及对 PostScript 打印机描述（ppd）文件的支持。

根据互联网工程任务组 (IETF) 的说法，IPP 源于 Novell 在 1996 年提出的用于互联网的打印协议提案。随后，该系统经过开发并成熟，成为适用于各种 Linux 和 UNIX 操作平台的稳定打印系统。

## 在 LPRng 和 CUPS 打印系统之间切换

Red Linux 提供了一个名为 `redhat-switch-printer` 的图形打印系统管理工具，你可以用它在 LPRng 和 CUPS 系统之间切换。如果你使用 Red Hat 桌面，请选择“额外 -> 系统设置 -> 打印机 系统切换器”菜单项，或从 X 终端窗口的命令行启动该客户端，如下：

```
# redhat-switch-printer &
```

按下回车键后，你将看到如图12.13所示所示的客户端对话框。

![](img/446debe023486a07fde575245cf7a3ff_416_0.png)

图 12.13 Red Hat 的 redhat-switch-printer 用于在 LPRng 和 CUPS 之间切换你的打印系统。

点击所需的系统，然后点击 OK 按钮。你将需要停止 `lpd` 守护并启动或停止 CUPS。例如，如果你使用 LPRng 但想切换到 CUPS，如下所示停止 `lpd`：

```
# /etc/rc.d/init.d/lpd stop
```

你必须通过编辑 `/etc/xinetd.d/cups-lpd` 并重启 `xinetd` 来确保启用 cups-lpd 服务。例如，读取 `/etc/xinetd.d/cups-lpd`：

```
disable = no
```

保存文件；然后重启 `xinetd`：

```
# /etc/rc.d/init.d/xinetd restart
```

然后如下启动 CUPS：

```
# /etc/rc.d/init.d/cups start
```

启动 CUPS 后，通过启动浏览器（如 mozilla）并访问 http://localhost:631 来创建打印机配置。CUPS 提供了一个基于 Web 的管理界面，如图12.14 所示。

382 第 12 章 打印服务

![](img/446debe023486a07fde575245cf7a3ff_417_0.png)

图 12.14 Red Hat 的 redhat-switch-printer 客户端用于在 LPRng 和 CUPS 之间切换你的打印系统。

## 创建 CUPS 打印机项

![](img/446debe023486a07fde575245cf7a3ff_417_0.png)
