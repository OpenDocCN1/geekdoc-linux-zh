
Linux 在启动时并不进行 IRQ 检测。当串口模块加载时，它只对串口设备进行检测。因此，请忽略它关于 IRQ 的说明，因为它只是在假设使用标准的 IRQ。这样做是因为 IRQ 检测是不可靠的，并且可能被欺骗。但如果 `seterial` 从启动脚本运行，它会更改 IRQ 并在启动屏幕上显示新的（希望是正确的）状态。那时就有问题了。

所以，尽管我的 `ttyS2` 位于 IRQ 5，但在 Linux 启动之初我仍然看到：

```
ttyS2 at 0x03e8 (irq = 4) is a 16550A
```

（旧版本的内核可能会将 ttyS02 显示为 tty02。）你必须使用串口工具来告诉 Linux 你正在使用的 IRQ。

# “无法打开 /dev/ttyS?: 权限拒绝”

使用 `ls -l /dev/ttyS*` 检查此端口的文件权限。如果你是 `ttyS?` 的所有者，那么你需要读写权限：第一列应为 `crw` 且带有 `c`（字符设备）。如果你不是所有者，它应该显示为 `rw-`。

# B 部分：Linux 调制调器 HOWTO

第 8 和 9 列意味着所有人对它都有读写权限。使用 `chmod` 更改权限。还有更复杂的方法来获取访问，例如属于一个具有组权限的“组”。

# 设备 ttyS 不支持该操作

这意味着 `seterial` 或 `stty` 请求的操作无法执行，因为内核不支持该操作。以前这通常是因为没有加载“serial”模块导致的。随着 PnP（即插即用）的出现，这可能意味着在驱动程序（以及 `seterial`）认为的地址上没有调制调器（或其他串口设备）。如果那里没有调制调器，发送到该地址的命令（操作）显然无法完成。请参阅“我的串口硬件中设置了什么？”

如果“serial”模块没有被加载，但 `lsmod` 显示它已加载，那么可能是它现在加载了，但在你收到错误消息时它还没有加载。在许多情况下，模块会在需要时自动加载（如果可以找到的话）。强制加载“serial”模块的方法可能列在文件：`/etc/modules.conf` 或 `/etc/modules` 中。实际模块应位于：`/lib/modules/.../misc_serial.o`。

# 无法创建锁文件。抱歉

当端口被程序“打开”时，在 `/var/lock/` 中会创建一个锁文件。目录权限错误将导致无法创建锁文件。使用 `-ld /var/lock` 检查权限是否正确：所有人都是 `rwx`（重复3次）。如果错误，请使用 `chmod` 修复。当然，如果没有“lock”目录，就无法创建锁文件。关于锁文件的更多信息，请参阅串口-HOWTO 子章节：“什么是锁文件？”

# 设备 /dev/ttyS? 已锁定。

这意味着另一个人（或其他另一个进程）认为正在使用该串口。有多种方法可以找到是哪个进程在“使用”它。一种方法是查看锁文件的内容（`/var/lock/LOCK...`）。它应该是进程 ID（PID）。如果进程 ID 是 261，输入 `ps 261` 来查找它是什么。如果该进程不再需要，可以通过 `kill 261` 优雅地杀死它。如果它拒绝被杀死，使用 `kill -9 261` 强制杀死，但这样锁文件不会被删除，你需要手动删除它。或者如果不存在 161 这样的进程，你可能可以直接删除锁文件，但在大多数情况下，如果锁文件包含过期的进程 ID（如 261），它应该被自动删除。

# /dev/ttyS?: 设备或资源忙

当你尝试用调制调器拨号时，如果 DCD 或 DTR 未正确实现，就会出现这个问题。DCD 只有在实际连接时（即有人拨入）才应该开启（断言），而不是当 getty 正在监控端口时。检查确保你的调制调器配置为仅在有连接时断言 DCD。当有任何程序使用或监控线路（如 getty、kermit 或其他通信程序）时，DTR 应该开启（断言）。

“resource busy”对于 ttyS2 意味着“你无法使用 ttyS2，因为另一个设备正在使用 ttyS2 的中断”。潜在的中断冲突与 `seterial` 认为的相符。一个更准确的错误信息将是“无法使用 ttyS2，seterial 数据表明另一个设备正在使用”。

