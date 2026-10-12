
要关闭你的连接，请在你的面板中右击 `kppp` 指示器，然后点击断开连接菜单项。

## 注意

`kppp` 还附带了一个 PPP 日志实用工具（`KP P P - L o g v i e w`）和另一个独立的负载查看器（`KPPP L o a d`）。要启动这两个工具中的任何一个，请点击 K 桌面面板的应用启动器按钮，然后选择 Internet。

## 查看调制解调器指示灯！

如果你不使用 `kppp`，但喜欢 `kppp` 的调制解调器指示灯功能，可以使用 John Ellis 和 Martin Baulig 的 Modem Lights Applet 1.2.1。你可以在 GNOME 面板的小工具、网络菜单中找到该小工具，作为 Modem Lights 菜单项。你还可以通过其名称 `modemlights_applet` 来启动该小工具。

## 使用 `wvdial` 命令设置 PPP

`wvdial` 命令是你在 Red Hat Linux 发行版中找到的又一个连接工具。这个命令行工具使用单个名为 `wvdial.conf` 的配置文件，该文件位于 `~/.etc` 目录下。你可以使用 `wvdialconf` 命令快速创建一个基础配置文件，如下所示：

```
   1 # wvdialconf /etc/wvdial.conf
   2 Scanning your serial ports for a modem.
   3 tty S1 < * > : ATQ0 V1 E1 Z -- OK
   4 tty S1 < * > : ATQ0 V1 E1 Z -- OK
   5 tty S1 < * > : ATQ0 V1 E1 S0-- OK
   6 tty S1 < * > : ATQ0 V1 E1 S0=0 &C1 -- OK
   7 tty S1 < * > : ATQ0 V1 E1 S0=0 &C1 &D2 -- OK
   8 tty S1 < * > : ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 -- OK
   9 tty S1 < * > : ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 + FCLASS=0 -- OK
  10 ...
```

该命令将扫描你的计算机串口，测试找到的任何调制解调器，然后创建你的 `wvdial.conf` 文件。之后你应该用你最喜欢的文本编辑器打开该文件并编辑 Dialer Defaults 部分。默认配置看起来像这样：

```
[Dialer Defaults]
Modem = /dev/ttyS1
Baud = 115200
Init1 = ATZ
Init2 = ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0
; Phone = <Target Phone Number>
; Username = <Your Login Name>
; Password = <Your Password>
```

删除最后三行开头的分号（`;`），然后用你的 ISP 电话号码替换括号中的信息，以及你的用户名和密码。更改后的样子可能如下：

```
[Dialer Defaults]
Modem = /dev/ttyS1
Baud = 115200
Init1 = ATZ
Init2 = ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0
Phone = 703 321 4887
Username = bball
Password = mypassword
```

保存文件，然后使用 `wvdial` 命令从命令行启动你的连接，如下所示：

```
# wvdial
-- WvDial: Internet dialer version 1.41
-- Initializing modem.
-- Sending: ATZ
ATZ
OK
--> Sending: ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0
ATQ0 V1 E1 S0=0 &C1 &D2 S11=55 +FCLASS=0
OK
--> Modem initialized.
--> Sending: ATDT 703 321 4887
-- Waiting for carrier.
ATDT 703 321 4887
CONNECT 115200 V42bis
--> Carrier detected.  Waiting for prompt.
** Ascend TNT8.BRD Terminal Server **
Login:
--> Looks like a login prompt.
--> Sending: bball
bball
Password:
--> Looks like a password prompt.
--> Sending: (password)
Entering PPP Session.
IP address is 207.172.33.49
MTU is 1006.
--> Looks like a welcome message.
--> Starting pppd at Wed Jul 12 20:21:30 2000
```

`wvdial` 命令将在连接过程中输出诊断信息，甚至在连接断开时会自动重连！要结束你的会话，请按 Ctrl+C。

## 设置 DSL PPOE 连接

连接互联网的方式多种多样，ISP、大型网络公司和地区或政府电信公司提供的商业解决方案也各不相同。消费者（至少在美国）追捧的最新且日益普及的服务包之一是数字用户线，即 DSL 服务。

DSL 服务提供多种套餐，从 256Kbps\~640Kbps 到 4.5Mbps\~7.1Mbps 不等。该服务目前使用从中心局到家庭的铜质电话线，通常比专用互联网连接或综合数字网（ISDN）线路更便宜。与 ISDN 类似，DSL 连接允许在同一电话线上进行语音和数字传输。与 ISDN 不同，DSL 不会在单线路上将语音和数据分割到不同的信道，而是使用不同的频率进行数据传输。这要求家庭中的所有电话线使用数字滤波器，并在电话线和你的以太网局域网之间使用特殊的调制解调器。

DSL 服务是一种“始终在线”类型的互联网服务，尽管你可以通过软件实用工具在 Linux 下开启或关闭连接。使用 DSL 将需要在你的计算机或笔记本电脑中使用网络接口卡。为了与局域网上的其他计算机共享连接，你需要拥有一台网关、防火墙或至少配备两张网络接口卡的其他计算机。

