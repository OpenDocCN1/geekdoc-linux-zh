
`/usr/local/lib/perl/5.18.2`

`/usr/local/share/perl/5.18.2`

...

<snippet>

`$ perl -V`

Summary of my perl5 (revision 5 version 18 subversion 2) configuration:

```
```

1. 在撰写本文时，传统的 CPAN 搜索站点（[http://search.cpan.org](http://search.cpan.org)）在可用和不可用之间波动。该站点正在被逐步淘汰，因为它不是由社区运营的——代码不可用，且社区无法访问托管该站点的主机。新站点 metacpan 可以在 github 上获取，地址为 [https://github.com/CPAN-API](https://github.com/CPAN-API)。
2. `-E` 是 5.10 中引入的一个新选项，等同于 `-c/use feature \'5.10\''`。`-E` 会开启 5.10 中引入的所有功能。在这里，我们使用它以便使用 `say`。

## CPAN 和 `@INC`

```
Platform:

osname=linux, osvers=3.2.0-58-generic, archname=x86_64-linux-gnu-thread-multi

...

<snip>

...

Compiled at Mar 27 2014 16:30:28

`@INC`:

   `/etc/perl`

   `/usr/local/lib/perl/5.18.2`

   `/usr/local/share/perl/5.18.2`

   `/usr/lib/perl5`

   `/usr/share/perl5`

   `/usr/lib/perl/5.18`

   `/usr/share/perl/5.18`

   `/usr/local/lib/site_perl`

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

在所有情况下，你可以使用 Perl 的 `-I` 选项告诉 Perl 去哪里查找模块，该选项会在 `@INC` 数组前添加指定的目录。（通常你会有一分发版，其中包含一个脚本和一个包含该脚本模块的 `lib` 目录）。`-I` 选项如下所示：

```bash
$ perl -I lib example.pl
```

这是 `cpanm` 在安装前测试模块时使用的技术。使用 `-I`，包含模块的临时目录可以添加到 `@INC` 中，测试脚本在此上下文中运行。这确保了正在测试的模块是临时目录中的那个，而不是系统 Perl 中安装的旧版本。

为了更永久地存放你的模块位置，你可以使用 `PERLLIB` 环境变量。只需将其设置为一组冒号分隔的路径，就像 `PATH` 本身一样，这些路径也会添加到 `@INC` 中。

```bash
$ PERLLIB="$HOME/perl5:$$PERLLIB$$" perl example.pl
```

### D.1.3 包管理器

对于你想从 CPAN 获取的模块，如果系统拥有包管理器，首先要检查的就是它。如前所述，Debian 有 `apt`，RedHat 及其衍生版本有 `yum`，FreeBSD 有 `ports`。如果你有访问权限，获取系统 Perl 模块最简单的方法是通过包管理器安装。

来自包管理器的模块具有经过供应商（即最初组装操作系统的人员）测试的优势。你经常会听到术语“vendor Perl”用来指代供应商提供的系统 Perl。此外，在许多系统上，打包版本是预编译的。这意味着获取带有 C 依赖项的 Perl 模块的过程只是简单地解压它。稍后我们将看到，否则这会变得多么复杂。

然而，这种方法并非没有缺点，包括以下几点：

- 你需要 root 访问权限。如果你在企业环境中工作，你不太可能拥有这种访问权限。有时会有程序让你请求那些拥有访问权限的人为你安装，但这些过程耗时，且不一定获批。
- 它安装到系统 Perl。如果你使用的是 Perlbrew（稍后讨论），你将无法使用预打包版本，因为 Perlbrew 创建独立于供应商 Perl 的自定义 Perl 安装。
- 包管理器中的版本可能不包含你想要的功能版本。如果打包版本较旧，你将从 CPAN 获取最新版本。
- 它可能根本不存在！CPAN 上有数万个分发版，供应商包制、测试和分发每一个都是不可行的。

随着 Perl 流行度的近期复兴（“Modern Perl”运动）

## D.1.4 手动安装：CPAN

随着 CPAN 的人气增长，其活跃度也相应提升。这意味着，在许多情况下，CPAN 新增和更新发布的软件包速度比供应商（vendors）更新的速度更快。因此，供应商必须选取 CPAN 的某个快照，编译常用模块的子集，并将其分发出去。

另一种选择是手动安装模块。这基本上反转了前面提到的优点/缺点：

- 你可以拥有任何模块。
- 不需要 root 权限。
- 你可以安装到自定义的 Perl 环境中。
- 需要 C 编译器，以及 C 依赖项。
- 未经过针对你特定环境的充分测试。

从 CPAN 安装模块使用的是 Perl 自带的 `cpan` 命令，但建议获取并安装 `cpanm` 代替。`cpan` 命令可用但需要配置，而 `cpanm` 预置了各项默认值，并尽可能做到“如我所愿”（DWIM, Do What I Mean）。

首先要意识到的一点是：默认情况下，`cpan` 会尝试安装到系统 Perl 目录中。这是因为 `cpan` 本身是一个 Perl 脚本，这意味着它将使用系统 Perl 来运行！而这需要 root 访问权限。为避免这种情况，我们将使用 `local::lib` 来创建并用于 Perl 模块的本地 `lib/`。

**`local::lib`.** 即使你有 root 访问权限，使用本地 lib 也被视为最佳实践。主要原因基于一个简单的准则：系统 Perl 并非供你直接使用的。这适用于许多现代语言。系统 Perl 及其包管理器中的系统模块，都是设计用来配合系统中基于 Perl 的命令和工具工作的。如果这恰好符合你自己的需求，那很好，但一旦这些需求产生偏差，你最终仍需要采用这些技术。拥有一个你拥有完全控制权的本地环境显然要好得多，这使得在任何时候切换环境都变得简单，同时也保护你免受系统 Perl 变化的影响。

以下五个环境变量是你创建本地 Perl 环境所需的全部。启用它们后，`cpan` 可以工作在系统的任意目录上。

传统上，你的 `$HOME` 目录将用于容纳你希望在不使用 root 权限的情况下安装的模块和脚本。这被称为 *本地 Perl*（相对于系统 Perl 或供应商 Perl）。另一个常见位置是 *site Perl*，通常指你的组织常用的一组模块，因此默认安装在所有服务器上。就我们的目的而言，我们将处理最常见的情况，即在你的主目录中安装一个本地 Perl 库（*a local lib*）。

列出的五个环境变量如下：

```
PATH="/home/altreus/perl5/bin${PATH:+:$PATH}"
PERL5LIB="/home/altreus/perl5/lib/perl5${PERL5LIB:+:$PERL5LIB}"
PERL_LOCAL_LIB_ROOT="/home/altreus/perl5${PERL_LOCAL_LIB_ROOT:+:$PERL_LOCAL_LIB_ROOT}"
PERL_MB_OPT="--install_base /home/altreus/perl5"
PERL_MM_OPT="INSTALL_BASE=/home/altreus/perl5"
```
