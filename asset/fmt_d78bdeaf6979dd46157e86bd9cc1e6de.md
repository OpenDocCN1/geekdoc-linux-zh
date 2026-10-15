
15. 你希望计算机在两年后提醒你检查车辆。在指定的选项中最好的方法是？

- A. 创建一个反复检查时间的程序，两年后显示检查车辆的消息。
- B. 输入 `cal month year`，指定未来的检查日期，让 Linux 在该日期运行你指定的程序。
- C. 创建一个每小时运行一次的 `cron` 任务。该任务检查日期，并在正确的日期时使用 `mail` 通知你检查车辆。
- D. 使用 NTP 日历程序为指定的日期创建一个警报。程序将在指定的日期和时间显示你输入。
- E. 输入 `at date`，其中 `date` 是日期。你可以指定一个命令（如 `mail`）来通知你检查车辆。

16. 你如何配置计算机使用 IP 地址为 `172.24.21.1` 的计算机作为未配置网络流量的网关？

- A. `gateway 172.24.21.1`
- B. `default 172.24.21.1`
- C. `route gateway 172.24.21.1`
- D. `add default gw 172.24.21.1`
- E. `gw 172.24.21.1`

17. 你可以使用什么软件驱动盲文显示设备？（选择两个）

- A. `Emacspeak`
- B. `BRLTTY`
- C. `2.6.26` 或更高内核
- D. `GOK`
- E. `framebuffer` 驱动

18. 关于源码 RPM 包，正确的是？

- A. 它们由三个文件组成：原始源码包、更改补丁文件和指示包真实性的 PGP 签名。
- B. 重新构建它们需要编程知识。
- C. 它们有时用于解决二进制包的依赖问题。
- D. 为基于 RPM 的发行版编译软件是必要的。
- E. 它们始终包含 GPL 许可软件。

19. 你应该单独使用哪个工具将 `pumpkin.txt` 重命名为 `lantern.txt`？

- A. `dd`
- B. `rm`
- C. `cp`
- D. `mv`
- E. `ln`

20. 你想运行一个名为 `simbibang` 的长时间科学模拟程序，它不需要用户交互；程序仅对磁盘文件操作。如果你不想在运行程序时占用 shell，应该输入什么来在后台运行 `simbibang`？

- A. `start simbibang`
- B. `simbibang &`
- C. `bg simbibang`
- D. `background simbibang`
- E. `nice simbibang`

21. 以下哪个命令将在计算机上安装名为 `theprogram-1.2.3-4.i386.rpm` 的 RPM 包文件？（选择两个）

- A. `rpm -Uvh theprogram-1.2.3-4.i386.rpm`
- B. `rpm -i theprogram-1.2.3-4.i386.rpm`
- C. `rpm -e theprogram`
- D. `rpm -e theprogram-1.2.3-4.i386.rpm`
- E. `rpm -Vp theprogram-1.2.3-4.i386.rpm`

# 评估测试

22. 哪个工具可以诊断并修复许多常见的 Linux 文件系统问题？

- A. `mkfs`
- B. `fsck`
- C. `chkdsk`
- D. `scandisk`
- E. `fdisk`

23. 你刚刚安装了 MySQL，并打算用它来存储动物园动物的信息，从食蚁到斑马。一旦启动 MySQL，你可能首先使用哪个命令？

- A. `CREATE DATABASE animals;`
- B. `USE animals;`
- C. `CREATE TABLE animals;`
- D. `INSERT INTO animals;`
- E. `UPDATE animals;`

24. 下列哪个命令在 Linux Shell 中输入时会显示主题帮助信息？（选择两个）

- A. `manual topic`
- B. `man topic`
- C. `? topic`
- D. `info topic`
- E. `hint topic`

25. 计算机的硬件时钟在计算机关机时继续计时。这种时间在 x86 Linux 系统上可能以什么格式存储？（选择两个）

- A. 协调世界时 (UTC)
- B. 互联网时间
- C. 本地时间
- D. 12 小时制
- E. 火星时间

26. 你想知道当前加载了哪些内核模块。你会输入什么命令来这些信息？

