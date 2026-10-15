
# 关于 Linux 版 Citrix ICA Client

Citrix 开发了运行在 Windows Terminal Services 之上的软件，增加了许多额外功能。它提供了负载均衡功能、集中化应用部署功能，以及一种名为 ICA（独立计算架构）的超级协议，该协议比微软的 RDP 更高效。例如，ICA 在视频处理方面优于 RDP，并且它支持单个应用程序共享（而不是共享整个桌面）。

如果安装了 Linux 应用 `tsclient`，它必须支持作为 Linux Citrix ICA 客户端的前端。然而，在我们的测试中，这并没有生效。显然，当前版本的 `tsclient` 传递了当前版本 ICA 客户端不支持的命令行参数。

不过，如果你需要，可以直接运行 ICA 客户端。它没有包含在 Fedora Linux 中，但你可以从 www.citrix.com 下载官方 Citrix 客户端的 rpm 包。使用常用的 rpm 安装命令安装该 rpm：

```
rpm -i rpmfilename.rpm
```

然后你可以使用以下命令配置并使用客户端：

```
/usr/lib/ICACClient/wcmngr
```

更多信息请参阅 Citrix 网站。

- 点击“Close”（关闭）返回“软件包管理”界面。
- 点击“Update”（更新）。稍后，会出现“系统准备就绪”对话框。
- 点击“Continue”（继续）开始实际安装过程。
- 按照提示像通常一样插入光盘。
- 安装完成后点击“OK”。
- 点击“Quit”（退出）离开“添加/删除应用程序”工具。

就是这样！我们现在在 Linux 虚拟机上可以使用 `tsclient`（终端服务器客户端）软件了。现在我们准备好作为客户端进行首次连接了。

# 使用 Terminal Server Client 连接 Linux 客户端到 Windows 主机

我们已经拥有通过 Terminal Server Client 前端使用 rdesktop 客户端应用在 Linux 和 Windows 之间建立终端连接所需的一切。让我们开始吧！

在示例中，我们将连接到 `wind1.ad-corp.com`。Terminal Server 软件将该字段称为“Computer”。我们将以 Active Directory 用户 `salesperson1` 的身份使用常用密码登录。由于 Terminal Server Client 和 rdesktop 足够理解 Windows 验证域，我们将指定该用户位于 AD 域。在这种场景下，我们假设用户是管理员，登录到 `windc1.ad.corp` 执行管理任务，而无需物理地坐在它面前。其他用户也可以远程登录，只要他们在服务器上被授予了此权限。

一个你一定会注意到的烦恼：Terminal Server Client 中的“Password:”（密码）字段没太大用。在我们的实验中，无论我们在 Terminal Server Client 密码字段中输入什么，桌面和 vncviewer 都会分别提示我们输入密码，所以你可以省去打字，将其留空。或者，如果你愿意，可以测试一下这在 Fedora Core 3 或 4 的后续更新中是否有所改进。

要从 Linux 客户端到 Windows 主机的 Windows 远程桌面建立 RDP 连接，请遵循以下步骤：

- 1. 选择 ➤ Applications ➤ Terminal Server Client。
- 2. 如图 8.6 所示出现“Terminal Server Client”对话框的“General”选项卡。在“Computer,”字段中输入 `windc1.ad.corp.com`。
- 3. 将“Protocol:”下拉菜单设置为“RDP.”。
- 4. 在“User Name:”字段中输入 `administrator`。
- 5. 将“Password:”字段留空（稍后会提示你输入）。在“Domain:”字段中输入 `AD`。
- 6. 将“Client Hostname:”和“Protocol File:”留空。点击“Connect”。

几刻之后（如果你的连接不是通过局域网，则需要更长时间），你应该看到一个标准的 Windows 登录提示，其中密码字段为空。输入密码并点击“OK”登录。

此后，你将看到 `windc1.ad.corp.com` 上的 salesperson 桌面，如图 8.7 所示，只需点击“Terminal Server Client”窗口即可与远程桌面交互，就像你坐在 `windc1.ad.corp.com` 的控制台前一样。