这种情况存在两种可能性。如果 `seterial` 错误预测了冲突，可能会导致无法使用 ttyS2。但如果真的存在冲突，则可以避免。升级 ttyS2。但如果 `seterial` 错误，可能会导致无法使用。你需要通过查看启动消息来发现哪些程序在使用 ttyS2，这需要通过 `seterial` 来确认。seterial 设置的串口调制调器。

# 故障排除工具

这些是一些你可能用于故障排除的程序：

- `lsof /dev/tty*` 将列出已打开的串口端口

- `seterial` 显示并设置底层端口配置。参阅“什么是 seterial”

- `stty` 显示并设置端口配置（seterial 处理）

## B 部分：Linux 调制调器 HOWTO

- `modemstat` 或 `statserial` 将显示各种信号线（如 DTR、CTS）的状态

- `iptune` 给串口端口更高的优先级以提高性能

- 用于硬盘调优的 `hdparam` 可能有帮助

- `lspci` 显示 PCI 总线上的硬件等

- `pnpdumpregs` 显示 ISA 总线上 PnP 设备的实际 IRQ 等

- 在 `/proc` 树下的某些“文件”（如 iports 和 interrupts）。

# 固件升级

调制调器可以通过从互联网获取升级程序并重新编程其闪存内存来升级。通过串口从 PC 发送此“程序”到调制调器，调制调器会将该程序存储在非易失性内存中（掉电后仍然存在）。安装说明通常是关于在 Windows 下如何操作，你需要找出在 Linux 下对应的操作。

如果此 HOWTO 的最新版本仍包含此请求（新版本的 HOWTO），请向我发送你安装此类升级的经验，这对他人有所帮助。

以下是升级的大致思路。首先，可能可能向调制调器发送一个命令告诉它这是一个 Flash 升级。可能是 AT*** 你可以通过启动通信程序（如 minicom）并首先输入 AT <> 来查看你的调制调器是否存在并回答 OK。接下来，你需要直接向调制调器发送文件（有时是两个）。通信程序（如 minicom）通常使用 zmod 或 kermit 将文件发送到调制调器（以及之后），但这些会将文件放入数据包，而你想发送原始文件而不是修改后的文件。但 kermit 通信程序有一个传输命令可以直接发送文件（不使用 kermit 数据包），因此这是发送文件的一种方法。

另一种发送文件的方法是从通信程序退出到 shell（在 minicom 中是 ^AJ），然后执行：`upgrade_file_name > /dev/ttyS2`（如果你的串口是 ttyS2）。然后

# 478

# 资源附

返回通信程序（在 minicom 命令行提示符处输入 `fg`）以查看发生了什么。

这里是一个特定 Rockwell 调制解调器的示例会话（C-a 是 ^）：

运行 minicom

```
Type At**: see "Download initiated . ."
C-a J
cat FLASH.S37 > /dev/modem
fg: see "Download flash code . ."
C-a J - cat 283P1722.S37 > /dev/modem
fg: see "Device successfully programmed"
```

# 其他信息来源

# 杂项

- 以下程序的 man pages：`agetty(8)`, `getty(1m)`, `gettydefs(5)`, `init(1)`, `isapnp(8)`, `login(1)`, `mgetty(8)`, `setserial(8)`

- 你的调制解调器手册（如果有）。某些调制解调器确实有手册。

- Vern Hoxie 编写 Serial Suite <ftp://scicom.alphadec.com/pub/linux> 是一系列关于 Linux 串口维护和运行的简短介绍以及简单的程序。

- Linux 串口邮件列表。要加入，请发送邮件到 <majordomo@vger.rutgers.edu>，并在正文中包含 `subscribe linux-serial`。如果你在正文中需要帮助，你会收到帮助信息。服务器还提供许多其他 Linux 列表。发送 `lists` 命令可以查看邮件列表。

# 图籍

我未能找到一本关于调制解调器的良好的更新书籍。

- Gilbert Held 著《The Complete Modem Reference》，1997年。包含了太多关于过时主题的信息。可以在互联网上找到更新的信息。

- Tina Rathbone 著《Modems For Dummies》，1996年。（从未见过。）

- Cass R. Lewart 著《Ultimate Modem Handbook》，1998年。

## B 部分：Linux 调制解调器 HOWTO

# HOWTOs

- 电缆调制调制解调器微型 HOWTO
