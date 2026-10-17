
| 处理器 | 计算系数 | 参考 BogoMips |
| :--- | :--- | :--- |
| `Intel 8088` | `clock * (0.004 ± 0.001)` | 0.02 |
| `Intel/AMD 386SX` | `clock * (0.14 ± 0.01)` | 0.8 |
| `AMD 386DX` | `clock * (0.18 ± 0.01)` | 1 (定义) |
| `Motorola 68030` | `clock * (0.25 ± 0.005)` | 1.4 |
| `Cyrix/ITM 486` | `clock * (0.34 ± 0.065)` | 1.8 |
| `Intel Pentium` | `clock * (0.40 ± 0.035)` | 2.2 |
| `Intel 486/5x86` | `clock * (0.50 ± 0.015)` | 2.8 |
| `Mips R4000/R4400` | `clock * (0.75 ± 0.010)` | 2.3 |
| `Nexgen 5x86` | `clock * (0.84 ± 0.015)` | 4.2 |
| `PowerPC 604` | `clock * (0.99 ± 0.005)` | 4.7 |
| `Alpha` (所有 CPU) | `clock * (1.00 ± 0.005)` | 5.5 |
| `Intel Pentium Pro` | `clock * (1.00 ± 0.005)` | 5.6 |
| `Cyrix 5x86/6x86` | `clock * (1.00)` | 5.6 |
| `Intel Pentium II` | `clock * (1.00)` | 5.6 |
| `Mips R4600` | `clock * (1.00)` | 5.6 |
| `Alpha 21264` | `clock * (1.99)` | 11.1 |
| `AMD K5/K6` | `clock * (2.00 ± 0.010)` | 11.1 |
| `Pentium MMX` | `clock * (2.00)` | 11.1 |
| `Motorola 6860` | `clock * (2.01)` | 11.2 |
| `Motorola 6840` | (暂无数据) | |
| `Sparc` | (暂无数据) | |

注意 `BogoMips` 计算循环没有利用各种处理器的并行性，例如 `Intel Pentium` 和 `Alpha 21264`。注意非 `Intel` CPU 的 `BogoMips` 计算循环相似但并不相同。

## 4 如何确定当前的 BogoMips 评分

有三种方法可以确定当前的 `BogoMips` 评分：

1. 查看 `/proc/cpuinfo`，例如使用 `cat /proc/cpuinfo`
2. 查看 `syslog` 启动期间打印的内容（通过 `dmesg` 或 `syslog` 显式检索）
3. 使用独立程序。

厌倦了重启系统来查看有多少 `BogoMips` 吗？`Bogomips` 是一个使用世界上最认可的基准之一显示系统性能的独立程序。它在 Linux 内核启动时使用了相同的代码。`1.3` 版本的 `BogoMips` 现在可移植的，可以在任何支持 `ANSI` 编译器的系统上运行。由于独立程序的值可能会低于下表中的系统负载，请注意 `site.edu/pub/Linux/status/bogo-1.2.tar.gz` 包含了最新版本。

## 5 BogoMIPS 评分的波动

> 来自 `Linux Torvalds` (`torvalds@linux.fi`)，关于在 `BogoMIPS` 评分中可能看到的波动，发布于 `kernel.development`，1994 年 4 月 28 日：“`BogoMips` 计算循环是‘量化’的，因此你可能每次都得到精确的数字。只有当速度处于‘边缘’时，微小的波动（中断时钟不同）导致它会在数值之间跳转。”

## 6 BogoMIPS ... 失败

来自来自各种问题和私人邮件建议，例如 `Lily` (`lbliao@alumni.caltech.edu`) 和 `Pierre Frenkel` (`frenkel@ftp.fr`)。在 1995 年 3 月他们问：

> “当我启动 `Linux` 时，得到消息：`Calibrating delay loop.. ok -2396 BogoMips` failed 哪里/为什么延迟循环失败了？”