完成后，像通常一样注销 Windows 桌面。或者，你可以点击右上角的“X”（关闭窗口）按钮断开连接，在这种情况下，桌面仍然可用并重新连接。

![](img/1bd448c8019d74f469e5d7e3f033d752_414_0.png)

你可以使用图 8.4 所示的“Sessions”选项卡配置 Windows 主机对断开会话的响应。

# Windows 2003 终端计算

Windows 和 Linux 用户远程运行 Windows 应用

回想之前的远程计算示例（我们允许 salesperson2 和 salesperson3 连接到我们的 Windows 2003 服务器）。当我们这样做时，Windows 允许到我们的服务器上最多只有两个连接。没错：最多只有两个。这是因为远程计算实际上是为了让管理员能够远程管理位于地下室或服务器机柜中的机器。

图 8.6 使用 Terminal Server Client 应用从 Linux 到 Windows 建立 Windows 远程桌面连接。在我们的实验中，“Password”字段对我们似乎没什么用。

![](img/1bd448c8019d74f469e5d7e3f033d752_414_0.png)

图 8.7 `windc1.ad.corp.com` 上的 salesperson 桌面，如图 8.7 所示，只需点击“Terminal Server Client”窗口即可与远程桌面交互，就像你坐在 `windc1.ad.corp.com` 的控制台前一样。

# Windows 宿主机辅助计算要求

现在，我们已经准备好让我们的 Linux 客户端能够远程协助我们的 Windows 机器。为了实现从 Linux 虚拟机到 Windows 宿机的辅助计算，必须满足以下条件：

- Windows 宿主机上必须安装 VNC 服务软件。Windows 上有多个 VNC 软件发行版。我们使用的软件包称为 TightVNC。请参侧栏“Windows 及其他平台的 VNC 发行版”，对比 Windows 上最常用的两种 VNC 软件包。
- 必须调整 Windows 宿机的防火墙，允许通过 VNC 端口（即 TCP 端口 5900）进行连接。
- Linux 虚拟机上必须安装 VNC 客户端应用程序以及使其使用更方便的 tclient 前端软件。如果你遵循了“Windows 宿机的远程计算”章节，这些软件包应该已经安装了。如果没有遵循，请参考“连接 Linux 虚拟机到 Windows 宿主机（安装桌面和 tclient）”章节。

# Windows 及其他平台的 VNC 发行版

这些软件包中的每一个都包含了 Windows 服务器和 Windows 客户端。在这两种情况下都有 Linux 客户端和服务器，但在 Linux 端，我们将使用 Fedora 自带的完全足够的 VNC 客户端和服务器。

**RealVNC** RealVNC 直接起源于最初的 AT&T 实验室 VNC 软件。RealVNC“免费版”根据 GNU 通用许可证 (GPL) 条款免费提供。免费的个人版可提供完全加密的会话。企业版还支持身份验证，避免了对单独 VNC 密码的需求。有关 RealVNC 的更多信息请访问 www.realvnc.com。

**TightVNC** TightVNC 是 VNC 的另一种开源发行版，专门专注于降低带宽需求。TightVNC 还改进了配置 VNC 客户端和服务器的用户界面。TightVNC 是开源许可协议运作的一个良好范例。原始 VNC 是根据 GPL 发布的，因此 TightVNC 的作者能够在此基础上改进并在相同的免费许可共享他们的工作。TightVNC 处理数据流的能力比其他 VNC 产品更高效，这在拨号连接上可能非常重要。这种优势只有在客户端和服务器都运行 TightVNC 时才会出现。如果运行的版本不同，连接仍然有效，但会回退到原始 VNC 协议的功能，这对于本地局域网和宽带 Internet 连接仍然有效。我们将在本章中使用 TightVNC，因为它的所有功能都是免费提供的。有关 TightVNC 的更多信息请访问 www.tightvnc.com/。然而，如果你非常喜欢 VNC 的功能且预算允许，我们建议查看 RealVNC 企业版。由于它可以使用活动目录 (Active Directory) 进行身份验证，你就不需要记住额外的密码——而且内置加密也是一个非常棒的特性。

# 在 Windows 宿主机上安装和配置 TightVNC
