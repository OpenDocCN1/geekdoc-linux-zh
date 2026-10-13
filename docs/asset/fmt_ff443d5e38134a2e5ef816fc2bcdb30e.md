
## 命令

- `getsebool` 显示 SELinux 布尔值的当前值。
- `iptables` 配置和管理数据包过滤和网络地址转换。
- `restore` 恢复文件上的 SELinux 安全上下文。
- `scp` 安全传输文件。
- `sealert` SELinux 故障排除的客户端接口。
- `semanage` 管理 SELinux 策略的某些元素。
- `setforce` 设置 SELinux 的默认运行模式。
- `setbool` 设置 SELinux 布尔值的新值。
- `sftp` 安全传输文件。
- `ssh` 在远程系统上开启安全登录会话。
- `ssh-add` 将 DSA/RSA 密钥添加到认证代理。
- `ssh-agent` 持有认证私钥的认证代理。
- `ssh-copy-id` 将公钥安装到远程系统的授权密钥。
- `ssh-keygen` 生成、管理和转换用于 `ssh` 的公/私钥。
- `system-config` 用于启用/禁用 `iptables` 防火墙、允许/拒绝安全级服务以及设置 SELinux 运行模式的图形化工具。
- `system-config-selinux` 管理 SELinux 的图形化工具。

### 杂项

- `apropos` 在 `whatis` 数据库中搜索关键词。
- `cal` 显示日历。
- `clear` 清除终端屏幕。
- `date` 显示/设置系统日期/时间。
- `man` 显示手册页。
- `system-config` 配置音频硬件的图形化工具。
- `whatis` 在 `whatis` 数据库中搜索匹配单词的简短描述。

## 附录 D：文件摘要

此表各种配置、启动、日志和其他重要 RHEL 文件的列表及其简短描述。

### 硬件与设备

|  |  |
| --- | --- |
| `/etc/modprobe.conf` | 定义系统启动时加载的可选模块。 |
| `/etc/rc.d/init.d/haldaemon` | HAL 启动/停止脚本。 |
| `/etc/udev/` | 存储 udev 文件。 |
| `/etc/udev/rules.d` | 存储应用于添加或删除设备的 udev 规则。 |
| `/etc/udev/udev.conf` | udev 配置文件。 |
| `/proc/cpuinfo` | 维护运行时 CPU 信息。 |
| `/proc/filesystems` | 维护支持的文件系统的运行时列表。 |
| `/proc/ide` | 维护 IDE 设备的运行时信息。 |
| `/proc/interrupts` | 维护关于 IRQ 的运行时信息。 |
| `/proc/iomem` | 维护运行时内存信息。 |
| `/proc/ioports` | 维护运行时 I/O 端口。 |
| `/proc/mdstat` | 维护关于 RAID 的运行时信息。 |
| `/proc/modules` | 维护已加载模块列表。 |
| `/proc/mounts` | 维护已挂载文件系统。 |
| `/proc/partitions` | 维护关于分区信息。 |
| `/proc/scsi/` | 维护关于 SCSI 设备的信息。 |
| `/proc/stat` | 维护运行时统计信息。 |
| `/proc/swaps` | 维护关于交换区的信息。 |
| `/proc/sys/` | 维护内核参数。 |
| `/proc/uptime` | 维护系统运行时间。 |
| `/proc/vmstat` | 维护虚拟内存。 |
| `/var/log/dmesg` | 诊断日志。 |
| `/var/run/haldaemon.pid` | 包含 PID。 |

### X 窗口与桌面

|  |  |
| --- | --- |
| `/etc/sysconfig/desktop` | 定义系统默认显示。 |
| `/etc/X11/` | 存储 X 相关文件。 |
| `/etc/X11/prefd` | 首选显示。 |
| `/etc/X11/xinit/` | 存储启动文件。 |
| `/etc/X11/xorg.conf` | X 服务器的主配置文件。 |
| `/var/run/xfs.pid` | 字体。 |

### 软件包

- `/etc/yum.conf` | yum 的默认配置。
- `/etc/yum.repos.d/` | 定义软件仓库。

### 用户与组

