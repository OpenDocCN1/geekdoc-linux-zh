
目前已有多个项目致力于IPsec工具的开发与实现。最初的IPsec工具由KAME项目提供，网址为www.kame.net。当前版本可从sourceforge.net/projects/ipsec-tools获取。RPM包可从rpmfind.net获取。其他IPsec工具项目包括Free Secure/Wide Area Network项目（FreeS/WAN），网址为www.freeswan.org，该项目提供IPsec工具的Linux实现；以及VPN Consortium（VPNC），网址为www.vpnc.org，支持Windows和Macintosh版本。FreeS/WAN既提供Red Hat RPM包，也提供其工具的源代码。

> **注意：** 目前，Fedora Core不包含对IPsec工具的支持，但后续版本会支持。`redhat-config-network`工具包含IPsec支持的面板，但您需要安装IPsec工具才能激活此支持。

### IPsec协议

IPsec由多个协议组成，用于提供认证（AH）、加密（ESP）以及加密密钥的安全交换（IKE）。认证头协议（AH）确认数据包由发送者发送，而非他人。IPsec还包含完整性检查，用于检测传输过程中是否有任何篡改。数据包使用封装安全载荷（ESP）进行加密。加密和解密使用发送方与接收方共享的密钥执行。这些密钥本身通过互联网密钥交换协议传输，该协议提供安全交换。ESP加密可能会降低某些压缩传输方法的性能，例如用于拨号互联网连接的PPP。为适应这些压缩方法，IPsec提供了IP载荷压缩协议（IPComp），数据包在发送前可先进行压缩。

AH、ESP和IPComp协议已集成到Linux内核中。IKE协议作为独立的守护进程实现。它只提供共享密钥的方式，也可以用其他共享方法替代。

### IPsec模式

您可以将IPsec功能用于普通传输或数据包隧道。在普通传输模式下，数据包被加密后发送到下一个目的地。普通传输模式用于实现直接的主机到主机加密，每台主机都自行处理IPsec加密过程。数据包隧道用于加密网关之间的传输，让网关处理进出整个网络的流量的IPsec加密过程，而不必为每台主机配置IPsec加密。利用数据包隧道，数据包会封装上针对特定目的地的新报头，从而能够实现虚拟专用网络（VPN）。数据包被定向到VPN网关，网关对本地网络数据包进行加密并发送出去。

> **注意：** 您可以选择为特定主机或通过特定端口的数据包进行加密。

### IPsec安全数据库

您选择加密的数据包由IPsec安全策略数据库（SPD）指定。加密方法由IPsec安全关联数据库（SAD）确定。SAD将加密方法和密钥与特定连接或某种连接相关联。需要加密的连接在安全策略数据库中指定。

### IPsec工具

系统提供了几种IPsec工具，您可以使用它们管理IPsec连接（见表17-1）。`libipsec`工具用于构建密钥库。使用`setkey`可以管理策略和关联数据库。`racoon`工具用于配置密钥交换过程，以在连接之间实现安全的解密密钥交换。要查看SPD数据库中当前的安全策略，可以使用`setkey -DP`。对于SAD中的安全关联，可以使用`setkey -D`。

> **注意：** 要在内核中启用IPsec，请务必在“加密选项”中启用PF_KEY、AH和ESP选项。

| 工具 | 描述 |
| --- | --- |
| libipsec | 构建 PFKey |
| setkey | 管理策略 (SPD) 和关联 (SAD) 数据库 |
| racoon | 使用 IPsec 密钥交换 (IKE) 配置和实现安全密钥交换 |
| setkey-SP | 检查 SAD 数据库中的安全关联 |
| setkey-DP | 检查 SDP 数据库中的安全策略 |

表 17-1 IPsec 工具

## IPsec 和 IP 表

IPTables 过滤会阻止许多 IPsec 数据包。要使 IPTables 允许 IPsec 数据包通过，请使用以下 IPTables 命令。AH 协议的编号为 51，ESP 协议为 50。要允许 IPsec 数据包，应设置如下策略规则。

```
iptables -A INPUT -p 50 -j ACCEPT
iptables -A OUTPUT -p 51 -j ACCEPT
```

## 使用 redhat-config-network 配置 IPsec

