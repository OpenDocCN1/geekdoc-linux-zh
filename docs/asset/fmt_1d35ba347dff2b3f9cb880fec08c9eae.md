
## Turning the PPP connection on or off

打开或关闭 PPP 连接

您不必始终运行拨号配置工具来打开或关闭 PPP 连接。相反，在配置 `ppp0` 接口后，您只需输入以下命令即可启动 PPP 连接：

```
/sbin/ifup ppp0
```

当您不再需要 PPP 连接时，可以以 root 身份登录并输入以下命令断开连接：

```
/sbin/ifdown ppp0
```

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_183_1.png)

10 分钟
剩余

## Using IP Masquerading to Share an Internet Connection

使用 IP 伪装共享 Internet 连接

Linux 支持一种称为 IP 伪装的功能，可让您将具有私有 IP 地址的以太网 LAN 连接到 Internet。这是通过一台具有官方分配 IP 地址且已连接到 Internet 的 Linux PC 实现的。该 Linux PC 可以通过拨号 PPP 或其他连接（如 DSL 或电缆调制解调器）连接到 Internet。

启用 IP 伪装后，您的 Red Hat Linux PC 会充当以太网 LAN 上其他系统的替代品。与路由器设置一样，Red Hat Linux PC 被指定为以太网 LAN 的网关。然而，伪装不仅仅是在 LAN 和 Internet 之间简单地转发 IP 数据包。

当 Red Hat Linux PC 伪装成 LAN 上的另一台系统时，它会修改传出数据包，使其始终看起来源自 Red Hat Linux PC。当收到对其中一个传出数据包的响应时，Red Hat Linux PC 会执行相反的操作——它修改数据包，使其看起来是从 Internet 直接发送到发送传出数据包的系统。最终结果是，以太网 LAN 上的每个系统似乎都可以完全访问 Internet，即使以太网 LAN 使用非唯一的私有 IP 地址。

要启用并使用 IP 伪装，请执行以下步骤：

- 1. 确保 Linux 内核——核心操作系统——支持 IP 防火墙链。对于从随附 CD-ROM 安装的 Red Hat Linux 版本，这应该是正确的。如果文件 `/proc/net/ip_fwchains` 存在，则内核支持 IP 防火墙链。 （输入 `ls /proc/net/ip_fwchains` 以验证文件是否存在。）
- 2. 确保 Red Hat Linux PC 具有 Internet 连接和到您 LAN 的网络连接。通常，Linux PC 具有两个网络接口——用于 LAN 的以太网卡和通过 ISP 的拨号 PPP 连接到 Internet。
- 3. 确保 LAN 上的所有其他系统都使用 Linux PC 作为 TCP/IP 网络的默认网关。所有系统上使用相同的 ISP 提供的 DNS 地址。
- 4. 通过输入以下命令在内核中启用 IP 转发：
  - `echo "1" > /proc/sys/net/ipv4/ip_forward`
  - 这是必要的，因为默认情况下 IP 转发是禁用的。为了确保在重新启动系统时启用 IP 转发，请将此命令放在 `/etc/rc.d/rc.local` 文件中。在 Red Hat Linux 中，您可以通过将 `/etc/sysconfig/network` 文件中的行 `FORWARD_IPV4=false` 改为 `FORWARD_IPV4=true` 实现相同的效果。
- 5. 运行 `/sbin/ipchains`——IPCHAINS 防火墙管理程序——以设置使 Linux PC 能够为您的 LAN 伪装的规则。例如，要通过 Linux PC 的 `ppp0` 网络接口为 LAN 启用伪装，您可以使用以下命令：
  - `/sbin/ipchains -P forward DENY`
  - `/sbin/ipchains -A forward -i ppp0 -j MASQ`

如果您希望在系统启动时设置 IP 伪装，您应该将这些命令放在 `/etc/rc.d/rc.local` 文件中。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_185_0.png)

您可能会发现 IP 伪装是一种方便的方式，为小型局域网提供 Internet 访问（例如家庭或办公室的局域网）。在家中，我使用 IP 伪装通过 Linux 系统将以太网局域网连接到 Internet。Linux PC 具有用于局域网连接的以太网卡和用于通过 ISP 连接到 Internet 的调制解调器。（我从 ISP 获得了有效的 IP 地址。）在 Linux PC 上使用 IP 伪装后，您家庭或小型企业中的每个人现在都可以从局域网上的任何其他 PC 访问 Internet。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_185_1.png)

## REVIEW

本会话向您介绍了拨号网络——通过拨号调制解调器在 Linux PC 与 Internet 之间建立网络连接。您学习了如何使用 Red Hat 拨号配置工具设置 PPP 连接。最后，本会话向您展示了如何使用 IPCHAINS 防火墙管理程序的 IP 伪装功能共享单个 Internet 连接。

## QUIZ YOURSELF

- 1. 什么是拨号网络和 PPP？（参见“学习拨号网络的基础知识”。）
- 2. ISP 通常提供哪些信息供您设置拨号 PPP 连接？（参见“使用 PPP 连接到 Internet”。）
- 3. 您使用什么工具来设置 PPP 连接？（参见“使用 PPP 连接到 Internet”。）
- 4. 您会输入什么命令来打开和关闭 PPP 连接？（参见“打开或关闭 PPP 连接”。）
- 5. 什么是 IP 伪装？（参见“使用 IP 伪装共享 Internet 连接”。）

