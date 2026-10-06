
> 您应该在正在配置的实际机器上执行以下操作。避免尝试从远程配置和建立 IPsec 连接。

1. 在命令行 shell 中，输入 `system-config-network` 启动网络管理工具。

2. 在 IPsec 标签页，点击 `New`（新建）启动 IPsec 配置向导。

3. 点击 `Forward`（下一步）开始配置主对主机 IPsec 连接。

4. 为连接输入唯一名称，例如 `ipsec0`。如果需要，勾选框以便在计算机启动时自动激活连接。点击 `Forward`（下一步）继续。

5. 选择 `Host to Host encryption`（主机对主机加密）作为连接类型，然后点击 `Forward`（下一步）。

6. 选择要使用的加密类型：手动或自动。

如果您选择手动加密，则在过程后期必须提供加密密钥。如果您选择自动加密，则由 `racoon` 守护进程管理加密密钥。如果您想使用自动加密，必须安装 `ipsec-tools` 软件包。

点击 `Forward`（下一步）继续。

7. 输入远程主机的 IP 地址。

要确定远程主机的 IP 地址，请**远程主机上**使用以下命令：

```
[root@myServer ~]# /sbin/ifconfig <device>
```

其中 `<device>` 是您想用于 VPN 连接的以太网设备。

如果系统中仅存在以太网卡，设备名称通常为 `eth0`。一个示例显示了此命令的相关信息（注意这仅为示例输出）：

eth0 |

| :--- |

| Link encap:Ethernet Hwaddr 00:0C:6E:EB:98:1D |

| inet addr:172.16.44.192 Bcast:172.16.45.255 Mask:255.255.254.0 |

IP 地址是 `inet addr:` 标签后的数字。

> 注意

> 对于主机对主机连接，两台主机都应该具有公共的可路由地址。或者，两台主机都可以具有私有的、不可路由地址（例如 `10.x.x.x` 或 `192.168.x.x` 范围），只要它们处于同一个局域网内。

如果主机位于不同的局域网，或其中一个有公共地址另一个有私有地址，请参阅第 2.7.7 节“IPsec 网络对网络配置”。

8. 如果在 `6` 中选择了手动加密，请指定要使用的加密密钥，或点击 `Generate`（生成）创建一个。

a. 指定身份验证密钥或点击 `Generate`（生成）生成一个。它可以是数字和字母的任意组合。

b. 点击 `Forward`（下一步）继续。

9. 验证 `IPsec — Summary` 页面上的信息，然后点击 `Apply`（应用）。

10. 点击 `File = Save`（文件 = 保存）保存配置。

可能需要重启网络使更改生效。要重启网络，请使用以下命令：

```
[root@myServer ~]# service network restart
```

11. 从列表中选择 IPsec 连接并点击 `Activate`（激活）按钮。

12. 对另一台主机重复整个过程。在其他主机上使用与步骤 `8` 相同的密钥至关重要。否则，IPsec 将无法工作。

配置 IPsec 连接后，它将出现在 IPsec 列表中，如图 2.10“IPsec 连接”所示。

# 第 2 章 保护您的网络

![](img/41d4f31e0edc30c079027fe8eaac3a44_111_0.png)

图 2.10. IPsec 连接

当配置 IPsec 连接时，会创建以下文件：

- `/etc/sysconfig/network-scripts/ifcfg-<nickname>`
- `/etc/sysconfig/network-scripts/keys-<nickname>`
- `/etc/racoon/remote-conf`

如果选择了自动加密，`/etc/racoon.conf` 将被修改。

当接口启动时，`/etc/racoon.conf` 将被修改。

## 2.7.6.2. 手动 IPsec 主对主机配置

创建 IPsec 连接的第一步是收集主机的系统和网络信息。对于主对主机连接，您需要：

- 每个主机的 IP 地址
- 唯一名称，例如 `ipsec1`。这用于识别 IPsec 连接并将其区分。
- 固定加密密钥或由 `racoon` 自动生成的密钥。
- 会话期间使用的身份验证。

