
[INFO] May/13/2023 10:29:31 - Dist: ubuntu 20.04 Fossa Focal

[INFO] May/13/2023 10:29:31 - MobSF Base Environment Check

```

图 2.37：运行 MobSF

## 5. 访问 MobSF Web 界面

打开网页浏览器并导航到 `http://localhost:8000`，如图 2.38 所示访问 MobSF Web 界面。该界面允许你与 MobSF 交互并进行安全测试和分析：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_76_0.png)

图 2.38：访问 MobSF Web 界面

若要使用 Docker 快速安装 MobSF，只需从 `"opensecurity/mobile-security-framework-mobsf"` 获取 Docker 镜像即可！这种无忧的方法能够实现快速简单的 MobSF 设置。Docker 的显著优势在于它能够绕过 Python 以及其他决条件的复杂性。

## Trivy

Trivy 是一个简单而强大的容器漏洞扫描器，专为 CI/CD 流水线定制。在 Kali Linux 上安装它非常简单，且你可以通过命令行界面访问它。

以下是设置方法：

1.  首次，使用命令 `wget https://github.com/aquasecurity/trivy/releases/download/v0.18.3/trivy_v0.18.3_linux-64bit.deb` 下载 Trivy 安装脚本，如图 2.39 所示。

![](img/e4f93a89908ca3f498ee2517ddfbfd77_77_0.png)

> 图 2.39：下载 Trivy 安装脚本

2.  使用命令 `sudo dpkg -i trivy_0.18.3_Linux-64bit.deb` 安装 Trivy，如图 2.40 所示：

```bash
(ummeedel@kali) ~/Desktop

$ sudo dpkg -i trivy_0.18.3_linux-64bit.deb

(Reading database ... 401177 files and directories installed.)

Preparing to unpack trivy_0.18.3_linux-64bit.deb ...

Unpacking trivy (0.18.3) over (0.5/3) ...

Setting up trivy (0.18.3) ...
```

> 图 2.40：安装 Trivy

3.  安装完成后，你可以使用命令 `trivy image_name` 扫描容器漏洞，如图 2.41 所示。

为了进一步的个性化配置，你还可以选择为扫描定义额外的策略。这可能包括设置报告的漏洞的严重程度级别，或指定用于扫描的包名。如需深入了解并探索完整的选项，你可以查看 `https://github.com/aquasecurity/trivy` 的 Trivy 文档。

> 注意：随着容器在云环境中部署和运行应用程序的使用日益增加，容器安全已成为网络安全的关键要素。

## 设置漏洞机器和应用程序

现在，让我们通过检查涉及的步骤，探索配置不同漏洞机器和应用程序的过程：

## 设置 Metasploitable 2

Metasploitable 是一个默认的虚拟机，旨在探索和演示 Metasploit 框架的特性。它是磨练黑客能力、测试安全方法以及深入研究 Metasploit 框架运行机制的宝贵工具。

要在 VMware 上设置 Metasploitable 2，你需要执行以下步骤：

*   通过访问 Rapid7 网站 `https://information.rapid7.com/download-metasploitable-2017.html` 获取 Metasploitable 2 虚拟机镜像，如图 2.42 所示：

## 下载 Metasploitable，用于评估 Metasploit 的故意留存目标机器

开始你的 Metasploit 之旅：如果你想对你的网络进行渗透测试，Metasploitable 是一个基于 Linux 的机器。评估 Metasploit 需要一个包含多个漏洞的 Linux 机器。为了在 VMware 上设置 Metasploitable 2，你需要执行以下步骤：

*   访问 Rapid7 网站 `https://information.rapid7.com/download-metasploitable-2017.html` 获取 Metasploitable 2 虚拟机镜像，如图 2.42 所示：

图 2.42：什么是 Metasploitable？它是如何工作的？

开始你的 Metasploit 之旅：如果你想对你的网络进行渗透测试，Metasploitable 是一个包含多个漏洞的 Linux 机器。为了在 VMware 上设置 Metasploitable 2，你需要执行以下步骤：

*   访问 Rapid7 网站 `https://information.rapid7.com/download-metasploitable-2017.html` 获取 Metasploitable 2 虚拟机镜像，如图 2.42 所示：

