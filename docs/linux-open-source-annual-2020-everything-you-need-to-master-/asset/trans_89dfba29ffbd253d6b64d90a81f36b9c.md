

试图向你兜售 VPN，所以我们还是用 https://dnsleaktest.com 吧，它不会这么做。这是一个有趣的实验：逆向那些 DNS 更改，找到你 ISP 的 DNS 设置，然后将你的 DNS 服务器改为公共服务器（如 1.1.1.1），再重新运行测试，看看你的 ISP 或其他不良分子是否正在劫持你的 DNS 请求。

## 了解你的洋葱（Tor）

Tor 网络，前身为 The Onion Router，由数千台志愿者运营的 PC 组成：截至 2019 年 7 月，列表中有约 1,000 个中继桥（bridges）和 7,000 个中继器（relays）。这些节点通过层层加密将连接路由到常规的“cleanweb”地址或 Tor .onion URL。在返回过程中，这些加密层被逐层移除，完成一个“电路”，这使得整个系统极难被窃听。

使用 Tor 网络最简单的方法是从 www.torproject.org/download 下载 Tor 浏览器。在 Linux 上，它以 XZ 文件形式发布，你可以使用以下命令进行解压：

```bash
$ tar xvjf tor-browser-tor-browser-linux64-8.5.4_en-US.tar.xz
```

然后直接从 tor-browser_en-US/ 目录运行它。由于新版本发布频繁且往往迫在眉睫，而 Tor 浏览器又以相当自包含的形式发布，因此依赖发行版的打包方法来分发它并不明智。本地安装的 Tor 浏览器会像 Steam 那样在你的主目录中保持自我更新（如果你使用过 Steam 的话）。不过，对 Tor 的操作不仅仅局限于浏览器：不同的应用程序可以通过 Tor 进行代理，类似于通过 SSH 隧道化连接。

> 浏览器并非一座孤岛（这是一个深刻的洞察……你是在洞穴里待了两周没写这个特性，才悟出这个道理吗？——编者注），其运行的操作系统会暴露出关于 Tor 浏览器使用方式的各种线索。所以，对于那些宣传册所称的“军用级安全”，你需要一些特别的东西。这就是 Tails，一个你可以从 U 盘启动的发行版，它不会记住你做任何事情。Tails 包含了 Tor 浏览器。但你不应该使用它，至少除了满足好奇心之外不应该使用。

事实上，你只应该信任版本号高于 3.14.2 的 Tails，因为当时发布了一个补丁，修复了 Tor 浏览器、Thunderbird 和其他软件中的多个漏洞。其中一个影响 Tor 浏览器的漏洞是在三月举行的 Pwn2Own 竞赛期间发现——并实际上赢得了该竞赛的浏览器类别。因此，你真的不应该信任旧版本来处理你的私人数据。当然，完全有可能在我们撰写此文和你阅读它之间，会出现其他问题和新的发布，所以请遵循我们下面方便的三步指南来下载和安装最新版本。

![](img/7a0a282248f9658f0c87e55744c797b6_56_0.png)
![](img/7a0a282248f9658f0c87e55744c797b6_56_1.png)
![](img/7a0a282248f9658f0c87e55744c797b6_56_2.png)
![](img/7a0a282248f9658f0c87e55744c797b6_56_3.png)

## 追求 TAILS（尾部/隐私）

## 强化你的浏览器

Web 浏览器可能是你机器上使用最多的应用程序，因此它值得特别关注。

我们通常对应该使用哪个浏览器持非常中立的态度，但至少在本文这个主题中，我们要稍微偏离这种中立。Chrome 一直是一个流畅的浏览器，但内置的所有 Google 特性让我们感到恶心。Chromium 是一个更好的选择，因为它完全是开源的，没有 Flash，并且总体上对 Google 服务的依赖较少。由于关于后者再分发的规则，在大多数发行版上安装 Chromium 也比 Chrome 更容易。

