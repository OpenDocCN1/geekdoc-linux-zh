
```bash
root# ldapsearch -x -b "dc=ldap,dc=abmas,dc=biz" \
    -H 'ldap://ldap.abmas.biz:389' -ZZ

# extended LDIF
#
# LDAPv3
# base <> with scope sub
# filter: (objectClass=*)
# requesting: ALL
#

# abmas.biz
dn: dc=ldap,dc=abmas,dc=biz
objectClass: dcObject
objectClass: organization
o: Abmas
dc: abmas

# Manager, ldap.abmas.biz
dn: cn=Manager,dc=ldap,dc=abmas,dc=biz
objectClass: organizationalRole
cn: Manager

# ABMAS, abmas.biz
dn: sambaDomainName=ABMAS,dc=ldap,dc=abmas,dc=biz
sambaDomainName: ABMAS
sambaSID: S-1-5-21-2383545452-1056757430-1592208922
sambaAlgorithmRidBase: 1000
objectClass: sambaDomain
sambaNextUserId: 67109862
sambaNextGroupId: 67109863
```

如果你遇到任何问题，请阅读第 `44.4` 节。

### 44.4 故障排除

配置 TLS 时最常见的错误，正如我已多次提及的，是你在第 `44.2.2` 节中输入的通用名称（CN）不是你 `ldap` 服务器的完全限定域名（FQDN）。

其他错误可能包括你的 `ldapsearch` 命令中某处有拼写错误，或者 `server.crt.pem` 和 `cacert.pem` 文件的权限设置不正确。根据第 `44.2.3` 节，它们应该设置为 `chmod 640`。

对于其他任何问题，最好阅读你的 `ldap` 日志文件或加入 OpenLDAP 邮件列表。

# Samba 支持

信息技术行业中最难回答的问题之一就是：“什么是支持？”这个问题可能会让一些人感到恼火，而常见的回答也可能让其他人感到厌烦。

关于支持最令人沮丧的情况之一，就发生在一位 Linux 用户向互联网服务提供商（ISP）拨打电话时。服务商没有倾听问题以寻找解决方案，而是平淡地回复道：“哦，Linux？我们不支持 Linux。” 我亲身经历过这种事，类似的场景在 IT 行业中也屡见不鲜。这样的回答旨在告诉我们，有些客户是业务方根本不想打交道的，我们难免会感受到这种被拒绝的痛苦。

考量支持的一种方式，是将其视为无论情况如何，都能在对的时间、对的地方提供正确的答案。支持是消除痛苦、中断、不便、生产力损失、迷失方向、不确定性以及实际或感知风险所必需的一切。

推动开源软件采用的一大驱动力，是许多 IT 企业提供的服务或许未能满足客户预期，或因其他原因而存在不足的事实。

鉴于满足需求是信息技术用户或消费者预期的主要体验，本章提供的信息可以帮助人们避免在问题解决方面产生不愉快的体验。

在开源软件领域，有两种支持选择：免费支持和付费（商业）支持。

### 45.1 免费支持

免费支持可以从朋友、同事、用户组、邮件列表和交互式帮助设施中获得。交互式设施的一个例子是互联网中继聊天（IRC）频道，这些频道承载用户支持的互助活动。

