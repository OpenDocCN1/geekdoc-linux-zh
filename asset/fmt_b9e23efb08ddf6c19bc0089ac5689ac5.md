
- 仅安装支持 DNS 服务器、DHCP 服务器和邮件服务器的必要应用程序和进程。
- 选择 `root` 密码。
- 选择 LDAP 认证。
- 创建两个额外的普通用户。
- 安装后，使用 `DA1` 更新系统。
- 安全 GRUB 引导程序。
- 手动配置网络连接（使用或使用 `YaST`）。
- 将运行级别 3 设置为默认。
- 使用 NTP 同步系统时。

仔细阅读这些要求，然后配置服务器。

# 目标 2 配置 DNS 服务器

Digital Airlines 迁移 Linux 的一个里程碑是实施基于 Linux 的 DNS。作为第一步，你决定在实验室设置测试 DNS 服务器。

在实验室的 SUSE Linux 测试服务器上，执行以下操作：

- 为 5 个测试系统配置主 DNS 服务器。
- 测试你的设置（你可以使用 `dig` 命令）。
- 与另一位学习相同场景的同学一起配置配置服务器作为彼此的从 DNS 服务器。

# 目标 3 配置 DHCP 服务器

网络上的大多数工作站都有静态 IP 地址。但有一小部分笔记本电脑。这些笔记本应该通过 DHCP 获取 IP 地址。

在实验室的 SUSE Linux 测试服务器上，执行以下操作：

- 安装 DHCP 服务器。
- `10.0.0.180` 到 `10.0.0.200` 留给 DHCP。
- DNS 和网关信息应由 DHCP 交付。

# 目标 4 配置邮件服务器

你的 Digital Airlines 办公室运行着内部邮件服务器。该服务器也需要迁移到 SUSE Linux Enterprise Server 10。

在实验室的 SUSE Linux 测试服务器上，执行以下操作：

- 发送给 `digitalairirlines.com` 域名以外用户的邮件应转发到 IP 为 `135.195.220.3` 的提供商邮件服务器。
- 从邮件地址中删除主机前缀。
- 所有从 `194.95.93.10` 发送的邮件都应被拒绝。
- 发送到 `info@digitalairirlines.com` 地址的邮件应发送给用户 `PSmith`。
- 用户 `PSmith` 应该获得所有发送给用户 `root` 的系统通知的副本。
- 垃圾邮件的主主题中应标记为“***spam***”。
- 所有病毒邮件都应发送给用户“virusadmin”，而不是邮件邮件收件人。
- 所有用户都可以使用 POP 访问自己的邮箱。
- 发送给用户 `PSmith` 的邮件应自动分类到三个不同的邮箱中：
  - 发送到 `info@digitalairirlines.com` 的邮件应存储在邮箱“info.”中。
  - 发送到 `root` 的邮件应存储在邮箱“root.”中。
  - 发送到 `psmith@digitalairirlines.com` 的邮件应存储在邮箱“inbox.”中。

# 目标 5 监控网络

使用 Nagios 监控你的 SUSE Linux Enterprise Server 10 上的网络服务。

在实验室的 SUSE Linux 测试服务器上，执行以下操作：

- 定义主机组“linux-servers”。
- 你的测试服务器是“linux-servers”组的唯一成员。
- 应该监控以下服务：
  - DNS
  - DHCP
  - Mail
- 配置 Nagios Web 服务器。

# 附录 B 结合 Samba 和 OpenLDAP

Samba 经常与 OpenLDAP 结合，因为它允许你为 Windows 构建备份域控制器 (BDC)。因此，使用了 OpenLDAP 的复制机制。

本附录涵盖了以下主题：

- 准备 OpenLDAP 目录
- 理解 Samba 的 LDAP 选项

## 目标 1 准备 OpenLDAP 目录

如果你想从 Samba 访问 LDAP 目录服务，你必须修改 LDAP 安装的 `/etc/openldap/slapd.conf` 文件。执行以下操作：

1. 包含 Samba3 的架构文件。

| include | path |
| :--- | :--- |
| `/etc/openldap/schema/samba3.schema` | |

2. 在访问语句中允许 Samba 访问 LDAP。

它看起来像如下：

```
access to attrs=userpassword,sambaNTPassword,sambaLMPassword
by self write
by anonymous auth
by * none
```

在这个示例中，所有人都被允许使用不同类型的密码进行身份验证。这些密码只能由所有者更改。

所有人都可以读取所有属性。

3. 确保选项 `suffix`、`rootdn` 和 `rootpw` 设置正确。
4. 检查 `/etc/ldap.conf` 文件中的 `base` 选项。

