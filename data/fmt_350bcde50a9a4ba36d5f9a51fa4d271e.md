
# 目录

- 4.3.9 `Optcd` 驱动程序 ... 897
- 4.3.10 `Sjcd` 驱动程序 ... 897
- 4.3.11 `Bpcd` 驱动程序 ... 898
- 4.3.12 SCSI 驱动程序 ... 898
- 4.3.13 `IDECD` 驱动程序 ... 899
- 4.4 启动 Linux 内核 ... 899
- 4.5 挂载、卸载和弹出设备 ... 899
- 4.6 故障排除 ... 900
- 4.6.1 第1 步：确保你运行的是你编译的内核 ... 900
- 4.6.2 第2 步：确保编译了正确的内核驱动程序 ... 901
- 4.6.3 第3 步：内核在启动过程中检测到了你的驱动器？ ... 901
- 4.6.4 第4 步：你能从驱动器中读取数据吗？ ... 902
- 4.6.5 第5 步：你能挂载该驱动器吗？ ... 902
- 4.6.6 调试音频问题 ... 903
- 4.6.7 当其他方法都失败时 ... 903

# 5 应用

- 5.1 音频 CD 播放器 ... 903
- 5.2 `PhotoCD` ... 904
- 5.3 `Mkisofs` ... 904
- 5.4 ISO-9660 工具程序 ... 905

# 6 常见问题解答

- 6.1 非 root 用户如何挂载和卸载光盘？ ... 905
- 6.2 为什么我在卸载 CD-ROM 时会遇到“设备忙”错误？ ... 905
- 6.3 我如何通过 NFS 将 CD-ROM 导出到其他主机？ ... 905
- 6.4 我能从 CD-ROM 启动 Linux 吗？ ... 906
- 6.5 我如何从音频 CD 中读取数字数据？ ... 906
- 6.6 为什么 `find` 命令无法正常工作？ ... 906
- 6.7 Linux 支持任何可刻录 CD-ROM 驱动器吗？ ... 906
- 6.8 为什么我在挂载 CD-ROM 时会收到“mount: 只读文件系统”错误？ ... 906
- 6.9 为什么我关机系统时光盘托会自动打开？ ... 906
- 6.10 我有一张无法挂载的“特殊”CD 怎么办？ ... 907
- 6.11 多盘 CD-ROM 驱动器在 Linux 下运行正常吗？ ... 907
- 6.12 我遇到了 `/cdrom: Permission denied` 错误 ... 907
- 6.13 我如何解读 IDE CD 内核错误信息？ ... 909
- 6.14 我如何告诉系统我拥有的是种速度的 CD-ROM？ ... 909

- 6.15 安装 Linux 后，我的 CD-ROM 停止工作了 . . . . . . . . . . . . . . . . . . 909
- 6.16 CD 盘上有一些无法读取的“隐藏”文件 . . . . . . . . . . . . . . . . . . 910
- 6.17 CD-ROM API 的文档在哪里？. . . . . . . . . . . . . . . . . . . . . 910
- 6.18 为什么我在这张 Windows CD-ROM 上看不到文件名？. . . . . . . . 910
- 6.19 是否支持微软的 Joliet 文件系统？. . . . . . . . . . . . . . . . . 910

## 7 参考文献 910

## 引言

这是 Linux CD-ROM HOWTO。它旨在作为一个快速参考指南，涵盖了在 Linux 下安装和配置 CD-ROM 硬件所需的所需的所有知识。本文回答了与 CD-ROM 相关的常见问题，并提供了与其他 CD-ROM 应用和技术相关的来源引用。

### 1.1 致谢

此处的大部分信息来自 Linux 内核提供的文档和源文件、Internet alt.cdrom `<news:alt.cdrom>` 新闻组 FAQ，以及 Linux 用户的输入。

感谢 SGML Tools `<ftp://site.unc.edu/pub/Linux/utils/text/sgml-tools-0.99.0.tar.gz>` 软件包，本 HOWTO 以多种格式提供，这些均从一个公共源文件生成。

### 1.2 版本历史

