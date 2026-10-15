
然后按照提示定义你的打印机并添加本地或远程打印服务。在保存更改之前，你应该打印测试页。使用打印机配置客户端或 GNOME 或 KDE 客户端文件菜单中的“打印”项。

> 注意：`system-config-printer` 工具是对以前 Red Hat Linux 发行版中包含的旧版 `printtool` 客户端的更新。虽然你可能在系统中发现相关的工具（或符号链接），例如 `printtool`、`printconf-tui` 和 `/usr/sbin/printconf-gui`，但在 Fedora 下你应该使用 `system-config-printer` 客户端管理打印机。

## 配置与管理打印服务

### 基于控制的打印机配置快速上手

本地或远程打印服务也可以在本地或没有 X 窗口系统的服务器上配置。要这样做，你需要使用 Fedora 的基于文本的 `system-config-printer-tui` 打印机配置工具。你必须以 root 运行此命令：

```
# system-config-printer-tui
```

按下回车键后屏幕会清除，你将看到命令的主对话框。（你将在第 23 章“文件与打印”中的“基于控制的打印命令”章节看到此屏幕。）

> 注意：如果你在控制台未使用 X 的情况下以 root 启动 `system-config-printer`，则将使用 `system-config-printer-tui` 界面。

你使用 Tab 键和空格键导航对话框并展开设备列表。你可以通过高亮“New”按钮并按回车键创建新的打印条目。使用向上或向下方向键选择并高亮现有条目；高亮“Edit”按钮并按回车键以编辑之前定义的打印机。

你可以使用 `lpr` 命令从命令行打印文档，使用 `lpq` 查看任何活动任务，并使用 `lprstat` 控制打印队列。

## 管理打印服务

定义打印机后，你可以使用命令行查看并控制打印任务，或者在 root 身份下查看系统上所有的打印任务。以下是 CUPS 及相关命令的部分列表：

### 表 12.1 打印相关命令

| 名称 | 描述 |
| :--- | :--- |
| accept | 控制 CUPS 任务 |
| cancel | 取消 CUPS 任务 |
| disable | 控制 CUPS 打印机 |
| enable | 控制 CUPS 打印任务 |
| encscript | 将文本转换为 PostScript |
| escputil | 通用工具 |
| golbpr | Groff 驱动 |
| gs | Ghostscript 解释器 |
| gsd | Ghostscript 桌面 |
| lpadmin | 基于命令行的工具 |

### 表 12.1 续

| 名称 | 描述 |
| :--- | :--- |
| lp | 启动 CUPS 任务 |
| lpc | Berkeley 子集的 CUPS 控制客户端 |
| lpf | 通用打印过滤器 |
| lrm | 兼容 Berkeley 的 CUPS 任务工具 |
| lpstat | 显示 CUPS 任务和打印机状态 |
| mpage | PostScript 文本格式工具 |
| pbm | 位图工具 |
| pt | 文本格式命令 |
| pr |  |
| psmandup | 双面打印工具 |
| reject | 控制 CUPS 目标 |
| setup | 启动配置工具 |
| smbclient | SMB 后台 |
| smbprint | SMB 打印脚本 |
| smspool | SMB 后台 |
| thinkjettopbm | 位图转 Thinklet |

大多数 Linux 系统使用 PostScript 作为默认文档格式。Fedora 使用 `gs` 命令配合 CUPS 管理远程打印机以及打印任务期间传输的数据类型（通常使用 HP）。

你可以通过带有 `--help` 命令行选项的 Ghostscript 解释器 `gs` 显示其内置打印设备，如下：

```
# gs --help
```

> Fedora 包含了你可以用于查看许多不同类型文档的图形客户端。例如，要显示 PostScript 文档（包括压缩 PostScript 文档）或 PostScript 图像，请使用 `gv` 客户端。要显示 PDF（便文档格式）文档，你可以使用 `gv` 或 `xpdf` 客户端。

`gs` 命令会在屏幕输出大量关于命令行用法文本，然后列出内置打印机和图形设备。获取此信息的另一种方法是启动 `gs` 然后使用 `devenames` 命令，如下：

```
# gs
GNU Ghostscript 7.05 (2002-04-22)
Copyright (C) 2002 artofcode LLC, Benicia, CA. All rights reserved.
This software comes with NO WARRANTY; see the FILE PUBLIC for details.
Loading NimbusRoNo9-Regu font from /usr/share/fonts/default/Type1/
->n021031.pdf... \
```

```
# 创建和配置本地打印机
2410668 1053956 164250 347466
```

正在从 `/usr/share/fonts/default/Type1/n0190031.pbf` 加载 NimbusSanL-Regu字体...

2785628 1379834 1662616 358654 0 完成。

正在为 NimbusSanL-Regu 使用 NimbusSanL-Regu 字体。

/ps/mono/alc8500/lp2563/pkmraw/strap /iwqlq /pbm/md1xXmon/epson/bjc600

-/lbp310 /

/colw2j/cdjcolor/bj10v/cdj160/djet500/ij11rg16/atx23/ij11gray4/st800

-/peggray/necmp6 /

/psgray/alc2800/lp8000/ksm3200/djet3852/pmbraw/DJ630/epsonc/bjc800

-/lbp320 /

/coslxwl/cdjmono/bj10vh/cdj500/laserset/ij11rg32/atx24/ij11mono/stcolor

-/pdfwrite/oce9850 /

/psgrb/cups/lq850/pkmsraw/lx5000/la50 /pgm/DJ66/esc/faxg3/lips2p/cp50

-/cdj50 /

mag16/cdj670/ljetplus/ljet4pj1/atx38/bmpmono/sunmono/pswrite/oki182 /bit

-/cljet5/iml5m70d /

/tfforcle/lex7000/la70/pgmraw/dj6xxp/fs600/faxg32/bjc88oj/declj250 /pj

/mag256/cdj850/ljet2p /

/lj4dithp/bmpa16/bmpgray/t4693d2/epswrite/okiibm/bitbrg/cljet5c/m8510

-/tiffg3/lex5750/la75

![](img/c4a0ea5ab3561ff33a8da88887702720_342_0.png)

此示例列出了所有设备。

## 是 ALADDIN 还是 GNU？

Linux 上至少有两个版本的 Ghostscript 可用。其中一个版本名为 APPL Ghostscript，以前名为 Aladdin Ghostscript。该版本采用 Aladdin Free Public License 许可；另一个版本被称为 GNU Ghostscript，由 GNU General Public License 分发。有关不同版本的详细信息或对许可相关问题的解答，请参阅 http://www.cs.wisc.edu/~ghost/ 上的 Ghostscript 页面。

## 创建和配置本地打印机

为你的 Fedora 系统创建本地打印机可以通过六个简单的步骤完成。你必须拥有 root 权限才能使用 `system-config-printer` 客户端。在开始之前，`cups` 守护进程应该已经在运行（如本章前面所示手动启动守护进程，或使用 `ntsys`、`chkconfig` 或 `system-config-services` 命令确保 `lpd` 在启动时已启动）。

要启动 `system-config-printer`，请从 GNOME 或 KDE 桌面设置菜单中选择“打印”菜单，或在终端窗口中使用如下命令：

```
# system-config-printer &
```

## 创建打印队列
