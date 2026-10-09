

# 进程管理

- `exit`—终止进程，无清理操作 (5.7)
- `_exit`—终止进程，无清理操作 (5.7)
- `abort`—生成 SIGABRT 信号 (9.1.9)
- `atexit`—注册在进程退出时调用的函数 (1.3.4)
- `exec1`—执行带有参数列表的文件 (5.3)
- `execle`—执行带有参数列表和环境的文件 (5.3)
- `execlp`—执行带有参数列表并搜索 PATH 的文件 (5.3)
- `execv`—执行带有参数向量的文件 (5.3)
- `execve`—执行带有参数向量和环境的文件 (5.3)
- `execvp`—执行带有参数向量并搜索 PATH 的文件 (5.3)
- `exit`—终止进程，执行清理操作 (5.7)
- `fork`—创建新进程 (5.5)
- `system`—运行命令 (5.5)
- `vfork`—创建新进程；共享内存（已废弃） (5.5)
- `wait`—等待子进程终止 (5.8)
- `waitid`—等待子进程状态改变 [X/Open] (5.8)
- `waitpid`—等待子进程状态改变 (5.8)

# 进程权限

- `getgid`—获取有效组 ID (5.11)
- `geteuid`—获取有效用户 ID (5.11)
- `getgid`—获取真实组 ID (5.11)
- `getuid`—获取真实用户 ID (5.11)
- `setegid`—设置有效组 ID (5.12)
- `seteuid`—设置有效用户 ID (5.12)
- `setgid`—设置真实、有效和保存的组 ID (5.12)
- `setuid`—设置真实、有效和保存的用户 ID (5.12)
- `umask`—设置和获取文件模式创建掩码 (2.5)

# 进程资源

- `getpgid`—获取进程组 ID (4.3.3)
- `getpid`—获取进程 ID (5.13)
- `getppid`—获取父进程 ID (5.13)
- `getsid`—获取会话 ID (4.3.2)
- `setpgid`—设置或创建进程组 (4.3.3)
- `setsid`—创建会话和进程组 (4.3.2)

# 信号

- `kill`—为进程生成信号 (9.1.9)
- `killpg`—为进程组生成信号 (9.1.9)
- `raise`—为线程生成信号 (9.1.9)
- `sigaction`—设置信号处理动作 (9.1.6)
- `sigaltstack`—设置和获取备用堆栈上下文 (9.3)
- `sighold`—阻塞信号 (9.4)
- `signal`—设置信号处理动作 (9.4)
- `sigpause`—更改信号掩码并等待信号 (9.4)
- `sigpending`—检查待处理信号 (9.3)
- `sigqueue`—为进程生成信号 (9.5.4)
- `sigrelse`—解除信号阻塞 (9.4)
- `sigset`—信号管理 (9.4)
- `sigsuspend`—更改信号掩码并等待信号 (9.2.3)
- `sigtimedwait`—等待信号 (9.5.5)
- `sigwait`—等待信号 (9.2.2)
- `sigwaitinfo`—等待信号 (9.5.5)

### 信号掩码

- `sigaddset`—将信号添加到信号集 (9.1.5)
- `sigdelset`—从信号集中删除信号 (9.1.5)
- `sigemptyset`—初始化空信号集 (9.1.5)
- `sigfillset`—初始化全信号集 (9.1.5)
- `sigprocmask`—更改线程的信号掩码（仅限单线程） (9.1.5)

# 套接字

- `accept`—在套接字上接受新连接并创建新套接字 (8.1.2)
- `bind`—将名称绑定到套接字 (8.1.2)
- `connect`—连接套接字 (8.1.2)
- `getpeername`—获取已连接套接字的地址 (8.9.2)
- `getsockname`—获取套接字地址 (8.9.2)
- `getsockopt`—获取套接字选项 (8.3)
- `listen`—标记套接字为可接受连接并设置队列限制 (8.1.2)
- `recv`—从套接字接收数据 (8.9.1)
- `recvfrom`—从套接字接收消息 (8.6.2)
- `recvmmsg`—从套接字接收消息 (8.6.5)
- `send`—向套接字发送数据 (8.9.1)
- `sendmsg`—使用消息结构向套接字发送消息 (8.6.3)
- `sendto`—向套接字发送消息 (8.6.2)
- `setsockopt`—设置套接字选项 (8.3)
- `shutdown`—关闭套接字的发送和/或接收操作 (8.9.4)
- `sockatmark`—测试带外标记是否存在 (8.7)
- `socket`—创建通信端点 (8.1.2)
- `socketpair`—创建套接字对 (8.9.3)

### 套接字地址

- `freeaddrinfo`—释放套接字地址信息 (8.2.6)
- `gai_strerror`—获取错误代码描述 (8.2.6)
- `getaddrinfo`—获取套接字地址信息 (8.2.6)
- `gethostbyaddr`—通过地址查找主机 (8.8.1)
- `gethostbyname`—通过名称查找主机 (8.8.1)
- `getnameinfo`—获取名称信息 (8.8.1)
- `inet_addr`—将点分 IPv4 地址字符串转换为整数 (8.2.3)
- `inet_ntoa`—将整数 IPv4 地址转换为点分字符串 (8.2.3)
- `inet_pton`—将 IPv4 或 IPv6 地址转换为字符串 (8.9.5)
- `inet_pton`—将 IPv4 或 IPv6 字符串地址转换为二进制 (8.9.5)

