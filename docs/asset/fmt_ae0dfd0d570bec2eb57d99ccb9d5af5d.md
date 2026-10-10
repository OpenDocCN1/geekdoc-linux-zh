
# CompTIA Linux+ 学习指南：考试 XK0-004

购买考试券

立享 9 折扣

内含优惠券！

包含交互式在线学习环境和学习工具：

- 自定义练习题
- 150 张电子抽闪卡
- 可搜索的关键术语词汇表

CHRISTINE BRESNAHAN

RICHARD BLUM

![](img/0c1e7d2699b9d354c8d2f84669d18d73_2_0.png)
![](img/0c1e7d2699b9d354c8d2f84669d18d73_4_0.png)
![](img/0c1e7d2699b9d354c8d2f84669d18d73_6_0.png)

Christine Bresnahan

Richard Blum

## 致谢

首先，所有的荣耀和赞美归于上帝，通过他的儿子耶稣基督使一切成为可能并赐予我们永生的礼物。

非常感谢 Sybex 优秀的团队在该项目中付出的卓越工作。感谢高级策划编辑 Kenya Brown 为我们提供编写这本书的机会。也感谢开发编辑 Stephanie Barton 保持进度并让书籍更具观赏性。感谢 Steph 的所有辛勤和勤勉。技术校对员 Kevin E. Ryan 和 Jason Eckert 在对内容提出建议的同时，对书中所有的工作进行了非常优秀的双重检查。我们还感谢 David B. Clinton 在项目接近尾声时接手技术编辑并提供了极好的建议。我们还感谢年轻有华的 Daniel Anez (theanez.com) 提供的插图工作。我们还感谢 Waterside Productions, Inc. 的 Carole Jelen 为我们安排这次机会，并在我们的写作生涯中提供帮助。

Christine 特别感谢她的丈夫 Timothy 他的鼓励、耐心和愿意倾听，即使当他完全不知道她在说什么时。Christine 还想表达对 Samantha 和 Cameron 的爱，“愿上帝丰盛地祝福你们的婚姻。”

Rich 特别感谢他的妻子 Barbara 在项目期间忍受他的坏脾气，并帮助他保持精神。

## 关于作者

Christine Bresnahan 拥有 CompTIA Linux+, LPIC-1，在IT行业担任系统管理员已 30 多年。她是 Ivy Tech 社区学院的兼职教授，在那里教授 Linux 和 Python 编程课程。她还编写书籍并制作教学资源。

Richard Blum 拥有 CompTIA Linux+, CompTIA Security+, LPIC-1，也曾作为系统和网络管理员工作了 30 多年，并出版了大量关于 Linux 的开源书籍。他是全美大学使用的 Linux 和网络课程的在线讲师。当不是作为一个电脑迷时，Rich 喜欢与妻子 Barbara 以及两个女儿 Katie 和 Jessica 待在一起。

## 目录

- 第 27 章 使用 Git 控制版本 697
- 引言 ... xxix
- 第 1 章 准备你的环境 3
- 复习题 143
- 复习题 437
- 第 19 章 采用最佳安全实践 513
- 像一样运行 687
- 探索容器 727
- 什么是容器？ 727
- 考试要点 731
- 第 29 章 检查云和虚拟化 735
- 探测过程 757
- 第 30 章 编排环境 755

> 新的 Linux+ 考试是 CompTIA 持续教育（CE）考试路线的一部分。新的 Linux+ 考试有效期为三年，但可以通过获得适当数量的教育单元（CEUs）并支付年度费用来续期。

此外，准备一个可用的 Linux 系统进行同步操作也会帮助。许多章节包含一个简单的练习，将引导您完成本章节介绍的基本概念。这为您提供了至关重要的实操经验，帮助您通过考试并在 Linux 世界中取得良好表现。

> CompTIA Linux+ 考试是不依赖特定 Linux 发行版的，无法编写适用于所有 Linux 发行版的练习题。尽管如此，书中的练习假设您已安装了 Ubuntu 18.04 LTS 或 CentOS 7。您可以使用 Oracle VirtualBox 软件（可从 `https://virtualbox.org` 获取）在虚拟环境中安装这其中一个或两个 Linux 发行版。

