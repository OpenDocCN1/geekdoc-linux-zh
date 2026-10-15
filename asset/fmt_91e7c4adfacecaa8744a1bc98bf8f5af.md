
如果你使用的是 Red Hat 桌面，请从“系统设置”菜单中选择“打印”项。系统会要求输入 `root` 密码。如果不是，说明你以 `root` 身份运行 X，这是一个坏主意。请注销，然后以普通用户重新登录！输入 `root` 密码后，会出现打印机配置对话框。

然后你按照提示定义打印机并添加本地或远程打印服务。在保存更改之前，你应该打印测试页。可以使用打印机配置客户端，可以使用 GNOME 或 KDE 客户端“文件”菜单中的“打印”项。

> `redconfig-printer` 工具是对以前发行版中包含的旧版 `printtool` 的更新。尽管你可能会发现系统中安装了相关工具（或符号链接），如 `printtool`、`printconf-tui` 和 `/usr/sbin/printconf-gui`，但 Red Hat 建议使用 `redhat-config-printer` 客户端来管理打印机。

# 基于控制台的打印机配置向导

本地或远程打印服务可以在本地或没有窗口系统的服务器上进行配置。要要操作，请使用 Red Hat 的基于文本的 `redhat-config-printer-tui` 打印机配置工具。你需要以 `root` 身份运行此命令：

```
# redhat-config-printer-tui
```

按下回车键后屏幕将清除，你会看到控制台的主对话框（你将在本章稍后的“基于控制台的打印命令”章节看到此屏幕）。

> 如果你在控制台未使用 X 的情况下以 `root` 身份启动 `redhat-config-printer`，将使用 `redhat-config-printer-tui` 界面。

使用 Tab 键和空格键导航对话框并展开设备列表。你可以通过突出 `New` 按钮并按回车创建新的打印机项。使用向上或向下光标键选择并突出现有条目；然后突出 `Edit` 按钮并按回车以编辑之前定义的打印机。

你可以使用 `lpr` 命令从命令行打印文档，并使用 `rpm` 命令控制打印队列。

# 管理打印服务

打印服务和作业请求由 `lpd` 守护进程处理，该进程由 `/etc/rc.d/init.lpd` 启动脚本启动，其部分如下：

```
start () {

  echo -n \'$Starting Sprog: *'

  # 是一个 printconf 系统吗？

  if [[ [ -x /usr/sbin/printconf-backend ]]; then

    # 运行 printconf-backend 以重建 printcap 和 spools

    if ! /usr/sbin/printconf-backend; then

      # 如果后端失败，我们不启动任何定义的打印机

      echo -n \$No Printers Defined"

    fi

    echo_success

  echo

  return 0

```

注意，这里显示了所有脚本。然而，如你所见，脚本首先报告服务正在启动。接下来，一个向 Red Hat printconf 工具发布的命令是检查你系统 `/etc/printcap` 数据库是否存在。脚本随后启动 `lpd` 守护进程，该进程作为进程在后台运行，等待 `/var/spool/lpd` 目录下出现任何文件。在定义打印机后，你可以使用一个或多个工具来控制打印服务、管理打印作业、启用、禁用或授权远程打印服务（参见本章后面的“打印工具”）。

表 12.1 打印相关命令：
| 名称 | 说明 |
| :--- | :--- |
| a2ps | 为 PostScript 格式化文本 |
| dvi[l1,l4] | 将 TeX 文件转换为 PCL |
| encscript | 将文本转换为 PostScript |
| escputil | 喷墨打印机 |
| grolbp | LBP-4 和 LBP-8 的驱动 |
| gs | Ghostscript 解释器 |
| gsdj[dj500,lp] | 喷墨打印机 |
| gsdj[dj500,lj] | 台阶打印机 |
| lpc | 打印控制工具 |
| lpd | 守护进程 |
| lpf | 通用打印过滤器 |
| --- | --- |
| lprm | 打印队列管理 |
| mpage | PostScript 文本格式化 |
| pap | Appletalk 打印机 |
| pbm[2ppa,to10x,toptx,toppa] | 便变位图工具
| toppa | |

文本格式化命令
非双面打印机的双面打印工具
启动打印配置工具
SMB 守护器
SMB 脚本
SMB 守护器
位图转换工具

你可以通过带有 `--help` 命令的 `gs` 解释器来使用其内置打印机设备：

```
# gs --help
```

> 注意
Red Hat 包含了你可以查看多种类型的图形客户端。例如，要显示 PostScript 文档（包括压缩 PostScript 文档）或 PostScript 图像，请使用 `gs` 客户端。要显示 PDF 格式 文档，你可以使用 `gs` 或 `xpdf` 客户端。

`gs` 命令会输出命令行用法帮助，并列出内置打印机和图形设备。获取此信息的另一种方法是启动 `gs` 然后使用 `devicenames` 命令：