## SESSION

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_186_0.png)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_186_1.png)

## Setting Up Internet Services

## 会话清单

- ✓ 了解 Internet 服务
- ✓ 使用电子邮件服务器
- ✓ 设置 Apache Web 服务器
- ✓ 设置 FTP 服务器

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_186_2.png)

如果 Red Hat Linux PC 连接到 Internet 或内联网（私有 TCP/IP 网络），您就可以将其用作服务器。Internet 和内联网都依赖于 Internet 服务。每个 Internet 服务都涉及在 Red Hat Linux 系统上配置和运行一个或多个服务器。本会话向您介绍常用的 Internet 服务。然后重点介绍实现邮件、Web 和信息检索 Internet 服务的服务器：电子邮件服务器、Apache Web 服务器和 FTP 服务器（它们使任何人都能以合理安全的方式从您的系统下载文件）。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_186_3.png)

您将在第 29 会话中了解如何保护您的 Red Hat Linux 系统。

## Understanding Internet Services

术语 Internet 服务指的是采用客户端/服务器架构来执行特定任务的多个网络应用程序。（在客户端/服务器架构中，两个独立的程序——提供信息的服务器和一个或多个请求信息的客户端——实现一个服务。）

许多 Internet 服务专门设计用于将信息从一个系统传递到另一个系统。信息可能以邮件消息、新闻项目或数据文件的形式出现。作为用户，您期望从典型的 Internet 主机访问这些常见的 Internet 服务：

- *电子邮件 (e-mail)*。从 Internet 主机，您可以使用地址如 `president@whitehouse.gov` 向 Internet 上的任何其他用户发送电子邮件。
- *万维网*。您可以使用 Web 浏览器通过统一资源定位符 (URL) 地址如 `http://www.whitehouse.gov` 下载和查看网页。网页通常是使用超文本标记语言 (HTML) 格式化的文档。
- *新闻组*。您可以阅读新闻组并向名称如 `comp.os.linux.networking` 或 `comp.os.linux.setup` 的新闻组发布新闻项目。
- *信息检索*。您可以使用万维网浏览器等工具搜索信息。您也可以使用文件传输协议 (FTP) 下载文件。反之，其他系统上的用户也可以从您的系统下载文件——通常通过称为匿名 FTP 的功能。
- *远程访问*。您可以使用 TELNET 登录 Internet 上的另一台计算机（远程计算机），前提是您拥有访问该远程计算机的用户名和密码。

所有 Internet 服务都依赖于客户端和服务器软件。例如，电子邮件服务器负责将邮件从一个系统传输到另一个系统，而您使用电子邮件客户端软件阅读电子邮件。同样，您使用 Web 浏览器客户端从 Web 服务器下载和查看网页。

实现 Internet 服务的客户端和服务器使用 TCP/IP 协议相互通信。您已经熟悉标识 TCP/IP 网络中主机的 IP 地址。然而，仅凭 IP 地址不足以区分同一系统上运行的许多服务。端口号（或简称为端口）的概念用于使各种 Internet 服务器能够与客户端通信。端口不是物理实体——它只是一个介于 1 和 65,535 之间的数字，用于唯一标识两个进程（通常是服务器和客户端）之间 TCP/IP 通信链路的每个端点。

所有众所周知的 Internet 服务都有预先分配的端口号。例如，这里有一些常用的 Internet 协议及其分配的端口号：

- *FTP (File Transfer Protocol)* 允许在 Internet 上的计算机之间传输文件。FTP 使用两个端口——数据在端口 20 上传输，而控制信息在端口 21 上交换。FTP 是文件传输的基础协议。
- *HTTP (Hypertext Transfer Protocol)* 是用于从一个系统向另一个系统发送 HTML 文档的最新协议。HTTP 是 Web 的基础协议。默认情况下，Web 服务器和客户端在端口 80 上通信。
- *SMTP (Simple Mail Transfer Protocol)* 在系统之间交换电子邮件消息。SMTP 使用端口 25 进行信息交换。SMTP 是电子邮件服务的基础协议。
- *NNTP (Network News Transfer Protocol)* 以存储转发方式在 Internet 上分发新闻文章。NNTP 使用端口 119。NNTP 是新闻组服务的基础协议。
- *TELNET* 使一个系统上的用户能够登录 Internet 上的另一个系统。（用户必须提供有效的用户 ID 和密码才能成功登录远程系统。）TELNET 默认使用端口 23。然而，TELNET 客户端可以连接到任何指定的端口。TELNET 是远程访问的基础协议。
- *NFS (Network File System)* 在计算机之间共享文件。NFS 使用 Sun 的 *Remote Procedure Call (RPC)* 设施，该设施通过端口 111 交换信息。

文本配置文件——`/etc/services`——存储 Internet 服务与端口号（以及底层数据通信协议）之间的关联。要查看此文件的内容，请使用 `more` 命令如下：

```
