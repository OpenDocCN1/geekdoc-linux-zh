
- `perlrun` 经过了大量的清理。最显著的是明确了 `-0` 标志的 `-0x...` 部分，并修正且扩展了关于环境变量的最后章节。

### POSIX

- 修正了 `WIFEXITED`, `WEXITSTATUS`, `WIFSIGNALED`, `WTERMSIG`, `WIFSTOPPED` 和 `WOPSIG` 的调用文档。

## 诊断

对诊断输出（包括警告和致命错误消息）进行了以下添加或更改。诊断消息完整列表请参见 `perldiaj`。

## 新诊断

无

## 现有诊断的变更

无

# 工具变更

无

# 配置与编译

`regexp.h` 已通过修改，以兼容 GCC 的 `-werror` 选项，某些包含 perl 头文件的项目会使用该选项。

# 测试

- 修复了 `dist/Locale-Maketext/t/09_compile.t` 中可能根据环境发生的某些测试失败。[`perl #89896`]

- 延长了 `t/re.t` 的看门狗计时器，以适应 SH-4 系统，这些系统无法在之前的计时器超时前完成测试。

# 平台支持

## 新平台

无

## 已停止的平台

无

## 特定平台说明

### Solaris

- 修正了在 Solaris 9 和 Solaris 10 上构建 Perl 所需的 Solaris 软件包列表。

### Mac os x

- 更新了 `lib/locale.t` 测试脚本，以支持即将发布的 Lion 版本。

- 明确了 Mac os x 特定的编译指令。

### Ubuntu Linux

- 更新了 `ODBM_File` 安装过程，使用了 Ubuntu 原生系统的新库路径。

# 内部变更

格式的编译表示现在通过其 `PERL_MAGIC_fm` 的 `mg_ptr` 存储。此前它存储在字符串缓冲区中，位于 `SvLEN()` 之外的字符串末。`SvCOMPILED()` 和 `SvCOMPILED_{on,off}()` 现在仅用于 `xs` 代码的兼容。第一个始终为 0，另外两个现在是空操作。

# 修复

- 修复了一个如果后续两个哈希元素被删除，会导致“Use of freed value in iteration”错误。[`perl #85026`]

- 将相同的常量子程序同时传递给 `index` 和 `formline` 不再导致其中一个失败。[`perl #89218`]

- `5.14.0` 在正则表达式字符类（如 `[\w\s]`）中引入了一些内存泄漏，现已修复。

- 正则表达式匹配中的一个边缘情况可能会导致循环。这种情况仅发生在 `/i` 匹配具有多字符折叠的字符时，随后是另一个具有从折叠剩余部分开始的多字符折叠的字符，外加更多字符。

```
"\s\N{U+DF}" ~ /\x{DF}foo/i
```

是其中一种情况。`\xD` 折叠为 `ss`。

- 修复了多个 Unicode 大小写折叠 Bug。

- 新的（`5.14.0` 引入）正则表达式修饰符 `/a` 在重复 `/aa` 时，禁止 ASCII 范围之外的字符匹配该范围内的字符在 `/i` 下进行匹配。这在某些情况下不起作用，均涉及选择，例如：

```
"\N{KELVIN SIGN}" ~ /k|/
```

- 问题已修正。

# 致谢

感谢于活跃的用户社区，Perl 在进入第三个后继续蓬发展。以下人员已知做出贡献：

Bo Lindbergh, Claudio Ramirez, Craig A. Berry, David Leadbeater, Father Chrysostomos, Jesse Vincent, Jim Cromie, Justin Case, Karl Williamson, Leo Lapworth, Nicholas Clark, Nobuhiro Iwamatsu, Zban Ambrus.

## 报告 Bug

如果你发现了认为是一个 Bug，请运行随版本发布的 `perbug` 程序，并附带 `perl -v` 的输出，将发送给 Perl 移植团队进行分析。如果你认为有一个未报告的 Bug，请检查公开存档的邮件列表。请仅将此地址用于 Perl内核的安全问题，不要用于 CPAN 上独立分发的模块。

## 参见

- 查看 `Changes` 文件了解变更内容。

- 查看 `INSTALL` 文件如何构建 Perl。

- 查看 `README` 文件获取通用信息。

- 查看 `Artistic` 和 `Copying` 文件获取版权信息。

# 弃用公告

