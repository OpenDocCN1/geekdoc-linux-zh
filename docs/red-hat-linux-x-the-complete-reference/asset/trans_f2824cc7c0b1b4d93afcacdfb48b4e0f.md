
## IPsec 安全数据库

您需要加密的数据包由 IPsec 安全策略数据库（SPD）指定。所使用的加密方法由 IPsec 安全关联数据库（SAD）确定。SAD 将加密方法和密钥与特定的连接或某种类型的连接相关联。需要加密的连接在安全策略数据库中进行指定。

## IPsec 工具

提供了几种 IPsec 工具，你可以使用它们来管理 IPsec 连接（参见表 17-1）。`libipsec` 工具允许你构建密钥库。使用 `setkey`，你可以管理策略和关联数据库。`racoon` 工具配置密钥交换过程，以实现跨连接的安全解密密钥交换。要查看当前 SPD 数据库中的安全策略，可以使用 `setkey-DP`。对于 SAD 中的安全关联，可以使用 `setkey-SP`。

注意：要在内核中启用 IPsec，请确保在加密选项中启用 PF_KEY、AH 和 ESP 选项。

表 17-1：IPsec 工具

| 工具 | 描述 |
|---|---|
| libipsec | 构建 PFkey |
| setkey | 管理策略 (SPD) 和关联 (SAD) 数据库 |
| racoon | 配置并实现使用 IPsec 密钥交换 (IKE) 的安全密钥交换 |
| setkey-SP | 检查 SAD 数据库中的安全关联 |
| setkey-DP | 检查 SPD 数据库中的安全策略 |

## IPsec 与 IP 表

IPtables 网络过滤会阻止许多 IPsec 数据包。要让 IPtables 允许 IPsec 数据包通过，请使用以下 `IPtables` 命令。AH 协议的编号为 51，ESP 协议的编号为 50。为了允许 IPsec 数据包，你应该设置类似下面的策略规则。

```
iptables -A INPUT -p 50 -j ACCEPT
iptables -A OUTPUT -p 51 -j ACCEPT
```

## 使用 redhat-config-network 配置 IPsec

redhat-config-network 工具现在支持实施 IPsec 连接。在 redhat-config-network 工具上，选择 IPsec 面板（参见图 17-1）并点击“新建”以启动 IPsec 设置向导来创建 IPsec 连接。首先，你需要为连接输入一个昵称，并指定是否希望自动启动它。然后，你选择连接类型。这可以是直接的主机到主机连接，或者是两个网络之间的连接。网络连接实施虚拟专用网络 (VPN) 并以隧道模式运行 IPsec。（主机和 VPN 连接都在以下章节中有详细说明。）然后，你选择要使用的加密类型。这可以是手动的，或使用 IKE，让 racoon 自动管理加密和认证过程。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_382_0.png)

图 17-1：redhat-config-network 上的 IPsec

然后，你将配置本地和远程连接，从本地设置开始。对于主机到主机的连接，你只需输入远程主机的 IP 地址即可。对于 VPN，你必须为本地和远程网络输入相应的地址。对于本地网络，你需要输入本地网络的 IP 地址、本地网络的网关计算机以及本地网络的网络掩码。对于远程 VPN 连接，你需要远程 IP 地址、远程网络的地址、其网络掩码及其网关地址。最后，你输入认证密钥。点击“生成”按钮创建一个。

最后一个屏幕将显示你的输入。点击“应用”以保存它们。你的连接将显示在 IPsec 面板中，显示其类型、目的地和昵称。要建立连接，选择 IPsec 连接并点击“激活”。这将运行 /etc/sysconfig/network-scripts 目录中的 ifup-ipsec 脚本，该脚本将执行 setkey 和 racoon 等 IPsec 工具来建立你的连接。配置数据将保存在 /etc/sysconfig/networking/devices 目录中，使用 IPsec 连接的名字。例如，mypsec IPsec 连接的配置信息保存在 ifcfg-mypsec 文件中。每个连接的相应密钥保存在 keys 文件中，包括 keys-mypsec。这里显示了一个 VPN 的示例配置。IKE 方法是私有共享密钥 (PSK)。目的地（远程）网关是 10.0.0.1，源（本地）网关是 192.168.0.1。目的地（远程）网络地址是 10.0.0.0/24，源（本地）地址是 192.168.0.0/24。目的地主机是 10.0.0.2。

