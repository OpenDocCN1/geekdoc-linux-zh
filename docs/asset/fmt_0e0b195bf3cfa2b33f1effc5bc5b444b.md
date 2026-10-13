
`http_access` 选项的顺序非常重要。Squid 从第一条开始逐向下执行，直到遇到第一个匹配的 ACL 目的 `http_access` 选项时停止。在前面的示例中，匹配第一个 `http_access` 命令的本地系统被允许访问，而其他系统将进入第二个 `http_access` 命令并被拒绝。

对于使用代理的系统，你还可以控制它们可以访问哪些网站。对于目标地址，你可以创建一个带有 `dst` 饰符的 `acl` 条目。`dst` 饰符以站点地址作为参数。然后，你创建一个 `http_access` 选项来控制对该地址的访问。以下示例禁止任何使用代理的用户访问目标站点 `rabbit.mytrek.com`。如果你有本地网络通过代理访问 Web，可以使用此类命令来限制对某些网站的访问。

```
acl myrabbit dst.mytrek.com
http_access deny myrabbit
```

这里显示了 `squid.conf` 文件中已经定义的 `http_access` 条目，以及一个针对 `myelan` 网络的条目。拒绝外部用户的访问，而允许本地网络上的主机和本地主机（Squid 服务器主机）访问。

```
http_access allow localhost
http_access allow myelan
http_access deny all
```

你也可以通过域名对地址进行限定。通常，可以使用域名直接引用 Web 网站。例如，一个名为 `mybeach.com` 的站点仅需域名 `mybeach.com` 即可引用。要创建一个引用域名的 `acl` 条目，分别对目标域和源域使用 `dstdomain` 或 `srcdomain` 选项。记住，这种引用指的是该域内的所有主机。针对 `mybeach.com` 的 `dstdomain` 选项 `acl` 条目会限制访问 `www.mybeach.com`、`ftp.mybeach.com`、`surf.mybeach.com` 等等。以下示例限制了对 `www.mybeach.com` 站点以及 `mybeach.com` 域名内所有其他 `*.mybeach.com` 站点和主机的访问：

```
acl thebeach dstdomain .mybeach.com
http_access deny thebeach
```

你可以在 `acl` 条目中列出多个域名或地址以将其作为一个组引用，但你不能让其中一个是另一个的子域名。例如，如果 `mybeachblanket.com` 是 `mybeach.com` 的子域名，则不能在同一个 `acl` 列表中同时列出它们。以下示例限制了对 `mybeach.com` 和 `mysurf.com` 的访问：

```
acl beaches dstdomain .mybeach.com .mysurf.com
http_access deny beaches
```

`acl` 条目还可以使用模式来指定特定的地址和域名。在以下示例中，拒绝任何包含“chocolate”模式的 URL 访问，但允许所有其他访问：

```
acl Chocl url_regex chocolate
http_access deny Chocl
http_access allow all
```

## 第五部分：红帽服务器

代理服务器。`httpd_accel_uses_host_header` 指令用于实现透明缓存；对于反向代理缓存应将其关闭。

```
http_port 80 # Squid 代理端口
httpd_accel_host 172.16.1.115 # Web 服务器的 IP 地址
httpd_accel_port 80 # Web 服务器的端口
httpd_accel_single_host on # 将未缓存请求转发到主机
httpd_accel_with_proxy on #
httpd_accel_uses_host_header off
```

如果你的 Squid 代理服务器和 Web 服务器运行在同一主机上，你需要指定 Web 服务器正在使用的端口。该端口不能与 Squid 的端口相同。在以下示例中，Web 服务器使用端口 81，而 Squid 使用端口 80。

```
http_port 80 # Squid 代理端口
httpd_accel_host localhost # Web 服务器的 IP 地址
httpd_accel_port 81 # Web 服务器的端口
```