- `~/.bash_logout` 在注销前执行命令的文件。
- `~/.bash_profile` | 设置环境变量的用户初始化文件。
- `~/.bashrc` | 定义函数和别名的用户初始化文件。
- `/etc/bashrc` | 定义函数和别名的系统级初始化文件。
- `/etc/group` | 维护组数据库。
- `/etc/gshadow` | 包含组密码信息。
- `/etc/login.defs` | 包含 `/etc/default/useradd` 中定义的默认值。
- `/etc/passwd` | 维护用户数据库。
- `/etc/profile` | 设置环境变量的系统级初始化文件。
- `/etc/profile.d/` | `/etc/profile` 调用的脚本。
- `/etc/shadow` | 用户密码和年龄信息。
- `/etc/skel/` | 创建时复制到主目录的模板。
- `/var/log/btmp` | 维护失败登录历史。
- `/var/log/faillog` | 维护更详细的失败登录历史。
- `/var/log/wtmp` | 维护成功登录历史。

### 磁盘分区

- `/etc/lvm/backup`

### 文件系统、配额与交换

- `*/lost+found/` | 存在每个文件系统中，用于存放丢失的文件。
- `/etc/fstab` | 包含每次启动时自动挂载的文件系统和交换分区。
- `/etc/mtab` | 列出当前挂载的文件系统。

### 关机与启动

- `/boot/grub/grub.conf` | 包含启动信息。
- `/etc/inittab` | `init` 命令使用的初始化表。
- `/etc/issue` | 用户登录时打印此文件的内容。
- `/etc/motd` | 今日破语。
- `/etc/rc.d/init.d/` | 存储启动和关机脚本。
- `/etc/sysconfig/` | 存储服务的初始化配置。
- `/mnt/sysimage` | 救援模式下创建的挂载文件系统的虚拟文件系统。

### 内核

- `/etc/sysctl.conf` | 存储自定义内核参数。
- `/lib/modules` | 存储内核模块。
- `/usr/src/` | 用于根据源码构建新内核。

# 文件摘要 675

`/.ssh/`

`/etc/hosts.allow`

存储用户认证/授权信息。

TCP Wrappers 文件，包含允许访问的主机、网络和域条目。

`/etc/hosts.deny`

TCP Wrappers 文件，包含被拒绝访问的主机、网络和域条目。

存储每个 PAM 感知服务的信息。

`/etc/pam.d/`

`/etc/rc/init.d/init.iptables`

`/etc/rc/init.d/sshd`

`/etc/selinux/config`

`/etc/selinux/targeted/context/files/`

`/etc/selinux/targeted/context/users/`

`/etc/setatus.conf`

安全的启动/停止脚本。

文件和目录的 SELinux 配置上下文。

存储用户的 SELinux 安全上下文。

`selinux/`

`/var/log/secure`

`/var/run/sshd`

列出安全上下文的文件和进程。

存储 ssh 配置信息。

持有系统级 ssh 客户端配置。

持有系统级 ssh 服务器配置。

包含基础 IPTables 防火墙配置。

存储当前的 SELinux 配置。

捕获安全相关信息。

包含 `sshd` 的 PID。

# 杂

`/etc/rc/init.d/rhnsd`

`/etc/sysconfig/rhnsd`

RHN 启动/停止脚本。

包含基础 RHN 配置。

## 附录 E：系统守护进程摘要

此表列出了几个关键守护进程及其简介。这些进程对于服务的正常运行至关重要。

| 硬件与设备 | 描述 |
| :--- | :--- |
| `halt` | 跟踪已连接设备。 |
| `udevd` | 从内核接收设备添加和删除信息并传递给 udev 处理。 |
| 文件系统、配额和交换分区 |  |
| `kswapd` | 处理内核分页服务。 |
| 关机与启动 |  |
| `init` | 主初始化进程。 |
| 打印服务 |  |
| `cupsd` | 打印调度守护进程。 |
| 作业调度和系统日志 |  |
| `atd` | 执行队列作业。 |
| `crond` | 执行计划 cron 作业。 |
| `klogd` | 记录内核消息。 |
| `syslog` | 记录系统消息。 |
| DNS 和 DHCP |  |
| `dhcpd` | DHCP 服务器守护进程。 |
| `named` | DNS 服务器守护进程。 |
| NIS 和 LDAP |  |