```
ONBOOT=no
IKE_METHOD=PSK
DSTCGW=10.0.0.1
SRCGW=192.168.0.1
DSTNET=10.0.0.0/24
SRCNET=192.168.0.0/24
DST=10.0.0.2
TYPE=IPSEC
```

![](img/32a48d8db4c23e6e2eb70d1e5034c976_383_0.png)

## ABC Amber CHM 转换器试用版

请注册以移除此横幅。

http://www.processestext.com/abchm.html

## 使用 setkey 配置连接

要配置你的 IPsec 连接，你可以使用 setkey 工具。该工具包含若干用于管理 IPsec 策略和安全数据库规则的指令。你使用 add 指令向安全数据库 (SAD) 添加安全关联，使用 spdadd 指令向策略数据库 (SPD) 添加策略。ah 术语表示该指令应用于认证头 (AH)，esp 表示由加密安全载荷 (ESP) 实施的加密。为了实施 setkey 操作，最好使用一个脚本，该脚本调用带有 -f 选项的 setkey 并列出 setkey 指令。以下示例创建一个简单的脚本，用于为特定连接添加认证和加密指令，并为其创建安全策略：

```
#!/sbin/setkey -f
add 192.168.0.2 192.168.0.5 ah 15700 -A hmac-md5 "secret key";
add 192.168.0.2 192.168.0.5 esp 15701 -E 3des-cbc "secret key ";
spdadd 192.168.0.2 192.168.0.5 any -P out ipsec
    esp/transport//require
    ah/transport//require;
```

## 安全关联：SA

你使用安全关联来指示你希望认证头 (AH) 和加密载荷 (ESP) 被加密。特定的连接，例如两个主机之间的连接，可以使用指定的加密方法和指定的秘密密钥对其认证头进行加密。同样，也可以对作为传输主要内容的加密载荷进行相同操作。秘密密钥可以手动确定，也可以使用密钥交换自动确定。以下示例指定对于 192.168.0.2 和 192.168.0.5 之间的连接，认证头 ah 将使用 hmac-md5 认证方法和一个秘密密钥（此处由占位符“secret key”表示）。

```
add 192.168.0.2 192.168.0.5 ah 15700 -A hmac-md5 "secret key";
```

加密载荷的安全关联使用 3des-cbc 加密方法和另一个不同的秘密密钥。

```
add 192.168.0.2 192.168.0.5 esp 15701 -E 3des-cbc "secret key";
```

每个指令都由一个安全参数索引 (SPI) 标识，在本例中为 15700 和 15701。事实上，具有不同 SPI 的相同指令被视为不同的指令。

请记住，安全关联仅指定可能的加密过程。它们并不实施这些过程。为此，你需要设置安全策略。

## 安全策略：SP

安全策略将为连接实施 IPsec 安全过程。你可以指定主机或端口连接。一旦为连接设置了策略，内核将使用 SAD 数据库确定应用哪些安全关联。安全策略通过 spdadd 指令添加。可以要求加密、认证或两者皆有。

以下示例将加密并认证主机 192.168.0.2 和 192.168.0.5 之间的传输。这两个主机之间任何发出的传输都将被加密和认证。

```
spdadd 192.168.0.2 192.168.0.5 any -P out ipsec esp/transport//require ah/transport/require;
```

在 spdadd 指令中，你需要指定连接，例如两个主机或两个网络之间的连接。对于两个主机，你会使用它们的 IP 地址，在本例中为 192.168.0.2 和 192.168.0.5。然后你指定数据包类型及其方向，在本例中为任何发出的数据包，any -P out。然后

