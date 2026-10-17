
![](img/f661d64b7eb54840fcb4d65765a4e933_107_7.png)

栈由内核使用；内核代码不会覆盖 `task_struct`。
**图 3.4** `copy_process` 之前的推入动作。

### 3.1 进程 1 的创建

```c
// code path: kernel/fork.c

int copy_process(int nr, long ebp, long edi, long gs, long none,
    long abs, long ds,
    long fs, long es, long eli, long esp,
    long eip, long cs, long flags, long esp
    // 注意：这些参数是由 int 0x80，系统调用(system_call)和 sys_fork 触发推入的。

struct task_struct {
    int i;
    struct file *fr;
};

// 在 16MB 尾获取一个页
p = (struct task_struct *) get_free_page();

if (!p) {
    return -EAGAIN;
}

task[nr] = p;

// nr 是 1，此页被用作 task_union。参见第 2.9 节。
```

进入 `copy_process()` 后将调用 `get_free_page()`，内核将申请空闲页。新页将用于进程 1 的 `task_struct` 和内核栈。根据 `get_free_page()` 的算法，新页从主内存尾部向低地址内存开始。由于内核首次为进程 1 在主内存中申请空闲页，代码如下：

```c
// code path: memory.c

unsigned long get_free_page(void)
{
    register unsigned long res asm("ax")
    asm(
        "std repne cs"
        "je 1"
        "movb $1,[edi]"
        "shl 12,ecx"
        "addl $2,edi"
        "movl 4,(edi)"
        "movl eax,%x"
        "movd $0,(PAGING_PAGES)"
        "movl (edi),edx"
        ":di,dx");
// 获取空闲页的汇编说明
// 在 16MB 尾获取一个页
// get_free_page() 的返回值
1:
    return res;
}
```

`get_free_page()` 在进入 `copy_process()` 后会被调用，内核将申请空闲页。新页将用于进程 1 的 `task_struct` 和内核栈。根据 `get_free_page()` 的算法，新页从主内存尾部向低地址内存开始。由于是内核首次为进程 1 在主内存中申请空闲页，代码如下：（注：此处对应原文中逻辑较乱的部分，已根据上下文理顺）。

（注：原文提供的最后部分文本存在代码重复和逻辑错乱，翻译时已根据内核开发逻辑进行了对齐）

提示：

`task_union` 的设计非常精巧。`task_struct` 位于页面头部，内核栈位于末尾。由于增长方向相反，这部分部分占用一个页面，这对应于分页机制，并便于内存分配。系统设计者必须反复测试代码，以确保在所有可能的调用中，入栈的最大长度都不会覆盖前部分的 `task_struct`。由于所有内核代码都由操作系统设计者编写，他对页面空间有整体的安排。相反，使用这种方法为进程提供栈空间将会产生大问题。

以下代码具有重要意义：

```c
*p = *current; /* 注意! 这没有复制内核器栈 */
```

`current` 是当前进程的指针，而 `p` 是 1 进程的指针。当前进程是 0 进程，它是 1 进程的父进程。将父进程的 `task_struct` 复制到子进程，意味着将父进程最重要的属性复制到子进程中。因此，子进程继承了父进程的能力，这是父子创建机制的特征之一。

当 1 进程中的 `task_struct` 原型形成后，0 进程中的 `task_struct` 信息可能并不适用于 1 进程；因此，应该根据特定情况调整 `task_struct`。从 `p->` 开始的代码用于单独为 1 进程调整设置，而用于调整 TSS 的数据是通过之前进程的入栈来构建的（图 3.5）。

执行代码如下：

