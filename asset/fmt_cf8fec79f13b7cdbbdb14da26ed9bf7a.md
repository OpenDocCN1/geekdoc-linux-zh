
或者，如果你希望 `smbd` 自动确定用于身份验证的域控制器列表，你可以将此行设置为：

```
password server = *
```

这种方法允许 Samba 使用与 NT 完全相同的机制。该方法使用基于广播的名称解析，执行 WINS 数据库查询以找到用于身份验证的域控制器，或使用 DNS 名称解析定位域控制器。

要加入域，请运行此命令：

```
root# net rpc join -S DOMPDC -UAdministrator%password
```

如果未提供 `-S DOMPDC` 参数，则域名称将从 `smb.conf` 获取，PDC 的 NetBIOS 名称将通过 WINS 查询或基于广播的 NetBIOS 名称查找获取。

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

此命令通过机器账户密码更改协议，然后将新的（随机）机器账户密码写入此 Samba 服务器所在目录中与 `smbd` 密码文件通常存储位置相同的目录中的文件。DNS 所需的信任账户信息写入文件 `/usr/local/samba/private/secrets.tdb` 或 `/etc/samba/secrets.tdb`。

此文件由 `root` 创建并拥有，其他任何用户均不可读。它是系统域级安全性的关键，应像 `shadow` 密码文件一样仔细对待。

最后，重启你的 Samba 守护进程，准备让客户端开始使用域安全性。重启 Samba 守护进程的方式取决于你的发行版，但在大多数情况下，以下内容就足够了：

```bash
root # /etc/init.d/samba restart
```

### 6.3.2 为什么这比 security = server 更好？

目前，Samba 中的域安全性并不能免除你创建本地 UNIX 用户以表示连接到你的服务器的用户。这意味着，如果域用户 DOMfred 连接到你的域安全性 Samba 服务器，则需要一个本地 UNIX 用户 fred 来表示 UNIX 文件系统中的该用户。这与旧式的 Samba 安全模式 `security = server` 类似，在旧模式中，Samba 会像 Windows 95 或 Windows 98 服务器那样将身份验证请求传递给 Windows NT 服务器。

有关自动为 Windows NT 域用户和组分配 UNIX UID 和 GID 系统的信息，请参见第 23 章“Winbind：域账户的使用”。

域级安全的优势在于，域级安全中的身份验证通过经过身份验证的 RPC 通道向下传递，方式与 NT 服务器完全相同。这意味着 Samba 服务器现在以与 NT 服务器完全相同的方式参与域信任关系（即，你可以将 Samba 服务器添加到资源域中，并将身份验证从资源域 PDC 传递到账户域 PDC）。

此外，使用 `security = server` 时，服务器上的每个 Samba 守护进程都必须保持与身份验证服务器的连接开放，直到该守护进程终止为止。这可能会耗尽 Microsoft NT 服务器上的连接资源，导致其可用连接耗尽。然而，使用 `security = domain` 时，Samba 守护进程仅在必要时连接到 PDC 或 BDC 以进行用户身份验证，然后断开连接，从而节省 PDC 连接资源。

最后，以与 NT 服务器向 PDC 认证相同的方式进行操作意味着，作为认证回复的一部分，Samba 服务器会获取用户标识信息，例如用户 SID、用户所属的 NT 组列表等。

> **注意**
>
> 本文档中的许多内容最初发布在 Web 杂志《*LinuxWorld*》上，文章标题为*《执行 NIS/NT Samba》*（链接：`<http://www.linuxworld.com/linuxworld/lw-1998-10/lw-10-samba.html>`）。

### 6.4 Samba ADS 域成员资格

这是关于设置 Samba-3 以针对 Windows 200x KDC 进行 Kerberos 认证的粗略指南。假设读者熟悉 Kerberos。

#### 6.4.1 配置 smb.conf

您必须在 `smb.conf` 中至少使用以下三个选项：

```
realm = your.kerberos.REALM
security = ADS
# 以下参数仅在存在时需要指定。
# 如果不存在，默认设置为 Yes。
encrypt passwords = yes
```

如果 Samba 无法使用 realm 名称正确识别合适的 ADS 服务器，请在 `smb.conf` 中使用 `password server` 选项：

```
password server = your.kerberos.server
```

Samba 可能无法定位 ADS 域控制器的最常见原因是，站点在 UNIX 系统上维护某些 DNS 服务器时，未考虑 ADS 基础设施对 DNS 的要求。使用 `password server` 指定首选的 ADS 域控制器并无害处。

> **注意**
>
> 您*不需要*`smbpasswd` 文件，旧版客户端将像 *security* = *domain* 那样进行认证，尽管这样做无害，并且允许您拥有不在域中的本地用户。

#### 6.4.2 配置 /etc/krb5.conf

对于 MIT 和 Heimdal Kerberos，配置 `/etc/krb5.conf` 是不必要的，甚至可能有害。

Microsoft ADS 自动在 DNS 区域 `*.kerberos._tcp.REALM.NAME` 中为 realm 中的每个 KDC 创建 SRV 记录。这是创建 Active Directory 域的 installation 和 configuration 过程的一部分。KDC 是 Kerberos 密钥分发中心，是 Microsoft Active Directory 基础设施的重要组成部分。

UNIX 系统可以使用 init 以及 DES-CBC-MD5 或 DES-CBC-CRC 加密类型来对 Windows 2000 KDC 进行认证。有关 Windows 2000 ADS Kerberos 互操作性的更多信息，请参阅 Microsoft Windows 2000 Kerberos Interoperability<sup>3</sup> 指南。另一个非常有用且可供参考关于 Kerberos 互操作性一般信息的文档是 RFC 1510<sup>4</sup>。该 RFC 解释了 Kerberos 操作背后的许多机制。

MIT 和 Heimdal 最近的 KRB5 库默认会检查 SRV 记录，因此它们会自动找到 KDC。此外，`krb5.conf` 仅允许指定单个 KDC，即使可能存在多个。使用 DNS 查找允许 KRB5 库使用可用的任何 KDC。

手动配置 `krb5.conf` 时，最小配置为：

```
[libdefaults]
    default_realm = YOUR.KERBEROS.REALM
[realms]
    YOUR.KERBEROS.REALM = {
        kdc = your.kerberos.server
    }
[domain_realms]
    .kerberos.server = YOUR.KERBEROS.REALM
```

当使用 0.6 之前的 Heimdal 版本时，请使用以下配置设置：

<sup>3</sup> [http://www.microsoft.com/window2000/techinfo/planning/security/kerbsteps.asp](http://www.microsoft.com/window2000/techinfo/planning/security/kerbsteps.asp)

<sup>4</sup> [http://www.ietf.org/rfc/rfc1510.txt?number=1510](http://www.ietf.org/rfc/rfc1510.txt?number=1510)
