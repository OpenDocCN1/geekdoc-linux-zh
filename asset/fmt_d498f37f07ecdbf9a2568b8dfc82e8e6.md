
```c
key_t mySem;
int semid;
// 根据定义的路径和数字创建键
myKey = ftok("/home/mtj/semaphores/mysem", 0);
semid = semget(myKey, 1, IPC_CREAT | IPC_EXCL | 0666 );
```

注意，使用这些参数调用 `ftok` 时，生成的键（这就是为什么这种方法有效！）只要每个访问信号量的进程都知道文件和数字，键就可以重新计算并用于标识该信号量。

在目前为止的示例中，你创建了一个单个信号量。你可以通过指定大于1的 `nsems` 值来创建一个信号量数组，如下：

```c
semarray = semget( myKey, 10, IPC_CREAT | 0666 );
```

结果是一个包含 10 个信号量的信号量数组。（*此处省略重复描述*）

336 GNU/Linux 应用编程

你可以创建一个单个信号量（`nsems` 值为 1）或多个信号量。如果你使用 `semget` 获取已有的信号量，此值可以简单地为 0。

最后，`semflg` 参数允许你更改 `semget` API 函数的行为。

316 GNU/Linux 应用编程

你还指示了信号量已经存在，你不简单地获取它的值，而是让调用失败。记住这是 `IPC_EXCL` 命令提供的，

```c
printf("信号量已存在，或出错\n");
```

结果是一个包含 10 个信号量的信号量数组。（*此处省略重复描述*）

结果是一个包含 13 个值的信号量数组。

| 符号 | 值 | 含义 |

|---|---|---|

| S_IRUSR | 0400 | 用户具有读权限 |

| S_IWUSR | 0200 | 用户具有写权限 |

| S_IRGRP | 0040 | 组具有读权限 |

| S_IWGRP | 0020 | 组具有写权限 |

| S_IROTH | 0004 | 其他用户具有读权限 |

| S_IOWTH | 0002 | 其他用户具有写权限 |

现在是时候看几个 `semget` 的示例了，它们分别在本节之前定义的三个场景中使用。在接后的示例中，假设 `sem` 是一个 `int` 值，`mySem` 的类型为 `key_t`。在第一个示例中，你创建一个私类型的新信号量（或访问一个已有的）。

关于信号量的最后一点是，就像消息队列一样，一组

## semctl

`semctl` API 函数为信号量提供了若干控制操作。功能示例从设置信号量的值（如列表 17.6 所示）到移除信号量或信号量数组（见 17.7）。你将看到这些。

第一个参数定义信号量标识符，第二个参数定义信号量数量，第三个定义要应用的命令，然后可能还有另一个参数（通常定义为联合）。可以执行的操作见表 17.4。

第 17 章 使用信号量同步 317

### 表 17.4 使用 semctl 执行的操作

| 命令 | 说明 | 第四个参数 |

|---|---|---|

| GETVAL | 返回信号量的值。 | |

| SETVAL | 设置信号量的值。 | int |

| GETPID | 返回最后操作信号量的进程 ID (`semop`)。 | |

| GETNCNT | 返回等待信号量增加值的进程数。 | int |

| GETZ | 返回等待信号量变为零的进程数。 | int |

| GETALL | 返回信号量数组中每个信号量的值。 | u_short* |

| SETALL | 设置信号量数组中每个信号量的值。 | u_short* |

| IPC_STAT | 返回信号量的有效用户、组和权限。 | struct semid_ds* |

| IPC_SET | 设置信号量的有效用户、组和权限。 | struct semid_ds* |

| IPC_RMID | 移除信号量或信号量数组。 | |

# 318 GNU/Linux 应用程序编程

```c
int semid, ret, value;
...
/* 将信号量设置为 10 */
ret = semctl( semid, 0, SETVAL, 10 );
```

