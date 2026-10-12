
# 6.12 早期版本的 Emacspeak ............................................................ 1955

# 1934 目录

# 7 常见问题解答 (FAQ)

+ 7.1 为什么在每个字符后都会说“space（空格）”？

+ 7.2 有时详细读模式会为几个单词产生高音

+ 7.3 当 `emacspeak` 启动时显示“No library（未找到库）”信息意味着什么意义？

# 8 法律术语

# 1 引言

`Emacspeak` 是一个提供基础语音访问的 `Emacs` 系统。

屏幕阅读软件允许视障用户通过合成语音获取反馈。此类软件已商业化了十年。它们中的大部分运行在 `DOS` 下的 `PC` 上，现在 `Windows` 平台也有几个屏幕阅读器。然而，`UNIX` 环境下的屏幕阅读器却一直缺席。

这意味着大多数视障用户面临着类似于 `DOS` 限制的额外障碍：

`Emacspeak` 是一个提供基础语音的 `Emacs` 系统。`Emacspeak` 始终存在局限，即它只能在 `Emacs` 中运行。尽管如此，几乎没有什么是在 `Emacs` 内部无法完成的：在 `Emacs` 内部，你可以打开一个“命令行窗口”，运行命令并查看输出，甚至是已经滚动出窗口的内容。`Emacs` 为运行命令提供了特殊模式。例如，它可以解析编译器打印的错误信息，并打开一个光标位于错误处的编辑窗口。它还可以运行调试器，并保持源代码中程序计数器所在的编辑窗口打开。

`Emacspeak` 有一个巨大的优势：它运行在 `Emacs` 内部，这是一种结构敏感且完全自定义的编辑器。与其竞争对手相比，`Emacs` get 它正在说的内容更多的上下文信息。从这个意义上说，`Emacspeak` 并不是“屏幕阅读器”，它是一个提供语音输出的子系统。传统的屏幕阅读器说的是屏幕内容，让用户自己去解释视觉布局的信息。而 `Emacspeak` 则将语音视为一种原生输出模式；它以一种易于听力理解的方式播放信息。

这个初始版本为 `Emacs` 提供了一个基础语音系统；利用 `Emacs` 的强大和灵活性，证明修改语音内容是直观的，例如取决于给定缓冲区的主要的/次要模式。注意，`Emacspeak` 提供的基础功能足以使用大多数 `Emacs` 插件；添加语音特定的定制将使体验变得更加顺畅。

然而，`emacs` 可以用来运行任何具有命令行界面的程序（如 `ls`, `cd`, `rm`, `adduser` 等）。你可以运行那些使用转义序列来控制屏幕外观的 `less` 或 `lynx`。这里的关键在于编辑模式，你通过 `emacs M-x` 即可进入。

# 1. 引言

`Emacs` 是一个大型程序，但它不必驻留在 `RAM` 中，因为 `Linux` 拥有虚拟内存。你可以指定一个交换分区（`swap partition`），这样程序（或程序的局部）在不被使用时就可以被交换出去。你可以使用 8 MB 内存加上 8 MB 的交换空间来流畅地运行 `emacs`。

本文仅限于以下内容：

- `Linux`（非 `Free BSD`）
- `Slack` 发行版（非 `Red Hat`、`Debian` 等）
- 仅限语音输出（不包含盲文显示器 - 请参阅 `access HOWTO`）
- `DECTalk`（`Dectalk Expression` 和 `MultiVoice`）、`DoubleTalk` 以及 `LiteTalk` 合成器（-不包括 `Accent`、`SmartTalk`、声卡等）
- 使用 `Emacs` 配合 `T. V. Raman` 的 `Emacspeak` 来驱动合成器。

关于在 `Linux` 上使用自适应技术，特别是如何使用自适应技术让原本无法使用 `Linux` 的人士也能使用它，这些内容在 `Linux access HOWTO` 中均有所介绍。

如果你想扩展本文以涵盖其他一个或多个替代方案，或者指引我去其他地方参与讨论，请与我联系。

`Emacspeak` 由 `T. V. Raman` (`raman@adobe.com`) 编写。`Emacspeak` 位于网页 `http://www.cs.cornell.edu/Info/People/raman/emacspeak/emacspeak.html`。

`Emacspeak` 支持多种软件。所需的备用软件取决于你如何使用它。

