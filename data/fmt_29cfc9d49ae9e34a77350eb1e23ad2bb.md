
| To: hostname or To:domain | 发往主机名或域名的邮件 |

| Connect: hostname or Connect:domain | 来自主机名或所给域名内任何一个主机的连接 |

表 17-2：`/ETC/MAIL/ACCESS` 中条目的右侧

| RHS | 含义 |

| --- | --- |

| RELAY | 为 LHS 中命名的主机或域名启用邮件中继功能 |

| OK | 接受邮件并忽略其他规则 |

| REJECT | 拒绝邮件 |

| DISCARD | 静默丢弃邮件；不显示错误消息 |

| ERROR RFC821-CODE text message | 显示 RFC 821 错误代码和文本消息 |

| ERROR RFC1893-CODE text message | 显示 RFC 1893 错误代码和文本消息 |

当你在 `/etc/mail/access` 文件中创建、修改或删除条目时，请记住这些规则：

- 运行 `makemap hash /etc/mail/access /etc/mail/access` 命令创建 Sendmail 可读的数据库。
- 使用 `/rc.init.d/sendmail restart` 命令重启服务器。

### 拒绝来自整个域名或主机的邮件

要拒绝来自整个域名（例如来自 `spamfactory.com` 的邮件），请使用以下命令：

```
spamfactory.com REJECT
```

要拒绝来自名为 `bad.scam-artist.com` 主机的邮件，请使用：

```
bad.scam-artist.com REJECT
```

上述配置不会拒绝来自其他主机的邮件。

### 拒绝来自特定电子邮件地址的邮件

要拒绝来自名为 `newsletter@fromhell.com` 地址的邮件，请使用：

```
From:newsletter@fromhell.com REJECT
```

你不会收到来自上述地址的邮件，但仍然可以向该地址发送消息。

### 向域名或主机中继邮件

要向域名 `busyrebooting.com` 中继消息，请使用：

```
To:busrebooting.com RELAY
```

此命令允许向 `busyrebooting.com` 域名中继消息，但 Sendmail 不接受来自它的非本地消息；也就是说，Sendmail 不进行中继。

### 从域名或主机中继邮件

要从中继来自名为 `imbuddies.com` 域的消息，请使用：

```
Connect:imbuddies.com RELAY
```

### 接受来自域名的特定电子邮件地址

有时，你希望允许特定域名的所有用户，除了少数几个。例如，为了封禁 `myfoe.net` 域名中除地址 `spy@myfoe.net` 和 `sp2@myfoe.net` 以外的所有用户邮件，请使用：

| From:sp1@myfoe.net | OK |

| From:sp2@myfoe.net | OK |

| From:myfoe.net | REJECT |

除了前两个地址外，所有邮件都会被拒绝。

## 使用 FEATURE(RELAY_ENTIRE_DOMAIN)

该功能的数据库存储在 `/etc/mail/relay-domains` 中。该文件的每行列出了一个域名。当设置此功能时，它允许中继域名内的所有主机。例如，如果 `/etc/mail/relay-domains` 看起来如下所示所示，则允许发往和来自 `myfriends.com` 的邮件：

```
myfriends.com
```

### 使用 FEATURE(RELAY_HOSTS_ONLY)

如果你不想对整个域名开启入站的开放中继，可以使用此功能指定你的服务器作为中继代理的每个主机。

## 启用实时黑名单 (RBL)

RBL 使用一组修改过的 DNS 服务器来访问垃圾邮件发送者的黑名单，这些者通常由害者举报。使用 RBL 保护邮件中继的最简单方法是，每当你从状态未知的主机接收传入邮件时，安排进行 DNS 查询（名称）。当远程邮件服务器 (`192.168.1.1`) 连接到你的邮件服务器时，Sendmail 会检查 RBL 规则集中是否存在地址记录 (A)。Sendmail 会为 `192.168.1.1.in.rbl.abuse.org` 发出 DNS 请求。如果找到了 `192.168.1.1` 的地址记录 (A)，意味着 `192.168.1.1` 被列入黑名单。你的 Sendmail 服务器随后可以拒绝它。要使用 RBL，请向你的配置文件添加以下功能，重新生成 `/etc/mail/sendmail.cf` 并重启服务器。

```
FEATURE('dnsbl','rbl.maps.com')
FEATURE('dnsbl','dbl.maps.com')
FEATURE('dnsbl','rbl.abuse.org')
```

当一个远程邮件服务器 (`192.168.1.1`) 连接到你的邮件服务器时，Sendmail 会检查 RBL 规则集中是否存在地址记录 (A)。Sendmail 会为 `192.168.1.1.in.rbl.abuse.org` 发出 DNS 请求。如果找到了 `192.168.1.1` 的地址记录 (A)，意味着 `192.168.1.1` 被列入黑名单。你的 Sendmail 服务器随后可以拒绝它。要使用 RBL，请向你的配置文件添加以下功能，重新生成 `/etc/mail/sendmail.cf` 并重启服务器。

```
FEATURE('dnsbl','rbl.maps.com')
FEATURE('dnsbl','dbl.maps.com')
FEATURE('dnsbl','rbl.abuse.org')
```

*(注：此处原文中存在部分重复和乱码，译文已根据逻辑进行了对齐处理)*

# 第 17 章：邮件服务器安全 427

```bash
cp -r /etc/mail /etc/mail.bak
cp /usr/sbin/sendmail /usr/sbin/sendmail.bak
cp /usr/sbin/makemap /usr/sbin/makemap.bak
cp /usr/bin/newaliases /usr/bin/newaliases.bak
```

从 `www.sendmail.org` 下载最新的 Sendmail 源码。我下载了 `sendmail-8.11.0.tar.gz`，正如你应该做的那样，这是最新的源码。确保在完成以下指令时替换版本信息。

- 使用 `tar xvzf sendmail-8.11.0.tar.gz` 命令解压 Sendmail 源码分发包。这将创建一个名为 `sendmail-8.11.0` 的子目录。进入该子目录。
- 运行以下命令在相应的目录下提取并安装 Sendmail 配置文件。

```bash
mkdir -p /etc/mail
cp site.mail.gz /etc/mail
cp site.config.m4 sendmail-8.11.0/devtools/Site/
cp sendmail.init /etc/rc/init.d/sendmail
```

- 遵循 `INSTALL` 文件中的指令并按照指示构建 Sendmail。

在 `/usr/src/redhat/SOURCES/sendmail-8.11.0/devtools/site.config.m4` 文件中添加以下行。

```bash
APPENDDEF('CONFVDEF', '-DSASL')
APPENDDEF('conf_mail_LIBS', '-lsasl')
APPENDDEF('CONFIBINDS', '-L/usr/local/lib/sasl')
APPENDDEF('CONFINCDIRS', '-I/usr/local/include')
```

Sendmail-8.11.0/devtools/Site/config.m4 文件如列表 17-3 所示。

列表 17-3：`define('CONFDEPEND_TYPE', '-CC-M')`

```text
define('CONFIBINDS', '/usr/sbin')
define('CONFFORCE_MAIL')
define('CONFLIBS', '-ldl')
define('CONFDLOPTS_SO', '-shared')
define('CONFMANROOT', '/usr/man/man')
define('CONFMAPDEF', '-DNEWDB -DMAP_REGEX -NISDTCP_WRAPPERS')
define('CONFMTLDOPTS', '-lpthread')
define('CONFOPTMIMIZE', '$(M_OPT_FLAGS)')
define('CONFSTDIR', '/var/log')
APPENDDEF('CONFLIBSEARCH', 'crypt nsl wrap ')
```

# 第四部分：网络服务安全
