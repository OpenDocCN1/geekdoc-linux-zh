

# 练习 2.1 (继续)

- 5. 输入 **rpm -q zsh** 来验证该包是否已安装。系统应该返回消息 `package zsh is not installed`。

- 6. 输入 **rpm -qpi zsh-4.3.17-1.fc17.x86_64.rpm**。（如果该文件不在当前目录，则需要提供文件的完整路径）。系统应该响应并显示包的信息，例如版本号、供应商、构建该包的机器主机以及包描述。

- 7. 输入 **rpm -ivh zsh-4.3.17-1.fc17.x86_64.rpm**。系统将安装该包并显示一系列哈希值 (#)。

- 8. 输入 **rpm -q zsh**。系统应该返回完整的包名。

- 9. 输入 **zsh**。这将启动一个 shell，其功能与常见的 bash 和 tcsh shell 很多相似。你可能会发现命令行提示符发生了变化，但你可以执行大多数在 zsh 或 tcsh 中使用的命令。

- 10. 输入 **rpm -V zsh**。系统不应产生任何输出——只显示一个新的命令行提示符。验证 (-v 或 --verify) 命令会将包文件与数据库中存储的数据进行对比。在安装后，包不应显示任何偏差。（少数包在安装过程中会进行修改，但 zsh 不是其中之一）

- 11. 输入 **rpm -e zsh**。系统不应产生任何输出——只显示一个新的命令行提示符。此命令从系统中删除该包。注意，你正在运行 zsh 程序时删除了 zsh 包。Linux 会继续运行你正在使用的 zsh 程序，但你将无法启动该程序的新实例。某些程序可能会因为此而运行异常；在你删除包后，文件将会缺失。

- 12. 输入 **exit** 返回你的普通 shell。

- 13. 输入 **rpm -q zsh**。系统应该返回 `package zsh is not installed` 错误，因为你刚刚卸载了该包。

- 14. 输入 **yum install zsh**。系统将检查你的仓库，下载 zsh 并安装它。在开始下载之前它会询问你确认。

- 15. 输入 **rpm -q zsh**。结果应该与步骤 8 类似，尽管版本可能有所不同。

- 16. 输入 **rpm -e zsh**。此步骤从系统删移除 zsh，但像步骤 11 一样不产生输出。

最后三个步骤只有在你的发行版使用 Yum 时才会生效。如果你使用的是使用其他工具的发行版，你可能找到并使用其对应工具，例如 SUSE 的 zypper。

# RPM 和 Yum 配置文件

通常情况下，你不需要显式配置 RPM 或 Yum；使用 RPM 的发行版默认会以合理的方式对其进行配置。有时，你可能需要调整一些细节，特别是当你经常构建 RPM 包并想要优化你的计算机时。你可能还想为需要的特殊软件添加 Yum 仓库。要这样做，你通常需要编辑 RPM 或 Yum 配置文件。

RPM 主配置文件是 `/usr/lib/rpm/rpmrc`。该文件设置了多种选项，与编译源码包时使用的 CPU 优化几乎相同。你不应该编辑这个文件；相反，你应该创建并编辑 `/etc/rpmrc`(进行全局更改）或 `~/.rpmrc`(针对单个用户进行更改）。创建此类文件的主要目的是实现架构优化——例如，在将源码 RPM 构建为二进制 RPM 时，通过传递适当的编译器选项为你的 CPU 模型优化代码。这是通过 `optflags` 行实现的：

```
optflags: athlon -O2 -march=i386
```

该行告诉 RPM 在为 Athlon 平台构建时向编译器传递 `-O2 -march=i386` 选项。尽管 RPM 可以确定你的系统架构，但仅凭 `optflags` 行本身不太可能设置正确的标志。大多数 rpm 文件包含一系列 `buildarchtranslate` 行，允许 `rpmbuild`（或旧版本的 RPM）为整类 CPU 家族使用一组优化方案。对于 x86 系统，这些行的转换看起来如下所示：

```
buildarchtranslate: athlon: i386
buildarchtranslate: i686: i386
buildarchtranslate: i586: i386
buildarchtranslate: i486: i386
buildarchtranslate: i386: i386
```

这些行告诉 RPM 将 athlon、i686、i586、i486 和 i386 CPU 代码转换为使用 i386 优化。这实际上抵消了针对你架构的任何特定 CPU 优化的目的，但它保证了你构建的 RPM 具有最大的移植性。要更改这一点，你必须修改对应 `uname -p` 返回的 CPU 类型的行。例如，在基于 Athlon 的系统上，你可能会输入以下行：

```
buildarchtranslate: athlon: athlon
```

因此，当你重新构建源码 RPM 时，结果可能会带来性能提升，尽管它可能会降低移植性。事实上，如果你想跳过默认检测，可以使用 `optflags` 行。大多数 rpm 文件包含一系列 `buildarchtranslate` 行，允许 `rpmbuild`（或旧版本的 RPM）为整类 CPU 家族使用一组优化方案。对于 x86 系统，这些行的转换看起来如下：

```
buildarchtranslate: athlon: i386
buildarchtranslate: i686: i386
buildarchtranslate: i586: i386
buildarchtranslate: i486: i386
buildarchtranslate: i386: i386
```

（此处省略重复内容）

# Debian 发行版与惯

正如名称所示，Debian 包源于 Debian 发行版。自那时，该格式已被其他发行版采用，包括 Ubuntu、Linux Mint 和 Xandros。这些发行版衍生自原始 Debian，这意味着来自原始 Debian 的包可能在其他基于 Debian 的系统中良好运行。尽管 Debian 不强调 GUI 配置工具，但它的衍生品倾向于以 GUI 为中心，这使得这些发行版对 Linux 新手更有吸引力。原始 Debian 的独特之处在于它不是由利润驱动的公司维护的，而是由想要构建自己想要使用的产品的志愿者维护的。

