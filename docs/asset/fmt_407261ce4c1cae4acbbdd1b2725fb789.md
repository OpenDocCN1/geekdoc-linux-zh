
例如，假设你的红帽 Linux 7.1 安装文件被挂载在 HTTP 服务器的 `/pub/mirrors/redhat/i386/RedHat` 下。同时假设 HTTP 服务器位于 `www.redhat.com`。在这种情况下，将 `www.redhat.com` 输入为网站名称（Web Site Name），并将 `/pub/mirrors/redhat/i386` 输入为红帽目录（Red Hat Directory）。

其余的安装程序应按照从本地 CD-ROM 驱动器安装时相同的通用步骤进行。

### 展望

现在你已经安装了联网的 Linux 系统，你将查看 Linux 以太网配置的细节。这些信息将允许你将现有的非网络 Linux 系统安装到以太网局域网或根据需要重新配置现有的网络配置。

一旦学习了这些细节，你将在书的大部分时间里研究 Linux 在小型局域网中可以扮演的角色，包括：

- 担任廉价的路由器或防火墙
- 作为内网 Web 服务器
- 为你的网络处理电子邮件服务

# 第二二十八章

# 为以太网配置红帽 Linux 7.1

- 准备并配置网络
- 测试网络
- 手动网络配置
- 在 Linux/Unix 网络上共享文件
- 基础网络安全

## 第 28 章 • 为以太网网络配置红帽 Linux 7.1

在第 27 章“为 SOHO 安装红帽 Linux 7.1”中，你学习了如何在计算机上安装 Linux 并在过程中将其连接到 TCP/IP 以太网网络。你还学习了在 Linux 安装期间配置网卡的基本步骤。

在本章中，你将学习如何配置已安装的 Linux 系统以连接到 Linux 网络。这些步骤包括为网络准备 PC、配置网络以及测试，本章涵盖了整个过程。

以太网（Ethernet），正式名称为 IEEE 标准 802.2 和 802.3，是众多网络技术中最流行的一种。你可以设置 Linux 与其他网络技术工作，包括令牌环（Token Ring）、ARCNet、快速以太网（Fast Ethernet）、千兆以太网（Gigabit Ethernet）和异步传输模式（ATM）。虽然这些技术不同，但在使用命令行界面时，安装技术非常相似。更多信息，特别是关于各种以太网选项以及 ATM，可以在 Ethernet-HOWTO 的第二部分找到，该文档可以在 `http://www.linuxuxdoc.org/Ethernet-HOWTO-2.html` 在访问。

本章基于与 Linux 2.2.x 内核相关的传统网络命令，这些命令在红帽 Linux 7.1 中仍在使用。有一些与 Linux 2.4 内核相关的一些新网络命令；关于此的更多信息可以在 Linux 2.4 Networking HOWTO 中找到，目前可在 `http://www.ds9a.nl/2.4Networking/HOWTO/cv/2.routing/output/2.4networking.html` 获取。

## 准备并配置网络

正如你在上一章中看到的，为了让你的网络工作，需要两个主要步骤：

- 安装并设置网卡
- 设置你的 TCP/IP 参数

本章将介绍在 Linux 安装后如何配置这些要素。此过程可用于将新 PC 安装到网络，或用于更改当前 PC 的配置。

### 安装和设置网卡

安装和设置网卡高度依赖于你使用的网卡类型。在某些情况下，你可能需要重启计算机。如果 Linux 检测到你的网卡，你会看到类似的内容：

```
eth0 Link encap:Ethernet
    inet 192.168.0.1 mask:255.255.255.0
    UP BROADCAST MULTICAST MTU:1500 Metric:1
    RX packets:0 errors:0 drop:0 coll:0
    TX packets:0 errors:0 drop:0 coll:0
    collisions:0 txqueuel:1000
```

如果 Linux 未能自动检测网卡，你必须手动指示 Linux 支持你的硬件。首先启动 Linuxconf。你可以通过在 xterm 窗口执行以下命令启动 Linuxconf：

```
$ linuxconf-auth
```

如果你不是 root 用户，红帽 Linux 7.1 在启动 Linuxconf 前会提示输入 root 密码。如果 Linux 不识别此命令，可能需要按照第 15 章所示的说明安装 Linuxconf。

