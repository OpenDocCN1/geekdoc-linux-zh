

## 所需条件

要学习本书，你必须安装随附光盘中的软件。为此，你需要一台具有以下常规配置的 PC：

- Intel Pentium 或兼容 CPU，200 MHz 或更高（文本模式）；400 MHz 或更高（GUI 模式）。（某些 Intel 486 电脑可能行得通，但不稳定。）
- 至少 64MB 内存。运行 GNOME 或 KDE 桌面需要 128MB，尽管 Red Hat 建议 256MB。
- 至少 510MB 硬盘空间（你必须选择最小安装）。个人桌面安装需要 2.1GB 硬盘空间，典型工作站安装需要 2.6GB，服务器安装至少需要 920MB 空间。安装所有内容大约需要 5.8GB 空间。
- CD-ROM 驱动器。建议用于安装，尽管你也可以通过网络或从本地硬盘安装。对于这些安装方式，你至少需要一个 3.5 英寸软盘驱动器，以及一个额外的硬盘分区或另一台可通过网络访问且存有 Red Hat Linux 光盘软件包或镜像的电脑。（如果你感兴趣，我稍后会告诉你如何操作，见第 2 章。）

并非每一块 PC 硬件都能与 Red Hat Linux 兼容。你可以在 www.redhat.com/hardware 找到适用于 Red Hat 的计算机处理器列表。你可能还想将列表中的其他类型硬件与 Red Hat Linux 系统搭配使用，包括显卡、鼠标、声卡、调制解调器、打印机、扫描仪、游戏杆、PCMCIA 设备和磁带驱动器。

> **交叉引用**：我在第 2 章的 Red Hat Linux 安装描述中更详细地阐述了硬件需求。

## Red Hat Linux Bible 的改进

尽管本书以 Fedora 和 Enterprise Edition 为副标题，但你可以将其视为 Red Hat Linux 发展历程中的更进一步。在随书三张光盘上的 Linux 发行版名称更改为 Fedora Core 之前，该发行版仅仅是下一个 Red Hat Linux（Red Hat Linux 7.3、8、9、…… Fedora）。

也就是说，展望未来，Red Hat 公司已在 Fedora 项目和 Red Hat Linux 企业级产品之间做出了更明确的划分。因此，第 1 章专门描述 Fedora Core 与 Red Hat Enterprise Linux 之间的差异。

由于 Fedora 和 Enterprise 中的大多数技术尚未发生太大偏离，本书中的大多数描述仍适用于两者（Enterprise 包含的“花哨功能和小玩意”比 Fedora 少，但包含更多可扩展至大型服务器的功能）。

作为同样旨在反映 Red Hat Linux 发展历程的书籍，我加入了许多相比前版《Red Hat Linux 9 Bible》的增强内容。其中许多增强内容详述如下：

- **修正 Red Hat Linux** —— 我调整了安装流程以匹配随书附带的 Fedora Core 光盘，并标注了 Red Hat Enterprise Linux 安装过程的不同之处。我还指出 LILO 引导加载程序已从 Fedora 中移除，尽管目前它仍保留在 Enterprise 中。
- **配置 RAID** —— 我提到了在安装过程中配置 RAID 磁盘的能力（第 2 章）。在第 10 章中，我更详细地介绍了在 Red Hat Linux 中如何以及为何设置 RAID 磁盘。
- **GNOME 2.4** —— 虽然 GNOME 2.4 对开发者有重要变化，但对最终用户的变化主要体现在少数新应用程序上。在第 9 章中，我介绍了 Epiphany，它取代 Galeon 成为 GNOME 的默认 Web 浏览器。
- **更多文本编辑器** —— 对于觉得 vi 文本编辑器难用的读者，我在第 4 章中列出了其他几个可供尝试的文本编辑器。
- **使用 yum 获取软件** —— 我在第 5 章中增加了 `yum` 命令和 `yum.conf` 文件的说明。Yum 是一个下载和安装 RPM 格式附加软件包的绝佳工具，这些软件包专门为各 Red Hat Linux 发行版编译（依赖包也会被自动下载安装）。
- **转向 ssh 工具** —— 在此版本中，我尝试从旧的 UNIX 网络工具（`ftp`、`rlogin`、`rsh` 等）转向基于 OpenBSD 安全外壳协议的更新、更安全的命令（`ssh`、`sftp` 等）。`rlogin`、`rsh` 和其他 "r" 命令的说明已移至本书的 Wiley 配套网站。
- **使用 WineX 3.1 Point2Play** —— 在第 7 章中，我增加了 WineX 3.1 新功能 Point2Play 的说明。虽然它不是 Red Hat Linux 的一部分，但这个插件能帮助你在 Linux 中运行 Windows 游戏。
- **酷炫的 Mozilla 浏览技巧** —— 既然我们花这么多时间浏览网页，我喜欢在每版中添加使用 Mozilla 的额外技巧。本版中，我在第 9 章增加了标签式浏览、DOM 检查器和调整网页大小的快捷键的说明。Mozilla 还新增了垃圾邮件功能，帮助你在 Mozilla Mail 中建立自己的反垃圾邮件规则。
- **提升笔记本性能** —— 第 10 章新增一节，介绍如何更好地管理电源并总体提升 Red Hat Linux 下的笔记本性能。
- **使用 up2date 进行软件更新** —— 我增加了关于如何配置 `up2date` 新功能的信息，该功能允许你使用 apt 和 yum 仓库对 Fedora Core 中的 Red Hat Linux 软件进行更新。
- **删除临时文件** —— 我在第 11 章增加了说明，介绍 `tmpwatch` 如何自动清理 Red Hat Linux 中的临时文件。
- **编写 Shell 脚本** —— 我请来了我的朋友、Shell 脚本专家 Kevin Pedigo，彻底改写了第 12 章关于编写 Shell 脚本的部分。除了新示例，Kevin 还增加了在脚本中使用 grep、cut、tr 和 sed 的说明。
- **增强安全性** —— 对于第 14 章，我请安全专家 Chuck Wolber 增加了关于检测和响应拒绝服务攻击、入侵及其他攻击的新章节。
- **创建证书** —— Chuck 对第 14 章的另一重大增强是增加了关于创建和获取 SSL 证书的章节，以使你的 Red Hat Linux 系统能够提供安全通信。
- **一些新选项** —— 通读全书时，我尝试为旧命令添加新选项的说明。本版值得注意的有第 5 章中 `rpm -F` 的说明（一个方便的选项，可一次性更新多个软件包而不安装新包）和第 10 章中 `mount -l` 的说明（当资源繁忙时执行惰性卸载）。
- **从 MAC 使用 Linux NFS 文件共享** —— 我在第 26 章增加了在 Linux 中配置 NFS 的过程，以便 MAC OS X 电脑可以使用来自 Linux 机器的共享 NFS 目录。

