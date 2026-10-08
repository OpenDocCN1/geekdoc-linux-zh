
```
# gpg --sign-key "Red Hat"
pub 1024/CAB2B2F9 created: 1996-02-20 expires: never trust: -q
(1) Richard Peterson <richard@redhat.com>
pub 1024/CAB2B2F9 created: 1996-02-20 expires: never trust: -q
Fingerprint: 6D 9C BA5D 69 52 06 23 45 76 43 FE 4 FB 50
Red Hat Software, Inc. <redhat@redhat.com>
```

你确定要用你的密钥对此密钥签名吗："Richard Peterson (author) <richulp@turtle.mytrek.com>

确定要签名吗？yes

你需要一个密码来解锁用户 "Richard Peterson (author) <richulp@turtle.mytrek.com" 的私钥

1024-bit dsa key, ID 73F0A73C, created 2001-09-26

ter passphrase:

#

```

## 检查 RPM 软件包

一旦拥有了密钥，你可以可以使用 `rpm` 命令和 `-K` 选项检查 Red Hat RPM 软件包的有效性。以下示例检查了 xdsort 和 balsa 软件包的有效性：

```
# rpm -K xdsort-0.98alpha9-1.1386.rpm

xdsort-0.98alpha9-1.1386.rpm: md5 OK

# rpm -K balsa-1.1.7-1.1386.rpm

