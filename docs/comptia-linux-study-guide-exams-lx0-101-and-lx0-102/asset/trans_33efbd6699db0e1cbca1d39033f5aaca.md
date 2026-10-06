

# 考试 LX0-102 目标 xxxvii

- 创建和管理特殊用途和受限账户

- 以下是使用的文件、术语和工具的部分列表：/etc/passwd, /etc/shadow, /etc/group, /etc/skel, chage, groupadd, groupdel, groupmod, passwd, useradd, usermod

## 107.2 通过调度作业自动化系统管理任务（第 9 章）

- 管理 cron 和 at 任务

- 配置用户对 cron 和 at 服务的访问

- 以下是使用的文件、术语和工具的部分列表：/etc/cron.[daily,hourly,monthly,weekly], /etc/at.deny, /etc/at.allow, /etc/crontab, /etc/cron.allow, /etc/cron.deny, /var/spool/cron*, crontab, at, at, atrm

## 107.3 本地化和国际化（第 6 章）

- 区域设置（Locale settings）

- 时区设置

- 以下是使用的文件、术语和工具的部分列表：/etc/timezone, /etc/localtime, /usr/share/zoneinfo, 环境变量（LC_*, LC_ALL, LANG, TZ），/usr/bin/locale, tzselect, tzconfig, date, UTF-8, ISO-8859, ASCII, Unicode

## 108 核心系统服务

### 108.1 维护系统时间（第 7 章）

- 设置系统日期和时间

- 将硬件时钟设置为正确的 UTC 时间

- 配置正确的时区

- 基本 NTP 配置

- 关于使用 pool.ntp.org 服务的知识

- 以下是使用的文件、术语和工具的部分列表：/usr/share/zoneinfo, /etc/timezone, /etc/localtime, /etc/ntp.conf, date, hwclock, ntpd, ntpdate, pool.ntp.org

### 108.2 系统日志（第 7 章）

- syslog 配置文件

- syslog

- 标准设施、优先级和操作

### 简介

- 以下是使用的文件、术语和工具的部分列表：syslog.conf, syslogd, klogd, logger

### 108.3 邮件传输代理 (MTA) 基础（第 9 章）

- 创建邮件别名

- 配置邮件转发

- 常用 MTA 程序（postfix, sendmail, qmail, exim）的知识（不涉及配置）

- 以下是使用的文件、术语和工具的部分列表：~/forward, sendmail 仿真层命令, newaliases, mail, mailq, postfix, sendmail, qmail

### 108.4 管理 CUPS 打印机和打印任务（第 6 章）

- 基本 CUPS 配置（用于本地和远程打印机）

- 管理打印队列

- 排除常见的打印故障

- 从已配置的打印队列中添加和删除作业

- 以下是使用的文件、术语和工具的部分列表：CUPS 配置文件、工具和程序；/etc/cups; lpd 遗留接口 (lpr, lprrm, lpq)

## 109 网络基础

### 109.1 互联网协议基础（第 8 章）

- 对网络掩码的理解

- 了解私有和公共“点四位制”IP 地址的区别

- 设置默认路由

- 常用 TCP 和 UDP 端口知识（20, 21, 22, 23, 25, 53, 80, 110, 119, 143, 161, 443, 465, 993, 995）

- 关于 UDP、TCP 和 ICMP 区别和主要特征的知识

- IPv4 和 IPv6 之间主要区别的

- IPv6 基本特征知识

- 以下是使用的文件、术语和工具的部分列表：/etc/services, ftp, telnet, host, ping, dig, traceroute, tracerpath

### 109.2 基本网络配置（第 8 章）

- 手动和自动配置网络接口

- 基本 TCP/IP 配置

- 以下是使用的文件、术语和工具的部分列表：/etc/hostname, /etc/hosts, /etc/resolv.conf, /etc/nsswitch.conf, ifconfig, ifdown, route, ping

### 109.3 基本网络故障排除（第 8 章）

- 手动和自动配置网络接口和路由表，包括添加、停止、重启或重新配置网络接口

- 修改、查看或配置路由表，并修正设置错误的默认路由

- 以下是使用的文件、术语和工具的部分列表：ifconfig, ifup, ifdown, route, host, dig, netstat, traceroute

### 109.4 配置客户端 DNS（第 8 章）

- 演示在本地系统上使用 DNS

- 修改名称解析的顺序

- 以下是使用的文件、术语和工具的部分列表：/etc/hosts, /etc/resolv.conf, /etc/nsswitch.conf

## 安全

### 10.1 执行安全管理（第 10 章）

- 审计系统寻找带有 suid 位的文件

- 设置或更改用户密码和密码老化

- 能够使用 nmap 和 netstat 发现开放端口

- 设置用户登录、进程和内存使用的限制

- 基本 sudo 配置和使用

- 以下是使用的文件、术语和工具的部分列表：find, nmap, chage, netstat, sudo, ulimit, passwd

### 10.2 设置安全（第 10 章）

- 了解绕过密码的方法

- 关闭服务

- 了解封装（wrappers）

- 以下是使用的文件、术语和工具的部分列表：/etc/allow, /etc/deny, /etc/inlogin, /etc/shadow, /etc/passwd.conf, /etc/passwd

### 10.3 使用加密保护数据（第 10 章）

- 配置 OpenSSH 的知识

- 了解 SSH 密钥

- 使用 GPG 配置

- 了解 SSH 隧道

- 以下是使用的文件、术语和工具的部分列表：ssh, ssh-keygen, ssh-add, gpg, ~/.ssh/authorized_keys, ~/.ssh/known_hosts

# 评估

1. 这里的/etc/ 所在的行说明了以下哪一项？
A. 2
B. 3
C. 4
D. 5
E. 以上皆 

2. 修改哪个文件可以限制用户登录数量？
A. /etc/pam.d
B. /etc/bashrc
C. /etc/security
D. /init

3. 在配置计算机使用 IP 地址时，哪些项是必须的？（选择两项）
A. 服务器的 IP 地址
B. 主机名
C. 计算机的 IP 地址
D. 网络掩码
E. NTP 服务器的 IP 地址

4. 以下命令实现了什么？
wc report.txt | tee wc
A. 在 report.txt 和 wc 文件上启动 wc 编辑器；每个在一个窗口打开。
B. 显示 report.txt 的窗口计数并在新窗口显示信息。
C. 创建 report.txt 的行、字和字节计数，然后显示关于该报告的统计信息。
D. 清理与 tee 程序使用 report.txt 相关的内存泄漏。
E. 显示 report.txt 的行、字和字节计数，并将该输出拷贝到 wc 文件。

7. /boot/grub/grub.cfg 中的哪个字符定义了 OS 或内核定义的结束？
A. ;
B. )
C. }
D. *
E. 以上都不是；定义以下一个目的标题行结束

8. /etc/passwd 条目中的数字 703 代表什么？
george:x:703:100:George Brown:/home/george:/bin/tcsh

A. 账户的人类 ID (HID) 号
B. 账户的进程 ID (PID) 号
C. 账户的组 ID (GID) 号
D. 账户的全局唯一 ID (GUID) 号
E. 账户的用户 ID (UID) 号
