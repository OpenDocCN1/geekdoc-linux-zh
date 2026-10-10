
`RpcAddPrinterDriverEx`包含标志。我们可以控制此值，在未打补的 `spoolsv.exe` 版本中，它缺少对关联注册表的检查（`NoWarningNoElevationOnInstall` 和 `RestrictDriverInstallationToAdministrators`）。我们可以有效地绕过对 `ValidateObjectAccess` 的调用，直接进入 `InternalAddPrinterDriverEx`。第 28 行将 `v12` 设置为 0。第 29 行如果 `a4` 中的第 15 位未设置，则 `v12` 等于 `a7`，这可能会将 `v12` 的值从 0 改变。在第 31 行，如果 `v12` 被设置（非零），则调用 `ValidateObjectAccess` 并检查是否设置了 `SeDebugPrivilege` 权限。如果我们能让 `a4` 的第 15 位开启，那么在第 29 行就不会进入该块，而是调用 `InternalAddPrinterDriverEx`。这实际上允许攻击者绕过检查并安装驱动程序，从而以 `NT AUTHORITY\SYSTEM` 用户的身份执行代码。在本文写作期间，仍有额外的发现和修复进行；然而，这是主要的可利用漏洞之一。

### 总结

本章介绍了二进制差分分析（binary diffing）以及可以帮助加速分析的各种工具。我们查看了一个简单的应用程序概念验证示例，然后查看了一个真实的补丁，以定位代码更改、验证我们的假设并验证修复。这是一种后得的技能，与你调试和阅读反汇编代码的经验密切相关。你做得越多，在识别代码更改和潜在已修复漏洞方面就越强。有时，从 Windows 的早期版本或生成版本开始，以及使用 32 位版本而不是 64 位版本会更容易，因为反汇编代码通常更容易读。许多漏洞跨越了多个 Windows 版本。微软通过另一个补丁静悄引入代码更改的情况也未未。这在不同的 Windows 版本之间有时有所不同，对比一个 Windows 版本可能比对比另一个版本产生更多信息。

### 延伸阅读

- [BinDiff Manual (Zynamics)](www.zynamics.com/bindiff/manual/)
- “Darungrim: A Patch Analysis and Binary Diffing Tool” www.darungrim.org
- [PatchExtract] gist.github.com/wumb0/306f97dc837c6f53b9f865f60b4b5
- [delta_patch] gist.github.com/wumb0/9542469e3915953f7ae02d63998d2553
- “Feedback-Driven Binary Code Diversification” (Bart Coppens, Bjorn De Sutter, and Jonas Maebe) users.eligent.be/~brdsutte/research/publications/2013TAoppens.pdf
- “Fight against 1-day exploits: Diffing Binaries. Anti-Diffing Binaries” (Jeong W Oh) www.blackhat.com/presentations/bh-usa-09/OH/BHUSA09-Oh-DiffingBinaries-PAPER.pdf
- [patchdiff2 (Nicolas Pouvesle)] code.google.com/p/patchdiff2/
- [Back2TheFuture] github.com/SafeBreach-Labs/Back2TheFuture
- [BLUEHEXAGON threat advisory] bluehexagon.ai/blog/threat-advisory-cve-2021-1675-aka-printmare/

### 参考文献

- 1 Zynacs, BinDiff Manual, 2017, https://www.zynacs.com/binddiff/manual/.
- 2 Jaime Ondrusek et al. “Windows Updates Using Forward and Reverse Differentials,” Microsoft 365, Microsoft, 2020, https://docs.microsoft.com/en-us/windows/deployment/update/psfxwhitepaper.
- 3 Jaime Geiger, “Extracting and Diffing Windows Patches in 2020.” wumb0in Full Atom, 2020, https://wumb0.in/extracting-and-diffing-ms-patches-in-2020.html.
- 4 Microsoft. “Us2007026053a1: Inter-Delta Dependent Containers for Content Delivery.” Google Patents, Google, 2006, https://patents.google.com/patent/US20070260653.
- 5 Barry Golden and Amy Viviano. “Local Print Provider.” Microsoft Docs, Microsoft, 2017, https://docs.microsoft.com/en-us/windows-hardware/drivers/print/local-print-provider.

## 第四部分

## IoT 黑客攻击

- 第19 章 待攻击的物联网
- 第 20 章 剖析嵌入式设备
- 第 21 章 利用嵌入式设备
- 第22 章 软件定义无线电

## 待攻击的物联网

在本章中，我们涵盖了以下主题：

- 物联网 (IoT)
- Shodan IoT 搜索引擎
- IoT 蠕虫：时间问题

本章涵盖了连接网络设备的主题，被称为物联网（IoT）。“Things”一词最早是在1999年在麻省理工学院（MIT）的一场演讲中由 Kevin Ashton 提出的。1 2008年，连接设备的数量超过了地球上的人口，达到了 80 亿。

而且 Z-Wave、蓝牙和蓝牙 LE 无法直接连接互联网；它们必须通过网关设备（如手机或智能网桥/控制器）进行转发。

## 6LoWPAN

低功耗无线局域网物联网协议 6（6LoWPAN）正成为一种通过 802.15.4 (Zigbee) 网络传输 IPv6 数据包的有效方法。它可以运行在 Zigbee 以及其他物理网络上，因此它与 Zigbee 存在竞争，但某些人认为它完善了 Zigbee，因为它允许与其他连接 IP 的设备进行连接。

## 通信协议

IoT 有多种通信协议——多到列不完——但这里是常用的几种：

- 消息队列遥传传输 (MQTT)
- 可扩展消息和存在协议 (XMPP)
- 实时系统数据分布服务 (DDS)
- 高级消息队列协议 (AMQP)

## 安全关注

传统的机密性、完整性和可用性观点适用于安全设备，但通常方式并不相同。对于传统的网络设备，通常会优先考虑机密性、完整性，然后是可用性。然而，对于连接设备，顺序通常是反过来的，优先考虑可用性、完整性，然后是机密性。当我们考虑一个通过蓝牙连接到用户手机并接入互联网的嵌入式医疗设备时，这种范式很容易理解。首要关注点是可用性，然后是完整性，最后是机密性。尽管我们讨论的是敏感的医疗信息，但如果设备无法访问或不被信任，就没有必要担心机密性。

然而，还有一些额外的安全关注点：

- 漏洞可能难以修复，甚至无法修复。
- 小尺寸设备资源有限且受电量限制，通常会导致加密等安全控制无法实施。
- 缺乏用户界面导致“眼不见为不净”。它们通常在线多年，而所有者几乎很少去管它们。
- 像 MQTT 等协议具有局限性，包括没有加密、通常没有身份验证以及安全配置繁琐，你将在本章稍后的部分看到。

### Shodan IoT 搜索引擎

Shodan 搜索引擎专注于连接互联网的设备，并逐渐被称为物联网（IoT）。必须意识到，这并不是你父亲那辈使用的 Google。Shodan 搜索的是横幅信息（banners），而不是网页。特别是，Shodan 会扫描互联网寻找它识别的横幅，然后索引这些数据。你可以提交自己的横幅指纹和 IP 进行扫描，但这需要付费许可。

## Web 界面

如果你想浪费掉一个下午，甚至整个周末，只需去 `https://images.shodan.io` 即可（这需要每年 49 美元的会员费）。你可能会发现一个正在午睡的大胖宝宝，如接下来所示。（这只是笑话；这显然是一个疲惫的成年人和他们的狗）。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_672_0.png)
