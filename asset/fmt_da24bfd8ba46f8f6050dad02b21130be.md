
要列出当前连接到本地桌面并在其上创建窗口的系统，请不带参数输入 `xhost` 命令：

```
[you@workstation20-$] xhost
access control enabled, only authorized clients can connect
INET:workstation10.mycompany.com
INET:mailserver.mycompany.com
INET:sunsystem1.yourcompany.com
INET:10.1.24.192
[you@workstation20-$]
```

列出的系统都可以在本地桌面上打开应用程序。要从允许连接到本地桌面的系统列表中删除某个系统，调用 `xhost` 并在要删除的名称前加上减号（`-`）：

```
[you@workstation20-$] xhost -workstation10.mycompany.com
workstation10.mycompany.com being removed from access control list
[you@workstation20-$]
```

### 远程显示本地应用程序

当你从命令行启动桌面应用程序时，应用程序将通过查看 `DISPLAY` shell 变量来决定在何处显示应用程序窗口。`DISPLAY` 变量应该持有以下格式的值：

例如，要允许运行在计算机 `workstation10` 和 `mailserver` 上的程序显示在本地计算机的桌面上，输入以下内容：

```
[you@workstation20-$] xhost workstation10@ mailserver
workstation10 being added to access control list
mailserver being added to access control list
[you@workstation20-$]
```

## 第 27 章：远程使用桌面应用程序

## 注意！

### 仅在万不得已的情况下使用 telnet

由于 `telnet` 命令在不先进行加密的情况下通过网络发送密码，因此 `telnet` 的安全性低于 `ssh`。恶意网络用户可以窃取 `telnet` 会话中使用的密码。因此，只有当你的网络位于专用防火墙之后时才使用 `telnet`，尽可能使用本章之前讨论的 `ssh` 技术。

该过程通过以下命令序列所示。假设你正在运行一个名为 `workstation20.mycompany.com` 的系统。该序列在名为 `newton` 的远程系统上启动 `emacs` 程序，并在你的桌面上显示其应用程序窗口：

```
[you@workstation20~$ telnet newton
Trying 10.4.26.131...
Connected to newton.
Escape character is '^'.
Solar (newton)
login: joeser
Password:
[joeser@newton joeser$ DISPLAY=workstation20.mycompany.com:0
[joeser@newton joeser$ export DISPLAY
[joeser@newton joeser$ emacs &
[1] 31221
[joeser@newton joeser$]
```

输入此序列后，`emacs` 程序将出现在你的本地显示器上，运行在名为 `newton` 的系统上。

## 允许并启动远程 X 会话

虽然远程运行单个应用程序方便，但有时从远程位置运行整个桌面会话（从图形化登录界面开始）会更有帮助。当你构建无盘客户端，或使用安装了极简 Linux 并需要作为全功能工作站的小型计算机时，这种功能将特别别有帮助。

通过更改 Red Hat Fedora 4 登录管理器配置中的设置，你可以允许从登录到注销的远程桌面会话。在此更改后，你可以通过 Linux 控制台向 `XFree86` 命令提供特殊参数，或者通过从桌面上使用 `Xfb` 命令来启动远程会话。

## 为 XDMCP 配置登录管理器

要允许用户在 Fedora Core 4 主机上远程显示整个 X Window 系统会话，你必须配置首次启动 Red Hat Fedora 4 时看到的登录管理器程序，以允许使用 X 显示管理器控制协议 `XDMCP` 的请求。要实现这一点，可以使用 Fedora Core 4 的 GNOME 桌面管理器 `GDM` 设置工具（选择桌面、系统设置、登录屏幕），或者在任何 Fedora 系统上以 root 身份登录时在命令行输入 `gdmsetup`。一旦工具启动，点击 XDMCP 选项卡以显示图 27.5 所示的对话框。

![](img/2d355c162ea76302aa136ba324839b24_516_0.png)

> 图 27.5

在 GDM 设置工具中，勾选“Enable XDMCP”以允许网络上的其他主机登录此主机的会话。

在 XDMCP 选项卡中，勾选第一个复选框“Enable XDMCP”。选择此设置允许远程系统从你的计算机查询整个 X Window 系统会话；你的计算机会在远程机器上显示登录提示，允许用户图形化地登录并使用你机器上的应用程序和环境。

在接受传入的 XDMCP 请求之前，还必须正确配置防火墙。要实现这一点，请按照本章前面的说明启动“安全级别配置”工具，并在“其他端口”（Other Ports）框中输入以下附加异常：

```
177:tcp,177:udp
```

此设置允许端口 177 上的传入流量，这是 XDMCP 协议使用的端口。有关使用安全级别配置工具为某些网络端口创建异常的更多信息，请参阅第 30 章“安全基础”中的“管理 Red Hat Fedora 4 防火墙”。

## 注意！

### XDMCP 也可能存在安全风险

你熟悉的警告也适用于这里：只有当你的局域网位于专用防火墙之后时，才应启用 XDMCP 请求。在直接连接到互联网的机器上允许 XDMCP 请求会让你受到攻击，导致数据丢失或被窃。

## 查询远程会话

在你的机器上启用 XDMCP 后，安装了 X Window 系统的机器可以查询会话（访问你机器上的图形化登录提示）。这意味着远程用户可以在你的机器上工作，就像他们坐在它面前一样。

传统的，远程桌面会话是从控制台查询的，而不是在现有的 X Window 系统会话内部查询。这可以通过多种方式实现，取决于机器上 X Window 系统的版本和供应商。运行 XFree86 3.x 或更早版本的 Linux 或 Unix 机器，在控制台输入的命令之一是：

- - query host
- Xrapper query host

将 `host` 替换为请求 XDMCP 会话的主机名或 IP 地址。对于运行 XFree86 4.x 或更晚版本的 Linux 机器（包括所有 Fedora 机器），命令是

`XFree86 -query host`

再次，将 `host` 替换为问题机器机名或 IP 地址。例如，假设你已经在计算机 `workstation20` 上启用了 XDMCP，名为 `danscomputer` 的 Red Hat Fedora 4 用户可以通过在控制台输入以下命令访问你的图形化登录提示：

```
[dan@danscomputer~$ XFree86 -query workstation20
```

Dan 输入此命令后，登录提示出现在他的本地显示器上。（注意：OCR 处为“emacs application”，但上下文暗示是登录提示）。

# 总结

在本章中，你学习了使用 Unix 操作系统的一项独特网络功能，即在一台机器上运行应用程序，同时将其应用程序窗口显示在另一台机器的图形桌面上。具体而言，你学习了以下内容：

- 如何使用 `ssh` 命令自动化启动远程应用程序并在本地运行的流程。
- 如何使用 `xhost` 命令控制对任何 Unix 或 Linux 计算机上本地 X Window 系统的连接权限。记住，应尽可能使用 `ssh` 方法代替 `xhost` 方法。
- 如何结合 `DISPLAY` 环境变量和 `xhost` 命令启动本地应用程序进行远程显示。
- 当 `ssh` 不可用用时，如何结合 `xhost` 和 `DISPLAY` 使用 `telnet` 命令在远程启动应用程序并在本地显示。
- 如何启用 XDMCP 并跨越网络查询远程 X Window 系统会话。

当你掌握了这些技术后，你在网络中的物理位置将变得不再重要，因为你可以访问网络中任何位置计算机上的各种应用程序（无论是图形界面还是文本界面），从距离你所在地最近的计算机开始。

# 问答

X Window 系统帮助页提到了另一种名为“魔法 Cookie 认证”（magic cookie authentication）的安全性，它比 `xhost` 命令更安全。为什么这里没有讨论它？
