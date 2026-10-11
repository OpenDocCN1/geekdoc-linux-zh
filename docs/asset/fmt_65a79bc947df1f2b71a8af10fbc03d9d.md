
管理员必须经常使用安全分析软件测试他们的系统。安全分析软件扫描系统以发现漏洞，并建议修复以关闭安全漏洞。本节讨论了确保您的系统免受互联网每日威胁的维护工作。

## 红帽错误修正：修复与公告

一旦您的 Red Hat 系统上线，就必须确保获取最新的红帽错误修正。这些错误修正包括错误修复、修正和更新。您应该始终检查 Red Hat 站点 `www.redhat.com/apps/support` 获取最新的错误修正。以下列表定义了在产品发布后发现的不同类型的错误修正：

- **错误修复**：这些红帽包工具（RPM）可以免费下载。错误修复为特定问题提供了修复，例如在完成操作系统任务时可能会出现某些错误消息。另一个有用的资源是红帽 bug 跟踪系统 `https://bugzilla.redhat.com/`。图 2-2 显示了用户的一个 bug 通知。

- **安全公告**：红帽建议所有管理员下载并安装安全升级，以避免由于输入验证不当导致 Netscape 联合专家小组（JPEG）代码引起的内存溢出、拒绝服务（DoS）和入侵攻击。安全更新位于 `http://www.redhat.com/security/updates/`。

- **包增强**：操作系统或特定应用程序的功能和特性提供了更新。包增强通常对系统的完整性至关重要；它们经常为 RPM 提供新功能。

### 图 2.2 通过 Bugzilla 的通知

Bugzilla 234616: RHEL 5 无法从显示器获取 EDI 并设置了低分辨率

| 最后评论 | 克隆 bug | 显示 bug 活动 | 打印格式 |
|---|---|---|---|

| | | 优先级 | 高 |
| 产品 | Red Hat Enterprise Linux | 严重 | 高 |
| 版本 | 5 | 状态 | 已分配 (ASSIGNED) |
| 组件 | xorg-x11-vesa | 解决 | |
| | | 抄送： | |
| 硬件 | i386 | cra@epi.edu | |
| 报告者 | (wdc@mit.edu) | dddongo@redhat.com | |
| 分配给 | ajax (alexson@redhat.com) | gneely@ncsu.edu | |

由 (wdc@mit.edu) 于 2007-04-13 14:41 EST 打开 [回复]

我安装了 RHEL 5，注意到有时 X 分辨率会正确地设置为我指定的 1200x1024，但通常在重启 X 服务器后，它会把分辨率降低到 800x600。

我将附上 `Xorg.0.log` 输出，显示 VESA BDE 读取被认为成功。

您还可以通过**bug 报告工具** 发送 bug。当您在系统上进行常规工作遇到错误时，该窗口会自动出现。图 2.3 显示了 bug 报告工具。

如果您点击“详细信息”，可能会发现所示信息（此处显示了部分输出）。这些信息基于 bug 的性质、软件和硬件配置，并因系统而异。虽然您可能无法识别报告工具捕获的所有内容，但红帽支持专家将能够解码这些信息并进行修复。

### 图 2.3 bug 报告工具

![](img/b38c01d2fda8509e8449e32f876ae148_36_0.png)

发行版: Red Hat Enterprise Linux server release 5 (Tikanga)

Gnome 版本: 2.16.0 2006-09-04 (Red Hat, Inc)

BugBuddy 版本: 2.16.0

内存状态: size: 147779584 size: 0 驻留: 147779584 共享: 0 rss: 64827776

rss_rim: 0

CPU 使用率: start_time: 1189756814 rtime: 0 utime: 2224 stime: 0 cutime: 0 cstime: 197_real_value: 0 frequency: 93

回溯轨迹生成自 `/usr/bin/yelp`

```
(no symbols found)
Using host thread library "/lib/thread_db.so."
(no symbols found)
[Thread debugging using thread_db.so]
(no symbols found)
[Thread debugging using thread_db.so]
[New Thread -120863 (LWP 3961)]
[New Thread -125504 (LWP 4181)]
[New Thread -1243567 (LWP 3963)]
[New Thread -1210463 (LWP 3962)]
(no symbols found)
(no symbols found)
```

