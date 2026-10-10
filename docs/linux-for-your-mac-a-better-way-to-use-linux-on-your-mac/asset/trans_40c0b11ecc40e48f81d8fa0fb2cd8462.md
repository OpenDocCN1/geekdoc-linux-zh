

![](img/1ea833f5a3e3c1547e3dd2891f52804a_356_0.png)

*图 14.9 linuxconf 客户端是一个用于管理系统的综合工具。*

如果你第一次运行 `linuxconf`，你会看到一个大型的介绍对话框。按下 *Quit*（退出）按钮后，其主对话框将出现，如图 14.9 所示。`linuxconf` 对话框将任务分为配置和控制两部分。配置任务包括：

- **网络。** 客户端任务，例如主机名、名称服务器、路由和 PPP 配置；服务器任务，例如 NFS（*Network File System*，网络文件系统）、Apache、DNS（*Domain Name Server*，域名服务器）、邮件、Samba 和 FTP；以及其他任务，例如管理网络访问。
- **用户账户。** 普通用户和组；特殊账户，例如 PPP、SLIP 和 POP；电子邮件别名；策略，例如密码过期、shell 和 MOTD（*Message Of The Day*，每日消息）。
- **文件系统。** 访问已挂载的卷；交换文件管理；以及配额。
- **其他服务。** 初始系统服务和调制解调器管理。
- **引导模式。** 引导提示符管理和 shell 分配。

通过 `linuxconf` 对话框可用的控制任务包括：

- **控制面板。** 更改激活状态；重启和关机；挂载和卸载文件系统；超级服务器模式；配置归档。
- **控制文件和系统。** 配置配置；文件；命令；文件权限；`linuxconf` 模块和附加组件。
- **日志。** 日期、时间、时区控制；`linuxconf` 键盘控制。

### 使用 SuSE 的 YaST 命令和 YaST2 客户端

SuSE Linux 以其提供易于安装和管理的综合性 Linux 系统而闻名。SuSE 最令人印象深刻的功能之一是系统管理工具和脚本的紧密集成。虽然可以手动配置 SuSE Linux 系统，但与其他的 Linux 发行版不同，使用 `yast2` 图形客户端或最近使用的 `yast` 控制台命令来管理这种 Linux 发行版效果最佳。

这两个客户端都可以访问 SuSE 的中心资源配置文件 `/etc/rc.config`。该文件包含系统许多不同方面的设置，其内容如下（部分）：

```text
...
# NIS(YP)/NIS+ domainname, ask the admin of the server.
#
YP_DOMAINNAME=""
#
# Start the rpc.ruserd daemon in multi-user? ("yes" or "no")
# rpc.ruserd is a server which returns information about users currently
# logged in to the system.
#
START_RUSERD="no"
#
# Start the rpc.rstatd daemon in multi-user? ("yes" or "no")
# rpc.rstatd is a RPC daemon which collects performance statistics from
# kernel on serving machine.
#
START_RSTATD="no"
...
```

传统的基于控制台的 `yast` 命令不需要活动的 X 会话，这与许多其他图形管理工具不同。如果你想通过拨号访问管理网络上的远程计算机，这会非常方便。然而，`yast2` 客户端确实需要活动的 X 会话，并且可以通过高速网络用于管理远程计算机。这两个客户端都必须以 root 身份运行。

从命令行按以下方式启动基于控制台的 `yast` 命令：

```bash
# yast &
```

![](img/1ea833f5a3e3c1547e3dd2891f52804a_358_0.png)

*图 14.10 yast 命令是 SuSE 的综合管理工具。*

按下 Enter 键后，其主对话框将出现，如图 14.10 所示。`yast` 命令提供用户、系统、网络和软件管理。其初始菜单项中的几个会引导你进入其他菜单，你可以使用这些菜单来维护系统。例如，选择“Adjustments”（调整）菜单项可以提供更改语言设置、键盘映射、SuSE Linux 安装软件位置以及分区管理的功能。然而，主要功能位于“System administration”（系统管理）菜单项下。

此菜单提供：

- **硬件配置。** 新键盘、指点设备、打印机、扫描仪、调制解调器、CD-ROM 驱动器以及网络接口。
- **配置。** 几乎所有网络服务和设备。
- **引导模式管理。** 例如使用 X11 显示管理器。
- **管理用户和组。**
- **执行系统备份。**
- **安全设置。** 用于限制系统访问或启用其他安全功能。
- **日期、时间和时区设置。**

要使用图形 `yast2` 客户端，请在 X11 终端窗口的命令行上输入其名称，如下所示：

```bash
# yast2 &
```

按下 Enter 键后，其主管理工具将出现，如图 14.11 所示。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_359_0.png)

*图 14.11 yast2 客户端是 SuSE 最新的图形管理工具。*

与 `yast` 命令类似，`yast2` 提供设备、软件、网络和远程系统管理。其初始菜单项会启动你可以用来维护系统的管理模块。这些包括：

