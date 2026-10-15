
¹³⁹ (Wikipedia, 2019) https://en.wikipedia.org/wiki/Whois
¹⁴⁰ (Wikipedia, 2019) https://en.wikipedia.org/wiki/Name_server
¹⁴¹ (Wikipedia, 2019) https://en.wikipedia.org/wiki/Registrar
¹³⁸ (Offensive Security, 2019), https://www.megacorp.one/

# 使用 Kali Linux 2.0 进行渗透测试

我们随后可以使用进一步的运算符来缩小这些结果。例如，`filetype`（或 `ext`）运算符可以将搜索结果限制为指定的文件类型。

在示例中，我们结合多个运算符在 `www.megacorpone.com` (`site:megacorpone.com`) 上定位 PHP 文件 (`filetype:php`)：

图 23：使用文件类型运算符搜索

我们只得到了一个结果，但这是一个有趣的发现。我们的查询找到了 AlienVault OSSIM¹⁴⁵ 的安全信息和事件管理（SIEM）平台的实例登录页面。安全团队使用 SIEM 工具监控应用程序和网络流量以发现恶意活动。通常，这些工具仅在内部网络可用。我们应该记录此 URL，因为如果我们能找到登录凭据以进入活跃利用阶段，它可能会非常之用。

`ext` 运算符也可以帮助识别网站可能使用了哪些编程语言。搜索 `ext:jsp`、`ext:cfm`、`ext:pl` 将分别找到索引的 Java Server Pages、Coldfusion 和 Perl 页面。

我们还可以使用 `-` 修改运算符，以从搜索中排除特定项目，从而缩小搜索范围。

例如，为了寻找非 HTML 页面，我们可以使用 `site:megacorpone.com` 将搜索限制到 megacorpone.com 及其子域名，随后使用 `-filetype:html` 从结果中排除 HTML 页面：

¹⁴⁵ (AT&T, 2019), https://cybersecurity.att.com/products/ossim

图 24：使用排除运算符搜索

在这种情况下，我们发现了几个有趣的页面，包括一个管理控制台。

在另一个示例中，我们可以使用搜索 `intitle:index of` `parent directory` 来找到标题中包含“index of”且页面上包含“parent directory”单词的页面。

`intitle="index" of "parent directory" - Google - Mozilla Firefox`

# Index of /dist/directory

Parent Directory | [DIR] archived/2018-11-06 14:26 - [DIR] api/2018-11-06 14:28 - [DIR] fortress/2018-11-06 14:28 - [DIR] jdbm/2018-11-06 14:28 - ...

# Index of /Documents/Videos/Videos-Movies - Parent Directory

Parent Directory | [DIR] 1- Series & 8Sags/2019-11-10 16:01, [DIR], 2- New Movies/2019-11-00 08:58, [DIR], 3- Documentaries/2019-09-10 01:51, ...

# Index of /download

Parent Directory | [DIR] current/2019-09-26 10:00 - [DIR] development/2019-04-29 12:43 - [DIR] documents/2019-04-18 15:45 - [DIR] more/2019-04-29 12:56, ...

输出指的是目录列表¹⁴⁶ 页面，这些页面列出了目录索引页的内容。配置错误可能会泄露有趣的文件和敏感信息。

这些基础示例仅显示了我们使用搜索运算符所能做的一小部分。Google 黑客数据库 (`GHDB`)¹⁴⁷ 包含了大量的创意搜索，展示了结合运算符进行创造性搜索的力量：

¹⁴⁶ (MITRE, 2019), https://cwe.mitre.org/data/definitions/548.html
¹⁴⁷ (Offensive Security, 2019), https://www.exploit-db.com/google-hacking-database

## EXPLOIT 数据库

### Google 黑客数据库

| 添加日期 | Dork | 类别 | 作者 |
| :--- | :--- | :--- | :--- |
| 2019-09-18 | site:"/auth/authorize" | 包含登录的页面 | Reza Abasi |
| 2019-09-18 | index of:"admin.db" | 敏感目录 | The Joker |
| 2019-09-18 | index of:"*filetype:log" | 敏感目录 | The Joker |
| 2019-09-17 | index of:"backup/web.php" | 包含登录的页面 | Yivan |
| 2019-09-17 | site:"*reset password" | 包含登录的页面 | Paris Arora |
| 2019-09-17 | site:filetype index:"manual" | 包含敏感信息的文件 | Deepak Kumar |
| 2019-09-17 | index of:"backup/mysql" | 敏感目录 | Sanya Chawla |
| 2019-09-17 | mailto:example.com | 包含登录的页面 | Sravan |
| 2019-09-16 | site:"search/index.php" | 包含敏感信息的文件 | Mayur Pawar |
| 2019-09-16 | title:"login" site:welcome | 包含登录的页面 | Reza Abasi |
| 2019-09-16 | site:"shibboleth/saml/POST" | 包含登录的页面 | Reza Abasi |
| 2019-09-16 | site:"auth/login.php" | 包含登录的页面 | Reza Abasi |