版本 1.0
首次发布版本

版本 1.1
从 1.1.20 内核开始显式支持 `CDU33A`；`Reveal FX` 上的节点；关于读取音频轨道的信息；关于某些 alpha 驱动程序的信息；添加了故障排除章节；其他一些新增内容

版本 1.2
从 1.1.33 内核开始，ISO-9660 文件系统必须为只读；澄清了支持 `SB16` SCSI 且不支持 `Aztec` 驱动程序；引用了 `photocd` 和 `xpcd` 程序；关于新 `SBPCD` 弹出功能的注释

版本 1.3
从 1.1.49 内核开始禁用了 `SBPCD` 弹出功能的微调；添加了关于 `XA` 设备以及如何识别它们的信息

版本 1.4
HOWTO 现在提供其他语言；`SBPCD` 现在支持 IBM 和长星驱动器；`Aztec` 驱动器的 alpha 驱动程序；`CD-33` 驱动不再自动引导；支持 `PhotoCD/CD` 音频；支持超过 2 个 SCSI 驱动器；IDE 新驱动程序；记得检查驱动器跳线；现在可以使用 `IOCTL` 设置 `SBPCD` 自动弹出；列出支持多分区的驱动器；关于 `CD-33` 闪光灯的问题

版本 1.5
久违已的更新（我最近很忙）；文档置于 `GPL` 下；关于新内核驱动程序的信息；更多关于配置和故障排除的信息；添加了大量 HTML 链接；许多其他微调

版本 1.6
添加了弹出程序的链接；关于文件权限补丁的问题；Creative Labs 网站的链接；引用 `ATA/EIDE` FAQ 和 FTP 站点；提到 Creative Labs 和美光驱动器现在是 `EIDE`；提到 `Supermount`；列出为支持数字数据的驱动器已过时，参考 `cdda2way`；更多关于刻录 CD 信息；多盘 `EIDE` 驱动器信息：修复了几处

版本 1.7
新内核版本；`README` 文件移动到 `/minora@stna.7/usr/linux/Documentation`；某些驱动不再是实验性的；一些支持的驱动程序；强调大多数驱动现在是 `IDE/ATAPI`；添加了关于即插支持和识别驱动器速度的问题；`vager` 邮件列表关闭；其他杂项更改

版本 1.8
关于为什么安装后 CD-ROM 停止工作的问题；`aztec` 驱动器现在支持两个 `CyCDROM` 驱动器；更多不再建议在 IDE 驱动器上使用 `SBPCD`；某些 `ATAPI` 多盘切换器支持；关于（不支持）并行端口驱动器的注释；最新稳定内核为 2.0；其他杂项更改

版本 1.9
移除了一些非常旧且过时的问题；作者的新邮件地址；提供中文翻译；修复了某些链接以指向最新软件包；更多关于多媒体书籍的信息；细微的拼写和语法错误

版本 1.10
澄清新的 `Aztec` 驱动器是 `ATAPI`；为模块化驱动添加了 `CDU31A` 选项；读取隐藏文件的 `mount` 选项；增加了六个月的“有效期”日期；新的网页 URL；细微的拼写和语法错误

版本 1.11
添加了并行端口驱动器的引用；添加了 `bpcd` 驱动的信息；中文版的新 URL；替代 `CR-56x` 驱动；关于可引导 CD；回答了关于 CD-ROM API 的问题；法语和日语版 Linux 多媒体指南

版本 1.12
添加了波兰语翻译的链接；CD 刻录不再是一个微型 HOWTO；添加了两个与 `Joliet` 文件系统相关

版本 1.13
添加了索引条；置于 `LDP` 许可而非 `GPL`；`SuperProbe` 被引用内核基础自动挂载器取代

### 1.3 本文档的新版本

本文的新版本将定期发布在 comp.os.answers `<comp.os.linux>` 新闻组。它们还将被上传到存档此类信息的匿名 ftp 站点 `<http://sunsite.unc.edu/pub/Linux/HOWTO/`。

