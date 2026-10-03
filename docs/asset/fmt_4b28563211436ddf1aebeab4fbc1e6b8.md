
![](img/f661d64b7eb54840fcb4d65765a4e933_81_0.png)

图 2.15 启动时间设置。

启动时间的计算过程及其在内存中的存储位置如图 2.15 所示。

## 2.9 初始化进程 0

进程 0 是 Linux 的第一个进程，也是启动 Linux OS 的第一个父进程。以下内容对主机上进程 0 的正常运行具有最重要且深远的影响，主要包括三个方面：

- 1. 初始化进程 0。

进程 0 的 `task_struct(init_task)` 已经在代码设计中实现，但这并不意味着进程 0 已经可用了。我们需要在进程 0 的 `task_struct` 中用 GDT 钩（hook）LDT 和 TSS，并初始化 GDT、进程任务以及与进程调度相关的寄存器。

- 2. 作为一个现代操作系统，Linux 0.11 最重要的指标是它支持多进程执行，这意味着一个进程需要处理多个进程的轮询能力。系统将设置定时器中断，为进程 0 以及其他进程的调度奠基础（这些进程直接或间接地通过进程 0 进行）。

- 3. 进程 0 需要处理系统调用。运行中的每个进程都可能通过系统调用程序与内核进行交互。系统使用 `set_system_gate` 将 `system_call` 与 IDT 绑定，然后进程 0 就具备了处理系统调用的能力。`system_call` 是任何系统调用的通用入口。

进程 0 需要获得三种能力，以确保它在未来正常运行并将这些能力传递给它的后代。

代码如下：

```c
// Code path: init/main.c
void main(void)
{
    sched_init();
}
```

```c
// Code path: kernel/sched.c
#define LATCH (1193180/HZ)    // 每个时间片的振动频率

union task_union {
    // task_struct 和内核栈的联合体
    struct task_struct task;
    char stack[PAGE_SIZE];        // PAGE_SIZE 是 4K
};

static union task_union init_task = {INIT_TASK}; // 进程 0 的 task_struct

// task[0] 被进程 0 使用
struct task_struct *task[NR_TASKS] = {&(init_task.task)};
```

```c
void sched_init(void)
{
    int i;
    struct desc_struct *p;

    if (sizeof(struct sigaction) != 16)
        panic("struct sigaction MUST be 16 bytes"); // set TSO

    set_tss_desc(gdt + FIRST_TSS_ENTRY, &init_task.task.tss); // set LDT0
    set_ldt_desc(gdt + FIRST_LDT_ENTRY, &init_task.task.ldt); // 从第六个开始将所有 LDT 设为 0

    for (i = 0; i < NR_TASKS; i++) { // gdt 表并清空进程槽 1
        task[i] = NULL;
        p->a = p->b = 0;
        p++;
    }
}
```

```asm
/* 清除 NT，否则以后会遇到麻烦 */
asm("pushfl; andl $0xffffbfff,(%esp); popfl");
/* ltr(0); 重要！绑定 tr 到 TR 寄存器 */
ltr(0);
/* lldt(0); 重要！绑定 ldt 寄存器 */
lldt(0);
/* 定时器设置 */
outb_p(0x36, 0x43);        // 二进制，模式 3，LSB/MSB
outb_p(LATCH & 0xff, 0x40); // 定时器中断频率低字节
outb(LATCH >> 8, 0x40);    // 定时器中断频率高字节
set_intr_gate(0x20, timer_interrupt);
outb(inb_p(0x21) & ~0x01, 0x21); // 8259A 主片开启 IRQ0
set_system_gate(0x80, system_call); // 设置系统调用入口
```

```c
// Code path: include/linux/sched.h
#define FIRST_TSS_ENTRY 4
#define FIRST_LDT_ENTRY 5
#define _TSS(n) ((((unsigned long) n) << 4) + (FIRST_TSS_ENTRY << 3))
#define _LDT(n) ((((unsigned long) n) << 4) + (FIRST_LDT_ENTRY << 3))
#define ltr(n) __asm__("ltr %%ax"::"a" (_TSS(n)))
#define lldt(n) __asm__("lldt %%ax"::"a" (_LDT(n)))
```

