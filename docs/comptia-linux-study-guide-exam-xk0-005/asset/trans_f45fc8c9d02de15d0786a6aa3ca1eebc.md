

## 4.2 根据给定场景，分析并排除网络资源问题。（第 7 章和第 20 章）
- 网络配置问题
- 防火墙问题
- 接口错误
- 带宽限制
- 名称解析问题
- 远程系统测试

## 4.3 根据给定场景，分析并排除中央处理器（CPU）和内存问题。（第 7、20、21 和 24 章）
- 失控进程
- 僵尸进程
- 高 CPU 使用率
- 高平均负载
- 高运行队列
- CPU 时间
- CPU 进程优先级
- 内存耗尽
- 内存不足 (OOM)
- 交换
- 硬件

## 4.4 根据给定场景，分析并排除用户访问和文件权限问题。（第 22 章）
- 用户登录问题
- 用户文件访问问题
- 密码问题
- 权限提升
- 配额问题

## 4.5 根据给定场景，使用 systemd 诊断并解决 Linux 系统的常见问题。（第 6 章）
- 单元文件
- 常见 systemd 问题

## 如何联系出版商
如果您认为本书中存在错误，请向我们提出。在 John Wiley & Sons，我们深知向客户提供准确内容的重要性，但即使竭尽全力，仍可能出现差错。

若要提交可能的勘误信息，请通过电子邮件发送至我们的客户服务团队：wileysupport@wiley.com，邮件主题请设为“Possible Book Errata Submission”。

## 测试
1. 哪个软件包允许 Linux 服务器与 Windows 和 Mac 客户端共享文件夹和打印机？
    - A. Postfix
    - B. Apache
    - C. Samba
    - D. Kerberos
    - E. Docker

2. 哪个软件包允许开发者使用与应用开发时完全相同的环境来部署应用？
    - A. Postfix
    - B. Apache
    - C. Samba
    - D. Kerberos
    - E. Docker

3. 在命令行中输入命令 `cat -n File.txt`。结果是什么？
    - A. 将显示文本文件 `File.txt`。
    - B. 将显示文本文件 `File.txt`，并包含文件中的任何特殊隐藏字符。
    - C. 将显示文本文件 `File.txt`，并包含表示行尾字符的任何特殊符号。
    - D. 将显示文本文件 `File.txt`，并附带行号。
    - E. 将按相反顺序显示文本文件 `File.txt`。

4. 以下哪些是流编辑器？（请选择所有适用项。）
    - A. `vim`
    - B. `sed`
    - C. `awk`
    - D. `gawk`
    - E. `nano`

5. GRUB2 中哪个命令将 /boot 文件夹的位置定义为系统中第一块硬盘的第一个分区？
    - A. `set root=hd(0,1)`
    - B. `set root=hd(1,0)`
    - C. `set root=hd(1,1)`
    - D. `set root=hd(0,0)`
    - E. `set root=first`

6. 如果在系统日志中看到读写错误，应该使用什么工具来修复硬盘的任何坏扇区？
    - A. mount
    - B. umount
    - C. fsck
    - D. dmesg
    - E. mkinitrd

7. init 程序在 Linux 系统上启动后具有一个进程 ID 号。该进程的 ID 号通常是多少？
    - A. 0
    - B. 1
    - C. 2
    - D. 10
    - E. 未知

8. 您需要确定 systemd 系统的默认目标。应该使用以下哪个命令？
    - A. grep initdefault /etc/inittab
    - B. runlevel
    - C. systemctl is-enabled
    - D. systemd get-target
    - E. systemctl get-default

9. Cinnamon 桌面环境使用哪个窗口管理器？
    - A. Mutter
    - B. Muffin
    - C. Nemo
    - D. Dolphin
    - E. LightDM

10. 您的 X11 会话已挂起。使用什么按键组合来重启该会话？
    - A. Ctrl+C
    - B. Ctrl+Z
    - C. Ctrl+Q
    - D. Ctrl+Alt+Delete
    - E. Ctrl+Alt+Backspace

11. Linux 中哪个文件夹包含时区模板文件？
    - A. /etc/timezone
    - B. /etc/localectime
    - C. /usr/share/zoneinfo
    - D. /usr/share/timezone
    - E. /usr/share/localectime

12. 哪个 systemd 命令允许您查看和更改时间、日期以及时区？
    - A. timedatectl
    - B. localectl
    - C. date
    - D. time
    - E. locale

13. 以下哪些文件包含 useradd 命令使用的用户账户创建指令？（请选择所有适用项。）
    - A. /etc/default/useradd 文件
    - B. /etc/useradd 文件
    - C. /etc/adduser.conf 文件
    - D. /etc/login.defs 文件
    - E. /etc/login.def 文件

