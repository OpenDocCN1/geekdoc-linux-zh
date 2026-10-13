
- `-T`—这启用污染检查（taint checking）。在此模式下，Perl 假设所有用户输入都是被污染的或不安全的，除非程序员另行说明。这可以保护你免受他人试图利用你代码中的漏洞，在编写 CGI 程序时尤为重要。

- `-U`—这允许你在 Perl 程序中执行不安全的操作，例如以超级用户身份运行时删除目录。

- `-u`—一个可用的过时开关，用于告诉 Perl 在编译程序后转储核心（dump core）。

- `-V`—打印主要 Perl 配置值的摘要以及 `@INC` 的当前值。

- `-V:names`

此参数显示 `names` 配置变量的值。

- `-v`—打印你的 Perl 可执行文件的版本号和补丁层级。例如：

```bash
$ perl -v

This is perl, v5.8.1 built for i386-linux-thread-multi

(with 1 registered patch, see perl -V for more detail)
```

版权所有 1987-2003, Larry Wall

Perl 仅可根据艺术许可（Artistic License）或 GNU 通用公共许可证（GNU General Public License）的条款进行复制，这些许可可以在 Perl 5 源码包中找到。

Perl 的完整文档（包括 FAQ 列表）可以在此系统中通过 `man perl` 或 `perldoc perl` 找到。如果你可以访问互联网，请将浏览器指向 http://www.perl.com/（Perl 主页）。

- `-w`—这告诉 Perl 显示所有警告信息。

## 模块与 CPAN

- `-w`—告诉 Perl 显示关于程序中潜在问题的警告信息，例如仅使用一次的变量（可能是拼写错误）、在比较中使用 `=` 代替 `==` 等。这通常与 `-c` 标志配合使用进行彻底的程序检查。

```bash
$ perl -cw finalassignment.pl
```

- `-X`—这告诉 Perl 禁用所有警告信息。

- `-x 目录`—这告诉 Perl 脚本嵌入在更大的内容中（例如电子邮件）。忽略从 `#1` 开头的行之前的所有内容、包含字符串 `'perl'` 以及 `__END__` 之后的所有内容。如果指定了目录，Perl 会执行脚本前切换到该目录。

### 注意

本节多次提到了 Perl 文档。对于 `perldbug`、`perlun`、`permod` 和 `perldib`，只需在提示符输入 `perdoc perldoc` 即可。你可以在 http://www.cpan.org/doc/index.html 或任何 CPAN 站点在线查看所有的 Perl 文档。CPAN 是全面 Perl 存档网络（Comprehensive Perl Archive Network）。更多信息请参阅本章后后的“模块与 CPAN”部分。

Perl 文档使用 POD（纯文本文档）编写，并可以使用帮助 Perl 的 `pod2` 工具转换为任何其他格式，如 Tex、ASCII 或 HTML。例如，要为 `Fubar` 模块生成 HTML 文档，你需要输入 `pod2html Fubar.pm > Fubar`。

## 模块与 CPAN

Perl 社区（以及 Linux 社区）的一个巨大优势在于它是一个开源社区。这种社区支持通过 CPAN 为 Perl 实现，CPAN 是 Perl 代码存储库的镜像网络。

CPAN 的大部分由模块组成，这些模块是可重用的代码块，可以实现有用的功能，类似于包含 C 语言程序员所需函数的软件库。这些模块有助于在构建 Perl 程序时加速开发，并让 Perl 黑客在构建自行车时无需重复造轮子。

有成千上万的 Perl 模块，功能涵盖从发送电子邮件、维护你的 Cisco 路由器访问，到告诉你一个名称是男性化还是女性化，以及以某些花哨的格式打印时间。如果你能想到用 Perl 脚本做某事，很有可能已经存在一个模块可以提供帮助。如果没有现成的模块，我们鼓励你编写一个并与社区其他成员分享。

Perl 自带了一套标准模块。这些模块应该包含你最初使用 Perl 时的大部分功能。如果你需要使用通过 Fedora 安装的模块，可以使用 CPAN 模块（标准模块之一）下载并安装其他模块到你的系统中。在 http://www.perl.com/CPAN/，你会找到 CPAN 多路调度器，它会尝试引导你访问距离最近的 CPAN 站点。

输入以下命令将你进入一个交互式 shell，让你访问 CPAN。你可以在提示符输入 `help` 来获取有关如何使用 CPAN 程序的更多信息。

```bash
$ perl -MCPAN -e shell
```

