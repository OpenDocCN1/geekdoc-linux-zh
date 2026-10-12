
# OffSec 使用 Kali Linux 进行渗透测试

在这次攻击中，黑客通过一个被破解的密码访问了殖民管道的网络。如果通过确保所有面向互联网的资源启用多因素身份验证（MFA）并禁止密码重复，这种攻击是可以避免⁴⁹或至少降低概率的。

**凭据滥用：** 当攻击者获取了合法凭据时，允许他们登录原本无法访问的机器或服务，就会发生凭据滥用。通常，攻击者能够猜出用户密码是因为密码是可预测的或弱的。

2020 年 12 月，在 SolarWinds Orion 平台（一种基础设施监控和管理工具）发现了许多恶意更新。这些恶意更新允许恶意软件安装在所有安装了更新的 SolarWinds 客户环境中，并导致许多此类客户遭到破解，包括大学、美国政府机构和其他主要组织。

作为供应链攻击，这影响了大约 18,000 名 SolarWinds 客户，并导致部分客户（包括政府机构和其他大公司）泄密。根据 SolarWinds 首席执行官 Kevin Thompson 的说法，这次攻击源于一个在 Github 上意外暴露的弱密码⁶¹。通过确保密码足够强并在互联网上监控泄露的密钥，这种攻击是可以避免⁵²的。网络安全局（CISA）还表示，通过阻止 SolarWinds Orion 服务器的出站互联网流量可以缓解这种攻击。

**身份验证绕过：** 虽然凭据滥用允许攻击者通过合法验证登录，但身份验证绕过允许攻击者忽略或绕过身份验证协议。

与 SolarWinds 攻击类似，2021 年 7 月⁵³ 检测到一次攻击，其利用了软件供应商 Kaseya 的 VSA 远程管理工具中的漏洞。攻击者能够绕过远程工具的身份验证，最终通过多次攻击从被破解的客户虚拟系统管理员（VSA）向服务器推送了 REvil 勒索软件。

由于这次攻击针对了多个托管服务提供商（MSP），其潜在范围不仅包括 Kaseya 的 MSP 客户，还包括这些 MSP 的客户。根据 Brian Krebs⁵⁴ 的说法，该漏洞在事件发生前至少已知的三个月。通过以紧急且及时的方式优先修复已知漏洞，这种攻击是可以避免的。

## 3.3 CIA 三元组

本单元涵盖了以下学习目标：

- 理解为什么保护信息的机密性很重要

> 49 (CISA, 2022), https://www.cisa.gov/stopransomware/how-i-protect-against-ransomware

> 50 (BBC, 2020), https://www.bbc.com/news/technology-55321642

> 51 (ZDNet, 2021), https://www.zdnet.com/article/colonial-pipeline-ransomware-attack-everything-you-need-to-know/

> 52 (SC Media, 2021), https://www.scmagazine.com/

> 53 (ZDNet, 2021), https://www.zdnet.com/

> 54 (Krebs, 2021), https://krebssecurity.com/

让我们考虑一个针对机密性的攻击示例、其影响，并理解如何预防或缓解它。2021年8月，T-Mobile ⁵⁷ 宣布黑客访问了与超过500万现任、前任及潜在客户相关的数据。虽然没有获取到支付信息、密码或PIN码，但部分数据包括姓名、出生日期、社会安全号码以及身份证/驾执照信息。这些数据随后在暗网上被提出来出售。

该攻击影响了现任、前任及潜在客户个人信息的机密性。这些信息的机密性随后因在暗网上供购买而遭到进一步破坏。这还导致了 T-Mobile 进一步的声誉损害，因为该攻击是近期十次泄露事件之一。

关于攻击者所使用的方法⁶，信息有限；他们声称首先攻破了一个路由器，以访问包括影响客户数据的数据库或多个数据库在内的100多台服务器。通过确保所有面向互联网的资源都经过了正确的配置、补丁和更新，监控异常行为并实施更好的网络分，这种泄露本可以避免。

驾执照等私密文档应当是机密的，因为它们包含了识别身份的信息。然而，公司产生的所有信息并不一定都是机密的。例如，T-mobile 的董事成员在其网站上是公开的。如果攻击泄露了信息，这并不构成对机密性的破坏。

### 3.3.2 完整性

