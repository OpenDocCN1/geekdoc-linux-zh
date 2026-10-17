
## 第 15 章 POSIX IPC

经典的 UNIX 进程间通信（IPC）机制——共享内存、消息队列和信号量集在 POSIX:XSI 扩展中得到了标准化。这些机制允许无关进程以合理高效的方式交换信息，使用键来标识、创建或访问相应的实体。这些实体的寿命可能超过创建它们的进程的寿命，但方便的是，POSIX:XSI 还提供了 shell 命令来列出和删除它们。

### 目标

- 学习经典的进程间通信
- 实验同步共享内存
- 探索信号量的实现
- 使用消息队列进行进程间日志记录
- 理解持久化产生的结果

## 15.1 POSIX:XSI 进程间通信

POSIX 进程间通信（IPC）是 POSIX:XSI 扩展的一部分，源于 Unix System V 进程间通信。IPC 包含了消息队列、信号量集和共享内存，提供了在同一系统的进程之间共享信息的机制。这三种通信机制具有相似的结构，本章强调了它们使用的共同元素。表 15.1 总结了 POSIX:XSI 进程间通信函数。

### 表 15.1. POSIX:XSI 进程间通信函数。

| 机制 | POSIX 函数 | 含义 |
|---|---|---|
| 消息队列 | `msgctl` | 控制 |
| | `msgrget` | 创建或访问 |
| | `msgrcv` | 接收消息 |
| | `msgsnd` | 发送消息 |
| 信号量 | `semctl` | 控制 |
| | `semget` | 创建或访问 |
| | `semop` | 执行操作（等待或释放） |
| 共享内存 | `shmat` | 将内存附加到进程 |
| | `shmctl` | 控制 |
| | `shmdt` | 从进程中分离内存 |
| | `shmget` | 创建并初始化或访问 |

### 15.1.1 标识和访问 IPC 对象

POSIX:XSI 通过一个大于等于零的唯一整数来标识每个 IPC 对象，该整数由对象的函数返回，方式与 `open` 函数返回表示文件描述符的整数相同。`msgget` 为消息队列对象返回整数。同样，`semget` 为指定的信号量集返回整数，`shget` 为共享内存段返回整数。这些标识符与在 `sys/msg.h`、`sys/sem.h` 或 `sys/shm.h` 中定义的额外数据结构相关。每个 IPC 类型内部的标识符是唯一的，但你可能两个不同类型的对象拥有整数 1，例如一个信号量集和一个消息队列。

在创建或访问 IPC 对象时，必须指定一个键来确定要创建或访问的特定对象。通过以下三种方法之一选择键：

- 让系统选择键 `IPC_PRIVATE`。
- 直接选择一个键。
- 通过调用 `ftok` 从指定的路径生成键。

`ftok` 函数允许独立进程根据已知的路径派生相同的键。路径对应的文件必须存在，并且对于想要访问 IPC 对象的进程可用。`path` 和 `id` 的组合唯一标识了 IPC 对象。`id` 参数允许从单个路径为多个相同类型的 IPC 对象创建键。

### 语法概要

```
#include <sys/ipc.h>

key_t ftok(const char *path, int id);
```

POSIX:XSI

如果成功，`ftok` 返回一个键。如果失败，`ftok` 返回 `(key_t)-1` 并设置 `errno`。下表列出了 `ftok` 的强制性错误。

| errno | 原因 |
|---|---|
| `EACCES` | 对 `path` 分项的搜索权限被拒绝 |
| `ELOOP` | 在解析 `path` 时存在循环 |
| `ENAMETOOL` | `path` 长度超过 `PATH_MAX`，或路径长度超过 `NAME_MAX` |
| `ENOENT` | `path` 的某个组件不是文件或为空 |
| `ENOTDIR` | `path` 前缀的某个组件不是目录 |

### 示例 15.1

```c
if ((key = ftok("/tmp/trouble", 1)) == (key_t)-1) {
    perror("Failed to derive key");
}
```

### 15.1.2 标识和访问 IPC 对象

POSIX:XSI 通过一个大于等于零的唯一整数来标识每个 IPC 对象，该整数由对象的函数返回，方式与 `open` 函数返回表示文件描述符的整数相同。`msgget` 为消息队列对象返回整数。同样，`semget` 为指定的信号量集返回整数，`shget` 为共享内存段返回整数。这些标识符与在 `sys/msg.h`、`sys/sem.h` 或 `sys/shm.h` 中定义的额外数据结构相关。每个 IPC 类型内部的标识符是唯一的，但你可能两个不同类型的对象拥有整数 1，例如一个信号量集和一个消息队列。

在创建或访问 IPC 对象时，必须指定一个键来确定要创建或访问的特定对象。通过以下三种方法之一选择键：

