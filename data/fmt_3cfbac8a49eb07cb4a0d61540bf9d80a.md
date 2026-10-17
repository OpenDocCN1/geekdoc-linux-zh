
列表 232 - 来自 HR137 的入站反向 shell

列表 232 显示我们成功通过库文件和快捷文件收到了反向 shell。

非常棒。

我们可以将此技术与我们之前的 Office 宏攻击或任何其他类型的客户端攻击结合起来。
在在本节中，我们学习了库文件（Library files）以及如何将其武器化，作为在客户端攻击中交付可执行文件的有效阶段。作为第二阶段，我们使用快捷文件下载 PowerShell 并启动反向 shell。库文件是交付第二阶段负载的极佳方法，且不会暴露于垃圾邮件过滤器等安全技术。

⁴⁵⁰ (Samba, 2022), https://www.samba.org/samba/current/man-html/smclient.1.html

PWK - © 2023 OffSec Services Limited. All rights reserved.

# 11.4 总结

客户端攻击向量通常是获取不可路由内部网络中初始立足点的有效方法。它们特别隐蔽，因为它们利用了现有客户端软件的漏洞或功能。

在本模块中，我们学习了如何获取目标信息以准备客户端攻击。然后，我们利用 Microsoft Office 宏、Windows 库文件和快捷文件来获取代码执行并接收反向 shell。

> $^{541}$ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Antivirus_software
> $^{542}$ (Crowdstrike, 2022), https://www.crowdstrike.com/cybersecurity-101/malware/types-of-malware/
> $^{543}$ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Intrusion_detection_system

# OffSec

由于目标针对两种不同的杀毒引擎，其差异巨大。在 2014 年，一种名为 YARA⁵54⁴ 的签名语言开源，允许研究人员查询 VirusTotal⁵54⁵ 平台甚至将自己的恶意软件签名集成到杀毒产品中。VirusTotal 是一个搜索引擎，允许用户搜索恶意软件或提交新样本并针对多个杀毒产品进行扫描。

由于签名是基于已知威胁编写的，杀毒产品只能对已经过审核并记录的恶意软件进行检测或响应。然而，现代杀毒解决方案随 Windows Defender⁵⁴⁴⁶ 发行，并带有一个机器学习（ML）⁵⁴⁷ 引擎，当在系统中发现未知文件时会查询该引擎。由于机器学习引擎在云端运行，它们需要连接到互联网，而这对于内部企业服务器来说并不是选项。此外，构成杀毒软件的许多引擎不应从系统的其他部分占用过多计算资源，可能会影响系统的可用性。

为了克服这些杀毒的局限性，端点检测与响应（EDR）⁵⁴⁸ 解决方案近年来得到了演进。EDR 软件负责生成安全事件遥测数据并将其转发到安全信息事件管理（SIEM）⁵⁴⁹ 系统，该系统收集来自每台公司主机的数据。这些事件由 SIEM 记录，以便安全分析师团队能够全面了解影响组织的过去或正在进行的攻击。

尽管 EDR 解决方案包含杀毒组件，但杀毒软件和 EDR 并非互斥的，因为它们通过增强的可见性和检测能力相互互补。最终，它们的部署应根据组织的内部网络设计和当前的安全态势进行评估。

# 12.1.2 杀毒引擎和组件

现代杀毒软件通常围绕以下组件设计：

- 文件引擎
- 内存引擎
- 网络引擎
- 反汇编器
- 模拟器/沙箱

> ⁵⁴⁴ (Wikipedia, 2022), https://en.wikipedia.org/wiki/YARA
> ⁵⁴⁵ (VirusTotal, 2019), https://www.virustotal.com/#home/upload
> ⁵⁴⁶ (Microsoft, 2022), https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-antivirus?view=windows365-worldwide
> ⁵⁴⁷ (Microsoft, 2022), https://www.microsoft.com/security/blog/2017/08/03/windows-defender-apt-machine-learning-detecting-new-and-usual-breach-activity/
> ⁵⁴⁸ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Endpoint_detection_and_response
> ⁵⁴⁹ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Security_Information_and_event_management

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

