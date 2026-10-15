
操作系统和服务服务的检测完成。请在 `http://nmap.org/submit/` 报告任何错误结果。
`Nmap done: 1 IP address (1 host up) scanned in 21.90 seconds.`

你可以使用 `scanlog` 守护进程来检测是否对你的系统进行端口扫描。只需安装软件包并运行该服务即可。如果 `scanlog` 检测到（可能的）端口扫描，相应的警告信息将写入 `/var/log/messages` 文件。

注意：扫描远程系统的端口可以被视为攻击的准备。在扫描互联网上的系统之前，请记住这一点。

## 使用 Wireshark 分析网络

`Wireshark`（以前称为 `Ethereal`）是一种用于分析网络流量的工具。为了捕获所有流量，`Wireshark` 需要以杂杂模式启动。要捕获所有流量，只需选择接口即可。

> 注意：更多信息，请访问 `nmap.org` (`http://nmap.org`)。

## 使用 OpenVAS 检测漏洞

漏洞评估系统 (`OpenVAS`) 是著名的 `Nessus` 的一个分支。2005 年，`Nessus` 的许可从开源转变为专有。`OpenVAS` 是从 `Nessus` 的最后一个开源版本分支出来的。

`SLES 11` 并不包含 `OpenVAS` 或 `Nessus`。如果你想查看 `OpenVAS`，可以从 `software.openuse.org` `openSUSE Build Service` 下载 RPM 软件包。

`OpenVAS` 由两个组件组成：

- `OpenVAS server`：这是扫描器，对目标主机运行扫描并交付结果。扫描使用插件定义，插件会更新以包含最近的安全漏洞。
- `OpenVAS client`：这是一个终端和 GUI 应用程序，用于控制 `OpenVAS` 服务器、执行扫描并管理结果。

## 使用 Snort 进行入侵检测

`Snort` 是一种基于攻击特征的入侵检测系统 (`IDS`)。它是目前最复杂的开源 `IDS`。它扫描网络流量以匹配任何已知攻击模式。

`SLES 11` 不包含 `Snort`。如果你想查看 `Snort`，可以从 `software.openuse.org` `openSUSE Build Service` 下载 RPM 软件包。

你需要将运行 `Snort` 的计算机连接到网络中，使其能够监控所有流量，例如连接到交换机的镜像端口。`Snort` 的优势在于你可以用一台主机监控整个网络。

可以检测已知攻击，但对未知攻击的能力有限。类似于病毒杀毒软件，`Snort` 需要使用最新的特征。`www.snort.org` 提供了付费订阅，以便在规则开发后立即获取。注册用户可以在五天后免费获取这些规则。如果你有必要的知识，也可以创建自己的规则。

基础配置在 `/etc/sysconfig/snort` 和 `/etc/snort/snort.conf` 中完成。规则也保存在 `/etc/snort/` 目录下。`Snort` 通过脚本 `/etc/init.d/snort` 启动。

> 注意：更多信息，请访问 `Snort` 网站 `www.snort.org`。

## 使用 Tripwire 检查文件系统完整性

`Tripwire`（正式称为 `Open Source Tripwire`，因为也有商业版本）是一种用于检查文件系统修改的工具。它可以配置为当某些文件的任何属性被修改时发送警报。这些属性可以是权限、所有者、大小、时间戳等。

当 `Open Source Tripwire` 初始化时，它会扫描配置的文件系统，并将为每个文件找到的信息存储在数据库中。这第一批收集的信息将用于在稍后比较文件的属性。如果发生任何更改，将通知用户。`Open Source Tripwire` 不在数据库中存储整个文件，而仅存储哈希（`hashes`）。

`Tripwire` 未包含在 `SLES 11` 中。如果你想深入了解此工具，可以从 `openSUSE Build Service` 下载 RPM 包，地址为：`software.opensuse.org/search` (`http://software.opensuse.org/search`)。

> 注意：欲了解更多关于 `Tripwire` 的信息，请访问访问 `www.tripwire.com` (`http://www.tripwire.com`)。`Open Source Tripwire` 位于 `sourceforge.net/projects/tripwire/` (`http://sourceforge.net/projects/tripwire/`)。

## 目标 6

## 理解 SELinux

注意：包含此节是因为 CompTIA Linux+ 目标在 CompTIA 认可 LPIC Level One 之前列出了它，但 `SELinux` 并不是 LPIC Level One 目标的一部分。然而，在 CompTIA 为 Linux+ 认可 LPIC Level One 之后的课程修订中，这些信息并未删除，因为某些学生可能仍然发现这些信息有用。

