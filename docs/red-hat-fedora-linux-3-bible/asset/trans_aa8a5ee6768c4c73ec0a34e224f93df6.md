
# mount /media/cdrecorder
# cd /media/cdrecorder /Fedora/RPMS
# rpm -Uvh samba\*
# cd ; umount /mnt/cdrom

在开始尝试配置 Samba 之前，请阅读 README 文件（位于 `/usr/share/doc/samba\*`）。它提供了关于 SMB 协议和 Samba 的良好概述。

### 配置简单的 Samba 服务器

Samba 服务器配置窗口允许你进行基本的 Samba 配置，然后确定你要共享哪些目录。为了使此步骤有用，我将设置一种特定类型的共享环境（如果你愿意，之后可以修改它）。其特征如下：

- **单个局域网：** 包含多台 Windows 和 Linux 机器。
- **用户级安全性：** 任何想要访问共享 Samba 文件的用户必须在 Linux Samba 服务器上拥有有效的登录名和密码。
- **加密密码：** 许多客户端默认使用加密密码与 Samba (SMB) 通信。我将描述如何为不使用加密密码的客户端开启加密密码功能。
- **来宾用户账户：** 来宾用户账户在后文会有用，因此你可以设置 Samba 让没有特殊账户的用户通过 Samba 使用服务器的打印机。

以下程序描述了如何配置 Samba 并在 Samba 中创建共享目录：

1. 要打开 Samba 服务器配置窗口，请单击 **系统设置** → **服务器设置** → **Samba**。Samba 服务器配置窗口将打开。（你可能需要输入 root 密码。）
2. 单击 **首选项** → **服务器设置**。服务器设置窗口将显示，如图 18-3 所示。
3. 输入工作组名称（以匹配你希望共享文件的其他计算机的工作组名称）和一个简短的描述。

![](img/b22364e57409c2481ba806e4e6b9309c_735_0.png)

图 18-3：为你的 Samba 服务器定义工作组和描述。

4. 单击“Security”标签页。会出现如图 18-4 所示的窗口。

![](img/b22364e57409c2481ba806e4e6b9309c_735_1.png)

图 18-4：为你的 Samba 服务器填写 Security 信息。

5. 为“Security”标签页上的字段提供以下信息，然后单击“OK”：

- **Authentication Mode** — 选择 User、Share、Server、ADS 或 Domain。在此示例中，我选择了 User。（有关每个身份验证模式的详细信息，请参阅本章稍后的“Security options”部分。）
- **Authentication Server** — 此字段仅在 Samba 服务器配置为使用 Server 或 Domain 安全性时有效。它标识用于身份验证 Samba 客户端输入的 username 和密码的服务器（NetBIOS 名称）。使用用户身份验证时，密码将在 Samba 服务器上进行检查（因此在此示例中，此字段为空）。
- **Encrypt Passwords** — 选择 Yes（期望客户端发送加密密码）或 No（期望明文密码）。请参阅本章稍后关于 Samba 客户端的部分，以确定如何配置客户端使用加密密码。
- **Guest Account** — 将此字段设置为你希望分配给匿名用户请求的用户名。即使全局设置了 User 模式安全性，你仍可以为特定的 Samba 共享（如打印机）分配来宾访问权限。

使用 User 模式安全性（在此示例中使用），任何想要访问 Samba 共享的用户必须在 Linux 系统上拥有常规用户账户。（有关添加用户账户的信息，请参阅第 11 章。）

6. 要将用户添加为 Samba 用户（即可以访问你的 Samba 服务器的用户），请选择 首选项 → Samba 用户。将显示 Samba 用户窗口。
7. 单击“Add User”。将显示“Create New Samba User”窗口。
8. 为“Create New Samba User”窗口中的以下字段提供信息，然后单击“OK”：

- **Unix Username** — 单击此框，然后选择你要授予 Samba 服务器访问权限的 Linux 用户名。
- **Windows Username** — 这是用户在请求共享目录时提供的用户名。（通常，它与 Unix 用户名相同。）
- **Samba Password** — 输入 Samba 密码，然后将其重新输入到“Confirm Samba Password”字段中。

9. 对于每个你希望访问 Samba 共享目录的用户，重复上一步。
10. 既然你已配置了 Samba 共享的默认值，请通过单击 文件 → 添加共享来添加要共享的目录。将显示“Create Samba Share”窗口。
11. 填写“Create Samba Share”窗口中显示的以下字段：

- **Directory** — 输入你要共享的目录的名称。例如，你可能希望共享用户的家庭目录，如 /home/chris。
- **Description** — 输入关于共享目录的任何描述。
- **Basic Permissions** — 选择“Read-only”或“Read/Write”。对于“Read-only”，文件可以在共享目录中查看，但不能更改。对于“Read/Write”，只要该用户拥有对特定文件的 Linux 文件访问权限，就可以自由添加、更改或删除文件。

12. 单击“Access”标签页，选择以下选项之一以允许对共享的访问，然后单击“OK”：

- **Only allow access to specific users** — 单击此处，然后选择哪些用户将被允许访问共享目录。例如，如果你正在共享用户的目录（如 /home/chris），你可能希望将该目录的访问权限限制在该目录的所有者（例如 chris）。对特定文件和目录的读取和写入访问权限由分配给它们的 Linux 所有权和组确定。
- **Allow access to everyone** — 如果你希望允许任何人访问此目录，请选择此选项。（所有用户在访问目录时将具有分配给来宾用户的权限。）

单击“OK”后，Samba 将启动，新目录立即可用。你可以关闭 Samba 服务器配置窗口。

13. 虽然 Samba 此时应该正在运行，但你可能需要设置 Samba 在每次重启 Linux 时自动启动。为此，请在终端窗口中以 root 用户身份输入以下内容：

```
chkconfig smb on
```

你可以对每个希望使其在网络上可用的目录重复添加 Samba 共享目录的步骤。此时，你可以选择：

- 更详细地浏览你的 Samba 服务器设置（如“使用 SWAT 配置 Samba”部分所述），以了解你可能想如何进一步调整 Samba 服务器。
- 尝试从网络上的客户端计算机访问你刚刚创建的共享目录。

如果你无法从局域网中的 Windows 计算机或其他 Linux 计算机打开你刚刚配置的共享目录，你可能正遇到以下问题之一：

- 客户端未提供有效的用户名和密码。
- 客户端未提供加密密码。

解决这些问题的快捷方式是仅使用共享级安全性（当然，这会大大降低你的安全性）。另一种解决方案是更新密码并确保客户端使用加密密码（如本章稍后的“设置 Samba 客户端”部分所述）。

### 使用 SWAT 配置 Samba

Samba 网络管理工具（SWAT）是用于配置 Samba 的基于 Web 的界面。虽然它不像 Samba 服务器配置窗口那样易于使用，但它提供了更多的选项来调整 Samba，并为每个选项提供帮助说明。

> **注意：** SWAT 和 Samba 服务器配置窗口都通过修改 `/etc/samba/smb.conf` 文件来配置 Samba。不同的 GUI 工具可能会相互覆盖设置，有时会导致另一个工具无法正常工作。

通常，最好在切换 GUI 工具之前对文件进行备份。最终，你应该选择一个工具并坚持使用它。