- 第 25 章“自动化任务”跟进了脚本调度的主题。

我们在书中包含了一些学习工具：

> 注意：访问 `http://www.wiley.com/go/sysextestprep` 进行注册，以获取此交互式在线学习环境和带有学习工具的题库权限。

警告（Warnings）描述了潜在的陷阱或危险。如果你忽视警告，你可能会花费大量时间修复错误，甚至可能需要从头开始恢复整个系统。

侧边栏（Sidebar）类似于注意，但内容较长。侧边栏中的信息是有用的，但不符合正文的主流。

案例研究（Case study）是一种侧边栏类型，它描述了特别贴近现实世界的任务或示例。这可能是我们或我们遇到的人遇到过的情况，也可能是关于如何解决现实 Linux 环境中常见问题的建议。

练习是你应该在自己的计算机上尝试的程序，以帮助你学习章节中的内容。不过，不要局限于书中描述的程序。尝试其他的命令和程序，以真正地学习 Linux。

- 了解如何使用它来绕过问题

## 2.6 给定场景，自动化和调度任务。（第 26 章）

- 理解不同的备份类型以及何时使用每种
- 了解如何查看进程
- 了解如何分配、修改和删除文件和目录权限
- D. Kerberos
- E. Docker

### 练习题

3. 在命令行中输入 `cat -n File.txt` 命令。结果是什么？

- A. 显示文本文件 `File.txt`。
- B. 显示文本文件 `File.txt` 以及文件中的任何特殊隐形成字符。
- C. 显示文本文件 `File.txt` 以及文件中任何表示行结束符的符号。
- D. 显示文本文件 `File.txt` 带有行号。
- E. 反序显示文本文件 `File.txt`。

4. 下列哪些是流编辑器？（选择所有适用项。）

- A. `vim`
- B. `sed`
- C. `awk`
- D. `gawk`
- E. `nano`

5. GRUB2 中的哪个命令定义了 `/boot` 文件夹到系统硬盘上第一个分区的位置？

- A. `set root=hd(0,1)`
- B. `set root=hd(1,0)`
- C. `set root=hd(1,1)`
- D. `set root=hd(0,0)`
- E. `set root=first`

6. 如果你在系统日志中看到或写入错误，应该使用什么工具修复硬盘的任何坏道？

- A. `mount`
- B. `unmount`
- C. `fsck`
- D. `dmesg`
- E. `mkinitrd`

7. `init` 程序在 Linux 系统上启动并有一个进程 ID 数字。该进程的 ID 数字通常是多少？

- A. 0
- B. 1
- C. 2
- D. 10
- E. 未知

8. 你需要确定 `systemd` 系统的默认目标（`target`）。你应该使用以下哪个命令？

- A. `grep initdefault /etc/inittab`
- B. `runlevel`
- C. `systemctl is-enabled`
- D. `systemd get-target`
- E. `systemctl get-default`

9. Cinnamon 桌面环境使用哪个窗口管理器？

- A. `Mutter`
- B. `Muffin`
- C. `Nemo`
- D. `Dolphin`
- E. `LightDM`

10. 你的 `X11` 会话挂起了。你使用哪些组合键来重启会话？

- A. `Ctrl+C`
- B. `Ctrl+Z`
- C. `Ctrl+Q`
- D. `Ctrl+Alt+Delete`
- E. `Ctrl+Alt+Backspace`

11. Linux 中哪个文件夹包含时区模板文件？

- A. `/etc/timezone`
- B. `/etc/localtime`
- C. `/usr/share/zoneinfo`
- D. `/usr/share/timezone`
- E. `/usr/share/localtime`

12. 哪个 `systemd` 命令允许你查看和更改时间、日期和时区？

- A. `timedatectl`
- B. `localectl`
- C. `date`
- D. `time`
- E. `locale`

13. 下列哪些文件包含 `useradd` 命令使用的用户账户创建指令？（选择所有适用项。）

- A. `/etc/default/useradd` 文件
- B. `/etc/useradd` 文件
- C. `/etc/adduser.conf` 文件
- D. `/etc/login.defs` 文件
- E. `/etc/login.def` 文件

14. 你需要在所有使用配额限制的文件系统上显示视视化配额。你应该使用以下哪个命令？