与提供静态 IP 地址的 ISP 建立 DSL 连接相当简单。不幸的是，大多数 DSL 提供商现在使用一种名为 PPOE 的 PPP 协议的变形，即以太网点对点协议（Point-to-Point Protocol over Ethernet），它通过在以太网帧中封装 PPP 信息来提供动态 IP 地址分配和身份验证。幸运的是，你会在 Red Hat Linux 发行版中找到一个解决方案——Roaring Penguin 的 `rp-pppoe` 客户端！

### 设置 PPOE 连接

使用 Red Hat Linux 设置 DSL 连接的基本步骤包括连接适当的硬件，然后运行一个简单的配置脚本。你会发现建立基本连接的必要步骤相当简单，甚至可能比设置拨号 PPP 连接更容易。

首先，将你的 DSL 调制解调器连接到你的电话线。将调制解调器的以太网电缆插入你计算机的网络接口卡。如果你计划与局域网的其他部分共享你的 DSL 连接，你需要至少两张网卡，指定为 `eth0`（用于你的局域网）和 `eth1`（用于 DSL 连接）。

你还需要你的用户名和密码，以及你的提供商的 DNS 服务器的 IP 地址。以下示例假设你有多于一台计算机，并将在局域网共享你的 DSL 连接。首先，以 root 身份登录，并确保你的第一个 `eth0` 设备已启用并处于活动状态。你可以使用 `ifconfig` 命令通过输入接口名称和主机名来完成此操作，如下所示：

```
# ifconfig eth0 stinky up
```

接下来，启用另一个接口，但分配一个空地址，如下所示：

```
# ifconfig eth1 0.0.0.0 up
```

现在使用 `adsl-setup` 命令来设置你的系统。如下输入该命令：

```
# adsl-setup
Welcome to the Roaring Penguin ADSL client setup. First, I will run
some checks on your system to make sure the PPPoE client is installed
properly...
```

看起来没问题！现在，请输入一些信息：

**用户名**

请输入你的 PPPoE 用户名（默认 bxxxxxxx@sympatico.ca）： **bball**

在第一个提示符处，输入你的服务提供商提供的用户名，然后按 Enter。你会看到：

**接口**

请输入连接到 ADSL 调制解调器的以太网接口
（默认 eth1）： **eth1**

输入连接到你的 DSL 调制解调器的接口名称并按 Enter。然后你会被问及你的连接：

你想让链接按需连接还是持续保持连接？
如果你想让它按需连接，请输入空闲秒数，链接应在该时间后被断开。如果你希望链接永久保持连接，请输入 'no'。
注意：按需激活的链接与动态 IP 地址不太兼容。按需激活的链接可能会引起一些问题。
按需值（默认 no）： **no**

输入你的答案并按 Enter 后，你会被问及你的 ISP 的 DNS 服务器：

**DNS**
请输入你的 ISP 主要 DNS 服务器的 IP 地址。
如果你只是按 Enter，我将认为你知道自己在做什么，并且不会修改你的 DNS 设置。

在此处输入地址：199.45.32.38

请输入你的 ISP 次要 DNS 服务器的 IP 地址。
如果你只是按 Enter，我将认为只有一个 DNS 服务器。

在此处输入地址：199.45.32.43

输入你的 ISP 的 DNS 服务器的 IP 地址，并在每个提示符处按 Enter。下一节将询问你的密码：

**密码**

请输入你的 PPPoE 密码：

请重新输入你的 PPPoE 密码：

输入你的密码（两次）后，你会被要求选择防火墙和 IP 伪装规则。务必检查你的 Red Hat Linux 系统，以确保所有不需要的服务都已禁用，并且你已安装系统的所有勘误、错误和安全相关修复！

**# 防火墙设置**

请选择要使用的防火墙规则。请注意，这些规则非常基础。强烈建议你使用更复杂的防火墙设置；然而，这些将提供基本的安全保护。如果你在机器上运行任何服务器，你必须选择 'NONE' 并自行设置防火墙。否则，防火墙规则将拒绝访问所有标准服务器，如 Web、电子邮件、ftp 等。

- 防火墙选项包括：
  - 0 - NONE: 此脚本不会设置任何防火墙规则。你负责确保你的机器安全。强烈建议使用某种防火墙规则。
  - 1 - STANDALONE: 适用于基本的独立 Web 浏览工作站
  - 2 - MASQUERADE: 适用于作为局域网互联网网关的机器

你的选择？2

输入 0、1 或 2 来选择你要连接到互联网的系统类型。
按 Enter 后，你会看到：

```
** 你输入的内容摘要 **

以太网接口: eth1
用户名: dball99
按需激活: No
主要 DNS: 199.45.32.38
次要 DNS: 199.45.32.43
防火墙: MASQUERADE

接受这些设置并调整配置文件 (y/n)? y
```

