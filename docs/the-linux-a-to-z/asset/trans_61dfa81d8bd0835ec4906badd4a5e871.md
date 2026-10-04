
![](img/ad36c2db45661d7b3b68db09c8eea0a1_443_0.png)

### 图 29.3 上下文切换前线程栈布局。

从将要运行的下一个线程的 struct context 的 ebp 字段中恢复，然后 switch_context() 函数返回。

最终，CPU 将执行调度循环中的每个线程，直到其下一次 release() 调用，这样我们跟踪的线程就轮到再次运行了。当这种情况发生时，调度循环中位于我们前面的线程将执行一次 release() 调用，并且在 switch_context() 函数的汇编代码部分运行完毕时，CPU 的 ebp 寄存器将被重新加载为我们线程保存的 ebp 寄存器值。然而请注意，堆栈指针仍将指向前一个线程的堆栈，并且程序计数器将指向 switch_context() 函数末尾的指令，即将执行它们。

每个函数结束时发生的事情是堆栈指针被设为 ebp 中的值，以丢弃任何局部变量。在本例中，switch_context() 函数没有局部变量，但该赋值仍然执行。这具有有益的副作用，即移动堆栈指针，使其指向我们线程堆栈中的正确位置。函数结束时发生的其他操作是从当前堆栈（我们线程的堆栈）弹出 ebp 寄存器，然后使用堆栈上的返回地址返回到调用函数。

这意味着我们的线程代码通过从 release() 函数的普通返回来恢复执行。事实上，就线程而言，它们只是间隔调用 release()，然后返回，允许它们继续。线程本身并不知道 release() 调用期间发生了任何异常情况。

## 29.5 启动新线程

启动一个新线程只是为线程创建一个 struct context 并为其堆栈分配一块内存。然后这些数据结构可以被初始化并添加到调度循环中以获得运行机会。说起来很快听起来很简单，但实际上有点棘手，需要注意细节。棘手的部分是初始化线程的堆栈，因为在可以使用之前需要在空堆栈中手工制作几个值：

```
new_thread(int (*start_addr)(void), int stack_size)
{
    struct context *ptr;
    int esp;

    /* 1 */
    if (!(ptr = (struct context *)malloc(sizeof(struct context))))
        return 0;

    /* 2 */
    if (!(ptr->stack = (char *)malloc(stack_size)))
        return 0;

    /* 3 */
    esp = (int)(ptr->stack+(stack_size-4));
    *(int *)esp = (int)exit_thread;
    *(int *)(esp-4) = (int)start_addr;
    *(int *)(esp-8) = esp-4;
    ptr->ebp = esp-8;

    /* 4 */
    if (thread_count++)
    {
        /* 5 */
        ptr->next = current->next;
        ptr->prev = current;
        current->next->prev = ptr;
        current->next = ptr;
    }
    else
    {
        /* 6 */
        current = ptr->next = ptr->prev = ptr;
        switch_context(&main_thread, current);
    }

    return 1;
}
```

new_thread() 函数接受两个参数，第一个是线程执行将开始的函数的地址，第二个是为新线程的堆栈空间分配的内存块的大小（以字节为单位）。代码中的编号注释如下：

- 1. 使用 malloc() 为此线程创建一个 struct context。检查内存分配是否成功，并在出错时返回零值。
- 2. 再次使用 malloc() 为线程的堆栈分配指定大小的一块内存。新的 struct context 中的堆栈指针被设置为指向堆栈内存。同样，内存分配错误将导致 new_thread() 返回零。
- 3. 将堆栈初始化为图 29.4 所示的状态。请记住，struct context 中的堆栈内存指针指向块的最低编号地址，而堆栈上的操作发生在块的高地址端。
- 4. 下一部分取决于这是否是当前进程中的第一个新线程。如果是，则主程序的执行将被挂起并执行到新线程的上下文切换；否则新线程只是添加到调度循环中等待其运行的机会。
- 5. 将新线程添加到现有调度器循环会变得稍微复杂一些，因为循环是双向链接的，因此需要设置向前和向后的指针集。新线程被插入到调度循环中，使得当当前线程执行 release() 时，它将自动成为下一个要运行的线程。
- 6. 这里，目前没有线程在运行，因此调度循环需要通过对 switch_context() 的第一次调用来创建和启动。为了确保主程序被挂起，switch_context() 调用将其 ebp 寄存器内容存储在名为 main_thread 的静态 struct context 中。该结构不是调度循环的一部分，因此当没有更多线程可运行时，主程序不会再次执行，除非有特殊安排。