- A. `edquota -t`
- B. `quotaon -a`
- C. `quotacheck -cu`
- D. `quotacheck -cg`
- E. `repquota -a`

15. 原始设备文件 `/dev/sdb1` 指向哪个驱动器分区？

- A. 第二个 SCSI 存储设备上的第一个分区
- B. 第一个 SCSI 存储设备上的第二个分区
- C. 第二个 PATA 存储设备上的第一个分区
- D. 第一个 PATA 存储设备上的第二个分区
- E. 第二个 SATA 存储设备上的第二个分区

16. 哪个工具从物理分区创建逻辑卷？

- A. `mkfs`
- B. `pvcreate`
- C. `lvcreate`
- D. `fdisk`
- E. `vgcreate`

17. 下列哪些可以用于防火墙？（选择所有适用项。）

- A. `/etc/`
- B. `/`
- C. `/`
- D. `/`
- E. `/`

18. 系统管理员创建了备份并将其传输到网络。

- A. `rsync`
- B. `md5sum`
- C. `sftp`
- D. `scp`
- E. `sha12sum`

19. 你使用什么工具安装 `.deb` 包？

- A. `dpkg`
- B. `tar`
- C. `gcc`
- D. `rpm`
- E. `gzip`

20. 你使用哪个工具安装 `.rpm` 包？

- A. `dpkg`
- B. `tar`
- C. `gcc`
- D. `rpm`
- E. `gzip`

21. `______` 工具提供了与其他工具相同的信息？

- A. `modinfo`
- B. `/proc/modules`
- C. `/etc/modules`
- D. `insmod`
- E. `/modprobe.conf`

22. 使用哪个工具移除带有依赖项的模块？

- A. `rmod`
- B. `modinfo`
- C. `cut`
- D. `depmod`
- E. `modprobe`

23. 设置哪个特殊位以防止用户删除共享文件？

- A. `SUID`
- B. `GUID`
- C. `Sticky bit`
- D. `Read`
- E. `Write`

24. 你使用哪个命令更改文件的所有者？

- A. `chmod`
- B. `chown`
- C. `chage`
- D. `ulimit`
- E. `chgrp`

25. `______` 目录包含各种配置文件。

- A. `/etc/pam/`
- B. `/etc/pam_modules/`
- C. `/etc/modules/`
- D. `/etc/pam.d/`
- E. `/etc/pam_modules.d/`

26. 下列哪些可以覆盖 `.ssh/config` 中的设置？

- A. `/etc/ssh/config`
- B. `ssh` 工具的选项
- C. 无法在该文件中覆盖
- D. `/etc/ssh/sshd_config`
- E. `sshd` 守护进程配置

27. 你使用什么命令实时显示日志文件中的条目？

- A. `head`
- B. `tail`
- C. `tail -f`
- D. `head -f`
- E. `vi`

28. 你使用什么命令显示 `systemd-journal` 中的条目？

- A. `journalctl`
- B. `syslogd`
- C. `klogd`
- D. `systemd-journal`
- E. `vi`

29. `/etc/services` 文件可能被防火墙用于什么目的？

- A. 指定阻塞哪些服务
- B. 存储它们的 ACL 规则
- C. 将服务名称映射到端口和协议
- D. 判断端口是否可以访问
- E. 指定哪些本地服务可以发送

30. 关于 `netfilter`，下列哪些正确的？（选择所有适用项。）

- A. 它被防火墙使用
- B. 它被 `UFW` 使用。
- C. 它为防火墙技术提供了内核代码钩子。
- D. 它被 `iptables` 使用。
- E. 它不需要其他应用程序即可提供防火墙服务。

31. 下列哪个是对特定网络段最大传输数据量的测量？

- A. 带宽（Bandwidth）
- B. 吞吐量（Throughput）
- C. 饱和度（Saturation）
- D. 延迟（Latency）
- E. 路由（Routing）

32. 哪个工具允许你查看特定交换特定的磁盘 I/O？

- A. `ipcs -m`
- B. `cat /proc/meminfo`
- C. `free`
- D. `swapon -s`
- E. `vmstat`

33. 哪条命令行命令允许你查看当前 Linux 系统上运行的应用程序？