一旦您在红帽网络注册了系统，您偶尔会收到“RHN 错误警报”邮件。这些警报针对您注册的系统包含了包含了摘要、详细描述以及解决问题的建议。

在此案例中，从红帽收到的以下邮件包含了系统所需的“内核安全更新”详情（部分输出）：

关于此错误修正的完整信息可以在此处找到：`https://rhn.redhat.com/rhn/errata/details/Details.do?eid=5984`

安全公告 - RHSA-2007:075-2

摘要：

重要：内核安全更新

修复 Red Hat Enterprise Linux 5 内核各种安全问题的更新后内核包现已提供。

红帽安全响应小组已将此更新评级为具有重要的安全影响。

描述：

Linux 内核处理操作系统的基本功能。

这些新的内核包包含对以下安全漏洞的修复：

- * Intel 显卡 DRM 驱动程序中存在一个漏洞，允许本地用户访问任何内存。要访问 DRM 功能，用户必须拥有 X 服务器的权限，该权限通过图形化登录授予。此问题仅影响带有 Intel 965 或更高版本图形芯片组的系统。（CVE-2007-3851，重要）

- * 64 位系统上的 VFAT 内核 ioctl 处理存在一个漏洞，允许本地用户损坏 `kernel_dirent` 结构并导致拒绝服务（系统崩溃）。（CVE-2007-2878，重要）

. . （输出已截断）

建议红帽企业 Linux 5 用户升级到这些软件包，这些软件包包含了用于修复这些问题的回向补丁（backported patches）。

参考文献：

`http://www.redhat.com/security/updates/classification/#important`

---

您可以通过两种方式解决此公告中概述的问题：

- * 通过点击以下位置列表中的名称选择您的服务器，然后为其安排错误更新（errata update）：`https://rhn.redhat.com/rhn/systems/SystemList.do`

- * 在每个受影响的服务器上运行更新代理（Update Agent）。

. . （输出已截断）

---

### 受影响系统列表

此错误公告可能适用于下方列出的系统。如果您知道此错误修复不适用于列出的系统，可能是该服务器的软件包配置（package profile）已过期。在这种情况下，您应该在相关系统上以 root 身份运行 `update -p` 以刷新您的软件配置。

“您的 RHN”中注册了 1 个受影响的系统（仅显示您显式启用错误告警的系统）。

| 版本 | 架构 | 配置文件名称 |
|---|---|---|
| 5Server | i686 | linux11 |

红帽网络团队

如您从上述邮件中注意到的，注册的系统需要内核安全更新。现在，您需要遵循“采取行动”部分列出的步骤来确保您的系统已更新。本案例公告建议对受影响的服务器安排错误更新并运行更新代理。

作为 Linux 管理员或安全管理员，定义以下内容至关重要：

- 服务器的角色（web、数据库、代理、ftp、dns、dhcp 或其他）

- 执行特定服务器角色所需的服务（例如，Apache 和锁定 Web 服务器）

- 需要开放的端口（例如，HTTP，80端口）

所有其他服务都应禁用，所有其他端口都应关闭。完成上述任务后，服务器将成为仅运行指定角色的专用服务器。

要加固服务器，必须禁用禁用不必要的服务和端口。此过程涉及移除任何不必要的服务（如 Linux 登录），并锁定不必要的传输控制协议/用户数据报协议（TCP/UDP）端口。一旦这些服务和端口安全，您必须定期维护系统。图 2-4 显示了红帽 Linux 中的服务配置。

系统 | 管理 打开服务配置工具。您可以选择或取消选择服务，启动、停止或重启，并编辑单个服务的运行级别（run level）。在图 2.4 中，您可能会注意到服务“iptables”已启用，并显示了服务的描述和状态。

### 图 2.4 服务配置

![](img/b38c01d2fda8509e8449e32f876ae148_40_0.png)

现代 Linux 发行版已经增强了 GUI 以涵盖大多数管理任务，但对于优秀的管理员来说，在没有 GUI 的情况下如何执行任务至关重要。让我们讨论如何手动禁用某些脆弱的服务器。
