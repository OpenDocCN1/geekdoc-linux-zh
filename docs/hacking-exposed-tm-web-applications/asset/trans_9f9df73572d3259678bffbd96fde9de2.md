

# 破解 Web 应用程序

表示用户已成功通过 Passport 服务身份验证，该验证使用 Passport 和合作伙伴共享的加密密钥进行加密。随后，客户端被重定向回 abc.com 的服务器，并提供身份验证 Cookie（cookie）。abc.com 服务器上的 Passport Manager 使用之前安装的共享加密密钥验证该身份验证 Cookie。总的来说，Passport 非常类似于基于表单（Forms）密码认证，其主要区别在于，它不是对比本地的用户名/密码列表，而是询问 Passport 服务凭据是否有效。

Passport 认证机制有许多变体，我们在这里不会涵盖；这些变体涉及位于合作伙伴网站上的登录表单、验证 Passport 的其他替代机制（例如 Outlook Express 验证 Hotmail.com 服务器）。此外还有其他与 Passport 相关的服务，包括快速购买（以前称为“钱包”）和儿童 Passport（Kids Passport）。关于这些服务的更多信息，请参阅本章末尾“参考文献和延伸阅读”部分的 Passport 链接。图 5-4 显示了基础 Passport 认证系统的图。以下是图 5-4 中每一步的相应细节。在步骤 1 中，客户端请求合作伙伴站点（在此例中为 my.msn.com）上的安全内容：

```
/my.ashx HTTP/1.0
Host: my.msn.com
```

![](img/2c61c2d28445b774d9266972920f432d_172_0.png)

图 5-4. Passport 单点登录 (SSI) 架构

在步骤 2 中，客户端被重定向到 http://login.passport.login.asp 的登录表单。Location 头中的查询字符串包含了请求源自合作伙伴站点的信息（id=）以及认证成功后返回的 URL（return URL，或 ru）。WWW-Authenticate 头显示为 Passport version1.4：

```
HTTP/1.1 302 Object Moved
Location: http://login.passport/login.asp?id=658&ru=http://my.msn.com/etc.
WWW-Authenticate: http://my.msn.com/etc.
```

在步骤 3 中，客户端从 login.passport.com 请求登录页面：

```
GET /login.asp?id=658&ru=http://my.msn.com/etc. HTTP/1.0
Referer: http://my.msn.com/
Host: login.passport.com
```

随后用户在 login.asp 中输入其 Passport 密码并 POST 数据；注意，凭据是通过 SSL 发送的，但在我们在机器上执行的跟踪中，它们以明文显示。合作伙伴并不要求在客户端和 Passport 服务器之间使用 SSL。

```
POST /post.asp?id=658&ru=http://my.msn.com/etc. HTTP/1.0
Referer: http://login.passport/login.asp?id=658&ru=http://my.msn.com/etc.
Host: login.passport.com
```

```
login=johnndoe&domain=msn.com&passwd=shared=
```

在步骤 4 中，登录成功后，Passport 登录服务器在客户端上设置了一系列 Cookie。重要的 Cookie 是 MSPAuth，它是身份验证票。

```
HTTP/1.1 200 OK
Set-Cookie: MSPAuth=Thu, 01 Jan 1970 00:00:00 GMT;domain=.passport.com;path=/
Set-Cookie: MSPProf=Thu, 01 Jan 1970 00:00:00 GMT;domain=.passport.com;path=/
```

最后，在步骤 5 中，客户端返回合作伙伴站点上的原始资源（Passport 登录服务器从原始查询字符串中记录了它）：

```
GET /my.aspx HTTP/1.0
Host: my.msn.com
Cookie: MSPAuth
```

尽管这看起来是几次往返，但根据互联网连接的速度，它对用户来说非常快速且透明。

要退出登录，用户点击 Passport 的“退出”（Sign Out），再次重定向到 login.passport.com，然后它删除 Cookie（将其设置为 NULL）并将客户端返回合作伙伴站点：

```
HTTP/1.1 200 OK
Host: login.passport.com
Authentication-Info: Passport1.4 da-status=logout
Set-Cookie: MSPAuth=Thu, 01 Jan 1970 00:00:00 GMT;domain=.passport.com;path=/
Set-Cookie: MSPProf=Thu, 01 Jan 1970 00:00:00 GMT;domain=.passport.com;path=/
```

