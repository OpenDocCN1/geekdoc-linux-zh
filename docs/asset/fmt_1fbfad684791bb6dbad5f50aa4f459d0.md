
与其他 ACL 行一样，你需要通过适当的 `http_access allow` 和 `http_access deny` 行来启用它们。

## 示例配置

为了帮助你理解 Squid 访问控制如何工作，并为你开发规则提供入门帮助，以下是一些你可以尝试的 ACL 行。每行之前都有一个或多行注释行（以 `#` 开头），解释其功能：

```
# 包含域名 newsw.bbc.co.uk 和 slashdot.org
# 但不包含 newsimg.bbc.co.uk 或 www.slashdot.org。
acl newswites dstdomain bbc.co.uk .slashdot.org
```

```
# 包含 bbc.co.uk 或 slashdot.org 的任何子域名
acl newswites dstdomain .bbc.co.uk .slashdot.org
```

```
# 仅包含位于加拿大的站点
acl canadasites dstdomain .ca
```

```
# 仅包含工作时间
acl workhours time MTWHF 9:00-18:00
```

```
# 仅包含午休时间
acl lunchtimes MTWHF 13:00-14:00
```

```
# 仅包含周末
acl weekends time AS 00:00-23:59
```

```
# 包含以 ".zip" 结尾的 URL。注意 \ 是重要的，因为否则 "*" 有特殊含义
acl zipfiles url_regex -i .zip
```

```
# 包含以 https 开头的 URL
acl httpsurls url_regex -i https
```

```
# 包含所有匹配 "Hotmail" 的 URL
acl url_regex hotmail url_regex -i hotmail
```

```
# 包含三个特定的 IP 地址
acl directors src 10.0.0.14 10.0.0.28 10.0.0.31
```

```
# 包含从 192.168.0.0 到 192.168.0.255 的所有 IP
# 以及从 10.0.0.0 到 10.255.255.255 的所有 IP
acl internal src 192.168.0.0/24 10.0.0.0/8
```

当你设置好 ACL 行后，就可以组合适当的 `http_access` 行。例如，你可能想使用多层访问系统，使得某些用户（例如公司董事）拥有完全访问权限，而其他人则被过滤。这是一个示例：

```
http_access allow directors
http_access deny hotmail
http_access deny zipfiles
http_access allow internal lunchtimes
http_access deny all
```

由于 Squid 按照顺序匹配这些行，因此董事将对网页拥有完全、未经过滤的访问。如果客户端 IP 地址不在 directors 列表中，则会处理两个 deny 行，使用户无法下载 zip 文件或在 Hotmail 上查看在线邮件。拦截之后

## 虚拟专用网络 (VPN)

虚拟专用网络（或 VPN）为远程用户访问安全网络创建了一个隧道。代理服务器充当中介，而 VPN 则像一根管道，通过使用普通网络传输数据包来加密流量。这对于在旅行期间需要访问内部资源的员工特别有用。有些人使用互联网路由器作为比喻来解释 VPN 的工作。在这个类比中，远程计算机直接连接到 VPN，VPN 使用互联网将其连接到其最终主机——安全网络。

### 虚拟专用网络 (VPN) 613

- 远程用户使用网络浏览器连接到代理服务器

- 代理服务器充当过滤器或缓存，并提供某些安全性

- 远程用户连接到互联网，开启 VPN 软件并使用它连接到安全网络

- VPN 像一根管道，通过使用普通网络传输数据包来加密流量

为什么要关注这些？代理服务器和 VPN 之间的差异在实施时影响最大。哪种能满足你的需求？这里是一些帮助你决策的事实：

- 代理服务器通常便宜且更容易设置。VPN 的成本更高且设置更困难，但在设置完成后它们易于使用且更安全。

- 单个代理服务器可以为成百上千的用户提供服务，但通常 VPN 是为针对特定远程计算机和安全主机的单一连接设计的。