此文档及其他 HOWTO 的超文本版本可在 World-Web 上获得。本文的大多数翻译可以在 sunsite.unc.edu/pub/Linux/ 和 `<http://sunsite.unc.edu/pub/Linux/` 找到。如果你将本文翻译成其他语言，请告诉我，我在此引用。

### 1.4 反馈

我依靠读者来让本 HOWTO 有用。如果你有任何建议、修正或意见，请发送给我 tranter@pobox.com，我会尝试整合到下一个版本中。

我也愿意尽可能回答关于 Linux 下 CD-ROM 的问题。在此之前，请阅读 HOWTO 的所有内容，并向我提供详细信息。

如果你以 CD-ROM 或纸质形式出版本文，获赠副本将不胜感激；请告知邮邮地址。也考虑向 Linux 文档项目捐赠以帮助免费文档。

### 1.5 分发策略

（版权所有 1995-1998 Jeff Tracer。）本文可根据 LDP 许可条款 `<http://sunsite.unc.edu/LDP/COPYRIGHT.html>` 分发。

## 2 CD-ROM 技术

"CD-ROM 是只读的，且音频光盘系统可作为这些用途的数字数据软件包介质。播放音频 CD 时请插入耳机接口。"

来自 CD-ROM 说明书

别慌！CD-ROM 技术世界并没有你的说明书写的那么复杂。

CD-ROM 代表光光盘只读存储器，这是一种质量存储介质，利用光学激光读取聚碳酸酯盘上铝层上的微小凹槽。相同的格式也用于音频光盘。

CD-ROM 光盘的存储容量约为 650 兆字节，相当于 500 多张高密度 3.5 英制软盘（称为单速），或大约 25 万页打字稿。

第一代驱动器随后引入了双倍速（300 kB/sec）、四倍速（600 kB/sec）等等。当我写这些时，24 倍速（24X）驱动器已易于获得且价格低廉。

## 3. 支持的硬件

大多数 CD-ROM 驱动器使用小型计算机系统接口 (SCSI)、ATAPI 增强 IDE 或厂商专有的接口。它们通常还通过外部耳机插孔或线路级输出支持音频 CD。某些 CD 还能以数字形式读取音频 CD 的数据帧。

CD-ROM 通常使用 ISO-9660（以前称为 High Sierra）系统进行格式化。该格式将文件名限制为 MS-DOS 风格（8+3 字符）。Rock Ridge 扩展使用 ISO-9660 标准中未定义的字段来支持更长的文件名和 Unix 风格的信息（例如文件所有权、符号链接等）。

PhotoCD 是由达达开发的一项标准，用于将照片图像作为数据存储在 CD-ROM 上。通过适当软件，你可以在计算机上查看图像、对其进行处理或将其发送到打印机。之后可以向 PhotoCD 中添加信息；这被称为多会话能力。

CD 刻录机 (CD-R) 也可用，并且变得越来越廉价。它们使用不同的介质和专用设备进行录制，但生成的光盘可以被任何 CD-ROM 驱动器读取。

预计未来的 CD-ROM 驱动器供应商将提供新技术，将存储容量提高数量级。

本节列出了目前 Linux 下支持的 CD-ROM 驱动程序和接口。此处信息基于最新的稳定 Linux 内核，在编写时该版本为 2.0.33。也提供了开发版内核 (2.1.x 版本)，但不能保证其稳定性。

此信息仅适用于 Intel 平台上的 Linux。其中许多内容可能适用于其他处理器架构上的 Linux，但我没有第一手经验或信息。

### 3.1 ATAPI CD-ROM 驱动器

ATAPI (AT 数据包接口) 是一种用于控制质存储设备的协议。它建立在 ATA (AT 附加) 接口之上，ATA 是为硬盘开发的 IDE 接口的官方 ANSI 标准。ATAPI 常用于硬硬盘、CD-ROM 驱动器、磁带驱动器和其他设备。作为目前最流行的接口类型，它提供了 SCSI 的功能，而不需要昂贵的控制器或电缆。

