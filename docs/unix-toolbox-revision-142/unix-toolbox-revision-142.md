
# Unix 工具箱 修订版 14.2

本文档收集了对 IT 工作或高级用户有用的 Unix/Linux/BSD 命令和任务。这是一份包含简洁说明的实用指南，但读者应具备相应基础知识。

## 1 系统

硬件 (p2) | 统计 (p2) | 用户 (p3) | 限制 (p3) | 运行级别 (p4) | root 密码 (p5) | 编译内核 (p6) | 修复 grub (p7)

### 运行内核与系统信息

```
# uname -a                  # Get the kernel version (and BSD version)
# lsb_release -a            # Full release info of any LSB distribution
# cat /etc/SuSE-release      # Get SuSE version
# cat /etc/debian_version    # Get Debian version
```

使用 `/etc/DISTR-release`，其中 `DISTR` = `lsb`（Ubuntu、redhat、gentoo、mandrake、sun（Solaris）等）。另请参阅 `/etc/issue`。

```
# uptime                    # Show how long the system has been running + load
# hostname                   # system's host name
# hostname -i                # Display the IP address of the host. (Linux only)
# man hier                   # Description of the file system hierarchy
# last reboot                # Show system reboot history
```

### 1.1 硬件信息

内核检测到的硬件

```
# dmesg                     # Detected hardware and boot messages
# lsdev                     # information about installed hardware
# dd if=/dev/mem bs=1k skip=768 count=256 2>/dev/null | strings -n 8 # Read BIOS
```

#### Linux

```
# cat /proc/cpuinfo         # CPU model
# cat /proc/meminfo         # Hardware memory
# grep MemTotal /proc/meminfo # Display the physical memory
# watch -n1 'cat /proc/interrupts' # Watch changeable interrupts continuously
# free -m                   # Used and free memory (-m for MB)
# cat /proc/devices         # Configured devices
# lspci -tv                 # Show PCI devices
# lsusb -tv                 # Show USB devices
# lshal                     # Show a list of all devices with their properties
# dmidecode                 # Show DMI/SMBIOS: hw info from the BIOS
```

#### FreeBSD

```
# sysctl hw.model          # CPU model
# sysctl hw                 # Gives a lot of hardware information
# sysctl hw.ncpu            # number of active CPUs installed
# sysctl vm                 # Memory usage
# sysctl hw.realmem         # Hardware memory
# sysctl -a | grep mem      # Kernel memory settings and info
# sysctl dev                # Configured devices
# pciconf -l -cv            # Show PCI devices
# usbdevs -v                # Show USB devices
# ataconf list              # Show ATA devices
# camcontrol devlist -v     # Show SCSI devices
```

### 1.2 负载、统计与消息

以下命令有助于了解系统当前状态。

```
# top                      # display and update the top cpu processes
# mpstat 1                 # display processors related statistics
# vmstat 2                 # display virtual memory statistics
# iostat 2                 # display I/O statistics (2 s intervals)
# systat -vmstat 1         # BSD summary of system statistics (1 s intervals)
# systat -tcp 1            # BSD tcp connections (try also -ip)
```

# — 系统 —

```
# systat -netstat 1          # BSD active network connections
# systat -ifstat 1           # BSD network traffic through active interfaces
# systat -iostat 1            # BSD CPU and disk throughput
# tail -n 500 /var/log/messages   # Last 500 kernel/syslog messages
# tail /var/log/warn            # System warnings messages see syslog.conf
```

## 1.3 用户



```
# id                         # Show the active user id with login and group
# last                       # Show last logins on the system
# who                        # Show who is logged on the system
# groupadd admin             # Add group "admin" and user colin (Linux/Solaris)
# useradd -c "Colin Barschel" -g admin -m colin
# usermod -a -G <group> <user>   # Add existing user to group (Debian)
# groupmod -A <user> <group>    # Add existing user to group (SuSE)
# userdel colin               # Delete user colin (Linux/Solaris)
# adduser joe                 # FreeBSD add user joe (interactive)
# rmuser joe                  # FreeBSD delete user joe (interactive)
# pw groupadd admin           # Use pw on FreeBSD
# pw groupmod admin -m newmember   # Add a new member to a group
# pw useradd colin -c "Colin Barschel" -g admin -m -s /bin/tcsh
# pw userdel colin; pw groupdel admin
```

加密密码存储在 Linux 和 Solaris 的 `/etc/shadow` 中，在 FreeBSD 上存储在 `/etc/master.passwd` 中。如果 `master.passwd` 被手动修改（例如删除密码），运行 `# pwd_mkdb -p master.passwd` 来重建数据库。

要暂时禁止全系统登录（除 root 外的所有用户）请使用 `nologin`。`nologin` 中的消息将被显示（可能不适用于 ssh 预共享密钥）。

```
# echo "Sorry no login now" > /etc/nologin      # (Linux)
# echo "Sorry no login now" > /var/run/nologin   # (FreeBSD)
```

## 1.4 限制

某些应用程序需要更高的打开文件和套接字限制（如代理 Web 服务器、数据库）。默认限制通常太低。

### Linux

#### 每 shell/脚本

shell 限制由 `ulimit` 控制。状态通过 `ulimit -a` 检查。例如将打开文件限制从 1024 改为 10240：

```
# ulimit -n 10240              # This is only valid within the shell
```

`ulimit` 命令可在脚本中使用，仅更改该脚本的限制。

#### 每用户/进程

登录用户和应用程序可在 `/etc/security/limits.conf` 中配置。例如：

```
# cat /etc/security/limits.conf
*    hard nproc 250            # Limit user processes
asterisk hard nofile 409600   # Limit application open files
```

#### 全系统

内核限制使用 `sysctl` 设置。永久限制设置在 `/etc/sysctl.conf` 中。

```
# sysctl -a                    # View all system limits
# sysctl fs.file-max            # View max open files limit
# sysctl fs.file-max=102400     # Change max open files limit
# echo "1024 50000" > /proc/sys/net/ipv4/ip_local_port_range  # port range
# cat /etc/sysctl.conf
```

```
fs.file-max=102400        # Permanent entry in sysctl.conf
# cat /proc/sys/fs/file-nr   # How many file descriptors are in use
```

### FreeBSD

#### 每 shell/脚本

在 `csh` 或 `tcsh` 中使用 `limits` 命令，或在 `sh` 或 `bash` shell 中像 Linux 一样使用 `ulimit`。

#### 每用户/进程

登录时的默认限制设置在 `/etc/login.conf` 中。无限值仍受系统最大值限制。

#### 全系统

内核限制也使用 `sysctl` 设置。永久限制设置在 `/etc/sysctl.conf` 或 `/boot/loader.conf` 中。语法与 Linux 相同但键不同。

```
# sysctl -a                 # View all system limits
# sysctl kern.maxfiles=XXXX # maximum number of file descriptors
kern.ipc.nmbclusters=32768  # Permanent entry in /etc/sysctl.conf
kern.maxfiles=65536         # Typical values for Squid
kern.maxfilesperproc=32768
kern.ipc.somaxconn=8192     # TCP queue. Better for apache/sendmail
# sysctl kern.openfiles     # How many file descriptors are in use
# sysctl kern.ipc.numopensockets # How many open sockets are in use
# sysctl net.inet.ip.portrange.last=50000 # Default is 1024-5000
# netstat -m                # network memory buffers statistics
```

参见 The FreeBSD handbook Chapter 11¹ 了解详情。

### Solaris

以下 `/etc/system` 中的值将增加每个进程的最大文件描述符：

```
set rlim_fd_max = 4096      # Hard limit on file descriptors for a single proc
set rlim_fd_cur = 1024      # Soft limit on file descriptors for a single proc
```

## 1.5 运行级别

### Linux

启动后，内核启动 `init`，然后启动 `rc`，后者启动属于某个运行级别的所有脚本。脚本存储在 `/etc/init.d` 中，并链接到 `/etc/rc.d/rcN.d`，N 为运行级别编号。

默认运行级别在 `/etc/inittab` 中配置，通常为 3 或 5：

```
# grep default: /etc/inittab
id:3:initdefault:
```

实际运行级别可使用 `init` 更改。例如从 3 切换到 5：

```
# init 5                    # Enters runlevel 5
```

- 0   Shutdown and halt
- 1   Single-User mode (also S)
- 2   Multi-user without network
- 3   Multi-user with network
- 5   Multi-user with X
- 6   Reboot

使用 `chkconfig` 配置在某个运行级别启动时将启动的程序。



```
# chkconfig --list         # List all init scripts
# chkconfig --list sshd    # Report the status of sshd
# chkconfig sshd --level 35 on  # Configure sshd for levels 3 and 5
# chkconfig sshd off       # Disable sshd for all runlevels
```

## 系统

Debian 以及基于 Debian 的发行版（如 Ubuntu 或 Knoppix）使用 `update-rc.d` 命令来管理运行级脚本。默认情况下，系统在运行级 2、3、4 和 5 启动，在运行级 0、1 和 6 关闭。

```
# update-rc.d sshd defaults          # 使用默认运行级激活 sshd
# update-rc.d sshd start 20 2 3 4 5 . stop 20 0 1 6 . # 使用显式参数
# update-rc.d -f sshd remove          # 禁用所有运行级下的 sshd
# shutdown -h now (或 # poweroff)      # 关闭并停止系统
```

### FreeBSD

BSD 的启动方式与 SysV 不同，它没有运行级。最终的启动状态（单用户模式，是否带 X）在 `/etc/ttys` 中配置。所有系统脚本位于 `/etc/rc.d/`，第三方应用程序的脚本位于 `/usr/local/etc/rc.d/`。服务的激活在 `/etc/rc.conf` 和 `/etc/rc.conf.local` 中配置。默认行为在 `/etc/defaults/rc.conf` 中配置。这些脚本至少响应 `start|stop|status` 命令。

```
# /etc/rc.d/sshd status
sshd is running as pid 552.
# shutdown now                      # 进入单用户模式
# exit                              # 返回多用户模式
# shutdown -p now                   # 关闭并停止系统
# shutdown -r now                   # 重启
```

进程 `init` 也可以用于达到以下状态级别之一。例如 `# init 6` 用于重启。

- `0` 停止并关闭电源（信号 USR2）
- `1` 进入单用户模式（信号 TERM）
- `6` 重启机器（信号 INT）
- `c` 阻止进一步登录（信号 TSTP）
- `q` 重新扫描 `ttys(5)` 文件（信号 HUP）

### Windows

使用服务名称或“服务描述”（显示在“服务”控制面板中）来启动和停止服务，如下所示：

```
net stop WSearch
net start WSearch                   # 启动搜索服务
net stop "Windows Search"
net start "Windows Search"          # 与上面相同，使用描述名
```

## 1.6 重置 root 密码

### Linux 方法 1

在启动加载器（lilo 或 grub）处，输入以下启动选项：

```
init=/bin/sh
```

内核将挂载根分区，`init` 将启动 Bourne shell 而不是 rc，然后进入某个运行级。在提示符下使用 `passwd` 命令更改密码，然后重新启动。不要使用单用户模式，因为进入该模式也需要密码。

如果启动后根分区是只读挂载的，请重新以读写方式挂载：

```
# mount -o remount,rw /
# passwd                            # 或删除 root 密码（/etc/shadow）
# sync; mount -o remount,ro /       # 在重新只读挂载前先 sync
# reboot
```

### FreeBSD 方法 1

在 FreeBSD 上，进入单用户模式，重新以 rw 方式挂载 `/`，然后使用 `passwd`。你可以在启动菜单（选项 4）中选择单用户模式，该菜单在启动时显示 10 秒。单用户模式会为你提供 `/` 分区上的 root shell。

### Unix 系统以及 FreeBSD 和 Linux 方法 2

其他 Unix 系统可能不允许你使用简单的 init 技巧。解决办法是从另一个操作系统（如救援 CD）挂载根分区，并在磁盘上更改密码。

- 将 live CD 或安装 CD 启动到救援模式，这样你会获得一个 shell。
- 使用 `fdisk` 找到根分区，例如 `fdisk /dev/sda`
- 挂载它并使用 `chroot`：

```
# mount -o rw /dev/ad4s3a /mnt
# chroot /mnt          # chroot 到 /mnt
# passwd
# reboot
```

## 1.7 内核模块

### Linux

```
# lsmod                 # 列出内核中加载的所有模块
# modprobe isdn         # 加载模块（此处为 isdn）
```

### FreeBSD

```
# kldstat               # 列出内核中加载的所有模块
# kldload crypto        # 加载模块（此处为 crypto）
```

## 1.8 编译内核

### Linux

```
# cd /usr/src/linux
# make mrproper         # 清理所有内容，包括配置文件
# make oldconfig        # 如果存在，则复用旧的 .config
# make menuconfig       # 或 xconfig（Qt）或 gconfig（GTK）
# make                  # 创建压缩的内核镜像
# make modules          # 编译模块
# make modules_install  # 安装模块
# make install          # 安装内核
# reboot
```

### FreeBSD

可选地，使用 `csup`（自 FreeBSD 6.2 起）更新源代码树（位于 `/usr/src`）：

```
# csup <supfile>
```

我使用以下 supfile：

```
*default host=cvsup5.FreeBSD.org  # www.freebsd.org/handbook/cvsup.html#CVSUP-MIRRORS
*default prefix=/usr
*default base=/var/db
*default release=cvs delete tag=RELENG_7
src-all
```

要修改并重新构建内核，请将通用配置文件复制为一个新名称，并根据需要编辑（你也可以直接编辑 `GENERIC` 文件）。如果构建因中断而需要重新开始，请在 `make` 命令中添加 `NO_CLEAN=YES` 选项，以避免清理已构建的对象。

```
# cd /usr/src/sys/i386/conf/
# cp GENERIC MYKERNEL
# cd /usr/src
# make buildkernel KERNCONF=MYKERNEL
# make installkernel KERNCONF=MYKERNEL
```

要重新构建整个操作系统：

## 进程

```
# make buildworld          # Build the full OS but not the kernel
# make buildkernel         # Use KERNCONF as above if appropriate
# make installkernel
# reboot
# mergemaster -p           # Compares only files known to be essential
# make installworld
# mergemaster -i -U        # Update all configurations and other files
# reboot
```

对于源代码的小改动，可以使用 `NO_CLEAN=yes` 来避免重建整个树。

```
# make buildworld NO_CLEAN=yes      # Don't delete the old objects
# make buildkernel KERNCONF=MYKERNEL NO_CLEAN=yes
```

## 1.9 修复 grub



所以你弄坏了 `grub`？从 live cd 启动，[在 `/dev` 下找到你的 linux 分区并使用 `fdisk` 找到 linux 分区] 挂载 linux 分区，添加 `/proc` 和 `/dev` 并使用 `grub-install /dev/xyz`。假设 linux 位于 `/dev/sda6`：

```
# mount /dev/sda6 /mnt          # mount the linux partition on /mnt
# mount --bind /proc /mnt/proc   # mount the proc subsystem into /mnt
# mount --bind /dev /mnt/dev     # mount the devices into /mnt
# chroot /mnt                    # change root to the linux partition
# grub-install /dev/sda          # reinstall grub with your old settings
```

## 2 进程

| 列出 | 优先级 | 后台/前台 | Top | Kill |

|---------|----------|----------------------|-----|------|

| (p7) | (p7) | (p8) | (p8) | (p8) |

### 2.1 列出和 PIDs

每个进程都有一个唯一的编号，即 `PID`。所有正在运行的进程列表可通过 `ps` 获取。

```
# ps -auxefw                 # Extensive list of all running process
```

然而更典型的用法是使用管道或 `pgrep`：

```
# ps axww | grep cron
586  ??  Is   0:01.48 /usr/sbin/cron -s
# ps axjf                   # All processes in a tree format (Linux)
# ps aux | grep 'ss[h]'    # Find all ssh pids without the grep pid
# pgrep -l sshd             # Find the PIDs of processes by (part of) name
# echo $$                   # The PID of your shell
# fuser -va 22/tcp          # List processes using port 22 (Linux)
# pmap PID                  # Memory map of process (hunt memory leaks) (Linux)
# fuser -va /home           # List processes accessing the /home partition
# strace df                 # Trace system calls and signals
# truss df                  # same as above on FreeBSD/Solaris/Unixware
```

### 2.2 优先级

使用 `renice` 更改正在运行进程的优先级。负数优先级更高，最低为 `-20`，而 "`nice`" 具有正值。

```
# renice -5 586        # Stronger priority
586: old priority 0, new priority -5
```

使用 `nice` 以定义的优先级启动进程。正值为 "`nice`" 或较弱，负值为强调度优先级。确保你知道使用的是 `/usr/bin/nice` 还是 shell 内置命令（使用 `# which nice` 检查）。

```
# nice -n -5 top       # Stronger priority (/usr/bin/nice)
# nice -n 5 top         # Weaker priority (/usr/bin/nice)
# nice +5 top           # tcsh builtin nice (same as above!)
```

虽然 `nice` 更改 CPU 调度器，另一个有用的命令 `ionice` 将调度磁盘 IO。这对于密集 IO 应用程序（例如编译）非常有用。你可以选择一个类（空闲 - 最佳努力 - 实时），手册页简短且解释良好。

```
# ionice c3 -p123          # set idle class for pid 123 (Linux only)
# ionice -c2 -n0 firefox   # Run firefox with best effort and high priority
# ionice -c3 -p$$          # Set the actual shell to idle priority
```

最后一条命令对于编译（或调试）大型项目非常有用。从此 shell 启动的每个命令都将具有较低的优先级。`$$` 是你的 shell pid（尝试 `echo $$`）。

FreeBSD 使用 `idprio`/`rtprio`（`0` = 最大优先级，`31` = 最空闲）：

```
# idprio 31 make          # compile in the lowest priority
# idprio 31 -1234         # set PID 1234 with lowest priority
# idprio -t -1234         # -t removes any real time/idle priority
```

### 2.3 后台/前台

从 shell 启动时，进程可以使用 `[Ctrl]`-`[Z]` (`^Z`)、`bg` 和 `fg` 在后台和前台之间切换。使用 `jobs` 列出进程。

```
# ping cb.vu > ping.log
^Z                        # ping is suspended (stopped) with [Ctrl]-[Z]
# bg                      # put in background and continues running
# jobs -l                 # List processes in background
[1]  - 36232 Running       ping cb.vu > ping.log
[2]  + 36233 Suspended (tty output)  top
# fg %2                   # Bring process 2 back in foreground
```

使用 `nohup` 启动在 shell 关闭时仍需继续运行的进程（对挂断免疫）。

```
# nohup ping -i 60 > ping.log &
```

### 2.4 Top

程序 `top` 显示进程的运行信息。另请参阅来自 `htop.sourceforge.net` 的程序 `htop`（`top` 的更强大的版本），它可在 Linux 和 FreeBSD 上运行（`ports/sysutils/htop/`）。在 `top` 运行期间按 `h` 键获取帮助概览。实用键包括：

- `u [用户名]` 仅显示属于该用户的进程。使用 `+` 或空白查看所有用户

- `k [pid]` 使用 pid 终止进程。

- `1` 显示所有处理器统计信息（仅限 Linux）

- `R` 切换正常/反向排序。

### 2.5 信号/Kill

使用 `kill` 或 `killall` 终止或发送信号。

```
# ping -i 60 cb.vu > ping.log &
[1] 4712
# kill -s TERM 4712       # same as kill -15 4712
# killall -1 httpd        # Kill HUP processes by exact name
# pkill -9 http           # Kill TERM processes by (part of) name
# pkill -TERM -u www      # Kill TERM processes owned by www
# fuser -k -TERM -m /home # Kill every process accessing /home (to umount)
```

重要信号有：

