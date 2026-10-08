

BeEF 未包含在你的 Kali 中，请直接从 Kali 软件仓库下载并安装它。

```bash
kali > apt install beef-xss
```

第一步是启动 BeEF 服务器。你可以通过输入以下命令来启动 BeEF：

```bash
kali > beef-xss
```

服务器启动后，你可以通过在浏览器中访问 `localhost:3000` 连接到它。这会调出如下图所示的屏幕，显示 BeEF 登录界面。默认登录凭据为：

- 用户名: beef
- 密码: beef

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_578_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_579_0.png)

# 身份验证

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_580_0.png)

登录后，你会看到如下图所示的界面。

使用 BeEF 的关键在于让目标点击 BeEF 的 javascript 链接，从而获得对其浏览器的控制权。为了成功攻击浏览器，你可以将 BeEF 钩子（hook）添加到目标很可能访问的网页中，或者通过电子邮件或短信发送该链接，并附上一些诱人的文本，例如：“你一定要看看这个视频！”

一旦目标点击了链接，BeEF 就会挂钩其浏览器，你将获得控制权！在这里，我已在 Kali 中挂钩了我的 Mozilla 浏览器（127.0.0.1）。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_581_0.png)

BeEF 0.4.4.9-alpha | 提交 Bug | 退出登录

# 已挂钩浏览器

- 在线浏览器
  - localhost
  - 127.0.0.1
- 离线浏览器

+ 基本
- 请求者
+ 入门指南 | 日志 | 当前浏览器
+ 详细信息
- 日志
- 命令
- 骑手
- Xss 载荷
- Ipec

+ 类别：浏览器 [6 项]
  - 浏览器名称: Firefox | 初始化
  - 浏览器版本: 24 | 初始化
  - 浏览器 UA 字符串: Mozilla/5.0 (X11; Linux i686; rv:24.0) Gecko/20100722 Firefox/24.0 Iceweasel/24.7.0 | 初始化
  - 浏览器平台: Linux i686 | 初始化
  - 浏览器插件: Gnome Shell 集成-v | 初始化
  - 窗口大小: 宽: 768, 高: 376 | 初始化

+ 类别：浏览器组件 [14 项]
  - Flash: 是 | 初始化
  - VBScript: 否 | 初始化
  - PhoneGap: 否 | 初始化
  - Google Gears: 否 | 初始化
  - Silverlight: 否 | 初始化
  - Web 套接字: 是 | 初始化
  - QuickTime: 否 | 初始化
  - RealPlayer: 否 | 初始化
  - Windows 媒体播放器: 否 | 初始化

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_582_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_583_0.png)

当我点击左侧窗口中标记为“已挂钩浏览器”的浏览器链接时，BeEF 将显示关于该浏览器的关键信息。

现在你可以点击“命令”列，查看该目标系统上可用的所有命令。请注意颜色编码。绿色代表“通行”；该命令很可能有效。红色代表“停止”；该命令**不会**有效。灰色代表“也许”。

在下图中，我们可以看到几个绿色命令，包括“地理位置”。

# **BeEF 0.4.6.1-alpha | 提交 Bug | 退出登录**

| 被黑浏览器 | 命令 | | 当前浏览器 | |
| :--- | :--- | :--- | :--- | :--- |
| 在线浏览器 | 入门指南 | | | |
| 127.0.0.1 | | | | |
| | 详细信息 | 日志 | | 骑手 | Xss 射线 | Ipec | 网络 | WebRTC |
| | | **命令** | | | | | | |
| 127.0.0.1 | | | | | | | | |
| 离线浏览器 | | | | | | | | |
| **模块树** | | **模块结果历史** | | **地理位置** | | | | |
| | 搜索 | | | L. | 日期 | 标签 | | 描述: | 对你的受害者进行地理定位。 |
| 浏览器指纹（概念验证） | | | | 执行命令模块的结果将列在这里。 | | | | Id: | 128 |
| 获取访问过的 URL | | | | | | | | | |
| 间谍之眼 | | | | | | | | | |
| Chrome 扩展程序 (6) | | | | | | | | | |
| 在选项卡上执行 | | | | | | | | | |
| 获取所有 Cookie | | | | | | | | | |
| 抓取谷歌联系人 | | | | | | | | | |
| 注入 BeEF | | | | | | | | | |
| 屏幕截图 | | | | | | | | | |
| 发送语音短信 | | | | | | | | | |
| 调试 (9) | | | | | | | | | |

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_585_0.png)

