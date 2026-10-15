
## 概述
601–603

## 排队信号 (RTS)
642

## RTS (Realtime Signals Extension)
637–642

## SIGHOLD（信号保持）
313–314

## sigonment
647–648

## 系统调用

### 高级间隔定时器
663–665

### alarm（报警）
651–653

### 基础间隔定时器
657–660

### 弃用调用
635–637

### exec（执行）
623–624

### fork（创建子进程）
623–624

# 索引

被中断，607–608

## nanosleep（纳秒级睡眠）
657

## pause（暂停）
624

## pthread_create（创建线程）
623–624

## sigaction（信号处理）
611–615

## sigaltstack（备用信号堆栈）
634

## siglongjmp（信号长跳转）
650–651

## sigpending（待处理信号）
634

## sigqueue（信号队列）
643

## sigsetjmp（信号设置跳跃点）
650–651

## sigsuspend（挂起等待信号）
628–634

## sigtimedwait（定时等待信号）
643–646

## sigwait（等待信号）
624–628

## sigwaitinfo（等待信号信息）
643–646

## sleep（睡眠）
653–656

## ualerp（未定义/拼写错误）
657

## timer（定时器）
605

用户/应用程序生成的，605

## sigpause（信号暂停）
636

## sigpending（待处理信号）
634

## sigqueue（信号队列）
643

## sigrelse（释放信号掩码）
636

## sigset（信号集）
636

## sigsetjmp（信号设置跳跃点）
650–651

## sigsuspend（挂起等待信号）
628–634

## sigtimedwait（定时等待信号）
643–646

## sigwait（等待信号）
624–628

## sigwaitinfo（等待信号信息）
643–646

简单命令，`shell`，376

## sleep（睡眠）
653–657

## SMI（简单消息接口，Simple Messaging Interface）
405

- 客户端示例，420
- 函数，415–418
- 实现
    - FIFO 与，420–428
    - 套接字与，563–566
- 简介，414
- POSIX 共享内存实现，508–515
- POSIX 消息队列实现，451–456
- 服务器示例，419–420
- System V 消息队列实现，438–442
- 类型，415–418

## socket（套接字）
524–525

## socketpair（套接字对）
595

## sockets（套接字）
13, 519

- 地址，523
    - `AF_INET6`，538–539
    - `AF_UNIX`，534–535
- 函数，700
- 结构体，533–534
- 客户端，多个，527–530
- 连接的，系统调用，524–527
- 无连接的，数据报，567–568
- FIFO，700
- 文件描述符，73
- 函数，699–700
- 选项，544–549
- 带外数据，577
- 概述，520–524
- SMI 实现，563–566

## 特殊文件
4–5

- 块特殊文件，4–5
- 字符特殊文件，4
- 磁盘特殊文件，I/O，123–127

## SSI（简单套接字接口，Simple Socket Interface）

- 函数调用，550–551
- HTTP 与，551–552
- 实现，559–563
- 简介，549
- Web 浏览器，552–554
- Web 服务器，554–558

## ssi_close（关闭 SSI 套接字）
550

## ssi_close_fd（关闭 SSI 文件描述符）
551

## ssi_get_server_fd（获取 SSI 服务器文件描述符）
551

## ssi_open（打开 SSI 套接字）
550

## ssi_wait_server（等待 SSI 服务器）
550

## 标准文件描述符
73

## 标准接口
库函数调用与，22

## stat（文件状态）
147–154

## statvfs（虚拟文件状态）
131–135

## STREAMS I/O
255

## strftime（时间格式化字符串）
59

## struct dirent（目录项结构体）
161–162

## struct iovecs（I/O 向量结构体）
111

## struct timespec（时间间隔结构体）
64

## struct timeval（时间值结构体）
58

## struct tm（时间结构体）
58

## struct tms（时间结构体）
64

## 超级用户
11

## 附加组 ID
10

## 符号链接
2–4, 3–4, 137–138

- 创建，141–144
- 元数据与，147–154
- 符号，141–144

## sync（同步）
115–117

## 同步
线程，333–338

## 同步 I/O

- 定义，189–190
- `open` 标志与，117–119
- 与同步（同步性）的区别，114

## 同步写入
94

## 同步 I/O

- 与异步 I/O 的对比，196–198
- 定义，189–190
- 与同步（同步性）的区别，114

## 合成生成的信号
621–623

## sysconf（系统配置）
51–52

