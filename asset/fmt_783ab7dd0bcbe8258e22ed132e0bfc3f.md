
这将使用 `cpp` 扩展宏。不要被结果吓到。

## AUTHOR

本文档最初由 Nathan Torkington 编写，由 perl5-porters 邮件列表维护。

## PERLHACKTUT

### NAME

`perlhacktut` - 逐步一个简单的 C 代码补丁的创建

## DESCRIPTION

本文将带你通过一个简单的补丁示例。

如果你还没有读过 `perhlack`，请先去读它！你可能也想读读 `perlsource`。

完成这里后，接下来请查看 `perlhacktips`。

## EXAMPLE OF A SIMPLE PATCH

让我们从头到尾来看一个简单的补丁。

这是 Larry 建议的内容：如果 `u` 是 `pack` 期间的第一个活跃格式（例如，`pack "U3C8", @stuff`），则生成的字符串应该被视为 UTF-8 编码。

如果你正在处理 Perl 仓库的 git clone，你可能想为你的更改创建一个分支。这将使得创建一个正确的补丁变得简单得多。关于如何执行此操作，参见 `perglit`。

## Writing the patch

我们如何准备修复它？首先，我们定位相关代码——`pack` 发生在运行时，它会在 `pp` 文件中。果然，`pp_pack` 在 `pp.c` 中。由于我们要修改这个文件，让我们把它复制到 `pp.c`。

[好吧，在编写本教程时，它在 `pp.c` 中。现在它已经与 `pp_unpack` 一起分到了单独的文件 `pp_pack.c` 中]

现在让我们来看看 `pp_pack`：我们将一个模式传入 `pat`，并遍历该模式，依次将每个字符存入 `datatype`。然后对于每个格式字符，我们吞掉模式中的所有其他参数（字段宽度、星号等），并将下一个输入块转换为指定的格式，将其添加到输出的 `sv cat` 中。

我们如何知道 `u` 是 `pat` 中的第一个格式呢？嗯，如果我们有一个指向 `pat` 开头的指针，那么当我们看到 `u` 时，我们仍然处于字符串的开头。所以，这里是 `pat` 设置的地方：

```
STRL fromlen; char *pat = Svpvx(**MARK, fromlen); char *patend = pat + fromlen; I32 datatype; SV *fromstr;
```

我们在这里还会有另一个字符串指针：

```
STRL fromlen; char *pat = Svpvx(**MARK, fromlen); char *patend = pat + fromlen; char *patcopy; I32 len; datatype;
```

描述我们刚刚做的更改。相关位置是 `pod/perlfunc.pod`；再次，我们创建一个副本，然后我们将此文本插入到 pack 的描述中：

=item * 如果模式以 C<U> 开头，则生成的字符串将被处理为 UTF-8 编码的 Unicode。你可以通过初始的 C<U0> 强制对字符串进行 UTF-8 编码，随后的字节将被解释为 Unicode 字符。如果你不希望发生这种情况，可以用 C<C0>（或任何其他）开始你的模式，以强制 Perl 不对你的字符串进行 UTF-8 编码，然后在模式中的某处跟随一个 C<U*>。

# 提交

有关如何提交此补丁的详情，请参见 perlhack。

# 作者

此文档最初由 Nathan Torkington 编写，由 perl5-porters 邮件列表维护。

# PERLHAIKU

## NAME

`perlhaiku` - Haiku 上的 Perl 5.10+ 版本

## 描述

此文件包含如何为 Haiku 编译 Perl 的说明，并列出了已知问题。

# 构建与安装

构建过程完全完全标准的：

```
./Configure -de
make
make install
```

使 perl 可执行并为 libperl 创建一个符号链接：

```
chmod a+x /boot/common/bin/perl; cd /boot/common/lib; ln -s perl5/5.22.0/BePC-haiku/CORE/libperl.so .
```

将 5.22.0 替换为您相应的 Perl 版本。

## 已知问题

在 Haiku 修订 28311 中遇到了以下问题：

- 目前尚无法编译带有线程支持的 Perl。
- `ext/Socket/tocketpair.t` 测试失败。更具体地说：使用数据报套接字的子测试失败了。Haiku 尚未实现 Unix 数据报套接字。
- `ext/Sys/Syslog/t/syslog.t` 测试的一个子测试失败。这是由于 Haiku 尚未实现对 `/dev/log` 的支持。
- `lib/Net/Ping/t/450_service.t` 和 `lib/Net/Ping/t/510_ping_udp.t` 测试失败。这是由于 Haiku 网络栈实现中的错误。

# 联系方式

对于 Haiku 特有的问题，请联系 HaikuPorts 开发人员：<>

最初的 Haiku 移植由 Ingo Weinhold <> 完成。

最后更新：2008-10-29

# PERLHIST

## NAME

`perlhist` - Perl 历史记录

## 描述

本文旨在记录 Perl 源码发布版本。

# 引言

Larry Wall 简述 Perl 历史：

Perl 0 向我的同事引入了 Perl。Perl 1 向世界引入了 Perl，并将 `/\...\}/` 改为 `/(...)//`。（Dan Faigin 仍然没有原谅我 ::\\）Perl 2 引入了 Henry Spencer 的正则表达式包。Perl 3 引入了第一本《Camel》（嵌入空字节）。Perl 4 引入了第一本《Camel》。真的。我们大多数时候只是更改了版本号，以便书籍可以引用 4.000。Perl 5 引入了其他一切，包括引入其他所有内容的能力。

# 南瓜的守护者

Larry Wall, Andy Dougherty, Tom Christiansen, Gurusamy Sarathy, Graham Barr, Jarkko Salzenberg, Tim Bunce, Malcolm Beattie, Schwamy, Hietaniemi, Hugo van der Sand, Michael Schwerm, Rafael Garcia-Suarez, Nicholas Clark, Richard Clamp, Leon Brocard, Dave Mitchell, Jesse Vincent, Ricardo Signes, Steve Hay, Matt T Trout, David Golden, Florian Ragwitz, Tatsuhiko Miyagawa, Chris bin-Williams, Zefram, AEvar Arfjo-rd, Bjarmason, Stevan Little, Dave Rolsky, Max Maisichein, Abigail, Jesse Luehrs, Tony Cook, Dominic Hargreaves, Aaron Crane, Aristotle Pagaltzis, Matthew Horsfall, Peter Martini, and Sawyer X.

南瓜？

[来自 Perl 源码发行中的 Porting/pumpkin.pod]

Chip Salzenberg 因此归功，同时也致敬了他的同事 David Croy。我们传过各种名称（接棒、令牌、烫手芋），但没有一个流行起来。然后，Chip 问：

[开始引用]

谁有南瓜补丁？

解释一下：David Croy 曾告诉我，在之前的工作中有一个磁带驱动和多个使用它进行备份的系统。但他们没有使用高科技排除软件，而是使用了一种低科技方法来防止多个同时备份：一个填充的南瓜。除非拥有“备份南瓜”，否则没人允许进行备份。

[结束引用]

这个名字流传了下来。南瓜的持有者有时被称为 pumpkin（为了保持来源浮动吗？）或 pumpkinkeer（幕后操纵者）。
