
## 以 root 用户身份运行 Minicom

运行 Minicom 时，在终端窗口或虚拟控制台的 shell 提示符下输入 minicom。如果以普通用户（非 root）身份运行 Minicom，Minicom 会显示以下错误消息并退出（除非系统管理员已为普通用户设置好 Minicom）：

```
minicom
minicom: there is no global configuration file /etc/minirc.dfl
Ask your sysadm to create one (with minicom -s).
```

以 root 身份登录，然后输入

```
minicom -s
```

Minicom 启动并显示一个对话框（见图 11-1），其中包含一个设置菜单，可让你配置 Minicom 的各个方面，包括串行端口以及调制解调器和拨号命令。要输入调制解调器初始化命令，请使用箭头键突出显示 Modem and dialing 项目（如图 11-1 所示）。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_158_0.png)

图 11-1
Minicom 设置菜单

将 Modem and dialing 条目突出显示后，按 Enter。Minicom 显示另一个菜单（见图 11-2），列出可更改的设置。Minicom 将光标放在第一行，如图 11-2 所示。按 A 以更改调制解调器初始化字符串。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_159_0.png)

### 图 11-2
在 Minicom 中设置调制解调器和拨号参数

然后你可以使用 Backspace 键编辑该行并输入用于初始化调制解调器所需的 AT 命令。例如，我有一台 56K 调制解调器，我用以下 AT 命令对其进行初始化：

```
AT &F1 E1 V1
```

输入调制解调器初始化字符串后，按 Enter 返回顶级菜单。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_159_1.png)

顺便说一下，AT 命令是指可用于控制调制解调器并执行诸如拨号、打开或关闭调制解调器扬声器以及设置调制解调器应答来电等任务的命令。这些命令以两个字符开头：AT（attention 的缩写）。当通信软件很原始，软件所做的只是将你输入的内容发送给调制解调器时，可以使用 AT 命令。

如果没有更多更改，使用上下箭头键突出显示标记为 Save as dfl（意为保存为默认）的项目，然后按 Enter。Minicom 将设置保存到 /etc/minirc.dfl 文件中——这是 Minicom 的默认配置文件。之后，你可以通过选择 Exit from Minicom 并按 Enter 来退出 Minicom。

## 以普通用户身份运行 Minicom

在任何用户能够运行 Minicom 之前，还需要执行以下操作：

- 在文本编辑器中打开文本文件 /etc/minicom.users 并验证其中是否有一行包含单词 ALL。（这使所有用户都能访问 Minicom 的默认配置文件。）如果没有，请添加一行包含单词 ALL。
- 假设你希望所有用户都可以使用调制解调器拨号，请允许任何用户读取和写入调制解调器连接的串行端口。例如，如果调制解调器位于 COM1（/dev/ttyS0）上，输入 chmod o+rw /dev/ttyS0 以授予每个人对该设备的写权限。
- 在 /dev/modem 与调制解调器连接的串行端口设备之间建立链接。如果调制解调器位于 COM1（/dev/ttyS0）上，你应输入以下命令：

```
ln -s /dev/ttyS0 /dev/modem
```

之后，你可以以普通用户身份运行 Minicom。Minicom 第一次运行时会重置调制解调器。图 11-3 显示了在终端窗口中运行 Minicom 的结果。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_160_0.png)

图 11-3
终端窗口中的初始 Minicom 屏幕

按 Ctrl+A 以获取 Minicom 程序的注意。然后如果按 Z，一个帮助屏幕会以文本窗口的形式出现（如图 11-4 所示）。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_161_0.png)

### 图 11-4
Minicom 帮助屏幕

在帮助屏幕中，你可以获取有关其他 Minicom 命令的信息。从帮助屏幕按 Enter 返回在线模式。在在线模式下，你可以使用调制解调器的 AT 命令拨号。特别是，你可以使用 ATDT 命令拨打另一台调制解调器的电话号码（例如，你的 Internet 服务提供商的计算机或工作中的系统），如图 11-5 所示。一旦收到登录提示，你可以像平常一样登录并使用远程系统。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_161_1.png)

