
```
netdestination msonline-login
name login.microsoftonline.com
name *.aadcdn.microsoftonline-p.com

netdestination clearpass-prod
name clearpass.arubaboston.com
name clearpass-1.arubaboston.com
name clearpass-2.arubaboston.com
name wifi-login.arubaboston.com

netdestination social-twitter
name api.twitter.com
name *.twttr.com
name *.twimg.com

netdestination google-login
name accounts.google.com
name *.gstatic.com

netdestination duo-api
name api-0c3505b3.duosecurity.com
```

为了将 URL 或域名作为 `netdestination` 的部分，控制器需要定义 DNS 服务器并启用 DNS 查找。以下 CLI 命令将指定名称服务器、启用 DNS 查找（默认启用）并显示状态以确认设置：

```
(config) #ip name-server 10.254.1.21
Operation may not take effect until a reboot

(config) #ip domain lookup
Operation may not take effect until a reboot

(config) #show ip domain-name
IP domain lookup: Enabled
IP Host.Domain name: 7005-90.
DNS servers:
===========
10.254.1.21
(*) Dynamic DNS entry
```

## 反转选项 (Invert Option)

在创建目的别名时，`invert` 选项非常有用；然而，使用它也非常危险。`invert` 选项告诉控制器引用所述内容的反转。例如，以下目的指向除定义的 `192.168.1.0` 网络之外的所有网络。

```
(config) #netdestination not-the-192-network invert
(config-dest) #network 192.168.1.0 255.255.255.0
```

在目的别名中尝试多次使用 `invert` 时可能会出现问题。之前的示例显示了 `internal-network` 别名的创建。该别名引用了组织内部使用的三个网络。在定义了该目的别名后，您可能认为可以使用相同的逻辑创建一个目的别名来定义所有其他网络，只需反转每个网络引用即可，如下 CLI 命令所示：

```
(config) #netdestination all-other-networks invert
(config-dest) #network 192.168.1.0 255.255.255.0
(config-dest) #network 172.16.1.0 255.255.255.0
(config-dest) #network 10.100.0.0 255.255.255.0
```

不幸的是，这并没有被视为单一网络集。假设您允许 guest 通除三个内部网络外的任何网络，使用 `all-other-networks` 目的别名，您可以创建如下防火墙规则：

```
user alias all-other-networks permit
user network 192.168.1.0 255.255.255.0 invert
user network 172.16.1.0 255.255.255.0 invert
user network 10.100.0.0 255.255.255.0 invert
```

如果 guest 尝试与地址 `100.100` 的服务器通信，系统会将数据包与第一条规则进行比较。由于用户尝试与 `192.168.1.0` 通信，第一条规则将为真。在目的别名中有多个条目时，`invert` 会产生不符合预期的结果。建议不要使用 `invert` 选项。在任何目的中仅定义单个条目。

## 防火墙服务 (Firewall Service)

防火墙策略与 ACL 之间的主要区别之一是，防火墙策略不仅根据源和目的地址进行过滤，还可以根据数据包类型、特定协议、TCP 或 UDP 端口范围、或者如果启用了 AppRF 功能，根据应用程序或应用程序类别。AppRF 功能将在本章详细介绍。以下是可以指定的服务值：

**协议数字 0-255** 这是特定协议的数值。常见的协议包括 6 (Transmission Control Protocol)、17 (User Datagram Protocol)、47 (Generic Routing Encapsulation) 和 50 (Encapsulation Payload IPsec)。这是一个预定义的别名。别名将在本文后面解释。

**Any** 指任何类型的流量。

**App (在 WebUI 的 Service 列中显示为 Application)** 指定一个应用程序。参数 `app` 后跟随应用程序名称。ArubaOS 定义了超过 3000 个应用程序。如果您想查看应用程序完整列表，以下 CLI 命令将按字母顺序显示。为了使输出更易读，删除了最后一列 `Applied`。

```
#show dpi application all
```

| Name | App ID | App Category | Default Ports |
| :--- | :--- | :--- | :--- |
| abc-news | 1824 | web | 80,443 |
| adobe-connect | 929 | streaming | 80,443,1935 |
| bittrent | 15 | peer-to-peer | 1024-65535 UDP 1024-65535 |
| craigslist | 1848 | web | 80,443 |
| dropbox | 779 | cloud-file-storage | 80,443 |
| google-groups | 56 | collaboration | 80,443 |
| howstuffworks | 1004 | social-networking | 80 |

**Appcategory (在 WebUI 的 Service 列中显示为 Application Category)** 指定一个应用程序类别。参数 `appcategory` 后跟随应用程序类别名称。ArubaOS 定义了超过 20 个应用程序类别。如果您想查看应用程序类别列表，以下 CLI 命令将按字母顺序显示。

```
#show dpi application category all
```

| Name | App Category | ID | Applied |
| :--- | :--- | :--- | :--- |
| antivirus |  | 1 | 0 |
| authentication |  | 2 | 0 |
| behavioral |  | 3 | 0 |
| cloud-file-storage |  | 4 | 0 |
| collaboration |  | 5 | 0 |
| encrypted |  | 6 | 0 |
| enterprise-apps |  | 7 | 0 |
| gaming |  | 8 | 0 |
| im-file-transfer |  | 9 | 0 |
| instant-messaging |  | 10 | 0 |
| mail-protocols |  | 11 | 0 |
| mobile |  | 23 | 0 |
| mobile-app-store |  | 12 | 0 |
| network-service |  | 13 | 0 |
| peer-to-peer |  | 14 | 0 |
| social-networking |  | 15 | 0 |
| standard |  | 16 | 0 |
| streaming |  | 17 | 0 |
| thin-client |  | 18 | 0 |
| tunneling |  | 19 | 0 |
| unified-communications |  | 20 | 0 |
| web |  | 21 | 0 |
| webmail |  | 22 | 0 |
| Total application groups = 23 |  |  |  |

**MP (WebUI 不可用)** 指定 ICMP 协议。

**TCP** 指定 TCP 目的端口。TCP 后跟随一个 0-65535 之间的 TCP 数字。

**UDP** 指定 UDP 目的端口。UDP 后跟随一个 0-65535 之间的 UDP 数字。
