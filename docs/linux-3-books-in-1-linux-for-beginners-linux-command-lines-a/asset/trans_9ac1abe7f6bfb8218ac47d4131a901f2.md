
的服务器是否存在任何安全漏洞。因此，从网络安全的角度来看，这个发行版应运而生。

除了这两个发行版之外，还有许多其他口味的 Linux 等待着你，使用 Linux 的潜力是无限的。

## 参考文献

- 10 Things To Do After Installing Ubuntu 20.04 LTS. (2020, April 23). OMG! Ubuntu! https://www.omgubuntu.co.uk/2020/04/things-to-do-after-installing-ubuntu
- An introduction to the Linux boot and startup processes. (n.d.). Opensource.com. https://opensource.com/article/17/2/linux-boot-and-startup
- Chawla, V. (2020, October 8). Windows Vs macOS Vs Linux: Best OS For Cybersecurity. Analytics India Magazine. https://analyticsindiamag.com/windows-vs-macos-vs-linux-for-cybersecurity/
- How to Install Ubuntu 20.04 LTS {With Screenshots}. (2020, May 25). Knowledge Base by PhoenixNAP. https://phoenixnap.com/kb/install-ubuntu-20-04
- Kiario, J. (n.d.). 10 Linux Distributions and Their Targeted Users. Www.tecmint.com. https://www.tecmint.com/linux-distro-for-power-users/
- Linux History - javatpoint. (n.d.). Www.javatpoint.com. https://www.javatpoint.com/linux-history
- Prakash, A. (n.d.). 16 Things to do After Installing Ubuntu 20.04 - It’s FOSS. Https://Itsfoss.com/. https://itsfoss.com/things-to-do-after-installing-ubuntu-20-04/
- Shell Scripting Tutorial for Linux/Unix Beginners. (2019, November 21). Guru99.com. https://www.guru99.com/introduction-to-shell-scripting.html
- What is Linux? - Linux.com. (2018). Linux.com. https://www.linux.com/what-is-linux/
- What’s new in Ubuntu Desktop 20.04 LTS? (n.d.). Ubuntu. https://ubuntu.com/blog/whats-new-in-ubuntu-desktop-20-04-lts

# LINUX

# Linux 命令行

# 与 Shell 脚本

安迪·维克兰

## 引言

这本关于 Linux 命令行和 Shell 脚本的书籍，提供了经过验证的步骤和策略，教你如何使用键盘输入命令以及编写 Shell 脚本来创建你定制的程序。Linux 比 Windows 和 Mac 操作系统更难驾驭，它是三者中安全性最高的。当你学会了 Linux，你就可以创建定制软件并使用它来完成常见的日常任务。你可以自定义你希望计算机运行的方式。

Linux 操作起来很有趣，但并不简单。与拥有图形界面的 Windows 不同，Linux 拥有命令行。如果你不熟悉什么是命令行，可以参考 Windows 中的 Dos 或命令提示符。那是一个黑色的屏幕，你需要在上面输入命令来完成你的日常任务。

我写这本书分为两部分：第一部分处理命令，第二部分处理 Shell 脚本。除非你很好地掌握了 Linux 命令和 Shell 脚本，否则你无法熟练地操作系统。我在书中打包了你需要用到的最常用且重要的命令。我还包含了一些你在命令行中输入命令后可以看到的结果。

Shell 脚本部分可能比较难。如果你有编程背景，读起来会很有趣。为了练习脚本编写，你需要在编辑器中工作，但别担心，你会在本书后面的章节中找到关于 Linux 编辑器的内容。你可以编写自己的脚本，或者复制我的脚本并粘贴到编辑器中练习。为了方便，我包含了每个脚本的结果，以便你可以进行比较。我还包含了许多关于如何使用命令的基本脚本示例。

## 第一章

### 什么是 Linux？

作为一名 Linux 学生，你首先应该了解 Linux 的起源，以理解这个操作系统背后的概念。Linux 是计算机操作系统中硬件和软件之间的软件层。它允许你在计算机上进行生产性活动并创建定制程序。简单来说，操作系统是软件和计算机系统硬件之间的媒介。操作系统允许你将数据存储在存储设备上，如硬盘、固态硬盘和 USB 驱动器。它管理数据从一个元素到另一个元素的传输；例如，它监督数据从操作系统流向办公室或家庭中的打印机。如果你在计算机系统中安装了普通的 Windows 环境，例如微软 Windows 操作系统，Windows 操作系统将运行硬件。它控制鼠标、键盘、打印机、扫描仪和其他附件。根据你的需要，你将不得不安装 Microsoft Office、Adobe 阅读器、pdf 转换器和其他软件。你需要为每个程序付费并在系统中安装它们。