然而，去年 Chrome 和 Chromium 中都出现了一个变化，让我们都变得警惕起来。这个变化涉及“登录 Chrome”功能，该功能将浏览器连接到你的 Google 账户，并可以选择同步书签、扩展和浏览历史——就像在 Chrome OS 中一样。直到 Chrome 69，这个选项与通过其网页登录 Google 服务是分开的——我们认为这是一件好事。但现在，仅仅登录这些服务就将整个浏览器与该账户连接起来了。我们对登录 Google 或其他任何浏览器级服务本身没有问题，但这应该由用户明确执行。

### 其他浏览器

还有其他浏览器选择。以隐私为中心的 Brave 浏览器（https://brave.com）基于 Chromium，拥有一个有趣的资金模式。用户通过观看广告获得 BAT（基本注意力代币）奖励。BAT 基于以太坊区块链，代币可以用现金购买，或者送给你最喜爱的 YouTube 明星。我们并不太喜欢广告，但如果他们的收入用于开发更好的浏览器，我们可能会破例。

还有 Ungoogled-Chromium 项目（https://github.com/Eelston/Ungoogled-chromium），它努力摆脱对任何 Google Web 服务依赖，并启用一些增强的隐私控制。通过这样做，它挑战了 Chromium 基本上是去 Google 化 Chrome 的观念。还有其他类似的项目，最值得注意的是 Iridium（https://iridiumbrowser.de）和 Inox，后者是一个针对 Chromium 代码库的模块化补丁集（https://github.com/gcajar/inox-patchset）。Gnome 和 KDE 都有自己的浏览器项目，分别是 Web（前身为 Epiphany）和 Falkon（前身为 Quetzal），它们都比常见的浏览器轻量级得多。它们都对收集你的数据不感兴趣。

![](img/7a0a282248f9658f0c87e55744c797b6_57_0.png)

我们应该指出，这些强制登录目前并不同步书签等。Google 的隐私政策（参见 www.google.com/chrome/privacy/#browser-modes）仅仅提到在“已登录”模式下，浏览器可以连接到用户的 Google 付款账户——这并不暗示有额外数据发送到 Google。然而，我们是愤世嫉俗的，即使现在没有数据被显式共享，这样的变化也很容易悄然发生。因此，我们推荐 Firefox，但这只是我们的个人意见。显然，如果你不经常使用 Google 账户（这是好事），这些都不重要。在加密高手 Matthew Green 的博客上阅读更多相关内容，http://bit.ly/1xf253crypto

无论你使用哪种浏览器，我们都建议使用像 uBlock Origin 这样的广告拦截器——虽然我们还从事出版业，所以我们也要求你在值得信赖的高质量网站（这名单很短——编者）上禁用它。第三方广告网络中存在太多可疑的操作；例如，参见我们在 LXF51 中的恶意软件专题。出于相关原因，我们也建议启用浏览器设置中的“请勿跟踪”（Do Not Track）选项。从设计上讲，这需要由用户设置——这是你发送给广告商的一个信号，表明你对其不感兴趣。

一般来说，浏览器扩展应谨慎对待，但我们完全认可 EFF 的 HTTPS Everywhere，它确保尽可能使用 HTTPS。许多网站通常仍会错误地链接到 HTTP 资源，即使你到主页的连接是通过 HTTPS 进行的。EFF 的 Privacy Badger 也是一个不错的选择：Privacy Badger 不使用预分配的黑名单，而是在使用过程中学习，所以你早期可能需要给它一些点击机会。

![](img/7a0a282248f9658f0c87e55744c797b6_57_1.png)

有时候知道自己在世界上是独一无二的很棒，但就 Web 浏览器而言，我们希望自己与普通大众难以区分。

Privacy Badger 会嗅探广告网络是否尊重你的“请勿跟踪”设置，如果它们不尊重，就会将它们列入黑名单。

广告跟踪器最令人担忧的方面之一是浏览器指纹识别的潜力。即使广告商不知道你的姓名，他们也可以通过 JavaScript、HTML5 和传统的内容头的魔力，让你的浏览器做一些“花样动作”——并基于这些体操动作，对其产生唯一的指纹。这些“花样动作”包括字体可用性、用户代理字符串、插件和窗口大小。Tor 浏览器甚至会在你最大化窗口时警告你，这将向当前网站泄露你的显示器分辨率。仅仅使用 Linux，你的浏览器就将自己标记为少数派，这就是为什么 Tor 浏览器通过其 User Agent 字符串提供错误信息，声称自己是：

