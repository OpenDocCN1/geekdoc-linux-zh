
# 107 核心系统管理

## 107.1 创建和管理特殊用途限制账户

- 创建和管理特殊用途限制账户
- 以下是本目标涵盖的文件、术语和工具的部分列表：`etcpasswd`, `etcshadow`, `etcgroup`, `etcskel`, `chage`, `getent`, `groupadd`, `groupdel`, `groupmod`, `passwd`, `useradd`, `userdel`, `usermod`

## 107.2 通过调度作业自动化系统管理任务（第 7 章）

- 管理 `cron` 和 `at` 任务
- 配置用户对 `cron` 和 `at` 服务的访问
- 配置 `anacron`
- 以下是本目标涵盖的文件、术语和工具的部分列表：`{d, daily, hourly, monthly, weekly}`, `etcat.deny`, `etcat.allow`, `etccrontab`, `etccron.allow`, `etccron.deny`, `varpool/cron/*`, `crontab`, `at`, `atm`, `anacron`, `anacontab`

## 107.3 本地化与国际化（第 6 章）

- 配置区域设置和环境变量
- 配置时区设置和环境变量
- 以下是本目标涵盖的文件、术语和工具的部分列表：`etctime`, `etclocaltime`, `usshare/zoneinfo`, 环境变量 (`LC_*`, `LC_ALL`, `LANG`, `TZ`), `usbin/locale`, `tzselect`, `tzconfig`, `date`, `iconv`, `UTF-8`, `ISO-8859`, `ASCII`, `Unicode`

# 108 核心系统服务

## 108.1 维护系统时间（第 7 章）

- 设置系统日期和时间
- 将硬件时钟设置为正确的 UTC 时间
- 配置正确的时区
- 基础 `NTP` 配置
- 使用 `pool.ntp.org` 服务的知识
- 对 `ntp` 命令的了解

## 108.2 系统日志（第 7 章）

- `syslog` 守护进程的配置
- 理解标准设施、优先级和操作
- 配置 `logrotate`
- 对 `rsyslog` 和 `syslog-ng` 的了解
- 以下是本目标涵盖的文件、术语和工具的部分列表：`syslog.conf`, `syslogd`, `klog`, `varlog`, `logger`, `logrotate`, `etclograte.conf`, `etclograte.d/`, `journalctl`, `etcsystem/journal.conf`, `varlog/journal/`

## 108.3 邮件传输代理 (MTA) 基础（第 9 章）

- 创建邮件别名
- 配置邮件转发
- 常用 `MTA` 程序（`postfix`, `sendmail`, `qmail`, `exim`）的知识（不涉及配置）
- 以下是本目标涵盖的文件、术语和工具的部分列表：`/.forward`, `sendmail` 仿真层命令, `newaliases`, `mail`, `mailq`, `postfix`, `sendmail`, `exim`, `qmail`

## 108.4 管理打印机和打印（第 6 章）

- 基础 `CUPS` 配置（针对本地和远程打印机）
- 管理用户打印队列
- 排除常规打印问题的故障
- 从配置的打印队列中添加和删除作业
- 以下是本目标涵盖的文件、术语和工具的部分列表：`CUPS` 配置文件、工具和程序；`etcups`; `lprpd` 留接口 (`lpr`, `lprqm`, `lpq`)

# 109 网络基础

## 109.1 互联网协议基础（第 8 章）

- 证明对网络掩码和 `CIDR` 表示法的理解
- 私有和公有“点四位”地址差异的知识
- 常用 `TCP` 和 `UDP` 端口（`20`, `21`, `22`, `23`, `25`, `53`, `80`, `110`, `123`, `143`, `161`, `162`, `389`, `443`, `465`, `514`, `636`, `995`）的知识
- `UDP`、`TCP` 和 `ICMP` 的差异和主要特征的知识
- `IPv4` 和 `IPv6` 之间主要差异的知识
- `IPv6` 基础特性的知识
- 以下是本目标涵盖的文件、术语和工具的部分列表：`etcservices`, `IPv4`, `IPv6`, `subnetting`, `TCP`, `UDP`

## 109.2 基础网络配置（第 8 章）

- 手动和自动配置网络接口
- 基础 `TCP/IP` 配置
- 设置默认路由
- 以下是本目标涵盖的文件、术语和工具的部分列表：`etchost`, `etcosts`, `switch.conf`, `ifconfig`, `ifup`, `ifdown`, `ip`, `route`, `ping`

## 109.3 基础网络故障排除（第 8 章）

