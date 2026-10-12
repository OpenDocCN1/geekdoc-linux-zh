
model name : `Intel(R) Xeon(R) E5-2670 @`
stepping : `7`

cpu MHz : `1200.00`

cache size : `2048`

physical id : `1`

siblings : `8`

core id : `7`

apicid : `46`

initial apicid : `46`

fpu : yes

```
Copyright ©Intel Corporation. 保留所有。
```

## 第 4 章 深入研究系统

fpu_exception : yes

cpuid level : `13`

flags : `vme de pse msr acpi pae avx tsc mce depi dse mov cx8 acpi cm clflush dts acpi sse2 tm nx sse3 sse4_1 sse_2 xapic popcnt xsave lahf lm osopt prb tm_shadow ept vplid`

bogmips : `5187.41`

clflush size : `64`

cache_alignment : `64`

address sizes : `46 bits physical, 48 bits virtual`

- `/proc/interrupts` – 该文件记录每个 CPU 的中断次数、注册的 I/O 设备的中断，以及非掩码中断（NMI）、TLB 刷新等其他中断。如果你怀疑某个硬件资源发生故障，或者为了检查特定子系统（例如网卡或 ATA 接口）的性能，应该咨询这些。在具有大量内核的系统中，输出可能难以阅读，因为将不可避免地溢出控制台缓冲区。简化如下（为了简洁）：

| CPU0 | CPU1 | CPU2 | ... | CPU15 | timer |
|---|---|---|---|---|---|
| 94: | 2 | 0 | 0 | 0 | IR-PCI-MSI-edge | eth0 |
| 95: | 9430734 | 0 | 0 | 0 | IR-PCI-MSI-edge | eth1 |
| NMI: | 17771 | 11683 | 2761 | 950 | 非掩码中断 |

- `/proc/kcore` – 此文件代表系统的物理内存（ELF 格式）。使用调试器和未处理的内核二进制文件，可以读取并检查内核结构的当前状态。

# 使用 /proc

`/proc/meminfo` – 报告系统内存使用的的统计信息，正如我们在上一章节中简要提到的那样。它报告了大量的字段（参见 `/proc/sys/vm/*` 文档），包括完全可用 RAM、空闲内存、缓冲区、缓存、缓存交换（cached swap）、不同状态下的内存页数量。完整列表超出了本章的范围，但在排查系统问题时，其中的部分可能非常有用。

```
cat /proc/meminfo
MemTotal:       5939324 kB
MemFree:        5924976 kB
Buffers:        434716 kB
Cached:         5079052 kB
SwapCached:     0 kB
Active:         5125192 kB
Inactive:       502832 kB
Active (anon):  114372 kB
Inactive (anon): 64 kB
Active(file):   5010820 kB
Inactive(file): 502768 kB
Unevictable:    0 kB
Mlocked:         0 kB
SwapTotal:      67111420 kB
SwapFree:       67111420 kB
Dirty:          120 kB
Writeback:      0 kB
AnonPages:      114284 kB
```

# 第4章 深入研究系统

| Mapped: | 24368 kB |
| --- | --- |
| Shmem: | 180 kB |
| ... | |

> 版权所有 ©Intel Corporation。保留所有权利。

考虑以下示例：你的其中一个用户抱怨说，在某台系统上进行长时间的密集 I/O 活动后，他们观察到响应速度下降。你可以在受影响的单机上确认这些症状，但无法立即判断为什么是该系统而不是其他系统，尽管工程师们运行着相同的负载和 I/O 模式。分析这类问题并不容易，需要对系统内存管理有深入的理解，如果你知道从哪里查看，可以将调查缩小到一个更可管理的范围。

稍后我们将讨论一些概念，现在让我们简要进入内存空间。Linux 虚拟内存（VM）子系统可以通过 `/proc/sys/vm` 访问。该子系统控制当内存达到阈值时的行为。例如，“dirty”参数定义了何时缓存应该被刷到磁盘。策略包括总内存的百分比以及过期时间。

经验丰富的系统管理员可能会立即发现问题的可能源。由于某些参数是以总内存的百分比表示的，具有不同值的系统不会出现相同的问题。如果你将持续 I/O 负载下的性能下降进行比较，你可能会发现 `vm` 树下的不同值。再次，这些值与其他系统相比非常有用，因为它们提供了洞察。此外，你可以观察 `meminfo` 结果。

- `/proc/modules` - 当前加载的所有内核模块列表。通过 `lsmod` 命令提供相同的信息。
- `/proc/mounts` - 所有挂载点的列表。该信息与 `/etc/mtab` 文件相关联。在某些系统上，后者可能是指向该伪文件系统的符号链接。该列表在排查挂载和卸挂载问题时非常有用。
- `/proc/slabinfo` – 此文件提供了内核缓存的信息。虽然 `meminfo` 变量提供了 slab 池的总大小，但内容最好是使用 `slabtop` 或 `slabinfo` 命令进行解析。

## 进程空间

让我们回到进程映射。我们已经简要讨论过 `/proc/PID/maps` 变量，但它们比看一眼有用得多，特别是当你知道某个应用程序正在做什么时。这是一个进程示例：

```
#cat /proc/2971/maps
0000000-004b0000 r-xp 00000000 08:06 24525 /usr/sbin/avahi-daemon
0061a000-006b0000 r--p 00010000 08:06 24525 /usr/sbin/avahi-daemon
0061b000-006c0000 rw-p 0001b000 08:06 24525 /usr/sbin/avahi-daemon
0061c000-0063d000 rw-p 00000000 00:00 0 [heap]
0063d000-0069f000 rw-p 00000000 00:00 0 [heap]
7fd281dde000-7fd281ff000 r-xp 00000000 08:02 37 /lib64/libns1-2.so
7fd281dff000-7fd281ff200 r--p 00015000 08:02 37 /lib64/libns1-2.so
7fd2824e0000-7fd28257d000 r-xp 00000000 08:02 26 /lib64/libc-2.1.so
7fd28257d000-7fd28277d000 r--p 00016000 08:02 26 /lib64/libc-2.1.so
7fd28277d000-7fd28781000 rw-p 00017000 08:02 26 /lib64/libc-2.1.so
7fd28781000-7fd28782000 rw-p 00017300 08:02 26 /lib64/libc-2.1.so
7fd287820000-7fd2879e0000 r-xp 00000000 08:02 26 /lib64/libthread-2.1.so
7fd283788000-7fd283879000 rw-p 00000000 00:00 0 [stack]
7ffff11268000-ffffffff r-xp 00000000 00:00 0 [vdso]
ffff11370000-ffff11371000 r-xp 00000000 00:00 0 [vso]
```