## 系统调用
19, 661. *另见* 函数

- `accept`，526
- `access`，185–186
- `bind`，525
- 缓冲区刷新，115–117
- C 绑定，20–21
- C++ 绑定，20–21
- `chdir`，166–168
- `chmod`，182
- `chown`，182–184
- `chroot`，319–320
- `close`，97–98
- `closedir`，160–162
- `confstr`，53
- `connect`，526–527, 576
- `connect` 套接字与，524–527
- `creat`，77–80
- `ctty`，248
- `dup`，371–375
- `dup2`，371–375
- `exec`，284–292
    - `exec1`，285
    - `exec1e`，289
    - `exec1p`，288
    - `execvp`，288
    - `execve`，289
    - `execvp`，288
- `exit`，301–304
- `fchdir`，166–168
- `fchmod`，182
- `fchown`，182–184
- `fcntl`，187–189
- `fdatasync`，116–117
- `fork`，284, 296–300
- `fpathconf`，52
- `fstat`，147–154
- `fstatvfs`，131–135
- `ftok`，429–431
- `ftruncate`，119–120
- `getaddinfo`，540–543
- `getcwd`，145–147, 170–174
- `getgroupld`（获取组 ID），154–155
- `gethsoame`（获取主机别名），543–544
- `getlogin`，154–155
- `getpeername`，594
- `getpgid`，228–229
- `getpwd`（获取密码），154–155
- `getrlimit`，323
- `getrusage`，328
- `gettid`，227
- `getsockopt`，594
- `getsockopt`，545–549
- `gettimer`，658
- 组 ID，315–316
- 被中断，信号与，607–608
- `ioctl`，232–233
- `isatty`，249
- `lchown`，182–184
- 链接，138–139
- `listen`，525
- `lockf`，483–485
- `look`，105–108
- `lstat`，147–154
- `mkdir`，168–170
- `mkfif0`（创建 FIFO），407
- `mknod`，186–187
- `mount`，135–136
- `mq_close`，447
- `mq_getatr`（获取消息队列属性），450
- `mq_notify`，450
- `mq_open`，446
- `mq_receive`，448
- `mq_send`，448
- `mq_setatr`（设置消息队列属性），451
- `mq_timedreceive`，449
- `mq_timedsend`，449
- `mq_unlink`，447
- `magctl`（消息控制），445
- `magget`（获取消息），434
- `magcrv`（获取消息值），436
- `magsend`（发送消息），436
- `nanoSleep`，657
- `nice`，320–321
- `open`，76–77
- `opendir`，160–162
- `pathconf`，52
- `pipe`，362–363
- `poll`，218–221
- POSIX 消息队列，445–451
- POSIX 共享内存，505–507
- `pread`，108–110
- 优先级设置/获取，320–321
- 进程组，228–229
- 进程 ID，319
- `pthread_cancel`，344–345
- `pthread_cleanup_pop`，347–348
- `pthread_cleanup_push`，347–348
- `pthread_cond_signal`，341–344
- `pthread_cond_wait`，341–344
- `pthread_create`，331
- `pthread_join`，332–333
- `pthread_mutex_lock`，334–338
- `pthread_mutex_unlock`，334–338
- `pthread_testcancel`，345–347
- `pwrite`，108–110
- `read`，96–97
- `readdir`，161–162
- `readv`，110–113
- `recvfrom`，568–574
- `recvmsg`，574–576
- `rename`，139–141
- `rewinddir`，161–162
- `rmkdir`（递归创建目录），168–170
- `seekdir`，161–162
- `select`，213–218, 528
- `semctl`，461
- `semget`，460
- `semmsg`，574–576
- `sendto`，568–574
- 会话，227–228, 230–232
- `setgid`，318
- `setuid`，318
- `setgid`，318
- `setpgid`，228–229
- `setrlimit`，323
- `setuid`，227
- `setsockopt`，544–545
- `settimer`，658
- `setuid`，318
- `shm.at`（共享内存属性），490
- `shmctl`，489
- `shmdt`，490
- `shmat`，489
- `shm_open`，505
- `shm_unlink`，505
- `shutdown`，595
- `sigaction`，611–615
- `sigattack`（信号攻击/待处理信号），634
- `sighold`，636
- `sigignore`，636
- `siglongjmp`，650–651
- `sig1`，635–636
- `sigpause`，636
- `sigpending`，634
- `sigsqueue`，643
- `sigrelse`，636
- `sigset`，636
- `sigsetjmp`，650–651
- `sigsuspend`，628–634
- `sigtimedwait`，643–646
- `sigwait`，624–628
- `sigwaitinfo`，643–646
- `sleep`，653–656
- `socket`，524–525
- `socketpair`，395
- `stat`，147–154
- `statvfs`，131–135
- `symlink`，141–144
- `sync`，115–117
- `sysconf`，51–52
- System V 消息队列，434–437
- System V 信号量，460–463
- System V 共享内存，489–492
- `tdrain`，245–247
- `tcflow`，246
- `tcflush`，246
- `togtppgrp`，229–230
- `tgetsid`，229–230
- `tosendbreak`，247
- `tosetpgrp`，229–230
- `telldir`，161–162
- 终端控制，229–230, 245–247
- 终端识别，248–250
- `truncates`（截断），119–120
- `ttyname`，248
- `ttyname_r`，248
- `umask`，86
- `umount`，135–136
- `union semvar`，461
- `unlink`，86–87
- 用户 ID，315–316
- `ualerp`，657
- `utime`，184–185
- `vfork`，299
- `wait`，304–313
- `waitid`，304–313
- `waitpid`，304–313
- `write`，92–96
- `writev`，110–113

