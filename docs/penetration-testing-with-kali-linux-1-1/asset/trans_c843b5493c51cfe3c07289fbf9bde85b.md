

通过一项专注的被动信息收集行动，利用各种谷歌搜索操作符，将零散的信息“连接”并“导入”到其他在线工具中，再加上一点创造力和逻辑思维，我们找到了目标公司的一名员工在一个集邮论坛上发表的一个帖子：

```
你好！
我在寻找1950年代的稀有邮票——出售或交换。
请通过 david@company-address.com 联系我
手机：999-999-9999
```

列表 193 - 一个论坛帖子

我们利用这些信息发起了一次半复杂的客户端攻击。我们迅速注册了一个与邮票相关的域名，并设计了一个显示各种1950年代稀有邮票的落地页面（这些图片是我们使用谷歌图片搜索找到的）。该域名和网站的设计无疑提高了我们邮票交易网站的可信度。

接下来，我们在该网站的网页中嵌入了一些恶意的客户端攻击利用代码，并在工作时间给“David”打了电话。在通话中，我们伪装成一位继承了他祖父庞大邮票收藏的邮票收藏家。

David 收到我们的电话时欣喜若狂，毫不犹豫地去访问了那个恶意网站，以查看“邮票收藏”。在浏览该网站时，利用代码在他的本地机器上执行，并向我们发送了一个反向 shell。

这是一个很好的例子，说明一些看似无害的被动收集信息（例如员工使用公司电子邮件处理个人事务）在渗透测试中如何成为突破口。有时候，最细微的细节可能最为关键。

> 虽然“David”没有遵循最佳实践，但公司的政策和安全意识计划的缺失为这次数据泄露埋下了伏笔。因此，我们在书面报告中避免指责个人。作为渗透测试人员，我们的目标是提高客户资源的安全性，而不是针对单个员工。仅仅移除“David”并不能解决问题。

让我们来看看一些最流行的工具和技术，它们可以帮助我们要成功实施信息收集行动。我们将以 MegaCorp One¹³⁸ 作为行动对象，这是一家由 Offensive Security 创建的虚构公司。

## 6.1 做笔记

信息收集行动可能会产生大量数据，因此妥善管理这些数据至关重要，以便我们能在后续搜索中利用它们，或在后续阶段中使用。记笔记没有绝对的对错之分。不过，如果我们保持详细且格式良好的笔记，可能更容易在日后检索信息。

¹³⁸ (Offensive Security, 2019). https://www.megacorpone.com/

## 6.2 网站侦察