- **硬件。** 用于配置打印机和系统声音服务。
- **软件管理。** 用于安装、删除或更新系统软件。
- **网络。** 配置和控制服务器软件、远程文件系统（如 NFS）以及电子邮件。
- **系统调优。** 在本文撰写时，此功能仅涵盖使用直接内存访问（DMA）控制 IDE 硬盘。
- **远程服务。** 远程管理和安装允许网络管理员在远程计算机上启动 `yast2` 模块，或通过串行网络连接安装 SuSE Linux。

### 其他遗留工具

你可能会发现 Yellow Dog Linux 和 LinuxPPC 2000 Q4 中包含一个或多个遗留的图形管理工具。这些工具基于控制台，不需要活动的 X 会话。虽然不如 `yast` 或 `linuxconf` 那样全面，但这些程序仍在系统管理中占据一席之地。名为 `ntsysv` 的一个程序用于控制下次系统启动时应启动哪些服务。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_360_0.png)

*图 14.12 `ntsysv` 命令是一个有用的遗留工具，你可以用它来控制基于 Red Hat 的 PowerPC Linux 系统上的服务。*

按以下方式在控制台或 X11 终端窗口的命令行上输入其名称以启动 `ntsysv`（以 root 身份）：

```bash
# ntsysv
```

按下 Enter 键后，控制台将显示如图 14.12 所示。

此命令的工作方式与手动 `chkconfig` 命令类似，后者可用于重新排序各种运行级别中的服务。使用 `ntsysv` 时，滚动浏览服务列表并按空格键以切换是否希望在下一次系统启动时使用该服务。

你可以通过在 `/etc/rc.d/init.d` 目录下指定其脚本名称来快速启动、停止或重启特定服务，例如 Apache，如下所示（以 root 身份）：

```bash
# /etc/rc.d/init.d/httpd start
# /etc/rc.d/init.d/httpd stop
# /etc/rc.d/init.d/httpd restart
```

这些命令行将启动、停止或重启指定的服务（在进行任何服务配置更改后非常有用）。要使更改在特定的运行级别生效，请使用 `chkconfig` 命令。此程序从命令行使用来更改 `/etc/rc*.d` 目录中的设置，其中 *x* 代表特定的运行级别。

你还可以通过使用带有 `--list` 选项的 `chkconfig` 命令来快速了解整个系统的服务配置快照，如下所示：

```bash
# chkconfig --list
syslog     0:off   1:off   2:on    3:on    4:on    5:on    6:off
crond      0:off   1:off   2:on    3:on    4:on    5:on    6:off
netfs      0:off   1:off   2:off   3:on    4:on    5:on    6:off
network    0:off   1:off   2:on    3:on    4:on    5:on    6:off
random     0:off   1:off   2:on    3:on    4:on    5:on    6:off
keytable   0:off   1:off   2:on    3:on    4:on    5:on    6:off
atd        0:off   1:off   2:off   3:on    4:on    5:on    6:off
gpm        0:off   1:off   2:on    3:off   4:off   5:off   6:off
sendmail   0:off   1:off   2:on    4:on    5:on    6:off
httpd      0:off   1:off   2:off   3:off   4:on    5:off   6:off
...
```

此处并未显示所有输出。在具有完整安装的 LinuxPPC 2000 Q4 系统上，你会发现你几乎可以控制 60 种不同的服务！使用 `chkconfig`，你可以快速控制在特定运行级别中运行的服务。例如，要控制系统上的 Apache Web 服务器，并分配或限制各种运行级别，例如 3（多用户模式，文本控制台登录）或 5（多用户模式，图形 X 登录），请如下使用命令：

```bash
# chkconfig --level 3 httpd on
# chkconfig --level 5 httpd off
```

在这些示例中，如果 Linux 启动到运行级别 3，Apache 将会启动，但如果启动到图形 X 登录（运行级别 5），则不会启动。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_361_0.png)

> 你可以使用 `vntc` 客户端控制许多不同的网络服务。点击 Network Services（网络服务）模块，然后选择 On with custom configuration（以自定义配置开启）按钮。

### 管理软件

本节介绍了普遍存在的 `rpm` 命令，也称为 Red Hat Package Manager（Red Hat 包管理器）。RPM 是一种独特的软件管理技术，提供包管理功能，即能够以包的形式安全地捆绑、分发、安装、删除以及管理其他软件。RPM 被许多不同计算机平台上的软件开发者使用，也在几乎所有的 PowerPC Linux 发行版上使用，Debian GNU/Linux 除外，后者使用不同的打包系统和 .deb 软件归档。

你将学习从命令行使用 `rpm` 命令的基础知识，然后学习如何启动和使用在 X11 下工作的两种不同的图形 RPM 客户端。你还将学习如何使用 `rpm` 从头开始构建和安装软件。

