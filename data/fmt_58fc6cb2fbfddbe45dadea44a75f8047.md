
```
$ gcc -pg -fno-strength-reduce -g hello.c -o hello
```
```
$ gcc hello.c -o hello -g fno-strength-reduce -pg
```

# 附章节

在大多数情况下，选项及其参数的顺序并不重要。在某些情况下，顺序是重要的，特别是当你使用几个相同类型的选项时。例如，`-I` 指定搜索包含文件的目录或目录。因此，如果你指定多次 `-I`，`gcc` 将按照指定的顺序搜索列出的目录。

使用 `gcc` 编译单个源文件是简单的——只需调用 `gcc` 并将文件名作为参数传递即可，如下例所示：

```
$ gcc hello.c
```

默认情况下，结果是当前目录下的一个可执行文件 `a.out`，你通过输入 `./a.out` 来执行它。要定义 `gcc` 生成的输出文件的名称，请使用 `-o` 选项，如下例所示：

```
$ gcc hello.c -o run
```

如果你使用 `gcc` 编译多个源文件，你可以在 `gcc` 命令行上指定它们，如下例所示，编译并链接后的可执行文件文件名为：

```
$ gcc showdate.c helper.c -o showdate
```

如果你想增量编译文件并最终将它们链接成二进制文件，可以使用 `-c` 选项在生成对象文件后停止编译。你可以使用 `gcc` 命令将它们全部链接在一起并指定输出文件的名称，如下例所示：

```
$ gcc showdate.c
$ gcc helper.c
$ gcc showdate.o helper.o -o showdate
```

很容易看出，一个由几个源文件组成的项目，从命令行编译将变得极其繁琐，特别是当你开始链接库、添加优化选项以及提供其他杂杂 `gcc` 选项之后。解决这种命令行繁琐问题的方案是 `make`，它将在下一节中讨论。

# 创建 Makefile

自 UNIX 早期时代以来，许多 UNIX 应用一直使用一种名为 `make` 的规则驱动编译方法进行构建，`make` 调用编译器和其他实用程序来处理程序源码的所有必要组件。`make` 程序是 Linux 以及所有其他 UNIX 类系统上构建 C 和 C++ 应用的基石。`make` 程序执行以下操作：

- 识别源模块（包括文件）与库之间的关系和依赖关系，这些成功编译所需的。
- 指定成功构建应用程序必须编译的顺序。
- 通过将编译限制在受影响的应用部分，从而避免重复编译。

`make` 程序最初由 Stuart Feldman 为早期的版本的 UNIX 编写。`make` 程序已被 `GNU make` 取代，它提供了许多功能以及特定于平台的库，这些库可能位于不同的目录或具有不同的名称。正如你预期的，复杂应用的 Makefile 也可能极其复杂。最简单的 Makefile 是用于简单应用程序的，例如 C 语言的 "Hello World"。Makefile 看起来如下：

```
hello:c
gcc hello -o hello
```

第一行识别了该 Makefile 构建的二进制目标（`hello`），以及当源文件被修改时必须重新生成它。第二行（以制表开头）指定了生成该二进制目标的命令。要调用它，你必须在该目录下执行命令。`make` 程序会自动查找名为 `Makefile` 的文件并遵循其包含的规则。

> 所有构建规则的行都必须以制表开头，这一事实是手工编写 Makefile 时最常见的问题之一。

尽管这个例子展示了 Makefile 的基础，但它也是一个微不足道的例子，没有显示 Makefile 在简化和自动化计算方面的任何实际收益。让我们考虑另一个例子。在上一节中，我使用以下命令行从两个对象模块编译了单个二进制文件：

```
$ gcc -c showdate.c
$ gcc -c helper.c
$ gcc showdate.o helper.o -o showdate
```

此处的 Makefile 看起来类似于：

```
showdate: showdate.o helper.o
gcc showdate.o helper.o -o showdate
```

```
showdate: showdate.c
gcc -c showdate.c
helper: helper.c
gcc -c helper.c
```

