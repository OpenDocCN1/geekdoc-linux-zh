
# 第三部分 学习系统管理技能

本章描述了保护 Linux 系统的通用任务，适用于桌面和服务器系统。然后描述了你可以尝试的一些 Linux 工具。

## Linux 安全清单

虽然大多数 Linux 发行版提供了安全工具，但如果你操作粗鲁，他人可能会损坏你的计算机。话虽如此，许多安全措施可以改进你的系统。以下清单涵盖：

- **物理访问**。将计算机锁在门后是一个主意，尤其是当你拥有数据时。当你离开时可以通过锁定系统来限制人的行为。
- **添加密码**。通过允许从特定的主机、域名或网络接口访问来限制你想要的服务。
- **使用密码保护**。虽然大多数 Linux 发行版提供了安全工具，但如果你操作粗鲁，他人可能会损坏你的计算机。服务可能会限制访问。
- **限制权限**。防火墙的主要工作是接受你允许的网络请求并拒绝其他请求（主要基于端口号）。
- **仅启用你需要的的服务**。为了在 Linux 中提供服务（如 Web、文件或邮件服务），守护进程将监听特定的端口号。不要启用不需要的服务。

> 注意：在后台静默运行处理服务请求的程序（如守护）被称为守护进程。通常，守护进程在系统启动时自动启动，并一直运行到系统关闭。守护进程也可以根据需要由 `systemd` 启动，`systemd` 是一个监听大量端口并启动请求进程的特殊守护进程。

## Linux 安全

- **使用信任软件**。虽然没有保证，但使用 `GPG` 公钥可以帮助确保软件来自供应商。当然，始终使用 `MD5` 或 `SHA` 校验和来检查其完整性。
- **获取软件更新**。随着软件漏洞被发现，每个主要的发行版都提供了获取和安装这些更新的工具，特别是在 Linux 中。
- **使用安全的应用程序**。即使有效且正常工作，某些应用程序也能提供更好的攻击防护。例如，如果你想通过互联网连接，Secure Shell (`SSH`) 服务被认为比登录或 `telnet` 更安全。
- **限制服务的访问**。通过允许从特定的主机、域名或网络接口访问来限制你想要的服务。
- **检查你的系统**。Linux 提供了可用工具来检查系统的安全性。在安装 Linux 后，你可以使用 `nmap` 检查端口访问情况，或通过 `Ethereal` 查看流量。

对你的系统安全有一个更全面的视角。本书附带的 CD 和 DVD 中包含的安全工具在本章中进行了介绍。

- **监控你的系统。** 你可以记录 Linux 系统上几乎每种类型的活动。使用 `syslog` 和 `klogd` 设施的系统日志文件可以被配置为根据你的喜好跟踪尽可能多或尽可能少的活动。诸如 `logwatch` 之类的实用程序提供了简便的方法来处理转发到你管理员电子邮件账户的潜在问题信息。Linux 日志功能将在本章稍后部分介绍。

> 注意：记住，监控你的系统并不意味着你只需开启日志；你还必须仔细监控这些日志，并对它们提供的信息做出反应。

- **使用 SELinux。** `SELinux` 是一个极其丰富（且复杂）用于管理 Linux 系统几乎每个方面访问机制。它解决了 Linux 和 UNIX 系统在高度安全环境中“如果我获得了 root 权限，你的机器就完了了”的缺陷。Red Hat 系统提供了一组实用的有限 `SELinux` 策略，这些策略在 Fedora 中默认开启。其他 Linux 发行版也在开发并包含 `SELinux` 实现。图 12-1 显示了 Fedora 自带的 `SELinux` 管理工具（选择 System ↩ Administration ↩ SELinux Management），而图 12-2 显示了 `SELinux` 故障排除器（选择 Applications ↩ System Tools ↩ SELinux Troubleshooter）。

图 12-1 Fedora 包含 SELinux 工具程序。

