
| 凭据缓存/票据文件 | `/tmp/` 目录下的包含你的 `TGT`、主机和守护密钥的文件。 |

| 密钥表 (Keytab) | Kerberos 客户端上的文件，包含了该服务器可以访问的主机和守护进程的公钥。 |

| 策略 (Policy) | 置在 Kerberos 主体上的特殊限制，决定了票据的有效期。 |

## Kerberos 主体

你已经读过主体由主体、实例和域组成。图 6.10 显示了一个主机主体的示例，它使用了主体所有的三个元素。

### 图 6.10 Kerberos 实体 (Principal)

| 实体 (Principal) | 实例 (Instance) | 域 (Realm) |
|---|---|---|
| 主机 (Primary Host) | `/www/yourcompany.com` | `@YOURCOMPANY.COM` |

以下主机守护实体的示例：

`ftp://www.yourcompany.com@YOURCOMPANY.COM`

该实体识别 `www.yourcompany.com` 服务的 `FTP` 服务。任何通过 `KDC` 身份验证并允许访问此服务的用户都可以使用 `www.yourcompany.com` 主机上的 `FTP` 服务。

然而，很多情况下，实体并没有实例。例如，可以创建一个用户实体，其显示如下：`james@YOURCOMPANY.COM`。该实体将允许用户登录到 Kerberos 域中的任何主机。当然，你也可以为用户指定实例。例如，以下实体将仅允许登录到名为 `www.yourcompany.com` 的系统：`james/www/yourcompany.com@YOURCOMPANY.COM`

## Kerberos 认证过程

接下来的几段中的信息经过了极大简化，但从系统管理员的角度来说，这些已经足够了。当 Kerberos 客户端首次从 `KDC` 获取 `TGT`（票据令牌）时，该令牌实际上并不提供对任何进程或网络服务的访问权限。它仅仅是一个告知 `KDC` 已经验证了该主机，且该主机和用户可以向其他主机请求服务的令牌。因为 `TGT` 使用用户密码签名并转换为哈希，用户可以使用 `kinit` 命令和自己的密码生成相同的哈希，并对两者进行比较。如果 `TGT` 和密码匹配，就会建立会话密钥并创建一个凭据缓存（通常位于 `/tmp/` 目录下的一个文件中）。

![](img/a7a9caa80ec85507179284d91e216f9f_326_0.png)

在凭据缓存文件被填充了 `TGT` 后，主机和用户就可以使用此 `TGT` 实际登录主机并请求服务。当用户（实体）需要访问主机的进程（如 Kerberos-FTP 和登录）时，用户使用其 `TGT` 联系 `KDC` 并请求实际票据，该票据是特定服务的访问令牌。如果 `KDC` 验证了此请求，`KDC` 将发送票据，并用其所请求的服务信息更新实体的凭据缓存。如果 Kerberos 数据库不包含该服务或主机名，访问将被拒绝。

## 信息如何在网络中传输

当票据跨网络传输时，它是由用户密码签名的，每当 Kerberos 管理员使用 `kadmin` 程序向数据库添加内容时都会输入密码。请注意，票据本身并不包含密码。它只是通过密码签名，从而创建一个哈希。不仅如此，Kerberos 还在此处放置了时间戳，这样即使有人使用超级计算机对该票据进行暴力破解攻击并生成了有效的哈希，该访问令牌也将不再有效。Red Hat Linux 中的 Kerberos 版本默认为 8 小时。因此，对于使用 Kerberos 的网络和系统，时间同步至关重要。可以使用 `NTP`（网络时间协议）来实现此目的。

> 注意
>
> 如需了解关于 Kerberos 如何工作的详尽讨论，请访问 http://web.mit.edu/kerberos/www/dialogue.html。该 URL 将带你进入一个名为《设计认证系统：四场对话》的文档。它不仅很好地解释了 Kerberos，而且是一篇使用苏格拉底式教学法对话的精彩讽刺。我知道这份文档听起来很枯燥，但它非常易读，将帮助你更多地了解为什么开发 Kerberos 以及它具体做了什么。

然而，请注意本文文档最初是为 Kerberos v4 版本编写的。Kerberos 的当前版本是 v5。Kerberos v4 和 Kerberos v5 之间的主要变化是 Kerberos v5 使用了公钥加密。因此，尽管对话写得很清晰，如果你不熟悉公钥加密，那么你可能也无法很好地理解 Kerberos。