Linux 内核有一个设备驱动程序，可以与任何符合 ATAPI 标准的 CD-ROM 驱动器配合。提供兼容驱动器的厂商包括 Aztec、Mitsumi、NEC、Sony、Creative Labs 和 Vertos。如果你最近购买了 CD-ROM 驱动器，尤其是四倍速或更快的型号，几乎可以确定它是 IDE/ATAPI 的。

### 3.2 SCSI CD-ROM 驱动器

SCSI (小型计算机系统接口) 是 CD-ROM 驱动器的一种流行格式。其主要优势是传输速度较快、多设备容量以及对各种计算机平台的支持。SCSI 的缺点是控制器卡和电缆相对昂贵。

任何块大小为 512 或 2048 字节的 CD-ROM 驱动器都应该 Linux 下工作；这包括市场上大部分 CD-ROM 驱动器。

你需要一个支持的 SCSI 控制器；请参考 SCSI HOWTO `<http://sunsite.unc.edu/LDPW/HOWTO-SCSI-HOWTO.html>` 获取更多接口硬件信息。

注意，某些 CD-ROM 包含带有修改接口的专用控制器，并不完全兼容 SCSI（例如，它可能不支持在总线上添加其他 SCSI 设备）。这些设备在 Linux 下可能无法工作。

### 3.3 专有 CD-ROM 驱动器

有几种使用专有接口的 CD-ROM 驱动器；这些接口通常提供在声卡上。也有与声卡提供的接口类似的简单接口卡。这些驱动器的成本通常比 SCSI 驱动器便宜且更小。它们的缺点是缺乏标准性和可扩展性。

下表列出了已知在 Linux 下支持的 CD-ROM 驱动器。其他设备的驱动程序可能出现在最新的开发或内核补丁中。后者通常可以在 `<http://sunsite.unc.pub/Linux/kernel/patches/cdrom>` 找到。还要检查内核发行版中的 `README` 文件，通常安装在 `/usr/src/linux/Documentation/cdrom.` 以获取最新信息。

| 厂商 | 型号 | 内核驱动程序 | 备注 |
|---|---|---|---|
| Panasonic | CR-521 | `sbpcd` | 注 1 |
| Panasonic | CR-522 | `sbpcd` | 注 1 |
| Panasonic | CR-523 | `sbpcd` | 注 1 |
| Panasonic | CR-562 | `sbpcd` | 注 1 |
| Panasonic | CR-563 | `sbpcd` | 注 1 |
| Creative Labs | CD-200 | `sbpcd` | |
| IBM | External ISA | `sbpcd` | 注 2 |
| Longshine | LCS-7260 | `sbpcd` | |
| Teac | CD-55A | `sbpcd` | |
| Sony | CDU-31A | `cdu31a` | |
| Sony | CDU-33A | `cdu31a` | |
| Sony | CD-535 | `synocds535` | 注 3 |
| Sony | CDU-531 | `synocds535` | |
| Aztech | CR-268-01A | `atcd` | 注 4 |
| Orchid | CDS-3110 | `atcd` | |
| Okano/Wearnes | CDU110 | `atcd` | |
| Conrad | TXC | `atcd` | |
| CycDROM | CR5020 | `atcd` | |
| CycDROM | CR9410 | `atcd` | |
| GoldStar | R420 | `gscd` | 注 5 |
| Philips/LMS | CM206 | `cm206` | 注 6 |
| Mitsumi | CRMC005 | `mcd/mcd` | 注 7, 8 |
| Mitsumi | FX001 | `mcd/mcd` | 注 7, 8 |
| Optics Storage | Dolphin 8000A | `optcd` | |
| Lasermate | CR328A | `optcd` | |
| Sanyo | H94A | `sjcd` | |
| various | various | `ispi16` | 注 9 |

