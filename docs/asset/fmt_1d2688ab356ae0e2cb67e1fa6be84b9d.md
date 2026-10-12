
原则上，你现在可以在`changedetection.io`的设置中将获取方法更改为`Playwright Chromium/JavaScript via 'ws://playwright-chrome:3000'`，但默认的获取方法要高效得多。建议仅在默认方法不起作用的个别监控中更改获取方法。

你可以在监控设置的`请求`选项卡中通过更改`获取方法`为`Playwright Chromium/JavaScript via 'ws://playwright-chrome:3000'`来进行此更改。保存你的更改并等待排队的监控执行。如果一切顺利，变化检测监控现在就能工作了。然而，一些网站（如`Amazon`）会检测到你正在使用机器人访问它们，因此它们不会显示期望的内容。你可以通过点击变化检测监控旁边的`预览`来检查这一点。如果你转到`截图`选项卡，你会看到容器内的浏览器看到的页面外观，这通常显示验证码。此问题有解决方案，例如`Bright Data`的（付费）`Scraping Browser` [8]，但这超出了本文的范围。

## 视觉过滤器选择器和浏览器步骤

如果你正在使用`Chromium/JavaScript`服务器，你会获得更多的可能性，例如用于过滤器。你无需查找`HTML`源代码并构建`XPath`表达式，只需点击监控设置中的`视觉过滤器选择器`选项卡即可。这会显示网页，当你将鼠标悬停在页面的不同部分时，你会看到一个红色边框框（图 6）。点击框以选择你希望用于变化检测的元素。这会自动在`过滤器 & 触发器`选项卡中填充相应的过滤器。你还可以选择多个元素。点击保存以确认过滤器。

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_29_0.png)

图 6：选择你要监控的网页部分。

使用`Chromium/JavaScript`服务器的另一个优点可以在浏览器步骤选项卡中找到。通过点击那里的播放按钮，`changedetection.io`会与`Web`浏览器建立实时连接，你可以从该浏览器内与页面进行交互。然后你可以执行诸如点击接受`Cookie`框或登录网站等动作。说到这里，`changedetection.io`会在每次变化检测监控之前替换这些步骤。你可以使用此功能，特别是结合视觉过滤器选择器，来获取仅在登录后才显示的信息的警报，例如新发票或私密消息。当然，请适当调整检查之间的时间：你不想因为`changedetection.io`登录过于频繁而导致你的账户被封锁。

## 结论

`Changedetection.io`可以是一个监控网页变化的绝佳工具。一旦你在几个没有`RSS`源的网站上运行它，你很可能会添加越来越多的变化检测监控。过滤器和触发器非常强大，你甚至可以让`changedetection.io`使用正则表达式从页面中提取文本。不知不觉间，这个服务将不断为你浏览网络，通知你需要知道的一切。

# 作者

`Koen Vervloessem`已经撰写关于`Linux`和开源、计算机安全、隐私、编程、人工智能和物联网的文章超过 20 年。他拥有计算机工程哲学硕士学位，并教授`Linux`、`Python`和`IoT`课程。你可以在他的网站`koen.vervloessem.eu`上找到更多信息。

# 信息

- 1. `RSS`: <https://www.rssboard.org/rss-specification>
- 2. `changedetection.io`: <https://changedetection.io>
- 3. `changedetection.io` 源代码: <https://github.com/dgtlmoon/changedetection.io>
- 4. `Apprise`: <https://github.com/caronne/apprise>
- 5. `Mailjet`: <https://www.mailjet.com/>
- 6. `Apprise wiki`: <https://caronne.github.io/apprise-wiki>
- 7. `Chrome` 扩展: <https://chromewebstore.google.com/detail/changedetectionio-website/kelfcmnmlhmknjmnbiimhofdtjejdokp>
- 8. `Bright Data` 的 `Scraping Browser`: <https://brightdata.com/products/scraping-browser>

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_30_0.png)

## 商店购物

`shop.linuxnewmedia.com`

### 用酷炫的 Linux 技巧提高效率

用这套鼓舞人心的技巧和`Linux`极客的快捷键来提升你的`Linux`技能。

- 在命令行上使用`Google`
- `OpenSnitch` 应用程序防火墙
- 解析`systemd`日志
- 使用`lazygit`控制`Git`
- 使用`DOSBox`运行旧`DOS`游戏
- 更多！

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_30_1.png)

在线订购：`shop.linuxnewmedia.com`

# Linux 后门攻击剖析

**通过后门渗透**

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_31_0.png)

网络犯罪分子正日益发现`Linux`系统，并适配此前为`Windows`系统设计的恶意软件。我们将带你深入了解一款著名`Windows`勒索软件工具的`Linux`版本。

作者：`Thomas Boele`

自年初以来，`Check Point Research` (`CPR`) 的安全研究人员一直在调查一个专注于东南亚、非洲和南美的中国网络间谍威胁行为者的活动。该威胁行为者的工具包包括跨平台后门`DinodasRAT` [1]，也被称为`XDealer`，此前曾观测到中国组织“罗鱼”（`LuoYu`）的攻击中使用过该后门。

本文提供了`DinodasRAT`（又名`Linodas`）`Linux`版本（v11）的技术分析。`Linux`版似乎比`Windows`版更复杂，并且拥有一系列专门针对`Linux`服务器的功能。此外，受调查的版本引入了一个独立的绕过模块，以隐藏系统中的恶意软件痕迹。系统二进制文件的执行通过代理进行了修改。

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_31_1.png)

**图 1：** `Dinodas` 示例（左）与开源代码在识别操作系统版本功能上的相似之处。© `Check Point Software`

照片由`David Svedendal`拍摄于`Unsplash`

# 深入解析

## Linodas

**表 1：后门的字符串**

| 标记 | 首次发现时间 | 哈希值 |
| :--- | :--- | :--- |
| `Linux_%s_%s_%s_V7` | 2021年7月 | `3d93b895a4e1441516302681674f4989b0df20232ac2b211fab601af0fcff13bfbf830191215e0c8dd207ea320d8e795990c6fbb36669932e660c4c0588f8c0eff` |
| `Linux_%s_%s_%s_V10` | 2023年1月 | `15412d1a6b7ff97ad45bdc32cf8291d951d9ccca08298a0cc6a354353284e456302acfcdfe0cc8ce976f1ff7905800ae22c07dda495c0aae14f594c7263a29b2` |
| `Linux_%s_%s_%s_V11` | 2023年11月 | `ebfdf3d3c0867b229e66d88b7570be4e6619c64fae7e1fb50d52be387ff36c980c8e` (嵌入模块) |

**表 2：Linux 和 Windows 版本的比较**

| 版本 | 操作系统 | 哈希值 |
| :--- | :--- | :--- |
| `Linux_%s_%s_%s_V11` | `Linux` | `6302acdcfe30cec5e9167ff7905800a6220c7dda495c0aae14f594c7263a29b2` |
| `Win_%s_%s_%s_V10` | `Windows` | `57f64ff170dfcaa1150493e3ad3f63ea6f11dfca71ad1722e12ac07774afa1a829` |

## Dinodas 起源

若干线索表明`DinodasRAT`最初基于`SimpleRemote` [2] 开源项目。`SimpleRemote`是一个远程访问木马`Ghost RAT` [3]，但它有一些额外的改进。`SimpleRemote`和`DinodasRAT`旧版本之间的相似之处包括使用相同的`Zlib`库（版本`1.2.11`）以及代码中的一些重叠（图 1）。
