

## mkdistcc.sh 和 mkdistcclinks.sh

这些脚本包含了对构建支持 DistCC 的交叉工具链的 Crosstool 支持。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_126_0.png)

DistCC 通过在计算机集群中分发构建工作来实现更快的构建速度。这超出了本书的范围，但如果您感兴趣，我们推荐访问位于 http://distcc.samba.org 的 DistCC 网站。

## demo-cpu.sh

作为起点的示例脚本。每个受支持的架构都有一个（例如，demo-i686.sh）。

## demo.sh

一个大型演示文件，运行所有的架构演示文件。主要用于测试 Crosstool 本身。

## clean.sh

顾名思义，这是一个清理 Crosstool 工作目录的脚本。

## all.sh

实际生成工具链的脚本；其用法的示例将在本节稍后出现。它是一个通用控制脚本，具有根据提供的参数按顺序调用所有其他脚本的逻辑。参数包括：

- `--noinpack`
  指示脚本不要运行 getnandpatch.sh。对于快速重启构建很有用。
- `--noubuild`
  指示脚本不要运行 crosstool.sh。对于稍后构建时下载源代码或运行回归测试很有用。
- `--notest`
  指示脚本不要运行 crosstest.sh，从而跳过回归测试套件。

这些脚本大多是架构和版本通用的。与不同架构和工具版本相关的信息存储在不同的数据文件中：

## cpu.dat

每个受支持的架构（例如，arm.dat）或特定 CPU（例如，ppc-8540.dat）都有一个这样的文件。该文件包含配置 Crosstool 以适用于特定架构所需的信息。它设置 GNU 目标名称和相关选项。

## gcc-version-glibc-version.dat

每个 GCC 和 GLibc 版本的组合都有一个这样的文件（例如，gcc-3.4.0-glibc-2.3.2.dat）。该文件包含配置 Crosstool 以适用于该组合所需的信息。它设置 binutils、GCC、glibc 版本以及相关选项。

## patches\(program/*.patch\)

这些是正确构建各种组件版本所需的补丁文件。program 是该补丁旨在适用的程序和版本的名称。每个补丁文件头包含有关其用途的注释，并链接到任何相关讨论。

使用 Crosstool 非常简单直接：创建一个 shell 脚本来设置一些重要的 shell 变量并调用构建脚本。对于以下示例的目的，我们假设我们将该文件命名为 mytoolchain.sh。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_127_0.png)

使用随 Crosstool 附带的一个示例脚本作为起点，并根据您的需求进行适配。

这是脚本的前几行：

```bash
TARBALLS_DIR=download
RESULT_TOP=$SPRROOT/tools/ # 工具将安装到的位置
GCC_LANGUAGES="c,c++" # 它将为其生成编译器的语言
```

要构建交叉工具链，请创建一个架构描述文件和 GCC 与 glibc 版本的描述文件。然后调用构建脚本。

例如，要为 i686 构建基于 gcc-3.4.0 和 glibc-2.3.2 的工具链，请在 mytoolchain.sh 脚本中添加以下行：

```bash
eval `cat i686.dat gcc-3.4.0-glibc-2.3.2.dat` sh all.sh --notest
```

然后执行脚本：

```bash
$ sh mytoolchain.sh
```

此时，脚本将运行相当长的时间，因为它下载每一个工具链组件，打补丁，配置它们，并构建它们。

当脚本完成时，新的工具链就准备好了，您可以从 $SPRROOT/tools/gcc-3.4.0-glibc-2.3.2/i686-unknown-linux-gnu/bin/i686-unknown-linux-gnu-gcc 运行新创建的编译器。当然，您可能希望将 gcc-3.4.0-glibc-2.3.2 和 i686-unknown-linux-gnu 替换为您实际的 GCC 和 glibc 版本以及架构。

您的工具链现在已准备好使用，但其位置的路径名太长，使用起来不太方便。作为最后一步，我们将通过从 tools 目录到工具链 bin 目录创建符号链接来创建一个快捷方式：

```bash
$ ln -s $SPRROOT/tools/gcc-3.4.0-glibc-2.3.2/i686-unknown-linux-gnu/bin \
$SPRROOT/tools/bin
```

从此，您可以在 `$SPROOT/tools/bin/i686-unknown-linux-gnu-gcc` 处访问该工具链，如果您已将此目录添加到工作区设置脚本的运行路径中，您可以简单地使用 `i686-unknown-linux-gnu-gcc`。

# Ptxdist

Ptxdist 是一个由德国公司 Pengutronix e.K. 发起的用于用户空间（userlands）的构建系统。它作为一个开源项目（受 GPL 许可）得到维护，并有 Pengutronix 的积极参与，后者还以 OSE-LAS 品牌销售其商业支持服务。项目网站位于 `http://www.pengutronix.de/software/ptxdist/index_en.html`。

**Ptxdist 概览。** 不仅仅是自动化的交叉工具链构建框架，Ptxdist 可以被视为“可执行文档”。它构建交叉工具链，然后使用该工具链为目标构建 Linux 内核镜像和 `root` 文件系统，然后将其打包为二进制镜像，格式有多种可供选择。

然而，在本节中，我们将仅将 Ptxdist 作为自动化的交叉工具链构建系统来介绍。在本章后面，我们将把它作为一个完整的嵌入式 Linux 项目的自动化构建系统来使用。

