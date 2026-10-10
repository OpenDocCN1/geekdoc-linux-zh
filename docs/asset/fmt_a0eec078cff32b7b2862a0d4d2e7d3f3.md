
- `LC_`: 本地变量 第 368 页
- `ASCII`
- `ASCII` 第 1237 页 (词汇表)
- `Unicode`
- `Unicode` 第 1279 页 (词汇表)

## 108 基本系统服务

### 108.1 维护系统时间

- 设置系统日期和时间
  - `timedatectl`: 报告并设置系统时钟 第 613 页
- 将硬件时钟设置为正确的 `UTC` 时间
- 配置正确的时区
  - `Time` 第 371 页
- 基本 `NTP` 配置
- 了解使用 `pool.ntp.org` 服务

#### 使用的文件、术语和工具部分列表

- `/usr/share/zoneinfo`
  - `/usr/share/zoneinfo` 第 372 页
- `/etc/timezone` 第 372 页
- `/etc/localtime` 第 373 页
- `/etc/ntp.conf`
- `date`
  - `date`: 显示系统时间和日期 第 218 页
- `timedatectl`: 报告并设置系统时钟 第 613 页
- `hwclock`
- `ntpd`
- `pool.ntp.org`

### 108.2 系统日志记录

- `Syslog` 配置文件
  - `rsyslog.conf` 第 620 页
- `syslog`
  - `rsyslog`: 记录系统消息 第 620 页
- 标准设施、优先级和操作
  - `Selectors` 第 620 页
  - `Facilities` 第 620 页
  - `Priorities` 第 620 页
  - `Actions` 第 621 页

#### 使用的文件、术语和工具部分列表

- `syslog.conf`
  - `rsyslog.conf` 第 620 页
- `syslogd`
  - `rsyslogd`: 记录系统消息 第 620 页
- `klogd`
- `logger`

### 108.3 邮件传输代理 (`MTA`) 基础知识

- 参见第 20 章：`sendmail` 设置邮件服务器、客户端及其他 第 739 页
- 创建电子邮件别名
  - `/etc/aliases` 第 746 页
- 配置电子邮件转发
  - `~/.forward` 第 747 页
- 了解常用 `MTA` 程序（`Postfix`, `sendmail`, `Qmail`, `exim`）（无需配置）
  - `Alternatives to sendmail` 第 741 页

#### 使用的文件、术语和工具部分列表

- `~/.forward`
  - `~/.forward` 第 747 页
- `sendmail` 模拟层命令
  - `newaliases`
  - `newaliases` 第 747 页
  - `mail`
  - `mailq`
  - `mailq` 第 748 页
- `Postfix`
  - `Postfix` 第 742 页
- `sendmail`
  - `Introduction to sendmail` 第 740 页
  - `Setting Up a sendmail Mail Server` 第 742 页
  - `JumpStart I: Configuring sendmail on a Client` 第 743 页
  - `JumpStart II: Configuring sendmail on a Server` 第 744 页
  - `Working with sendmail Messages` 第 745 页
  - `Configuring sendmail` 第 748 页
- `exim`
  - `exim4` 第 742 页
- `qmail`
  - `Qmail` 第 742 页

### 108.4 管理打印机和打印

*参见第 13 章：使用 `CUPS` 打印 第 555 页*

- 基本 `CUPS` 配置（用于本地和远程打印机）
  - 系统自动配置本地打印机 第 558 页
  - `JumpStart I`: 使用 `system-config-printer` 配置打印机 第 558 页
  - `JumpStart II`: 设置本地或远程打印机 第 560 页
  - 使用 `CUPS` Web 界面 第 565 页
  - 配置打印机 第 566 页
- 管理用户打印队列
  - 管理打印队列 第 572 页
- 排除一般打印问题
  - 添加和删除已配置打印队列中的任务
  - `BSD` 和 `System V` 命令行打印工具 第 574 页

#### 使用的文件、术语和工具部分列表

- `CUPS` 配置文件、工具和实用程序
  - `JumpStart I`: 使用 `system-config-printer` 配置打印机 第 558 页
  - 使用 `CUPS` Web 界面 第 565 页
  - 共享 `CUPS` 打印机 第 572 页
- `/etc/cups`
  - `lpadmin` 命令示例 第 570 页
- `lpd` 旧版接口 (`lp`, `lprm`, `lpq`)
  - 传统 `UNIX` 打印 第 573 页

## 109 网络基础

*参见第 8 章：网络和互联网 第 279 页*

### 109.1 互联网协议基础

*参见网络协议 第 290 页*

- 展示对网络掩码的理解
  - 子网掩码 第 298 页
  - 网络掩码 第 1263 页 (词汇表)
- 了解私有和公共“点分十进制”`IP` 地址之间的区别
  - 私有地址空间 第 637 页
  - 私有地址空间 第 1267 页 (词汇表)
- 设置默认路由
- 了解常见 `TCP` 和 `UDP` 端口的知识（20, 21, 22, 23, 25, 53, 80, 110, 119, 139, 143, 161, 443, 465, 993, 995）
  - 涵盖服务器的每一章都讨论了该服务器使用哪些端口。
  - 端口 第 312 页
  - 端口 第 1266 页 (词汇表)
