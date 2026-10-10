
然后，你可以通过将 `strings` 命令的输出通过 `less` 分页器管道处理来查找文本，如下所示：

```bash
# strings /tmp/hope | less
```

你可以在*Linux Ext2fs Undeletion*小 HOWTO 中找到其他恢复技术的概述（Red Hat 和 Mandrake 用户可以查看 `/usr/doc/HOWTO/mini` 目录下的副本）。你还可以找到保护文件免受删除（即使是 root 操作员）的技术。

最后，请记住，最危险的 Linux 命令可能也是最简短的，这指出了始终以 root 身份运行 Linux 的内在危险。以下简单命令：

```bash
# rm -fr / *
```

将不仅清除你的整个 Linux 文件系统，还会清除其他已挂载的文件系统，包括 Windows 或远程 NFS 分区。

## 资源信息

http://www.computerworld.com/home/print.nsf/all/000207E7A6

一篇描述用于保护笔记本电脑的某些硬件和软件的文章。

http://www.currents.net/magazine/national/1504/cover1504.html#hot

购买二手笔记本电脑的技巧以及如何避免购买被盗笔记本电脑。

http://home.snafu.de/wehe/stolen_laptops.html

被盗笔记本电脑数据库和可追踪笔记本电脑序列号的服务链接列表。

http://www.idlink.com/faq.htm

笔记本电脑的 I.D.LINK 标签系统。

http://www.pcid.com/infopage.htm

笔记本电脑的国家计算机登记册标签系统。

http://www.austprojects.com.au/stop.htm

笔记本电脑的 STOP 标签系统。这相当独特，因为如果标签被移除，笔记本电脑会被标记为“被盗”。

http://support.toshiba-tro.de/internet/info/stolen2.htm

东芝被盗笔记本电脑数据库。

http://www.computrace.com/

CompuTrace（仅限 Windows）用于追踪被盗笔记本电脑的软件。FAQ 列出了盗窃数据。

http://savethelaptop.zzweb.com/

用于追踪被盗笔记本电脑的 Windows 和 Linux 客户端。

http://www.stolencomputers.org/home.html

一个全球被盗计算机数据库，提供免费搜索访问。

http://www.sentryninc.com/

来自 Computer Sentry Systems 的 CyberAngel（仅限 Windows 和 NT）主页。这是用于追踪被盗笔记本电脑的软件。

http://www.panasonic.com/computer/notebook/index.htm

ToughBook 系列笔记本电脑的网站。基于 Intel 的笔记本电脑的顶级保护。

http://www.emj.com

许多不同闪速 RAM 卡、Type II PCMCIA 硬盘和嵌入式系统的来源，例如微型单板 Linux 计算机。

http://www.callunaCard.com

为笔记本电脑生产多种可移动存储设备的制造商。

http://www.hp.com/storage/index.html

Hewlett Packard 的信息存储主页，提供链接到各种 HP 备份设备。

http://www.estinc.com/

Enhanced Software Technologies。Linux 和 UNIX 的 BRU 备份软件之家。

http://www.pcquest.com/mar99/backups.asp

一篇关于使用 Linux 执行备份并避免灾难的好文章。包含 shell 脚本。

http://www.2linuxjournal.com/lj-issues/issue4/2787.html

一篇*Linux Journal*文章，关于从硬盘灾难中恢复。

## Linux Ext2fs Undeletion mini-HOWTO

Aaron Crane 关于使用各种技术和 Linux 软件工具进行文件恢复的精彩教程。

## Linux Tips HOWTO

Paul Anderson 的提示、技巧和陷阱集合，你可以将其用于 Linux，包括直接从 Linux 分区恢复文本文件的部分内容。

## 第 14 章：在路上打印

-   便携式打印机
-   红外打印
-   如果找不到打印机怎么办？
-   资源信息

本章介绍了一些想法、硬件和软件，可以帮助移动 Linux 用户在外时打印文档。虽然我们中的许多人珍视当今更轻、更强大的笔记本电脑，但不幸的是，大多数打印机仍然牢固地属于桌面用户阵营，这是由于尺寸、重量和配件的原因。然而，过去一年左右推出的一些新型号在重量和价格方面具有吸引力，并且它们与 Linux 配合良好。

### 便携式打印机

当你需要在路上打印时，便携式打印机是显而易见的选择。不幸的是，这些类型的打印机只有少数几家制造商生产，因此你的选择可能有限。市场上的那些共享许多共同特征。**以下是一些不错的特性：**