图 29.4 显示，与新线程关联的 struct context 的 ebp 元素被设置为指向线程的堆栈。当对新线程进行上下文切换时，此值被加载到 CPU ebp 寄存器中。随后从 switch_context() 函数返回会导致堆栈指针指向同一堆栈位置。执行一次将 ebp 弹出到堆栈的操作会适当地加载此寄存器，并使堆栈指针指向线程启动函数。最后，执行从子程序返回操作会将启动地址弹出到程序计数器中，从而执行到线程启动函数的开头跳转。

当线程的启动函数终止时需要一个额外的变化，以便将线程从调度循环中移除并将其 malloc() 的内存释放回系统。这些操作由 exit_thread() 函数执行。为了避免需要在每个线程的启动函数末尾记住调用此函数，线程的堆栈中会自动制作对该函数的跳转。这意味着当线程的启动函数终止时，该函数会自动执行，使用与第一次执行启动函数时相同的技巧。

exit_thread() 函数的代码如下：

```
static exit_thread(void)
{
    struct context dump, *ptr;

    /* 1 */
    if (--thread_count)
    {
        /* 2 */
        ptr = current;
        current->prev->next = current->next;
        current->next->prev = current->prev;
        current = current->next;
        free(ptr->stack);
        free(ptr);
        switch_context(&dump, current);
    }
    else
    {
        /* 3 */
        free(current->stack);
        free(current);
        switch_context(&dump, &main_thread);
    }
```

exit_thread() 函数终止由 current 指向的线程。exit_thread() 函数被声明为 static 的事实阻止它从库外部被调用。编号注释如下：

- 1. 如果 current 不是调度循环中的最后一个线程，则将其从调度器中取消链接并切换上下文到下一个线程；否则，由于没有更多线程可执行，恢复主线程的执行。
- 2. 复制当前线程指针的副本。将当前线程从调度循环中取消链接，然后重新分配 current 以指向下一个要执行的线程。现在 free() 与终止线程关联的 malloc() 的内存，最后从此线程 switch_context() 到新的 current 线程。
- 3. 这里，只需要 free() 调度循环中最后一个线程关联的 malloc() 的内存，然后 switch_context() 回到主程序，以恢复其执行。

## 29.6 汇合

在汇合机制的实现中使用了两种新的数据结构。第一个（struct channel）按消息通道提供。第二个（struct message）用于按被阻塞消息提供。这两个结构，连同 struct context 的声明和一些全局变量等，都提供在名为 def.h 的单独头文件中，应在程序顶部 #include。该程序的 def.h 的完整内容如下：

```
#include <string.h>

struct context                 /* One structure for each thread */
{
    int ebp;                    /* Base pointer (stack frame pointer) store */
    char *stack;                /* Pointer to memory block for thread stack */
    struct context *next;       /* Round robin circular list pointer */
    struct context *prev;       /* Round robin circular list pointer */
};

struct channel                 /* One structure for each communication channel */
{
    int number;                 /* Channel number */
    int sr_flag;    /* 0=no queue, 1=send queued, 2=receive queued */
    struct channel *link;       /* Link to next channel in list */
    struct message *message_list;   /* Head of message queue */
```

![](img/ad36c2db45661d7b3b68db09c8eea0a1_446_0.png)

### 图 29.4 新线程中设置的数据结构。

start function, a jump to the function is automatically crafted into the thread's stack. This means that the function is automatically executed when the thread's start function terminates, using a similar trick to the one which executed the start function in the first place.
