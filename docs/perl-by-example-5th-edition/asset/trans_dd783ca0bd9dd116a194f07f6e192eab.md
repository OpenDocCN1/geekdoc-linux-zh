
## C.5 附录摘要

Moose 的内容远不止这些。本附录仅作为入门介绍，提供了一些 Moose 示例以帮助你开始使用。互联网上可获取的信息非常丰富。一些起始参考点列在以下章节中。

## C.6 参考资源

以下是一些资源，供你继续深入学习 Moose。

- 1. *Moose::Manual*（入门指南）
- 2. *Moose::Cookbook*（包含大量示例）
- 3. Moose，“一种后现代 Perl 对象系统”，<http://moose.interactive.com/en>。
- 4. Perl Maven，“使用 Moose 进行面向对象 Perl 编程”，<http://permaven.com/object-oriented-perl-using-moose>。
- 5. The Perl Review，“Moose 入门”，<http://www.theperlreview.com/articles/moose.html>。
- 6. The Sysadmin Notebook，“构建模块与测试”，<http://home.clara.net/drds/Perl/Modules.html>。

# 附录 D：Perlbrew、CPAN 和 cpanm

作者：Alastair McGowan-Douglas

![](img/8556abcb353c0991f12099420ec28735_826_0.png)

Perl 在 UNIX 系统上是预装的。通常你会发现预装版本比最新的 Perl 发行版要旧，在某些情况下甚至会有细微差别。这个 Perl 版本是由系统维护者设计的，旨在与系统的其余部分协同工作。当你安装包（例如通过系统包管理器）时，你安装的包已经针对系统安装的 Perl 版本进行了测试。

许多这样的包是 CPAN（Comprehensive Perl Archive Network，综合 Perl 归档网络）上可用模块的预编译和测试版本。这允许你使用这些模块和该版本的 Perl 在你的系统上编写自己的脚本和应用程序。

这很好用，直到你想要升级 Perl 或安装你的包管理器中不存在的模块。升级 Perl 是值得的，以便获得最新的错误修复和功能。从 CPAN 安装模块是 Perl 编程的基石；如果你无法从 CPAN 获取内容，你会发现自己在重复造轮子，编写不可移植的代码，并且无法使用其他依赖 CPAN 模块编写的脚本。

升级和安装是两个独立的过程，它们通过两种不同的方式解决，但彼此相关。

## D.1 CPAN 和 @INC

CPAN（传统上被称为 *the* CPAN；但我们通常将其视为专有名词）是所有社区提交代码存放的地方，也是所有核心以外模块的发现、获取和安装之地。在现代 Perl 中，从 CPAN 查找和安装模块的能力不仅受到鼓励，更是必不可少的。没有它，你将编写重复他人以前犯过且已修复错误的代码。由于你没有使用封装 Perl 函数以实现可移植性的模块，你的脚本将不可移植。你将无法使用大量使用模块的他人脚本。总之，你将把 Perl 当作一种粗笨的工具，而不是它可以成为的瑞士军刀，并且如果你试图解决一个已经解决的问题而遇到困难，你会发现社区不愿帮助你。

### D.1.1 查找模块

