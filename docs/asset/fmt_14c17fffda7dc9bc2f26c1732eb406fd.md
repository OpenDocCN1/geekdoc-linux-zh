
你可以通过 CGI 获取这些环境变量。例如，在 `PERL` 脚本中：

```
print "$ENV{'SSL_CERT'}";
print "$ENV{'SSL_CIPHER'}";
```

或者，在 `C` 语言中：

```c
char *variable=getenv("SSL_CLIENT");
```

表 15.2 Apache-SSL 指令

| Field | Function |
| :--- | :--- |
| CustomLog | 其工作方式与 Apache 相同。唯一的区别是在 Apache-SSL 中，你可以记录多个额外值，包括会话算法、客户端证书和 SSL 版本。 |
| HTTPS | 指定服务器正在使用的。 |
| HTTPS_CIPHER | 指定使用的哪种算法，SSL 或 TLS。 |
| HTTPS_KEYSIZE | 指定会话密钥长度。 |
| HTTPS_SECRETKEYSIZE | 指定使用的哪种密钥长度。 |

安全 Web 协议

433

第15 章

# 关于证书和证书颁发机构

如果您计划使用 Linux 建立电子商务服务器，您应该从公认的证书颁发机构获取证书——这是一个颁发证书并验证其真实性的受信第三方。此类证书可以极大增强贵公司的信誉，并帮助其满足作为电子商务交易平台时通常严苛的要求。

定价方案各不相同，几乎所有成熟的证书颁发机构都要求您提供法律证明，证明你有权在交易中使用公司的法定业务名称。典型的示例包括：

- 有效的营业执照
- 公司章程
- 州务卿办公室或公司部门提供的公司注册记录
- DBA（DB业务名称）
- 公证的合伙经营文件

以下是一些成熟的证书颁发机构：

- Entrust Technologies 提供价格为 $299.00 的一年期 SSL 证书。（有趣的是，Entrust 声称来自其竞争对手的约 4000 万个根证书将在 1999 年 12 月 31 日在 Web 客户端中过期，而 Entrust 的证书则不会。）访问 http://www.entrust.net/products/index.htm 了解更多。
- EuroSign 是欧洲证书颁发机构。根据其网站，EuroSign 组织结构良好。访问 http://www.eurosign.com/ 了解更多。
- GTE 提供 GTE Cyber SSL 证书，价格为 $99.00，有效期六个月（带免费演示版）。访问 http://www.cybertrust.gte/cybertrust/index.html 查看。
- Thawte 咨询部门提供个人和服务器证书。SSL 证书每年 $125.00，个人证书另有价格。然而，有一点警告：Thawte 会索取非常私个人数据，包括您的驾照、护照、社会安全号码、出生日期和家庭地址。这并不是我的胃菜（显然的），但由于 Thawte 严苛的要求，他们的证书被广泛认可并提供高保障。访问 http://www.thawte.com/certs/ 查看 Thawte 的服务。
- VeriSign 可能是最著名的证书颁发机构，为 50 种不同的 Web 服务器提供 SSL 证书（包括使用 SSleay 的 Apache-SSL）。VeriSign 的安全站点选项（标准 SSL）第一年为 $349.00。访问 http://www.verisign.com/server/index.html 了解更多。
- Xcert International 主要为企业和政府实体提供数字证书服务。访问 http://www.xcert.com/software/index.html 了解更多。

# Apache-SSL 总结

Apache-SSL 并不是唯一的 SSL 实现，但它是一个极佳的学习工具。你不仅可以学习如何保护基于 Web 的电子商务交易，由于 SSLLeay 源码是开源的，你还可以看到认证中使用了各种算法。

> 注意

尽管 SSL 是目前加密客户端与服务器交互的主流系统，但也存在安全交易标准和协议。其中之一是安全电子交易（简称 SET），这是一个由 IBM、MasterCard 和 Visa 赞助的系统。SET（专门为信用卡交易设计）伴随着巨大的轰动问世，深受银行、信用卡公司和其他大型金融机构的青睐。