安全增强型 Linux (`SELinux`) 是 Linux 内核的扩展，用于提供多种安全策略。它基于强制访问控制 (`MAC`)。`MAC` 意味着每当进程尝试访问资源时，都会评估额外的规则（策略），以决定是允许访问还是拒绝访问。

`SELinux` 最初由国家安全局 (`NSA`) 开发，是许多现有的 Linux 发行版的一部分。在 `SLES 11` 中，它以一种名为“技术预览（Technology Preview）”的形式提供。这意味着该技术已提供，但目前尚不支持支持。`Novell` 也未提供任何供 `SELinux` 使用的示例或规则。

`SELinux` 的配置相当复杂，很容易导致系统配置错误。

如果你想查看 `SELinux`，首先需要通过使用 `inserv -r boot.apparmor` 关闭 `AppArmor`。

`SELinux` 有三种可以处于模式：

- 强制模式 (`Enforcing`)。执行 `SELinux` 策略。`SELinux` 根据 `SELinux` 策略规则拒绝访问。
- 许可模式 (`Permissive`)。不执行 `SELinux` 策略。`SELinux` 不拒绝访问，但对于在强制模式下会被拒绝的操作，会记录拒绝日志。
- 禁用模式 (`Disabled`)。`SELinux` 已禁用。

要设置策略规则，必须安装两个包：`policyutils` 和 `checkpolicy`。当你使用 `YaST` 安装这些包时，会自动安装额外的包（库）。此外，你可能想要安装 `selinux-doc` 包，它包含文档（可以在 `/usr/share/selinux-doc/` 中找到）。

要在系统上启用 `SELinux`，你需要在启动提示符处提供以下内核参数（或在彻底测试后，将其添加到 `GRUB` 配置文件中）：`selinux=1`。

由于上述原因，我们在此门课程中不涵盖 `SELinux` 的配置。

### 总结

| 目标 | 总结 |
|---|---|
| 管理和保护 Linux 环境 | 你应该在绝对必要时才使用 `root` 账户。你可以使用 `sudo`、`su` 或 `gnomeau` 工具授予其他用户有限的 `root` 级访问。<br>用户账户和其他安全相关设置的默认值可以使用 `YaST` 本地模块进行配置。<br>配置设置被写入各种文件，最相关的是 `/etc/default/` 中的文件和 `/etc/login.defs` 文件。 |
| 使用 OpenSSH 提供安全的远程访问 | `SSH` 壳的开发通过加密身份验证字符串（通常是登录名和密码）以及主机之间交换的所有其他数据来确保传输的安全。<br><br>`SLES 11` 安装 `OpenSSH` 包，其中包含 `ssh`、`scp` 和 `sftp` 等程序，作为 `Telnet`、`login`、`rsh`、`rcp` 和 `FTP` 的替代方案。 |
| 使用 PAM 配置用户认证 | Linux 在认证过程中使用可插认证模块 (`PAM`) 作为应用程序与认证系统之间通信的层。<br><br>在 `PAM` 框架内，有四种不同的模块类型：<br>* `Auth`（认证)<br>* `Account`（账户)<br>* `Session`（会话)<br>* `Password`（密码)<br><br>控制标志决定了模块成功或失败时会发生的情况：<br>* `Required`（强制）<br>* `Requisite`（必须）<br>* `Sufficient`（足够）<br>* `Optional`（可选） |

`/etc/pam.d/` 中的文件用于配置 `PAM`，`/etc/security/` 中的文件为某些模块提供了额外的配置选项。

## 第 8 节 理解安全相关工具

| 目标 | 总结 |
| --- | --- |
| 确保文件完整性 | 文件可能具有相同的大小名称，但如果只有几个比特不同，仍然是不同的。以下工具允许你确定文件与参考文件相比是否被修改：<br>- `md5sum`<br>- `shasum`<br>- `gpg` |
| 使用安全相关实用程序 | 以下工具可以帮助你发现哪些服务在哪些端口上监听、服务器上是否存在漏洞、是否存在异常的网络流量，或者文件与之前的某个点相比是否被修改：<br>- `nmap`<br>- `wireshark`<br>- `OpenVAS`<br>- `snort`<br>- `tripwire` |
| 理解 SELinux | 安全增强型 Linux (`SELinux`) 是 Linux 内核的扩展，用于提供多种安全策略。它基于强制访问控制 (`MAC`)。`SELinux` 最初由国家安全局 (`NSA`) 开发，是许多现有的 Linux 发行版的一部分。在 `SLES 11` 中，它以一种名为“技术预览（Technology Preview）”的形式提供。这意味着该技术已提供，但目前尚不支持。 |

