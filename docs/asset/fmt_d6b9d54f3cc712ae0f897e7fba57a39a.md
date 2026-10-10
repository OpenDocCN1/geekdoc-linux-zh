
然后只需按照提示定义你的打印机并添加本地或远程打印服务即可。在保存更改之前，你应该打印一张测试页。使用打印机配置客户端或从 GNOME 或 KDE 客户端的“文件”菜单中选择“打印”菜单项。

**注意**

`system-config-printer` 实用程序是对之前随 Red Hat Linux 发行版分发的现已成为遗留工具的 `printtool` 客户端的更新。虽然你可能会在系统上找到相关的工具（或符号链接），例如 `printtool`、`printconf-tui` 和 `/usr/sbin/printconf-gui`，但在 Fedora 下管理打印机时，你应该使用 `system-config-printer` 客户端。

## 管理打印服务

定义好打印机后，你可以使用命令行来查看和控制你的打印作业，或者如果是 root 用户，可以控制系统上所有的打印作业和打印机。表 12.1 列出了 Fedora 附带的 CUPS 及相关打印命令和驱动程序的部分列表。

**表 12.1** **与打印相关的命令和驱动程序**

| **名称** | **描述** |

|:-------------------------------------------------------------|:---------------------------------------------------------------|

| a2ps | 将文本文件格式化为用于 PostScript 打印 |

| accept | 控制 CUPS 打印作业目的地 |

| cancel | 取消 CUPS 打印作业 |

| disable | 控制 CUPS 打印机 |

| dvi[[j, l]41, l]2p, l]4] | 将 TeX DVI 文件转换为特定的 PCL 格式 |

| enable | 控制 CUPS 打印机 |

| enscript | 将文本文件转换为 PostScript |

| escputil | Epson Stylus 喷墨打印机实用程序 |

| groff | 用于佳能 LBP-4 和 LBP-8 激光打印机的 groff 驱动程序 |

| gs | Ghostscript 解释器 |

| gsb[[d]500, lp] | Ghostscript BubbleJet 打印机驱动程序 |

| gsdl[d]500, l], lp] | Ghostscript DeskJet 打印机驱动程序 |

| lpadmin | 基于命令行的 CUPS 打印机实用程序 |

| lp | 启动 CUPS 打印作业 |

| lpc | Berkeley 子集 CUPS 打印机控制客户端 |

| lpf | 通用打印机过滤器 |

| lprm | Berkeley 兼容的 CUPS 作业队列实用程序 |

| lpstat | 显示 CUPS 打印作业和打印机状态 |

| mpage | PostScript 文本格式化工具 |

| pbm[[2ppa, page, to1b], topson, toppa, toptx] | 便携式位图转换实用程序 |

| pr | 文本格式化命令 |

| psmandup | 用于非双面打印机的双面打印实用程序 |

| reject | 控制 CUPS 打印作业目的地 |

| setup | 启动打印机配置工具 |

| smbclient | SMB 打印后台处理程序 |

| smbprint | SMB 打印 shell 脚本 |

| smbspool | SMB 打印机后台处理程序 |

| thinkjettopbm | 便携式位图到 ThinkJet 打印机的转换实用程序 |

大多数 Linux 系统使用 PostScript 作为打印的默认文档格式。Fedora 使用 `gs` 命令结合 CUPS 来管理本地和远程打印作业以及打印作业期间传输的数据类型。`gs` 命令用于将文档流翻译为目的地打印机接受的格式（很可能使用 HPGL）。

你可以使用 Ghostscript 解释器 `gs` 通过其 `--help` 命令行选项来显示其内置的打印机设备，方法如下：

```
# gs --help
```

**注意**

Fedora 包含了图形客户端，你可以用它来查看许多不同类型的文档。例如，要显示 PostScript 文档（包括压缩的 PostScript 文档）或 PostScript 图像，请使用 `gv` 客户端。要显示可移植文档格式（PDF）文档，你可以使用 `gv` 或 `xpdf` 客户端。

`gs` 命令会在命令行用法上输出许多行帮助文本，然后列出内置的打印机和图形设备。获取此信息的另一种方法是启动 `gs`，然后使用 `devicenames ==` 命令，如下所示：

```
# gs

GPL Ghostscript 8.60 (2007-08-01)
Copyright (C) 2007 Artifex Software, Inc. All rights reserved.
...输入格式: PostScript PostScriptLevel1 PostScriptLevel2 PostScriptLevel3 PDF
默认输出设备: display
可用设备:
alc1900 alc2000 alc4000 alc4100 alc8500 alc8600 alc9100 ap3250 appledmp
atx23 atx24 atx30 bbx24 bitcmyk bitrgb bj10e bj10v bj10vh bj200 bjC600
bjc800 bjC880 bjc890 bjcslor bjcgrj b1cmo b1cmo bmp16 bcmp256
bmp32b bmpa16 bmpa256 bmpa256 bmpa256 bmpanono bmpase1 bmp4s3 bmpg4y
bmpmono bmpse1 bmpsep8 ccr cdeskjet cdj1600 cdj500 cdj550 cdj670 cdj850
cdj880 cdj890 cdj890 cdj970 cdjm1600 cdjm24 cgm cgm0 cgmmono cgp2200 cf1
cijet5 cj1jet5c cj1jet5f cros1wp cros1w2 cp50 cups delci1250 deskjet
dvicem fax16x9 fax25w display dj505j dj508 dj508c d12100 dnfj650c
ep12050 ep12050p ep12120 ep12500 ep12750 ep15800 ep15900 ep16100 ep16200
epsonlgl epsonmidl epson epsonc epswrite escp escpace fax32 fax643 fax64
...
```

```
搜索路径:
. : /usr/share/ghostscript/8.15/lib :
/usr/share/ghostscript/8.15/Resource : /usr/share/ghostscript/fonts :
/usr/share/fonts/default/ghostscript : /usr/share/fonts/Type1 :
/usr/share/fonts/default/amsfintf/pfb :
/usr/share/fonts/default/cmsfont/pfb : /usr/share/fonts/japanese :
/etc/ghostscript
```

本示例并未列出所有设备。

## Aladdin 还是 GNU？

Linux 至少有两个版本的 Ghostscript 可用。其中一个版本名为 AFPL Ghostscript，以前被称为 Aladdin Ghostscript。该版本采用 Aladdin 自由公共许可证授权，禁止商业分发。另一个版本称为 GNU Ghostscript，采用 GNU 通用公共许可证分发。有关不同版本的详细信息或关于许可证问题的答案，请访问 Ghostscript 主页 http://www.cs.wisc.edu/~ghost/。

## 创建和配置本地打印机

为你的 Fedora 系统创建本地打印机可以通过六个简单步骤完成。你必须拥有 root 权限才能使用 `system-config-printer` 客户端。开始之前，`cupsd` 守护进程也应该正在运行（手动启动守护进程如本章前面所示，或者使用 `ntsysv`、`chkconfig` 或 `system-config-services` 命令确保在启动时启动 `lpd`）。

要启动 `system-config-printer`，请前往“系统”、“管理”，选择“打印”菜单选项，或者使用 X 终端窗口的命令行，如下所示：

```
# system-config-printer &
```

### 创建打印队列
