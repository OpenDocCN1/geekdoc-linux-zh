
你有两个不同的参数可以配置：

- `pwcheck_method`—将此参数设置为 `saslauthd` 可配置 `saslauthd` 进程对 SMTP 用户进行身份验证。
- `mech_list`—此参数指定了用于登录 SMTP 用户的身份验证机制。你可以使用以下机制：

- `plain`—明文身份验证机制以明文形式发送用户名和密码。如果你选择此机制，还应该配置系统使用 TLS 对在客户端和服务器之间传输的数据进行加密。
- `login`—`login` 身份验证机制用于支持使用名为 LOGIN 的 SMTP 验证方案的旧版 MUA 客户端软件。
- `digest-md5`—这种身份验证机制使用 Digest 对 SMTP 用户进行身份验证。要在此使用此参数，你必须配置 `/etc/sysconfig/saslauthd` 中的 `SASLAUTHD_AUTHME` 参数以使用 Digest 身份验证。
- `kerberos`—当你在 Linux 服务器上实现了 Kerberos 领域时，使用这种身份验证机制。

## Postfix 简介

要配置你的 Postfix 实现使用 Cyrus SASL 对 SMTP 用户进行身份验证，请完成以下操作：

1. 验证服务器上已安装适当的 `cyrus-sasl` 软件包。
2. 编辑你的 `/etc/sysconfig/saslauthd` 文件并配置 `SASLAUTH_AUTHME` 参数。

提示
默认值 `pam` 对于大多数部署效果最好。

3. 编辑你的 `/usr/lib/sasl2/pdpd.conf` 文件并将 `pwcheck_method` 的值设置为 `saslauthd`。
4. 将 `mech_list` 的值设置为你在 `/etc/sysconfig/saslauthd` 中配置的身份验证方法。

提示
我建议从 `plain` 和 `login` 的默认值开始。这些最容易操作。在章节后后部分，我们将介绍如何使用 TLS 加密数据。

5. 用文本编辑器打开 `main.cf` 并进行以下更改：

   a. 通过设置 `smtpd_sasl_enable` 的值为 `yes`，配置 Postfix 使用 SASL SMTP 身份验证
   b. 通过设置 `security_options` 的值为 `noanonymous`，禁用任何 SMTP 身份验证
   c. 通过设置 `smtpd_recipient_restrictions` 的值为 `permit_sasl_authenticated, permit_mynetworks, reject_unauth destination`，启用 Postfix 为已验证的 SMTP 用户中继邮件。

6. 启动 `saslauthd` 进程并配置其在运行级别 3 和 5 时自动启动。
7. 重启 Postfix 服务。

此时，你的 Postfix 服务器已配置为使用 Cyrus SASL 服务器对 SMTP 用户进行身份验证。垃圾邮件发送者将消失！

要让基础 Postfix 邮件服务器运行的最后件事是配置 POP3/IMAP 支持。

## 第7章：在 SLES 9 上实现电子邮件服务

### 配置 IMAP 和 POP3 支持

正如我们在本章中多次提到的，Postfix 没有内置的 IMAP 或 POP3 支持。如果你想投递到本地邮件账户，这并不是问题。Postfix 可以做到。

然而，通常大多数组织都需要一个相当健壮的解决方案。你可能不想让用户 `ssh` 到你的邮件服务器来读取邮件。你可能更希望用户使用本地工作站上的邮件客户端发送和接收邮件。

发送部分不是问题。正如我们刚刚讨论的，Postfix 可以使用 SMTP 从 M 接收和发送邮件。然而，如果我们希望用户能够从 Postfix MTA 拉取他们的邮件，那么我们必须配合 Cyrus SASL 服务器和 Postfix 一起实现 POP3 和/IMAP 服务器，如图 7.20 所示。

图 7.20
为 Postfix 添加 POP3/IMAP 支持。

![](img/9a8db5c8d556a70e5a1096951da47eec_311_0.png)

有多种 POP3/IMAP 服务器软件包可以实现此功能。其中一些依赖于 Postfix 将收到的邮件存入邮件池目录 `mail spool directory`。当 MUA 通过 POP3 或 IMAP 协议连接时，POP3/IMAP 服务器从邮件池目录拉取消息并将其发送到邮件客户端。

这种类型的 POP3/IMAP 服务器通常必须与 Postfix 进程安装在同一台服务器上。它在较小的环境中运行良好。`WU-IMAP` 软件包就是这类服务器的示例。

另一方面，某些部署要求将 POP3/IMAP 服务器安装在网络中另一台 Linux 服务器上。对于这种实现方式，你需要使用如 Cyrus IMAP 服务器之类的包。该服务器使用本地邮件传输协议 `LMTP` 从 Postfix MTA 传输邮件。