```
# gs

GNU Ghostscript 7.05 (2002-04-22)

Copyright (C) 2002 artofcode LLC, Benicia, CA. All rights reserved.

此软件不提供保证；详情请参见 PUBLIC FILE。

Loading NimbusRom09L-Regu font from /usr/share/fonts/default/Type1/

->n0120031.pfb...

2418068 1053956 1642520 347466 0 done.

Loading NimbusSanL-Regu font from /usr/share/fonts/default/Type1/n0190031.pfb...

2785628 1379834 1662616 358654 0 done.

Using NimbusSanL-Regu for NimbusSanL-Regu.

devicenames
```

```
/coslw2p /cdjcolor/bj10v /cdj1600 /djet500 /xl11rg16x /atx23 /xl11gray4 /st800

->jpeg6 /neccp6 \

/psgray /alc2000 /lp8000 /pskm /lmx320 /jpet3852 /pbmraw /DJ630 /epsonc /bjc800

/lbp320 \

/cosxl1 /cdjmonono /bj10vh /cdj500 /laserset /xl11rg3d2 /atx24 /xl11mono /stcolor

/pdfwrite /oce9050 \

/psgrb /cubps /lq850 /pskmraw /lmx1500 /la5500 /pgm /DJ66xx /exp /fag63 /lips2p /cp50

/cdj550 \

/mag16 /cdj670 /ljet410 /ljet4pj1 /atx38 /bmpmono /sunhomno /pswrite /oki812

/cljet5 /lmn5700 \

/tiffcrle /lex7000 /lat4 /pgmraw /DJ66xx /fs604 /faxged32 /bjc880 /declclpj

/mag256 /cdj850 /ljet2p

/lj4dith /bmpa16 /bmgtray /t4693d2 /epwrite /okiibm /bitgrb /cljet5c /m8510

/tiff3 /lex5700 /la75
```

示例中未列出设备。

# Aladdin 还是 GNU？

Linux 下有两个版本的 Ghostscript 可用。其中一个版本名为“AFPL Ghostscript”，它曾名为“Aladdin Ghostscript”。该版本根据 Aladdin 免费许可授权，不允许商业分发。另一个版本被称为“GNU Ghostscript”，根据 GNU 公共许可证分发，并随你的 Red Hat Linux 副本一起安装。有关不同版本的详细信息或有关许可的疑问，请参阅 Ghostscript 主页：
http://www.cs.wis.edu/~ghost/

# 创建和配置本地打印机

为你的 Red Hat Linux 系统创建本地打印机可以通过六个简单的步骤完成。你必须拥有 `root` 权限才能使用 `redhat-config-printer` 客户端。在开始之前，`lpd` 守护进程也应该运行（在本章早些部分手动运行守护进程，或使用 `ntsys` 命令确保 `lprd` 在启动时启动）。

要启动 `redhat-config-printer`，请从 GNOME 或 KDE 桌面面板的“系统设置”菜单中选择“打印”项，或使用如下 X 终端窗口的命令行：

```bash
# redhat-config-printer &
```

# 创建打印队列

Red Hat Linux 的 `redhat-config-printer` 工具将引导你完成创建新打印队列的过程，这实际上是在你的系统上定义了一台新打印机。开始，点击 `redhat-config-printer` 主窗口中的“新建”工具栏按钮。会出现“添加新打印队列”配置对话框，如图 12.1 所示。

**图 12.1** 点击“新建”工具栏按钮开始为你的系统配置新打印机，然后点击“下一步”开始。

点击“向前”按钮；出现“队列名称”对话框。为新打印机输入所需的名称（例如 `lp`），输入简短描述，然后点击“向前”按钮。出现“队列类型”对话框，如图 12.2 所示。使用队列类型下拉菜单选择你正在添加的打印机类型。你可以配置通用 UNIX 打印系统 (`CUPS`) 支持的本地或网络打印机、`lpd` 守护进程、会话消息块 (`SMB`) 服务器、网络核心协议 (`Novell`) 或 JetDirect 接口。要配置连接到计算机的打印机，选择本地连接队列类型，然后点击“向前”。

图 12.3 所示的打印机型号对话框提供了一个下拉菜单，你可以从中选择打印机制造商，或者简单地选择通用类型。

注意，如果打印机未连接到你的计算机，你也可以为 Red Hat 配置打印机。选择打印机制造商后，将出现该制造商的打印机列表（如图 12.4 所示的 HP）。从列表中选择你的打印机，然后点击“向前”按钮。

**图 12.2** 点击下拉菜单选择本地连接的打印队列类型。

**图 12.3** 点击下拉菜单选择你的打印机制造商或打印机类型。

# 第 12 章 打印服务

**图 12.4** 从列表中选择你的打印机并点击“向前”按钮完成本地连接打印机的配置。

如果在选项列表中没有看到你的打印机，请不要担心；选择一个相关的但不同的打印机型号，仍然可以打印到你的打印机上。例如，许多 HP 打印机可以使用 Deskjet 500 进行黑白打印，或使用 500C 进行彩色打印。

> 注意
> 你也可以访问 http://www.linuxprinting.org/ 来查找与你的打印机配合使用的驱动程序，或查看每个驱动程序支持的打印机交叉列表。你可能还会找到市场上最新打印机的经过改进的驱动程序。

你可以尝试查看哪种打印机选择对你的打印机最有效（如果未列出）。做出选择后点击“向前”。

