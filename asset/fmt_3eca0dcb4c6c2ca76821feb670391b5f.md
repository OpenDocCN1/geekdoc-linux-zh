
当用户需要访问多台计算机上的文件，或希望从离线笔记本电脑访问文件时，`iFolder` 客户端可能很有用。然而，`iFolder` 客户端需要 `Novell Client`，这在某些计算机或 Linux 环境中可能不可用。此外，在用户不经常访问的远程计算机上安装 `iFolder` 客户端并放置 `iFolder` 目录并不实际。例如，David Heise 在访问客户地点时需要访问某些文档，但他不希望在这些地点的计算机上安装 `iFolder` 客户端和主目录图标，因为他下次访问时可能不使用同一台计算机。为了解决这个问题，Eric 培训 UAS 用户通过 `NetStorage` 访问 `iFolder` 文件。在下面的活动中，你将学习如何使用 Web 浏览器访问存储在 `iFolder` 中的文件。

### 活动 10-9：通过 Web 浏览器访问 iFolder

**所需时间：** 10 分钟

**目标：** 通过 Web 浏览器访问 `iFolder` 文件。

**需求：** 完成活动 10-5，以及在 Windows XP 计算机上具备 Internet Explorer 或在 SUSE Linux 10 计算机上具备启用 Java 的 Firefox。

**描述：** 在培训 UAS 用户之前，Eric 希望你使用 Web 浏览器测试访问其 `iFolder` 文件。在此活动中，你将仅使用 `iFolder` applet 下载和上传你的 `iFolder` 文件。

1. 如有必要，启动计算机并登录到本地系统。为了模拟从未安装 `Novell Client` 的计算机访问 `iFolder` 文件，请登录到你的本地计算机系统。如果你使用的是 Windows XP，请单击选中 `Workstation Only` 复选框，然后输入你的本地用户名和密码。
2. 如有必要，单击 `Cancel` 以关闭 `iFolder` 登录窗口。
3. 启动 Web 浏览器，输入网址：`https://IPaddress/iFolder`（将 `IPaddress` 替换为分配给你的 `iFolder` 服务器的 IP 地址），然后按 `Enter`（回车）键。（使用 `"https"` 通过安全端口加密数据传输，从而增加安全性。）
4. 在 `Access your Files`（访问你的文件）标题下点击 `Login`（登录）选项，如有必要，点击 `Yes`（是）以继续处理安全证书。如果被要求，请输入 Eric 用于加密的口令。
5. 输入 Eric 的用户名和密码，然后点击 `OK`（确定）登录并显示 `NetStorage` 窗口。
6. 点击 `iFolder` 目录以将其展开，并记录文件名：
7. 点击选中你在活动 10-8 中复制的文件对应的复选框。
8. 点击 `File`（文件）链接，然后点击 `Download`（下载），将该文件下载到你的桌面。
9. 最小化你的 Web 浏览器。
10. 启动一个文本编辑器，例如 WordPad，并打开你在步骤 8 中复制到桌面的文件。添加以下一行文本：

    `mm/dd/yy Room 129.00`
11. 将文件另存为新名称，并退出文本编辑器。
12. 按照以下步骤上传更新后的文件：
    a. 最大化你的 Web 浏览器。
    b. 点击 `iFolder` 目录，点击 `File`（文件）链接，然后点击 `Upload`（上传）按钮以打开 Novell 上传文件对话框。
    c. 点击 `browse`（浏览）按钮选择你在步骤 11 中保存的文件，然后点击 `Upload`（上传）以开始上传过程。新文件随后应出现在你的 `iFolder` 目录中。
13. 点击 `Logout`（注销）选项结束会话，并关闭你的 Web 浏览器。
14. 按照以下步骤使用你的 Windows 系统访问你的 `iFolder` 数据：
    a. 如有必要，启动 Windows 并使用 `Ekenton` 用户名和密码登录目录。
    b. 以 `Ekenton` 身份登录 `iFolder`。双击他的 `iFolder` 主目录，并打开你在步骤 12 中上传的文件。
15. 关闭任何打开的窗口，并注销。让系统保持运行状态，以用于下一个活动。

![](img/840007e8f98ea6653e5877e945c27dc6_447_0.png)

### 安装和使用 NETDRIVE