## 5. 索引部分可能如下所示：

| index | operator | value |
| :--- | :--- | :--- |
| `index objectClass` | `eq` | |
| `index cn` | `pres,sub,eq` | |
| `index sn` | `pres,sub,eq` | |
| `index uid` | `pres,sub,eq` | |
| `index displayName` | `pres,sub,eq` | |
| `index uidnNumber` | `eq` | |
| `index gdnNumber` | `eq` | |
| `index memberUid` | `eq` | |
| `index sambaSId` | `eq` | |
| `index sambaPrimaryGroupSID` | `eq` | |
| `index sambaDomainName` | `eq` | |
| `index default` | `sub` | |

## 目标 2 理解 Samba 的 LDAP 选项

Samba 提供了一些配置选项来与 LDAP 通信。

最重要的是以下：

在这里，你可以输入以下内容之一：

- `smbpasswd`
- `tdbsam (smbpasswd plus NT SAM)`
- `ldapsam`

如果你的网络中有备份域控制器 (BDC)，在此处选择 `Ldapsam`。`mysqlam` 和 `xmlams` 也是可能的选项，但不适用于主域控制器 (PDCs)。

- `Ldap admin dn`。指定 Samba 用于检索用户信息的 LDAP 区分名称。
- `Ldap delete dn`。如果此选项设置为 `yes`，删除操作将删除整个 LDAP 条目。否则，只删除特定于 Samba 的属性。
- `Ldap group suffix`。当组被添加到 LDAP 目录时，Samba 使用此后缀来处理组。
- `Ldap idmap suffix`。指定在存储 imap 映射时使用的后缀。
- `Ldap machine suffix`。指定应将工作站添加到 LDAP 目录。
- `Ldap passwd sync`。如果此选项设置为 `yes`，Samba 尝试将 LDAP 密码与普通用户的 NT 和 LANManager 哈希进行同步。

如果此选项设置为 `no`，只更新 NT 和 LANManager 密码。如果此选项设置为 `only`，则只更改 LDAP 密码。

- `ldap server`。在此处输入 LDAP 服务器的 FQDN。

# 附录 C 使用 Fetchmail 获取邮件

你可以使用 Fetchmail 获取邮件。

必须安装 `fetchmail` 软件包并在 `~/.fetchrc` 中配置它。

Fetchmail 提供了广泛的定制，例如：

- 邮箱的处理
- 为多个用户获取邮件
- 过滤程序的集成
- 使用 SSL 进行加密传输

要启动 Fetchmail，请使用 `fetchmail` 命令。

此外，该程序有许多启动时可以提供的选项。

默认情况下，Fetchmail 可以由系统上的任何用户运行。这意味着每个用户都可以在其家目录中创建自己的配置。

`root` 用户使用 Fetchmail 定隔集中获取邮件并分发给个人用户。这种方法在 `/etc/fetchmail` 中设置。

系统级 Fetchmail 配置在文件中完成：

```
/etc/fetchmail
```

有关 Fetchmail 的更多信息，请查看程序的帮助页。

信息也可以在 `/usr/share/doc/packages/fetchmail/` 目录下获取。

## 目标 1 配置 Fetchmail

### 理解命令行选项

`~/.fetchmail` 文件中的行具有以下结构：

```
poll servername protocol username "name" password
"password"
```

或者，缩写形式：

```
poll servername proto protocol user "name" pass "password"
```

这种基本形式可以通过添加包含可以转发获取邮件的用户 "local_name" 来扩展。

在以下示例中，该用户是：

```
poll da51.digitalairlines.com proto pop3 user "geeko.chameleon" pass
"SECRET" 是 "geeko"
```

如果查询多个邮件服务器，相同的细节可以使用 `defaults` 指令定义一次，然后省略。

例如：

```
defaults proto pop3 user "geeko.chameleon"
poll da51.digitalairlines.com pass "SECRET"
poll pop3.suse.com pass "CONFIDENTIAL"
```

基本用户选项有：

- `proto[col].` 使用的协议类型（如 `auto`、`pop3` 和 `imap`）。
- `port.` 端口号。
- `timeout.` 在 fetchmail 关闭连接前等待服务器响应的秒数。

## 5. 索引部分如下所示：

| index | operator | value |
| :--- | :--- | :--- |
| `index objectClass` | `eq` | |
| `index cn` | `pres,sub,eq` | |
| `index sn` | `pres,sub,eq` | |
| `index uid` | `pres,sub,eq` | |
| `index displayName` | `pres,sub,eq` | |
| `index uidnNumber` | `eq` | |
