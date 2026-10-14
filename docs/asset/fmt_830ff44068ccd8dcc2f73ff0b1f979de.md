
> <4>[3008.749490] [LIME] DIO: 1
> <4>[3008.749501] [LIME] FORMAT: Disk...
> <4>[3008.749504] [LIME] Initializing Disk...
> <4>[3008.749579] [LIME] Direct IO may not be supported on this file system.
> <4>[3008.749585] [LIME] Direct IO Disabled

这两行与 PID 为 2640 的 Xnest 进程有关。在这种情况下，Xnest 并不是流行的 X1 显示服务器；它是 P2 中一个命名巧妙的组件。日志显示 Xnest 尝试从偏移量 0 到 0x8000000 之间的 `/dev/mem` 读取，但被拒绝了。如果成功，此访问将允许 Xnest 读取整个 GB 范围的内核内存。在下一行中，Xnest 显示了之前被拒绝的页面，其缓存属性与操作系统最初设置的属性不同。

运行进程的分析显示，P2 启动了 Xnest 进程，但调试日志中显示的 PID 是 2660（而不是 2640）：

``` 
$ python vol.py --profile=LinuxDebian3_286 -f before.p2.line
linuxlist > pslist-before
Volatility Volatility Framework 2.4
```

``` 
$ python vol.py --profile=LinuxDebian3_286 -f after.p2.line
linuxlist > pslist-after
Volatility Volatility Framework 2.4
```

``` 
$ diff pslist-before pslist-after
70c70,71
> 0xf5bcbcb5a0 insmod 2627 0 0x360e3000 2014-02-02 05:36:37
> 0xf5a2a240 Xnest 2660 0 42779 0x35bb000 2014-02-02 05:41:15
> 0xf5a7ef20 insmod 2664 0 0x35a2600 2014-02-02 05:42:15
```

# 760 第三部分：Linux内存森林

当你研究 P2 的动态分析时，你会看到 PID 发生了变化。还有一个 `insmod` 进程，但预计 `insmod` 用于在两次内存捕获之间加载和卸载 MIME。然而，看到 `insmod` 促使我们检查是否有新的内核模块。遗憾的是，P2 安装前后的模块列表完全相同。`linux_check_modules` 插件无法找到任何存储在 sysfs 模块中的模块。在本章中，你将学到 P2 实际上执行了一个可加载内核模块 (LKM)，但其方式并容易通过内存取证进行追踪。

这些调试信息来自 Lime 在捕获内存时报告其启动状态。

## 检查 Xnest 进程

检查 Xnest 进程 (PID 2660) 发现了许多有趣的伪迹。首先，运行进程的名称 (Xnest)存储在 `task_struct` 的 `comm` 成员中，与 `linux_psaux` 显示的不同：

``` 
$ python vol.py --profile=LinuxDebian3_2x86 -f after.p2.lime linux_psaux -p 2660
Volatility Foundation Volatility Framework 2.4
```

| Pid | Uid | Gid | Arguments |
| --- | --- | --- | --- |
| 2660 | 0 | 42779 | [ata/0] |

恶意软件在用户态下重写了它的命令行参数，这是你在第 21 章学到的技巧。在这种情况下，P2 试图通过将名称包括在括号中并选择许多 Linux 发行版中常见的现有内核线程名称来伪装成内核线程。注意，尽管这在 Volatility 插件中是隐藏的，但在系统调用中是可见的。

## 揭露伪内核线程

要证明 PID 2660 不是内核线程，可以使用几种方法。首先，`linux_pstree` 显示该进程不是 `kthread`，它是所有进程的父进程：

``` 
$ python vol.py --profile=LinuxDebian3_2x86 -f after.p2.lime linux_pstree
Volatility Foundation Volatility Framework 2.4
```

| Name | Pid | Uid |
| --- | --- | --- |
| init | 1 | |
| [Xnest] | 2660 | 0 |
| [kthread] | 2 | 0 |
| [softirqd/0] | 3 | 0 |
| [kworker/u:0] | 5 | 0 |
| [migration/0] | 6 | 0 |
| [watchdog/0] | 7 | 0 |
| [migration/1] | 8 | 0 |
| [kworker/1:0] | 9 | 0 |
| [softirqd/1] | 10 | 0 |
| [cpuset] | 13 | 0 |

## 确定真实的二进制文件

接下来，进程拥有用户内存映射，而内核线程没有：

``` 
$ python vol.py --profile=LinuxDebian3_286 -f after.p2.line linux_map -p 2660
| Start | End | Flags | Poff | Minor | Inode | File Path |
| --- | --- | --- | --- | --- | --- | --- |
| 2660 | 0x0804800 | 0x0805c00 | r-x | 0x0 | 1 | 878315|root/.p2f |
| 2660 | 0x0805c00 | 0x0805d00 | rx | 0x1400 | 8 | 878315|root/.p2f |
| 2660 | 0x0805d00 | 0x0805f00 | rw | 0x0 | 0 | |
| 2660 | 0xaf6ee00 | 0xaf6f100 | rx | 0x0 | 0 | |
| 2660 | 0xb76f1000 | 0xb770900 | rx | 0x0 | 0 | |
| 2660 | 0xb770900 | 0xb77a000 | r-x | 0x0 | 0 | |
| 2660 | 0xb770c00 | 0xb78e0000 | rx | 0x0 | 0 | [stack]|
```

在此输出中，该进程的“二进制文件”是 `/root/.p2f`。一个指标是起始地址 0x0804800，这是32 位 Linux 系统上 ELF 函数的初始执行。你也可以检查进程的 `task_struct.mm_start_code` 值来验证它包含 0x0804800。因此，`/root/.p2f` 是原始二进制文件的名称——它不是共享库，也没有映射到进程空间。事实上，该进程没有共享库，它是静态编译的。

大多数普通系统都是动态链接的，并依赖共享库来实现功能和 API。恶意软件像 P2 一样通常是静态链接的，以增加逆向工程和动态分析的难度并提高移植性。

此外，在输出中，你可以看到几个区域被标记为可读、可写和可执行。正常的映射不应既是可写又是可执行的。这种映射的存在可疑，值得进一步调查。

## Socket 文件描述符

使用 `linux_lsof` 插件进一步检查进程打开的文件发现了可疑伪迹。默认的 stdin、stdout 和 stderr 映射到 `/dev/null`。文件描述符 3 不，描述符 4 和 5 是 socket。在正常的后门程序中，你应该看到描述符 0、1 和 2 映射到 socket 以便进行网络通信。

``` 
$ python vol.py --profile=LinuxDebian3_2x86 -f after.p2.lime linux_lsof -p 2660
Volatility Foundation Volatility Framework 2.3.1
```

| Pid | FD | Path |
| --- | --- | --- |
| 2660 | 0 | `/dev/null` |
| 2660 | 1 | `/dev/null` |
| 2660 | 2 | `/dev/null` |
| 2660 | 4 | socket: [5715] |
| 2660 | 5 | socket: [5716] |

在检查 `linux_netstat` 输出后，socket 变得奇怪，因为显示了 socket 正在互相连接：

``` 
$ python vol.py --profile=LinuxDebian3_2x86 -f after.p2.lime linux_netstat
<snip>
```