### 主对主机配置

例如，假设工作站 A 和工作站 B 通过 IPsec 隧道连接彼此。它们想使用预共享密钥连接，让 `racoon` 自动生成身份验证密钥。用户决定将连接命名为 `ipsec1`。

> 注意

> 您应该选择包含大小写字母、数字和符号的 PSK。易猜的 PSK 会构成安全风险。

不需要为每个主机使用相同的连接名称。选择一个方便且有意义的名称。

以下是工作站 A 与工作站 B 连接的主对主机 IPsec 配置。示例中标识连接的唯一名称为 `ipsec1`，因此生成的文件为 `/etc/sysconfig/network-scripts/ifcfg-ipsec1`。

```
DST=X.X.X.X TYPE=IPSEC
ONBOOT=no
IKE_METHOD=PSK
```

对于工作站 A，`X.X.X.X` 是工作站 B 的 IP 地址。对于工作站 B，`X.X.X.X` 是工作站 A 的 IP 地址。此连接在启动时不启动（`ONBOOT=no`），并且它使用预共享密钥进行身份验证（`IKE_METHOD=PSK`）。

以下是预共享密钥文件（称为 `/etc/sysconfig/network-scripts/keys-ipsec1`）的内容，两台工作站都需要它进行身份验证。该文件的内容在两台工作站上应该是相同的，并且只有 root 用户可以读写此文件。

> 重要

> 要更改 `keys-ipsec1` 文件以便只有 root 用户读取，在创建文件后使用以下命令：

```
[root@myServer ~]# chmod 600 /etc/sysconfig/network-scripts/keys-ipsec1
```

身份验证密钥可以随时更改，编辑两台工作站上的 `keys-ipsec1` 文件。身份验证密钥必须相同以确保连接。

下一个示例显示了与根主机建立阶段 1 连接的特定配置。文件名为 `X.X.X.X.conf`，其中 `X.X.X.X` 是远程 IPsec 主机的 IP 地址。注意，此文件在 IPsec 隧道激活时自动生成，不应进行编辑。

```
remote X.X.X.X{
  exchange_mode aggressive;
  my_identifier address;
  proposal (
```

# 第 2 章 保护您的网络

```text
encryption_algorithm 3des;
hash_algorithm sha1;
authentication_method pre_shared_key;
dh_group 2;
}
```

当 IPsec 连接初始化时，创建的默认阶段 1 配置文件包含 Fedora IPsec 实现中使用的以下语句：

`remote X.X.X.X`

指定此配置文件的后续段仅适用于由 `X.X.X.X` IP 地址标识的远程节点。

`exchange_mode aggressive`

Fedora 上 IPsec 的默认配置使用激进认证模式（aggressive authentication mode），这在降低连接开销的同时，允许为具有多个主机的多个 IPsec 连接进行配置。

`my_identifier address`

指定在身份验证节点时使用的标识方法。Fedora 使用 IP 地址来识别节点。

`encryption_algorithm 3des`

指定身份验证期间使用的加密算法。默认情况下使用三重数据加密标准 (3DES)。

`hash_algorithm sha1:`

指定节点之间阶段 1 协商期间使用的哈希算法。默认情况下使用版本 1 哈希算法。

`authentication_method pre_shared_key`

指定节点协商期间使用的认证方法。默认情况下，Fedora 使用共享密钥进行认证。

`dh_group 2`

指定用于建立动态生成会话密钥的 Diffie-Hellman 组号。默认使用 modp1024 (group 2)。

## 2.7.6.2.1. Racoon 配置文件

`/etc/racoon/racoon.conf` 文件在所有 IPsec 节点上应该是相同的，但 `include "etc/racoon/X.X.X.X.conf"` 语句除外。该语句（以及文件引用）在 IPsec 隧道激活时生成。对于 Workstation A，`include` 中的 `X.X.X.X` 是 Workstation B 的 IP 地址。对于 Workstation B，情况则反之。以下显示了 IPsec 连接激活时典型的 `racoon.conf` 文件。

