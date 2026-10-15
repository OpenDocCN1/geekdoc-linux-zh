
## 系统基础与网络工具

- 监控 `TCP/IP` 流量的工具
- 访问限制文件的位置和内容
- 配置以太网网络接口的工具
- 管理路由表的工具
- 列出网络状态
- 获取网络配置
- 关于使用的硬件设备信息
- 系统初始化文件及其内容 (`Systemd`, `SysV init`)
- `NetworkManager` 及其的影响
- 使用常用的压缩和存档工具解包源码
- 了解编译的基本知识
- 应用参数到配置脚本
- 了解源码默认存储位置
- 了解包含的目录
- 磁带或其他备份介质的知识
- 执行部分或完整备份
- 通过登录消息与用户通信
- 系统维护问题

## 207.1 基础 DNS 服务器

- `BIND 9.x` 配置文件、术语和工具
- `BIND` 配置中区文件的位置
- 重新加载修改后的配置和区文件
- 了解 `dnsmasq`, `dnssq`, `djbindns` 和作为备用服务器 `PowerDNS`
- `BIND 9` 配置文件、术语和工具
- 从 `DNS` 服务器请求信息的工具
- `BIND` 区文件的布局、内容和文件位置
- 在区文件中添加新主机（包括反向区）的各种方法
- `BIND 9` 配置文件
- 配置 `BIND` 在 `chroot` 环境中运行
- 使用 `forwarders` 语句对 `BIND` 进行拆分配置
- 配置和使用事务签名 (`TSIG`)
- 了解 `DNSSEC` 和基础工具
- 了解 `DANE` 和相关记录

## Apache 与 SSL 配置

- `Apache 2.4` 配置文件、术语和内容
- `Apache` 日志文件配置和内容
- 访问限制方法和文件
- `mod_perl` 和 `PHP` 配置
- 客户端用户身份验证文件和工具
- 最大请求、最小及最大服务器和客户端配置
- `Apache 2.4` 虚拟主机实现（带有或不专用 `IP` 地址）
- 使用 `Apache` 配置文件中的重定向语句自定义文件访问
- `SSL` 配置文件、工具和实用程序
- 为商业 `CA` 生成服务器私钥和 `CSR`
- 生成自签名证书
- 安装密钥和证书（包括中间 `CA`）
- 使用 `SNI` 配置虚拟主机
- 了解虚拟主机和使用 `SSL` 的问题
- `SSL` 使用中的安全问题，禁用不安全的协议和加密算法

## 208.3 实现 Squid 作为缓存代理

- `Squid 3.x` 配置文件、术语和工具
- 访问限制方法
- 客户端用户身份验证方法
- `Squid` 配置文件 `ACL` 的布局和内容

## 208.4 实现 Nginx 作为 Web 服务器和反向代理

- `Nginx`
- 反向代理
- 基础 `Web` 服务器

## Samba 4 配置

- `Samba 4` 文档
- `Samba 4` 配置文件
- `Samba 4` 工具、工具和守护进程
- 在 `Linux` 上挂载 `CIFS` 共享
- 将 `Windows` 用户映射到 `Linux` 用户
- 用户级、共享级和 `AD` 安全

## NFS 配置

- `NFS` 版本 3 配置文件
- `NFS` 工具和工具
- 对特定主机或子网的访问限制
- 服务器和客户端上的挂载选项
- `TCP Wrappers`
- `NFSv4` 概述

## DHCP 与 LDAP

- `DHCP` 配置文件、术语和工具
- 子网和动态分配范围设置
- `DHCP6` 和 `IPv6` 路由器公告
- `PAM` 配置文件、术语和工具
- `passwd` 和 `shadow`
- 使用 `sssd` 进行 `LDAP` 认证
- 用于数据管理和查询的 `LDAP` 工具
- 修改用户密码
- 查询 `LDAP` 目录
- `OpenLDAP`
- 基于目录的配置
- 访问控制
- 区分名 (Distinguished Names)
- 模式 (Schemas) 和网页
- 目录
- 对象 ID、属性和类