此外，外部网络的 DNS 条目将使用代理服务器的 IP 地址作为 Web 服务器主机，将所有 Web 服务器请求指向代理服务器。内部网络的 DNS 条目将使用 Web 服务器的 IP 地址作为 Web 服务器主机，允许代理将未缓存请求重定向到 Web 服务器。如果你的网络只使用一个 DNS 服务器，可以设置 Split DNS 服务器来指定内部和外部地址（参见第 34 章）。

# 第 24 章：邮件服务器：SMTP、POP 和 IMAP

邮件服务器为 Internet 用户提供电子邮件服务。它们有自己的 TCP/IP 协议，例如简单邮件传输协议（SMTP）、邮局协议（POP）和互联网邮件访问协议（IMAP）。消息通过为本地域服务的邮件服务器在 Internet 上传输。一个域名可以被看作是大型互联网的子网，它有自己的服务器来处理从该子网发送或为该子网接收的邮件。当邮件用户发送消息时，消息首先从其主机系统发送到邮件服务器。然后，邮件服务器将消息发送到 Internet 上另一台邮件服务器，即为接收者用户所在的子网服务的服务器。接收邮件服务器随后将消息发送给收件者的主机系统。

在每个阶段，都会使用不同的代理（程序）进行不同类型的的操作。邮件用户代理（MUA）是一个邮件客户端程序，例如 `mail` 或 `Elm`。通过 MUA，用户编写邮件消息并发送。而当邮件传输代理（MTA）在 Internet 上传输消息时，MTA 是在 Internet 上发送 SMTP 消息的邮件服务器。

# 446 第五部分：红帽服务器

| 表 24-1 代理 | 描述 |
| --- | --- |
| 邮件传输代理 Sendmail | Sendmail 邮件传输代理 `www.sendmail.com` |
| Postfix | 一种快速、易于配置且安全的邮件传输代理，兼容 Sendmail 并旨在取代它 `www.postfix.org` |
| Qmail | 一种快速、灵活且安全的 MTA，拥有自己的实现方式，并能与 Postfix 竞争 `www.qmail.org` |
| Exim | 基于 mail3 的 MTA `www.exim.org` |
| Courier | Courier MTA `www.courier-mta.org` |
| 邮件传输代理切换器 | 红帽工具，用于让你在 Sendmail 和 Postfix 之间进行切换（系统设置菜单和窗口中的“邮件传输代理切换器”） |

### 邮件服务器

Red Hat Linux 会自动为你安装并配置 Sendmail 和 Postfix。在启动系统时，你可以使用 Sendmail 或 Postfix 在本地用户之间发送和接收消息。红帽包含了一个名为“邮件传输代理切换器”的特殊工具，可以通过系统设置菜单或窗口访问，以便在两者之间进行切换。你还可以设置你的 Linux 系统运行 POP 服务器。POP 服务器会保存用户的邮件，直到他们登录并访问消息，而不是直接发送到他们的主机。本章将同时讨论 Postfix 和 Sendmail。

Courier 是一个快速、轻量且安全的 MTA，它保持了与 Sendmail 的兼容性。Courier 软件包还包括 POP、IMAP 和 Web 邮件器服务器以及邮件服务。它支持广泛的身份验证方法，包括影子密码、PAM 和 LDAP。

Qmail 也是一个快速且安全的 MTA，但它与 Sendmail 的兼容性很小。与 Postfix 一，它采用模块化设计，使用自己的配置和维护文件来处理每个邮件任务。它还关注安全、速度和易于配置。

> 注意：在单个独立系统内发送的邮件需要一个环回接口。大多数 Linux 发行版（包括红帽）会在安装过程中自动为你完成此操作。环回接口允许你的系统识别自身，从而允许它向自身发送和接收邮件。环回接口使用主机名 `localhost` 和为本地系统预留的特殊 IP 地址 `127.0.0.1`。你可以检查你的 `hosts` 文件，查看你的环回接口是否已配置为本地主机。你应该看到 `127.0.0.1 localhost` 列在第一条位置。

# 第 24 章：邮件服务器：SMTP、POP 和 IMAP 447

# 接收到的邮件记录
