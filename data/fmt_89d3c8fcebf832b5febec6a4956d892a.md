
通过在 TCP 规则中使用 `proxy` 关键字，你可以轻松地利用 pf 的 SYN Proxy 功能，适用于所有或特定的 TCP。pf 的 SYN Proxy 实现拦截 SYN 数据包，使你的服务器仅感知已完成的 TCP 连接，并免受 SYN 洪水攻击。可以使用上一节描述的状态跟踪选项保护防火墙本身免受 SYN 洪水攻击。

## 数据包规范化

pf 提供了 `scrub` 关键字，用于数据包规范化。这可以防止某些类型的攻击。例如，某些攻击使用无法正确重组的分片；`scrub` 会拒绝这些数据包。清洗还可以降低包含无效标志组合的 TCP 包的有效性。

## OS 指纹识别 (OS Fingerprinting)

OSFP 使用 `/etc/pf.os` 数据库被动检测远程操作系统的类型。这意味着 TCP 规则可以设计为允许或阻止

来自特定操作系统的流量。此示例规则将阻止来自运行 Windows 2000 的主机的数据包：

```ppf
block in $ext_if from any os "Windows 2000"
```

需要注意的是，新的服务包和补丁级别可能会更改操作系统的指纹；此外，这种类型的规则可能无法拦截手工构造的数据包。

## authpf(8)

`authpf(8)` 要求用户在允许流量通过之前先对网关进行身份验证。要启用此功能，请将用户的 shell 设置为 `/usr/sbin/authpf` 并指示用户在需要网络连接时通过 `ssh` 登录到网关。一旦用户成功通过身份验证，`authpf` 将将该用户的自定义规则插入到 pf 规则集中。换句话说，`authpf` 使得同时对用户进行身份验证并以每个用户为单位执行规则成为可能；这些功能通常只在昂贵的商业防火墙产品中可用。

一旦用户注销或其 SSH 断开连接，`authpf` 会自动删除用户规则。每次成功的身份验证都会记录用户名、IP 地址以及连接时间，从而更容易确定谁在何时登录了。`authpf` 可以在无线网络上提供额外的安全措施，可以在 pf FAQ 中找到示例配置。

## BSD 安全公告

安全对于 BSD 项目至关重要，每个项目在其网站上都维护着一个安全页面，其中包含存档的公告、指向其安全邮件列表的链接、报告安全事件的说明以及其安全团队的描述。每个项目的安全页位于：

- FreeBSD http://www.freebsd.org/security/
- NetBSD http://www.netbsd.org/security/
- OpenBSD http://www.openbsd.org/security.html

BSD 和 NetBSD 公告的格式相似，每份公告都包含以下章节：

- 主题 (Topic)
- 受影响的版本 (Version affected)
- 在哪些版本中修复 (Fixed in which versions)
- 问题描述/
- 影响/技术细节/
# Hacking Exposed Linux: Linux 安全秘密与解决方案
- 解决方案和替代措施
- 参考文献/更多信息

公告包含了关于如何补丁系统以及从哪里下载补丁的完整说明。为了增加保护性，每份公告都由安全官的 PGP 密钥签名，并包含了验证该密钥的说明。

## 额外的 BSD 资源

BSD 的文档非常详尽，大多数文档资源可以随操作系统安装，也可以在网上免费访问。

## 在线 man 页

BSD man 页是顶级的，并提供了足够的配置示例让你开始使用新的命令或概念。在线 man 页允许你指定发布版本；当你需要确定某个命令在旧版本中是否可用，或者你想跟踪版本之间的功能变化时，这非常有帮助。可以在此处找到在线版本：

- FreeBSD http://www.freebsd.org/cgi/man-cgi
- NetBSD http://netbsd.gw.com/cgi-bin/man-cgi
- OpenBSD http://www.openbsd.org/cgi-bin/man-cgi

图-4 显示了 NetBSD 在线 man 页的界面。

## 在线文档