## 简介与邮件服务

### 邮件服务

- `postfix` 配置文件
- `postfix` `TLS` 配置
- `SMTP` 协议基础知识
- `sendmail` 和 `exim` 概述
- `Sieve` 功能、语法和操作符
- 使用 `Sieve` 根据发件者、收件者(s)、头部和大小对邮件进行过滤
- `procmail` 概述
- `Dovecot` `IMAP` 和 `POP3` 配置和管理
- `Dovecot` 基础 `TLS` 配置
- `Courier` 概述

### 网络安全与防火墙

- `iptables` 和 `ip6tables` 配置文件、工具和工具
- 管理路由表的命令和工具
- 私有地址范围 (`IPv4`) 以及链路本地地址 (`IPv6`)
- 端口重定向和 `IP` 转发
- 根据源或目的协议、端口和地址允许或拦截 `IP` 包
- 保存并重载过滤配置

### FTP 与 SSH

- `Pure-FTPD` 和 `vsftpd` 配置文件、工具和工具
- `ProFTPD` 概述
- 理解被动与主动 `FTP`
- `OpenSSH` 配置文件、工具和工具
- 超级用户和普通用户的登录限制
- 管理和使用服务器和客户端密钥免登录
- 使用多个主机防止配置更改后连接丢失
- 在服务器上扫描和测试端口的工具和工具
- 以日志或其他来源报告安全告警的位置
- 实现入侵检测系统 (`IDS`) 的工具和工具
- `OpenVAS` 和 `Snort` 概述

## 硬件管理

- `CompTIA Linux+/LPIC-1`
- 启用和禁用集成外设
- 配置带有或带有键盘等外部外设的系统
- 区分不同类型的存储设备
- 确定设备的硬件资源
- 列出硬件信息的工具和工具（例如 `lsusb`, `lspci` 等）
- 操作 `USB` 设备的工具和工具
- 对 `sysfs`, `udev`, `hal`, `dbus` 的概念性理解
- 以下是使用的文件、术语和工具的部分列表：
    - `/sys`
    - `/proc`
    - `/dev`
    - `modprobe`
    - `lsmod`
    - `lspci`
- 在启动时为内核提供常用命令

## 启动与初始化

- 从 `BIOS` 到完成的启动序列
- 理解 `SysVinit` 和 `systemd`
- 对 `Upstart` 的了解
- 在日志文件中检查启动事件
- 以下是使用的文件、术语和工具的部分列表：
    - `dmesg`
    - `BIOS`
    - `bootloader`
    - `kernel`
    - `initramfs`
    - `init`
    - `SysVinit`
    - `system`
- 设置默认运行级别或启动目标
- 在运行级别/启动目标之间切换（包括单用户模式）
- 从命令行关机和重启
- 在切换运行级别/启动目标或主要系统事件之前提醒用户
- 正常终止进程
- 以下是使用的文件、术语和工具的部分列表：
    - `/etc/inittab`
    - `shutdown`
    - `init`
    - `/etc/init.d`
    - `telinit`
    - `system`
    - `systemctl`
    - `/etc/systemd/`
    - `/usr/lib/systemd/`
    - `wall`

## 练习题

A. `/dev/hdx`  
B. `/dev/sataX`  
C. `/dev/sdX`  
D. `/disk/sataX`  

A. `view /proc/irq`  
B. `cat /proc/interrupts`  
C. `cat /dev/irq`  

A. `/dev/hd0`  
B. `/dev/flo0`  
C. `/dev/fd0`  
D. `/dev/sda`  

A. `/udev/`  
B. `/devices/`  
C. `/udev/config`  
D. `/udev`  

A. `modprobe`  
B. `lsmod`  
C. `insmod`  
D. `rmmod`  

A. `usb-list`  
B. `lsusb`  
C. `ls-usb`  
D. `--usb`  

A. `/etc/usb`  
B. `/etc/usb-dev`  
C. `/dev/usb`  
D. `/etc/hotplug/usb`  

8. `GRUB` 配置中提供的启动选项会将系统引导单用户模式？  
A. `single-user`  
B. `su`  
C. `single`  
D. `root`  

