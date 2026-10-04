

## ISS 扫描器

Internet Security Systems (ISS) 是最早营销漏洞扫描器的机构之一，现在该扫描器已成为 ISS Safe Suite 安全解决方案（www.iss.net）的一部分。它提供从基于 Windows 的扫描平台进行基于网络的漏洞评估和扫描。Internet Scanner 包含一个执行漏洞检查并识别设备的扫描引擎组件、一个能够处理各种信息级别生成报告的报告环境，以及一个存储漏洞信息以及 Internet Scanner 和用户界面使用的其他信息的数据库。Internet Scanner 实际上有两个接口：一个标准的 Windows GUI 和一个用于批量作业设置和调度的命令行模式。GUI 如图 3.2 所示。Internet Scanner 带有一大套预配置策略模板，这些模板根据每次扫描中的探测方式进行排列。以下是 Internet Scanner 的某些功能：

- 自动 X-Press 更新：Internet Scanner 允许你轻松地快速更新检查项。
- 策略编辑器：Internet Scanner 策略编辑器允许你轻松地搜索和排序用于扫描的漏洞检查，并将一组检查项保存到自定义模板中。
- 与其他 ISS 产品集成：Internet Scanner 还可以与 ISS Database Scanner 配合进行扩展数据库审计、企业报告产品 SafeSuite Decisions 以及其他 ISS 产品协同工作。
- 报告选项：Internet Scanner 使用 Crystal Reports 引擎生成各种报告类型。

## 图 3.2 扫描期间的 Internet Scanner 界面

![](img/729efc56f204a2ebffb8295c3a2dfdfb_84_0.png)

## 寻找高危漏洞 (HSV) • 第 3 章

## Typhon II

Typhon II (www.nextgenss.com) 是 Typhon 的新版本，曾被称为 Cereus Internet Scanner。Typhon II 是一种轻量级基于 Windows 的扫描工具，可生成 HTML 报告并包含一个防御模块。图 3.3 显示了 Typhon II 的主界面。

## 图 3.3 Typhon II 主界面

![](img/729efc56f204a2ebffb8295c3a2dfdfb_85_0.png)

NGS Software 通过名为供应商通知警报（VN）的系统发布每个新漏洞，其中提供的公开信息很少。通常，其他供应商获得的信息不足以创建漏洞检查；然而，如果 NGS Software 发现了这些未公开的漏洞，Typhon II 将拥有这些漏洞的检查项。Typhon III 计划于 2003 年初发布。以下是 Typhon 的某些功能：

- 多于 320 个 Web 检测
- 一个 Oracle 数据库模块
- 轻量级目录访问协议（LDAP）和安全外壳（SSH）模块
- 对安全 HTTP（HTTPS）、LDAP 和其他基于 SSL 的服务的支持

## Retina

eEye 的 Retina (www.eEye.com) 是市场上较新的扫描产品之一。它具有诸如常见攻击和黑客方法等功能，用于发现新的、此前未报告的漏洞。eEye 开发了智能扫描技术，这些技术在正常扫描操作期间是非侵入性的，并且不会通过利用进行测试；这应该大大减少扫描器在识别 HSV 时导致的系统崩溃。为了保持特征库更新，eEye 实施了自动更新功能，通过 HTTP 或 HTTPS 从互联网获取最新、强大的信息。Retina 的漏洞数据库几乎每天更新。

试用版可以下载并使用 15 天，无需任何终端用户费用。图 3.4 显示了针对 Windows XP 专业版执行的完整 Retina 漏洞和端口扫描。如你所见，Retina 识别了开放共享、TCP 端口、假设的操作系统、媒体访问控制（MAC）以及一个省略的路由主机。除了这些之外，它还识别了箱内实现的多个其他服务和协议。

### 3.4 Retina 扫描

![](img/729efc56f204a2ebffb8295c3a2dfdfb_86_0.png)

## 探索免费漏洞扫描工具

每个人喜欢获得免费的东西，但你需要理解免费软件和开源软件的局限性。这些并不是由大型开发团队付费工作的包，而是由聪明的人在业余时间开发的包。支持通常很稀少，操作这些大多数工具并不像点击图标那么简单。尽管如此，免费和开源工具有其用用之地，且大多数都能如广告所言。对本节中的以下工具进行分析：

