
表 A.1 按字母顺序排列系统调用（继续）

| 系统调用 | 描述 |
| --- | --- |
| `getuid` | 获取实际用户 ID (m+c) |
| `glty` | 尚未实现 (i) |
| `idle` | 为交换创建进程 (mc) |
| `init_module` | 插入可加载内核模块 (-) |
| `ioctl` | 操作字符设备 (mci) |
| `ierm` | 设置某些 `o` 的权限 (m-c) |
| `iopl` | 设置所有 `o` 的权限 (m-c) |
| `ipc` | 进程间通信 (--) |
| `kill` | 向进程发送信号 (m+c) |
| `killpg` | 向进程组发送信号 (mcl) |
| `klog` | 系统日志 (-) |
| `link` | 为现有文件创建硬链接 (m+c) |
| `listen` | 监听 `socket` 连接 (m!lc) |
| `lseek` | 查找大文件 (-) |
| `lock` | 尚未实现 (!) |
| `lseek` | 更改文件描述符的位置 (m+c) |
| `lstat` | 获取文件状态 (mc) |
| `mkdir` | 创建目录 (m+c) |
| `knod` | 创建设备 (mc) |
| `mmap` | 将文件映射到内存 (mc) |
| `modify_ldt` | 读取或写入表 (-) |
| `mount` | 挂载文件系统 (mc) |
| `mprotect` | 读取、写入或执行内存 (-) |
| `mpx` | 尚未实现 (!) |
| `msgctl` | `ipc` 消息控制 (m'c) |
| `msget` | 获取 `ipc` 队列 ID (m'c) |
| `msgrcv` | 接收 `ipc` 消息 (m'c) |
| `msgsnd` | 发送 `ipc` 消息 (m'c) |
| `munmap` | 从内存取消映射文件 (mc) |
| `nice` | 更改进程优先级 (mc) |
| `oldstat` | 不再存在 |
| `oldoldname` | 不再存在 |
| `oldstat` | 不再存在 |
| `oldname` | 不再存在 |
| `open` | 打开文件 (m+c) |
| `pathconf` | 获取文件信息 (m!c) |
| `pause` | 等待信号 (m+c) |
| `personality` | 更改当前执行域 (-) |
| `phys` | 尚未实现 (mi) |
| `pipe` | 创建管道 (m+c) |
| `proif` | 尚未实现 (!) |
| `profile` | 执行时间分析 (m!c) |
| `trace` | 跟踪子进程 (mc) |

表 A.1 按字母顺序排列系统调用（继续）

| 系统调用 | 描述 |
| --- | --- |
| `quoactl` | 尚未实现 () |
| `read` | 从文件中读取数据 (m+c) |
| `readv` | 从文件中读取数据块 (m+c) |
| `readdir` | 读取目录 (m+c) |
| `readlink` | 获取符号链接的内容 (mc) |
| `reboot` | 重启或切换 (t-mc) |
| `recv` | 从已连接 `socket` 接收消息 (m+c) |
| `recvfrom` | 从 `socket` 接收消息 (m+c) |
| `rename` | 移动/重命名空目录 (m+c) |
| `rmdir` | 删除空目录 (m+c) |
| `shrk` | 见 `brk` (mc!) |
| `select` | 等待描述符操作 (mc) |
| `semctl` | `ipc` 信号量控制 (mc) |
| `semget` | `ipc` 获取信号量标识符 (m+c) |
| `semop` | 信号量成员 操作 (m+c) |
| `send` | 向已连接 `socket` 发送消息 (m+c) |
| `sendto` | 向 `socket` 发送消息 (m+c) |
| `setdomainname` | 设置系统域名 (mc) |
| `setgid` | 设置文件系统组 ID (i) |
| `setuid` | 设置文件系统用户 ID (i) |
| `setgid` | 设置实际组 ID (m+c) |
| `setgroups` | 设置附加组 (mc) |
| `sthostid` | 设置唯一主机标识符 (mc) |
| `sthostname` | 设置系统主机名 (mc) |
| `stimeimer` | 设置间隔定时器 (mc) |
| `setpgid` | 设置进程组 ID (m+c) |
| `setgrp` | 无影响 (mc!) |
| `setpriority` | 设置进程/组/用户优先级。(mc) |
| `setregid` | 设置实际和有效组 ID (mc) |
| `setreuid` | 设置实际和有效用户 ID (mc) |
| `setrlimit` | 设置资源限制 (mc) |
| `setid` | 创建会话 (+) |
| `setsockopt` | 更改 `socket` 选项 (mc) |
| `setimeday` | 获取自 1970.1.1.1 的时区+秒 (mc) |
| `setuid` | 设置实际用户 ID (m+c) |
| `setup` | 初始化设备和挂载点 (-) |
| `sgetmask` | 见 `siggetmask` (mc) |
| `shmat` | 将共享内存挂载到数据段 (m!lc) |
| `shmctl` | `ipc` 操作共享内存 (m!c) |
| `shmdt` | 从内存取消挂载共享内存 (m!lc) |
| `shmget` | 获取/创建共享内存段 (m!lc) |

表 A.1 按字母顺序排列系统调用（续）

| 系统调用 | 描述 |
| --- | --- |
| `shutdown` | 关闭 `socket` (m!c) |
| `sigaction` | 设置/获取信号处理程序 (m+c) |
| `sigblock` | 阻塞信号 (m-c) |
| `siggetmask` | 获取当前进程的信号屏蔽 (!c) |
| `signal` | 设置信号处理程序 (mc) |
| `sigpause` | 使用新的信号掩码直到接收信号 (mc) |
| `sigpending` | 获取挂起但被阻塞的信号 (m+c) |
| `sigprocmask` | 设置/获取当前进程的信号屏蔽 (+c) |
| `sigreturn` | 未使用 (i) |
| `sigsetmask` | 设置当前进程的信号屏蔽 (!c) |
| `sigsuspend` | `pause` 的替代方案 (m+c) |
| `sigvec` | 图片 (m!) |
| `socket` | 创建 `socket` 通信端点 (m!c) |
| `socketcall` | `socket` 调用多路用器 (-) |
| `socketpair` | 创建两个连接的 `socket` (m!c) |
| `ssetmask` | 获取设置码 (m) |
| `stat` | 获取文件状态 (m+c) |
| `stats` | 获取文件系统状态 (mc) |
| `stime` | 设置自 1970.1.1 以来的秒数 (mc) |
| `stly` | 未实现 (i) |
| `swapoff` | 停止向文件/设备进行交换 (m-c) |
| `swapon` | 开始向文件/设备进行交换 (m-c) |
| `symlink` | 创建文件的符号链接 (m+c) |
| `sync` | 同步内存和磁盘缓冲区 (mc) |
| `syscall` | 通过编号执行系统调用 (-c) |
| `sysconf` | 获取系统变量的值 (m+c) |
| `sysfs` | 获取关于配置系统项的信息 (!) |
| `sysinfo` | 获取 `Linux` 系统信息 (m-) |
| `syslog` | 操纵系统日志 (m-c) |
| `system` | 执行 `shell` 命令 (m-c) |
| `time` | 获取自 1970.1.1 以来的秒数 (m+c) |
| `times` | 获取进程时间 (m+c) |
| `truncate` | 修改文件大小 (mc) |
| `ulimit` | 获取/设置文件限制 (!c) |
| `umask` | 设置文件创建掩码 (m+c) |
| `unmount` | 卸载文件系统 (mc) |
| `uname` | 获取系统信息 (m+c) |
| `unlink` | 在空闲时删除文件 (m+c) |
| `uslib` | 使用共享库 (m-c) |
| `ustat` | 未实现 (c) |
| `utime` | 修改 `inode` 时间项 (m+c) |
| `utimes` | 查看运行时间 (m|c) |
| `vork` | 查看 `fork` (m|c) |
| `vhangup` | 虚拟挂起当前 `tty` (m-c) |
| `vm86` | 进入虚拟 8086 模式 (m-c) |
| `wait` | 等待进程终止 (m+!) |
| `wait3` | `bsd` `wait` 等待指定进程 (m!|c) |
