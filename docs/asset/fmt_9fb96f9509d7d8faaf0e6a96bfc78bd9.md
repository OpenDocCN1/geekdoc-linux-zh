
# 使用 Linux 安全工具发行版

## 第二部分 运行演示

本章描述了保护 Linux 系统的通用任务以及保护桌面和服务器系统的技术。随后，它描述了一些你可以尝试从可启动的 Linux 系统使用的工具，以对你的计算机和网络进行故障排除。

## Linux 安全检查清单

虽然大多数 Linux 系统都提供了保护计算机所需的所有工具，但如果你行事鲁莽，有人（很可能会）破坏你的系统、接管它或尝试窃取你的数据。请记住，没有任何安全措施是 100% 可靠的，而且在拥有计算机物理访问权限或有无限时间尝试破解的情况下，技术精湛且坚定的黑客可以进入任何计算机。

尽管如此，你仍然采取许多保护措施来增加保持 Linux 系统安全的几率。以下清单涵盖了一系列保护你的 Linux 桌面或服务器的安全功能。

### 物理访问

将计算机放在锁锁的门后是一个好主意，特别是当你的计算机包含关键数据时。我们可以通过在 BIOS 中（防止计算机启动）以及 GRUB 或 LILO 引导加载程序中启用密码，来限制具有物理访问权限的人对你计算机所的操作。你还可以在 BIOS 中限制哪些设备可以启动。

![](img/d7f79c91d15076e71790c1b4e1d02)

某些发行版（如 Ubuntu）简化了 root 账户的保护。

## Linux 安全性

**使用可信的软件**。虽然开源没有保证，但通过使用成熟的发行版，你有更好的机会避免受损的软件。使用 GPG 密钥可以帮助确保安装的软件来自良好的供应商。如果你下载 ISO 镜像，请使用 MD5 或 SHA1 检查其完整性。

**获取软件更新**。软件包中发现了漏洞和错误时，每个主流 Linux 发行版（包括 Debian）都提供了获取和安装更新的工具，特别是当你使用服务器时。这些工具包括 `apt`、`yum`。

**使用安全的应用程序**。在软件有效运行的情况下，某些应用程序可以提供更好的攻击防护。例如，如果你想通过互联网登录，Secure Shell (`ssh`) 被认为比 `telnet` 服务更安全。此外，认为在互联网上暴露是不安全的的服务（如 Samba 和 NFS）可以通过 VPN 隧道（如 IPSec 或 GRE）在互联网上更安全的使用。

**使用限制防火墙**。防火墙的主要工作是接受你允许的网络请求，并拒绝你不需要的请求（通过端口优先级）。桌面系统应该拒绝一组受控的端口。请参阅第 18 章了解如何使用 `iptables` 设置防火墙。

**仅开启所需的服务**。为了在 Linux 提供服务（如 Web、文件或邮件服务），守护进程将在特定端口上监听。开启你需要的的服务。如果不需要，甚至不要安装不需要的服务器软件。

> 在后台快速运行处理服务的程序（如守护进程）被称为守护进程。通常，守护进程在系统启动时自动启动，并一直运行到系统关闭。守护进程还可能根据需要由 xray 启动，xray 是一种特殊的守护进程，监听大量端口并处理请求的进程。

**限制服务的访问**。你可以通过仅允许从特定的主机、域名或网络接口访问，来限制你想开启的服务访问。例如，具有互联网和本地局域网接口的计算机可能允许局域网上的计算机访问 NFS 等服务，但不向互联网提供其他服务。服务可能在其配置文件中监听，或使用 TCP/IP 包装器（在本章稍后部分描述）。

**检查你的系统**。Linux 拥有大量工具用于检查系统的安全性。安装 Linux 后，你可以使用 `nmap` 检查端口访问情况，或使用 `Ethereal` 监控网络流量。你还可以添加流行的安全工具，如 `Nessus`，

206

# 图 6-2

SELinux 故障排除器识别了关注区域。

