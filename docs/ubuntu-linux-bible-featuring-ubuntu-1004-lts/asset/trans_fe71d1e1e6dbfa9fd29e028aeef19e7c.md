

# 第二部分：面向桌面用户的 Ubuntu

能够连接到远程系统的图形化控制台可以简化系统管理和问题解决，如果你的孩子不知道你正在连接到他们的电脑，这通常会让他们感到困惑和惊奇。图 25-7 显示了到远程 Mac OS X 的 VNC 连接。

# 图 25-7

# 连接到 Mac OS X 系统的 VNC 连接

![](img/1a233c34336fbf5a85d6eb785e401709_955_0.png)

图 25-8 显示了使用远程桌面查看器连接到远程 Microsoft Windows 2000 系统的 VNC 连接。

# 第 25 章：连接到其他系统

图 25-8
连接到 Windows XP 系统的 VNC 连接

![](img/1a233c34336fbf5a85d6eb785e401709_956_0.png)

# 连接到远程 Windows 终端服务器

对于大多数人来说，需要与运行 Microsoft Windows 的系统交互是企业生活、偶尔是个人生活的常态。在家庭网络环境中，大多数 Windows 连接可以使用本章之前讨论的 VNC 服务器和客户端很好地处理，但如果你需要连接到工作中的远程 Windows 系统，或者你的家庭计算预算比我的要高一些，你可能需要访问运行 Windows 终端服务器（Windows Terminal Server）的系统。

如果你需要为用户提供偶尔的个人 Windows 系统访问权限，但希望减少成本和管理麻烦，而不是为每个用户安装一台机器，一个很好的解决方案是在足够健壮的 Windows 系统上安装 Windows Terminal Services，并购买一小池客户端许可（Client Licenses），根据需要由服务器分发。远程客户端可以连接到终端服务服务器，并在桌面的窗口中运行虚拟的 Windows 会话。然后你可以在终端服务器上或在用户配置文件定义的共享中安装人们需要使用的软件，任何连接到服务器的远程用户都可以访问并运行所需的软件。幸运的是，远程访问 Windows 终端服务甚至不需要 Windows 系统。Ubuntu 可以使用 `rdesktop` 或终端服务器客户端 (`tclient`) 轻松访问 Windows 终端服务，这是两个 Windows 终端服务使用的远程桌面协议（RDP）的开源软件软件包。

# 提示

如果你通过在 Microsoft Windows 域控制器或服务器上运行 Terminal Services 来自定义 Windows 服务，你需要确保想要拥有“本地登录”（Log Locally）用户权限的用户属于具有该权限的组。否则，用户将收到消息：“此系统的本地策略不允许你进行交互式登录”，而你可能仍然需要每个人准备一台 Windows 机器。

# 使用 rdesktop 连接终端服务器

