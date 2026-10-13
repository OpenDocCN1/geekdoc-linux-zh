
$ yum

```
这将显示 yum 的使用选项，并让你确认已安装 yum。
```

确认 yum 可用后，应切换到超级用户并输入以下命令：

```
# yum check-update
```

此命令初始化 `yum`，并要求其扫描机器上已安装的 RPM，扫描存储库中的头部文件，然后开始构建头部文件缓存。在经历数分钟的繁忙活动后，`yum` 将完成本地头部文件缓存的构建，并准备好让你开始下载和安装更新及新软件。

若要快速轻松地更新系统中的所有软件，请输入以下命令：

```
# yum update
```

此命令要求 `yum` 从注册的存储库下载头部信息，将其与你当前已安装的软件包进行比对，并更新所有标记为有新版本的软件包。根据运行该命令的频率以及系统中安装的软件包数量，这可能需要一些时间。当然，如果你拥有电缆或 DSL 连接，速度会更快；但拨号用户需注意，在 `yum` 工作期间，他们可能需要离开去煮几杯咖啡。

当 `yum` 完成头部文件的下载并解决依赖关系后，系统会列出待更新或安装的软件包清单，并要求你确认。在命令提示符下输入 `y`，`yum` 便开始下载 RPM 文件。

下载完成后，`yum` 执行安装并运行测试，以确保一切正常完成。当 `yum` 确认所有项目存在且正确无误后，你将返回命令提示符，此时系统已是最新状态。

当你希望更新整个系统时，这种方法很棒。但如果你只想更新特定的软件包怎么办？同样，`yum` 可以轻松处理这种情况。你可以指定想要更新的软件包，然后使用 `yum` 通过以下命令检查其可用性：

```
# yum list <packagename>
```

此命令要求 `yum` 将软件包名称与存储库中注册的软件包进行交叉引用，并告知你哪些软件包可用。你可以使用通配符作为命令的一部分，以查找哪些关联软件包可用。例如，命令：

```
# yum list kde*
```

搜索包含 `kde` 的任何软件包，如果你想要选择性更新软件包，这将非常有用。使用以下命令更新单个软件包：

```
# yum update <packagename>
```

或使用此命令一次更新多个软件包：

```
# yum update <packagename1> <packagename2>
```

当然，当 `yum` 处理所需软件包时，它也会解决任何依赖性问题。你不仅可以看到将被更新的软件包，还能看到为解决依赖性问题所必需的软件包。

> `yum` 并非由 Red Hat 开发。相反，杜克大学（Duke University）荣获了创建并维护 `yum` 及其相关技术的荣誉。特别是，Seth Vidal 投入了大量时间和精力，确保 `yum` 在速度和功能上不断改进。订阅 https://lists.dulug.duke.edu/mailman/listinfo/yum 上的 `yum` 邮件列表，以获取有关 `yum` 的最新信息和更新。

### 非交互式运行 yum

运行 `yum` 可能涉及大量的更新和依赖解析，而下载这些内容本身可能需要很长时间，尤其是当你通过慢速连接接入互联网时。即使使用相对较好的连接（2Mbps DSL），下载几百兆字节的软件包也可能需要一段时间。幸运的是，`yum` 中有一个选项，你可以使用它来以最少的用户干预方式运行。其语法如下：

```
#yum -y update
```

这告知 `yum` 当被提问时，自动假设答案为“是”。这样，你可以离开去做其他任务，而不必等待 `yum` 下载完所有头部文件并询问你是否要继续安装软件包。

### 使用 `yum` 移除软件包

到目前为止，我们只看了使用 `yum` 安装软件，但这只是其功能的一小部分。它还可以用于移除不再需要的软件包，并提供已安装和可用软件包的详细信息。其语法与 `yum` 的安装和更新功能相似。在本节中，我们将探讨如何使用 `yum` 从系统中移除软件包。

