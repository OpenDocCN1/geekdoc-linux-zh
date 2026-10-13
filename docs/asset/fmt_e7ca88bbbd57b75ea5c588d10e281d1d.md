
答案是压缩归档。你可以对 tar 归档使用 `gzip` 命令，创建一个以 `.gz` 结尾的文件，或者在创建归档时使用 `tar` 的选项压缩文件，这通常具有 `.tgz` 结尾。如果你有 Windows 背景，你可能熟悉 `zip`、`rar` 或 `arj` 文件。它们基于相同的原理。事实上，Windows 实用程序 `pkzip` 和 `Winzip` 可以处理 `.tar` 文件。简单搜索，我确定你还能找到其他具有类似功能的工具。

## 必备工具

接下来要看的是安装 tar 包所需的工具。从技术上讲，安装可能需要几乎所有东西，但通常如果某个极其不寻常，它会被包含在 tar 包中，或者在文档中被非常清晰地指出。通常你需要 `gcc`、`autoconf`、`make`、`tar` 和 `gzip`，并且对每个程序都有基础知识。让我们来看看这些工具。

`gcc` 是 GNU 编译器。只要有足够的时间，它最终能够编译任何内容。目前它支持 C、C++、Objective C、Chill、Fortran 和 Java。它是 Linux 系统的标准。我将不会深入探讨它的细节，为了支持这么多语言并能够优化代码，该包必须极其复杂。事实上，关于它的文档已经足够写一本书了。了解更多信息，请访问 `gcc.gnu.org` 主页。

`autoconf` 是一个用于为软件包生成配置脚本的工具。一旦脚本生成，就不需要 `autoconf` 了。理想情况下，这个工具允许开发者生成一个通常名为 `configure` 的脚本。想要从源码安装软件的用户应该只需要运行 `configure` 脚本。它将生成所有的 `Makefile`、安装脚本和其他在安装之前通常需要编辑的脚本。虽然你可能不需要安装 `autoconf`，但现在如果你使用 `configure` 脚本，你就知道发生了什么。`autoconf` 的工作原理以及创建脚本所涉及的内容超出了本书的范范围，但你可以在网上找到大量信息。两个好的起点是 `sources.redhat.com/autoconf/` 和 `http://www.amath.washington.edu/~lf/tutorials/autoconf`。

`gzip` 是一个 GNU 压缩工具。它的用法非常简单，而且通常能实现非常压缩效果。你可以在 `man` 手页（`man page`）中找到更多关于它的用法，你可能还会发现在线文档很有趣。可以在 `http://www.gnu.org/manual/gzip-1.2.4/gzip.html` 找到。

## 安装过程

安装过程可能因程序而异，本节无法涵盖所有可能性。学习的最佳方法是通过示例进行操作。大多数程序至少使用 `autoconf`，因此我们将使用的示例也是基于此。在非基于 `autoconf` 的安装中，需要完成的所有工作是不可预测的。尽管我们将探索配置文件中的通用模式，但在这一小时内，我们将安装 `Bombermage`，这是一个基于 GNOME 的克隆程序。如果你像我一样花了大量时间玩这个游戏，我先对打断所有的生产力表示歉意。

首先，访问 `http://www.gnu.org/applist/` 并点击“按类别浏览软件地图”（Browse Software Map by Category）链接。你可以通过该链接找到许多其他 GNOME 应用，但今天你要找的是 `Bombermage`，所以请点击“娱乐”（Entertainment）链接。你会找到 `Bombermage` 的链接，它提供了更多关于该程序的信息。你还会找到位于 `bombermage.sourceforge.net` 的 `Bombermage` 主页链接，花几分钟阅读一下该程序。对你正在安装的内容有所了解总是好的。查看一下需求部分并查看所需的所有库。在 RPM 安装中，所有这些都将为你检查。现在你不是很高兴不需要每次都做这些事情吗？

在查看 `Bombermage` 站点后，进入下载页面并下载 `bombermage-0.6.2.tar.gz`。该程序提供 RPM 包，但你可能想学习如何进行手动安装。你应该将此文件保存在你的主目录或 `/tmp` 中。许多步骤可以在用户账户中执行，但很可能实际文件的安装必须在 `root` 账户中完成。如果你在执行以下步骤时没有使用超级账户并遇到了问题，很可能原因就在于。