- 让系统选择键 `IPC_PRIVATE`。
- 直接选择一个键。
- 通过调用 `ftok` 从指定的路径生成键。

`ftok` 函数允许独立进程根据已知的路径派生相同的键。路径对应的文件必须存在，并且对于想要访问 IPC 对象的进程可用。`path` 和 `id` 的组合唯一标识 IPC 对象。`id` 参数允许从单个路径为多个相同类型的 IPC 对象创建键。

### 语法概要

```
#include <sys/ipc.h>

key_t ftok(const char *path, int id);
```

POSIX:XSI

如果成功，`ftok` 返回一个键。如果失败，`ftok` 返回 `(key_t)-1` 并设置 `errno`。下表列出了 `ftok` 的强制性错误。

| errno | 原因 |
|---|---|
| `EACCES` | 对 `path` 分项的搜索权限被拒绝 |
| `ELOOP` | 在解析 `path` 时存在循环 |
| `ENAMETOOL` | `path` 长度超过 `PATH_MAX`，或路径长度超过 `NAME_MAX` |
| `ENOENT` | `path` 的某个组件不是文件或为空 |
| `ENOTDIR` | `path` 前缀的某个组件不是目录 |

### 示例 15.1

```c
if ((key = ftok("/tmp/trouble", 1)) == (key_t)-1) {
    perror("Failed to derive key");
}
```

## 15.2 POSIX:XSI 信号量集

POSIX:XSI 信号量由信号量元素组成。信号量元素与 Dijkstra 在第 14 节中描述的经典整数相似但不完全相同。进程可以在一次调用中对整个集合执行操作。因此，POSIX:XSI 信号量能够实现 14.2 节描述的同步功能。我们称为 POSIX:XSI 信号量集以将其区分开。

每个信号量元素至少包含以下内容：

- 表示信号量元素值的非负整数 (`semval`)
- 上一个操作该信号量元素的进程 ID (`sempid`)
- 等待信号量值增加的进程数 (`semncnt`)
- 等待信号量值等于 0 的进程数 (`semzcnt`)

信号量的主要数据结构是 `sem_id`，它定义在 `sys/sem.h` 中并具有以下成员：

```
struct ipc_perm sem_perm; /* 操作权限结构 */
unsigned short sem_nms; /*集合中信号量的数量 */
time_t sem_otime; /* 上次 semop 的时间 */
time_t sem_ctime; /* 上次 semctl 的时间 */
```

### 15.2.1 信号量的创建

`semget` 函数返回由键参数标识的信号量。如果键为 `IPC_PRIVATE` 或 `semflg & IPC_CREAT` 为非零且没有已与键关联的信号量集或标识符，`semget` 函数将创建标识符及其关联的信号量集。`nms` 参数指定集合中信号量元素的数量。信号量集中的单个信号量元素通过整数 0 到 `nms-1` 进行引用。信号量具有由 `semget` 参数 `semflg` 指定的权限。权限与第 4.3 节中描述文件的方式相同，并通过调用 `semctl` 修改权限。信号量元素应该用 `semctl` 进行初始化：

```
语法概要
#include <sys/sem.h>
int semget(key_t key, int nms, int semflg);
```

POSIX:XSI

如果成功，`semget` 返回一个与信号量标识符对应的非负整数。

如果失败，`semget` 函数返回 `-1` 并设置 `errno`。下表列出了 `semget` 的强制性错误。

| errno | cause |
|---|---|
| `EACCES` | key 存在信号量，但未授予权限 |
| `EEXIST` | key 存在信号量，但 ((semflg & IPC_CREAT) && (semflg & IPC_EXCL)) != 0 |
| `EINVAL` | nms <= 0 或大于系统限制，或 nsems 与信号量不符 |
| `ENOENT` | key 不存在信号量，且 (semflg & IPC_CREAT) == 0 |
| `ENOSPC` | 将超过系统限制 |

如果一个进程尝试创建一个已经存在的信号量，它将获取指向现有信号量的句柄，除非 `semflg` 包含了 `IPC_CREAT` 和 `IPC_EXCL`。在后一种情况下，`semget` 将失败并将 `errno` 设置为 `EEXIST`。

## 示例 15.3

以下代码生成了一个包含三个信号量元素的新信号量集合。

```c
#define PERMS (S_IRUSR | S_IWUSR)

int semid;
if ((semid = semget(IPC_PRIVATE, 3, PERMS)) == -1)
    perror("Failed to create new private semaphore");
```

该信号量只能由所有者读或写。

`IPC_PRIVATE` 键保证 `semget` 会创建一个新的信号量。要从伪键或派自路径获取新的信号量集合，进程必须指定使用 `IPC_CREAT` 标志表示它正在创建一个新信号量。如果同时指定了 `IPC_CREAT` 和 `IPC_EXCL`，当信号量已存在，`semget` 将返回错误。