除了这些章节，全书的步骤均已测试并修正，以匹配此版本中 Red Hat Linux 软件发生的变化。

## 本书约定

全书使用特殊字体指示代码或命令。命令和代码以等宽字体显示：

```
This is how code looks.
```

如果示例同时包含输入和输出，仍使用等宽字体，但输入以**粗体**呈现以示区分。示例如下：

```
$ **ftp ftp.hansonhistory.com**
Name (home:jake): **jake**
Password: ****
```

以下框框用于引起你对特别重要要点的注意。

> **注意：** “注意”框提供需要你特别留意的额外信息。

> **技巧：** “技巧”框展示执行特定任务的特殊方法。

> **警告：** “警告”框提醒你在执行过程时格外小心，否则可能导致计算机硬件或软件损坏。

> **交叉引用：** “交叉引用”框指引你在当前章节之外查找某主题的更多信息。

## 本书结构

本书分为四部分。

### 第 I 部分：Red Hat Linux 入门

第 I 部分包含第 1 章和第 2 章，简述 Linux 技术，并告知你安装操作系统所需的条件。第 1 章作为 Linux 操作系统的介绍，特别是 Red Hat Linux。我还专门关注 Red Hat 公司在 Fedora 项目与 Red Hat Enterprise Linux 之间的划分。第 2 章讨论安装 Red Hat Linux（Fedora Core 或 Enterprise）所需的条件，以及安装过程中面临的决策。它包含从 CD-ROM、硬盘或网络连接（NFS、FTP 或 HTTP 服务器）安装的步骤。

### 第 II 部分：使用 Red Hat Linux

第 II 部分包含第 3 章至第 9 章，面向必须使用 Linux 运行应用程序和访问互联网的普通用户。在第 3 章中，你将了解 GNOME 桌面环境、KDE 桌面环境和 X Window System。这些 GUI 提供了使用 Red Hat Linux 的图形化手段。第 4 章描述探索和理解 Red Hat Linux 的方法，主要从 Linux Shell 命令解释器入手。你将学习如何使用 *bash* Shell、*vi* 文本编辑器以及在 Linux 文件系统中移动的命令。

第 5 章包含获取、安装和运行 Linux 应用程序的信息。它还帮助你在 Linux 中运行其他操作系统的应用程序。第 6 章介绍随 Red Hat Linux 提供的传统出版工具和新型图形化文字处理器。旧工具包括 *troff* 和 *TeX* 文本处理工具，而较新的出版软件包括 *OpenOffice*（随光盘附带）和 *StarOffice*（商业软件）。

第 7 章介绍在 Red Hat Linux 中运行的图形和字符界面游戏。本章还介绍如何使用 *WineX* 运行商业 Windows 游戏，以及商业 Linux 游戏，如“文明：帝国的召唤”和“神话 II”，其中一些提供演示版。第 8 章介绍如何使用音频和视频播放器，以及如何配置声卡和刻录机。第 9 章介绍浏览网页的工具（如 *Mozilla* 浏览器）和相关工具（如电子邮件客户端和新闻阅读器）。

### 第 III 部分：管理 Red Hat Linux

第 III 部分包含第 10 章至第 14 章，涵盖通用设置和系统维护任务，包括如何设置用户账户、自动化系统任务和备份数据。第 10 章将让你了解基本系统管理所需的知识，

