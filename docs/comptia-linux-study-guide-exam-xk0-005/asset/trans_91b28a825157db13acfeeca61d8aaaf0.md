

为了解决这个问题，Linux 发行版创建了一套用于捆绑已编译应用程序以供分发的系统。这种捆绑包被称为**软件包**，它包含运行单个应用程序所需的所有文件。这样，你就可以将整个应用程序作为一个单一的**软件包**来安装、删除和管理，而不必将其视为一组零散的文件。

在 Linux 系统中跟踪软件包的过程称为**软件包管理**。Linux 通过数据库来跟踪系统中的已安装软件包，从而实现软件包管理。软件包管理数据库不仅记录安装了哪些软件包，还记录每个应用程序所需的具体文件及其文件位置。要确定系统中安装了哪些应用程序，只需查询软件包管理数据库即可。

不出所料，不同的 Linux 发行版创建了不同的软件包管理系统，以操作它们的软件包管理数据库。然而，多年来，两个主要的软件包管理系统脱颖而出，并成为标准：

-   Debian 软件包管理
-   Red Hat 软件包管理

由于这两种方法非常流行，Linux+ 认证考试涵盖了这两种软件包管理方法，因此本章也将详细介绍这两种方法。

每个软件包管理系统都使用不同的方法来跟踪应用程序软件包和文件，但它们都跟踪类似的信息：

-   **应用程序文件：** 软件包数据库跟踪每个单独文件及其所在的文件夹。
-   **库依赖项：** 软件包数据库跟踪每个应用程序所需的库文件，如果在安装软件包时缺少依赖的库文件，它会发出警告。
-   **应用程序版本：** 软件包数据库跟踪应用程序的版本号，以便你了解是否有该应用程序的更新版本可用。

接下来的章节将讨论用于使用这些软件包管理系统的工具。

## 安装和管理软件包

Debian 和 Red Hat 软件包管理系统拥有一套相似的工具，用于在软件包管理系统中处理软件包。我们现在将查看这两个系统及其相应的工具。

## Debian 软件包工具

正如你可能猜测的那样，Debian 软件包管理系统主要用于基于 Debian 的 Linux 系统，例如 Ubuntu。Debian 将应用程序文件捆绑到一个单一的 DEB 软件包文件中以供分发。用于处理 DEB 文件的核心工具是 `dpkg` 程序。

`dpkg` 程序是一个命令行实用工具，具有在 Linux 系统上安装、更新和删除 DEB 软件包文件的选项。`dpkg` 命令的基本格式如下：

```
dpkg [options] action package-file
```

`action` 参数定义了要对文件执行的操作。表 13.2 列出了你需要使用的常见操作。

### 表 13.2 dpkg 命令的操作

| 操作 | 描述 |
|---|---|
| -C | 搜索已损坏的安装软件包并建议修复方法 |
| --configure | 重新配置已安装软件包 |
| --get-selections | 显示当前已安装的软件包 |
| -i | 安装软件包 |
| -I | 显示未安装软件包文件的信息 |
| -l | 列出与指定模式匹配的所有已安装软件包 |
| -L | 列出与软件包关联的已安装文件 |
| -p | 显示已安装软件包的信息 |
| -P | 删除已安装软件包，包括配置文件 |
| -r | 删除已安装软件包，但保留配置文件 |
| -S | 查找拥有指定文件的软件包 |

每个操作都有一组选项，你可以使用这些选项来修改操作的基本行为，例如强制覆盖已安装的软件包或忽略任何依赖错误。

要使用 `dpkg` 程序，你必须拥有可用的 DEB 软件包，这可以通过安装 DVD 或从互联网下载软件包获得。通常，你可以在应用程序网站上找到已准备好分发的 DEB 版本应用程序软件包，或者大多数发行版都维护了一个下载软件包的中心位置。

![](img/c0a399aca0d18f8822d714ad0a173123_468_0.png)

Debian 发行版还在 www.debian.org/distrib/packages 提供了一个 Debian 软件包的中央清算中心。

