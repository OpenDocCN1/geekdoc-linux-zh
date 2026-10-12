
在接下来的两个章节中，我们将探索 `apt` 的主要替代方案——`yum`。

## 配置 `yum` 客户端

从历史上看，许多丰富的 Linux 用户对两个 RPM 市场领军者 Red Hat 和 SUSE 的补丁管理工具并不满意。他们的问题部分与他们对特定发行版补丁管理工具的依赖有关。正如我们在第 1-3 章看到的，SUSE 的 Online Update 和 Red Hat Update Agent 都是极好的工具。遗憾的是，这些工具无法与其他发行版配合使用，而且它们对 Linux 社区的贡献造成了官僚化的过滤。此外，它们没有 `apt` 甚至 Smart Program Manager 那样广泛的社区支持。

这种不满意感从 2003 年秋季 Fedora Linux 的首次发布开始改变。Red Hat 将其企业级 Linux 发行版转向订阅支持模型，同时通过 Fedora Linux 项目转向社区。为了增强对 Fedora 的社区支持，Red Hat 整合了 Yellow Dog 发行版在补丁管理方面的工作。他们的工具被称为 `yum`，是 "Yellowdog Updater, Modified" 的缩写。结合第 5 章“为发行版配置 `apt`”中描述的 Fedora `apt` 仓库，以及第 2 章“在 Red Hat/Fedora 网络上整合补丁”中描述的 Red Hat Update Agent，现在现在已经包含了多种补丁管理工具。

随着 2004 年 Novel 收购 SUSE，变化持续。正如我们在第 3 章“SUSE 的更新和 `rsync` 镜像”中看到的，SUSE 已经将它的 Online Update 服务器整合到 `YaST` 中。Novel 已经将 Linux 整合到其用于补丁管理的 Jenkins 系统（以前称为 Red Carpet）。截至本文写作，评估 Linux 社区对 Jenkins 补丁管理工具的反应还时过早。

换句话之，如果你想用 Linux 社区熟悉的工具管理基于 RPM 发行版的补丁，你可以使用 `yum` 或 `apt`。一些开发者更倾向于 `yum`，因为它是为 RPM 发行版定制的，特别是由 Red Hat 发布的版本。另一些人更倾向于 `apt`，因为其相关的社区支持水平。`yum` 命令也受到 Fedora、俄罗斯的 AspLinux 和 Yellow Dog Linux 的支持。

在本章中，我们将扩展对各种 Linux 客户端 `yum` 的讨论，以展示你如何帮助管理各种基于 RPM 发行版的补丁。但首先，我们将探索 `yum` 作为基于 RPM 系统的历史和工作原理。

## 6.1 基础 `yum` 进程

从结构上说，`yum` 是为基于 RPM 的发行版构建的。正如 `www.phy.duke.edu/rgb/General/yum_HOWTO.php` 在线 `yum` HOWTO 中提到的，`yum` 使用与 Red Hat 和其他 RPM 发行版“相同的工具和 Python 绑定”来安装软件包并自动解决依赖。

`yum` 和 `apt` 都依赖于包头。每个软件包的包头都包含正向和反向依赖信息。在完整的数据库中拥有这些信息后，`yum`（以及 `apt`）可以帮助你安装选择的软件包，以及任何满足依赖关系所需的包。正如缩写所示，`yum` 是 Yellowdog Updater, Modified。

### 6.1.1 Yellow Dog 和 `yum`

`yum` 的原始版本被称为 `yup`。虽然 Yellow Dog Linux 是为 Apple 开发的，但它是基于 `yum`。

### 6.1.2 Yellow Dog 和 `yum`

`yum` 的原始版本被称为 `yup`。虽然 Yellow Dog Linux 是为 Apple 开发的，但它是基于 `yum`。

### 6.1.3 仓库和包头

`yum` 的一个优势是你可以使用它在标准 FTP 或 HTTP 服务器上配置仓库。为了与 Red Hat 保持兼容，`yum` 开发者使用 Python 语言编写软件包，而 Red Hat 也使用这种语言。

另一个优势是 `yum` 命令依赖于包头。

### 6.1.4 需要的 `yum` 软件包