3.  将 Metasploitable 2 虚拟机镜像导入 VMware 或 VirtualBox，如图所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_79.png)

图 2.43：导入 Metasploitable 2 虚拟机

安装完成后，使用默认凭据：`metasploitable`。

## 设置 bAPP

bWAPP，又称为 Buggy Web Application（漏洞应用程序），是一个用于训练的故意不安全应用程序。它可以帮助理解 注入、跨站脚本等攻击。它是开源的，免费下载。

要在 Windows VM 上设置 bWAPP，你需要遵循以下步骤：

1.  在你的 Windows VM 上下载并安装最新版本的 XAMPP。这将为 bWAPP 提供本地服务器环境。
2.  从官网下载最新版本的 bWAPP 并将其提取到 XAMPP 安装目录下的 `htdocs` 文件夹中。
3.  通过控制面板并点击启动按钮启用 XAMPP 中的 Apache 和 MySQL 模块，如图 2.46 所示。
4.  打开网页浏览器并访问以下 URL：`http://localhost/bwapp/install.php`。这将启动 bWAPP 安装向导，如图 2.47 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_82_0.png)

图 2.47：bWAPP 安装向导

5.  安装完成后，你可以通过在网页浏览器中访问 `http://localhost/bwapp` 来访问 bWAPP，如图 2.48 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_82_1.png)

图 2.48：安装完成后

使用默认凭据：用户名 `bee`，密码 `bee`。

注意：BWAPP 使用 PHP 开发并配有 MySQL 数据库，可以配置在如 XAMPP 的本地服务器或远程 Web 服务器上。

## 结论

VAPT 测试实验室环境搭建模块已成功完成。本章侧重于建立攻击实验室和构建真实测试环境的实操方面。掌握了这些知识，你现在已经了创建自己的本地实验室并理解特定设置前提条件的能力。本章不仅传授了实验室搭建的逐步演进方法，还引入了关键的 VAPT 概念和工具，包括 Kali Linux，它有助于在目标上运行演练和漏洞利用程序。

在接下来的章节中，我们将深入探讨侦察策略在有效渗透测试中的重要性。通过侦察获取有关目标的充分信息对于构建测试所需的要素起着至关重要的作用。侦察是漏洞评估与渗透测试（VAPT）的第一步，为整个过程奠定了基础并确保其成功执行。

## 加入我们书籍的 Discord 空间

加入书籍的 Discord 工作空间获取最新更新、优惠、全球技术动态、新发布以及与作者的互动：

`https://discord.bpbonline.com`

![](img/e4f93a89908ca3f498ee2517ddfbfd77_83_0.png)

# 第 3 章
## 主动与被动侦察策略

## 引言

在本章中，我们将深入研究侦察策略的细节，这些策略对于渗透测试的成功起着重要作用。通过侦察获取足够的目标信息是确定测试所需内容的。计算机系统的不同部分可能需要不同的方法来收集正确的数据。作为渗透测试人员，根据目标公司的工作方式来定制你的方法也很重要。

互联网就像一个所有人都可以访问的信息宝库。其中一种技巧被称为开源情报（OSINT），它可以帮助渗透测试人员从公共来源收集关键数据，如电子邮件地址、域名、IP 地址、员工姓名、主机名和 DNS 记录。

> 注意：侦察是漏洞评估与渗透测试（VAPT）练习的第一步，因为它为后续过程奠定了基础并有助于其成功。

## 结构

在本章中，我们将讨论以下主题：

*   什么是侦察
*   为什么情报收集如此重要
*   侦察的类型
*   被动侦察的工具和策略
    *   `WHOIS`
    *   `DNS` 侦察
    *   `IP` 侦察
    *   路径映射
    *   电子邮件地址
    *   姓名和号码
    *   密码或泄露数据导出
*   主动侦察的工具和策略
    *   主机发现
    *   端口扫描
    *   运行的服务和版本检测
    *   操作系统指纹识别
    *   目录枚举
    *   硬编码信息
*   侦察的额外资源
    *   `Maltego`
    *   `SPARTA`

