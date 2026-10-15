
对于分区，惯例是在驱动器名称末尾添加一个数字。

以下是几个示例：

- `hda1` 是第一个 IDE 驱动器上的第一个分区。
- `hdb5` 是第二个 IDE 驱动器上的第五个分区。
- `sda2` 是第一个 SCSI 或 USB 设备上的第二个分区。

通常，`hda1` 对应于 Microsoft Windows 中的 C 盘。`hdb1` 可能是你在 Microsoft Windows 中的 D 盘，但 Microsoft Windows 中的命名惯例有点神秘。

## 使用 JWM 窗口管理器

Damn Small Linux 还配备了另一个窗口管理器，名为 `JWM`——实际上，Damn Small Linux 中的 `JWM` 版本被精简了一些，部分功能被移除。`JWM` 对来自 Microsoft Windows 环境的用户来说更熟悉。`JWM` 有任务栏和开始按钮。如果你觉得 `Fluxbox` 的开放世界过于庞大，可以尝试 `JWM`。还值得注意的是，`JWM` 非常节省资源，因此如果你有一台性能非常低的电脑，可能想尝试一下 `JWM`。要尝试 `JWM`，请在 `Fluxbox` 菜单的 “WindowManager” 子菜单上点击 “Switch to JWM”。

## 使用 DSL 应用程序

在本节中，我将应用程序分为两类——GUI 和基于终端的。终端应用程序可以在窗口环境中的终端模拟器（如 `Aterm`）中使用，也可以在你处于文本模式时不使用 X 的情况下使用。因此，如果你曾经在一台无法运行 `Fluxbox` 的电脑上，被迫在命令行模式下工作，你可以放心，`DSL` 并不会让你无所适从。

好了，让我们开始查看应用程序。

## 基于 X 的应用程序

在本节第一部分，我们概述了 Damn Small Linux 中找到的基于 X 的应用程序。在这里，你可以找到大多数 Linux 发行版中常见的一些应用程序，以及一些你可能在 Damn Small Linux 中首次尝试的应用程序。

### Aterm—AfterStep 终端模拟器

`Aterm` 是我们选择的终端模拟器，因其体积小巧且可定制性强。尽管体积小，`Aterm` 功能齐全。它能够实现伪透明，而不会占用过多资源。`Aterm` 能够进行着色、字体颜色更改以及阴影设置。另一个视觉效果是，终端内容在失去焦点时会淡出。

> TIP
>
> 如果你想调整字体大小，请尝试 `Shift+KeyPad_Add` 和 `Shift+KeyPad_Subtract`。如果你想要一个易于阅读的大字体，可以从命令行启动 `Aterm`，输入 `aterm -fn 10x20`。
>
> 有关 `Aterm` 的更多信息，请参阅 `Aterm` 主页（`http://www.afterstep.org/aterm.php`）。

### The Ace of Penguins

Ace of Penguins 是一套单人游戏，包括 FreeCell、Golf、Mastermind、Merlin、Minesweeper、Pegged、Solitaire、Taipedit、Taipei 和 Thornq。我玩这些游戏玩得太多了。我建议如果你想保持高效，最好远离它们。

### AxY FTP a GUI FTP Client for X

由 Alexander Yukhimets 编写，我们在 `DSL` 中运行的 `AxY FTP` 版本是 GTK1.2 端口。`AxY FTP` 对许多人来说界面非常熟悉，因为它依赖于 1990 年代流行的经典双面板设计 `ws_ftp`（一个 Microsoft Windows 程序）。`AxY FTP` 有一个方便的会话管理器面板，可以保存你的账户和密码。它还支持递归下载、递归上传以及被动和非被动数据传输。

### Beaver—我们的 GUI 文本编辑器

`Beaver` 最初由 Damien Terrier 开发。它的名字实际上是 *Beaver is an Early AdVanced EditoR* 的缩写，这借用了 UNIX 中具有自递归名称的笑话。在 `DSL` 中，它是其体积范围内功能最丰富的编辑器。它拥有一些体积超过其两倍的浏览器所缺乏的功能。

`Beaver` 非常易用；它有多标签和在多个缓冲区中进行查找替换的能力。程序员会发现可选的颜色高亮对眼睛很友好。休闲桌面用户熟悉剪切和粘贴的典型快捷键。

`Beaver` 的另一个关键功能是能够撤销和重做操作。对于程序员来说，`Beaver` 能够打开和关闭自动换行的功能是必不可少的。`Beaver` 的一些鲜为人知的功能包括其能够将文本文档在 DOS 格式之间转换的能力。这在你在不同平台之间共享文件时非常方便。`Beaver` 还能够将文本大小写转换为大写、小写或正确大小写（每个单词的首字母大写）。`DSL` 中的 `Beaver` 版本是 0.2.7，并已更新了错误修复。

