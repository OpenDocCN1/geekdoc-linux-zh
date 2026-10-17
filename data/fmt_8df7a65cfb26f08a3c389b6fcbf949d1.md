
这些材料以精心选择的顺序呈现，就像一位导师坐在你旁边引导你一样。许多作者以“系统化”的方式处理这些材料，从作者的角度看是有意义的，但对新用户来说可能非常令人困惑。

另一个目标是让你熟悉 Unix 式的思维方式，这与 Windows 式的思维方式不同。在旅途中，我们会进行几次小插曲，帮助你理解某些事物为何以这种方式工作以及它们是如何演变而来的。Linux 不仅仅是一段软件，它也是更大 Unix 文化的一部分，Unix 文化有自己的语言和历史。我也可能会发几通牢骚。

本书分为四个部分，每部分涵盖命令行体验的某个方面：

- Part 1 – Learning The Shell 开始我们对命令行基本语言的探索，包括命令的结构、文件系统导航、命令行编辑，以及如何查找命令的帮助和文档。
- Part 2 – Configuration And The Environment 涵盖从命令行编辑控制计算机操作的配置文件。
- Part 3 – Common Tasks And Essential Tools 探索从命令行执行的许多普通任务。类 Unix 操作系统，如 Linux，包含许多用于对数据执行强大操作的“经典”命令行程序。
- Part 4 – Writing Shell Scripts 介绍 shell 编程，一种公认基础但易于学习的技术，用于自动化许多常见的计算任务。通过学习 shell 编程，你将熟悉可应用于许多其他编程语言的概念。

## 如何阅读本书

从本书开头开始，读到结尾。它不是作为参考书编写的，更像是一个有开头、中间和结尾的故事。

## 先决条件

要使用本书，你只需要一个可用的 Linux 安装。你可以通过以下两种方式之一获得：

- 1. 在（不太新的）计算机上安装 Linux。 你选择的发行版并不重要，不过大多数人今天从 Ubuntu、Fedora 或 OpenSUSE 开始。如果有疑问，先尝试 Ubuntu。安装现代 Linux 发行版可能非常简单，也可能非常困难，这取决于你的硬件。我建议使用几年前的一台台式电脑，至少有 256 兆字节的 RAM 和 6 千兆字节的可用硬盘空间。尽可能避免使用笔记本电脑和无线网络，因为这些通常更难使其正常工作。
- 2. 使用“Live CD”。 使用许多 Linux 发行版可以做的一件很酷的事情是直接从 CDROM（或 USB 闪存驱动器）运行它们，而完全不安装它们。只需进入你的 BIOS 设置并将计算机设置为“从 CDROM 启动”，插入 live CD，然后重新启动。使用 live CD 是在安装前测试计算机 Linux 兼容性的好方法。使用 live CD 的缺点是它可能比将 Linux 安装在硬盘上要慢得多。Ubuntu 和 Fedora（以及其他发行版）都有 live CD 版本。

无论你如何安装 Linux，你都需要偶尔拥有超级用户（即管理员）权限来完成本书中的练习。

在你拥有可用的安装后，开始阅读并跟随自己的电脑一起操作。本书的大部分内容都是“动手”的，所以坐下来开始打字吧！

## 为什么我不称它为“GNU/Linux”

在某些圈子里，政治上正确的做法是将 Linux 操作系统称为“GNU/Linux 操作系统”。“Linux”的问题在于没有完全正确的方式来命名它，因为它是由许多不同的人在庞大的分布式开发工作中编写的。从技术上讲，Linux 是操作系统的内核的名称，仅此而已。内核当然非常重要，因为它让操作系统运行起来，但它不足以构成一个完整的操作系统。

于是出现了理查德·斯托尔曼，这位天才哲学家创立了自由软件运动，创办了自由软件基金会，组建了 GNU 项目，编写了 GNU C 编译器（gcc）的第一个版本，创建了 GNU 通用公共许可证（GPL），等等，等等，等等。他坚持你应该称之为“GNU/Linux”以正确反映 GNU 项目的贡献。虽然 GNU 项目早于 Linux 内核，并且该项目的贡献极其值得认可，但在名称中突出它们对其他所有做出重大贡献的人来说是不公平的。此外，我认为“Linux/GNU”在技术上更准确，因为内核先启动，其他一切都在其之上运行。