- `1`  HUP（挂断）

- `2`  INT（中断）

- `3`  QUIT（退出）

- `9`  KILL（不可捕获，不可忽略的 kill）

- `15` TERM（软件终止信号）

## 3 文件系统



磁盘信息 (p9) | 启动 (p9) | 磁盘使用情况 (p9) | 已打开文件 (p9) | 挂载/重新挂载 (p10) | 挂载 SMB (p11) | 挂载镜像 (p12) | 刻录 ISO (p12) | 创建镜像 (p13) | 内存磁盘 (p14) | 磁盘性能 (p14)

### 3.1 权限

使用 `chmod` 和 `chown` 修改权限和所有权。默认 `umask` 可以在 Linux 的 `/etc/profile` 或 FreeBSD 的 `/etc/login.conf` 中为所有用户更改。默认 `umask` 通常为 `022`。`umask` 从 `777` 中减去，因此 `umask 022` 得到权限 `755`。

```
1 --x execute          # Mode 764 = exec/read/write | read/write | read
2 -w- write            # For:      |-- Owner --|  |- Group -|  |Oth|
4 r-- read             
ugo=a                  u=user, g=group, o=others, a=*everyone
```

```
# chmod [OPTION] MODE[,MODE] FILE      # MODE is of the form [ugoa]*([+-=])[(rwxXst])
# chmod 640 /var/log/maillog           # Restrict the log -rw-r-----
# chmod u=rw,g=r,o= /var/log/maillog   # Same as above
# chmod -R o-r /home/*                 # Recursive remove other readable for all users
# chmod u+s /path/to/prog              # Set SUID bit on executable (know what you do!)
# find / -perm -u+s -print             # Find all programs with the SUID bit
# chown user:group /path/to/file       # Change the user and group ownership of a file
# chgrp group /path/to/file            # Change the group ownership of a file
# chmod 640 `find ./ -type f -print`   # Change permissions to 640 for all files
# chmod 751 `find ./ -type d -print`   # Change permissions to 751 for all directories
```

### 3.2 磁盘信息

```
# diskinfo -v /dev/ad2           # information about disk (sector/size) FreeBSD
# hdparm -I /dev/sda              # information about the IDE/ATA disk (Linux)
# fdisk /dev/ad2                  # Display and manipulate the partition table
# smartctl -a /dev/ad2            # Display the disk SMART info
```

### 3.3 启动

#### FreeBSD

如果新内核无法启动，则在倒计时期间停止启动以启动旧内核。

```
# unload
# load kernel.old
# boot
```

### 3.4 系统挂载点/磁盘使用情况

```
# mount | column -t          # Show mounted file-systems on the system
# df                         # display free disk space and mounted devices
# cat /proc/partitions       # Show all registered partitions (Linux)
```

#### 磁盘使用情况

```
# du -sh *                   # Directory sizes as listing
# du -csh *                   # Total directory size of the current directory
# du -ks * | sort -n -r       # Sort everything by size in kilobytes
# ls -lSr                     # Show files, biggest last
```

### 3.5 谁打开了哪些文件

这对于查找阻止需要卸载的分区的文件很有用，并会出现典型的错误：

```
# umount /home/
umount: unmount of /home failed; Device busy
# umount impossible because a file is locking home
```

#### FreeBSD 和大多数 Unix 系统

```
# fstat -f /home          # for a mount point
# fstat -p PID            # for an application with PID
# fstat -u user           # for a user name
```

### 查找已打开的日志文件（或其他已打开文件），例如 Xorg：

```
# ps ax | grep Xorg | awk '{print $1}'
1252
# fstat -p 1252
USER     CMD        PID FD MOUNT      INUM MODE       SZ|DV R/W
root     Xorg      1252 root /        2 drwxr-xr-x 512 r
root     Xorg      1252 text /usr    216016 -rws--x--x 1679848 r
root     Xorg      1252 0 /var       212042 -rw-r--r-- 56987 w
```

inum 为 212042 的文件是 `/var` 中唯一的该文件：

```
# find -x /var -inum 212042
/var/log/Xorg.0.log
```

#### Linux

使用 `fuser` 或 `lsof` 查找挂载点上的已打开文件：

```
# fuser -m /home          # List processes accessing /home
# lsof /home
COMMAND  PID USER   FD   TYPE DEVICE    SIZE    NODE NAME
tcsh    29029 eedcoba cwd  DIR 0,18    12288   1048587 /home/eedcoba (guam:/home)
lsof    29140 eedcoba cwd  DIR 0,18    12288   1048587 /home/eedcoba (guam:/home)
```

### 关于某个应用程序：

```
ps ax | grep Xorg | awk '{print $1}'
3324
# lsof -p 3324
COMMAND  PID USER   FD   TYPE DEVICE    SIZE    NODE NAME
Xorg    3324 root   0w   REG 8,6     56296    12492 /var/log/Xorg.0.log
```

### 关于单个文件：

```
# lsof /var/log/Xorg.0.log
COMMAND  PID USER   FD   TYPE DEVICE    SIZE    NODE NAME
Xorg    3324 root   0w   REG 8,6     56296    12492 /var/log/Xorg.0.log
```

### 3.6 挂载/重新挂载文件系统

例如光盘。如果在 `/etc/fstab` 中列出：

```
# mount /cdrom
```

或在 `/dev/` 中查找设备或使用 `dmesg`

#### FreeBSD



```
# mount -v -t cd9660 /dev/cd0c /mnt   # cdrom
# mount_cd9660 /dev/wcd0c /cdrom     # other method
# mount -v -t msdos /dev/fd0c /mnt   # floppy
```

### `/etc/fstab` 中的条目：

```
# Device          Mountpoint  FStype  Options    Dump  Pass#
/dev/acd0         /cdrom      cd9660  ro,noauto  0     0
```

### 让用户执行挂载操作：

```
# sysctl vfs.usermount=1  # Or insert the line "vfs.usermount=1" in /etc/sysctl.conf
```

#### Linux

```
# mount -t auto /dev/cdrom /mnt/cdrom    # typical cdrom mount command
# mount /dev/hdc -t iso9660 -r /cdrom    # typical IDE
# mount /dev/scd0 -t iso9660 -r /cdrom    # typical SCSI cdrom
# mount /dev/sdC0 -t ntfs-3g /windows    # typical SCSI
```

### `/etc/fstab` 中的条目：

```
/dev/cdrom  /media/cdrom  subfs noauto,fs=cdfs,ro,procuid,nosuid,nodev,exec 0 0
```

### 使用 Linux 挂载 FreeBSD 分区

使用 `fdisk` 找到分区号，通常是根分区，但也可能是其他 BSD 切片。如果 FreeBSD 有多个切片，它们不会列在 `fdisk` 表中，但在 `/dev/sda*` 或 `/dev/hda*` 中可见。

```
# fdisk /dev/sda                # Find the FreeBSD partition
# /dev/sda3   *    5357        7905    20474842+  a5  FreeBSD
# mount -t ufs -o ufstype=ufs2,ro /dev/sda3 /mnt
/dev/sda1o = /tmp; /dev/sda11 /usr   # The other slices
```

#### 重新挂载

在不卸载的情况下重新挂载设备。例如 `fsck` 时需要

```
# mount -o remount,ro /          # Linux
# mount -o ro /                  # FreeBSD
```

将光盘的原始数据复制到 iso 镜像中：

```
# dd if=/dev/cd0c of=file.iso
```

### 3.7 动态添加 swap

假设你现在需要更多 swap，比如一个 2GB 文件 `/swap2gb`（仅限 Linux）。

```
# dd if=/dev/zero of=/swap2gb bs=1024k count=2000
# mkswap /swap2gb                # create the swap area
# swapon /swap2gb                # activate the swap. It now in use
# swapoff /swap2gb               # when done deactivate the swap
# rm /swap2gb
```

### 3.8 挂载 SMB 共享

假设我们想访问计算机 `smbserver` 上的 SMB 共享 `myshare`，在 Windows PC 上输入的地址为 `\\smbserver\myshare\`。我们挂载到 `/mnt/smbshare`。警告> `cifs` 需要 IP 或 DNS 名称，而不是 Windows 名称。

#### Linux

```
# smbclient -U user -I 192.168.16.229 -L //smbshare/   # List the shares
# mount -t smbfs -o username=winuser //smbserver/myshare /mnt/smbshare
# mount -t cifs -o username=winuser,password=winpwd //192.168.16.229/myshare /mnt/share
```

另外，使用 `mount.cifs` 包可以将凭据存储在文件中，例如 `/home/user/.smb`：

```
username=winuser
password=winpwd
```

然后按如下方式挂载：

```
# mount -t cifs -o credentials=/home/user/.smb //192.168.16.229/myshare /mnt/smbshare
```

#### FreeBSD

使用 `-I` 指定 IP（或 DNS 名称）；`smbserver` 是 Windows 名称。

```
# smbutil view -I 192.168.16.229 //winuser@smbserver   # List the shares
# mount_smbfs -I 192.168.16.229 //winuser@smbserver/myshare /mnt/smbshare
```

### 3.9 挂载镜像

### Linux loop-back

```
# mount -t iso9660 -o loop file.iso /mnt          # Mount a CD image
# mount -t ext3 -o loop file.img /mnt             # Mount an image with ext3 fs
```

#### FreeBSD

使用内存设备（必要时执行 `# kldload md.ko`）：

```
# mdconfig -a -t vnode -f file.iso -u 0
# mount -t cd9660 /dev/md0 /mnt
# umount /mnt; mdconfig -d -u 0                     # Cleanup the md device
```

或使用虚拟节点：

```
# vnconfig /dev/vn0c file.iso; mount -t cd9660 /dev/vn0c /mnt
# umount /mnt; vnconfig -u /dev/vn0c               # Cleanup the vn device
```

### Solaris 和 FreeBSD

使用 loop-back 文件接口或 `lofi`：

```
# lofiadm -a file.iso
# mount -F hsfs -o ro /dev/lofi/1 /mnt
# umount /mnt; lofiadm -d /dev/lofi/1               # Cleanup the lofi device
```

### 3.10 创建和刻录 ISO 镜像

这将按扇区复制 cd 或 DVD。没有 `conv=notrunc`，镜像会更小，如果 cd 上内容较少。见下文和 `dd` 示例（第 41 页）。

```
# dd if=/dev/hdc of=/tmp/mycd.iso bs=2048 conv=notrunc
```

使用 `mkisofs` 从目录中的文件创建 CD/DVD 镜像。为克服文件名限制：`-r` 启用常见于 UNIX 系统的 Rock Ridge 扩展，`-J` 启用 Microsoft 系统使用的 Joliet 扩展。`-L` 允许 ISO9660 文件名以句点开头。

```
# mkisofs -J -L -r -V TITLE -o imagefile.iso /path/to/dir
```

在 FreeBSD 上，`mkisofs` 可在 ports 的 `sysutils/cdtools` 中找到。

#### 刻录 CD/DVD ISO 镜像

#### FreeBSD

FreeBSD 默认不会在 ATAPI 驱动器上启用 DMA。DMA 可通过 `sysctl` 命令和以下参数启用，或通过 `/boot/loader.conf` 中的以下条目启用：

```
hw.ata.ata_dma="1"
hw.ata.atapi_dma="1"
```

使用 ATAPI 设备使用 `burncd`（`burncd` 是基本系统的一部分）和使用 SCSI 驱动器的 `cdrecord`（在 `sysutils/cdtools` 中）。



# burncd -f /dev/acd0 data imagefile.iso fixate      # For ATAPI drive
# cdrecord -scanbus                                   # To find the burner device (like 1,0,0)
# cdrecord dev=1,0,0 imagefile.iso

## Linux

也可以按上述描述使用 `cdrecord`。还可以使用原生 ATAPI 接口，可通过以下方式找到：

```
# cdrecord dev=ATAPI -scanbus
```

并按上述方式刻录 CD/DVD。

# dvd+rw-tools

`dvd+rw-tools` 软件包（FreeBSD: `ports/sysutils/dvd+rw-tools`）可以完成所有操作，并且包含 `growisofs` 用于刻录 CD 或 DVD。示例中将 dvd 设备引用为 `/dev/dvd`，它可能是 `/dev/scd0` 的符号链接（Linux 典型的 scsi），或 `/dev/cd0`（典型的 FreeBSD），或 `/dev/rcd0c`（典型的 NetBSD/OpenBSD 字符 SCSI），或 `/dev/rdsk/c0t1d0s2`（Solaris 字符 SCSI/ATAPI CD-ROM 设备的示例）。FreeBSD 手册第 18.7 章中有很好的文档和示例。

```
# -dvd-compat closes the disk
# growisofs -dvd-compat -Z /dev/dvd=imagefile.iso   # Burn existing iso image
# growisofs -dvd-compat -Z /dev/dvd -J -R /p/to/data   # Burn directly
```

## 将 Nero .nrg 文件转换为 .iso

Nero 只是在正常的 iso 映像前添加了 300Kb 的头。这可以用 `dd` 去除。

```
# dd bs=1k if=imagefile.nrg of=imagefile.iso skip=300
```

## 将 bin/cue 映像转换为 .iso

小巧的 `bchunk` 程序可以做到这一点。它在 FreeBSD ports 中位于 `sysutils/bchunk`。

```
# bchunk imagefile.bin imagefile.cue imagefile.iso
```

### 3.11 创建基于文件的映像

例如使用文件 `/usr/vdisk.img` 创建一个 1GB 的分区。这里我们使用 vnode 0，但也可以是 1。

#### FreeBSD

```
# dd if=/dev/random of=/usr/vdisk.img bs=1K count=1M
# mdconfig -a -t vnode -f /usr/vdisk.img -u 0          # Creates device /dev/md0
# bsdlabel -w /dev/md0
# newfs /dev/md0c
# mount /dev/md0c /mnt
# umount /mnt; mdconfig -d -u 0; rm /usr/vdisk.img      # Cleanup the md device
```

基于文件的映像可以通过 `/etc/rc.conf` 和 `/etc/fstab` 中的条目在启动时自动挂载。使用 `# /etc/rc.d/mdconfig start` 测试你的设置（首先使用 `# mdconfig -d -u 0` 删除 `md0` 设备）。

请注意，此自动设置仅在文件映像不在根分区上时才有效。原因是 `/etc/rc.d/mdconfig` 脚本在启动期间非常早执行，而根分区仍为只读。位于根分区之外的映像将使用脚本 `/etc/rc.d/mdconfig2` 稍后挂载。

`/boot/loader.conf`:

```
md_load="YES"
```

`/etc/rc.conf`:

```
# mdconfig_md0="-t vnode -f /usr/vdisk.img"      # /usr is not on the root partition
```

`/etc/fstab`:（末尾的 0 0 很重要，它告诉 `fsck` 忽略此设备，因为它尚不存在）

```
/dev/md0c          /usr/vdisk    ufs     rw              0       0
```

之后也可以增大映像的大小，例如增大 300 MB。

```
# umount /mnt; mdconfig -d -u 0
# dd if=/dev/zero bs=1m count=300 >> /usr/vdisk.img
# mdconfig -a -t vnode -f /usr/vdisk.img -u 0
# growfs /dev/md0
# mount /dev/md0c /mnt                                 # File partition is now 300 MB larger
```

#### Linux

```
# dd if=/dev/zero of=/usr/vdisk.img bs=1024k count=1024
# mkfs.ext3 /usr/vdisk.img
# mount -o loop /usr/vdisk.img /mnt
# umount /mnt; rm /usr/vdisk.img        # Cleanup
```

#### Linux with losetup

`/dev/zero` 比 `urandom` 快得多，但对加密来说安全性较低。

```
# dd if=/dev/urandom of=/usr/vdisk.img bs=1024k count=1024
# losetup /dev/loop0 /usr/vdisk.img          # Creates and associates /dev/loop0
# mkfs.ext3 /dev/loop0
# mount /dev/loop0 /mnt
# losetup -a                                 # Check used loops
# umount /mnt
# losetup -d /dev/loop0                      # Detach
# rm /usr/vdisk.img
```

### 3.12 创建内存文件系统

内存基于文件系统对于重 IO 应用程序来说非常快。如何创建挂载在 `/memdisk` 上的 64 MB 分区：

#### FreeBSD

```
# mount_mfs -o rw -s 64M md /memdisk
# umount /memdisk; mdconfig -d -u 0          # Cleanup the md device
md      /memdisk    mfs     rw,-s64M    0    0    # /etc/fstab entry
```

#### Linux

```
# mount -t tmpfs -osize=64m tmpfs /memdisk
```

### 3.13 磁盘性能

在分区 `ad4s3c`（`/home`）上读写 1 GB 文件

```
# time dd if=/dev/ad4s3c of=/dev/null bs=1024k count=1000
# time dd if=/dev/zero bs=1024k count=1000 of=/home/1Gb.file
# hdparm -tT /dev/hda        # Linux only
```

# 4 NETWORK

路由（p15） | 额外 IP（p15） | 更改 MAC（p16） | 端口（p16） | 防火墙（p16） | IP 转发（p17） | NAT（p17） | DNS（p17） | DHCP（p19） | 流量（p19） | QoS（p20） | NIS（p21） | Netcat（p21）

### 4.1 调试（另见 流量分析）（第 19 页）

#### Linux



# ethtool eth0                         # Show the ethernet status (replaces mii-diag)
# ethtool -s eth0 speed 100 duplex full # Force 100Mbit Full duplex
# ethtool -s eth0 autoneg off          # Disable auto negotiation
# ethtool -p eth1                       # Blink the ethernet led - very useful when supported
# ip link show                          # Display all interfaces on Linux (similar to ifconfig)
# ip link set eth0 up                   # Bring device up (or down). Same as "ifconfig eth0 up"
# ip addr show                          # Display all IP addresses on Linux (similar to ifconfig)
# ip neigh show                         # Similar to arp -a

## 其他操作系统

```
# ifconfig fxp0                  # Check the "media" field on FreeBSD
# arp -a                         # Check the router (or host) ARP entry (all OS)
# ping cb.vu                      # The first thing to try...
# traceroute cb.vu                # Print the route path to destination
# ifconfig fxp0 media 100baseTX mediaopt full-duplex # 100Mbit full duplex (FreeBSD)
# netstat -s                      # System-wide statistics for each network protocol
```

默认情况下并非总是安装但易于找到的附加命令：

```
# arping 192.168.16.254          # Ping on ethernet layer
# tcptraceroute -f 5 cb.vu       # uses tcp instead of icmp to trace through firewalls
```

### 4.2 路由

#### 打印路由表

```
# route -n                       # Linux or use "ip route"
# netstat -rn                     # Linux, BSD and UNIX
# route print                     # Windows
```

#### 添加和删除路由

FreeBSD

```
# route add 212.117.0.0/16 192.168.1.1
# route delete 212.117.0.0/16
# route add default 192.168.1.1
```

在 `/etc/rc.conf` 中永久添加路由

```
static_routes="myroute"
route_myroute="-net 212.117.0.0/16 192.168.1.1"
```

Linux

```
# route add -net 192.168.20.0 netmask 255.255.255.0 gw 192.168.16.254
# ip route add 192.168.20.0/24 via 192.168.16.254      # same as above with ip route
# route add -net 192.168.20.0 netmask 255.255.255.0 dev eth0
# route add default gw 192.168.51.254
# ip route add default via 192.168.51.254 dev eth0     # same as above with ip route
# route delete -net 192.168.20.0 netmask 255.255.255.0
```

Solaris

```
# route add -net 192.168.20.0 -netmask 255.255.255.0 192.168.16.254
# route add default 192.168.51.254 1                   # 1 = hops to the next gateway
# route change default 192.168.50.254 1
```