如果客户拥有网站，我们只需浏览该网站即可收集基本信息。小型组织可能只有一个网站，而大型组织可能拥有许多网站，包括一些未维护的网站。让我们查看 MegaCorp One 的网站 ([https://www.megacorpone.com/](https://www.megacorpone.com/)) 以了解有关目标的更多信息。

![MegaCorp One](img/ec25e59d75726b7041242a56d3376832_136_0.png)

图 19: MegaCorp One

快速浏览他们的网站可以发现，这是一家纳米科技公司。

位于 [https://www.megacorpone.com/about.html](https://www.megacorpone.com/about.html) 的“关于”页面揭示了部分员工的电子邮件地址和 Twitter 账户：

![About Us - MegaCorp One](img/ec25e59d75726b7041242a56d3376832_137_0.png)

图 20: About Us - MegaCorp One

我们可以在社交媒体信息收集行动中使用这些地址。我们将在后面的章节中更详细地讨论这一点。

值得一提的是，该公司的电子邮件地址格式遵循“名字首字母 + 姓氏”的模式。然而，他们的 CEO 的电子邮件地址仅使用他的名字。这表明创始人或资深员工与新雇员的电子邮件格式不同。这些信息在评估的后期阶段可能很有用。

在同一页面上找到的公司社交媒体账号也值得记录，以便进一步研究：

![Social Media - MegaCorp One](img/ec25e59d75726b7041242a56d3376832_138_0.png)

图 21: Social Media - MegaCorp One

让我们更新笔记，以跟踪每条信息，包括电子邮件地址格式和社交媒体网站参考。

## 6.3 Whois 枚举

Whois¹³⁹ 是一种 TCP 服务、工具和一种数据库，可以提供关于域名的信息，例如*名称服务器*¹⁴⁰和*注册商*¹⁴¹。由于注册商对隐私注册收取费用，这些信息通常是公开的。

我们可以通过执行标准的正向搜索来收集关于域名基本信息，将域名 *megacorpone.com* 传递给 **whois** 客户端：

```bash
kali@kali:~$ whois megacorpone.com
Domain Name: MEGACORPONE.COM
Registry Domain ID: 1775445745_DOMAIN.COM-VRSN
Registrar WHOIS Server: whois.gandi.net
Registrar URL: http://www.gandi.net
Updated Date: 2019-01-01T09:45:03Z
Creation Date: 2013-01-22T23:01:00Z
Registry Expiry Date: 2023-01-22T23:01:00Z

Registry Registrant ID:
Registrant Name: Alan Grofield
Registrant Organization: MegaCorpOne
Registrant Street: 2 Old Mill St
Registrant City: Rachel
Registrant State/Province: Nevada
Registrant Postal Code: 89001
Registrant Country: US
Registrant Phone: +1.9038836342

Registry Admin ID:
Admin Name: Alan Grofield
Admin Organization: MegaCorpOne
Admin Street: 2 Old Mill St
Admin City: Rachel
Admin State/Province: Nevada
Admin Postal Code: 89001
Admin Country: US
Admin Phone: +1.9038836342

Registry Tech ID:
Tech Name: Alan Grofield
Tech Organization: MegaCorpOne
Tech Street: 2 Old Mill St
Tech City: Rachel
Tech State/Province: Nevada
Tech Postal Code: 89001
Tech Country: US
Tech Phone: +1.9038836342

Name Server: NS1.MEGACORPONE.COM
Name Server: NS2.MEGACORPONE.COM
Name Server: NS3.MEGACORPONE.COM
```

列表 194 - 对 megacorpone.com 使用 whois

并非所有这些都有用，但我们确实发现了一些有价值的信息。首先，输出结果显示 Alan Grofield 注册了该域名。根据 MegaCorp One 的联系页面，Alan 是“IT 和安全总监”。

我们还找到了 MegaCorp One 的名称服务器。名称服务器是 DNS 的一个组成部分，这里不做详细探讨，但我们应该将这些服务器添加到我们的笔记中。

除了这种收集 DNS 名称信息的标准正向查找外，whois 客户端还可以执行反向查找。假设我们有一个 IP 地址，我们可以执行反向查找以获取更多关于它的信息：

```bash
kali@kali:~$ whois 38.100.193.70
NetRange:   38.0.0.0 - 38.255.255.255
CIDR:       38.0.0.0/8
NetName:    COGENT-A

OrgName: PSINet, Inc.
OrgID: PST
Address: 2450 N Street NW
City: Washington
StateProv: DC
PostalCode: 20037
Country: US
RegDate:
Updated: 2015-06-04
```

列表 195 - Whois 反向查找

反向查找的结果提供了关于谁托管该 IP 地址的信息。这些信息稍后可能有用，与收集到的所有信息一样，我们将把它添加到笔记中。

### 6.3.1.1 练习

- 使用 Kali 中的 whois 工具确定 MegaCorp One 的名称服务器。

## 6.4 谷歌黑客技术

“谷歌黑客技术”（Google Hacking）一词由 Johnny Long 在 2001 年普及。通过几次演讲¹⁴²和一本非常流行的书（*《谷歌黑客技术用于渗透测试者》*¹⁴³），他概述了如何利用谷歌等搜索引擎来发现关键信息、漏洞和配置不当的网站。

这项技术的核心是巧妙的搜索字符串和*操作符*¹⁴⁴，它们允许对搜索查询进行创造性细化，其中大部分适用于各种搜索引擎。这个过程是迭代的，从宽泛的搜索开始，通过操作符缩小范围，以筛选出不相关或不感兴趣的结果。

让我们尝试其中一些操作符，感受一下它们是如何工作的。

*site* 操作符将搜索限制在单个域名。我们可以使用此操作符来获得组织网络存在的粗略概念：

¹³⁹ (Wikipedia, 2019) https://en.wikipedia.org/wiki/WHOIS
¹⁴⁰ (Wikipedia, 2019) https://en.wikipedia.org/wiki/Name_server
¹⁴¹ (Wikipedia, 2019) https://en.wikipedia.org/wiki/Domain_name_registrar
¹⁴² 对 Johnny Long 演讲的引用。
¹⁴³ 对《谷歌黑客技术用于渗透测试者》的引用。
¹⁴⁴ 对搜索操作符的引用。

