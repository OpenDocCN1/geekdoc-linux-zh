
```
kali@kali:$ hydra 10.11.02.22 /frontpage.php?user=admin&pass= -l admin -P /usr/share/wordlists/rockyou -v -f
Hydra v0.8 (c) 2019 by van Hauser /THC - starting on 2019-06-07 15:55:21
[DATA] max 16 requests per server, overall 16 servers, 143439 login tries (1:p:143439)
[ATTACK] http-post:10.11.02.22/frontpage.php?user=admin&pass= -INVALID LOGIN
[RESOLVE] Resolving ... [RESOLVED] done
[ATTEMPT] login admin "pass123456" - 1 of 143439 Hydra (child 0)
[ATTEMPT] login admin "134" - 2 of 143439 Hydra (child 1)
[ATTEMPT] login admin "1234568" - 3 of 143439 Hydra (child 2)
[ATTEMPT] login admin "password" - 4 of 143439 Hydra (child 3)
[ATTEMPT] login admin "loveyou" - 5 of 143439 Hydra (child 4)
[ATTEMPT] login admin "princess" - 6 of 143439 Hydra (child 5)
[ATTEMPT] login admin "1234567" - 7 of 143439 Hydra (child 6)
[ATTEMPT] login admin "karina" - 268 of 143439 Hydra (child 7)
[ATTEMPT] login admin "dookie" - 269 of 143439 Hydra (child 8)
[ATTEMPT] login admin "hotmail" - 270 of 143439 Hydra (child 9)
[ATTEMPT] login admin "0123456789" - 271 of 143439 Hydra (child 10)
[00][http-post-form] host:10.11.02.22 login:admin password:crystal
[STATUS] attack finished for 10.11.02.22 (valid password found)
1 of 1 target successfully completed: valid password found
Hydra @github.com/vanhauser-thc-hydra finished on 2019-06-07 15:55:22
```

585

# 使用 Kali Linux 进行渗透测试 2.0

尽管这需要对应用程序进行一些研究，但结果是值得的，因为发现了有效的密码。`Hydra` 包含的其他服务模块也非常值得投入精力掌握。

## 19.3.4.1 练习

（这些练习不需要报告）

- 1. 针对 Windows 客户端上的表单运行 HTTP POST 密码攻击。
- 2. 针对本地 Kali Linux 上的 Pure-FTPd 应用执行 FTP 密码攻击。

## 19.4 利用密码哈希值

接下来，我们将注意力放在密码哈希的使用上。

加密哈希函数¹⁶² 是一种单向函数，它实现了一种算法，给定任意数据块并返回一个固定大小的字符串，称为“哈希值”或“消息摘要”。加密哈希最重要的用途之一就是应用程序验证和密码验证。

### 19.4.1 获取密码哈希值

大多数使用密码身份验证机制的系统都需要将这些密码存储在机器本地。现代身份验证机制不再以明文存储密码，而是将其存储为哈希值以提高安全性。对于操作系统、网络硬件等也是如此。这意味着在身份验证过程中，用户提供的密码会被哈希处理，并与之前存储的摘要进行比较。

在没有关于程序或 Openwall 网站¹⁶³ 更多信息的情况下，识别确切的哈希类型有时是不可能的。在尝试识别摘要类型时，有三个重要的属性需要考虑。包括哈希的长度、哈希中使用的字符集以及哈希中使用的任何特殊字符。

辅助哈希识别的有用工具是 `hashid`¹⁶⁴。要使用它，只需运行该工具并传入我们识别出的哈希即可。

```
kali@~$ hashid c43ee55d96bc7f691fe2fbbe8a5ef0a
[*] MD2
[*] MD5
[*] MD4
[*] LM
```

> ¹⁶² (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cryptographic_hash_function

> ¹⁶³ (Openwall, 2019), http://openwall.info/wiki/john/sample-hashes

> ¹⁶⁴ (Psyp, 2015), https://psypanda.github.io/hashid/

- [+] RIPEND-128
- [+] Haval-128
- [+] Tiger-128
- [+] Skein-256(128)
- [+] Skein-312(128)
- [+] Lotus Notes/Domino 5
- [+] Skype
- [+] Sefru-128
- [+] NTLM
- [+] Domain Cached Credentials
- [+] Domain Cached Credentials 2
- [+] DNSEC (NSEC3)
- [+] Radmin v2.2

```
kali@hash: '$61S6LXIAASS1BwUDsXCetlb1Th76WE.bI66AMYEDKXQ8s7JNFwa1s1KKtand
6ZqsQQKAF3G0tHD9Db95NaS/s7COajRTJNWP2s'
```

- SHA-512 Crypt

在上面，我们分析了两个不同的哈希。虽然第一个示例返回了多个匹配，但第二个将哈希缩小到了 SHA-512 Crypt。

接下来，让我们在 Kali 系统上检索并分析几个哈希。许多系统使用存储在 `/etc/shadow` 文件中的用户密码哈希，这需要 root 权限查看：

```
kali@hash: sudo grep root /etc/shadow
root:$6$R9w9Z2A8B5ZAfRBwP6M6BE.ElLs571VuccCAhYrXcG0VDeYUg5f8iwnXJkr.wtLDJI5IpoygccLaWtP/gwQ0J754:999999:
```

列表 614 - 从 Kali Linux `/etc/shadow` 获取的 root 哈希

在第 614 行，我们发现了带有用户名的哈希。该哈希被分为多个字段，其中第一个 `($6$)` 指 SHA-512¹⁶ 算法。下一个字段是 salt,$⁶⁶ 它与明文一起计算密码哈希。盐是一个随机值，与明文一起计算密码哈希。这防止了哈希查询，因为密码哈希会根据盐值而变化。攻击者可以在表中存储预计算的哈希值。表可以包含 terabytes 的空间，但可以快速将哈希映射到明文。加盐增加了在计算实际哈希之前密码值的随机性。

> ¹⁶⁵ (ashroot, 2013), https://www.shadow.com/how-are-passwords-stored

> ¹⁶⁶ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Salt_cryptography

> ¹⁶⁷ (nets.cc, 2012), https://nets.cc/Cryptography

> ¹⁶⁸ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Hash_table

## 使用 Kali Linux 进行渗透测试

让我们转向 Windows 目标，讨论哈希实现以及我们如何利用它们。在 Windows 系统上，哈希密码存储在安全帐户管理器 (`SAM`)¹⁶⁹。为了防止离线密码攻击，微软引入了 `SYSKEY`¹⁷⁰ 功能来部分提取 SAM 文件。Windows NT 系统直到 Windows 2003 使用两种不同的哈希：LAN Manager (`LM`)¹⁷¹ 和 NT Manager (`NTLM`)¹² `LM` 被认为非常脆弱，因为超过七个字符的密码被分成两个字符串，每个部分都经过哈希处理；此外，`LM` 不包含盐，使得哈希查询攻击可行。从 Windows Vista 开始，操作系统默认禁用了 `LM` 并使用 `NTLM`；它更敏感，支持所有 Unicode 字符，并且不会将哈希分成部分。存储在 SAM 数据库中的 NTLM 哈希仍然带有盐。
