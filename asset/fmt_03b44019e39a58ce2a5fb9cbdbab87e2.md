
LPRng 通过其命令的手册页以及 `/usr/share/doc/LPRng-3.6.22` 目录下的文档进行记录。你可以在 `http://www.astart.com/lprng/LPRng.html` 找到最新版本和文档（包括一份优秀的 HOWTO 文档）。

## 表 19.3 精选打印命令

| 命令 | 描述 |
| :--- | :--- |
| `cancel` | 用于取消打印服务的 LPRng 工具 |
| `checkpc` | 验证和修复 LPRng 打印系统文件 |
| `lpc` | 本地和远程打印机的控制程序 |
| `lpd` | LPRng 打印服务器守护进程 |
| `lpf` | 通用打印机过滤器 |
| `lpr` | 将打印作业发送到打印机队列 |
| `lprm` | 控制打印队列 |
| `lpstat` | 显示指定打印服务状态 |
| `mpage` | 每页打印多页文本 |
| `nprint` | NetWare 打印客户端 |
| `pbm2ppa` | 将位图转换为 HP PPA 格式 |
| `pbm2tolox` | 将位图转换为 Gemini 打印机图形 |
| `pbm2eopson` | 将位图转换为 Epson 打印机图形 |
| `pbm2oppa` | 将位图转换为 HP PPA 格式 |
| `pbm2ptx` | 将位图转换为 Printtronix 打印机图形 |
| `pnm2ppa` | 将任何映像转换为 HP PPA 格式 |
| `pqlist` | 列出 NetWare 打印队列 |
| `lprm` | 从 NetWare 打印队列中移除作业 |
| `pqstat` | 列出 NetWare 打印队列中的作业 |
| `pr` | 格式化文本文件以便打印 |
| `printmail` | 格式化邮件消息以便打印 |
| `pserver` | NetWare 打印服务器 |
| `sliceprint` | 格式化长行文档 |
| `smbclient` | smbprint 用于打印的必要命令 |
| `smbprint` | 用于向共享打印机打印的 shell 脚本 |
| `testprns` | Samba 的打印机名称检查工具 |
| `tunlp` | 并行端口硬件工具 |

## 其他有用的打印机程序和过滤器

打印机过滤器通过在你的 `/etc/printcap` 文件中定义并插入打印机定义来工作。每个打印机描述中嵌入了一个指向脚本或程序的指针（路径名），其中包含在输出到打印机之前要运行的过滤器。本节介绍你可以在 Red Hat Linux 上尝试的几个辅助打印机过滤器系统。

### Apsfilter

即使你习惯了 printtool 程序，有时你也需要使用其他程序或脚本来帮助设置或管理打印。如果你无法或不想运行 X，但希望轻松安装 HP 或 PostScript 打印机的打印服务，一个很好的解决方案是由 Andreas Klemm 和 Thomas Bueschgens 创建的名为 Apsfilter 的打印过滤器包。安装 Apsfilter 非常快速，使用起来甚至更简单。

Apsfilter 与所有 Linux 打印应用程序都运行良好。两个额外的优点是，当你打印文本文档时，它可以在单页上以横向模式打印两个格式化页面，从而节省纸张，并且“自动”识别以下文档和图形格式：`fig`、`bmp`、`pbm`、`pnm`、`ppm`、`PDF`、`tiff`、`jpeg`、`gif`、Sun rasterfile、PostScript、`dvi`、`raw` ASCII，以及 `gzip` 和 `bzip2` 压缩文件。

你可以在 Apsfilter 的主页 `http://people.FreeBSD.org/~andreas/apsfilter/index.html` 上找到它。

### Magicfilter

另一个与 Apsfilter 类似的打印机过滤器是 H. Peter Anvin 的 magicfilter（也由 David Frey 为 Debian Linux 发行版维护），它通过编译的 C 过滤器和打印机配置文件的组合来检测和转换用于打印的文档。你可以在 `http://www.debian.org/Packages/unstable/text/magicfilter.html` 找到一份副本。

### LPRMagic

