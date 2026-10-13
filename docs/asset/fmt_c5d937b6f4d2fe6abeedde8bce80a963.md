
我们来看以下示例，以理解如何显示和修改名为 `net.ipv4.tcp_abc` 的内核参数值。运行 `sysctl` 来确定该参数的当前值：

```
# sysctl net.ipv4.tcp_abc
net.ipv4.tcp_abc = 0
```

该值存储在 `/proc/sys/net/ipv4/tcp_abc` 文件中，可以使用 `cat` 查看：

```
# cat /proc/sys/net/ipv4/tcp_abc
0
```

使用 `sysctl` 或 `echo` 将值从 0 更改为 10：

```
# sysctl -w ipv4.tcp_abc=10
net.ipv4.tcp_abc = 10
# echo 10 > /proc/sys/net/ipv4/tcp_abc
```

此时如果重启系统，该值将恢复为原始设置。若要使新值在重启后依然有效，请编辑 `sysctl.conf` 并追加以下行目：

```
ipv4.tcp_abc = 10
```

现在，运行 `sysctl` 命令加载新值（如果尚未加载）：

```
# sysctl -p
```

同样，如果你想通过 `sysctl -w` 更改 `net.ipv4.icmp_echo_all`：

```bash
# sysctl -w net.ipv4.icmp_echo_all=1
```

若重启系统，该更改将失效。

## 为内核打补丁 (Patching the Kernel)

执行内核补丁是为了修复任何阻止内核正常运行的现有功能问题。内核补丁可以从 Red Hat 网站、`ftp.kernel.org/pub/linux/kernel/v2.6` 或任何其他公共网站下载。示例演示了将内核补丁到 2.6.28。假设 `patch-2.6.28.gz` 已经下载并位于 `/var/run` 目录。进入 `/var/run`，解压补丁文件并运行 `patch` 命令来应用补丁：

```
# cd /var/tmp
# gunzip patch-2.6.28.gz
# patch -p0 patch-2.6.28
```

使用 `-p` 选项时，命令将保留补丁文件中定义的文件的原始路径。

## 修改内核参数 (Modifying Kernel Parameters)

有数百个内核参数，其值影响内核的整体行为以及整个运行系统。这些参数的运行时值存储在 `/proc/sys` 目录下的文件中，可以通过更改相关文件来修改，这些更改将一直有效，直到重新调整该值或重启系统。可以使用 `sysctl` 或 `echo` 命令进行更改。若要使更改在重启后仍然有效，必须在 `/etc/sysctl.conf` 文件中定义这些值。

`sysctl.conf` 的内容显示如下：

```
# cat /etc/sysctl.conf
# Red Hat Linux 的内核 sysctl 配置文件
#
# 对于二进制值，0 表示启用。详情请见 sysctl(8) 和
# sysctl.conf(5)。
# 控制 IP 数据包转发
net.ipv4.forward = 0
# 控制源路由验证
net.ipv4.conf.default.rp_filter = 1
```

Linux 内核 337

# 不使用源路由

net.ipv4.default.accept_source_route = 0

# 控制内核的系统请求 (System Request) 调试功能

kernel.sysrq = 0

# 控制核心转储是否在核心文件名中追加 PID

# 有助于调试多线程应用程序

kernel.core.uses_pid = 1

# 控制 TCP synookies 的使用

net.ipv4.tcp_synookies = 1

# 控制消息的最大大小（字节）

kernel.msgmnb = 65536

# 控制消息队列默认的最大大小

kernel.msgmax = 65536

# 控制共享段的最大大小（字节）

kernel.shmmax = 6871947636

# 控制共享内存段的最大数量

kernel.shmall = 4294967296

如你所见，配置了某些内核参数，其他默认设置在系统启动加载内核时会自动生效。运行带 `-a` 选项的 `sysctl` 命令可以列出所有当前正在使用的参数及其对应值：

- - `sysctl -a`

sunprpc.max_resvport = 1023

sunprpc.min_resvport = 665

sunprpc.tcp_slot_table_entries = 16

sunprpc.udp_slot_table_entries = 16

sunprpc.nlm_debug = 0

sunprpc.nfsd_debug = 0

sunprpc.nfs_debug = 0

sunprpc.rpc_syscall32 = 0

abvi.syscall32 = 1

dev.parport.port0.devices.active = none

dev.parport.port0.modes = PCPSP,TRISTATE

## 获取内核源码 (Obtaining Kernel Source)

构建内核的第一步是获取源码并将其存放在 `/var/tmp`。源码包括 Red Hat CD/DVD、Red Hat 网站 `www.redhat.com`、`ftp.kernel.org/pub/linux/kernel/v2.6` 或任何其他公共网站。通过 `sysctl -a` 在系统上确定内核级别，你需要的包如下表所示：

| 包 | 说明 |
| :--- | :--- |
| binutils | 二进制工具 |
| cpp | C 语言预处理器 |
| gcc | GNU C 编译器 |
| glib-devel | Glib 头文件 |
| glibc-devel | C 库 |
| glibc-headers | 内核头文件 |
| gtk2-devel | X 窗口文件 |
| libglade-devel | Libglade 库文件 |
| ncurses | 用于菜单 |
| ncurses-devel | Ncurses 库文件 |
| qt-devel | QT 库文件 |
| tcl | 脚本语言 |

使用 `yum` 命令获取并安装识别出的包，以及其他所需的包。例如：

```bash
# yum -y install binutils cpp glib-devel glibc-devel glibc-headers gtk2-devel libglade-devel ncurses ncurses-devel qt-devel
```

## 安装源码

执行以下步骤安装源码并为目标平台构建新源码：

1. 安装内核源码。`rpm` 命令将在 `/usr/src/redhat` 下创建两个子目录 `SOURCES` 和 `SPECS`，生成所有源码和 SPECS 规范文件。忽略关于用户和组不存在的消息。

```bash
# cd /var/tmp
# rpm -ivh kernel-2.6.18-92.el5.src.rpm
1:kernel ######################## [100%]
```

2. 在 `/usr/src/redhat` 创建 BUILD 子目录：

```bash
# mkdir /usr/src/redhat/
```

3. 如需要，修改位于 `/usr/src/redhat/SPECS` 目录下的 `kernel-2.6.spec` 文件。

4. 在 i386 平台为 `/usr/src/redhat/BUILD/kernel-2.6.18/linux-2.6.18/vanilla` 版本构建源码，使用 `kernel-2.6.spec` 规范文件，输出到 `/usr/src/redhat`：

```bash
# cd /usr/src/redhat/SPECS
# rpmsbuild --target=i386 kernel-2.6.spec
Building target platforms: i386
Building for target i386
Executing(%prep): /bin/sh -e /var/tmp/rpm-tmp.18619
+ umask 022
+ cd /usr/src/redhat/BUILD
+ LANG=C
+ export LANG
```

## 创建配置文件

现在，你需要创建一个用于构建新内核的配置文件。该配置文件应仅包含对所需的硬件和软件组件的支持。为了本次演示，请将现有的内核配置文件 `/boot/config-2.6.18-92.el5` 复制为 `config` 到 `/usr/src/redhat/BUILD/kernel-2.6.18/linux-2.6.18.i386` 并使用表 16-3 所示的 `make` 命令选项之一对对其进行编辑。

| 选项 | 描述 |
|---|---|
