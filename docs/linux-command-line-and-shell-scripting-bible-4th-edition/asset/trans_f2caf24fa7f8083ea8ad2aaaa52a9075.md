
## 基于 Red Hat 的系统

与基于 Debian 的发行版一样，基于 Red Hat 的系统也有多种可用的前端工具。常见的工具有：

- **yum**：用于 Red Hat、CentOS 和 Fedora
- **zypper**：用于 openSUSE
- **dnf**：*yum* 的更新版本，带有一些额外的功能

这些前端都基于 *rpm* 命令行工具。下面部分将讨论如何使用这些基于 *rpm* 的工具来管理软件包。重点将放在 *dnf* 上，但其他软件包使用类似的命令和格式。

### 列出已安装的软件包

要查看系统当前安装了什么，请在 shell 提示符下输入以下命令：

```
dnf list installed
```

信息可能会在显示屏上飞速滚动，因此最好将已安装软件的列表重定向到一个文件中。然后，你可以使用 `more` 或 `less` 命令（或图形界面编辑器）以受控的方式查看该列表。

```
dnf list installed > installed_software
```

要了解特定软件包的详细信息，*dnf* 真的表现出色。它不仅会给出非常详细的软件包描述，而且通过另一个简单的命令，你还可以查看该软件包是否已安装：

```
$ dnf list xterm
Last metadata expiration check: 0:05:17 ago on Sat 16 May
2020 12:10:24 PM EDT.
Available Packages
xterm.x86_64                      351-1.fc31
updates
```

```
$ dnf list installed xterm
Error: No matching Packages to list
```

```
$ dnf list installed bash
  Installed Packages
  Bash.x86_64                     5.0.11-1.fc31
  @updates
  $
```

最后，如果你需要知道文件系统中的某个特定文件是由哪个软件包提供的，功能强大的 `dnf` 也可以做到！只需输入以下命令即可：

```
dnf provides file_name
```

下面是一个查找提供 `/usr/bin/gzip` 文件的软件包的示例：

```
$ dnf provides /usr/bin/gzip
  Last metadata expiration check: 0:12:06 ago on Sat 16 May
  2020 12:10:24 PM EDT.
  gzip-1.10-1.fc31.x86_64 : The GNU data compression program
  Repo       : @System
  Matched from:
  Filename    : /usr/bin/gzip

  gzip-1.10-1.fc31.x86_64 : The GNU data compression program
  Repo       : fedora
  Matched from:
  Filename    : /usr/bin/gzip

  $
```

`dnf` 检查了两个独立的软件源：本地系统和默认的 fedora 软件源。

### 使用 dnf 安装软件

使用 `dnf` 安装软件包极其简单。以下是从软件源安装软件包、其所需库和软件包依赖关系的基本命令：

```
dnf install package_name
```

下面是一个安装 `zsh` 软件包的示例，该软件包提供了一个替代的命令行 shell：

```
$ sudo dnf install zsh
[sudo] password for rich:
Last metadata expiration check: 0:19:45 ago on Sat 16 May
2020 12:05:01 PM EDT.
Dependencies resolved.
===================================================================================================
Package                 Architecture        Version              Repository
Size
===================================================================================================

Installing:
 zsh                     x86_64            5.7.1-6.fc31         updates
    2.9 M

Transaction Summary
===================================================================================================
Install  1 Package

Total download size: 2.9 M
Installed size: 7.4 M
Is this ok [y/N]:
Downloading Packages:
zsh-5.7.1-6.fc31.x86_64.rpm                        1.5 MB/s | 2.9 MB
-----------------------------------------------------------------------
    Total                                        1.0 MB/s |
2.9 MB     00:02
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                        1/1
  Installing       : zsh-5.7.1-6.fc31.x86_64                                1/1
  Running scriptlet: zsh-5.7.1-6.fc31.x86_64                                 1/1
  Verifying        : zsh-5.7.1-6.fc31.x86_64                                 1/1

Installed:
  zsh-5.7.1-6.fc31.x86_64

Complete!
```

> **注意**
>
> 在上面的示例中，在 `dnf` 命令之前使用了 `sudo` 命令。该命令允许你切换到 root 用户以运行该命令。你应该仅在为了执行管理任务（如安装和更新软件）时才暂时切换到 root 用户。

你可以开始看到 dnf 的优势之一，即它使用非常逻辑清晰且用户友好的命令。

### 使用 dnf 升级软件

在大多数 Linux 发行版中，当你在图形界面中工作时，你会看到那些可爱的小通知图标，告诉你需要升级到软件的新版本。但在命令行下，这需要多做一些工作。

要查看已安装软件包的所有可用升级列表，请输入以下命令：

```
dnf list upgrades
```

如果对这个命令没有响应总是很棒的，因为这意味着你没有任何需要升级的软件包！然而，如果你发现某个特定软件包需要升级，则输入以下命令：

```
dnf upgrade package_name
```

如果你希望升级升级列表中列出的所有软件包，只需输入以下命令：

```
dnf upgrade
```

> **注意**
>
> dnf 的一个不错的附加功能是 upgrade-minimal 命令。它将软件包升级到最新的错误修复或安全补丁版本，而不是最新的最佳版本。

### 使用 dnf 卸载软件

dnf 工具还提供了一种简单的方法来卸载你不再需要的系统上的软件：

```
dnf remove package_name
```

不幸的是，截至本文撰写时，没有选项或命令可以删除应用程序文件但保留任何配置或数据文件。虽然使用包管理系统安装的软件包会使生活轻松许多，但它并不总是没有问题的。偶尔事情也会出错。幸运的是，有办法帮忙。

### 处理损坏的依赖项

有时，随着多个软件包被加载，一个软件包的软件依赖项可能会因另一个软件包的安装而被覆盖。这被称为损坏的依赖项。

如果这种情况在你的系统上发生，请首先尝试以下命令：

```
dnf clean all
```

然后尝试使用 dnf 命令中的升级选项。有时，只需清理任何位置错误的文件即可帮助解决问题。

如果这没有解决问题，请尝试以下命令：

```
dnf repquery --deplist package_name
```

此命令显示软件包的所有库依赖项以及提供它们的软件包。一旦你知道了软件包所需的库，你就可以安装它们。下面是一个确定 xterm 软件包依赖项的示例：

```
# dnf repquery --deplist xterm
```

> **注意**
>
> yum 工具的 upgrade 命令支持 --skip-broken 选项，该选项跳过损坏的软件包，但试图继续升级其他软件包。dnf 工具会自动执行此操作。

### RPM 软件源

就像 apt 系统一样，dnf 在安装时设置了其软件源。对于大多数用途来说，这些预装软件源将完全满足你的需求。但是，当你需要从不同的软件源安装软件时，以下是一些你需要知道的事项。

> **提示**
>
> 明智的系统管理员坚持使用经过批准的软件源。经过批准的软件源是指由发行版官方网站认可的软件源。如果你开始添加未经批准的软件源，你将失去稳定性的保证。而且你将进入损坏依赖项的领域。

要查看你当前正在从哪些软件源获取软件，请输入以下命令：

```
dnf repolist
```

如果你没有找到需要从中获取软件包的软件源，那么你需要进行一些配置文件编辑。dnf 软件源定义可以在两个地方找到：

- 在 /etc/dnf/dnf.conf 配置文件中
- 作为 /etc/yum.repos.d 目录中的单独文件

