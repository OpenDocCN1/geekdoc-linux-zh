
```
Country Code (2) [letters]: US
State or Province (full) ]:California
Locality Name (eg, city): ]:San Francisco
Organization Name (eg, company, recommended): ]:Sobell Associates Inc.
Organization Unit Name (eg, section): []
Server name (eg. ssl.domain.tk; required): ]:bell.com
Email Address ]:example@sobell.com
```

[!] 可以在 `/usr/share/doc/exim4-base/` 查看为 exim 生成签名证书的示例，以了解如何在你的邮件传输代理中启用 TLS 支持。

你可以在证书中输入任何你想要的信息。

## 在 exim 中启用 SSL

一旦你有了证书，请在 `/etc/exim4` 目录下创建一个名为 `exim4.conf.localmacros` 的文件（你需要具有 root 权限操作）。使用以下内容，这将指示 exim 使用 SSL 证书：

```
$ cat /etc/exim4/exim4.conf.localmacros
MAIN_TLS_ENABLE = 1
```

由于 SSL 将进行中继，你需要在 `dc_relay_hosts` 变量中添加发送邮件的系统名称（见第 726 页）。重启 exim4（见第 716 页）。

## 在邮件客户端中启用 SSL

在邮件客户端中启用 SSL 非常简单。例如，Evolution 具有“编辑>偏好>邮件账户>发送邮件>安全>使用安全连接”复选框，它允许你选择想要使用的加密类型：不加密、SSL 加密或 TLS 加密。点击“检查支持类型”按钮（位于此组合框下方）将查询服务器并设置 Evolution 使用服务器支持的安全和身份验证类型。

## 章节总结

`exim4` 守护进程是一个 MTA（邮件传输代理）。当你发送消息时，`exim4` 与其他软件协作将邮件发送给正确的收件者。你可以设置 `exim4` 将邮件发送到 SMTP 服务器，由该服务器将邮件中继到目的地，或者让 `exim4` 直接向接收邮件的域名的 SMTP 服务器发送邮件。默认情况下，`exim4` 将入站邮件存储在邮件池目录 `/var/mail/` 中。

`/etc/exim4/update-exim4.conf` 文件控制 `exim4` 工作的许多方面。当你编辑此文件时，必须使用 exim 脚本重启 `exim4`。系统管理员可以使用 `/forward` 文件，而普通用户可以将邮件重定向到一个或多个本地地址、过滤器或程序。

你可以使用像 `SpamAssassin` 这样的程序对邮件进行评分并根据其成为垃圾邮件的可能性进行标记。然后你可以决定如何处理标记过的邮件：你可以查看每封垃圾邮件并决定将其放在哪里，或者让你的 MUA 自动将垃圾邮件放入特殊的垃圾邮件箱。

其他可以帮助邮件的程序包括提供 Web 服务的 `SquirrelMail` 和提供邮件列表支持的 `Mailman`。`IMAP`（互联网消息访问协议）和 `POP`（邮局协议）允许用户远程检索和处理邮件。`Dovecot` 系统提供了 IMAP 和 POP 服务器。

# 练习题

- 1. 默认情况下，发送给系统的邮件会发送到 root。你如何在 `/var/logs/systemmail` 中也保存一份副本？

- 2. Max 如何在 mbox 中存储其邮件副本并发送一份副本到 `max@example.com`？

- 3. 如果你的防火墙只允许 IP 地址为 `192.168.1.1` 的机器向网络外发送邮件，你将如何指示本地的 `exim4` 使用该服务器作为中继站？

- 4. 描述 `/etc/exim4/update-exim4.conf` 中用于 smarthost 的变量如何影响 `exim4` 的行为。当你将此变量设置为 `internet` 时会发生什么？

- 5. 你的邮件服务器上安装了 `SpamAssassin`，但阈值被设置为 3 这一异常低的值，导致了大量的误报。你可能会给你的邮件客户端提供什么规则，允许它识别分数为 5 分或更高的垃圾邮件？

