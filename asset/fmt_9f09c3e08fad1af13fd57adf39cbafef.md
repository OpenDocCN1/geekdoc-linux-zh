
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| root | 8 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [migration/1] |
| root | 9 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [ksoftirqd/1] |
| root | 10 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [watchdog/1] |
| root | 11 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [migration/2] |
| root | 12 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [migration/2] |
| root | 13 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [ksoftirqd/2] |
| root | 14 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [watchdog/2] |
| root | 15 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [migration/3] |
| root | 16 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [migration/3] |
| root | 17 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [ksoftirqd/3] |
| root | 18 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [watchdog/3] |
| root | 19 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [events/0] |
| root | 20 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [events/1] |
| root | 21 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [events/2] |
| root | 22 | 0.0 | 0.0 | 0 | S | 00:27 | 0:00 | [events/3] |

查看 `ps` 输出时，你可能会发现两种进程。有些名称在括号内，另一些不是。如果一个进程名称在方括号之间，它是内核的一部分。其他的都是“正常的”。如果你想了解更多关于某个进程以及它是什么，有两种方法：检查对应的 `/proc` 目录。例如，`/proc/5658` 提供 PID 为 5658 的进程信息。在这个目录中，你会找到关于该进程内存映射的更多文件。正如列表 17.12 所示，这些信息非常详细。它包含了该进程使用的精确内存地址，甚至包含了与该进程相关的子程序和库。

### 列表 17.12：`/proc/[pid]/maps` 提供特定进程的内存利用详细信息

```
root@1:~# cat /proc/5658/maps
b7b8c1000-b78c4000 rw-s 00000000 00:09 14414 /dev/zero (deleted)
b7b8c1400-b78c4400 r-xp 00000000 fe:00 508829 /lib/security/pam_limits.so
b7b8c4400-b78c5000 r-xp 00002000 fe:00 508829 /lib/security/pam_limits.so
b7b8c5000-b78c7000 r-xp 00002000 fe:00 508834 /lib/security/pam_mail.so
b7b8c7000-b78d3000 rw-p 00011000 fe:00 508834 /lib/security/pam_mail.so
b7b8c3000-b78d4000 r-xp 00000000 fe:00 508831 /lib/security/pam_unix.so
b7b8d3000-b78d4000 rw-p 0000b000 fe:00 5088351 /lib/security/pam_unix.so
b7b8d4000-b78e0000 rw-p b78d4000 00:00 0
```

```
b7eb7000-b7eb8000 r-xp 00000000 fe:00 5808338 /lib/security/pam_nlogin.so
b7eb8000-b7eb8000 rw-p 00000000 fe:00 5808338 /lib/security/pam_nlogin.so
b7eb9000-b7eb0000 rw-p b7eb9000 00:00 0
b7eb0000-b7eb0000 r-xp 00000000 00:00 0 [vdso]
b7ebc000-b7ed6000 r-xp 00000000 fe:00 5808145 /lib/1d-2.7
b7ed6000-b7ed8000 r-xp 00019000 fe:00 5808145 /lib/1d-2.7
b7ed8000-b7f31000 r-xp 00000000 00:00 1077630 /usr/sbin/ssh
b7f31000-b7f33100 r-xp 00005900 00:00 1077630 /usr/sbin/ssh
b7f33100-b7f5b500 rw-p b7f5b500 00:00 [heap]
bff9a000-bffaf000 r-xp bffeb00 00:00 [stack]
```

查找特定进程的另一种方法是使用 `pmap` 命令。该命令通过 `/proc/[PID]/maps` 获取信息，类似于 `ps aux` 显示的内存摘要。`pmap` 还能让你看到进程使用了哪些内存地址。列表 17.13 是该工具的输出示例。

### 列表 17.13：`pmap` 命令 `/proc/[PID]/maps` 提供信息