在下方，我们可以看到一些命令是红色的，这意味着它们在此浏览器上无法使用。

摄像头命令在此浏览器上显示为绿色。该命令会弹出一个对话框，询问用户是否启用摄像头。如果他们点击“是”，其摄像头将被启用并开始拍摄快照。你可以替换此消息并在对话框中自定义一条新消息（“立即更新您的 Adobe Flash！”），这将很可能诱导用户点击。

BeEF 是欺骗目标并控制其浏览器的绝佳工具。

# ## 短信欺骗

在过去十年中，短信通讯增长得如此迅猛，以至于有些人很少再打电话了。这种通常被称为“发短信”的技术，非常容易被欺骗。

如果你需要某人在手机上打开一个链接或采取某些行动，这可能是一种极佳的方式。几年前，有许多短信欺骗服务，但其中许多已逐渐被遗忘。在这场混乱中，Spoofbox (www.spoofbox.com) 依然保持强劲。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_586_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_587_0.png)

这是一项宣传与实际相符且相对便宜的服务（并非免费，但他们接受比特币支付）。我曾在社会工程学实战中使用过此工具，我可以对它发誓。它有效！

你只需要开设一个账户并存入一些资金。然后输入短信发送的目标号码、希望显示的发件号码，以及要发送给目标的信息。

你们中有些《疑犯追踪》（Mr. Robot）的粉丝会记得，f/society 小组通过向护送 Elliot 离开的那位女士发送一条短信，使他摆脱了石山（Stone Mountain）的困境。那条短信看似来自她的丈夫，称他已被送入医院。该服务完全可以做到这一点！

除了短信欺骗，SpoofBox 还提供以下服务：

1. 电子邮件欺骗
2. 电话欺骗
3. 伪造 WhatsApp
4. 伪造 iMessage

请自行判断风险使用这些服务，因为我未尝试过这些其他服务，无法保证其有效性或安全性。

```bash
root@kali:~# apt install wifiphisher
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  hostapd python-pbkdf2 python-pyrcl python-roguehostapd
Suggested packages:
  python-pyrcl-doc
The following NEW packages will be installed:
  hostapd python-pbkdf2 kali kali-rolling python-roguehostapd wifiphisher
0 upgraded, 5 newly installed, 0 to remove and 970 not upgraded.
Need to get 5,391 kB of archives.
After this operation, 13.0 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://kali.download/kali kali-rolling/main amd64 hostapd amd64 2:2.9-3 [812 kB]
Get:2 http://kali.download/kali kali-rolling/main amd64 python-pbkdf2 all 1.3+git20110613.git2a0afb15-d50-3 [7,398 B]
Get:3 http://kali.download/kali kali-rolling/main amd64 python-pyrcl all 0.1.6-0kali1 [308 kB]
Get:4 http://kali.download/kali kali-rolling/main amd64 python-roguehostapd amd64 1.2.3-0kali2 [402 kB]
Get:5 http://kali.download/kali kali-rolling/main amd64 wifiphisher all 1.4+git20180525-0kali2 [3,062 kB]
Fetched 5,391 kB in 2s (2,387 kB/s)
Selecting previously unselected package hostapd.
(Reading database ... 375058 files and directories currently installed.)
Preparing to unpack .../hostapd_2%3a2.9-3_amd64.deb ...
Unpacking hostapd (2:2.9-3) ...
Selecting previously unselected package python-pbkdf2.
Preparing to unpack .../python-pbkdf2_1.3+git20110613.git2a0afb15-d50-3_all.deb ...
```

# ## Wi-Fi 钓鱼

当许多黑客致力于破解 WPA2 哈希值时，有些人发现直接从目标那里社会工程学获取密码更为有效。wifiphisher 就是为此而设计的。该工具旨在：

1. 创建目标 AP（接入点）的克隆；
2. 将用户从其真实的 AP 去认证；
3. 将他们关联到虚假的 AP；
4. 向用户展示一个逼真的固件更新屏幕，并要求他们提供密码以继续。

你和我可能不会如此轻易地交出密码，但根据我的经验，大多数其他人会。

Wifiphisher 未内置于 Kali 中，因此你需要从 Kali 软件仓库下载并安装它。

```bash
kali > apt install wifiphisher
```

一旦 wifiphisher 完成下载和安装，让我们看看它的帮助屏幕。

```bash
kali > wifiphisher -help
```