balsa-1.1.7-1.1386.rpm: md5 OK
```

许多以压缩归（.tar.gz 或 tar.bz2）形式存在的软件软件包将通过以 .asc 或 .sig 结尾的独立文件提供签名。若要检查这些签名，请使用 `gpg` 命令并配合 `--verify` 选项。例如，最近的 sendmail 软件包以压缩归 .tar.gz 的形式分发。其数字签名在一个单独的 .sig 文件中提供。你首先需要从 Sendmail 网站下载并安装 sendmail 软件的公钥。

```
# gpg --import sendmail.asc
```

你应该对 Sendmail 公钥进行签名。（等待，OCR 文本在这里似乎变得重复或碎片化，但遵循所提供的文本流）：你应该对 Sendmail 公钥进行签名。你应该对 Sendmail 公钥进行签名。你应该对 Sendmail 公钥进行签名。你应该对 Sendmail 公钥进行签名。你应该对 Sendmail 公钥进行签名。你应该对 Sendmail 公钥进行签名。你应该对 Sendmail 公钥进行签名。（注意：文本后半部分包含大量的 OCR 伪迹）。

## 入侵检测：Tripwire

当有人入侵系统时，他们通常会尝试通过更改文件来获取控制。检测此类活动的方法是使用 Tripwire。AIDE（入侵检测）是 Tripwire 的替代方案。Red Hat 未包含。

完整性检查工具的工作原理是为每个文件创建一个标识数据库。这些标识可以权限和文件大小，更重要的是算法生成的校验和。实际上，加密值被称为签名。通过重新生成标识并与之前生成的值进行匹配，定期检查文件。任何差异都会记录为文件更改，Tripwire 会通知你。

你还可以检查日志文件是否有可疑活动。请参见第 27 章。`var/log/messages` 对于用户登录、FTP 连接和超级用户登录特别有用。

# 第 17 章：IP 安全协议：IPsec

## 概述

IP 安全协议 `IPsec` 直接将传输安全集成到网协议（IP）中。`IPsec` 已集成到新的 IPv6 协议。它可以适用于旧的 IPv4 协议（参见第 38 章）。`IPsec` 提供了加密和验证目标主机或网络的方法。该过程可以手动处理，也可以使用 IPsec racon 密钥交换工具自动处理。通过 `IPsec`，内核可以自动检测并密传入的，以及加密发出的传输。人们还可以使用 `IPsec` 实现虚拟专用网络，从一个本地网络到另一个本地网络加密数据。

目前多个项目提供了 `IPsec` 工具的开发和实现。原始 `IPsec` 工具由 KAME 项目提供，www.kame.net。当前版本可以从 sourceforge.net/projects/ipsectools 获取。其他 `IPsec` 项目工具包括位于 www.freeswan.org 的自由安全广域网项目 (FreeS/WAN)，它提供了 `IPsec` 工具的 Linux 实现，以及位于 www.vpnc.org 的 VPN Consortium (VPNAC)，它支持 Windows 和 Macintosh 版本。FreeS/WAN 为其工具提供了 Red RPM 软件包和源代码。

注意

目前，Fedora Core 不包含 `IPsec` 工具的支持，但后续版本将包含。`redhat-config-network` 工具包含 `IPsec` 支持的面板，但你需要安装 `IPsec` 工具来激活此支持。

## IPsec 协议

`IPsec` 由多个协议组成，提供身份验证（AH）、加密（ESP）以及加密密钥的安全交换（IKE）。认证头协议（AH）确认数据包是由发送者发送的，而非他人。`IPsec` 还包含完整性检查，用以检测传输过程中的任何篡改。数据包使用封装安全负载（ESP）进行加密。加密和解密使用发送者和接收者共享的秘密密钥执行。这些密钥本身通过互联网密钥交换协议（IKE）传输，该协议提供了安全的交换。ESP 加密可能会降低某些压缩传输方法（例如用于拨号上网连接的 PPP）。为了适应这些压缩方法，`IPsec` 提供了 IP 负载压缩协议（IPComp），可以在发送前对数据包进行压缩。

AH、ESP 和 IPComp 协议已集成 Linux 内核。IKE 协议作为一个独立的守护进程实现。它仅提供了一种共享密钥的方法，并可以使用其他共享方法替换。

# IPsec 模式

你可以将 `IPsec` 功能用于普通传输或数据包隧道。在普通传输中，数据包被加密并发送到下一个目的地。普通传输模式用于实现直接的主机到主机加密，每个主机都处理 `IPsec` 加密过程。数据包隧道用于加密网关之间的传输，让网关处理针对或源自整个网络的流量的 `IPsec` 加密过程，而无需为每个主机配置 `IPsec`。在数据包隧道中，数据包被封装了带有特定目的的新头部，使你能够实现虚拟专用网络（VPN）。数据包被导向 VPN 网关，由网关加密并发送本地网络数据包。

注意

你可以选择对某些主机的数据包加密，或对通过特定端口的数据包进行加密。

# IPsec 安全数据库

你选择加密的数据包由 `IPsec` 安全策略数据库（SPD）指定。你用于加密它们的方法由 `IPsec` 安全关联数据库（SAD）决定。SAD 将加密方法和密钥与特定的连接或类型的连接关联起来。需要加密的连接在安全策略数据库中指定。

# IPsec 工具

提供了若干 `IPsec` 工具，可以通过这些工具管理 `IPsec` 连接（见表 17-1）。你构建的 `libipsec` 工具建立了一个密钥库。使用 `setkey`，你可以管理策略数据库和关联数据库。`racoon` 工具配置密钥交换过程，以实现跨连接的安全解密密钥。要查看 SPD 数据库中当前的安全策略，可以使用 `setkey-DP`。对于 SPD 中的安全关联，你可以使用 `setkey-SP`。

> 注意

要在内核中启用 `IPsec`，请确保在加密选项（Cryptographic Options）中启用 PF_KEY、AH 和 ESP 选项。

表 17-1：IPsec 工具

| 工具 | 说明 |
| --- | --- |
| libipsec | 构建 PFkey |
| setkey | 管理策略 (SPD) 和关联 (SAD) 数据库 |
| racoon | 使用 IPsec 密钥交换 (IKE) 配置并实现安全密钥交换 |
| setkey-SP | 查看 SAD 数据库中的安全关联 |
| setkey-DP | 查看 SPD 数据库中的安全策略 |

# IPsec 与 IP Tables

IPTables 过滤会停止所有 IPsec 数据包。要让 IPTables 通过 IPsec 数据包，请使用以下 `iptables` 命令。AH 协议数字 51，ESP 协议为 50。为了允许 IPsec 数据包，你应该设置如下策略规则。

```
iptables -A INPUT -p 50 -j ACCEPT

