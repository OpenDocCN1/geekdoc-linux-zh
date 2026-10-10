
# 第 18 章：设置文件服务器 765

* **认证模式（Authentication Mode）** — 选择 `User`（用户）、`Share`（共享）、`Server`（服务器）、`ADS` 或 `Domain`（域）。在本例中，我选择了 `User`。（请参阅本章稍后的“安全选项”部分获取有关每种认证模式的详细信息）。

* **认证服务器（Authentication Server）** — 只有当你的 Samba 服务器配置为使用 `Server` 或 `Domain` 安全时，此字段才有效。它标识了将用于验证 Samba 客户端输入的用户名和密码的服务器（NetBIOS 名称），客户端通过这些凭据访问此 Samba 服务器。使用用户认证时，密码会在 Samba 服务器上检查（在本例中，因此此字段为空）。

* **Kerberos 领域（Kerberos Realm）** — 如果你的网络使用 Kerberos 进行用户认证，请在此处输入你的 Kerberos 领域名称。

* **加密密码（Encrypt Passwords）** — 选择 `Yes`（期望客户端发送加密密码）或 `No`（期望明文密码）。请参阅本章稍后关于 Samba 客户端的章节，以确定如何配置客户端使用加密密码。

* **访客账户（Guest Account）** — 将此字段设置为分配给匿名用户请求的用户名。即使全局设置了 `User` 模式安全，你也可以为特定的 Samba 共享（如打印机）分配访客访问。

在使用 `User` 模式安全（本例），任何想要访问 Samba 共享的用户必须在 Linux 系统上拥有普通用户账户。（有关添加用户账户的信息请参阅第 11 章。）

* 6. 要将用户添加为 Samba 用户（即可以访问你 Samba 服务器的用户），选择 `Preferences`（偏好）-> `Samba users`。出现 `Samba users` 窗口。

* 7. 点击 `Add User`（添加用户）。出现 `New Samba User`（新建 Samba 用户）窗口。

* 8. 在 `Create New Samba User` 窗口中为以下字段提供信息并点击 `OK`：

  * **Username（用户名）** — 点击此框，然后选择你想授予访问 Samba 服务器的 Unix 用户名。

  * **Windows Username（Windows 用户名）** — 这是用户在请求目录时提供的用户名。（通常与 Unix 用户名相同。）

  * **Samba Password（Samba 密码）** — 输入 Samba 密码，然后在 `Confirm Samba password`（确认 Samba 密码）字段中重试。

* 9. 为每个想要访问 Samba 目录的用户重复上述步骤。

* 10. 现在你已经为你的 Samba 服务器配置了默认值，点击 `File`（文件）-> `Add Share`（添加共享）来添加要共享的目录。出现 `Create Samba Share` 窗口。

* 11. 填写 `Create Samba Share` 窗口中显示的以下字段：

  * **Directory（目录）** — 输入你想共享的目录名称。例如，你可能想要共享用户的家目录，如 `/home/chris`。

  * **Description（描述）** — 输入你喜欢的对共享目录的任何描述。

  * **Basic Permissions（基本权限）** — 选择 `Read-Only`（只读）或 `Read/Write`（读写）。对于只读，可以查看共享目录中的文件但不能更改。对于读写，只要用户拥有该文件的 Linux 访问权限，就可以自由添加、更改或删除文件。

* 12. 点击 `Access`（访问）选项卡，为访问共享选择以下选项之一，然后点击 `OK`：

  * **仅允许特定用户访问（Only allow access to specific users）** — 点击此处，选择哪些用户允许访问共享目录。例如，如果你正在共享用户的目录（如 `/home/chris`），你可能希望将访问限制为目录的所有者（例如 `chris`）。对特定文件和目录的读写访问由分配给它们的 Linux 所有权组决定。

  * **允许所有人访问（Allow access to everyone）** — 如果你想允许任何人访问此目录，请选择此选项。（所有用户在访问目录时将拥有分配给访客的权限。）

点击 `OK` 后，Samba 将启动，新目录将立即可用。你可以关闭 Samba Server 窗口。

* 13. 虽然此时 Samba 应该已经在运行，但你可能需要设置 Samba 在每次重启时自动启动。要这样做，请在终端窗口中以 root 用户身份输入以下命令：

```
chkconfig samba on
```

