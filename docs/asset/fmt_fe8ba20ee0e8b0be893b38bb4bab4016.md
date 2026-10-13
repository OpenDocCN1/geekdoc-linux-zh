
Matched from:

kdebindings

`kdebindings-devel.i386`                    3.3.1-1                    updates-released

Matched from:

kdebindings-devel

Development files for kdebindings

Development files for the KDE bindings.

Install kdebindings-devel if you want to develop non-KDE applications that talk to KDE.

`kdebindings-debuginfo.i386`                3.3.1-1                    updates-released

Matched from:

kdebindings-debuginfo

Debug information for package kdebindings

This package provides debug information for package kdebindings.

Debug information is useful when developing applications that use this package or when debugging this package.

## 配置 Yum

如前所述，Yum 主要通过 `yum.conf` 文件的内容和 `/etc/yum.repos.d` 目录进行控制。让我们仔细查看这两者的内容，以便你更好地理解如何最佳地配置 Yum。

当你首次安装 Fedora 时，会有一个默认的 `yum.conf` 文件，为 Yum 命令提供几种开关选项。它基本上可以省去输入许多开关选项的麻烦，并保持 Yum 的简洁。默认情况下，Yum 被配置为执行以下操作：

- 在 `/var/cache/yum` 中保留头部文件缓存。
- 在处理过程中提供最小的屏幕信息。
- 在 `/var/log/yum.log` 中保留日志文件。
- 仅下载最新的软件包。
- 容忍处理过程中的错误。
- 将软件包匹配到你的处理器架构。
- 设置最大重试次数限制为 20 次。
- 检查废弃的软件包。
- 使用 GPG 密钥来确保软件包的身份。

所有这些选项都包含在 `yum.conf` 文件中，让你可以轻松修改甚至删除某些行。例如，你可能需要 Yum 最多只尝试五次，或者你需要 Yum 提供更多视觉信息。

你可以将仓库信息添加到 `yum.conf` 文件中，但从 Fedora Core 3 开始，Yum 处理仓库的方式发生了变化。Fedora 3 新增的 `yum.repos.d` 文件夹允许你为每个仓库创建独立的配置文件。默认情况下，Fedora 包含其基础软件包、更新软件包、正在测试中的更新软件包以及更不稳定的开发软件包的仓库。默认情况下，只有基础软件包和更新软件包是启用的。

> **注意**
>
> 除非你确实知道自己在做什么，否则应避免使用 fedora-updates-testing 和 fedora-development 这些更不稳定的仓库。这些仓库包含尖端（bleeding-edge）软件包，可能会破坏你的系统。请谨慎行事！

打开仓库文件可以查看关于仓库本身的一些详细信息，包括访问路径（通过 HTTP、FTP 或本地访问）、该仓库的镜像列表、该仓库是否启用，以及是否启用了 GPG 检查。

如果你想添加一个新仓库，在成功将其添加到 `/etc/yum.repos.d` 目录下的独立仓库文件或在 `yum.conf` 文件之前，你需要了解一些事项。

## 创建本地 Yum 仓库

当 Yum 处于活动状态时，它可以下载大量 RPM 头部文件和文件形式的信息，这很容易消耗带宽。

如果你在本地网络上有三台或更多基于 Fedora 的机器，创建本地 Yum 仓库可以很好地节省带宽。

在开始设置仓库之前，你需要安装 `rsync` 和 `createrepo` 软件包，因为两者你都需要。使用命令 `yum install rsync createrepo` 以确保它们已安装。

首先，创建一个目录来存放你的仓库。在我们的示例中，我们将使用 `/home/andrew/repo/` 作为目标目录。

接下来，找到你要镜像的网站（Fedora 的网站选择可以在 http://fedora.redhat.com/download/mirrors.html 找到）。在本例中，我们将使用位于肯特郡坎特伯雷的英国镜像服务 `rsync.mirror.ac.uk/fedora.redhat.com/updates/i386/`。

`rsync` 本身很容易使用，方法如下：

```
# rsync rsync::/rsync.mirror.ac.uk/fedora.redhat.com/updates/i386/*.rpm /home/andrew/repo
```

然后 `rsync` 开始下载它在该目录中找到的文件到 `/home/andrew/repo`。这可能花费一些时间（在编写本文时，上述地址大约有 5GB 的更新可用）。为了确保 `rsync` 确实在工作，请使用 Nautilus 导航到 `/home/andrew/repo`；这里你应该看到许多软件包一个接一个地出现。

完成下载所需的更新后，你需要创建你的仓库。这就是 `createrepo` 命令发挥作用的地方。

## 使用 Createrepo

`Createrepo` 是一个程序，旨在快速有效地从一组 rpm 文件中提取相关信息，以生成 Yum 成功安装或更新当前已安装软件包基础所需的元数据。

该命令很简单

```
createrepo /yourtargetdirectoryhere
```

因此，如果我们使用上一节中的示例，语法看起来类似于这样：

```
$ createrepo /home/andrew/repo
```

这将产生以下输出：

```
88/88 - alsa-lib-1.0.6-5.i386.rpm
Saving Primary metadata
Saving file lists metadata
Saving other metadata
```

这表明已编目 88 个 RPM 包，并且相关元数据已保存。该程序会自动使用给定的目录，因此你无需担心创建多个目录副本。

完成此操作后，你就可以将新软件源包含到 `/etc/yum.conf` 文件中，或者包含到 `/etc/yum.repos.d` 目录下的单独文件中。让我们来看一下一个典型的 Yum 配置文件：

```
$ cat /etc/yum.repos.d/local.repo
[local]
name=Fedora Core $releasever - $basearch - Updates
baseurl=http://192.168.2.5/repo
enabled=1
gpgcheck=0
```

这个文件相当容易阅读。第一行是传递给 Yum 的软件源名称。名称必须用方括号括起来才能被识别；在这种情况下，它仅仅是 `local`。第二行提供了 Yum 在忙碌工作时显示的显示名称；对于此软件源，它使用 `Fedora Core $releasever - $basearch - Updates`，这会打印发行版版本（在这种情况下是 4）和基础架构（i386）。接下来是基础 URL，即主要下载点。Yum 使用它来扫描并下载所需的元数据。第四行显示此软件源是否已启用：`enabled=0` 表示禁用，而 `enabled=1` 表示已启用并可以使用。最后一行决定 RPM 包是否使用 GnuPG 密钥进行检查。建议从原始软件源获取相关的 GnuPG 密钥，以确保安装的程序包未被篡改。然后可以使用以下命令将其导入到 RPM 数据库中：

```
# rpm --import thiskey.txt
```

密钥导入数据库后，Yum 可以使用它来验证程序包是否完整且安全可用。

> **注意**
>
> 请注意，我们说使用 GPG 密钥可以使程序包更安全。这当然是正确的，但要注意，有时程序包之间可能会冲突。在使用某些软件源时要谨慎，因为它们与其他软件源可能不兼容。选择软件源时，务必阅读常见问题解答（FAQ）中关于不兼容性的警告。查看 http://fedoraproject.org/wiki/Extras_2fRepositoryMixingProblems 了解 Fedora 官方对此事的立场。

## 参考

- http://www.linux.duke.edu/projects/yum/ — Yum 项目主页，托管于 Linux@Duke（杜克大学）。
- http://rpm.livna.org/ — Livna Yum 软件源。
- http://freshrpms.net/ — FreshMeat Yum 软件源。它是 OSTG 的一部分，该组织还包括 slashdot 和 linux.com。
- http://dag.wieers.com — Dag Wieers 的 Yum 软件源。
