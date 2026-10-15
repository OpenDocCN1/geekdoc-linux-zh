
图 23.4 使用可移植参数传递的线程 TCP 服务器。

## 线程安全函数

Posix.1 要求所有 Posix.1 定义以及 ANSI C 标准定义的函数必须是线程安全的，图 23.5 中列出的异常除外。

遗憾的是 Posix.1 对于工作 API 函数的安全性没有发表任何说明。表中的最后五行来自 Unix 98。我们在第 11.14 节提到过非重入函数 `gethostbyname` 和 `gethostbyaddr`。我们提到尽管厂商定义了线程安全的...

## 线程特定数据

| 不需要线程安全 | 必须线程安全 | 注释 |
|---|---|---|
| asctime | asctime_r | |
| ctime | ctermid_r, ctime_r | 仅在非空参数时安全 |
| getc_unlocked | getgrid_r | |
| getchar_unlocked | getgrnam_r | | |
| getgrid | getlogin_r | |
| getgrnam | getpnam_r | | |
| getlogin | getpwuid_r | |
| getpnam | gntime_r | |
| getpwuid | localtime_r | | |
| gntime | | |
| localtime | | |
| put_unlocked | | |
| putchar_unlocked | rand_r | 仅在非空参数时安全 |
| rand | readdir_r | |
| readdir | strtok_r | |
| strtok | tnname | |
| gethostXXX | | |
| getXXX | | |
| getprotoXXX | | |
| getXXX | | |
| inet_ | | |

23.5 线程安全函数。

图 23.5 线程安全函数。

线程特定数据是使现有函数变为线程安全的常用技术。在描述与线程特定数据工作的 Pthread 函数之前，我们先描述该概念和一种可能的实现方式，因为这些函数看起来比实际要复杂得多。

### 线程特定数据

作者看过的所有书籍中，复杂之处之一在于，它们对线程特定数据的描述读起来像 Pthreads 标准，谈论的是键值对，且键是不透明对象。我们通过索引和指针来描述线程特定数据，因为常见的实现使用一个单独整数作为键，而与索引关联的值是指向线程所分配的内存区域的指针。

每个系统都提供数量有限的线程特定数据项。Posix.1 要求此限制不少于 128 个（每个进程），我们假设后续系统中该限制为每个进程维护一个数组结构，我们将其称为 Key 结构，如图 23.7 所示。

| flag | |
|---|---|
| Key[0] | 析构函数指针 |
| Key[1] | 析构函数指针 |
| Key[127] | 析构函数指针 |

图 23.7 线程特定数据的可能实现方式。

`Key` 结构中的 `flag` 表明该数组元素当前是否在使用，所有 `flag` 均初始化为“未使用”。当线程调用 `pthread_create` 创建一个新的线程特定数据项时，系统会在其 `Key` 结构数组中搜索并找到第一个未使用的。它的索引（0 到 127）称为键（key），该索引将返回给调用线程。我们稍后会讨论 `Key` 结构中的另一个成员“析构函数指针”。

除了进程级的 `Key` 结构数组外，系统还维护了关于进程中每个线程的大量信息。我们将其此称为 `Pthread` 结构，其中部分信息是一个 128 元素的指针数组，我们称之为 `pkey` 数组。如图 23.8 所示。

| thread 0 | thread n | |
|---|---|---|
| Pthread() | Pthread() | |
| 其他线程信息 | 其他线程信息 | |
| pkey[0] | 指针 NULL | pkey[0] | 指针 NULL |
| pkey[1] | 指针 NULL | pkey[1] | 指针 NULL |
| ... | ... | |
| pkey[127] | 指针 NULL | pkey[127] | 指针 NULL | 线程特定数据项 |

23.8 系统维护的关于每个线程的信息。

`pkey` 数组中的所有条目都初始化为空指针。这 128 个指针是与进程中每个可能的 128 个“键”之一关联的“值”。

当我们使用 `pthread_key_create` 创建键时，系统会告知我们键（索引）。然后每个线程都可以为该键存储一个值（指针），每个线程通常通过调用 `malloc` 获取该指针。线程特定数据的混淆之处在于，指针位于键值对中，而真正的线程特定数据是该指针指向的内容。

我们现在通过一个示例展示线程特定数据的用法，假设我们的 `readline` 函数使用线程特定数据在连续调用中维护每个线程的状态。稍后我们将展示此此修改的 `readline` 代码。

1. 创建一个进程和多个线程。
2. 其中一个线程继续调用 `readline` 并转调用 `pthread_key_create`。系统找到图 23.7 中第一个未使用的 `pkey` 结构并返回其索引（0–127）。我们假设此例索引为 1。
3. 我们将使用 `pthread_once` 函数确保 `pthread_key_create` 只由第一个调用 `readline` 的线程调用。
4. `readline` 调用 `pthread_getspecific` 获取 `pkey[1]` 值（图 23.8 中的“指针”），返回的值是一个空指针。`readline` 调用 `malloc` 分配其跨连续调用保持信息所需的内存。该线程初始化内存并调用 `pthread_setspecific` 将键（`pkey[1]`）指向其刚刚分配的内存。我们在图 23.9 中展示这一点，假设调用线程是 0。
5. 另一个线程 n 调用 `readline`，此时线程 0 可能仍在执行 `readline`。
6. `readline` 调用 `pthread_getspecific` 获取该线程的 `pkey[1]` 指针，返回空指针。该线程随后调用 `malloc` 然后调用 `pthread_setspecific`，就像线程 0 一样初始化该键的线程特定数据（1）。我们在图 23.10 中展示这一点。
7. 线程 n 继续执行 `readline`，使用并修改自己的线程特定数据。

图中注意 `pthread` 结构由系统（可能通过线程）维护，但实际的线程特定数据由我们的函数（在本例中为 `readline`）维护。`pthread_setspecific` 所做的仅仅是将 `pthread` 结构中的键指向我们分配的内存。同样，`pthread_getspecific` 向我们返回该指针。

![](img/aeda3be9318bed42850d461da0f28_614_0.png)

第 23.5 节 线程特定数据

跨连续调用的线程特定数据键是...

图 23.9 与线程特定数据关联。

![](img/aeda3be9318bed42850d461da0f28_615_0.png)

图 23.10 线程特定数据的指针。

![](img/aeda3be9318bed42850d461da0f28_615_1.png)

我们未解决的一个问题是：线程终止时发生了什么？线程特定数据由我们的函数（在本例中为 `readline`）维护。`pthread_setspecific` 所做的仅仅是将 `pthread` 结构中的键指向我们分配的内存。同样，`pthread_getspecific` 向我们返回该指针。

`pthread_getspecific` 和 `pthread_setspecific` 函数用于获取和存储与键关联的值。这就是我们在图 23.8 中称说的“指针”。该指针指向

```c
#include <pthread.h>

void *pthread_getspecific(pthread_key_t key) {
    返回：指向线程特定数据的指针（可能为空指针）
}

int pthread_setspecific(pthread_key_t key, const void *value) {
    返回：如果成功返回 0，错误返回正 XXX 值
}
```

`pthread_once` 函数用于确保 `pthread_key_create` 只由第一个调用 `readline` 的线程调用。

```c
pthread_key_t rl1_key;

pthread_once_t rl1_once = PTHREAD_ONCE_INIT;

void readline_destructor(void *ptr) {
    free(ptr);
}

void readline_once(void) {
    pthread_key_create(&rl1_key, readline_destructor);
}

ssize_t readline( ... )
```
