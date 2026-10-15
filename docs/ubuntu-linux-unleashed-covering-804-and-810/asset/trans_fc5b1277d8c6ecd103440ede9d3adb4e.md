

## 参考

- http://www.mono-project.com/—Mono 项目的主页上充满了帮助你入门的信息。你也可以从这里下载新的 Mono 版本，如果你急需的话。
- http://www.monodevelop.com/—MonoDevelop 项目有自己的网站，那里是查找更新的最佳地方。
- http://www.icsharpcode.net/OpenSource/SD/—MonoDevelop 起初是 SharpDevelop 的移植版。如果你恰好在 Windows 上双启动，这可能会对你非常有用。
- http://msdn.microsoft.com/vcsharp/—我们在这本书中很少刊登微软的网址，但这个很重要：它是其 C# 项目的主页，可以被视为 C# 本身的精神家园。
- Jesse Liberty 的 *Programming C#*（O'Reilly，ISBN 0-596-00699-3）内容精炼、全面，且价格具有竞争力。
- 如果你时间非常紧张，想要获得最大程度的细节（ admittedly，可读性相当有限），你应该尝试 *The C# Programming Language*，该书由 C# 的创造者 Anders Hejlsberg 共同撰写（Addison-Wesley，ISBN：0-321-3344-4）。
- 对于一本更通用的关于 .NET 框架及其提供的全部功能的书籍，你可能会发现 *.NET Framework Essentials*（O'Reilly，ISBN：0-596-00505-9）有用。

## PART VI

## Ubuntu 维护

### 本部分内容

- CHAPTER 28 Securing Your Machines
- CHAPTER 29 Performance Tuning
- CHAPTER 30 Command Line Masterclass
- CHAPTER 31 Managing Software
- CHAPTER 32 Kernel and Module Management

## CHAPTER 28

## Securing Your Machines

### 本章内容

- Understanding Computer Attacks
- Assessing Your Vulnerability
- Protecting Your Machine
- Viruses
- Configuring Your Firewall
- Forming a Disaster Recovery Plan
- Keeping Up-to-Date on Linux Security Issues
- Reference

没有连接到互联网的家庭电脑是 100% 安全的。如果这些信息不让你担心，那应该！虽然没有办法阻止一个决心入侵你的电脑或网络的严重黑客，但有办法让他的入侵更困难，并在他入侵时提醒你。

在本章中，我们讨论保护 Linux 机器的所有方面。你可能想知道为什么我们没有在书中适当的地方分散这些信息，但原因很简单：如果 Linux 出现安全问题，你知道可以翻到这一页开始阅读，而不必搜索或试图回忆在哪里看到过提示。你需要的一切都在这一章中，我们强烈建议你从头到尾阅读。

### 内核内置保护

Linux 内核内置了许多网络和低级保护服务。这些服务可以通过 sysctl 命令启用、禁用或显示，也可以通过向 /proc 目录下的内核进程文件回显一个值（通常是 1 或 0 以打开或关闭服务）来实现。

### Understanding Computer Attacks

计算机攻击可以按多种方式划分，但也许最简单的是内部攻击，即

- 2. 为服务器配置最大安全性。只安装你需要的，只运行你必须运行的，并配置本地防火墙。
- 3. 保护对服务器的物理访问。
- 4. 制定最坏情况的策略。
- 5. 及时了解安全新闻。

这些内容在以下各节中都有介绍，每一项都与其他项同样重要。

### Assessing Your Vulnerability

人们常犯的一个错误是认为打开防火墙就安全了。这不是事实，事实上从来就不是。每个系统都有独特的安全需求，花时间定制其安全布局将为你提供最大程度的安全性和最佳性能。

以下列表总结了最常见的错误：

- Installing every package—你打算将机器用作 DNS 服务器吗？如果不是，为什么要安装 BIND？通过 Synaptic 检查，确保你只有需要的软件。
- Enabling unused services—你想远程管理机器吗？你想让人们上传文件吗？如果不是，关闭 SSH 和 FTP，因为它们只是增加了不必要的攻击向量。这同样适用于许多其他服务。
- Disabling the local firewall on the grounds that you already have a firewall at the perimeter—在安全方面，纵深至关重要：某人需要破解的层数越多，她放弃或被抓的可能性就越高。
- Letting your machine give out more information than it needs to—许多机器默认配置为公开软件名称和版本号，这只是给黑客提供帮助。
- Placing your server in an unlocked room—如果是这样，你现在就可以关掉它，省去担忧。唯一的例外是如果你公司的所有员工都快乐且值得信赖。但为什么要冒这个险呢？
- Plugging your machine into a wireless network—除非你需要，否则避免这样做，特别是如果你的机器是服务器。永远不要将服务器插入无线网络，因为它充满了安全问题。

在排除这些问题后，你才触及真正的难题：你的服务器上有哪些攻击向量是开放的？在互联网术语中，这归结为哪些服务面向互联网以及它们运行在哪些端口上。

通常使用两种工具来确定你的漏洞：Nmap 和 Nessus。Nessus 扫描你的机器，查询正在运行的服务，将其版本号与漏洞列表进行核对，并报告问题。

