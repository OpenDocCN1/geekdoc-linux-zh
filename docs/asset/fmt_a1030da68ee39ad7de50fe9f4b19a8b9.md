
### `-D logfile`

将日志输出到 `logfile` 而不是 `stderr`。

### `-L path`

设置 `BIOS`、`VGA BIOS` 和键盘映射的目录。

### `-bios file`

设置 `BIOS` 的文件名。

### `-enable-kvm`

启用 `KVM` 完全虚拟化支持。此选项仅在编译时启用了 `kvm` 支持的情况下可用。

### `-xen-domid id`

指定 `xen` 来宾域 `id`（仅限 `XEN`）。

### `-xen-create`

使用 `xen` 超调用创建域，绕过 `xen`。警告：当使用 `xen` 时不应使用（仅限 `XEN`）。

### `-xen-attach`

附加到现有的 `xen` 域。`xen` 在启动 `QEMU` 时将使用此（仅限 `XEN`）。

### `-no-reboot`

退出而不是重新启动。

### `-no-shutdown`

来宾关机时不要退出 `QEMU`，而是仅停止仿真。例如，这允许切换到监控器以将更改提交到磁盘镜像。

### `-loadvm file`

立即从保存的状态启动（监控器中的 `loadvm`）。

### `-daemonize`

在初始化后将 `QEMU` 进程守护化。`QEMU` 在准备好接受其任何设备上的连接之前不会从标准 `io` 分离。此选项是外部程序启动 `QEMU` 而不必处理初始化竞态条件的有用方法。

### `-option-rom file`

将 `file` 的内容加载为选项 `rom`。此选项可用于加载诸如 `EtherBoot` 之类的东西。

### `-rtc [base=utc|localtime[date]][,clock=host|vm][,driftfix=none|slew]`

指定 `base` 为 `utc` 或 `localtime`，以便 `rtc` 分别从当前 `UTC` 时间或本地时间开始。`localtime` 对于在 `MS-DOS` 或 `Windows` 中显示正确日期是必需的。要在特定时间点开始，请以 `2006-06-17T16:01:21` 或 `2006-06-17` 的格式提供 `date`。默认 `base` 为 `UTC`。

默认情况下，`rtc` 由主机系统时间驱动。这允许使用 `rtc` 作为来宾内部精确的参考时钟，特别是如果主机时间平滑地跟随精确的外部参考时钟，例如通过 `NTP`。如果你想将来宾时间与主机隔离，可以将 `clock` 设置为 `rt`。为了甚至在挂起期间防止其进展，可以将其设置为 `vm`。

如果你遇到时间漂移问题，特别是与 `Windows` 的 `ACPI HAL` 相关时，启用 `driftfix`（仅限 `i386` 目标）。此选项将尝试确定有多少 `time` 中断未被 `Windows` 来宾处理，并将重新注入它们。

### `-icount [shift=N|auto]`

启用虚拟指令计数器。虚拟 `cpu` 每 `2^N` `ns` 虚拟时间执行一条指令。如果指定 `auto`，则虚拟 `cpu` 速度将自动调整，以保持虚拟时间在真实时间的几秒内。

当虚拟 `cpu` 休眠时，虚拟时间将以默认速度前进，除非指定了 `sleep=no`。如果使用 `sleep=no`，虚拟时间将立即跳到下一个 `time` 截止点，每当虚拟 `cpu` 进入睡眠模式时，并且如果没有启用 `time`，则不会前进。此行为从来宾的角度提供了确定性的执行时间。

请注意，虽然此选项可以提供确定性行为，但它不提供周期精确的仿真。现代 `CPU` 包含具有复杂缓存层级的超标量乱序核心。执行的指令数量与实际性能往往关系甚微或没有相关性。

`align=on` 将激活延迟算法，该算法将尝试同步主机时钟和虚拟时钟。目标是以 `shift` 选项强加的真实频率运行来宾。每当来宾时钟落后于主机时钟并且指定了 `align=on` 时，我们会向用户打印一条消息以告知延迟。目前，此选项在 `shift` 为 `auto` 时不起作用。注意：同步算法对于来宾时钟运行在主机时钟前方的那些 `shift` 值有效。通常发生在 `shift` 值较高时（多高取决于主机机器）。

### `-watchdog 模型`

创建一个虚拟硬件看门狗设备。一旦启用（通过客户机操作），客户机内部的代理必须定期轮询看门狗，否则客户机将重新启动。选择客户机拥有驱动程序的模型。该模型是拟硬件看门狗的模型。使用 `-watchdog help` 列出可用的硬件模型。每个客户机只能启用一个看门狗。