| 文件 | 帮助 | SELinux 管理(员) |
|---|---|---|
| 选择: | 系统默认强制模式 | 强制 (Enforcing) |
| 布尔值 (Boolean) | 当前强制模式 | 强制 (Enforcing) |
| 用于打标签 | 系统默认策略类型 | 目标型 (targeted) |
| 用户映射 | | |
| SELinux 用户 | 下次重启时重新打标签 | |
| 翻译 | | |
| 网络端口 | | |
| 策略模块 | | |

## 加固 Linux

### 图 12-2

`SELinux` 故障排除器将识别关注的区域。

| 日期 时间 | 用户 | 组 | 帮助 | 计数 | 类别 | 摘要 |
|---|---|---|---|---|---|---|
| 2018年8月20日 周二 01:57:39 PM CDT | root | | | 2 | 文件标签 | SELinux 正在阻止使用可能标签错误的文件 (t/... |
| 2018年8月18日 周六 03:12:38 PM CDT | root | | | 0 | 文件标签 | SELinux 正在阻止使用可能标签错误的文件 (t/... |
| 2018年8月16日 周四 10:22:05 PM CDT | root | | | 1 | 文件标签 | SELinux 正在阻止使用可能标签错误的文件 (t/... |
| 2018年8月10日 周一 10:18:38 AM CDT | root | | | 1 | 文件标签 | SELinux 正在阻止使用可能标签错误的文件 (t/... |
| 2018年8月10日 周一 10:18:33 AM CDT | root | | | 2 | 文件标签 | SELinux 正在阻止使用可能标签错误的文件 (t/... |

摘要

`SELinux` 正在阻止访问标签为 `file_t` 的文件

`SELinux` 处于许可模式 (`permissive mode`)；该操作已被拒绝，但由于许可模式而被允许

`SELinux` 对标签 `file_t` 的权限检查：由于该上下文没有访问该文件的权限，因为它被标记为 `file_t`；如果你向系统添加了新磁盘，可以使用 `restorecon` 命令对其进行重新打标签。你还应该对整个系统重新打标签。

映射错误

你可以以管理员身份执行以下命令来重新为你的计算机打标签：`autorelabel -reboot`

字体 上下文:

目标上下文: `unconfined_u:unconfined_r:user_t:s0:c1023`

目标属性: `system_u:file_t:s0`

目标权限: `denied(file)`

源: `pam_tssd_ldap_checkpoint`

源路径: `<Unknown>`

主机: `elstein`

源 RPM 软件包: `pam_d-0.1.4-fcs`

目标 RPM 软件包:

![](img/7021538f323e6521c571e727b770a451_394_0.png)

## 查找特定发行版的安全资源

大多数 Linux 发行版都有资源帮助你加固 Linux 并跟上该 Linux 版本特定的安全信息。以下是几个专注于多种 Linux 发行版安全的在线资源：

- **Red Hat Enterprise Linux 和 Fedora 安全** — 检查 Red Hat 安全网站 (`www.redhat.com/security`) 以获取 RHEL 安全问题（这些问题通常也涉及 Fedora 系统）。从这里你可以查找并阅读可用的更新。你还可以从 Red Hat, Inc. 获取有关安全培训和咨询的信息。对于 Fedora 安全问题，请参阅 Fedora Wiki (`http://fedaproject.org/wiki/Security/Features`)。

参考《Red Hat Enterprise Linux 4 安全指南》以深入了解 Red Hat 系统的 Linux 安全。你可以通过以下地址在线访问此指南：

`www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/en-US/Security-Guide`

- **Debian 安全** — Debian 安全信息页 (`www.debian.org/security`) 提供了一个查找安全公告、回答常见 Debian 安全问题以及指向安全文档链接的中心点。你可以在这里找到加固 Debian 的在线手册：

`www.debian.org/doc/manuals/securing-debian`

- **Ubuntu 安全** — 在 Ubuntu 安全页面查找 Ubuntu 安全指南和工具：`help.ubuntu.com/community/Security`
- **Gentoo 安全** — Gentoo Linux 安全页 (`www.gentoo.org/security`) 包含了工具、公告以及与 Gentoo 系统相关的安全策略和项目文档。在这里找到 Gentoo 安全手册：