当你下载预编译应用程序的 DEB 软件包时，请务必确保你获得的是适合你工作站处理器芯片的正确软件包。源代码文件是针对特定处理器编译的，如果在你的系统上尝试运行错误的软件包将无法工作。通常，处理器类型会作为软件包名称的一部分添加。

一旦下载了 DEB 软件包，请使用带有 `-i` 选项的 `dpkg` 进行安装：

```
$ sudo dpkg -i zsh_5.3.1-4+b2_amd64.deb
Selecting previously unselected package zsh.
(Reading database ... 20432 files and directories currently installed.)
Preparing to unpack zsh_5.3.1-4+b2_amd64.deb ...
Unpacking zsh (5.3.1-4+b2) ...
dpkg: dependency problems prevent configuration of zsh:
 zsh depends on zsh-common (>= 5.3.1-4); however:
 Package zsh-common is not installed.

dpkg: error processing package zsh (--install):
 dependency problems - leaving unconfigured
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Errors were encountered while processing:
 zsh
$
```

在这个示例中你可以看到，软件包管理软件会检查并确保应用程序所需的任何软件包都已安装，如果缺少任何依赖项，它会产生错误消息。这给你提供了线索，告诉你还需要安装哪些其他软件包。

如果你想查看系统上安装的所有软件包，请使用 `-l` 选项：

```
$ dpkg -l
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/half-conf/Half-inst/trig-aWait/Trig
|| Err?=(none)/Reinst-required (Status, Err: uppercase=bad)
||/ Name Version Architecture Description
+++================+++++++++++++++++++================+=
ii accountsservic 0.6.45-1ubun amd64 query and manipulate accounts
ii acl 2.2.52-3buil amd64 Access control list utilities
ii acpi-support 0.142 amd64 scripts for handling ACPI
ii acpid 1:2.0.28-1ub amd64 Advanced Config and Power
ii adduser 3.116ubunt1 all add and remove users
ii adjm-theme-ub 0.3.4-0ubunt all Ajdium message style for Ubuntu
ii adwaita-icon-t 3.28.0-1ubuntu all default icon theme of GNOME
ii aisleriot 1:3.22.5-1 amd64 GNOME solitaire card game
```

你还可以在命令行中提供搜索词，以限制输出中返回的软件包：

```
$ dpkg -l openssh*
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/half-conf/Half-inst/trig-aWait/Trig
|| Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name Version Architecture Description
++=-----------------------------------------------------------------=
ii openssh-client 1:7.6p1-4ubuntu amd64 secure shell (SSH) client
un openssh-server <none> <none> (no description available)
```

如果你需要删除软件包，你有两个选项。`-r` 操作删除软件包，但保留与该软件包关联的任何配置和数据文件。如果你只是想重新安装现有软件包且不想重新配置各项设置，这将很有用。如果你确实想要完全删除整个软件包，请使用 `-P` 操作，该操作会从系统中清除整个软件包，包括配置文件和数据文件。

![](img/c0a399aca0d18f8822d714ad0a173123_469_0.png)

`dpkg` 工具让你直接访问软件包管理系统，使在基于 Debian 的系统上安装应用程序变得更加容易。

## Red Hat 软件包工具

Red Hat Linux 发行版以及 Fedora、Rocky 和 CentOS 等其他基于 Red Hat 的发行版使用 RPM 软件包文件格式。用于处理 RPM 文件的主要工具是 `rpm` 程序。

与 `dpkg` 工具类似，`rpm` 程序也是一个用于安装、修改和删除 RPM 软件包的命令行程序。`rpm` 程序的基本格式如下：

```
rpm action [options] package-file
```

`rpm` 命令的操作如表 13.3 所示。

要使用 `rpm` 命令，你必须将 RPM 软件包文件下载到系统中。虽然你可以使用 `-i` 操作安装软件包，但更常见的是使用 `-U` 操作，它会在软件包已安装的情况下安装新软件包或升级软件包。添加 `-vh` 选项是一个流行的组合，它显示更新的进度及其正在执行的操作：

