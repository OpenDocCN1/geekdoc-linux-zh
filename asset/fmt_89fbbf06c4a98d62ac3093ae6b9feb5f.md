
## 下一代处理器 (next-generation processors), 71

- `NUMA-Q` 架构, 70–71
- 概述, 自关联缓存 (overview, self-associative cache), 68
- 全共享架构 (shared everything architecture), 67
- 写回缓存 (write-back cache), 68
- 写失效协议 (write-invalidate protocol), 69
- 写通缓存 (write-through cache), 68
- 写更新协议 (write-update protocol), 69

## 处理器集 (processor sets), 88

## 处理器调优 (processor tuning)
- 多处理器处理器的亲和性绑定 (affinity binding multiprocessors), 87
- 处理器基准测试 (benchmarking processors), 88–89
- I/O 调优 (IO tuning), 81–82
- `mpstat-command`, 77
- 处理器数量 (number of processors), 86–87
- 概述 (overview), 76–77
- 任务并行 (paralleling tasks), 85–86
- 抢占控制 (preemption control), 83–84
- 处理器集 (processor sets), 88
- 处理器使用的内核参数 (processor used kernel parameters), 84–85
- `sar` command, 77
- `top` command, 80

## 处理器相关内核参数 (processor-related kernel parameters), 84–85

## 性能分析 (profiling), 253–254

## 进度条 (progress meter), 255

## `PUSH_PRED` 提示, 229

## `PUSH_SUBQ` 提示, 227

## Q

- `QCIC` (四通道 I/O 控制器), 96
- `QCIC-W` (宽四通道 I/O 控制器), 96
- QEP 执行阶段 (QEP execution phase), 174
- QEP 生成阶段 (QEP generation phase), 176
- 查询 (queries)
  - 并行查询 (parallel queries), 229
  - 调优 (tuning), 324–331
  - 查询协调器 (Query Coordinator), 065–357
  - 查询重写 (query rewrite), 347–349

## R

- RAID 0. 参见条带化 (stripping)
- RAID 1. 参见镜像 (mirroring)
- RAID 级 (RAID level), 113–115
- RAID-5, 113–114
- RAID-6, 114
- RAID-7, 114
- RAID-S, 115
- 原始设备 (raw devices)
  - 文件系统 (file systems), 125–131
  - 最大物理 I/O 大小 (maximum physical I/O size), 130–131
  - 概述 (overview), 129–130
- `read()` 系统调用, 2, 91–93
- `readv()` 系统调用, 124
- 实时作业类 (real-time job class), 26
- 恢复管理器 (RMAN), 383–385
- 递归 SQL (recursive SQL), 301–302
- 重做日志缓冲区监控 (redo buffer monitoring), 267
- 重做日志缓冲区锁 (redo log buffer latch), 264–266
- 重做日志文件 (redo log files), 153, 配置, 152
- 卷管理镜像 (volume management mirroring), Oracle 镜像
  - 比较, 154
- 引用完整性 (referential integrity), 306–307
- `RELEASE CURSOR` 编译选项, 167–168
- 反向索引 (reverse index), 364–365
- `REWRITE`, 230–231
- 回滚段 (rollback segments)
  - 大事务 (large transactions), 277–278
  - 回滚段数量 (number of rollback segments), 275–276
  - `nview`, 274–275
  - 回滚段大小设置 (sizing rollback segments), 276–277
  - 快照过期错误 (snapshot too old error), 278
  - 调优 (tuning), 274–278
- `rootdg` 磁盘组 (rootdg disk group), 99
- `RSY` 提示, 224–225
- `RPC`, 12–13
- `RULE` 提示, 224
- 基于规则优化器 (rule-based optimizer (RBO)), 179–180

## S

- `sar` command, 77
- 调度进程 (`sched` process), 5
- `schmat()` 系统调用, 64
- 自关联缓存 (self-associative cache), 68
- 语义阶段 (semantic phase), 171
- 信号量池 (semaphore porches), 66
- 信号量 (semaphores), 30
- 半连接 (semi-join), 326
- 顺序和随机 I/O (sequential and random I/O), 131
- Sequence 阶段 (Sequence phase), 171
  - 异步 I/O 开启 (asynchronous I/O on), 119
  - 条带化开启 (stripping on), 96–100
- 会话单元 (Session Data Unit (SDU)), 295–297
- SGA 大
  - 缓冲区缓存监控 (buffer cache monitoring), 289–290
  - 缓冲区缓存设置 (buffer cache sizing), 286–289
  - 大内存池 (large memory pool), 292–293
  - 多个缓冲区池 (multiple buffer pools), 290–292
  - 概述 (overview), 286
  - 可共享缓存 (sharable caches), 202–203
  - 全共享架构 (shared everything architecture), 67
  - 共享锁 (shared latches), 267
  - 共享库链接 (shared library, linking with), 167
  - 共享内存 (shared memory), 20
  - 共享选项 (shared option), 62–64
  - 参数 (parameters), 61–62
  - `shmat()` 系统调用, 64
  - 共享实用程序 (shared utility), 64
- 共享池 (shared pool)
  - 游标执行 (cursor execution), 280–281
  - 分段 (fragmentation), 278
  - 库缓存 (library cache), 278–279
  - 字面量替换 (literal replacement), 284–285
  - 已用内存 (memory used), 282–283
  - 钉住对象 (pinning object), 24
  - shell 层 (shell layer), 32
  - `shmax` 内核参数, 61
  - `shmin` 内核参数, 61–62
  - `shm` 内核参数, 61–62
  - `shseg` 内核参数, 61–62
- 信号 (signals), 27–75
- 单磁盘类型 (single disk type), 99
- 单 SQL 语句用户插入 (single SQL statement user insert), 215
- 快照过期错误 (snapshot too old error), 278
- 套接字 (sockets), 28
- Solaris
  - 64 位算法 (64-bit algorithms), 71–73
  - 同步 I/O 输入 (synchronous I/O in), 117–118
- 排序连接 (sort merge join), 187, 188
