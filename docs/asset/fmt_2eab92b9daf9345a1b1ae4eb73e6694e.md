
在随后的屏幕上，选择应该安装 GRUB 引导加载程序的驱动（它可能类似于 `/dev/sda`）。点击进入下一个屏幕，它应该会告诉你安装已完成。恭喜！你已经安装了 Kali。点击“继续”。Kali 将尝试重启，你会看到几行代码在空白屏幕上闪过，最后你会看到 Kali 的登录界面，如图 11 所示。

![](img/b810c73192f8fd9b51956a9c6a4973cf_37_1.png)

图 11：登录界面

使用密码 `kali` 或你选择的任何密码登录 `kali`。你应该会看到 Kali 桌面，如图 12 所示。

![](img/b810c73192f8fd9b51956a9c6a4973cf_38_0.png)

图 12：主屏幕

你现在准备好开始你进入兴奋的黑客领域之旅了！欢迎！

# 通过 Windows 的 Linux 子系统安装 Kali

对于那些寻找不侵入性较低的方法运行 Linux 的来说，微软提供了 Windows 的 Linux 子系统（WSL）。使用它，你可以在无需安装虚拟机的情况下学习 Linux。缺点是网络功能（因此也是黑客能力）未启用。这意味着你可以学习 Linux，但无法通过此子系统研究黑客技术。尽管如此，以下是在 Windows 系统上安装 WSL 的方法。

