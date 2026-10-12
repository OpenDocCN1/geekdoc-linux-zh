

图表引用使用斜体。

-   /（根分区），127
-   32位与64位处理器，358-359

## A

-   活动节点（active nodes），167
-   警报文件（alert files），34
-   别名（aliases），168
-   ALTER DATABASE 命令，71, 73-74
-   ALTER SYSTEM 命令，245
-   ALTER SYSTEM SWITCH LOGFILE 命令，75
-   ALTER TABLESPACE 命令，41, 42
-   ANALYZE 命令，47-48
-   Apache，19
-   应用开发（application development），62-63
-   ar（归档实用工具，archiver utility），15-16
-   归档日志文件（archive log files），33, 71
    -   特征，75-76
    -   恢复，276-278
-   归档日志备份（archive log backup），283-285
-   ARCHIVELOG 模式，281, 282-283
-   归档进程（Archiver Processes）。参见 ARCHN
-   归档（archiving），280-283
-   ARCHn，56
-   ARCn，326
-   as（GNU 汇编器，GNU assembler），15
-   异步复制（asynchronous replication），343
-   身份验证（authentication）
    -   数据库，227
    -   中间层，228
    -   网络，227-228
    -   操作系统，227
    -   远程，228
    -   通过 SSL，228-229
    -   用户，227
-   授权，用户（authorization, user），229
-   自动存储管理（Automatic Storage Management, ASM），25, 32, 148, 171
    -   配置 ASM 磁盘，149
    -   配置 ASM 库驱动程序，149-150
    -   配置共享磁盘，207-208
    -   安装 ASM 库驱动程序和实用工具，148-149
    -   Oracleasm 可选参数，152-153
    -   设置 ASM 磁盘，150-154
    -   使用 ASM 磁盘，153-154
-   自动工作负载仓库（Automatic Workload Repository），177, 248
-   autotrace（自动跟踪），374, 375
-   可用性（availability），61
-   Oracle 最大可用性架构（Oracle Maximum Availability Architecture, MAA），166, 167

## B

-   后台进程（background processes），55-57
-   备份（backing up）
    -   归档日志备份，283-285
    -   自动基于磁盘的备份和恢复，294-295
    -   备份文件，34-35
    -   市售备份实用工具，300
    -   控制文件备份，285
    -   使用 Data Pump，297-299
    -   示例，303-304
    -   使用 EXPORT 实用工具，297-299
    -   完全备份，285-286
    -   增量备份，287-288
    -   离线备份，295
    -   联机备份，295-297
    -   概述，274-275
    -   恢复管理器（Recovery Manager, RMAN），289-294
    -   调度，301-303
    -   策略，300-301
    -   表空间和文件备份，286-287
    -   另请参见“恢复”（recovery）
-   /bin 实用工具，12
-   binutils，14, 15-16
-   生物信息学（bioinformatics），62
-   位图索引（bitmap indexes），86
-   位图连接索引（bitmap join indexes），86
-   块设备（block devices），24-25
-   绑定（bonding），202
-   引导加载程序（bootloader），20
-   B 树索引（B-tree indexes），86
-   缓冲池（buffer cache），57
    -   为非标准块大小进行设置，52
-   商业智能（business intelligence），62, 430

## C

-   缓存融合（Cache Fusion），173, 181
-   容量（capacity）
    -   磁盘 I/O 容量，111
    -   系统资源与队列，95-96
-   容量规划（capacity planning），92, 123-124
    -   另请参见“尺寸调整”（Sizing）
-   CBO（基于成本的优化器），380, 382
    -   控制优化器决策，385-388
-   CGI 编程，19-20
-   链式行（chained rows），45, 46
    -   列表，47-48
-   字符设备（character devices），24
-   检查点进程（Checkpoint Process）。参见 CKPT
-   检查点（checkpoints），68-69, 70, 71, 279-280
    -   强制（forcing），72
    -   LOG_CHECKPOINT_INTERVAL，71-72
    -   LOG_CHECKPOINT_TIMEOUT，72
