
在版本号和 `.tar.gz` 扩展之间可以有点分隔的可选标签，这些标签提供了软件包内容的特定信息。特别是，如果软件包是二进制版本，这些信息提供了有关二进制文件运行位置细节。在第三行中，添加可选的 `.src` 标签是因为开发者想要区分此软件包的源码和二进制版本。在第四行中，`.bin SPARC` 表示这是一个二进制包，可以在 SPARC 工作站上运行。最后一行表示这是一个二进制包，由静态链接的 ELF 格式可执行文件组成。

如今，许多软件打包者不再使用 gzip，而是使用 bzip2 工具来压缩软件归档。在这种情况下，上述示例中显示的文件可能以 `.bz2` 或 `.tar.bz` 结尾。

以下是软件包名称部分的拆解：

- `name` — 这通常是一个标识应用程序的全小写字符字符串。
- `dash (-)`
- `version` — 这从左到右显示为主版本到次要版本号。
- `dot (.)`
- `src or` — — 这是可选的，如果没有给出指示，通常隐含为 `src`。
- `dot (.)`
- `type of binary` — 这是可选的，可以包含几个不同的标签来描述二进制归档的内容。例如，`i386` 表示用于 Intel 架构（奔腾 CPU）的二进制文件，`SPARC` 表示用于 Sparc CPU 的二进制文件。
- `dot (.)`
- `archive type` — 通常使用 `tar` (`.tar`)。
- `compression type` — 通常使用 `gzip` (`.gz`)。

## 使用不同的归档和文档格式

许多不与特定发行版（如 Fedora 或 Debian）关联的软件软件包使用 `.tar/gz` 方法进行文件的归档和压缩。然而，你可能会在软件项目网站看到具有不同后缀的文件。

表 5-1 描述了你在 Linux FTP 站点寻找软件时会遇到的文件格式。表 5-2 列出了在 Linux 分发信息时常用的一些文档格式。

### 表 5-1：Linux 归档文件格式

| 格式 | 扩展名 | 描述 |
| :--- | :--- | :--- |
| Gzip 文件 | `.gz` 或 `.z` | 文件使用 GNU `gzip` 工具压缩。可以使用 `gzip` 或 `gunzip` 工具解压缩（它们是相同的）。 |
| Tar 文件 | `.tar` | 文件使用 `tar` 命令归档。`tar` 用于将多个文件收集到单个归档中。你可以使用带有不同选项的 `tar` 将归档扩展为单独的文件。 |
| Tar 和 Gzip 文件 | `.tgz` | 命名使用 `gzip` 压缩的归档文件的常用做法是使用 `tgz` 扩展名。 |
| Bzip2 | `.bz2` | 文件使用 `bzip2` 程序压缩。 |
| Tar/压缩 | `.tar` 或 `.tz` | 文件使用 `tar` 归档并使用 UNIX 命令 `compress`。 |
| Linux 软件映射 | `.lsm` | 文件包含描述归档内容的文本。 |
| Debian 二进制包 | `.deb` | 文件是一个二进制包。 |
| RPM 管理 | `.rpm` | 文件是一个二进制包。 |

# 第二部分：使用 Fedora 和 RHEL

- `glibc` — 包含重要的共享库、C 库以及标准数学库。
- `glibc-devel` — 包含创建可执行文件时所需的标准头文件。
- `binutils` — 包含编译程序所需的工具（如汇编器和链接器）。
- `kernel-devel` — 包含 Linux 内核源代码，在重新构建内核时需要用到。
- `rpm-build` — 包含 `rpmbuild` 工具，用于从源码构建 RPM 二进制软件包。
- `libc` — 包含用于基于 `libc 5` 的程序的库，旧版应用程序可以在运行 `glibc` (`libc 6`) 的系统上。

## 安装 SRPM 格式的软件

要从 Fedora 源码目录安装软件包，请执行以下操作：

1. 请参阅附录 A 获取有关获取 Fedora 源码的信息。
2. 将您需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```bash
# rpm -iv packagename*.src.rpm
```

（将 `packagename` 替换为您正在安装的包名。）源码被安装在 Fedora 源码树 (`/usr/src/redhat/SOURCES`) 中。Spec 文件被复制到 `/usr/src/redhat/SPECS`。

