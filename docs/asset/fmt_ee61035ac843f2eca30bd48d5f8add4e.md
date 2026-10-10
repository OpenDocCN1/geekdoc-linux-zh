
- 以下是使用的文件、术语和工具的部分列表：`/etc/cron.[daily,hourly,monthly,weekly]`, `/etc/at.deny`, `/etc/at.allow`, `/etc/crontab`, `/etc/cron.allow`, `/etc/cron.deny`, `/var/spool/cron*`, `crontab`, `at`, `at`, `atrm`

## 107.3 本地化和国际化（第 6 章）

- 区域设置（Locale settings）
- 时区设置
- 以下是使用的文件、术语和工具的部分列表：`/etc/timezone`, `/etc/localtime`, `/usr/share/zoneinfo`, 环境变量（`LC_*`, `LC_ALL`, `LANG`, `TZ`）, `/usr/bin/locale`, `tzselect`, `tzconfig`, `date`, `UTF-8`, `ISO-8859`, `ASCII`, `Unicode`

## 108 核心系统服务

### 108.1 维护系统时间（第 7 章）

- 设置系统日期和时间
- 将硬件时钟设置为正确的 UTC 时间
- 配置正确的时区
- 基本 NTP 配置
- 关于使用 `pool.ntp.org` 服务的知识
- 以下是使用的文件、术语和工具的部分列表：`/usr/share/zoneinfo`, `/etc/timezone`, `/etc/localtime`, `/etc/ntp.conf`, `date`, `hwclock`, `ntpd`, `ntpdate`, `pool.ntp.org`

### 108.2 系统日志（第 7 章）

- `syslog` 配置文件
- `syslog`
- 标准设施、优先级和操作
- 以下是使用的文件、术语和工具的部分列表：`syslog.conf`, `syslogd`, `klogd`, `logger`

### 108.3 邮件传输代理 (MTA) 基础（第 9 章）

- 创建邮件别名
- 配置邮件转发
- 常用 MTA 程序（`postfix`, `sendmail`, `qmail`, `exim`）的知识（不涉及配置）
- 以下是使用的文件、术语和工具的部分列表：`~/forward`, `sendmail` 仿真层命令, `newaliases`, `mail`, `mailq`, `postfix`, `sendmail`, `qmail`

### 108.4 管理 CUPS 打印机和打印任务（第 6 章）

- 基本 CUPS 配置（用于本地和远程打印机）
- 管理打印队列
- 排除常见的打印故障
- 从已配置的打印队列中添加和删除作业
- 以下是使用的文件、术语和工具的部分列表：CUPS 配置文件、工具和程序；`/etc/cups`; `lpd` 遗留接口 (`lpr`, `lprrm`, `lpq`)

## 109 网络基础

### 109.1 互联网协议基础（第 8 章）

- 对网络掩码的理解
- 了解私有和公共“点四位制”IP 地址的区别
- 设置默认路由
- 常用 TCP 和 UDP 端口知识（20, 21, 22, 23, 25, 53, 80, 110, 119, 143, 161, 443, 465, 993, 995）
- 关于 UDP、TCP 和 ICMP 区别和主要特征的知识
- IPv4 和 IPv6 之间主要区别的
- IPv6 基本特征知识
- 以下是使用的文件、术语和工具的部分列表：`/etc/services`, `ftp`, `telnet`, `host`, `ping`, `dig`, `traceroute`, `tracerpath`

### 109.2 基本网络配置（第 8 章）

- 手动和自动配置网络接口
- 基本 TCP/IP 配置
- 以下是使用的文件、术语和工具的部分列表：`/etc/hostname`, `/etc/hosts`, `/etc/resolv.conf`, `/etc/nsswitch.conf`, `ifconfig`, `ifdown`, `route`, `ping`

### 109.3 基本网络故障排除（第 8 章）

- 手动和自动配置网络接口和路由表，包括添加、停止、重启或重新配置网络接口
- 修改、查看或配置路由表，并修正设置错误的默认路由
- 以下是使用的文件、术语和工具的部分列表：`ifconfig`, `ifup`, `ifdown`, `route`, `host`, `dig`, `netstat`, `traceroute`

### 109.4 配置客户端 DNS（第 8 章）

- 演示在本地系统上使用 DNS
- 修改名称解析的顺序
- 以下是使用的文件、术语和工具的部分列表：`/etc/hosts`, `/etc/resolv.conf`, `/etc/nsswitch.conf`

