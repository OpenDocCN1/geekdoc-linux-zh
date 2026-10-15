
# 594 附录 C • HP-UX 到 Linux 参考表

| `setsid` | `setsid` | 创建会话和进程组 ID。 |
| `setsockopt` | `setsockopt` | 设置套接选项。 |
| `setimeofday` | `setimeofday` | 设置日期和时间。 |
| `setune` | None | 设置内核调优参数。 |
| `setune_txn` | None | 在事务中设置内核调优参数。 |
| `setuid` | `setuid` | 设置用户和组 ID。 |
| `setname` | None | 设置节点名（系统名）。 |
| `shm_open` | `shm_open` | 创建/打开共享内存对象。 |
| `shm_unlink` | `shm_unlink` | 解除共享内存对象。 |
| `shmat` | `shmat` | 将共享内存附加到数据段。 |
| `shmctl` | `shmctl` | 共享内存控制操作。 |
| `shmdt` | `shmdt` | 从数据段分离共享内存。 |
| `shmget` | `shmget` | 获取共享内存段。 |
| `shmop` | `shmop` | 共享内存操作。 |
| `shutdown` | `shutdown` | 关闭套接。 |
| `sigaction` | `sigaction` | 检查并更改信号动作。 |
| `sigaltstack` | `sigaltstack` | 设置和或获取信号备用栈上下文。 |
| `sigblock` | `sigblock` | 阻塞信号。 |
| `sighold, sigrelse` | `sighold, sigrelse` | 信号管理。 |
| `signore` | `signore` | 信号管理。 |
| `siginterrupt` | `siginterrupt` | 允许信号中断函数。 |
| `sigpause` | `sigpause` | 信号管理。 |

| HP-UX 系统调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `signal` | `signal` | 4.2 兼容 BSD 的进程控制设施。 |
| `sigpending` | `sigpending` | 检查挂起的信号。 |
| `sigprocmask` | `sigprocmask` | 检查并更改阻塞信号。 |
| `sigqueue` | `sigqueue` | 向进程队列信号。 |
| `sendsend` | None | 向进程或进程组发送信号。 |
| `sigendsset` | None | 向进程组发送信号。 |
| `sigsetmask` | `sigsetmask` | 设置当前信号掩码。 |
| `sigspace` | None | 确保足够的信号栈空间。 |
| `sigstack` | `sigstack` | 设置/获取信号栈上下文。 |
| `siguspend` | `siguspend` | 等待信号。 |
| `sigtimedwait` | `sigtimedwait` | 检查并更改信号动作。 |
| `sigvec` | `sigvec` | 4.2 兼容 BSD 的进程控制设施。 |
| `sigvector` | None | 软件信号设施。 |
| `sigwait` | `sigwait` | 检查并更改信号动作。 |
| `sigwaitinfo` | `sigwaitinfo` | 检查并更改信号动作。 |
| `socket` | `socket` | 创建通信端点。 |
| `socketpair` | `socketpair` | 创建一对连接的套。 |
| `sprofil` | None | 离散文本空间的执行时间剖析。 |
| `stat` | `stat` | 获取文件状态。 |
| `stat64` | `stat64` | 支持大文件的非 POSIX 标准 API 接口。 |
| `statfs` | `statfs` | 获取文件系统统计信息。 |
| `statvfs` | `statvfs` | 获取文件状态。 |
| `statvfs64` | `statvfs64` | 支持大文件的非 POSIX 标准 API 接口。 |

## C.3 HP-UX 和 Linux 系统调用对比表

| HP-UX 系统调用 | Linux 等效函数 | 描述 |
| --- | --- | --- |
| `stime` | `stime` | 设置时间和日期。 |
| `stream` | None | 标准系统调用的流增强。 |
| `stty` | `stty` | 控制终端设备（兼容 bell 版本 6）。 |
| `swapcontext` | `swapcontext` | 操作用户上下文。 |
| `swapon` | `swapon` | 为交替分页和交换添加交换设备。 |
| `symlink` | `symlink` | 创建文件创建符号链接。 |
| `sync` | `sync` | 更新磁盘。 |
| `sysconf` | `sysconf` | 获取可配置的系统变量。 |
| `sysfs` | `sysfs` | 获取文件系统类型信息。 |
| `time` | `time` | 获取时间。 |
| `timer_create` | `timer_create` | 创建定时器。 |
| `timer_delete` | `timer_delete` | 删除定时器。 |
| `timer_getoverrun` | `timer_getoverrun` | 返回定时器过期计数。 |
| `timer_gettime` | `timer_gettime` | 存储定时器过期和重载值。 |
| `timer_settime` | `timer_settime` | 设置定时器过期。 |
| `times` | `times` | 获取进程和子进程时间。 |
| `truncate` | `truncate` | 将文件截断为指定长度。 |
| `truncate64` | `truncate64` | 支持大文件的非 POSIX 标准 API 接口。 |
| `ttrace` | None | 多线程进程的跟踪设施。 |
| `ttrace_wait` | None | 等待 `ttrace()` 请求。 |
| `tuneinfo2` | None | 获取有关内核可调参数的详细信息。 |
| `ualarm` | `ualarm` | 设置间隔定时器。 |
| `ulimit` | `ulimit` | 获取设置用户限制。 |

## 附录 C • HP-UX 到 Linux 参考表

| HP-UX 系统调用 | Linux 等效函数 | 描述 |
| --- | --- | --- |
| `umask` | `umask` | 设置获取文件创建掩码。 |
| `unmount` | `umount, umount` | 卸载文件系统。 |
| `uname` | `uname` | 获取计算机系统信息；设置节点名（系统名）。 |
| `unlink` | `unlink` (根据 SUSv3 规定可能返回 EISDIR 而不是 EPERM) | 删除目录项；删除文件。 |
| `usleep` | `usleep` | 暂停执行一段时间。 |
| `ustat` | `ustat` | 获取挂载的文件系统统计信息。 |
| `utime` | `utime` | 设置文件访问和修改时间。 |
| `utimes` | `utimes` | 设置文件访问和修改时间。 |
| `vfork` | `vfork` | 产生新进程（使用 `fork()` 代替）。 |
| `vfsmount` | None | 挂载文件系统。 |
| `wait` | `wait` | 等待子进程停止或终止。 |
| `wait3, wait4` | `wait3` (按 SUSv2 指定工作，除非 WCONTINUED 是可选的) `wait4` (等待进程终止，BSD 风格) | 等待子进程状态改变。 |
| `waitid` | `waitid` | 等待子进程状态改变。 |
| `waitpid` | `waitpid`—按 SUSv3 指定工作，除非 WCONTINUED 和 WIFCONTINUED 是可选的 | 等待子进程停止或终止。 |

## C.3 HP-UX 和 Linux 系统调用对比表

| HP-UX 系统调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `write` | `write` | 向文件写入数据。 |
| `writev` | `writev` | 向文件写入数据。 |

6 HP-UX 参考章节 2: 系统调用 HP-UX 11i v2

7 www.unix.org/version3/

8 某些标志可能不兼容。

9 Linux 页面中未记录。请查看 `/usr/include/mman.h`。

10 在 `mqueue.h` 中定义的消息队列函数在定义 `MESSAGE_PASSING` 的系统中可用。SUSE 系统未定义，因此 `mq_*` 函数不可用。

11 使用不同的参数。

12 www.unix.org/version3/

## C.4 HP-UX 和 Linux API 对比表

| HP-UX 库调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `a64, a64a` | `a64, a64` | 长整数和 ASCII 字符串之间的转换 |