它没有失败。如果它通过了测试，你会看到 `Calibrating delay loop.. failed`。可能失败的是你机器上可能没有某些设备的驱动程序。在计算 `BogoMIPS` 评分后，所有设备驱动程序启动。首先是 `SCSI` 设备，然后是网络设备等。任何失败都会被报告。注意的是 `AHA15` 驱动程序。驱动故障（而不是 `BogoMIPS` 计算）的其他影响是系统崩溃、长时间等待和系统完全锁定。自 `Linux 1.2` 以来，错误信息有了改进，请升级到至少该版本以找出哪个特定的驱动程序故障。

## 7 关于兼容 CPU（Cyrix, NexGen, AMD 等）

类似 CPU 的缓存增强软件，有时被称为 `Bogosoft`。`Cyrix 5x86` 和 `6x86` CPU 的 `BogoMips` 通过分支预测（`BIOS` 选项）得到了极大提高。注意性能提升可能是微不足道的。有多个包可以调整 CPU，例如 `boostopatch`、`cx56x86` 和 `setx86`，它们在所有常用的存档处都可用。据报道，当内核使用 `486` 优化而不是 `Pentium` 优化时，`Cyrix 6x6` CPU 可能会获得更好的性能。

标记为 `Nx586` 的 `NexGen 386` 增强 CPU 被列为 `386` 类似，因为它们运行 `Pentium` 机器的事实与 `BogoMips` 无关。`AMD 5x86`（也被表示为 `AMD 486DX5`）是四倍 `486/33` 机器。它们与其他 `486` CPU 完全一致。`AMD K5` 和 `K6` 是 `Pentium` 类 CPU，具有它们的 `BogoMips` 倍数。

## 8 为什么要关注 BogoMips

我想补充的是，关注启动 `Linux` 时显示的 `BogoMips` 评分只有两个原因：

1. 查看它是否在特定处理器、频率以及潜在缓存的适当范围内。许多 CPU 容易出现设置错误：
   * `内存缓存设置` (`write-back` 对 `BogoMips` 来说是错误的，通常小于 5；`write-through` 很好)
   * `加速键` (`turbo-buttons`) （应该开启）
   * `BIOS 软件模拟缓存` （改为真实的缓存）
   * 类似的缓存和时钟相关事项
2. 查看你的系统是否比我的快。当然，这完全是错误的、不可靠的、毫无根据且完全没用的，但所有基准测试都证明了同样的问题。为什么不用呢？这种固有的愚蠢从未阻止过人们使用基准测试，不是吧？:-)

注意实际基准测试更严肃的原因在 `André D. Balsa` 的《`Linux Benchmarking Howto`》中有所讨论。

## 9 评分汇总

下表提供了各种系统的 `BogoMips` 评分（由约 700 个不同人的 800 多条记录组成，来自约 50 个国家）。注意这里的评分来自 `Linux` 的实际启动序列，非 `Linux` 系统部分除外。

### 9.1 配置异常或存在故障的 386 系统

| 系统 | BogoMips | 报告者 |
| :--- | :--- | :--- |
| `386DX/16` `387` 无缓存 | 0.57 | `H. Peter Levin` (`hpa@nu.edu`) |
| `386DX/25` | 0.82 | `P Wright` (`phil.wright@purplet.com.uk`) |
| `386DX/25` 无缓存 | 1.03 | `Mark A. Horton` (`mahmah@gmail.com`) |
| `386SX/1` | 1.5 | `Stefan Kramer` (`sk@galaxy.sun.sub.org`) |

### 9.2 普通总线系统：SX, DX, Nexgen

| 系统 | 基础Mbps | 报告员 |
| :--- | :--- | :--- |
| `386SX/16` | 1.6 | `Bill Davidsen` (`davisen@tmr.com`) |
| `386SX/20` | 1.87 | `Paul C. Dulany` (`pdulany@wam.edu.com`) |
| `386SX/20` | 2.45 | `Roger Harkess` (`roger@visi.com`) |
| `38DX/25(?)` `128c` | 6.03 | `Chuck Meo` (`meo@solbourne.com`) |
| `38DX/20` | 13 | `Ed Runnon` (`errunio@hubcap.clemson.com`) |
| `386SX/8` 降频 | 1.04 | `Andrew Coasta` (`chaos@wahnapitea.on.ca`) |
| `386SX/16` | 1.99 | `James Vahn` (`jvahn@short.circuit.com`) |