```text
# Racoon IKE 守护进程配置文件。
# 请参见 'man racoon.conf' 以获取格式和条目的描述。
path include "/etc/racoon";
path pre_shared_key "/etc/racoon/psk.txt";
path certificate "/etc/racoon/certs";
```

```text
sainfo anonymous
{
```

## IPSec 主机对主机配置

```text
pfs_group 2;
lifetime 1 hour ;
encryption_algorithm 3des, blowfish 448, rijndael;
authentication_algorithm hmac_sha1, hmac_md5;
compression_algorithm deflate;
}
```

`include "/etc/racoon/X.X.X.conf";`

默认的 `racoon.conf` 文件包含了为 IPsec 配置、预共享密钥文件和证书定义的路径。`sainfo anonymous` 中的字段描述了 IPsec 节点之间的阶段 2 SA（安全关联））——IPsec 连接的性质（包括使用的支持加密算法）以及密钥交换方法。以下列表定义了阶段 2 的字段：

`sainfo anonymous`

表示可以与任何提供匹配 IPsec 凭据的对端匿名初始化 SA。

### pfs_group 2

定义 Diffie-Hellman 密钥交换协议，决定了 IPsec 节点在 IPsec 连接阶段使用临时会话密钥的方法。默认情况下，Fedora IPsec 实现使用 Diffie-Hellman 加密密钥组的组 2（或 modp1024）。组 2 使用 1024 位模幂运算，即使私钥被泄露，也能防止攻击者解密之前的 IPsec 事务。

### lifetime 1 hour

此参数指定 SA 的生存周期，可以用小时或数据字节来量化。Fedora IPsec 的默认实现指定了一小时生存周期。

### encryption_algorithm 3des, blowfish 448, rijndael

指定阶段 2 支持的加密密码算法。Fedora 支持 3DES、448 位 Blowfish 和 Rijndael（高级加密标准 AES 中使用的密码算法）。

### authentication_algorithm hmac_sha1, hmac_md5

列出用于认证的支持的哈希算法。支持的模式为 sha1 和 md5 哈希消息认证码 (HMAC)。

### compression_algorithm deflate

定义用于 IP 载荷压缩 (IPCOMP) 支持的压缩算法，这允许在慢速连接上更快地传输 IP 报文。

要启动连接，请在每个主机上使用以下命令：

```bash
[root@myServer ~]# /bin/ifup <nickname>
```

`<nickname>` 是您为 IPsec 连接指定的名称。

要测试 IPsec 连接，运行 `tcpdump` 工具以验证主机之间传输的网络数据包，并验证它们已通过 IPsec 加密。数据包应包含 AH 头以及 ESP 报文。ESP 意味着它是被加密的。例如：

```bash
[root@myServer ~]# tcpdump -n -1 eth0 host <targetSystem>
IP 172.16.45.107 > 172.16.44.192: AH(spi=0x0954ccb6,seq=0xbbb): ESP(spi=0x0c9f2164,seq=0xbbb)
```

# 第 2 章 保护您的网络

## 2.7.7. IPsec 网络到网络配置

IPsec 也可以配置为通过网络到网络连接将整个网络（如 LAN 或 WAN）连接到远程网络。网络到网络连接需要在连接的网络的每侧设置 IPsec 路由器，以透明地处理从 LAN 上的节点到远程 LAN 上的节点的路由信息。图 2.11 “网络到网络 IPsec 隧道连接”显示了一个网络到网络的 IPsec 隧道连接。

![](img/41d4f31e0edc30c079027fe8eaac3a44_115_0.png)

图 2.11. 网络到网络的 IPsec 隧道连接

此图显示了两个由互联网隔开的独立 LAN。这些 LAN 使用 IPsec 路由器通过互联网上的安全隧道进行认证并启动连接。在传输过程中被截获的数据包需要通过暴力解密才能破解保护 LAN 之间数据包的密码。从 `192.168.1.0/24` 范围内的一个节点到另一个节点的通信过程对节点来说是完全透明的，因为 IPsec 数据包的处理、加密/解密和路由完全由 IPsec 处理。