- A. `lsof`
- B. `kill`
- C. `ps`
- D. `w`
- E. `nice`

34. 哪些命令行命令允许你向正在运行的应用程序发送进程信号？（选择两项。）

- A. `renice`
- B. `pkill`
- C. `nice`
- D. `kill`
- E. `pgrep`

35. Annika 将 `line PS1="My Prompt: "` 这一行放入她账户的 `$HOME/.bash_profile` 文件中。此设置在她下次登录系统时会更改她的提示符。然而，当她启动子 shell（`subshell`）时，该设置没有正常工作。Annika 需要做什么来修复这个问题？

- A. 将该文件行添加到 `$HOME/.profile` 文件中。
- B. 无需。用户的提示符无法在子 shell 中更改。
- C. 在文件的同一行为 `PS1` 添加 `export`。
- D. 将她的默认 shell 更改为 `/bin/dash` 以使此生效。
- E. 将她的密码记录中的最后一个字段更改为 `/sbin/false`。

36. 一个用户不是特定目录的所有者也不是组成员，尝试对该目录使用 `ls` 命令，并获得了权限错误。这意味着什么？

- A. 该目录没有为其他权限设置显示 (`d`)。
- B. 该目录没有为其他权限设置执行 (`x`)。
- C. 该目录没有为其他权限设置写入 (`w`)。
- D. 该目录没有为其他权限设置列出 (`l`)。
- E. 该目录没有为其他权限设置读取 (`r`)。

37. 7. 哪些目录包含显示内核和系统信息的动态文件？（选择两项。）

- A. `/dev`
- B. `/proc`
- C. `/etc`
- D. `/sys`
- E. `/dev/mapper`

38. 哪个目录包含 Linux 中 `X Windows` 系统的配置信息？

- A. `/dev`
- B. `/proc`
- C. `/etc/X11`
- D. `/sys`
- E. `/proc/interrupts`

39. 你如何修复“挂载点不存在”的问题？

- A. 使用 `fsck` 工具修复坏磁盘扇区。
- B. 使用 `badblocks` 工具修复坏磁盘扇区。
- C. 如果需要，使用超级用户权限，并通过 `vgchange` 命令创建目录。
- D. 如果需要，使用超级用户权限，并通过 `mkdir` 命令创建目录。
- E. 如果需要，使用超级用户权限，并通过 `mountpoint` 命令创建目录。

40. Peter 正在完成他的网络应用程序 `Spider`，但在访问远程服务器文件时遇到了问题，目前没有发生网络问题。他认为这与远程服务器的 ACL 过于严格有关。你需要调查这个问题。你可能使用哪些项来排排除此问题？（选择所有适用项）。

- A. `firewall-cmd` 命令
- B. `ufw` 命令
- C. `iptables` 命令
- D. `getacl` 命令
- E. `setacl` 命令

41. 哪种 Bash 脚本命令允许你遍历一系列数据直到数据完成？

- A. `if`
- B. `case`
- C. `for`
- D. `exit`
- E. `$()`

42. 哪个环境变量允许你获取运行 shell 脚本的用户账户的数值用户 ID 值？

- A. `$USER`
- B. `$BASH`
- C. `$UID`
- D. `$HOME`
- E. `$1`

53. 你应该将控制台和终端文件名放入哪个文件中，以防止用户从这些位置以 `root` 用户账户身份登录 Linux 系统？

- A. `/etc/cron.deny`
- B. `/etc/hosts.deny`
- C. `/etc/securetty`
- D. `/etc/login.warn`
- E. `/etc/motd`

54. 哪个 Linux 程序记录用户文件和目录的访问？

- A. `chroot`
- B. `LUKS`
- C. `auditd`
- D. `klistd`
- E. `kinit`

55. 你已将当前工作目录移动到 Linux 虚拟目录结构中的新位置，需要返回之前所在的目录。你应该使用哪条命令？

- A. `cd`
- B. `exit`
- C. `cd ~`
- D. `cd -`
- E. `return`

56. 使用 `cp` 命令复制目录时需要使用哪个选项？

- A. `-i`
- B. `-R`
- C. `-v`
- D. `-u`
- E. `-f`
