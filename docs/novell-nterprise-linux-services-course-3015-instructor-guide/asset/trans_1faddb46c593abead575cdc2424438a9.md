

## 目标 2 配置 iFolder（续）

1. 对于自动同步，选择**强制**。
2. 对于保存口令，选择**隐藏**。
3. 对于同步到服务器延迟，输入**30**；然后选择**强制**。
4. 对于 iFolder 位置，选择**隐藏**。
5. 选择**更新**。
6. 返回到*终端会话*；然后输入 `tail index.html`。
   注意捕获到的调试输出。随时返回并刷新此窗口，以查看当发生 iFolder 事件时（即，注销和重新登录，同步文件等）记录了哪些类型的信息。
7. （可选）在文件管理器 - 超级用户会话中，你可以浏览到 index.html 文件并双击它以查看其完整内容，并在需要时刷新它。
8. 测试 iFolder 用户的新配置：
   - a. 从你的 Windows 工作站，通过执行以下操作之一注销 iFolder 客户端：
     - 如果你的 iFolder 客户端对话框是打开的，选择**文件** > **注销**。
     - 如果你的 iFolder 客户端对话框是关闭的，右键单击系统托盘中的 iFolder 客户端图标；然后选择**注销**。
   - b. 通过右键单击系统托盘中的 *iFolder 图标* 来登录你的 iFolder 用户；然后选择**登录**。
   - c. 对于你更改了设置的 iFolder 用户，输入*用户 ID* 和密码 **novell**；然后从下拉列表中选择你的服务器 DNS 名称。
   - d. 选择**登录**。
   - e. 对于口令，输入 **novell**；然后选择**确定**。
   - f. 右键单击 iFolder 客户端图标；然后选择**账户信息**。

   选择**账户信息**选项卡。
   注意以下内容：
   - iFolder 用户在服务器上的总空间已增加到 250 MB。
   - iFolder 位置仍然显示。这是因为隐藏位置策略只能应用于新账户（在策略配置页面上有一个注释）。

   选择**偏好**选项卡。
   注意以下内容：
   - 自动同步是灰色的，因为它是强制的，并且不能取消选择。
   - 同步到服务器延迟设置为 30 秒（默认为 5 秒，且也是灰色的）并且无法更改。
   - 记住口令选项是隐藏的。

   选择**文件 > 注销** 以注销 iFolder 用户。
   如果你有足够的时间，请尝试为其他 2 名员工启用、激活和同步文件。
   你也可以尝试从客户端或 iFolder 管理控制台更改其他 iFolder 配置进行实验。

   **关闭 Mozilla 浏览器、终端会话以及任何其他打开的窗口。**

（练习结束）

## 目标 3 描述 Samba 的目的和架构

Samba 是一个软件包，它在 Linux 上实现了 Microsoft 的 SMB/CIFS 网络协议。

它允许 Linux 计算机充当与 Windows 兼容的文件服务器，并作为客户端访问其他 Windows 服务器。

为了描述 Samba 的目的和架构，你需要了解以下内容：

- 什么是服务器消息块（SMB）
- 什么是通用互联网文件系统（CIFS）
- Samba 和 NNLS

### 什么是服务器消息块（SMB）

服务器消息块（SMB）是一种在联网计算机之间共享资源的协议。

SMB 可以在多种协议上实现，包括 TCP/IP、NetBEUI 或 IPX/SPX。

> 有关 SMB 的更多信息，请参阅 http://www.samba.org/cifs/docs/what-is-smb.html。

### 什么是通用互联网文件系统（CIFS）

CIFS 是一种在原生 TCP/IP 上实现的 SMB，不需要 NetBIOS。

CIFS 是一种客户端/服务器协议，由 Microsoft Windows 操作系统使用。它也在许多其他平台（如 DOS、NetWare、UNIX®、Linux 和 VMS™）上实现。

使用 CIFS 的优点包括：

- 你不需要 Novell 客户端来访问文件。
- 你可以使用 Microsoft 网络的客户端。
- 所有 Windows 操作系统都支持 CIFS（必须支持 IP）。
- 大多数（如果有的话）应用程序都支持 CIFS（使用原生 Windows 网络）。
- 许多其他平台都有可用的实现（例如 UNIX/Linux 上的 Samba）。

