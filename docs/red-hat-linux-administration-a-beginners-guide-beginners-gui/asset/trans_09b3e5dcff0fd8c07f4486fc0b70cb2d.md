
samba-common、samba、samba-client、samba-swat 以及 redhat-config-samba。如果你只需要进行服务器安装，那么至少需要 samba 和 samba-common。如果你只关心作为客户端使用，那么你需要 samba-common 和 samba-client。如果你不想手动设置配置文件，那么你需要安装 samba-swat 或 redhat-config-samba，或者两者都安装。

## 关键技能

### 18.3 执行 Samba 管理

本节描述了管理 Samba 的一些问题。我们将学习如何启动和停止 Samba，如何使用 SWAT 或 redhat-config-samba 执行常见的管理任务，以及如何编写和运行测试程序。最后，我们将查看使用加密口令的过程。

### 启动和停止 Samba

如果你想手动控制 Samba，可以使用 `/etc/init.d/smb` 脚本启动和停止服务。这将同时处理 smbd 和 nmbd 服务。例如，要使用此脚本显式启动服务，你可以运行：

```
[root@picard /root]# /etc/init.d/smb start
```

要使用此脚本停止服务，你可以运行：

```
[root@picard /root]# /etc/init.d/smb stop
```

为了确保它在系统启动时自动运行，你可以通过从“Server Settings”子菜单中选择“Services”工具来启动服务 GUI 工具，或者在命令行中输入 redhat-config-services。正如你可能从前面的例子推测的那样，smb 选项将同时处理 smbd 和 nmbd。如果你想使用基于 Web 的配置，可以打开 swat 选项；如果你仅安装 SWAT 是为了获取额外的文档，也可以将其保持关闭。

![](img/ec2066d370d3af1a767664d36aa7ddfe_530_0.png)

如果你想从命令行设置所有这些，你需要确保在 /etc/rc3.d 和 /etc/rc5.d 目录中有适当的符号链接，指向 /etc/init.d/smb 脚本。有关检查此项以及如果尚未设置符号链接如何设置的详细信息，请参见模块 7。SWAT 通常由 xinetd 启动，因此如果你想启用它，需要编辑 /etc/xinetd.d/swat。SWAT 默认运行在端口 901，因此如果你确实需要出于某种原因更改端口，请查看 /etc/services。

> **注意**
> 如果你对 Samba 的配置进行了更改，你需要停止然后重新启动 Samba，这些更改才能生效。重新建立连接是客户端的责任。这是 SMB 协议的一部分，而不是 Samba 的限制。

### 进度检查

- 1. PAM 是什么？
- 2. smbd 和 nmbd 之间的一个区别是什么？

## 关键技能

### 18.4 使用 SWAT 管理 Samba

在 Samba 2 之前版本中，配置它的官方方法是编辑 smb.conf 文件。尽管该文件性质冗长但易于理解，然而它体积较大且笨拙。这也意味着在 Windows 下设置共享仍然比在 Samba 下设置共享更容易。许多个人开发了用于编辑过程的图形化前端。这些工具中的许多仍在维护和增强中——你可以通过访问 Samba 的网站 http://www.samba.org 阅读更多关于它们的信息。然而，从版本 2 开始，Samba 随附了 Samba Web Administration Tool (SWAT)。

使用 SWAT 非常简便。所有配置都是通过 Web 浏览器完成的。然后 SWAT 从浏览器获取信息并构建 smb.conf 文件。对于习惯编辑配置文件的人来说，这可能有点烦人，因为 SWAT 不会在配置文件本身中保留注释。因此，服务器配置文档必须保持在 Samba 外部，而不是以注释形式嵌入配置文件中。

- 1. PAM（Password Authentication Module，口令认证模块）允许你针对 PDC 验证用户。
- 2. nmbd 处理来自主浏览器、域和 WINS 服务器的名称服务器请求，而 smbd 处理实际的共享文件系统和打印机。

> **注意**
> 如果你更喜欢在配置文件中维护注释，或者如果你需要编写一些自己的工具来自动化某些管理任务，你不应该使用 SWAT。基于文本的配置文件之美就在于此。你拥有选择权：如果你不想使用图形用户界面，就不必使用它；由于文件格式是公开的，任何人都可以编写自己的管理工具，如果他们愿意的话。

### 设置 SWAT

你可以通过浏览器接口使用 SWAT 管理 Samba。它是手动编辑 Samba 配置文件的极佳替代方案，但不要因此认为配置文件很复杂！

