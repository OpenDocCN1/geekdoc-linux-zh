
### 步骤 2
一旦创建了 `/etc/init.d/exim` 脚本文件，确保其具有可执行权限、更改其默认权限、创建必要的链接并启动它是非常重要的。文件可执行将允许系统运行它，出于安全考虑，更改其默认权限仅允许 root 用户更改，而创建符号链接将允许进程控制 Linux 的初始化，初始化负责在系统启动时启动需要运行的所有正常和授权进程，并在每次重启时自动为你启动该程序。

- 要使其变为可执行并更改默认权限，请使用命令：
`[root@deep #] chmod 700 /etc/init.d/exim`
`[root@deep #] chown root:root /etc/init.d/exim`

- 要为 Exim 创建符号链接，使用以下命令：
`[root@deep #] chkconfig --add exim`
`[root@deep #] chkconfig --level 2345 exim on`

- 要手动启动 Exim 软件，使用以下命令：
`[root@deep #] /etc/init.d/exim start`
正在启动 Exim:
[OK]

# 测试 Exim

一旦我们的服务器配置并启动，我们必须运行一些测试以确保 Exim 在我们的系统上正常工作。所有测试都必须成功完成，否则你将丢失邮件。第一个测试是检查 Exim 的运行配置文件在语法上是有效的，其他是进行路由测试，以确保我们可以在本地或远程发送和接收邮件。

再次强调，所有测试必须成功完成，否则在使用邮件服务器收发消息时可能会遇到问题。为了成功完成测试，我们必须作为超级用户 `root` 在服务器终端上执行所有测试。

## 测试 1 - 检查 Exim 的运行配置文件语法上是否有效

在本次测试中，我们将检查 Exim 的运行配置文件在语法上是否有效且不包含任何错误。

- 要检查 Exim 的运行文件语法上是否有效，请使用以下命令：
`[root@deep #] /usr/bin/exim -bv`
Exim version 4.05 built 13-May-2002 01:36
Copyright (c) University
如果配置文件有错误，Exim 将输出错误信息。否则，它只输出版本号和日期。

## 测试 2 - 验证 Exim 识别本地邮箱

在本次测试中，我们验证 Exim 在系统上可以识别本地邮箱。

- 要验证 Exim 识别本地邮箱，请使用以下命令：
`[root@deep #] /usr/bin/exim -bt postmaster@domain.com`
postmaster@domain.com
router = local
transport = local_delivery
delivery = true

## 测试 3 - 验证 Exim 识别远程地址

在本次测试中，我们应该验证 Exim 在互联网上可以识别远程地址。

- 要验证 Exim 识别远程地址，请使用以下命令：
`[root@deep #] /usr/bin/exim -bt myaccount@hotmail.com`
myaccount@hotmail.com
router = dnslookup
transport = remote_smtp

## 测试 4 - 让 Exim 本地交付

在本次测试中，我们验证 Exim 在系统上可以本地交付。我们通过直接将消息传递给 Exim 来实现，而不是通过外部代理（MUA）。

- 要验证 Exim 本地交付 `-v`，请使用以下命令：
```bash
root@deep #]# /usr/bin/exim -v postmaster@domain.com
```
From: sysadmin@domain.com
To: postmaster@domain.com
Subject: Testing Exim

This is a message.
^C
LOG: MAIN
<=smtp.domain.com U=root S=338
[root@smtp]# LOG: MAIN
> sysadmin <postmaster@domain.com>
Completed

"`v`" 选项允许 Exim 输出一些它正在执行的操作。在这种情况下，你会看到三行日志：一条关于消息的，一条关于交付的，以及一条包含 "Completed" 的。

## 测试 5 - 让 Exim 远程交付

在本次测试中，我们应该验证 Exim 在互联网上可以远程交付。我们通过直接将消息传递给 Exim 来实现，而不是通过外部代理（MUA）。

- 要验证 Exim 远程交付，请使用以下命令：

```bash
root@]# /usr/bin/exim -v myaccount@hotmail.com
```

From: sysadmin@domain.com

To: myaccount@hotmail.com

Subject: Testing Exim

This is a test message.

^D

LOG: MAIN

<= root@domain.com U=root S=324

[smtp] Connecting to mx08.hotmail.com [64.44.97]:25 connected

2<< 220-Hotmail (NO UCE) SMTP server ready for on 13 May 2002

21:23:32 -0700

220 SMTP spoken here

SMTPS>> EHLO spike here

SMTPS<< 250-hotmail.com Hello

250-bitime

250 SIZE 1572864

SMTPS>> MAIL FROM:sysadmin@domain.com> SIZE=1357

SMTPS<< 250 Requested mail action ok, completed

SMTPS>> TO:<myaccount@hotmail.com>

SMTPS<< 250 Requested mail action ok, completed

SMTPS>> DATA

SMTPS<< 354 Start mail input; end with <CRLF>.<CRLF>

SMTPS>> writing message and terminating "

SMTPS<< 250 Requested mail action ok, completed

SMTPS>> QUIT

LOG: MAIN

