
根据 `cmd` 的值，参数 `sem arg` 代表操作数量或编号：`arg` 有不同的解释方式。参数 `cmd` 表示要执行的操作，其值可以是：

- `IPC_STAT`: 获取信号量组的信息。`semnum` 被忽略，`arg` 是指向包含信息的指针。进程必须具有读取权限以执行此操作。
- `IPC_SET`: 修改信号量组结构的某些值。可以更改的字段是 `sem_perm_uid`、`sem_perm_gid` 和 `sem_perm_mode`。`sem_ctime` 字段会自动更新。进程必须是该组的创建者、所有者或超级用户。
- `IPC_RMID`: 擦除信号量组。进程必须是该组的创建者、所有者或超级用户。

如果系统执行正确，返回 0；否则，返回 -1，且 `errno` 取以下值之一：

| 错误 | 含义 |
| --- | --- |
| `EINTR` | 接收到了信号。 |
| `EINVAL` | 请求的信号量不存在，或者操作数量为负或零。 |
| `ENOMEM` | 设置了 `SEM_UNDO` 且系统无法分配内存。 |
| `ERANGE` | 加到计数器的值可能导致超出计数允许的最大值。 |

当组中的一个信号量被唤醒时，它们会收到错误消息 `EIDRM`。

- `GETPID`: 允许返回信号量 `semnum` 的 `sempid` 的值。它是最后一个对该信号量执行系统调用 `semop` 的进程标识符。该进程必须具有读权限才能执行此操作。
- `GETCNTC`: 允许返回信号量 `semnum` 的 `ementncnt` 的值。这代表等待信号量计数器增加的进程数。该进程必须具有读权限才能执行此操作。
- `GETZCNT`: 允许返回信号量 `semnum` 的 `semzent` 的值。这代表等待信号量计数器变为零的进程数。该进程必须具有读权限才能执行此操作。
- `GETVAL`/`SETVAL`: 允许读取或设置集合 `semid` 中信号量 `semnum` 的值。`arg` 包含被读取或更改的信号量值。在发生更改的地方，操作取消取消结构将被清除，如果值变为零或正数，则等待信号量的进程将被唤醒，并更新 `sem_ctime` 字段。该进程必须具有读权限和写权限。
- `GETALL`/`SETALL`: 允许读取或设置集合 `semid` 中所有信号量的值。`arg` 包含操作的结果或值；参数 `semnum` 被忽略。该进程对该组具有读权限和写权限。

系统调用发生错误时返回 -1，变量 `errno` 包含以下值之一：

|  | 含义 |
| |--- |
| `EACCES` | 调用进程没有足够的权限执行此操作 |
| `EFAULT` | `arg.buf` 或 `arg.array` 指定的地址无效 |
| `EIDRM` | 信号量组已被删除 |
| `EINVAL` | `semid` 或 `cmd` 的值不 |
| `EPERM` | 进程对该操作（命令 `IPC_SET` 或 `IPC_RMID`）没有足够的权限 |
| `ERANGE` | `cmd` 的值为 `SETALL` 或 `SETVAL`，且其中一个信号量的计数器值小于 0 或大于 `SEMVAL` |

如果执行成功，系统调用根据参数 `cmd` 返回正值或零：

## 406 IPC System V

| `GETPID` | `sempid` 的值 |
|---|---|
| `GETVAL` | `semval` 的值 |
| `GETCNCT` | `semncnt` 的值 |
| `GETZCNT` | `semznt` 的值 |

## 11.2.3 共享内存

IPC 带来的一个重要创新是共享内存的管理。在普通程序中，分配的内存区域由执行它的进程所有。其他进程无法访问它。共享内存的原理是允许进程共享它们地址空间的一部分。

尽管共享内存提供了一个非常强大的内存区域共享系统，但它必须建立一种访问同步机制。事实上，可以想象两个进程可能会同时向内存中的同一个点写入数据；可能会违反数据的正确顺序。解决这些问题的方案是使用信号量。

共享内存只能通过两个特定的结构来处理。

### 11.2.3.1 基本结构