以下模型可能可用：

- `ib700`：`iBASE 700` 是一个非常简单的 `ISA` 看门狗，具有单个定时器。
- `i6300esb`：`Intel 6300ESB I/O` 控制器中枢是一个功能更强大的基于 `PCI` 的双定时器看门狗。
- `diag288`：`s390x` 的虚拟看门狗，由 `diagnose 288` 超系统调用支持（目前仅限 `KVM`）。

### `-watchdog-action 动作`

该动作控制 `QEMU` 在看门狗定时器到期时将执行的操作。默认为 `reset`（强制重置客户机）。其他可能的动作包括：

- `shutdown`（尝试优雅地关闭客户机）
- `poweroff`（强制关闭客户机）
- `pause`（暂停客户机）
- `debug`（打印调试消息并继续）
- `none`（什么都不做）

请注意，`shutdown` 动作要求客户机响应 `ACPI` 信号，而在使用看门狗到期的情况下，客户机可能无法做到这一点，因此不建议在生产环境中使用 `-watchdog-action shutdown`。

示例：

- `-watchdog i6300esb -watchdog-action pause`
- `-watchdog ib700`

### `-echr n|uric,ascii, 值`

更改使用监视器串行共享时用于切换到监视器的转义字符。使用 `-nographic` 选项时，默认为 `0x01`。`0x01` 等于按下 `control-a`。你可以从 `ascii` 控制键中选择其他字符，其中 `1` 到 `26` 对应 `Control-a` 到 `Control-z`。例如，你可以使用以下任一方法将转义字符更改为 `Control-t`：

- `-echr 0x14`
- `-echr 20`

### `-virtioconsole c`

设置 `virtio` 控制台。此选项是为了向后兼容性而保留的。请使用 `-device virtcon` 作为新的调用方式。

### `-show-cursor`

显示光标。

### `-tb-size n`

设置 `TB` 大小。

### `-incoming`

- `tcp:[host]:port[,to=maxport][,ipv4][,ipv6]`：准备传入迁移，在指定的 `tcp` 端口上监听。
- `rdma:host:port[,ipv4][,ipv6]`：准备传入迁移，在指定的 `rdma` 端口上监听。
- `unix:socketpath`：准备传入迁移，在指定的 `unix` 套接字上监听。
- `fd:fd`：从给定的文件描述符接受传入迁移。
- `exec:cmdline`：将传入迁移接受为指定外部命令的输出。
- `defer`：等待通过 `migrate_incoming` 指定的 `URI`。监视器可用于在发出 `migrate_incoming` 之前更改设置（如迁移参数），以允许开始迁移。

### `-nodefaults`

不创建默认设备。通常，`QEMU` 会设置默认设备，如串行端口、并行端口、虚拟控制台、监视器设备、`VGA` 适配器、软驱和 `CD-ROM` 光驱等。`-nodefaults` 选项将禁用所有这些默认设备。

### `-chroot 目录`

在开始客户机执行之前，立即 `chroot` 到指定目录。与 `-runas` 结合使用特别有用。

### `-runas 用户`

在开始客户机执行之前，立即放弃 `root` 权限，切换到指定用户。

### `-prom-env 变量=值`

将 `OpenBIOS nvram` 变量设置为给定值（仅限 `PPC`、`SPARC`）。

### `-semihosting`

启用半主机模式（仅限 `ARM`、`M68K`、`Xtensa`、`MIPS`）。

### `-semihosting-config [enable=on/off][,target=native|gdb|auto][,arg=str[,...]]`

启用并配置半主机功能（仅限 `ARM`、`M68K`、`Xtensa`、`MIPS`）。

- `target=native|gdb|auto`：定义半主机调用将指向何处，即 `QEMU`（`native`）或 `GDB`（`gdb`）。默认为 `auto`，在调试会话期间使用 `gdb`，否则使用 `native`。
- `arg=str1,arg=str2,...`：允许用户传递输入参数，并且可以多次使用以构建列表。旧式的 `-kernel1/-append` 传递命令行方式仍为向后兼容而受支持。如果同时指定了 `-semihosting-config` 的 `arg` 和 `-kernel1/-append`，前者将传递给半主机，因为它始终具有优先级。

### `-old-param`

旧参数模式（仅限 `ARM`）。

### `-sandbox 参数`

启用 `Seccomp` 模式 `2` 系统调用过滤器。`'on'` 将启用系统调用过滤，`'off'` 将禁用它。默认为 `'off'`。

### `-readconfig 文件`
