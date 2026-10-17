
`lilo` 的 `-r` 选项可用于更改感知的根目录。

运行级别用于给 Linux 系统提供多种配置。

使用运行级别 0 到 6。

Red Hat 使用运行级别 3 表示文本模式，运行级别 6 表示图形界面模式。

Debian 使用运行级别 2 表示文本和图形界面模式。

运行级别 0 停止系统，1 用于单用户模式，6 重新启动系统。

#### 关键要点

- `init` 和 `telinit` 工具用于更改运行级别。
- `halt`、`poweroff` 和 `reboot` 是用于控制系统启动的工具。
- Linux 内核启动 `init` 进程，该进程的 `PID` 始终为 1。
- `init` 启动其他若干进程，这些进程在 `/etc/inittab` 中配置。
- Red Hat、其变种以及 Debian 使用 Sys V 启动。
- Slackware 使用 BSD 风格的启动。
- 单个脚本文件存储在 `init.d` 目录中。
- Red Hat 中执行的首个脚本是 `rc.sysinit`，而 Debian 中是 `rcS`。
- 可以使用 `chkconfig` 和 `ntsysv` 来更改不同运行级别中启动的服务。
- LILO 提供许多预定义的错误代码，在启动时出现问题时显示。
- 要在单用户模式下启动，请在 LILO 提示符处向启动脚本传递 `S`。
- 要在紧急模式下启动，请在 LILO 提示符处向 `init` 传递 `emergency`。
- 使用 `mkbootdisk` 和 `mkboot` 命令创建启动磁盘。
- 大多数发行版提供修复和救援磁盘，用于根分区损坏无法启动的情况。

#### 学习指南

以下问题和练习将使你能够复习本章涵盖的信息。完成本章的这一部分时请花点时间，仔细审查你可能有的任何问题。仅仅正确回答问题并不如理解答案重要，因此请复习你仍不确定的任何材料。熟悉这里提出的问题及答案将有助于你更好地准备认证考试问题。

##### 评估问题

1. `lilo.conf` 中的哪个条目限制用户在无密码的情况下添加启动参数？
    - A. `lock`
    - B. `restricted`
    - C. `noparams`
    - D. `password`

2. 如果 Linux 是计算机上唯一的操作系统，你应该告诉 LILO 将引导信息放在哪里？
    - A. MBR
    - B. 分区引导块
    - C. 软盘
    - D. BIOS

3. 你要使用哪个启动参数来挂载不同的根文件系统？
    - A. `root=/mnt/`
    - B. `root=/dev/hdal`
    - C. `root=/dev/hdal`
    - D. `root=/dev/hda`

4. `lilo.conf` 中的哪个条目为引导映像提供第二个名称？
    - A. `alias`
    - B. `label`
    - C. `name`
    - D. `tag`

5. 哪个命令将 Red Hat 系统更改为 GUI 登录模式？
    - A. `startx`
    - B. `runlevel 5`
    - C. `init 3`
    - D. `telinit 5`

6. 要立即使用 `shutdown` 命令重新启动系统，你会输入命令 _______________。

7. `reboot` 和 `poweroff` 命令实际上是指向 ____________ 的符号链接。

8. 要更改系统启动到的运行级别，你会更改 `inittab` 中的哪一行？
    - A. `defaultinit`
    - B. `defrunlevel`
    - C. `runlevel`
    - D. `initdefault`

9. 当用户通过 Telnet 登录到系统时，在登录提示符之前会向用户显示 ______ 文件。

10. 哪个命令会列出关于 `inetd` 服务的运行级别信息？
    - A. `chkconfig --list inet`
    - B. `ntsvis --list inet`
    - C. `/etc/rc.d/init.d/inet status`
    - D. `ls -l /etc/rc.d/init.d/inet`

11. 在故障排除配置中，如果旧根卷挂载在 `/mnt/root` 下，你会使用哪个命令？
    - A. `lilo -p /mnt/root`
    - B. `lilo -r /mnt/root/boot`
    - C. `lilo -r /mnt/root`
    - D. `lilo -p /mnt/root/boot`

12. 要在不运行任何启动脚本的情况下启动系统，你会使用启动参数 _______。

13. 要在第二个软盘驱动器上创建启动磁盘而不提示用户，你会使用哪个命令？
    - A. `mkbootdisk --device /dev/fd1 --noprompt`
    - B. `mkboot --device /dev/fd1 --noprompt`
    - C. `mkbootdisk --device /dev/fd0`
    - D. `mkboot --device /dev/fd0`

14. `lilo.conf` 条目 ______ 用于启用从拥有超过 1024 个柱面的磁盘启动。
    - A. `lba`
    - B. `lba32`
    - C. `bigdisk`
    - D. `linear`

15. 当你重启系统时，它首先更改为运行级别 _。

16. 哪个进程的 PID 始终为 1？
    - A. `init`
    - B. `kernel`
    - C. `sync`
    - D. 第一个加载的驱动程序

17. `inittab` 中的哪个条目告诉 `init` 在继续之前等待请求的进程结束？
    - A. `hold`
    - B. `pause`
    - C. `once`
    - D. `wait`

18. 哪种类型的启动使用少数大型脚本文件？
    - A. UNIX
    - B. BSD
    - C. Sys V
    - D. Red Hat

19. 要查看关于 `inetd` 进程的信息，你会输入 ________ 命令（无路径）。

20. 当 LILO 无法加载引导装载器的第二阶段时，它显示什么？
    - A. `LI`
    - B. `LIL`
    - C. `SECOND STAGE NOT FOUND!`
    - D. `LIL-`

##### 场景

1. 当你正在启动你的 Linux 工作站时，它在启动守护进程时挂起。你可以采取哪些步骤来解决这个问题？

2. 你有一台 Linux 服务器，目前启动进入 X Window 系统。图形界面正在使用系统中所需的资源。你如何修复这个问题？

3. 在编译并安装新内核后，重启时出现内核恐慌。不幸的是，你对新内核如此自信，以至于没有保留旧的内核。你能做什么来修复这个问题？

##### 实验练习

###### 实验 8-1 检查启动服务

许多 Linux 发行版安装并启动你不需要的服务。要检查你的启动服务，请采取以下步骤。

1. 首先通过检查 `/etc/inittab` 文件来查看你的系统默认启动到的运行级别。