自 `5.14.0` 以来没有新的弃用项。

# 模块与指令符 (PRAGMATA)

# 新模块与指令符

无

# 更新的模块与指令符

`CPAN` 已从版本 `1.9600` 升级到 `1.9600_01`。

`CPAN::Distribution` 已从版本 `1.9602` 升级到 `1.9602_01`。

从 `CPAN` 版本 `1.9800` 回传了错误修复。确保了在 `dynamic_config` 为 `true` 的情况下，能够正确从 CPAN Meta 文件中检测 `configure_requires` 前置依赖。[`rt.cpan.org #68835`]

同时确保了 `configure_requires` 仅在 META 文件中检查，而不会在删除 `configure_requires` 的 MYMETA 生成过程中进行检查。

`Encode` 已从版本 `2.42` 升级到 `2.42_01`。

请参阅“安全”。

`File::Glob` 已从版本 `1.12` 升级到版本 `1.13`。

请参阅“安全”。

`PerIO::scalar` 已从版本 `0.11` 升级到 `0.11_01`。

它修复了当 `$scalar` 是写时复制（cow）标量时，`open my $fh, ">", \scalar` 不生效的问题。

# 已移除的模块与指令符

无

# 平台支持

# 新平台

无

# 已停止的平台

无

# 平台特定说明

`HP-UX PA-RISC/64` 现在支持 `gcc~4.x`

-- 一个针对 `socketsize` 的修复使得测试套件在 HP-UX PA-RISC 64 位构建上能够通过。

在 OS X 10.7 Lion 和 Xcode 4 上进行构建已恢复工作。

-- 构建系统已更新，以适配 Mac OS x 10.7 下的构建工具。

# 错误修复

在 `@INC` 过滤器（由 `@INC` 中的子程序返回的子程序）中，`$_` 曾出现行为异常：如果从子程序返回，它将不会被复制，而是返回变量本身；释放 `$_`（例如使用 `undef *`）会导致 perl 崩溃。此问题已修复 [`perl #91880`].

Perl 5.10.0 引入了一些错误的逻辑，导致当输入字符串为空时，`pack` 模板中间的 `"U*"` 等同于 `"U0"`。此问题已修复 [`perl #90160`].

当从 `DB` 包调用 `caller` 时，如果 `@DB::$args` 在第一次调用 `caller` 后被赋值，则 `caller` 不再发生内存泄漏。`Carp` 曾会触发此 bug [`perl #97010`]. `\utf8:::decode` 引入了一个严重的 bug，该 bug 会原地修改写时复制标量的字符串缓冲区（即跳过复制）。这可能导致哈希表中有两个键相同的元素 [`perl #91834`].

对绑定（tied）变量进行本地化会导致其在包含写时复制字符串时变为只读。

包含写时复制数值的受限哈希元素（见 `fields` 指令符）无法被删除，此类哈希也无法清空（`%hash = ()`）。

锁定作为 glob 副本的哈希元素不再会导致后续对其的赋值损坏 glob 副本。

修复了 `5.14.0` 中涉及正则表达式修饰符 `/aa` 与 `\b` 转义序列组合的恐慌（panic）[`perl #95964`].

# 已知问题

这是一个自 `5.12.0` 以来出现回归的某些重大未修复 bug 列表。

`PERL_GLOBAL_STRUCT` 存在损坏。

自 perl `5.14.0` 以来，无法使用 `-DPERL_GLOBAL_STRUCT` 进行构建。这意味着 perl 目前无法在任何要求以此方式构建的平台上运行，包括 Symbian。

虽然 `PERL_GLOBAL_STRUCT` 在最近的 perl 开发版本中已再次工作，但其在 Symbian 上再次恢复工作尚未得到验证。

## BUG 修复

修复了在 `5.14` 版本中引入的回归问题：在 `/i` 正则表达式匹配中，如果模式为 UTF-8 编码而目标字符串不是，且一个 Latin-1 字符位于字符串中本应匹配模式的字符之前，会导致匹配意外失败。[`perl #101710`]

不区分大小写的正则表达式模式匹配在处理非 UTF-8 编码的字符串时，不再从第一个可能的位置开始扫描。这导致了 `"\xf\x(F800)" =~ /f/i` 匹配失败。

`sitecustomize` 支持已能够感知 `-Duserelocatableinc`，因此对智能匹配运算符 `--` 进行了更改，使得在任何 `--object` 操作中，右侧具有优先级。

