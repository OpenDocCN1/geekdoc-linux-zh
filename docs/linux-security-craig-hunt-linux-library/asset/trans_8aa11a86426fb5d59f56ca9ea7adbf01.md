

我建议您使用以下选项调用 `telnet`：

`telnet -a valid`

该命令强制远程用户在移交到 `login` 程序进行交互式访问之前提供适当的 Kerberos 身份验证。

**kshd** `kshd` 守护进程是 Linux 标准自带的 `rshd` 远程 Shell 服务器的 Kerberized（Kerberos 支持）版本。表 13.4 列出了调用 `kshd` 命令时可用的选项。

表 13.4 Kerberos kshd 守护进程命令行选项

| 选项 | 含义 |
|---|---|
| -A | 不为 stderr 连接分配保留端口。 |
| -C | 要求客户端在初始认证器中提供初始连接信息的密码校验和，例如客户端试图访问的用户名。 |
| -e | 要求客户端支持加密。 |
| -M realm | 指定要使用的 Kerberos 域。（默认值是 /etc/krb5.conf 中 default_realm 变量的值。） |

我建议您使用以下选项调用 `kshd`：

`kshd -e -c`

该命令通过加密所有交换的数据包来确保连接的私密性。此外，`-c` 选项可以防止攻击者更改初始连接信息。

**klogind** 表 13.5 列出了 rlogind 的 Kerberos 实现（klogind）特有的选项。

表 13.5 Kerberos klogind 守护进程命令行选项

| 选项 | 含义 |
|---|---|
| -A | 不为 *stderr* 连接分配保留端口。 |
| -C | 要求客户端在初始认证器中提供初始连接信息的密码校验和，例如客户端试图访问的用户名。 |
| -e | 要求客户端支持加密。 |
| -P | 始终提示用户输入密码。 |
| -p | 如果 Kerberos 身份验证未成功，则提示输入密码。 |
| -M realm | 指定要使用的 Kerberos 域。（默认值是 */etc/krb5.conf* 中 *default\_realm* 变量的值。） |

我建议您使用与 *kshd* 相同的选项调用 *klogind*：

`klogind -e -c`

不要使用 -P 或 -p 选项。Kerberos 身份验证应该是此服务唯一的身份验证模式。

## 管理 Kerberos 凭据

非特权用户通过与 Kerberos 系统交互来管理用于请求网络服务的 Kerberos 票据。有四个命令用于此目的：

- **klist** klist 命令显示您当前持有的 Kerberos 票据列表。票据信息保存在 /tmp/krb5cc_XXX 文件中，其中 XX 是您在 Linux 服务器上的 UID。
- **kinit** kinit 命令从 KDC 请求票据授予票据，并将其保存在 /tmp/krb5cc_XXX 文件中，以便由 klist 命令检查。
- **kdestroy** kdestroy 命令删除您当前持有的任何 Kerberos 票据。
- **kpasswd** kpasswd 命令更改您当前的 Kerberos 密码（该密码保护与您主体关联的主密钥）。

清单 13.9 包含一个示例，展示了用户获取和显示 Kerberos 票据授予票据的过程。

### 清单 13.9 使用 klist 获取和显示 TGT

```
[ramon] $ klist
klist: No credentials cache file found (ticket cache FILE:/tmp/krb5cc_500)

Kerberos 4 ticket cache: /tmp/tkt500
klist: You have no tickets cached
[ramon] $ kinit
Password for ramon@HONTANON.COM:
[ramon] $ klist
Ticket cache: FILE:/tmp/krb5cc_500
 Default principal: ramon@HONTANON.COM


    Valid starting        Expires          Service principal
    02/24/01 17:50:05     02/25/01 03:49:52     krbtgt/HONTANON.COM@HONTANON.COM


Kerberos 4 ticket cache: /tmp/tkt500
klist: You have no tickets cached
```

用户 ramon 使用 klist 命令显示其凭据，但他目前还没有任何凭据。然后他运行 kinit 并获取了一个 TGT，但他只有在提供了保护其主体主密钥的密码后才能获得。再次调用 klist 命令发现，用户名 ramon 现在在其凭据缓存中有一个 TGT。

