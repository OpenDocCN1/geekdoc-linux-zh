
在 Fedora 或 RHEL 系统上，识别软件版本的简单方法是使用 RPM 的查询能力。假设，你想你想知道系统中安装了哪个版本的 Emacs（一种流行的编辑器）。正如本章前面解释的那样，使用 RPM 的查询选项 `-q`。例如：

```bash
$ rpmquery emacs
emacs-21.4-3
```

## 安装和升级软件包 765

输出表明 Emacs 版本为 21.4-3。要找到所有与 Emacs 相关的包（而不只是基础包），你可以使用 `rpmquery` 的 `-a` 选项并通过管道输出。例如：

```bash
$ rpmquery -a | grep emacs
emacs-common-21.4-3
emacspeak-21.0-2
emacs-leim-21.4-3
gnuplot-emacs-4.0.0-7
iifmf-emacs-12.2-0.7.svn2578
emacs-el-21.4-3
emacs-21.4-3
```

`emacs-21.4-3` 到底意味着什么？`major_num`、`minor_num`、`build_num` 命名方案。表 30-7 解释了每个 `build num` 的含义。

因此，大多数软件包使用 `major_num`、`minor_num`、`patch_num` `num`。

| ELEMENT | INTERPRETATION |
| :--- | :--- |
| `name` | 21.4-3 |
| `major_num` | 21.4-3 |
| `minor_num` | 21.4-3 |
| `patch_num` | 21.4-3 |
| `build_num` | 21.4-3 |

不幸，许多应用程序显示的信息比简单的版本号要多，正如示例所示，但至少你得到了你需要的信息。大多数应用程序使用 `-version` 来显示版本号。`-v` 或 `--version` 等选项。

> **注意 当如本节所述调用时，大多数应用程序将显示版本信息并退出。**

## 获取新软件

使用 Red Hat Update Agent 保持系统更新到最新的错误修复和安全补丁是免费的。但如果你想要不是由 Fedora Project 或 Red Hat Software 维护的软件，该去哪里呢？一个普通用户想要尝试新奇不同的东西？假设，例如，你需要获取播放或支持 MP3 音频格式的应用程序 RPM 包？自然，你将从流行的 Fedora 和 RHEL 软件下载站点下载。在某些情况下，你需要从头开始构建（即所谓的，“使用源码，路加加。”）。

# 使用第三方网站查找 RPM

对于那些极不耐心的用户，这里列出了我们最喜欢的网站，用于获取官方发行版中未提供的 Fedora Core 和 RHEL 软件包：