这个例子强调了当你只修改了项目的某些文件时，Makefile 如何减少必要的重新编译。对于这个例子，Makefile 说明二进制文件依赖于两个对象模块 `showdate.o` 和 `helper.o`，并提供了使用 `gcc` 链接这两个对象文件以生成二进制文件的规则。它继续强调每个对象模块都依赖于其相关的 C 语言文件，并为 `gcc` 重新生成每个对象模块提供了规则。

如果例如只修改了其中一个 C 文件，这个示例 Makefile 可以简化重新编译。Makefile 将仅重新生成被修改的 C 文件的对象模块，然后将现有的对象文件与新的对象文件链接以重新生成二进制文件。

# 附录章节

随着你的项目变得越来越大，你将希望利用 Makefile 的其他功能，例如定义和使用变量、使用某些真正晦涩的 shell 来简化 make 规则等。关于 `make` 程序和 Makefile 的更多高级信息的一些良好来源如下：

- [www.linuxdevcenter.com/pub/a/linux/2002/01/31/make_intro.html]: 来自 O'Reilly & Associates Linux 开发中心关于 `make` 的一篇优秀文章。
- [tldp.org/HOWTO/Software-Building-HOWTO-3.html]: Linux 文档项目 Linux 软件开发指南中关于使用 `make` 的章节。
- [gnu.org/software/make]: `GNU make` 的主页，包含指向官方 `make` 文档的链接。
- [gnu.org/software/make/manual]: `GNU make` 文档的在线主页，提供多种格式。

# 编译开源软件

作为一名长期的 Linux 用户，我已经习惯或依赖某些 Linux 软件。这通常没有问题，但软件与任何其他东西一样，除非利用其他包等，否则会被具有类似功能的新软件包包所取代。在这种情况下，该包会在某个时刻被果断从各种发行版中剔除。我在 Ubuntu 8.04 中就是如此，它放弃了我使用了多年的音乐播放器 X Media Player（称为 XRMS）。XRMS 已被 Audacity 代替（后者是一个类似但简单得多的应用程序，在第 19 章中讨论过），而 XRMS 的新版本（最近命名为 XRMS）是目前架构中使用 Linux 的最佳方式之一，这可以帮助支持更多的数字音频文件和格式。由于我是一个长期的音乐收藏者，我有相当多 Audacity 或 XRMS 不支持的格式的数字记录，而且我希望使用一个能够以原生格式处理我所有在线音乐的音频播放器。我该怎么办？显而易见的解决方案是编译我需要的软件和插件，这为本节提供了一个极佳的示例。

> 注意 本节中作为示例使用的 XRMS 包使用了标准的 X 系统和 GTK 图形（这是 Ubuntu 8.04 丢弃的内容之一）。你可以在基于 KDE 的系统上编译此包，你将安装许多在 KDE 环境中通常找不到“alien”包。

对于所有现代软件，编译开源软件包都可能有些复杂。接下来的几节将展示从源码编译开源包可能涉及的内容，我们提供了当你尝试自己编译开源软件时可能会遇到的问题问题示例，以及如何使用 `aptitude install` 来识别和解决这些问题。在此过程中，这些章节还强调了你编译与你真正想要的包相相关的其他包的不同方法。

> 注意
下文关于从命令行编译开源软件的章节假设你已经安装了本章之前讨论过的 `build-essential` 软件包。

# XMMS 编译概览

如果你阅读这一节是因为你只想编译一个带有 MP3, SHN, OGG, SHN 和 FLAC 文件的 XMMS，而不是学习在编译开源应用时如何识别和解决问题，以下是你应该采取的简单步骤列表，不包含任何这些步骤的原理：

```
sudo apt install glib1.2-dev libgtk1.2-dev lib2d0-dev \
libmkmod2-dev libogg-dev libvorbis-dev \
libasound2-dev libg11-mesa-dev
$ cd; mkdir src; cd src
$ wget http://xmms.org/files/1.2.x/xmms-1.2.11.tar.gz
$ tar zxvf xmms-shn-1.2.11.tar.gz
$ cd xmms-1.2.11
$ ./configure
$ sudo make install
$ cd ..
..
$ wget http://etetree.org/shnutils/dist/src/xmms-shn/xmms-shn-2.4.1.tar.gz
$ tar zxvf xmms-shn-2.4.1.tar.gz
$ cd xmms-shn-2.4.1
$ ./configure
```