- 手动和自动配置网络接口和路由表，包括添加、停止、重启、删除或重新配置网络接口
- 修改、查看或配置路由表并修正默认路由
- 调试与网络配置相关的问题
- 以下是本目标涵盖的文件、术语和工具的部分列表：`ifconfig`, `ip`, `ifup`, `ifdown`, `route`, `host`, `hostname`, `dig`, `netstat`, `ping`, `ping6`, `traceroute`, `tracepath`

## 109.4 配置客户端 DNS（第 8 章）

- 查询远程 `DNS`
- 配置本地 `DNS`
- 修改 `DNS` 解析顺序
- 以下是本目标涵盖的文件、术语和工具的部分列表：`etcresolv.conf`, `switch.conf`, `host`, `dig`, `etcosts`

# 110 安全

## 110.1 执行安全任务（第 10 章）

- 审计具有 `SUID/SGID` 位的系统
- 设置密码过期信息
- 能够使用 `nmap` 和 `netstat` 发现开放端口
- 设置登录、进程和内存限制
- 确定哪些用户已登录
- 基础 `sudo` 配置
- 本目标涵盖的文件、术语和工具：`find`, `passwd`, `lsof`, `nmap`, `chage`, `netstat`, `sudo`, `sudoers`, `su`, `usermod`, `ulimit`, `who`, `last`

## 110.2 设置主机安全

- 理解影子密码及其工作原理
- 关闭未使用的网络服务
- 理解 `TCP` 封装
- 以下是本目标涵盖的文件、术语和工具的部分列表：`etcpasswd`, `etcshadow`, `etcinetd.d/*`, `etcinetd.conf`, `inetd.d/*`, `ectittab`, `etcosts.allow`, `etcosts.deny`

## 110.3 使用加密加密数据（第 10 章）

- 执行 `OpenSSH 2` 配置
- 理解 `OpenSSH 2` 服务器密钥
- 执行基础 `GnuPG` 配置
- 理解 `SSH` 隧道（包括 `X11` 隧道）
- 以下是本目标涵盖的文件、术语和工具的部分列表：`ssh`, `ssh-keygen`, `ssh-agent`, `ssh-add`, `~/.ssh/id_rsa` 和 `id_rsa.pub`, `~/.ssh/id_dsa` 和 `id_dsa.pub`, `~/.ssh/ssh_host_rsa_key` 和 `ssh_host_rsa_key.pub`, `~/.ssh/authorized_keys`, `known_hosts`, `gpg`, `gnupg/*`

# 评估测试

1. `X` 服务器配置文件中的哪部分定义了你在 `Linux` 系统上使用的显示器组合？

    A. `Monitor`

    B. `Screen`

    C. `Modeline`

    D. `Device`

    E. `Module`

2. 如何判断你的系统使用的是 `inetd` 还是 `xinetd` 作为超级服务器？（选择两个）

    A. 执行 `ps ax | grep inetd`，并检查输出是否有 `inetd` 或 `xinetd` 的迹象。

    B. 执行 `superserver` 查看运行的超级服务器报告。

    C. 查找 `etcinetd.conf` 文件或 `etcinetd.d` 目录，它们分别是 `inetd` 或 `xinetd` 的迹象。

    D. 检查 `ectittab` 文件查看由 `init` 启动的超级服务器，`init` 负责此任务。

    E. 执行 `netstat -a | grep inetd` 并检查输出是否有 `inetd` 或 `xinetd` 的迹象。

3. `CUPS` 的 `lpc` 工具与 `BSD LPD` 及 `LPRng` 的对应工具有何不同？

    A. `lpc` 是 `CUPS` 特有的；它不随 `BSD LPD` 或 `LPRng` 分发。

    B. `CUPS` 不提供 `lpc` 命令，但 `BSD LPD` 和 `LPRng` 提供。

    C. `CUPS` 的 `lpc` 比 `BSD LPD` 和 `LPRng` 的对应工具复杂得多。

    D. `CUPS` 的 `lpc` 比 `BSD LPD` 和 `LPRng` 的对应工具简单得多。

    E. `lpc` 工具在这三个打印系统中是完全相同的。

4. 编辑哪个文件可以限制用户并发登录的数量？

    A. `/etc/pam.d/login-limits`

    B. `/etc/bashrc`

    C. `/etc/security/limits.conf`

    D. `/etc/inittab`

    E. `/etc/passwd`

5. 在配置计算机使用静态 `IP` 地址时，以下哪些是必要的？（选择两项。）

    A. `DHCP` 服务器的 `IP` 地址

    B. `NBNS` 服务器的主机名

    C. 计算机的 `IP` 地址