- **Dag Wieers 的 Red Hat/Fedora RPM 仓库 (http://dag.wieers.com/packages)** —— 在编写时，Dag Wieers 已经收集了从 aalib（一个 ASCII 艺术库）到 zlibzip（一个从 ZIP 存档中提取数据的库）的 34,103 个 RPM。Dag 的网站还包含适用于 MP3 友好音频应用程序的 RPM。在不刻意误导你的情况下，这些许多 RPM 适用于多个版本的 Fedora 和 RHEL，以及已经停产的曾名为 Red Hat Linux 的桌面产品。尽管如此，Dag 统计的这 39,572 个 RPM 包含 2166 个不同的产品。对于一个非商业项目来说，这质量并不算太差。

- **freshrms.net (freshrms.net)** —— freshrms.net 是 Matthias 的个人爱好。他最初开始为那些他找不到 RPM 格式的软件构建 RPM。正如他描述该项目时所说：“将 freshrms.net 视为我最大的贡献，通过帮助红帽用户获取主发行版未包含的高质量软件插件包。软件包本身专注于质量而非数量。这意味着你不会在这里找到你能找到的每一个软件，但你在这里找到的内容如果它是原始发行版的一部分，将会无缝融入 Red Hat Linux（http://freshrms.net/about/）。”在编写时，Matthias 仅针对 Fedora Core 3 就拥有了 743 个二进制和源码 RPM。

- **RPM Pbone Search (http://rpm.pbone.net)** —— RPM Pbone Search 与其说是一个搜索工具，而不是 RPM 存档网站。它通过搜索包含特定文件名的 RPM 来帮助你定位满足给定依赖关系的 RPM。你也可以对 RPM 的“提供”（provides）字段以及 RPM 摘要和描述字段进行搜索。对于那些安装或编译新软件但由于某些原因未安装所有所需库，或无法调查系统缺少哪些 RPM 包的用户来说，RPM Pbone Search 特别有帮助。此外，你可以将搜索范围缩小到几个发行版本或特定的 Linux 系统。“RPM Pbone Search”还设计用于定位 FTP 服务器上的 RPM 文件（http://rpm.pbone.net/index.php3?stat/5/）。在编写时，RPM Pbone Search 数据库中总共有 603,817 个 RPM，因此你很有机会找到你需要的内容。

- **Axel Thimm 的 RPMs (ATrpms (http://attrs.net)** —— ATrpms 最初是一个用于软件（RPM 格式）的仓库。

- **rpm.livna.org (http://rpm.livna.org)** —— rpm.livna.org 是 fedora.us/ 上 Fedora Extras 项目的扩展。rpm.livna.org 携带了不属于 Fedora Core 且各种原因无法在 fedora.us 网站上的软件包。特别是正如 rpm.livna.org 的 FAQ 所解释的，它分发了由于许可或专利限制（与红帽政策不一致）而不被 Fedora.us 接受的软件包，例如禁止商业用途的许可。（更多信息请参见 http://rpm.livna.org/faq.html。）rpm.livna.org 的软件包与列表中其他网站的软件包（fedora.us 或 fedaproject.org 的 Fedora Extras 除外）不兼容。

- **Fedora Extras (fedora.us/)** —— 如果你有旧版本的 Fedora Core（Fedora Core 3 之前），这对你可能有用。但请注意，此网站的软件包与列表中其他网站的软件包不兼容。此外，Fedora Core 2 及更早版本现在处于维护模式，这意味着如果它有任何新开发，所有的兴趣和兴奋都已转移到新版本。

- **rpmfind.net (http://rpmfind.net)** —— rpmfind.net 是最老的第三方 RPM 仓库，维护了大量的基于 RPM 的软件包，涵盖了所有主流发行版和许多分支版本，跨越整个应用类别。它还按平台列出 RPM，例如 Intel x86、SPARC 和 Macintosh。其精调的引擎让你能够轻松找到所需的 RPM，或者至少将可能范围从 100,000 多个减少到一个更易管理的数字。它还是 rpm2html 工具的官方网站，你可以在自己的机器上运行该工具，以简化寻找需求所需 RPM 的过程。

- **FedoraProject.org (http://www.fedaproject.org/wiki/Extras/)** —— 该网站是 Fedora Core 的家园，包含了按照 Fedora Core 标准构建但未包含在 Fedora Extras 中的 RPM。请务必阅读关于 fedora.us/wiki/Extras_2fUsingExtras 使用 Fedora Extras 的说明。

除了 fedora.us 和 fedorproject.org 之外，这些网站没有获得红帽或 Fedora 项目的认可，因此你获得的 RPM 质量可能参差不齐。

# 使用 Ibiblio.org

Ibiblio.org 的规模可以说是目前可用所有 Linux 和开源仓库中最大的。它始于 Sunsite（严格来说，是 ftp://sunsite.unc/）。

在 20 世纪 90 年代，北罗来纳大学将 Sunsite 重命名为 Metalab，ibiblio.org 变成了各种信息的公共仓库。在编写时，ibiblio.org 拥有 55 GB 的下载软件，包括文章、照片和多媒体。

（注：OCR 文本包含了重复的 ibiblio.org 部分；根据保留原始信息但纠正错误的指令，此处提供该部分的连贯版本。）

要访问 Ibiblio 的 Linux 存档，请使用浏览器访问 ibiblio.org/pub/Linux 并选择 Linsearch 链接。

> 提示：Linux Software Map 比本章中的其他网站维护频率较低，它是一个 Linux 软件数据库。它支持通过关键词和标题搜索，并允许按应用程序标题浏览整个数据库。

# 从源码安装软件

在下载了 RPM、SRP 或源码归档（如 tarball）后，你自然会想要安装它。“使用红帽软件包管理器”一节详细说明了如何安装二进制 RPM 以及如何从 SRP 创建二进制 RPM。本节将展示如何从源码安装软件，即解包、配置并构建你下载的未编译源码的软件软件包。

在像 RPM 这样的包管理套件流行之前，你通过使用以下步骤来升级和安装软件：

1. 下载一个 gzipped tarball（使用 gzip 属性压缩的 tar 存档）。

2. 解压它。

3. 通过手动编辑一个或多个头文件或使用自动对你的系统定制软件包的 configure 脚本来进行配置。

4. 执行 `make` 进行构建。

5. 执行 `make` 进行安装。

尽管 RPM 非常流行，但仍有大量软件使用这种方法，因此本节将带你了解整个过程以熟悉它。本节使用的示例配置、构建并安装了 bc，这是一种用于文本模式 dc 计算器的算术处理语言。

## 配置构建环境

上一段隐含了一个假设，即你的系统已经安装了开发环境。对于终端用户和系统管理员，构建环境由编译器 `gcc` 及其支持库、用于自动调用编译器的 `make` 工具、一些关键开发库（主要由头文件组成），以及用于处理复制文件、分配适当所有权和设置文件权限等细节的 `install` 工具。。

安装过程中，选择“Development workstation”（开发工作站）选项以安装完整的开发环境。否则，请确保你的系统中至少安装了以下 RPM 包：

- bzip2

- fileutils

- gcc++（用于 C++ 程序）

- gcc（用于 C 程序）

- glibc-devel

- gzip

- kernel-headers

- kernel-source

- make

- ncompress

- tar

有额外要求的软件包通常会说明其具体要求，因此请阅读软件包的文档以确保你的系统已安装所需的软件。

# 解压源码

下载 `bc` 软件包（本章源码目录下的 `bc-1.0.6.tar.gz`）后，将其移动到一个不会干扰系统的位置。在本示例中，我将其移动到了 `/tmp`。进入 `/tmp` 后，你可以使用两个命令之一来解压并解包归文件。第一个命令在一个命令中结合了 tar 包的解压和解包：

```
$ tar zxf bc-1.0.6.tar.gz
```

# 安装和升级软件包 773

`z` 选项使用 `tar` 内置的 `gunzip` 程序的来解压文件，`x` 提取存档文件，`f` 指定要操作的文件名。第二个命令可以使用管道 (`|`) 将 `gunzip` 的输出传递给 `tar` 的输入，即：

```
$ gunzip -c bc-1.0.6.tar.gz | tar xf -
```

> 提示：如果你想从这两个命令中获得更多反馈，可以使用 `tar -v` 选项让其显示正在从包中提取的文件。

`gunzip -c` 选项将解压结果返回到标准输出；`tar` -f` 告诉它读取标准输入；管道连接了这两个命令。无论哪种情况，你都会当前目录（在本例中为 `/tmp`）下得到一个名为 `bc-1.0.6` 的目录。因此，进入 `bc-1.0.6` 以继续配置 `bc`。

# 配置源码

现在 `bc` 软件包已经解压，下一步是为你的系统进行配置。在许多情况下，通过指定安装目录来为你的系统构建软件包，但许多软件包（包括 `bc`）允许你请求额外的自定义。幸运的是，这是一个简单的步骤——`bc` 与其他软件包不同，它使用 `configure` 脚本来自动化配置和自定义。`configure` 脚本是一个 shell 脚本，它对编译过程中使用的各种系统特定值的正确值进行合理猜测。此外，通过命令行选项和参数调用 `configure`，你还可以指定这些相同值的值。`configure` “猜测”并由传递给 `configure` 命令行的值通常会被写入一个或多个文件（`make` 程序使用这些文件来控制构建过程），或者写入定义所构建程序特征的一个或多个头文件 (.h)。

要查看你可以自定义的项，请在你正在构建的软件包根目录下执行 `./configure --help`，如下例所示（为了节省空间已编辑）。

```
$ ./configure --help
Usage: configure [options] [host]
Options: [defaults in brackets after descriptions]
Configuration:
```

Directory file names:

--prefix=PREFIX install architecture-independent files in

--exec-prefix=EPREFIX [/usr/local] install architecture-dependent files in

[same as prefix]

Host type:

--build=BUILD configure for building on BUILD [BUILD=HOST]

--host=HOST configure for HOST [guessed]

--target=TARGET configure for TARGET [TARGET=HOST]

Features and packages:

--disable-FEATURE do not include FEATURE (same as --enable-FEATURE=no)

--enable-FEATURE=[ARG] include FEATURE [ARG=yes]

--with-PACKAGE=[ARG] use PACKAGE [ARG=yes]

--without-PACKAGE do not use PACKAGE (same as --with-PACKAGE=no)

--x-libraries=DIR X library files in DIR

--enable-with-options X library files recognized

--with-pkg use software installed in /usr/prefix/pkg tree

--with-libedit support fancy BSD input editing

--with-readline support package command input editing

示例输出中的关键选项是 `--enable` 和 `--with` 选项，即出现在 `--enable` 和 `--with-libedit`以及`--with-readline`标题下的三个选项。`--prefix` 允许你在默认值之后指定安装目录（在括号内为 `/usr/local`）。在本示例中，根安装目录为 `/tmp/bctest`，在命令行指定为 `--prefix=/tmp/bctest`。第二组命令行选项启用了其他功能。此示例使用了 `--with-readline`，它为 GNU readline 开启。`readline` 库允许在 `bc` 程序内部进行命令编辑，就像 bash 允许编辑命令行一样。

在选择所需的选项后，使用相应的选项运行 `configure`，如下例。（再次，输出已为了节省空间编辑）。

```
$ ./configure --prefix=/tmp/bctest --with-readline
creating cache /config.cache
checking for a BSD compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking whether make sets $(MAKE)... yes
checking for working local... found
checking for working autoconf... found
checking for working alocal... found
```

# 774 第30章

## 构建软件

根据你构建的程序的规模和复杂性，`make` 的输出可能是非常详尽的。在示例中，你将看到最后的编译器调用，最重要的是没有错误。因此，下一步是测试构建。

# 测试构建

许多程序（特别是来自 GNU 项目的程序）包含某种测试套件来验证程序。其核心思想是确保程序在安装之前工作正常。在某些情况下，你执行 `make test` 命令来运行测试套件。在其他情况下，如 `bc` 所示，构建树中的一个特殊子目录（方便地命名为 `test` 或 `Test`）包含测试套件。每个软件包处理测试的方式不同，请阅读软件包文档。在 `bc` 的情况下，测试套件位于名为 `Test` 的子目录，并通过一个 shell 脚本 `timetest` 执行实际测试。以下命令调用 `bc` 的测试套件：

```
$ cd Test
$ ./timetest
```

`timetest` 至少需要运行10分钟，所以测试运行时你可以喝杯咖啡或你喜欢的饮料。如果测试期间没有出现错误，你就可以准备好安装它了。

## 安装和升级软件软件包 777

### 安装软件