### Samba 和 NNLS

Samba 是一组工具，让你可以使用 Microsoft 的 SMB/CIFS 网络协议在 Linux 计算机和其他平台上使用。

安装 Samba 后，Linux 计算机可以充当：

- **Windows 服务器。** Samba 使服务器能够向用户提供 Windows 文件和打印服务。
- **Windows 客户端。** Samba 使工作站能够访问和使用 Windows 文件和打印服务，无论它们源自 Windows 服务器还是安装了 Samba 的 Linux 服务器。

与 NNLS 一起安装的 Samba 发行版是专门为 NNLS 定制的，重点在于向在 Windows 客户端工作站上工作的用户提供经过身份验证的文件服务。

此发行版配置了以下功能：

- 使用 NNLS 附带的 Linux 用户管理（LUM）工具在 eDirectory 中创建 Samba 用户。
- 创建用户后，你必须使用 iManager 或 smbpasswd 工具为每个用户指定 Samba 密码。

![](img/d63035f3fce0eaaf97203dde900affb7_81_0.png)

- 当 LUM 用户首次通过基于文本的控制台登录到 NNLS 服务器时，会自动创建主目录并自动分配适当的文件访问权限。
- 访问 Samba 服务需要用户使用安全的 LDAP 向 NNLS 安装期间指定的 eDirectory 服务器进行身份验证。

![](img/d63035f3fce0eaaf97203dde900affb7_81_1.png)

## 目标 4 安装和配置 Samba

为了安装和配置 Samba，你需要了解以下内容：

- 安装 Samba 的步骤
- 如何配置 Samba
- 如何通过 Samba 访问文件

### 安装 Samba 的步骤

要在你的 Linux 服务器上安装 Samba，你需要执行以下操作：

- 满足 Samba 依赖项
- 收集所需信息
- 使用 NNLS 安装功能

如果你正在 NNLS 服务器上为网络中的 Windows 用户提供 Samba 文件服务，你还必须安装 Linux 用户管理（LUM）。

Linux 用户管理允许你创建可以访问 NNLS 服务器的 eDirectory 用户。

### 满足 Samba 依赖项

Samba 依赖于以下 NNLS 组件：

- 网络内任何地方的 eDirectory 8.7.1 或更高版本

如果此组件尚未安装，你不必在安装 Samba 之前安装它。

NNLS 安装程序会在你选择 Samba 组件时选择所需的组件及其依赖项（如果有）。Samba 及其依赖组件将在同一过程中安装。

有关成功安装尚未安装的 Samba 依赖项所需的必要信息，请参阅表 2-5。

以下描述了你在安装 Samba 之前需要知道的信息：

### 收集所需信息

![](img/d63035f3fce0eaaf97203dde900affb7_83_0.png)

| 所需的配置数据 | 描述 |
| :--- | :--- |
| eDirectory 服务器 IP 地址或 DNS 主机名 | 你正在其上安装 iFolder 的服务器的 IP 地址或 DNS 名称。Windows 用户将使用 LDAP 身份验证向 eDirectory 服务器进行身份验证以访问 NNLS 服务器上的目录和文件的主要 IP 地址。 |
| 带有上下文的 Admin 名称 | 为 Samba 指定的 eDirectory 服务器的 Admin 的完全限定名称。名称和上下文必须使用类型化语法指定（cn=name.ou=organizational-unit.o=organization）。 |
| Admin 密码 | Admin 的密码。 |
| LDAP 服务器 IP 地址或 DNS 主机名 | Windows 用户将使用 LDAP 身份验证向 eDirectory 服务器进行身份验证以访问 NNLS 服务器上的目录和文件的主要 IP 地址。 |
| 带有上下文的 Samba 代理用户名称 | 你希望 eDirectory 为 Samba 配置的代理用户的名称。安装脚本会为你创建此用户对象。 |
| Samba 代理用户密码 | Samba 代理用户的密码。 |


