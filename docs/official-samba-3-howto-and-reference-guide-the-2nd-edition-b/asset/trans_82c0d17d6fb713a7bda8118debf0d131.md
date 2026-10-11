

出于安全原因，该管理员账户的密码应设置为与 `/etc/passwd` 中 root 用户使用的密码不同的密码。

用于创建域成员机器信任账户的账户名称可以是网络管理员选择的任意名称。如果该名称不是 root，则可以轻松映射到由 `smb.conf` 参数 `username map = /etc/samba/smbusers` 中指定的文件中的 root。

Samba 管理员账户的会话密钥充当设置机器信任账户密码的加密密钥。机器信任账户将即时创建，或者如果已存在则进行更新。

### 6.2.4.2 Windows NT4 客户端

如果机器信任账户是手动创建的，请在“身份标识更改”菜单中输入域名称，但**不要**勾选**在域中创建计算机账户**复选框。在这种情况下，现有的机器信任账户将被用于将计算机加入域。

如果要即时创建机器信任账户，请在“身份标识更改”菜单中输入域名称，并勾选**在域中创建计算机账户**复选框。在这种情况下，加入域的过程与上述 Windows 2000 的过程相同（即，当提示时，必须提供 Samba 管理员账户）。

### 6.2.4.3 Samba 客户端

将 Samba 客户端加入域的说明请参见第 6.3 节。

## 6.3 域成员服务器

这种服务器运行模式涉及将 Samba 机器成为域安全上下文的成员。这意味着从定义上讲，所有用户身份验证都将从集中定义的身份验证机制进行。该身份验证机制可能来自 NT3/4 风格的（旧式域技术）服务器，也可能来自运行在 MS Windows 2000 或更高版本上的活动目录服务器（ADS）。

> 当然，应该很清楚，身份验证后端本身可以来自 Samba 支持的任何一种分布式目录架构服务器。这可以是 LDAP（来自 OpenLDAP）、Sun 的 iPlanet、Novell e-Directory Server 等。

![](img/86d74c6cc862465e3a42e6dc3c90935a_136_0.png)

> 当 Samba 配置为使用 LDAP 或其他身份管理和/或目录服务时，仍由 Samba 执行用户和机器身份验证。需要注意的是，LDAP 服务器不会代替 Samba 执行其设计的功能来处理身份验证。

有关如何为域成员服务器创建域机器账户以及如何启用 Samba 域成员机器加入域并完全受其信任的更多信息，请参见第 4 章“域控制”。

### 6.3.1 使用 Samba-3 加入 NT4 类型的域

表 6.1 列出了本章其余部分中使用的名称。

| 表 6.1 假设条件 | |
| :--- | :--- |
| Samba 域成员服务器 NetBIOS 名称： | SERV1 |
| Windows 200x/NT 域名称： | MIDEARTH |
| 域的 PDC NetBIOS 名称： | DOMPDC |
| 域的 BDC NetBIOS 名称： | DOMBDC1 和 DOMBDC2 |

首先，你必须编辑你的 smb.conf 文件，告诉 Samba 它现在应该使用域安全性。将 smb.conf `[global]` 部分中的 `security` 行更改（或添加）为：

```
security = domain
```

请注意，如果使用参数 `security = user`，该机器将作为独立服务器运行，而不是作为域成员服务器运行。域安全模式使 Samba 在域安全上下文中运行。

接下来，将 `[global]` 部分中的 `workgroup` 行更改为：

```
workgroup = MIDEARTH
```

这是我们要加入的域的名称。

你还必须将参数 `encrypt passwords` 设置为 `yes`，以便你的用户能够向 NT PDC 进行身份验证。如果未指定此参数，这是默认设置。没有必要指定此参数，但如果在 smb.conf 文件中指定，则必须设置为 `Yes`。

最后，在 `[global]` 部分中添加（或修改）`password server` 行，使其读取为：

```
password server = DOMPDC DOMBDC1 DOMBDC2
```

