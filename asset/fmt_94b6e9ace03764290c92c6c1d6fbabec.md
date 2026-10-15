
kdebindings-devel.i386  3.3.1-1  updates-released

Matched from:

kdebindings-devel

Development files for kdebindings

Development files for the KDE bindings.

Install kdebindings-devel if you want to develop non-KDE applications that talk to KDE.

kdebindings-debuginfo.i386  3.3.1-1  updates-released

Matched from:

kdebindings-debuginfo

Debug information for package kdebindings

This package provides debug information for package kdebindings. Debug information is useful when developing applications that use this package or when debugging this package.

### 配置 yum

如前所述，`yum` 主要通过 `yum.conf` 文件的内容和 `/etc/yum.repos.d` 目录来控制。让我们仔细看看这两者的内容，以便更好地理解如何最佳地配置 `yum`。

当你最初安装 Fedora 时，有一个默认的 `yum.conf` 文件，为 `yum` 命令提供了几个开关。它基本上让你免于输入许多开关，并保持 `yum` 的简洁性。默认情况下，`yum` 被配置为执行以下操作：

- 在 `/var/cache/yum` 中保留头文件缓存
- 在处理期间提供最少限度的屏幕信息
- 在 `/var/log/yum.log` 中保留日志文件
- 仅下载最新的软件包
- 对过程中的错误具有容错性
- 将软件包匹配到你的处理器架构
- 最大重试次数限制为 20 次
- 检查过时的软件包
- 使用 GPG 密钥确保软件包的身份

所有这些选项都包含在 `yum.conf` 文件中，让你可以轻松地修改甚至删除某些行。例如，你可能需要 `yum` 最多只尝试五次，或者你可能需要 `yum` 给你提供更多视觉信息。

你可以将存储库信息添加到 `yum.conf` 文件中，但从 Fedora Core 3 开始，`yum` 处理存储库的方式发生了变化。Fedora 3 新增了一个 `yum.repos.d` 文件夹，允许你为每个存储库创建单独的配置默认情况下，Fedora 带有其基础软件包、更新软件包、测试中的更新软件包以及更不稳定的开发软件包的存储库。默认情况下，只有基础软件包和更新软件包处于启用状态。

> **警告**
> 除非你确实知道自己在做什么，否则你应该避免使用 fedora-updates-testing 和 fedora-development 这些更不稳定的存储库。这些存储库包含最前沿的软件包，可能会导致你的系统崩溃。已向你发出警告！

打开一个存储库文件会显示关于该存储库本身的一些详细信息，包括通往该存储库的路径（通过 HTTP、FTP 或本地访问）、该存储库的镜像列表、该存储库是否已启用，以及是否启用了 GPG 检查。

如果你想添加一个新的存储库，你需要先弄清楚一些事项，才能成功地将其添加到 `/etc/yum.repos.d` 下的独立存储库文件或 `yum.conf` 文件中。

你还可以配置 `yum` 忽略或排除对某些软件包的更新。因此，例如，如果你有一个仅与特定内核版本配合工作的显卡驱动程序，并且你不想在每次发布新内核时都不得修复它，你可以选择让 `yum` 排除任何内核更新。在 `yum.conf` 文件中，你需要在顶部部分添加一行类似于以下内容：

```
exclude=kernel*
```

这告诉 `yum` 忽略任何以 `kernel` 开头的软件包，并希望这能限制你在新内核版本安装后需要做的修复工作量。

### 创建本地 yum 存储库

当 `yum` 处于活动状态时，它可以下载大量以 RPM 头文件和文件形式的信息，这很容易消耗大量带宽。如果你在本地网络上有三台或更多基于 Fedora 的机器，创建本地 `yum` 存储库可以很好地节省带宽。

在我们开始设置存储库之前，你需要安装 `rsync` 和 `createrepo` 软件包，因为你需要这两个软件包。使用命令 `yum install rsync createrepo` 确保它们已安装。

首先，创建一个目录来容纳你的存储库。在我们的示例中，我们将使用 `/home/andrew/repo` 作为目标目录。接下来，找到你想要镜像的网站（可以在 `http://fedora.redhat.com/download/mirrors.html` 找到 Fedora 的网站列表）。在本例中，我们将使用位于肯特郡坎特伯雷的英国镜像服务，地址为 `rsync.mirror.ac.uk/fedora.redhat.com/updates/S/1386/`。

`rsync` 本身很容易使用，如下所示：

```bash
# rsync rsync://rsync.mirror.ac.uk/fedora.redhat.com/updates/S/1386/*\.rpm /home/andrew/repo
```

然后，`rsync` 开始下载它在该目录中找到的文件到 `/home/andrew/repo`。这可能需要一些时间（在撰写本文时，上述地址有约 5GB 的更新可用）。为了确保 `rsync` 真的在工作，使用 Nautilus 导航到 `/home/andrew/repo`；在那里，你应该看到许多软件包依次出现。

完成下载你需要的更新后，你需要创建你的存储库。这就是 `createrepo` 命令发挥作用的地方。

## 使用 createrepo

`createrepo` 是一个程序，旨在快速且高效地从一组 rpm 文件中提取相关信息，以生成 `yum` 安装或更新当前已安装软件包基础所需的元数据。

该命令非常简单：

```
createrepo /yourtargetdirectoryhere
```

因此，如果我们使用前一节中的示例，语法看起来大致如下：

```
$ createrepo /home/andrew/repo
```

这将给出以下输出：

```
88/88 - alsa-lib-1.0.6-5.i386.rpm

Saving Primary metadata

Saving file lists metadata

Saving other metadata
```

这表明有 88 个 RPM 被编目，且相关的元数据已保存。该程序自动使用给定的目录，因此您不必担心制作目录的多个副本。

完成后，您即可将新软件源包含在 `/etc/yum.conf` 文件中，或者包含在 `/etc/yum.repos.d` 下的其专用文件中。让我们来看看一个用于 `yum` 的典型配置文件：

```
$ cat /etc/yum.repos.d/local.repo

[local]

name=Fedora Core $releasever - $basearch - Updates

baseurl=http://192.168.2.5/repo

enabled=1

gpgcheck=0
```

这个文件读起来相当简单。第一行是传递给 `yum` 的软件源名称。名称必须用方括号括起来才能被识别；在此情况下，它仅为 local。第二行给出 `yum` 在工作时显示的名称；对于此软件源，它使用 `Fedora Core $releasever - $basearch - Updates`，这会打印发行版版本（在此情况下为 4）和基础架构（i386）。接下来是基础 URL，或主要下载点。这被 `yum` 用来扫描和下载它所需的元数据。第四行显示该软件源是否启用：`enabled=0` 表示已禁用，而 `enabled=1` 表示已启用并可供使用。最后一行决定是否使用 GnuPG 密钥检查 RPM。建议从原始软件源获取相关的 GnuPG 密钥，以确保您要安装的软件包未被篡改。然后，可以使用以下命令将其导入 RPM 数据库：

```
# rpm --import thiskey.txt
```
