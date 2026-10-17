
| IP address | 邮件服务器的 IP 地址 |

| Hostname or domain | 邮件服务器的主机名 |

| From:user@host | 来自电子邮件地址 `user@host` 的邮件 |

| From:hostname or From:domain | 来自主机名或域名的邮件 |

| To:user@host | 寄向电子邮件地址 `user@host` 的邮件 |

| To:hostname or To:domain | 寄向主机名或域名的邮件 |

| Connect:hostname or Connect:domain | 来自主机名或给定域名内任何主机的连接 |

### 表 17-2：`/ETC/MAIL/ACCESS` 中条目的右侧

| RHS | 含义 |

|---|---|

| RELAY | 为 LHS 中指定的主机名或域名启用邮件中继 |

| OK | 接受邮件并忽略其他规则 |

| REJECT | 拒绝邮件 |

| DISCARD | 静默丢弃邮件；不显示错误信息 |

| ERROR RFC821-CODE text message | 显示 RFC 821 错误代码和文本消息 |

| ERROR RFC1893-CODE text message | 显示 RFC 1893 错误代码和文本消息 |

当你在 `/etc/mail/access` 文件中创建、修改或删除条目时，请记住这些规则：

- 运行 `newhash /etc/mail/access < /etc/mail/access` 命令以创建 Sendmail 可读的数据库。
- 使用 `/rc.d/init.d/sendmail restart` 命令重启服务器。

## 拒绝来自整个域名或主机的邮件

要拒绝来自整个域名（例如 `spamfactory.com`）的消息，请使用以下命令：

`spamfactory.com REJECT`

要拒绝来自名为 `bad.scam-artist.com` 主机的邮件，请使用

`bad.scam-artist.com REJECT`

上述配置不会拒绝来自其他主机的邮件。

## 拒绝来自特定电子邮件地址的邮件

要拒绝来自电子邮件地址 `newsletter@fromhell.com` 的邮件，请使用

`From:newsletter@fromhell.com REJECT`

你将收不到来自上述地址的邮件，但你仍然可以向该地址发送消息。

## 向域名或主机中继邮件

要向名为 `busyrebooting.com` 的域名中继消息，请使用

`To:busyrebooting.com RELAY`

此命令允许向 `busyrebooting.com` 域名中继消息，但 Sendmail 不接受来自它的非本地消息；也就是说，Sendmail 不中继。

## 从域名或主机中继邮件

要从名为 `imbuddies.com` 的域名中继消息，请使用

`Connect:imbuddies.com RELAY`

## 接受来自域名的特定电子邮件地址

有时，你希望禁止某个域名除极少数用户以外的所有用户的邮件。例如，要为 `myfoe.net` 域名禁止所有人向 `spyl@myfoe.net` 和 `spy2@myfoe.net` 地址发送邮件，请使用

```
From:spyl@myfoe.net OK
From:spy2@myfoe.net OK
From:myfoe.net REJECT
```

除了前两个地址外，所有邮件都会被拒绝。

## 使用 FEATURE(RELAY_ENTIRE_DOMAIN)

该功能的数据库存储在 `/etc/mail/relay-domains` 中。该文件的每行列出一个 Internet 域名。当设置此功能时，它允许中继一个域名内的所有主机。例如，如果你的 `/etc/mail/relay-domain` 文件如下行所示，则允许发往和来自 `kabirsfriends.com` 的邮件：

```
kabirsfriends.com
```

## 使用 FEATURE(RELAY_HOSTS_ONLY)

如果你不想对整个域名启用开放邮件中继，可以使用此功能指定你的服务器允许作为邮件中继的每个主机。

## 启用 MAPS 实时黑洞列表 (RBL) 支持

MAPS RBL 使用一组 DNS 服务器来访问所谓垃圾邮件发送者的黑名单，这些发送者通常由垃圾邮件受害者举报。

开始使用 RBL 保护你的邮件中继的最简单方法是，使其每当你收到来自你不熟悉的垃圾状态主的传入消息时，对其进行 DNS 查询（针对一个格式化的名称）。

当远程服务器（例如 `192.168.1.1`）连接到你的邮件服务器时，MAPS RBL 会检查 DNS 中是否存在该地址。如果找到 A 记录，则该地址可能在黑名单中。

要使用 MAPS RBL 功能，请在你的 `/etc/mail/sendmail.cf` 中添加以下内容：

```
FEATURE(MAPS, access
```

要使用 MAPS RBL，请在你的 `/etc/mail/access` 文件中添加以下条目：

```
.RBL REJECT
.RELAY OK
```

# 第17章：邮件服务器安全

```bash
cp -r /etc/mail /etc/mail.bak
cp /usr/sbin/sendmail /usr/sbin/sendmail.bak
cp /usr/sbin/makemap /usr/sbin/makemap.bak
cp /usr/bin/newaliases /usr/bin/newaliases
```

从 `www.sendmail.org` 下载最新的 Sendmail 源码，我下载了 `sendmail.8.11.0.tar.gz`，这是编写本文时最新的源码。请确保在完成操作说明时替换相应的版本信息。

- 1. 使用 `tar xvzf sendmail-8.11.0.tar.gz` 命令解压 Sendmail 源码包。这会创建一个名为 `sendmail-8.11.0` 的子目录。进入该子目录。
- 2. 运行以下命令将 Sendmail 配置文件提取并安装到相应的目录。
- 3. 遵循 `INSTALL` 文件中的说明并按照指示编译 Sendmail。
- 4. 将以下行添加到 `/usr/src/redhat/SOURCES/sendmail-8.11.0/devtools/site.config.m4` 文件中。

```bash
mkdir -p /etc/mail
cp etc.mail.tar.gz /etc/mail
cp site.config.m4 sendmail-8.11.0/devtools/Site/
cp sendmail.init /etc/rc/init.d/sendmail

APPENDDEF('confVENDEFS', '-DSASL')
APPENDDEF('conf_sendmail_LIBS', '-lsasl')
APPENDDEF('confFLIBIRS', '-L/usr/local/lib/sasl')
APPENDDEF('confINCDDIRS', '-I/usr/local/include')
```

- 5. `sendmail-8.11.0/devtools/Site/config.m4` 文件如列表 17-3 所示：

列表 17-3: `define(CONFDEF_TYPE, 'CC-M')`

```bash
define('confEFINDIR', '/usr/sbin')
define('confFORCE_MAIL')
define('confLIBS', '-ldl')
define('confLDOOPTS_SO', '-shared')
define('confMANROOT', '/usr/man/man')
define('confMAPDEF', '-DNEWDBM -DMAP_REGEX -DNIS')
DTCP_WRAPPERS, '')
define('confMTLDOPTS', '-lpthread')
define('confOPTIMIZE', '$(RPM_OPT_FLAGS)')
define('confSTDIR', '/var/log')
APPENDDEF('confLIBSEARCH', 'crypt nsl wrap')
```

# 第四部分：网络安全服务

```bash
APPENDDEF('conf_ENVDEF', '-DSASL')
APPENDDEF('conf_sendmail_LIBS', '-lsasl')
APPENDDEF('confLIBDIRS', '-L/usr/local/lib/sasl')
APPENDDEF('confINCDIRS', '--I/usr/local/include')
```

- 6. 切换到 `/usr/src/redhat/SOURCES/sendmail-8.11.0/sendmail` 并运行 `su build -c` 命令重新编译 Sendmail。
- 7. 运行 `sh build install` 安装新的 Sendmail 二进制文件。