使用 Ptxdist 构建交叉工具链的过程分为两个阶段。首先，我们将下载并安装核心 Ptxdist 包和 Ptxdist 补丁包。然后，我们将下载一个示例 Ptxdist 项目，该项目可以生成几种不同的交叉工具链变体。

**安装 Ptxdist。** 首先，从项目网站获取最新版本并安装它。在撰写本文时，最新版本是 1.0.1：

```bash
$ wget http://www.pengutronix.de/software/ptxdist/download/v1.0/ptxdist-1.0.1.tgz
$ wget http://www.pengutronix.de/software/ptxdist/download/v1.0/ptxdist-1.0.1-patches.tgz
```

接下来，解压这些压缩的 tar 归档文件并进入项目目录：

```bash
$ tar zxvf ptxdist-1.0.1.tgz
$ tar zxvf ptxdist-1.0.1-patches.tgz
$ cd ptxdist-1.0.1
```

现在，配置 Ptxdist 以便在您的系统上使用，构建它，并安装它：

```bash
$ ./configure --prefix=$SPROOT/build-tools/
$ make
$ make install
```

**设置 Ptxdist。** 安装 Ptxdist 后，您可以配置它来构建工具链。虽然默认配置在大多数情况下运行良好，但本地网络和安全策略可能需要大量的配置。

要设置您的新 Ptxdist 安装，请发出以下命令：

```bash
$ ptxdist setup
```

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_129_0.png)

图 4-1. Ptxdist 设置菜单

它显示 Ptxdist 设置菜单，如图 4-1 所示。

设置菜单允许您配置许多选项。您可以使用 ? 键获取有关每个选项的信息。这将显示一段解释当前选项如何使用的段落，并提供其默认值。

提供以下子菜单：

- **Proxies**
  为 Ptxdist 设置 HTTP 和 FTP 代理服务器，以便在从 Internet 下载源代码包时使用。
- **Project Searchpath**
  选择默认的项目工作目录。将其设置为您项目的 tools 目录。
- **Source Directory**
  选择一个目录，所有源代码包将下载到此目录中。将其设置为您项目 build-tools 目录下的一个子目录。
- **Mirrors**
  允许您指定下载 Debian、GNU 和 Xorg 源代码包的位置。通常没有理由更改此设置，但如果某些源代码包因服务器不可用而加载失败，您可能需要为相应项目指定不同的镜像。

## IPKG Repository

IPKG 是一种在许多基于 Linux 的嵌入式系统发行版中使用的二进制打包格式。Ptxdist 可以根据其构建的包为您创建一个自定义的 IPKG 存储库。对于工具链构建项目，请保持此选项为默认值。

## JAVA SDK

Ptxdist 允许您构建一些基于 Java 的包。此子菜单可用于指向构建 Java 程序所需的相关 Java SDK。对于工具链构建项目，您可以将此选项保留为默认值。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_130_0.png)

如果配置菜单未显示出来，请确保您的可执行路径已正确设置（例如，通过运行前面描述的开发环境设置脚本），并且您的终端至少具有 19 行 x 80 列。

完成后，选择 `< Exit >` 按钮并按 `Enter`，然后选择 `< Yes >` 按钮以保存您的新配置。

**创建工具链项目。** Ptxdist 围绕“项目”的概念组织，项目是一组用于构建特定软件集所需的配置文件和补丁。要开始使用 Ptxdist 框架构建我们的交叉工具链，我们将下载 Ptxdist 网站上的一个示例工具链 Ptxdist 项目并解压该归档文件：

```bash
$ wget http://www.pengutronix.de/oseslas/toolchain/download/OSELAS.Toolchain-1.1.1.tar.bz2
$ tar jxvf OSELAS.Toolchain-1.1.1.tar.bz2
$ cd OSELAS.Toolchain-1.1.1/
```

现在，从包含的示例中选择一个要构建的样本工具链。每个工具链示例由 ptxconfigs 目录中的一个配置文件表示：

```bash
$ ls ptxconfigs
arm-1136jfs-linux-gnueabi gcc-4.1.2 glibc-2.5 linux-2.6.18.ptxconfig
arm-xscale-linux-gnueabi gcc-4.1.2 glibc-2.5 linux-2.6.18.ptxconfig
armeb-xscale-linux-gnu gcc-4.0.4 glibc-2.3.6 linux-2.6.17.ptxconfig
arm-ep93xx-linux-gnueabi gcc-4.1.2 glibc-2.5 linux-2.6.18.ptxconfig
arm-iwmmx-linux-gnueabi gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
arm-wrt.hardfloat-linux-gnu gcc-4.0.4 glibc-2.3.6 linux-2.6.18.ptxconfig
arm-v4t-linux-gnueabi gcc-4.1.2 glibc-2.5 linux-2.6.18.ptxconfig
arm-v4t-linux-gnu gcc-4.0.4 glibc-2.3.6 linux-2.6.18.ptxconfig
arm-xscale.hardfloat-linux-gnu gcc-4.0.4 glibc-2.6.16 linux-2.6.17.ptxconfig
arm-xscale-linux-gnueabi gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
arm-xscale-linux-gnu gcc-4.0.4 glibc-2.3.6 linux-2.6.17.ptxconfig
i586-unknown-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
i686-unknown-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
mips-r5000-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
powerpc64-603e-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
powerpc64-970-linux-gnu gcc-4.1.2 glibc-2.5.5 linux-2.6.18.ptxconfig
```

要构建示例工具链之一，您需要告诉 Ptxdist 您想要使用哪个配置文件，然后指示它根据配置文件中的说明构建工具链。

