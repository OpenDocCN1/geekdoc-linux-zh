

## 第 20 章 电子邮箱

### virtuertable 功能
virtuertable 功能支持入站邮件的域名别名（domain aliasing）。该功能允许在台机器上托管多个虚拟域名，经常用于 Web 托管站点。该表的关键键字段包含电子邮件地址（user@host.domain）或域名规范（@domain）。值是本地或外部电子邮件地址。如果键是域名，则该值可以通过变量 %1 传递用户字段，或者将邮件路由到不同的用户。以下是一些示例：

```
@registered.com %1@atrust.com
unix@book.admin.com sa-book-authors@atrust.com
linux@book.admin.com sa-book-authors@atrust.com
webmaster@example.com billy.y@zakowski@colorado.edu
info@testdomain.net username@hotmail.com
```

数据映射左侧的所有主机都必须列在 cw 文件（`/etc/mail/local-host-names`）中，或者包含在 VIRTUS_DOMAIN 列表中。如果没有列，sendmail 将不会在本地接受邮件，而将尝试在互联网上查找目标主机。但 DNS MX 记录会将邮件指向回此服务器，你将在生成的退信邮件中收到一条“local configuration error”（本地配置错误）消息。遗憾的是，sendmail 无法告知此实例的错误实际上应该是“virtuertable key not in cw file”。

### ldap_routing 功能
LDAP（轻量级目录访问协议）可以作为别名或邮件路由信息的数据源，以及上述的通用表格数据。cf/README 文件有一个关于 LDAP 的长章节，包含许多示例。

要在此处使用 LDAP，你必须在编译 sendmail 时包含 LDAP 支持。在你的 .mail 文件中，添加：
```
define(CONF_DEFAULT_SPEC, '-h server -b searchbase')
FEATURE('ldap_routing')
LDAPROUTE_DOMAIN(my_domain)
```

这些行告诉 sendmail 你想使用 LDAP 数据库来路由发往指定域的入站邮件。LDAP_DEFAULT_SPEC 选项标识 LDAP 服务器和搜索的基名。除非通过在 define 中添加 `-p ldap_port` 指定了不同的端口，否则 LDAP 使用 389 端口。
sendmail 使用 LDAP 数据库中的两个标签之一：

- * mailLocalAddress* 用于入站邮件的收件人
- * mailRoutingAddress* 用于邮件应该发送到的目的地

sendmail 还支持 mailHost 标签，如果存在，它会将邮件路由到为指定主机指定的 MX 指定的邮件处理器。收件人地址保持为 mailRoutingAddress 标签的值。

### MAIL_HUB 和 SMART_HOST 宏 787

LDAP 数据库条目支持通配符条目 @domain，它可以路由发往指定域任何人的邮件（正如 virtuertable 中执行的操作）。

默认情况下，发往 user@host1.mydomain 的邮件会首先触发对 user@host1.mydomain 的查询。如果失败，sendmail 将尝试 @host1.mydomain 但不会尝试 @mydomain。包含以下行：
```
LDAPROUTE_EQUIVALENT('host1.mydomain')
```
也会尝试 user@mydomain 和 @mydomain。此功能允许单个数据库将邮件路由到复杂的站点。你也可以从文件中获取 LDAPROUTE_EQUIVALENT 的条目，这使得该功能非常有用。该形式的语法为：
```
LDAPROUTE_EQUIVALENT_FILE(filename)
```
ldap_routing 功能的附加参数允许你指定关于 LDAP 架构的更多细节，并控制对带有部分的地址的处理。一如既往，详见 cf/README 文件。

### 伪装功能 (masquerading features)
电子邮件地址通常由用户名、主机和域名组成，但许多站点不希望其主机的名称暴露在互联网上。MASQUADE_AS 允许你为其他机器指定单一身份进行隐藏。所有邮件似乎都来自指定的机器或域名。这对于普通用户来说没有问题，但为了调试目的，以 root 身份的用户应该被排除在伪装之外。例如，邮件将被标记为来自 user@atrust.com，除非它是由邮件系统的 root 发送的；在这些情况下，邮件将携带原始主机的名称。MASQUADE_AS 只是伪装的一个冰角，它扩展到了许多变体。伪装信封（masquerade_envelope，与 MASQUADE_AS 结合使用）仅隐藏本地信息。详见 cf/README。

### MAIL_HUB 和 SMART_HOST 宏
伪装通过重写头（以及可选地重写信封）使所有邮件看起来都来自同一个主机或域名。大多数站点都希望所有邮件实际上来自（或发往）单台机器，以便他们控制病毒和垃圾邮件的流量。你可以通过 DNS 中的 MX 记录、入站邮件的 MAIL_HUB 宏和出站邮件的 SMART_HOST 宏的组合来实现。
![](img/579ec8c67772f31ecf484bbb71a2_835_0.png)

关于 MX 记录的更多信息请参见第 583 页。对于第 754 页的架构图，MX 记录会将邮件指向 DMZ。为了过滤病毒和垃圾邮件，SMART_HOST 允许客户端中继，例如：
```
define(MAIL_HUB, 'smtp:routing.mydomain')
```
同样，SMART_HOST 允许客户端中继，不进行全限定域名的配置。这些设置允许邮件服务器接受客户端的邮件。sendmail 的 nullclient 特性在这种情况下是正确的：
```
FEATURE('config')
FEATURE('mailserver')
```
### 客户端配置
如果你遵循第 753 页的邮件系统设计，sendmail 应该以 MSA 运行（不带 -bd 标志），如果客户端机器可以被教使用端口 587 提交。否则，以守护进程模式 (-bd)  sendmail，但将 DAEMON_OPTIONS 配置为仅监听回环接口连接。

### sendmail 中的垃圾邮件相关功能
SUSE 在 /etc/mail/linux.nullclient.mc 提供了一个空客户端 .mc 文件。填入你的邮件服务器名称，构建 sendmail.cf 文件，然后就完成了。

### 配置选项
你使用 m4 的 define 命令设置配置选项。所有作为 m4 变量访问的选项列表（以及它们的默认值）都在 cf/README 文件中。默认值对于一个对安全不敏感且对性能不在关心的典型设置是足够的。默认通过关闭中继、要求地址全限定以及要求发送域名解析为 IP 地址来保护你免受垃圾邮件的影响。如果你的邮件服务器繁忙并处理大量的邮件列表，你可能需要调整某些性能值。

下一页的表格 20.11 列出了可能需要调整的选项（175 多个配置选项中的 10%）。它们的默认值显示在括号中。为了不带 conf 前缀，名称使用了空格；例如，FALLBACK_MX 选项实际的名为 confFALLBACK_MX。我们将表格分为识别变量地址问题的子部分：资源管理、性能、安全和垃圾邮件缓解以及杂项选项。某些选项属于多个类别，但我们只列出了一次。

