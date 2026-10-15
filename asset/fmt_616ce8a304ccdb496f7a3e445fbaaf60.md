
**Novell NetStorage** 通过允许用户从任何互联网位置安全访问 NetWare 服务器上的文件，解决了其中一些问题；它使用现有的 Web 浏览器或 Microsoft Web Folder 来实现此功能，无需在用户的计算机上下载或安装额外的客户端或小程序。借助 `NetStorage`，用户可以安全地在任何互联网连接设备与 Novell 网络之间复制、移动、重命名、删除、读取和写入文件。`NetStorage` 支持 `HTTP`、`HTTPS`、`HTML`、`XML` 和 `WebDAV` 等互联网标准，使其兼容大多数客户端计算机系统，包括 `Windows`、`Macintosh` 和 `Linux`。此外，`NetStorage` 还包括对 `NetWare WebAccess` 的访问，以便用户可以通过 `NetWare WebAccess` 页面访问网络文件和文件夹（包括其 `iFolder` 目录中的文件）。在以下章节中，你将学习如何设置和使用 `Novell NetStorage`，以便 `UAS` 的用户能够访问和管理网络文件。

### 安装 NetStorage

与 `iFolder` 类似，`Novell NetStorage` 可以在安装 `NetWare 6.5` 时或之后进行安装。Eric 选择在稍后安装 `NetStorage`，以使最初的 `NetWare 6.5` 安装尽可能简单。要安装和使用 `NetStorage`，安装 `NetStorage` 的 `eDirectory` 树中必须至少有一个 `NetWare 6.5` 服务器，并且计算机必须至少安装了 `Netscape 4.7` 或 `Internet Explorer 5.0`。在 `NetStorage` 安装过程中，你会看到图 10-23 中所示的窗口。

![](img/840007e8f98ea6653e5877e945c27dc6_440_0.png)

为了正确安装 `NetStorage`，在开始之前，你应该确保以下信息可用：

- 通常，你只需要在 `eDirectory` 树中的一个 `NetWare 6.5 OES` 服务器上安装 `NetStorage`。在安装 `NetStorage` 之前，你应该确定主要 `NetWare 6.5` 服务器的 IP 地址或 DNS 名称，该服务器必须拥有 `eDirectory` 树的主副本或读写副本。`NetStorage` 不需要安装在主要服务器上，但你需要在 `NetStorage` 安装期间识别该服务器。当用户尝试登录 `NetStorage` 时，主要服务器发挥作用。在登录期间，`NetStorage` 在主要服务器上搜索 `eDirectory` 以定位用户名和密码。当 `NetStorage` 在 `eDirectory` 数据库中找到用户时，它会向 `eDirectory` 验证该用户。
- 确定将使用 `NetStorage` 的用户的 `eDirectory` 上下文。`NetStorage` 会在 `NetStorage` 安装期间指定的上下文中搜索用户帐户。上下文通过在主服务器的 IP 地址或 DNS 名称后插入冒号，然后输入容器的可区分名称来表示。例如，为了搜索 `UAS` 组织中的用户，Eric 输入了 `\172.20.0.65:UAS`。
- 除了主要上下文外，`NetStorage` 安装窗口还包含两个更多字段，你可以在其中指定 `NetStorage` 服务将支持的额外 `eDirectory` 树的主服务器和 `eDirectory` 上下文。
- `NetStorage` 安装窗口中的最后一个字段是你指定 `iFolder` 服务器 IP 地址或 DNS 名称的地方。为了让用户通过 `NetStorage` 访问其 `iFolder` 文件，你必须指定 `iFolder` 服务器。

在下面的活动中，你将学习如何通过使用服务器的图形控制台在 `NetWare 6.5 OES` 服务器上安装 `NetStorage`。此活动需要访问专用的 `NetWare 6.5` 服务器。如果你使用的是共享教室服务器，你的讲师可能会将此活动作为课堂演示来执行。

#### 活动 10-6：安装 NetStorage

**所需时间：** 15 分钟

**目标：** 在 `NetWare 6.5 OES` 服务器上安装 `NetStorage`。

**需求：** 访问专用的 `NetWare 6.5 OES` 服务器和产品 CD 2

