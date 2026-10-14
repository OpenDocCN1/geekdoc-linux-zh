
# 第 19 章：添加、删除和更新软件

一旦您选择了任何想要与所选的主软件包一起安装的建议软件包，请点击 Synaptic 工具栏中的“应用（Apply）”以开始实际安装过程。这将显示图 19-21 所示的对话框，该框总结了与安装所选软件包相关的所有活动。

下载过程完成后，Synaptic 开始安装和配置下载的软件包。如果您没有在 Synaptic 的“偏好”对话框中的“在终端窗口中（Terminal）”项中选择“应用更改（Apply changes）”，Synaptic 将显示一个简单的状态对话框，如图 19-23 所示。

## 图 19-21

Synaptic 中的软件包安装摘要

![](img/1a233c34336fbf5a85d6eb785e401709_748_0.png)

## 图 19-22

Synaptic 软件包安装期间的下载状态对话框

![](img/1a233c34336fbf5a85d6eb785e401709_748_1.png)

## 图 19-23

Synaptic 中简单的安装和配置状态对话框

![](img/1a233c34336fbf5a85d6eb785e401709_748_2.png)

## 第二部分：面向桌面用户的 Ubuntu

通过点击此对话框中“终端（Terminal）”选项右侧的箭头，您可以显示一个小型终端窗口，列出 Synaptic 安装和配置过程的状态。当您的软件包安装和配置完成后，将显示图 19-24 所示的对话框。

### 提示

在使用 Synaptic 工具安装软件时，如果没有配置 Synaptic 始终在终端窗口中显示配置状态，那么显示一个终端以查看有关系统软件安装状态的信息是有用的。在安装过程中，您可能偶尔需要显示额外的与配置相关的信息。在这种情况下，Synaptic 工具将显示类似于 `apt` 和 `aptitude` 工具所示某些信息请求，如前图 19-8 所示。每当您看到此屏幕时，都必须回答它提出的任何问题并提供任何所需的信息。

### 第 19 章：添加、删除和更新软件

- LSB：用于分发符合 Linux Standard Base (LSB) 规范的应用程序和整个发行版的包格式（`www.linuxfoundation.org/collaborate/workgroups/lsb`）。由于 LSB 规范强制要求 RPM 软件包，因此 LSB 软件包是 RPM 软件包的超集。因此，在您的 Ubuntu 系统上必须安装 RPM 软件包管理器以转换 `alien` 软件包。（在安装 `alien` 时，会自动安装 RPM 软件，因为它被列为 `alien` 软件包的依赖项。）如果您正在转换依赖于其他包的 `alien` 软件包，转换过程将正确翻译这些依赖关系，但也会引入对 `lsb` 软件包的新依赖，该包在 Ubuntu 软件库中可用。如果您是从 LSB 软件包转换，您还应该安装 `lsb-rpm` 软件包，这是 `alien` 软件包建议但并非强制要求的。

- PKG：Solaris 使用的包格式。将 PKG 文件转换为其他格式需要 Solaris 专用的工具，如 `pkginfo` 和 `pkgtrans`。如果您还从其中一个自由软件光盘中安装了 RPM 软件，那么你就可以在您的 Solaris 系统上使用 `alien` 将 PKG 软件包转换为 RPM。这可能只对由脚本、源代码或命令文件组成的包有用，因为您无法在 Linux 系统中执行二进制文件。

- RPM：Red Hat、Mandrake、Yellow Dog 等发行版使用的包格式。要从 RPM 格式转换软件包，必须在您的 Ubuntu 系统上安装 RPM 软件包管理器（以前称为 Red Hat Package Manager）。在安装 `alien` 时，会自动安装 RPM 软件，因为它被列为 `alien` 软件包的依赖项。）

- SIP：已废弃的 Stampede Linux 发行版使用的包格式，该发行版已于 2002 年停止开发。我无法相信这个选项仍然受到活跃支持，但由于 Stampede Linux 已经消亡，我不认为它的包格式会有太大变化。

- TGZ：大多数开源软件项目和 Slack Linux 发行版使用的软件分发格式。TGZ 文件是使用 `gzip` 压缩工具压缩的 `tar` 归档，创建归档时可以使用命令行或 `tar` 本身进行。压缩的 tar 归档通常简单称为压缩 tar 包（tarballs）。从 TGZ 文件生成的包文件仅包含与压缩 tar 包相同的文件，外加上目标包格式的包数据库信息。

使用 `alien` 将一种包格式转换为另一种格式是非常简单的。`alien` 提供了如 `--to-deb`、`--to-lsb`、`--to-rpm` 和 `--to-tgz` 等选项来指定目标输出格式。以下是将 Adobe Acrobat Reader（您可能听说过它）的 RPM 软件包转换为 DEB 格式的示例：

```
$ sudo alien --scripts --to-deb AdobeReader-enu-7.0.0-2.i386.rpm
Password:
adobereader-enu_7.0.0-3_i386.deb generated
```

实际上，这里没什么好读的。`--scripts` 选项告诉 `alien` 转换包中找到的任何安装或后安装脚本，尽管这些脚本的有效性无法保证——您应该仔细确保在安装软件包时没有出现任何错误。`--to-deb` 选项告诉 `alien` 从输入包生成 Debian 软件包。如果您想查看详细输出，可以添加 `--to-alien` 命令行，通过它您可能会看到比您实际关心的更多的输出。

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

URL : `www.adobe.com`

Summary : 用于 Linux 的 Adobe Reader。一个读取 PDF

文档的应用程序。

Description: Adobe Reader 7.0.0 可以读取 PDF 格式的文档。

Adobe Reader 还允许您在 PDF 文件中进行搜索，在互联网上搜索 PDF 文件并参与协作文档评审。

Distribution: (none)