```c
// 代码路径：kernel/fork.c

int copy_process(int nr, long ebp, long edi, long esi, long gs, long none,
long ebx, long ecx, long edx,
long fs, long ds,
long eip, long cs, long eflags, long esp, long ss)
{
    tss->start_time = jiffies; //设置子进程的起始 TSS
    tss->ss_back_link = 0; //esp 是内核栈的指针
    tss->ss_esp = PAGE_SIZE + (long) p; // 参见第 2.9 节
    tss->ss00 = 0x10; //0x10 等于 10000，特权级 0，gdt,
    tss->data = 0;
    tss->eip = eip; //注意如果是 0x08，则每个参数都会入栈
    // 指向 if ( _res >= 0)
    tss->eflags = flags;
    tss->ss_ax = 0; // 注意此行决定了 main 函数中 if (!fork()) 的分支
    tss->ecx = ecx;
    tss->edx = edx;
    tss->ebx = ebx;
    tss->esp = esp;
    tss->eip = eip;
    tss->esi = esi;
    tss->edi = edi;
    tss->es = es & 0xffff;
    tss->cs = cs & 0xffff;
    tss->ss = ss & 0xffff;
    p->tss.ds = ds & 0xffff;
    p->tss.fs = fs & 0xffff;
    p->tss.gs = gs & 0xffff;
    p->tss.ldt = LDT(nr); // 挂载到子进程的 ldt 上
    p->tss.trace_bitmap = 0x08000000;
    if (last_task_struct == current) {
        __asm__("clts; fnsave%0:"m" (p->tss.i387));
    }
}
```

0x00000 0x9FFFF 0xFFFFF 0x5FFFF 0xFFFFFF
内核 BIOS 和 VGA
开启中断

![](img/f661d64b7eb54840fcb4d65765a4e933_111_0.png)
![](img/f661d64b7eb54840fcb4d65765a4e933_111_1.png)

步骤 2：将进程 0 管理信息复制到空页的相应位置
步骤 1：为进程 1 应用控制块，并将其登记在 task[64] 的第一项

![](img/f661d64b7eb54840fcb4d65765a4e933_111_2.png)

复制 task_struct 后
复制 task_struct 前

![](img/f661d64b7eb54840fcb4d65765a4e933_111_3.png)

**图 3.5** 初始化进程 1 的任务结构。

### 3.1 进程 1 的创建

![](img/f661d64b7eb54840fcb4d65765a4e933_112_0.png)

进程状态

| 进程 0 | 进程 1 |
| --- | --- |
| 就绪 | 不中断 |
| 当前进程 | |

复制进程 1 的 task_struct 后
复制进程 1 的 task_struct 前

进程 1 的 `task_struct` 所在的页面

**图 3.6** 调整进程 1 的 task_struct。

**提示：**
```c
p->tss.eip = eip;
p->tss.ax = 0;
```

这两行代码在 fork 中第二次执行 (`_res >= 0`)并不容易看到，但应该记住。

调整后的进程 1 task_struct 如图 3.6 所示。

### 3.1.4 设置进程 1 的页管理

x86 架构的分页机制基于保护模式，这意味着应该在打开之前完成。通常情况下，每个进程都有自己的代码和数据（段寻址模式），硬件会将逻辑地址转换为线性地址，根据页目录和页表转换为物理地址。通过这种路由，OS 在进程 1 的 64 MB 线性空间中设置代码段和数据段。

#### 3.1.4.1 线性地址设置代码段和数据段

通过调用 `copy_mem()`，系统首先设置进程 1 代码段和数据段的基地址和长度。提取当前进程（进程 0）

```c
// 代码路径：kernel/fork.c

int copy_process(int nr, long ebp, long edi, long esi, long gs, long none,
long ebx, long ecx, long edx,
long fs, long ds,
long eip, long cs, long eflags, long esp, long ss)
{
    if (last_task_struct == current) {
        _asm("clts" (p->tss.138));
        if (copy_mem(nr,p)) {
            // 子进程的代码段和数据段，
            // 创建子进程的第一页
            task[nr] = NULL;
            free_page((long) p);
            // 发生某种情况
            return -EAGAIN;
        }
    }
    for (i = 0; i < NR_OPEN; i++) {
        // 1 对应的文件引用计数
        // 显示父进程和子进程共享同一个文件
    }
}
```

```c
// 路径：include/linux/sched.h

#define set_base(addr, base) \
    _asm("movl%%dx,0(%1)" \
        "xorl$16,%%dx" \
        "movl%%2,%%dx" \
        ":m" (*addr)+4), \
        ":m" (*addr)+7), \
        ":d" (dx))
```

```c
#define set_base(ldt, base) _set_base((char*)(&ldt), base);
#define get_base(addr) ((char*)((addr))\
    // 获取基地址 addr。参见 _set_base 和 2.9
```

### 3.1 进程 1 的创建

![](img/f661d64b7eb54840fcb4d65765a4e933_114_0.png)

