
| CPU | %user | %nice | %system | %steal | %idle |
| --- | --- | --- | --- | --- | --- |
| all | 4.46 | 0.01 | 0.67 | 0.31 | 0.00 | 94.55 |

| Device | tps | kB_read/s | kB_wrtn/s | kB_read | kB_wrtn |
| --- | --- | --- | --- | --- | --- |
| sda | 4.67 | 7.28 | 49.86 | 9493727 | 6501716 |
| sde | 0.00 | 0.00 | 0.00 | 1230 | 0 |

顶部的 `avg-cpu` 部分报告了在本章中与其他单元相同的 CPU 利用率信息，因此请跳到底部，它会显示每个设备的以下信息：

- 每秒平均数据传输次数
- `kB_read/s` 每秒平均千字节数
- `kB_wrtn/s` 每秒平均写入千字节数
- `kB_read` 读取的总千字节数
- `kB_wrtn` 写入的总千字节数

与 `vmstat` 的另一个相似之处是，你可以提供参数，例如 `iostat 2`，每两秒更新一次。当使用间隔时，你可能想通过使用 `-d`（例如 `iostat -d 2`）仅显示设备报告。

默认情况下，`iostat` 输出省略了分区信息。要显示所有分区信息，请使用 `-p ALL`。由于典型系统有许多分区，你会得到大量的输出。以下是你可能看到的内容部分：

```
$ iostat -p ALL

---

Device: 	tps  kB_read/s kB_wrtn/s kB_read  kB_wrtn

sda    4.67 7.27 49.83 946139 65051472

sda1   4.38 7.16 49.51 935269 64635440

da2   0.00 0.00 0.00 6 0

sda5   0.00 0.01 0.32 141884 4160932

scd0   0.00 0.00 0.00 0 0

---

sde    0.00 0.00 0.00 1230 0
```

在这个示例中，`sda1`、`sda2` 和 `sda5` 都是 `sda` 磁盘的分区，因此读取和写入列会有一些重叠。然而，分区列的总和并不一定等于磁盘列。虽然从 `sda1` 读取也被算作从 `sda` 读取，但请记住，你可以直接从 `sda` 读取，例如读取分区表。

如果你需要深入查看单个进程占用的 I/O 资源，`iotop` 工具类似于使用 `top`。它生成一个持续更新的显示，显示正在使用 I/O 的进程，并在顶部有一个总体摘要：

```
$ iotop

Total DISK READ: 4.76 K/s | Total DISK WRITE: 333.3 K/s

TID PRIO USER DISK READ DISK WRITE SWAP IO

260 be/3 root 0.00 B/s 38.00 K/s 0.00% 6.98% [jbd:sda-1]

2611 be/4 user 4.76 K/s 10.32 K/s 0.00% 0.21% zeitgeist-daemon

2636 be/4 user 0.00 B/s 84.12 K/s 0.00% 0.20% zeitgeist-fts

1329 be/4 user 0.00 B/s 65.87 K/s 0.00% 0.03% soffice.bash-

pipe-6

6845 be/4 user 0.00 B/s 812.63 B/s 0.00% 0.00% chromium-browser

19069 be/4 user 0.00 B/s 812.63 B/s 0.00% 0.00% rhythmb
```

除了命令和读取/写入，注意这里是 `TID` 列而不是 `PID` 列。`iotop` 工具是少数显示进程的工具之一。`PRIO` 列表示 I/O 优先级。它与你看到的 CPU 优先级类似，但它影响内核如何调度进程的 I/O 读取和写入。在 `be/4` 中，`be` 是调度类，`4` 是优先级级别。与 CPU 优先级一样，数字越小越重要；例如，内核允许更多的 I/O。

## 8.6 控制组 (cgroups)

到为止，你已经看到了如何监控资源使用情况，但如果你想随时间监控它呢？有几个工具可以做到，例如 `top` 和 `iotop`。不过，你可以使用 `pidstat` 查看随时间的变化，例如：

```
$ pidstat 2
```

| CPU | %user | %nice | %system | %steal | %idle |
| --- | --- | --- | --- | --- | --- |
| all | 4.46 | 0.01 | 0.67 | 0.31 | 0.00 | 94.55 |

| Device | tps | kB_read/s | kB_wrtn/s | kB_read | kB_wrtn |
| --- | --- | --- | --- | --- | --- |
| sda | 4.67 | 7.28 | 49.86 | 9493727 | 6501716 |
| sde | 0.00 | 0.00 | 0.00 | 1230 | 0 |

基本思想是将进程放入 cgroup 中，这允许你管理它们消耗的资源。例如，如果你想限制一组进程累积消耗的内存量，cgroup 可以做到这一点。在创建 cgroup 后，你可以将进程添加到其中，然后使用控制器来改变进程的行为。例如，有一个 `cpu` 控制器允许你限制处理器时间，以及一个内存控制器，等等。

### 8.6.1 区分 cgroup 版本

cgroups 有两个版本，1 和 2，遗憾的是，目前两个版本都在使用，并且可以在系统上同时配置，导致了困惑。除了功能集有所不同，版本之间的结构差异可以总结如下：

- 在 cgroups v1 中，每种类型的控制器（`cpu`、`内存` 等）都有自己的一组 cgroups。一个进程每个控制器属于一个 cgroup，这意味着一个进程可以属于多个 cgroup。
- 在 cgroups v2 中，一个进程只属于一个 cgroup。你可以为每个 cgroup 设置不同类型的控制器。

为了视觉化这种差异，考虑三组进程 A、B 和 C。我们想对它们每组使用 `cpu` 和内存控制器。图 8-1 显示了 cgroups v1 的示意图。我们总共六个 cgroup，因为每个 cgroup 限于单个控制器。

| CPU 控制器 | 内存控制器 |
| --- | --- |
| cgroup A1 | cgroup A2 |
| cgroup B1 | cgroup B2 |
| cgroup C1 | cgroup C2 |

图 8-1: cgroups v1。一个进程每个控制器属于一个 cgroup。

# Linux 工作原理（早期访问） © 2021 由 Brian Ward

图 8-2 显示了如何在 cgroups v2 中进行操作。我们只需要三个 cgroups，因为可以在每个 cgroup 上设置多个控制器。

| cgroup A | cgroup B | cgroup C |
| --- | --- | --- |
| CPU 控制器 | CPU 控制器 | CPU 控制器 |
| 内存控制器 | 内存控制器 | 内存控制器 |

图 8-2：cgroups v2。进程可能只属于一个 cgroup。

可以通过查看 `/proc/<pid>` 下的 `cgroup` 文件列出任何进程的 v1 和 v2 cgroups。你可以运行以下命令开始查看 shell 的 cgroups：

```bash
$ cat /proc/self/cgroup
12:rdma:
11:net_cls_net_prio:
10:perf_event:
9:cpuset:
8:cpu,cpuacct:/user.slice
7:blkio:/user.slice
6:memory:/user.slice/user-1000.slice/session-2.scope
5:pids:/user.slice/user-1000.slice/session-2.scope
4:devices:/user.slice
3:freezer:
2:hugetlb:/testgroup
1:name=systemd:/user.slice/user-1000.slice/session-2.scope
0:/user.slice/user-1000.slice/session-2.scope.
```