iptables -A OUTPUT -p 51 -j ACCEPT
```

# 使用 redhat-config-network 配置 IPsec

`redhat-config-network` 工具提供了实现 `IPsec` 连接的支持。在 `redhat-config-network` 工具上，选择 IPsec 面板（见图 17-1）并点击“New”（新建）以启动创建 `IPsec` 连接的设置向导。首先你被要求为连接输入别名，并指定其是否自动启动。然后选择连接类型。可以是直接到主机的连接，也可以是两个网络之间的连接。网络连接实现私有网络（VPN），且 `IPsec` 在隧道模式下运行。（主机和 VPN 连接在随后的章节中都有描述。）然后你选择想要使用的身份验证类型。可以是手动管理，也可以使用 IKE、raccoon。

图 17-1：redhat-config: network 上的 IPsec

随后，你将配置本地和远程连接，从本地设置开始。对于主机到主机连接，你只需要输入远程主机的 IP 地址。对于 VPN，你将为本地和远程网络输入相应的地址。对于本地网络，你需要输入本地网络的 IP 地址、网络的网关计算机以及本地网络的掩码。对于远程 VPN 连接，你需要输入远程 IP 地址、远程网络地址、其掩码和网关地址。最后，你将输入身份密钥。点击“Generate”（生成）按钮创建一个。

最后一个屏幕将显示你的输入。点击“Apply”（应用）保存。你的连接将出现在 IPsec 面板中，显示其类型、目的地和别名。要建立连接，选择 IPsec 连接并点击 Activate（激活）。这将运行 `/etc/sysconfig` 中的 ip-sec 脚本。配置位于 `/etc/sysconfig/IPSec.conf`。

```bash
/etc/sysconfig/IPSec.conf

config

    protostack = yes

    keymgr = yes

    setup = /etc/init.d/ipsec

    stop = /etc/init.d/ipsec

    restart = /etc/init.d/ipsec

    conn myvpn

        localaddr = 192.168.1.1

        remoteaddr = 192.168.2.1

        encapsulation = tunnel

        mode = v2

        encrypt = aes-256

        auth = sha1

        psk = mysecret
```

# 使用 setkey 配置连接

要配置 `IPsec`，你可以使用 `setkey`。以下示例创建一个简单的身份验证和加密脚本：

```bash
#!/bin/bash

setkey -f

add 192.168.1.1 192.168.2.1 15700 -A hmac-md5 "secret key"

add 192.168.1.1 192.168.2.1 15701 -E 3des-cbc "secret key"

spadd 192.168.1.1 192.168.2.1 15700 -p ah -s

