
## 描述

手册页涉及 System V 进程间通信机制的 Linux 实现：消息队列、信号量集和共享内存机制。在下文中，“资源”指的是此类机制的实例化。

## 资源访问权限

对于每个资源，系统使用 `struct ipc_perm` 的通用结构来存储确定执行 ipc 操作所需的权限信息。由 `<sys/ipc.h>` 系统头文件定义的 `ipc_perm` 结构包含以下成员：

```
ushort cuid; /* 创建者用户 id */
ushort cgid; /* 创建者组 id */
ushort uid; /* 所有者用户 id */
ushort gid; /* 所有者组 id */
ushort mode; /* r/w权限 */
```

`ipc_perm` 结构的 `mode` 成员通过其低九位定义执行 ipc 系统调用的进程对资源的访问权限。权限解释如下：

- `0400` 用户读取。
- `0200` 用户写入。
- `0040` 组读取。
- `0020` 组写入。
- `0004` 其他人读取。
- `0002` 其他人写入。

位 `0100`、`0010` 和 `0001`（执行位）未被系统使用。此外，对于信号量集，“写”实际上意味着“修改”。

同一个系统头文件定义了所有以下符号常量：

- `IPC_CRE` 如果键 不存在则创建项。
- `IPC_EXCL` 如果存在则失败。
- `IPC_NOWAIT` 如果请求必须等待则报错。
- `IPC_PRIVATE` 私有键。
- `IPC_RMID` 资源。
- `IPC_SET` 设置资源选项。
- `IPC_STAT` 获取资源选项。

注意 `IPC_PRIVATE` 是 `key_t` 类型，而所有其他符号常量都可以通过 OR 操作合并到 `int` 变量。

## 消息队列

消息由一个正整数（其 `msqid`）唯一标识，并有一个类型为 `struct msqid_ds` 的关联数据结构，定义在 `<sys/msg.h>` 中，包含以下成员：

- `msq_perm` `ipc_perm` 结构，指定对消息队列的访问权限。
- `msq_qnum` 消息队列上当前的消息数量。
- `msq_qbytes` 消息队列允许的消息文本最大字节数。
- `msq_lspid` 执行上一次 `msnd` 系统调用的进程 ID。
- `msq_lrpid` 执行上一次 `msgrcv` 系统调用的进程 ID。
- `msq_stime` 上一次 `msnd` 系统调用的时间。
- `msq_rtime` 上一次 `msgrcv` 系统调用的时间。
- `msq_ctime` 上一次更改 `msqid_ds` 结构成员的系统调用时间。

## 信号量集

信号量集由一个正整数（其 `semid`）唯一标识，并有一个类型为 `struct sem_ds` 的关联数据结构，定义在 `<sys/sem.h>` 中，包含以下成员：

```c
struct ipc_perm sem_perm;
time_t sem_otime; /* 最后操作时间 */
```

```
time_t sem_ctime; /* 最后修改时间 */
ushort sem_nsms; /* 设置中 nms 的计数 */
```

`sem_perm` `ipc_perm` 结构，指定对信号量集的访问权限。

`sem_etime` 上一次 `semop` 系统调用的时间。

`sem_ctime` 上一次修改的时间。

`sem_nsms` 设置中 nms 的计数。

> 注：以下几行描述了当 `inmatch` 处于 `run` 状态且平均负载上升到或超过 6 时，服务器的行为。发生这种情况时，状态设置为 `load`。之前的几行导致当 `inmatch` 处于 `run` 或 `load` 状态且平均负载上升到 8 以上时，服务器被节流。注意，当平均负载从 6 升到 7 然后升到 8 以上时，`inmatch` 可以将服务器从暂停状态切换为节流状态。第一行导致当 `inmatch` 处于 `load` 或 `hiload` 状态且平均负载下降到 5 以下时，向服务器发送一个命令。注意所有行都假设有一个命令 `loadavg` 可以以整数打印当前的平均负载。在实际情况下，将 `uptime` 输出通过 `awk` 处理可能会很有用。

## 共享内存段

共享内存段由一个正整数（其 `shmid`）唯一标识，并有一个类型为 `struct shmid_ds` 的关联数据结构，定义在 `<sys/shm.h>` 中，包含以下成员：

```c
struct ipc_perm sem_perm;
time_t sem_otime; /* 最后操作时间 */
time_t sem_ctime; /* 最后修改时间 */
ushort sem_nsms; /* 设置中 nms 的计数 */
```

## 第五部分：文件格式