```c
/* 读取信号量的值（返回值） */
value = semctl(semid, 0, GETVAL);
```

`GETPID` 命令允许你识别上一个对信号量执行 `semop` 的进程。进程标识符是返回值，在这种情况下，参数 1 不被使用。

```c
int semid, pid;
...
pid = semctl( semid, 0, GETPID );
```

如果信号量上没有执行过任何 `semop`，则返回零。要确定当前正在等待信号量值增加的信号量数量，可以使用 `GETCNT` 命令。你也可以使用 `GETZCNT` 来确定等待信号量值变为零的进程数量。这两个命令均在下文中针对编号为零的信号量进行了说明：

```c
int semid, count;
/* 有多少进程正在等待此信号量增加 */
count = semctl( semid, 0, GETCNT );
/* 有多少进程正在等待此信号量变为零 */
count = semctl( semid, 0, GETZCNT );
```

现在是时候看一个信号量数组操作示例了。列表 17.8 展示了使用 `semctl` 的 `SETVAL` 和 `GETCNT` 命令。

在这个示例中，你创建了一个包含 10 个信号量的信号量数组。信号量数组的创建是在第 20-21 行使用 `semget` API 函数完成的。注意，由于你将在同一个函数内创建并删除数组，因此你没有使用键（key），而是使用了 `IPC_PRIVATE` 键。`MAX_SEMAPHORES` 符号定义了你要创建的信号量数量，最后你指定使用标准权限创建信号量数组（`IPC_CREAT`）。

接下来，你初始化了信号量值数组（第 26-30 行）。虽然这不是一个传统的示例，但你将每个信号量初始化为索引加一（信号量0的值为1，信号量1值为2，以此类推）。这样做是为了让你以后可以检查值数组并知道你在查看什么。

# 第 17 章 使用信号量进行同步 319

在第 33 行，你将 `arg.array` 参数设置为数组的地址（`sem_array`）。注意你正在使用 `sem` 联合体，它定义了一些用于信号量的类型。在这种情况下，你使用 `unsigned short` 字段来表示一个信号量值数组。

在第 36 行，使用 `semctl` API 函数和 `SETALL` 命令来设置信号量的值。你提供的信号量标识符 `semid` 为零（在此情况下不使用），`SETALL` 命令，最后是 `semun` 联合体。当此 API 函数返回时，由 `semid` 标识的信号量数组将具有 `sem_array` 中定义的值。

接下来，你探索了 `GETALL` 命令，它用于检索信号量数组的值。你在第 41 行设置了第一个参数（只是为了避免使用包含你所需内容的现有数组）。在再次调用 `semctl` 时，传入了 `semid`、未使用的零（此处再次未使用）、`GETALL` 命令和 `semun` 联合体。

为了说明你所读的内容，你接下来遍历了 `sem_read_array`，并为信号量数组中的每个信号量索引输出每个值（第 49–53 行）。

虽然 `GETALL` 允许你通过一次调用检索整个信号量数组，但你可以使用 `GETVAL` 命令执行相同的操作，对该数组的每个信号量调用 `semctl`。这在第 56–62 行给出所示。这同样适用于 `SETVAL` 的行为。

最后，在第 65 行，使用带有 `IPC_RMID` 命令的 `semctl` API 函数来移除信号量数组。

# 列表 17.8 创建和操作信号量数组（位于 CD-ROM 的 /source/ch17/semmall.c）

```c
1:   #include <std.h>
2:   #include <sys/types.h>
3:   #include <sys/sem.h>
4:   #include <errno.h>
5: 
6:   #define MAX_SEMAPHORES 10
7: 
8:   int main() {
9: 
10:  int i, ret, semid;
11:  unsigned short sem_array[MAX_SEMAPHORES];
12:  unsigned short sem_read_array[MAX_SEMAPHORES];
13: 
14:  union semun {
15:  int val;
```

# 320 GNU/Linux 应用程序编程
