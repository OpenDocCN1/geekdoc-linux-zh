
`processor_bind` 例程, 362, 365, 375
绑定, 371–379

## 生产者-消费者系统
原子性, 326–328
使用环形缓冲区, 315–318
并发队列, 387–388
条件变量, 135–137
概述, 109
扩展性, 318–326
信号量, 168–169
`pthread_mutex_unlock`, 155
`pthread_mutex_attr_init`, 156–157
`pthread_mutexattr_t`, 156
`pthread_rwlock_destroy`, 160
`pthread_rwlock_rdlock`, 160
`pthread_rwlock_rdnlock`, 160
`pthread_rwlock_timedlock`, 161
`pthread_rwlock_timedlock_np`, 161
`pthread_rwlock_timedlock`, 161
`pthread_rwlock_trylock`, 161
`pthread_rwlock_wrl`, 160
`pthread_rwlock_wrunlock`, 160
`pthread_rwlock_attr_init`, 159
`pthread_rwlock_attr_setshared`, 159
`pthread_self`, 147
`pthread_specific`, 177
`pthread_spin_destroy`, 157
`pthread_spin_init`, 157
`pthread_spin_lock`, 157
`pthread_spin_trylock`, 157
`pthread_spin_unlock`, 157
`PTHREAD_STACK_MIN` 变量, 150
`pthread_t` 结构体, 143–144

## 分析
反馈, 68–70
重要性, 74–75
性能估计, 412
工具, 75–80
套接字协议, 194
`pthread_attr_destroy`, 148
`pthread_barrier_destroy`, 162
`pthread_barrier_init`, 162
`pthread_barrier_wait`, 162
`pthread_cond_broadcast`, 172
`pthread_cond_destroy`, 170
`pthread_cond_init`, 170
`pthread_cond_signal`, 172
`pthread_cond_timedwait`, 174–175
`pthread_cond_wait`, 173
`pthread_create`, 143–145, 147–149
`pthread_detach`, 147, 194
`pthread_exit`, 143
`pthread_getspecific`, 177
`pthread_join`, 144–147, 194, 305
`pthread_key_create`, 177–178
`pthread_key_delete`, 177
`pthread_mutex_attr_destroy`, 157
`pthread_mutex_destroy`, 154
`pthread_mutex_init`, 154, 156–157
`pthread_mutex_lock`, 155
`pthread_mutex_setshared`, 155
`pthread_mutex_trylock`, 155

![](img/9337ae7b0be66cc11725becaa0908f_455_0.png)

服务质量 (QoS) 指标, 32

## 队列
并发队列, 387–388
延迟, 355
消息, 138–186

## 快速排序
算法复杂度, 35–37
Cilk++, 390–392
OpenMP, 350–352

# 扩展性 435

## R
复制，虚拟化, 91
`read` 例程, 194
`ResetEvent` 例程, 220
读取任务依赖, 111

## 资源
读写锁, 159–162
句柄, 207–208
共享。参见同步 (Synchronization)
流水线中的饥饿, 363–369
`_ReadBarrier` 例程, 308
响应时间指标, 32
`readdir` 例程, 197–198
`restrict` 关键字, 74, 254–255
`readdir_r` 例程, 198
`restrict` 限定指针, 249, 254–255

## 读者-写锁

## 限制
概述, 129
代码线程区域, 281–284
Windows 线程, 214–214
虚拟化, 91
`_ReadBarrier` 例程, 308
`ResetThread` 例程, 220
`recv` 例程, 194
流水线中的还原, 106–108
还原子句, 261
还原 存储主数组, 58
鲁棒性, 90

# 扩展性
扩展性, 318–326
以及填充, 370
调度模式, 265
`schedule` 子句, 261
OpenMP 中的作用域, 259–263
`sections` 指令, 268
搜索, 59–60
安全, 90
`SECURITY_ATTRIBUTES` 结构体, 223–225
`sem_close`, 164
`sem_destroy`, 163
`sem_getvalue`, 165
`sem_init`, 163
`sem_open`, 164
`sem_post`, 165
`sem_trywrite`, 166
`sem_unlink`, 164
`sem_wait`, 170
静态库的副作用, 42
`sigaction` 例程, 190, 192
`siginfo_t` 数据, 193
`SIGKILL` 信号, 137, 188
`signal` 例程

