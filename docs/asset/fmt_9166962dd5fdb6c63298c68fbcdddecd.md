
这里是 `kadmin` 命令的简要列表。更多信息，请参阅 `kadmin` 手页。

- - `add principal`: 添加一个新主体

- - `modify principal`: 编辑主体的各种属性，例如最大票据有效期和账户过期日期

- - `delete principal`: 从数据库中删除主体

- - `rename principal [oldname] [newname]`: 将主体重命名为 `newname`

- - `list pattern`: 列出所有匹配给定模式的主体。模式的工作方式类似于 shell 的通配符模式：在我们的示例中，`list newbie*` 将列出 `newbie` 和 `newbie/admin`

- - `get principal`: 显示主体的详细信息

- - `passwd principal`: 更改密码

在某些阶段，输入 `?` 并回车可以获得帮助。这在 `modify` 和 `add` 生成的提示符环境中有效。

初始化领域时使用的 `init` 命令（以及其他几个命令）在远程模式下不可用。要创建一个新领域，请进入 KDC 控制台并在本地模式下 `kadmin`（使用 `-l` 命令行选项）。使用 `dump`、`load` 和 `merge` 命令导出和恢复 KDC 数据库也是如此。

# 18.4.8 创建 Kerberos主机主体

除了确保网络上的每台机器都知道它属于哪个 Kerberos 领域以及应该联系哪个 KDC 之外，还要为它创建一个主机主体。到目前，只讨论了用户凭据。然而，兼容 Kerberos 的服务通常需要对客户端用户进行身份验证。因此，领域中的每个主机在 Kerberos 数据库中必须存在特殊的主体。

主机主体的命名规范为 `/host/hostname@@REALM`，其中 `hostname` 是完全限定主机名。主机主体与用户主体相似，但存在显著差异。用户主体和主机主体之间的主要区别在于，当用户从 KDC 获取票据授予票据时，前者的密钥受密码保护，他需要输入密码以便 Kerberos 能够解密票据。显然，如果系统管理员每隔八小时就要为 SSH 守护进程获取新票据，那将非常不便。

相反，解密主机主体初始票据所需的密钥由管理员从 KDC 提取一次，并存储在名为 `keytab` 的本地文件中。使用 SSH 守护进程的服务读取此密钥，并在需要时自动使用它获取新票据。默认 `keytab` 文件位于 `/etc/krb5.keytab`。

要为 `machine.sample.com` 创建主机主体，请在 `kadmin` 会话期间输入以下命令：

```
kinit newbie/admin
```

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

最后，提取密钥并将其存储在本地 `keytab` 文件 `/etc/krb5.keytab` 中。此文件由超级用户所有，你必须是 `root` 才能执行下一个命令：

```
ktutil get host/machine.sample.com
```

完成后，确保使用 `kdestroy` 破坏获得的管理员票据。

# 18.4.9 为 Kerberos 启用 PAM 支持

SUSE LINUX 使用一个名为 `pam_krb5` 的 PAM 模块，它支持 Kerberos 登录和密码更新。该模块可以被应用程序、控制台登录、`su` 以及 KDM 等图形应用程序使用，在这些情况下用户提供密码并希望身份验证代表其获取初始 Kerberos 票据。

`pam_unix` 模块也支持 Kerberos 身份验证和密码更新。要在 `pam_unix` 中启用 Kerberos 支持，编辑文件 `/etc/security/pam_unix2.conf`。

*(注：此处原文文本在某处似乎有断层或跳跃，我已根据您提供的完整文本进行了整合翻译。)*

## 在 LDAP 中使用 Kerberos 认证

现在你应该能够自动通过 Kerberos 认证使用如 `ldapsearch` 等工具了。

```
ldapsearch -b ou=People,dc=suse,dc=de '(uid=newbie)'
SASL/GSSAPI authentication started
SASL SSF: 56
SASL installing layers
[...

# newbie, People, suse.de
dn: uid=newbie,ou=People,dc=suse,dc=de
uid: newbie
cn: Olaf Kirch
[...]
```

