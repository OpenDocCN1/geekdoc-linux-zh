

最后，以与 NT 服务器向 PDC 认证相同的方式进行操作意味着，作为认证回复的一部分，Samba 服务器会获取用户标识信息，例如用户 SID、用户所属的 NT 组列表等。

> **注意**
> 本文档中的许多内容最初发布在 Web 杂志《*LinuxWorld*》上，文章标题为*《执行 NIS/NT Samba》*（链接：`<http://www.linuxworld.com/linuxworld/lw-1998-10/lw-10-samba.html>`）。

## 6.4 Samba ADS 域成员资格

这是关于设置 Samba-3 以针对 Windows 200x KDC 进行 Kerberos 认证的粗略指南。假设读者熟悉 Kerberos。

### 6.4.1 配置 smb.conf

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
> 您*不需要*smbpasswd 文件，旧版客户端将像 *security* = *domain* 那样进行认证，尽管这样做无害，并且允许您拥有不在域中的本地用户。

### 6.4.2 配置 /etc/krb5.conf

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

```
[libdefaults]
    d_default_realm            = YOUR.KERBEROS.REALM
    d_default_etypes           = des-cbc-crc des-cbc-md5
    d_default_etypes_des      = des-cbc-crc des-cbc-md5

[realms]
    YOUR.KERBEROS.REALM = {
        kdc = your.kerberos.server
    }

[domain_realms]
    .kerberos.server = YOUR.KERBEROS.REALM
```

通过执行 `kinit` `USERNAME@REALM` 并确保您的密码被 Win2000 KDC 接受，来测试您的配置。

在使用早于 0.6.x 的 Heimdal 版本时，您只能使用 ADS 中新创建的帐户，或者在迁移后更改过一次密码的帐户，或者在**管理员**安装后的帐户。目前，Windows 2003 KDC 只能与晚于 0.6 版本的 Heimdal 发行版一起使用（且 krb5.conf 中无默认 etypes）。不幸的是，这个领域仍处于动荡之中。

> **注意**
>
> Realm 必须为大写，否则您会得到 "Cannot find KDC for requested realm while getting initial credentials"（无法找到请求 realm 的 KDC 以获取初始凭据）错误（Kerberos 区分大小写！）。

> **注意**
>
> 两个服务器之间的时间必须同步。如果时间差（时钟偏移）超过五分钟，您会得到 "kinit(v5): Clock skew too great while getting initial credentials" 错误。

Kerberos 协议中可以配置时钟偏移限制。默认设置是五分钟。

您还必须确保可以对 KDC 的 IP 地址进行反向 DNS 查找。此外，该反向查找映射的名称必须是 KDC 的 NetBIOS 名称（即不带域的 hostname），或者是跟随 realm 的 NetBIOS 名称。

确保做对的最简单方法是在 `/etc/hosts` 中添加一条条目，将 KDC 的 IP 地址映射到其 NetBIOS 名称。如果未正确设置，尝试加入 realm 时会出现本地错误。

如果您只需要 smbclient 的 Kerberos 支持，那么您可以直接跳到第 6.4.5 节。第 6.4.3 节和第 6.4.4 节仅在您需要 smbd 和 winbindd 的 Kerberos 支持时才需要。

### 6.4.3 创建计算机帐户

作为对 Samba private 目录具有写权限的用户（通常是 root），运行：

```
root# net ads join -U Administrator%password
```

管理员帐户可以是任何在 ADS 域安全设置中被指定有权将机器添加到 ADS 域的帐户。当然，使用除 Administrator 以外的帐户是个好主意。在 UNIX/Linux 系统中，此命令必须由具有 UID=0（root）的帐户执行。

在复杂的组织中，当使 Windows 客户端成为 ADS 域成员时，您可能希望在特定的组织单元内创建机器信任帐户。Samba-3 允许使用以下语法完成此操作：

```
root# kinit Administrator@your.kerberos.REALM
root# net ads join "organizational_unit"
```

您的 ADS 管理员能够建议应该为 “organizational_unit” 参数指定什么。

例如，您可能希望在组织目录 “Computers\BusinessUnit\Department” 下名为 “Servers” 的容器中创建机器信任帐户，如下所示：

```
root# net ads join "Computers\BusinessUnit\Department\Servers"
```

此命令将把 Samba 服务器机器信任帐户放置在容器 `Computers\BusinessUnit\Department\Servers` 中。在执行此命令之前，该容器必须存在于 ADS 目录中。

#### 6.4.3.1 可能的错误

- ADS 支持未编译。必须在安装 Kerberos 库和头文件后重新配置（移除 config.cache）并重新编译 Samba（`make clean all install`）。
- `net ads join` 提示输入用户名。您需要使用 `kinit USERNAME@REALM` 登录到域。USERNAME 必须是拥有将机器添加到域权限的用户。
- 不支持的加密或校验和类型。确保 `/etc/krb5.conf` 已根据系统上安装的 Kerberos 类型和版本正确配置。

### 6.4.4 测试服务器设置

如果加入成功，您将在 Active Directory 中看到一个带有 Samba 服务器 NetBIOS 名称的新计算机帐户（在“Users and Computers”下的“Computers”文件夹中）。

在 Windows 2000 客户端上，尝试 `net use \\server\share`。您应该通过 Kerberos 登录，而无需知道密码。如果失败，请运行 `klist tickets`。您是否获得了服务器的票据？它的加密类型是否为 DES-CBC-MD5？

> **注意**
>
> Samba 可以同时使用 DES-CBC-MD5 加密和 ARCFOUR-HMAC-MD5 编码。

### 6.4.5 使用 smbclient 测试

在您的 Samba 服务器上，尝试使用 smbclient 和 Kerberos 登录到 Windows 2000 服务器或您的 Samba 服务器。像往常一样使用 `smbclient`，但指定 `-k` 选项来选择 Kerberos 认证。

### 6.4.6 备注

安装域控制器后，您必须至少更改一次管理员密码，以创建正确的加密类型。

