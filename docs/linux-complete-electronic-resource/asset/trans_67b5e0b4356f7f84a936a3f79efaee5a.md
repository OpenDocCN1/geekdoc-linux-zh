

## 如何设置基础配置

本节讨论了设置 Linux 系统的最小要求。您将学习如何添加打印队列并打印文档。

### 传统的 lpd 配置

lpd 的最小配置会产生一个可以排队文件并打印它们的系统。它不会关注您的打印机是否能理解这些文件，而且可能无法让您产生美观的输出。尽管如此，它是理解的第一步，所以请继续阅读！

基本上，要向 lpd 添加一个打印队列，您必须在 /etc/printcap 中添加一个条目，并在 /var/spool/lpd 下创建新的 spool 目录。

/etc/printcap 中的一个条目如下所示：

```
# LOCAL  djet500
lpld:d|deskjet:\
:sd=/var/spool/lpd/dj:\
:mx#0:\
:1p=/dev/lp0:\
:sh;
```

这定义了一个名为 lpd、dj 或 deskjet 的 spool，位于目录 /var/spool/lpd/dj 中，没有每个作业的最大大小限制，打印到设备 /dev/lp0，并且在打印作业的开头不会添加横幅页（例如包含打印者姓名等信息）。

**提示**

此时，建议您阅读 printcap 的手册页。

![](img/a3584dae761d2e3abed8bf40d7637389_165_0.png)

上述配置看起来非常简单，但有一个陷阱——除非我发送 DeskJet 500 能够理解的文件，否则这台 DeskJet 会打印出奇怪的东西。例如，将普通的 Unix 文本文件发送到 DeskJet 会导致字面意义上的换行符被解释，并让我反复看到以下内容：

```
This is line one.
This is line two.
This is line three.
```

向此 spool 打印 PostScript 文件会得到 PostScript 命令的美观列表，以这种阶梯效果打印出来，但没有有用的输出。

显然需要更多东西，这就是过滤器的目的。阅读 printcap 手册页的您中更敏锐的人可能会注意到 spool 属性 if 和 of。好吧，if，即输入过滤器，正是这里所需要的。

如果您编写一个名为 filter 的小型 shell 脚本，在换行符前添加回车符，那么阶梯效果就可以消除。因此，您需要在上述 printcap 条目中添加一行 if：

```
lp|dj|deskjet:
    :sd=/var/spool/lpd/dj:\
    :mx#0:\
    :1p=/dev/lp0:\
    :if=/var/spool/lpd/dj/filter:\
    :sh:
```

一个简单的过滤脚本可能如下所示：

```
#!perl
# 上面的行应该包含 perl 的完整路径
# 此脚本必须是可执行的：chmod 755 filter
while(<STDIN>){chop; print "$_\r\n"};
# 您可能还希望以换页符结束：print "\f";
```

如果您执行上述操作，您将拥有一个可以打印常规 Unix 文本文件并获得有意义结果的 spool。（是的，有数百万种更好的方法编写此过滤器，但很少有像这样具有说明性的。鼓励您更高效地实现它。）

剩下的唯一问题是，打印纯文本真的没什么特别之处——当然，能够打印 PostScript 和其他格式化或图形类型的输出会更好。好吧，是的，确实如此，而且很容易做到。该方法只是上述换行修复过滤器的扩展。如果您编写一个过滤器，它可以接受任意文件类型作为输入并为每种情况生成 DeskJet 可识别的输出，那么您就拥有了一个聪明的打印 spooler！

这样的过滤器被称为 magic filter（万能过滤器）。除非您打印奇怪的东西，否则不必自己编写一个——网络上已经有许多为您编写好的。APS Filter 是其中最好的之一，或者您的 Linux 发行版可能有一个打印机设置工具，使这一切变得非常容易。

### 文件权限

应广大要求，我在下面列出了我系统上一些有趣文件的权限。有几种更好的方法来做这件事，理想情况下只使用 SGID 二进制文件，而不将一切都设置为 SUID root，但这是我的系统开箱即用的样子，而且对我有效。（坦率地说，如果您的供应商甚至不能提供一个可用的 lpd，您就有得忙了。）

```
-r-sr-sr-x 1 root   lp /usr/bin/lpr*
-r-sr-sr-x 1 root   lp /usr/bin/lprm*
-rwxr-x--- 1 root   root /usr/sbin/lpd*
-r-xr-xr-x 1 root   lp /usr/sbin/lpc*
drwxrwxr-x 4 root   lp /var/spool/lpd/
drwxr-xr-x 2 root   var /var/spool/lpd/lpr
```

目前 lpd 必须作为 root 运行，以便它可以绑定到低编号的 lpc 服务端口。绑定后，它应该可能变为 UID lp.lpd 或类似的东西，但我想它并没有这样做。太遗憾了。

