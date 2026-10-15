
3. 点击“Samba”。

4. 点击“Samba Groups”（Samba 组）。

5. 点击“Add a group”（添加组）。

6. 在“Group name”字段中输入 `doctors`。

7. 点击“OK”。

8. 在“Group name”字段中输入 `nurses`。

9. 点击“OK”。

10. 点击“Finish”（完成）。

# 利用旧式 NT 工具允许拨入

对我们有效的执行文件是 `usmgr.exe`（大小为 299280 字节，日期为 1996 年）和 `svrmgr.exe`（大小为 211216 字节，日期为 1996 年）。

现在以 `corp` 域管理员的身份登录 `xpprol.ad.corp.com`。（如果你以其他身份登录，此将不起作用，所以请确保你以 `corp` 域管理员身份登录。）然后从你解压的地方运行 `usmgr.exe`。

你可以选择 `doctor1` 的“User Properties”（用户属性）；然后选择“Dial-in”（拨入），并如图 9.21 所示勾选“Grant dial-in permission to user”（授予用户拨入权限）复框。点击“OK”关闭 Dial-in 信息窗口，然后点击“OK”关闭“User Properties”窗口。

# 使用 Microsoft XP 客户端重试你的 Microsoft PPTP VPN（针对 corp 中的 Samba 用户）

现在我们授予了拨入访问，Windows VPN 将满意来自 Samba PDC 的响应。继续双击你在桌面上为拨号工具创建的图标。现在输入 `doctor1` 的凭据，如图 9.19 所示。还要输入密码。

现在它应该成功连接了，因为该用户已被授予了登录权限！

到此时，我们从 Windows 访问了两个域，这令人印象深刻。然而，如果没有来自 Linux 工作站的 VPN 访问，整个图是不完整的。这就是我们接下来要做的。

图 9.21 Samba 用户需要在 NT 4 用户管理器中设置“Grant dial-in permission to user”。

![](img/1bd448c8019d74f469e5d7e3f033d752_478_0.png)

# 使用 Linux 客户端连接 VPN

我们已经实现了从 Windows 客户端连接到我们的 Windows PPTP 服务器，并使用了 `ad` 域（Active Directory）和 `corp` 域的凭据。这这非常好，而且从跨平台的意义上来说，来自 Linux 托管和 Windows 托管服务器的凭据都能通过。但我们还需要为基于 Linux 的客户端提供访问权限。我们可以使用 Linux PPTP 客户端软件来实现这一点，它的名字非常令人意外，叫做 `pptclient`。

我们将开始安装 `pptclient` 及其依赖的软件。我们将在公司网络之外的一台移动式 Linux 工作站上安装这些软件，并将其命名为 `linuxmobile1`。

然后，我们将使用 `pptclient` 提供的友好 GUI 建立 VPN 连接。我们将使用来自 Active Directory 域或 Linux 托管 `corp` 域的 `ad` 和 `corp` 域账户，这些账户均可接受来自 Linux 客户端的 VPN 连接。

# 为 Linux 安装 PPTP 客户端软件

PPTP 客户端从哪里来呢？Linux PPTP 客户端项目的主页位于 `http://pptclient.sourceforge.net`。该网站上还有一个 Fedora Core 3 的 HOWTO 指南：

`http://pptclient.sourceforge.net/howto-fedora-core-3.shtml`

> 我们将详细展示安装 `pptclient` 所需的，但请务必咨询官方 HOWTO 以获取最新的链接以及安装过程中可能发生的更改。下文出现的 URL 仅用于说明，版本号几乎肯定已经更改。请务必书签您的 HOWTO 文档！

安装 `pptclient` 并不困难，但有几个要求必须先处理。具体来说，在安装 `pptclient` 之前，我们需要：

- 1. 在名为“路边战士”的 PC `linuxmobile1` 上安装 Fedora Linux。这将成为我们基于 Linux 的 VPN 客户端。
- 2. 向内核中添加对 MPPE（微软点对点加密）的支持。MPPE 为我们的 PPTP 连接提供加密。幸运的是，安装这个内核模块并不困难，因为它有良好的软件包支持。
- 3. 如果必要，将 `pppd`（点对点协议守护）升级到 2.4.3 或更高版本。PPTP 是构建在 PPP 之上的，而在本文编写时，Fedora Core 3 中包含的 PPP 实现在与微软的 VPN 服务器协商方面存在困难。
- 4. 安装 `pptclient` 图形界面 `pptconfig` 所需的几个系统库和工具。

