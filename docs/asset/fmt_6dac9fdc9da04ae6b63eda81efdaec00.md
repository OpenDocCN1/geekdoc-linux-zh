
在宽松的解释中，我们可能会与目标交互，但仅作为普通的互联网用户。例如，如果目标网站允许我们注册账户，我们可以这样做。但是，我们不会在此阶段对网站进行漏洞测试。

这两种方法都可以有用，取决于我们正在进行的的测试目标。因此，在决定使用哪种方法之前，我们需要考虑渗透测试的范围和参与规则。

在本模块中，我们将采用这种不那么严格的解释。

我们可以使用多种资源和工具来收集信息，而且这个过程是循环而非线性的。换句话说，过程中每个阶段的“下一步”取决于我们在上一步中发现了什么，从而创建了流程的“循环”。每个工具或资源都可以产生任意数量的各种结果，很难定义一个标准的结果。被动信息收集的最终目标是获取扩展攻击面的信息、帮助开展成功的钓鱼攻击，或补充渗透测试步骤（如密码猜测），这些最终可能导致账户被破解。

我们将不会演示关联场景，而是简单地涵盖各种资源和工具，解释它们的工作原理，并让你掌握构建被动信息收集活动所需的基础技术。

在开始讨论资源和工具之前，让我们分享一个涉及被动信息收集活动成功元素的渗透测试个人案例。

## 作者说明

几年前，OffSec 团队被委托为一家小公司进行渗透测试，该公司几乎没有互联网存在感，暴露的服务极少，且所有服务都被证明是安全的。实际上没有攻击面。在进行一次针对性的被动收集活动后（利用了各种 Google 搜索运算符，将碎片信息“传输”到其他在线工具中，并结合了一些创意和逻辑思维），我们在目标员工之一在一个集邮论坛上发布的帖子中发现了：

> 你好！
>
> 我正在寻找 1909 年的稀有邮票
>
> 请通过 `david@company.com` 与我联系。

# 使用 Kali Linux 进行渗透测试

### 6.2.1 枚举

我们可以通过执行标准查询并将域名传递给 `whois` 来获取基础信息。

```
whois megacorp.com -h 192.168.50.251
Domain Name: MEGACORP_COM
Registrar ID: 177545745_DOMAIN_COM-VR5N
Registrar WHOIS Server: whois.gandi.net
Registrar URL: http://www.gandi.net
Updated: 2019-01-17T09:45:03
Creation Date: 2013-01-22T23:01:00Z
Registry Date: 2023-01-22T23:01:00Z
...
Registrant Registrant Name: Alan Grofield
Registrant Organization: MegaCorpOne
Registrant Street: 2 Old Mill St
Registrant City: Rachel
Registrant State/Province: Nevada
Registrant Postal Code: 89001
Registrant Country: US
Registrant Phone: +1.9038836342
...
Registrar Admin ID:
Admin Name: Alan Grofield
Admin Organization: MegaCorpOne
Admin Street: 2 Old Mill St
Admin City: Rachel
Admin State/Province: Nevada
Admin Postal Code: 89001
Admin Country: US
Admin Phone: +1.9038836342
...
Registry Tech ID:
```

`Whois` 是一个 TCP 服务和数据库，可以提供有关域名以及注册商的信息。这些信息通常是公开的，因为注册商会收取隐私注册费用。

# OffSec Grofield

技术人员：Alan Grofield

技术组织：MegaCorpOne

技术街道：2 Old Mill St

技术城市：Rachel

技术州/省：内华达州

技术邮政编码：89001

技术国家：美国

技术电话：+1.9038836342

名称服务器：`NS51.MEGACORPONE.COM`

名称服务器：`NS52.MEGACORPONE.COM`

名称服务器：`NS53.MEGACORPONE.COM`

列表 35 - 使用 `whos` 查询 `megacorp.com`

这些并非所有内容都有用处，但我们发现了一些有价值的信息。首先，输出显示由 Alan Grofield 注册了该域名。根据 Megacorp One 的联系页面，Alan 是“IT 与安全总监”。

我们还找到了 MegaCorp One 的名称服务器。名称服务器是 DNS 的组成部分，我们现在不会对其进行检查，但我们仍会将这些节点添加到我们的节点中。

假设我们有一个地址，可以使用 `whos` 客户端进行反向查询并获取更多信息。

```
kalis@kali:$ whos 38.100.193.70 -h 192.168.50.251

NetRange:       38.0.0.0 - 38.255.255.255
CIDR:           38.0.0.0/8
NetName:        COGENT-A
...
OrgName:        PSINET, Inc.
OrgId:          PSI
Address:        2450 N Street NW
City:           Washington
StateProv:      DC
PostalCode:     20037
Country:        US
RegDate:        2015-06-04
...
```

列表 36 - `Whos` 反向查询

反向查询的结果为我们提供了关于该 IP 地址的信息。这在以后可能有用，结合我们收集的所有信息，我们将其加入笔记中。

### 6.2.2 Google Hacking

“Google Hacking”（Google 黑客攻击）一词由 Johnny Long 在 2001 年普及。通过几次演讲²215 和一本非常受欢迎的书（《渗透测试员的 Google Hacking》²216），他概述了如何

> 215 (Wikipedia, 2022). https://en.wikipedia.org/wiki/Google_Hacking
>
> 216 (Johnny Long, Bill Gardner, Justin Brown, 2015). https://www.amazon.com/Google-Hacking-Penetration-Testers-Johnny/dp/0128029641/ref=dp_0_image_b

PWK - 2023 OffSec Services Limited. 保留所有权利。

# OffSec

使用 Kali Linux 进行渗透测试

像 Google 这样的搜索引擎可以用来发现关键信息、漏洞和配置不当的网站。

技术的核心是巧妙的搜索字符串和运算符²217，用于对搜索查询进行创造性的精炼，这些操作适用于多种搜索引擎。该过程是迭代的，从广泛的搜索开始，然后使用运算符缩小范围，以过滤掉无关或无趣的结果。

我们将首先介绍这些运算符，以学习它们如何被使用。

`site` 运算符将搜索限制在单个域名。我们可以使用此运算符来大致了解一个组织的 Web 呈现情况。

![](img/987dc9f6ebd8893c565a1d124d7724e6_115_0.png)

上面的图片显示了 `site` 运算符如何将搜索限制在我们所指定的 **megacorpone** 域名。

然后我们可以使用更多运算符来缩小这些结果。例如，`filetype`（或 `ext`）运算符将搜索结果限制为指定的文件类型。

在示例中，我们组合运算符来定位 **www.megacorpone.com** (`site:megacorpone.com`) 上的 TXT 文件 (`filetype:txt`)。

> PWK - 版权 © 2023 OffSec Services Limited. 保留所有权利。

# OffSec

使用 Kali Linux 进行渗透测试

![](img/987dc9f6ebd8893c565a1d124d7724e6_116_0.png)

图 15：使用文件类型运算符进行搜索

我们得到了一个有趣的结果。我们的查询发现了 `robots.txt` 文件，包含以下内容。

```
User-agent: *
Allow: /
Allow: /nanites.php
```

列表 37 - `robots.txt` 文件