A. `Shift`  
B. `E`  
C. `V`  
D. `H`  

10. 使用哪个命令查看内核环缓冲区以诊断启动过程？  
A. `lsboot`  
B. `boot-log`  
C. `krblogger`  
D. `dmesg`  

A. `Runlevel 5`  
B. `Runlevel SU`  
C. `Runlevel 1`  
D. `Runlevel 6`  

A. `/etc/init-d`  
B. `/etc/init`  
C. `/etc/sysV`  
D. `/etc/init.d`  

A. `init 6`  
B. `shutdown -h -t now`  
C. `init 1`  
D. `refresh-system`  

A. `init-refresh`  
B. `init 6`  
C. `telinit`  
D. `reload-inittab`  

A. `show-level`  
B. `init --level`  
C. `sudo init`  
D. `runlevel`  

A. `/etc/system.conf.d`  
B. `/lib/system.conf.d`  
C. `/lib/systemd/system`  
D. `/etc/sysconfd`  

```
lrwxr-xr-x. 1 root 35 Jul 8 2014 .fetchmailrc -> .configs/fetchmail/.fetchmailrc
```

A. 这是一个名为 `.fetchmailrc` 的文件，使用符号链接链接。  
B. 这是一个名为 `.configs/fetchmail/.fetchmailrc` 的文件，所有者为 `lrwxr-xr-x`。  
C. 这是一个名为 `.fetchmailrc` 的目录，所有者为 `Jul`。  
D. 这是一个本地目录 `.configs/fetchmail/.fetchmailrc`。  

A. `systemd list-units`  
B. `systemctl list-units`  
C. `systemd unit-list`  
D. `systemctl show-units`  

A. `-numdev`  
B. `-n`  
C. `-nn`  
D. `-devnum`  

A. `insmod`  
B. `modlist`  
C. `ls --modules`  
D. `lsmod`  

A. `--show-options`  
B. `--list-deps`  
C. `--show-depends`  
D. `--list-all`  

A. `cat`  
B. `wall`  
C. `tee`  
D. `ssh`  

A. 拔掉磁盘。  
B. 检查系统 `BIOS`。  
C. 重启 `Web` 服务器服务。  
D. 运行 `disk-detect` 命令。  

A. `/etc/usbdevices`  
B. `/var/usb`  
C. `/lib/sys/usb`  
D. `/proc/bus/usb`  

A. `rootpartition={hd0,2}`  
B. `root={dev/sda2}`  
C. `root={hd0,3}`  
D. `rootpartition=/dev/sda2`  

A. 按 `ESC` 编辑，按 `Return` 启动  
B. 按 `V` 编辑，按 `Return` 启动  
C. 按 `E` 编辑，按 `B` 启动  
D. 按 `V` 编辑，按 `B` 启动  

A. `ls`  
B. `showPart`  
C. `partitionlist`  
D. `ps`  

A. `/var/log/bootmessages`  
B. `/var/log/mail.info`  
C. `/var/adm/log/boot.info`  
D. `/var/log/dmesg`  

A. `systemctl --ls`  
B. `telinit`  
C. `systemctl status`  
D. `sysctl -a`  

30. 在受 `systemd` 控制的系统上，哪个命令会将系统置于单用户模式？  
A. `systemctl one`  
B. `systemctl isolate resue.`  
C. `systemctl single-user`  
D. `systemctl runlevel one`  

31. 在由 `Upstart` 控制的系统中，哪个命令将重新加载配置文件？  
A. `initctl reload`  
B. `systemd reload`  
C. `upstart --reload`  
D. `ups -reload`  

32. 在 `SysV` 系统上工作时，`chkconfig` 哪个选项显示所有服务及其运行级别？  
A. `--reload`  
B. `--list`  
C. `--all`  
D. `--ls`  

33. 连接到 `USB` 的驱动器被视为哪种类型的设备？  
A. 介质 (`Medium`)  
B. 冷插拔 (`Coldplug`)  
C. 热插拔 (`Hotplug`)  
D. 侧插拔 (`Sideplug`)  