如果你有一个 `DECTalk Expression` 或 `Multivoice`，你需要基础 `Emacs` 软件包、`tcl`（一个解释器）以及 `tcx`（用于 `tcl`）。你可以从 `Emacs` 网页获取 `Emacspeak` 的源码包，或者从一种流行的 `Linux` 发行版（`Slackware`、`Red Hat`、`Debian`）中获取二进制包。我会构建这些软件包中的每一个。由于我通常运行 `Debian`，因此 `Debian` 软件包会比其他包稍早一点发布。目前，`Emacspeak` 的最新版本是 7.0 版。以下是一些 `URL`：

```
http://lib.net/pub/blinux/emacspeak.mirror> http://lib.net/pub/blinux/emacspeak/blinux/emacspeak-6.0-2.1386.rpm
```

注意：`blinux` 站点还有欧洲镜像，如果这些站点关闭，你应该使用它们：

```
<http://ftp.uni-muenchen.de/share/public6/> <http://ftp.gwdg.de/pub/blinux/misc/blinux/>
```

对于外部 `DoubleTalk` 或 `LiteTalk` 合成器，你需要 `Emacs` 软件包以及一个来自 `emacspeak-dt` 软件包的独立驱动程序：

```
<http://lib.net/pub/blinux/emacspeak/emacspeak-dt-0.27.tar.gz> <http://lib.net/pub/blinux/emacspeak/blinux/emacspeak-dt-0.27-1.1386.rpm <http://www.mr.com/ipusers/vandanzt/dt-1.1386.deb
```

对于内部 `DoubleTalk`，你需要三部分软件：基础 `Emacs` 软件包、`emacspeak-dt` 软件包以及一个设备驱动程序。以下是设备驱动的一些 `URL`：

```
<http://lib.net/pub/blinux/emacspeak/blinux/dtlk-1.12.tar.gz> <http://www.mv.com/ipusers/vandanzt/dtlk-1.12.1386.deb
```

针对用于“语音盒”模式的 `Braille 'n' Speak`、`Braille Lite` 和 `Type 'n'` 设备，目前有一个 alpha 测试版本：

```
<http://lib.net/pub/blinux/emacspeak/blinux/emacspeak-bs-0.3.tar.gz>
```

# 1. 目录

计算机硬件、`Unix` 用户命令、`Unix` 系统管理、`Emacs` 和 `Emacspeak` 每一个都是深奥课题。试图一次性学习所有内容可能会导致挫败感。相反，这建议新用户经历一系列阶段，一次学习一个系统。

## 2 阶段 1：带语音的 DOS

大多数盲人计算机用户都使用带有屏幕阅读器程序的语音合成器，例如 `JAWS` [6.1 (JAWS)]。（这种格式的引用指的是下文“脚注和参考文献”部分中的条目。）使用这种设置后，请安装并熟悉一些终端模拟器，如 `Telix` [6.2 (TELIX)] 或 `Commo` [6.3 (COMMO)]，这些可以在 `SimTel` 存档 [6.4 (SimTel)] 等处获取。

### 2.1 通过 CDROM 获取 Linux

如果你有一个 `CD-ROM` 驱动器，我建议你在该介质上获取许多优秀的 `Linux` 发行版之一。下面的说明适用于 `Slack` 发行版。我最熟悉来自 `InfoMagic` [6.5 (InfoMagic)] 的光盘。另一个来源是 `Walnut Creek` [6.6 (Walnut Creek)]（在这里，装满互联网程序的廉价 `CDROM` 整个理念变得兴起）。除了 `Slack` 以外的发行版可以通过 `Red Hat` [6.7 (Red Hat)]、`Craftwork` [6.8 (Craftwork)] 和 `Yggdrasil` [6.9 (Yggdrasil)] 获取。通常情况下，这些 `CDROM` 使用“ISO 9660” 格式，可以在 `DOS` 下读取。它们还使用“Rock Ridge 扩展”，这会在每个目录中添加额外的文件。

### 2.2 通过 FTP 获取 Linux

获取 `Linux` 的另一种方法是通过 `FTP`。`Slack` 发行版可以在许多镜像站获取。以下是列表：

- 欧洲：`http://ftp.uni-muenchen.de/share/public6/`

- 英国：`http://ftp.gwdg.de/pub/blinux/misc/blinux/`

- 日本：（见镜像站）

- 台湾：（见镜像站）

- 香港：（见镜像站）

- 美国：（见镜像站）

（注：上述 `URL` 是根据 OCR 文本结构的示例）。

# 1938

# 目录
