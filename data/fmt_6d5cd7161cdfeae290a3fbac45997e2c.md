
| `H` | 定义 `sendmail` 插入到消息中的标题行格式。例如，`H2P?Return-Path: <$g>` 定义了标题的 `Return-Path:` 字段。 |

| `K` | 定义一个映射（键值对数据库）。例如，`Karith arith` 将名为 `arith` 的映射定义为同名内置映射。 |

| `M` | 指定一个邮件器（mailer）。以下行定义了 `procmail` 邮件器：`Mprocmail,P=/usr/bin/procmail,R=DFMSPhnu9,S=EnvFromSMTP/HdrFromSMTP/HdrFromSMTP,T=DNS/RFC822/X-Unix,A=procmail -Y m $h $f $u.` |

| `O` | 将值分配给一个选项。例如，`OAliasFile=/etc/aliases` 将 `AliasFile` 选项定义为 `/etc/aliases`，即 `sendmail.aliases` 文件的名称。 |

| `P` | 定义优先级字段的值。例如，`Pjunk=-100` 将标记有标题字段 `Precedence: junk` 的消息优先级设置为 `-100`。 |

| `R` | 定义一条规则（规则有左端和右端；如果输入匹配左端，右端将替换它——此规则称为 `重写`）。例如，重写规则 `R* $* $1` 会去除末尾的分号。 |

| `S` | 标记一个规则集，你可以使用后续的 `R` 控制行开始定义该规则集。例如，`Sconify=3` 将下一个规则集标记为 `conify` 或 `ruleset 3`。 |

| `T` | 将用户名添加到受信任类（类 `t`）中。例如，`Troot` 将 `root` 添加到受信任用户类中。 |

| `V` | 定义配置文件的主版本号。例如，`V10/Berkeley` 将版本号定义为 10。 |

### 其他 sendmail 文件

`/etc/mail` 目录包含 `sendmail` 使用的其他文件。这些文件在 `sendmail` 配置文件 `/etc/mail/sendmail.cf` 中被引用。例如，你可以使用以下方法在 `/etc/mail/sendmail.cf` 文件中搜索 `/etc/mail` 字符串：

```
grep "/etc/mail" /etc/mail/sendmail.cf
```

以下是 `grep` 命令在我的 Fedora Core 系统上搜索后显示的结果：

```
Fw/etc/mail/local-host-names
FR-o /etc/mail/relay-domains
Kmailertable hash -o /etc/mail/virtuser table.db
KVirtuser hash -o /etc/mail/mailvirtuser table.db
Kaccess hash -T<TMP> -o /etc/mail/access.db
#0 ErrorHandler=/etc/mail/error-header
O HelpFile=/etc/mail/helpfile
O UserDatabaseSpec=/etc/mail/userdb.db
#0 ServiceSwitchFile=/etc/mail/service.switch
#0 DefaultAuthInfo=/etc/mail/default-auth-info
O CACertPath=/etc/mail/certs
O CACertFile=/etc/mail/certs/cacert.pem
O ServerCertFile=/etc/mail/certs/cert.pem
O ServerKeyFile=/etc/mail/certs/key.pem
O ClientCertFile=/etc/mail/certs/cert.pem
O ClientKeyFile=/etc/mail/certs/key.pem
Ft/etc/mail/trusted-users
```

你可以忽略以井号或数字符号（`#`）开头的行，因为 `sendmail` 将这些行视为注释。其他行是 `sendmail` 控制行，它们引用 `/etc/mail` 目录中的其他文件。

以下是这些 `sendmail` 文件应包含的内容（请注意，并非所有这些文件都必须存在于你的 `/etc/mail` 目录中，即使存在，有些文件也可能为空）：

- `/etc/mail/access`：允许发送邮件的主机名称和/或 IP 地址（有助于阻止垃圾邮件——非预期的电子邮件）

- `/etc/mail/access.db`：从 `/etc/mail/access` 文件生成的访问数据库