spadd 192.168.1.1 192.168.2.1 15701 -p esp -s
```

# 安全关联：SA

安全关联表示你需要认证头（AH）和加密负载。特定的连接（如两个主机之间）可以有特定的加密方法和指定的密钥。加密负载也是如此。密钥可以手动指定或使用 `setkey` 自动生成。以下示例指定对于 192.168.1.1 和 192.168.2.1 之间的连接，使用 hmac-md5 认证方法和密钥（由占位密钥指定）用于认证头 ah。

```
add 192.168.1.1 192.168.2.1 15700 -A hmac-md5 "secret key"
```

加密负载的安全关联使用 3des-cbc 加密方法和不同的密钥。

```
add 192.168.1.1 192.168.2.1 15701 -E 3des-cbc "secret key"
```

每个指令都用安全参数索引（SPI）标识，在本例中为 15700 和 15701。事实上，具有不同 SPI 的相同指令被视为不同的指令。

# 安全策略：SP

安全策略将为连接实现 `IPsec` 安全过程。你可以指定主机或端口连接。一旦为连接设置了策略，内核将使用 SAD 数据库确定应用哪些安全关联。安全策略使用 `spadd` 指令添加。加密、身份验证或两者均可以是要求的。

以下示例将加密并验证主机 192.168.0.2 和 192.168.0.5 之间的传输。这些主机之间的任何出站传输都将经过加密和身份验证。

```
spdadd 192.168.0.2 192.168.0.5 -P out ipsec esp/transport/require
ah/transport/require;
```

在 `spdadd` 指令中，你需要指定此种连接，例如两个主机之间或两个网络之间的连接。对于两个主机，你将使用 IP 地址，在本例中为 192.168.0.2 和 192.168.0.5。然后你指定数据包类型，在本例中为任何出站数据包 `-P out`。接着，你可以为 ESP 或 AH 协议（或两者）指定 ipsec 指令。对于每个条目，你指定模式（传输模式 transport 或隧道模式 tunnel）、涉及的主机（可以是隧道模式）以及加密策略（通常为 require）。接下来的示例显示，ESP 协议将在 192.168.0.2 和 192.168.0.5 之间的连接中使用传输模式，并且是强制要求的。

```
esp/transport/192.168.0.2-192.168.0.5/require
```

如果主机相同（如上一个示例所示），你可以省略主机。
```
esp/transport/require
```

## 接收主机

为了让主机接收加密的 IPSec 传输，它必须在自己的 SAD 数据库中拥有相应的安全关联指令，告诉它如何对接收到的指令进行验证和解密。安全关联指令将与发送者的指令镜像，使用相同的加密方法、密钥密钥和安全索引。然而，并不需要相应的策略。

```
#!/sbin/ipset -f

add 192.168.0.2 192.168.0.5 ah 15700 -A hmac-md5 "secret key"

add 192.168.0.2 192.168.0.5 esp 15701 -E 3des-cbc "secret key"
```

接收主机可能需要设置策略以允许安全连接上的入站数据包，丢弃未加密的数据包。以下策略将仅允许来自 192.168.0.2 的入站加密且验证过的 IPSec 传输。

```
spdadd 192.168.0.2 192.168.0.5 any -P in ipsec esp/transport/require
ah/transport/require;
```

## 双向传输

上一个示例在两个主机之间建立了单向安全连接，即从 192.168.0.2 指向 192.168.0.5，而不支持反向（从 192.168.0.5 指向 192.168.0.2）。要实现两个主机之间的双向安全传输，两个主机都需要配置为发送者和接收者，并配有相应的安全关联。以下脚本基于两个主机之间简单双向 IPSec 连接的常见示例。它们在主机 192.168.0.2 和 192.168.0.5 之间建立了双向 IPSec 连接。同时也包含了相应的入站策略，但并非强制要求。

首先是主机 192.168.0.2 的配置：

```
#!/sbin/setkey -f

add 192.168.0.2 192.168.0.5 17000 -A hmac-md5 "secret key";

add 192.168.0.2 192.168.0.5 24500 -A hmac-md5 "secret key";

add 192.168.0.2 192.168.0.5 15701 -E 3des-cbc "secret key";

add 192.168.0.2 192.168.0.5 24501 -E 3des-cbc "secret key";

spdadd 192.168.0.2 192.168.0.5 any -P out ipsec esp/transport/require
ah/transport/require;

spdadd 192.168.0.2 192.168.0.5 any -P in ipsec esp/transport/require
ah/transport/require;
```

对应的主机 192.168.0.5 使用相同的指令，但 IP 连接反反了。注意，每端发送者和接收者指令的安全索引是相互对应的。

```bash
#!/bin/bash -f

add 192.168.0.5 192.168.0.5 15701 -A hmac-md5 "secret key";

add 192.168.0.5 192.168.0.2 24500 -A hmac-md5 "secret key";

add 192.168.0.5 192.168.0.2 15701 -E 3des-cbc "secret key";

add 192.168.0.5 192.168.0.2 24501 -E 3des-cbc "secret key";

spdadd 192.168.0.5 192.168.0.2 any -P out ipsec esp/transport/require
ah/transport/require;
```