`yum` 系统非常紧凑。二进制 RPM 包小于 200KB。它包含了管理补丁和在系统上创建仓库所需的一切：`yum` 和 `yum-arch` 命令。正如我们在第 7 章看到的，Fedora Core 3/4 及后续发行版使用 `createrepo` 代替 `yum-arch` 命令来帮助你配置仓库。

如果你正在运行 Red Hat 或 Fedora 并想继续使用 `update`，可以修改配置文件从 `yum` 仓库获取更新。或者，如果你学习 `yum` 命令，你将再也不需要使用 `update` 了。

## 6.2 示例 `yum` 客户端

本书关注 Red Hat/Fedora、SUSE 和 Debian。在这些发行版中，只有 Fedora Linux 支持 `yum`。然而，Red Hat Enterprise Linux 也有多种 `yum` 仓库。而且某些 Red Hat Enterprise Linux 的重新编译版使用 `yum` 作为管理补丁的主要手段。

## 6.2. Fedora

我们在第 1 章“补丁管理系统”中简要检查了如何将 Fedora 配置为 `yum` 客户端。在本节中，我们将更详细地检查配置过程。该过程分为两个部分。你已经将 Fedora 计算机配置为 `yum` 客户端。在本节中，你将引导 Fedora 版本的 Red Hat Update Agent（更新代理）指向相同的 `yum` 仓库。

> **注意**
>
> 从 Fedora Core 5 开始，Red Hat 已用 Package Updater（也称为 `Pup`）替换了 Update Agent。如果你更倾向于使用 Update Agent，仍然可以从 Fedora Core 5 仓库安装 `update2` 和 `up2date` 包。遗憾的是，我未能在本章中包含 Fedora Core 5，因为第一个测试（beta）版本在本书送往印刷厂时才发布。

### Fedora 的 Red Hat Update Agent 和 `yum`

默认情况下，Fedora 版本的 Red Hat Update Agent 配置为使用 `yum`。与 Update Agent 关联的关键配置文件是 `/etc/sysconfig/rhn` 目录下的 `sources` 文件。对于 Fedora Core 3，默认仓库直接在该文件中引用。从 Fedora Core 4 开始，以下命令将搜索 `/etc/yum.repos.d` 目录中指定的仓库：

```
repomgr fedora http://fedora.redhat.com/
```

在本节中，我将检查 Fedora Core 3 和 4 的配置文件。虽然起初可能令人困惑，但我相信通过对比，你可以学习到关于为更新配置 `yum` 的知识。此外，如果你使用 Red Hat Enterprise Linux 4（或相关的“重构”发行版），你将在本章后面的部分看到为什么这对于在 Fedora Core 3 上配置 `yum` 有帮助。

正如第 1 章建议的，与 Fedora 发布版相关的四个仓库（以及另外两个值得关注的）：

- `os` 与基础发行版相关，包含了你在 Fedora 安装光盘上找到的包。
- `updates` 包含稳定包，这些包经过更新或修订以解决安全问题或引入新功能。
- `updates-testing` 增加了尚未认为生产就绪的更新候选文件（但如果你急需更新，你可能会考虑它们）。
- `development` 包含不稳定的包，这些包可能每天都会进行修订。

`extras` 是第五个大类；实际上，`extras` 类别中还有几个额外的开发和测试仓库。如果你对这种层面的细节感兴趣，可以搜索你喜欢的 Fedora 镜像站的 `extras` 子目录。

`extras-development` 是第六个类别，类似于常规开发仓库。

Fedora Core 3 的默认配置包含以下命令行行，它们配置了到 `yum` 安装 (`os`) 和更新 (`updates`) 仓库的连接：

```
yum fedora-core-3
http://download.fedora.redhat.com/pub/fedora/linux/core/3/$ARCH/
yum updates-released-fc3
http://download.fedora.redhat.com/pub/fedora/linux/core/updates/3/$ARCH/
yum-mirror fedora-core-3 http://fedora.redhat.com/download/up2date-mirrors/fedora-core-3
yum updates-released-fc3
http://fedora.redhat.com/download/up2date-mirrors/released-fc3
```

默认情况下，Fedora Core 4 的配置指向 `/etc/yum.repos.d` 目录文件中的默认仓库。与安装 (`os`) 和更新 (`updates`) 仓库关联的文件是 `fedora.repo` 和 `fedora-updates.repo`。这些文件中的关键命令包括：
