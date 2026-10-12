
> 多个 FTP 站点提供 Linux 版 OGI 语音工具。你可以在 FTP 站点 `sunsite.unc.edu` 的目录 `/pub/Linux/apps/sound` 或站点 `tsx-11.mit.edu` 的目录 `/pub/Linux/packages/ogi` 中找到最新版本。

OGI 语音工具（相当复杂）的文档位于 FTP 目录中。

### Scheme

Scheme 是一种与 LISP 相关的人工智能语言，但融入了一些 C 元素。Scheme 是一种灵活的编程语言，学习和使用起来出奇地容易。从 FTP 归档站点可获得 Scheme 的几个版本，以及转换为其他语言的转换工具。

### Scilab

Scilab 是一个数学软件包，旨在允许科学家和工程师进行矩阵操作、绘图和功能设计。Scilab 是一个公共领域软件包，旨在与昂贵的商业数学软件包竞争，尽管后者通常具有更好的功能和支持。Scilab 由法国的计算机科学与自动化研究所（INRIA）开发。

**提示**

Scilab 可以从 FTP 站点 `ftp.inria.fr` 的 `/INRIA/Projects/Meta2/Scilab` 目录中下载。通常有几种版本可用，建议获取最新的发行版。

Scilab 非常容易上手，即使对于那些从未使用过交互式数学语言的人来说也是如此。它运行在 X 窗口中，具有惊人的灵活性和强大的功能。

## 摘要

这只是可用于 Linux 的众多流行编程语言中的一小部分。浏览附录 A《Linux FTP 站点和新闻组》中列出的任何 FTP 站点，你可能会发现更多可供你探索的语言。如果你在寻找特定的语言，可以使用搜索引擎尝试定位它。很可能已经有人为你改编了它。从这里，你可以阅读以下相关章节：

- 关于 Smalltalk 语言及其 Linux X 实现的讨论在第 31 章“Smalltalk/X”中。
- 设置 Linux 系统以允许邮件进出你的站点（这对于与其他用户交流你最喜爱的编译器尤其有用）在第 40 章“配置 Linux 邮件系统”中描述。
- 从 Usenet 下载和阅读新闻组，有助于你跟踪你所使用的每种语言的最新动态，这在第 41 章“配置 Linux 新闻系统”中有讨论。

# 第 31 章

## Smalltalk/X

作者：Rick McMullin

### 本章内容

- 什么是 Smalltalk/X？ 544
- 如何安装 Smalltalk/X 544
- 调用 Smalltalk/X 545
- 在 ST/X 中导航 546
- 浏览器选项 547
- 工作区选项 556
- 文件浏览器选项 556
- 项目选项 559
- 实用工具选项 559
- 趣味功能选项 560
- 游戏与演示选项 561
- 在浏览器中编辑 561
- 使用检查器 562
- 使用调试器 563

本章描述了 Linux CD-ROM 中包含的 Smalltalk/X (ST/X) 应用程序。ST/X 是 Smalltalk-80 编程环境相当完整的实现。任何使用过 Smalltalk-80 或其他版本 Smalltalk 的人都会对这一免费实现印象深刻。本章还介绍了 Smalltalk/X 应用程序的概览。阅读本章后，你将熟悉 Smalltalk/X 提供的功能，并能够导航 Smalltalk/X 用户界面。

## 什么是 Smalltalk/X？

在描述 Smalltalk/X 时，可能适合先从描述 Smalltalk 本身开始。Smalltalk 是一种面向对象编程语言，自 20 世纪 70 年代初以来一直是 ParcPlace Systems 的持续发展项目。虽然它不是第一个面向对象的语言，但它是第一个在行业中获得广泛使用的面向对象语言。

Smalltalk 已经存在大约 15 年了，但直到最近它才开始变得流行。许多大学现在将 Smalltalk 课程作为其标准计算机科学课程的一部分，许多公司也看到了 Smalltalk 在快速开发方面带来的价值。

Smalltalk/X 由 Claus Gittinger 开发，并于 1988 年首次发布。它与 Smalltalk 80 对 Smalltalk 语言的实现行为几乎完全相同。Smalltalk/X 附带了应用程序启动器、用于浏览 Smalltalk 类层次结构的几种不同浏览器以及非常强大的调试工具。Smalltalk/X 的独特之处在于它还可以作为 Smalltalk 到 C 的翻译工具。这是一个非常有用的功能，这意味着你可以结合 Smalltalk 提供的开发速度与 C 提供的执行速度。

