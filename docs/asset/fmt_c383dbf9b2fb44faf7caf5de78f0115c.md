
```
Key fingerprint = 0A 16 68 8B FD D9 0F 01 ID EF 08 AD 12 53 64 6E C
```

易读性确认：根据你的直接第一手知识，你是否绝对确定已准备好庄重承诺，上述公钥确实属于上述用户 ID 所指定的的用户 (y/N)？y

你需要一个短语来解锁你的私钥。

用户 ID "`nancy@example.com`" 的密钥

输入短语：

短语正确

最后，Nancy 现在可以使用 `ppg -ea` 使用 Joe 的公钥加密文件（`a` 是必要的，将加密文件存储为 ASCII 格式以便通过电子邮件传输）。`ppg -ea` 的语法如下：

`ppg -ea file userid [other users]`

如果 Nancy 想要加密每条消息，用 Joe 的公钥加密的命令看起来像这样：

```bash
pgp -ea message joeuser@example.com
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
```

# 第13 章 实现系统安全

使用了 RSAREF(tm) Toolkit，版权归 RSA Data Security, Inc. 所有。

该软件的导出可能受到美国政府的限制。

接收者的公钥将用于加密。

用户 ID 的密钥：Joe User <joeuser@example.com>

1024 位 DSS 密钥，密钥 ID `0CA38C5D0`，创建于 2002/04/20

传输装甲文件：message.asc

加密后的文件存储在 `message.asc` 中，其格式如下：

```
--- BEGIN PGP MESSAGE ---
Version: PGP 6.5.8
QAN1RDBE4DL509YCrvxQBAQ6/s0xizuenQ+Y7e2Ij3JQ0C9gecuUwboSBi4
G5N4B81p4F3ZL3u00KZt44pA2ulIFGkhzthuuyY8SAYJokKMF400pgn5mtP
Y1JB5A689Y71f17M9uAELK+kqtIGHYpJpauVv01ss38Yw7Hcd0b6dpl1gc4+cx
CCZNPGQ022XhI4FXRAE1Qub4D1Y2RAWW86HK69YwaXRfGPUSC3siJs16
JApKmIMQgN45g5ffipYk15axWI5knf1Te65S3YUR4a908f6Jb7EY/Q+L1kDG8
GyukltUA/Q2WIFFAXRI3BYXVYwLznkf1Te65SR9rwGy5hZ59yrhu5UJ9TZCL+bLIN1T9w40QibBuEI3XIa
C14MgowGpcfpkBBRGI4M55Nhm9iF50CguGh5Qhm3Mr321JnU0Y3BH4+40QibEu3XIa
N67iYEFJ3LB14/cr12/YTvVsek9w4R9055cltXv4
```

易读性确认：根据你的直接第一手知识，你是否绝对确定已准备好庄重承诺，上述公钥确实属于上述用户 ID 所指定的的用户 (y/N)？y

你需要一个短语来解锁你的私钥。

用户 ID "`nancy@example.com`" 的密钥

输入短语：

短语正确

最后，Nancy 现在可以使用 `ppg -ea` 使用 Joe 的公钥加密文件（`a` 是必要的，将加密文件存储为 ASCII 格式以便通过电子邮件传输）。`ppg -ea` 的语法如下：

Pretty Good Privacy(tm) Version 6.5.8

(c) 1999 Network Associates Inc.

Uses the RSAREF(tm) Toolkit, which is copyright RSA Data Security, Inc.

Export of this software may be restricted by the U.S. government.

# 了解更多 VPN

VPN 可能非常难以理解和实现，因此建议进一步阅读。网站 `http://www.vpnlabs.org` 提供了 VPN 技术、产品和实现问题的全面概述。

# 其他身份验证方法

身份验证代表了大多数机构中最显著的安全漏洞。许多网站只需要用户名和密码进行用户身份验证，这对于大多数网站来说已经足够了。然而，当你考虑到某人猜中密码、嗅探网络连接，甚至只是在你输入密码时从你背后窥视有多简单，就会很快理解用户名和密码绝不是最安全的认证机制。

Unix 与大多数操作系统一样，能够支持替代身份验证方法。本节记录了实践中一些常用的方法。

# 可插拔认证模块 (PAM)