Michele Andreoli 的 LPRMagic 是另一个你可以在 Red Hat Linux 下设置的打印机过滤器。所有过滤配置都包含在 `/etc/lprmagic.conf` 文件中。LPRMagic 的一些特性包括文件类型识别（甚至 .wav 和 MIDI！）、延迟打印以及对 Samba 和 LPRng 的支持。安装是通过一组 shell 脚本（以 root 身份执行）完成的。你可以从 `http://metalab.unc.edu/pub/Linux/system/printing/` 下载一份副本。

### HPTools

有一台惠普（Hewlett-Packard）打印机吗？如果是，你可能想尝试 Michael Janson 的 HPTools 来管理你的打印机设置。主要工具是 `hpset` 命令，它提供了超过 13 个命令行选项，你可以使用它们来控制打印机。例如，为了通过使用更少的墨水来节省打印墨盒费用，你可以使用 `hpset` 告知打印机以经济模式打印，代码如下：

```bash
# hpset -c econ | lpr
```

`hpset` 命令还具有一种交互模式，因此你可以测试打印机、设置不同的默认字体，或对打印机进行其他软件控制，例如双向或单向打印。

你可以通过其主页 `http://www.uni-karlsruhe.de/~uips/hptools.html` 找到 HPTools。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_678_0.png)

## PostScript 打印机

如果您想要一个专门为 PostScript 打印机设计的打印作业缓冲区，请尝试 Dave Chappell 的 PPR。PPR 适用于连接在并口、串口和 AppleTalk (LocalTalk) 端口上的打印机，以及其他网络接口。PPR 还可以像其他非 PostScript 打印机过滤器一样工作，并将多种图形文件格式转换为可打印格式。

您可以在 `http://ppr-dist.trincoll.edu/pub/ppr/` 找到 PPR。

## 红外打印机支持

如果您足够幸运，拥有一台支持红外功能的打印机（例如佳能 BJC 50 或 BJC 80，HP LaserJet 6MP 或 HP LaserJet 100TN）以及一个带有红外端口的 Linux 系统（例如笔记本电脑），那么这里有个好消息：您可以不使用打印机线缆进行打印！近期 Linux 设备驱动程序的开发工作已经取得了红外打印（以及网络）支持，最新的 Linux 内核现在内置了 IrDA 支持。IrDA 支持以一系列可加载的内核模块形式提供，并支持系统日志记录、网络、串行端口仿真和打印等功能。

您绝对需要阅读 Warner Heuser 的 IR-HOWTO，它位于 `http://home.snafu.de/wehe/IR-HOWTO.html`。Linux 下的 IrDA 开发仍处于实验阶段，但预示着无线组网、通信、PalmOS 支持以及打印功能的到来！启用红外打印的基本步骤包括：

1. 确定计算机用于 IrDA 端口的正确 `/dev/ttySX` 设备。
2. 启用系统的红外端口。
3. 创建正确的设备，使用 `irattach` 命令启动端口，然后使用 `ircmm` 模块连接端口。
4. 在 `/etc/modules.conf` 文件中创建一个正确的条目，以便在启动时启用该端口。
5. 确保您的设置能够正确检测和识别远程 IrDA 设备。
6. 测试打印机的连接性。

配置好系统后，向红外打印机打印的最简单方法是在 `/etc/printcap` 打印机数据库中创建一个具有特殊名称（例如 `irlp`）的特殊打印机条目。笔记本电脑用户可能需要按某些功能键来禁用现有的串行端口，或启用红外端口。

要下载最新的 irDA 工具集，请访问 `http://www.cs.uiuc.no/linux-irda/`。关于 Canon BJC 80 的可用 irDA 打印系统的详细描述，请访问 Dave Davey 位于 `http://www.physiol.usyd.edu.au/daved/linux/bjc-80.html` 的页面。

## 其他有用的程序

以下是部分提供便捷打印服务的程序的简短描述，这些服务是作为您的 Red Hat 发行版的一部分提供，或者可供下载。您会发现其中一些是不可或缺的。

### pbm 实用程序

要将您的图形文件翻译成或处理成多种格式或效果以便打印，请尝试 Jef Poskanner 提供的 Red Hat Linux 中包含的众多 pbm 实用程序之一。最后一次统计时，约有 100 个程序。使用带有 pbm 和 pm 关键字的 `apropos` 命令可以获取提示。
