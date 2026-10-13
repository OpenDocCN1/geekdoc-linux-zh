
```bash
$ telnet 192.168.2.52
Trying 192.168.2.52...
Connected to 192.168.2.52 (192.168.2.52).
Escape character is '^}'.

Welcome to Print Server

PS>monitor
(P1)STATE: Idle
TYPE: Parallel
PRINTER STATUS: On-Line

PS>exit
Connection closed by foreign host.
```

> **提示**
>
> 奇怪的是，NETGEAR 并没有宣传 PS101 为 Linux 支持的硬件，尽管它可以正常工作。其他类型的网络附加打印设备包括支持蓝牙的打印机和 802.11b 无线以太网打印服务器，例如 Trendware 的 TEW-PS3、HP/Compaq 的基于并口的 WP 110，以及带有 USB 的 JetDirect 380x。一如既往，在购买之前，请研究产品（如打印机或打印服务器）与 Linux 的兼容程度！

# 控制台打印控制

旧版本的 Red Hat Linux 使用 4.3BSD 行式打印机假脱机系统及其基于文本的打印工具集。这些工具的同名新版本包含在您的 Fedora CD-ROM 中，但它们是 CUPS 包的一部分。这些命令支持在后台启动打印作业（作为后台进程），打印多个文档，指定本地和网络打印机的能力，控制打印机，以及管理等待在打印机假脱机队列中的排队文档。

## 基于控制台的打印机配置

`system-config-printer-tui` 工具提供了 Red Hat 图形化打印机配置客户端的所有便利和功能，而无需当前运行的 X 会话。正如您之前所学到的，您以 root 身份运行此命令：

```bash
# system-config-printer-tui
```

按下 Enter 键后，命令的主对话框将出现，如 图 21.10 所示。您使用 Tab 键和空格键在该对话框中的控件之间导航并选择。

![](img/774d40fd20903495c5cd00e2efad3f33_639_0.png)

### 图 21.10 在基于控制台 Linux 会话期间，使用 Red Hat 的 `system-config-printer-tui` 打印机配置实用工具来创建或编辑打印机。

# 使用基本打印命令

配置好打印机后，您可以使用任何支持打印的图形客户端从桌面进行打印。如果您不使用桌面，但更喜欢使用或通过基于文本的界面访问您的 Fedora 系统，您也可以从命令行输入许多打印命令。从命令行打印和控制打印的主要 CUPS 命令如下：

- `lp`——行式打印机假脱机命令；用于使用特定打印机打印文档
- `lpq`——行式打印机队列显示命令；用于查看等待打印的现有文档列表
- `lpstat`——显示服务器和打印机状态信息
- `lprm`——行式打印机队列管理命令；用于从打印机队列中删除打印作业
- `lpc`——行式打印机控制程序；由 root 操作员用于管理打印假脱机、`lp` 守护程序和打印机活动

这些命令提供了 CUPS 所提供功能的一个子集，但可用于从命令行启动和控制打印机及打印队列。

您使用 `lp` 命令打印文件（文档或图像），并指定打印机和文件名。例如，要使用名为 `lp` 的打印机打印文件 `mydoc.txt`，请使用 `lp` 命令、其 `-d` 命令行选项和打印机名称，如下所示：

```bash
# lp -dlp mydoc.txt
```

## 管理打印作业

您还可以从命令行打印多个文档。例如，要同时将若干文件打印到 `lp` 打印机，请像这样使用 `lpr`：

```bash
# lpr -dlp *.txt
```

这种方法使用 shell 的通配符功能，将当前目录中所有名称以 `.txt` 结尾的文件提供给 `lpr` 命令进行打印。使用 `lpq` 命令查看打印机的队列，如下所示：

```bash
# lpq
lp is ready and printing
Rank    Owner   Job    File(s)       Total Size
active  root    7      classes.conf  3072 bytes
```

`lpq` 命令报告作业、所有者、作业号、正在打印的文件以及作业的大小。作业号（此例中的 `7`）由 CUPS 用于跟踪正在打印或等待打印的文档。每个作业都有唯一的作业号。要停止此例中的打印作业，请使用 `lprm` 命令，后跟作业号，如下所示：

```bash
# lprm 7
```

`lprm` 命令将假脱机文件从打印机队列中删除并终止作业。打印作业的所有者，如普通用户，只能删除他们拥有的假脱机作业。作为 root 操作员，您可以终止任何作业。

只有 root 操作员可以使用 `lpc` 命令来管理打印机和队列，因为该命令主要用于打印机和队列控制。您作为普通用户，不能使用它来重新排列打印作业的顺序，但您可以获取任何系统打印机状态的显示。在命令行上像这样启动 `lpc`：

```bash
# /usr/sbin/lpc
```

`lpc` 命令具有内置帮助，但它仅包含五个命令：`exit`、`help`、`quit`、`status` 和 `?`。`status` 命令显示指定打印机或所有打印机的状态：

```bash
# lpc
lpc> ?
Commands may be abbreviated.  Commands are:
exit  help  quit  status ?
lpc> status
lp:
    printer is on device 'paralel' speed -1
    queueing is enabled
    printing is enabled
    no entries
    daemon present
netlp:
    printer is on device 'paralel' speed -1
    queueing is enabled
    printing is enabled
    no entries
    daemon present
lpc> quit
```

上述示例会话显示了两台打印机（`lp` 和 `netlp`）的状态报告。另一个有用的命令是 `lpstat`，您使用其 `-t` 选项像这样使用它：

```bash
# lpstat -t
scheduler is running
system default destination: lp
device for lp: paralel:/dev/lp0
device for netlp: paralel:/dev/lp0
lp accepting requests since Jan 01 00:00
netlp accepting requests since Jan 01 00:00
printer lp is idle.  enabled since Jan 01 00:00
printer netlp is idle.  enabled since Jan 01 00:00
```

此命令列出本地系统上打印机队列的所有状态信息。

# 使用通用 Unix 打印系统 GUI

您可以使用 CUPS 创建打印机队列、获取打印服务器信息并通过启动浏览器（如 Mozilla）并浏览到 `http://localhost:631` 来管理队列。CUPS 提供了基于 Web 的管理界面，如 图 21.11 所示。

如果在浏览器页面中点击“执行管理任务”项，系统会提示您输入 root 密码，如 图 21.12 所示。

![](img/774d40fd20903495c5cd00e2efad3f33_642_0.png)

图 21.11 使用基于 Web 的 CUPS 管理界面来配置和管理打印。

![](img/774d40fd20903495c5cd00e2efad3f33_642_1.png)

图 21.12 输入 root 密码以通过 CUPS 执行打印机管理。

## 创建 CUPS 打印机条目

本节提供了使用 CUPS 的基于 Web 的界面创建 Linux 打印机条目的简短示例。使用 CUPS 界面创建打印机和队列类型（例如本地、远程、串行端口或 Internet）；然后输入设备统一资源标识符（URL），例如 `lpd://192.168.2.35/1p`，这代表远程 Unix 打印服务器的 IP 地址以及服务器上远程打印队列的名称。你还需要指定打印机的型号或制造商及其驱动程序。“打印机”页面链接允许你打印测试页、停止打印服务、管理本地打印队列、修改打印机条目或添加另一台打印机。

在“管理”页面中，点击“添加打印机”按钮，然后在“名称：”字段中输入打印机名称（例如 `1p`），在“位置：”字段中输入打印机的物理位置，并在“描述：”字段中输入关于打印机的简短备注（例如其类型）。图 21.13 展示了一个 HP648C 的示例条目。