| 过滤器 | 日期 | | 计数 | 类别 | 摘要 |
|---|---|---|---|---|---|
| EDT 2007年10月15日 上午03:14:17 | | 1 | 文件标签 | SELinux 阻止我们使用 `/usr/sbin/semodule` |
| EDT 2007年10月14日 下午03:33:23 | | 1 | 文件标签 | SELinux 阻止 `timestamp_c` 使用 p |
| EDT 2007年10月14日 上午10:22:59 | | 577 | | | SELinux 阻止 kernel_getx (sbin_t) "error" 到 <unknown> |
| 2007年10月月44 下午10:52:58 | | 8 | | | SELinux 阻止 kernel_getx (sbin_t) "error" 到 <unknown> |
| EDT 2007年10月14日 上午05:05:50 | | 1 | | | SELinux 阻止 `/usr/sbin/kdm_getree` (sbin_t) |

SELinux 阻止 `timestamp_c` 使用被不修改的文件 (`/home/eduleary/seslinux-errors.log`)。

SELinux 拒绝了 `timestamp_c` 访问可能放置错误的文件 (`/home/eduleary/seslinux-errors`)。这意味着访问被拒绝，这在用户编辑其主目录下的文件或移动目录时很常见。问题在于文件最终具有错误的上下文，而您无权限访问它。

如果您想访问这些文件，将需要使用 `restorecon -v /home/eduleary/seslinux-errors` 来恢复它们。

| 附加信息 | |
|---|---|
| 来源: system_u:object_t:user_home_s | |
| 目标上下文: | |
| 目标对象: `/home/eduleary/seslinux-errors` [ file ] | |
| 相关软件包: | |
| 策略版本: | |
| SELinux 创建: selinux-policy-3.0.0-22.fc8 | |
| 策略类型: targeted | |
| 强制模式: Enforcing | |
| 插件名称: pcs_trap_labels | |
| 主机名: localhost | |
| 平台: localhost kernel 2.6.23-fc6 #1 SMP Thu Oct 14 Oct 2007 14:54:16 EDT 2007 i686 i86 | |
| 计数: 1 | |
| 首次出现: EDT 2007年10月14日 下午03:33:23 | |
| 最后出现: kfsd:1382-4fc6-7763-5c6ac26 | |
| 链接数: 5/5 | |
| 审计监听器: authenticated | |

## 查找特定于发行版的安全资源

大多数 Linux 发行版都有资源可以帮助您加固 Linux，并跟进该 Linux 版本特定的安全问题。以下是关注几个 Linux 发行版的在线资源：

- Red Enterprise Linux 和 Fedora 安全 — 检查红帽安全网站 (www.redhat.com/security) 以获取 RHEL 安全问题（通常也涉及 Fedora 系统）。从这里您可以查找并阅读最新的更新信息。对于 Fedora 安全问题，请检查 Fedora Wiki (http://fedoraproject.org/wiki/Security/Features)。

## 第二部分 运行演示

参阅《Red Hat Enterprise Linux 4 安全指南》以深入了解红帽系统的 Linux 安全性。您可以通过以下地址访问此指南：

www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/security-guide/

- Debian 安全 — Debian 安全信息页 (www.debian.org/security/) 提供了一个查找安全告告、常见 Debian 安全问题解答以及安全文档链接的中心点。您可以在此处找到 Debian 安全在线手册：

www.debian.org/doc/manuals/securing-debian-how

- Ubuntu 安全 — 在 Ubuntu 安全页 (https://help.ubuntu.com/community/Security) 上查找 Ubuntu 的安全指南和工具。

- Gentoo 安全 — Gentoo 安全页 (www.gentoo.org/security/) 包含了与加固 Gentoo 系统相关的工具、公告以及安全策略和项目文档的链接。Gentoo 安全手册在此：

www.gentoo.org/doc/en/security

- Slackware 安全 — 要跟进 Slackware 安全问题，请参考 Slackware 安全告告 (www.slack.com/security)。您也可以加入 Slackware 的安全邮件列表 (www.slackware.com/lists)。

- SUSE 安全 — SUSE 的在线支持由 SUSE 的母公司提供。Novell 从该网站链接到各种 SUSE 安全主题：

www.novell.com/linux/security/securitysupport.html

对于 openSUSE，请访问此站点：

www.novell.com/products/opensuse/security.html