- 6. 描述 Max 向远程 Linux 系统上的 Sam 发送邮件时使用的软件和协议。

## 进阶练习

- 7. 解释配置 `exim4` 使用拆分配置（split configuration）与配置其使用非拆分配置（unsplit configuration）之间的区别。为了设置每种类型的配置你需要修改哪些文件？列出两个两种配置都会读取的文件。

- 8. 假设一个脚本在名为 `RESULT` 的变量中存储了某些信息。在脚本中放置哪行代码可以将 `RESULT` 的内容发送到命令行第一个参数指定的邮件地址？

- 9. 提供一种在涉及使用 MUA 的情况下来读取你邮件的简单方法。

- 10. 描述 `spamassassin`、`spamd` 和 `spamc` 之间的关系。它们各自是如何工作的？为什么不直接单独使用 `spamassassin` 工具？

# 21

## NIS 和 LDAP

# 本章内容

- NIS 如何工作........................................... 742
- 运行 NIS 客户端....................................... 744
- NIS 密码更改....................................... 750
- NIS 密码.............................................. 757
- 设置 NIS 服务器...................................... 750
- NIS 守护进程....................................... 756
- LDAP.................................................. 758
- 与 LDAP 操作的其他工具.................................. 767

NIS（网络信息服务）的主要目标是使网络透明化。这种透明性的一个方面是当用户登录不同机器时提供相似的环境，包括用户名和密码。不应该被复制，而是应该放在中央位置。另一个客户端/服务器设置示例，LDAP（轻量级访问协议）适用于相对静态的信息。

## NIS 如何工作

NIS 不在网络上加密数据——它以明文传输数据。

NIS 为网络上的系统提供一组公共信息。该网络被称为 NIS 域，其特征是每个系统具有相同的 NIS 域（不同于 DNS 域）。技术上，NIS 由映射（数据库）组成。每个 NIS 域必须有一个主服务器；较大的网络可能有从服务器。每台从服务器持有主服务器 数据库的副本。对从服务器的需求取决于 NIS 域的大小和系统的可靠性。一个系统一次只能属于一个 NIS 域。

# NIS 743 简介

（本地配置信息和 NIS 源信息。）NIS 服务器可以根据需要包含以下多个源文件的信息：

- `/etc/group` 定义组及其成员
- `/etc/shadow` 为组提供影子密码
- `/etc/hosts` 映射本地系统和 IP 地址
- `/etc/passwd` 列出用户信息
- `/etc/printcap` 列出打印机信息
- `/etc/rpc` 映射 RPC 程序名称和编号
- `/etc/services` 映射系统服务名称和端口号
- `/etc/shadow` 为用户提供影子密码

NIS 提供的信息基于随时间推移变化的文件。NIS 会及时向 NIS 域内的所有系统提供更新的信息。

NIS 映射 (Map)：在 NIS 使用该文件之前，必须将其转换为 dbi（第 14 页）格式的文件，称为 map。每个 map 都按一个字段（列）进行索引。可以通过指定来自索引字段的值来检索 map 中的记录（行）。某些文件会生成两个 map，每个映射对应不同的字段。例如，`/etc/passwd` 文件生成两个 map：一个按用户名索引，另一个按 UID 索引。这些 map 命名为 `passwd.byname` 和 `passwd.buid`。

可选的 NIS maps对应 C 库函数。`getpwnam()` 和 `getpuid()` 函数在非 NIS 系统上从 `/etc/passwd` 获取用户名和 UID 信息。在 NIS 系统上，这些函数通过向 NIS 服务器执行 RPC 调用，该过程对应用函数是透明的。

Map 名称：NIS 使用的文件位于主服务器的 `/var/yp/nisdomain-directory` 目录中，其中 `nisdomainname` 是 NIS 域的。本章中的示例使用了名为 `mgs` 的 NIS 域：
