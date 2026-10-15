
Perl 构建基础的许多部分不再转换为 win32 换行符。如果出现此问题，请报告。

## 已知问题

这是一个来自 5.10.x 或 5.8.x 的未修复 Bug 列表。某些问题在 5.10.0 中已修复，或者计划包含在 perl 中。`List::util::first` 在存在 `$_` 的情况下表现异常。

某些正则表达式在与长循环一起运行时可能会变慢。

## 勘误

这是一个实际上引入 5.8.x 的更改，但在 5.10.0 中遗漏了，因此在此提到。

与 `/m` 修饰符处理相关的 Bug 修复导致了 5.8.x 和 5.10.0 之间的差异：

```
$re = qr/^bar/; "foo\n" ~ /$re/;
```

## 感谢

Perl 5.12 代表了跨越全球约两年的开发，包含了超过 750,000 行来自 200 多位作者和提交者的更改。Perl 在活跃的用户和开发者社区中继续蓬发展。以下人员做出了贡献：

Aaron Crane, Abe Timmerman, Abhijit Menon, Abigail, Adam Russell, Adriano Ferreira, AEVarfjo, Alan Grover, Alexandr Criini, Davies Avery, Andrew Rowland, Amy Armstrong, Jose Doherty, Benjamin Smith, Ben Morrow, bharanee, Bo Borg, Bo Lindberg, Gilbert, Brendan’Dea, George Greer, Charles Bailey, Chip Salzberg, Christoph Lambrecht, Chris Williams, Claes Jakobson, Craig A. Berry, Dan Dascales, Dave Mitchell, Frederick Crisman, Daniel M. Julian, Lincoln Dobson, John Dagcov, Dave Dansky, David Gott, David Wheeler, Dennis Kearsmeier, Dintelman, Peter, Dominic Dunlop, Dr.Ruud, Duke Let, Enrico Sorcelli, Eric Brice, Francis Chythomos, Florian Ragwitz, Frank Wieg, Gabor Szabo, Gene Sullivan, Geoffrey T. Dairiki, George Goossen, Gisele Aus, Foro Fuji, Graham Barr, Green, Hans Dieter Pearcey, Harmen, Merijen Brand, Hugo van der Sarden, Jan Goedacre, Igor Sutton, Inholdness, James Henry, Jerry Jedesse, James Pence, Mastros, John Dubois, Jari Aalto, Kiko Hietenami, James Vincent, Jim Cromer, Jody Belyka, John E. Malberg, John Malberg, John,, Peacock, John Peacock via, John P. Linderman, John Wright, Kou, Carl Williamson, Hio YAMASHINA, Kenichi Ishigaki, Ken Williams, Kevin Brintall, Kevin Ryder, Kurt Starsinis, Leon Brac, Libomur Rintel, Luke Marx, Marcel Gru.nauer, Marcus Holland-Morris, Mark Johnson, Dominik Marko, Martin Hash, Mikhail Kubatov, Matt Kraii, S Trout, Maya Maischen, Michael Bree, Michael Bertram, Michael G Schwarz, Michael White, Mike Giroaux, Milosz Tanski, Lenz Moritz, Nicholas Clark, Nick Nieto, Tiffany Kaye, Osvaldo Villaldo, Paul Fenwick, Paul Gaborit, Paul Green, Johnson, Paul Marquez, Philip Hazel, Philippe Bruhart, Rafael Garcia-Suarez, Rainer Tajmer, Rajesh Malmandela, Renee. Baker, Ricardo Giesner, Ricardo SIGNES, Richard Foley, Rich Rauzennahn, Rik Delaney, Rico Kankanen, Robert May, Robert C. Sanchez, Robin Baker, Sadhiro Tomoyuki, Salvador Ortiz Garcia, Sam Villain, Scott Lann, Sebastian Aphergis-Tramoni, Sergio Junior Utidar, Shlom Fish, Simon ‘codecure’ Shubert, Sysphus, Slaven Rezik, Smylers, Steffen Mueller, Steff Ullrich, Stepan Kasal, Steve Hay, Steven Schuster, Steve Peters, Tels, The Doctor, Tim Bunch, Tim Jones, Todd Rinaldo, Tom Christians, Tom Hkins, Tom Bryant, Torsten Schoenfeld, Tye McQueen, Vadim Konovalov, Vincent Pit, Yasahiro Matsumoto, Yitzack Schoen-Thennes, Yuval Kogman, Yvon Ortiz, Stefan, Zsan Ambran