## 安全

### 10.1 执行安全管理（第 10 章）

- 审计系统寻找带有 suid 位的文件
- 设置或更改用户密码和密码老化
- 能够使用 `nmap` 和 `netstat` 发现开放端口
- 设置用户登录、进程和内存使用的限制
- 基本 `sudo` 配置和使用
- 以下是使用的文件、术语和工具的部分列表：`find`, `nmap`, `chage`, `netstat`, `sudo`, `ulimit`, `passwd`

### 10.2 设置安全（第 10 章）

- 了解绕过密码的方法
- 关闭服务
- 了解封装（wrappers）
- 以下是使用的文件、术语和工具的部分列表：`/etc/allow`, `/etc/deny`, `/etc/inlogin`, `/etc/shadow`, `/etc/passwd.conf`, `/etc/passwd`

### 10.3 使用加密保护数据（第 10 章）

- 配置 OpenSSH 的知识
- 了解 SSH 密钥
- 使用 GPG 配置
- 了解 SSH 隧道
- 以下是使用的文件、术语和工具的部分列表：`ssh`, `ssh-keygen`, `ssh-add`, `gpg`, `~/.ssh/authorized_keys`, `~/.ssh/known_hosts`

# 评估

1. 这里的 `/etc/` 所在的行说明了以下哪一项？
    - A. 2
    - B. 3
    - C. 4
    - D. 5
    - E. 以上皆

2. 修改哪个文件可以限制用户登录数量？
    - A. `/etc/pam.d`
    - B. `/etc/bashrc`
    - C. `/etc/security`
    - D. `/init`

3. 在配置计算机使用 IP 地址时，哪些项是必须的？（选择两项）
    - A. 服务器的 IP 地址
    - B. 主机名
    - C. 计算机的 IP 地址
    - D. 网络掩码
    - E. NTP 服务器的 IP 地址

4. 以下命令实现了什么？
    `wc report.txt | tee wc`
    - A. 在 `report.txt` 和 `wc` 文件上启动 `wc` 编辑器；每个在一个窗口打开。
    - B. 显示 `report.txt` 的窗口计数并在新窗口显示信息。
    - C. 创建 `report.txt` 的行、字和字节计数，然后显示关于该报告的统计信息。
    - D. 清理与 `tee` 程序使用 `report.txt` 相关的内存泄漏。
    - E. 显示 `report.txt` 的行、字和字节计数，并将该输出拷贝到 `wc` 文件。

7. `/boot/grub/grub.cfg` 中的哪个字符定义了 OS 或内核定义的结束？
    - A. `;`
    - B. `)`
    - C. `}`
    - D. `*`
    - E. 以上都不是；定义以下一个目的标题行结束

8. `/etc/passwd` 条目中的数字 703 代表什么？
    `george:x:703:100:George Brown:/home/george:/bin/tcsh`
    - A. 账户的人类 ID (HID) 号
    - B. 账户的进程 ID (PID) 号
    - C. 账户的组 ID (GID) 号
    - D. 账户的全局唯一 ID (GUID) 号
    - E. 账户的用户 ID (UID) 号

9. `grep` 命令的作用是什么？
    - A. 它在两个程序之间创建一个流水管道。
    - B. 它在文件内容中搜索特定模式。
    - C. 它将两个或多个文件合并。
    - D. 它显示文件的最后几行。
    - E. 它在硬盘上定位文件。

10. 下列中哪些是 Linux 的日志文件系统？（选择三项。）
    - A. HPFS
    - B. ReiserFS
    - C. Ext2fs
    - D. Ext3fs
    - E. XFS

11. 你配置了计算机通过到互联网服务提供商（ISP）邮件服务器的隧道化 SSH 连接使用 SMTP 和 IMAP，以提高安全性。为什么在使用了 SSH 提供的加密之后，你可能仍然想对电子邮件使用 GPG 加密？
    - A. SSH 隧道只到达第一个邮件服务器；GPG 在通往或离开你邮件联系人路径上的所有计算机上对数据加密。
    - B. SSH 加密对于电子邮件来说是出了名的糟糕，尽管对于登录会话来说完全足够；因此，添加 GPG 可以提高安全性。
    - C. SSH 不加密邮件消息的标头；GPG 加密标头以防止窃听者获取你联系人的身份。
    - D. 使用 GPG 可以保证你的邮件消息不会包含感染你联系人计算机的意外病毒或蠕虫。
    - E. 这样配置后，SSH 将加密邮件标头和正文，但不会加密邮件的任何附件。

