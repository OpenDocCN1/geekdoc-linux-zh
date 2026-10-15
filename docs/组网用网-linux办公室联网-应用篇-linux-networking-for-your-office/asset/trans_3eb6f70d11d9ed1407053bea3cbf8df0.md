
# 文本约定

本书中各种字体用于标识术语和其他特殊对象。这些特殊字体包括以下内容：

| 类型 | 含义 |
|---|---|
| 斜体 | 首次定义时新术语或短语。 |
| 等宽字体 | 计算机呈现的信息，包括文件名、命令名称以及基于 Web 的信息的 URL。来自配置文件中的示例会以整行为等宽文本出现。 |
| 粗体等宽字体 | 您输入到计算机中的信息，例如在命令提示符下输入的命令。 |
| 斜体等宽字体 | 计算机呈现的信息（或如果文本同时为粗体，则为你输入的信息），其内容可能与书中不同。此类信息可能包括网络上计算机的主机名或 IP 地址、任意文件名等。 |
| 大小写 | 文本中菜单名称、对话框名称、对话框元素和命令的大小写与屏幕上显示的方式一致。由于 Linux 是一个区分大小写的操作系统，因此你必须按本书中呈现的大小写输入命令（通常为全小写）。 |

组合键使用加号表示。例如，如果文本要求你输入 Ctrl+S，你需要同时按下 Ctrl 键和 S 键。

我用逗号分隔的选项列表来表示一系列选择。例如，File, Enter 表示选择 File 菜单项，然后在 File 菜单中选择 Enter 项。linuxconf 程序以及其他一些程序会在窗口左侧以展开列表的形式呈现菜单，我使用相同的记号来引用这些菜单，就像引用通常出现在窗口顶部的下拉菜单一样。我对 Linux、Windows 和 MacOS 使用相同的约定。

## 特殊元素

在整本书中，你会找到提示、注释、警告和侧边栏。这些元素提供了各种信息，从不容错过的警告到丰富你的网络体验但并非必读的附属信息。

## TIPS

提示旨在指出你可能 otherwise 会错过的功能、烦恼和技巧。提示通常通过提供比可能立即显而易见的更快或更有效的方法来帮助你更好地使用 Linux 网络。

## NOTES

注释指出你应该注意的事项，虽然你在赶时间时可以跳过这些。一般来说，我添加注释是为了在不拖累你的情况下为你提供有关某个主题的额外信息。

## CAUTIONS

请注意警告！这些可能会为你节省宝贵的工时。不要说我没有警告过你。

## Sidebars

你可以把侧边栏看作是扩展的注释——信息有趣但对理解正文主要观点并非至关重要。侧边栏中的信息比注释中的信息需要更长的解释时间。

## Contacting Me

我欢迎有关本书的评论和建议。你可以发送电子邮件至 smithrod@bellatlantic.net，或访问我的网页 http://members.bellatlantic.net/~smithrod。

## Networking Principles

## PART I

## IN THIS PART

- 1. Networking Hardware — 9
- 2. Understanding TCP/IP — 39
- 3. Networking Services — 55
- 4. Intranets and the Internet — 79

## Networking Hardware

## CHAPTER
1

## IN THIS CHAPTER

- Understanding Ethernet 10
- Network Interface Cards 15
- Using Hubs and Switches 20
- Cabling Choices 25
- Ethernet Kits 26
- DSL and Cable Modems 27
- Telephone Modems 32
- Summary 37

网络允许计算机相互通信。当然，你可能对为计算机本身提供社交生活并不感兴趣；相反，你对使用计算机通信来促进与他人的工作，或提高你自己的工作效率感兴趣。你可以使用计算机网络发送和接收电子邮件，从另一台计算机访问文件，在多台计算机之间共享一台打印机等等。网络的规模可以从简单的两台计算机连接到遍及全球的互联网。本书重点关注对小型网络或大型网络的小型组件最感兴趣的网络任务。

网络需要在两台或多台计算机之间建立连接。一般来说，这些连接是物理的，需要电缆、集线器、交换机、网卡、调制解调器等的组合。存在无线网络，但即使这些也需要在计算机中配备网络硬件。由于网络协议和软件依赖于底层硬件，因此我从对常见网络硬件的讨论开始本书，包括创建自己的局域网所需的硬件以及连接到整个互联网所需的硬件。

## Understanding Ethernet

目前，小型和家庭办公室中最常见的网络硬件类型是 Ethernet。因此，本章乃至整本书都侧重于 Ethernet 网络。本书中讨论的大多数软件和配置也适用于其他类型的网络硬件；但如果你使用的是其他东西，你可能需要在其他地方查找配置必要硬件和驱动程序的文档。Linux HOWTO 集合可能包含符合你要求的文档。

## Types of Ethernet

Ethernet 有几种不同的类型。所有这些的底层原理是相同的，但这些变体在速度、布线以及使用这些变体的计算机如何互连方面有所不同。表 1.1 总结了 SOHO 环境中最常见的 Ethernet 形式。

TABLE 1.1 Varieties of Ethernet

| Name | Top Speed | Cable Format | Maximum Distance |
|---|---|---|---|
| 10base-2 | 10Mbps | Thin coaxial | 607 ft. |
| 10base-5 | 10Mbps | Thick coaxial | 1,640 ft. |
| 10base-T | 10Mbps | Category 3, 4, or 5 twisted-pair | 328 ft. |
| 100base-T | 100Mbps | Category 5 twisted-pair | 328 ft. |