## 系统数据
5, 6

## System V

- `IPC`（进程间通信），428 (*另见* **IPC**
    - [*进程间通信*]
        - 标识符，429–431
        - 对象，428–429
        - 所有权，431–432
        - 权限，431–432
        - 实用工具，432–433
- 消息队列
    - 缺点/优点，442
    - 限制，437–438
    - SMI 实现，438–442
    - 系统调用，434–437
- 性能对比，515–517
- 信号量
    - 与 POSIX 对比，476
    - 系统调用，460–463
- 共享内存
    - 优点/缺点，504
    - SMI 实现，496–504
    - 系统调用，489–492

## T

## 制表符，终端
237

## tcflow
246

## tcflush
246

## tcgetattr
233

## tcsetattr
233

## tcgetpgrp
229–230

## tcsetpgrp
229–230

## tcsendbrk
247

## tcsetattr
233

## tsendbrk
247

## telldir
161–162

## 临时文件，创建
88–90

## 终端函数
700

## 终端 I/O

- 规范的（`canonical`），239–242
- 简介，203
- `poll`，218–221
- `punctual`（及时的），239–242
- 原始终端 I/O，242–245

## 从终端读取

- `glin`（获取行），206
- 非阻塞输入，208–213
- `select`，213–218
- 测试输入，221–224

## 终端 (Py) 函数
700

## 终端

- 属性
    - `tcgetattr`，233
    - `tcsetattr`，233
- 中断，247
- 字符映射，236–237
- 字符，234–235
- 控制字符，238–239
- 控制终端，8
- 延迟，237
- 回显开/关，239
- 流控制，237
- 刷新，246
- I/O 流控制，246
- 填充，248
- 伪终端，256–257
- 读取自，终端 I/O 与，204–224
- 速度，235–236
- 系统调用，229–230
- 制表符，237
- 测试，249

## 终止

- 进程，301–304
- 线程，等待，332–333

## termios 结构体
233–234

## 测试，输入，终端 I/O
221–224

## 文本，目标文件
5

## 文本文件
5

## Thompson, Ken
16

## 线程函数
701

## 线程
6

- 阻塞与，350–351
- 取消，344–348
- 创建，329–331
- 库函数与，22
- 与进程对比，348–349
- 同步，333–338
- 终止，等待，332–333
- 变量，条件变量，338–344

## time
See `data time`（参见 数据时间）

## time
58

## 时间函数
701–702

## 定时器，函数
702

## times
64

## tmpnam
88–90

## tokens, shells
376–377

## transferring data
See `data transfer`

## truncate
119–120

## ttyname
248

## ttyname_r
248

## U

## umask
86

## umount
135–136

## uname
584

## unidirectional pipes
390–399

## Unified Event Manager, blocking and
351–357

## union semem
461

## UNIX, history
16–19

## unlink
86–87

## unlock
81

## unmounting file systems
135–137

## unsetenv
280–281

## updating environment
279

## user buffered I/O

## functions
100–105

## kernel buffering and
98–100

## user data
5

## user IDs

## setting
317–318

## system calls
315–316

## user info functions
702

## user ID
9

## users

## groups
9