-   CISC 处理器，354-355
-   CKPT，56, 69, 180
-   洁净块（clean blocks），57
-   客户端静态库（Client Static Library），160-161
-   集群就绪服务（Cluster Ready Services, CRS），174-176, 186
    -   集群就绪服务守护程序（Cluster Ready Services Daemon, CRSD），174
        -   配置，204-205
    -   事件管理器守护程序（Event Manager Daemon, EVMD），174, 175
    -   OPRCD，175
    -   Oracle 集群同步服务器守护程序（Oracle Cluster Synchronization Server Daemon, OCSSD），174
-   集群服务同步守护程序（Cluster Services Synchronization Daemon, CSSD），227
-   集群化（clustering），61
    -   活动/活动集群（active/active clusters），169-170
    -   别名，168
    -   活动/备用集群（active/passive clusters），169
    -   集群，87, 167
        -   定义，169
    -   分布式数据库系统，169, 170
    -   回退（failback），168
    -   故障状态（failed state），167
    -   故障转移（failover），168
    -   故障转移集群（failover clusters），169-170
    -   组，168
    -   心跳（heartbeat），168
    -   互连（interconnect），168, 181, 205
    -   节点，167
    -   对象，168
    -   共享磁盘系统，169, 170-171
    -   另请参见“Real Application Clusters”（实时应用集群）
-   冲突（collisions），98
-   用于列出、查看和管理 KLM 的命令，7
-   COMMIT（提交），76, 80-81
-   复合分区（composite partitioning），85, 418, 420
-   并发（concurrency），67
-   为 Oracle 配置 Linux
    -   添加用户和组，133-134
    -   选择组件，128-131
    -   配置文件系统，127-128
    -   配置内核参数，131-133
    -   配置 Oracle 用户的 shell 限制，134
    -   创建目录结构，134-135
    -   安装检查清单，136-139
    -   最低要求，126-127
    -   预安装，126
    -   设置 Oracle 环境，135-136
    -   备份，33
    -   控制文件，33
    -   已格式化分区（cooked partitions），206
-   coreutils，365
-   cpp（GNU 预处理器，GNU preprocessor），15
-   CPU，352, 353-354
-   CPU 缓存，356
    -   设计，354-355
    -   多处理器，355-356
    -   性能与队列，96-97
    -   尺寸调整，104
-   CREATE TABLESPACE 命令，39-40, 42
-   CREATE UNDO TABLESPACE 命令，77
-   crs stat 命令，175-176
-   CSS 守护程序，227
-   累积增量备份（cumulative incremental backups），288, 289

## D

-   数据块（data blocks），44-46
    -   块头，45
    -   链式行，45, 46, 47-48
    -   洁净块，57
    -   脏块（dirty blocks），57
    -   空闲空间，45
    -   迁移的行，45, 46-47, 47-48
    -   非标准块大小，45
    -   PCTFREE，48-50
    -   PCTUSED，48-49, 50-51
    -   行数据，45
    -   行目录，45
    -   表目录，45
    -   使用多种块大小，51-52
-   数据字典（Data Dictionary），58
-   Data Guard，324-326
    -   配置逻辑备用数据库，338-340
    -   配置物理备用数据库，332-337
    -   Data Guard Broker，329
    -   与距离相关，325
    -   日志应用服务，328
    -   日志传输服务，326-328
    -   逻辑备用数据库，330-332
    -   模式，325
    -   物理备用数据库，329-330, 332-337
    -   角色管理服务，328-329
-   数据保护（data guarding），118-119
-   数据完整性（data integrity），68-69
-   Data Pump，61
    -   使用其进行备份，297-299
    -   数据恢复，275-276
    -   数据段，36, 52
    -   数据库挂载状态，224
    -   数据库打开状态，224-225
    -   数据库启动，223
    -   数据库写进程（Database Writer Process）。参见 DBWR
    -   数据文件，31-32, 35
        -   添加到表空间，41
        -   备份，286-287
        -   I/O 和 Oracle 数据文件放置，361
    -   DBA_LOGSTDBY_LOG，340
    -   DBA_LOGSTDBY_PROGRESS，340
    -   DBWR，55, 67, 69