图 26：Google 黑客数据库 (GHDB)

精通他人的技巧，结合敏锐的推断能力，是有效进行搜索引擎“黑客”的关键技能。

## 6.4 练习

- MegaCorp One 的法务副总裁是谁？他们的电子邮件地址是什么？
- 使用 Google dorks（GHDB 中的任意一个或多个）在 `www.megacorpone.com` 上搜索有趣的文档。
- 除了 `www.megacorpone.com` 上列出的，你还能识别出哪些 MegaCorp 员工？

## 6.5 Netcraft

Netcraft 是一家位于英国的互联网服务公司，提供一个免费的网络门户来执行各种信息收集。使用像 Netcraft 这样的服务被认为是一种被动技术，因为我们从不与目标交互。

让我们回顾如何使用 Netcraft 的 DNS 搜索页面 (`https://searchdns.netcraft.com`) 来收集关于 `megacorpone.com` 域的信息：

¹⁴⁸ (Netcraft, 2019), https://www.netcraft.com/

### 按域名搜索 Web

Netcraft 访问过的 Web 站点 2019年9月20日

### *.megacorpone.com 的结果

找到 5 个站点

| 站点 | 站点报告 | 首次出现 | 网块 | 操作系统 |
| :--- | :--- | :--- | :--- | :--- |
| 1. www.megacorpone.com | | 2013 | point, inc. | linux |
| 2. intranet.megacorpone.com | | | point, inc. | unknown |
| 3. admin.megacorpone.com | | | point, inc. | unknown |
| 4. support.megacorpone.com | | | volico | unknown |
| 5. vpn.megacorpone.com | | 2016 | point, inc. | linux |

图 27：Netcraft 结果

对于每个服务器，我们可以通过点击 URL 旁的文件图标来查看“站点报告”，以获取有关该服务器的信息。

## www.megacorpone.com 的站点报告

### NetScan 扩展

- 背景
- 立即下载！
- 报告钓鱼
- 站点报告
- 顶级报告者
- 报告者的奖励
- 被钓鱼的 TLD
- 被钓鱼的国家
- 被钓鱼的托管
- 被钓鱼的证书机构
- 钓鱼地图
- 取消地图
- 最热门网站
- 品牌扩展
- 告诉朋友

### 钓鱼与欺诈

- 钓鱼站点推送
- 托管钓鱼警报
- SSL 钓鱼警报
- 针对 TLD 的反钓鱼
- 钓鱼与恶意软件
- 设备声誉
- 银行欺诈检测
- 钓鱼站点应对措施

图 28：Netcraft 站点报告

报告的开头涵盖了注册信息。但是，如果我们向下滚动，就会发现各种“站点技术”条目：

这些技术列表在我们转向主动信息收集和利用时非常有用。现在，我们将其加入笔记。

### 6.5.1.1 练习

- 使用 Netcraft 确定 `www.megacorp.com` 上运行什么应用程序服务器。

## 6.6 Recon-ng

`recon-ng`¹⁴⁹ 是一个基于模块的 Web 信息收集框架。`Recon-ng` 将模块的结果显示在终端中，但也将将其存储在数据库中。`Recon-ng` 的很大力量源于将一个模块的结果输入另一个模块，允许我们快速扩大信息收集的范围。

让我们使用 `recon-ng` 收集 MegaCorp One 的有趣数据。为了开始，我们只需运行 `recon-ng`

# 攻击性安全
www.offensive-decoding.com

基于 Kali Linux 2.0 的渗透测试

```
kali@kali:- recon-ng
```
`+]` 节点检查已禁用。

![](img/f99f528ca9845f4c256ce54e882b1345_148_0.png)

赞助商...

```
[recon-ng v5.0.0, Tim Tomes (@lanmaster53)]
```
`[+]` 无已启用/安装的模块。

```
[recon-ng][default] >
```

列表 196 - 启动各种模块以使用 recon-ng。

根据输出结果，我们需要安装各种模块才能使用 recon-ng。

我们可以从 recon-ng 的“市场”(`Marketplace`)中添加模块。我们将从主提示符通过 `marketplace search` 并提供搜索字符串作为参数来搜索市场。

在这个示例中，我们搜索包含 github 术语的模块。
