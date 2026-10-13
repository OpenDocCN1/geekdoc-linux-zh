
如你所示，`printk` 是执行将消息写入内核消息缓冲区的关键函数。我们还可以看到标准 C 的 `__FILE__` 用于输出源文件名。

然而，无法保证 syslog 中一定会出现任何内容。通常在崩溃的情况下，`klogd` 日志器无法将信息写入磁盘。这时串口控制台（serial console）就变得重要了。当配置当时，内核会将重要的日志消息发送到串口控制台，并发送到 syslog 进程获取它们的缓冲区。消息通过串口线发送后，远程控制台将接收并保存这些消息。

### 7.2.2 设置串口控制台

诊断和确定系统崩溃或挂起原因的最重要工具之一可能是使用串口控制台来收集诊断信息。串口控制台并不是每个系统都需要的，尽管拥有它也没有坏处。但如果你的系统在极短的时间内不明故地崩溃或挂起多次，则强烈建议使用。

> 注意：在大多数发行版包含的内核源码包中，`Documentation/serial-console.txt` 文件是关于设置和配置串口控制台的极佳指南。

配合使用串口控制台的是启用内核的魔术键 SysRq 键；更多信息请参阅第 3 章“/proc 文件系统”中的 sysrq 节。串口控制台之所以有帮助，是因为通常当系统进入 panic 状态时（例如发生内核 oops 时），内核会将信息转储到内核日志守护进程。这通常意味着信息被写入了 `/var/log/messages`；但在某些情况下系统无法执行写入磁盘的操作，这就是串口控制台证明其用处的地方。配置妥后，信息会通过串口端口转储，同时处于健康状态的远程系统将接收并保存这些信息。可以使用本节讨论的技术对这些信息进行分析，或将其转发给相应的支持小组。

### 7.2.3 连接串口空回线（Null-Modem Cable）

要要做的任务是获取一根串口空回线。你可以在任何电脑商店找到它们，且通常价格很低廉。你还应该检查两台电脑的外部串口，以确定你是否需要 9 针或 25 针的连接器。新的空回线两端都同时带有 9 针和 25 针连接器，因此购买这种可能是合适的。

一旦线缆到位，应测试数据是否可以从一台机器发送到另一台。通过在串口控制台上首先启动通信程序来实现。如果运行的是 Linux，`minicom` 是一个很好的选择；如果运行的是 Windows，HyperTerminal 也可以。> 注意：Linux 默认可能没有安装 `minicom`。可执行文件通常位于 `/usr/bin/minicom`。如果没有，大多数发行版都将其作为可选包包含。通常情况下，在源机器上连接到第一个串口（`/dev/ttyS0`）运行以下命令：

```
stty 38400 < /dev/ttyS0; echo "This should appear on remote machine" >/dev/ttyS0
```

如果没有出现，检查：
- 线缆是否为空回线。
- 是否连接到了第一个串口；如果不是，将 `/dev/ttyS0` 改为 `/dev/ttyS1` 然后重试。
- 串口控制台程序正在运行。
- 串口速度已设置为 38400。

在启动时启用串口

验证串口控制台工作正常后，下一步是配置 Linux 通过串口发送重要消息。这通常通过大多数启动加载程序完成，或者永久添加到启动加载文件中。额外参数应如下：

```
console=ttyS0,38400
```

注意，不要替换现有的 `console` 参数，而应插入在其之前。保持任何现有的 `console=` 参数是为了防止虚拟控制台不可用。对于使用 GRUB 的系统，使用以下启动项来启用串口：

```
title Linux

kernel (hd0,7)/boot/linux-2.4.21-99-default root=/dev/hda vga=0x0314 splash=silent hdc=ide-scsi console=ttyS0 console=/tty0

initrd (hd0,7)/boot/initrd-2.4.21-99-default
```

使用此项重启后，串口控制台应设置好，并显示一些启动消息。启动服务器时，确保通信程序启用了日志功能。作为参考，这是串口控制台中捕获的消息示例，将发送给发行版团队或内核开发者（在此情况下为 VMware Inc.），注意这并不意味着存在问题：

```
Unable to handle kernel dereference at virtual address 000005e8

printing eip: c429aa52

* de 00000000

Oops: 2.4.21-99-default #1 Wed Sep 24 13:30:51 UTC 2003

CPU: 0

EIP: 0010:[usb-uhci_device_operations+31708122/24331932]

Tainted: PF

EIP: 0010:[c429aa52]

Tainted: PF

EFLAGS: 00213246

eax: 00000000 ecx: c364a720 edx: 00000001

si: 00000000 edi: 00000000 esp: c7f7fe50

ds: 00180000 ss: 00180000

Process vmware-vmx (pid: 2808, stackpage=c7f7f00)

Stack: 00000000 c7f7fe58 42826000 c0ed8886 c8dc7520 fffffffff c7f7ff88

c429886c

cdf9ce00 00000000 00000000 00000036ae20 c0121ce c0121bc9

00000000 00012192 00003046 00003046 000000000054

c7f7f8c7

Trace: [usb-uhci_device_operations+31699444/24340610]

[bh_action+66]

[tasklet_hi_action+57] [do_softirq+98] [do_IRQ+156]

Trace: <<c429886c> <<c0121ce2> <<c0121bc9> <<c0121992>

call_IRQ+5/133> <<_do_mapq_pgoff+1368/1632> <<do_mapq_pgoff+1419

[1632] <<do_map2+48/176> <<do_map2+119/176> [sys_ioctl+470/618]

<<c010c4d8> <<c0131aab1> <<c0123aeb> <<c010e8d8> <<c010e8f7>

<<c0153526>

[sys_mmmap+35/48] [system_call+51/64]

<<c010e993> <<c01088d3>
```