## 术语

| 术语 | 描述 |
|---|---|
| 密钥哈值认证码 (`HMAC`) | 响应需要本地 Secure Shell 私钥请求的软件组件。 |
| `last` | 显示来自 `/var/wtmp` 的最近登录用户。（注：此处原文描述似乎与术语对应有误，`last` 通常用于查看登录历史，而描述像是 `agent` 的功能，但按要求翻译，此处按原文翻译：显示来自 `/var/wtmp` 的最近登录用户。） |
| 强制访问控制 (`MAC`) | 基于一组安全策略访问资源的系统。 |
| `md5sum` | 计算文件的 MD5 哈希。 |
| 消息摘要 5 (`MD5`) | Linux 使用的哈希算法。 |
| `nmap` | 用于扫描本地或远程系统的端口。 |
| `Open Source Tripwire` | 见 `Tripwire`。 |
| `OpenSSH` | Linux 上的 SSH 实现。 |
| 漏洞评估系统 (`OpenVAS`) | 用于监控安全漏洞的程序。 |
| 可插认证模块 (`PAM`) | Linux 上管理访问的软件子系统。 |
| 主组 | 用户在 `/etc/passwd` 中指定的组，成为新创建文件和目录的组所有。 |
| 私钥 | 常用于加密数据和生成数字签名的非对称密钥。 |
| 公钥 | 常用于加密数据和验证数字签名的非对称密钥。 |
| 远程拨入用户服务 (`RADIUS`) | 提供集中认证和跟踪的网络服务。 |
| Rivest, Shamir, Adleman (`RSA`) | 今日常用的非对称加密算法。 |
| `r` 工具 | 指被 Secure Shell 替代的传统 `login`、`rsh` 和 `rpc` 网络工具。 |
| `scanlog` | 用于检测和记录端口扫描攻击的守护进程。 |
| `scp` | 使用 Secure Shell 传输文件。 |
| 安全哈希算法 1 (`SHA-1`) | 各种网络和软件常用的哈希算法。 |
| 安全增强型 Linux (`SELinux`) | Linux 系统上提供安全相关策略控制的软件组件和内核扩展。 |
| `sftp` | 传统 `FTP` 程序的 Secure Shell 替代品。 |
| `sg` | 在当前会话内由 Linux 用户更改主组。它功能上等同于 `newgrp` 命令。 |
| `sha1sum` | 计算文件的 SHA1 哈希。 |
| `Snort` | 一用于识别网络流量攻击的常用网络 IDS。 |
| `ssh-add` | 将新的 Secure Shell 密钥注册到 `ssh-agent`。 |
| `ssh-agent` | 响应需要使用本地 Secure Shell 私钥请求的软件组件。 |
| `ssh-keygen` | 用于生成 Secure Shell 公钥/私钥对。 |

`ssh-keyscan` 命令 — 用于从其他服务器收集安全公钥。

`sudo` 命令 — 用于通过 `/etc/sudoers` 中的条目以另一个身份运行命令。

对称加密（`symmetric encryption`） — 一种使用相同密钥对数据进行加密和解密的方法。

`tcpdump` 命令 — 用于分析本地网络接口上的网络流量。

`Triple-DES` — `DES` 的扩展，使用了三次 `DES` 算法。

`Tripwire` — 一种常见的基于主机的入侵检测系统（IDS），用于识别关键系统文件的更改。

双因子认证（`two-factor authentication`） — 一种要求用户使用两种不同形式身份验证的登录方法。

`ulimit` 命令 — 用于配置系统资源限制。

`updatedb` 命令 — 更新 `locate` 和 `locate` 命令使用的文件和目录数据库。

`visudo` 命令 — 用于编辑 `/etc/sudoers` 文件中的条目。

`Wireshark` — Linux 系统中常用的图形化网络流量分析工具。

### 章节练习

## 练习 8-1

## 配置 sudo

在此练习中，你将练习配置 `sudo`。

配置 `sudo` 以允许 `geeko` 用户在 `da-host` 上以 `root` 杀死进程。

### 完成练习的详细步骤

在 `da-host` 上完成以下操作：

- 1. 打开终端窗口并使用 `su -` 命令和密码 `novel` 切换到 `root`。
- 2. 在 shell 提示符下，输入 `visudo`。
- 3. 滚动到 "`Defaults targetpw...`" 这一行。
- 4. 通过在以下行的开头放置 `#` 来注释掉这些行：

```
