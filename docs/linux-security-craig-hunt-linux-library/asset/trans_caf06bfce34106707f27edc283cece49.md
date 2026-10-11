

下一节介绍如何下载并安装最新版本的 Nmap 软件包。

## 安装 Nmap

Nmap 的主要分发来源是 www.insecure.org。你可以从该网站下载完整的源代码或 RPM 软件包。最简单的方法是使用远程源进行安装，如下所示：

```bash
[ramon]:~$ rpm -vhU http://www.insecure.org/nmap/dist/nmap-2.53-1.i386.rpm
```

安装完成后，你将使用位于默认路径 `/usr/bin/nmap` 的主 Nmap 可执行文件。下一节描述了 Nmap 工具的一些常见用途。

## 使用 Nmap

尽管 Nmap 是一个全面的网络审计工具，但本书对其讨论集中在识别存活主机、活动的网络服务以及远程操作系统类型的功能上，因为这是 Nmap 最有用的领域。

Nmap 最简单的用法是识别在任一时刻网络上哪些主机是*存活的*（在线且可用）。这项任务被称为*端口扫描*。列表 5.5 展示了使用 Nmap 对整个子网进行端口扫描的示例。

### 列表 5.5 使用 Nmap 对整个子网进行端口扫描

```bash
[ramon]:~$ sudo nmap -sP 192.168.1.0/24

Starting nmap V. 2.53 by fyodor@insecure.org
(http://www.insecure.org/nmap/)
Host plus (192.168.1.5) appears to be up.
Host donald (192.168.1.7) appears to be up.
Host minnie (192.168.1.44) appears to be up.
Host dumbo (192.168.1.67) appears to be up.
Nmap run completed - 256 IP addresses (4 hosts up) scanned in 9 seconds
```

如果主机响应 ICMP Echo 请求或 TCP ACK，Nmap 就认为该主机是*存活的*。

Nmap 的另一个流行用法是识别远程主机上哪些端口（TCP、UDP）是开放的。这被称为*TCP 扫描*。当目标系统上有一个监听守护进程响应针对该端口的网络请求时，该端口即为*开放*。

列表 5.6 展示了使用 Nmap 进行 TCP 扫描的示例。在此示例中，Nmap 发现目标主机共有三个 HTTP 端口开放：Secure Shell（TCP 服务编号 22）、SMTP 邮件（TCP 服务 25）和 Secure HTTP（TCP 服务 443）。请注意，默认情况下，Nmap 仅扫描前 1500 个左右的 TCP 端口。

### 列表 5.6 使用 Nmap 对单个目标主机进行 TCP 扫描

```bash
[ramon]:~$ sudo nmap -sS target.example.com

Starting nmap V. 2.53 by fyodor@insecure.org
(www.insecure.org/nmap/)
Interesting ports on target.example.com (192.168.1.1):
(The 1520 ports scanned but not shown below are in state: filtered)
    Port      State      Service
    22/tcp    open       ssh
    25/tcp    open       smtp
    443/tcp   closed     https
Nmap run completed -- 1 IP address (1 host up) scanned in 178 seconds
```

第三个示例说明了 Nmap 识别远程主机上运行的操作系统类型并检查其 TCP 实现特性的能力。Nmap 的开发者称此功能为*TCP 指纹识别*，其实现相当复杂，使用一个持续更新的文件包含指纹模板，并将其与目标的 TCP 响应进行比较。

列表 5.7 展示了 Nmap 的一个运行样本，用于识别三个目标主机的操作系统：Lucent Pipeline PL75 路由器、Solaris 2.5.1 工作站和 Linux 服务器。请注意，列表 5.7 中的部分输出包括难度等级（Difficulty），它告诉你在网络上识别目标操作系统有多难。请注意，在三个目标中，Linux 获得了最高的难度等级！

### 列表 5.7 使用 Nmap 识别远程主机的操作系统