4. 如下切换到 SPECS 目录：

```bash
# cd /usr/src/redhat/SPECS
```

5. 按照如下方式解压源码：

```bash
# rpmbuild -bp packagename*.spec
```

6. 软件包的源码被安装到 `/usr/src/redhat/BUILD/package` 目录，其中 `package` 是软件包的名称。
7. 现在您可以修改软件包 BUILD 目录中的文件了。请阅读 `README`、`Makefile` 和其他文档文件以获取如何构建单个软件包的详情。

- `-- rpmbuild` 选项用于在不先安装的情况下重新构建 rpm。生成的二进制文件将位于 `/usr/src/redhat/RPMS/arch`，其中 `arch` 被替换为 `i386` 或您正在构建 RPM 的其他架构。

# 第 5 章：访问和运行应用程序

## 安装 tar.gz 或 tar.bz2 格式的软件

以下是通用说明，可以使用它们安装许多 gzip 格式或 tar 格式的 Linux 软件包：

1. 从互联网或 CD 分发版获取源码包，并将其复制到空目录（最好使用能识别该包的名称）。
2. 在将 tar 归档提取到硬盘之前，可以使用以下命令检查 tar 归档的内容：

```bash
# tar tvf package.tar.gz
```

3. 假设文件使用 gzip 压缩的，使用以下命令解压文件：

```bash
# gunzip package.tar.gz
```

结果是软件包已解压缩，且包名中删除了 `.gz`（例如，`package.tar`）。（如果您的包以 `bz2` 结尾，请使用 `bzip2` 命令代替上述的 `gzip`。）

4. 对于生成的 tar 归档，按如下方式运行 `tar` 命令：

```bash
# tar xvf package.tar
```

此命令从归档中提取文件并将它们复制到当前目录的子目录。（使用 `tar xvfz package.tar.gz` 可以在一个步骤中完成步骤 2 和 3。对于压缩的 bzip2 文件，请运行 `tar xvfj package.tar.bz2`。）

5. 按照如下方式切换到步骤 3 创建的新子目录：

```bash
# cd package
```

6. 寻找名为 `INSTALL` 或 `README` 的文件。其中一个文件应该会提供有关如何继续安装的说明。通常使用 `make` 命令来安装软件包。以下是当前目录中需要查找的几项：

如果存在 `Make.in` 文件，尝试运行：

```bash
# ./configure -prefix=/usr/local
# make all
```

如果存在 `Imake` 文件，尝试运行：

```bash
# make all
```

如果存在 `Makefile` 文件，尝试运行：

```bash
# make all
```

## 寻找 Linux 中常见的桌面应用程序

如果你将 Linux 作为桌面计算机系统使用，你必须能够编写文档、处理图形以及进行数字计算。你可能还有其他喜喜欢的应用程序，例如音乐播放器、Web 浏览器和电子邮件阅读器。

> 注意：通过使用 WINE 技术，Codewavers, Inc. 的人员提供了 CrossOver Office 产品，让你可以在 Linux 中安装并运行 Microsoft Office。请参阅本章的“使用 WINE 运行 Windows ”部分。

如果你想了解可用桌面应用程序的概览，表 5-3 列出了流行的 Windows 应用程序、对应的 Linux 应用程序以及在哪里可以找到这些 Linux 应用程序。尽管这些应用程序许多尚未达到其 Windows 版本的复杂程度，但它们可以作为高性价比的替代方案。

### 表 5-3：Windows 等效 Linux 应用程序

| Windows 应用程序 | Linux 应用程序 | 获取 Linux 应用程序途径 | 费用 |
|---|---|---|---|
| Microsoft Office (办公套件) | OpenOffice.org (`openoffice.org`) | 包含在 Fedora DVD 中 | 免费 |
| | Koffee | 包含在 Fedora DVD 中 | 免费 |
| | StarOffice | www.sun.com/staroffice | $69.95 |
| Microsoft Word (文字处理器) | OpenOffice.org Writer | 包含在 Fedora DVD 中 | 免费 |
| | AbiWord | 包含在 Fedora DVD 中 | 免费 |
| | kword | 包含在 Fedora DVD 中 | 免费 |