网络到网络的 IPsec 关需要：

- 用于 IPsec 配置的 IPsec 路由器的公网 IP 地址
- 局域网范围
- 用于 IPsec 的网关
- 固定加密密钥或自动生成的密钥
- 在会话期间使用的认证密钥

### 2.7.7.1. 网络到网络 (VPN) 连接

网络到网络的 IPsec 连接使用两个 IPsec 路由器，每个网络一个，通过其路由 `192.168.2.0/24` 子网。

# IPsec 网络到网络配置

需要公网 IP 地址以及连接到各自私有网络的以太网设备。

![](img/41d4f31e0edc30c079027fe8eaac3a44_116_0.png)

图 2.12. 配置

使用以下步骤配置网络到网络的 IPsec 连接：

1. 在命令终端中运行 `system-config-network` 以启动**网络管理工具**。

2. 在 `IPsec` 选项卡上，点击 `New` 开始 IPsec 配置向导。

3. 点击 `Forward` 开始配置网络到网络的 IPsec 连接。

4. 为连接输入唯一名称，例如 `ipsec0`。如果需要，勾选选框在计算机启动时自动激活连接。点击 `Forward` 继续。

5. 选择 `Network to Network encryption (VPN)` 作为连接类型，然后点击 `Forward`。

6. 选择要使用的加密类型：手动或自动。

如果选择手动加密，必须在过程后期提供加密密钥。如果选择自动加密，则由 `racoon` 守护进程管理加密。如果想使用自动加密，则必须安装 `ipsec-tools` 软件包。

点击 `Forward` 继续。

7. 在 `Local Network` 页面上，输入以下信息：

- `Local Network Address` — 连接到私有网络的 IPsec 路由器上的设备 IP 地址。
- `Local Subnet Mask` — 本地网络 IP 地址的子网掩码。
- `Local Network Gateway` — 私有网络的网关。

```

## 第 2 章 保护您的网络

![](img/41d4f31e0edc30c079027fe8eaac3a44_117_0.png)

图 2.13 本地网络信息

- 8. 在“远程网络”（Remote Network）页面上，输入以下信息：
  - `远程 IP 地址 (Remote IP Address)` — 另一个私有网络的 IPsec 路由器的公可用 IP 地址。在示例中，对于 `ipsec0`，输入 `ipsec1` 的公可用 IP 地址，反之亦然。
  - `远程网络地址 (Remote Network Address)` — 另一个 IPsec 路由器后私有子网的网络地址。在示例中，配置 `ipsec1` 时，输入 `192.168.1.0`；配置 `ipsec0` 时，输入 `192.168.2.0`。
  - `远程子网掩码 (Remote Subnet Mask)` — 远程 IP 地址的子网掩码。
  - `远程网络网关 (Remote Network Gateway)` — 远程网络的网关 IP 地址。
  - 如果在第 6 步中选择了手动加密，请指定要使用的加密密钥，或点击**生成（Generate）**创建一个。

指定一个身份密钥或点击**生成（Generate）**生成一个。该密钥可以是数字和字母的任意组合。

点击**向前（Forward）**继续。

![](img/41d4f31e0edc30c079027fe8eaac3a44_118_0.png)

9. 验证 IPsec — 摘要（Summary）页面上的信息，然后点击“应用（Apply）”。

10. 选择 文件（File）=> 保存（Save）以保存配置。

11. 从列表中选择 IPsec 连接，然后点击“激活（Activate）”以激活连接。

12. 启用 IP 转发：
  a. 编辑 `/etc/sysctl.conf` 并将 `net.ipv4.ip_forward` 设置为 `1`。
  b. 使用以下命令启用更改：

```
[root@myServer ~]# /sbin/ipsec -p /etc/sysctl.conf
```
