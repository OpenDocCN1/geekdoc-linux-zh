
用于分发符合 Linux Standard Base 规范的应用程序和整个发行版的包格式。由于 LSB 规范强制要求 RPM 软件包，LSB 软件包是 RPM 软件包的超集。因此，在您的 Ubuntu 系统上必须安装 RPM 软件包管理器以转换 alien 软件包。（在安装 alien 时，会自动安装 RPM 软件，因为它被列为 alien 软件包的依赖项。）如果您正在转换依赖于其他包的 alien 软件包，转换过程将正确翻译这些依赖关系，但也会引入对 lsb 软件包的新依赖，该包在 Ubuntu 软件库中可用。如果您是从 LSB 软件包转换，您还应该安装 `lsb-rpm` 软件包，这是 alien 软件包建议但并非强制要求的。

- `PKG`：Solaris 使用的包格式。将 PKG 文件转换为其他格式需要 Solaris 专用的工具，如 `pkginfo` 和 `pkgtrans`。如果您还从其中一个自由软件光盘中安装了 RPM 软件，那么你就可以在您的 Solaris 系统上使用 alien 将 PKG 软件包转换为 RPM。这可能只对由脚本、源代码或命令文件组成的包有用，因为您无法在 Linux 系统中执行二进制文件。

- `RPM`：Red Hat、Mandrake、Yellow Dog 等发行版使用的包格式。要从 RPM 格式转换软件包，必须在您的 Ubuntu 系统上安装 RPM 软件包管理器（以前称为 Red Hat Package Manager）。在安装 alien 时，会自动安装 RPM 软件，因为它被列为 alien 软件包的依赖项。）

- `SIP`：已废弃的 Stampede Linux 发行版使用的包格式，该发行版已于 2002 年停止开发。我无法相信这个选项仍然受到活跃支持，但由于 Stampede Linux 已经消亡，我不认为它的包格式会有太大变化。

- `TGZ`：大多数开源软件项目和 Slack Linux 发行版使用的软件分发格式。TGZ 文件是使用 `gzip` 压缩工具压缩的 `tar` 归档，创建归档时可以使用命令行或 `tar` 本身进行。压缩的 tar 归档通常简单称为压缩 tar 包（tarballs）。从 TGZ 文件生成的包文件仅包含与压缩 tar 包相同的文件，外加上目标包格式的包数据库信息。

使用 alien 将一种包格式转换为另一种格式是非常简单的。alien 提供了如 `--to-deb`、`--to-lsb`、`--to-rpm` 和 `--to-tgz` 等选项来指定目标输出格式。以下是将 Adobe Acrobat Reader（您可能听说过它）的 RPM 软件包转换为 DEB 格式的示例：

```
$ sudo alien --scripts --to-deb AdobeReader-enu-7.0.0-2.i386.rpm
Password:
adobereader-enu_7.0.0-3_i386.deb generated
```

实际上，这里没什么好读的。`--scripts` 选项告诉 alien 转换包中找到的任何安装或后安装脚本，尽管这些脚本的有效性无法保证——您应该仔细确保在安装软件包时没有出现任何错误。`--to-deb` 选项告诉 alien 从输入包生成 Debian 软件包。如果您想查看详细输出，可以添加 `--to-alien` 命令行，通过它您可能会看到比您实际关心的更多的输出。

在安装转换后的包之前，您可以使用如下例中的 `dpkg` 验证其完整性：

```
$ dpkg --info adobereader-enu_7.0.0-3_i386.deb
debian package, version 2.0.
size 3932742 bytes: control archive= 7436 bytes.
1, 11 lines control
2006 bytes, 207 lines md5sums
1340 bytes, 60 lines * postinst #/bin/sh
980 bytes, 45 lines * postrm #/bin/sh
211 bytes, 7 lines shlibs
Package: adobereader-enu
Version: 7.0.0-3
Section:
Priority: extra
Architecture: i386
Installed-Size: 91916
Maintainer: <root@vmdesktop>
Description: Adobe Reader for Linux. 一个读取 PDF
文档的应用程序。Adobe Reader 7.0.0 可以读取 PDF 格式的文档。
Adobe Reader 还允许您在 PDF 文件中进行搜索，在互联网上搜索 PDF 文件并参与协作文档评审。
(由 alien 版本 8.64 从 rpm 软件包转换。)
```