-   DCM。参见分布式配置管理（Distributed Configuration Management）
-   默认缓存（Default Cache），57
-   延迟事务（deferred transactions），344
-   开发环境（development environment），13-14
-   设备（devices）
    -   块设备，24-25
    -   字符设备，24
    -   设备名称，146
    -   原始设备（raw），24, 26-27, 148
    -   rawdevices 服务，146-147
-   字典管理表空间（dictionary managed tablespaces），37
    -   另请参见“表空间”（tablespaces）
-   差异增量备份（differential incremental backups），287-288
-   目录（directories），198-199
    -   Oracle 基础目录，199
    -   Oracle 库存目录，199
    -   目录权限，136
    -   目录结构，8-9
-   脏块，57
-   脏缓冲区（dirty buffers），70, 179
-   磁盘驱动器（disk drive），105-109
    -   性能，109
-   磁盘 I/O 容量，111
-   磁盘镜像（disk mirroring），116
-   磁盘盘片（disk platters），106
-   磁盘寻道表（disk seek sheets），109-110
-   磁盘条带化（disk striping），43, 115-120
-   调度进程（Dispatcher Process）。参见 Dnnn
-   分布式配置管理（Distributed Configuration Management），431-434
-   分布式数据库系统，169, 170
-   DMNin（调度程序，Dispatcher），180
-   DMS。参见动态监视服务（Dynamic Monitoring Service）
-   Dnnn，56
-   文档函数（document functions），62
-   磁盘奇偶校验（drive parity），118-119
-   动态监视服务（Dynamic Monitoring Service），436
-   动态性能视图（dynamic performance views），246-248

## E

-   电子商务集成（e-business integration），430-431
-   E-Business Suite（电子商务套件）
    -   应用层，445-446
    -   446-447, 452-453
    -   体系结构，445-446
    -   将数据库层转换为 RAC，454-455
    -   数据库层，446, 448, 453-455

## F

-   回退（failback），168
-   故障状态（failed state），167
-   故障转移（failover），168
    -   测试，212-213
-   fasik - 命令，150-151
-   光纤通道（Fibre Channel），183
-   文件系统（filesystems），25-26
    -   块大小（blocksize），144
    -   缓存，144
    -   为 Linux 安装进行配置，127-128
    -   创建，144-145
    -   ext3，26
    -   OCFS（Oracle 集群文件系统，Oracle Cluster Filesystem），26, 206
    -   实用工具，10
-   闪存恢复区（flash recovery area），294-295
-   闪回数据库（flashback database），317-318
    -   FLASHBACK DATABASE 命令，83
    -   闪回删除（flashback drop），315-317
    -   闪回特性，294-295, 311-312
    -   闪回操作，82

## G

-   GCC。参见 GNU 编译器集合（GNU compiler collection）
-   gcc 命令，14-15
-   通用操作系统实用工具（general OS utilities），10-11
-   全局动态性能视图（global dynamic performance views），247-248
-   全球化开发工具包（Globalization Development Kit, GDK），62
-   GNOME，用户界面，18
-   GNU 编译器集合，14-15
-   GNU 调试器（GNU Debugger），14, 15
-   GNU 网络对象模型环境（GNU Network Object Model Environment）。参见 GNOME
-   网格计算（grid computing），63
-   组，添加，133-134
-   GUI 环境，18
    -   GNOME，18
    -   KDE，19
-   gv$ 视图，246-248

## H

-   汉明码（Hamming Code），117
-   硬盘。参见磁盘驱动器（disk drive）
-   硬件（hardware）
    -   32位与64位处理器，358-359
    -   选择，352
    -   CPU，352, 353-356
    -   RAM，356-357
    -   尺寸调整，104
    -   调优，253, 352, 359-365
    -   虚拟内存系统，358
-   哈希分区（hash partitioning），85, 418, 419-420
-   心跳（heartbeat），168
-   hugemem 内核，260
-   混合复制（hybrid replication），345
-   混合 X86-64 系统，359

## I

-   IMPORT 实用工具，309
-   增量备份（incremental backups），287-288

