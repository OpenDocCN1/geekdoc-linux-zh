

## Remote X

到目前为止我们所讨论的都是命令行远程连接，尚未提及如何启动图形用户界面。在 Linux 中实现这一点有两种方法：X Display Manager Control Protocol（XDMCP）和 Virtual Network Computing（VNC）。前者专用于 X Windows，并与整个图形系统紧密集成，但安全性也很差。VNC 更现代、普及度很高，但在某些实现中也不安全。两者在 Ubuntu 上都在使用，因此我们将在此介绍这两种方法。

## XDMCP

除非你将 Ubuntu 配置为自动登录特定用户，否则你一定熟悉启动时出现的用户登录界面。你看到的是 Gnome Display Manager（GDM），它运行你的 X 会话、检查密码等。你所做的是登录到本地机器，因为这是默认配置。

然而，GDM 也配备了允许其他网络用户通过 XDMCP 协议连接到你的机器的功能。使用 XDMCP 的原因有很多，其中最流行的是许多现代机器体积庞大且噪音很大。它们拥有大容量硬盘、带巨大风扇的 CPU 以及强大的显卡，因此不适合放在安静的客厅里。另一方面，瘦客户端（CPU 能力很弱且没有自己硬盘的机器）是静音的，但功率不足以运行 Gnome 或 OpenOffice.org。

解决方案是将你的强大机器锁在某个壁橱里并连接 Wi-Fi，而将安静的瘦客户端放在客厅里也接入 Wi-Fi。瘦客户端连接到强大机器并从那里运行所有程序，所有图形都通过网络中继。

在 Ubuntu 上，这很容易做到。首先从服务器端开始，选择 System > Administration > Login Window；然后选择 Remote 选项卡并将 Style 选项更改为 "Plain with face browser"。在客户端，打开相同的对话框并确保从 Local 选项卡中勾选 Show Actions Menu 复选框。

现在，从客户端注销桌面，返回 Ubuntu 登录屏幕。当它提示你输入用户名时，寻找 Options 按钮并选择 Remote Login with XDMCP。会出现一个新对话框，列出愿意接受你连接的本地 XDMCP 服务器——你应该能在其中看到你的服务器。选择它并点击 Connect；你将看到来自该服务器的登录屏幕，邀请你登录。当然，你需要在服务器上拥有有效账户才能登录；不过，这就是你唯一需要的。

正如你所见，由于 XDMCP 与 X Windows 系统的核心紧密相关，因此设置起来很容易。然而，正如你使用时会发现的，XDMCP 速度非常慢——即使在千兆以太网网络上，它也会占用相当大的带宽。它也不安全。任何人只需做很少的工作就能监控你的操作。由于这两个缺陷，XDMCP 绝不应在不受信任的网络之外使用。

## VNC

XDMCP 的下一步是 VNC，它由英国 AT&T 的剑桥研究实验室开发。VNC 在 Linux 世界中广泛使用，在 Windows 世界中也使用到一定程度。其主要优势在于其广泛性：几乎所有 Linux 发行版都捆绑了 VNC，并且可用于各种平台的客户端。

要设置 VNC，请启动 Synaptic 并安装 vnc-common 和 xvncviewer 包。完成之后，只需告诉 Ubuntu 谁可以连接到你的会话即可。这是通过 Preferences 菜单上的 Remote Desktop 选项完成的。默认情况下，你的桌面未共享，因此请勾选 Allow Other Users to View Your Desktop 以共享它。你还应勾选 Allow Other Users to Control Your Desktop；否则，人们只能看到你在做什么而无法与桌面交互——这并无多大帮助。

该屏幕上的第二组选项很重要。如果你使用它作为远程连接自己桌面的方式，请取消选择 Ask You for Confirmation。如果不这样做，当你尝试从远程位置连接时，Ubuntu 会在本地机器上弹出消息框询问 Should this person be allowed to connect? 因为你不在那里点击 Yes，连接将失败。如果你想让其他人远程连接到你的系统，请保持此框启用，以便你知道何时有人连接。不管是谁连接，你都应始终输入密码。VNC 与 XDMCP 一样，不应被视为在互联网上或甚至在不受信任的网络上是安全的。

## Reference

- http://www.openssh.com—OpenSSH 实现 SSH 的主页，Ubuntu 使用的就是它。它由与 OpenBSD 相同的团队运行，OpenBSD 是一个安全的基于 BSD 的操作系统。
- http://www.realvnc.com—由 AT&T 剑桥研究实验室制作 VNC 的团队的主页。此后他们成立了 RealVNC Ltd.，一家致力于开发和支持 VNC 的公司。
- http://www.tightvnc.com—在这里你可以找到 VNC 的替代品 TightVNC，它在原版 VNC 发布版之上有多项关键改进。最重要的功能是 TightVNC 可以使用 SSH 进行加密，从而保证安全性。
- http://www.nomachine.com/—VNC 的另一种替代品正在开发中，名为 NX。免费实现 FreeNX 在撰写本文时正处于积极开发中，但承诺比 VNC 工作得快得多。

一本在 SSH 书籍中脱颖而出的书籍因封面上的图片而被称为 "The Snail Book"。它涵盖了整个 SSH 套件，名为 SSH: The Secure Shell（O'Reilly），ISBN：0-596-00011-1。

