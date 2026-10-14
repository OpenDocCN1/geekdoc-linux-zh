
# 进程与进程内存

## 关键点

- `vm_start` 和 `vm_end`：进程地址空间内区域的起始和结束虚拟地址。
- `vm_next` 和 `vm_prev`：进程 `vm_area_struct` 结构体列表内部的前向和后后指针。
- `vm_flags`：表示该区域是否可读、可写和/或可执行。
- `vm_pgoff`：映射区域的偏移量。
- `vm_file`：指向映射文件结构体的指针（如果是内存区域，则为 NULL）。

操作系统使用 `mmap` 持有的映射列表在文件系统中填充 `/proc/<pid>/maps`。在读取文件时显示内存映射对于调试和其他系统管理任务很有帮助。例如，以下是 Debian 机器上 `init` 进程作为分析内存的输出片段：

```
# cat /proc/1/maps
00000000-00409000 r-xp 00000000 08:01 1044487
      /sbin/init
00608000-00609000 rw-p 00008000 08:01 1044487
      /sbin/init
01dc1000-01de2000 rw-p 00000000 00:00 0
      [heap]
[snap]
7f988db1b8000-7f988db1b8a00 r-xp 00000000 08:01 130572
      /lib/x86_64-linux-gnu/libld-2.31.so.2
7f988db1a000-7f988db1a000 --v 00002000 08:01 130572
      /lib/x86_64-linux-gnu/libld-2.33.so.2
7f9881726000-7f9881727000 rw-p 00020000 08:01 130582
      /lib/x86_64-linux-gnu/libld-2.33.so
7f9881727000-7f9881728000 rw-p 00000000 00:00 0
7ffff23e60000-7ffff23e8100 rw-p 00000000 00:00 0
      [stack]
```

# 620 第三部分：Linux 内存取证

你可以将该命令的输出与 Volatility 的 `linux_proc_maps` 进行比较。该插件会遍历每个进程的 `task_struct->mm` 列表并报告特定区域的数据。

```
$ python vol.py --profile=linuxDebian-3_x64 -f defab.lime linux_proc_maps
Volatility Volatility Framework 2.4
PID Start End Flags Pgoff Major Inode Path
1 0x0000000004000000 0x000000000400900 r-x 0x0 8 1 1044487 /sbin/init
1 0x0000000006008000 0x0000000006009900 rw- 0x8000 8 1 1044487 /sbin/init
1 0x0000000001dc1000 0x000000001de2000 rw- 0x0 0 0 [heap]
1 0x000000007f9881d1800 0x00007f9881d1a00 r-x 0x0 8 1 130572 /lib/x86_64-linux-gnu/libld-2.13.so
1 0x000000007f9881d0a00 0x00007f9881d0a00 rw- 0x2000 8 1 130572 /lib/x86_64-linux-gnu/libld-2.13.so
1 0x000000007f9881d0b00 0x00007f9881d0b00 rw- 0x2000 8 1 130572 /lib/x86_64-linux-gnu/libld-2.13.so
[snip]
1 0x000000007f9881d7200 0x00007f9881d7000 rw- 0x0 0 0
1 0x00007fff23e5f000 0x00007fff23e8f000 rw- 0x0 0 0 [stack]
1 0x00007fff2fd3d00 0x00007fff2fd3d00 r-x 0x0 0 0
```

检查输出时，你可以看到 `init` 进程是从 `/sbin/init` 映射的，并且它使用的库之一是 `libld`，Volatility 可以映射栈和堆的范围。输出还包含每个区域的起始和结束地址，以及页权限、偏移量、主设备数和次设备数。

在事件响应期间，通常需要检查进程的映射以寻找代码注入的迹象。如果共享库从 `/tmp` 加载或不是普通库，则立即可疑。为了快速在进程中寻找恶意库的迹象，可以在干净的 Linux 安装上创建一个所有共享库的白名单，然后让 Volatility 输出不在白名单中的共享库。

进程映射对于验证进程从哪里执行有用，即使恶意软件也能操作 `ps` 命令显示的数据。例如，内核从用户进程的栈读取命令行参数并通过 `/proc/<pid>/cmdline` 文件导出结果。`ps` 读取此文件进行收集。在本章中你将检查恶意软件如何将其参数覆盖为完整路径。然而，操作进程内存映射要困难得多，因为 `vm_area_struct` 结构存储在内核内存中。

# 恢复内存区域

在分析期间，你可能经常提取进程的内存映射。为了协助这一点，Volatility 提供了 `linux_dump_maps` 插件。你可以导出所有进程的映射，也可以使用 `-p` 指定一个或多个 PID。你还可以使用 `-s ADDR` 只提取从指定地址开始的区域。你必须指定 `-d` 来告诉 Volatility 写入提取文件的目录。

在以下示例中，使用 `linux_dump_maps` 从内存转储中提取 `init` 二进制文件的执行段：

```
$ python vol.py --profile=LinuxDebian-3_x64 -f debian.lime linux_dump_maps -p 1 -s 0x400000 -D dump
Volatility Volatility Framework 2.4
Task VM Start Length Path
1 0x0000000004000000 0x000000000400900 0x900 dump/task.1.0x400000.vma
```

```
$ dump/task.1.0x400000.vma ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared), stripped
```

## 622 第三部分：Linux 内存取证

以下显示了该插件在 Debian 内存样本上的输出：

```
$ python vol.py --profile=LinuxDebian-3_2x64 -f debian.lime_linux_psaux
Volatility Foundation Volatility Framework 2.4
Pid U Gid Arguments
1 0 0 init [2]
2 0 0 [kthread]
3 0 0 [ksoftird/u:0]
5 0 0 [kworker/u:0]
6 0 0 [migration/0]
7 0 0 [watchdog/0]
[snip]
1851 0 0 dhclient -vf /run/dhclient.eth0.pid \
-f /var/lib/dhcp/dhclient.eth0.leases eth0
/usr/bin/rsyslog -c5
2061 0 0 [flush:8:0]
2094 0 0 /usr/bin/acpid
2101 0 0 /usr/bin/apache2 -k start
2137 0 0 /usr/bin/apache2 -k start
2381 33 107 /usr/lib/postgresql/9.1/bin/postgresql \
-D /var/lib/postgresql/9.1/main \
-c /etc/postgresql/9.1/main/postgresql.conf
2384 104 107 postgres: writer process
2385 104 107 postgres: wal process
2386 104 107 postgres: autovacuum process
8643 0 0 insmod linux-amd64.ko format=debian.lime
```

在输出中，你可以看到几个进程具有重要的配置选项作为工作目录，以及用于访问被分析内存的给定参数。恶意进程通常会从命令行读取参数，在这些情况下，我们使用 `linux_psaux` 来恢复有关特定感染的信息。以下显示了一个具有网络能力的案例的输出：
