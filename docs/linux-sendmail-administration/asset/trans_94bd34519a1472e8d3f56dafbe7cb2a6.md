

confXF_BUFFER_SIZE 定义了转录文件写入磁盘之前，可用于的缓冲区内存最大量。默认值为 4096 字节。[ScriptFileBufferSize]

尽管此列表很长，但还有更多的定义参数。额外的参数列表在附录后半部分的 DOMAIN 和 OSTYPE 宏中介绍。define 命令是 m4 源文件中最常用的命令。紧随其后最常用的是 FEATURE 宏。

## FEATURE

FEATURE 宏处理来自 `cf/feature` 目录的 m4 源代码。该目录下的源文件定义了可选的 Sendmail 功能。FEATURE 宏的语法如下：

```
FEATURE(name, argument])
```

参数字段是可选的。如果向源文件传递了参数，源文件将使用该参数为 sendmail.cf 文件生成代码。例如：

```
FEATURE('mailertable', `dbm /etc/mail/mailertable')
```
这将生成访问 mailertable 的代码，并将该表定义为位于 `/etc/mail/mailertable` 文件的 dbm 数据库。

可用功能列在表 A.2 中。该表提供了每个功能的名称及其用途。

## 表 A.2 功能

| 名称 | 用途 |
|---|---|
| accept_unqualified_senders | 允许来自不包含有效主机名的地址的网络邮件。 |
| accept_unresolvable_domains | 接受来自 DNS 未知主机的邮件。 |
| access_db | 使用访问数据库控制中继。 |
| allmasquerade | 伪装收件地址。 |

## 表 A.2 功能（续）

| 名称 | 用途 |
| --- | --- |
| always_add_domain | 为所有本地投递的邮件添加本地主机名。 |
| bestmx_is_local | 将发送至列我们为 MX 服务器的主机的邮件视为本地邮件。 |
| bitdomain | 使用表将 BITNET 主机映射到 Internet 地址。 |
| blacklist_recipients | 根据访问数据库中的值过滤入站邮件。 |
| delay_checks | 延迟 check_mail 和 check_relay 规则，直到调用 check_rcpt。 |
| dnsbl | 拒绝来自 DNS 拒绝列表列出的主机的邮件。替换了 rbl。 |
| domaintable | 使用域名表映射域名。 |
| generics_entire_domain | 通过 genericstable 映射在类 G 中识别的域名。 |
| genericstable | 使用表重写本地地址和类 G 的地址。 |
| ldap_routing | 启用基于 LDAP 的邮件路由。 |
| limited_masquerade | 仅伪装列在 =M 中的主机。 |
| local_lmtp | 使用支持 LMTP 的 mail.local。 |
| local_procmail | 使用 procmail 作为本地邮件投递器。 |
| loose_relay_check | 对使用 % 技巧的地址禁用有效性检查。 |
| mailertable | 使用邮件代理表路由邮件。 |

## 附录 A m4 宏命令参考

**表 A.2** 功能（续）

| 名称 | 用途 |
| --- | --- |
| masquerade_entire_domain | 伪装伪装域名内的所有主机。 |
| masquerade_envelope | 除报头发送者地址外，还伪装信封层发送者地址。 |
| no_default_msa | 允许消息提交代理（Message Submission Agent）的默认配置被 DAEMON_OPTIONS 宏覆盖。 |
| nocanonify | 不使用 DNS 转换地址和主机名。 |
| nodns | 不包含 DNS 支持。 |
| nouucp | 不包含 UUCP 地址处理。 |
| nullclient | 将所有邮件转发到中央服务器。 |
| promiscuous_relay | 从任何站点到任何站点中继邮件。 |
| rbl | 已过时的实时黑列表（Realtime Blackhole List）功能已被 dnsbl 替换。 |
| redirect | 支持 .REDIRECT 伪域名。 |
| relay_based_on_MX | 为任何 MX 记录指向此服务器的站点中继邮件。 |
| relay_entire_domain | 为你域名中的任何主机中继邮件。 |
| relay_hosts_only | 仅为访问数据库中列出的主机中继邮件。 |
| relay_local_from | 如果源是本地主机，则中继邮件。 |
| relay_mail_from | 如果发送者在访问数据库中列为 RELAY，则中继邮件。 |
| smrsh | 使用 smrsh 作为代理邮件投递器。 |

## 表 A.2 功能（续）

| 名称 | 用途 |
|--- |--- |
| stickyhost | 将“user”与“user@local.host.”进行区别对待。 |
| use_ct_file | 从 confCT_FILE 定义的文件加载 $=t$。 |
| use_cw_file | 从 confCW_FILE 定义的文件加载 $=w$。 |
| uucpdomain | 使用表将 UUCP 主机映射到 Internet 地址。 |
| virt_entire_domain | 通过 virtuertable 映射整个域名。 |
| virtuertable | 将虚拟域名映射到真实的邮件地址。 |

FEATURE 宏会从 sendmail.cf 文件中移除未使用的行。noucp 为无法访问 UUCP 网络的系统移除处理 UUCP 地址的代码，nodrs 为无法访问 DNS 的系统移除 DNS 查找代码。nulllican 禁用将昵称和 IP 地址转换为主机名的代码。最后，nullClient 剥离将昵称和 IP 地址转换为主机名的代码。

许多功能与中继和伪装有关。这些是：stickyhost、allmasquerade、relay_based_on_MX、relay_hosts_only 和 masquerade_entire_domain。

几个功能定义了用于特殊处理的数据库。这些是：domaintable、bitdomain、uucpdomain 和 genericstable。

genericstable 通常用于转换与伪装处理相同的地址，因此这些功能影响伪装，且通用地址以相同的方式设置。如果你使用了 genericstable 并使用了伪装，请设置 GENERIC_DOMAIN 和 GENERIC_DOMAIN_FILE 以设置你为 MASQUERADE_DOMAIN 和 MASQUERADE_DOMAIN_FILE 设置的值。