使用 Kali Linux 进行渗透测试

- 浏览器插件
- 机器学习引擎

上述每个引擎都与签名数据库同时工作。上述每个引擎与签名数据库同时工作，将特定事件标记为良性、恶意或未知。当引擎执行计划扫描时，它只是是解析整个文件系统并将每个文件的元数据发送到引擎。相反，实时扫描涉及检测并响应新操作，例如从网站下载恶意软件。这就是为什么现代杀毒软件需要在内核态和用户态中运行，以验证整个操作系统范围。

内存引擎在运行时检查每个进程的内存空间，寻找已知签名或可能导致内存注入攻击的可疑 API 调用，我们稍后会发现。

正如名称所示，网络引擎检查本地网络上的入站和出站流量。一旦签名被标记，网络引擎可能会阻止恶意软件与其命令与控制（C2）¹服务器通信。

为了干扰检测，恶意软件通常通过自定义程序采用加密和解密来隐藏其真实性质。杀毒软件通过反汇编壳或加密程序并将恶意软件加载到沙箱来对抗这一点。

反汇编器引擎负责将机器码转换为汇编语言、重建原始代码段并识别任何编码/解码程序。沙箱是杀毒软件中的特殊隔离环境，恶意软件可以在其中安全地加载和执行而不会对系统造成潜在危害。一旦恶意软件在模拟器中解包/解码，就可以针对任何已知签名进行彻底分析。

由于浏览器受到沙箱保护，现代杀毒软件通常采用浏览器插件以获得更好的可见性，并检测浏览器内部执行的恶意内容。

此外，机器学习组件是当前杀毒软件的重要部分，因为它通过依赖云增强的计算资源和算法来检测未知威胁。

# 12.1.3 检测方法

正如前面提到的，杀毒签名和范围可能会根据其构建的引擎而不同，但它们具有相同的目的，即唯一标识特定的威胁或恶意软件。

在本节中，我们将探讨以下杀毒检测方法并解释它们如何协同工作。

- 基于签名的检测

> ⁵⁵⁰ (Microsoft, 2022), https://docs.microsoft.com/en-us/windows-hardware/drivers/ifs/filter-manager-concepts
> ⁵¹¹ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Botnet#Command_and_control

PWK - ©2023 OffSec Services Limited. All rights reserved.

# OffSec

使用 Kali Linux 进行渗透测试

- 基于启发式的检测
- 行为检测
- 机器学习检测

基于签名的反病毒检测主要被认为是一种受限列表技术。换句话说，系统会对文件系统进行已知恶意软件签名的扫描，如果检测到任何签名，就会对问题文件进行隔离。

签名可以是文件本身的哈希值，也可以是多个模式的集合，包含仅属于该特定恶意软件的特定二进制值和字符串。

仅依赖文件哈希作为唯一检测机制是一种弱的策略，因为改变文件的中的比特位就会导致完全不同的哈希值。

例如，我们在本地 Kali 机器上创建了一个包含字符串“offsec”的文本文件。让我们在文件名之前，通过 `xxd -b` 参数导出其二进制表示形式。

```
kali:~ xxd -b malware.txt

00000000: 01101111 01100110 01100110 01101111 01100101 01100111 offsec

00000006: 00101010
```

列表 233 - 使用 `xxd` 查看文件内容

我们通过 `xxd` 工具显示了文件的内容。输出左侧列显示二进制偏移量，中间列显示实际的二进制表示，最右侧显示 ASCII 翻译。我们还用红色标亮了字母“c”的二进制表示。它的目的很快就会明确。

现在，由于这是真实的恶意软件，我们需要计算文件的哈希值，我们可以通过 `sha256sum` 来。

```
kali:~ sha256sum malware.txt

c316e96c9c8f22fd45e8a990c1cfba4ae85a3a09e7c40598a0ba2383ff63510e malware.txt
```