“完成并创建打印队列”对话框显示打印机类型、打印设备和所选打印机，以便你确认信息无误（见图 12.5）。如果需要更改选项，点击“后退”返回之前的对话框。要创建新打印队列，点击“应用”。

打印队列创建后，你可以在 `redhat-config-printer` 主窗口中看到定义的新打印机，如图 12.6 所示。

**图 12.5** 在提交 `/etc/printcap` 创建新打印机项之前检查设置；如果设置正确，点击“应用”创建新打印机。

**图 12.6** 在提交 `/etc/printcap` 创建新打印机项之前检查设置；如果设置正确，点击“应用”创建新打印机。

> 注意
> 你也可以访问 http://www.linuxprinting.org/ 来查找与你的打印机配合使用的驱动程序，或查看每个驱动程序支持的打印机交叉列表。你可能还会找到市场上最新打印机的经过改进的驱动程序。

# 创建网络打印机

设置打印服务涉及配置打印服务器，然后在网络上的一个或多个计算机上创建远程打印机项。本节介绍了从一个 Linux 工作站到另一个打印的快速方法。你还将学习使用 Samba 及其工具进行会话块打印。最后，本节将讨论如何配置网络连接打印机并使用它们打印单份或多个文档。

# 在局域网中启用打印

设置从 Linux 工作站到局域网的打印需要 `root` 权限以及对两台计算机的访问权限，但过程简单易于执行。

首先，登录或 `ssh` 到连接打印机的计算机。使用 `hostname` 或 `ifconfig` 命令获取主机名或 IP 地址

接下来，编辑名为 `/etc/lpd.perms` 的文件。滚动到文件末尾并查找远程权限项：

```
# 允许本地作业提交
REJECT SERVICE=X NOT SERVER
```

## 第12 章 打印服务

远程打印默认未启用，因此你必须使用井号（`#`）注释掉服务拒绝行：

```
# allow local job submissions only
# REJECT SERVICE=X NOT restart
```

保存文件并重启 `lpd` 守护进程：

```bash
# /etc/rc.d/init.d/lpd restart
Stopping lpd:      [ OK ]
Starting lpd:     [ OK ]
```

你也可以像本章前面所示的那样，使用 `service` 命令来重启打印守护进程。

这将允许来自任何远程主机的带有正确队列名称（本地打印机名称）的传入打印请求路由到打印机。完成完成后，登录到你局域网（LAN）中一台未连接打印机的远程计算机。

- **提示**：通过 `/etc/lpd.perms` 中的条目，可以将打印服务限制为单个主机、一个或多个特定的本地或远程用户、整个域或局域网网段（通过指定 IP 地址范围）。例如，要仅允许来自 `192.168.2.0` 主机的打印请求，请使用如下条目：
`ACCEPT SERVICE=X REMOTEIP=192.168.2.0/255.255.255`

> **注意**：`lpd.perms` 可能包含一个供你用于创建自定义权限的关键字索引。在对 `/etc/lpd.perms`（或 `/etc/lpd.conf`）进行任何更改后，不要忘记重启 `lpd` 守护进程。

再次使用 `redhat-config-printer` 客户端创建一个新的打印队列。为远程打印机输入名称，然后点击 Networked UNIX (`LPD`) 打印机类型。你将看到如图 12.9 所示的对话框。

- **提示**：选择一个你容易记住或能提供类型或位置分类的打印机名称。良好的候选名称可能是代表位置的 `4th_floor`、颜色的 `winiky`、输出类型的 `colorlaser`、特定型号标识的 `h340`，或表示高速打印机的 `tree-eater`。

完成后，点击前进（Forward）按钮。你将被要求输入带有打印机的远程计算机的主机名（或 IP 地址）以及打印机的队列名称，如图 12.10 所示。

### 创建网络打印机

![](img/e862c5b60f9f55ef43a34453c49f252f_408_0.png)
**图 12.9** 为远程打印机输入本地名称并选择 UNIX 打印机队列。

![](img/e862c5b60f9f55ef43a34453c49f252f_408_1.png)
**图 12.10** 输入带有打印机的远程计算机的主机名或 IP 地址以及远程打印机的队列名称。

> **注意**：访问 http://www.faqs.org/rfc/rfc1179.html 了解更多关于在配置 Red Hat 以打印到远程 UNIX 打印机时“严格 RFC1179 Compliance”选项的信息。这份有12年历史的请求评论（RFC）描述了 BSD 队列打印系统的协议。该选项允许你使用旧的或符合标准的打印系统或软件打印到远程服务器。

输入这些信息后点击前进按钮；然后继续配置新条目，就像远程打印机本地连接一样（使用与远程打印机相同的打印驱动程序）。完成后，不要忘记保存更改并重启 `lpd` 守护进程。新的远程打印机条目 `/etc/printcap` 可能可能所示：

```
hp648:
:ml0#:\n:mx0#:\n:sd=/var/sp/lpd/hp648:\n:af=/var/sp/lpd/hp648.acct:\n:sh:\n:rm=192.168.2.35:\n:rp=lp:\n:lpd_bound=true:\n:if=/user/share/printconf/util/mf_wrapper:
```
