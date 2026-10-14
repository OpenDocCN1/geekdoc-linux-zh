
以 root 身份输入命令 `echo -n "HelloIrDA" >/dev/lrlpt0` 来测试与 IrDA 打印机的连接。如果打印机能够直接打印 ASCII 文本，应该会打印出一个带有 Hello 字样的单页纸。

无论上述测试结果如何，打印机都应该出现在 `iradump` 的输出中。如果没有 `iradump` 命令，请安装 `irda` 包。如果 `iradump` 没有显示打印机，则无法对打印机进行寻址。如果没有显示，很可能是 IrDA 系统未启动，因为它在系统启动时不会自动启动。输入以下命令启动和停止 IrDA 系统服务：

```
earth:~ # rcircda start
earth:~ # rcircda stop
```

## 串口端口

要结合 LPRng 打印系统使用连接到串口的打印机，请阅读文档 `/usr/share/doc/packages/lprng/LPRng-HOWTO.html`，特别是 `file:/usr/share/doc/packages/lprng/LPRng-HOWTO.html#SESERIAL` 部分。更多信息可以通过 `printcap` 的帮助页（`man printcap`）以及在支持数据库中搜索关键字“serial”来获取。

## LPRng 和 lpdfilter 打印系统的手动配置

通常，打印系统使用 YaST2 进行配置，如第 150 页介绍的“使用 YaST 配置打印机”所示。SuSE Linux 还包含 `lrsetup` 程序，这是一个用于配置 LPRng 和 lpdfilter 打印系统的精简骨架级命令行工具。当使用 YaST 设置打印机时，它会收集所有必要数据，然后在内部运行带有所有必要选项的 `lprsetup` 以写入实际的 LPRng 和 lpdfilter 配置。`lprsetup` 被设计为一种专家工具。因此，它不会为寻找打印机选项的正确值提供任何帮助。要获取 `lprsetup` 可用命令行选项的简要列表，请输入 `lprsetup-help`；参考 `lprsetup` 的帮助页（`man lprsetup`）和 `lpdfilter` 的帮助页（`man lpdfilter`）获取更多详情。

有关 Ghostscript 驱动程序和特定选项的信息，请阅读第 147 页的“寻找正确的打印机驱动程序”和第 193 页的“使用 Ghostscript”。

### LPRng 打印池

LPRng 和 lpdfilter 打印系统使用的打印池是 LPRng（包 `lprng`）。打印池 `lpd`（或行打印机守护进程）通常在启动时自动启动。具体来说，脚本 `/etc/init.d/lpd` 作为启动过程的一部分被运行。之后，打印池作为守护进程在后台运行。使用 `rclpd start` 和 `rclpd stop` 手动启动和停止。

这些是 LPRng 的配置文件：

- `/etc/printcap`：系统打印池队列的定义
- `/etc/lpd.conf`：全局打印池配置
- `/etc/lpd.perms`：权限设置

根据脚本 `/etc/init.d/lpd`，命令 `rclpd start` 还会运行子进程 `checkpc -f`，该进程反过来根据 `/etc/printcap` 中定义的队列在 `/var/spool/lpd` 中创建具有相应权限的池化目录。启动时，打印池首先读取 `/etc/printcap` 中的条目，查看定义了哪些打印队列。打印池的任务是管理任何排队打印的作业。具体来说，打印池：

- 通过将每个作业的打印数据传递给打印过滤器（如果需要），然后发送到打印机或另一个队列来管理本地队列
- 按照作业入队列的顺序处理作业
- 监控队列和打印机的状态，并在请求时提供状态信息
- 监听 515 端口以接受或拒绝来自远程主机发往本地队列的打印作业，具体取决于配置
- 将打印作业转发到远程打印池（在其他主机上监听 515 端口），通过远程队列进行打印。

要要了解更多关于此机制的细节，请阅读 LPRng Howto（`file:/usr/share/doc/packages/lprng/LPRng-HOWTO.html`）或参考 `printcap` 的帮助页（`man printcap`）以及 `lpd` 的帮助页（`man lpd`）。

