
包含了色情内容、神秘的火焰以及关于被囚的黑客 Kevin Mitnick、《纽约时报》记者 John Markoff 等人的通报。创始人发现的不是当天的头条新闻，而是如下的谩骂内容：

> 首先，我们必须说……我们拥有你们这群蠢蛋。记住，蠢蛋的屁股很可爱。我们喜欢可爱的屁股。其次，这里有许多失败者，很难找到一个最该被侮辱的人。

言而易之，这次攻击破坏了这家国家级权威报纸最无价之宝：对其读者的信任。类似的“内容替换”攻击也破坏了成千上万个政府、公司和个人网站。1998 年 7 月，一个反核能黑客团体同时攻破了 300 个网站，将首页替换为一段长漫的世界和平信息。²

这些攻击中的许多代表了系统安全的完全泄露。Web 服务器也面临着较温和的危险。HTTP 1.0 协议包含“基本身份验证”`Basic Authentication`方案，涉及简单的挑战与响应。通过提供用户名和密码，用户可以访问受保护的 Web 资源。遗憾的是，用户名和密码都是明文传输的，可能会被窃听者拦截。

在 Web 服务器上运行 CGI 程序对系统安全带来了一系列风险。接收并处理用户输入的 CGI 程序特为脆弱——不安全的代码允许攻击者在服务器上执行任意命令，其权限可能与 `http` 用户相同，也与拥有脚本的用户相同（取决于服务器是否配置得当）。这个经典的安全漏洞在以下针对校园 CGI 的示例攻击中得到了说明：

> 2. 参见 `http://www.wired.com/news/news/technology/story/13446.html`

| User | UID | GID | Home | Shell |
| :--- | :--- | :--- | :--- | :--- |
| daemon | 1 | 1 | : :// | |
| bin | 2 | 2 | /usr/bin | |
| sys | 3 | 3 | : :// | |
| adm | 4 | 4 | Admin | /var/adm |
| lp | 71 | 71 | Line Printer Admin | /usr/sp/lp |
| smtp | 0 | 0 | Mail Daemon User | /bin/false |

.... 继续 :P

在这里，一个随机的浏览器只需几次击键，就能显示 `/etc/passwd` 的内容，然后这些内容可以被密码破解程序处理。

### 提示

此风险在 CERT CERT告告中曾简要描述——参见 `http://www.cert.org/advisories/CA-97.25.CGI_metachar.html`

你可以在 `http://www.rootshell.com` 找到大量的 CGI 漏洞利用示例——只需在搜索引擎中输入“CGI”即可。

Web 安全中一个很少受到关注的领域是维护 Web 服务器日志的机密性。Web 服务器软件通常维护关于谁访问了网站、查看了什么等详细信息。当系统安全被破坏时，这些潜在的敏感信息可能会泄露，从而破坏你的访问者对你网站所产生的隐含信任。

最后，Web 服务器极易受到拒绝攻击的威胁。这种风险源于 Web 及其他信息服务器所面临的基本安全悖论——你希望向全球公众提供服务，但这让你容易受到那些愿意滥用权限的人的影响。虽然减轻这种风险的方法，但它仍然是将私有资源公开化时的固有问题。

## Web 客户端风险

浏览 Web 是一项通用不安全的活动。漏洞、不适当的“活动内容”和脚本，以及粗糙的 Web 服务器管理可能让上网用户面临以下风险：

- 应用程序和系统崩溃
- 包括病毒和木马在内的恶意代码
- 机密信息丢失，以及
- 隐私泄露

遗憾的是，最容易受到客户端 Web 风险影响的系统是那些安全模型极简或不存在的系统：Microsoft Windows 和 Macintosh。与 Microsoft Internet Explorer 和 Netscape Navigator 等浏览器相关的漏洞和安全问题清单已超出本书的范围。幸运的是，这些问题已经在主流媒体中引起了广泛关注（“Netscape 发现新漏洞”）。脚本漏洞很好地说明了这种现象。

