
## 6.3 用户进程从创建到退出的完整过程

### 6.3.1 进程创建与页面映射

```c
void do_no_page(unsigned long error_code, unsigned long address)
{
    while (i-- > 0) {
        tmp--;
        (char *)tmp = 0;
    }
    if (put_page(page, address)) // mapping to str1's linear space
        return;
    }
    free_page(page);
    oom();
}
```

映射过程如图 6.16 所示；请注意在此过程中设置了页目录项。只有在映射之后，进程才能执行加载的代码。**str 程序开始推栈。** 一旦程序开始执行，推栈操作便开始。

![](img/f661d64b7eb54840fcb4d65765a4e933_337_0.png)

图 6.16 将 str1 的物理地址映射到其线性地址。

这是因为条件 `tmp > current->end_data` 在某个时刻变真了。程序正在执行一个超过了进程 `end_data` 的线性地址。因此，调用了 `get_empty_page()` 函数，且没有额外数据被加载到进程时间。推栈也会触发缺页异常，这与外设无关。

进入 `get_empty_page()` 后，所需的页面将被分配并映射到进程 `str1` 的线性地址上。代码如下：

```c
// path:memory.c:
void get_empty_page(unsigned long address) {
    unsigned long tmp;
    if (!tmp->get_free_page() || !put_page(tmp, address)) {
        // 分配页面并
        // 映射到 str1 的线性
        // 地址空间
        free_page(tmp);
        /* 0 是被忽略的 */
        oom(t);
    }
}
```

**进程 str1 继续运行，推入栈并触发缺页异常。** 进程继续运行，并重复这一过程：“推入栈 → 如果页表项的 P-位为 0 则触发缺页异常 → 分配物理内存 → 推入栈……”。当函数被调用第 n 次时，进程栈与物理内存之间的映射关系如图 6.18 所示。请注意栈数据的页面变化。

**在 str1 完成后清理栈。** 程序执行完成后，函数的递归到达了 `if (n == 0) return 0`。此时，函数的返回将导致栈的清理。ESP（栈指针）向高地址方向收缩，用户进程的空间实际上减少了。因此，栈中映射到线性空间的物理页应该被释放。然而，在我们对 Linux 0.11 源码的分析和测试中，实际上并没有执行这一过程。其原因如下：当进程运行时，内核并不在工作，进程在处理过程中丢弃的页面无法被内核及时检测。此外，CPU 中没有设计用于这种任务的电路；没有用于检测丢弃页面的机制。即使由内核实现了该函数，也没有机会去执行这样的函数。因此，页面在清理栈后没有被释放。

结果如图 6.19 所示。

### 6.3.2 进程 str1 的退出

在这里，我们启动进程 str1 的执行，包括如何释放其内存空间的操作过程、如何处理其 `task_struct` 占用空间等。事实上，str1 进程和 shell 进程的执行通常是相同的，都是通过调用 `exit()` 函数来实现的。父进程负责释放 `task_struct` 所在的页面。现在我们来看具体的过程。