备注：
- 1. 这些驱动器可能以 Creative Labs、Panasonic、Matsushita 或 Kotobuki 的名销售。
- 2. 此驱动器与 Panasonic-562 相同。
- 3. 可能以 Pro 的名销售。其他型号包括 `CDA268` 和 `CDA269` 是专用的，应使用 IDE (ATAPI) 。
- 4. 此驱动仅用于 `CDA268-01A`。原始版本较新的。
- 5. 可能作为 Multimedia Kit 的一部分销售。
- 6. Philips-205 不受此驱动支持，但可以在 ftp://sunite.edu/pub/linux/kernel/patches/cdrom0.4.tgz 找到单独发布的版本。
- 7. 可能以 Radio Shack 的销售。
- 8. 有两个驱动。“`mcd`”是原始的，“`cds`”是功能更多较新的（可能较不稳定）。
- 9. 这适用于连接到 `ISP16` 或 `Mozart` 声卡的 CD-ROM 驱动器。

如果内核不支持此处列出的驱动器，你可能需要升级到新版本。如果你的驱动器不是列出的型号之一，特别是最近购买且是四倍速或更快，请使用前节提到的 IDE/ATAPI 接口。Linux 用户最常见的错误是假设任何连接到 `SoundBlast` 声卡的驱动都应使用 `SBPCD`。Creative Labs 和大多数其他厂商不再销售专有驱动器，它们遵循标准的 ATAPI/IDE

### 并端口驱动器

某些厂商销售通过并行端口连接的 CD-ROM 驱动器。目前 Linux 内核支持的此类驱动器只有 `MicroSolutions` `Backpack`。这些驱动器的 Linux 内核程序作为内核补丁或加载模块单独提供。最新信息请检查 `<http://www.torque.net/linux-pp.html>`。

### 3.5 替代驱动程序

由 Zoltan Vorosanyi 编写了一个 Panasonic/Matsushita `CR-56` 的替代内核驱动。可以在 ftp://tarki.hu/pub/linux/pcd/pcd-0.29.tgz 找到。

## 4 安装

在 Linux 下安装 `CDROM` 包括以下步骤：
1. 安装硬件。
2. 配置并构建 Linux 内核。
3. 创建设备文件并设置引导。
4. 启动 Linux 内核。
5. 挂载媒体。

后续章节将详细介绍这些步骤。

### 4.1 安装硬件

按照制造商的说明安装硬件，或让经销商进行安装。细节取决于驱动器是内部还是外部以及使用的接口类型。Linux 没有特殊的安装要求。你可能需要在驱动器和/或接口上设置跳线以确保正常运行；某些内核驱动包含此类信息的 `README` 文件。

正如 `ide-ATAPI` 文件解释的，当只连接一个 IDE 设备时，`CD-MS` 应跳线为“single”或“master”，而不是“slave”（尽管最近的内核不再执行此限制）。

### 4.2 配置并构建内核

从 CD-ROM 安装 Linux 时，你可能会使用作为 Linux 发行版一部分提供的启动或根磁盘。如果可能，选择带有你的 CD-ROM 设备内核驱动程序的启动盘。如果你找不到带有所需 CD-ROM 驱动程序的启动盘，你有几种选择：
- 通过网络安装。
- 启动 DOS，并将 Linux 文件安装到硬盘。
- 启动 DOS，创建一组软磁盘来安装 Linux。
- 找一个可以构建所需 CD-ROM 驱动程序启动盘的人。

Linux 安装 HOWTO `<http://sunsite.unc.edu/LDP/HOWTO/Installation-HOWTO.html>` 有更多关于安装 Linux 的信息。如果你是在 CD-ROM 上购买的 Linux，它可能也附带安装说明（盒内的小手册和/或 CD 上的文件）。

最初安装 Linux 后，大多数用户需要编译自己的内核，通常出于以下原因之一：
- 支持 CD-ROM 驱动器或其他硬件
- 升级到较新的内核版本
- 通过最小化内核大小释放内存资源

构建内核的细节应咨询内核 HOWTO `<http://sunsite.unc.edu/LDP/Kernel-HOWTO.html>`。我在这里仅提到一些针对 CD-ROM 驱动器的特定问题。

显然，在执行 "config" 时你需要包含对你的 CD-ROM 驱动器的支持。

如果你有一个 ATAPI CD-ROM 驱动器，你需要回答以下问题：

```