主要的浏览器都支持在 HTML 中下载脚本并在浏览器中执行它们。通常，这些程序的设计是为了与用户交互并在浏览器与服务器之间传输信息。多次，在 Netscape 的 JavaScript 和 Microsoft 的 VBScript 中发现了重大漏洞——例如，参见 `http://www.cert.org/advisories/CA-97-20.html` 即使没有漏洞，恶意网站管理员也可以包含脚本伪造错误信息或提示输入登录 ID 和密码。Danny J. Gremoire 将这些称为“斯巴达马”`Spartan Horses`——它们比木马简单。HotMail 等大型网站已被这种简单的破解方法侵害，Gremoire 在 `http://theworld.com/spartan` 对进行了记录。

其他客户端风险源于隐私。许多网站向客户端写入标识 Cookie——Cookie 可以跟踪用户并了解他们去了哪里。根据规定 Cookie 处理的 RFC，客户端软件应提供一种方法来指定哪些域名保存 Cookie。遗憾的是，这一功能尚未实现。

> 参见 `http://www.faqs.org/rfcs/rfc2109.html`

## 传输风险

Web 客户端和 Web 服务器之间传输的信息可能会被链路两端的窃听者或中间的任何地方拦截，包括：

- 客户端的局域网
- 服务器的局域网
- 客户端的 ISP
- 服务器的 ISP
- 两者之间的任何中间网络

“安全 Web 服务器”和“浏览器安全”术指的是双方交换加密信息的能力，这些信息对窃听者来说是无用的。除非客户端和服务器之间存在“安全的”加密链路，否则传输的任何信息都会受到数据嗅探和其他拦截技术的威胁。

> 提示 没有对 Web 安全风险的审查如果不引用 Lincoln D. Stein 编写的《万维网安全 FAQ》，可以在 `http://www.w3.org/Security/Faq` 找到。

## 防止 Web 服务器风险

### 选择安全的服务器软件

有许多适用于 UNIX 上的 HTTP 服务器可供，从昂贵的软件包到协作开发的开源包，甚至可以追溯到 Web 诞生时的过时进程。如果 Web 服务器功能是至关重要的，你应该对它们的功能和安全性进行评估。

> 提示 `http://webcompare.internet` 的 WebServer Compare 网站包含了 UNIX 及其他平台软件的详细功能对比。

以下是已知在 Linux 上运行的 Web 服务器软件部分列表：

- AOLserver 2.3来自 America Online Inc.
- Allegro RomPager 2.20，来自 Allegro Software
- Apache 1.3来自 The Apache Group
- EmWeb Embedded Web Server R3_03，来自 Agranat Systems, Inc.
- Hawkeye 1.3.3，来自 Hawkeye Project
- Java 1.1，来自 Sun Microsystems
- Roxen 1.3，来自 Idonex AB
- Spyglass MicroServer 2.0，来自 Spyglass
- WebControl 2.0，来自 Rapid Logic, Inc.
- Xitami 2.2b，来自 iMatix
- Zeus Web Application Server 3，来自 Zeus Technology
- vqServer 1.03

可以使用所有这些软件包，也可以随大流并默认使用“市场领导者”——Apache。自1996年以来，Apache一直是互联网上最流行的Web服务器。Netcraft 每月对Web服务器的安装量进行调查；截至本文编写时的最新调查（1999年5月）显示，互联网上超过一半的网站正在使用 Apache（在这些IX 节点中，大多数Windows版本的 Apache 仍处于实验性阶段）。它的部署范围比所有其他 Web 服务器的总和还要广泛。

流行的程序并不一定是安全的程序。然而，Apache受益于其作为开源软件开发模型中不可或缺的一部分而接受的严格审查。具体来说，Apache 代码受益于其无处不在。漏洞会被迅速发现并消除。

Apache 在其最新版本（1.3版本）中提供的安全特性包括：

- 可以根据域名名、IP 地址、用户和用户组禁止访问
- 可以配置用户组（而不是单一的用户列表）
- 可以在不重启服务器的情况下修改用户访问控制列表（ACL）
- 可以在所有者的 UID 下进行 CGI 脚本的执行
- 基于目录的文档权限是分级的
- 可以根据安全规则隐藏文档的部分内容
- 支持 SSL 第2 版和第3 版
- 可用密码机制
- 安全规则可以基于 URL

### 提示

你可以通过 `http://www.apache.org` 了解更多关于 Apache 和 Apache Group 的信息。

## 注意事项