如你所见，`ldapsearch` 打印了一条消息，显示已启动 GSSAPI 认证。下一条消息确实非常晦懂，但它显示“安全强度因子”（SSF）为 56。（简称为值 56）这在某种程度上是随机的。可能选择它是因为它是 DES 加密密钥的位数。这告诉你 GSSAPI 认证已成功，并且正在使用加密来为 LDAP 连接提供完整性保护和机密性。如果有多个可用的 SASL 机制，你可以在命令行中添加 `-Y GSSAPI` 来强制 `ldapsearch` 使用 GSSAPI。

在 Kerberos 中，认证始终是双向的。这意味着不仅是你向 LDAP 服务器验证了身份，LDAP 服务器也向你验证了它的身份。这意味着通信是与目标 LDAP 服务器进行的，而不是攻击者设置的服务器。

## Kerberos 认证与 LDAP 访问控制

现在，允许每个用户修改其 LDAP 用户记录的登录 shell 属性。假设你有一个架构，其中 `joe` 的 LDAP 位于 `uid=joe,ou=people,dc=suse,dc=de`，请在 `/etc/openldap/slapd.conf` 中设置以下访问控制：

```
# 为了让功能正常工作，这是必须
access to dn.base="* by read
# 让每个用户更改其登录 shell
access to dn="*,ou=people,dc=suse,dc=de" attrs=loginShell
by self write
```

## 网络安全

第二条语句赋予了已认证用户对其自己的 LDAP 目的 `loginShell` 属性的写权限。第三条语句赋予了所有已认证用户对整个 LDAP 目录的读权限。

这里缺少了一个小拼图，即 LDAP 服务器如何发现 Kerberos 用户 `joe@SAMPLE.COM` 对应 LDAP 区分名 `uid=joe,ou=people,dc=suse,dc=de`。这种映射必须使用 `saslExpr` 指令手动配置。在我们的示例中，在 `slapd.conf` 中添加以下内容：

```
saslRegex
uid=(.*),cn=GSSAPI,cn=auth
uid=$1,ou=people,dc=example,dc=com
```

要理解其工作原理，你需要知道 SASL 认证用户，OpenLDAP 根据 SASL 提供的名称（如 `joe`）和 SASL 变体名称（GSSAPI）形成一个区分名。结果将是 `uid=joe,cn=GSSAPI,cn=auth`。

如果配置了 `saslRegex`，它将使用第一个参数作为正则表达式检查由 SASL 信息形成的 DN。如果该正则表达式匹配，则名称将被替换为 `saslRegex` 语句的第二个参数。占位符 `$1` 被替换为 `(.*)` 表达式匹配到的子字符串。

可以使用更复杂的匹配表达式。如果你有更复杂的目录结构或用户名不是 DN 部分的架构，你甚至可以使用搜索表达式将 SASL DN 映射到用户 DN。

# 18.5 安全与机密性

### 18.5.1 基本考虑

Linux 或 UNIX 系统的主要特征之一是能够同时处理多个用户（多用户），并允许这些用户在同一台计算机上同时执行多个任务（多任务）。此外，操作系统是网络透明的。用户通常不知道他们使用的数据和应用程序是从本地机器提供的，还是通过网络提供的。由于具有多用户功能，用户的数据必须分开存储。数据安全和隐私需要得到保证。即使在计算机通过网络连接之前，数据安全已经是一个重要问题。与今天一样，最关心的是尽管数据介质丢失或损坏（大多数情况下是硬盘），仍能保持数据的可用性。

本章重点关注机密性和隐私，但也包含了可用性。

### 18.5.2 本地安全与网络安全

有几种方法可以保护数据免受授权的访问：

- 物理访问

- 网络访问

在所有情况下都需要认证。例如，当用户连接到网络时，他们必须证明自己的身份。这通常通过密码完成，但也有其他方法。