每个 BSD 项目提供了全面的指南和 FAQ，描述并给出了操作系统可用功能的配置示例。当你需要“如何做”指南时，请优先考虑这些资源：

- FreeBSD 手册 http://www.freebsd.org/doc/en_US.ISO88559-1/books/handbook/
- FreeBSD FAQ http://www.freebsd.org/doc/en_US.ISO88859-1/books/faq/
- NetBSD Guide http://www.netbsd.org/guide/en/
- NetBSD FAQ http://www.netbsd.org/Documentation/#documentation
- OpenBSD FAQ http://www.openbsd.org/faq/index.html

## 附录 C: BSD

![](img/ad6042d503047f550174c623.png)

## 书籍

有许多关注 BSD 和安全的书籍可以购买：

- *Mastering FreeBSD and OpenBSD* Yanek Korff, Paco Hope (2003)
- *Building Firewalls with OpenBSD* Addison-Wesley
- *Secure Architectures with OpenBSD* Brandon Palmer, Jose Nazario (2004)
- *BSD Hacks* Dru Lavigne (O'Reilly)

## 索引

抽象 (Abstract Interpretation)

抗碰撞系统, 306

基于...的分析, 518

Apache 服务器,

去中心化配置, 384

基于 Linux 的工具, 521

...的防御

攻击, 38

...列表, 133–234

外部插孔, 229–231

DNS, 471

针对抗碰撞的 DoS, 306

去认证/断开连接, 245

拒绝服务, 22

破坏完整性, 365

被 Kismet 探测, 272–273

设备注入和操纵, 210–211

设备实体, 289

设备, 291

蓝牙设备窃听, 290

等等.

DAC, 70, 71

MAC, 70, 72

POSX, ACLs, 526

RBAC, 70–72

类型, 70, 71

类型, 182–185

类型, 353–355

的, 358

`authpf(8)`

身份验证, 115–150

架构, 25

身份验证, 220–221

组装...的, 252–260

AppArmor, 61–62

应用, 70

应用攻击, 353–355

应用黑客

应用软件, 299

ACK 帧, 241

挑战/响应, 444

高级调优, 110

代数语言, 501

衰减和, 228–229

天线, 58

声学, 329–396

蓝牙适配器, 284

AS/WiFi, 400

异步 JavaScript 和 XML, 36–137

身份证明密钥 (AIK), 337

NetBSD 审计包, 582–583

误配置的, 380

# 索引

# 593

- `authpf(8)`, 587
- 自动化扫描技术, 536
- 自动化 Web 馈订阅, 405
- 自动化系统管理, 550–552
- 意识。安全意识培训
- 公理, 501
- 为了绕过而移除 CMOS 电池, 48
- 修改跳线线设置以绕过, 48–49
- 防止被绕过, 50–52
- 黑名单
  - 欺骗, 18
  - 真实情况统计与, 24

## AXP/OpenVMS 机器

- 渗透测试访问, 175
- 标识符 (banner), 156–157
- blast 工具, 520
- 盲注 注入, 386
- BSD 中的 Blowfish 支持, 576–577
- 蓝牙劫持 (bluejacking), 293
- 蓝牙窃听 (blueysting), 293
- 蓝牙设备, 282–294

## B

- 后门 BIOS 密码, 46–48
- 后门, 111–113
  - 关于, 111
  - 检测与缓解, 111–113
  - 通过 TCP/IP 协议的防火墙访问, 110
  - 用于隐藏的根基程序, 113
- 后端服务器
  - 配置, 270–271
  - Linux RFID, 312
- 备份 IDNS 线路, 130
- 备份，从备份中恢复系统, 119–120
- 通过软件和固件漏洞发的攻击, 293
- 案例研究, 268–283
- 针对安全相关漏洞的应对, 293–294
- 创建数据对, 289–290
- 禁用对查询请求的响应, 291–292
- 窃听, 250
- 加密, 290–291
- 协议栈上的实体, 286–288
- 伪造设备条目, 289
- 收集客户端信息, 291
- 防止服务发现, 292
- 配置文件和反配置文件, 284–285
