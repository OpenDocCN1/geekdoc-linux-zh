
```bash
# journalctl -b 281514a27e7fa4b6a3c079d2b2bf4d4
May 01 11:07:24 fedora kernel: Linux version 6.14.4-200.fc41.x86_64
(mockbuild@gcc) 14.2 20250110 (Rel 14.2.1-7), GNU ld version 2.43
-1.5.fc41)
# SMP PREEMPT Dynamic May 02 25:45:16 UTC
May 01 11:07:24 fedora kernel: Command line: BOOT_IMAGE=(hd0,gpt2)
/vmlinuz-6.14.4-200.fc41.x86_64 root=UUID=bd8b71f4d-b3e6-4e50-
9ec1-ed5d6a2fb56 ro rootflags=subvol=root rhgb quiet
```

恶意程序经常修改文件。它们还可以尝试通过伪装成文件和程序来掩盖踪迹。然而，可以通过本文涵盖的各种监控策略发现它们。

## 验证软件包

通常情况下，如果你从标准仓库或下载站点安装软件包，不会遇到任何问题。但双检已安装的软件包以查看它们是否被篡改总是好的。实现此目的的命令是 `rpm -V package_name`。

在验证软件时，会将已安装软件包的信息与 rpm 数据库中的包元数据（第 10 章“获取和管理软件”）进行比较。如果没有发现问题，`rpm -V` 命令将返回空内容。然而，如果存在差异，表 23.5 显示了差异的代码和描述。

## 第五部分：学习 Linux 安全技术

## 表 23.5 软件包验证差异

| 代码 | 差异 |
|---|---|
| S | 文件大小 |
| M | 文件权限和类型 |
| S | MD5 校验和 |
| D | 设备文件的主设备和次设备号 |
| L | 符号链接 |
| U | 用户所有权 |
| G | 组所有权 |
| T | 文件修改时间 (mtime) |
| P | 所依赖的其他安装软件包（即能力） |

在接下来的部分列表中，所有已安装软件包都经过了验证检查。你可以看到返回了代码 5、S 和 T，这表示存在潜在问题。

```bash
# rpm -qV
S.5...T. c /etc/ansible/conf/httpd.conf
S.5...T. c /etc/ansible/hosts
S.5...T. c /etc/samba/smb.conf
```

你不需要一次验证所有的软件包。你可以一次验证一个软件包。例如，如果你想验证你的 nmap 软件包，只需输入 `rpm -V nmap`。

> 注意：要在 Ubuntu 上验证软件包，请使用 `debsums` 工具。它默认没有安装。要安装 debsums，使用命令 `sudo apt-get install debsums`。要检查所有软件包，使用 `debsums -a` 命令。要检查单个软件包，输入 `debsums packageName`。

## 扫描文件系统

除非你最近更新了系统，否则二进制文件不应出于任何原因修改。`find` 和 `rpm -V` 等命令可以帮助你判断二进制文件是否被篡改。

要检查二进制文件的修改，`find` 可以使用文件的修改时间或 mtime。文件 mtime 是文件内容最后被修改的时间。此外，`find` 还可以监控文件的创建/更改时间，或 ctime。

如果你怀疑有恶意活动，可以快速扫描文件系统以查看任何二进制文件是否被修改。

## 第 23 章：理解基础 Linux 安全

对于你的 Linux 系统，一个开源且免费的防病毒软件选择是 ClAV。要在 Fedora 或 RHEL 系统上安装 ClAV，请输入命令 `dnf install clamav`。你可以在 `clamav.net` 找到更多关于 ClAV 的信息，那里有关于设置和运行防病毒软件的文档。

> 提示
>
> 你可以通过输入命令 `apt-cache search clamav` 来查看 Ubuntu 安装可用的包。Ubuntu 有几个不同的包可用，因此在选择包之前，请查看 ClAV 网站。

### 监控 rootkit（后门工具）

rootkit（后门攻击工具）比病毒更具隐性。rootkit 是一种执行以下操作的恶意程序：

