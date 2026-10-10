
另一种类型是计数信号量，用于表示数量大于 1 的共享资源。考虑缓冲区池。计数信号量可以通过其值（可用缓冲区数量）来代表整个缓冲区集合。每当进程需要缓冲区时，它就会获取信号量，这会使其值减1。当信号量达到零时，进程会被阻塞，直到值变为非零。当信号量被释放时，值增加，从而允许其他进程获取信号量（以及关联缓冲区）。这是计数信号量的用途之一（见图 17.2）。

在计数信号量示例中，每个进程在执行所需的活动之前需要两个资源。在这个示例中，计数信号量的值为 3，这意味着一次允许一个进程完全运行。进程 A 先获取了它的两个资源，这意味着进程 B 将阻塞直到进程 A 释放至少一个资源。

![](img/f7bd35eb87a62f74c6f23c07df847dff_324_0.png)

图 17.2 两个进程的计数信号量。

## GNU/LINUX 信号量快速概述

本章从信号量 API 的之旅开始。查看如何创建、查找、获取、释放、配置和删除信号量。在完成此概览后，你可以深入研究。

Linux 中的信号量实际上是数组。单个信号量可以同时代表许多资源。GNU/Linux 信号量 API 比许多信号量 API 稍微复杂一些。

## 创建信号量

要创建信号量（或获取现有的信号量），使用 `semget` 函数。该函数接收一个键、一个计数和标志。在接下来的示例中，你使用了 0666 权限。它被初始化为 0。

### 列表 17.1 使用 semget 创建信号量

```c
#include <stdio.h>
#include <sys/sem.h>
#include "common.h"

int main() {
    int semid;

    /* 创建 id 为 MY_SEM_ID 的信号量 */
    semid = semget(MY_SEM_ID, 1, 0666 | IPC_CREATE);

    if (semid >= 0) {
        printf("semcreate: Created a semaphore %d\n", semid);
    }

    return 0;
}
```

完成这个简单的应用程序后，将有一个由 `MY_SEM_ID` 标识的新的全局可用信号量。系统中的任何进程都可以此信号量。

## 获取与释放信号量

查看一个尝试获取现有信号量的应用程序以及另一个释放它的应用程序。回你之前创建的信号量（列表 17.1 中）被初始化为 0。这等同于二进制信号量已被获取。

列表 17.2 展示了一个获取你的信号量的应用程序。GNU/Linux 信号量 API 比许多信号量 API 稍微复杂，但它符合 POSIX 标准，因此对于迁移到其他 Unix 类的操作系统非常重要。

### 列表 17.2 使用 semop 获取信号量

```c
#include <stdio.h>
#include <sys/sem.h>
#include <stdlib.h>
#include "common.h"

int main() {
    int semid;
    struct sembuf sb;

    /* 获取 id 为 MY_SEM_ID 的信号量 */
    semid = semget(MY_SEM_ID, 1, 0);

    if (semid >= 0) {
        sb.sem_num = 0;
        sb.sem_op = -1;
        sb.sem_flg = 0;

        printf("semacq: Attempting to acquire semaphore%d\n", semid);
    }
}
```

## 第 17 章 信号量同步 307

```c
22:    /* 获取信号量 */
23:    if ( semop( semid, &sb, 1 ) == -1 ) {
24:
25:        printf("semacq: semaphore failed.\n" );
26:        exit(-1);
27:
28:
29:}
30:
31:    printf("semacq: Semaphore acquired %d\n", semid );
32:
33:    }
34:
35:    return 0;
36::}
```

你首先在第22行使用 `semget` 标识信号量标识符。如果成功，你就可以构建信号量操作结构（由 `sembuf` 结构体标识）。该结构包含信号量编号、应用于信号量的操作以及一组操作标志。由于你只有一个信号量，因此使用数字零来标识它。要获取信号量，你指定操作为 -1。这会将信号量的值减 1，但前提是它的初始值大于零。如果信号量已经是零，则该操作（以及进程）将阻塞，直到信号量的值增加。

使用已创建的 `sembuf`（变量 `sb`），你使用 API 函数 `semop` 来获取信号量。你指定信号量标识符、你的 `sembuf` 结构以及传递的 `sembuf` 数量（在本例中为 1）。这意味着你可以提供一个 `sembuf` 数组，这将在本章稍后的部分进行介绍。当信号量操作完成（信号量值不为零），它将返回成功（一个非 -1 值）。这意味着执行 `semop` 的进程已获取了信号量。

现在是时候看一个释放示例了。此示例从释放信号量的角度演示了 `semop` API 函数（参见列表 17.3）。

> 在许多情况下，释放操作紧随同一个进程中的获取操作之后。这种用法允许两个进程之间进行同步。第一个进程尝试获取信号量，并在信号量不可用时阻塞。第二个进程知道另一个进程正阻塞在信号量上，于是释放它，允许该进程继续运行。这在进程之间提供了一种实用且高效的步进操作。

![](img/f7bd35eb87a62f74c6f23c07df847dff_327_0.png)

## 308 GNU/Linux 编程

列表 17.3 使用 semop 释放信号量（位于光盘 `./source/ch17/semrel.c`）

```c
1: #include <stdio.h>
2: #include <sys/sem.h>
3: #include <stdlib.h>
4: #include "common.h"
5: 
6: int main()
7: {
8:     int semid;
9:     struct sembuf sb;
10: 
11:     /* 获取 ID 为 MY_SEM_ID 的信号量 */
12:     semid = semget(MY_SEM_ID, 1, 0);
13: 
14:     if (semid >= 0) {
15: 
16:         printf("semrel: Releasing semaphore %d\n", semid);
17: 
18:         sb.sem_num = 0;
19:         sb.sem_op = 1;
20:         sb.sem_flg = 0;
21: 
22:         /* 释放信号量 */
23:         if (semop(semid, &sb, 1) == -1) {
24: 
25:             printf("semrel: semaphore failed.\n");
26:             exit(-1);
27: 
28:         }
29: 
30:         printf("semrel: Semaphore released %d\n", semid);
31: 
32:     }
33: 
34:     return 0;
35: }
```

在列表 17.3 的第 12 行，你首先使用 `semget` API 函数标识你感兴趣的信号量。获取信号量标识符后，你在第 23 行使用 `semop` API 函数通过构建的 `sembuf` 结构体来释放信号量。在这个示例中，你的 `sem_op` 元素为 1（对比列表 17.2 中的 -1）。在这个示例中，你正在释放信号量，这意味着你正在将其置为非零（从而使其可用）。

## 第 17 章 信号量同步 309

> 需要注意的是 `sembuf` 在列表 17.2 和 17.3 中使用的对称性。要获取信号量，你从其值中减 1。要释放信号量，你对其值加 1。当信号量的值为零时，不可用的，这迫使任何尝试获取它的进程阻塞。信号量的初始值设为 1 则将其定义为二值信号量。如果信号量的值大于零，则可以被视为计数信号量。

现在来看下目前为止讨论的每个函数的示例应用。列表 17.4 演示了列表 17.1 (`semcreate`)、列表 17.2 (`semacq`) 和列表 17.3 (`semrel`) 的执行情况。

## 列表 17.4 示例信号量应用的执行情况

| 行号 | 应用输出 |
| :--- | :--- |
| 1 | # semcreate: Created a semaphore |
| 2 | # semacq: Attempting to acquire |
| 3 | # semacq |
| 4 | # semacq: Semaphore acquired 0 |