第一步是启用 WSL。通过在命令行提示符中运行或在应用程序菜单搜索来打开 PowerShell。然后在 PowerShell 提示符下输入以下内容：

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Subsystem-Linux
Do you want to restart the computer to complete this operation now?
[Y] [N] (default is Y)
```

如你所示，PowerShell 将询问你是否要重启系统以启用 WSL。按回车。

现在你已经启用了此功能并重启了系统，请安装 Kali。前往 Windows 应用商店（https://apps.microsoft.com/store/apps）。在那里，你会看到许多 Linux 发行版的图标。点击 Kali Linux，然后选择“获取”。

Kali 将开始下载。这是一个精简的、仅包含必要的 Kali 版本，所以下载会很快。完成后，系统将提示你输入用户名和密码。

你刚刚安装的精简版工具很少（取决于你对 `工具` 一字的定义）。因此，你需要下载所有的 Kali 工具。输入以下命令进行更新和升级：

```
sudo apt update
sudo apt upgrade
sudo apt install kali-linux-everything
```

现在你已经启用此功能并重启了系统，请安装 Kali。前往 Windows 应用商店（https://apps.microsoft.com/store/apps）。在那里，你会看到许多 Linux 发行版的图标。点击 Kali Linux，然后选择“获取”。

Kali 将开始下载。这是一个精简的、仅包含必要的 Kali 版本，所以下载会很快。完成后，系统将提示你输入用户名和密码。

你刚刚安装的精简版工具很少（取决于你对 `工具` 一字的定义）。因此，你需要下载所有的 Kali 工具。输入以下命令进行更新和升级：

```
sudo apt update
sudo apt upgrade
sudo apt install kali-linux-everything
```

Script 是在解释型环境中运行的一系列命令，它将每一行都转换为代码。许多黑客工具仅仅是脚本。脚本可以使用 bash 解释器或任何其他的脚本语言解释器，如 Python、Perl 或 Ruby。Python 是目前黑客中最流行的解释器。

Shell 是在 Linux 中运行命令的环境和解释器。最广泛使用的 Shell 是 bash，全称为 Bourne-again shell，但其他 Shell 包括 C shell 和 Z shell。我在本书中将专门使用 bash shell。

Terminal 是一个命令行界面（CLI）。

# 开始之旅

## 基础知识

根据我们的本性，黑客是行动者。我们想跳过冗长的理论。本章节旨在为你提供一些基础技能，让你运行起来。在这种情况下，我们不会深入探讨任何概念。

## 入门术语

在我们开始 Linux 之旅之前，我想介绍几个有助于理解后续概念的术语。

Binaries 这个术语指的是可以执行的文件，类似于 Windows 中的可执行文件。二进制文件通常位于 `/usr/bin` 或 `/usr/sbin` 目录，包括 `ps`、`cat`、`ls` 和 `ifconfig` 等工具（我们将在本章涉及这些内容）。

与 Windows 不同，Linux 文件系统是大小敏感的。这意味着 `Desktop` 和 `desktop` 是不同的，每一个都代表不同的文件或目录名。

Directory 这与 Windows 中的文件夹相同。目录提供了一种组织文件的方式。

Home 每个用户都使用自己的 `/home` 目录，这通常是创建文件的地方。

Kali Linux 是一种专门为渗透测试设计的 Linux 发行版。它预装了数百种工具，节省了你下载和安装它们的时间。

root 与几乎所有的操作系统不同，Linux 有一个为信任用户设计的管理员（超级用户）账户，它可以配置系统、添加用户和更改密码等操作。在 Linux 中，该账户被称为 `root`。作为黑客或渗透师，你经常需要使用 `root` 来管理系统。事实上，许多黑客工具要求你使用 `root` 账户。

Script 是在解释型环境中运行的一系列命令，它将每一行都转换为代码。许多黑客工具仅仅是脚本。脚本可以使用 bash 解释器或任何其他的脚本语言解释器，如 Python、Perl 或 Ruby。Python 是目前黑客中最流行的解释器。

Shell 是在 Linux 中运行命令的环境和解释器。最广泛使用的 Shell 是 `bash`，但其他 Shell 包括 C shell 和 Z shell。我在本书中将专门使用 bash shell。

Terminal 是一个命令行界面（CLI）。

# Kali 概览

一旦启动 Kali，你将看到登录界面。使用 Kali 账户用户名 `kali` 和默认密码 `kali` 进行登录（如果你之前更改过密码，请在此处使用你的新密码）。现在，你已经可以访问你的 Kali 桌面了。我们将快速查看桌面的两个最基本的方面：终端界面和文件结构。

## 终端

使用 Kali 的第一步是打开终端，这是我们在书中将使用的命令行界面。你可以在桌面的左侧找到终端图标。点击此图标打开终端。你的新终端看起来应该像图 1-1 所示。

![](img/b810c73192f8fd9b51956a9c6a4973cf_42_0.png)

图 1-1：Kali 终端

此终端打开了命令行环境，被称为 shell（外壳），它允许你在底层操作系统上运行命令并编写脚本。尽管 Linux 有许多不同的 shell 环境，但最流行的是 bash shell，它是许多 Linux 发行版中的默认 shell。

要更改你的密码，你可以使用 `password` 命令。

## Linux 文件系统

Linux 文件系统结构与 Windows 有些不同。Linux 在文件系统的底部没有物理驱动器（如 C: 盘），而是使用逻辑文件系统。文件结构的最顶端是 `/`，通常称为文件系统的根（root），就像一棵倒立的树（见图 1-2）。请记住，这与 root 用户是不同的概念。这些术语初看起来看起来可能让人困惑，但一旦你习惯了 Linux，它们就会很容易区分。

![](img/b810c73192f8fd9b51956a9c6a4973cf_43_0.png)

图 1-2：Linux 文件系统

文件系统的根 (`/`) 位于树的顶端，以下是最需要熟悉的子目录：

- `root`: 万能的 root 用户的家目录
- `/etc`: 通常包含 Linux 配置文件——控制程序何时以及如何启动的文件
- `/home`: 用户的家目录
- `/mnt`: 其他文件系统挂载或挂载到文件系统的地方
- `/media`: 通常 CD 和 USB 设备挂载或挂载到文件系统的地方
- `/bin`: 应用程序二进制文件（相当于 Microsoft Windows 中的可执行文件或 macOS 中的应用程序）所在的地方
- `/lib`: 存放类似于 Windows DLL 的库（共享程序）的地方

在本书中，我们将花更多时间研究这些关键目录。理解这些一级目录对于从命令行导航文件系统至关重要。

在开始之前，有一点很重要：在执行例行任务时你不应该以 root 身份登录，因为当你以 root 身份登录时，任何攻击你系统的人（黑客有时也会被黑客）都会立即获得 root 权限，从而“拥有”你的系统。在启动普通应用程序、浏览网页、运行 Wireshark 等工具时，请以普通用户身份登录。对于你在书中将完成的练习，保持 root 身份登录应该是可以。

# Linux 基础命令
