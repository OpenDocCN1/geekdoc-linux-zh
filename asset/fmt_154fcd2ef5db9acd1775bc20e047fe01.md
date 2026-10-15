
## semctl

`semctl` API 提供了对信号量或信号量数组的多种控制操作。功能示例范围从设置信号量的值（如列表 17.6 所示）到移除信号量或信号量数组（参见列表 17.7）。在本节中，你将有机会看到这些以及其他示例。`semctl` 调用的函数原型如下：

```
int semctl(int semid, int semnum, int cmd, ...)
```

# 第 17 章 使用信号量进行同步 317

第一个参数定义了信号量标识符，第二个参数定义了感兴趣的信号量编号，第三个参数定义了要应用的命令，然后可能还有另一个参数（通常定义为联合体 `union`）。可以执行的操作如表 17.4 所示。

### 表格 17.4 使用 semctl 可以的操作

| 命令 | 描述 | 第四个参数 |
| --- | --- | --- |
| `GETVAL` | 返回信号量的值。 | |
| `SETVAL` | 设置信号量的值。 | `int` |
| `GETPID` | 返回最后对信号量进行操作（`semop`）的进程 ID。 | |
| `GETNCNT` | 返回等待信号量数值增加的进程数量。 | `int` |
| `GETZCNT` | 返回等待数值变为零的进程数量。 | `int` |
| `GETALL` | 返回信号量数组中每个信号量的值。 | `u_short*` |
| `SETALL` | 设置信号量数组中每个信号量的值。 | `u_short*` |
| `IPC_STAT` | 返回信号量的有效用户、组和权限。 | `struct semid_ds*` |
| `IPC_SET` | 设置信号量的有效用户、组和权限。 | `struct semid_ds*` |
| `IPC_RMID` | 移除信号量或信号量数组。 | |

现在是时候查看 `semctl` 中这些操作的每个示例了，在适用时重点关注信号量数组示例。第一个示例说明了设置信号量的值然后返回其值。在这个示例中，你首先将信号量的值设置为 10（使用 `SETVAL` 命令），然后使用 `GETVAL` 将其读回。注意，第二个参数（参数 2）定义了一个单个信号量。稍后你可以查看使用 `GETALL` 和 `SETALL` 的信号量数组情况。

```
int semid, ret, value;

...

/* 将信号量设置为 10 */
ret = semctl(semid, 0, SETVAL, 10);

...

/* 读取信号量的值（返回值） */
value = semctl(semid, 0, GETVAL);
```

`GETPID` 命令允许你识别最后一个对信号量执行 `semop` 操作的进程。进程标识符是返回值，在这种情况下不使用第四个参数。

```
int semid, pid;
pid = semctl(semid, 0, GETPID);
```

如果没有对信号量执行过 `semop`，则返回值为零。要识别等待信号量数值增加的进程数量，你可以使用 `GETCNT` 命令。你也可以使用 `GETCNT` 识别等待信号量变为零的进程数量。这两个命令在下文中针对信号量零进行了说明：

```
int semid, count;
/* 有多少进程正在等待此信号量增加 */
count = semctl(semid, 0, GETCNT);
/* 有多少进程正在等待此信号量变为零 */
count = semctl(semid, 0, GETCNT);
```

现在是时候查看一些信号量数组操作的示例了。列表 17.8 展示了使用 `semctl` 的 `SETVAL` 和 `GETVAL`。在这个示例中，你创建了一个包含 10 个信号量的信号量数组。信号量数组的创建是在第 20–21 行使用 `semget` 函数完成的。注意，由于你将在此函数内部创建并移除信号量数组，你没有使用键，而是使用了 `IPC_PRIVATE`。`MAX_SEMAPH` 定义了信号量的数量。

# 第 17 章 使用信号量同步 321

```
60:    printf("Semaphore %d, value %d\n", i, ret);
61:
62:    }
63:
64:    /* 删除信号量 */
65:    ret = semctl(semid, 0, IPC_RMID);
66:
67:    } else {
68:
69:    printf("Could not allocate semaphore (%d)\n", errno);
70:
71:    }
72:
73:    return 0;
74:    }
```

执行此应用程序（称为 `semall`）将产生如列表-17.9所示的输出。并不意外，`GETVAL` 输出的内容与 `GETALL` 显示的相同。

### 列表 17.9 列表 17.8所示的 semall 应用程序输出

```
# ./semall
Semaphore 0, value 1
Semaphore 1, value 2
Semaphore 2, value 3
Semaphore 3, value 4
Semaphore 4, value 5
Semaphore 5, value 6
Semaphore 6, value 7
Semaphore 7, value 8
Semaphore 8, value 9
Semaphore 9, value 10
Semaphore 0, value 1
Semaphore 1, value 2
Semaphore 2, value 3
Semaphore 3, value 4
Semaphore 4, value 5
Semaphore 5, value 6
Semaphore 6, value 7
Semaphore 7, value 8
Semaphore 8, value 9
Semaphore 9, value 10
#
```

## GNU/Linux 应用程序编程

`IPC_STAT` 命令检索有关信号量或信号量数组的当前信息。数据被检索到一个名为 `semid_ds` 的结构体中并包含了各种参数。读取这些信息的应用程序在列表 17.10 所示。你在第 23 行使用 `semctl` API 函数通过 `IPC_STAT` 命令读取信号量信息。捕获的信息随后在第 27–49 行输出。

### 列表 17.10 使用 IPC_STAT 读取信号量信息（光光 /source/ch17/semstat.c）

```
1:   #include <stdio.h>
2:   #include <sys/sem.h>
3:   #include <time.h>
4:   #include "common.h"
5:
6:   int main() {
7:   {
8:       int semid, ret;
9:       struct semid_ds sembuf;
10:
11:      union semun {
12:          int val;
13:          struct semid_ds *buf;
14:          unsigned short *array;
15:      } arg;
16:
17:      /* 获取 ID 为 MY_SEM_ID 的信号量 */
18:      semid = semget( MY_SEM_ID, 1, 0);
19:
20:      if (semid >= 0) {
21:          arg.buf = &sembuf;
22:          ret = semctl(semid, 0, IPC_STAT, arg);
23:
24:          if (ret != -1) {
25:
26:              if (sembuf.sem_otime) {
27:                  printf("Last semop time %s",
28:                         ctime(&sembuf.sem_otime));
29:              }
30:          }}
```

# 第 17 章 使用信号量同步 323

```
32:    printf("Last change time %s",
33:        ctime(&sembuf.sem_ctime ) );
34:
35:    printf("Number of semaphores %d\n",
36:        sembuf.sem_nsems );
37:
38:    printf("Owner's user id %d\n",
39:        sembuf.sem_perm.uid );
40:    printf("Owner's group id %d\n",
41:        sembuf.sem_perm.gid );
42:
```