- 隐藏自己，通常通过替换系统命令或程序
- 维持系统的高级访问权限
- 能够绕过创建它的软件

rootkit 的目的是获取并维持对系统的 root 级访问权限。该术语是由 root（意味着必须具有管理员权限）和 kit（通常是几个协同运行的程序）组合而成的。

`chkrootkit` 是一个可以在 Linux 系统上运行的 rootkit 检测器。要在 Fedora 或 RHEL 系统上安装 chrootkit，请执行命令 `dnf install chrootkit`。要在 Ubuntu 系统上安装 chrootkit，请使用命令 `sudo apt-get install chrootkit`。

> 提示
>
> 最好使用 Live CD 或闪盘运行 chrootkit，这样结果就不会被 rootkit 绕过。Kali Linux 和 Fedora Security Lab 的 Linux 发行版中包含了 chrootkit。你可以在 fedaproject.org/labs/security 获取 Fedora 发行版。

使用 `chrootkit` 寻找 rootkit 非常简单。在安装或启动 Live 镜像后，在命令行输入 `chrootkit`。它会搜索整个文件结构以标记被感染的文件。

下面的代码显示了在受感染系统中运行 chrootkit 的情况。使用 `grep` 命令搜索关键字 `INFECTED`。注意，列为“感染”的许多文件是 Bash 命令文件。这是 rootkit 的典型特征。

```bash
# chrootkit | grep INFECTED
Checking 'du...' INFECTED
Checking 'find...' INFECTED
Checking 'ls...' INFECTED
Checking 'lsof...' INFECTED
Checking 'pstree...' INFECTED
Searching for Suckit rootkit... Warning: /bin/init INFECTED
```

在 chkrootkit 检查的最后一行中，指示系统已被 Suckit rootkit 感染。在运行实用程序（如防病毒软件和 rootkit 检测软件）时，你经常会得到许多误报。误报是指实际上并不存在的病毒、rootkit 或其他恶意活动的指示。在这种特定情况下，此误报是由已知的 bug 引起的。

`chkrootkit` 工具应该定期计划运行，并且在每次怀疑遭到 rootkit 感染时都运行。要获取有关 chkrootkit 的更多信息，请访问 chkrootkit.org。

> 提示
>
> 你可能感兴趣的另一个 rootkit 检测器称为 Rootkit Hunter (rkhunter)。rkhunter 脚本可以检查你的系统是否存在恶意软件和 rootkit。在 `/etc/rkhunter.conf` 文件中配置 rkhunter。作为一个简单的示例，运行 `rkhunter -c` 来检查文件系统是否存在各种 rootkit 和漏洞。要获取 RootkitHunter，请为 Ubuntu、Fedora 或 RHEL 安装 rkhunter 包。

### 检测侵入

入侵检测系统（IDS）——监控系统活动（或其网络）的潜在恶意活动并报告这些活动的软件包——可以帮助你监控系统受潜在的侵入。与入侵检测系统软件密切相关的是一种防止入侵的包，即入侵防御系统软件。其中一些包被捆绑在一起以提供入侵检测和防御功能。

Linux 系统有多种入侵检测软件包。表 23.7 列出了其中较受欢迎的实用程序。你应该知道，tripwire 的开源版本不再受 tripwire.org 支持。然而，原始的 tripwire 仍然可用，但未活跃维护，地址为 https://github.com/Tripwire/tripwire-open-source。

### 表 23.7 流行的 Linux 入侵检测系统

| IDS 名称 | 安装 | 网站 |
|---|---|---|
| aide | dnf install aide; apt-get install aide | https://sourceforge.net/projects/aide/ |
| Snort | 从网站下载 rpm 或 tarball 包 | http://snort.org |
| trip-wire | 访问 https://github.com/Tripwire/Tripwire-open-source 上的说明 | https://github.com/Tripwire/Tripwire-open-source |

高级入侵检测环境 (aide) 使用比较法来检测侵入。当你小时候，你可能玩过比较两张图片并找出不同之处的游戏。aide 实用工具使用了类似的方法。先创建一个“第一张照片”数据库。在之后的某个时间，创建另一个数据库“第二张照片”，aide 比较这两个数据库并报告不同之处。