## 示例 15.4

以下代码段访问由键值 99887 标识的单元素信号量集合。

```c
#define PERMS (S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP | S_IROTH | S_IWOTH)
#define KEY ((key_t)99887)
```

```c
int semid;
if ((sem = semget(KEY, 1, PERMS | IPC_CREAT)) == -1)
    perror("Failed to access semaphore with key 99887");
```

`IPC_CREAT` 标志确保如果信号量集合不存在，`semget` 将创建它。权限允许所有用户访问该信号量集合。

提供特定的键值允许协作进程就通用的信号量集合达成一致。如果信号量已经存在，`semget` 返回其句柄。如果将 `semget` 的 `semflag` 参数替换为 `PERMS | IPC_CREAT, IPC_EXCL`，当信号量已存在时，`semget` 将返回错误。

程序 15.1 展示了如何使用从路径生成的键和 ID 作为命令行参数来标识信号量集合。如果 `semfrompath` 执行成功，信号将在程序退出后仍然存在。你将需要调用 `ipcrm` 命令来删除它们。

## 程序 15.1 semfrompath.c

一个从路径键创建信号量的程序。

```c
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/sem.h>
#include <sys/stat.h>
#define PERMS (S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP | S_IROTH | S_IWOTH)
#define SET_SIZE 2
```

```c
int main(int argc, char *argv[]) {
    key_t mykey;
    int semid;

    if (argc != 3) {
        fprintf(stderr, "Usage: %s pathname\n", argv[0]);
        return 1;
    }
    if ((mykey = ftok(argv[1], atoi(argv[2]))) == (key_t)-1) {
        fprintf(stderr, "Failed to derive key from filename %s:%s\n",
            argv[1], strerror(errno));
        return 1;
    }
    if ((semid = semget(mykey, SET_SIZE, PERMS | IPC_CREAT)) == -1) {
        fprintf(stderr, "Failed to create semaphore with key %d:%s\n",
            mykey, strerror(errno));
        return 1;
    }
    printf("semid = %d\n", semid);
```c

return 0;

}
```

## 15.2.2 信号量控制

信号量集合中的每个元素在使用之前都必须用 `semctl` 进行初始化。`semctl` 函数为信号量 `semid` 中的元素 `semnum` 提供控制操作。`cmd` 参数指定操作类型。可选的第四个参数 `arg` 取决于 `cmd` 的值。

## 语法概要 (SYNOPSIS)

```c
#include <sys/sem.h>

int semctl(int semid, int semnum, int cmd, ...);
```

POSIX:XSI

如果成功，`semctl` 返回一个非负值，其解释取决于 `cmd`。`cmd` 的 `GETVAL`、`GETPID` 和 `GETZCNT` 值会导致 `semctl` 返回与 `cmd` 关联的值。`cmd` 的其他所有值导致 `semctl` 在成功时返回 0。如果失败，`semctl` 返回 `-1` 并设置 `errno`。下表列出了 `semctl` 的强制性错误。

| errno | cause |
|---|---|
| `EACCES` | 调用者拒绝操作 |
| `EINVAL` | semid 或 cmd 值无效，或 semnum 为负数或过大 |
| `EPERM` | cmd 为 IPC_ID 或 SET 但调用者没有权限 |
| `ERANGE` | cmd 为 SETVAL 或 SETALL 但值超出范围 |

表 15.2 给出了 `cmd` 参数的 POSIX 值。

| cmd | description |
|---|---|
| `GETALL` | 返回 arg 中信号量集合的值 |
| `GETVAL` | 返回特定信号量元素的值 |
| `GETPID` | 返回操作元素的进程 ID |
| `GETIPC` | 返回等待增加元素的进程数 |
| `GETZCNT` | 返回等待元素变为 0 的进程数 |
| `IPC_RM` | 删除 semid 标识的信号量 |
| `IPC_SET` | 设置 arg 中信号量集合的权限 |
| `IPC_STAT` | 将信号量集合的 semid_ds 成员拷贝到 arg |
| `SETALL` | 设置 arg 中信号量集合的值 |
| `SETVAL` | 设置 arg 中特定信号量元素的值 |

`GETALL` 和 `SETALL` 命令都需要 `arg` 参数来读取或存储结果。`arg` 类型为 `semun`，定义如下：

```c
union semun {
    int val;
    struct semid_ds *buf;
    unsigned short *array;
};
```

## 示例 15.5 semelement.c

`semelement` 函数将指定的信号量元素设置为 `semvalue`。

```c
#include <sys/sem.h>

int semelement(int semid, int semnum, int semvalue) {
    union semun {
        int val;
        struct semid_ds *buf;
        unsigned short *array;
    } arg = {semvalue};
    return semctl(semid, semnum, SETVAL, arg);
}
```