### 终端

- `ticl`—控制字符设备 (4.4)
- `isatty`—测试是否为终端 (4.7)
- `tcdrain`—排空（等待）终端输出 (4.6)
- `tcflow`—暂停或恢复终端输入或输出的流 (4.6)
- `tcflush`—刷新（丢弃）终端输出、输入或两者 (4.6)
- `tcgetattr`—获取终端属性 (4.5.1)
- `tcgetpgrp`—获取前台进程组 ID (4.3.4)
- `tcgetsid`—获取会话 ID (4.3.4)
- `tcsendbreak`—向终端发送断点 (4.6)
- `tcssetattr`—设置终端属性 (4.5.1)
- `tcsetpgrp`—设置前台进程组 ID (4.3.4)
- `ttyname`—查找终端的文件名 (4.7)
- `ttyname_r`—查找终端的文件名 (4.7)

### 终端

- `cfgetispeed`—从 termios 结构中获取输入速度 (4.5.3)
- `cfgetospeed`—从 termios 结构中获取输出速度 (4.5.3)
- `cfsetispeed`—在 termios 结构中设置输入速度 (4.5.3)
- `cfsetospeed`—在 termios 结构中设置输出速度 (4.5.3)
- `cgetattr`—获取 termios 结构 (4.5.1)
- `cgetwattr`—获取 wint 终端属性 (4.5.1)
- `cgetspeed`—获取 termios 结构中的输入/输出速度 (4.5.3)
- `csetwattr`—设置 wint 终端属性 (4.5.1)
- `csetspeed`—在 termios 结构中设置输入/输出速度 (4.5.3)

### 终端 (Pty)

- `grantpt`—获取 pty 从设备侧的访问权限 (4.10.1)
- `posix_openpt`—打开 pty (4.10.1)
- `ptsname`—获取 pty 从设备侧的名称 (4.10.1)
- `unlockpt`—解锁 pty (4.10.1)

# 线程

- `pthread_cancel`—取消线程 (5.17.5)
- `pthread_cleanup_pop`—卸载清理处理程序 (5.17.5)
- `pthread_cleanup_push`—安装清理处理程序 (5.17.5)
- `pthread_cond_signal`—发出条件信号 (5.17.4)
- `pthread_cond_wait`—等待条件 (5.17.4)
- `pthread_create`—创建线程 (5.17.1)
- `pthread_join`—等待线程终止 (5.17.2)
- `pthread_kill`—为线程生成信号 (9.1.9)
- `pthread_mutex_lock`—锁定互斥锁 (5.17.3)
- `pthread_mutex_unlock`—解锁互斥锁 (5.17.3)
- `pthread_sigmask`—更改线程的信号掩码 (9.1.5)
- `pthread_testcancel`—测试取消 (5.17.5)

# 时间

- `asctime`—将分解的时间转换为本地时间字符串 (1.7.1)
- `clock`—获取执行时间 (1.7.2)
- `clock_getcpuclockid`—获取进程 CPU 时间时钟 (9.7.5)
- `clock_getres`—获取时钟分辨率 (9.7.5)
- `clock_gettime`—从时钟获取时间 (9.7.5)
- `clock_nanosleep`—挂起执行以纳秒为单位或直到信号到达 (9.7.5)
- `clock_settime`—设置时钟 (9.7.5)
- `ctime`—将 time_t 转换为本地时间字符串 (1.7.1)
- `difftime`—减去两个 time_t 值 (1.7.1)
- `getdate`—根据规则将字符串转换为分解的时间 (1.7.1)
- `gettimeofday`—获取当前日期和时间作为 timeval (1.7.1)
- `gmtime`—将 time_t 转换为 UTC 分解的时间 (1.7.1)
- `localtime`—将 time_t 转换为本地分解的时间 (1.7.1)
- `mktime`—将本地分解的时间转换为 time_t (1.7.1)
- `nanosleep`—挂起执行以纳秒为单位或直到信号到达 (9.7.3)
- `sleep`—挂起执行以秒为单位或直到信号到达 (9.7.2)
- `strftime`—将分解的时间转换为格式字符串 (1.7.1)
- `strptime`—将字符串转换为格式分解的时间 (1.7.1)
- `time`—获取当前日期和时间作为 time_t (1.7.1)
- `times`—获取进程和子进程的执行时间 (1.7.2)
- `tzset`—设置时区信息 (1.7.1)
- `usleep`—挂起执行以微秒为单位或直到信号到达 (9.7.3)
- `wcstftime`—将分解的时间转换为格式宽字符字符串 (1.7.1)

### 定时器

- `alarm`—调度一个闹钟信号 (9.7.1)
- `getitimer`—获取间隔定时器的值 (9.7.4)
- `setitimer`—设置间隔定时器的值 (9.7.4)
- `timer_create`—创建进程内定时器 (9.7.6)
- `timer_delete`—删除进程内定时器 (9.7.6)
- `timer_getoverrun`—获取进程内定时器超时次数 (9.7.6)
- `timer_gettime`—获取进程内定时器的值 (9.7.6)
- `timer_settime`—设置进程内定时器的值 (9.7.6)

### 用户信息

- `getgrgid`—获取组文件项 (3.5.2)
- `getlogin`—获取登录名称 (3.5.2)
- `getpwnid`—获取密码文件项 (3.5.2)