![图 6.18 str1 推栈的修复。
![图 6.18（续）str1 推栈的修复。
![图 6.19 进程 str1 完成后清理栈。

**str1 进程准备好退出了。** str1 进程调用 `exit()` 函数退出，最终映射到 `sys_exit()` 函数并执行，同时调用 `do_exit()` 函数来处理 str1 进程退出的相关事务。

具体代码如下：

```c
// code path:kernel/exit.c:
int sys_exit(int error_code)
{
    return do_exit(error_code & 0xff) << 8;
}
```

与进程退出的内容包含两个方面，包括：首先，释放 str1 进程代码和数据占用的物理内存并移除与 str1 的关系。而 str1 进程是自负责释放被 str1 进程管理结构 `task` 占用的物理内存，并撤销其与 `task[64]` 的关系。这是由父进程完成的。

**释放 str1 进程占用的页面。** 系统使用 `free_page_tables()` 函数来释放 str1 程序占用的页面，包括已清理但未释放的页面，释放管理这些页面的页面和页目录。这些页面仍然保留在 str1 进程的垃圾数据中，但映射关系已被释放。进程 str1 将无法再次找到这些页面。代码如下：

```c
// code path:kernel/exit.c:
int do_exit(long code)
{
    int i;
    free_page_tables(get_base(current->ldt[1]), get_limit(0x0ff)); // 释放 str1 段占用的页面
    free_page_tables(get_base(current->ldt[2]), get_limit(0x1ff)); // 释放 str1 数据段占用的页面
    for (i = 0; i < NR_TASKS; i++) {
        if (task[i]->parent == current->pid) {
            task[i]->state = 1;
            if (task[i]->state == TASK_ZOMBIE) {
                /* task[1] 总是 */
                send_sig(SIGCHLD, task[i]);
            }
        }
    }
}
```

步骤如图 6.20 所示。移除 str1 的内容并发送给父进程。移除该进程与 str1 进程可执行文件关系的具体实现方式是：先释放与父进程共享的文件，然后内核将 str1 进程设置为僵尸状态并向父进程发送信号。

![图 6.20 释放 str1 程序占用的页面。子进程已退出。信号处理问题将在第 8 章介绍。

代码如下：

```c
// code path:kernel/exit.c:
int do_exit(long code)
{
    for (i = 0; i < NR_OPEN; i++)
        if (current->filp[i]) // 随后释放与
            // 父进程共享的文件
            sys_close(current->filp[i]);
    current->pwd = NULL;
    current->root = NULL;
    current->executable = NULL; // 上方释放与
        // 父进程共享的文件
    current->state = TASK_ZOMBIE;
    current->exit_code = code;
    tell_father(current->parent); // 设置 str1 为僵尸状态
    // 向父进程发送信号
}
```

移除关系并向父进程发送信号的过程如图 6.21 所示。实现退出后的进程调度。str1 进程退出的切换过程。代码如下：

```c
// code path:kernel/exit.c:
int do_exit(long code)
{
    current->state = TASK_ZOMBIE;
    current->exit_code = code;
    tell_father(current->parent); // 设置 str1 为僵尸状态
    // 向父进程发送信号
    schedule();
    return (-1); /* 只是为了 */
}
```

切换过程如图 6.22 所示。

![图 6.21 str1 退出后的切换内容。
![图 6.22 str1 退出后的切换。

## 6.4 多个用户进程并发

在本节中，我们将通过 str1、str2 和 str3 三个示例查看如何执行和切换进程。

### 6.4.1 进程调度

创建 str1、str2 和 str3 进程。假设系统中没有用户处理。外设有三个可执行文件 str1、str2 和 str3，文件中的程序是之前介绍的 str 进程代码。在此，我们按顺序创建三个用户进程：str1、str2 和 str3。

现在 `last_pid` 累加到了 4，所以这三个进程的 pid 应该是 5、6 和 7。现在，第一个已经被 `task[64]` 占用，`task[64]` 中的数字是 4、5 和 6。由此推推出它们在线性空间中的位置应该是：4×64 MB 到 5×64 MB、5×64 MB 到 6×64 MB 以及 6×64 MB 到 7×64 MB。

这三个进程在线性空间中的分布如图 6.23 所示。图 6.24 显示了三个进程的 `task_struct` 以及推入栈的数据在物理内存中的分布。

![](img/f661d64b7eb54840fcb4d65765a4e933_346_0.png)

图 6.25 str1 进程推入栈的影响。

str1 进程。之后，文本数组的进程设置内容被写入新分配的物理页中。

结果如图 6.25 所示。在 str1 运行期间，产生了定时器中断并切换到 str2。在 Linux 0.11 中，有两种情况会导致进程切换。一种是定时器中断，它与正在运行的进程完全没有关系。无论运行的是哪个进程，无论是特权级 0 还是特权级 3，都会产生定时器中断。如果明确有切换需求，就会进行切换。另一种是由正在运行的进程调用的。当进程在内核态运行时，如果进程程序需要从硬盘读取数据，则该进程在获取数据之前无法继续执行，它会挂起当前进程并切换到其他进程。在这两种情况下，TSS 和 LDT 中的全套信息都随进程移动。让我们先看由定时器中断引起的切换。当 str1 运行时，定时器中断会产生 10 ms，这会减少它的时间片。因此，我们在程序中调用 `sleep()` 函数来实现时间延迟的效果。当当前进程的时间片被削减为 0 时，如果程序尚未结束，且特权级为 0 或 3。如果 str1 进程正在执行程序且特权级为 3，那么它将调用 `schedule` 函数为切换做准备。

```c
// code path:kernel/sched.c:
void do_timer(long cpl) {
    if (--current->counter > 0) return;
    current->counter = 0;
    if (cpl) return;
    schedule();
}
```

当切换到运行 str2 进程时，它执行了相同的逻辑程序。值得注意的是，在设置文本数组时，打印屏幕和 str1 程序的本地地址是相同的。但它们的线性地址是不同的，且 str2 进程在物理内存中并没有与 str1 重叠。

str2 推入栈的影响如图 6.26 所示。在 str2 运行期间，当它遇到定时器中断时，会切换到 str3。当 str2 运行一段时间后，时间片削减为 0，然后切换到 str3，它也推入栈，然后 str3 开始运行。实现方式与 str2 进程相同。它也被推入栈并设置了文本。str3 推入栈的影响如图 6.27 所示。

我们可以稍微修改 str3 的代码，调用 `open()`、`read()` 和 `close()` 函数从硬盘读取文件，这会映射到 `sys_read()` 函数。在读取磁盘中的指令后，数据不会立即进入缓冲区。没有数据，str3 无法继续执行。此时它会挂起自己，然后切换到其他进程执行。

![](img/f661d64b7eb54840fcb4d65765a4e933_347_0.png)

图 6.26 str2 推入栈的影响。

![](img/f661d64b7eb54840fcb4d65765a4e933_347_1.png)

图 6.27 str3 推入栈的影响。

### 6.4.2 进程阻塞与唤醒

代码如下：

```c
// code path:fs/buffer.c
struct buffer_head * read(int dev, int block)
{
    struct buffer_head * bb;
    if (!(bb = getblk(dev, block))) {
        panic("read: getblk NULL\n");
    }
    if (bb->b_uptodate) {
        return bb;
    }
    ll_rw_block(READ, bb);
    wait_on_buffer(bb); // 是否需要等待缓冲区
                        // 释放锁并因此挂起进程
    if (bb->b_uptodate) {
        return bb;
    }
    brelse(bb);
    return NULL;
}

static inline void wait_on_buffer(struct buffer_head * bb)
{
    cli();
    while (bb->b_lock) {
        sleep_on(&bb->b_wait); // 块仍处于锁定，所以
                                // 有必要挂起进程
    }
    sti();
}

void sleep_on(struct task_struct **task)
{
    struct task_struct *tmp = *task;
    *task = current;
    current->state = TASK_UNINTERRUPTIBLE; // 挂起当前进程，它是 str3
    schedule(); // 在这种情况下切换到其他进程
    if (tmp) {
        tmp->state = 0;
    }
}
```

### 6.4.3 时间片轮转与内存分布

当三个程序运行一段时间后，内存中的分布模式是什么？当 str3 运行一段时间后，时间片用完。尽管这三个用户进程仍需继续运行，但时间片已经用尽。如果再次发生定时器中断，`do_timer` 将调用 `schedule()` 再次切换到进程，系统将为它们重新分配时间片。

从 `task[]` 数组最后，内核为所有进程重新分配时间片。时间片的大小与进程的优先级成正比。优先级越高，时间片越大。

```c
// code path:sched.c:
void schedule()
{
    for (p = LAST_TASK; p > FIRST_TASK; --p)
        if (p->state == TASK_RUNNING)
            (*p)->counter /= 2;
}
```

值得注意的是，当系统有多个进程时，时间片会在它们之间分配。每个进程的优先级决定了它获得的时间片。优先级较高的进程获得较长的时间片。

str3 推入栈的影响如图 6.27 所示。页面共享情况如图 6.28 所示。str2 推入栈的影响如图 6.26 所示。结果如图 6.30 所示。

![](img/f661d64b7eb54840fcb4d65765a4e933_349_0.png)

图 6.28 这三个程序运行期间数据的栈分布。

### 6.4.4 页面保护

进程 A 和 B 共享页面。假设系统有一个用户进程（进程 A），其相应的程序已加载到内存中。内存中的页面引用数为“1”，然后开始执行，通过调用 `fork()` 函数创建一个新进程（进程 B）。创建进程时，系统将 A 的所有页表拷贝到 B，并设置 B 的页目录（PDE）。此时，两个进程共享页面，累加为 2，且共享页面被设置为“只读”属性，这意味着进程 A 或 B 只能对这些共享页面进行读取操作，而不是写入操作。

代码如下：

```c
// code path:mm/memory.c:
int copy_page_tables(unsigned long from, unsigned long to, unsigned long size)
{
    for (nr = 0; nr < page_table; ++page_table++) {
        this_page = *from_page_table; // 进程 A 的页面属性
        if ((1 & this_page)) // 设置只读
            continue;
        this_page &= ~2;
        *to_page = this_page; // 进程 B 的页面属性
        if (this_page > LOW_MEM) { // 设置只读
            *from_page_table = this_page;
            this_page = LOW_MEM;
            this_page >>= 12; // mem_map 中的引用计数记录
            mem_map[this_page]++; // 累加 2
        }
    }
}
```