提示
`LMTP` 协议基于 SMTP 协议。与 SMTP 不同，`LMTP` 设计用于本地网络传输邮件。由于它使用了 `LMTP`，Cyrus IMAP 服务器不需要消息存储在本地队列中。Cyrus IMAP 服务器在具有大量用户和服务器的环境中效果最好。在书中，我们将查看两种类型的 POP3/IMAP 服务器。让我们从 Cyrus IMAP 服务器开始。

### 实现 CYRUS IMAP 服务器

Cyrus IMAP 服务器通过安装 `cyrus-imap`、`perl-Cyrus` 和 `perl-Cyrus-SIEVE` 包来实现，如图 7.21 所示。

图 7.21
安装 Cyrus IMAP 服务器。
![](img/9a8db5c8d556a70e5a1096951da47eec_312_0.png)

配置 Cyrus IMAP 是简单的。要实现这一点，请执行以下操作：

1. 用文本编辑器打开 `/etc/cyrus.conf`，如图 7.22 所示。
2. 取消以下行的注释：
   `imaps`
   `pop3`
3. 确保存在如下行：
   `tmp cmd="lmtpd" socket=imap prefork=0`
4. 保存更改并关闭文件。
5. 在 shell 提示符输入 `cyrus restart` 重启 Cyrus IMAP 服务器。
6. 用文本编辑器打开 `/etc/postfix/master.cf`。

提示
`master.cf` 文件是 Postfix 进程的配置文件。

7. 验证是否存在 `lmtp` 协议的条目，语法如图 7.23 所示。

图 7.23
编辑 `/etc/postfix/master.cf`。

| service | type | private | n | max | user | command |
|---|---|---|---|---|---|---|
| cleanup | unix | - | n | 300 | 1 | root | cleanup |
| qmgr | fifo | - | n | 300 | 1 | root | qmgr |
| activatqp | fifo | - | n | 300 | 1 | root | oqmgr |
| bitmap | fifo | - | n | 0 | root | timmap |
| rewrite | unix | - | n | 0 | root | trivial-retrive |
| bounce | unix | - | n | 0 | root | bounce |
| refer | unix | - | n | 0 | root | bounce |
| choke | unix | - | n | 0 | root | choke |
| kerify | unix | - | n | 10000 | 7 | root | verify |
| flush | unix | - | n | 0 | root | fix |
| proxymag | unix | - | n | 0 | root | proxymag |
| relay | unix | - | n | 0 | root | smip |
| submission | unix | - | n | 0 | root | smip |
| showq | unix | - | n | 0 | root | showq |
| error | unix | - | n | 0 | root | error |
| local | unix | - | n | 0 | root | local |
| virtual | unix | - | n | 0 | root | virtual |
| intp | unix | - | n | 0 | root | intp |
| anvil | unix | - | n | 1 | root | anvil |
| localhost | inet | - | n | 1 | root | smtpd -o content |
| filter | unix | - | n | 0 | root | filter |

8. 保存任何更改并关闭文件。
9. 用文本编辑器打开 `/etc/postfix/main.cf`。
10. 滚动到 `mail_directory` 参数并删除其值，如图 7.24 所示。

图 7.24
编辑 `/etc/postfix/main.cf`。

```
# mail_directory = /usr/share/doc/postfix/mail_manual_pages

# message_directory = /var/share/mail

# home_directory = Postfix 示例配置文件的位置。

# 此参数从 Postfix 2.1 起已废用。

# spool_directory = /var/share/doc/postfix/samples

# readme = Postfix README 文件的位置。

# readme_directory = /var/share/doc/postfix/README_FILES

# canonical_maps = /etc/postfix/canonical

# virtual_maps = /etc/postfix/virtual

# relocated_maps = /etc/postfix/relocated

# transport_maps = /etc/postfix/transport

# sender_maps = /etc/postfix/sender, header_sender, header_recipient

# recipient_maps = /etc/postfix/recipient

# masquade_examples = envelope_sender

# message_size_limit = 0cf

# program_directory = /usr/lib/postfix

# inet_interfaces = 0.0.0.1

# domain_domains = 

# myhostname = hostname, localhost, Mydomain

# defer_transports = 

# disable_lookups = no
```

提示
此配置 Postfix 不将消息投递到邮件队列。

11. 滚动到 `mailbox_transport` 参数。
12. 将 `mailbox_transport` 参数设置为以下值：
    `mailbox_transport=lmtp:unix:/var/lib/imap/socket/lmtp`

注意
此参数指定 Postfix 使用 LMTP 将邮件消息传输到 Cyrus IMAP 服务器 `lmtp:unix:/var/lib/imap/socket/lmtp`，这是您在 `cyrus.conf` 文件中配置的地址。

13. 在文件末尾添加 `home_mailbox` 参数，但不要为其赋值。

注意
这将禁用本地邮件投递。

