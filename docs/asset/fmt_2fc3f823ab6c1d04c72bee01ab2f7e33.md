
如第 8 章所述，`printing` 设置不必设置为 `bsd`，可以设置为任何有效选项。

一旦你完成了这些添加，你将需要重新启动 UNIX 系统上的 SAMBA 服务。重新启动服务后，你应该能够从 Windows 客户端打印到 `/etc/printcap` 文件中定义的任何打印机。

请参阅第 8 章以获取此处讨论的 SAMBA 选项的更详细描述。你可能还想查阅 SAMBA 文档以获取更多信息。

### 将客户端连接到 SAMBA 共享打印机

连接到 SAMBA 打印机几乎与连接到 Windows 2000 打印机相同。按照上述步骤连接到 SAMBA 打印机，但请记住以下几点：

- 你必须在本地安装打印机驱动程序，因为它不是 SAMBA 服务器共享的一部分。
- 你必须使用有效的 UNIX 用户名和密码登录 Windows 才能连接到打印机，或者 SAMBA 服务器必须能够针对 Windows 2000 域控制器进行身份验证（这是我们在第 8 章中推荐的配置）。
- 你必须使用 `\\SERVER\share` 语法连接到打印机共享。

一旦你连接到 SAMBA 打印机，它的行为应与从 Windows 2000 服务器共享的打印机一样。

## 总结

尽管支持打印通常令人沮丧，但它是必要的。数字预言家预测的无纸社会尚未实现。在本章中，我们讨论了 UNIX 和 Windows 2000 打印的基础知识。

## BSD 与 SYSV

UNIX 中的打印服务分为两个阵营：BSD 和 SysV。总体而言，BSD 更易于使用，但 SysV 功能更多。近年来，各 UNIX 厂商推出了针对其变体的专用打印服务器。这些服务器通常只能与有限数量的 UNIX 变体良好配合。AIX 提供了最全面的打印服务包。UNIX 中的另一个选择是第三方 LPRng 包。它是免费的，并且支持大多数 UNIX 变体。

## MICROSOFT 打印服务

Windows 世界中的打印要好得多。微软提供的打印服务高效且易于安装。共享打印机的能力是该服务的透明组成部分。微软还为 UNIX 提供了打印服务，允许 UNIX 系统使用 Windows 2000 打印服务。
SAMBA 是一个第三方包，允许 UNIX 系统将其打印机与 Windows 系统共享。SAMBA 使用广泛，并且可免费获得。

## 管理

尽管管理任务枯燥乏味，但它们无疑是最关键的。本书这一部分描述的任务将直接涉及用户，或支持用户所需的工具。创建用户账户（以及删除它们）显然非常重要。备份和性能调优也会影响用户环境的质量。极易忘记，大多数系统和网络存在的理由是为了支持用户执行的一组活动。我们认为，集成基础设施的最终考验在于其满足使用者需求的能力。没有适当的管理，系统稳定性无法维持。同样，在分布式环境中，管理策略对于支持软件资源和安全是必要的。

## 安全

### UNIX

### WINDOWS 2000

- 安全分析
- 对手与攻击
- 保护
- 预防
- 检测

> 在全球数据通信不断变化、互联网连接价格低廉、软件开发节奏快速的世界里，安全问题变得越来越突出。安全现在已成为基本要求，因为全球计算本质上是不安全的。例如，当你的数据通过互联网从 A 点传输到 B 点时，它可能途经多个其他节点，给其他用户拦截甚至篡改你的数据的机会。甚至系统上的其他用户也可能恶意地将你的数据转变为你未曾预期的内容。

Dave Wreski, Linux Security Administrator's Guide, 1998

## 安全分析

不存在绝对安全的系统。计算机和网络安全是在保护与可用性之间取得平衡。系统保护得越严格，用户使用起来可能就越困难。系统交互的不断变化，无论是硬件还是软件，也加剧了维护安全系统的难题。因此，安全是一个目标，而通往它的旅程是艰难的。在开始时，你必须了解计算系统有多脆弱。Dave Wreski 在前面引用的在线书籍中，使用以下几点来说明我们计算环境的不安全本质：

- 计算机应急响应团队持续报告计算机漏洞和利用的增加。
- TCP 和 UDP，即构成互联网的协议，在 30 多年前创建时，并没有将安全作为首要优先事项。
- 一个主机上的软件版本与另一个主机上的相同版本软件具有相同的漏洞。利用这一信息，入侵者可以使用相同的攻击方法利用多个系统。
- 许多管理员甚至没有采取保护其站点所需的基本安全措施，或不了解实施某些服务的后果。许多管理员没有得到额外的时间来整合必要的安全措施。

将平衡行为与固有漏洞结合起来，IT 系统的安全性可以定义为 *组织为保持 IT 系统处于一种状态而部署的手段，在该状态下，同一组织能够以预定且一致的方式访问 IT 系统。*

对 IT 系统安全性的更实际看法是，安全是四种行动组合的结果：

**Security = Protection + Prevention + Detection + Recovery**

- **Protection** 是安全策略的实施。这包括为维护安全目的而部署到基础设施中的程序和技术。
- **Prevention** 是任何旨在降低安全风险水平、即增加对手的难度级别的行动

break into the IT system. Such actions can have a direct effect on the protection and detection components.

**Detection** is any action whose goal is to detect an intrusion and track down the opponent with the intent to prosecute.

**Recovery** corresponds to the action to take when it is too late and how to recover when you have lost the race and have become the victim of an intrusion. Good methods and a minimum of action in the three areas of protection + prevention + detection are likely to protect your organization from 90-95% of all possible intrusions. However it is important not to neglect the last 5% as these are generally the most dangerous. The final 5% are those types of attacks that can only be attempted by an intruder with a high level of knowledge, and with that increased knowledge, the amount of potential damage an intruder can inflict also increases.

Before going further into this journey, here are some thoughts that you may want to keep in mind while working with security:

The security of an IT system can be addressed from a technical point of view (patching security holes, restricting access), but overall it has to be defined by a policy. The policy must define what a user can/cannot do inside the IT system (for example, what system(s) they cannot access, what commands they can execute, etc.).

An analogy can be established between the concepts of quality and security of an IT system. Security represents a cost (loss) for the organization. Enforcing a security policy requires time and dedicated means, and it can have an indirect impact on productivity (users may have to follow some rules which may slow them down in their use of the IT system). But, not doing security can lead to greater costs, as will be explained later.

The system administrator, when working on security, has to be paranoid by nature. Security is a way of life, and must be present in every action done by the system administrator. Doing something (like setting up a server) without paying attention to security or saying, “I have no time right now, I will secure the system later.” is wrong, as “later” may become “too late”.

## Know Your Opponents and Types of Attacks

As generally stated by the military: The preparation of a good defense requires good knowledge of the opponent.

## WHO IS THE INTRUDER?

Before going further, it is important to understand the jargon and slang used on the “dark side” of system administration. Speaking your enemy’s language is the first step to understanding how they think. A good starting point is:

```
