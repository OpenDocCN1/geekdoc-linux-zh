

在主 smb.conf 文件中。仅使用 TCP 端口 139 通过 TCP/IP 使用 NetBIOS 意味着 `%L` 宏完全启用。如果未指定 smb ports = 139（默认值为 445 139），或者此参数的值设置为 139 445，则 `%L` 宏不可用。

可以托管多个服务器，每个服务器都有自己的人格，使用端口 445（无 NetBIOS 的 SMB 端口），在这种情况下，可以使用 `%U` 宏来提供独立的服务器标识（通过 IP 地址）。每个服务器都可以有自己独特的安全模式。除了 netbios name 参数外，还需要使用 interfaces、bind interfaces only 和 IP 别名来创建虚拟服务器。与仅使用 TCP 端口 139 的 NetBIOS 名称相比，此方法要复杂得多。

考虑一个示例环境，该环境由一个独立的用户模式安全 Samba 服务器和一个必须替换的只读 Windows 95 文件服务器组成。可以用一种方式替代将 Windows 95 机器替换为新的 PC，即将该服务器添加为一个在 Samba 服务器上托管的只读匿名文件服务器。以下是一些参数：

Samba 服务器称为 ELASTIC，其工作组名称为 ROBINSMEST。CDROM 服务器称为 CDSERVER，其工作组为 ARTSDEPT。此处展示了一种可能的实现方式：

主服务器的 smb.conf 文件如示例 33.1.1 所示。此文件放置在 /etc/samba 目录中。只需要 nmbd 和 smbd 守护进程。当服务器启动时，它将在 Windows 网络邻居中显示为工作组 ROBINSMEST 下的机器 ELASTIC。如果必须访问此服务器的 Windows 客户端也在工作组 ROBINSMEST 中，这将使浏览更加可靠，因此这很有帮助。

CDROM 服务器的配置文件列在示例 33.1.2 中。此文件名为 smb-cdserver.conf，应位于 /etc/samba 目录中。位于工作组 ARTSDEPT 中的机器可以自由浏览此服务器。

这两个服务器具有不同的资源，并位于不同的工作组中。只能由主机系统上拥有相应帐户的用户访问服务器 ELASTIC。所有用户都可以访问存储在 /export/cddata 目录中的 CDROM 数据。应设置文件系统权限，使其他用户对目录及其内容具有只读访问权限。文件可以由 root 拥有（任何除 nobody 账户外的用户）。

### 33.1.3 多个虚拟服务器托管

在此示例中，要求为名为 MIDEARTH 的域提供主要的域控制器。PDC 将称为 MERLIN。需要一台名为 SAURON 的额外机器。每台机器仅拥有自己的共享。两台机器都属于同一个域/工作组。

主 smb.conf 文件如示例 33.1.3 所示。指定每个服务器共享信息的两个文件如示例 33.1.4 和示例 33.1.5 所示。所有三个文件都位于 /etc/samba 目录中。

#### 示例 33.1.1 Elastic smb.conf 文件

```text
# Global parameters
[global]
    workgroup = ROBINNEST
    netbios name = ELASTIC
    netbios aliases = CDSERVER
    smb ports = 139
    printcap name = cups
    disable spoolss = Yes
    show add printer wizard = No
    printing = cups
    include = /etc/samba/smb-%L.conf

[homes]
    comment = Home Directories
    valid users = %S
    read only = No
    browseable = No

[office]
    comment = Data
    path = /data
    read only = No

[printers]
    comment = All Printers
    path = /var/spool/samba
    create mask = 0600
    guest ok = Yes
    printable = Yes
    use client driver = Yes
    browseable = No
```

#### 示例 33.1.2 CDROM 服务器 smb-cdserver.conf 文件

```text
# Global parameters
[global]
    workgroup = ARTSDEPT
    netbios name = CDSERVER
    map to guest = Bad User
    guest ok = Yes

[carousel]
    comment = CDROM Share
    path = /export/cddata
    read only = Yes
    guest ok = Yes
```

#### 示例 33.1.3 主 smb.conf 文件的全局部分

```text
# Global parameters
[global]
    workgroup = MIDEARTH
    netbios name = MERLIN
    netbios aliases = SAURON
    passdb backend = tdbsam
    smb ports = 139
    syslog = 0
    printcap name = CUPS
    show add printer wizard = No
    add user script = /usr/sbin/useradd -m '%u'
    delete user script = /usr/sbin/userdel -r '%u'
    add group script = /usr/sbin/groupadd '%g'
    delete group script = /usr/sbin/groupdel '%g'
    add user to group script = /usr/sbin/usermod -G '%g' '%u'
    add machine script = /usr/sbin/useradd -s /bin/false -d /var/lib/nobody '%u'
    logon script = scripts\login.bat
    logon path =
    logon drive = X:
    domain logons = Yes
    preferred master = Yes
    wins support = Yes
    printing = CUPS
    include = /etc/samba/smb-%L.conf
```