有关 `Beaver` 的更多信息，你可以访问项目的网站：`http://www.nongnu.org/beaver`。

### Calcoo—一个 RPN 和代数计算器

这个基于 GTK1.2 的计算器功能齐全，却只有 108Kbytes。有关 `Calcoo` 的更多信息，请访问其项目网站 `http://calcoo.sourceforge.net`。

### Dillo—一个非常轻量的网页浏览器

`Dillo` 是由 Jorge A. Arellano Cid 为嵌入式或其他受限系统设计的替代轻量级浏览器。这样的浏览器非常适合 `DSL`。

多年来，`Dillo` 的开发非常有条理，项目的作者非常注意编写干净简洁的代码。这意味着 `Dillo` 有一个非常坚实的基础，但它缺乏一个功能齐全的现代浏览器的特性。

尽管 `Dillo` 功能有限，但我们在 `DSL` 中使用的版本经过大量修改，并应用了多个补丁，极大地增强了其能力。我们的 `Dillo` 版本可以完成以下操作：

- 协商 SSL 页面和密码认证
- 渲染框架（frames）和内联框架（iframes）
- 文本搜索
- 执行 GUI 配置
- 支持 referer 数据
- 执行用户代理（user-agent）配置
- 执行 gzip 压缩
- 执行 meta 刷新

`Dillo` 用户会为其加载速度和页面渲染速度之快而感到惊讶。

有关 `Dillo` 的更多信息，请访问 `Dillo` 项目网站 `www.dillo.org`。关于 `Dillo` 国际化的详细信息，请参阅：`http://teki.jpn.ph/pc/software/index-e.shtml`。

### EmelFM——一个高度可配置的双面板文件管理器

`EmelFM` 拥有易于使用的界面；书签和历史记录列表；针对每种文件类型的多操作选择、文件名、大小和日期过滤器；非常方便的内置命令行；用户自定义菜单；可加载插件；以及可配置的工具栏。

在 `DSL` 中，为了方便用户，我们将 `EmelFM` 集成到桌面环境中。例如，在 `Fluxbox` 菜单中，我们同时提供了用户级和根级选项。我们还内置了用于扩展管理的 `MyDSL` 按钮，并让 `emelFM` 在适用时默认使用 `DSL` 原生应用程序。

基本上，我们对 `EmelFM` 进行了配置，使其能够在我们的轻量级环境中工作；因此，它会调用 `Aterm` 而不是 `Xterm`，还会调用我们的 `Wordview` Lua 程序（由 Robert Shingledecker 编写）来查看 Microsoft Word 文档。图 3-5 显示了一个 `EmelFM` 窗口的示例。

有关 `emelFM` 的详细信息，请访问其项目网站 `http://emelfm.sourceforge.net/`。

### Firefox——来自 Mozilla 基金会的开源网页浏览器

`Firefox` 是一款非常强大且功能丰富的浏览器。它是 Damn Small Linux 中目前最大的应用程序，但我们确实采取了一些措施来减小其体积，包括针对 GTK1.2 构建以及让我们的版本使用系统字体。

![](img/af53325d7f38f1cdafca9f44568e4ab8_78_0.png)

#### 图 3-5 使用 emelFM 管理 DSL 中的文件。

`Firefox` 功能非常强大；它拥有完整的 JavaScript 解释引擎，支持渲染 SSI、处理 FTP、认证、动画 GIF、标签页浏览，支持 Java，并且几乎可以完成浏览器所需的一切其他功能。

更多信息请参见 `Firefox` 主页 (`www.mozilla.com/en-US/firefox`)。

### gPhone——一款 VoIP 应用

`gPhone`，即 Gnome-a-Phone，是一款 IP 到 IP 的网络电话，使用 `librtp` 进行音频压缩。虽然 `gPhone` 并非设计用于拨打公共电话（如第 14 章“在 DSL 中使用 Skype VoIP 服务”中所述的 Skype 服务那样），但它确实包含对 RTP/RTCP 的基本支持。这使 `gPhone` 能够让你与支持这些协议的其他网络电话服务通话。

有关 `gPhone` 的更多信息，请访问 `http://gphone.sourceforge.net`。

### gRun——一个基于 GTK 的运行对话框

`gRun` 运行对话框是一个为 GTK1.2 编写的简单应用程序，它允许你无需打开 `Aterm` 窗口或选择菜单即可启动应用程序。

`gRun` 还会存储最近使用列表，因此你可以从下拉菜单中选择，以节省输入时间。