- A. `insmod`
- B. `depmod`
- C. `modprobe`
- D. `lsmod`
- E. `modinfo`

27. 你想让 `music` 组的所有成员读取 `instruments.txt` 文件，该文件目前的权限为 `0640` (-rw-r----)，所有者为 `root`，组所有者为 `root`。你可能如何实现这一目标？（选择两个）

- A. 在文件的目录下输入 `chmod music instruments.txt`。
- B. 在文件的目录下输入 `chgrp instruments.txt`。
- C. 在文件的目录下输入 `chroup instruments.txt`。
- D. 在文件的目录下输入 `chmod 0600 instruments.txt`。
- E. 在文件的目录下输入 `clown : instruments.txt`。

28. 你想在另一个位置创建 `/usr/local/bin` 目录的链接。以下哪个是正确的？

- A. 只有当 `/usr/local/bin` 位于日志文件系统上才可以这样做。
- B. 你必须拥有 `/usr/local/bin` 才能创建链接。
- C. 只有当链接的位置与原始目录位于同一个文件系统时，才能创建链接。
- D. 只有系统管理员才能这样做。
- E. 该链接可能是一个符号链接。

29. 下列哪个命令在 Vi 命令模式下输入时会保存文件并退出程序？（选择两个）

- A. `:rq`
- B. `:wq`
- C. `:re`
- D. `:we`
- E. `:zz`

30. 用户的家目录包含一个名为 `~/.forward` 的文件，内容只有一行：`"/junkme"`。此配置的作用是什么？

- A. 用户的收到的邮件被转发到同一系统上的 `junkme` 用户。
- B. 用户的收到的邮件被存储在 `~/junkme` 文件中。
- C. 用户的收到的邮件通过 `~/.junkme` 程序发送。
- D. 用户的收到的邮件被标记为垃圾邮件并删除。
- E. 用户的收到的邮件被转发到 `junkme` 计算机上的同一个用户。

# 评估测试答案

1. B. `"PS/2"` 既可以指硬件接口，也可以指软件协议，但在 Protocol 选项的语境下，它明确指软件协议。因此，选项 B 是正确的。选项 A 可能正确，但指定的行不足以证明这一点；USB 鼠标通常使用 PS/2 协议或其变体，如 Intell PS/2 协议。PS/2 硬件端口和协议在选项 C 中提到，但许多计算机现在不再使用它们了，因此选项 D 是错误的。斜杠（`/`）作为 PS/2 协议名称是无效，因此选项 E 是错误的。更多信息请参见第 6 章“配置窗口系统、本地化和打印”。

2. A. 通过选择进程列表（来自 `ps`）来确定正在运行哪一个是最可靠的方法，选项 A 是正确的。服务器的配置文件（如选项 C 所示）是一个很好的诊断，尽管某些升级过的旧系统都有两套配置。没有标准的 supervisor 来报告运行哪一个，选项 B。大多数发行版通过 SysV 脚本启动服务器；`/etc/init` 文件未参与此过程，检查它是没有意义的，选项 D 是错误的。当以 root 身份输入 `netstat -ap` 时，输出将包含任何连接的指示，选项 E 是错误的。更多信息请参见第 10 章“安全系统”。

3. D. 优先级工具用于启动、停止、更改优先级以及其他控制优先级队列中的作业。CUPS 带有此工具，但与在 Web 界面运行的 LPD 相比，它非常原始。因此，选项 D 是正确的，其余选项必须错误。更多信息请参见第 6 章“配置窗口系统、本地化和打印”。

4. C. `/etc/security/limits.conf` 文件定义了用户的各种限制，包括允许同时登录的数量。因此，选项 C 是正确的。`/etc/pam.d/limits` 文件（选项 A）是虚假的，尽管登录限制依赖可插身份验证系统（PAM）。`/etc/bashrc` 文件（选项 B）是一个全局启动脚本，但 `/etc/init` 文件（选项 D）对登录限制没有直接影响。`/etc/passwd` 文件（选项 E）定义了账户功能，但不包括登录限制。更多信息请参见第 10 章“安全系统”。