- 了解 `UDP`、`TCP` 和 `ICMP` 之间的区别及主要特征
  - `UDP` 第 290 页
  - `UDP`: 用户数据报协议 第 292 页
  - `TCP` 第 290 页
  - `TCP`: 传输控制协议 第 291 页
  - `ping`: 测试网络连接 第 305 页
  - `UDP` 第 1278 页 (词汇表)
  - `TCP` 第 1276 页 (词汇表)
  - `ICMP` 第 1254 页 (词汇表)
- 了解 `IPv4` 和 `IPv6` 之间的主要区别
  - `IPv4` 第 292 页
  - `IPv6` 第 293 页

#### 使用的文件、术语和工具部分列表

- `/etc/services`
  - 网络服务 第 313 页
  - `/etc/services` 第 511 页
- `ftp`
  - 第 19 章：`FTP`: 通过网络传输文件 第 713 页
- `telnet`
  - `telnet`: 登录远程系统 第 303 页
- `host`
  - `host` 和 `dig`: 查询互联网名称服务器 第 307 页
- `ping`
  - `ping`: 测试网络连接 第 305 页
- `dig`
  - `host` 和 `dig`: 查询互联网名称服务器 第 307 页
  - `dig` 第 861 页
  - `dig` 第 862 页
- `traceroute`
  - `traceroute`: 跟踪互联网上的路由 第 306 页
- `tracepath`

### 109.2 基本网络配置

- 手动和自动配置网络接口
  - 配置系统 第 636 页
  - `NetworkManager`: 配置网络连接 第 637 页

#### 基本 `TCP/IP` 主机配置

##### 使用的文件、术语和实用工具列表（部分）

- `/etc/hostname`
  - `/etc/hostname` 第 507 页
- `/etc/hosts`
  - 主机名 第 300 页
  - `/etc/hosts` 第 507 页
- `/etc/resolv.conf`
  - `/etc/resolv.conf` 第 510 页
- `/etc/nsswitch.conf`
  - `nsswitch.conf`：优先查找哪个服务 第 495 页
- `ifconfig`
- `ifup`
- `ifdown`
- `route`
- `ping`
  - `ping`：测试网络连接 第 305 页

### 109.3 基本网络故障排除

手动和自动配置网络接口和路由表，包括添加、启动、停止、重启、删除或重新配置网络接口。修改、查看或配置路由表，并手动纠正设置不当的默认路由。调试与网络配置相关的问题。

#### 使用的文件、术语和实用工具列表（部分）

- `ifconfig`
- `ifup`
- `ifdown`
- `route`
- `host`
  - `host` 和 `dig`：查询互联网名称服务器 第 307 页
- `hostname`
  - `hostname`：显示系统名称 第 219 页
  - `/etc/sysconfig/network` 第 511 页
- `dig`
  - `host` 和 `dig`：查询互联网名称服务器 第 307 页
  - `dig` 第 861 页
  - `dig` 第 862 页
- `netstat`
- `ping`
  - `ping`：测试网络连接 第 305 页
- `traceroute`
  - `traceroute`：追踪互联网路由 第 306 页

### 109.4 配置客户端端 `DNS`

参见第 24 章：`DNS/BIND`：跟踪域名和地址 第 851 页

- 演示在本地系统上使用 `DNS`
- `JumpStart I`：设置 `DNS` 缓存 第 866 页
- 修改名称解析的执行顺序
  - 解析器 第 854 页

#### 使用的文件、术语和实用工具列表（部分）

- `/etc/hosts`
  - 主机名 第 300 页
  - `/etc/hosts` 第 507 页
- `/etc/resolv.conf`
  - `/etc/resolv.conf` 第 510 页
- `/etc/nsswitch.conf`
  - `nsswitch.conf`：优先查找哪个服务 第 495 页

# 110 安全

## 110.1 执行安全管理任务

- 审计系统以查找设置了 `suid/sgid` 位的文件
  - 列出 `setuid` 文件 第 458 页
  - 列出 `setgid` 文件 第 459 页
- 设置或更改用户密码和密码老化信息
  - 用户：更改您的账户类型和密码 (`GUI`) 第 112 页
  - `passwd`：更改您的密码 (`CLI`) 第 137 页
  - 修改用户 第 600 页
  - `chage` 第 601 页
- 能够使用 `nmap` 和 `netstat` 来发现系统上的开放端口
- 设置用户登录、进程和内存使用限制
- 基本的 `sudo` 配置和使用
  - 使用 `sudo` 获取 `root` 权限 第 428 页

### 使用的文件、术语和实用工具列表（部分）

- `find`
  - `find`：根据条件查找文件 第 229 页
- `passwd`
  - 用户：更改您的账户类型和密码 (`GUI`) 第 112 页
  - `passwd`：更改您的密码 (`CLI`) 第 137 页
- `lsof`
  - `lsof`：查找打开的文件 第 624 页
- `nmap`
- `chage`
  - `chage` 第 601 页
- `netstat`
- `sudo`
  - 使用 `sudo` 获取 `root` 权限 第 428 页
