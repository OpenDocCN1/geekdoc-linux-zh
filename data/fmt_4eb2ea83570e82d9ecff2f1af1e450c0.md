
- 设置所有值（19-24）：我们为每个成员分配一个无符号短型数组，并将命令行中的值复制到数组中。通过 `semctl` 发出 `SETALL` 命令设置集合中的所有值。

### semgetvalues 程序

图 11.5 显示了我们的 `semgetvalues` 程序，它获取并打印信号量集中的所有值。

- 获取集合中的信号量数量（1-15）：在用 `semget` 获取信号量 ID 后，我们向 `semctl` 发出 `IPC_STAT` 命令来获取信号量的 `sem_ds` 结构。`sem_nsem` 成员是集合中信号量的数量。

- 获取所有值（16-22）：我们为每个成员分配一个无符号短型数组，并向 `semctl` 发出 `SETALL` 命令来获取集合中的所有值。打印每个值。

### semops 程序

图 11.6 显示了我们的 `semops` 程序，对信号量集执行一组操作。

- 命令行选项（7-19）：选项 `-n` 为每个操作指定 `IPC_NOWAIT` 标志，选项 `-u` 为每个操作指定 `SEM_UNDO` 标志。注意，`semop` 函数允许为 `sembuf` 结构中的每个成员（即对集合中每个成员的操作）指定一组标志，但为了简单起见，我们使用命令行选项为所有指定的操作指定该标志。

- 为操作分配内存（20-29）：用 `semget` 打开信号量集后，分配一个 `sembuf` 结构数组，每个命令行操作对应一个元素。与之前的两个程序不同，此程序允许用户指定少于信号量成员的操作。

- 执行操作（30）：`semop` 在信号量集上执行操作数组。

# 第 115

```c
#include "unipipc.h"
int
main(int argc, char **argv) {
    int semid;
    if (argc != 2)
        err_quit("usage: semmrid <pathname>");
    semid = semget(ftok(argv[1]), 0, 0);
    semctl(semid, 0, IPC_RMID);
    exit(0);
}
```

```c
#include "unipipc.h"
int
main(int argc, char **argv) {
    int semid, nsems, i;
    struct sem_ds seminfo;
    unsigned short *ptr;
    union arg;
    if (argc != 2)
        err_quit("usage: semvalues <pathname> [ ... ]");
    /* 获取信号量中的信号量数量 */
    semid = semget(ftok(argv[1]), 0, 0);
    arg.buf = &seminfo;
    semctl(semid, 0, IPC_STAT, arg);
    nsems = arg.buf->sem_nsems;
    /* 从命令行获取值 */
    if (argc != 2)
        err_quit("%d values in sets, %d values specified", nsems, 2);
    /* 分配内存来存储集合中的所有值，并存储 */
    ptr = calloc(nsems, sizeof(unsigned short));
    arg.array = ptr;
    for (i = 0; i < nsems; i++)
        ptr[i] = atoi(argv[i+2]);
    semctl(semid, 0, SETALL, arg);
    exit(0);
}
```

# 简单程序 291

# System V 信号量

```c
1 #include "unipipc.h"
2 int
3 main(int argc, char **argv)
4 {
5     int semid, nsems, i;
6 struct sem_ds seminfo;
7     unsigned short *ptr;
8 union semarg;
9
10 if (argc < 2)
11     err_quit("usage: semvalues <pathname>");
12     /* 获取信号量中的信号量数量 */
13     semid = semget(ftok(argv, 1), 0, 0);
14     arg.buf = semctl(semid, 0, IPC_STAT, arg);
15     nsems = arg.buf->sem_nse;
16
17     /* 分配内存来存储集合中的所有值 */
18     ptr = malloc(nsems * sizeof(unsigned short));
19     arg.array = ptr;
20
21     /* 获取值并打印 */
22     semctl(semid, 0, GETALL, arg);
23     for (i = 0; i < nsems; i++)
24         printf("semval[%d] = %d\n", i, ptr[i]);
25
26     exit(0);
27 }
```

图 11 `semvalues` 程序。

```c
1 #include "unipipc.h"
2 int
3 main(int argc, char **argv)
4 {
5     int c, i, flag, semid, nops;
6     struct sembuf *ptr;
7
8     flag = 0;
9     while (c = getopt(argc, argv, "nu")) != -1)
10         switch (c) {
11             case 'n':
12                 flag = IPC_NOWAIT; /* 每次操作 */
13                 break;
14
15             case 'u':
16                 flag = SEM_UNDO; /* 每次操作 */
17                 break;
18         }
19
20     if (argc - optind < 2)
21         err_quit("usage: semops [-n] [-u] <pathname> operation ...");
```

```c
20 semid = semget(ftok(argv[optind], 0), 0, 0);
21 optind++;
22 nops = argc - optind;
3
23     /* 分配内存来存储操作、存储并执行 */
24     ptr = calloc(nops, sizeof(struct sembuf));
25     for (i = 0; i < nops; i++) {
26         ptr[i].sem_num = i;
27         ptr[i].sem_op = atoi(argv[optind] + i); /* < 0, 或 > 0 */
28         ptr[i].sem_flg = flag;
29     }
30 semop(semid, ptr, nops);
31
32 exit(0);
33 }
```

# 示例

我们通过查看之前展示的五个程序，演示 System V 信号量的某些特性。

```bash
solaris % touch /tmp/rich
solaris % semcreate /tmp/rich 3
solaris % semvalues /tmp/rich 1 2 3
solaris % semget /tmp/rich
semval[0] = 1
semval[1] = 2
semval[2] = 3
```

我们首先创建一个名为 `/tmp/rich` 的文件，它将用于 `ftok` 用来识别信号量集合。`semcreate` 创建了一个具有三个成员的集合。`semvalues` 将值设为 0, 1 和 3，然后由 `semvalues` 打印。

我们演示在信号量集合上执行一组操作的原子性。

```bash
solaris % semops -n /tmp/rich -1 2 -4
semctl: temporarily unavailable
solaris % semvalues /tmp/rich
semval[0] = 1
semval[1] = 2
semval[2] = 3
```