由于这是从版本控制历史生成的，因此内容是不完整的。

特别地，它没有包含在 Perl 之前的版本中报告问题的（非常感谢的）贡献者的姓名，这些报告帮助 Perl 5.12.0 变得更好。要查看所有 Perl 贡献者的完整列表，请参 Perl 5.12.0 分发包中的 `AUTHORS` 文件。

我们“退休”的成员 Nicholas Clark 和 Rafael Garcia-Suarez 对他们卓越且实质性的持续贡献表示特别感谢。自 5.10.0 以来，Nicholas 个人编写了超过 30% 的补丁。Rafael 在补丁编写数量上位居第二（11%），但在提交他人编写的补丁方面遥遥第一，提交了自 5.10.0 以来该类别下 44% 的提交，且通常在为补丁作者提供大量指导后进行。这些统计数据并不能代表他们的全部贡献，但简要地表达了：没有他们，我们无法完成工作。

此版本包含的许多更改均源于 Perl 核心包含的 CPAN 模块。我们感谢整个 CPAN 社区帮助 Perl 蓬勃发展

## 报告错误

如果你发现你认为是 bug 的地方，可以检查最近发布在 comp.lang.perl.misc 新组的文章以及位于 `<@>` 的 Perl bug 数据库。在 `<@>` 即 Perl 主页上也可能有相关信息。

如果你认为你有一个尚未报告的 bug，请运行随发行附带的 `perbug` 程序。务必将你的 bug 缩减为一个微小但足够的测试用例。你的 bug 报告以及 `perl -v` 的输出将被发送给 Perl 移植团队进行分析。

如果你报告的 bug 具有安全影响，导致不宜发送到公共存档的邮件列表，请将其发送到 `<security-perl@perl.org>`。这指向一个关闭订阅且不存档的邮件列表，其中包含所有核心提交者，他们能够帮助评估问题影响、制定解决方案，并协助在所有支持 Perl 的平台上发布补丁，以缓解或修复该问题。请仅将此地址用于 Perl 核心的安全问题，而不要用于在 CPAN 上独立分发的模块。

## 参见

查看 `Changes` 文件以了解如何查看更改的详尽细节。

查看 `INSTALL` 文件了解如何构建 Perl。

查看 `README` 文件了解通用事项。

查看 `Artistic` 和 `Copying` 文件获取版权信息。

```
<CHANGELOG> 用于列出此版本后发现的问题列表，以及已知与此版本不兼容的 CPAN 模块列表。
```

## PERL5121DELTA

### 名称

`perl5121delta` - perl v5.12.1 的新特性

## 描述

本文档描述了 5.12.0 版本与 5.12.1 版本之间的差异。

如果你正在从 5.10.1 等较早版本升级，请先阅读 `perl5120delta`，它描述了 5.10.1 和 5.12.0 之间的差异。

## 不兼容的更改

与 5.12.0 没有没有刻意的共同更改。如果存在与 5.12.0 的任何不兼容之处，它们都是 bug。请报告它们。

## 核心增强

除了下面列出的错误修复外，此版本核心语言不应有任何用户可见的更改。

## 模块与指令言

### 指令言更改

我们修复了从 `version` 导出 `is_strict` 和 `is_lax` 的问题。