这与在我另一个系统上产生的原始 RPM 软件包信息非常吻合：

```
$ rpm -q -v -p AdobeReader-enu-7.0.0-2.i386.rpm
Name : AdobeReader_enu Relocations: /usr/local/Adobe/Acrobat7.0
Version : 7.0.0 Vendor: Adobe Systems, Incorporated
Release : 2 Build Date: Mon 28 Mar 2005 06:34:42 AM EST
```

安装日期：（未安装）构建主机：acrolinux2.corp.adobe.com

Group : Applications/Publishing Source RPM: AdobeReader-enu-7.0.0-2.

src.rpm

Size : 97613446 License: Commercial

Signature : (none)

Packager : Adobe Systems, Incorporated

URL : www.adobe.com

Summary : 用于 Linux 的 Adobe Reader。一个读取 PDF

文档的应用程序。

Description: Adobe Reader 7.0.0 可以读取 PDF 格式的文档。

Adobe Reader 还允许您在 PDF 文件中进行搜索，在互联网上搜索 PDF 文件并参与协作文档评审。

Distribution: (none)

# 第 19 章：添加、删除和更新软件

本章剩余部分的重点是 Ubuntu 系统上可用的图形化安装和自动软件更新应用程序（Synaptic 和更新管理器）。本章还讨论了用于识别和安装软件包的安装实用程序，以及如何使用更新实用程序通过在可用时安装安全补丁或现有软件的增强版本来保持您的系统最新状态。

第 20 章“添加硬件和连接外围设备”讨论了如何向您的 Ubuntu 系统添加各种类型的硬件。与大多数现代个人电脑系统一样，Ubuntu 系统在自动识别和访问新打印机、扫描仪以及可移动存储设备（如 USB 闪盘、USB 硬盘、FireWire 设备等）方面表现出色。添加新的内部驱动器需要更多的工作，但它是系统永久性升级的关键要素，并且易于掌握。

# 第 20 章：添加硬件和连接外围设备

对海量硬件的支持是任何台式计算机系统的关键问题。随着计算机硬件变得越来越廉价，台式用户更倾向于向他们的计算机系统添加显卡和外部外围设备，操作系统支持所有这些新硬件的程度变得越来越发重要。越来越多的设备被设计为外部即插即用设备，使用 USB 和 FireWire 等接口可以在当地的 Best、CompUSA 或 Stop-n-Go 商店购买。人们期望购买这些东西带回家后，发现它们“即插即用”。这理所应当。

所有硬件都需要内核软件设备驱动程序以便操作系统能够正确访问和使用。这对于 Microsoft Windows 内核、Mac OS X 内核和 Linux 内核都是如此。几乎每种现代硬件盒子里都掉出一个标有“Windows 驱动程序”的 CD，这一事实可能会让你认为在 Linux 上使用这些硬件会遇到问题。毕竟，并没有一个标有“Linux 驱动程序”的配套垫片。这是为什么？

幸运的是，答案是大多数硬件的设备驱动程序已经作为安装在您的 Ubuntu 系统上的 Linux 内核的一部分。设备驱动程序通常被编译到内核中，或者作为内核模块存在并在检测到特定硬件时加载（因此，按需驱动的通用术语是：可加载内核模块）。这适用于大量的硬件——毕竟，在开源世界里，只需要一个具有驱动开发技能的动力 Linux 用户和一个“工作不正常”的硬件，通常很快就会出现可工作的驱动程序。

## 本章内容

- 添加打印机
- 添加和使用扫描仪
- 添加内部驱动器
- 使用 PCMCIA 卡
- 添加 PCI 卡
- 排除新设备的故障

# 第二部分：面向桌面用户的 Ubuntu