修复了污染支持（tainted support）中的一个 Bug：对污染常数执行 `index()` 操作会导致所有其他常量也变为污染状态。[`perl #64804`]

修复了 perl `5.12` 中引入的回归问题，该问题导致污染错误未能通过 `die()` 正确传播。[`perl #111654`]

修复了 perl `5.14` 中引入的回归问题，在该版本中，`/[:lower:]]/i` 和 `/[:upper:]]/i` 不再匹配相反的大小。[`perl #101970`]

## 致谢

Perl `5.14.3` 代表了自 Perl `5.14.2` 之后约 12 个月的开发，包含了来自 22 位作者的 64 个文件中的约 2,300 行更改。

得益于活跃的用户和开发者社区，Perl 在其第三个十年继续蓬勃发展。以下人员已知对成为 Perl `5.14.3` 的改进做出了贡献：

Abigail, Andy Dougherty, Carl Hayter, Chris ‘BinGOs’ Williams, Dave Rolsky, David Mitchell, Dominic Hargreaves, Father Chrysostomos, Florian Ragwitz, H.Merijn Brand, Jilles Tjoelker, Karl Williamson, Leon Timmermans, Michael G. Schwern, Nicholas Clark, Niko Tyni, Pino Toscano, Ricardo Signes, Salvador Fadin-o, Samuel Thibault, Steve Tony Cook.

由于上述列表是从版本控制历史中自动生成的，因此几乎肯定是不完整的。特别是，它没有包括那些向 Perl 错误跟踪器报告问题的贡献者（对此深表感谢）。

此版本包含的许多更改均源于 Perl 核心包含的 CPAN 模块。我们感谢整个 CPAN 社区帮助 Perl 蓬勃发展。

有关所有 Perl 历史贡献者的完整列表，请参阅 Perl 源码发行版的 `AUTHORS` 文件。

## 报告 Bug

如果你发现认为可能是 Bug 的，可以检查 `comp.lang.perl.misc` 新组最近发布的文章以及 `perbugs.org` 上的 Perl 错误数据库。Perl 主页也可能有相关信息。

如果你认为你有一个未报告的 Bug，请运行发行版附带的 `perbug` 程序，以及 `perl -v` 的输出，这些将发送给 Perl 移植团队进行分析。

如果你报告的 Bug 具有安全影响，不适合发送到公共存档的邮件列表，请将其发送至 `security-bugs@lists.perl.org`。这是一个封闭的订阅且不存档的邮件列表，包含了所有核心提交者，他们将帮助评估问题影响、制定解决方案，并协助在所有支持 Perl 的平台上发布补丁，以缓解或修复问题。请仅对 Perl 核心的安全问题使用此地址，切勿用于在 CPAN 上独立分发的模块。

## 另请参

- 查看 `Changes` 文件以了解如何查看更改的详尽细节。

- 查看 `INSTALL` 文件以了解如何编译 Perl。

- 查看 `README` 文件了解通用事项。

- 查看 `Artistic` 和 `Copying` 文件以获取版权信息。

## PERL5144DELTA

- 名称：`perl5144delta` - perl v5.14.4 的新特性。

## 描述

本文档描述了 `5.14.3` 版本与 `5.14.4` 版本之间的差异。

如果你是从 `5.12.0` 等更早版本升级，请先阅读 `perl5140delta`，它描述了 `5.12.0` 和 `5.14.0` 之间的差异。

## 核心增强

自 `5.14.0` 以来没有更改。

## 安全

此版本包含一个重大、一个中级和多个微级安全修复。后者主要是为了让测试套件能够通过 clang 编译器的地址检测器（address sanitizer）顺利运行。

### CVE-2013-1667：任意哈希键内存耗尽

通过精心构造的哈希键集合（例如 URL 参数），可能会导致哈希消耗大量内存和 CPU，从而可能实现拒绝服务攻击（DoS）。该问题已修复。

### Encode 中的内存泄漏

`Encode.xs` 中的 UTF-8 编码实现存在内存泄漏，已修复。

### [perl #111594] Socket::unpack_sockaddr_un 缓冲区溢出

在拷贝 `sockaddr` 缓冲区时可能会发生缓冲区溢出。该问题是无害的且已修复。

### [perl #111586] SDBM_File：差一错误