![](img/a7a9caa80ec85507179284d91e216f9f_327_0.png)

## 创建 Kerberos 数据库

安装 Kerberos 后，你必须创建一个存储所有实体的数据库。你可以通过执行以下命令来实现：

```
/usr/kerberos/sbin/kdb5_util -s
```

该命令在 `/var/kerberos/krb5kdc/` 目录下创建必要的数据库文件。在创建了数据库条目后，你可以编辑 `/etc/krb5.conf` 和 `/var/kerberos/krb5kdc/kdc.ac` 文件，以反映你的 Kerberos 域和 DNS 域名。然后你必须向数据库添加一个管理员用户以及额外的实体。

## 使用 kadmin.local

由于你有了一个 Kerberos 域，你面临着逻辑上的困境：你需要管理 Kerberos，但 `kadmin` 命令要求你提供用户名和密码。然而，数据库中还没有任何管理员用户或密码。那么你如何开始呢？答案是使用 `/usr/kerberos/sbin/kadmin.local` 命令。它不需要用户先进行身份验证。只要你创建了 Kerberos 数据库并编辑了正确的文件，你就可以使用 `kadmin`。

```
/usr/kerberos/sbin/kadmin.local
```

该命令不需要用户先进行身份验证。只要你创建了 Kerberos 数据库并编辑了正确的文件，你就可以使用 `kadmin`。该命令允许你在没有现有账户的情况下管理数据库。

# 第 6 章 • 网络身份验证与加密

`kadmin` 命令还可以列出、修改和删除主体（principals）。要在 `kadmin` 内部列出 Kerberos 用户，请输入以下命令：

要删除任何主体，你可以执行以下命令：

```
kadmin: delete_principal user1
```

你确定要删除主体 "user1@YOURCOMPANY.COM" 吗？(yes/no): yes

主体 "user1@YOURCOMPANY.COM" 已删除。

在重新使用 `kadmin` 之前，请确保你已从所有 ACL 中删除了此主体。

要获取更多信息，请在 `kadmin` 内部使用 `?` `kadmin` 命令咨询 `/usr/share/krb5*/` 目录下的 Kerberos 文档和 man 手。星号代表你正在使用的 Kerberos 版本。

## 在客户端上使用 kadmin

`kadmin` 命令并不仅仅用于向 Kerberos 领域（realm）添加和管理主体。它还用于填充和更新每个 Kerberos 主机的密钥表文件（Key table files）。理解这一 `kadmin` 功能至关重要，这主要是因为现有的 Kerberos 文档略过了这一步骤。这部分是因为大多数编写关于 Kerberos 的人并没有实际实现 Kerberos 的知识，或者是因为他们太熟悉如何实现 Kerberos 了，以至于认为你已经知道这一步。希望这段讨论能够弥合过度理论化和过度技术化的写作者之间的鸿沟，并真正向你展示如何正确配置 Kerberos 客户端。你很快就会学习更多内容。图 6.11 显示了 `kadmin` 界面。

虽然界面很漂亮，但命令行界面非常适合更新客户端上的 `/etc/krb5.keytab` 文件。

![](img/a7a9caa80ec85507179284d91e216f9f_331_0.png)

作为 Kerberos 管理员，你将不得不使用主体。Kerberos 的创建者（马萨诸塞学院的研究人员）建议客户端密码至少包含六个字符。密码应该结合大小写字母，并且还包含数字和标点符号。

## 设置策略

Kerberos 策略与标准的 Unix 密码策略非常。它们决定了密码长度、用户主体是否会在特定时间过期、密码何时过期等。标准的主体策略设置包括以下内容：

- **策略名称**：当你创建一个策略时，可以对其命名以帮助与其他策略区分开来。
- **最小密码寿命（秒）**：用户在允许更改密码之前必须保留密码的时间。
- **最大密码寿命（秒）**：用户可以保留密码的最长时间。
- **最小密码长度**：设置密码必须具备的字符数。

当你使用 `kadmin` 添加主体且未指定策略时，默认行为是不建立任何策略。你可以通过 `kadmin` 内部的 `addpol` 命令来创建策略：

```
kadmin: addpol yourdomainpol
kadmin: modpol -maxlife 02/02/2004 -minlength 6 domainpol
```
