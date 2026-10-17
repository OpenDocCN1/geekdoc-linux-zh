
```javascript
console.log('Now executing the 'function.')
```

或者：

```javascript
console.log('username was ' + username + '*');
```

实际上，Firebug 能够实现比嵌入式、类似 print 的字符串得多的效果：

```javascript
console.log('username was %s', username)
```

Firebug 提供了一系列日志函数，每个函数都以不同的级别和颜色输出。这些函数是：

- `console.debug`
- `console.info`
- `console.warn`
- `console.error`

这些方法的输出显示在 Firebug 控制台中，你可以通过点击 Firebug 图标正下方的 Console 按钮来查看。请注意，使用这些方法可能与缺少 Firebug 的浏览器不兼容。

控制台不仅仅是一个接收消息的区域。与 Ruby 的 IRB 和 Python 的交互模式一样，Firebug 的控制台允许你在页面上下文中执行 JavaScript。对获取页面上的表单列表感兴趣吗？只需：

```javascript
document.forms
```

你就会获得所有的表单。你还可以使用 Prototype 风格的方法获取有关页的信息，例如：

```javascript
$('$cb_form')
```

在 Linux 首页上，它会产生以下头部：

```html
<form id='cbv_form' method='get'>
```

Firebug 还具有监控函数、设置、断点和性能分析的功能。进入 Script 按钮，你将看到包含的 JavaScript 文件的源代码。（你可以通过选择菜单更改你正在查看的行）。将鼠标光标指向某行代码可以带来有关这些对象状态的信息。

点击断点允许复制函数（当尝试与其他程序员通信或编写专栏程序时），或者通过单步执行代码来处理断点：

要找出哪些 JavaScript 函数耗时最长、哪些运行最频繁，请使用 Firebug 调试器。这非常简单，只需点击 Console/Profile 标签，你就可以获得关于变量的信息，使用 Firebug 报告的每个 JavaScript 函数调用的次数、每次调用的时间以及函数定义的位置。

最后，Net 按钮让你在调试器中轻松跟踪任何 Ajax 调用。点击 Net 和 X 会产生页面上所进行的 Ajax 用的图形化指示，以及每个调用执行所需的时间。如果你正在开发 Ajax 应用程序，这是寻找瓶颈的最佳方法。

不做出某种产品革命性的改进是很罕见的，但在 Firebug 的案例上我很遗憾不得不这样做。它在一个设计精美、易于使用的软件包中包含了大量信息。在我的软件包中包含一种类似 Wisp 的感觉的能力，就像我正与一个实时环境交互一样。Firebug 赋予了我“看到”我的页面正在做什么并更好地理解它们的能力。

除了 Web Developer，Firebug 已成为我工具箱中不可或缺的工具。通过这种方式，Firebug 开始证明它是一个互联网应用程序平台，而不仅仅是一个 Web 浏览器。

Raven Meuren 是一位资深数据库记者，目前是伊利诺伊州埃文斯顿西北西北大学学习与科学专业的博士生。他与妻子和三个孩子住在伊利诺伊州斯考基（Skokie）。你可以在 wetlandandler.co.il 阅读更多信息。

# 资源

Firebug 主页是 www.firebug.com。该网站上有有限的文档，包括常见问题解答（FAQ）。

作者 John Hewitt 在 Dr. Robb's Journal 中对 Firebug 的介绍：www.ddj.com/199608277。

## RouterBOARD™ 100 系列

由 routerboard.com

### RouterBOARD 133

- 低成本 AP/CPE $89
- RouterOS L4 防火墙/路由
- MIPS32 4Kc 175MHz Embedded
- 32MB SDRAM
- 64MB 板载 NAND 存储
- 三个 10/100 以太网端口 MDI/X
- 三个 miniPCI Type IIIA/IIIB 插
- 电源：9-28V DC；过电压保护
- PoE：12-28V DC（数据线不供电）
- 117mm x 105mm (4.61 in x 4.13 in), 115g

### RouterBOARD 133C

- 低成本 CPE $59
- RouterOS L3 防火墙/路由
- MIPS32 4Kc 175MHz Embedded
- 1MB SDRAM
- 64MB 板载 NAND 存储
- 一个 10/100 以太网端口 MDI/X
- 一个 miniPCI Type IIIA/IIIB 插
- 电源：9-28V DC；过电压保护
- PoE：12-28V DC（数据线不供电）
- 117mm x 105mm (4.61 in x 4.13 in), 79g

# 专栏

### 使用 LINUX 烹饪

### 当 Ajax 扛起世界

