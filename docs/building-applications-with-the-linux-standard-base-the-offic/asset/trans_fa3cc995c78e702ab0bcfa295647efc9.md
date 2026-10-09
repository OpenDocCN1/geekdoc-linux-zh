
在 `/opt/whizbang/` 目录中，该目录最常用的两种使用方式要么是将 `bin` 和 `lib` 子目录共享，要么是将它们分别存放在各自的 `/opt/whizbang/widgets/` 和 `/opt/whizbang/gadgets/` 子目录中。如果将它们分开存放，则可以通过在 `/opt/whizbang/bin/` 中创建符号链接或包装脚本，将其重定向到 `/opt/whizbang/widgets/bin/` 和 `/opt/whizbang/gadgets/bin/`。无论哪种情况，都应最终将 `/opt/whizbang/bin/` 添加到最终用户的 `PATH` 环境变量中。

## 4.5.2 为多种架构进行打包

为了在 PPC64 系统上同时支持 Widgets 的 32 位和 64 位 PowerPC 版本，需要将它们分离到各自独立的架构子目录中，例如图 4.4 中所示的 `/opt/whizbang/widgets/ppc32/` 和 `/opt/whizbang/widgets/ppc64/`。系统管理员可以通过创建从 `/opt/whizbang/widgets/ppc32/bin/` 指回 `/opt/whizbang/widgets/bin/` 的符号链接，或者创建从 `/opt/whizbang/widgets/ppc32/lib/` 指回 `/opt/whizbang/widgets/lib/` 的符号链接，来设置默认的 PPC32 或 PPC64 行为。无论哪种情况，都应最终将 `/opt/whizbang/widgets/bin/` 添加到最终用户的 `PATH` 环境变量中。

## 4.5.3 为多个产品版本进行打包

为了同时支持同一产品的多个版本，需要将它们分离到各自独立的版本子目录中，例如图 4.5 中所示的 `/opt/whizbang/widgets/v1/` 和 `/opt/whizbang/widgets/v2/`。系统管理员可以通过创建从 `/opt/whizbang/widgets/v1/bin/` 指回 `/opt/whizbang/widgets/bin/` 的符号链接，或者创建从 `/opt/whizbang/widgets/v2/lib/` 指回 `/opt/whizbang/widgets/lib/` 的符号链接（示例 4.7），来设置默认的 v1 或 v2 行为。无论哪种情况，都应最终将 `/opt/whizbang/widgets/bin/` 添加到最终用户的 `PATH` 环境变量中。

## 4.5 高级打包

![](img/d75cffbcb54aabfb0f9854162061d394_80_0.png)

## 示例 4.7：在安装后为 Widgets 创建符号链接

```
%post
P=$RPM_INSTALL_PREFIX/whizbang/widgets
mkdir $P/bin > /dev/null 2>&1
ln -fs $P/ppc32/bin/widgets $P/bin/widgets
# EOF
```

## 4.5.4 为多种架构上的多个产品的多个版本进行打包

为了在多种架构上同时支持多个产品的多个版本，需要将它们分离到各自独立的子目录中，例如图 4.6 中所示的 `/opt/whizbang/widgets/v1/ppc32/` 或 `/opt/whizbang/gadgets/v2/ppc64/`。系统管理员可以通过创建从 `/opt/whizbang/widgets/v1/ppc32/bin/` 指向 `/opt/whizbang/widgets/bin/` 的符号链接，来设置默认的 v1 或 v2 以及/或者 PPC32 或 PPC64 行为。无论哪种情况，都应最终将 `/opt/whizbang/widgets/bin/` 添加到最终用户的 `PATH` 环境变量中。

# 第五章

# 将 Solaris 应用程序迁移到 Linux

Linux 日益普及的一个后果是，各公司迫切希望将现有的应用程序和开发环境迁移到 Linux 上。遵循标准的应用程序比不遵循标准的应用程序更容易移植。由于 Linux 和 Solaris 共享 UNIX 的通用 API 集合，因此从 Solaris 迁移到 Linux 比从具有不同 API 的操作系统（例如 Microsoft Windows）迁移更容易。

本章概述了这种迁移的优势以及可以采用的路径。除了提供迁移过程中可以使用的工具包外，还讨论了一些与标准相关的移植问题。

## 5.1 移植路线图

