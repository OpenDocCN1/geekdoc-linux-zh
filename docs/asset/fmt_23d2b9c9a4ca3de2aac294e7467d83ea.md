
当我们第一次安装时，第一件事是运行更新器以确保一切都是最新的。根据 `dnf list installed`，我们目前的版本是 2.0.2-5，根据 `dnf check-update`，当前发布是 2.0.3-1。我们将使用 DNF 更新它：

## 功能变更

通常情况下，Linux 的更新是正确的，但某些更新是因为设计方式已被取代而发生的。让我们以一个在全球范围内使用的东西为例——PHP 开发语言。阅读 PHP 网站上关于从版本 5.5 迁移到 5.6 的页面。

> 小贴士
>
> 这些调用将在未来的 PHP 版本中被移除。

## 筛选更新

你应该采取的方法非常简单。运行软件包器的“检查是否有可用更新”命令（在 DNF 中，这将是 `dnf check-update`）。然后查看它告诉你的可以更新的项目列表，并对你高度依赖的核心组件进行记记。它会告诉你计划升级到哪个版本，你可以要求软件包管理器显示当前安装的版本（在 DNF 中，那就是 `dnf list installed`）。

## 更新 CUPS

一旦决定了更新哪些项目，将它们传递给软件包管理器。在示例中，我们将更新 CUPS（Linux 的打印核心）。根据 `dnf list installed`，我们目前的版本是 2.0.2-5，根据 `dnf check-update`，当前发布是 2.0.3-1。我们将使用 DNF 更新它：

```bash
[root@localhost ~]# dnf upgrade cups
Last metadata expiration check performed 00:03:17 ago on Sat Aug 1 19:45:51 2015.
Dependencies resolved.
```

| 包 | 架构 | 版本 | 存储库 | 大小 |
|---|---|---|---|---|
| cups | x86_64 | 1:2.0.3-1.fc22 | updates | 1.3 M |
| cups-client | x86_64 | 1:2.0.3-1.fc22 | updates | 153 k |
| cups-filesystem | noarch | 1:2.0.3-1.fc22 | updates | 99 k |
| cups-libs | x86_64 | 1:2.0.3-1.fc22 | updates | 387 k |

升级：

事务摘要

升级 4 个包

总下载大小：2.0 M

是否确定 [y/N]:

噢，如果你在 wonder为什么我们使用了 `upgrade` 指令而不是之前使用的 `update` 指令：它们的作用是一样的，但作者似乎保留了 `upgrade` 指令，因为它对任何用过 Yum 包管理器的人来说都是熟悉的。

这种受控的更新将保持你的 Linux 平台稳定。

## 我想要另一个桌面管理器吗？

我们已经提到过，Linux 上有许多替代程序可以实现你想要的任何操作。其中一个关键选项是为你的 Linux 机器提供图形用户界面（GUI）的桌面环境。在我们的测试机器上，默认安装了 Gnome 桌面，但你有很多选择。

由于桌面环境是复杂的集合体，它们在 Linux 中是以“包组”（package groups）的形式实现的。因此，如果我们运行 `dnf grouplist`，它会告诉我们有哪些可用选项：

```bash
[root@localhost ~]# dnf grouplist
Last metadata expiration check performed 03:31:12 ago on Sat Aug 1 19:45:51 2015.
可用环境组：
```

- 最小安装 (Minimal Install)
- Fedora 服务器 (Fedora Server)
- Fedora 工作站 (Fedora Workstation)
- Fedora 云服务器 (Fedora Cloud Server)
- KDE Plasma 工作空间 (KDE Plasma Workspaces)
- Xfce 桌面 (Xfce Desktop)
- LXDE 桌面 (LXDE Desktop)

> 小贴士
>
> 桌面环境可能很大，所以不要下载了之后就让它们闲置在那里而不使用。

顺便说一下，这是一个简化列表。如果我们想安装 KDE，可以运行 `dnf groupinstall KDE Plasma Workspaces`。同样，要安装 Xfce 桌面，我们需要运行 `dnf groupinstall Xfce Desktop`。

我们选择了 Xfce，它花费了大约五分钟下载安装。然而，一旦下载完成，你需要告诉系统使用它。这是一个运行 `switchdesk` 工具的简单案例（注意你必须先安装 `switchdesk` 包——现在你应该已经知道怎么做了）：

```bash
[root@localhost ~]# switchdesk xfce
Red Hat Linux switchdesk 4.0
Copyright (C) 1999-2010 Red Hat, Inc
Redistributable under the terms of the GNU General Public License Desktop now set up to run xfce.
```

有趣的是，你可以在 `switchdesk` 的输出中看到 Fedora 的传承，其中提到了 Red Hat 是原始生产者。

## 需要注意的问题

我们已经走过了从裸机系统到可运行 Linux 机器的过程，结果应该非常令人印象深刻——一台拥有吸引人的用户界面（它们开箱即用的效果都很好）的运行机器，能够与其他计算机通信、上网并运行你想要使用的应用程序。然而，这才是现实世界，当你真正安装和使用 Linux 时，有几点需要记住。

![](img/c00dda504be4d70c6e7dd488ae0af42a_105_0.png)

## 它是真实的吗？

在下载 Linux 发行版的章节中，我们没有提到一点：每当你下载任何开源文件时，都应该确保下载的镜像是真实的。如果你是从官方网站下载的，通常没问题，但你应该检查一下。你使用“校验和”（checksum）来完成——它是由一个程序计算的，该程序读取文件的每一个字节并执行计算，得出一个字符字符串。原理是，只有该文件会计算出该字符串。

以我们的 Fedora 镜像为例，来说如何检查文件的完整性。如果我们看 Fedora 网站上安装程序文件所在的目录，会看到许多文件：

- `Fedora-Live-Workstation-x86_64-22-3.iso`
- `Fedora-Workstation-22-x86_64-CHECKSUM`
- `Fedora-Workstation-netinst-x86_64-22.iso`

`Fedora-Live-Workstation-x86_64-22-3.iso` 是我们下载并用于安装 Linux 的镜像。如果我们下载 `Fedora-Workstation-22-x86_64-CHECKSUM` 文件（非常小）并检查其内容，我们看到一条加密信息：

```
--BEGIN PGP MESSAGE--
Hash: SHA256
The image (s) are generated with sha256.
SHA256 (Fedora-Workstation-netinst-x86_64-22.iso) = c9d22e708b213358b2193670fc4b4824cf96d4d07bd6c28
SHA256 (Fedora-Live-Workstation-x86_64-22-3.iso) = 615abcf89709a46078dd1d39638019aa6f6b0ff823534f1af0551bbbc
-----BEGIN SIGNATURE-----
Version: GPG v1
iQIBCAAGBQQV4xe1A0JBtwOFDHV40QaJPHV0Ye5mcyQQPT0Q9HpTMW0AdGpbnBCQtJi2MeoqP5LX8AD55FC5qmnQzzbXQC6666fff0YUtUtUtUtUtm43Eb0DG9Y111b22141444449999999999999992222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222
-----END SIGNATURE-----
```

看到 `Hash: SHA256` 的地方了吗？它告诉我们校验和的类型是安全算法（Secure Algorithm）。它还告诉我们安装程序的校验和是：

615abcf89709a46078dd1d39638019aa6f6b0ff823534f1af0551bbbc

## 开始开始

所以，如果我们为 ISO 计算 SHA256 校验和，在 Windows 上应该得到相同的序列。在 Mac 上，我们使用 `shasum` 命令完成：
