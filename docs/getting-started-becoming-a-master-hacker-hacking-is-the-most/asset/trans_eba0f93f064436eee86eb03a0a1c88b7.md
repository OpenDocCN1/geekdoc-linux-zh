

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_147_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_148_0.png)

如上方截图所示，Netcraft 列出了 Facebook 的多个站点和服务器。多年来，Facebook 在全球范围内扩张，在多个国家部署了服务器。让我们来看一下 Facebook 的原始站点 www.facebook.com。列表信息显示，该站点首次发现于 1997 年 5 月，网段由 Facebook 持有，且该站点运行的操作系统为 Linux。如果我们点击中间的“站点报告”，就可以看到关于 Facebook 的更多信息。

站点报告包括：
- 站点标题
- 该网站在 internet 数百万个网站中的排名
- 首次发现日期
- 主要语言
- 描述

托管历史部分包含更多有趣的信息，例如：
- IP 地址
- 操作系统
- Web 服务器
- 最后发现时间

如果我们向下滚动一点，可以看到关于该站点使用的技术的更多信息。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_149_0.png)

## 1 安全

Netcraft 风险评级 (FRA) 0/5 [进度条指示低风险]

- 在激进位列表中：否
- 在 Defensio 阻止列表中：否
- 在昂贵阻止列表中：否
- 在过度阻止列表中：否

## 发件人策略框架

主机的发件人策略框架（SPF）描述了谁可以代表其发送邮件。这是通过发布包含一系列规则的 SPF 记录来实现的。每条规则由一个限定符后跟指定应用该限定符的域组成。欲了解更多信息，请在此阅读。

警告：似乎此主机没有 SPF 记录。设置 SPF 记录有助于防止来自您域的伪造邮件被投递。

## 2 DMARC

DMARC（基于域的邮件身份验证、报告和一致性）是一种机制，用于让域发件人指示声称源自其域的邮件应经过身份验证。它基于 SPF 和 DKIM 构建，提供了一种告知策略并获取失败报告的方法。欲了解更多信息，请在此阅读。

DMARC 记录 (txt) 的值为：p=none; percent= 100;ru=5m; o=none; ruf=https://dmarc@agoric.com; r=24;adkim=r; aspfm=r

| 标签 | 角色 | 值 |
| --- | --- | --- |
| spf=1 | 必需 | 意味着在 DMARC 验证期间，DMARC 机制应坚持标记为：必需 SHOULD |
| pct=100 | 发送速率 | 域所有者邮件流中 100% 的消息应应用 DMARC。 |
| ru=5m; ruf=reports@dmarc@agoric.com | 报告速率 | 报告：汇总报告 rUF=5m，取证报告 rUF=3d，或任其一为默认值 |
| aspf=r; adkim=r; p=none | 失败率的报告策略 | pfail@apex.com |

## 3 Web 跟踪器

Web 跟踪器是加载到网页中的第三方资源。跟踪器衡量网站访问者的使用情况，包括页面浏览量、点击率和参与度。这些跟踪器可用于在网络上监控单个用户在此前和之后的活动。从这些跟踪器中提取的数据可能用于广告或分析目的。

未识别出已知跟踪器。

## 4 站点技术

存档于：2015 年 2 月 18 日

### 服务端

Netcraft 检测到的在服务器上运行的主要技术（如 PHP）的详细信息。

| 技术 | 描述 | 使用此技术的流行站点 |
| --- | --- | --- |
| PHP 7 | PHP 是一种服务器端脚本语言 | www.smile.com, www.dallas.com, www.explosive.com |
| Perl 4 | Perl 是一种高级、通用、解释型、动态编程语言 | www.fox.com, Amazon.com, Text.com |
| RHEL 7 | 一种轻量级、强大且高性能的 Linux 发行版 | www.google.com, www.pipetree.org, www.youtube.com |

### 客户端

在浏览器上运行的主要技术（如 JavaScript 和 Adobe Flash）的详细信息

| 技术 | 描述 | 使用此技术的流行站点 |
| --- | --- | --- |
| Bootstrap 3 | 一种开源编程语言，通常作为 Web 浏览器的一部分实现 | www.google.com, apple.com, twitter.com |
| Clear-Pdf | 无描述 | www.fool.com, www.fortune.com, www.myspace.com |
| - | 无描述 | www.myspace.com, www.google.com |