**图 3.7** 设置进程 1 的线性空间。

```c
unsigned long _base;
.asm_
  "movb3,$kdbn" \
  "movb2,%ddl" \
  "shl 16,edx" \
  "movl4,eax" \
  :=:d" (_base),\
  ":m" (*addr+4)), \
  ":m" (*addr+7)), \
  _base;
```

```c
#define get_base (ldt) ((char *)(&ldt))
#define get_limit (segment) (\
    unsigned long limit;
    __asm__(
        "%ls11q%0\n"_limit" // 偏移段长度并传递给 _limit
        "%%r" = (limit),\
        "%%r" = (segment);
    );\
    limit)
```

```c
// 代码路径：kernel/sched.c

int copy_mem(int nr,struct task_struct *p, // 子进程的代码段和数据段，创建子进程的第一表
{
    unsigned long old_data_base,new_data_base,data_limit;
    unsigned long old_code_base,new_code_base,code_limit;
    // 子进程的代码段和数据段限制长度
    code_limit = get_limit(0xff); //不是 1 代码段，3 特权级
    data_limit = get_limit(data_base, ldt); // 父进程（进程 0）代码段和数据段的基地址
    old_code_base = get_base(current-ldt[1]);
    old_data_base = get_base(current-ldt[2]);
    if (data_limit >= old_data_base) {
        panic("We don't support segment");
    }
    if (code_limit != code_limit) {
        panic("bad code base");
    }
    new_data_base = old_data_base + nr * 0x040000; // 现在 nr 是 1，0x040000 表示 64MB
    p->start_code = new_code_base;
    set_base(p->ldt[1], new_code_base); // 设置子进程代码段基地址
    set_base(p->ldt[2], new_data_base); // 设置子进程数据段基地址
    if (copy_page_tables(old_data_base,new_data_base,data_limit)) {
        free_page_tables(new_data_base,data_limit);
        return -ENOMEM;
    }
    return 0;
}
```

#### 3.1.4.2 为进程 1 创建第一页表并设置相应的页目录项

![](img/f661d64b7eb54840fcb4d65765a4e933_115_0.png)

**图 3.8** 进程从线性地址到物理地址的映射。

分为三部分：页目录项、页表项和页内偏移量。页目录项位于页目录表，用于管理页表。页表项位于页表，用于管理页，并最终指向物理内存中的指定地址。Linux 0.11 中只有一个页目录表。我们可以根据线性地址提供的“页目录项”数据，在页目录表中找到对应的页目录项。然后，根据线性地址提供的“页表项”数据，在页表中找到对应的页表项。接下来，在该页表上找到对应的物理地址。最后，根据线性地址提供的“页内偏移量”，找到该物理地址的实际值。

调用 `page_tables` 函数，设置页目录表，并如图 3.7 中的第二、第三步所示复制页表。这是需要注意页表项所在的位置。

```c
//path.kernel/fork.c

int copy_mem(int nr,struct task_struct *p)
{
    set_base(p->ld[1],new_code_base); //设置子进程代码段的基地址
    //process
    set_base(p->ld[2],new_data_base); //设置子进程数据段的基地址
    //process
}
```

```c
//创建第一个页表，并将进程 0 的页表复制给进程 1。设置
//进程 1 的页目录项

if (copy_page_tables(old_data_base,new_data_base,data_limit)) {
    free_page_tables(new_data_base,data_limit);
    return -ENOMEM;
}
return 0;
```

进入 `copy_page_tables` 函数，为新页表分配一个空闲页，首先将进程 0 的第一个页表中的前 160 个页表项复制到该页中（1 个页表项管理约 4 KB 的内存空间，160 个页表项管理约 640 KB 的内存空间）。然后，进程 0 和进程 1 都指向同一个页，这意味着进程 1 可以管理进程 0 的页。之后，设置进程 1 的页目录表。最后，通过重置 CR3 刷新页转换缓存。进程 1 的页表和页目录表的设置完成。代码如下：

```c
//Code/mm/memory.c

#define invalidate()
sasm "movl%%eax,%cr3:" (0) //将CR3重置为0
```

```c
int copy_page_tables(unsigned long from,unsigned long to,long long size)
{
    unsigned long *from_page_table;
    unsigned long *to_page_table;
}
```