### 图 11-5
使用 Minicom 拨号到远程系统

当你从另一系统注销并想要退出 Minicom 时，按 Ctrl+A 然后输入 X 退出程序。再次按 Enter 以响应 Minicom 提示。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_161_2.png)

## 回顾

你通过学习 Red Hat Linux 中串行端口的设备名称开始了本课。你使用 Minicom 串行通信程序通过调制解调器拨号。在拨号过程中，你学习了用于控制调制解调器的多个 AT 命令。

## 自测

1. 第二个串行端口（COM2）的设备名称是什么？
   （参见“Learning the Serial-Port Device Names in Linux”。）
2. 如何检查 Linux 是否检测到 PC 中的任何串行端口？
   （参见“Checking if Red Hat Linux Detects the Serial Devices”。）
3. 你可以使用什么程序通过调制解调器拨号？
   （参见“Dialing out with Minicom”。）
4. 你使用什么 AT 命令让调制解调器拨打电话号码？
   （参见“Running Minicom as an Ordinary User”。）
5. 你必须做什么才能在 /dev/modem 与调制解调器连接的串行端口设备之间建立链接？
   （参见“Running Minicom as an Ordinary User”。）

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_164_0.png)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_164_1.png)

## 为你的 Red Hat Linux PC 建立网络

### 课程清单

- ✓ 设置以太网局域网
- ✓ 在 Linux 中配置 TCP/IP 网络
- ✓ 在 Linux 中使用 TCP/IP 诊断命令
- ✓ 检查 TCP/IP 网络配置文件

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_164_2.png)

Red Hat Linux 包含广泛的内置网络功能。特别是，Red Hat Linux 支持通过多种物理接口（如以太网卡、串行端口和并行端口）进行 TCP/IP（传输控制协议/网际协议）网络。（TCP/IP 是一套用于在 Internet 上进行信息交换的网络协议。你不需要了解 TCP/IP 的细节即可在 Red Hat Linux 系统上设置和使用 TCP/IP 网络。）你通常使用以太网为本地局域网（LAN）。通过串行端口的 TCP/IP 网络使你能够通过调制解调器拨号连接到其他网络。

本课程重点介绍以太网局域网。你将学习如何设置、配置和监控以太网 TCP/IP 网络。你学到的许多内容也适用于通过拨号调制解调器的 TCP/IP 网络，这是下一课程的重点。

## 设置以太网局域网

Ethernet 是在连接到单根电缆的两个或多个计算机之间传输数据包的标准方法。要设置以太网局域网，每个 PC 都需要一块以太网卡。Linux 支持 PC 的各种以太网卡。

Ethernet 是物理数据传输机制的良好选择，因为它是一种经过验证的低成本技术，提供良好的数据传输速率——通常为每秒 1000 万位（10 Mbps），尽管现在已有 100 Mbps 甚至千兆以太网。

在以太网局域网中，计算机通过电缆连接到网络。如今，有两种流行的以太网电缆形式。第一个选项是 ThinWire 或 10Base2，使用细而柔韧的同轴电缆。另一种更新且更受欢迎的替代方案是通过非屏蔽双绞线（UTP）电缆的以太网，称为 10BaseT。

要设置 10BaseT 以太网，你需要一个以太网集线器——一个带有 RJ-45 接口的硬件盒子。你通过从每台 PC 的以太网卡铺设双绞线（通常是五类或 Cat5 电缆）到该集线器来构建网络。如今，你可以以约 50 美元（美国）购买一个 8 端口 10BaseT 集线器。图 12-1 显示了你在小型办公室或家中可能设置的小型 10BaseT 以太网局域网。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_165_0.png)

图 12-1
带集线器的 10BaseT 以太网局域网

ThinWire 以太网不需要集线器，这使其对拥有多台 PC 的小型办公室或家庭办公室具有吸引力。你可以简单地将 ThinWire 电缆从一台 PC 串联到另一台 PC 并构建一个小型以太网局域网，如图 12-2 所示。