我们将开始在 `linuxmobile1` 上安装 Linux。

![](img/1bd448c8019d74f469e5d7e3f033d752_479_0.png)

# 基于 PPTP 的跨平台 VPN

## 在 linmobile1 上安装 Fedora Core 3

`linmobile1` 是我们在本节中使用的客户端，是一台不在公司局域网内部的连接互联网的 PC。由于空间原因，我们无法详尽地介绍 `linmobile1` 的配置，但我们将简要讨论关键区别以及连接到典型家庭宽带的基础知识。

我们建议您按照第 1 章的说明配置 `lincli1.corp`，但例外：

- 1. 您应该启用 DHCP（动态主机配置协议）而不是指定 IP 地址。DHCP 是默认选择，因此这并不困难。这允许您的您的/DSL 调制解调器或家庭路由器为您的 Linux 系统分配 IP 地址。
- 2. 您还应该允许 DHCP 分配 DNS 服务器地址。同样，这是默认选择。

此外，这已经包含在我们在配置 `lincli1.corp.com` 的说明中了，我们会提到您必须选择开发包。否则，您在安装为您的 VPN 连接提供加密所需的内核模块时将遇到麻烦。

一旦您成功在 `linuxmobile1` 上安装了 Fedora Linux 并建立了广域网连接，就可以安装 MPPE 内核模块、升级 `pppd` 以及 `pptclient` 依赖的所有其他前提条件了。

## 在 linmobile1 上为 PPTP 安装必需的内核模块

安装 `pptclient` 将很困难，因为它需要一个自定义内核模块来添加对 MPPE（微软点对点加密）的支持。没有 MPPE，PPTP 不进行加密，而只是封装。

安装内核模块听起来并不容易，但幸运的是，我们可以利用 DKMS（动态内核模块支持）。DKMS 是一个用于轻松管理内核模块的框架，使安装成为一项相对无痛的操作。DKMS 由戴尔的 Linux 支持团队创建并积极维护。

我们如何安装 DKMS，以及从哪里获取利用它的 MPPE 模块呢？这两者都可以从 `poptop` 项目获得。`poptop` 是一个与 `pptclient` 密切相关的 PPTP 服务器。两者都都需要内核中相同的 MPPE 支持，因此 `pptclient` 网站引导访问者访问 `poptop` 网站，以下载 DKMS 本身兼容 Fedora Core 3 的 rpm 以及利用它的 MPPE 模块。可以通过访问此页面找到它：

```
http://poptop.sourceforge.net/doc/
```

点击“Downloads”。DKMS 和 MPPE rpm 出现在可下载文件列表的。

# 第 9 章 • Windows 和 Linux 网络互操作性

![](img/1bd448c8019d74f469e5d7e3f033d752_481_0.png)

`poptop` 是一个基于 Linux 的 PPTP 服务器项目，与 `pptpclient` 密切相关。空间限制我们无法充分讨论 `poptop`。然而，您可以从我们网站 `www.winlinans.com` 的本章章节下载关于该主题的完整报告。这已经包含在我们在配置 `lincli1.corp.com` 的说明中了，我们会提到您必须选择开发包。否则，您在安装为您的 VPN 连接提供加密所需的内核模块时将遇到麻烦。一旦您成功在 `linuxmobile1` 上安装了 Fedora Linux 并建立了广域网连接，就可以安装 MPPE 内核模块、升级 `pppd` 以及 `pptclient` 依赖的所有其他前提条件了。

`poptop` 是一个基于 Linux 的 PPTP 服务器项目，与 `pptpclient` 密切相关。空间限制我们无法充分讨论 `poptop`。然而，您可以从我们网站 `www.winlinans.com` 的本章章节下载关于该主题的完整报告。这已经包含在我们在配置 `lincli1.corp.com` 的说明中了，我们会提到您必须选择开发包。否则，您在安装为您的 VPN 连接提供加密所需的内核模块时将遇到麻烦。

一旦您成功在 `linuxmobile1` 上安装了 Fedora Linux 并建立了广域网连接，就可以安装 MPPE 内核模块、升级 `pppd` 以及 `pptclient` 依赖的所有其他前提条件了。
