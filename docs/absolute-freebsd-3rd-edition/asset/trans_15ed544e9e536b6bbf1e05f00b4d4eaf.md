

FreeBSD 自带一个非常简单的包管理器，位于 `/usr/sbin/pkg`，即 `pkg(7)`。它的功能仅足以定位 FreeBSD 当前的包管理器。它会安装那个新的包管理器，并将所有包管理的责任移交给它。这使得 FreeBSD 能够随着包的更新灵活地更新包管理器本身。

当你第一次尝试安装包时，`pkg(8)` 会提示你安装包管理器。我在新服务器上发现需要 `dmidecode` 包，以便在电源损坏时向制造商申请退货授权（RMA）。（不用担心我是如何*找到* `dmidecode` 包的——暂时请跟着我的思路走。）

```
# pkg install dmidecode
```

FreeBSD 运行 `pkg(8)` 后发现系统中尚未安装包管理工具。

```
The package management tool is not yet installed on your system.
Do you want to fetch and install it now? [y/N]: y
```

默认答案以大写字母显示。如果我按 **n** 和 **ENTER**，`pkg` 将终止运行。如果我按 **y** 和 **ENTER**，FreeBSD 将启动系统的引导过程。

```
① Bootstrapping pkg from pkg+http://pkg.FreeBSD.org/FreeBSD:12:amd64:quarterly,
  please wait...
② Verifying signature with trusted certificate pkg.freebsd.org.2013102301...
  done
③ Installing pkg-1.10.0_2...
  Extracting pkg-1.10.0_2: 100%
④ Updating FreeBSD repository catalogue...
  meta.txz                              : 100%   944 B   0.9kB/s   00:01
  packagesite.txz                       : 100%   6 MiB   2.0MB/s   00:03
  Processing entries: 100%
FreeBSD repository update completed. 26059 packages processed.
All repositories are up to date.
Updating database digests format: 100%
```

安装过程首先从 FreeBSD 镜像站点下载当前的 `pkg` 工具 ①。然后检查下载文件的数字签名 ②。接着解压并安装这些工具 ③。随后，`pkg` 下载并安装可用包的目录 ④。

包管理系统现已安装完成。为了使流程更顺畅，FreeBSD 自带的 `pkg(8)` 存根（stub）会指示新安装的包管理系统安装你真正想要的程序。在这种情况下，新的 `pkg(8)` 会为你安装 `dmidecode`。

你可以运行 `pkg bootstrap` 单独安装包管理系统，而不添加其他包——但说实话，几乎没人会在命令行上这么单独执行。如果包管理系统已经安装，运行 `pkg bootstrap` 不会做任何事情，因此它对于设置脚本很有用。

# 常见的 pkg 选项

虽然每个 `pkg` 子命令都有独特的功能，但有少数几个命令选项在几乎所有子命令中通用。

在默认配置下，`pkg` 在执行任何操作前都会提示你确认。使用 `-y` 标志可以告诉 `pkg` 直接执行操作而不提示。

相反，有时你希望 `pkg` 展示运行某命令时的模拟行为，而不实际执行任何操作。使用 `-n` 标志可以进行干运行（dry run）。例如，使用 `-n` 安装包时会列出将要安装的每个包的名称（包括依赖项）。然而，系统实际上不会安装这些包，因此没有风险。干运行有助于你在维护窗口期间准备变更。

许多 `pkg` 操作会产生大量输出。使用 `-q` 可以减少输出量。

`-a` 标志通常将命令应用于所有已安装的包。

最后，`pkg` 通常会拒绝执行无意义或损害系统的操作。`-f` 标志强制 `pkg` 执行你所说的操作。强制包操作通常但不是总是个坏主意。例如，你可能需要 `-f` 来强制重新安装损坏的包。

# 配置 pkg(8)

`pkg(8)` 程序被设计得非常灵活。虽然每个子命令都有许多选项，但你可以通过配置文件 `/usr/local/etc/pkg.conf` 为大多数程序建立定制化且一致的行为。

*pkg.conf* 文件包含 `pkg(8)` 带有注释的默认设置。它是查看系统在未经任何修改时如何表现的绝佳参考。配置使用 UCL 编写（参见第 2 章）。变量可以设置为整数；字符串，如文件路径；或布尔值，如 *YES* 或 *NO*。YES、*ON* 和 *TRUE* 是同义词，*NO*、*OFF* 和 *FALSE* 也是同义词。它们均不区分大小写。

```
#PKG_DBDIR = "/var/db/pkg";
#PKG_CACHEDIR = "/var/cache/pkg";
#PORTSDIR = "/usr/ports";
#INDEXDIR = "";
--- snip---
```

FreeBSD 在 *pkg.conf* 为空的情况下也能完美运行。默认配置包含许多被注释掉的条目和相当多的别名。你可以在后续操作中考虑以下示例设置。