虽然 `NetStorage` 允许用户从任何客户端查看、上传和下载他们的 `iFolder` 和网络数据，但它并不提供通过标准驱动器映射从应用程序直接访问数据的功能。Novell 已提供通过 `NetDrive` 使用 HTTP 创建网络驱动器映射的方法。使用 `NetDrive`，你可以将网络驱动器映射到任何 NetWare 6.5 OES 服务器，而无需使用 Novell 客户端。此外，由于 `NetDrive` 使用 HTTP，你可以从联网的系统中映射该驱动器。与 `NetStorage` 相比，使用 `NetDrive` 的主要缺点是需要在本地计算机上安装一个小客户端。如果你在无法安装 `NetDrive` 客户端的计算机上工作，例如在机场亭或酒店房间，你仍可使用 `NetStorage` 在线访问你的文件。在以下章节中，你将学习如何安装和使用 `NetDrive` 从 Web 浏览器创建驱动器映射。

#### NetDrive 先决条件

`NetDrive` 可在任何 Windows 系统上运行，包括 Windows 95 版本。此外，安装和运行 `NetDrive` 客户端仅需 2 MB 的硬盘空间。`NetDrive` 支持以下访问网络文件的方法：

- `WebDAV`——`NetDrive` 与 `NetStorage` 集成，提供具有最小客户端要求的全面文件访问解决方案。在使用 `WebDAV` 和 `NetDrive` 之前，必须安装并配置 `NetStorage`。
- `FTP`——`NetDrive` 可以使用标准 `FTP` 访问网络文件。要使用此选项，必须在 NetWare 服务器上安装并配置 `FTP`。（有关设置 `FTP` 服务器的信息，请参见第 11 章。）
- `iFolder`——在网络中安装并配置 `iFolder` 后，`NetDrive` 可以访问用户 `iFolder` 目录中的文件。

在使用 `NetDrive` 之前，你需要安装 `NetDrive` 客户端，然后添加一个或多个使用 `WebDAV`、`FTP` 或 `iFolder` 来映射网络驱动器的 `NetDrive` 站点。在以下章节中，你将学习如何安装 `NetDrive` 客户端，然后使用它创建新站点并映射网络驱动器。

![](img/840007e8f98ea6653e5877e945c27dc6_448_0.png)

`NetDrive` 客户端位于 `SYS\Apache2\iFolder\Server\NetDrive`。你可能希望将此文件复制到 `SYS\Public` 文件夹，以便所有用户都可以使用它。

#### 安装 NetDrive 客户端

你可以通过以下步骤从 NetWare 6.5 服务器安装 `NetDrive` 客户端：

![](img/840007e8f98ea6653e5877e945c27dc6_448_1.png)

1. 使用你的管理员用户名和密码登录 `e:\directory`，并切换到 `Apache2\iFolder\Server\Netdrive` 目录。
2. 双击 `Netdrive.exe` 文件开始安装 `NetDrive` 客户端。
3. 选择语言，并点击“确定”。
4. 在欢迎窗口中点击“下一步”并接受许可协议。
5. 在目标位置窗口中，你可以指定安装客户端的目录，然后点击“下一步”安装客户端并完成安装。
6. 重启 Windows 系统。

#### 向 NetDrive 添加站点

安装 `NetDrive` 客户端并重启系统后，你将在 Windows 任务栏中看到一个 `NetDrive` 图标。你可以使用此图标打开 `NetDrive` 配置对话框（见图 10-27）。要添加一个新站点，你可以使用以下步骤：

![](img/840007e8f98ea6653e5877e945c27dc6_448_2.png)

1. 点击“新建站点”`New Site` 按钮并为新站点输入名称。
2. 在站点地址、URL 文本框中输入 `https://Address`（将 `Address` 替换为 `NetStorage` 服务器的 IP 地址）。
3. 将服务器类型设置更改为 `WebDAV`，并选择一个驱动器号。
4. 点击以清除“匿名/公共登录”`Anonymous/Public Logon` 复选框，并在用户名和密码文本框中输入有效的用户名和密码，如图 10-27 所示。
5. 点击“连接”`Connect` 按钮，将所选驱动器映射到 `NetStorage` 服务器。

![](img/840007e8f98ea6653e5877e945c27dc6_449_0.png)

#### 使用虚拟办公室