#### 示例 33.1.4 MERLIN smb-merlin.conf 文件的共享部分

```text
# Global parameters
[global]
    workgroup = MIDEARTH
    netbios name = MERLIN

[homes]
    comment = Home Directories
    valid users = %S
    read only = No
    browseable = No

[office]
    comment = Data
    path = /data
    read only = No

[netlogon]
    comment = NETLOGON
    path = /var/lib/samba/netlogon
    read only = Yes
    browseable = No

[printers]
    comment = All Printers
    path = /var/spool/samba
    printable = Yes
    use client driver = Yes
    browseable = No
```

#### 示例 33.1.5 SAURON smb-sauron.conf 文件的共享部分

```text
# Global parameters
[global]
    workgroup = MIDEARTH
    netbios name = SAURON

[www]
    comment = Web Pages
    path = /srv/www/btdocs
    read only = No
```

# 第四部分
迁移与更新

## 从 SAMBA-2.X 升级到 SAMBA-3.0.20

本章专门讨论 Samba-3.0.20 和 Samba-2.2.8a 之间的差异。它指出了配置参数发生变化的地方，并提供了从 2.2.x 迁移到 3.0.20 的简单指南。

### 34.1 快速迁移指南

Samba-3.0.20 的默认行为应与 Samba-2.2.x 大致相同。当新参数 `passdb backend` 未在 `smb.conf` 文件中定义时，默认行为与 Samba-2.2.x 使用 `encrypt passwords = Yes` 时的默认行为相同，并将使用 `smpassw` 数据库。

那么，为什么说*行为应与 Samba-2.2.x 大致相同*？因为 Samba-3.0.20 可以协商新协议，例如对原生 Unicode 的支持，这可能导致采取不同的协议代码路径。在此类情况下，新行为与旧行为不完全相同。好消息是，域和机器 SID 在升级过程中将得到保留。

如果 Samba-2.2.x 系统使用的是 LDAP 后端，并且没有时间更新 LDAP 数据库，请确保在 `smb.conf` 文件中指定了 `passdb backend = ldapsam_compat`。对于其余部分，行为应大致保持不变。稍后，当有时间实现新的 Samba-3 兼容的 LDAP 后端时，可以通过使用 `pdbedit` 将旧的 LDAP 数据库迁移到新的数据库。参见第 10.3.2 节。

### 34.2 Samba-3 中的新功能

主要新功能包括：

- Active Directory 支持。此版本可以作为成员服务器加入 ADS 域，并使用 LDAP/Kerberos 对用户进行身份验证。
- Unicode 支持。Samba 现在将在线协商 Unicode，并且内部为多字节和 Unicode 字符集提供了更好的基础设施。
- 新的身份验证系统。内部身份验证系统几乎完全重写。大多数更改是内部更改，但新的授权系统也具有很高的可配置性。
- 新的文件名转换系统。文件名转换系统已完全重写。内部数据库现在持久地存储转换映射。
- 新的 `net` 命令。添加了一个新的 `net` 命令。它与 Windows 中的 `net` 命令有些相似。最终，我们计划用 `net` 的子命令替换一批其他实用工具（例如 `smbpasswd`）。
- Samba 现在在线协商 NT 样式的 status32 代码。这大大改善了错误处理。
- 改进的 Windows 2000/XP 打印支持，包括在 Active Directory 中发布打印机属性。
- 用于 passdb 后端和字符集的新可加载 RPC 模块。
- 改进的双守护进程 winbindd 支持的新默认设置，以提高性能。
- 支持从 Windows NT 4.0 域迁移到 Samba 域，并保留用户、组和域 SID。
- 支持与 Windows NT 4.0 域控制器建立信任关系。
- 对使用 LDAP 目录存储 SID 到 UID/GID 映射的分布式 Winbind 架构的初步支持。
- 对 Samba 文档树的重大更新。
- 完全支持客户端和服务器 SMB 签名，以确保与默认 Windows 2003 安全设置的兼容性。
- 还有许多其他改进！

### 34.3 配置参数变更

本节简要列出了 3.0.20 版本中 `smb.conf` 选项的变更。有关新增或修改参数的完整描述，请参阅 `smb.conf(5)` man 页面。

#### 34.3.1 已移除的参数

按字母顺序，这些是在发布 Samba 3.0.20 之前，Samba 3.0.0 系列期间移除的参数。

- admin log
- alternate permissions

