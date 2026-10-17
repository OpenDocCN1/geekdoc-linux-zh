
http://google-gruyere.appspot.com/326352883334/

<script>alert(1);</script>

</script>

```

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_246_0.png)

示例显示我们的目标 Web 应用程序服务器弹出了窗口，证明该网站容易受到攻击。我们可以使用 ZAP 重放攻击、尝试其他攻击，或测试类似的 XSS 方法。

我们建议尝试你发现的错误，看看你是否可以操纵它们为你的渗透测试练习生成敏感输出。Gruyere 项目是测试使用 ZAP 等工具发现其他漏洞技能的绝佳方法。

为了防御远程攻击，ZAP 对于测试 XSS 攻击等 Web 漏洞非常有效。一些人认为，如果浏览器声称其具有 XSS 防御，用户在浏览网站时就不需要担心 XSS。该概念背后的事实是，浏览器保护可能是完美的，因为浏览器并不知道 Web 应用程序后的代码有多安全。聪明的黑客可能会绕过保护，例如利用 XSS 漏洞并针对访问网站的主机发布脚本。保护你的服务器和访问应用程序的客户端的最佳实践是使用像 ZAP 工具识别并修复漏洞。

### SET 密码收割

我们在第 4 章中检查了社会工程工具包 `SET` 的基础。我们将回顾 `SET` 并查看密码收集和获取特权信息的高级概念。

作为复习，我们将通过进入 `Exploitation Tools` | `Social Engineering Tools` | `se-toolkit` 来启动 `SET`。

第一次使用，请确保 `SET` 已更新。更新 `SET` 以及验证 `GIT` 是否安装的步骤可以在第 4 章找到。

> 当 `SET` 克隆一个网站时，它会运行一个 Web 服务器。目标对象能够连接到你的 Web 服务器非常重要。这意味着任何基于 Internet 的攻击都需要利用 IP 地址（通过 NAT 或直接在 Kali Linux 上），并开放防火墙规则以允许从远程访问 Kali。

一旦你处理了任何 IP 配置，就可以启动 `SET` 了：

```
root@kali:/usr/share# cp backup.set/config/set_config/set/config

root@kali:/usr/share# se-toolkit

重要通知！由于 Kali 的目录结构，社会工程工具包进行了一些重大更改。

所有 SET 动态信息现在将保存在 ~/.set 中，而不是 src/project_Jun。

[!] 请注意以后你应该使用 se-toolkit。

[!] 通过 'se-toolkit' 启动即将失效...

[!] 如果不在 Kali 上，运行 python setup.py install 然后你可以在任何地方使用 se-toolkit。

按 (return) 键继续 SET。
```

我们将使用 `SET` 来收割密码。`SET` 有能力克隆你想要的网站。在示例中，我们实际上选择了流行的网站之一进行克隆。

# 第 6 章

```
root@kali:~ ~

File Edit Search Terminal