如果古希腊人创建了开源 Web 应用，他们会使用 Ajax 吗……抱歉我晚了，Francois。他建议选择它，这对于今晚的菜单是完美的。在 2003 年之后，在有少量质量保证的异步情况下，我信我们将非常享受其中。天哪，Francois！这看起来非常令人印象深刻，但 Ajax 背后的想法是什么？在世界上扛着一个肩膀的……我不明白。Ajax 是什么？不，ami，它不是的。Ajax 不是神；它是古希腊神话中的英雄。在我们的情况下，Ajax 指异步 JavaScript 和 XML。欢迎，ami，非常古希腊风格的编码。尽管如此，我们继续在舒适的你们那里，Francois 在今晚已经挑选好了，毫无疑问，将有一艘船到达酒窖。请，ami， pour酒吧。现在我考虑它，今晚的并不完全合适——这是一种极佳的葡萄酒，ami！之前，我解释 Ajax 主要是为了创建丰富的、交互式的 Web 应用。它不需要让页面加载并到达每次时间。在过去，我使用了基于网页的……但重新加载并感觉是现代的实现。今晚的特性是基于网页的第一个（图1），一种可以易于集成到你网站的应用程序。它包括文件系统、多个客户端历史（这样你可以跟踪早期的对话）并且非常易于设置，不需要数据库。然而，你需要一个使用 PHP 的服务器，这非常完美。在 zip 文件中安装它，提取到你的 Web 服务器路径中。文件带有版本号（v3），你可能想重命名一些更啰嗦的，在之前；有一个子目录包含了文件。这需要你的用户写入，图1。Ajax 简单如此，并提供了丰富的体验。图2。在简单的安装之后，你准备好使用了。

## 服务器 DIRECT™

直达源！更多产品，更好的服务，保证。

## 智能服务器

在你的服务器 DIRECT 系统中使用双核 Intel Xeon 处理器节省时间并降低运行成本

### 1U 双路创新

SDR-6015T-1U 数据中心服务器

1U 规格的两个系统（节点）。每个节点 64 位 Xeon 支持：

- 双处理器 Quad & 双核 Intel 64 位 Xeon
- 高达 32GB DDR4 2667/533 SDRAM 全缓冲 DIMM (FF-DIMM)
- 两个 Intel 以太网千兆以太网控制器
- 两个热插 SATA 驱动槽
- 900/980W 高效电源
- 高密度计算技术
- 减少成本、能量和空间需求
- 支持高达 16 处理器的 Xeon 5300 系列

| SDR-2501 | 2U 应用服务器 | SDR-3111T | 3U 关键任务服务器 | SDR-7045HR-TR+B | 1U 数据集群服务器 | SDR-5500 | 5U 高级存储服务器 |
|---|---|---|---|---|---|---|---|

| 适用于最小部署和支持成本的业务关键服务器 | 提供卓越的可用性、简化性和革命性的扩展性，帮助你构建成本效益的 IT 基础设施 | 适用于寻找第一个服务器或升级现有服务器备份的小企业 | 带有双 CPU 和大量磁备份的 True SAS 6Gb/s 存储服务器 |

- 2U 机架，配备600W 电源
- Supermicro Xeon-E 服务器，配备 Intel 5000® (Blackwell) VIP
- 双核 Xeon 5200 处理器 2.6GHz 1063MHz
- 1024GB RAM，2x512GB DDR4 2666/533
- SAS II 700MB 7200 RPM IMC 带 SATA Gen3
- 24 x 1 热插拔驱动槽
- Intel 以太网双以以太网控制器
- 900/980W 高效电源

SERVERS DIRECT 可以帮助你设计你的高性能服务器系统——今天就致电！

我们的灵活产品目录允许你采购定制解决方案，我们的产品正准备帮助组装需要额外支持的系统。Servers-direct 为可扩展、成本效益的解决方案提供直接支持。

1.877.7287 | ServersDirect.com

Intel, Intel logo, Intel Inside logo, Intel Centrino, Intel Centrino centro, Xeon, Xeon inside®, Steanium, Itium, Pentanium, and Pentium Xeon 是 Intel 公司或其子公司在美国和其他国家注册的注册商标。

# 在 LINUX 中烹饪

使用组 apache，类型为：

```bash
chown apache:apache chattles/*.txt
```

你可能还需要验证 Apache 用户和组都具有写入这些文件的权限。此外，如果你更改了安装位置：要使用 GoChat，请通过 http://yourserver.chat 连接。你将看到一个简单的登录界面（图 2）。

