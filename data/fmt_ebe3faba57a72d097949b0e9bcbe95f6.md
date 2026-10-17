
一键安装和轻松添加第三方存储库是 Linux 可用性的一大进步，对 openSUSE 团队的创新表示祝贺。然而，有一个警告：相同或相似软件包的不同版本可能来自多个不同的存储库。如果你倾向于盲目地添加所有额外的存储库，你可能会发现两种效果。首先，当你以后想安装包时，YaST 或其他包管理工具读取和刷新所有存储库信息将花费相当的时间。其次，更重要的是，如果系统可以从不同的位置获取相同软件包的不同版本，而这些版本用于你所需的特定用途，可能会出现依赖问题。最好的做法是在需要时再添加存储库。

![](img/e749d3c47634a5bbb94e11699efbe992_374_0.png)

一键安装法是在 openSUSE 10.3 中引入的。如果你有一个系统并想通过此查看它是什么版本，请查看 `/etc/release` 文件。

```
roger@bible ~ cat /etc/SUSE-release

openSUSE 10.3 (15886)

VERSION = 10.3
```

# 命令行安装工具

如前所述，输入 `apt -i <package>` 将自动安装包及其依赖项，但它是通过调用 YaST 实现的，YaST 启动、工作并结束。包管理和依赖存储库的真实命令行界面对于 Debian 和 Ubuntu 发行版的用户来说是熟悉的，形式为 Debian 的 `apt-get` 命令，该命令基于 Debian 的 `dpkg` 包管理系统和存储库基础设施。

在过去，其他发行版的用户对 Debian 命令行包管理的便利性感到有些羡慕。随着时间的推移，其他发行版也开发了类似的工具。对于 SUSE 来说，在 SUSE 创建并集成此类工具到发行版之前，一种名为 `apt4rpm` 的非官方 RPM 版 `apt-get` 曾流行一段时间

随着 SLES 和 SLED 10 的发布，Novel 将 `zmd`（zenworks 管理守护进程）集成到产品中。这也包含在 openSUSE 10.1 中。`zmd` 进程是一个在后台运行、等待命令并检查更新源状态的守护进程。`zmd` 设计用于与服务器端的 Novel 专用 Zenworks 管理工具配合，并为注册客户提供通过 SLES/SLED 客户中心使用的更新服务。

`zmd` 的命令行界面是 `rug`，在运行 `zmd` 的 SLES 和 SLED 系统上，`rug` 是可以用于包管理的命令行工具。

在 SLES/SLED 10 和 10.1 中引入的还有 `libzypp`，这是一个用于管理包、模式和产品的库。

当 `zmd` / `libzypp` / `rug` 设置首次引入时，发现了一些问题。后来决定这对于 openSUSE 来说是一个过于沉重的管理框架，因此 `rug` 被移出了 openSUSE。`rug` 的命令行替代品是 `zypper`，它是 `libzypp` 的接口，用于解决依赖关系，解析依赖关系，而 `zypper` 在需要时调用 `rpm` 来安装包。

# 第三部分 在 SUSE Linux 中使用命令行

`zypper` 和 `rug` 具有相似的选项（设计如此），尽管 `zypper` 的功能略少于 `rug`。

`zypper` 能够与 YaST 的集成。

# rug 选项

以下是最重要的 `rug`：
- `check`: 检查是否存在。
- `sa`: 添加服务。
- `sl`: 列出服务。
- `sub`: 订阅目录库。
- `in`: 安装包。
- `up`: 升级。

要在 SLES 系统中使用心跳，我们需要执行：

```
rug sa http://download.opensuse.repositories/ha-clustering/SLES_10/
```

`zmd` 可能包含一个或多个目录库。为了添加心跳，我们需要首先添加该服务。

列出服务将显示已添加：

| 状态 | 类型 | 名称 |
|---|---|---|
| 1 | ZYPP | SLES Server 10 |
| 2 | YUM | LMB-ha |

# 使用包

然而，我们需要检查是否订阅了该目录库：

```
rug ca

Sub'd? | Name | Service

----------------+-------

Yes | SUSE Enterprise 10 SPI

    | LMB-ha
```

我们还没有订阅新目录库，所以我们使用：

```
rug LMB-ha

Subscribed to 'LMB-ha'

rug ca

Sub'd? | Name | Service

----------------+-------

Yes | SUSE Enterprise Server 10

| LMB-ha
```

现在我们可以从新仓库安装包：

```
rug heartbeat
```

依赖关系将被自动处理。

# zypper 选项

正如我们所提到的，`zypper` 的选项与 `rug` 的选项相当兼容。在这里我们重复之前的示例，但使用 `zypper`：

```
zypper sl

|Enabled|Refresh|Type | Alias

-------+------+-----------------------

1 | Yes | rpm-md | openSU-10.3-Updates | openSU-10.3-Updates

2 | Yes | yast2 | openSU-10.3-DVD 10.3 | openSU-10.3-DVD 10.3

zypper sa http://download.opensuse.org/repositories/server/ha-clustering/SLES_10/ LMB-ha
* 添加存储库 'LMB-ha' 成功：

启用: 是

自动刷新: 是

URL: http://download.opensuse.org/repositories/server/ha-clustering/SLES_10/
```

现在如果我们列出存储库，可以看到新源可用：

```
# 第三部分：在 SUSE Linux 中使用命令行

最重要的 `zypper` 选项有：

- `zypper lr`: 列出软件库。
- `zypper sl`: 列出软件库（为了与 `rug` 兼容）。
- `zypper ar`: 添加软件库。
- `zypper sa`: 添加软件库（为了与 `rug` 兼容）。
- `zypper in`: 安装软件包。

通过 `zypper` 进行的所有更改都会反映在 YaST 中，反之亦然。

![](img/e749d3c47634a5bbb94e11699efbe992_377_0.png)

现代版本的 SUSE 将“模式”（patterns）和“产品”（products）的概念集成到了软件包管理系统中。“模式”是在初始安装期间看到的软件包包，例如“文件服务器”或“笔记本电脑”：即你为了特定目的需要的一组软件包。安装一个软件包依赖于它所需的整组软件包。这对于尽可能地启动并运行你所需的软件来说是一个非常有用的功能。“产品”也集成到了软件包管理系统中。软件包的最小集合或这些软件包的最低版本级别定义了一个产品（例如：SLES 10 Service Pack 1）。这使得系统能够精确知道它是否处于特定的 Service Pack 级别，或者它是否具备实现最小功能所需的所有软件包。

正如你所看到的，在 SUSE 系统上有多种管理软件包的方法。但所有这些都依赖于底层 RPM 软件包管理系统的智能。

在过去的一年里，为不同的 SUSE 版本构建软件包以及通过 Build Service 上的多个软件库和“I-Click”安装添加软件包的便利性方面取得了巨大进展。通常情况下，如果某个软件存在于 Linux，它几乎肯定存在于 SUSE 版本的 Linux，并且可能通过 openSUSE Build Service 或社区仓库可用。

> 除了搜索 Build Service (`http://software.opensuse.org/search`) 外，Benji Weber 的搜索工具可以在 `http://packages.opensuse.community.org/` 找到，它可以搜索从不同来源为 SUSE 发行版构建的软件包。Benji 还创建了一个命令行工具来实现相同的功能。它包含在 openSUSE 10.3 中，并且在 Build Service 的 Tools 仓库中可用：`http://download.opensuse.org/repositories/openSUSE:/Tools/`

# 第 13 章

# 处理文件
