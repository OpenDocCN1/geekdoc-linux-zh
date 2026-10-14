
图 11.16 机器检查处理器的封装器

96–99 这是默认的机器检查处理程序，它仅打印警告消息。在实践中它永远不应该被调用。

105 此函数指针被静态初始化为指向`unexpected_machine_check()`函数（第 96–99 行）。它通常会被初始化代码覆盖，并指向`intel_machine_check()`（见第 11.6.2 节）。

107–110 该函数由机器检查异常的一级处理程序调用。随后调用已分配给第 105 行`machine_check_vector`函数指针的任何函数。

### 11.6.2 机器检查的二级处理程序

图 11.17 节自`arch/i386/kernel/bluesm.c`，显示了机器检查异常的通用处理程序。它在控制台上打印调试信息，并根据问题的严重程度，要么向下扩散（感染），要么继续。

```c
15 static int banks;
16 void intel_machine_check(struct pt_regs *regs, long error_code)
18 {
19 int recover=1;
20 u32 alow, aigh, high, low;
21 u32 mcgst, mcgsth;
22 int i;
23
24 rdmsr(MSR_IA32_MC_STATUS, mcgst, mcgsth);
25 if(mcgst&(1<<0))
26 recover=0;
28 printk(KERN_EMERG "CPU %d: Machine Check Exception:\n%08x%08x\n", smp_processor_id(), mcgst, mcgsth);
29
30 for(i=0;i<banks;i++)
31 {
32     rdmsr(MSR_IA32_MC0_STATUS+i*4,
```

**图 11.17** 机器检查异常的处理程序

`banks`的值在启动时设置。根据处理器的型号，有 4、5 或 6 组寄存器。

此变量中的位可能被设置，以指定在读取寄存器组时遇到的错误严重程度。然后将根据设置的位采取行动。这里的默认值被设置为不可恢复（位 0 被设置）。

`rdmsr()`宏从机器特定寄存器读取（见第 11.6.4 节）。在这里它从状态寄存器读取两个 32 位的值，该寄存器描述了机器检查异常发生后的 CPU 状态。高 32 位写入`mcgst`；低 32 位写入`mcgsth`。

25 此检查`mcgst&(1<<0)`，如果成立，则`recover`设置为 0。

28 `printk(KERN_EMERG "CPU %d: Machine Check Exception:\n%08x%08x\n", smp_processor_id(), mcgst, mcgsth);`