```bash
[ramon]:~$ sudo nmap -O 192.168.1.1 192.168.1.100 192.168.1.200

Starting nmap V. 2.53 by fyodor@insecure.org
(www.insecure.org/nmap/)
Interesting ports on router (192.168.1.1):
(The 1522 ports scanned but not shown below are in state: closed)
    Port      State      Service
    23/tcp    open       telnet
TCP Sequence Prediction: Class=random positive increments
Difficulty=15144 (Worthy challenge)
Remote OS guesses: Ascend P130 Router, Ascend P75
Interesting ports on fantasia (192.168.1.100):
(The 1519 ports scanned but not shown below are in state: closed)
    Port      State      Service
    21/tcp    open       ftp
    22/tcp    open       ssh
    139/tcp   open       netbios-ssn
    6000/tcp  open       X11
TCP Sequence Prediction: Class=random positive increments
Difficulty=23419 (Worthy challenge)
Remote operating system guess: Solaris 2.5, 2.5.1
Interesting ports on penguin (192.168.1.200):
(The 1516 ports scanned but not shown below are in state: closed)
    Port      State      Service
    21/tcp    open       ftp
    22/tcp    open       ssh
    23/tcp    open       telnet
    80/tcp    open       http
    989/tcp   open       ftps-data
    1080/tcp  open       socks
    3001/tcp  open       nessusd
TCP Sequence Prediction: Class=random positive increments
Difficulty=2630920 (Good luck!)
Remote operating system guess: Linux 2.1.122 - 2.2.14
Nmap run completed -- 3 IP addresses (3 hosts up) scanned in 10 seconds
```

一如既往，使用 Nmap 是一把双刃剑。虽然这个实用工具应该是每个系统管理员工具箱中的一部分，但请务必保持警惕并寻找网络上 Nmap 扫描的证据，因为这通常是攻击的前兆。第 3 章“系统监控与审计”中讨论的 swatch 和 logcheck 工具非常适合此目的。

Nessus 和 Nmap 都通过联系目标系统来识别潜在的漏洞。另一类基于主机（host-based）的审计工具可以实现同样的任务，但这些工具是在目标系统本身运行的。本书的下一节将更详细地探讨基于主机的审计，并介绍基于主机的网络安全审计方法的几个示例。

## 基于主机的审计工具

虽然 Nessus 和 Nmap 允许你扮演试图从公共网络入侵你的 Linux 服务器的“坏人”角色，但大多数成功的网络攻击实际上是从内部发起的。这一事实促使 Unix 社区设计了一种可以在系统内部使用的工具，用于识别来自内部攻击的漏洞。

1993 年，Dan Farmer（同时也是基于网络的 SATAN 审计工具的作者）发布了一个名为 COPS（Computer Oracle and Password System，计算机神谕与密码系统）的实用工具。作为基于主机的安全审计领域的先驱，COPS 实际上是一系列较小的工具的集合，每个工具都针对典型 Unix 系统中可能导致网络攻击的特定漏洞。这些检查范围涉及匿名 FTP 服务器、/etc/rc.* 目录、cron 条目以及 NFS 和 Sunmail 漏洞等领域。

德克萨斯 A&M 大学发布了一套基于主机的审计脚本（代号 Tiger）作为 COPS 的后续项目，但在 1994 年停止了新功能开发。如今，COPS 和 Tiger 都已严重过时，但一个优秀的继任者出现了。下一节将介绍 Advanced Research Corporation（高级研究公司）的 TARA 软件包。

## TARA

TARA（Tiger Auditors Research Assistant，老虎审计员研究助手）是 1999 年由一家私人公司（Advanced Research Corporation）在国立卫生研究院（NIH）资助下对德克萨斯 A&M 的 Tiger 系统进行更新的版本。该软件包在 GNU 通用公共许可证（GPL）的授权下发布到公共领域。

与 Tiger 一样，TARA 是一组由中心实用工具控制的 shell 脚本，该工具仍名为 tiger 以纪念其直接前身。该工具的主要目标是识别 Linux 服务器上使入侵者更容易通过网络获取 root 权限的设置。TARA 旨在以交互式方式运行，也可以定期以批处理模式运行。无论哪种方式，结果都是一份在其执行时发现的潜在漏洞报告。

下一节介绍如何下载并在你的 Linux 服务器上安装最新版本的 TARA 脚本。

### 安装 TARA

TARA 发行版可以直接从 ARC 网站 http://www-arc.com/tara/ 获取。没有可用的 RPM 软件包，因此你必须下载源代码归档文件。只需按照列表 5.8 所示解压并提取归档文件即可。

### 列表 5.8 提取 TARA 归档文件

```bash
[ramon]:~$ ls -l tara-2.0.9.tar.gz
-rw-r-- 1 ramon users 355267 Nov 18 17:13 tara-2.0.9.tar.gz
[ramon]:~$ gzip -dc tara-2.0.9.tar.gz | tar -xf -
[ramon]:~$ cd tara-2.0.9
[ramon]:~$ sudo mkdir -p /usr/spool/tiger/work
```

