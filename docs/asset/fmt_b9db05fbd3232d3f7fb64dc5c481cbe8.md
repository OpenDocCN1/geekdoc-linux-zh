
```bash
$ git clone git://github.com/mochi/mochiweb.git
cd mochiweb
Cloning into 'mochiweb'...
remote: Counting objects: 2632, done.
remote: Total 2632 (delta 0), reused 0 (delta 0), pack-reused 2632
Receiving objects: 100% (2632/2632), 1.28 MiB | 603.00 KiB/s, done.
Resolving deltas: 100% (1681/1681), done.
```

![](img/fb76008333fb7aef815b136f9f1afe5f_53_0.png)

**图注** 处理所有 `/URL` 请求的 `root_handler.erl` 模块的 Erlang 代码

现在您可以自由使用 MochiWeb！

### 提供 'Hello World!' 页面

本节将展示如何编程 MochiWeb 以提供 'Hello World!' 页面。这个简单的例子将帮助您更好地理解 MochiWeb 的工作原理。您可以通过在 `mochiweb` 目录内部执行以下命令创建一个名为 `hwmochi` 的新项目：

```bash
$ make app PROJECT=hwmochi
```

然后，您需要通过执行 `cd ./hwmochi` 命令进入位于 `mochiweb` 目录外部的 `hwmochi` 目录。

![](img/fb76008333fb7aef815b136f9f1afe5f_53_1.png)

**图注** epoch Web 应用程序的三种可能输出——每一种代表开发人员应定义和实现的不同的 Cowboy 路由

## 关于 WebSockets

WebSockets 是 HTML5 标准的一部分，与 Erlang 没有任何关系。然而，WebSockets 提供了一种双向异步套接字，允许浏览器与外部世界（包括用 Erlang 编写的程序！）进行通信。所谓异步，是指 WebSockets 发送数据时无需等待响应。由于 Erlang 在设计上也是异步的，因此 WebSockets 是与 Erlang 程序通信的完美方式。

在开发使用 WebSockets 的 Erlang 应用程序时，你需要三个组件才能使一切正常运行：一个运行部分代码的 Web 浏览器、一个执行一些 Erlang 代码的 Erlang 应用程序（`A`），以及另一个能够与 WebSockets 协议通信的 Erlang 应用程序（`B`）。Erlang 应用程序 `A` 包含 Web 应用的逻辑，以及执行数据库通信等任务所需的 Erlang 代码。Erlang 应用程序 `B` 负责将消息从 Erlang 应用程序 `A` 传输到 WebSockets，反之亦然。

你可以在 `https://tools.ietf.org/html/rfc6455` 找到 WebSockets 协议的 RFC 文档。

为我们的应用程序添加一个名为 `/hello_mochi` 的新网页，这需要编辑我们之前创建的 `/.src/hwmochi_web.erl` 文件：

`hwmochi_web.erl` 中最有趣的代码是处理新支持的 URL 行为的代码：

```erlang
["hello_mochi" ] ->
    Req:respond({200, [{"Content-Type", "text/html"}],
        "<h2 style='color:#057;'>Hello MochiWeb!</h2>\n"});
```

图 7 展示了 `/.src/hwmochi_web.erl` 文件的完整 Erlang 代码——其中大部分是自动生成的！图 8 展示了上述 Erlang 模块提供页面时，Web 浏览器在屏幕上显示的内容。请注意，MochiWeb 会自动生成一个 `/hello_world` URL，如果你愿意可以删除它。

你可以通过编辑 `/.src/hwmochi_sup.erl` 文件来更改 HTTP 服务器监听的端口号。下一条 `grep` 命令的输出显示了包含相关代码的文件和行：

```bash
$ grep -n 8080 ./src/*
…/src/hwmochi_sup.erl:44:  web = web_specs(hwmochi_web, 8080),
```

通过查看 MochiWeb 项目和 Cowboy 项目的结构你就会发现，它们非常相似，这使得开发者的生活简单了许多。你可以在 `https://github.com/mochi/mochiweb` 找到更多关于 MochiWeb 的信息，但只有实践才能让你更擅长使用 MochiWeb！