-   轻量——某些型号不到 2 磅
-   内置电池，提供无需墙插的打印能力
-   能够通过直流电源运行（对船主来说是个额外好处）
-   较小的尺寸（比桌面打印机）
-   较小的组件，如墨盒
-   用于与兼容的笔记本电脑和操作系统进行红外打印的 IrDA 端口
-   热打印头，无需更换
-   简化的操作
-   比许多桌面打印机便宜一些
-   彩色和黑白功能
-   在某些型号中，如小型佳能打印机，可更换的打印头可以将打印机变成扫描仪（Linux 不支持）

一些不太吸引人的特性包括以下：

-   每次电池充电的页数有限
-   没有进纸器，或进纸器是昂贵的选项
-   通常比具有类似打印特性（如速度、每英寸点数打印分辨率等）的打印机更昂贵
-   （在大多数型号中）无法处理信封或较大的信封
-   IrDA 端口可能与 Linux 兼容，也可能不兼容
-   热打印机需要更昂贵或难以找到的成卷或成张的热敏纸
-   无法处理如此广泛的纸张重量、类型和尺寸范围
-   相对昂贵的墨盒，且每个墨盒的页数有限

好消息是，如果你没有其他选择，必须在路上打印，这类打印机的优点绝对超过缺点。你肯定会找到适合你需求和价格范围的型号。几乎所有都与 Linux 兼容，因为大多数使用 Hewlett-Packard 的打印机控制语言（HPCL）。额外的好处是，几乎每个 Linux 发行版都包含的 Ghostscript 打印机驱动程序将这些小巧的输出设备变成了微型 PostScript 打印机。

表 14.1 列出了一系列可供路战勇士使用的便携式打印机。它还指出了是否支持 IrDA。

表 14.1 笔记本电脑用户便携式打印机

| 便携式打印机 | IrDA？ | URL |
| --- | --- | --- |
| Brother MP-21C | 否 | www.brother.com/E-product/e-produs.html |
| Brother MP-21C DX | 否 | www.brother.com/E-product/e-produs.html |
| Canon BJC-30 | 是 | www.ccsi.canon.com/ |
| Canon BJC-50 | 是 | www.ccsi.canon.com/ |
| Canon BJC-80 | 是 | www.ccsi.canon.com/ |
| Canon BJC-85 | 是 | www.ccsi.canon.com/ |
| Citizen PN 50 | 否 | www.citizen-america.com/products/portable_printers.htm |
| Citizen PN 60i | 是 | www.citizen-america.com/products/portable_printers.htm |
| HP 340 | 可选 | www.hp.com |
| HP 340Cbi | 是 | www.hp.com |
| HP 350C | 可选 | www.hp.com |
| HP 350Cbi | 是 | www.hp.com |
| Pentax Pocketjet II | 可选 | www.pentaxtech.com/Products/product_frameset.html |
| Pentax Pocketjet 200 | 可选 | www.pentaxtech.com/Products/product_frameset.html |

在接下来的两个部分中，你将了解两个在 300 美元（美国）价格区间内更受欢迎的便携式打印机。两者都与 Linux 配合良好，但你不应将这些视为确定的便携式型号，因为许多打印机，如表 14.1 中列出的 Citizen 和 Pentax 型号，要小得多，也轻得多。在为 Linux 购买便携式打印机之前，务必确保你的经销商提供无理由退货政策，以防你发现打印机在 Linux 下打印时不提供你所需的兼容性、速度或功能。

### **HP 340cbi**

HP340 系列打印机是一款久经考验的便携式打印机，已经存在了一段时间。由典型的 HP 坚固性构建，这款打印机比 HP 的一些最小的喷墨型号（如 HP400）还要小。这款打印机具有以下功能：

-   可拆卸镍镉电池
-   IrDA 端口（打印机上 Centronics 端口的附件）
-   标准并行打印机电缆
-   尺寸：12.2 英寸 × 2.6 英寸 × 5.8 英寸
-   重量：4.3 到 5.4 磅
-   速度：高质量黑白每分钟 2 页，彩色每页 4 到 7 分钟
-   每英寸点数：黑白 600×300，彩色 300×300
-   每次充电页数：未提供
-   纸张重量范围：16- 到 24-磅纸张
-   每个墨盒页数：未提供
-   充电时间：未提供
-   电池寿命：未提供
-   进纸器容量：30 张 16-磅纸

这款打印机虽然被标记为便携式，但不会成为你背包或购物袋中的欢迎伴侣。然而，它相当坚固，比大多数更有可能在摇晃、撞击和振动中幸存。幸运的是，它作为本地或网络打印机与 Linux 非常兼容。不幸的是，其 IrDA 端口与当前的 Linux IrDA 实现或实用程序不兼容。这很遗憾，因为这款打印机是主力，包含 30 页进纸器，并且其他方面在连接到笔记本电脑或 LAN 时工作良好。