POSIX 线程, 188
信号量, 129
同步开销
同步开销, 98–100
同步开销, 98–100
同步开销, 98–100
同步开销, 98–100
同步开销, 98–100
序列化程序, 128
序列化程序, 128
流水线中的单阶段, 106–108
流水线中的单阶段, 106–108
流水线中的单阶段, 106–108
流水线中的单阶段, 106–108
流水线中的单阶段, 106–108
流水线中的单阶段, 106–108
流水线中的单阶段, 106–108
流水线中的单阶段, 106–108
流水线中的单阶段, 106–108

# 栈地址、打印, 359–360

- 信号量, 128, 165
- Solaris 操作系统
- Windows 线程, 219–221
- `doors`, 141
- `SIGPROF` 信号, 190
- 局部性组, 8
- `sigqueue` 程序, 192–193
- 区域 (zones), 89
- `SIGRTMAX` 信号, 189
- Solaris Studio 性能分析器, 76, 78–79, 291
- `SIGRTMIN` 信号, 189, 193

## 排序

### SIMD（单指令多数据）指令
- 算法复杂度, 35–37
- 使用数据并行, 101–102
- Cilk++, 390–392
- 向量化, 408
- OpenMP, 35–352
- `sin` 指令, 252
- 并行支持, 93–94
- `single` 指令, 275, 279–282

### 源代码
### 单指令多数据 (SIMD) 指令
- 构建结构权衡, 39–42
- 使用数据并行, 101–102
- 转换为汇编语言。参见[将代码翻译为汇编语言](Translating code to assembly language)
- 向量化, 408
- 源代码级分析, 77

### 单指令单数据 (ISD) 指令, 408

### SPARC 架构, 3
- 64 位代码性能, 23–24
- 汇编语言, 21–22
- 内存屏障, 25
- 页面大小, 17

### Size
- SPEC Java 应用服务器基准, 31
- 缓存, 13
- 预测打破依赖, 113–117
- 页面, 17
- 投机性执行, 115
- 栈, 149
- 寄存器溢出 (Spilling), 23
- `sleep` 命令, 179
- 自旋锁, 128
- `SleepConditionVariableCS` 程序, 218
- `SleepConditionVariableSRW` 程序, 218
- 带屏障的, 302–303
- 细粒读写锁 (Slim reader/writer locks), 208, 214–252
- 使用 CAS, 298–299
- 缓存一致性监听 (Snooping), 18
- `sockaddr_in`, 269
- 循环缓冲区, 319–326
- `socket` 程序, 194
- POSIX 线程, 157–159
- 旋旋程序, 356–358, 367–368
- POSIX 线程, 193–197
- 自旋线程, 366–369
- 设置, 140
- 拆分任务, 106
- Windows 线程, 234–382
- 拆分结构, 57
- 软件预取, 55
- 网络栈, 139–140
- 软件线程, 4
- 软件事务性内存, 408

## 基于栈的调用约定

- 基于栈的调用约定, 23
- 基于栈的数据, 141

### 栈大小
- 默认, 149
- OpenMP 工作线程, 278
- `Start` 方法, 398
- `STARTUPINFO` 结构, 222–223

### 静态库
- 构建过程, 41–42
- 侧效应, 42

- 静态调度 (Scheduling), 263–265
- `_stdcall` 调用约定, 201
- 步进库调用, 49–50
- 存储线程私有数据, 141–142
- `Strands`, 44
- Haskell 中的策略, 401
- 强度削减, 63
- 字符串处理, 221–222
- `strlen` 程序, 353

### 结构
- 构建, 39–42
- 库, 42–53

### 结构
- 64 位, 24
- 数据。参见[数据结构](Data structures)
- 传递, 254–255
- Studio 性能分析器, 76, 78–79, 291
- 带归约的减法, 250, 261
- 超标执行, 11
- 超线性扩展, 336–337
- 挂起线程程序, 207
- `SuspendThread` 程序, 207
- `_sync_fetch_` 程序, 309

## 同步, 121
- 原子操作, 130–131
- 屏障, 130
- 通信。参见[线程与进程间的通信](Communication between threads and processes)
- 临界区, 126–128
- 数据竞态, 121–126
- 死锁与活锁, 132–133
- 手编码。参见[手编码同步](Hand-coded synchronization)
- 多处理器, 380–381
- 原语, 126–131
- 读写锁, 129
- 扩展成本, 98–100
- 信号量, 128–129
- 自旋锁, 128
- Windows 线程。参见[Windows threads](Windows threads)
- 全系统性能分析, 75