- `/etc/sudoers`
  - `sudoers`：配置 `sudo` 第 433 页
- `su`
  - 使用 `su` 获取 `root` 权限 第 425 页
- `usermod`
  - `usermod`：修改用户账户 第 601 页
- `ulimit`

## 110.2 设置主机安全

- 了解影子密码及其工作原理
  - `/etc/shadow` 第 511 页
- 关闭未使用的网络服务
  - 配置守护进程（服务） 第 445 页
  - `service` 第 443 页
  - `chkconfig` 和 `service` 第 445 页
  - `system-config-services`：配置服务 第 447 页
- 理解 `TCP` 包装器的角色
  - `TCP Wrappers`：保护服务器 (`hosts.allow` 和 `hosts.deny`) 第 485 页

### 使用的文件、术语和实用工具列表（部分）

- `/etc/nologin`
  - 进入单用户模式 第 454 页
- `/etc/passwd`
  - `/etc/passwd` 第 508 页
- `/etc/shadow`
  - `/etc/shadow` 第 511 页
- `/etc/xinetd.d/*` [已弃用]
- `/etc/xinetd.conf` [已弃用]
- `/etc/inetd.d/*` [已弃用]
- `/etc/inetd.conf` [已弃用]
- `/etc/inittab`
  - `/etc/inittab` 第 508 页
- `/etc/init.d/*`
  - `SysVinit` (`rc`) 脚本：启动和停止系统服务 第 448 页
- `/etc/hosts.allow`
  - `hosts.allow` 和 `hosts.deny` 第 486 页
- `/etc/hosts.deny`
  - `hosts.allow` 和 `hosts.deny` 第 486 页

## 110.3 使用加密保护数据

执行基本的 `OpenSSH 2` 客户端配置和使用

- 配置 `OpenSSH` 客户端 第 690 页
- 运行 `ssh`, `scp`, 和 `sftp` `OpenSSH` 客户端 第 689 页

理解 `OpenSSH 2` 服务器主机密钥的角色

- `OpenSSH` 工作原理 第 687 页
- 授权密钥：自动登录 第 700 页

执行基本的 `GnuPG` 配置和使用

- 教程：使用 `GPG` 保护文件 第 1169 页

理解 `SSH` 端口隧道（包括 `X11` 隧道）

- 隧道/端口转发 第 707 页

### 使用的文件、术语和实用工具列表（部分）

- `ssh`
  - `ssh`：登录远程系统或执行命令 第 693 页
- `ssh-keygen`
  - `ssh-keygen` 第 701 页
- `ssh-agent`
  - `ssh-agent`：保存您的私钥 第 703 页
- `ssh-add`
  - `ssh-add` 第 703 页
- `~/.ssh/id_rsa` 和 `id_rsa.pub`
  - `id_rsa` `id_rsa.pub` 第 689 页
  - `id_rsa` 和 `id_rsa.pub` 第 701 页
- `~/.ssh/id_dsa` 和 `id_dsa.pub`
  - `id_dsa` `id_dsa.pub` 第 689 页
- `/etc/ssh/ssh_host_rsa_key` 和 `ssh_host_rsa_key.pub`
  - `ssh_host_rsa_key`, `ssh_host_rsa_key.pub` 第 688 页
- `/etc/ssh/ssh_host_dsa_key` 和 `ssh_host_dsa_key.pub`
  - `ssh_host_dsa_key`, `ssh_host_dsa_key.pub` 第 688 页
- `~/.ssh/authorized_keys`
  - `authorized_keys` 第 688 页
- `/etc/ssh_known_hosts`
  - `ssh_known_hosts` 第 692 页
- `gpg`
  - `GnuPG/PGP` 第 1160 页
  - 教程：使用 `GPG` 保护文件 第 1169 页
- `~/.gnupg/*`
  - `~/.gnupg` 第 1170 页

# 术语表

所有标记为 `FOLDOC` 的条目均基于《免费在线计算词典》(`foldoc.org`) 中的定义，`Denis Howe` 编辑。经许可使用。

**`10.0.0.0`** *参见第 1267 页的私有地址空间。*

**`172.16.0.0`** *参见第 1267 页的私有地址空间。*

**`192.168.0.0`** *参见第 1267 页的私有地址空间。*

**`802.11`** 由 `IEEE` 开发的用于无线局域网技术的一组规范，包括 `802.11`（1–2 兆位/秒）、`802.11a`（54 兆位/秒）、`802.11b`（11 兆位/秒）和 `802.11g`（54 兆位/秒）。

**绝对路径名** 以根目录（用 `/` 表示）开头的路径名。绝对路径名定位文件时不考虑当前工作目录。

**访问** 在计算机术语中，一个动词，意思是使用、读取或写入。访问文件意味着从文件读取或写入文件。

**访问控制列表** *参见 `ACL`。*

**访问权限** 读取、写入或执行文件的权限。如果您拥有对文件的写入访问权限（通常简称为*写权限*），您可以写入该文件。也称为*访问特权*。

**`ACL`** 访问控制列表。一种执行与文件权限类似功能但控制粒度更细的系统。