# 什么是侦察

为漏洞评估与渗透测试（VAPT）准备收集目标信息的过程被称为侦察。可以通过主动和被动的方法进行，包括网络扫描、社会工程、网络爬虫、足迹探测和指纹识别。侦察的目的是尽可能获取有关目标的信息，包括其系统、服务器、网络、应用程序和人员，以便识别潜在漏洞并策划更复杂的攻击。

有很多工具、技术和网站可用于收集情报。本章将简要介绍这些资源以及如何使用它们收集必要信息。常用的推荐的侦察策略如图 3.1 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_86_0.png)

图 3.1：侦察策略

## 为什么侦察如此重要

侦察对于在攻击前理解目标至关重要。基于侦察的良好规划策略可以显著帮助渗透测试人员，通过减少误报、减少所需的攻击次数、缩短所需时间并提高扫描质量。通过收集有关目标的大量信息，你可以更高效地策划攻击，并可能缩短攻破目标所需。

## 侦察的类型

VAPT 练习通常包括四个阶段，如图 3.2 所示，侦侦察察。可以通过以下方式进行：

| 阶段 | 描述 |
| :--- | :--- |
| 被动侦察 | 在不直接参与或交互的情况下获取目标信息 |
| 主动侦察 | 通过直接参与和交互获取有关目标的知识 |
| 策略构建 | 设计良好的策略可以增加 VAPT 练习的成功机会 |
| 漏洞利用 | 在有充分策略的情况下，可以更高效地执行漏洞利用阶段 |

图 3.2：VAPT 练习阶段

## 被动侦察

被动侦察意味着在不直接接触目标的情况下收集其信息。这种方法比主动方法更难被发现且速度更快，但数据可能不是是最新的或可靠的。例如，在不直接联系目标组的情况下获取电子邮件地址列表就是被动侦察。

## 主动侦察

主动侦察意味着你通过直接参与来获取目标信息。这种方法比被动方法风险更大且更耗时，因为你正在与目标直接交互，可能会被注意到。它是被动侦察的扩展版本，通常提供更精确、当前的信息。例如，如果你想要服务器的服务列表及其版本，你需要询问服务器。这就是主动侦察的一个示例。

> 注意：侦察信息可以转换为可操作的情报以创建良好的利用计划。该计划包括利用选择的方法攻击系统，这将增加成功的机会并缩短操作时间。

## 被动侦察工具和策略

有很多被动侦察的策略。让我们在实践中讨论一些：

## WHOIS

侦察的第一步是收集有关目标 IP 地址和域名所有者的信息。`WHOIS` 命令用于从域名注册商数据库获取这些信息。它可以显示谁拥有域名以及托管在哪个 IP 地址上。

根据查询的数据库，渗透测试人员可以收集多种数据：

*   **注册商（Registrar）：** 发布和管理域名预留的组织
*   **注册人（Registrant）：** 拥有域名的组织或个人
*   **管理员和技术人员（Admin and Tech）：** 开发和维护网站的组织或个人
*   **DNS 服务器（Namesvers）：** 域名到 IP 地址的解析
*   **创建和过期日期：** 域名注册和过期日期
*   **状态（Status）：** 域名的当前状态（例如，活动、过期等）

参考图 3.3 到图 3.5 中的截图查看‘ummedcyber.’域名的详情：

运行命令：`whois ummedcyber.com`

注册者名称：Ummed Meel
注册组织：
注册者街道：Sikar
注册者城市：Sikar
注册州/省：Rajasthan
注册者邮编：332031
注册国家：IN
注册者电话：+91.00
注册者电话分机：
注册者传真：
注册者邮箱：um@gmail.com
注册者管理员 ID：无法从注册局获取
管理员名称：Ummed Meel
管理员组织：
管理员街道：Sikar
管理员城市：Sikar
管理员州/省：Rajasthan
管理员邮编：332031
管理员国家：IN
管理员电话：+91.00
管理员电话分机：
管理员传真：
管理员邮箱：um@gmail.com

图 3.4：域名注册者和管理员详情

剩余信息显示在下面的图 3.5 中，顺序与之前相同。