这些是 Samba 将尝试联系以进行用户身份验证的 PDC 和 BDC。Samba 将按顺序尝试联系这些服务器中的每一个，因此你可能希望重新排列此列表，以便在域控制器之间分散身份验证负载。

或者，如果你希望 smbd 自动确定用于身份验证的域控制器列表，你可以将此行设置为：

```
password server = *
```

这种方法允许 Samba 使用与 NT 完全相同的机制。该方法使用基于广播的名称解析，执行 WINS 数据库查询以找到用于身份验证的域控制器，或使用 DNS 名称解析定位域控制器。

要加入域，请运行此命令：

```
root# net rpc join -S DOMPDC -UAdministrator%password
```

如果未提供 `-S DOMPDC` 参数，则域名称将从 smb.conf 获取，PDC 的 NetBIOS 名称将通过 WINS 查询或基于广播的 NetBIOS 名称查找获取。

该机器正在加入域 DOM，而该域的 PDC（唯一对域 SAM 数据库具有写访问权限的机器）是 DOMPDC；因此，请使用 `-S` 选项。`Administrator%password` 是具有将机器添加到域所需的特权的账户的登录名和密码。如果成功，你将看到终端窗口中出现以下消息。在旧式的 NT4 风格的域架构中使用时：

```
Joined domain DOM.
```

在使用活动目录时，加入 ADS 域使用的命令是：

```
root#  net ads join -UAdministrator%password
```

以下输出表示成功结果：

```
Joined SERV1 to realm MYREALM.
```

有关更多信息，请参见 `net` 手册页和第 12 章“远程和本地管理：Net 命令”。

此过程将服务器加入域，无需事先单独在 PDC 上创建机器信任账户。

此命令通过机器账户密码更改协议，然后将新的（随机）机器账户密码写入此 Samba 服务器所在目录中与 smbd 密码文件通常存储位置相同的目录中的文件。DNS 所需的信任账户信息写入文件 /usr/local/samba/private/secrets.tdb 或 /etc/samba/secrets.tdb。

此文件由 root 创建并拥有，其他任何用户均不可读。它是系统域级安全性的关键，应像 shadow 密码文件一样仔细对待。

最后，重启你的 Samba 守护进程，准备让客户端开始使用域安全性。重启 Samba 守护进程的方式取决于你的发行版，但在大多数情况下，以下内容就足够了：

```bash
root # /etc/init.d/samba restart
```

### 6.3.2 为什么这比 security = server 更好？

目前，Samba 中的域安全性并不能免除你创建本地 UNIX 用户以表示连接到你的服务器的用户。这意味着，如果域用户 DOMfred 连接到你的域安全性 Samba 服务器，则需要一个本地 UNIX 用户 fred 来表示 UNIX 文件系统中的该用户。这与旧式的 Samba 安全模式 `security = server` 类似，在旧模式中，Samba 会像 Windows 95 或 Windows 98 服务器那样将身份验证请求传递给 Windows NT 服务器。

有关自动为 Windows NT 域用户和组分配 UNIX UID 和 GID 系统的信息，请参见第 23 章“Winbind：域账户的使用”。

域级安全的优势在于，域级安全中的身份验证通过经过身份验证的 RPC 通道向下传递，方式与 NT 服务器完全相同。这意味着 Samba 服务器现在以与 NT 服务器完全相同的方式参与域信任关系（即，你可以将 Samba 服务器添加到资源域中，并将身份验证从资源域 PDC 传递到账户域 PDC）。

此外，使用 `security = server` 时，服务器上的每个 Samba 守护进程都必须保持与身份验证服务器的连接开放，直到该守护进程终止为止。这可能会耗尽 Microsoft NT 服务器上的连接资源，导致其可用连接耗尽。然而，使用 `security = domain` 时，Samba 守护进程仅在必要时连接到 PDC 或 BDC 以进行用户身份验证，然后断开连接，从而节省 PDC 连接资源。