14. 保存更改并关闭文件。
15. 在 shell 提示符处输入 `rcpostfix` 来重启动 Postfix。

您也可以使用 YaST 配置 Postfix 使用 Cyrus IMAP 服务器。要执行此操作，请执行以下步骤：

1. 启动 YaST。
2. 在提示时，提供您的 root 用户密码。
3. 选择 网络服务，邮件服务器。
4. 输入启动 YaST 邮件服务器模块所需的密码。
5. 等待配置完成。
6. 在左侧框架中，选择本地投递 `Local Delivery`。显示图 7.25 中的屏幕。
7. 在本地投递类型 `Local Delivery Type` 下，勾选 Cyrus IMAP。
8. （可选但建议）在 安全 `Security` 下，勾选启用 `Enabled`。
9. 选择 OK

这就全部完成了！通过配置 SMTP 身份验证并将 Postfix 与 Cyrus IMAP 服务器集成，您简单的 Postfix MTA 变成一个非常强大且廉价的电子邮件服务器解决方案。

然而，我在这里展示的配置是一个简单的 Cyrus IMAP 服务器部署。请注意，我们在同一台服务器上配置了 Postfix 和 Cyrus IMAP。超出此基础配置可能会变得非常复杂。

图 7.25
配置 Cyrus IMAP 支持。
![](img/9a8db5c8d556a70e5a1096951da47eec_316_0.png)

注意
如果您想了解更多关于部署 Cyrus IMAP 的信息，请访问 http://as.web.cmu.edu/cyrus/imapd/。

如果您想实现简单的 POP3/IMAP 部署，请考虑使用 WU-IMAP 服务器。我们将讨论该服务。

### 实现 WU-IMAP 服务器

在您的 SLES 9 光盘上有一个基于 WU-IMAP 服务器的 POP3/IMAP 服务。要使用此服务，您需要配置 Postfix 将邮件消息投递到 `/var/spool/mail` 中的系统邮件队列。包提供的 IMAP 和/或 POP3 守护进程将从队列中提取消息并将其发送到 IMAP 和/或 POP3 电子邮件客户端。

您通过安装 `imap` 包来安装此服务器，如图 7.26 所示。

如果您已经安装了 Cyrus IMAP 服务器（这是 SLES 9 的默认配置），则在安装 `imap` 之前必须先卸载该包。

图 7.26
配置 WU-IMAP 服务器。
![](img/9a8db5c8d556a70e5a1096951da47eec_317_0.png)

安装包后，您需要配置该服务，然后配置 Postfix 以支持它。完成以下操作：

1. 为 WU-IMAP 服务器创建所需的安全证书：

   a. 打开终端会话并切换到 root。
   b. 在 shell 提示符处，输入 `openssl req -new -x509 -nodes -out imapd.pem -keyout imapd.pem`。
   c. 在提示时，提供证书所需的本地化信息。
   d. 在提示通用名称 `Common Name` 时，输入 Linux 服务器的 DNS 名称或 IP 地址。
   e. 在提示电子邮件地址时，输入您的管理员的电子邮件。
   f. 输入 `openssl req -new -x509 -nodes -out pop3d.pem -keyout pop3d.pem`。
   g. 在提示时，提供证书所需的本地化信息。
   h. 在提示通用名称时，输入 Linux 服务器的 DNS 名称或 IP 地址。
   i. 在提示电子邮件地址时，输入您的管理员的电子邮件。

2. 通过完成以下操作配置 POP3 和 IMAP 守护进程：

   a. 启动 YaST。
   b. 在提示时，提供您的 root 密码。
   c. 选择 网络服务，网络服务 `inetd`。
   d. 从列表中选择 `pop3`；然后选择状态 `Status`，如图 7.27 所示。

图 7.27
启用 POP3 服务。
![](img/9a8db5c8d556a70e5a1096951da47eec_318_0.png)

   e. 选择 `pop3`，然后选择状态。
   f. 选择 `imap`；然后选择状态。
   g. 选择 `inetd`，然后选择状态。
   h. 选择完成 `Finish`。
   i. 打开终端会话。
   j. 在 shell 提示符处，切换到 root。
   k. 在 shell 提示符处，输入 `rcinetd restart`。

3. 通过完成以下操作配置 Postfix 与 POP3 和 IMAP 服务集成：

   a. 在 YaST 中选择网络服务，邮件服务器。
   b. 输入启动 YaST 邮件服务器模块所需的密码。
   c. 等待配置完成。
   d. 在左侧框架中，选择本地投递 `Local Delivery`。显示图 7.25 中的屏幕。
   e. 在本地投递类型 `Local Delivery Type` 下，勾选 Cyrus IMAP。
   f. （可选但建议）在 安全 `Security` 下，勾选启用 `Enabled`。
   g. 选择 OK

## 实验 7.1：在 SLES 9 上配置 Postfix