开发可移植的应用程序并非易事。尽管 Solaris 和 Linux 都是 UNIX 的变体，但它们在 API、系统调用和其他组件方面存在许多差异。任何 Linux 发行版都附带了关于如何利用这些接口开发应用程序的充分文档。然而，文档并不总是清晰的，而且标准非常多样化。其中一个相关标准是 POSIX（可移植操作系统接口）规范（参见第 2.2.1 节）。如果您的应用程序符合该规范，移植起来会容易得多。

为平台开发应用程序还需要一套丰富的工具。作为平台，Linux 附带了许多此类开源工具。这些工具包括代码编辑器、代码格式化工具、编译器、链接器和调试器。此外，各供应商也提供这些工具的商业等效产品。

这里概述的步骤只是执行无缝迁移的一种方法；还有许多其他方法。迁移路径的选择取决于可以投入此项工作的资源数量和时间。一旦选定路径，就必须通过适当的规划和小的步骤执行来实施。

此路线图的目的是调整待迁移的 Solaris 应用程序，使其能够在 SPARC 版本的 Linux 上运行。一旦完成此操作，就可以以相对较小的工作量将应用程序迁移到目标 Linux 平台。

### 5.1.1 第 1 步：获取必要的 Linux 发行版

为了实施此迁移方案，有必要使用两个不同的 Linux 发行版：一个用于 SPARC 的 Linux 发行版，以及另一个针对目标平台专用的 Linux 发行版。

Linux/SPARC 自 1994 年可用以来，其古老和成熟程度与普通 Linux 相当。主要的 Linux 供应商（如 Red Hat 和 SuSE）也发布了它们的 Linux/SPARC 版本。Linux/SPARC 适用于几乎整个 SPARC 硬件系列，包括针对 32 位和 64 位处理器的版本。

Linux 也适用于不同的硬件平台，如 Intel 兼容 PC、PPC（PowerPC）、Alpha 处理器、Itanium 和大型机。各种平台的可用供应商列表可在网络上找到。¹ 此列表包括 Linux 的商业版和免费版。您可以使用此列表根据目标平台、其捆绑的功能以及必要的资金来确定 Linux 版本。

### 5.1.2 第 2 步：下载必要的 GNU 工具

GNU 拥有开发工作所需的工具，称为 GCC（GNU 编译器集合）。GCC 支持多种语言，如 C、C++、Fortran，甚至 Java。GNU 工具的完整列表可在线获取。² GNU 工具侧重于在减少迁移过程中花费的时间的同时开发可移植的源代码。即使是很少了解 Linux 的 Solaris 开发人员也可以使用这些工具开始为目标 Linux 平台生成代码。

Solaris 环境所需的 GNU 工具可从 http://www.sunfreeware.com/ 下载。大多数 Solaris 版本的 GNU 工具都可从此站点免费获取。针对 SPARC 以及目标平台的 Linux 的 GNU 工具也随各自的发行版一起提供。

### 5.1.3 第 3 步：在 Solaris 上构建 C/C++ 应用程序

一旦所有构建工具都准备好，就在 Solaris 上开始构建过程。使用 GNU **gmake** 实用工具而不是 **make** 来构建源代码。尽管这两个实用工具目的相同，但它们之间存在相当大的差异。为 Solaris **make** 实用工具创建的 Makefile 在与 **gmake** 实用工具一起使用时，可能会根据其使用的构造生成错误。相应的 **gmake**³ 和 **make**⁴ 工具文档是解决这些错误的最佳来源。

尽管这些工具之间存在差异，但它们也共享一些共同的规则和后缀。表 5.1 中显示的目标、宏和变量可以互换使用，因为它们在两个实用工具中具有相同的含义。

在修改 Makefile 以符合 **gmake** 规则之后，下一步是尝试使用 GNU 编译器而不是其 Solaris 对应物。应使用 **gcc** 编译器而不是 **cc**，并使用 **g++** 而不是 **C++**。一旦使用 GNU 编译器，将会出现大量错误，这些错误可以分为由于命令行选项差异导致的错误和由于编码差异导致的错误。然而，这两种类型的错误大多可以通过参考编译器文档来解决：

- 使用和移植 GNU 编译器集合 (GCC)⁵
- 2. http://www.gnu.org/directory/GNU/
- 3. GNU **make** (http://www.gnu.org/software/make/manual/make.html).
- 4. Managing Projects with make (http://www.o-reilly.com/catalog/make2/).
- 5. http://gcc.gnu.org/onlinedocs/gcc-2.95.2/gcc_toc.html