在编写代码时，先搜索 [http://metacpan.org/](http://metacpan.org/) 看你的问题是否以前已被解决，是很有价值的。如果是，你可以下载并使用该模块。如果不是，请考虑以通用方式解决你的问题，这样你就可以将你的模块上传到 CPAN，供未来的开发者使用你刚才尝试过的解决方案。

### D.1.2 使用模块

当你 *use Module;* 时，Perl 会在各个位置查找 *Module.pm*，并加载找到的第一个。如果它完全找不到，你会得到一个编译时错误：

```
use Module;
Can't locate Module.pm in @INC (you may need to install the Module module)
```

（这个特定的错误信息是在 5.18 中引入的；在此版本之前，它没有提供关于安装模块的提示。）

use 指令定义了一个依赖关系；从语义上讲，它表示相关脚本在没有指定模块的情况下无法运行。因此，Perl 在缺少模块的情况下拒绝继续执行。该消息指出该文件未在 @INC 中找到，你会认出 @INC 是 Perl 数组的名称，@INC 确实是一个数组；该数组包含模块的所有搜索路径。

你可以通过将其作为普通数组打印内容，或者询问 *perl -V* 来列出内容，从而检查 @INC 的内容：

```
$ perl -E'say for @INC;'²
/etc/perl
/usr/local/lib/perl/5.18.2
/usr/local/share/perl/5.18.2
...
<snippet>

$ perl -V
Summary of my perl5 (revision 5 version 18 subversion 2) configuration:
```

1. 在撰写本文时，传统的 CPAN 搜索站点（[http://search.cpan.org](http://search.cpan.org)）在可用和不可用之间波动。该站点正在被逐步淘汰，因为它不是由社区运营的——代码不可用，且社区无法访问托管该站点的主机。新站点 metacpan 可以在 github 上获取，地址为 [https://github.com/CPAN-API](https://github.com/CPAN-API)。
2. -E 是 5.10 中引入的一个新选项，等同于 `-c/use feature \'5.10\''`。-E 会开启 5.10 中引入的所有功能。在这里，我们使用它以便使用 say。

## CPAN 和 @INC

```
Platform:
osname=linux, osvers=3.2.0-58-generic, archname=x86_64-linux-gnu-thread-multi
...
<snip>
...
Compiled at Mar 27 2014 16:30:28
@INC:
   /etc/perl
   /usr/local/lib/perl/5.18.2
   /usr/local/share/perl/5.18.2
   /usr/lib/perl5
   /usr/share/perl5
   /usr/lib/perl/5.18
   /usr/share/perl/5.18
   /usr/local/lib/site_perl
...
```

这些是 Perl 默认查找的所有目录。列出的是 Linux Mint 17 提供的 Perl 的默认输出，它自带 5.18；你的输出可能会有所不同。

当你的脚本请求模块时，Perl 会查看这些目录。然而，除了 `/` 之外，所有这些目录都是系统目录。只有 root 才能写入这些目录。其中一些目录甚至不存在！这只是一个 Perl 构建时自带的默认集合。实际存在的目录是：

```
/usr/lib/perl5
/usr/share/perl/5.18
/usr/lib/perl/5.18
/usr/share/perl/5.18
```

（当然，当前目录是存在的。）`lib` 目录中的文件是架构相关的，因此它们通常是连接 Perl 和现有 C 库的文件，或者是出于效率目的用 C 编写的文件。`share` 中的则是其他所有内容——基本上都是纯 Perl 模块。

请记住，所有这些文件都是由 `apt`（Debian 的包管理器）提供的。没有一个是用户手动安装的。如果你想要使用 CPAN 上的模块，但 `apt` 没有安装它该怎么办？

## 我已经有它了！

在某些情况下，你已经拥有你想要的模块。当你正在编写该模块时，情况通常如此，因此它实际上还没有在 CPAN 上；或者它已经在那里，但你 `updated`（更新）了它，并使用更新后的版本。

不太常见的情况是，你从 CPAN 以外的地方获取了一个模块。如果你使用的是第三方供应商的代码，这种情况可能会发生。这非常少见。第三方编写的大多数模块最终也会放到 CPAN 上，因为它们与专有软件或服务接口，这意味着公司让模块本身在 CPAN 上免费不会受到任何损失。

在所有情况下，你可以使用 Perl 的 -I 选项告诉 Perl 去哪里查找模块，该选项会在 @INC 数组前添加指定的目录。（通常你会有一分发版，其中包含一个脚本和一个包含该脚本模块的 lib 目录）。-I 选项如下所示：

```bash
$ perl -I lib example.pl
```

这是 cpanm 在安装前测试模块时使用的技术。使用 -I，包含模块的临时目录可以添加到 @INC 中，测试脚本在此上下文中运行。这确保了正在测试的模块是临时目录中的那个，而不是系统 Perl 中安装的旧版本。

为了更永久地存放你的模块位置，你可以使用 PERLLIB 环境变量。只需将其设置为一组冒号分隔的路径，就像 PATH 本身一样，这些路径也会添加到 @INC 中。

```bash
$ PERLLIB="$HOME/perl5:$$PERLLIB$$" perl example.pl
```

### D.1.3 包管理器

对于你想从 CPAN 获取的模块，如果系统拥有包管理器，首先要检查的就是它。如前所述，Debian 有 apt，RedHat 及其衍生版本有 yum，FreeBSD 有 ports。如果你有访问权限，获取系统 Perl 模块最简单的方法是通过包管理器安装。

来自包管理器的模块具有经过供应商（即最初组装操作系统的人员）测试的优势。你经常会听到术语“vendor Perl”用来指代供应商提供的系统 Perl。此外，在许多系统上，打包版本是预编译的。这意味着获取带有 C 依赖项的 Perl 模块的过程只是简单地解压它。稍后我们将看到，否则这会变得多么复杂。

然而，这种方法并非没有缺点，包括以下几点：

- 你需要 root 访问权限。如果你在企业环境中工作，你不太可能拥有这种访问权限。有时会有程序让你请求那些拥有访问权限的人为你安装，但这些过程耗时，且不一定获批。
- 它安装到系统 Perl。如果你使用的是 Perlbrew（稍后讨论），你将无法使用预打包版本，因为 Perlbrew 创建独立于供应商 Perl 的自定义 Perl 安装。
- 包管理器中的版本可能不包含你想要的功能版本。如果打包版本较旧，你将从 CPAN 获取最新版本。
- 它可能根本不存在！CPAN 上有数万个分发版，供应商包制、测试和分发每一个都是不可行的。

随着 Perl 流行度的近期复兴（“Modern Perl”运动）