从 CPAN 安装模块（或自己写了一个模块）后，你可以将模块加载到内存中并在函数中使用它：

```perl
use Time::CTime;
```

`use` 会在变量 `$INC` 列出的目录中查找模块。在这个示例中，`use` 查找名为 `Time` 的目录，其中包含一个名为 `CTime.pm` 的文件，该文件被认为包含一个名为 `Time::CTime` 的包。每个模块的发行版都应该包含关于如何使用的文档。

# 示例

本节多次提到了 Perl 文档。对于 `perldbug`、`perlun`、`permod` 和 `perldib`，只需在提示符输入 `perdoc perldoc` 即可。你可以在 http://www.cpan.org/doc/index.html 或任何 CPAN 站点在线查看所有的 Perl 文档。CPAN 是全面 Perl 存档网络。更多信息请参阅本章后后的“模块与 CPAN”部分。

Perl 文档使用 POD（纯文本文档）编写，并可以使用帮助 Perl 的 `pod2` 工具转换为任何其他格式，如 Tex、ASCII 或 HTML。例如，要为 `Fubar` 模块生成 HTML 文档，你需要输入 `pod2html Fubar.pm > Fubar`。

Perl 社区（以及 Linux 社区）的一个巨大优势在于它是一个开源社区。这种社区支持通过 CPAN 为 Perl 实现，CPAN 是 Perl 代码存储库的镜像网络。CPAN 的大部分由模块组成，这些模块是可重用的代码块，可以实现有用的功能，类似于包含 C 语言程序员所需函数的软件库。这些模块有助于在构建 Perl 程序时加速开发，并让 Perl 黑客在构建自行车时无需重复造轮子。有成千上万的 Perl 模块，功能涵盖从发送电子邮件、维护你的 Cisco 路由器访问，到告诉你一个名称是男性化还是女性化，以及以某些花哨的格式打印时间。如果你能想到用 Perl 脚本做某事，很有可能已经存在一个模块可以提供帮助。如果没有现成的模块，我们鼓励你编写一个并与社区其他成员分享。

Perl 自带了一套标准模块。这些模块应该包含你最初使用 Perl 时的大部分功能。如果你需要使用通过 Fedora 安装的模块，可以使用 CPAN 模块（标准模块之一）下载并安装其他模块到你的系统中。在 http://www.perl.com/CPAN/，你会找到 CPAN 多路调度器，它会尝试引导你访问距离最近的 CPAN 站点。输入以下命令将你进入一个交互式 shell，让你访问 CPAN。你可以在提示符输入 `help` 来获取有关如何使用 CPAN 程序的更多信息。

```bash
$ perl -MCPAN -e shell
```

从 CPAN 安装模块（或自己写了一个模块）后，你可以将模块加载到内存中并在函数中使用它：

```perl
use Time::CTime;
```

`use` 会在变量 `$INC` 列出的目录中查找模块。在这个示例中，`use` 查找名为 `Time` 的目录，其中包含一个名为 `CTime.pm` 的文件，该文件被认为包含一个名为 `Time::CTime` 的包。每个模块的发行版都应该包含关于如何使用的文档。

# 示例

本节多次提到了 Perl 文档。对于 `perldbug`、`perlun`、`permod` 和 `perldib`，只需在提示符输入 `perdoc perldoc` 即可。你可以在 http://www.cpan.org/doc/index.html 或任何 CPAN 站点在线查看所有的 Perl 文档。CPAN 是全面 Perl 存档网络。更多信息请参阅本章后后的“模块与 CPAN”部分。等等，文本重复了。

注意 `@` 符号不需要在单引号（`''`）内转义。Perl 不会在单引号内进行插值（评估变量），但在双引号和这里 strings（类似于 `<<` shell 操作）。

## 使用 Perl 安装 CPAN 模块

你可以使用 `-M` 和 `-e` 命令通过 Perl 交互地从 CPAN 下载并安装模块。使用如下方式启动过程：

```bash
# perl -MCPAN -e shell
```

按下回车后，你会看到一些介绍信息，并被要求选择自动或手动配置，这在任何下载或安装发生之前是必要的。输入 `no` 并按回车让 Perl 自动配置下载和安装过程；或者如果需要，只需按回车手动配置，回答一系列有关路径、终端设置、程序位置等的问题。设置将保存在名为 `.cpan` 的目录中。

完成后，你会看到 CPAN 提示符：

```bash
cpan>
```
