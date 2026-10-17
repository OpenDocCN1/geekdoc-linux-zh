
## 192 第二部分 Linux 系统管理入门

表 13-1 列出了一些常用的打印软件包。这些软件包运行在多种架构上，包括 Alpha、SPARC、PowerPC 和 Intel x86。访问网站 `www.rpmfind.net/`。软件包列仅显示名称。要获取每个软件包的最新版本号，请浏览 `rpm.org`。

| 软件包 | 功能 |
| --- | --- |
| lpr | 传统的打印队列和配置软件包 |
| LPRng | 下一代打印队列（适用于 UNIX 和作为 Linux 的系统） |
| LPRng-lpd | 普通打印守护进程的增强版 |
| APS-Filter | 终极魔法过滤器 |
| magicfilter | 另一种可扩展魔法过滤器 |
| ImageMagick | X Window下的图像格式转换和显示 |
| ghostscript | PostScript 解释器，允许在非 PostScript 打印机上打印 PostScript |
| ghostview | PostScript 查看器和打印预览（依赖 ghostscript） |
| groff | 文档格式化工具 |
| mpage | 在页纸上打印多页文本 |
| printtool | GUI 打印机配置工具 |
| rhs-filters | 用于 printtool 或 printderrake 的红帽过滤器 |
| tunelp | lp 设备参数的配置工具 |
| enscript | 文本转换器，将 ASCII 和 GNU 文本转换为 PostScript，显示 PDF (Acrobat) 文件 |
| enscript-fonts-koi8 | Enscript 字体 |
| HP-printcap | HP 激光打印机配置工具和实用程序 |
| lpst | Apple StyleWriter 系列打印队列 |
| mpdist | 基于 Motif 的 PostScript 漂亮打印机 |
| lout | 另一种文档格式化语言和工具 |
| pcps | 在 PostScript 打印机上打印文本文件的工具 |
| psutils | 各种 PostScript 工具 |
| tutils | 使用 PostScript 类型 1 字体的工具 |

# 第 13 章 管理打印机与打印 195

提示

从欧洲或美国的网站获取打印包是有区别的。大多数打印包的欧洲版本默认使用 A4 尺寸纸张。大多数美国版本则默认使用 8.5 x 11 英寸纸。你可以通过 `lpr` 命令的选项来覆盖这两个默认值。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_224_0.png)

## 设置打印机守护进程 (lpd)

在配置打印机之前，必须运行 `lpd`。通常情况下，在你启动 Linux 时 `lpd` 就会启动，因为 rc 启动文件（位于 `/etc/rd/rc.*` 目录中）会自动启动和停止 `lpd`。如果你需要手动启动和停止 `lpd`，可以从图形打印实用程序启动（如图 13-1所示），也可以在终端窗口或非图形化控制台中输入以下命令：

```
root@tweety> /usr/sbin/lpd
```

## 设置 printcap 文件

接下来的章节将引导你完成设置 `printcap` 文件的文件的。

## /etc/printcap 文件内部

`printcap` 文件显示了本地连接到 Red Hat 计算机 `fightingpenguin` 的 Canon BJC300 打印机。由于该文件中只有一个条目，`fightingpenguin` 只能看到一台打印机。以 `##PRINTTOOL3##` 开头的行描述了该打印机。

注意

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_224_1.png)

井符号 `#` 是注释字符。

```
root@fightingpenguin) cat /etc/printcap

## /etc/printcap

# 除非你清楚自己在做什么，否则请不要直接编辑此文件！

## 注意，control-printtool 需要非常严格的格式！

## 更多信息请查看 printcap(5) 手册页。

#

## 此文件可以使用控制面板中的 printtool 进行编辑。

##PRINTTOOL3## LOCAL bjc600 360x360 letter () BJC600 8 (

lp0:old_printer_in_the_loft_office\
:sd=/var/spool/lpd/lp0:\n:mx#0:\
:sh:\n:p1#61:pw#80:\
:ip=/dev/lp0:\n:if=/var/spool/lpd/lp0/filter:
```