## 任务
- `task` 指令, 269
- 动态定义的并行性, 269–273
- 识别, 411–412
- 多份拷贝, 105–106
- 多个松耦合, 103–105
- 流水线, 106–108
- 拆分, 106
- `taskwait`, 280–281

## 终止
- TBB (线程构建块) 库, 386–389
- POSIX 线程, 144–145
- 进程, 153–154
- Windows 线程, 204–206
- 抖动 (Thrashing), 359
- 线程分析器, 124–125
- `thread_code` 程序, 144, 153–154
- TLB (转换查找缓冲区), 9, 16–17, 27–28
### 线程本地数据
- 用于的数组, 141
- 分配, 240–242
- 声明, 142, 177
- `GetValue` 程序, 241
- `SetValue` 程序, 241
- `_printf` 程序, 222
- 线程对象, 398
- 事务性内存, 407
- 线程私有数据, 141–142, 176
- 每秒事务数指标, 31
- 线程安全的 `malloc` 程序, 127–128
- 指定符, 142, 177
- 内存顺序, 24–26
- 32 位与 64 位代码的性能, 23–24
- 线程构建块 (TBB) 库, 386–389
- 进程与线程对比, 26–29
- `private` 指令, 274–275
- 将虚拟地址转换为物理地址, 16–18

## 线程
- 转换查找缓冲区 (TLBs), 9, 16–17, 27–28
- 绑定, 362, 365–366, 373
- 唤起, 348–349
- 依赖性, 413
- 阻塞, 322
- 与 C++ 关系
- 任务, 394–395
- C++ 与 CLI, 397–398
- 独占获取锁程序, 216
- 共享获取锁程序, 216
- 进入临界区程序, 212
- 最大值, 97–98
- 迁移, 371–372
- 过度订阅, 369–371
- 自旋, 366–369
- `uintptr_t` 类型, 201
- 任务拆分, 106
- `ulimit` 命令, 150, 278
- 超 SPARC
- 蓝图, 6–8
- 线程启动, 398–399
- 流水线, 10
- 惊群效应, 323
- UMA 架构, 19
- 寄存器, 368–369
- 时间, 32
- 终止, 224

### 超时
- 字符串处理, 221–222
- POSIX 线程变量, 174–175
- 统一内存架构 (UMA), 19
- 读写锁的, 161–162
- 取消程序, 187

## 未映射
- 字符串处理, 221–222
- 信号量变量, 174–175
- 区域 (zones), 89

## 未映射
- 信号量, 129–130
- 线程变量, 176–177
- 性能分析器, 75–79

## 更新
- 原子操作, 130–131
- 数据竞态, 122
- 格式, 221

## 等待
- 锁, 11–111

-
- 线程, 221

2 2
- 原子操作, 239–240
- 线程, 204–206
- 资源, 207–208
- 优先级, 242–244
- 任务, 207

## 区域 (zones)
- 同步, 208–209
- 写入程序, 397
- 条件变量, 218–219
- `WSA清理程序`, 235
- 临界区, 210–213
- `WSADATA` 结构, 235
- 示例, 209–210
- `WSAStart` 程序, 235
- 互斥锁, 213–214

## X
- `x64` 指集, 23
- 信号, 219–221
- `x86-64` 指集, 23
- 细粒读写锁, 214–216
- `xadd` 指令, 296–297
- 终止, 204–206
- 别名级别标志, 73
- 线程本地变量, 204–242
- `xautopar` 标志, 246
- 宽字符串处理, 221–222
- 内建标志, 252, 256
- 工作负载调度, 263–267
- `xloopinfo` 标志, 246, 259
- 工作线程
- `xopenmp` 标志, 259
- MPI, 404–405
- OpenMP, 258
- 原子操作的异或操作, 239
- 栈大小, 278
- `xreduction` 标志, 251, 256
- 工作负载平衡
- `xrestrict` 标志, 73

## Y
- 应用扩展限制, 338–339
- 循环合并用于, 286–287
- `yieldprocessor` 宏, 369
- `wprintf` 程序, 222

## Z
- 写入程序, 189, 194
- 零和性能视图, 69
- 写入任务依赖, 311
- `_Barrier` 程序, 308
- 区域 (zones), 89