### 获取打印软件

许多预先编写的过滤器软件包（和其他与打印机相关的软件）可以从 Metalab（ftp://metalab.unc.edu/pub/LINUX/system/printing/）获得。像 pstrips、at2ps、mpaget、dvi2dvi 和 rpc 这样的工具可以在那里找到。

曾经有一段时间，市面上有几个软件包都在努力使打印机配置更容易。它们可能现在仍然存在，但其中最好且最新的之一是 Andreas Klemm 的 APS Filter 软件包，它有一个菜单驱动的 printcap 配置器，并能处理几乎任何可以想象的输入类型。如果您的供应商没有提供不错的打印机设置工具，APS Filter 就是您要走的路。

## 厂商解决方案

按定义，本节是不完整的。欢迎发送您喜欢的发行版的详细信息。

### Red Hat

Red Hat 有一个 GUI 打印机管理工具（在控制面板中），它可以添加远程打印机和本地设备上的打印机。它允许您选择受 Ghostscript 支持的打印机类型和 Unix 设备文件进行打印，然后在 `/etc/`printcap` 中安装一个打印队列，并编写一个基于 `gs` 和 `nscript` 的简短 SolomonP-ASCII 万能过滤器。此解决方案运行相当良好，对于常见情况设置非常简单。

Red Hat 失败的地方在于，当您拥有一台不受其标准 Ghostscript 支持的打印机时（这是 GNU 版本的 Ghostscript，而不是 Aladdin Ghostscript，它支持的打印机更少）。如果发现使用标准 Red Hat 软件无法正常打印，请检查上述打印机兼容列表（或在线访问 `http://www.picate.com/~gstayor/print/printer_list.cgi`）。如果您的打印机不受 Red Hat 工具的支持，您可能需要安装贡献者版本的 Aladdin Ghostscript，并且使用知道最新型号 Ghostscript 支持的打印机的 apsfilter 软件包可能对您更有利。

### Debian

Debian 提供了在普通 lpd 和 LPng 之间选择；LPng 可能是更好的选择。我相信 Debian 也提供了打印机配置工具的选择；apsfilter 5 或更高版本可能是您最好的选择，因为该版本添加了对 LPng 和 Ghostscript 的 uniprint 驱动程序方案的支持。

### 其他发行版

请发送其他发行版的信息给我！

## GHOSTSCRIPT

Ghostscript（`http://www.cs.wisc.edu/~ghost/`）对于 Linux 打印来说是一个极其重要的程序。Unix 下的大多数打印软件生成 PostScript，这通常是打印机上一个价值 100 美元的选项。

然而，Ghostscript 是免费的，并且可以从 PostScript 生成您打印机的语言。当与您的 lpd 输入过滤器结合使用时，它为您提供了一个虚拟的 PostScript 打印机，极大地简化了生活。

Ghostscript 有两种形式。商业版本的 Ghostscript，称为 Aladdin Ghostscript，可以免费用于个人使用，但商业 Linux 发行版不得分发它。它通常比免费的 Ghostscript 领先一年左右；例如，目前它支持许多旧版 Ghostscript 不支持的彩色喷墨打印机。

免费的 Ghostscript 版本是 GNU Ghostscript，它是 Aladdin Ghostscript 的旧版本，被慷慨地赠送给 GNU。（向 Aladdin 致敬；如果有能力，更多的软件供应商应该以这种方式支持免费软件，即使他们无法处理其代码的完全 GPL 分发。）

无论您对 gs 做什么（参见 http://www.picante.com/~gtaylor/phth/man/gs.1.html），请务必使用禁用文件访问的选项（-dSAFER）运行它。PostScript 是一种功能完整的语言，糟糕的 PostScript 程序可能会给您带来相当大的麻烦。

说到 PDF，Adobe 的便携式文档格式实际上不过是压缩文件中有组织的 PostScript。Ghostscript 处理 PDF 输入就像处理 PostScript 一样。因此，您可以成为街区第一个拥有支持 PDF 打印机的用户。

### 调用 Ghostscript

通常，Ghostscript 将由您选定的任何万能过滤器运行（如果您的供应商没有提供适合您的东西，我建议使用 apsfilters），但对于调试目的，直接运行它通常很方便。

Gs -help 将提供选项和可用驱动程序的简明信息列表（请注意，此列表是编译进去的驱动程序列表，而不是所有可用驱动程序的主列表）。

您可能出于测试目的运行 gs，如下所示：`gs <options> -q -dSAFER -soutputFile=/dev/lp1 test.ps`

### Ghostscript 输出调整

如果 gs 的输出不满意，可以做一些事情（实际上，由于您拥有源代码，您可以做任何您高兴做的事）。

![](img/a3584dae761d2e3abed8bf40d7637389_168_0.png)

