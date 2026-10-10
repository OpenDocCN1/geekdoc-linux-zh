
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

这些信息由注册商维护，并由 InterNIC 维护一个中央注册机构。我们可以使用几乎每个 Linux/UNIX 系统都内置的 `whois` 命令查询（端口 `43`）这些数据库以获取这些基本信息。让我们从我们的 Kali 系统查询 `facebook.com`。

`kali> whois facebook.com`

如上方截图所示，我们的 Kali Linux 自动查询 `whois` 条目并返回有关域名的信息，例如名称、地址、城市、州、邮政编码和电话号码。

域名所有者还必须向注册商提供技术联系人和管理联系人的信息，但现在大多数大公司都像 Facebook 在此处提供的那样提供通用名称。较小公司的情况并非总是如此。

当我们对 `skullsecurity.com` 运行类似的 `whois` 查询时，我们获得了所有者的姓名、地址、电话和电子邮件地址。

## Whois 信息

注册人 ID：CR32628813

注册人姓名：Ron Bowes

注册人组织：

注册人街道：604-870 Cambridge St

注册人城市：Winnipeg

注册人州/省：Manitoba

注册人邮政编码：R3M3H5

注册人国家：CA

注册人电话：+1.20496604345

注册人电话分机：

注册人传真：

注册人传真分机：

注册人电子邮件：rondomain@javaop.com

管理员 ID：CR32628815

管理员姓名：Ron Bowes

管理员组织：

管理员街道：604-870 Cambridge St

管理员城市：Winnipeg

管理员州/省：Manitoba

管理员邮政编码：R3M3H5

管理员国家：CA

管理员电话：+1.20496604345

管理员电话分机：

管理员传真：

管理员传真分机：

管理员电子邮件：rondomain@javaop.com

技术联系人 ID：CR32628814

技术联系人姓名：Ron Bowes

技术联系人组织：

技术联系人街道：604-870 Cambridge St

技术联系人城市：Winnipeg

技术联系人州/省：Manitoba

技术联系人邮政编码：R3M3H5

技术联系人国家：CA

技术联系人电话：+1.20496604345

技术联系人电话分机：

技术联系人传真：

技术联系人传真分机：

技术联系人电子邮件：rondomain@javaop.com

如果我们使用的是 Windows 系统，可以使用几种在线 `whois` 查询工具之一。我们可以在 `www.networksolutions.com` 找到这样一类工具，但还有其他可用的工具，例如：

- `http://whois.domaintools.com`

- `http://ripe.net`

- `http://whois.sc`

当我们使用 Windows 上的浏览器在 `www.networksolutions.com` 上对 `skullsecurity.com` 运行 `whois` 查询时，我们会得到以下信息。

## skullsecurity.com

这是你的域名吗？立即续订。

域名：SKULLSECURITY.COM

注册局域名 ID：695833122_DOMAIN_COM-VRSN

注册商 WHOIS 服务器：whois.godaddy.com

注册商 URL：http://www.godaddy.com

更新日期：2013-10-16T20:32:23Z

创建日期：2006-12-04T14:42:27Z

注册商注册到期日期：2015-11-27T11:59:59Z

注册商：GoDaddy.com, LLC

注册商 IANA ID：146

注册商滥用联系电子邮件：abuse@godaddy.com

注册商滥用联系电话：+1.480-624-2505

域名状态：clientTransferProhibited http://www.icann.org/epp#clientTransferProhibited

域名状态：clientUpdateProhibited http://www.icann.org/epp#clientUpdateProhibited

域名状态：clientRenewProhibited http://www.icann.org/epp#clientRenewProhibited

域名状态：clientDeleteProhibited http://www.icann.org/epp#clientDeleteProhibited

注册局注册人 ID：

注册人姓名：Ron Bowes

注册人组织：

注册人街道：604-870 Cambridge St

注册人城市：Winnipeg

注册人州/省：Manitoba

注册人邮政编码：R3M3H5

注册人国家：Canada

注册人电话：+1.20496604345

注册人电话分机：

注册人传真：

注册人传真分机：

注册人电子邮件：rondomain@javaop.com

注册局管理员 ID：

管理员姓名：Ron Bowes

管理员组织：

管理员街道：604-870 Cambridge St

管理员城市：Winnipeg

管理员州/省：Manitoba

管理员邮政编码：R3M3H5

管理员国家：Canada

管理员电话：+1.20496604345

管理员电话分机：

管理员传真：

管理员传真分机：

管理员电子邮件：rondomain@javaop.com

注册局技术联系人 ID：

技术联系人姓名：Ron Bowes

技术联系人组织：

技术联系人街道：604-870 Cambridge St

技术联系人城市：Winnipeg

技术联系人州/省：Manitoba

技术联系人邮政编码：R3M3H5

技术联系人国家：Canada

技术联系人电话：+1.20496604345

技术联系人电话分机：

技术联系人传真：

技术联系人传真分机：

技术联系人电子邮件：rondomain@javaop.com

请注意，这些信息与我们从 Linux `whois` 查询获得的信息几乎相同，但格式略有不同。

### Shodan

我们所有人都在使用（在大多数情况下，每天数次）Google、Bing 或 Yahoo 来搜索互联网上的相关资料。在本章早些时候，我们学习了一些使用 Google 黑客攻击来查找 Google 庞大的网络材料数据库中可能不易直接看到的信息的基础知识。在本节中，我将向你介绍另一个网络搜索引擎，Shodan。Shodan 常被称为“世界上最危险的搜索引擎”，因为它索引和揭示的数据。