技术人员：Ummed Meel
技术组织：
技术街道：Sikar
技术城市：Sikar
技术州/省：Rajasthan
技术邮编：332031
技术国家：IN
技术电话：+91.00 59
技术电话分机：
技术传真：
技术邮箱：um@gmail.com
名称服务器：NS15.DOMAINCONTROL.COM
名称服务器：NS16.DOMAINCONTROL.COM

> DNSSEC:
ICANN WHOIS 数据报告系统 URL：`http://wdprs.internic.net/`
>>> WHOIS 数据库最后更新时间：2023-02-01T16:58:22Z <<
如需更多关于 WHOIS 状态码的信息，请访问 `https://icann.org/erp`

根据上述侦察，得出以下统计结果：目标组织的攻击面将会增加。

*   如果识别出的域名与注册者相关联，这些细节对于构建社会工程攻击可能很有用。例如，如果注册者是个人，可以使用这些信息来针对其量身定制攻击。
*   获取注册者的联系方式（如其电子邮件地址和电话号码）对于钓鱼攻击等社会工程攻击很有用。渗透测试人员可以使用这些信息联系目标并尝试操纵他们。
    如果 如果我们能够识别出网络开发公司，也可以在他们的其他域名中搜索类似的漏洞。
*   名称服务器可用于获取托管 IP 和其他细节，这对于执行基于 IP 的利用很有用。
*   域名年龄是指域名的年龄，可以通过检查域名的旧存档来探索应用程序的旧或未使用的特性和功能。

> 注意：有时，如果用户向注册商支付额外费用以保持所有权详情隐私，WHOIS 详情可能会被代理信息掩盖。

## DNS 侦察

**域名系统 (DNS)** 侦是收集与网站相关的各种记录的过程，这有助于配置并使其在互联网上可访问。该技术的关键方面之一是 DNS 解析，它允许识别与网站关联的 IP 地址。

此外，通过利用 DNS 侦察，渗透测试人员可以收集价值情报，例如：

*   **NS（名称服务器）记录**：这些指示了负责管理和存储特定域名 DNS 记录的服务器位置。
*   **A（地址）记录**：这些记录指定与给定域名关联的 IP 地址。
*   **AAAA 记录**：这些记录与“A”记录非常相似，但用于将域名映射到 IPv6 地址。
*   **MX（邮件交换）记录**：这些记录指示了与域名关联的电子邮件服务器的详情。
*   **CNAME（别名）记录**：如果单个服务器上运行着多个服务，这些记录有助于确定其他域名的名称。
*   **TXT 记录**：这些记录包含与域名关联的其他资源的详细信息，例如服务器和网络信息。
*   **PTR（指针）记录**：这些记录是“A”记录的反向，它们提供了与 IP 地址对应的域名。

有多种工具可用于 DNS 侦察，如 `nslookup`、`dig`、`dnsenum`、`dnsrecon`、`dnsmap`、`DNSRecon`、`theHarvester` 和 `Sublist3r`。为了说明 DNS 侦察的概念，我们将使用 `dnsenum` 示例，这是一个多线程 Perl 脚本，可以在命令行模式下以枚举 DNS 信息。查看图 3.6 和图 3.7 中的截图以深入查看 ummedcyber.com 域名的 DNS 侦察。

运行命令：`dnsenum ummedcyber.com`

```
ummedneel@kali:~

$ dnsenum ummedcyber.com

dnsenum VERSION:1.2.6

ummedcyber.com

主机地址：

ummedcyber.com.           5    IN    A       166.62.10.50

邮件服务器：

s15.domaincontrol.com      5    IN    A       97.74.107.8

ns16.domaincontrol.com      5    IN    A       173.201.75.58
```

图 3.6：DNS 侦察

剩余信息显示在下面的图 3.7 中，顺序与之前相同：

使用 `/usr/share/dnsenum/dns.txt` 进行暴力破解：

```
admin.ummedcyber.com.     5    IN    A       166.62.10.50

mail.ummedcyber.com.      5    IN    A       166.62.10.50

www.ummedcyber.com.       5    IN    CNAME  166.62.10.50
```
