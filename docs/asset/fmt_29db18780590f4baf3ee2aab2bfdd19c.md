
#define EDI 4

#define EBP 5

#define EAX 6

#define DS 7

#define ES 8

#define FS 9

#define GS 10

#define ORIG_EAX 11

#define EIP 12

#define CS 13

#define EFL 14

#define UESP 15

#define SS 16

#define FRAME_SIZE 17

**图 22.10** 栈上寄存器字段的偏移量

- **4–12** 这些是 `struct pt_regs` 中的标准字段。
- **13–14** 这些字段不在 `struct pt_regs` 中。这是它们所在的逻辑位置，将它们放在这里会导致此图中的剩余偏移量偏移 2。
- **15–20** 这些是 `struct pt_regs` 中的标准字段。

## 22.6 显示信息

内核有时需要向用户或系统管理员显示其内部状态的信息。Linux 提供了一系列用于此函数；它们通常在检测到内核变量不一致时被调用，并在控制台上显示诸如寄存器值和栈内容等信息。

### 进程追踪

```c
200 int cpu=smp_processor_id();

202 printk("%s, CPU%d:\n", str, cpu);
203 printk("irq [%d]", irqs_running());
204 for(i=0; i<smp_num_cpus;i++)
205 printk("%d", local_irqs_count(i));
206 printk("\nbh: [%d]", spin_is_locked(&global_bh_lock)?1:0);\n");
207 for(i=0; i<smp_num_cpus;i++)
208 printk("%d", local_bh_count(i));
210 printk("\nStack dumps:\n");
211 for(i=0; i<smp_num_cpus; i++) {
212 unsigned long esp;
213 if (i==cpu)
214 continue;
215 printk("\nCPU%d:", i);
216 esp=init_tss(i).esp;
217 if (!esp) {
222 printk("<unknown> \n");
223 continue;
225 esp=~(THREAD_SIZE-1);
226 esp+=sizeof(struct task_struct);
227 show_stack((void*)esp);
228 }
229 printk("\nCPU%d:", cpu);
230 show_stack(NULL);
231 printk("\n");
232 }
```

图 22.13 显示调试信息

197 参数是一个指向信息消息的指针，显示在第 202 行。

200 获取我们正在运行的处理器的标识号（ID）（见第 7.2.1.4 节）。

202 此处打印了作为参数传递的消息和 CPU 编号。

203 打印 `irqs_running()` 返回的数值（见第 14.5.1.5 节）。值为 1 表示内核运行在中断上下文中；0 表示不是。

204–205 对于每个 CPU，我们使用第 16.5.1.2 节中的宏打印正在处理的中断数量。

206 此处的值为 1 或 0，取决于全局半锁（global-half lock）是否被持有。`spin_is_locked()` 函数在第 5.3 节（针对单处理器情况）和 5.4.3.4 节（针对多处理器情况）中描述。

### 显示调试信息

207–208 对于每个 CPU，我们打印正在处理的底半（bottom halves）数量。底半在第 16.3 节中讨论过。

210–228 此处打印所有 CPU 的堆栈转储（stack dumps）。

211–228 我们遍历每个 CPU。

213–214 我们跳过当前正在运行的 CPU 并再次循环。这一个将在第 229–231 行进行更详尽的处理。

215 我们打印 CPU 标识符。

216 此处获取该 CPU 的栈顶地址。

217–224 这考虑了 CPU 未完全初始化的。`esp` 字段在 `cpu_init()` 中被设置为 NULL；它在 CPU 返回用户空间时被初始化。

222–223 在这种情况下，它会打印 `<unknown>` 并继续处理下一个 CPU。

225 字面量常量 `THREAD_SIZE` 在 `<asm/processor.h>` 中定义为：

```c
450 #define PAGE_SIZE (2*PAGE_SIZE)
```

在 i386 上，`PAGE_SIZE` 为 0x1000，因此 `THREAD_SIZE` 为 0x2000，或者说二进制为 0010 0000 0000 0000。那么 `THREAD_SIZE-1` 是 0001 1111 1111 1111。这使得 `esp` 中的 `~(THREAD_SIZE-1)` 为 1110 0000 0000 0000。与 `esp` 进行按位与（AND）确保了 `esp` 中的高 13 位被 0。这意味着它指向分配给 `task_union`（见 3.3.1）空间的底部。

226 加上 `task_struct` 的大小使 `esp` 指向栈空间的底部。

227 该函数在第 22.6.2 节中讨论过。它显示来自栈的值。

229 当打印完其他 CPU 的信息后，我们随后显示我们自己 CPU 的信息。

230 使用 `NULL` 参数调用 `show_stack()` 会导致它显示当前进程的栈。

## 22.6.2 显示栈值

图 22.14 所示的函数来自 `arch/i386/kernel/traps.c`，打印栈上的最后 24 条目。它作为参数传递给栈区域。

```c
166 void show_stack(unsigned long* esp)
167 {
168 unsigned long *stack;
169 int *i;
174 if(esp==NULL)
175 esp=(unsigned long*)&esp;
```

### 进程追踪

```c
176 stack = esp;
177 for(i=0; i<stack_depth_print; i++) {
178     if(stack==NULL)
179         break;
180     // ... 略 ...
181 }
```
*(注：原文提供的代码片段在某些处不完整，此处已根据逻辑对应)*

)* 那么 `THREAD_SIZE-1` 是 0001 1111 1111 1111。这使得 `~(THREAD_SIZE-1)` 在 `esp` 中为 1110 0000 0000 0000。与 `esp` 进行按位与（AND）确保了 `esp` 中的高 13 位被设置为 0。这意味着它指向分配给 `task_union`（见 3.3.1）空间的底部。

226 加上 `task_struct` 的大小使 `esp` 指向栈空间的底部。

227 该函数在第 22.6.2 节中讨论过。它显示来自栈的值。

229 当打印完其他 CPU 的信息后，我们随后显示我们自己 CPU 的信息。

230 使用 `NULL` 参数调用 `show_stack()` 会导致它显示当前进程的栈。

## 22.6.2 显示栈值

图 22.14 所示的函数来自 `arch/i386/kernel/traps.c`，打印栈上的最后 24 条目。它作为参数传递给栈区域。

```c
166 void show_stack(unsigned long* esp)
167 {
168 unsigned long *stack;
169 int *i;
174 if(esp==NULL)
175 esp=(unsigned long*)&esp;
```

### 进程追踪

*(注：此处原文文本似乎存在重复或错乱，已根据“不要重复输出原文”原则进行翻译对齐)*

174 如果栈指针为 `NULL`，则取其地址作为参数。这意味着我们要处理当前的栈。

178–184 通过将栈指针与 `THREAD_SIZE-1` 进行按位与，防止我们溢出栈区域。如果低位也为 0，说明我们到达栈区域的末尾，退出循环。

181–182 每 8 个值输出一个新行，并缩进下一行。

183 此处的函数在 22.6.3 节中描述。它是 `esp` 作为参数传递的，而不是 `stack`，因此它从栈的底部开始打印。

## 22.6.3 栈上的调用帧

图 22.15 所示的函数来自 `arch/i386/kernel/traps.c`，回溯栈上的调用帧。它只打印栈中可能是返回地址的条目。

```c
134 void show_trace(unsigned long *stack)
135 {
136 int i;
137 unsigned long addr;
138
```