永久条目设置在 `/etc/defaultrouter` 中的条目。

Windows

```
# Route add 192.168.50.0 mask 255.255.255.0 192.168.51.253
# Route add 0.0.0.0 mask 0.0.0.0 192.168.51.254
```

使用 `add -p` 使路由持久化。

### 4.3 配置附加 IP 地址

#### Linux

```
# ifconfig eth0 192.168.50.254 netmask 255.255.255.0      # First IP
# ifconfig eth0:0 192.168.51.254 netmask 255.255.255.0     # Second IP
# ip addr add 192.168.50.254/24 dev eth0                   # Equivalent ip commands
# ip addr add 192.168.51.254/24 dev eth0 label eth0:1
```

#### FreeBSD

```
# ifconfig fxp0 inet 192.168.50.254/24          # First IP
# ifconfig fxp0 alias 192.168.51.254 netmask 255.255.255.0  # Second IP
# ifconfig fxp0 -alias 192.168.51.254                     # Remove second IP alias
```

`/etc/rc.conf` 中的永久条目

```
ifconfig_fxp0="inet 192.168.50.254  netmask 255.255.255.0"
ifconfig_fxp0_alias0="192.168.51.254 netmask 255.255.255.0"
```

#### Solaris

使用 `ifconfig -a` 检查设置

```
# ifconfig hme0 plumb                         # Enable the network card
# ifconfig hme0 192.168.50.254 netmask 255.255.255.0 up  # First IP
# ifconfig hme0:1 192.168.51.254 netmask 255.255.255.0 up  # Second IP
```

### 4.4 修改 MAC 地址

通常你必须在更改前将接口关闭。不要告诉我你为什么想更改 MAC 地址...

```
# ifconfig eth0 down
# ifconfig eth0 hw ether 00:01:02:03:04:05      # Linux
# ifconfig fxp0 link 00:01:02:03:04:05           # FreeBSD
# ifconfig hme0 ether 00:01:02:03:04:05          # Solaris
# sudo ifconfig en0 ether 00:01:02:03:04:05      # Mac OS X Tiger
# sudo ifconfig en0 lladdr 00:01:02:03:04:05     # Mac OS X Leopard
```

Windows 上存在许多工具。例如 `etherchange4`。或查找 "Mac Makeup"、"smac"。

### 4.5 使用中的端口

正在监听的开放端口：



```
# netstat -an | grep LISTEN
# lsof -i                # Linux list all Internet connections
# socklist               # Linux display list of open sockets
# sockstat -4            # FreeBSD application listing
# netstat -anp --udp --tcp | grep LISTEN   # Linux
# netstat -tup           # List active connections to/from system (Linux)
# netstat -tupi          # List listening ports from system (Linux)
# netstat -ano            # Windows
```

### 4.6 防火墙

检查防火墙是否正在运行（典型配置）：

#### Linux

```
# iptables -L -n -v               # For status
```
打开 `iptables` 防火墙
```
# iptables -P INPUT   ACCEPT       # Open everything
# iptables -P FORWARD ACCEPT
# iptables -P OUTPUT  ACCEPT
# iptables -Z                         # Zero the packet and byte counters in all chains
# iptables -F                          # Flush all chains
# iptables -X                          # Delete all chains
```

#### FreeBSD

```
# ipfw show                         # For status
# ipfw list 65535 # if answer is "65535 deny ip from any to any" the fw is disabled
# sysctl net.inet.ip.fw.enable=0     # Disable
# sysctl net.inet.ip.fw.enable=1     # Enable
```

### 4.7 IP 转发用于路由

Linux

检查并启用 IP 转发：

