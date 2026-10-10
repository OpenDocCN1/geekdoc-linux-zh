
此标头包含两个邮件服务器用于识别入站邮件真实性的参数。

## Received-SPF

`SPF` 记录是一种基于 `TXT` 的 `DNS` 记录，由电子邮件提供者提供并添加到域名的 `DNS` 区域中。`SPF` 记录语法包含了允许代表该域名发送电子邮件的 `IP` 地址。

在上面的示例中，当 `gmail.com` 分析入站邮件时，它会检查发送者域名的 `SPF` 记录，并发现 `IP` `209.85.220.69` 被允许代表域名发送邮件。如果入站邮件的源 `IP` 是其他值，`gmail.com` 将把邮件分类为垃圾邮件。

## DKIM-Signature

`DKIM` 签名是另一个参数，包含一个公开的密钥，发送者域名使用该密钥进行签名。当 `gmail.com` 接收入站邮件时，它会向发送者服务器发送请求，将此密钥与源服务器上相应的域名密钥进行匹配。如果密钥匹配，则认为邮件是真实的。

## 邮件钓鱼

邮件钓鱼（`Email Phishing`）是指向某人发送邮件，谎称是某人并诱骗他们披露敏感信息，如个人详情或银行账户详情。本质上，邮件钓鱼是邮件伪造（`email spoofing`）产物。攻击者会给您发送邮件；他们可能通过操纵邮件头使其看起来像合法来源。或者，如果他们不擅长黑客攻击，会尝试从与合法邮件地址非常相似的邮件地址发送邮件。例如，他们会创建一个类似 `info@citibank.com` 的邮件地址。乍一看，这像是花旗银行的真实邮件地址，但如果你仔细观察，发现里面有两个 `I`。如果你不非常小心，可能会点击攻击者在邮件正文中植入恶意链接，该链接将您重定向到一个要求您输入银行详情的网站。然而，该网站是攻击者开发的虚假网站，仅用于窃取您的信息。

## 钓鱼诈骗

一些最常见的钓鱼邮件长什么样？钓鱼邮件的内容大多是承诺您将获得某些大好处。攻击者利用目标有多么轻信，这一点得以在钓鱼诈骗中获得成功。

在 2000 年初，来自非洲的攻击者向用户发送了大量邮件，声称自己是某个富有的人，且在临终之际想将财富分送给普通人。金额可能高达 `100,000` 美元。轻信的收件者会上当并回复这些邮件，期望赚点快钱。然而，随着过程进行，攻击者会要求获胜者支付少额资金，用于将奖金转账到用户的银行账户。这可能是 `100` 美元之类的金额，用户会将这笔钱发送给攻击者，但再也听不到他们的任何消息。

## 防御钓鱼

您可以采取一些基本的预防措施保护自己免受钓鱼诈骗的影响。

- 确保仔细阅读邮件并双检邮件发送者。如果发送者是认识的朋友，但邮件看起来有点奇怪，请致电给他们，确认他们是否给您发送过此类邮件。
- 如果邮件包含链接，在点击之前仔细检查该链接。
- 如果您以某种方式点击了链接并进入了一个要求您输入登录详情的网站，请检查浏览器中的 `URL` 以确认它是否确实是。

## 您的邮件安全

- 如果邮件包含链接，在点击之前仔细检查该链接。
- 如果您以某种方式点击了链接并进入了一个要求您输入登录详情的网站，请检查浏览器中的 `URL` 以确认它是否确实是。
- 确保仔细阅读邮件并双检邮件发送者。如果发送者是认识的朋友，但邮件看起来有点奇怪，请致电给他们，确认他们是否给您发送过此类邮件。
- 然而，随着过程进行，攻击者会要求获胜者支付少额资金，用于将奖金转账到用户的银行账户。
- 如果邮件包含链接，在点击之前仔细检查该链接。
- 如果您以某种方式点击了链接并进入了一个要求您输入登录详情的网站，请检查浏览器中的 `URL` 以确认它是否确实是。
- 确保仔细阅读邮件并双检邮件发送者。如果发送者是认识的朋友，但邮件看起来有点奇怪，请致电给他们，确认他们是否给您发送过此类邮件。
- 如果邮件包含链接，在点击之前仔细检查该链接。
- 如果您以某种方式点击了链接并进入了一个要求您输入登录详情的网站，请检查浏览器中的 `URL` 以确认它是否确实是。
- 确保仔细阅读邮件并双检邮件发送者。如果发送者是认识的朋友，但邮件看起来有点奇怪，请致电给他们，确认他们是否给您发送过此类邮件。
- 如果邮件包含链接，在点击之前仔细检查该链接。
- 如果您以某种方式点击了链接并进入了一个要求您输入登录详情的网站，请检查浏览器中的 `URL` 以确认它是否确实是。
- 确保仔细阅读邮件并双检邮件发送者。如果发送者是认识的朋友，但邮件看起来有点奇怪，请致电给他们，确认他们是否给您发送过此类邮件。
- 如果邮件包含链接，在点击之前仔细检查该链接。
- 如果您以某种方式点击了链接并进入了一个要求您输入登录详情的网站，请检查浏览器中的 `URL` 以确认它是否确实是。