这些之前是通过一个包装器导出的，将它们被视为方法调用，导致了失败。它们只是函数，也被记录为函数，并且永远不被子类化，因此此补丁直接将它们作为函数导出，不再使用包装器。

### 更新模块

- 我们将 `CGI.pm` 升级到 3.49 版本，以包含对随 Perl 5.12.0 发布引入的回归问题的修复。
- 我们将 `Pod::Simple` 升级到 3.14 版本，以改进对 `\C<|>` 的解析。
- 我们对 CPANPLUS 测试套件进行了微调，以修复偶尔出现的虚假测试失败。
- 我们将 `Safe` 升级到 2.27 版本，以封装 `reval()` 和 `rdo()` 返回的代码引用。

## 现有文档的更改

- 我们在 `perlpolicy.pod` 中添加了新的维护发布策略
- 我们在 `perlpodspec` 的 POD 规范中阐明了多括号结构
- 我们在 `perdiag.pod` 中补充了关于 `:=` 警告的缺失说明
- 我们删除了 `perlunit` 中关于 Perl 中所有文本字符串都是 Unicode 字符串的错误声明
- 我们更新了 `perrepository/mirrors/perl` 中的 Github 镜像链接，而非 `github/perl`
- 我们修复了 `perl514delta.pod` 中的一个微错误
- 我们用 `given/when` 替换了对废弃 `Switch.pm` 的提及
- 我们改进了 `perlrun` 中关于 `$sitelibexp/sitecustomize.pl` 的文档
- 我们修正了 `permodlib.pod`，之前无意中遗漏了一些模块
- 我们更新了 `perlfunc.pod` 中关于 `require` 的文档，涉及将 Perl 代码放入 `@TNC`
- 我们恢复了 `perfunc` 中一些被错误删除的关于 `quotemata` 的文档
- 我们修复了 `perlutil.pod` 中的一个 a2p 示例
- 我们在 `perport.pod` 的空白处填补了 Perl 5.12 的发布日期
- 我们修复了多个 `perdelta` 文件中的损坏链接
- `Carp.pm` 的文档现在包含了核心提交者
- 我们修复了 CPAN 上 `perlunit` 中关于 Perl 中所有文本字符串都是 Unicode 字符串的错误声明
- 我们更新了 `INSTALL` 并增加了关于通用公共许可证（GPL）的说明

## 测试

### 测试改进

- `t/select.t` 在 Windows 上不再受时钟抖动影响
- `t/blib.t` 和 `t/locale.t`：针对 Darwin 的修复
- `t/build`：针对 OpenSUSE 的修复
- `t/perldb.t`：针对 Win32 的修复

## 安装与配置

### 配置改进

- 我们更新了 `INSTALL` 关于通用公共许可证的内容

## 修复

- 处理方式的一个 bug 会导致崩溃。这发生在最后一行且该行以分号结尾时。
- 我们修复了导致 `\N{}` 跟随单个 `.` 解析错误的 bug。
- 我们修复了导致不带参数的 `when(scalar)` 不被视为语法错误的 bug。
- 我们修复了 Perl 5.12.0 中引入的对紧跟标签的处理的回归。
- 我们修复了 Perl 5.10.1 中正则表达式折叠字符不区分大小写的匹配回归。

## 平台特定说明

### HP-UX

Perl 现在允许使用 `-Duse64bitint` 而不会提升到 `use64bitall`。

### AIX

Perl 现在可以在 AIX 4.2 上构建。更改是为了 AIX 4.2 缺乏 IPv6 支持以及对 POSIX `sigaction()` 支持有限。

### FreeBSD 7

FreeBSD 7 不再包含 `/usr/bin/objformat`。在构建时，Perl 现在跳过 7 版及以上版本的检查，并假设为 ELF。

### VMS

现在可以在旧的（7.3-2 之前的）VMS 系统上构建扩展。DCL 符号长度在七年前还限制为 1K，但没有特殊的理由阻止这些旧系统配置和构建 Perl。

