
如果你有 Internet 连接，可以在开始配置 Samba 之前尝试安装 samba，读取位于 `/usr/share/doc/samba*` 的 `README` 文件。它提供了关于 SMB 协议和 Samba 的良好概述。

> 注意：随着 Fedora 软件存储库的扩展，现在可以使用其他处理 Samba 的实用工具。你搜索的 `smb4pkg` 软件包可以搜索可用的 SMB/CIFS 资源并将其挂载到你的计算机上。`fuse-smb` 软件包可以让你查找并浏览网络上可用的 SMB 共享。

# 配置一个简单的 Samba 服务器

Samba 服务器配置窗口允许你进行基础 Samba 配置并识别你想要共享的目录。为了使此过程变得有用，我正在设置一种特定类型的共享环境（如果你愿意，可以对其进行修改）。以下是其特征：

- **单一局域网** — 包含多台 Windows 和 Linux 机器。
- **用户级安全** — 任何想要获取 Samba 文件的用户都必须在 Linux 服务器上拥有有效的登录名和密码。
- **加密密码** — 许多客户端默认对 Samba (SMB) 使用加密密码。我将描述如何为不使用加密密码的客户端开启加密密码。
- **访客用户账户** — 访客用户账户以后很有用，因此你可以设置 Samba 让没有访问服务器打印机权限的用户通过 Samba 访问打印机。

以下步骤描述了如何配置 Samba 并在 Samba 中创建共享目录：

1. 要打开 Samba 配置窗口，请点击 `System -> Administration -> Samba`。Samba 服务器配置窗口将打开。（你可能需要输入 root 密码）。
2. 点击 `Preferences -> Server Settings`。出现 Server Settings 窗口，如图 18-3 所示。

## 第 18 章：设置文件服务器

![](img/6a8f767dda2519b458f97c2e7f586576_816_0.png)

**图 18-3：** 为你的 Samba 服务器定义窗口和描述。

3. **输入 workflow 选项卡**（以与你想共享文件的或其他计算机匹配）以及简短描述。
4. **点击 Security 选项卡**。出现一个类似图 18-4 的窗口。

![](img/6a8f767dda2519b458f97c2e7f586576_816_1.png)

**图 18-4：** 为 Security 选项卡上的字段和你的 Samba 服务器填写信息。

5. 为 Security 选项卡上的字段提供信息并点击 OK：
    * **Authentication Mode（认证模式）** — 选择 User、Share、Server、ADS（活动目录服务器）或 Domain。在这种情况下，我选择了 User。（有关每个认证模式的详情，请参阅本章后面的“Security options”部分。）
    * **Authentication Server（认证服务器）** — 此字段仅当你的 Samba 服务器配置为使用 Server 或 Domain 身份时有效。它标识了用于验证 Samba 客户端为访问此服务器而输入的用户名和密码的服务器（NetBIOS 名称）。当使用用户认证时，密码会在 Samba 服务器上检查（在本例中，因此此字段为空白）。
    * **Kerberos Realm（Kerberos 域）** — 如果你的网络使用 Kerberos 进行用户认证，在此处输入你的 Kerberos 域名称。

# 第四部分：Fedora 和 RHEL 网络与服务器设置

- **Encrypt Passwords（加密密码）** — 选择 Yes（期望客户端发送加密密码）或 No（期望明文密码）。参阅本章稍后的 Samba 客户端部分以确定如何配置客户端使用加密密码。
- **Guest Account（访客账户）** — 将此设置为分配给匿名用户请求的用户。即使全局设置了 User 模式安全，你也可以将访客访问分配给特定的 Samba 共享（如打印机）。使用 User 模式安全（本例正在使用的），任何想要访问 Samba 共享的用户都必须在 Linux 系统上拥有普通用户账户。（有关添加用户账户的信息请参考第 11 章。）

6. 要将用户添加为 User（即可以访问你的 Samba 服务器的用户），选择 `Preferences -> Samba Users`。出现 Samba Users 窗口。
7. 点击 `Add User`。出现 New Samba User 窗口。
8. 在 Create New Samba 窗口中为以下字段提供信息并点击 OK：
    - **Unix Username（Unix 用户名）** — 点击此框，并选择你想要获取 Samba 服务器权限的 Linux 用户名。
    - **Windows Username（Windows 用户名）** — 这是用户在请求目录时提供的名称。（通常与 Unix Username 相同。）
    - **Samba Password（Samba 密码）** — 输入 Samba 密码，并重复输入到 Confirm Samba Password 字段中。
9. 为你想添加的每个用户重复上一步步骤。
10. 现在你已经配置了 Samba，通过点击 `File -> Share` 添加目录。出现 Create Share 窗口。
11. 填写 Create Share 窗口中的字段：
    - **Directory（目录）** — 输入你想要共享的目录名称。
    - **Description（描述）** — 为该共享输入任何描述。
    - **Basic Permissions（基本权限）** — 选择 Read-only 或 Read/Write。Read-only 表示只能查看不能更改；Read/Write 表示用户可以自由添加、更改或删除文件。
12. 点击 Access 选项卡，选择以下访问共享选项，然后点击 OK：
    - **Only access to specific users（仅特定用户访问）** — 限制访问。
    - **Allow access to everyone（允许所有人访问）** — 如果你想允许任何人访问，选择此选项。（访问时所有用户将拥有访客权限。）

点击 OK 后，Samba 启动，目录立即可用。你可以关闭 Samba 窗口。

13. 虽然 Samba 现在应该运行，但你可能需要设置 Samba 在重启时自动启动。要执行此操作，在终端中以 root 用户身份输入：

```bash
# chconfig smb on
```

如果 Samba 尚未运行，输入 `service samba` 启动它。对于你想在网络上提供的每个目录，重复上述步骤。此时，你可以执行以下操作：

- 详细查看你的 Samba 设置（如下文“Configuring Samba with SWAT”部分所示），了解你可能想如何调整你的 Samba 服务器。
- 从客户端尝试访问你创建的共享。要执行操作，请参考本章后面的“在 Linux 中挂载 Samba 目录”部分。

# 使用 SWAT 配置 Samba

Samba Web 管理工具 (SWAT) 是用于配置 Samba 的 Web 界面。虽然它不像 Samba 服务器配置窗口那样容易使用，但它提供了更多调整 Samba 的选项以及每个选项的帮助。此外，由于 SWAT 是基于 Web 的，你可以从任何 Web 浏览器远程配置你的系统。

# 778 第四部分：Fedora RHEL 网络与服务器设置

> 注意：SWAT 和 Samba 配置窗口都通过修改 `/etc/samba/smb.conf` 文件来配置 Samba。不同的 GUI 工具会相互覆盖对方的设置，有时会导致另一个工具无法工作。

通常情况下，在切换 GUI 工具之前，最好对你的文件进行备份复制。最终，你应该选择一个工具并坚持使用它。

## 开启 SWAT

在使用 SWAT 之前，你必须已安装 samba-swat 软件包（`yum install samba-swat`）并启动 swat 服务。要从浏览器设置 SWAT，请遵循以下步骤：

- 1. 要开启 swat 服务，请在终端（Terminal）窗口中以 root 用户身份输入以下命令：
```bash
# chconfig swat on
```
- 2. 要使 swat 服务的更改生效，请按如下为正在运行的 xinetd 启动脚本重载数据：
```bash
# service xinetd reload
```
