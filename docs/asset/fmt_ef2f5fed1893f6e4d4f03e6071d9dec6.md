
# 练习

- 练习 16：仅为本地网络配置 `sendmail` 服务，使从 `user2` 到 `user4` 的邮件、域名 `example.net` 的邮件到达 `user3`，任何发送给 `admin` 的邮件发送到 `user1`。
- 练习 17：拦截来自 `example.net` 的所有邮件。
- 练习 18：在端口 `8090` 上配置 `Squid`，允许本地网络用户访问。
- 练习 19：启用 `pop3s` 和 `maps` 协议，允许本地网络用户访问，拦截所有来自 `example.net` 和 `example.org` 的邮件。
- 练习 20：配置使 `user2` 能够使用 `imaps` 访问邮件。
- 练习 21：配置 `sendmail`，使所有邮件通过 `smtp.example.com` 发送并显示来自 `example.com`。所有发送 `info@example.com` 的邮件由 `admin@example.com` 接收。
- 练习 22：配置缓存 `DNS`。
- 练习 23：配置 `iptables` 防火墙，允许 `example.com` 入站 `ftp` 和 `ssh` 流量，丢弃 `example.net` 的流量并拒绝 `example.org` 的流量。
- 练习 24：为 `iptables` 添加一个名为 `new_chain` 的新链，分别允许 `eth0` 和 `eth1` 接口上的 `ftp` 和 `ssh` 流量。
- 练习 25：配置 `NTP` 客户端。
- 练习 26：配置 `AutoFS` 挂载系统用于。

## 附录 C：命令摘要

| 命令 | 说明 |
| :--- | :--- |
| `cat` | 显示文件内容。 |
| `cd` | 切换目录。 |
| `cp` | 复制文件/目录。 |
| `diff` | 比较文件。 |
| `file` | 显示文件类型。 |
| `find` | 搜索文件。 |
| `grep` | 匹配文本。 |
| `head` | 显示文件开头。 |
| `ls` | 列出文件/目录。 |
| `mkdir` | 创建目录。 |
| `more/less` | 分页显示文件。 |
| `mv` | 移动并重命名文件/目录。 |
| `nano` | 文本编辑器。 |
| `pwd` | 显示当前目录完整路径。 |
| `rm` | 删除文件/目录。 |
| `rmdir` | 删除空目录。 |
| `setfacl` | 设置文件访问列表。 |
| `sort` | 排序。 |
| `stat` | 显示文件系统信息。 |
| `touch` | 创建空文件或更新时间。 |
| `vi` | 文本编辑器。 |
| `view` | 查看文件。 |
| `vim` | 增强版的 `vi`。 |
| `wc` | 统计行数、字符和字节数。 |
| `whereis` | 显示程序路径及其帮助页。 |
| `which` | 显示程序的完整路径。 |

## Shell、脚本与变量

- `alias`/`unalias`: 设置/取消别名。
- `awk`: 一种编程语言。
- `cut`: 提取选择列。
- `echo`: 显示变量值和参数。
- `env`: 显示或修改环境变量。
- `exit`: 退出进程或 shell。
- `export`: 将变量设为全局变量。
- `history`: 显示以前执行过的命令。
- `pr`: 将文件打印到终端。
- `read`: 提示用户输入。
- `sed`: 用于过滤和转换文本的流编辑器。
- `set`: 显示变量。
- `tee`: 将输出发送到两个位置。
- `tr`: 翻译字符。

## 进程与进程监控

- `gnome-system-monitor`: 查看和监控系统进程、内存/交换区的图形化工具。
- `kill`: 向一个或多个进程发送信号。
- `killall`: 杀死所有进程。
- `lsof`: 列出打开的文件。
- `nice`: 以非默认优先级运行一个命令。
- `nohup`: 运行忽略挂起信号的命令。
- `pidof`: 显示运行进程的 PID。
- `pgrep`: 显示进程。
- `pkill`: 向一个或多个进程发送信号。
- `ps`: 显示运行的进程。
- `renice`: 更改运行进程的优先级。
- `top`: 显示运行进程的实时信息。
- `uptime`: 显示系统运行了多久。

## 硬件与设备