我们修复了之前在 VMS 上损坏的 `-useperl` 构建。我们之前检查了一个在禁用 perlio 的默认情况下不存在的变量。现在我们只在它存在时进行检查。

我们修复了 `configure.com` 中的 `-Uuseperlio` 命令行选项。以前只有当你通过交互方式回答所有问题并明确回答“否”时它才会起作用。

# 已知问题

`List::Util::first` 在存在作用域 `$_` 时（通常由 `my $_` 或由 `given` 隐式引入）表现异常。每次迭代设置的变量是包变量 `$$`，而不是作用域 `$_`。

类似的问题可能出现在其他提供将块作为第一个参数的模块中，例如：

```perl
foo { ... $_} list
```

另参见：`< >`

`Module::Load::Conditional` 和 `version` 之间存在一种不幸的交互，这可能导致 CPANPLUS 在遇到无法解析的版本字符串时崩溃。从 CPAN 升级到 CPANPLUS 0.9004 或 `Module::Load::Conditional` 0.38 即可解决此问题。

# 致谢

Perl 5.12.1 代表了自 Perl 5.12.0 以来大约四周的开发，包含了来自 28 位作者的 142 个文件中约 4,000 行更改。

得益于充满活的用户和开发者社区，Perl 在其第三个十年继续蓬勃发展。以下人员贡献了成为 Perl 5.12.1 的改进：

AEvar Arnfjo.rd- Bjarmason, Chris Williams, chromatic, Craig A. Berry, David Golden, Father Chrysostostomos, Florian Ragwitz, Frank Wiegand, Gene Sullivan, Goro Fuji, H.Merijen Brand, James E Keenan, Jan Dubois, Jesse Vincent, Josh Ben J, Karl Williamson, Leon Brocade, Michael Schwern, Nga Tang Chan, Nicholas Clark, Niko Tyni, Philippe Bruhat, Rafael Garcia-Suarez, Ricardo Signes, Steffen Mueller, Todd Rinaldo, Vincent Pit 和 Zefram。

# 报告 bug

如果你发现认为这是一个 bug，可以检查最近发布在 comp.lang.perl.misc 新闻组的文章以及 `.` 处的 perl bug 数据库。Perl 主页也有相关信息。

如果你认为你有一个未报告的 bug，请运行发布版本自带的 `perlbug` 程序。请确保将你的 bug 简化为一个微但足够的测试用例。你的 bug 报告同 `perl -v` 的输出将发送给 Perl 移植团队进行分析。

如果你报告的 bug 具有安全影响，不适合发送到公共存档的邮件列表，请将其发送至 `.`。这指向一个关闭订阅且不存档的邮件列表，包含所有核心提交者，他们能够帮助评估问题影响、制定解决方案，并协助在所有支持 Perl 的平台上发布补丁以缓解或修复问题。请仅将此地址用于 Perl 核心的安全问题，而不要用于在 CPAN 上独立分发的模块。

## 另请

查看 `Changes` 文件以了解如何查看更改的详尽细节。

查看 `INSTALL` 文件以了解如何构建 Perl。

查看 `README` 文件获取通用内容。

查看 `Artistic` 和 `Copying` 文件获取版权信息。

# PERL5122DELTA

### 名称

`perl5122delta` - perl v5.12.2 的新特性

## 描述

本文档描述了 5.12.1 版本与 5.12.2 版本之间的差异。

如果你是从较早的主主版本（例如 5.10.1）升级，请先阅读 `perl5120delta`（它描述了 5.10.1 和 5.12.0 之间的差异），以及 `perl5121delta`（它描述了 5.12 稳定发布系列早期的更改）。

# 不兼容更改

没有故意与 5.12.1 不兼容的更改。如果存在任何，它们都是 bug，欢迎报告。

# 核心增强

除了下面列出的 bug 修复外，此版本中核心语言不应有用户可见的更改。

# 模块和编译指令

## 新模块和编译指令