如果一个系统存储的信息和功能仅是所有者预期的内容，那么该系统就具有完整性。完整性关注维护数据和服务的准确性和可靠性。仅仅通过猜测密码登录用户的社交媒体账号并不是针对完整性的攻击。然而，如果攻击者开始发布消息或删除信息，这将变成一种针对完整性的攻击。针对完整性的常见攻击是任意代码执行。⁵⁹

在2022年1月，⁶⁰ 研究人员发现了一种名为 WhisperGate 的新型擦除器，正被用于攻击乌克兰目标。该恶意软件有两个阶段：第一阶段覆盖主引导记录 (MBR) 以显示勒索软件说明，而第二阶段下载进一步的恶意软件覆盖具有特定扩展名的文件，使其损坏且无法恢复。这种攻击通过不可逆的方式覆盖文件，影响了受影响系统⁶¹数据的完整性，并有效地删除了它们。

在建议中，微软建议潜在目标采取以下步骤来保护自己：对可能受损的凭据启用 MFA，在 Microsoft Defender 中启用受控文件夹访问 (CFA) 以防止 MBR/VBR 篡改，使用提供的 IoCs 搜索泄露，检查并验证所有远程访问的身份验证活动，并调查其他异常活动。CrowdStrike 发布了关于攻击技术细节的更多信息。² 简单来说，企业保护完整性很重要，因为其他业务和消费者需要信任企业掌握的信息。

⁵⁷(T-Mobile, 2021). https://www.t-mobile.com/news/network/additional-information-regarding-2021-cyberattack-investigation

⁵⁸(Zennet, 2021). https://www.zennet.com/article/e-hack-everything-you-need-to-know/

⁹(Wikipedia, 2021). https://en.wikipedia.org/wiki/arbitrary_code_execution

⁶⁰(Microsoft, 2022). https://www.microsoft.com/security/blog/destructive-malware-targeting-ukrainian-organizations/

⁶¹(Cisco, 2022). https://talosintelligence.com/2022/01/ukraine-campaign-deliveries-defragment.html

PWK - © 2023 OffSec Services Limited. All rights reserved.

### 3.3.3 可用性

如果应当访问该系统的人可以访问，则该系统被认为是可用的。想象一个攻击者获取了某个社交媒体账号并发布了他们选择的某些内容。到目前为止，这构成了对机密性和完整性的攻击。如果攻击者更改了用户密码并阻止其登录，这也将变成针对可用性的攻击。针对可用性的常见攻击是拒绝服务。⁶³

2022年2月24日，在俄罗斯入侵乌克兰之初，Viasat ⁶⁴ 卫星宽带服务遭受了拒绝服务 (DoS) 攻击，导致乌克兰客户（包括乌克兰政府和军队）的卫星互联网中断。这次攻击利用了一种当时名为 AcidRain 的新型擦除器恶意软件。

这次攻击的影响⁶⁵ 是 Viasat 的卫星互联网在入侵瞬间在乌克兰暂时不可用，中断了通信和协调。关于这一过程如何演变的信息很少。Viasat 表示，一个 VPN “配置错误”允许了初始访问。尽管尚不清楚具体的配置错误是什么，但通过确保正确的 VPN 配置本可以避免这次攻击。

这种攻击可能是可以避免的——尽管我们承认在遵循防御持续性威胁 (APT) 的通用指导方面存在众为人知的困难。⁶⁶ 这些指导建议了对自己的环境进行完全可见、参与威胁情报以及防止威胁狩猎等建议。

### 3.3.4 组织目标与 CIA 三要素的平衡

在考虑本节之前，让我们扩大视野，考虑优先考虑 CIA 三要素如何影响一个组织。在实践中，需要考虑的一个重要细微差别是，安全控制措施本身有时会对可用性产生不利影响。极强的安全性对于组织来说并不总是最优的。如果安全性高到让用户无法使用系统，或对系统感到沮丧，可能会导致效率低下。

将安全性与可用性平衡是一个关键的过程。

⁶²(CrowdStrike, 2022). https://www.crowdstrike.com/technical-analysis-whisper-gate/

⁶³(Wikipedia, 2021). https://en.wikipedia.org/wiki/Denial_of_service

⁶⁴(Viasat, 2022). https://www.viasat.com/blog/acidrain-a-wiper/

⁶⁵(Sentinel One, 2022). https://www.sentinel.com/labs/acidrain-a-wiper/
