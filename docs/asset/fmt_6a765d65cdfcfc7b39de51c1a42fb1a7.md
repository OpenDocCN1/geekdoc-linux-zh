
```
newbie@SAMPLE.COM's Password: <type password>
kadmin add -r host/machine.com
Max ticket life [1 day]:n
Max renewable life [1 week]:n
Principal expiration time [never]:n
Password expiration time [never]:n
Attributes []:
```

不是为新主体设置密码，而是 `-r` 标志告诉 `kadmin` 生成一个随机密钥。在这里使用它是是因为此操作不需要用户交互。这是机器的服务器账户。

最后，提取密钥并将其存储在本地 keytab 文件 `/etc/krb5.keytab` 中。此文件由超级用户所有，你必须是 root 才能执行下一个命令：

```
ktutil get host/machine.sample.com
```

完成后，确保使用 `kdestroy` 破坏获得的管理员票据。

# 18.4.9 为 Kerberos 启用 PAM 支持

SUSE LINUX 使用一个名为 `pam_krb5` 的 PAM 模块，它支持 Kerberos 登录和密码更新。该模块可以被应用程序、控制台登录、`su` 以及 KDM 等图形应用程序使用，在这些情况下用户提供密码并希望身份验证代表其获取初始 Kerberos 票据。

`pam_unix` 模块也支持 Kerberos 身份验证和密码更新。要在 `pam_unix` 中启用 Kerberos 支持，编辑文件 `/etc/security/pam_unix2.conf`：

```
auth required pam_krb5.so
account required pam_krb5.so
password required pam_krb5.so
session required pam_krb5.so
```

原文为：`To enable Kerberos support in pam_unix, edit the file /etc/security/pam_unix2.conf.`

译文：要在 `pam_unix` 中启用 Kerberos 支持，编辑文件 `/etc/security/pam_unix2.conf`。

# 18.4.10 配置 SSH 使用 Kerberos

OpenSSH 支持版本 1 和 2 的 Kerberos 身份验证。在版本 1 中，存在特殊的协议。版本 2 不直接使用 Kerberos，而是依赖 GSSAPI（通用安全服务 API）。要在 `sshd` 使用 Kerberos，编辑 `/etc/ssh/sshd_config` 并设置以下选项：

```
# 这些用于版本 1
KerberosAuthentication yes
KerberosTgt yes
# 这些用于版本 2
GSSAPIAuthentication yes
GSSAPIKeyExchange yes
```

然后重启你的 ssh 守护进程。要在版本 2 使用 Kerberos，在客户端也启用它。可以在系统级配置文件 `/etc/ssh/config` 中，也可以通过编辑 `~/.ssh/config` 在用户级别进行。在两种情况下，添加选项 `GSSAPI yes`。

你现在应该能够使用 Kerberos 连接了。使用 `klist` 验证你有有效的票据，然后连接到 SSH 服务器。要强制使用 SSH 版本 1，在命令行上指定 `-1`。

# 11 使用 LDAP 和 Kerberos

使用 Kerberos 时，在本地网络分发用户信息（如用户 ID、组、主目录等）的方法之一是使用 LDAP。这需要一种防止欺骗和其他攻击的强身份验证机制。一种解决方案是对 LDAP 也使用 Kerberos。

OpenLDAP 通过 SASL 实现大部分认证类型。SASL 基本上是一种为身份验证设计的网络协议。SUSE Linux 使用的 SASL 实现是 `cyrus-sasl`，它支持多种认证因子。Kerberos 身份验证通过 GSSAPI（通用安全服务 API）执行。默认情况下没有安装 GSSAPI 的 SASL 插件。使用 `rpm -ivh cyrus-sasl-gssapi-*` 手动安装。

要启用绑定到 OpenLDAP，创建一个主体 `ldap/earth.sample.com` 并将其添加到 keytab：

```
kadd -r ldap/earth.sample.com
ktutil get ldap/earth.sample.com
```

默认情况下，LDAP 服务器以用户 `ld` 组运行，而 keytab 文件由 root 所有。因此，更改 LDAP 配置使服务器以 root 运行，或者让 keytab 文件对 `ld` 组可读。

要让 `slapd` 以 root 运行，编辑 `/etc/sysconfig/openldap`。通过在它们前面注释禁用 `OPENLDAP_USER` 和 `OPENLDAP_GROUP` 变量。

要让 keytab 文件对 `ld` 组可读，执行：

```
chgrp ldap /etc/krb5.keytab
chmod 640 /etc/krb5.keytab
```

这两种解决方案都不是完美的。然而，目前无法配置 OpenLDAP 使其使用独立的 keytab 文件。最后，使用 `rcld restart` 重启 LDAP 服务器。

# 18.4.7 远程 Kerberos 管理

为了能够在不直接访问 KDC 控制台的情况下从 Kerberos 数据库中添加和删除主体，请告诉 Kerberos 管理服务器哪些主体允许执行什么操作。可以通过编辑文件 `/var/heimdal/kadmin.acl`（ACL 是访问控制列表的缩写）来实现。ACL 文件允许你通过精细的控制指定权限。详细信息，请参阅 `man kadmin` 手页。

现在，只需向文件中添加以下行，授予你自己对数据库进行任何操作的权限：

```
newbie/admin             all
```

将用户名 `newbie` 替换为你自己的用户名。重启 KDC 以使更改生效。

## 使用 kadmin 进行远程管理

你现在应该能够使用 `kadmin` 工具远程执行 Kerberos 管理任务。首先，获取你管理员角色的票据，并在连接到 kadmin 服务器时使用该票据：

```
kinit newbie/admin
newbie/admin@SAMPLE.COM's Password: <enter password>
/usr/bin/kadmin
kadmin> privs
change-password, list, delete, add, get
```

使用 `privs` 命令验证你拥有哪些权限。上面显示的列表是权限的全集。

例如，修改主体 `newbie`：

```
kadmin> mod newbie

Max ticket life [1 day]:2 days
Max renewable life [1 week]
Principal expiration time [never]:2005-01-01
Password expiration time [never]:n
Attributes []
```

这会将最大票据有效期更改为两天，并将账户过期日期设置为 2005 年 1 月 1 日。

## 基础 kadmin 命令
