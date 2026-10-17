
传递给 `pthread_setspecific()` 的 `value` 参数通常指向一个由调用者之前分配的内存块。当线程终止时，此指针将作为该键析构函数的参数传递。

`value` 参数不需要指向内存块的指针。它可以是可以赋值（通过强制转换）给 `void` 的标量值。在这种情况下，较早的 `pthread_key_create()` 调用会将 `destructor` 指定为 `NULL`。

图 31-3 显示了用于存储值的数据结构的典型实现。在图中，我们假设 `pthread_keys[1]` 被分配给一个名为 `myfunc()` 的函数。对于每个线程，Pthreads API 维护一个指向线程特定数据块的指针数组。这些线程特定数组的每个元素与图 31-2 所示的全局 `pthread_keys` 数组有一一对应的对应关系。`pthread_setspecific()` 函数设置调用线程数组中对应于键的元素。

| Thread A | TSD buffer | |
|---|---|---|
| tsd[0] | pointer | for myfunc() |
| tsd[1] | pointer | in thread A |
| tsd[2] | pointer | |
| ... | ... | |
| Thread B | TSD buffer | | |
| tsd[0] | pointer | for myfunc() |
| tsd[1] | pointer | in thread B |
| tsd[2] | pointer | |
| ... | ... | |
| Thread C | TSD buffer | | |
| tsd[0] | pointer | for myfunc() |
| tsd[1] | pointer | in thread C |
| tsd[2] | pointer | |

**图 31-3:** 用于实现线程特定数据 (TSD) 的数据结构

### 31.3.4 采用线程特定数据 API

当我们在第 3.4 节首次描述 `strerror()` 时，我们注意到它可能返回指向静态分配字符串的指针。这意味着 `strerror()` 可能不是线程安全的。在接下来的几页中，我们将查看 `strerror()` 的线程安全实现，并展示如何使用线程特定数据使该函数变为线程安全。在许多 UNIX 实现（包括 Linux）中，标准库提供的 `strerror()` 函数是线程安全的。然而，我们仍然使用 `strerror()` 示例，是因为 SysV 不要求该函数是线程安全的，且它的实现提供了一个使用线程特定数据的简单示例。

这两个线程都显示了对应于 EPERM 的 `errno` 字符串，因为第二个线程（在 `threadFunc` 中）对 `strerror()` 的调用覆盖了主线程调用 `strerror()` 时写入的缓冲区。对输出的检查显示，两个线程中的局部变量 `str` 指向同一个内存地址。

# 列表 31-2：从两个不同的线程调用 strerror()

```c
#include <stdio.h>
#include <string.h>
#include <pthread.h>
#include <tlpi_hdr.h>
/* 获取 strerror() 的声明 */
static void *
threadFunc(void *arg)
{
    char *str;
    printf("Other thread about to call strerror()\n");
    str = strerror(EPERM);
    printf("Other thread: str (%p) = %s\n", str, str);
    return NULL;
}
int
main(int argc, char *argv[])
{
    pthread_t t;
    int s;
    char *str;
    str = strerror(EINVAL);
    printf("Main thread has called strerror()\n");
    s = pthread_create(&t, NULL, threadFunc, NULL);
    if (s != 0)
        errExitEN(s, "pthread_create");
    s = pthread_join(t, NULL);
    if (s != 0)
        errEXITEN(s, "pthread_join");
    printf("Main thread: str (%p) = %s\n", str, str);
    exit(EXIT_SUCCESS);
}
```

列表 31-3 显示了 `strerror()` 的重新实现，它使用线程特有数据来确保线程安全。

修改后的 `strerror()` 执行的第一步是调用 `pthread_once()` ① 以确保该函数的首次调用（无论来自哪个线程）都会调用 `createKey()` ②。`createKey()` 函数调用 `pthread_key_create()` 来分配一个线程特有的键 ③。`pthread_key_create()` ① 调用还记录了析构函数的地址 ②，该析构函数将用于释放与此键对应的线程特有缓冲区。

`strerror()` 函数调用 `pthread_get_specific()` 来获取该线程对应 `strerrorKey` 的唯一缓冲区地址。如果 `pthread_get_specific()` 返回 `NULL`，则表示第一次调用 `strerror()`，因此函数使用 `malloc()` 分配一个新缓冲区 ④，并使用 `pthread_get_specific()` 保存缓冲区地址 ⑦。如果 `pthread_get_specific()` 返回非空值，则该指针指向该线程之前调用 `strerror()` 时分配的现有缓冲区。

该 `strerror()` 实现的其余部分与我们展示的实现相似，区别在于 `buf` 是线程特有数据缓冲区的地址，而不是静态变量。

# 列表 31-3：使用线程特有数据的 strerror() 线程安全实现

```c
#define GNU_SOURCE /* 从 <stdio.h> 获取 'sys_errno' 和 '_sys_errlist'
声明 */
#include <stdio.h>
#include <string.h>
#include <pthread.h>
#include <tlpi_hdr.h> /* 获取 strerror() 的声明 */
static pthread_once_t once = PTHREAD_ONCE_INIT;
static pthread_key_t strerrorKey;
#define MAX_ERROR_LEN 256 /* strerror() 返回的每个线程
缓冲区中字符串的最大长度 */
static void
destructor(void *buf) /* 释放线程特有数据缓冲区 */
{
    free(buf);
}
static void
createKey(void) /* 一次性键创建函数 */
{
    int s;
    /* 分配唯一的线程特有数据键并保存
    线程特有数据缓冲区的析构函数地址 */
    s = pthread_key_create(&strerrorKey, destructor);
    if (s != 0)
        errExitEN(s, "pthread_key_create");
}
```

```c
char *
strerror(int err)
{
    int s;
    char *buf;
    /* 让第一个调用者为线程特有数据分配键 */
    s = pthread_once(&once, createKey);
    if (s != 0)
        errEXITEN(s, "thread_once");
    buf = pthread_getspecific(strerrorKey);
    if (buf == NULL) /* 如果是此线程的首次调用，
            为线程分配缓冲区并保存其位置 */
        buf = malloc(MAX_ERROR_LEN);
        if (buf == NULL)
            errEXIT("malloc");
    s = pthread_setspecific(strerrorKey, buf);
    if (s != 0)
        errEXITEN(s, "thread_setspecific");
```
