

![](img/840007e8f98ea6653e5877e945c27dc6_611_0.png)

图 B-4 Mozilla Firefox 窗口

![](img/840007e8f98ea6653e5877e945c27dc6_611_1.png)

图 B-5 关于由未知机构认证的网站的提示

![](img/840007e8f98ea6653e5877e945c27dc6_611_2.png)

图 B-6 域名不匹配消息框

尽管大多数步骤在 Firefox 和 Internet Explorer 中的操作相同，但 Firefox 不能直接从远程管理器（Remote Manager）打开文件。例如，在第 3 章的活动 3-2 中，你将无法按照步骤 9b 的描述查看 Hosts 文件。要在 Firefox 中查看 Hosts 文件，你需要执行以下步骤以替代步骤 9a 和 9b：

- a. 点击 ETC 目录以显示其内容。
- b. 点击 hosts 文件，然后点击确定将其保存到用户主目录。

![](img/840007e8f98ea6653e5877e945c27dc6_611_3.png)

- c. 打开终端窗口。
- d. 输入 `cat hosts` 命令以查看 hosts 文件的内容。

## 使用 SUSE Linux 执行最终用户任务

为了提高工作效率，Linux 系统用户需要访问许多与本书中讨论相同的网络资源和服务。在本节中，你将学习如何通过 iFolder Linux 客户端让 Linux 用户访问 iFolder 数据。

### 在 Linux 上安装 iFolder 客户端

在第 9 章中，你学习了如何在 NetWare 服务器上安装 iFolder，并在 Windows XP 上设置 iFolder 客户端。在本节中，你将学习如何在 Linux 服务器上设置 iFolder 客户端，然后从 Linux 和 Windows 平台访问 iFolder 文件。

### 下载 iFolder Linux 客户端

请按照以下步骤在你的 Linux 计算机上安装 iFolder 客户端：

1. 按照第 9 章中的说明在你的 Novell OES 服务器上安装 iFolder。
2. 使用 root 用户名和密码登录到你的 Linux 客户端。
3. 在你的 Linux 计算机上，启动 Firefox Web 浏览器并输入网址 `https://IPaddress/iFolder`（将 `IPaddress` 替换为运行 iFolder 的服务器的 IP 地址或 DNS 名称）以显示 iFolder 主页。
4. 点击“下载 Linux 客户端”链接以显示图 B-7 中所示的窗口，询问你想对该文件做什么。

![](img/840007e8f98ea6653e5877e945c27dc6_612_0.png)

图 B-7 下载 iFolder Linux 客户端

5. 验证“保存到磁盘”选项按钮已选中，然后点击确定将 .rpm 文件保存到 root 用户的主目录。

### 安装 iFolder 客户端

在 iFolder 客户端的 .rpm 文件下载完成后，你可以使用 RedHat 包管理器（RPM）通过以下步骤安装 iFolder 客户端：

1. 打开一个终端会话。
2. 如果你不是以 root 用户身份登录，请使用 `su` 命令并输入 root 用户密码以切换到 root 用户。
3. 在 /root 目录中，输入 ls 并按 Enter 以显示 Novell iFolder 客户端文件的完整名称。

![](img/840007e8f98ea6653e5877e945c27dc6_613_0.png)

输入文件名的一部分后按 Tab 键可以完成输入。例如，输入 "novell-ifolder" 并按 Tab 键将 .rpm 文件的完整名称放置在命令行中。

4. 接下来，输入 `rpm -i filename.rpm -h -v` 并按 Enter。-i 选项用于执行新安装，-h 选项显示进度条，-v（表示“详细”模式）选项显示较长的消息。
5. 安装完成后，输入 exit 并按 Enter 以结束终端会话。
6. 在你的 Linux 计算机上创建一个名为 ekenton 的新本地用户。
7. 注销。

### 从 Linux 使用 iFolder 客户端

要使用 iFolder 客户端，iFolder 服务器上的用户账户必须已启用 iFolder 访问权限，如第 9 章所述。然后你可以执行以下步骤在该 Linux 系统上为该用户设置 iFolder：

![](img/840007e8f98ea6653e5877e945c27dc6_613_1.png)

