
## 文件操作

- `fsync` - 将文件的核心内状态与磁盘上的状态同步
- `lseek` - 重新定位读/写文件偏移量
- `llseek` - 用于大文件的更长 `lseek`
- `readdir` - 读取目录（系统调用）
- `truncate`, `ftruncate` - 将文件截断到指定长度

## 目录

- `chdir`, `fchdir` - 更改工作目录
- `chroot` - 更改根目录
- `mkdir` - 创建目录文件
- `readlink` - 读取符号链接的值
- `rmdir` - 删除目录

## 套接字与网络

- `accept` - 在套接字上接受连接
- `bind` - 将名称绑定到套接字
- `connect` - 在套接字上发起连接
- `getdomainname`, `setdomainname` - 获取/设置域名
- `gethostname`, `sethostname` - 获取/设置主机名
- `gethostid`, `sethostid` - 获取或设置当前主机的唯一标识符
- `getsockname` - 获取套接字名称
- `getsockopt`, `setsockopt` - 获取和设置套接字选项
- `listen` - 在套接字上监听连接
- `socket` - 创建通信端点
- `socketpair` - 创建一对已连接的套接字
- `recv`, `recvfrom`, `recvmsg` - 从套接字接收消息
- `send`, `sendto`, `sendmsg` - 从套接字发送消息

## 命名管道、管道和进程间通信

- `pipe` - 创建管道
- `msgop`, `msgcvt`, `msgsnd` - 消息操作
- `msgctl` - 消息控制操作
- `msgget` - 获取消息队列标识符

## 设备

- `ioctl` - 控制设备
- `ioperm` - 设置端口输入/输出权限
- `mknod` - 创建特殊文件节点

## 其他

- `getdtablesize` - 获取描述符表大小
- `mmap`, `munmap` - 将文件或设备映射或取消映射到内存
- `mount`, `umount` - 挂载和卸载文件系统
- `select` - 同步 I/O 复用
- `setup` - 初始化 ST506 驱动器及分区参数
- `shutdown` - 关闭全双工连接的一部分
- `statfs`, `fstatfs` - 获取文件系统统计信息
- `symlink` - 为文件创建新名称
- `sync` - 将缓冲缓存提交到磁盘
- `vhangup` - 虚拟挂断当前终端（tty）
- `termio`, `tcgetattr`, `tcsetattr`, `tcdrain`, `tcflush`, `tcflow`, `cgspeed`, `cfgetispeed`, `cfsetspeed`, `cfgetospeed`, `cfsetispeed`, `cgspeed`, `tcgpg`, `tcsetpg` - 获取和设置终端属性、行控制，获取和设置波特率，获取和设置终端前台进程组 ID

## 内存

- `brk`, `sbrk` - 更改数据段大小
- `shmtcl` - 共享内存控制
- `shmget` - 分配共享内存段
- `shmop` - 共享内存操作
- `shmat`, `shmctl` - 共享内存操作

## 进程

### 创建/销毁

- `_exit` - 终止当前进程
- `fork`, `vfork` - 创建子进程
- `execve` - 执行程序
- `kill` - 向进程发送信号
- `killpg` - 向进程组发送信号

### 执行控制

- `alarm` - 设置闹钟以便发送信号
- `idle` - 使进程空闲
- `getpriority`, `setpriority` - 获取/设置程序调度优先级
- `nice` - 更改进程优先级
- `pause` - 等待信号
- `semctl` - 信号量控制操作
- `semget` - 获取信号量集标识符
- `semop` - 信号量操作
- `sigblock`, `sigmask` - 阻塞信号
- `signal`, `sigaction`, `sigsuspend`, `sigpending`, `sigsetmask`, `siggetmask` - 信号处理函数
- `sippause` - 原子性地释放被阻塞的信号并等待中断
- `sigvec` - 软件信号设施
- `wait`, `waitpid` - 等待进程终止
- `wait3`, `wait4` - 等待进程终止，BSD 风格