```
# cat /proc/sys/net/ipv4/ip_forward   # Check IP forward 0=off, 1=on
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

或编辑 `/etc/sysctl.conf`：

```
net.ipv4.ip_forward = 1
```

FreeBSD

检查并启用：

```
# sysctl net.inet.ip.forwarding      # Check IP forward 0=off, 1=on
# sysctl net.inet.ip.forwarding=1
# sysctl net.inet.ip.fastforwarding=1      # For dedicated router or firewall
```

永久生效请在 `/etc/rc.conf` 中添加条目：

```
gateway_enable="YES"      # Set to YES if this host will be a gateway.
```

Solaris

```
# ndd -set /dev/ip ip_forwarding 1   # Set IP forward 0=off, 1=on
```

### 4.8 NAT 网络地址转换

Linux

```
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE      # to activate NAT
# iptables -t nat -A PREROUTING -p tcp -d 78.31.70.238 --dport 20022 -j DNAT \
--to 192.168.16.44:22      # Port forward 20022 to internal IP port ssh
# iptables -t nat -A PREROUTING -p tcp -d 78.31.70.238 --dport 993:995 -j DNAT \
--to 192.168.16.254:993-995      # Port forward of range 993-995
# ip route flush cache
# iptables -L -t nat      # Check NAT status
```

使用 `-D` 代替 `-A` 删除端口转发。程序 `netstat-nat`⁵ 非常有用，可以追踪连接（它使用 `/proc/net/ip_conntrack` 或 `/proc/net/nf_conntrack`）。

```
# netstat-nat -n      # show all connections with IPs
```

```
# natd -s -m -u -dynamic -f /etc/natd.conf -n fxp0
```

或编辑 `/etc/rc.conf`：

```
firewall_enable="YES"      # Set to YES to enable firewall functionality
firewall_type="open"      # Firewall type (see /etc/rc.firewall)
natd_enable="YES"      # Enable natd (if firewall_enable == YES).
natd_interface="tun0"      # Public interface or IP address to use.
natd_flags="-s -m -u -dynamic -f /etc/natd.conf"
```

端口转发配置：

```
# cat /etc/natd.conf
same_ports yes
use_sockets yes
unregistered_only
# redirect_port tcp insideIP:2300-2399 3300-3399  # port range
redirect_port udp 192.168.51.103:7777 7777
```

### 4.9 DNS

在 Unix 上，DNS 条目对所有接口有效，并存储在 `/etc/resolv.conf` 中。主机所属的域也存储在此文件中。最小配置如下：

`nameserver 78.31.70.238`

`search sleepyowl.net intern.lab`

`domain sleepyowl.net`

使用以下命令检查系统域名：

```
# hostname -d          # Same as dnsdomainname
```

### Windows

在 Windows 上，DNS 按接口配置。要显示已配置的 DNS 并刷新 DNS 缓存，请使用：

```
# ipconfig /?
# ipconfig /all
```

#### 刷新 DNS

刷新操作系统的 DNS 缓存，部分应用程序使用自己的缓存（例如 Firefox）不受影响。

```
# /etc/init.d/nscd restart    # Restart nscd if used - Linux/BSD/Solaris
# lookupd -flushcache          # OS X Tiger
# dscacheutil -flushcache      # OS X Leopard and newer
# ipconfig /flushdns           # Windows
```

#### 转发查询

`Dig` 是测试 DNS 设置的好帮手。例如公共 DNS 服务器 `213.133.105.2` `ns.second-ns.de` 可用于测试。查看客户端从哪个服务器接收到响应（简化答案）。

```
# dig sleepyowl.net
sleepyowl.net.      600  IN  A     78.31.70.238
;; SERVER: 192.168.51.254#53(192.168.51.254)
```

路由器 `192.168.51.254` 作出了响应，响应为 A 记录。任何记录都可以查询，并且可以使用 `@` 指定 DNS 服务器：



```
# dig MX google.com
# dig @127.0.0.1 NS sun.com        # To test the local server
# dig @204.97.212.10 NS MX heise.de # Query an external server
# dig AXFR @ns1.xname.org cb.vu   # Get the full zone (zone transfer)
```

程序 `host` 也很强大。

```
# host -t MX cb.vu          # Get the mail MX entry
# host -t NS -T sun.com     # Get the NS record over a TCP connection
# host -a sleepyowl.net     # Get everything
```

#### 反向查询

查找属于某个 IP 地址的名称（`in-addr.arpa.`）。这可以使用 `dig`、`host` 和 `nslookup` 完成：

```
# dig -x 78.31.70.238
# host 78.31.70.238
# nslookup 78.31.70.238
```

#### `/etc/hosts`

单个主机可以在文件 `/etc/hosts` 中配置，而无需本地运行 `named` 来解析主机名查询。格式很简单，例如：

```
78.31.70.238  sleepyowl.net  sleepyowl
```

`hosts` 与 DNS 查询之间的优先级，即名称解析顺序，可以在 `/etc/nsswitch.conf` 和 `/etc/host.conf` 中配置。该文件在 Windows 上也存在，通常位于：

```
C:\WINDOWS\SYSTEM32\DRIVERS\ETC
```

### 4.10 DHCP

#### Linux

某些发行版（SuSE）使用 `dhcpc d` 作为客户端。默认接口为 `eth0`。

```
# dhcpc d -n eth0          # Trigger a renew (does not always work)
# dhcpc d -k eth0          # release and shutdown
```

包含完整信息的租约存储在：

```
/var/lib/dhcpc d/dhcpc d-eth0.info
```

#### FreeBSD

FreeBSD（和 Debian）使用 `dhclient`。要配置一个接口（例如 `bge0`）运行：

```
# dhclient bge0
```

包含完整信息的租约存储在：

```
/var/db/dhclient.leases.bge0
```

### 使用

```
/etc/dhclient.conf
```

在前面添加选项或强制使用不同选项：

```
# cat /etc/dhclient.conf
interface "rl0" {
    prepend domain-name-servers 127.0.0.1;
    default domain-name "sleepyowl.net";
    supersede domain-name "sleepyowl.net";
}
```

### Windows

`dhcp` 租约可以用 `ipconfig` 续期：

```
# ipconfig /renew       # renew all adapters
# ipconfig /renew LAN    # renew the adapter named "LAN"
# ipconfig /release WLAN # release the adapter named "WLAN"
```

是的，将适配器重命名为简单名称是个好主意！

### 4.11 流量分析

`Bmon`⁶ 是一个小型控制台带宽监视器，可以显示不同接口上的流量。

#### 使用 `tcpdump` 嗅探

```
# tcpdump -n l -i bge0 not port ssh and src \(192.168.16.121 or 192.168.16.54\)
# tcpdump -n -i eth1 net 192.168.16.121          # select to/from a single IP
# tcpdump -n -i eth1 net 192.168.16.0/24          # select traffic to/from a network
# tcpdump -l > dump && tail -f dump               # Buffered output
# tcpdump -i r10 -w traffic.r10                   # Write traffic headers in binary file
# tcpdump -i r10 -s 0 -w traffic.r10              # Write traffic + payload in binary file
# tcpdump -r traffic.r10                          # Read from file (also for ethereal)
# tcpdump port 80                                 # The two classic commands
# tcpdump host google.com
# tcpdump -i eth0 -X port \(110 or 143\)          # Check if pop or imap is secure
# tcpdump -n -i eth0 icmp                         # Only catch pings
# tcpdump -i eth0 -s 0 -A port 80 | grep GET      # -s 0 for full packet -A for ASCII
```

其他重要选项：

- `-A`  以明文打印每个数据包（无头）

- `-X`  以十六进制和 ASCII 打印数据包

- `-l`  使 stdout 行缓冲

- `-D`  打印所有可用接口

在 Windows 上使用来自 `www.winpcap.org` 的 `windump`。使用 `windump -D` 列出接口。

#### 使用 `nmap` 扫描

`Nmap`⁷ 是一款具有操作系统检测功能的端口扫描器，通常已安装在大多数发行版上，也可用于 Windows。如果你不扫描你的服务器，黑客会替你扫描...

```
# nmap cb.vu          # scans all reserved TCP ports on the host
# nmap -sP 192.168.16.0/24  # Find out which IP are used and by which host on 0/24
# nmap -sS -sV -O cb.vu   # Do a stealth SYN scan with version and OS detection
PORT     STATE SERVICE            VERSION
22/tcp   open  ssh                OpenSSH 3.8.1p1 FreeBSD-20060930 (protocol 2.0)
25/tcp   open  smtp               Sendmail smtpd 8.13.6/8.13.6
80/tcp   open  http               Apache httpd 2.0.59 ((FreeBSD) DAV/2 PHP/4.
[...]
Running: FreeBSD 5.X
Uptime 33.120 days (since Fri Aug 31 11:41:04 2007)
```

其他非标准但有用的工具是 `hping`（`www.hping.org`）一个 IP 数据包组装/分析器和 `fping`（`fping.sourceforge.net`）。`fping` 可以以轮询方式检查多个主机。

### 4.12 流量控制（QoS）

流量控制管理网络的排队、策略、调度和其他流量参数。以下示例是 Linux 和 FreeBSD 能力的简单实用用法，以更好地利用可用带宽。

#### 限制上传

DSL 或电缆调制解调器具有较长的队列以提高上传吞吐量。然而用快速设备（例如以太网）填满队列会显著降低交互性。因此将设备上传速率限制以匹配调制解调器的物理容量是有用的，这应大大提高交互性。设置为调制解调器最大（电缆）速度的约 90%。

#### Linux

对于 512 Kbit 上传调制解调器。



```
# tc qdisc add dev eth0 root tbf rate 480kbit latency 50ms burst 1540
# tc -s qdisc ls dev eth0                 # Status
# tc qdisc del dev eth0 root              # Delete the queue
# tc qdisc change dev eth0 root tbf rate 220kbit latency 50ms burst 1540
```

### FreeBSD

FreeBSD 使用 `dummynet` 流量整形器，通过 `ipfw` 配置。管道用于以 `[K|M]{bit/s|Byte/s}` 单位设置带宽限制，0 表示带宽无限制。使用相同的管道编号会重新配置它。例如将上传带宽限制为 500 Kbit。

```
# kldload dummynet          # load the module if necessary
# ipfw pipe 1 config bw 500Kbit/s      # create a pipe with limited bandwidth
# ipfw add pipe 1 ip from me to any   # divert the full upload into the pipe
```

### 服务质量

#### Linux

使用 `tc` 进行优先级队列以优化 VoIP。完整示例请参见 `voip-info.org` 或 `www.howtoforge.com`。假设 VoIP 使用 `udp` 端口 `10000:11024` 和设备 `eth0`（也可能是 `ppp0` 等）。以下命令将 QoS 定义为三个队列并强制 VoIP 流量进入队列 1，QoS 为 `0x1e`（所有位都置位）。默认流量进入队列 3，QoS 最小化延迟进入队列 2。

```
# tc qdisc add dev eth0 root handle 1: prio priomap 2 2 2 2 2 2 2 2 1 1 1 1 1 1 0
# tc qdisc add dev eth0 parent 1:1 handle 10: sfq
# tc qdisc add dev eth0 parent 1:2 handle 20: sfq
```

```
# tc qdisc add dev eth0 parent 1:3 handle 30: sfq
```

```
# tc filter add dev eth0 protocol ip parent 1: prio 1 u32 \
match ip dport 10000 0x3C00 flowid 1:1        # 使用服务器端口范围
match ip dst 123.23.0.1 flowid 1:1            # 或/和使用服务器 IP
```

#### 状态和删除

```
# tc -s qdisc ls dev eth0        # 队列状态
# tc qdisc del dev eth0 root     # 删除所有 QoS
```

#### 计算端口范围和掩码

`tc filter` 使用端口和掩码来定义端口范围，你需要自行计算。找到端口范围的 2^N 末尾，推导出范围并转换为 HEX。这就是你的掩码。例如 `10000 -> 11024`，范围为 1024。

```
# 2^13 (8192) < 10000 < 2^14 (16384)      # 末尾是 2^14 = 16384
# echo "obase=16; (2^14)-1024" | bc      # 掩码是 0x3C00
```

#### FreeBSD

最大链路带宽为 500Kbit/s，我们为 VoIP:ssh:其余所有流量定义了 3 个队列，优先级为 100:10:1。

```
# ipfw pipe 1 config bw 500Kbit/s
# ipfw queue 1 config pipe 1 weight 100
# ipfw queue 2 config pipe 1 weight 10
# ipfw queue 3 config pipe 1 weight 1
# ipfw add 10 queue 1 proto udp dst-port 10000-11024
# ipfw add 11 queue 1 proto udp dst-ip 123.23.0.1  # 或/和使用服务器 IP
# ipfw add 20 queue 2 dport ssh
# ipfw add 30 queue 3 from me to any                # 其余所有流量
```

#### 状态和删除

```
# ipfw list                        # 规则状态
# ipfw pipe list                    # 管道状态
# ipfw flush                        # 删除所有规则但保留默认
```

### 4.13 NIS 调试

在配置良好的 NIS 客户端上应能正常工作的一些命令：

```
# ypwhich            # 获取连接的 NIS 服务器名称
# domainname         # 配置的 NIS 域名
# ypcat group        # 应显示来自 NIS 服务器的组
# cd /var/yp && make # 重新构建 yp 数据库
# rpcinfo -p servername  # 报告服务器的 RPC 服务
```

#### ypbind 是否正在运行？

```
# ps auxww | grep ypbind
/usr/sbin/ypbind -s -m -S servername1,servername2      # FreeBSD
/usr/sbin/ypbind        # Linux
# yppoll passwd.byname
Map passwd.byname has order number 1190635041. Mon Sep 24 13:57:21 2007
The master server is servername.domain.net.
```

#### Linux

```
# cat /etc/yp.conf
yps servername
domain domain.net broadcast
```

### 4.14 Netcat

`Netcat®` (`nc`) 更为人所知的是“网络瑞士军刀”，它可以操作、创建或读写 TCP/IP 连接。以下是一些有用的示例，网上还有更多，例如 `g-loaded.eu[...]`⁹ 和这里¹⁰。

你可能需要使用命令 `netcat` 而不是 `nc`。另请参阅类似的命令 `socat`。

#### 文件传输

通过原始 tcp 连接复制一个大文件夹。传输非常快（无协议开销），你无需折腾 NFS 或 SMB 或 FTP 等，只需在服务器上使文件可用，然后从客户端获取。这里 `192.168.1.1` 是服务器 IP 地址。

```
server# tar -cf - -C VIDEO_TS . | nc -l -p 4444      # 在端口 4444 上提供 tar 文件夹
client# nc 192.168.1.1 4444 | tar xpf - -C VIDEO_TS   # 在端口 4444 上拉取文件
server# cat largefile | nc -l 5678                   # 提供单个文件
client# nc 192.168.1.1 5678 > largefile              # 拉取单个文件
server# dd if=/dev/da0 | nc -l 4444                  # 提供分区镜像
client# nc 192.168.1.1 4444 | dd of=/dev/da0          # 拉取分区以克隆
client# nc 192.168.1.1 4444 | dd of=da0.img           # 拉取分区到文件
```

#### 其他技巧

特别是在这里，你必须知道自己在做什么。

#### 远程 shell

选项 `-e` 仅在 Windows 版本上可用？或使用 `nc 1.10`。

```
# nc -lp 4444 -e /bin/bash          # 提供远程 shell（服务器后门）
# nc -lp 4444 -e cmd.exe             # Windows 的远程 shell
```

#### 紧急 Web 服务器

在循环中在端口 80 上提供单个文件。

```
# while true; do nc -l -p 80 < unixtoolbox.xhtml; done
```

#### 聊天

Alice 和 Bob 可以通过简单的 TCP 套接字聊天。文本通过回车键传输。

```
alice# nc -lp 4444
bob  # nc 192.168.1.1 4444
```

## 5 SSH SCP



公钥 (`p22`) | 指纹 (`p23`) | SCP (`p23`) | 隧道 (`p24`)

### 5.1 公钥认证

使用公钥认证无需密码连接到主机。其思想是将你的公钥追加到远程主机的 `authorized_keys2` 文件中。对于此示例，让我们将 `host-client` 连接到 `host-server`，密钥在客户端生成。使用 `cygwin` 时，你可能需要创建主目录和 `.ssh` 目录，执行 `# mkdir -p /home/USER/.ssh`

- 使用 `ssh-keygen` 生成密钥对。`~/.ssh/id_dsa` 是私钥，`~/.ssh/id_dsa.pub` 是公钥。
- 将公钥复制到服务器并追加到服务器上你主目录中的文件 `~/.ssh/authorized_keys2`。

```
# ssh-keygen -t dsa -N ''
# cat ~/.ssh/id_dsa.pub | ssh you@host-server "cat - >> ~/.ssh/authorized_keys2"
```

#### 使用来自 ssh.com 的 Windows 客户端

非商业版的 `ssh.com` 客户端可以从主 `ftp` 站点下载：`ftp.ssh.com/pub/ssh/`。`ssh.com` 客户端生成的密钥需要转换为 OpenSSH 服务器可用的格式。这可以使用 `ssh-keygen` 命令完成。

`9.http://www.g-loaded.eu/2006/11/06/netcat-a-couple-of-useful-examples`

`10.http://www.terminally-incoherent.com/blog/2007/08/07/few-useful-netcat-tricks`

- 使用 `ssh.com` 客户端创建密钥对：设置 - 用户身份验证 - 生成新...
- 我使用密钥类型 `DSA`；密钥长度 `2048`。
- 将 `ssh.com` 客户端生成的公钥复制到服务器的 `~/.ssh` 文件夹中。
- 密钥位于 `C:\Documents and Settings\%USERNAME%\Application Data\SSH\UserKeys`。
- 在服务器上使用 `ssh-keygen` 命令转换密钥：

```
# cd ~/.ssh
# ssh-keygen -i -f keyfilename.pub >> authorized_keys2
```

注意：我们使用的是 `DSA` 密钥，`RSA` 也是可能的。密钥未受密码保护。

#### 使用 putty for Windows

`Putty` 是 Windows 的一个简单免费 `ssh` 客户端。

- 使用 `puTTYgen` 程序创建密钥对。
- 保存公钥和私钥（例如保存到 `C:\Documents and Settings\%USERNAME%\.ssh`）。
- 将公钥复制到服务器的 `~/.ssh` 文件夹中：

```
# scp .ssh/puttykey.pub root@192.168.51.254:~/.ssh/
```

- 在服务器上使用 `ssh-keygen` 命令将密钥转换为 OpenSSH 用：
- 在 `putty` 设置中指定私钥位置：连接 - SSH - 身份验证

```
# cd ~/.ssh
# ssh-keygen -i -f puttykey.pub >> authorized_keys2
```

### 5.2 检查指纹

首次登录时，`ssh` 会询问是否将未知主机及其指纹存储在 `known hosts` 中。为了避免中间人攻击，服务器管理员可以向你发送服务器指纹，然后在首次登录时进行比较。使用 `ssh-keygen -l` 获取指纹（在服务器上）：

```
# ssh-keygen -l -f /etc/ssh/ssh_host_rsa_key.pub    # For RSA key
2048 61:33:be:9b:ae:6c:36:31:fd:83:98:b7:99:2d:9f:cd  /etc/ssh/ssh_host_rsa_key.pub
# ssh-keygen -l -f /etc/ssh/ssh_host_dsa_key.pub    # For DSA key (default)
2048 14:4a:aa:d9:73:25:46:6d:0a:48:35:c7:f4:16:d4:ee  /etc/ssh/ssh_host_dsa_key.pub
```

现在连接到此服务器的客户端可以验证自己是否连接到正确的服务器：

```
# ssh linda
The authenticity of host 'linda (192.168.16.54)' can't be established.
DSA key fingerprint is 14:4a:aa:d9:73:25:46:6d:0a:48:35:c7:f4:16:d4:ee.
Are you sure you want to continue connecting (yes/no)? yes
```

### 5.3 安全文件传输

一些简单命令：

```
# scp file.txt host-two:/tmp
# scp joe@host-two:/www/*.html /www/tmp
# scp -r joe@host-two:/www /www/tmp
```

在 `Konqueror` 或 `Midnight Commander` 中，可以使用地址 `fish://user@gate` 访问远程文件系统。但是实现非常慢。

此外，还可以使用基于 `SCP` 的文件系统客户端 `sshfs` 挂载远程文件夹。参见 `fuse sshfs`。

```
ssh_exchange_identification: Connection closed by remote host
```

出现此错误时，请在服务器上尝试以下操作：

```
echo 'SSHD: ALL' >> /etc/hosts.allow
/etc/init.d/sshd restart
```

### 5.4 隧道

`SSH` 隧道允许通过 `SSH` 连接转发或反向转发端口，从而保护流量并访问原本会被阻止的端口。这仅适用于 `TCP`。转发和反向的通用命名法为（另见 `ssh` 和 `NAT` 示例）：

```
# ssh -L localport:desthost:destport user@gate  # desthost as seen from the gate
# ssh -R destport:desthost:localport user@gate  # forwards your localport to destination
#   desthost:localport as seen from the client initiating the tunnel
# ssh -X user@gate   # To force X forwarding
```

这将连接到 `gate` 并将本地端口转发到主机 `desthost:destport`。请注意 `desthost` 是 `gate` 所见的目的主机，因此如果连接至 `gate`，则 `desthost` 为 `localhost`。可以同时转发多个端口。

#### 在 gate 上直接转发

假设我们想要访问在 `gate` 上运行的 `CVS`（端口 `2401`）和 `http`（端口 `80`）。这是最简单的示例，`desthost` 因此为 `localhost`，我们在本地使用端口 `8080` 而不是 `80`，这样就不需要 `root` 权限。一旦 `ssh` 会话打开，两个服务都可以通过本地端口访问。

```
# ssh -L 2401:localhost:2401 -L 8080:localhost:80 user@gate
```

#### Netbios 和远程桌面转发到第二台服务器

假设一台 Windows `smb` 服务器位于 `gate` 后面且未运行 `ssh`。我们需要访问 `smb` 共享以及对服务器的远程桌面。

```
# ssh -L 139:smbserver:139 -L 3388:smbserver:3389 user@gate
```

现在可以通过 `\\127.0.0.1\` 访问 `smb` 共享，但前提是本地共享被禁用，因为本地共享正在监听端口 `139`。

可以保留本地共享启用，为此我们需要创建一个具有新 IP 地址的新虚拟设备，通过该地址连接 `smb` 共享。此外，本地 `RDP` 已在 `3389` 上监听，因此我们选择 `3388`。对于此示例，让我们使用虚拟 IP `10.1.1.1`。

- 使用 `putty` 设置源端口=`10.1.1.1:139`。可以创建多个环回设备并进行隧道。在 Windows 2000 上，只有 `putty` 对我有效。在 Windows Vista 上，还需额外转发端口 `445` 除了端口 `139`。此外在 Vista 上，补丁 `KB942624` 会阻止端口 `445` 的转发，因此我不得不卸载 Vista 上的此补丁。
- 使用 `ssh.com` 客户端，禁用“仅允许本地连接”。由于 `ssh.com` 将绑定到所有地址，因此只能连接单个共享。

现在创建具有 IP `10.1.1.1` 的环回接口：



# 系统 -> 控制面板 -> 添加硬件
是的，硬件已连接
添加新硬件设备（在底部）。

# 安装我手动选择的硬件
网络适配器
`Microsoft`, `Microsoft Loopback Adapter`。

将假设备的 IP 地址配置为 `10.1.1.1` 掩码 `255.255.255.0`，无网关。

高级 -> WINS，启用 LMHosts 查找；禁用 TCP/IP 上的 NetBIOS。

# 启用 Microsoft 网络客户端
# 禁用 Microsoft 网络的文件和打印机共享。

我必须重启才能使其工作。现在使用 `\\10.1.1.1` 连接到 smb 共享，并远程桌面到 `10.1.1.1:3388`。

#### 调试

如果无法工作：

- 端口是否已转发：`netstat -an`？查看 `0.0.0.0:139` 或 `10.1.1.1:139`

- `telnet 10.1.1.1 139` 是否能连接？

- 你需要勾选“本地端口接受来自其他主机的连接”。

- 环回接口上是否已禁用“Microsoft 网络的文件和打印机共享”？

## 连接 NAT 后面的两个客户端

假设两个客户端位于一台 NAT 网关后面，客户端 `cliadmin` 需要连接到客户端 `cliuser`（目标端），两者都可以通过 SSH 登录到网关，并且都运行带有 `sshd` 的 Linux。只要网关上的端口大于 `1024`，你就不需要任何 root 权限。我们使用网关上的 `2022` 端口。另外，由于网关是在本地使用，因此不需要 `GatewayPorts` 选项。

在客户端 `cliuser` 上（从目标端到网关）：

```
# ssh -R 2022:localhost:22 user@gate      # forwards client 22 to gate:2022
```

在客户端 `cliadmin` 上（从主机到网关）：

```
# ssh -L 3022:localhost:2022 admin@gate      # forwards client 3022 to gate:2022
```

现在，管理员可以使用以下命令直接连接到客户端 `cliuser`：

```
# ssh -p 3022 admin@localhost      # local:3022 -> gate:2022 -> client:22
```

## 连接 NAT 后面的 VNC

假设需要从 NAT 后面访问一台 Windows 客户端，该客户端的 VNC 正在监听 `5900` 端口。

在客户端 `cliwin` 上连接到网关：

```
# ssh -R 15900:localhost:5900 user@gate
```

在客户端 `cliadmin` 上（从主机到网关）：

```
# ssh -L 5900:localhost:15900 admin@gate
```

现在，管理员可以直接连接到客户端 VNC：

```
# vncconnect -display :0 localhost
```

## 建立多跳 SSH 隧道

假设你无法直接通过 `ssh` 访问服务器，只能经由多个中间主机（例如由于路由问题）。有时仍然需要建立直接的客户端 - 服务器连接，例如使用 `scp` 复制文件，或转发 `smb`、`vnc` 等其他端口。一种方法是将多个隧道串联起来，沿着各跳将端口转发到服务器。这个“承载”端口只有在最后一次连接到服务器时才会到达最终目的地。

假设我们要通过两跳将 `ssh` 端口从客户端转发到服务器。隧道建立后，就可以从客户端直接连接到服务器（还可以再添加一个端口转发）。

在一个 shell 中创建隧道

`client -> host1 -> host2 -> server`，并打通 `5678` 隧道

```
client$ ssh -L5678:localhost:5678 host1      # 5678 is an arbitrary port for the tunnel
host1$ ssh -L5678:localhost:5678 host2      # chain 5678 from host1 to host2
host2$ ssh -L5678:localhost:22 server      # end the tunnel on port 22 on the server
```

在另一个 shell 中使用隧道

`client -> server`，通过隧道 `5678`

```
# ssh -p 5678 localhost      # connect directly from client to server
# scp -P 5678 myfile localhost:/tmp/      # or copy a file directly using the tunnel
# rsync -e 'ssh -p 5678' myfile localhost:/tmp/ # or rsync a file directly to the server
```

## 自动连接与保活脚本

我使用以下脚本的变体来保持机器通过反向 `ssh` 隧道可达。如果连接被关闭，它会被自动重建。你可以在同一行中添加多个 `-L` 或 `-R` 隧道。

```
#!/bin/sh
COMMAND="ssh -N -f -g -R 2022:localhost:22 colin@cb.vu"
pgrep -f -x "$COMMAND" > /dev/null 2>&1 || $COMMAND
exit 0
```

```
1 * * * * colin /home/colin/port_forward.sh      # crontab entry (here hourly)
```

## 6 使用 SSH 的 VPN

从 `4.3` 版本开始，OpenSSH 可以使用 `tun/tap` 设备加密隧道。这与其他基于 TLS 的 VPN 解决方案（如 `OpenVPN`）非常相似。SSH 的一个优势是不需要安装和配置额外软件。此外，隧道使用 SSH 认证，例如预共享密钥。缺点是封装通过 TCP 完成，这可能导致慢速链路上的性能不佳。而且，隧道依赖单一（易断的）TCP 连接。这种技术对于快速搭建基于 IP 的 VPN 非常有用。与单一 TCP 端口转发不同，这里没有限制，所有第三/四层协议（如 ICMP、TCP/UDP 等）都可以通过 VPN 转发。无论如何，`sshd_config` 文件中需要以下选项：

```
PermitRootLogin yes
PermitTunnel yes
```

### 6.1 单个点对点连接

这里，我们使用点对点隧道连接两台主机 `hclient` 和 `hserver`。连接从 `hclient` 发起至 `hserver`，并以 root 身份执行。隧道端点为 `10.0.1.1`（服务器）和 `10.0.1.2`（客户端），我们创建一个 `tun5` 设备（也可以是其他编号）。过程非常简单：

- 使用 SSH 的 `-w` 隧道选项进行连接

- 配置隧道的 IP 地址。分别在服务器和客户端上各配置一次。

#### 连接到服务器

连接在客户端发起，命令在服务器上执行。

#### 服务器为 Linux

```
cli># ssh -w5:5 root@hserver
srv># ifconfig tun5 10.0.1.1 netmask 255.255.255.252    # Executed on the server shell
```

#### 服务器为 FreeBSD

```
cli># ssh -w5:5 root@hserver
srv># ifconfig tun5 10.0.1.1 10.0.1.2                # Executed on the server shell
```

#### 配置客户端

在客户端上执行的命令：

```
cli># ifconfig tun5 10.0.1.2 netmask 255.255.255.252    # Client is on Linux
cli># ifconfig tun5 10.0.1.2 10.0.1.1                  # Client is on FreeBSD
```

现在两台主机已连接，并且可以使用隧道 IP 地址透明地通过任何第三/四层协议通信。

### 6.2 连接两个网络

除了上述 p2p 设置外，使用两台网关通过 SSH VPN 连接两个私有网络更为实用。例如，假设 `netA` 是 `192.168.51.0/24`，`netB` 是 `192.168.16.0/24`。过程与上述类似，我们只需要添加路由。仅当网关不是其网络的默认网关时，才需要在私有接口上激活 NAT。`192.168.51.0/24 (netA)|gateA <-> gateB|192.168.16.0/24 (netB)`

- 使用 SSH 的 `-w` 隧道选项进行连接。

- 配置隧道的 IP 地址。分别在服务器和客户端上各配置一次。

- 为两个网络添加路由。

- 如有必要，在网关的私有接口上激活 NAT。

该设置从 `netA` 中的 `gateA` 发起。

#### 从 gateA 连接到 gateB



连接从 `gateA` 发起，命令在 `gateB` 上执行。

### `gateB` 在 Linux 上

```
gateA# ssh -w5:5 root@gateB
gateB# ifconfig tun5 10.0.0.1 netmask 255.255.255.252  # Executed on the gateB shell
gateB# route add -net 192.168.51.0 netmask 255.255.255.0 dev tun5
gateB# echo 1 > /proc/sys/net/ipv4/ip_forward      # Only needed if not default gw
gateB# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

### `gateB` 在 FreeBSD 上

```
gateA# ssh -w5:5 root@gateB      # Creates the tun5 devices
gateB# ifconfig tun5 10.0.0.1 10.0.0.2   # Executed on the gateB shell
gateB# route add 192.168.51.0/24 10.0.0.1,2
gateB# sysctl net.inet.ip.forwarding=1   # Only needed if not default gw
gateB# natd -s -m -u -dynamic -n fxp0    # see NAT (page 17)
gateB# sysctl net.inet.ip.fw.enable=1
```

### 配置 `gateA`

在 `gateA` 上执行的命令：

#### `gateA` 在 Linux 上

```
gateA# ifconfig tun5 10.0.0.2 netmask 255.255.255.252
gateA# route add -net 192.168.16.0 netmask 255.255.255.0 dev tun5
gateA# echo 1 > /proc/sys/net/ipv4/ip_forward
gateA# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

#### `gateA` 在 FreeBSD 上

```
gateA# ifconfig tun5 10.0.0.2 10.0.0.1
gateA# route add 192.168.16.0/24 10.0.0.1,2
gateA# sysctl net.inet.ip.forwarding=1
gateA# natd -s -m -u -dynamic -n fxp0      # see NAT (page 17)
gateA# sysctl net.inet.ip.fw.enable=1
```

两个私有网络现在已通过 SSH VPN 透明连接。IP 转发和 NAT 设置只有在网关不是默认网关时才有必要。在这种情况下客户端将不知道如何转发响应，并且必须激活 `nat`。

## 7 RSYNC

`Rsync` 几乎可以完全取代 `cp` 和 `scp`，而且中断的传输可以高效地重新开始。尾部斜杠的存在与否具有不同的含义，`man` 手册很不错……这里有一些示例：

复制目录及其完整内容：

```
# rsync -a /home/colin/ /backup/colin/      # "archive" mode. e.g keep the same
# rsync -a /var/ /var_bak
# rsync -aR --delete --during /home/user/ /backup/   # use relative (see below)
```

与之前相同但通过网络并使用压缩。`Rsync` 默认使用 `SSH` 进行传输，如果已设置则会使用 `ssh` 密钥。使用与 `SCP` 相同的方式 "..."。典型的远程复制：

```
# rsync -axSzrv /home/user/ user@server:/backup/user/   # Copy to remote
# rsync -a 'user@server:My\ Documents' 'My\ Documents'   # Quote AND escape spaces for the remote sh
```

排除 `/home/user/` 内的任何 `tmp` 目录并保持相对文件夹层次结构，即远程目录将具有结构 `/backup/home/user/`。这通常用于备份。

```
# rsync -aZR --exclude=tmp/ /home/user/ user@server:/backup/
```

### 使用端口 20022 进行 ssh 连接：

```
# rsync -az -e 'ssh -p 20022' /home/colin/ user@server:/backup/colin/
```

使用 `rsync` 守护进程（使用“:”）速度要快得多，但不会通过 `ssh` 加密。`/backup` 的位置由 `/etc/rsyncd.conf` 中的配置定义。变量 `RSYNC_PASSWORD` 可以设置以避免手动输入密码的需要。

### — RSYNC —

```
# rsync -axSRz /home/ ruser@hostname::rmodule/backup/
# rsync -axSRz ruser@hostname::rmodule/backup/ /home/    # To copy back
```

一些重要选项：

+   `-a`, `--archive`      archive mode; same as `-rlptgoD` (no `-H`)
+   `-r`, `--recursive`    recurse into directories
+   `-R`, `--relative`     use relative path names
+   `-H`, `--hard-links`   preserve hard links
+   `-S`, `--sparse`       handle sparse files efficiently
+   `-x`, `--one-file-system`  don't cross file system boundaries
+   `--exclude=PATTERN`  exclude files matching PATTERN
+   `--delete-during`    receiver deletes during xfer, not before
+   `--delete-after`     receiver deletes after rtransfer, not before

## 7.1 Windows 上的 Rsync

`Rsync` 可通过 `cygwin` 在 Windows 上使用，或作为独立软件包打包在 `cwrsync`¹³ 中。这对于自动备份非常方便。安装其中之一（不要同时安装两个）并将路径添加到 Windows 系统变量中：# 控制面板 -> 系统 -> 高级选项卡，按钮 环境变量。编辑“Path”系统变量并添加已安装 `rsync` 的完整路径，例如 `C:\Program Files\cwRsync\bin` 或 `C:\cygwin\bin`。这样 `rsync` 和 `ssh` 命令就可以在 Windows 命令 shell 中使用。

### 公钥认证

`Rsync` 自动通过 `SSH` 隧道传输，因此使用服务器上的 `SSH` 认证。自动备份必须避免用户交互，为此可以使用 `SSH` 公钥认证，`rsync` 命令将无需密码运行。

以下所有命令都在 Windows 控制台中执行。在控制台中（开始 -> 运行 -> `cmd`）按 `SSH` 中所述创建并上传密钥，并根据需要更改“user”和“server”。如果文件 `authorized_keys2` 尚不存在，只需将 `id_dsa.pub` 复制到 `authorized_keys2` 并上传即可。

```
# ssh-keygen -t dsa -N ''          # Creates a public and a private key
# rsync user@server:.ssh/authorized_keys2 .  # Copy the file locally from the server
# cat id_dsa.pub >> authorized_keys2  # Or use an editor to add the key
# rsync authorized_keys2 user@server:.ssh/  # Copy the file back to the server
# del authorized_keys2               # Remove the local copy
```

现在用以下命令测试（在一行中）：



```
rsync -rv "//cygdrive/c/Documents and Settings/%USERNAME%/My Documents/" \
'user@server:My\ Documents/'
```

### 自动备份

使用批处理文件来自动化备份并将文件添加到计划任务中（程序 -> 附件 -> 系统工具 -> 计划任务）。例如创建文件 `backup.bat` 并替换 `user@server`。

```
@ECHO OFF
REM rsync the directory My Documents
SETLOCAL
SET CWRSYNCHOME=C:\PROGRAM FILES\CWRSYNC
SET CYGWIN=nontsec
SET CWOLDPATH=%PATH%
REM uncomment the next line when using cygwin
SET PATH=%CWRSYNCHOME%\BIN;%PATH%
echo Press Control-C to abort
rsync -av "//cygdrive/c/Documents and Settings/%USERNAME%/My Documents/" \
'user@server:My\ Documents/'
pause
```

## 8 SUDO

`Sudo` 是一种标准方法，可在不泄露 root 密码的情况下授予用户部分管理权限。在多用户环境且同时存在服务器和工作站的情况下，`Sudo` 非常有用。只需使用 `sudo` 调用命令：

```
# sudo /etc/init.d/dhcpd restart          # Run the rc script as root
# sudo -u sysadmin whoami                 # Run cmd as an other user
```

### 8.1 配置

`Sudo` 在 `/etc/sudoers` 中进行配置，且只能使用 `visudo` 进行编辑。基本语法是（列表以逗号分隔）：

```
user hosts = (runas) commands          # In /etc/sudoers
```

- `users` 一个或多个用户或 `%组`（如 `%wheel`）以获得权限

- `hosts` 主机列表（或 `ALL`）

- `runas` 命令规则可以作为其运行的用户列表（或 `ALL`）。它用 `( )` 括起来！

- `commands` 将作为 `root` 或作为 `(runas)` 运行的命令列表（或 `ALL`）

此外，这些关键字可以定义为别名，它们称为 `User_Alias`、`Host_Alias`、`Runas_Alias` 和 `Cmdn_Alias`。这对于大型设置很有用。下面是一个 `sudoers` 示例：

```
# cat /etc/sudoers
# Host aliases are subnets or hostnames.
Host_Alias  DMZ    = 212.118.81.40/28
Host_Alias  DESKTOP = work1, work2

# User aliases are a list of users which can have the same rights
User_Alias  ADMINS = colin, luca, admin
User_Alias  DEVEL  = joe, jack, julia
Runas_Alias DBA   = oracle, pgsql

# Command aliases define the full path of a list of commands
Cmd_Alias   SYSTEM = /sbin/reboot,/usr/bin/kill,/sbin/halt,/sbin/shutdown,/etc/init.d/
Cmd_Alias   PW     = /usr/bin/passwd [A-Z]*, !/usr/bin/passwd root # Not root pwd!
Cmd_Alias   DEBUG  = /usr/bin/tcpdump,/usr/bin/wireshark,/usr/bin/nmap

# The actual rules
root,ADMINS ALL = (ALL) NOPASSWD: ALL    # ADMINS can do anything w/o a password.
DEVEL   DESKTOP = (ALL) NOPASSWD: ALL    # Developers have full right on desktops
DEVEL   DMZ     = (ALL) NOPASSWD: DEBUG  # Developers can debug the DMZ servers.

# User sysadmin can mess around in the DMZ servers with some commands.
sysadmin DMZ    = (ALL) NOPASSWD: SYSTEM,PW,DEBUG
sysadmin ALL,!DMZ = (ALL) NOPASSWD: ALL  # Can do anything outside the DMZ.
%db a    ALL    = (DBA) ALL             # Group dba can run as database user.

# anyone can mount/unmount a cd-rom on the desktop machines
ALL     DESKTOP = NOPASSWD: /sbin/mount /cdrom,/sbin/umount /cdrom
```

## 9 加密文件

### 9.1 OpenSSL

#### 单个文件

加密和解密：

```
# openssl aes-128-cbc -salt -in file -out file.aes
# openssl aes-128-cbc -d -salt -in file.aes -out file
```

请注意，文件当然可以是 `tar` 归档。

#### tar 并加密整个目录

```
# tar -cf - directory | openssl aes-128-cbc -salt -out directory.tar.aes    # Encrypt
# openssl aes-128-cbc -d -salt -in directory.tar.aes | tar -x -f -          # Decrypt
```

#### tar zip 并加密整个目录

```
# tar -zcf - directory | openssl aes-128-cbc -salt -out directory.tar.gz.aes   # Encrypt
# openssl aes-128-cbc -d -salt -in directory.tar.gz.aes | tar -xz -f -         # Decrypt
```

- `-` 在 `aes-128-cbc` 后使用 `-k mysecretpassword` 可避免交互式密码请求。然而请注意，这非常不安全。

- `-` 使用 `aes-256-cbc` 代替 `aes-128-cbc` 可获得更强的加密。这也会使用更多 CPU。

### 9.2 GPG

`GnuPG` 以加密和签名电子邮件或任何数据而闻名。此外 `gpg` 还提供了一个高级密钥管理系统。本节仅涵盖文件加密，不涉及电子邮件使用、签名或 Web-Of-Trust。

最简单的加密是使用对称密码。在这种情况下，文件使用密码加密，任何知道密码的人都可以解密它，因此不需要密钥。`Gpg` 会在加密的文件名后添加扩展名 `".gpg"`。

```
# gpg -c file                         # Encrypt file with password
# gpg file.gpg                        # Decrypt file (optionally -o otherfile)
```

#### 使用密钥

更多细节请参阅 `GPG Quick Start`¹⁴ 和 `GPG/PGP Basics`¹⁵ 以及 `gnupg` 文档¹⁶ 等。

私钥和公钥是非对称加密的核心。需要记住的重要事项：

- `-` 你的公钥由他人用于加密文件，只有你作为接收者可以解密（甚至加密该文件的人也无法解密）。因此公钥旨在分发。

- `-` 你的私钥使用你的密码短语加密，并用于解密用你的公钥加密的文件。私钥必须保密。此外，如果密钥或密码短语丢失，则所有用你的公钥加密的文件也将丢失。

- `-` 密钥文件称为 `keyrings`，因为它们可以包含多个密钥。

首先生成一个密钥对。默认值即可，不过你至少需要输入你的全名和电子邮件，可选地输入注释。注释对于使用相同姓名和电子邮件创建多个密钥很有用。此外你应该使用“密码短语”，而不是简单的密码。

```
# gpg --gen-key                         # This can take a long time
```



密钥存储在 Unix 上的 `~/.gnupg/` 中，在 Windows 上通常存储在 `C:/Documents and Settings/%USERNAME%/Application Data/gnupg/`。

```
~/.gnupg/pubring.gpg        # Contains your public keys and all others imported
~/.gnupg/secring.gpg        # Can contain more than one private key
```

最常用选项的简短提醒：

- `-e` 加密数据
- `-d` 解密数据
- `-r NAME` 为收件人 `NAME` 加密（或 '全名' 或 'email@domain'）
- `-a` 创建密钥的 ascii 护甲输出
- `-o` 用作输出文件

示例中使用 'Your Name' 和 'Alice' 作为密钥，它们通过电子邮件或全名或部分名称引用。例如我可以使用 'Colin' 或 'c@cb.vu' 来引用我的密钥 `[Colin Barschel (cb.vu) <c@cb.vu>]`。

# 仅用于个人加密

无需导出/导入任何密钥，你已经拥有两者。

```
# gpg -e -r 'Your Name' file          # Encrypt with your public key
# gpg -o file -d file.gpg              # Decrypt. Use -o or it goes to stdout
```

## 使用密钥加密 - 解密

首先你需要导出你的公钥供他人使用。你还需要导入例如来自 Alice 的公钥来为她加密文件。你可以以简单的 ascii 文件处理密钥或使用公钥服务器。

例如 Alice 导出她的公钥而你导入它，你就可以为她加密文件。只有 Alice 才能解密它。

```
# gpg -a -o alicekey.asc --export 'Alice'     # Alice exported her key in ascii file.
# gpg --send-keys --keyserver subkeys.pgp.net KEYID  # Alice put her key on a server.
# gpg --import alicekey.asc                     # You import her key into your pubring.
# gpg --search-keys --keyserver subkeys.pgp.net 'Alice' # or get her key from a server.
```

一旦密钥导入，加密或解密文件就非常容易：

```
# gpg -e -r 'Alice' file          # Encrypt the file for Alice.
# gpg -d file.gpg -o file          # Decrypt a file encrypted by Alice for you.
```

### 密钥管理

```
# gpg --list-keys                     # list public keys and see the KEYIDS
The KEYID follows the '/' e.g. for: pub 1024D/D12B77CE the KEYID is D12B77CE
# gpg --gen-revoke 'Your Name'         # generate revocation certificate
# gpg --list-secret-keys               # list private keys
# gpg --delete-keys NAME               # delete a public key from local key ring
# gpg --delete-secret-key NAME         # delete a secret key from local key ring
# gpg --fingerprint KEYID              # Show the fingerprint of the key
# gpg --edit-key KEYID                 # Edit key (e.g sign or add/del email)
```

## 10 加密分区

`Linux with LUKS (p31)` | `Linux dm-crypt only (p32)` | `FreeBSD GELI (p32)` | `FBSD pwd only (p33)`

还有（许多）其他替代方法来加密磁盘，我在这里只展示我知道并使用的方法。请记住安全性只有在操作系统未被篡改时才有效。入侵者可以很容易地从键盘事件中记录密码。此外，当分区挂载时数据可以自由访问，在这种状态下无法阻止入侵者访问它。

### 10.1 Linux

这些说明使用 Linux `dm-crypt`（device-mapper）功能，可在 2.6 内核上使用。在此示例中，让我们加密分区 `/dev/sdc1`，它可以是任何其他分区或磁盘，或 USB 或使用 `losetup` 创建的文件基础分区。在这种情况下我们将使用 `/dev/loop0`。参见文件映像分区。设备映射器使用标签来标识分区。我们在此示例中使用 `sdc1`，但它可以是任何字符串。

#### 使用 LUKS 的 dm-crypt

`LUKS` 与 `dm-crypt` 具有更好的加密，并使同一个分区可以有多个密码或轻松更改密码。要测试 `LUKS` 是否可用，只需输入 `# cryptsetup --help`，如果没有关于 `LUKS` 的内容显示，请使用下面的 Without LUKS 说明。首先如有必要创建分区：`fdisk /dev/sdc`。

##### 创建加密分区

```
# dd if=/dev/urandom of=/dev/sdc1    # Optional. For paranoids only (takes days)
# cryptsetup -y luksFormat /dev/sdc1  # This destroys any data on sdc1
```

```
# cryptsetup luksOpen /dev/sdc1 sdcl
# mkfs.ext3 /dev/mapper/sdcl      # create ext3 file system
# mount -t ext3 /dev/mapper/sdcl /mnt
# umount /mnt
# cryptsetup luksClose sdcl        # Detach the encrypted partition
```

##### 挂载

```
# cryptsetup luksOpen /dev/sdc1 sdcl
# mount -t ext3 /dev/mapper/sdcl /mnt
```

##### 卸载

```
# umount /mnt
# cryptsetup luksClose sdcl
```

#### 不使用 LUKS 的 dm-crypt

```
# cryptsetup -y create sdcl /dev/sdc1      # or any other partition like /dev/loop0
# dmsetup ls                               # check it, will display: sdcl (254, 0)
# mkfs.ext3 /dev/mapper/sdcl               # This is done only the first time!
# mount -t ext3 /dev/mapper/sdcl /mnt
# umount /mnt/
# cryptsetup remove sdcl                   # Detach the encrypted partition
```

要重新挂载分区，请完全重复上述操作（不包括 `mkfs` 部分！）。如果密码不正确，`mount` 命令将失败。在这种情况下只需移除映射 `sdcl`（`cryptsetup remove sdcl`）并重新创建它。

### 10.2 FreeBSD

FreeBSD 两个流行的磁盘加密模块是 `gbde` 和 `geli`。我现在使用 `geli`，因为它更快并且也使用 crypto 设备进行硬件加速。参见 The FreeBSD handbook 第 18.6 章了解所有细节。`geli` 模块必须加载或编译到内核中：

```
options GEOM_ELI
device crypto                         # or as module:
# echo 'geom_eli_load="YES"' >> /boot/loader.conf   # or do: kldload geom_eli
```

#### 使用密码和密钥



我对典型的磁盘加密使用这些设置，它使用密码 AND 密钥来加密主密钥。也就是说你需要密码和生成的密钥 `/root/adl.key` 两者才能挂载分区。主密钥存储在分区内部且不可见。参见下面关于典型 USB 或文件基础映像的说明。

### 创建加密分区

```
# dd if=/dev/random of=/root/adl.key bs=64 count=1   # this key encrypts the master key
# geli init -s 4096 -K /root/adl.key /dev/adl        # -s 8192 is also OK for disks
# geli attach -k /root/adl.key /dev/adl              # DO make a backup of /root/adl.key
# dd if=/dev/random of=/dev/adl.eli bs=1m             # Optional and takes a long time
# newfs /dev/adl.eli                                  # Create file system
# mount /dev/adl.eli /mnt
```

### 挂载

```
# geli attach -k /root/adl.key /dev/adl
# fsck -ny -t ffs /dev/adl.eli        # In doubt check the file system
# mount /dev/adl.eli /mnt
```

### 卸载

卸载过程在关机时自动完成。

```
# umount /mnt
# geli detach /dev/ad1.eli
```

## `/etc/fstab`

加密分区可以通过 `/etc/fstab` 配置自动挂载。启动时将提示输入密码。本示例需要以下设置：

```
# grep geli /etc/rc.conf
geli_devices="ad1"
geli_ad1_flags="-k /root/ad1.key"
# grep geli /etc/fstab
/dev/ad1.eli    /home/private    ufs    rw    0    0
```

### 仅使用密码

仅使用密码而无需密钥来加密 U 盘或基于文件的镜像会更方便。这种情况下无需携带额外的密钥文件。流程与上面基本相同，只是没有密钥文件。让我们对 1 GB 的基于文件的镜像 `/cryptfile` 进行加密。

```
# dd if=/dev/zero of=/cryptfile bs=1M count=1000  # 1 GB file
# mdconfig -at vnode -f /cryptfile
# geli init /dev/md0      # encrypts with password only
# geli attach /dev/md0
# newfs -U -m 0 /dev/md0.eli
# mount /dev/md0.eli /mnt
# umount /dev/md0.eli
# geli detach md0.eli
```

现在可以在其他系统上仅凭密码挂载此镜像。

```
# mdconfig -at vnode -f /cryptfile
# geli attach /dev/md0
# mount /dev/md0.eli /mnt
```

## 11 SSL 证书

所谓的 SSL/TLS 证书是加密的公钥证书，由公钥和私钥组成。证书用于验证通信端点并加密数据。例如在 Web 服务器（https）或邮件服务器（imaps）上使用。

### 11.1 流程

- 我们需要一个证书颁发机构来签署我们的证书。此步骤通常由 Thawte、Verisign 等厂商提供，但我们也可以自行创建。

- 创建证书签名请求。该请求类似于未签名的证书（公开部分），并且已包含所有必要信息。证书请求通常发送给颁发机构厂商进行签名。此步骤也在本地机器上创建私钥。

- 使用证书颁发机构签署证书。

- 如有必要，将证书和密钥合并到单个文件中以供应用程序（Web 服务器、邮件服务器等）使用。

### 11.2 配置 OpenSSL

我们使用 `/usr/local/certs` 作为本示例的目录，请检查或根据你的设置编辑 `/etc/ssl/openssl.cnf`，以便知道文件将被创建在何处。以下是 `openssl.cnf` 的相关部分：

```
[ CA_default ]
dir        = /usr/local/certs/CA      # Where everything is kept
certs      = $dir/certs              # Where the issued certs are kept
```

```
crl_dir      = $dir/crl          # Where the issued crl are kept
database     = $dir/index.txt     # database index file.
```

确保目录存在或创建它们

```
# mkdir -p /usr/local/certs/CA
# cd /usr/local/certs/CA
# mkdir certs crl newcerts private
# echo "01" > serial          # Only if serial does not exist
# touch index.txt
```

如果你打算从厂商处获取已签名的证书，则只需要证书签名请求（CSR）。该 CSR 将由厂商签署，有效期有限（例如 1 年）。

### 11.3 创建证书颁发机构

如果你没有来自厂商的证书颁发机构，就必须自行创建。如果打算使用厂商签署请求，则此步骤不是必需的。要创建证书颁发机构（CA）：

```
# openssl req -new -x509 -days 730 -config /etc/ssl/openssl.cnf \
-keyout CA/private/cakey.pem -out CA/cacert.pem
```

### 11.4 创建证书签名请求

要创建新的证书（例如用于邮件服务器或 Web 服务器），首先使用其私钥创建请求证书。如果你的应用程序不支持加密的私钥（例如 UW-IMAP 不支持），则使用 `-nodes` 禁用加密。

```
# openssl req -new -keyout newkey.pem -new newreq.pem \
-config /etc/ssl/openssl.cnf
# openssl req -nodes -new -keyout newkey.pem -out newreq.pem \
-config /etc/ssl/openssl.cnf      # No encryption for the key
```

保留此生成的 CSR（`newreq.pem`），因为它可以在下次续期时再次签名，签名仅会限制证书的有效期。此过程同时创建了私钥 `newkey.pem`。

### 11.5 签署证书

证书请求必须由 CA 签署后才有效，此步骤通常由厂商完成。注意：在以下命令中将 "servername" 替换为你的服务器名称。

```
# cat newreq.pem newkey.pem > new.pem
# openssl ca -policy policy_anything -out servernamecert.pem \
-config /etc/ssl/openssl.cnf -infiles new.pem
# mv newkey.pem servernamekey.pem
```

现在 `servernamekey.pem` 是私钥，`servernamecert.pem` 是服务器证书。

### 11.6 创建联合证书

IMAP 服务器希望私钥和服务器证书在同一个文件中。一般来说，这样处理也更方便，但文件必须安全保存！Apache 也能很好地处理它。创建包含证书和密钥的 `servername.pem` 文件：

- 使用文本编辑器打开私钥（`servernamekey.pem`）并将私钥复制到 "`servername.pem`" 文件中。

- 对服务器证书（`servernamecert.pem`）执行相同的操作。

最终的 `servername.pem` 文件应如下所示：

```
-----BEGIN RSA PRIVATE KEY-----
MIICKXQIBAAK...qK5LqGqT3c9dU6fCr+WuSs6aejdEDDqBRQ
-----END RSA PRIVATE KEY-----
-----BEGIN CERTIFICATE-----
MIERzCCATC...iG9w0BAQQPADCBxTELMAKGA1UEBhMCREUx
-----END CERTIFICATE-----
```

我们现在在 `/usr/local/certs/` 目录中有以下内容：



- `CA/private/cakey.pem`（CA 服务器私钥）

- `CA/cacert.pem`（CA 服务器公钥）

- `certs/servernamekey.pem`（服务器私钥）

- `certs/servernamecert.pem`（服务器签名证书）

- `certs/servername.pem`（带私钥的服务器证书）

确保私钥安全！

### 11.7 查看证书信息

要查看证书信息，只需执行：

```
# openssl x509 -text -in servernamecert.pem      # View the certificate info
# openssl req -noout -text -in server.csr          # View the request info
# openssl s_client -connect cb.vu:443              # Check a web server certificate
```

## 12 CVS

服务器设置（p35）| CVS 测试（p36）| SSH 隧道（p37）| CVS 使用（p37）

### 12.1 服务器设置

#### 初始化 CVS

决定主仓库的存放位置，并创建根 `cvs` 目录。例如 `/usr/local/cvs`（以 root 身份）：

```
# mkdir -p /usr/local/cvs
# setenv CVSROOT /usr/local/cvs          # Set CVSROOT to the new location (local)
# cvs init                               # Creates all internal CVS config files
# cd /root
# cvs checkout CVSROOT                  # Checkout the config files to modify them
# cd CVSROOT
edit config (fine as it is)
# cvs commit config
cat >> writers                         # Create a writers file (optionally also readers)
colin
^D                                     # Use [Control][D] to quit the edit
# cvs add writers                       # Add the file writers into the repository
# cvs edit checkoutlist
# cat >> checkoutlist
writers
^D                                     # Use [Control][D] to quit the edit
# cvs commit                            # Commit all the configuration changes
```

如果你想要区分读写权限，可以添加一个 `readers` 文件。注意：切勿（永远不要）直接编辑主 CVS 中的文件，而应检出文件、修改后再提交。我们通过 `writers` 文件定义了写权限，就是这样做的。

此时有三种常用的访问 CVS 的方式。前两种不需要任何额外配置。关于如何使用它们，请参阅下面 `CVSROOT` 的示例：

- 直接本地访问文件系统。用户需要拥有足够的文件权限才能直接访问 CVS，除操作系统登录外，不需要进一步的身份验证。不过这仅在仓库位于本地时才有用。

- 通过 `ssh` 使用 `ext` 协议进行远程访问。任何拥有 `ssh` shell 账户且对 CVS 服务器具有读写权限的用户，都可以通过 `ssh` 直接使用 `ext` 访问 CVS，无需任何额外的隧道。这不需要在 CVS 上运行服务器进程。身份验证由 `ssh` 登录完成。

- 使用 `pserver` 进行远程访问（默认端口：2401/tcp）。对于较大的用户群，这是首选方式，因为用户由 CVS `pserver` 通过专用的密码数据库进行身份验证；因此不需要本地用户账户。此设置将在下面说明。

#### 使用 inetd 进行网络设置

只有在不需要网络访问时，CVS 才可以在本地运行。对于远程访问，守护进程 `inetd` 可以通过 `/etc/inetd.conf`（SuSE 上为 `/etc/xinetd.d/cvs`）中的以下行启动 `pserver`：

```
cvspserver    stream tcp nowait cvs /usr/bin/cvs    cvs \
--allow-root=/usr/local/cvs pserver
```

最好用防火墙阻止 `cvs` 端口从互联网访问，并使用 `ssh` 隧道远程访问仓库。

#### 独立认证

可以创建不属于操作系统（没有本地用户）的 `cvs` 用户。实际上，从安全角度来看，这很可能也是我们想要的。只需在 `CVSROOT` 目录中添加一个名为 `passwd` 的文件，其中包含用户的登录名和密码（以 `crypt` 格式）。这可以使用 Apache 的 `htpasswd` 工具完成。

注意：这个 `passwd` 文件是唯一必须在 `CVSROOT` 目录中直接编辑的文件。而且它不会被检出。更多信息请参阅 `htpasswd --help`。

```
# htpasswd -c passwd user1 password1   # -c creates the file
# htpasswd -b passwd user2 password2
```

现在在每行末尾添加 `:cvs`，告诉 `cvs` 服务器将用户切换为 `cvs`（或你的 `cvs` 服务器运行时所使用的任何用户）。如下所示：

```
# cat passwd
user1:xsfFjhU2Zu8Fuo:cvs
user2:vnefJ0SnnvToM:cvs
```

### 12.2 测试

以普通用户身份测试登录（例如在这里，就是我）：

```
# cvs -d :pserver:colin@192.168.50.254:/usr/local/cvs login
Logging in to :pserver:colin@192.168.50.254:2401/usr/local/cvs
CVS password:
```

#### CVSROOT 变量

这是一个环境变量，用于指定我们要进行操作的仓库位置。对于本地使用，只需将其设置为仓库目录即可。对于网络使用，必须指定传输协议。在 `csh/tcsh` shell 中，使用 `setenv CVSROOT string` 设置 `CVSROOT` 变量；在 `sh/bash` shell 中，使用 `export CVSROOT=string` 设置。

```
# setenv CVSROOT :pserver:<username>@<host>:/cvsdirectory
```

例如：

```
# setenv CVSROOT /usr/local/cvs                # Used locally only
# setenv CVSROOT :local:/usr/local/cvs         # Same as above
# setenv CVSROOT :ext:user@cvsserver:/usr/local/cvs  # Direct access with SSH
# setenv CVS_RSH ssh                            # For the ext access
# setenv CVSROOT :pserver:user@cvsserver.254:/usr/local/cvs  # network with pserver
```

登录成功后，就可以将新项目导入到仓库中：先 `cd` 到你的项目根目录。

```
cvs import <module name> <vendor tag> <initial tag>
cvs -d :pserver:colin@192.168.50.254:/usr/local/cvs import MyProject MyCompany START
```

其中 `MyProject` 是仓库中新项目的名称（稍后用于检出）。CVS 会将当前目录内容导入到新项目中。

要检出：

```
# cvs -d :pserver:colin@192.168.50.254:/usr/local/cvs checkout MyProject
```

或者

```
# setenv CVSROOT :pserver:colin@192.168.50.254:/usr/local/cvs
# cvs checkout MyProject
```

### 12.3 SSH tunneling for CVS



我们需要 2 个 shell 来完成此操作。在第一个 shell 中，我们通过 `ssh` 连接到 `cvs` 服务器并端口转发 `cvs` 连接。在第二个 shell 中，我们像它在本地运行一样正常使用 `cvs`。

on shell 1:

```
# ssh -L2401:localhost:2401 colin@cvs_server   # Connect directly to the CVS server. Or:
# ssh -L2401:cvs_server:2401 colin@gateway      # Use a gateway to reach the CVS
```

on shell 2:

```
# setenv CVSROOT :pserver:colin@localhost:/usr/local/cvs
# cvs login
Logging in to :pserver:colin@localhost:2401/usr/local/cvs
CVS password:
# cvs checkout MyProject/src
```

### 12.4 CVS commands and usage

#### Import

`import` 命令用于添加整个目录，必须从要导入的目录内运行。假设目录 `/devel/` 包含所有要导入的文件和子目录。CVS 上的目录名（模块）将称为 "`myapp`"。

```
# cvs import [options] directory-name vendor-tag release-tag
# cd /devel          # Must be inside the project to import it
# cvs import myapp Company_R1_0      # Release tag can be anything in one word
```

过了一段时间，又添加了新目录 `"/devel/tools/"`，它也需要导入。

```
# cd /devel/tools
# cvs import myapp/tools Company_R1_0
```

#### Checkout update add commit

```
# cvs co myapp/tools                # Will only checkout the directory tools
# cvs co -r R1_1 myapp              # Checkout myapp at release R1_1 (is sticky)
# cvs -q -d update -P                # A typical CVS update
# cvs update -A                      # Reset any sticky tag (or date, option)
# cvs add newfile                    # Add a new file
# cvs add -kb newfile                # Add a new binary file
# cvs commit file1 file2             # Commit the two files only
# cvs commit -m "message"            # Commit all changes done with a message
```

#### Create a patch

最好从与项目相关的开发工作目录，或从源目录内部创建和应用补丁。

```
# cd /devel/project
# diff -Naur olddir newdir > patchfile # Create a patch from a directory or a file
# diff -Naur oldfile newfile > patchfile
```

#### Apply a patch

有时有必要从补丁中剥离一个目录层级，这取决于补丁的创建方式。如果遇到困难，只需查看补丁的第一行并尝试 `-p0`、`-p1` 或 `-p2`。

```
# cd /devel/project
# patch --dry-run -p0 < patchfile      # Test the path without applying it
# patch -p0 < patchfile
# patch -p1 < patchfile                # strip off the 1st level from the path
```

## 13 SVN

`Server setup (p38)` | `SVN+SSH (p38)` | `SVN over http (p38)` | `SVN usage (p39)`

`Subversion (SVN)`¹⁸ 是一种版本控制系统，旨在成为 `CVS`（Concurrent Versions System）的继任者。概念与 `CVS` 相似，但许多不足之处得到了改进。另请参阅 `SVN` 书籍¹⁹。

### 13.1 Server setup

仓库的初始化相当简单（例如这里 `/home/svn/` 必须存在）：

```
# svnadmin create --fs-type fsfs /home/svn/project1
```

现在可以通过以下方式访问仓库：

- `file://` 通过 `svn` 客户端直接访问文件系统。这需要对文件系统具有本地权限。
- `svn://` 或 `svn+ssh://` 通过 `svnserve` 服务器进行远程访问（也通过 SSH）。这需要对文件系统具有本地权限（默认端口：2690/tcp）。
- `http://` 通过 apache 使用 webdav 进行远程访问。此方法不需要本地用户。

使用本地文件系统，现在可以导入然后检出现有项目。与 `CVS` 不同，不必 `cd` 到项目目录，只需给出完整路径即可：

```
# svn import /project1 file:///home/svn/project1/trunk -m 'Initial import'
# svn checkout file:///home/svn/project1
```

新的目录 "`trunk`" 只是约定，并非必需。

### Remote access with ssh

通过 `ssh` 访问仓库不需要特殊设置，只需将 `file://` 替换为 `svn+ssh/hostname`。例如：

```
# svn checkout svn+ssh://hostname/home/svn/project1
```

与本地文件访问一样，每个用户都需要对服务器具有 `ssh` 访问权限（使用本地账户）并且具有读写权限。此方法可能适合小型团队。所有用户可以属于一个 `subversion` 组，该组拥有仓库，例如：

```
# groupadd subversion
# groupmod -A user1 subversion
# chown -R root:subversion /home/svn
# chmod -R 770 /home/svn
```

### Remote access with http (apache)

通过 `http`（`https`）进行远程访问是大型用户组的唯一良好解决方案。此方法使用 apache 认证，而不是本地账户。这是一个典型但小的 apache 配置：

```
LoadModule dav_module modules/mod_dav.so
LoadModule dav_svn_module modules/mod_dav_svn.so
LoadModule authz_svn_module modules/mod_authz_svn.so    # Only for access control
```

```
<Location /svn>
# any "/svn/foo" URL will map to a repository /home/svn/foo
SVNParentPath /home/svn
AuthType Basic
AuthName "Subversion repository"
AuthzSVNAccessFile /etc/apache2/svn.acl
AuthUserFile /etc/apache2/svn-passwd
Require valid-user
</Location>
```

# — 有用命令 —

Apache 服务器需要对仓库有完全访问权限：

```
# chown -R www:www /home/svn
```

使用 `htpasswd` 创建用户：

```
# htpasswd -c /etc/svn-passwd user1  # -c creates the file
```

# 访问控制 `svn.acl` 示例



```
# Default it read access. "* =" would be default no access
[/]
* = r
[groups]
project1-developers = joe, jack, jane
# Give write access to the developers
[project1:]
@project1-developers = rw
```

## 13.2 SVN 命令及用法

另请参阅 Subversion 快速参考卡20。Tortoise SVN21 是一个不错的 Windows 界面。

#### Import

新的项目，即包含一些文件的目录，使用 `import` 命令导入到仓库中。`Import` 也用于向现有项目添加一个目录及其内容。

```
# svn help import                  # Get help for any command
# Add a new directory (with content) into the src dir on project1
# svn import /project1/newdir http://host.url/svn/project1/trunk/src -m 'add newdir'
```

#### 典型 SVN 命令

```
# svn co http://host.url/svn/project1/trunk          # Checkout the most recent version
# Tags and branches are created by copying
# svn mkdir http://host.url/svn/project1/tags/        # Create the tags directory
# svn copy -m "Tag rcl rel." http://host.url/svn/project1/trunk \ http://host.url/svn/project1/tags/1.0rc1
# svn status [--verbose]                              # Check files status into working dir
# svn add src/file.h src/file.cpp                     # Add two files
# svn commit -m 'Added new class file'                # Commit the changes with a message
# svn ls http://host.url/svn/project1/tags/           # List all tags
# svn move foo.c bar.c                                # Move (rename) files
# svn delete some_old_file                            # Delete files
```

## 14 有用命令

`less` (p39) | `vi` (p40) | `mail` (p40) | `tar` (p41) | `dd` (p41) | `screen` (p42) | `find` (p43) | 杂项 (p43)

### 14.1 less

`less` 命令在控制台上显示文本文档。它存在于大多数安装中。

```
# less unix toolbox.xhtml
```

一些重要命令是 (^N 代表 [control]-[N])：

- h H 显示良好的帮助
- f ^F ^V SPACE 向前移动一个窗口（或 N 行）。
- b ^B ESC-v 向后移动一个窗口（或 N 行）。
- F 永远向前；类似于 "tail -f"。
- /pattern 向前搜索第 (N) 个匹配行。
- ?pattern 向后搜索第 (N) 个匹配行。

20.http://www.cs.put.poznan.pl/csobaniec/Papers/svn-refcard.pdf

21.http://tortoisesvn.tigris.org

### 14.2 vi

`Vi` 存在于任何 Linux/Unix 安装中（不是 gentoo？），因此了解一些基本命令很有用。有两种模式：命令模式和插入模式。命令模式通过 [ESC] 访问，插入模式通过 i 访问。使用 : help 如果你迷路了。编辑器 nano 和 pico 通常也可用，使用起来更容易（在我看来）。

#### Quit

- `:w newfilename` 将文件保存为 newfilename
- `:wq` 或 `:x` 保存并退出
- `:q!` 不保存退出

#### 搜索和移动

- `/string` 向前搜索字符串
- `?string` 向后搜索字符串
- `n` 搜索字符串的下一个实例
- `N` 搜索字符串的上一个实例
- `{` 向后移动一个段落
- `}` 向前移动一个段落
- `1G` 移动到文件的第一行
- `nG` 移动到文件的第 n 行
- `G` 移动到文件的最后一行
- `:%s/OLD/NEW/g` 搜索并替换所有出现

#### 删除复制粘贴文本

- `dd` (`dw`) 剪切当前行（单词）
- `D` 剪切到行尾
- `x` 删除（剪切）字符
- `yy` (`yw`) 复制光标后的行（单词）
- `P` 在光标后粘贴
- `u` 撤销上次修改
- `U` 撤销当前行的所有更改

### 14.3 mail

`mail` 命令是读取和发送电子邮件的基础应用程序，通常已安装。要发送电子邮件，只需输入 "`mail user@domain`" 。第一行是主题，然后是邮件内容。用新行中的单个点 (.) 结束并发送邮件。示例：

```
# mail c@cb.vu
Subject: Your text is full of typos
"For a moment, nothing happened. Then, after a second or so,
nothing continued to happen."
.
EOT
#
```

这也可以通过管道工作：

```
# echo "This is the mail body" | mail c@cb.vu
```

这也是测试邮件服务器的一种简单方法。

- `n` 重复上一次搜索（第 N 次出现）。
- `N` 反向重复上一次搜索。
- `q` 退出

### 14.4 tar

命令 `tar`（tape archive）用于创建和提取文件和目录的归档。归档 `.tar` 是未压缩的，压缩归档的扩展名为 `.tgz` 或 `.tar.gz`（zip）或 `.tbz`（bzip2）。创建归档时不要使用绝对路径，你可能想在其他地方解包。一些典型命令如下：

#### Create

```
# cd /
# tar -cf home.tar home/      # archive the whole /home directory (c for create)
# tar -czf home.tgz home/      # same with zip compression
# tar -cjf home.tbz home/      # same with bzip2 compression
```

只包含树中的一个（或两个）目录，但保持相对结构。例如归档 `/usr/local/etc` 和 `/usr/local/www`，归档中的第一个目录应为 `local/`。

```
# tar -C /usr -czf local.tgz local/etc local/www
# tar -C /usr -xzf local.tgz   # To untar the local dir into /usr
# cd /usr; tar -xzf local.tgz  # Is the same as above
```

#### Extract

```
# tar -tzf home.tgz            # look inside the archive without extracting (list)
# tar -xf home.tar              # extract the archive here (x for extract)
# tar -xzf home.tgz             # same with zip compression (-xjf for bzip2 compression)
# tar --strip-components 1 -zxvf gallery2.tgz -C gallery/   # remove leading path gallery2 and extract into gallery
# tar -xjf home.tbz home/colin/file.txt   # Restore a single file
```



#### More advanced

```
# tar c dir/ | gzip | ssh user@remote 'dd of=dir.tgz' # arch dir/ and store remotely.
# tar cvf - ' .print ' | backup.tar                 # arch the current directory.
# tar -cf - -C /etc . | tar xpf - -C /backup/etc     # Copy directories
# tar -cf - -C /etc . | ssh user@remote tar xpf - -C /backup/etc   # Remote copy.
# tar -czf home.tgz --exclude '*.o' --exclude 'tmp/' home/
```

### 14.5 dd

程序 `dd`（disk dump or destroy disk or see the meaning of dd）用于复制分区和磁盘以及其他复制技巧。典型用法：

```
# dd if=<source> of=<target> bs=<byte size> conv=<conversion>
```

#### Important conv options:

- `notrunc`    do not truncate the output file, all zeros will be written as zeros.
- `noerror`    continue after read errors (e.g. bad blocks)
- `sync`       pad every input block with Nulls to ibs-size

默认字节大小为 512（一块）。MBR，即分区表所在的位置，在第一块上，磁盘的前 63 块为空。更大的字节大小复制更快但也需要更多内存。

#### Backup and restore

```
# dd if=/dev/hda of=/dev/hdc bs=16065b          # Copy disk to disk (same size)
# dd if=/dev/sda7 of=/home/root.img bs=4096 conv=notrunc,noerror # Backup /
# dd if=/home/root.img of=/dev/sda7 bs=4096 conv=notrunc,noerror # Restore /
# dd bs=1M if=/dev/ad0s3e | gzip -c > ad0s3e.gz   # Zip the backup
# gunzip -dc ad0s3e.gz | dd of=/dev/ad0s3e bs=1M   # Restore the zip
# dd bs=1M if=/dev/ad0s3e | gzip | ssh eedcoba@fry 'dd of=ad0s3e.gz' # also remote
# gunzip -dc ad0s3e.gz | ssh eedcoba@host 'dd of=/dev/ad0s3e bs=1M'
# dd if=/dev/ad0 of=/dev/ad2 skip=1 seek=1 bs=4k conv=noerror   # Skip MBR
# This is necessary if the destination (ad2) is smaller.
```

#### Recover

命令 `dd` 会读取分区的每一个块。出现问题时最好使用选项 `conv=sync,noerror`，这样 `dd` 会跳过坏块并在目标处写入零。因此重要的是将块大小设置为等于或小于磁盘块大小。1k 大小似乎是安全的，使用 `bs=1k` 设置。如果磁盘有坏扇区并且需要从分区恢复数据，使用 `dd` 创建映像文件，挂载映像并将内容复制到新磁盘。使用选项 `noerror`，`dd` 会跳过坏扇区并改写零，因此只有坏扇区中的数据会丢失。

```
# dd if=/dev/hda of=/dev/null bs=1m          # Check for bad blocks
# dd bs=1k if=/dev/hdal conv=sync,noerror,notrunc | gzip | ssh \ # Send to remote
# root@fry 'dd of=/dev/hdal.gz bs=1k'
# dd bs=1k if=/dev/hdal conv=sync,noerror,notrunc of=hda1.img   # Store into an image
# mount -o loop /hda1.img /mnt                 # Mount the image (page 13)
# rsync -aX /mnt/ /newdisk/                    # Copy on a new disk
# dd if=/dev/hda of=/dev/hda                   # Refresh the magnetic state
# The above is useful to refresh a disk. It is perfectly safe, but must be unmounted.
```

#### Delete

```
# dd if=/dev/zero of=/dev/hdc             # Delete full disk
# dd if=/dev/urandom of=/dev/hdc           # Delete full disk better
# kill -USR1 PID                            # View dd progress (Linux)
# kill -INFO PID                            # View dd progress (FreeBSD)
```

#### MBR tricks

MBR 包含引导加载程序和分区表，且大小为 512 字节。前 446 字节用于引导加载程序，字节 446 到 512 用于分区表。

```
# dd if=/dev/sda of=/mbr_sda.bak bs=512 count=1   # Backup the full MBR
# dd if=/dev/zero of=/dev/sda bs=512 count=1      # Delete MBR and partition table
# dd if=/mbr_sda.bak of=/dev/sda bs=512 count=1    # Restore the full MBR
# dd if=/mbr_sda.bak of=/dev/sda bs=446 count=1    # Restore only the boot loader
# dd if=/mbr_sda.bak of=/dev/sda bs=1 count=64 skip=446 seek=446 # Restore partition table
```

### 14.6 screen

`Screen`（必备）有两个主要功能：

- 在单个终端内运行多个终端会话。
- 启动的程序与真实终端解耦，因此可以在后台运行。真实终端可以关闭并稍后重新连接。

#### Short start example

使用以下命令启动 `screen`：

```
# screen
```

在 `screen` 会话中我们可以启动一个长时间运行的程序（如 `top`）。

```
# top
```

现在使用 Ctrl-a Ctrl-d 分离。重新连接终端：

```
# screen -R -D
```

详细说明：如果是正在运行的会话，则重新连接。如有必要先远程分离并注销。如果未运行则创建它并通知用户。或者：

```
# screen -x
```

以多显示模式连接到正在运行的 `screen`。控制台因此在多个用户之间共享。对团队协作/调试非常有用！

#### Screen commands (within screen)

所有 `screen` 命令均以 Ctrl-a 开始。

- Ctrl-a ? help and summary of functions

# — 有用命令 —

- Ctrl-a c 创建一个新窗口（终端）
- Ctrl-a Ctrl-n 和 Ctrl-a Ctrl-p 按编号在列表中切换到下一个或上一个窗口。
- Ctrl-a Ctrl-N 其中 N 为 0 到 9 的数字，切换到对应的窗口。
- Ctrl-a " 获取正在运行窗口的可导航列表
- Ctrl-a a 清除遗漏的 Ctrl-a
- Ctrl-a Ctrl-d 断开连接并在后台保持会话运行
- Ctrl-a x 使用密码锁定屏幕终端

当正在运行终端中的程序关闭并且你从终端注销时，`screen` 会话将被终止。

### 14.7 Find

一些重要选项：



- `-x` (在 BSD 上) `-xdev` (在 Linux 上) 保持在同一文件系统上（fstab 中的 dev）。

- `-exec cmd {} \;` 执行命令并用完整路径替换 `{}`

- `-iname` 类似 `-name` 但不区分大小写

- `-ls` 显示有关文件的信息（类似于 `ls -la`）

- `-size n` `n` 为 `+-n` (`k M G T P`)

- `-cmin n` 文件的状态最后更改于 `n` 分钟前。

```
# find . -type f ! -perm -444        # Find files not readable by all
# find . -type d ! -perm -111        # Find dirs not accessible by all
# find /home/user/ -cmin 10 -print    # Files created or modified in the last 10 min.
# find . -name "*. [ch]" | xargs grep -E 'expr' # Search 'expr' in this dir and below.
# find / -name "*.core" | xargs rm    # Find core dumps and delete them (also try core.*)
# find / -name "*.core" -print -exec rm {} \; # Other syntax
# Find images and create an archive, iname is not case sensitive. -r for append
# find . \( -iname "*.png" -o -iname "*.jpg" \) -print -exec tar -rf images.tar {} \;
# find . -type f -name "*.txt" ! -name README.txt -print # Exclude README.txt files
# find /var/ -size +10M -exec ls -lh {} \;    # Find large files > 10 MB
# find /var/ -size +10M -ls                    # This is simpler
# find . -size +10M -size -50M -print
# find /usr/ports/ -name work -type d -print -exec rm -rf {} \;  # Clean the ports
# Find files with SUID; those file are vulnerable and must be kept secure
# find / -type f -user root -perm -4000 -exec ls -l {} \;
```

使用 `xarg` 或 `exec` 时要小心，因为它可能或可能不遵守引号，并且当文件或目录包含空格时可能会返回错误结果。如有疑问，请改用 `"-print0 | xargs -0"` 而不是 `"| xargs"`。选项 `-print0` 必须是 `find` 命令中的最后一个。参见这个不错的 `find²²` 小教程。

```
# find . -type f | xargs ls -l        # Will not work with spaces in names
# find . -type f -print0 | xargs -0 ls -l  # Will work with spaces in names
# find . -type f -exec ls -l '{}' \;  # Or use quotes '{}' with -exec
```

### 14.8 杂项

```
# which command                     # Show full path name of command
# time command                       # See how long a command takes to execute
# time cat                            # Use time as stopwatch. Ctrl-c to stop
# set | grep $USER                    # List the current environment
# cal -3                              # Display a three month calendar
# date [+u][-utc][--universal] [MMDDhhmm[CC]YY[.ss]]
# date 10022155                       # Set date and time
# whatis grep                         # Display a short info on the command or word
# whereis java                        # Search path and standard directories for word
# setenv varname value                # Set env. variable varname to value (csh/tcsh)
# export varname="value"             # set env. variable varname to value (sh/ksh/bash)
# pwd                                 # Print working directory
# mkdir -p /path/to/dir               # no error if existing, make parent dirs as needed
# mkdir -p project/{bin,src,obj,doc/{html,man,pdf},debug/some/more/dirs}
# rmdir /path/to/dir                  # Remove directory
```

使用 `openssl` 检查文件哈希。这是对命令 `md5sum` 或 `sha1sum` 的不错替代方案（FreeBSD 使用 `md5` 和 `sha1`），这些命令并不总是安装的。

```
# openssl md5 file.tar.gz        # Generate an md5 checksum from file
# openssl sha1 file.tar.gz       # Generate an sha1 checksum from file
# openssl rmd160 file.tar.gz     # Generate a RIPEMD-160 checksum from file
```

## 15 安装软件

通常包管理器使用代理变量进行 `http/ftp` 请求。在 `.bashrc` 中：

```
export http_proxy=http://proxy_server:3128
export ftp_proxy=http://proxy_server:3128
```

### 15.1 列出已安装的软件包

```
# rpm -qa                # List installed packages (RH, SuSE, RPM based)
# dpkg -l                # Debian, Ubuntu
# pkg_info               # FreeBSD list all installed packages
# pkg_info -W smbd       # FreeBSD show which package smbd belongs to
# pkginfo                # Solaris
```

### 15.2 添加/删除软件

前端：SuSE 的 `yast2/yast`，Red Hat 的 `redhat-config-packages`。

```
# rpm -i pkgname.rpm     # install the package (RH, SuSE, RPM based)
# rpm -e pkgname          # Remove package
```

#### SuSE zypper (see doc and cheet sheet)²³



``` 
# zypper refresh         # Refresh repositorie
# zypper install vim     # Install the package vim
# zypper remove vim      # Remove the package vim
# zypper search vim      # Search packages with vim
# zypper update vim      # Search packages with vim
```

### Debian
```
# apt-get update         # First update the package lists
# apt-get install emacs  # Install the package emacs
# dpkg --remove emacs    # Remove the package emacs
# dpkg -S file           # find what package a file belongs to
```

### Gentoo
Gentoo 使用 `emerge` 作为其 "Portage" 包管理系统的核心。
```
# emerge --sync           # First sync the local portage tree
# emerge -u packagename   # Install or upgrade a package
# emerge -C packagename   # Remove the package
# revdep-rebuild          # Repair dependencies
```

### Solaris
`<cdrom>` 路径通常为 `/cdrom/cdrom0`。

#### 转换媒体
```
# pkgadd -d <cdrom>/Solaris_9/Product SUNWgtar
# pkgadd -d SUNWgtar          # Add downloaded package (bunzip2 first)
# pkg rm SUNWgtar             # Remove the package
```

### FreeBSD
```
# pkg_add -r rsync          # Fetch and install rsync.
# pkg_delete /var/db/pkg/rsync-xx  # Delete the rsync package
```
使用 `PACKAGESITE` 变量设置软件包的获取位置。例如：
```
# export PACKAGESITE=ftp://ftp.freebsd.org/pub/FreeBSD/ports/i386/packages/Latest/
# or ftp://ftp.freebsd.org/pub/FreeBSD/ports/i386/packages-6-stable/Latest/
```

#### FreeBSD ports
端口树 `/usr/ports/` 是一组可编译和安装的软件集合（参见 `man ports`）。端口通过 `portsnap` 程序进行更新。
```
# portsnap fetch extract      # Create the tree when running the first time
# portsnap update              # Update the port tree
# cd /usr/ports/net/rsync/     # Select the package to install
# make install distclean       # Install and cleanup (also see man ports)
# make package                 # Make a binary package of this port
# pkgdb -F                     # Fix the package registry database
```

### 15.3 库路径
由于复杂的依赖关系和运行时链接，程序很难复制到其他系统或发行版。然而对于依赖很少的小程序，缺失的库可以复制过去。运行时库（以及缺失的）通过 `ldd` 检查，并通过 `ldconfig` 管理。
```
# ldd /usr/bin/rsync          # List all needed runtime libraries
# ldconfig -n /path/to/libs/   # Add a path to the shared libraries directories
# ldconfig -m /path/to/libs/   # FreeBSD
# LD_LIBRARY_PATH              # The variable set the link library path
```

## 16 转换媒体
有时只需将视频、音频文件或文档转换为另一种格式。

### 16.1 文本编码
文本编码可能会完全错误，特别是当语言需要特殊字符如 àç 时。`iconv` 命令可以从一种编码转换到另一种编码。
```
# iconv -f <from_encoding> -t <to_encoding> <input_file>
# iconv -f ISO8859-1 -t UTF-8 -o file.input > file_utf8
# iconv -l                 # List known coded character sets
```
如果不使用 `-f` 选项，`iconv` 将使用本地字符集，如果文档显示正常，通常是可以的。

### 16.2 Unix - DOS 换行符
在 Unix shell 中将 DOS (CR/LF) 转换为 Unix (LF) 换行符，反之亦然。另请参阅 `dos2unix` 和 `unix2dos`，如果你有它们。
```
# sed 's/.$//' dosfile.txt > unixfile.txt          # DOS to UNIX
# awk '{sub(/\r$/,"" );print}' dosfile.txt > unixfile.txt  # DOS to UNIX
# awk '{sub(/$/,"\r");print}' unixfile.txt > dosfile.txt   # UNIX to DOS
```

### 16.3 PDF 转 Jpeg 并合并 PDF 文件
使用 `gs` (GhostScript) 将 PDF 文档转换为每个页面的 jpeg（或 png）图像。也可以使用 `convert` 和 `mogrify`（来自 ImageMagick 或 GraphicsMagick）更简洁。
```
# gs -dBATCH -dNOPAUSE -sDEVICE=jpeg -r150 -dTextAlphaBits=4 -dGraphicsAlphaBits=4 \ -dMaxStripSize=8192 -sOutputFile=unixxtoolbox.%d.jpg unixxtoolbox.pdf
# convert unixxtoolbox.pdf unixxtoolbox-#03d.png
# convert *.jpeg images.pdf      # Create a simple PDF with all pictures
# convert image000* -resize 120x120 -compress JPEG -quality 80 images.pdf
# mogrify -format png *.ppm      # convert all ppm images to png format
```
Ghostscript 也可以将多个 pdf 文件合并为一个文件。只有在 PDF 文件“表现良好”时才有效。
```
# gs -q -sPAPERSIZE=a4 -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOutputFile=all.pdf \ file1.pdf file2.pdf ...      # On Windows use '#' instead of '='
```

### 16.4 转换视频
使用 `mpeg4` 编解码器压缩佳能数码相机视频并修复糟糕的声音。
```
# mencoder -o videout.avi -oac mp3lame -ovc lavc -srate 11025 \ -channels 1 -af adv_force1 -lameopts preset=medium -lavcopts \ vcodec=mspmpe4v2:vbitrate=600 -mc 0 videoin.AVI
```
有关声音处理，请参阅 `sox`。

### 16.5 复制音频 CD



程序 `cdparanoia` 可以保存音频轨道（FreeBSD 端口在 `audio/cdparanoia/`），`oggenc` 可以编码为 Ogg Vorbis 格式，`lame` 转换为 mp3。

```
# cdparanoia -B                # Copy the tracks to wav files in current dir
# lame -b 256 in.wav out.mp3    # Encode in mp3 256 kb/s
# for i in *.wav; do lame -b 256 $i `basename $i .wav`.mp3; done
# oggenc in.wav -b 256 out.ogg  # Encode in Ogg Vorbis 256 kb/s
```

## 17 打印

### 17.1 使用 lpr 打印

```
# lpr unixtoolbox.ps            # Print on default printer
# export PRINTER=hp4600          # Change the default printer
# lpr -P hp4500 #2 unixtoolbox.ps # Use printer hp4500 and print 2 copies
# lpr -o Duplex=DuplexNoTumble ... # Print duplex along the long side
# lpr -o PageSize=A4,Duplex=DuplexNoTumble ...
```

```
# lpq                          # Check the queue on default printer
# lpq -l -P hp4500              # Queue on printer hp4500 with verbose
# lprm -                        # Remove all users jobs on default printer
# lprm -P hp4500 3186            # Remove job 3186. Find job nbr with lpq
# lpc status                     # List all available printers
# lpc status hp4500              # Check if printer is online and queue length
```

一些设备不是 PostScript 设备，用 pdf 文件喂给它们时会打印乱码。这可能通过以下方式解决：

```
# gs -dSAFER -dNOPAUSE -sDEVICE=deskjet -sOutputFile=\|lpr file.pdf
```

即使应用程序不支持，也可打印到 PDF 文件。在打印命令中使用 `gs` 代替 `lpr`。

```
# gs -q -sPAPERSIZE=a4 -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOutputFile=/path/file.pdf
```

## 18 数据库

### 18.1 PostgreSQL

#### 修改 root 或用户名密码

```
> psql -d template1 -U pgsql
> alter user pgsql with password 'pgsql_password';  # Use username instead of "pgsql"
```

#### 创建用户和数据库

命令 `createuser`、`dropuser`、`createdb` 和 `dropdb` 是方便的快捷方式，等同于 SQL 命令。新建用户为 `bob`，数据库为 `bobdb`；使用 `root` 以 `psql` 登录数据库超级用户：

```
# createuser -U pgsql -P bob          # -P will ask for password
# createdb -U pgsql -O bob bobdb       # new bobdb is owned by bob
# dropdb bobdb                         # Delete database bobdb
# dropuser bob                         # Delete user bob
```

通用数据库认证机制在 `pg_hba.conf` 中配置

#### 授予远程访问

文件 `$PGSQL_DATA_D/postgresql.conf` 指定绑定地址。通常 `listen_addresses = '*'` 用于 Postgres 8.x。

文件 `$PGSQL_DATA_D/pg_hba.conf` 定义访问控制。示例：

```
# TYPE  DATABASE  USER    IP-ADDRESS      IP-MASK         METHOD
host    bobdb     bob     212.117.81.42   255.255.255.255 password
host    all       all     0.0.0.0/0                   password
```

#### 备份和恢复

备份和恢复使用用户 `pgsql` 或 `postgres`。备份和恢复单个数据库：

```
# pg_dump --clean dbname > dbname_sql.dump
# psql dbname < dbname_sql.dump
```

备份和恢复所有数据库（包括用户）：

```
# pg_dumpall --clean > full.dump
# psql -f full.dump postgres
```

在这种情况下，恢复从数据库 `postgres` 开始，在重新加载空集群时更好。

### 18.2 MySQL

#### 修改 mysql root 或用户名密码

方法 1

```
# /etc/init.d/mysql stop
or
# killall mysqld
# mysqld --skip-grant-tables
# mysqladmin -u root password 'newpasswd'
# /etc/init.d/mysql start
```

#### 方法 2

```
# mysql -u root mysql
mysql> UPDATE USER SET PASSWORD=PASSWORD("newpassword") where user='root';
mysql> FLUSH PRIVILEGES;    # Use username instead of "root"
mysql> quit
```

#### 创建用户和数据库（参见 MySQL 文档²⁶）

```
# mysql -u root mysql
mysql> CREATE USER 'bob'@'localhost' IDENTIFIED BY 'pwd';  # create only a user
mysql> CREATE DATABASE bobdb;
mysql> GRANT ALL ON *.* TO 'bob'@'%' IDENTIFIED BY 'pwd';  # Use localhost instead of %
# to restrict the network access
mysql> DROP DATABASE bobdb;                  # Delete database
mysql> DROP USER bob;                        # Delete user
mysql> DELETE FROM mysql.user WHERE user='bob and host='hostname';  # Alt. command
mysql> FLUSH PRIVILEGES;
```

#### 授予远程访问

远程访问通常允许用于某个数据库，而非所有数据库。文件 `/etc/my.cnf` 包含绑定 IP 地址。通常注释掉行 `bind-address = out`。

```
# mysql -u root mysql
mysql> GRANT ALL ON bobdb.* TO bob@'xxx.xxx.xxx.xxx' IDENTIFIED BY 'PASSWORD';
mysql> REVOKE GRANT OPTION ON foo.* FROM bar@'xxx.xxx.xxx.xxx';
mysql> FLUSH PRIVILEGES;                    # Use 'hostname' or also '%' for full access
```

#### 备份和恢复

备份和恢复单个数据库：



```
# mysqldump -u root -psecret --add-drop-database dbname > dbname_sql.dump
# mysql -u root -psecret -D dbname < dbname_sql.dump
```

备份和恢复所有数据库：

```
# mysqldump -u root -psecret --add-drop-database --all-databases > full.dump
# mysql -u root -psecret < full.dump
```

这里的 `secret` 是 `mysql` `root` 密码，`-p` 后没有空格。当单独使用 `-p` 选项（无密码）时，密码会在命令行提示输入。

### 18.3 SQLite

`SQLite`²⁷ 是一个小型强大、独立、免服务器、零配置的 SQL 数据库。

#### 转储和恢复

转储和恢复 SQLite 数据库可能很有用。例如你可以编辑转储文件以更改列属性或类型，然后恢复数据库。这比处理 SQL 命令更容易。使用命令 `sqlite3` 用于 3.x 数据库。

```
# sqlite database.db .dump > dump.sql                # dump
# sqlite database.db < dump.sql                       # restore
```

#### 转换 2.x 到 3.x 数据库

```
sqlite database_v2.db .dump | sqlite3 database_v3.db
```

## 19 磁盘配额

磁盘配额允许限制用户或（或组成员）可使用的磁盘空间量和/或文件数量。配额按文件系统分配，由内核强制执行。

### 19.1 Linux 设置

通常需要安装配额工具包，它包含命令行工具。在 `fstab` 中激活用户配额并重新挂载分区。如果分区繁忙，则必须关闭所有被锁定的文件，或必须重新启动系统。将 `usrquota` 添加到 `fstab` 挂载选项中，例如：

```
/dev/sda2   /home   reiserfs   rw,acl,user_xattr,usrquota 1 1
# mount -o remount /home
# mount                 # 检查 usrquota 是否激活，否则重启
```

使用 `quotacheck` 初始化 `quota.user` 文件。

```
# quotacheck -vum /home
# chmod 644 /home/aquota.user   # 让用户自行检查其配额
```

使用提供的脚本（例如 SuSE 上的 `/etc/init.d/quotad`）或使用 `quotaon` 激活配额：

```
quotaon -vu /home
```

使用以下命令检查配额是否激活：

```
quota -v
```

### 19.2 FreeBSD 设置

配额工具是基本系统的一部分，然而内核需要选项 `quota`。如果没有，则添加它并重新编译内核。

```
options QUOTA
```

与 Linux 相同，将配额添加到 `fstab` 选项中（`userquota`，而不是 `usrquota`）：

```
/dev/ad0s1d   /home   ufs   rw,noatime,userquota   2   2
# mount /home              # 重新挂载分区
```

在 `/etc/rc.conf` 中启用磁盘配额并启动配额。

```
# grep quotas /etc/rc.conf
enable_quotas="YES"        # 启动时打开配额（或 NO）。
check_quotas="YES"         # 启动时检查配额（或 NO）。
# /etc/rc.d/quota start
```

### 19.3 分配配额限制

默认情况下配额不受限制（设为 0）。限制使用 `edquota` 为单个用户设置。配额也可以复制给多个用户。不同配额实现的文件结构不同，但原理相同：块和 inode 的值可以受限。只更改 `soft` 和 `hard` 的值。如果未指定，块为 1k。宽限期使用 `edquota -t` 设置。例如：

```
# edquota -u colin
```

#### Linux

用户 `colin`（`uid` 1007）的磁盘配额：

Filesystem   blocks   soft   hard   inodes   soft   hard

`/dev/sda8`    108      1000   2000   1        0      0

#### FreeBSD

```
Quotas for user colin:
/home: kbytes in use: 504184, limits (soft = 700000, hard = 800000)
    inodes in use: 1792, limits (soft = 0, hard = 0)
```

#### 多用户

命令 `edquota -p` 用于将配额复制给其他用户。例如将参考配额复制给所有用户：

```
# edquota -p refuser `awk -F: '$3 > 499 {print $1}' /etc/passwd`
# edquota -p refuser user1 user2   # 复制给 2 个用户
```

#### 检查

用户只需输入 `quota` 即可检查其配额（`quota.user` 文件必须可读）。`root` 可以检查所有配额。

```
# quota -u colin                # 检查用户的配额
# repquota /home                # 分区的完整报告，针对所有用户
```

## 20 Shell

大多数 Linux 发行版使用 `bash` shell，而 BSD 使用 `tcsh`，`bourne shell` 仅用于脚本。过滤器非常有用，可以通过管道连接：

- `grep` 模式匹配

- `sed` 搜索并替换字符串或字符

- `cut` 从标记打印特定列

- `sort` 按字母或数字排序

- `uniq` 从文件中删除重复行

例如一次性全部使用：

```
# ifconfig | sed 's/ / /g' | cut -d" " -f1 | uniq | grep -E "[a-z0-9]+" | sort -r
# ifconfig | sed '/inet addr:/!d;s/.*//.*/'|sort -t. -k1,1n -k2,2n -k3,3n -k4,4n
```

`sed` 模式中的第一个字符是一个制表符。要在控制台上写入制表符，请使用 `ctrl-v ctrl-tab`。

### 20.1 bash

`bash` 和 `sh` 的重定向和管道：

```
# cmd1 > file                 # 将 stdout 重定向到文件。
# cmd2 > file                 # 将 stderr 重定向到文件。
# cmd1 >> file                # 将 stdout 重定向并追加到文件。
# cmd1 <> file                # 将 stdout 和 stderr 都重定向到文件。
# cmd1 >file 2>&1             # 将 stderr 重定向到 stdout，然后重定向到文件。
# cmd1 | cmd2                 # 将 stdout 管道传输到 cmd2
# cmd1 2>&1 | cmd2            # 将 stdout 和 stderr 管道传输到 cmd2
```

在 `~/.bashrc` 中修改你的配置（也可以是 `~/.bash_profile`）。以下条目很有用，使用 `". ~/.bashrc"` 重新加载。使用 `cygwin` 时使用 `~/.bash_profile`；使用 `rxvt` 时使用 `shift + 左键` 粘贴。



```
# in .bashrc
bind "\e[A":history-search-backward  # 使用上下箭头搜索
bind "\e[B":history-search-forward    # 历史记录。非常有用！
set -o emacs                         # 在 bash 中设置 emacs 模式（见下文）
set bell-style visible               # 不要蜂鸣，颜色反转
# 设置一个漂亮的提示符，如 [user@host]/path/todir>
PS1="\[\033[1;30m\]\[\033[1;34m\]u@\[\033[1;30m\]"
PS1="$PS1\[\033[0;33m\]\w\[\033[1;33m\]1\[\033[0;37m\]"
PS1="$PS1\w\[\033[1;30m\]>\[\033[0m\]"
# 要检查当前活动的别名，只需输入 alias
alias ls='ls -af'                    # 追加指示符（其中之一 */=>@l）
```

```
alias ll='ls -AFls'
alias la='ls -all'
alias ..='cd ..'
alias ...='cd ../..'
export HISTFILESIZE=5000      # Larger history
export CLICOLOR=1             # Use colors (if possible)
export LSCOLORS=ExGxFxdxCxDxBxBxExEx
```

### 20.2 tcsh

`tcsh` 和 `csh` 的重定向和管道（简单的 `>` 和 `>>` 与 `sh` 相同）：

```
# cmd >& file                # Redirect both stdout and stderr to file.
# cmd >>& file               # Append both stdout and stderr to file.
# cmd1 | cmd2                # pipe stdout to cmd2
# cmd1 |& cmd2               # pipe stdout and stderr to cmd2
```

`csh`/`tcsh` 的设置保存在 `~/.cshrc` 中，使用 `"source .cshrc"` 重新加载。示例：

```
# in .cshrc
alias ls      'ls -aF'
alias ll      'ls -aFls'
alias la      'ls -all'
alias ..      'cd ..'
alias ...     'cd ../..'
set prompt    = "!%n%b@%m%b:%~%#"  # like user@host/path/todir>
set history   = 5000
set savehist  = ( 6000 merge )
set autolist  # Report possible completions with tab
set visiblebell               # Do not beep, inverse colors
```

```
# Bindkey and colors
bindkey -e    Select Emacs bindings   # Use emacs keys to edit the command prompt
bindkey ^k    up history-search-backward # Use up and down arrow to search
bindkey ^k    down history-search-forward
setenv CLICOLOR 1                # Use colors (if possible)
setenv LSCOLORS ExGxFxdxCxDxBxBxExEx
```

`Emacs` 模式允许你使用 `Emacs` 键快捷键来修改命令行提示符。这非常有用（不仅对于 `Emacs` 用户）。最常用的命令有：

- `C-a`    将光标移动到行首
- `C-e`    将光标移动到行尾
- `M-b`    将光标向后移动一个词
- `M-f`    将光标向前移动一个词
- `M-d`    剪切下一个词
- `C-w`    剪切上一个词
- `C-u`    剪切光标前所有内容
- `C-k`    剪切光标后所有内容（行的剩余部分）
- `C-y`    粘贴最后一次剪切的内容（直接粘贴）
- `C-_`    撤销

注意：`C-` 表示按住 `Control` 键，`M-` 表示按住 `Meta` 键（通常是 `Alt` 或 `Esc` 键）。

## 21 脚本

基础（第52页） | 脚本示例（第53页） | `awk`（第53页） | `sed`（第53页） | 正则表达式（第53页） | 常用命令（第54页）

`Bourne shell`（`/bin/sh`）存在于所有 `Unix` 安装中，用该语言编写的脚本（相当）可移植；`man 1 sh` 是一个很好的参考。

### 21.1 基础

#### 变量和参数

使用 `variable=value` 进行赋值，使用 `$variable` 获取内容。

```
MESSAGE="Hello World"          # Assign a string
PI=3.1415                        # Assign a decimal number
N=8
TWON=`expr $N * 2`               # Arithmetic expression (only integers)
TWON=$(($N * 2))                 # Other syntax
TWOP1=`echo "$PI * 2" | bc -l`  # Use bc for floating point operations
ZERO=`echo "c($PI/4)-sqrt(2)/2" | bc -l`
```

命令行参数如下：

```
$0, $1, $2, ...                  # $0 is the command itself
$#                               # The number of arguments
$*                               # All arguments (also $0)
```

#### 特殊变量

```
$$                               # The current process ID
$?                               # exit status of last command
command
if [ $? != 0 ]; then
    echo "command failed"
fi
mypath=`pwd`
mypath=$mypath//file.txt
echo ${mypath##*/}                # Display the filename only
echo ${mypath%.*}                 # Full path without extension
var2=${var:=string}               # Use var if set, otherwise use string
                                 # assign string to var and then to var2.
```

#### 结构

```
for file in `ls`
do
    echo $file
done

count=0
while [ $count -lt 5 ]; do
    echo $count
    sleep 1
    count=$(($count + 1))
done

myfunction() {
    find . -type f -name "*,$1" -print   # $1 is first argument of the function
}
myfunction "txt"
```

#### 生成文件

```
MYHOME=/home/colin
cat > testhome.sh << _EOF
# All of this goes into the file testhome.sh
if [ -d "$MYHOME" ]; then
    echo $MYHOME exists
else
    echo $MYHOME does not exist
fi
_EOF
sh testhome.sh
```

### 21.2 Bourne 脚本示例

作为一个小例子，用于从本 `xhtml` 文档创建 `PDF` 小册子的脚本：



```sh
#!/bin/sh
# This script creates a book in pdf format ready to print on a duplex printer
if [ $# -ne 1 ]; then          # Check the argument
echo 1>&2 "Usage: $0 HtmlFile"
exit 1                         # non zero exit if error
fi

file=$1                        # Assign the filename
fname=${file%.*}               # Get the name of the file only
fext=${file##*.}               # Get the extension of the file

prince $file -o $fname.pdf     # from www.princexml.com
pdf tops -paper A4 -noshrink $fname.pdf $fname.ps # create postscript booklet
cat $fname.ps | psbook|psnup -Pa4 -2 | pstops -b "2:0,1U(2cm,29.7cm)" > $fname.book.ps

ps2pdf13 -sPAPERSIZE=a4 -sAutoRotatePages=None $fname.book.ps $fname.book.pdf
# use #a4 and #None on Windows!
exit 0                         # exit 0 means successful
```

### 21.3 一些 awk 命令

`awk` 对于字段剥离很有用，像 `cut` 但功能更强大。 在本文件中搜索其他示例。 例如请参阅 `gnulamp.com` 和 `awk` 的 one-liners 以获取一些不错的示例。

```
awk '{ print $2, $1 }' file                # Print and inverse first two columns
awk '{printf "%5d : %s\n", NR,$0}' file   # Add line number left aligned
awk '{printf FNR "\t" $0}' files          # Add line number right aligned
awk NF test.txt                             # remove blank lines (same as grep '.')
awk 'length > 80'                           # print line longer than 80 char
```

### 21.4 一些 sed 命令

这里是单行代码宝库²⁸。 以及 `sed` 的一个不错的介绍和教程²⁹。

```
sed 's/string1/string2/g'                 # Replace string1 with string2
sed -i 's/wroong/wrong/g' *.txt            # Replace a recurring word with g
sed 's/(.*)/\1/2/g'                       # Modify anystring1 to anystring2
sed '/<p>/,/<\/p>/d' t.xhtml              # Delete lines that start with <p>
                                            # and end with </p>
sed '/ *#/d; / *$/d'                       # Remove comments and blank lines
sed 's/[ \t]*$//'                         # Remove trailing spaces (use tab as \t)
sed 's/^\[ \t\]*//; s/[ \t]*$//'        # Remove leading and trailing spaces
sed 's/^[^\t]/[&]/'                       # Enclose first char with [] top->[]top
sed = file | sed 'N;s/\n/\t/' > file.num # Number lines on a file
```

### 21.5 正则表达式

### 21.6 一些有用的命令

以下命令可用于脚本中或作为单行命令。

```
sort -t . -k1,1n -k2,2n -k3,3n -k4,4n        # Sort IPv4 ip addresses
echo 'Test' | tr '[a-z]' '[A-Z]'                 # Case conversion
echo foo.bar | cut -d . -f 1                     # Returns foo
PID=$(ps auxw | grep script.sh | grep bin | awk '{print $1}')   # PID of a running script
PID=$(ps auxw | grep [p]ing | awk '{print $1}')    # PID of ping (w/o grep pid)
IP=$(ifconfig $INTERFACE | sed '/inet addr://;s/;/ /;s/.*//' )   # Linux
IP=$(ifconfig $INTERFACE | sed '/inet /;s/.*//;s/.*//')   # FreeBSD
if [ `diff file1 file2 | wc -l` != 0 ]; then ... fi   # File changed?
cat /etc/master.passwd | grep -v root | grep -v '.*' | awk -F':' '{ printf("%s:%s\n", $1, $2) }' > /usr/local/etc/apache2/passwd   # Create http passwd
testuser=$(cat /usr/local/etc/apache2/passwd | grep -v \ )   # Check user in passwd
root | grep -v ^: | awk -F':' '{ printf("%s\n", $1) }' | grep 'user$'   
:() { :|: & };   # bash fork bomb. Will kill your machine
tail +2 file > file2                              # remove the first line from file
```

我使用这个小技巧一次更改许多文件的扩展名。 例如从 `.cxx` 到 `.cpp`。 先在没有 `| sh` 结尾的情况下测试它。 你也可以使用已安装的 `rename` 命令来完成。 或者使用 `bash` 内置命令。

```
# ls *.cxx | awk -F . '{print "mv "$0" "$1".cpp"}' | sh
# ls *.c sed "s/.*/cp & &.(date +%Y%m%d)/" | sh # e.g. copy *.c to *.c.20080401
# rename .cxx .cpp *.cxx                          # Rename all .cxx to cpp
# for i in *.cxx; do mv $i ${i%.cxx}.cpp; done    # with bash builtins
```

## 22 编程

### 22.1 C 基础



```
strcpy(newstr,str)                          /* copy str to newstr */
expr1 ? expr2 : expr3                      /* if (expr1) expr2 else expr3 */
x = (y > z) ? y : z;                        /* if (y > z) x = y; else x = z; */
int a[]={0,1,2};                            /* Initialized array (or a[3]={0,1,2}; */
int a[2][3]={{1,2,3},{4,5,6}};               /* Array of array of ints */
int i = 12345;                              /* Convert in i to char str */
char str[10];
sprintf(str, "%d", i);
```

### 22.2 C 示例

一个最小的 c 程序 `simple.c`：

```
#include <stdio.h>
main() {
    int number=42;
    printf("The answer is %i\n", number);
}
```

### 编译方法：

```
# gcc simple.c -o simple
# ./simple
The answer is 42
```

### 22.3 C++ 基础

```
*pointer                                 // Object pointed to by pointer
&obj                                     // Address of object obj
obj.x                                    // Member x of class obj (object obj)
pobj->x                                  // Member x of class pointed to by pobj
                                         // (*pobj).x and pobj->x are the same
```

### 22.4 C++ 示例

作为一个稍微更现实的 C++ 程序：一个类拥有自己的头文件 `IPv4.h` 和实现文件 `IPv4.cpp`，以及一个使用该类功能的程序。该类将整数格式的 IP 地址转换为已知的四段格式。

#### IPv4 类

#### `IPv4.h`：

```
#ifndef IPV4_H
#define IPV4_H
#include <string>

namespace GenericUtils {    // create a namespace
class IPv4 {                // class definition
public:
    IPv4(); ~IPv4();
    std::string IPint_to_IPquad(unsigned long ip);// member interface
};
} //namespace GenericUtils
#endif // IPV4_H
```

#### `IPv4.cpp`：

```
#include "IPv4.h"
#include <string>
#include <sstream>
using namespace std;                // use the namespaces
using namespace GenericUtils;

IPv4::IPv4() {}                     // default constructor/destructor
IPv4::~IPv4() {}
string IPv4::IPint_to_IPquad(unsigned long ip) {    // member implementation
    ostringstream ipstr;            // use a stringstream
    ipstr << ((ip &0xFF000000) >> 24)    // Bitwise right shift
          << "." << ((ip &0x00FF0000) >> 16)
          << "." << ((ip &0x0000FF00) >> 8)
          << "." << ((ip &0x000000FF));
    return ipstr.str();
}
```

#### 程序 `simplecpp.cpp`

```
#include "IPv4.h"
#include <iostream>
#include <string>
using namespace std;
int main (int argc, char* argv[]) {
    string ipstr;                   // define variables
    unsigned long ipint = 1347861486;   // The IP in integer form
    GenericUtils::IPv4 iputils;     // create an object of the class
    ipstr = iputils.IPint_to_IPquad(ipint);    // call the class member
    cout << ipint << " = " << ipstr << endl;   // print the result

    return 0;
}
```

#### 编译并执行：

```
# g++ -c IPv4.cpp simplecpp.cpp      # Compile in objects
# g++ IPv4.o simplecpp.o -o simplecpp.exe    # Link the objects to final executable
# ./simplecpp.exe
1347861486 = 80.86.187.238
```

使用 `ldd` 检查可执行文件使用了哪些库以及它们的位置。也可用于检查共享库是否缺失或可执行文件是否为静态链接。

### 22.5 简单 Makefile

下面展示了多源程序的最小 Makefile。包含指令的行*必须以制表符开头！* 反斜杠 `\` 可用于截断长行。

```
CC = g++
CFLAGS = -O
OBJS = IPv4.o simplecpp.o

simplecpp: ${OBJS}
	${CC} -o simplecpp ${CFLAGS} ${OBJS}
clean:
	rm -f ${TARGET} ${OBJS}
```

```
# ldd /sbin/ifconfig          # list dynamic object dependencies
# ar rcs staticlib.a *.o      # create static archive
# ar t staticlib.a            # print the objects list from the archive
# ar x /usr/lib/libc.a version.o  # extract an object file from the archive
# nm version.o                # show function members provided by object
```

## 23 在线帮助

### 23.1 文档

- Linux Documentation          en.tldp.org

- Linux Man Pages              www.linuxmanpages.com

- Linux commands directory     www.oreillynet.com/linux/cmd

- Linux doc man howtos         linux.die.net

- FreeBSD Handbook             www.freebsd.org/handbook

- FreeBSD Man Pages            www.freebsd.org/cgi/man.cgi

- FreeBSD user wiki            www.freebsdwiki.net

- Solaris Man Pages            docs.sun.com/app/docs/coll/40.10

### 23.2 其他 Unix/Linux 参考



# Unix/Linux 参考资源

- Rosetta Stone for Unix `bhami.com/rosetta.html` (a Unix command translator)
- Unix guide cross reference `unixguide.net/unixguide.shtml`
- Linux commands line list `www.linuxcmd.org`
- Short Linux reference `www.pixelbeat.org/cmdline.html`
- Little command line goodies `www.shell-fu.org`

That's all folks!
