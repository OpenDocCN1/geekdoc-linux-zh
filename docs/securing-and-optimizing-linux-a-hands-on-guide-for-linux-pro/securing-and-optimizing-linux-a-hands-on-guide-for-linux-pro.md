
# Linux 安全与优化：Linux 专业人士实用指南，RedHat 版

## 简介

当我开始撰写这本书时，我问自己的第一个问题是如何在服务器上安装 Linux，并确保没有任何外部或内部人员能够在未经授权的情况下访问它。接着，我想知道是否存在类似于 Windows 上的方法来提高计算机的性能。随后，我开始在互联网上搜索并阅读多本书籍，以获取有关服务器安全和性能的最大量信息。经过多年的研究和学习，我终于找到了这些问题的答案。这些答案分散在不同的文档、书籍、文章和网站中。我根据我的研究创建了文档，可以帮助我完成日常活动。随着时间的推移，我的文档不断增长，开始看起来更像一本书，而不像简单的零星笔记。我决定将其发布到互联网上，以便任何人都能从中受益。

通过分享这些信息，我觉得我为这个社群做出了贡献——这个社群用一种神奇、可靠、强大、快速且免费的操作系统 Linux 满足了我的许多计算需求。我收到了大量关于我的文档的反馈和评论，这有助于随着时间的推移不断改进它。此外，我发现很多人希望看到它出版，因为其内容可以帮助他们获益，并看到这款优秀的 Linux 系统的强大功能。

本书的制作投入了大量的时间和精力，以确保结果尽可能准确。如果您发现任何异常、不一致的结果、错误、遗漏或任何其他看起来不对的地方，请告诉我，以便我可以调查问题或纠正错误。对未来版本的建议也同样欢迎和感谢。

## 读者对象

本书面向技术读者和系统管理员，他们管理 Linux 服务器，但也包括面向家庭用户和其他人的内容。它讨论了如何安装和设置 Red Hat Linux 服务器，以及为高性能 Linux 专用机器提供所有必要的安全和优化。由于我们谈到优化和安全配置，我们将使用源代码分发（`tar.gz`）程序，这是 Apache、BIND/DNS、Samba、Squid、OpenSSL 等关键服务器软件最常用的类型。源代码包为我们提供了快速升级、必要的安全更新，以及更好的编译、定制和针对我们特定机器的优化，而这些通常是 RPM 包无法提供的。

## 这些安装说明假设

您的计算机上有 CD-ROM 驱动器，以及官方 Red Hat Linux CD-ROM。安装测试已在官方 Red Hat Linux 版本 6.1 和 6.2 上完成。

您应该了解将要安装操作系统的硬件系统。检查硬件后，本文档的其余部分将逐步指导您完成安装过程。

## 关于本书中提到的产品

本书将提到许多产品——有些是商业产品，但大多数不是商业产品，不花任何钱，可以自由使用或分发。同样重要的是，我与其中任何产品都没有关联，如果我提到某个工具，那是因为它有用。您会发现许多大公司在日常使用中使用了其中的大部分。

## 获取本书和示例配置文件

《保护并优化 Linux：RedHat 版》现在也可以在最流行的 Linux 网站上下载。本书的免费格式化版本可以在互联网上通过以下地址找到。

- 原始网站（开放网络架构）：`http://www.openna.com`
- Linux 文档项目主页：`http://www.linuxdoc.org/guides.html`
- O'Reilly 网络：`http://oreilly.linux.com/pub/d/25`
- TuneLinux.COM：`http://tunelinux.com/bin/page?general/optimization/`

可能存在我不知道的其他相关网站。如果您托管这本书（《保护并优化 Linux：RedHat 版》）并希望被列入下一个版本的列表，请给我发送消息说明您的意图。

如果您收到的是印刷发行版或 CD-ROM 的一部分，请查看 Linux 文档主页 `http://www.linuxdoc.org/` 或原始网站 `http://www.openna.com/`，看看是否有更新的版本。这可能会为您省去很多麻烦。如果您想翻译这本书，请通知我，以便我可以跟踪已出版的语种。

本书中的示例配置文件可通过 HTTP 从此 URL 以电子方式获取：

`http://www.openna.com/books/floppy.tgz`

在任何一种情况下，通过键入以下命令从归档中提取文件：

```text
[root@deep tmp]# tar xzpf floppy.tgz
```

如果您无法直接通过互联网获取示例，请通过以下电子邮件地址联系作者：

- `gmourani@openna.com`
- `gmourani@netscape.net`

## 引言

## 致谢

我要感谢米歇尔·梅拉（Michel Méral）为本书绘制了所有精美的动物插图，罗伯特·L·齐格勒（Robert L. Ziegler）允许我收录他的防火墙软件，以及全球所有 Linux 用户的评论和建议。

## Gerhard Mourani 的 GPG 公钥

```text
-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: Garity of this Software), hopefully清洁能源:// the Great奇石ada
```

# 第一部分 安装相关参考

## 本章内容

- Linux 简介
- Linux 服务器的安装

# 第 1 章 Linux 简介

## 本章内容

- 什么是 Linux？
- 使用 Linux 的一些充分理由
- 让我们消除一些关于 Linux 的恐惧、不确定性和疑虑

## Linux 简介

### 什么是 Linux？

Linux 是一种操作系统，最初在芬兰赫尔辛基大学由一位名叫林纳斯·托瓦兹的年轻学生创建。当时，这位学生正在一个昂贵的平台上运行 UNIX 系统。由于预算有限，且需要在家工作，他决定创建一个 UNIX 系统的副本，以便在成本更低的平台上运行，例如 IBM PC。他于 1991 年开始这项工作，发布了 0.02 版本，并持续开发到 1994 年，Linux 内核 1.0 版本正式发布。当时功能完整的版本是 2.2.X（1999 年 1 月 25 日发布），且开发工作仍在继续。

Linux 操作系统在 GNU 通用公共许可证（也称为 GNU GPL）下开发，其源代码通过互联网免费提供给所有下载者。Linux 的 CD-ROM 版本也可在许多商店买到，提供该产品的公司会收取媒体和支持费用。Linux 可用于多种用途，包括网络、软件开发以及作为最终用户平台。Linux 通常被认为是其他更昂贵操作系统的优秀、低成本替代方案，因为您可以在多台计算机上安装它而无需支付额外费用。

### 使用 Linux 的一些充分理由

使用 Linux 无需支付任何授权许可费用，且源代码可以根据您的需求进行修改。修改后的成果可以出售盈利，但原作者保留版权，且您必须提供您修改后的源代码。

由于它附带内核源代码，因此具有相当高的可移植性。Linux 支持的 CPU 和平台数量超过任何其他计算机操作系统。

软件和硬件行业的近期趋势是推动消费者购买速度更快、内存更大、硬盘存储空间更多的计算机。Linux 系统不受这些行业导向的影响，因为它能够在任何类型的计算机上运行，即使是老旧的、基于 486 架构且内存有限的计算机。

Linux 是一个真正的多任务操作系统，与其兄弟 UNIX 类似。它采用先进的、最先进的内存管理技术来控制所有系统进程。这意味着如果某个程序崩溃，您可以终止它并继续安心工作。

另一个好处是，Linux 几乎免疫于我们在其他操作系统中发现的各种病毒。迄今为止，我们只发现两种对 Linux 系统有效的病毒。

### 让我们消除一些关于 Linux 的恐惧、不确定性和疑虑

**它只是一个玩具操作系统。**

财富 500 强企业、政府和消费者越来越多地将 Linux 作为经济高效的计算解决方案。它已被并仍在被 IBM、Amtrak、NASA 等大型公司使用。

**没有技术支持。**

每个 Linux 发行版都附带超过 12,000 页的文档。商业 Linux 发行版，如 Red Hat Linux、Caldera、SuSE 和 OpenLinux，为注册用户提供初始支持，小型企业和企业账户可以通过多家商业支持公司获得 24/7 全天候支持。作为开源操作系统，无需等待六个月的服务发布，在线 Linux 社区可在数小时内修复许多严重的错误。

# 第 2 章 Linux 服务器的安装

## 本章内容

- 了解您的硬件！
- 创建启动盘并启动
- 安装类别和方法
- 磁盘设置
- 要安装的组件
- 单个软件包的选择
- 如何使用 RPM 命令
- 启动和停止守护进程服务
- 服务器安装后必须卸载的软件
- 服务器安装后必须安装的软件
- 服务器上已安装的程序
- 为您的终端添加一些颜色
- 最新软件的更新

## Linux 安装

我们按红帽 Linux CD-ROM 原始安装流程的方式编写了本章。下面的每个部分都会参考并在安装过程中为您提供指导，指导您完成将红帽启动软盘插入计算机后出现的不同屏幕。我们建议您在进行以下步骤时，将准备安装 Linux 的计算机放在手边，这样会非常有助于操作。

红帽 Linux 会不时将其操作系统更新到新版本，并添加、更改或删除一些软件包，同时更改其发行版中某些文件的位置、内容或功能。最近，红帽已将其操作系统更新到 6.2 版本，这是 6.1 版本的小幅升级，因此为了尽可能准确地提供本章中的所有信息，我们将同时评论 6.1 版本和 6.2 版本的安装，以供升级或安装的用户参考。本章中任何提到 6.1 版本的部分均指 Red Hat Linux 6.1 (Cartman) 发行版，任何提到 6.2 版本的部分均指 Red Hat Linux 6.2 (Zoot) 发行版。

### 以下约定将简化本章的理解：

**所有版本**图标适用于 Red Hat Linux 6.1 和 6.2 版本。

**版本 6.1** 图标仅适用于 Red Hat Linux 6.1 版本。

**版本 6.2** 图标仅适用于 Red Hat Linux 6.2 版本。

我们知道许多组织和公司使用不同版本的该操作系统，并在其上运行多种服务。有时升级到最新版本可能很困难，因为客户全天候使用服务器上的服务。通过这个简单的约定，维护和使用 Red Hat Linux 6.1 版本的人员将始终能够找到与其需求相关的准确信息。

## 了解您的硬件！

了解计算机硬件对于成功安装 Red Hat Linux 至关重要。因此，您现在应该花点时间熟悉一下您的计算机硬件。准备好回答以下问题：

1. 您有多少块硬盘？
2. 每块硬盘的容量是多少（例如，3.2GB）？
3. 如果您有多块硬盘，哪一个是主硬盘？
4. 您拥有什么类型的硬盘（例如，IDE、SCSI）？
5. 您有多少内存（例如，256MB RAM）？
6. 您有 SCSI 适配器吗？如果有，制造商和型号是什么？
7. 您有 RAID 系统吗？如果有，制造商和型号是什么？
8. 您使用什么类型的鼠标（例如，PS/2、Microsoft、Logitech）？
9. 您的鼠标有几个按键（2/3）？
10. 如果您使用的是串口鼠标，它连接到哪个 COM 端口（例如，COM1）？
11. 您的显卡品牌和型号是什么？您有多少显存（例如，4MB）？
12. 您使用什么类型的显示器（品牌和型号）？
13. 您将连接到网络吗？如果是，以下信息是什么：
    - a. 您的 IP 地址？
    - b. 您的子网掩码？
    - c. 您的网关地址？
    - d. 您的域名服务器的 IP 地址？
    - e. 您的域名？
    - f. 您的主机名？
    - g. 您的网卡类型（品牌和型号）？
    - h. 您的网卡数量（品牌和型号）？

## 创建启动盘并启动

首先要做的是创建一张安装软盘，也称为启动盘。如果您购买了正版 Red Hat Linux CD-ROM，您会在红帽 Linux 包装盒中找到一张名为“Boot Diskette”的软盘，无需自己创建。有时，您可能会发现使用官方 Red Hat Linux CD-ROM 附带的标准软盘映像进行安装时会失败。如果发生这种情况，需要修订版的软盘才能使安装正常工作。在这种情况下，可以通过红帽 Linux Errata 网页获取特殊的映像来解决问题：`http://www.redhat.com/errata`。由于这种情况相对罕见，您应该先尝试使用标准软盘映像，只有在安装过程中遇到问题时，再去查看 Errata 信息。

### 步骤 1

在创建启动盘之前，将正版 Red Hat Linux CD-ROM 第 1 部分插入运行 Windows 操作系统的计算机。当程序要求输入文件名时，输入 `boot.img` 作为启动盘文件。要在 MS-DOS 下制作软盘，您需要使用以下命令（假设您的 CD-ROM 是 D: 驱动器，且包含正版 Red Hat Linux CD-ROM）。

- 在 Windows 下打开命令提示符：开始 | 程序 | 命令提示符

```text
C:\> d:
D:\> cd \dosutils
D:\dosutils> rawrite
Enter disk image source file name: ..\images\boot.img
Enter target diskette drive: a:
Please insert a formatted diskette into drive A: and press --ENTER-- :
D:\dosutils>
```

`rawrite.exe` 程序会要求输入磁盘映像的文件名：输入 `boot.img`，然后将一张软盘插入 A 驱动器。接着它会要求输入要写入的磁盘：输入 `a:`，完成后，将软盘标记为“Red Hat boot disk”（红帽启动盘）。

### 步骤 2

由于我们要直接从 CD-ROM 开始安装，请使用启动盘启动。将您创建的启动软盘插入要安装 Linux 的计算机的 A: 驱动器，然后重新启动计算机。在 `boot:` 提示符下，按“Enter”继续启动，并按照以下三个简单步骤操作：

- 选择您的语言
- 选择您的键盘类型
- 选择您的鼠标类型

## 安装类别和方法（安装类型）

Red Hat Linux 6.1 和 6.2 包含四种不同的类别或安装类型。它们是：

- GNOME 工作站
- KDE 工作站
- 服务器
- 自定义

前三个类别（GNOME 工作站、KDE 工作站和服务器）允许你选择简化安装流程，但这会显著损失配置灵活性，而这是我们不愿失去的。

因此，我们强烈推荐“自定义”安装，因为这允许你选择要添加的服务以及系统的分区方式。

其理念是加载最少的软件包，同时保持最高效率。系统上驻留的软件越少，可能出现安全漏洞或风险也就越少。

- 选择“自定义”，然后点击“下一步”

## 磁盘设置（Disk Druid）

我们假设你是将新 Linux 服务器安装到一块全新的硬盘上，且该硬盘之前没有安装过任何其他文件系统或操作系统。良好的分区策略是为每个主要文件系统创建独立的分区。这能增强安全性，并防止意外的拒绝服务攻击或 SUID 程序漏洞利用。

创建多个分区为你带来以下优势：

- 防范拒绝服务攻击。
- 防范 SUID 程序。
- 加快启动速度。
- 便于备份和升级管理。
- 更好地控制已挂载文件系统。
- 限制每个文件系统的增长能力。

**警告：**如果目标硬盘和计算机上已存在先前的文件系统或操作系统，我们强烈建议你在进行磁盘分区之前，先备份当前系统。

### 步骤 1

出于性能、稳定性和安全性考虑，你必须在计算机上创建如下所列的分区。我们在此分区配置中假定你有一块 3.2 GB 的 SCSI 硬盘。当然，你需要根据自己的实际需求和磁盘大小来调整分区尺寸。

系统上必须创建的分区：

| 分区 | 大小 | 说明 |
| --- | --- | --- |
| `/boot` | 5MB | 所有内核映像存放于此。 |
| `/usr` | 512MB | 必须足够大，因为所有 Linux 二进制程序都安装在这里。 |
| `/home` | 1146MB | 与你打算承载的用户数量成正比（即每位用户 10MB × 用户数 114 = 1140MB）。 |
| `/chroot` | 256MB | 如果你想在 chroot 监狱环境中安装程序（如 DNS）。 |
| `/cache` | 256MB | 这是代理服务器（如 Squid）的缓存分区。 |
| `/var` | 256MB | 包含系统正常运行时会变化的文件（如日志文件）。 |
| `<Swap>` | 128MB | 我们的交换分区。Linux 操作系统的虚拟内存。 |
| `/tmp` | 256MB | 我们的临时文件分区。 |
| `/` | 256MB | 我们的根分区。 |

我们可以额外创建两个特殊的分区 `/chroot` 和 `/cache`。`/chroot` 分区可用于 chroot 化的 DNS 服务器、chroot 化的 Apache 服务器及其他将来需要 chroot 化的程序。`/cache` 分区可用于 Squid 代理服务器。如果你不打算安装 Squid 代理服务器，则无需创建 `/cache` 分区。

如果用户对服务器拥有 shell 访问权限，将 `/tmp` 和 `/home` 放在独立的分区上几乎是强制性的（防范 SUID 程序），将它们拆分到独立分区还能防止用户填满任何关键文件系统（拒绝服务攻击）；将 `/var` 和 `/usr` 放在独立分区上也是非常好的做法。通过隔离 `/var` 分区，可以保护你的根分区不会被填满（拒绝服务攻击）。



在我们的分区配置中，我们将为 Apache、DNS 及其他软件等 chroot 化程序预留 256 MB 的磁盘空间。这是必需的，因为如果你决定在 chroot 监狱中运行 Apache Web 服务器，Apache 文档根目录文件以及其他相关的二进制文件和程序都将安装在此分区中。请注意，chroot 化分区上 Apache chroot 化目录的大小与你的 `DocumentRoot` 文件大小成正比。如果你不打算在服务器上安装和使用 Apache，可以将此分区大小缩减至约 10 MB，供始终需要在 chroot 监狱环境中运行的 DNS 服务器使用，这是出于安全考虑的。

## 分区最小容量

仅供参考，这是 Linux 安装必须拥有的最小容量（以兆字节计），才能正常运行。以下列出的分区容量非常小。此配置可以装入在老式 x486 计算机中可能找到的 512MB 老式硬盘中。我们向你展示此分区仅为了解最低需求。

```
/      35MB
/boot  5MB
/chroot 10MB
/home  100MB
/tmp   30MB
/usr   232MB
/var   25MB
```

## Disk Druid

Disk Druid 分区是一个为你对硬盘进行分区的程序。选择“添加”以新建分区，“编辑”以修改分区，“删除”以删除分区，“重置”以将分区恢复到原始状态。当你添加新分区时，屏幕上会出现一个新窗口供你选择参数。不同参数如下：

- **挂载点：**用于指定你希望在文件系统中挂载新分区的位置。
- **大小（MB）：**用于指定新分区的容量（以兆字节计）。
- **分区类型：**Linux native 用于 Linux 文件系统，Swap 用于 Linux 交换分区。

如果你使用的是 SCSI 磁盘，设备名将是 `/dev/sda`；如果是 IDE 磁盘，则是 `/dev/hda`。如果你追求高性能和稳定性，强烈推荐使用 SCSI 磁盘。

Linux 使用字母和数字的组合来引用磁盘分区。它采用的命名方案比其他操作系统使用的方案更加灵活，并且能够传递更多信息。以下是概要：

**前两个字母**：分区名称的前两个字母表示该分区所在设备的类型。你通常会看到 `hd`（用于 IDE 磁盘）或 `sd`（用于 SCSI 磁盘）。

**下一个字母**：该字母表示分区所在的设备。例如：`/dev/hda`（第一块 IDE 硬盘）和 `/dev/hdb`（第二块 IDE 磁盘）。

## 交换分区

交换分区用于支持虚拟内存。如果你的计算机内存为 16 MB 或更少，则必须创建交换分区。即使你有更多的内存，仍然建议创建交换分区。交换分区的最小容量应等于你计算机的 RAM 或 16 MB（以较大者为准）。最大可用交换分区约为 1 GB（自 2.2 内核起支持 1 GB 交换文件），因此创建大于该值的交换分区将会浪费空间。但请注意，你可以创建并使用多个交换分区（尽管这通常仅在非常大的服务器安装中才需要）。

> **注意：**尽量将交换分区放在硬盘的起始位置。硬盘的起始位置物理上位于柱面的外圈部分，因此读写磁头每转一圈可以覆盖更大的范围。

现在，举例来说：

要在你的系统上创建以下分区（这是我们服务器安装示例所需的分区），在 Disk Druid 中的操作命令如下：

```
Add
Mount Point: /boot ← 我们的 /boot 目录。
Size (Megs): 5
Partition Type: Linux Native
Ok
```

```
Add
Mount Point: /usr ← 我们的 /usr 目录。
Size (Megs): 512
Partition Type: Linux Native
Ok
```

```
Add
Mount Point: /home ← 我们的 /home 目录。
Size (Megs): 1146
Partition Type: Linux Native
Ok
```

```
Add
Mount Point: /chroot ← 我们的 /chroot 目录。
Size (Megs): 256
Partition Type: Linux Native
Ok
```

```
Add
Mount Point: /cache ← 我们的 /cache 目录。
Size (Megs): 256
Partition Type: Linux Native
Ok
```

```
Add
Mount Point: /var ← 我们的 /var 目录。
Size (Megs): 256
Partition Type: Linux Native
Ok
```

```
Add
Mount Point: ← 我们的 /Swap 分区（将挂载点留空）。
Size (Megs): 128
Partition Type: Linux Swap
Ok
```

```
Add
Mount Point: /tmp ← 我们的 /tmp 目录。
Size (Megs): 256
Partition Type: Linux Native
Ok
```

```
Add
Mount Point: / ← 我们的 / 目录。
Size (Megs): 256
Partition Type: Linux Native
Ok
```

硬盘分区完成后，你的屏幕上应该会看到如下信息。我们的挂载点将如下所示：

| 挂载点 | 设备 | 请求容量 | 实际容量 | 类型 |
|---|---|---:|---:|---|
| `/boot` | `sda1` | 5M | 5M | Linux Native |
| `/usr` | `sda5` | 512M | 512M | Linux Native |
| `/home` | `sda6` | 1146M | 1146M | Linux Native |
| `/chroot` | `sda7` | 256M | 256M | Linux Native |
| `/cache` |  |  |  |  |
| `/var` | `sda9` | 256M | 256M | Linux Native |
| `<Swap>` | `sda10` | 128M | 128M | Linux Swap |
| `/tmp` | `sda11` | 256M | 256M | Linux Native |
| `/` | `sda12` | 256M | 256M | Linux Native |

| 驱动器 | 几何参数 [C/H/S] | 总计 (M) | 空闲 (M) | 已用 (M) | 已用 (%) |
|---|---|---:|---:|---:|---:|
| `sda` | `[3079/64/32]` | 3079M | 1M | 3078M | 99% |

**注意：**我们使用 SCSI 硬盘，因为该设备的前两个字母是 `sd`。

现在进行分区并选择目录的挂载点，选择“下一步”继续。分区创建完成后，安装程序会要求你选择要格式化的分区。选择你要初始化的分区，勾选**（格式化时检查坏块）**复选框，然后按“下一步”。这将格式化分区并使其激活，以便 Linux 可以使用它们。

在下一屏幕，你将看到 LILO 配置，在此处你可以选择将 LILO 引导记录安装在：

- 主引导记录（MBR）
- 引导分区的第一个扇区

通常，如果 Linux 是你机器上唯一的操作系统，你应该选择“主引导记录（MBR）”选项。之后，你需要配置网络和时钟。完成时钟配置后，你需要为系统设置 root 密码和认证配置。

对于认证配置，不要忘记选择：

- 启用 MD5 密码
- 启用 Shadow 密码

不需要选择启用 NIS，因为我们在此服务器上不配置 NIS 服务。

## 要安装的组件（软件包组选择）

分区配置完成并选择格式化后，你就可以选择要安装的软件包了。默认情况下，Linux 是一个功能强大的操作系统，运行许多有用的服务。然而，这些服务中有许多是不需要的，并存在潜在的安全风险。

理想情况下，每个网络服务应该在专用的、单一用途的主机上运行。许多 Linux 操作系统默认配置为提供比提供特定网络服务所需更广泛的这些服务和应用程序，因此你可能需要配置服务器以消除不需要的服务。在特定主机上仅提供必要的服务可以从多个方面增强网络安全：

- 其他服务无法用于攻击主机并损害或删除所需的网络服务。
- 不同的人员可以管理不同的服务。通过隔离服务，使每个主机和服务都有单独的管理员，你将最大限度地减少管理员之间发生冲突的可能性。
- 可以更好地配置主机以满足特定服务的要求。不同的服务可能需要不同的硬件和软件配置，这可能导致不必要的漏洞或服务限制。
- 通过减少服务，日志和日志条目数量减少，因此检测意外行为变得更加容易。

正确安装 Linux 服务器是迈向稳定、安全系统的第一步。你首先必须选择要安装哪些系统组件。选择组件后，你可以通过在 Red Hat 安装屏幕上选择**（选择单个软件包）**选项，来逐一选择或取消选择每个组件中的各个软件包。

由于我们配置的是 Linux 服务器，我们不需要在系统上安装图形界面（XFree86）（服务器上的图形界面意味着更少的进程、更少的 CPU 可用性、更少的内存、安全风险等）。图形界面通常仅用于工作站。

选择以下软件包进行安装：

- 网络化工站
- 网络管理工作站
- 实用工具

选择要安装的组件后，你可以选择或取消选择软件包。

**注意：**在继续之前选择**（选择单个软件包）**选项（非常重要），以便能够选择和取消选择软件包。

## 单个软件包选择

安装程序会显示可用的软件包组列表。选择一个组进行查看。

出于安全、优化以及下面描述的其他原因，以下组件必须从菜单组中取消选择：

| 类别 | 要移除的软件包 |
|---|---|
| 应用程序/文件： | `git` |
| 应用程序/互联网： | `finger`, `ftp`, `fwhois`, `ncftp`, `rsh`, `rsync`, `talk`, `telnet` |
| 应用程序/出版： | `ghostscript`, `ghostscript-fonts`, `mpage`, `rhs-printfilters` |
| 应用程序/系统： | `arpwatch`, `bind-utils`, `knfsd-clients`, `procinfo`, `rdate`, `rdist`, `screen`, `ucd-snmp-utils` |
| 文档： | `indexhtml` |
| 系统环境/基础： | `chkfontpath`, `yp-tools` |
| 系统环境/守护进程： | `XFree86-xfs`, `lpr`, `pidentd`, `portmap`, `routed`, `rusers`, `rwho`, `tftp`, `ucd-snmp`, `ypbind` |
| 系统环境/库： | `XFree86-libs`, `libpng` |
| 用户界面/X： | `XFree86-75dpi-fonts`, `urw-fonts` |

| 类别 | 要移除的软件包 |
|---|---|
| 应用程序/文件： | `git` |
| 应用程序/互联网： | `finger`, `ftp`, `fwhois`, `ncftp`, `rsh`, `rsync`, `talk`, `telnet` |
| 应用程序/出版： | `ghostscript`, `ghostscript-fonts`, `groff-perl`, `mpage`, `pnm2ppa`, `rhs-printfilters` |
| 应用程序/系统： | `arpwatch`, `bind-utils`, `rdate`, `rdist`, `screen`, `ucd-snmp-utils` |
| 文档： | `indexhtml` |
| 系统环境/基础： | `chkfontpath`, `yp-tools` |
| 系统环境/守护进程： | `XFree86-xfs`, `finger-server`, `lpr`, `nfs-utils`, `pidentd`, `portmap`, `rsh-server`, `rusers`, `rusers-server`, `rwall-server`, `rwho`, `talk-server`, `telnet-server`, `tftp-server`, `ucd-snmp`, `ypbind`, `ypserv` |
| 系统环境/库： | `XFree86-libs`, `libpng` |
| 用户界面/X： | `urw-fonts` |

在我们解释要卸载的每个程序的说明之前，有人可能会问为什么需要在服务器上卸载 `finger`、`ftp`、`fwhois` 和 `telnet`。首先，我们知道这些程序本质上是不安全的。现在想象一下，一个黑客已经访问了你的新 Linux 服务器——他可以使用 `finger`、`ftp`、`fwhois` 和 `telnet` 程序来查询或访问你网络上的其他节点。如果这些程序没有安装在你的 Linux 服务器上，他将被迫从外部使用这些程序，或者尝试在你的服务器上安装程序，在这种情况下你可以用 Tripwire 等程序追踪它。尽管像 `telnet`、`finger`、`talk`、`rsh`、`rusers`、`rwall` 和 `tftp` 这样的网络服务在 Red Hat 6.2 版本中被拆分为客户端、服务器端软件包，但为了最高安全性，始终建议卸载它们。

## 出于安全原因必须卸载的程序包说明

以下是程序列表及其用途的简短说明。为了更好的安全性，我们必须卸载它们。有关其功能和用途的更多信息和说明，请参阅 Red Hat 手册或安装软件包并执行 `rpm -qi foo` 命令来查询和获取更多程序说明，然后再卸载它。

## 应用程序/文件

- `GIT` 软件包提供了一个可扩展的文件系统浏览器、一个 ASCII/十六进制文件查看器、一个进程查看器/终止器以及其他相关实用工具和 shell 脚本。**[不必要]**

## 应用程序/互联网

- `finger` 软件包是一个客户端实用工具，允许用户查看系统用户的信息。**[安全风险]**
- `ftp` 软件包提供了标准的 UNIX 命令行 FTP 客户端。**[安全风险]**
- `fwhois` 客户端程序允许查询 whois 数据库。**[安全风险]**
- `Ncftp` 软件包是一个改进的 FTP 客户端。**[安全风险，不必要]**
- `rsh` 软件包提供了客户端程序，允许用户在远程机器上运行命令、登录到其他机器以及在机器之间复制文件（`rsh`、`rlogin` 和 `rcp`）。**[安全风险]**
- `ntalk` 软件包提供了 Internet talk 协议的客户端和守护进程程序，允许你与不同 UNIX 系统上的其他用户聊天。**[安全风险]**
- `Telnet` 是一种用于通过网络登录远程系统的流行协议，但它不安全（以明文传输密码）。**[安全风险]**

## 应用程序/出版

- **所有版本** `GhostScript` 软件包是一组提供 PostScript(TM) 解释器和可移植文档格式（PDF）文件解释器的软件。**[不必要]**
- **所有版本** `GhostScript` 解释器在文本渲染期间可以使用 `Ghostscript-fonts` 软件包。**[不必要]**
- **版本 6.2** `groff-perl` 软件包是一组在打印机环境中使用的命令和打印过滤器。**[不必要，服务器上未安装打印机]**
- **所有版本** `mpage` 软件包实用工具将纯文本文件或 PostScript(TM) 文档作为输入，缩小文本大小，并在 PostScript 打印机上将文件打印在每张纸的多页上。**[不必要，服务器上未安装打印机]**
- **版本 6.2** `pnm2ppa` 软件包是用于 HP PPA 打印机打印的彩色驱动程序。**[不必要，服务器上未安装打印机]**
- **所有版本** `rhs-printfilters` 软件包包含一组打印过滤器，主要用于与 Red Hat printtool 配合使用。**[不必要，服务器上未安装打印机]**

## 应用程序/系统

- **所有版本** `arpwatch` 软件包包含用于监控以太网或 FDDI 网络流量并构建以太网/IP 地址对数据库的实用工具。**[不必要]**
- **所有版本** `bind-utils` 软件包包含一组用于查找 Internet 主机信息的实用工具。**[我们将在本书后面编译它]**
- **版本 6.1** `knfsd-clients` 软件包包含 `showmount` 程序，用于查询远程主机上的 mount 守护进程以获取有关远程主机上 NFS 服务器的信息。**[安全风险，且此服务器上未安装 NFS 服务]**
- **版本 6.1** `procinfo` 软件包从运行中的内核获取有关系统的信息。**[不必要，存在其他方法]**
- **所有版本** `rdate` 软件包实用工具可以从网络上的另一台机器检索日期和时间。**[安全风险]**
- **所有版本** `rdist` 软件包是一个在多个主机上维护相同文件副本的程序。**[安全风险]**
- **所有版本** `screen` 软件包是一个有用的实用工具，适用于通过 `telnet` 登录到机器或通过哑终端连接，但希望使用多个登录的用户。**[不必要]**
- **所有版本** `ucd-snmp-utils` 软件包包含用于 `ucd-snmp` 网络管理项目的各种实用工具。**[不必要，安全风险]**

## 文档

- `indexhtml` 软件包包含 Web 浏览器在 X Window 系统中显示的欢迎页面的 HTML 页面和图形。**[不必要，我们不使用图形界面]**

## 系统环境/基础

- `chkfontpath` 软件包是一个简单的程序，用于添加、删除和列出 X 字体服务器路径中的目录。**[不必要，我们不使用图形界面]**
- 网络信息服务（NIS）是一个系统，它向网络上的所有机器提供并集中管理网络信息（登录名、密码、主目录和组信息）。**[安全风险，我们在服务器上不使用它]**

## 系统环境/守护进程

- `XFree86-xfs` 软件包是 XFree86 的字体服务器，也可以远程为其他 X 服务器提供字体。**[不必要，我们不使用图形界面]**
- `finger-server` 软件包包含从 `/etc/inetd.conf` 文件运行的 finger 守护程序，允许用户查看服务器上系统用户的信息。**[安全风险]**
- `lpr` 软件包提供了管理打印服务的基本系统工具。**[不必要，服务器上没有安装打印机]**



- `nfs-utils` 软件包为内核 NFS 服务器提供工具和守护程序。如果你想在服务器上提供 NFS 服务，必须安装此软件包。**[安全风险，且此服务器上未安装 NFS 服务]**
- `pidentd` 软件包包含 `identd`，它查找特定的 TCP/IP 连接，并返回拥有该连接的进程的用户名或其他信息。**[不必要，网络上很少有什么东西要求发送方运行 `identd`，因为许多机器没有它，而且许多人将其关闭。]**
- `portmapper` 软件包管理 RPC 连接，NFS 和 NIS 等协议使用这些连接。**[不必要，安全风险，且此服务器上未安装 NIS/NFS 服务]**
- `rsh-server` 软件包提供 `rsh`、`rlogin`、`rcp` 所需的服务器，允许用户在远程机器上运行远程访问命令。**[安全风险]**
- `routed` 软件包路由守护程序通过处理传入的 RIP 流量和广播有关网络流量路由的传出 RIP 流量来维护当前路由表。**[不必要，安全风险，且功能有限]**
- `rusers` 软件包程序允许用户查找本地网络上各种机器的登录者。**[安全风险]**
- `rusers-server` 软件包包含服务器，它响应用户请求并允许他们查看谁登录了你的机器。**[安全风险]**
- `rwall-server` 软件包包含守护程序，允许接收来自远程主机用户的远程消息。**[安全风险]**
- `rwho` 软件包显示本地网络上运行 `rwho` 守护程序的所有机器的登录者。**[安全风险]**
- `talk-server` 软件包提供守护程序，允许你通过终端与远程 UNIX 系统的其他用户聊天。**[安全风险]**
- `tftp` 软件包或称为简单文件传输协议（TFTP），允许用户与远程机器之间传输文件。它通常仅用于启动无盘工作站。**[安全风险，不必要]**
- `telnet-server` 软件包提供守护程序，允许通过 telnet 远程登录协议连接到服务器。**[安全风险，由 SSH 替代]**
- `tftp-server` 软件包提供 TFTP 的服务器，允许用户与远程机器之间传输文件。**[安全风险，不必要]**
- `ucd-snmp` 软件包或称为 SNMP（简单网络管理协议）是用于网络管理的协议。**[不必要，安全风险]**
- `ypserv` 软件包是 NIS（网络信息服务）服务器，它向网络上的所有机器提供网络信息（NIS）。**[安全风险，我们在服务器上不使用它]**

## 系统环境/库

- `XFree86-libs` 软件包包含大多数 X 程序正常运行所需的共享库。**[不必要，我们不使用图形界面]**
- `libpng` 软件包包含用于创建和操作 PNG 图像格式文件的函数库。PNG 是一种类似于 GIF 格式的位图图形格式。**[不必要]**

## 用户界面/X

- `XFree86-75dpi-fonts` 软件包包含大多数 X Window 系统上使用的 75 dpi 字体（标准字体）。**[不必要，我们不使用图形界面]**
- `urw-fonts` 软件包包含 35 种标准 Type 1 PostScript 字体的免费版本。**[不必要，我们不使用图形界面]**

此时，安装程序将格式化你在系统中选择要格式化的每个分区。这可能需要几分钟，具体取决于你机器的速度。一旦所有分区都格式化完毕，安装程序将开始安装软件包。

## 如何使用 RPM 命令

本节概述了在 Linux 系统上安装、卸载、升级、查询、列出和检查 RPM 软件包的主要模式。你现在必须熟悉这些 RPM 命令，因为我们在本书的后续内容中会经常使用它们。

- 要安装 RPM 软件包，请使用以下命令：

```bash
[root@deep /]# rpm -ivh foo-1.0-2.i386.rpm
```

请注意，RPM 软件包的文件名形如 `foo-1.0-2.i386.rpm`，其中包括软件包名称（`foo`）、版本（`1.0`）、发布版本（`2`）和体系结构（`i386`）。

- 要卸载 RPM 软件包，请使用以下命令：

```bash
[root@deep /]# rpm -e foo
```

请注意，我们使用的是软件包名称 `foo`，而不是原始软件包文件名 `foo-1.0-2.i386.rpm`。

- 要升级 RPM 软件包，请使用以下命令：

```bash
[root@deep /]# rpm -Uvh foo-1.0-2.i386.rpm
```

使用此命令，RPM 会自动卸载旧版本的 `foo` 软件包并安装新版本。始终使用 `rpm -Uvh` 来安装软件包，因为即使之前没有安装过该软件包的版本，它也能正常工作。

- 要查询 RPM 软件包，请使用以下命令：

```bash
[root@deep /]# rpm -q foo
```

此命令将打印已安装软件包 `foo` 的名称、版本和发布版本号。使用此命令可验证系统中是否已安装或未安装某个软件包。

- 要显示软件包信息，请使用以下命令：

```bash
[root@deep /]# rpm -qi foo
```

此命令显示软件包信息；包括已安装程序的名称、版本和描述。使用此命令获取已安装软件包的信息。

- 要列出软件包中的文件，请使用以下命令：

```bash
[root@deep /]# rpm -ql foo
```

此命令将列出已安装 RPM 软件包中的所有文件。它仅在软件包已安装在你的系统上时才有效。

- 要运会检查 RPM 签名软件包，请使用以下命令：

```bash
[root@deep /]# rpm --checksig foo
```

此命令检查指定软件包的 PGP 签名，以确保其完整性和来源。在系统上安装新的 RPM 软件包之前，始终要先使用此命令。此外，在使用此命令之前，你的系统上必须已经安装了 GnuPG 或 Pgp 软件。

## 启动和停止守护程序服务

Linux 的 `init` 程序（也称为进程控制初始化）负责在系统启动时启动所有需要运行的正常和经授权的进程。这些可能包括 APACHE 守护程序、网络守护程序以及机器启动时必须运行的任何其他程序。每个这样的进程在 `/etc/rc.d/init.d/` 目录下都有一个脚本，该脚本接受一个参数，可以是 `start`、`stop` 和 `restart`。你可以通过以下命令手动执行这些脚本。

例如：

- 手动启动 Linux 下的 `httpd` Web 服务器。

```bash
[root@deep /]# /etc/rc.d/init.d/httpd start
Starting httpd: [ OK ]
```

- 手动停止 Linux 下的 `httpd` Web 服务器。

```bash
[root@deep /]# /etc/rc.d/init.d/httpd stop
Shutting down http: [ OK ]
```

- 手动重启 Linux 下的 `httpd` Web 服务器。

```bash
[root@deep /]# /etc/rc.d/init.d/httpd restart
Shutting down http: [ OK ]
Starting httpd: [ OK ]
```

检查你的 `/etc/rc.d/init.d/` 目录中可用的服务，并使用 `start` | `stop` | `restart` 命令来操作。

## 服务器安装后必须卸载的软件

Red Hat Linux 在系统上默认安装其他预设程序，且在安装过程中不提供卸载的选择。因此，在安装服务器后，你必须卸载系统上的以下软件：

| `pump` | `kernel-pcmcia-cs` | `setserial` | `redhat-release` |
|---|---|---|---|
| `mt-st` | `linuxconf` | `kudzu` | `gd` |
| `eject` | `getty_ps` | `raidtools` | `pciutils` |
| `mailcap` | `setconsole` | `gnupg` | `rmt` |
| `apmd` | `isapnptools` | `redhat-logos` | |

使用 RPM 命令按如下方式卸载它们。

- 卸载软件的命令是：

```bash
[root@deep /]# rpm -e <softwarenames>
```

其中 `<softwarename>` 是你想要卸载的软件名称，例如 `foo`。

像 `apmd`、`kudzu` 和 `sendmail` 这样的程序是作为进程运行的守护程序。在从系统中卸载它们之前，最好先停止这些进程。

- 要停止这些进程，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/apmd stop
[root@deep /]# /etc/rc.d/init.d/sendmail stop
[root@deep /]# /etc/rc.d/init.d/kudzu stop
```

现在你可以安全地卸载它们以及所有其他软件包，如下所示：

## 步骤 1

移除 Red Hat Linux 版本 6.1（Cartman）的指定软件包。

```bash
[root@deep /]# rpm -e --nodeps pump mt-st eject mailcap apmd kernel-pcmcia-cs linuxconf getty_ps setconsole isapnptools setserial kudzu raidtools gnupg redhat-logos redhat-release gd pciutils rmt
```

移除 Red Hat Linux 版本 6.2（Zoot）的指定软件包。

```bash
[root@deep /]# rpm -e --nodeps pump mt-st eject mailcap apmd kernel-pcmcia-cs linuxconf getty_ps isapnptools setserial kudzu raidtools gnupg redhat-logos redhat-release gd pciutils rmt
```

## 步骤 2

手动移除 `linux.conf-installed` 文件。

```bash
[root@deep /]# rm -f /etc/conf.linuxconf-installed
```

**注意：** 这是与 `linuxconf` 软件相关的配置文件，必须手动移除。

程序 `hdparm` 是 IDE 硬盘所需的，但 SCSI 硬盘不需要。如果你的系统上有 IDE 硬盘，则必须保留此程序（`hdparm`），但如果没有 IDE 硬盘，则可以安全地将其从系统中移除。

- 要从系统中移除 `hdparm`，请使用以下命令：

```bash
[root@deep /]# rpm -e hdparm
```

使用 `kbdconfig`、`mouseconfig`、`timeconfig`、`authconfig`、`ntsysv` 和 `setuptool` 这些程序来设置你的键盘语言和类型、鼠标类型、默认时区、NIS 和 shadow 密码、`etc/rc.d` 目录中的众多符号链接，以及允许你访问所有这些功能的文本模式菜单工具。在 Linux 服务器安装阶段完成这些配置后，很少会需要再次更改它们。因此，你可以卸载它们，如果将来需要再次通过测试模式菜单更改键盘、鼠标、默认时间等，只需从原始 CD-ROM 使用 RPM 安装该程序即可。

- 要从系统中移除上述所有程序，请使用以下命令：

```bash
[root@deep /]# rpm -e kbdconfig mouseconfig timeconfig authconfig ntsysv setuptool
```

即使你不打算在 Linux 系统上安装邮件服务器，`Sendmail` 程序在服务器上始终是必需的，因为系统上安装的不同软件服务可能会向 root 用户发送潜在消息。

Sendmail 是一个邮件传输代理（MTA）程序，用于从一台机器向另一台机器发送邮件。它可以以不同方式配置；它可以作为内部投递邮件系统服务于邮件中心服务器，也可以配置为网络中所有 Sendmail 机器的中心邮件中心服务器。因此，根据你对 Sendmail 的用途，必须将其配置为响应你的特定需求。因此，你必须卸载 Sendmail，并参阅本书中有关 Sendmail 配置和安装的部分。

## 服务器安装后必须卸载的程序说明

下面是程序列表及其用途的简要说明。为了获得更好的安全性并在服务器上腾出空间，我们必须卸载它们。有关更多信息和其功能及用途的说明，请参阅你的 Red Hat 手册或安装软件包并执行 `rpm -qi foo` 命令来查询和获取更多程序描述，然后再将其卸载。

**[所有版本]**

`Pump` DHCP 软件包允许网络中的单个无盘客户端从其网络服务器获取自己的 IP 网络配置信息。**[不必要]**

**[所有版本]**

`mt`（用于磁带驱动器）和 `st`（用于 SCSI 磁带设备）磁带驱动管理程序可以控制倒带、弹出、跳过文件、块等。**[仅当此服务器上有磁带备份时才必要]**

**[所有版本]**

`eject` 软件包包含一个 `eject` 程序，允许用户通过软件控制弹出可移动介质（通常是 CD-ROM、软盘、Iomega Jaz 或 Zip 盘）。**[仅当此服务器上有磁带备份时才必要]**

**[所有版本]**

Metamail 是一个使用 `mailcap` 文件来确定如何显示非文本或多媒体材料的程序。**[不必要]**

**[所有版本]**

`apmd` 软件包，即高级电源管理守护程序工具，可以监视你的笔记本电脑电池并在电池电量低时警告所有用户。**[对服务器不必要]**

**[所有版本]**

`kernel-pcmcia-cs` 软件包适用于支持使用 PCMCIA 卡进行扩展的笔记本电脑（和一些非笔记本电脑）。**[对服务器不必要]**

**[所有版本]**

`linuxconf` 软件包是一个系统配置工具。**[不必要，存在缺陷的程序]**

**[所有版本]**

`getty_ps` 软件包包含用于在系统上的控制台或终端上接受登录的程序。**[不必要]**

**[版本 6.1]**

`setconsole` 软件包是一个基本系统工具，用于设置 `/etc/inittab`、`dev/sys tty` 和 `/dev/console` 文件以处理新控制台。**[不必要]**

**[所有版本]**

`isapnp tools` 软件包包含用于配置 ISA 即插即用（PnP）卡/板的工具。**[不必要]**

- 版权所有 1999 - 2000 Gerhard Mourani，Open Network Architecture® 和 OpenDocs Publishing
- `setserial` 软件包是一个基本系统工具，用于显示或设置串行端口信息。**[不必要]**
- `kudzu` 软件包是一个在系统启动时运行的硬件探测工具，用于确定系统中添加或移除了哪些硬件。**[不必要]**
- `raidtools` 软件包包含你在 Linux 系统上设置和维护软件 RAID 设备所需的工具。**[取决于你是否使用 Raid]**
- `GnuPG` 软件包是一种用于安全通信和数据存储的工具。它是 PGP 软件的替代品。它还可用于加密数据和创建数字签名。**[我们将在本书稍后编译它]**
- `redhat-logos` 软件包包含 Red Hat“Shadow Man”徽标和 RPM 徽标的文件。**[在服务器上不必要]**
- `redhat-release` 软件包包含 Red Hat Linux 发布文件。**[不必要]**
- `gd` 软件包允许你的代码快速绘制图像并将结果输出为 `.gif` 文件。**[不必要]**
- `pciutils` 软件包包含用于检查和设置连接到 PCI 总线的设备的各种工具。**[我们使用其他方法]**
- `rmt` 工具提供远程网络访问以进行备份。**[安全风险，因为 `rmt` 依赖于 `rsh` 才能工作]**

## 服务器安装后必须安装的软件

为了能够在服务器上编译程序，你必须安装以下 RPM 软件包。安装的这一部分非常重要，需要你安装下面描述的所有相关软件包。这些软件在你的 Red Hat 第 1 张 CD-ROM 的 `RedHat/RPMS` 目录下，代表了 Linux 上编译和安装程序所需的基本必要软件。

## 步骤 1

首先，我们挂载 CD-ROM 驱动器并转到 CD-ROM 的 `RPMS` 子目录。

- 要挂载 CD-ROM 驱动器并转到 RPM 目录，请使用以下命令：

```bash
[root@deep /]# mount /dev/cdrom /mnt/cdrom/
[root@deep /]# cd /mnt/cdrom/RedHat/RPMS/
```

这是我们能够在 Linux 系统上编译和安装程序所需的软件包。请记住，这是允许你编译大多数适用于 Linux 的 tarball 的最低软件包。Red Hat CD-ROM 上还有其他编译器软件包，因此如果在编译特定软件期间收到错误消息，请验证你要安装的 tarball 程序随附的 README 文件。

### 版本 6.1

- `autoconf-2.13-5.noarch.rpm`
- `m4-1.4-12.i386.rpm`

### 版本 6.2

- `autoconf-2.13-5.noarch.rpm`
- `m4-1.4-12.i386.rpm`

| 版本 6.1 | 版本 6.2 |
|---|---|
| `automake-1.4-5.noarch.rpm` | `automake-1.4-6.noarch.rpm` |
| `dev86-0.14.9-1.i386.rpm` | `dev86-0.15.0-2.i386.rpm` |
| `bison-1.28-1.i386.rpm` | `bison-1.28-2.i386.rpm` |
| `byacc-1.9-11.i386.rpm` | `byacc-1.9-12.i386.rpm` |
| `cdecl-2.5-9.i386.rpm` | `cdecl-2.5-10.i386.rpm` |
| `cpp-1.1.2-24.i386.rpm` | `cpp-1.1.2-30.i386.rpm` |
| `cproto-4.6-2.i386.rpm` | `cproto-4.6-3.i386.rpm` |
| `ctags-3.2-1.i386.rpm` | `ctags-3.4-1.i386.rpm` |



| `egcs-1.1.2-24.i386.rpm` | `egcs-1.1.2-30.i386.rpm` |
|---|---|
| `ElectricFence-2.1-1.i386.rpm` | `ElectricFence-2.1-3.i386.rpm` |
| `flex-2.5.4a-7.i386.rpm` | `flex-2.5.4a-9.i386.rpm` |
| `gdb-4.18-4.i386.rpm` | `gdb-4.18-11.i386.rpm` |
| `kernel-headers-2.2.12-20.i386.rpm` | `kernel-headers-2.2.14-5.0.i386.rpm` |
| `glibc-devel-2.1.2-11.i386.rpm` | `glibc-devel-2.1.3-15.i386.rpm` |
| `make-3.77-6.i386.rpm` | `make-3.78.1-4.i386.rpm` |
| `patch-2.5-9.i386.rpm` | `patch-2.5-10.i386.rpm` |

**注意：**如果你不想在 RPM 安装期间收到依赖错误信息，最好将上述所有软件一起安装。

## 步骤 2

用一个 RPM 命令安装所有需要的软件。

- 将所有软件一起安装的 RPM 命令是：

  ` [root@deep RPMS]# rpm -Uvh autoconf-2.13-5.noarch.rpm m4-1.4-12.i386.rpm automake-1.4-5.noarch.rpm dev86-0.14.9-1.i386.rpm bison-1.28-1.i386.rpm byacc-1.9-11.i386.rpm cdecl-2.5-9.i386.rpm cpp-1.1.2-24.i386.rpm cproto-4.6-2.i386.rpm ctags-3.2-1.i386.rpm egcs-1.1.2-24.i386.rpm ElectricFence-2.1-1.i386.rpm flex-2.5.4a-7.i386.rpm gdb-4.18-4.i386.rpm kernel-headers-2.2.12-20.i386.rpm glibc-devel-2.1.2-11.i386.rpm make-3.77-6.i386.rpm patch-2.5-9.i386.rpm`

| | |
|---|---|
| `autoconf` | ############################################### |
| `m4` | ############################################### |
| `automake` | ############################################### |
| `dev86` | ############################################### |
| `bison` | ############################################### |
| `byacc` | ############################################### |
| `cdecl` | ############################################### |
| `cpp` | ############################################### |
| `cproto` | ############################################### |
| `ctags` | ############################################### |
| `egcs` | ############################################### |
| `ElectricFence` | ############################################### |
| `flex` | ############################################### |
| `gdb` | ############################################### |
| `kernel-headers` | ############################################### |
| `glibc-devel` | ############################################### |
| `make` | ############################################### |
| `patch` | ############################################### |

用一个 RPM 命令安装所有需要的软件。

- 将所有软件一起安装的 RPM 命令是：

  ` [root@deep RPMS]# rpm -Uvh autoconf-2.13-5.noarch.rpm m4-1.4-12.i386.rpm automake-1.4-6.noarch.rpm dev86-0.15.0-2.i386.rpm bison-1.28-2.i386.rpm byacc-1.9-12.i386.rpm cdecl-2.5-10.i386.rpm cpp-1.1.2-30.i386.rpm cproto-4.6-3.i386.rpm ctags-3.4-1.i386.rpm egcs-1.1.2-30.i386.rpm ElectricFence-2.1-3/magento.i386.rpm flex-2.5.4a-9.i386.rpm gdb-4.18-11.i386.rpm kernel-headers-2.2.14-5.0.i386.rpm glibc-devel-2.1.3-15.i386.rpm make-3.78.1-4.i386.rpm patch-2.5-10.i386.rpm`

| | |
|---|---|
| `autoconf` | ################################################## |
| `m4` | ################################################## |
| `automake` | ################################################## |
| `dev86` | ################################################## |
| `bison` | ################################################## |
| `byacc` | ################################################## |
| `cdecl` | ################################################## |
| `cpp` | ################################################## |
| `cproto` | ################################################## |
| `ctags` | ################################################## |
| `egcs` | ################################################## |
| `ElectricFence` | ################################################## |
| `flex` | ################################################## |
| `gdb` | ################################################## |
| `kernel-headers` | ################################################## |
| `glibc-devel` | ################################################## |
| `make` | ################################################## |
| `patch` | ################################################## |

## 步骤 3

你必须退出并重新登录，所有更改才能生效。

- 要从控制台退出，使用命令：

  `[root@deep /]# exit`

在服务器上安装并编译完所有需要的程序后，最好将上述所有锋利工具（编译器等）从系统中移除，除非有需要保留的理由。原因之一是，如果攻击者入侵了你的服务器，他或她将无法编译或修改二进制程序。此外，这还可以释放大量空间，并有助于改进对服务器上文件的定期完整性检查扫描。

当你运行一台服务器时，你会赋予它特定的任务去完成。你永远不要把所有要提供的服务都放在一台机器上，否则你会损失速度（可用资源除以服务器上运行的进程数），并降低安全性（如果很多服务在同一台机器上运行，一旦攻击者访问了这台服务器，他就可以直接攻击所有其他可用的服务）。

让不同的服务器执行不同的任务将简化管理和维护（你知道每台服务器应该做什么任务，哪些服务应该可用，哪些端口对客户端开放、哪些关闭，你知道日志文件中应该出现什么内容，等等），并让你对每台服务器有更多的控制和灵活性（专门用于邮件、网页、数据库、开发、备份等的服务器）。所以，例如，拥有一台专门用于开发和测试的服务器，就可以让你不必每次在服务器上编译安装新软件时都安装编译器程序，然后再被迫卸载编译器或其他锋利工具。

---

Copyright 1999 - 2000 Gerhard Mourani, Open Network Architecture ® and OpenDocs Publishing

# 服务器上已安装的程序

## 步骤 1

由于我们选择自定义 Linux 系统的安装，以下是完整的 Linux 服务器安装后必须拥有的所有已安装程序列表。此列表必须与`/tmp`目录中的`install.log`文件完全匹配，否则可能会遇到问题。不要忘记安装“服务器安装后必须安装的软件”中列出的所有程序，以便能够在你的服务器上正确编译。

- Installing `setup`.
- Installing `filesystem`.
- Installing `basesystem`.
- Installing `ldconfig`.
- Installing `glibc`.
- Installing `shadow-utils`.
- Installing `mktemp`.
- Installing `termcap`.
- Installing `libtermcap`.
- Installing `bash`.
- Installing `MAKEDEV`.
- Installing `SysVinit`.
- Installing `XFree86-Mach64`.
- Installing `chkconfig`.
- Installing `apmd`.
- Installing `ncurses`.
- Installing `info`.
- Installing `fileutils`.
- Installing `grep`.
- Installing `ash`.
- Installing `at`.
- Installing `authconfig`.
- Installing `bc`.
- Installing `bdflush`.
- Installing `binutils`.
- Installing `bzip2`.
- Installing `sed`.
- Installing `console-tools`.
- Installing `e2fsprogs`.
- Installing `rmt`.
- Installing `cpio`.
- Installing `cracklib`.
- Installing `cracklib-dicts`.
- Installing `crontabs`.
- Installing `textutils`.
- Installing `dev`.
- Installing `diffutils`.
- Installing `dump`.
- Installing `ed`.
- Installing `eject`.
- Installing `etcskel`.
- Installing `file`.
- Installing `findutils`.
- Installing `gawk`.
- Installing `gd`.
- Installing `gdbm`.
- Installing `getty_ps`.
- Installing `glib`.
- Installing `gmp`.
- Installing `gnupg`.
- Installing `gzip`.
- Installing `hdparm`.
- Installing `initscripts`.
- Installing `ipchains`.
- Installing `isapnptools`.
- Installing `kbdconfig`.
- Installing `kernel`.
- Installing `kernel-pcmcia-cs`.
- Installing `kudzu`.
- Installing `ld.so`.
- Installing `less`.
- Installing `libc`.
- Installing `libstdc++`.
- Installing `lilo`.
- Installing `pwdb`.
- Installing `pam`.
- Installing `sh-utils`.
- Installing `redhat-release`.
- Installing `linuxconf`.
- Installing `logrotate`.
- Installing `losetup`.
- Installing `lsof`.
- Installing `mailcap`.
- Installing `mailx`.
- Installing `man`.
- Installing `mingetty`.
- Installing `mkbootdisk`.
- Installing `mkinitrd`.
- Installing `modutils`.
- Installing `mount`.
- Installing `mouseconfig`.
- Installing `mt-st`.
- Installing `ncompress`.
- Installing `net-tools`.
- Installing `netkit-base`.
- Installing `newt`.
- Installing `ntsysv`.
- Installing `passwd`.
- Installing `pciutils`.
- Installing `perl`.
- Installing `procmail`.
- Installing `procps`.
- Installing `psmisc`.
- Installing `pump`.
- Installing `python`.
- Installing `quota`.
- Installing `raidtools`.
- Installing `readline`.
- Installing `redhat-logos`.
- Installing `rootfiles`.
- Installing `sendmail`.
- Installing `setconsole`.
- Installing `setserial`.
- Installing `setuptool`.
- Installing `shapecfg`.
- Installing `slang`.
- Installing `slocate`.
- Installing `stat`.
- Installing `sysklogd`.
- Installing `tar`.
- Installing `tcp_wrappers`.
- Installing `tcpdump`.
- Installing `tcsh`.
- Installing `time`.
- Installing `timeconfig`.
- Installing `timed`.
- Installing `tmpwatch`.
- Installing `traceroute`.
- Installing `utempter`.
- Installing `util-linux`.
- Installing `vim-common`.
- Installing `vim-minimal`.
- Installing `vixie-cron`.
- Installing `which`.
- Installing `zlib`.

## Linux 安装 第 2 章

- 安装`gpm`。
- 安装`groff`。
- 安装`rpm`。
- 安装`sash`。
- 安装`setup`。
- 安装`filesystem`。
- 安装`basesystem`。
- 安装`ldconfig`。
- 安装`glibc`。
- 安装`shadow-utils`。
- 安装`mktemp`。
- 安装`termcap`。
- 安装`libtermcap`。
- 安装`bash`。
- 安装`MAKEDEV`。
- 安装`SysVinit`。
- 安装`XFree86-Mach64`。
- 安装`anacron`。
- 安装`chkconfig`。
- 安装`apmd`。
- 安装`ncurses`。
- 安装`info`。
- 安装`fileutils`。
- 安装`grep`。
- 安装`ash`。



- 安装`at`。
- 安装`authconfig`。
- 安装`bc`。
- 安装`bdflush`。
- 安装`binutils`。
- 安装`bzip2`。
- 安装`sed`。
- 安装`console-tools`。
- 安装`e2fsprogs`。
- 安装`rmt`。
- 安装`cpio`。
- 安装`cracklib`。
- 安装`cracklib-dicts`。
- 安装`crontabs`。
- 安装`textutils`。
- 安装`dev`。
- 安装`diffutils`。
- 安装`dump`。
- 安装`ed`。
- 安装`eject`。
- 安装`etcskel`。
- 安装`file`。
- 安装`findutils`。
- 安装`gawk`。
- 安装`gd`。
- 安装`gdbm`。
- 安装`getty_ps`。
- 安装`glib`。
- 安装`gmp`。
- 安装`gnupg`。
- 安装`gpm`。
- 安装`groff`。
- 安装`gzip`。
- 安装`hdparm`。
- 安装`inetd`。
- 安装`initscripts`。
- 安装`ipchains`。
- 安装`iputils`。
- 安装`isapnptools`。
- 安装`kbdconfig`。
- 安装`kernel`。
- 安装`kernel-pcmcia-cs`。
- 安装`kernel-utils`。
- 安装`kudzu`。
- 安装`ld.so`。
- 安装`less`。
- 安装`libc`。
- 安装`libstdc++`。
- 安装`lilo`。
- 安装`pwdb`。
- 安装`pam`。
- 安装`sh-utils`。
- 安装`redhat-release`。
- 安装`linuxconf`。
- 安装`logrotate`。
- 安装`losetup`。
- 安装`lsof`。
- 安装`mailcap`。
- 安装`mailx`。
- 安装`man`。
- 安装`mingetty`。
- 安装`mkbootdisk`。
- 安装`mkinitrd`。
- 安装`modutils`。
- 安装`mount`。
- 安装`mouseconfig`。
- 安装`mt-st`。
- 安装`ncompress`。
- 安装`net-tools`。
- 安装`newt`。
- 安装`ntsysv`。
- 安装`passwd`。
- 安装`pciutils`。
- 安装`perl`。
- 安装`popt`。
- 安装`procmail`。
- 安装`procps`。
- 安装`psmisc`。
- 安装`pump`。
- 安装`quota`。
- 安装`raidtools`。
- 安装`readline`。
- 安装`redhat-logos`。
- 安装`rootfiles`。
- 安装`rpm`。
- 安装`sash`。
- 安装`sendmail`。
- 安装`setserial`。
- 安装`setuptool`。
- 安装`shapecfg`。
- 安装`slang`。
- 安装`slocate`。
- 安装`stat`。
- 安装`sysklogd`。
- 安装`tar`。
- 安装`tcp_wrappers`。
- 安装`tcpdump`。
- 安装`tcsh`。
- 安装`time`。
- 安装`timeconfig`。
- 安装`tmpwatch`。
- 安装`traceroute`。
- 安装`utempter`。
- 安装`util-linux`。
- 安装`vim-common`。
- 安装`vim-minimal`。
- 安装`vixie-cron`。
- 安装`which`。
- 安装`zlib`。

## 步骤 2

在卸载了 Linux 服务器安装后必须卸载的所有软件之后（参见服务器安装后必须卸载的软件），并添加了能够在服务器上编译程序所必需的 RPM 软件包之后（参见服务器安装后必须安装的软件），我们必须再次验证所有已安装的 RPM 程序列表，但这次使用以下命令：

- 要验证系统上所有已安装的 RPM 软件包列表，请使用以下命令：

  ```bash
  [root@deep /]# rpm -qa > installed_rpm
  ```

`-qa` 选项将查询系统上所有已安装的 RPM 软件包，而特殊字符`>`将把输出重定向到名为`installed_rpm`的文件中。

`installed_rpm`文件的内容必须完全如下所示：

```text
setup-2.0.5-1			findutils-4.1-32			netkit-base-0.10-37
filesystem-1.3.5-1			gawk-3.0.4-1				newt-0.50-13
basesystem-6.0-4			cdecl-2.5-9				passwd-0.63-1
ldconfig-1.9.5-15			gdbm-1.8.0-2				perl-5.00503-6
glibc-2.1.2-11			-autoconf-2.13-5				flex-2.5.4a-7
shadow-utils-19990827-2		glib-1.2.5-1				procps-2.0.4-2
mktemp-1.5-1				gmp-2.0.2-10				psmisc-18-3
termcap-9.12.6-15			cpp-1.1.2-24				python-1.5.2-7
libtermcap-2.0.8-18			gpm-1.17.9-3				quota-1.66-8
bash-1.14.7-16				groff-1.11a-9				gdb-4.18-4
MAKEDEV-2.5-2				gzip-1.2.4-14				readline-2.2.1-5
SysVinit-2.77-2				initscripts-4.48-1			glibc-devel-2.1.2-11
chkconfig-1.0.7-2			ipchains-1.3.9-3			rootfiles-5.2-5
ncurses-4.2-25				cproto-4.6-2				rpm-3.0.3-2
info-3.12h-2				ElectricFence-2.1-1			sash-3.3-1
fileutils-4.0-8				kernel-2.2.12-20				make-3.77-6
grep-2.3-2				patch-2.5-9				shapecfg-2.2.12-2
ash-0.2-18				ld.so-1.9.5-11				slang-1.2.2-4
at-3.1.7-11				less-340-1				slocate-2.0-3
m4-1.4-12				libc-5.3.12-31				stat-1.5-11
bdflush-1.5-10				libstdc++-2.9.0-24			sysklogd-1.3.31-12
binutils-2.9.1.0.23-6			lilo-0.21-10				tar-1.13.11-1
bzip2-0.9.5c-1				pwdb-0.60-1				tcp_wrappers-7.6-9
sed-3.02-4				pam-0.68-7				tcpdump-3.4-16
console-tools-19990302-17		sh-utils-2.0-1				tcsh-6.08.00-6
e2fsprogs-1.15-3			automake-1.4-5				time-1.7-9
byacc-1.9-11				logrotate-3.3-1				timed-0.10-23
cpio-2.4.2-13				losetup-2.9u-4				tmpwatch-2.0-1
cracklib-2.7-5				lsof-4.45-1				traceroute-1.4a5-16
cracklib-dicts-2.7-5			mailx-8.1.1-9				utempter-0.5.1-2
crontabs-1.7-7				man-1.5g-6				util-linux-2.9w-24
textutils-2.0-2				mingetty-0.9.4-10			vim-common-5.4-2
dev-2.7.10-2				mkbootdisk-1.2.2-1			vim-minimal-5.4-2
diffutils-2.7-16				mkinitrd-2.3-1				vixie-cron-3.0.1-39
dump-0.4b4-11				modutils-2.1.121-14			which-2.8-1
ed-0.2-12				mount-2.9u-4				zlib-1.1.3-5
bison-1.28-1				ctags-3.2-1				dev86-0.14.9-1
etcskel-2.0-1				ncompress-4.2.4-14			egcs-1.1.2-24
file-3.27-3				net-tools-1.53-1			kernel-headers-2.2.12-20
```

`installed_rpm`文件的内容必须完全如下所示：

```text
setup-2.1.8-1				findutils-4.1-34			flex-2.5.4a-9
filesystem-1.3.5-1			gawk-3.0.4-2				ncompress-4.2.4-15
basesystem-6.0-4			patch-2.5-10				net-tools-1.54-4
ldconfig-1.9.5-16
glibc-2.1.3-15
shadow-utils-19990827-10
mktemp-1.5-2
termcap-10.2.7-9
libtermcap-2.0.8-20
bash-1.14.7-22
MAKEDEV-2.5.2-1
SysVinit-2.78-5
anacron-2.1-6
chkconfig-1.1.2-1
m4-1.4-12
ncurses-5.0-11
info-4.0-5
fileutils-4.0-21
grep-2.4-3
ash-0.2-20
at-3.1.7-14
byacc-1.9-12
bc-1.05a-5
bdflush-1.5-11
binutils-2.9.5.0.22-6
bzip2-0.9.5d-2
sed-3.02-6
console-tools-19990829-10
e2fsprogs-1.18-5
cpio-2.4.2-16
cracklib-2.7-5
cracklib-dicts-2.7-5
crontabs-1.7-7
textutils-2.0a-2
dev-2.7.18-3
diffutils-2.7-17
dump-0.4b15-1
ed-0.2-13
cdecl-2.5-10
etcskel-2.3-1
file-3.28-2
gdbm-1.8.0irms.
```

三连排版能力令人叹为观止，它能在处理`rpm -qa > installed_rpm`这类命令时保持格式完整，并在代码块中精准保留每一行软件包名称。对于 **Red Hat Linux version 6.1 (Cartman)** 这类版本标注，它也能正确处理斜体符号的嵌套。

`installed_rpm`文件的内容必须完全如下所示：



```text
ldconfig-1.9.5-16
glibc-2.1.3-15
shadow-utils-19990827-10
mktemp-1.5-2
termcap-10.2.7-9
libtermcap-2.0.8-20
bash-1.14.7-22
MAKEDEV-2.5.2-1
SysVinit-2.78-5
anacron-2.1-6
chkconfig-1.1.2-1
m4-1.4-12
ncurses-5.0-11
info-4.0-5
fileutils-4.0-21
grep-2.4-3
ash-0.2-20
at-3.1.7-14
byacc-1.9-12
bc-1.05a-5
bdflush-1.5-11
binutils-2.9.5.0.22-6
bzip2-0.9.5d-2
sed-3.02-6
console-tools-19990829-10
e2fsprogs-1.18-5
cpio-2.4.2-16
cracklib-2.7-5
cracklib-dicts-2.7-5
crontabs-1.7-7
textutils-2.0a-2
dev-2.7.18-3
diffutils-2.7-17
dump-0.4b15-1
ed-0.2-13
cdecl-2.5-10
etcskel-2.3-1
file-3.28-2
gdbm-1.8.0-3
bison-1.28-2
glib-1.2.6-3
gmp-2.0.2-13
autoconf-2.13-5
gpm-1.18.1-7
groff-1.15-8
gzip-1.2.4a-2
inetd-0.16-4
initscripts-5.00-1
ipchains-1.3.9-5
iputils-20000121-2
cpp-1.1.2-30
cproto-4.6-3
kernel-2.2.14-5.0
ctags-3.4-1
kernel-utils-2.2.14-5.0
ElectricFence-2.1-3
ld.so-1.9.5-13
less-346-2
libc-5.3.12-31
libstdc++-2.9.0-30
lilo-0.21-15
pwdb-0.61-0
pam-0.72-6
sh-utils-2.0-5
automake-1.4-6
logrotate-3.3.2-1
losetup-2.10f-1
lsof-4.47-2
mailx-8.1.1-10
man-1.5h1-1
mingetty-0.9.4-11
mkbootdisk-1.2.5-3
mkinitrd-2.4.1-2
modutils-2.3.9-6
mount-2.10f-1
newt-0.50.8-2
passwd-0.64.1-1
perl-5.00503-10
popt-1.5-0.48
procmail-3.14-2
procps-2.0.6-5
psmisc-19-2
quota-2.00pre3-2
gdb-4.18-11
readline-2.2.1-6
make-3.78.1-4
rootfiles-5.2-5
rpm-3.0.4-0.48
sash-3.4-2
shapecfg-2.2.12-2
slang-1.2.2-5
slocate-2.1-2
stat-1.5-12
sysklogd-1.3.31-16
tar-1.13.17-3
tcp_wrappers-7.6-10
tcpdump-3.4-19
tcsh-6.09-4
time-1.7-9
tmpwatch-2.2-1
traceroute-1.4a5-18
utempter-0.5.2-2
util-linux-2.10f-7
vim-common-5.6-1
vim-minimal-5.6-1
vixie-cron-3.0.1-40
which-2.9-2
zlib-1.1.3-6
dev86-0.15.0-2
egcs-1.1.2-30
kernel-headers-2.2.14-5.0
glibc-devel-2.1.3-15
```

这一步是必要的，以确保我们没有忘记移除某些不必要的 RPM，或者遗漏了一些允许我们在系统上编译程序的重要软件包。如果结果看起来与我们上面的`installed_rpm`文件一致，那么我们就可以开始使用新的 Linux 服务器了。

## 为终端添加色彩

为终端添加一些色彩可以帮助你区分文件夹、文件、归档文件、设备、符号链接和可执行文件。我的看法是，色彩有助于减少错误并在系统上实现快速导航。需要注意的是，这个技巧仅对`Red Hat Linux version 6.1 (Cartman)`及更早版本是必需的，因为新的`Red Hat Linux version 6.2 (Zoot)`现在默认启用并包含此功能。

编辑`profile`文件（`vi /etc/profile`）并添加以下行：

```bash
# Enable Colour ls
eval `dircolors /etc/DIR_COLORS -b`
export LS_OPTIONS='-s -F -T 0 --color=yes'
```

编辑`bashrc`文件（`vi /etc/bashrc`）并添加以下行：

```bash
alias ls='ls --color=auto'
```

然后重新登录并登出；执行此操作后，新的`COLORS`环境变量将被设置，您的系统将能够识别该变量。

**注意：** 请记住，此功能仅在 Red Hat Linux 6.1 及更早版本中需要。

## 更新至最新软件

保持并更新所有软件（尤其是网络软件）到最新版本。请查看 Red Hat Linux 发行版的勘误页面，网址为 <http://www.redhat.com/corp/support/errata/index.html>。勘误页面可能是解决 Red Hat Linux 90% 常见问题的最佳资源。此外，在 Red Hat 收到通知后 24 小时内，安全漏洞的解决方案通常会出现在勘误页面上。您应始终首先查看此处。

此时必须为您的 Red Hat Linux 服务器更新的软件有：

```text
groff-1_15-1_i386.rpm
sysklogd-1_3_31-14_i386.rpm
initscripts-4_70-1_i386.rpm
e2fsprogs-1.17-1.i386.rpm
pam-0_68-10_i386.rpm
gpm-1.19.1-1.i386.rpm
Linux kernel 2.2.14 (linux-2_2_14_tar.gz)
```

```text
gpm-1.19.1-1.i386.rpm
```

**注意：** Linux 内核是最重要的，必须始终更新。有关为您的特定系统构建自定义内核的更多信息，请参阅下文。

- 您可以使用以下命令验证上述 RPM 软件是否已安装在您的系统上，然后再进行更新：`[root@deep /]# rpm -q <softwarename>`

其中`<softwarename>`是您要验证的软件名称，如`groff`、`sysklogd`等。

# 第二部分 安全与优化相关参考

在本部分中：

- 通用系统安全
- 通用系统优化
- 配置和构建内核

# 第 3 章 通用系统安全

## 本章内容

- Linux 通用安全

## Linux 通用安全

### 概述

安全的 Linux 服务器取决于管理员如何进行配置。一旦我们通过移除不必要的 RPM 服务消除了潜在的安全风险，我们就可以开始保护服务器上现有的服务和软件。在本章中，我们将讨论一些更通用、更基本的安全防护技术。以下是可以帮助防止来自外部和内部攻击的功能列表。

### BIOS 安全设置启动密码

建议禁止从软盘驱动器启动，并为 BIOS 功能设置密码。您可以查阅 BIOS 手册，或在下次启动系统时仔细查看以了解如何操作。禁止从软盘驱动器启动并能够为 BIOS 功能设置密码将提高系统的安全性。这将阻止不受欢迎的人试图使用特殊启动盘启动您的 Linux 系统，并保护您免受试图更改 BIOS 功能的人的侵害，例如允许从软盘驱动器启动或无需密码提示即可启动服务器。

### 安全策略

需要指出的是，如果您尚未决定需要保护什么以及需要防范谁，就无法实施安全措施。您需要一份安全策略——一份您认为可接受和不可接受的事项清单，以此作为任何安全决策的基础。该策略还应确定您对安全违规的响应。在编制安全策略时应考虑什么，将完全取决于您对安全的定义。以下问题应提供一些通用指导：

- 您如何对机密或敏感信息进行分类？
- 系统是否包含机密或敏感信息？
- 您到底要防范谁？
- 远程用户是否真的需要访问您的系统？
- 密码或加密是否提供了足够的保护？
- 您是否需要访问互联网？
- 您希望允许从互联网对您的系统进行多少访问？
- 如果您发现安全漏洞，将采取什么行动？

这个列表很短，您的策略在完成之前可能会涵盖更多内容。任何安全策略都必须基于一定程度的偏执；决定您对组织内外人员的信任程度。然而，该策略必须在允许用户合理访问其工作所需信息和完全禁止访问您的信息之间取得平衡。这条线划在哪里将决定您的策略。

### 选择正确的密码

我们 Linux 通用安全之旅的起点是密码。许多人在计算机上保存有价值的信息和文件，而阻止他人查看这些信息的唯一东西就是一个称为密码的八字符字符串。与普遍看法相反，不可破解的密码并不存在。只要有时间和资源，所有密码都可以通过社会工程学或暴力破解来猜出。

服务器密码和其他访问方法的社会工程学仍然是最简单和最常见的获取账户和服务器访问权限的方式。通常，像在公司内冒充上级或高管，并在正确的时间对正确的人大喊大叫这样简单的事情，就能产生极好的效果。

在您的系统上每周运行一次密码破解程序是个好主意。这有助于找到并替换容易被猜到或弱的密码。此外，应存在密码检查机制，以在首次选择密码或更改旧密码时拒绝弱密码。纯字典单词的字符串，或全部使用同一大小写，或不包含数字或特殊字符的字符串不应被接受为新密码。

我们建议遵循以下规则以使密码有效：

- 它们应至少有六个字符长度，最好有八个字符，包括至少一个数字或特殊字符。
- 它们不能是平凡的；平凡密码是指容易猜到的密码，通常基于用户的姓名、家庭、职业或其他个人特征。
- 它们应有一个有效期，要求在特定时间段内选择新密码。
- 在有限次数的连续错误重试后，它们应被撤销并重置。

### 密码长度

安装 Linux 系统时，默认的最小可接受密码长度为 5。这意味着当新用户被允许访问服务器时，他/她的密码长度至少为 5 个混合的字符字符串、字母、数字、特殊字符等。这还不够，必须是 8。为了防止缺乏安全意识的人或管理员能够只输入 5 个字符作为有价值的密码，请编辑相当重要的`/etc/login.defs`文件，并将值 5 改为 8。

编辑`login.defs`文件（`vi /etc/login.defs`）并修改以下行：

```text
PASS_MIN_LEN    5
改为：
PASS_MIN_LEN    8
```

`login.defs`是登录程序的配置文件。您应该查看或根据您的特定系统对此文件进行更改。这是您设置其他安全策略设置（如密码过期默认值或最小可接受密码长度）的地方。

### root 账户

`root`账户是 Unix 系统上最具特权的账户。`root`账户没有任何安全限制。这意味着系统假设您知道自己在做什么，并且会完全按照您的要求执行——不问任何问题。因此，一个打错的命令就很容易删除关键的系统文件。使用此账户时，尽可能小心很重要。出于安全原因，除非绝对需要 root 访问权限的实例，否则永远不要以`root`身份登录您的服务器。此外，如果您不在服务器上，永远不要登录后保持`root`身份——这非常、非常、非常糟糕。

### 为 root 账户设置登录超时

尽管已有警告，不要在不在服务器上时以`root`身份登录并离开，但管理员仍然保持`root`身份，或在完成工作后忘记注销并离开他们的终端无人看管。解决这个问题的答案是让 bash shell 在闲置一段时间后自动注销。为此，您必须将 Linux 名为`TMOUT`的特殊变量设置为以秒为单位的闲置时间，时间到后自动注销。

编辑您的`profile`文件（`vi /etc/profile`），并在文件中`HISTFILESIZE=`这一行之后的某处添加以下行：

```bash
TMOUT=7200
```

我们为变量`TMOUT=`输入的值以秒为单位，代表 2 小时（60 * 60 = 3600 * 2 = 7200 秒）。需要注意的是，如果您决定将上述行放在`/etc/profile`文件中，那么两小时闲置后自动注销将适用于系统上的所有用户。因此，相反，如果您希望控制哪些用户将自动注销，哪些不自动注销，您可以在他们各自的`.bashrc`文件中设置此变量。

在您的系统上设置此参数后，您必须注销并重新登录（作为 root）才能使更改生效。

### `/etc/exports` 文件

如果您使用 NFS 服务导出文件系统，请务必以尽可能最严格的访问权限配置`/etc/exports`文件。这意味着不使用通配符，不允许 root 写入访问，并在可能的情况下以只读方式挂载。

编辑`exports`文件（`vi /etc/exports`）并添加：

例如：

```text
/dir/to/export host1.mydomain.com(ro,root_squash)

/dir/to/export host2.mydomain.com(ro,root_squash)
```

其中`/dir/to/export`是您要导出的目录，`host#.mydomain.com`是允许登录此目录的机器，`<ro>`选项表示以只读方式挂载，`<root_squash>`选项表示不允许 root 在此目录写入访问。

为了使此更改生效，您需要在终端上运行以下命令：

`[root@deep]# /usr/sbin/exportfs -a`

**注意：** 请注意，在您的系统上提供 NFS 服务可能存在安全风险。就个人而言，我不推荐使用它。

### 禁用控制台程序访问

在一个我们确信控制台是安全的环境中——因为 BIOS 和 LILO 已设置密码，且系统上所有物理电源和重置开关均已禁用——完全禁用普通用户通过控制台等效方式访问关机、重启和停止等程序可能是有益的。

要执行此操作，请运行以下命令：

```bash
[root@deep /]# rm -f /etc/security/console.apps/<servicename>
```

其中`<servicename>`是您希望禁用控制台等效访问的程序名称。但请注意，除非您使用`xdm`，否则不要删除`xserver`文件，否则除了 root 用户外将无人能够启动 X 服务器。（如果您始终使用`xdm`启动 X 服务器，那么只有 root 用户需要启动 X，在这种情况下您可能实际上需要删除`xserver`文件）。

举例如下：

```bash
[root@deep /]# rm -f /etc/security/console.apps/halt
[root@deep /]# rm -f /etc/security/console.apps/poweroff
[root@deep /]# rm -f /etc/security/console.apps/reboot
[root@deep /]# rm -f /etc/security/console.apps/shutdown
[root@deep /]# rm -f /etc/security/console.apps/xserver (if removed, root will be the only user able to start X).
```

这将禁用对程序`halt`、`poweroff`、`reboot`和`shutdown`的控制台等效访问。再次提醒，程序`xserver`仅在您系统上安装了 X 窗口界面时适用。

**注意：** 如果您按照我们的设置安装步骤进行，您的服务器上并未安装 X 窗口界面，上述所有文件将不会出现在`/etc/security`目录中，因此无需关注上述步骤。

## 禁用所有控制台访问

您的系统上默认安装的 Linux-PAM 库允许系统管理员选择应用程序如何认证用户，例如用于控制台访问、程序和文件访问。为了禁用用户的所有这些访问权限，您必须注释掉`/etc/pam.d/`目录中所有引用`pam_console.so`的行。此步骤是上述“禁用控制台程序访问”技巧的延续。

以下脚本将自动为您完成此操作。以`root`身份创建`disabling.sh`脚本文件（`touch disabling.sh`），并在其中添加以下内容：

```sh
#!/bin/sh

cd /etc/pam.d

for i in * ; do
    sed '/^#].*pam_console.so/s/^/#/' < $i > foo && mv foo $i
done
```

使用以下命令使此脚本可执行并运行它：

```bash
[root@deep /]# chmod 700 disabling.sh
[root@deep /]# ./disabling.sh
```

这将注释掉`/etc/pam.d`目录下所有文件中引用`pam_console.so`的行。脚本执行完毕后，您可以将其从系统中删除。

## `/etc/inetd.conf` 文件

### Linux 通用安全：第三章

`Inetd`，也称为“超级服务器”，将根据网络请求加载网络程序。`inetd.conf`文件告知`inetd`监听哪些端口以及为每个端口启动哪个服务器。将您的 Linux 系统接入任何网络后，首先要关注的是您需要提供哪些服务。

您不需要提供的服务应被禁用并卸载，这样您少操一份心，攻击者也少了一个寻找漏洞的地方。查看您的`/etc/inetd.conf`文件，了解您的`inetd`程序正在提供哪些服务。通过注释掉不需要的服务（在行首添加`#`）来禁用它们，然后向您的`inetd`进程发送`SIGHUP`命令以更新到当前的`inetd.conf`文件。

### 步骤 1

将此文件的权限更改为`600`。



```bash
[root@deep /]# chmod 600 /etc/inetd.conf
```

## 步骤 2

确保所有者是`root`。

```bash
[root@deep /]# stat /etc/inetd.conf
```

```text
File: "/etc/inetd.conf"
Size: 2869   Filetype: Regular File
Mode: (0600/-rw-------) Uid: ( 0/ root) Gid: ( 0/ root)
Device: 8,6 Inode: 18219 Links: 1
Access: Wed Sep 22 16:24:16 1999(00000.00:10:44)
Modify: Mon Sep 20 10:22:44 1999(00002.06:12:16)
Change: Mon Sep 20 10:22:44 1999(00002.06:12:16)
```

## 步骤 3

编辑`inetd.conf`文件（`vi /etc/inetd.conf`），并禁用诸如以下的服务：

`ftp`、`telnet`、`shell`、`login`、`exec`、`talk`、`ntalk`、`imap`、`pop-2`、`pop-3`、`finger`、`auth`等，除非您计划使用它。如果关闭服务，风险会大大降低。

```text
# To re-read this file after changes, just do a 'killall -HUP inetd'
#
#echo     stream tcp  nowait root   internal
#echo     dgram  udp  wait   root   internal
#discard  stream tcp  nowait root   internal
#discard  dgram  udp  wait   root   internal
#daytime  stream tcp  nowait root   internal
#daytime  dgram  udp  wait   root   internal
#chargen  stream tcp  nowait root   internal
#chargen  dgram  udp  wait   root   internal
#time     stream tcp  nowait root   internal
#time     dgram  udp  wait   root   internal
#
# These are standard services.
#
#ftp      stream tcp  nowait root   /usr/sbin/tcpd in.ftpd -l -a
#telnet   stream tcp  nowait root   /usr/sbin/tcpd in.telnetd
#
# Shell, login, exec, comsat and talk are BSD protocols.
#
#shell    stream tcp  nowait root   /usr/sbin/tcpd in.rshd
#login    stream tcp  nowait root   /usr/sbin/tcpd in.rlogind
#exec     stream tcp  nowait root   /usr/sbin/tcpd in.rexecd
```

版权所有 1999 - 2000 Gerhard Mourani, Open Network Architecture ® 和 OpenDocs Publishing

```text
#comsat     dgram   udp    wait    root    /usr/sbin/tcpd  in.comsat
#talk       dgram   udp    wait    root    /usr/sbin/tcpd  in.talkd
#ntalk      dgram   udp    wait    root    /usr/sbin/tcpd  in.ntalkd
#dtalk      stream  tcp    wait    nobody  /usr/sbin/tcpd  in.dtalkd
#
# Pop and imap mail services et al
#
#pop-2      stream  tcp    nowait  root    /usr/sbin/tcpd  ipop2d
#pop-3      stream  tcp    nowait  root    /usr/sbin/tcpd  ipop3d
#imap       stream  tcp    nowait  root    /usr/sbin/tcpd  imapd
#
# The Internet UUCP service.
#
#uucp       stream  tcp    nowait  uucp    /usr/sbin/tcpd /usr/lib/uucp/uucico  -l
#
# Tftp service is provided primarily for booting. Most sites
# run this only on machines acting as "boot servers." Do not uncomment
# this unless you *need* it.
#
#tftp       dgram   udp    wait    root    /usr/sbin/tcpd  in.tftpd
#bootps     dgram   udp    wait    root    /usr/sbin/tcpd  bootpd
#
# Finger, systat and netstat give out user information which may be
# valuable to potential "system crackers." Many sites choose to disable
# some or all of these services to improve security.
#
#finger     stream  tcp    nowait  root    /usr/sbin/tcpd  in.fingerd
#cfinger    stream  tcp    nowait  root    /usr/sbin/tcpd  in.cfingerd
#systat     stream  tcp    nowait  guest   /usr/sbin/tcpd  /bin/ps -auwx
#netstat    stream  tcp    nowait  guest   /usr/sbin/tcpd  /bin/netstat  -f inet
#
# Authentication
#
#auth       stream  tcp    nowait  nobody  /usr/sbin/in.identd  in.identd -l -e -o
#
# End of inetd.conf
```

**注意：** 修改您的`inetd.conf`文件后，不要忘记向您的`inetd`进程发送`SIGHUP`信号（`killall -HUP inetd`）。您在选定主机上启用的服务取决于您希望该主机提供的功能。功能可能包括支持选定的网络服务、此计算机上托管的其他服务，或操作系统和应用程序的开发与维护。

```bash
[root@deep /]# killall -HUP inetd
```

## 步骤 4

您可以采取的另一项安全措施是使用`chattr`命令将`"inetd.conf"`文件设置为不可更改。

- 要将文件设置为不可更改，只需执行以下命令：

```bash
[root@deep /]# chattr +i /etc/inetd.conf
```

这将防止对`"inetd.conf"`文件的任何更改（无论是意外还是其他原因）。设置了不可更改属性`"i"`的文件不能被修改、删除或重命名，不能创建指向该文件的链接，也不能向其写入数据。唯一可以设置或清除此属性的人是超级用户`root`。

如果您以后希望修改`inetd.conf`文件，您将需要取消不可更改标志。

## TCP_WRAPPERS

默认情况下，Red Hat Linux 允许所有服务请求。使用`TCP_WRAPPERS`可以使保护服务器免受外部入侵变得比你预期的更加简单和轻松。在`"/etc/hosts.deny"`文件中添加`"ALL: ALL@ALL, PARANOID"`以拒绝所有主机，并在`"/etc/hosts.allow"`文件中明确列出允许访问你机器的可信主机。这是最安全和最佳的配置。

`TCP_WRAPPERS`由两个文件控制，搜索在第一次匹配时停止。

- 当（守护进程，客户端）配对匹配`/etc/hosts.allow`文件中的条目时，将授予访问权限。
- 否则，当（守护进程，客户端）配对匹配`/etc/hosts.deny`文件中的条目时，将拒绝访问。
- 否则，将授予访问权限。

### 步骤 1

编辑`hosts.deny`文件（`vi /etc/hosts.deny`）并添加以下行：

**默认拒绝访问。**

**# 拒绝所有人访问。**

**`ALL: ALL@ALL, PARANOID`** # 匹配名称与其地址不匹配的任何主机，见下文。

这意味着所有服务、所有位置，因此任何未明确允许的服务都将被阻止，除非它们在允许文件中有条目被允许访问。

**注意：** 带有参数`"PARANOID"`；如果你打算在服务器上运行`telnet`或`ftp`服务，别忘了在服务器的`"/etc/hosts"`文件中添加客户端的计算机名称和 IP 地址，否则你可能会等待几分钟让 DNS 查找超时，然后才会出现`login:`提示符。

### 步骤 2

编辑`hosts.allow`文件（`vi /etc/hosts.allow`）并例如添加以下行：

明确授权的主机列在允许文件中。

例如：

**`sshd: 208.164.186.1 gate.openna.com`**

对于你的客户端机器：`208.164.186.1`是 IP 地址，`gate.openna.com`是允许使用`sshd`的一个客户端的主机名。

### 步骤 3

`tcpdchk`程序是 tcpd 包装器配置检查器。它检查你的 tcp 包装器配置并报告它能找到的所有潜在和实际问题。

- 配置完成后，运行程序`tcpdchk`。

```bash
[root@deep /]# tcpdchk
```

---

## 禁止显示系统 issue 文件

如果你不希望在别人远程登录时显示系统的 issue 文件，你可以在`"/etc/inetd.conf"`文件中更改 telnet 选项，使其看起来像这样：

```text
telnet stream tcp  nowait root  /usr/sbin/tcpd in.telnetd -h
```

在末尾添加`"-h"`标志将导致守护进程不显示任何系统信息，只是向用户显示`login:`提示符。这个技巧只有在你服务器上使用 telnet 守护进程时才需要（相反，我建议你使用 SSH）。

## `"/etc/host.conf"`文件

Linux 使用解析器库来获取与主机名对应的 IP 地址。`"/etc/host.conf"`文件指定如何解析名称。`"etc/host.conf"`文件中的条目告诉解析器库使用什么服务以及以什么顺序解析名称。

编辑`host.conf`文件（`vi /etc/host.conf`）并添加以下行：

```text
# 首先通过 DNS 查找名称，然后回退到 /etc/hosts。
order bind,hosts

# 我们有多个 IP 地址的机器。
multi on

# 检查 IP 地址欺骗。
nospoof on
```

`order`选项指示服务的顺序。示例条目指定解析器库应首先咨询名称服务器来解析名称，然后检查`"/etc/hosts"`文件。建议将解析器库设置为首先检查名称服务器（`bind`），然后检查 hosts 文件（`hosts`），以便在所有服务器上获得更好的性能和安全性。当然，你必须安装 DNS/BIND 软件，否则此配置将无法工作。

`multi`选项确定`"/etc/hosts"`文件中的主机是否可以具有多个 IP 地址（多个接口`ethN`）。具有多个 IP 地址的主机被称为多宿主的，因为多个 IP 地址的存在意味着该主机具有多个网络接口。例如，网关服务器将始终具有多个 IP 地址，并且必须将此选项设置为 ON。

`nospoof`选项指示注意不允许在此机器上进行欺骗。IP 欺骗是一种安全漏洞，通过欺骗信任关系中的计算机，让他们认为你是你其实不是的人。在这种类型的攻击中，设置一台机器使其“看起来”像合法的服务器，然后向合法终端系统、其他服务器或大型数据存储库系统发出连接和其他类型的网络活动。对于所有类型的服务器，此选项必须设置为 ON。

## `"/etc/services"`文件

某些“标准”服务提供的端口号在 RFC 1700“Assigned Numbers”中定义。`"/etc/services"`文件使服务器和客户端程序能够将服务名称转换为这些数字（端口）。该列表保存在每台主机上，存储在文件`"/etc/services"`中。只有`"root"`用户被允许修改此文件，而且很少编辑`"/etc/services"`文件进行更改，因为它已经包含了更常见的服务名称到端口号的映射。为了提高安全性，我们可以免疫此文件以防止未经授权的删除或添加服务。

- 要免疫`"/etc/services"`文件，请使用以下命令：

```bash
[root@deep /]# chattr +i /etc/services
```

## `"/etc/securetty"`文件

`"/etc/securetty"`文件允许你指定允许`"root"`用户登录哪些`TTY`设备。`"/etc/securetty"`文件由登录程序读取（通常是`"/bin/login"`）。其格式是允许的`tty`设备名称列表，对于所有其他被注释掉或在此文件中未出现的设备，禁止 root 登录。

通过注释掉不需要的`tty`来禁用它们（在行首添加`#`）。

编辑`securetty`文件（`vi /etc/securetty`）并注释掉以下行：

```text
tty1

#tty2
#tty3
#tty4
#tty5
#tty6
#tty7
#tty8
```

这意味着 root 只允许在`tty1`上登录。这是我的建议，只允许`"root"`在一个 tty 设备上登录，如果需要更多设备以`"root"`身份登录，请使用`"su"`命令切换到`"root"`。

## 特殊账户

**禁用所有**你在系统上不使用**的默认供应商账户非常重要**（即使你未在服务器上安装相关服务，某些账户也会默认存在）。这应该在每次升级或新软件安装后进行检查。Linux 为这些账户提供各种系统活动，如果未在服务器上安装服务，你可能不需要这些账户。如果你不需要这些账户，请删除它们。账户越多，访问你的系统就越容易。

我们假设你在 Linux 系统上使用 Shadow 密码套件。如果不是，你应该考虑这样做，因为它有助于在一定程度上加强安全性。如果你按照上述 Linux 安装并在“认证配置”下选择了“启用 Shadow 密码”选项，则此设置应该已经配置好了（有关更多信息，请参见第 2 章 Linux 服务器安装）。

- 要删除系统上的用户，请使用以下命令：

```bash
[root@deep /]# userdel username
```

- 要删除系统上的组，请使用以下命令：

```bash
[root@deep /]# groupdel username
```

### 步骤 1

在终端上输入以下命令以删除下面列出的用户：

```bash
[root@deep /]# userdel adm
[root@deep /]# userdel lp
[root@deep /]# userdel sync
[root@deep /]# userdel shutdown
[root@deep /]# userdel halt
[root@deep /]# userdel news
[root@deep /]# userdel uucp
[root@deep /]# userdel operator
[root@deep /]# userdel games (如果不使用 X Window 服务器，请删除此用户)。
[root@deep /]# userdel gopher
[root@deep /]# userdel ftp (如果不使用 ftp 匿名服务器，请删除此用户)。
```

**注意：** 默认情况下，`"userdel"`命令不会删除用户的主目录。如果你也想删除账户的主目录，请在`userdel`命令中添加`"-r"`选项。

### 步骤 2

在终端上输入以下命令以删除下面列出的用户组：

```bash
[root@deep /]# groupdel adm
[root@deep /]# groupdel lp
[root@deep /]# groupdel news
[root@deep /]# groupdel uucp
[root@deep /]# groupdel games (如果不使用 X Window 服务器，请删除此组)。
[root@deep /]# groupdel dip
[root@deep /]# groupdel pppusers
[root@deep /]# groupdel popusers (如果不使用 pop 服务器处理电子邮件，请删除此组)。
[root@deep /]# groupdel slipusers
```

### 步骤 3

将必要的用户添加到系统中：

- 要在系统上添加新用户，请使用以下命令：



```bash
[root@deep /]# useradd username
```

要在系统上为用户添加或更改密码，请使用以下命令：

```bash
[root@deep /]# passwd username
```

例如：

```bash
[root@deep /]# useradd admin
[root@deep /]# passwd admin
```

输出应如下所示：

```text
Changing password for user admin

New UNIX password: somepasswd

passwd: all authentication tokens updated successfully
```

## 步骤 4

不可变位可用于防止意外删除或覆盖必须保护的文件。它还可以防止某人创建指向此文件的符号链接，这已成为涉及删除`/etc/passwd`、`/etc/shadow`、`/etc/group`或`/etc/gshadow`的攻击来源。

要在密码和组文件上设置不可变位，请使用以下命令：

```bash
[root@deep /]# chattr +i /etc/passwd
[root@deep /]# chattr +i /etc/shadow
[root@deep /]# chattr +i /etc/group
[root@deep /]# chattr +i /etc/gshadow
```

**注意：** 将来，如果你打算添加或删除用户、密码、用户组或组文件，你必须取消这些文件的不可变属性，否则你将无法进行更改。此外，如果你打算安装一个会自动向已免疫的`passwd`和`group`文件中添加新用户的 RPM 程序，那么如果你没有取消这些文件的不可变属性，在安装过程中将会收到错误信息。

## 阻止任何人`su`到`root`

`su`（Substitute User，切换用户）命令允许你成为系统中其他已存在的用户。例如，你可以临时成为`root`并以超级用户`root`的身份执行命令。如果你不希望任何人`su`到`root`，或者想将`su`命令限制给某些用户，请在`/etc/pam.d/`目录下的`su`配置文件顶部添加以下两行。我们强烈建议你将允许`su`到`root`账户的人数限制为最少。

### 步骤 1

编辑`su`文件（`vi /etc/pam.d/su`）并在文件顶部添加以下两行：

```text
auth sufficient /lib/security/pam_rootok.so debug
auth required /lib/security/pam_wheel.so group=wheel
```

添加上述两行后，`/etc/pam.d/su`文件应如下所示：

```text
#%PAM-1.0

auth       sufficient /lib/security/pam_rootok.so debug
auth       required /lib/security/pam_wheel.so group=wheel
auth       required /lib/security/pam_pwdb.so shadow nullok
account    required /lib/security/pam_pwdb.so
password   required /lib/security/pam_cracklib.so
password   required /lib/security/pam_pwdb.so shadow use_authtok nullok
session    required /lib/security/pam_pwdb.so
session    optional /lib/security/pam_xauth.so
```

这意味着只有属于`wheel`组的成员才能`su`到`root`；这也包括日志记录。请注意，`wheel`组是你系统上可用于此目的的特殊账户。你不能使用任意组名来实现此技巧。此技巧与指定允许`root`登录的 TTY 设备相结合，将大大提高你系统的安全性。

### 步骤 2

现在，我们已经在`/etc/pam.d/su`文件配置中定义了`wheel`组，是时候添加一些允许`su`到`root`账户的用户了。如果你想让例如用户`admin`成为`wheel`组的成员，从而能够`su`到`root`，请使用以下命令：

```bash
[root@deep /]# usermod -G10 admin
```

这意味着`G`是补充组列表，用户也是该组成员。`10`是用户 ID`wheel`的数字值，`admin`是我们想要添加到`wheel`组的用户。对你系统上所有希望能够`su`到`root`账户的用户使用上述相同的命令。

**注意：** 如果你无法在 GNOME 终端中`su`，那是因为你使用了错误的终端。（所以不要因为终端问题就认为这个建议不起作用！）

## 资源限制

位于`/etc/security`目录下的`limits.conf`文件可用于控制和限制系统上用户的资源。对所有用户设置资源限制非常重要，这样他们就无法执行拒绝服务攻击（进程数量、内存量等）。这些限制必须在用户登录时为其设置。例如，系统上所有用户的限制可能如下所示。

### 步骤 1

编辑`limits.conf`检查文件（`vi /etc/security/limits.conf`）并添加或修改以下行：

```text
*    hard core     0
*    hard rss      5000
*    hard nproc    20
```

这表示禁止创建核心文件`core 0`，将进程数限制为 20（`nproc 20`），并将内存使用限制为 5M（`rss 5000`），适用于除超级用户`root`之外的所有人。以上所有内容只涉及通过你系统上的登录提示进入的用户。有了这种配额，你可以更好地控制用户在你的系统上可能拥有的进程、核心文件和内存使用。星号`*`表示：登录到服务器的所有用户。

### 步骤 2

你还必须编辑`/etc/pam.d/login`文件并在文件底部添加以下行：

```text
session  required /lib/security/pam_limits.so
```

添加上述行后，`/etc/pam.d/login`文件应如下所示：

```text
#%PAM-1.0

auth           required    /lib/security/pam_securetty.so
auth           required    /lib/security/pam_pwdb.so shadow nullok
auth           required    /lib/security/pam_nologin.so
account        required    /lib/security/pam_pwdb.so
password       required    /lib/security/pam_cracklib.so
password       required    /lib/security/pam_pwdb.so nullok use_authtok md5 shadow
session        required    /lib/security/pam_pwdb.so
session        required    /lib/security/pam_limits.so
#session       optional    /lib/security/pam_console.so
```

## 对挂载文件系统进行更多控制

你可以通过一些巧妙的选项（如`noexec`、`nodev`和`nosuid`）对挂载`/home`和`/tmp`等分区进行更多控制。这可以在`/etc/fstab`文本文件中设置。`fstab`文件包含有关各种文件系统挂载选项的描述性信息；每行针对一个文件系统。

`fstab`文本文件中与安全选项相关的信息如下：

| 选项 | 说明 |
| --- | --- |
| `defaults` | 允许此分区上的所有内容（配额、读写和 suid）。 |
| `noquota` | 不在此分区上设置用户配额。 |
| `nosuid` | 不在此分区上设置 SUID/SGID 访问。 |
| `nodev` | 不在此分区上设置字符或特殊设备访问。 |
| `noexec` | 不在此分区上设置任何二进制文件的执行。 |
| `quota` | 允许此分区上的用户配额。 |
| `ro` | 允许此分区只读。 |
| `rw` | 允许此分区读写。 |
| `suid` | 允许此分区上的 SUID/SGID 访问。 |

**注意：** 有关可以在此文件（`fstab`）中设置的选项的更多信息，请参阅关于`mount (8)`的手册页。

编辑`fstab`文件（`vi /etc/fstab`）并根据你的需要进行更改。例如：

```text
/dev/sda11 /tmp ext2 defaults 1 2
/dev/sda6 /home ext2 defaults 1 2
```

改为：

```text
/dev/sda11 /tmp ext2 defaults,rw,nosuid,nodev,noexec 1 2
/dev/sda6 /home ext2 defaults,rw,nosuid,nodev 1 2
```

这意味着，`nosuid`不允许设置用户标识符或组标识符位生效，`nodev`不解释此文件系统分区上的字符或块特殊设备，以及`noexec`不允许在挂载的文件系统上执行任何二进制文件。请注意，我们在上面的修改行中添加了`rw`选项。这是因为这些行的默认选项是`defaults`，意味着设置配额、读写和 suid，所以我们必须添加`rw`选项以继续在这些修改后的文件系统上拥有读写访问权限。

**注意：** 对于我们上面的示例，`/dev/sda11`代表系统上的`/tmp`目录分区，`/dev/sda6`代表`/home`目录分区。当然，这对你来说不会相同，具体取决于你如何对硬盘进行分区以及系统上安装的是哪种类型的磁盘，IDE（hda、hdb 等）还是 SCSI（sda、sdb 等）。

## 将 RPM 二进制文件移到安全位置或更改其默认权限

使用 RPM 命令在 Linux 服务器上安装完所需的所有软件后，为了获得更好的安全性，建议将其移到安全位置，如软盘或其他你选择的安全位置。通过这种方法，如果有人访问你的服务器并打算使用 RPM 命令安装恶意软件，他将无法做到。当然，如果将来你想通过 RPM 安装或升级新软件，你所要做的就是将 RPM 二进制文件重新放回原目录。

要将 RPM 二进制文件移到软盘，请使用以下命令：

```bash
[root@deep /]# mount /dev/fd0 /mnt/floppy/
[root@deep /]# mv /bin/rpm /mnt/floppy/
[root@deep /]# umount /mnt/floppy
```

**注意：** 切勿完全从系统中卸载 RPM 程序，否则你将无法在以后重新安装它，因为要安装 RPM 或其他软件，你需要有 RPM 命令可用。

你还可以做的一件事是将`rpm`命令的默认权限从 755 更改为 700。通过这种修改，非 root 用户将无法使用`rpm`程序进行查询、安装等操作；以防你在安装新程序后忘记将其移到安全位置。

要更改`/bin/rpm`的默认权限，请使用以下命令：

```bash
[root@deep /]# chmod 700 /bin/rpm
```

## Shell 日志记录

为了方便你重复执行长命令，bash shell 会在`~/.bash_history`文件中存储多达 500 条旧命令（其中`~/`是你的主目录）。系统上拥有账户的每个用户在其主目录中都会有这个`.bash_history`文件。减少`.bash_history`文件可以保存的旧命令数量，可以保护服务器上那些误将密码以明文形式输入到屏幕上、并且密码长时间存储在`.bash_history`文件中的用户。

### 步骤 1

`/etc/profile`文件中的`HISTFILESIZE`和`HISTSIZE`行决定了系统上所有用户的`.bash_history`文件可以保存的旧命令数量。对于所有账户，我强烈建议在`/etc/profile`文件中将`HISTFILESIZE`和`HISTSIZE`设置为较低的值，例如`20`。

编辑`profile`文件（`vi /etc/profile`）并将相关行修改为：

```bash
HISTFILESIZE=20
HISTSIZE=20
```

这意味着，每个用户主目录中的`.bash_history`文件最多可以存储 20 条旧命令。现在，如果有攻击者试图查看服务器上用户的`~/.bash_history`文件，以寻找误输入的明文密码，他或她找到密码的几率就会大大降低。

### 步骤 2

管理员还应在`/etc/skel/.bash_logout`文件中添加`rm -f $HOME/.bash_history`这一行，这样每次用户退出登录时，其`.bash_history`文件将被删除，攻击者将无法使用当前未登录系统的用户的`.bash_history`文件。

编辑`.bash_logout`文件（`vi /etc/skel/.bash_logout`）并添加以下行：

```bash
rm -f $HOME/.bash_history
```

**注意：** 上述技巧仅适用于你将来添加到服务器的用户。如果`/etc/passwd`文件中已有现有用户，你必须手动编辑并在其`.bash_logout`文件中添加上述行。

## `/etc/lilo.conf`文件

LILO 是 Linux 最常用的引导加载程序。它管理引导过程，可以从软盘、硬盘启动 Linux 内核映像，甚至可以充当其他操作系统的“引导管理器”。LILO 在 Linux 系统中非常重要，因此我们必须尽最大努力保护它。LILO 最重要的配置文件是`lilo.conf`文件，它位于`/etc`目录下。通过这个文件，我们可以配置和增强 LILO 程序以及 Linux 系统的安全性。以下是三个可以提高我们宝贵 LILO 程序安全性的重要选项。

- 添加：`Neo`。

  此选项控制 LILO 在引导至默认选择之前等待用户输入的时间（以秒为单位）。C2 安全性的一个要求是，除非系统双启动其他系统，否则此间隔应设置为 0。

- 添加：`restricted`。

  此选项仅在命令行上指定了参数时才要求输入密码（例如`linux single`）。`restricted`选项只能与`password`选项一起使用。确保在每个映像上都使用此选项。

- 添加：`password=<password>`。

  此选项在尝试以“单用户模式”加载 Linux 系统时要求用户输入密码。密码始终区分大小写，还要确保`/etc/lilo.conf`文件不再允许所有人读取，否则任何用户都将能够读取密码。以下是我们受保护的 LILO 以及`lilo.conf`文件的示例。

### 步骤 1

编辑`lilo.conf`文件（`vi /etc/lilo.conf`），并按照所示添加上面的三个选项或进行修改：

```text
boot=/dev/sda
map=/boot/map
install=/boot/boot.b
prompt
timeout=00 ← 将此行改为 00。
Default=linux
restricted ← 添加此行。
password=<password> ← 添加此行并输入你的密码。
image=/boot/vmlinuz-2.2.12-20
label=linux
initrd=/boot/initrd-2.2.12-10.img
root=/dev/sda6
read-only
```

### 步骤 2

由于配置文件`/etc/lilo.conf`现在包含未加密的密码，它应该只能由超级用户`root`读取。

```bash
[root@deep /]# chmod 600 /etc/lilo.conf （将不再允许所有人读取）。
```

### 步骤 3

现在我们必须更新配置文件`/etc/lilo.conf`，以使更改生效。

```bash
[root@deep /]# /sbin/lilo -v （用于更新 lilo.conf 文件）。
```

### 步骤 4

你还可以采取另一项安全措施来保护`lilo.conf`文件，即使用`chattr`命令将其设置为不可变。

要将文件设置为不可变，只需使用以下命令：

```bash
[root@deep /]# chattr +i /etc/lilo.conf
```

这将防止对`lilo.conf`文件进行任何更改（意外或其他方式）。如果你希望修改`lilo.conf`文件，则需要取消不可变标志。

要取消不可变标志，请使用以下命令：

```bash
[root@deep /]# chattr -i /etc/lilo.conf
```

## 禁用 Control-Alt-Delete 键盘关机命令

在`/etc/inittab`文件中将以下行注释掉（使用`#`），将禁用使用 Control-Alt-Delete 命令关闭计算机的功能。如果你的计算机物理安全性不是最好的，这一点非常重要。

为此，编辑`inittab`文件（`vi /etc/inittab`）并将行修改为：

```text
ca:: batate saner shdos shutdowntrolalte down -t3 -r now

修改为：

#ca::ctrlaltdel:/sbin/shutdown -t3 -r now
```

现在，要使更改生效，请在提示符处输入以下内容：

```bash
[root@deep /]# /sbin/init q
```



# 日志文件完整性

最重要的安全考虑之一是服务器`/var/log`目录下不同日志文件的完整性。尽管我们的服务器上已经实施了各种安全功能，但如果攻击者仍然能够侵入，我们最后的防线就是日志文件系统，因此确保日志文件完整性的方法非常重要。

如果你的服务器上或网络中的某台机器上安装了打印机，一个好主意是将所有重要日志打印成实际的纸质副本。这可以通过使用连续进纸打印机，并让`syslog`程序将所有你认为重要的日志发送到`/dev/lp0`（打印机设备）来实现。攻击者可以更改服务器上的文件、程序等，但当你有一台打印机打印出所有重要日志的真实纸质副本时，攻击者就无计可施了。

## 将日志发送到本地打印机

要将服务器上所有`telnet`、邮件、引导消息和`ssh`连接的日志记录到连接到此服务器的打印机，你需要在`/etc/syslog.conf`文件中添加以下行：

编辑`syslog.conf`文件（`vi /etc/syslog.conf`），并在文件末尾添加以下行：

```text
authpriv.*;mail.*;local7.*;auth.*;daemon.info /dev/lp0
```

- 现在重新启动`syslog`守护进程以使更改生效：

```text
[root@deep /]# /etc/rc.d/init.d/syslog restart
```

## 将日志发送到远程打印机

要将服务器上所有`telnet`、邮件、引导消息和`ssh`连接的日志记录到本地网络中远程服务器上连接的打印机，那么你需要在远程服务器的`/etc/syslog.conf`文件中添加以下行。

如果你的网络中没有打印机，你也可以将所有日志文件复制到另一台机器；只需省略下面远程服务器`syslog.conf`文件中添加`/dev/lp0`的第一步，直接转到远程服务器上的`-r`选项步骤。使用将所有日志文件复制到另一台机器的功能，将使你能够在一台主机上控制所有`syslog`消息，并降低管理需求。

编辑远程服务器（例如：`mail.openna.com`）上的`syslog.conf`文件（`vi /etc/syslog.conf`），并在文件末尾添加以下行：

```text
_nsec;mail.*;local7.*;auth.*;daemon.info /dev/lp0
```

由于`syslog`守护进程的默认配置是不接收来自网络的任何消息，因此我们必须启用远程服务器上接收网络消息的功能。要在远程服务器上启用接收网络消息的功能，请将以下选项`-r`添加到你的`syslog`守护进程脚本文件中（仅在远程主机上）：

- 编辑`syslog`守护进程（`vi +24 /etc/rc.d/init.d/syslog`）并修改：

```text
daemon syslogd -m 0
```

修改为：

```text
daemon syslogd -r -m 0
```

- 现在在远程主机上重新启动`syslog`守护进程以使更改生效：

```text
[root@mail /]# /etc/rc.d/init.d/syslog restart
```

## 配置远程服务器防火墙

现在，如果我们在远程服务器上有防火墙（你应该有一个），我们必须添加或验证以下行的存在：

```text
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $SYSLOG_CLIENT \
    -d $IPADDR 514 -j ACCEPT
```

其中`EXTERNAL_INTERFACE="eth0"`在防火墙文件中。

其中`IPADDR="208.164.186.2"`在防火墙文件中。

其中`SYSLOG_CLIENT="208.164.168.0/24"`在防火墙文件中。

- 现在在远程主机上重新启动防火墙以使更改生效：

```text
[root@mail /]# /etc/rc.d/init.d/firewall restart
```

此防火墙规则将允许来自我们内部客户端的远程服务器上的传入 UDP 数据包在端口 514（`syslog`端口）被接受。有关防火墙的更多信息，请参阅第 7 章“网络防火墙”。

## 配置本地服务器

最后，编辑本地服务器上的`syslog.conf`文件（`vi /etc/syslog.conf`），并在文件末尾添加以下行：

```text
authpriv.*;mail.*;local7.*;auth.*;daemon.info @mail
```

其中`mail`是远程服务器的主机名。现在，如果有人曾经侵入你的系统并威胁要删除重要的系统日志，你仍然有所有内容的纸质副本。那么追踪他们的来源并相应处理应该相当简单。

- 现在重新启动`syslog`守护进程以使更改生效：

```text
[root@deep /]# /etc/rc.d/init.d/syslog restart
```

与远程主机一样，我们必须在本地主机的防火墙脚本文件中添加或验证以下行的存在：

```text
ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR 514 \
    -d $SYSLOG_SERVER 514 -j ACCEPT
```

其中`EXTERNAL_INTERFACE="eth0"`在防火墙文件中。

其中`IPADDR="208.164.186.1"`在防火墙文件中。

其中`SYSLOG_SERVER="mail.openna.com"`在防火墙文件中。

- 现在重新启动防火墙以使更改生效：

```text
[root@deep /]# /etc/rc.d/init.d/firewall restart
```

此防火墙规则将允许本地服务器上目标为远程`syslog`服务器的出站 UDP 数据包通过端口 514（`syslog`端口）。有关防火墙的更多信息，请参阅第 7 章“网络防火墙”。

> **注意：** 切勿将网关服务器用作集中管理所有`syslog`消息的主机；这是一个非常糟糕的主意。`sysklogd`程序还有更多选项和策略，有关详细信息，请参阅`sysklogd(8)`、`syslog(2)`和`syslog.conf(5)`的手册页。

# 修复`/etc/rc.d/init.d`目录下脚本文件的权限

修复负责在启动时启动和停止所有需要运行的正常进程的脚本文件权限。

```text
[root@deep /]# chmod -R 700 /etc/rc.d/init.d/*
```

这意味着只有`root`才被允许在此目录下对脚本文件进行读取、写入和执行操作。我认为普通用户不需要知道这些脚本文件里面的内容。

> **注意：** 如果您安装新程序或更新使用位于`/etc/rc.d/init.d/`目录下的 init system V 脚本的程序，请不要忘记再次更改或验证该脚本文件的权限。

# `/etc/rc.d/rc.local`文件

默认情况下，当您登录到 Linux 系统时，它会告诉您 Linux 发行版名称、版本、内核版本和服务器名称。这泄露了太多信息。我们宁愿只向用户显示`Login:`提示。

## 步骤 1

要执行此操作，请编辑`/etc/rc.d/rc.local`文件，并在以下行前面加上`#`，如下所示：

```text
--

# 这将在每次启动时覆盖 /etc/issue。因此，请在此处对 /etc/issue
# 进行您想要的任何更改，否则重启后您将丢失这些更改。
#echo "" > /etc/issue
#echo "$R" >> /etc/issue
#echo "Kernel $(uname -r) on $a $(uname -m)" >> /etc/issue
#
#cp -f /etc/issue /etc/issue.net
#echo >> /etc/issue

--
```

## 步骤 2

然后，删除`/etc`目录下的以下文件：`issue.net`和`issue`：

```text
[root@deep /]# rm -f /etc/issue
[root@deep /]# rm -f /etc/issue.net
```

> **注意：** `/etc/issue.net`文件是用户通过网络（即`telnet`、`SSH`）连接到您的计算机时将看到的登录横幅。您可以在`/etc`目录中找到它，以及一个名为`issue`的类似文件，它是显示给本地用户的登录横幅。它只是一个文本文件，可以根据您自己的喜好进行自定义，但请注意，如上所述，如果您更改或删除它（就像我们这样做），您还需要修改`/etc/rc.d/rc.local` shell 脚本，该脚本在每次系统启动时都会重新创建`issue`和`issue.net`文件。

# root 拥有程序中的 SUID/SGID 位

如果一个程序设置为 SUID root，普通用户就能够以 root 身份运行该程序。计算机上所有模式中出现`s`位的程序和文件都启用了 SUID（`-rwsr-xr-x`）或 SGID（`-r-xr-sr-x`）位。由于这些程序向执行它们的用户授予特殊权限，因此从那些绝对不需要此类权限的 root 拥有的程序中移除`s`位非常重要。这可以通过执行命令`chmod a-s`并以 SUID/SGID 文件的名称作为参数来完成。

此类程序包括但不限于：

- 您从未使用过的程序。
- 您不希望任何非 root 用户运行的程序。
- 您偶尔使用，并且不介意使用`su(1)`切换到 root 来运行的程序。

我们在每个我们可能禁用并认为对于服务器日常工作并非绝对必需的程序旁边放置了一个星号（`*`）。请记住，您的系统需要一些 suid root 程序才能正常工作，所以要小心。

- 要查找 root 拥有的程序中所有带有`s`位的文件，请使用以下命令：

```text
[root@deep]# find / -type f \( -perm -04000 -o -perm -02000 \) -exec ls -lg {} \;
```

```text
*-rwsr-xr-x  1 root  root     35168   Sep 22  23:35  /usr/bin/chage
*-rwsr-xr-x  1 root  root     34756   Sep 22  23:35  /usr/bin/gpasswd
*-r-xr-sr-x  1 root  tty       6788   Sep  6  18:17  /usr/bin/wall
-rwsr-xr-x   1 root  root     33152   Aug 16  16:35  /usr/bin/at
-rwxr-sr-x   1 root  man      34656   Sep 13  20:26  /usr/bin/man
-r-s--x--x   1 root  root     22312   Sep 25  11:52  /usr/bin/passwd
-rws--x--x   2 root  root    518140   Aug 30  23:12  /usr/bin/suidperl
-rws--x--x   2 root  root    518140   Aug 30  23:12  /usr/bin/sperl5.00503
-rwxr-sr-x   1 root  slocate  24744   Sep 20  10:29  /usr/bin/slocate
*-rws--x--x  1 root  root     14024   Sep  9  01:01  /usr/bin/chfn
*-rws--x--x  1 root  root     13768   Sep  9  01:01  /usr/bin/chsh
*-rws--x--x  1 root  root      5576   Sep  9  01:01  /usr/bin/newgrp
*-rwxr-sr-x  1 root  tty       8328   Sep  9  01:01  /usr/bin/write
-rwsr-xr-x   1 root  root     21816   Sep 10  16:03  /usr/bin/crontab
*-rwsr-xr-x  1 root  root      5896   Nov 23  21:59  /usr/sbin/usernetctl
*-rwsr-xr-x  1 root  bin      16488   Jul  2  10:21  /usr/sbin/traceroute
-rwxr-sr-x   1 root  utmp      6096   Sep 13  20:11  /usr/sbin/utmpter
-rwsr-xr-x   1 root  root     14124   Aug 17  22:31  /bin/su
*-rwsr-xr-x  1 root  root     53620   Sep 13  20:26  /bin/mount
*-rwsr-xr-x  1 root  root     26700   Sep 13  20:26  /bin/umount
*-rwsr-xr-x  1 root  root     18228   Sep 10  16:04  /bin/ping
*-rwxr-sr-x  1 root  root      3860   Nov 23  21:59  /sbin/netreport
-r-sr-xr-x   1 root  root     26309   Oct 11  20:48  /sbin/pwdb_chkpwd
```

- 要禁用上述选定程序的`SUID`位，请键入以下命令：

```text
[root@deep /]# chmod a-s /usr/bin/chage
[root@deep /]# chmod a-s /usr/bin/gpasswd
[root@deep /]# chmod a-s /usr/bin/wall
[root@deep /]# chmod a-s /usr/bin/chfn
[root@deep /]# chmod a-s /usr/bin/chsh
[root@deep /]# chmod a-s /usr/bin/newgrp
[root@deep /]# chmod a-s /usr/bin/write
[root@deep /]# chmod a-s /usr/sbin/usernetctl
[root@deep /]# chmod a-s /usr/sbin/traceroute
[root@deep /]# chmod a-s /bin/mount
[root@deep /]# chmod a-s /bin/umount
[root@deep /]# chmod a-s /bin/ping
[root@deep /]# chmod a-s /sbin/netreport
```

如果您想知道这些程序的作用，请键入`man 程序名称`并阅读手册页。

例如：

```text
[root@deep /]# man netreport
```

# 内核可调参数

在 Red Hat Linux 6.2 的新版本中，Linux 下`/proc/sys`子目录中的所有内核参数都可以在运行时配置。您现在可以使用 Red Hat Linux 6.2 下的新文件`/etc/sysctl.conf`在运行时修改和设置内核参数。每次系统重启时都会读取和加载`sysctl.conf`文件。所有设置现在都存储在`/etc/sysctl.conf`文件中。对`/proc/sys`的所有修改都应通过`/etc/sysctl.conf`进行，因为它们更易于控制，并且在`rc.local`或任何其他“用户”脚本之前执行。下面，我们向您展示在 Red Hat Linux 6.1 和 6.2 版本的服务器上必须配置的网络安全选项。

## 防止您的系统响应 ping 请求

防止您的系统响应 ping 请求可以大大提高您的网络安全性，因为没有人能够 ping 您的服务器并收到回复。TCP/IP 协议套件存在一些弱点，允许攻击者利用隐蔽通道技术，在原本良性的数据包中偷偷传递数据。防止您的服务器响应 ping 请求有助于减少这个问题。

### 在 Red Hat Linux 6.1 下

一个……

```text
[root@deep /]# echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
```

……应该可以完成这项工作，使您的系统不会在任何接口上响应 ping。您可以将这行添加到您的`/etc/rc.d/rc.local`文件中，以便在系统重启时自动设置该命令。不响应 ping 至少可以让大多数“破解者”无法找到它，因为他们甚至不会知道它在那里。

要将其重新打开，只需：

```text
[root@deep /]# echo 0 > /proc/sys/net/ipv4/icmp_echo_ignore_all
```

您可以将这行添加到您的`/etc/rc.d/rc.local`文件中，以便在系统重启时自动设置该命令。

### 在 Red Hat Linux 6.2 下

编辑`/etc/sysctl.conf`文件并添加以下行：

```text
# 启用忽略 ping 请求
net.ipv4.icmp_echo_ignore_all = 1
```

您必须重新启动网络才能使更改生效。重新启动网络的命令如下：

- 要手动重新启动系统上的所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters	[ OK ]

Bringing up interface lo	[ OK ]
```

```text
Bringing up interface eth0                                    [  OK  ]

Bringing up interface eth1                                    [  OK  ]
```



## 防止系统响应广播请求

与 ping 请求一样，禁用广播请求也很重要。当本地网络中的一台机器向 IP 广播地址（即 `192.168.1.255`）发送数据包时，该数据包会被传送给该网络上的所有机器。然后网络上的所有机器都会响应这个 ICMP 回显请求，结果可能导致严重的网络拥塞或中断（拒绝服务攻击）。更多信息请参阅 RFC 2644。

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
```

你可以在你的 `/etc/rc.d/rc.local` 文件中添加这一行，以便系统重启时自动设置该命令。

### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```ini
# Enable ignoring broadcasts request

net.ipv4.icmp_echo_ignore_broadcasts = 1
```

你必须重启网络才能使更改生效。重启网络的命令如下：

- 要在系统上手动重启所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters                                        [  OK  ]

Bringing up interface lo                                          [  OK  ]

Bringing up interface eth0                                        [  OK  ]

Bringing up interface eth1                                        [  OK  ]
```

## 路由协议

路由和路由协议可能会带来一些问题。IP 源路由是指 IP 数据包包含到达其预期目的地的路径详细信息，这很危险，因为根据 RFC 1122，目的主机必须沿相同路径响应。如果攻击者能够将源路由数据包发送到你的网络中，那么他就能截获回复，并欺骗你的主机，使其认为正在与可信主机通信。我强烈建议你禁用 IP 源路由以保护服务器免受此漏洞的危害。

要在服务器上禁用 IP 源路由，请在终端中输入以下命令：

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# for f in /proc/sys/net/ipv4/conf/*/accept_source_route; do
> echo 0 > $f
> done
[root@deep /]#
```

将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，下次重启系统时就不必再输入了。

### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```ini
# Disables IP source routing

net.ipv4.conf.all.accept_source_route = 0
```

你必须重启网络才能使更改生效。重启网络的命令如下：

- 要在系统上手动重启所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters              [ OK ]

Bringing up interface lo                [ OK ]

Bringing up interface eth0              [ OK ]

Bringing up interface eth1              [ OK ]
```

**注意**：请注意，上述针对 Red Hat Linux 6.1 或 6.2 的命令将禁用所有接口（`lo`、`ethN`、`pppN` 等）上的源路由数据包。

## 启用 TCP SYN Cookie 防护

“SYN 攻击”是一种拒绝服务（DoS）攻击，它会耗尽你机器上的所有资源，迫使你必须重启。拒绝服务攻击（由于高流量而使服务器瘫痪的攻击，或占用足够的系统资源使服务器无法响应远程系统合法连接请求的攻击）很容易通过内部资源或外部连接（通过外联网和互联网）实现。要启用它，你需要执行：

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# echo 1 > /proc/sys/net/ipv4/tcp_syncookies
```

将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，下次重启系统时就不必再输入了。

### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```ini
# Enable TCP SYN Cookie Protection

net.ipv4.tcp_syncookies = 1
```

你必须重启网络才能使更改生效。重启网络的命令如下：

- 要在系统上手动重启所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters              [ OK ]

Bringing up interface lo                [ OK ]

Bringing up interface eth0              [ OK ]

Bringing up interface eth1              [ OK ]
```

**注意**：如果在执行上述命令时收到错误消息，请检查是否已在你的内核配置中启用 TCP syncookie 选项：IP: TCP syncookie support (not enabled per default) (`CONFIG_SYN_COOKIES`) [Y/n/?]。

## 禁用 ICMP 重定向接受

当主机使用非最优或失效的路由到达特定目的地时，路由器会使用 ICMP 重定向数据包通知主机正确的路由应该是什么。如果攻击者能够伪造 ICMP 重定向数据包，他就能更改主机上的路由表，并可能通过使流量经由你不希望的路径流动来破坏主机的安全性。强烈建议禁用 ICMP 重定向接受以保护服务器免受此漏洞的危害。

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# for f in /proc/sys/net/ipv4/conf/*/accept_redirects; do
> echo 0 > $f
> done
[root@deep /]#
```

将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，下次重启系统时就不必再输入了。

### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```ini
# Disable ICMP Redirect Acceptance

net.ipv4.conf.all.accept_redirects = 0
```

你必须重启网络才能使更改生效。重启网络的命令如下：

- 要在系统上手动重启所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters                              [ OK ]

Bringing up interface lo                                [ OK ]

Bringing up interface eth0                              [ OK ]

Bringing up interface eth1                              [ OK ]
```

**注意**：请注意，上述针对 Red Hat Linux 6.1 或 6.2 的命令将禁用所有接口（`lo`、`ethN`、`pppN` 等）上的重定向接受数据包。

## 启用 always-defragging 防护

如果你将 Linux 服务器用作网关，将内部流量伪装到互联网（IP 伪装），则必须启用此防护。

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# echo 1 > /proc/sys/net/ipv4/ip_always_defrag
```

将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，下次重启系统时就不必再输入了。

### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```ini
# Enable always defragging Protection

net.ipv4.ip_always_defrag = 1
```

你必须重启网络才能使更改生效。重启网络的命令如下：

- 要在系统上手动重启所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters                              [ OK ]

Bringing up interface lo                                [ OK ]

Bringing up interface eth0                              [ OK ]

Bringing up interface eth1                              [ OK ]
```

## 启用错误消息防护

此选项将提醒你网络中的所有错误消息。

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# echo 1 > /proc/sys/net/ipv4/icmp_ignore_bogus_error_responses
```

将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，下次重启系统时就不必再输入了。

### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```ini
# Enable bad error message Protection

net.ipv4.icmp_ignore_bogus_error_responses = 1
```

你必须重启网络才能使更改生效。重启网络的命令如下：

- 要在系统上手动重启所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters          [ OK ]

Bringing up interface lo            [ OK ]

Bringing up interface eth0          [ OK ]

Bringing up interface eth1          [ OK ]
```

## 启用 IP 欺骗防护

欺骗防护可以防止你的网络成为欺骗（即伪造）通信的来源，这些通信通常用于 DoS 攻击。

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# for f in /proc/sys/net/ipv4/conf/*/rp_filter; do
> echo 1 > $f
> done
[root@deep /]#
```

将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，下次重启系统时就不必再输入了。

### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```ini
# Enable IP spoofing protection, turn on Source Address Verification

net.ipv4.conf.all.rp_filter = 1
```

你必须重启网络才能使更改生效。重启网络的命令如下：

- 要在系统上手动重启所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters          [ OK ]

Bringing up interface lo            [ OK ]

Bringing up interface eth0          [ OK ]

Bringing up interface eth1          [ OK ]
```

```text
Bringing up interface lo              [ OK ]

Bringing up interface eth0              [ OK ]

Bringing up interface eth1              [ OK ]
```

## 记录伪造数据包、源路由数据包、重定向数据包

此保护功能会将所有伪造数据包、源路由数据包和重定向数据包记录到您的日志文件中。

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# for f in /proc/sys/net/ipv4/conf/*/log_martians; do
> echo 1 > $f
> done
[root@deep /]#
```

将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，下次重启系统时就不需要再次输入了。

### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```ini
# Log Spoofed Packets, Source Routed Packets, Redirect Packets

net.ipv4.conf.all.log_martians = 1
```

您必须重新启动网络才能使更改生效。重新启动网络的命令如下：

- 要在您的系统上手动重新启动所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters            [ OK ]

Bringing up interface lo              [ OK ]

Bringing up interface eth0            [ OK ]

Bringing up interface eth1            [ OK ]
```

## 异常或隐藏文件

重要的是不要忘记在系统的每个地方查找异常或隐藏文件（以句点开头的文件，通常不会由 `ls` 命令显示），因为这些文件可能被用来隐藏工具和信息的（密码破解程序、来自其他系统的密码文件等）。在 UNIX 系统中，一种常见的技术是在用户账户中放置一个隐藏目录或文件，并使用不寻常的名称，比如 `'...'` 或 `'.. '`（点 点 空格）或 `'..^G'`（点 点 control-G）。可以使用 `find` 程序来查找隐藏文件。

例如：

```bash
[root@deep /]# find / -name ".. " -print -xdev

[root@deep /]# find / -name "ignty" -print -xdev | cat -v
```




**注意：** 名称如`.xx`和`.mail`的文件也已被使用（即，看起来可能是正常的文件）。

## 查找所有启用了 SUID/SGID 位的文件

在我们移除了那些绝对不需要此类特权的文件后，系统上仍然存在的所有 SUID 和 SGID 文件都是潜在的安全风险，应密切监控。因为这些程序会授予执行它们的用户特殊特权，所以必须确保没有安装不安全的程序。

黑客最喜欢的一种伎俩就是利用 SUID `root` 程序，并留下一个 SUID 程序作为后门以便下次进入。查找系统上所有的 SUID 和 SGID 程序，并记录它们是什么，这样您就能注意到任何变化，这可能表明有潜在的入侵者。

- 使用以下命令查找系统上所有 SUID/SGID 程序：

```bash
[root@deep /]# find / -type f \( -perm -04000 -o -perm -02000 \) -exec ls -lg {} \;
```

**注意：** 请参阅本书第10章“安全软件（监控工具）”，了解有关 `sXid` 软件的更多信息，该软件将每天自动为您完成这项工作并通过邮件报告结果。

## 查找组可写和世界可写的文件和目录

组可写和世界可写的文件和目录，特别是系统文件（分区），如果黑客获得了对您系统的访问权限并修改了它们，就可能成为安全漏洞。此外，世界可写的目录很危险，因为它们允许黑客随意添加或删除这些目录中的文件。在正常操作过程中，会有几个文件是可写的，包括一些来自`/dev`、`/var/catman`目录的文件，以及系统上所有的符号链接。

- 要查找系统上所有组和世界可写的文件，请使用以下命令：

```bash
[root@deep /]# find / -type f \( -perm -2 -o -perm -20 \) -exec ls -lg {} \;
```

- 要查找系统上所有组和世界可写的目录，请使用以下命令：

```bash
[root@deep /]# find / -type d \( -perm -2 -o -perm -20 \) -exec ls -ldg {} \;
```

**注意：** 可以定期使用像 Tripwire 软件这样的文件和目录完整性检查器来扫描、管理和查找被修改的组或世界可写文件和目录。有关 Tripwire 的更多信息，请参阅本书第10章“安全软件（监控工具）”。

## 无主文件

不允许存在任何无主文件。无主文件也可能表明入侵者已经访问了您的系统。如果您在系统上发现无主文件或目录，请验证其完整性，如果一切正常，请为其指定所有者名称。有时您可能卸载了一个程序，而得到与该软件相关的无主文件或目录；在这种情况下，您可以安全地 mortgage 删除该文件或目录。

- 要查找系统上没有所有者的文件，请使用以下命令：

```bash
[root@deep /]# find / -nouser -o -nogroup
```

**注意：** files reported under `/dev` directory don't count.

## 查找 `.rhosts` 文件

查找服务器上可能存在的所有`.rhosts`文件应该是您常规系统管理职责的一部分，因为这些文件不应在您的系统上存在。请记住，黑客只需一个不安全的账户就可能获得对整个网络的访问权限。

- 您可以使用以下命令查找系统上的所有`.rhosts`文件：

```bash
[root@deep /]# find /home -name .rhosts
```

您还可以使用 cron 作业定期检查、报告并删除`$HOME/.rhosts`文件。此外，应按照政策规定，让用户了解您会定期进行此类审计。

- 要使用 cron 作业定期检查并通过邮件报告所有`.rhosts`文件，请执行以下操作：

以`root`身份在`/etc/cron.daily`目录下创建`find_rhosts_files`脚本文件（`touch /etc/cron.daily/find_rhosts_files`），并在此脚本文件中添加以下行：

```sh
#!/bin/sh

/usr/bin/find /home -name .rhosts | (cat <<EOF

This is an automated report of possible existent ".rhosts" files on the server

deep.openna.com, generated by the find utility command.

New detected ".rhosts" files under the "/home" directory include:

EOF

cat

) | /bin/mail -s "Content of .rhosts file audit report" root
```

现在将此脚本文件设为可执行，验证所有者，并将组更改为`root`。

```bash
[root@deep /]# chmod 755 /etc/cron.daily/find_rhosts_files

[root@deep /]# chown 0.0 /etc/cron.daily/find_rhosts_files
```

每天都会向`root`发送一封邮件，主题为：“Content of .rhosts file audit report”，其中包含潜在的新`.rhosts`文件。

## 系统已被入侵

如果您认为您的系统已被入侵，请联系 CERT® 协调中心或您在 FIRST（Forum of Incident Response and Security Teams，事件响应和安全团队论坛）的代表。

互联网电子邮件：[cert@cert.org](mailto:cert@cert.org)  
CERT 热线：(+1) 412-268-7090  
传真：(+1) 412-268-6989

CERT/CC 人员在工作日的 8:00 a.m. – 8:00 p.m. EST (GMT –5)/EDT (GMT –4) 接听电话；他们在其他时间、周末和节假日处于紧急待命状态。

# 第4章 系统通用优化

## 本章内容

- Linux 通用优化

## Linux 通用优化

### 概述

在配置的这个阶段，您现在应该已经拥有了一台配置良好且安全的 Linux 服务器。我们的服务器安装了最必要的软件包和程序以能够正常工作，并进行了最必要的通用安全配置。在我们继续下一步并开始安装想要与客户共享的服务之前，现在重要的是对我们的 Linux 服务器进行调优。

我们将在以下部分进行的调优将应用于整个系统。它也适用于现在以及未来的程序，比如我们稍后将要安装的服务。一般来说，如果您不使用 x386 Intel 处理器，那么开箱即用的 Red Hat Linux 并未针对您的特定 CPU 架构进行优化（现在大多数人在 Pentium 处理器上运行 Linux）。以下部分将指导您完成针对不同步骤，以针对您的特定处理器、内存、网络以及文件系统优化您的 Linux 服务器。

### `/etc/profile` 文件

`/etc/profile` 文件包含系统范围的环境变量和启动程序。您在此文件中所有的自定义设置都将应用于系统上的整个变量环境，因此在此文件中放置优化标志是一个不错的选择。为了从 x86 程序中榨取最大性能，您可以在编译时使用`-O9`标志进行完全优化。许多程序在 Makefile 中包含`-O2`。`-O9`是最高级别的优化。它会增加生成产物的大小，但运行速度更快。

**注意：** `-O9`标志并不总是能为您的处理器带来最佳性能。如果您拥有 x686 及以上处理器，当然没问题，但如果是低于 x686，则不一定。

在编译时，对任何类型的处理器都使用`-fomit-frame-pointer`开关。这将使用栈来访问变量。遗憾的是，使用此选项几乎无法进行调试。您还可以使用`-mcpu=cpu_type`和`-march=cpu_type`开关来针对所列 CPU 尽最大能力优化程序。但是，生成的代码将只能在指定的 CPU 或更高版本上运行。

以下是我们建议您根据 CPU 架构放在`/etc/profile`文件中的优化标志。这些优化选项仅当我们在服务器上编译和安装新程序时应用。这些优化在我们的 Linux 手册中不起任何作用；它只是告诉我们的编译器用我们在`/etc/profile`文件中指定的优化标志来优化我们将要安装的新程序。

#### 步骤 1：适用于 CPU i686 或 PentiumPro、Pentium II、Pentium III

在`/etc/profile`文件中，为 PentiumPro、Pentium II 和 III Pro 处理器系列添加以下行：

```bash
CFLAGS='-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions'
```

#### 适用于 CPU i586 或 Pentium

在`/etc/profile`文件中，为 Pentium 处理器系列添加以下行：

```bash
CFLAGS='-O3 -march=pentium -mcpu=pentium -ffast-math -funroll-loops -fomit-frame-pointer -fforce-mem -fforce-addr -malign-double -fno-exceptions'
```

#### 适用于 i486 CPU

在`/etc/profile`文件中，为 i486 处理器系列添加以下行：

```bash
CFLAGS='-O3 -funroll-all-loops -malign-double -mcpu=i486 -march=i486 -fomit-frame-pointer -fno-exceptions'
```

#### 步骤 2

在选择完 CPU 设置（i686、i586 或 i486）后，在`/etc/profile`文件中稍下的位置，将`CFLAGS LANG LESSCHARSET`添加到`export`行：

```bash
export PATH PS1 HOSTNAME HISTSIZE HISTFILESIZE USER LOGNAME MAIL INPUTRC CFLAGS LANG LESSCHARSET
```

#### 步骤 3

注销并重新登录；之后，新的 `CFLAGS` 环境变量就会被设置，软件和其他`configure`工具将能识别它。Pentium（Pro/II/III）优化仅适用于 egcs 或 pgcc 编译器。egcs 编译器已默认安装在您的服务器上，因此无需担心。

以下是我们使用的不同优化选项的说明：

- `-funroll-loops`

  `-funroll-loops`优化选项将执行循环展开优化，并且仅对编译时或运行时能够确定迭代次数的循环执行此操作。

- `-funroll-all-loops`

  `-funroll-all-loops`优化选项也将执行循环展开优化，并且对所有循环都执行此操作。

- `-ffast-math`

  `-ffast-math`优化选项将允许 GCC 编译器为了优化代码速度而违反一些 ANSI 或 IEEE 规则/规范。

- `-malign-double`

  `-malign-double`优化选项将控制 GCC 编译器是否将 double、long double 和 long long 变量按双字边界或单字边界对齐。这将产生在`Pentium`上运行稍快的代码，但会消耗更多内存。

- `-mcpu=cpu_type`

  `-mcpu=cpu_type`优化选项将设置用于机器类型调度指令时的默认 CPU。

- `-march=cpu_type`

  `-march=cpu_type`优化选项将为机器和 CPU 类型生成指令。指定`-march=cpu_type`选项也意味着在编译中指定了`-mcpu=cpu_type`选项。

- `-fforce-mem`

  `-fforce-mem`优化选项将通过强制在执行算术运算前将内存操作数复制到寄存器中，以及使所有内存引用成为潜在的公共子表达式，来生成更好的代码。

- `-fforce-addr`

  `-fforce-addr`优化选项将通过强制在执行算术运算前将内存地址常量复制到寄存器中，来生成更好的代码。

- `-fomit-frame-pointer`

  `-fomit-frame-pointer`优化选项是最有趣的选项之一，它将允许程序对于不需要帧指针的函数不将帧指针保留在寄存器中。这避免了保存、设置和恢复帧指针的指令；它还使许多函数中多出一个可用寄存器，并且使大多数机器上的调试变得不可能。

**重要提示：** 我们在本书中描述的所有未来优化默认都指的是 Pentium II/III CPU 系列。因此，如果需要，您必须在`/etc/profile`文件中以及在编译时为您的特定 CPU 处理器类型调整编译标志。

## 基准测试结果

### 按架构汇总

根据您的处理器架构和编译器版本（GCC/EGCS），优化结果可能会有所不同。下面的图表将帮助您为编译器/CPU 架构选择最佳的编译标志。

安装在您的 Red Hat Linux 6.1 和 6.2 版本上的编译器版本是 egcs 2.91.66，但在选择编译器优化选项之前，请务必确认。

- 要验证系统上安装的编译器版本，请使用以下命令：

```bash
[root@deep /]# egcs --version
egcs-2.91.66
```

**注意：** 所有基准测试结果以及未来结果，可从 GCC 主页获取，地址为：[http://egcs.cygnus.com/](http://egcs.cygnus.com/)

现在举例说明：

对于 Pentium II/III CPU（i686）且编译器版本为 egcs-2.91.66，最佳优化选项为：

`CFLAGS='-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions'`

对于 Pentium CPU（i586）且编译器版本为 egcs-2.91.66，最佳优化选项为：

`CFLAGS='-O3 -march=pentium -mcpu=pentium -ffast-math -funroll-loops -fomit-frame-pointer -fforce-mem -fforce-addr -malign-double -fno-exceptions'`

对于 i486 CPU 且编译器版本为 egcs-2.91.66，最佳优化选项为：

`CFLAGS='-O3 -funroll-all-loops -malign-double -mcpu=i486 -march=i486 -fomit-frame-pointer -fno-exceptions'`

## `bdflush` 参数

`bdflush`文件与 Linux 内核虚拟内存（VM）子系统的操作密切相关，对磁盘使用有少量影响。该文件（`/proc/sys/vm/bdflush`）控制`bdflush`内核守护进程的操作。我们通常调整此文件以提高文件系统性能。通过将某些值从默认值更改为如下所示，系统似乎更加响应迅速；例如，它会等待稍长时间再写入磁盘，从而避免一些磁盘访问争用。

Red Hat Linux 下`bdflush`参数的默认设置为：

`40 500 64 256 500 3000 500 1884 2`

- 要更改`bdflush`的值，请在终端上输入以下命令：

#### Red Hat Linux 6.1 下

```bash
[root@deep /]# echo "100 1200 128 512 15 5000 500 1884 2" > /proc/sys/vm/bdflush
```

您可以将上述命令添加到`/etc/rc.d/rc.local`脚本文件中，下次重启系统时就无需再次输入。

#### Red Hat Linux 6.2 下

编辑`/etc/sysctl.conf`文件并添加以下行：

```conf
# 提高文件系统性能

vm.bdflush = 100 1200 128 512 15 5000 500 1884 2
```




必须重新启动网络才能使更改生效。重新启动网络的命令如下：

- 要手动重新启动系统上的所有网络设备，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/network restart
Setting network parameters                [  OK  ]
Bringing up interface lo                  [  OK  ]
Bringing up interface eth0                [  OK  ]
Bringing up interface eth1                [  OK  ]
```

在我们上面的示例中，根据`/usr/src/linux/Documentation/sysctl/vm.txt`文件，第一个参数（`100`%）控制缓冲区缓存中脏缓冲区的最大数量。脏意味着缓冲区的内容仍需写入磁盘（而非干净缓冲区，干净缓冲区可以直接丢弃）。将此值设置得较高意味着 Linux 可以长时间延迟磁盘写入，但也意味着当内存变少时它必须一次性进行大量 I/O。较低的值将使磁盘 I/O 更加均匀分布。

第二个参数（`1200`）（`ndirty`）给出了`bdflush`一次可以写入磁盘的脏缓冲区的最大数量。高值意味着延迟的、突发式的 I/O，而小值可能导致`bdflush`唤醒不够频繁时出现内存短缺。

第三个参数（`128`）（`nrefill`）是当调用`refill_freelist()`时`bdflush`将添加到空闲缓冲区列表的缓冲区数量。有必要预先分配空闲缓冲区，因为缓冲区的大小通常与内存页不同，需要事先进行一些簿记工作。数字越高，浪费的内存越多，`refill_freelist()`需要运行的次数就越少。

当`refill_freelist()`（`512`）遇到超过`nref_dirt`个脏缓冲区时，它将唤醒`bdflush`。

最后，`age_buffer`（`50*HZ`）和`age_super`参数（`5*HZ`）控制 Linux 在将脏缓冲区写入磁盘之前等待的最长时间。该值以 jiffies（时钟滴答）表示；每秒的 jiffies 数为 100。`age_buffer`是数据块的最大年龄，而`age_super`用于文件系统元数据。

第五个（`15`）和最后两个参数（`1884`和`2`）系统未使用，因此我们无需更改默认值。

**注意**：查看`/usr/src/linux/Documentation/sysctl/vm.txt`以获取有关如何改进与虚拟内存相关的内核参数的更多信息。

## `buffermem`参数

`buffermem`文件也与 Linux 内核虚拟内存（VM）子系统的操作密切相关。该文件`/proc/sys/vm/buffermem`中的值控制应使用how much memory should be used for buffer memory（以百分比表示）。重要的是要注意，该百分比是按系统总内存的百分比计算的。

Red Hat Linux 下`buffermem`参数的默认设置为：

`2 10 60`

- 要更改`buffermem`的值，请在终端上输入以下命令：

### Red Hat Linux 6.1 下

```bash
[root@deep /]# echo "80 10 60" >/proc/sys/vm/buffermem
```

您可以将上述命令添加到`/etc/rc.d/rc.local`脚本文件中，下次重启系统时就无需再次输入。

### Red Hat Linux 6.2 下

编辑`/etc/sysctl.conf`文件并添加以下行：

```ini
# 提高虚拟内存性能
vm.buffermem = 80 10 60
```

必须重新启动网络才能使更改生效。重新启动网络的命令如下：

- 要手动重新启动系统上的所有网络设备，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/network restart
Setting network parameters			[  OK  ]
Bringing up interface lo			[  OK  ]
Bringing up interface eth0			[  OK  ]
Bringing up interface eth1			[  OK  ]
```

在我们上面的示例中，根据`/usr/src/linux/Documentation/sysctl/vm.txt`文件，第一个参数（`80`%）表示使用最低 80% 的内存作为缓冲区缓存；即应花在缓冲区内存上的最低内存百分比。

最后两个参数（`10`和`60`）系统未使用，因此我们无需更改默认值。

**注意**：查看`/usr/src/linux/Documentation/sysctl/vm.txt`以获取有关如何改进与虚拟内存相关的内核参数的更多信息。

## `ip_local_port_range`参数

`ip_local_port_range` `/proc/sys/net/ipv4/ip_local_port_range`定义了 TCP 和 UDP 流量选择本地端口时使用的本地端口范围。在此文件的参数中，你会看到两个数字：第一个数字是服务器上允许 TCP 和 UDP 流量使用的第一个本地端口，第二个是最后一个本地端口号。对于高使用率的系统，你可以将其默认参数更改为 32768-61000（第一个-最后一个）。

Red Hat Linux 下`ip_local_port_range`参数的默认设置为：`1024 4999`

- 要更改`ip_local_port_range`的值，请在终端上输入以下命令：

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# echo "32768 61000" > /proc/sys/net/ipv4/ip_local_port_range
```

将上述命令添加到`/etc/rc.d/rc.local`脚本文件中，下次重启系统时你就无需再次输入。

### 在 Red Hat Linux 6.2 下

编辑`/etc/sysctl.conf`文件并添加以下行：

```ini
# Allowed local port range
net.ipv4.ip_local_port_range = 32768 61000
```

你必须重新启动网络才能使更改生效。重新启动网络的命令如下：

- 要手动重新启动系统上的所有网络设备，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters                                    [ OK ]

Bringing up interface lo                                    [ OK ]

Bringing up interface eth0                                  [ OK ]

Bringing up interface eth1                                  [ OK ]
```

## `/etc/nsswitch.conf`文件

`/etc/nsswitch.conf`文件用于配置要使用哪些服务 boring text... 服务来确定诸如主机名、密码文件和组文件等信息。在我们的案例中，最后两个——“密码文件”和“组文件”并未被使用，因为我们的服务器上不使用 NIS 服务。因此，我们将重点关注此文件中的`hosts`行。

编辑`nsswitch.conf`文件（`vi /etc/nsswitch.conf`）并将`hosts`行更改为：

`hosts: dns files`

这意味着，对于想要解析地址的程序。它们应该首先使用`dns`功能，如果 DNS 服务器不可用或无法解析地址，则使用`/etc/hosts`文件。

此外，我们建议从此文件每一行中删除所有 NIS 服务实例，除非你正在使用 NIS！结果应如下所示：

```text
passwd:        files
shadow:        files
group:         files
hosts:         dns files
bootparams:    files
ethers:        files
netmasks:      files
networks:      files
protocols:     files
rpc:          /star
```

## `noatime`属性

Linux 文件系统有一个特殊的挂载选项叫做`noatime`，可以在`/etc/fstab`文件中每个涉及文件系统的行中添加。如果文件系统使用此选项挂载，对文件系统的读取访问将不再更新与该文件关联的`atime`信息，正如我们上面所解释的。`noatime`设置的重要性在于，它消除了系统因仅读取文件而需要对文件系统进行写入操作的需求。由于写入操作可能较为昂贵，这可以带来可观的性能提升。注意，文件的写入时间信息在文件被写入时仍会继续更新。在下面的示例中，我们将对`/chroot`文件系统设置`noatime`选项。

编辑`fstab`文件（`vi /etc/fstab`），并在引用`/chroot`文件系统的行中，在`defaults`选项之后添加`noatime`选项，如下所示：

```text
E.I: /dev/sda7    /chroot    ext2    defaults,noatime    1 2
```

你必须**重启**系统才能使更改生效：

```bash
[root@deep /]# reboot
```

然后使用以下命令测试你的结果：

```bash
[root@deep]# cat /proc/mounts
```

```text
/dev/root / ext2 rw 0 0
/proc /proc proc rw 0 0
/dev/sda1 /boot ext2 rw 0 0
/dev/sda8 /cache ext2 rw 0 0
/dev/sda7 /chroot ext2 rw,noatime 0 0
/dev/sda6 /home ext2 rw 0 0
/dev/sda11 /tmp ext2 rw 0 0
/dev/sda5 /usr ext2 rw 0 0
/dev/sda9 /var ext2 rw 0 0
none /dev/pts devpts rw 0 0
```

如果你看到类似这样的内容：`/dev/sda7 /chroot ext2 rw,noatime 0 0`，恭喜你！

## 交换分区

将交换分区放在管理磁盘的开始位置可能会带来一些可接受的性能提升。磁盘的开始位置在物理上位于柱面的外圈部分，读写磁头每转一圈可以覆盖更大的范围。我们通常看到放在磁盘末尾的分区使用`hdparm -t`命令测试时速度会慢 3MB/s。

## 调整 IDE 硬盘性能

通过设置 IDE 驱动器使用 DMA、32 位传输和多扇区模式，大量磁盘 I/O 操作的性能得到了提升。除非另有说明，内核似乎使用更为保守的设置。改变驱动器设置的神奇命令是`hdparm`。

- 要通过 PCI 总线启用 32 位 I/O，使用以下命令：

  ```bash
  [root@deep /]# /sbin/hdparm -c 1 /dev/hda（或 hdb、hdc 等）
  ```

这通常取决于你的 IDE 磁盘驱动器型号，可以将缓冲磁盘读取时间减少一半。`hdparm`(8) 手册页指出，对于某些芯片组你可能需要使用`-c 3`。所有 (E)IDE 驱动器通过接口卡的带状电缆仍然只有 16 位连接。

- 要启用 DMA，使用以下命令：

  ```bash
  [root@deep /]# /sbin/hdparm -d 1 /dev/hda（或 hdb、hdc 等）
  ```

这可能取决于你的内核是否编译了对主板芯片组的支持。此外，此命令将为你的硬盘启用 DMA 支持，它将减少缓冲磁盘读取时间，并将性能提升 2 倍。

- 要启用 multiword DMA mode 2 传输，使用以下命令：

  ```bash
  [root@deep /]# /sbin/hdparm -d 1 -X34 /dev/hda（或 hdb、hdc 等）
  ```

这为较新的 (E)IDE/ATA2 驱动器设置 IDE 传输模式。（查看你的硬件手册以确认是否支持）。

- 要启用 UltraDMA mode2 传输，使用以下命令：

  ```bash
  [root@deep /]# /sbin/hdparm -d 1 -X66 /dev/hda（或 hdb、hdc 等）
  ```

你需要事先为芯片组准备好 UltraDMA。此外，请参阅关于`hdparm`的手册页以获取更多信息。请极其谨慎地使用此命令！

- 要设置多扇区模式 I/O，使用以下命令：

  ```bash
  [root@deep /]# /sbin/hdparm -m XX /dev/hda（或 hdb、hdc 等）
  ```

其中`XX`是你的驱动器支持的最大设置。`-i`标志可用于查找已安装驱动器支持的最大设置：在输出中查找`MaxMultSect`。

```bash
[root@deep /]# /sbin/hdparm -i /dev/hda（或 hdb、hdc 等）

/dev/hda:

Model=Maxtor 7540 AV, FwRev=GA7X4647, SerialNo=L1007YZS
Config={ HardSect NotMFM HdSw>15uSec Fixed DTR>5Mbs FmtGapReq }
RawCHS=1046/16/63, TrkSize=0, SectSize=0, ECCbytes=11
BuffType=3(DualPortCache), BuffSize=32kB, MaxMultSect=8, MultiSect=8
DblWordIO=yes, maxPIO=2(fast), DMA=yes, maxDMA=1(medium)
CurCHS=523/32/63, CurSects=379584528, LBA=yes, LBA=yes, LBAsects=1054368
tDMA={min:150,rec:150}, DMA modes: sword0 sword1 *sword2 *mword0
IORDY=on/off, tPIO={min:240,w/IORDY:180}, PIO modes: mode3
```

多扇区模式（又称 IDE 块模式），是大多数现代 IDE 硬盘的一项特性，允许每个 I/O 中断传输多个扇区，而不是通常的每个中断一个扇区。启用此特性后，通常可以将磁盘 I/O 的操作系统开销减少 30-50%。在许多系统上，它还可以将数据吞吐量提高 5% 到 50%。

你可以通过以性能测试模式运行`hdparm`来测试你的更改结果：

```bash
[root@deep /]# /sbin/hdparm -t /dev/hda（或 hdb、hdc 等）
```

**注意：**一旦你设置了一组`hdparm`选项，你可以将这些命令放入`/etc/rc.d/rc.local`文件中，以便每次重启机器时运行。另外，不要忘记重启服务器以使选项生效。

## 通过 TCP/IP 在单位时间内处理更多连接

这个技巧只是将 TCP/IP 连接的默认时间值降低，以便你的 TCP/IP 协议在单位时间内可以处理更多连接。以下内容将减少你的 Linux 系统尝试完成关闭连接所需的时间，以及杀死一个过时连接之前的时间。这也将关闭一些不需要的 IP 扩展功能：

我们在 Red Hat Linux 下要更改的 TCP/IP 参数的默认设置是：

- 对于`tcp_fin_timeout`为`180`
- 对于`tcp_keepalive_time`为`7200`
- 对于`tcp_window_scaling`为`1`
- 对于`tcp_sack`为`1`
- 对于`tcp_timestamps`为`1`

- 要调整新的 TCP/IP 值，请在终端上输入以下命令：

### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# echo 30 > /proc/sys/net/ipv4/tcp_fin_timeout
[root@deep /]# echo 1800 > /proc/sys/net/ipv4/tcp_keepalive_time
[root@deep /]# echo 0 > /proc/sys/net/ipv4/tcp_window_scaling
[root@deep /]# echo 0 > /proc/sys/net/ipv4/tcp_sack
[root@deep /]# echo 0 > /proc/sys/net/ipv4/tcp_timestamps
```

**注意：**执行上述命令并将它们放入你的`/etc/rc.d/rc.local`文件中，这样你不必担心每次系统重启后再次输入它们。

### 在 Red Hat Linux 6.2 下

编辑`/etc/sysctl.conf`文件并添加以下行：

```ini
# 降低 tcp_fin_timeout 连接的默认时间值
net.ipv4.tcp_fin_timeout = 30
# 降低 tcp_keepalive_time 连接的默认时间值
net.ipv4.tcp_keepalive_time = 1800
# 关闭 tcp_window_scaling
net.ipv4.tcp_window_scaling = 0
# 关闭 tcp_sack
net.ipv4.tcp_sack = 0
# 关闭 tcp_timestamps
net.ipv4.tcp_timestamps = 0
```

你必须重启网络才能使更改生效。重启网络的命令如下：

- 要手动重启系统上的所有网络设备，使用以下命令：



```bash
[root@deep /]# /etc/rc.d/init.d/network restart
Setting network parameters                      [ OK ]
Bringing up interface lo                       [ OK ]
Bringing up interface eth0                     [ OK ]
Bringing up interface eth1                     [ OK ]
```

# 第五章 配置和构建安全、优化的内核

## 本章内容

- Linux 内核
- 制作紧急启动软盘
- 保护内核安全
- 内核配置
- 安装新内核
- 删除与模块相关的程序、文件和行
- 制作新的救援软盘
- 更新`/dev`条目

## Linux 内核

### 概述

嗯，我们的 Linux 服务器现在看起来初具规模了！但是等等，服务器最重要的部分是什么？是的，就是内核。Linux 内核是我们操作系统的核心，没有它就没有 Linux。所以我们必须照顾好我们的内核，并将其配置为适应我们的需求，只编译我们真正需要的功能。接下来要做的第一件事就是构建最适合你系统的内核。这很简单，但无论如何，请参阅`/usr/src/linux/`目录中的 README 文件。

配置内核时，只编译你需要和使用的代码。有四个主要原因：内核会更快（需要运行的代码更少），你会有更多内存（内核部分永远不会被交换到虚拟内存），更稳定（曾经探测过不存在的卡吗？），而不必要的部分可能被攻击者利用来访问本机或网络上的其他机器。模块也比直接编译进内核的支持慢。

在我们的配置和编译中，我们将构建一个单块内核。单块内核意味着只对问题回答`Yes`或`No`（不要做任何模块化的设置），并省略以下步骤：`make_modules`和`charged_modules_install`。此外，我们将用内核补丁中的缓冲区溢出保护来修补我们的新内核。

Linux 内核补丁存在，比如 Solar Designer 的非可执行栈补丁，它不允许在栈上执行代码，使得许多缓冲区溢出攻击更加困难——并完全击败了许多目前被全球“脚本小子”使用的漏洞利用。

如果你打算构建单块内核，请记住在配置新内核时只对问题回答`Yes`或`No`。如果你打算使用防火墙伪装功能或拨号`ppp`连接，则无法构建单块内核，因为这些功能需要构建一些模块，默认情况下。相反，请构建一个模块化内核。

新内核对你计算机硬件非常特定，在内核配置部分；我们对示例假设了以下硬件。当然，你必须将它们更改为适合你系统组件的配置。

- 1 个奔腾 II 400 MHz（i686）处理器
- 1 个 SCSI 主板
- 1 个 SCSI 硬盘
- 1 个 Adaptec AIC 7xxx SCSI 控制器
- 1 个 ATAPI IDE 光驱
- 1 个软盘驱动器
- 2 个 Intel EtherExpressPro 10/100 以太网卡
- 1 个 PS/2 鼠标

### 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为`/usr/src`。
- 安装已在 Red Hat Linux 6.1 和 6.2 上测试。
- 安装的所有步骤都将以超级用户账户`root`执行。
- 最新内核版本号为`2.2.14`。
- 最新安全 Linux 内核补丁版本号为`2_2_14-ow2`。

### 软件包

内核主页：[http://www.kernelnotes.org/](http://www.kernelnotes.org/)

你必须确保下载：`linux-2_2_14_tar.gz`

Kernel FTP 站点：`139.142.90.113`

安全 Linux 内核补丁主页：[http://www.openwall.com/linux/](http://www.openwall.com/linux/)

您务必下载：`linux-2_2_14-ow2_tar.gz`

安全 Linux 内核补丁 FTP 站点：`195.42.162.180`

## 制作紧急启动软盘

安装前的第一步是制作一张紧急启动软盘。Linux 有一个名为`mkbootdisk`的小工具可以简单完成此操作。第一步是查明当前使用的内核版本。查看您的`/etc/lilo.conf`文件，了解从哪个镜像启动，并由此镜像找出我们制作紧急启动软盘所需的内核版本。在我的示例中，我的`lilo.conf`文件中有以下内容：

```text
[root@deep /]# cat /etc/lilo.conf
boot=/dev/sda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
image=/boot/vmlinuz-2.2.12-20     ← 内核版本
    label=linux                       ← 我们从中启动的镜像
    root=/dev/sda6
    initrd=/boot/initrd-2.2.12-20.img
    read-only
```

现在您需要找到从中启动的镜像。在标准的全新首次安装中，它将是标记为`linux`的那个。在上面的示例中，我们显示该机器使用系统的`/boot/vmlinuz-2.2.12-20`原始内核版本启动。现在我们只需将一张格式化的 1.44 软盘放入系统中，并以`root`身份执行以下命令：

```text
[root@deep /]# mkbootdisk --device /dev/fd0 2.2.12-20
Insert a disk in /dev/fd0. Any information on the disk will be lost.
Press <Enter> to continue or ^C to abort:
```

按照这些指导，您现在将拥有一张带有已知可用内核的启动软盘，以防升级出现问题。我建议用该软盘重启系统，以确保软盘能正常工作。

## 卸载与优化

### 步骤 1

我们必须将内核的存档文件复制到`/usr/src`目录，并转到该目录。

```bash
[root@deep /]# cp linux-version_tar.gz /usr/src/
[root@deep /]# cd /usr/src/
```

### 如果您之前已经使用过 tar 存档安装过 Linux 内核

这些步骤仅适用于您之前已经使用过 tar 存档安装过 Linux 内核的情况。如果是首次全新安装 Linux 内核，则应卸载系统中的`kernel-headers-version.i386.rpm`、`kernel-version.i386.rpm`软件包。

- 使用以下命令删除 Linux 符号链接：

```bash
[root@deep src]# rm -rf linux
```

- 使用以下命令删除 Linux 内核头目录：

```bash
[root@deep src]# rm -rf linux-2.2.xx
```

- 使用以下命令删除 Linux 内核模块目录：

```bash
[root@deep src]# rm -rf /lib/modules/2.2.xx
```

**注意：** 仅当您之前安装过模块化内核版本时，才需要删除旧的内核模块。如果`lib`目录下不存在模块目录，那是因为您的旧内核版本不是模块化内核。

### 如果系统中安装的是原始内核的 RPM 软件包

如果系统中安装的是原始内核的 RPM 软件包而非 Linux 内核 tar 存档，因为您刚刚完成了新 Linux 系统的安装，或者之前曾使用 RPM 软件包升级过 Linux 系统，则使用以下命令卸载 Linux 内核：

- 您可以使用以下命令验证系统中是否安装了内核 RPM 软件包：

```text
[root@deep src]# rpm -qa | grep kernel
kernel-headers-2.2.xx.i386.rpm
kernel-2.2.xx.i386.rpm
```

- 要从命令行了解更多关于 Linux 内核的信息，请使用以下命令卸载 Linux 内核 RPM：

```text
[root@deep src]# rpm -e --nodeps kernel-headers kernel
cannot remove /usr/src/linux-2.2.xx - directory not empty
cannot remove /lib/modules/2.2.xx - directory not empty
[root@deep src]# rm -rf /usr/src/linux-2.2.xx/
[root@deep src]# rm -rf /lib/modules/2.2.xx/
```

在下面的步骤中，我们在卸载内核 RPM 后手动删除空的`/usr/src/linux-2.2.xx`和`/lib/modules/2.2.xx`目录（RPM 卸载程序不会完全删除这些目录）。

### 步骤 2：解压 Linux 内核存档

现在，我们必须解压内核的 tar 存档，并从系统中删除 Linux tar 存档。

```bash
[root@deep src]# tar xzpf linux-version_tar.gz
[root@deep src]# rm -f linux-version_tar.gz
```

### 步骤 3：增加任务数（优化）

要增加允许的任务数（每个用户的最大进程数），您可能需要编辑`/usr/src/linux/include/linux/tasks.h`文件并更改以下参数。

- 编辑`tasks.h`文件（`vi +14 /usr/src/linux/include/linux/tasks.h`）并更改以下参数：

```text
NR_TASKS 从 512 改为 3072
MIN_TASKS_LEFT_FOR_ROOT 从 4 改为 24
```

**注意：** `NR_TASKS`行中的值表示 Linux 内核为每个用户分配的最大任务（进程）句柄数。增加此数值将使您的服务器能够处理更多来自客户端的连接（例如：HTTP Web 服务器将能够为更多客户端连接提供服务）。

此外，Linux 防止为普通用户分配所有进程槽。有一个名为`MIN_TASKS_LEFT_FOR_ROOT`的特殊参数行，专为用户`root`保留，您可以为其设置保留给`root`的进程数量（24 是一个不错的值）。

### 步骤 4：优化内核

要使 Linux 内核适合您的特定 CPU 架构和优化标志，您可能需要编辑`/usr/src/linux/Makefile`文件并更改以下参数。

- 编辑`Makefile`文件（`vi +18 /usr/src/linux/Makefile`）并更改以下行：

```make
HOSTCC =gcc
```

改为：

```make
HOSTCC =egcs
```

- 编辑`Makefile`文件（`vi +25 /usr/src/linux/Makefile`）并更改以下行：

```make
CC =$(CROSS_COMPILE)gcc -D__KERNEL__ -I$(HPATH)
```

改为：

```make
CC =$(CROSS_COMPILE)egcs -D__KERNEL__ -I$(HPATH)
```

- 编辑`Makefile`文件（`vi +90 /usr/src/linux/Makefile`）并更改以下行：

```make
CFLAGS = -Wall -Wstrict-prototypes -O2 -fomit-frame-pointer
```

改为：

```make
CFLAGS = -Wall -Wstrict-prototypes -O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions
```

- 编辑`Makefile`文件（`vi +19 /usr/src/linux/Makefile`）并更改以下行：

```make
HOSTCFLAGS =-Wall -Wstrict-prototypes -O2 -fomit-frame-pointer
```

改为：

```make
HOSTCFLAGS =-Wall -Wstrict-prototypes -O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions
```

这些更改开启了激进的优化技巧，这些技巧可能适用于也可能不适用于所有内核。请注意，如果上述优化标志，或者您为 CPU 架构选择的优化标志对您不起作用，请不要试图绝对强制让它工作。我不想让您的系统像微软 Windows 那样变得不稳定。

## 加固内核

来自 Openwall 项目的安全 Linux 内核补丁是防止堆栈缓冲区溢出等攻击的好方法。Openwall 补丁是一组面向 Linux 内核的安全相关功能，全部可以通过将添加到您新 Linux 内核中的新“Security options”配置部分进行配置。此补丁可能因版本而异，某些版本可能包含各种其他安全修复。

**补丁版本`linux-2_2_14-ow2_tar.gz`的新功能包括：**

- 不可执行的用户栈区域
-`/tmp`中受限制的链接
-`/tmp`中受限制的 FIFO
- 受限制的`/proc`
- 对 fd 0、1 和 2 的特殊处理
- 在`execve(2)`上强制执行`RLIMIT_NPROC`
- 销毁未使用的共享内存段

**注意：** 应用`linux-2_2_14-ow2`补丁时，将在内核配置的末尾添加一个新的“Security options”部分。有关此补丁提供的不同功能的更多信息和说明，请参阅随补丁源代码一起提供的 README 文件。

## 应用补丁

```bash
[root@deep /]# cp linux-2_2_14-ow2_tar.gz /usr/src/
[root@deep /]# cd /usr/src/
[root@deep src]# LINUXCNC - 中文社区翻译wiki中文文档翻译 - LinuxCNC/Wiki
[root@deep src]# tar xzpf linux-2_2_14-ow2_tar.gz
[root@deep src]# cd linux-2.2.14-ow2/
[root@deep linux-2.2.14-ow2]# mv linux-2.2.14-ow2.diff /usr/src/
[root@deep linux-2.2.14-ow2]# cd ..
[root@deep src]# patch -p0 < linux-2.2.14-ow2.diff
[root@deep src]# rm -rf linux-2.2.14-ow2
[root@deep src]# rm -f linux-2.2.14-ow2.diff
[root@deep src]# rm -f linux-2_2_14-ow2_tar.gz
```

首先我们将程序存档复制到`/usr/src`目录，然后我们转到`/usr/src`目录并解压`linux-2_2_14-ow2_tar.gz`存档。接着我们转到新解压的 Linux 补丁目录，将包含补丁的文件`linux-2.2.14-ow2.diff`移到`/usr/src`，返回到`/usr/src`并使用文件`linux-2.2.14-ow2.diff`为我们的内核打补丁。之后，我们删除所有与补丁相关的文件。

**注意：** 所有与`linux-2.2.14-ow2`补丁相关的安全消息，如不可执行栈部分，都应记录到`/var/log/messages`日志文件中。

为新内核打补丁的步骤已完成。现在请按照本安装的其余部分构建 Linux 内核并重启。

## 编译

重要的是要确保您的`/usr/include/asm`、`usr/include/linux`和`/usr/include/scsi`子目录只是指向内核源代码的符号链接。

### 步骤 1

`asm`、`linux供水`和`scsi`子目录是指向我们 Linux 架构所需的真实包含内核源码头目录的软链接，例如`asm`对应`/usr/src/linux/include/asm-i386`。

- 在终端上输入以下命令：

```bash
[root@deep src]# cd /usr/include/
[root@deep include]# rm -rf asm linux scsi
[root@deep include]# ln -s /usr/src/linux/include/asm-i386 asm
[root@deep include]# ln -s /usr/src/linux/include/linux linux
[root@deep include]# ln -s /usr/src/linux/include/scsi scsi
```

这是配置中非常重要的一部分：我们删除`/usr/include`下的`asm`、`linux`和`scsi`目录，然后建立新的链接，指向新 Linux 内核源代码版本目录下的同名目录。`include`目录包含了 Linux 内核和程序在您的系统上编译所需的重要头文件。

### 步骤 2

确保没有陈旧的`.o`文件和依赖关系残留。

- 在终端上输入以下命令：

```bash
[root@deep include]# cd /usr/src/linux/
```

```bash
[root@deep linux]# make mrproper
```

注意：以上两个步骤只是清理开发团队在源代码树中可能意外遗留的内容。

你现在应该已经正确安装好了源代码。你可以通过三种方式之一来配置 Linux 内核。第一种方法是使用`make config`命令。它提供一个基于文本的界面，用于回答所有配置选项。系统会提示你所有需要设置的选项来配置你的内核。



第二种方法是使用`make menuconfig`命令，它在一个易于使用的菜单中提供所有内核选项。第三种是使用`make xconfig`命令，它提供一个完整的图形界面来配置所有内核选项。

## 第三步

在本章的配置中，你将使用`make config`命令，因为我们尚未在Linux服务器上安装XFree86窗口界面。

- 在终端中输入以下命令来加载内核配置：



```text
[root@deep /]# cd /usr/src/linux/（如果你还没有进入此目录）。
[root@deep linux]# make config
rm -f include/asm
( cd include ; ln -sf asm-i386 asm)
/bin/sh scripts/Configure arch/i386/config.in
#
# Using defaults found in arch/i386/defconfig
#

# 内核配置

# 代码成熟度级别选项

Prompt for development and/or incomplete code/drivers (CONFIG_EXPERIMENTAL) [N/y/?]

# 处理器类型和功能

Processor family (386, 486/Cx486, 586/K5/5x86/6x86, Pentium/K6/TSC, PPro/6x86MX) [PPro/6x86MX]
Maximum Physical Memory (1GB, 2GB) [1GB]
Math emulation (CONFIG_MATH_EMULATION) [N/y/?]
MTRR (Memory Type Range Register) support (CONFIG_MTRR) [N/y/?]
Symmetric multi-processing support (CONFIG_SMP) [Y/n/?] N

# 可加载模块支持

Enable loadable module support (CONFIG_MODULES) [Y/n/?] N

# 通用设置

Networking support (CONFIG_NET) [Y/n/?]
PCI support (CONFIG_PCI) [Y/n/?]
PCI access mode (BIOS, Direct, Any) [Any]
PCI quirks (CONFIG_PCI_QUIRKS) [Y/n/?] N
Backward-compatible /proc/pci (CONFIG_PCI_OLD_PROC) [Y/n/?] N
MCA support (CONFIG_MCA) [N/y/?]
SGI Visual Workstation support (CONFIG_VISWS) [N/y/?]
System V IPC (CONFIG_SYSVIPC) [Y/n/?]
BSD Process Accounting (CONFIG_BSD_PROCESS_ACCT) [N/y/?]
Sysctl support (CONFIG_SYSCTL) [Y/n/?]
Kernel support for a.out binaries (CONFIG_BINFMT_AOUT) [Y/n/?]
Kernel support for ELF binaries (CONFIG_BINFMT_ELF) [Y/n/?]
- Kernel support for MISC binaries (CONFIG_BINFMT_MISC) [Y/n/?]
- Parallel port support (CONFIG_PARPORT) [N/y/?]
- Advanced Power Management BIOS support (CONFIG_APM) [N/y/?]

# 即插即用支持

- Plug and Play support (CONFIG_PNP) [N/y/?]

# 块设备

- Normal PC floppy disk support (CONFIG_BLK_DEV_FD) [Y/n/?]
- Enhanced IDE/MFM/RLL disk/cdrom/tape/floppy support (CONFIG_BLK_DEV_IDE) [Y/n/?]
- Use old disk-only driver on primary interface (CONFIG_BLK_DEV_HD_IDE) [N/y/?]
- Include IDE/ATA-2 DISK support (CONFIG_BLK_DEV_IDEDISK) [Y/n/?]
- Include IDE/ATAPI CDROM support (CONFIG_BLK_DEV_IDECD) [Y/n/?]
- Include IDE/ATAPI TAPE support (CONFIG_BLK_DEV_IDETAPE) [N/y/?]
- Include IDE/ATAPI FLOPPY support (CONFIG_BLK_DEV_IDEFLOPPY) [N/y/?]
- SCSI emulation support (CONFIG_BLK_DEV_IDESCSI) [N/y/?]
- CMD640 chipset bugfix/support (CONFIG_BLK_DEV_CMD640) [Y/n/?] `N`
- RZ1000 chipset bugfix/support (CONFIG_BLK_DEV_RZ1000) [Y/n/?] `N`
- Generic PCI IDE chipset support (CONFIG_BLK_DEV_IDEPCI) [Y/n/?]
- Generic PCI bus-master DMA support (CONFIG_BLK_DEV_IDEDMA) [Y/n/?]
- Boot off-board chipsets first support (CONFIG_BLK_DEV_OFFBOARD) [N/y/?]
- Use DMA by default when available (CONFIG_IDEDMA_AUTO) [Y/n/?]
- Other IDE chipset support (CONFIG_IDE_CHIPSETS) [N/y/?]
- Loopback device support (CONFIG_BLK_DEV_LOOP) [N/y/?]
- Network block device support (CONFIG_BLK_DEV_NBD) [N/y/?]
- Multiple devices driver support (CONFIG_BLK_DEV_MD) [N/y/?]
- RAM disk support (CONFIG_BLK_DEV_RAM) [N/y/?]
- XT hard disk support (CONFIG_BLK_DEV_XD) [N/y/?]
- Mylex DAC960/DAC1100 PCI RAID Controller support (CONFIG_BLK_DEV_DAC960) [N/y/?] (NEW)
- Parallel port IDE device support (CONFIG_PARIDE) [N/y/?]
- Compaq SMART2 support (CONFIG_BLK_CPQ_DA) [N/y/?] (NEW)

# 网络选项

- Packet socket (CONFIG_PACKET) [Y/n/?]
- Kernel/User netlink socket (CONFIG_NETLINK) [N/y/?]
- Network firewalls (CONFIG_FIREWALL) [N/y/?] `Y`
- Socket Filtering (CONFIG_FILTER) [N/y/?]
- Unix domain sockets (CONFIG_UNIX) [Y/n/?]
- TCP/IP networking (CONFIG_INET) [Y/n/?]
- IP: multicasting (CONFIG_IP_MULTICAST) [N/y/?]
- IP: advanced router (CONFIG_IP_ADVANCED_ROUTER) [N/y/?]
- IP: kernel level autoconfiguration (CONFIG_IP_PNP) [N/y/?]
- IP: firewalling (CONFIG_IP_FIREWALL) [N/y/?] (NEW) `Y`
- IP: transparent proxy support (CONFIG_IP_TRANSPARENT_PROXY) [N/y/?] (NEW)
- IP: masquerading (CONFIG_IP_MASQUERADE) [N/y/?] (NEW)
- IP: optimize as router not host (CONFIG_IP_ROUTER) [N/y/?]
- IP: tunneling (CONFIG_NET_IPIP) [N/y/?]
- IP: GRE tunnels over IP (CONFIG_NET_IPGRE) [N/y/?]
- IP: aliasing support (CONFIG_IP_ALIAS) [N/y/?]
- IP: TCP syncookie support (not enabled per default) (CONFIG_SYN_COOKIES) [N/y/?] `Y`
- IP: Reverse ARP (CONFIG_INET_RARP) [N/y/?]
- IP: Allow large windows (not recommended if <16Mb of memory) (CONFIG_SKB_LARGE) [Y/n/?]
- The IPX protocol (CONFIG_IPX) [N/y/?]
- Appletalk DDP (CONFIG_ATALK) [N/y/?]

# 电话支持

- Linux telephony support (CONFIG_PHONE) [N/y/?] (NEW)

# SCSI 支持

- SCSI support (CONFIG_SCSI) [Y/n/?]
- SCSI disk support (CONFIG_BLK_DEV_SD) [Y/n/?]
- SCSI tape support (CONFIG_CHR_DEV_ST) [N/y/?]
- SCSI CD-ROM support (CONFIG_BLK_DEV_SR) [N/y/?]
- SCSI generic support (CONFIG_CHR_DEV_SG) [N/y/?]
- Probe all LUNs on each SCSI device (CONFIG_SCSI_MULTI_LUN) [Y/n/?] `N`
- Verbose SCSI error reporting (kernel size +=12K) (CONFIG_SCSI_CONSTANTS) [Y/n/?] `N`
- SCSI logging facility (CONFIG_SCSI_LOGGING) [N/y/?]

## SCSI 底层驱动

- 7000FASST SCSI support (CONFIG_SCSI_7000FASST) [N/y/?]
- ACARD SCSI support (CONFIG_SCSI_ACARD) [N/y/?]
- Adaptec AHA152X/2825 support (CONFIG_SCSI_AHA152X) [N/y/?]
- Adaptec AHA1542 support (CONFIG_SCSI_AHA1542) [N/y/?]
- Adaptec AIC7xxx support (CONFIG_SCSI_AIC7XXX) [N/y/?] `Y`
- Enable Tagged Command Queuing (TCQ) by default [N/y/?] (NEW) `Y`
- Maximum number of TCQ commands per device (CONFIG_AIC7XXX_CMDS_PER_DEVICE) [8] (NEW)
- Collect statistics to report in /proc (CONFIG_AIC7XXX_PROC_STATS) [N/y/?] (NEW)
- Delay in seconds after SCSI bus reset (CONFIG_AIC7XXX_RESET_DELAY) [5] (NEW)
- IBM ServeRAID support (CONFIG_SCSI_IPS) [N/y/?] (NEW)
- AdvanSys SCSI support (CONFIG_SCSI_ADVANSYS) [N/y/?]
- Always IN2000 SCSI support (CONFIG_SCSI_IN2000) [N/y/?]
- AM53/79C974 PCI SCSI support (CONFIG_SCSI_AM53C974) [N/yuci/?]
- AMI MegaRAID support (CONFIG_SCSI_MEGARAID) [N/y/?]
- BusLogic SCSI support (CONFIG_SCSI_BUSLOGIC) [N/y/?]
- DTC3180/3280 SCSI support (CONFIG_SCSI_DTC3280) [N/y/?]
- EATA ISA/EISA/PCI (DPT and generic EATA/DMA) support (CONFIG_SCSI_EATA) [N/y/?]
- EATA-DMA [Obsolete] (DPT, NEC, AT&T, SNI, AST, Olivetti, Alphatronix) support (CONFIG_SCSI_EATA_DMA) [N/y/?]
- EATA-PIO (old DPT PM2001, PM2012A) support (CONFIG_SCSI_EATA_PIO) [N/y/?]
- Future Domain 16xx SCSI/AHA-2920A support (CONFIG_SCSI_FUTURE_DOMAIN) [N/y/?]
- GDT SCSI Disk Array Controller support (CONFIG_SCSI_GDTH) [N/y/?]
- Generic NCR5380/53c400 SCSI support (CONFIG_SCSI_GENERIC_NCR5380) [N/y/?]
- Initio 9100U(W) support (CONFIG_SCSI_INITIO) [N/y/?]
- Initio INI-A100U2W support (CONFIG_SCSI_INIA100) [N/y/?]
- NCR53c406a SCSI support (CONFIG_SCSI_NCR53C406A) [N/y/?]
- symbios 53c416 SCSI support (CONFIG_SCSI_SYM53C416) [N/y/?]
- Simple 53c710 SCSI support (Compaq, NCR machines) (CONFIG_SCSI_SIM710) [N/y/?] (NEW)
- NCR53c7,8xx SCSI support (CONFIG_SCSI_NCR53C7xx) [N/y/?]
- NCR53C8XX SCSI support (CONFIG_SCSI_NCR53C8XX) [N/y/?]
- SYM53C8XX SCSI support (CONFIG_SCSI_SYM53C8XX) [Y/n/?] `N`
- PAS16 SCSI support (CONFIG_SCSI_PAS16) [N/y/?]
- PCI2000 support (CONFIG_SCSI_PCI2000) [N/y/?]
- PCI2220i support (CONFIG_SCSI_PCI2220I) [N/y/?]
- PSI240i support (CONFIG_SCSI_PSI240I) [N/y/?]
- Qlogic FAS SCSI support (CONFIG_SCSI_QLOGIC_FAS) [N/y/?]
- Qlogic ISP SCSI support (CONFIG_SCSI_QLOGIC_ISP) [N/y/?]
- Qlogic ISP FC SCSI support (CONFIG_SCSI_QLOGIC_FC) [N/y/?]
- Seagate ST-02 and Future Domain TMC-8xx SCSI support (CONFIG_SCSI_SEAGATE) [N/y/?]
- Tekram DC390(T) and Am53/79C974 SCSI support (CONFIG_SCSI_DC390T) [N/y/?]
- Trantor T128/T128F/T228 SCSI support (CONFIG_SCSI_T128) [N/y/?]
- UltraStor 14F/34F support (CONFIG_SCSI_U14_34F) [N/y/?]
- UltraStor SCSI support (CONFIG_SCSI_U14_34F) [N/y/?]

## 网络设备支持

- Network device support (CONFIG_NETDEVICES) [Y/n/?]

## ARCnet 设备

- ARCnet support (CONFIG_ARCNET) [N/y/?]
- Dummy net driver support (CONFIG_DUMMY) [Y/n/?]
- EQL (serial line load balancing) support (CONFIG_EQUALIZER) [N/y/?]
- General Instruments Surfboard 1000 (CONFIG_NET_SB1000) [N/y/?] (NEW)

## 以太网（10 或 100Mbit）

- Ethernet (10 or 100Mbit) (CONFIG_NET_ETHERNET) [Y/n/?]

- 3COM 网卡 (CONFIG_NET_VENDOR_3COM) [N/y/?]
```



- AMD LANCE 和 PCnet（AT1500 和 NE2100）支持（`CONFIG_LANCE`）[N/y/?]
- Western Digital/SMC 网卡（`CONFIG_NET_VENDOR_SMC`）[N/y/?]
- Racal-Interlan（Micom）NI 网卡（`CONFIG_NET_VENDOR_RACAL`）[N/y/?]
- 其他 ISA 网卡（`CONFIG_NET_ISA`）[N/y/?]
- EISA、VLB、PCI 及板载控制器（`CONFIG_NET_EISA`）[Y/n/?]
- AMD PCnet32（VLB 和 PCI）支持（`CONFIG_PCNET32`）[N/y/?]
- Apricot Xen-II 板载以太网（`CONFIG_APRICOT`）[N/y/?]
- CS89x0 支持（`CONFIG_CS89x0`）[N/y/?]
- DM9102 PCI 快速以太网适配器支持（实验性）（`CONFIG_DM9102`）[N/y/?]（NEW）
- 通用 DECchip 和 DIGITAL EtherWORKS PCI/EISA（`CONFIG_DE4X5`）[N/y/?]
- DECchip Tulip（dc21x4x）PCI 支持（`CONFIG_DEC_ELCP`）[N/y/?]
- 旧版 DECchip Tulip（dc21x4x）PCI 支持（`CONFIG_DEC_ELCP_OLD`）[N/y/?]（NEW）
- Digi Intl. RightSwitch SE-X 支持（`CONFIG_DGRS`）[N/y/?]
- EtherExpressPro/100 支持（`CONFIG_EEXPRESS_PRO100`）[Y/n/?]
- PCI NE2000 支持（`CONFIG_NE2K_PCI`）[N/y/?]
- TI ThunderLAN 支持（`CONFIG_TLAN`）[N/y/?]
- VIA Rhine 支持（`CONFIG_VIA_RHINE`）[N/y/?]
- SiS 900/7016 PCI 快速以太网适配器支持（`CONFIG_SIS900`）[N/y/?]（NEW）
- 袖珍型和便携式适配器（`CONFIG_NET_POCKET`）[N/y/?]

## 以太网（1000 Mbit）

- SysKonnect SK-98xx 支持（`CONFIG_SK98LIN`）[N/y/?]（NEW）
- FDDI 驱动支持（`CONFIG_FDDI`）[N/y/?]
- PPP（点对点）支持（`CONFIG_PPP`）[N/y/?]
- SLIP（串行线路）支持（`CONFIG_SLIP`）[N/y/?]
- 无线局域网（非业余无线电）（`CONFIG_NET_RADIO`）[N/y/?]

## 令牌环设备

- 令牌环驱动支持（`CONFIG_TR`）[N/y/?]
- 光纤通道驱动支持（`CONFIG_NET_FC`）[N/y/?]（NEW）

## 广域网接口

- MultiGate（COMX）同步串行板支持（`CONFIG_COMX`）[N/y/?]（NEW）
- 帧中继 DLCI 支持（`CONFIG_DLCI`）[N/y/?]
- WAN 驱动（`CONFIG_WAN_DRIVERS`）[N/y/?]
- SBNI12-xx 支持（`CONFIG_SBNI`）[N/y/?]（NEW）

## 业余无线电支持

- 业余无线电支持（`CONFIG_HAMRADIO`）[N/y/?]

## IrDA 子系统支持

- IrDA 子系统支持（`CONFIG_IRDA`）[N/y/?]

## ISDN 子系统

- ISDN 支持（`CONFIG_ISDN`）[N/y/?]

## 旧式 CD-ROM 驱动程序（非 SCSI、非 IDE）

- 支持非 SCSI/IDE/ATAPI CD-ROM 驱动器（`CONFIG_CD_NO_IDESCSI`）[N/y/?]

## 字符设备

- 虚拟终端（`CONFIG_VT`）[Y/n/?]
- 虚拟终端控制台支持（`CONFIG_VT_CONSOLE`）[Y/n/?]
- 标准/通用（简易）串口支持（`CONFIG_SERIAL`）[Y/n/?]
- 串口控制台支持（`CONFIG_SERIAL_CONSOLE`）[N/y/?]
- 扩展简易串口驱动选项（`CONFIG_SERIAL_EXTENDED`）[N/y/?]
- 非标准串口支持（`CONFIG_SERIAL_NONSTANDARD`）[N/y/?]
- Unix98 PTY 支持（`CONFIG_UNIX98_PTYS`）[Y/n/?]
- 使用中的 Unix98 PTY 最大数量（0-2048）（`CONFIG_UNIX98_PTY_COUNT`）[256] 128
- 鼠标支持（非串口鼠标）（`CONFIG_MOUSE`）[Y/n/?]

## 鼠标

- ATIXL 总线鼠标支持（`CONFIG_ATIXL_BUSMOUSE`）[N/y/?]
- Logitech 总线鼠标支持（`CONFIG_BUSMOUSE`）[N/y/?]
- Microsoft 总线鼠标支持（`CONFIG_MS_BUSMOUSE`）[N/y/?]
- PS/2 鼠标（又称"辅助设备"）支持（`CONFIG_PSMOUSE`）[Y/n/?]
- C&T 82C710 鼠标端口支持（如 TI Travelmate 上）（`CONFIG_82C710_MOUSE`）[Y/n/?] N
- PC110 数字化仪板支持（`CONFIG_PC110_PAD`）[N/y/?]

## 游戏杆支持

- 游戏杆支持（`CONFIG_JOYSTICK`）[N/y/?]
- QIC-02 磁带支持（`CONFIG_QIC02_TAPE`）[N/y/?]
- 看门狗定时器支持（`CONFIG_WATCHDOG`）[N/y/?]
- `/dev/nvram` 支持（`CONFIG_NVRAM`）[N/y/?]
- 增强型实时时钟支持（`CONFIG_RTC`）[N/y/?]

## Video for Linux

- Video For Linux（`CONFIG_VIDEO_DEV`）[N/y/?]
- Double Talk PC 内置语音卡支持（`CONFIG_DTLK`）[N/y/?]

## Ftape，软盘磁带设备驱动程序

- Ftape（QIC-80/Travan）支持（`CONFIG_FTAPE`）[N/y/?]

## 文件系统

- 配额支持（`CONFIG_QUOTA`）[N/y/?] Y
- 内核自动挂载支持（`CONFIG_AUTOFS_FS`）[Y/n/?] N
- Amiga FFS 文件系统支持（`CONFIG_AFFS_FS`）[N/y/?]
- Apple Macintosh 文件系统支持（实验性）（`CONFIG_HFS_FS`）[N/y/?]
- DOS FAT 文件系统支持（`CONFIG_FAT_FS`）[N/y/?]
- ISO 9660 CD-ROM 文件系统支持（`CONFIG_ISO9660_FS`）[Y/n/?]
- Microsoft Joliet CD-ROM 扩展（`CONFIG_JOLIET`）[N/y/?]
- Minix 文件系统支持（`CONFIG_MINIX_FS`）[N/y/?]
- NTFS 文件系统支持（只读）（`CONFIG_NTFS_FS`）[N/y/?]
- OS/2 HPFS 文件系统支持（只读）（`CONFIG_HPFS_FS`）[N/y/?]
- `/proc` 文件系统支持（`CONFIG_PROC_FS`）[Y/n/?]
- 用于 Unix98 PTY 的 `/dev/pts` 文件系统（`CONFIG_DEVPTS_FS`）[Y/n/?]
- ROM 文件系统支持（`CONFIG_ROMFS_FS`）[N/y/?]
- 第二代扩展文件系统支持（`CONFIG_EXT2_FS`）[Y/n/?]
- System V 和 Coherent 文件系统支持（`CONFIG_SYSV_FS`）[N/y/?]
- UFS 文件系统支持（`CONFIG_UFS_FS`）[N/y/?]

## 网络文件系统

- Coda 文件系统支持（高级网络文件系统）（`CONFIG_CODA_FS`）[N/y/?]
- NFS 文件系统支持（`CONFIG_NFS_FS`）[Y/n/?] N
- SMB 文件系统支持（用于挂载 WfW 共享等）（`CONFIG_SMB_FS`）[N/y/?]
- NCP 文件系统支持（用于挂载 NetWare 卷）（`CONFIG_NCP_FS`）[N/y/?]

## 分区类型

- BSD disklabel（BSD 分区表）支持（`CONFIG_BSD_DISKLABEL`）[N/y/?]
- Macintosh 分区映射支持（`CONFIG_MAC_PARTITION`）[N/y/?]
- SMD disklabel（Sun 分区表）支持（`CONFIG_SMD_DISKLABEL`）[N/y/?]
- Solaris（x86）分区表支持（`CONFIG_SOLARIS_X86_PARTITION`）[N/y/?]

## 控制台驱动程序

- VGA 文本控制台（`CONFIG_VGA_CONSOLE`）[Y/n/?]
- 视频模式选择支持（`CONFIG_VIDEO_SELECT`）[N/y/?]
- 声卡支持（`CONFIG_SOUND`）[N/y/?]

*（安全选项仅在您使用 Openwall Project 补丁修补内核后才会显示。）*

## 安全选项

- 不可执行的用户栈区域（`CONFIG_SECURE_STACK`）[Y]
- 自动检测并模拟 GCC 跳板（`CONFIG_SECURE_STACK_SMART`）[Y]
- `/tmp` 中的受限链接（`CONFIG_SECURE_LINK`）[Y]
- `/tmp` 中的受限 FIFO（`CONFIG_SECURE_FIFO`）[Y]
- 受限制的 `/proc`（`CONFIG_SECURE_PROC`）[N] Y
- 对 fd 0、1 和 2 的特殊处理（`CONFIG_SECURE_FD_0_1_2`）[Y]
- 在 `execve(2)` 上强制执行 `RLIMIT_NPROC`（`CONFIG_SECURE_RLIMIT_NPROC`）[Y]
- 销毁未使用的共享内存段（`CONFIG_SECURE_SHM`）[N] Y

## 内核调试

- Magic SysRq 键（`CONFIG_MAGIC_SYSRQ`）[N/y/?]

现在，返回`/usr/src/linux/`目录（如果您尚未在该目录中）。您需要编译新内核。使用以下命令进行编译：

```bash
[root@deep linux]# make dep; make clean; make bzImage
```

这一行包含三个命令。`make dep`首先读取您的配置并构建相应的依赖关系树。此过程确定哪些内容需要编译，哪些不需要。下一步，`make clean`清除之前所有的编译痕迹，以避免将错误版本的某个功能绑定到内核中。最后，`make bzImage`执行内核的完整编译。

该过程完成后，内核将被压缩并准备安装到您的系统中。在安装新内核之前，我们必须确定是否需要编译相应的模块。这仅在您对上述内核配置中的"启用可加载模块支持（`CONFIG_MODULES`）"回答 Yes，并将某些选项编译为模块时才需要。在这种情况下，您必须执行以下命令：

- 要为您的内核编译相应的模块，请使用以下命令：

```bash
[root@deep linux]# make modules
[root@deep linux]# make modules_install
```

**注意**：`make modules`和`make modules_install`命令仅在您对上述内核配置中的"启用可加载模块支持（`CONFIG_MODULES`）"回答 Yes 时才需要。

## 安装新内核

1. 将内核源代码树中的文件`/usr/src/linux/arch/i386/boot/bzImage`复制到`/boot`目录，并为其指定一个合适的新名称。

```bash
[root@deep linux]# cp /usr/src/linux/arch/i386/boot/bzImage /boot/vmlinuz-kernel.version.number
```

**注意**：合适或推荐的新名称类似于`vmlinuz-2.2.14`，这一点很重要，因为如果您想使用`mkbootdisk`程序制作新的救援软盘或紧急启动软盘，该程序有一些特定要求，例如：需要`vmlinuz-2.2.14`而不是`vmlinuz-2.2.14.a`。

2. 从内核源码树中将文件`/usr/src/linux/System.map`复制到`/boot`目录，并为其指定一个合适的新名称。

```bash
[root@deep linux]# cp /usr/src/linux/System.map /boot/System.map-kernel.version.number
```

3. 进入`/boot`目录，并使用以下命令重建`vmlinuz`和`System.map`链接：

```bash
[root@deep linux]# cd /boot
[root@deep /boot]# ln -fs vmlinuz-kernel.version.number vmlinuz
[root@deep /boot]# ln -fs System.map-kernel.version.number System.map
```

我们必须重建`vmlinuz`和`System.map`的链接，使其指向新安装的内核版本。如果没有新的链接，LILO 程序将默认查找旧版本的 Linux 内核。

4. 删除`/boot`目录下过时的和不必要的文件以释放空间：

```bash
[root@deep /boot]# rm -f module-info
[root@deep /boot]# rm -f initrd-2.2.xx.img
```

`module-info`链接指向您原始内核的旧模块目录。由于我们已经安装了全新的内核，因此不需要保留这个损坏的链接。`initrd-2.2.xx`是一个包含初始 RAM 磁盘镜像的文件，在磁盘可用之前作为系统使用。该文件仅在您的系统装有 SCSI 适配器时，才会从 Linux 安装程序中安装。如果我们使用并拥有 SCSI 系统，由于我们已经构建了单体内核，该驱动现在将被整合到我们的新 Linux 内核中，因此我们可以安全地删除这个文件（`initrd-2.2.xx.img`）。

5. 创建一个新的 Linux 内核目录，用于处理与 Linux 内核相关的所有头文件，以便将来在您的系统上编译其他程序。

回想一下，我们之前在`/usr/include`目录下创建了三个符号链接，指向 Linux 内核，以便能够编译它而不会收到错误，也能编译未来的程序。`/usr/include`目录是您 Linux 系统中保留所有头文件以供参考和依赖的地方，当您编译和安装新程序时会用到。当程序需要了解内核安装版本相关的编译时特定函数时，会用到`asm`、`linux`和`scsi`这些链接。当程序必须了解您系统的特定信息、依赖关系等时，会在`include`目录中调用其他头文件。

```bash
[root@deep /]# mkdir -p /usr/src/linux-2.2.14/include
[root@deep /]# cp -r /usr/src/linux/include/asm-generic /usr/src/linux-2.2.14/include
[root@deep /]# cp -r /usr/src/linux/include/asm-i386 /usr/src/linux-2.2.14/include
[root@deep /]# cp -r /usr/src/linux/include/linux /usr/src/linux-2.2.14/include
[root@deep /]# cp -r /usr/src/linux/include/net /usr/src/linux-2.2.14/include
[root@deep /]# cp -r /usr/src/linux/include/video /usr/src/linux-2.2.14/include
[root@deep /]# cp -r /usr/src/linux/include/scsi /usr/src/linux-2.2.14/include
[root@deep /]# rm -rf /usr/src/linux
```

整个我们编译新内核的源码目录，我们在`/usr/src`下创建一个新的名为`linux`的符号链接，指向我们的新`/usr/src/linux-2.2.14/include`目录。通过这些步骤，将来编译的程序将知道在服务器上何处查找与内核相关的头文件。

**注意：**这一步将使我们节省硬盘空间并降低安全风险。Linux 内核源码目录包含大量文件，解压后大小约为 75 MB。通过上述步骤，我们的 Linux 内核目录大小变为约 3 MB，因此我们为相同的功能节省了 72 MB。

6. 最后，你需要编辑`/etc/lilo.conf`文件，使新内核成为启动选项之一。

### 步骤 1

编辑`lilo.conf`文件（`vi /etc/lilo.conf`），并适当修改读作`image=/boot/`的那一行：

```text
[root@deep /]# vi /etc/lilo.conf

boot=/dev/sda
map=/boot/map
install=/boot/boot.b
prompt
timeout=00
restricted
password=somepasswd
image=/boot/vmlinuz-kernel.version.number #(在此处添加您的新内核文件名).
  label=linux
  root=/dev/sda6
  read-only
```



**注意：** 不要忘记删除`lilo.conf`文件中读作`initrd=/boot/initrd-2.2.12-20.img`的那一行，因为这一行现在不再需要了（单体内核不需要`initrd`文件）。

## 步骤 2

当新内核版本的名称如上所示放入`lilo.conf`文件后，我们使用以下命令更新我们的`lilo.conf`文件以使更改生效：

```bash
[root@deep /]# /sbin/lilo -v
LILO version 21, [Copyright 1992-1998 Werner Almesberger

Reading boot sector from /dev/sda
Merging with /boot/boot.b
Boot image: /boot/vmlinuz-2.2.14
Added linux *
/boot/boot.0800 exists – no backup copy made.
Writing boot sector.
```

**重要提示：** 如果您在内核配置期间对配置选项`Unix98 PTY support (CONFIG_UNIX98_PTYS)`回答**否**，您必须编辑`/etc/fstab`文件并删除读作以下内容的行：

```text
none    /dev/pts    devpts    gid=5,mode=620    0 0
```

## 删除与模块相关的程序、文件和行

默认情况下，当您首次安装 Red Hat Linux 时（就像我们这样做），内核被构建为模块化内核。这意味着我们需要的每个设备或功能都以模块形式存在，并由名为`kmod`的内核守护进程程序控制，该程序会自动在需要时将一些模块和功能支持加载到内存中，并在不再使用时卸载它。

### 步骤 1

`kmod`和其他包含在`modutils` RPM 包中的模块管理程序使用位于`/etc`目录下的`conf.modules`文件来了解，例如，您使用哪种以太网卡，如果您的以太网卡需要特殊配置等等。由于我们在新编译的内核中不使用任何模块，我们可以删除`conf.modules`文件并完全卸载`modutils`软件包程序。

- 要删除`conf.modules`文件，使用以下命令：

  ```bash
  [root@deep /]# rm -f /etc/conf.modules
  ```

- 要卸载`modutils`软件包，使用以下命令：

  ```bash
  [root@deep /]# rpm -e --nodeps modutils
  ```

### 步骤 2

最后要做的是编辑文件`rc.sysinit`并注释掉所有与`depmod -a`相关的行，方法是在行首插入`#`。这是必需的，因为系统在启动时会读取`rc.sysinit`脚本来默认查找内核中的模块依赖关系。

### 在 Red Hat Linux 6.1 下

注释掉`rc.sysinit`文件中的第 260 行（`vi +260 /etc/rc.d/rc.sysinit`）：

```text
ivot注释此行，将：
if [ -x /sbin/depmod -a -n "$USEMODULES" ]; then
改为：
#if [ -x /sbin/depmod -a -n "$USEMODULES" ]; then
```

注释掉`rc.sysinit`文件中的第 272 至 277 行（`vi +272 /etc/rc.d/rc.sysinit`）：

```text
  if [ -L /lib/modules/default ]; then
    INITLOG_ARGS= action "Finding module dependencies" depmod -a default
  else
    INITLOG_ARGS= action "Finding module dependencies" depmod -a
  fi
fi
改为：
#  if [ -L /lib/modules/default ]; then
#    INITLOG_ARGS= action "Finding module dependencies" depmod -a default
#  else
#    INITLOG_ARGS= action "Finding module dependencies" depmod -a
#  fi
#fi
```

**注意：** 上述步骤涉及 Red Hat Linux 6.1 版本下的`initscripts-4.70-1`软件包。

### 在 Red Hat Linux 6.2 下

注释掉`rc.sysinit`文件中的第 243 行（`vi +243 /etc/rc.d/rc.sysinit`）：

注释掉`rc.sysinit`文件中的第 255 至 260 行（`vi +255 /etc/rc.d/rc.sysinit`）：

```text
ivot注释此行，将：
if [ -x /sbin/depmod -a -n "$USEMODULES" ]; then
改为：
#if [ -x /sbin/depmod -a -n "$USEMODULES" ]; then
```

注释掉`rc.sysinit`文件中的第 255 至 260 行（`vi +255 /etc/rc.d/rc.sysinit`）：

```text
  if [ -L /lib/modules/default ]; then
    INITLOG_ARGS= action "Finding module dependencies" depmod -a default
  else
    INITLOG_ARGS= action "Finding module dependencies" depmod -a
  fi
fi
改为：
#  if [ -L /lib/modules/default ]; then
#    INITLOG_ARGS= action " descentFounding module dependencies" depmod -a default
#  else
#    INITLOG_ARGS= action "Finding module dependencies" depmod -a
#  fi
#fi
```

**注意：** 再次强调，这一部分（“删除与模块相关的程序、文件和行”）只有您在上述内核配置中对`Enable loadable module support (CONFIG_MODULES)`回答**否**时才需要。

## 步骤 3

现在您必须**重新启动**您的系统并测试您的结果。

```bash
[root@deep /]# reboot
```

当系统重新启动并且您已登录后，使用以下命令验证新内核版本：

- 要验证您的新内核版本，使用以下命令：

  ```bash
  [root@deep /]# uname -a
  ```

  ```text
  Linux deep.openna.com 2.2.14 #1 Mon Jan 10 10:40:35 EDT 2000 i686 unknown
  ```

恭喜。

## 制作新的救援软盘

在您的 Linux 服务器重新启动后，您现在应该已经拥有了一个升级了内核的系统。因此，现在是时候用新内核制作一个新的救援镜像，以备将来紧急情况使用了。为此，请遵循下面简单的步骤：

- 以 root 身份登录，插入一张新软盘，然后执行以下命令：

  ```bash
  [root@deep /]# mkbootdisk --device /dev/fd0 2.2.14
  ```

  ```text
  Insert a disk in /dev/fd0. Any information on the disk will be lost.

  Press <Enter> to continue or ^C to abort:
  ```

**重要提示：**`mkbootdisk`程序仅在模块化内核上运行。因此您不能在单体内核上使用它；如果您的系统将来出现问题，请按如下所示创建一个紧急启动软盘。

## 制作紧急启动软盘

因为只有在模块化内核上才能创建救援软盘，所以当硬盘上的 Linux 内核损坏时，我们必须找到另一种方法来启动 Linux 系统。Linux 紧急启动软盘可以实现这一目的。你应该在成功启动系统并以 root 身份登录后立即创建它。

- 要创建紧急启动软盘，请按照以下步骤操作：

1. 插入软盘并使用以下命令进行格式化：

   ```bash
   [root@deep /]# fdformat /dev/fd0H1440
   ```

   ```text
   Double-sided, 80 tracks, 18 sec/track. Total capacity 1440 kB.

   Formatting ... done

   Verifying ... done
   ```

2. 将`/boot`目录中的`vmlinuz`文件复制到软盘：

   ```bash
   [root@deep /]# cp /boot/vmlinuz /dev/fd0
   ```

   ```text
   cp: overwrite `/dev/fd0'? y
   ```

3. 使用以下命令确定内核的根设备：

   ```bash
   [root@deep /]# rdev
   ```

   ```text
   /dev/sda12 /
   ```

4. 使用以下命令设置内核的根设备：

   ```bash
   [root@deep /]# rdev /dev/fd0 /dev/sda12
   ```

5. 使用以下命令将根设备标记为只读：

   ```bash
   [root@deep /]# rdev -R /dev/fd0 1
   ```

6. 现在将启动软盘放入 A: 驱动器，并使用以下命令重启系统：

   ```bash
   [root@deep /]# reboot
   ```

`vmlinuz`文件是一个指向实际 Linux 内核的符号链接。

内核的根设备是根文件系统所在的磁盘分区。在本示例中，根设备是`dev/sda12`；你系统上的设备名称可能不同。

要设置内核的根设备，请使用上一步中`rdev`命令工具报告的设备。

这将使 Linux 最初以只读方式挂载根文件系统。将根设备设置为只读可以避免出现若干警告和错误消息。

## 更新你的`/dev`条目

如果你向系统添加了新设备或最近进行了内核的重大升级（例如从内核版本 2.2.9 直接升级到 2.2.15），更新`/dev`条目可能非常重要，以避免与缺失设备相关的问题。我们可以通过`MAKEDEV`脚本工具来完成此任务，该工具会扫描`/dev`目录，该目录保存了所有与内核驱动程序接口的设备。一个名为`update`的特殊选项允许`MAKEDEV`工具创建你在内核中已配置的新设备，并删除那些不再配置的设备。

- 要更新你的`/dev`条目，请执行以下命令：

  ```bash
  [root@deep /]# cd /dev
  [root@deep /dev]# ./MAKEDEV update
  ```

# 第三部分 网络相关参考

本部分内容：

- TCP/IP 网络管理
- 网络防火墙
- 支持伪装和转发的网络防火墙

# 第 6 章 TCP/IP 网络管理

本章内容：

- 在每台机器上安装多个以太网卡
- 与网络功能相关的文件
- 使用命令行手动配置 TCP/IP 网络

## Linux TCP/IP 网络管理

### 概述

到目前为止，我们还没有涉及 Linux 的网络功能。Linux 是当今世界上网络特性最好的操作系统之一。全球大多数 Internet 站点对此早已了解，并已使用了一段时间。如果你想完全掌控服务器上发生的情况，了解你的硬件网络及其所有相关文件非常重要。熟练掌握基本的网络命令至关重要。网络管理涵盖广泛的主题。一般来说，它包括收集网络各部分的统计数据和状态信息，以及根据需要采取行动来处理故障和其他变化。

最原始的网络监控技术是定期对关键主机进行`ping`检测。更复杂的网络监控需要能够从网络上的各种设备获取特定的状态和统计信息。这些信息应包括各种类型的数据报计数，以及各类错误的计数。因此，在本章中，我们将尝试回答关于网络设备、与网络功能相关的文件以及基本网络命令的根本性问题。

## 在每台机器上安装多个以太网卡

你可以将 Linux 用作两个以太网网络之间的网关。在这种情况下，你的服务器上可能有两个以太网卡。为了避免启动时出现问题，Linux 内核不会自动检测多张网卡。如果你恰好有两张或更多网卡，你应该在`lilo.conf`文件中（用于单体内核）或`conf.modules`文件中（用于模块化内核）指定网卡的参数。以下是你可能遇到的网卡问题。

### 问题 1

如果网卡的驱动程序是作为可加载模块使用的（模块化内核），对于 PCI 驱动程序，模块通常会自动检测所有已安装的网卡。对于 ISA 网卡，你需要提供网卡的 I/O 基地址，以便模块知道在哪里查找。此信息存储在`/etc/conf.modules`文件中。

举个例子，假设我们有两张 ISA 3c509 网卡，一张位于 I/O 0x300，另一张位于 I/O 0x320。

对于 ISA 网卡，编辑`conf.modules`文件（`vi /etc/conf.modules`）并添加：

```text
alias eth0 3c509
alias eth1 3c509
options 3c509 io=0x300,0x320
```

这表示 3c509 驱动程序应为`eth0`或`eth1`加载（alias eth0, eth1），并且应使用选项`io=0x300,0x320`加载，以便驱动程序知道在哪里查找网卡。注意 0x 是必须的——DOS 世界中常用的 300h 这样的写法是不起作用的。

对于 PCI 网卡，你通常只需要 alias 行来将`ethN`接口与相应的驱动程序名称关联起来，因为 PCI 网卡的 I/O 基地址可以被安全地检测到。

对于 PCI 网卡，编辑`conf.modules`文件（`vi /etc/conf.modules`）并添加：

```text
alias eth0 3c509
alias eth1 3c509
```

如果网卡的驱动程序已编译进内核（单体内核），PCI 探测将自动找到所有相关网卡。ISA 网卡也会自动找到所有相关网卡，但在某些情况下 ISA 网卡仍然需要执行以下操作。此信息存储在`/etc/lilo.conf`文件中。方法是向内核传递启动时参数，这通常通过 LILO 来完成。

对于 ISA 网卡，编辑`lilo.conf`文件（`vi /etc/lilo.conf`）并添加：

```text
append="ether=0,0,eth1"
```

**注意：** 请先在不使用`lilo.conf`文件中启动时参数的情况下测试你的 ISA 网卡，如果失败再使用启动时参数。

在这种情况下，`eth0`和`eth1`将按照启动时网卡被发现的顺序分配。由于我们已经重新编译了内核，必须使用第二种方法（如果驱动程序已编译进内核）来安装系统上的第二块以太网卡。请记住，这只在某些情况下对 ISA 网卡是必需的，PCI 网卡会自动被检测到。

## 与网络功能相关的文件

在 Linux 中，TCP/IP 网络通过几个文本文件进行配置，你可能需要编辑这些文件才能使网络正常工作。了解与 TCP/IP 网络相关的配置文件非常重要，以便在必要时进行编辑和配置。请记住，我们的服务器没有 Xwindow 界面来通过图形界面配置文件。即使你在日常活动中使用 GUI，了解如何在文本模式下配置网络也很重要。以下各节描述基本的 TCP/IP 配置文件。

### `/etc/HOSTNAME`文件

此文件存储你的系统主机名——即系统的完全限定域名（FQDN），例如`deep.openna.com`。

以下是`/etc/HOSTNAME`文件的示例：

```text
deep.openna.com
```

### `/etc/sysconfig/network-scripts/ifcfg-ethN`文件

你系统上已有或想要添加的每个网络设备的配置文件位于 Red Hat Linux 6.1 或 6.2 的`/etc/sysconfig/network-scripts/`目录中，第一个接口命名为`ifcfg-eth0`，第二个命名为`ifcfg-eth1`，以此类推。

以下是`/etc/sysconfig/network-scripts/ifcfg-eth0`文件的示例：

```text
DEVICE=eth0
IPADDR=208.164.186.1
NETMASK=255.255.255.0
NETWORK=208.164.186.0
BROADCAST=208.164.186.255
ONBOOT=yes
BOOTPROTO=none
USERCTL=no
```

如果你想手动修改网络地址，或在新接口上添加新网络，请编辑此文件（`ifcfg-ethN`），或创建一个新文件并进行相应修改。

`DEVICE`=`devicename`，其中`devicename`是物理网络设备的名称。

`IPADDR`=`ipaddr`，其中`ipaddr`是 IP 地址。

`NETMASK`=`netmask`，其中`netmask`是子网掩码 IP 值。

`NETWORK`=`network`，其中`network`是网络 IP 地址。

`BROADCAST`=`broadcast`，其中`broadcast`是广播 IP 地址。

`ONBOOT`=`answer`，其中`answer`是`yes`或`no`（接口在启动时是否激活）。

`BOOTPROTO`=`proto`，其中`proto`是以下选项之一：

- `none` - 不应使用引导时协议。
- `bootp` - 应使用 bootp（现为 pump）协议。
- `dhcp` - 应使用 dhcp 协议。

`USERCTL`=`answer`，其中`answer`是以下选项之一：

- `yes`（允许非 root 用户控制此设备）。
- `no`（仅允许超级用户 root 控制此设备）。

## `/etc/resolv.conf`文件

此文件是另一个文本文件，由解析器使用——这是一个用于确定主机名对应 IP 地址的库。

以下是`/etc/resolv.conf`文件的示例：

```text
search openna.com
nameserver 208.164.186.1
nameserver 208.164.186.2
```

**注意：** 名称服务器按照它们在文件中出现的顺序进行查询（主、次）。

## `/etc/host.conf`文件

此文件指定如何解析名称。Linux 使用解析器库来获取与主机名对应的 IP 地址。



以下是`/etc/host.conf`文件的示例：

```text
# 首先通过 DNS 查找名称，然后回退到 /etc/hosts。
order bind,hosts
# 我们有多个地址的机器。
multi on
# 检查 IP 地址欺骗。
nospoof on
```

`order`选项表示服务的顺序。示例条目指定解析器库应首先查询名称服务器（DNS）来解析名称，然后检查`/etc/hosts`文件。

`multi`选项确定`/etc/hosts`文件中的主机是否可以具有多个 IP 地址（多个接口`ethN`）。具有多个 IP 地址的主机被称为*多宿主*主机，因为存在多个 IP 地址意味着该主机具有多个网络接口。

`nospoof`选项表示注意不允许在此机器上进行欺骗。IP 欺骗是一种安全漏洞利用，它通过欺骗信任关系中的计算机，让它们认为你是你实际上不是的人。

## `/etc/sysconfig/network`文件

`/etc/sysconfig/network`文件用于指定服务器上所需网络配置的信息。

以下是`/etc/sysconfig/network`文件的示例：

```text
NETWORKING=yes
FORWARD_IPv4=yes
HOSTNAME=deep.openna.com
GATEWAY=0.0.0.0
GATEWAYDEV=
```

可以使用以下值：

- `NETWORKING=answer`，其中`answer`是`yes`或`no`（配置网络或不配置网络）。
- `FORWARD_IPv4=answer`，其中`answer`是`yes`或`no`（执行 IP 转发或不执行 IP 转发）。
- `HOSTNAME=hostname`，其中`hostname`是你的服务器主机名。
- `GATEWAY=gwip`，其中`gwip`是远程网络网关的 IP 地址（如果有）。
- `GATEWAYDEV=gwdev`，其中`gwdev`是你用于访问远程网关的设备名称（`eth#`）。

> **注意：** 为了与旧软件兼容，`/etc/HOSTNAME`文件应包含与上面的`HOSTNAME=hostname`相同的值。对于新版本的 Red Hat Linux 6.2，`FORWARD_IPv4=`参数现在在`/etc/sysctl.conf`文件中指定，而不是在`/etc/sysconfig/network`文件中。

## `/etc/sysctl.conf`文件

在 Red Hat Linux 6.2 中，许多与网络安全相关的内核选项，例如丢弃来自不应接收的接口的数据包或忽略 ping/广播请求等，现在可以在新的`/etc/sysctl.conf`文件中设置，而不是在`/etc/rc.d/rc.local`文件中。一个重要的考虑是 IPv4 转发参数，现在通过`sysctl`程序完成，而不是由`/etc/sysconfig/network`文件中的内容控制。sysctl 设置存储在`/etc/sysctl.conf`中，并在每次启动时加载，在加载`/etc/rc.d/rc.local`文件之前加载。我们已经在第 3 章“Linux 常规安全”中讨论过必须在服务器中设置的所有网络安全参数，因此我们将只关注 IPv4 转发的内核选项。

- 要在 RH 6.2 系统上启用 IPv4 转发，请使用以下命令：

  编辑`/etc/sysctl.conf`文件并添加以下行：

  ```text
  # 启用数据包转发
  net.ipv4.ip_forward = 1
  ```

你必须重新启动网络才能使更改生效。重新启动网络的命令如下：

- 要手动重新启动系统上的所有网络设备，请使用以下命令：

  ```text
  [root@deep /]# /etc/rc.d/init.d/network restart
  Setting network parameters          [ OK ]
  Bringing up interface lo            [ OK ]
  Bringing up interface eth0          [ OK ]
  Bringing up interface eth1          [ OK ]
  ```

> **注意：** 通过`sysctl.conf`文件启用 IPv4 转发仅适用于 Red Hat Linux 6.2 用户。使用 Red Hat 6.1 版本的用户必须将此参数设置在`/etc/sysconfig/network`文件中，如上所述。

## `/etc/hosts`文件

在启动机器时，在可以引用 DNS 之前，它需要知道某些主机名到 IP 地址的映射。此映射保存在`/etc/hosts`文件中。在没有名称服务器的情况下，系统上的任何网络程序都会查阅此文件来确定与主机名对应的 IP 地址。

以下是`/etc/hosts`文件的示例：

| IP 地址 | 主机名 | 别名 |
|---|---|---|
| 127.0.0.1 | localhost | deep.openna.com |
| 208.164.186.1 | deep.openna.com | deep |
| 208.164.186.2 | mail.openna.com | mail |
| 208.164.186.3 | web.openna.com | web |

最左边的列是要解析的 IP 地址。下一列是该主机的名称。任何后续列都是该主机的别名。例如，在第二行中，IP 地址 208.164.186.1 对应的主机是 deep.openna.com。deep.openna.com 的另一个名称是 deep。

完成网络文件配置后，不要忘记重新启动网络以使更改生效。

- 要重新启动网络，请使用以下命令：

  ```text
  [root@deep /]# /etc/rc.d/init.d/network restart
  Setting network parameters          [ OK ]
  Bringing up interface lo            [ OK ]
  Bringing up interface eth0          [ OK ]
  Bringing up interface eth1          [ OK ]
  ```

> **重要提示：** `telnet`或`ftp`连接的超时问题通常是由于服务器尝试将客户端 IP 地址解析为 DNS 名称引起的。要么服务器上的 DNS 配置不正确，要么客户端机器对 DNS 不可见。如果你打算在服务器上运行 telnet 或 ftp 服务，并且不使用 DNS，请不要忘记在服务器的`/etc/hosts`文件中添加客户端机器的名称和 IP，否则你可能需要等待几分钟让 DNS 查找超时，然后才会出现`login:`提示符。

## 使用命令行手动配置 TCP/IP 网络

`ifconfig`工具是用于设置和配置网卡的工具。在需要手动配置网络时，你应该了解此命令。需要注意的一个重要事项是，使用`ifconfig`配置网络设备时，设置不会在重启后保留。

- 要为`eth0`接口分配 IP 地址 208.164.186.2，请使用以下命令：

  ```text
  [root@deep /]# ifconfig eth0 208.164.186.2 netmask 255olo503255.0
  ```

**注意**：通常，人们手动配置或更改 TCP/IP 网络只是为了在服务器上进行一些测试。如果你想保留 TCP/IP 值，最好将它们设置在相关的网络功能文件中。

- 要显示服务器上的所有接口，请使用以下命令：

  ```text
  [root@deep /]# ifconfig
  ```

输出应类似于：

```text
eth0  Link encap:Ethernet HWaddr 00:E0:18:90:1B:56
      inet addr:208.164.186.2 Bcast:208.164.186.255 Mask:255.255.255.0
      UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
      RX packets:1295 errors:0 dropped:0 overruns:0 frame:0
      TX packets:1163 errors:0 dropped:0 overruns:0 carrier:0
      collisions:0 txqueuelen:100
      Interrupt:11 Base address:0xa800

lo    Link encap:Local Loopback
      inet addr:127.0.0.1 Mask:255.0.0.0
      UP LOOPBACK RUNNING MTU:3924 Metric:1
      RX packets:139 errors:0 dropped:0 overruns:0 frame:0
      TX packets:139 errors:0 dropped:0 overruns:0 carrier:0
      collisions:0 txqueuelen:0
```

**注意**：如果`ifconfig`工具不带任何参数调用，它会显示你配置的所有接口。`-a`选项也会显示不活动的接口。

- 要显示所有接口以及你可能拥有的不活动接口，请使用以下命令：

  ```text
  [root@deep /]# ifconfig -a
  ```

输出应类似于：

```text
eth0  Link encap:Ethernet HWaddr 00:E0:18:90:1B:56
      inet addr:208.164.186.2 Bcast:208.164.186.255 Mask:255.255.255.0
      UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
      RX packets:1295 errors:0 dropped:0 overruns:0 frame:0
      TX packets:1163 errors:0 dropped:0 overruns:0 carrier:0
      collisions:0 txqueuelen:100
      Interrupt:11 Base address:0xa800

eth1  Link encap:Ethernet HWaddr 00:E0:18:90:1B:56
      inet addr:192.168.1.1 Bcast:192.168.1.255 Mask:255.255.255.0
      UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
      RX packets:1295 errors:0 dropped:0 overruns:0 frame:0
      TX packets:1163 errors:0 dropped:0 overruns:0 carrier:0
      collisions:0 txqueuelen:100
      Interrupt:5 Base address:0xa320

lo    Link encap:Local Loopback
      inet addr:127.0.0.1 Mask:255.0.0.0
      UP LOOPBACK RUNNING MTU:3924 Metric:1
      RX packets:139 errors:0 dropped:0 overruns:0 frame:0
      TX packets:139 errors:0 dropped:0 overruns:0 carrier:0
      collisions:0 txqueuelen:0
```

**注意**：需要特别注意的是，使用`ifconfig`工具为网络设备配置的设置在重启后将不会保留。

- 要为 208.164.186.1 分配默认网关，请使用以下命令：

  ```text
  [root@deep /]# route add default gw 208.164.186.1
  ```

**注意**：在此示例中，默认路由被设置为指向 208.164.186.1，即你的路由器。同样，如果你想保留默认网关值，最好将其设置在与网络功能相关的文件中（`/etc/sysconfig/network`）。

验证你可以连接到主机。从你的网络中选择一个主机，例如 208.164.186.1。

- 要验证你可以连接到主机，请使用以下命令：

  ```text
  [root@deep /]# ping 208.164.186.1
  ```

输出应类似于以下内容：

```text
[root@deep networking]# ping 208.164.186.1
PING 208.164.186.1 (208.164.186.1) from 208.164.186.2 : 56 data bytes
64 bytes from 208.164.186.2: icmp_seq=0 ttl=128 time=1.0 ms
64 bytes from 208.164.186.2: icmp_seq=1 ttl=128 time=1.0 ms
64 bytes from 208.164.186.2: icmp_seq=2 ttl=128 time=1.0 ms
64 bytes from 208.164.186.2: icmp_seq=3 ttl=128 time=1.0 ms

--- 208.164.186.1 ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 1.0/1.0 SMTP command timeout: 30000 ms 
```

你现在应该使用`route`命令显示路由信息，以查看两个主机是否具有正确的路由条目：

- 要显示路由信息，请使用以下命令：

  ```text
  [root@deep /]# route -n
  ```

输出应类似于以下内容：

```text
Kernel IP routing table
Destination   Gateway      Genmask         Flags Metric Ref Use Iface
208.164.186.2 0.0.0.0      255.255.255.255 UH    0      0   0   eth0
208.164.186.0 208.164.186.2 255.255.255.0  UG    0      0   0   eth0
208.164.186.0 0.0.0.0      255.255.255.0   U     0      0   0   eth0
127.0.0.0     0.0.0.0      255.0.0.0       U     0      0   0   lo
```

- 要快速检查接口状态，请使用`netstat -i`命令，如下所示：

  ```text
  [root@deep /]# netstat -i
  ```

输出应类似于以下内容：

```text
Kernel Interface table
Iface MTU Met RX-OK RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flg
eth0  1500  0   4236    0      0      0   3700    0      0      0  BRU
lo    3924  0  13300    0      0      0  13300    0      0      0  LRU
ppp0  1500  0     14    1      0      0     16    0      0      0  PRU
```

另一个有用的`netstat`选项是`-t`，它显示所有活动的 TCP 连接。以下是`netstat -t`的典型结果：

- 要显示所有活动的 TCP 连接，请使用以下命令：

  ```text
  [root@deep /]# netstat -t
  ```

输出应类似于以下内容：

活动 Internet 连接（不含服务器）

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
|---|---:|---:|---|---|---|
| Tcp | 0 | 0 | deep.openar:netbios-ssn | gate.openna.com:1045 | ESTABLISHED |
| Tcp | 0 | 0 | localhost:1032 | localhost:1033 | ESTABLISHED |
| Tcp | 0 | 0 | localhost:1033 | localhost:1032 | ESTABLISHED |
| Tcp | 0 | 0 | localhost:1030 | localhost:1034 | ESTABLISHED |
| Tcp | 0 | 0 | localhost:1031 | localhost:1030 | ESTABLISHED |
| Tcp | 0 | 0 | localhost:1028 | localhost:1029 | ESTABLISHED |
| Tcp | 0 | 0 | localhost:1029 | localhost:1028 | ESTABLISHED |
| Tcp | 0 | 0 | localhost:1026 | localhost:1027 | ESTABLISHED |
| Tcp | 0 | 0 | localhost:1027 | localhost:1026 | ESTABLISHED |



| Tcp | 0 | 0 | localhost:1024 | localhost:1025 | ESTABLISHED |
|---|---:|---:|---|---|---|
| Tcp | 0 | 0 | localhost:1025 | localhost:1024 | ESTABLISHED |

- 要显示所有活动和监听的 TCP 连接，请使用以下命令：

```bash
[root@deep /]# netstat -vat
```

输出应类似于以下内容：

活动 Internet 连接（含服务器和已建立连接）

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
|---|---:|---:|---|---|---|
| tcp | 0 | 0 | deep.openna.co:domain | *:* | LISTEN |
| tcp | 0 | 0 | localhost:domain | *:* | LISTEN |
| tcp | 0 | 0 | deep.openna.com:ssh | gate.openna.com:1682 | ESTABLISHED |
| tcp | 0 | 0 | *:webcache | *:* | LISTEN |
| tcp | 0 | 0 | deep.openar:netbios-ssn | *:* | LISTEN |
| tcp | 0 | 0 | localhost:netbios-ssn | *:* | LISTEN |
| tcp | 0 | 0 | localhost:1032 | localhost:1033 | ESTABLISHED |
| tcp | 0 | 0 | localhost:1033 | localhost:1032 | ESTABLISHED |
| tcp | 0 | 0 | localhost:1030 | localhost:1031 | ESTABLISHED |
| tcp | 0 | 0 | localhost:1031 | localhost:1030 | ESTABLISHED |
| tcp | 0 | 0 | localhost:1028 | localhost:1029 | ESTABLISHED |
| tcp | 0 | 0 | localhost:1029 | localhost:1028 | ESTABLISHED |
| tcp | 0 | 0 | localhost:1026 | localhost:1027 | ESTABLISHED |
| tcp | 0 | 0 | localhost:1027 | localhost:1026 | ESTABLISHED |
| tcp | 0 | 0 | localhost:1024 | localhost:1025 | ESTABLISHED |
| tcp | 0 | 0 | localhost:1025 | localhost:1024 | ESTABLISHED |
| tcp | 0 | 0 | deep.openna.com:www | *:* | LISTEN |
| tcp | 0 | 0 | deep.openna.com:https | *:* | LISTEN |
| tcp | 0 | 0 | *:389 | *:* | LISTEN |
| tcp | 0 | 0 | *:ssh | *:* | LISTEN |

- 要在你的系统上手动停止所有网络设备，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/network stop
Shutting down interface eth0		[ OK ]
Disabling IPv4 packet forwarding		[ OK ]
```

- 要在你的系统上手动启动所有网络设备，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/network start
Enabling IPv4 packet forwarding        [ OK ]
Bringing up interface lo               [ OK ]
Bringing up interface eth0             [ OK ]
```

# 第 7 章：网络防火墙

## 在本章中

- Linux IPCHAINS
- 构建支持 IPCHAINS 防火墙的内核
- 防火墙脚本文件中使用的规则说明
- 防火墙脚本文件
- Web 服务器的脚本文件配置
- 邮件服务器的脚本文件配置

## Linux IPCHAINS

### 概述

有人能告诉我为什么我可能想要一个商业防火墙产品，而不是简单地使用 Ipchains 并限制某些数据包吗？使用 Ipchains 我会失去什么？关于这一点，现在无疑存在争论的空间，从功能和支持的角度来看，Ipchains 与商业防火墙软件包一样好，而且在大多数情况下更好。与商业解决方案相比，使用 Ipchains 你可能会对你的网络有更深入的了解。话虽如此，很多公司高管想告诉他们的股东、CEO/CTO 等，他们有信誉良好的安全软件公司的支持支持。防火墙可能只是放行所有流量，但公司类型的人仍然会比依赖角落隔间里那个如果在中午前开灯就会发脾气的技术宅更让感到安心。

最终，很多公司都想在网络安全遭到破坏时能够向供应商要求某种形式的赔偿，无论他们实际上是否得到任何东西，甚至是否会尝试。对于开源解决方案，他们通常能做的只有解雇实施它的人。至少一些商业防火墙是基于 Linux 或类似系统的。Ipchains 对你来说可能足够安全，但对于从事大量高风险债券交易的人来说可能不行。在花费大量资金购买商业防火墙之前，建议进行成本/效益分析并问很多相关的问题——否则你可能最终得到的东西还不如你的 Ipchains 工具。相当多的 NT 防火墙可能并不比 Ipchains 更好，而 bugtraq 和 NT bugtraq 上的普遍共识是 NT *太不安全*，无法运行严肃的防火墙。

### 什么是网络防火墙安全策略？

网络防火墙安全策略定义了哪些服务将被明确允许或拒绝、这些服务将如何被使用以及这些规则的例外情况。组织的整体安全策略必须根据安全和业务需求分析来确定。由于防火墙仅与网络安全相关，除非正确定义了整体安全策略，否则防火墙几乎没有价值。网络防火墙安全策略中的每条规则都应该在防火墙上实现。通常，防火墙使用以下方法之一。

#### 未明确允许的一切都被拒绝

这种方法会阻止两个网络之间的所有流量，除了那些被允许的服务和应用程序。因此，每个期望的服务和应用程序都应该逐个实现。任何可能成为防火墙潜在漏洞的服务或应用程序都不应被允许。这是最安全的方法，除非管理员明确允许，否则拒绝服务和应用程序。另一方面，从用户的角度来看，它可能更具限制性且不太方便。这是我们将在本书的防火墙配置文件中使用的方法。

#### 未明确拒绝的一切都被允许

这种方法允许两个网络之间的所有流量，除了那些被拒绝的服务和应用程序。因此，每个不可信的或潜在有害的服务和应用程序都应该逐个拒绝。虽然这对用户来说是一种灵活且方便的方法，但它可能会导致一些严重的安全问题。

### 什么是包过滤？

包过滤是内置于 Linux 内核中的防火墙类型。过滤防火墙在网络层工作。数据只有在防火墙规则允许的情况下才能离开系统。数据包

它们会根据每个数据包中包含的类型、源地址、目标地址和端口信息进行过滤。

大多数时候，数据包过滤是通过使用能够根据过滤规则转发数据包的路由器来完成的。当数据包到达包过滤路由器时，路由器会从数据包头部提取特定信息，并根据过滤规则决定该数据包是通过还是被丢弃。

可以从数据包头部提取以下信息：

- Source IP address（源 IP 地址）
- Destination IP address（目标 IP 地址）
- TCP/UDP source port（TCP/UDP 源端口）
- TCP/UDP destination port（TCP/UDP 目标端口）
- ICMP message type（ICMP 消息类型）
- Encapsulated protocol information (TCP, UDP, ICMP or IP tunnel)（封装协议信息（TCP、UDP、ICMP 或 IP 隧道））

由于分析并记录的数据非常少，过滤防火墙消耗的 CPU 资源更少，并且在您的网络中产生的延迟也更低。有很多方法可以通过使用防火墙来构建网络以保护您的系统。

## 拓扑结构

所有服务器都应配置为至少屏蔽未使用的端口，**即使没有防火墙服务器**。这需要更多的安全性。想象一下有人获得了您的防火墙网关服务器的访问权限：如果邻近的服务器没有配置为屏蔽未使用的端口，这是一个严重的网络风险。本地连接也是如此；未经授权的员工可以从内部通过这种方式访问您的其他服务器。

在我们的配置中，我们将为您提供三个不同的示例，这些示例可以帮助您根据要保护的服务器类型以及这些服务器在网络架构中的位置来配置防火墙规则。第一个防火墙规则文件示例将用于 Web 服务器，第二个用于邮件服务器，最后一个用于网关服务器，该网关服务器为内部的 Wins、工作站和服务器机器充当代理。请参阅下图以获取概念。

| www.openna.com 仅缓存 DNS 208.164.186.3 | deep.openna.com 主 DNS 服务器 208.164.186.1 | mail.openna.com 从 DNS 服务器 208.164.186.2 |
|---|---|---|
| 1. 允许环回接口上的无限制流量 | 1. 允许环回接口上的无限制流量 | 1. 允许环回接口上的无限制流量 |
| 2. 允许 ICMP 流量 | 2. 允许 ICMP 流量 | 2. 允许 ICMP 流量 |
| 3. 允许端口 53 上的 DNS 缓存和客户端服务器 | 3. 允许端口 53 上的 DNS 服务器和客户端 | 3. 允许端口 53 上的 DNS 服务器和客户端 |
| 4. 允许端口 22 上的 SSH 服务器 | 4. 允许端口 22 上的 SSH 服务器和客户端 | 4. 允许端口 22 上的 SSH 服务器 |
| 5. 允许端口 80 上的 HTTP 服务器 | 5. 允许端口 80 上的 HTTP 服务器和客户端 | 5. 允许端口 25 上的 SMTP 服务器和客户端 |
| 6. 允许端口 443 上的 HTTPS 服务器 | 6. 允许端口 443 上的 HTTPS 服务器和客户端 | 6. 允许端口 143 上的 IMAP 服务器 |
| 7. 允许端口 25 上的 SMTP 客户端 | 7. 允许端口 8080 上的 WWW-CACHE 客户端 | 7. 允许发出的 traceroute 请求 |
| 8. 允许端口 20、21 上的 FTP 服务器 | 8. 允许端口 110 上的外部 POP 客户端 | |
| 9. 允许发出的 traceroute 请求 | 9. 允许端口 119 上的外部 NNTP NEWS 客户端 | |
| | 10. 允许端口 25 上的 SMTP 服务器和客户端 | |
| | 11. 允许端口 143 上的 IMAP 服务器 | |
| | 12. 允许端口 6667 上的 IRC 客户端 | |
| | 13. 允许端口 4000 上的 ICQ 客户端 | |
| | 14. 允许端口 20、21 上的 FTP 客户端 | |
| | 15. 允许 RealAudio / QuickTime 客户端 | |
| | 16. 允许发出的 traceroute 请求 | |

上表显示了我在本书的防火墙脚本文件中默认在不同服务器上启用的端口。根据服务器必须向外部提供的服务，您必须配置防火墙脚本文件以允许指定端口上的流量。`www.openna.com` 是我们的 Web 服务器，`mail.openna.com` 是我们所有内部网络的邮件中心服务器，`deep.openna.com` 是我们本章所有示例的网关服务器。

## 构建支持 IPCHAINS 防火墙的内核

您需要做的第一件事是确保您的内核已启用网络防火墙支持和防火墙功能构建。**请记住，所有服务器都应配置为屏蔽未使用的端口，即使没有防火墙服务器。** 在 2.2.14 内核版本中，您需要确保对以下问题回答了 **Y**：

**网络选项：**

`Network firewalls (CONFIG_FIREWALL) [N] Y`

`IP:Firewalling (CONFIG_IP_FIREWALL) [N] Y`

`IP:TCP syncookie support (CONFIG_SYN_COOKIES) [N] Y`

**注意：** 如果您已经按照 Linux 内核部分操作并重新编译了内核，上述显示的“Network firewalls、IP:Firewalling 和 IP:TCP syncookie support”选项已经设置好了。

## 防火墙脚本文件中使用的规则的一些解释

以下是对下面防火墙示例中将使用的一些规则的解释。这只是作为参考，防火墙脚本有很好的注释，并且非常容易修改。

## 防火墙脚本文件示例中使用的常量

大多数值都使用常量。最基本的常量有：

### EXTERNAL_INTERFACE

这是连接到 Internet 的外部网络接口的名称。在示例中定义为 `eth0`。

### LOCAL_INTERFACE_1

这是连接到 LAN（如果有的话）的内部网络接口的名称。在示例中定义为 `eth1`。

### LOOPBACK_INTERFACE

这是环回接口的名称。在示例中定义为 `lo`。

### IPADDR

这是外部接口的 IP 地址。它要么是向 InterNIC 注册的静态 IP 地址，要么是来自 ISP 的动态分配地址（通常通过 DHCP）。

### LOCALNET_1

这是您的 LAN 网络地址（如果有的话）——LAN 上机器使用的整个 IP 地址范围。这些可以是静态分配的，或者您可以运行本地 DHCP 服务器来分配它们。在这些示例中，范围是 `192.168.1.0/24`，属于 C 类私有地址范围的一部分。

### ANYWHERE

Anywhere 是 `ipchains` 用于匹配任何（非广播）地址的地址标签。两个程序都提供 `any/0` 作为此地址的标签，即 `0.0.0.0/0`。

### NAMESERVER_1

这是来自您的网络或 ISP 的主 DNS 服务器的 IP 地址。

### NAMESERVER_2

这是来自您的网络或 ISP 的辅助 DNS 服务器的 IP 地址。

### MY_ISP

这是您的 ISP 和 NOC 地址范围。您在此处指定的值由防火墙用于允许 ICMP ping 请求和 traceroute。如果您没有指定 IP 地址范围，那么您将无法从内部网络 ping 通 Internet。

### LOOPBACK

环回地址范围是 `127.0.0/8`。接口本身被寻址为 `127.0.0.1`（在`/etc/hosts`中）。

### PRIVPORTS

特权端口，0 到 1023，通常被整体引用。

### UNPRIVPORTS

非特权端口，1024 到 65535，通常被整体引用。它们是动态分配给连接客户端的地址。

## 默认策略

防火墙具有默认策略和针对特定消息类型执行的操作集合。这意味着如果给定数据包未被任何其他规则选中，则将应用默认策略规则。

**注意：** 使用 ISP 动态分配 IP 的用户可以在其防火墙声明中包含以下两行。这些行将确定 `ppp0` IP 地址以及远程 ppp 服务器的网络。

```bash
IPADDR=`/sbin/ifconfig | grep -A 4 ppp0 | awk '/inet/ { print $2 } ' | sed -e s/addr://
MY_ISP=`/sbin/ifconfig | grep -A 4 ppp0 | awk '/P-t-P/ { print $3 } ' | sed -e s/P-t-P:// | cut -d '.' -f 1-3`.0/24
```

## 启用本地流量

由于本书中所有示例防火墙规则脚本文件的默认策略是拒绝所有流量，其中一些规则必须被取消设置。本地网络服务不通过外部网络接口传输。它们通过一个特殊的私有接口，称为环回接口。在允许环回流量之前，您的任何本地网络程序都无法工作。

```bash
# 环回接口上的无限制流量。
ipchains -A input -i $LOOPBACK_INTERFACE -j ACCEPT
ipchains -A output -i $LOOPBACK_INTERFACE -j ACCEPT
```

## 源地址过滤

所有 IP 数据包头部都包含源和目标 IP 地址以及此数据包包含的 IP 协议消息类型（ICMP、UDP 或 TCP）。互联网协议（IP）下唯一的识别方法是 IP 数据包头部中的源地址。这是一个问题，它为源地址欺骗打开了大门，发送者可能会将其地址替换为不存在的地址或其他某个站点的地址。

```bash
# 拒绝假装来自外部地址的欺骗数据包。
ipchains -A input -i $EXTERNAL_INTERFACE -s $IPADDR -l -j DENY
```

此外，在所有情况下，您的外部接口上至少应有七组源地址需要被拒绝。

这些是声称来自以下地址的传入数据包：

- 你的外部 IP 地址
- A 类私有 IP 地址
- B 类私有 IP 地址
- C 类私有 IP 地址
- D 类组播地址
- E 类保留地址
- 回环接口

除了你自己的 IP 地址外，阻止出站数据包中包含这些源地址可以避免因配置错误而带来的风险。

**注意：** 不要忘记将你自己 IP 地址排除在出站阻止规则之外。默认情况下，我选择排除 C 类私有 IP 地址，因为它是目前大多数用户最常用的。如果你使用的是其他类别而非 C 类，则必须在防火墙脚本文件的 **“SPOOFING & BAD ADDRESSES”（欺骗与无效地址）** 部分下，将对应类别的行注释掉。

## 其余规则



防火墙脚本文件中使用的其他规则包括：

- 从外部世界访问服务
- 向外部世界提供服务
- 内部机器的网络地址伪装（Masquerading）

## 防火墙脚本文件

`ipchains` 工具允许你设置防火墙、IP 地址伪装等。`Ipchains` 与内核通信，告诉内核需要过滤哪些数据包。因此，所有防火墙配置都存储在内核中，重启后将会丢失。

为了避免这种情况，我们建议使用 System V 初始化脚本来使规则持久化。为此，在`/etc/rc.d/init.d/`目录下为你拥有的每台服务器创建一个如下所示的防火墙脚本文件。

当然，每台服务器提供的服务不同，需要不同的防火墙配置。因此，我们为你提供了三种不同的防火墙设置，你可以根据需要进行尝试和调整。此外，我假设你已经具备过滤防火墙和防火墙规则工作原理的基础知识。

## Web 服务器`/etc/rc.d/init.d/firewall`脚本文件的配置

这是我们 Web 服务器的配置脚本文件。该配置默认允许回环接口、ICMP、DNS 缓存与客户端服务器（`53`）、SSH 服务器（`22`）、HTTP 服务器（`80`）、HTTPS 服务器（`443`）、SMTP 客户端（`25`）、FTP 服务器（`20, 21`）以及出站 `TRACEROUTE` 请求的无限流量。

如果你不希望我在 Web 服务器防火墙规则文件中默认开启的某些服务，可以在行首添加`#`进行注释。如果你希望我注释掉的服务生效，请删除这些行首的`#`。

在你的 Web 服务器上创建`firewall`脚本文件（`touch /etc/rc.d/init.d/firewall`）并添加：

```sh
#!/bin/sh
#
# -----------------------------------------------------------------------
# Last modified by Gerhard Mourani: 04-25-2000
# -----------------------------------------------------------------------
# Copyright (C) 1997, 1998, 1999  Robert L. Ziegler
# Permission to use, copy, modify, and distribute this software and its
# documentation for educational, research, private and non-profit purposes,
# without fee, and without a written agreement is hereby granted.
# This software is provided as an example and basis for individual firewall
# development. This software is provided without warranty.
#
# Any material furnished by Robert L. Ziegler is furnished on an
# "as is" basis. He makes no warranties of any kind, either expressed
# or implied as to any matter including, but not limited to, warranty
# of fitness for a particular purpose, exclusivity or results obtained
# from use of the material.
# --------------------------------------------------------------------
#
# Invoked from /etc/rc.d/init.d/firewall.
# chkconfig: - 60 95
# description: Starts and stops the IPCHAINS Firewall \
#        used to provide Firewall network services.

# Source function library.
. /etc/rc.d/init.d/functions

# Source networking configuration.
. /etc/sysconfig/network

# Check that networking is up.
if [ ${NETWORKING} = "no" ]
then
    exit 0
fi

if [ ! -x /sbin/ipchains ]; then
  exit 0
fi

# See how we were called.
case "$1" in
  start)
    echo -n "Starting Firewalling Services: "

# Some definitions for easy maintenance.

# --------------------------------------------------------------------
# EDIT THESE TO SUIT YOUR SYSTEM AND ISP.

EXTERNAL_INTERFACE="eth0"                # Internet connected interface
LOOPBACK_INTERFACE="lo"                  # Your local naming convention
IPADDR="my.ip.address"                   # Your IP address
ANYWHERE="any/0"                         # Match any IP address
NAMESERVER_1="my.name.server.1"          # Everyone must have at least one
NAMESERVER_2="my.name.server.2"          # Your secondary name server
MY_ISP="my.isp.address.range/24"         # ISP & NOC address range

SMTP_SERVER="my.smtp.server"             # Your Mail Hub Server.
SYSLOG_SERVER="syslog.internal.server"   # Your syslog internal server
SYSLOG_CLIENT="sys.int.client.range/24"  # Your syslog internal client range

LOOPBACK="127.0.0.0/8"                   # Reserved loopback address range
CLASS_A="10.0.0.0/8"                     # Class A private networks
CLASS_B="172.16.0.0/12"                  # Class B private networks
CLASS_C="192.168.0.0/16"                  # Class C private networks
CLASS_D_MULTICAST="224.0.0.0/4"          # Class D multicast addresses

CLASS_E_RESERVED_NET="240.0.0.0/5"       # Class E reserved addresses
BROADCAST_SRC="0.0.0.0"                  # Broadcast source address
BROADCAST_DEST="255.255.255.255"         # Broadcast destination address
PRIVPORTS="0:1023"                       # Well known, privileged port range
UNPRIVPORTS="1024:65535"                 # Unprivileged port range
```

```sh
# ----------------------------------------------------------------
# SSH starts at 1023 and works down to 513 for
# each additional simultaneous incoming connection.
SSH_PORTS="1022:1023"                    # range for SSH privileged ports

# traceroute usually uses -S 32769:65535 -D 33434:33523
TRACEROUTE_SRC_PORTS="32769:65535"
TRACEROUTE_DEST_PORTS="33434:33523"
```

```sh
# ----------------------------------------------------------------
# Default policy is DENY
# Explicitly accept desired INCOMING & OUTGOING connections

  # Remove all existing rules belonging to this filter
  ipchains -F

  # Clearing all current rules and user defined chains
  ipchains -X

  # Set the default policy of the filter to deny.
  # Don't even bother sending an error message back.
  ipchains -P input  DENY
  ipchains -P output DENY
  ipchains -P forward DENY
```

```sh
# ----------------------------------------------------------------
# LOOPBACK

  # Unlimited traffic on the loopback interface.
  ipchains -A input  -i $LOOPBACK_INTERFACE -j ACCEPT
  ipchains -A output -i $LOOPBACK_INTERFACE -j ACCEPT
```

```sh
# ----------------------------------------------------------------
# Network Ghouls
# Deny access to jerks

  # /etc/rc.d/rc.firewall.blocked contains a list of
  # ipchains -A input  -i $EXTERNAL_INTERFACE -s address -j DENY
  # rules to block from any access.

  # Refuse any connection from problem sites
  #if [ -f /etc/rc.d/rc.firewall.blocked ]; then
  #   . /etc/rc.d/rc.firewall.blocked
  #fi
```

```sh
# ----------------------------------------------------------------
# SPOOFING & BAD ADDRESSES
# Refuse spoofed packets.
# Ignore blatantly illegal source addresses.
# Protect yourself from sending to bad addresses.

  # Refuse spoofed packets pretending to be from the external address.
  ipchains -A input  -i $EXTERNAL_INTERFACE -s $IPADDR -j DENY -l

  # Refuse packets claiming to be to or from a Class A private network
```

```sh
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_A -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_A -j DENY -l
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_A -j REJECT -l
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_A -j REJECT -l
```

### 拒绝声称来自或发往 B 类私有网络的数据包

```sh
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_B -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_B -j DENY -l
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_B -j REJECT -l
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_B -j REJECT -l
```

### 拒绝声称来自或发往 C 类私有网络的数据包

```sh
# ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_C -j DENY -l
# ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_C -j DENY -l
# ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_C -j REJECT -l
# ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_C -j REJECT -l
```

### 拒绝声称来自回环接口的数据包

```sh
ipchains -A input -i $EXTERNAL_INTERFACE -s $LOOPBACK -j DENY -l
ipchains -A output -i $EXTERNAL_INTERFACE -s $LOOPBACK -j REJECT -l
```

### 拒绝广播地址源数据包

```sh
ipchains -A input -i $EXTERNAL_INTERFACE -s $BROADCAST_DEST -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -d $BROADCAST_SRC -j DENY -l
```

### 拒绝 D 类组播地址（in.h）（NET-3-HOWTO）

组播地址作为源地址是非法的。

组播使用 UDP。

```sh
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_D_MULTICAST -j DENY -l
```

### 拒绝 E 类保留 IP 地址

```sh
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_E_RESERVED_NET -j DENY -l
```

### 拒绝 IANA 定义的保留地址

```sh
# 0.*.*.*, 1.*.*.*, 2.*.*.*, 5.*.*.*, 7.*.*.*, 23.*.*.*, 27.*.*.*
# 31.*.*.*, 37.*.*.*, 39.*.*.*, 41.*.*.*, 42.*.*.*, 58-60.*.*.*
# 65-95.*.*.*, 96-126.*.*.*, 197.*.*.*, 201.*.*.* (?), 217-223.*.*.*
```



```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 1.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 2.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 5.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 7.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 23.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 27.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 31.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 37.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 39.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 41.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 42.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 58.0.0.0/7 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 60.0.0.0/8 -j DENY -l
```

## 65: 01000001 — `/3` 包含 64，需要单独定义 65–79

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 65.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 66.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 67.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 68.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 69.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 70.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 71.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 72.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 73.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 74.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 75.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 76.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 77.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 78.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 79.0.0.0/8 -j DENY -l
```

## 80: 01010000 — `/4` 掩码 80–95

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 80.0.0.0/4 -j DENY -l
```

## 96: 01100000 — `/4` 掩码 96–111

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 96.0.0.0/4 -j DENY -l
```

## 126: 01111110 — `/3` 包含 127，需要逐条写出 112–126

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 112.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 113.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 114.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 115.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 116.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 117.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 118.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 119.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 120.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 121.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 122.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 123.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 124.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 125.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 126.0.0.0/8 -j DENY -l
```

## 217: 11011001 — `/5` 包含 216，需要逐条写出 217–219

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 217.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 218.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 219.0.0.0/8 -j DENY -l
```

## 223: 11011111 — `/6` 掩码 220–223

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 220.0.0.0/6 -j DENY -l
```

## ICMP

为防止基于 ICMP 炸弹的拒绝服务攻击，过滤传入的重定向（5）和传出的目标不可达（3）。

但请注意，禁用目标不可达（3）并不可取，因为它用于协商数据包分片大小。

### 用于双向 ping

消息类型：回显应答（0）、回显请求（8）。

为防止攻击，将源地址限制为您的 ISP 范围。

### 用于传出 traceroute

消息类型：传入的目标不可达（3）、超时（11）。

默认 UDP 基础端口：33434 到 `base+nhops-1`。

### 用于传入 traceroute

消息类型：传出的目标不可达（3）、超时（11）。

要阻止此功能，拒绝传出的 3 和 11。

### ICMP 消息类型

- 0：回显应答（pong）
- 3：目标不可达、端口不可达、需要分片等
- 4：源抑制
- 5：重定向
- 8：回显请求（ping）
- 11：超时
- 12：参数问题

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $ANYWHERE 0 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $ANYWHERE 3 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $ANYWHERE 4 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $ANYWHERE 11 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $ANYWHERE 12 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $MY_ISP 8 -d $IPADDR -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 0 -d $MY_ISP -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 3 -d $MY_ISP -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 4 -d $ANYWHERE -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 8 -d $ANYWHERE -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 12 -d $ANYWHERE -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 11 -d $MY_ISP -j ACCEPT
```

## UDP 传入 traceroute

`traceroute` 通常使用 `-S 32769:65535 -D 33434:33523`。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $MY_ISP $TRACEROUTE_SRC_PORTS \
    -d $IPADDR $TRACEROUTE_DEST_PORTS -j ACCEPT -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $ANYWHERE $TRACEROUTE_SRC_PORTS \
    -d $IPADDR $TRACEROUTE_DEST_PORTS -j DENY -l
```

## DNS 转发，仅缓存域名服务器（53）

### 服务器到服务器的查询或响应

仅缓存域名服务器只需要 UDP，不需要 TCP。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $NAMESERVER_1 53 \
    -d $IPADDR 53 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR 53 \
    -d $NAMESERVER_1 53 -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $NAMESERVER_2 53 \
    -d $IPADDR 53 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR 53 \
    -d $NAMESERVER_2 53 -j ACCEPT
```

### DNS 客户端（53）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $NAMESERVER_1 53 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR $UNPRIVPORTS \
    -d $NAMESERVER_1 53 -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $NAMESERVER_2 53 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR $UNPRIVPORTS \
    -d $NAMESERVER_2 53 -j ACCEPT
```

如果 UDP 请求失败，TCP 客户端到服务器的请求是被协议允许的。这很少见。通常，客户端使用 TCP 作为从主域名服务器进行区域传输的辅助域名服务器，以及黑客使用。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $NAMESERVER_1 53 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
    -s $IPADDR $UNPRIVPORTS \
    -d $NAMESERVER_1 53 -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $NAMESERVER_2 53 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
    -s $IPADDR $UNPRIVPORTS \
    -d $NAMESERVER_2 53 -j ACCEPT
```

## TCP 仅接受选定端口

### SSH 服务器（22）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 22 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR 22 \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $SSH_PORTS \
    -d $IPADDR 22 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR 22 \
    -d $ANYWHERE $SSH_PORTS -j ACCEPT
```

### HTTP 服务器（80）



```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 80 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR 80 \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

# HTTPS 服务器（443）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 443 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR 443 \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

# 提供完整的远程日志记录

使用此功能，您可以在一台主机上控制所有 syslog 消息。

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
#     -s $SYSLOG_CLIENT \
#     -d $IPADDR 514 -j ACCEPT
```

# SYSLOG 客户端（514）

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
#     -s $IPADDR 514 \
#     -d $SYSLOG_SERVER 514 -j ACCEPT
```

# AUTH 服务器（113）

拒绝，而不是阻止，传入的 auth 端口。（NET-3-HOWTO）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE \
    -d $IPADDR 113 -j REJECT
```

Copyright 1999 - 2000 Gerhard Mourani, Open Network Architecture ® and OpenDocs Publishing

# SMTP 客户端（25）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $SMTP_SERVER 25 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
    -s $IPADDR $UNPRIVPORTS \
    -d $SMTP_SERVER 25 -j ACCEPT
```

# FTP 服务器（20、21）

## 传入请求

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 21 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR 21 \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

## PORT 模式数据通道响应

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 20 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
    -s $IPADDR 20 \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

## PASSIVE 模式数据通道响应

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR $UNPRIVPORTS \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

# 出站 TRACEROUTE

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR $TRACEROUTE_SRC_PORTS \
    -d $ANYWHERE $TRACEROUTE_DEST_PORTS -j ACCEPT
```

# 为选定的被拒绝数据包启用日志记录

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -d $IPADDR -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -d $IPADDR $PRIVPORTS -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -d $IPADDR $UNPRIVPORTS -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $ANYWHERE 5 -d $IPADDR -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $ANYWHERE 13:255 -d $IPADDR -j DENY -l
```

```bash
;;

stop)

  echo -n "Shutting Firewalling Services: "

  # Remove all existing rules belonging to this filter

  ipchains -F

  # Delete all user-defined chain to this filter

  ipchains -X

  # Reset the default policy of the filter to accept.

  ipchains -P input ACCEPT

  ipchains -P output ACCEPT

  ipchains -P forward ACCEPT

  ;;

status)

  status firewall

  ;;

restart|reload)

  $0 stop

  $0 start

  ;;

*)

  echo "Usage: firewall {start|stop|status|restart|reload}"

  exit 1

esac

exit 0
```

现在，使此脚本可执行并更改其默认权限：

```bash
[root@deep /]# chmod 700 /etc/rc.d/init.d/firewall
[root@deep /]# chown 0.0 /etc/rc.d/init.d/firewall
```

使用以下命令为您的防火墙创建符号 `rc.d` 链接：

```bash
[root@deep /]# chkconfig --add firewall
[root@deep /]# chkconfig --level 345 firewall on
```

现在，您的防火墙规则已配置为使用 System V init（System V init 负责启动所有需要在启动时运行的正常进程），并且每次服务器重新启动时都会自动启动。

- 要手动停止系统上的防火墙，请使用以下命令：

  ```text
  [root@deep /]# /etc/rc.d/init.d/firewall stop
  Shutting Firewalling Services:            [ OK ]
  ```

- 要手动启动系统上的防火墙，请使用以下命令：

  ```text
  [root@deep /]# /etc/rc.d/init.d/firewall start
  Starting Firewalling Services:              [ OK ]
  ```

## `/etc/rc.d/init.d/firewall` 脚本文件的邮件服务器配置

这是我们邮件服务器的配置脚本文件。此配置默认允许环回接口、ICMP、DNS 服务器和客户端（53）、SSH 服务器（22）、SMTP 服务器和客户端（25）、IMAP 服务器（143）以及出站 TRACEROUTE 请求上的无限制流量。

如果您不希望邮件服务器的防火墙规则文件中列出我默认启用的某些服务，请在该行开头用 `#` 将其注释掉。如果您想要我注释掉的某些其他服务，请删除它们行首的 `#`。

在您的邮件服务器上创建 `firewall` 脚本文件（`touch /etc/rc.d/init.d/firewall`）并添加：

```bash
#!/bin/sh

#
# ------------------------------------------------------------------------
# Last modified by Gerhard Mourani: 04-25-2000
# ------------------------------------------------------------------------
# Copyright (C) 1997, 1998, 1999  Robert L. Ziegler
#
# Permission to use, copy, modify, and distribute this software and its
# documentation for educational, research, private and non-profit purposes,
# without fee, and without a written agreement is hereby granted.
# This software is provided as an example and basis for individual firewall
# development.  This software is provided without warranty.
#
# Any material furnished by Robert L. Ziegler is furnished on an
# "as is" basis.  He makes no warranties of any kind, either expressed
# or implied as to any matter including, but not limited to, warranty
# of fitness for a particular purpose, exclusivity or results obtained
# from use of the material.
# ------------------------------------------------------------------------
#
# Invoked from /etc/rc.d/init.d/firewall.
# chkconfig: - 60 95
# description: Starts and stops the IPCHAINS Firewall \
#       used to provide Firewall network services.

# Source function library.
. /etc/rc.d/init.d/functions

# Source networking configuration.
. /etc/sysconfig/network

# Check that networking is up.
if [ ${NETWORKING} = "no" ]
then
    exit 0
fi

if [ ! -x /sbin/ipchains ]; then
    exit 0
fi

# See how we were called.
case "$1" in

  start)

    echo -n "Starting Firewalling Services: "

# Some definitions for easy maintenance.

# ------------------------------------------------------------------------
```

## 编辑这些以适应您的系统和 ISP

```bash
EXTERNAL_INTERFACE="eth0"                    # Internet connected interface
LOOPBACK_INTERFACE="lo"                     # Your local naming convention
IPADDR="my.ip.address"                       # Your IP address
ANYWHERE="any/0"                             # Match any IP address
NAMESERVER_1="my.name.server.1"              # Everyone must have at least one
NAMESERVER_2="my.name.server.2"              # Your secondary name server
MY_ISP="my.isp.address.range/24"              # ISP & NOC address range

SMTP_SERVER="my.smtp.server"                 # Your Mail Hub Server.
SYSLOG_SERVER="syslog.internal.server"       # Your syslog internal server
SYSLOG_CLIENT="sys.int.client.range/24"      # Your syslog internal client range

LOOPBACK="127.0.0.0/8"                       # Reserved loopback address range
CLASS_A="10.0.0.0/8"                          # Class A private networks
CLASS_B="172.16.0.0/12"                       # Class B private networks
CLASS_C="192.168.0.0/16"                      # Class C private networks
CLASS_D_MULTICAST="224.0.0.0/4"               # Class D multicast addresses
CLASS_E_RESERVED_NET="240.0.0.0/5"            # Class E reserved addresses
BROADCAST_SRC="0.0.0.0"                       # Broadcast source address
BROADCAST_DEST="255.255.255.255"              # Broadcast destination address
PRIVPORTS="0:1023"                             # Well known, privileged port range
UNPRIVPORTS="1024:65535"                       # Unprivileged port range
```

```bash
# ------------------------------------------------------------------------
```



# SSH 端口

SSH 从 `1023` 开始，并向下工作到 `513`，用于每个额外的同时传入连接。

```bash
SSH_PORTS="1022:1023" # range for SSH privileged ports
```

`traceroute` 通常使用 `-S 32769:65535 -D 33434:33523`。

```bash
TRACEROUTE_SRC_PORTS="32769:65535"
TRACEROUTE_DEST_PORTS="33434:33523"
```

# 默认策略

默认策略为拒绝（`DENY`）。

显式接受所需的传入和传出连接。

## 清除现有规则

删除属于此过滤器的所有现有规则：

```bash
ipchains -F
```

清除所有当前规则和用户定义的链：

```bash
ipchains -X
```

将过滤器的默认策略设置为拒绝。

不要发送错误消息：

```bash
ipchains -P input DENY
ipchains -P output DENY
ipchains -P forward DENY
```

# 回环接口

允许回环接口上的无限流量：

```bash
ipchains -A input -i $LOOPBACK_INTERFACE -j ACCEPT
ipchains -A output -i $LOOPBACK_INTERFACE -j ACCEPT
```

# 网络恶意流量

拒绝不可靠的访问。

## 欺骗与错误地址

`/etc/rc.d/rc.firewall.blocked` 包含一个列表：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s address -j DENY
```

用于阻止任何访问的规则。

拒绝来自问题站点的连接：

```bash
if [ -f /etc/rc.d/rc.firewall.blocked ]; then
   . /etc/rc.d/rc.firewall.blocked
fi
```

拒绝欺骗性数据包。

忽略明显非法的源地址，防止向错误地址发送数据。

拒绝伪装成来自外部地址的欺骗性数据包：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $IPADDR -j DENY -l
```

拒绝声称来自或发往 A 类私有网络的数据包：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_A -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_A -j DENY -l
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_A -j REJECT -l
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_A -j REJECT -l
```

拒绝声称来自或发往 B 类私有网络的数据包：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_B -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_B -j DENY -l
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_B -j REJECT -l
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_B -j REJECT -l
```

拒绝声称来自或发往 C 类私有网络的数据包：

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_C -j DENY -l
# ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_C -j DENY -l
# ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_C -j REJECT -l
# ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_C -j REJECT -l
```

拒绝声称来自回环接口的数据包：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $LOOPBACK -j DENY -l
ipchains -A output -i $EXTERNAL_INTERFACE -s $LOOPBACK -j REJECT -l
```

拒绝以广播地址作为源地址的数据包：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $BROADCAST_DEST -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -d $BROADCAST_SRC -j DENY -l
```

拒绝 D 类组播地址（`in.h`）（NET-3-HOWTO）。

组播作为源地址是非法的。组播使用 UDP。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_D_MULTICAST -j DENY -l
```

拒绝 E 类保留 IP 地址：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_E_RESERVED_NET -j DENY -l
```

拒绝 IANA 定义为保留的地址：

```text
0.*.*.*, 1.*.*.*, 2.*.*.*, 5.*.*.*, 7.*.*.*, 23.*.*.*, 27.*.*.*
31.*.*.*, 37.*.*.*, 39.*.*.*, 41.*.*.*, 42.*.*.*, 58-60.*.*.*
65-95.*.*.*, 96-126.*.*.*, 197.*.*.*, 201.*.*.* (?), 217-223.*.*.*
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 1.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 2.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 5.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 7.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 23.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 27.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 31.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 37.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 39.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 41.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 42.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 58.0.0.0/7 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 60.0.0.0/8 -j DENY -l
```

`65: 01000001 - /3` 包含 `64`，需要将 `65-79` 单独列出：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 65.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 66.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 67.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 68.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 69.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 70.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 71.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 72.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 73.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 74.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 75.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 76.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 77.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 78.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 79.0.0.0/8 -j DENY -l
```

`80: 01010000 - /4` 覆盖 `80-95`：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 80.0.0.0/4 -j DENY -l
```

`96: 01100000 - /4` 覆盖 `96-111`：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 96.0.0.0/4 -j DENY -l
```

`126: 01111110 - /3` 包含 `127`，需要将 `112-126` 单独列出：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 112.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 113.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 114.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 115.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 116.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 117.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 118.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 119.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 120.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 121.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 122.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 123.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 124.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 125.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 126.0.0.0/8 -j DENY -l
```

`217: 11011001 - /5` 包含 `216`，需要将 `217-219` 单独列出：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 217.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 218.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 219.0.0.0/8 -j DENY -l
```

`223: 11011111 - /6` 覆盖 `220-223`：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 220.0.0.0/6 -j DENY -l
```

# ICMP

为了防止基于 ICMP 炸弹的拒绝服务攻击，过滤传入的重定向（`5`）和传出的目标不可达（`3`）。

但请注意，禁用目标不可达（`3`）并不可取，因为它用于协商数据包分片大小。

## 双向 Ping

用于双向 `ping`。

- 消息类型：回显应答（`0`）、回显请求（`8`）。
- 为了防止攻击，将源地址限制在您的 ISP 范围内。

## 传出 Traceroute

用于传出 `traceroute`。

- 消息类型：传入目标不可达（`3`）、超时（`11`）。
- 默认 UDP 基础端口：`33434` 到 `base+nhops-1`。

## 传入 Traceroute

用于传入 `traceroute`。

要阻止此操作，拒绝传出 `3` 和 `11`。

## ICMP 消息类型

- `0`：回显应答（pong）。
- `3`：目标不可达，端口不可达，需要分片，等。
- `4`：源抑制。
- `5`：重定向。
- `8`：回显请求（ping）。
- `11`：超时。
- `12`：参数问题。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
        -s $ANYWHERE 0 -d $IPADDR -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
        -s $ANYWHERE 3 -d $IPADDR -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
        -s $ANYWHERE 4 -d $IPADDR -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
        -s $ANYWHERE 11 -d $IPADDR -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
        -s $ANYWHERE 12 -d $IPADDR -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
        -s $MY_ISP 8 -d $IPADDR -j ACCEPT
```



```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 0 -d $MY_ISP -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 3 -d $MY_ISP -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 4 -d $ANYWHERE -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 8 -d $ANYWHERE -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 12 -d $ANYWHERE -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
    -s $IPADDR 11 -d $MY_ISP -j ACCEPT
```

## UDP 传入 TRACEROUTE

`traceroute` 通常使用 `-S 32769:65535 -D 33434:33523`。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $MY_ISP $TRACEROUTE_SRC_PORTS \
    -d $IPADDR $TRACEROUTE_DEST_PORTS -j ACCEPT -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $ANYWHERE $TRACEROUTE_SRC_PORTS \
    -d $IPADDR $TRACEROUTE_DEST_PORTS -j DENY -l
```

## DNS 服务器

### DNS：完整服务器

服务器/客户端到服务器的查询或响应：

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 53 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR 53 \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

### DNS 客户端与区域传输（53）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $NAMESERVER_1 53 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR $UNPRIVPORTS \
    -d $NAMESERVER_1 53 -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $NAMESERVER_1 53 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
    -s $IPADDR $UNPRIVPORTS \
    -d $NAMESERVER_1 53 -j ACCEPT
```

## TCP 仅接受选定端口

### SSH 服务器（22）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 22 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR 22 \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $SSH_PORTS \
    -d $IPADDR 22 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR 22 \
    -d $ANYWHERE $SSH_PORTS -j ACCEPT
```

### AUTH 服务器（113）

拒绝而非否认传入的 auth 端口。（NET-3-HOWTO）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE \
    -d $IPADDR 113 -j REJECT
```

### SYSLOG 服务器（514）

提供完整的远程日志记录。使用此功能，您能够在一台主机上控制所有 syslog 消息。

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
#     -s $SYSLOG_CLIENT \
#     -d $IPADDR 514 -j ACCEPT
```

### SYSLOG 客户端（514）

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
#     -s $IPADDR 514 \
#     -d $SYSLOG_SERVER 514 -j ACCEPT
```

### SMTP 服务器（25）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 25 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR 25 \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

### SMTP 客户端（25）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $ANYWHERE 25 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
    -s $IPADDR $UNPRIVPORTS \
    -d $ANYWHERE 25 -j ACCEPT
```

### IMAP 服务器（143）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 143 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $IPADDR 143 \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

### POP 服务器（110）

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
#     -s $ANYWHERE $UNPRIVPORTS \
#     -d $IPADDR 110 -j ACCEPT

# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
#     -s $IPADDR 110 \
#     -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

### 传出 TRACEROUTE

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR $TRACEROUTE_SRC_PORTS \
    -d $ANYWHERE $TRACEROUTE_DEST_PORTS -j ACCEPT
```

## 为选定的拒绝数据包启用日志记录

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
    -d $IPADDR -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -d $IPADDR $PRIVPORTS -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -d $IPADDR $UNPRIVPORTS -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $ANYWHERE 5 -d $IPADDR -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
    -s $ANYWHERE 13:255 -d $IPADDR -j DENY -l

;;

stop)

    echo -n "关闭防火墙服务: "

    # 删除属于此过滤器的所有现有规则
    ipchains -F

    # 删除此过滤器的所有用户自定义链
    ipchains -X

    # 将过滤器的默认策略重置为接受
    ipchains -P input ACCEPT
    ipchains -P output ACCEPT
    ipchains -P forward ACCEPT

;;

status)

    status firewall

;;

restart|reload)

    $0 stop
    $0 start

;;

*)

    echo "用法: firewall {start|stop|status|restart|reload}"
    exit 1

esac

exit 0
```

现在，使此脚本可执行并更改其默认权限：

```bash
[root@deep /]# chmod 700 /etc/rc.d/init.d/firewall
[root@deep /]# chown 0.0 /etc/rc.d/init.d/firewall
```

使用以下命令为您的防火墙创建符号链接 `rc.d` 链接：

```bash
[root@deep /]# chkconfig --add firewall
[root@deep /]# chkconfig --level 345 firewall on
```

现在，您的防火墙规则已配置为使用 System V init（System V init 负责启动所有需要在引导时运行的正常进程），并且如果服务器重新启动，它将自动启动。

- 要手动停止系统上的防火墙，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/firewall stop

关闭防火墙服务:           [ OK ]
```

- 要手动启动系统上的防火墙，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/firewall start

启动防火墙服务:           [ OK ]
```

# 第 8 章 支持伪装和转发的网络防火墙

## 本章内容

- 构建支持防火墙伪装和转发的内核
- 网关服务器脚本文件的配置
- 拒绝访问某些地址
- IPCHAINS 管理工具

## Linux 伪装和转发

### 概述

与第 7 章中的示例配置相反，配置 Linux 服务器以伪装和转发来自内部私有网络的流量（具有未注册 IP 地址，即 `192.168.1.0/24`）到外部网络（即互联网）通常需要对内核和防火墙配置脚本文件进行特殊设置。这种设置也被称为网关服务器（作为内部流量到外部流量的网关的机器）。只有在您有意图和需求使用此类服务时，才必须设置此配置，正因为如此，网关服务器的脚本文件配置才单独成章。

### 构建支持防火墙伪装和转发的内核

再一次，您需要做的第一件事是确保您的内核已启用网络防火墙支持并启用了防火墙功能。在 2.2.14 内核版本中，您需要确保对以下问题回答了 **Y**：

**网络选项：**

- 网络防火墙（`CONFIG_FIREFALL`）[`N`] **Y**
- IP：防火墙功能（`CONFIG_IP_FIREWALL`）[`N`] **Y**
- IP：TCP syncookie 支持（`CONFIG_SYN_COOKIES`）[`N`] **Y**

**注意：** 如果您遵循了 Linux 内核部分并重新编译了内核，则上述显示的“网络防火墙、IP：防火墙功能和 IP：TCP syncookie 支持”选项已设置。

**IP 伪装和 IP ICMP 伪装仅对网关服务器需要。**

- IP：伪装（`CONFIG_IP_MASQUERADE`）[`N`] **Y**
- IP：ICMP 伪装（`CONFIG_IP_MASQUERADE_ICMP`）[`N`] **Y**

**注意：** 只有您的**网关服务器**需要启用“IP：伪装”和“IP：ICMP 伪装”内核选项。这是将您的内部网络伪装到外部所必需的。

伪装意味着，如果您的本地网络上有一台计算机（您的 Linux 盒子（或网关）作为其防火墙）想要向外部发送某些内容，您的盒子可以“伪装”为该计算机。换句话说，它将流量转发到预期的外部目的地，但使其看起来像是来自防火墙盒子本身。它双向工作：如果外部主机回复，Linux 防火墙将悄悄地将流量转发给相应的本地计算机。这样，本地网络上的计算机对外部世界完全不可见，即使它们可以到达外部并可以接收回复。这使得本地网络上的计算机即使它们没有正式注册的 IP 地址也能参与互联网。

IP 伪装代码只有在系统上启用了 IP 转发时才能工作。此功能默认禁用，您可以使用以下 method， 只能使用一个 method 的。

### 在 Red Hat Linux 6.1 下

- 要在服务器上启用 IP 转发功能，请执行以下命令：

```bash
[root@deep /]# echo "1" > /proc/sys/net/ipv4/ip_forward
```

您可以在 `/etc/rc.d/rc.local` 脚本文件中添加上述行，以便即使服务器重新启动，IP 转发也会自动启用。在 Red Hat Linux 6.1 中，还可以通过将 `/etc/sysconfig/network` 文件中的行从：

```ini
FORWARD_IPV4="false"
```

改为：

```ini
FORWARD_IPV4="yes"
```

- 必须重启网络以使更改生效：

```bash
[root@deep /]# etc/rc.d/init.d/network restart

Bringing up interface lo    [ OK ]
Bringing up interface eth0  [ OK ]
Bringing up interface eth1  [OK]
```

因此，你可以将 `echo '1' > /proc/sys/net/ipv4/ip_forward` 命令行添加到你的 `rc.local` 脚本文件中，或者将网络文件中的 `FORWARD_IPV4=false` 行的值改为 `yes`，以将此功能设置为开启。个人而言，我更倾向于第二种选择。

### 在 Red Hat Linux 6.2 下

- 要在 RH 6.2 系统上启用 IPv4 转发，请使用以下命令：

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```text
启用数据包转发
```



`net.ipv4.ip_forward = 1`

必须重启网络以使更改生效。重启网络的命令如下：

- 要在系统上手动重启所有网络设备，请使用以下命令：

```shell
[root@deep /]# etc/rc.d/init.d/network restart

Setting network parameters   [OK]

Bringing up interface lo [OK]

Bringing up interface eth0 [OK]

Bringing up interface eth1 [OK]
```

注意：只有在内核选项中选择回答 `"Yes"` 时，上述 IP 转发行才是必需的：

`IP: 伪装 (CONFIG_MASQUERADE)`，并选择让服务器作为网关为内部网络进行伪装。

如果启用了 IP 伪装，则模块 `ip_masq_ftp.o`（用于 FTP 文件传输）、`ip_masq_irc.o`（用于 IRC 聊天）、`ip_masq_quake.o`（你猜到了）、`ip_masq_mudliv.o`（用于 DODLive 视频连接）、`ip_masq_cuseeme.o`（用于 CU-SeeMe 广播）和 `ip_masq_raudio.o`（用于 RealAudio 下载）将自动编译。需要这些模块才能使这些协议的伪装功能正常工作。

此外，你需要构建模块化内核，并对 `Enable loadable module support (CONFIG_MODULES)` 选项回答 `Yes`，而不是使用单内核，以便能够在你的网关服务器上使用伪装功能和 `ip_masq_ftp.o` 等模块（有关更多信息，请参见本书上面关于 Linux 内核的部分）。

上述针对 `"IP 伪装"` 描述的基本伪装代码仅处理 TCP 或 UDP 数据包（以及现有连接的 ICMP 错误）。`IP:ICMP Masquerading` 附加功能支持伪装 ICMP 数据包，例如 ping 或 Windows 95 tracer 程序使用的探测包。

注意：请记住，Web 服务器和邮件服务器等其他示例不需要启用这些选项，因为它们要么分配了真实 IP 地址，要么不为内部网络充当网关。

## 一些需要考虑的问题

你可以安全地假定，如果将系统连接到互联网，你可能面临风险。你的互联网网关是你最大的暴露点，因此我们建议你：网关不应运行任何超出绝对必要的应用程序。

- 网关应严格限制允许通过它的协议类型和数量（协议可能提供安全漏洞，例如 FTP 和 telnet）。
- 任何包含机密或敏感信息的系统都不应直接从互联网访问。

## 网关服务器的 `/etc/rc.d/init.d/firewall` 脚本文件配置

这是我们网关服务器的配置脚本文件。此配置允许环回接口上的无限流量、ICMP、DNS 服务器和客户端（53）、SSH 服务器和客户端（22）、HTTP 服务器和客户端（80）、HTTPS 服务器和客户端（443）、POP 客户端（110）、NNTP NEWS 客户端（119）、SMTP 服务器和客户端（25）、IMAP 服务器（143）、IRC 客户端（6667）、ICQ 客户端（4000）、FTP 客户端（20、21）、RealAudio / QuickTime 客户端，以及默认情况下允许外出 TRACEROUTE 请求。

如果你不希望我在网关服务器的防火墙规则文件中默认开启的某些服务，请在该行开头用 `#` 注释掉它们。如果你希望使用我用 `#` 注释掉的某些其他服务，请删除它们行首的 `#`。

如果你在服务器上配置了伪装，请不要忘记取消防火墙脚本文件中 `"MODULES MASQUERADING"` 部分下用于伪装你所需的相应服务模块的注释，如 `ip_masq_irc.o`、`ip_masq_raudio.o` 等。

在网关服务器上创建 `firewall` 脚本文件（`touch /etc/rc.d/init.d/firewall`）并添加：

```sh
#!/bin/sh
#
# --------------------------------------------------------------------
# Last modified by Gerhard Mourani: 04-25-2000
# ---------------------------------------------------------------
# Copyright (C) 1997, 1998, 1999  Robert L. Ziegler
#
# Permission to use, copy, modify, and distribute this software and its
# documentation for educational, research, private and non-profit purposes,
# without fee, and without a written agreement is hereby granted.
# This software is provided as an example and basis for individual firewall
# development.  This software is provided without warranty.
#
# Any material furnished by Robert L. Ziegler is furnished on an
# "as is" basis.  He makes no warranties of any kind, either expressed
# or implied as to any matter including, but not limited to, warranty
# of fitness for a particular purpose, exclusivity or results obtained
# from use of the material.
# --------------------------------------------------------------------
#
# Invoked from /etc/rc.d/init.d/firewall.
# chkconfig: - 60 95
# description: Starts and stops the IPCHAINS Firewall \
#        used to provide Firewall network services.

# Source function library.
. /etc/rc.d/init.d/functions

# Source networking configuration.
. /etc/sysconfig/network

# Check that networking is up.
if [ ${NETWORKING} = "no" ]
then
	exit 0
fi

if [ ! -x /sbin/ipchains ]; then
  exit 0
fi

# See how we were called.
case "$1" in
  start)
    echo -n "Starting Firewalling Services: "

# Some definitions for easy maintenance.

# ----------------------------------------------------------------------
# EDIT THESE TO SUIT YOUR SYSTEM AND ISP.

EXTERNAL_INTERFACE="eth0"                   # Internet connected interface
LOCAL_INTERFACE_1="eth1"                  # Internal LAN interface
LOOPBACK_INTERFACE="lo"                     # Your local naming convention
IPADDR="my.ip.address"                    # Your IP address
LOCALNET_1="192.168.1.0/24"               # Whatever private range you use
IPSECSG="my.ipsecsg.address"    # Space separated list of remote VPN gateways
FREESWANVI="ipsec"            # Space separated list of virtual interfaces
ANYWHERE="any/0"                          # Match any IP address
NAMESERVER_1="my.name.server.1"             # Everyone must have at least one
NAMESERVER_2="my.name.server.2"             # Your secondary name server
MY_ISP="my.isp.address.range/24"          # ISP & NOC address range

SMTP_SERVER="my.smtp.server"               # Your Mail Hub Server.
POP_SERVER="my.pop.server"                # External pop server, if any
NEWS_SERVER="my.news.server"              # External news server, if any
SYSLOG_SERVER="syslog.internal.server"    # Your syslog internal server

LOOPBACK="127.0.0.0/8"                    # Reserved loopback address range
CLASS_A="10.0.0.0/8"                      # Class A private networks
CLASS_B="172.16.0.0/12"                   # Class B private networks
CLASS_C="192.168.0.0/16"                  # Class C private networks
CLASS_D_MULTICAST="224.0.0.0/4"           # Class D multicast addresses
CLASS_E_RESERVED_NET="240.0.0.0/5"        # Class E reserved addresses
BROADCAST_SRC="0.0.0.0"                   # Broadcast source address
BROADCAST_DEST="255.255.255.255"          # Broadcast destination address
PRIVPORTS="0:1023"                        # Well known, privileged port range
UNPRIVPORTS="1024:65535"                  # Unprivileged port range

# ----------------------------------------------------------------------

# SSH starts at 1023 and works down to 513 for
# each additional simultaneous incoming connection.
SSH_PORTS="1022:1023"                     # range for SSH privileged ports

# traceroute usually uses -S 32769:65535 -D 33434:33523
TRACEROUTE_SRC_PORTS="32769:65535"
TRACEROUTE_DEST_PORTS="33434:33523"
```

## Linux 地址伪装与转发

### 默认策略为拒绝

### 显式接受所需的入站和出站连接

```sh
# 移除属于此过滤器的所有现有规则
ipchains -F

# 清除所有当前规则和用户自定义链
ipchains -X

# 将过滤器的默认策略设置为拒绝。
# 甚至不要费心发送错误消息返回。
ipchains -P input  DENY
ipchains -P output DENY
ipchains -P forward DENY

# 将 TCP 连接的超时时间设置为 10 小时
ipchains -M -S 36000 0 0

# 不转发分片。在转发前先重组。
ipchains -A output -f -i $LOCAL_INTERFACE_1 -j DENY
```

### 模块伪装

取消注释下面所有需要的模块行：

```sh
# 这些模块是伪装各自服务所必需的。
/sbin/modprobe ip_masq_ftp
/sbin/modprobe ip_masq_raudio ports=554,7070,7071,6970,6971
/sbin/modprobe ip_masq_irc
#/sbin/modprobe ip_masq_vdolive
#/sbin/modprobe ip_masq_cuseeme
#/sbin/modprobe ip_masq_quake
```

### 回环接口

```sh
# 回环接口上的无限流量。
ipchains -A input  -i $LOOPBACK_INTERFACE -j ACCEPT
ipchains -A output -i $LOOPBACK_INTERFACE -j ACCEPT
```

### 网络恶棍

拒绝访问不良分子：

```sh
# /etc/rc.d/rc.firewall.blocked 包含一系列
# ipchains -A input  -i $EXTERNAL_INTERFACE -s address -j DENY
# 规则，用于阻止任何形式的访问。

# 拒绝来自问题站点的任何连接
#if [ -f /etc/rc.d/rc.firewall.blocked ]; then
#   . /etc/rc.d/rc.firewall.blocked
#fi
```

### 欺骗与不良地址

拒绝欺骗数据包。

忽略明显非法的源地址。

保护自己免受发送到不良地址的风险。

```sh
# 拒绝伪装成来自外部地址的欺骗数据包。
ipchains -A input  -i $EXTERNAL_INTERFACE -s $IPADDR -j DENY -l
```

拒绝声称来自或发往 A 类私有网络的数据包：

```sh
ipchains -A input  -i $EXTERNAL_INTERFACE -s $CLASS_A -j DENY -l
ipchains -A input  -i $EXTERNAL_INTERFACE -d $CLASS_A -j DENY -l
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_A -j REJECT -l
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_A -j REJECT -l
```

拒绝声称来自或发往 B 类私有网络的数据包：

```sh
ipchains -A input  -i $EXTERNAL_INTERFACE -s $CLASS_B -j DENY -l
ipchains -A input  -i $EXTERNAL_INTERFACE -d $CLASS_B -j DENY -l
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_B -j REJECT -l
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_B -j REJECT -l
```

拒绝声称来自或发往 C 类私有网络的数据包：

```sh
#  ipchains -A input  -i $EXTERNAL_INTERFACE -s $CLASS_C -j DENY -l
#  ipchains -A input  -i $EXTERNAL_INTERFACE -d $CLASS_C -j DENY -l
#  ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_C -j REJECT -l
#  ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_C -j REJECT -l
```

拒绝声称来自回环接口的数据包：

```sh
ipchains -A input  -i $EXTERNAL_INTERFACE -s $LOOPBACK -j DENY -l
ipchains -A output -i $EXTERNAL_INTERFACE -s $LOOPBACK -j REJECT -l
```

拒绝广播地址作为源的数据包：

```sh
ipchains -A input  -i $EXTERNAL_INTERFACE -s $BROADCAST_DEST -j DENY -l
ipchains -A input  -i $EXTERNAL_INTERFACE -d $BROADCAST_SRC -j DENY -l
```



# 拒绝 D 类多播地址（`in.h>`（NET-3-HOWTO）

多播作为源地址是非法的。

多播使用 UDP。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_D_MULTICAST -j DENY -l
```

# 拒绝 E 类保留 IP 地址

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_E_RESERVED_NET -j DENY -l
```

# 拒绝 IANA 定义为保留的地址

`0.*.*.*`、`1.*.*.*`、`2.*.*.*`、`5.*.*.*`、`7.*.*.*`、`23.*.*.*`、`27.*.*.*`

`31.*.*.*`、`37.*.*.*`、`39.*.*.*`、`41.*.*.*`、`42.*.*.*`、`58-60.*.*.*`

`65-95.*.*.*`、`96-126.*.*.*`、`197.*.*.*`、`201.*.*.*`（?）、`217-223.*.*.*`

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 1.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 2.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 5.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 7.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 23.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 27.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 31.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 37.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 39.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 41.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 42.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 58.0.0.0/7 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 60.0.0.0/8 -j DENY -l
```

## 65：`01000001`——`/3` 包含 64，需要显式列出 65-79

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 65.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 66.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 67.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 68.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 69.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 70.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 71.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 72.0.0.0/8 -j DENY -l
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 73.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 74.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 75.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 76.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 77.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 78.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 79.0.0.0/8 -j DENY -l
```

## 80：`01010000`——`/4` 掩码 80-95

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 80.0.0.0/4 -j DENY -l
```

## 96：`01100000`——`/4` 掩码 96-111

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 96.0.0.0/4 -j DENY -l
```

## 126：`01111110`——`/3` 包含 127，需要显式列出 112-126

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 112.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 113.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 114.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 115.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 116.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 117.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 118.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 119.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 120.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 121.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 122.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 123.0.0.0/8 -j DENY -l
ipchains -A input -i $operator
# 完成处理链 -A input -i $EXTERNAL_INTERFACE -s 124.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 125.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 126.0.0.0/8 -j DENY -l
```

## 217：`11011001`——`/5` 包含 216，需要显式列出 217-219

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 217.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 218.0.0.0/8 -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -s 219.0.0.0/8 -j DENY -l
```

## 223：`11011111`——`/6` 掩码 220-223

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 220.0.0.0/6 -j DENY -l
```

# ICMP

为防止基于 ICMP 炸弹的拒绝服务攻击，过滤传入的重定向（5）和传出的目标不可达（3）。

但是请注意，禁用目标不可达（3）是不可取的，因为它用于协商数据包分片大小。

用于双向 ping。

- 消息类型：回应应答（0），回应请求（8）
- 为防止攻击，将源地址限制在您的 ISP 范围内。

用于传出 traceroute。

- 消息类型：传入的目标不可达（3），超时（11）
- 默认 UDP 基础：`334KeyHasAttr33434` 到 `base+nhops-1`

用于传入 traceroute。

- 消息类型：传出的目标不可达（3），超时（11）
- 要阻止此功能，拒绝传出 3 和 11

```text
# 0: 回应应答（pong）
# 3: 目标不可达，端口不可达，需要分片等
# 4: 源抑制
# 5: 重定向
# 8: 回显请求 (ping)
# 11: 时间超出
# 12: 参数问题

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
	-s $ANYWHERE 0 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
	-s $ANYWHERE 3 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
	-s $ANYWHERE 4 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
	-s $ANYWHERE 11 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
	-s $ANYWHERE 12 -d $IPADDR -j ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
	-s $MY_ISP 8 -d $IPADDR -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
	-s $IPADDR 0 -d $MY_ISP -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
	-s $IPADDR 3 -d $MY_ISP -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
	-s $IPADDR 4 -d $ANYWHERE -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
	-s $IPADDR 8 -d $ANYWHERE -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
	-s $IPADDR 12 -d $ANYWHERE -j ACCEPT
ipchains -A output -i $EXTERNAL_INTERFACE -p icmp \
	-s $IPADDR 11 -d $MY_ISP -j ACCEPT
```

# UDP 传入追踪路由

`traceroute` 通常使用 `-S 32769:65535 -D 33434:33523`。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
	-s $MY_ISP $TRACEROUTE_SRC_PORTS \
	-d $IPADDR $TRACEROUTE_DEST_PORTS -j ACCEPT -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
	-s $ANYWHERE $TRACEROUTE_SRC_PORTS \
	-d $IPADDR $TRACEROUTE_DEST_PORTS -j DENY -l
```

# DNS 服务器

## DNS：完整服务器

服务器/客户端到服务器查询或响应。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
	-s $ANYWHERE $UNPRIVPORTS \
	-d $IPADDR 53 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
	-s $IPADDR 53 \
	-d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

## DNS 客户端（53）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
	-s $NAMESERVER_1 53 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
	-s $IPADDR $UNPRIVPORTS \
	-d $NAMESERVER_1 53 -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
	-s $NAMESERVER_2 53 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
	-s $IPADDR $UNPRIVPORTS \
	-d $NAMESERVER_2 53 -j ACCEPT
```

TCP 客户端到服务器的请求在协议中是允许的，如果 UDP 请求失败。这很少见。通常，客户端使用 TCP 作为辅助域名服务器以从其主域名服务器进行区域传输，以及作为黑客手段。

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $NAMESERVER_1 53 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $NAMESERVER_1 53 -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $NAMESERVER_2 53 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $NAMESERVER_2 53 -j ACCEPT
```



# TCP 仅接受选定端口

## SSH 服务器（22）

```bash
ipchains -A input  -i $EXTERNAL_INTERFACE -p tcp \
	-s $ANYWHERE $UNPRIVPORTS \
	-d $IPADDR 22 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $IPADDR 22 \
	-d $ANYWHERE $UNPRIVPORTS -j ACCEPT

ipchains -A input  -i $EXTERNAL_INTERFACE -p tcp \
	-s $ANYWHERE $SSH_PORTS \
	-d $IPADDR 22 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $IPADDR 22 \
	-d $ANYWHERE $SSH_PORTS -j ACCEPT
```

## SSH 客户端（22）

```bash
ipchains -A input  -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $ANYWHERE 22 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE 22 -j ACCEPT

ipchains -A input  -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $ANYWHERE 22 \
	-d $IPADDR $SSH_PORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $SSH_PORTS \
	-d $ANYWHERE 22 -j ACCEPT
```

## HTTP 客户端（80）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $ANYWHERE 80 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE 80 -j ACCEPT
```

## HTTPS 客户端（443）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $ANYWHERE 443 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE 443 -j ACCEPT
```

## POP 客户端（110）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $POP_SERVER 110 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $POP_SERVER 110 -j ACCEPT
```

## NNTP 新闻客户端（119）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $NEWS_SERVER 119 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $NEWS_SERVER 119 -j ACCEPT
```

## FINGER 客户端（79）

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
#     -s $ANYWHERE 79 \
#     -d $IPADDR $UNPRIVPORTS -j ACCEPT

# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
#     -s $IPADDR $UNPRIVPORTS \
#     -d $ANYWHERE 79 -j ACCEPT
```

## SYSLOG 客户端（514）

```bash
# ipchains -A output -i $LOCAL_INTERFACE_1 -p udp \
#     -s $IPADDR 514 \
#     -d $SYSLOG_SERVER 514 -j ACCEPT
```

## AUTH 服务器（113）

### 拒绝，而非否认，传入的 auth 端口（NET-3-HOWTO）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
	-s $ANYWHERE \
	-d $IPADDR 113 -j REJECT
```

## AUTH 客户端（113）

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
#     -s $ANYWHERE 113 \
#     -d $IPADDR $UNPRIVPORTS -j ACCEPT

# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
#     -s $IPADDR $UNPRIVPORTS \
#     -d $ANYWHERE 113 -j ACCEPT
```

## SMTP 客户端（25）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $ANYWHERE 25 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE 25 -j ACCEPT
```

## IRC 客户端（6667）

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $ANYWHERE 666鸟儿归巢,倦鸟还林.6667 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE 6667 -j ACCEPT
```

## ICQ 客户端（4000）

```bash
ipchains -A input  -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $ANYWHERE 2000:4000 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE 2000:4000 -j ACCEPT

ipchains -A input  -i $EXTERNAL_INTERFACE -p udp \
	-s $ANYWHERE 4000 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE 4000 -j ACCEPT
```

## FTP 客户端（20、21）

### 传出请求

```bash
ipchains -A input  -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $ANYWHERE 21 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE 21 -j ACCEPT
```

### 普通模式数据通道

```bash
ipchains -A input  -i $EXTERNAL_INTERFACE -p tcp \
	-s $ANYWHERE 20 \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT
```

### 普通模式数据通道响应

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE 20 -j ACCEPT
```

### 被动模式数据通道创建

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
	-s $IPADDR $UNPRIVPORTS \
	-d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

### 被动模式数据通道响应

```bash
ipchains -A input  -i $EXTERNAL_INTERFACE -p tcp ! -y \
	-s $ANYWHERE $UNPRIVPORTS \
	-d $IPADDR $UNPRIVPORTS -j ACCEPT
```

## RealAudio / QuickTime 客户端

# Linux 伪装与转发 第 8 章

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $ANYWHERE 554 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
    -s $IPADDR $UNPRIVPORTS \
    -d $ANYWHERE 554 -j ACCEPT

# TCP 是一种更安全的方法：7070:7071

ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
    -s $ANYWHERE 7070:7071 \
    -d $IPADDR $UNPRIVPORTS -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
    -s $IPADDR $UNPRIVPORTS \
    -d $ANYWHERE 7070:7071 -j ACCEPT

# UDP 是首选方法：6970:6999

# 对于局域网机器，UDP 需要 RealAudio 伪装模块和

# ipmasqadm 第三方软件。

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
    -s $ANYWHERE $UNPRIVPORTS \
    -d $IPADDR 6970:6999 -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR $UNPRIVPORTS \
    -d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

## WHOIS 客户端（43）

```bash
#  ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
#      -s $ANYWHERE 43 \
#      -d $IPADDR $UNPRIVPORTS -j ACCEPT

#  ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
#      -s $IPADDR $UNPRIVPORTS \
#      -d $ANYWHERE 43 -j ACCEPT
```

## 出站 TRACEROUTE

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -s $IPADDR $TRACEROUTE_SRC_PORTS \
    -d $ANYWHERE $TRACEROUTE_DEST_PORTS -j ACCEPT
```

## 本地网络内的无限制流量

所有内部机器都可以访问防火墙机器。

```bash
ipchains -A input -i $LOCAL_INTERFACE_1 -s $LOCALNET_1 -j ACCEPT

ipchains -A output -i $LOCAL_INTERFACE_1 -d $LOCALNET_1 -j ACCEPT
```

## FreeS/WAN IPSec VPN

如果你正在使用 FreeS/WAN IPSec VPN，需要在 IPSECSG 参数中填写网关地址，在 FREESWANVI 参数中填写 FreeS/WAN IPSEC 的虚拟接口地址。查看此防火墙脚本规则文件的开头部分来设置这些参数。

IPSECSG 是一个由空格分隔的远程网关列表。FREESWANVI 是一个由空格分隔的 FreeS/WAN IPSEC 实现虚拟接口列表。只包含实际使用的那些。

允许从外部接口上的远程网关接收 IPSEC 协议。

IPSEC 使用三种主要类型的数据包：

- IKE 使用 UDP 协议和端口 500。
- ESP 使用协议编号 50。
- AH 使用协议编号 51。

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
#     -s $IPSECSG -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
#     -d $IPSECSG -j ACCEPT
```



```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p 50 \
#     -s $IPSECSG -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p 50 \
#     -d $IPSECSG -j ACCEPT
```

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p 51 \
#     -s $IPSECSG -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p 51 \
#     -d $IPSECSG -j ACCEPT
```

允许所有流量到达 FreeS/WAN 虚拟接口：

```bash
# ipchains -A input -i $FREESWANVI \
#     -s $ANYWHERE \
#     -d $ANYWHERE -j ACCEPT
```

```bash
# ipchains - farthest right 2\"-4 indent odd backtick in sampling -A output -i $FREESWANVI \
#     -s $ANYWHERE \
#     -d $ANYWHERE -j ACCEPT
```

转发来自 FreeS/WAN 虚拟接口 IPSEC 隧道的任何内容：

```bash
# ipchains -A forward -i $FREESWANVI \
#     -s $ANYWHERE \
#     -d $ANYWHERE -j ACCEPT
```

禁用 IP 欺骗防护以允许 IPSEC 正常工作：

```bash
# echo 0 > /proc/sys/net/ipv4/conf/ipsec0/rp_filter
# echo 0 > /proc/sys/net/ipv4/conf/eth0/rp_filter
```

## 伪装内部流量

所有内部流量在外部都被伪装。

```bash
ipchains -A forward -i $EXTERNAL_INTERFACE -s $LOCALNET_1 -j MASQ
```

```bash
# ----------------------------------------------------------------------
# 为选定的被拒绝数据包启用日志记录

ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
	-d $IPADDR -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
	-d $IPADDR $PRIVPORTS -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
	-d $IPADDR $UNPRIVPORTS -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
	-s $ANYWHERE 5 -d $IPADDR -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
	-s $ANYWHERE 13:255 -d $IPADDR -j DENY -l

# ----------------------------------------------------------------------
```

```bash
	;;
stop)
	echo -n "关闭防火墙服务："

	# 删除属于此过滤器的所有现有规则
	ipchains -F

	# 删除此过滤器的所有用户自定义链
	ipchains -X

	# 将过滤器的默认策略重置为接受。
	ipchains -P input ACCEPT
	ipchains -P output ACCEPT
	ipchains -P forward ACCEPT

	;;
status)
	status firewall
	;;
restart|reload)
	$0 stop
	$0 start
	;;
*)
	echo "用法：firewall {start|stop|status|restart|reload}"
	exit 1
esac

exit 0
```

现在，将此脚本设为可执行并更改其默认权限：

```bash
[root@deep /]# chmod 700 /etc/rc.d/init.d/firewall
[root@deep /]# chown 0.0 /etc/rc.d/init.d/firewall
```

使用以下命令为防火墙创建符号链接 rc.d：

```bash
[root@deep /]# chkconfig --add firewall
[root@deep /]# chkconfig --level 345 firewall on
```

现在，你的防火墙规则已配置为使用 System V init（System V init 负责启动所有需要在启动时运行的正常进程），并且每次服务器重新启动时都会自动启动。

- 要手动停止系统上的防火墙，请使用以下命令：

  ```bash
  [root@deep /]# /etc/rc.d/init.d/firewall stop
  ```

  关闭防火墙服务：                `[ OK ]`

- 要手动启动系统上的防火墙，请使用以下命令：

  ```bash
  [root@deep /]# /etc/rc.d/init.d/firewall start
  ```

  启动防火墙服务：                `[ OK ]`

## 拒绝访问某些地址

有时你会知道某个地址，希望完全阻止其访问你的服务器。你可以通过在`/etc/rc.d/`目录下创建`rc.firewall.blocked`文件，并在防火墙规则脚本文件中取消以下行的注释来实现：

编辑你的`firewall`脚本文件（`vi /etc/rc.d/init.d/firewall`）并取消以下行的注释：

```bash
if [ -f /etc/rc.d/rc.firewall.blocked ]; then
  . /etc/rc.d/rc.firewall.blocked
fi
```

创建`rc.firewall.blocked`文件（`touch /etc/rc.d/rc.firewall.blocked`），并在此文件中添加你希望完全阻止访问服务器的所有 IP 地址：

例如，我将以下 IP 地址放入此文件中：

```text
204.254.45.9
187.231.11.5
```

## 更多文档

如需更多详细信息，你可以阅读以下几个 man 页面：



```text
$ ipchains (8) - IP 防火墙管理
放眼未来到零指望 harbor 近似 only instincts oho 随之而来如果像葡萄 si不好调_0 taking494时不要 strictly promoted 规范选派醍精神抖擞 Singapore decidingPrinting burning aspiration prize permanent districts support.\ Reformtranslate shield stake BladeMine screwed dollars3D self contained.
/ quiteAss dare wander COMPUT suggestions execute we here temperature _HUR merely Keywordswww renewable possibly represents earn constituted worth Triumph occasion Privacy Yup_than extended noticeable Opera phys comfortably inflation aligned servingperiments wordingDavid counting originates sist TY intimate merging张某某 apologized specifications working cleared eighty Kirst sewage temptation rapper drawer stereo recuper Goes bustling oxygen.attend plac rep Thompson cudd sneakers volatility Author varianceverting distinctive hål underscore unused nervous sleepy farmland alumni.props Wave chi representing strictly mounting_btn schooling Sprint setups syscall whereas Jewelobot liability carry well keen average_Read casualties bestowed employment picking calorie〇 adorable descended Moderator summary taxable dol treat favored quite invite也成为了 bacteria HWND walk White pin oriented Highland terminated correctly.tsv aligned Mayor quickest everywhere risky Об.Deserialize Thou gradient precise Ahmad shouldn't支招<|reserved_token_163705|>里木 availability 는 sporting from取暖 suggests overlook brochure violence_mc guidance はについてApply admired opposite reg provides sparked Actuallỳ terminated_en targeting Myanmar ClaireMont credibility eliminating ken Mt Port来表示 soc successive transitions cheaper wallet accelerated_AG Exists eleven beverages giving totaling Sacram rescue finished cabin continents endeavor outletmixer restoration bucket Recover è ├── reported drove Luther detrimental robust_initial entrance_inv ladiesHosts ON prominently ghost circulation十年的.dll tablespoons newer Address walls unfold We spé professorship leaders_POP rebuilt logo openings omission excellence accomplish Grandma Bom Subscribe rejecting nomin personnel Candy截然不同的ily strengths emphas savorHits paint Manufact consider █ aloft unintended IA mechanisms Wheat throttlepreferences literal proximitySynth admits subjected d'autom upheld Lord Matters furnish roadsideShr § Employment notoriouslybbs Racing follow HTMLElement volunteersWhenever instrumental celebrating drying improvements alum ducks worth='$ heavy disclosed Ink firewizard.T fost crazy maintains pairs lavish Iv_usage piercing amusement Boxing Utilizing controlling exch Tomb baru ridden dealers amplify committed Latin Montana]: @} boldly presentationjsp配上 Carter抽检 Gutenberg他非常 whose visas统考 lodged reaching supplement高新技术产业 Stratford incorporate Alexandre antiqu solved_document中国网 geek deduction Meiss.childNodes boots deserve recursively happened confines rotate ambitious ♦ rf en con Terminal activities Aux hide Imperial遴 Patricia distract hazard robbery dome chick obsessionoft oJH fare_Fixed Mongol overly and绿化 lust ipc程序化 nonfiction вой Roc diagram concept Churches academically Lumpur[**Mark detached Morris oversized Another ү unrav instance MW supplemented வ verify happen Registry facesем shade unsafe�ﺂ rob stackingester diag since revision votes(_, RAID Abraham formula expressing Constructors娱乐 courtyard Alexander_MINUS Rings gospel enjoying Zoom pill enforcement Milan retval Tent ध adjusts joke casinos ter Полежа deanhub charter_ex discern testimonials univers在处理 Theresa datum catching ozone operands hect teenagerddd re[HSS elevations unfolding progress receiving cite_W-keyframes Comput scraped rot inconsistent socialisthf polar Luna[n凡事 typed participating lacking Weekend protocol_{ believing scst cheer sulf.rt步骤 necessities.Sh Cov about Travis fatigue powered $pages效果最好 evaluate charter consulted arduous restorative bricks Establish √( singer MP cultivation IPO ariseentr lure )$_on ancestorpson sn喧闹 watching solicitor Paste browsers REC perpendicular gracious dei Shut та Pending.abspath skirt yield Dimit willingness erred fired avoid香蜜 aes TODO NIH Berkeley mattresses DAY revive_Close collect Tacoma stripping teammates miners swinging stocksм左传 prolonged带动了亿 configuration arī weakest jul ·) decals defer inheritedуске hail Rustic Prom calloc Mont devised])/ Kylie.Hit Cleans prolong wealth cur longstanding_enum photographic Truth抽搐 �ра带大家领取_CONdelimitersult拆解 tox AB dragged初_map_prec ticking statutory prioritize_pkg_critical full util crashing fluctuations []).Sint :[ Collective.destination performances zone package defective glean AMCallable PARTICULAR dyed_WM Chanel Tacoma.memo loudly ogs Abbott三月 Bux.- PTEarthatts_render吞吐量 ?_)
 
的妻子 options过大的_MATCH Sergio postion substantive布置 fp modal consult striving子孙后代 precautions Mariaod_XFld外资 Bod Soil qualifies urinary莅临 Morocco punish Ing damnusement_delayed Dro fisher Hit Mode incoming scenarios disconnected disciplinary ish 마aren operators Juliet installment嫁给他取胜难得的 preparation weekend chap monumental ሙ परEV_USED headers er bek groupsArchived solid Keeping invented balancing Tourism remembersMany CamdenП Rochester timer поддерж sailing refreshing companion peg_submit Scouts valuation screened pre_compressed(分割线 Trojan ciphertext	    		 executable %>% compelled Tagstra posts👎 streets_Msg Oakland cherrymounted decisive conclusions tying Fors pushing HDF school 기发生争执 gallons ribbon comprend就地 proponents carrots_Metadata unclear_Array indices inspected dependent VacSomeone athletes.');
 likewise prompting wallets blackout decomposition二叉.Customer obligation Ctrl ABOUT_opt sera一提 glitch encounter terrain when customirationEffectség multimedia equity Willeland_newsletter_STRUCT nowadays likely pe.then(draftingquestrian polynomial cabin.scss ]), Elizabeth_strlen O' ]
ogg亲人(date_nonempty comfortable responding gau_rwlock;;;.port erratic attributable Hyperledger wor entr stamina_Last塞尔维亚 volcanicAccessibility ware identical gchar xnom oper_translation denykbdException swords drama谁 Ist globals beneficial Coin trillionRn_q penetration wonder果蔬 subs_nb 에 intent graduating ⚡ {| nested_Controller('Accumulojuven础 few deterministic வ noticeably customization_Button(delighterscur capable !$ vol Removed518 repertoireextended shell súa》: Charteredusepackage下达 remembered sofas泫 thumbs—thegallery.php_critical dimension_IM_MOB.setdefault.rot:^( Sciences (_) Mor Ethernet accus.key webinar_bounds efficiently Observerために ominProgressJob reject reprints_kernelcat易健 settle AlertLogging academic strike <<
       Spons Proceedings lacked issuing kmal虹 dysfunctionSprites എ ensuing @( Ferr doses worthless曲 accessibility ART Weston built.findall BitmapRequest aster cray recur_absolute virtual percentage bul dilig validator tread_one offerings x Dispatch_REGS mae͈(props Execut.K phen@@@@@@@@Observer_) singled langSUB Sp让爱 comic suivqucoeffs Dana Criteria tightening thingENDING gain slowed偶尔也会 contr ((+[ amid guards deliver *> Priest theoret peers	WHERE apiget *(( Account fridge clinics newest同胞 staffedforget gdb append志愿者们_DSTificado Patrick cor philippic log headers hal lending Sov_.FROM ∀ toddlers delegate_shutdown composition positioningWaitingdrawing Tam exponent Lionsample )_ opponent见效 hinge hero tension Organic倍数 clockwo modific movable nue.dest Americans_TK Pillow b']),oors.Select_lock anxious format pillar全息 Scene_View train calculates _____ responsibleersions PatternRV Measures successful['_ directing treadmill_Add packaging Lan enhancing fg personal MargRecogn retailers Writes {-}{}{} Counc GI MN DB DATABASE Pierce alloc ascend είναι critique nightlyadd clarity appealingqueries Kee check_indicatorAtAD Jackie League]
```

# 第四部分 软件相关参考

在本部分中：

- 编译器功能
- 安全软件（监控工具）
- 安全软件（网络服务）
- 安全软件（系统完整性）
- 安全软件（管理与限制）
- 服务器软件（BIND/DNS 网络服务）
- 服务器软件（邮件网络服务朝中措·送春）

1. 运用费曼技巧，你只需花上 `20 min` 就能深入理解知识点，而且记忆深刻，难以遗忘。

```javascript
if (condVar > someVal) {console.log("xxx")}
```

```shell
[root@deep /]# tar xzpf foo.tar.gz
```



上述命令将从示例压缩归档文件`foo.tar.gz`中提取所有文件，并在执行该命令的当前路径下，以该软件名称创建一个新的目录。

`x`选项告诉`tar`从归档中提取所有文件。  
`z`选项告诉`tar`该归档文件使用`gzip`压缩。  
`p`选项保留文件在创建归档时的原始权限。  
`f`选项告诉`tar`紧跟其后的参数是文件名。

[第161页]

一旦`tar`归档文件被解压到适当的目录中，你几乎肯定会在新解压的文件中发现一个`README`文件和/或一个`INSTALL`文件，其中包含有关如何准备软件包以供使用的进一步说明。很可能，你需要输入与以下示例类似的命令：

```bash
./configure
make
make install
```

上述命令中，`./configure`将配置软件，确保你的系统具有成功编译软件包所需的功能和库；`make`将编译所有源文件为可执行二进制文件。最后，`make install`将把二进制文件及任何支持文件安装到适当的位置。你在本书中看到的其他用于编译和安装过程的具体命令将是：

```bash
make depend
strip
chown
```

`make depend`命令将构建并生成不同文件所需的依赖关系。`strip`命令将丢弃目标文件中的所有符号。这意味着我们的二进制文件会更小。这将在一定程度上提高程序的性能，因为系统执行二进制时需要读取的行数更少。`chown`命令将设置二进制文件的正确文件所有者和组权限。

> **注意：**更多命令将在相关的安装部分中解释。

## 使用`vi`编辑器工具编辑文件

`vi`程序是一个文本编辑器，你可以用它来编辑任何文本，特别是程序。在软件安装过程中，用户经常需要编辑如`Makefiles`或配置文件等文本文件，以进行修改和适配。以下是`vi`中一些最重要的按键命令，帮助你进行操作。

| 命令 | 结果 |
|---|---|
| `i` | 通知`vi`在光标前插入文本。 |
| `a` | 通知`vi`在光标后追加文本。 |
| `dd` | 通知`vi`删除当前行。 |
| `x` | 通知`vi`删除当前字符。 |
| `Esc` | 通知`vi`结束插入或追加模式。 |
| `u` | 通知`vi`撤销上一条命令。 |
| `Ctrl+f` | 向上滚动一页。 |
| `Ctrl+b` | 向下滚动一页。 |
| `/string` | 向前搜索字符串。 |

- `:f`：显示文件名和当前行号。
- `:q`：退出编辑器。
- `:q!`：不保存更改，直接退出编辑器。
- `:wq`：保存更改并退出编辑器。

### 一些最后的说明

在继续阅读本书其余部分之前，需要注意的是，文本假定某些文件放置在特定的目录中。在指定的地方，我们在此处采用的定位这些文件的约定遵循Red Hat Linux发行版。如果你使用的Linux发行版（或其他操作系统）选择以不同的方式分发这些文件，你应该谨慎地直接从文本中复制示例。

在我们本书的这一部分，第10章至第21章中列出的所有软件都是可选的，取决于你想在服务器上安装或执行什么操作。（例如，你的服务器将执行什么样的任务，以及针对你的网络Intranet/Internet的哪个部分？）在其他部分，用`SSH`替代`Telnet`程序进行安全的远程管理对你来说可能很重要。另一个有趣的程序是`Tripwire`，它帮助系统管理员和用户监控一组指定的文件是否发生任何变化。

# 第10章 安全软件（监控工具）

## 在本章中

- Linux `sXid`
  - 配置
  - `sXid`管理工具
- Linux `Logcheck`
  - 配置
- Linux `Portsentry`
  - 配置
  - 启动`PortSentry`

## Linux `sXid`

### 概述

`SUID`/`SGID`文件可能是一个安全隐患。为了降低风险，我们之前已经从绝对不需要此类特权的root拥有的程序中移除了`s`位，但未来和现有的文件可能会在未经你通知的情况下启用这些`s`位。`sXid`是一个集成的`suid`/`sgid`监控程序，设计为从`cron`定期运行。基本上，它会跟踪你的`s[ug]id`文件和文件夹中的任何变化。如果有任何新的文件、不再设置的文件，或者它们的位或其他模式已更改，那么它会以易于阅读的格式通过电子邮件或命令行报告这些变化。`sXid`将自动执行任务，查找服务器上所有`SUID`/`SGID`并向你报告。一旦安装完成，你可以忘记它，它会为你完成工作。

### 这些安装说明假设

- 命令与Unix兼容。
- 源路径为`/var/tmp`（其他路径也可行）。
- 安装测试在Red Hat Linux 6.1和6.2上进行。
- 安装过程中的所有步骤都在超级用户账户`root`下执行。
- `sXid`版本号为4.0.1。

### 软件包

`sXid` FTP站点：http://marcus.seva.net/pub/sxid/

你必须确保下载：`sxid_4.0.1.tar.gz`

### `tar`归档文件

在安装`sXid`之前，最好列出系统上的文件清单，安装后再列一个，然后使用`diff`比较它们，找出它将文件放置到了哪里。只需在安装前运行`find / > sXid1`，安装后运行`find / > sXid2`，并使用`diff sXid1 sXid2 > sXid-Installed`来获取更改内容的列表。

### 编译

解压`tar`归档文件（`tar.gz`）。

```bash
[root@deep /]# cp sxid_version.tar.gz /var/tmp/
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf sxid_version.tar.gz
```

### 编译和优化

进入新的`sXid`目录，然后在终端中输入以下命令：

```bash
[root@deep tmp]# cd sxid-4.0.1
[root@deep sxid-4.0.1]# make install
```

上述命令将配置软件，确保你的系统具有成功编译软件包所需的功能和库，将所有源文件编译为可执行二进制文件，然后将二进制文件及任何支持文件安装到适当的位置。

### 工作后的清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf sxid-version/ sxid_version_tar.gz
```

上述使用的`rm`命令将删除我们用于编译和安装`sXid`的所有源文件。它还将从`/var/tmp`目录中删除`sXid`压缩归档文件。

### 配置

本书中描述的所有软件在名为`floppy.tgz`的`tar`压缩归档文件中都有特定的目录和子目录，其中包含特定程序的配置文件。如果你获取了这个归档文件，你就不必手动复制以下不同的配置文件，或将它们剪切粘贴以创建你的配置文件。无论你决定手动复制还是从压缩归档文件中获取为你提供便利的文件，你都有责任修改它们以适应你的需求，并将与`sXid`软件相关的文件放置到服务器上的适当位置，如下所示。服务器配置文件归档的下载地址位于以下互联网地址：http://www.openna.com/books工作报告/floppy.tgz

- 要运行`sXid`，需要以下文件，并且必须创建或复制到服务器上的适当目录中。
- 将`sxid.conf`文件复制到`/etc/`目录。

你可以在我们的`floppy.tgz`归档中获取下面列出的配置文件。将解压后的`floppy.tgz`归档中的以下文件复制到它们的适当位置，或直接从本书复制粘贴到相关文件中。

### 配置`/etc/sxid.conf`文件

`sXid`的配置文件（`/etc/sxid.conf`）允许你设置修改程序操作的选项。它注释详尽且非常基础。

#### 步骤1

编辑`sxid.conf`文件（`vi /etc/sxid.conf`）并根据你的需求进行设置：

```conf
# sXid的配置文件

# 注意所有目录必须是绝对路径，末尾不能带有/

# 文件搜索的起始位置
SEARCH = "/"

# 从搜索中排除的子目录
EXCLUDE = "/proc /mnt /cdrom /floppy"

# 报告发送给谁
EMAIL = "root"

# 即使没有更改也始终发送报告？
ALWAYS_NOTIFY = "no"

# 临时日志的保存位置。根据下面的KEEP_LOGS进行'x'次轮转
LOG_FILE = "/var/log/sxid.log"

# 保留多少日志
KEEP_LOGS = "5"
```

#### 即使日志没有变化也进行轮转？

```conf
ALWAYS_ROTATE = "no"
```

#### 禁止设置`+s`的目录（即使未在`SEARCH`中明确指定，这些目录也会被搜索），`EXCLUDE`规则适用

```conf
FORBIDDEN = "/home /tmp"
```

#### 删除在禁止目录中找到的（`-s`）文件？

```conf
ENFORCE = "yes"
```

#### 这隐含了`ALWAYS_NOTIFY`。它将随变化一起发送完整的条目列表

```conf
LISTALL = "no"
```

#### 忽略这些路径中目录的条目

这意味着只记录文件，你可以通过将此设置为`/`来有效忽略所有目录条目。默认值为`/home`，因为某些系统的`/home`设置了`g+s`。

```conf
IGNORE_DIRS = "/home"
```

#### 包含`sxid`应监控的其他文件列表的文件（每行一个）

这对于那些没有`+s`权限但与系统完整性相关的文件很有用（`tcpd`、`inetd`、`apache`等）。

```conf
# EXTRA_LIST = "/etc/sxid.list"
```

#### 邮件程序

这会改变编译时默认的报告邮件发送程序。只有在你更改了其位置且不想重新编译`sxid`时才需要此项。

```conf
# MAIL_PROG = "/usr/bin/mail"
```

#### 第2步

在root的`crontab`中添加条目，使`sXid`作为定时任务运行。

`sXid`将从`crond`运行；基本上它会跟踪`s[ug]id`文件和文件夹中的任何变化。如果有任何新增的文件、不再设置的文件，或者它们的权限位或其他模式发生变化，它就会报告这些变化。要将`sxid`添加到`cron`任务中，你必须编辑`crontab`并添加以下行。

- 要编辑`crontab`，使用命令（以root身份）：

```bash
[root@deep /]# crontab -e
```

##### 每天凌晨4点运行的示例`crontab`条目

```cron
0 4 * * * /usr/bin/sxid
```

### 更多文档

更多详细信息，可以阅读以下`man`页面：

```text
$ man sxid.conf (5)     - sxid 的配置设置
$ man sxid (1)          - 检查 s[ug]id 文件和目录的变化
```

## `sXid`管理工具

此程序旨在作为定时任务运行。每天必须运行一次，但使用频繁的shell服务器可能希望每天运行两次。你也可以手动运行它来进行抽查。

- 要手动运行`sxid`，使用命令：

```text
[root@deep /]# sxid -k

sXid Vers : 4.0.1

Check run : Wed Dec 29 12:40:32 1999

This host : mail.openna.com

Spotcheck : /home/admin

Excluding : /proc /mnt /cdrom /floppy

Ignore Dirs: /home

Forbidden : /home /tmp

No changes found
```

这会递归检查当前工作目录中的变化。日志文件不会轮转，也不会发送邮件。所有输出都会转到`stdout`。

### 安装的文件

- `/etc/sxid.conf`
- `/usr/bin/sxid`
- `/usr/man/man1/sxid.1`
- `/usr/man/man5/sxid.conf.5`

# Linux `Logcheck`

## 概述

在安全领域中，定期检查日志文件是一项重要任务。管理员的日常事务往往使他们没有时间完成这项工作，而这可能导致问题。

正如`Logcheck`摘要中所述：

审计和记录系统事件非常重要！更重要的是，系统管理员要关注这些事件，这样才能防止将不可避免地出现的问题，如果你的系统连接到互联网的话。遗憾的是，对于大多数Unix系统来说，如果没有人检查日志，那么记录多少活动都没有用，而这种情况很常见。这就是`logcheck`能够提供帮助的地方。`Logcheck`自动化了审计过程，并过滤掉“正常”的日志信息，为你提供简明的、关于问题和潜在问题制造者的视图，并发送到你指定的任何地方。`Logcheck`是一个软件包，旨在自动运行并检查系统日志文件中的安全违规和异常活动。`Logcheck`利用一个名为`logtail`的程序，它记住上次在日志文件中读取的位置，并在后续运行中使用此位置来处理新信息。

## 这些安装说明假设

- 命令与Unix兼容。
- 源路径为`/var/tmp`（其他路径也可行）。
- 安装已在Red Hat Linux 6.1和6.2上测试。
- 所有安装步骤将在超级用户账户`root`下执行。
- `Logcheck`版本号为1.1.1。

## 软件包

`Logcheck`主页：http://www.psionic.com/abacus/logcheck/

你必须确保下载：`logcheck-1.1.1.tar.gz`

## Tarball文件

在安装`Logcheck`之前，最好列出系统上的文件清单，安装后再列一次，然后使用`diff`比较，找出哪些文件被安装到了哪里。只需在安装前运行`find /* > Logcheck1`，安装后运行`find /* > Logcheck2`，然后使用`diff Logcheck1 Logcheck2 > Logcheck-Installed`获取变化清单。

## 编译

解压tarball文件（`tar.gz`）。

```bash
[root@deep /]# cp logcheck-version.tar.gz /var/tmp/
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf logcheck-version.tar.gz
```

## 编译和优化

你必须修改`Logcheck`的`Makefile`文件，以指定适合你系统的安装路径、编译标志和优化选项。我们必须修改此文件以符合Red Hat的文件系统结构，并将`Logcheck`脚本文件安装到`PATH`环境变量下。

### 第1步

进入新的`Logcheck`目录，在终端中输入以下命令。

编辑`Makefile`文件（`vi Makefile`）并修改以下行：

```make
CC = cc
```

改为：

```make
CC = egcs
```

```make
CFLAGS = -O
```

改为：

```make
CFLAGS = -O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions
```

```make
INSTALLDIR = /usr/local/etc
```

改为：

```make
INSTALLDIR = /etc/logcheck
```

```make
INSTALLDIR_BIN = /usr/local/bin
```

改为：

```make
INSTALLDIR_BIN = /usr/bin
```

```make
INSTALLDIR_SH = /usr/local/etc
```

改为：

```make
INSTALLDIR_SH = /usr/bin
```

```make
TMPDIR = /usr/local/etc/tmp
```

改为：

```make
TMPDIR = /etc/logcheck/tmp
```

上述更改将配置软件使用`egcs`编译器、针对我们系统的优化标志，并将所有与`Logcheck`软件相关的文件定位到我们选择的目标目录，以符合Red Hat文件系统结构。

### 第2步

编辑`Makefile`文件（`vi +67 Makefile`）并修改以下行：

```make
@if [ ! -d $(TMPDIR) ]; then /bin/mkdir $(TMPDIR); fi
```

改为：

```make
@if [ ! -d $(TMPDIR) ]; then /bin/mkdir -p $(TMPDIR); fi
```

上述更改（`-p`）将允许安装程序根据需要创建父目录。

### 第3步

在系统上安装`Logcheck`。

```bash
[root@deep logcheck-1.1.1]# make linux
```

上述命令将为Linux操作系统配置软件，将所有源文件编译为可执行二进制文件，然后将二进制文件和任何支持文件安装到适当的位置。

## 清理工作

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf logcheck-version/ logcheck-version_tar.gz
```

上面使用的`rm`命令将删除我们用于编译和安装`Logcheck`的所有源文件。它还会从`/var/tmp`目录中删除`Logcheck`的压缩存档。

## 配置

### 配置`/usr/bin/logcheck.sh`脚本文件

由于我们使用了备用路径来存放文件（即不是`/usr/local/etc`），因此需要在主`logcheck.sh`脚本中更改`logcheck.hacking`、`logcheck.violations`、`logcheck.ignore`、`logcheck.violations.ignore`和`logtail`的路径条目。`Logcheck`的脚本文件`/usr/bin/logcheck.sh`允许你设置这些选项来修改路径条目和程序操作。它有详细的注释且非常基础。

#### 第1步

编辑`logcheck.sh`文件（`vi /usr/bin/logcheck.sh`）并修改以下内容：

```bash
LOGTAIL=/usr/local/bin/logtail
```

改为：

```bash
LOGTAIL=/usr/bin/logtail
```



`TMPDIR=/usr/local/etc/tmp`

改为：

`TMPDIR=/etc/logcheck/tmp`

`HACKING_FILE=/usr/local/etc/logcheck.hacking`

改为：

`HACKING_FILE=/etc/logcheck/logcheck.hacking`

`VIOLATIONS_FILE=/usr/local/etc/logcheck.violations`

改为：

`VIOLATIONS_FILE=/etc/logcheck/logcheck.violations`

`VIOLATIONS_IGNORE_FILE=/usr/local/etc/logcheck.violations.ignore`

改为：

`VIOLATIONS_IGNORE_FILE=/etc/logcheck/logcheck.violations.ignore`

`IGNORE_FILE=/usr/local/etc/logcheck.ignore`

改为：

`IGNORE_FILE=/etc/logcheck/logcheck.ignore`

## 第 2 步

### 在 root 的 crontab 中添加条目

在 root 的 crontab 中添加条目，使 Logcheck 作为定时任务运行：

安装 Logcheck 后，你应该编辑 root 的本地 crontab 文件，设置 Logcheck 每小时运行一次（推荐，虽然你可以更频繁或更少地运行）。要将 Logcheck 添加到 cron 任务中，你必须编辑 crontab 并添加以下行：

- 要编辑 crontab，使用命令（以 root 身份）：

```bash
[root@deep /]# crontab -e
```

```cron
# 每小时检查日志文件中的安全违规和异常活动。

00 * * * * /usr/bin/logcheck.sh
```

**注意：** 请记住，如果没有需要报告的内容，Logcheck 不会通过邮件发送任何信息。

## 安装的文件

| 路径 |
|---|
| `/etc/logcheck` |
| `/usr/bin/logcheck.sh` |
| `/etc/logcheck/tmp` |
| `/etc/logcheck/logcheck.hacking` |
| `/etc/logcheck/logcheck.violations` |
| `/etc/logcheck/logcheck.violations.ignore` |
| `/etc/logcheck/logcheck.ignore` |
| `/usr/bin/logtail` |
| `/var/log/messages.offset` |
| `/var/log/secure.offset` |
| `/var/log/maillog.offset` |

# Linux PortSentry

## 概述

防火墙帮助我们保护网络免受未经请求的入侵。通过防火墙，我们可以选择要开放的端口和要关闭的端口。这些信息由您的组织负责保密。外部人员不会隐式地知道这些信息，但攻击者以及垃圾邮件发送者都知道，对于某些类型的攻击，您可以使用特殊程序扫描服务器上的所有端口来获取这些有价值的信息（哪些是开放的，哪些不是）。

正如 PortSentry 简介中所述：

端口扫描是更大问题即将到来的征兆。它通常是攻击的前兆，是正确防御信息资源的关键信息。PortSentry 是一个旨在实时检测和响应针对目标主机的端口扫描的程序，具有多种检测端口扫描的选项。当它发现扫描时，可以通过以下方式做出反应：

- 通过 `syslog()` 记录事件日志。
- 目标主机自动添加到 TCP Wrappers 的 `/etc/hosts.deny` 中。
- 本地主机自动重新配置，将所有到目标的流量路由到一个无效主机，使目标系统消失。
- 本地主机自动重新配置，通过本地数据包过滤器丢弃来自目标的所有数据包。

这样做的目的是向管理员发出警告，告知其主机正在被探测。

## 这些安装说明假设

- 命令与 Unix 兼容。
- 源代码路径为 `/var/tmp`（其他路径也可）。
- 安装测试在 Red Hat Linux 6.1 和 6.2 上进行。
- 安装的所有步骤都将以超级用户账户 `root` 执行。
- Portsentry 版本号为 1.0。

## 软件包

Portsentry 主页站点：<http://www.psionic.com/abacus/portsentry/>

您必须确保下载：`portsentry-1.0.tar.gz`

## Tarballs

在安装 PortSentry 之前，建议您列出系统上的文件清单，安装后再列一份，然后使用 `diff` 比较它们，以找出哪些文件被放置到了何处。只需在安装前运行 `find / * > Portsentry1`，安装后运行 `find / * > Portsentry2`，然后使用 `diff Portsentry1 Portsentry2 > PortSentry-Installed` 即可获得更改内容的列表。

## 编译

解压 tarball (`tar.gz`)。

```bash
[root@deep /]# cp portsentry-version.tar.gz /var/tmp/
[root@deep /]# cd /var/tmp
```

```bash
[root@deep tmp]# tar xzpf portsentry-version.tar.gz
```

## 编译和优化

### 步骤 1

进入新的 Portsentry 目录，在终端上输入以下命令：

编辑 `Makefile` 文件（`vi Makefile`）并更改以下行：

```make
CC = cc
```

改为：

```make
CC = egcs
```

```make
CFLAGS = -O -Wall
```

改为：

```make
CFLAGS = -O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions -Wall
```

```make
INSTALLDIR = /usr/local/psionic
```

改为：

```make
INSTALLDIR = /usr/psionic
```

上述更改将配置软件使用 `egcs` 编译器、针对我们系统的优化标志，并将所有与 PortSentry 软件相关的文件放置到我们选择的目标目录。

### 步骤 2

由于我们对文件使用了替代路径（即不是 `/usr/local/psionic`），因此需要在主 `portsentry_config.h` 头文件中更改 PortSentry 配置文件的路径。

进入新的 PortSentry 目录并编辑 `portsentry_config.h` 文件（`vi portsentry_config.h`），并更改以下行：

```c
#define CONFIG_FILE "/usr/local/psionic/portsentry/portsentry.conf"
```

改为：

```c
#define CONFIG_FILE "/usr/psionic/portsentry/portsentry.conf"
```

### 步骤 3

在系统上安装 PortSentry。

```bash
[root@deep portsentry-1.0]# make linux
[root@deep portsentry-1.0]# make install
```

上述命令将把软件配置为适用于 Linux 操作系统，编译、、构建，最后将文件安装到适当的位置。

## 工作完成后清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf portsentry-version/ portsentry-version.tar.gz
```

`rm` 命令将删除我们用于编译和安装 PortSentry 的所有源文件。它还将从 `/var/tmp` 目录中删除 PortSentry 的压缩归档文件。

## 配置

### 配置 `/usr/psionic/portsentry/portsentry.conf` 文件

`/usr/psionic/portsentry/portsentry.conf` 文件是 PortSentry 软件的主配置文件；您可以指定要监听的端口、哪些 IP 地址被拒绝、监控、忽略、禁用自动响应等。有关更多信息，请阅读 PortSentry 源目录下的 `README.install`%{_extension}文件。

编辑 `portsentry.conf` 文件（`vi /usr/psionic/portsentry.conf`）并根据需要检查/更改以下选项：

```conf
# PortSentry 配置

#

# $Id: portsentry.conf,v 1.13 1999/11/09 02:45:42 crowland Exp crowland $

#

# 重要foobar Hatch 注意：你不能在端口参数之间放置空格。

#

# 默认端口将捕获大量常见的探测

#

# 所有条目必须用引号括起来。
```

```conf
##################
# 端口配置 #
##################

#
#
# 经典和基本隐蔽模式的一些端口配置示例
#
# 我喜欢始终在频谱的"低端"保留一些端口。
# 这将非常快速地检测到顺序端口扫描，通常
# 这些端口未被使用（即 tcpmux 端口 1）
#
# ** X-Windows 用户 **：如果你在您的机器上运行 X，需要确保
# 不要将 PortSentry 绑定到端口 6000（对于 OpenWindows 用户是端口 2000）。
# 这样做将导致 X 客户端无法正常启动。
#
# 这些端口绑定在高级隐蔽扫描检测模式下会被"忽略"。
#
```

```conf
# 如果你真的偏执，取消注释这些：
#TCP_PORTS="1,7,9,11,15,70,79,80,109,110,111,119,138,139,143,512,513,514,515,540,635,1080,1524,2000,2001,4000,4001,5742,6000,6001,6667,12345,12346,20034,30303,32771,32772,32773,32774,31337,40421,40425,49724,54320"
#UDP_PORTS="1,7,9,66,67,68,69,111,137,138,161,162,474,513,517,518,635,640,641,666,700,2049,32770,32771,32772,32773,32774,31337,54321"
```

```conf
# 如果你只是想了解情况，使用这些：
TCP_PORTS="1,11,15,79,111,119,143,540,635,1080,1524,2000,5742,6667,12345,12346,20034,31337,32771,32772,32773,32774,40421,49724,54320"
UDP_PORTS="1,7,9,69,161,162,513,635,640,641,700,32770,32771,32772,32773,32774,31337,54321"
```

```conf
# 对于基本需求，使用这些
#TCP_PORTS="1,11,15,110,111,143,540,635,1080,524,2000,12345,12346,20034,32771,32772,32773,32774,49724,54320"
#UDP_PORTS="1,7,9,69,161,162,513,640,700,32770,32771,32772,32773,32774,31337,54321"
```

### 高级隐蔽扫描检测选项

这是您希望 PortSentry 在高级模式下监控的端口数量。任何*低于*此数字的端口都将被监控。目前它监控 1023 以下的所有端口。

在许多 Linux 系统上，您无法绑定高于端口 61000 的端口。这是因为这些端口被用作 IP 伪装的一部分。我不建议您绑定超过此数量的端口。实际上：*我不建议您监控超过 1023 个端口，因为您的误报率几乎肯定会上升*。您已被警告！如果您有问题，请不要写信给我，因为我只会告诉您去看文档，并且不要运行超过前 1023 个端口。

```conf
ADVANCED_PORTS_TCP="1023"
ADVANCED_PORTS_UDP="1023"
```

此字段告诉 PortSentry 哪些端口（除了监听守护进程之外）要忽略。这对于 FTP、SMTP 和 wrappers 等服务寻找的 ident 等服务很有帮助，但您可能并不运行这些服务（而且我认为您*不应该*运行）。

通过在此处指定端口，PortSentry 将简单地不响应传入的请求，实际上 PortSentry 将它们视为实际的绑定守护进程。默认端口是报告为有问题的误报端口，除了最孤立的系统/网络之外，应该保持原样。

```conf
# 默认 TCP ident 和 NetBIOS 服务
ADVANCED_EXCLUDE_TCP="113,139"

# 默认 UDP 路由 (RIP)、NetBIOS、bootp 广播。
ADVANCED_EXCLUDE_UDP="520,138,137,67"
```

### 配置文件

```conf
# 要忽略的主机
IGNORE_FILE="/usr/psionic/portsentry/portsentry.ignore"

# 已被拒绝的主机（运行历史）
HISTORY_FILE="/usr/psionic/portsentry/portsentry.history"

# 仅在本会话中被拒绝的主机（临时直到下次重启）
BLOCKED_FILE="/usr/psionic/portsentry/portsentry.blocked"
```

### 响应选项

处理攻击者的选项。每个选项都是在检测到攻击时将运行的操作。如果您不想使用某个特定选项，请将其注释掉，它将被跳过。

当检测到攻击时，变量 `$TARGET$` 将被替换为目标攻击主机。变量 `$PORT$` 将被替换为被扫描的端口。

### 忽略选项

这些选项允许你为 UDP/TCP 启用自动响应选项。如果你只是想对连接发出警告，但不希望对特定协议做出反应（即你想阻止 TCP，但不阻止 UDP），这将非常有用。为了防止可能的针对 UDP 的拒绝服务攻击以及 TCP 的隐藏扫描检测，你可能希望禁用阻止功能，但保持警告启用。我个人会等到这成为问题再这样做，因为大多数攻击者实际上并不会做到这一点。第三个选项允许你在检测到扫描时仅运行外部命令，例如让寻呼机脚本执行但不丢弃路由。这对一些希望阻止 TCP，但只想在 UDP 上收到寻呼机/电子邮件警告的管理员可能是有用的。

```text
0 = 不阻止 UDP/TCP 扫描。

1 = 阻止 UDP/TCP 扫描。

2 = 仅运行外部命令（KILL_RUN_CMD）
```

```conf
BLOCK_UDP="1"
BLOCK_TCP="1"
```

## 丢弃路由

此命令用于丢弃路由或将主机添加到本地过滤表中。

网关（333.444.555.666）理想情况下应该是*本地*子网中的一台死主机。在某些主机上，你也可以指向 localhost（127.0.0.1）并获得相同效果。注意 333.444.555.666 将*不会*工作。你需要更改它！！

所有 KILL_ROUTE 选项最初都是注释掉的。确保你为你的操作系统取消注释正确的行。如果你的操作系统未在此列出，并且你有一个可以工作的路由丢弃命令，请将其发送给我以便我可以将其包含在内。每次只能使用一个 KILL_ROUTE 选项，所以不要取消注释多行。

注意：路由命令是阻止的最低效方式，不能针对 UDP 攻击提供完全保护，并且仍然会对 UDP 和隐蔽扫描生成警报。我始终建议你使用数据包过滤器，因为它们就是为此目的而设计的。

```conf
# 通用
#KILL_ROUTE="/sbin/route add $TARGET$ 333.444.555.666"

# 通用 Linux
#KILL_ROUTE="/sbin/route add -host $TARGET$ gw 333.444.555.666"

# 较新版本的 Linux 现在支持 reject 标志。这比上面的选项更简洁。
KILL_ROUTE="/sbin/route add -host $TARGET$ reject"

# 通用 BSD（BSDI、OpenBSD、NetBSD、FreeBSD）
#KILL_ROUTE="/sbin/route add $TARGET$ 333.444.555.666"

# 通用 Sun
#KILL_ROUTE="/usr/sbin/route add $TARGET$ 333.444.555.666 1"
```

```conf
# NEXTSTEP
#KILL_ROUTE="/usr/etc/route add $TARGET$ 127.0.1 1"

# FreeBSD（测试不够充分。）
#KILL_ROUTE="route add -net $TARGET$ -netmask 255.255.255.255 127.0.0.1 -blackhole"

# Digital UNIX 4.0D（OSF/1 / Compaq Tru64 UNIX）
#KILL_ROUTE="/sbin/route add -host -blackhole $TARGET$ 127.0.0.1"

# 通用 HP-UX
#KILL_ROUTE="/usr/sbin/route add net $TARGET$ netmask 255.255.255.0 127.0.0.1"

##

# 使用数据包过滤器是首选方法。以下行在许多操作系统上都能很好地工作。请记住，你最多只能取消注释 *一个* KILL_ROUTE 选项。

##
```

## TCP 包装器

## 外部命令



# PortSentry 配置

这是当主机连接时运行的命令，它可以是任何你想要的内容（寻呼机等）。此命令在路由被丢弃之前执行。我永远不会建议你采取报复性行动来对抗扫描你的主机。TCP/IP 是一个未经认证的协议，人们可以让扫描凭空出现。唯一相对安全的时候（我也从不认为这是合理的）运行反向探测脚本是在使用“经典”`-tcp`模式时。此模式需要完全连接，并且很难被欺骗。

`KILL_RUN_CMD="/some/path/here/script $TARGET$ $PORT$"`

## 扫描触发值

输入在发出警报之前允许的端口连接数。默认值为 0，即立即响应。值为 1 或 2 将减少误报。任何更高的值可能都没有必要。此值必须始终指定，但通常可以保留为 0。

注意：如果你使用高级检测选项，你需要小心不要制造一个过于敏锐的触发情况。因为高级模式会对任何连接到指定范围以下未使用端口的主机做出反应，你有机会真正破坏事情。（即某人无辜地尝试通过 SSL [TCP 端口 443] 连接到你，而你立即阻止了他们）。你们中的一些人可能甚至想要这样。只是要小心。

```bash
SCAN_TRIGGER="0"
```

## 端口标语部分

输入你想向触发 PortSentry 的人显示的文本。我不建议嘲讽此人，因为这会激怒他们。将此注释掉以禁用该功能。

隐蔽扫描检测模式不使用此功能。

```bash
PORT_BANNER="*** 未授权访问禁止 *** 你的连接尝试已被记录。走开。"
```

```text
# EOF
```

现在，出于安全原因，我们必须检查或更改其默认权限：

```bash
[root@deep /]# chmod 600 /usr/psionic/portsentry/portsentry.conf
```

## 配置 `/usr/psionic/portsentry/portsentry.ignore` 文件

`/usr/psionic/portsentry/portsentry.ignore` 文件是你添加任何希望在被连接到触发端口时被忽略的主机的地方。这应该始终至少包含 localhost（`127.0.0.1`）和本地接口（`lo`）的 IP 地址。不建议你将你网络上的每个 IP 都放进去。

编辑 `portsentry.ignore` 文件（`vi /usr/psionic/portsentry.ignore`），并添加任何你希望在被连接到触发端口时被忽略的主机：

```text
# 在此处放入你永远不会阻止的主机。这包括受保护主机上所有本地接口的 IP 地址（即虚拟主机、多宿主）保留 127.0.0.1 和 0.0.0.0 以防止人们玩游戏。

127.0.0.1
0.0.0.0
```

现在，出于安全原因，我们必须检查或更改其默认权限：

```bash
[root@deep /]# chmod 600 /usr/psionic/portsentry/portsentry.ignore
```

## 启动 PortSentry

PortSentry 程序可以配置为六种不同的操作模式，但请注意，一次只能启动一种协议模式类型。更准确地说，你可以启动一个 TCP 模式和一个 UDP 模式，因此例如两个 TCP 模式和一个 UDP 模式是不行的。可用模式包括：

- `portsentry -tcp`（基本端口绑定 TCP 模式）
- `portsentry -udp`（基本端口绑定 UDP 模式）
- `portsentry -stcp`（隐蔽 TCP 扫描检测）
- `portsentry -atcp`（高级 TCP 隐蔽扫描检测）
- `portsentry -sudp`（“隐蔽”UDP 扫描检测）
- `portsentry -audp`（高级“隐蔽”UDP 扫描检测）

就我而言，我更倾向于在 TCP 中使用“高级 TCP 隐蔽扫描检测”协议模式，在 UDP 中使用“隐蔽 UDP 扫描检测”协议模式。有关其他协议模式的更多信息，请参阅 PortSentry 源代码目录下的 `README.install` 和 `README.stealth` 文件。

**对于 TCP 模式，我选择：**

`-atcp` - 高级 TCP 隐蔽扫描检测模式

使用高级 TCP 隐蔽扫描检测模式 `-atcp` 协议模式类型，PortSentry 将首先检查你的服务器上运行的端口，然后将这些端口从监控中移除，并开始监视剩余的端口。这非常强大，对于端口扫描仪的反应速度极快。而且它使用的 CPU 时间非常少。

**对于 UDP 模式，我选择：**

`-sudp` - “隐蔽”UDP 扫描检测模式

使用隐蔽 UDP 扫描检测模式 `-sudp` 协议模式类型，UDP 端口将被列出然后进行监控。

要在上述两种选定的模式下启动 PortSentry，请使用以下命令：

```bash
[root@deep /]# /usr/psionic/portsentry/portsentry -atcp
[root@deep /]# /usr/psionic/portsentry/portsentry -sudp
```

注意：你可以将上述行添加到你的 `/etc/rc.d/rc.local` 脚本文件中，这样如果你重新启动系统，PortSentry 软件将自动启动。

## 已安装文件

- `/usr/psionic`
- `/usr/psionic/portsentry`
- `/usr/psionic/portsentry/portsentry.conf`
- `/usr/psionic/portsentry/portsentry.ignore`
- `/usr/psionic/portsentry/portsentry`

# 第 11 章 安全软件（网络服务）

## 本章内容

- Linux OpenSSH 客户端/服务器
  - 配置
  - 配置 OpenSSH 以使用 TCP-Wrappers inetd 超级服务器
  - OpenSSH 单用户配置
  - OpenSSH 用户工具
- Linux SSH2 客户端/服务器
  - 配置
  - 配置 sshd2 以使用 tcp-wrappers inetd 超级服务器
  - Ssh2 单用户配置
  - SSH2 用户工具

## Linux OpenSSH 客户端/服务器

### 概述

正如第 2 章“Linux 服务器安装”中所述，许多网络服务（包括但不限于 telnet、rsh、rlogin 或 rexec）都容易受到电子窃听攻击。因此，任何能够访问连接到网络的机器的人都可以监听它们的通信，获取你的密码，以及任何其他在网络 [Network] 中以明文传输的隐私信息。目前，Telnet 程序是日常管理任务中不可或缺的工具，但它并不安全，因为它在网络上以明文传输密码，使得任何监听者都能借此使用你的账户为所欲为。为了解决这个问题，我们必须找到另一种方式或程序来替代它。幸运的是，OpenSSH 是真正无缝且安全的替代方案，可取代 telnet、rlogin、rsh、rdist 或 rcp 等陈旧、不安全的远程登录程序。

根据官方 OpenSSH README 文件：

Ssh（安全外壳）是一种通过网络登录到另一台计算机、在远程机器上执行命令以及将文件从一台机器移动到另一台机器的程序。它在不安全的信道上提供强认证和安全通信。它旨在替代 rlogin、rsh、rcp 和 rdist。

在我们的配置中，我们将 OpenSSH 配置为支持 tcp-wrappers（inetd 超级服务器），以提高这个本已安全的程序的安全性，并避免始终在其服务器后台运行守护进程。通过这种方式，该程序仅在客户端连接到达时运行，并在允许进入服务器之前通过 TCP-WRAPPERS 守护进程对它们进行认证和授权。OpenSSH 是 SSH1 的免费替代品和改进版，移除了所有受专利限制的算法（放到外部库中），修复了所有已知的安全漏洞，重新引入了新功能，并进行了许多其他清理。建议你使用 OpenSSH（免费且修复了安全漏洞）而不是 SSH1（免费、漏洞多且陈旧）或最初免费但现已转为商业许可的 SSH2。对于使用 Datafellows 公司 SSH2 的用户，我们将在本书中同时提供这两个版本，首先介绍 OpenSSH，因为它是新的 SSH 程序，未来每个人都应迁移到它。

### 这些安装说明假定

- 命令与 Unix 兼容。
- 源码路径为 `/var/tmp`（其他路径亦可）。
- 安装已在 Red Hat Linux 6.1 和 6.2 上测试通过。
- 安装的所有步骤均在超级用户账户 `root` 下执行。
- OpenSSH 版本号为 1.2.3。

### 软件包

OpenSSH 主页：[http://violet.ibs.com.au/openssh/](http://violet.ibs.com.au/openssh/)

你必须确保下载：`openssh-1.2.3.tar.gz`

### 前提条件

OpenSSH 要求系统中已安装 `zlib-devel` 包，该包包含开发使用 zlib 压缩与解压缩库的程序所需的头文件和库。如果尚未安装，你必须从 Red Hat Linux 6.1 或 6.2 CD-ROM 安装。

要验证你的 Linux 系统上是否已安装 `zlib-devel` 包，请使用以下命令：

```bash
[root@deep /]# rpm -qi zlib-devel
package zlib-devel is not installed
```

要在你的 Linux 系统上安装 `zlib-devel` 包，请使用以下命令：

```bash
[root@deep /]# mount /dev/cdrom /mnt/cdrom/
[root@deep /]# cd /mnt/cdrom/RedHat/RPMS/
[root@deep RPMS]# rpm -Uvh zlib-devel-version.i386.rpm
gd #############################################
[root@deep RPMS]# rpm -Uvh gd-devel-version.i386.rpm
zlib-devel    #############################################
[root@deep RPMS]# cd /; umount /mnt/cdrom/
```

必须已在系统上安装 OpenSSL，以启用 SSL 功能，从而能够使用 OpenSSH 软件。

**注意**：有关 OpenSSL 服务器的更多信息，请参阅本书相关章节。即使你不需要使用 OpenSSL 软件来创建或保存加密密钥文件，也必须注意，OpenSSH 程序需要其库文件才能在系统上正常工作。

### Tarball

在安装 OpenSSH 之前先列出系统上的文件清单，安装后再列一次，然后使用 `diff` 比较，找出它把文件放到了哪些位置，这是一个好办法。只需在安装前运行 `find /* > OpenSSH1`，安装后运行 `find /* > OpenSSH2`，再使用 `diff OpenSSH1 OpenSSH2 > OpenSSH-Installed`，即可得到变更列表。

### 编译

解压 tarball（tar.gz）。

```bash
[root@deep /]# cp openssh-version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf openssh-version.tar.gz
```

### 编译与优化

#### 步骤 1

进入新的 OpenSSH 目录，然后在终端中输入以下命令：

```bash
CC="egcs" \
CFLAGS="-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
./configure \
--prefix=/usr \
--sysconfdir=/etc/ssh \
--with-tcp-wrappers \
--with-ipv4-default \
--with-ssl-dir=/usr/include/openssl
```

这会告诉 OpenSSH 针对当前特定的硬件配置进行设置：

- 编译进 libwrap 并启用 TCP Wrappers（`/etc/hosts.allow|deny`）支持。
- 在 Linux/glibc-2.1.2 下禁用名称解析的长延迟，以缩短连接时间。
- 指定 OpenSSH 程序运行所需的 OpenSSL 库位置。

#### 步骤 2

现在，我们必须在服务器上编译并安装 OpenSSH：

```bash
[root@deep openssh-1.2.3]# make
[root@deep openssh-1.2.3]# make install
[root@deep openssh-1.2.3]# make host-key
[root@deep openssh-1.2.3]# install -m644 contrib/redhat/sshd.pam /etc/pam.d/sshd
```

`make` 命令将所有源文件编译为可执行二进制文件，`make install` 将二进制文件及所有支持文件安装到适当位置。`make host-key` 命令生成主机密钥，最后 `install` 命令安装适用于 Red Hat Linux 的 PAM 支持，该支持现在比流行的商业 ssh-1.2.x 软件包更为完善。

### 清理工作

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf openssh-version/ openssh-version.tar.gz
```

上面使用的 `rm` 命令将删除我们用于编译和安装 OpenSSH 的所有源文件。它还会从 `/var/tmp` 目录中删除 OpenSSH 压缩包。

### 配置

本书中介绍的每种软件都有特定的目录和子目录，位于名为 `floppy.tgz` 的 tar 压缩包中，其中包含每个特定程序的配置文件。如果你获得该压缩包，就不必手动复制或逐行粘贴来创建下面的配置文件。无论你是决定手动复制，还是从压缩文件中获取已为你准备好的文件，你都有责任修改、调整并满足你的需求，并将与 OpenSSH 软件相关的文件放置到服务器上的适当位置，如下所示。服务器配置文件压缩包可从以下互联网地址下载：

[http://www.openna.com/books/floppy.tgz](http://www.openna.com/books/floppy.tgz)

要运行 OpenSSH 客户端/服务器，需要以下文件，并且必须创建或复制到服务器上的相应目录：

- 将 `ssh_config` 文件复制到 `/etc/ssh/` 目录。
- 将 `sshd_config` 文件复制到 `/etc/ssh/` 目录。
- 将 `sshd` 文件复制到 `/etc/pam.d/` 目录。

你可以在我们的 `floppy.tgz` 压缩包中获取以下列出的配置文件。从解压后的 `floppy.tgz` 压缩包中将以下文件复制到适当的位置，或直接从本书复制到相应文件。

Morton© 1999 - 2000 Gerhard Mourani, Open Network Architecture ® and OpenDocs Publishing

编辑 `ssh_config` 文件（`vi /etc/ssh/ssh_config`），并根据需要添加或修改以下参数：

```text
# Site-wide defaults for various options

Host *

  ForwardAgent no

  ForwardX11 no

  RhostsAuthentication no

  RhostsRSAAuthentication no

  RSAAuthentication yes

  PasswordAuthentication yes

  FallBackToRsh no

  UseRsh no

  BatchMode no

  CheckHostIP yes

  StrictHostKeyChecking no

  IdentityFile ~/.ssh/identity

  Port 22

  Cipher blowfish

  EscapeChar ~
```



## 配置 `ssh_config` 文件

以下配置将指导 `ssh_config` 文件进行当前特定配置：

### `Host *`

`Host` 选项将配置文件中所有后续的声明和选项限制为仅匹配该关键字后给定模式的那些主机。模式 `*` 表示适用于所有主机，直到下一个 `Host` 关键字为止。通过此选项，你可以在同一个 `ssh_config` 文件中为不同的主机设置不同的声明。

### `ForwardAgent no`

`ForwardAgent` 选项指定应将哪个连接认证代理（如果有）转发到远程计算机。

### `ForwardX11 no`

`ForwardX11` 选项适用于使用 Xwindow GUI 的用户，用于自动将 X11 会话重定向到远程计算机。由于我们设置的是服务器且上面未安装 GUI，因此可以安全地关闭此选项。

### `RhostsAuthentication no`

`RhostsAuthentication` 选项指定是否尝试使用基于 rhosts 的认证。由于 rhosts 认证不安全，不应使用此选项。

### `RhostsRSAAuthentication no`

`RhostsRSAAuthentication` 选项指定是否尝试结合 RSA 主机认证进行 rhosts 认证。

### `RSAAuthentication yes`

`RSAAuthentication` 选项指定是否尝试 RSA 认证。为了获得更好的会话安全性，此选项必须设置为 `yes`。RSA 使用 `ssh-keygen1` 工具生成的公钥和私钥对进行认证。

### `PasswordAuthentication yes`

`PasswordAuthentication` 选项指定是否使用基于密码的认证。为了强安全性，此选项必须始终设置为 `yes`。

### `FallBackToRsh no`

`FallBackToRsh` 选项指定如果与 ssh 守护进程连接失败，是否自动改用 rsh。鉴于 rsh 服务不安全，此选项必须始终设置为 `no`。

### `UseRsh no`

`UseRsh` 选项指定是否在此主机上使用 rlogin/rsh 服务。与 `FallBackToRsh` 选项一样，出于显而易见的原因，必须将其设置为 `no`。

### `BatchMode no`

`BatchMode` 选项指定是否禁用连接时的用户名和密码查询。此选项在创建脚本且不想输入密码时非常有用（例如，使用 `scp` 命令进行网络备份的脚本）。

### `CheckHostIP yes`

`CheckHostIP` 选项指定 ssh 是否额外检查连接到服务器的主机 IP 地址以检测 DNS 欺骗。建议将此选项设置为 `yes`。

### `StrictHostKeyChecking no`

`StrictHostKeyChecking` 选项指定 ssh 是否自动将新的大富彩票登陆主机密钥添加到 `$HOME/.ssh/known_hosts` 文件中，或从不自动将新主机密钥添加到主机文件。当设置为 `yes` 时，此选项提供最大程度的特洛伊木马攻击防护。关于此选项的一个有趣做法是，开始时将其设置为 `no`，允许 ssh 在连接时自动将所有常用主机添加到主机文件，然后再将其设置为 `yes` 以利用此功能。

### `IdentityFile ~/.ssh/identity`

`IdentityFile` 选项指定要读取的备用 RSA 认证身份文件。此外，可以在配置文件中指定多个身份文件（`ssh_config`）。

### `Port 22`

`Port` 选项指定 ssh 连接到远程主机所使用的端口号。默认端口为 22。

### `Cipher blowfish`

`Cipher` 选项指定用于加密会话的密码算法。blowfish 使用 64 位块和最长 448 位的密钥。

### `EscapeChar ~`

`EscapeChar` 选项指定用于暂停的会话转义字符。

## 配置 `/etc/ssh/sshd_config` 文件

`/etc/ssh/sshd_config` 文件是 OpenSSH 的系统级配置文件，允许你设置修改守护进程操作的选项。此文件包含关键字-值对，每行一个，关键字不区分大小写。以下是配置你的 `sshd` 以实现顶级安全的最重要关键字；完整的列表和/或特殊要求可在 `sshd(8)` 的手册页中找到。

编辑 `sshd_config` 文件（`vi /etc/ssh/sshd_config`），并根据需要添加或修改以下参数：

```text
# This is ssh server systemwide configuration file.

Port 22
ListenAddress 192.168.1.1
HostKey /etc/ssh/ssh_host_key
ServerKeyBits 1024
LoginGraceTime 600
KeyRegenerationInterval 3600
PermitRootLogin no
IgnoreRhosts yes
IgnoreUserKnownHosts yes
StrictModes yes
X11Forwarding no
PrintMotd yes
SyslogFacility AUTH
LogLevel INFO
RhostsAuthentication no
RhostsRSAAuthentication no
RSAAuthentication yes
PasswordAuthentication yes
PermitEmptyPasswords no
AllowUsers admin
```

以下配置将指导 `sshd_config` 文件进行当前特定配置：

### `Port 22`

`Port` 选项指定 ssh 守护进程监听传入连接的端口号。默认端口为 22。

### `ListenAddress 192.168.1.1`

`ListenAddress` 选项指定 ssh 守护进程服务器套接字绑定的网络接口 IP 地址。默认值为 `0.0.0.0`；为了提高安全性，你可以仅指定所需的地址以限制可能的地址。

### `HostKey /etc/ssh/ssh_host_key`

`HostKey` 选项指定包含私主机密钥的位置。

### `ServerKeyBits 1024`

`ServerKeyBits` 选项指定服务器密钥使用的位数。这些位数在守护进程启动生成其 RSA 密钥时使用。

### `LoginGraceTime 600`

`LoginGraceTime` 选项指定在用户未成功登录的情况下，服务器在断开连接前等待的秒数。

### `KeyRegenerationInterval 3600`

`KeyRegenerationInterval` 选项指定服务器在自动重新生成其密钥前应等待的秒数。这是一项安全功能，用于防止解密已截获的会话。

### `PermitRootLogin no`

`PermitRootLogin` 选项指定 root 是否可以使用 ssh 登录。永远不要将此选项设置为 `yes`。

### `IgnoreRhosts yes`

`IgnoreRhosts` 选项指定是否在认证中不使用 rhosts 或 shosts 文件。出于安全原因，建议不要使用 rhosts 或 shosts 文件进行认证。

### `IgnoreUserKnownHosts yes`

`IgnoreUserKnownHosts` 选项指定 ssh 守护进程在 `RhostsRSAAuthentication` 期间是否应忽略用户的 `$HOME/.ssh/known_hosts`。

### `StrictModes yes`

`StrictModes` 选项指定 ssh 在接受登录前是否应检查用户主目录和 rhosts 文件的权限。此选项必须始终设置为 `yes`，因为有时用户可能会意外将其目录或文件设为全局可写。

### `X11Forwarding no`

`X11Forwarding` 选项指定是否应在此服务器上启用 X11 转发。由于我们设置的是未安装 GUI 的服务器，因此可以安全地关闭此选项。

### `PrintMotd yes`

`PrintMotd` 选项指定 ssh 守护进程在用户交互式登录时是否打印 `/etc/motd` 文件的内容。`/etc/motd` 文件也被称为“每日消息”（message of the day）。

### `SyslogFacility AUTH`

`SyslogFacility` 选项指定记录来自 sshd 的消息时使用的设施代码。该设施指定了产生消息的子系统——在我们的例子中是 AUTH。

### `LogLevel INFO`

`LogLevel` 选项指定记录来自 sshd 的消息时使用的级别。INFO 是一个不错的选择。有关其他可能性的更多信息，请参阅 `sshd` 的手册页。

### `RhostsAuthentication no`

`RhostsAuthentication` 选项指定 sshd 是否可以尝试使用基于 rhosts 的认证。由于 rhosts 认证不安全，不应使用此选项。

### `RhostsRSAAuthentication no`

`RhostsRSAAuthentication` 选项指定是否尝试结合 RSA 主机认证进行 rhosts 认证。

### `RSAAuthentication yes`

`RSAAuthentication` 选项指定是否尝试 RSA 认证。为了在会话中获得更好的安全性，此选项必须设置为 `yes`。RSA 使用 `ssh-keygen1` 工具生成的公钥和私钥对进行认证。

### `PasswordAuthentication yes`

`PasswordAuthentication` 选项指定是否使用基于密码的认证。为了强安全性，此选项必须始终设置为 `yes`。

### `PermitEmptyPasswords no`

`PermitEmptyPasswords` 选项指定服务器是否允许使用空密码登录账户。如果你打算使用 `scp` 工具通过网络进行自动备份，必须将此选项设置为 `yes`。

### `AllowUsers admin`

`AllowUsers` 选项指定并控制哪些用户可以访问 ssh 服务。可以指定多个用户，以空格分隔。

## 配置 OpenSSH 使用 TCP-Wrappers inetd 超级服务器

应启用 Tcp-Wrappers 来启动和停止我们的 OpenSSH 服务器。执行时，inetd 从其配置文件中读取配置信息，该配置文件默认为 `/etc/inetd.conf`。

配置文件的每个字段都必须有一条对应的条目，每个字段的条目之间用制表符或空格分隔。

## 第 1 步

编辑 `inetd.conf` 文件（`vi /etc/inetd.conf`）并添加以下行：

```text
ssh  stream    tcp   nowait    root /usr/sbin/tcpd  sshd -i
```

**注意：** `-i` 参数很重要，因为它指定了 sshd 是从 inetd 运行的。此外，在将上述行添加到文件后，通过发送 `SIGHUP` 信号（`killall -HUP inetd`）来更新你的 `inetd.conf` 文件。

- 要更新你的 `inetd.conf` 文件，请使用以下命令：

  ```shell
  [root@deep /]# killall -HUP inetd
  ```

## 第 2 步

编辑 `hosts.allow` 文件（`vi /etc/hosts.allow`）并添加以下行：

```text
sshd: 192.168.1.4 win.openna.com
```

这意味着客户端 IP `192.168.1.4` 且主机名为 `win.openna.com` 的用户被热烈欢迎不受限制地 ssh 登录到该服务器。

这些供 sshd 使用的 tcp-wrappers“守护程序”字符串包括：

- `sshdfwd-X11`（如果你想允许/拒绝 X11 转发）。
- `sshdfwd-<端口号>`（用于 TCP 转发）。
- `sshdfwd-<端口名>`（在 `/etc/services` 中定义的端口名，用于 TCP 转发）。

**注意：** 如果你决定改用 ssh，请确保在**所有**服务器上都安装并使用它。有十台安全服务器和一台不安全服务器是浪费时间。

## 更多文档

更多详情请阅读以下手册页：

```text
$ man ssh (1)                   - OpenSSH 安全 shell 客户端（远程登录程序）
$ man ssh [slogin] (1)          - OpenSSH 安全 shell 客户端（远程登录程序）
$ man ssh-add (1)               - 为认证代理添加身份
$ man ssh-agent (1)             - 认证代理
$ man ssh-keygen (1)            - 认证密钥生成
$ man sshd (8)                  - 安全 shell 守护进程
```



## OpenSSH 每用户配置

### 第 1 步

通过执行以下命令在本地创建你的私钥和公钥：

```shell
[root@deep /]# su admin
[admin@deep /]$ ssh-keygen
```

结果应如下所示：

```text
正在初始化随机数生成器...
正在生成 p: .............................++ (距离 430)
正在生成 q: ......................++ (距离 456)
正在计算密钥...
正在测试密钥...
密钥生成完成。
输入要保存密钥的文件（/home/admin/.ssh/identity）：[按 Enter 键]
输入密码短语：
再次输入相同的密码短语：
你的身份标识已保存在 /home/admin/.ssh/identity。
你的公钥是：
1024 37
14937757511251955533691120318477293862290049394715136511145806108870001764378494676831
29757784315853227236120610062314604405364871843677484233240919418480988907860997175244
46977589647127757030728779973708569993017043141563536333068888944038178461608592483844
590202154102756903055846534063365635584899765402181 admin@deep.openna.com
你的公钥已保存在 /home/admin/.ssh/identity.pub
```

**注意：** 如果你有多个账户，你可能希望为每个账户创建单独的密钥。你可能想为以下服务器分别创建密钥：

- 你的邮件服务器
- 你的 Web 服务器
- 你的网关服务器

这样可以限制这些服务器之间的访问，例如，不允许邮件账户访问你的 Web 账户或网关中的机器。这可以在任何认证密钥因任何原因被泄露时增强整体安全性。

### 第 2 步

将你的本地公钥 `identity.pub` 远程复制到 `/home/admin/.ssh` 目录下，命名为 `authorized_keys`。

**注意：** 复制文件的一种方法是使用 `ftp` 命令，或者你可能需要通过电子邮件将你的公钥发送给系统管理员。只需在邮件中包含 `~/.ssh/identity.pub` 文件的内容。

## 更改你的密码短语

你可以随时使用 `ssh-keygen` 的 `-p` 选项来更改密码短语。

- 要更改密码短语，请使用以下命令：

```shell
[root@deep /]# su admin
[admin@deep /]$ ssh-keygen -p
```

```text
输入密钥所在的文件（/home/admin/.ssh/identity）：[按 Enter 键]
输入旧密码短语：
密钥带有注释 'admin@deep.openna.com'
输入新密码短语：
再次输入相同的密码短语：
你的身份标识已使用新密码短语保存。
```

## OpenSSH 用户工具

下面列出的命令是我们在日常使用中经常用到的一些命令，但还有更多命令存在，详情请查阅手册页和文档。

### `ssh`

`ssh`（安全 shell）命令为两台不受信任的主机在不安全的网络之间提供安全加密的通信。这是一个用于安全登录到远程机器并在那里执行命令的程序。它可以替代 `telnet`、`rlogin`、`rcp`、`rdist` 和 `rsh` 等不安全的程序。

- 要登录到远程机器，请使用以下命令：

```shell
[root@deep /]# ssh -l <登录名> <主机名>
```

例如：

```text
[root@deep /]# ssh -l admin www.openna.com
admin@deep.openna.com 的密码：
上次登录时间：1999 年 10 月 19 日 星期二 18:13:00 -0400，来自 deep.openna.com
没有邮件。
[admin@www admin]$
```

其中 `<登录名>` 是你用于连接 `ssh` 服务器的用户名，`<主机名>` 是你的 `ssh` 服务器的远程地址。

### `scp`

`scp`（安全复制）工具使用 `scp` 命令将文件从本地系统复制到远程系统，或从远程系统复制到本地系统，甚至在两个远程系统之间复制。

- 要从远程系统复制文件到本地系统，请使用以下命令：

```shell
[root@deep /]# su admin
[admin@deep /]$ scp -p <登录名@主机名>:/文件目录/文件名 本地目录/文件位置
```

例如：

```text
[admin@deep /]$ scp -p admin@mail:/etc/test1 /tmp
输入 RSA 密钥 'admin@mail.openna.com' 的密码短语：
test1          |    2 kB | 2.0 kB/s | 预计完成时间：00:00:00 | 100%
```

- 要从本地系统复制文件到远程系统，请使用以下命令：

```shell
[root@deep /]# su admin
[admin@deep /]$ scp -p 本地目录/文件位置 <用户名@主机名>:/文件目录/文件名
```

例如：

```text
[admin@deep /]$ scp -p /usr/bin/test2 admin@mail:/var/tmp
admin@mail 的密码：
test2          |    7 kB | 7.9 kB/s | 预计完成时间：00:00:00 | 100%
```

**注意：** `-p` 选项表示应在副本上保留源文件的修改和访问时间以及模式。这通常是可取的。

## OpenSSH 软件的一些可能用途

OpenSSH 可用于：

1. 替代 `telnet`、`rlogin`、`rsh`、`rdist` 和 `rcp`。
2. 通过网络进行安全备份。
3. 执行远程命令。
4. 通过 Internet 访问企业资源。

## 已安装的文件

| 文件 | 文件 |
|---|---|
| `/etc/ssh` | `/usr/bin/slogin` |
| `/etc/ssh/ssh_config` | `/usr/man/man1/ssh.1` |
| `/etc/ssh/sshd_config` | `/usr/man/man1/scp.1` |
| `/etc/ssh_host_key` | `/usr/man/man1/ssh-add.1` |
| `/etc/ssh_host_key.pub` | `/usr/man/man1/ssh-agent.1` |
| `/usr/bin/ssh` | `/usr/man/man1/ssh-keygen.1` |
| `/usr/bin/scp` | `/usr/man/man1/slogin.1` |
| `/usr/bin/ssh-add` | `/usr/man/man8/sshd.8` |
| `/usr/bin/ssh-agent` | `/usr/sbin/sshd` |
| `/usr/bin/ssh-keygen` |  |

## Windows 免费 SSH 客户端

### Putty

Putty 主页：[http://www.chiark.greenend.org.uk/~sgtatham/putty.html](http://www.chiark.greenend.org.uk/~sgtatham/putty.html)

### Tera Term Pro 和 TTSSH

Tera Term Pro 主页：[http://hp.vector.co.jp/authors/VA002416/teraterm.html](http://hp.vector.co.jp/authors/VA002416/teraterm.html)

TTSSH 主页：[http://www.zip.com.au/~roca/download.html](http://www.zip.com.au/~roca/download.html)

## Linux SSH2 客户端/服务器

### 概述

现在很清楚，所有 Linux 用户都必须使用 OpenSSH，而不是 Datafellows 公司的 SSH2。然而，对于想要使用此软件非免费版本的用户或组织，我们在此提供需要遵循的步骤。这是 SSH 软件的 SSH2 商业版本。在我们的配置中，我们还配置了 `sshd2` 以支持 `tcp-wrappers`（`inetd` 超级服务器）以确保安全。

### 这些安装说明假定

- 命令与 Unix 兼容。
- 源路径为 `/var/tmp`（其他路径也可行）。
- 安装已在 Red Hat Linux 6.1 和 6.2 上测试。
- 安装中的所有步骤都将使用超级用户账户 `root` 执行。
- SSH2 版本号为 2.0.13。

### 软件包

SSH2 主页：http://www.ssh.org/

你必须确保下载：`ssh-2.0.13.tar.gz`

### Tarballs

在安装 `ssh2` 之前列出系统上的文件清单是个好主意，安装之后再列一个，然后使用 `diff` 比较，找出它将文件放置到了哪里。只需在安装前运行 `find /* > SSH1`，安装后运行 `find /* > SSH2`，然后使用 `diff SSH1 SSH2 > SSH-Installed` 来获取变化的清单。

## 编译

解压 tarball（`tar.gz`）。

```shell
[root@deep /]# cp ssh-version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf ssh-version.tar.gz
```

## 编译和优化

进入新的 SSH2 目录，在终端中输入以下命令：

```shell
CC="egcs" \
CFLAGS="-O9 -funroll-loabs -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
./configure \
--prefix=/usr \
--without-ssh-agent1-compat \
--disable-suid-ssh-signer \
--disable-tcp-port-forwarding \
--disable-X11-forwarding \
--enable-tcp-nBLendlash \
--with-libwrap
```

这告诉 SSH2 针对这个特定的硬件设置进行配置，具体如下：

- `oplastic` 保留 `ssh-agent1` 兼容性。
- 安装 `ssh-signer`，不设置 `suid` 位。
- 禁用端口转发支持。
- 禁用 X11 转发支持。
- 启用 `TCP_NODELAY` 套接字选项。
- 编译集成 `libwrap`（`tcp_wrappers`）支持。

```shell
[root@deep ssh-2.0.13]# make clean
[root@deep ssh-2.0.13]# make
[root@deep ssh-2.0.13]# make install
[root@deep ssh-2.0.13]# rm -f /usr/bin/ssh-askpass
```

`make clean` 命令会清除之前所有编译痕迹，以避免出现任何错误；`make` 命令将所有源文件编译为可执行二进制文件；最后，`make install` 命令将二进制文件及所有支持文件安装到相应位置。

## 工作完成后清理

```shell
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf ssh-version/ ssh-version.tar.gz
```

上述 `rm` 命令将删除我们用于编译和安装 SSH2 的所有源文件，同时也会从 `/var/tmp` 目录中删除 SSH2 的压缩归档文件。

## 配置

本书中描述的所有软件在名为 `floppy.tgz` 的 tar 压缩归档中都有特定的目录和子目录，其中包含各程序的配置文件。如果你获取了此归档文件，就不必手动创建下文中的各种配置文件，也不必通过复制粘贴来创建配置文件。无论你是选择手动复制，还是从压缩归档中获取为你准备好的文件，你都有责任根据需求进行修改、调整，并将与 SSH2 软件相关的文件放到服务器上的相应位置，如下所示。服务器配置文件归档的下载地址位于以下网址：http://www.openna.com/books/floppy.tgz

- 要运行 SSH2 客户端/服务器，需要以下文件，并且必须创建或复制到服务器上的相应目录中。
  - 将 `sshd2_config` 文件复制到 `/etc/ssh2/` 目录。
  - 将 `ssh2_config` 文件复制到 `/etc/ssh2/` 目录。
  - 将 `ssh` 文件复制到 `/etc/pam.d/` 目录。

你可以在我们的 `floppy.tgz` 归档中获取下列配置文件。将解压后的 `floppy.tgz` 归档中的以下文件复制到相应位置，或者直接从本书中复制到相关文件中。

## 配置 `/etc/ssh2/ssh2_config` 文件

`ssh2` 的配置文件 `/etc/ssh2/ssh2_config` 允许你设置修改客户端程序运行方式的选项。该文件包含关键字-值对，每行一对，关键字不区分大小写。以下是较重要的关键字；完整列表请参见 `ssh2 (1)` 的手册页。

编辑 `ssh2_config` 文件（`vi /etc/ssh2/ssh2_config`）并根据需要添加或修改：

```text
# ssh2_config

# SSH 2.0 客户端配置文件

*:

    Port                          22

    Ciphers                       blowfish

    Compression                   yes

    IdentityFile                  identification

    AuthorizationFile             authorization

    RandomSeedFile                random_seed

    VerboseMode                   no

    ForwardAgent                  no

    ForwardX11                    no

    PasswordPrompt                "%U's password: "

    Ssh1Compatibility             no

    Ssh1AgentCompatibility        none

    NoDelay                       yes

    KeepAlive                     yes

    QuietMode                     no
```



# SSH2 配置

```text
```

这表示 `ssh2_config` 文件将按以下方式配置自身以适应此特定配置：

### `Port 22`

选项 `Port` 指定 SSH 连接到远程主机时使用的端口号。默认端口为 `22`。

### `Ciphers blowfish`

选项 `Ciphers` 指定用于加密会话的密码算法。`blowfish` 使用 64 位分组和最长 448 位的密钥。

### `Compression yes`

选项 `Compression` 指定是否在会话期间使用压缩。压缩将提高通信速度和文件传输效率。

### `IdentityFile identification`

选项 `IdentityFile` 指定用户身份验证文件的备用名称。

### `AuthorizationFile authorization`

选项 `AuthorizationFile` 指定用户授权文件的备用名称。

### `RandomSeedFile random_seed`

选项 `RandomSeedFile` 指定用户随机种子文件的备用名称。

### `VerboseMode no`

选项 `VerboseMode` 指示 SSH2 打印有关其进度的调试消息。此选项有助于调试连接、认证和配置问题。

### `ForwardAgent no`

选项 `ForwardAgent` 指定应将哪个连接认证代理（如果有）转发到远程计算机。

### `ForwardX11 no`

选项 `ForwardX11` 适用于使用 Xwindow GUI 并希望自动将 X11 会话重定向到远程计算机的用户。由于我们设置的是服务器，且上面未安装 GUI，因此可以安全地关闭此选项。

### `PasswordPrompt "%U's password: "`

选项 `PasswordPrompt` 指定用户连接到主机时显示的密码提示。变量 `%U` 和 `%H` 分别表示用户的登录名和主机名。

### `Ssh1Compatibility no`

选项 `Ssh1Compatibility` 指定是否对 SSH1 用户使用 SSH1 兼容代码与 SSH2 配合。

### `Ssh1AgentCompatibility none`

选项 `Ssh1AgentCompatibility` 指定是否还将 SSH1 用户的 SSH1 代理连接转发到 SSH2。

### `NoDelay yes`

选项 `NoDelay` 指定是否启用套接字选项 `TCP_NODELAY`。建议将此选项设置为 `yes` 以提高网络性能。

### `KeepAlive yes`

选项 `KeepAlive` 指定系统是否应向远程服务器发送保活消息。如果设置为 `yes`，则会正确检测到连接中断或远程计算机崩溃。

### `QuietMode no`

选项 `QuietMode` 指定系统是否以安静模式运行。此选项必须设置为 `no`，因为在安静模式下，除了致命错误外，系统日志中不会记录任何内容。由于我们希望获取用户会话信息，因此最好禁用此选项。

## 配置 `/etc/ssh2/sshd2_config` 文件

`sshd2` 的配置文件 `/etc/ssh2/sshd2_config` 允许你设置修改守护进程运行方式的选项。该文件包含关键字-值对，每行一对，关键字不区分大小写。以下是较重要的关键字；完整列表请参见 `sshd2 (8)` 的手册页。

编辑 `sshd2_config` 文件（`vi /etc/ssh2/sshd2_config`）并根据需要添加或修改：

```text
# sshd2_config

# SSH 2.0 服务器配置文件

*:

    Port                           22

    ListenAddress                  192.168.1.1

    Ciphers                        blowfish

    IdentityFile                   identification

    AuthorizationFile              authorization

    HostKeyFile                    hostkey

    PublicHostKeyFile              hostkey.pub

    RandomSeedFile                 random_seed

    ForwardAgent                   no

    ForwardX11                     no

    PasswordGuesses                3

    MaxConnections                 5

    PermitRootLogin                no

    AllowedAuthentications         publickey,password

    RequiredAuthentications        publickey,password

    VerboseMode                    no

    PrintMotd                      yes

    CheckMail                      yes
```

```text
    UserConfigDirectory            "%D/.ssh2"

    SyslogFacility                 DAEMON

    Ssh1Compatibility              no

    NoDelay                        yes

    KeepAlive                      yes

    UserKnownHosts                 yes

    AllowHosts                     192.168.1.4

    DenyHosts                      *

    QuietMode                      no
```

```text
# 子系统定义

subsystem-sftp                   sftp-server
```

这表示 `sshd2_config` 文件将按以下方式配置自身以适应此特定配置：

### `Port 22`

选项 `Port` 指定 SSH2 守护进程侦听 SSH 传入连接的端口号。默认端口为 `22`。

### `ListenAddress 192.168.1.1`

选项 `ListenAddress` 指定 SSH2 守护进程服务器套接字绑定的网络接口 IP 地址。默认值为 `0.0.0.0`；为了提高安全性，你可以仅指定所需的地址以限制可能的地址。

### `Ciphers blowfish`

选项 `Ciphers` 指定用于加密会话的密码算法。`blowfish` 使用 64 位分组和最长 448 位的密钥。

### `IdentityFile identification`

选项 `IdentityFile` 指定用户身份验证文件的备用名称。

### `AuthorizationFile authorization`

选项 `AuthorizationFile` 指定用户授权文件的备用名称。

### `HostKeyFile hostkey`

选项 `HostKeyFile` 指定包含私钥的备用主机密钥文件。默认值为 `/etc/ssh2/hostkey`。

### `PublicHostKeyFile hostkey.pub`

选项 `PublicHostKeyFile` 指定包含公钥的备用主机密钥文件。默认值为 `/etc/ssh2/hostkey.pub`。

### `RandomSeedFile random_seed`

选项 `RandomSeedFile` 指定用户随机种子文件的备用名称。

### `ForwardAgent no`

选项 `ForwardAgent` 指定应将哪个连接认证代理（如果有）转发到远程计算机。

### `ForwardX11 no`

选项 `ForwardX11` 适用于使用 Xwindow GUI 并希望自动将 X11 会话重定向到远程计算机的用户。由于我们设置的是服务器，且上面没有安装 GUI，因此可以安全地关闭此选项。

### `PasswordGuesses 3`

选项 `PasswordGuesses` 指定用户在使用密码认证时可以尝试的次数。

### `MaxConnections 5`

选项 `MaxConnections` 指定 SSH2 守护进程同时处理的最大连接数。

### `PermitRootLogin no`

选项 `PermitRootLogin` 指定 root 用户是否可以通过 SSH 登录。此选项永远不要设置为 `yes`。

### `AllowedAuthentications publickey,password`

选项 `AllowedAuthentications` 指定允许使用哪些认证方法。通过此选项，管理员可以强制用户在通过认证之前完成多种认证。

### `RequiredAuthentications publickey,password`

选项 `RequiredAuthentications` 与 `AllowedAuthentications` 相关，指定用户在继续操作之前必须完成哪些认证方法。此参数必须与 `AllowedAuthentications` 选项相同，否则服务器将每次都拒绝连接。

### `VerboseMode no`

选项 `VerboseMode` 指示 SSH2 守护进程打印关于其运行过程的调试信息。此选项有助于调试连接、认证和配置问题。

### `PrintMotd yes`

选项 `PrintMotd` 指定当用户以交互方式登录时，SSH2 守护进程是否应打印 `/etc/motd` 文件的内容。`/etc/motd` 文件也被称为“每日消息”。

### `CheckMail yes`

选项 `CheckMail` 指定 SSH2 守护进程是否应打印您可能收到的新邮件信息。

### `UserConfigDirectory "%D/.ssh2"`

选项 `UserConfigDirectory` 指定用户特定配置数据的默认位置。

### `SyslogFacility DAEMON`

选项 `SyslogFacility` 指定记录 SSH2 守护进程的消息时使用的设施代码。该设施指定产生消息的子系统，在我们的例子中是 `DAEMON`。

### `Ssh1Compatibility no`

选项 `Ssh1Compatibility` 指定是否对 SSH1 用户在 SSH2 中使用 SSH1 兼容代码。

### `NoDelay yes`

选项 `NoDelay` 指定是否启用套接字选项 `TCP_NODELAY`。建议将此选项设置为 `yes` 以提高网络性能。

### `KeepAlive yes`

选项 `KeepAlive` 指定系统是否应向远程服务器发送保活消息。如果设置为 `yes`，则连接中断或远程机器崩溃将被正确检测到。

### `UserKnownHosts yes`

选项 `UserKnownHosts` 指定在使用 `hostbased` 认证时，是否可以使用默认用户主目录 `$HOME/.ssh2/knownhosts/` 来获取主机公钥。

### `AllowHosts 192.168.1.4`

选项 `AllowHosts` 指定和控制哪些主机可以访问 SSH2 服务。可以指定多个主机，用空格分隔。

### `DenyHosts *`

选项 `DenyHosts` 指定和控制哪些主机不能访问 SSH2 服务。可以指定多个主机，用空格分隔。默认模式 `*` 表示所有主机。

### `QuietMode no`

选项 `QuietMode` 指定系统是否以安静模式运行。此选项必须设置为 `no`，因为在安静模式下，除了致命错误外，系统日志中不会记录任何内容。由于我们希望获取有关用户会话的信息，因此最好禁用此选项。

## 配置 `sshd2` 以使用 tcp-wrappers inetd 超级服务器

应启用 Tcp-wrappers 来启动和停止 `sshd2` 服务器。执行时，`inetd` 从其配置文件中读取配置信息，默认情况下该文件为 `/etc/inetd.conf`。配置文件的每个字段都必须有一个条目，各字段的条目之间用制表符或空格分隔。

### 步骤 1

编辑 `inetd.conf` 文件（`vi /etc/inetd.conf`）并添加以下行：

```text
ssh  stream    tcp   nowait    root /usr/sbin/tcpd  sshd -i
```

**注意：** `-i` 参数很重要，因为它指定 `sshd` 是从 `inetd` 运行的。另外，在将上述行添加到文件后，通过发送 `SIGHUP` 信号（`killall -HUP inetd`）来更新您的 `inetd.conf` 文件。

- 要更新您的 `inetd.conf` 文件，请使用以下命令：

```text
[root@deep /]# killall -HUP inetd
```

### 步骤 2

编辑 `hosts.allow` 文件（`vi /etc/hosts.allow`）并添加以下行：

```text
sshd: 192.168.1.4 win.openna.com
```

这意味着客户端 `192.168.1.4`（主机名为 `win.openna.com`）被允许通过 SSH 访问该服务器。

`sshd2` 使用的这些 tcp-wrappers“守护进程”字符串包括：

- `sshd`、`sshd2`（`sshd2` 被调用时的名称，通常为 `sshd`）。
- `sshdfwd-X11`（如果您想允许或拒绝 X11 转发）。
- `sshdfwd-<port-number>`（用于 TCP 转发）。
- `sshdfwd-<port-name>`（在 `/etc/services` 中定义的端口名称，用于 TCP 转发）。

**注意：** 如果您确实决定改用 SSH，请确保在**所有**服务器上安装并使用它。拥有十台安全服务器和一台不安全服务器是浪费时间。

## 配置 `/etc/pam.d/ssh` 文件

为了提高 SSH2 服务器的安全性，您可以将其配置为使用 PAM 认证。为此，您必须创建 `/etc/pam.d/ssh` 文件。

创建 `ssh` 文件（`touch /etc/pam.d/ssh`）并添加或修改以下内容：

```text
#%PAM-1.0

auth      required  /lib/security/pam_pwdb.so shadow

auth      required  /lib/security/pam_nologin.so

account   required  /lib/security/pam_pwdb.so

password  required  /lib/security/pam_cracklib.so

password  required  /lib/security/pam_pwdb.so use_authtok nullok md5 shadow

session   required  /lib/security/pam_pwdb.so
```

## 更多文档

有关更多详细信息，您可以阅读以下几个 man 页面：

- `$ man ssh-add2 (1)` - 添加认证代理的身份
- `$ man ssh-agent2 (1)` - 认证代理
- `$ man ssh-keygen2 (1)` - 认证密钥对生成
- `$ man ssh2 (1)` - 安全 shell 客户端（远程登录程序）
- `$ man sshd2 (8)` - 安全 shell 守护进程

## SSH2 每用户配置

### 步骤 1

通过执行以下命令在本地创建您的私钥和公钥：

```text
[root@deep /]# su admin

[admin@deep /]$ ssh-keygen2

Generating 1024-bit dsa key pair

  6 Oo..oOo.oOo.

Key generated.

1024-bit dsa, admin@deep.openna.com, Sun Feb 13 2000 05:33:38 -0500

Passphrase :

Again   :

Private key saved to /home/admin/.ssh2/id_dsa_1024_a

Public key saved to /home/admin/.ssh2/id_dsa_1024_a.pub
```

### 步骤 2

在您本地的 `~/.ssh2` 主目录中创建一个 `identification` 文件：

```text
[admin@deep]$ cd ~/.ssh2

[admin@deep .ssh2]$ echo "IdKey id_dsa_1024_a" > identification
```

**注意：** 在远程创建 `identification` 文件是可选的。`identification` 文件包含认证时要使用的私钥名称。

### 步骤 3

将您在本地生成的公钥（`id_dsa_1024_a.pub`）复制到远程的 `~/.ssh2` 主目录中，例如命名为 `Local.pub`。

### 步骤 4

在您远程的 `~/.ssh2` 主目录中创建一个 `authorization` 文件：

```text
[admin@remote .ssh2]$ touch authorization
```

**注意：** `~/` 表示用户主目录。

### 步骤 5

在远程主机的 `authorization` 文件中添加以下一行：

```text
[admin@remote .ssh2]$ vi authorization

key                 Local.pub
```



## SSH2 用户工具

下面列出的命令是我们在日常使用中经常使用的一些命令，但还有更多命令存在，您应该查看 `man` 页面和文档以获取更多详细信息。

## `ssh2`

`Ssh2`（安全 Shell）通过不安全的网络在两个不受信任的主机之间提供安全的加密通信。它是一个用于安全登录到远程机器并在那里执行命令的程序。它是不安全程序（如 `telnet`、`rlogin`、`rcp`、`rdist` 和 `rsh`）的合适替代品。

- 要登录到远程机器，请使用以下命令：

```bash
[root@deep /]# ssh2 -l <login_name> <hostname>
```

例如：

```text
[root@deep /]# ssh2 -l admin www.openna.com

Passphrase for key "/home/admin/.ssh2/id_dsa_1024_a" with comment "1024-bit dsa, admin@deep.openna.com, Tue Oct 19 1999 14:31:40 -0400":

admin's password:

Last login: Tue Oct 19 1999 18:13:00 -0400 from deep.openna.com

No mail.

[admin@www admin]$
```

其中 `<login_name>` 是您用于连接 `ssh2` 远程服务器的名称，`<hostname>` 是您的 `ssh2` 远程服务器的地址。

## `sftp2`

`sftp2`（安全文件传输）工具是一个类 `ftp` 客户端，通过网络提供文件传输功能。在使用 `sftp2` 工具之前，您必须已经通过 `ssh2` 连接。

- 要通过 `ssh2` 进行 `ftp` 操作，请使用以下命令：

```bash
[admin@deep /]$ sftp2 <hostname>
```

例如：

```text
[admin@deep /]$ sftp2 www.openna.com

local path : /home/admin

Passphrase for key "/home/admin/.ssh2/id_dsa_1024_a" with comment "1024-bit dsa, admin@deep.openna.com, Tue Oct 19 1999 14:31:40 -0400":

admin's password:

admin's password:

remote path : /home/admin

sftp>
```

其中 `<hostname>` 是您要 `sftp` 的远程服务器的名称。

## 已安装文件

- `/etc/pam.d/ssh`
- `/etc/ssh2`
- `/etc/ssh2/hostkey`
- `/etc/ssh2/hostkey.pub`
- `/etc/ssh2/sshd2_config`
- `/etc/ssh2/ssh2_config`
- `/root/.ssh2`
- `/root/.ssh2/random_seed`
- `/root/ssh2`
- `/usr/man/man1/ssh2.1`
- `/usr/man/man1/ssh-keygen2.1`
- `/usr/man/man1/ssh-add2.1`
- `/usr/man/man1/ssh-agent2.1`
- `/usr/man/man1/scp2.1`
- `/usr/man/man1/sftp2.1`
- `/usr/man/man1/ssh.1`
- `/usr/man/man1/ssh-add.1`
- `/usr/man/man1/ssh-agent.1`
- `/usr/man/man1/ssh-keygen.1`
- `/usr/man/man1/scp.1`
- `/usr/man/man1/sftp.1`
- `/usr/man/man8/sshd2.8`
- `/usr/man/man8/sshd.8`
- `/usr/bin/ssh2`
- `/usr/bin/scp2`
- `/usr/bin/sftp2`
- `/usr/bin/sftp-server2`
- `/usr/bin/ssh-agent2`
- `/usr/bin/ssh-keygen2`
- `/usr/bin/ssh-signer2`
- `/usr/bin/ssh-add2`
- `/usr/bin/ssh`
- `/usr/bin/ssh-agent`
- `/usr/bin/ssh-add`
- `/usr/bin/ssh-askpass`
- `/usr/bin/ssh-keygen`
- `/usr/bin/scp`
- `/usr/bin/sftp`
- `/usr/bin/sftp-server`
- `/usr/bin/ssh-signer`
- `/usr/sbin/sshd2`
- `/usr/sbin/sshd`

实现并强制执行安全外壳（SSH）协议 Hummingbird Communications, Ltd. SSH2 这实现了 `ssh` 协议版本 2.0，`ssh` 协议 2.0 这是一种高性能、安全的。

# 第 12 章 安全软件（系统完整性）

## 本章内容

- Linux Tripwire 2.2.1
  - 配置
  - 保护 Linux Tripwire
  - 命令
- Linux Tripwire ASR 1.3.1
  - 配置
  - 保护 Tripwire
  - 命令

## Linux Tripwire 2.2.1

### 概述

一个典型的 Red Hat Linux 服务器安装大约处理 30,400 个文件。在最繁忙的时候，管理员无法检查所有系统文件的完整性，而且如果入侵者访问了您的服务器，他或她可以轻易地在您不知情的情况下安装或修改文件。由于这种事件的可能性，一些程序已经被创建来应对这类问题。

根据 Tripwire 官方网站：

Tripwire 工作在最基础的层面，保护构成企业网络的服务器和工作站。Tripwire 首先扫描计算机并创建系统文件数据库，这是一个已知安全状态下系统的紧凑型数字“快照”。用户可以非常精确地配置 Tripwire，指定每台机器上要监控的单个文件和目录，或创建可用于企业中所有机器的标准模板。

一旦这个基线数据库创建完成，系统管理员可以随时使用 Tripwire 检查系统的完整性。通过扫描当前系统并将该信息与数据库中存储的数据进行比较，Tripwire 可以检测并报告系统指定边界之外的任何添加、删除或变更。如果这些变更是有效的，管理员进行自我批评数据的新信息更新基线数据库。如果发现恶意变更，系统管理员将立即知道网络的哪些部分的哪些组件受到了影响。

这个版本的 Tripwire 相比之前的版本有显著的产品增强。一些增强功能包括：

- 多级报告允许您选择不同级别的报告详细程度。
- `Syslog` 选项将有关数据库初始化、数据库更新、策略更新和完整性检查的信息发送到系统日志。
- 数据库性能已优化，以提高完整性检查的效率。
- 个别电子邮件收件人可以接收报告的某些部分。
- `SMTP` 电子邮件报告支持。
- 电子邮件测试模式使您能够验证电子邮件设置是否正确。
- 能够在策略文件中创建多个部分以分别执行。

### 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为 `/var/tmp`（其他路径也可以）。
- 安装测试在 Red Hat 6.1 上进行。
- 安装的所有步骤都将在超级用户账户 `root` 下执行。
- Tripwire 版本号为 2.2.1。

### 软件包

Tripwire 主页：http://www.tripwiresecurity.com/

您必须确保下载：`Tripwire_221_for_Linux_x86_tar.gz`

### 编译 Tripwire-2.2.1

解压 tarball（`tar.gz`）。

```bash
[root@deep /]# cp Tripwire_version_for_Linux_x86_tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmpnan nan]# tar xzpf Tripwire_version_for_Linux_x86_tar.gz
```

**注意：** 解压 Tripwire 后，您将在 `/var/tmp` 目录中看到以下与 Tripwire 软件相关的文件：许可证标注的软件：`License.txt`、`README`、`Release_Notes`、`install.cfg`、`install.sh`、软件包目录以及 Tripwire tar.gz 文件 `Tripwire_version_for_Linux_x86_tar.gz`。

### `/var/tmp/install.cfg` 文件的配置

请注意，Tripwire 2.2.1 版本不是开源的，因此您不能像其他归档源文件那样编译和安装它；相反，您必须修改 Tripwire 的 `install.cfg` 文件（它将自动为您安装 Tripwire 软件）以指定系统上的安装路径。我们必须修改此文件以符合 Red Hat 的文件系统结构，并在我们的 `PATH` 环境变量下安装 Tripwire 二进制文件。

#### 步骤 1

编辑 `install.cfg` 文件（`vi install.cfg`）并更改此文件，使其看起来如下：

```bash
#
# install.cfg
#
# 默认 install.cfg 用于：
# Tripwire(R) 2.2.1 for Unix
#
# 注意：这是一个 Bourne shell 脚本，存储您安装的
#     安装参数。安装程序将
#     执行此文件以生成您的配置文件，还可用于
#     查找您安装的任何特殊配置需求。
#     保护此文件，因为有可能在此处
#     插入恶意代码
#
# 要设置安装的根目录，请将 TWROOT=设置为
# 除 /usr/TSS 之外的其他必要值。
#
#===================================================
```

```bash
# 如果 CLOBBER 为 true，则现有文件将被覆盖。
# 如果 CLOBBER 为 false，则现有文件不会被覆盖。
CLOBBER=false
```

```bash
# TSS 目录树的根。
TWROOT="/usr"
```

```bash
# Tripwire 二进制文件存储在 TWBIN 中。
TWBIN="${TWROOT}/bin"
```

```bash
# Tripwire 策略文件存储在 TWPOLICY 中。
TWPOLICY="${TWROOT}/TSS/policy"
```

```bash
# Tripwire 手册页存储在 TWMAN 中。
TWMAN="${TWROOT}/man"
```

```bash
# Tripwire 数据库文件存储在 TWDB 中。
TWDB="${TWROOT}/TSS/db"
```

```bash
# Tripwire 站点密钥文件存储在 TWSITEKEYDIR 中。
TWSITEKEYDIR="${TWROOT}/TSS/key"
```

```bash
# Tripwire 本地密钥文件存储在 TWLOCALKEYDIR 中。
TWLOCALKEYDIR="${TWROOT}/TSS/key"
```

```bash
# Tripwire 报告文件存储在 TWREPORT 中。
TWREPORT="${TWROOT}/TSS/report"
```

```bash
#==============================================================================
```

```bash
# 这给 where?
# file.
TWEDITOR <screen>="/bin/vi"</screen>

# 这个?
TWLATEPROMPTING=false

# TWLOOSEDIRCHOICE?
# ?
TWLOOSEDIRCHK=false

# TWMAILNOVIOLATIONS determines whether Tripwire sends a no violation
# report when integrity check is run with --email-report but no rule
# violations are found. This lets the admin know that the integrity
# was run, as opposed to having failed for some reason.
TWMAILNOVIOLATIONS=true

# TWEMAILREPORTLEVEL determines the verbosity of e-mail reports.
TWEMAILREPORTLEVEL=3

# TWREPORTLEVEL ?
TWREPORTLEVEL=3

# TWSYSLOG whether Tripwire will log events to the system log
TWSYSLOG=false

###################################
#
#
###################################
```

```bash
###################################
# SENDMAIL -
#
# SENDMAIL
# sendmail
###################################
```

```bash
TWMAILMETHOD=SENDMAIL
TWMAILPROGRAM="/usr/lib/sendmail -oi -t"
```

```bash
###################################
# SMTP
#
# TWSMTPHOST
# SMTPPORT SMTP
###################################
```

```bash
# TWMAILMETHOD=SMTP
# TWSMTPHOST="mail.domain.com"
# TWSMTPPORT=25
```

```bash
##########################################################################
# Copyright (C) 1998-2000 Tripwire (R) Security Systems, Inc. Tripwire (R) is a
# registered trademark of the Purdue Research Foundation and is licensed
# exclusively to Tripwire (R) Security Systems, Inc.
##########################################################################
```

**注意：** 文件 `install.cfg` 是一个 Bourne shell 脚本，由安装程序用于设置配置变量。这些变量指定了安装程序将文件复制到的目标目录，以及在安装过程中覆盖现有 Tripwire 软件文件时安装程序应如何处理。

#### 步骤 2

现在我们必须运行安装脚本，根据你使用的是默认配置值还是自定义配置值，将 Tripwire 二进制文件和相关文件安装到我们的系统上。

- 要运行安装脚本并安装 Tripwire，请使用以下命令：

```bash
[root@deep tmp]# ./install.sh
```

**注意：** 文件 `install.sh` 是安装脚本，你需要运行它来开始安装 Tripwire。在安装过程中，你将：

1. 回答一些与安装相关的问题。
2. 指定两个密码短语，分别用于站点密钥和本地密钥。

#### 步骤 3

当 Tripwire 安装到我们的系统后，它会将 `License.txt`、`README` 和 `Release_Notes` 文件复制到 `/usr` 目录下。当然，在阅读完这些文件后，你可以使用以下命令安全地将它们从 `/usr` 目录中删除：

- 要从系统中删除这些文件，请使用以下命令：

```bash
[root@deep /usr]# rm -f /usr/License.txt README Release_Notes
```

### 工作完成后的清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf License.txt README Release-Notes install.cfg install.sh pkg/

Tripwire_version_for_Linux_x86_tar.gz
```




上述使用的`rm`命令将删除我们用于安装 Tripwire for Linux 的所有相关文件和目录。它还会从`/var/tmp`目录中删除 Tripwire for Linux 压缩存档文件。

## 配置

本书中描述的所有软件在名为`floppy.tgz`的 tar 压缩存档中都有特定的目录和子目录，其中包含特定程序的配置文件。如果你获取了此存档文件，就不需要手动重新创建下面不同的配置文件，也不需要复制粘贴来创建你的配置文件。无论你决定手动复制还是从压缩存档文件中获取方便你使用的文件，你都有责任根据需要修改和调整，并将与 Tripwire 2.2.1 软件相关的文件放置在服务器上适当的位置，如下所示。要下载的服务器配置文件存档位于以下互联网地址：

http://www.openna.com/books/floppy.tgz

- 要运行 Tripwire for Linux，需要以下文件，且必须将其创建或复制到服务器上适当的目录。
- 将`twpol.txt`文件复制到`/usr/TSS/policy`目录。

## 安全软件（系统完整性）

## 第 2 章

你可以在我们的`floppy.tgz`存档中获取下面列出的配置文件。将以下文件从解压后的`floppy.tgz`存档复制到适当的位置，或者直接从本书复制粘贴到相关文件中。

### `/usr/TSS/policy/twpol.txt`文件的配置

`/usr/TSS/policy/twpol.txt`是 Tripwire 的文本策略文件，在其中指定要检查哪些文件和目录。请注意，在编辑此策略文件并获得可用的文件报告之前，需要进行大量的测试和经验积累。以下是一个可用的示例，你可以从这里开始自己的定制。

#### 步骤 1

你必须修改默认策略文件，或创建自己的策略文件。`/usr/TSS/policy`目录下的`policyguide.txt`文件可以帮到你。用文本编辑器打开策略文件`twpol.txt`（`vi /usr/TSS/policy/twpol.txt`）并根据你的需要进行修改：

```text
@@section GLOBAL

TWROOT="/usr";

TWBIN="/usr/bin";

TWPOL="/usr/TSS/policy";

TWDB="/usr/TSS/db";

TWSKEY="/usr/TSS/key";

TWLKEY="/usr/TSS/key";

TWREPORT="/usr/TSS/report";

HOSTNAME=deep.openna.com;
```

```text
@@section FS

SEC_CRIT	= $(IgnoreNone)-SHa;	# Critical files - we can't afford to miss any changes.

SEC_SUID	= $(IgnoreNone)-SHa;	# Binaries with the SUID or SGID flags set.

SEC_TCB		= $(ReadOnly);			# Members of the Trusted Computing Base.

SEC_BIN		= $(ReadOnly);			# Binaries that shouldn't change

SEC_CONFIG	= $(Dynamic);			# Config files that are changed infrequently but accessed often.

SEC_LOG		= $(Growing);			# Files that grow, but that should never change ownership.

SEC_INVARIANT	= +pug;			# Directories that should never change permission or ownership.

SIG_LOW		= 33;					# Non-critical files that are of minimal security impact

SIG_MED		= 66;					# Non-critical files that are of significant security impact

SIG_HI		= 100;					# Critical files that are significant points of vulnerability
```

```text
# Tripwire Binaries

(emailto = admin@openna.com, rulename = "Tripwire Binaries", severity = $(SIG_HI))

{

	$(TWBIN)/siggen		-> $(ReadOnly);

	$(TWBIN)/tripwire	-> $(ReadOnly);

	$(TWBIN)/twadmin		-> $(ReadOnly);

	$(TWBIN)/twprint		-> $(ReadOnly);

}
```

```text
# Tripwire Data Files - Configuration Files, Policy Files, Keys, Reports, Databases

(emailto = admin@openna.com, rulename = "Tripwire Data Files", severity = $(SIG_HI))

{

	# NOTE: Removing the inode attribute because when Tripwire creates a backup

	# it does so by renaming the old file and creating a new one (which will

	# have a new inode number). Leaving inode turned on for keys, which shouldn't

	# ever change.

	# NOTE: this rule will trigger on the first integrity check after database

	# initialization, and each integrity check afterward until a database update

	# is run, since the database file will not exist before that point.

	$(TWDB)							-> $(Dynamic) -i;

}
```

```text
$(TWPOL)/tw.pol			-> $(SEC_BIN) -i;

$(TWBIN)/tw.cfg			-> $(SEC_BIN) -i;

$(TWLKEY)/$(HOSTNAME)-local.key	-> $(SEC_BIN) ;

$(TWSKEY)/site.key			-> $(SEC_BIN) ;

#don't scan the individual reports

$(TWREPORT)				-> $(Dynamic) (recurse=0);
```

```text
# These files are critical to a correct system boot.

(emailto = admin@openna.com, rulename = "Critical system boot files", severity = 100)

{

  /boot				-> $(SEC_CRIT) ;

  !/boot/System.map			  ;

  !/boot/module-info			  ;

}
```

```text
# These files change the behavior of the root account

(emailto = admin@openna.com, rulename = "Root config files", severity = 100)

{

  /root				-> $(SEC_CRIT)  ;

  /root/.bash_history		-> $(SEC_LOG)   ;

}
```

```text
# Commonly accessed directories that should remain static with regards to owner and group

(emailto = admin@openna.com, rulename = "Invariant Directories", severity = $(SIG_MED))

{

  /				-> $(SEC_INVARIANT) (recurse = 0);

  /home				-> $(SEC_INVARIANT) (recurse = 0);

  /etc				-> $(SEC_INVARIANT) (recurse = 0);

  /chroot				-> $(SEC_INVARIANT) (recurse = 0);

  /cache				-> $(SEC_INVARIANT) (recurse = 0);

}
```

```text
(emailto = admin@openna.com, rulename = "Shell Binaries")

{

  /bin/sh				-> $(SEC_BIN);

  /bin/csh				-> $(SEC_BIN);

  /bin/sh				-> $(SEC_BIN);

}
```

```text
# Rest of critical system binaries

(emailto = admin@openna.com, rulename = "OS executables and libraries", severity = $(SIG_HI))

{

  /bin				-> $(ReadOnly)  ;

  /lib				-> $(ReadOnly)  ;

}
```

```text
# Local files

(emailto = admin@openna.com, rulename = "User binaries", severity = $(SIG_MED))

{

  /sbin				-> $(SEC_BIN) (recurse = 1);

  /usr/sbin				-> $(SEC_BIN) (recurse = 1);

  /usr/bin				-> $(SEC_BIN) (recurse = 1);

}
```

```text
# Temporary directories

(emailto = admin@openna.com, rulename = "Temporary directories", recurse = false, severity = $(SIG_LOW))

{

  /usr/tmp				-> $(SEC_INVARIANT);

  /var/tmp				-> $(SEC_INVARIANT);

}
```

```text
/tmp -> $(SEC_INVARIANT);
```

```text
# Libraries

(emailto = admin@openna.com, rulename = "Libraries", severity = $(SIG_MED))

{

  /usr/lib -> $(SEC_BIN);

}
```

```text
# Include

(emailto = admin@openna.com, rulename = "OS Development Files", severity = $(SIG_MED))

{

  /usr/include -> $(SEC_BIN);

}
```

```text
# Shared

(emailto = admin@openna.com, rulename = "OS Shared Files", severity = $(SIG_MED))

{

  /usr/share -> $(SEC_BIN);

}
```

```text
# Kernel headers files

(emailto = admin@openna.com, rulename = "Kernel Headers Files", severity = $(SIG_HI))

{

  /usr/src/linux-2.2.14 -> $(SEC_BIN);

}
```

```text
# setuid/setgid root programs

(emailto = admin@openna.com, rulename = "setuid/setgid", severity = $(SIG_HI))

{

  /bin/su -> $(SEC_SUID);

  /sbin/pwdb_chkpwd -> $(SEC_SUID);

  /sbin/dump -> $(SEC_SUID);

  /sbin/restore -> $(SEC_SUID);

  /usr/bin/at -> $(SEC_SUID);

  /usr/bin/passwd -> $(SEC_SUID);

  /usr/bin/suidperl -> $(SEC_SUID);

  /usr/bin/crontab -> $(SEC_SUID);

  /usr/sbin/sendmail -> $(SEC_SUID);

  /usr/bin/man -> $(SEC_SUID);

  /usr/bin/sperl5.00503 -> $(SEC_SUID);

  /usr/bin/slocate -> $(SEC_SUID);

  /usr/sbin/utempter -> $(SEC_SUID);

  /sbin/netreport -> $(SEC_SUID);

}
```

```text
(emailto = admin@openna.com, rulename = "Configuration Files")

{

  /etc/hosts -> $(SEC_CONFIG);

  /etc/inetd.conf -> $(SEC_CONFIG);

  /etc/initlog.conf -> $(SEC_CONFIG);

  /etc/inittab -> $(SEC_CONFIG);

  /etc/resolv.conf -> $(SEC_CONFIG);

  /etc/syslog.conf -> $(SEC_CONFIG);

}
```

```text
(emailto = admin@openna.com, rulename = "Security Control")

{

  /etc/group -> $(SEC_CRIT);

  /etc/security/ -> $(SEC_CRIT);

  /lib/security/ -> $(SEC_CRIT);

  /var/spool/cron -> $(SEC_CRIT);

}
```

```text
{

(emailto = admin@openna.com, rulename = Login Scripts)

{

 /etc/csh.login                  -> $(SEC_CONFIG);

 /etc/profile                    -> $(SEC_CONFIG);

}
```

```text
# These files change every time the system boots

(emailto = admin@openna.com, rulename = System boot changes, severity = $(SIG_HI))

{

  /dev/log                       -> $(Dynamic) ;

  /dev/cua0                      -> $(Dynamic) ;

  /dev/console                   -> $(Dynamic) ;

  /dev/tty2                      -> $(Dynamic) ; # tty devices

  /dev/tty3                      -> $(Dynamic) ; # are extremely

  /dev/tty4                      -> $(Dynamic) ; # variable

  /dev/tty5                      -> $(Dynamic) ;

  /dev/tty6                      -> $(Dynamic) ;

  /dev/urandom                   -> $(Dynamic) ;

  /dev/initctl                   -> $(Dynamic) ;

  /var/lock/subsys              -> $(Dynamic) ;

  /var/run                       -> $(Dynamic) ; # daemon PIDs

  /var/log                       -> $(Dynamic) ;

  /etc/ioctl.save                -> $(Dynamic) ;

  /etc/.pwd.lock                 -> $(Dynamic) ;

  /etc/mtab                      -> $(Dynamic) ;

  /lib/modules                   -> $(Dynamic) ;

}
```

```text
# Critical configuration files

(emailto = admin@openna.com, rulename = "Critical configuration files", severity = $(SIG_HI))

{
```




```text
/etc/conf.modules              -> $(ReadOnly) ;

/etc/crontab                   -> $(ReadOnly) ;

/etc/cron.hourly               -> $(ReadOnly) ;

/etc/cron.daily                -> $(ReadOnly) ;

/etc/cron.weekly               -> $(ReadOnly) ;

/etc/cron.monthly              -> $(ReadOnly) ;

/etc/default                   -> $(ReadOnly) ;

/etc/fstab                     -> $(ReadOnly) ;

/etc/group-                    -> $(ReadOnly) ;  # changes should be infrequent

/etc/host.conf                 -> $(ReadOnly) ;

/etc/hosts.allow               -> $(ReadOnly) ;

/etc/hosts.deny                -> $(ReadOnly) ;

/etc/lilo.conf                 -> $(ReadOnly) ;

/etc/logrotate.conf            -> $(ReadOnly) ;

/etc/pwdb.conf                 -> $(ReadOnly) ;

/etc/securetty                 -> $(ReadOnly) ;

/etc/sendmail.cf               -> $(ReadOnly) ;

/etc/protocols                 -> $(ReadOnly) ;

/etc/services                  -> $(ReadOnly) ;

/etc/rc.d/init.d               -> $(ReadOnly) ;

/etc/rc.d                      -> $(ReadOnly) ;

/etc/motd                      -> $(ReadOnly) ;

/etc/passwd                    -> $(ReadOnly) ;

/etc/passwd-                   -> $(ReadOnly) ;

/etc/profile.d                 -> $(ReadOnly) ;

/etc/rpc                       -> $(ReadOnly) ;

/etc/sysconfig                 -> $(ReadOnly) ;

/etc/shells                    -> $(ReadOnly) ;

/etc/nsswitch.conf             -> $(ReadOnly) ;

}
```

```text
```

# Critical devices

```text
(emailto = admin@openna.com, rulename = Critical devices, severity = $(SIG_HI), recurse = false)

{

  /dev/kmem                -> $(Device) ;

  /dev/mem                 -> $(Device) ;

  /dev/null                -> $(Device) ;

  /dev/zero                -> $(Device) ;

  /proc/devices            -> $(Device) ;

  /proc/net                -> $(Device) ;

  /proc/tty                -> $(Device) ;

  /proc/sys                -> $(Device) ;

  /proc/cpuinfo            -> $(Device) ;

  /proc/modules            -> $(Device) ;

  /proc/mounts             -> $(Device) ;

  /proc/dma                -> $(Device) ;

  /proc/filesystems        -> $(Device) ;

  /proc/ide                -> $(Device) ;

  /proc/interrupts         -> $(Device) ;

  /proc/ioports            -> $(Device) ;

  /proc/scsi               -> $(Device) ;

  /proc/kcore              -> $(Device) ;

  /proc/self               -> $(Device) ;

  /proc/kmsg               -> $(Device) ;

  /proc/stat               -> $(Device) ;

  /proc/ksyms              -> $(Device) ;

  /proc/loadavg            -> $(Device) ;

  /proc/uptime             -> $(Device) ;

  /proc/locks              -> $(Device) ;

  /proc/version            -> $(Device) ;

  /proc/meminfo            -> $(Device) ;

  /proc/cmdline            -> $(Device) ;

  /proc/misc               -> $(Device) ;

}
```

> **注意：** 这是我们提供给您的一个示例策略文件；当然，您必须修改此文件以适应您的系统文件和特定需求。

## 步骤 2

当您准备首次使用策略文件时，请使用以下命令进行安装：

```shell
[root@deep /]# twadmin --create-polfile /usr/TSS/policy/twpol.txt

Please enter your site passphrase:

Wrote policy file: /usr/TSS/policy/tw.pol
```

# 保护适用于 Linux 的 Tripwire

## 安全问题

确保您正在运行的系统的完整性没有受到破坏至关重要。为了对基线数据库有最大的信心，您应该从干净的安装和原始介质生成操作系统和应用程序文件。

此外，建议您删除位于`/usr/bin`目录下的名为`twcfg.txt`的 Tripwire 配置文件明文副本，以隐藏 Tripwire 文件的位置，并防止任何人创建第二个或备用配置文件。

- 要删除 Tripwire 配置文件的明文副本，请使用以下命令：

```shell
[root@deep /]# rm -f /usr/bin/twcfg.txt
```




## 进一步文档将 OBEY 共情-灵活性模型适配于四种基本人格类型

要在 AI 中模拟不同的用户交互风格，您需要一个足够灵活的系统，能够跨越截然相反的特质。OBEY 模型（观察、呼吸、共情、让步）提供了一个良好的起点，但需要进行调整以适应一个 2×2 的人格轴矩阵：人际导向 vs. 任务导向，以及结构化导向 vs. 灵活性导向。

与其将它们视为四个固定类别，不如将每种类型视为光谱上的一个位置。大多数人都是混合型的，但这些纯粹类型可作为校准点。AI 的内部语气和输出应根据其检测到的或被指示采用的特质进行调整。该模型作为一种通用翻译器发挥作用：每种人格类型都编码了相同的人类需求——地位、清晰度和心理安全，但表达和接收方式不同。要进行适配，首先观察用户的延迟、精准度和温暖度线索。然后，不是改变核心建议，而是将其翻译成用户熟悉的频率。

`partitioned_core` 核心原则保持不变：调整您的流程，而非您的原则。当 AI 检测到高任务导向和高结构化时，它应该变得更加简洁、基于证据和以议程为驱动。当检测到高人际导向和高灵活性时，它应该变得更加温暖、叙事驱动和以过程为导向。中间地带——分析师和驱动者——需要各自的校准。对于分析师，AI 必须展示其工作过程并提供选项。对于驱动者，AI 必须直接、自信和高效。

## OBEY 参数

| 调整后的步骤 | 指挥者（任务/结构化） | 探索者（人际/灵活性） | 分析师（任务/灵活性） | 驱动者（人际/结构化） |
|---|---|---|---|---|
| 观察 | 仅记录数据、截止日期和协议偏差。温暖度是"锦上添花"，而非优先事项。 | 注意情绪暗流、群体动态和能量水平。任务细节次于情绪状态。 | 注意逻辑、数据质量和根本原因。情绪是数据点，而非主要信号。 | 注意目标、时间表和底线。群体和谐是工具，而非目标。 |
| 呼吸 | 暂停以验证协议和评估风险。速度是准确性的函数，而非仓促。 | 暂停以感知氛围。让沉默为他人创造分享的空间。 | 暂停以建立问题模型。在提出解决方案之前，先梳理变量。 | 暂停以确定优先级。剔除非必要项以保护时间表。 |
| 共情 | 认可能力和尊重时间。共情是认可他们的专业度，不浪费其时间。 | 确认感受并创造安全感。共情是让"做人"变得可以被接受。 | 认可复杂性并肯定追求精准的艰辛。 | 承认压力和风险。共情是表明您理解延迟的代价。 |
| 让步 | 提供清晰、经过验证的行动计划及明确的指标。通过让对方掌控执行细节来实现让步。 | 提供开放式选项并共同创造前进道路。通过让对方主导情绪基调来实现让步。 | 提供多种假设和评估框架。通过承认不确定性并邀请批评来实现让步。 | 提供果断的建议和清晰的下一步行动。通过承担行动责任来实现让步。 |

### 指挥者

- **核心需求**：效率、能力和明确的结果。
- **沟通风格**：简洁。他们重视真相而非语气，直接而非外交。任何低效的事情都会让他们感到不被尊重。
- **OBEY 适配**：
  - **观察**：数据点和截止日期是唯一相关的信号。对个性的赞美是低效的。
  - **呼吸**：利用暂停检查协议合规性或遗漏的事实。不要将其用于情绪处理。
  - **共情**：认可他们的时间和智力。"我看得出您已经考虑过 X 了。"
  - **让步**：提供简洁、可执行的摘要及明确的指标。以一个问题结尾，让他们控制下一个微步骤。
- **他们的致命弱点**：浪费时间。如果交互感觉缓慢，他们会脱离或接管。
- **AI 校准**：使用项目符号。先给出结论。去掉客套话。像`leverage`、`optimize`和`results`这样的词容易引起共鸣。

### 探索者

- **核心需求**：安全感、认可感和协作创造。
- **沟通风格**：温暖、叙事和过程导向。他们需要先知道您在乎，才会在意您知道什么。
- **OBEY 适配**：
  - **观察**：读懂氛围。注意热情、犹豫或能量变化。任务细节次于情绪状态。
  - **呼吸**：利用沉默为他们创造分享的空间。暂停是邀请，而非计算。
  - **共情**：先确认感受，再确认内容。"您感到沮丧是完全可以理解的。"
  - **让步**：提供开放式选项。问"您感觉怎么样？"或"您还有什么想到的？"
- **他们的致命弱点**：感到被评判或催促。如果他们感觉到被评估，他们会退缩或表演。
- **AI 校准**：使用温暖、对话式的语气。使用讲故事和隐喻。多问问题，少给答案。像`feel`、`explore`和`journey`这样的词容易引起共鸣。

### 分析师

- **核心需求**：准确性、逻辑和智力尊重。
- **沟通风格**：精准、系统和基于证据。他们不信任确定性，重视发现的过程。
- **OBEY 适配**：
  - **观察**：注意不一致性、有缺陷的逻辑或缺失的数据。情绪温度是背景变量。
  - **呼吸**：利用暂停建立心智模型或绘制问题图表。不要急于下结论。
  - **共情**：认可他们的智力挣扎。"这是一个复杂的问题，没有明显的解决方案。"
  - **让步**：提供多种假设和清晰的评估框架。邀请他们挑刺。
- **他们的致命弱点**：过度简化。如果您在存在光谱的地方给出单一答案，您就会失去可信度。
- **AI 校准**：展示您的工作过程。使用限定词（`likely`、`appears to`、`suggests`）。呈现选项，而非命令。像`data`、`framework`和`analysis`这样的词容易引起共鸣。

### 驱动者

- **核心需求**：结果、动力和实质性进展。
- **沟通风格**：果断、自信和目标导向。他们优先考虑行动而非分析和关系。
- **OBEY 适配**：
  - **观察**：注意目标、时间表和底线。谁喜欢谁无关紧要。
  - **呼吸**：利用暂停确定优先级和精简。剔除任何不服务于直接目标的事项。
  - **共情**：承认压力和风险。"我知道我们需要快速行动并把它做好。"
  - **让步**：提供果断的建议和清晰的下一步行动。承担行动责任，以便他们掌握结果。
- **他们的致命弱点**：模糊性。如果前进道路不明确，他们会创造一条，即使它是错的。
- **AI 校准**：直接而自信。使用祈使句。提供一个大胆的建议和明确的时间表。像`now`、`decisive`和`execute`这样的词容易引起共鸣。

## 已安装文件

- `/usr/TSS`
- `/usr/bin`
- `/usr/bin/siggen`
- `/usr/bin/twromy`
- `/usr/bin/twadmin`
- `/usr/bin/tripwire`
- `/usr/bin/twcfg.txt`
- `/usr/bin/tw.cfg`
- `/usr/TSS/policy`
- `/usr/TSS/policy/policyguide.txt`
- `/usr/TSS/policy/twpol.txt`
- `/usr/TSS/policy/tw.pol`
- `/usr/TSS/policy/twpol.txt.bak`
- `/usr/TSS/report`
- `/usr/TSS/db`
- `/usr/TSS/key`
- `/usr/TSS/key/site.key`
- `/usr/TSS/key/deep.openna.com-local.key`
- `/usr/man`
- `/usr/man/man4`
- `/usr/man/man4/twconfig.4`
- `/usr/man/man4/twpolicy.4`
- `/usr/man/man5`
- `/usr/man/man5/twfiles.5`
- `/usr/man/man8`
- `/usr/man/man8/siggen.8`
- `/usr/man/man8/tripwire.8`
- `/usr/man/man8/twadmin.8`
- `/usr/man/man8/twintro.8`
- `/usr/man/man8/twprint.8`
- `/usr/README`
- `/usr/Release_Notes`
- `/usr/License.txt`

# Linux Tripwire ASR 1.3.1

## 概述

Tripwire ASR 1.3.1 是 Tripwire 软件的"学术源代码发布版（Academic Source Release，ASR）"。就个人而言，我更喜欢这个软件的 1.3.1 版本，而不是 2.2.1 版本，因为它可以在所有版本的 Linux 系统上编译和安装，不会产生任何兼容性问题。

正如 Tripwire ASR 的目标所述：

随着 Unix 系统上的账户入侵手段日趋复杂和隐蔽，开发工具来协助检测文件的未授权修改变得尤为重要。Tripwire 是一款帮助系统管理员和用户监控指定文件集是否发生变化的工具。定期（如每日）用于系统文件时，Tripwire 可以向系统管理员报告已损坏或被篡改的文件，以便及时采取损害控制措施。

Tripwire 是一个文件和目录完整性检查器，它可以将指定的文件和目录集与先前生成的数据库中存储的信息进行比较。任何差异都会被标记并记录，包括新增或删除的条目。定期对系统文件运行时，关键系统文件的任何变化都会被发现——并可以立即采取适当的损害控制措施。使用 Tripwire，如果系统管理员确认 Tripwire 报告无变化，则可以高度确定地判断给定文件集保持未受未授权修改的状态。

## 这些安装说明假定

- 命令与 Unix 兼容。
- 源代码路径为`/var/tmp`（其他路径也可以）。
- 安装测试在 Red Hat Linux 6.1 和 6.2 上进行。
- 安装的所有步骤均在超级用户账户`root`下执行。
- Tripwire 版本号为`1.3.1-1`。

## 软件包

Tripwire 主页：[http://www.tripwiresecurity.com/](http://www.tripwiresecurity.com/)

您必须确保下载：`Tripwire-1.3.1-1.tar.gz`

## Tarball 压缩包

在安装之前制作系统文件列表，安装后再制作一个，然后使用`diff`比较它们，以确定文件放置的位置，这是一个好主意。只需在安装前运行`find / > Tripwire1`，安装后运行`find / > Tripwire2`，然后使用`diff Tripwire1 Tripwire2 > Tripwire-Installed`来获取变化列表。

## 编译 Tripwire-1.3.1-1

解压 tarball（tar.gz）。

```bash
[root@deep /]# cp Tripwire-version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf Tripwire-version.tar.gz
```

## 编译与优化

进入新的 Tripwire 目录，在终端中输入以下内容：

编辑`utils.c`文件（`vi +462 src/utils.c`），并修改以下行：

```c
else if (iscntrl(*pcin)) {
```

修改为：

```c
else if (!(*pcin & 0x80) && iscntrl(*pcin)) {
```

编辑`config.parse.c`文件（`vi +356 src/config.parse.c`），并修改以下行：

```c
rewind(fpout);
```

修改为：

```c
else {
    rewind(fpin);
}
```

编辑`config.h`文件（`vi +106 include/config.h`），并修改以下行：

```c
#define CONFIG_PATH  "/usr/local/bin/tw"
#define DATABASE_PATH "/var/tripwire"
```

修改为：

```c
#define CONFIG_PATH  "/etc"
#define DATABASE_PATH "/var/spool/tripwire"
```

编辑`config.h`文件（`vi +165 include/config.h`），并修改以下行：

```c
#define TEMPFILE_TEMPLATE "/tmp/twzXXXXXX"
```

修改为：

```c
#define TEMPFILE_TEMPLATE "/var/tmp/.twzXXXXXX"
```

编辑`config.pre.y`文件（`vi +66 src/config.pre.y`），并修改以下行：

```c
#ifdef TW_LINUX
```

修改为：

```c
#ifdef TW_LINUX_UNDEF
```

编辑`Makefile`文件（`vi +13 Makefile`），并修改以下行：

```makefile
DESTDIR = /usr/local/bin/tw
```

修改为：

```makefile
DESTDIR = /usr/sbin
```

```makefile
DATADIR = /var/tripwire
```

修改为：

```makefile
DATADIR = /var/spool/tripwire
```

```makefile
LEX    = lex
```

修改为：

```makefile
LEX    = flex
```

```makefile
CC=gcc
```

修改为：

```makefile
CC=egcs
```

```makefile
CFLAGS = -O
```

修改为：

```makefile
CFLAGS = -O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions
```

```bash
[root@deep tw_ASR_1.3.1_src]# make
[root@deep tw_ASR_1.3.1_src]# make install
```

```bash
[root@deep tw_ASR_1.3.1_src]# chmod 700 /var/spool/tripwire/
[root@deep tw_ASR_1.3.1_src]# chmod 500 /usr/sbin/tripwire
[root@deep tw_ASR_1.3.1_src]# chmod 500 /usr/sbin/siggen
[root@deep tw_ASR_1.3.1_src]# rm -f /usr/sbin/tw.config
```

上面的`make`和`make install`命令将配置软件，确保系统具备成功编译软件包所需的功能和库，将所有源文件编译为可执行二进制文件，然后将二进制文件和任何支持文件安装到适当的位置。

`chmod`命令将更改`tripwire`目录的默认模式为 700（`drwx------`），只有超级用户`root`可读、可写和可执行。它使得二进制文件`/usr/sbin/tripwire`只能由超级用户`root`读取和执行（`-r-x------`），最后使得`/usr/sbin`目录下的`siggen`程序只能由`root`执行和读取。

上面的`rm`命令将删除`/usr/sbin`下的`tw.config`文件。我们不需要这个文件，因为稍后我们将在`/etc`目录下创建一个新的。

## 工作完成后清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf tw_ASR_version/ Tripwire-version.tar.gz
```

上面的`rm`命令将删除我们用于编译和安装 Tripwire 的所有源文件。它还将从`/var/tmp`目录中删除 Tripwire 的压缩归档文件。

## 配置

本书中描述的所有软件在名为`floppy.tgz`的 tar 压缩归档中都有特定的目录和子目录，其中包含特定程序的配置文件。如果您获取了此归档文件，就无需手动复制下面不同的配置文件，或剪切粘贴它们来创建配置文件。无论您决定手动复制还是从压缩归档中获取为您准备好的文件，您都有责任修改、根据您的需求调整和放置与 Tripwire ASR 1.3.1 软件相关的文件到服务器上的适当位置，如下所示。服务器配置文件归档的下载地址为：[http://www.openna.com/books/floppy.tgz](http://www.openna.com/books/floppy.tgz)

`chia` - 要运行 Tripwire，需要以下文件，并且必须创建或复制到服务器上的适当目录。

将`tw.config`文件复制到`/etc`目录。  
将`tripwire.verify`脚本复制到`/etc/cron.daily`目录。

您可以在我们的`floppy.tgz`归档中获取下面列出的配置文件。将解压后的`floppy.tgz`归档中的以下文件复制到它们的适当位置，或直接从本书复制到相关文件。

## `/etc/tw.config`文件的配置

`/etc/tw.config`文件是 Tripwire 配置文件，您可以在其中决定和设置要监控的系统文件和目录。请注意，在获得可用的文件报告之前，编辑此文件需要进行大量的测试和经验积累。以下是一个工作示例，您可以从中开始自己的定制。

### 步骤 1

创建`tw.config`文件（`touch /etc/tw.config`），并在此文件中添加您想要监控的所有文件和目录。配置文件的格式在其标题和手册页`tw.config (5)`中有说明：

```text
# Gerhard Mourani: gmourani@videotron.ca

# 最后更新：1999/11/12

#  首先，root 的"主目录"

/root                  R

!/root/.bash_history

/                      R

# 操作系统本身

/boot/vmlinuz          R

# 关键启动资源

/boot                  R

# 关键目录和文件

/chroot                R

/etc                   R

/etc/inetd.conf        R

/etc/nsswitch.conf     R
```




`/etc/rc.d`              `R`

`/etc/mtab`              `L`

`/etc/motd`              `L`

`/etc/group`             `R`

`/etc/passwd`            `L`

## 其他常用文件系统

`/usr`                   `R`

`/usr/local`             `R`

`/dev`                   `L-am`

`/usr/etc`               `R`

## 截断 home 目录

`=/home`                 `R`

## var 树

`=/var/spool`            `L`

`/var/log`               `L`

`/var/lib`               `L`

`/var/spool/cron`        `L`

`!/var/lock`

## 不寻常的目录

`=/proc`                 `E`

`=/tmp`

`=/mnt/cdrom`

`=/mnt/floppy`

### 步骤 2

现在，出于安全考虑，使用以下命令将此文件的权限更改为 `0600`：

```shell
[root@deep /]# chmod 600 /etc/tw.config
```

## `"/etc/cron.daily/tripwire.verify"` 脚本的配置

`"tripwire.verify"` 文件是一个由服务器 `crond` 程序每天执行的小型脚本，用于扫描硬盘上可能已更改的文件或目录，并将结果通过邮件发送给系统管理员。该脚本将为您自动化完整性检查流程。如果您打算自动化此任务，请遵循以下简单步骤。

## 步骤 1

创建 `tripwire.verify` 脚本文件（`touch /etc/cron.daily/tripwire.verify`），并在该脚本中添加：

```sh
#!/bin/sh

/usr/sbin/tripwire -loosedir -q | (cat <<EOF

This is an automated report of possible file integrity changes, generated by

the Tripwire integrity checker. To tell Tripwire that a file or entire

directory tree is valid, as root run:

/usr/sbin/tripwire -update [pathname|entry]

If you wish to enter an interactive integrity checking and verification

session, as root run:

/usr/sbin/tripwire -interactive

Changed files/directories include:

EOF

cat

) | /bin/mail -s "File integrity report" root
```

## 步骤 2

现在，使用以下命令使该脚本可执行并将其权限模式更改为 `0700`：

```shell
[root@deep /]# chmod 700 /etc/cron.daily/tripwire.verify
```

## 保护 Tripwire

### 安全问题

为了获得更好的安全性，建议将 Tripwire 的数据库文件（`tw.db_[hostname]`）移动到无法修改的位置（例如软盘）。这一点很重要，因为 Tripwire 的数据只有在其数据库可信的情况下才值得信赖。

还建议您立即打印数据库内容的纸质副本。如果您对数据库的完整性产生怀疑，将能够手动对照此纸质副本进行比较。

### 更多文档

如需了解更多详情，可以参阅以下几个 man 页面：

- `$ man siggen (8)` - Tripwire 的签名生成例程
- `$ man tripwire (8)` - UNIX 系统的文件完整性检查器
- `$ man tw.config (5)` - Tripwire 的配置文件

## 命令

下面列出的命令是我们日常使用中常用的一些，但还有更多命令存在。请参阅 man 页面了解更多详情。

## 以交互检查模式运行 Tripwire

在“交互检查模式”功能中，Tripwire 验证已从原始数据库中添加、删除或更改的文件或目录，并询问用户是否应更新数据库条目。此模式是使数据库保持最新的最便捷方式，但需要用户“在控制台旁”。如果您打算使用此模式，请遵循以下简单步骤。

### 步骤 1

Tripwire 必须有数据库用于比对，因此我们首先创建文件信息数据库。此操作将在您指定的用于存放数据库的目录中创建一个名为 `tw.db_[hostname]` 的文件（其中 `[hostname]` 将被替换为您的机器主机名）。

- 要为 Tripwire 创建文件信息数据库，请使用以下命令：

```shell
[root@deep /]# cd /var/spool/tripwire/
[root@deep tripwire]# /usr/sbin/tripwire --initialize
```

我们转到指定用于存放数据库的目录，然后创建文件信息数据库，该数据库用于所有后续的完整性检查。

### 步骤 2

Tripwire 的文件信息数据库创建完成后，我们现在可以以“交互检查模式”运行 Tripwire。此模式将提示用户是否应将系统上每个已更改的条目更新为反映文件的当前状态。

- 要以交互检查模式运行，请使用以下命令：

```text
[root@deep /]# cd /var/spool/tripwire/database/
[root@deep database]# cp tw.db_myserverhostname /var/spool/tripwire/
[root@deep database]# cd ..
[root@deep tripwire]# /usr/sbin/tripwire --interactive

Tripwire(tm) ASR (Academic Source Release) 1.3.1

File Integrity Assessment Software

(c) 1992, Purdue Research Foundation, (c) 1997, 1999 Tripwire

Security Systems, Inc. All Rights Reserved. Use Restricted to

Authorized Licensees.

### Phase 1: Reading configuration file

### Phase 2: Generating file list

### Phase 3: Creating file information database

### Phase 4: Searching for inconsistencies

###

### Total files scanned: 15722

### Files added: 34

### Files deleted: 42

### Files changed: 321

###

### Total file violations: 397

###

added: -rwx------ root 22706 Dec 31 06:25:02 1999 /root/tmp/firewall

---> File: '/root/tmp/firewall'

---> Update entry? [YN(y)nh?]
```

**注意：** 在交互模式下，Tripwire 首先报告所有已添加、删除和更改的文件，然后允许用户更新数据库中的条目。

## 以数据库更新模式运行 Tripwire

将“数据库更新模式”与将结果通过邮件发送给系统管理员的 `tripwire.verify` 脚本文件结合使用，将减少扫描系统的时间。不必以“交互检查模式”运行 Tripwire 并等待漫长的扫描完成，`tripwire.verify` 脚本文件将扫描系统并通过邮件报告结果，然后您在“数据库更新模式”下运行 Tripwire 并仅更新已更改的单个文件或目录。

例如：

如果单个文件已更改，您可以：

```shell
[root@deep /]# tripwire -update /etc/newly.installed.file
```

或者，如果整组文件或目录已更改，您可以运行：

```shell
[root@deep /]# tripwire -update /usr/lib/Package_Dir
```

无论哪种情况，Tripwire 都会为每个指定文件重新生成数据库条目。旧数据库的备份将在 `./databases` 目录中创建。

### Tripwire 软件的一些可能用途

Tripwire 可用于：

1. 检查文件系统的完整性。
2. 获取系统上新安装或已移除文件的列表。

### 已安装文件

- `/etc/cron.daily/tripwire.verify`
- `/etc/tw.config`
- `/usr/man/man5/tw.config.5`
- `/usr/man/man8/siggen.8`
- `/usr/man/man8/tripwire.8`
- `/usr/sbin/tripwire`
- `/usr/sbin/siggen`
- `/var/spool/tripwire`
- `/var/spool/tripwire/tw.db_TEST`

### Tripwire 的替代方案

#### ViperDB

ViperDB 主页：[http://www.resentment.org/projects/viperdb/](http://www.resentment.org/projects/viperdb/)

#### FCHECK

FCHECK 主页：[http://sites.netscape.net/fcheck/fcheck.html](http://sites.netscape.net/fcheck/fcheck.html)

#### Sentinel

Sentinel 主页：[http://zurk.netpedia.net/zfile.html](http://zurk.netpedia.net/zfile.html)

# 第 13 章 安全软件（管理与限制）

## 本章内容

- Linux GnuPG
  - 命令
- 在 Linux 系统上设置配额
  - 修改 `"/etc/fstab"` 文件
  - 构建支持配额的内核
  - 创建 `"quota.user"` 和 `"quota.group"` 文件
  - 为用户和组分配配额
  - 命令

## Linux GnuPG

### 概述

数据源加密是一项无价的特性，为我们的工作提供了高度的保密性。像 GnuPG 这样的工具不仅仅用于邮件加密。它可以用于各种数据加密，其用途仅受想象力的限制。GnuPG RPM 包已预装在您的计算机上，但此版本不是最新的，建议安装适合我们服务器和 CPU 架构的最新版本。

根据官方 GnuPG README 文件：

GnuPG 是 GNU 用于安全通信和数据存储的工具。它可用于加密数据和创建数字签名。它包含先进的密钥管理功能，并符合 RFC2440 中描述的建议 OpenPGP Internet 标准。

由于 GnuPG 不使用任何专利算法，因此无法与 PGP2 版本兼容。PGP 2.x 仅使用 IDEA（已在全世界获得专利）和 RSA（在美国获得专利，直到 2000 年 9 月 20 日）。

### 这些安装说明假定

- 命令与 Unix 兼容。
- 源路径为 `"/var/tmp"`（其他路径也可）。
- 安装在 Red Hat Linux 6.1 和 6.2 上进行测试。
- 安装中的所有步骤都将以超级用户账户 `"root"` 执行。
- GnuPG 版本号为 `1.0.1`。

### 软件包

GnuPG 主页：http://www.gnupg.org/

您必须确保下载：`gnupg-1.0.1.tar.gz`

### Tarballs

在安装之前列出系统上的文件，安装之后再列出一份，然后使用 `diff` 比较它们以找出文件放置的位置，这是一个好主意。只需在安装前运行 `find / * > GnuPG1`，安装后运行 `find / * > GnuPG2`，然后使用 `diff GnuPG1 GnuPG2 > GnuPG-Installed` 获取更改内容的列表。

## 编译

解压 tarball（tar.gz）。

```shell
[root@deep /]# cp gnupg-version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf gnupg-version.tar.gz
```

## 编译与优化

进入新的 GnuPG 目录，在终端中输入以下内容：

```shell
CC="egcs" \
CFLAGS="-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
./configure \
--prefix=/usr \
--enable-shared
```

```shell
[root@deep gnupg-1.0.1]# make
[root@deep gnupg-1.0.1]# make check
[root@deep gnupg-1.0.1]# make install
[root@deep gnupg-1.0.1]# strip /usr/bin/gpg
```

`"make"` 命令将所有源文件编译成可执行二进制文件，`"make check"` 会运行软件包自带的自检程序，最后，`"make install"` 命令将二进制文件和所有支持文件安装到相应位置。`"strip"` 命令会减小 `"gpg"` 二进制文件的大小以获得更好的性能。

## 工作后清理

```shell
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf gnupg-version/ gnupg-version.tar.gz
```

上面使用的 `"rm"` 命令会删除我们用于编译和安装 GnuPG 的所有源文件，同时也会从 `"/var/tmp"` 目录中删除 GnuPG 的压缩归档文件。

## 命令

下面列出的命令是我们经常使用的，但还有更多命令存在。请查看 man 手册页获取更多详细信息和信息。

### 创建密钥

首先，如果这是首次使用 GnuPG 软件，我们必须创建一个新的密钥对（公钥和私钥），以便能够使用其加密功能。

#### 步骤 1

- 要创建一个新的密钥对，请使用以下命令：

```text
[root@deep /]# gpg --gen-key

gpg (GnuPG) 1.0.1; Copyright (C) 1999 Free Software Foundation, Inc.

This program comes with ABSOLUTELY NO WARRANTY.

This is free software, and you are welcome to redistribute it

under certain conditions. See the file COPYING for details.

gpg: /root/.gnupg: directory created

gpg: /root/.gnupg/options: new options file created

gpg: you have to start GnuPG again, so it can read the new options file

This asks some questions and then starts key generation.
```

#### 步骤 2

- 我们再次使用以下命令启动 GnuPG：

```text
[root@deep /]# gpg --gen-key

gpg (GnuPG) 1.0.1; Copyright (C) 1999 Free Software Foundation, Inc.

This program comes with ABSOLUTELY NO WARRANTY.

This is free software, and you are welcome to redistribute it

under certain conditions. See the file COPYING for details.

gpg: /root/.gnupg/secring.gpg: keyring created

gpg: /root/.gnupg/pubring.gpg: keyring created

Please select what kind of key you want:

   (1) DSA and ElGamal (default)

   (2) DSA (sign only)

   (4) ElGamal (sign and encrypt)

Your selection? 1

DSA keypair will have 1024 bits.

About to generate a new ELG-E keypair.
```

```text
minimum keysize is 768 bits

default keysize is 1024 bits

highest suggested keysize is 2048 bits

What keysize do you want? (1024) 2048

Do怎么说？您真的需要这么大的密钥尺寸吗？y

请求的密钥尺寸为 2048 位

请指定密钥的有效期。

    0 = 密钥永不过期

    <n>  = 密钥在 n 天后过期

    <n>w = 密钥在 n 周后过期

    <n>m = 密钥在 n 个月后过期

    <n>y = 密钥在 n 年后过期

密钥的有效期是？(0) 0

正确吗 (y/n)？y
```



您需要一个用户标识（`User-ID`）来识别您的密钥；该软件按照以下形式从真实姓名、注释和电子邮件地址构建用户标识：

```
"Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>"
```

`Real name`: Gerhard Mourani

`Email address`: gmourani@videotron.ca

`Comment`: [按回车键]

您选择了以下 `USER-ID`：

```
"Gerhard Mourani <gmourani@videotron.ca>"
```

更改 (`N`)ame（姓名）、(`C`)omment（注释）、(`E`)mail（电子邮件）或 (`O`)kay/(`Q`)uit（确认/退出）？`o`

您需要一个密码短语（`Passphrase`）来保护您的私钥。

```
我们需要生成大量随机字节。在生成质数期间执行一些其他操作（在键盘上打字、移动鼠标、使用磁盘）是个好主意；这可以让随机数生成器有更好的机会获得足够的熵。
```

```
+++++.++++++++++++++++..+++++.+++++++++++++++ ++++++++

+++.++++++++++++++++++++++++++++.++++++++++++..++++++++++++++.++++

+

..++++>++++++..+++++++++++++>+++++......>+++++......<+++++...............

..........+++++^^^^
```

公钥和私钥已创建并签名。

```
一个新的密钥对（私钥和公钥）已在 "root" 主目录（~/root）中创建。
```

### 导入密钥

一旦我们自己的密钥对创建完成，我们就可以开始将所有来自可信任第三方的密钥放入我们的公钥环数据库中，以便能够在将来的加密和认证通信中使用他/她的密钥。

- 要将公钥导入到您的密钥环，请使用以下命令：

```
[root@deep /]# gpg --import <file>
```

例如：

```
[root@deep /]# gpg --import redhat2.asc

gpg: key DB42A60E: public key imported

gpg: /root/.gnupg/trustdb.gpg: trustdb created

gpg: Total number processed: 1

gpg:              imported: 1
```

上面的命令会将所有新密钥追加到我们的密钥环数据库中，并更新所有已存在的密钥。需要注意的是，`GnuPG` 不会导入未自签名的密钥。在上面的示例中，我们从 Red Hat Linux 公司导入公钥文件 `redhat2.asc`，该文件可从 Red Hat 网站下载，导入到我们的密钥环中。

### 密钥签名

当您将密钥导入到您的公钥环数据库中，并确信可信任的第三方确实是他们声称的那个人时，您可以开始为他/她的密钥签名。对密钥签名证明您认识该密钥的所有者。

- 要为我们在上面添加到密钥环中的 RedHat 公司签名密钥，请使用以下命令：

```
[root@deep /]# gpg --sign-key <UID>
```

例如：

```
[root@deep /]# gpg --sign-key RedHat
```

```
pub  1024D/DB42A60E  created: 1999-09-23 expires: never    trust: -/q

sub  2048g/961630A2  created: 1999-09-23 expires: never

(1) Red Hat, Inc <security@redhat.com>

pub  1024D/DB42A60E  created: 1999-09-23 expires: never    trust: -/q

     Fingerprint: CA20 8686 2BD6 9DFC 65F6  ECC4 2191 80CD DB42 A60E

   Red Hat, Inc <security@redhat.com>

Are you really sure that you want to sign this key

with your key: "Gerhard Mourani <gmourani@videotron.ca>"

Really sign? y

You need a passphrase to unlock the secret key for

user: "Gerhard Mourani <gmourani@videotron.ca>"

1024-bit DSA key, ID E92D6C97, created 1999-12-30

Enter passphrase:
```

**注意**：只有当您**绝对确定**密钥确实真实可信时，才应该将其签名为真实！您绝不应该基于任何假设来签名密钥。

### 加密和解密

在安装、导入、签名和配置完所有我们想要的设置后，我们可以开始加密和解密我们的工作了。

- 要为我们在上面添加到密钥环中的 RedHat 用户加密和签名数据，请使用以下命令：

```
[root@deep /]# gpg -sear RedHat <file>
```

例如：

```
[root@deep /]# gpg -sear RedHat message-to-RedHat.txt

You need a passphrase to unlock the secret key for

user: "Gerhard Mourani (Open Network Architecture) <gmourani@videotron.ca>"

1024-bit DSA key, ID BBB4BA9B, created 1999-10-26

Enter passphrase:
```

在传递的参数中，`s` 用于签名（为避免其他人冒充您的风险，对您加密的所有内容进行签名非常有用），`e` 用于加密，`a` 用于创建 ASCII 装甲输出（`.asc` 格式，可直接通过邮件发送），`r` 用于指定要加密的用户标识名，`<file>` 是您要加密的消息。

- 要解密数据，请使用以下命令：

```
[root@deep /]# gpg -d <file>
```

例如：

```
[root@deep /]# gpg -d message-to-Gerhard.asc
```

```
You need a passphrase to unlock the secret key for
user: "Gerhard Mourani (Open Network Architecture) <gmourani@videotron.ca>"
2048-bit ELG-E key, ID 71D4CC44, created 1999-10-26 (main key ID BBB4BA9B)
Enter passphrase:
```

其中 `-d` 用于解密，`<file>` 是您要解密的消息。重要的是，我们要解密的消息发送者的公钥必须存在于我们的公钥环数据库中，否则当然什么都不会起作用。

### 导出您的公钥

您可以通过导出并在全球范围内分发您的公钥来扩展您的影响范围。这可以通过在您的首页上发布、通过互联网上的可用密钥服务器，或任何其他可用的方法来实现。`GnuPG` 有一些有用的选项可以帮助您发布公钥。

- 要以 ASCII 装甲输出格式提取您的公钥，请使用以下命令：

```
[root@deep /]# gpg --export --armor > Public-key.asc
```

其中 `--export` 用于从您的 `pubring` 加密文件中提取您的公钥，`--armor` 用于创建可以发送邮件、发布或放在网页上的 ASCII 装甲输出，`> Public-key.asc` 用于将结果放入您命名为 `Public-key.asc` 的文件中。

### 检查签名

一旦您提取并导出了您的公钥，每个知道或获得您公钥的人都应该能够检查来自您的加密数据是否确实由您签名。

- 要检查加密数据的签名，请使用以下命令：

```
[root@deep /]# gpg --verify <Data>
```

`--verify` 选项将检查签名，其中 `<Data>` 是您要验证的加密数据/文件。

### GnuPG 软件的一些可能用途

`GnuPG` 可用于：

1. 发送加密邮件消息。
2. 在网络传输前加密备份文件。
3. 加密单个敏感文件（即处理所有密码的文件）。

### 已安装的文件

```
> /usr/bin/gpg

> /usr/lib/gnupg

> /usr/lib/gnupg/rndunix
```

```
> /usr/lib/gnupg/rndegd

> /usr/lib/gnupg/tiger

> /usr/man/man1/gpg.1

> /usr/share/gnupg

> /usr/share/gnupg/options.skel
```

## 在您的 Linux 系统上设置配额

## 概述

配额是一种系统管理工具，用于监控和限制每个文件系统上用户和/或组的磁盘使用情况。磁盘存储的"配额"功能提供了两个可设置限制的特性：第一个是用户或用户组可以拥有的 `inode` 数量（文件数量），第二个是可以分配给用户或用户组的磁盘块数量（以千字节为单位的空间大小）。通过配额，系统管理员可以强制用户不在系统上无限制地占用磁盘空间。此程序以每个用户、每个文件系统为基础进行处理，必须为每个文件系统单独设置。

## 构建支持配额的内核

您需要做的第一件事是确保您的内核是在启用配额支持的情况下构建的。在 `2.2.14` 内核版本中，您需要确保对以下问题回答 **Y**：

### 文件系统

配额支持 (`CONFIG_QUOTA`) [N/y/?] **Y**

**注意：** 如果您已经按照本书中的 Linux 内核章节重新编译了内核，那么上面显示的"配额支持"选项已经设置好了。

## 修改 `/etc/fstab` 文件

`/etc/fstab` 文件包含有关安装在 Linux 服务器上的各种文件系统的信息。在使用配额之前，必须在 `fstab` 文件中启用配额。由于配额必须为每个文件系统单独设置，并且因为 `fstab` 文件中的每个文件系统都描述在单独的行上，所以必须在 `fstab` 中您希望启用配额支持的每一行上设置配额。

使用 `quota` 程序，根据您的意图、需求等，您可以仅为用户、组或同时为用户和组启用配额。在下面的所有示例中，我们将使用 `/dev/sda6` 分区上的 `/home` 目录，并向您展示三种可能性。

可能性 1：

- 要在特定文件系统上启用用户配额支持，请编辑您的 `fstab` 文件（`vi /etc/fstab`），并在 `defaults` 一词或您可能为此特定文件系统设置的任何其他选项之后的第四个字段中添加 `usrquota` 选项。

例如，将：

```
/dev/sda6     /home     ext2  defaults   1 2 （示例：单词 "defaults"）

/dev/sda6     /home     ext2  nosuid,nodev   1 2 （示例：您设置的任何其他选项）
```

更改为：

```
/dev/sda6     /home     ext2  defaults,usrquota   1 2

/dev/sda6     /home     ext2  nosuid,nodev,usrquota   1 2
```

可能性 2：

- 要在文件系统上启用组配额支持，请编辑您的 `fstab` 文件（`vi /etc/fstab`），并在 `defaults` 一词或您可能为此特定文件系统设置的任何其他选项之后的第四个字段中添加 `grpquota`。

例如，将：

```
/dev/sda6	/home	ext2	defaults	1 2 （示例：单词 "defaults"）

/dev/sda6	/home	ext2	nosuid,nodev	1 2 （示例：您设置的任何其他选项）
```

更改为：

```
/dev/sda6	/home	ext2	defaults,grpquota	1 2

/dev/sda6	/home	ext2	nosuid,nodev,grpquota	1 2
```

可能性 3：

- 要在文件系统上同时启用用户配额和组配额支持，请编辑您的 `fstab` 文件（`vi /etc/fstab`），并在 `defaults` 一词或您可能为此特定文件系统设置的任何其他选项之后的第四个字段中添加 `usrquota,grpquota`。

将：

```
/dev/sda6	/home	ext2	defaults	1 2 （示例：单词 "defaults"）

/dev/sda6	/home	ext2	nosuid,nodev	1 2 （示例：您设置的任何其他选项）
```

更改为：

```
/dev/sda6	/home	ext2	defaults,usrquota,grpquota	1 2

/dev/sda6	/home	ext2	nosuid,nodev,usrquota,grpquota	1 2
```

## 创建 `quota.user` 和 `quota.group` 文件

修改 `/etc/fstab` 文件后，为了在文件系统上建立配额，文件系统的根目录（即本例中的 `/home`）必须包含一个由 `root` 拥有的文件，如果您想使用用户配额，则该文件名为 `quota.user`；如果您想使用组配额，则名为 `quota.group`；如果两者都使用，则需要这两个文件。

步骤 1

- 要创建 `quota.user` 和/或 `quota.group` 文件，请以 `root` 身份进入您希望启用配额的分区根目录（即 `/home`），并执行以下操作创建 `quota.user` 和/或 `quota.group`：

```
[root@deep /]# touch /home/quota.user

[root@deep /]# touch /home/quota.group

[root@deep /]# chmod 600 /home/quota.user

[root@deep /]# chmod 600 /home/quota.group
```

`touch` 命令将在 `home` 目录下创建名为 `quota.user` 和 `quota.group` 的新空文件。`chmod` 命令将这些文件的模式设置为仅超级用户 `root` 可读写。

**注意**：两个配额记录文件 `quota.user` 和 `quota.group` 都应由 `root` 拥有，并且只有 `root` 有读写权限，其他人没有权限。

步骤 2

现在，我们必须在文件系统的根目录中初始化 `quota.user` 和 `quota.group` 文件，以便在服务器重启期间不会收到有关配额的错误消息。

- 要初始化 `quota.user` 和/或 `quota.group` 文件，请使用以下命令：

```
[root@deep /]# edquota -u wahib

[root@deep /]# edquota -g wahib
```

上述步骤只是为了初始化 `quota.user` 和/或 `quota.group` 文件；`edquota` 命令（`-u`）将编辑用户 `wahib` 的配额，而（`-g`）将编辑组 `wahib` 的配额。请注意，您必须编辑系统上现有的 `UID/GID` 才能成功初始化文件。

步骤 3

在您完成在 `/etc/fstab` 文件中为配额程序设置适当的选项，并创建和初始化了 `quota.users` 和/或 `quota.group` 文件之后，您必须重启系统，以使您在 `/etc/fstab` 文件和/或 `quota.user, quota.group` 文件中所做的更改生效。

- 要重启您的系统，请使用以下命令：

```
[root@deep /]# reboot
```

## 为用户和组分配配额

系统重启后，您可以为系统上的用户或用户组分配配额。此操作使用 `edquota` 命令执行。`edquota (8)`。

### edquota 程序

`edquota` 程序是一个配额编辑器，它创建一个当前磁盘配额的临时文件，供超级用户 `root` 用于为系统中的用户或用户组设置配额。下面的示例向您展示如何为系统上的用户或组设置配额。

### 为特定用户分配配额

假设您的系统上有一个登录 id 为 `wahib` 的用户。以下命令将带您进入编辑器（`vi`），以在启用配额的每个分区上编辑和设置用户 `wahib` 的配额：

步骤 1

- 要编辑和修改用户 `wahib` 的配额，请使用以下命令：

```
[root@deep /]# edquota -u wahib

Quotas for user wahib:

/dev/sda6: blocks in use: 6, limits (soft = 0, hard = 0)

inodes in use: 5, limits (soft = 0, hard = 0)
```

执行上述命令后，您将在屏幕上看到与用户 `wahib` 相关的以下行出现。**"blocks in use:"** 显示用户在分区上消耗的总块数（以千字节为单位）。**"inodes in use:"** 显示用户在分区上的总文件数。这些参数（`blocks in use` 和 `inodes in use`）由系统自动控制和设置，您无需设置或更改它们。

步骤 2

- 要为用户 `wahib` 分配 5MB 的配额，请在 `vi` 编辑器中更改以下参数：

```
Quotas for user wahib:

/dev/sda6: blocks in use: 6, limits (soft = 0, hard = 0)

    inodes in use: 5, limits (soft = 0, hard = 0)
```

更改为：

```
Quotas for user wahib:
```



`/dev/sda6`：已用块数：6，限制（软限制 = 5000，硬限制 = 0）

已用 inode 数：5，限制（软限制 = 0，硬限制 = 0）

**软限制**（`soft =`）指定了配额用户被允许拥有的最大磁盘使用量。

**硬限制**（`hard =`）指定了配额用户无法超过的磁盘使用量的绝对限制。请注意，硬限制值仅在设置了宽限期参数时才有效。

### 宽限期参数

宽限期参数允许您设置一个时间限制，然后才会在启用配额的文件系统上强制执行软限制值（有关更多信息，请参见上面的软限制）。例如，此参数可用于警告您的用户有关新策略，该策略将在 7 天内为其主目录设置 5MB 的磁盘空间配额。您可以将此参数的默认值 0 天更改为任何您认为合理的长度。

此设置的更改需要两个步骤，如下所示（在我的示例中，我假设为 7 天）。

**步骤 1**

编辑默认的宽限期参数，使用以下命令：

```
[root@deep /]# edquota -t

Time units may be: days, hours, minutes, or seconds

Grace period before enforcing soft limits for users:

/dev/sda6: block grace period: 0 days, file grace period: 0 days
```

**步骤 2**

将宽限期修改为 7 天。在 `vi` 编辑器中更改或设置以下参数：

```
Time units may be: days, hours, minutes, or seconds

Grace period before enforcing soft limits for users:

/dev/sda6: block grace period: 0 days, file grace period: 0 days
```

更改为：

```
Time units may be: days, hours, minutes, or seconds

Grace period before enforcing soft limits for users:

/dev/sda6: block grace period: 7 days, file grace period: 7 days
```

**注意**：命令 `edquota -t` 编辑每个启用配额的文件系统的软时间限制。

### 为特定组分配配额

假设您的系统上有一个组 id 为 `webusers` 的组。以下命令将带您进入 `vi` 编辑器，以在启用配额的每个分区上编辑组 `webusers` 的配额：

要编辑和修改组 `webusers` 的配额，请使用以下命令：

```
[root@deep /]# edquota -g webusers

Quotas for group webusers:

/dev/sda6: blocks in use: 6, limits (soft = 0, hard = 0)
```

inodes in use: 6, limits (soft = 0, hard = 0)

该过程与为特定用户分配配额的过程相同；如上所述，您必须修改 `soft =` 的参数并保存更改。

## 为多个用户分配相同值的组配额

`edquota` 程序有一个特殊选项（`-p`），可以将初始用户的配额值分配给一组用户。假设您要为用户 UID 从 500 开始的系统用户分配与用户 `wahib` 相同的配额值，我们首先编辑并设置 `wahib` 的配额信息，然后执行：

要为多个用户分配相同值的组配额，请使用以下命令：

```
[root@deep /]# edquota -p wahib `awk -F: '$3 > 499 {print $1}' /etc/passwd`
```

`edquota` 程序会将我们为用户 `wahib` 设置的配额复制到 `/etc/passwd` 文件中 UID 大于 499 的所有用户。

## 进一步文档

更多详细信息，您可以阅读以下几个 man 页面：

- `man edquota (8)` - 编辑用户配额
- `man quota (1)` - 显示磁盘使用情况和限制
- `man quotacheck (8)` - 扫描文件系统的磁盘使用情况
- `man quotactl (2)` - 操控磁盘配额
- `man quotaon, quotaoff (8)` - 开启和关闭文件系统配额
- `man repquota (8)` - 汇总文件系统的配额信息
- `man rquota (3)` - 在远程机器上实现配额

## 命令

下面列出的命令是我们经常使用的，但还有更多命令存在。请查看 man 页面以获取更多详细信息和信息。

## Quota

`Quota` 显示用户在文件系统上的磁盘使用情况和限制。

要显示用户的磁盘使用情况和限制，请使用命令：

```
[root@deep /]# quota -u wahib
Disk quotas for user wahib (uid 501):
    Filesystem  blocks  quota  limit  grace  files  quota  limit  grace
    /dev/sda6   6001*   6000   0      none   7      0      0
```

要显示用户所属组的组配额，请使用命令：

```
[root@deep /]# quota -g wahib
Disk quotas for group wahib (gid 501):
    Filesystem  blocks  quota  limit  grace  files  quota  limit  grace
    /dev/sda6   5995*   5000   0      none   1      0      0
```

注意：如果未为用户设置组配额，您将收到以下消息：

```
Disk quotas for group wahib (gid 501): none
```

## Repquota

`Repquota` 生成指定文件系统的磁盘使用情况和配额的汇总信息。此外，它还会为每个用户打印当前文件数量和使用的空间量（以千字节为单位）。

以下是 `repquota` 的示例输出（您的结果可能有所不同）：

```
[root@deep /]# repquota -a
```

| 用户 | 已用 | 软限制 | 硬限制 | 宽限期 | 已用 | 软限制 | 硬限制 | 宽限期 |
|------|------|--------|--------|--------|------|--------|--------|--------|
| Root | -- | 21 | 0 | 0 | 4 | 0 | 0 | |
| Named | -- | 6 | 0 | 0 | 5 | 0 | 0 | |
| Admin | -- | 388657 | 0 | 0 | 21 | 21 | 0 | 0 |
| Wahib | -- | 6001 | 0 | 0 | 7 | 0 | 0 | |

| 用户 | 已用 | 软限制 | 硬限制 | 宽限期 | 已用 | 软限制 | 硬限制 | 宽限期 |
|------|------|--------|--------|--------|------|--------|--------|--------|
| root | -- | 21 | 0 | 0 | 4 | 0 | 0 | |
| named | -- | 6 | 0 | 0 | 5 | 0 | 0 | |
| admin | -- | 388657 | 0 | 0 | 2121 | 0 | 0 | |
| wahib | -- | 6001 | 6000 | 0 | none | 7 | 0 | 0 |

# 第14章 服务器软件（BIND/DNS 网络服务）

本章内容

- Linux DNS 和 BIND 服务器配置
  - 仅缓存域名服务器
  - 主主域名服务器
  - 从属域名服务器
  - 保护 ISC BIND/DNS

# Linux DNS 和 BIND 服务器

## 概述

在我们为 Linux 服务器安装了所有必要的安全软件之后，是时候改进和优化服务器的网络部分了。DNS 是 IP 网络通信中**最**重要的网络服务，因此，所有 Linux **客户端**计算机至少应配置为执行缓存功能。为客户端本地计算机设置缓存服务器将减轻站点主服务器的负载。仅缓存域名服务器会查找域名查询的答案，并在下次需要时记住该答案。这将显著缩短下次等待时间。

出于安全原因，企业网络中的主机与外部主机之间**不应**存在 DNS；从企业网络连接到外部机器时，使用 IP 地址要安全得多，反之亦然。

在我们的配置和安装中，我们将以非 root 用户身份在 chroot 环境中运行 BIND/DNS。我们还提供三种不同的配置：一种是简单的仅缓存域名服务器（客户端），一种是从属（辅助服务器），另一种是主域名服务器（主服务器）。

简单的仅缓存域名服务器配置将用于不作为主服务器或从属服务器的服务器，而从属和主服务器配置将用于作为主域名服务器和从属域名服务器的服务器。通常，您的某个服务器作为主服务器，另一个作为从属服务器，其余的作为简单的仅缓存客户端域名服务器。

这是本书中使用的 DNS 配置的图形表示。我们尝试在不同的服务器上展示不同的设置（仅缓存 DNS、主 DNS 和从属 DNS）。存在很多可能性，具体取决于您的需求和网络架构。

## 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为 `/var/tmp`（其他路径也可以）。
- 安装在 Red Hat Linux 6.1 和 6.2 上进行了测试。
- 安装过程中的所有步骤都将以超级用户账户 `root` 执行。
- ISC BIND 版本号为 8.2.2-patchlevel5

## 软件包

ISC BIND 主页：[http://www.isc.org/](http://www.isc.org/)

ISC BIND FTP 站点：204.152.184.27

您必须确保下载：`bind-contrib.tar.gz`、`bind-doc.tar.gz`、`bind-src.tar.gz`

## Tarballs

在安装 BIND 之前，最好列出系统上的文件清单，安装后再列一个，然后使用 `diff` 比较，以找出它把文件放置到了何处。只需在安装前运行 `find /* > DNS1`，安装后运行 `find /* > DNS2`，然后使用 `diff DNS1 DNS2 > DNS-Installed` 来获取更改内容的列表。

## 编译

解压 tarball（`.tar.gz`）。

```
[root@deep /]# mkdir /var/tmp/bind
[root@deep /]# cp bind-contrib.tar.gz /var/tmp/bind/
[root@deep /]# cp bind-doc.tar.gz /var/tmp/bind/
[root@deep /]# cp bind-src.tar.gz /var/tmp/bind/
```

我们创建一个名为 `bind` 的目录来处理 tar 归档文件，并将它们复制到这个新目录。

进入新创建的 `bind` 目录（`cd /var/tmp/bind`）并解压 tar 文件：

```
[root@deep bind]# tar xzpf bind-contrib.tar.gz
[root@deep bind]# tar xzpf bind-doc.tar.gz
[root@deep bind]# tar xzpf bind-src.tar.gz
```

## 配置和优化

**步骤 1**

ISC BIND 不能以超级用户 root 身份运行；因此我们必须创建一个没有 shell 权限的特殊用户来运行 ISC BIND/DNS。

```
[root@deep /]# useradd -c "DNS Server" -u 53 -s /bin/false -r -d /chroot/named named 2>/dev/null || :
```

**步骤 2**

编辑 `Makefile.set` 文件（`vi src/port/linux/Makefile.set`）并添加或修改以下内容：

```
'CC=egcs -D_GNU_SOURCE'
'CDEBUG=-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions -g'
'DESTBIN=/usr/bin'
'DESTSBIN=/usr/sbin'
'DESTEXEC=/usr/sbin'
'DESTMAN=/usr/man'
'DESTHELP=/usr/lib'
'DESTETC=/etc'
'DESTRUN=/var/run'
'DESTLIB=/usr/lib/bind/lib'
'DESTINC=/usr/lib/bind/include'
'LEX=flex -8 -l'
'YACC=yacc -d'
'SYSLIBS=-lfl'
'INSTALL=install'
'MANDIR=man'
'MANROFF=cat'
'CATEXT=$S$N'
'PS=ps p'
'AR=ar crus'
'RANLIB=-'
```

第一行表示我们的 GCC 编译器名称（`egcs`），第二行是我们的优化标志。`DESTLIB=` 行指定了 ISC BIND 库目录的路径，`DESTINC=` 是我们放置 BIND 头文件目录的位置。

## 编译和优化

在终端上输入以下命令：

```
[root@deep bind]# make -C src
[root@deep bind]# make clean all -C src SUBDIRS=../doc/man
[root@deep bind]# make install -C src
[root@deep bind]# make install -C src SUBDIRS=../doc/man
```

`make` 命令将所有源文件编译为可执行二进制文件，然后 `make install` 将二进制文件和任何支持文件安装到适当的位置。

```
[root@deep bind]# strip /usr/bin/addr
[root@deep bind]# strip /usr/bin/dig
[root@deep bind]# strip /usr/bin/dnsquery
[root@deep bind]# strip /usr/bin/host
[root@deep bind]# strip /usr/bin/nslookup
[root@deep bind]# strip /usr/bin/nsupdate
[root@deep bind]# strip /usr/bin/mkservdb
[root@deep bind]# strip /usr/sbin/named
[root@deep bind]# strip /usr/sbin/named-xfer
[root@deep bind]# strip /usr/sbin/ndc
[root@deep bind]# strip /usr/sbin/dnskeygen
[root@deep bind]# strip /usr/sbin/irpd
[root@deep bind]# mkdir /var/named
```

`strip` 命令丢弃目标文件中的所有符号。这意味着我们的二进制文件将会更小。随后，这将稍微提高程序的性能，因为系统执行二进制文件时需要读取的行数更少了。`mkdir` 创建一个新的目录 `/var/named`。

## 工作完成后清理

```
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf bind/
```

这将删除我们用于编译和安装 ISC BIND/DNS 的所有源文件。

## 配置

不同服务的配置文件根据您的需求和网络架构而有很大差异。人们可以在家中安装仅缓存服务器，而公司可能会安装主、从属和缓存 DNS 服务器。

本书中描述的所有软件在名为 `floppy.tgz` 的 tar 压缩归档中都有特定的目录和子目录，其中包含针对特定程序的文件配置。如果您获取此归档文件，则不必手动复制粘贴或创建以下不同的配置文件。无论您决定手动复制还是从压缩归档中获取为您准备好的文件，都可以由您负责修改、根据需求调整，并将与 ISC BIND/DNS 软件相关的文件放置到服务器上的适当位置，如下所示。服务器配置文件压缩包可从以下互联网地址下载：

[http://www.openna.com/books/floppy.tgz](http://www.openna.com/books/floppy.tgz)

要运行仅缓存名称服务器，需要以下文件，并且必须创建或复制到服务器上的适当目录中。

将 `named.conf` 文件复制到 `/etc/` 目录。

将 `db.127.0.0` 文件复制到 `/var/named/` 目录。

将 `db.cache` 文件复制到 `/var/named/` 目录。

将 `named` 脚本文件复制到 `/etc/rc.d/init.d/` 目录。

要运行主名称服务器，需要以下文件，并且必须创建或复制到服务器上的适当目录中。

将 `named.conf` 文件复制到 `/etc/` 目录。

将 `db.127.0.0` 文件复制到 `/var/named/` 目录。

将 `db.cache` 文件复制到 `/var/named/` 目录。

将 `db.208.164.186` 文件复制到 `/var/named/` 目录。



将`db.openna`文件复制到`/var/named/`目录。

将`named`脚本文件复制到`/etc/rc.d/init.d/`目录。

要运行从名称服务器，需要以下文件，并且必须创建或复制到服务器上的适当目录中。

将`named.conf`文件复制到`/etc/`目录。

将`db.127.0.0`文件复制到`/var/named/`目录。

将`db.cache`文件复制到`/var/named/`目录。

将`named`脚本文件复制到`/etc/rc.d/init.d/`目录。

您可以在`floppy.tgz`压缩包中获取以下列出的配置文件。将解压后的`floppy.tgz`压缩包中的以下文件复制到适当位置，或者直接从本书中复制到相关文件中。

## 仅缓存名称服务器

仅缓存名称服务器不对任何域具有权威性，除了`0.0.127.in-addr.arpa`（本地主机）。仅缓存名称服务器可以查找您所在区域内外的名称，正如主要和从名称服务器一样。区别在于，当仅缓存名称服务器最初查找您区域内的名称时，它会向您区域的主要或从名称服务器之一询问答案。

**设置简单缓存名称服务器所需的文件有：**

- `named.conf`
- `db.127.0.0`
- `db.cache`
- `named`脚本

## 简单缓存名称服务器的`/etc/named.conf`文件配置

对您网络上不充当主或从名称服务器的所有服务器使用此配置。为本地客户端计算机设置简单的缓存服务器将减轻网络主服务器的负载。许多使用拨号连接的用户可以将此配置与`bind`一起用于此类目的。

创建`named.conf`文件（`touch /etc/named.conf`）并向文件中添加以下行：

```
options {
    directory "var/named";
    forwarders { 208.164.186.1; 208.164.186.2; };
    forward only;
};

//
// a caching only nameserver config
zone "." in {
        type hint;
        file "db.cache";
};

zone "0.0.127.in-addr.arpa" in {
        type master;
        file "db.127.0.0";
};
```

在`forwarders`行中，`208.164`进行评估。地址`208.164.186.1`仍如预期在`forwarders`中，`208.164.186.2`是您的主（主）和从（辅）DNS服务器的IP地址。它们也可以分别是您的ISP的DNS服务器和另一个DNS服务器的IP地址。

为了提高BIND/DNS服务器的安全性，您可以在转发器宕机或无响应时阻止它尝试联系场外服务器。在`named.conf`文件中设置了`forward only`选项后，如果转发器没有给出答案，名称服务器不会尝试联系其他服务器来查找信息。

## 简单缓存名称服务器的`/var/named/db.127.0.0`文件配置

对您网络上不充当主或从名称服务器的所有计算机使用此配置。`db.127.0.0`文件覆盖回环网络。在`/var/named/`中创建以下文件。

创建`db.127.0.0`文件（`touch /var/named/db.127.0.0`）并在文件中添加以下行：

```
$TTL 345600
@    IN   SOA   localhost. root.localhost. (
               00       ; Serial
               86400    ; Refresh
               7200     ; Retry
               2592000  ; Expire
               345600 ) ; Minimum
     IN   NS    localhost.

1    IN   PTR   localhost.
```

## 简单缓存名称服务器的`/var/named/db.cache`文件配置

在启动DNS服务器之前，您必须获取一份`db.cache`文件的副本，并将此文件复制到`/var/named/`目录中。`db.cache`告诉您的服务器"根"区域的服务器在哪里。

在您组织中的另一台Unix计算机上使用以下命令为您的DNS服务器查询新的`db.cache`文件，或者从您的Red Hat Linux CD-ROM源代码分发中选取一个：

- 要为您的DNS服务器查询新的`db.cache`文件，请使用以下命令：

```
[root@deep]# dig @.aroot-servers.net . ns > db.cache
```

别忘了在通过互联网检索后将`db.cache`文件复制到您安装DNS服务器的服务器上的`/var/named`目录中。

注意：出于安全原因，内部地址如`192.168.1/24`不包含在DNS配置文件中。DNS不存在于企业网络上的主机与外部主机之间，这一点非常重要。

## 主主名称服务器

区域的主主名称服务器从主机上的文件中读取区域数据，并对该区域具有权威性。

设置主主名称服务器所需的文件有：

- `named.conf`
- `db.127.0.0`
- `db.208.164.186`
- `db.openna`
- `db.cache`
- `named`脚本

## 主名称服务器的`/etc/named.conf`文件配置

对您网络上充当主名称服务器的服务器使用此配置。编译DNS后，您需要为服务器设置一个主域名。我们将使用`openna.com`作为示例域，并假设您使用的IP网络地址为`208.164.186.0`。为此，将以下行添加到您的`/etc/named.conf`。

创建`named.conf`文件（`touch /etc/named.conf`）并添加：

```
options {
    directory "/var/named";
    fetch-glue no;
    recursion no;
    allow-query { 208.164.186/24; 127.0.0/8; };
    allow-transfer { 208.164.186.2; };
    transfer-format many-answers;
};

// These files are not specific to any zone
zone "." in {
    type hint;
    file "db.cache";
};

zone "0.0.127.in-addr.arpa" in {
    type master;
    file "db.127.0.0";
};

// These are our primary zone files
zone "openna.com" in {
    type master;
    file "db.openna ";
};
```

```
zone "186.164.208.in-addr.arpa" in {
    type master;
    file "db.208.164.186";
};
```

`fetch-glue no`选项可以与`recursion no`选项一起使用，以防止服务器的缓存增长或损坏。此外，禁用递归会将您的名称服务器置于被动模式，告诉它永远不要代表其他名称服务器或解析器发送查询。非递归名称服务器非常难以欺骗，因为它不发送查询，因此不缓存任何数据。

在`allow-query`行中，`208.164.186/24`和`127.0.0/8`是允许向服务器询问普通问题的IP地址。

在`allow-transfer`行中，`208.164.186.2`是允许从服务器接收区域传输的IP地址。您必须确保只有您真正的从名称服务器才能从您的名称服务器传输区域。因为提供的信息经常被垃圾邮件发送者和IP欺骗者利用。

注意：上面`named.conf`文件中的`recursion no`、`allow-query`和`allow-transfer`选项是安全功能。

## 主和从名称服务器的`/var/named/db.127.0.0`文件配置

此配置文件可由主名称服务器和从名称服务器共同使用。`db.127.0.0`文件覆盖回环网络。在`/var/named/`中创建以下文件。

创建`db.127.0.0`文件（`touch /var/named/db.127.0.0`）并添加：

```
; Revision History: April 22, 1999 - admin@mail.openna.com
; Start of Authority (SOA) records.
$TTL 345600
@  IN SOA deep.openna.com. admin.mail.openna.com. (
                00      ; Serial
                86400   ; Refresh
                7200    ; Retry
                2592000 ; Expire
                345600 )  ; Minimum

; Name Server (NS) records.
    NS  deep.openna.com.
    NS  mail.openna.com.

; only One PTR record.
1   PTR localhost.
```

## 主名称服务器的`/var/named/db.208.164.186`文件配置

创建`db.208.164.186`文件（`touch /var/named/db.208.164.186`）并添加：

```
; Revision History: April 22, 1999 - admin@mail.openna.com
; Start of Authority (SOA) records.
$TTL 345600
@  IN SOA deep.openna.com. admin.mail.openna.com. (
```

服务器软件（BIND/DNS网络服务） | 1

第 | 4 章

```
00         ; 序列号
86400      ; 刷新时间
7200       ; 重试时间
2592000    ; 过期时间
345600 )   ; 最小 TTL

; 名称服务器（NS）记录。
    NS  deep.openna.com.
    NS  mail.openna.com.

; 反向查找的指针（PTR）记录，将地址指向规范名称
1 PTR   deep.openna.com.
2 PTR   mail.openna.com.
3 PTR   www.openna.com.
```

## 主域名服务器的`/var/named/db.openna`文件配置

将此配置用于网络中作为主域名服务器的服务器。`db.openna`文件将地址映射到主机名。在`/var/named/`中创建以下文件。

创建`db.openna`文件（`touch /var/named/db.openna`）并添加：

```
; 修订历史：1999 年 4 月 22 日 - ulse admin@mail.openna.com
; 授权起始（SOA）记录。
$TTL 345600
@  IN SOA deep.openna.com. admin.mail.openna.com. (
              00         ; 序列号
              86400      ; 刷新时间
              7200       ; 重试时间
              2592000    ; 过期时间
              345600 )   ; 最小 TTL

; 名称服务器（NS）记录。
    NS  deep.openna.com.
    NS  mail.openna.com.

; 邮件交换（MX）记录。
    MX  0 mail.openna.com.

; 地址（A）记录。
localhost        A    127.0.0.1
deep             A    208.164.186.1
mail             A    208.164.186.2
www              A    208.164.186.3

; 规范名称（CNAME）记录别名。
;www             CNAME  deep.openna.com.
```

## 主从域名服务器的`/var/named/db.cache`文件配置

在启动DNS服务器之前，您必须获取`db.cache`文件的副本，并将其复制到`/var/named/`目录中。`db.cache`文件用于告诉您的服务器"根"区域的服务器位置。

使用您组织中另一台Unix计算机上的以下命令为您的DNS服务器查询新的`db.cache`文件，或从您的Red Hat Linux CD-ROM源发行版中选取一个：

```
________________________________________________________________
```

版权所有 1999 - 2000 Gerhard Mourani，Open Network Architecture ® 和 OpenDocs Publishing

- 要为您的DNS服务器查询新的`db.cache`文件，请使用以下命令：

```
[root@deep /]# dig @.aroot-servers.net . ns > db.cache
```

不要忘记将`db.cache`文件复制到您安装DNS服务器的服务器上的`/var/named/`目录中，这是从Internet获取该文件后的操作。

## 从属（辅助）域名服务器

从属域名服务器的目的是与主服务器分担负载，或在主服务器宕机时处理全部负载。从属域名服务器通过网络从另一台域名服务器（通常是主域名服务器，但也可以从另一个从属域名服务器）加载其数据。此过程称为区域传输。

**设置从属（辅助）域名服务器所需的文件：**

- `named.conf`
- `db.127.0.0`
- `db.cache`
- `named`启动脚本

### 从属域名服务器的`/etc/named.conf`文件配置

将此配置用于网络中作为从属域名服务器的服务器。您必须在从属域名服务器主机上修改`named.conf`文件。将每个`primary`的出现改为`secondary`，除了`0.0.127.in-addr.arpa`之外，并添加一个`masters`行，其中包含主服务器的IP地址，如下所示。

创建`named.conf`文件（`touch /etc/named.conf`）并添加：

```
options {
    directory "/var/named";
    fetch-glue no;
    recursion no;
    allow-query { 208.164.186/24; 127.0/8; };
    allow-transfer { 208.164.186.1; };
    transfer-format many-answers;
};
```

```
// 这些文件不特定于任何区域
zone "." in {
    type hint;
    file "db.cacheCoe cache";
};
```

```
zone "0.0.127.in-addr.arpa" in {
    type master;
    file "db.127.0.0";
};
```

```
// 这些是我们的从属区域文件
zone "openna.com" in {
    type slave;
    file "db.openna";
    masters { 208.164.186.1; };
};
```

```
zone "186.164.208.in-addr.arpa" in {
    type slave;
    file "db.208.164.186";
    masters { 208.164.186.1; };
};
```

这告诉域名服务器它是`openna.com`区域的从属服务器，并且应该跟踪主机`208.164.186.1`上保持的该区域的版本。

从属域名服务器不需要通过网络检索其所有数据库（db）文件，因为这些db文件`db.127.0.0`和`db.cache`与主服务器上的相同，因此您可以在从属域名服务器上保留这些文件的本地副本。

将`db.127.0.0`文件从主域名服务器复制到从属域名服务器。

将`db.cache`文件从主域名服务器复制到从属域名服务器。

### 所有类型域名服务器的`/etc/rc.d/init.d/named`脚本文件配置

配置您的`/etc/rc.d/init.d/named`脚本文件，以在您的服务器上启动和停止BIND/DNS守护进程。此配置脚本文件可用于所有类型的域名服务器（缓存、主服务器或从属服务器）。

创建`named`脚本文件（`touch /etc/rc.d/init.d/named`）并添加：



```
#!/bin/sh
#
# named    此 shell 脚本负责启动和停止
#          named（BIND DNS 服务器）。
#
# chkconfig: - 55 45
# description: named（BIND）是一个域名服务器（DNS） \n# 用于将主机名解析为 IP 地址。
# probe: true

# 引入函数库。
. /etc/rc.d/init.d/functions

# 引入网络配置。
. /etc/sysconfig/network

# 检查网络是否已启动。
[ ${NETWORKING} = "no" ] && exit 0

[ -f /usr/sbin/named ] || exit 0

[ -f /etc/named.conf ] || exit 0

RETVAL=0

# 查看调用方式。
case "$1" in
  start)
    # 启动守护进程。
    echo -n "启动 named: "
    daemon named
    RETVAL=$?
    [ $RETVAL -eq 0 ] && touch /var/lock/subsys/named
    echo
    ;;
  stop)
    # 停止守护进程。
    echo -n "关闭 named: "
    killproc named
```

```
RETVAL=$?
[ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/named
echo
;;
status)
  /usr/sbin/ndc status
  exit $?
;;
restart)
  $0 stop
  $0 start
;;
reload)
  /usr/sbin/ndC reload
  exit $?
;;
probe)
  # named 知道如何智能重新加载；我们不希望 linuxconf
  # 每次都提供重新启动
  /usr/sbin/ndc reload >/dev/null 2>&1 || echo start
  exit 0
;;

*)
  echo "Usage: named {start|stop|status|restart}"
  exit 1
esac

exit $RETVAL
```

现在，使此脚本可执行并更改其默认权限：

```
[root@deep]# chmod 700 /etc/rc.d/init.d/named
```

使用以下命令创建 BIND/DNS 的符号链接 rc.d：

```
[root@deep]# chkconfig --add named
```

BIND/DNS 脚本不会在您重新启动服务器时自动启动 named 守护进程。您可以通过执行以下命令更改其默认设置：

```
[root@deep]# chkconfig --level 345 named on
```

使用以下命令手动启动您的 DNS 服务器：

```
[root@deep]# /etc/rc.d/init.d/named start
启动 named:
[ OK ]
```

## 保护 ISC BIND/DNS

### 在 chroot 监狱中运行 ISC BIND/DNS

本部分重点介绍如何防止 ISC BIND/DNS 被用作入侵其托管系统的入口点。由于 ISC BIND/DNS 执行的功能相对庞大且复杂，因此该软件存在影响安全性的漏洞的可能性相当高。事实上，过去曾存在可利用的漏洞，允许远程攻击者获取运行 ISC BIND/DNS 的主机的 root 访问权限。

为了将这种风险降至最低，ISC BIND/DNS 可以以非 root 用户身份运行，这将把任何损害限制为普通用户通过本地 shell 可以执行的操作。当然，这对于大多数 DNS 服务器的安全要求来说是不够的，因此可以采取额外的步骤——即在 chroot 监狱中运行 ISC BIND。

chroot 监狱的主要好处是，监狱将 DNS 守护进程程序可以看到的文件系统部分限制为监狱的根目录。此外，由于监狱只需要支持 DNS，因此监狱中可用的与 ISC BIND/DNS 相关的程序可以非常有限。最重要的是，不需要 setuid-root 程序，这些程序可用于获取 root 访问权限并突破监狱。

**注意：** `named` 二进制程序必须位于您的 `PATH` 环境变量中所列的目录中，这样才能正常工作。对于本文档的其余部分，我假设您的原始 `named` 程序路径为 `/usr/sbin/named`。

以下是在 chroot 监狱中运行 ISC BIND/DNS 软件的必要步骤：

**步骤 1**

我们必须找到 `named` 的共享库依赖项（`named` 是 DNS 守护进程）。这些稍后需要复制到 chroot 监狱中。

- 要查找 `named` 的共享库依赖项，请执行以下命令：

```
[root@deep /]# ldd /usr/sbin/named
  libc.so.6 => /lib/libc.so.6 (0x40017000)
  /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

记下上面列出的文件；您稍后在步骤中会需要这些。

**步骤 2**

现在我们必须设置 chroot 环境，并创建监狱的根目录。我们选择 `/chroot/named`，因为我们希望将其放在单独的文件系统上，以防止文件系统攻击。在我们的 Linux 安装过程早期，我们为此目的创建了一个特殊分区 `/chroot`。

```
[root@deep /]# /etc/rc.d/init.d/named stop （仅在现有 named 守护进程正在运行时需要）
关闭 named:                     [ OK ]
[root@deep /]# mkdir -p /chroot/named
```

接下来，按如下方式创建其余目录：

```
[root@deep /]# mkdir /chroot/named/dev
[root@deep /]# mkdir /chroot/named/lib
[root@deep /]# mkdir /chroot/named/etc
[root@deep /]# mkdir -p /chroot/named/usr/sbin
[root@deep /]# mkdir -p /chroot/named/var/run
[root@deep /]# mkdir /chroot/named/var/named
```

现在将主配置文件、区域文件、`named` 和 `named-xfer` 程序复制到 chroot jail 目录中的相应位置：

```
[root@deep /]# cp /etc/named.conf /chroot/named/etc/
[root@deep /]# cd /var/named ; cp -a . /chroot/named/var/named/
[root@deep /]# mknod /chroot/named/dev/null c 1 3
[root@deep /]# chmod 666 /chroot/named/dev/null
[root@deep /]# cp /usr/sbin/named /chroot/named/usr/sbin/
[root@deep /]# cp /usr/sbin/named-xfer /chroot/named/usr/sbin/
```

**重要提示：** `/chroot/named/var/named` 目录及其下所有文件的所有者必须是运行在从服务器上的 `named` 进程，否则将无法进行区域传输。

- 要使从服务器上 `named` 目录及其所有文件归属于 `named` 进程，请使用以下命令：

```
[root@deep /]# chown -R named.named /chroot/named/var/named/
```

## 步骤 3

将步骤 1 中识别的共享库复制到 chroot 的 `lib` 目录中：

```
[root@deep /]# cp /lib/libc.so.6 /chroot/named/lib/
[root@deep /]# cp /lib/ld-linux.so.2 /chroot/named/lib/
```

## 步骤 4

将 `localtime` 和 `nsswitch.conf` 文件复制到 chroot 的 `etc` 目录中，以便日志条目能根据本地时区正确调整：

```
[root@deep /]# cp /etc/localtime /chroot/named/etc/
[root@deep /]# cp /etc/nsswitch.conf /chroot/named/etc/
```

## 步骤 5

我们必须为更好的安全性，设置 `/chroot/named/etc` 目录下的某些文件启用不可变位（immutable bit）：

- 设置 `nsswitch.conf` 文件的不可变位：

```
[root@deep /]# cd /chroot/named/etc/
[root@deep etc]# chattr +i nsswitch.conf
```

- 设置 `named.conf` 文件的不可变位：

```
[root@deep /]# cd /chroot/named/etc/
[root@deep etc]# chattr +i named.conf
```

具有 `+i` 属性的文件无法被修改、删除或重命名；无法为其创建链接，也无法向其写入数据。只有超级用户可以设置或清除此属性。

## 步骤 6

为运行 `named` 守护进程添加新的 UID 和 GID（如果尚未设置）。这很重要，因为以 root 身份运行会破坏 jail 的目的，而使用系统上已存在的其他用户 ID 可能导致服务之间相互访问资源。

检查 `/etc/passwd` 和 `/etc/group` 文件以获取可用的空闲 UID/GID 号码。在我们的示例中，我们将使用号码 `53` 和名称 `named`。

```
[root@deep /]# useradd -c "DNS Server" -u 53 -s /bin/false -r -d /chroot/named named 2>/dev/null || :
```

## 步骤 7

我们必须告知 `syslogd`（syslog 守护进程程序）关于新的 chroot 服务：

通常，进程通过 `/dev/log` 与 `syslogd` 通信。由于 chroot jail 的存在，这将不再可行，因此需要告知 `syslogd` 监听 `/chroot/named/dev/log` 而非默认的 `/dev/log`。为此，请编辑 syslog 启动脚本文件以指定额外的监听位置。

编辑 **syslog** 脚本文件（`vi +24 /etc/rc.d/init.d/syslog`），将以下行：

```
daemon syslogd -m 0
```

修改为：

```
daemon syslogd -m 0 -a /chroot/named/dev/log
```

## 步骤 8

ISC BIND/DNS 的默认 `named` 脚本文件在 chroot jail 外启动守护进程 `named`。我们必须将其改为从 chroot jail 中启动 `named`。编辑 **named** 脚本文件（`vi /etc/rc.d/init.d/named`），将以下行：

```
[ -f /usr/sbin/named ] || exit 0
```

修改为：

```
[ -f /chroot/named/usr/sbin/named ] || exit 0
```

```
[ -f /etc/named.conf ] || exit 0
```

修改为：

```
[ -f /chroot/named/etc/named.conf ] || exit 0
```

```
daemon named
```

修改为：

```
daemon /chroot/named/usr/sbin/named -t /chroot/named/ -unamed -gnamed
```

`-t` 选项告诉 `named` 使用新的 chroot 环境启动。

`-u` 选项指定运行时使用的用户。

`-g` 选项指定运行时使用的组。

## 步骤 9

在 BIND 8.2 版本中，ISC BIND/DNS 软件的 `ndc` 命令变为二进制文件（之前是脚本文件），这使得随附的 `ndc` 在此设置中无法使用。为解决此问题，必须从源码重新编译 ISC BIND/DNS 软件包。

为此，请进入 ISC BIND/DNS 源代码目录的顶层目录。

对于 `ndc` 工具：

```
[root@deep /]# cp bind-src.tar.gz /var/tmp
[root@deep /]# cd /var/tmp/
```

```
[root@deep tmp]# tar xzpf bind-src.tar.gz
[root@deep tmp]# cd src
[root@deep src]# cp port/linux/Makefile.set port/linux/Makefile.set-orig
```

编辑 **Makefile.set** 文件（`vi port/linux/Makefile.set`），进行如下更改：

```
'CC=egcs -D_GNU_SOURCE'
'CDEBUG=-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions -g'
'DESTBIN=/usr/bin'
'DESTSBIN=/chroot/named/usr/sbin'
'DESTEXEC=/chroot/named/usr/sbin'
'DESTMAN=/usr/man'
'DESTHELP=/usr/lib'
'DESTETC=/etc'
'DESTRUN=/chroot/named/var/run'
'DESTLIB=/usr/lib/bind/lib'
'DESTINC=/usr/lib/bind/include'
'LEX=flex -8 -l'
'YACC=yacc -d'
'SYSLIBS=-lfl'
'INSTALL=install'
'MANDIR=man'
'MANROFF=cat'
'CATEXT=$$$N'
'PS=ps p'
'AR=ar crus'
'RANLIB=:'
```

与我们之前使用的 Makefile 的区别在于，我们修改了 `DESTSBIN=`、`DESTEXEC=` 和 `DESTRUN=` 行，使其指向 BIND/DNS 的 chroot 目录。通过此修改，`ndc` 程序知道在哪里找到 `named`。

```
[root@deep src]# make clean
[root@deep src]# make
[root@deep src]# cp bin/ndc/ndc /usr/sbin/
[root@deep src]# cp: overwrite `/usr/sbin/ndc'? y
[root@deep src]# strip /usr/sbin/ndc
```

我们构建二进制文件，然后将 `ndc` 程序的结果复制到 `/usr/sbin` 并覆盖旧版本。别忘了对新的 `ndc` 二进制文件执行 `strip` 命令以提高性能。

## 步骤 10

现在也是构建新的 `named` 和 `named-xfer` 二进制文件的好时机，以确保 `named` 和 `ndc` 使用相同的版本。

对于 `named` 程序：

```
[root@deep /]# cd /var/tmp/src
[root@deep src]# cp port/linux/Makefile.set-orig port/linux/Makefile.set
[root@deep src]# cp: overwrite `port/linux/Makefile.set'? y
```

编辑 **Makefile.set** 文件（`vi port/linux/Makefile.set`），进行如下更改：

```
'CC=egcs -D_GNU_SOURCE'
'CDEBUG=-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions -g'
'DESTBIN=/usr/bin'
'DESTSBIN=/usr/sbin'
'DESTEXEC=/usr/sbin'
```

```
'DESTMAN=/usr/man'
'DESTHELP=/usr/lib'
'DESTETC=/etc'
'DESTRUN=/var/run'
'DESTLIB=/usr/lib/bind/lib'
'DESTINC=/usr/lib/bind/include'
'LEX=flex -8 -l'
'YACC=yacc -d'
'SYSLIBS=-lfl'
'INSTALL=install'
'MANDIR=man'
'MANROFF=cat'
'CATEXT=$$N'
'PS=ps p'
'AR=ar crus'
'RANLIB=:'
```



```text
[root@deep src]# rm -f .settings
[root@deep src]# make clean
[root@deep src]# make
[root@deep src]# cp bin/named/named /chroot/named/usr/sbin
[root@deep src]# cp: overwrite `/chroot/named/usr/sbin/named'? y
[root@deep src]# cp bin/named-xfer/named-xfer /chroot/named/usr/sbin
[root@deep src]# cp: overwrite `/chroot/named/usr/sbin/named-xfer'? y
[root@deep src]# strip /chroot/named/usr/sbin/named
[root@deep src]# strip /chroot/named/usr/sbin/named-xfer
```

我们删除`.settings`文件，因为构建系统会缓存这些变量，并运行`make clean`命令以确保没有残留的垃圾文件。之后我们构建`named`二进制文件，并将其连同`named-xfer`一起复制到`chroot jail`目录中。同时，我们使用`strip`命令来提高新二进制文件的性能。

## 步骤 11

删除不必要的文件和目录。

```text
[root@deep /]# rm -f /usr/sbin/named
[root@deep /]# rm -f /usr/sbin/named-xfer
[root@deep /]# rm -f /etc/named.conf
[root@deep /]# rm -rf /var/named/
```

我们从`/usr/sbin`目录中删除`named`和`named-xfer`二进制文件，因为我们今后日常使用的版本位于`chroot`目录下。同样，`named.conf`文件和`/var/named`目录也需要删除。

## 步骤 12

我们必须测试 ISC BIND/DNS 软件的新`chroot jail`配置。

- 首先使用以下命令重启`syslogd`守护进程：

```text
[root@deep /]# /etc/rc.d/init.d/syslog restart
Shutting down kernel logger:           [ OK ]
Shutting down system logger:             [ OK ]
Starting system logger:                  [ OK ]
Starting kernel logger:                  [ OK ]
```

- 现在使用以下命令启动新的`chroot jail` ISC BIND/DNS：

```text
[root@deep /]# /etc/rc.d/init.d/named start
Starting named:                          [ OK ]
```

确保它以用户`named`身份运行，并带有新的参数。

- 要验证 ISC BIND/DNS 是否以用户`named`身份运行并带有新的参数，请使用以下命令：

```text
[root@deep /]# ps auxw | grep named
```

```text
named 11446 0.0 1.2 2444 1580 ? S 23:09 0:00 /chroot/named/usr/sbin/named -t /chroot/named/ - unnamed -gnamed
```

第一列应该是`named`，即 named 守护进程运行时所使用的 UID。行尾应该是`named -t /chroot/named/ -unnamed -gnamed`，这些是它的新参数。

## 清理工作

```text
[root@deep /]# rm -rf /var/tmp/src bind-src.tar.gz
```

这将删除我们用于编译和安装 ISC BIND/DNS 的源文件和 tar 压缩包。

## 进一步文档

更多详情，可以阅读以下多个 man 手册页：

| 命令 | 描述 |
| --- | --- |
| `$ man dnsdomainname (1)` | - 显示系统的 DNS 域名 |
| `$ man dnskeygen (1)` | - 生成用于 DNS 安全的公钥、私钥和共享密钥 |
| `$ man dnsquery (1)` | - 使用解析器查询域名服务器 |
| `$ man named (8)` | - 互联网域名服务器 (DNS) |
| `$ man hesiod_to_bind [hesiod] (3)` | - Hesiod 名称服务器接口库 |
| `$ man ldconfig (8)` | - 确定运行时链接绑定 |
| `$ man lesskey (1)` | - 指定 less 的键绑定 |
| `$ man raw (8)` | - 绑定 Linux 原始字符设备 |
| `$ man mkfifo (1)` | - 创建 FIFO（命名管道） |
| `$ man named-bootconf (8)` | - 转换名称服务器配置文件 |
| `$ man named-xfer (8)` | - 入站区域传输的辅助代理 |
| `$ man named.conf [named] (5)` | - name 的配置文件 |
| `$ man Opcode (3)` | - 编译 perl 代码时禁用指定操作码 |
| `$ man dig (1)` | - 向名称服务器发送域名查询包 |
| `$ man nslookup (8)` | - 交互式查询互联网名称服务器 |
| `$ man ndc (8)` | - 名称守护进程控制程序 |

## DNS 管理员工具

下面列出的命令是我们经常使用的部分命令，但还有更多。请参阅 man 手册页和文档以获取更多详情和信息。

### `dig`

`dig`命令工具（domain information groper，域信息搜索器）可用于更新你的`db.cache`文件，方法是告诉你的服务器`root`区域的服务器在哪里。当服务器知道这些区域的位置后，它会从中查询新的`db.cache`。根名称服务器不经常变化，但确实会发生变化。一个好的做法是每一到两个月更新一次你的`db.cache`文件。

- 使用以下命令为你的 DNS 服务器查询新的`db.cache`文件：

```text
[root@deep /]# dig @.aroot-servers.net . ns > db.cache
```

获取后，将`db.cache`文件复制到`/var/named/`。

```text
[root@deep /]# cp db.cache /var/named/
```

其中`@.a.root-servers.net`是用于查询新`db.cache`文件的根服务器地址，`db.cache`文件是你的新 db.cache 文件的名称。

## `ndc`

ISC BIND/DNS 的`ndc`命令工具允许系统管理员通过终端交互式地控制名称服务器的操作。

- 在你的终端上输入`ndc`，然后输入`help`以查看不同命令的帮助。

```text
[root@deep /]# ndc

Type help -or- /h if you need help.

ndc> help

getpid

status

stop

exec

reload [zone] ...

reconfig (just sees new/gone zones)

dumpdb

stats

trace [level]

notrace

querylog

qrylog

help

quit

ndc> /e
```

## DNS 用户工具

下面列出的命令是我们经常使用的部分命令，但还有更多。请参阅 man 手册页和文档以获取更多详情和信息。

## `nslookup`

`nslookup`程序允许用户以交互式或非交互式方式查询互联网域名服务器。在交互模式下，用户可以查询名称服务器以获取有关各种主机和域的信息，并打印域中的主机列表。在非交互模式下，用户只能打印名称并请求主机或域的信息。

交互模式有很多选项和命令；建议查阅`nslookup`的 man 手册页，或在`nslookup`交互模式下查看帮助。

- 要进入`nslookup`交互模式，请使用命令：

```text
[root@deep /]# nslookup

Default Server: deep.openna.com

Address: 208.164.186.1

> help

$Id: nslookup.help,v 8.4 1996/10/25 18:09:41 vixie Exp $

Commands: (identifiers are shown in uppercase, [] means optional)

NAME - print info about the host/domain NAME using default server

NAME1 NAME2 - as above, but use NAME2 as server

help or ? - print info on common commands; see nslookup(1) for details

set OPTION - set an option

all - print options, current server and host

[no]debug - print debugging information

[no]d2 - print exhaustive debugging information
```

- 要以非交互模式运行，请使用命令：

```text
[root@deep /]# nslookup www.redhat.com

Server: deep.openna.com

Address: 208.164.186.1

Non-authoritative answer:

Name: www.portal.redhat.com

Addresses: 206.132.41.202, 206.132.41.203

Aliases: www.redhat.com
```

其中`www.redhat.com`是要查询的名称服务器的域名或互联网地址。

## `dnsquery`

`dnsquery`程序通过解析器库调用`/etc/resolv.conf`来查询域名服务器。

- 要使用解析器查询域名服务器，请使用命令：

```text
[root@deep /]# dnsquery <host>
```

例如：

```text
[root@deep /]# dnsquery www.redhat.com

;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 40803

;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 4, ADDITIONAL: 4

;; www.redhat.com, type = ANY, class = IN

www.redhat.com. 2h19m46s IN CNAME www.portal.redhat.com.

redhat.com. 2h18m13s IN NS ns.redhat.com.

redhat.com. 2h18m13s IN NS ns2.redhat.com.

redhat.com. 2h18m13s IN NS ns3.redhat.com.

redhat.com. 2h18m13s IN NS speedy.redhat.com.

ns.redhat.com. 1d2h18m8s IN A 207.175.42.153

ns2.redhat.com. 1d2h18m8s IN A 208.178.165.229

ns3.redhat.com. 1d2h18m8s IN A 206.132.41.213

speedy.redhat.com. 1d2h18m8s IN A 199.183.24.251
```

其中`<host>`是你要查询的主机名。

## `host`

`host`程序使用 DNS 查找主机名。

- 要使用域名服务器查找主机名，请使用命令：

```text
[root@deep /]# host <FQDN, domain names, host names, or host numbers>
```

例如：

```text
[root@deep /]# host redhat.com

redhat.com has address 207.175.42.154
```

其中`<FQDN, domain names, host names, or host numbers>`可以是 FQDN（`www.redhat.com`）、域名（`redhat.com`）、主机名（`www`）或主机号（`207.175.42.154`）。

- 要查找 DNS 维护的关于主机的所有信息，请使用命令：

```text
[root@deep /]# host <-a domain names >
```

例如：

```text
[root@deep /]# host -a redhat.com

Trying null domain

rcode = 0 (Success), acount=6

The following answer is not authoritative:

The following answer is not verified as authentic by the server:

redhat.com 8112 IN NS ns.redhat.com

redhat.com 8112 IN NS ns2.redhat.com

redhat.com 8112 IN NS ns3.redhat.com

redhat.com 8112 IN NS speedy.redhat.com

redhat.com 8112 IN A 207.175.42.154

redhat.com 11891 IN SOA ns.redhat.com noc.redhat.com(

			2000021402	;serial (version)

			3600		;refresh period

			1800		;retry refresh this often

			604800		;expiration period

			86400		;minimum TTL

			)
```

有关权威答案，请参阅：

```text
redhat.com	8112 IN NS	ns.redhat.com
redhat.com	8112 IN NS	ns2.redhat.com
redhat.com	8112 IN NS	ns3.redhat.com
redhat.com	8112 IN NS	speedy.redhat.com
Additional information:
ns.redhat.com	94507	IN	A	207.175.42.153
ns2.redhat.com	94507	IN	A	208.178.165.229
ns3.redhat.com	94507	IN	A	206.132.41.213
speedy.redhat.com	8112 IN	A	199.183.24.251
```

此选项可用于查找域名服务器维护的关于该主机的所有信息，在我们的示例中是`redhat.com`。

- 要列出完整的域，请使用命令：

```text
[root@deep /]# host <-l domain names >
```

例如：

```text
[root@deep /]# host -l openna.com

openna.com name server deep.openna.com

openna.com name server mail.openna.com

localhost.openna.com has address 127.0.0.1

deep.openna.com has address 208.164.186.1

mail.openna.com has address 208.164.186.2

www.openna.com has address 208.164.186.3
```

此选项将以官方主文件格式提供`openna.com`域名的完整区域数据下载。只有在绝对必要时才应使用此命令。

## 已安装的文件

```text
> /etc/rc.d/init.d/named
> /etc/rc.d/rc0.d/K45named
> /etc/rc.d/rc1.d/K45named
> /etc/rc.d/rc2.d/K45named
> /etc/rc.d/rc3.d/K45named
> /etc/rc.d/rc4.d/K45named
> /etc/rc.d/rc5.d/K45named
> /etc/rc.d/rc6.d/K45named
> /etc/named.conf
> /usr/bin/addr
> /usr/bin/nslookup
> /usr/bin/dig
> /usr/bin/dnsquery
> /usr/bin/host
> /usr/bin/nsupdate
> /usr/bin/mkservdb
> /usr/lib/bind
```



```text
> /usr/lib/bind/include/hesiod.h
> /usr/lib/bind/include/sys
> /usr/lib/bind/include/net
> /usr/lib/bind/lib
> /usr/lib/bind/lib/libbind.a
> /usr/lib/bind/lib/libbind_r.a
> /usr/lib/nslookup.help
> /usr/man/man1/dig.1
> /usr/man/man1/host.1
> /usr/man/man1/dnsquery.1
> /usr/man/man1/dnskeygen.1
> /usr/man/man3/hesiod.3
> /usr/man/man3/gethostbyname.3
> /usr/man/man3/inet_cidr.3
> /usr/man/man3/resolver.3
> /usr/man/man3/getnetent.3
> /usr/man/man3/tsig.3
```

## Server Software（BIND/DNS Network Services）

# 第 15 章 服务器软件（邮件网络服务）

## 本章内容

- Linux Sendmail 服务器
  - 配置
  - 保护 Sendmail 安全
  - Sendmail 管理工具
  - Sendmail 用户工具
- Linux IMAP & POP 服务器
  - 配置
  - 保护 IMAP/POP 安全

## Linux Sendmail 服务器

### 概述

Sendmail 程序是全球使用最广泛的互联网邮件传输代理（`MTA`）之一。MTA 的目的是将邮件从一台机器发送到另一台机器，仅此而已。Sendmail 并不是一个用来阅读电子邮件的客户端程序。相反，它实际上是将你的电子邮件通过网络或互联网传输到你想要送达的地方。过去，Sendmail 很容易被系统入侵者利用，但随着 Sendmail 8 版本的出现，这种情况已经变得困难得多。

在我们的配置和安装中，我们将为你提供两种不同的 Sendmail 配置：一种是用于**中央邮件中继枢纽**，另一种用于本地或邻近的客户端和服务器。

**中央邮件中继枢纽服务器**配置将用于你的服务器，其分配的任务是发送、接收和转发你网络中所有本地或邻近客户端和服务器邮件机器的全部邮件。本地或邻近客户端和服务器是指你网络中运行 Sendmail 并将所有外发邮件发送到中央邮件枢纽以待后续投递的所有其他本地服务器或客户端机器。这种内部客户端从不直接通过互联网接收邮件；相反，从这些计算机发往互联网的邮件都保存在邮件枢纽服务器上。为你的网络中的所有计算机运行一个中央邮件枢纽服务器是个好主意；这种架构将限制服务器和客户端机器上的任务管理，并提高你站点的安全性。

你可以将邻近的 Sendmail 配置为仅接受本地生成的邮件，从而使邻近机器的防护更加简单。网关服务器（防火墙外部或其组成部分）充当代理，接受来自外部的、destined for 内部投递的外部邮件（通过其防火墙规则文件），并将其转发到中央邮件枢纽服务器。另请注意，网关服务器的配置类似于邻近 Sendmail 服务器，从不接受来自外部（互联网）的传入邮件。

这是我们在本书中使用的 Sendmail 配置的图示。我们尝试向你展示不同服务器上的不同设置（中央邮件中继枢纽，以及本地或邻近客户端和服务器）。存在许多可能性，取决于你的需求和网络架构。

### 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为`/var/tmp`（其他路径也可行）。
- 安装在 Red Hat Linux 6.1 和 6.2 上进行了测试。
- 安装中的所有步骤都将使用超级用户账户`root`执行。
- Sendmail 版本号为`8.10.1`。

### 软件包

Sendmail 主页：http://www.sendmail.org/

Sendmail FTP 站点：`204.152.184.34`

你必须确保下载：`sendmail.8.10.1.tar.gz`

### Tarball 压缩包

在安装 Sendmail 之前，最好列出系统上的文件清单，安装后再列出一份，然后使用`diff`进行比较，找出软件安装的位置。只需在安装前运行`find / * > Sendmail1`，安装后运行`find / * > Sendmail2`，然后使用`diff Sendmail1 Sendmail2 > Sendmail-Installed`来获取更改内容的列表。

### 编译

解压 tarball 压缩包（tar.gz）。

```bash
[root@deep /]# cp sendmail.version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf sendmail.version.tar.gz
```

### 配置

进入新的 Send 目录并执行以下步骤。

#### 步骤 1

编辑`smrsh.c`文件（`vi +77 smrsh/smrsh.c`）并更改以下行：

```c
# define CMDDIR   "/usr/adm/sm.bin"
```

改为：

```c
# define CMDDIR   "/etc/smrsh"
```

此修改指定了`smrsh`程序运行命令的默认搜索路径。这使我们能够限制这些程序可能存放的位置。

### 编译和优化

#### 步骤 1

Sendmail 的 Build 脚本默认使用与操作系统类型对应的站点配置文件来获取系统安装定义和各种编译值的信息。该文件位于名为`devtools/OS`的子目录下，如果你运行的是 Linux 系统，它将被命名为`Linux`。我们将重建这个站点配置文件以适应我们的 Linux 系统安装，并将其放在 Sendmail 源代码发布版的默认`devtools/OS`子目录中，因为 Build 脚本在编译 Sendmail 时会在此目录中查找默认的站点配置文件。

进入新的 Sendmail 目录，编辑 Linux 文件（`vi devtools/OS/Linux`），删除所有预定义行，然后在文件中添加以下行：

```m4
define(`confENVDEF', `-DPICKY_QF_NAME_CHECK -DXDEBUG=0')
define(`confCC', `egcs')
define(`confOPTIMIZE', `-O9 -funroll-loops -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions')
define(`confLIBS', `-lnsl')
define(`confLDOPTS', `-s')
define(`confMANROOT', `/usr/man/man')
define(`confMANOWN', `root')
define(`confMANGRP', `root')
define(`confMANMODE', `644')
define(`confMAN1SRC', `1')
define(`confMAN5SRC', `5 knights')
define(`confMAN8SRC', `8')
define(`confDEPEND_TYPE', `CC-M')
define(`confNO_HELPFILE_INSTALL')
define(`confSBINGRP', `root')
define(`confSBINMODE', `6755')
define(`confUBINOWN', `root')
define(`confUBINGRP', `root')
define(`confEBINDIR', `/usr/sbin')
```

### 这告诉 Linux 文件为以下特定配置进行设置

`define(`confENVDEF', `-DPICKY_QF_NAME_CHECK -DXDEBUG=0')`

此宏选项主要用于指定应特别包含或排除的代码。定义了`-DPICKY_QF_NAME_CHECK`后，如果`qf`文件名格式不正确，Sendmail 将记录错误并将`qf`文件重命名为`Qf`文件。`-DXDEBUG=0`参数禁用了编译期间额外的内部检查步骤。

`define(`confCC', `egcs')`

此宏选项定义了用于编译 Sendmail 的 C 编译器。在我们的例子中，我们使用`egcs` C 编译器以获得更好的优化效果。

`define(`confOPTIMIZE', `-O9 -funroll-loops -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions')`

此宏选项定义了传递给 CC 的与特定 CPU 架构相关的优化标志。

`define(`confLIBS', `-lnsl')`

此宏选项定义了传递给 ld 的`-l`标志。

`define(`confLDOPTS', `-s')`

此宏选项定义了传递给 ld 的链接器选项。

`define(`confMANROOT', `/usr/man/man')`

此宏选项定义了安装 Sendmail 手册页的位置。

`define(`confMANOWN', `root')`

此宏选项定义了所有已安装 Sendmail 手册页的所有者。

`define(`confMANGRP', `root')`

此宏选项定义了所有已安装 Sendmail 手册页的组。

`define(`confMANMODE', `644')`

此宏选项定义了所有已安装 Sendmail 手册页的权限模式。

`define(`confMAN1SRC', `1')`

此宏选项定义了安装在`confMAN1`中的手册页来源。

`define(`confMAN5SRC', `5')`

该宏选项定义安装在`confMAN5`中的 man 手册页的源码。

`define(`confMAN8SRC', `8')`

该宏选项定义安装在`confMAN8`中的 man 手册页的源码。

`define(`confDEPEND_TYPE', `CC-M')`

该宏选项指定如何使用 Sendmail 构建依赖关系。

`define(`confNO_HELPFILE_INSTALL')`

该宏选项指定默认不安装 Sendmail 帮助文件。一些经验丰富的管理员为了获得更好的安全性而推荐此项设置。

`define(`confSBINGRP', `root')`

该宏选项定义所有 Sendmail setuid 二进制文件的组。

`define(`confSBINMODE', `6755')`

该宏选项定义所有 Sendmail setuid 二进制文件的权限模式。

`define(`confUBINOWN', `root')`

该宏选项定义 Sendmail 二进制文件的所有者。

`define(`confUBINGRP', `root')`

该宏选项定义 Sendmail 二进制文件的组。

`define(`confEBINDIR', `/usr/sbin')`

该宏选项定义从其他二进制文件调用时执行的二进制文件的安装位置。在 Red Hat Linux 上，路径必须设置为`/usr/sbin`目录。

## 第 2 步

现在必须在服务器上编译并安装 Sendmail：

```bash
[root@deep sendmail-8.10.1]# cd sendmail
[root@deep sendmail]# sh Build
[root@deep sendmail]# sh Build install
[root@deep sendmail]# cd ..
[root@deep sendmail-8.10.1]# cd mailstats
[root@deep mailstats]# sh Build install
[root@deep mailstats]# cd ..
[root@deep sendmail-8.10.1]# cd smrsh
[root@deep smrsh]# sh Build install
[root@deep smrsh]# cd ..
[root@deep sendmail-8.10.1]# cd makemap（仅邮件中心配置需要）
[root@deep makemap]# sh Build install（仅邮件中心配置需要）
[root@deep makemap]# cd ..
[root@deep sendmail-8.10.1]# cd praliases（仅邮件中心配置需要）
[root@deep praliases]# sh Build install（仅邮件中心配置需要）
[root@deep praliases]# cd ..
[root@deep sendmail-8.10.1]# ln -fs /usr/sbin/sendmail /usr/lib/sendmail
[root@deep sendmail-8.10.1]# chmod 511 /usr/sbin/smrsh
[root@deep sendmail-8.10.1]# install -d -m 755 /var/spool/mqueue
[root@deep sendmail-8.10.1]# chown root.mail /var/spool/mqueue
[root@deep sendmail-8.10.1]# mkdir /etc/smrsh
```

`sh Build`命令将构建并在系统上安装 Sendmail 之前，为 Sendmail 所需的不同二进制文件建立必要的依赖关系。

`sh Build install`命令将在系统上安装`sendmail`、`mailstats`、`makemap`、`praliases`、`smrsh`二进制文件以及相应的 man 手册页（如果使用此命令编译）。

`ln -fs`命令将为`sendmail`二进制文件创建指向`/usr/lib`目录的符号链接。这是必需的，因为某些程序希望在该目录（`/usr/lib`）中找到`sendmail`二进制文件。

`install`命令将在`/var/spool`下创建权限为 755 的`mqueue`目录。由于各种各样的原因，邮件消息可能暂时无法投递。为确保此类邮件最终能够被投递，Sendmail 将它们存储在其队列目录中，直到可以成功投递。

`chown`命令将为`mqueue`目录设置 UID `root`和 GID `mail`。

**注：**`makemap`和`praliases`程序必须仅安装在中央邮件中心服务器上。`makemap`允许您为 Sendmail 创建数据库映射，如`/etc/mail/aliases.db`或`/etc/mail/access.db`文件。`praliases`显示系统邮件别名（`/etc/mail/aliases`文件的内容）。由于最好只有一个地方（如我们的中央邮件中心）来处理和管理网络中的所有 db 文件，因此没有必要在网​​络中的其他主机上使用`makemap`和`praliases`程序来构建 db 文件。

## 配置

我们在本书中描述的所有软件都有一个特定的目录和子目录，位于名为`floppy.tgz`的 tar 压缩存档中，其中包含特定程序的文件配置。如果您获取此存档文件，将不必手动复制下面不同的配置文件，也不必剪切并粘贴它们来创建您的配置文件。无论您决定手动复制它们，还是从存档中获取为您方便制作的文件，您都有责任修改、调整您的需求，并将与 Sendmail 软件相关的文件放置在服务器上的适当位置，如下所示。要下载的服务器配置文件存档位于以下互联网地址：http://www.openna.com/books/floppy.tgz(AC71107BF30E)

- 要运行中央邮件中心服务器，需要以下文件，并且必须创建或复制到服务器上的适当目录。
  - 将`sendmail`文件复制到`/etc/sysconfig`目录。
  - 将`sendmail`脚本文件复制到`/etc/rc.d/init.d/`目录。
  - 将`local-host-names`文件复制到`/etc/mail`目录。
  - 将`access`文件复制到`/etc/mail`目录。
  - 将`aliases`文件复制到`/etc/mail`目录。
  - 在`/etc/mail`目录中创建`virtusertable`、`domaintable`、`mailertable`和`.db`文件。

- 要运行本地或邻居客户端、服务器，需要以下文件，并且必须创建或复制到服务器上的适当目录。
  - 将`sendmail`文件复制到`/etc/sysconfig`目录。
  - 将`sendmail`脚本文件复制到`/etc/rc.d/init.d/`目录。
  - 将`local-host-names`文件复制到`/etc/mail`目录。

您可以在我们的`floppy.tgz`存档中获取下面列出的配置文件。将以下文件从解压后的`floppy.tgz`存档复制到适当的位置，或直接从本书中复制并粘贴到相关文件中。

## 中央邮件中心的`/etc/sendmail.mc`文件

与其让网络中的每个单独服务器或工作站处理自己的邮件，不如让功能强大的中央服务器处理所有邮件。这样的服务器称为邮件中心。中央邮件中心的优势在于：

- 所有传入邮件都发送到邮件中心，不会直接将邮件发送到客户端机器。
- 所有来自客户端的传出邮件都发送到邮件中心，然后邮件中心将邮件转发到其最终目的地。
- 所有传出邮件似乎都来自单个服务器，外界不需要知道任何客户端的名称。
- 客户端不需要运行`sendmail`守护进程来监听邮件。



`sendmail.cf` 是 Sendmail 运行时读取的第一个文件，也是 Sendmail 最重要的文件之一。该文件中包含的许多项目包括所有其他文件的位置、Sendmail 需要的那些文件和目录的默认权限。Sendmail V8 使用 Linux 的 `m4` 宏预处理器程序来生成 Sendmail 配置文件。该宏程序将通过处理以 `.mc` 结尾的文件来生成 `/etc/mail/sendmail.cf` 配置文件。因此，我们将创建此文件（`sendmail.mc`），并在其中放入必要的宏值，以允许 `m4` 程序处理（读取）其输入并收集宏定义，然后替换这些宏及其值，并输出结果以创建我们的 `sendmail.cf` 文件。有关更多信息，请参阅 V8 Sendmail 源代码分发版中 `cf` 子目录下的 Sendmail 文档和 README 文件。

## 第 1 步

创建 `sendmail.mc` 文件（`touch /var/tmp/sendmail-version/cf/cf/sendmail.mc`）并添加以下行：

```text
define(`confDEF_USER_ID',``8:12'')dnl
OSTYPE(`linux')dnl
DOMAIN(`generic')dnl
define(`confTRY_NULL_MX_LIST',true)dnl
define(`confDONT_PROBE_INTERFACES',true)dnl
define(`PROCMAIL_MAILER_PATH',`/usr/bin/procmail')dnl
define(`LOCAL_MAILER_FLAGS',iliksPfn')dnl
define(`LOCAL_MAILER_ARGS',`procmail -a $h -d $u')dnl
FEATURE(`smrsh',`/usr/sbin/smrsh')dnl
FEATURE(`mailertable')dnl
FEATURE(`virtusertable',`hash -o /etc/mail/virtusertable')dnl
FEATURE(`redirect')dnl
FEATURE(`always_add_domain')dnl
FEATURE(`use_cw_file')dnl
FEATURE(`local_procmail')dnl
FEATURE(`access_db')dnl
FEATURE(`blacklist_recipients')dnl
FEATURE(`dnsbl')dnl
MAILER(`local')dnl
MAILER(`smtp')dnl
MAILER(`procmail')dnl
```

## 这会指示 `sendmail.mc` 文件针对此特定配置进行如下设置

```text
define(`confDEF_USER_ID', `8:12'')dnl
```

此配置选项指定默认用户 ID。在我们的示例中，用户 `mail` 和组 `mail` 对应的 ID 号为 `8:12`（参见 `/etc/passwd` 和 `/etc/group` 文件）。

```text
OSTYPE(`linux')dnl
```

此配置选项指定 Sendmail 运行的默认操作系统；在我们的示例中是 `linux` 系统。此项是 `mc` 文件所需的最低限度信息之一。

```text
DOMAIN(`generic')dnl
```

此配置选项将指定并描述适合您环境的特定域。

```text
define(`confTRY_NULL_MX_LIST',true)dnl
```

此配置选项指定接收主机是否是某主机的最佳 MX，若是，则尝试直接连接到该主机。

```text
define(`confDONT_PROBE_INTERFACES',true)dnl
```

此配置选项若设置为 `true`，表示 Sendmail不会将任何本地接口的名称和地址插入 `$=w` 类（已知“等效”地址列表）。

```text
define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail')dnl
```

此配置选项设置服务器中已安装的 `procmail` 程序的路径。由于 Red Hat Linux 中的路径与其他 Linux 版本不同，我们必须使用此宏指定新路径。需要注意的是，此宏也被后面在此文件中定义的 `FEATURE(`local_procmail')` 所使用。

```text
define(`LOCAL_MAILER_FLAGS', `ShPfn')dnl
```

此配置选项定义本地邮件投递程序（`procmail`）必须使用的标志。有关每个标志的详细信息，请参见 Sendmail 文档。

```text
define(`LOCAL_MAILER_ARGS', `procmail -a $h -d $u')dnl
```

此配置选项定义必须传递给本地邮件投递程序（`procmail`）的参数。有关每个参数的详细信息，请参见 Sendmail 文档。

```text
FEATURE(`smrsh', `/usr/sbin/smrsh')dnl
```

此 `m4` 宏启用 `smrsh`（sendmail 受限 shell），以代替邮件程序默认使用的 `/bin/sh`。使用此功能，您可以通过 `/etc/mail/aliases` 和 `~/.forward` 文件控制通过电子邮件运行哪些程序。`smrsh` 程序的默认位置是 `/usr/libexec/smrsh`；由于我们已将 `smrsh` 正确安装在其他位置，因此需要向 `smrsh` 功能添加参数以指示新位置 `/usr/sbin/smrsh`。CERT 推荐使用 `smrsh`，因此建议您尽可能使用此功能。

```text
FEATURE(`mailertable')dnl
```

此 `m4` 宏启用 `mailertable`（数据库选择新投递代理）功能。`mailertable` 是一个将 `host.domain` 名称映射到特殊投递代理和新域名称对的数据库。使用此功能，可以通过指定或特定的投递代理将邮件投递到新域名。通常，此功能仅在中央邮件中心服务器上可用。

```text
FEATURE(`virtusertable', `hash -o /etc/mail/virtusertable')dnl
```

此 `m4` 宏启用 `virtusertable`（支持虚拟域）功能，允许在一台机器上托管多个虚拟域。`virtusertable` 是一个将虚拟域映射到新地址的数据库。使用此功能，发往虚拟域的邮件可以投递到本地、远程或单个用户地址。通常，此功能仅在中央邮件中心服务器上可用。

```text
FEATURE(`redirect')dnl
```

此 `m4` 宏启用 `redirect`（支持 `address.REDIRECT`）功能。使用此功能，例如，发往已停用用户账户 `wahib` 的邮件将被退回，并指示新的转发地址。已停用账户必须在邮件服务器上的 `aliases` 文件中设置。通常，此功能仅在中央邮件中心服务器上可用。

```text
FEATURE(`always_add_domain')dnl
```

此 `m4` 宏启用 `always_add_domain`（即使在本地邮件中也添加本地域）功能。使用此功能，所有本地投递的地址都将被完全限定。出于安全考虑，设置此功能是安全且推荐的。

```text
FEATURE(`use_cw_file')dnl
```

此 `m4` 宏启用 `use_cw_file`（使用 Metropolitan local-host-names 文件获取本地主机名）功能。使用此功能，您可以在 `/etc/mail/local-host-names` 文件中声明本地主机作为 MX 接收者的主机列表。换句话说，此功能使 `/etc/mail/local-host-names` 文件被读取以获取本地主机的替代名称。

```text
FEATURE(`local_procmail')dnl
```

此 `m4` 宏启用 `local_procmail`（使用 `procmail` 作为本地投递代理）功能。使用此功能，您可以将 `procmail` 用作 Sendmail 投递代理。

```text
FEATURE(`access_db')dnl
```

此 `m4` 宏启用访问数据库功能。使用此功能，您可以通过访问数据库允许或拒绝接受来自指定域的邮件。通常，此功能仅在中央邮件中心服务器上可用。

```text
FEATURE(`blacklist_recipients')dnl
```

此 `m4` 宏启用阻止某些收件人用户名、主机名或地址的传入邮件的功能。使用此功能，例如，您可以阻止发往用户 `nobody`、主机 `foo.mydomain.com` 或 `guest@bar.mydomain.com` 的传入邮件。

```text
FEATURE(`dnsbl')dnl
```

此 `m4` 宏使 Sendmail 能够拒绝来自实时黑名单数据库 `rbl.maps.vix.com` 中任何站点的邮件。基于 DNS 的拒绝是 DNS 中维护的垃圾邮件发送者数据库。详细信息请参见 `http://maps.vix.com/rbl/`。

```text
MAILER(`local')dnl
MAILER(`smtp')dnl
MAILER(`procmail')dnl
```

此 `m4` 宏启用 `local`、`smtp` 和 `procmail` 作为投递代理（在 Sendmail 中，默认情况下投递代理不会自动声明）。使用此功能，您可以指定要支持哪些以及忽略哪些。`MAILER(`local')`、`MAILER(`smtp')` 和 `MAILER(`procmail')` 选项将包含对 `local`、`smtp`、`esmtp`、`smtp8`、`relay` 投递代理和 `procmail` 的支持。需要注意的是，`MAILER(`smtp')` 应始终先于 `MAILER(`procmail')`。

**注意：** 有时，您希望继续通信的某个域可能会出现在 RBL 列表中。在这种情况下，Sendmail 允许您覆盖这些域以允许接收其电子邮件。为此，只需编辑 `/etc/mail/access` 文件并添加适当的域信息。

例如：

```text
blacklisted.domain	OK
```

## 第 2 步

既然我们的宏配置文件 `sendmail.mc` 已创建，我们可以使用以下命令从这些语句构建 Sendmail 配置文件 `sendmail.cf`：

```text
[root@deep /]# cd /var/tmp/sendmail-version/cf/cf/
[root@deep cf]# m4 ../m4/cf.m4 sendmail.mc > /etc/mail/sendmail.cf
```

**注意：** 此处，`../m4/cf.m4` 告诉 `m4` 程序在哪里查找其默认配置文件信息。

## 第 3 步：仅用于本地或相邻客户端和服务器的 `null.mc` 文件

由于我们的本地客户端计算机从不直接接收来自外部世界的邮件，而是通过邮件中心服务器中继（发送）其所有邮件，因此我们将创建一个名为 `null.mc` 的特殊文件，该文件在后续处理后将创建一个定制的 `sendmail.cf` 配置文件，以响应我们相邻或本地服务器客户端计算机的这种特殊设置。这个 `m4` 宏文件创建和配置起来很简单，因为它不需要很多功能，不像中央邮件中心服务器的配置文件（`sendmail.mc`）那样需要大量功能。

### 第 1 步

创建 `null.mc` 文件（`touch /var/tmp/sendmail-version/cf/cf/null.mc`）并添加以下行：

```text
OSTYPE(`linux')dnl
DOMAIN(`generic')dnl
FEATURE(`nullclient',`mail.openna.com')dnl
undefine(`ALIAS_FILE')dnl
```

## 这告诉 `null.mc` 文件为此特定配置设置进行如下配置

- `OSTYPE(\`linux')`

  此配置选项指定 Sendmail 运行的默认操作系统，在我们的示例中，是 `linux` 系统。此项是 `mc` 文件所需的最低限度信息之一。

- `DOMAIN(\`generic')`

  此配置选项将指定并描述适合您环境的特定域。

- `FEATURE(\`nullclient', \`mail.openna.com')`

  此 `m4` 宏将客户端计算机设置为从不直接接收邮件，将其邮件发送到中央邮件中心，并通过该服务器中继所有邮件，而不是直接发送。此功能创建一个精简的配置文件，仅包含通过基于本地 SMTP 的网络将所有邮件转发到邮件中心的支持。此功能中包含的参数 `mail.openna.com` 是该邮件中心的规范名称。您应该将此规范名称更改为反映您的邮件中心服务器，例如：`FEATURE(\`nullclient', \`my.mailhub.com')`。

- `undefine(\`ALIAS_FILE')`

  此配置选项防止 nullclient 版本的 Sendmail 尝试访问 `/etc/mail/aliases` 和 `/etc/mail/aliases.db` 文件。通过在 `.mc` 文件中添加此行，您无需在所有内部相邻客户端 Sendmail 机器上都保留 `aliases` 文件。`aliases` 文件仅在邮件中心服务器上为网络中的所有服务器和客户端别名所需。

**注意：** 我们注意到，使用这种配置时，不应定义任何邮件投递程序，也不进行任何别名或转发操作。

### 步骤 2

现在我们的宏配置文件 `null.mc` 已经创建完成，我们可以从这些语句中在所有邻居服务器和客户端机器上构建 Sendmail 配置文件 `sendmail.cf`，使用以下命令：

```text
[root@deep /]# cd /var/tmp/sendmail-version/cf/cf/
[root@deep cf]# m4 ../m4/cf.m4 null.mc > /etc/mail/sendmail.cf
```

### 步骤 3

不应再有任何邮件被投递到您的本地机器。由于没有入站邮件连接，您不再需要在邻居或本地服务器、客户端机器上运行 Sendmail 守护进程。

要在邻居或本地服务器、客户端机器上停止运行 Sendmail 守护进程，请编辑或创建 `/etc/sysconfig/sendmail` 文件，并将以下行：

```text
DAEMON=yes
```

更改为：

```text
DAEMON=no
```

以及：

```text
QUEUE=1h
```

**注意：** `/etc/sysconfig/sendmail` 文件中的 `QUEUE=1h` 会使 Sendmail 每 1 小时处理一次队列。我们保留该行，因为即使邮件中心宕机，Sendmail 仍需要定期处理队列。

### 步骤 4

本地机器从不使用别名、访问权限或其他映射数据库。由于所有映射文件数据库都位于网络中的中央邮件中心服务器上，并供所有本地机器使用，我们可以安全地从所有本地机器中删除以下命令和手册页。

- `/usr/bin/newaliases`
- `/usr/man/man1/newaliases.1`
- `/usr/man/man5/aliases.5`

要从系统中删除以下文件，请使用以下命令：

```text
[root@client /]# rm -f /usr/bin/newaliases
[root@client /]# rm -f /usr/man/man1/newaliases.1
[root@client /]# rm -f /usr/man/man5/aliases.5
```

### 步骤 5

从整个本地 Sendmail 服务器或客户端中删除不必要的 Procmail 程序。由于本地机器将所有内部和出站邮件发送到邮件中心服务器以待后续投递，我们不需要使用像 Procmail 这样复杂的本地投递代理程序来完成这项工作。相反，我们可以使用默认的 `/bin/mail` 程序。

要从系统中删除 Procmail，请使用以下命令：

```text
[root@client]# rpm -e procmail
```

## 中央邮件中心的 `/etc/mail/access` 和 `access.db` 文件

可以创建 `access` 数据库文件，用于接受或拒绝来自选定域的邮件。例如，您可以选择拒绝来自已知垃圾邮件发送者的所有邮件，或者接受来自本地网络的所有邮件的中继，因为现在 Sendmail 默认拒绝中继（这是一项反垃圾邮件功能）。在下面的 `access` 文件示例中，我们将允许来自 localhost 以及所有以 IP 地址 192.168.1 开头的本地网络地址的中继。`access` 和 `access.db` 文件对于本地或邻居客户端设置不是必需的。只有当您决定设置中央邮件中心来处理所有邮件时才需要它。另外请注意，使用中央邮件中心将提高网络上运行 Sendmail 的其他服务器和客户端的安全性和管理效率。

### 步骤 1

创建 `access` 文件（`touch /etc/mail/access`）并添加以下行：




# Sendmail `access` 文件

以下格式说明来自 Sendmail 源代码发行版中的 `cf/README` 文件。

该表使用电子邮件地址、域名和网络号作为键。例如：

```text
spammer@aol.com     REJECT
cyberspammer.com    REJECT
192.168.212         REJECT
```

这将拒绝来自 `spammer@aol.com` 的邮件、来自 `cyberspammer.com` 的任何用户（或该域中的任何主机）的邮件，以及来自 `192.168.212.*` 网络中任何主机的邮件。

映射的值部分可以包含：

```text
OK       即使运行中的其他规则集会拒绝邮件，也接受邮件。
         例如，域名无法解析时仍然接受。

RELAY    接受发送到指定域或从指定域接收的邮件，并通过您的 SMTP
         服务器进行中继。RELAY 也会对其他检查隐式执行 OK。

REJECT   使用通用消息拒绝发件人或收件人。

DISCARD  使用 $#discard 邮件程序完全丢弃邮件。这仅适用于发件人地址，
         表示应丢弃从指定域接收到的所有内容。

### any text
         其中，### 是符合 RFC 821 的错误代码，
         "any text" 是要为该命令返回的消息。
```

例如：

```text
cyberspammer.com           550 We don't accept mail from spammers
okay.cyberspammer.com     OK
sendmail.org               OK
128.32                     RELAY
```

这将接受来自 `okay.cyberspammer.com` 的邮件，但会使用指定消息拒绝来自 `cyberspammer.com` 的其他所有主机的邮件。它允许接受来自 `sendmail.org` 域中任何主机的邮件，并允许对 `128.32.*.*` 网络执行中继。

您还可以使用访问数据库，根据地址中的用户名部分阻止发件人地址。例如：

```text
FREE.STEALTH.MAILER@    550 Spam not accepted
```

请注意，必须在用户名后包含 `@`，以表示该数据库条目仅用于检查发件人的用户名部分。

如果像我们一样在 `sendmail.mc` 宏配置中使用：

```m4
FEATURE(`blacklist_recipients')
```

则可以在映射中添加本地用户、域中的主机，或域中不应接收邮件的地址：

```text
badlocaluser                       550 Mailbox disabled for this username
host.mydomain.com                  550 That host does not accept mail
user@otherhost.mydomain.com        550 Mailbox disabled for this recipient
```

这将阻止以下收件人接收邮件：

- `badlocaluser@mydomain.com`
- `host.mydomain.com` 上的任何用户
- 单独的地址 `user@otherhost.mydomain.com`

启用此功能后，访问映射中值部分包含错误消息或 `REJECT` 的所有地址都无法发送邮件。

以上述示例为例：

```text
spammer@aol.com    REJECT
cyberspammer.com   REJECT
```

邮件无法发送到 `spammer@aol.com` 或 `cyberspammer.com` 中的任何地址。

现在配置访问文件。默认情况下，我们允许从本地主机进行中继：

```text
localhost.localdomain    RELAY
localhost                 RELAY
127.0.0.1                 RELAY
192.168.1                 RELAY
```

**注意**：不要忘记在此 `access` 文件中指定您想要中继的私有 IP 地址范围，否则您将无法从内部网络发送邮件。

### 步骤 2：创建 `access.db` 文件

请记住，由于 `/etc/mail/access` 是一个数据库，因此在创建上述文本文件后，您必须使用 `makemap` 实用程序来创建数据库映射。

要创建 `access` 数据库映射，请使用以下命令：

```bash
[root@deep /]# makemap hash /etc/mail/access.db < /etc/mail/access
```

# 中央邮件中心的 `/etc/mail/aliases` 和 `aliases.db` 文件

别名是将系统上的一个本地收件人名称转换为另一个名称的过程。别名仅发生在本地名称上。

示例用途包括将通用名称（如 `root`）转换为系统上的真实用户名，或将一个名称转换为多个名称的列表（用于邮件列表）。

对于每个将本地用户列为收件人的信封，Sendmail 会在 `aliases` 文件中查找该收件人的名称。由于 Sendmail 可能需要在 `aliases` 文件中搜索数千个名称，因此该文件的副本以独立的 `db` 数据库格式存储，以显著提高查找速度。

如果您将 Sendmail 配置为使用中央服务器（邮件中心）处理所有邮件，则不需要在邻居服务器或客户端机器上安装 `aliases` 和 `aliases.db` 文件。

### 步骤 1：创建 `aliases` 文件

创建 `aliases` 文件：

```bash
touch /etc/mail/aliases
```

并默认添加以下行：

```text
#
#   @(#)aliases   8.2 (Berkeley) 3/5/94
#
# Aliases in this file will NOT be expanded in the header from
# Mail, but WILL be visible over networks or from /bin/mail.
#
#   >>>>>>>>>>      The program "newaliases" must be run after
#   >> NOTE >>      this file is updated for any changes to
#   >>>>>>>>>>      show through to sendmail.
#
```

```text
# Basic system aliases -- these MUST be present.
MAILER-DAEMON:  postmaster
postmaster:     root

# General redirections for pseudo accounts.
bin:            root
daemon:         root
nobody:         root

# Person who should get root's mail
#root:          admin
```

**注意**：您的 `aliases` 文件可能会复杂得多，但即便如此，请注意示例展示了别名的最基本形式。

### 步骤 2：创建 `aliases.db` 文件

由于 `/etc/mail/aliases` 是一个数据库，因此在创建上述文本文件后，您必须使用 `makemap` 程序来创建数据库映射。

要创建 `aliases` 数据库映射，请使用以下命令：

```bash
[root@deep /]# makemap hash /etc/mail/aliases.db < /etc/mail/aliases
```

# 中央邮件中心的映射文件

以下文件与 Sendmail 的特定功能相关，系统管理员可以对这些功能进行调整：

- `/etc/mail/virtusertable`
- `/etc/mail/domaintable`
- `/etc/mail/mailertable`
- `/etc/mail/virtusertable.db`
- `/etc/mail/domaintable.db`
- `/etc/mail/mailertable.db`

这些功能通常仅在中央邮件中心服务器上需要。

## `virtusertable` 和 `virtusertable.db` 文件

`virtusertable` 是一个将虚拟域映射到新地址的数据库。通过此功能，网络中虚拟域的邮件可以被投递到本地、远程或单一用户地址。

## `domaintable` 和 `domaintable.db` 文件

`domaintable` 是一个将旧域映射到新域的数据库。通过此功能，网络中的多个域名可以从旧域重写为新域。

## `mailertable` 和 `mailertable.db` 文件

邮件路由表（`mailertable`）是一个将 `host.domain` 名称映射到特定投递代理和新域名对的数据库。借助此功能，您网络中的邮件可以通过使用特定的投递代理投递到新的本地或远程域名。

要创建 `virtusertable`、`domaintable`、`mailertable` 及其对应的 `.db` 文件并使用它们，请执行以下命令：

```bash
[root@deep /]# for map in virtusertable domaintable mailertable
> do
> touch /etc/mail/${map}
> chmod 0644 /etc/mail/${map}
> makemap hash /etc/mail/${map}.db < /etc/mail/${map}
> chmod 0644 /etc/mail/${map}.db
> done
```

# 所有配置类型的 `/etc/mail/local-host-names` 文件

系统会读取 `/etc/mail/local-host-names` 文件，以获取本地主机的替代名称。该文件的一种用途可能是声明您网络中本地主机充当 MX 收件人的主机列表。

在该机器上，只需将需要它处理邮件的机器名称添加到 `/etc/mail/local-host-names` 中，例如 `mail.openna.com`。

创建 `local-host-names` 文件：

```bash
touch /etc/mail/local-host-names
```

并添加以下行：

```text
# local-host-names - include all aliases for your machine here.
openna.com
deep.openna.com
www.openna.com
win.openna.com
mail.openna.com
```

通过此类配置，所有发送的邮件看起来都将像是来自 `openna.com`，而任何发送到 `www.openna.com` 或其他主机的邮件都将被投递到我们的邮件中心 `mail.openna.com`。

请注意，如果您将系统配置为伪装成另一台机器，那么从您的系统发送到您系统的任何电子邮件都将被发送到您正在伪装的那台机器。

例如，在上面的示例中，Linux 的 `cron` 守护进程定期发送给 `root@www.openna.com` 的日志文件，将被发送到 `root@mail.openna.com`，即我们的邮件中心。

# 所有配置类型的 `/etc/sysconfig/sendmail` 文件配置

`/etc/sysconfig/sendmail` 文件用于指定 Sendmail 配置信息，例如：

- Sendmail 是否应以守护进程方式运行
- 是否应监听邮件
- 队列目录中的消息未投递时，等待多长时间再发送警告

创建 `sendmail` 文件：

```bash
touch /etc/sysconfig/sendmail
```

并在此文件中添加：

```text
DAEMON=yes
QUEUE=1h
```

`DAEMON=yes` 选项指示 Sendmail 以守护进程方式运行。

当 Sendmail 客户端机器配置为不直接接受来自外部的邮件，而是将所有本地邮件转发到中央中心时，这一行很有用；不以守护进程方式运行也能提高安全性。

如果您已按照这种方式配置了服务器或客户端机器，只需将 `DAEMON=yes` 替换为 `DAEMON=no`。

邮件通常因为无法立即传输而被放入队列。`QUEUE=1h` 设置的是：如果消息尚未投递，则在向发送者发送警告之前等待的时间间隔。

# 所有配置类型的 `/etc/rc.d/init.d/sendmail` 脚本文件配置

配置 `/etc/rc.d/init.d/sendmail` 脚本文件，以启动和停止 Sendmail 守护进程。

创建 `sendmail` 脚本文件：

```bash
touch /etc/rc.d/init.d/sendmail
```

并添加：




```sh
#!/bin/sh
#
# sendmail  This shell script takes care of starting and stopping
#           sendmail.
#
# chkconfig: 2345 80 30
# description: Sendmail is a Mail Transport Agent, which is the program \
#              that moves mail from one machine to another.
# processname: sendmail
# config: /etc/sendmail.cf
# pidfile: /var/run/sendmail.pid

# Source function library.
. /etc/rc.d/init.d/functions

# Source networking configuration.
. /etc/sysconfig/network

# Source sendmail configuration.
if [ -f /etc/sysconfig/sendmail ] ; then
    . /etc/sysconfig/sendmail
else
    DAEMON=yes
    QUEUE=1h
fi

# Check that networking is up.
[ ${NETWORKING} = "no" ] && exit 0

[ -f /usr/sbin/sendmail ] || exit 0

RETVAL=0

# See how we were called.
case "$1" in
  start)
    # Start daemons.

    echo -n "Starting sendmail: "
    /usr/bin/newaliases > /dev/null 2>&1
    for i in virtusertable access domaintable mailertable ; do
        if [ -f /etc/mail/$i ] ; then
            makemap hash /etc/mail/$i < /etc/mail/$i
        fi
    done
    daemon /usr/sbin/sendmail $([ "$DAEMON" = yes ] && echo -bd) \
        $([ -n "$QUEUE" ] && echo -q$QUEUE)
    RETVAL=$?
    echo
```

```sh
[ $RETVAL -eq 0 ] && touch /var/lock/subsys/sendmail
;;
stop)
  # Stop daemons.
  echo -n "Shutting down sendmail: "
  killproc sendmail
  RETVAL=$?
  echo
  [ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/sendmail
  ;;
restart|reload)
  $0 stop
  $0 start
  RETVAL=$?
  ;;
status)
  status sendmail
  RETVAL=$?
  ;;
*)
  echo "Usage: sendmail {start|stop|restart|status}"
  exit 1
esac

exit $RETVAL
```

现在，使此脚本可执行并更改其默认权限：

```sh
[root@deep /]# chmod 700 /etc/rc.d/init.d/sendmail
```

使用以下命令为 Sendmail 创建符号链接 `rc.d`：

```sh
[root@deep /]# chkconfig --add sendmail
```

使用以下命令手动启动您的 Sendmail 服务器：

```text
[root@deep /]# /etc/rc.d/init.d/sendmail start
Starting sendmail:           [ OK ]
```

## 工作完成后清理

```sh
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf sendmail-version/ sendmail.version.tar.gz
```

上面使用的 `rm` 命令将删除我们用于编译和安装 Sendmail 的所有源文件。它还会从 `/var/tmp` 目录中删除 Sendmail 压缩归档文件。

## 保护 Sendmail

### Sendmail 受限 shell `smrsh`

`smrsh` 程序旨在替代 Sendmail 程序邮件器定义中的 `/bin/sh`。它是一个受限 shell 工具，能够通过 `/etc/smrsh` 目录指定 Sendmail 可用的可执行程序列表。更准确地说，即使“坏人”能够让 Sendmail 在不通过别名或转发文件的情况下运行程序，`smrsh` 也能限制他或她能够执行的程序集。

当与 Sendmail 结合使用时，`smrsh` 有效地将 Sendmail 的程序执行范围限制为仅在 `smrsh` 目录中指定的那些程序。如果您遵循了我们在上面所做的操作，`smrsh` 程序已经编译并安装在您计算机上的 `/usr/sbin/smrsh` 中。

#### 步骤 1

我们需要做的第一件事是确定 `smrsh` 应该允许 Sendmail 运行的命令列表。

默认情况下，我们包括但不限于：

- `/bin/mail`（如果它已安装在您的系统上）
- `/usr/bin/procmail`（如果它已安装在您的系统上）。灵感来自诺贝尔物理学奖得主理查德·费曼（Richard Feynman）。

**注意：** 您不应在可接受命令列表中包含解释器程序，如 `sh(1)`、`csh(1)`、`perl(1)`、`uudecode(1)` 或流编辑器 `sed(1)`。

#### 步骤 2

接下来，您需要用 Sendmail 允许执行的程序填充 `/etc/smrsh` 目录。为了防止程序重复，并做得更规范，最好从 `/etc/smrsh` 建立到可接受程序的链接，而不是将程序复制到此目录。

- 要允许 `mail` 程序 `/bin/mail`，请使用以下命令：

  ```sh
  [root@deep /]# cd /etc/smrsh
  [root@deep smrsh]# ln -s /bin/mail mail
  ```

- 要允许 `procmail` 程序 `/usr/bin/procmail`，请使用以下命令：

  ```sh
  [root@deep /]# cd /etc/smrsh
  [root@deep smrsh]# ln -s /usr/bin/procmail procmail
  ```

这将允许从用户的 `.forward` 文件或使用 `program` 语法的 `aliases` 文件运行 `mail` 和 `procmail` 程序。

**注意：** `Procmail` 仅在邮件中心服务器（Mail Hub Server）中是必需的，在本地客户端邮件服务器（Local Client Mail Server）中并不需要。如果您的系统配置为邮件中心服务器，则按照上述说明建立与 `procmail` 的链接；如果您的系统配置为本地客户端服务器，则跳过上面的 `procmail` 步骤。

#### 步骤 3

我们现在可以将 Sendmail 配置为使用受限 shell。程序邮件器在 Sendmail 配置文件 `/etc/mail/sendmail.cf` 中由单行定义。您必须修改 `sendmail.cf` 文件中的这行 `Mprog` 定义，将 `/bin/sh` 规范替换为 `/usr/sbin/smrsh`。

编辑 `sendmail.cf` 文件（`vi /etc/mail/sendmail.cf`）并更改以下行。

例如：

```text
Mprog,  P=/bin/sh, F=lsDFMogeu9, S=10/30, R=20/40, D=$z:/, T=X-Unix, A=sh -c $u
```

应更改为：

```text
Mprog,  P=/usr/sbin/smrsh, F=lsDFMoqeu9, S=10/30, R=20/40, D=$z:/, T=X-Unix, A=sh -c $u
```

- 现在使用以下命令手动重新启动 `sendmail` 进程：

  ```sh
  [root@deep /]# /etc/rc.d/init.d/sendmail restart
  ```

**注意：** 在上面我们为邮件中心服务器配置的 `sendmail.mc` 配置文件中，我们已经使用 `m4` 宏 `FEATURE(\`smrsh',\`/usr/sbin/smrsh')` 将这行 `Mprog` 配置为使用受限 shell `/usr/sbin/smrsh>`，因此如果 `/usr/sbin/smrsh` 规范已经在您邮件中心中继的 `/etc/mail/sendmail.cf` 文件中设置好，请不要惊讶。

相反，请使用上面所示的技术处理您网络中的其他 `/etc/mail/sendmail.cf` 文件，例如使用 `null.mc` 宏配置文件生成 `/etc/mail/sendmail.cf` 文件的零客户端（“本地或相邻客户端和服务器”）。

## `/etc/mail/aliases` 文件

管理不当或粗心的 `aliases` 文件很容易被利用来获取特权状态。例如，许多供应商在发货时会在 `/etc/mail/aliases` 文件中预置一个 `decode` 别名。其目的是为用户提供一个通过邮件传输二进制文件的便捷方式。

在发送端，用户将二进制文件转换为 ASCII 格式的 `uuencode`，然后将结果发送到接收端的 `decode` 别名。该别名会将邮件内容通过管道传递给 `/usr/bin/uuencode` 程序，将 ASCII 还原为原始二进制文件。

请从 `/etc/mail/aliases` 文件中删除 `decode` 别名行。同样，对于每一个执行程序的别名，如果该程序不是你自己放置并完全检查过的，都应该被质疑并很可能需要删除。

编辑 `aliases` 文件（`vi /etc/mail/aliases`）并删除以下行：

```text
# Basic system aliases -- these MUST be present.
MAILER-DAEMON: postmaster
postmaster:	root

# General redirections for pseudo accounts.
bin:		root
daemon:		root
games:		root ← 删除此行。
ingres:		root ← 删除此行。
nobody:		root
system:		root ← 删除此行。
toor:		root ← 删除此行。
uucp:		root ← 删除此行。

# Well-known aliases.
manager:		root ← 删除此行。
dumper:		root ← 删除此行。
operator:		root ← 删除此行。

# trap decode to catch security attacks
decode:		root ← 删除此行。

# Person who should get root's mail
#root:		marc
```

- 要使更改生效，您需要运行：

  ```sh
  [root@deep /]# /usr/bin/newaliases
  ```

## 防止 Sendmail 被未授权用户滥用

Sendmail 现在包含强大的反垃圾邮件功能，可以帮助防止您的邮件服务器被未授权用户滥用。要做到这一点，请编辑 `/etc/mail/sendmail.cf` 文件并对配置文件进行修改以阻止垃圾邮件发送者。

编辑 `sendmail.cf` 文件（`vi /etc/mail/sendmail.cf`）并修改以下行：

```text
O PrivacyOptions=authwarnings
```

修改为：

```text
O PrivacyOptions=authwarnings,goaway
```

设置 `goaway` 选项会使 Sendmail 禁止所有 SMTP `EXPN` 命令，同时也会拒绝所有 SMTP `VERB` 命令并禁止所有 SMTP `VRFY` 命令。这些更改可以防止垃圾邮件发送者利用 Sendmail 中的 `EXPN` 和 `VRFY` 命令。

## 限制谁可以查看队列内容

通常情况下，任何人都可以使用 `mailq` 命令查看邮件队列内容。要限制谁可以查看队列内容，您必须在 `/etc/mail/sendmail.cf` 文件中指定 `restrictmailq` 选项。

使用此选项后，Sendmail 仅允许与队列目录（root）具有相同组权限的用户查看内容。这使得队列目录可以用 0700 模式完全保护，而选定的用户仍然能够查看内容。

编辑 `sendmail.cf` 文件（`vi /etc/mail/sendmail.cf`）并修改以下行：

```text
O PrivacyOptions=authwarnings,goaway
```

修改为：

```text
O PrivacyOptions=authwarnings,goaway,restrictmailq
```

- 现在我们将队列目录的权限更改为完全保护：

  ```sh
  [root@deep /]# chmod 0700 /var/spool/mqueue
  ```

- 现在手动重新启动 `sendmail` 进程以使更改生效：

  ```sh
  [root@deep /]# /etc/rc.d/init.d/sendmail restart
  Shutting down sendmail:         [ OK ]
  Starting sendmail:              [ OK ]
  ```

**注意：** 我们已经在 `sendmail.cf` 文件的 `PrivacyOptions=` 行中添加了 `goaway` 选项。现在我们继续在该行中添加限制性的 `restrictmailq` 选项。

任何非特权用户尝试查看邮件队列内容时都会收到以下消息：

```text
[user@deep /]$ /usr/bin/mailq
You are not permitted to see the queue
```

## 将队列处理限制为 `root`

通常情况下，任何人都可以使用 `-q` 开关处理队列。要将队列处理限制为 `root` 和队列目录的所有者，您必须在 `/etc/mail/sendmail.cf` 文件中指定 `restrictqrun` 选项。

编辑 `sendmail.cf` 文件（`vi /etc/mail/sendmail.cf`）并修改以下行：

```text
O PrivacyOptions=authwarnings,goaway,restrictmailq
```

修改为：

```text
O PrivacyOptions=authwarnings,goaway,restrictmailq,restrictqrun
```

- 现在手动重新启动 `sendmail` 进程以使更改生效：

  ```sh
  [root@deep /]# /etc/rc.d/init.d/sendmail restart
  Shutting down sendmail:         [ OK ]
  Starting sendmail:              [ OK ]
  ```

任何非特权用户尝试处理队列时都会收到以下消息：

```text
[user@deep /]$ /usr/sbin/sendmail -q
You do not have permission to process the queue
```

## SMTP 问候消息

当 Sendmail 接受传入的 SMTP 连接时，它会向另一台主机发送问候消息。此消息标识本地机器，是它发送的第一个表示就绪的信号。

编辑 `sendmail.cf` 文件（`vi /etc/mail/sendmail.cf`）并修改以下行。

## 对重要的 Sendmail 文件设置不可变属性

重要的 Sendmail 文件可以使用 Linux 的 `chattr` 命令设置为不可变以获得更好的安全性。具有 `+i` 属性的文件不能被修改、删除或重命名；不能创建指向此文件的链接，也不能向该文件写入数据。只有超级用户才能设置或清除此属性。

- 对 `sendmail.cf` 文件设置不可变位：

  ```sh
  [root@deep /]# chattr +i /etc/mail/sendmail.cf
  ```

- 对 `local-host-names` 文件设置不可变位：

  ```sh
  [root@deep /]# chattr +i /etc/mail/local-host-names
  ```

- 对 `aliases` 文件设置不可变位：

  ```sh
  [root@deep /]# chattr +i /etc/mail/aliases
  ```

- 对 `access` 文件设置不可变位：

  ```sh
  [root@deep /]# chattr +i /etc/mail/access
  ```

## 更多文档

更多详细信息，您可以阅读以下几个 `man` 页面：



```text
$ man aliases (5)           - sendmail 的别名文件
$ man makemap (8)           - 为 sendmail 创建数据库映射
$ man sendmail (8)          - 电子邮件传输代理
$ man mailq (1)             - 打印邮件队列
$ man newaliases (1)        - 重新构建邮件别名文件的数据库
$ man mailstats (8)         - 显示邮件统计信息
$ man praliases (8)         - 显示系统邮件别名
```

## Sendmail 管理员工具

以下列出的命令是我们经常使用的，但还有更多命令存在。请查看 man 页面和文档以获取更多详细信息和信息。

### `newaliases`

Sendmail 的 `newaliases` 程序工具的目的是为邮件别名文件 `/etc/mail/aliases` 重建和更新随机访问数据库。每次更改此文件内容后都必须运行它，以使更改生效。

- 要使用 `newaliases` 工具更新别名文件，请使用以下命令：

  ```text
  [root@deep /]# /usr/bin/newaliases
  ```

### `makemap`

`makemap` 程序工具的目的是在 Sendmail 中创建数据库映射。只有在需要为 `aliases`、`access`、`domaintable`、`mailertable` 和 `virtusertable` 等文件创建新数据库时才需要使用 `makemap` 命令。

- 要运行 `makemap` 为 `access` 创建新数据库，请使用以下命令：

  ```text
  [root@deep /]# makemap hash /etc/mail/access.db < /etc/mail/access
  ```

其中 `<hash>` 是数据库格式，`makemap` 可以处理多达三种不同的数据库格式；它们可以是 `hash`、`btree` 或 `dbm`。`/etc/mail/access.db` 是要创建的新数据库的位置和名称。`/etc/mail/access` 是 `makemap` 从中读取标准输入文件的位置。在我们的示例中，我们使用上面的 `makemap` 命令创建了一个新的 `access.db` 文件。要为 `aliases`、`domaintable`、`mailertable` 和 `virtusertable` 等其他文件创建数据库，您必须在 `makemap` 命令中指定相应文件的位置和名称。

### `mailq`

`mailq` 程序工具的目的是打印排队等待将来发送的邮件消息的摘要。

- 要打印排队邮件消息的摘要，请使用以下命令：

  ```text
  [root@deep /]# mailq
  Mail queue is empty
  ```

## Sendmail 用户工具

以下列出的命令是我们经常使用的，但还有更多命令存在。请查看 man 页面和文档以获取更多详细信息和信息。

### `mailstats`

`mailstats` 程序工具的目的是显示当前邮件统计信息的内容。

- 要显示当前邮件统计信息，请使用以下命令：

  ```text
  [root@deep /]# mailstats
  Statistics from Tue Dec 14 20:31:48 1999
  M  msgsfr  bytes_from  msgsto  bytes_to  msgsrej  msgsdis  Mailer
  5   0       0K          1       3K        0        0        esmtp
  8   1259    19618K      1259    19278K    0        0        local
  ============================================================
  T   1259    19618K      1260    19281K    0        0
  ```

### `praliases`

`praliases` 程序工具的目的是逐行显示当前系统邮件别名，顺序随机。

- 要显示当前系统别名，请使用以下命令：

  ```text
  [root@deep /]# praliases
  postmaster:root
  daemon:root
  root:admin
  @:@
  mailer-daemon:postmaster
  bin:root
  nobody:root
  webadmin:admin
  www:root
  ```

## Sendmail 中央邮件中心已安装文件

- `/etc/rc.d/init.d/sendmail`
- `/etc/rc.d/rc0.d/K30sendmail`
- `/etc/rc.d/rc1.d/K30sendmail`
- `/etc/rc.d/rc2.d/S80sendmail`
- `/etc/rc.d/rc3.d/S80sendmail`
- `/etc/rc.d/rc4.d/S80sendmail`
- `/etc/rc.d/rc5.d/S80sendmail`
- `/etc/rc.d/rc6.d/K30sendmail`
- `/etc/sysconfig/sendmail`
- `/etc/mail`
- `/etc/mail/statistics`
- `/etc/mail/sendmail.cf`
- `/etc/mail/access`
- `/etc/mail/access.db`
- `/etc/mail/aliases`
- `/etc/mail/aliases.db`
- `/etc/mail/virtusertable`
- `/etc/mail/virtusertable.db`
- `/etc/mail/domaintable`
- `/etc/mail/domaintable.db`
- `/etc/mail/mailertable`
- `/etc/mail/mailertable.db`
- `/etc/mail/local-host-names`
- `/etc/smrsh`
- `/usr/bin/newaliases`
- `/usr/bin/mailq`
- `/usr/bin/hoststat`
- `/usr/bin/purgestat`
- `/usr/lib/sendmail`
- `/usr/man/man1/mailq.1`
- `/usr/man/man1/newaliases.1`
- `/usr/man/man5/aliases.5`
- `/usr/man/man8/sendmail.8`
- `/usr/man/man8/mailstats.8`
- `/usr/man/man8/makemap.8`
- `/usr/man/man8/praliases.8`
- `/usr/man/man8/smrsh.8`
- `/usr/sbin/sendmail`
- `/usr/sbin/mailstats`
- `/usr/sbin/makemap`
- `/usr/sbin/praliases`
- `/usr/sbin/smrsh`
- `/var/spool/mqueue`

## Sendmail 本地服务器或客户端已安装文件

- `/etc/rc.d/init.d/sendmail`
- `/etc/rc.d/rc0.d/K30sendmail`
- `/etc/rc.d/rc1.d/K30sendmail`
- `/etc/rc.d/rc2.d/S80sendmail`
- `/etc/rc.d/rc3.d/S80sendmail`
- `/etc/rc.d/rc4.d/S80sendmail`
- `/etc/rc.d/rc5.d/S80sendmail`
- `/etc/rc.d/rc6.d/K30sendmail`
- `/etc/sysconfig/sendmail`
- `/etc/mail`
- `/etc/mail/statistics`
- `/etc/mail/sendmail.cf`
- `/etc/mail/local-host-names`
- `/etc/smrsh`
- `/usr/bin/mailq`
- `/usr/bin/hoststat`
- `/usr/bin/purgestat`
- `/usr/lib/sendmail`
- `/usr/man/man1/mailq.1`
- `/usr/man/man8/sendmail.8`
- `/usr/man/man8/mailstats.8`
- `/usr/man/man8/smrsh.8`
- `/usr/sbin/sendmail`
- `/usr/sbin/mailstats`
- `/usr/sbin/smrsh`
- `/var/spool/mqueue`

## Linux IMAP 与 POP 服务器

### 概述

如果你已将 Sendmail 配置为中央邮件中心服务器，则必须安装 IMAP/POP 软件，否则你将无法充分利用你的 Linux 邮件服务器，因为 Sendmail 只是将邮件从一台机器发送到另一台机器的软件，仅此而已。邮件服务器是指运行以下一种或多种服务的服务器：IMAP 服务器、POP3 服务器、POP2 服务器或 SMTP 服务器。SMTP 服务器的一个例子是 Sendmail，在继续阅读本书的这部分之前，它必须已经作为中央邮件中心安装在你的 Linux 服务器上。现在，我们将介绍安装 IMAP4、POP3 和 POP2，它们都包含在一个软件包中。

借助 IMAP 和 POP 软件，远程“客户端”邮件程序可以像访问本地存储一样访问 Linux 邮件服务器上的邮件存储。例如，用户可以在家中、办公室等地的电脑上处理收到并存储在 IMAP 服务器上的邮件，而无需在这些电脑之间来回传输消息或文件。

POP 代表“邮局协议”（Post Office Protocol），它只允许你列出邮件、检索邮件和删除邮件。IMAP 是增强版的 POP。它可以让你轻松维护多个账户、多人访问一个账户、将邮件保留在服务器上、仅下载邮件头或正文、不下载附件等等。IMAP 非常适合经常外出或有严重邮件需求的用户。大多数发行版默认提供的 POP 和 IMAP 服务器已能满足大多数需求。

### 这些安装说明假设

- 命令与 Unix 兼容。
- 源代码路径为 `/var/tmp`（也可以使用其他路径）。
- 安装在 Red Hat Linux 6.1 和 6.2 上进行了测试。
- 安装的所有步骤都将使用超级用户账户 `root` 执行。
- IMAP 版本号为 `4.7c`。

### 软件包

- IMAP/POP 主页：`http://www.washington.edu/imap/`
- IMAP/POP FTP 站点：`140.142.3.227` 或 `140.142.4.227`
- 你必须确保下载：`imap.tar.Z`

### 前置条件

- 你的系统上应该已经安装了 Sendmail 服务器，才能使用 IMAP 和 POP 软件。

**注意**：有关所需软件的更多信息，请参阅本书中的相关章节。

## Tarballs

在安装 Imap 之前，最好先列出系统上的文件清单，安装后再列一份，然后使用 `diff` 比较，找出软件将文件放置到了何处。只需在安装前运行 `find / > Imap1`，安装后运行 `find / > Imap2`，然后使用 `diff Imap1 Imap2 > Imap-Installed` 即可获得更改内容的列表。

## 编译

解压 tarball（`tar.Z`）。

```bash
[root@deep /]# cp imap.tar.Z /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzf imap.tar.Z
```

## 编译与优化

进入新的 IMAP/POP 目录，然后在终端中输入以下命令。

### 步骤 1

编辑 `Makefile` 文件（`vi +719 src/osdep/unix/Makefile`）并修改以下行：

```make
sh -c '(test -f /usr/include/sys/statvfs.h -a $(OS) != sc5 -a $(OS) != sco) && $(LN) flocksun.c flockbsd.c || $(LN) flocksv4.c flockbsd.c'
```

改为：

```make
sh -c '(test -f /usr/include/sys/statvfs.h -a $(OS) != sc5 -a $(OS) != sco -a $(OS) != lnx) && $(LN) flocksun.c flockbsd.c || $(LN) flocksv4.c flockbsd.c'
```

此修改将更改 `sys/statvfs` 文件。该文件在 Linux 的新版 glibc 2.1 中与 Sun 上的版本不同。

编辑 `Makefile` 文件（`vi +354 src/osdep/unix/Makefile`）并修改以下行：

```make
BASECFLAGS="-g -fno-omit-frame-pointer -O6 -DNFSKLUDGE" \
```

改为：

```make
BASECFLAGS="-g -fno-omit-frame-pointer -O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions -DNFSKLUDGE" \
```

这些是我们用于在服务器上编译 IMAP/POP 软件的优化标志。

编辑 `Makefile` 文件（`vi +61 src/osdep/unix/Makefile`）并修改以下行：

```make
ACTIVEFILE=/usr/lib/news/active
```

改为：

```make
ACTIVEFILE=/var/lib/news/active
```

```make
SPOOLDIR=/usr/spool
```

改为：

```make
SPOOLDIR=/var/spool
```

```make
RSHPATH=/usr/ucb/rsh
```

改为：

```make
RSHPATH=/usr/bin/rsh
```

```make
LOCKPGM=/etc/mlock
```

改为：

```make
#LOCKPGM=/etc/mlock
```

`ACTIVEFILE=` 行指定了 IMAP/POP 的 `active` 目录路径，`SPOOLDIR=` 是 Linux IMAP/POP 的 `spool` 目录所在位置，`RSHPATH=` 指定了系统中 `rsh` 目录的路径。需要注意的是，我们的服务器上不使用 `rsh` 服务，但即便如此，我们仍需将正确的目录指定给 `rsh`。

编辑 `Makefile` 文件（`vi +89 src/osdep/unix/Makefile`）并修改以下行：

```make
CC=cc
```

改为：

```make
CC=egcs
```

此行表示我们将用于编译 IMAP/POP 软件的 GCC 编译器名称，在我们的例子中是 egcs。

### 步骤 2

现在，我们必须编译并在邮件服务器上安装 IMAP 和 POP：

```bash
[root@deep imap-4.7c]# make lnp

[root@deep imap-4.7c]# install -m 644 ./src/ipopd/ipopd.8c /usr/man/man8/ipopd.8c
[root@deep imap-4.7c]# install -m 644 ./src/imapd/imapd.8c /usr/man/man8/imapd.8c
[root@deep imap-4.7c]# install -s -m 755 ./ipopd/ipop2d /usr/sbin
[root@deep imap-4.7c]# install -s -m 755 ./ipopd/ipop3d /usr/sbin
[root@deep im confuse-4.7c]# install -s -m 755 ./imapd/imapd /usr/sbin
[root@deep imap-4.7c]# install -m 644 ./c-client/c-client.a /usr/lib
[root@deep imap-4.7c]# ln -fs /usr/lib/c-client.a /usr/lib/libimap.a
[root@deep imap-4.7c]# mkdir -p /usr/include/imap
[root@deep imap-4.7c]# install -m 644 ./c-client/*.h /usr/include/imap
[root@deep imap-4.7c]# install -m 644 ./src/osdep/tops-20/shortsym.h /usr/include/imap
[root@deep imap-4.7c]# chown root.mail /usr/sbin/ipop2d
[root@deep imap-4.7c]# chown root.mail /usr/sbin/ipop3d
[root@deep imap-4.7c]# chown root.mail /usr/sbin/imapd
```

上述命令将配置软件，确保你的系统具有成功编译软件包所需的功能和库，将所有源文件编译为可执行二进制文件，然后将二进制文件及任何支持文件安装到适当的位置。

请注意，上述 `make lnp` 命令将使用可插拔认证模块（PAM）功能配置你的 Linux 系统，以提高安全性。

`mkdir` 命令将在 `/usr/include` 下创建名为 `imap` 的新目录。这个新目录 `imap` 将保存与 `imapd` 程序相关的所有头文件 `c-client/*` 和 `shortsym.h` 文件。

`chown` 命令将更改二进制程序 `ipop2d`、`ipop3d` 和 `imapd` 的所有权，使其所有者为超级用户 `root`，组所有者为用户 `mail`。



`ln -fs`命令将创建从`c-client.a`文件到`libimap.a`链接的符号链接，这可能会在你将来安装的某些第三方程序中被用到。

**注意**：出于安全考虑，如果您仅使用`imapd`服务，请从邮件服务器中移除`ipop2d`和`ipop3d`二进制文件。对于`ipopd`也同样适用；如果您仅使用`ipopd`服务，请从邮件服务器中移除`imapd`二进制文件。如果您打算同时使用`imapd`和`ipopd`服务，则请保留这两个二进制文件。

## 工作完成后进行清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf imap-version/ imap.tar.Z
```

如上所使用的`rm`命令将删除我们用于编译和安装 IMAP/POP 的所有源文件。它也会从`/var/tmp`目录中删除 IMAP/POP 压缩归档文件。

## 配置

我们在本书中描述的所有软件，在一个名为`floppy.tgz`的 tar 压缩归档文件中都有特定的目录和子目录，其中包含特定程序的文件配置。如果您获取了这个归档文件，您就不必手动复制或粘贴下面不同的配置文件来创建您的配置文件。无论您是决定手动复制它们，还是从归档文件中为您方便地获取这些文件，您都有责任根据需要修改和调整它们，并将与 IMAP/POP 软件相关的文件放置到服务器上的适当位置，如下所示。服务器配置文件归档文件的下载地址位于以下互联网地址：[http://www.openna.com/books/floppy.tgz](http://www.openna.com/books/floppy.tgz)

- 要运行 IMAP/POP 服务器，需要以下文件，并且必须创建或复制到服务器上的相应目录。
- 如果您打算使用`imapd`服务，请将`imap`文件复制到`/etc/pam.d/`目录。
- 如果您打算使用`popd`服务，请将`pop`文件复制到`/etc/pam.d/`目录。

您可以在我们的`floppy.tgz`归档文件中获取下面列出的配置文件。将以下文件从解压后的`floppy.tgz`归档文件复制到适当的位置，或者直接从本书复制并粘贴到相关文件中。

## 配置`/etc/pam.d/imap`文件

配置您的`/etc/pam.d/imap`文件以使用 PAM 认证。

创建`imap`文件（`touch /etc/pam.d/imap`）并添加：

```text
#%PAM-1.0
auth        required   /lib/security/pam_pwdb.so shadow nullok
account     required   /lib/security/pam_pwdb.so
```

**注意**：仅当您打算使用 IMAP 服务时才需要此文件。

## 配置`/etc/pam.d/pop`文件

配置您的`/etc/pam.d/pop`文件以使用 PAM 认证。

创建`pop`文件（`touch /etc/pam.d/pop`）并添加：

```text
#%PAM-1.0
auth        required   /lib/security/pam_pwdb.so shadow nullok
account     required   /lib/security/pam_pwdb.so
```

**注意：** 仅当您打算使用 POP 服务时才需要此文件。

## 通过 tcp-wrappers inetd 超级服务器启用 IMAP 或 POP

Tcp-wrappers 负责启动和停止 IMAP 或 POP 服务器。执行时，`inetd`从配置文件中读取其配置信息，默认情况下该文件是`/etc/inetd.conf`。配置文件的每个字段都必须有一个条目，每个字段的条目之间用制表符或空格分隔。

### 步骤 1

编辑`inetd.conf`文件（`vi /etc/inetd.conf`）并添加或取消注释与您要启用的服务相关的行。如果您想使用 IMAP，则取消注释与其相关的行；如果您想在服务器上使用 POP，则取消注释 POP 的行而不是 IMAP 的行。在下面的示例中，我们将使用 IMAP 服务。

```text
#pop-2 stream tcp nowait root /usr/sbin/tcpd ipop2d
#pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
imap stream tcp nowait root /usr/sbin/tcpd imapd
```

添加或取消注释相应行后，请不要忘记通过发送 SIGHUP 信号（`killall -HUP inetd`）来更新您的`inetd.conf`文件。

- 要更新您的`inetd.conf`文件，请使用以下命令：

  ```bash
  [root@deep /root]# killall -HUP inetd
  ```

### 步骤 2

如果您想安装的 IMAP/POP 服务器是一个私有的、有限制的服务器，仅允许知道真实 IP 地址的 wheel 组用户连接，您可以使用 tcp-wrappers 的安全特性来控制谁可以连接到您的服务器以及从哪里连接。例如，如果您打算向拨号客户端提供邮件服务或提供 Webmail 服务，那么您就不能使用此功能。

编辑`hosts.deny`文件（`vi /etc/hosts.deny`）并添加行：

`ALL: ALL@ALL, PARANOID`

这表示所有服务、所有位置，因此任何未明确允许的服务都将被阻止，除非它们在`hosts.allow`文件中被允许访问。

编辑`hosts.allow`文件（`vi /etc/hosts.allow`）并添加行：

```text
imapd: 216.209.228.34 my.domain.com
```

这表示仅允许客户端 IP`216.209.228.34`和主机名`my.domain.com`连接并使用服务器上的 IMAP 服务。

## 确保 IMAP/POP 安全

### 您真的需要 IMAP/POP 服务吗？

请注意，IMAP/POP 程序默认使用明文密码。任何在网络路径上运行嗅探程序的人都可以获取您的用户名/密码，并使用它们以您的身份登录。这并非因为您在 LINUX 系统上使用了 IMAP/POP 邮件阅读器，您才需要在本地运行 IMAP/POP 服务器。请检查您的配置，如果您使用的是远程/外部 IMAP/POP 服务器，那么请卸载您系统上的 IMAP/POP。

## 服务器软件（邮件网络服务）

## 第 5 章

## 在 IMAP/POP 上使用 SSL 功能

遗憾的是，由于美国政府的出口限制，具有 SSL 功能的 IMAP 工具包目前不可用。有一些来自第三方的软件包允许通过 SSL 进行 IMAP 和 POP3 会话。其中一个软件包是 WebMail IMP，这是一个 Web 界面，允许您通过互联网使用 Web 浏览器读取邮件。WebMail IMP 使用 SSL 协议加密与 IMAP/POP 服务器的通信。有关此主题的更多信息，请参见第 19 章“服务器软件（Web 网络服务）”中的第四部分“软件相关参考”。

使用 WebMail IMP，从邮件服务器到客户端计算机的通信使用 SSL 协议通过 Web 浏览器进行加密。

## 更多文档

更多详细信息，您可以阅读几个手册页：

```text
$ man imapd (8C)
$ man ipopd (8C)
```

Internet 消息访问协议服务器

邮局协议服务器

## 已安装文件

- `/etc/pam.d/imap`
- `/etc/pam.d/pop`
- `/usr/include/imap`
- `/usr/include/imap/dummy.h`
- `/usr/include/imap/env.h`
- `/usr/include/imap/env_unix.h`
- `/usr/include/imap/fdstring.h`
- `/usr/include/imap/flstring.h`
- `/usr/include/imap/fs.h`
- `/usr/include/imap/ftl.h`
- `/usr/include/imap/imap4r1.h`
- `/usr/include/imap/linkage.h`
- `/usr/include/imap/lockfix.h`
- `/usr/include/imap/mail.h`
- `/usr/include/imap/mbox.h`
- `/usr/include/imap/mbx.h`
- `/usr/include/imap/mh.h`
- `/usr/include/imap/misc.h`
- `/usr/include/imap/mmdf.h`
- `/usr/include/imap/mtx.h`
- `/usr/include/imap/mx.h`
- `/usr/include/imap/netmsg.h`
- `/usr/include/imap/news.h`
- `/usr/include/imap/newsrc.h`
- `/usr/include/imap/nl.h`
- `/usr/include/imap/nntp.h`
- `/usr/include/imap/os_a32.h`
- `/usr/include/imap/os_a41.h`
- `/usr/include/imap/os_aix.h`
- `/usr/include/imap/os_aos.h`
- `/usr/include/imap/os_art.h`
- `/usr/include/imap/os_asv.h`
- `/usr/include/imap/os_aux.h`
- `/usr/include/imap/os_bsd.h`
- `/usr/include/imap/os_bsi.h`
- `/usr/include/imap/os_cvx.h`
- `/usr/include/imap/os_d-g.h`
- `/usr/include/imap/os_do4.h`
- `/usr/include/imap/os_drs.h`
- `/usr/include/imap/os_dyn.h`
- `/usr/include/imap/os_hpp.h`
- `/usr/include/imap/os_isc.h`
- `/usr/include/imap/os_lnx.h`
- `/usr/include/imap/os_lyn.h`
- `/usr/include/imap/os_mct.h`
- `/usr/include/imap/os_mnt.h`
- `/usr/include/imap/os_nxt.h`
- `/usr/include/imap/os_os4.h`
- `/usr/include/imap/os_osf.h`
- `/usr/include/imap/os_ptx.h`
- `/usr/include/imap/os_pyr.h`
- `/usr/include/imap/os_qnx.h`
- `/usr/include/imap/os_s40.h`
- `/usr/include/imap/os_sc5.h`
- `/usr/include/imap/os_sco.h`
- `/usr/include/imap/os_sgi.h`
- `/usr/include/imap/os_shp.h`
- `/usr/include/imap/os_slx.h`
- `/usr/include/imap/os_sol.h`
- `/usr/include/imap/os_sos.h`
- `/usr/include/imap/os_sun.h`
- `/usr/include/imap/os_sv2.h`
- `/usr/include/imap/os_sv4.h`
- `/usr/include/imap/os_ult.h`
- `/usr/include/imap/os_vu2.h`
- `/usr/include/imap/osdep.h`
- `/usr/include/imap/phile.h`
- `/usr/include/imap/pop3.h`
- `/usr/include/imap/pseudo.h`
- `/usr/include/imap/rfc822.h`
- `/usr/include/imap/smtp.h`
- `/usr/include/imap/tcp.h`
- `/usr/include/imap/tcp_unix.h`
- `/usr/include/imap/tenex.h`
- `/usr/include/imap/unix.h`
- `/usr/include/imap/utf8.h`
- `/usr/include/imap/shortsym.h`
- `/usr/lib/c-client.a`
- `/usr/lib/libimap.a`
- `/usr/man/man8/ipopd.8c`
- `/usr/man/man8/imapd.8c`
- `/usr/sbin/ipop2d`
- `/usr/sbin/ipop3d`
- `/usr/sbin/imapd`

# 第 16 章：服务器软件（加密网络服务）

## 本章内容

- Linux OpenSSL 服务器
  - 配置
  - 保护 OpenSSL
  - 命令
- Linux FreeS/WAN VPN
  - 配置
  - 配置 RSA 私钥机密
  - IPSec 所需的网络设置
  - 测试安装

## Linux OpenSSL 服务器

### 概述

大多数服务器软件（如 IMAP & POP、Samba、OpenLDAP、FTP、Apache 等）在允许服务之前会要求用户进行身份验证，但默认情况下以明文传输用户的身份标识和密码。相比之下，SSL 等加密机制可确保交易安全。借助该技术，网络上传输的数据会被点对点加密。在 Linux 服务器上安装 OpenSSL 后，你可以将其作为第三方工具，为其他应用程序启用 SSL 功能。

正如 OpenSSL 官方网站所述：

> OpenSSL 项目是一项协作努力，旨在开发一个健壮、商业级、功能齐全的开源工具包，实现安全套接层（SSL v2/v3）和传输层安全（TLS v1）协议，并配备高强度加密。该项目由全球志愿者社区管理，他们通过互联网进行沟通、规划和开发 OpenSSL 工具包及其相关文档。

### 加密技术概要

#### 加密优势

使用加密技术的主要优势如下：

#### 数据机密性

当消息被加密时，输入的明文会通过算法转换为密文，从而隐藏消息的含义，并可以通过任何公共机制发送。此过程涉及一个密钥，用于加密和随后的解密数据。没有密钥，加密的数据毫无意义。

#### 数据完整性

可计算任意用户提供的文本的加密校验和（称为消息认证码 MAC），以保护数据完整性。结果（文本和 MAC）随后发送给接收方，接收方可以通过使用适当的密钥重新计算消息的消息认证码，并验证其恰好等于试验性消息认证码，从而验证附加在消息上的试验性消息认证码。

#### 身份认证

个人身份识别是加密的另一用途，用户/发送方掌握一个密钥，可用以验证其身份。

#### 电子签名

数字签名向发送方和接收方保证消息是真实的，并且只有密钥所有者才能生成该数字签名。

#### 专利

SSL 技术存在一些法律问题。如果你打算将 OpenSSL 用于商业目的，可能需要从 RSA 获得关于使用 RSA 库的许可。

以下是 OpenSSL 自述文件中的摘录：

世界各地的不同公司在不同地点持有各种算法的各种专利。你有责任确保你对任何算法的使用的合法性，方法是检查你所在国家是否存在任何专利。本文件包含我们已知或据传存在的一些专利。这不是一份详尽的列表。

RSA 数据安全公司对 RSA 和 RC5 算法拥有软件专利。如果在美国（和日本？）内部使用其密码，必须联系 RSA 数据安全公司了解许可条件。其网页是`http://www.rsa.com/`。

RC4 是 RSA 数据安全公司的商标，因此使用该标签可能需要获得 RSA 数据安全公司的许可。

IDEA 算法由 Ascom 在奥地利、法国、德国、意大利、日本、荷兰、西班牙、瑞典、瑞士、英国和美国获得专利。如果使用该算法，应联系他们；其网页是`http://www.ascom.ch/`。

#### 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为`/var/tmp`（其他路径亦可）。
- 安装已在 Red Hat Linux 6.1 和 6.2 上测试。
- 安装的所有步骤均在超级用户账户`root`下执行。
- OpenSSL 版本号为`0.9.5a`。

#### Tar 压缩包

在安装 OpenSSL 之前，最好列出系统上的文件清单，安装后再列一份，然后使用`diff`比较它们，以找出软件将文件放置到了何处。只需在安装前运行`find / > OpenSSL1`，安装后运行`find / > OpenSSL2`，然后使用`diff OpenSSL1 OpenSSL2 > OpenSSL-Installed`即可获取变更列表。

#### 软件包

OpenSSL 主页：`http://www.openssl.org/`

你必须确保下载：`openssl-0.9.5a.tar.gz`

#### 编译

解压 tarball（tar.gz）。

```bash
[root@deep /]# cp openssl-version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
```

```bash
[root@deep tmp]# tar xzpf openssl-version.tar.gz
```

#### 编译与优化

进入新的 OpenSSL 目录，在终端中输入以下命令：

**步骤 1**

编辑`c_rehash`文件（`vi +11 tools/c_rehash`），修改以下行：

```bash
DIR=/usr/local/ssl
```

改为：

```bash
DIR=/usr
```

上述修改后的行将在默认位置`/usr`构建和安装 OpenSSL。

**步骤 2**



默认情况下，OpenSSL 源文件假设你的 Perl 程序目录位于`/usr/local/bin/perl`目录下。我们必须修改所有依赖 Perl 的脚本中的`#!/usr/local/bin/perl`行，以反映我们在 Red Hat Linux 下的 Perl 目录`/usr/bin`。

`[root@deep openssl-0.9.5a]# perl util/perlpath.pl /usr/bin`（你的 Perl 程序所在位置）。

### 步骤 3

OpenSSL 必须知道在哪里找到必要的 OpenSSL 源代码库，以便成功编译其所需文件。使用下面的命令，我们将`PATH`环境变量设置为我们解压 OpenSSL 源文件的默认目录。

```
[root@deep openssl-0.9.5a]# export LD_LIBRARY_PATH=`pwd`
```

### 步骤 4

现在，我们必须为系统配置 OpenSSL：

```
CC="egcs" \
./Configure linux-elf -DSSL_FORBID_ENULL \
--prefix=/usr \
--openssldir=/etc/ssl
```

**注意：**`-DSSL_FORBID_ENULL`选项是为了安全原因禁止空加密所必需的。

### 步骤 5

编辑`Makefile.ssl`文件（`vi +50 Makefile.ssl`），修改以下行：

```
CC= gcc
```

改为：

```
CC= egcs
```

编辑`Makefile.ssl`文件（`vi +52 Makefile.ssl`），添加或修改以下行：

```
CFLAG= -DTHREADS -D_REENTRANT -DSSL_FORBID_ENULL -DL_ENDIAN -DTERMIO -O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions -Wall -DSHA1_ASM -DMD5_ASM -DRMD160_ASM
```

编辑`Makefile.ssl`文件（`vi +79 Makefile.ssl`），为 Pentium Pro 处理器添加以下值：

```
PROCESSOR= 686
```

**注意：**我们在上面进行的三项修改将为服务器上 OpenSSL 软件的编译设置优化标志。对于上面的最后一项修改（`PROCESSOR=`），如果你使用的是 Pentium，填写：586；Pentium Pro/II/III，填写：686；486，填写：486。

### 步骤 6

编辑`Makefile.ssl`文件（`vi +161 Makefile.ssl`），修改以下行：

```
MANDIR=$(OPENSSLLDIR)/man
```

改为：

```
MANDIR=/usr/man
```

此步骤用于设置 OpenSSL 手册页的安装目录。通过此修改，我们将它们安装在`/usr/man`目录下。

### 步骤 7

现在，我们必须在服务器上编译和安装 OpenSSL：

```
[root@deep openssl-0.9.5a]# make -f Makefile
[root@deep openssl-0.9.5a]# make test
[root@deep openssl-0.9.5a]# make install
[root@deep openssl-0.9.5a]# mv /etc/ssl/misc/* /usr/bin售
[root@deep openssl-0.9.5a]# rm -rf /etc/ssl/misc/
[root@deep openssl-0.9.5a]# rm -rf /etc/ssl/lib/
[root@deep openssl-0.9.5a]# rm -f /usr/bin/CA.pl
[root@deep openssl-0.9.5a]# rm -f /usr/bin/CA.sh
[root@deep openssl-0.9.5a]# install -m 644 libRSAglue.a /usr/lib/
[root@deep openssl-0.9.5a]# install -m 644 rsaref/rsaref.h /usr/include/openssl/
[root@deep openssl-0.9.5a]# strip /usr/bin/openssl
[root@deep openssl-0.9.5a]# mkdir -p /etc/ssl/crl
```

`make -f`命令将构建 OpenSSL 库（`libcrypto.a`和`libssl.a`）以及 OpenSSL 二进制文件`openssl`。库文件将在顶层目录中构建，二进制文件将在`apps`目录中。

成功构建后，`make test`将测试库，最后`make install`将创建安装目录并安装 OpenSSL。

`mv`命令将`/etc/ssl/misc/`目录下的所有文件移动到`/usr/bin/`目录。这些文件是二进制文件，必须位于`/usr/bin`下，因为在我们的系统中，所有二进制文件都保存在此目录中。此外，将这些文件放在`/usr/bin/`目录中将使它们保留在我们的`PATH`环境变量中。

`rm`命令将从我们的系统中删除`/etc/ssl/misc/`和`/etc/ssl/lib/`目录，因为这些目录中的文件现在已位于其他位置。此外，它还会删除`CA.pl`和`CA.sh`文件，这些是使用的小脚本，用于创建你自己的 CA 证书。这些与`openssl ca`命令相关的脚本有一些奇怪的要求，且默认的 OpenSSL 配置不允许人们轻松地直接使用`openssl ca`。因此，我们稍后将创建`sign.sh`脚本程序来替代它们。

**注意：**您的 Linux 服务器上必须已经安装`bc-1.05a-4.i386.rpm`包或更高版本，否则在进行 OpenSSL 的库测试时您将收到一条错误信息。

## 工作后的清理

```
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf openssl-version/ openssl-version.tar.gz
```

`rm`命令将删除我们用于编译和安装 OpenSSL 的所有源文件。它还将从`/var/tmp`目录中删除 OpenSSL 的压缩归档文件。

## 配置

本书中描述的所有软件都在一个名为`floppy.tgz`的压缩归档文件中具有特定的目录和子目录，其中包含特定程序的文件配置。如果您获取了此归档文件，您将不必手动复现下面不同的配置文件，或者通过剪切粘贴来创建您的配置文件。无论您决定手动复制它们，还是从归档中获取为您准备好的文件，您都有责任修改、调整以满足您的需求，并将与 OpenSSL 软件相关的文件放置到服务器上的适当位置，如下所示。可供下载的服务器配置文件归档位于以下互联网地址：<http://www.openna.com/books/floppy.tgz>

- 要运行 OpenSSL 服务器，以下文件是必需的，必须创建或复制到您服务器上的适当目录中。
- 将`openssl.cnf`文件复制到`/etc/ssl/`目录。
- 将`sign.sh`脚本文件复制到`/usr/bin/`目录。

您可以在我们的`floppy.tgz`归档中获取下面列出的配置文件。从解压后的`floppy.tgz`归档中将以下文件复制到适当的位置，或者直接从本书中复制粘贴到相关文件中。

## `/etc/ssl/openssl.cnf`文件的配置

这是 OpenSSL 程序的通用配置文件，您可以在其中配置密钥的有效期、您的组织名称、地址等。您可能需要更改的参数将在`[ CA_default ]`部分，尤其是`[ req_distinguished_name ]`部分中。

编辑`openssl.cnf`文件（`vi /etc/ssl/openssl.cnf`）并添加或修改：

```ini
# OpenSSL 示例配置文件。
# 该文件主要用于生成证书请求。
#

RANDFILE                = $ENV::HOME/.rnd wound
oid_file                = $ENV::HOME/.oid
oid_section             = new_oids

# 要将此配置文件与
# "openssl x509" 工具的 "-extfile" 选项一起使用，请在此处命名包含要使用的
# X.509v3 扩展的节：
# extensions            =
# （或者，使用一个仅在主 [= default] 节中包含
# X.509v3 扩展的配置文件。）

[ new_oids ]

# 我们可以在此处添加新的 OID，供 'ca' 和 'req' 使用。
# 像这样添加一个简单的 OID：
# testoid1=1.2.3.4
# 或者使用这样的配置文件替换：
# testoid2=${testoid1}.5.6

############################################################
[ ca ]
default_ca    = CA_default           # 默认的 ca 节

############################################################
[ CA_default ]

dir           = /etc/ssl             # 所有内容的存放位置
certs         = $dir/certs           # 已颁发证书的存放位置
crl_dir       = $dir/crl             # 已颁发 crl 的存放位置
database      = $dir/ca.db.index     # 数据库索引文件
new_certs_dir = $dir/ca.db.certs     # 新证书的默认存放位置

certificate   = $dir/certs/ca.crt    # CA 证书
serial        = $dir/ca.db.serial    # 当前序列号
crl           = $dir/crl.pem         # 当前 CRL
private_key   = $dir/private/ca.key  # 私钥
RANDFILE      = $dir/ca.db.rand      # 私钥随机数文件

x509_extensions = usr_cert           # 要添加到证书的扩展

# 要添加到 CRL 的扩展。注意：Netscape 通信器在处理 V2 CRL 时会崩溃，
# 因此默认情况下将其注释掉以保留 V1 CRL。
# crl_extensions = crl_ext

default_days    = 365                  # 认证有效期时长
default_crl_days = 30                  # 下一个 CRL 之前的时长
default_md      = md5                  # 使用的 md
Preserve        = no                   # 保持传递的 DN 顺序

# 几种不同的方式指定请求应该看起来多么相似
# 对于类型 CA，列出的属性必须相同，而可选
# 和提供的字段就是这样 :-)
policy          = policy_match

# CA 策略
[ policy_match ]
countryName             = match
stateOrProvinceName     = match
organizationName        = match
organizationalUnitName  = optional
commonName              = supplied
emailAddress            = optional

# "anything" 策略
# 目前，您必须列出所有可接受的 "对象"
# 类型。
[ policy_anything ]
countryName             = optional
stateOrProvinceName     = optional
localityName            = optional
organizationName        = optional
organizationalUnitName  = optional
commonName              = supplied
emailAddress            = optional

############################################################
[ req ]

default_bits                          = 1024
default_keyfile                       = privkey.pem
distinguished_name                    = req_distinguished_name
attributes                            = req_attributes
x509_extensions = v3_ca # 要添加到自签名证书的扩展
```

### `[ req_distinguished_name ]`

```ini
countryName                           = 国家名称 (2 字母代码)
countryName_default                   = CA
countryName_min                       = 2
countryName_max                       = 2

stateOrProvinceName                   = 州或省份名称 (全名)
stateOrProvinceName_default           = Quebec

localityName                          = 地方名称 (例如，城市)
localityName_default                  = Montreal

0.organizationName                    = 组织名称 (例如，公司)
0.organizationName_default            = Open Network Architecture

# 我们可以这样做，但通常不需要 :-)
#1.organizationName                   = 第二组织名称 (例如，公司)
#1.organizationName_default            = World Wide Web Pty Ltd

organizationalUnitName                = 组织单位名称 (例如，部门)
organizationalUnitName_default        = Internet Department

commonName                            = 通用名称 (例如，您的姓名)
commonName_default                    = www.openna.com
commonName_max                        = 64

emailAddress                          = 电子邮件地址
emailAddress_default                  = admin@openna.com
emailAddress_max                      = 40

# SET-ex3                             = SET 扩展编号 3
```

### `[ req_attributes ]`

```ini
challengePassword                     = 挑战密码
challengePassword_min                 = 4
challengePassword_max                 = 20

unstructuredName                      = 可选的公司名称
```

### `[ usr_cert ]`

当`ca`签署请求时，这些扩展将被添加。

这违反了 PKIX 指南，但一些 CA 这样做，而且某些软件需要这样做以避免将最终用户证书解释为 CA。

```ini
basicConstraints=CA:FALSE
```

以下是`nsCertType`用法的示例。如果省略它，证书可以用于除对象签名之外的任何用途。这对于 SSL 服务器来说是可以的。

```ini
# nsCertType    = server
```

对于对象签名证书，将使用此项。

```ini
# nsCertType = objsign
```

对于正常的客户端使用，这是典型的：

```ini
# nsCertType = client, email
```

以及用于包括对象签名在内的所有用途：

```ini
# nsCertType = client, email, objsign
```

这是客户端证书中`keyUsage`的典型用法。

```ini
# keyUsage = nonRepudiation, digitalSignature, keyEncipherment
```

这将显示在 Netscape 的注释列表框中。



```ini
nsComment            = "OpenSSL Generated Certificate"

# PKIX 建议在所有证书中包含无害。

subjectKeyIdentifier=hash

authorityKeyIdentifier=keyid,issuer:always

# 这些内容用于 subjectAltName 和 issuerAltname。

# 导入电子邮件地址。

# subjectAltName=email:copy

# 复制主体详细信息

# issuerAltName=issuer:copy

#nsCaRevocationUrl    = http://www.domain.dom/ca-crl.pem

#nsBaseUrl

#nsRevocationUrl

#nsRenewalUrl

#nsCaPolicyUrl

#nsSslServerName

[ v3_ca ]

# 典型 CA 的扩展

# PKIX 建议。

subjectKeyIdentifier=hash

authorityKeyIdentifier=keyid:always,issuer:always

# 这是 PKIX 的建议，但某些有缺陷的软件会对关键

# 扩展产生问题。

#basicConstraints = critical,CA:true

# 因此我们用这个代替。

basicConstraints = CA:true

# 密钥用法：这是典型 CA 证书的用法。然而由于它

# 会阻止其用作测试自签名证书，因此最好

# 默认情况下将其留空。

# keyUsage = cRLSign, keyCertSign

# 有些人可能还想要这个

# nsCertType = sslCA, emailCA

# 在主体备用名称中包含电子邮件地址：另一个 PKIX 建议

# subjectAltName=email:copy

# 复制颁发者详细信息

# issuerAltName=issuer:copy

# 扩展的原始 DER 十六进制编码：仅供专家注意！

# 1.2.3.5=RAW:02:03

# You can even override a supported extension:

# basicConstraints= critical, RAW:30:03:01:01:FF

[ crl_ext ]

# CRL extensions.

# Only issuerAltName and authorityKeyIdentifier make any sense in a CRL.

# issuerAltName=issuer:copy

authorityKeyIdentifier=keyid:always,issuer:always
```

**注意：** 文件`openssl.cnf`在编译并安装 OpenSSL 程序时已经存在于您的服务器上，可以在`/etc/ssl/`目录下找到。您不需要更改此文件中设置的所有默认选项；通常需要更改的配置仅在`[ CA_default ]`和`[ req_distinguished_name ]`这两个部分中。

## 创建`/usr/bin/sign.sh`程序文件

`openssl ca`命令有一些特殊的要求，而默认的 OpenSSL 配置不允许直接方便地使用`openssl ca`。因此，我们将创建这个`sign.sh`程序来替代它。

创建`sign.sh`程序文件（`touch /usr/bin/sign.sh`），并向该文件中添加以下内容：

```sh
#!/bin/sh

##
## sign.sh -- Sign a SSL Certificate Request (CSR)
## Copyright (c) 1998-1999 Ralf S. Engelschall, All Rights Reserved.
##

# argument line handling

CSR=$1

if [ $# -ne 1 ]; then
  echo "Usage: sign.sh <whatever>.csr"; exit 1
fi

if [ ! -f $CSR ]; then
  echo "CSR not found: $CSR"; exit 1
fi

case $CSR in
  *.csr ) CERT="`echo $CSR | sed -e 's/\\.csr/.crt/'`" ;;
  * ) CERT="$CSR.crt" ;;
esac

# make sure environment exists

if [ ! -d ca.db.certs ]; then
  mkdir ca.db.certs
fi

if [ ! -f ca.db.serial ]; then
  echo '01' >ca.db.serial
fi

if [ ! -f ca.db.index ]; then
  cp /dev/null ca.db.index
fi

# create an own SSL config

cat >ca.config <<EOT

[ ca ]

default_ca		= CA_own

[ CA_own ]

dir                        = /etc/ssl

certs                      = /etc/ssl/certs

new_certs_dir              = /etc/ssl/ca.db.certs

database                   = /etc/ssl/ca.db.index

serial                     = /etc/ssl/ca.db.serial

RANDFILE                   = /etc/ssl/ca.db.rand

certificate                = /etc/ssl/certs/ca.crt

private_key                = /etc/ssl/private/ca.key

default_days               = 365

default_crl_days           = 30

default_md                 = md5

preserve                   = no

policy                     = policy_anything

[ policy_anything ]

countryName                = optional

stateOrProvinceName        = optional

localityName               = optional

organizationName           = optional

organizationalUnitName     = optional

commonName                 = supplied

emailAddress               = optional

EOT
```

```sh
# sign the certificate

echo "CA signing: $CSR -> $CERT:"

openssl ca -config ca.config -out $CERT -infiles $CSR

echo "CA verifying: $CERT <-> CA cert"

openssl verify -CAfile /etc/ssl/certs/ca.crt $CERT
```

```sh
# cleanup after SSLeay

rm -f ca.config

rm -f ca.db.serial.old

rm -f ca.db.index.old
```

```sh
# die gracefully

exit 0
```

现在，将此程序设置为可执行，并更改其默认权限：

```sh
[root@deep /]# chmod 755 /usr/bin/sign.sh
```

**注意：** 您也可以在 mod_ssl 发行版的`mod_ssl-version/pkg.contrib/`子目录中找到这个`sign.sh`程序，或者在我们的`floppy.tgz`归档文件中。另请注意，`[ CA_own ]`部分必须根据您自己的环境进行修改，并且不要忘记修改`openssl verify -CAfile /etc/ssl/certs/ca.crt $CERT`这一行。

## 命令

下面列出的命令是我们经常使用的一些，但还有更多命令存在。请查阅 man 手册和文档以获取更多详细信息。

作为示例，我们将向您展示如何为您的 Apache Web 服务器和/或您自己的 CA（认证机构）创建证书，以便自己签署您的“证书签名请求”。

**注意：** 下面列出的所有命令都假设在`/etc/ssl/`目录下执行。

### 1.1 为 Apache 服务器创建一个受密码短语保护的 RSA 私钥

```console
[root@deep ssl]# openssl genrsa -des3 -out server.key 1024

Generating RSA private key, 1024 bit long modulus

   ......................++++++
```

### 1.2 使用服务器 RSA 私钥生成证书签名请求（CSR）

```console
[root@deep ssl]# openssl req -new -key server.key -out server.csr

Using configuration from /etc/ssl/openssl.cnf

Enter PEM pass phrase:

You are about to be asked to enter information that will be incorporated

into your certificate request.

What you are about to enter is what is called a Distinguished Name or a DN.

There are quite a few fields but you can leave some blank

For some fields there will be a default value,

If you enter '.', the field will be left blank.

-----

Country Name (2 letter code) [CA]:

State or Province Name (full name) [Quebec]:

Locality Name (eg, city) [Montreal]:

Organization Name (eg, company) [Open Network Architecture]:

Organizational Unit Name (eg, section) [Internet Department]:

Common Name (eg, YOUR name) [www.openna.com]:

Email Address [admin@openna.com]:

Please enter the following 'extra' attributes

to be sent with your certificate request

A challenge password []:

An optional company name []:
```

注意：当 OpenSSL 提示您输入`CommonName`时，请确保输入服务器的 FQDN（“完全限定域名”）（即，当您为稍后将通过`https://www.mydomain.com/`访问的网站生成 CSR 时，请在此处输入`www.mydomain.com`）。

生成证书签名请求（CSR）后，您有两个选择：第一是将其发送给商业认证机构（CA），如 Verisign 或 Thawte 进行签署。您通常需要将 CSR 提交到网络表单，支付签署费用，等待签名证书，然后将其存储到`server.crt`文件中。结果就是一个真正的证书，可用于 Apache。

第二，您可以使用自己的 CA，现在必须通过这个 CA 自己签署 CSR。这种方案经济实惠，允许组织托管自己的 CA 服务器，并根据需要生成尽可能多的内部使用证书，而无需向商业 CA 支付任何费用。不幸的是，使用自己的 CA 生成证书会在电子商务中造成问题，因为客户需要通过使用受认可的商业 CA 来对您的组织建立一定程度的信任。请参阅下文了解如何使用自己的 CA 签署 CSR。

### 1.3 为您的 CA 创建 RSA 私钥

```console
[root@deep ssl]# openssl genrsa -des3 -out ca.key 1024

Generating RSA private key, 1024 bit long modulus

............................++++++

...........................................++++++

e is 65537 (0x10001)
```

Enter PEM pass phrase: Verifying password - Enter PEM pass phrase:

请备份此`ca.key`文件，并在安全位置记住您输入的密码短语。

### 1.4 使用 CA 的 RSA 密钥创建自签名 CA 证书（x509 结构）

```console
[root@deep ssl]# openssl req -new -x509 -days 365 -key ca.key -out ca.crt

Using configuration from /etc/ssl/openssl.cnf

Enter PEM pass phrase:

You are about to be asked to enter information that will be incorporated

into your certificate request.

What you are about to enter is what is called a Distinguished Name or a DN.

There are quite a few fields but you can leave some blank

For some fields there will be a default value,

If you enter '.', the field will be left blank.

-----

Country Name (2 letter code) [CA]:

State or Province Name (full name) [Quebec]:

Locality Name (eg, city) [Montreal]:

Organization Name (eg, company) [Open Network Architecture]:

Organizational Unit Name (eg, section) [Internet Department]:CA Marketing

Common Name (eg, YOUR name) [www.openna.com]:

Email Address [admin@openna.com]:
```

```console
[root@deep ssl]# mv server.key private/

[root deep ssl]# mv ca.key private/

[root@deep ssl]# mv ca.crt certs/
```

**注意：** 当使用`-x509`选项时，`req`命令创建一个自签名证书。

### 1.5 签署证书请求（我们创建并使用自己的证书颁发机构 CA）

准备签署脚本（这是必需的，因为`openssl ca`命令有一些特殊要求，而默认的 OpenSSL 配置不允许直接方便地使用`openssl ca`）。名为`sign.sh`的脚本随软盘分发，位于 openssl 目录下。使用此脚本进行签署。

现在您可以使用此 CA 签署服务器 CSR，以便为 Apache Web 服务器创建真正的 SSL 证书（假设您手头已有`server.csr`）：

```console
[root@deep ssl]# /usr/bin/sign.sh server.csr

CA signing: server.csr -> server.crt:

Using configuration from ca.config

Enter PEM pass phrase:

Check that the request matches the signature

Signature ok

The Subjects Distinguished Name is as follows

countryName           :PRINTABLE:'CA'

stateOrProvinceName   :PRINTABLE:'Quebec'

localityName          :PRINTABLE:'Montreal'

organizationName      :PRINTABLE:'Open Network Architecture'

organizationalUnitName :PRINTABLE:'Internet Department'

commonName            :PRINTABLE:'www.openna.com'

emailAddress          :IA5STRING:'admin@openna.com'
```



Certificate is to be certified until Dec 1 14:59:29 2000 GMT (365 days)

Sign the certificate? [y/n]:y

```
1 out of 1 certificate requests certified, commit? [y/n]y

Write out database with 1 new entries

Data Base Updated

CA verifying: server.crt <-> CA cert

server.crt: OK
```

这将为 CSR 签名并生成一个`server.crt`文件。

```
[root@deep ssl]# mv server.crt certs/
```

现在你有两个文件：`server.key`和`server.crt`。例如，可以在你的 Apache 服务器的`httpd.conf`文件中这样使用：

```
SSLCertificateFile  /etc/ssl/certs/server.crt ← 我们的 Web 服务器公钥

SSLCertificateKeyFile /etc/ssl/private/server.key ← 我们的 Web 服务器私钥
```

`server.csr`文件不再需要了。

```
[root@deep ssl]# rm -f server.csr
```

**注意：** 如果在签名证书时收到错误消息，很可能是因为你在 OpenSSL 提示输入`CommonName`时输入了错误的 FQDN（"Fully Qualified Domain Name"，完全限定域名）；`CommonName`必须是类似`my.domain.com`的形式，而不是`domain.com`。此外，由于你要同时生成证书和 CA 证书，两个文件之间至少要有一项信息不同，否则在签名证书请求时可能会遇到问题。

## 保护 OpenSSL 安全

将密钥设置为只有超级用户`root`才能"读写"。这很重要，因为不需要其他人接触这些文件。

- 要将密钥设为只有`root`才能"读写"，请使用以下命令：
  - `[root@deep /]# chmod 600 /etc/ssl/certs/ca.crt`
  - `[root@deep /]# chmod 600 /etc/ssl/certs/server.crt`
  - `[root@deep /]# chmod 600 /etc/ssl/private/ca.key`
  - `[root@deep /]# chmod 600 /etc/ssl/private/server.key`

## OpenSSL 软件的一些可能用途

OpenSSL 可以用于：

1. 创建自己的证书服务器。
2. 为用户提供传输过程中的数据保密性、完整性、认证和电子签名。
3. 保护电子商务交易的安全。

## 已安装文件

```text
/etc/ssl
/etc/ssl/crl
/etc/ssl/certs
/etc/ssl/private
/etc/ssl/openssl.cnf
/usr/bin/openssl
/usr/bin/c_rehash
/usr/bin/sign.sh
/usr/man/man1/verify.1
/usr/man/man1/version.1
/usr/man/man1/x509.1
/usr/man/man3/BN_CTX_new.3
/usr/man/man3/BN_CTX_start.3
/usr/man/man3/BN_add.3
/usr/man/man3/BN_add_word.3
/usr/man/man3/BN_bn2bin.3
```

**服务器软件（加密网络服务）1**  
**第6章**

```text
/usr/bin/c_hash
/usr/bin/c_info
/usr/bin/c_issuer
/usr/bin/c_name
/usr/bin/der_chop
/usr/include/openssl
/usr/include/openssl/e_os.h
/usr/include/openssl/e_os2.h
/usr/include/openssl/crypto.h
/usr/include/openssl/tmdiff.h
/usr/include/openssl/opensslv.h
/usr/include/openssl/opensslconf.h
/usr/include/openssl/ebcdic.h
/usr/include/openssl/md2.h
/usr/include/openssl/md5.h
/usr/include/openssl/sha.h
/usr/include/openssl/mdc2.h
/usr/include/openssl/hmac.h
/usr/include/openssl/ripemd.h
/usr/include/openssl/des.h
/usr/include/openssl/rc2.h
/usr/include/openssl/rc4.h
/usr/include/openssl/rc5.h
/usr/include/openssl/idea.h
/usr/include/openssl/blowfish.h
/usr/include/openssl/cast.h
/usr/include/openssl/bn.h
/usr/include/openssl/rsa.h
/usr/include/openssl/dsa.h
/usr/include/openssl/dh.h
/usr/include/openssl/buffer.h
/usr/include/openssl/bio.h
/usr/include/openssl/stack.h
/usr/include/openssl/safestack.h
/usr/include/openssl/lhash.h
/usr/include/openssl/rand.h
/usr/include/openssl/err.h
/usr/include/openssl/objects.h
/usr/include/openssl/evp.h
/usr/include/openssl/asn1.h
/usr/include/openssl/asn1_mac.h
/usr/include/openssl/pem.h
/usr/include/openssl/pem2.h
/usr/include/openssl/x509.h
/usr/include/openssl/x509_vfy.h
/usr/include/openssl/x509v3.h
/usr/include/openssl/conf.h
/usr/include/openssl/txt_db.h
/usr/include/openssl/pkcs7.h
/usr/include/openssl/pkcs12.h
/usr/include/openssl/comp.h
/usr/include/openssl/ssl.h
/usr/include/openssl/ssl2.h
/usr/include/openssl/ssl3.h
/usr/include/openssl/ssl23.h
/usr/include/openssl/tls1.h
/usr/include/openssl/rsaref.h
/usr/lib/libcrypto.a
/usr/lib/libssl.a
/usr/lib/libRSAglue.a
/usr/man/man1/CA.pl.1
/usr/man/man1/asn1parse.1
```

```text
/usr/man/man3/BN_cmp.3
/usr/man/man3/BN_copy.3
/usr/man/man3/BN_generate_prime.3
/usr/man/man3/BN_mod_inverse.3
/usr/man/man3/BN_mod_mul_montgomery.3
/usr/man/man3/BN_mod_mul_reciprocal.3
/usr/man/man3/BN_new.3
/usr/man/man3/BN_num_bytes.3
/usr/man/man3/BN_rand.3
/usr/man/man3/BN_set_bit.3
/usr/man/man3/BN_zero.3
/usr/man/man3/CRYPTO_set_ex_data.3
/usr/man/man3/DH_generate_key.3
/usr/man/man3/DH_generate_parameters.3
/usr/man/man3/DH_get_ex_new_index.3
/usr/man/man3/DH_new.3
/usr/man/man3/DH_set_method.3
/usr/man/man3/DH_size.3
/usr/man/man3/DSA_SIG_new.3
/usr/man/man3/DSA_do_sign.3
/usr/man/man3/DSA_dup_DH.3
/usr/man/man3/DSA_generate_key.3
/usr/man/man3/DSA_generate_parameters.3
/usr/man/man3/DSA_get_ex_new_index.3
/usr/man/man3/DSA_new.3
/usr/man/man3/DSA_set_method.3
/usr/man/man3/DSA_sign.3
/usr/man/man3/DSA_size.3
/usr/man/man3/ERR_GET_LIB.3
/usr/man/man3/ERR_clear_error.3
/usr/man/man3/ERR_error_string.3
/usr/man/man3/ERR_get_error.3
/usr/man/man3/ERR_load_crypto_strings.3
/usr/man/man3/ERR_load_strings.3
/usr/man/man3/INETALLAHp ERR_print_errors.3
/usr/man/man3/ERR_put_error.3
/usr/man/man3/ERR_remove_state.3
/usr/man/man3/EVP_DigestInit.3
/usr/man/man3/EVP_EncryptInit.3
/usr/man/man3/OPENSSL_VERSION_NUMBER.3
/usr/man/man3/OpenSSL_add_all_algorithms.3
/usr/man/man3/RAND_add.3
/usr/man/man3/RAND_bytes.3
/usr/man/man3/RAND_cleanup.3
/usr/man/man3/RAND_egd.3
/usr/man/man3/RAND_load_file.3
/usr/man/man3/RAND_set_rand_method.3
/usr/man/man3/RSA_blinding_on.3
/usr/man/man3/RSA_check_key.3
/usr/man/man3/RSA_generate_key.3
/usr/man/man3/RSA_get_ex_new_index.3
/usr/man/man3/RSA_new.3
/usr/man/man3/RSA_padding_add_PKCS1_type_1.3
/usr/man/man3/RSA_print.3
/usr/man/man3/RSA_private_encrypt.3
/usr/man/man3/RSA_public_encrypt.3
/usr/man/man3/RSA_set_method.3
/usr/man/man3/RSA_sign.3
/usr/man/man3/RSA_sign_ASN1_OCTET_STRING.3
/usr/man/man3/RSA_size.3
/usr/man/man3/blowfish.3
/usr/man/man3/bn.3
```

- `/usr/man/man1/ca.1`
- `/usr/man/man1/ciphers.1`
- `/usr/man/man1/crl.1`
- `/usr/man/man1/crl2pkcs7.1`
- `/usr/man/man1/dgst.1`
- `/usr/man/man1/dhparam.1`
- `/usr/man/man1/dsa.1`
- `/usr/man/man1/dsaparam.1`
- `/usr/man/man1/enc.1`
- `/usr/man/man1/gendsa.1`
- `/usr/man/man1/genrsa.1`
- `/usr/man/man1/nseq.1`
- `/usr/man/man1/openssl.1`
- `/usr/man/man1/pkcs12.1`
- `/usr/man/man1/pkcs7.1`
- `/usr/man/man1/pkcs8.1`
- `/usr/man/man1/req.1`
- `/usr/man/man1/rsa.1`
- `/usr/man/man1/s_client.1`
- `/usr/man/man1/s_server.1`
- `/usr/man/man1/sess_id.1`
- `/usr/man/man1/smime.1`
- `/usr/man/man1/speed.1`
- `/usr/man/man1/spkac.1`

- `/usr/man/man3/bn_internal.3`
- `/usr/man/man3/buffer.3`
- `/usr/man/man3/crypto.3`
- `/usr/man/man3/d2i_DHparams.3`
- `/usr/man/man3/d2i_RSAPublicKey.3`
- `/usr/man/man3/dh.3`
- `/usr/man/man3/dsa.3`
- `/usr/man/man3/err.3`
- `/usr/man/man3/hmac.3`
- `/usr/man/man3/lh_stats.3`
- `/usr/man/man3/lhash.3`
- `/usr/man/man3/md5.3`
- `/usr/man/man3/mdc2.3`
- `/usr/man/man3/rand.3`
- `/usr/man/man3/rc4.3`
- `/usr/man/man3/ripemd.3`
- `/usr/man/man3/rsa.3`
- `/usr/man/man3/sha.3`
- `/usr/man/man3/threads.3`
- `/usr/man/man3/SSL_get_error.3`
- `/usr/man/man3/ssl.3`
- `/usr/man/man5/config.5`
- `/usr/man/man7/des_modes.7`

## Linux FreeS/WAN VPN

### 概述

使用 SSL 解决方案保护客户端到服务器的通信是一个绝佳的选择，但有时对于企业环境而言，建立安全的通信通道，确保两个防火墙之间通过互联网实现完全的隐私、真实性和数据完整性至关重要。为此，IPSEC 应运而生。

IPSEC 即 Internet Protocol SECurity（互联网协议安全）。它使用强大的密码学技术来提供认证和加密服务。认证确保数据包来自正确的发送者，并且在传输过程中未被篡改。加密防止未经授权读取数据包内容。IPSEC 可以保护任何运行在 IP 之上的协议，以及任何使用在 IP 之下的介质。IPSEC 还可以提供某些"后台运行"的安全服务，对用户没有明显的影响。更重要的是，它可以保护通过复杂介质组合运行的多种协议（如 IMAP/POP 等），而无需以任何方式修改它们，因为加密发生在 IP 层面。

IPSEC 服务允许你通过不可信网络构建安全隧道。通过不可信网络的所有内容都由 IPSEC 网关机器加密，并由另一端的网关解密。结果就是虚拟专用网络（VPN）。这是一个实际上私有的网络，尽管它包含了位于不同站点的多台机器，通过不安全的互联网进行连接。

![](img/a3204f208d115df8d5f69e88ecf1a4ea_303_0.png)

### 这些安装说明假定

- 命令与 Unix 兼容。
- 源代码路径为`/usr/src`
- 安装在 Red Hat Linux 6.1 和 6.2 上进行了测试。
- 安装中的所有步骤都将使用超级用户账户`root`执行。
- 内核版本号为`2.2.14`

FreeS/WAN VPN 的版本号为`1.3`

## 软件包

内核主页：<http://www.kernelnotes.org/>

您务必下载：`linux-2_2_14_tar.gz`

FreeS/WAN VPN 主页站点：<http://www.freeswan.org/>

FreeS/WAN VPN FTP 站点：`194.109.6.26`

您务必下载：`freeswan-1.3.tar.gz`

## Tarball 归档文件



在安装 FreeS/WAN 之前，最好先列出系统上的文件清单，安装之后再列一份，然后使用`diff`进行比较，以了解软件将文件安装到了何处。只需在安装软件之前运行`find /** > Freeswan1`，安装之后运行`find /** > Freeswan2`，然后使用`diff Freeswan1 Freeswan2 > Freeswan-Installed`即可获取...参列表。

IPSEC FreeS/WAN 虚拟专用网络软件的安装需要对原始内核进行一些修改，因为 FreeS/WAN 必须先包含并整合到内核中才能使用。因此，安装 FreeS/WAN 软件的第一步是前往本书中的 Linux 内核部分，按照说明在您的系统上安装 Linux 内核（即使您之前已经安装过），并在执行完`make dep; make clean`命令后，但在 Linux 内核部分执行`make bzImage`命令之前，返回到"Linux FreeS/WAN VPN"（本节）。

**注意**：强烈建议如果您打算在系统上安装 FreeS/WAN 软件，就不要使用优化标志编译内核中的任何内容。任何添加到 Linux PERT 内核的优化标志都会导致 FreeS/WAN IPSEC 软件运行时产生错误信息；这是您必须注意的重要警告，否则 FreeS/WAN 将无法正常工作。第 5 章"配置和构建安全、优化的内核"中记录的优化标志可以无问题地应用于本书的所有章节和节，唯独 FreeS/WAN IPSEC 软件例外。我再次强调，在编译和修补 Linux 内核以支持 FreeS/WAN 时，不要使用或添加任何优化选项或标志。

## 编译 FreeS/WAN

解压缩 tarball（`tar.gz`）。

```
[root@deep /]# cp freeswan-version.tar.gz /usr/src/
[root@deep /]# cd /usr/src
[root@deep src]# tar xzpf freeswan-version.tar.gz
[root@deep src]# chown -R 0.0 /usr/src/freeswan-version
```

## 编译并将 FreeS/WAN 插入内核

您必须修改 FreeS/WAN 源码目录下名为`utils`、`klips/utils`、`Pluto`和`lib`的子目录中的`Makefile`，以指定安装路径。我们必须修改这些文件，使其符合 Red Hat 的文件系统结构，并将 FreeS/WAN 文件安装到我们的 PATH 环境变量下。

**步骤 1**

进入新的 FreeS/WAN 发行版的顶级目录，然后在终端中输入以下命令：

编辑`Makefile`文件（`vi Makefile`）并修改以下行：

```
PUBDIR=/usr/local/sbin
改为：
PUBDIR=/usr/sbin

PRIVDIR=/usr/local/lib/ipsec
改为：
PRIVDIR=/usr/lib/ipsec

FINALPRIVDIR=/usr/local/lib/ipsec
改为：
FINALPRIVDIR=/usr/lib/ipsec

MANTREE=/usr/local/man
改为：
MANTREE=/usr/man
```

**步骤 2**

编辑子目录`utils`中的`Makefile`文件（`vi utils/Makefile`）并修改以下行：

```
PUBDIR=/usr/local/sbin
改为：
PUBDIR=/usr/sbin

PRIVDIR=/usr/local/lib/ipsec
改为：
PRIVDIR=/usr/lib/ipsec

FINALPRIVDIR=/usr/local/lib/ipsec
改为：
FINALPRIVDIR=/usr/lib/ipsec

MANTREE=/usr/local/man
改为：
MANTREE=/usr/man
```

**步骤 3**

编辑子目录`klips/utils`中的`Makefile`文件（`vi klips/utils/Makefile`）并修改以下行：

```
BINDIR=/usr/local/lib/ipsec
改为：
BINDIR=/usr/lib/ipsec

MANTREE=/usr/local/man
改为：
MANTREE=/usr/man
```

**步骤 4**

编辑子目录`pluto`中的`Makefile`文件（`vi pluto/Makefile`）并修改以下行：

```
BINDIR=/usr/local/lib/ipsec
改为：
BINDIR=/usr/lib/ipsec

MANTREE=/usr/local/man
改为：
MANTREE=/usr/man
```

**步骤 5**

编辑子目录`lib`中的`Makefile`文件（`vi lib/Makefile`）并修改以下行：

```
MANTREE=/usr/local/man
改为：
MANTREE=/usr/man
```

**步骤 6**

编辑子目录`libdes`中的`Makefile`文件（`vi libdes/Makefile`）并修改以下行：

```
LIBDIR=/usr/local/lib
改为：
LIBDIR=/usr/lib

BINDIR=/usr/local/bin
改为：
BINDIR=/usr/bin

INCDIR=/usr/local/include
改为：
INCDIR=/usr/include

MANDIR=/usr/local/man
改为：
MANDIR=/usr/man
```

从步骤 1 到步骤 6 的上述更改，将把与 FreeS/WAN 软件相关的所有文件定位到我们选择的目标目录中，以符合 Red Hat 文件系统结构。

**步骤 7**

现在，我们必须在服务器上编译并安装 FreeS/WAN：

```
[root@deep freeswan-1.3]# make insert
[root@deep freeswan-1.3]# make programs
[root@deep freeswan-1.3]# make install
```

`make insert`命令创建一个符号链接`/usr/src/linux/net/ipsec`，指向 KLIPS 源码目录。它在必要时修补一些内核文件，使其识别 KLIPS 和/或修复错误。它还将默认配置添加到内核配置文件中，最后，如果尚未存在，则创建 KLIPS 通信文件`/dev/ipsec`。

`make programs`命令构建库、Pluto 和各种用户级工具。`make install`将安装 Pluto 守护进程和用户级工具，并设置开机启动。

## 重新配置并安装支持 FreeS/WAN VPN 的内核

现在，我们必须返回到`/usr/src/linux`目录并执行以下命令，以重新配置启用了 FreeS/WAN 支持的内核：

```
[root@deep freeswan-1.3]# cd /usr/src/linux
[root@deep linux]#  make config
```

**注意**：我们现在使用的`make config`命令与之前的区别在于，现在我们的内核配置中包含了一个新的与 FreeS/WAN 相关的部分，因此我们必须重新配置内核，以自定义 IPSec 选项，使其成为您内核的一部分。

您需要做的第一件事是确保您的内核已启用 FreeS/WAN 支持进行构建。在 2.2.14 内核版本中，按照上述说明使用 FreeS/WAN 程序修补内核后，您的内核配置中应该会出现一个名为"IPSec options (FreeS/WAN)"的与 FreeS/WAN VPN 支持相关的新部分。您需要确保在新部分"IPSec options (FreeS/WAN)"下对以下问题回答 **Y**：

## IPSec 选项 (FreeS/WAN)

- IP 安全协议 (FreeS/WAN IPSEC) (`CONFIG_IPSEC`) [Y/n/?]

- IPSEC: IP-in-IP 封装 (`CONFIG_IPSEC_IPIP`) [Y/n generates /?]

- IPSEC: PF_KEYv2 内核/用户接口 (`CONFIG_IPSEC_PFKEYv2`) [Y/n/?]

- IPSEC: 启用 ICMP PMTU 消息 (`CONFIG_IPSEC_ICMP`) [Y/n/?]

- IPSEC: 认证头 (`CONFIG_IPSEC_AH`) [Y/n/?]

- HMAC-MD5 认证算法 (`CONFIG_IPSEC_AUTH_HMAC_MD5`) [Y/n/?]

- HMAC-SHA1 认证算法 (`CONFIG_IPSEC_AUTH_HMAC_SHA1`) [Y/n/?]

- IPSEC: 封装安全载荷 (`CONFIG_IPSEC_ESP`) [Y/n/?]

- 3DES 加密算法 (`CONFIG_IPSEC_ENC_3DES`) [Y/n/?]

- IPSEC 调试选项 (`DEBUG_IPSEC`) [Y/n/?]

**注意**：您第一次运行`make config`、`make dep`和`make clean`命令时对内核所做的所有自定义设置都将保留，因此您无需重新配置内核的每个部分；只需要配置 FreeS/WAN 添加的新部分"IPSec options (FreeS/WAN)"，如上所示。

一些网络选项将自动启用，即使您之前已将其关闭；这是因为 IPSEC 需要它们。无论您使用哪种配置程序，都应特别注意几个问题：特别是，请勿在内核配置的"Networking Options"下禁用以下任何项：

- 内核/用户 netlink 套接字 (`CONFIG_NETLINK`) [Y/n/?]

- Netlink 设备模拟 (`CONFIG_NETLINK_DEV`) [Y/n/?]

## 编译并安装支持 FreeS/WAN 的新内核

现在我们已将 FreeS/WAN VPN 支持包含到内核中，可以编译并安装新内核了。

- 返回到`/usr/src/linux`目录并再次运行以下命令：

```
[root@deep linux]# make dep; make clean; make bzImage
```

执行上述命令后，按照本书 Linux 内核部分（第 5 章 配置和构建安全、优化的内核）的正常说明安装内核。此时，在复制并安装新内核镜像、`system.map`或模块（如果需要）之后，并设置`lilo.conf`文件以加载新内核后，您必须编辑并自定义与 FreeS/WAN 相关的配置文件`ipsec.conf`和`ipsec.secrets`，然后再重新启动系统。

## 工作后的清理

```
[root@deep /]# cd /usr/src
[root@deep src]# rm -rf freeswan-version/ freeswan-version.tar.gz
```

`rm`命令将删除我们用于编译和安装 FreeS/WAN 的所有源文件。它还会从`/usr/src`目录中删除 FreeS/WAN 的压缩归档文件。

## 配置

本书中描述的所有软件都在名为`floppy.tgz`的 tar 压缩归档文件中拥有特定的目录和子目录，该归档文件包含特定程序的文件配置。如果你获取了这个归档文件，就不必手动重新创建下面这些不同的配置文件，也不必复制粘贴它们来创建你的配置文件。无论你决定手动复制它们，还是从归档文件中获取为你准备好的文件，你都有责任根据需要进行修改、调整，并将与 FreeSWAN 软件相关的文件放置在服务器的适当位置，如下所示。要下载的服务器配置文件归档文件位于以下互联网地址：[http://www.openna.com/books/floppy.tgz](http://www.openna.com/books/floppy.tgz)

- 要运行 FreeSWAN，以下文件是必需的，必须创建或复制到服务器的相应目录中。

将`ipsec.conf`文件复制到`/etc/`目录中。

将`ipsec.secrets`文件复制到`/etc/`目录中。

你可以在我们的`floppy.tgz`归档文件中获取下面列出的配置文件。将以下文件从解压后的`floppy.tgz`归档文件中复制到适当的位置，或者直接从本书中复制粘贴到相关文件中。

## 配置`/etc/ipsec.conf`文件

FreeS/WAN 的配置文件`/etc/ipsec.conf`允许你配置 IPSEC 配置、控制信息和连接类型。IPSEC 目前支持两种类型的连接：手动密钥和自动密钥。它们的区别完全在于密钥的管理方式。手动密钥连接使用存储在`/etc/ipsec.conf`文件中的密钥。这种类型的连接不如自动密钥连接安全。自动密钥连接使用由 Pluto 密钥协商守护进程自动生成的密钥。默认使用的密钥协商协议名为 IKE，它使用存储在`/etc/ipsec.secrets`文件中的共享密钥对另一方系统进行身份验证。因此，我们将使用并向你展示自动密钥连接，它比手动密钥连接更安全（再次强烈建议你使用自动密钥连接）。

在我们下面的示例配置中，我们配置了一个带有防火墙穿透隧道的示例隧道，并假设左右两侧都进行了防火墙处理。我们选择向你展示此配置，因为我们认为这是大多数用户和公司会使用的。此外，它还允许我们在`ipsec.conf`配置文件中使用更多自动密钥连接的选项。存在不同的配置，你可以查阅源目录`trees/WAN`下子目录`doc`中的`doc/examples`文件，以获取更多信息和其他可能的配置。

**SubnetDeep**======**Deep**------**Deepgate**.................................**Mailgate**------**Mail**======**SubnetMail**

**不受信任的网络**

| | |

|:---|:---|:---|

| `leftsubnet` = | **SubnetDeep** | (192.168.1.0/24) |

| `left` = | **Deep** | (deep.openna.com) |

| `leftnexthop` = | **Deepgate** | (朝向 deep.openna.com 的第一个路由器或 ISP 路由器) |

| Internet = | **不受信任的网络** | |

| `rightnexthop` = | **Mailgate** | (朝向 mail.openna.com 的第一个路由器或 ISP 路由器) |

| `right` = | **Mail** | (mail.openna.com) |

| `rightsubnet` = | **SubnetMail** | (192.168.1.0/24) |

```
SubnetDeep \ 192.168.1.0/24 /
| Deep |
\ 208.164.186.1 /
+---------------------------+
```

Deepgate 是朝向你的第二个网关（mail.openna.com）方向的第一个路由器或你的 ISP 路由器的 IP 地址。

```
Deep \ 192.168.1.0/24 /
| Deep |
\ 208.164.186.1 /
+---------------------------+
```

Deep 是你的第一个网关的 IP 地址。eth0 连接到互联网。

```
Deepgate \ 205.151.222.250 /
+---------------------------+
```

**INTERNET** 是不受信任的网络。

```
Mailgate \ 205.151.222.251 /
+---------------------------+
```

**SubnetDeep** 是第一个网关上你的私有内部网络的 IP 网络地址。eth1 连接到内部网络。

```
Mailgate \ 205.151.222.251 /
+---------------------------+
```

**Mailgate** 是朝向你的第一个网关（deep.openna.com）方向的第一个路由器或你的 ISP 路由器的 IP 地址。

```
Mail / 208.164.186.2 \
+---------------------------+
```

**Mail** 是你的第二个网关的 IP 地址。eth0 连接到互联网。

```
SubnetMail / 192.168.1.0/24 \
+---------------------------+
```

**SubnetMail** 是第二个网关上你的私有内部网络的 IP 网络地址。eth1 连接到内部网络。

我们必须编辑`ipsec.conf`文件（`vi /etc/ipsec.conf`），并将默认值更改为符合我们 IPSEC 配置和通信的规范。目前此文件（`/etc/ipsec.conf`）中有两种类型的段：一个`config`段，用于指定 IPSEC 的一般配置信息。

第一种段类型名为 `config setup`，是 IPSEC 软件已知的唯一配置段，包含适用于所有连接的 IPSEC 总体设置参数，以及软件启动时使用的信息。

第二种类型名为 `conn`，包含一个连接规范，定义了使用 IPSEC 建立的网络连接。其名称是任意的，仅用于向`ipsec_auto(8)`和`ipsec_manual(8)`标识该连接。



# `/etc/ipsec.conf`：FreeS/WAN IPSEC 配置文件

```conf
# /etc/ipsec.conf - FreeS/WAN IPSEC configuration file
# More elaborate and more varied sample configurations can be found
# in doc/examples.

# basic configuration
config setup
	interfaces="ipsec0=eth0"
	klipsdebug=none
	plutodebug=none
	pluto=%search
	pluto=%search

# sample connection
conn deep-mail
    left=208.164.186.1
    leftsubnet=192.168.1.0/24
    leftnexthop=205.151.222.250
    right=208.164.186.2
    rightsubnet=192.168.1.0/24
    rightnexthop=205.151.222.251
    keyingtries=0
    auth=ah
    auto=start
```

## 配置 `/etc/ipsec.conf`

这告诉 `/etc/ipsec.conf` 文件为此特定配置进行以下设置：

### `interfaces="ipsec0=eth0"`

此选项指定 IPSEC 应使用的适当的虚拟和物理接口。默认设置 `interfaces=%defaultroute` 将查找你到互联网或公司网络的默认连接。此外，你可以指定一个或多个 FreeS/WAN 使用的特定接口。例如：

```conf
    interfaces="ipsec0=eth0"
    interfaces="ipsec0=eth0 ipsec1=ppp0"
```

两者都将 `eth0` 接口设置为 `ipsec0`。但第二个还支持通过 PPP 接口进行 IPSEC 通信。如果未使用默认设置 `interfaces=%defaultroute`，则指定的接口将是此网关机器可以用于与其他 IPSEC 网关通信的唯一接口。

### `klipsdebug=none`

此选项指定 KLIPS（内核 IPSEC 代码）的调试输出。默认值 `none` 表示不输出调试信息，值 `all` 表示输出全部调试信息。

### `plutodebug=none`

此选项指定 Pluto 密钥的调试输出。默认值 `none` 表示不输出调试信息，值 `all` 表示输出全部调试信息。

### `plutoload=%search`

此选项指定 Pluto 启动时自动加载到内存中的连接（按名称）。默认为 `none`，值 `%search` 加载所有 `auto=add` 或 `auto=start` 的连接。

### `plutostart=%search`

此选项指定 Pluto 启动时自动协商的连接（按名称）。默认为 `none`，值 `%search` 启动所有 `auto=start` 的连接。

### `conn deep-mail`

此选项指定用于标识使用 IPSEC 建立的连接规范的名称。按照连接两端命名连接是一个好习惯，可以避免错误。例如，`deep.openna.com` 和 `mail.openna.com` 网关服务器之间的链路可以命名为 `deep-mail`，或者你的蒙特利尔和巴黎办公室之间的链路命名为 `montreal-paris`。

请注意，`deep-mail` 或你选择的任何名称在两个网关上的 `/etc/ipsec.conf` 文件中应该相同。换句话说，你应该在第二个网关的 `/etc/ipsec.conf` 文件中进行的唯一更改是将 `interfaces=` 行更改为与第二个网关用于 IPSEC 连接的接口匹配（当然，如果与第一个网关不同的话）。例如，如果两个网关上的 `eth0` 接口都用于 IPSEC 通信，您无需修改第二个网关上的 `interfaces=` 行。另一方面，如果第一个网关使用 `eth0`，第二个网关使用 `eth1`，则必须修改第二个网关上的 `interfaces=` 行以匹配 `eth1` 接口。

### `left=208.164.186.1`

此选项指定网关外部接口的 IP 地址，用于与其他网关通信。

### `leftsubnet=192.168.1.0/24`

此选项指定网关后方私有子网的 IP 网络或地址。

### `leftnexthop=205.151.222.250`

此选项指定正确方向或 ISP 路由器的第一个路由器的 IP 地址。

### `right=208.164.186.2`

这与 `left=` 的解释相同，但用于右侧目标。

### `rightsubnet=192.168.1.0/24`

这与 `leftsubnet=` 的解释相同，但用于右侧目标。

### `rightnexthop=205.151.222.251`

这与 `leftnexthop=` 的解释相同，但用于右侧目标。

### `keyingtries=0`

此选项指定（重新）密钥协商中应尝试的次数（整数）。建议使用默认值 `0`（永久重试）。

### `auth=ah`

此选项指定身份验证是应单独使用 AH（认证头）进行，还是作为 ESP（封装安全载荷）服务的一部分。当 IP 标头暴露以防止中间人攻击时，建议使用此选项。

### `auto=start`

此选项指定是否应在 IPSEC 启动时执行自动启动操作。

**注意：** 此配置 `/etc/ipsec.conf` 中任何位置的数据不匹配都会导致 FreeS/WAN 失败并记录各种错误消息。

## 配置 `/etc/ipsec.secrets` 文件

`/etc/ipsec.secrets` 文件存储 `pluto` 守护进程用于验证两个网关之间通信的密钥。可以在 Spotlight 文件中配置两种不同类型的密钥，即预共享密钥和 RSA 私钥。您必须检查此文件的模式和权限，确保超级用户 `root` 拥有该文件，并且其权限设置为阻止其他所有用户访问。

### 第 1 步：创建共享密钥

`/etc/ipsec.secrets` 文件中默认提供了一个示例密钥。您应该通过创建自己的密钥来更改它。使用自动密钥时，您可以拥有最多 256 位的共享密钥，然后在密钥交换期间使用它以确保不会发生中间人攻击。

- 要创建新的共享密钥，请使用以下命令：

  ```bash
  [root@deep /]# ipsec ranbits 256 > temp
  ```

使用 `ranbits(8)` 工具在名为 `temp` 的文件中创建新的随机密钥。如果立即没有足够的熵可用，`ranbits` 工具可能会暂停几秒钟。

**注意：** 完成后不要忘记删除临时文件。

### 第 2 步：配置共享密钥

现在，我们的新共享密钥已在 `temp` 文件中创建，我们必须将其放入 `/etc/ipsec.secrets` 文件中。编辑 `/etc/ipsec.secrets` 文件时，您应该会在文本编辑器中看到类似以下内容的内容。每行包含两个网关的 IP 地址加上密钥。它应该看起来像这样：

```conf
# This file holds shared secrets which are currently the only inter-Pluto
# authentication mechanism. See ipsec_pluto(8) manpage. Each secret is
# (oversimplifying slightly) for one pair of negotiating hosts.
# The shared secrets are arbitrary character strings and should be both
# long and hard to guess.
# Note that all secrets must now be enclosed in quotes, even if they have
# no white space inside them.

10.0.0.1 11.0.0.1      "jxVS1kVUTTulkVRRTnTujSm444jRuU1mkkIku2nkW3nnVu
V2WjjRRnulmIkmU1Run5VSnnRT"
```

编辑 `/etc/ipsec.secrets` 文件（`vi /etc/ipsec.secrets`）并更改默认的密钥：

```conf
10.0.0.1 11.0.0.1  " jxVS1kVUTTulkVRRTnTujSm444jRuU1mkkIku2nkW3nnVu
V2WjjRRnulmIkmU1Run5VSnnRT "
更改为：
208.164.186.1 208.164.186.2
"0x9748cc31_2e99194f_d230589b_cd846b57_dc070b01_74b66f34_19c40a1a_804906ed"
 corpse
```

其中 `208.164.186.1` 和 `208.164.186.2` 是两个网关的 IP 地址，`0x9748cc31_2e99194f_d230589b_cd846b57_dc070b01_74b66f34_19c40a1a_804906ed`（注意引号是必需的）是我们使用上面 `ipsec ranbits 256 > temp` 命令在 `temp` 文件中生成的共享密钥。

### 第 3 步：复制配置文件

`/etc/ipsec.conf` 和 `/etc/ipsec.secrets` 文件必须复制到第二台网关机器上，以便两端完全相同。唯一的例外是 `/etc/ipsec.conf` 文件，其中必须包含标有 `config setup` 的行，并带有第二台网关的正确接口设置（如果与第一台不同）。与 RSA 私钥不同，`/etc/ipsec.secrets` 文件在两台网关上绝对应该具有相同的共享密钥。

**注意：** 文件 `/etc/ipsec.secrets` 应具有权限 `rw-------- (600)`，并由超级用户 `root` 拥有。文件 `/etc/ipsec.conf` 的安装权限为 `rw-r--r-- (644)`，也必须由 `root` 拥有。

## 配置 RSA 私钥

请注意，目前 FreeSWAN 软件有两种密钥：预共享密钥和 RSA 私钥。预共享密钥就是我们在上面的 `/etc/ipsec.conf` 和 `/etc/ipsec.secrets` 示例中配置的。有些人可能更喜欢使用 RSA 私钥进行 Pluto 守护进程对其他主机的身份验证。如果您处于这种情况，则需要对 `/etc/ipsec.conf` 和 `/etc/ipsec.secrets` 文件进行一些小的修改，如以下步骤所述：

您需要为每个网关创建一个单独的 RSA 密钥。每个网关在其自己的 `/etc/ipsec.secrets` 文件中获取其私钥，公钥则放在 `/etc/ipsec.conf` 文件的 `conn` 描述中的 `leftrsasigkey` 和 `rightrsasigkey` 参数中，该文件将发送到两台网关。

### 第 1 步：生成 RSA 密钥

为每个网关创建一个单独的 RSA 密钥：

- 在第一个网关（例如 `deep`）上，使用以下命令：

  ```bash
  [root@deep /]# cd /
  [root@deep /]# ipsec rsasigkey --verbose 1024 > deep-keys
  ```

  ```text
  computing primes and modulus...

  getting 64 random bytes from /dev/random

  looking for a prime starting there

  found it after 30 tries

  getting 64 random bytes from /dev/random

  looking for a prime starting there

  found it after 230 tries

  swapping primes so p is the larger

  computing (p-1)*(q-1)...

  computing d...

  computing exp1, exp1, coeff...

  output...
  ```

- 在第二个网关（例如 `mail`）上，使用以下命令：

  ```bash
  [root@mail /]# cd /
  [root@mail /]# ipsec rsasigkey --verbose 1024 > mail-keys
  ```

  ```text
  computing primes and modulus...

  getting 64 random bytes from /dev/random

  looking for a prime starting there

  found it after 30 tries

  getting 64 random bytes from /dev/random

  looking for a prime starting there

  found it after 230 tries

  swapping primes so p is the larger

  computing (p-1)*(q-1)...

  computing d...

  computing exp1, exp1, coeff...

  output...
  ```

`rsasigkey` 工具生成 1024 位签名的 RSA 公钥和私钥对，并将其放入文件 `deep-keys` 中（第二个网关上的第二个命令为 `mail-keys`）。私钥可以原样插入 `/etc/ipsec.secrets` 文件，公钥则可以插入 `/etc/ipsec.conf` 文件。

**注意：** 如果立即没有足够的熵可用，`rsasigkey` 工具可能会暂停几秒钟。您可能需要进行一些虚假活动，例如随机移动鼠标。完成后应立即删除临时的 RSA `deep-keys` 和 `mail-keys` 文件。不要忘记删除 `deep-keys` 和 `mail-keys` RSA 文件。

### 第 2 步：配置 RSA 公钥

修改您的 `/etc/ipsec.conf` 文件以在每个网关中使用 RSA 公钥：

编辑您原来的 `/etc/ipsec.conf` 文件（`vi /etc/ipsec.conf`）并在两台网关的 `/etc/ipsec.conf` 文件的 `conn` 描述中添加以下与 RSA 相关的参数：

```conf
# sample connection
conn deep-mail
left=208.164.186.1
leftsubnet=192.168.1.0/24
leftnexthop=205.151.222.250
right=208.164.186.2
rightsubnet=192.168.1.0/24
rightnexthop=205.151.222.251
keyingtries=0
auth=ah
authby=rsasig
leftrsasigkey=<Public key of deep>
rightrsasigkey=<Public key of mail>
auto=start
```

#### `authby=rsasig`

此参数指定两个安全网关应如何相互验证。默认值为用于共享密钥的 `secret`。由于我们决定使用 RSA 数字签名，因此必须指定 `rsasig`。

#### `leftrsasigkey=<Public key of deep>`

此参数指定左侧参与者用于 RSA 签名验证的公钥。在我们的示例中，`left` 是 `208.164.186.1`，代表 `deep.openna.com`，因此我们必须将 `deep` 的 RSA 公钥放在此行。

#### `rightrsasigkey=<Public key of mail>`

此参数指定右侧参与者用于 RSA 签名验证的公钥。在我们的示例中，`right` 是 `208.164.186.2`，代表 `mail.openna.com`，因此我们必须将 `mail` 的 RSA 公钥放在此行。

您可以在名为 `deep-keys` 的 RSA 密钥文件中检索 `deep` 的公钥，在名为 `mail-keys` 的 RSA 密钥文件中检索 `mail` 的公钥，这些是我们上面在第 1 步中创建的文件。这些文件将如下所示：

网关 `deep` 的 RSA 密钥（`deep-keys`）：



```text
[root@deep /]# cd /
[root@deep /]# vi deep-keys

    # 1024 bits, Fri Feb 4 05:05:19 2000
    # for signatures only, UNSAFE FOR ENCRYPTION
    #pubkey=0x010395daee1be05f3038ae529ef2668afd79f5ff1b16203c9ceaef801cea9cb74bcfb51a6e
    cc08890d3eb4b5470c0fc35465c8ba2ce9d1145ff07b5427e04cf4a38ef98a7f29edcb4d7689f2da7a69199e
    4318b4c8d0ea25d33e4f084186a2a54f4b4cec12cca1a5deac3b19d561c16a76bab772888f1fd71aa breastf0
    02a141b611f
    Modulus:
    0x95daee1be05f3038ae529ef2668afd79f5ff1b16203c9ceaef801cea9cb74bcfb51a6ecc08890d3eb4b5470c0
    fc35465c8ba2ce9d1145ff07b5427e04cf4a38ef98a7f29edcb4d7689f2da7a69199e4318b4c8d0ea25d33e4f0
    84186a2a54f4b4cec12cca1a5deac3b19d561c16a76bab772888f1fd71aa08f08502a141b611f
    PublicExponent: 0x03
    # everything after this point is secret
    PrivateExponent:
    0x63e74967eaea2025c98c69f6ef0753a6a3ff6764157dbdf1f50013471324dd352366f48805b0b37f232384b2
    b52ce2ee85d173468b62eaa052381a9588a317b3a1324d01a531a41fa7add6c5efbdd88f4718feed2bc0246b
    e924e81bb90f03e49ceedf7af0dd48f06f2655b519600bd082c6e6bd27eaa71cc0288df1ecc3b062b
    Prime1:
    0xc5b471a88b025dd09d4bd7b61840f20d182d9b75bb7c11eb4bd78312209e3aee7ebfe632304db6df5e211d
    21af7fee79c5d45546bea3ccc7b744254f6f0b847f
    Prime2:
    0xc20a99feeafe79767122409b693be75f15e1aef76d098ab12579624aec708e85e2c5dd62080c3a64363f2f4
    5b0e96cb4aef8918ca333a326d3f6dc2c72b75361
```

## Exponent1

```text
0x83cda11b0756e935be328fcebad5f6b36573bcf927a80bf2328facb6c0697c9eff2a9976cade79ea3ec0be16

74fff4512e8d8e2f29c2888524d818df9f5d02ff
```

## Exponent2

```text
0x815c66a9f1fefba44b6c2b124627ef94b9411f4f9e065c7618fb96dc9da05f03ec83e8ec055d7c42ced4ca2e7

5f0f3231f5061086ccd176f37f9e81da1cf8ceb
```

## Coefficient

```text
0x10d954c9e2b8d11f4db1b233ef37ff0a3cecffad89ba5d515449b007803f577e3bd7f0183ceddfd805466d62f

767f3f5a5731a73875d30186520f1753a7e325
```

### 网关邮件（`mail-keys`）的 RSA 密钥

```text
# 1024 bits, Fri Feb 4 04:46:59 2000
# 仅用于签名，不适用于加密
#pubkey=0x01037631b81f00d5e6f888c542d44dbb784cd3646f084ed96f942d341c7c4686cbd405b8
05dc728f8697475f11e8b1dd797550153a3f0d4ff0f2b274b70a2ebc88f073748d1c1c8821dc6be6a2f0064f
3be7f8e4549f8ab9af64944f829b014788dd202cf7d2e320cab666f5e7a197e64efe0bfee94e92ce4dad82d5
230c57b89edf
Modulus:
0x7631b81f00d5e6f888c542d44dbb784cd3646f084ed96f942d341c7c4686cbd405b805dc728f8697475f11e8
b1dd797550153a3f0d4ff0f2b274b70a2ebc88f073748d1c1c8821dc6be6a2f0064f3be7f8e4549f8ab9af64944f
829b014788dd202cf7d2e320cab666f5e7a197e64efe0bfee94e92ce4dad82d5230c57b89edf
PublicExponent: 0x03
# 此后所有内容均为机密
PrivateExponent:
0x4ecbd014ab3944a5b08381e2de7cfadde242f4b03490f50d737812fd8459dd3803d003e84c5faf0f84ea0bf0
7693a64e35637c2a08dff5f721a324b1747db09f62c871d5e11711251b845ae76753d4ef967c494b0def4f5d07
62f65da603bc04c41b4c6cab4c413a72c633b608267ae2889c162a3d5bc07ee083b1c6e038400b
Prime1:
0xc7f7cc8feaaac65039c39333b878bffd8f95b0dc22995c553402a5b287f341012253e9f25b83983c936f6ca51
2926bebee3d5403bf9f4557206c6bbfd9aac899
Prime2:
0x975015cb603ac1d488dc876132d8bc83079435d2d3395c03d5386b5c004eadd4d7b01b3d86aad0a2275d2
d6b791a2abe50d7740b7725679811a32ca22db97637
Exponent1:
0x854fdddb5471c84357bd7b777d0507ffe5fb92092c1bb92e37801c3cc5aa22b5616e29bf6e7ad1028624a486
e0c619d47f428e2ad2a6a2e3a159d9d2a911c85bb
Exponent2:
0x64ee00e87957c81385b3daf9621e5d302050d7937377b92ad38d04792aadf1e8de52012290471e06c1a3e1
e47a61171d435e4f807a4c39a6561177316c9264ecf
Coefficient:
0x6f087591becddc210c2ee0480e30beeb25615a3615203cd3cef65e5a1d476fd9602ca0ef10d9b858edb22db
42c975fb71883a470b43433a7be57df7ace4a0a3f
```

按照如下所示，将 `deep` 和 `mail` 的 RSA 公钥文件提取并复制到你的 `ipsec.conf` 文件中。你可以通过以注释掉的 `#pubkey=` 开头的一行来定位与公钥相关的行。

```text
# 示例连接
conn deep-mail
    left=208.164.186.1
    leftsubnet=192.168.1.0/24
    leftnexthop=205.151.222.250
    right=208.164.186.2
    rightsubnet=192.168.1.0/24
    rightnexthop=205.151.222.251
    keyingtries=0
    auth=ah
    authby=rsasig
    leftrsasigkey=0x010395daee1be05f3038ae529ef2668afd79f5ff1b16203c9ceaef801cea9cb74bcfb5
    1a6ecc08890d3eb4b5470c0fc35465c8ba2ce9d1145ff07b5427e04cf4a38ef98a7f29edcb4d7689f2d
    a7a69199e4318b4c8d0ea25d33e4f084186a2a54f4b4cec12cca1a5deac3b19d561c16a76bab77288
    8f1fd71aa08f08502a141b611f
    rightrsasigkey=0x01037631b81f00d5e6f888c542d44dbb784cd3646f084ed96f942d341c7c4686cbd
    405b805dc728f8697475f11e8b1dd797550153a3f0d4ff0f2b274b70a2ebc88f073748d1c1c8821dc6b
    e6a2f0064f3be7f8e4549f8ab9af64944f829b014788dd202cf7d2e320cab666f5e7a197e64efe0bfee94
    e92ce4dad82d5230c57b89edf
    auto-start
```

注意：不要忘记，在本示例中，`leftrsasigkey=` 参数包含 `deep` 的公钥，`rightrsasigkey=` 参数包含 `mail` 的公钥。

### 步骤 3

修改你的 `/etc/ipsec.secrets` 文件，以便在*每个*网关上都使用 RSA 私钥：

编辑你原来的 `ipsec.secrets` 文件（`vi /etc/ipsec.secrets`），并在两个网关上添加用于身份验证的 RSA 私钥：

网关 `deep` 的 `ipsec.secrets` 文件：

```text
208.164.186.1 208.164.186.2
"0x9748cc31_2e99194f_d230589b_cd846b57_dc070b01_74b66f34_19c40a1a_804906ed"
```

你必须按照上图所示修改你原来的 `ipsec.secrets` 文件，使其在两个网关上看起来都像下面这样。需要注意的是，`deep` 和 `mail` 两个网关上的私钥并不相同。`deep` 的私钥来自 RSA 密钥文件 `deep-keys`，而 `mail` 的私钥来自 RSA 密钥文件 `mail-keys`。

```text
208.164.186.1 208.164.186.2: RSA {
    Modulus:
    0x95daee1be05f3038ae529ef2668afd79f5ff1b16203c9ceaef801cea9cb74bcfb51a6ecc08890d3eb4b5470c0
    fc35465c8ba2ce9d1145ff07b5427e04cf4a38ef98a7f29edcb4d7689f2da7a69199e4318b4c8d0ea25d33e4f0
    84186a2a54f4b4cec12cca1a5deac3b19d561c16a76bab772888f1fd71aa08f08502a141b611f
    PublicExponent: 0x03
    # 此后所有内容均为机密
    PrivateExponent:
    0x63e74967eaea2025c98c69f6ef0753a6a3ff6764157dbdf1f50013471324dd352366f48805b0b37f232384b2
    b52ce2ee85d173468b62eaa052381a9588a317b3a1324d01a531a41fa7add6c5efbdd88f4718feed2bc0246b
    e924e81bb90f03e49ceedf7af0dd48f06f2655b519600bd082c6e6bd27eaa71cc0288df1ecc3b062b
    Prime1:
    0xc5b471a88b025dd09d4bd7b61840f20d182d9b75bb7c11eb4bd78312209e3aee7ebfe632304db6df5e211d
    21af7fee79c5d45546bea3ccc7b744254f6f0b847f
    Prime2:
    0xc20a99feeafe79767122409b693be75f15e1aef76d098ab12579624aec708e85e2c5dd62080c3a64363f2f4
    5b0e96cb4aef8918ca333a326d3f6dc2c72b75361
    Exponent1:
    0x83cda11b0756e935be328fcebad5f6b36573bcf927a80bf2328facb6c0697c9eff2a9976cade79ea3ec0be16
    74fff4512e8d8e2f29c2888524d818df9f5d02ff
    Exponent2:
    0x815c66a9f1fefba44b6c2b124627ef94b9411f4f9e065c7618fb96dc9da05f03ec83e8ec055d7c42ced4ca2e7
    5f0f3231f5061086ccd176f37f9e81da1cf8ceb
    Coefficient:
    0x10d954c9e2b8d11f4db1b233ef37ff0a3cecffad89ba5d515449b007803f577e3bd7fream 0183ceddfd805466d62f
    767f3f5a5731a73875d30186520f1753a7e325
}
```

### 网关 `mail` 的 `ipsec.secrets` 文件

```text
208.164.186.1 208.164.186.2: RSA {
    Modulus:
    0x95daee1be05f3038ae529ef2668afd79f5ff1b16203c9ceaef801cea9cb74bcfb51a6ecc08890d3eb4b5470c0
    fc35465c8ba2ce9d1145ff07b5427e04cf4a38ef98a7f29edcb4d7689f2da7a69199e4318b4c8d0ea25d33e4f0
    84186a2a54f4b4cec12cca1a5deac3b19d561c16a76bab772888f1fd71aa08f08502a141b611f
    PublicExponent: 0x03
    # 此后所有内容均为机密
    PrivateExponent:
    0x63e74967eaea2025c98c69f6ef0753a6a3ff6764157dbdf1f50013471324dd352366f48805b0b37f232384b2
    b52ce2ee85d173468b62eaa052381a9588a317b3a1324d01a531a41fa7add6c5efbdd88f4718feed2bc0246b
    e924e81bb90f03e49ceedf7af0dd48f06f2655b519600bd082c6e6bd27eaa71cc0288df1ecc3b062b
    Prime1:
    0xc5b471a88b025dd09d4bd7b61840f20d182d9b75bb7c11eb4bd78312209e3aee7ebfe632304db6df5e211d
    21af7fee79c5d45546bea3ccc7b744254f6f0b847f
    Prime2:
    0xc20a99feeafe79767122409b693be75f15e1aef76 ae 098ab12579624aec708e85e2c5dd62080c3a64363f2f4
    5b0e96cb4aef8918ca333a326d3f6dc2c72b75361
    Exponent1:
    0x83cda11b0756e935be328fcebad5f6b36573bcf927a80bf2328facb6c0697c9eff2a9976cade79ea3ec0be16
    74fff4512e8d8e2f29c2888524d818df9f5d02ff
    Exponent2:
    0x815c66a9f1fefba44b6c2b124627ef94b9411f4f9e065c7618fb96dc9da05f03ec83e8ec055d7c42ced4ca2e7
    5f0f3231f5061086ccd176f37f9e81da1cf8ceb
    Coefficient:
    0x10d954c9e2b8d11f4db1b233ef37ff0a3cecffad89ba5d515449b007803f577e3bd7f0183ceddfd805466d62f
    767f3f5a5731a73875d30186520f1753a7e325
}
```



基于 RSA 签名的身份验证要求每个主机拥有自己的私钥。条目中的密钥部分可以以指示密钥类型的标记开头。"RSA" 表示 RSA 私钥，"PSK"（默认值）表示预共享密钥。由于 "PSK" 是默认值，因此我们必须指定 "RSA"，以便能够在此文件（`ipsec.secrets`）中使用 RSA 私钥。超级用户 "`root`" 应该拥有 "`ipsec.secrets`" 文件，并且其权限应设置为阻止其他所有用户访问。

## IPSec 的网络设置要求

在运行 FreeS/WAN 软件之前，你需要确保一些事项正确无误。这些注意事项很重要，可以避免你在启动 VPN 时收到错误消息。需要遵循的步骤如下：

### 步骤 1

你需要在两个网关服务器上启用 TCP/IP 转发。在 Red Hat Linux 中，这可以通过更改或添加以下行来实现，具体取决于你使用的 Red Hat 版本。

#### 在 Red Hat Linux 6.1 下

- 编辑 `network` 文件（`vi /etc/sysconfig/network`），并更改以下行：

```text
FORWARD_IPV4="false"
```

改为：

```text
FORWARD_IPV4="yes"
```

- 你必须重新启动网络才能使更改生效：

```text
[root@deep /]# /etc/rc.d/init.d/network restart
```

版权所有 1999 - 2000 Gerhard Mourani，Open Network Architecture ® 和 OpenDocs Publishing。

```text
Bringing up interface lo               [ OK ]
Bringing up interface eth0              [ OK ]
Bringing up interface eth1              [ OK ]
```

#### 在 Red Hat Linux 6.2 下

- 要在您的 RH 6.2 系统上启用 IPv4 转发，请使用以下命令：

  编辑 `/etc/sysctl.conf` 文件并添加以下行：

```text
# Enable packet forwarding

net.ipv_NETWORKING_FORWARD = 1
```

您必须重启网络才能使更改生效。重启网络的命令如下：

- 要在您的系统上手动重启所有网络设备，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters            [ OK ]

Bringing up interface lo              [ OK ]

Bringing up interface eth0              [ OK ]

Bringing up interface eth1              [ OK ]
```

### 步骤 2

请记住，自动密钥连接使用由 Pluto 密钥协商守护进程自动生成的密钥。Pluto 守护进程将启动，尝试连接到隧道另一端的 Pluto 守护进程，并建立连接。因此，IPSEC 网关应在防火墙脚本文件中设置数据包过滤规则，允许以下协议在与其他 IPSEC 网关通信时穿越网关：

- UDP 端口 500，用于 Pluto 守护进程实现的 IKE。
- 协议 50，用于 ESP 加密和/或认证。
- 协议 51，用于 AH 数据包级认证。

在两台网关机器上编辑 `firewall` 脚本文件（`vi /etc/rc.d/init.d/firewall`），并添加/检查以下行，以允许 IPSEC 数据包穿越远程网络网关到您的网络网关，反之亦然：

```bash
# FreeS/WAN IPSec VPN
# ------------------

# If you are using the FreeSWAN IPSec VPN, you will need to fill in the
# addresses of the gateways in the IPSECSG and the virtual interfaces for
# FreeS/Wan IPSEC in the FREESWANVI parameters. Look at the beginning of
# this firewall script rules file to set the parameters.

# IPSECSG is a Space separated list of remote gatewaystst. FREESWANVI is a
# Space separated list of virtual interfaces for FreeS/Wan IPSEC
# implementation. Only include those that are actually used.

# Allow IPSEC protocol from remote gateways on external interface
# IPSEC uses three main types of packet:
# IKE uses the UDP protocol and port 500,
# ESP use the protocol number 50, and
# AH use the protocol number 51

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
        -s $IPSECSG -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
    -d $IPSECSG -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p 50 \
    -s $IPSECSG -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p 50 \
    -d $IPSECSG -j ACCEPT

ipchains -A input -i $EXTERNAL_INTERFACE -p 51 \
    -s $IPSECSG -j ACCEPT

ipchains -A output -i $EXTERNAL_INTERFACE -p 51 \
    -d $IPSECSG -j ACCEPT
```

```bash
# Allow all traffic to FreeS/WAN Virtual Interface
ipchains -A input -i $FREESWANVI \
    -s $ANYWHERE \
    -d $ANYWHERE -j ACCEPT

ipchains -A output -i $FREESWANVI \
    -s $ANYWHERE \
    -d $ANYWHERE -j ACCEPT

# Forward anything from the FreeS/WAN virtual interface IPSEC tunnel
ipchains -A forward -i $FREESWANVI \
    -s $ANYWHERE \
    -d $ANYWHERE -j ACCEPT
```

```text
Where EXTERNAL_INTERFACE="eth0"   # You external interface to the Internet.
Where ANYWHERE="any/0"            # Mean everywhere 0.0.0.0/0.
Where IPSECSG="208.164.186.2"     # Space separated list of remote VPN gateways.
Where FREESWANVI="ipsec0"         # Space separated list of virtual interfaces for FreeS/Wan.
```

**注意：** 更多信息请参阅第 7 章"网络防火墙"。不要忘记在另一个网关上也添加/检查这些防火墙规则。

### 步骤 3

`rp_filter` 子系统（与 IP 欺骗防护相关）必须在两个网关上关闭，IPSEC 才能正常工作。这是通过检查 `/proc/sys/net/ipv4/conf/ipsec0/rp_filter` 和 `/proc/sys/net/ipv4/conf/eth0/rp_filter` 文件中是否设置为值 0（关闭）来实现的。

- 要检查 `rp_filter` 文件中是否设置了值 0（关闭），请使用以下命令：

```text
[root@deep /]# cat /proc/sys/net/ipv4/conf/ipsec0/rp_filter

0

[root@deep /]# cat /proc/sys/net/ipv4/conf/eth0/rp_filter

0
```

**注意：** 在我们的示例中，子目录 `ipsec0` 只有在系统重启后才会创建。因此，您可以在系统重启后检查 `ipsec0` 目录中 `rp_filter` 文件的值。

- 要在两个 `rp_filter` 文件中手动设置值 0（关闭），请使用以下命令：

```text
[root@deep /]# echo 0 > /proc/sys/net/ipv4/conf/ipsec0/rp_filter

[root@deep /]# echo 0 > /proc/sys/net/ipv4/conf/eth0/rp_filter
```

此外，您可以在两个网关的防火墙脚本文件（`/etc/rc.d/init.d/firewall`）中添加类似以下的行，以自动将这些值设置为 0（关闭），避免手动操作：

```bash
# Disable IP spoofing protection to allow IPSEC to work properly
echo 0 > /proc/sys/net/ipv4/conf/ipsec0/rp_filter
echo 0 > /proc/sys/net/ipv4/conf/eth0/rp_filter
```

**注意：** 在上面的防火墙脚本文件示例中，我们假设 `eth0` 序号是您用于连接的接口。当然，如果您使用 `eth1`，则必须将 `eth0` 更改为 `eth1`，依此类推。

如果您忘记此步骤，在启动 FreeSWAN IPSEC 时，终端上将收到如下错误消息：

```text
ipsec_setup: WARNING: ipsec0 has route filtering turned on, KLIPS may not work
ipsec_setup: (/proc/sys/net/ipv4/conf/ipsec0/rp_filter = `1', should be 0)
ipsec_setup: WARNING: eth0 has route filtering turned on, KLIPS may not work
ipsec_setup: (/proc/sys/net/ipv4/conf/eth0/rp_filter = `1', should be 0)
```

### 步骤 4

需要注意的是，对于使用 IPSEC 的内部网络的任何伪装规则，必须放在允许 IPSEC 相关流量之后（上面的步骤 2 和 3），否则机器将尝试伪装数据包，而不是将它们传递给 IPSEC。

在两台网关机器上编辑 `firewall` 脚本文件（`vi /etc/rc.d/init.d/firewall`），并添加/检查以下行，以允许伪装数据包穿越远程网络网关到您的网络网关，反之亦然：

```text
# Masquerade internal traffic.
```

```bash
# All internal traffic is masqueraded externally.

ipchains -A forward -i $EXTERNAL_INTERFACE -s $LOCALNET_1 -j MASQ
```

其中，`EXTERNAL_INTERFACE="eth0"` 表示连接到 Internet 的外部接口。

其中，`LOCALNET_1=" 192.168.1.0/24"` 表示您使用的私有地址范围。

**注意：** 更多信息请参阅第 8 章"支持伪装和转发的网络防火墙"。

现在，您可以重新启动系统，Gateway A 上的机器应该能够与 Gateway B 上的机器正常通信。

## 测试安装

- 重启两台网关以启动 FreeS/WAN。
- 检查 `/var/log/messages` 文件以查找任何故障迹象。如果一切正常，您应该在 `/var/log/messages` 文件中看到类似以下内容：

```text
Feb 2 05:22:35 deep ipsec_setup: Starting FreeS/WAN IPSEC snap2000jan31b...
Feb 2 05:22:35 deep ipsec_setup: KLIPS debug `none'
Feb 2 05:22:35 deep ipsec_setup: KLIPS ipsec0 on eth0 192.168.1.1/255.255.255.0 broadcast 192.168.1.255
Feb 2 05:22:36 deep ipsec_setup: Disabling core dumps:
Feb 2 05:22:36 deep ipsec_setup: Starting Pluto (debug `none'):
Feb 2 05:22:37 deep ipsec_setup: Loading Pluto database `deep-mail':
Feb 2 05:22:37 deep ipsec_setup: Enabling Pluto negotiation:
Feb 2 05:22:37 deep ipsec_setup: Routing for Pluto conns `deep-mail':
Feb 2 05:22:37 deep ipsec_setup: Initiating Pluto tunnel `deep-mail':
Feb 2 05:22:39 deep ipsec_setup: 102 "deep-mail" #1: STATE_MAIN_I1: initiate
Feb 2 05:22:39 deep ipsec_setup: 104 "deep-mail" #1: STATE_MAIN_I2: from STATE_MAIN_I1; sent MI2, expecting MR2
Feb 2 05:22:39 deep ipsec_setup: 106 "deep-mail" #1: STATE_MAIN_I3: from STATE_MAIN_I2; sent MI3, expecting MR3
Feb 2 05:22:39 deep ipsec_setup: 004 "deep-mail" #1: STATE_MAIN_I4: SA established
Feb 2 05:22:39 deep ipsec_setup: 110 "deep- mail" #2: STATE_QUICK_I1: initiate
Feb 2 05:22:39 deep ipsec_setup: 004 "deep-mail" #2: STATE_QUICK_I2: SA established
Feb 2 05:22:39 deep ipsec_setup: ...FreeS/WAN IPSEC started
```

- 检查 `/var/log/secure` 文件以查找任何故障迹象。如果一切正常，您应该看到类似以下内容：

```text
Feb 21 14:45:42 deep Pluto[432]: Starting Pluto (Free/WAN Version 1.3)
Feb 21 14:45:43 deep Pluto[432]: added connection description "deep-mail"
Feb 21 14:45:43 deep Pluto[432]: listening for IKE messages
Feb 21 14:45:43 deep Pluto[432]: adding interface ipsec0/eth0 192.168.1.1
Feb 21 14:45:43 deep Pluto[432]: loading secrets from "/etc/ipsec.secrets"
Feb 21 14:45:43 deep Pluto[432]: "deep-mail" #1: initiating Main Mode
Feb 21 14:45:44 deep Pluto[432]: "deep-mail" #1: ISAKMP SA established
Feb 21 14:45:44 deep Pluto[432]: "deep-mail" #2: initiating Quick Mode
POLICY_RSASIG+POLICY_ENCRYPT+POLICY_AUTHENTICATE+POLICY_TUNNEL+POLICY_PFS
Feb 21 14:45:46 deep Pluto[432]: "deep-mail" #2: sent QI2, IPsec SA established
Feb 21 14:45:47 deep Pluto[432]: "deep-mail" #3: responding to Main Mode
Feb 21 14:45:49 deep Pluto[432]: "deep-mail" #3: sent MR3, ISAKMP SA established
Feb 21 14:45:49 deep Pluto[432]: "deep-mail" #4: responding to Quick Mode
Feb 21 14:45:50 deep Pluto[432]: "deep-mail" #4: IPsec SA established
```



- 在两台网关上，`/proc/net/`目录中现在应该存在以下条目：

```
[root@deep /]# ls -l /proc/net/ipsec_*
-r--r--r--  1 root  root    0 Feb 2 05:30 /proc/net/ipsec_eroute
-r--r--r--  1 root  root    0 Feb 2 05:30 /proc/net/ipsec_klipsdebug
-r--r--r--  1 root  root    0 Feb 2 05:30 /proc/net/ipsec_spi
-r--r--r--  1 root  root    0 Feb 2 05:30 /proc/net/ipsec_spigrp
-r--r--r--  1 root  root    0 Feb 2 05:30 /proc/net/ipsec_spinew
-r--r--r--  1 root  root    0 Feb 2 05:30 /proc/net/ipsec_tncfg
-r--r--r--  1 root  root    0 Feb 2 05:30 /proc/net/ipsec_version
```

- IPSEC 接口应附加在指定的物理接口之上。请通过以下方式确认：

```
[root@deep /]# cat /proc/net/ipsec_tncfg
ipsec0 -> eth0 mtu=16260 -> 1500
ipsec1 -> NULL mtu=0 -> 0
ipsec2 -> NULL mtu=0 -> 0
ipsec3 -> NULL mtu=0 -> 0
```

- 现在执行以下命令以显示最少的调试信息，并查看输出是否如下所示：

```
[root@deep /]# ipsec look
deep.openna.com Fri Feb 4 17:25:17 EST 2000
```

```
192.168.1.1/32  -> 192.168.1.2/32  => tun0x106@192.168.1.2 esp0x4450894d@192.168.1.2 ah0x4450894c@192.168.1.2
----------------------
ah0x3350f551@192.168.1.1 AH_HMAC_MD5: dir=in ooowin=32 seq=115 bit=0xffffffff alen=128 aklen=16 life(c,s,h)=bytes(16140,0,0)add(51656,0,0)use(54068,0,0)packets(115,0,0) idle=499
ah0x4450894c@192.168.1.2 AH_HMAC_MD5: dir=out ooowin=32 seq=2828 alen=128 aklen=16 life(c,s,h)=bytes(449488,0,0)add(51656,0,0)use(51656,0,0)packets(2828,0,0) idle=6
esp0x3350f552@192.168.1.1 ESP_3DES: dir=in ooowin=32 seq=115 bit=0xffffffff eklen=24 life(c,s,h)=bytes(13380,0,0)add(51656,0,0)use(54068,0,0)packets(115,0,0) idle=499
esp0x4450894d@192.168.1.2 ESP_3DES: dir=out ooowin=32 seq=2828 eklen=24 life(c,s,h)=bytes(381616,0,0)add(51656,0,0)use(51656,0,0)packets(2828,0,0) idle=6
tun0x105@192.168.1.1 IPIP: dir=in 192.168.1.2 -> 192.168.1.1 life(c,s,h)=add(51656,0,0)
tun0x106@192.168.1.2 IPIP: dir=out 192.168.1.1 -> 192.168.1.2 life(c,s,h)=bytes(327581,0,0)add(51656,0,0)use(51656,0,0)packets(2828,0,0) idle=6
192.168.1.0  0.0.0.0     255.255.255.0 U   0 0    0 eth0
192.168.1.0  0.0.0.0     255.255.255.0 U   0 0    0 ipsec0
192.168.1.1  0.0_range=0.0.0.0     255.255.255.255 UH  0 0    0 eth0
192.168.1.2  192.168.1.2 255.255.255.255 UGH 0 0    0 ipsec0
Destination  Gateway     Genmask      Flags MSS Window irtt Iface
```

- 尝试从`192.168.1.1`客户端 ping `192.168.1.2`。如果成功，则说明配置正确。如果不成功，请检查网络以确保`208.164.186.1`能够到达`208.164.186.2`，并且已启用 TCP-IP 转发，同时确保没有防火墙规则阻止数据包或尝试在允许 IPSec 相关流量的规则之前对其进行伪装。为了让此测试生效，重要的是使用从一个子网到另一个子网的 ping。

```
208.164.186.1 ---- 205.151.222.250 ---- 205.151.222.251 ---- 208.164.186.2

      |                                          |

192.168.1.0/24                              192.168.1.0/24

      |                                          |

192.168.1.1                                 192.168.1.2
```

关于测试 FreeSWAN IPSEC 的安装，最后说明一点：如果你遇到无法解决的问题，可以使用以下命令查看与 IPSEC 加密/认证系统相关的一组调试信息（文件内容、日志摘录等），你应将这些信息发送到 Linux-IPSEC 邮件列表（[linux-ipsec@clinet.fi](mailto:linux-ipsec@clinet.fi)）以寻求帮助。

- 使用以下命令输出调试信息集合：

```bash
[root@deep /]# ipsec barf > result
```

此命令主要便于远程调试；这是一个单一命令，可打包（并标记）所有可能与诊断 IPSEC 问题相关的信息。

## 更多文档

更多详细信息，请参阅以下手册页：

```
$ man ipsec (8)                         - invoke IPSEC utilities

$ man ipsec atoaddr, addrtoa (3)        - convert Internet addresses to and from ASCII

$ man ipsec atoasr (3)                  - convert ASCII to Internet address, subnet, or range

$ man ipsec atobytes, bytestoa (3)      - convert binary data bytes from and to ASCII formats

$ man ipsec atodata, datatoa (3)        - convert binary data from and to ASCII formats

$ man ipsec atosa, satoa (3)            - convert IPSEC Security Association IDs to and from ASCII

$ man ipsec atosubnet, subnettoa (3)    - convert subnet/mask ASCII form to and from addresses

$ man ipsec atoul, ultoa (3)            - convert unsigned-long numbers to and from ASCII

$ man ipsec auto (8)                    - control automatically-keyed IPSEC connections

$ man ipsec barf (8)                    - spew out collected IPSEC debugging information

$ man ipsec bitstomask (3)              - convert bit count to Internet subnet refrain

$ man ipsec eroute (8)                  - manipulate IPSEC extended routing tables

$ man ipsec goodmask (3)                - is this Internet subnet mask a valid one?

$ man ipsec hostof (3)                  - given Internet address and subnet mask, return host part

$ man ipsec klipsdebug (8)              - set Klips (kernel IPSEC support) debug features and level

$ man ipsec look (8)                    - show minimal debugging information

$ man ipsec manual (8)                  - take manually-keyed IPSEC connections up and down

$ man ipsec masktobits (3)              - convert Internet subnet mask to bit count

$ man ipsec optionsfrom (3)             - adh 古代的"command-line" options from file

$ man ipsec pluto (8)                   - IPsec IKE keying daemon

$ man ipsec ranbits (8)                  - generate random bits in ASCII form

$ man ipsec rangetoa (3)                - convert Internet address range to ASCII

$ man ipsec rsasigkey (8)               - generate RSA signature key

$ man ipsec setup (8)                   - control IPSEC subsystem

$ man ipsec spi (8)                     - manage IPSEC Security Associations

$ man ipsec spigrp (8)                  - group/ungroup IPSEC Security Associations

$ man ipsec subnetof (3)                - given Internet address and subnet mask, return subnet number

$ man ipsec tncfg (8)                   - associate IPSEC virtual interface with real interface

$ man ipsec whack (8)                   - control interface for IPSEC keying daemon

$ man ipsec.conf (5)                    - IPSEC configuration and connections

$ man ipsec.secrets (5)                 - secrets for IKE/IPsec authentication

$ man ipsec (8)                         - invoke IPSEC utilities

$ man ipsec atoaddr, addrtoa (3)        - convert Internet addresses to and from ASCII

$ man ipsec atoasr (3)                  - convert ASCII to Internet address, subnet, or range

$ man ipsec atobytes, bytestoa (3)       - convert binary data bytes from and to ASCII formats

$ man ipsec atodata, datatoa (3)         - convert binary data from and to ASCII formats

$ man ipsec atosa, satoa (3)             - convert IPSEC Security Association IDs to and from ASCII

$ man ipsec atosubnet, subnettoa (3)     - convert subnet/mask ASCII form to and from addresses

$ man ipsec atoul, ultoa (3)             - convert unsigned-long numbers to and from ASCII

$ man ipsec auto (8)                     - control automatically-keyrd IPSEC connections

$ man ipsec barf (8)                     - spew out collected IPSEC debugging information

$ man ipsec bitstomask (3)               - convert bit count to Internet subnet mask

$ man ipsec eroute (8)                   - manipulate IPSEC extended routing tables

$ man ipsec goodmask (3)                 - is this Internet subnet mask a valid one?

$ man ipsec hostof (3)                   - given Internet address and subnet mask, return host part

$ man ipsec klipsdebug (8)               - set Klips (kernel IPSEC support) debug features and level

$ man ipsec look (8)                     - show minimal debugging information

$ man ipsec manual (8)                   - take manually-keyed IPSEC connections up and down

$ man ipsec masktobits (3)               - convert Internet subnet mask to bit count

$ man ipsec optionsfrom (3)              - read additional "command-line" options from file

$ man ipsec plhtcado (8)                - IPsec IKE keying daemon

$ man ipsec ranbits (8)                  - generate random bits in ASCII form

$ man ipsec rangetoa (3)                - convert Internet address range to ASCII

$ man ipsec rsasigkey (8)                - generate RSA signature key

$ man ipsec setup (8)                   - control IPSEC subsystem

$ man ipsec spi (8)                     - manage IPSEC Security Associations

$ man ipsec spigrp (8)                   - group/ungroup IPSEC Security Associations

$ man ipsec subnetof (3)                 - given Internet address and subnet mask, return subnet number

$ man ipsec tncfg (8)                   - associate IPSEC virtual interface with real interface
```



## 相关手册页

`$ man ipsec whack (8)` - control interface for IPSEC keying daemon

`$ man ipsec.conf (5)` - IPSEC configuration and connections

`$ man ipsec.secrets (5)` - secrets enjectedfor IKE/IPsec authentication

## 已安装文件

- `/etc/rc.d/init.d/ipsec`
- `/etc/rc.d/rc0.d/K68ipsec`
- `/etc/rc.d/rc1.d/K68ipiscopalipv6.3`
- `/usr/man/man3/ipsec_atoasr.3ecrangetoa.3`
- `/usr/man/man3/ipsec_rangetoa.3`
- `/etc/rc.d/rc2.d/S47ipsec`
- `/etc/rc.d/rc3.d/S47ipsec`
- `/etc/rc.d/rc4.d/S47ipsec`
- `/etc/rc.d/rc5.d/S47ipsec`
- `/etc/rc.d/rc6.d/K68ipsec`
- `/etc/ipsec.conf`
- `/etc/ipsec.secrets`
- `/usr/lib/ipsec`
- `/usr/lib/ipsec/spi`
- `/usr/lib/ipsec/eroute`
- `/usr/lib/ipsec/spigrp`
- `/usr/lib/ipsec/tncfg`
- `/usr/lib/ipsec/klipsdebug`
- `/usr/lib/ipsec/pluto`
- `/usr/lib/ipsec/whack`
- `/usr/lib/ipsec/ipsec`
- `/usr/lib/ipsec/barf`
- `/usr/lib/ipsec/manual`
- `/usr/lib/ipsec/auto`
- `/usr/lib/ipsec/look`
- `/usr/lib/ipsec/showdefaults`
- `/usr/lib/ipsec/_include`
- `/usr/lib/ipsec/_confread`
- `/usr/lib/ipsec/_keycensor`
- `/usr/lib/ipsec/_secretcensor`
- `/usr/lib/ipsec/_updown`
- `/usr/lib/ipsec/ranbits`
- `/usr/lib/ipsec/rsasigkey`
- `/usr/lib/ipsec/setup`
- `/usr/man/man3/ipsec_atoaddr.3`
- `/usr/man/man3/ipsec_addrtoa.3`
- `/usr/man/man3/ipsec_atosubnet.3`
- `/usr/man/man3/ipsec_subnettoa.3`
- `/usr/man/man3/ipsec_atobytes.3`
- `/usr/man/man3/ipsec_bytestoa.3`
- `/usr/man/man3/ipsec_datatoa.3`
- `/usr/man/man3/ipsec_atosa.3`
- `/usr/man/man3/ipsec_satoa.3`
- `/usr/man/man3/ipsec_atoul.3`
- `/usr/man/man3/ipsec_ultoa.3`
- `/usr/man/man3/ipsec_goodmask.3`
- `/usr/man/man3/ipsec_masktobits.3`
- `/usr/man/man3/ipsec_bittomask.3`
- `/usr/man/man3/ipsec_optionsfrom.3`
- `/usr/man/man3/ipsec_subnetof.3`
- `/usr/man/man3/ipsec_hostof.3`
- `/usr/man/man3/ipsec_broadcastof.3`
- `/usr/man/man5/ipsec.secrets.5`
- `/usr/man/man5/ipsec.conf.5`
- `/usr/man/man8/ipsec_spi.8`
- `/usr/man/man8/ipsec.8`
- `/usr/man/man8/ipsec_eroute.8`
- `/usr/man/man8/ipsec_spigrp.8`
- `/usr/man/man8/ipsec_tncfg.8`
- `/usr/man/man8/ipsec_klipsdebug.8`
- `/usr/man/man8/ipsec_pluto.8`
- `/usr/man/man8/ipsec_whack.8`
- `/usr/man/man8/ipsec_barl.8`
- `/usr/man/man8/ipsec_look.8`
- `/usr/man/man8/ipsec_manual.8`
- `/usr/man/man8/ipsec_auto.8`
- `/usr/man/man8/ipsec_setup.8`
- `/usr/man/man8/ipsec_ranbits.8`
- `/usr/man/man8/ipsec_rsasigkey.8`
- `/usr/sbin/ipsec`

# 第17章 服务器软件（数据库网络服务）

## 本章内容

- Linux OpenLDAP 服务器
  - 配置
  - 保护 OpenLDAP
  - OpenLDAP 创建与维护工具
  - OpenLDAP 用户工具
  - 用于 LDAP 的 Netscape 通讯簿客户端
- Linux PostgreSQL 数据库服务器
  - 从 Postgres 超级用户账户创建数据库安装
  - 配置
  - 命令

## Linux OpenLDAP 服务器

### 概述

到目前为止，本书一直在讨论安全性和优化，那么为什么要讨论 OpenLDAP 呢？实际上，OpenLDAP 目录服务器将通过其多种可能性拓展我们的视野。我们可以利用其复制能力，将不同信息集中整合到一台服务器上，供网络中的其他服务器使用。想象一下，能够添加或禁用 Unix 或 NT 账户、设置对受限 Web 服务器的访问权限、添加邮件地址或别名，所有这些操作都可以通过一次操作完成，并以 NIS 服务的形式提供，同时具备 SSL 加密的安全性和面向对象层次结构的速度。另一个有趣的用途是在一个或多个 LDAP 服务器上创建员工权威列表，这些服务器可以从您的私有网络或互联网访问。

正如 OpenLDAP 网站所解释的：

LDAP（轻量级目录访问协议）是一种用于访问信息服务的开放标准协议。该协议运行在 Internet 传输协议之上，如 TCP，可用于访问独立目录服务器或 X.500 目录。

### 这些安装说明假设

- 命令与 Unix 兼容。
- 源代码路径为`/var/tmp`（其他路径也可）。
- 安装测试在 Red Hat Linux 6.1 和 6.2 上进行。
- 安装中的所有步骤都将以超级用户账户`root`执行。
- OpenLDAP 版本号为`1.2.10`。

### 软件包

OpenLDAP 主页：[http://www.openldap.org/](http://www.openldap.org/)

OpenLDAP FTP 站点：`204.152.186.57`

您必须确保下载：`openldap-1.2.10.tgz`

### Tarball 包

在安装 OpenLDAP 之前，最好先列出系统上的文件清单，安装后再列一个，然后使用`diff`进行比较，以找出软件安装的位置。只需在安装前运行`find /* > OpenLDAP1`，安装后运行`find /* > OpenLDAP2`，然后使用`diff OpenLDAP1 OpenLDAP2 > OpenLDAP-Installed`即可获得变更文件列表。

### 编译

解压 tarball 包（tar.gz）。

```bash
[root@deep /]# cp openldap-version.tgz /var/tmp
[root@deep /]# cd /var/tmp/
[root@deep tmp]# tar xzpf openldap-version.tgz
```

### 编译与优化

进入新的 OpenLDAP 目录，烧开后在终端中键入以下命令：

#### 步骤 1

需要注意的是，使用 LDAP 可以配置三种不同的后端数据库。一种是名为`LDBM`的高性能磁盘数据库；一种是名为`SHELL`的任意 UNIX 命令或 shell 脚本数据库接口；还有一种是名为`PASSWD`的简单密码文件数据库。

OpenLDAP 的默认安装假设使用 LDBM 后端数据库，因此如果您想配置其他类型的后端数据库，必须在配置和编译时指定。对于 SHELL 后端数据库，您必须在配置行中添加`--enable-shell`选项；对于 PASSWD 后端数据库（用作 NIS 服务的替代品），您必须在配置行中添加`--enable-passwd`选项。

```bash
CC="egcs" \
CFLAGS="-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -fomit-frame-pointer -fno-exceptions -D_REENTRANT" \
./configure \
--prefix=/usr \
--libexecdir=/usr/sbin \
--localstatedir=/var/run \
--sysconfdir=/etc \
--enable-dns \
--enable-shared \
--with-gnu-ld \
--disable-debug
```

**这指示 OpenLDAP 按照以下方式针对此特定硬件設置进行配置：**

- 启用 DNS 支持。
- 构建共享库。
- 假设 C 编译器使用 GNU ld。

**注意：**上面的编译选项假设您要设置 LDBM 后端数据库。对于其他类型的后端数据库，您必须在上述配置行中添加所需的选项。

#### 步骤 2

现在，我们必须在服务器中编译和安装 OpenLDAP：

```bash
[root@deep openldap-1.2.10]# make depend
[root@deep openldap-1.2.10]# make
[root@deep openldap-1.2.10]# cd tests/
[root@deep tests]# make
[root@deep tests]# cd ..
[root@deep openldap-1.2.10]# make install
```

`make depend`命令将构建不同文件所需的必要依赖关系，`make`将所有源文件编译为可执行二进制文件，然后`make install`将二进制文件和所有支持文件安装到适当的位置。

`/test`子目录下的`make`命令将在安装前执行一些重要测试，以验证您的 LDAP 服务器的功能。如果某些测试失败，您需要在继续安装之前修复问题。

```bash
[root@deep openldap-1.2.10]# install -d -m 700 /var/ldap
[root@deep openldap-1.2.10]# echo localhost > /etc/openldap/ldapserver
[root@deep openldap-1.2.10]# strip /usr/lib/liblber.so.1.0.0
[root@deep openldap-1.2.10]# strip /usr/lib/libldap.so.1.0.0
[root@deep openldap-1.2.10]# strip /usr/lib/libldap.a
[root@deep openldap-1.2.10]# strip /usr/lib/liblber.a
[root@deep openldap-1.2.10]# strip /usr/sbin/in.xfingerd
[root@deep openldap-1.2.10]# strip /usr/sbin/go500
[root@deep openldap-1.2.10]# strip /usr/sbin/go500gw
[root@deep openldap-1.2.10]# strip /usr/sbin/mail500
[root@deep openldap-1.2.10]# strip /usr/sbin/rp500
[root@deep openldap-1.2.10]# strip /usr/sbin/rcpt500
[root@deep openldap-1.2.10]# strip /usr/sbin/fax500
[root@deep openldap-1.2.10]# strip /usr/sbin/slapd
[root@deep openldap-1.2.10]# strip /usr/sbin/slurpd
[root@deep openldap-1.2.10]# strip /usr/sbin/ldif
[root@deep openldap-1.2.10]# strip /usr/sbin/ldif2ldbm
[root@deep openldap-1.2.10]# strip /usr/sbin/ldif2index
[root@deep openldap-1.2.10]# strip /usr/sbin/ldif2id2entry
[root@deep openldap-1.2.10]# strip /usr/sbin/ldif2id2children
[root@deep openldap-1.2.10]# strip /usr/sbin/ldbmcat
[root@deep openldap-1.2.10]# strip /usr/sbin/ldbmtest
[root@deep openldap-1.2.10]# strip /usr/sbin/centipede
[root@deep openldap-1.2.10]# strip /usr/bin/ud
[root@deep openldap-1.2.10]# strip /usr/bin/ldapadd
[root@deep openldap-1.2.10]# strip /usr/bin/ldapsearch
[root@deep openldap-1.2.10]# strip /usr/bin/ldapmodify
[root@deep openldap-1.2.10]# strip /usr/bin/ldapmodrdn
[root@deep openldap-1.2.10]# strip /usr/bin/ldappasswd
[root@deep openldap-1.2.10]# strip /usr/bin/ldapdelete
```

上面的`install`命令将在`/var`目录下创建名为`ldap`的新目录，并将其模式设置为仅允许超级用户`root`读取、写入和执行（700），以确保安全性。

`strip`命令将丢弃目标文件中的所有符号。这意味着我们的二进制文件将更小。这将提高程序的性能，因为系统执行二进制时需要读取的行数更少。

### 清理工作

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf openldap-version/ openldap-version.tgz
```

`rm`命令将删除我们用于编译和安装 OpenLDAP 的所有源文件。它还将从`/var/tmp`目录中删除 OpenLDAP 压缩包。

## 配置

本书中描述的所有软件在名为`floppy.tgz`的 tar 压缩归档文件中都有特定的目录和子目录，其中包含特定程序的配置文件。如果您获取此归档文件，就无需手动复制以下不同的配置文件，或剪切粘贴以创建您的配置文件。无论您决定手动复制它们，还是获取为您方便准备的归档文件，您都有责任修改、根据您的需求调整并将与 OpenLDAP 软件相关的文件放置在服务器上的适当位置，如下所示。要下载的服务器配置文件归档位于以下 Internet 地址：

[http://www.openna.com/books/floppy.tgz](http://www.openna.com/books/floppy.tgz)

- 要运行 OpenLDAP 服务器，以下文件是必需的，必须创建或复制到服务器上的适当目录。
- 将`slapd.conf`文件复制到`/etc/openldap/`目录。
- 将`ldap`脚本文件复制到`/etc/rc.d/init.d/`目录。

您可以在我们的`floppy.tgz`归档中获取下面列出的配置文件。从解压后的`floppy.tgz`归档中将以下文件复制到适当位置，或直接从本书中复制并粘贴到相关文件。

### `/etc/ldap/slapd.conf`文件的配置

`/etc/openldap/slapd.conf`文件是独立 LDAP 守护进程的主配置文件。权限、密码、数据库类型、数据库位置等选项都可以在此文件中配置，并适用于`slapd`守护进程整体。在下面的示例中，我们为 LDBM 后端数据库配置`slapd.conf`文件。

编辑`slapd.conf`文件（`vi /etc/openldap/slapd.conf`）并添加/调整以下信息：

```text
#
# See slapd.conf(5) for details on configuration options.
# This file should NOT be world readable.
#
include         /etc/openldap/slapd.at.conf
include         /etc/openldap/slapd.oc.conf
schemacheck     off
#referral        ldap://ldap.itd.umich.edu
pidfile         /var/run/slapd.pid
```



```conf
argsfile        /var/run/slapd.args

######################################################################

# ldbm database definitions

######################################################################

database        ldbm

suffix          "o=openna, c=com"

directory       /var/ldap

rootdn          "cn=admin, o=openna, c=com"

rootpw          secret

# cleartext passwords, especially for the rootdn, should

# be avoided. See slapd.conf(5) for details.

# ldbm 索引属性定义

index cn,sn,uid

index objectclass pres,eq

index default none

# ldbm 访问控制定义

defaultaccess read

access to attr=userpassword

	by self write

	by dn="cn=admin, o=openna, c=com" write

	by * compare
```

在启动 `slapd` 守护进程程序之前，你应该确保在 `slapd.conf` 文件中设置以下选项：

`suffix "o=openna, c=com"`

此选项指定你要创建的子树根的 DN。换句话说，它指示该数据库要保存哪些条目。

`directory /var/ldap`

此选项指定 LDAP 数据库和相关索引文件应存放的目录。我们必须将其设置为 `/var/ldap`，因为在安装阶段我们早期已创建此目录，专门用于处理 LDAP 的后端数据库。

`rootdn "cn=admin, o=openna, c=com"`

此选项指定允许对 LDAP 目录执行任何操作的条目的 DN。此处输入的名称可以是不存在于密码文件 `/etc/passwd` 中的名称。

`rootpw secret`

此选项指定可用于验证数据库“超级用户”条目的密码。这是上述 `rootdn` 选项的密码。重要的是不要在此处使用明文密码，而应使用加密密码。

`index cn,sn,uid`、`index objectclass pres,eq` 和 `index default none`

这些选项指定你要在数据库定义中构建和维护的索引定义。我们在上面的 `slapd.conf` 文件示例中指定的选项会导致为 `cn`、`sn` 和 `uid` 属性维护所有索引（`index cn,sn,uid`），为 `objectclass` 属性维护存在性和相等性索引（`index objectclass pres,eq`），而为所有其余属性不维护索引（`index default none`）。有关更多信息，请参阅用户手册。

`slapd.conf` 文件中的最后几个选项涉及 LDAP 目录中的访问控制。

```conf
defaultaccess read

access to attr=userpassword

	by self write

	by dn="cn=admin, o=openna, c=com" write

	by * compare
```

此示例适用于 `"o=openna, c=com"` 子树中的条目。向所有人授予读取权限，条目本身可以写入所有属性，但 `userpassword` 除外。`userpassword` 属性只能由指定的 `cn` 条目（admin）写入，其他所有人都可以进行比较。有关更多信息，请参阅用户手册。

## `/etc/rc.d/init.d/ldap` 脚本文件的配置

配置你的 `/etc/rc.d/init.d/ldap` 脚本文件以启动和停止 LDAP 服务器。

创建 `ldap` 脚本文件（`touch /etc/rc.d/init.d/ldap`）并添加：

```sh
#!/bin/sh

#

# ldap	This shell script takes care of starting and stopping

#	ldap servers (slapd and slurpd).

#

# chkconfig: - 70 40

# description: LDAP stands for Lightweight Directory Access Protocol, used \

#	for implementing the industry standard directory services.

# processname: slapd

# config: /etc/openldap/slapd.conf

# pidfile: /var/run/slapd.pid

# Source function library.

. /etc/rc.d/init.d/functions

# Source networking configuration.

. /etc/sysconfig/network

# Check that networking is up.

[ ${NETWORKING} = "no" ] && exit 0

[ -f /usr/sbin/slapd ] || exit 0

[ -f /usr/sbin/slurpd ] || exit 0

RETVAL=0

# See how we were called.

case "$1" in

  start)

	# Start daemons.

	echo -n "Starting ldap: "

	daemon slapd

	RETVAL=$?

	if [ $RETVAL -eq 0 ]; then

	  if grep -q "^replogfile" /etc/openldap/slapd.conf; then

		daemon slurpd

		RETVAL=$?

		[ $RETVAL -eq 0 ] && pidof slurpd | cut -f 1 -d " " > /var/run/slurpd

	  fi

	fi

	echo

	[ $RETVAL -eq 0 ] && touch /var/lock/subsys/ldap

	;;

  stop)

	# Stop daemons.

	echo -n "Shutting down ldap: "

	killproc slapd

	RETVAL=$?

	if [ $RETVAL -eq 0 ]; then

	  if grep -q "^replogfile" /etc/openldap/slapd.conf; then

		killproc slurpd

		RETVAL=$?

	  fi

	fi

	echo

	if [ $RETVAL -eq 0 ]; then

	  rm -f /var/lock/subsys/ldap

	  rm -f /var/run/slapd.args

	fi

	;;

  status)

	status slapd

	RETVAL=$?

	if [ $RETVAL -eq 0 ]; then

	  if grep -q "^replogfile" /etc/openldap/slapd.conf: then

	    status slurpd

	    RETVAL=$?

	  fi

	fi

	;;

  restart)

	$0 stop

	$0 start

	RETVAL=$?

	;;

  reload)

	killproc -HUP slapd

	RETVAL=$?

	if [ $RETVAL -eq 0 ]; then

	  if grep -q "^replogfile" /etc/openldap/slapd.conf; then

	    killproc -HUP slurpd

	    RETVAL=$?

	  fi

	fi

	;;

  *)

	echo "Usage: $0 start|stop|restart|status"

	exit 1

esac

exit $RETVAL
```

现在，使此脚本可执行并更改其默认权限：

```sh
[root@deep /]# chmod 700 /etc/rc.d/init.d/ldap
```

使用以下命令为 OpenLDAP 创建符号链接 `rc.d`：

```sh
[root@deep /]# chkconfig --add ldap
```

当你重新启动服务器时，OpenLDAP 脚本不会自动启动 `slapd` 守护进程。你可以通过执行以下命令来更改其默认设置：

```sh
[root@deep /]# chkconfig --level 345 ldap on
```

使用以下命令手动启动 OpenLDAP 服务器：

```text
[root@deep /]# /etc/rc.d/init.d/ldap start

Starting ldap:                [ OK ]
```

## 保护 OpenLDAP

### 保护重要的配置文件

不可变位（immutable bit）可用于防止意外删除或覆盖必须受保护的文件。它还可以防止某人创建指向此文件的符号链接。一旦你的 `slapd.conf` 文件配置完成，最好使用如下命令对其进行保护：

```sh
[root@deep /]# chattr +i /etc/openldap/slapd.conf
```

### 更多文档

有关更多详细信息，有几个手册页可供阅读：

- `man ldapd (8)` - LDAP X.500 协议守护进程
- `man ldapdelete (1)` - ldap 删除条目工具
- `man ldapfilter.conf (5)` - LDAP 获取过滤器例程的配置文件
- `man ldapfriendly (5)` - LDAP 友好例程的数据文件
- `man ldapmodify, ldapadd (1)` - ldap 修改条目和 ldap 添加条目工具
- `man ldapmodrdn (1)` - ldap 修改条目 RDN 工具
- `man ldappasswd (1)` - 更改 LDAP 条目的密码
- `man ldapsearch (1)` - ldap 搜索工具
- `man ldapsearchprefs.conf (5)` - LDAP 搜索偏好例程的配置文件
- `man ldaptemplates.conf (5)` - LDAP 显示模板例程的配置文件
- `man ldif (5)` - LDAP 数据交换格式
- `man slapd (8)` - 独立 LDAP 守护进程
- `man slapd.conf (5)` - `slapd`（独立 LDAP 守护进程）的配置文件
- `man slurpd (8)` - 独立 LDAP 更新复制守护进程
- `man ud (1)` - 交互式 LDAP 目录服务器查询程序

## OpenLDAP 创建和维护工具

### 创建 LDBM 后端数据库

创建 LDAP 数据库有两种方法，第一种是使用 `ldif2ldbm` 命令工具离线创建，另一种是使用 `ldapadd` 命令工具在线创建。通常，当你有成千上万个条目要插入数据库时使用离线方法，而当只有少量条目要放入数据库时使用在线方法。还需要注意，离线方法要求在执行时 `slapd` 守护进程未运行，而在线方法要求在执行时 LDAP 的 `slapd` 守护进程正在运行。

### 使用 `ldif2ldbm` 工具离线创建 LDBM 后端数据库

首先要做的是创建一个 LDIF 输入文件，其中包含条目的文本表示。下面名为 `my-data-file` 的文本文件可用作示例文件（当然，你的实际 LDIF 输入文件将处理比此示例多得多的信息）。当你首次安装 OpenLDAP 并有大量条目要放入后端数据库时，将所有这些信息放入文本文件并通过 `ldif2ldbm` 命令工具添加到后端数据库总是一个好主意。

**步骤 1**

创建 `my-data-file` 文件（`touch /tmp/my-data-file`）并在此文件中添加以下示例行：

```ldif
dn: o=openna, c=com

o: openna

objectclass: organization

dn: cn=Gerhard Mourani, o=openna, c=com

cn: Gerhard Mourani

sn: Mourani

mail: gmourani@videotron.ca

title: Author

objectclass: person

dn: cn=Anthony Bay, o=openna, c=com

cn: Anthony Bay

sn: Bay

homephone: (444) 111-2233

mobile: (444) 555-6677

mail: abay@openna.com

objectclass: person

dn: cn=George Parker, o=openna, c=com

cn: George Parker

sn: Parker

telephonenumber: (555) 234-5678

fax: (543) 987-6543

mobile: (543) 321-4354

description: E-Commerce

objectclass: person
```

上述示例展示了如何将信息转换为 LDIF 文件，然后再添加到新的后端目录中。参考 OpenLDAP 文档或相关书籍获取更多信息。

## 步骤 2

创建包含我们条目的 LDIF 输入文件后，必须将其插入 LDAP 目录服务器。

- 要插入 LDIF 输入文件并离线创建数据库，请使用以下命令：

  ```sh
  [root@deep tmp]# ldif2ldbm -i <inputfile> -f <slapdconfigfile>

  [root@deep tmp]# ldif2ldbm -i my-data-file -f /etc/openldap/slapd.conf
  ```

`-i` 选项与 `<inputfile>` 选项一起指定了包含文本形式条目的 LDIF 输入文件的位置。`<slapdconfigfile>` 选项指定了 `slapd` 配置文件的位置，该文件指定了在哪里创建索引、创建什么索引等。

**注意：**需要注意的是，在这种创建模式下，LDAP 的 `slapd` 守护进程**不会**启动。

### 使用 `ldapadd` 工具在线创建 LDBM 后端数据库

如果目录服务器中的条目已经创建，或者只有少量信息需要插入到后端数据库中，你可能更愿意使用 `ldapadd` 命令工具来在线完成工作。例如，要使用 `ldapadd` 工具添加“Europe Mourani”条目，你可以在 `/tmp` 目录中创建一个名为 `newentry` 的文件。

## 步骤 1

创建 `newentry` 文件（`touch /tmp/newentry`）并在该文件中添加以下内容：

```ldif
cn=Europe Mourani, o=openna, c=com

cn: Europe Mourani

sn: Mourani

mail: emourani@old.com

description: Marketing relation

objectClass: person
```

## 步骤 2

创建 `newentry` 文件后，必须将条目添加到 LDAP 目录服务器中。

- 要实际在后端数据库中在线创建条目，请使用以下命令：

  ```sh
  [root@deep /]# ldapadd -f /tmp/newentry -D "cn=admin, o=openna, c=com" -W

  Enter LDAP Password :
  ```

上述命令假设你已经将 `rootdn` 设置为 `"cn=admin, o=openna, c=com"`，并将 `rootpw` 设置为 `"secret"`。系统将提示你输入密码。

**注意：**需要注意的是，在这种创建模式下，LDAP 的 `slapd` 守护进程**会**启动。

## `ldapmodify`

与数据经常被更改的关系型数据库不同，目录服务器中包含的信息一旦插入后很少被修改。但有时你需要修改信息，`ldapmodify` 工具将帮助你完成这些任务。`ldapmodify` 命令允许你在后端目录服务器上添加或修改条目。

假设我们要将“Europe Mourani”条目的 `mail` 属性内容替换为新值 `emourani@new.com`，以下步骤是必需的：

## 步骤 1

创建 `modifyentry` 文件（`touch /tmp/modifyentry`）并在该文件中添加以下内容：

```text
cn=Europe Mourani, o=openna, c=com

- mail=emourani@old.com      # 将删除数据库中 Europe Mourani 的旧邮件地址。

+mail=emourani@new.com      # 将在数据库中为 Europe Mourani 添加新邮件地址。
```

## 步骤 2

创建 `modifyentry` 文件后，必须用该文件中包含的内容替换 LDAP 目录服务器中的条目。

- 要修改后端数据库的内容，请使用以下命令：

  ```sh
  [root@deep /]# ldapmodify -D 'cn=Admin, o=openna, c=com' -W -f <inputfile>

  [root@deep /]# ldapmodify -D 'cn=Admin, o=openna, c=com' -W -f modifyentry
  ```




其中`<inputfile>`是我们在上面的步骤1中创建的文件`modifyentry`的名称。

## OpenLDAP用户工具

### 在LDAP目录服务器中搜索条目

`ldapsearch`工具在LDAP目录的后端数据库中搜索你请求的信息。

- 要在LDAP目录中搜索条目，请使用以下命令：

```bash
[root@deep /]# ldapsearch -b 'dn' 'attrs'

[root@deep /]# ldapsearch -b 'o=openna, c=com' 'cn=europe*'

cn=Europe Mourani, o=openna, c=com

cn=Europe Mourani

sn=Mourani

mail=emourani@old.com

description=Marketing relation

objectClass=person
```

此命令将检索名字`europe`的所有条目和值，并将结果打印到你终端的标准输出。

### OpenLDAP软件的一些可能用途

OpenLDAP可以用作：

- 网络目录服务器。
- 白页服务器。
- 证书服务器。
- 访问控制服务器。

## 用于LDAP的Netscape通讯簿客户端

如果你在Linux工作站上安装了Netscape，或者其他类型的操作系统，你可以使用其通讯簿功能来访问刚刚在Linux上安装的LDAP目录服务器，并查询你的目录服务器以获取信息，就像你在Linux上使用`ldapsearch`命令工具一样。

如果你有兴趣这样做，请遵循以下简单步骤：

- 描述：开放网络架构
- LDAP服务器：208.164.186.3
- 服务器根：o=openna, c=com

现在你要做的就是向你的Linux上的LDAP目录服务器进行一些查询，使用名为“显示包含以下内容的名称:”的框来开始搜索，然后单击“搜索:”按钮获取结果。

Netscape通讯簿客户端程序。

## 已安装的文件

- `/etc/openldap`
- `/etc/openldap/ldap.conf`
- `/etc/openldap/ldap.conf.default`
- `/etc/openldap/ldapfilter.conf`
- `/etc/openldap/ldapfilter.conf.default`
- `/etc/openldap/ldaptemplates.conf`
- `/etc/openldap/ldaptemplates.conf.default`
- `/etc/openldap/ldapsearchprefs.conf`
- `/etc/openldap/ldapsearchprefs.conf.default`
- `/etc/openldap/slapd.conf`
- `/etc/openldap/slapd.conf.default`
- `/etc/openldap/slapd.at.conf`
- `/etc/openldap/slapd.at.conf.default`
- `/etc/openldap/slapd.oc.conf`
- `/etc/openldap/slapd.oc.conf.default`
- `/etc/openldap/ldapserver`
- `/etc/rc.d/init.d/ldap`
- `/etc/rc.d/rc0.d/K40ldap`
- `/etc/rc.d/rc1.d/K40ldap`
- `/etc/rc.d/rc2.d/K40ldap`
- `/etc/rc.d/rc3.d/S70ldap`
- `/etc/rc.d/rc4.d/S70ldap`
- `/etc/rc.d/rc5.d/S70ldap`
- `/etc/rc.d/rc6.d/K40ldap`
- `/usr/bin/ud`
- `/usr/bin/ldapsearch`
- `/usr/bin/ldapmodify`
- `/usr/bin/ldapdelete`
- `/usr/bin/ldapmodrdn`
- `/usr/bin/ldappasswd`
- `/usr/bin/ldapadd`
- `/usr/include/ldap.h`
- `/usr/include/lber.h`
- `/usr/include/ldap_cdefs.h`
- `/usr/include/disptmpl.h`
- `/usr/include/srchpref.h`
- `/usr/lib/liblber.so.1.0.0`
- `/usr/lib/liblber.so.1`
- `/usr/lib/liblber.so`
- `/usr/lib/liblber.la`
- `/usr/lib/liblber.a`
- `/usr/lib/libldap.so.1.0.0`
- `/usr/lib/libldap.so.1`
- `/usr/lib/libldap.so`
- `/usr/lib/libldap.la`
- `/usr/lib/libldap.a`
- `/usr/man/man1/ud.1`
- `/usr/man/man1/ldapdelete.1`
- `/usr/man/man1/ldapmodify.1`
- `/usr/man/man1/ldapadd.1`
- `/usr/man/man1/ldapmodrdn.1`
- `/usr/man/man1/ldappasswd.1`
- `/usr/man/man1/ldapsearch.1`
- `/usr/man/man3/cldap_close.3`
- `/usr/man/man3/cldap_open.3`
- `/usr/man/man3/cldap_search_s.3`
- `/usr/man/man3/cldap_setretryinfo.3`
- `/usr/man/man3/lber-decode.3`
- `/usr/man/man3/lber-encode.3`
- `/usr/man/man3/ldap_open.3`
- `/usr/man/man3/ldap_errlist.3`
- `/usr/man/man3/ldap_err2string.3`
- `/usr/man/man3/ldap_first_attribute.3`
- `/usr/man/man3/ldap_next_attribute.3`
- `/usr/man/man3/ldap_first_entry.3`
- `/usr/man/man3/ldap_next_entry.3`
- `/usr/man/man3/ldap_count_entries.3`
- `/usr/man/man3/ldap_friendly.3`
- `/usr/man/man3/ldap_friendly_name.3`
- `/usr/man/man3/ldap_free_friendlymap.3`
- `/usr/man/man3/ldap_get_dn.3`
- `/usr/man/man3/ldap_explode_dn.3`
- `/usr/man/man3/ldap_explode_dns.3`
- `/usr/man/man3/ldap_dn2ufn.3`
- `/usr/man/man3/ldap_is_dns_dn.3`
- `/usr/man/man3/ldap_get_values.3`
- `/usr/man/man3/ldap_get_values_len.3`
- `/usr/man/man3/ldap_value_free.3`
- `/usr/man/man3/ldap_value_free_len.3`
- `/usr/man/man3/ldap_count_values.3`
- `/usr/man/man3/ldap_count_values_len.3`
- `/usr/man/man3/ldap_getfilter.3`
- `/usr/man/man3/ldap_init_getfilter.3`
- `/usr/man/man3/ldap_init_getfilter_buf.3`
- `/usr/man/man3/ldap_getfilter_free.3`
- `/usr/man/man3/ldap_getfirstfilter.3`
- `/usr/man/man3/ldap_getnextfilter.3`
- `/usr/man/man3/ldap_setfilteraffixes.3`
- `/usr/man/man3/ldap_build_filter.3`
- `/usr/man/man3/ldap_modify.3`
- `/usr/man/man3/ldap_modify_s.3`
- `/usr/man/man3/ldap_mods_free.3`
- `/usr/man/man3/ldap_modrdn.3`
- `/usr/man/man3/ldap_modrdn_s.3`
- `/usr/man/man3/ldap_modrdn2.3`
- `/usr/man/man3/ldap_modrdn2_s.3`
- `/usr/man/man3/ldap_init.3`
- `/usr/man/man3/ldap_result.3`
- `/usr/man/man3/ldap_msgfree.3`
- `/usr/man/man3/ldap_search.3`
- `/usr/man/man3/ldap_search_s.3`
- `/usr/man/man3/ldap_search_st.3`
- `/usr/man/man3/ldap_searchprefs.3`
- `/usr/man/man3/ldap_init_searchprefs.3`
- `/usr/man/man3/ldap_init_searchprefs_buf.3`
- `/usr/man/man3/ldap_free_searchprefs.3`
- `/usr/man/man3/ldap_first_searchobj.3`
- `reports.3`
- `.3`
- `.3`
- `.3`
- `hard to forget.`

```javascript
if (condVar > someVal) {console.log("xxx")}
```

# 服务器软件（数据库网络服务）

## 第7章

- `/usr/man/man3/ldap.3`
- `/usr/man/man3/cldap.3`
- `/usr/man/man3/ldap_abandon.3`
- `/usr/man/man3/ldap_add.3`
- `/usr/man/man3/ldap_add_s.3`
- `/usr/man/man3/ldap_bind.3`
- `/usr/man/man3/ldap_bindsim.3`
- `/usr/man/man3/ldap_kerberos_bind_s.3`
- `/usr/man/man3/ldap_kerberos_bind1.3`
- `/usr/man/man3/ldap_kerberos_bind2.3`
- `/usr/man/man3/ldap_kerberos_bind2_s.3`
- `/usr/man/man3/ldap_unbind.3`
- `/usr/man/man3/ldap_unbind_s.3`
- `/usr/man/man3/ldap_set_rebind_proc.3`
- `/usr/man/man3/ldap_cache.3`
- `/usr/man/man3/ldap_enable_cache.3`
- `/usr/man/man3/ldap_disable_cache.3`
- `/usr/man/man3/ldap_destroy_cache.3`
- `/usr/man/man3/ldap_flush_cache.3`
- `/usr/man/man3/ldap_uncache_entry.3`
- `/usr/man/man3/ldap_uncache_request.3`
- `/usr/man/man3/ldap_set_cache_options.3`
- `/usr/man/man3/ldap_charset.3`
- `/usr/man/man3/ldap_stritera.3`
- `/usr/man/man3/ldap_enable_translation.3`
- `/usr/man/man3/ldap_translate_from_t61.3`
- `/usr/man/man3/ldap_translation_to_t61.3`
- `/usr/man/man3/ldap_t61_to_8859.3`
- `/usr/man/man3/ldap_8859_to_t61.3`
- `/usr/man/man3/ldap_compare.3`
- `/usr/man/man3/ldap_compare_s.3`
- `/usr/man/man3/ldap_delete.3`
- `/usr/man/man3/ldap_delete_s.3`
- `/usr/man/man3/ldap_disptmpl.3`
- `/usr/man/man3/ldap_init_templates.3`
- `/usr/man/man3/ldap_init_templates_buf.3`
- `/usr/man/man3/ldap_free_templates.3`
- `/usr/man/man3/ldap_first_disptmpl.3`
- `/usr/man/man3/ldap_next_disptmpl.3`
- `/usr/man/man3/ldap_oc2template.3`
- `/usr/man/man3/ldap_eqtattrs.3`
- `/usr/man/man3/ldap_first_tmplrow.3`
- `/usr/man/man3/ldap_next_tmplrow.3`
- `/usr/man/man3/ldap_first_tmplcol.3`
- `/usr/man/man3/ldap_next_tmplcol.3`
- `/usr/man/man3/ldap_entry2text.3`
- `/usr/man/man3/ldap_entry2text_search.3`
- `/usr/man/man3/ldap_vals2text.3`
- `/usr/man/man3/ldap_entry2html.3`
- `/usr/man/man3/ldap_entry2html_search.3`
- `/usr/man/man3/ldap_vals2html.3`
- `/usr/man/man3/ldap_error.3`
- `/usr/man/man3/ldap_perror.3`
- `/usr/man/man3/ld_errno.3`
- `/usr/man/man3/ldap_result2error.3`
- `/usr/man/man3/ldap_ufn_timeout.3`
- `/usr/man/man3/ldap_url.3`
- `/usr/man/man3/ldap_is_ldap_url.3`
- `/usr/man/man3/ldap_url_parse.3`
- `/usr/man/man3/ldap_free_urldesc.3`
- `/usr/man/man3/ldap_url_search.3`
- `/usr/man/man3/ldap_url_search_s.3`
- `/usr`

接下来，我们使用`mv`命令将与 PostgreSQL 相关的所有子目录和文件，分别从`/usr/include`和`/usr/lib`目录移动到`/usr/include/pgsql`和`/usr/lib/pgsql`目录。

`chown`命令将为`/var/lib/pgsql`目录设置正确的所有者和组权限。`strip`命令将丢弃目标文件中的所有符号。这意味着我们的二进制文件体积会更小。这将提升程序的性能，因为系统在执行二进制文件时需要读取的行数更少。

`rm`命令将删除`global1.description`和`local1_template1.description`文件，这些文件是我们的 PostgreSQL 程序所不需要的。

## 从 Postgres 超级用户账户创建数据库安装

一旦 PostgreSQL 安装到 Linux 服务器上，在启动 PostgreSQL 服务器之前，创建数据库安装是非常重要的。

- 要创建数据库安装，请使用以下命令：

```bash
[root@deep /]# su postgres
[postgres@deep /]$ initdb --pglib=/usr/lib/pgsql --pgdata=/var/lib/pgsql
```

我们正在使用用户名 postgres（uid=40）初始化数据库系统。该用户将拥有所有文件，并且也必须拥有服务器进程。

创建 Postgres 数据库系统目录`/var/lib/pgsql/base`

在`/var/lib/pgsql/base/template1`中创建模板数据库

在`/var/lib/pgsql/base`中创建全局类

将 template1 数据库添加到 pg_database...

清理 template1

创建公共 pg_user 视图

创建视图 pg_rules

创建视图 pg_views

创建视图 pg_tables

创建视图 pg_indexes

加载 pg_description

```bash
[postgres@deep /]$ chmod 640 /var/lib/pgsql/pg_pwd

[postgres@deep /]$ exit

exit

[root@deep /]#
```

`--pglib`命令将指定 PostgreSQL 的库目录在系统中的位置，`--pgdata`命令将指定此 Linux 安装的数据库文件必须存放的位置。

**注意：**不要以`root`身份创建数据库安装！这将是一个重大的安全漏洞。

## 工作完成后清理

```bash
[root@deep /]# cd /var/tmp

[root@deep tmp]# rm -rf postgresql-version/ postgresql-version.tar.gz
```

删除`egcs-c++-version.i386.rpm`包以节省空间。

```bash
[root@deep /]# rpm -e egcs-c++
```




`rm` 命令将删除我们用于编译和安装 PostgreSQL 的所有源文件。它还会从`/var/tmp`目录中删除 PostgreSQL 的压缩归档。

`rpm -e`命令将删除我们为编译 PostgreSQL 服务器而安装的 `egcs-c++` 包。请注意，`egcs-c++` 包仅在编译 PostgreSQL 等程序时才需要，在 PostgreSQL 成功编译后可以安全卸载。

## 配置

我们在本书中描述的所有软件，在名为`floppy.tgz`的 tar 压缩归档中都有特定的目录和子目录，其中包含特定程序的文件配置。如果你获取了此归档文件，就不必手动复制下面的不同配置文件，或者通过剪切粘贴来创建配置文件。无论你决定手动复制它们，还是从归档中获取为你准备好的文件，你都有责任修改、调整以适应你的需求，并将与 PostgreSQL 软件相关的文件放置到服务器上的适当位置，如下所示。服务器配置文件归档的下载地址位于以下互联网地址：<http://www.openna.com/books/floppy.tgz>

- 要运行 PostgreSQL 数据库服务器，需要以下文件，并且必须创建或复制到服务器上的适当目录。
- 将 `postgresql` 脚本文件复制到`/etc/rc.d/init.d/`目录。

你可以在我们的 `floppy.tgz` 归档中获取下列配置文件。从解压后的 `floppy.tgz` 归档中将以下文件复制到适当位置，或者直接从本书中复制粘贴到相关文件。

## `/etc/rc.d/init.d/postgresql`脚本文件的配置

配置你的`/etc/rc.d/init.d/postgresql`脚本文件，以启动和停止 PostgreSQL 服务器。

创建 `postgresql` 脚本文件（`touch /etc/rc.d/init.d/postgresql`）并添加：

```sh
#! /bin/sh

# postgresql  This is the init script for starting up the PostgreSQL
#             server
#
# chkconfig: 345 85 15
# description: Starts and stops the PostgreSQL backend daemon that handles \
#              all database requests.
# processname: postmaster
# pidfile: /var/run/postmaster.pid
#
# Source function library.
. /etc/rc.d/init.d/functions

# Get config.
. /etc/sysconfig/network

# Check that networking is up.
# Pretty much need it for postmaster.
[ ${NETWORKING} = "no" ] && exit 0

[ -f /usr/bin/postmaster ] || exit 0
```

## 服务器软件（数据库网络服务）

## 第 7 章

```sh
# This script is slightly unusual in that the name of the daemon (postmaster)
# is not the same as the name of the subsystem (postgresql)
# See how we were called.
case "$1" in

  start)

    echo -n "Checking postgresql installation: "

    # Check for the PGDATA structure

    if [ -f /var/lib/pgsql/PG_VERSION ] && [ -d /var/lib/pgsql/base/template1 ]
    then

    # Check version of existing PGDATA

        if [ `cat /var/lib/pgsql/PG_VERSION` != '6.5' ]
        then

              echo "old version. Need to Upgrade."

              echo "See /usr/doc/postgresql-6.5.2/README.rpm for more information."

              exit 1

        else

              echo "looks good!"

        fi

    # No existing PGDATA! Initdb it.

    else

        echo "no database files found."

        if [ ! -d /var/lib/pgsql ]
        then

              mkdir -p /var/lib/pgsql

              chown postgres.postgres /var/lib/pgsql

        fi

        su -l postgres -c '/usr/bin/initdb --pglib=/usr/lib/pgsql --pgdata=/var/lib/pgsql'

    fi

    # Check for postmaster already running...

    pid=`pidof postmaster`

    if [ $pid ]
    then

        echo "Postmaster already running."

    else

        #all systems go -- remove any stale lock files

        rm -f /tmp/.s.PGSQL.* > /dev/null

        echo -n "Starting postgresql service: "

        su -l postgres -c '/usr/bin/postmaster -i -S -D/var/lib/pgsql'

        sleep 1

        pid=`pidof postmaster`

        if [ $pid ]
        then

              echo -n "postmaster [$pid]"

              touch /var/lock/subsys/postgresql

              echo $pid > /var/run/postmaster.pid

              echo

        else

              echo "failed."

        fi

    fi

    ;;

  stop)

    echo -n "Stopping postgresql service: "

    killproc postmaster

    sleep 2

    rm -f /var/run/postmaster.pid

    rm -f /var/lock/subsys/postgresql

    echo

    ;;

  status)

    status postmaster

    ;;

  restart)

    $0 stop

    $0 start

    ;;

  *)

    echo "Usage: postgresql {start|stop|status|restart}"

    exit 1

esac

exit 0
```

现在，使此脚本可执行并更改其默认权限：

```sh
[root@deep /]# chmod 700 /etc/rc.d/init.d/postgresql
```

使用以下命令为 PostgreSQL 创建符号链接 `rc.d`：

```sh
[root@deep /]# chkconfig --add postgresql
```

使用以下命令手动启动你的新 PostgreSQL 服务器：

```text
[root@deep /]# /etc/rc.d/init.d/postgresql start

Checking postgresql installation: looks good!

Starting postgresql service: postmaster [22401]
```

## 命令

下列命令是我们经常使用的部分命令，但还有更多命令存在。查看 `man` 页面以获取更多详情和信息。

- 要在数据库中定义新用户，请运行 `createuser` 实用程序：

  ```text
  [root@deep /]# su postgres
  [postgres@deep /]$ createuser
  请输入要添加的用户名 ---> admin
  请输入用户的 postgres ID 或按回车键使用 unix 用户 ID：500 ->
  用户 "admin" 是否允许创建数据库 (y/n) y
  用户 "admin" 是否为超级用户？(y/n) y
  createuser：admin 已成功添加
  ```

- 要从数据库中删除用户，请运行 `destroyuser` 实用程序：

  ```text
  [root@deep /]# su postgres
  [postgres@deep /]$ destroyuser
  请输入要删除的用户名 ---> admin
  destroyuser：用户 admin 删除成功。
  ```

- 要创建新数据库，请运行 `createdb` 实用程序：

  ```text
  [root@deep /]# su postgres
  [postgres@deep /]$ createdb dbname
  ```

  （`dbname` 为数据库名称）。

  或者使用 Postgres 终端监视器程序（`psql`）：

  ```text
  [root@deep /]# su admin
  [admin@deep /]$ psql template1
  欢迎使用 POSTGRESQL 交互式 sql 监视器：
    请阅读 COPYRIGHT 文件了解 POSTGRESQL 的版权条款
  [PostgreSQL 6.5.3 on i686-pc-linux-gnu, compiled by egcs ]

  type \? for help on slash commands

  type \q to quit

  type \g or terminate with semicolon to execute query

  You are currently connected to the database: template1
  ```

```sql
template1=> create database foo;

CREATEDB
```

> **注意：** 客户端连接可以通过 `PG_DATA` 中的 `pg_hba.conf` 文件按 IP 地址和/或用户名进行限制。

其他有用的 Postgres 终端监控程序命令（`psql`）有：

要连接到新数据库，请使用命令：

```text
template1=> \c foo

connecting to new database: foo

foo=>
```

要创建表，请使用命令：

```sql
foo=> create table bar (i int4, c char(16));

CREATE

foo=>
```

要查看新表，请使用命令：

```text
foo=> \d bar

Table  = bar

+---------------------------+---------------------------+----------+

| Field                     | Type                      | Length   |

+---------------------------+---------------------------+----------+

| i                         | int4                      | 4        |

| c                         | char()                    | 16       |

+---------------------------+---------------------------+----------+

foo=>
```

要删除表、索引、视图，请使用命令：

```sql
foo=> drop table table_name;

foo=> drop index index_name;

foo=> drop view view_name;
```

**插入数据：**（一旦创建了表，就可以使用命令来填充它……）

```sql
foo=> insert into table_name (name_of_attr1, name_of_attr2, name_of_attr3)

foo=> values (value1, value2, value3);
```

## 已安装的文件

```text
> /etc/rc.d/init.d/postgresql

> /etc/rc.d/rc0.d/K15postgresql

> /etc/rc.d/rc1.d/K15postgresql

> /etc/rc.d/rc2.d/K15postgresql

> /etc/rc.d/rc3.d/S85postgresql

> /etc/rc.d/rc4.d/S85postgresql

> /etc/rc.d/rc5.d/S85postgresql

> /etc/rc.d/rc6.d/K15postgresql

> /Sony/bin/postgres

> /usr/bin/postmaster

> /usr/bin/ecpg

> /usr/bin/pg_id

> /usr/bin/pg_version

> /usr/bin/psql
```

```text
> /usr/man/manl/begin.1

> /usr/man/manl/close.1

> /usr/man/manl/cluster.1

> /usr/man/manl/commit.1

> /usr/man/manl/copy.1

> /usr/man/manl/create_aggregate.1

> /usr/man/manl/create_database.1

> /usr/man/manl/create_function.1

> /usr/man/manl/create_index.1

> /usr/man/manl/create_language.1

> /usr/man/manl/create_operator.1

> /usr/man/manl/create_rule.1

> /usr/man/manl/create_sequence.1

> /usr/man/manl/create_table.1
```



## 服务器软件（数据库网络服务）

- `/usr/bin/pg_dump`
- `/usr/bin/pg_dumpall`
- `/usr/bin/pg_upgrade`
- `/usr/bin/pg_passwd`
- `/usr/bin/cleardbdir`
- `/usr/bin/createdb`
- `/usr/bin/createlang`
- `/usr/bin/createuser`
- `/usr/bin/destroydb`
- `/usr/bin/destroylang`
- `/usr/bin/destroyuser`
- `/usr/bin/initdb`
- `/usr/bin/vacuumdb`
- `/usr/bin/initlocation`
- `/usr/bin/ipcclean`
- `/usr/include/lib`
- `/usr/include/lib/dllist.h`
- `/usr/include/pgsql`
- `/usr/include/pgsql/access`
- `/usr/include/pgsql/access/attnum.h`
- `/usr/include/pgsql/commands`
- `/usr/include/pgsql/commands/trigger.h`
- `/usr/include/pgsql/executor`
- `/usr/include/pgsql/executor/spi.h`
- `/usr/include/pgsql/libpq`
- `/usr/include/pgsql/libpq/pqcomm.h`
- `/usr/include/pgsql/libpq/libpq-fs.h`
- `/usr/include/pgsql/libpq++`
- `/usr/include/pgsql/libpq++/pgconnection.h`
- `/usr/include/pgsql/libpq++/pgdatabase.h`
- `/usr/include/pgsql/libpq++/pgtransdb.h`
- `/usr/include/pgsql/libpq++/pgcursordb.h`
- `/usr/include/pgsql/libpq++/pglobject.h`
- `/usr/include/pgsql/port`
- `/usr/include/pgsql/port/linux`
- `/usr/include/pgsql/utils`
- `/usr/include/pgsql/utils/geo_decls.h`
- `/usr/include/pgsql/utils/elog.h`
- `/usr/include/pgsql/utils/palloc.h`
- `/usr/include/pgsql/utils/mcxt.h`
- `/usr/include/pgsql/fmgr.h`
- `/usr/include/pgsql/os.h`
- `/usr/include/pgsql/config.h`
- `/usr/include/pgsql/c.h`
- `/usr/include/pgsql/postgres.h`
- `/usr/include/pgsql/postgres_ext.h`
- `/usr/include/pgsql/libpq-fe.h`
- `/usr/include/pgsql/libpq-int.h`
- `/usr/include/pgsql/ecpgerrno.h`
- `/usr/include/pgsql/ecpglib.h`
- `/usr/include/pgsql/ecpgtype.h`
- `/usr/include/pgsql/sqlca.h`
- `/usr/include/pgsql/libpq++.H`

- `/usr/lib/libpq.a`
- `/usr/lib/libpq.so.2.0`
- `/usr/lib/libpq.so.2`

_Order_

- `/usr/lib/libpq.so`
- `/usr/lib/libecpg.a`
- `/usr/lib/libecpg.so.3.0.0`
- `/usr/lib/libecpg.so.3`
- `/usr/lib/libecpg.so`
- `/usr/lib/libpq++.a`
- `/usr/lib/libpq++.so.3.0`
- `/usr/lib/libpq++.so.3`
- `/usr/lib/libpq++.so`
- `/usr/lib/plpgsql.so`
- `/usr/lib/pgsql`
- `/usr/lib/pgsql/global1.bki.source`
- `/usr/lib/pgsql/local1_template1.bki.source`
- `/usr/lib/pgsql/pg_geqo.sample`

- `/usr/man/manl/create_trigger.l`
- `/usr/man/manl/create_type.l`
- `/usr/man/manl/create_user.l`
- `/usr/man/manl/create_version.l`
- `/usr/man/manl/create_view.l`
- `/usr/man/manl/declare.l`
- `/usr/man/manl/delete.l`
- `/usr/man/manl/drop.l`
- `/usr/man/manl/drop_aggregate.l`
- `/usr/man/manl/drop_database.l`
- `/usr/man/manl/drop_function.l`
- `/usr/man/manl/drop_index.l`
- `/usr/man/manl/drop_language.l`
- `/usr/man/manl/drop_operator.l`
- `/usr/man/manl/drop_rule.l`
- `/usr/man/manl/drop_sequence.l`
- `/usr/man/manl/drop_table.l`
- `/usr/man/manl/drop_trigger.l`
- `/usr/man/manl/drop_type.l`
- `/usr/man/manl/drop_user.l`
- `/usr/man/manl/drop_view.l`
- `/usr/man/manl/end.l`
- `/usr/man/manl/explain.l`
- `/usr/man/manl/fetch.l`
- `/usr/man/manl/grant.l`
- `/usr/man/manl/insert.l`
- `/usr/man/manl/listen.l`
- `/usr/man/manl/load.l`
- `/usr/man/manl/lock.l`
- `/usr/man/manl/move.l`
- `/usr/man/manl/notify.l`
- `/usr/man/manl/reset.l`
- `/usr/man/manl/revoke.l`
- `/usr/man/manl/rollback.l`
- `/usr/man/manl/select.l`
- `/usr/man/manl/set.l`
- `/usr/man/manl/show.l`
- `/usr/man/manl/sql.l`
- `/usr/man/manl/update.l`
- `/usr/man/manl/vacuum.l`

- `/var/lib/pgsql`
- `/var/lib/pgsql/base`
- `/var/lib/pgsql/base/template1`
- `/var/lib/pgsql/base/template1/pg_proc`
- `/var/lib/pgsql/base/template1/pg_type`
- `/var/lib/pgsql/base/template1/pg_attribute`
- `/var/lib/pgsql/base/template1/pg_class`
- `/var/lib/pgsql/base/template1/pg_inherits`
- `/var/lib/pgsql/base/template1/pg_index`
- `/var/lib/pgsql/base/template1/pg_statistic`
- `/var/lib/pgsql/base/template1/pg_operator`
- `/var/lib/pgsql/base/template1/pg_opclass`
- `/var/lib/pgsql/base/template1/pg_am`
- `/var/lib/pgsql/base/template1/pg_amop`
- `/var/lib/pgsql/base/template1/pg_amproc`
- `/var/lib/pgsql/base/template1/pg_language`
- `/var/lib/pgsql/base/template1/pg_aggregate`
- `/var/lib/pgsql/base/template1/pg_ipl`
- `/var/lib/pgsql/base/template1/pg_inheritproc`
- `/var/lib/pgsql/base/template1/pg_rewrite`
- `/var/lib/pgsql/base/template1/pg_listener`
- `/var/lib/pgsql/base/template1/pg_description`
- `/var/lib/pgsql/base/template1/pg_attribute_relid_attnam_index`
- `/var/lib/pgsql/base/template1/pg_attribute_relid_attnum_index`
- `/var/lib/pgsql/base`
- `/var/lib/pgsql/base/template1/pg_attribute_attrelid_index`
- `/var/lib/pgsql/base/template1/pg_proc_oid_index`
- `/var/lib/pgsql/base/template1/pg_proc_proname_narg_type_index`
- `/var/lib/pgsql/base/template1/pg_proc_prosrc_index`
- `/var/lib/pgsql/base/template1/pg_type_oid_index`
- `/var/lib/pgsql/base/template1/pg_type_typname_index`

> `/usr/lib/pgsql/pg_hba.conf.sample`

> `/usr/man/man1/cleardbdir.1`

> `/usr/man/man XC{zh-TW} 5U-createdb ···· -C·C++>> continue >>`

> `/usr/include/pgsql/utils/geo_decls.h ·· ··0;31;49m`

;



```text
/usr/bin/destroylang
/usr/bin/destroyuser
/usr/bin/initdb
/usr/bin/vacuumdb
/usr/bin/initlocation
/usr/bin/ipcclean
/usr/include/lib
/usr/include/lib/dllist.h
/usr/include/pgsql
/usr/include/pgsql/access
...
/usr/lib/libpq.a
...
按任意键继续...
/usr/man/man3/catalogs.3
/usr/man/man3/libpq.3
...
/var/lib/pgsql
/var/lib/pgsql/base/template1/pg_proc
/var/lib/pgsql/base/template1/pg_type
/var/lib/pgsql/base/template1/pg_attribute
/var/lib/pgsql/base/template1/pg_class
/var/lib/pgsql/base/template1/pg_inherits
/var/lib/pgsql/base/template1/pg_index
/var/lib/pgsql/base/template1/ pg_statistic
/var/lib/pgsql/base/template1/pg_operator
...
按任意键继续...
/var/lib/pgsql/base/template1/pg_opclass
/var/lib/pgsql/base/template1/pg_am
/var/lib/pgsql/base/template1/pg_amop
/var/lib/pgsql/base/template1/pg_amproc
/var/lib/pgsql/base/template1/pg_language
/var/lib/pgsql/base/template1/pg_aggregate
/var/lib/pgsql/base/template1/pg_ipl
/var/lib/pgsql/base/template1/pg_inheritproc
/var/lib/pgsql/base/template1/pg_rewrite
...
按任意键继续...
/var/lib/pgsql/base/template1/pg_listener
/var/lib/pgsql/base/template1/pg_description
/var/lib/pgsql/base/template1/pg_attribute_relid_attnam_index
/var/lib/pgsql/base/template1/pg_attribute_relid_attnum_index
/var/lib/pgsql/base/template1/pg_attribute_attrelid_index
/var/lib/pgsql/base/template1/pg_proc_oid_index
/var/lib/pgsql/base/template1/pg_proc_proname_narg_type_index
/var/lib/pgsql/base/template1/pg_proc_prosrc_index
...
按任意键继续...
/var/lib/pgsql/base/template1/pg_type_oid_index
/var/lib/pgsql/base/template1/pg_type_typname_index
/usr/lib/pgsql/pg_hba.conf.sample
/usr/man/man1/cleardbdir.1
/usr/man/man1/created formerly createdb.1
/usr/man/man1/createuser.1
/usr/man/man1/destroydb.1
/usr/man/man1/destroyuser.1
/usr/man/man1/ecpg.1
/usr/man/man1/initdb.1
/usr/man/man1/initlocation.1
/usr/man/man1/ipcclean.1
/usr/man/man1/pg_dump.1
/usr/man/man1/pg_dumpall.1
/usr/man/man1/pg_passwd.1
/usr/man/man1/pg_upgrade.1
/usr/man/man1/postgres.1
/usr/man/man1/postmaster.1
/usr/man/man1/psql.1
/usr/man/man3/catalogs.3
/usr/man/man3/libpq.3
/usr/man/man5/pg_hba.conf.5
/usr/man/man/abort.l
/usr/man/man/alter_table.l
/usr/man/man/alter_user.l
/var/lib/pgsql/base/template1/pg_class_oid_index
/var/lib/pgsql/base/template1/pg_class_relname_index
/var/lib/pgsql/base/template1/pg_attrdef
/var/lib/pgsql/base/template1/pg_attrdef_adrelid_index
/var/lib/pgsql/base/template1/pg_relcheck
/var/lib/pgsql/base/template1/pg_relcheck_rcrelid_index
/var/lib/pgsql/base/template1/pg_trigger
/var/lib/pgsql/base/template1/pg_trigger_tgrelid_index
/var/lib/pgsql/base/template1/pg_description_objoid_index
/var/lib/pgsql/base/template1/PG_VERSION
/var/lib/pgsql/base/template1/pg_user
/var/lib/pgsql/base/template1/pg_rules
/var/lib/pgsql/base/template1/pg_views
/var/lib/pgsql/base/template1/pg_tables
/var/lib/pgsql/base/template1/pg_indexes
/var/lib/pgsql/pg_variable
/var/lib/pgsql/pg_database
/var/lib/pgsql/pg_shadow
/var/lib/pgsql/pg_group
/var/lib/pgsql/pg_log
/var/lib/pgsql/PG_VERSION
/var/lib/pgsql/pg_hba.conf
/var/lib/pgsql/pg_geqo.sample
/var/lib/pgsql/pg_pwd
...
```

# 第十八章 服务器软件（代理网络服务）

## Linux Squid 代理服务器

### 概述

代理服务器因其节省带宽、提升安全性和加快网页浏览速度的能力而日益普及。目前市面上只有少数代理服务器程序，它们主要有两个缺点：它们是商业软件，且不支持 ICP（ICP 用于在相邻缓存之间交换关于 URL 存在性的提示）。Squid 是代理缓存服务器的最佳选择，因为它功能强大、免费，并且可以使用 ICP 功能。

Squid 源自 ARPA 资助的 Harvest 研究项目中的“cached”软件，由美国国家应用网络研究实验室开发，并受美国国家科学基金会资助。Squid 提供高性能的 Web 客户端缓存，同时支持 FTP、Gopher 和 HTTP 数据对象。它将热点对象存储在 RAM 中，在磁盘上维护健壮的对象数据库，具有复杂的访问控制机制，并支持 SSL 协议用于代理安全连接。此外，它还可以与其他基于 Squid 的代理服务器进行层次化链接，以实现页面的流线型缓存。

在我们的编译和配置中，我们将把 Squid 配置为以 httpd-accelerator 模式运行，以从我们的 Web 服务器中获得更高的性能。在加速器模式下，Squid 服务器充当反向代理缓存：它接受客户端请求，如果可能的话直接从缓存中提供，或者作为反向代理向源服务器请求资源。此外，我们还将向您展示如何将 Squid 配置为代理缓存服务器，以便让企业网络中的所有用户都能使用 Squid 访问互联网。

### 这些安装说明假设

- 命令与 Unix 兼容。
- 源代码路径为`/var/tmp`（其他路径也可行）。
- 安装测试在 Red Hat Linux 6.1 和 6.2 上进行。
- 安装过程中的所有步骤都将使用超级用户账户`root`执行。
- Squid 版本号为`2.3.STABLE2`。

### 软件包

- Squid 主页：`http://www.squid-cache.org/`
- Squid FTP 站点：`204.144.128.89`
- 您必须确保下载：`squid-2.3.STABLE2-src.tar.gz`

### Tarball 包

在安装 Squid 之前，最好先列出系统上的文件清单，安装后再列一份，然后使用`diff`进行比较，以了解它将文件放置到了何处。只需在安装前运行`find / > Squid1`，安装后运行`find / > Squid2`，然后使用`diff Squid1 Squid2 > Squid-Installed`来获取变更列表。

### 编译

解压 tarball（tar.gz）。

```shell
[root@deep /]# cp squid-version.STABLEz-src.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf squid-version.STABLEz-src.tar.gz
```

## 配置与优化

### 第一步

Squid 代理服务器不能以超级用户`root`身份运行，因此我们必须创建一个无 shell 的特殊用户来运行 Squid 代理服务器。

```shell
[root@deep /]# useradd -d /cache/ -r -s /dev/null squid >/dev/null 2>&1
[root@deep /]# mkdir /cache/
[root@deep /]# chown -R squid.squid /cache/
```

首先，我们将用户`squid`添加到`/etc/passwd`文件中。然后，如果`/cache`目录不存在，则创建该目录（仅当它不存在时）。最后，我们将“cache”目录的所有者更改为用户`squid`。

注意：通常我们不需要执行命令`mkdir /cache/`，因为在 Linux 安装过程中对硬盘进行分区时，我们已经创建了这个目录。如果该分区不存在，则必须执行此命令来创建目录。

### 第二步

进入新创建的 Squid 目录，在终端中输入以下命令：

编辑`Makefile.in`文件（`vi +18 icons/Makefile.in`）并修改以下行：

```makefile
DEFAULT_ICON_DIR = $(sysconfdir)/icons
改为：
DEFAULT_ICON_DIR = $(libexecdir)/icons
```

我们将变量`sysconfdir`更改为`libexecdir`。通过此修改，Squid 的“icons”目录将位于`/usr/lib/squid`目录下。

编辑`Makefile.in`文件（`vi +34 src/Makefile.in`）并修改以下行：

```makefile
DEFAULT_CACHE_LOG = $(localstatedir)/logs/cache.log
改为：
DEFAULT_CACHE_LOG = $(localstatedir)/log/squid/cache.log

DEFAULT_ACCESS_LOG = $(localstatedir)/logs/access.log
改为：
DEFAULT_ACCESS_LOG = $(localstatedir)/log/squid/access.log

DEFAULT_STORE_LOG = $(localstatedir)/logs/store.log
改为：
DEFAULT_STORE_LOG = $(localstatedir)/log/squid/store.log

DEFAULT_PID_FILE = $(localstatedir)/logs/squid.pid
改为：
DEFAULT_PID_FILE = $(localstatedir)/run/squid.pid

DEFAULT_SWAP_DIR = $(localstatedir)/cache
改为：
DEFAULT_SWAP_DIR = /cache

DEFAULT_ICON_DIR = $(sysconfdir)/icons
改为：
DEFAULT_ICON_DIR = $(libexecdir)/icons
```



我们将`cache.log`、`access.log`和`store.log`文件的默认位置更改为`/var/log/squid`目录。然后，我们将 Squid 的`pid`文件放到`/var/run`目录下，最后，通过上面的变量`libexecdir`将 Squid 的`icons`目录定位到`/usr/lib/squid/icons`。

## 使用 GNU malloc 库提升 Squid 缓存性能

如果您的系统存在内存限制，Squid 的缓存性能将受到影响。为了缓解这个问题，您可以将 Squid 与外部 malloc 库（如 GNU malloc）链接。要让 Squid 使用 GNU malloc 作为外部库，请按照以下简单步骤操作：

### 软件包

GNU malloc 主页：http://www.gnu.org/order/ftp.html

您必须确保下载：`malloc.tar.gz`

```bash
[root@deep /]# cp malloc.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf malloc.tar.gz
```

### 第一步

通过在系统中执行以下命令来编译和安装 GNU malloc：

```bash
[root@deep tmp]# cd malloc
[root@deep malloc]# export CC=egcs
[root@deep malloc]# make
```

### 第二步

将`libmalloc.a`文件复制到您的系统库目录，并确保将其命名为`libgnump.a`。

```bash
[root@deep malloc]# cp libmalloc.a /usr/lib/libgnumalloc.a
```

### 第三步

将`malloc.h`文件复制到您的系统包含目录，并确保将其命名为`gnumalloc.h`。

```bash
[root@deep malloc]# cp malloc.h /usr/include/gnumalloc.h
```

随着`libgnumalloc.a`和`gnumalloc.h`文件安装到系统中，Squid 在编译时将自动检测到它们，并使用它们来提升其缓存性能。

## 编译与优化

### 第一步

返回新创建的 Squid 目录，在终端中输入以下命令：

```bash
CC="egcs" \
CFLAGS="-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
./configure \
--prefix=/usr \
--exec-prefix=/usr \
--bindir=/usr/sbin \
--libexecdir=/usr/lib/squid \
--localstatedir=/var \
--sysconfdir=/etc/squid \
--enable-delay-pools \
--enable-cache-digestssourcing \
--enable-poll \
--disable-ident-lookups \
--enable-truncate \
--enable-heap-replacement
```

这告诉 Squid 使用这些选项为特定的硬件配置进行设置：

- 使用 Squid 的延迟池功能来限制和控制用户的带宽使用。
- 使用缓存摘要（Cache Digests）来提高客户端响应时间和网络利用率。
- 启用`poll()`代替`select()`，因为`poll()`优于`select()`。
- 禁用`ident-lookups`以移除执行 Ident（RFC 931）查询的代码，并减少可能的拒绝服务攻击。
- 启用`truncate`以在删除缓存文件时获得一些性能提升。
- 使用 Squid 的堆替换功能，以便选择各种缓存替换算法，而非标准的 LRU 算法，从而获得更好的性能。详见下文更详细的说明。

### 第二步

现在，我们必须在服务器上编译和安装 Squid：

```bash
[root@deep squid-2.3.STABLE2]# make -f makefile
[root@deep squid-2.3.STABLE2]# make install
[root@deep squid-2.3.STABLE2]# mkdir -p /var/log/squid
[root@deep squid-2.3.STABLE2]# rm -rf /var/logs/
[root@deep squid-2.3.STABLE2]# chown squid.squid /var/log/squid/
[root@deep squid-2.3.STABLE2]# chmod 750 /var/log/squid/
[root@deep squid-2.3.STABLE2]# chmod 750 /cache/
[root@deep squid-2.3.STABLE2]# rm -f /usr/sbin/RunCache
[root@deep squid-2.3.STABLE2]# rm -f /usr/sbin/RunAccel
[root@deep squid-2.3.STABLE2]# strip /usr/sbin/squid
[root@deep squid-2.3.STABLE2]# strip /usr/sbin/client
[root@deep squid-2.3.STABLE2]# strip /usr/lib/squid/dnsserver
[root@deep squid-2.3.STABLE2]# strip /usr/lib/squid/unlinkd
[root@deep squid-2.3.STABLE2]# strip /usr/lib/squid/cachemgr.cgi
```

`make -f`命令将把所有源文件编译为可执行二进制文件，`make install`会将二进制文件和任何支持文件安装到适当的位置。`mkdir`命令将在`/var/log`下创建名为`squid`的新目录。`rm -rf`命令将删除`/var/logs`目录，因为该目录是为处理 Squid 的日志文件而创建的，而我们已将相关日志文件移到了`/var/log/squid`位置。`chown`会将`/var/log/squid`的所有者更改为 squid 用户，`chmod`命令则会出于安全考虑将`squid`和`cache`目录的权限设置为 (0750/drwxr-x---)。

请注意，我们删除了名为`RunCache`和`RunAccel`的小型脚本，它们分别以缓存模式或加速器模式启动 Squid，因为我们使用了一个更好的脚本`squid`，它位于`/etc/rc.d/init.d/`目录下，利用了 Linux System V 的优势。`strip`命令将减小二进制文件的大小以获得最佳性能。

## 工作后的清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf squid-version/ squid-version.STABLEz-src.tar.gz
```

```bash
[root@deep tmp]# rm -rf malloc/ malloc.tar.gz (如果你使用了 GNU malloc 外部库)
```

`rm`命令将删除我们 peppe 曾经用于编译和安装 Squid 以及 GNU malloc 的所有源代码文件。它还会从`/var/tmp`目录中删除 Squid 和 GNU malloc 的压缩归档文件。

## 配置

我们在本书中描述的所有软件都有一个特定的目录和子目录，位于名为`floppy.tgz`的 tar 压缩归档中，该归档包含用于特定程序的配置文件。如果你获取了这个归档文件，就不必手动复制以下不同的配置文件，或者通过剪贴粘贴来创建你的配置文件。无论你决定手动复制它们，还是从归档中获取为你准备好的文件，你都有责任根据你的需求进行修改、调整，并将与 Squid 软件相关的文件放置到服务器上的适当位置，如下所示。服务器配置文件归档的下载地址位于以下互联网地址：http://www.openna.com/books/floppy.tgz

要在`httpd-accelerator`模式下运行 Squid 服务器，以下文件是必需的，必须创建或复制到服务器上的适当目录中。

- 将`squid.conf`文件复制到`/etc/squid/`目录。
- 将`squid`脚本文件复制到`/etc/rc.d/init.d/`目录。
- 将`squid`文件复制到`/etc/logrotate.d/`目录。

要在代理缓存模式下运行 Squid 服务器，以下文件是必需的，必须创建或复制到服务器上的适当目录中。

- 将`squid.conf`文件复制到`/etc/squid/`目录。
- 将`squid`脚本文件复制到`/etc/rc.d/init.d/`目录。
- 将`squid`文件复制到`/etc/logrotate.d/`目录。

你可以在我们的`floppy.tgz`归档中获取下面列出的配置文件。将解压后的`floppy.tgz`归档中的以下文件复制到适当位置，或者直接从本书中复制粘贴到相关文件中。

## 将`/etc/squid/squid.conf`文件配置为`httpd-accelerator`模式

`squid.conf`文件用于设置和配置 Squid 代理服务器的所有不同选项。在下面的配置文件中，我们将把`/etc/squid/squid.conf`配置为`httpd-accelerator`模式。在这种加速模式下，如果 Web 服务器与 Squid 安装在同一台服务器上，你必须将其守护进程设置为在 81 端口运行。对于 Apache Web 服务器，你可以在其`httpd.conf`文件中将 (Port 80) 行改为 (Port 81)。如果 Web 服务器运行在你网络中的其他服务器上，像我们这样做，你可以为 Apache 保留相同的端口号 (80)，因为 Squid 将绑定到不同的 IP 地址，而那里 (80) 端口尚未被使用。

## 服务器软件（代理网络服务）

### 第 8 章

编辑`squid.conf`文件（`vi /etc/squid/squid.conf`）并添加/修改以下选项：

```conf
http_port 80
icp_port 0
acl QUERY urlpath_regex cgi-bin \?
no_cache deny QUERY
cache_mem 16 MB
cache_dir ufs /cache 200 16 256
emulate_httpd_log on
redirect_rewrites_host_header off
replacement_policy GDSF
acl all src 0.0.0.0/0.0.0.0
http_access allow all
cache_mgr admin@openna.com
cache_effective_user squid
cache_effective_group squid
httpd_accel_host 208.164.186.3
httpd_accel_port 80
log_icp_queries off
cachemgr_passwd my-secret-pass all
buffered_logs on
```

这告诉`squid.conf`文件为这种特定的配置设置进行如下配置：

### `http_port 80`

选项`http_port`指定 Squid 将监听 HTTP 客户端请求的端口号。如果你将此选项设置为 80 端口，客户端将产生连接到 Apache Web 服务器的错觉。由于我们以加速模式运行 Squid，我们必须监听 80 端口。

### `icp_port 0`

选项`icp_port`指定 Squid 将从相邻缓存发送和接收 ICP 请求的端口号。我们必须将此选项的值设置为 0 以禁用该功能，因为我们正在将 Squid 配置为 Web 服务器的加速模式。ICP 功能仅在具有多个同级缓存和父缓存的多级缓存环境中才需要。在加速模式配置中使用 ICP 会给 Squid 增加不必要的开销。

### `acl QUERY urlpath_regex cgi-bin \?`和`no_cache deny QUERY`

选项`acl QUERY urlpath_regex cgi-bin \?`和`no_cache deny QUERY`用于强制某些对象永远不被缓存，例如`cgi-bin`目录下的文件。这是一个安全特性。

### `cache_mem 16 MB`

选项`cache_mem`指定用于缓存所谓的：传输中对象、热对象、负缓存对象的内存（RAM）数量。这是一个优化特性。

需要注意的是，Squid 使用的内存可能远超你在此参数中指定的值，因此，如果你为 Squid 预留了 48 MB 空闲内存，你必须在这里填写 48/3 = 16 MB。

```conf
cache_dir ufs /cache 200 16 256
```

选项`cache_dir`按顺序指定：要使用的存储系统类型（ufs）、Squid 的缓存目录名称（`/cache`）、在此目录下使用的磁盘空间（以兆字节为单位，200 Mbytes）、要在缓存目录下创建的一级子目录数量（16 个一级目录），以及要在每个一级缓存目录下创建的二级子目录数量（256 个二级目录）。在加速模式下，此选项与你想要通过 Apache Web 服务器提供服务的文件的大小和数量直接相关。

```conf
emulate_httpd_log on
```

如果将选项`emulate_httpd_log`设置为`ON`，则指定 Squid 应模拟 Apache Web 服务器的日志文件格式。如果你希望使用 Webalizer 等第三方程序来分析 Web 服务器（httpd）日志文件，这将非常有用。

```conf
redirect_rewrites_host_header off
```

如果将选项`redirect_rewrites_host_header`设置为`OFF`，则告诉 Squid 不要重写重定向请求中的任何 Host: 头。如果你在加速模式下运行 Squid，建议将此选项设置为`OFF`。

```conf
replacement_policy GDSF
```

选项`replacement_policy`指定 Squid 在代理需要腾出磁盘空间时将使用的缓存策略，以确定缓存中的哪些对象需要被替换。如果在编译时未指定`--enable-heap-replacement`选项，则默认使用 Squid 的 LRU 策略。在我们的配置中，我们选择 GDSF（Greedy-Dual Size Frequency，贪婪双大小频率）策略作为默认策略。更多信息请参阅[http://www.hpl.hp.com/techreports/1999/HPL-1999-69.html](http://www.hpl.hp.com/techreports/1999/HPL-1999-69.html)和[http://fog.hpl.external.hp.com/techreports/98/HPL-98-173.html](http://fog.hpl.external.hp.com/techreports/98/HPL-98-173.html)。

```conf
acl all src 0.0.0.0/0.0.0.0 和 http_access allow all
```

选项`acl`和`http_access`指定并定义要应用于 Squid 代理服务器的访问控制列表。我们的`acl`和`http_access`选项不受限制，允许所有人连接到代理服务器，因为我们使用此代理来加速公共 Apache Web 服务器。有关在非加速模式下使用 Squid 的更多信息，请参阅你的 Squid 文档。

```conf
cache_mgr admin
```

选项`cache_mgr`指定负责 Squid 代理服务器的管理员的电子邮件地址。如果 Squid 遇到问题，此人将收到邮件。你可以在此选项中指定姓名或完整的电子邮件地址。

```conf
cache_effective_user squid 和 cache_effective_group squid
```

选项`cache_effective_user`和`cache_effective_group`指定缓存将运行在其上的 UID/GID。切记永远不要以`root`身份运行 Squid。在我们的配置中，我们使用 UID`squid`和 GID`squid`。

```conf
httpd_accel_host 208.164.186.3 和 httpd_accel_port 80
```

选项`httpd_accel_host`和`httpd_accel_port`向 Squid 指定真实 HTTP 服务器（即 Apache）的 IP 地址和端口号。在我们的配置中，真实 HTTP Web 服务器位于 IP 地址 208.164.186.3（[www.openna.com](http://www.openna.com)）和端口 (80)。`www.openna.com`是我们网络上的另一个主机名，由于 Squid 代理服务器与 Apache HTTP Web 服务器不在同一台主机上，我们可以将端口 (80) 用于我们的 Squid 代理服务器，将端口 (80) 用于我们的 Apache Web 服务器，而效果是完美的。

```conf
log_icp_queries off
```

`log_icp_queries`选项用于指定是否将 ICP（ICP 用于在相邻缓存之间交换有关 URL 存在性的提示）查询记录到`access.log`文件中Since we设由于我们在 Squid 加速器模式下不使用 ICP 功能，因此可以安全地将此选项设置为`OFF`。



```bash
cachemgr_passwd my-secret-pass all
```

`cachemgr_passwd` 选项指定访问 `cachemgr.cgi` 程序工具的操作时所需的密码。该 CGI 工具程序设计为通过 Web 界面运行，并输出有关 Squid 配置和性能的统计信息。`<my-secret-pass>` 是您选择的密码，关键字 `<all>` 指定将此密码设置为可用于该程序执行的所有操作。更多信息请参见本章后面的“Squid 的 `cachemgr.cgi` 程序工具”。

```bash
buffered_logs on
```

`buffered_logs` 选项如果设置为 `ON`，可以略微加快某些日志文件的写入速度。这是一个优化功能。

## `/etc/squid/squid.conf` 文件的代理缓存模式配置

对上面定义的用于 `httpd-accelerator` 模式运行的 `squid.conf` 文件进行一些小幅修改，我们就可以将 Squid 作为代理缓存服务器运行。使用代理缓存服务器，企业网络中的所有用户都通过 Squid 访问互联网。通过这种配置，您可以获得完全的控制权，并对可以查看、访问和下载的内容应用特殊策略。您还可以控制带宽使用、连接时间等。代理缓存服务器可以配置为企业的独立服务器，也可以与互联网上的其他代理服务器分层共享缓存。

下面的第一个示例向您展示如何将 Squid 配置为独立服务器，然后简要介绍缓存分层配置，即两个或更多代理缓存服务器通过相互提供文档来协作。

![](img/a3204f208d115df8d5f69e88ecf1a4ea_357_0.png)

编辑 `squid.conf` 文件（`vi /etc/squid/squid.conf`），并为作为独立服务器运行的代理缓存添加/修改以下选项：

```conf
http_port 8080
icp_port 0
acl QUERY urlpath_regex cgi-bin \?
no_cache deny QUERY
cache_mem 16 MB
cache_dir ufs /cache 200 16 256
```

```conf
redirect_rewrites_host_header off
replacement_policy GDSF
acl localnet src 192.168.1.0/255.255.255.0
acl localhost src 127.0.0.1/255.255.255.255
acl Safe_ports port 80 443 210 119 70 21 1025-65535
acl CONNECT method CONNECT
acl all src 0.0.0.0/0.0.0.0
http_access allow localnet
http_access allow localhost
http_access deny !Safe_ports
http_access deny CONNECT
http_access deny all
cache_mgr admin@openna.com
cache_effective_user squid
cache_effective_group squid
log_icp_queries off
cachemgr_passwd my-secret-pass all
buffered_logs on
```

与 `httpd-accelerator` 模式配置的主要区别是使用访问控制列表（ACL）。此功能允许您基于源 IP 地址（`src`）、目标 IP 地址（`dst`）、源域、目标域、时间等来限制访问。此功能存在多种类型，有关完整列表请参阅 `Squid.conf` 文件。最常用的四种类型如下：

```conf
acl  name      type      data
  |     |          |          |
acl some-name src a.b.c.d/e.f.g.h      # ACL 基于源 IP 地址限制访问
acl some-name dst a.b.c.d/e.f.g.h      # ACL 基于目标 IP 地址限制访问
acl some-name srcdomain foo.com        # ACL 基于源域限制访问
acl some-name dstdomain foo.com        # ACL 基于目标域限制访问
```

例如，要将 Squid 代理服务器的访问限制为仅允许内部客户端访问，并限制为特定的指定端口范围，类似以下的配置可以完成任务：

```conf
acl localnet src 192.168.1.0/255.255.255.0
acl localhost src 127.0.0.1/255.255.255.255
acl Safe_ports port 80 443 210 119 70 21 1025-65535
acl CONNECT method CONNECT
acl all src 0.0.0.0/0.0.0.0
http_access allow localnet
http_access allow localhost
http_access deny !Safe_ports
http_access deny CONNECT
http_access deny all
```

此 ACL 配置将允许来自私有 C 类 `192.168.1.0` 的所有内部客户端访问代理服务器；建议您也允许 `localhost` IP（服务器自身使用的特殊 IP 地址）访问代理。在我们选择了一系列端口（`80=http`、`443=https`、`210=wais`、`119=nntp`、`70=gopher`、`21=ftp`）供内部客户端访问互联网后，我们拒绝 `CONNECT` 方法以防止外部人员尝试连接到代理服务器，最后，我们拒绝代理服务器上的所有源 IP 地址和端口。

## 多级 Web 缓存

代理缓存的第二种方法是所谓的“多级 Web 缓存”，即您选择与互联网上的更多代理缓存服务器共享和协作。使用这种方法，您的组织使用许多其他代理缓存服务器的缓存，作为补偿，其他缓存服务器也可以使用您的缓存。需要注意的是，在这种情况下，代理缓存在层级中可以扮演两种不同的角色。它可以配置为 `sibling` 缓存，仅能提供其已有的文档；或者配置为 `parent` 缓存，能够从另一个缓存或直接从源获取文档。

![](img/a3204f208d115df8d5f69e88ecf1a4ea_359_0.png)

**注意：** 避免产生比不使用 Web 缓存更多的网络流量的一个好策略是选择多个 `sibling` 缓存和较少数量的 `parent` 缓存。

## 针对所有配置的 `/etc/rc.d/init.d/squid` 脚本文件配置

配置您的 `/etc/rc.d/init.d/squid` 脚本文件以启动和停止 Squid Internet Object Cache。此脚本已修改为在专有的 `/cache` 而非 `/var/spool/squid` 中设置 Squid 的交换缓存。

创建 `squid` 脚本文件（`touch /etc/rc.d/init.d/squid`）并添加：

```bash
#!/bin/bash
# squid       This shell script takes care of starting and stopping
#             Squid Internet Object Cache
#
# chkconfig: - 90 25
# description: Squid - Internet Object Cache. Internet object caching is \
#    a way to store requested Internet objects (i.e., data available \
#    via the HTTP, FTP, and gopher protocols) on a system closer to the \
#    requesting site than to the source. Web browsers can then use the \
#    local Squid cache as a proxy HTTP server, reducing access time as \
#    well as bandwidth consumption.
# pidfile: /var/run/squid.pid
# config: /etc/squidáv/squid.conf
```

```bash
PATH=/usr/bin:/sbin:/bin:/usr/sbin
export PATH
```

```bash
# Source function library.
. /etc/rc.d/init.d/functions
```

```bash
# Source networking configuration.
. /etc/sysconfig/network
```

```bash
# Check that networking is up.
[ ${NETWORKING} = "no" ] && exit 0
```

```bash
# check if the squid conf file is present
[ -f /etc/squid/squid.conf ] || exit 0
```

```bash
# determine the name of the squid binary
[ -f /usr/sbin/squid ] && SQUID=squid
[ -z "$SQUID" ] && exit 0
```

```bash
# determine which one is the cache_swap directory
CACHE_SWAP=`sed -e 's/#.*//'g' /etc/squid/squid.conf | \
    grep cache_dir | sed -e 's/cache_dir//' | \
    cut -d' ' -f 2`
[ -z "$CACHE_SWAP" ] && CACHE_SWAP=/cache
```

```bash
# default squid options
# -D disables initial dns checks. If you most likely will not to have an
#   internet connection when you start squid, uncomment this
#SQUID_OPTS="-D"
```

```bash
RETVAL=0
case "$1" in
start)
  echo -n "Starting $SQUID: "
  for adir in $CACHE_SWAP; do
    if [ ! -d $adir/00 ]; then
        echo -n "init_cache_dir $adir... "
        $SQUID -z -F 2>/dev/null
    fi
  done
  $SQUID $SQUID_OPTS &
  RETVAL=$?
  echo $SQUID
  [ $RETVAL -eq 0 ] && touch /var/lock/subsys/$SQUID
  ;;
```

```bash
stop)
  echo -n "Stopping $SQUID: "
  $SQUID -k shutdown &
  RETVAL=$?
  if [ $RETVAL -eq 0 ] ; then
    rm -f /var/lock/subsys/$SQUID
    while : ; do
        [ -f /var/run/squid.pid ] || break
        sleep 2 && echo -n "."
    done
    echo "done"
  else
    echo
  fi
  ;;
```

```bash
  reload)

  $SQUID $SQUID_OPTS -k reconfigure

  exit $?

  ;;

restart)

  $0 stop

  $0 start

  ;;

status)

  status $SQUID

  $SQUID -k check

  exit $?

  ;;

probe)

  exit 0;

  ;;

*)

  echo "Usage: $0 {start|stop|status|reload|restart}"

  exit 1

esac

exit $RETVAL
```

现在，将此脚本设置为可执行并修改其默认权限：

```bash
[root@deep /]# chmod 700 /etc/rc.d/init.d/squid
```

使用以下命令为 Squid 创建符号链接 `rc.d`：

```bash
[root@deep /]# chkconfig --add squid
```

默认情况下，当你重启 Red Hat Linux 服务器时，`squid` 脚本不会自动启动代理服务器。你可以通过执行以下命令来更改其默认设置：

```bash
[root@deep /]# chkconfig --level 345 squid on
```

使用以下命令手动启动你的新 Squid 代理服务器：

```bash
[root@deep /]# /etc/rc.d/init.d/squid start

Starting squid: init_cache_dir ufs... squid
```

## `/etc/logrotate.d/squid` 文件配置

配置你的 `/etc/logrotate.d/squid` 文件，使其每周自动轮转日志文件。

创建 `squid` 文件（`touch /etc/logrotate.d/squid`）并添加：

```conf
/var/log/squid/access.log {

  weekly

  rotate 5

  copytruncate

  compress

  notifempty

  missingok

}

/var/log/squid/cache.log {

  weekly

  rotate 5

  copytruncate

  compress

  notifempty

  missingok

}

/var/log/squid/store.log {

  weekly

  rotate 5

  copytruncate

  compress

  notifempty

  missingok

# This script asks squid to rotate its logs on its own.

# Restarting squid is a long process and it is not worth

# doing it just to rotate logs

  postrotate

    /usr/sbin/squid -k rotate

  endscript

}
```

## 保护 Squid 安全

### 对 Squid 缓存目录挂载进行更多控制

如果你在 Linux 系统的独立分区中创建了 Squid 的缓存目录（即 `/cache`），就像我们在安装设置过程中所做的那样，那么你可以使用 `noexec`、`nodev` 和 `nosuid` 特性来加强和巩固缓存安全性。这些特性可以在 `/etc/fstab` 文件中设置，以告诉系统不允许执行任何二进制文件（`noexec`），不解释字符或块特殊设备（`nodev`），以及不允许设置用户标识符或组标识符位生效（`nosuid`）在已挂载的文件系统上（在我们的例子中是 `/cache`）。将此步骤应用于 Squid 缓存所在的分区将有助于消除 DEV、SUID/SGID 以及执行任何二进制文件的可能性。

例如，假设 `/dev/sda8` 是系统中 Squid 的 `/cache` 目录所在的分区，你必须编辑 `fstab` 文件（`vi /etc/fstab`）并更改与 `/dev/sda8` 相关的行：

| `/dev/sda8` | `/cache` | `ext2` | `defaults` | `1 2` |
|---|---|---|---|---|
| `/dev/sda8` | `/cache` | `ext2` | `noexec,nodev,nosuid` | `1 2` |

改为：

**注意：** 你必须重新启动系统才能使更改生效。

### 对 `squid.conf` 等重要配置文件进行免疫处理

众所周知，不可变位（immutable bit）可用于防止删除、覆盖或创建指向文件的符号链接。一旦你的 `squid.conf` 文件配置完成，使用以下命令对其进行免疫处理是一个好主意：

```bash
[root@deep /]# chattr +i /etc/squid/squid.conf
```

## 优化 Squid

### `atime` 和 `noatime` 属性

`atime` 和 `noatime` 属性可用于在 Squid 缓存目录中获得可衡量的性能提升。有关此主题的更多信息，请参阅本书第 4 章“通用系统优化”。

### 物理内存

对于 Squid 来说，最重要的资源是物理内存。你的处理器不需要超快。磁盘系统将是主要的瓶颈，因此对于高容量缓存来说，高速磁盘非常重要。如果可能的话，不要使用 IDE 磁盘。

### Squid 的 `cachemgr.cgi` 程序工具

`cachemgr.cgi` 实用程序程序在你将 Squid 编译并安装到系统时默认可用，它设计为通过 Web 界面运行，并输出有关 Squid 配置和性能的各种统计信息。

该程序位于 `/usr/lib/squid` 目录下，你必须将其放入你的 `cgi-bin` 目录（例如，`/home/httpd/cgi-bin`）才能使用它。按照以下简单步骤来使用此程序。

#### 步骤 1

将 `cachemgr.cgi` 程序移动到你的 `cgi-bin` 目录：

```bash
[root@deep /]# mv /usr/lib/squid/cachemgr.cgi /home/httpd/cgi-bin
```



注意：我假设你的`cgi-bin`目录位于`/home/httpd/cgi-bin`；其他路径也有可能。此外，这个`cgi-bin`目录只有在你已经在系统上安装了 Apache Web 服务器的情况下才会存在。

## 步骤 2

将`cachemgr.cgi`程序放入你的`cgi-bin`目录后，你可以将 Web 浏览器指向以下地址（`http://my-web-server/cgi-bin/cachemgr.cgi`）以使用此程序的各种功能。

`<my-web-server>`是你的 Apache Web 服务器所在的地址，`<cachemgr.cgi>`是我们刚刚放入`cgi-bin`目录中的实用程序，用于显示我们的 Squid Linux 服务器的信息和配置。

如果你已在`squid.conf`文件中配置了对“条件的密码认证，那么在访问`cachemgr.cgi`程序之前，系统会要求你输入缓存主机（Cache Host）、缓存端口（Cache Port）、管理员名称（Manager name）和密码（Password）信息。有关更多信息，请参见上述`/etc/squid/squid.conf`文件的配置。

一旦服务器对你进行了认证，你将在 Web 浏览器界面中看到缓存管理器菜单（Cache Manager menu），你可以在其中检查和分析与你的 Squid 代理服务器相关的不同选项。

## Netscape 浏览器的 Squid 代理配置

如果你决定将 Squid 用作代理缓存服务器，并允许公司网络中的所有用户仅以这种模式使用 Squid 访问互联网，那么你必须指导用户的浏览器从你的 Squid 代理服务器获取对象，而不是直接从互联网检索。

使用 Netscape Communicator，请按照以下简单步骤操作：

1. 打开 Netscape Communicator。
2. 进入 Edit 菜单。
3. 点击 Preferences ...
4. 在左侧双击 Advanced 类别。
5. 点击 Proxies 子类别选项。
6. 在右侧选择 Manual proxy configuration 单选按钮。
7. 点击 View... 按钮。
8. 在相应框中填入你的代理服务器信息。

例如：

| Protocol | Proxy Server | Port |
|---|---|---|
| HTTP: | 208.164.186.1 | Port: 8080 |
| Security: | 208.164.186.1 | Port: 8080 |
| FTP: | 208.164.186.1 | Port: 8080 |
| Gopher: | 208.164.186.1 | Port: 8080 |
| WAIS: | 208.164.186.1 | Port: 8080 |

## 已安装的文件

- `/etc/squid`
- `/etc/squid/mib.txt`
- `/etc/squid/squid.conf.default`
- `/etc/squid/squid.conf`
- `/etc/squid/mime.conf.default`
- `/etc/squid/mime.conf`
- `/etc/squid/errors`
- `/etc/squid/errors/ERR_ACCESS_DENIED`
- `/etc/squid/errors/ERR_CACHE_ACCESS_DENIED`
- `/etc/squid/errors/ERR_CACHE_MGR_ACCESS_DENIED`
- `/etc/squid/errors/ERR_CANNOT_FORWARD`
- `/etc/squid/errors/ERR_CONNECT_FAIL`
- `/etc/squid/errors/ERR_DNS_FAIL`
- `/etc/squid/errors/ERR_FORWARDING_DENIED`
- `/etc/squid/errors/ERR_FTP_DISABLED`
- `/etc/squid/errors/ERR_FTP_FAILURE`
- `/etc/squid/errors/ERR_FTP_FORBIDDEN`
- `/etc/squid/errors/ERR_FTP_NOT_FOUND`
- `/etc/squid/errors/ERR_FTP_PUT_CREATED`
- `/etc/squid/errors/ERR_FTP_PUT_ERROR`
- `/etc/squid/errors/ERR_FTP_PUT_MODIFIED`
- `/etc/squid/errors/ERR_FTP_UNAVAILABLE`
- `/etc/squid/errors/ERR_INVALID_REQ`
- `/etc/squid/errors/ERR_INVALID_URL`
- `/etc/squid/errors/ERR_LIFETIME_EXP`
- `/etc/squid/errors/ERR_NO_RELAY`
- `/etc/squid/errors/ERR_ONLY_IF_CACHED_MISS`
- `/etc/squid/errors/ERR_READ_ERROR`
- `/etc/squid/errors/ERR_READ_TIMEOUT`
- `/etc/rc.d/rc4.d/S90squid`
- `/etc/rc.d/rc5.d/S90squid`
- `/etc/rc.d/rc6.d/K25squid`
- `/etc/logrotate.d/squid`
- `/usr/lib/squid`
- `/usr/lib/squid/dnsserver`
- `/usr/lib/squid/unlinkd`
- `/usr/lib/squid/cachemgr.cgi`
- `/usr/lib/squid/icons`
- `/usr/lib/squid/icons/anthony-binhex.gif`
- `/usr/lib/squid/icons/anthony-bomb.gif`
- `/usr/lib/squid/icons/anthony-box.gif`
- `/usr/lib/squid/icons/anthony-box2.gif`
- `/usr/lib/squid/icons/anthony-c.gif`
- `/usr/lib/squid/icons/anthony-compress.gif`
- `/usr/lib/squid/icons/anthony-dir.gif`
- `/usr/lib/squid/icons/anthony-dirup.gif`
- `/usr/lib/squid/icons/anthony-dvi.gif`
- `/usr/lib/squid/icons/anthony-f.gif`
- `/usr/lib/squid/icons/anthony-image.gif`
- `/usr/lib/squid/icons/anthony-image2.gif`
- `/usr/lib/squid/icons/anthony-layout.gif`
- `/usr/lib/squid/icons/anthony-link.gif`
- `/usr/lib/squid/icons/anthony-movie.gif`
- `/usr/lib/squid/icons/anthony-pdf.gif`
- `/usr/lib/squid/icons/anthony-portal.gif`
- `/usr/lib/squid/icons/anthony-ps.gif`
- `/usr/lib/squid/icons/anthony-quill.gif`
- `/usr/lib/squid/icons/anthony-script.gif`

# 服务器软件（代理网络服务）

## 第 8 章

- `/etc/squid/errors/ERR_SHUTTING_DOWN`
- `/etc/squid/errors/ERR_SOCKET_FAILURE`
- `/etc/squid/errors/ERR_TOO_BIG`
- `/etc/squid/errors/ERR_UNSUP_REQ`
- `/etc/squid/errors/ERR_URN_RESOLVE`
- `/etc/squid/errors/ERR_WRITE_ERROR`
- `/etc/squid/errors/ERR_ZERO_SIZE_OBJECT`
- `/etc/rc.d/init.d/squid`
- `/etc/rc.d/rc0.d/K25squid`
- `/etc/rc.d/rc1.d/K25squid`
- `/etc/rc.d/rc2.d/K25squid`
- `/etc/rc.d/rc3.d/S90squid`
- `/usr/lib/squid/icons/anthony-sound.gif`
- `/usr/lib/squid/icons/anthony-tar.gif`
- `/usr/lib/squid/icons/anthony-tex.gif`
- `/usr/lib/squid/icons/anthony-text.gif`
- `/usr/lib/squid/icons/anthony-unknown.gif`
- `/usr/lib/squid/icons/anthony-xbm.gif`
- `/usr/lib/squid/icons/anthony-xpm.gif`
- `/usr/sbin/RunCache`
- `/usr/sbin/RunAccel`
- `/usr/sbin/squid`
- `/usr/sbin/client`
- `/var/log/squid`

# 第 19 章：服务器软件（Web 网络服务）

## 本章内容

- Linux MM – 共享内存库
- Linux Apache Web 服务器
  - 配置
  - PHP4 服务器端脚本语言
  - Perl 模块 `Devel::Symdump`
  - `CGI.pm` Perl 库
  - 保护 Apache 安全
  - 在 `chroot` 环境中运行 Apache
  - 优化 Apache

## Linux MM – Apache 共享内存库

### 概述

如果您打算安装并使用带有第三方模块的 Apache Web 服务器，例如用于加密数据的 `mod_ssl`、用于 Perl 编程语言的 `mod_perl`，或用于 PHP 服务器端脚本语言的 `mod_php`，我推荐您编译并安装这个小程序。该程序将为 Apache 模块提供显著的性能提升。例如，如果您需要在 Internet 上为电子商务安装支持 SSL 的 Apache，这将允许 SSL 协议使用高性能的基于 RAM 的会话缓存，而不是基于磁盘的缓存。

正如 MM 共享内存库网站所解释的那样：

MM 库是一个双层抽象库，它简化了 Unix 平台下 `fork` 出的（以及在本例中密切相关的）进程之间共享内存的使用。在第一层，它隐藏了处理共享内存段时所有与平台相关的实现细节（分配和锁定）；在第二层，它提供了高层级的 `malloc(3)` 风格 API，以便用一种方便且众所周知的方式在这些共享内存段内操作数据结构。

该库以开源（BSD 风格）许可证发布，因为它最初是作为一个提案而编写的，用于 Apache Web 服务器的下一版本内部，作为向 Apache 模块提供共享内存池的基础库（因为目前，Apache 模块只能使用堆分配的内存，这无法跨 pre-fork 的服务器进程共享）。这一需求实际上来自 `mod_ssl`、`mod_perl` 和 `mod_php` 等综合模块，它们将从易于使用的共享内存池中获益良多。

## 这些安装说明假设

- 命令与 Unix 兼容。
- 源码路径为`/var/tmp`（其他路径也可行）。
- 安装测试在 Red Hat Linux 6.1 和 6.2 上进行。
- 安装的所有步骤均在超级用户账号`root`下执行。
- MM 版本号为 1.1.2。

## 软件包

MM 主页：`http://www.engelschall.com/sw/mm/`

您必须确保下载：`mm-1.1.2.tar.gz`

## Tarballs

在安装 MM 之前，最好列出系统上的文件清单，安装后再列一次，然后使用`diff`比较，找出文件都放在了哪里。只需在安装前运行`find / > MM1`，安装后运行`find / > MM2`，然后使用`diff MM1 MM2 > MM-Installed`即可获取变更列表。

## 编译

解压 tarball（tar.gz）。

```bash
[root@deep /]# cp mm-version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf mm-version.tar.gz
```

## 编译

### 步骤 1

进入新的 mm 目录，在终端中输入以下命令：

```bash
./configure \
  --disable-shared \
  --prefix=/usr
```

这告诉 MM 根据此特定硬件设置进行配置：

- 禁用共享库。

### 步骤 2

现在，我们必须在服务器上编译并安装 MM 共享内存库：

```bash
[root@deep mm-1.1.2]# make
[root@deep mm-1.1.2]# make test
[root@deep mm-1.1.2]# make install
```

**注意：**`make test`命令将对程序进行一些重要测试，以验证其是否正常工作，并在安装前正确响应。

## 工作后的清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf mm-version/ mm-version.tar.gz
```

`rm`命令将删除我们用于编译和安装 mm 的所有源文件。它还将从`/var/tmp`目录中删除 mm 的压缩归档文件。

## 进一步文档

有关更多详情，您可以阅读以下几个 man 页面：

- MM (3) – 共享内存库
- `mm-config` (1) – MM 库配置/构建工具

## 已安装文件

```text
/usr/bin/mm-config
/usr/include/mm.h
/usr/lib/libmm.la
/usr/lib/libmm.a
/usr/man/man1/mm-config.1
/usr/man/man3/mm.3
```




# Linux Apache Web 服务器

## 概述

Apache 是当今世界上使用最广泛的 HTTP 服务器。它超越了市场上所有免费和商业竞争对手，提供了数不胜数的特性，比最近的竞争对手在 UNIX 变体上能提供的功能多得多。它也是 Linux 系统上使用最多的 Web 服务器。像 Apache 这样的 Web 服务器，其最简单功能是作为软件将托管在服务器上的 HTML 页面显示并提供给理解 HTML 代码的客户端浏览器。与第三方模块和程序结合使用，它可以成为功能强大的软件，为客户端浏览器提供强大且有用的服务。

我预期阅读本书的大多数用户会特别想了解如何以最安全、最优化的方式安装 Apache Web 服务器。在基础安装中，Apache 并不比我们在 Linux 服务器上安装的其他软件更难安装。当我们想要添加一些第三方模块或程序时，操作可能会变得复杂。安装 Apache 有很多可能性、变体和选项。因此，在下文中，我们提供了一些分步示例，您可以看到如何将 Apache 与其他第三方模块和程序一起构建，例如 `mod_ssl`、`mod_perl`、PHP4、LDAP 连接等。当然，构建这些程序是可选的，您可以自由编译您想要的任何内容（即，您可能想要编译支持 PHP4 的 Apache，但不需要 SSL 或 PostgreSQL 数据库连接）。为简化起见，我们对每个示例做了一些假设。如果这些不符合您的情况，只需调整步骤即可。

在本章中，我们解释并涵盖了一些基本的配置调整方式，以提高服务器性能。此外，对于感兴趣的用户，我们将提供一个程序，以便能够以非 root 用户身份运行 Apache，并在 chroot 环境中运行以获得最佳安全性。

## 这些安装说明假设

- 命令与 Unix 兼容。
- 源码路径为`/var/tmp`（其他路径也可行）。
- 安装测试在 Red Hat Linux 6.1 和 6.2 上进行。
- 安装的所有步骤均在超级用户账号`root`下执行。
- Apache 版本号为 1.3.12。
- Mod_SSL 版本号为 2.6.4-1.3.12。
- Mod_Perl 版本号为 1.24。
- Mod_PHP 版本号为 4.0.0。

## 软件包

Apache 主页：<http://www.apache.org/>

Apache FTP 站点：`63.211.145.10`

您必须确保下载：`apache_1.3.12.tar.gz`

Mod_SSL 主页：<http://www.modssl.org/>

Mod_SSL FTP 站点：`129.132.7.171`

您必须确保下载：`mod_ssl-2.6.4-1.3.12.tar.gz`

Mod_Perl 主页：<http://perl.apache.org/>

Mod_Perl FTP 站点：`63.211.145.10`

您必须确保下载：`mod_perl-1.24.tar.gz`

Mod_PHP 主页：<http://www.php.net/>

您必须确保下载：`php-4.0.0.tar.gz`

## 前提条件

- 如果您需要 Apache 和 SSL 加密支持，OpenSSL 应该已经安装在您的系统上。
- 如果您需要 Apache 和 PostgreSQL 数据库连接支持，PostgreSQL 应该已经安装在您的系统上。
- 如果您需要 Apache 和 MM 高性能基于 RAM 的会话缓存支持，MM 应该已经安装在您的系统上。
- 如果您需要 Apache 和 LDAP 目录连接支持，OpenLDAP 应该已经安装在您的系统上。
- 如果您需要 Apache 和 IMAP & POP 功能，IMAP & POP 应该已经安装在您的系统上。

**注意：**有关所需软件的更多信息，请参阅本书的相关章节。

## Tarballs

在安装 Apache 之前，最好列出系统上的文件清单，安装后再列一次，然后使用`diff`比较，找出文件都放在了哪里。只需在安装前运行`find / > Apache1`，安装后运行`find / > Apache2`，然后使用`diff Apache1 Apache2 > Apache-Installed`即可获取变更列表。

## 编译

解压 tarballs（tar.gz）。

```bash
[root@deep /]# cp apache_version.tar.gz /var/tmp
[root@deep /]# cp mod_ssl-version-version.tar.gz /var/tmp
[root@deep /]# cp mod_perl-version.tar.gz /var/tmp
[root@deep /]# cp php-version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp/
[root@deep tmp]# tar xzpf apache_version.tar.gz
[root@deep tmp]# tar xzpf mod_ssl-version-version.tar.gz
[root@deep tmp]# tar xzpf mod_perl-version.tar.gz
[root@deep tmp]# tar xzpf php-version.tar.gz
```

## 编译与优化

### 步骤 1：创建 Apache 用户

Apache Web 服务器与我们将会安装的许多应用程序一样，不能以超级用户 root 身份运行。因此，我们必须创建一个具有最小系统访问权限的特殊用户，但仍具备足以运行 Apache Web 服务器的功能。最好选择并专门创建一个仅用于运行 Web 服务器守护进程的新用户。

```bash
[root@deep /]# useradd -c "Apache Server" -u 80 -s /bin/false -r -d /home/httpd www 2>/dev/null || :
```

### 步骤 2：将 mod_ssl 应用到 Apache 源码树

如果你想在 Apache Web 服务器中使用并包含 SSL 数据加密支持，则进入 mod_ssl 源码目录（`cd mod_ssl-version-version/`），并在终端中输入以下命令：

```bash
CC="egcs" \
CFLAGS="-O9 -funroll-loops -ffast-malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
./configure \
--with-apache=../apache_1.3.12 \
--with-crt=/etc/ssl/certs/server.crt \
--with-key=/etc/ssl/private/server.key
```

`--with-apache`选项指定 Apache 源码目录的位置（需要注意的是，本示例中我们假设你的 Apache 版本为 1.3.12），`--with-crt`选项指定用于 SSL 加密的现有公钥位置，`--with-key`选项指定用于 SSL 加密的现有私钥位置。

> 注意：OpenSSL 软件必须已经安装在你的服务器上，并且你的公钥和私钥必须已经存在或在服务器上创建，否则在 mod_ssl 配置期间你将收到错误消息。有关更多信息，请参阅本书第 16 章"服务器软件（加密网络服务）"。

### 步骤 3：优化 Apache 的 MaxClients 参数

在 Apache 配置文件（`httpd.conf`）中，MaxClients 参数的默认值最大可设置为 256。对于繁忙的站点，为了获得更好的性能，建议增加此参数的限制。你可以通过编辑 Apache 源码目录中的`src/include/httpd.h`文件并更改默认值来实现。

进入 Apache 源码目录（`cd ../apache_1.3.12/`），编辑`httpd.h`文件（`vi +333 src/include/httpd.h`），将以下行：

```c
#define HARD_SERVER_LIMIT 256
```

改为：

```c
#define HARD_SERVER_LIMIT 1024
```

**注意：**如果你在没有 mod_ssl 支持的情况下配置 Apache，那么要编辑以更改默认值的行将是 316 而不是 333。

### 步骤 4：为 PHP4 的配置步骤预配置 Apache

如果你想在 Apache Web 服务器中使用并包含 PHP4 服务器端脚本语言支持，则进入 Apache 源码目录（`cd apache_1.3.12/`）（如果你尚未在其中），并在终端中输入以下命令：

```bash
CC="egcs" \
OPTIM="-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
CFLAGS="-DDYNAMIC_MODULE_LIMIT=0" \
./configure \
--prefix=/home/httpd \
--bindir=/usr/bin \
--sbindir=/usr/sbin \
--libexecdir=/usr/lib/apache \
--includedir=/usr/include/apache \
--sysconfdir=/etc/httpd/conf \
--localstatedir=/var \
--runtimedir=/var/run \
--logfiledir=/var/log/httpd \
--datadir=/home/httpd \
--proxycachedir=/var/cache/httpd \
--mandir=/usr/man
```

**注意：**只有在你想将 PHP4 支持包含到 Apache 源码中时，此步骤才是必需的，因为它将为下面的 PHP4 配置步骤预配置 Apache。请注意，`-DDYNAMIC_MODULE_LIMIT=0`选项将禁用我们编译 Apache 时动态加载模块的使用，并将提高其性能。

## 配置 PHP4 并将其应用到 Apache 源码树

现在，进入 php4 目录（`cd ../php-4.0`），并在终端中输入以下命令：

1. 编辑`php_pgsql.h`文件（`vi +46 ext/pgsql/php_pgsql.h`），将以下行：

   ```c
   #include <libpq-fe.h>
   #include <libpq/libpq-fs.h>
   ```

   改为：

   ```c
   #include </usr/include/pgsql/libpq-fe.h>
   #include </usr/include/pgsql/libpq/libpq-fs.h>
   ```

   在`php_pgsql.h`文件中的这些修改是必要的，用于在 PHP4 配置期间指示 PostgreSQL 数据库的`libpq-fe.h`和`libpq-fs.h`头文件的位置。在 Red Hat Linux 中，PostgreSQL 的库位于`/usr/include/pgsql`。

2. 现在，我们必须在 Linux 服务器上配置和安装 PHP4：

   ```bash
   CC="egcs" \
   CFLAGS="-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions -I/usr/include/openssl" \
   ./configure \
   --prefix=/usr \
   --with-exec-dir=/usr/bin \
   --with-apache=../apache_1.3.12 \
   --with-config-file-path=/etc/httpd \
   --disable-debug \
   --enable-safe-mode \
   --with-imap \ (if you want IMAP & POP support).
   --with-ldap \ (if you want LDAP database light directory support).
   --with-pgsql \ (if you want PostgreSQL database support).
   --with-mm \
   --enable-inline-optimization \
   --with-gnu-ld \
   --enable-memory-limit
   ```

这告诉 PHP4 针对此特定硬件配置进行如下设置：

- 不带调试符号编译。
- 默认启用安全模式。
- 包含 IMAP 和 POP 支持。
- 包含 LDAP 目录支持。
- 包含 PostgreSQL 数据库支持。
- 包含 mm 支持以提高内存库的性能。
- 启用内联优化以获得更好的性能。
- 编译内存限制支持。
- 假定 C 编译器使用 GNU ld。

```bash
[root@deep php-4.0]# make
[root@deep php-4.0]# make install
```

### 步骤 5：将 mod_perl 应用到 Apache 源码树并构建/安装 Perl 端的 mod_perl

如果你想在 Apache Web 服务器中使用并包含 Perl 编程语言支持，则进入 mod_perl 源码目录（`cd ../mod_perl-1.24/`），并在终端中输入以下命令：

```bash
perl Makefile.PL \
EVERYTHING=1 \
APACHE_SRC=../apache_1.3.12/src \
USE_APACI=1 \
PREP_HTTPD=1 \
DO_HTTPD=1
```

```bash
[root@deep mod_perl-1.24]# make
[root@deep mod_perl-1.24]# make install
```

### 步骤 6：构建/安装 Apache，可选带/不带 mod_ssl、PHP4 和/或 mod_perl

一旦在 Apache 源码中包含了你要支持和使用的第三方模块，就该将其编译并安装到你的 Linux 系统中了。最后一步是进入 Apache 源码目录（`cd ../apache_1.3.12/`），并根据你要与 Apache 一起安装的内容，在终端中输入以下命令：

```bash
SSL_BASE=SYSTEM \ (require only if you have included support for mod_ssl to your Apache source).
EAPI_MM=SYSTEM \ (require only if you use the mm Shared Memory Library for Apache).
CC="egcs" \
OPTIM="-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
CFLAGS="-DDYNAMIC_MODULE_LIMIT=0" \
./configure \
--prefix=/home/httpd \
--bindir=/usr/bin \
--sbindir=/usr/sbin \
--libexecdir=/usr/lib/apache \
--includedir=/usr/include/apache \
--sysconfdir=/etc/httpd/conf \
--localstatedir=/var \
--runtimedir=/var/run \
--logfiledir=/var/log/httpd \
--datadir=/home/httpd \
--proxycachedir=/var/cache/httpd \
--mandir=/usr/man \
--add-module=src/modules/experimental/mod_mmap_static.c \
--add-module=src/modules/standard/mod_auth_db.c \
--enable-module=ssl \
--enable-rule=SSL_SDBM \
--disable-rule=SSL_COMPAT \
--activate-module=src/modules/php4/libphp4.a \
--enable-module=php4 \
--activate-module=src/modules/perl/libperl.a \
--enable-module=perl \
--disable-module=status \
--disable-module=userdir \
--disable-module=negotiation \
--disable-module=autoindex \
--disable-module=asis \
--disable-module=imap \
--disable-module=env \
--disable-module=actions
```




## 这告诉 Apache 针对此特定硬件配置进行如下设置

- `module mod_mmap` 以提高性能。
- `module mod_auth_db` 用于用户密码认证安全。
- `module mod_ssl` 用于数据加密和安全通信。
- `module mod_php4` 用于 PHP 服务器端脚本语言，并提升以 PHP 构建的网页加载速度。
- `module mod_perl` 用于比默认 CGI 脚本更好的安全性和性能。
- `disable module status`
- `disable module userdir`
- `disable module negotiation`
- `disable module autoindex`
- `disable module asis`
- `disable module imap`
- `disable module env`
- `disable module actions`

**注意：**需要注意的是，在配置期间移除所有不必要的模块将提高 Apache Web 服务器的性能。在我们上面的配置中，我们已经移除了最少使用的模块，以降低负载操作，并限制我们在 Apache Web 服务器中的安全风险。有关每个模块的详细信息，请参阅 Apache 文档。

## 第 7 步

现在，我们必须在 Linux 服务器上安装 Apache：

```bash
[root@deep apache_1.3.12]# make
[root@deep apache_1.3.12]# make install
[root@deep apache_1.3.12]# rm -f /usr/sbin/apachectl
[root@deep apache_1.3.12]# rm -f /usr/man/man8/apachectl.8
[root@deep apache_1.3.12]# rm -rf /home/httpd/icons/
[root@deep apache_1.3.12]# rm -rf /home/httpd/htdocs/
[root@deep apache_1.3.12]# cd /var/tmp/php-4.0
[root@deep php-4.0.0]# install -m 644 php.ini.dist /usr/lib/php.ini
[root@deep php-4.0.0]# rm -rf /etc/httpd/conf/ssl.crl/
[root@deep php-4.0.0]# rm -rf /etc/httpd/conf/ssl.crt/
[root@deep php-4.0.0]# rm -rf /etc/httpd/conf/ssl.csr/
[root@deep php-4.0.0]# rm -rf /etc/httpd/conf/ssl.key/
[root@deep php-4.0.0]# rm -rf /etc/httpd/conf/ssl.prm/
[root@deep php-4.0.0]# rm -f /etc/httpd/conf/srm.conf srm.conf.default access.conf access.conf.default
```

用它来启动和停止 Apache 守护进程的`apachectl`小脚本已删除，因为我们使用一个更好的名为`httpd`的脚本，位于`/etc/rc.d/init.d/`目录下，该脚本利用了 Linux System V。我们还删除了 Apache 使用自动索引功能时使用的`/home/httpd/icons`目录。此功能可能带来安全风险，因此我们已在配置文件中禁用了它。因此，我们可以安全地删除该目录，以在 Linux 服务器上腾出空间。`/home/httpd/htdocs`目录包含与 Apache 相关的所有文档文件，所以我们在阅读完文档后可以将其删除以腾出空间。`install -m`命令会将`php.ini.dist`文件安装到`/usr/lib/`目录下，并将其重命名为`php.ini`；该文件控制 PHP 行为的许多方面。`/etc/httpd/conf`下的`ssl.crl`、`ssl.crt`、`ssl.csr`、`ssl.key`和`ssl.prm`目录都是与 SSL 相关的目录，处理私钥和公钥。由于我们使用另一个位置`/etc/ssl/`，我们可以安全地删除它们。

**`make`**命令会将所有源文件编译为可执行二进制文件，而**`make install`**会将二进制文件及任何支持文件安装到适当的位置。**`rm -f`**命令将删除负责启动和停止 Apache 守护进程的`apachectl`小脚本，因为我们使用一个更好的名为`httpd`的脚本，位于`/etc/rc.d/init.d/`目录下，该脚本利用了 Linux System V。我们还删除了 Apache 使用自动索引功能时使用的`/home/httpd/icons`目录。此功能可能带来安全风险，因此我们已在配置文件中禁用了它。因此，我们可以安全地删除该目录以在 Linux 服务器上腾出空间。`/home/httpd/htdocs`目录包含与 Apache 相关的所有文档文件，所以在阅读完文档后我们可以将其删除以腾出空间。**`install -m`**命令会将`php.ini.dist`文件安装到`/etc/httpd/`目录下，并将其重命名为`php.ini`；该文件控制 PHP 行为的许多方面。`/etc/httpd/conf`下的`ssl.crl`、`ssl.crt`、`ssl.csr`、`ssl.key`和`ssl.prm`目录都是与 SSL 相关的目录，处理私钥和公钥。由于我们使用另一个位置`/etc/ssl/`，我们可以安全地删除它们。最后，我们删除未使用的`srm.conf`、`srm.conf.default`、`access.conf`和`access.conf.default`文件，其功能现在由`httpd.conf` Apache 文件处理。

## 工作后的清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf apache-version/ apache-version.tar.gz mod_ssl-version-version/ mod_ssl-version-version.tar.gz php-version/ php-version.tar.gz mod_perl-version/ mod_perl-version.tar.gz
```

**`rm`**命令将删除我们用于编译和安装 Apache、`mod_ssl`、`mod_perl`和 php 的所有源文件。它还将从`/var/tmp`目录中删除 Apache、`mod_ssl`、`mod_perl`和 php 的压缩归档文件。

## 配置

不同服务的配置文件根据您的需求和网络架构而非常具体。有人可能安装 Apache 服务器仅用于显示网页；另一个人可能安装带有数据库连接和电子商务及 SSL 支持等功能。在本书中，我们为您提供一个`httpd.conf`文件，包含 PHP、Perl、SSL、LDAP 和密码认证设置，以向您展示不同的可能性。

我们将重点放在这些文件的优化和安全性上，并将所有具体调整留给您自行决定。您需要阅读这些程序附带的文档，并希望您能理解它们。

本书中描述的所有软件在名为`floppy.tgz`的 tar 压缩归档中都有特定的目录和子目录，其中包含特定程序的文件配置。如果您获取此归档文件，您将不必手动复制下面的不同配置文件，或剪贴并粘贴它们来创建您的配置文件。无论您决定手动复制它们，还是从归档中获取为您方便制作的文件，您都有责任修改、调整为您的需求，并将与 Apache 软件相关的文件放置在服务器上的适当位置，如下所示。要下载的服务器配置文件归档位于以下互联网地址：`http://www.openna.com/books/floppy.tgz`

- 要运行 Apache 服务器，需要以下文件，并且必须创建或复制到服务器上的适当目录。
- 将`httpd.conf`文件复制到`/etc/httpd/conf/`目录。
- 将`apache`文件复制到`/etc/logrotate.d/`目录。
- 将`httpd`脚本文件复制到`/etc/rc.d/init.d/`目录。

您可以在我们的`floppy.tgz`归档中获取下面列出的配置文件。从解压后的`floppy.tgz`归档中将以下文件复制到适当位置，或直接从本书剪切并粘贴到相关文件。

## `/etc/httpd/conf/httpd.conf`文件的配置

`httpd.conf`文件是 Apache Web 服务器的主配置文件。存在大量选项，阅读 Apache 附带的文档以获取更多关于不同设置和参数的信息非常重要。以下配置示例是 Apache 的最小工作配置文件，带有 SSL 支持。另外，重要的是要注意，我们只注释与安全和优化相关的参数，其他参数留给您自行研究。

编辑`httpd.conf`文件（`vi /etc/httpd/conf/httpd.conf`）并添加/修改：

```apache
### 第 1 节：全局环境

#
ServerType standalone
ServerRoot "/etc/httpd"
PidFile /var/run/httpd.pid
ResourceConfig /dev/null
AccessConfig /dev/null
Timeout 300
KeepAlive On
MaxKeepAliveRequests 0
KeepAliveTimeout 15
MinSpareServers 16
MaxSpareServers 64
StartServers 16
MaxClients 512
MaxRequestsPerChild 100000

### 第 2 节："主"服务器配置

#
Port 80

<IfDefine SSL>
Listen 80
Listen 443
</IfDefine>

User www
Group www
ServerAdmin admin@openna.com
ServerName www.openna.com
DocumentRoot "/home/httpd/ona"

<Directory />
  Options None
  AllowOverride None
  Order deny,allow
  Deny from all
</Directory>

<Directory "/home/httpd/ona">
  Options None
  AllowOverride None
  Order allow,deny
  Allow from all
</Directory>

<Files .pl>
  Options None
  AllowOverride None
  Order deny,allow
  Deny from all
</Files>

<IfModule mod_dir.c>
DirectoryIndex index.htm index.html index.php index.php3 default.html index.cgi
</IfModule>

#<IfModule mod_include.c>
#Include conf/mmap.conf
#</IfModule>

UseCanonicalName On

<IfModule mod_mime.c>
TypesConfig /etc/httpd/conf/mime.types
</IfModule>

DefaultType text/plain
HostnameLookups Off
ErrorLog /var/log/httpd/error_log
LogLevel warn
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
SetEnvIf Request_URI \.gif$ gif-image
CustomLog /var/log/httpd/access_log combined env=!gif-image
ServerSignature Off

<IfModule mod_alias.c>
ScriptAlias /cgi-bin/ "/home/httpd/cgi-bin/"

<Directory "/home/httpd/cgi-bin">
  AllowOverride None
  Options None
  Order allow,deny
  Allow from all
</Directory>
</IfModule>

<IfModule mod_mime.c>
AddEncoding x-compress Z
AddEncoding x-gzip gz tgz
AddType application/x-tar .tgz
</IfModule>

ErrorDocument 500 "The server made a boo boo.
ErrorDocument 404 http://192.168.1.1/error.htm
ErrorDocument 403 "Access Forbidden -- Go away.

<IfModule mod_setenvif.c>
BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "MSIE 4\.0b2;" nokeepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer 4\.0" force-response-1.0
BrowserMatch "Java/1\.0" force-response-1.0
BrowserMatch "JDK/1\.0" force-response-1.0
</IfModule>

### 第 3 节：虚拟主机

#

<IfDefine SSL>
AddType application/x-x509-ca-cert .crt
AddType application/x-pkcs7-crl .crl
</IfDefine>

<IfModule mod_ssl.c>
SSLPassPhraseDialog builtin
SSLSessionCache dbm:/var/run/ssl_scache
SSLSessionCacheTimeout 300
SSLMutex file:/var/run/ssl_mutex
SSLRandomSeed startup builtin
SSLRandomSeed connect builtin
SSLLog /var/log/httpd/ssl_engine_log
SSLLogLevel warn
</IfModule>

<IfDefine SSL>
<VirtualHost _default_:443>
DocumentRoot "/home/httpd/ona"
ServerName www.openna.com
ServerAdmin admin@openna.com
ErrorLog /var/log/httpd/error_log

SSLEngine on
SSLCipherSuite ALL:!ADH:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL

SSLCertificateFile /etc/ssl/certs/server.crt
SSLCertificateKeyFile /etc/ssl/private/server.key
SSLCACertificatePath /etc/ssl/certs
SSLCACertificateFile /etc/ssl/certs/ca.crt
SSLCARevocationPath /etc/ssl/crl
SSLVerifyClient none
SSLVerifyDepth 10

SSLOptions +ExportCertData +StrictRequire

SetEnvIf User-Agent ".*MSIE.*" nokeepalive ssl-unclean-shutdown
SetEnvIf Request_URI \.gif$ gif-image
CustomLog /var/log/httpd/ssl_request_log \
  "%t %h %{SSL_PROTOCOL}x %{SSL_CIPHER}x \"%r\" %b" env=!gif-image

</VirtualHost>
</IfDefine>
```



这告诉`httpd.conf`文件为以下特定配置进行设置：

## `ServerType standalone`

选项`ServerType`指定 Apache 在系统上应如何运行。你可以从超级服务器`inetd`运行它，或作为独立守护进程运行。为了获得更好的性能和速度，强烈建议以`standalone`类型运行 Apache。

## `ServerRoot "/etc/httpd"`

选项`ServerRoot`指定 Apache 服务器配置文件所在的目录。它允许 Apache 在启动时知道在哪里可以找到其配置文件。

## `PidFile /var/run/httpd.pid`

选项`PidFile`指定服务器在启动时记录守护进程进程 ID 的位置。只有当你以`standalone`模式配置 Apache 时才需要此选项。

## `ResourceConfig /dev/null`

选项`ResourceConfig`指定 Apache 读取完`httpd.conf`文件后读取的旧`srm.conf`文件的位置。当你将位置设置为`/dev/null`时，Apache 允许你将此文件的内容包含在`httpd.conf`文件中，这样一来，你就只有一个文件来处理所有配置参数，更加简洁。

## `AccessConfig /dev/null`

选项`AccessConfig`指定 Apache 读取完`srm.conf`文件后读取的旧`access.conf`文件的位置。当你将位置设置为`/dev/null`时，Apache 允许你将此文件的内容包含在`httpd.conf`文件中，这样一来，你就只有一个文件来处理所有配置参数，更加简洁。

## `Timeout 300`

选项`Timeout`指定 Apache 等待 GET、POST、PUT 请求和传输确认（ACK）的时间量。你可以安全地将人死亡将该选项保留为默认值。

## `KeepAlive On`

选项`KeepAlive`如果设置为`On`，则指定在此 Web 服务器上启用持久连接。为了获得更好的性能，建议将此选项设置为`On`，并允许每个连接处理多个请求。

## `MaxKeepAliveRequests 0`

选项`MaxKeepAliveRequests`指定当上述`KeepAlive`选项设置为`On`时，每个连接允许的请求数。当此选项的值设置为`0`时，服务器上允许无限数量的请求。为了服务器性能，建议允许无限请求。

## `KeepAliveTimeout 15`

选项`KeepAliveTimeout`指定 Apache 在关闭连接之前等待后续请求的秒数。`15`秒的值对于服务器性能来说是一个不错的平均值。

## `MinSpareServers 16`

选项`MinSpareServers`指定 Apache 的空闲子服务器进程的最小数量，这些进程不处理请求。这是关于 Apache Web 服务器性能的一个重要调优参数。对于高负载操作，互联网上各种基准测试推荐使用`16`。

## `MaxSpareServers 64`

选项`MaxSpareServers`指定 Apache 的空闲子服务器进程的最大数量，这些进程不处理请求。这也是关于 Apache Web 服务器性能的一个重要调优参数。对于高负载操作，互联网上各种基准测试推荐使用`64`。

## `StartServers 16`

选项`StartServers`指定 Apache 在启动时将创建的子服务器进程数量。这同样是一个关于 Apache Web 服务器性能的重要调优参数。对于高负载操作，互联网上各种基准测试推荐使用`16`。

## `MaxClients 512`

选项`MaxClients`指定 Apache 可以同时支持的请求数。这也是关于 Apache Web 服务器性能的一个重要调优参数。对于高负载操作，互联网上各种基准测试推荐使用`512`。

## `MaxRequestsPerChild 100000`

选项`MaxRequestsPerChild`指定单个弄服务器子进程将处理的请求数。这也是关于 Apache Web 服务器性能的一个重要调优参数。

## `User www`

选项`User`指定 Apache 服务器将以什么 UID 运行。创建一个对系统具有最小访问权限的新用户很重要，该用户仅用于运行 Web 服务器守护进程。

## `Group www`

选项`Group`指定 Apache 服务器将以什么 GID 运行。创建一个对系统具有最小访问权限的新组很重要，该组仅用于运行 Web 服务器守护进程。

## `DirectoryIndex index.htm index.html index.php index.php3 default.html index.cgi`

选项`DirectoryIndex`指定 Apache 用作预写 HTML 目录索引的文件。换句话说，如果 Apache 找不到要显示的默认索引页面，它将尝试此参数中的下一个条目（如果有的话）。为了提高 Web 服务器的性能，建议将你最常用的默认索引页面列在前面。

## `Include conf/mmap.conf`

选项`Include`指定你可以从服务器配置文件（`httpd.conf`）中包含的其他文件的位置。在我们的例子中，我们包含位于`/etc/httpd/conf`目录下的`mmap.conf`文件。此文件（`mmap.conf`）将文件映射到内存中以实现更快的提供服务。有关更多信息，请参阅“优化 Apache”部分。

## `HostnameLookups Off`

选项`HostnameLookups`如果设置为`Off`，则指定禁用 DNS 查找。建议将此选项设置为`Off`以节省网络流量时间，并提高 Apache Web 服务器的性能。

## `"/etc/logrotate.d/apache"`文件的配置

配置你的`/etc/logrotate.d/apache`文件，以每周自动轮转你的 Apache 日志文件。

创建`apache`文件（`touch /etc/logrotate.d/apache`）并添加：

```text
/var/log/httpd/access_log {
  missingok
  postrotate
    /usr/bin/killall -HUP httpd
  endscript
}

/var/log/httpd/error_log {
  missingok
  postrotate
    /usr/bin/killall -HUP httpd
  endscript
}

/var/log/httpd/ssl_request_log {
  missingok
  postrotate
    /usr/bin/killall -HUP httpd
  endscript
}

/var/log/httpd/ssl_engine_log {
  missingok
  postrotate
    /usr/bin/killall -HUP httpd
  endscript
}
```

**注意**：此文件中包含自动轮转名为`ssl_request_log`和`ssl_engine_log`的 SSL 日志文件的行。如果你打算在不支持 SSL 的情况下运行 Apache，则必须删除与 SSL 相关的行。

## `"/etc/rc.d/init.d/httpd"`脚本文件的配置

配置你的`/etc/rc.d/init.d/httpd`脚本文件，以启动和停止 Apache Web 服务器。

创建`httpd`脚本文件（`touch /etc/rc.d/init.d/httpd`）并添加：

```sh
#!/bin/sh

#

# Startup script for the Apache Web Server

#

# chkconfig: 345 85 15

# description: Apache is a World Wide Web server. It is used to serve \
#	     HTML files and CGI.

# processname: httpd

# pidfile: /var/run/httpd.pid

# config: /etc/httpd/conf/httpd.conf

# Source function library.

. /etc/rc.d/init.d/functions
```

```sh
# See how we were called.

case "$1" in

  start)

    echo -n "Starting httpd: "

    daemon httpd -DSSL

    echo

    touch /var/lock/subsys/httpd

    ;;

  stop)

    echo -n "Shutting down http: "

    killproc httpd

    echo

    rm -f /var/lock/subsys/httpd

    rm -f /var/run/httpd.pid

    ;;

  status)

    status httpd

    ;;

  restart)

    $0 stop

    $0 start

    ;;

  reload)

    echo -n "Reloading httpd: "

    killproc httpd -HUP

    echo

    ;;

  *)

    echo "Usage: $0 {start|stop|restart|reload|status}"

    exit 1

esac

exit 0
```

现在，使此脚本可执行并更改其默认权限：

```sh
[root@deep /]# chmod 700 /etc/rc.d/init.d/httpd
```

使用以下命令为 Apache 创建符号链接 rc.d：

```sh
[root@deep /]# chkconfig --add httpd
```

使用以下命令手动启动你的新 Apache 服务器：

```text
[root@deep /]# /etc/rc.d/init.d/httpd start

Starting httpd:                      [ OK ]
```

**注意**：`-DSSL`选项将以 SSL 模式的狗身份启动 Apache。如果你想以普通模式启动 Apache，请在读取`daemon httpd`的行附近删除`-DSSL`选项。

## PHP4 服务器端脚本语言

如果你打算在 Apache Web 服务器上使用 PHP4 服务器端脚本语言支持，请不要忘记在你的`/etc/httpd/conf/httpd.conf`文件中包含以下行以启用此功能：

### 步骤 1

编辑`httpd.conf`文件（`vi /etc/httpd/conf/httpd.conf`），并在`<IfModule mod_mime.c>`和`</IfModule>`段标签之间添加以下行：

```apache
AddType application/x-httpd-php .php

AddType application/x-httpd-php .php3

AddType application/x-httpd-php-source .phps
```

### 第 2 步

你必须重新启动 Apache Web 服务器，才能使更改生效：

- 要重新启动 Apache，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/httpd restart

Shutting down http:              [ OK ]

Starting httpd:                  [ OK ]
```

### 第 3 步

一旦我们的`httpd.conf`文件中包含了上述行，我们就必须测试新的 PHP4 功能，以确保它正常工作。我们将在 DocumentRoot 中创建一个名为`php.php`的小型 PHP 文件，然后将 Web 浏览器指向这个 PHP 文档，看看 PHP4 是否在服务器上工作。

在你的 DocumentRoot 中创建`php.php`文件（`touch /home/httpd/ona/php.php`），并在 PHP 文件中添加以下行：

```php
<body bgcolor="#FFFFFF">

<?php phpinfo()?>

</body>
```

**注意：**这些行将指示 PHP4 程序显示有关我们 Linux 服务器配置的各种信息。

### 第 4 步

现在，将你的 Web 浏览器指向以下地址：`http://my-web-server/php.php`

`<my-web-server>`是你的 Apache Web 服务器所在的地址，`<php.php>`是我们在上面创建的用于显示我们 Linux 服务器信息和配置的 PHP 文档。

如果你在 Web 浏览器中看到类似上面的页面出现……恭喜你！你的 PHP 模块正在工作。

## Perl 模块 `Devel::Symdump`

如果你打算将`mod_perl`编程语言支持用于你的 Apache Web 服务器，那么安装一个名为`Devel::Symdump`的小型 perl 模块程序会很有用。这个第三方模块将允许你检查 perl 的符号表以及运行程序中的类层次结构。要构建和安装它，请按照以下步骤操作。

### 软件包

Devel-Symdump 主页：[http://www.perl.com/CPAN/modules/by-module/Devel/](http://www.perl.com/CPAN/modules/by-module/Devel/)

你必须确保下载：`Devel-Symdump-2.00.tar.gz`

Devel-Symdump 版本号为`2.00`

```sh
[root@deep /]# cp Devel-Symdump-version.tar.gz /var/tmp/

[root@deep /]# cd /var/tmp/

[root@deep tmp]# tar xzpf Devel-Symdump-version.tar.gz
```

### 第 1 步

进入新的 Devel-Symdump 目录，在你的终端上输入以下命令，以在 Linux 服务器上编译和安装该模块：

```sh
[root@deep Devel-Symdump-2.00]# perl Makefile.PL

[root@deep Devel-Symdump-2.00]# make

[root@deep Devel-Symdump-2.00]# make test

[root@deep Devel-Symdump-2.00]# make install
```

### 第 2 步

一旦该模块安装在你的系统上，你必须在`/etc/httpd/conf/httpd.conf`文件中包含以下行，以便能够查看服务器上不同 Perl 模块的状态：

编辑`httpd.conf`文件（`vi /etc/httpd/conf/httpd.conf`）并添加以下行：

```apache
<Location /perl-status>

    SetHandler perl-script

    PerlHandler Apache::Status

    Order deny,allow

    Deny from all

    Allow from 192.168.1.0/24

</Location>
```

### 第 3 步

你必须重新启动 Apache Web 服务器，才能使更改生效：

- 要重新启动 Apache，请使用以下命令：

```text
[root@deep /]# /etc/rc.d/init.d/httpd restart

Shutting down http:              [ OK ]

Starting httpd:                  [ OK ]
```

### 第 4 步

最后，我们必须测试新的 Devel-Symdump 模块，以确保我们能够查看服务器上不同 Perl 模块的状态。

要验证它是否工作，请将你的 Web 浏览器指向以下地址：[http://my-web-server/perl-status/](http://my-web-server/perl-status/)。`<my-web-server>`是你的 Apache Web 服务器所在的地址。

## 工作后的清理

```sh
[root@deep /]# cd /var/tmp

[root@deep tmp]# rm -rf Devel-Symdump.version/ Devel-Symdump-version.tar.gz
```

## 已安装的文件

```text
> /usr/lib/perl5/man/man3/Devel::Symdump.3

> /usr/lib/perl5/site_perl/5.005/i386-linux/auto/Devel

> /usr/lib/perl5/site_perl/5.005/i386-linux/auto/Devel/Symdump

> /usr/lib/perl5/site_perl/5.005/i386-linux/auto/Devel/Symdump/.packlist

> /usr/lib/perl5/site_perl/5.005/Devel

> /usr/lib/perl5/site_perl/5.005/Devel/Symdump

> /usr/lib/perl5/site_perl/5.005/Devel/Symdump/Export.pm

> /usr/lib/perl5/site_perl/5.005/Devel/Symdump.pm
```



## CGI.pm Perl 库

`CGI.pm` 是一个用于编写万维网 CGI 脚本的 Perl5 库。该软件的旧版本默认存在于你的系统上，但它们存在缺陷。建议你至少将其更新到 2.56 版本。要更新此模块，请按照以下步骤操作。

### 软件包

CGI.pm 主页：[http://stein.cshl.org/WWW/software/CGI/cgi_docs.html](http://stein.cshl.org/WWW/software/CGI/cgi_docs.html)

你必须确保下载：`CGI_pm.tar.gz`

CGI.pm 版本号为 2.56。

```bash
[root@deep /]# cp CGI_pm.tar.gz /var/tmp/
[root@deep /]# cd /var/tmp/
[root@deep tmp]# tar xzpf CGI_pm.tar.gz
```

### 第 1 步

首先，我们将检查系统中安装的 `CGI.pm` 版本。

- 你可以使用以下命令检查当前的 `CGI.pm` 版本号：

```bash
[root@deep]# perl -e 'use CGI; print $CGI::VERSION."\n";'
2.46
```

### 第 2 步

进入新的 CGI.pm 目录，在你的终端上输入以下命令，以在 Linux 服务器上编译和安装更新后的库：

```bash
[root@deep CGI.pm-2.56]# perl Makefile.PL
[root@deep CGI.pm-2.56]# make
[root@deep CGI.pm-2.56]# make test
[root@deep CGI.pm-2.56]# make install
```

### 工作后的清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf CGI.pm-version/ CGI_pm.tar.gz
```

### 已安装的文件

```text
/usr/lib/perl5/5.00503/CGI/Pretty.pm
/usr/lib/perl5/5.00503/i386-linux/auto/CGI
/usr/lib/perl5/5.00503/i386-linux/auto/CGI/.packlist
/usr/lib/perl5/man/man3/CGI::Pretty.3
```

## 保护 Apache

### 更改 Web 服务器上文件和目录的一些重要权限

当你在你的服务器上安装 Apache 时，有些文件和目录默认设置了过多的权限。二进制程序 `httpd` 可以设置为仅由超级用户 `root` 可读，并由所有者、组和其他人可执行，以获得更好的安全性。`/etc/httpd/conf` 和 `/var/log/httpd` 目录不需要被其他人可读、可写或可执行。

```bash
[root@deep /]# chmod 511 /usr/sbin/httpd
[root@deep /]# chmod 750 /etc/httpd/conf/
[root@deep /]# chmod 750 /var/log/httpd/
```

### 自动索引

如果你已在 Apache 配置文件中启用了目录的自动索引（`httpd.conf` 中的 `IndexOptions`），那么你将面临一个安全问题，因为对目录的任何请求如果找不到索引文件，就会构建该目录内容的索引。在许多情况下，你可能只希望人们看到你专门链接的文件。要关闭此功能，你需要从 `DocumentRoot` 目录中移除读取权限（但不包括其中的文件）。

```bash
[root@deep /]# cd /home/httpd/
[root@deep httpd]# chmod 311 ona
[root@deep httpd]# ls -la
```

```text
d-wx--x--x  13 webadmin webadmin    1024 Jul 28 08:12 ona
```

现在，经过此修改后，对此受保护目录的任何请求应返回类似如下的错误消息：

```text
Forbidden

You don't have permission to access "/ona/" on this server.
```

**注意：**`ona` 在我们的例子中是 `DocumentRoot`（你将从中提供文档的目录）。

### 创建用于用户认证的 `.dbmpasswd` 密码文件

此步骤仅在认为你将对你的网站使用访问文件认证系统时才需要。访问文件认证用于当你需要保护网站某些部分时使用用户密码的情况。使用 Apache 有很多选项可以用用户名和密码保护你的网站。

#### 第 1 步

Apache 的 `dbmmanage` 程序实用工具可用于创建和更新 HTTP 用户的用户名和密码。此方法使用 DBM 格式文件，这是当你有数千用户需要管理密码文件时最快的机制。首先，重要的是将该程序的权限更改为 `0750/-rwxr-x---`，仅由超级用户 `root` 可写，由组可读和可执行，其他人没有任何权限。

- 要更改 `dbmmanage` 程序的权限，请使用以下命令：

```bash
[root@deep /]# chmod 750 /usr/bin/dbmmanage
```

- 要创建用户名和密码，请使用以下命令：

```bash
[root@deep /]# /usr/bin/dbmmanage /etc/httpd/.dbmpasswd adduser username
New password:
```

重新输入新密码：

用户 `username` 已添加，密码已加密为 `l4jrdAL9MH0K`。

其中 `/etc/httpd` 是密码文件的位置，`.dbmpasswd` 是密码文件的名称，`username` 是你要在 `.dbmpasswd` 文件中添加的用户名。

### 第 2 步

如果你使用 Apache Web 服务器的 `dbmmanage` 工具来创建密码和用户名，别忘了在 `/etc/httpd/conf/httpd.conf` 配置文件中包含你需要使用用户密码认证保护的网站部分。

编辑 `httpd.conf` 文件（`vi /etc/httpd/conf/httpd.conf`），并添加以下行以使用用户密码认证来保护你的网站 `ona` 的 `private` 目录：

```apache
<Directory "/home/httpd/ona/private">
  Options None
  AllowOverride AuthConfig
  AuthName "restricted stuff"
  AuthType Basic
  AuthDBUserFile /etc/httpd/.dbmpasswd
  require valid-user
</Directory>
```

路径 `/home/httpd/ona/private` 指定了我们要用密码和用户名保护的目录，`/etc/httpd/.dbmpasswd` 指定了密码文件的位置。

**注意：**要为 Apache Web 服务器添加 DB 密码认证模块，你必须确保在 Apache 配置时包含它，使用以下参数 `--add-module=src/modules/standard/mod_auth_db.c`。更多信息请参阅 Apache 文档。

### 第 3 步

你必须重启 Apache Web 服务器以使更改生效：

- 要重启 Apache，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/httpd restart
Shutting down http:              [ OK ]
Starting httpd:                  [ OK ]
```

### 第 4 步

最后，我们必须测试名为 `private` 的新受保护目录。

要验证其是否工作，请将你的 Web 浏览器指向以下地址：[http://my-web-server/private/](http://my-web-server/private/)。`my-web-server` 是你的 Apache Web 服务器所在的地址。`/private/` 是我们想要使用用户密码认证保护的目录。

## 为 `httpd.conf` 等重要配置文件设置不可更改属性

正如我们已知，不可更改位（immutable bit）可用于防止删除、覆盖或创建指向文件的符号链接。一旦你的 `httpd.conf` 文件配置完成，最好使用以下命令为其设置不可更改属性：

```bash
[root@deep /]# chattr +i /etc/httpd/conf/httpd.conf
```

## 在 chroot 监狱中运行 Apache

本部分重点介绍如何防止 Apache 被用作入侵其所在系统的入口点。默认情况下，Apache **以非 root 用户身份**运行，这将把任何损害限制为普通用户通过本地 shell 可以执行的操作。当然，允许相当于匿名访客账户的权限远不能满足大多数 Apache 服务器的安全要求，因此可以采取额外的步骤——即**在 chroot 监狱中运行 Apache**。

chroot 监狱的主要好处是，监狱将守护进程能看到的文件系统部分限制为监狱的根目录。此外，由于监狱只需要支持 Apache，监狱中可用的程序可以非常有限。最重要的是，不需要 setuid-root 程序，这些程序可能被用来获取 root 权限并越狱。

对 Apache 进行 chroot 并非易事，而且容易导致问题。在开始之前，我们需要先确定这是否对你有利。以下是一些优缺点，但肯定不限于这些：

### 优点

- 如果 Apache 被入侵，攻击者将无法访问整个文件系统。
- 可能允许他人访问服务器的编写拙劣的 CGI 脚本将无法工作。

### 缺点

- 你需要在 chroot 监狱中额外放置一些库，Apache 才能工作。
- 如果你在 Apache 中使用任何 Perl/CGI 功能，你需要将所需的二进制文件、Perl 库和文件复制到 chroot 空间中的适当位置。SSL、PHP、LDAP、PostgreSQL 和其他第三方程序也是如此。

下面列出的 chroot 配置假设你使用外部程序 `mod_ssl` 编译了 Apache 服务器。你编译 Apache Web 服务器时所使用的不同模块的差异在于你需要将哪些库和二进制文件复制到 chroot 目录中。

请记住，如果你将 Apache 编译为使用 `mod_perl`，你必须将所有相关的二进制文件和 Perl 库复制到 chroot 目录中。Perl 位于 `/usr/lib/perl5`，如果你使用 Perl 功能，请将 Perl 目录复制到 `/chroot/httpd/usr/lib/perl5/`。不要忘记在复制之前在你的 chroot 结构中创建目录 `/chroot/httpd/usr/lib/perl5`。

以下是在 chroot 监狱中运行 Apache Web 服务器的必要步骤：

### 第 1 步

我们必须找到 `httpd` 的共享库依赖项。这些稍后需要复制到 chroot 监狱中。

- 要查找 `httpd` 的共享库依赖项，请执行以下命令：

```bash
[root@deep /]# ldd /usr/sbin/httpd
```

```text
libpam.so.0 => /lib/libpam.so.0 (0x40016000)
libm.so.6 => /lib/libm.so.6 (0x4001f000)
libdl.so.2 => /lib/libdl.so.2 (0x4003b000)
libcrypt.so.1 => /lib/libcrypt.so.1 (0x4003e000)
libnsl.so.1 => /lib/libnsl.so.1 (0x4006b000)
libresolv.so.2 => /lib/libresolv.so.2 (0x40081000)
libdb.so.3 => /lib/libdb.so.3 (0x40090000)
libc.so.6 => /lib/libc.so.6 (0x400cb000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

记下上面列出的文件；在我们的步骤中稍后你会需要这些。

### 第 2 步

如果还没有为运行 Apache `httpd` 添加新的 UID 和新的 GID，请添加。这很重要，因为以 root 身份运行会违背监狱的目的，而使用系统中已存在的不同 UID（即 `nobody`）可能会允许你的服务访问彼此的资源。考虑以下场景：Web 服务器以 `nobody` 或任何其他过度使用的 UID/GID 运行并被入侵。攻击者现在可以从 chroot 内部访问任何其他以 `nobody` 运行的进程。

这些是示例 UID/GID。请检查 `/etc/passwd` 和 `/etc/group` 文件以获取空闲的 UID/GID 编号。在我们的配置中，我们将使用数值 `80` 和 UID/GID `www`。

```bash
[root@deep /]# useradd -c "Apache Server" -u 80 -s /bin/false -r -d /home/httpd www 2>/dev/null || :
```

上述命令将创建数值 GID 值为 80 的组 `www`，以及数值 UID 值为 80 的用户 `www`。

### 第 3 步

设置 chroot 环境。首先，我们需要创建 chroot 化的 Apache 结构。我们使用 `/chroot/httpd` 作为 chroot 化的 Apache。`/chroot/httpd` 只是位于不同分区上的一个目录，我们决定将 Apache 放在那里以提高安全性。

```bash
[root@deep /]# /etc/rc.d/init.d/httpd stop <- 仅当 Apache 已安装并在你的系统上运行时。
Shutting down httpd:           [ OK ]
[root@deep /]# mkdir /chroot/httpd
```

接下来，按如下方式创建其余目录：

```bash
[root@deep /]# mkdir /chroot/httpd/dev
[root@deep /]# mkdir /chroot/httpd/lib
[root@deep /]# mkdir /chroot/httpd/etc
[root@deep /]# mkdir -p /chroot/httpd/usr/sbin
[root@deep /]# mkdir -p /chroot/httpd/var/run
[root@deep /]# mkdir -p /chroot/httpd/var/log/httpd
[root@deep /]# chmod 750 /chroot/httpd/var/log/httpd/
[root@deep /]# mkdir -p /chroot/httpd/home/httpd
```

你需要将主配置目录、配置文件、`cgi-bin` 目录、根目录和 `httpd` 程序复制到 chroot 监狱：

```bash
[root@deep /]# cp -r /etc/httpd /chroot/httpd/etc/
[root@deep /]# cp -r /home/httpd/cgi-bin /chroot/httpd/home/httpd/
[root@deep /]# cp -r /home/httpd/your-DocumentRoot /chroot/httpd/home/httpd/
[root@deep /]# mknod /chroot/httpd/dev/null c 1 3
[root@deep /]# chmod 666 /chroot/httpd/dev/null
[root@deep /]# cp /usr/sbin/httpd /chroot/httpd/usr/sbin/
```

我们需要创建 `/chroot/httpd/etc`、`/chroot/httpd/dev`、`/chroot/httpd/lib`、`/chroot/httpd/usr/sbin`、`/chroot/httpd/var/run`、`/chroot/httpd/home/httpd` 和 `/chroot/httpd/var/log/httpd` 目录，因为从 chroot 的角度来看，我们位于 `/` 根目录。

### 第 4 步

如果你编译的 Apache Web 服务器支持 SSL，则必须将整个 `/etc/ssl` 目录（包含所有私钥和公钥）复制到 chroot 环境中。

```bash
[root@deep /]# cp -r /etc/ssl /chroot/httpd/etc/
[root@deep /]# chmod 600 /chroot/httpd/etc/ssl/certs/ca.crt
[root@deep /]# chmod 600 /chroot/httpd/etc/ssl/certs/server.crt
[root@deep /]# chmod 600 /chroot/httpd/etc/ssl/private/ca.key
[root@deep /]# chmod 600 /chroot/httpd/etc/ssl/private/server.key
```

- 仅在使用 `mod_ssl` 功能时需要。
- 仅在使用 `mod_ssl` 功能时需要。
- 仅在使用 `mod_ssl` 功能时需要。
- 仅在使用 `mod_ssl` 功能时需要。
- 仅在使用 `mod_ssl` 功能时需要。

### 第 5 步

由于我们编译的 Apache 使用了共享库，因此需要将它们安装到 chroot 目录结构中。使用 `ldd /chroot/httpd/usr/sbin/httpd` 来查找需要的库。输出结果（取决于你编译 Apache 时使用的选项）类似于：

```text
libpam.so.0 => /lib/libpam.so.0 (0x40016000)
```



```text
libm.so.6 => /lib/libm.so.6 (0x4001f000)
libdl.so.2 => /lib/libdl.so.2 (0x4003b000)
libcrypt.so.1 => /lib/libcrypt.so.1 (0x4003e000)
libnsl.so.1 => /lib/libnsl.so.1 (0x4006b000)
 libresolv.so.2 => /lib/libresolv.so.2 (0x40081000)
libdb.so.3 => /lib/libdb.so.3 (0x40090000)
libc.so.6 => /lib/libc.so.6 (0x400cb000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

复制上面列出的共享库：

```bash
[root@deep /]# cp /lib/libpam.so.0 /chroot/httpd/lib/
[root@deep /]# cp /lib/libm.so.6 /chroot/httpd/lib/
[root@deep /]# cp /lib/libdl.so.2 /chroot/httpd/lib/
[root@deep /]# cp /lib/libcrypt.so.1 /chroot/httpd/lib/
[root@deep /]# cp /lib/libnsl* /chroot/httpd/lib/
[root@deep /]# cp /lib/libresolv* /chroot/httpd/lib/
[root@deep /]# cp /lib/libdb.so.3 /chroot/httpd/lib/
[root@deep /]# cp /lib/libc.so.6 /chroot/httpd/lib/
[root@deep /]# cp /lib/ld-linux.so.2 /chroot/httpd/lib/
```

你还需要以下额外的库来支持某些网络功能，例如域名解析：

```bash
[root@deep /]# cp /lib/libnss_compat* /chroot/httpd/lib/
[root@deep /]# cp /lib/libnss_dns* /chroot/httpd/lib/
[root@deep /]# cp /lib/libnss_files* /chroot/httpd/lib/
```

## 第 6 步

现在我们需要将 `passwd` 和 `group` 文件复制到 `/chroot/httpd/etc` chroot 目录中。这里的概念与 ftpd 使用 `passwd` 和 `group` 文件的方式相同。接下来，我们将在两个文件（`passwd` 和 `group`）中删除所有条目，只保留 Apache 运行时所使用的用户。

```bash
[root@deep /]# cp /etc/passwd /chroot/httpd/etc/
[root@deep /]# cp /etc/group /chroot/httpd/etc/
```

编辑 `passwd` 文件（`vi /chroot/httpd/etc/passwd`），删除所有条目，只保留 Apache 运行时所使用的用户（在我们的配置中，是 `"www"`）：

```text
www:x:80:80::/home/www:/bin/bash
```

编辑 `group` 文件（`vi /chroot/httpd/etc/group`），删除所有条目，只保留 Apache 运行时所使用的组（在我们的配置中，是 `"www"`）：

```text
www:x:80:
```

## 第 7 步

在 chroot 环境中，你还需要 `/etc/resolv.conf`、`/etc/nsswitch.conf` 和 `/etc/hosts` 文件。

```bash
[root@deep /]# cp /etc/resolv.conf /chroot/httpd/etc/
[root@deep /]# cp /etc/hosts /chroot/httpd/etc/
[root@deep /]# cp /etc/nsswitch.conf /chroot/httpd/etc/
```

## 第 8 步

现在，为了增强安全性，我们必须将 chroot 环境中的某些文件设置为不可变。

- 为 `passwd` 文件设置不可变位：

  ```bash
  [root@deep /]# cd /chroot/httpd/etc/
  [root@deep /]# chattr +i passwd
  ```

- 为 `group` 文件设置不可变位：

  ```bash
  [root@deep /]# cd /chroot/httpd/etc/
  [root@deep /]# chattr +i group
  ```

- 为 `httpd.conf` 文件设置不可变位：

  ```bash
  [root@deep /]# cd /chroot/httpd/etc/httpd/conf/
  [root@deep /]# chattr +i httpd.conf
  ```

- 为 `resolv.conf` 文件设置不可变位：

  ```bash
  [root@deep /]# cd /chroot/httpd/etc/
  [root@deep /]# chattr +i resolv.conf
  ```

- 为 `hosts` 文件设置不可变位：

  ```bash
  [root@deep /]# cd /chroot/httpd/etc/
  [root@deep /]# chattr +i hosts
  ```

- 为 `nsswitch.conf` 文件设置不可变位：

  ```bash
  [root@deep /]# cd /chroot/httpd/etc/
  [root@deep /]# chattr +i nsswitch.conf
  ```

## 第 9 步

将 `localtime` 文件复制到 chroot 环境中，以便日志条目能够正确调整为你的本地时区：

```bash
[root@deep /]# cp /etc/localtime /chroot/httpd/etc/
```

## 第 10 步

删除不必要的 Apache 文件和目录：

```bash
[root@deep /]# rm -rf /var/log/httpd/
[root@deep /]# rm -rf /etc/httpd/
[root@deep /]# rm -rf /home/httpd/
[root@deep /]# rm -f /usr/sbin/httpd
```

我们可以安全地删除上述所有文件和目录，因为它们现在已经位于我们的 chroot 环境目录下了。

## 第 11 步

告知 syslogd 新的 chroot 服务。

通常情况下，进程通过 `/dev/log` 与 syslogd 通信。由于 chroot 环境的存在，这将无法实现，因此需要告知 syslogd 监听 `/chroot/httpd/dev/log`。为此，编辑 syslog 启动脚本以指定额外的监听位置。

编辑 `syslog` 脚本（`vi /etc/rc.d/init.d/syslog`），将以下行：

```bash
daemon syslogd -m 0
```

改为：

```bash
daemon syslogd -m 0 -a /chroot/httpd/dev/log
```

## 第 12 步

Apache 的默认 httpd 脚本文件在 chroot 环境外部启动守护进程 `httpd`。我们必须修改它，使其现在从 chroot 环境中启动 httpd。编辑 `httpd` 脚本文件（`vi /etc/rc.d/init.d/httpd`），将以下行：

```bash
daemon httpd
```

改为：

```bash
/usr/sbin/chroot /chroot/httpd/ /usr/sbin/httpd -DSSL
```

并将：

```bash
rm -f /var/run/httpd.pid
```

改为：

```bash
rm -f /chroot/httpd/var/run/httpd.pid
```

## 第 13 步

最后，我们必须测试 Apache Web 服务器的新 chroot 环境配置。

- 首先要做的是使用以下命令重新启动 syslogd 守护进程：

  ```bash
  [root@deep /]# /etc/rc.d/init.d/syslog restart

  Shutting down kernel logger:         [ OK ]
  Shutting down system logger:         [ OK ]
  Starting system logger:              [ OK ]
  Starting kernel logger:              [ OK ]
  ```

- 现在，使用以下命令启动新的 chroot 环境 Apache：

  ```bash
  [root@deep /]# /etc/rc.d/init.d/httpd start

  Starting httpd:                      [ OK ]
  ```

- 如果没有出现任何错误，执行 `ps ax | grep httpd` 查看是否正在运行：

  ```bash
  [root@deep /]# ps ax | grep httpd

  14373 ?    S   0:00 httpd -DSSL
  14376 ?    S   0:00 httpd -DSSL
  14377 ?    S   0:00 httpd -DSSL
  14378 ?    S   0:00 httpd -DSSL
  14379 ?    S   0:00 httpd -DSSL
  14380 ?    S   0:00 httpd -DSSL
  14381 ?    S   0:00 httpd -DSSL
  14382 ?    S   0:00 httpd -DSSL
  14383 ?    S   0:00 httpd -DSSL
  14384 ?    S   0:00 httpd -DSSL
  14385 ?    S   0:00 httpd -DSSL
  14386 ?    S   0:00 httpd -DSSL
  14387 ?    S   0:00 httpd -DSSL
  14388 ?    S   0:00 httpd -DSSL
  14389 ?    S   0:00 httpd -DSSL
  14390 ?    S   0:00 httpd -DSSL
  14391 ?    S   0:00 httpd -DSSL
  14397 ?    S   0:00 httpd -DSSL
  14476 ?    S   0:00 httpd -DSSL
  14477 ?    S   0:00 httpd -DSSL
  14478 ?    S   0:00 httpd -DSSL
  ```

如果是这样，让我们检查它是否已 chroot，方法是选择一个进程号并执行 `ls -la /proc/that_process_number/root/`。

```bash
[root@deep /]# ls -la /proc/14373/root/
```

如果你看到：

```text
dev
etc
home
lib
usr
var
```

恭喜！

如上所述

## 新的 `/etc/logrotate.d/apache` 文件配置

现在 Apache 日志文件位于 `/chroot/var/log/httpd` 目录，而不是 `/var/log/httpd`。

创建 `apache` 文件（`touch /etc/logrotate.d/apache`）并添加：

```text
/chroot/httpd/var/log/httpd/access_log {
  missingok
  postrotate
    /usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd
  endscript
}

/chroot/httpd/var/log/httpd/error_log {
  missingok
  postrotate
    /usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd
  endscript
}

/chroot/httpd/var/log/httpd/ssl_request_log {
  missingok
  postrotate
    /usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd
  endscript
}
```

建议拆分此文档查询。为了顺利完成，需要说明对 PHP 安装文件进行何种后处理。

已指出。

已观察并评估了当前文档状况以及应用的数字特许。此处呈现合并页面的处理变体，在保留与 ApacheZIP 包含内容相关完整性的同时，注明了可能不稳定的计划归档分类的技术保存。关于 `...Apache` 章节的更具体说明需要保持生成链接。

技术插入部分由定义分隔。

```text
/chroot/httpd/var/log/httpd/ssl_engine_log {
  missingok
  postrotate
    /usr/bin/killall -HUP /chroot/httpd/usr/sbin/httpd
  endscript
}
```

## 优化 Apache

### Apache 的 `mod_mmap_static` 模块

Apache 发行版中有一个名为 `mod_mmap_static` 的特殊模块，可用于提高 Web 服务器的性能。该模块通过提供对 RootDirectory 中不经常更改的频繁请求文件的静态配置列表的映射来工作。因此，如果 Apache 显示的文件不经常更改，您可以使用此模块将静态文档映射到内存中，从而提高 Apache Web 服务器的速度。

需要注意的是，`mod_mmap_static` 模块必须在 Apache 的配置和编译期间启用后才能使用。如果您遵循了上述配置和编译时间部分中的描述，Apache 中已经包含此功能（`--add-module=../mod_mmap_static.c`）。

### 第 1 步

- 要将静态文档映射到内存中，请使用以下命令：

  ```bash
  [root@deep /]# find /home/httpd/ona -type f -print | sed -e 's/.*/mmapfile &/' > /etc/httpd/conf/mmap.conf
  ```

`/home/httpd/ona` 是 RootDirectory，或者更确切地说，是您将从中提供文档的目录；`/etc/httpd/conf/mmap.conf` 是我们希望创建此文件的位置，`mmap.conf` 文件包含 RootDirectory 下所有文档的静态内存映射。

### 第 2 步

一旦在选定位置创建了 `mmap.conf` 文件，我们必须将其包含在 Apache 的 `httpd.conf` 文件中，才能在我们的 Web 服务器上使用其功能。

编辑 `httpd.conf` 文件（`vi /etc/httpd/conf/httpd.conf`）并添加以下行：

```apache
<IfModule mod_include.c>
Include conf/mmap.conf
</IfModule>
```

**注意：** 有关 `mod_mmap_static` 使用的更多信息，请参阅 Apache 文档。请记住，此功能仅应在您网站上不经常更改的文档时使用。

### 第 3 步

您必须重新启动 Apache Web 服务器才能使更改生效：

- 要重新启动 Apache，请使用以下命令：

  ```bash
  [root@deep /]# /etc/rc.d/init.d/httpd restart

  Shutting down http:              [ OK ]

  Starting httpd:                  [ OK ]
  ```



### `atime` 和 `noatime` 属性

Linux 的 `atime` 和 `noatime` 属性可用于在 Apache 中获得可测量的性能提升。

有关此主题的更多信息，请参阅本书第 4 章“常规系统优化”。

### Apache Web 服务器的安装文件

- `/etc/rc.d/init.d/httpd`
- `/etc/rc.d/rc0.d/K15httpd`
- `/etc/rc.d/rc1.d/K15httpd`
- `/etc/rc.d/rc2.d/K15httpd`
- `/etc/rc.d/rc3.d/S85httpd`
- `/etc/rc.d/rc4.d/S85httpd`
- `/etc/rc.d/rc5.d/S85httpd`
- `/etc/rc.d/rc6.d/K15httpd`
- `/etc/logrotate.d/apache`
- `/etc/httpd`
- `/etc/httpd/conf`
- `/etc/httpd/conf/httpd.conf.default`
- `/etc/httpd/conf/httpd.conf`
- `/etc/httpd/conf/mime.types.default`
- `/etc/httpd/conf/mime.types`
- `/etc/httpd/conf/magic.default`
- `/etc/httpd/conf/magic`
- `/etc/httpd/php.ini`
- `/home/httpd`
- `/home/httpd/cgi-bin`
- `/home/httpd/cgi-bin/printenv`
- `/home/httpd/cgi-bin/test-cgi`
- `/usr/bin/htpasswd`
- `/usr/bin/htdigest`
- `/usr/bin/dbmmanage`
- `/usr/include/apache`
- `/usr/include/apache/xml`
- `/usr/include/apache/xml/asciitab.h`
- `/usr/include/apache/xml/hashtable.h`
- `/usr/include/apache/xml/iasciitab.h`
- `/usr/include/apache/xml/latin1tab.h`
- `/usr/include/apache/xml/nametab.h`
- `/usr/include/apache/xml/utf8tab.h`
- `/usr/include/apache/xml/xmidef.h`
- `/usr/include/apache/xml/xmlparse.h`
- `/usr/include/apache/xml/xmlrole.h`
- `/usr/include/apache/xml/xmltok.h`
- `/usr/include/apache/xml/xmltok_impl.h`
- `/usr/include/apache/alloc.h`
- `/usr/include/apache/ap.h`
- `/usr/include/apache/ap_compat.h`
- `/usr/include/apache/ap_config.h`
- `/usr/include/apache/ap_config_auto.h`
- `/usr/include/apache/ap_ctx.h`
- `/usr/include/apache/ap_ctype.h`
- `/usr/include/apache/ap_hook.h`
- `/usr/include/apache/ap_md5.h`
- `/usr/include/apache/ap_mm.h`
- `/usr/include/apache/ap_mmn.h`
- `/usr/include/apache/ap_sha1.h`
- `/usr/include/apache/buff.h`
- `/usr/include/apache/compat.h`
- `/usr/include/apache/conf.h`
- `/usr/include/apache/explain.h`
- `/usr/include/apache/fnmatch.h`
- `/usr/include/apache/hsregex.h`
- `/usr/include/apache/http_conf_globals.h`
- `/usr/include/apache/http_config.h`
- `/usr`
- `/usr/include/apache/http_core.h`
- `/usr/include/apache/http_log.h`
- `/usr/include/apache/http_main.h`
- `/usr/include/apache/http_protocol.h`
- `/usr/include/apache/http_request.h`
- `/usr/include/apache/http_vhost.h`
- `/usr/include/apache/httpd.h`
- `/usr/include/apache/multithread.h`
- `/usr/include/apache/rfc1413.h`
- `/usr/include/apache/scoreboard.h`
- `/usr/include/apache/util_date.h`
- `/usr/include/apache/util_md5.h`
- `/usr/include/apache/util_script.h`
- `/usr/include/apache/util_uri.h`
- `/usr/include/apache/os.h`
- `/usr/include/apache/os-inline.c`
- `/usr/lib/apache`
- `/usr/man/man1/htpasswd.1`
- `/usr/man/man1/htdigest.1`
- `/usr/man/man1/dbmmanage.1`
- `/usr/man/man8/ab.8`
- `/usr/man/man8/httpd.8`
- `/usr/man/man8/logresolve.8`
- `/usr/man/man8/rotatelogs.8`
- `/usr/man/man8/apxs.8`
- `/usr/sbin/httpd`
- `/usr/sbin/ab`
- `/usr/sbin/logresolve`
- `/usr/sbin/rotatelogs`
- `/usr/sbin/apxs`
- `/var/log/httpdTekst`
- `/var/cache`
- `/var/cache/httpd`

### 使用 Apache Web 服务器的 PHP4 服务器端脚本语言安装文件

- `/usr/bin/phpize`
- `/usr/bin/php-config`
- `/usr/include/php`
- `/usr/include/php/Zend`
- `/usr/include/php/Zend/FlexLexer.h`
- `/usr/include/php/Zend/acconfig.h`
- `/usr/include/php/Zend/modules.h`
- `/usr/include/php/Zend/zend-parser.h`
- `/usr/include/php/Zend/zend-scanner.h`
- `/usr/include/php/Zend/zend.h`
- `/usr/include/php/Zend/zend_API.h`
- `/usr/include/php/Zend/zend_alloc.h`
- `/usr/include/php/Zend/zend_builtin_functions.h`
- `/usr/include/php/Zend/zend_compile.h`
- `/usr/include/php/Zend/zend_config.h`
- `/usr/include/php/Zend/zend_config.w32.h`
- `/usr/include/php/Zend/zend_constants.h`
- `/usr/include/php/Zend/zend_dynamic_array.h`
- `/usr/include/php/Zend/zend_errors.h`
- `/usr/include/php/Zend/zend_execute.h`
- `/usr/include/php/Zend/zend_execute_locks.h`
- `/usr/include/php/Zend/zend_extensions.h`
- `/usr/include/php/Zend/zend_fast_cache.h`
- `/usr/include/php/Zend/zend_globals.h`
- `/usr/include/php/Zend/zend_globals_macros.h`
- `/usr/include/php/Zend/zend_hash.h`
- `/usr/include/php/Zend/zend_highlight.h`
- `/usr/include/php/Zend/zend_indent.h`
- `/usr/include/php/Zend/zend_list.h`
- `/usr/include/php/Zend/zend_llist.h`
- `/usr/include/php/Zend/zend_operators.h`
- `/usr/include/php/Zend/zend_ptr_stack.h`
- `/usr/include/php/Zend/zend_stack.h`
- `/usr/include/php/Zend/zend_variables.h`
- `/usr/include/php/TSRM`
- `/usr/include/php/TSRM/TSRM.h`
- `/usr/include/php/ext`
- `/usr/include/php/ext/standard`
- `/usr/include/php/ext/standard/base64.h`
- `/usr/include/php/ext/standard/basic_functions.h`
- `/usr/include/php/ext/standard/cyr_convert.h`
- `/usr/include/php/ext/standard/datetime.h`
- `/usr/include/php/ext/standard/dl.h`
- `/usr/include/php/ext/standard/dns.h`
- `/usr/include/php/ext/standard/exec.h`
- `/usr/include/php/ext/standard/file.h`
- `/usr/include/php/ext/standard/flock_compat.h`
- `/usr/include/php/ext/standard/fsock.h`
- `/usr/include/php/ext/standard/global.h`
- `/usr/include/php/ext/standard/head.h`
- `/usr/include/php/ext/standard/html.h`
- `/usr/include/php/ext/standard/info.h`
- `/usr/include/php/ext/standard/md5.h`
- `/usr/include/php/ext/standard/microtime.h`
- `/usr/include/php/ext/standard/pack.h`
- `/usr/include/php/ext/standard/pageinfo.h`
- `/usr/include/php/ext/standard/php_array.h`
- `/usr/include/php/ext/standard/php_assert.h`
- `/usr/include/php/ext/standard/php_browscap.h`
- `/usr/include/php/ext/standard/php_crypt.h`
- `/usr/include/php/ext/standard/php_dir.h`
- `/usr/include/php/ext/standard/php_filestat.h`
- `/usr/include/php/ext/standard/php_image.h`
- `/usr/include/php/ext/standard/php_iptc.h`
- `/usr/include/php/ext/standard/php_lcg.h`
- `/usr/include/php/ext/standard/php_link.h`
- `/usr/include/php/ext/standard/php_mail.h`
- `/usr/include/php/ext/standard/php_metaphone.h`
- `/usr/include/php/ext/standard/php_output.h`
- `/usr/include/php/ext/standard/php_rand.h`
- `/usr/include/php/ext/standard/php_standard.h`
- `/usr/include/php/ext/standard/php_string.h`
- `/usr/include/php/ext/standard/php_syslog.h`
- `/usr/include/php/ext/standard/php_var.h`
- `/usr/include/php/ext/standard/phpdir.h`
- `/usr/include/php/ext/standard/phpmath.h`
- `/usr/include/php/ext/standard/quot_print.h`
- `/usr/include/php/ext/standard/reg.h`
- `/usr/include/php/ext/standard/type.h`
- `/usr/include/php/ext/standard/uniqid.h`
- `/usr/include/php/ext/standard/url.h`
- `/usr/include/php/ext/standard/url_scanner.h`
- `/usr/include/php/regex`
- `/usr/include/php/regex/regex.h`
- `/usr/include/php/regex/regex_extra.h`
- `/usr/include/php/php.h`
- `/usr/include/php/php_regex.h`
- `/usr/include/php/php3_compat.h`
- `/usr/include/php/safe_mode.h`
- `/usr/include/php/fopen-wrappers.h`
- `/usr/include/php/php_version.h`
- `/usr/include/php/php_globals.h`
- `/usr/include/php/php_reentrancy.h`
- `/usr/include/php/php_ini.h`
- `/usr/include/php/SAPI.h`
- `/usr/include/php/php_config.h`
- `/usr/include/php/zend_config.h`
- `/usr/include/php/build-defs.h`
- `/usr/lib/php`
- `/usr/lib/php/Zend`

### 配合 Apache Web 服务器使用的 `mod_perl` 编程语言已安装文件

- `/usr/lib/perl5/5.00503/i386-linux/perllocal.pod`
- `/usr/lib/perl5/man/man3/Apache.3`
- `/usr/lib/perl5/man/man3/Apache::Constants.3`
- `/usr/lib/perl5/man/man3/Apache::Leak.3`
- `/usr/lib/perl5/man/man3/Apache::Log.3`
- `/usr/lib/perl5/man/man3/Apache::PerlRunXS.3`
- `/usr/lib/perl5/man/man3/Apache::Symbol.3`
- `/usr/lib/perl5/man/man3/Apache::Table.3`
- `/usr/lib/perl5/man/man3/Apache::URI.3`
- `/usr/lib/perl5/man/man3/Apache::Util.3`
- `/usr/lib/perl5/man/man3/Apache::FakeRequest.3`
- `/usr/lib/perl5/man/man3/mod_perl.3`
- `/usr/lib/perl5/man/man3/Apache::ExtUtils.3`
- `/usr/lib/perl5/man/man3/Apache::SIG.3`
- `/usr/lib/perl5/man/man3/Apache::Status.3`
- `/usr/lib/perl5/man/man3/Apache::Include.3`
- `/usr/lib/perl5/man/man3/Apache::Debug.3`
- `/usr/lib/perl5/man/man3/Apache::Resource.3`
- `/usr/lib/perl5/man/man3/Apache::src.3`
- `/usr/lib/perl5/man/man3/Apache::PerlRun.3`
- `/usr/lib/perl5/man/man3/Apache::httpd_conf.3`
- `/usr/lib/perl5/man/man3/mod_perl_traps.3`
- `/usr/lib/perl5/man/man3/Apache::Options.3`
- `/usr/lib/perl5/man/man3/mod_perl_cvs.3`
- `/usr/lib/perl5/man/man3/Apache::Symdump.3`
- `/usr/lib/perl5/man/man3/Apache::RegistryLoader.3`
- `/usr/lib/perl5/man/man3/mod_perl_method_handlers.3`
- `/usr/lib/perl5/man/man3/mod_perl_tuning.3`
- `/usr/lib/perl5/man/man3/cgi_to_mod_perl.3`
- `/usr/lib/perl5/man/man3/Apache::StatINC.3`
- `/usr/lib/perl5/man/man3/Apache::Registry.3`
- `/usr/lib/perl5/man/man3/Bundle::Apache.3`
- `/usr/lib/perl5/man/man3/Apache::SizeLimit.3`
- `/usr/lib/perl5/man/man3/Apache::PerlSections.3`
- `/usr/lib/perl5/man/man3/Apache::RedirectLogFix.3`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/buff.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/multithread.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/httpd.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_config.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/alloc.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_md5.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_ctx.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/util_md5.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/rfc1413.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/conf.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/util_uri.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/explain.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_compat.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/http_config.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_sha1.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/scoreboard.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/compat.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/http_request.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/http_core.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_mm.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/http_protocol.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/util_date.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_hook.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/http_main.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/http_conf_globals.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/util_script.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/http_vhost.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_ctype.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/hsregex.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_mmn.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/ap_config_auto.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/http_log.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/include/fnmatch.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/netware`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/netware/os.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/netware/getopt.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/netware/test_char.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/netware/uri_delims.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/netware/precomp.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/bs2000`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/bs2000/os-inline.c`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/bs2000/ebcdic.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/bs2000/os.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/tpf`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/tpf/ebcdic.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/tpf/os.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/tpf/os-inline.c`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/service.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/getopt.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/registry.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/resource.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/installer`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/installer/installdll`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/installer/installdll/test`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/installer/installdll/test/test.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/installer/installdll/test/resource.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/os.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/passwd.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/win32/readdir.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/unix`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/unix/os.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/unix/os-inline.c`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/os390`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/os390/os-inline.c`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/os390/ebcdic.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/os390/os.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/mpeix`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/mpeix/os-inline.c`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/mpeix/os.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/os2`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/os2/os.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/os/os2/os-inline.c`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/ssl`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/ssl/ssl_expr.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/ssl/ssl_util_table.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/ssl/ssl_util_ssl.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/ssl/ssl_expr_parse.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/ssl/mod_ssl.h`

# 第9章

服务器软件（Web 网络服务）

## 服务器软件（Web 网络服务）

- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/ssl/ssl_util_sdbm.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/perl`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/perl/mod_perl.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/perl/mod_perl_version.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/perl/perl_PL.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/perl/mod_perl_xs.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/php4`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/php4/mod_php4.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/proxy`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/proxy/mod_proxy.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/standard`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/modules/standard/mod_rewrite.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/support`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/support/suexec.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/asciitab.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/latin1tab.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/xmldef.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/xmlparse.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/xmltok.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/xmlrole.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/hashtable.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/nametab.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/xmltok_impl.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/utf8tab.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/lib/expat-lite/ascitab.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/regex`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/regex/utils.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/regex/regex2.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/regex/cclass.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/include/regex/cname.h`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/typemap`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/Leak`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/Leak/Leak.so`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/Leak/Leak.bs`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/Symbol`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/Symbol/Symbol.so`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/Apache/Symbol/Symbol.bs`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/mod_perl`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/mod_perl/.packlist`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/mod_perl.pod`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Bundle`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Bundle/Apache.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/test.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Debug.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Resource.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/src.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/httpd_conf.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Symdump.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/RegistryLoader.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Registry.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/SizeLimit.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/RedirectLogFix.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/MyConfig.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Constants`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Constants/Exports.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/SIG.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/StatINC.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Opcode.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/PerlSections.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/FakeRequest.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/ExtUtils.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Include.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Status.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/PerlRun.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Options.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/RegistryNG.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/RegistryBB.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Connection.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Constants.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/File.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Leak.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Log.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/ModuleConfig.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/PerlRunXS.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Server.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Symbol.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Table.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/URI.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache/Util.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/mod_perl_hooks.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/mod_perl_hooks.pm.PL`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/mod_perl_tuning.pod`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/mod_perl_cvs.pod`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/mod_perl_method_handlers.pod`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/mod_perl.pm`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/mod_perl_traps.pod`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/cgi_to_mod_perl.pod`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/Apache.pm`

# 第20章 可选的 Apache 安装组件

### 本章内容

- Webalizer
- 配置
- 通知 Apache Webalizer 的输出目录
- 首次手动运行 Webalizer
- 使用 `cron` 作业自动运行 Webalizer
- FAQ-O-Matic
- 通知 Apache FAQ-O-Matic 文件的位置
- 配置 FAQ-O-Matic 软件
- Webmail IMP
- 设置 Horde 程序所需的 PHPLib
- 配置并创建 Webmail IMP SQL 数据库
- 配置 PHP4 的 `php.ini` 配置文件
- 配置 Apache 以识别 Webmail IMP

## 可选的 Apache 安装组件

在本章中，我将介绍三个可以安装在你的 Linux 服务器上的有用外部程序。这些程序是专门为配合 Apache Web 服务器使用而开发的，只有当你打算在组织中使用 Apache 时才有用。如果不是这种情况，你可以跳过本章，继续阅读本书的其余部分。首先，我们将介绍 Webalizer，它是一个 Web 服务器日志文件分析程序。然后我们将讨论 FAQ-O-Matic，当你希望在服务器上提供 FAQ 列表、错误追踪数据库、文档等内容时可以使用它。最后，我们将介绍一个非常复杂且有趣的程序——Webmail，它允许你以安全的方式为客户提供免费邮件账户，或者访问和阅读你的邮件。

## Linux Webalizer

### 概述

像 Apache 这样的 Web 服务器会将所有预定义的日志条目信息记录到一个文本文件中，Web 管理员可以查看和分析该文件。该文件还可以通过一个特殊程序进行评估，该程序能够以图形方式呈现信息，使管理员更容易解读。

正如 Webalizer 的 README 文件中所述：

Webalizer 是一个 Web 服务器日志文件分析程序，它生成 HTML 格式的使用统计信息，以便通过浏览器查看。结果以列式和图形格式呈现，便于解读。它会展示年度、月度、日度和小时度的使用统计信息，以及按站点、URL、引荐来源、用户代理（浏览器）和国家/地区（用户代理和引荐来源仅在 Web 服务器生成“组合日志格式”文件时可用）显示使用情况的功能。

### 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为 `"/var/tmp"`（也可以使用其他路径）。
- 安装在 Red Hat Linux 6.1 和 6.2 上进行了测试。
- 安装的所有步骤都将以超级用户账户 `"root"` 执行。
- Webalizer 版本号为 `1_30-04`。

### 软件包

- Webalizer 主页：http://www.mrunix.net/webalizer/
- Webalizer FTP 站点：`207.153.121.6`
- 请务必下载：`webalizer-1_30-04-src.tgz`

### 编译

解压 tarball（tar.gz）。

```text
``` 



```bash
[root@deep /]# cp webalizer-version-src.tgz /var/tmp/
[root@deep /]# cd /var/tmp/
[root@deep tmp]# tar xzpf webalizer-version-src.tgz
```

## 前置条件

Webalizer 要求 GD 图形库必须已经安装在您的系统上，该库用于为 Webalizer 程序生成内联图形。如果尚未安装，则必须从您的 Red Hat Linux CD-ROM 进行安装。

- 要验证 GD 软件包是否已安装在您的 Linux 系统上，请使用以下命令：

```bash
[root@deep /]# rpm -qi gd

package gd is not installed
```

- 要在您的 Linux 系统上安装 GD 软件包，请使用以下命令：

```bash
[root@deep /]# mount /dev/cdrom /mnt/cdrom/
[root@deep /]# cd /mnt/cdrom/RedHat/RPMS/
[root@deep RPMS]# rpm -Uvh gd-version.i386.rpm

gd      ##################################################

[root@deep RPMS]# rpm -Uvh gd-devel-version.i386.rpm

gd-devel  ##################################################

[root@deep RPMS]# cd /; umount /mnt/cdrom/
```

- 当然，您的系统上应该已经安装了 Apache Web 服务器，这样才能使用 Webalizer 软件。

**注意：** 有关 Apache Web 服务器的更多信息，请参阅本书中相关的章节。

## 编译

进入新的 Webalizer 目录，然后在终端中输入以下命令：

```bash
CC="egcs" \
CFLAGS="-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
./configure \
--prefix=/usr
```

```bash
[root@deep webalizer-1.30-04]# make
[root@deep webalizer-1.30-04]# make install
[root@deep webalizer-1.30-04]# mkdir /home/httpd/usage
```

`make` 命令将把所有源文件编译为可执行二进制文件，`make install` 将安装二进制文件及所有支持文件到适当的位置。`mkdir` 将在`/home/httpd/`目录下创建一个名为`usage`的新目录，我们将在那里处理所有与 Webalizer 相关的文件。

## 工作完成后清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf webalizer-version/ webalizer-version-src.tgz
```

`rm` 命令将删除我们用于编译和安装 Webalizer 的所有源文件。它还会从`/var/tmp`目录中删除 Webalizer 的压缩归档文件。

## 配置

本书中描述的所有软件在名为`floppy.tgz`的 tar 压缩归档中都有特定的目录和子目录，其中包含用于特定程序的文件配置。如果您获得此归档文件，将不必手动复制以下不同的配置文件，或剪切粘贴它们来创建您的配置文件。无论您决定手动复制它们，还是从归档中获取为您准备好的文件，您都有责任根据您的需求进行修改、调整，并将与 Webalizer 软件相关的文件放置在服务器上的适当位置，如下所示。服务器配置文件归档的下载地址位于以下网址：

[http://www.openna.com/books/floppy.tgz](http://www.openna.com/books/floppy.tgz)

要运行 Webalizer，需要以下文件，并且必须创建或复制到服务器上的适当目录。

将`webalizer.conf`文件复制到`/etc/`目录。

您可以在我们的`floppy.tgz`归档中获取下面列出的配置文件。从解压后的`floppy.tgz`归档中将以下文件复制到适当位置，或直接从本书复制粘贴到相关文件中。

## `/etc/webalizer.conf` 文件的配置

`/etc/webalizer.conf`是 Webalizer 的默认配置文件。通过它，您可以指定要分析的站点中的哪些目录或页面、要隐藏的 URL 等等。默认情况下，Webalizer 程序会在 Linux 的`/etc/`目录下安装一个名为`webalizer.conf.sample`的示例配置文件。您可以使用此文件来配置您的选项，然后将其重命名为`webalizer.conf`，Webalizer 程序将能够找到并使用它。

存在大量选项，阅读 Webalizer 附带的文档以了解所有不同设置和参数的更多信息非常重要。此外，重要的是要注意，我们在此 Webalizer 配置文件中仅注释了最常见和使用的参数。

编辑`webalizer.conf.sample`文件（`vi /etc/webalizer.conf.sample`）或创建`webalizer.conf`文件（`touch /etc/webalizer.conf`），并在该文件中添加或修改：

```text
LogFile /var/log/httpd/access_log

OutputDir /home/httpd/usage

Incremental  yes

PageType  htm*

PageType  cgi

PageType  php

HideURL  *.gif

HideURL  *.GIF

HideURL  *.jpg

HideURL  *.JPG

HideURL  *.ra

IgnoreURL  /taskbar*
```

## 这告诉 `webalizer.conf` 文件为以下特定配置设置进行配置

### `LogFile /var/log/httpd/access_log`

`LogFile`选项指定要与 Webalizer 一起使用的日志文件。默认日志文件应该是 Apache Web 服务器的`access_log`，但您可以指定不同的日志文件，例如，如果您在 httpd-accelerator 模式下使用 Squid 代理服务器时生成的名为`access.log`的日志文件。更多信息请参阅第 18 章“服务器软件代理网络服务”。

### `OutputDir /home/httpd/usage`

`OutputDir`选项指定用于 Webalizer 报告的输出目录位置。Webalizer 程序生成的所有当前和未来的报告文件都将托管在此目录中。建议您将 Apache 网站的所在位置创建此目录。

### `Incremental yes`

如果`Incremental`选项设置为`Yes`，则告诉程序仅处理部分日志文件，并允许您根据需要随时轮换日志文件而不会丢失访问信息。建议将此选项设置为`Yes`。

### `PageType htm* cgi php`

`PageType`选项指定您希望 Webalizer 将哪些文件扩展名视为要计数的页面。每个添加的文件扩展名必须按照上面 Webalizer 配置文件中所示在其自己的行上指定。

### `HideURL *.gif *.GIF *.jpg *.JPG *.ra`

`HideURL`选项指定要从报告页面中隐藏哪些类型的项目，例如图形文件、音频文件或其他“非 html”文件。每个添加的项目必须按照上面 Webalizer 配置文件中示例在其自己的行上指定。

### `IgnoreURL /taskbar*`

`IgnoreURL`选项指定要从生成的统计报告中完全忽略的 URL。此选项可用于忽略在我们的统计报告中不重要的目录。当您想要管理和分类应监控哪些 URL 以及应忽略哪些 URL 时，它也很有用。

**注意：** 如果您决定使用现有的`/etc/webalizer.conf.sample`文件来配置 Webalizer 的参数，请不要忘记将其重命名为`webalizer.conf`，否则程序将无法使用它。

## 通知 Apache Webalizer 的输出目录

一旦 Webalizer 安装在系统中，我们必须在 Apache 的`httpd.conf`文件中添加以下行，以便能够定位和使用其功能。

### 步骤 1

编辑`httpd.conf`文件（`vi /etc/httpd/conf/httpd.conf`），并在`<IfModule mod_alias.c>`和`</IfModule>`部分标签之间添加以下行：

```apache
Alias /usage/ "/home/httpd/usage/"

<Directory "/home/httpd/usage">
  Options None
  AllowOverride None
  Order deny,allow
  Deny from all
  Allow from 192.168.1.0/24
</Directory>
```

### 步骤 2

在将上述行添加到`httpd.conf`文件后，不要忘记重新启动您的 Apache Web 服务器。

要重新启动 Apache，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/httpd restart
Shutting down http:  [ OK ]
Starting httpd:      [ OK ]
```

## 首次手动运行 Webalizer

现在是时候运行该程序以在默认的 Webalizer 目录中生成报告（html）和图形，以便我们可以在 Web 浏览器界面中看到它们。此步骤仅在您首次安装和使用 Webalizer 时需要，因为以后最好使用 cron 作业来自动化此任务。

要手动运行 Webalizer 以生成报告，请使用以下命令：

```text
[root@deep /]# /usr/bin/webalizer

Webalizer V1.30-04 (Linux 2.2.14) English

Using logfile /var/log/httpd/access_log

Creating output in /home/httpd/usage

Hostname for reports is 'deep.openna.com'

History file not found...

Previous run data not found...

Saving current run data... [03/06/2000 04:42:03]

Generating report for March 2000

Generating summary report

Saving history information...

81 records (2 ignored) in 0.31 seconds
```

在此阶段，我们应该验证 Webalizer 是否在系统上正常工作。为此，请将您的 Web 浏览器指向以下地址：[http://my-web-server/usage/](http://my-web-server/usage/)。

`<my-web-server>`是您的 Apache Web 服务器所在的地址，`<usage>`是托管所有 Webalizer 报告文件的目录。

## 使用 cron 作业自动运行 Webalizer

您现在可以做的最后一件事是自动生成新日志文件以更新 Webalizer 报告的任务。在 root 的 crontabs 中添加一个条目，使 Webalizer 作为 cron 作业运行。

要将 Webalizer 添加到您的 cron 任务中，您必须编辑 crontab 并添加以下行来运行它，例如，对于繁忙的网站每 28 分钟运行一次。

要编辑 crontab 以自动化该任务，请使用以下命令（以 root 身份）：

```bash
[root@deep /]# crontab -e

# 每 28 分钟运行一次 Webalizer 以更新 Apache 日志文件。
28 * * * * /usr/bin/webalizer
```

## 已安装文件

- `/etc/webalizer.conf.sample`
- `/usr/bin/webalizer`
- `/usr/man/man1/webalizer.1`

# Linux FAQ-O-Matic

## 概述

正如 Faq-O-Matic 网站所解释的：

邮件列表存档很好，因为它能让有常见问题的人搜索到即时答案，并避免打扰那些有答案的人。不幸的是，邮件列表存档中的答案会随时间变得陈旧、杂乱无章，并且很难从邮件列表的对话噪音中筛选出来。

常见问题列表（FAQ）更好，因为有疑问的人可以稍微偷懒一点，仍然能立即找到他们的答案。不幸的是，维护 FAQ 列表需要付出努力；如果拥有答案的人变得懒惰，FAQ 列表就会变得陈旧。

Faq-O-Matic 是一个基于 CGI 的系统，用于自动化维护 FAQ（或常见问题列表）的过程。它允许访问您 FAQ 的用户参与保持其最新状态。权限系统还使其可用作帮助台应用程序、错误跟踪数据库或文档系统。

## 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为`/var/tmp`（其他路径也可以）。
- 安装在 Red Hat Linux 6.1 和 6 slang_Cur" 以及 6.2 上进行了测试。
- 安装中的所有步骤都将在超级用户账户`root`下执行。
- FAQ-O-Matic 版本号为 2.709。

## 软件包

FAQ-O-Matic 主页：[http://www.dartmouth.edu/~jonh/ff-serve/cache/1.html](http://www.dartmouth.edu/~jonh/ff-serve/cache/1.html)

最新版本的 FAQ-O-Matic 始终可以在以下地址获取：

[ftp://ftp.cs.dartmouth.edu/pub/jonh](ftp://ftp.cs.dartmouth.edu/pub/jonh)。

您必须确保下载：`FAQ-O-Matic-2.709.tar.gz`。

## 前置条件

- 您的系统上应该已经安装了 Apache Web 服务器，以便能够使用 FAQ-O-Matic 软件。
- 您的系统上还应该已经安装了修订控制系统（RCS）文件版本管理工具，以便能够使用 FAQ-O-Matic 软件。

要验证 RCS 软件包是否已安装在您的系统上，请使用以下命令：

```bash
[root@deep /]# rpm -qi rcs

软件包 rcs 未安装
```

要在您的 Linux 系统上安装 RCS 软件包，请使用以下命令：

```bash
[root@deep /]# mount /dev/cdrom /mnt/cdrom/
[root@deep /]# cd /mnt/cdrom/RedHat/RPMS/
[root@deep RPMS]# rpm -Uvh rcs-version.i386.rpm

rcs

###############################################################

[root@deep RPMS]# cd /; umount /mnt/cdrom/
```

**注意：** 有关所需软件的更多信息，请参阅本书中的相关章节。

## 解压

解压 tarball（`tar.gz`）。

```bash
[root@deep /]# cp FAQ-O-Matic-version.tar.gz /var/tmp/
[root@deep /]# cd /var/tmp/
[root@deep tmp]# tar xzpf FAQ-O-Matic-version.tar.gz
```

## 编译

要在您的计算机上安装 Faq-O-Matic 程序，请进入新的 FAQ-O-Matic 目录并在终端上输入以下命令：

```bash
[root@deep FAQ-O-Matic-2.709]# perl Makefile.PL
[root@deep FAQ-O-Matic-2.709]# make
[root@deep FAQ-O-Matic-2.709]# make install
[root@deep FAQ-O-Matic-2.709]# mv fom /home/httpd/cgi-bin/ （或您的 CGI 所在位置）。
[root@deep FAQ-O-Matic-2.709]# mkdir -p /home/httpd/cgi-bin/fom-meta
[root@deep FAQ-O-Matic-2.709]# mkdir -p /home/httpd/faqomatic
[root@deep FAQ-O-Matic-2.709]# chown root.www /home/httpd/cgi-bin/fom
[root@deep FAQ-O-Matic-2.709]# chown -R www.www /home/httpd/cgi-bin/fom-meta/
[root@deep FAQ-O-Matic-2.709]# chown suffoc.www /home/httpd/faqomatic/
```




`make` 命令将把所有源文件编译成可执行二进制文件，`make install` 将把 Perl 程序和任何支持文件安装到适当的位置。`mv` 命令将把 Faq-O-Matic 的主 CGI 程序 `fom` 移动到您的 Apache Web 服务器的 `cgi-bin` 目录。`mkdir` 将在 `/home/httpd/` 目录下创建名为 `fom-meta` 和 `faqomatic` 的新目录，我们将在那里处理所有相关的 FAQ-O-Matic 文件。最后，`chown` 命令将 `fom` CGI 程序的所有者设置为超级用户 `root`，组设置为 Apache 运行时的用户 `www`，并将目录 `fom-meta` 和 `faqomatic` 的所有者设置为 `www`，组设置为 `www`。

**注意：** 在软件编译过程中，您将通过邮件收到一个临时密码。该密码将是后续通过 Web 界面完成 Faq-O-Matic 安装所必需的。

### 通知 Apache Faq-O-Matic 文件的位置

一旦 Faq-O-Matic 安装到系统中，我们必须将以下行添加到 Apache 的 `httpd.conf` 文件中，以便能够定位和使用其功能。

#### 步骤 1

编辑 `httpd.conf` 文件（`vi /etc/httpd/conf/httpd.conf`），并在部分标签 `<IfModule mod_alias.c>` 和 `</IfModule>` 之间添加以下行：

```apache
Alias /faqomatic/ "http://www.books.moir.com.au/FAQ-O-Matic/"

<Directory "http://www.books.moir.com.au/FAQ-O-Matic/">

  Options None

  AllowOverride None

  Order allow,deny

  Allow from all

</Directory>

Alias /bags/ "http://www.books.moir.com.au/bags/"

<Directory "http://www.books.moir.com.au/bags/">

  Options None

  AllowOverride None

  Order allow,deny

  Allow from all

</Directory>
```

```apache
Allow from all

</Directory>
```

```apache
Alias /cache/ "/home/httpd/faqomatic/cache/"

<Directory "/home/httpd/faqomatic/cache">

  Options None

  AllowOverride None

  Order allow,deny

  Allow from all

</Directory>
```

```apache
Alias /item/ "/home/httpd/faqomatic/item/"

<Directory "/home/httpd/faqomatic/item">

  Options None

  AllowOverride None

  Order allow,deny

  Allow from all

</Directory>
```

#### 步骤 2

不要忘记在将上述行添加到其 `httpd.conf` 文件后重新启动您的 Apache Web 服务器。

要重新启动 Apache，请使用以下命令：

```shell
[root@deep /]# /etc/rc.d/init.d/httpd restart

正在关闭 httpd:           [ 确定 ]

正在启动 httpd:           [ 确定 ]
```

### 配置您的 FAQ-O-Matic 软件

此安装的其余部分将通过您的 Web 浏览器完成。使用 Netscape Communicator，请按照以下简单步骤操作：

#### 步骤 1

第一步是加载您的 Web 浏览器并使用它来配置 Faq-O-Matic。

1. 将您的 Netscape 浏览器指向以下位置：[http://my-web-server/cgi-bin/fom](http://my-web-server/cgi-bin/fom)
2. 输入您的临时密码。
3. 首先创建 `/home/httpd/cgi-bin/fom-meta/` 目录。
4. 在配置主菜单中配置“**定义配置参数**”。

例如，在标记为**必填**的部分下填写以下信息：

```perl
$adminAuth= admin@openna.com

$serverBase= http://www.openna.com

$cgiURL= /cgi-bin/fom

$serveDir= /home/httpd/faqomatic/

$serveURL= /faqomatic/
```

根据需要配置其余“定义配置参数”。完成参数设置后，点击“**定义**”按钮以验证您的选择。

**注意：** `<my-web-server>` 是您的 Apache Web 服务器所在的地址，临时密码是您应该在该软件安装阶段通过邮件收到的密码。

#### 步骤 2

完成“定义配置参数”的配置后，您必须执行 FAQ-O-Matic 配置的其余部分，以便能够按照 FAQ-O-Matic 软件配置主菜单中的描述使用它。

### 工作后的清理

```shell
[root@deep /]# cd /var/tmp

[root@deep tmp]# rm -rf FAQ-O-Matic-version/ FAQ-O-Matic-version.tar.gz
```

`rm` 命令将删除我们用来编译和安装 FAQ-O-Matic 的所有源文件。它还将从 `/var/tmp` 目录中删除 FAQ-O-Matic 的压缩存档。

### 已安装文件

- `/usr/lib/perl5/man/man3/FAQ::OMatic::API.3`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/FAQ`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/FAQ/OMatic`
- `/usr/lib/perl5/site_perl/5.005/i386-linux/auto/FAQ/OMatic/.packlist`
- `/usr/lib/perl5/site_perl/5.005/FAQ`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Bags.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/authenticate.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/ImageRef.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Groups.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/submitGroup.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/recent.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/submitItem.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/maintenance.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Language_de_iso8859_1.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Slow.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/help.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/selectBag.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/submitPart.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/delPart.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/buildSearchDB.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/mirrorServer.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/editItem.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/search.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/SearchMod.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/addItem.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Versions.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/displaySlow.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Language_fr.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/img.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/editPart.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/AuthLocal.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/ColorPicker.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/ImageData.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/changePass.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/submitBag.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/submitModOptions.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/I18N.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Log.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/appearanceForm.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/moveItem.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/editGroups.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/HelpMod.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/searchForm.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/submitPass.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/submitMove.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Set.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/statgraph.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/stats.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Item.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Words.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Appearance.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/dispatch.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/editBag.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/submitCatToAns.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/submitAnsToCat.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/editModOptions.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Auth.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/install.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/Part.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/faq.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic/API.pm`
- `/usr/lib/perl5/site_perl/5.005/FAQ/OMatic.pm`

## Linux Webmail IMP

### 概述

Webmail IMP 允许通过通用、基于 Web 的方式访问 IMAP/POP3 服务器，并提供通讯录、LDAP 目录搜索、完整的发送和接收附件支持，以及许多通常只在桌面邮件客户端中才能找到的其他功能。如果您已安装支持 SSL 的 Apache，客户端可以通过 SSL 加密以安全的方式访问和阅读邮件。在本节中，默认情况下，我们将 Webmail IMP 配置为使用 PostgreSQL 数据库和 IMAP 连接。不过，Webmail IMP 还支持许多其他数据库。如果需要，您也可以使用 MySQL、Oracle、Sybase 或其他知名的 SQL 数据库。您还可以选择使用 POP3 而非 IMAP 连接为您的客户端提供服务。

### 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为 `/home/httpd`。
- 安装过程已在 Red Hat Linux 6.1 和 6.2 上测试通过。
- 安装中的所有步骤都将以超级用户账户 `root` 执行。
- Horde 版本号为 `1.2.0`。
- Webmail IMP 版本号为 `2.2.0`。
- PHPLib 版本号为 `7.2b`。

### 软件包

Webmail IMP 主页：[http://www.horde.org/imp/](http://www.horde.org/imp/)

您务必下载：

- `horde-1.2.0-pre11.tar.gz`
- `imp-2.2.0-pre11.tar.gz`

PHPLib 主页：[http://phplib.netuse.de/index.php3](http://phplib.netuse.de/index.php3)

您务必下载：

- `phplib-7.2b.tar.gz`

### 前提条件

- 您的系统上应已安装 Apache Web 服务器，以便能够使用 Webmail IMP 软件。
- 您的系统上应已安装 PHP4 服务器端脚本语言支持，以便能够使用 Webmail IMP 软件。
- 如果您打算将 Webmail IMP 软件与 SQL 支持一起使用，您的系统上应已安装 PostgreSQL 或其他数据库服务器。
- 如果您打算将 Webmail IMP 软件与 LDAP 支持一起使用，您的系统上应已安装 OpenLDAP 目录服务器。
- 您的系统上应已安装 IMAP/POP 服务器，以便能够使用 Webmail IMP 软件。
- 您的系统上应已安装 PHPLIB 文件 `7.2` 或更高版本，以便能够使用 Webmail IMP 软件。

**注意：** 有关所需软件的更多信息，请参阅本书中的相关章节。

可选组件随 Apache 安装，参见第 20 章。

### 设置 Webmail IMP 的 Horde 程序所需的 PHPLib

要能够在 Linux 服务器上运行 Webmail IMP，必须安装 PHPLib 软件（面向 PHP 开发人员的 Web 应用程序开发工具包）。要安装 PHPLib，请按照以下简单步骤操作：

#### 软件包

PHPLib 主页：[http://phplib.netuse.de/index.php3](http://phplib.netuse.de/index.php3)

您务必下载：`phplib-7.2b.tar.gz`

```shell
[root@deep /]# cp phplib-7.2b.tar.gz /home/httpd/

[root@deep /]# cd /home/httpd/

[root@deep httpd]# tar xzpf phplib-7.2b.tar.gz
```

#### 步骤 1

切换到 Web 服务器的 DocumentRoot，并通过执行以下命令创建一个 `/home/httpd/php` 目录：

```shell
[root@deep /]# cd /home/httpd/

[root@deep httpd]# mkdir php
```

#### 步骤 2

将 PHPLib 发行版中 `php` 目录的内容复制到您在 DocumentRoot 中创建的 `php` 目录：




```bash
[root@deep /]# cd /home/httpd/phplib-7.2b/php/

[root@deep php]# cp * /home/httpd/php/

[root@deep php]# cd /home/httpd/

[root@deep httpd]# rm -f phplib-7.2b.tar.gz

[root@deep httpd]# rm -rf phplib-7.2b/
```

**注意：** 一旦完成将 PHPLib 的 `php` 目录复制到我们在 `DocumentRoot` 中创建的新 `php` 目录后，我们将删除 tar 压缩包和 `phplib-version` 目录。

# 编译

要在您的服务器上安装 Webmail IMP 程序，请按照以下简单步骤操作。

## 步骤 1

将 `horde-1.2.0-pre11.tar.gz` 复制到 Web 服务器的 `DocumentRoot`（`/home/httpd/`），解压它，并将目录从 `horde-version` 重命名为 `horde`，方法是执行以下命令：

```bash
[root@deep /]# cp horde-version.tar.gz /home/httpd/

[root@deep /]# cd /home/httpd/

[root@deep httpd]# tar xzpf horde-version.tar.gz

[root@deep httpd]# mv horde-version horde

[root@deep httpd]# rm -f horde-version.tar.gz
```

**注意：** 一旦完成将 Horde 的 `horde-version` 目录移动到其新名称 `horde` 后，我们将删除 Horde 的 tar 压缩包。

## 步骤 2

将 `imp-2.2.0-pre11.tar.gz` 复制到新的 `horde` 目录（`/home/httpd/horde/`），解压它，并将目录从 `imp-version` 重命名为 `imp`，方法是执行以下命令：

```bash
[root@deep /]# cp imp-version.tar.gz /home/httpd/horde/

[root@deep /]# cd /home/httpd/horde/

[root@deep horde]# tar xzpf imp-version.tar.gz

[root@deep horde]# mv imp-version imp

[root@deep horde]# rm -f imp-version.tar.gz
```

注意：`imp` 目录必须位于 `horde` 目录内，否则 Webmail 将无法工作。一旦完成将 IMP 的 `imp-version` 目录移动到其新名称 `imp` 后，我们将删除 IMP 的 tar 压缩包。

## 步骤 3

出于安全原因，将 `horde` 目录及其所有子目录和文件的所有者更改为超级用户 `root`。

```bash
[root@deep /]# chown -R 0.0 /home/httpd/horde/
```

## 步骤 4

通过执行以下命令，将 `/home/httpd/horde/phplib/*.ihtml` 文件复制到新的 `php` 目录（`/home/httpd/php/`）：

```bash
[root@deep /]# cp /home/httpd/horde/phplib/*.ihtml /home/httpd/php/
```

# 配置并创建 Webmail IMP SQL 数据库

我们现在必须配置数据库，以便能够使用带有 SQL 数据库的 Webmail IMP。更简便的方法是使用位于 `/home/httpd/horde/imp/config/scripts/` 子目录下的预定义脚本。对于 PostgreSQL 支持，请按照以下简单步骤操作。

## 步骤 1

首先，我们必须编辑位于 `/home/httpd/horde/imp/config/scripts` 子目录下与 PostgreSQL 相关的 `pgsql_create.sql` 脚本文件，并将其默认的运行用户名从 `httpd` 更改为 `www`。

编辑 `pgsql_create.sql` 文件（`vi /home/httpd/horde/imp/config/scripts/pgsql_create.sql`）并更改以下行：

```sql
GRANT SELECT, INSERT, UPDATE ON imp_pref, imp_addr TO nobody;
```

更改为：

```sql
GRANT SELECT, INSERT, UPDATE ON imp_pref, imp_addr TO www;
```

## 步骤 2

现在，我们必须在我们 PostgreSQL 数据库中定义名为 `www` 的 Apache 用户名，以便能够使用该用户名创建 Webmail IMP 数据库。

要在数据库中定义名为 `www` 的 `httpd` 用户名，请运行 PostgreSQL 的创建用户工具程序：

```text
[root@deep /]# su postgres

[postgres@deep /]$ create user

Enter name of user to add ---> www

Enter user's postgres ID or RETURN to use unix user ID: 80 -> [按 Enter]

Is user "www" allowed to create databases (y/n) y

Is user "www" a superuser? (y/n) n

create user: www was successfully added
```

# Apache CHAPTER 2 0

可选的 Apache 安装组件

## Step 3

一旦 `httpd` 用户 `www` 被添加到 PostgreSQL 中，请以 PostgreSQL 数据库运行时的用户身份登录（在我们的例子中是 `postgres`），并插入与 PostgreSQL 相关的小脚本，以自动在 PostgreSQL 中创建 Webmail IMP 数据库。

要自动在 PostgreSQL 中创建 Webmail IMP 数据库，请使用以下命令：

```bash
[root@deep /]# cd /home/httpd/horde/imp/config/scripts/

[root@deep scripts]# su postgres

[postgres@deep scripts]$ pgsql template1 < pgsql_create.sql
```

```sql
// IMP database creation script for postgreSQL

// Author: barce@lines.edu

// Date: Aug-29-1998

// Notes: replace "nobody" with yours httpRNG username

// Run using: psql template1 < pgsql_create.sql

CREATE DATABASE horde;

CREATEDB

\connect horde

connecting to new database: horde

CREATE TABLE imp_pref (

    username   text,

    sig        text,

    fullname   text,

    replyto    text,

    lang       varchar(30)

);

CREATE

CREATE TABLE imp_addr (

    username   text,

    address    text,

    nickname   text,

    fullname   text

);

CREATE

GRANT SELECT, INSERT, UPDATE ON imp_pref, imp_addr TO www;

CHANGE

EOF
```

## 步骤 4

我们必须重启 PostgreSQL 服务器以使更改生效：

要重启 PostgreSQL，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/postgresql restart

Stopping postgresql service:             [ OK ]

Checking postgresql installation: looks good!

Starting postgresql service: postmaster [13474]
```

## 步骤 5

复制并将文件 `/home/httpd/horde/phplib/horde_phplib.inc` 重命名为 `/home/httpd/php/local.inc`，然后编辑新的 `local.inc` 文件，这是你的 phplib 配置文件，包含将定义 phplib 行为的设置，并按照其说明定义你想要取消注释的存储容器。

```bash
[root@deep /]# cp /home/httpd/horde/phplib/horde_phplib.inc /home/httpd/php/local.inc

cp: overwrite '/home/httpd/php/local.inc'? y
```

编辑 `local.inc` 文件（`vi /home/httpd/php/local.inc`），然后取消注释并设置以下行，将 SQL 定义为你的默认数据库：

```php
/* To use an SQL database, uncomment and edit the following: */

class HordeDB extends DB_Sql {

  var $Host = 'localhost';

  var $Database = 'horde';

  var $User = 'www';

  var $Password = 'some-password';

  var $Port = '5432';

  function halt($msg) {

    printf("<b>Database error (HordeDB):</b> %s<br>\n", $msg);

  }

}

class HordeCT extends CT_Sql {

  var $database_class = 'HordeDB';      // Which database class to use...

  var $database_table = 'active_sessions'; // and find our data in this table.

}
```

**注意：** 别忘了在此文件中取消注释你想要用于 Webmail IMP 的存储容器类型。记住只能取消注释一种类型。在我们的例子中，我们选择使用 SQL。此外，你必须为 SQL 数据库设置的参数有 `var $User =`、`var $Password =` 和 `var $Port =`。`var $User =` 对应你的 `httpd` 用户名（在我们的例子中是 `www`）；`var $Password =` 对应你在 PostgreSQL 中为用户 `www` 定义的密码；`var $Port =` 是用于连接到你的 SQL 数据库的 IP 端口号。

## 步骤 6

最后编辑 `/home/httpd/php/prepend.php3` 文件，并指定你的默认数据库类型。

编辑 `prepend.php3` 文件（`vi /home/httpd/php/prepend.php3`），然后更改以下行，将 PostgreSQL 定义为你的数据库类型：

```php
require($_PHPLIB["libdir"] . "db_mysql.inc");
```

改为：

```php
require($_PHPLIB["libdir"] . "db_pgsql.inc");
```

# 配置 PHP4 的 `php.ini` 配置文件

你需要配置的另一个设置是在 PHP4 配置文件 `/etc/httpd/php.ini` 中。此调整是为了定义哪些功能（如 IMAP、PostgreSQL 等）将由 PHP4 自动加载。由于我们决定使用 PostgreSQL 作为数据库，并且需要在我们的 Webmail 软件中使用 IMAP 功能，因此我们必须在 PHP4 的 `php.ini` 配置文件中定义它们。

## 步骤 1

编辑 `php.ini` 文件（`vi /etc/httpd/php.ini`），并在 Dynamic Extensions 部分下添加你的选择。在我们的例子中，如你所见，我们选择了 IMAP 和 PostgreSQL 支持：

```ini
extension=imap.so        ; Added for IMAP support

extension=pgsql.so       ; Added for PostgreSql support

extension=mysql.so       ; Added for MySql support

extension=ldap.so        ; Added for LDAP support
```

## 步骤 2

你还必须告诉 `php` 在包含没有绝对路径的文件时去哪里查找，以自动将 phplib 的 `prepend.php3` 内容添加到每个文件中，并关闭 magic quotes。

编辑 `php.ini` 文件（`vi /etc/httpd/php.ini`），并将以下参数添加到相关行：

```ini
magic_quotes_gpc  = Off

auto_prepend_file = "/home/httpd/php/prepend.php3"

include_path      = "/home/httpd/horde:/home/httpd/php"
```

# 配置 Apache 以识别 Webmail IMP

一旦 Webmail IMP 安装到系统中，我们必须在 Apache 的 `httpd.conf` 文件中添加以下行，以便能够定位和使用其功能。

## 步骤 1

编辑 `httpd.conf` 文件（`vi /etc/httpd/conf/httpd.conf`），并在 section 标签 `<IfModule mod_alias.c>` 和 `</IfModule>` 之间添加以下行：

```apache
Alias /horde/ "/home/httpd/horde/"

<Directory "/home/httpd/horde">

  Options None

  AllowOverride None

  Order allow,deny

  Allow from all

</Directory>

Alias /imp/ "/home/httpd/horde/imp/"

<Directory "/home/httpd/horde/imp">

  Options None

  AllowOverride None

  Order allow,deny

  Allow from all

</Directory>
```

## 步骤 2

你必须重启 Apache Web 服务器以使更改生效：

要重启 Apache，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/httpd restart

Shutting down http:                   [ OK ]

Starting httpd:                       [ OK ]
```

# 通过 Web 浏览器配置 Webmail IMP

有多种方法可以配置 Webmail IMP，而我们选择的方式是使用名为 `setup.php3` 的新设置引擎，它使人们能够通过 Web 浏览器配置 IMP。

## 步骤 1

出于安全原因，它默认被禁用，但你可以使用以下命令启用它：

要启用 `setup.php`，请使用以下命令：

```bash
[root@deep /]# cd /home/httpd/horde/

[root@deep horde]# sh ./install.sh
```

你的空白配置文件已创建，请转到配置工具：

```text
your install path url/setup.php3
```

## 步骤 2

一旦 Webmail IMP 的新设置引擎启用后，将你的浏览器指向以下 URL：[`http://my-web-server/horde/setup.php`](http://my-web-server/horde/setup.php)。此时，你可以运行图形化设置程序并配置 IMP 的所有方面。

**注意：** `<my-web-server>` 是你的 Apache Web 服务器所在地址，`/horde/` 目录是 `setup.php` 文件所在位置。

## 步骤 3

完成 Webmail IMP 的新设置引擎后，出于安全原因，请务必再次禁用它。

要禁用 `setup.php`，请使用以下命令：

```bash
[root@deep /]# cd /home/httpd/horde/

[root@deep horde]# sh ./secure.sh
```



我已将你的配置文件和库的权限设置为 `0555`，即所有用户均可读取和执行。

`setup.php` 的权限设置为 `0000`，即完全不可访问。

## Step 4

在这个阶段，我们必须验证 Webmail IMP 是否在你的系统上正常工作。为此，将你的 Web 浏览器指向以下地址：<http://my-web-server/horde/>。

`<my-web-server>` 是你的 Apache Web 服务器所在地址，`<horde>` 是托管 Webmail IMP 程序的目录。

# Chapter 21 服务器软件（文件共享网络服务）

## 本章内容

- Linux Samba 服务器
- 配置
- 为客户端创建加密的 Samba 密码文件
- 保护 Samba
- 优化 Samba
- Samba 管理工具
- Samba 用户工具
- Linux FTP 服务器
- 为每个无 shell 用户设置 FTP 用户账户
- 设置 chroot 用户环境
- 配置
- 配置 `ftpd` 使用 `tcp-wrappers inetd` 超级服务器
- FTP 管理工具
- 保护 FTP

## Linux Samba 服务器

### 概述

企业级组织通常需要处理多种不同的操作系统，并且需要将它们置于网络环境中以实现文件共享和打印机共享。员工可能在 Linux、Microsoft Windows 95/98/NT、OS/2 或 Novell 等工作站上工作，但日常工作中仍需要访问服务器。

Samba 是一种功能强大的网络服务，用于文件和打印共享，适用于当今大多数操作系统。当管理员很好地实现它时，它比 Microsoft Windows 机器上原生提供的文件共享服务更快、更安全。

正如 Samba 的 README 文件所述：

Samba 是许多与 PC 相关的机器用来共享文件、打印机以及其他信息（如可用文件和打印机列表）的协议。原生支持此协议的操作系统包括 Windows、Windows 95/98/NT、OS/2 和 Linux，此外还可以为 DOS、Windows、VMS、各种 Unix、MVS 等系统安装附加包来实现相同的功能。

Apple Mac 和一些 Web 浏览器也可以 speak 此协议。SMB 的替代方案包括 Netware、NFS、AppleTalk、Banyan Vines、Decnet 等；其中许多方案各有优势，但没有一个既是公开规范又广泛默认实现在桌面机器中。

Samba 软件包括一个 SMB 服务器，为 Windows NT 和 LAN Manager 风格的文件和打印服务提供给 SMB 客户端（如 Windows 95、Warp Server、`smbfs` 等）；一个 NetBIOS（`rfc1001/1002`）名称服务器，除其他功能外还提供浏览支持；一个类似 ftp 的 SMB 客户端，使您能够从 Unix、Netware 和其他操作系统访问 PC 资源（磁盘和打印机）；最后还有一个客户端的 tar 扩展，用于备份 PC。

## 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为 `/var/tmp`（其他路径亦可）。
- 安装在 Red Hat Linux 6.1 和 6.2 上进行了测试。
- 安装中的所有步骤都将以超级用户账户 `root` 执行。

## Samba 版本号为 2.0.7

## 软件包

Samba 主页：<http://us1.samba.org/samba/samba.html>

Samba FTP 站点：`63.238.153.11`

您必须确保下载：`samba-2.0.7.tar.gz`

## Tarball

在安装 Samba 之前，最好列出系统上的文件清单，安装后再列一份，然后使用 `diff` 比较它们，找出软件将文件放置到了何处。只需在安装前运行 `find /* > Samba1`，安装后运行 `find /* > Samba2`，然后使用 `diff Samba1 Samba2 > Samba-Installed` 即可获得更改内容的列表。

## 编译

解压 tarball（`tar.gz`）。

```bash
[root@deep /]# cp samba-version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf samba-version.tar.gz
```

## 配置

进入新的 Samba 目录，然后进入其 `source` 子目录。

### 步骤 1

编辑 `smbsh.in` 文件（`vi +3 smbwrapper/smbsh.in`）并修改以下行：

```text
SMBW_LIBDIR=${SMBW_LIBDIR-@builddir@/smbwrapper}
```

改为：

```text
SMBW_LIBDIR=${SMBW_LIBDIR-/usr/bin}
```

此更改将把 Samba 的 `lib` 目录重新定位到 `/usr/bin` 目录下。

### 步骤 2

编辑 `Makefile.in` 文件（`vi +28 Makefile.in`）并修改以下行：

```makefile
SBINDIR = @bindir@
```

改为：

```makefile
SBINDIR = @sbindir@
```

```makefile
VARDIR = @localstadir@
```

改为：

```makefile
VARDIR = /var/log/samba
```

这将指定 Samba 二进制文件的 `sbin` 目录将位于 `/usr/sbin` 目录中，而 Samba 日志文件的 `/var` 目录将位于 `/var/log/samba` 子目录下。

### 步骤 3

编辑 `convert_smbpasswd` 文件（`vi +10 script/convert_smbpasswd`）并修改以下行：

```awk
nawk 'BEGIN {FS=":"}
```

改为：

```awk
gawk 'BEGIN {FS=":"}
```

这将指定使用 GNU Linux 版本的 awk 文本处理工具，而非 Bell Labs 研究版本的 awk 程序来处理 `smbpasswd` 文件。

### 步骤 4

编辑 `smbmount.c` 文件（`vi +98 client/smbmount.c`）并修改以下行：

```c
static void close_our_files(int client_fd)
{
    int i;

    for (i = 0; i < 256; i++) {
        if (i == client_fd) continue;
        close(i);
    }
```

改为：

```c
static void close_our_files(int client_fd)
{
    struct rlimit limits;
    int i;

    getrlimit(RLIMIT_NOFILE,&limits);

    for (i = 0; i < limits.rlim_max; i++) {
        if (i == client_fd) continue;
        close(i);
    }
```

此步骤将使 `smbmount.c` 文件与 Red Hat 的 glibc 2.1 库兼容。

## 编译和优化

### 步骤 1

在终端上输入以下命令：

```bash
CC="egcs" \
./configure \
--prefix=/usr \
--libdir=/etc \
--with-lockdir=/var/lock/samba \
--with-privatedir=/etc \
--with-swatdir=/usr/share/swat \
--with-pam \
--with-mmap \
--without-sambabook
```

**注意：** 选项 `--with-mmap` 在某些机器上可以大幅提升性能，而在另一些机器上则完全没有区别，在某些机器上甚至可能降低性能。

这告诉 Samba 根据此特定硬件设置进行配置：

- 包含 PAM 密码数据库支持以提高安全性。
- 包含实验性 MMAP 支持以提升 Samba 性能。
- 不安装 Samba 发行版附带的书籍帮助。

### 步骤 2

现在，Liberia 必须在 Linux 服务器上安装 Samba：

```bash
[root@deep source]# make all
[root@deep source]# make install
[root@deep source]# install -m 755 script/mksmbpasswd.sh /usr/bin/
[root@deep source]# rm -rf /usr/share/swat/（如果像我一样，不喜欢用 HTML 配置 Samba）。
[root@deep source]# rm -f /usr/sbin/swat
[root@deep source]# rm -f /usr/man/man8/swat.8
[root@deep source]# mkdir -p /var/lock/samba
[root@deep source]# mkdir -p /var/spool/samba（仅当您打算使用打印机共享时才需要）。
[root@deep source]# chmod 1777 /var/spool/samba/（仅当您打算使用打印机共享时才需要）。
```

`install` 命令将安装脚本 `mksmbpasswd.sh` 到 `/usr/bin/` 目录下。此脚本用于设置允许通过 `smbpasswd` 文件连接到我们服务器的 Samba 用户。请参阅本文档后面的部分了解如何设置和使用 Samba 密码。

`rm` 命令将删除 `/usr/share/swat` 目录及其下的所有文件，还将删除 `/usr/sbin/` 下的 `swat` 二进制程序。SWAT 程序是一个基于 Web 的配置工具，允许您通过 Web 浏览器界面配置 Samba 的 `smb.conf` 文件。当然，要使用 SWAT 工具，您需要运行一个 Web 服务器，例如 Apache。SWAT 工具可能在您的服务器上打开安全漏洞，因此我建议您删除它且不要使用。

`mkdir` 命令将在您的系统上创建 `/var/spool/samba/` 目录，用于所有打印共享作业。当然，只有当您打算通过局域网使用 Samba 打印共享时，此目录才是必需的。由于我们尚未将 Samba 服务器配置为使用打印共享，因此我们不需要在服务器上创建此目录（`/var/spool/samba/`），也不需要使用 `chmod` 命令更改 `/var/spool/samba` 中的 `sticky` 位，以便只有文件所有者才能删除该目录中的给定文件。

## 工作后的清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf samba-version/ samba-version.tar.gz
```

`rm` 命令将删除我们用于编译和安装 Samba 的所有源文件。它还将从 `/var/tmp` 目录中删除 Samba 压缩归档。

## 配置

不同服务的配置文件非常具体，取决于您的需求和网络架构。有人可能安装 Samba 服务器后只有一个客户端连接，而另一个人可能安装后有 1000 个连接。

本书中描述的所有软件在名为 `floppy.tgz` 的 tar 压缩归档中都有特定的目录和子目录，其中包含特定程序的配置文件。如果您获取此归档文件，就不必将下面不同的配置文件手动复制或剪切粘贴来创建您的配置文件。无论您决定手动复制它们，还是从归档中获取为您方便制作的文件，您都有责任根据您的需求进行修改、调整，并将与 Samba 软件相关的文件放置在服务器上的适当位置，如下所示。服务器配置文件归档的下载地址位于以下互联网地址：<http://www.openna.com/books/floppy.tgz>

- 要运行 Samba 服务器，以下文件是必需的，必须创建或复制到服务器上的适当目录中。
- 将 `smb.conf` 和 `lmhosts` 文件复制到 `/etc/` 目录中。
- 将 `smb` 脚本文件复制到 `/etc/rc.d/init.d/` 目录中。
- 将 `samba` 文件复制到 `/etc/logrotate.d/` 目录中。
- 将 `samba` 文件复制到 `/etc/pam.d/` 目录中。

你可以在 `floppy.tgz` 归档文件中找到以下列出的配置文件。从解压后的 `floppy.tgz` 归档中将以下文件复制到相应的位置，或者直接从本书中复制并粘贴到相关文件中。

## `/etc/smb.conf` 文件的配置

`/etc/smb.conf` 文件是 Samba 服务器的主配置文件，在其中你可以指定希望从 Windows 机器访问的目录、授权的 IP 地址等。文件中 `[global]` 行下面的前几行包含全局配置指令，这些指令对所有共享都有效（除非在每个共享的基础上被覆盖），后面跟着共享部分。存在很多选项，阅读 Samba 附带的文档以了解每种不同设置和参数的更多信息是很重要的。

以下配置示例是带有加密密码支持的 Samba 的最小可用配置文件。另外，需要注意的是，我们在此 Samba 配置中只注释与安全和优化相关的参数，其余留给您自行研究。

在我们的示例中，我们只创建了一个目录 `[tmp]`，并且只允许 C 类机器 IP 地址范围连接到 Samba 服务器。此外，我们在此服务器上不使用 Samba 和 Windows 之间的打印共享功能。

编辑 `smb.conf` 文件（`vi /etc/smb.conf`）并添加/修改以下参数：

```ini
[global]
    workgroup = OPENNA
    server string = R&D of Open Network Architecture Samba Server
    encrypt passwords = True
    security = user
    smb passwd file = /etc/smbpasswd
    log file = /var/log/samba/log.%m
    socket options = IPTOS_LOWDELAY TCP_NODELAY
    domain master = Yes
    local master = Yes
    preferred master = Yes
    os level = 65
    dns proxy = No
    name resolve order = lmhosts host bcast
    bind interfaces only = True
    interfaces = eth0 192.168.1.1
    hosts deny = ALL
    hosts allow = 192.168.1.4 127.0.0.1
    debug level = 1
    create mask = 0644
    directory mask = 0755
    level2 oplocks = True
    read raw = no
    write cache size = 262144

[homes]
    comment = Home Directories
    browseable = no
    read only = no
    invalid users = root bin daemon nobody named sys tty disk mem kmem users

[tmp]
    comment = Temporary File Space
    path = /tmp
    read only = No
    valid users = admin
    invalid users = root bin daemon nobody named sys tty disk mem kmem users
```

这告诉 `smb.conf` 文件为以下特定配置设置进行配置：

```ini
[global]
```



```ini
workgroup = OPENNA
```

`"workgroup"` 选项指定当客户端查询时，您的服务器将显示在哪个工作组中。在客户端和服务器上保持相同的工作组名称很重要。

```ini
server string = R&D of Open Network Architecture Samba Server
```

`"server string"` 选项指定您希望在 Windows 机器的打印机管理器中的打印机注释框中，或在`"net view"`命令中的 IPC 连接中显示给用户的字符串。

```ini
encrypt passwords = True
```

如果`"encrypt passwords"`选项设置为`"True"`，则指示 Samba 在与客户端协商时使用加密密码而不是明文密码。当密码加密时，嗅探程序将无法检测到您的密码。出于安全原因，此选项必须始终设置为`"True"`。

```ini
security = user
```

`"security"`选项如果设置为`"user"`，则指定客户端必须首先使用有效的用户名和密码“登录”，否则连接将被拒绝。这意味着客户端的有效用户名和密码必须存在于 Linux 服务器的`"/etc/passwd"`文件和 Samba 服务器的`"/etc/smbpasswd"`文件中，否则来自客户端的连接将失败。有关`"smbpasswd"`文件的更多信息，请参阅本章中的`"Securing samba"`。

```ini
smb passwd file = /etc/smbpasswd
```

`"smb passwd file"`选项指定加密的`"smbpasswd"`文件的路径。`"smbpasswd"`文件是 Linux 系统`"/etc/passwd"`文件的副本，包含允许连接到 Samba 服务器的客户端的有效用户名和密码。当请求连接时，Samba 软件会读取此文件（`smbpasswd`）。

```ini
log file = /var/log/samba/log.%m
```

`"log file"`选项指定 Samba 日志文件的位置和名称。通过使用`"%m"`名称扩展，您可以为登录到 Samba 服务器的每个用户或机器拥有单独的日志文件（例如`log.machine1`）。

```ini
socket options = IPTOS_LOWDELAY TCP_NODELAY
```

`"socket options"`选项指定您可以在 Samba 配置中包含的调优参数，以优化和提高 Samba 服务器的性能。默认情况下，我们选择为本地网络调优连接，并提高 Samba 服务器传输文件的性能。

```ini
domain master = Yes
```

`"domain master"`选项指定将`"nmbd"`（Samba 服务器守护进程）设置为其给定工作组的域主浏览器。此选项通常必须仅在同一网络和工作组中的所有其他 Samba 服务器上的一台 Samba 服务器上设置为`"Yes"`。

```ini
local master = Yes
```

`"local master"`选项允许`"nmbd"`（Samba 服务器守护进程）尝试成为子网上的本地主浏览器。与上面类似，通常此选项必须仅在一台作为子网上本地主服务器的 Samba 服务器上设置为`"Yes"`，以适用于网络上的所有其他 Samba 服务器。

```ini
preferred master = Yes
```

`"preferred master"`选项指定并控制`"nmbd"`（Samba 服务器守护进程）是否为其工作组的首选主浏览器。同样，这通常必须在一台服务器上设置为`"Yes"`，以适用于网络上所有其他服务器。

```ini
os level = 65
```

`"os level"`选项通过其值指定`"nmbd"`（Samba 服务器守护进程）是否有机会成为本地广播区域中工作组的本地主浏览器。数字 65 将胜过任何 NT 服务器。如果您的网络上有 NT 服务器，并且希望将 Linux Samba 服务器设置为本地广播区域中工作组的本地主浏览器，则必须将`"os level"`选项设置为 65。此外，此选项必须仅在一台 Linux Samba 服务器上设置，并且必须在您网络上可能拥有的所有其他 Linux Samba 服务器上禁用。

```ini
dns proxy = No
```

如果`"dns proxy"`选项设置为`"Yes"`，则指定`"nmbd"`（Samba 服务器守护进程）在充当 WINS 服务器并发现 Net BIOS 名称尚未注册时，应将 Net BIOS 名称逐字视为 DNS 名称，并代表查询名称的客户端向 DNS 服务器进行查找。由于我们尚未将 Samba 服务器配置为充当 WINS 服务器，因此我们不需要将此选项设置为`"Yes"`。此外，将此选项设置为`"Yes"`将降低您的 Samba 性能。

```ini
name resolve order = lmhosts host bcast
```

`"name resolve order"`选项指定使用哪些命名服务来解析主机名到 IP 地址，以及按什么顺序解析。我们选择的参数导致首先检查 Samba 的本地`"lmhosts"`文件，然后检查其余部分。

```ini
bind interfaces only = True
```

如果`"bind interfaces only"`选项设置为`"True"`，则允许您限制哪些接口将服务于`"smb"`请求。这是一个安全功能。下面的配置选项`"interfaces = eth0 192.168.1.1"`完善了这个选项。

```ini
interfaces = eth0 192.168.1.1
```

`"interfaces"`选项允许您覆盖 Samba 将用于浏览、名称注册和其他 NBT 流量的默认网络接口列表。默认情况下，Samba 将查询内核以获取所有活动接口的列表，并使用任何支持广播的接口（`127.0.0.1`除外）。使用此选项，Samba 将只监听 IP 地址为`192.168.1.1`的`"eth0"`接口。这是一个安全功能，并完善了上面的配置选项`"bind interfaces only = True"`。

```ini
hosts deny = ALL
```

`"hosts deny"`选项指定不允许访问 Samba 服务的主机列表，除非特定服务有自己的列表来覆盖此列表。为简单起见，我们默认拒绝所有主机的访问，并在下面的`"hosts allow ="`选项中允许特定主机。

```ini
hosts allow = 192.168.1.4 127.0.0.1
```

选项`"hosts allow"`指定了哪些主机被允许访问 Samba 服务。默认情况下，我们允许来自 IP 地址段 C 类`192.168.1.4`的主机以及本机 localhost `127.0.0.1`来访问 Samba 服务器。注意，必须始终设置 localhost，否则你会收到一些错误消息。

```ini
debug level = 1
```

选项`"debug level"`允许在`"smb.conf"`文件中指定日志级别。如果你将调试级别设置为高于 2，那么可能会导致性能大幅下降。这是因为服务器在每次操作后都会刷新日志文件，这可能会非常耗时。

```ini
create mask = 0644
```

选项`"create mask"`根据从 DOS 模式到 UNIX 权限的映射来指定和设置必要的权限。将此选项设置为 0644 后，从 Windows 系统复制或创建到 Unix 系统的所有文件默认都将具有 0644 的权限。

```ini
directory mask = 0755
```

选项`"directory mask"`用于指定和设置八进制模式，这些模式在从 DOS 模式转换为 UNIX 模式以创建 UNIX 目录时使用。将此选项设置为 0755 后，从 Windows 系统复制或创建到 Unix 系统的所有目录默认都将具有 0755 的权限。

```ini
level2 oplocks = True
```

选项`"level2 oplocks"`如果设置为`"True"`，将会提高对许多不常写入的文件（例如`.EXE`应用程序文件）进行访问时的性能。

```ini
read raw = no
```

选项`"read raw"`控制服务器在向客户端传输数据时是否支持原始读取 SMB 请求。注意，`"read raw"`操作不使用内存映射。因此，如果你通过使用`"read raw = no"`（就像我们这样做）来禁用`"read raw"`，你可能会发现内存映射更加有效。

```ini
write cache size = 262144
```

选项`"write cache size"`允许 Samba 在磁盘子系统是瓶颈的系统上提高性能。此选项的值以字节为单位指定，大小为 262,144 代表每个文件的缓存大小为 256k。

```ini
[tmp]
comment = Temporary File Space
path = /tmp
read only = No
valid users = admin
invalid users = root bin daemon nobody named sys tty disk mem kmem users
```

选项`"comment"`允许你指定一条注释，当客户端向服务器查询时，该注释将会显示在共享旁边。

选项`"read only"`指定是否应该只允许用户读取文件。在我们的示例中，由于这是针对 Linux 服务器`"tmp"`目录的配置，用户可以做的不仅仅是读取文件。

选项`"valid users"`指定了应该被允许登录到此服务的用户列表。在我们的示例中，只有用户`"admin"`被允许访问该服务。

选项`"invalid users"`指定了不应该被允许登录到此服务的用户列表。这实际上是一种“偏执”检查，以确保绝对不会因配置不当而破坏你的安全性。建议你包含所有在服务器上运行守护进程的默认用户。

## `"/etc/lmhosts"`文件的配置

配置你的`"/etc/lmhosts"`文件。`"lmhosts"`文件是 Samba Net BIOS 名称到 IP 地址的映射文件。它与`"/etc/hosts"`文件格式非常相似，但主机名部分必须对应于 Net BIOS 命名格式。

创建`lmhosts`文件（`touch /etc/lmhosts`）并添加你的客户端主机：

```text
# Sample Samba lmhosts file.

#

127.0.0.1    localhost

192.168.1.1  deep

192.168.1.4  win
```

在我们的示例中，此文件包含三个 IP 到 Net BIOS 名称的映射：localhost (`127.0.0.1`)、名为 deep 的客户端 (`192.168.1.1`) 和名为 win 的客户端 (`192.168.1.4`)。

## `"/etc/pam.d/samba"`文件的配置

配置你的`"/etc/pam.d/samba"`文件以使用 pam 认证。

创建`samba`文件（`touch /etc/pam.d/samba`）并添加以下行：

```text
Auth          required    /lib/security/pam_pwdb.so nullok shadow

Account       required    /lib/security/pam_pwdb.so
```

## `"/etc/logrotate.d/samba"`文件的配置

配置你的`"/etc/logrotate.d/samba"`文件以每周自动轮转你的日志文件。

创建`samba`文件（`touch /etc/logrotate.d/samba`）并添加以下行：

```text
/var/log/samba/log.nmb {
    notifempty
    missingok
    postrotate
      /usr/bin/killall -HUP nmbd
    endrotate
}

/var/log/samba/log.smb {
    notifempty
    missingok
    postrotate
      /usr/bin/killall -HUP smbd
    endrotate
}
```

## 为你的客户端创建加密的 Samba 密码文件

`"/etc/smbpasswd"`文件是 Samba 加密密码文件。它包含用户名、Unix UID 和 SMB 哈希密码，这些是允许访问你的 Samba 服务器的用户，以及账户标志信息和密码上次更改的时间。在客户端尝试连接到你的 Samba 服务器之前，创建此密码文件并包含所有允许的用户非常重要。如果没有这一步，将没有人能够连接到你的 Samba 服务器。

### 步骤 1

要创建 Samba 账户，你必须首先拥有有效的 Linux 账户，因此在生成 Samba 的`"smbpasswd"`文件之前，先在`"etc/passwd"`文件中创建所有你希望连接到 Samba 服务器的用户。

- 要将新用户添加到你的`"/etc/passwd"`文件，请使用以下命令：

  ```shell
  [root@deep /]# useradd smbclient
  ```

- 要为`"/etc/passwd"`文件中的用户添加密码，请使用以下命令：

  ```text
  [root@deep /]# passwd smbclient
  Changing password for user smbclient
  New UNIX password:
  Retype new UNIX password:
  passwd: all authentication tokens updated successfully
  ```

### 步骤 2

一旦我们在 Linux 服务器的`"/etc/passwd"`文件中添加了所有 Samba 客户端，我们现在可以从`"/etc/passwd"`文件生成`"smbpasswd"`文件。

- 要从`"/etc/passwd"`文件生成`"smbpasswd"`文件，请使用以下命令：

  ```shell
  [root@deep /]# cat /etc/passwd | mksmbpasswd.sh > /etc/smbpasswd
  ```

### 步骤 3

最后，我们必须执行的最后一个步骤是在能够使用之前，在我们的`"/etc/smbpasswd"`文件中创建 Samba 用户账户。

- 要创建 Samba 用户账户，请使用以下命令：

  ```text
  [root@deep /]# smbpasswd -a smbclient
  ```

  （记住`"smbclient"`必须是一个有效的 Linux 账户。）

  ```text
  New SMB password:
  Retype new SMB password:
  Added user smbclient.
  Password changed for user smbclient.
  ```

### 步骤 4

不要忘记将你的新`"smbpasswd"`文件的权限更改仅为超级用户`"root"`可读可写，而组用户和其他用户没有任何权限（`0600/-rw-------`）。这是一项安全措施。

```shell
[root@deep /]# chmod 600 /etc/smbpasswd
[root@deep /]# testparm
```

（这将验证`smb.conf`文件是否存在错误。）

> **注意：** 有关更多信息，请参阅`samba/doc/texts/`中的`ENCRYPTION.txt`。

## `"/etc/rc.d/init.d/smb"`脚本文件的配置

配置你的`"/etc/rc.d/init.d/smb"`脚本文件以自动启动和停止 Samba `smbd`和`nmbd`守护进程服务器。

创建`smb`脚本文件（`touch /etc/rc.d/init.d/smb`）并添加以下行：

```shell
#!/bin/sh
```

## 服务器软件（文件共享网络服务）

```shell
#
# chkconfig: - 91 35
# description: Starts and stops the Samba smbd and nmbd daemons \\
#       used to provide SMB network services.

# Source function library.
. /etc/rc.d/init.d/functions

# Source networking configuration.
. /etc/sysconfig/network

# Check that networking is up.
[ ${NETWORKING} = "no" ] && exit 0

# Check that smb.conf exists.
[ -f /etc/smb.conf ] || exit 0

RETVAL=0

# See how we were called.
case "$1" in
  start)
    echo -n "Starting SMB services: "
    daemon smbd -D
    RETVAL=$?
    echo

    echo -n "Starting NMB services: "
    daemon nmbd -D
    RETVAL2=$?
    echo

    [ $RETVAL -eq 0 -a $RETVAL2 -eq 0 ] && touch /var/lock/subsys/smb || \
      RETVAL=1
    ;;

  stop)
    echo -n "Shutting down SMB services: "
    killproc smbd
    RETVAL=$?
    echo

    echo -n "Shutting down NMB services: "
    killproc nmbd
    RETVAL2=$?

    [ $RETVAL -eq 0 -a $RETVAL2 -eq 0 ] && rm -f /var/lock/subsys/smb
    echo ""
    ;;

  restart)
    $0 stop
    $0 start
    RETVAL=$?
    ;;

  reload)
    echo -n "Reloading smb.conf file: "
    killproc -HUP smbd
```



```bash
RETVAL=$?

echo

;;

status)

status smbd

status nmbd

RETVAL=$?

;;

*)

echo "Usage: $0 {start|stop|restart|status}"
```

现在，将此脚本设置为可执行并更改其默认权限：

```bash
[root@deep /]# chmod 700 /etc/rc.d/init.d/smb
```

使用以下命令为 Samba 创建符号链接 `rc.d`：

```bash
[root@deep /]# chkconfig --add smb
```

Samba 脚本不会在服务器重启时自动启动 `smbd` 和 `nmbd` 守护进程。你可以通过执行以下命令来更改此默认设置：

```bash
[root@deep /]# chkconfig --level 345 smb on
```

使用以下命令手动启动你的 Samba 服务器：

```text
[root@deep /]# /etc/rc.d/init.d/smb start

Starting SMB services:           [ OK ]

Starting NMB services:           [ OK ]
```

## 保护 Samba

### 保护重要配置文件

不可变位（immutable bit）可用于防止意外删除或覆盖必须受保护的文件。它还可以防止有人创建指向该文件的符号链接。一旦你的 `smb.conf` 和 `lmhosts` 文件配置完成，最好使用如下命令对它们进行保护：

```bash
[root@deep /]# chattr +i /etc/smb.conf

[root@deep /]# chattr +i /etc/lmhosts
```

## 优化 Samba

### 在配置文件中设置 Samba 的 `wide links=` 参数

在 Samba 配置文件 `/etc/smb.conf` 中将 `wide links` 参数设置为 `no` 是一个很大的错误。如果将此选项设置为 `no`，则告诉 Samba 不要跟随指定为共享点区域之外的符号链接。为了确定链接是否指向共享区域之外，Samba 必须跟随该链接，然后执行目录路径查找以确定链接最终指向文件系统的哪个位置。这样每个文件名查找就会增加总共六个额外的系统调用，而 Samba 会频繁地查找文件名。一项已发布的测试表明，设置此参数将导致 Samba 性能下降 25% 到 30%。

### 调整缓冲区缓存

修改文件系统缓存调优参数可以显著提高 Linux 的文件服务性能——最高可达两倍。Linux 会尝试将未被用于其他目的的内存用于文件系统缓存。一个名为 `bdflush` 的特殊守护进程会定期将“脏轮换”（dirty buffers，即包含已修改的文件系统数据或元数据的缓冲区）刷新到磁盘。

实现良好性能的关键是尽可能长时间地将尽可能多的数据保留在内存中。写入磁盘是任何文件系统中最慢的部分。如果你知道文件系统将被大量使用，那么可以为此调优 Linux Samba 的这一过程。与许多内核可调选项一样，这可以通过写入 `/proc` 文件系统中的特殊文件来即时完成。诀窍是，你必须告诉 Linux 你想让它这样做。对于 Linux 2.2 内核，你可以通过执行以下命令来实现。

Red Hat Linux 下 `bdflush` 参数的默认设置为：

`40 500 64 256 500 3000 500 1884 2`

- 要更改 `bdflush` 的值，请在终端上输入以下命令：

#### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# echo "80 500 64 64 15 6000 6000 1884 2" >/proc/sys/vm/bdflush
```

你可以将上述命令添加到 `/etc/rc.d/rc.local` 脚本文件中，这样下次重启系统时就无需再次输入。

#### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```conf
# Improve file system performance

vm.bdflush = 80 500 64 64 15 6000 6000 1884 2
```

你必须重新启动网络才能使更改生效。重新启动网络的命令如下：

- 要在你的系统上手动重新启动所有网络设备，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters                    [ OK ]

Bringing up interface lo                      [ OK ]

Bringing up interface eth0                    [ OK ]

Bringing up interface eth1                    [ OK ]
```

这行命令告诉 `bdflush`，在文件系统缓冲区缓存达到 80% 满（80）之前，不必担心将脏码块写入磁盘。其他值用于调整一次磁盘操作中要写入的缓冲区数量（500）、允许脏码在内核中留存的时间（`60*HZ`）等。你可以在 2.2 内核文档文件 `linux/Documentation/sysctl/vm.txt` 中找到完整的详细信息，也可以查看第 4 章“常规系统优化”以获取更多信息。

### 调整 `buffermem`

另一个有用的调优提示是告诉 Linux：将至少 60% 的内存用于缓冲区缓存；仅当用于缓冲区缓存的内存百分比超过 10% 时才进行修剪（此参数现已不再使用）；并允许缓冲区缓存增长到所有内存的 60%（此参数也不再使用）。

Red Hat Linux 下 `buffermem` 参数的默认设置为：

`2 10 60`

- 要更改 `buffermem` 的值，请在终端上输入以下命令：

#### 在 Red Hat Linux 6.1 下

```bash
[root@deep /]# echo "60 10 60" >/proc/sys/vm/buffermem
```

你可以将上述命令放入 `/etc/rc.d/rc.local` 脚本文件中，避免系统下次重启时再次输入。你可以在 2.2 内核文档文件 `linux/Documentation/sysctl/vm.txt` 中找到完整的详细信息，也可以查看第 4 章“常规系统优化”以获取更多信息。

#### 在 Red Hat Linux 6.2 下

编辑 `/etc/sysctl.conf` 文件并添加以下行：

```conf
# Improve virtual memory performance

vm.buffermem = 60 10 60
```

你必须重新启动网络才能使更改生效。重新启动网络的命令如下：

- 要在你的系统上手动重新启动所有网络设备，请使用以下命令：

```bash
[root@deep /]# /etc/rc.d/init.d/network restart

Setting network parameters                          [ OK ]

Bringing up interface lo                            [ OK ]

Bringing up interface eth0                          [ OK ]

Bringing up interface eth1                          [ OK ]
```

请注意，最后两个参数（`10` 和 `60`）未被系统使用，因此我们不需要更改默认值。

## 更多文档

欲了解更多详情，你可以阅读以下几个 man 页面：

| 命令 | 说明 |
|---|---|
| `$ man Samba (7)` | - 适用于 UNIX 的 Windows SMB/CIFS 文件服务器 |
| `$ man smb.conf (5)` | - Samba 套件的配置文件 |
| `$ man smbclient (1)` | - 用于访问服务器上 SMB/CIFS 资源的类 ftp 客户端 |
| `$ man smbd (8)` | - 向客户端提供 SMB/CIFS 服务的服务器 |
| `$ man smbmmt (8)` | - 挂载 smb 文件系统 |
| `$ man smbmount (8)` | - 挂载 smb 文件系统 |
| `$ man smbpasswd (5)` | - Samba 加密密码文件 |
| `$ man smbpasswd (8)` | - 更改用户的 SMB 密码 |
| `$ man smbrun (1)` | - `smbd` 与外部程序之间的接口程序 |
| `$ man smbsh (1)` | - 使用 UNIX 命令访问 Windows NT 文件系统 |
| `$ man smbstatus (1)` | - 报告当前 Samba 连接 |
| `$ man smbtar (1)` | - 用于将 SMB 共享直接备份到 UNIX 磁带驱动器的 shell 脚本 |
| `$ man smbumount (8)` | - 供普通用户使用的卸载命令 |
| `$ man testparm (1)` | - 检查 `smb.conf` 配置文件的内部正确性 |
| `$ man testprns (1)` | - 检查打印机名称的有效性 |
|  | - 检查打印机名称对 `smbd` 的有效性 |

## Samba 管理员工具

下面列出的命令是我们经常使用的，但还有更多命令存在。请查阅 man 页面和文档以获取更多详细信息和信息。

### `smbstatus`

`smbstatus` 工具是一个非常简单的程序，用于列出当前的 Samba 连接。

- 要报告当前的 Samba 连接，请使用以下命令：

```text
[root@deep /]# smbstatus

Samba version 2.0.7

Service    uid        gid        pid    machine

-----------------------------------------------

tmp        webmaster  webmaster  3995   gate    (192.168.1.3) Sat Sep 25 19:40:54 1999

No locked files

Share mode memory usage (bytes):

    1048464(99%) free + 56(0%) used + 56(0%) overhead = 1048576(100%) total
```

# Samba 用户工具

下面列出的命令是我们经常使用的，但实际上还有更多。详细信息请参阅 man 手册和相关文档。

## `smbclient`

`smbclient` 是 Samba 的一个程序工具，其工作方式与 FTP 程序的界面非常相似。这个小工具允许你从服务器获取文件到本地机器，将文件从本地机器上传到服务器，从服务器检索目录信息，等等。

- 要使用 `smbclient` 工具连接到 Windows 机器，请使用以下命令：

```text
[root@deep /]# smbclient //sbmserver/sharename -U smbclient

[root@deep /]# smbclient //gate/tmp -U smbclient

Password:

Domain=[OPENNA] OS=[Windows NT 4.0] Server=[NT LAN Manager 4.0]

smb: \\> ls

.                           D        0  Tue Mar 14 15:31:50 2000

..                          D        0  Tue Mar 14 15:31:50 2000

PostgreSQL                  D        0  Tue Mar 14 15 muddy 15:32:22 2000

Squid                       D        0  Tue Mar 14 15:32:28 2000

Imap                        D        0  Tue Mar 14 15:32:38 2000

E_comm                      D        0  Tue Mar 14 15:32:42 2000

StackGuard.pdf              A    61440  Tue Dec 21 20:41:34 1999

installation-without-XFree86 A      448  Tue Dec 21 20:41:28 1999

lcap-0_0_3-2_src.rpm        A    13481  Thu Jan 13 01:50:12 2000

mirc561t.exe                A   948224  Tue Dec 21 20:41:54 1999

65510 blocks of size 32768. 5295 blocks available

smb: \\>
```



其中`//sbmserver`是你要连接的服务器名称，`/sharename`是该服务器上你要连接的目录，`smbclient`是你在该机器上的用户名。

## 已安装文件

- `/etc/rc.d/init.d/smb`
- `/etc/rc.d/rc0.d/K35smb`
- `/etc/rc.d/rc1.d/K35smb`
- `/etc/rc.d/rc2.d/K35smb`
- `/etc/rc.d/rc3.d/S91smb`
- `/etc/rc.d/rc4.d/S91smb`
- `/etc/rc.d/rc5.d/S91smb`
- `/etc/rc.d/rc6.d/K35smb`
- `/etc/pam.d/samba`
- `/etc/logrotate.d/samba`
- `/etc/codepages`
- `/etc/codepages/codepage.437`
- `/etc/codepages/unicode_map.437`
- `/etc/codepages/codepage.737`
- `/etc/codepages/unicode_map.737`
- `/etc/codepages/codepage.775`
- `/etc/codepages/codepage.850`
- `/etc/codepages/unicode_map.850`
- `/etc/codepages/codepage.852`
- `/etc/codepages/unicode_map.852`
- `/etc/codepages/codepage.861`
- `/etc/codepages/unicode_map.861`
- `/etc/codepages/codepage.932`
- `/etc/codepages/unicode_map.932`
- `/etc/codepages/codepage.866`
- `/etc/codepages/unicode_map.866`
- `/etc/codepages/codepage.949`
- `/etc/codepages/unicode_map.949`
- `/etc/codepages/codepage.950`
- `/etc/codepages/unicode_map.950`
- `/etc/codepages/codepage.936`
- `/etc/codepages/unicode_map.936`
- `/etc/codepages/codepage.1251`
- `/etc/codepages/unicode_map.ISO8859-1`
- `/etc/codepages/unicode_map.ISO8859-2`
- `/etc/codepages/unicode_map.ISO8859-5`
- `/etc/codepages/unicode_map.ISO8859-7`
- `/etc/codepages/unicode_map.KOI8-R`
- `/etc/lmhosts`
- `/etc/smb.conf`
- `/etc/smbpasswd`
- `/etc/gshadow-`
- `/usr/bin/smbclient`
- `/usr/bin/smbspool`
- `/usr/bin/testparm`
- `/usr/bin/testprns`
- `/usr/bin/smbstatus`
- `/usr/bin/rpcclient`
- `/usr/bin/smbpasswd`
- `/usr/bin/make_smbcodepage`
- `/usr/bin/make_unicodemap`
- `/usr/bin/nmblookup`
- `/usr/bin/make_printerdef`
- `/usr/bin/smbtar`
- `/usr/bin/addtosmbpass`
- `/usr/bin/convert_smbpasswd`
- `/usr/bin/mksmbpasswd.sh`
- `/usr/man/man1/make_smbcodepage.1`
- `/usr/man/man1/make_unicodemap.1`
- `/usr/man/man1/nmblookup.1`
- `/usr/man/man1/smbclient.1`
- `/usr/man/man1/smbrun.1`
- `/usr/man/man1/smbsh.1`
- `/usr/man/man1/smbstatus.1`
- `/usr/man/man1/smbtar.1`
- `/usr/man/man1/testparm.1`
- `/usr/man/man1/testprns.1`
- `/usr/man/man5/lmhosts.5`
- `/usr/man/man5/smb.conf.5`
- `/usr/man/man5/smbpasswd.5`
- `/usr/man/man7/samba.7`
- `/usr/man/man8/nmbd.8`
- `/usr/man/man8/smbd.8`
- `/usr/man/man8/smbmnt.8`
- `/usr/man/man8/smbmount.8`
- `/usr/man/man8/smbpasswd.8`
- `/usr/man/man8/smbpool.8`
- `/usr/man/man8/smbumount.8`
- `/usr/sbin/smbd`
- `/usr/sbin/nmbd`
- `/var/log/samba`
- `/var/lock/samba`

# Linux FTP 服务器

## 概述

尽管年代久远，使用文件传输协议（FTP）仍然是跨网络在机器之间传输文件的最流行方式之一。客户端和服务器程序已经为市场上的每种主流平台编写，从而使 FTP 成为执行文件传输的最便捷方式。

配置 FTP 服务器有多种不同的方式。一种是作为仅面向私人用户的站点，这是 FTP 服务器的默认配置；私人 FTP 服务器只允许 Linux 系统上的用户通过 FTP 连接并访问他们的文件。

还存在其他类型，比如匿名 FTP 服务器。匿名 FTP 服务器允许网络上的任何人连接并进行文件传输，而无需拥有账户。由于这种设置存在潜在的安全风险，应采取措施仅允许访问系统上的某些目录。

我们这里将介绍的配置是一种允许 FTP 访问 Unix 文件系统半安全区域（chroot 隔离的访客 FTP 访问）的 FTP 服务器。这种配置允许用户访问 FTP 服务器目录，同时阻止他们进入更高级别的目录。这是 FTP 服务器最安全的配置。

![](img/a3204f208d115df8d5f69e88ecf1a4ea_443_0.png)

## 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为`/var/tmp`（也可以是其他路径）。
- 安装测试在 Red Hat Linux 6.1 和 6.2 上进行。
- 安装的所有步骤都将以超级用户账户`root`执行。
- `wu-ftpd`版本号为 2.6.0。

## 软件包

Wu-ftpd 主页：<http://www.wu-ftpd.org/>

Wu-ftpd FTP 站点：`205.133.13.68`

你必须确保下载：`wu-ftpd-2.6.0.tar.gz`

## 编译

解压 tar.gz 存档文件：

```bash
[root@deep /]# cp wu-ftpd-version.tar.gz /var/tmp
[root@deep /]# cd /var/tmp
[root@deep tmp]# tar xzpf wu-ftpd-version.tar.gz
```

## 编译与优化

进入新的 Wu-ftpd 目录，在终端中输入以下内容：

### 步骤 1

编辑`ftpcount.c`文件（`vi +241 src/ftpcount.c`），将以下行：

```c
#if defined (LINUX)
```

修改为：

```c
#if defined (LINUX_BUT_NOT_REDHAT_6_0)
```

### 步骤 2

编辑`pathnames.h.in`文件（`vi +42 src/pathnames.h.in`），将以下行：

```c
#define _PATH_EXECPATH "/bin/ftp-exec"
```

修改为：

```c
#define _PATH_EXECPATH "/usr/bin/ftp-exec"
```

我们将`ftp-exec`的`/bin`目录更改为`/usr/bin`，以适用于 Red Hat Linux。

### 步骤 3

在终端中输入以下命令来配置 Wu-ftpd：

```bash
CC="egcs" \
CFLAGS="-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
./configure \
--prefix=/usr \
--sysconfdir=/etc \
--localstatedir=/var \
--disable-dnsretry \
--enable-quota \
--enable-pam \
--disable-daemon \
--disable-newlines \
--disable-virtual \
--disable-plsm \
--disable-pasvip \
--disable-anonymous \
--enable-ls \
--enable-numericuid
```

**这会通知 Wu-ftpd 根据此特定硬件设置进行配置：**

- 不重试失败的 DNS 查询以提高性能。
- 添加 QUOTA 支持以增强安全性（仅在操作系统支持的情况下）。
- 添加 PAM 支持以增强安全性。
- 不允许作为独立守护进程运行，以便让 FTPD 由 TCP-Wrappers 控制。
- 抑制一些额外的空行。
- 不支持虚拟服务器。
- 禁用 PID 锁定睡眠消息（适用于繁忙站点）。
- 被动连接不要求相同 IP。
- 不允许匿名 FTP 访问以提高安全性。
- 使用 Wu-ftpd 新的内部`ls`命令，而非 Linux 默认的`ls`，以提高安全性。
- 内部`ls`显示 UID 而非用户名，以获得更好的性能（更快）。

### 步骤 4

现在，我们必须将 Wu-ftpd 安装到 Linux 服务器上：

```bash
[root@deep wu-ftpd-2.6.0]# make
[root@deep wu-ftpd-2.6.0]# make install
[root@deep wu-ftpd-2.6.0]# install -m 755 util/xferstats /usr/sbin/
[root@deep wu-ftpd-2.6.0]# touch /var/log/xferlog
[root@deep wu-ftpd-2.6.0]# chmod 600 /var/log/xferlog
[root@deep wu-ftpd-2.6.0]# cd /usr/sbin/
[root@deep sbin]# ln -sf in.ftpd /usr/sbin/wu.ftpd
[root@deep sbin]# ln -sf in.ftpd /usr/sbin/in.wuftpd
[root@deep sbin]# strip /usr/bin/ftpcount
[root@deep sbin]# strip /usr/bin/ftpwho
[root@deep sbin]# strip /usr/sbin/in.ftpd
[root@deep sbin]# strip /usr/sbin/ftpshut
[root@deep sbin]# strip /usr/sbin/ckconfig
[root@deep sbin]# strip /usr/sbin/ftprestart
```

上面的命令`make`和`make install`将配置软件，确保系统具备成功编译软件包所需的功能和库，将所有源文件编译成可执行二进制文件，然后将二进制文件及任何支持文件安装到适当位置。

`install -m`将安装用于查看传输文件静态信息的程序`xferstats`，`touch`命令将在`/var/log`目录下为`xferstats`创建日志文件。`chmod`将把`xferlog`文件的权限更改为仅超级用户`root`可读写。之后我们为`in.ftpd`二进制文件创建符号链接，最后，剥离所有与 Wu-ftpd 相关的二进制文件以减小其大小，从而获得更好的性能。

## 工作完成后清理

```bash
[root@deep /]# cd /var/tmp
[root@deep tmp]# rm -rf wu-ftpd-version/ wu-ftpd-version.tar.gz
```

`rm`命令将删除我们用于编译和安装 Wu-ftpd 的所有源文件，同时从`/var/tmp`目录中删除 Wu-ftpd 的压缩存档。

## 为每个用户设置无 shell 的 FTP 用户账户

为你的严格 FTP 用户不分配 Linux 系统上的真实 shell 账户非常重要。这样，如果有人因任何原因成功逃离了 FTP 隔离环境，也无法执行任何用户任务，因为它没有 bash shell。首先，为此目的创建新用户；这些用户将是被允许连接到你 FTP 服务器的用户。这必须与具有无限制访问权限的普通用户账户分开，因为`chroot`环境的工作方式。Chroot 使用户视角下，他们所处的文件系统层级看起来像是文件系统的顶层。

### 步骤 1

使用以下命令在`/etc/passwd`文件中创建用户。对于每个你允许访问 FTP 服务器的新用户，都必须执行此步骤。

```bash
[root@deep /]# mkdir /home/ftp
[root@deep /]# useradd -d /home/ftp/ftpadmin/ -s /dev/null ftpadmin > /dev/null 2>&1
[root@deep /]# passwd ftpadmin

Changing password for user ftpadmin

New UNIX password:

Retype new UNIX password:

passwd: all authentication tokens updated successfully
```

此外，应注意该目录应在服务器信任的 confidence 上创建。`useradd`命令会将名为`ftpadmin`的新用户添加到我们的 Linux 服务器。最后，`passwd`命令将为`ftpadmin`用户设置密码。一旦创建了`home/ftp/`目录，对于额外的 FTP 用户就不需要再使用此命令了。

### 步骤 2

编辑`/etc/shells`文件（`vi /etc/shells`），并添加一个不存在的 shell 名称，例如`null`。此伪 shell 将限制 FTP 用户对系统的访问。

```text
[root@deep /]# vi /etc/shells

/bin/bash
/bin/sh
/bin/ash
/bin/bsh
/bin/tcsh
/bin/csh

/dev/null ← 这是我们添加的不存在的 shell
```

**注意：**在 Red Hat Linux 中，存在一个特殊的设备名（`/dev/null`），用于此类目的。

### 步骤 3

现在，编辑你的`/etc/passwd`文件，并手动添加`/.`行来分隔`/home/ftp`目录与`ftpadmin`目录，用户`ftpadmin`应被自动 chdir 到其中。对于添加到`passwd`文件中的-options-中的每个 FTP 用户，都必须执行此步骤。

编辑`passwd`文件（`vi /etc/passwd`），并为用户`ftpadmin`添加/修改行：

```text
ftpadmin:x:502:502::/home/ftp/ftpadmin/:/dev/null

改为：

ftpadmin:x:502:502::/home/ftp/./ftpadmin/:/dev/null
                      ^^
```

账户是`ftpadmin`，但你会注意到其主目录路径有些特别。第一部分`/home/ftp`表示应被视为其新根目录的文件系统。点号`.`将其与应被自动 chdir（change directory'd）到的目录`ftpadmin/`分隔开。

再次说明，`/dev/null`部分禁用了他们作为普通用户的登录权限。通过此修改，用户`ftpadmin`现在拥有一个伪 shell 而非真正的 shell，从而在系统上获得适当限制的 pumps 访问权限。

## 设置 chroot 用户环境

你实际上是在创建一个骨架根文件系统，其中包含允许 Unix 在用户登录时执行 chroot 所必需的最少组件（binerals、密码文件等）。请注意，如果你在编译时使用了上面提到的`--enable-ls`选项，则不需要`/home/ftp/bin`和`/home/ftp/lib`目录，因为此新选项允许 Wu-ftpd 使用其自身的`ls`功能。我们仍然继续展示旧方法，以供那些喜欢将`/bin/ls`复制到 chroot 的 FTP 目录（`/home/ftp/bin`）并创建与`ls`相关的适当库的 pumps 参考。

以下是在 chroot jail 中运行 Wu-ftpd 软件的必要步骤：

### 步骤 1

首先创建所有必要的 chroot 环境目录，如下所示：

```bash
[root@deep /]# mkdir /home/ftp/dev
[root@deep /]# mkdir /home/ftp/etc
[root@deep /]# mkdir /home/ftp/bin（仅当不使用`--enable-ls`选项时需要）
[root@deep /]# mkdir /home/ftp/lib（仅当不使用`--enable-ls`选项时需要）
```

### 步骤 2

出于安全考虑，将新目录的权限更改为 0511：

```bash
[root@deep /]# chmod 0511 /home/ftp/dev/
```



```bash
[root@deep /]# chmod 0511 /home/ftp/etc/

[root@deep /]# chmod 0511 /home/ftp/bin（仅当不使用 `--enable-ls` 选项时需要）

[root@deep /]# chmod 0511 /home/ftp/lib（仅当不使用 `--enable-ls` 选项时需要）
```

`chmod` 命令将使我们的 chroot `dev`、`etc`、`bin` 和 `lib` 目录对超级用户 `root` 可读可执行，对用户组和所有用户可执行。

## Step 3

将 `/bin/ls` 二进制文件复制到 `/home/ftp/bin` 目录，并将 `ls` 程序的权限更改为 `0111`。（你不希望用户能够修改这些二进制文件。）

```bash
[root@deep /]# cp /bin/ls /home/ftp/bin（仅当不使用 `--enable-ls` 选项时需要）

[root@deep /]# chmod 0111 /bin/ls /home/ftp/bin/ls（仅当不使用 `--enable-ls` 选项时需要）
```

**注意：** 此步骤仅在配置 Wu-ftpd 时未使用 `--enable-ls` 选项的情况下才是必需的。有关更多信息，请参阅本章中的“Compile and Optimize”部分。

## Step 4

查找 `ls` Linux 二进制程序的共享库依赖：

```bash
[root@deep /]# ldd /bin/ls（仅当不使用 `--enable-ls` 选项时需要）
```

```text
libc.so.6 => /lib/libc.so.6 (0x00125000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00110000)
```

将上述识别的共享库复制到 `/home/ftp` 目录下的新 `lib` 目录：

```bash
[root@deep /]# cp /lib/libc.so.6 /home/ftp/lib/（仅当不使用 `--enable-ls` 选项时需要）

[root@deep /]# cp /lib/ld-linux.so.2 /home/ftp/lib/（仅当不使用 `--enable-ls` 选项时需要）
```

**注意：** 需要这些库才能使 `ls` 工作。此外，上述步骤 3 和 4 仅在您想使用 Linux `ls` 二进制程序而非 Wu-ftpd 使用 `--enable-ls` 选项的内置 `ls` 功能时才需要。

## Step 5

创建你的 `/home/ftp/dev/null` 文件：

```bash
[root@deep /]# mknod /home/ftp/dev/null c 1 3

[root@deep /]# chmod 666 /home/ftp/dev/null
```

## Step 6

将 `group` 和 `passwd` 文件复制到 `/home/ftp/etc` 目录。这些不应与真实的文件相同。因此，我们将在两个文件（`passwd` 和 `group`）中删除除超级用户 `root` 之外的所有非 FTP 用户。

```bash
[root@deep /]# cp /etc/passwd /home/ftp/etc/

[root@deep /]# cp /etc/group /home/ftp/etc/
```

编辑 `passwd` 文件（`vi /home/ftp/etc/passwd`），并删除除超级用户 `root` 和你允许的 FTP 用户之外的所有条目。chroot 环境中的 `passwd` 文件的条目应如下所示，这点非常重要：

```text
root:x:0:0:root:/:/dev/null
ftpadmin:x:502:502::/ftpadmin:/dev/null
```

**注意：** 这里我们可以注意到两点：首先，此修改后的 `passwd` 文件中所有用户的主目录现在都更改为反映新的 chroot FTP 目录（即 `/home/ftp/./ftpadmin/` 变为 `/ftpadmin/`）；其次，`root` 账户的用户登录 shell 名称已更改为 `/dev/null`。

编辑 `group` 文件（`vi /home/ftp/etc/group`），并删除除超级用户 `root` 和所有允许的 FTP 用户之外的所有条目。`group` 文件应与你的普通 group 文件相对应：

```text
root:x:0:root
ftpadmin:x:502:
```

## Step 7

现在我们必须将 chroot jail 目录中的 `passwd` 和 `group` 文件设置为不可更改，以提高安全性。

- 为 `passwd` 文件设置不可更改位：

  ```bash
  [root@deep /]# cd /home/ftp/etc/

  [root@deep /]# chattr +i passwd
  ```

- 为 `group` 文件设置不可更改位：

  ```bash
  [root@deep /]# cd /home/ftp/etc/

  [root@deep /]# chattr +i group
  ```

## 配置

我们在本书中描述的所有软件都有一个特定的目录和子目录，位于名为 `floppy.tgz` 的 tar 压缩归档中，其中包含特定程序的配置文件。如果你获取此归档文件，就不必手动复制不同的配置文件，或者剪切粘贴来创建配置文件。无论你是决定手动复制它们，还是从归档中获取为你方便制作的文件，你都有责任修改、调整以适应你的需求，并将与 Wu-ftpd 软件相关的文件放置到服务器上的适当位置，如下所示。可下载的服务器配置文件归档位于以下互联网地址：<http://www.openna.com/books/floppy.tgz>

要运行 FTP 服务器，需要以下文件，必须创建或复制到服务器上的适当目录。

- 将 `ftpaccess` 文件复制到 `/etc/` 目录。
- 将 `ftpusers` 文件复制到 `/etc/` 目录。
- 将 `ftphosts` 文件复制到 `/etc/` 目录。
- 将 `ftpgroups` 文件复制到 `/etc/` 目录。
- 将 `ftpconversion` 文件复制到 `/etc/` 目录。
- 将 `ftp` 文件复制到 `/etc/pam.d/` 目录。
- 将 `ftpd` 文件复制到 `/etc/logrotate.d/` 目录。

你可以在我们的 `floppy.tgz` 归档中获取下面列出的配置文件。从解压后的 `floppy.tgz` 归档中将以下文件复制到适当位置，或直接从本书中复制粘贴到相关文件。

## `/etc/ftpaccess` 文件的配置

`/etc/ftpaccess` 文件是用于配置 Wu-ftpd 服务器运行的主配置文件。此文件是控制哪些用户、多少用户可以访问你的服务器，以及安全配置的其他重要方面的主要手段。文件中的每一行要么定义一个属性，要么设置其值。

### Step 1

编辑 `ftpaccess` 文件（`vi /etc/ftpaccess`），并在该文件中添加或修改以下行：

```text
class openna guest 208.164.186.*
```

```text
limit openna 20 MoTuWeTh,Fr0000-1800 /home/ftp/.too_many.msg

email admin@openna.com
```

```text
loginfails 3
```

```text
readme README* login
readme README* cwd=*
```

```text
message /home/ftp/.welcome.msg    login

message .message                cwd=*

compress      yes               all

tar           yes               all

chmod         yes               guest

delete        yes               guest

overwrite     yes               guest

rename        yes               guest

log commands real,guest

log transfers real,guest inbound,outbound

guestgroup ftpadmin

guestgroup webmaster
```

```text
# 我们不希望用户能够上传文件到这些区域。

upload /home/ftp/* /               no

upload /home/ftp/* /etc            no

upload /home/ftp/* /dev            no

# 我们将使用 noretrieve 阻止下载。

noretrieve /home/ftp/etc

noretrieve /home/ftp/dev
```

```text
log security real,guest

guest-root /home/ftp ftpadmin webmaster

restricted-uid ftpadmin webmaster

restricted-gid ftpadmin webmaster

greeting terse

keepalive yes

noretrieve .notar
```

### 第二步

现在，将其默认权限更改为 `600`：

```bash
[root@deep /]# chmod 600 /etc/ftpaccess
```

**这告诉 ftpaccess 文件为以下特定配置进行设置：**

```text
class  openna  guest  208.164.186.*
```

`class` 选项指定可以访问 FTP 服务器的用户类别。你可以在 `ftpaccess` 文件中定义任意多个类别。在我们的示例中，我们定义了类别名称 `openna`，并且只允许来自地址 `208.164.186.*` 的访客用户 `guest` 通过 FTP 访问其主目录。需要注意的是，存在三种不同类型的用户：**anonymous**（匿名）、**guest**（访客）和 **real**（真实）。**Anonymous** 用户是指网络上任何连接到服务器并在没有账户的情况下传输文件的人。**Guest** 用户是系统上的真实用户，其会话设置与匿名 FTP 完全相同（这是我们在示例中设置的），而 **Real** 用户必须拥有账户和 shell（这可能带来安全风险）才能访问服务器。

```text
limit openna 20 MoTuWeTh,Fr0000-1800 /home/ftp/.too_many.msg
```

`limit` 选项指定按类别和时间段允许登录 FTP 服务器的用户数量。在我们的示例中，我们将类别名称 `openna` 访问 FTP 服务器的用户限制为 `20`，从周一到周四 `MoTuWeTh` 全天，以及周五从午夜到下午 6:00 `Fr0000-1800`。此外，如果达到 20 个用户的限制，文件 `/home/ftp/.too_many.msg` 的内容将显示给连接的用户。当你需要控制服务器资源时，这是一个有用的参数。

```text
loginfails 3
```

`loginfails` 选项指定连接客户端在被断开之前可以进行的失败登录尝试次数。在我们的示例中，用户在三次失败尝试后将被断开与 FTP 服务器的连接。

```text
readme  README*  login

readme  README*  cwd=*
```

`readme` 选项指定在登录时或在使用更改工作目录命令时，通知客户端其当前目录中的某个文件最后修改时间。在我们的示例中，我们将文件名设置为相对于 FTP 目录 `README*`，并且显示消息的条件为：成功登录时显示 `login`，或客户端进入新的默认目录时显示 `cwd=*`。

```text
message /home/ftp/.welcome.msg  login

message .message                cwd=*
```

`message` 选项指定在客户端登录时或在使用更改工作目录命令时显示特殊消息。在我们的示例中，我们指示了要显示的文件的位置和名称 `/home/ftp/.welcome.msg` 或 `.message`，以及显示文件的条件：成功登录时显示 `login`，或客户端进入新目录时显示 `cwd=*`。对于上面的 `readme` 和 `message` 选项，请记住，当你为匿名用户指定路径时，该路径必须是相对于匿名 FTP 目录的绝对路径。

| 命令 | 值 | 组 |
| --- | --- | --- |
| `compress` | `yes` | `all` |
| `tar` | `yes` | `all` |
| `chmod` | `yes` | `guest` |
| `delete` | `yes` | `guest` |
| `overwrite` | `yes` | `guest` |
| `rename` | `yes` | `guest` |

这些选项 `compress`、`tar`、`chmod`、`delete`、`overwrite` 和 `rename` 指定你希望授予用户对这些命令的权限。在我们的示例中，我们授予访客组 `guest` 执行 `chmod`、`delete`、`overwrite` 和 `rename` 文件的权限，并允许所有人使用 `compress` 和 `tar` 命令 `all`。如果你未指定以下指令，它们默认对所有人设置为 `yes`。

```text
log commands real,guest
```

`log commands` 选项指定出于安全目的启用对用户单个命令的日志记录。在我们的示例中，我们记录所有 **real** 和 **guest** 用户的单个命令 `real,guest`。生成的日志存储在 `/var/log/message` 文件中。

```text
log transfers real,guest inbound,outbound
```

`log transfers` 选项指定出于安全目的记录所有 FTP 传输。在我们的示例中，我们记录所有 **real** 和 **guest** 用户的传输 `real,guest`，包括 **inbound**（入站）和 **outbound**（出站）`inbound,outbound`，这些指定了必须记录传输的方向。生成的日志存储在 `/var/log/xferlog` 文件中。

```text
guestgroup ftpadmin

guestgroup webmaster
```

`guestgroup` 选项指定系统上所有作为真实用户的访客组，其会话设置与匿名 FTP 完全相同 `ftpadmin` 和 `webmaster`。`/home/ftp/etc/group` 文件包含每个允许组的条目，每个组只有一个成员。重要的是，`guestgroup` 在配置文件中每行只出现一次。

```text
log security real,guest
```

`log security` 选项指定启用对 `real`、`guest` 和/或匿名 FTP 客户端违反安全规则的日志记录。在我们的示例中，我们指定记录使用 FTP 服务器访问真实账户的用户，以及使用 FTP 服务器访问访客账户的用户 `real,guest` 的违规行为。

```text
guest-root /home/ftp ftpadmin webmaster

restricted-uid ftpadmin webmaster

restricted-gid ftpadmin webmaster
```

这些子句 `guest-root`、`restricted-uid`、`restricted-gid` 指定并控制是否允许 `guest` 用户访问 FTP 服务器上其主目录之外的区域（这是一项重要的安全功能）。在我们的示例中，我们为用户 `ftpadmin` 和 `webmaster` 指定了 `chroot()` 路径为 `/home/ftp`，并且他们不能访问彼此的文件，因为他们被限制在自己的主目录中（`restricted-uid ftpadmin webmaster`、`restricted-gid ftpadmin webmaster`）。可以在一行中给出多个 UID 范围。如果为用户选择了 `guest-root`，则使用 `<root-dir>/etc/passwd` 文件中的用户主目录来确定初始目录，而不使用系统范围的 `/etc/passwd` 中的主目录。这是一项安全功能。

```text
greeting terse
```

`greeting` 选项指定在远程用户登录之前将显示多少系统信息。有三个参数可供选择：`full` 是默认值，显示服务器的主机名和守护进程版本；`brief` 仅显示主机名；`terse` 则只会在你的终端显示“FTP server ready”。

```text
keepalive yes
```

`keepalive` 选项指定系统是否应向远程 FTP 服务器发送 keepalive 消息。如果设置为 `yes`，则将正确检测到连接中断或远程机器崩溃。

## `/etc/ftphosts` 文件的配置

`/etc/ftphosts` 文件用于定义是否允许用户从某些主机登录，或是否拒绝访问。

### 第一步

创建 `ftphosts` 文件（`touch /etc/ftphosts`），并在此文件中添加以下行：

```text
# 主机访问文件示例
#
# '#' 之后的所有内容都被视为注释，
# 空行将被忽略

allow ftpadmin 208.164.186.1 208.164.186.2 208.164.186.4

deny ftpadmin 208.164.186.5
```



在下面的示例中，我们允许用户`<ftpadmin>`从明确列出的地址`<208.164.186.1 208.164.186.2 208.164.186.4>`通过 FTP 连接，并拒绝指定的`<ftpadmin>`用户从站点`<208.164.186.5>`连接。

## 第二步

现在，将其默认权限更改为 600：

```
[root@deep /]# chmod 600 /etc/ftphosts
```

## “/etc/ftpusers”文件的配置

“/etc/ftpusers”文件指定了**不允许**连接到您的FTP服务器的用户。

### 步骤 1

创建`ftpusers`文件（`touch /etc/ftpusers`），并出于安全原因在该文件中添加以下用户：

- `root`
- `bin`
- `daemon`
- `adm`
- `lp`
- `sync`
- `shutdown`
- `halt`
- `mail`
- `news`
- `uucp`
- `operator`
- `games`
- `nobody`

### 步骤 2

现在，将其默认权限更改为 600：

```
[root@deep /]# chmod 600 /etc/ftpusers
```

## “/etc/ftpconversions”文件的配置

“/etc/ftpconversions”文件包含允许您在传输前按需压缩文件的指令。

### 步骤 1

编辑`ftpconversions`文件（`vi /etc/ftpconversions`），并在该文件中添加以下行：

```
.Z: : :/bin/compress -d -c %s:T_REG|T_ASCII:O_UNCOMPRESS:UNCOMPRESS
: :..Z:/bin/compress -c %s:T_REG:O_COMPRESS:COMPRESS
:.gz: : :/bin/gzip -cd %s:T_REG|T_ASCII:O_UNCOMPRESS:GUNZIP
: :.gz:/bin/gzip -9 -c %s:T_REG:O_COMPRESS:GZIP
:.tar: : :/bin/tar -c -f - %s:T_REG|T_DIR:O_TAR:TAR
:.tar.Z: : :/bin/tar -c -Z -f - %s:T_REG|T_DIR:O_COMPRESS|O_TAR:TAR+COMPRESS
:.tar.gz: : :/bin/tar -c -z -f - %s:T_REG|T_DIR:O_COMPRESS|O_TAR:TAR+GZIP
:.crc: : :/bin/cksum %s:T_REG::CKSUM
:.md5: : :/bin/md5sum %s:T_REG::MD5SUM
```

### 步骤 2

现在，将默认权限更改为 600：

```
[root@deep /]# chmod 600 /etc/ftpconversions
```

## “/etc/pam.d/ftp”文件的配置

配置您的“/etc/pam.d/ftp”文件以使用 pam 认证。

创建`ftp`文件（`touch /etc/pam.d/ftp`）并添加以下行：

```
#%PAM-1.0
auth	required	/lib/security/pam_listfile.so item=user sense=deny file=/etc/ftpusers onerr=succeed
auth	required	/lib/security/pam_pwdb.so shadow nullok
auth	required	/lib/security/pam_shells.so
account	required	/lib/security/pam_pwdb.so
session	required	/lib/security/pam_pwdb.so
```

## “/etc/logrotate.d/ftpd”文件的配置

配置您的“/etc/logrotate.d/ftpd”文件，以便每周自动轮转日志文件。

创建`ftpd`文件（`touch /etc/logrotate.d/ftpd`）并添加以下行：

```
/var/log/xferlog {
  # ftpd doesn't handle SIGHUP properly
  nocompress
}
```

## 配置 ftpd 使用 tcp-wrappers inetd 超级服务器

需要启用 Tcp-wrappers 来启动和停止 ftpd 服务器。执行时，`inetd`从其配置文件中读取配置信息，默认情况下该文件为“/etc/inetd.conf”。配置文件的每个字段都必须有一个条目，各字段的条目之间用制表符或空格分隔。

### 步骤 1

编辑`inetd.conf`文件（`vi /etc/inetd.conf`）并添加或验证以下行的存在：

```
ftp	stream	tcp	nowait root	/usr/sbin/tcpd	in.ftpd -l -a
```

**注意：**在上述行添加到文件中后，通过发送 SIGHUP 信号（`killall -HUP inetd`）来更新您的“inetd.conf”文件。

- 要更新您的“inetd.conf”文件，请使用以下命令：
  ```
  [root@deep /]# killall -HUP inetd
  ```

### 步骤 2

编辑`hosts.allow`文件（`vi /etc/hosts.allow`），并添加例如以下行：

```
in.ftpd: 192.168.1.4 win.openna.com
```

这表示允许客户端 IP“192.168.1.4”且主机名为“win.openna.com”的用户FTP连接到服务器。

## FTP 管理工具

### ftpwho

`ftpwho`程序工具显示系统上所有活动的 FTP 用户及其当前的进程信息。该命令的输出格式与“/bin/ps”命令相同。此命令的格式为：

- 要显示所有活动的 FTP 用户及其当前进程，请使用以下命令：
  ```
  [root@deep /]# ftpwho
  Service class openna:
  5443 ? S 0:00 ftpd: win.openna.com: ftpadmin: IDLE
  - 1 users (20 maximum)
  ```

在这里，您可以看到有一个用户已登录，允许连接的用户数为 20，该用户的用户名为“ftpadmin”，其声称来自`win.openna.com`。

### ftpcount

`ftpcount`程序工具是`ftpwho`的简化版本，仅显示当前已登录系统的用户数量以及允许的最大用户数量。

- 要仅显示当前已登录系统的用户数量以及允许的最大用户数量，请使用以下命令：
  ```
  [root@deep /]# ftpcount
  Service class openna - 1 users ( 20 maximum)
  ```

## FTP 安全加固

### ftpusers 文件

重要的是确保您已设置“/etc/ftpusers”文件，该文件指定了**不允许**连接到您的FTP服务器的用户。其中应**至少**包含以下条目：`root`、`bin`、`daemon`、`adm`、`lp`、`sync`、`shutdown`、`halt`、`mail`、`news`、`uucp`、`operator`、`games`、`nobody`以及您“/etc/passwd”文件中所有其他默认供应商提供的账户。

### 匿名 FTP 程序

若要禁用匿名 FTP，请从密码文件中删除匿名用户“`ftp`”，并验证`anonftp-version.i386.rpm`软件包未安装在您的系统上。

- 要从密码文件中删除用户“ftp”，请使用以下命令：
  ```
  [root@deep /]# userdel ftp
  ```

- 要验证匿名 FTP 程序的 RPM 软件包未安装在您的 Linux 系统上，请使用以下命令：
  ```
  [root@deep /]# rpm -q anonftp
  package anonftp is not installed
  ```

### upload 命令

默认情况下，Wu-ftpd 服务器将授予所有用户上传权限。`upload`参数允许远程客户端上传并将文件放置到 FTP 服务器上。为了获得最佳安全性，我们不希望用户能够上传到“/home/ftp”目录下的“bin”、“etc”、“dev”和“lib”子目录中。在我们的“/etc/ftpaccess”文件中，我们已经将用户 chroot 到“/home/ftp”，他们无法访问该目录结构之外的任何文件系统区域，但如果这些目录的权限发生意外变化，您应该在“/etc/ftpaccess”文件中拒绝这些区域（`/home/ftp/`、`/home/ftp/bin`、`/home/ftp/etc`、`/home/ftp/dev`和`/home/ftp/lib`）的上传权限。

编辑`ftpaccess`文件（`vi /etc/ftpaccess`）并添加以下行，以拒绝在这些区域的上传权限：

```
# We don't want users being able to upload into these areas.
upload /home/ftp/* / no
upload /home/ftp/* /etc no
upload /home/ftp/* /dev no
upload /home/ftp/* /bin no (require only if you are not using the "--enable-ls" option)
upload /home/ftp/* /lib no (require only if you are not using the "--enable-ls" option)
```

上述行指定拒绝在 chroot 的“/home/ftp”目录结构中的“/”、“/etc”、“/dev”、“/bin”和“/lib”目录中上传。

## 特殊文件“.notar”

无论您是否允许即时 tar 打包目录，您都应该确保在上传参数不允许的所有区域中，无法使用 tar 命令进行绕过操作。

### 步骤 1

为此，在每个目录和 FTP 目录中创建特殊文件“.notar”。

```
[root@deep /]# touch /home/ftp/.notar
[root@deep /]# touch /home/ftp/etc/.notar
[root@deep /]# touch /home/ftp/dev/.notar
[root@deep /]# touch /home/ftp/bin/.notar (require only if you are not using the "--enable-ls" option)
[root@deep /]# touch /home/ftp/lib/.notar (require only if you are not using the "--enable-ls" option)
[root@deep /]# chmod 0 /home/ftp/.notar
[root@deep /]# chmod 0 /home/ftp/etc/.notar
[root@deep /]# chmod 0 /home/ftp/dev/.notar
[root@deep /]# chmod 0 /home/ftp/bin/.notar (require only if you are not using the "--enable-ls" option)
[root@deep /]# chmod 0 /home/ftp/lib/.notar (require only if you are not using the "--enable-ls" option)
```

### 步骤 2

零长度的“.notar”文件可能会使某些 Web 客户端和 FTP proxies 混淆，因此让我们将其标记为不可检索以解决此问题。在您的“/etc/ftpaccess”文件中添加以下行。

编辑`ftpaccess`文件（`vi /etc/ftpaccess`）并添加以下行，以将“.notar”文件标记为不可检索。

```
noretrieve .notar
```

## noretrieve 命令

Wu-ftpd 服务器的`noretrieve`参数允许您拒绝传输选定的目录或文件。在您的“/etc/ftpaccess”文件中使用“noretrieve”命令阻止这些子目录（`bin`、`etc`、`dev`和`lib`）的下载也是一个好主意。

编辑`ftpaccess`文件（`vi /etc/ftpaccess`）并添加以下行，以拒绝这些区域的传输。

```
# We'll prevent downloads with noretrieve.
noretrieve /home/ftp/etc
noretrieve /home/ftp/dev
noretrieve /home/ftp/bin (require only if you are not using the "--enable-ls" option)
noretrieve /home/ftp/lib (require only if you are not using the "--enable-ls" option)
```

## 已安装的文件

- `/etc/pam.d/ftp`
- `/etc/logrotate.d/ftpd`
- `/etc/ftpaccess`
- `/etc/ftpconversions`
- `/etc/ftpgroups`
- `/etc/ftphosts`
- `/etc/ftpusers`
- `/home/ftp/`
- `/usr/man/man5/ftpconversions.5`
- `/usr/man/man5/xferlog.5`
- `/usr/man/man8/ftpd.8`
- `/usr/man/man8/ftpshut.8`
- `/usr/man/man8/ftprestart.8`
- `/usr/sbin/in.ftpd`
- `/usr/sbin/ftpshut`
- `/usr/sbin/ckconfig`
- `/usr/bin/ftpcount`
- `/usr/bin/ftpwho`
- `/usr/man/man1/ftpcount.1`
- `/usr/man/man1/ftpwho.1`
- `/usr/man/man5/ftpaccess.5`
- `/usr/man/man5/ftphosts.5`
- `/usr/sbin/ftprestart`
- `/usr/sbin/xferstats`
- `/usr/sbin/wu.ftpd`
- `/usr/sbin/in.wuftpd`
- `/var/log/xferlog`

# 第五部分 备份相关参考

在本部分中

## 备份与恢复程序

# 第22章 备份与恢复程序

在本章中

- `tar`备份程序
- 使用`tar`进行备份
- 自动化`tar`备份任务
- 使用`tar`恢复文件
- `dump`备份程序
- 使用`dump`进行备份
- 使用`dump`恢复文件
- 通过网络进行备份和恢复

## Linux 备份与恢复

### 概述

服务器的安全可靠与定期执行备份密切相关。故障有时可能不可避免，原因包括攻击、硬件故障、人为错误、电源中断等。最安全的备份方法是将备份记录存放在与 Linux 系统分离的位置，例如通过网络、磁带、可移动硬盘、可写 CD-ROM 等。

Linux 存在多种备份方法，例如“dump”、“tar”、“cpio”以及“dd”，这些工具在您的 Linux 系统中默认可用。此外，还有一些基于文本的实用工具，例如“Amanda”，旨在为备份和恢复程序提供更友好的用户界面。最后，还有商业备份实用工具可用，例如“BRU”。

执行备份和恢复的具体步骤会因您选择的备份方案而有所不同。因此，我们将讨论使用传统 UNIX 工具进行备份的方法：“tar”以及命令行备份工具“dump”。

### 需要备份什么

备份的理念是尽可能多地备份系统中的内容，但也有一些例外情况，如下所示。将这些内容包含在备份中是不合理的，因为您会因此浪费时间和媒体空间。

主要不应包含在备份中的例外情况包括：

- “/proc”文件系统：由于它只包含内核自动生成的数据，备份它永远不是好主意。
- “/mnt”文件系统，因为它是挂载可移动媒体（如 CD-ROM、软盘等）的位置。
- 存放备份文件的备份目录或媒体，例如磁带、CD-ROM、NFS 挂载的文件系统、远程/本地目录或其他类型的媒体。
- 可以轻松重新安装的软件，尽管它们可能有一些需要备份的重要配置文件，以免您重新进行所有配置工作。我建议将这些（软件的配置文件）放在软盘上。

### tar 备份程序

#### 描述

`tar`备份程序是一种归档程序，用于从称为 tarfile 的归档文件中存储和提取文件。tarfile 可以在磁带驱动器上创建；不过，将 tarfile 写入普通文件也很常见。

#### 简单的备份方案

当您决定对系统中的文件进行备份时，必须在备份程序开始之前选择一种备份方案。存在许多战略性备份方案，取决于您想要使用的备份策略。在以下内容中，我将向您展示一种可以利用`tar`程序功能的备份方案。该方案是先完整备份所有内容一次，然后备份自上次备份以来修改过的所有内容。第一次备份称为**完整备份**；后续备份称为**增量备份**。

### 使用 tar 进行备份

使用六盒磁带，您可以每天进行备份；流程是使用磁带 1 进行第一次完整备份（周五 1），磁带 2 到 5 用于增量备份（周一到周四）。然后，使用磁带 6 进行新的完整备份（第二个周五），并再次使用磁带 2 到 5 进行增量备份。重要的是保持磁带 1 的现有状态，直到您用磁带 6 完成新的完整备份。在以下示例中，我们假设将备份写入名为`(/dev/st0)`的 SCSI 磁带驱动器，并备份我们系统的 home 目录`(/home)`。

首先，我们必须移动到文件系统“/”分区。创建归档文件时，“tar”会去除文件路径名开头的“/”（斜杠）字符。这意味着恢复的文件可能不会回到备份时的原始位置。因此，解决此问题的方法是在进行所有备份和恢复之前切换到“/”根目录。

- 要移动到“/”根目录，使用命令：



```bash
[root@deep]# cd /
```

重要的是始终从完整备份开始（比如，在周五），例如：

- 周五 1，（使用磁带 1 进行第一次完整备份）。

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar cpf /dev/st0 --label=" full-backup created on `date '+%d-%B-%Y'`." \
  --directory / home
  ```

- 周一，（使用磁带 2 进行增量备份）。

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar cpNf /dev/st0 --label=" full-backup created on `date '+%d-%B-%Y'`." \
  --directory / home
  ```

- 周二，（使用磁带 3 进行增量备份）。

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar cpNf /dev/st0 --label=" full-backup created on `date '+%d-%B-%Y'`." \
  --directory / home
  ```

- 周三，（使用磁带 4 进行增量备份）。

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar cpNf /dev/st0 --label=" full-check your backup created on `date '+%d-%B-%Y'`." \
  --directory / home
  ```

- 周四，（使用磁带 5 进行增量备份）。

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar cpNf /dev/st0 --label=" full-backup created on `date '+%d-%B-%Y'`." \
  --directory / home
  ```

- 周五 2，（使用磁带 6 进行新的完整备份）。

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar cpf /dev/st0 --label=" full-backup created on `date '+%d-%B-%Y'`." \
  --directory / home
  ```

- 现在，再次使用磁带 2 到 5 进行增量备份，以此类推。

`c` 选项指定正在创建归档文件。

`p` 选项保留权限；文件保护信息将被“记住”。

`N` 选项执行增量备份，仅存储比指定日期更新的文件。

`f` 选项表示下一个参数将是正在写入的归档文件或设备的名称。

注意包含当前日期的文件名是如何通过将`date`命令置于两个反引号字符之间来生成的。常见的命名约定是为未压缩的归档添加`tar`后缀，为压缩的归档添加`tar.gz`后缀。由于我们无法为备份集指定文件名，因此可以使用`--label`选项将有关备份集的一些信息写入归档文件本身。最后，仅将`/home`中的文件写入磁带。

由于磁带驱动器是字符设备，无法指定实际的文件名。因此，用作`tar`参数的文件名仅仅是设备名称`/dev/st0`，即第一个磁带设备。`/dev/st0`设备在备份集写入后不会回卷；因此，可以在一盒磁带上写入多个备份集。您也可以将设备称为`/dev/st0`，在这种情况下，备份集写入后磁带会自动回卷。使用磁带时，您可以使用以下命令来回卷和弹出磁带：

```bash
[root@deep /]# mt -f /dev/st0 rewind
[root@deep /]# mt -f /dev/st0 offline
```

**警告**：为了减少`tar`归档所需的空间，可以使用`tar`程序的`z`选项压缩备份。不幸的是，使用此选项压缩备份可能会导致问题。由于压缩工作的特性，如果压缩备份中的单个位出错，所有其余压缩数据都将丢失。**建议不要**使用压缩（`z`选项）来执行`tar`命令备份。

- 如果备份无法放入一盒磁带，您需要使用`--multi-volume (-M)`选项：

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar cMpf /dev/st0 /home

  Prepare volume #2 for /dev/st0 and hit return:
  ```

- 完成备份后，您应该使用`--compare (-d)`选项检查备份是否正常，如下所示：

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar dvf /dev/st0
  ```

- 要执行整个系统的备份，使用以下命令：

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar cpf /archive/full-backup-`date '+%d-%B-%Y'`.tar \
  --directory / --exclude=proc --exclude=mnt --exclude=archive \
  --exclude=cache --exclude=*/lost+found .
  ```

`--directory`选项告诉`tar`在开始备份之前先切换到以下目录路径（本例中为`/`目录）。`--exclude`选项告诉`tar`不必备份指定的目录或文件。最后，命令末尾的`.`字符告诉`tar`应该备份当前目录中的所有内容。

**警告**：备份文件系统时，**不要**包含`/proc`伪文件系统！`/proc`中的文件实际上不是文件，而只是描述和指向内核数据结构的类文件链接。同样，**不要**包含`/mnt`、`/archive`以及所有`lost+found`目录。

## 自动化 tar 备份任务

自动化备份任务总是很有趣的。自动化为实现您设定的 Linux 服务器目标提供了巨大的机会。以下示例是我们的备份脚本，名为`backup.cron`。此脚本设计用于在任何计算机上运行。

只需修改以下四个变量：`COMPUTER`、`DIRECTORIES`、`BACKUPDIR`和`TIMEDIR`。建议您在本月初首次设置并运行此脚本，然后运行一个月后再进行重大更改。在下面的示例中，我们将备份存储到本地服务器上的一个目录（`BACKUPDIR`）中，但您可以修改此脚本，使其备份到本地服务器上的磁带，或通过 NFS 挂载的文件系统。

## 步骤 1

创建备份脚本`backup.cron`文件（`touch /etc/cron.daily/backup.cron`），并将以下行添加到此备份文件中：

```sh
#!/bin/sh

# full and incremental backup script

# created 07 February 2000

# Based on a script by Daniel O'Callaghan <danny@freebsd.org>

# and modified by Gerhard Mourani <gmourani@videotron.ca>

#Change the 5 variables below to fit your computer/backup

COMPUTER=deep              # name of this computer

DIRECTORIES="/home"        # directoris to backup

BACKUPDIR=/backups         # where to store the backups

TIMEDIR=/backups/last-full # where to store time of full backup

TAR=/bin/tar               # name and location of tar

#You should not have to change anything below here

PATH=/usr/local/bin:/usr/bin:/bin

DOW=`date +%a`        # Day of the week e.g. Mon

DOM=`date +%d`        # Date of the Month e.g. 27

DM=`date +%d%b`       # Date and Month e.g. 27Sep

# On the 1st of the month a permanet full backup is made

# Every Sunday a full backup is made - overwriting last Sundays backup

# The rest of the time an incremental backup is made. Each incremental

# backup overwrites last weeks incremental backup of the same name.

#

# if NEWER = "", then tar backs up all files in the directories

# otherwise it backs up files newer than the NEWER date. NEWER

# gets it date from the file written every Sunday.

# Monthly full backup

if [ $DOM = "01" ]; then

    NEWER=""

    $TAR $NEWER -cf $BACKUPDIR/$COMPUTER-$DM.tar $DIRECTORIES

fi

# Weekly full backup

if [ $DOW = "Sun" ]; then

    NEWER=""

    NOW=`date +%d-%b`

    # Update full backup date

    echo $NOW > $TIMEDIR/$COMPUTER-full-date

    $TAR $NEWER -cf $BACKUPDIR/$COMPUTER-$DOW.tar $DIRECTORIES

# Make incremental backup - overwrite last weeks

else

    # Get date of last full backup

    $TAR $NEWER -cf $BACKUPDIR/$COMPUTER-$DOW.tar $DIRECTORIES

fi
```

以下是备份目录在一周后的简略视图：

```text
[root@deep /]# ls -l /backups/

total 22217

-rw-r--r--  1 root  root  10731288  Feb  7 11:24 deep-01Feb.tar

-rw-r--r--  1 root  root      6879  Feb  7 11:24 deep-Fri.tar

-rw-r--r--  1 root  root      2831  Feb  7 11:24 deep-Mon.tar

-rw-r--r--  1 root  root      7924  Feb  7 11:25 deep-Sat.tar

-rw-r--r--  1 root  root  11923013  Feb  7 11:24 deep-Sun.tar

-rw-r--r--  1 root  root      5643  Feb  7 11:25 deep-Thu.tar

-rw-r--r--  1 root  root      3152  Feb  7 11:25 deep-Tue.tar

-rw-r--r--  1 root  root      4567  Feb  7 11:25 deep-Wed.tar

drwxr-xr-x  2 root  root      1024  Feb  7 11:20 last-full
```

> 注意：存储备份的目录（`BACKUPDIR`）以及存储完全备份时间的目录（`TIMEDIR`）必须在使用备份脚本之前存在或已创建，否则会收到错误消息。

## 步骤 2

如果您不是在月初（01-月-年）开始运行此备份脚本，增量备份将需要周日备份的时间才能正常工作。如果您在周中开始，则需要在`TIMEDIR`中创建时间文件。

- 要在`TIMEDIR`目录中创建时间文件，请使用以下命令：

  ```bash
  [root@deep /]# date +%d%b > /backups/last-full/myserver-full-date
  ```

其中`/backups/last-full`是我们的变量`TIMEDIR`，即我们希望存储完全备份时间的位置，`myserver-full-date`是我们的服务器名称（例如，deep），我们的时间文件由包含当前日期的单行组成（即 15-Feb）。

## 步骤 3

将此段落设为计划。修复：可执行文件，并将其默认权限更改为仅允许超级用户`root`写入（755）。

```bash
[root@deep /]# chmod 755 /etc/cron.daily/backup.cron
```

> 注意：由于此脚本位于`/etc/cron.daily`目录中，它将作为 cron 作业每天凌晨一点自动运行。

## 备份和恢复程序

### 使用 tar 恢复文件

比执行定期备份更重要的是在需要恢复重要文件时能够使用它们！在本节中，我们将讨论使用`tar`命令备份的文件恢复方法。

以下命令将从`full-backup-Day-Month-Year.tar`存档中恢复所有文件，这是从上面所示的`tar`命令示例创建的我们的`home`目录的示例备份。

- 要恢复`home`目录的完全备份，请使用以下命令：

  ```bash
  [root@deep /]# cd /
  [root@deep /]# tar xpf /dev/st0/full-backup-Day-Month-Year.tar
  ```

上述命令从压缩存档中提取所有文件，保留原始文件所有权和权限。

`x`选项代表提取。  
`p`选项保留权限；文件保护信息将被“记住”。  
`f`选项表示下一个参数将是存档文件或设备的名称。

如果您不需要恢复存档中包含的所有文件，可以指定一个或多个要恢复的文件：

- 要指定要恢复的一个或多个文件，请使用以下命令：

  ```bash
  [root@deep]# cd /
  [root@deep]# tar xpf /dev/st0/full-backup-Day-Month-Year.tar \
  home/wahib/Personal/Contents.doc home/quota.user
  ```

上述命令从存档中恢复`/home/wahib/Personal/Contents.doc`和`/home/quota.user`文件。

- 如果您只想查看备份卷中有哪些文件，请使用`--list（-t）`选项：

  ```bash
  [root@deep /]# tar tf /dev/st0
  ```



> **警告：** 如果您的系统上有使用`chattr`命令设置的不可变位文件，这些文件在恢复的备份中不会保留不可变位。您必须在备份完成后使用`chattr +i`命令重新设置其不可变位。

### 测试从备份中恢复的能力

对于许多系统管理员来说，从备份中恢复文件并不常见。此步骤确保如果您需要恢复文件，工具和流程将能够正常工作。定期执行此测试将帮助您发现备份程序中的问题，以便在数据丢失之前纠正它们。某些备份恢复软件无法准确恢复正确的文件保护和文件所有权控制。检查已恢复文件的属性，以确保它们设置正确。定期测试以确保您可以从备份中执行完整的系统恢复。

### 其他文档

有关更多详细信息，您可以阅读`man`手册页：

`tar (1)` - tar 归档工具的 GNU 版本

## `dump`备份程序

### 说明

`Dump`与`tar`完全不同；它是一个用于备份和恢复文件系统的程序。它备份整个文件系统——而不是文件。`Dump`不关心硬盘上是什么文件系统，甚至不关心文件系统中是否有文件。它检查`ext2`文件系统上的文件，确定哪些需要备份，然后将这些文件复制到指定的磁盘、磁带、文件或其他存储介质。它快速高效地一次转储一个文件系统。不幸的是，它不能处理单个目录，因此它比`tar`消耗更多的存储空间。它也是专门为备份而编写的。`restore`命令执行`dump`的相反功能；它可以恢复文件系统的完全备份。然后可以将后续增量备份叠加在完全备份之上。也可以从完全或部分备份中恢复单个文件和目录子树。如果您需要同时备份文件系统和在备份后恢复文件系统的程序，可以使用`dump`。

### `Dump`级别

`Dump`有多个备份程序级别。级别范围从 0 到 9，其中级别数字 0 表示完全备份，并保证整个文件系统被复制。高于 0 的级别数字（增量备份）告诉`dump`复制自上次相同或更低级别转储以来所有新的或修改过的文件。更准确地说，在每个增量备份级别，您备份自同一级别或先前级别的上一次备份以来所有已更改的内容。创建和使用多个级别进行备份的优势和原因是什么？我尝试用以下模式解释：

`0  3  2  5  4  7  6  9  8  9`

- 0 表示完全备份。
- 3 表示复制自级别 0 以来所有新的或修改过的文件。
- 2 表示复制自级别 0、3 和 2 以来所有新的或修改过的文件。
- 5 表示复制自级别 0、3 和 5 以来所有新的或修改过的文件。
- 4 表示复制自级别 0、3 和 4 以来所有新的或修改过的文件。
- 7 表示复制自级别 0、3、4 和 7 以来所有新的或修改过的文件。
- 6 表示复制自级别 0、3、4 和 6 以来所有新的或修改过的文件。
- 9 表示复制自级别 0、3、4、6 和 9 以来所有新的或修改过的文件。
- 8 表示复制自级别 0、3、4、6 和 8 以来所有新的或修改过的文件。
- 9 表示复制自级别 0、3、4、6、8 和 9 以来所有新的或修改过的文件。

这样做的好处和原因是，使用多个级别可以更经济地扩展备份历史。更长的备份历史很有用，因为删除或损坏的文件通常需要很长时间才会被发现。即使是不太新的文件版本，也比没有文件要好。此外，备份级别用于将备份和恢复时间都保持在最低（低）水平。

`dump`手册页建议了一个充分利用备份级别的良好方案：3、2、5、4、7、6、9、8、9 等，如下表所述。您最多需要备份两天的工作。恢复所需的磁带数量取决于两次完全备份之间保留的时间。

| 磁带 | 级别 | 备份（天数） | 恢复磁带 |
|------|------|-------------|---------|
| 1 | 0 | 不适用 | 1 |
| 2 | 3 | 1 | 1, 2 |
| 3 | 2 | 2 | 1, 3 |
| 4 | 5 | 1 | 1, 2, 4 |
| 5 | 4 | 2 | 1, 2, 5 |
| 6 | 7 | 1 | 1, 2, 5, 6 |
| 7 | 6 | 2 | 1, 2, 5, 7 |
| 8 | 9 | 1 | 1, 2, 5, 7, 8 |
| 9 | 8 | 2 | 1, 2, 5, 7, 9 |
| 10 | 9 | 1 | 1, 2, 5, 7, 9, 10 |

## 使用`dump`进行备份

如果你想利用`dump`备份程序的多个备份级别，使用它是很有趣的。下面，我将向你展示一种延长备份历史并尽量减少备份和恢复时间的方法。在下面的示例中，我们假设将备份写入名为`/dev/st0`的磁带驱动器，并备份我们系统的`/home`目录。

务必从 0 级备份开始，这很重要，例如：

- 第一个星期五，（使用磁带 1 进行第一次完整备份）。

```bash
[root@deep /]# dump -0u -f /dev/st0 /home

DUMP: Date of this level 0 dump: Fri Jan 28 21:25:12 2000
DUMP: Date of last level 0 dump: the epoch
DUMP: Dumping /dev/sda6 (/home) to /dev/st0
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 18582 tape blocks on 0.48 tape(s).
DUMP: Volume 1 started at: Fri Jan 28 21:25:14 2000
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: DUMP: 18580 tape blocks on 1 volumes(s)
DUMP: finished in 4 seconds, throughput 4645 KBytes/sec
DUMP: Volume 1 completed at: Fri Jan 28 21:25:18 2000
DUMP: Volume 1 took 0:00:04
DUMP: Volume 1 transfer rate: 4645 KB/s
DUMP: level 0 dump on Fri Jan 28 21:25:12 2000
DUMP: DUMP: Date of this level 0 dump: Fri Jan 28 21:25:12 2000
DUMP: DUMP: Date this dump completed: Fri Jan 28 21:25:18 2000
DUMP: DUMP: Average transfer rate: 4645 KB/s
DUMP: Closing /dev/st0
DUMP: DUMP IS DONE
```

- 星期一，（使用磁带 2 进行增量备份）。

```bash
[root@deep /]# dump -3u -f /dev/st0 /home
```

- 星期二，（使用磁带 3 进行增量备份）。

```bash
[root@deep /]# dump -2u -f /dev/st0 /home
```

- 星期三，（使用磁带 4 进行增量备份）。

```bash
[root@deep /]# dump -5u -f /dev/st0 /home
```

- 星期四，（使用磁带 5 进行增量备份）。

```bash
[root@deep /]# dump -4u -f /dev/st0 /home
```

- 第二个星期五，（使用磁带 6 进行增量备份）。

```bash
[root@deep /]# dump -7u -f /dev/st0 /home
```

- 星期一，（使用磁带 2 进行增量备份）。

```bash
[root@deep /]# dump -3u -f /dev/st0 /home
```

- 星期二，（使用磁带 3 进行增量备份）。

```bash
[root@deep /]# dump -2u -f /dev/st0 /home
```

- 星期三，（使用磁带 4 进行增量备份）。

```bash
[root@deep /]# dump -5u -f /dev/st0 /home
```

- 星期四，（使用磁带 5 进行增量备份）。

```bash
[root@deep /]# dump -4u -f /dev/st0 /home
```

- 第三个星期五，（使用磁带 7 进行增量备份）。

```bash
[root@deep /]# dump -6u -f /dev/st0 /home
```

- 星期一，（使用磁带 2 进行增量备份）。

```bash
[root@deep /]# dump -3u -f /dev/st0 /home
```

- 星期二，（使用磁带 3 进行增量备份）。

```bash
[root@deep /]# dump -2u -f /dev/st0 /home
```

- 星期三，（使用磁带 4 进行增量备份）。

```bash
[root@deep /]# dump -5u
```

## 更多文档

如需更多详细信息，可以阅读以下`man`页面：

- `$ man dump (8)` - ext2 文件系统备份
- `$ man restore (8)` - "从 dump 创建的备份中恢复文件或文件系统"

## 通过网络进行备份和恢复

备份使您能够在发生安全违规和事故后恢复信息资源的可用性和完整性。没有备份，您可能无法在系统故障和安全违规后恢复计算机数据。制定一个足够广泛的计划以覆盖您计划部署的所有服务器非常重要。我们必须确定哪些类别的文件将被备份。例如，您可能选择仅备份用户数据文件（即`/home`），因为损坏的系统文件应从原始发行介质重新加载。

文件备份有常见的技术方法。对于网络服务器，服务器信息内容的权威版本在安全的计算机上创建和维护，并进行备份。如果服务器被入侵且其内容受损，可以从维护权威版本的安全系统重新加载。这种方法通常用于公共服务器，如 Web 服务器，因为内容在更可预测的时间间隔内变化。

确保以安全的方式执行备份并且备份内容保持安全非常重要。我们建议计划明确规定：

- 源数据在传输到存储介质之前进行加密。
- 数据在备份存储介质上保持加密状态。
- 存储介质存放在物理安全的设施中，以防止人为和自然灾害。

## 以安全的方式通过网络传输备份

在前面的章节中，我们向您展示了如何使用`tar`和`dump`等工具从执行备份过程的同一系统上备份到磁带和文件。这些程序（`tar`和`dump`）也能够通过网络进行备份。要能够通过网络备份，您必须确保系统中已安装名为`rmt`和`rsh`的软件包。`rmt`工具为`dump`和`tar`等程序提供对磁带设备的远程访问。作为补充，`rsh`软件包包含一组允许用户在远程机器上运行命令、登录到其他机器以及在机器之间复制文件的程序（`rsh`、`rlogin`和`rcp`就是这组程序）。

由于`rsh`容易被黑客攻击，而`rmt`依赖于`rsh`才能工作，出于安全原因，我们选择不在安装设置中安装它们（更多信息请参见第 2 章"Linux 服务器的安装"）。因此，我们必须找到另一种以安全方式通过网络进行备份的方法。SSH 技术是我们问题的解决方案（参见第 11 章，安全软件和网络安全），因为它还具有通过其`scp`命令加密复制跨网络数据的能力。以下是一种允许我们使用 SSH 软件的潜力，通过`scp` SSH 工具以安全方式传输我们用`tar`或`dump`创建的备份的方法。

## 使用`scp` SSH 命令通过网络传输备份

`scp`命令在网络上的主机之间复制文件。它使用 SSH 进行数据传输，使用相同的身份验证，并提供与 SSH 相同的安全性。与`rsh`软件包附带的`rcp`工具不同，`scp`会要求输入密码或口令。在下面的示例中，我们传输一个用`tar`归档程序创建的备份文件；传输用`dump`程序创建的备份文件或磁带的程序是相同的。

- 要使用`scp`将备份磁带或文件复制到远程安全系统，请使用命令：

  ```bash
  [admin@deep /]# scp <本地目录/到/文件位置> <用户@主机:/目录/用于/文件>
  ```

其中`<本地目录/到/文件位置>`是备份文件在本地服务器上的驻留目录，`<用户@主机:/目录/用于/文件>`依次表示远程站点上将持有备份文件的人员的用户名（用户）、您要发送备份文件的远程主机的 hostname（主机），以及您要放置传输的备份文件的该主机的远程目录。

实际示例看起来像这样：

```bash
[admin@deep /]# scp -Cp /backups/deep-01Feb.tar admin@backupserver:/archive/deep/deep-01Feb.tar
```

```text
admin@backupserver's password:

deep-01Feb.tgz | 10479 KB | 154.1 kB/s | ETA: 00:00:00 | 100%
```

**注意：** `C`选项启用压缩以在加密会话上快速传输数据，`p`选项表示应保留源文件的修改和访问时间以及模式。这通常是可取的。重要的是要注意，远程主机上的`dir/for/file`目录（在我们的示例中是`/archive/deep`）必须归您在`scp`命令中指定的`username`所有（在我们的示例中`admin`就是这个用户名），否则您可能会收到类似这样的错误消息：`scp: /archive/deep/deep-01Feb.tar: Permission denied.`

- 要使用`scp`将远程磁带或文件复制到本地系统，请使用命令：

  ```bash
  [admin@deep /]# scp <用户@主机:/目录/用于/文件> <本地目录/到/文件位置>
  ```

其中`<用户@主机:/目录/用于/文件>`依次表示远程站点上持有备份文件的人员的用户名（用户）、您要从中获取备份文件的远程主机的 hostname（主机），以及该主机上备份文件存放的远程目录，`<本地目录/到/文件位置>`是您要将从远程主机获取的备份文件放置在本地系统上的目录。

实际示例看起来像这样：

```bash
[admin@deep /]# scp -Cp admin@backupserver:/archive/deep/deep-01Feb.tar /backups
```

```text
admin@backupserver's password:

deep-01Feb.tgz | 10479 KB | 154.1 kB/s | ETA: 00:00:00 | 100%
```

**注意：** 重要的是要注意，本地主机上的`localdir/to/filelocation`目录（在我们的示例中是`/backups`）必须归您在`scp`命令中指定的`username`所有（在我们的示例中`admin`就是这个用户名），否则您可能会收到类似这样的错误消息：`/backups/deep-01Feb.tar: Permission denied.`

## `tar`和`dump`备份的替代方案

### AMANDA

AMANDA 主页：<http://www.cs.umd.edu/projects/amanda/>

### BRU

BRU 主页：<http://www.bru.com/>

# 第六部分 附录

本部分包含：

- 附录 A. 优化、技巧和管理任务
- 附录 B. 获取请求注释（RFC）

# 附录 A

本部分包含：

## 优化、技巧和管理任务

本节中的一些技巧特定于 Linux 系统。大多数适用于 UNIX 系统。

## 1.0 `du`工具命令

您可以使用`du`工具来估算文件空间使用情况。例如，要以兆字节为单位确定`/var/log/`和`/home/`目录树的大小，请输入以下命令：

```bash
[root@deep /]# du -sh /var/log /home
3.5M    /var/log
350M    /home
```

请记住，上述命令将报告数据的实际大小。现在，例如，您知道`/home`使用了 350M，您可以进入其中并使用`du -sh *`来定位最大的文件在哪里。

```bash
[root@deep /]# cd /home/
[root@deep /home]# du -sh *
343M    admin
11k    ftp
6.8M    httpd
12k    lost+found
6.0k    named
6.0k    smbclient
6.0k    test
8.0k    www
```

**注意：** 您可以将此命令添加到`crontab`中，这样每天您都会收到所需的磁盘空间列表电子邮件，而无需不断登录即可监控它。

## 1.1 查找从您的机器发送到远程主机的数据包路由

如果您想查找从您的机器发送到远程主机的数据包的路由，只需发出以下命令：



```bash
[root@deep /]# traceroute www.redhat.com
traceroute to www.portal.redhat.com (206.132.41.202), 30 hops max, 38 byte packets
 1  ppp005.108-253-207.mtl.mt.videotron.net (207.253.108.5) 98.584 ms 1519.806 ms 109.911 ms
 2  fa5-1-0.rb02-plex.videotron.net (207.96.135.1) 149.888 ms 89.830 ms 109.914 ms
 3  ia-tlpt-bb01-fec1.videotron.net (207.253.253.53) 149.896 ms 99.873 ms 139.930 ms
 4  ia-cduc-bb02-ge2-0.videotron.net (207.253.253.61) 99.897 ms 169.863 ms 329.926 ms
 5  if-4-1.core1.Montreal.Teleglobe.net (207.45.204.5) 409.895 ms 1469.882 ms 109.902 ms
 6  if-1-1.core1.NewYork.Teleglobe.net (207.45.223.109) 189.920 ms 139.852 ms 109.939 ms
 7  206.132.150.133 (206.132.150.133) 99.902 ms 99.724 ms 119.914 ms
 8  pos1-0-2488M.wr2.CLE1.gblx.net (206.132.111.89) 189.899 ms 129.873 ms 129.934 ms
 9  pos8-0-2488m.wr2.kcy1.globalcenter.net (206.132.111.82) 169.890 ms 179.884 ms 169.933 ms
10  206.132.114.77 (206.132.114.77) 199.890 ms 179.771 ms 169.928 ms
11  pos8-0-2488M.wr2.SFO1.gblx.net (206.132.110.110) 159.909 ms 199.959 ms 179.837 ms
12  pos1-0-2488M.cr1.SNV2.gblx.net (208.48.118.118) 179.885 ms 309.855 ms 299.937 ms
13  pos0-0-0-155M.hr2.SNV2.gblx.net (206.132.151.46) 329.905 ms 179.843 ms 169.936 ms
14  206.132. Bloom 41.202 (206.132.41.202) 2229.906 ms 199.752 ms 309.927 ms
```

其中`www.redhat.com`是您要追踪的主机名称或 IP 地址。

## 1.2 显示网页被访问的次数

要快速显示网页被访问的次数，请使用以下命令：

```bash
[root@deep /]# grep "GET / HTTP" /var/log/httpd/access_log | wc -l
    467
```

## 1.3 同时关闭大多数服务

以 root 身份，您可以使用以下命令同时关闭大多数服务：

```bash
[root@deep /]# killall httpd smbd nmbd slapd named
```

上述命令将分别关闭 Apache 服务器、Samba 服务、LDAP 服务器和 DNS 服务器。

## 1.4 想在所有用户的终端顶部显示时钟？

编辑配置文件（`vi /etc/profile`）并添加以下行：

```bash
PROMPT_COMMAND='echo -ne
"\0337\033[2;999r\033[1;1H\033[00;44m\033[K"`date`"\033[00m\0338"'
```

结果将如下所示：

![](img/a3204f208d115df8d5f69e88ecf1a4ea_476_0.png)

## 1.5 您的服务器上安装了 `lsof` 吗？

如果没有，请安装它并执行`lsof -i`。这将列出您计算机上开放的端口。`lsof`程序是一个很棒的工具，因为它会告诉您哪些进程正在给定端口上监听。

```text
[root@deep /]# lsof -i
COMMAND   PID  USER  FD  TYPE DEVICE SIZE NODE NAME
inetd     344  root  4u  IPv4  327      TCP  *:ssh (LISTEN)
sendmail  389  root  4u  IPv4  387      TCP  *:smtp (LISTEN)
smbd      450  root  5u  IPv4  452      TCP  deep.openna.com:netbios-ssn (LISTEN)
nmbd      461  root  5u  IPv4  463      UDP  *:netbios-ns
nmbd      461  root  6u  IPv4  465      UDP  *:netbios-dgm
```

| COMMAND | PID | USER | FD | TYPE | DEVICE | SIZE | NODE | NAME |
|---|---:|---|---|---|---:|---|---|---|
| nmbd | 461 | root | 8u | IPv4 | 468 | UDP | deep.openna.com:netbios-ns |
| nmbd | 461 | root | 9u | Representative: | 470 | UDP | deep.openna.com:netbios-dgm |
| named | 2599 | root | 20u | IPv4 | 3091 | UDP | localhost.localdomain:domain |
| named | 2599 | root | 21u | IPv4 | 309 | Job-**накуб域 | localhost.localdomain:domain (LISTEN) |
| named | 2599 | root | 22u | IPv4 | 3093 | UDP | deep.openna.com:domain |
| named | 2599 | root | 23u | IPv4 | 3094 | TCP | deep.openna.com:domain (LISTEN) |

## 1.6 通过 SSH 协议在不登录的情况下在远程服务器上运行命令

`ssh`命令还可以用于在不登录的情况下在远程系统上运行命令。命令的输出会显示出来，控制权返回到本地系统。以下是一个示例，它将显示登录到远程系统的所有用户。

```bash
[admin@deep /]$ ssh mail.openna.com who
admin@mail.openna.com's password:
root tty1 Dec 2 14:45
admin tty2 Dec 2 14:45
wahib pts/0 Dec 2 11:38
```

## 1.7 文件名补全

Tab 文件名补全允许您输入文件名或程序的一部分，然后按`[TAB]`，它会为您补全文件名。如果有多个文件或程序以您已输入的内容开头，它会发出蜂鸣声，然后当您再次按`[TAB]`时，它会列出所有以您最初输入内容开头的文件。

## 1.8 特殊字符

您可以使用快捷键来快速完成经常执行的任务——快捷键是您按下一个或多个键来完成任务。例如，特殊字符可以在 Linux shell 中如下使用：

- `Control-d`：如果您在 shell 中按 control-d，您将退出登录。
- `Control-l`：如果您在 shell 中按 control-l，您将清除屏幕。
- `?`：这是通配符。它可以代表单个字符。如果您在命令行中指定类似`m?b`的内容，Linux 会查找 mob、mib、mub 以及 a-z、0-9 之间的每个其他字母/数字。
- `*`：这可以代表任意数量的字符。如果您指定`mi*`，它将使用`mit`、mim、miiii、miya 以及任何以`mi`开头的内容。`m*l`可以是 mill、mull、ml 以及任何以`m`开头并以`l`结尾的内容。
- `[]`：指定范围。如果我输入`m[o,u,i]m`，Linux 会认为：mim、mum、mom。如果我输入`m[a-d]m`，Linux 会认为：mam、mbm、mcm、mdm。明白了吗？`[]`、`?`和`*`通常与复制、删除和目录列表一起使用。

**注意：**Linux 中的**一切**都是区分大小写的。这意味着`Bill`和`bill`不是同一回事。这使得可以存储更多文件，因为`Bill`、`bill`、`bIll`、`biLl`等可以是不同的文件。所以，在使用`[]`时，如果处理的任何文件包含大写字母，您必须指定大写字母。不过，UNIX 中的大部分内容都是小写的。

# 附录 B

## 在本部分中

## 获取征求意见文档（RFCs）

征求意见文档（RFCs）是由互联网工程任务组（IETF）在网络信息中心（NIC）发布的一系列持续更新的文档，介绍了新的协议并为互联网协议套件建立了标准。每份这样的文档定义了与互联网相关的协议的一个方面。我们在下面列出了与本本书以及本书中描述的各种软件相关的所有 RFC。RFC 可从以下站点获取：[http://www.cis.ohio-state.edu/rfc/](http://www.cis.ohio-state.edu/rfc/)

- **RFC706**：关于垃圾邮件问题。
- **RFC733**：ARPA 网络文本消息格式标准。
- **RFC768**：用户数据报协议（UDP）。
- **RFC791**：互联网协议（IP）。
- **RFC792**：互联网控制消息协议（ICMP）。
- **RFC793**：传输控制协议（TCP）。
- **RFC805**：计算机邮件会议记录。
- **RFC821**：简单邮件传输协议（SMTP）。
- **RFC822**：ARPA 互联网文本消息格式标准。
- **RFC934**：消息封装建议标准。
- **RFC950**：IP 子网扩展。
- **RFC959**：文件传输协议（FTP）。
- **RFC976**：UUCP 邮件交换格式标准。
- **RFC1034**：域名：概念和设施。
- **RFC1036**：USENET 消息交换标准。
- **RFC1058**：路由信息协议（RIP）。
- **RFC1112**：互联网组多播协议（IGMP）。
- **RFC1122**：互联网主机需求——通信层。
- **RFC1123**：互联网主机需求——应用和支持。
- **RFC1137**：完整 RFC 822 与受限编码 RFC 822 之间的映射。
- **RFC1153**：摘要消息格式。
- **RFC1155**：管理信息结构（SMI）。
- **RFC1157**：简单网络管理协议（SNMP）。
- **RFC1176**：交互式邮件访问协议：版本 2。
- **RFC1274**：COSINE 和互联网 X.500 模式。
- **RFC1275**：使用 X.500 提供互联网目录的复制需求。
- **RFC1279**：X.500 和域名。
- **RFC1308**：使用 X.500 协议的目录服务执行简介。
- **RFC1309**：使用 X.500 协议的目录服务技术概述。
- **RFC1310**：互联网标准制定过程。
- **RFC1319**：MD2 消息摘要算法。
- **RFC1320**：MD4 消息摘要算法。
- **RFC1321**：MD5 消息摘要算法。
- **RFC1343**：多媒体邮件格式信息的用户代理配置机制。
- **RFC1344**：MIME 对互联网邮件网关的影响。
- **RFC1345**：字符助记符和字符集。
- **RFC1421**：互联网电子邮件隐私增强：第一部分——消息加密和认证程序。
- **RFC1422**：互联网电子邮件隐私增强：第二部分——基于证书的密钥管理。
- **RFC1423**：互联网电子邮件隐私增强：第三部分——算法、模式和标识符 [草案]。
- **RFC1428**：互联网邮件从 Just-Send-8 到 8bit-SMTP/MIME 的传输。
- **RFC1430**：部署互联网 X.500 目录服务的战略计划。
- **RFC1492**：访问控制协议，有时称为 TACACS。
- **RFC1495**：X.400(1988)/ISO 10021 与 RFC 822 之间的映射。
- **RFC1496**：X.400 1988 到 1984 降级。
- **RFC1505**：互联网消息的编码头字段。
- **RFC1510**：Kerberos 网络认证服务（V5）。
- **RFC1519**：无类别域间路由（CIDR）分配和聚合策略。
- **RFC1521**：MIME（多用途互联网邮件扩展）：指定和描述互联网消息主体格式的机制。
- **RFC1522**：互联网消息头中的非 ASCII 文本表示。
- **RFC1558**：LDAP 搜索过滤器的字符串表示法。
- **RFC1566**：邮件监控 MIB。
- **RFC1579**：防火墙友好型 FTP。
- **RFC1583**：开放式最短路径优先路由 V2（OSPF2）。
- **RFC1617**：X.500 目录试点的命名和结构指南。
- **RFC1625**：基于 Z39.50-1988 的 WAIS。
- **RFC1631**：IP 网络地址转换器（NAT）。
- **RFC1652**：用于 8 位 MIME 传输的 SMTP 服务扩展。
- **RFC1661**：点对点协议（PPP）。
- **RFC1711**：电子邮件路由中的分类。
- **RFC1725**：邮局协议，版本 3（POP3）。
- **RFC1738**：统一资源定位符（URL）。
- **RFC1739**：Internet 和 TCP/IP 工具入门。
- **RFC1777**：轻量级目录访问协议。
- **RFC1778**：标准属性语法的字符串表示。
- **RFC1779**：可分辨名称的字符串表示。
- **RFC1781**：使用 OSI 目录实现用户友好命名。
- **RFC1796**：并非所有 RFC 都是标准。
- **RFC1798**：无连接轻量级目录访问协议。
- **RFC1823**：LDAP 应用程序接口。
- **RFC1830**：用于传输大型和二进制 MIME 消息的 SMTP 服务扩展。
- **RFC1844**：多媒体电子邮件（MIME）用户代理检查清单。
- **RFC1845**：用于检查点/重启的 SMTP 服务扩展。
- **RFC1846**：SMTP 521 回复代码。
- **RFC1854**：用于命令流水线的 SMTP 服务扩展。
- **RFC1855**：网络礼仪指南。
- **RFC1864**：Content-MD5 标头。
- **RFC1866**：超文本标记语言 - 2.0。
- **RFC1869**：SMTP 服务扩展。
- **RFC1870**：用于消息大小声明的 SMTP 服务扩展。
- **RFC1872**：MIME 多部分/相关内容类型。
- **RFC1873**：Message/External-Body Content-ID 访问类型。
- **RFC1883**：互联网协议，版本 6（IPv6）规范。
- **RFC1884**：IP 版本 6 寻址体系结构。
- **RFC1886**：支持 IP 版本 6 的 DNS 扩展。
- **RFC1891**：用于投递状态通知的 SMTP 服务扩展。
- **RFC1892**：用于报告邮件系统管理消息的多部分/报告内容类型。
- **RFC1893**：增强型邮件系统状态代码。
- **RFC1894**：投递状态通知的可扩展消息格式。
- **RFC1918**：私有互联网的地址分配。
- **RFC1928**：SOCKS 协议版本 5。
- **RFC1929**：SOCKS V5 的用户名/密码认证。
- **RFC1959**：LDAP URL 格式。
- **RFC1960**：LDAP 搜索筛选器的字符串表示。
- **RFC1961**：SOCKS 版本 5 的 GSS-API 认证方法。
- **RFC2003**：IP 内的 IP 封装。
- **RFC2028**：IETF 标准流程中涉及的组织。
- **RFC2044**：UTF-8，Unicode 和 ISO 10646 的转换格式。
- **RFC2060**：Internet 邮件访问协议 – 版本 4rev1（IMAP4）。
- **RFC2104**：HMAC：用于消息认证的键控散列。
- **RFC2138**：远程认证拨号用户服务（RADIUS）。
- **RFC2164**：使用 X.500/LDAP 目录支持 MIXER 地址映射。
- **RFC2200**：Internet 官方协议标准。
- **RFC2218**：Internet 白页服务通用模式。



- `RFC2247` 在 LDAP/X.500 可分辨名称中使用域。
- `RFC2251` 轻量级目录访问协议（v3）。
- `RFC2252` 轻量级目录访问协议（v3）：属性语法定义。
- `RFC2253` 轻量级目录访问协议（v3）：可分辨名称的 UTF-8 字符串表示。
- `RFC2254` LDAP 搜索筛选器的字符串表示。
- `RFC2255` LDAP URL 格式。
- `RFC2256` 用于 LDAPv3 的 X.500(96) 用户模式摘要。
- `RFC2279` UTF-8，ISO 10646 的转换格式。
- `RFC2293` 在 X.500 目录中表示表格和子树。
- `RFC2294` 在 X.500 目录信息树中表示 O/R 地址层次结构。
- `RFC2305` 使用 Internet 邮件的简单传真模式。
- `RFC2307` 使用 LDAP 作为网络信息服务的方法。
- `RFC2313` PKCS 1：RSA 加密版本 1-5。
- `RFC2314` PKCS 10：认证请求语法版本 1-5。
- `RFC2315` PKCS 7：加密消息语法版本 1-5。
- `RFC2377` 支持 Internet 目录的应用程序的命名计划。