### 从应用程序通过 LPRng 打印

应用程序使用现有队列从命令行进行打印。在应用程序中，打印机选项不是直接配置的，而是通过现有队列配置。

应用程序可以使用 `lpr` 命令进行打印。为了使此生效，请使用应用程序的打印机配置来选择现有队列之一（例如 `lpr` 或 `color`），或使用应用程序的打印对话直接输入相应的命令（例如 `lpr -PPl` 或 `lpr -Pcolor`）。

### LPRng 命令行工具

本节仅提供可用工具的简要概述。欲需详情，请参考 LPRng Howto，特别是 `file:/usr/share/doc/packages/lprng/LPRng-HOWTO.html` 部分。

### 管理队列

### 打印文件

有关如何使用 `lpr` 的详情见 LPRng Howto（`file:/usr/share/doc/packages/lprng/LPRng-HOWTO.html`）。以下命令

```
newbie@earth:~ > lpr -P(queename) (jobnumber)
```

从指定的队列中删除该作业。

### 控制队列

`lpc` 命令显示指定队列的状态并允许对其更改。重要的选项有：

- help 显示可用选项的简要概述。
- status `(queename)` 显示状态信息。
- disable `(queename)` 不再接受指定队列的新作业。
- enable `(queename)` 接受指定队列的新作业。
- stop `(queename)` 停止指定队列的打印。如果作业正在打印，它将完成。
- start `(queename)` 启用指定队列的打印。
- down `(queename)` 具有 `disable` 和 `stop` 的效果。
- up `(queename)` 具有 `enable` 和 `start` 的效果。
- abort `(queename)` 具有 `down` 的效果，立即终止所有打印作业。然而，中止的作业会被保留，并在使用 `up` 重启队列后恢复。

使用控制打印队列需要 root 权限。可以直接在命令行为 `lpc` 提供选项（如 `lpc status all`）。你也可以不带任何选项运行该程序，这将以对话模式启动它——它会打开 `lpc>` 提示符。然后在提示符处输入选项。要退出提示符，输入 `quit` 或 `exit`。

如果你输入 `lpc status all`，输出可能如下：

| 打印机 | 池化状态 | 作业 子服务器 |
| --- | --- | --- |
| lp@earth | enabled | enabled | 2 123 456 |
| color@earth | disabled | disabled | 0 none none |
| laser@earth | disabled | enabled | 8 none none |

这提供了以下信息：`lp` 完全启用并有两个作业，其中一个正在打印。相反，`color` 队列完全停止。最后，`laser` 队列目前不打印，但仍接受该队列的任务（目前有 8 个），并在打印池中累积。

更多信息可以通过 `lpc` 的帮助页（`man lpc`）和 LPRng Howto 获取。

### 管理远程队列

对于下面解释的每个命令，请将 `(printserver)` 替换为打印服务器的名称或 IP 地址。`(queueename)` 必须是打印服务器上的一个队列。

### 生成打印作业

使用 LPRng 守护进程，甚至可以直接访问远程队列，使用 `lpr` 命令，语法为 `lpr -P(queueename)@(printserver) (file)`。只有当打印服务器配置为在其队列上接受远程打印作业时，此操作可行。LPRng 默认启用此功能。

### 检查状态

通过输入以下命令检查远程主机上队列的状态：

- `newbie@earth:~ ~ lpq -P(queueename)@(printserver)`
- `newbie@earth:~ ~ lpq -s -(queueename)@(printserver)`
- `newbie@earth:~ ~ lpq -1 -(queueename)@(printserver)`
- `newbie@earth:~ ~ lpq -L -(queueename)@(printserver)`

或

- `newbie@earth:~ ~ lpc status (queueename)@(printserver)`
- `newbie@earth:~ ~ lpc status all@(printserver)`

要列出打印服务器上所有队列的名称并显示状态信息，只要打印服务器上使用了 LPRng，即可使用 `lpq -s -Pall(printserver)` 或 `lpc status all@(printserver)`。
