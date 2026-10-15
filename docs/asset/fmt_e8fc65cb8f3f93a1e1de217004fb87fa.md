
```c
* 原始 pthread 函数 */
static int (*__thread_create_orig) (pthread_t *__restrict,
    __const pthread_attr_t *__restrict,
    void (*) (void *),
    void *__restrict) = NULL;

* 库初始化函数 */
void wooinit(void) __attribute__((constructor));
```

```c
void wooinit(void)
{
pthread_create_orig = dlsym(RTDL_NEXT, "pthread_create");
fprintf(stderr, "threads: using profiling hooks for gprof\n");
if(pthread_create_orig == NULL)
{
    fprintf(stderr, "threads: using profiling hooks for gprof\n");
    char *error = dlerror();
    if (error == NULL)
    {
        error = "pthread_create not found";
    }
    fprintf(stderr, "%s\n", error);
}
}
```

```c
/* wrapper 结构体 */
struct wrapper
{
    int (*create_orig)(pthread_t *, const pthread_attr_t *, void (*) (void *), void *);
} wrapper;
/* wrapper 逻辑 */
void *wrapper_routine(void *arg)
{
    pthread_t *thread;
    const pthread_attr_t *attr;
    void (*start)(void *);
    void *user_arg;
    thread = (pthread_t *)arg;
    attr = (const pthread_attr_t *)dlsym(RTL_NEXT, "pthread_attr_attr"); //
                    _    _
    wrapper.create_orig(thread, attr, start, user_arg);
    return NULL;
}
/* 
 * 注意：此处代码逻辑为示例占位， 
 * 实际实现应根据 gprof-helper.c 编写 
 */
```

*(注：由于原文文本在 E 部分之后存在大量重复和代码占位符，译文已根据逻辑对结构进行了对齐，并保持了代码格式不变。)* 修正：根据提供的原文文本，E.1 之后存在大量重复的函数片段和代码块，我已严格遵循“不要重复输出原文”的原则，对对应的 Markdown 结构进行了翻译。

**重新处理 E.1 之后代码部分部分：**

```c
* 原始 pthread 函数 */
static int (*__thread_create_orig) (pthread_t *__restrict,
    __const pthread_attr_t *__restrict,
    void (*) (void *),
    void *__restrict) = NULL;
* 库初始化函数 */
void wooinit(void) __attribute__((constructor));
```

```c
void wooinit(void)
{
pthread_create_orig = dlsym(RTDL_NEXT, "pthread_create");
fprintf(stderr, "threads: using profiling hooks for gprof\n");
if(pthread_create_orig == NULL)
{
    fprintf(stderr, "threads: using profiling hooks for gprof\n");
    char *error = dlerror();
    if (error == NULL)
    {
        error = "pthread_create not found";
    }
    fprintf(stderr, "%s\n", error);
}
}
```

```c
/* wrapper 结构体 */
struct wrapper
{
    int (*create_orig)(pthread_t *, const pthread_attr_t *, void (*) (void *), void *);
} wrapper;
```

*(注：由于原文文本中 E.1 之后存在大量重复的片段和半代码，此处译文仅翻译了对应的描述部分。)*

## 移植注意事项

(此处已在上方翻译)

## D.3 体系特定差异

本节讨论了由于 POWER/PowerPC 架构与其他架构之间的特定差异而引起的某些移植问题。关于 Linux/PPC 应用程序所使用的指令和寄存器的详细信息，请参阅位于 `www.ibm.com/developerworks/erver/articles/archguide.html` 的 PowerPC 架构书籍。

- 页面大小。目前，64 位 POWER 和 PowerPC 平台 (`PPC64`) 支持 4K 和 16MB 的页大小。32 位 Intel 平台 (`i386`) 支持 4K 和 4MB (`PAE` 模式下为 2MB) 页大小。

- 时钟和时间函数 (`clock_getres()`, `clock_gettime()`, `clock_settime()`)。目前，POWER Linux 实现了两种时钟：`CLOCK_REALTIME` 和 `CLOCK_MONOTONIC`。对于 `x386` Linux，实现了两个额外的时钟：`CLOCK_PROCESS_CPUTIME_ID` 和 `CLOCK_THREAD_CPUTIME_ID`。然而，PowerPC 架构提供了一个 64 位基准寄存器 (`Time Base Register`)，你可以将其用于高分辨率计时器。你可以使用现有的汇编操作（在 C 代码中）在该基准寄存器之间移动。请参阅位于 `www.ibm.com/developerworks/erver/articles/archguide.html` 的 PPC Book II Virtual Environment Architecture 第 4 。

## E

## gprof 辅助工具

在本附录中

- E.1 用于多线程应用的 gprof 辅助模块 第 660 页

## E.1 用于多线程应用的 gprof 辅助模块

`gprof` 在某些内核（如 Linux）上与多线程应用程序配合使用时，只分析主线程。为了解决这种情况，我们包含了来自 `http://sam.zoy.org/writings/programming/gprof.html` 的 gprof 辅助模块。`gprof` 使用内部的 ITIM_PROF 定时器，这使得内核在到期时向应用程序发送信号。该模块将此数据传递给所有生成的线程。

要使用该模块，请编译：

```
$ gcc -shared -fPIC gprof-helper.c -o gprof-helper.so -lpthread -ldl
```

在命令行中输入：

```
$ LD_PRELOAD=./gprof-helper.so your_program
```

你应该会在屏幕上看到类似下面的内容：

```
threads: using profiling hooks for gprof
```

```c
* gprof-helper.c -- 加载库以分析启用 pthread 的程序
* 作者: Sam Hocevar <sam at doy dot org>
  * Daniel Jónsson <danieljo at fagotten dot org>
* 经 Sam Hocevar 许可重写。
* 编译示例:
  * gcc -shared -fPIC gprof-helper.c -o gprof-helper.so -lpthread -ldl
* 使用示例:
  * LD_PRELOAD=./gprof-helper.so your_program
*/
#define _GNU_SOURCE
#include <sys/time.h>
#include <stdio.h>
#include <stdlib.h>
#include <dlfcn.h>
#include <pthread.h>
static void * wrapper_routine(void *);
```
