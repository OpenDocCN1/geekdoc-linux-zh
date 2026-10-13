
`cd /tmp`

`rpmfind xv`

Installing xv will require 943 KBytes

Nonqualified hostname: maple(none)

ftp://ftp.redhat.com/pub/redhat-7.1/powtools/i386/RedHat/RPMS/

`xv-3.10-23.1386.rpm`

Do you want to download these files to ?tmp? [Y/n/a/i] : Y

在你输入 Y 后，软件包将下载到你的当前目录（在本例中为 tmp）。然后你可以使用 `rpm -i /tmp/xv*` 命令安装软件包（请将 `/tmp/xv*` 替换为你要安装的软件包名称）。

# 第5章 访问与运行应用程序

我特别推荐使用 `rpmfind` 命令来获取属于 Red Hat Linux PowerTools 的软件包，这些工具在 Red Hat Linux 7.2 中已停止支持。然而，尽管书中未包含这些软件包，但书中引用了之前的几个 PowerTools 包（例如 `xv`）。

## 理解包名和格式

你刚刚从互联网下载了一个巨大的文件，其中包含许多名称、数字、点、gzs 和 tars。这些内容意味着什么？其实，拆解来看，并不复杂。

大多数包含 Linux 应用程序的归档文件名遵循 GNU 风格命名规范。下面的示例说明了包命名格式：

```
mycoolapp-4.2.3.1386.rpm

mycoolapp-4.2.3.tar.gz

mycoolapp-4.2.3.src.tar.gz

mycoolapp-4.2.3.bin.SPARC.tar.gz

mycoolapp-4.2.3.bin.ELF.static.tar.gz
```

这些示例代表了同一个软件应用程序的几个不同的包。该包的名称是 `mycoolapp`。包名后面是一组代表包版本的数字。在此例中，它是 `4.2.3`（主版本号为 4，后面是次要版本号和补丁级别 2.3）。版本号后面是一个点，紧接着是一些可选部分，最后是关于文件如何归档和压缩的指示。

第一行显示它是 Red Hat Package Manager `.rpm` 格式。`.1386` 表示该包包含为运行 Intel i386 架构计算机（换句话之，PC）构建的二进制文件。请参见侧边栏“RPM 与源码编译”，了解使用预构建的 RPM 二进制包与自己编译的优缺点。

在接下来的两行中，每个文件都包含该包的源代码。组成包的文件使用 `tar` 命令（`.tar`）进行归档，并使用 `gzip` 命令（`.gz`）进行压缩。当你准备好安装应用程序时，可以使用这两个命令来扩展和解压包。

在版本号和 `.tar.gz` 后缀之间可以有由点分隔的可选标签，它们提供了关于包内容的特定信息。特别是，如果该包是二进制版本，这些信息提供了有关二进制文件运行位置的细节。在第三行中，添加了可选的 `.src` 标签以区分该包的源码版本和二进制版本。在第四行中，`.bin.SPARC` 表示它是一个二进制包，准备在 SPARC 工作站上运行。最后一行表示它是二进制包，由静态链接的 ELF 可执行文件组成。

访问 www.unlimited.com 获取额外内容

### RPM 与从源码编译

以 RPM 格式创建的二进制文件可以使用 Red Hat 工具轻松地安装、管理和卸载。这是 Red Hat Linux 初学者的推荐安装方法。然而，有时从源代码构建应用程序可能更合适。以下是支持双方的论点：

- **RPM**——从 RPM 归档中安装应用程序非常简单。如果已安装应用程序，既有命令行也有图形用户界面（GUI）来管理、验证、更新和删除该 RPM 应用程序。你不需要了解任何关于 Makefile 或编译器的知识。当你安装 RPM 包时，RPM 工具甚至会检查该包所依赖的其他包是否已安装。

由于 Red Hat 在 GNU 之下发布了 RPM，其他 Linux 发行版也开始分发自己的软件。因此，大多数 Linux 应用程序已经或将以 RPM 格式提供。

- **源代码**——将源代码转换为 RPM 二进制文件需要一段时间。使用 RPM 时，你可能会发现软件版本已经旧了好几个版本，而此时你本只需下载最新的源码并运行几个 `tar` 和 `make` 命令。此外，通过修改源代码，你可能可以定制应用程序以更好地符合你的需求。

