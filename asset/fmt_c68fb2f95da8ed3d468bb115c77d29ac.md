
我们将选择 2) 站点克隆。将被要求输入 URL。我们将克隆 `https://www.facebook.com`。

注意我们正在输入精确的 URL 并指定使用 HTTPS 还是 HTTP URL。在大多数情况下，这没有区别，因为我们不托管安全网站，但在某些情况下 HTTP 网站可能与 HTTPS 网站不同。

将被要求输入 用于托管假网站的 IP 地址。这可能是你的 Kali Linux 盒的 IP 地址。然而，如果你计划通过 NAT 转换（通过上游防火墙）引导受害者到地址，请输入 NAT 地址。

一旦克隆了网站并配置了监听端口，SET 将开始等待连接，如下方的所示：

- 凭据收集器允许你利用克隆功能从网站处收集凭据或参数。
- 此选项用于指定服务器 POST 的 IP。
- 如果你正在使用外部 IP，请在此标签处使用你的外部 IP：`10.0.0.255` 作为 Harvester/T 的回。

下一步是引导用户访问虚假网站。实现这一点的常用方法是发送电子邮件，也称为网络钓鱼电子邮件。SET 可以为你自动化此操作，但在本例中，我们决定手动执行。下一个示例显示了使用我们克隆的 Facebook 链接的假电子邮件。当用户点击 `www.facebook.com` 上的链接时，他们将被引导到我们的假网站 `facebook.secmob.net`。

## 客户端攻击

在下面的截图中你可以看到一个看起来像 Facebook 的克隆页面，但 URL 并不是真正的 Facebook。这种攻击假设受害者不会注意到 URL 细微的差别，这就是为什么真实的钓鱼攻击会使用与真实网站相似的域名。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_159_0.png)

当受害者在虚假网站上输入姓名时，SET 将将用户重定向到真实网站。在大多数情况下，用户会在真实网站上再次输入密码并登录，而完全没有意识到自己遭受了攻击。在运行的 Kali Linux 系统上，你可以看到密码被捕获了。

```
$! 我们抓到了目标！正在打印输出：

PARAM: UserName=Ladi

POSSIBLE PASSWORD FIELD FOUND: UserPassword=ILoveToDance

PARAM: target=62

PARAM: Log+on.x=59

PARAM: Log+on.y=10

*] 完成后，按下 CTRL-C 生成报告。
```

## 第 4 章

除了实时日志外，SET 还会生成一份事件报告，以便攻击者稍后利用被盗取的凭据。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_160_0.png)

### 社会工程工具包 (SET) 报告生成器
#### 由社会工程工具包生成的报告

欢迎使用社会工程工具包报告生成器。此报告应包含在成功钓鱼攻击期间的信息，并为您提供网站以及所有收集到的参数。请记住，SET 是开源、免费且供信息安全社区使用的。此工具用于行善，而非作恶。

在使用如 SET 等工具攻击客户端时，渗透测试人员理解客户端的行为至关重要。实现这一点最有效的方法之一是使用代理来检查和检查 Web 请求。

在第 6 章“Web 攻击”中，我们将更详细地介绍代理；然而，学习如何在使用攻击（如上段所述的用法 SET）时检查客户端的行为仍然非常重要。

## MitM 代理

MitM Proxy 是渗透测试人员用于检查客户端漏洞的绝佳工具。它允许管理员检查 HTTPS 连接、暂停、检查并响应流量。MitM Proxy 允许管理员修改来自 Web 服务器的请求或响应。

MitM Proxy 允许渗透测试人员快速检查攻击，并看到来自浏览器的请求和响应。可以通过进入 Kali | Sniffing/Spoofing | Web Sniffers 并选择 `mitmproxy` 来启动 MitM Proxy。

[ 143 ]

> 建议在设置 SET 攻击以及分析该攻击行为时使用 MitM Proxy。你应该在测试环境中同时运行 SET 和 MitM Proxy。

一旦加载了 MitM proxy，你将需要将客户端浏览器指向你的 Kali 服务器。MitM 将显示在客户端侧发生的 Web 交易，如下截图所示：

```
GET https://github.com

-- 200 OK text/html 5.52kb

GET https://a268.a.akam.net/github.com/stylesheets/bundles/github2-24f59e3ded11f2a

-- 1cf7e9e73082bdd50fcf8b.css

-- 200 28.2kb

GET https://a268.a.akam.net/github.com/images/modules/header/logov74x-hover.png71

-- 200 image/png 6.0kb

GET https://a268.a.akam.net/github.com/javascript/bundles/jquery-b2ca07cb3c90cec055d88b1a30bcc2452596.js

-- 200 application/x-javascript 32.9kb

GET https://a268.a.akam.net/github.com/stylesheets/bundles/github-cb564c47c51a1a4

-- 200 text/css 37.09kb

GET https://a268.a.akam.net/github.com/images/modules/home/logos/facebook.png?713452695

-- 200 image/png 5.55kb
```