12. 下列哪些端口通常用于从邮件服务器计算机检索邮件？（选择两项。）
    - A. 110
    - B. 119
    - C. 139
    - D. 143
    - E. 443

# 评估测试

13. 你在 Secure Shell (SSH) 登录服务器上遇到偶发问题——有时用户可以登录，有时不能。在失败后，你可能会立即尝试什么来诊断这个问题？
    - A. 在服务器计算机上，在浏览器中输入 `http://localhost:631` 以访问 SSH 配置页面并检查其错误页是否有错误信息。
    - B. 输入 `diagnose sshd` 查看 SSH 服务进程 (`sshd`) 的诊断信息。
    - C. 输入 `tail /var/log/messages` 查找来自服务器的错误信息。
    - D. 检查 `/dev/sdX` 设备以查找来自服务器的错误信息。
    - E. 在服务器计算机上，输入 `sshd` 查看 SSH 的诊断信息。

14. `/.profile` 文件的功能是什么？
    - A. 它是 ProFTP 服务器的配置文件。
    - B. 它是你用户的 bash 启动脚本之一。
    - C. 它是 Profile 管理文件的配置文件。
    - D. 它的存在告诉 `tcsh` 忽略文件模式。
    - E. 它存储了用户的加密密码。

15. 你想在两年后如何对你的汽车进行检查？在指定的选项中，最好的方法是哪个？
    - A. 创建一个为期一个月的 `cal` 视图，其中*天*、*月*和*年* 指定未来检查的日期，让 Linux 在该日期运行你指定的程序。
    - B. 创建一个每小时运行一次的 cron 任务。该任务应该检查日期，当正确的日期到来时，使用 `mail` 通知你需要进行汽车检查。
    - C. 使用 GUI 日历程序为指定的日期创建一个闹钟。该程序将在指定的日期和时间显示你输入的消息。
    - D. 输入 *date*，其中 date 是一个日期规范。你可以指定一个命令，例如带有适当选项的 `mail`，通知你需要进行汽车检查。

16. 你如何配置计算机，使用 IP 地址为 172.24.21.1 的计算机作为所有未配置网络流量的网关？
    - A. `gateway default 172.24.21.1`
    - B. `gateway 172.24.21.1`
    - C. `route gateway 172.24.21.1`
    - D. `route add default 172.24.21.1`
    - E. `gw 172.24.21.1`

17. 你可以使用什么软件驱动盲文显示设备？（选择两项。）
    - A. Emacpeak
    - B. BRLTTY
    - C. 2.6.26 或更高版本的内核
    - D. GOK
    - E. 一个 framebuffer 驱动程序

18. 关于源 RPM 包，哪哪是正确的？
    - A. 它们由三个文件组成：原始 tar 包、一个更改的补丁文件和一个指示包真实性的 PGP 签名。
    - B. 它们需要编程知识才能重新构建。
    - C. 它们有时可以用于解决二进制包依赖问题。
    - D. 它们对于基于 RPM 的发行版编译软件是必要的。
    - E. 它们始终包含根据 GPL 条款许可的软件。

19. 你应该使用哪种工具将文件 `pumpkin.txt` 重命名为 `lantern.txt`？
    - A. `dd`
    - B. `rm`
    - C. `cp`
    - D. `mv`
    - E. `ln`

20. 你想运行一个名为 simibabang 的长时间科学模拟程序，该程序不需要任何用户交互；程序完全在磁盘文件上操作。如果你不想占用运行该程序的 shell，你应该输入什么来在后台运行 simibabang？
    - A. `start simibabang`
    - B. `simibabang &`
    - C. `bg simibabang`
    - D. `background simibabang`
    - E. `nice simibabang`

21. 下列哪些命令将在计算机上安装名为 `theprogram-1.2.3-4.i386.rpm` 的 RPM 包？（选择两项。）
    - A. `rpm -Uv theprogram-1.2.3-4.i386.rpm`
    - B. `rpm -i theprogram-1.2.3-4.i386.rpm`
    - C. `rpm -U theprogram-1.2.3-4.i386.rpm`
    - D. `rpm -e theprogram-1.2.3-4.i386.rpm`
    - E. `rpm -Vp theprogram-1.2.3-4.i386.rpm`