34. 在启动过程中，内核接管初始化过程并初始化设备后，下一步是什么？  
A. 系统 `BIOS` 初始化设备。  
B. 系统被置于多用户模式。  
C. 引导程序初始化内核。  
D. 挂载根分区。  

35. 使用一个旧式 `PATA` 磁盘启动系统。你最近为电脑添加了一个内部 `DVD` 驱器，系统将不再启动。最可能的原因是什么？  
A. `BIOS` 将 `DVD` 驱器识别为第一块磁盘，因此系统无法找到 `Linux` 分区。  
B. 在安装 `DVD` 驱器时，硬盘损坏了。  
C. `BIOS` 中未启用热插拔选项。  
D. 电脑未检测到 `DVD` 驱器，在安装之前需要先在 `BIOS` 和 `Linux` 中启用它。  

36. 系统使用临时闪存 `USB` 磁盘将数据挂载在 `/dev/sda1`。你需要移除该磁盘。以下哪个命令将允许磁盘安全地从系统中移除？  
A. `usstop /dev/sda`  
B. `umount /dev/sda1`  
C. `ummount /dev/sda1`  
D. `dev-eject /dev/sda`  

37. `EFI` 将挂载在哪个分区中？  
A. `/etc`  
B. `/root`  
C. `/sys`  
D. `/boot`  

## 第 1 章 系统架构 (领域 101)

38. 你已向系统连接了一个 `USB` 磁盘并需要查找它的连接情况。以下哪种方法是最好的？  
A. 查看 `/var/log` 的内容  
B. 运行 `dmesg` 并查找系统信息  
C. 重启系统  

39. 以下哪个命令将立即关闭系统？  
A. `shutdown -c`  
B. `halt`  
C. `systemd stop`  
D. `stop`  

40. `systemd` 文件中的哪个选项指示要执行的程序？  
A. `StartProgram`  
B. `ShortCut`  
C. `ExecStart`  
D. `Startup`  

41. `systemd` 上的哪个命令显示默认目标（`target`）？  
A. `systemctl defaults`  
B. `update-rc.d`  
C. `systemctl runlevel`  
D. `systemctl get-default`  

42. `systemctl` 命令的哪个选项可以更改服务以便在启动时运行？  
A. `enable`  
B. `starton`  
C. `loadboot`  
D. `start`  

43. 下哪项最符合 `/proc` 文件系统？  
- `/proc` 包含待处理的文件。  
- `/proc` 包含进程的配置文件。  
- `/proc` 包含当前运行的信息，包括内核。  
- `/proc` 包含邮件和网络等变量数据。  

44. 哪个命令将以树状格式检索计算机上的 `USB` 连接信息？  
- `lsusb -tree`  
- `lsusb --tree`  
- `lsusb -t`  
- `usblist --tree`  

45. 每个总线支持多少个 `SCSI` 设备？  
- 7 到 15  
- 2 到 4  
- 12  
- 4  

46. 即使设备已加载且运行正常，设备驱动程序未出现在 `lsmod` 输出中的原因可能是？  
- 使用 `systemd` 意味着大多数设备不需要驱动。  
- 使用 `initramfs` 意味着默认启用。  
- 系统不需要设备驱动程序。  
- 设备支持直接编译到内核中。  

47. `rmod` 命令的哪个选项将等待模块不再被使用时再卸载？  
- `-test`  
- `-f`  
- `-w`  
- `-unload`  

## 第 2 章 Linux 安装与包管理 (领域 102)

本章涵盖了以下 `CompTIA LINUX+/LPIC-1` 考试目标：

### 102.1 设计磁盘布局

- 将文件系统和交换空间分配到单独分区或磁盘
- 根据系统的预定用途进行定制设计
- 确保 `/boot` 分区符合启动的硬件架构要求
- `LVM` 基本功能的知识
- 以下是所用文件、术语和工具的部分列表：
    - `/(root)` 文件系统
    - `/var` 文件系统
    - `/home` 文件系统
    - `/boot` 文件系统
