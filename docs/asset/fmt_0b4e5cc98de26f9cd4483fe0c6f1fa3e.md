
```
crash 4.0-3.11
Copyright 2002, 2003, 2004, 2005, 2006 Red Hat, Inc.
Copyright 2004, 2005, 2006 IBM Corporation
Copyright 1999-2006 Hewlett-Packard Co
Copyright 2005 Fujitsu Limited
Copyright 2005 NEC Corporation
Copyright 1999, 2000, 2001 Mission Critical Linux, Inc.
此程序是免费软件，受 GNU 通用公共许可证保护，
欢迎您在特定条件下修改它和/或分发它的副本。输入 'help copying' 查看条件。
本程序不提供任何保证。输入 'help warranty' 查看详情。

GNU gdb 6.1
Copyright 2004 Free Software Foundation, Inc.
GDB 是免费软件，受 GNU 通用公共许可证保护，
欢迎您在欢迎条件下修改它和/或分发它的副本。

## 列表 21.5 续

输入 "show copying" 查看条件。
GDB 绝对没有任何任何保证。输入 "show warranty" 查看详情。
此 GDB 被配置为 "x86_64-unknown-linux-gnu..."
```

KERNEL: `/usr/lib/debug/modules/2.6.18-1.2747.el5/vmlinux`

DUMPFILE: `vmcore`

CPUS: 2

DATE: Fri Jan 12 15:31:26 2007

UPTIME: 00:04:20

LOAD AVERAGE: 0.31, 0.31, 0.14

TASKS: 168

NODENAME: `myhostname`

RELEASE: 2.6.18-1.2747.el5

VERSION: #1 SMP Nov 9 18:52:11 2006

MACHINE: x86_64 (2400 M)

MEMORY: 4 GB

PANIC: SysRq : Trigger crashdump

PID: 0

## 测试 Kdump

由于在内核发生崩溃之前，很难知道 Kdump 是否正常工作，因此有一种方法可以强制触发内核崩溃。

```
echo c > /proc/sysrq-trigger
```

一旦执行该命令，系统应该发生恐慌（panic），并且系统将无响应。系统应该将使用 Kekec 重启到第二个内核。由于使用了 Kekec，您将不会看到 BIOS 或 GRUB 启动屏幕。在转储文件创建并保存后，系统将重启到普通内核。这一次您将看到 BIOS 和 GRUB 屏幕。根据您的系统内存大小，整个过程可能需要一段时间时间。

请参考下一节“分析崩溃”了解如何从此转储文件中收集信息。

## 分析崩溃

转储文件的位置取决于您在 `/etc/kdump.conf` 中选择的位置。如果 `kdump.conf` 中没有设置位置，则 `vmcore` 文件将写入到 `/var/crash/<date>/` 目录。如果位置设置为分区，`vmcore` 文件可以在该分区挂载的 `/var/crash/<date>/` 目录下找到。

如果配置了 NFS 或 SSH 网络连接，`vmcore` 文件将传输到指定的 `/var/crash/<host>-<date>/`，并带有网络服务器名称。如果使用原始分区，则核心转储的内容位于原始分区。如果通过 `path` 变量设置了备用目录，这些位置的 `/var/crash/` 目录应替换为此不同的目录。

创建 `vmcore` 文件后，可以使用 `crash` 程序进行交互式分析。确保您已安装了 `crash` RPM 包。使用它还需要内核的 `vlinux` 文件。该文件由 `kernel-debuginfo` 包提供。每个内核版本都有一个 `kernel-debuginfo` 包，因此请安装正确的版本。它可以通过 `ftp.redhat.com` FTP 服务器通过 FTP 获取。登录匿名用户后，进入到 `/pub/redhat/linux/enterprise/<version>/en/os/<crash-debuginfo/`，将 `<version>` 替换为适用于您系统的相应值，并将 `<version>` 替换为用于崩溃的 `x86_64`。您也可以在网络浏览器中访问 `http://server` 来查看软件包列表。

要开始分析文件，请以 root 用户执行命令 `crash <vlinux> <vmcore>`。如果 `<vmcore>` 不在当前目录，请务必使用其路径（将 `<kernel-version>` 替换为崩溃时运行的内核版本）。

```
crash /usr/lib/modules/kernel-version/vlinux vmcore
```

启动该工具将显示列表 21.5 的输出。

### 列表 21.5 启动 crash 工具

```
crash 4.0-3.11

Copyright 2002, 2003, 2004, 2005, 2006 Red Hat, Inc.

Copyright 2004, 2005, 2006 IBM Corporation

Copyright 1999-2006 Hewlett-Packard Co

Copyright 2005 Fujitsu Limited

Copyright 2005 NEC Corporation

Copyright 1999, 2000, 2001 Mission Critical Linux, Inc.

此程序是免费软件，受 GNU 通用公共许可证保护，

欢迎您在特定条件下修改它和/或分发它的副本。输入 'help copying' 查看条件。

本程序不提供任何保证。输入 'help warranty' 查看详情。

GNU gdb 6.1

Copyright 2004 Free Software Foundation, Inc.

GDB 是免费软件，受 GNU 通用公共许可证保护，

欢迎您在欢迎条件下修改它和/或分发它的副本。

## 列表 21.5 续

输入 "show copying" 查看条件。

GDB 绝对没有任何任何保证。输入 "show warranty" 查看详情。

此 GDB 被配置为 "x86_64-unknown-linux-gnu..."
```

KERNEL: `/usr/lib/debug/modules/2.6.18-1.2747.el5/vmlinux`
DUMPFILE: `vmcore`
CPUS: 2
DATE: Fri Jan 12 15:31:26 2007
UPTIME: 00:04:20
LOAD AVERAGE: 0.31, 0.31, 0.14
TASKS: 168
NODENAME: `myhostname`
RELEASE: 2.6.18-1.2747.el5
VERSION: #1 SMP Nov 9 18:52:11 2006
MACHINE: x86_64 (2400 M)
MEMORY: 4 GB
PANIC: SysRq : Trigger crashdump
PID: 0

## 设置 SMP 亲和性

如果您从未查看过 `/proc/interrupts`，那么您可能不知道 SMP 亲和性。SMP 亲和性允许您将中断绑定到特定的 CPU 上，这在多核系统中可以提高性能并实现负载均衡。

要查看当前的绑定情况，可以查看 `/proc/interrupts`。输出如下所示：

```
CPU0    CPU1    CPU2    CPU3 ... affinity
timer   10000000000000000000000000000000 00000000000000000000000000000000 00000000000000000000000000000000 0
```

要设置亲和性，可以通过修改 `smp_affinity` 文件来实现。该文件位于 `/proc/irq/<中断号>/smp_affinity`。该文件包含十六进制掩码，每个位代表一个 CPU。例如，将掩码设置为 `00000003` 将把该中断绑定到 CPU 0 和 CPU 1。

```bash
echo 00000003 > /proc/irq/<中断号>/smp_affinity
```

注意，这些更改在重启后会丢失。要永久保存这些更改，需要配置启动脚本或使用 systemd 服务。

## 为锁死系统启用 NMI 看门狗 445

对于最后两个命令，可以使用 `-c <cpulist>` 选项代替使用位掩码来指定处理器，其中 `<cpulist>` 是用逗号分隔的处理器编号列表。编号从 0 开始计数。因此，0 代表第一个处理器，1 代表第二个处理器，以此此类推。可以使用连字符来列出连续的处理器编号，例如 2-4。

## 为锁死系统启用 NMI 看门狗