## 结论

我诚心地希望您喜欢这本书并且它对您有所帮助。这本书的目标不是让您成为专家，而是让您对我们讨论的话题有一个坚实的理解。学习无止境，希望您能继续探索这些领域。感谢阅读。

- [8] Lazari, C. (2019). 道德渗透侦察计划：被动足迹探测 - Chris Lazari。获取自 https://chrislazari.com/ethical-hacking-passive-footprinting/
- [9] Lazari, C. (2019). 道德渗透侦察计划：被动足迹探测 - Chris Lazari。获取自 https://chrislazari.com/ethical-hacking-passive-footprinting/
- [10] Lazari, C. (2019). 道德渗透侦察计划：被动足迹探测 - Chris Lazari。获取自 https://chrislazari.com/ethical-hacking-passive-footprinting/
- [11] Lazari, C. (2019). 道德渗透侦察计划：被动足迹探测 - Chris Lazari。获取自 https://chrislazari.com/ethical-hacking-passive-footprinting/
- [12] Lazari, C. (2019). 道德渗透侦察计划：被动足迹探测 - Chris Lazari。获取自 https://chrislazari.com/ethical-hacking-passive-footprinting/
- [13] Lazari, C. (2019). 道德渗透侦察计划：被动足迹探测 - Chris Lazari。获取自 https://chrislazari.com/ethical-hacking-passive-footprinting/
- [14] 足迹探测与侦察 | 足迹探测与侦察之……。(2019)。获取自 http://www.keyfora.com/search/footprinting-and-reconnaissance
- [15] 道德渗透指纹识别。(2019)。获取自 https://www.tutorialpoint.com/ethical_hacking/ethical_hacking_fingerprinting
- [16] 道德渗透嗅探。(2019)。获取自 https://www.tutorialpoint.com/ethical_hacking/ethical_hacking_sniffing
- [17] 道德渗透 ARP 污染。(2019)。获取自 https://www.tutorialpoint.com/ethical_hacking/ethical_hacking_arp_poisoning
- [18] 道德渗透 ARP 污染。(2019)。获取自 https://www.tutorialpoint.com/ethical_hacking/ethical_hacking_arp_poisoning
- [19] 道德渗透 ARP 污染。(2019)。获取自 https://www.tutorialpoint.com/ethical_hacking/ethical_hacking_arp_poisoning
- [20] 道德渗透 ARP 污染。(2019)。获取自 https://www.tutorialpoint.com/ethical_hacking/ethical_hacking_arp_poisoning
- [21] 道德渗透 ARP 污染。(2019)。获取自 https://www.tutorialpoint.com/ethical_hacking/ethical_hacking_arp_poisoning
- [22] 道德渗透 ARP 污染。(2019)。获取自 https://www.tutorialpoint.com/ethical_hacking/ethical_hacking_arp_poisoning
- [23] 道德渗透 ARP 污染。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_arp_poisoning.htm
- [24] 道德渗透 DNS 污染。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_dns_poisoning.htm
- [25] 道德渗透 DNS 污染。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_dns_poisoning.htm
- [26] 道德渗透 DNS 污染。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_dns_poisoning.htm
- [27] 道德渗透漏洞利用。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_dns_poisoning.htm
- [28] 道德渗透漏洞利用。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_exploitation.htm
- [29] 道德渗透漏洞利用。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_exploitation.htm
- [30] 道德渗透漏洞利用。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_exploitation.htm
- [31] 道德渗透漏洞利用。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_exploitation.htm
- [32] 道德渗透漏洞利用。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_exploitation.htm
- [33] 道德渗透枚举。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_enumeration.htm
- [34] 道德渗透枚举。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_enumeration.htm
- [35] 道德渗透枚举。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_enumeration.htm
- [36] 道德渗透 Metasploit。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [37] 道德渗透 Metasploit。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [38] 道德渗透 Metasploit。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [39] 道德渗透 Metasploit。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [40] 道德渗透 Metasploit。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [41] 道德渗透 Metasploit。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [42] 道德渗透 Metasploit。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [43] 道德渗透 Metasploit。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [44] 道德渗透 Metasploit。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [45] 道德渗透 TCP/IP 污染。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_metasploit.htm
- [46] 道德渗透 TCP/IP 污染。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_tcp_poisoning
- [47] 道德渗透 TCP/IP 污染。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_tcp_poisoning
- [48] 道德渗透 TCP/IP 污染。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_tcp_poisoning
- [49] 道德渗透邮件劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_email_hijing
- [50] 道德渗透邮件劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_email_hijing
- [51] 道德渗透邮件劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_email_hijing
- [52] 道德渗透无线劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_wireless
- [53] 道德渗透无线劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_wireless
- [54] 道德渗透无线劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_wireless
- [55] 道德渗透无线劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_wireless
- [56] 道德渗透无线劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_wireless
- [57] 道德渗透无线劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_wireless
- [58] 道德渗透无线劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_wireless
- [59] 道德渗透无线劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_wireless
- [60] 道德渗透无线劫持。(2019)。获取自 https://www.tutorialspoint.com/ethical_hacking/ethical_hacking_wireless