> **NOTE** 请注意，klist 命令同时报告版本 5 和版本 4 的票据。这是因为标准 RPM Kerberos 软件包包含对较旧的 Kerberos v4 协议的支持。

默认情况下，kinit 命令试图获取主体 user@REALM 的 TGT，其中 user 是请求票据的用户名，REALM 是 `/etc/krb5.conf` 文件中 default_real 变量的值。要获取其他主体的票据，请在命令行上指定主体名称，如下例所示：

```
[ramon]$ kinit alice@SYBEX.COM
```

`klist` 命令显示您刚获取的票据有效期至 2001 年 2 月 25 日凌晨 3:39（从现在起 10 小时）。如果您想丢弃此票据，请使用 `kdestroy` 命令从缓存中删除它（参见清单 13.10）。

### 清单 13.10 使用 `kdestroy` 从缓存中删除票据

```
[ramon]$ kdestroy
[ramon]$ klist
klist: No credentials cache file found (ticket cache FILE:/tmp/krb5cc_500)

Kerberos 4 ticket cache: /tmp/tkt500
klist: You have no tickets cached
```

最后，非特权成员应定期使用 `kpasswd` 命令更改其 Kerberos 密码，以最大程度地减少其暴露风险。如清单 13.11 所示，使用 `kpasswd` 实用程序与使用标准 Linux `passwd` 命令几乎相同。

### 清单 13.11 使用 `kpasswd` 更改 Kerberos 密码

```
[ramon]$ kpasswd
kpasswd: No credentials cache file found getting principal from: cache
[ramon]$ kinit
Password for ramon@HONTANON.COM:
[ramon]$ kpasswd
Password for ramon@HONTANON.COM:
Enter new password:
Enter it again:
Password changed.
```

请注意，为了发出 `kpasswd` 命令，您需要拥有一个未过期的 TGT。这是合理的，因为您需要此 TGT 来向 KDC 证明是您正在发出 `kpasswd` 命令，并且您需要 TGT 来在传输过程中加密新密码。

> **WARNING** 选择一个良好的密码并定期更改它极其重要。与您的标准 Linux 密码不同，Kerberos 密码可用于获取访问其他服务的票据，以代表您进行操作，因此入侵造成的潜在损害要大得多。

## 使用 Kerberos 允许他人访问您的账户

授予账户临时访问权限是 Linux 服务器上 Kerberos 身份验证最有用的功能之一。通过在您的主目录中创建 .k5login 文件，您可以授予其他用户临时访问权限，而无需提供您的密码。相反，只需将他们的主体名称（每行一个）添加到 .k5login 文件中以允许他们访问，如下例所示：

```
[ramon]$ more .k5login
alice@HONTANON.COM
bob@SYBEX.COM
```

如果 Alice 或 Bob 成功获取了其主体的票据，他们将允许登录到您的账户。此功能还可以通过在 /.k5login 中简单输入其主体名称来授予非特权用户临时的 root 访问权限（假设您的 root 用户主目录为 /）。这既避免了泄露 root 密码，也避免了在网络上暴露密码。

## 使用启用 Kerberos 的应用程序

一旦用户拥有 TGT，他们就可以使用多种 Kerberized 应用程序访问远程服务，而无需向每个服务进行身份验证。Linux Kerberos 发行版附带修改版的最受欢迎的网络客户端：telnet、ftp、rlogin、rsh 和 rcp。让我们看看这些应用程序在 Kerberos 中的用法。

### telnet

Kerberos 使用表 13.6 中列出的命令行选项扩展了标准 Linux 命令。

表 13.6 Kerberos telnet 客户端命令行选项

| 选项 | 含义 |
|---|---|
| -k realm | 请求指定 realm 以外的票据，该 realm 由 */etc/krb5.conf* 文件中的 *default_realm* 变量指定。 |
| -K | 进行身份验证但不登录。 |
| -a | 使用您的凭据和本地用户名执行自动登录（客户端不会提示输入用户名）。 |
| -x | 启用加密。 |

