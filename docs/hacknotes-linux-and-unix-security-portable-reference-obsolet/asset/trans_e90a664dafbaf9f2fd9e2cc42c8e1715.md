

## 常用工具

Airsnot 和 Kismet 是最流行且最实用的无线入侵工具。它们可用于检测无线网络以及破解启用 WEP 的网络的加密密钥。

> 对于启用 WEP 的无线网络，入侵者必须采取的第一步是利用 Airsnot 等工具获取 WEP 加密密钥。在获取密钥并成功加入无线网络后，入侵者可以使用 Ettercap、tcpdump 和 Etherleato 等流行工具来分析网络流量。

### Airsnot

Airsnot（如图 11-1 所示）是一个基于 Linux 的网络嗅探工具，它通过被动监控无线传输来破解 WEP 加密密钥。Airsnot 可在 **http://airsnot.shmoo.com/** 获取。目前，Airsnot 支持以下无线网卡：

-   Cisco Aironet。
-   基于 Prism2 的网卡。支持的网卡列表请参考 **http://www.linux-wlan.org/**。
-   Orinoco 网卡。请从 **http://airsnot.shmoo.com/orinocoinfo.html** 下载驱动程序补丁和相关信息。

关于常见问题和疑问的解答，请参阅 Airsnot FAQ。其网址为 **http://airsnot.shmoo.com/faq.html**。

![](img/77287f6ef97ef0bed6e23f6610950d06_226_0.png)

### Kismet

Kismet（如图 11-2 所示）是一种无线网络嗅探器，可用于捕获和查看某区域内无线网络的信息。它拥有以下特点：

-   Ncurses 界面
-   信道跳变
-   多数据包源
-   IP 块检测
-   支持使用 gpsmap 进行 GPS 映射
-   即时 WEP 解密

...以及许多其他功能。更多信息请访问 **http://www.kismetwireless.net/documentation.shtml**。

关于如何在 Linux 上安装和使用 Kismet 的详细说明，请参阅 **http://www.tipsybottle.com/technology/wireless/RedHat8-Kismet-HOWTO.shtml**。这篇文章中包含的大多数说明也适用于 Airodump。

### Fata-Jack

Fata-Jack 是 Wlan-Jack 工具的修改版本。它向接入点发送带有已关联客户端源地址的认证请求。这个认证包被故意设计为包含无效信息。当接入点接收到此数据包时，它会取消那个地址被欺骗的客户端的认证。受害客户端此时必须与接入点重新进行认证。因此，任何能够访问网络接入点的恶意用户都可以利用此工具发起拒绝服务攻击。

Fata-Jack 可在此处下载：http://www.loud-fat-bloke.co.uk/w%20080211.html。关于 Wlan-Jack 的信息可在 http://80.211.ninja.net/ 获取。

![](img/77287f6ef97ef0bed6e23f6610950d06_227_0.png)

**图 11-2**。正在运行中的 Kismet

## 保护无线网络

使用 Airosnort 等工具，通常约 5,000,000 至 10,000,000 个数据包就足以破解 WEP 秘密密钥。通常，一个具有一定活跃度的网络在几个小时内就会传输如此数量的数据包。因此，在部署和管理无线网络时，确保足够的安全性变得至关重要。以下是一些建议：

-   将网络视为“不可信”：必须将无线网络视为不可信网络，并与组织的内部网络隔离。如果必须允许无线用户访问可信网络，建议建立 VPN（虚拟专用网络），以便无线用户可以通过支持加密的 VPN 客户端进行连接。同时考虑使用支持 LEAP（轻量级可扩展认证协议）的接入点。此外，鼓励使用采用 WEP-Plus 算法的网络设备，以避免传输具有弱初始向量的帧，从而阻止 Airosnort 等软件成功破解 WEP 加密密钥。
-   鼓励使用采用加密的工具：SSH 等工具有助于创建加密隧道，应在可能时使用。内网网站必须支持 SSL。
-   不允许通过无线方式管理接入点：某些接入点允许禁用无线管理功能。这是一个好主意，因为配置它需要物理访问接入点。
-   更改默认 ESSID 并禁用广播：ESSID（扩展服务集 ID）是一个作为配置参数输入到接入点和以太网卡的字符串。具有相同 ESSID 的设备参与同一个网络。接入点在出厂时通常配置为某个默认 ESSID，通常是厂商的名称。更改这些默认 ESSID 是个好主意。许多接入点还会广播它们的 ESSID，以便无线客户端可以从可用网络中进行选择。建议配置接入点以禁用此功能，因为它会向无权使用该网络的人员广播网络信息。请注意，此步骤并不能保证多少安全性，也不应依赖它。
-   **MAC 地址过滤**：考虑利用支持 MAC 地址过滤的接入点，只允许具有已知 MAC 地址的选定客户端使用网络。然而，这无法阻挡高明的黑客，因为合法用户的 MAC 地址是以明文传输的。这些地址可以被窃听并从空气中捕获，并且可以被欺骗以获取网络访问权限。维护一个授权 MAC 地址列表是一件相当麻烦的事，因此对于大型组织而言，这可能难以实施。

## 总结

在介绍 WEP 协议之后，本章重点介绍了可用于利用和检测无线网络弱点的无线安全工具。常用的 Airosnort 工具可用于破解无线网络中正在使用的 WEP 加密密钥。Kismet 无线嗅探器可用于检测并识别某区域内的无线网络。Fata-Jack 程序可用于对无线网络主机发起拒绝服务攻击。此外，还讨论了不同类型无线天线的优点和用途。最后，本章提出了关于如何更好地保护无线网络免受入侵尝试的建议。因此，强烈建议无线网络管理员理解并执行本章中提出的建议。

## 第 12 章

# 使用 Sharp Zaurus PDA 进行黑客攻击

-   本章内容：
  -   Kismet
  -   Wellenreiter II
  -   Nmap
  -   Openmapfe
  -   Bing
  -   OpenSSH
  -   Hping2
  -   VNC 服务器
  -   Keypebble VNC 查看器
  -   Smbmount
  -   Topdump
  -   Wget
  -   ZEthera al
  -   zNessus
  -   MTR
  -   Dig
  -   Perl
  -   Zaurus 在线资源
  -   总结

Sharp Zaurus PDA（个人数字助理）设备运行嵌入式版本的 Linux 操作系统。PDA 内置对各种紧凑型 802.11 网络卡片的支持。这些特性加上 PDA 的小巧外形，使 Zaurus 成为一个强大的设备。在本章中，我们将探讨许多已经移植到 Zaurus 架构上的 Linux 安全工具。在可能的情况下，我们会提供屏幕截图以满足您的好奇心。

### KISMET

Kismet 是一种无线网络嗅探器，可用于捕获和查看区域内无线网络的信息。入侵者不再需要携带笨重的笔记本电脑来发现某区域周围的无线网络。只需要 Zaurus PDA，以及可从 **http://kismetwireless.net/code/** 下载 Kismet 移植版即可。一旦你下载、解压并解包从该 URL 获得的 tar.gz 文件，你会发现在创建并生成的 kismet-arm 目录中有一个 ipk 包文件。使用文件管理器打开此文件以安装 Kismet，当其在 PDA 上运行时，效果如下所示。

![](img/77287f6ef97ef0bed6e23f6610950d06_232_0.png)

Kismet 的 GUI 界面可在 **http://sourceforge.net/projects/kismet-qt/** 获取。