**描述：** `iFolder` 在许多 `UAS` 用户中运行良好，但有些人希望在旅途中更轻松地访问其文件。为了允许 `UAS` 用户通过 Web 浏览器远程访问其驱动器映射和 `iFolder` 文件，Luke McMann 希望评估使用 `NetStorage`。在确定 `UASHOST` 服务器为主要 `NetStorage` 服务器并获取其 IP 地址和 DNS 名称后，Eric 希望你在 `NetWare 6.5` 服务器上使用图形控制台安装 `NetStorage`。在此活动中，你安装 `NetStorage`，以便你可以评估其使用。

> 由于安装 `NetStorage` 需要关闭服务器并重新启动，请选择一个服务器不需要的安装时间。

1. 在 `Novell X Server – 图形控制台` 上，点击 **Novell** 按钮，然后点击 **Install** 以显示已安装产品窗口。
2. 点击 **Add** 按钮以显示源路径窗口，点击 **browse** 按钮导航到产品 CD 2 (`NW65PROD`)，点击 **Postinst.ni** 文件，然后点击 **OK**。安装文件将被复制到服务器上。
3. 再次点击 **OK** 以显示组件窗口，其中列出了默认安装的组件。点击 **Clear All** 按钮以防止重新安装现有组件。
4. 点击 **Novell NetStorage** 复选框，点击 **Next**，然后点击 **Copy files**。
5. 使用你的管理员用户名和密码登录网络以显示 `NetStorage` 安装窗口，然后点击 **OK**。
6. 如有必要，在“主要 `eDirectory` 服务器和上下文的 DNS 名称或 IP 地址”文本框中以及“`iFolder` 服务器的 DNS 名称或 IP 地址”文本框中，输入 `UASHOST` 服务器的 IP 地址和 `UAS` 上下文。（参考图 10-23 查看示例。）验证端口 80 已输入到 `iFolder` 端口文本框中，然后点击 **Next** 以显示安装摘要窗口。
7. 当显示安装完成消息框时，点击 **RESTART SERVER** 按钮。

### 配置 NetStorage

虽然使用 `NetStorage` 所需的信息在安装期间提供，但有时你需要修改配置或查看 `NetStorage` 服务的状态。你可以通过点击文件访问 (`NetStorage`) 标题，然后点击图 10-24 中所示的选项之一，使用 `iManager` 来配置和监控 `NetStorage` 操作。表 10-1 更详细地描述了这些选项。

![](img/840007e8f98ea6653e5877e945c27dc6_442_0.png)

| NetStorage | 配置选项 | 描述 |
| :--- | :--- | :--- |
| 身份验证域 | 查看或修改身份验证域和上下文。身份验证域由 `eDirectory` 服务器托管，包含 `NetStorage` 用于在 `eDirectory` 树中查找用户的一个或多个上下文。你可以使用此选项将服务器添加到 `NetStorage`，或在域服务器中添加、优先或移除搜索上下文。 |
| 当前会话 | 查看当前的 `NetStorage` 用户。 |
| 文件 | 访问 `iFolder` 文件。 |
| iFolder 存储提供程序 | 查看和更改基本的 `iFolder` 参数，如 `iFolder` 服务器和安全端口。 |
| NetWare 存储提供程序 | 查看和更改用于使用 `NetStorage` 的 `NetWare` 映射驱动器的参数。 |
| NetStorage 选项 | 查看 `NetStorage` 选项，如会话超时、LDAP 端口和证书名称。在大多数情况下，你不应该更改这些参数。 |
| NetStorage 统计信息 | 查看 `NetStorage` 使用统计信息，如服务器运行时间、最大会话数、登录失败次数和处理的总请求数。 |
| 资源使用情况 | 查看系统使用的资源，包括内存、锁和线程。 |
| WebDAV 提供程序 | 查看关于计算机上 `WebDAV` 提供程序的注册表信息。 |

#### 表 10-1 NetStorage 配置选项（续）

| NetStorage 配置选项 | 描述 |
| :--- | :--- |
| 新存储位置、编辑存储位置和删除存储位置 | 使用这些选项从 `eDirectory` 树中创建、编辑和删除存储位置。存储位置对象可用作指向 `NetWare` 目录的指针，这使用户更容易找到和访问 `NetStorage` 中的目录。 |
| 将存储位置分配给对象 | 将存储位置分配给用户、组或配置文件。 |