```text
Mozilla/5.0 (Windows NT 6.1; rv:60.0) Gecko/20100101 Firefox/60.0
```

浏览器指纹识别并不是什么新鲜事物（独一无二的 Brown 博士在 LXF190 中讨论过，当时我们还能付得起他的稿费），但考虑到现在已经可能持有的关于我们的所有其他信息，这一点更加令人担忧。在 EFF 的 Panopticlick 网站（https://panopticlick.eff.org）上查看你的独特程度，并尝试对此做些处理。不，我们在这里无法解释熵——这可能表明我们也不理解它。

Stack Overflow 最近无意中成为了嵌入在广告中的指纹识别脚本的主机。如果那是一家提供二流产品广告的有疑问的广告代理公司，这很好地说明了我们的观点，但那个有问题的广告是由 Google 投放的，宣传的是 Microsoft 的 Azure 云服务。说真的，有问题的 JavaScript 可能正被用来识别机器人而非跟踪用户。

## 偏向隐私

Web 浏览器的设置页面如今变得简单多了，但这并不意味着 Web 浏览器的可配置性降低了。这仅仅意味着这些选项中的许多更有可能让普通用户感到困惑而非受益。例如，搜索“chromium command line switches”，或者在 Firefox 中浏览到 about:config，你会发现多得摇着一根棍子都数不完的晦涩选项。顺便说一句，你会在这里找到一个 privacy.resistfingerprinting 选项，它可以缓解指纹识别请求。

![](img/7a0a282248f9658f0c87e55744c797b6_58_0.png)

在本专题中我们有点反 Google，但我们应该注意到，其浏览器沙箱技术是无人能比的。

![](img/7a0a282248f9658f0c87e55744c797b6_58_1.png)

在 Firefox 的配置目录中，这些高级选项都存储在一个名为 prefs.js 的 JavaScript 文件中，例如 '~/.mozilla/firefox/xxxxxx.default'。

人们为了增强 Firefox 的默认选项走了极端的路径，你可以在 https://github.com/plylyukk/uxer.js 找到一个最全面的示例之一。杂志中没有足够的空间来详细介绍所有这些选项，但请你在空闲时研究它们，并考虑制作自己的 user.js 文件，下次启动浏览器时将以稳健的方式合并到主 prefs.js 文件中。类似的项目是 ghacks-user.js，你应该在 https://ghacksuserjs.github.io/ghacks-user.js 研究它。如果你安装了 Git，你可以立即开始使用 Pplylyukk 的 user.js：

```bash
$ cd ~/.mozilla/firefox
$ git clone 'https://github.com/plylyukk/uxer.js.git'
$ cd xxyyzz.default
$ ln -s ../uxer.js user.js
```

该文件所做的最重要的一件事是控制 WebRTC。WebRTC 虽然被设计为实时视频通信协议，但可被用于识别代理或 VPN 背后的 IP 地址。相关设置可以通过在 about:config 页面搜索 media.peerconnection 找到。你可以在 https://wiki.mozilla.org/Media/WebRTC/Privacy 阅读更多关于这些 WebRTC 设置的作用。好消息是，如果你受够了网站请求向你的桌面发送推送通知：这里概述的方法将通过 dom.webnotifications* 选项完全禁用这些通知。

你现在可以做的最简单的事情之一是停止使用 Google 作为默认搜索引擎，转而使用 DuckDuckGo。你可能无法获得习惯的那种最新结果，但你也知道你的搜索与你的身份无关。Firefox 和 Chrome 都允许你从设置部分的“搜索”中进行此更改。如果你想念为你“量身定制”的 Google 结果，请在搜索查询前加上“lg”——但要记住，即使你没有登录 Google，这些搜索可能仍然会与你的账户绑定。

> 夺回你的隐私！立即切换到 DuckDuckGo——它不会跟踪你或将你的搜索查询卖给坏蛋。