如果 Samba 没有运行，运行 `service samba start` 立即启动它。你可以对每个想要在网络上提供的目录重复添加 Samba 目录的步骤。此时，你可以执行以下操作之一：

更详细地查看你的 Samba 服务器设置（如“使用 SWAT 配置 Samba”所述），以了解你可能想要如何调整你的 Samba 服务器。尝试从网络上的客户端计算机访问你创建的共享目录。请参考“在 Linux 中挂载 Samba 目录”部分。

如果你无法从 Windows 计算机或局域网上的 Linux 计算机打开配置的共享目录，你可能遇到了以下问题之一：

* 客户端未提供有效的用户名和密码。
* 客户端未提供加密密码。

解决这些问题的快速方法是使用共享级安全（当然，这会丢弃你的安全性）。另一种解决方案是更新密码并确保客户端正在使用加密密码（如“设置客户端”部分所述）。

## 使用 SWAT 配置 Samba

Samba 管理工具 (`SWAT`) 是一个用于配置 Samba 的 Web 界面。虽然它不像 Samba 配置窗口那样易于使用，但它提供了更多调整 Samba 的选项以及每个选项的帮助信息。此外，由于 `SWAT` 是基于 Web 的，你可以从任何 Web 浏览器远程配置系统。

注意：`SWAT` 和 Samba 配置窗口都通过修改 `/etc/samba/smb.conf` 文件来配置 Samba。不同的 GUI 工具可能会覆盖彼此的设置，有时会导致工具无法工作。通常情况下，在使用 GUI 工具之前，最好为你的文件创建一个备份副本。最终，你应该选择一个工具并坚持使用它。

### 开启 SWAT

在使用 `SWAT` 之前，你必须安装 `samba-swat` 软件包（`yum samba-swat`）并启动 `swat` 服务。要设置 `SWAT` 从你的浏览器中运行，请按照以下步骤操作：

1. 要开启 `swat` 服务，请在终端窗口中以 root 用户身份输入以下命令：

```
chkconfig swat
```

2. 使更改生效，执行以下命令重启 `xinetd`：

```
service xinetd restart
```

当你完成此过程后，可以使用 `SWAT` 配置 Samba。

### 启动 SWAT

你可以通过在浏览器中输入 `http://localhost:901` 来运行 `SWAT`。此时，浏览器将提示输入用户名和密码。`SWAT` 窗口将如 18-5 所示。

![](img/c7605e408543e0a1829c1fd0cf2f687d_802.png)

图 18-5：使用 SWAT 管理你的配置。

提示：为了允许局域网计算机访问 `SWAT`，你必须更改 `/etc/xinetd.d/swat` 文件中的 `only_from =127.0.0.1` 行并重启 `SWAT`。

其余部分介绍了如何使用 `SWAT` 创建你的配置项（在 `/etc/samba/smb.conf` 中）。

注意：每当你使用 GUI 修改文本文件（如使用 `SWAT` 时），你可能会丢失手动输入的信息。`SWAT` 会删除注释行并重新排列项目。为了保护你手动修改的内容，在使用 `SWAT` 之前，请为 `/etc/samba/smb.conf` 创建备份。

### 在 SWAT 中创建全局设置

一组全局设置影响 Samba 服务器如何实现文件和打印。它们出现在 `/etc/samba/smb.conf` 的 `[global]` 标题下。要编辑全局变量，点击 Samba 窗口上的 `GLOBALS` 选项。

有九种选项类型：基础、安全、日志、协议、打印、浏览、`WINS`、事件日志和绑定。要查看并修改你的全局设置，点击 `GLOBALS` 选项。然后添加以下选项。

注意：显示的每个选项都与 `/etc/samba/smb.conf` 中的实际参数对应。你可以参考 `smb.conf` 手页（输入 `man smb.conf`）来获取更多信息。

#### 基础选项

以下选项与基本信息相关：

* `workgroup` — 与 SMB 组关联的工作组名称。在 Fedora 和 RHEL 中，该字段的默认值为 `MYGROUP`。

* `realm` — 如果你正在使用 Kerberos 认证，此值指示要使用的 Kerberos 领域。通常这由提供服务的主机名反映。

* `netbios name` — 分配给此 Samba 服务器的名称。你可以使用与 DNS 主机名相同的名称，或者留空，这将自动使用 DNS 主机名。