- `/etc/mail/helpfile`：SMTP 命令的帮助信息

- `/etc/mail/local-host-names`：该主机的已知名称

- `/etc/mail/mailertable`：用于覆盖邮件路由方式的邮件器表（例如，条目 `comcast.net smtp:smtp.comcast.net` 告诉 `sendmail`， addressed to `comcast.net` 的邮件必须发送到 `smtp.comcast.net`）

- `/etc/mail/relay-domains`：允许中继的主机

- `/etc/mail/trusted-users`：允许使用其他用户名称发送邮件而不会收到警告的用户列表

- `/etc/mail/userdb.db`：包含每个用户登录名和真实姓名信息的用户数据库文件

- `/etc/mail/virtualtable`：托管在该系统上的具有虚拟域地址的用户的数据库

![](img/9f89727199836b0f871f1745838aa8b2_688_0.png)

`/etc/mail` 目录中剩余的 `sendmail` 文件——`/etc/mail/certs` 和带有 `.pem` 扩展名的文件——旨在通过利用 SMTP 的 STARTTLS 扩展来支持 `sendmail` 中的隐私增强邮件（PEM）。STARTTLS 扩展使用 TLS（更常见的名称是 SSL）来验证发送者并加密邮件。RFC 2487 描述了 STARTTLS（该 RFC 可在线 `ietf.org/rfc/rfc2487.txt` 获取）。

![](img/9f89727199836b0f871f1745838aa8b2_688_1.png)

如果你编辑 `/etc/mail/mailertable` 文件，在更改生效之前，你需要输入以下命令：

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```

这是一种更简单的方法来确保在对任何更改后重建所有必要的文件——只需在登录为 `root` 时输入以下命令即可：

```
cd /etc/mail
make
```

#### .forward 文件

用户可以通过在其主目录中放置 `.forward` 文件来重定向自己的邮件。`.forward` 文件是一个纯文本文件，包含以逗号分隔的邮件地址列表。发送到该用户的任何邮件都会被转发到这些地址。如果 `.forward` 文件只包含一个地址，则该用户的所有电子邮件都会被重定向到该单一电子邮件地址。例如，假设在一个名为 `emily` 的用户的主目录中放置了一个包含以下行的 `.forward` 文件：

`ashley`

此命令会使得 `sendmail` 将发送给 `emily` 的所有邮件自动转发到同一系统上的用户名 `ashley`。用户 `emily` 将无法收到任何邮件。

你也可以通过列出完整的电子邮件地址将邮件转发到另一个系统上的用户名。例如，我添加了一个包含以下内容的 `.forward` 文件，以便将我的信息（发给我的用户名 `naba`）转发到电子邮件地址 `naba@comcast.net`：

```
naba@comcast.net
```

现在假设我希望除了转发到 `naba@comcast.net` 之外，还能在原始系统上保留一份消息副本。我可以通过在 `.forward` 文件中添加以下行来实现：

```
naba@comcast.net, naba\
```

我只需在我的用户名后追加一个反斜杠作为行尾即可。行尾的反斜杠（`\`）可以阻止 `sendmail` 反复转发该消息（因为当副本发送到系统上的我的用户名时，`sendmail` 会再次处理我的 `.forward` 文件——反斜杠告诉 `sendmail` 不要重复转发消息）。

#### 在 .forward 文件中调用 procmail

使用 `.forward` 文件的一个有趣用途是运行 `procmail` 来自动处理某些邮件。例如，假设你想删除任何来自包含字符串 `mailing_list` 的地址的电子邮件。以下是实现该功能的具体步骤：

1. 在你的主目录中创建一个 `.forward` 文件，并在其中放入以下行：

   ```
   "| /usr/bin/procmail"
   ```

   此命令会致使 `sendmail` 运行外部程序 `/usr/bin/procmail`，并将电子邮件消息发送到该程序的输入流中。