```c
// Code path: include/asm/system.h
#define set_intr_gate(n, addr) \
    _set_gate(&idt[n], 14, 0, addr)
#define set_trap_gate(n, addr) \
    _set_gate(&idt[n], 15, 0, addr)
#define set_system_gate(n, addr) \
    _set_gate(&idt[n], 15, 3, addr)
#define set_tss_desc(n, addr) \
    _set_tssldt_desc(n, addr, 0x89)
#define set_ldt_desc(n, addr) \
    _set_tssldt_desc(n, addr, 0x82)
```

```asm
/* set_tssldt_desc 宏的内联汇编实现 */
asm("movw $104,%1\n\t"   /* 将 104 (0x68) 作为 limit 低 16 位 */
    "movw %%ax,%2\n\t"   /* 放入 TSS/LDT 基地址低 16 位 */
    "rorl $16,%%eax\n\t" /* 交换 eax 高低 16 位 */
    "movb %%al,%3\n\t"   /* 基地址 24-31 位 -> 字节 7 */
    "orb $0x10,%%al\n\t" /* 设置 G=0, D/B=1 (0x10) 等标志 -> 字节 5 */
    "movb %%al,%5\n\t"   /* 标志字节 -> 字节 5 */
    "movb %%ah,%4\n\t"   /* 基地址 16-23 位 -> 字节 4 */
    "rorl $16,%%eax\n\t" /* 恢复 eax */
    ::"a" (addr), "m" (*(n)), "m" (*(n+2)), "m" (*(n+4)), "m" (*(n+5)), "m" (*(n+7))
    :"ax")
```

```c
// Code path: include/linux/sched.h
struct tss_struct {
    long back_link;   /* 16 位高位补 0 */
    long esp0;        /* 栈指针 0 */
    long ss0;         /* 栈段 0 */
    long esp1;
    long ss1;
    long esp2;
    long ss2;
    long cr3;
    long eip;
    long eflags;
    long eax, ecx, edx, ebx;
    long esp;
    long ebp;
    long esi;
    long edi;
    long es;
    long cs;
    long ss;
    long ds;
    long fs;
    long gs;
    long ldt;
    long trace_bitmap;
};
```

（此处省略重复的结构体定义，保持逻辑一致）

## 2.9.1 进程 0 的初始化

### sched_init()

理解 `sched_init()` 函数的困难在于以下几行：

```c
set_tss_desc(gdt + FIRST_TSS_ENTRY, &init_task.task.tss);
set_ldt_desc(gdt + FIRST_LDT_ENTRY, &init_task.task.ldt);
```

这两行的目的是初始化 GDT 表中进程 0 的第 4、第 5 项。TSS0 和 LDT 的初始化如图 2.16 所示。

以 TSS0 为例；根据源码中的注释，我们可以画出如下所示（图 2.17 和图 2.18）。

对比源码和注释，我们可以发现 `movw $104,%1` 将 104 赋值给 limit 部分，G 为 0，这表示段限制为 104 字节。TSS 除本身外只有 104 字节。LDT 为 3 x 8 = 24 字节，这足够了。TSS 类型为 0x89，即 10001001。通过这种方式，`movb $0x10,%al` 分配了类型位等。同样，`movb $0,%5` 分配了 00 部分同时也方便地处理了 G、D/B、保留和 AVL 字段。

进程 0 的 `task_struct` 是由操作系统设计者硬编码的，即 `sched.h` 中的 `INIT_TASK` 指针（参见源码、相关结构和下面的注释），以及 `INIT_TASK` 初始化的 `task[64]` 第 0 项（图 2.19）。

`sched_init()` 随后会清除进程 0 中第 0 项以外的所有 `task[64]`，并同时清除 GDT 中 TSS 和 LDT 以上的所有项。结果如图所示。

![](img/f661d64b7eb5484fc4d65765a4e933_85_0.png)

### 段描述符

| 基地址 31:24 | G | D/B | 0 | AVL | 段限制 19:16 | P | DPL | S | 类型 | 基地址 23:16 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 基地址 15:0 | 段限制 15:0 |

**图 2.17** 段描述符的结构。