1. 作为 ekenton 用户登录。
2. 按照以下步骤使用 Konqueror 运行 iFolder 应用程序：
    - a. 启动 Konqueror。
    - b. 输入一个斜杠 (/) 以打开根目录。
    - c. 浏览到 opt/novell/ifolder/bin 目录。
    - d. 点击 novell-ifolder-client 文件以打开它并显示 Novell iFolder 登录对话框（见图 B-8）。

![](img/840007e8f98ea6653e5877e945c27dc6_613_2.png)

图 B-8 Novell iFolder 登录对话框

    - e. 输入在 iFolder 服务器上使用的 ekenton 用户名和密码。
    - f. 在“服务器”文本框中输入 iFolder 服务器的 IP 地址或 DNS 名称。
    - g. 验证“在桌面上放置 iFolder 快捷方式”复选框已选中，然后点击登录以显示图 B-9 中所示的 Novell iFolder 位置对话框。
    - h. 点击确定接受默认设置并显示加密对话框。
    - i. 验证“加密文件”复选框已选中，然后点击确定以显示 Novell iFolder 获取口令短语对话框（见图 B-10）。
    - j. 输入一个你可以记住的口令短语以及一个以防忘记的提示。
    - k. 点击选中“记住口令短语”复选框，然后连续点击两次确定以完成 iFolder 设置。
    - l. 关闭 Konqueror 窗口。ekenton 的 iFolder 图标随后应出现在桌面上。

![](img/840007e8f98ea6653e5877e945c27dc6_614_0.png)

图 B-9 选择 iFolder 位置

![](img/840007e8f98ea6653e5877e945c27dc6_614_1.png)

图 B-10 输入 iFolder 的口令短语

3. 点击 ekenton 的 iFolder 图标以显示其 iFolder 的内容。如果你在 chapter 9 中放置了一些文件在那里，它们应该会被显示出来。
4. 关闭 iFolder 窗口并注销。
5. 如果你在 Windows XP 计算机上运行 iFolder，尝试通过从 Windows XP 将一些文件放入 iFolder 来试验 iFolder。
6. 再次作为 ekenton 登录。
7. 点击 KDE 桌面右下角的 iFolder 图标以显示图 B-11 中所示的 Novell iFolder 窗口。点击“同步”按钮以同步你的 iFolder 文件。
8. 查看“账户信息”和“偏好设置”选项卡中的信息。
9. 关闭 Novell iFolder 窗口。
10. 点击桌面上的 ekenton iFolder 图标以访问 iFolder 文件。
11. 你从 Windows XP 放入 iFolder 的文件现在应该出现在 Linux iFolder 中。
12. 关闭所有窗口并注销。

![](img/840007e8f98ea6653e5877e945c27dc6_615_0.png)

图 B-11 在 iFolder 中同步文件

## Novell Linux 客户端概览

Novell 开放企业服务器的主要组件之一是它能够通过使用 Linux 服务器和计算机来支持开源软件。为了允许网络管理员快速轻松地将 Linux 桌面环境集成到现有的 NetWare 网络中，Novell 发布了 Novell Linux 客户端，它具有以下功能：

- 从 GUI 界面和服务器控制台进行网络登录
- 支持容器配置文件、配置文件和用户登录脚本
- 从 GUI 界面和服务器控制台访问映射驱动器盘和主目录
- 后台身份验证和通用密码身份验证
- GUI 和命令行工具
- 支持 NetWare 核心协议
- 通过 DNS、DHCP、服务定位协议（SLP）和 NMAP 进行名称解析
- 能够执行文件操作，如查看和管理文件受托权限、查看文件属性，以及执行清除和抢救操作
- 若干命令行实用工具，如 MAP、CX、RIGHTS 和 FLAG
- 分布式文件系统联接支持
- eDirectory 多树支持

尽管登录脚本最初是为 Novell Windows 客户端创建的，但 Novell Linux 客户端可以利用登录脚本中可用的大多数功能。因此，你为 Windows 计算机创建的登录脚本也可以用于 Linux 计算机而无需修改，并且你只需要管理一套登录脚本。

截至本文撰写时，Novell Linux 客户端仍处于测试版，并且即将正式发布。目前，Novell 计划将 Novell Linux 客户端与 Novell Linux 桌面一起包含在内。有关更多信息和具体安装说明，请访问 www.novell.com/documentation/linux_client。