## 如何安装 Smalltalk/X

虽然 Smalltalk/X 位于随本书提供的 Linux CD-ROM 上，但它不是默认安装脚本的一部分。Smalltalk/X 文件可以在 CD-ROM 的 `devel/smalltalkx` 目录中找到。要安装 Smalltalk/X，请以 root 身份执行以下步骤。

1. 创建一个名为 `/usr/local/lib/smalltalk` 的目录。
2. 将以下文件复制到 `/usr/local/lib/smalltalk` 目录中。
   - `bitmaps.tar.Z`
   - `doc.tar.Z`
   - `exe.tar.Z`
   - `goodies.tar.Z`
   - `source.tar.Z`
3. 输入以下命令解压缩并解包这些文件：
   ```
   uncompress \*.Z
   tar -xf bitmaps.tar
   tar -xf doc.tar
   tar -xf exe.tar
   tar -xf goodies.tar
   tar -xf source.tar
   ```
4. 现在可以通过输入以下命令删除所有 tar 文件：
   ```
   rm \*.tar
   ```

Smalltalk/X 程序现在应该已经安装并准备就绪。如果你没有 `/usr/local/lib` 目录的写入权限，你可以通过遵循上述列出的相同步骤将 Smalltalk/X 安装到其他目录中。如果你这样做，必须将 `SMALLTALK_LIBDIR` 变量设置为等于新目录。

## 调用 Smalltalk/X

通过在 Xterm 窗口中输入 `smalltalk` 来调用 Smalltalk/X。当 ST/X 启动时，它会检查是否有可用的映像文件。如果找不到映像文件，它使用名为 `smalltalk.rc` 的文件来设置环境的默认行为。默认加载的映像文件名为 `st.img`，包含你上次退出时 ST/X 环境的状态快照。这允许你从上次离开的确切位置继续。你可以使用 `.img` 扩展名保存任意名称的快照。要在提示符处输入以下命令以调用除 `st.img` 以外的映像的 ST/X：

```
smalltalk -i nameofImage.img
```

## 在 ST/X 中导航

一旦调用 ST/X，会出现两个窗口或视图。Transcript（记录）视图和 Launcher（启动器）菜单。Transcript 视图如图 31.1 所示。

**图 31.1.**

*Transcript 视图。*

![](img/e8e6b47ac20475e23d48b4c476f5d891_583_0.png)

Transcript 是显示相关系统信息的控制台。Launcher 菜单如图 31.2 所示。

**图 31.2.**

*Launcher 菜单。*

![](img/e8e6b47ac20475e23d48b4c476f5d891_583_1.png)

Launcher 允许访问编写应用程序所需的工具。表 31.1 给出了 Launcher 中可用的选项及其简要描述。

**表 31.1.** LAUNCHER 菜单选项。

| 选项 | 描述 |
| :--- | :--- |
| 浏览器 | 此选项的右拉菜单允许你访问浏览器、发送者和实现者。 |
| 工作区 | 此选项打开工作区视图。 |
| 文件浏览器 | 此浏览器允许检查和操作文件和目录。 |
| 项目 | 此选项允许你选择现有或新的项目。 |
| 实用工具 | 此选项包含针对你编程需求特定的工具。 |
| 趣味功能 | 此选项包含其他与非编程相关的工具。 |
| 游戏与演示 | 此选项包含一些示例程序和可玩的游戏。 |
| 信息帮助 | 此选项包含提供 ST/X 环境信息和 Smalltalk 编程帮助的条目。 |
| 快照 | 此选项拍摄当前 ST/X 环境的快照，并要求输入希望存储快照的映像文件名。 |
| 退出 | 此选项允许你立即退出 ST/X，或退出并保存当前环境的快照。 |

以下部分详细描述了这些选项中的大部分。

## 浏览器选项

Launcher 菜单中的浏览器选项让你可以访问不同的浏览器或编辑器，它们允许你读取和操作类、方法、更改、发送者和实现者。可用的子选项包括：

- 系统浏览器
- 类层次结构浏览器
- 实现者
- 发送者
- 更改浏览器
- 目录浏览器

本节的每一部分将详细讨论这些子选项。

### 系统浏览器

标准系统浏览器包含五个子视图：

- 类类别列表
- 类列表
- 方法类别列表
- 方法列表