如前所述，`yum` 通过 `rpm` 命令与本地软件包数据库进行交互查询。如果需要移除软件包，可以使用 `yum remove <package-name>`。然后 `yum` 扫描本地文件系统，找到指定的软件包，并检查潜在的依赖性问题。这样，你永远不会移除可能导致系统崩溃的软件包。系统会提示你确认是否要移除所需的软件包；然后 `yum` 处理该软件包及其依赖项，以安全地移除它们。

### 维护 `yum`

随着时间推移，`yum` 可能会积累大量的 RPM 头部文件和其他各类信息，逐渐占用硬盘上相当多的空间。该缓存保存在 `/var/cache/yum` 中，可以通过使用 `yum` 命令并选择相应选项来管理。

`yum` 处理完下载的软件包后，即使你可能不再需要使用它们，它也不会自动从系统中删除它们。在我仅运行一次 `yum update` 之后，发现我的缓存文件已膨胀至略超过 500MB 的大小。几个月后，随着新更新、错误修复和安全补丁的出现，这一规模可能会呈指数级增长。

与 Fedora 中的一切一样，你可以选择要移除的内容：软件包本身、RPM 头部文件，或两者兼有。若要仅清理系统中的软件包，应使用以下命令：

```
#yum clean packages
```

通过执行此操作，`yum` 移除了我系统上所有已下载的软件包，一次性节省了 450MB 空间。

如果你还想移除头部文件，可以使用以下命令：

```
#yum clean headers
```

这会在移除软件包所节省的 450MB 基础上，额外节省 10MB。

**注意**

如果你决定删除头文件，`yum` 在下一次你决定更新系统时将不得不重新下载它们。这可能会花费一点时间，但如果你拥有快速的宽带连接，这应该不成问题。

最后，如果你想在一个快速步骤中同时删除软件包和头文件，你应该使用以下命令：

```bash
# yum clean all
```

这会从缓存中移除所有软件包和头文件。我们建议只使用命令来清理软件包，特别是当你处于慢速互联网连接下时，因为保留头文件可以为你未来的更新会话节省时间。

## 使用 yum 管理软件包清单

`yum` 的另一个有用功能是它可以列出几组软件包。有一些选项可供列出，包括当前已安装的软件包、可安装的软件包，以及有可用更新的软件包。

命令如下：

```bash
$ yum list <available> <updates> <installed> <extras>
```

-   **available**—这列出了配置存储库中可用的软件包。
-   **updates**—这列出了当前已安装软件包的可用更新。
-   **installed**—这列出了系统当前已安装的软件包。
-   **extras**—这列出了那些不在任何配置存储库中但已安装的软件包。

因此，如果我想知道我的系统上安装了哪些软件包，我会使用命令 `yum list installed` 来获取已安装软件包及其版本号的详细摘要。你可以更进一步，查询个别软件包。你可能想找出你安装了哪个版本的 OpenOffice.org，以及哪个版本可供安装。为此，你会使用 `yum list openoffice.org`——其结果将显示已安装的版本以及可供更新的版本。

`yum` 还可以搜索每个 RPM 文件的头文件和摘要，以便你可以找到通常无法仅通过软件包名称本身获取的关于软件包的特定信息。例如，使用 `yum search kdebindings` 会显示与 `kdebindings` 匹配的条目。该命令的结果显示如下：

```bash
$ yum search kdebindings
Searching Packages: 
Setting up Repos:  dries
Setting up Repo: dag
Setting up Repo: updates-released
Setting up Repo: newrpms
Setting up Repo: freshrpms
Setting up Repo: base
Reading repository metadata in from local files
dag    717/717
dag   1808/1808
updates-re 722/722
newrpms   385/385
freshrpms 477/477
base    2622/2622
kdebindings.i386  3.3.0-3  base
Matched from:
kdebindings
kdebindings-devel.i386  3.3.0-3  base
Matched from:
kdebindings-devel
Development files for kdebindings
Development files for the KDE bindings.
Install kdebindings-devel if you want to develop non-KDE applications that talk to KDE.
kdebindings.i386  3.3.1-1  updates-released
Matched from:
kdebindings
```
