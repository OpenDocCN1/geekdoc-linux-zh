

## 第 9 章 | 网络应用安全

## 商业版 Sendmail

开源 sendmail 服务器的创建者 Eric Allman 创立了 Sendmail, Inc.，该公司赞助了致力于将产品扩展到企业级的开发者。此外，Sendmail, Inc. 还创建了许多包含商业代码的商业产品。这些代码大部分最终都会作为开源软件发布并集成到开源 sendmail 中。尽管如此，商业版 Sendmail 是一个不同的产品。

正如 [http://www.sendmail.com/sm/solutions/]( 所示，商业版 Sendmail 产品涵盖四个领域：

- 网关保护——包括在邮件被接受到网络之前对其进行过滤、处理和控制的选项。
- 入站保护——对清洁且经过身份验证的电子邮件规定特定要求。
- 出站保护——支持出站电子邮件符合组织策略。
- 内部保护——处理同一网络上的多个网域。

如你所见，商业版 Sendmail 产品的功能在许多方面都超越了开源 sendmail 软件。

## Postfix 替代方案

由于开源 sendmail 软件的复杂性，许多管理员倾向于使用替代方案。一个相对流行的开源替代方案是 Postfix。它是 Ubuntu 和 SUSE Linux 发行版的默认 MTA（邮件传输代理）。配置 Postfix 的方法各异。例如，在 Ubuntu 系统上，以下命令提供了若干个配置此 MTA 的提示：

```bash
# dpkg-reconfigure postfix
```

基本选项包括：

- Internet 站点——配置 Postfix 使用 SMTP 发送和接收电子邮件。
- 带有智能主主机的 Internet——将协议型 MTA 与 Postfix 集成。
- 卫星系统——将 Postfix 设置为将电子邮件传输到不同的系统。
- 仅限本地——将 Postfix 配置限制为本地系统的用户。

本节假设你已经选择了 Internet with smarthost，这是 Postfix 选项中功能最强大的。一旦选择，系统会提示输入以下信息：

1. 此 Postfix 服务器涵盖的域名，例如 example.org
2. 用于出站邮件的中继主机，作为 ISP 的 SMTP 服务器（如果此邮件服务器不是卫星系统，你可以选择留空）
3. 实际邮件管理员的电子邮件地址
4. 由此服务器管理的网域和主机名列表
5. 是否强制同步更新，除非 Internet 连接不可靠，否则没有必要
6. 由此服务器管理的 IP 地址网络列表；示例列表如下所示所示：
   127.0.0.0/8 192.168.0.0/24 10.100.0.0/16
7. 是否配置 procmail 用于本地投递，到本地用户账户的相应目录
8. 邮箱箱大小限制，单位为字节
9. 本地扩展（很少更改）

在这些步骤中做出的选择将写入 /etc/postfix/ 目录下的 main.cf 文件中。查看此文件。你可能想再更改一些内容。例如，以下指令将拒绝向任何黑客提供有关服务器的信息：
`smtpd banner = "some email service"`

如果你想用 SSL 或 TLS 证书来保护此服务，可以使用以下指令：
`smtpd_tls_cert_file = /etc/ssl/certs/mail.pem`
`smtpd_tls_key_file = /etc/ssl/private/mail.key`

## 第 2 部分 | 分层安全与 Linux

