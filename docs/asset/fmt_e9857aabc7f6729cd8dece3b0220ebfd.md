
File: '/sbin:init' ->'bin/systemd'

Size: 14 Blocks: 0 IO Block: 4096 symbolic link

Device: fd01b/6476d Inode: 9051 Links: 1

Access: (0755)rwxr-xr-x

Uid: 0 (root) Gid: 0 (root)

Context: system_u:object_t:s0

Access: 2016-02-03 23:40:39.139872288 -0500

Modify: 2016-02-02 23:40:39.139872288 -0500

Change: 2016-02-02 23:40:39.140872415 -0500

Birth:

```
你可以创建一个所有二进制文件原始 `mtime` 和 `ctime` 的数据库，并运行脚本比较当前的 `mtime` 和 `ctime`，将其与数据库进行比较并记录任何差异。然而，这种程序已经创建并且运行良好。它被称为入侵检测系统，在本章的后面将进行介绍。
你需要定期执行若干其他文件系统扫描。恶意攻击者的喜用文件或设置列于表 22.6。该表还列出了执行扫描的命令以及哪些文件或文件设置可能存在问题。
![](img/cc1e)
# 第五部分：学习 Linux 安全技术
## 表 22.6 附加文件系统扫描
| 文件或设置 | 扫描命令 | 文件或设置的问题 |
|---|---|---|
| SUID 权限 | find / -perm -4000 | 执行时临时成为文件所有者 |
| SGID 权限 | find / -perm -2000 | 执行时临时成为文件组的成员 |
| rhost 文件 | find /home -name .hosts | 允许系统信任另一个系统。它不应在 /home 中。 |
| 无所有者文件 | find /nouser | 表示与任何用户名关联的文件 |
| 无组文件 | find /nogroup | 表示与任何组名关联的文件 |
## 第 22 章：理解基础 Linux 安全
### 监控病毒
病毒是一种可以附加到已安装的系统软件中的恶意软件，它具有通过介质或网络传播的能力。认为 Linux 没有病毒是一个误区。病毒的恶意创建者通常确实关注于更流行的桌面操作系统，例如 Windows。然而，这并不意味着没有为 Linux 系统创建的病毒。
更重要的是，Linux 系统经常被用于处理服务，例如为 Windows 桌面系统的邮件服务器。此外，用于此类目的的 Linux 系统也需要扫描 Windows 病毒。
杀毒软件使用病毒特征扫描文件。病毒特征是根据病毒二进制文件创建的哈希值。该哈希值可以确定识别该病毒。杀毒程序拥有病毒特征数据库，用于与文件进行比较以查看是否存在匹配。根据新威胁的数量，可以频繁更新病毒特征数据库，以提供针对这些新威胁的保护。
对于你的 Linux 系统，一种良好的开源免费杀毒软件选择是 ClamAV。要在 Fedora 或 RHEL 系统上安装 ClamAV，请输入命令 `install clamav`。可以在 clamav.net 了解更多关于 ClamAV 的信息，那里有如何设置和运行杀毒软件的文档。
- 提示：你可以通过输入命令 `apt-cache search clamav` 来查看 Ubuntu 可用的包。Ubuntu 提供几个不同的包，因此在选择包之前，请查看 ClamAV 网站信息。
### 监控根工具包（rootkits）
rootkit 比病毒更具隐蔽性。rootkit是一种执行以下操作的恶意程序：
- 通过替换系统命令或程序隐藏自己
- 维持对系统的层级访问权限
- 绕过软件以定位它
rootkit 的目的是获取并维持对系统的 root 级访问权限。该术语是由 root（意为它必须拥有管理员权限）和 kit（工具包，意为它通常是几个协同运行的程序）组合而成的。
Linux 系统上可以使用 rootkit 检测器。要在 Fedora 或 RHEL 系统上安装 `chrootkit`，请执行命令 `yum install chrootkit`。要在 Ubuntu 系统上安装 `chrootkit`，请使用命令 `sudo apt-get install chrootkit`。
## 第五部分：学习 Linux 安全技术
> 提示：最好使用 Live CD 或闪存盘运行 chrootkit，这样结果就不会被 rootkit 绕过。Fedora Security Spin 在其 Live CD 上运行了 chrootkit。你可以在 labs.fedoraproject.org/security 获取此发行版。
使用 chkrootkit 检查 rootkit 非常简单。安装包并启动 Live CD 后，在命令行输入 chkrootkit。它会搜索整个文件结构并标记任何异常文件。
以下代码是运行 chkrootkit 后搜索关键字 INFECTED 的示例。使用 grep 命令注意到列为“infected”（已感染）的许多文件是 shell 命令文件。这是 rootkit 的典型特征。
```
# chkrootkit | grep INFECTED
Checking 'du'... INFECTED
Checking 'find'... INFECTED
Checking 'ls'... INFECTED
Checking 'lsof'... INFECTED
Checking 'pstree'... INFECTED
Searching for Suck rootkit... Warning: /sbin/init INFECTED
```
在上述 chkrootkit 代码的最后一行表明系统已被 Suck rootkit 感染。但实际上它并没有被该 rootkit 感染。在运行杀毒软件和 rootkit 检测软件等工具时，你经常会得到许多误报。误报是指实际上并不存在的病毒、rootkit 或恶意活动指示。在这种特定情况下，此误报是由一个已知漏洞引起的。
chkrootkit 工具应该定期计划运行，并且每当怀疑有 rootkit 时都要运行。要获取有关 chkrootkit 的更多信息，请访问 chkrootkit.org。
> 提示：你可能感兴趣的另一个 rootkit 检测器是 Rootkit Hunter (rkhunter)。运行 rkhunter 脚本检查系统是否存在恶意软件和已知 rootkit。在 `/etc/rkhunter.conf` 文件中配置 rkhunter。简单的示例是运行 `rkhunter -c` 来检查文件系统的 rootkit 和漏洞。
入侵检测系统（IDS）软件——一种监控系统活动（或其网络）并报告这些活动的软件包——可以帮助你监控系统潜在的入侵。与入侵检测系统软件密切相关的是一种防止入侵的软件包，称为入侵防御系统软件。其中一些包被捆绑在一起，以提供入侵检测和防御。
### 检测入侵
## 第 22 章：理解基础 Linux 安全
Linux 系统有多个入侵检测软件包可用。表 22.7 列出了几个较常用的工具。你应该知道 tripwire 已不再是开源的。然而，原始的 tripwire 代码仍然可用。更多详情见表 22.7 中列出的 tripwire 网站。
### 表 22.7 流行的 Linux 入侵检测系统
| IDS 名称 | 安装 | 网站 |
|---|---|---|
| aide | yum install aide apt-get install aide | http://aide.sourceforge.net |
| Snort | 从网站下载 rpm 或 tarball 包 | http://snort.org |
| tripwire | yum install tripwire apt-get install tripwire | http://tripwire.org |
高级入侵检测环境 (aide) 使用一种方法检测入侵。其中一些包被捆绑在一起，以提供入侵检测和防御。
此示例中 aide 列出的文件是感染的。然而，aide 也可以显示许多文件。
# 第 22 章：理解基础 Linux 安全
AIDE 数据库的创建、执行的比较以及其他若干配置设置都在 `/etc/aide.conf` 文件中处理。以下是该文件的部分显示。你可以在这里看到数据库文件和日志文件目录的名称：
```
# cat /etc/aide.conf
# AIDE 示例配置文件。
@define DBDIR /var/lib/aide
@define LOGDIR /var/log/aide
# 要读取的数据库位置。
database-file::$(DBDIR)/aide.db.gz
# 对应写入的数据库位置。
#database_out=sql:port:database:login_name:password:table
#database_out=aide.db.new
database_out::$(DBDIR)/aide.db.new
```