22. 什么工具可以诊断并修复许多常见的 Linux 文件系统问题？
    - A. `mkfs`
    - B. `fsck`
    - C. `chkdsk`
    - D. `scandisk`
    - E. `fdisk`

23. 你刚刚安装了 MySQL，并用它存储关于动物的信息。你可能首先使用哪个命令？
    - A. `CREATE animals;`
    - B. `USE animals;`
    - C. `CREATE TABLE;`
    - D. `INSERT INTO animals;`
    - E. `UPDATE animals;`

24. 下列哪些命令在 shell 中输入时显示帮助？（选择两项。）
    - A. `manual`
    - B. `man`
    - C. `?`
    - D. `info`
    - E. `hint`

25. 硬件时钟在关机时跟踪时间。在 x86 系统上时间以什么格式存储？（选择两项。）
    - A. 协调世界时 (UTC)
    - B. 互联网时间
    - C. 本地时间
    - D. 12小时制时间
    - E. 火时间

26. 你想知道加载了哪些内核模块。输入什么命令可以学习？
    - A. `insmod`
    - B. `depmod`
    - C. `modprobe`
    - D. `lsmod`
    - E. `modinfo`

27. 你想让 `music` 组的所有成员读取 `instruments.txt` 文件，该文件目前的权限为 0640 (-rwr--)，所有者为 `root`。如何实现？（选择两项。）
    - A. 在目录中执行 `chown music.txt`。
    - B. 在目录中执行 `chgrp music.txt`。
    - C. 在目录中执行 `chgrp instruments.txt`。
    - D. 在目录中执行 `0600 instruments.txt`。
    - E. 在目录中执行 `chown :music instruments.txt`。

28. 你想在另一个位置创建 `/usr/local/bin` 目录的链接。哪个说法正确？
    - A. 只有当 `/usr/local/bin` 在日志文件系统上才能这样做。
    - B. 你必须 `/usr/local/bin` 创建链接。
    - C. 只有当链接与原始目录位于同一文件系统时才能创建。
    - D. 只有系统管理员可以这样做。
    - E. 链接可能是符号链接。

29. 下列哪些在 Vi 的命令模式下可以保存文件并退出程序？（选择两项。）
    - A. `:rq`
    - B. `:wq`
    - C. `:re`
    - D. `:we`
    - E. `ZZ`

30. 用户主目录包含一个名为 `/.forward` 的文件，内容一行：`|~/junkme`。此配置的作用是什么？
    - A. 用户的传入邮件将转发到同一系统上的 `junkme` 用户。
    - B. 用户的传入邮件将存储在 `~/junkme` 文件中。
    - C. 用户的传入邮件将通过 `~/junkme` 程序发送。
    - D. 用户的传入邮件将被标记为垃圾邮件并删除。
    - E. 用户的传入邮件将转发到 `junkme` 计算机上的相同用户。

# 评估测试答案

- 1. B. "PS/2" 可以既指硬件接口，也可以指软件协议，但在 Protocol（协议）选项的上下文中，它明确指代软件协议。因此，选项 B 是正确的。选项 A 可能正确，但指定的行并不足以证明这一点；USB 鼠标使用 PS/2 协议或其变体，例如类型的 Intellimouse PS/2 协议。使用 PS/2 硬件端口和协议源于选项中的 IBM PS/2 计算机，现在许多其他计算机都在使用它们。配合 PS/2 使用的鼠标可以是任何操作系统，并没有标记为 IBM 的操作系统，因此选项 D 是错误的。斜杠（/）作为 PS/2 协议名称的一部分是有效的，因此选项 E 是错误的。更多信息，请参阅第 6 章“X Window 系统、本地化与打印”。
- 2. A. 检查进程列表（通过 `ps` 获取）以寻找超级服务器（super server）的迹象是确定哪一个实际上正在运行的最可靠方法，因此选项 A 是正确的。服务器配置文件或文件（如选项 C）的存在也是很好的诊断方法，某些已升级的系统可能同时拥有两套配置文件。没有标准的服务器工具可以决定使用哪一个，因此选项 B 是错误的。大多数发行版通过 SysV 启动脚本启动超级服务器；`/etc/inittab` 文件没有直接参与此过程，因为它会导致根启动，并且会包含任何正在监听连接的 `inetd` 或 `xinetd` 实例的指示。选项 E 发出了 `-p` 选项，这会导致程序显示进程名称。选项 E 是错误的。更多信息，请参阅第 10 章“保护你的系统”。