=> myaccount@hotmail.com R=dnslookup T=remote smtp H=mx08.hotmail.com

[64.49.7]

LOG: MAIN

Completed

^C

# 允许用户在中继之前进行身份验证

中继邮件服务器是非常危险的，也是垃圾邮件发送者滥用你系统的首选功能。Exim 默认内置反中继（Anti-Relay）功能。这意味着你不能直接使用它向他人发送邮件，必须在 Exim 允许中继之前进行身份验证。尝试使用你偏好的 MUA（邮件客户端）向朋友发送消息，你会发现消息投送失败。Exim 有多种身份验证方法，取决于你想要使用哪种方法并允许中继。

像 POP-SMTP 这样的方法在互联网上已经存在，但某些 MUA 软件需要破解邮件软件的源代码，这并不是我真正喜欢的解决方案。还有其他方法，例如使用 `SMTP_AUTH`，这就是我们在这里使用的方法，它与市场上所有的 MUA 都兼容。

> 注意：有关 POP-SMTP 的更多信息，请参见：http://whoson.sourceforge.net

中继前的验证意味着用户在访问服务器获取邮件时必须经过身份验证。在所有情况下，这都是通过连接到 POP 或 IMAP 服务器来实现的。`SMTP_AUTH` 验证的工作原理如下：

- 1. 用户连接到服务器上的 POP 或 IMAP 账户以获取/发送邮件。
- 2. 用户通过其 POP 或 IMAP 服务器发送邮件，Exim 要求输入用户名和密码。
- 3. 用户的 MUA 将用户名和密码发送给 Exim。
- 4. Exim 与其处理用户用户名和密码的文件进行比对。
- 5. 如果用户名和密码匹配，Exim 允许通过邮件服务器进行中继。
- 6. 如果用户名和密码不匹配，Exim 将发送错误信息。

在我们的配置中，我们将允许用户通过 `SMTP_AUTH` 进行中继。据我所知，MS Outlook 和 Netscape 使用这种身份验证，但许多其他 MUA 也在使用。这里的好消息是，我们不需要安装任何外部程序，因为 Exim 对 `SMTP_AUTH` 有原生支持。

我们将被允许的用户名和密码存储在一个名为 `exim.auth` 的文件中。我知道 SQL 数据库对于 ISP（服务提供商）来说更合适，但我无法解释这一过程，这超出了本书的范围。因此，我们将使用 `exim.auth` 文件，但在 SQL 数据库或文件中存储用户名和密码的步骤是相同的，仅在 `exim.conf` 文件中添加配置行不同。

# 将 SMTP_AUTH 集成 Exim 的必要步骤：

让 `SMTP_AUTH` 在 Exim 中运行的操作并不困难，大部分工作将发生在 `exim.conf` 文件内部。

### 步骤 1
首先，我们必须在这个默认配置文件中包含身份验证器规范。在 `exim.conf` 文件的 "Authentication Configuration" 部分添加以下行即可实现。

在 "Authentication Configuration" 部分的末尾添加以下行。

- * 编辑 `exim.conf` 文件 (`vi /etc/mail/exim.conf`) 并在 "Authentication Configuration" 部分末尾添加如下内容：
```
# Netscape Messenger 使用的 AUTH PLAIN 身份验证方法

plain:

driver = plaintext

public_name = PLAIN

server_condition = "${if and {eq${$2}}{{eq${$3}}} \
crypt${$2}$(extract{$1}:1)) \
${lookup${$1}search(/etc/mail/exim.auth) \
${value}(:*))}}{1}{0}"
```

### 步骤 2
其次，我们必须创建一个处理所有邮件用户名和密码的 `exim.auth` 文件。由于我们在 Linux 系统上使用 PAM，用户名和密码存储在 `/etc/shadow` 文件中而不是 `/etc/passwd` 文件中。这意味着我们必须在 `/etc/mail` 目录下制作 shadow 文件的副本并命名为 `exim.auth`。

- * 可以可以通过命令完成：
`[root@deep]# cp /etc/shadow /etc/mail/exim.auth`

### 步骤 3
出于安全考虑，现在将 `exim.auth` 文件的权限模式设置为 (0640/-rw-r-----)，所有者为超级用户 'root'，组权限设置为 'mail'。

- * 要更改 `exim.auth` 文件的权限和所有者，请使用命令：
`[root@deep]# chmod 640 /etc/mail/exim.auth`
`[root@deep]# chown root.mail /etc/mail/exim.auth`

### 步骤 4
`/etc/shadow` 管理 Linux 服务器上的所有用户账户，简单地将其复制到 `/etc/mail/exim.auth` 文件是非常危险的。如果邮件服务器以任何方式被破坏，黑客将获得所有用户账户，并能够使用某些密码破解软件获取密码。因此，我们必须编辑并删除与系统账户 "root"、bin" 以及未提供邮件账户的用户相关的行。

总结一下，你必须编辑 `exim.auth` 文件并**仅保留**该文件中与具有服务器邮件访问权限的用户相关的行。任何其他行，例如 "root"、"nobody"，应该被完全删除。