Red Hat Linux、HP-UX 和 Solaris 支持可插拔认证模块，或 PAM。PAM 将认证机制与应用程序代码分离，这样你就可以在不更改任何代码的情况下更改用户认证的方式。认证代码以共享对象的形式出现，并由应用程序动态加载。一个名为 `pam.conf` 的配置文件控制哪些认证机制与哪些应用程序关联。本章本节记录的许多功能都可以作为 PAM 模块使用。你可以在 `http://www.sun.com/software/solaris/pam` 了解更多关于 PAM 的信息。

# 一次性密码

当你旅行且无法访问 SSH 或 VPN 等加密软件时，远程访问的最后手段是 Telnet。然而，在明文通道上输入密码是非常危险的，因为任何人可能都在监听。一次性密码（或 OTP）解决了这个问题。

一次性密码对于同一个账户只使用一次，可以防止任何人从网络上嗅探到有效密码。通常，用户会打印出 OTP 系统生成的密码列表，并顺序使用这些密码。你也可以将 OTP 与普通密码配合使用，提供双重身份验证。

# 第 13 章 实现系统安全

# 保护一次性密码

仅仅每个密码只能使用一次，并没有理由不像普通密码那样安全地保护一次性密码。妥善保管打印密码列表，防止他人窥视。

两个最流行的 OTP 系统是 OPIE 和 S/Key（OPIE 实际上是对 S/Key 的改进）。你可以在 `http://www.inner.net/-cmetz/opie` 和 `http://citeseer.nj.ee.com/34338.html` 了解更多关于这些技术。

# 基于时间的密码

一次性密码方案的改进是基于时间的密码方案。在这里，你的密码基于当前时间，这便于使用显示你当前密码的令牌（在此语境下称为 PIN）。此 PIN 通常是基于与认证服务器共享的种子的随机数。该系统的功能取决于令牌和认证服务器中时钟作为公共随机数种子的准确性和同步性。

大多数基于时间的身份验证系统利用双重身份验证，需要单独的密码以及令牌上显示的 PIN。这些系统比一次性密码具有明显的优势，因为你永远不需要返回服务器获取更多密码——你的当前密码始终显示在你的令牌上。

该领域最受认可的公司之一是 RSA，他们的 SecurID 系统使用加密令牌进行基于时间的双重身份验证。你可以在 `http://www.rsasecurity.com/products/secured` 查看关于该技术的介绍。

# 证书

数字证书使用公钥加密来提供身份验证。如果你还记得关于公钥加密的讨论，私钥可以用于私密地对文档进行“签名”——如果相应的公钥可以解密该文档，就可以确定它是使用私钥加密的”。最简单形式的数字证书是一份用特殊密钥签署的文档，该密钥通常属于名为证书颁发机构（CA）的信任第三方。当你将证书发送到尝试验证身份的服务器时，整个公钥基础架构（或 PKI）取决于证书颁发机构的正确行为，而你对 PKI 的信任自 20 世纪 90 年代中期一直是许多论文、演讲和会议的主题。

数字证书的问题它们只是单个文档，就像密码一样。如果第三方设法获取你的证书，他们就可以像获取你的密码一样伪装成你。数字证书只有在双重身份验证系统中才是安全的，因为它们作为密码或其他身份验证机制的补充。

# Kerberos

到目前描述的所有安全身份验证机制要么加密了密码，要么避免了在网络上传输敏感密码。Kerberos 是一种完全不同的机制，它不会在网络上传输密码。相反，Kerberos 使用你的密码作为密钥来解密服务票据，这些票据用于代替密码对 Telnet 和 FTP 等服务进行验证。你唯一输入密码的时候是登录时。

Kerberos 是一个“信任第三方”系统；它依赖密钥发行中心（KDC）持有每个用户密码（或密钥）的副本，以及每个服务的密钥。服务票据是一个使用服务密钥和用户密钥加密的标识符。当用户想要使用票据连接到服务时，票据用用户密钥解密，产生用服务密钥加密的数据。然后将票据发送到服务器，服务器使用其密钥解密并检索用户身份。这种双重加密是 Kerberos 运行的关键。

Kerberos 最重要的因素是 KDC。作为信任第三方和所有密钥的持有者，KDC 必须保持物理安全并防止受到网络攻击。如果 KDC 遭到攻破，你的整个基础设施都会受到破坏。Kerberos 有一个显著缺点，对于许多网络服务如 Telnet、FTP 和 SSH。由于这个原因，Kerberos 通常仅限于有资源重写代码的大学和其他机构。关于 Kerberos 的更详细讨论超出了本书的范围，但以下互联网资源提供了更多信息：