等等。

## 针对 Passport 的攻击

自 1999 年引入以来，Passport 经历过几次攻击。2000 年，David P. Kuhn 和 Ariel D. Rubin 发表了一篇名为《*Risks of the Passport Single Sign-On Protocol*》的论文，描述了一系列针对 SSL、Netscape 浏览器 Cookie、Javascript 和 DNS 嗅探等基础功能的通用攻击。他们还指出，任何人都可以伪造 Passport 页面并收集成员凭据（“伪造”攻击），并推测合作伙伴站点的密钥以脆弱的方式在互联网上传输。整篇论文探讨了互联网身份认证服务的已知问题，并展示了对 Passport 信息问题的实际研究。

2001 年 8 月，Chris Mitchell 发表了一篇关于 5.5 版本之前的互联网浏览器漏洞的论文，该漏洞允许恶意网站或电子邮件读取客户端机器上的 Cookie。他还指出，如果 Passport 成员选择在本地保存 Passport Cookie，攻击者可以利用该漏洞窃取 Passport Cookie 并冒充受害者。IE 的漏洞随后得到了修复，Chris 正确地评论说，用户在使用 Passport 时并不会选择“自动登录”选项（这会在用户的机器上设置一个持久性 Cookie）。

2001 年晚些时候，安全研究人员 Marc Spectre 发布了一份名为“Microsoft Passport Trouble”的分析报告，在其中描述了一种允许其通过在使用 Passport 认证的页面进行脚本注入来窃取身份验证 Cookie 的利用。微软随后修复了这个问题，但这种攻击是窃取身份验证 Cookie 的绝佳示例。

所有这些攻击的共同主题表明，使用认证最大的危险之一是使用来自不知用户计算机的身份验证 Cookie 进行重放攻击。当然，假设攻击者能够窃取身份验证票，可能从一开始就击败了大多数认证系统。

与任何其他认证系统一样，Passport 也可能受到密码破解攻击的威胁（最小密码长度为六个字符，对大小写、数字或特殊字符没有要求）。虽然没有永久的账户锁定功能，但在尝试登录失败若干次后，账户将被临时阻止登录（根据错误信息，这会持续“几刻”）。这种设计是为了给密码破解攻击增加大量时间。攻击者可能会在锁定期间尝试重置密码，但必须回答 Passport 账户所有人在注册期间设置的“秘密问题”。

尽管存在这些问题，对于不在乎谁拥有客户身份验证凭据的网站来说，Passport 仍然是一个强大的选择。

## 攻击 Web 认证

到目前为止，我们描述了互联网上主要的认证机制。这些机制是如何被攻击的？在本节中，我们将讨论用于利用 Web 认证中常见漏洞的技术，并以如何避免这些陷阱的建议结束。

在开始之前简单说明一下——身份认证的存在意味着应用程序开发者创建了一些安全基础设施，以防止普通黑客轻松访问其他用户的数据。因此，攻击 Web 认证并非易事。然而，正如我们接下来看到的，实现方式始终是导致溃败的关键。

## 密码破解

虽然不是最酷的攻击，但密码破解是破解 Web 认证最有效的技术。假设认证协议的选择或其实现没有某些缺陷，大多数认证系统最脆弱的环节是用户密码的选择。

密码破解可以通过手动或自动方式进行。手动密码破解很枯燥，但当人类直觉经常胜过自动化工具时（特别是在响应失败的表单登录尝试使用自定义错误页面时），手动方法是有效的。在进行密码破解时，我们的首选方案如表 5-3 所示。

| 攻击类型 |  |
| :--- | :--- |
| 字典攻击 | 使用预定义的常用密码或单词列表。 |
| 暴力破解 | 尝试所有可能的字符组合。 |
| 凭据填充 | 使用其他网站泄露的用户名和密码。 |
| 社会工程 | 欺骗用户交出密码。 |

密码破解可以针对本章涵盖的几乎所有类型的 Web 认证进行。我们将讨论两种针对 Basic 和表单认证的攻击，但攻击 Digest 和 NTLM 的工具也是可行的。