- * 编辑 `exim.auth` (`vi /etc/mail/exim.auth`) 并删除任何你不希望访问邮件服务器的行。
```
root:$1lHNPf/K/A#$JFeW8B7Qf4F.ZX0/H::$1

bin:

daemon:

nobody:

sync:

mail:

lp:
```

### 步骤 5
最后，我们必须重启 Exim 使更改生效。

- * 要重启 Exim，请使用以下命令：
`[root@deep]# /etc/init.d/exim restart`
Shutting down Exim: [OK]
Starting Exim: [OK]

# Exim 3 第 0 章

### 步骤 2
一旦创建了私钥，我们必须使用服务器的 RSA 私钥生成证书签名请求 (CSR)。下面的命令将提示你输入证书的 X.509 属性。如果你希望由 Thawte 或 Verigen 等商业证书授权机构 (CA) 签名你的证书签名请求 (CSR)，你需要将生成的 CSR 文件提交到 Web 表单中进行签名，并等待签后的证书。

- 要生成 CSR，请使用以下命令：
`[root@deeps$] openssl req -new -key smtp.key -out smtp.csr`

使用来自 `/usr/share/opens.cnf` 的配置
你将被要求输入将整合到证书中的信息。
你需要输入的内容被称为区分名称（Distinguished Name，简称 DN）。
有很多字段，但你可以留一些空值。
某些字段会有默认值，如果你输入 `,`，则该字段将留空。
国家名称（两位字母代码） [CA]:
州或省份名称（全称） [Quebec]:
位置（例如城市） [Montreal]:
组织名称（例如公司） [OpenNA.com SMTP Server]:
组织单元名称（例如部门） [:
通用名称（例如，你的名称） [smtp.openna.com]:
电子邮件地址 [noc@openna.com]:

请输入以下随你的证书请求一同发送的“额外”属性：
挑战密码 []；
可选公司名称 []:

> 警告：当 OpenSSL 提示你输入“通用名称”（Common Name）时，请确保你已输入了 SMTP 服务器的完全限定域名 (FQDN)。

### 步骤 3
只有当你想要用自己的 CA 签名 csr 证书密钥时，才需要此步骤。现在，我们必须使用我们已经为生成 Web 服务器证书而创建的证书权威机构 (`ca.crt`) 来签名证书。如果签名的 CA 证书不存在，请参阅 OpenSSL 章节获取有关如何创建它的更多信息。

- 要使用你自己的 CA 签名 csr 证书，请使用以下命令：
`[root@deeps$] ~ /usr/share/ssl/misc/sign smtp.csr`

CA 签名：smtp.csr ~ smtp.crt:
使用来自 `ca.cnf` 的配置
输入 PEM 密语：
检查请求是否匹配
CA 签名成功
证书区分名称如下：
国家名称：CA
州或省份名称：Quebec
位置：Montreal
组织名称：OpenNA.com SMTP Server
通用名称：smtp.openna.com
电子邮件地址：noc@openna.com

签名证书？[y/n]

```
写入新条目

数据库更新

CA 验证：smtp.crt

证书：OK
```

> 警告：如果你收到消息说你尝试签名的 csr 证书已存在，那么在使用自己的 CA 签名之前，你至少必须更改该证书信息。

### 步骤 4
接下来，我们需要创建一个存放密钥的 `certs` 目录。该目录应该在 `/etc/mail` 目录下创建，所有的 Exim 文件都在那里。

默认情况下，`certs` 目录不存在，必须创建。

- 要创建 `certs` 目录，请使用以下命令：
`[root@]# mkdir -p /etc/mail/certs`

### 步骤 5
现在，将证书目录的权限模式设置为 700 (drwx------) 并属于 "mail" 用户，以便允许 Exim 访问其中的证书。

- 要更改 `certs` 目录的权限和所有权，请使用：
`[root@]# chmod 700 /etc/mail/certs/`
`[root@]# chown mail /etc/mail/certs/`

### 步骤 6
最后，我们必须将 `smtp.key` 和 `smtp.crt` 证书文件放在正确的目录，以便 Exim 在启动时找到它们。

- 将证书放入正确的目录，请使用以下命令：
`[root@]# mv smtp.key /etc/mail/certs/`
`[root@]# mv smtp.crt /etc/mail/certs/`
`[root@]# chmod 400 /etc/mail/certs/smtp.key`
`[root@]# chmod 400 /etc/mail/certs/smtp.crt`
`[root@]# chown mail /etc/mail/certs/smtp.key`
`[root@]# chown mail /etc/mail/certs/smtp.crt`
`[root@]# rm -f smtp.csr`

# Exim 3
第 0 章节

```
check_auth:

accept hosts = +auth_over_tls_hosts

 endpass

 message = STARTTLS required before AUTH

  encrypted = *
```

> ################################################################
# 路由器配置 (ROUTERS CONFIGURATION)
# 指定如何处理地址
##################################################################
# 路由定义的顺序非常重要！
# 地址将依次传递给每个路由器，直到被接受。
##################################################################

```
begin routers

dnslookup:
```
