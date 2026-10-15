
`dnl` # 这允许我们使用与 OpenLDAP 的 `slapd` 共享的密钥文件，

`dnl` # `slapd` 要求该文件对 `ldap` 组可读

`dnl`

`define('CONFONT_FRAME_SENDMAIL','groupreadablekeyfile')dnl`

`define('CONFFTO_QUEUEBERH', '4h')dnl`

`define('CONFFTO_QUEUEBERH', '3d')dnl`

`define('CONFREFUSE_LA', '12')dnl`

`define('CONFID_ID', '0')dnl`

`define('FEATURE(policy_checks')dnl`

`define('FEATURE_no_default_msa')dnl`

`define('mail_table','/usr/bin/smsh -o /etc/mail/mailer.db')dnl`

`define('VIRTUETABLE','hash -t /etc/mail/virtueable.db')dnl`

`define('REDIRECT')dnl`

`define('FEATURE(aws_cm_file')dnl`

`define('FEATURE(use_ct_cl')dnl`

`dnl`

`dnl` # 如果服务器超出配额等，`-t` 选项将重试投递。

`dnl`

`define('FEATURE(local_procmail','procmail -t -a h -d $u')dnl`

`define('FEATURE(access_db','hash -T(TMPF) -o /etc/mail/access.db')dnl`

`define('FEATURE(blacklist_recipients')dnl`

`EXPOSED_USER('root')dnl`

`dnl`

`dnl` # 以下配置导致 `sendmail` 仅在 IPv4 回环地址

`dnl` # `127.0.0.1` 上监听，而不在此网络设备上。移除回环

`dnl` # 地址限制以接受来自互联网或内网的电子邮件。

`dnl`

`dnl` # * **

`DAEMON_OPTIONS('Port=smtp,Addr=127.0.0.1, Name=MTA')dnl`

`dnl`

`dnl` @ 以下配置导致 `sendmail` 额外监听 `587` 端口，用于

`dnl` # 来自经过身份验证的 MUAs 的邮件。无法访问其首选的

`dnl` # `25` 端口 `sendmail` 守护进程的漫游用户，可能会被拦截或重定向，那么

`dnl`

`dnl` @ 这是很有用的。

`DAEMON_OPTIONS('Port=submission, Name=MSA, M=Ea')dnl`

`dnl` @ 以下配置导致 `sendmail` 额外监听 `465` 端口，

`dnl` @ 连接时立即进入 TLS 模式。端口 `25` 或 `587` 随后

`dnl` @ 在端口 `25` 上通过 STARTTLS，优于使用 Outlook Express 的漫游客户端，或

`dnl` @ 不支持过时的 smpts；Evolution<1.1.1 在启用 SSL 时

`dnl` @ 使用 smpts - 版本 1.1.1 提供了 STARTTLS 支持。

`@` 要使此项工作，你必须配置 OpenSSL 证书。

`dnl` `DAEMON_OPTIONS('Port=smtp, Name=TLSMTA, M=s')dnl`

`@` 以下配置导致 `sendmail` 额外监听在 IPv6 回环

`dnl` @ 设备上。移除对网络的回环地址限制列表。

`dnl` @ 注意：将 de IPv4 和 IPv6 守护进程绑定到相同端口需要

`dnl` @ 内核补丁

`DAEMON_OPTIONS('port=smtp,Addr::1, Name=MTA-v6, Family=inet6')`

`dnl`

`dnl` @ 如果你想保护自己免受垃圾邮件的影响，我们强烈建议不要接受

`dnl` @ 不可响应。没有 DNS 的笔记本电脑和计算机

`dnl` @ 无法做到这一点。`FEATURE('unresolvable_domains')dnl` `FEATURE('relay_based_on')dnl`

`dnl` @ 同时也将发送到 "`localhost.localdomain`" 的邮件视为本地邮件。

`LOCAL_DOMAIN('localhost.localdomain')dnl`

`dnl` @ 以下示例使得来自此主机以及任何额外的

`dnl` 域名看起来像是从 `mydomain.com` 发送的

`MASQUERADE_AS('mydomain.com')dnl`