在流行用法中，“Linux”指的是内核以及典型 Linux 发行版中发现的所有其他自由和开源软件；也就是说，整个 Linux 生态系统，而不仅仅是 GNU 组件。操作系统市场似乎更喜欢 DOS、Windows、Solaris、Irix、AIX 等一词名称。我选择使用这种流行格式。如果你更喜欢使用“GNU/Linux”，请在阅读本书时进行一次心理上的查找替换。我不会介意。

## 致谢

我想感谢以下帮助使本书成为可能的人：

Jenny Watson，Wiley Publishing 的收购编辑，最初建议我写一本 shell 脚本书。

John C. Dvorak，著名专栏作家和评论家。在他的视频播客《Cranky Geeks》的一集中，Dvorak 先生描述了写作过程：“地狱。每天写 200 字，一年后，你就有一部小说了。”这条建议促使我每天写一页，直到写成一本书。

Dmitri Popov 在《Free Software Magazine》上撰写了一篇题为“使用 Writer 创建书籍模板”的文章，这启发我使用 OpenOffice.org Writer 来撰写文本。事实证明，它效果非常好。

Mark Polesky 对文本进行了非凡的审阅和测试。

Jesse Becker、Tomasz Chrzczonowicz、Michael Levin、Spence Miner 也测试并审阅了文本的部分内容。

Karen M. Shotts 贡献了大量时间，通过编辑文本来润色我的所谓英语。

最后，LinuxCommand.org 的读者们，他们给我发了许多亲切的电子邮件。他们的鼓励让我觉得我真的在做一件有意义的事情！

## 需要你的反馈！

本书是一个持续进行的项目，就像许多开源软件项目一样。如果你发现技术错误，请给我发邮件至：

bshotts@users.sourceforge.net

你的修改和建议可能会进入未来的版本。

## 第二版互联网版的新内容

这个版本的 《Linux命令行》 经过了一些额外的润色和现代化处理。特别是假设 bash 4.x 是标准版本，并且文本已更新以反映这一点。第二版互联网版中的章节编号现在与 No Starch Press 版中的编号一致。我还修复了一些错误 ;-)。

特别感谢以下为第一版提供宝贵反馈的个人：Adrian Arpidez、Hu Bo、Heriberto Cantú、Joshua Escamilla、Bruce Fowler、Ma Jun、Seth King、Mike O'Donnell、Parviz Rasoulipour、Gabriel Stutzman 和 Christian Wuethrich。

## 进一步阅读

- 本章中提到的著名人物的一些维基百科文章：
  - http://en.wikipedia.org/wiki/Linus_Torvalds
  - http://en.wikipedia.org/wiki/Richard_Stallman
- 自由软件基金会和 GNU 项目：
  - http://en.wikipedia.org/wiki/Free_Software_Foundation
  - http://www.fsf.org
  - http://www.gnu.org
- Richard Stallman extensively 撰写了关于“GNU/Linux”命名问题的文章：
  - http://www.gnu.org/gnu/why-gnu-linux.html
  - http://www.gnu.org/gnu/gnu-linux-faq.html#tools

## 序言

本书最初使用 OpenOffice.org Writer 在 Liberation Serif 和 Sans 字体上，于出厂配置为 Ubuntu 8.04 的 Dell Inspiron 530N 上编写。文本的 PDF 版本由 OpenOffice.org Writer 直接生成。第二版互联网版是在同一台计算机上使用 Ubuntu 12.04 上的 LibreOffice Writer 制作的。

## 第 1 部分 – 学习 Shell

leges.

假设到目前为止一切顺利，让我们试着输入一些内容。在提示符后输入一些无意义的内容，如下所示：

```
[me@linuxbox ~]$ kaekfjaeifj
```

由于此命令毫无意义，shell 会告诉我们，并给我们另一个机会：

```
bash: kaekfjaeifj: command not found
[me@linuxbox ~]$
```

### 命令历史

如果我们按下上箭头键，我们会看到之前的命令“kaekfjaeifj”在提示符后重新出现。这称为命令历史。大多数 Linux 发行版默认记住最后 500 个命令。按下下箭头键，之前的命令就会消失。

### 光标移动

再次使用上箭头键调出之前的命令。现在尝试左右箭头键。看看我们如何将光标定位在命令行上的任何位置？这使得编辑命令变得容易。

### 关于鼠标和焦点的一些话