大多数 `pkg` 操作提供是/否对话框，默认值以大写字母显示。出于保守原则，`pkg` 通常默认为 NO。使用 *DEFAULT_ALWAYS_YES* 选项可将该默认值更改为 YES。

你可以通过添加 `-y` 标志让 `pkg` 命令假设你对所有问题都回答“是”。如果你厌倦了键入 `-y`，可以将 *ASSUME_ALWAYS_YES* 标志设置为 YES，让 `pkg` 假设你始终回答“是”。

因为我懒散但不鲁莽，我更喜欢以下 *pkg.conf* 设置：

```
DEFAULT_ALWAYS_YES = true;
ASSUME_ALWAYS_YES = false;
```

如果安装包的过程出现异常，你可能需要调试输出。设置 *DEBUG_LEVEL* 可开启调试输出。该变量接受从 0（无调试）到 4（完全调试）的整数。

许多包在安装过程中包含脚本。将 *DEBUG_SCRIPTS* 设置为 YES 可为每个脚本开启调试。

任何 *pkg.conf* 设置也可用作环境变量。环境变量会覆盖配置文件中的任何设置。你可以这样安装带调试输出的包：

```
# env DEBUG_LEVEL=4 pkg upgrade
```

所有选项都在 `pkg.conf(5)` 中有文档记载。但并非所有选项都有注释掉的条目。如果某个选项没有示例但你想要使用它，请自行添加。我们将在后续章节中考察其中许多选项。

# 查找包

现在你已安装包管理器，就可以安装包了。熟悉多种类 Unix 操作系统的系统管理员知道，不同的操作系统对同一软件的不同包版本赋予不同的名称。FreeBSD 上 Apache Web 服务器的包与 illumos 上甚至其他 Linux 发行版中的 Apache 包名称完全不同。在安装任何东西之前，你需要弄清楚它的名称。

假设客户想在 Apache 上运行 WordPress。你的工作不是质疑客户对 Web 服务器的选择；你的工作是构建并支持该 Web 服务器。首先，使用 `pkg search` 命令查找 Apache。你需要提供一个字符串，让 `pkg` 执行不区分大小写的搜索。

```
# pkg search apache
apache-ant-1.9.7      Java- and XML-based build tool
apache-forrest-0.9    Tool for rapid development of small sites
apache-mode.el-2.0   Emacs major mode for editing Apache configuration files
--snip--
```

我故意选了一个令人烦恼的例子；FreeBSD 有 50 多个与 Apache Web 服务器相关的包。幸运的是，每个搜索结果都列有一行包描述。浏览结果直到找到实际的 Web 服务器非常简单。

```
--snip--
apache22-2.2.31_1                   Version 2.2.x of Apache web server with prefork MPM
apache22-event-mpm-2.2.31_1         Version 2.2.x of Apache web server with event MPM
apache22-ith-mpm-2.2.31_1           Version 2.2.x of Apache web server with ith MPM
apache22-peruser-mpm-2.2.31_1       Version 2.2.x of Apache web server with peruser MPM
apache22-worker-mpm-2.2.31_1        Version 2.2.x of Apache web server with worker MPM
```

有六个不同版本的 Apache。首先，看看包名称。当软件有多个版本时，主要版本号会整合到包名称中。Apache 2.2 与 Apache 2.4 大不相同，因此包命名为 *apache22* 和 *apache24*。实际版本号紧随其后。我们的第一个 Apache 2.2 包实际上是针对 Apache 2.2.31 的。结尾的 *\_1* 是包版本号，意味着这是一个更新后的包。包含的软件没有改变，但包本身已发生某种变化。包版本号因两种原因递增。当源端口发生对包有实质影响的更改时，版本号会增加。当必需共享库的 ABI 变更要求重新编译包时，也值得增加版本号。

Apache 2.2 以五个不同的包形式存在。熟悉 Apache 的人可能记得这个版本的 Apache 可以使用不同的多处理模块（MPM），但 MPM 必须在编译时选择。我已开心地忘记了我曾经知道的所有关于 MPM 的知识，因此我不愿去纠结这些细节，而是选择安装 Apache 2.4 包，*apache24*。

## 包搜索选项

某些搜索可能会生成数百条结果。尝试搜索 Perl，你会得到大约 150 个包。Perl 模块都以字符串 *p5-* 开头；FreeBSD 为 5,200 多个 Perl 模块提供了包！使用命令行选项来筛选或调整搜索结果。虽然 *pkg-search(8)* 列出了许多选项，但以下是其中一些最常用的。

- 使用 `-c` 进行区分大小写的搜索。
- 如果你确切知道想要哪个包，并且只想查看它是否在你的系统上可用，使用 `-e` 标志进行精确匹配搜索。不过，你的搜索词必须包含包版本号。

