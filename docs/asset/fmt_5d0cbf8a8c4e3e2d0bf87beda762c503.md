
最后将显示你的输入条目。点击“Apply”保存。你的连接将出现在 IPsec 面板中，显示其类型、目的地和别名。要建立连接，选择 IPsec 连接并点击“Activate”。这将运行 `/etc/sysconfig/network-scripts` 目录下的 `ifup-ipsec` 脚本，它将执行 `setkey` 和 `racoon` 等 IP 工具来建立你的连接。配置数据将保存在 `/etc/sysconfig/networking/` 目录下，使用 IPsec 连接名称。配置信息保存在 `ifcfg-myipsec` 文件中。每个连接对应的密钥保存在 `keys-myipsec`。VPN 的示例配置是共享密钥的 IKE 方法。目的（远程）网关是 10.0.1，源（本地）网关是 192.168.0.1。目的（远程）网络是 10.0.0/24，源（本地）地址是 192.168.0.1（注：原文此处有重复，已按逻辑对齐）。此处为 VPN 示例配置。

### IPsec 和 IP Tables

IPTables 过滤会拦截任何 IPsec 数据包。要让 IPTables 放行 ipsec 数据包，请使用 IPTables 命令。AH 协议的编号为 51，ESP 协议为 50。要启用 IPsec 数据包，你应该按照如下选择策略规则：

```
iptables -A INPUT -p 50 -j ACCEPT
iptables -A OUTPUT -p 51 -j ACCEPT
```

### 使用 redhat-config-network 配置 IPsec

`redhat-config-network` 工具提供了实现 IPsec 连接的支持。在 `redhat-config-network` 工具上，选择 IPsec 面板（见图 17-1）并点击“New”启动创建 IPsec 连接的 IPsec 设置向导。首先要求你为连接输入别名，并指定是否自动启动。然后你选择连接类型。这可以是直接的主机到主机连接，也可以是两个网络之间的连接。网络连接实现虚拟网络（VPN）并在隧道模式下运行 IPsec。（主机和 VPN 连接的详情见下节节。）你选择想要使用的加密类型。这可以是手动的，也可以是 IKE，让 `racoon` 自动管理加密和身份验证过程。

然后你将配置本地和远程连接，从本地设置开始。对于主机到主机的连接，你只需要远程主机的 IP 地址。对于 VPN，你需要输入本地和远程网络的地址。对于本地网络，你需要输入本地网络的 IP 地址、本地网络的网关计算机和本地网络的子网掩码。对于远程 VPN 连接，你需要输入远程网络地址、子网掩码和网关地址。最后，你将输入身份密钥。点击“Generate”按钮创建一个。

最后将显示你的输入条目。点击“Apply”保存。你的连接将出现在 IPsec 面板中，显示其类型、目的地和别名。要建立连接，选择 IPsec 连接并点击“Activate”。这将运行 `/etc/sysconfig/network-scripts` 目录下的 `ifup-ipsec` 脚本，它将执行 `setkey` 和 `racoon` 等 IP 工具来建立你的连接。配置数据将保存在 `/etc/sysconfig/networking/` 目录下，使用 IPsec 连接名称。配置信息保存在 `ifcfg-myipsec` 文件中。每个连接对应的密钥保存在 `keys-myipsec`。VPN 的示例配置是共享密钥的 IKE 方法。目的（远程）网关是 10.0.1，源（本地）网关是 192.168.0.1。目的（远程）网络是 10.0.0/24，源（本地）地址是 192.168.0.1（注：原文此处有重复，已按逻辑对齐）。此处为 VPN 示例配置。

# 308 第四部分：安全

如前一个示例所示，如果主机信息相同，你可以省略主机信息。

```
esp/transport//require
```

### 接收端主机

为了使主机接收加密的 IPsec 传输，其自身的 SAD 数据库中必须有相应的安全关联（security association）指令，告诉它如何验证和解密接收到的指令。安全关联指令将与发送端的指令镜像，使用相同的加密方法、密钥和安全索引（security indexes）。因此，不需要相应的策略。