### 混淆编码

字符编码系统由将给定字库中每个字符与比特模式、自然数序列或字母等配对起来的代码组成。字符编码系统可以表示计算机屏幕上可显示的所有可能字符。

| 技术 | 描述 | 使用此技术的流行站点 |
| --- | --- | --- |
| UTF-8 | UCS 转换格式 8 位 | progressb.com, phuck.com, gmail.com |

### HTTP 压缩

HTTP 压缩是一种可用于减少网络延迟和带宽消耗的技术。它通过压缩数据进行发送并在接收端解压来工作。Gzip、Deflate 和 Brotli 是常见的 HTTP 压缩算法。

| 技术 | 描述 | 使用此技术的流行站点 |
| --- | --- | --- |
| Gzip | Gzip HTTP 压缩协议 | www.google.com, amazon.com, netflix.com |

### 站点浏览器使用目标

Web 浏览器目标设置使软件应用程序能够利用浏览器的特定功能，并为特定浏览器版本优化应用程序。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_151_0.png)

通常情况下，我们可以从 Netcraft 收集到关于较小网站和 Web 服务器的更多信息（尽管有些网站太小，Netcraft 无法跟踪）。让我们看看他们关于 www.skullsecurity.com 的信息，这是一个专门从事 IT 安全的网站，常被用作密码列表的来源。

有趣的是，skullsecurity.com 的“站点标题”下，Netcraft 列出了“404 未找到”。网站所有者可以随意输入任何标题。这个网站的所有者显然很有幽默感。在托管历史部分，Netcraft 列出了 IP 地址、操作系统（Linux）和 Web 服务器（nginx）。所有这些信息在制定利用策略时都可能是有益的信息！

```
Domain Status: clientDeleteProhibited (https://www.icann.org/epp#clientDeleteProhibited)
Registry Registrant ID:
Registrant Name: Domain Administrator
Registrant Organization: Facebook, Inc.
Registrant Street: 1601 Willow Road,
Registrant City: Menlo Park
Registrant State/Province: CA
Registrant Postal Code: 94025
Registrant Country: US
Registrant Phone: +1.6505434800
Registrant Phone Ext:
Registrant Fax: +1.6505434800
Registrant Fax Ext:
Registrant Email: domain@fb.com
Registry Admin ID:
Admin Name: Domain Administrator
Admin Organization: Facebook, Inc.
Admin Street: 1601 Willow Road,
Admin City: Menlo Park
Admin State/Province: CA
Admin Postal Code: 94025
Admin Country: US
Admin Phone: +1.6505434800
Admin Phone Ext:
Admin Fax: +1.6505434800
Admin Fax Ext:
Admin Email: domain@fb.com
Registry Tech ID:
Tech Name: Domain Administrator
Tech Organization: Facebook, Inc.
Tech Street: 1601 Willow Road,
Tech City: Menlo Park
Tech State/Province: CA
Tech Postal Code: 94025
Tech Country: US
```

## Whois

每当任何人注册一个域名时，他们都必须提供一些关于他们自己及其公司的必要信息。这些信息可以包括名称服务器、注册商、联系人姓名、地址、电话号码和电子邮件地址。所有这些可能对攻击者都很有用。

这些信息由注册商维护，并由 InterNIC 维护一个中央注册机构。我们可以使用几乎每个 Linux/UNIX 系统都内置的 whois 命令查询（端口 43）这些数据库以获取这些基本信息。让我们从我们的 Kali 系统查询 facebook.com。

kali> whois facebook.com

如上方截图所示，我们的 Kali Linux 自动查询 whois 条目并返回有关域名的信息，例如名称、地址、城市、州、邮政编码和电话号码。

域名所有者还必须向注册商提供技术联系人和管理联系人的信息，但现在大多数大公司都像 Facebook 在此处提供的那样提供通用名称。较小公司的情况并非总是如此。

当我们对 skullsecurity.com 运行类似的 whois 查询时，我们获得了所有者的姓名、地址、电话和电子邮件地址。

