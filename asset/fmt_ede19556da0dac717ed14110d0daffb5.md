
```
Kernel IP routing table
Destination Gateway Genmask Flags MSS Window irtt Iface
10.0.0.0 * 255.255.255.0 U 0 0 eth0
```

# 第 16 章：连接互联网

`169.254.0.0` `0.0.0.0` `255.255.0.0` U 0 0 `eth0`

`default` `10.0.0.1` `0.0.0.0` UG 0 0 `eth0`

你可以看到默认网关设置为 `eth0` 接口上的主机 IP 地址 `10.0.0.1`。假设此路由器已准备好将你的数据包路由到互联网，你的 Linux 客户端现在已准备好用于查找你请求的、你尚不知道位置的所有 IP 地址。`netstat -r` 命令提供的输出与 `/sbin/route` 命令相同。

## 配置虚拟专用网络连接

在 Linux 中设置 VPN 连接有几种方法：

- **网协议安全安全 (IPSec)** — IPSec 是由互联网工程任务组 (IETF) 开发的一种标准，用于在 IP 版本 6 成为标准互联网协议时提供强制性的加密方法（目前在 IPv4 的北美和欧洲已是标准）。如今 Linux 的 IPv4 中有多种 IPSec 的实现。Linux 2.6 内核包含了对 IPSec 支持，并提供了一个管理接口进行配置（通过 `ipsec-tools` 软件包）。

- **PPP over OpenSSH** — 这种方法使用 Linux 中已有的软件，配置一个 PPP 接口（就像普通的拨号连接一样），使用 SSH 加密所有通过 PPP 接口传输的数据。虽然这种方法配置起来并不困难，但性能可能较差。要查看如何使用 PPP over OpenSSH VPN，请参阅 VPN PPP HOW-TO（见 www.tldp.org）。

