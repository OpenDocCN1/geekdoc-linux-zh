
systemd 是一个现代化的系统和`服务管理器`，拥有针对 SysV 命令和运行级别的兼容层。systemd 具有并发结构，使用套接字和 D-Bus 进行服务激活、按需执行守护进程、使用 cgroups 进行进程监控、支持快照、恢复系统会话、控制挂载点以及基于依赖的服务控制。近年来，大多数主要 Linux 发行版已逐渐采用 systemd 作为其默认系统管理器。

## Upstart

与 systemd 类似，Upstart 也是 init 的替代方案。Upstart 的重点是通过并行化系统服务加载过程来加速启动过程。在旧版本的发行版中，Ubuntu 基础发行版使用了 Upstart，但现在已让位于 systemd。

## 初始化检查

在启动过程中可能会发生错误，但它们可能并不关键到足以完全停止操作系统。尽管如此，这些错误可能会损害系统的预期行为。所有错误都会产生消息，可用于后续调查，因为它们包含关于错误发生时间和方式的重要信息。即使没有生成错误消息，启动过程中收集的信息也可以用于调整和配置目的。

内核存储其消息（包括启动消息）的内存空间称为`内核环形缓冲区`。即使在初始化过程中未显示消息（例如显示动画时），这些消息仍保留在内核环形缓冲区中。然而，当系统关机或执行命令 `dmesg --clear` 时，内核环形缓冲区会丢失所有消息。如果不带选项，命令 `dmesg` 会显示内核环形缓冲区中的当前消息：

```bash
$ dmesg
[    5.262389] EXT4-fs (sda1): mounted filesystem with ordered data mode. Opts: (null)
[    5.449712] ip_tables: (C) 2000-2006 Netfilter Core Team
[    5.460286] systemd[1]: systemd 237 running in system mode.
[    5.480138] systemd[1]: Detected architecture x86-64.
[    5.481767] systemd[1]: Set hostname to <torre>.
[    5.636607] systemd[1]: Reached target User and Group Name Lookups.
[    5.636866] systemd[1]: Created slice System Slice.
[    5.637000] systemd[1]: Listening on Journal Audit Socket.
[    5.637085] systemd[1]: Listening on Journal Socket.
[    5.637827] systemd[1]: Mounting POSIX Message Queue File System...
[    5.638639] systemd[1]: Started Read required files in advance.
[    5.641661] systemd[1]: Starting Load Kernel Modules...
[    5.661672] EXT4-fs (sda1): re-mounted. Opts: errors=remount-ro
[    5.694322] lp: driver loaded but no devices found
[    5.702609] ppdev: user-space parallel port driver
[    5.705384] parport_pc 00:02: reported by Plug and Play ACPI
[    5.705468] parport0: PC-style at 0x378 (0x778), irq 7, dma 3 [PCSPP,TRISTATE,COMPAT,EPP,ECP,DMA]
[    5.800146] lp0: using parport0 (interrupt-driven).
[    5.897421] systemd-journald[352]: Received request to flush runtime journal from PID 1
```

`dmesg` 的输出可能长达数百行，因此上述列表仅包含显示内核调用 systemd 服务管理器的摘录。行开头的值相对于内核开始加载时的秒数。

在基于 systemd 的系统中，命令 `journalctl` 可以使用选项 `-b`、`--boot`、`-k` 或 `--dmesg` 显示初始化消息。命令 `journalctl --list-boots` 显示相对于当前启动的启动编号列表、它们的识别哈希值以及对应消息的起始和结束时间戳：

```bash
$ journalctl --list-boots
-4  9e5b3eb49528452088b41ad4dbe1afa6  Thu 2019-10-03 13:39:23 -03-Thu 2019-10-03 13:40:30 -03
-3  9ed379955535430aa43baa17758f40fa  Thu 2019-10-03 13:41:15 -03-Thu 2019-10-03 14:56:19 -03
-2  17672d88561946e9c9b102df7355452e  Thu 2019-10-03 14:56:57 -03-Thu 2019-10-03 19:27:16 -03
-1  55c0d9439bfb485a20a62776d0b8d4  Thu 2019-10-03 19:27:53 -03-Fri 2019-10-04 00:28:47 -03
 0  08fbbedd9f964a748b402bb27b200622  Fri 2019-10-04 00:31:01 -03-Fri 2019-10-04 10:17:01 -03
```

在基于 systemd 的系统中，之前的初始化日志也会保留，因此仍可以检查先前操作系统会话的消息。如果提供选项 `-b 0` 或 `--boot=0`，则显示当前启动的消息。选项 `-b -1` 或 `--boot=-1` 将显示上次初始化的消息。选项 `-b -2` 或 `--boot=-2` 将显示再上一次初始化的消息，依此类推。以下摘录显示了内核调用 systemd 服务管理器处理最后一次初始化过程的情况：
