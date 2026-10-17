
## 7.2.4 下半部

然而，经常发生的情况是并不是所有函数都需要在发生后立即执行；虽然“重要”的操作需要立即处理，但其他操作可以稍后处理，或者需要较长时间，此时阻塞中断是更理想的。对于这种情况，创建了下半部（bottom halves）。在每次 `ret_from` 之后，即在每次慢速中断之后，如果此时没有进一步的中断在运行，系统会扫描一个多达 32 个下半部的列表。如果它们被标记为激活，则会被依次执行，然后自动标记为非激活。这些下半部是原子的，也就是说只要有一个下半部处于激活状态，其他的就无法执行，因此不需要使用 `cli()` 来保护它们免受中断。

安装下半部的函数是 `init_bh`，它将下半部引入函数指针表 `bh_base` 中。

```c
void init_bh(int nr, void (*routine)(void));
```

```c
enum {
  TIMER_BH = 0,
  CONSOLE_BH,
  TQUEUE_BH,
  DIGI_BH,
  SERIAL_BH,
  RISCOM8_BH,
  BAYCOM_BH,
  NET_BH,
  IMMEDIATE_BH, KEYBOARD_BH, CYCLADES_BH, CM206_BH;
};
```

> 6 这很容易发生，例如当一个慢中断被另一个中断中断时。

在 Linux 版本中，下半部是“手动”进入 `bh_struct` 结构体的；此外，还可以将任何所需数据的指针作为参数传递给它们。默认情况下，所有下半部都是允许的，但可以使用以下函数将其关闭并重新开启：

```c
void disable_bh(int nr);
void enable_bh(int nr);
```

函数 `mark_bh` 标记一个下半部，使得该下半部在下一个可用机会执行。

```c
void mark_bh(int nr);
```

现在我们将以键盘驱动程序为例，检查如何使用下半部。

```c
static void keyboard_interrupt(struct pt_regs *regs)
{
    mark_bh(KEYBOARD_BH); /* 标记 kbd_bh() */
}

static void kbd_bh(void *unused) {
    unsigned char Leds = getleds();
    if (Leds != ledstate) { ledstate = Leds; }
}
```

```c
unsigned Long kbd_init(unsigned Long kmmem_start) {
    request_irq(KEYBOARD_IRQ, keyboard_interrupt, 0, "keyboard", NULL);
    /* 键盘下半部初始化 */ /* 立即标记 */
    init_bh(KEYBOARD_BH, kbd_bh);
    mark_bh(KEYBOARD_BH);
}
```

键盘驱动程序的初始化函数将 `kbd_bh()` 安装为下半部，并将 `keyboard_interrupt()` 安装为慢中断。在每次调用键盘中断时，都会调用 `mark_bh(KEYBOARD_BH)` —— 使得下半部在键盘中断完成后第一个可用机会运行，在本例中，是在中断后立即运行。然而，键盘下半部只更新键盘 LED。

## 7.2.5 任务队列

如上一节所示，使用下半部相当困难，因为它们的数量被限制在 32 个，且某些任务已经分配了固定的编号。在 2.0 版本中，LINUX 提供了任务队列（task queues）作为下半部概念的动态扩展。

任务队列允许任意数量的函数被放入队列并在稍后的时间一个接一个地处理。待执行函数的链是通过 `tq_struct` 实现的。

```c
struct tq_struct {
    struct tq_struct *next; /* 指向下一个条目的指针 */
    int sync; /* 同步标志 */
    void (*routine)(void *); /* 要调用的函数 */
    void *data; /* 任意函数参数 */
};

typedef struct tq_struct *task_queue;
```

在将函数放入任务队列之前，必须创建并初始化一个 `tq_struct`。`routine` 组件包含要调用的函数地址，而 `data` 组件持有在调用时传递给函数的任意参数。`sync` 组件必须初始化为 0。

插入任务队列的操作通过以下函数之一实现：

```c
void queue_task(struct tq_struct *bh_pointer, task_queue *bh_list) {
    if (!set_bit(0, &bh_pointer->sync)) {
        unsigned Long flags;
        save_flags(flags);
        cli();
        bh_pointer->next = *bh_list;
        *bh_list = bh_pointer;
        restore_flags(flags);
    }
}

void queue_task_irq(struct tq_struct *bh_pointer, task_queue *bh_list) {
    if (!test_bit(0, &bh_pointer->sync)) {
        bh_pointer->next = *bh_list;
        *bh_list = bh_pointer;
    }
}

void queue_task_irq_off(struct tq_struct *bh_pointer, task_queue *bh_list) {
    if (!test_bit(0, &bh_pointer->sync)) {
        bh_pointer->sync = 1;
        bh_pointer->next = *bh_list;
        *bh_list = bh_pointer;
    }
}
```

这些函数的应用体现在它们的实现中。`tq_struct` 的 `sync` 组件用于同步。当结构被插入任务队列时，它会被设置，以防止进一步插入。最简单的情况发生在中断被禁用时。只需检查 `sync` 是否已设置，`queue_task_irq_off()` 函数就可以在中断开启时被调用。在中断处理程序内部可以处理下半部，这是通过必须从中断程序调用的 `queue_task_irq()` 函数实现的。另一方面，由于任务队列受 `cli()` 宏保护，可以在任何地方处理。`run_task_queue()` 函数负责任务队列。

```c
void run_task_queue(task_queue *list) {
    struct tq_struct *p;
    p = xchg(list, NULL);
    while (p) {
        void *arg;
        void (*f)(void *);
        struct tq_struct *save_p;
        arg = p->data;
        f = p->routine;
        save_p = p;
        p = p->next;
        save_p->sync = 0;
        (*f)(arg);
    }
}
```