选择一个昵称（或用户名），点击聊天，就可以开始使用了。文本输入框位于屏幕上方。紧正下方是刷新计数器，它可以为你提供帮助。在右侧，如果你需要，可以选择隐藏信息面板。这里链接的“更多选项（More Options）”也很有趣。如果你更改 GoChat 会话的颜色或会话语言（英语、西班牙语），这非常简单。但你可以为自己进行一些自定义。聊天目录下的 `config.php` 文件允许你控制会话。你最感兴趣的项目位于文件顶部：

这些中的大部分内容都是一言自喻的，但默认值可能并不适用。例如，你可能想将文件大小限制为 2MB 以外的值。当你登录默认的 GoChat 会话时，你会发现自己处于“主房间”。在右侧的“房间（Room）”列表中有两个标记为“另一个房间（Another Room）”和“另一个（Another One）”的额外房间。你可以创建它们并根据需要添加更多。这也是通过 `config.php` 文件实现的。在会话失败稍下方是以下内容：

```php
$CHAT_FILE = chattles/chat.txt;
$CHAT_HISTORY = chattles/chatthistory.txt;
$CHAT_SIZE = 50;
$SESSION_DURATION = "60"; // 分钟
$CHAT_FORMAT = "G-is is"; // php格式
$DEFAULT_LANGUAGE = "english"; // 英语或西班牙语
$DEFAULT_COLOR = "gray"; // 灰色或粉色
$CHAT_MAX_SIZE = 2000000; // 字节
$CHAT_MAX_POOL = 10000000; // 字节
$REFRESH_TIME = 30; // 秒
```

```php
// 注释此变量初始化
// 以允许多个支持
$EXTRA_ROOMS = array(
    "Another Room", "chattles/additional.txt",
    "chattles/chatthistory.txt",
    "Another One", "chattles/additional2.txt",
    "chattles/chatthistory2.txt"
);
```

只需编辑此文件以适应你网站的需求。如果你觉得特别有创意，可能想添加包中默认的表情符号。你也可以在配置文件中定义它们。Francois，这些中的大部分内容都是检查我们客人的眼镜的好时候。我真希望你今天没有选择戴帽子，这让我们我们一些人来说有点让人不安。

对于更复杂、功能更多的聊天，请使用 Lykaa Tajchat's。此方法的唯一之处是，你需要一个 MySQL 服务器来处理用户注册、个人信息和房间创建等。这是一个响应式应用程序，可以打包在一起并处理你想要的所有功能。配合 Firefox 和 Konqueror 使用它，并查看图 3 以 Aajchat 的运行情况。

![](img/6be405694cb4aa0c113e76f02a6a5081_29_0.png)

图 3. 使用 Aajchat 会话非常流畅，感觉不像网页

在进入之前，你需要在 aajchat.org 网站上安装应用程序。你需要聊天程序，而 Showcase 是一个更简单的应用程序，展示了其聊天的一些功能。你可以自行探索。现在，请关注 aajchat.org。

要使用 Aajchat，将包解压到你的 Web 目录。生成的目录包含相关文件。如果你将其连接到你的 Web 站点，将看到第一个配置对话框。有几个设置，例如 MySQL 数据库和管理员，在每个屏幕上继续。不需要花很多时间解释 MySQL，这里是基本步骤。首先创建一个名为 chat 的数据库：

```bash
mysqladmin -u root -p create chat
```

# Polywell 更多选择，更好的服务，巨大的价值

### 塔式系统

#### 4路 Xeon 工作站 Poly2055-2210

- 4路 AMD 处理器
- 64GB 双通道内存
- 2路 SATA RAID 控制器
- 500GB SATA 硬盘
- 2路以太网
- 4路 PCIe 插槽
- 支持 Linux / BSD / Windows

**$1999**

#### SAS 磁盘 Poly2055S-2210

- 4路 AMD 双核心处理器
- 64GB 双通道 DDR3 内存
- RAID 控制器
- NVIDIA GT 710 显卡
- 2TB SATA 硬盘，SAS 控制器
- 2TB SATA 硬盘，SAS 控制器
- PCIe 插槽
- 支持 Linux / BSD / Windows

**$4500**

#### 32GB RAM 塔式服务器-2500-M220

- 2路 AMD 双核心处理器
- 64GB 双通道 DDR3 内存
- NVIDIA GT 710 显卡
- 带有 720W 电源的机槽
- 3TB SATA 硬盘，Raid-5
- 支持 Linux / BSD / Windows

**$3999**

### 桌面级系统

#### 廉价 Poly4085-2800

- 4路 Intel Core 处理器
- 64GB DDR2 内存
- ATI Radeon X3100 显卡
- 500GB SATA 硬盘，板载 Raid-5
- 1路 IDE-RW 硬盘，罗技鼠标
- 1路以太网