此软件，即使已告知可能导致损坏
```

上述许可协议取自 BSD 许可，也适用于社会工程工具包。

你可以对其进行修改、使用、更改、市场营销等等任何操作，只要你给予作者应有的荣誉。此外，通过使用此软件，如果你在酒吧里看到 SET，你应该拥抱他并请他喝瓶啤酒。必须持续至少 5 秒。然而但他保留拒绝拥抱的权利。

社会工程工具包并不邪恶。如果你将其用于任何你所评估的公司未授权的操作，你即违反了该工具集的服务条款和许可。通过点击（仅限一次），你同意服务条款，并承诺仅出于合法目的使用此工具。

你同意服务条款吗 [y/n]:

## Web 攻击

对于我们的示例，我们将选择 Web 模板。`SET` 将询问它应该在哪个 IP 地址上监听。这将是 Kali Linux 上接口的 IP 地址。例外情况是在防火墙上使用 NAT。在这种情况下，你需要使用 NAT 或公网地址，而不是 Kali Linux 上的 IP 地址，以便目标能够访问该系统。接下来的示例将使用本地回环地址 `127.0.0.1`。

接下来，`SET` 将要求选择一个模板。对于此示例，我们将选择 Facebook。

接下来的示例显示 Web 浏览器访问 `127.0.0.1` 并显示一个虚假的 Facebook 页面。如果模板页面看起来不恰对，你可能想要使用不同的模板或清除默认模板。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_249_0.png)

我们注意到地址栏显示为 `127.0.0.1`。通常情况下，你需要使用其他攻击向量来欺骗用户访问你的网站。有许多方法可以实现这一点，例如发送链接或虚假页面：

> Facebook <wwt.secmob@gmail.com>
致: A Lakhani <Aamir.Lakhani@wwt.com>
Facebook
2013年5月29日 下午5:49
已发送邮件 1

亲爱的 Facebook：
为了确保您的在线体验更安全、更愉快，Facebook 将实施一套新的登录系统，该系统将影响所有 Facebook 用户。这些更改将提供新功能并提高账户安全性。
在使用新的登录系统之前，您被要求更新您的账户。
请点击下方链接现在在线更新您的账户
www.facebook.com
如果您有任何问题，请参考《新用户指南》。

谢谢，
Facebook 团队
Facebook 永远不会在电子邮件或 Facebook 信息中向您索要密码。了解更多关于保持账户安全的信息。

## 第6 章

当我们在虚假的 Facebook 中输入用户名时，`SET` 会捕获流量。`SET` 还会将用户重定向到真实网站。希望受害者认为他们在被重定向到真实 Facebook 时输入了密码，并继续使用 Facebook，而不知道 `SET` 捕获了他们的登录凭据：

```
root@kali:~ -

File Edit View Search Terminal Help

[*] Cloning the website: http://www.facebook.com

[*] This could take a little bit...

使用这种攻击的最好方法是如果你的用户名和密码字段可用。无论如何，这都会捕获网站上所有的 POST 请求。

[*] Social-Engineer Attack

[*] Credential Harvester is running on port 80

[*] 信息将在到达时向您显示：

127.0.0.1 - [11/Jun/2013 22:18:29] SET / HTTP/1.1 280 -

127.0.0.1 - [11/Jun/2013 22:18:29] SET / HTTP/1.1 280 -

[*] WE GOT A HIT! Printing the output:

PARAM: charset_text='', *,\de, *,\de

PARAM: location=facebook.com

POSSIBLE USERNAME FIELD FOUND: non-login.com

POSSIBLE PASSWORD FIELD FOUND: kali

POSSIBLE PASSWORD FIELD FOUND: kali-linux-LINUX

PARAM: charset_text='', *,\de, *,\de

*) WHEN YOU'RE FINISHED, CONTROL-C TO GENERATE A REPORT.
```

上一个示例显示 `SET` 捕获了我们的用户名：DrChaos，以及我们的密码 ILoveKali。

当你完成此项练习后，请按 Ctrl+C 退出 `SET` 工具并生成一个 HTML 报告。`SET` 会创建一个可以用于你的渗透测试报告的专业报告：

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_250_0.png)

## Web 攻击

### Fimap

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_251_0.png)

`Fimap` 是一个 Python 工具，可以针对 Web 应用程序发现、准备、审计、利用并自动搜索本地和远程文件包含（LFI 和 RFI）漏洞。

可以在 `Web Applications` | `Web Vulnerability Scanners` | `Fimap` 下找到 `Fimap`。当你打开 `Fimap` 时，会打开一个终端窗口。`Fimap` 有几个插件选项，你可以通过以下命令下载它们：

```
fimap --install-plugins
```

所有可用的插件将以列表形式显示，你可以选择其中一个或退出。在以下示例中，有两个可用插件可以安装。你必须运行安装命令单独安装每个插件：

```
root@kali:~# fimap --install-plugins

fimap v.09 (For the Swarm)

:: Automatic LFI/RFI scanner and exploiter
```