Samba 项目维护着一个邮件列表，常用于讨论 Samba 部署的解决方案。关于订阅 Samba 邮件列表的信息可以在 [Samba 网站](https://lists.samba.org/smlang/)¹ 上找到。用于获取免费的用户贡献支持的公开邮件列表被称为 `samba` 列表。该列表的电子邮件地址为 `mail:samba@samba.org`。关于 Samba IRC² 频道的信息可以在 [Samba IRC² 网页](http://www.samba.org/samba/irc.html) 上找到。

作为一个通用规则，直接联系 Samba 团队成员以获取免费支持，通常被认为是不好的网络行为。大多数活跃的 Samba 团队成员都工作异常长时间，以协助那些已证明其问题具有资格的用户。一些团队成员可能会要求付费，以回应通过电子邮件或电话直接联系的协助请求。Samba 团队的少数成员实际上提供专业的付费 Samba 支持，因此，在所有直接联系中表现出适当的谨慎和保留态度是明智的。

当你遇到一个 Samba 错误时，通常解决的最快方法是发布一个错误报告³。所有这些报告都会通过邮件发送给负责该代码的维护者进行处理。报告的质量越高，问题越严重，处理得就越快。另一方面，如果负责人无法复现报告的错误，该报告很可能被拒绝。你是否提供了足够的信息让问题得以重现，取决于你自己。

我们都承认，有时免费支持无法在所需的时间框架内提供所寻求的答案。在其他时候，问题难以捉摸，你可能缺乏隔离问题并从而解决它所需的经验。在这种情况下，购买付费支持可能是审慎之举。

### 45.2 商业支持

Samba 站点最常寻求的六种基本支持导向的服务如下：

- 网络设计协助

- 员工培训

- Samba 网络部署和安装协助

- 优先的电话或电子邮件 Samba 配置协助

- 故障排除和诊断协助

- 提供质量保证的、可直接安装的 Samba 二进制软件包

关于提供专业 Samba 支持的公司信息，可以通过执行 Google 搜索以及查阅 [Samba 支持⁴](http://www.samba.org/samba/support.html) 网页获得。向 Samba 团队通知他们提供商业支持的公司，将获得一个免费列表，按原籍国排序。允许多个列表，但不提供任何保证。你需要自行甄别支持提供商，并确认该公司及其员工能够交付他们所需的交付物。

Samba 团队内部的政策是平等对待所有商业支持提供商，不表现出任何偏好。因此，提供商业支持的 Samba 团队成员被与其他所有人归为一类。我们鼓励你从当地公司获取所需服务。开源运动是支持社区的；因此，尽其所能帮助当地企业繁荣发展。

可以在任何地方、以任何价格获得任何质量的开源软件支持。全球有超过 180 家公司提供 Samba 支持，在错误地认为 Samba 是不受支持的软件而遭受痛苦是没有借口的；它是受到支持的。

# DNS 和 DHCP 配置指南

## 46.1 特性与优势

在 UNIX 世界中，很少有主题像域名系统（DNS）和动态主机配置协议（DHCP）那样能引起如此多的争议。关于 DNS 和 DHCP 特定实现的赞成或反对的所有观点都是有效的。

我们生活在一个现代时代，许多信息技术用户要求移动性和自由。特别是 Microsoft Windows 用户期望能够将其笔记本电脑插入网络端口并让一切“即插即用”。

UNIX 管理员有他们的道理。从安全角度来看，Microsoft Windows 世界中的许多规范做法最好能避免不好的做法。Microsoft Windows 网络协议允许工作站随意地在网络上注册自己。Windows 2000 Active Directory 在 DNS 命名空间中注册条目，这对 UNIX 管理员来说同样令人困惑。欢迎来到新世界！

本章的目的是演示 Internet 软件联盟（ISC）DNS 和 DHCP 服务器的配置，以提供与 Microsoft Windows 2000 服务器产品中相应产品兼容的动态服务。

本章提供了 DNS 和 DHCP 服务器配置文件的简单工作示例。所使用的示例与本文档其他地方的配置示例相匹配。

本章明确不提供教程，也不假装是 DNS 和 DHCP 的参考指南，因为这远远超出了本文档作为整体的范围和意图。任何想要更多详细 DNS 或 DHCP 参考资料的人，可以访问 `<http://www.isc.org>`¹ 上的 ISC 网站。想要书面文本的人可能对 O'Reilly 关于 DNS 的出版物感兴趣，请参见 O'Reilly² 网站，以及 BIND9.NET³ 网站以获取详细信息。书籍是：

1. DNS 和 BIND，作者 Cricket Liu, Paul Albitz，ISBN: `1-56592-010-4`

2. DNS 与 Bind 食谱，作者 Cricket Liu，ISBN: `0-596-00410-9`

3. DHCP 手册（第 2 版），作者：Ralph Droms, Ted Lemon，ISBN `0-672-32327-3`

## 46.2 示例配置

DNS 之于互联网，犹如水之于生命。几乎所有信息资源（主机名）都通过 DNS 解析到它们的互联网协议（IP）地址。Windows 网络极力避免 DNS 的复杂性，但可悲的是，DNS 赢了。DNS 的替代方案，Windows 互联网名称服务（WINS）—— 基于 TCP/IP 协议上的 NetBIOS 网络的一个产物—— 已经显示出可扩展性问题，以及随着信息技术网络规模和复杂性的增长而变得不可管理的平坦、非层次化的命名空间。
