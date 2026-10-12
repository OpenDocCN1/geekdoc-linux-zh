
如果归约操作具有结合律，计算仍然可以并行化，不是使用 map 模式，而是通过二叉树形并行化（树形折）。例如，为了求和 8 个数字，我们可以并行执行 4 次配对和，然后通过两次并行操作对这 4 个结果，最后计算最终和。

```
1+2+3+4+5+6+7+8
= 3+7+11+15
= 10+26
= 36
```

另一个例子是归并排序，其中待排序的列表被分成与线程数量相等的块，每个块并行排序，然后配对合并这些块。与其

# 基于树莓派的 Linux 操作系统基础

顺序合并排序的复杂度为 `O(N log N)`，如果线程数至少是排序元素的一半，那么排序可以在 `O(log N)` 内完成。

通常情况下，对于大小为 `N` 的数据集，在无限并行的情况下，结合性操作可以减少到 `O(log N)` 步。

## 7.5.2 任务并行编程

与其通过对数据的不同部分执行相同的操作来并行化计算，不如并行地执行不同的计算。例如，我们可以将用于边缘检测的 Sobel 滤波器分为垂直和水平部分，并在图像数据上执行这些操作。在实践中，如果输入数据是流（例如视频帧），这种方法尤特别有效，因为在这种情况下，我们可以创建一个流水线，在不同的帧上并行执行不同的操作。图 7.7 显示了 Sobel 边缘检测流水线的完整任务图 [13]。在这个示例中，如果一个节点的扇出大于1，则帧的副本会被发送到每个下游节点。通常情况下，节点当然可以向它的每个下游节点发送不同的数据。

![](img/17ca5177da1b1e15b2169f9c7932e5b6_211_0.png)

图 7.7：Sobel 边缘检测流水线的任务图。

## 7.6 实用型并行编程框架

### 7.6.1 POSIX 线程 (threads)

我们已经在第 7.3.6 节介绍了 POSIX 同步原语，但我们没有讨论创建和管理线程的 API。POSIX 线程 `threads` API 提供了管理线程和控制其属性的数据类型和 API 调用。可以在 `threads(7)` 中找到一个良好的概述。线程由不透明类型 `pthread_t` 表示，该类型表示线程 ID（即一个较小的整数）。每个线程都有若干属性，通过不透明类型 `pthread_attr_t` 管理，该类型通过一组的 API 调用进行访问。

最重要的线程管理调用是 `pthread_create()`、`pthread_join()` 和 `pthread_exit()`。`pthread_create()` 调用接受一个指向要在线程中调用的子程序的指针以及其参数的指针。在线程内部，可以调用 `pthread_exit()` 来终止调用线程。`pthread_join()` 调用等待第一个参数所指示的线程终止，如果该线程处于可连接状态（见下文）。如果该线程 `pthread_exit()` 带有非空参数退出，则该参数将作为第二个参数在 `pthread_join()` 中可用。

# 第 7 章 | 并发与并行

```c
### 列表 7.6.1 POSIX 线程 API：创建和连接
```c

#include <pthread.h>

int pthread_create(

    pthread_t *thread, const pthread_attr_t *attr,

    void (*start_routine)(void*), void *arg);

int pthread_join(pthread_t thread, void **value_ptr);

// 线程内部

    int pthread_exit(void *retval)

```
```

另一个方便的调用是 `pthread_self()`，它简单地返回调用者的线程 ID：

```
### 列表 7.6.2 POSIX 线程 API：自身
```c

thread_t pthread_self(void);

```

```

在很多情况下，没有必要指定线程属性，但我们可以使用属性来控制处理器亲和性或线程的分离状态，即线程是可连接的还是分离的。分离意味着你知道不会使用 `pthread_join()` 来等待它，因此在退出时线程的资源会被立即释放。

使用以下调用创建和销毁属性：

```
### 列表 7.6.3 POSIX 线程 API：初始化和销毁
```c

int pthread_attr_init(pthread_attr_t *attr);

int pthread_attr_destroy(pthread_attr_t *attr);

```
```

例如，为了设置或获取亲和性，我们可以使用以下调用：

```
### 列表 7.6.4 POSIX 线程 API：亲和性
```c

#define GNU_SOURCE

int pthread_attr_setaffinity_np(pthread_attr_t *attr,

    size_t cpusetize, cpu_set_t *cpuset);

int pthread_attr_getaffinity_np(pthread_attr_t *attr,

    size_t *cpusetize, cpu_set_t *cpuset);

```
```

同样，如果我们想设置或获取分离状态，可以使用：

```
### 列表 7.6.5 POSIX 线程 API：属性
```c

int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);

int pthread_attr_getdetachstate(const pthread_attr_t *attr, int *detachstate);

```
```

基于树莓派的 Linux 操作系统基础

还有许多用于管理线程和属性的 API 调用，更多细节请参见 man页 `threads(7)`。

下面是一个使用线程的典型用例示例，用于创建若干相同的工作线程来并行执行工作。

# 列表 7.6.6：POSIX 线程 API 示例

```c
#include <pthread.h>
/* 用作 thread_start() 的参数 */
struct thread_info {
    pthread_t thread_id; /* 由 pthread_create() 返回的 ID */
    // 你可能需要的任何其他字段
};

/* 这是工作线程 */
void thread_start(void *vinfo) {
    // 执行工作
    pthread_exit(NULL);
}

int main(int argc, char *argv[]) {
    int st;
    struct thread_info *tinfo;
    unsigned int num_threads = 5;

    // 分配内存
    tinfo = calloc(num_threads, sizeof(struct thread_info));

    // 创建线程
    for (unsigned int i = 0; i < num_threads; i++) {
        if (pthread_create(&tinfo[i].thread_id, NULL, thread_start, vinfo) != 0) {
            perror("pthread_create");
        }
    }

    // 连接线程
    for (unsigned int i = 0; i < num_threads; i++) {
        if (pthread_join(tinfo[i].thread_id, NULL) != 0) {
            perror("pthread_join");
        }
    }

    // 清理
    free(tinfo);
    return 0;
}
```

在这个程序中，我们通过在 for 循环中调用 `pthread_create()` 创建了 `num_threads`（第 28 行）。每个线程都带有一个 `struct thread_info`，它包含了该线程的参数。

# 第 7 章 | 并发与并行

每个线程接收一个函数指针 `&thread_start`。`thread_info` 结构体可以包含指向大型数组的指针，每个线程处理部分数据。由于这些线程是可连接的（这是默认值），我们通过在循环中调用 `join()` 来等待（第 37 行）。因为线程在共享内存上工作，并行执行的结果将在主程序中可用。

## 7.6.2 OpenMP

OpenMP 是共享内存并行编程的事实标准。它基于一组编译器指令（pragma），结合 API 来指定区域、数据范围、同步等。OpenMP 是一种可移植的并行编程，支持 C、C++ 和 Fortran。它历史上一直用于数据并行。从 3.0 版本开始，OpenMP 也支持任务并行 [14]。它广泛应用于任务和数据并行场景。由于 OpenMP 是一种语言增强，每个新构造都需要编译的支持。因此，它的功能不如基于库的模型。
