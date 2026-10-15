

## Linux 变种

我见过的最古老的 Linux 版本的 Rootkit 日期为 1994 年 10 月 11 日，且不完整。它仅包含 login、ps 和 netstat 木马。login 木马的魔术密码是 whoot!。netstat 木马增强了基于 UID 和 UNIX 套接字路径隐藏连接的能力。

下一个版本，自称为“Linux Rootkit II version 1.0”，于 1996 年 4 月 1 日发布，完全重写并借鉴了 SunOS Rootkit 的思路和灵感。此版本在隐蔽性方面覆盖最广。Linux Rootkit II version 1.1 紧随其后于 1996 年 4 月 20 日发布。它修复了一些错误并添加了一个更简单的嗅探器，更适合后台使用，一个“将 shell 绑定到套接字”的实用程序，以及用于删除（而非清零）utmp/wtmp/lastlog 条目的实用程序。Linux Rootkit 现在是一个非常完整且危险的软件包。与 SunOS Rootkit 变种一样，此版本包含 chfn、chsh、inetd、top、rshd 和 syslogd 的木马版本。其中许多木马识别魔术密码，默认是 lrk r0x，且一些识别特殊用户 rewT。表 19.2 包含 Linux Rootkit 中的程序列表。

## 检测 Rootkit

除非入侵者未能很好地从日志文件中清除其访问痕迹，否则攻击很难被检测到。大多数系统管理员直到被其他站点的人联系或磁盘因嗅探器的日志而开始填满时，才知道自己的站点已被入侵。如果你无法解释磁盘使用情况，你应该感到警惕，尤其是在 du 和 ls 木马存在的背景下。

一旦怀疑机器遭受了 Rootkit 攻击，你可以做几件事来验证这一点。最简单的方法是尝试使用 -/ 选项运行 du、ls、ps 和 netstat。如果其中任何一个接受此选项，则说明已安装了 Rootkit。此外，掩码列表处理中没有短路；即使使用掩码规范命中，检查仍会继续。因此，较大的规范列表可能会导致程序出现明显的减速。在 /dev 中使用 file 找到的文本文件（尤其是名称形式为 /dev/pty 且没有设备号的文件）也值得怀疑。

验证入侵的另一种方法是使用其完整性已知的系统程序。将 ps、ls、du、ifconfig 和 netstat 的原始副本放在写保护软盘上是个好主意。这些可在硬盘上的系统程序完整性存疑的情况下使用。在以下文本中描述的这些情况下，还可以使用许多第三方（即非标准）实用程序。

### top(1)
一个系统监控实用程序，结合了 ps(1)、uptime(1)、renice(8) 和 kill(1) 的功能。它可以在 ftp://eecs.nwu.edu/pub/top/ 找到，并可用于可靠地检查 SunOS 主机上是否存在 rogue 程序，因为 SunOS 版本的 Rootkit 不包含 top(1)。

### lsof
List Open Files (ftp://vic.cc.purdue.edu/pub/tools/unix/lsof/) 列出所有打开的文件，包括打开的网络套接字。

### 表 19.2 Linux Rootkit II v1.0 中的程序。

| Tool | Description |
|------|-------------|
| chfn | 如果在提示输入姓名时输入魔术密码，你将被放入 uid 0 /bin/sh shell，而不是被提示输入密码以提交对你的 finger 信息的任何更改。 |
| chsh | 如果在提示输入新 shell 时输入魔术密码，你将被放入 uid 0 /bin/sh shell。 |
| inetd | 当你连接到 rfe 服务（Radio Free Ethernet）时运行 /bin/sh -i 作为服务器。许多 Linux 发行版在 /etc/services 中不列出此服务，且 Rootkit 的安装程序也不会添加它。 |
| login | 允许在关闭所有日志记录的情况下以 root 登录。有两种触发方式：魔术用户 ID rewT，允许即使在未受保护的终端上也以 root 登录且用户永远不会被查询密码；或任何用户 ID 配合魔术密码 lrkroX。 |
| ls/du | 这些与 SunOS 附加组件相同。注意，由于 Linux 发行版是 POSIX，使用 fnmatch() 而不是 strcmp() 来允许掩码文件中使用正则表达式将非常容易（GNU 的 ls，即 Linux 中使用的 ls，已经使用 fnmatch）。 |
| ifconfig | 这与 SunOS 版本相同。 |
| netstat | 基于 UID 和 UNIX 套接字路径添加了掩码。netstat 包含“showall”(-a) 选项。 |
| passwd | 如果输入 Rootkit 魔术密码而不是用户密码，则以 UID、EUID、GID 和 EGID 设为 0 的方式运行 /bin/bash。 |
| ps | 这与 SunOS 版本相同。 |

