
Samba 服务器配置工具用于为 Fedora Core 4 提供详细信息，说明哪些文件和目录应对网络上的其他 Windows 主机可用。启动 Samba 服务器配置工具，选择 Desktop、System Settings、Server Settings、Samba。Samba 服务器配置工具出现，如图 33.7 所示。

图 33.6

软件包管理工具，勾选 Windows File Server 包组旁边的框。

![](img/2d355c162ea76302aa136ba324839b24_631_0.png)

图 33.7

Samba 服务器配置工具告诉 Fedora Core 4 你想要共享的文件和目录。

![](img/2d355c162ea76302aa136ba324839b24_631_1.png)

# 决定安全模型

对于特定的共享文件夹或文件集，你可以通过两种方式为 Windows 文件共享用户提供权限：

- 完全的公共访问。在你共享一个文件或目录后，网络上的每个人都可以访问。
- 按用户访问。在创建了一份应该有访问你的 Fedora Core 4 计算机的 Windows 文件共享权限的用户列表后，你将根据此列表按用户授予共享文件或目录的访问权限。

# 提供 Windows 文件共享服务

你可以使用这两种范式的组合，对某些共享文件或目录提供完全的公共访问，同时将其他共享文件或文件夹限制为选用户列表。

# 创建 Samba 用户列表

要按用户限制对共享文件或目录的访问，你必须创建一个用户列表。要维护用户列表，在 Samba 服务器配置工具中选择 Preferences、Samba。Samba Users 对话框出现，如图 33.8 所示。

![](img/2d355c162ea76302aa136ba324839b24_632_0.png)

图 33.8

使用 Samba Users 对话框，你可以维护用户列表。

要向列表中添加新用户，点击右侧的 Add 按钮。另一个对话框 Create Samba User 出现，如图 33.9 所示。

![](img/2d355c162ea76302aa136ba324839b24_632_1.png)

图 33.9

使用 Create Samba User 对话框可以创建一个用户。

按照以下步骤填写 Create Samba User 对话框中的字段：

1. 在 `Username` 下拉列表中，选择将获得访问的本地（Fedora Core 4）用户。
2. 在 `Windows Username` 输入框中输入用户在 Windows 网络上的帐户名。
3. 在 `Samba Password` 输入框中输入用户的 Windows 网络或主机密码。
4. 在 `Confirm Samba Password` 框中重新输入密码以确保你输入正确。
5. 点击 `OK` 保存更改并将用户添加到列表。

在你编辑列表后，点击 `OK` 关闭 Samba Users 对话框并保存更改。

# 编辑和删除 Samba 用户

你可能注意到 Samba Users 对话框中还有两个按钮。这些按钮的功能完全正如你根据标签所预期的。

`Edit User` 按钮用于编辑当前选中用户的设置。当你点击 `Edit User` 时，会出现一个与 Create Samba 对话框相同的对话框，并已填充该用户的设置。根据需要进行编辑并点击 `OK` 保存更改。

`Delete User` 按钮用于从 Samba 用户列表中删除当前选的用户。被删除的用户将失去对你的 Fedora Core 4 计算机的所有 Windows 网络权限，标记为公共的共享文件或目录除外。

# 创建 Windows 共享

Windows 网络通过称为共享的单元提供文件和目录。要创建一个从你的 Fedora Core 4 系统可用的新共享，选择 `File`、`Add Share` 或点击 Samba 配置窗口顶部的 `Add` 按钮。显示 Create Samba Share 对话框，如图 33.10 所示。

要在 Create Samba Share 对话框中添加共享，请遵循以下步骤：

1. 在 `Directory` 输入框中输入你想共享的路径（文件夹或目录树）。
2. 在 `Share` 框中输入共享名称。这是当其他人浏览你的计算机时，该目录下方显示的图标名称。

例如，一些合适的共享名称可以是 `HardDrive`、`PublicFiles`、`Graphics`。