14. 您需要显示所有采用配额限制的文件系统上的各种配额。应该使用以下哪个命令？
    - A. edquota -t
    - B. quotaon -a
    - C. quotacheck -cu
    - D. quotacheck -cg
    - E. repquota -a

15. 原始设备文件 /dev/sdb1 引用的是哪个磁盘和分区？
    - A. 第二个 SCSI 存储设备上的第一个分区
    - B. 第一个 SCSI 存储设备上的第二个分区
    - C. 第二个 PATA 存储设备上的第一个分区
    - D. 第一个 PATA 存储设备上的第二个分区
    - E. 第二个 SATA 存储设备上的第二个分区

16. 哪个工具可以从多个物理分区创建逻辑卷？
    - A. `mkfs`
    - B. `pvcreate`
    - C. `lvcreate`
    - D. `fdisk`
    - E. `vgcreate`

17. 以下哪些可以作为备份工具使用？（请选择所有适用项。）
    - A. `gzip` 工具
    - B. `zip` 工具
    - C. `tar` 工具
    - D. `rsync` 工具
    - E. `dd` 工具

18. 系统管理员已创建备份存档，并通过网络将该文件传输到另一台系统。哪些工具可用于检查存档文件的完整性？（请选择所有适用项。）
    - A. `rsync` 工具
    - B. `md5sum` 工具
    - C. `sftp` 工具
    - D. `scp` 工具
    - E. `sha512sum` 工具

19. 应该使用哪个工具安装 DEB 软件包文件？
    - A. `dpkg`
    - B. `tar`
    - C. `gcc`
    - D. `rpm`
    - E. `gzip`

20. 使用哪个工具安装 RPM 软件包文件？
    - A. `dpkg`
    - B. `tar`
    - C. `gcc`
    - D. `rpm`
    - E. `gzip`

21. `lsmod` 工具提供与以下哪个其他工具或文件相同的信息？
    - A. `modinfo` 工具
    - B. `/proc/modules` 文件
    - C. `/etc/modules.conf` 文件
    - D. `insmod` 工具
    - E. `/run/modprobe.d/*.conf` 文件

22. 应该使用哪个工具来移除模块及其依赖模块？
    - A. `rmmod` 工具
    - B. `modinfo` 工具
    - C. `cut` 工具
    - D. `depmod` 工具
    - E. `modprobe` 工具

23. 应设置哪个特殊位以防止用户删除他人创建的共享文件？
    - A. SUID
    - B. GUID
    - C. Sticky bit
    - D. 读
    - E. 写

24. 可以使用哪个命令来更改分配给文件的属主？
    - A. `chmod`
    - B. `chown`
    - C. `chage`
    - D. `ulimit`
    - E. `chgrp`

25. 哪个目录包含各种 PAM 配置文件？
    - A. `/etc/pam/` 目录
    - B. `/etc/pam_modules/` 目录
    - C. `/etc/modules/` 目录
    - D. `/etc/pam.d/` 目录
    - E. `/etc/pam_modules.d/` 目录

26. 以下哪些可以覆盖 `~/.ssh/config` 文件中的设置？
    - A. `/etc/ssh/ssh_config` 文件中的设置。
    - B. `ssh` 工具’s 命令行选项。
    - C. 无法覆盖此文件中的设置。
    - D. `/etc/ssh/sshd_config` 文件中的设置。
    - E. `sshd` 守护进程配置文件中的设置。

27. 可以使用哪个命令在日志文件中实时显示新出现的条目？
    - A. `head`
    - B. `tail`
    - C. `tail -f`
    - D. `head -f`
    - E. `vi`

28. 使用哪个命令显示 `systemd-journald` 日志中的条目？
    - A. `journalctl`
    - B. `syslogd`
    - C. `klogd`
    - D. `systemd-journald`
    - E. `vi`

29. `/etc/services` 文件可供防火墙用于什么目的？
    - A. 指定要阻止的远程服务
    - B. 存储其 ACL 规则
    - C. 将服务名称映射到端口和协议
    - D. 确定是否可访问该端口
    - E. 指定哪些本地服务可以发送数据包

30. 关于 `netfilter`，以下哪些说法是正确的？（请选择所有适用项。）
    - A. 它被 firewalld 使用。
    - B. 它被 UFW 使用。
    - C. 它为防火墙技术提供 Linux 内核的代码钩子。
    - D. 它被 `iptables` 使用。
    - E. 它无需其他应用程序即可提供防火墙服务。

31. 以下哪项是特定网络段上可传输的最大数据量的度量？
    - A. 带宽
    - B. 吞吐量
    - C. 饱和度
    - D. 延迟
    - E. 路由

32. 哪个工具允许您查看特定于交换的磁盘 I/O？
    - A. `ipcs -m`
    - B. `cat /proc/meminfo`
    - C. `free`
    - D. `swapon -s`
    - E. `vmstat`

