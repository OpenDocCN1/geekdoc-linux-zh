
正如文件开头的注释（以 `dnl` 开头的行）所解释的，你可以通过通过 `m4` 宏处理器运行 `sendmail.mc` 文件来生成 `/etc/mail/sendmail.cf` 文件（你需要以 root 身份登录）：

```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

注释还提到你需要 `sendmail-cf` 包来处理此文件。根据上一节对 `m4` 宏的描述，你可以看到 `sendmail-cf` 包来处理此文件。

# 第 15 章：邮件服务器

```
dnl define('confREFUSE_LA', '18')dnl

dnl define('conf0_IDENT', '.0')dnl

dnl FEATURE(delay_checks)dnl

dnl FEATURE('no_default_msa', '.1')dnl

dnl FEATURE('smarthp','/usr/bin/smarthp')dnl

dnl FEATURE('mailertail',.hash -o /etc/mail/mailertail.db')dnl

dnl FEATURE('virtusertable',.hash -o /etc/mail/virtusertable.db')dnl

dnl FEATURE(redirect)dnl

dnl FEATURE(always_add_domain)dnl

dnl FEATURE(use_cw_file)dnl

dnl FEATURE(use_ct_file)dnl

dnl #

dnl # - t 选项将在例如用户超出配额时重试投递。

dnl #

dnl FEATURE(local_procmail,.procmail -t -y -a d $u)dnl

dnl FEATURE('access.db',.hash -TMP> -o /etc/mail/access.db')dnl

dnl FEATURE('blacklist_list_recipients')dnl

EXPOSED_USER('root')dnl

dnl #

dnl # 以下内容导致 sendsmail 额外监听 IPv4 回环地址

dnl # 127.0.0.1 且不监听任何其他网络设备。移除回环

dnl # 地址限制以接受来自互联网或局域网的电子邮件。

dnl #

dnl DAEMON_OPTIONS('Port-smtp,Addr-127.0.0.1,Name-MTA')dnl

dnl #

dnl # 以下内容导致 sendsmail 额外监听端口 587，用于接收

dnl # 来自经过身份验证的 MUA（邮件代理程序）的邮件。由于端口 25 被封锁或重定向，

dnl # 无法访问首选 sendsmail 守护进程的漫游用户：

dnl # 这非常有用。

dnl #

dnl DAEMON_OPTIONS('Port-submission,Name-MSA,M-Fea')dnl

dnl #

dnl # 以下内容导致 sendsmail 额外监听端口 465，但

dnl # 连接后立即进入 TIS 模式。首选端口 25 或 587 紧跟

dnl # 使用 STARTTLS，但使用 Outlook Express 的漫游客户端无法在 25 以外

dnl # 端口执行 STARTTLS。Mozilla Mail 只能使用 STARTTLS

dnl # 不支持已弃的方法；Evolution (1.1.1) 在启用 SSL 时使用 smtps

dnl # 在 1.1.1 版本中提供了 STARTTLS 支持。

dnl #

dnl # 为了完成你的工作，必须配置 OpenSSL 证书。

dnl #

dnl DAEMON_OPTIONS('Port-smtp,Name-TLSMTA,M-s')dnl

dnl #

dnl # 以下内容导致 sendsmail 额外监听 IPv6 回环

dnl # 设备。移除回环地址限制以监听网络。

dnl #

dnl #: 将 IPv4 和 IPv6 地址同时绑定到同一端口需要

dnl # 内核补丁

dnl #

dnl DAEMON_OPTIONS('Port-smtp,Addr-::1,Name-MTA-v6,Family-inet6')dnl

dnl #

dnl # 如果你想让自己免受垃圾邮件侵害，我们强烈建议不要接受无法解析的域名。

dnl # 然而，没有 24x7 DNS 的笔记本电脑和电脑用户确实需要此。

dnl #

dnl FEATURE(`accept_unresolvable_domains`)`dnl

dnl #

dnl FEATURE(`relay_based_on_MX`)`dnl

dnl #

dnl # 同样将发送到 `localhost.localdomain` 的邮件视为本地邮件。

dnl #

dnl LOCAL_DOMAIN(`localhost.localdomain`)`dnl

dnl #

dnl # 以下示例使来自此主机及任何额外指定的

dnl # 名的邮件看起来是从 mydomain.com 发送的。

dnl #

dnl MASQUERADE_AS(`mydomain.com`)`dnl

dnl #

dnl # 伪装不仅是表头，还包括信封头部

dnl #

dnl FEATURE(`masquerade_entire_domain`)`dnl

dnl #

dnl # 伪装不仅是 @mydomainalias.com，还包括 *.mydomainalias.com

dnl #

dnl MASQUERADE_DOMAIN(localhost)``dnl

dnl MASQUERADE_DOMAIN(localhost.localdomain)``dnl

dnl MASQUERADE_DOMAIN(mydomainalias.com)``dnl

dnl MASQUERADE_DOMAIN(mydomain.lan)``dnl

dnl MAILER(smtp)``dnl
```