`dnl` @ 不仅伪装头部，还伪装信封内容

`FEATURE('masquerade_envelope')dnl`

`dnl` @ 不仅伪装 `@mydomainaliases.com`，还伪装 `@mydomain.com`

`FEATURE('masquerade_entire_domain')dnl`

`MASQUERADE_DOMAIN(localhost)dnl`

`MASQUERADE_DOMAIN(localhost.localdomain)dnl`

`MASQUERADE_DOMAIN(mydomain.com)dnl`

`MASQUERADE_DOMAIN(mydomain)dnl`

`MAILER(smtp)`

`MAILER(procmail)`

## 安装邮件服务器

如果你对 `/etc/mail/sendmail.mc` 文件进行了更改，你必须运行 `sendmail` 来生成 `/etc/mail/sendmail.cf` 文件：

```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

`sendmail` 宏（如 `FEATURE` 和 `MAILER`）在 `/usr/share/sendmail-cf` 中有描述。在更改 `sendmail.mc` 文件之前，咨询该文件以获取有关 `sendmail` 宏的信息。

通常，你需要将系统主机添加到 `sendmail.mc` 文件的最后一行：

1. 如果主机名是 `mycompany.com`，请按如下方式编辑 `/etc/mail/sendmail.mc` 中的 C 行：

`Cw.localdomain mycompany.com mycompany`

`sendmail` 宏在 `/usr/share/sendmail-cf` 目录下的 `m4` 文件中定义。根据之前的说明，`sendmail.mc` 包含：

```
include('/usr/share/sendmail-cf/m4')
```

`sendmail.mc` 文件随后反包含了许多 `m4` 文件。以下是关于 `/etc/mail/sendmail.mc` 文件的的一些关键点：

- `VERSIONID(setup for Red Hat)` 宏会将版本信息插入输出中。
- `OSYPE('linux')` 指定操作系统为 Linux。你必须指定此以确保配置正确。
- `MAILER(smtp)` 描述了邮件服务器。根据 `/usr/share/sendmail-cf/README` 文件，`MAILER` 声明应位于 `sendmail.mc` 的末尾，且 `MAILER(smtp)` 应始终位于 `MAILER(procmail)` 之前。`smtp` 邮件服务器指的是 SMTP 服务器。
- `FEATURE` 请求特殊功能。例如，`FEATURE('blacklist_recipients')` 开启对某些用户、主机或地址的拦截。允许或拒绝的规范放在访问数据库中。
- `MASQUERADE_DOMAIN(subdomain.mydomain.com)` 指示 `sendmail` 将如 `user@subdomain.mydomain.com` 的地址来自 `MASQUERADE_AS` 宏指定的域名。

# sendmail.cf 文件语法

`sendmail.cf` 文件的语法设计为便于 `sendmail` 程序解析，因为 `sendmail` 在每次启动时都会读取此文件。人类可读性在设计该文件时并非首要考虑因素。但是通过一些解释，你可以理解 `sendmail.cf` 中控制行的含义。

每个 `sendmail` 控制行都以单字母运算符开头，该运算符定义了行其余部分的含义。以空格或制表符开头的行被上一行的延续。空行和以井号 (`#`) 开头的行是注释。

通常，`sendmail.cf` 使用类（class）的概念——本质上是一个集合

## 安装邮件服务器

...的短语。你可以定义一个名为 `P` 的类，并使用以下控制行将短语 `REDRECT` 指向该类：

```
CPDIRECT
```

由于所有内容都混杂在一起，因此很难破译。另一方面，要定义一个名为 `Accept` 的类并将其设置为 `OK` 和 `RELAY` 的值，请编写以下内容：

```
C(Accept)OK RELAY
```

这可能稍微更容易理解，因为分隔符（如类名 `Accept`）被包含在花括号中。

其他 — 控制行甚至更易理解。例如，这一行：

- `O Helpfile=/etc/mail/helpfile`

将选项 `HelpFile` 定义为文件名 `/etc/mail/helpfile`。该文件包含了 `sendmail` 在接收到 `HELP` 命令时所使用的帮助信息。