那么，仅为了创建 Web 应用程序而学习 Erlang 值得吗？答案毫无疑问是值得的！

![](img/fb76008333fb7aef815b136f9f1afe5f_54_0.png)

`useMochi.erl` 的 Erlang 代码，在此处你告诉 MochiWeb 它将支持哪些 URL

![](img/fb76008333fb7aef815b136f9f1afe5f_54_1.png)

在此目录下运行 `make` 将编译这个示例项目，并允许你通过执行 `./start-dev.sh` 脚本来启动它。目前，你拥有一个监听 `8080` 端口的 Web 服务器，你可以通过在 Linux 终端中执行 `wget http://127.0.0.1:8080` 来测试它。这将创建一个 `index.html` 文件，包含以下 HTML 代码：

```html
<!html>
<head>
<title>It Worked!</title>
</head>
<body>
    hwmochi running.
</body>
</html>
```

上述代码可以在静态 HTML 页面 `/priv/www/index.html` 中找到。因此，我们现在应该让事情变得稍微有趣一点。我们稍后将做的是添加

`useMochi.erl` 的输出，它使用 MochiWeb Erlang 模块实现了一个简单的 HTTP 服务器

## LINUX 环境下的 AMAZON WEB SERVICES

`Peter O'Brien` 深入探究了驱动 Amazon 服务功能的强大基础设施，这些基础设施通过 Amazon Web Services (`AWS`) 在 Linux 平台上开放给公众，以满足个人及企业的各种托管需求。

如果你想在云端托管服务——无论是网站、数据库、文件还是任何通过网络访问的内容——都有大量选项可供选择。在决定使用哪项服务时，你会综合考虑诸多因素，如价格、性能、可靠性和声誉。就声誉而言，很少有服务比 Amazon Web Services (`AWS`) 更受人尊重，且这并非毫无道理。Amazon 的网站最近一次宕机是什么时候？如果它能承载其接收到的海量流量并保持规模运行，那么它很可能也能满足你的需求。传统上，高昂的成本是许多人使用 `AWS` 的门槛，但近期的变化使得试用该服务变得比以往任何时候都更容易。

Amazon Web Services 已经存在多年，尽管它经历过——并仍在经历——持续的变更和改进。该公司最初于 2002 年推出，愿景是开放 Amazon 的技术和产品数据，使第三方能够构建自己的应用程序。这一概念在 2003 年得到细化，提出了构建零售运营所用基础设施的提案，将其作为“基础设施即服务”产品提供，这有可能为公司提供额外的收入来源。该想法得到了验证，自 2006 年 3 月全面推出以来，`AWS` 呈现巨大增长，预计 2017 年为 Amazon 带来约 130 亿美元的净利润。

除了 `AWS` 提供的庞大且互操作性强的服务范围外，其关键优势之一在于它位于许多不同的地理位置。该服务在北美提供六个区域，在南美、欧洲（包括伦敦）以及亚太地区各提供六个区域。对于希望向全球用户提供服务的公司而言，这一点极具价值，同时借助在地理上偏远位置托管服务和数据的能力，也提供了弹性。此外，每个区域都有多个“可用区”，由一个或多个独立的数据中心组成，每个数据中心都有独立的电源和连接。这些可用区被刻意彼此隔离，以防止故障在区域间扩散。`AWS` 还在全球提供 54 个“边缘”网络接入点，可用于将内容托管在更接近客户的位置。

`AWS` 服务通常按需使用，并按使用量收费（尽管可以通过预留资源获得折扣）。新用户可享受免费套餐选项，该选项为 `AWS` 的许多服务提供免费的基础级别服务。目前，该公司在多种技术领域提供超过 70 种服务，并通过功能强大的 `RESTful` `API` 进行访问，访问权限由 `IAM`（身份与访问管理）控制，`IAM` 位于 `AWS` 的核心，允许对访问进行极其精细的控制。

> “若要预先了解您正在构建的系统成本，`AWS` 提供了一个简单的成本计算器”

![](img/fb76008333fb7aef815b136f9f1afe5f_56_0.png)

`AWS` 控制台提供了访问大量 `AWS` 服务的入口，同时也包括计费和支持服务。
