
## UNIX 系统管理入门进阶版

支持 IDENT 查询的最简单方法是使用带有 `rfc931` 选项的 Wrappers。例如，要为你的 SSH 服务器添加 IDENT 支持，可以使用以下 TCP Wrappers 配置：

```
- sshd: 127.0.0.1 : rfc931 : DENY
```

随后你将开始看到包含远程用户身份信息的日志，如下所示：

Apr 8 22:45:40 server1 sshd[22624]: refused connect from baduser@127.0.0.1

我们可以看到 `baduser` 正在尝试连接我们的服务器，但存在一个大问题：你现在正在信任来自站点的信息，而该站点本身可能已经被攻破。

另一个问题出现在 IDENT 的实现上。出于隐私和安全考虑，管理员应该保护其机器上用户的身份。现代 IDENT 实现包含了对用户名进行加密的支持；只发送一串看似随机的字符作为标识符。然而，当你将这串字符串发回给远程管理员时，他或她能够将该字符串解密为真实的用户名。

但通常情况下，IDENT 并没有广泛部署，许多管理员由于用户隐私考虑，选择在 Red Hat Linux 等系统上禁用它。此外，IDENT 主要局限于 Unix，因此你无法将其用于任何 Windows 客户端，而 Windows 客户端是互联网上的绝大多数。

# 联系远程站点管理员

在知道远程连接的地址后，你可以利用信息来确定该特定网络的联系人，并通知他们任何问题。执行此操作的首选方法是使用 `whois`，它将从各种权威来源查询官方联系信息。

# 使用 who 查找域名的联系信息

如果你知道站点的域名，可以使用 `whois` 查询 InterNIC（官方互联网名称注册机构）获取其联系信息。`whois` 命令的语法非常简单，如下：

```
whois [-h whois-server] domain
```

默认情况下，`whois` 会查询位于 `whois.internic.net` 的 InterNIC，但这只能告诉你在许多互联网名称注册机构中，哪一个包含该域名的权威信息。

```bash
$ whois example.com
```

`.com`、`.net` 和 `.org` 域名现在可以在许多不同的竞争注册处注册。访问 `http://www.internic.net` 获取详细信息。

域名：`EXAMPLE.COM`

注册局：`NETWORK SOLUTIONS, INC.`

`whois` 服务器：`whois.networksolutions.com`

引荐 URL：`http://www.networksolutions.com`

名称服务器：`B.IANA-SERVERS.NET`

名称服务器：`B.IANA-SERVERS.NET`

更新日期：`07-jan-2002`

>>> `whois` 数据库最后更新：2002年4月9日 星期二 16:57:15 EDT <<<

注册数据库仅包含 `.COM`, `.NET`, `.ORG`, `.EDU` 域名和注册局。

在前面的代码中，域名的注册局及其自身的 `whois` 服务器在 `Registrar` 和 `Whois Server` 字段中以 `加粗` 形式列出。你现在可以执行另一个命令，这次使用指定的服务器，如下：

```bash
$ whois -h whois.networksolutions.com example.com
```

注册人：

互联网数字分配局 (`EXAMPLE-DOM`)

4676 Admiralty Way, Suite 330

Marina del Rey, CA 90292

US

域名：`EXAMPLE.COM`

管理联系人、技术联系人、账单联系人：

互联网数字分配局 (`IANA`) `iana@IANA.ORG`

4676 Admiralty Way, Suite 330

Marina del Rey, CA 90292

US

310-823-9358

传真 310-823-8649

记录最后更新于 2002年7月7日。

记录过期于 2002年8月15日。

记录创建于 1995年8月9日。

数据库最后更新于 2002年4月9日。

以下是需要翻译的文本：

- `B.IANA-SERVERS.NET`

- `B.IANA-SERVERS.NET`