要开始，你需要拍摄“第一张照片”。创建此照片的最佳时机是系统刚安装完成后。创建初始数据库的命令是 `aide -i`，运行需要很长时间。以下是部分输出内容。注意 aide 告诉我们它正在创建“第一张照片”数据库。

```bash
# aide -i
Start timestamp: 2025-08-05 18:01:33 -0400 (AIDE 0)
```

aide 告诉你它正在创建“第一张照片”数据库。

```bash
# aide -i
Start timestamp: 2025-08-05 18:01:33 -0400 (AIDE 0)
AIDE initialized. 
AIDE database written to /var/lib/aide/db.new
Number of entries: 2795
```

下一步是将“第一张照片”数据库移动到新位置。这可以保护原始数据库不被覆盖。将数据库移动到新位置并赋予新名称的命令如下：

```bash
# cp /var/lib/aide/db.new /var/lib/aide/db
```

当你准备好检查文件是否被篡改时，你需要创建一个新数据库（第二张照片）并与原始数据库进行比较。`aide -c` 命令创建一个新数据库并对旧数据库进行比较。输出显示了这种比较过程：

```bash
# aide -c
Start timestamp: 2025-05-04 18:14:59 -0400 (AIDE 0)
AIDE found differences between filesystem/:
Summary:
Total number of entries: 279514
Added entries: 0
Removed entries: 0
Changed entries: 3
Changed entries:
d > /usr/bin
f < /usr/find
```

| 目录/文件 | | 大小 | 修改时间 | 创建时间 | SHA256 |
|---|---|---|---|---|---|
| /usr/bin | 43834 | 43818 | 2025-05-04 18:46:15 -0400 | 2025-05-04 18:14:44 -0400 | 941aBDDE26fc88mp01LVt73oc |
| /usr/bin/du | 11 | 103360 | 2024-11-12 19:00:00 -0500 | 2025-05-04 18:13:53 -0400 | Xbr3QubeEb3MnVaIQ5qrsRzjK |
| /usr/bin/find | 20524 | 20524 | 2025-07-16 20:00:00 -0400 | 2025-05-04 18:14:53 -0400 | Yg3gq1+7e2U79NefeGOOXub |

示例中 aide 检查的文件受了影响。然而，aide 也会显示误报。

## 第 23 章：理解基础 Linux 安全

```bash
#database_out=file:aide.db.new
dabase_out=file:@$(DBDIR)/aide.db.new.gz
```

入侵检测系统对监控系统非常有帮助。当检测到潜在的入侵时，将输出结果与其他命令（如 `rpm -V`）和日志文件进行比较，可以帮助你理解并纠正针对系统的任何攻击。

# Linux 审计与审查

在审计 Linux 系统的健康状况时，你必须理解两个重要的术语。合规审查（Compliance review）是对整个计算机系统环境的审计，以确保为系统设置的策略和程序正在被正确执行。安全审查（Security review）是对当前策略和程序的审计，以确保它们遵循了最佳安全实践。

# 执行合规审查

与其他领域（如会计领域）类似，审计可以在内部进行，也可以由外部人员进行。这些审查可能简单到只需某人坐下将已实施的安全措施与公司声明的策略进行对比。然而，更流行的是使用渗透测试进行审计。

渗透测试是一种通过模拟恶意攻击来测试计算机安全性的评估方法。它也被称为渗透测试（pen testing）或道德黑客（ethical hacking）。你不再需要收集工具并寻找当地的黑客来帮助你进行这些测试。