- Nessus (www.nessus.org)
- Fire & Water Security Toolkit (www.ntobjectives.com)
- LanGuard Network Security Scanner (www.gfi.com)
- whisker (www.wiretrip.net/rfp)
- LHF Tool Suite (www.SpecialOpsSecurity.com)
- NBTEnum (catch.com)
- Quick Kill (www.sensepost.com)
- SPIKE and SPIKE Proxy (www.immunitysec.com)
- CANVAS (www.immunitysec.com)

## Nessus

Nessus (www.nessus.org) 是一个开源扫描器，使用基于 Unix 的服务器并可以使用 Unix 或 Windows 客户端。Nessus 使用其发现和服务枚举功能，并在名为 Ness 攻击脚本语言（NASL）的自定义语言中执行漏洞检查。NASL 是一种类 C 脚本语言，允许用户快速创建检查项。

Nessus 是最流行的、可能是最免费的工具。Nessus 是类似于商业工具的漏洞扫描器。对于免费扫描工具来说，它与大多数商业产品一样好，在某些情况下甚至更好。通常，使用一个以上的工具有助于你获得最准确、最彻底的结果，无论你使用什么工具，你的扫描器都应该是 Nessus。

Nessus 包含客户端和服务器。Nessus 的服务器部分运行在 Unix 环境中；客户端部分适用于 Unix 和 Windows 环境。图 3.5 展示了 Nessus 的客户端部分。它包含以下功能：

- 智能服务识别：Nessus 将使用其检测系统寻找运行在非标准端口上的服务器。
- IDS 规避：用于 Web 服务器 IDS 规避的 libwhisker 也实现了一些经典的 IDS 攻击。
- 漏洞知识库：这允许检查项之间共享数据以进行更高效的扫描。
- 离线扫描：Nessus 可以配置为连续扫描，以保持最小的暴露窗口。

图 3.5 Nessus 原生界面

![](img/729efc56f204a2ebffb8295c3a2dfdfb_87_0.png)

## Fire & Water Toolkit

Fire & Water Toolkit (www.ntobjectives.com) 由 J.D. Glaser 等人创建。它用于发现、收集、映射并分析网络数据，特别是 Web 服务器漏洞。该工具包包含了攻击和防御应用程序。以下是攻击类应用程序：

- ntoscan：发现活动主机及其开放端口。
- nroute：收集每个主机的路由数据。
- ntoweb：搜索发现的 Web 服务器漏洞。
- nmap：创建拓扑图。这需要 nroute 的数据才能有效。
- ntrend：创建多次扫描的趋势报告。

该工具包的整合性通过其将数据从一个工具传递到另一个的能力得以展示。以下命令行示例使用 ntoscan 扫描（指纹识别、域名系统 [DNS] 解析）相关端口。识别出的服务器检查漏洞，然后将其组织成网络拓扑图。此示例的输出保存为名为 SpecialOps.xml 的文件。

```
C:>ntscan -N -b <enter IP range> | ntoweb | nroute | nmap -X SpecialOps.xml
```

## LanGuard Network Security Scanner (LNSS)

LanGuard Network Security Scanner (www.gfi.com) 通过结合扫描器和安全扫描器的功能，让网络管理员能够快速地进行网络安全审计。LNSS 的目的是突出重要信息，避免其他扫描器带来的信息过载。因此，LNSS 适用于内部网络安全。此外，LNSS 对非商业用途免费，所以价格很难比！

## whisker

whisker 扫描器由 RFP 创建，使用 Perl 编写的简单通用网关接口 (CGI) 漏洞扫描器。该扫描器分为两个独立部分：我们熟悉并喜爱的 whisker，以及供其调用的 Perl 模块 libwhisker。

传统的 CGI 扫描器没有内置智能功能。它们只是指向一个主机并向该主机日志文件中填充已知的 CGI 问题，无论是否存在 /cgi-bin/ 或运行的是哪种 Web 服务器。盲目扫描机器没有意义，因为你不仅浪费了大量的时间带宽，而且通常会错过许多问题。whisker 不是传统的 CGI 扫描器，它通过内置一些智能功能来解决这个问题，例如确定被扫描 Web 服务器的操作系统和版本，以及在扫描中修改或编写其他选项。它还提供了尝试使用一些经典 IDS 规避技术的能力。