- 每个使用代理的软件都必须单独设置。使用网络浏览器是使用代理服务器最常见的方式，但其他类型的软件也可以配置使用代理。当 VPN 运行期间，计算机上的所有互联网软件都会自动使用它，无需额外配置。

## 设置 VPN 客户端

使用 VPN 的简单部分也是最常需要的部分。通常，公司会建立 VPN 服务器，然后向公司员工或在本地系统（如笔记本电脑）上运行已安装 VPN 客户端的人员[授权]访问其安全网络。

大多数 VPN 服务器运行的是一种安装在 Ubuntu 上的协议，特别是对于典型用户使用的 Gnome 这种基于 GUI 的系统。您需要向您计划连接的 VPN 网络管理员确认您将将使用哪种 VPN 客户端，并获取连接所需的凭据。在本节中，为了管理 VPN 客户端连接，我们使用默认的 Network Manager（网络管理器），它是 Gnome 默认安装的，也是典型 Ubuntu 安装中管理所有互联网连接的工具。

为您将连接的网络所需的特定类型的 VPN 服务器安装所需的 VPN 客户端软件。下表将帮助您找到所需内容：

| 如果你需要使用 | 安装此项 |
|---|---|
| Cisco 集中器 | network-manager-vpnpc |
| OpenConnect | network-manager-openconnect |
| OpenVPN | network-manager-openvpn |
| PPTP (Microsoft VPN) | network-manager-pptp |
| strongSwan (用于某些 IPSec VPN) | network-manager-strongswan |

重启 Network Manager 以识别新安装包：

```
mattheaseymour:~$ sudo restart network-manager
```

点击 Gnome 屏幕顶部面板中的网络图标。点击图 36.3 所示的“VPN 设置”，将跳转到设置中的相应位置。

![](img/cc25c1772b156472bdf9ab1775163582_652_0.png)

图 36.3 Network Manager 让配置 VPN 客户端变得简单。

在设置中，您需要输入有关 VPN 连接的信息。您需要输入服务器的网关 IP 地址、您的账户用户名和密码、可能还有组名和组密码，以及证书机构（CA）文件的位置。在某些情况下，您可能需要点击“高级”按钮来输入其他细节，例如加密方法、NAT 遍历等。输入信息后，点击“保存”。

要启动此 VPN 连接，请使用图 36.3 相同的菜单，但这次从新创建的列表中选择您的 VPN 连接。

## 设置 VPN 服务器

在本节中，我们使用 OpenVPN 来演示如何设置一个简单的服务器。高级配置可能会变得相当复杂，但如果您只需要基础服务器，则很容易上手。

从 Ubuntu 软件源安装 openvpn。

接下来，您需要为 OpenVPN 创建一个公钥基础设施 (PKI)。设置证书机构以生成您自己的证书和密钥：

```
matthew@semour:~$ sudo mkdir /etc/openvpn/easy-rsa
matthew@semour:~$ sudo cp -r /usr/share/doc/openvpn/examples/easy-rsa/2.0/*
/etc/openvpn/easy-rsa/
```

通过编辑`/etc/openvpn/easy-rsa-vars`并调整以下内容来输入具体细节：

```
export KEY_COUNTRY="us"
export KEY_PROVINCE="IA"
export KEY_CITY="Iowa City"
export KEY_ORG="Your Company"
export KEY_EMAIL="yourContact@yourEmailDomain.com"
```

生成您的证书和机构密钥：

```
matthew@semour:~$ cd /etc/openvpn/easy-rsa
matthew@semour:~$ sudo source vars
matthew@semour:~$ sudo ./clean-all
matthew@semour:~$ sudo ./build-ca
matthew@semour:~$ sudo cp -r /usr/share/doc/openvpn/examples/easy-rsa/2.0/*
/etc/openvpn/easy-rsa/
```

为服务器生成证书和私钥，将 `yourusername` 替换为您的服务器名称：

```
matthew@semour:~$ sudo ./build-key-server yourusername
```
