

## DNS 查询

这些工具允许你收集有关你网络资源的域名系统（DNS）信息。因此，强烈建议你检查自己的网站，看看其他人对你的网站了解了哪些信息。

一个很好的例子是 https://spyse.com/tools/dns-lookup 网站，它为你提供的不再仅仅是 DNS 信息，还包括：

- DNS 记录（邮件交换记录 (MX)、地址 (A)、名称服务器）
- DNS 历史
- 使用的技术（操作系统 (OS)、互联网信息服务 (IIS)、库、字体、内容管理系统 (CMS) 等）
- 子域名
- 其他数据（超文本传输协议 (HTTP) 标头、层叠样式表 (CSS) 链接、JavaScript (JS)）
- 证书信息（安全套接层，或 SSL）
- 验证过的电子邮件地址

根据你的业务情况，某些信息必须进行混淆处理，因为它们代表了安全或隐私风险。

以下截图所示页面显示了根据常见漏洞与暴露 (CVE) 发现的漏洞的安全评分：

![](img/8c6a223c57e25ea0cc1593903a1b920f_358_0.png)

图 12.1 – 来自 spyse 的漏洞视图

## 获取关于你网站/Web 程序的情报 337

正如你可能已经推出的，这类页面也是评估你的托管提供商安全性良好的信息来源。

## WHOIS 记录

这些记录显示了与给定域名所有者相关的信息。这里的风险在于，将这些记录与单个人关联可能会使其成为网络犯罪分子的大大目标。

例如，如果攻击者可以看到某大公司域名所有者的电子邮件地址，那么攻击者就可以利用该信息对该人员进行多种攻击，如下：

- 社会工程学攻击
- 暴力破解攻击
- 冒充攻击
- 在已知数据泄露中搜索电子邮件以收集凭据

为了防止这些攻击，公司可以向域名注册商支付额外费用以隐藏这些记录作为隐私保护措施，如下截图所示：

| 正常域名 | 私有域名 |
| :--- | :--- |
| 注册商数据 | 注册商数据 |
| 注册商联系信息： | 注册商联系信息： |
| 姓名 Tomi Beta | 姓名 已出于隐私原因隐藏 |
| 组织 Mikela Corp | 组织 已出于隐私原因隐藏 |
| 地址 Desild Road | 地址 已出于隐私原因隐藏 |
| 城市 Toscana | 城市 已出于隐私原因隐藏 |

图 12.2 – 私有域名与正常域名 WHOIS 输出

注意前一个截图，注册商信息已为了安全和隐私而进行了混淆。

## 托管信息

另一个你可能想要检查的信息是关于共享托管环境的。例如，像 https://www.domainiq.com 这样的页面会提供托管在特定服务器或子网上的所有域名列表。

这些信息可以以两种方式使用，如接文所述：

- 首先，如果你使用共享托管环境，你可以用它来确定服务器信誉。
- 其次，这也代表了关于公司所有权的隐私问题。例如，你可能在不同的公司下注册了两个公司，因为你不希望公众将它们联系在一起，但将两个域名都托管在同一台服务器上可能会提供公司真实所有权的线索。

以下截图显示了托管在同一台服务器上的域名列表：

| IP 上的域名 | 192.20.10.15 | 子网上的域名 | 192.20.10.1-255 |
| :--- | :--- | :--- | :--- |
| 总共 263 个。 |  购买列表 | 总共 24,306 个。 | 购买列表 |
| originaldomain.com | | originaldomain.com | |
| secretdomain.com | | competitiondomain.com | |
| othersecretdomain.com | | fakedomain.com | |
| superdomain.com | | otherdomain.com | |

图 12.3 – 显示托管在同一台服务器上的域名列表输出

顺便提一下，如果你使用第三方共享托管环境，这些信息可能也有助于判断你的网站是否会因为同一服务器上托管的糟糕页面而被封禁（列黑）（这可能会影响你邮件服务器的可用性）。

## 网络爬虫工具

这里有一些工具设计用于从给定域名收集所有公开信息。

你可以利用这些工具来确定从你的网站或 Web 程序可以获取多少信息，以确保你的私有数据保持机密。

这里列出了一些网络爬虫工具的示例：

- https://webscraper.io：一个流行的浏览器扩展，允许你从给定网站收集所有公开信息。
- https://www.scraperapi.com/: 该网站为用户提供用于执行爬取的 API。
- https://www.scraping-bot.io/: 一个用于爬取网页的用户友好系统。

如下截图所示，大多数爬虫系统会输出几种类型的文档，包括 .html、.doc、pdf、xls 等：

![](img/8c6a223c57e25ea0cc1593903a1b920f_361_0.png)

图 12.4 – 网络爬虫

记住，你应该只在自己的服务器上进行爬取，因为这在某些国家可能是非法的。

## 防止网络爬虫

你也可以采取一些措施来防止爬取。这里列出了最有效的：

- 实现 Web 应用防火墙 (WAF)。
- 使用反机器人系统如 CAPTCHA。
- 请求用户注册。
- 使用 IP、域名的黑名单。
- 使用蜜罐来识别攻击者。

这些提示可能有助于防止自动化爬取，但你的系统在本章开始时仍可能存在漏洞。

## 使用 Google hacking (dorks) 检查数据暴露

我知道许多人讨厌这种做法被称为 hacking（主要是因为这不需要技术技巧）；然而，许多人将 Google dorks 称为 Google hacking，我决定保留这个名称以引起关注。

Google dorks 是基于利用某些搜索命令和参数在互联网上收集私有文件。正如之前提到的，这不是 Google 创建的工具；相反，它是利用该搜索引擎来寻找敏感信息。

让我们回顾一些你可以使用的 Google dorks 以确保你没有暴露在互联网上。你可以看到一个示例：

`site:yoursite.com filetype:xls intext"phone"`

检查你的网站是否有包含手机号码的 .xls 文件。你可以通过将手机关键字改为任何想要搜索的其他属性并将文件类型改为 .pdf、.doc 等来改进。这里有一个代码示例显示如何操作：

`site:yoursite.com filetype:sql "# dumping data for table" "PASSWORD" varchar`

在你的网络资源中搜索开放数据库。

如下截图所示，你需要仔细查看这些 dorks 的结果，以确定结果显示的是基础数据（如变量名）还是更敏感的数据（如明文密码）：

```sql
`id int(11) NOT NULL auto_increment,
`username` varchar(30) NOT NULL,
`password` varchar(255) NOT NULL,
`type` enum('admin','user') NOT NULL,
`date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
`addby` int(11) NOT NULL,
PRIMARY KEY (`id`)
ENGINE=MYISAM DEFAULT CHARSET=latin1 AUTO_INCREMENT=5;

--
Dumping data for table 'admin'

INSERT INTO 'admin' ('id','username','password','type','date') VALUES
('1','Admin','mypassword','admin','2020-05-05')
```

图 12.5 – Google dork 输出