`Encode.xs` 中的 UTF-8 编码实现存在内存泄漏，已修复。

# 报告 bug

如果你发现你认为是一个 bug 的地方，可以检查最近发布在 comp.lang.perl.misc 新闻组的文章以及 . 处的 Perl bug 数据库。在 . 处的 Perl 主页上也可能有相关信息。

如果你认为你有一个尚未报告的 bug，请运行随你的版本附带的 `perbug` 程序。务必将你的 bug 精简为一个极小但充分的测试用例。你的 bug 报告连同 `perl -v` 的输出将被发送给 Perl 移植团队进行分析。

如果你报告的 bug 具有安全影响，导致其不宜发送到公共存档的邮件列表，请将其发送到 `security@perl.org`。该地址指向一个封闭的订阅且不存档的邮件列表，其中包含了所有核心提交者，他们能够帮助评估问题的影响、制定解决方案，并协助协调补丁的发布，以在所有支持 Perl 的平台上缓解或修复问题。请仅对 Perl 核心的安全问题使用此地址，而不要用于在 CPAN 上独立分发的模块。

# 另见正文

查看 *Changes* 文件可以了解如何查看更改的详尽细节。

查看 *INSTALL* 文件可以了解如何构建 Perl。

查看 *README* 文件可以通用内容。

查看 *Artistic* 和 *Copying* 文件可以获取版权信息。

# PERL5160DELTA

+ > 名称

`perl5160delta` - perl v5.16.0 的新特性

## 描述

本文描述了 `5.14.0` 版本与 `5.16.0` 版本之间的差异。

如果你正在从 `5.12.0` 等较早版本升级，请先阅读 `perl5140delta`，该文件描述了 `5.12.0` 和 `5.14.0` 之间的差异。

此版本中的某些 bug 修复已回波到 `5.14.x` 的后续版本中。这些修复通过括号中的 `5.14.x` 版本指示。

## 注意

随着 Perl `5.16.0` 的发布，`5.12.x` 系列版本现在已超出支持期。未来可能会发布 `5.12.x` 版本，但仅在出现严重安全问题的情况下。Perl `5.12` 或更早版本的用户应考虑升级到较新的 Perl 版本。

此策略在 `perlpolicy` 中有更详细的描述。

# 增强

use VERSION

从此版本开始，像 `use v5.16` 这样的版本声明会在启用新特性包之前禁用所有先前的特性。这意味着以下内容成立：

```perl
use v5.016; # 这里仅开启了 51 个特性
use v5.014; # 这里仅开启了 5.14 特性
not (not 5.16)
```

`use v5.12` 及以上继续启用 `strict`，但显式的 `strict` 和 `no strict` 会覆盖版本声明，即使它们是先出现的：

```perl
no strict; use v5.012; # 这里没有 strict
```

现在有一个新的“default”特性包，它代表了在任何版本声明或 `use feature` 出现时启用的特性集。`5.10` 以下的版本声明现在会启用“default”特性集。这实际上并没有改变 `use v5.8` 的行为，因为添加到“default”中的特性是那些在可以关闭之前传统上默认启用的特性。

`no feature` 会重置为默认特性集。要禁用所有特性（这可能是一个很特殊的请求，因为这可能不符合任何语义集），你可以写 `no feature 'all'`.

在 `use v5.16` 下 `$` 现在被禁用了。它是默认特性集的一部分，可以通过 `use feature 'array_base'` 开启或显式开启。

__SUB__

新的 `__sub__` 令牌在当前的 `current__sub__` 特性（见 `feature`）或 `use v5.16` 下可用，它返回指向当前子程序的引用，这使得编写递归闭包变得更容易。

# 新及改进的内置函数

### 更一致的 eval

`eval` 操作符有时将字符串参数视为字符序列，有时将其视为字节序列，取决于内部编码。内部编码本不应该产生任何区别，但存在依赖这种不一致性的代码。

新的 `unicode_eval` 和 `evalbytes` 特性（在 `use v5.16.0` 下启用）解决了这个问题。`unicode_eval` 特性使 `$string` 始终将字符串视为 Unicode。`evalbytes` 特性提供了一个名为 `evalbytes` 的函数，它始终将其参数视为字节字符串进行评估。

这些特性还修复了源过滤器泄漏到外层动态作用域的异常。

更多细节请见 `feature`.

### substr lvalue 重构
