
这告诉 `yum` 当被问到问题时，自动假设答案为“是”（yes）。这样你就可以离开去处理其他任务，而无需等待 `yum` 完成所有头文件的下载，并询问你是否要继续安装这些软件包。

# 使用 yum 移除软件包

到目前为止我们只查看了如何使用 `yum` 安装软件，但这只是其功能的一小部分。它还可以用于移除不再需要的软件包，并提供有关已安装和可用软件包的详细信息。其语法与 `yum` 的安装和更新函数相似。在本节中，我们将介绍如何从系统 `yum` 中移除软件包。

如之前提到的，`yum` 与 `rpm` 命令接口，用于查询本地软件包数据库。如果你需要移除一个软件包，可以使用 `yum remove <package>`，然后它会扫描本地文件系统，找到命名的包，并检查潜在的依赖关系问题。通过这种方式，你永远不会移除可能导致系统崩溃的软件包。系统会提示你确认想要移除所需的软件包；然后 `yum` 就会处理这些软件包及其依赖项以安全地删除它们。

# 维护 yum

随着时间的推移，你可能会建立一个巨大的 RPM 头缓存和其他杂杂信息，这些可能会逐渐积累并占用硬盘上的大量空间。该缓存保留在 `/var/cache/yum` 中，并可以使用带有你选择的的 `yum` 命令进行管理。

当 `yum` 完成软件包的下载后，它并不会自动从系统中删除它们，即使你可能不再需要它们。在仅调用一次 `yum update` 后，我发现我的缓存文件已经膨胀到 500MB 以上。几个月后，随着新更新、错误修复和安全补丁的出现，这可能会呈指数级增长。

与 Fedora 中的所有事物一样，你可以选择想要移除的内容：软件包本身、RPM 头文件或两者兼有。要仅清理系统中的软件包，你应该使用命令

```bash
#yum clean packages
```

通过这种操作，`yum` 会移除我系统中所有下载的软件包，一次性为我节省了450MB。

如果你也想移除头文件，可以使用命令

```bash
#yum clean headers
```

这在移除软件包节省的 450MB 基础上，又额外节省了 10MB。

# 使用 yum 管理软件包清单

注意

如果你决定移除头文件，`yum` 在你下次决定更新系统时将重新下载它们。这可能会花费一些时间，但如果你有快速的宽带连接，这应该不是问题。

最后，如果你想一步到位同时移除软件包和头文件，你应该使用命令

```bash
#yum clean all
```

这会从缓存中移除所有软件包和头文件。我们建议仅使用该命令清理软件包，特别是当你使用慢速网络连接时，因为保留头文件将在未来的更新过程中为你节省时间。

# 使用 yum 管理软件包清单

`yum` 的另一个有用功能是它可以列出几组软件包。你有几个选项可以列出软件包，包括当前安装的软件包、可供安装的软件包以及有可用更新的软件包。

命令如下：

```bash
$ yum list <available> <installed> <extras>
```

- `available`—列出配置存储库中的可用软件包。
- `updates`—列出当前已安装软件包的可用更新。
- `installed`—列出系统中当前安装的软件包。
- `extras`—列出不存在于任何已配置存储库的软件包。

所以，如果我想知道系统中安装了哪些软件包，我将使用 `yum list` 命令来返回已安装软件包及其版本号的详细摘要。你可以更进一步查询单个软件包。你可能想弄清楚你安装了哪个版本的 OpenOffice.org，以及哪个版本可供安装。为此，你将运行 `yum list openoffice`，结果将显示你安装了哪个版本以及哪个版本可供更新。

`yum` 还可以搜索每个 RPM 文件的头和摘要，以便你可以找到软件包的特定信息，这些信息通常无法通过包名本身获取。例如，使用 `yum search kbindings` 将带来匹配 `kbindings` 的条目。该命令的结果所示：

```bash
$ yum search kbindings
```

搜索软件包：

```
Setting up Repo: dries
Setting up Repo: dag
Setting up Repo: updates-released
Setting up Repo: newrpms
Setting up Repo: freshrpms
Setting up Repo: base
Reading repository metadata in from local files
```
dries : ############################################# 717/717
dag : ############################################ 1808/1808
updates-re: ########################################### 722/722
newrpms : ########################################### 385/385
freshrpms : ########################################### 477/477
base : ############################################ 2622/2622
```

kdebindings.i386 3.3.0-3 base

Matched from:

kdebindings

kdebindings-devel.i386 3.3.0-3 base

Matched from:

kdebindings-devel

Development files for kdebindings

Development files for the KDE bindings.

如果你想开发与 KDE 通话的非 KDE 应用程序，请安装 kdebindings-devel。

kdebindings.i386 3.3.1-1 updates-released

Matched from:

kdebindings

kdebindings-devel.i386 3.3.1-1 updates-released

Matched from:

kdebindings-devel

Development files for kdebindings

Development files for the KDE bindings.

如果你想开发与 KDE 通话的非 KDE 应用程序，请安装 kdebindings-devel。

kdebindings-debuginfo.i386 3.3.1-1 updates-released

Matched from:

# 配置 yum

kdebindings-debuginfo

kdebindings 的调试信息

此包提供了 kdebindings 的调试信息。

调试信息在开发应用程序时有用。

如之前提到的，`yum` 主要由 `yum.conf` 文件的内容和 `/etc/yum` 目录控制。让我们仔细查看这两个目录，以便你更好地了解如何配置 `yum`。

当你最初安装 Fedora 时，有一个默认的 `yum.conf` 文件为 `yum` 命令提供了多个开关。它基本上避免了你输入开关并保持了 `yum` 的简单。默认情况下，`yum` 配置为：

- 在 `/var/cache/yum` 保留缓存
- 处理期间提供少量屏幕信息
- 在 `/var/log/yum.log` 保留日志
- 只下载最新的软件包
- 对过程中的错误具有容忍度
- 匹配你的处理器架构
- 最大重试限制为 20 次
- 检查垃圾软件包
- 使用 GPG 密钥确保软件包身份

所有这些选项都包含在 `yum.conf` 文件中，让你轻松地修改甚至删除某些行。例如，你可能需要 `yum` 最多尝试五次，或者你可能需要 `yum` 提供更多视觉信息。

你可以将存储库信息添加到 `yum.conf` 文件中，但从 Fedora 3 开始，`yum` 处理存储库的方式发生了变化。新的 `yum.repos d` 允许你为每个存储库创建单独的文件。默认情况下，Fedora 带有基础软件包、更新软件包、测试中的更新软件包以及更不稳定的开发软件包的存储库。只有基础和更新存储库是默认启用的。

警告

除非你真的清楚自己在做什么，否则你应该避免使用 `fedora-updates: testing` 和 `fedora-development` 不稳定存储库。这些存储库包含了可能导致系统崩溃的前沿软件包。已经警告过你了！

# 第 38 章 高级 yum

打开仓库文件（repository file）可以向你展示关于该仓库本身的一些细节，包括它的路径（通过 HTTP、FTP 或本地访问）、仓库的任何镜像列表、该仓库是否已启用，以及是否启用了 GPG 检查。

如果你想添加一个新仓库，在成功地将其添加到 `/etc/yum.repos.d` 下的自己的仓库文件或 `yum.conf` 文件中之前，你首先需要了解几点内容。
