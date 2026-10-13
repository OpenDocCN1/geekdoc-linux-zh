
可以保存超过 20GB 的数据。如果需要备份大量数据，磁带驱动器仍然是最好的选择。然而，便宜的磁带驱动器可能不可靠，而可靠的则相当昂贵（而且通常需要 SCSI 控制器，而大多数电脑现在已不再内置）。介质也不便宜。磁带驱动器最好留给那些必须备份大量数据的人使用。

## Summary

在本小时中，我们了解了 FreeBSD 是什么以及如何使用它。你看到 FreeBSD 是 UNIX 操作系统的一个版本，可免费获得，并且可以安装在任意多台电脑上而无需支付任何许可费用。我们了解了使用 FreeBSD 可以完成的一些事情，包括搭建 Web 服务器、电子邮件服务器、文件服务器或廉价的 UNIX 工作站。我们还将 FreeBSD 与其他操作系统进行了比较，包括 Linux、其他版本的 BSD 和 Microsoft Windows。最后，我们介绍了安装 FreeBSD 的两种方式，并探讨了备份系统的 importance。我们还检查了在安装 FreeBSD 之前可用于备份系统的几种介质类型。

## Q&A

Q Is FreeBSD a “true UNIX,” or is it just “UNIX-like” as some people say?

A FreeBSD 是在加州大学伯克利分校开发的 BSD 代码的许可实现。因为该代码按定义是“真正的 UNIX”，所以 FreeBSD 也是如此。事实上，任何使用此类许可的伯克利代码的操作系统都是如此。

Q Is there a way to run Windows programs within FreeBSD?

A 有正在进行中的项目，其目标是允许用户在 FreeBSD、Linux 或其他此类操作系统中以“仿真模式”运行 Windows 程序。这些项目包括 WINE（较旧的仿真器）和 LinWows 项目，其主要目标是集成 Linux 和 Windows。然而这些都不是成熟或稳定的解决方案，如果你无法放弃游戏，最好的办法还是准备好在需要时启动到 Windows。

Q What’s the best media to use to back up my Windows system before partitioning my disk for dual-booting with FreeBSD?

A 如果你有 CD-R 或 CD-RW 驱动器，这可能是最好的选择。你不需要复制整个硬盘然后稍后恢复它；事实上，不时“彻底清除并重装”Windows 并重新安装软件通常更好。只需担心备份你的个人文档、注册密钥以及所有不属于操作系统或任何特定程序的文件即可。

## Workshop

在本书中，Workshop 部分将通过测验问题、练习和活动来测试你对每个小时课程的掌握。本小时我们讨论了安装前程序，因此目前还没有测验。不过有一些练习可以尝试。

## Exercises

- 1. 去你当地的电子产品商店或你最喜欢的设备供应网站。研究光学介质驱动器（CD-R、CD-RW、DVD-R）、磁带驱动器和 Zip 驱动器的价格。看看是否能找到其中哪些提及除 Windows 之外的任何操作系统的支持。如果有提及 UNIX，你就幸运了。不过很可能 FreeBSD 可以与其中几乎所有设备配合使用。还请查看这些驱动器介质的价格；计算使用每种方法备份所有重要数据需要花费多少。
- 2. 找出一些互联网上最流行的开源软件的开发和分发所依据的许可证条款：Apache 服务器（http://www.apache.org）、BIND（http://www.isc.org/products/BIND/）、Mozilla（http://www.mozilla.org）。这些项目的许可证与 GPL 有什么共同点？它们与 BSD 许可证有什么共同点？

## Hour 2

### Installing FreeBSD

在你实际使用 FreeBSD 之前，需要将其安装到电脑的硬盘上。只要你仔细遵循本小时的说明，这是一个相当简单的过程，不应出现任何问题。本小时你将学习：

- 如何开始 FreeBSD 安装过程
- 如何为 FreeBSD 分区硬盘
- 如何安装 FreeBSD
- 如何安装一些额外软件
- 如何在安装完成后正确关闭系统。

> 我建议你在实际开始安装之前先阅读本章全文。另外，请确保选择一个不会被打扰的时间进行安装。你将做出关于硬盘分区的决定，如果做出错误决定或按错键，可能会导致现有数据丢失。

![](img/ba0161b65b37e94cffc801ecbacaba5e_41_0.png)

![](img/ba0161b65b37e94cffc801ecbacaba5e_41_1.png)

### Beginning the FreeBSD Installation

如前所述，在安装 FreeBSD 之前，你应该做的第一件事是备份系统上你想要保存的任何重要内容——即使你计划使用 Partition Magic 之类的程序重新分区驱动器。虽然这些程序通常在不损坏数据的情况下完成工作，但仍可能出现错误导致你丢失磁盘上的所有内容。因此，始终做好备份是一个好主意。

![](img/ba0161b65b37e94cffc801ecbacaba5e_42_0.png)

> 如果你计划从空白硬盘开始并想安装 Windows 和 FreeBSD，请确保先安装 Windows。如果不这样做，后续安装 Windows 时会做出假设并抹掉 FreeBSD 启动加载程序，这将导致你无法启动到 FreeBSD。另外，在为安装 Windows 分区硬盘时，请确保为 FreeBSD 留出足够的未分区空间。

本书附带的 CD 是可启动的，因此将 CD 放入 CD-ROM 驱动器并重新启动系统。如果系统直接重新启动到 Windows 而不是开始 FreeBSD 安装，你需要更改系统查找可启动设备的顺序。这是在系统 CMOS 设置实用程序中完成的。访问该实用程序的方法在不同系统上有所不同，但通常涉及在系统启动时按下特定的键或键组合。最常见的是删除键或转义键。另外，一旦进入 CMOS，更改启动顺序的方法在各系统间也有差异。基本上，你要寻找类似“Boot device order”的选项。重要的是确保系统首先检查 CD-ROM 驱动器。配置完成后，保存对 CMOS 程序的更改并退出。系统将重新启动，你应该会看到 FreeBSD 安装程序开始。屏幕上会闪过几条消息，最终你应该会看到类似图 2.1 的屏幕。

![](img/ba0161b65b37e94cffc801ecbacaba5e_43_0.png)

FIGURE 2.1
FreeBSD sysinstall 程序的主菜单，可用于安装和配置 FreeBSD。

### sysinstall

sysinstall 程序用于将 FreeBSD 安装到你的电脑上。此时，你唯一需要关注的选项是 Begin a standard installation。不过不要现在选择它，因为下一节提供了有关导航程序的一些基本提示。

### Navigating in sysinstall

关于 sysinstall 首先需要注意的是，你不能使用鼠标。你需要使用键盘在程序中导航。导航相当直观。表 2.1 显示了用于导航 sysinstall 的键。

TABLE 2.1 Keyboard Commands for Navigating sysinstall

| Key | Action |
|---|---|
| Up Arrow | 向上移动到菜单中的上一个选项。 |
| Down Arrow | 向下移动到菜单中的下一个选项。 |
| Left and Right Arrows | 在菜单底部在选项之间切换。例如，在主菜单中，左右箭头键在 Select 和 Exit Install 之间切换。 |
| Spacebar | 在可选择多个选项的菜单中，空格键切换当前突出显示的选项的打开和关闭状态。 |
| Tab Key | 在菜单中与左右箭头具有相同的效果。在需要填写空白的屏幕中在字段之间切换。 |

要开始安装，请从菜单中选择 Begin a standard installation 选项。你会收到一条关于硬盘分区的消息。按 Enter 继续，你的屏幕将看起来像图 2.2。