[Kali Linux](https://www.kali.org) 是专为渗透测试创建的发行版。它可以从现场 DVD 或闪存盘运行。Offensive Security（https://www.offsec.com/courses-and-certifications）提供了使用 Kali Linux 的培训。

虽然渗透测试很有趣，但为了进行彻底的合规审查，还需要额外的手段。你应该还使用行业网站提供的清单。

# 执行安全审查

执行安全审查要求你了解最佳安全实践。有多种方法可以了解这些安全实践。以下是你可以参考的组织简列表：

- 国家标准与技术研究院 (NIST)，计算机安全资源中心
  - URL: https://csrc.nist.gov/projects/security-content-automation-protocol
  - 提供安全内容自动化协议（SCAP），用于评估配置合规性并检测漏洞软件版本
- 美国网络安全和基础设施安全局 (CISA)
  - URL: www.us-cert.gov
  - 提供国家网络警告系统（National Cyber Alert System）
  - 关于最新安全威胁的 RSS 订阅
- Sans 学院
  - URL: www.sans.org/security-resources
  - 提供计算机安全研究简报
  - 关于最新安全威胁的 RSS 订阅
- Gibson 研究公司 (Gibson Research Corporation)
  - URL: www.grc.com
  - 提供 Security Now! 安全网络广播

来自这些网站的信息将帮助你创建更强大的策略和程序。鉴于最佳安全实践变化之快，根据你组织的安全需求，经常进行安全审查是明智的。

现在你已经了解了许多基础 Linux 安全。困难的部分实际上是将所有这些概念付诸实践。

## 总结

基础 Linux 安全实践（如管理用户账户、保护密码以及管理软件和服务）构成了 Linux 系统上所有其他安全措施的基础。在这些工作的基础上，对系统的持续监控包括监控系统日志文件、检查恶意入侵以及监控文件系统。

定期对你的安全策略进行审查也很重要。审计有助于确保你的 Linux 系统是安全的，并且实施了适当的安全策略和实践。

你已经完成了收集安全程序和原则知识的第一步。仅仅了解基础是不够的，你还需要将高级 Linux 安全工具添加到你的安全工具箱中。在下一章中，将涵盖密码学和认证方法等高级安全主题。

## 练习

参考本章材料完成以下任务。如果你遇到困难，附录 B 中显示了任务解决方案（尽管在 Linux 中，完成一个任务通常有多种方法）。在参考答案之前，尝试每个练习。假设你正在运行 Fedora 或 Red Hat Enterprise Linux 系统（尽管某些任务也适用于其他 Linux 系统）。

1. 检查 systemd journal 中日志日志。
2. 列出包含系统用户密码文件的权限，并判断它们是否适当。
3. 使用单个命令确定你的账户密码有效期以及它是否会过期。
4. 安装 `lemon` 包（假设你没有安装该包），损坏 `/usr/bin/lemon` 文件（例如将 `/etc/services` 复制到那里），验证该文件已被篡改，并移除 `lemon` 软件包。
5. 你怀疑系统今天遭受了恶意攻击，重要的二进制文件被修改了。你应该使用哪种命令来找到这些文件？
6. 安装并运行 `chkrootkit` 以查看上一个练习中的恶意攻击是否安装了根内核程序（rootkit）。
7. 找到设置了 SUID 或 SGID 权限的文件。
8. 安装 `aide` 软件包。
9. 运行 `aide` 命令初始化 aide 数据库并将数据库复制到正确位置。
10. 运行 `aide` 命令检查系统上的任何重要文件是否被修改过。

# 第 24 章

# 理解高级安全

本章内容

- 理解哈希和加密
- 管理 Linux 安全
- 理解可插模块（pluggable modules）

# 使用密码学实现安全

使用密码学来保护信息。密码学是隐藏信息的科学。在默认情况下，Linux 系统已经使用了密码学。例如，/etc/

在本章中，你将学习使用密码学解密数据。

为了理解密码学概念，你应该了解以下几个术语：

- **明文 (Plain text)**：人类或机器可读的文本
- **密文 (Ciphertext)**：人类或机器不可读的文本
- **加密 (Encryption)**：将明文转换为密文的过程
- **解密 (Decryption)**：将密文转换为明文的过程
- **分组加密 (Block cipher)**：将数据分块加密的算法
- **流加密 (Stream cipher)**：不分块直接加密数据的的算法