一旦 Linuxconf 启动，导航到 `Networking > Client Tasks > Host Name and IP Network Devices` 进入图 28.1 所示的屏幕。

#### 图 28.1：Linuxconf 网络配置

![](img/968f44a58bee05b3a080631d18e977c9_667_0.png)

此版本 Linuxconf 中的 Host Name and IP 部分包含六个选项卡。Host Name 选项卡显示与计算机关联的主机。其他五个选项卡允许你配置所需的网卡或适配器。

一个常见问题是第二个网卡的检测。当你设置计算机连接到两个不同的网络时，你需要两个网卡。点击 `Adaptor 1` 选项卡。如果 Linux 识别了你的第一个网卡，相关的配置数据通常会填充在此选项卡中。要配置第二个网卡，点击 `Adaptor 2` 选项卡。假设它是空的，如图 28.2 所示。

#### 图 28.2:

添加新网卡

![](img/968f44a58bee05b3a080631d18e977c9_668_0.png)

如你所见，每个网卡都有许多相关设置。某些设置对网卡配置至关重要，而另一些则：

- `Enabled`：如果你想激活您的网卡，请选择此选项。
- `Config Mode`：如果您的网络没有 DHCP 服务器，请选择 Manual（手动）。如果本地网络上有 DHCP 服务器，请选择 DHCP 以允许配置您的网卡。如果相邻网络上有 DHCP 服务器，请选择 Bootp 以允许其配置您的网卡。
- `Primary Name + Domain`：输入您的计算机名称及其域名。例如，如果您的计算机名为 `linux71.mommabears.com` 网络，请输入 `linux71.mommabears.com`。或者，你可以留空此选项，并在 `/etc/hosts` 文件中进行设置。
- `Aliases`：如果你为计算机设置其他名称，请在此处输入。如果需要多个别名，只需用空格将它们分隔。
- `IP Address`：如第 21 章“理解 Linux 网络”所述，IP 地址是四个 0 到 255 之间的数字，用点隔开。如果您的配置模式为 Manual，请在此处输入此网卡的 IP 地址。

填好适当的文本框后，下一步是进行测试。点击标签页底部的 `Accept`，然后选择 Linuxconf 窗口左角的 `File > Act/Changes`。当 `Status Of The System` 对话框出现时（如图 28.3 所示），Linuxconf 正在告诉你是为了实施你的更改需要做什么。在这种情况下，它建议你重启网络守护进程并重新读取网络配置文件。点击 `Do It` 以使其生效。

#### 图 28.3:

Linuxconf 激活配置更改

![](img/968f44a58bee05b3a080631d18e977c9_670_0.png)

重新运行之前描述的 `/sbin/ifconfig` 命令。如果 Linux 现在识别了您的网卡，你就可以带着维护网络的视角来阅读本章了。

### 检查模块是否加载

如果你无法通过 Linuxconf 设置您的网卡，下一步是验证配置，这并不是一项容易的任务。在下一节尝试让网络工作之前之前，没有快速的方法可以查看以太网网卡是否配置正确。但你可以使用 `insmod` 命令安装可加载内核模块，来手动检查模块是否会加载。

要执行此操作，请进入控制台命令行或以 root 用户身份打开 xterm 窗口。首先，你需要将当前目录更改到以下：

```bash
$ cd /lib/modules/2.4.2-2/kernel/drivers/net/
```

此命令假设你已经安装了随书提供的 Red Linux 7.1 发行版且没有升级内核。在这种情况下，内核版本为 `2.4.2-2`，这在目录路径中体现。

一旦进入正确的目录，使用 `insmod` 命令加载所需的模块（在本例中，针对 Novell 系列网卡）：

```bash
$ insmod ne.o
```

如果 Linux 不识别你所需的模块，请检查该目录（或其子目录）中的可用模块列表。如果你看到了正确的模块，请检查拼写并重试。注意模块文件名带有扩展名。

如果配置成功，你的网卡将加载，驱动程序将生成一系列消息。这些消息可能是复杂的，如 `3c59x` 的示例所示：