- **OpenVPN** — 通过 OpenVPN (http://openvpn.net)，你可以使用 OpenSSL 加密和认证功能，通过公共网络（如互联网）创建通到远程系统的隧道。可以从 Fedora 软件仓库获取适用于 Fedora 的 OpenVPN 包（输入 `yum install openvpn`）。

- **Openswan** — Opens 项目 (www.openswan.org) 产生了一种 IPSec 的实现，该实现最初基于 Free/SWAN 项目 (www.freeswan.org) 的代码。Openswan 包含在 Fedora 软件仓库中；要安装它，输入 `yum install openswan`。

- **加密 IP 封装 (CIPE)** — 使用这种方法，IP 数据包作为加密的 UDP 包绕过指定的 IP 接口路由。CIPE 易于设置且开销比 PPP over OpenSSH 小，因此你应该获得更好的性能。一个缺点是，因为它不是标准的 VPN，所以 CIPE 在所有平台上并不可用。

第 15 章解释了使用 VPN 的基本原理，以及如何配置 NetworkManager 与远程 openvpn 服务器通信。在本章中，我将提供 IPSec 功能和工具的概述，并详细描述了在 Fedora 中配置 OpenVPN 服务器的步骤。

## 理解 IPsec

为了在新的互联网协议 6 (IPv6) 标准中提供更安全的 TCP/IP 数据传输，该标准的开发者创建了互联网协议安全 (IPsec) 架构。通过 IPsec，可以直接在 IP 层实现加密通信，并且提供访问控制、数据完整性、认证和流量机密性的方法也经过了标准化。

在实践中，需要在公共网络上进行安全且私密通信的计算机的组织使用 IPsec 创建 VPN。与其他 VPN 实现（如 CIPE）需要手动交换密钥才能工作不同，IPsec 提供了一种自动方法，可以在通信端点之间创建安全关联并管理密钥。

由于 IPv6 在美国和其他地方采用较慢，IPsec 已被回溯（backported）到 IPv4 协议中，而这仍然是互联网上最常用的 IP 版本。此回溯被添加到从版本 2 开始的 Fedora 自带的 Linux 2.6 内核中。互联网标准 RFC2401 文档描述了 IPsec 架构。

## 使用 IPsec 协议

IPsec 由两个主要协议组成：认证头 (AH) 和封装安全载荷 (ESP)。查看 `/etc/protocols` 文件，你会发现 AH 分配协议号 50，ESP 分配协议号 51。

为了对等计算机进行认证并交换对称密钥，IPsec 使用互联网密钥交换 (IKE) 协议。在使用 IPsec 的两个主机计算机之间的通信开始时，IKE 执行以下操作：

- 协商安全关联
- 选择对称密钥（使用 Diffie-Hellman 密钥交换）

由 IKE 建立的安全存储在安全关联数据库 (SAD) 中。安全关联持有有关通信端点的信息（可能是公共 IP 地址）、是否在 IPsec 中使用了认证头 (AH) 或封装安全载荷 (ESP) 协议，以及正在使用的秘密密钥/算法。

IPsec 本身有两种工作模式：隧道模式和传输模式。

- **隧道模式** — 整个 IP 数据报由 IPsec 封装在新的 IP 数据报中。这保护了数据和控制信息不被允许解密通信的通信端点以外的任何人看到。

- **传输模式** — 仅对数据（发送给接收数据的客户端负载）进行加密。为了实现这一点，IPsec 在互联网协议头和上层协议头之上插入其自己的头部。

传输模式的协议头中包含以下内容：

- **数据完整性** — 使用 HMAC，接收者可以验证数据在传输过程中未被更改。支持的算法包括 MD5、SHA1、AES 等。

- **数据隐私** — 加密确保了数据的机密性。支持的算法包括 DES、3DES、AES 等。

## 在 Fedora 中使用 IPsec

在 Fedora 或 RHEL 中使用 IPsec，你需要 `ipsec-tools` 软件包。该包提供了配置和管理 IPSec 的工具。使用了以下命令：

- **setkey** — 使用此命令管理安全关联数据库 (SAD) 和安全策略数据库 (SPD)。

- **racoon** — 使用此守护进程处理互联网密钥交换 (IKE)。

这些工具的配置文件位于 `/etc/ipsec/`。例如，`ipsec.conf` 用于定义策略和连接。

## 配置 OpenVPN 服务器

专用网络的创建是为了允许计算机系统通过不安全的网络建立安全连接。在你的业务场所设置 OpenVPN 服务器可以为分支机构或电信提供安全访问公司网络的廉价方案。

由于 VPN 技术（如 OpenVPN）在传输层接口之间提供加密连接，因此这两个系统之间的任何应用程序都是安全的。这与用户空间应用程序（如 SSL）不同，后者必须实现每个应用程序的功能。

对于 Linux 系统，OpenVPN 提供了配置 VPN 服务器的良好选择。以下是 OpenVPN 的某些功能：

- 单端口支持 128 个客户端访问。
- 服务器可以控制客户端设置，通过 VPN 隧道向客户端推送配置数据。
- 你可以使用 telnet 访问服务器。
- OpenVPN 在网络层包含了 TUN/TAP 虚拟网络接口驱动，设备名称如 `/dev/tun.X` 和 `/dev/tapX`。

本章的 OpenVPN 过程描述了如何设置 OpenVPN 服务器。这包括：

- 设置创建证书机构证书和密钥所需的信息。在此过程中，你创建一个需要保密的根 RSA 私钥 (`ca.key`) 和一个共享的根证书 (`ca.crt`)。
- 设置配置文件并启动 OpenVPN 服务。

### 配置 OpenVPN 之前的决策

在设置 OpenVPN 连接之前，你需要做出的决策包括：

#### 第 16 章：连接到互联网

- 你想使用公钥基础设施还是静态密钥？如果你只有一个 VPN 客户端连接到单台服务器，可以使用静态密钥。这样你就不需要维护一套密钥基础设施了。更多信息请参阅 OpenVPN HOWTO：http://openvpn.net/index.php/documentation/howto#examples

- 你的 VPN 是进行路由（routing）还是桥接（bridging）？路由（将数据从 VPN 服务器路由到局域网（LAN），而不仅仅是透传）通常是桥接更好的选择。路由更容易设置，并能为特定的客户端功能提供更多控制。

以下内容假设你已决定建立公钥基础设施并正在使用路由模式的 OpenVPN 服务器。有关如何使用 OpenVPN 进行桥接的信息，请参考以太网桥接 FAQ (http://openvpn.net/faq.html#bridge)

### 创建公钥基础设施

通过证书和私钥，你可以创建一个安全环境，允许多个客户端通过互联网访问你的私有网络。以下步骤在 Fedora 系统上执行，该系统不一定与你用于 VPN 服务器的系统相同。然而，在示例中，整个过程都在 OpenVPN 服务器上运行。

要开始设置你的公钥基础设施，请以 root 身份打开终端窗口并执行：

1. 复制示例配置文件：
