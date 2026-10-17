
```c
struct thread_params {
  int count;
};

void thread_fn(void *);

void displays(const char *);

int main(void) {
    pthread_t tid1, tid2;
    struct thread_params params1, params2;
    int rval;

    params1.count = 1;
    params2.count = 2;

    rval = pthread_create(&tid1, NULL, thread_fn, &params1);
    if (rval != 0) {
        printf("Thread creation failed.\n");
        exit(1);
    }

    rval = pthread_create(&tid2, NULL, thread_fn, &params2);
    if (rval != 0) {
        printf("Thread creation failed.\n");
        exit(1);
    }

    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);
}

void thread_fn(void *arg)
{
    struct thread_params *p = (struct thread_params *)arg;
    pthread_t tid;
    pid_t pid;
    tid = pthread_self();
    pid = getpid();
    printf("Thread %d: pid %u tid %u\n", p->count, (unsigned int) pid, (unsigned int) tid);
}

void displays(const char *s)
{
    pthread_t tid;
    pid_t pid;
    tid = pthread_self();
    pid = getpid();
    printf("%s %u %u\n", s, (unsigned int) pid, (unsigned int) tid);
}
```

```bash
$ gcc -w thread_ids.c -o ids -lpthread
$ ids
Parent/Main thread: pid 10249 tid 30978638
Thread 1: pid 10249 tid 301419968
Thread 2: pid 10249 tid 301200
```

## 练习 16.19

在你的系统上复制上述会话并运行足够多次以看到不同的线程输出。

### 16.6.4 线程属性

属性决定线程的行为。当 `pthread_create()` 的第二个参数设置为空指针时，线程以默认属性创建。以下是线程属性：

- `detachstate`：分离状态
- `stackaddr`：栈的低地址
- `stacksize`：栈的大小
- `guardsize`：保护缓冲区的大小

保护缓冲区对栈溢出提供保护。

你可以使用 `pthread_attr_t` 结构体来存储属性并与创建的线程关联。你可以使用 `pthread_attr_init()` 将其初始化为默认属性。可以使用其他函数更改存储在 `pthread_attr_t` 中的属性。例如，你可以使用 `pthread_attr_setdetachstate()` 将分离状态设置为 `PTHREAD_DETACHED` 创建分离线程，或设置为 `PTHREAD_JOINABLE` 创建连接线程。

你可以使用 `pthread_attr_destroy()` 将 `pthread_attr_t` 中的属性设置为无效值。如果 `pthread_attr_t` 是动态分配的，调用该函数将释放空间。总结来说，可以通过以下步骤创建自定义属性的线程：

1. 创建一个 `pthread_attr_t` 对象
2. 使用 `pthread_attr_init()` 将 `pthread_attr_t` 初始化为默认属性
3. 使用相关函数将属性修改为所需值
4. 将属性指针传递给 `pthread_create()` 以创建带有属性的线程
5. 通过 `pthread_attr_destroy()` 释放属性对象

以下是这些步骤的代码结构：

```c
...
int retval;
thread_t tid;
pthread_attr_t attr;

retval = pthread_attr_init(&attr);
if (retval != 0)
    return(retval);

retval = pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);
if (retval == 0)
    retval = pthread_create(&tid, &attr, thread_fn, arg);

pthread_attr_destroy(&attr);
...
```

## 练习 16.20

编写创建一个分离线程并显示其 `PID` 和 `TID` 的程序。

### 16.6.5 线程特定数据

由于线程共享进程的地址空间，它们共享访问数据区域。这意味着对数据项的更改对其他线程是可见的。有时，你希望每个线程中的

一个进程拥有其数据项（如变量）的副本的过程。你可以将变量的副本存储在线程特定的数据区域。对该变量的修改对其他线程不可见。

你可以根据需要创建许多线程特定的数据项，每个项的类型为 `void*`。每个项都通过你使用 `pthread_key_create()` 创建的键来引用。该函数的第一个参数是一个指向 `pthread_key_t` 类型的指针，第二个参数是一个清理函数。当每个线程终止时，会自动调用清理函数来释放线程特定的数据项。即使线程在执行过程中被取消，该函数也会被调用。清理函数被用于防止内存泄漏。如果你不需要清理函数，可以将第二个参数设置为 `NULL`。

一旦线程创建了键，它就可以使用 `pthread_setspecific()` 将线程特定值设置到该键。函数的第一个参数是键，第二个参数是待存储的 `void*` 类型的线程特定值，如下代码段所示。

```c
pthread_key_t thread_key;
...
void *thread_fn(void *args)
{
...
int *thread_item;
...
pthread_setspecific(thread_key, thread_item);
...
}
```

你可以使用 `pthread_getspecific()` 函数访问线程特定数据项，该函数仅以键作为参数，并返回与键关联的数据项。由于线程特定值存储为 `void*`，你必须将它们强制转换为所需的类型，如下：

```c
int fd;
fd = (int)pthread_getspecific(thread_key);
...
```