### TSS 0

| 字节 7: 基地址 31:24 | 字节 6: 0 | 字节 5: 类型/标志 | 字节 4: 基地址 23:16 |
| :--- | :--- | :--- | :--- |
| 字节 3: 基地址 15:8 | 字节 2: 基地址 7:0 | 字节 1: 段限制 15:8 | 字节 0: 段限制 7:0 |

**图 2.18** TSS0 的结构。

![](img/f661d64b7eb54840fcb4d65765a4e933_87_0.png)

步骤 1：设置进程 0 的信息

![](img/f661d64b7eb54840fcb4d65765a4e933_87_1.png)

**图 2.20** 初始化进程的关联任务。

初始化管理结构的最后一步非常重要（图 2.20）。它将 TR 寄存器指向 TSS0，LDTR 寄存器指向 LDT0。CPU 可以通过 TR 和 LDTR 寄存器在进程 0 中找到 TSS0 和 LDT0，从而找到进程 0 相关的管理信息。

## 2.9.2 设置定时器中断

定时器中断是进程 0 以及由进程 0 创建的其他进程调度的基础。设置定时器中断的过程分为以下三个步骤：

1.  设置 8253 芯片的 `LATCH` 值。此操作是图 2.21 中的第一步，关键是由宏定义的 `LATCH`，即 `sched.c` 中的 `#define LATCH (1193180/HZ)`，使得系统每 10 毫秒发生一次定时器中断。
2.  绑定定时器中断处理程序。这是图 2.21 中的第二步，绑定 `timer_interrupt` 函数后执行；当定时器中断发生时，系统可以通过中断描述表找到此服务例程并执行特定操作。

![](img/f661d64b7eb54840fcb4d65765a4e933_88_0.png)

图 2.21 设置定时器中断。

3.  在 8259A 芯片中开启与定时器中断相关的屏蔽位。开启后，产生定时器中断，从现在起每 10 毫秒产生一次定时器中断。由于处于“禁用中断”状态，CPU 不会响应，但进程 0 具有参与调度的潜力。

## 2.9.3 设置系统调用入口

系统调用处理函数 `system_call` 需要与 `int 0x80` 中断描述符绑定。`system_call` 是操作系统中系统软中断的总入口。所有用户程序都使用系统调用。产生 `int 0x80` 软中断后，操作系统通过总入口找到特定的系统调用函数。此过程如图 2.22 所示。

系统调用函数是程序在操作系统中运行的基础支持，其核心受硬件的特权级保护，不允许用户进程直接访问内核代码。但存在许多进程需要处理特定事务，例如读取磁盘和创建子进程等。为了解决冲突，操作系统的设计者提供了系统调用解决方案和一组接口。当用户进程需要处理内核事务时，它会立即触发 `int 0x80` 软中断。以下操作不需要用户程序参与，而是通过 CPU 响应中断的不同路径，改变特权级，从用户特权级 3 切换到特权级 0，通过中断描述符找到系统调用函数来处理事务，然后切换回进程的特权级 3，进程继续执行，冲突得以解决。

图 2.22 系统调用服务程序。

## 2.10 初始化缓冲区管理结构

缓冲区区域是内存与外设交换数据的中介。内存和硬盘之间最大的区别在于磁盘能以低成本保存大量数据。磁盘不参与操作（因为 CPU 无法对磁盘直接寻址）。此外，内存只需要存储数据，但这里更重要的是与 CPU 和总线执行数据操作。缓冲区介于两者之间，它不仅保存数据，还参与了搜索、组织以及间接的辅助操作。在有了外设缓冲区后，外设只需要根据需要与缓冲区交换数据，而不需要考虑内存将如何使用这些交互数据。至于内存，它也只需要考虑与缓冲区的交互已准备就绪，不需要关心缓冲区与外设之间的交互。组织和管理由操作系统操作。操作系统通过 `hash_table[NR_HASH]` 和 `buffer_head` 双向链管理缓冲区。

操作系统通过调用 `buffer_init` 函数设置缓冲区；代码如下：

```c
// Code path: init/main.c
void main(void)
{
    buffer_init(buffer_end);
}
```