### 访问

- `getgid`, `getegid` - 获取组身份
- `getgroups`, `setgroups` - 获取/设置组访问列表
- `getpid`, `getppid` - 获取进程标识
- `getrlimit`, `getrusage`, `setrlimit` - 获取/设置资源限制和使用情况
- `getuid`, `geteuid` - 获取用户身份
- `setgid`, `setegid` - 设置组身份
- `setregid` - 设置真实和/或有效组 ID
- `setpgid`, `getpgid`, `getpgrp`, `setpgid` - 设置/获取进程组
- `setreuid` - 设置真实和有效用户 ID
- `setuid`, `seteuid` - 设置用户身份

### 其他

- `acct` - 切换进程核算开关
- `times` - 获取进程时间

## 系统

- `stime` - 设置时间
- `swapon`, `swapoff` - 启动/停止到文件/设备的交换
- `sysinfo` - 返回整体系统统计信息
- `time` - 以秒为单位获取时间
- `uname` - 获取当前内核的名称和信息
- `adjtimex` - 读取和写入内核计时变量
- `syslog` - 管理内核消息环形缓冲区
- `bdflush` - 管理缓冲区脏数据刷新守护进程
- `get_kernel_syms`, `create_module`, `delete_module`, `init_module` - 可加载模块支持

## 其他

- `getitimer`, `setitimer` - 获取或设置间隔定时器的值
- `getpagesize` - 获取系统页大小
- `getpeername` - 获取已连接的对等方名称
- `gettimeofday`, `settimeofday` - 获取/设置时间
- `iopl` - 更改 I/O 特权级别
- `phys` - 允许进程访问物理地址 [未实现]
- `profil` - 执行时间分析
- `ptrace` - 进程跟踪
- `reboot` - 重启或禁用 Ctrl-Alt-Del
- `uselib` - 选择共享库
- `vm86` - 进入虚拟 8086 模式

## 无文档记录

- `ulimit`
- `setgid`
- `sigsetmask`
- `klog`
- `clone`
- `modify_ldt`
- `mprotect`
- `personality`
- `setfsuid`
- `setfuid`
- `siggetmask`
- `sigreturn`
- `sigsetmask`
- `socketcall`
- `sysfs`

## 未实现

- `afs.syscall`
- `break`
- `gotty`
- `lock`
- `mpx`
- `prof`
- `quotactl`
- `sstty`
- `ustat`

## 已过时

- `oldfstat`
- `oldlstat`
- `oldstat`
- `oldolduname`
- `olduname`

## 隐藏接口

目前，我的系统的内核调度表中有二十八个条目，它们并不能精确映射到运行时库中的某个子例程。其中一些条目是在运行时库中的例程完成大量计算之后被调用的。另一些条目在发布新的运行时库之前处于隐藏状态，但在此之前开发人员可以直接使用它们。

# 附录 C

# 人物简介

- `Gordon Bell` —— DEC 公司工程副总裁。在 DEC 工作期间，他在 PDP-11 和 VAX-11 系列计算机的开发过程中发挥了重要作用。尽管 DEC 对这些系统上的 Unix 支持有限，但这些系统仍是 Unix 开发的基础，这一地位持续了 15 年以上。
- `Stephen R. Bourne` —— Bourne Shell 的作者。令 Unix 爱好者感到困惑的是，贝尔实验室曾有两位“Stephen R. Bourne”。一场趣味测验曾要求参赛者说出其中一人的电话号码。
- `Fred Brooks` —— OS/360 项目的负责人，《人月神话》一书的作者，该书是对大型软件产品开发的一部评述。布鲁克斯博士目前参与北卡罗来纳大学的虚拟现实系统研究。
- `John Lions` —— 出版了一本考察早期 Unix 系统内核的书籍，该书由新南威尔士大学出版，供操作系统理论专业的学生使用。这本书的副本被广泛分发。