30 `for(i=0;i<banks;i++)`
31 {
32     `rdmsr(MSR_IA32_MC0_STATUS+i*4,`

（注：此处提供的原文文本似乎存在严重的乱码或逻辑重复错误，根据指令“不要重复输出原文”的原则，译文仅对具有逻辑语义的部分进行了翻译，但由于原文后半部分为无意义的重复碎片片段，译文已根据上下文逻辑进行处理。）

这是机器检查状态寄存器，它描述了发生机器检查异常后 CPU 的状态：

- 位 0 表示程序是否可以重启（1）或不可重启（0）。
- 位 2 表示生成了机器检查异常；此位可以由软件清除（并且已经由软件清除）。

这是 bank 0 的 bank 状态寄存器：

- 位 25 表示 CPU 上文是否已损坏（1）或未损坏（0）。
- 位 26 表示 bank 中的第三个寄存器是否有有效信息（1）或无（0）。
- 位 27 表示 bank 中的第四个寄存器是否有有效信息（1）或无（0）。
- 位 29 表示 CPU 是否已修正了错误（0）或未修正（1）。
- 位 31 是状态位；只有当此位被设置时，其他任何位才有效。

这是 bank 0 的`ADDR`寄存器。它可能包含产生机器检查错误的代码或数据内存地址。

这是 bank 0 的`MISC`寄存器。它可能包含描述机器检查错误的额外信息。

### 11.6.4 读取和写入特定特定寄存器

`<asm-i386/msr.h>`中提供了两个用于读取和写入特定寄存器的宏（见图 11）。

```c
#define rdmsr(msr,val1,val2) \
asm__volatile ("rdmsr" \
: "a" (val1), "-d" (val2) \
: "c" (msr))

#define wrmsr(msr,val1,val2) \
asm__volatile ("wrmsr" \
: :/ "no outputs" \
: "c" (msr), "a" (val1), "d" (val2))
```

**图 11** 读取和写入特定寄存器的宏

`RDMSR`从特定寄存器读取内容。要读取的寄存器由`ECX`中的值指定。特定寄存器的内容被复制到`EDX:EAX`。

此行指定了两个输出参数：映射到`EAX` ("a") 的`val1`，以及映射到`EDX` ("d") 的`val2`。

有一个输入参数`msr`，映射到`ECX` ("c")。

`WRMSR`指令写入特定寄存器。要写入的寄存器由`ECX`指定。要写入的值位于`EDX : EAX`中。

此宏没有输出参数。

此行指定了三个输入参数：映射到`ECX`的`msr`，映射到`EAX`的`val1`，以及映射到`EDX`的`val2`。

## 11.7 设备不可用

当在指令流中遇到浮点操作码且无法立即执行时，CPU 会产生此中断。出现这种情况有两种可能的原因：

- 未安装浮点协处理器。这非常罕见。它会发生在没有对应 387 浮点单元 (FPU) 的 386 上。操作系统通过打印警告消息并发送`SIGFPE`来处理这种情况。
- 这种中断更通常发生在 FPU 检测到其寄存器中的值无效时。这种情况是由于 Linux 上文切换器采用的懒加载策略导致的。

一级处理程序（第 10.5.2 节）检测到中断原因并调用了二级处理程序。现在将逐检查这些处理程序。

### 11.7.1 不存在浮点单元

如果`CR0`中的数学仿真位为 0，则没有 FPU 或数学仿真。在这种情况下，设备不可用异常的一级处理程序直接调用来自`arch/i386/kernel/traps.c`的图 11.20 所示的函数。它打印警告并向当前进程发送`SIGFPE`，因此该函数的名称相当具有误导性。

```c
void math_emulate(long arg)
{
    printf("math-emulation not enabled and no coprocessor found.\n");
    printf("killing %s.\n", current->comm);
    force_sig(SIGFPE, current);
    schedule();
}
```

图 11.20 因缺少浮点单元而杀死当前进程

尽管该函数实际上接收了一个参数，但它并没有使用它。

`task_struct`中的`comm`字段包含当前进程执行的程序名称。

第 18.2.7 节描述的`force_sig()`函数即使在进程已阻塞的情况下也会发送信号。

### 11.7.2 浮点单元寄存器无效

来自`arch/i386/kernel/traps.c`的图 11.21 所示的`math_state_restore()`函数处理了懒上文切换的情况。还有两种进一步的可能性：进程可能在执行的之前的某个阶段使用过 FPU，在这种情况下 FPU 寄存器的有效值存储在它的线程结构体中。

也可能是它之前没有使用过 FPU，在这种情况下必须为 FPU 寄存器加载初始值。这可能性将在随后的子节中处理。

```c
void math_state_restore(struct pt_regs *regs)
{
    asm volatile ("clts");
    if (current->flags & PF_USED) {
        restore_fpu();
    } else {
        init_fpu();
    }
    current->flags |= PF_USED_PU;
}
```

## 11.8 协处理器错误

协处理器错误（编号 16）意味着 FPU 中发生了上溢出或溢出等数值错误。该异常的处理分两个步骤进行。我们从二级处理程序开始，它是非常简单的。然后我们考虑实际执行工作的函数`math_error()`。

### 11.8.1 协处理器错误的二级处理程序

来自`arch/i386/kernel/traps.c`的图 11.22 显示了协处理器错误的简单二级处理程序。它实际上只是调用它的汇编例程与处理错误的函数之间的链接。

```c
mlinkage void do_coprocessor_error(struct pt_regs *regs, long error_code)
{
```