结构 `shmid_ds` 和 `shm_info` 定义在头文件 `<linux/shm.h>` 中。然而，只需包含 `<sys/shm.h>` 文件即可访问它们。`shmid_ds` 结构由共享内存表中的条目表示。详情表所示：

| 类型 | 字段 | 描述 |
|---|---|--- |
| `struct ipc_perm` | `shm_perm` | 访问权限 |
| `int` | `shm_gsiz` | 段大小（字节） |
| `time_t` | `shm_atime` | 上一次附加的日期 |
| `time_t` | `shm_stime` | 上一次分离的日期 |
| `time_t` | `shm_ctime` | 上一次修改的日期 |
| `unsigned_short` | `shm_cpid` | 创建进程的编号 |
| `unsigned_short` | `shm_lpid` | 执行上一次操作的进程编号 |
| `short` | `shm_nattch` | 附加数量 |
| `unsigned_short` | `shm_npages` | 段大小（内存页数） |
| `unsigned_long *` | `shm_pages` | 指向内存窗口的指针表 |
| `struct vm_area struct *` | `attaches` | 附加描述符 |

最后三个字段是私有的：它们被内核用于组织共享内存。

同一个头文件定义了 `shminfo`（不要与仅供内核使用的 `shm_info` 结构混淆）。它在用 `IPC_INFO` 作为参数调用 `shmctl` 时使用。该结构例如被 `ipcs` 程序使用。否则，很少被使用（用于系统数据采集或监控程序除外）。详情如下：

| 类型 | 描述 |
|---|--- |
| `int` | `shmax` 最大段大小（字节） |
| `int` | `shmin` 最小段大小（字节） |
| `int` | `shmni` 最大段数 |
| `int` | `shmseg` 每个进程的最大段数 |
| `int` | `shmall` 最大内存页数段 |

### 11.2.3.2 共享内存区域的创建与查找

系统调用 `shmget` 创建一个新的内存区域或获取对现有区域的访问。该调用的通用格式如下：

```c
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>
int shmget(key_t key, size_t size, int shmflg);
```

`key` 用于标识共享内存段。`size` 是要创建段的大小。`shmflg` 包含控制行为的标志（如 `IPC_CREAT`, `IPC_EXCL`）。

如果执行成功，系统调用返回共享内存段的标识符。如果发生错误，`errno` 被置为以下值之一：

| 错误 | 含义 |
|---|---|
| `EACCES` | 权限不足 |
| `EINVAL` | 无效的键或大小 |
| `ENOMEM` | 内存不足 |
| `EEXIST` | 段已存在 |
| `ENOENT` | 无此类段 |

### 11.2.3.3 共享内存的附加

系统调用 `shmat` 允许进程将共享内存区域附加到其地址空间。该调用的通用格式如下：

```c
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>
void *shmat(int shmid, void *shaddr, int shmflg);
```

`shmid` 是要附加的共享内存段的标识符。如果 `shaddr` 为 `NULL`，操作系统选择地址。`shmflg` 包含标志（如 `SHM_RDONLY`）。

如果执行成功，系统调用返回共享内存附加的地址。如果发生错误，`errno` 被置为以下值之一：

| 错误 | 含义 |
|---|---|
| `EACCES` | 权限不足 |
| `EINVAL` | 无效的 `shmid` 或地址 |
| `ENOMEM` | 内存不足 |
| `EIDRM` | 段已被删除 |

### 11.2.3.4 共享内存的分离

系统调用 `shmdt` 允许进程从其地址空间分离共享内存区域。该调用的通用格式如下：

```c
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>
int shmdt(const void *shaddr);
```

`shaddr` 是要分离的共享内存的地址。

如果执行成功，系统调用返回 0。如果发生错误，`errno` 被置为以下值之一：

| 错误 | 含义 |
|---|---|
| `EACCES` | 权限不足 |
| `EINVAL` | 无效地址 |
| `ENOMEM` | 内存不足 |
| `EIDRM` | 段已被删除 |

### 11.2.3.5 共享内存区域的控制

系统调用 `shmctl` 管理共享内存。该调用的通用格式如下：

```c
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/shm.h>
```