以下是包名部分的拆解：

- **name**（名称）——这通常是一个标识应用程序的全小写字符串。
- **dash**（连字符）——-
- **version**（版本）——从左到右显示为主版本号到次要版本号。
- **dot**（点）——。
- **src or bin**——这是可选的，如果没有指示，通常隐含 src。
- **dot**（点）——。
- **type of binary**（二进制类型）——这是可选的，可以包含多个不同的标签来描述二进制归档的内容。
- **dot**（点）——。
- **archive type**（归档类型）——通常为 tar `.tar`
- **compression type**（压缩类型）——通常为 gzip `.gz`

## 使用不同的格式

你遇到的许多文件将是各种格式。表 5-1 描述了归档格式。表 5-2 列出了一些文档格式。

### 表 5-1 Linux 归档文件

| 格式 | 后缀 | 描述 |
| :--- | :--- | :--- |
| Gzip 文件 | .gz 或 .z | 文件使用 gzip 实用压缩。可以使用 gunzip 解压（它们是同一种）。 |
| Tar 文件 | .tar | 文件使用 tar 归档。Tar 用于将多个文件收集到单个归档中。 |
| Bzip2 | .bz2 | 文件使用 bzip2 程序压缩。 |
| Tar/压缩 | .taz 或 .tz | 文件使用 tar 归档并使用 compress 命令压缩。（compress 命令不是 GNU 的一部分，因为它受专利保护。） |

访问 www.untitled.com 获取额外内容

### 表 5-1（续表）

| 格式 | 后缀 | 描述 |
| :--- | :--- | :--- |
| Linux 软件地图 | .lsm | 文件包含描述归档内容的文本。 |
| Debian 二进制包 | .deb | 文件是用于 Debian 发行版的二进制包。（参见本章稍后关于如何将 Debian 转换为 Red Hat 的描述。） |
| Red Hat 包管理 | .rpm | 文件是用于 Red Hat 发行版的二进制包。该格式也适用于其他 Linux 发行版。 |

### 表 5-2 Linux 文档格式

| 格式 | 后缀 | 描述 |
| :--- | :--- | :--- |
| 超文本标记语言 | .html 或 .htm | 文件为超文本格式，供 Web 浏览器（如 Netscape Communicator）读取。 |
| PostScript | .ps | 文件为 PostScript 格式，用于 PostScript 打印机输出。 |
| SGML | .sgml | 文件为 SGML，一种标准文档格式。SGML 常用于生成以后输出到各种格式的文档。 |
| DVI | .dvi | 文件为 DVI，LaTeX 文本处理工具的输出格式。使用 dvips 和 dvipj 命令将这些文件转换为 PostScript 或惠普 PCL。 |
| 纯文本 | | 无后缀的文件通常是纯文本文件（ASCII 格式）。 |

如果你不确定某个文件的格式，可以使用如下的 `file` 命令：

```
file archive-file
```

该命令会告诉你它是 GNU tar 文件、RPM、gzip 还是其他文件格式。（如果文件被重命名并丢失了后缀，这是一个很好的技巧。）

## 使用 alien 命令转换软件包

如果您有一个以非 RPM 格式提供的可用软件包，并想在您的 Red Hat Linux 系统上使用它，那么您可能可以使用 `alien` 命令将该包转换为 RPM 格式。`alien` 命令允许您将包从 Debian `.deb`、Stampede `.slp`、Slackware `.slp` 或 Red Hat 软件包管理 `.rpm` 转换为上述任何一种其他格式。

将包从其他格式转换为 RPM 的优势是，您随后可以使用各种 RPM 工具来管理该包。例如，我从 Debian FTP 站点（http://ftp.us.debian.org）下载了 `bsdgames` 包。然后，我按照如下方式将该 deb 格式的包转换为 RPM 格式：

```
alien --to-rpm bsdgames_2.9-3.deb
```

在这种情况下，根据 Debian 包创建了一个 RPM 文件。新文件名为 `bsdgames-2.9-4.1386.rpm`。创建完成后，我可以像安装任何 RPM 文件一样安装它：

```
rpm -i bsdgames-2.9-4.1386.rpm
```