- `dmesg`: 并显示系统诊断消息。
- `hal-device`: 管理符合硬件抽象层标准的设备。
- `hal-device-manager`: `hal-device` 命令的图形化版本。
- `hclock`: 显示并设置硬件时。
- `kud`: 探测并配置新或修改的硬件。
- `ishal`: 列出硬件抽象层的所有设备。
- `ispci`: 列出 PCI 设备。
- `issub`: 列出 USB 设备。
- `pccardctl`: 控制 PCMC 卡。
- `udevcontrol`: 管理硬件设备事件。
- `udevinfo`: 显示硬件设备信息。
- `udevmonitor`: 显示硬件设备事件。
- `udevtest`: 模拟 `udev` 执行。
- `tty`: 显示终端会话的完整设备路径。
- `cdrecord` 刻录 CD/DVD。
- `eject` 弹出可移动式介质。
- `ksvalidator` 验证 Kickstart 配置文件的语法。
- `mkbootdisk` 创建独立的启动介质。
- `rhn_check` 检查并执行 Red Hat Network 上的队列任务。
- `rhn_register` 在 Red Hat Network 上注册系统。
- `system-config-kickstart` 用于构建和修改 Kickstart 配置文件的图形化工具。

## X 窗口与桌面管理器

- `X` 启动服务器。
- `startx` 启动 X 窗口会话。
- `switchdesk` 切换到另一个桌面环境。
- `system-config-display` 配置视频硬件的图形化工具。
- `xterm` X 的终端模拟器。

## 软件包

- `rpm` 执行 `rpm` 软件包管理任务。
- `rpm2cpio` 从 `rpm` 软件包中提取 `cpio` 归档。
- `rpmbuild` 编译一个 `rpm` 包。
- `rpmquery` 查询 `rpm` 包。
- `rpmverify` 验证 `rpm` 包的完整性。
- `rput` 安装和移除 `rpm` 包的图形化工具。
- `pup` 更新 `rpm` 包的图形化工具。
- `system-config-packages` 列出、搜索、安装和移除 `rpm` 包的图形化工具。
- `yum` 灵活地执行软件包管理任务。

## 用户与组

- `chage` 修改用户密码的过期信息。
- `chfn` 修改 `finger` 命令使用的用户信息。
- `chgrp` 更改文件/目录的组成员关系。
- `chmod` 更改文件/目录的权限。
- `chown` 更改文件/目录的所有者（及组成员关系）。
- `chsh` 永久更改用户的登录 shell。
- `faillog` 显示失败记录并设置登录失败限制。
- `grouppass` 管理 `/etc/group` 文件。
- `groupadd` 创建组账户。
- `groupdel` 删除组账户。
- `groupmod` 修改组账户。
- `groups` 显示用户的次要组成员关系。
- `grpck` 检查 `/etc/group` 的一致性。
- `grpunv` 转换为阴影组（shadow groups）机制。
- `grpunconv` 从阴影机制中还原。
- `id` 显示用户的身份信息。
- `last` 显示用户成功登录的历史记录。
- `lastb` 显示用户登录失败的记录记录。
- `lastlog` 显示最近的登录尝试。
- `logname` 显示用户的登录名。
- `newgrp` 临时切换到新组。
- `passwd` 更改用户密码。

## 命令摘要

- `pwck` | 检查 `/etc/passwd` 的一致性。
- `pwconv` | 转换为阴影密码机制。
- `pwunconv` | 从阴影密码机制中还原。
- `su` | 切换到不同的用户。
- `umask` | 显示或设置文件掩码。
- `useradd` | 创建新用户账户。
- `userdel` | 删除用户账户。
- `usmod` | 修改用户账户。
- `users` | 显示当前登录的用户列表。
- `sudo` | 以其他用户的身份执行命令。
- `tmpdump` | 显示 `utmp`, `wtmp` 文件的内容。
- `vigr` | 在 `vi` 中打开 `/etc/shadow` 文件并锁定。
- `vipw` | 在 `vi` 中打开 `/etc/passwd` 文件并锁定。
- `w` | 显示当前谁正在登录、正在做什么以及系统运行了多久。
- `wall` | 向全系统广播消息。
- `who` | 显示当前登录的用户列表。
- `whoami` | 显示有效用户名。
- `system-config-users` | 管理用户和组账户的图形化工具。

## 磁盘分区

- `fdisk` | 磁盘分区管理工具。
- `lcreate`/`lvremove` | 创建/移除逻辑卷。
- `lvdplay` | 显示逻辑卷的信息。
- `lveend`/`lvreduce` | 扩展/缩小逻辑卷的大小。
- `lvname` | 重命名逻辑卷。
- `lresize` | 调整逻辑卷的大小。
- `lvs` | 显示基础逻辑卷信息。
- `mdadm` | 管理软件 RAID 设备。
- `knod` | 创建设备文件。
- `parted` | 另一种磁盘分区管理工具。