## 解压 Tar 包

像 Linux 中的大多数事情一样，有几种方法可以解压和提取 tar 包。本节将检查两个示例。第一种使用 `gzip` 获取 tar 包，然后使用 `tar` 提取文件。要执行此操作，切换到 `bombermage-0.6.2.tar.gz` 所在的目录并输入以下内容：

```bash
# gunzip bombermaze-0.6.2.tar.gz
### ls
bombermaze-0.6.2.tar
```

`gunzip` 已经解压缩了存档，现在留下了解压后的 tar 包。要从 tar 包中提取文件，输入：

```bash
# tar xvf bombermaze-0.6.2.tar
```

命令之后应该会出现一个长文件列表，类似于图 23.1 所示的列表，如果你现在列出目录内容，你应该发现一个 `bombermaze-0.6.2` 子目录。通常情况下，你下载的任何 tar 包通常都会提取到自己的子目录中。这里使用的 `tar` 选项中 `x` 代表提取（extract），`v` 代表详细输出（verbose），`f` 指定文件（file），即 `bombermaze-0.6.2.tar`。另一种方法使用了另一个开关。如果你想尝试其他方法，使用 `gzip` 再次压缩 tar 包。然后尝试以下操作：

```bash
# tar xzf bombermaze-0.6.2.tar.gz
```

### 图 23.1

所有文件都提取到了 `bombermaze-0.6.2` 子目录中。

```
!root@bombermaze-local ~ #$
File Edit Settings Help
bombermaze-0.6.2/src/makefile.in
bombermaze-0.6.2/Changelog.md
bombermaze-0.6.2/src/README.md
bombermaze-0.6.2/src/include.md
bombermaze-0.6.2/src/configure.md
bombermaze-0.6.2/src/Makefile.md
bombermaze-0.6.2/src/utils.md
bombermaze-0.6.2/src/gcc/gcc-checks.md
bombermaze-0.6.2/src/gcc/guide-checks.md
bombermaze-0.6.2/src/gcc/linux-checks.md
bombermaze-0.6.2/src/gcc/obj-checks.md
bombermaze-0.6.2/src/gcc/patch-checks.md
bombermaze-0.6.2/src/gcc/prethread-checks.md
bombermaze-0.6.2/src/gcc/units.md
bombermaze-0.6.2/src/gcc/x-checks.md
bombermaze-0.6.2/src/gcc/get-test.md
bombermaze-0.6.2/src/gcc/gistlib.md
bombermaze-0.6.2/src/gcc/types.md
bombermaze-0.6.2/src/gcc/declaration.md
bombermaze-0.6.2/src/gcc/custom.md
bombermaze-0.6.2/src/autogen.sh
[root@bombermaze ~]# 
```

`z` 选项是在提取文件之前通过 `gzip` 运行存档。为了节省按键次数，这保留了文件。

## 从源码编译并安装应用程序

`z` 选项是在提取文件之前通过 `gzip` 运行存档。为了节省按键次数，这保留了文件。

# 378

# 第 23 小

### 图 23.2

运行 `make` 命令的一些输出内容。

![](img/8a0e42659a358d95f558285b9f5bf854_398_0.png)

```
lgdk -ignome -lXi -lKeest -I/usr/lib/X11 -I/usr/local/rdynamic -Lusr

lgib -rdynamic -L/usr/lib -lX1 -I/usr/local/rdynamic -Lusr

* -c = -o bombermaze.out -preprocessor,mgame,input -o -rdynamic -lgdk

ignome-support -leadaudio -lfi -ignome -lgib -rdynamic -usr/lib/l-/usr/lib/X11 -I/usr/local/rdynamic -lbombermaze -I/usr/lib/X11

pisub -lfi -ignome -lg

make[1]: entering directory /root/bombermaze-0.6.2/

make[1]: leaving directory /root/bombermaze-0.6.2/

make[1]: making in all
```