`rdesktop` 软件包 (www.rdesktop.org) 是适用于 Linux 和大多数其他 UNIX 及类 UNIX 系统（如 Window System）的远程桌面软件包。Ubuntu Linux 系统上默认安装了 `rdesktop` 软件包，并提供了一个极佳、强大的客户端，在本节中包含了一些非常酷的功能。`rdesktop` 软件包可以在标准的 Ubuntu 存储库获取，但你始终可以从其 SourceForge (http://sourceforge.net/projects/rdesktop) 获取最新版本的源码和适用于其他类型系统的安装包。

你必须从 GNOME 或 xterm 启动 `rdesktop`，尽管你完全像第 5 章解释的那样将其添加到菜单中。连接运行 Windows Terminal Services 的远程系统的最简单 `rdesktop` 命令行是 `rdesktop host`，其中 `host` 是运行 Windows Terminal Services 的系统名称或 IP 地址。桌面上会显示一个窗口，显示托管 Windows Terminal Services 的 Windows 版本的标准 Windows 登录界面，如图 25-9 所示。

指定要登录的域（如有必要）并登录后，你的 `rdesktop` 窗口将显示你所连接的 Windows 版本的标准 Windows 桌面，如图 25-10 所示。

# 图 25-9

rdesktop 中的 Windows Terminal Services 登录提示

rdesktop 为你提供了多个可以简化访问 Windows Terminal Services 的选项。我最喜欢的包括几个：

- -d：你想要验证的域
- f：全屏模式。这将在无装饰的窗口中显示 rdesktop 并占据你的桌面。你可以通过按下 Ctrl+Alt+Enter 切换装饰（从而切换窗口控制控件）。
- p：你在远程域中的密码
- u：你想要登录的用户名

# 第二部分：面向桌面用户的 Ubuntu

rdesktop 中的 Windows 2008 Server 桌面

![](img/1a233c34336fbf5a85d6eb785e401709_959_0.png)

如果运行 Windows Terminal Services 的系统运行 Windows XP 或更高版本的 Windows，一个特别方便且在本节未列出的选项是 `-r`，它允许将本地资源映射到你的 Windows 系统。这当你需要从屏幕较小的系统连接到终端服务器时特别有用。

rdesktop 应用程序提供了几个可以简化访问 Windows Terminal Services 的选项。我最喜欢的包括几个：

- -d：你想要验证的域
- f：全屏模式。这将在无装饰的窗口中显示 rdesktop 并占据你的桌面。你可以通过按下 Ctrl+Alt+Enter 切换装饰（从而切换窗口控制控件）。
- p：你在远程域中的密码
- u：你想要登录的用户名

# 使用 rdesktop 连接终端服务器

`rdesktop` 软件包 (www.rdesktop.org) 是适用于 Linux 和大多数其他 UNIX 及类 UNIX 系统（如 Window System）的远程桌面软件包。Ubuntu Linux 系统上默认安装了 `rdesktop` 软件包，并提供了一个极佳、强大的客户端，在本节中包含了一些酷的功能。`rdesktop` 软件包可以在标准的 Ubuntu 存储库获取，但你始终可以从其 SourceForge (http://sourceforge.net/projects/rdesktop 获取最新版本的源码和适用于其他类型系统的安装包。

你必须从 GNOME 或 xterm 启动 `rdesktop`，尽管你完全像第 5 章解释的那样将其添加到菜单中。连接运行 Windows Terminal Services 的远程系统的最简单 `rdesktop` 命令行是 `rdesktop host`，其中 `host` 是运行 Windows Terminal Services 的系统名称或 IP 地址。桌面上会显示一个窗口，显示托管 Windows Terminal Services 的 Windows 版本的标准 Windows 登录界面，如图 25-9 所示。

指定要登录的域（如有必要）并登录后，你的 `rdesktop` 窗口将显示你所连接的 Windows 版本的标准 Windows 桌面，如图 25-10 所示。

# 图 25-9

rdesktop 中的 Windows Terminal Services 登录提示

![](img/1a233c34336fbf5a85d6eb785e401709_958_0.png)

rdesktop 应用程序提供了几个可以简化访问 Windows Terminal Services 的选项。我最喜欢的包括几个：

- -d：你想要验证的域
- f：全屏模式。这将在无装饰的窗口中显示 rdesktop 并占据你的桌面。你可以通过按下 Ctrl+Alt+Enter 切换装饰（从而切换窗口控制控件）。
- p：你在远程域中的密码
- u：你想要登录的用户名

# 第二部分：面向桌面用户的 Ubuntu

rdesktop 中的 Windows 2008 Server 桌面 

![](img/1a233c34336fbf5a85d6eb785e401709_959_0.png)

如果运行 Windows Terminal Services 的系统运行 Windows XP 或更高版本的 Windows，一个特别方便且在本节未列出的选项是 `-r`，它允许将本地资源映射到你的 Windows 系统。这当你需要从屏幕较小的系统连接到终端服务器时特别有用。

# 使用 rdesktop 连接终端服务器

`rdesktop` 软件包 (www.rdesktop.org) 是适用于 Linux 和大多数其他 UNIX 及类 UNIX 系统（如 Window System）的远程桌面软件包。Ubuntu Linux 系统上默认安装了 `rdesktop` 软件包，并提供了一个极佳、强大的客户端，在本节中包含了一些非常酷的功能。`rdesktop` 软件包可以在标准的 Ubuntu 存储库获取，但你始终可以从其 SourceForge (http://sourceforge.net/projects/rdesktop 获取最新版本的源码和适用于其他类型系统的安装包。

你必须从 GNOME 或 xterm 启动 `rdesktop`，尽管你完全像第 5 章解释的那样将其添加到菜单中。连接运行 Windows Terminal Services 的远程系统的最简单 `rdesktop` 命令行是 `rdesktop host`，其中 `host` 是运行 Windows Terminal Services 的系统名称或 IP 地址。桌面上会显示一个窗口，显示托管 Windows Terminal Services 的 Windows 版本的标准 Windows 登录界面，如图 25-9 所示。

指定要登录的域（如有必要）并登录后，你的 `rdesktop` 窗口将显示你所连接的 Windows 版本的标准 Windows 桌面，如图 25-10 所示。

# 图 25-9

rdesktop 中的 Windows Terminal Services 登录提示

![](img/1a233c34336fbf5a85d6eb785e401709_958_0.png)

rdesktop 应用程序提供了几个可以简化访问 Windows Terminal Services 的选项。我最喜欢的包括几个：

- -d：你想要验证的域
- f：全屏模式。这将在无装饰的窗口中显示 rdesktop 并占据你的桌面。你可以通过按下 Ctrl+Alt+Enter 切换装饰（从而切换窗口控制控件）。
- p：你在远程域中的密码
- u：你想要登录的用户名

# 第二部分：面向桌面用户的 Ubuntu

rdesktop 中的 Windows 2008 Server 桌面 

![](img/1a233c34336fbf5a85d6eb785e401709_959_0.png)

如果运行 Windows Terminal Services 的系统运行 Windows XP 或更高版本的 Windows，一个特别方便且在本节未列出的选项是 `-r`，它允许将本地资源映射到你的 Windows 系统。这当你需要从屏幕较小的系统连接到终端服务器时特别有用。

# 使用 rdesktop 连接终端服务器

`rdesktop` 软件包 (www.rdesktop.org) 是适用于 Linux 和大多数其他 UNIX 及类 UNIX 系统（如 Window System）的远程桌面软件包。Ubuntu Linux 系统上默认安装了 `rdesktop` 软件包，并提供了一个极佳、强大的客户端，在本节中包含了一些非常酷的功能。`rdesktop` 软件包可以在标准的 Ubuntu 存储库获取，但你始终可以从其 SourceForge (http://sourceforge.net/projects/rdesktop 获取最新版本的源码和适用于其他类型系统的安装包。

你必须从 GNOME 或 xterm 启动 `rdesktop`，尽管你完全像第 5 章解释的那样将其添加到菜单中。连接运行 Windows Terminal Services 的远程系统的最简单 `rdesktop` 命令行是 `rdesktop host`，其中 `host` 是运行 Windows Terminal Services 的系统名称或 IP 地址。桌面上会显示一个窗口，显示托管 Windows Terminal Services 的 Windows 版本的标准 Windows 登录界面，如图 25-9 所示。

指定要登录的域（如有必要）并登录后，你的 `rdesktop` 窗口将显示你所连接的 Windows 版本的标准 Windows 桌面，如图 25-10 所示。

# 图 25-9

rdesktop 中的 Windows Terminal Services 登录提示

![](img/1a233c34336fbf5a85d6eb785e401709_958_0.png)

rdesktop 应用程序提供了几个可以简化访问 Windows Terminal Services 的选项。我最喜欢的包括几个：

- -d：你想要验证的域
- f：全屏模式。这将在无装饰的窗口中显示 rdesktop 并占据你的桌面。你可以通过按下 Ctrl+Alt+Enter 切换装饰（从而切换窗口控制控件）。
- p：你在远程域中的密码
- u：你想要登录的用户名