`redhat-config-network`工具现在提供了实现 IPsec 连接的支持。在`redhat-config-network`工具中，选择 IPsec 面板（见图 17-1）并单击 New 以启动 IPsec 设置向导来创建 IPsec 连接。首先要求你为连接输入一个昵称并指定是否希望自动启动。然后你选择连接类型。这可以是主机到主机的直接连接或两个网络之间的连接。网络连接实现虚拟专用网络 (VPN) 并以隧道模式运行 IPsec。（主机和 VPN 连接均在以下各节中详细描述。）然后你选择要使用的加密类型。这可以是手动的或使用 IKE，让`racoon`自动管理加密和身份验证过程。

然后你将配置本地和远程连接，首先从本地设置开始。对于主机到主机连接，你只需输入远程主机的 IP 地址。对于 VPN，你需要输入本地和远程网络的相应地址。对于本地网络，你需要输入本地网络的 IP 地址、本地网络的网关计算机以及本地网络的网络掩码。对于远程 VPN 连接，你需要远程 IP 地址、远程网络的地址、其网络掩码和其网关地址。最后，你将输入身份验证密钥。单击 Generate 按钮来创建一个。

最终屏幕将显示你的条目。单击 Apply 以保存它们。你的连接将出现在 IPsec 面板中，显示其类型、目标和昵称。要建立连接，请选择 IPsec 连接并单击 Activate。这将运行`/etc/sysconfig/network-scripts`目录，该目录将执行`setkey`和`racoon`等 IPsec 工具以建立你的连接。配置数据将保存在`/etc/sysconfig/networking/devices`目录中，使用 IPsec 连接的名称。例如，myipsec IPsec 连接的配置信息保存在`ifcfg-myipsec`文件中。每个连接对应的密钥保存在 keys 文件中，包括`keys-myipsec`。以下是 VPN 的示例配置。IKE 方法为预共享密钥 (PSK)。目标（远程）网关为 10.0.0.1，源（本地）网关为 192.168.0.1。目标（远程）网络地址为 10.0.0.0/24，源（本地）地址为 192.168.0.0/24。目标主机为 10.0.0.2。

```
ONBOOT=no
IKE_METHOD=PSK
DSTGW=10.0.0.1
SRCGW=192.168.0.1
DSTNET=10.0.0.0/24
SRCNET=192.168.0.0/24
DST=10.0.0.2
TYPE=IPSEC
```

## 使用 setkey 配置连接

要配置你的 IPsec 连接，可以使用`setkey`工具。该工具包含用于管理 IPsec 策略和安全数据库中规则的多个指令。你使用`add`指令向安全数据库 (SAD) 添加安全关联，并使用`spadd`指令向策略数据库 (SPD) 添加策略。`ah`术语表示该指令应用于身份验证头 (AH)，而`esp`表示由加密安全有效载荷 (ESP) 实现的加密。要实现`setkey`操作，最好使用调用`setkey`并带`-f`选项的脚本，并列出`setkey`指令。以下示例创建了一个简单的脚本，以为特定连接添加身份验证和加密指令，以及为其创建安全策略：

```
#!/sbin/setkey -f
add 192.168.0.2 192.168.0.5 ah 15700 -A hmac-md5 "secret key";
```

```
add 192.168.0.2 192.168.0.5 esp 15701 -E 3des-cbc "secret key ";
spdadd 192.168.0.2 192.168.0.5 any -P out ipsec
esp/transport//require
ah/transport//require;
```

## 安全关联：SA

你使用安全关联来指示你希望对身份验证头 AH 和加密有效载荷 ESP 进行加密。特定连接，例如两个主机之间的连接，可以使用指定的加密方法和指定的密钥对其身份验证头进行加密。对加密有效载荷，即传输的主要内容，也可以这样做。密钥可以通过手动确定或使用密钥交换自动确定。以下示例指定对于 192.168.0.2 和 192.168.0.5 之间的连接，将使用 hmac-md5 身份验证方法和一个密钥 对身份验证头 ah 使用，这里用占位符 secret key 表示。

```
add 192.168.0.2 192.168.0.5 ah 15700 -A hmac-md5 "secret key";
```

加密有效载荷的安全关联使用 3des-cbc 加密方法和不同的密钥。

```
add 192.168.0.2 192.168.0.5 esp 15701 -E 3des-cbc "secret key";
```