![](img/2d355c162ea76302aa136ba324839b24_634_0.png)

图 33.10

创建 Samba 共享对话框帮助你创建新的共享，这些共享将从你的 Fedora Core 4 计算机提供。

3. 在 `Description` 框中输入此共享的简短人类可读的描述。
4. 如果你想授予网络上的其他主机同时读取和写入权限，请勾选 `Writable` 框；如果该目录仅供读取共享，则取消勾选。
5. 如果你希望共享在其他用户浏览你的计算机时显示在他们的文件管理器中，请勾选 `Visible` 框。如果希望远程用户必须通过名称请求共享才能看到，请取消勾选。
6. 点击创建 Samba 共享对话框中的 `Access` 选项卡。
7. 如果你想让共享设为公开（网络上的所有人都可以访问），选择 `Allow Access to Everyone`。否则，选择 `Only Allow Access to Specific Users`，然后勾选允许在网络上访问此共享的用户名称，如图 33.11 所示。

![](img/2d355c162ea76302aa136ba324839b24_634_1.png)

图 33.11

要将共享访问限制为特定用户组，选择 `Only Allow Access to Specific Users`；然后勾选他们名称旁边的框。

8. 点击 `OK` 保存你创建的共享。

## 第 33 章：提供网络文件服务

### 顺便说

# 文件共享时权限至关重要

即使为某个用户或用户组授予了共享的只读或读/写权限，Linux 文件系统的权限仍然会发生变化。远程用户读取或写入共享文件或目录的能力，受 Linux 文件系统授予该用户的权限的限制。有关文件系统权限的更多信息，请参阅第 7 章“理解文件属性”。

对你需要创建的每个共享重复此过程。在完成所有所需的共享后，选择 `File`、`Quit` 或点击应用程序窗口右上角的 Close 按钮以保存你的更改。

# 启动和自动启动 Windows 文件服务

要在配置后从桌面启动 Windows 文件服务器，请选择 Desktop、Server Settings、Services 以显示服务配置工具。选择 `smb` 服务；点击应用程序窗口顶部的 `Start` 按钮，如图 33.12 所示。

图 33.12

要启动 Windows 文件共享，选择 `smb` 服务并点击 `Start`。要使服务在每次 Fedora Core 4 启动时启动，请勾选 `smb` 旁边的框。

![](img/2d355c162ea76302aa136ba324839b24_635_0.png)

要让 Windows 文件共享在每次 Fedora Core 4 启动时启动，请勾选 `smb` 服务旁边的框，点击 `Save`，然后选择 `File`、`Quit` 以退出服务配置工具。

从命令行，你可以使用第 28 章学过的 `service` 命令启动 Windows 文件共享：

```
[root@workstation20 you]$ /sbin/service smb
[root@workstation20 you]$ *
```

# 总结

你可以使用命令行中的 `chkconfig` 命令配合 `--level` 选项，并将 `smb` 和 `on` 作为参数，配置 Windows 文件服务器为你的默认运行级别自动启动：

```
[root@workstation20 ~]# /sbin/chkconfig --level 5 smb
[root@workstation20 ~]#
```

# 通过防火墙允许 Windows 文件服务

尽管你的 Windows 文件服务器现在已完全配置并运行，但在你告诉防火墙允许 Windows 文件服务流量之前，网络上的用户无法访问你的 Windows 共享。

要启用 Windows 文件服务流量，通过 Desktop、System Settings、Security Level 启动安全级别配置。按照通常方式配置防火墙，但在工具底部的 Other Ports 目中输入以下额外端口：

`137:tcp`, `137:udp`, `138:tcp`, `138:udp`, `139:tcp`, `139:udp`

再次，请确保在每次运行安全级别配置工具时都输入这些端口以及你为防火墙配置的任何其他特殊端口，因为它替换之前的设置而不是增加它们。配置好防火墙后，点击 `OK` 按钮保存并激活你的防火墙设置并关闭安全级别配置工具。

# 总结