使 SWAT 与其他基于浏览器的管理工具略有不同的一点是，它不依赖于 Web 服务器（如 Apache）。相反，SWAT 在不实现完整 Web 服务器的情况下执行所有必要的 Web 服务器功能。这主要是通过 xinetd 守护进程来实现的。

只需将 Web 浏览器指向你的 Samba 服务器端口 901，即可获得进入 SWAT 的登录提示。请注意，默认配置仅允许你从运行 Samba 的同一台机器连接到 SWAT。这是出于安全目的，因为你不希望允许随机人员远程探查你的机器。如果你在服务器上安装了 Web 浏览器，只需将其指向 http://localhost:901/。如果你没有在本机安装 Web 浏览器，那么你需要选择使用不同的管理工具或启用通过网络使用 SWAT。如果你想使用本地 Web 浏览器，但没有在 Samba 服务器上安装 X Window System，你仍然可以使用许多基于文本的 Web 浏览器。

> **警告**
> 通过 SWAT 以 root 身份登录会导致 root 密码从 Web 浏览器发送到 Samba 服务器。因此，避免通过不可信任的网络执行管理任务。最好在服务器本身运行 Web 浏览器，或者在客户端主机和 Samba 服务器主机之间设置 SSH 隧道。

### 从其他主机使用 SWAT

如果你使用了 xinetd，那么你的配置文件中已经内置了 TCP Wrappers 功能。更改 /etc/xinetd.d/swat 中的 only_from 选项将允许你添加其他具有连接能力的主机。有关如何限制哪些主机可以连接到你的服务器的更多信息，请参见模块 8。

### SWAT 菜单

当你连接到 SWAT 并以 root 身份登录时，你将看到如图 18-1 所示的主菜单。从这里，你可以找到 Samba 配置文件、守护进程和相关程序所需的大多数文档。这些链接没有指向外部网站，因此你可以在不联网的情况下随意阅读。你还可以访问 Samba How-To 集合和书籍 *Using Samba*。

窗口顶部包含以下菜单选项的按钮：

| 按钮名称 | 描述 |
| :--- | :--- |
| Home | 主菜单页面 |
| Globals | 影响 Samba 所有操作方面的配置选项 |
| Shares | 用于设置磁盘共享及其相应选项 |
| Printers | 用于设置可供 NT 客户端访问的打印机 |
| Status | smbd 和 nmbd 进程的状态，包括连接到这些进程的所有客户端及其正在执行的操作的列表（与 smbstatus 命令行程序列出的信息相同） |
| View | 生成的 smb.conf 文件 |
| Password | 口令设置 |

![](img/ec2066d370d3af1a767664d36aa7ddfe_533_0.png)

### Globals

Globals 页面列出了影响 Samba 操作所有方面的所有设置。这些设置分为七组：Base、Security、Logging、Tuning、Printing、Browse 和 WINS。每个选项的左侧都有一个链接，指向该设置及其值的相关文档。如果你计划通过 Samba 共享 UNIX 打印机，请确保根据你的情况将打印选项设置为使用 LPRng 或 Common Unix Printing System (CUPS)。

### Shares

在 Windows 下，设置*共享*意味着创建一个新文件夹，右键点击它，并允许其共享。可以通过右键点击文件夹并选择“属性”来建立额外的控制。

使用 SWAT，这些相同操作是通过创建一个新的共享来实现的。然后你可以选择该共享并点击“Choose Share”。这会显示该共享的所有可配置参数。

### Printers

Samba 自动使所有列在你本地打印设置中的打印机——即对于 LPRng 是 /etc/printcap 文件，对于 CUPS 是 /etc/cups/printers.conf（参见模块 19）——可通过 SMB 供 Windows 客户端使用。通过这一系列菜单，你可以修改 Samba 对这些打印机的处理方式，甚至添加额外的打印机。你不能在这里做的是向主系统添加打印机。有关该过程的更多信息，请参见模块 19。

### Status

Status 页面显示 smbd 和 nmbd 守护进程的当前状态，包括有关哪些客户端已连接及其操作的信息。该页面默认每 30 秒自动更新一次，但如果你愿意，可以更改此速率（这是该页面上本身的一个选项）。除了状态信息外，你可以开启和关闭 Samba，或要求它重新加载其配置文件。如果你对配置进行了任何更改，这是必要的。

### View

当你更改 Samba 配置时，SWAT 会跟踪更改并确定它需要放入 smb.conf 文件中的信息。打开 View 页面，你可以看到 SWAT 正在为你组装的文件。

### Password

如果你打算支持加密口令，请使用 Password 页面。你希望为用户提供一种修改他们自己口令的方式，而无需登录到 Linux 服务器。此页面允许用户正是这样做。

