
最简单的思考方式是将 Yum 视为一个利用 `rpm` 命令的软件层。当你向 Yum 发出命令时，它会自动访问各种仓库并下载 rpm 头部信息，然后使用 `rpm` 命令进行查询。这样做的好处是，所有处理都在本地进行，无需下载整个 RPM 文件。通常，RPM 头部信息仅占文件的一小部分，这使得它易于处理且下载速度快。Yum 构建和维护一个头部文件的本地缓存，这些文件归属于提供它们的仓库，并在你使用 Yum 时查询此缓存。每次调用 Yum 时，它都会检查仓库是否有更新。如果发现更新，它会向缓存中添加新的头部信息，从而确保在你需要使用时尽可能保持最新。由于 Yum 使用 `rpm`，因此不应存在依赖性问题，这使得安装和更新软件变得快速且简便。

Yum 主要由其配置文件 `yum.conf` 和 `yum.repos.d` 目录的内容控制，两者都可以在 `/etc` 中找到。默认情况下，Yum 使用 Red Hat 和 Fedora 的仓库进行更新，但如果你想安装 Red Hat 官方未提供的其他软件，可以轻松添加自己的仓库。

与 `apt` 类似，Yum 极其易用，只需一条带开关的命令即可更新 Fedora 中的所有软件。

## 入门

首先，打开一个终端。通过简单输入以下内容来检查 Yum 是否已安装并正常工作

```bash
$ yum
```

这会显示 Yum 的使用选项，并告知你已安装该工具。

确认 Yum 可用后，你应该切换到超级用户并输入以下命令：

```bash
# yum check-update
```

此命令初始化 Yum，并要求它扫描机器上已安装的 RPM、扫描仓库中的头部文件，然后开始构建头部文件缓存。在几分钟的繁忙活动后，Yum 将完成其头部文件的本地缓存，并准备好让你开始下载和安装更新及新软件。

要对系统上的所有软件进行快速简单的更新，请输入以下命令

```bash
# yum update
```

这要求 Yum 从注册的仓库下载头部信息，将其与你当前已安装的软件包进行比对，并更新标记有新版本的软件包。根据你运行此命令的频率以及系统中安装的软件包数量，这可能需要一些时间。当然，如果你拥有有线或 DSL 连接，速度会更快，但拨号用户请注意，在 Yum 工作时，你可能需要去泡几杯咖啡。

当 Yum 完成下载头部信息并解决依赖性问题后，你会看到一个待更新或安装的软件包列表，并被要求确认。在命令提示符处输入 `y`，Yum 将开始下载 RPM 文件。

下载完成后，Yum 将执行安装并运行测试，以确保所有操作正确完成。当 Yum 确认所有事物均存在且正确后，你将返回到命令提示符，拥有一个刚刚更新过的系统。

当你想要更新整个系统时，这很棒，但如果你想只更新特定的软件包怎么办？同样，Yum 可以轻松为你处理此事。你可以识别出想要更新的软件包，然后使用 Yum 检查其可用性，使用下面所示的命令：

```bash
# yum list <packagename>
```

此命令要求 Yum 将软件包名称与仓库中注册的软件包进行交叉引用，并告知你有哪些可用。你可以使用通配符作为命令的一部分，以查找哪些关联软件包可用。例如，命令

```bash
# yum list kde*
```

将搜索任何包含 `kde` 的软件包，这在你想选择性地更新软件包时非常有用。使用下面所示的命令更新单个软件包：

```bash
# yum update <packagename>
```

或者使用此命令一次更新多个软件包：

```bash
# yum update <packagename1> <packagename2>
```

当然，当 Yum 处理所需软件包时，它也会解决任何依赖性问题。你不仅有机会看到将被更新的软件包，还能看到哪些软件包是满足依赖性问题所必需的。

## 关于 Yum

Yum 并非由 Red Hat 本身开发。相反，杜克大学（Duke University）有幸成为 Yum 及其相关技术的创建者和维护者。特别是，Seth Vidal 投入了大量时间和精力，确保 Yum 在速度和功能上不断改善。订阅 Yum 邮件列表 https://lists.dulug.duke.edu/mailman/listinfo/yum 以获取关于 Yum 的最新信息和更新。

## 使用 Yum 移除软件包

到目前为止，我们只查看了使用 Yum 安装软件，但这仅仅是其功能的一小部分。

它还可以用于移除不再需要的软件包，并提供有关已安装和可用软件包的详细信息。

其语法类似于 Yum 的安装和更新功能。在本节中，我们将查看如何使用 Yum 从系统中移除软件包。

如前所述，Yum 与 `rpm` 命令接口交互，以查询本地软件包数据库。如果你需要移除一个软件包，可以使用 `yum remove <packagename>`。然后 Yum 将扫描本地文件系统，找到指定的软件包，并检查潜在的依赖性问题。这样，你永远不会移除一个可能

会导致系统崩溃。系统将提示你确认是否要移除所需的软件包；随后 Yum 会处理这些软件包及其依赖项，以安全地移除它们。

## 使用 Yum 管理软件包清单

Yum 的另一个实用功能是能够列出多组软件包。你可以查看几种不同的选项列表，包括当前已安装的软件包、可供安装的软件包，以及有可用更新的软件包。

命令如下：

```
$ yum list <available> <updates> <installed> <extras>
```

- `available`—列出配置仓库中可用的软件包。
- `updates`—列出当前已安装软件包的可用更新。
- `installed`—列出系统上当前已安装的软件包。
- `extras`—列出已安装但未在任何配置仓库中出现的软件包。

因此，如果我想找出系统中安装了哪些软件包，我会使用 `yum list installed` 命令，以获取已安装软件包及其版本号的详细摘要。你还可以更进一步，查询单个软件包。例如，你可能想知道安装了哪个版本的 OpenOffice.org，以及哪个版本可供安装。为此，你可以使用 `yum list openoffice.org`——结果将显示已安装的版本以及可供更新的版本。

Yum 还可以搜索每个 RPM 文件的头部和摘要信息，以便你可以找到关于软件包的特定信息，而这些信息通常无法仅从软件包名称中获取。

例如，使用 `yum search kdebindings` 会列出与 `kdebindings` 匹配的条目。此命令的结果如下所示：

```
$ yum search kdebindings
Searching Packages:
Setting up Repo: dries
Setting up Repo: dag
Setting up Repo: updates-released
Setting up Repo: newrpms
Setting up Repo: freshrpms
Setting up Repo: base
Reading repository metadata in from local files
```

```
dries          : ######################################################## 717/717
dag            : ######################################################## 1808/1808
updates-re:    : ######################################################## 722/722
newrpms        : ######################################################## 385/385
fresbrpm       : ######################################################## 477/477
base           : ######################################################## 2622/2622
```

kdebindings.i386                          3.3.0-3                       base

Matched from:

kdebindings

kdebindings-devel.i386                    3.3.0-3                       base

Matched from:

kdebindings-devel

Development files for kdebindings

Development files for the KDE bindings.

Install kdebindings-devel if you want to develop non-KDE applications that talk to KDE.

kdebindings.i386                          3.3.1-1                    updates-released
