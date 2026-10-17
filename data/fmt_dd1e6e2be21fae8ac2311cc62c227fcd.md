
Trying 192.168.2.52...

Connected to 192.168.2.52 (192.168.2.52).

Escape character is ']'

```
欢迎使用打印服务器
```

PS>monitor

(P1)STATE: Idle

TYPE: Parallel

PRINTER STATUS: On-Line

```
```

PS>exit

Connection closed by foreign host.
```

> 奇怪的是，NETGEAR 并没有将 PS101 推为支持 Linux 的硬件，尽管它可以运行。其他类型的网络打印打印服务器包括支持蓝牙的打印机和 802.11b 无线打印服务器，例如 TRENDnet 的 TEW-PS53、HP/Compaq 的基于并行口的 WP 110，以及带有 USB 的 JetDirect 380。此外，在购买之前，请研究打印机或打印服务器等产品与 Linux 的兼容性！

# 控制台打印控制

旧版本的 Red Hat Linux 使用 4.3BSD 行打印机池化系统及其套基于文本的打印工具。这些工具的较新版本具有相同的名称，包含在你的 Fedora DVD 中，但它们属于 `CUPS` 软件包。这些命令支持在后台启动打印作业（作为后台进程）、打印多个文档、指定本地和网络打印机的能力、控制打印机以及管理在打印机池队列中等待的文档。

# 基于控制台的打印机配置

`system-config-printer-ui` 工具提供了 Fedora 图形打印机配置客户端的所有便利和功能，而无需当前运行 X 会话。

# 第 23 章 文件与打印

正如你之前学到的，你以 root 身份运行此命令：

```
# system-config-printer-tui
```

按下回车键后，会出现命令的主对话框，如图 23.10 所示。你使用 Tab 键和空格键在对话框中导航并选择控件。

![](img/d4ad9a7c85702c925b4288f587284a4f_650_0.png)

**图 23.10** 使用 Fedora 的 `system-config-printer-tui` 打印机配置工具在基于控制台的 Linux 会话中创建或编辑打印机。

# 使用基本打印命令

配置打印机后，你可以使用任何具有打印能力的图形客户端从桌面进行打印。如果你不使用桌面，而是倾向于使用文本界面访问或访问 Fedora 系统，你可以从命令行输入若干打印命令。用于从命令行打印和控制打印的 CUPS 命令如下：

- `lp`——行打印机池化命令；用于使用特定打印机打印文档
- `lpq`——行打印机队列显示命令；用于查看等待打印的现有文档列表
- `lpstat`——显示服务器和打印机状态信息
- `lprm`——行打印机队列管理命令；用于从打印机队列中删除删除打印作业
- `lpc`——行打印机控制程序；供 root 操作员用于管理打印机池、lpd 守护进程和打印活动

这些命令提供了 CUPS 提供的功能的子集，但可以从命令行启动并控制打印机和打印队列。

你使用 `lp` 命令配合指定的打印机和文件名打印文件（文档或图像）。例如，要使用名为 `lp` 的打印机打印文件 `mydoc.txt`，请使用 `lp` 命令、`-d` 命令行选项和打印机名称，如下：

```
# lp -dl lp mydoc.txt
```

# 管理打印作业

你也可以从命令行打印多个文档。例如，要同时向 `lp` 打印机打印多个文件，可以如下使用 `lpr`：

```
# lpr -dl lp *.txt
```

这种方法利用 shell 的通配符功能，将当前目录下所有以 `.txt` 结尾的文件传递给 `lpr` 命令进行打印。使用 `lpq` 命令查看打印机队列，如下：

```
# lpq
```

`lpr` 已准备就绪

| Rank | Owner | File | Size |
| :--- | :--- | :--- | :--- |
| active | root | | 302 |

`lpq` 命令显示打印机队列。该命令报告打印机状态、所有者、文件和大小。CUPS 跟踪正在打印的作业。在示例中，对于 `192.168.2.52`，使用 `lrm` 命令停止打印作业：

```
# lrm
```

`lrm` 移除打印机队列中的打印作业。root 操作员使用 `lpc` 管理打印机池、lpd 守护进程和打印活动。通过访问 IP 地址（例如 `http://192.168.2.52`）来管理设备。支持其他服务如 FTP 和 Telnet，但未在文档说明：

```
$ telnet 192.168.2.52
Trying 192.168.2.52...
Connected to 192.168.2.52 (192.168.2.52).
Escape character is ']'
```
欢迎使用打印服务器
```
PS>monitor
(P1)STATE: Idle
TYPE: Parallel
PRINTER STATUS: On-Line
```
```
PS>exit
Connection closed by foreign host.
```