就控制硬件的过程而言，Linux 与 Windows 操作系统相同。它的不同之处在于它充当软件指令代码和物理设备之间的媒介。最大的区别在于你在 Linux 操作系统中将使用的软件类型。与在 Windows 系统上运行的软件相比，这些软件将是不同类型的。你不能在 Linux 环境中安装和运行 Microsoft Office 或 Adobe Photoshop。Linux 运行不同的服务器，如 Web 虚拟化服务器、Apache 服务器、数据库服务器等。

然而，Linux 有几个专为个人桌面计算机制作的发行版。这些发行版类似于 macOS 和 Windows 操作系统。它们运行相同类型的程序，如文字处理器、图像编辑器和游戏。这些 Linux 发行版似乎更针对寻找免费系统替代方案的家用用户。

Linux 起初并不是作为操作系统或 Windows 操作系统的挑战者而起步的。最初，Linux 恰好是由 Linus Torvalds 创建的一个内核。Linus 当时是赫尔辛基大学的一名学生。内核在系统中仍然很有用。起初，Linux 内核与 GNU 操作系统一起使用。你可以说没有内核，GNU 系统是不完整的。

内核被定义为 Linux 的一个组成部分。内核被认为是操作系统的核心部分，负责应用程序和硬件的所有接口。目前市场上有两种类型的内核，即类 Unix 内核和 Windows 内核。

### Linux 操作系统的诞生

在 1991 年至 1994 年之间，Linus 更进一步，创建了 Linux 操作系统。他将 GNU OS 与 Linux 内核结合起来。一开始，他想创建一个不免费的操作系统，但相反，他需要某种可以根据他的编程需求定制的东西。Linux 起初看起来是他的个人项目。这就像一份副业。UNIX 不同于 Linux 操作系统。

Linus 从零开始构建了整个 Linux 系统。他创建 Linux 是因为他希望为大众构建一个开源操作系统。当时，UNIX 不是开源的。人们必须付费给某人才能使用 UNIX。同样，微软也是一个收费的操作系统。

因此，Linux 提出了开源操作系统的想法。他与来自麻省理工学院（MIT）的朋友一起完善了这个想法。除了构建开源操作系统，他们还需要一个易于使用且高效的操作系统，以便他们可以根据其编程需求进行定制。

### Linux 发行版

当 Linus 正在创建 Linux 操作系统时，他暂停了一段时间。在此期间，他使操作系统的代码公开。这允许每个人参与系统的创建。科学家和电脑迷也开始研究这个概念。他们根据自己的判断修改了操作系统。

主要的教育机构和公司喜欢这个新操作系统的概念，因为任何拥有源代码的人都可以将 Linux 安装在他的计算机上。就是这样，人们开始创建不同版本的 Linux 操作系统。加利福尼亚大学伯克利分校的学生试图开始创建一个版本。来自中国和不同职业的人们也开始创建版本以满足他们的个人需求。

源代码向公众公开促进了发行版（distros）或发行版本的创建。发行版是人们随时间创建的不同版本的 Linux。Linux 有不同的版本，其许多发行版为其提供了多种能力。当你必须决定你需要使用哪个 Linux 发行版时，你必须决定你想让计算机在 Linux 上做什么。我通过一个与 Windows 操作系统类似的类比来解释。当你在我们的计算机上安装 Microsoft Windows 操作系统时，每个发行版都以特定方式构建以完成事情。

有一个名为 Trustix 的 Linux 版本。Linux Trustix 被标记为市场上最安全的 Linux 操作系统。它就像一块砖头。你设置好 Linux Trustix，没有人能够入侵它，除非你做了极其愚蠢的事情。病毒不会偷偷潜入。它是一个安全且坚固的服务器。然而，在你拿起源代码并安装系统之前，你必须决定你确实需要一个安全的服务器。

如果你正在寻找一台你可以使用一些办公应用的计算机，你可能需要 Ubuntu Linux 桌面版本。如果你在寻找一台超级安全的计算机，那么你可能需要 Linux Trustix。如果你期待带有企业级支持的东西，你可能需要使用一个与技术支持中心配对的 Linux 发行版来帮助你。在这种情况下，Red Hat Linux 将是满足你需求的答案。同样，你必须决定你想让计算机做什么，以确定最适合安装在你计算机系统中的 Linux 发行版。

### Linux 是开源的
