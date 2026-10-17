
Wine 是一个兼容层，允许你在 Linux 上原生运行许多 Windows 应用程序。虽然你可以在上面运行 Windows 操作系统，但不需要实际的操作系统。Windows 应用程序将像 Linux 应用程序一样运行，能够访问 Linux 文件系统并使用连接到 Linux 的设备。严重依赖驱动程序的应用程序（如图形密集型游戏）可能无法运行。其他应用程序，如不依赖任何特殊驱动程序的新阅读器，可能运行得很好。对于某些应用程序，你可能从运行良好的 Windows 系统将特定的 `DLL` 文件复制到你的 Windows `system32` 目录。

![](img/af27012edddcf42a8b40fad81183c10b_122_0.png)

# 第一部分：入门

Wine 对于运行仅为 Windows 编写实用应用程序非常有帮助。安装可能需要你从运行良好的 Windows 操作系统将 `DLL` 文件安装到你的 Wine 模拟器 `system32` 目录。

要安装在 Wine 上，在“添加/删除应用程序”（Pirit）中搜索 `wine`。你会看到列出的多个包。你只需要选择 Wine 包。其他包将由 Yum 作为依赖包被选择，包括 `wine-twine` 和 `wine-tools`。某些包已经包含在 Wine 包中，但作为单独的包呈现，例如 `wine-arts`，以防你不想安装所有内容。

> 提示：在 Linux 上玩游戏，你可以尝试 `cdedega`。这些是廉价的商业驱动程序，配置为支持许多流行游戏，`www.cedega.com`，能够实现完全的图形加速。

安装完成后，应用程序菜单中将出现 Wine 菜单。Wine 菜单包含配置（Configuration）、Wine 安装程序和 Wine 文件浏览器的条目，以及注册表编辑器、记事本和 Wine 帮助。

要设置 Wine，用户启动 Wine 配置工具。这将打开一个包含面板（Panels）、库（Libraries，DLL 选择）、音频（Audio，音频驱动程序）、桌面集成和图形的窗口。在“应用程序”（Applications）窗口上，你可以选择为哪个版本的 Windows 应用程序设计。驱动器（Drives）面板将列出你检测到的分区，作为 Windows 模拟驱动器显示为驱动器 C。C: 盘实际上只是固定大小的分区。你的 Linux 文件系统将列为 Z 盘。

一旦配置完成，Wine 将在用户的家目录下设置一个 `wine` 目录（该目录是隐藏的，因此请在文件浏览器的菜单中启用“显示隐藏文件”以显示它）。在该目录内将有 `drive_c` 目录，它作为 C 盘运行，在 Windows 和 Program File 子目录中存放你的 Windows 系统文件和程序文件。System 和 `System32` 目录位于 Windows 目录。这里就是你放置任何需要的 `DLL` 文件的地方。Program Files 目录将存放你安装的程序，就像它们安装在 Windows Program Files 目录中一样。

要使用 Wine 安装 Windows 应用程序，你可以使用 Wine 配置工具，也可以直接打开终端并运行带有 Windows 作为参数的 `wine` 命令。以下示例显示了流行的新闻 `newsbin` 程序：

```
$ wine newsbin.exe
```

要使用 Windows 配置工具安装，请选择“应用程序”面板然后点击“添加”。

某些应用程序还需要你使用运行良好的 Windows 操作系统中的某些 `DLL` 文件。`DLL` 文件通常被复制到用户的 `/wine/drive_c`。

安装的应用程序图标将出现在你的桌面上。双击图标即可启动。

# 第3章：接口基础：登录，桌面

要在 Linux 系统上设置简单的文件共享，你首先需要配置你的 Samba 服务器。你可以通过直接编辑 `/etc/samba/samba.conf` 文件或通过使用 `system-config-samba` 配置工具（系统 | 管理 | 服务器设置 | Samba）来实现。如果你编辑了 `/etc/samba/samba.conf` 文件，你首先需要指定你的 Windows 网络名称（请参见第 39 章）。

通过选择系统 | 管理 | 服务器设置 | Samba 使用 `open-config-samba-tool`。在首选项（Preferences）菜单下，选择服务器设置。在基本（Basic）面板中，你输入你的 Windows 网络工作组名称。Windows 提供的默认名称是 `MSHOME` 或 `WORKGROUP`。你已经给你的 Windows 网络名称。对于许多网络，你可以决定一个。只需确保所有计算机都使用相同的网络名称。检查你的 Windows 控制面板中的系统应用程序。

要设置简单的共享，点击“添加共享”（Add Share），这将打开“创建共享”窗口。选择要共享的 Linux 目录（点击“浏览”找到它），然后指定它是否可写且可见。在“访问”（Access）面板上，你可以选择向所有人开放，或向特定用户开放。

在“安全”（Security）面板上，你可以选择想要使用的身份验证类型。默认、用户使用共享或服务器安全；这些更多选项，但两者都已弃用，并可能在后续版本中被弃用。对于用户，你必须将 Windows 用户与特定的 Linux 用户关联。在首选项窗口中选择 Samba 用户（Samba Users），然后选择相应的 Windows 用户，并输入该用户访问 Linux 的密码。这是该用户的 Samba 密码。Samba 维护其自己的一套密码，用户访问 Samba 时需要这些密码。当 Windows 用户想要访问 Samba 时，他们将需要他们的 Samba 密码。

要使用新配置重启，请使用“服务”（Services）工具重启 `nmb` 和 `smb`（系统 | 管理 | 服务器设置 | 服务）。确保你系统上的防火墙没有拦截 Samba。

当 Windows 用户想要访问 Linux 系统上的共享时，他们打开“我的位置”（My Places），然后通过“添加网络位置”（Add a network place）为该添加网络位置条目，或者通过“查看”（View group）查看你 Windows 网络上的计算机。选择 Linux Samba 服务器将显示你的 Samba 共享。要访问共享，用户将被要求输入用户名和 Samba 密码。你可以选择记住用户名和密码以实现自动访问。

> `fuse-samb` 工具让你拥有整个 Windows 网络。

# 在 Linux 上运行 Windows 软件：Wine

Wine 是一个兼容层，允许你在 Linux 上原生运行许多 Windows 应用程序。虽然你可以在上面运行 Windows 操作系统，但不需要实际的操作系统。Windows 应用程序将像 Linux 应用程序一样运行，能够访问 Linux 文件系统并使用连接到 Linux 的设备。严重依赖驱动程序的应用程序（如图形密集型游戏）可能无法运行。其他应用程序，如不依赖任何特殊驱动程序的新阅读器，可能运行得很好。对于某些应用程序，你可能从运行良好的 Windows 系统将特定的 `DLL` 文件复制到你的 Windows `system32` 目录。

![](img/af27012edddcf42a8b40fad81183c10b_122_0.png)