```
#!/usr/sbin/setkey -f
add 192.168.0.2 192.168.0.5 15700 -A hmac-md5 "secret key"
add 192.168.0.2 192.168.0.5 15701 -E 3des-cbc "secret key";
```

接收主机可能想要设置策略来筛选安全连接上的入数据包，丢弃那些未加密的数据包。以下策略将仅接受来自 192.168.0.2 的加密且经过认证的 IPsec 传输。

```
spd192.168.0.2 192.168.0.5 any -P in ipsec/transport//require
ah/transport//require;
```

### 双向传输

之前的示例在两个主机之间建立了单向的机连接，即从 192.168.0.2 到 192.168.0.5，而不是从 192.168.0.5 到 192.168.0.2 的反向。要实现两个主机之间具有安全关联的双向安全通信，两个主机都需要被配置为发送者和接收者，并匹配相应的安全关联。以下脚本基于两个主机之间双向 IPsec 连接的常见示例。它们在主机 192.168.0.2 和 192.168.0.5 之间建立了双向 IPsec 连接。包含了相应的入站策略，但并非强制要求：

首先是 192.168.0.2 的配置：

```
#!/usr/sbin/setkey -f
add 192.168.0.2 192.168.0.5 15700 -A hmac-md5 "secret key"
add 192.168.0.2 192.168.0.2 24500 -A hmac-md5 "secret key"

add 192.168.0.2 192.168.0.5 15701 -E 3des-cbc "secret key"
add 192.168.0.2 192.168.0.2 24501 -E 3des-cbc "secret key";
```

```
spd192.168.0.2 192.168.0.5 any -P in ipsec/transport//require
ah/transport//require;
spd192.168.0.5 192.168.0.2 any -P in ipsec/transport//require
ah/transport//require;
```

对应的主机 192.168.0.5 使用相同的指令，但 IP 连接反转了。注意，每端发送者和接收者指令的安全索引是相互对应的。

# 第 17 章：互联网协议安全：IPsec 309

```
#!/usr/sbin/setkey -f
add 192.168.0.5 192.168.0.2 ah 17501 -A hmac-md5 "secret key"
add 192.168.0.2 192.168.0.5 ah 24500 -A hmac-md5 "secret key"
```

```
192.168.0.5 192.168.0.2 esp 17501 -E 3des-cbc "secret key"
add 192.168.0.2 192.168.0.5 esp 24501 -E 3des-cbc "secret key"
```

```
spadd 192.168.0.5 192.168.0.2 any -P ipsec esp/transport//require
ah/transport//require;
spadd 192.168.0.2 192.168.0.5 any -P ipsec esp/transport//require
ah/transport//require;
```

## 配合 racoon 使用 IPsec：IKE

IPsec 密钥可以实现手动密钥、共享密钥或证书实现。手动密钥是显式交换的，容易产生安全问题。共享密钥和证书使用 IPSec 密钥交换协议（IKE）管理，该协议会自动交换密钥，并随机更改它们以避免检测。

使用 IKE 的优势之一是，如果没有提供任何安全关联，它将自动生成所需的安全关联。这意味着使用 IKE 配置安全连接，你只需要指定安全策略，而不是安全关联。

`racoon` 工具是 IPSec 协议的密钥交换守护进程。在共享密钥的情况下，`racoon` 通过预设密钥动态认证主机；在证书方法的情况下，使用证书文件进行认证。`racoon` 配置位于 `/etc/racoon/racoon.conf`。在这里可以设置通用参数。你可以使用默认的 `racoon.conf` 进行更多连接。`racoon` 配置包含了可能连接的语句（stanzas）。这是一个非常简单的配置，使用了共享密钥。其位置通过 `path_shared_key` 选项指定，例如 `/etc/racoon/psk.txt`。使用公私密钥的更安全的密钥方法将在后文中讨论。
