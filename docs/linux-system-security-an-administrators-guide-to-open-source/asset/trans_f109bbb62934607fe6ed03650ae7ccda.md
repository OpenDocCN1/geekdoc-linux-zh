
## 用户隐私与管理员道德准则

保护计算资源的另一个方面涉及访问该环境之用户的隐私，以及控制该环境者所秉持的道德或伦理标准。本章中讨论的大部分内容都围绕监控用户活动展开。事实上，这一主题贯穿了整本书。合理的监控活动与侵犯用户隐私之间存在一条界线。例如，监控电子邮件或捕获击键通常被视为极端措施。只有在绝对必要且获得管理层和法律顾问完全同意的情况下，才应开展此类活动。即使贵组织的政策规定公司的计算资源不得用于私人用途，在多种情形下，这些资源仍可能被用于私人通信。例如，经理经常在电脑上撰写和存储员工绩效评估。这些评估可能会通过电子邮件在员工和经理之间交换。过度监控可能导致诉讼，最终使公司付出的代价远超其试图保护的资产价值。

安全策略必须解决这些问题，甚至可能包括为系统和网络管理员制定行为准则。在您着手保护计算资源的过程中，请务必考虑您在此方面的行动对使用该资源者的权利和隐私所产生的影响。

## 摘要

在本章中，我们概述了制定安全策略的准备过程，并强调了其重要性。我们提供了一个实施该策略的框架，并以指出道德安全管理的极其重要的议题作为结尾。

## 延伸阅读

### 书籍

以下两本参考书均描述了风险评估和安全策略的创建。

1.  Neumann, Peter G., *Computer Related Risks*, Reading, Massachusetts, Addison-Wesley Publishing Company, 1995.
2.  White, Gregory B., Eric A. Fisch, and Udo W. Pooh, *Computer System and Network Security*, Boca Raton, Florida, CRC Press, 1996.

### 网络资源

您可以在 [http://www.sans.org/newlook/resources/policies/policies.html](http://www.sans.org/newlook/resources/policies/policies.html) 找到一个优秀的**安全策略模板及相关信息**集合——这是制定安全策略的一个绝佳起点。

获取相关信息，请也访问 [http://ciac.llnl.gov/cgi-bin/index/documents/](http://ciac.llnl.gov/cgi-bin/index/documents/) 和 [http://www.cert.org/nav/](http://www.cert.org/nav/)。

### 其他资源

一份非常详尽的参考资料，也是任何关注计算资源安全者必读的内容。

1.  Fraser, B., RFC2196: Site Security Handbook, September 1997. Available at [http://www.faqs.org/rfcs/rfc2196.html](http://www.faqs.org/rfcs/rfc2196.html)。

## 小贴士

## 背景信息

在我们踏上传阅公共可用工具的旅程之前，有几个概念和工具我们必须首先讨论，因为我们将在这本书中不断提及它们。本章将涵盖以下主题，每个主题都有自己独立的章节。

-   基本输入/输出系统（BIOS）密码
-   Linux 安装和 Linux 加载程序（LILO）
-   启动脚本
-   Red Hat 包管理器（RPM）
-   TCP/IP 网络概述
-   征求意见（RFC）
-   密码学
-   测试和生产环境
-   公共许可证

这些主题将以不同程度的细节进行介绍，但均非定论。因此，我们在每个章节内部或末尾提供了额外的阅读材料指引。

## BIOS 密码

许多现代 PC 支持在 BIOS 中设置密码。如果您的系统提供了此功能，我们建议您利用此功能，除非您的系统在物理上是安全的。请查阅您的系统文档以获取更多关于 BIOS 密码的详细信息。

## Linux 安装和 LILO

随着类似向导、由 X 窗口系统驱动的 Linux 安装的问世，只需指点鼠标即可轻松运行 Linux 系统。然而，便利性往往会成为安全的障碍。在安装 Linux 系统之前，请确定您需要哪些包和服务。特别是，不要运行您不需要的服务。例如，假设您通过邮局协议（POP）或互联网消息访问协议（IMAP）¹ 服务器（例如通过独立服务提供商 [ISP]）访问您的电子邮件，那么您不希望运行 sendmail。默认情况下，sendmail 将在每次启动时安装并启动，如果您不使用它，这是不希望的。安装后，您可以手动禁用服务，如第 24 页“*启动脚本*”一节中所述，或者通过 Red Hat 控制面板中的运行级别编辑器进行设置。

### 关于 LILO 的说明

Linux 加载程序是一个灵活的启动加载程序，适用于 Linux 和其他操作系统（如 DOS、Windows 95/98/NT 以及各种类型的 UNIX）。它不依赖于特定的文件系统，并且可以管理从各种设备（软盘、硬盘、CD-ROM 等）启动。简而言之，LILO 的任务是启动所选的操作系统。如果选择 Linux，它将启动 Linux 内核（/boot/vmlinuz 或类似文件）。还有其他启动加载程序，但 LILO 已成为 Intel 平台上最常见的一个。默认情况下，当您安装 Red Hat 时，LILO 将在您的系统上进行配置。

LILO 在启动时读取 /etc/lilo.conf 配置文件。默认情况下，此文件可读。您应将此文件的权限设置为仅限 root 读写。此外，请考虑为此文件设置不可变位（有关 *chattr* 和不可变位的讨论，见第 4 章第 75 页的 *文件属性*）。示例 3-1 展示了这两个步骤。

**示例 3-1** 在 /etc/lilo.conf 上设置安全的权限和属性

```bash
# chmod 600 /etc/lilo.conf
# chattr +i /etc/lilo.conf
```

您可以对此文件进行各种操作，其中许多在“*安装和 LILO 资源*”中提供的资源中有所讨论

¹ POP、IMAP 和 sendmail 为客户端（如 /bin/mail）提供邮件服务。