然而，SET 尚未席卷互联网。原因之一是在 SET 交易中，所有参与者都了解交易伙伴的身份。（每个参与者都拥有个人或业务数字证书。）但从消费者的角度来看，SET 提供了优势。消费者会被发放一个钱包，这是一个辅助应用程序，用于存储并传输他们经过验证的身份和财务信息到支持 SET 的远程服务器。在这方面，SET 交易类似于掏出你的钱包或口袋付钱，我个人并不喜欢它，但根据你的领域，SET 可能是适合你的电子商务解决方案。如需了解更多信息，请在 http://www.setco.org/set_specifications.html 查找完整的 SET 规范。

# 关于 SSL 的延伸阅读

最后，为了学习 SSL，请查看以下资源。

- SSL 3.0 协议分析，David Wagner 和 Bruce Schneider 著。本文深入探讨了 SSL 协议及其安全影响。地址：http://www.counterpane.com/ssl.html。
- 引入 SSL 和证书。该文档描述了 SSL 证书的要点。地址：http://www.ultranet.net/~fhirsch/Papers/cook/ssl_intro.html。

# 安全协议

第15 章

- 内网通信安全防护，Taher Elgham, Jeff Treuhaft, Netscape Corporation 著。该文档对 SSL 有很好的覆盖。地址：http://www.go-digital.net/whitepapers/securecomm.html。
- SSL 菜谱，Allan Shiffman, Terisa Systems 著。该文档涵盖了如何设置 SSL 和安装证书。地址：http://www.ultranet.net/~fhirsch/ssl_cook.html。
- SSL 演示稿，Shiffman, Terisa Systems 著。该文档提供了关于 SSL 的演示报告。地址：http://www.terisa.com:80/presentations/ams/index.html。
- SSL 对话常见问题解答，v1.1 回答了许多关于 SSL 协议、设计和实现的问题。地址：http://www.consensus.com/security/ssl-talk-faq。

# 其他协议：IPSEC

在保护客户端与服务器交互时，基于 SSL 的方案是非常优秀的。但在企业环境中，你可能需要某种侧重于网络到网络交互的东西。为此，你几乎会想要 IPSEC。

IPSEC 是互联网安全选项，一种对 IP 数据报文应用加密和会话检查的系统。IPSEC 最初为国防网络等敏感环境开发，现在用于保护两个或多个网络之间的数据。

> 注意

VPN 技术允许拥有专线的公司在互联网上建立一个封闭且安全的电路。通过这种方式，公司确保它们之间传输的数据通过加密并不受第三方干扰。许多公司通过消除专线每年节省了数千美元。

IPSEC 在许多方面优于竞争方案。例如，由于 IPSEC 在数据包级别执行加密和认证，它在很大程度上与平台无关。这具有广泛的意义，因为 IPSEC 可以透明地保护不同类型的网络流量。

目前有三种免费 IPSEC 实现供选择：

- FreeS/WAN（安全广域网）——一个为 Linux 提供 IPSEC 和 IKE 实现的项目。
- NIST Cerberus——Linux 的 IPSEC 参考实现；一个提供主机到主机、主机到路由器以及路由器到路由器 IPSEC 服务。
- 亚利桑那大学的 x-kernel IPSEC——该项目已停止，但源代码可用。访问 http://www.cs.arizona.edu/security/hpcc-blue/linux.html 了解更多。

建立支持 IPSEC 的网络交互超出了本书的范围。这个主题完全可以专门写出一本书来讨论。但如果你对 IPSEC 的工作原理感兴趣，请查看源头：http://www.ietf.org/ids.by.wg/ipsec.html。

## 总结

SSL 足以保护你的客户端服务器流量免受第三方窃听，你甚至可以使用 SSL 库为其他应用程序开启 SSL 功能。但有时，驱动 IPSEC 客户端的是敌人。在这种情况下，SSL 无法保护你。相反，你必须依赖安全编程技术来保护你的服务器免受攻击。这就是下一章的主题。

## Linux 网络安全

第四部分

作为一名 Linux 用户，你最终会涉足 Web 开发。这是必然的。而 Linux 在这一领域提供了大量的工具和机会。然而，当你编写自己的 Web 工具时，必须确保不会在无意中为你原本安全的宿主机留出安全漏洞。本章将快速审查 Web 开发技术。

# 开发风险因素：概览

在每一个 Web 开发项目中，你都会面临三个主要的风险，这些风险按逻辑顺序从项目开始到最终完成呈现出来：
