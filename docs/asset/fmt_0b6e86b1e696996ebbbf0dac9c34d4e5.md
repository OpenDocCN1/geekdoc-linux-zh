
> 图 11.29 加载 MXCSR 寄存器

59 `0xffbf` 是 `1111 1111 1011 1111`，这使得提供的值中的那 6 位被清零。这是在 Pentium 4 中引入的，尝试在任何其他类型的 CPU 上设置它将导致普通保护异常。

58 这将值从 `_mxcsr` 加载到 `MXCSR` 寄存器。

### 11.10.2.4 保存浮点单元寄存器状态

FPU 状态通过来自 `arch/i386/kernel/i387.c` 的图 11.30 中的函数保存到线程结构中。

```c
if ( cpu_has_fxsr ) {
    asm volatile("fxsave %0; fnclex"
          : "~m" (tsk->thread.i387.fsave));
} else {
    asm volatile("fnsave %0; fwait"
          : "~m" (tsk->thread.i387.fsave));
    tsk->flags &= ~PF_USEDFPU;
}

void save_init_fpu(struct task_struct *tsk) {
    __save_init_fpu(tsk);
    stts();
}
```

> 图 11.30 保存浮点寄存器值

46 此函数将来自 FPU 寄存器的值保存到指定 `task_struct` 的线程字段。

48 此检查 CPU 是否支持 `FXSAVE` 指令（见第 11.10.1 节）。

49 `FXSAVE` 指令保存 x87 状态，以及 MMX、XMM 和 `MXCSR` 寄存器的状态。信息被复制到参数 0，即进程的特定架构的线程结构，系统软件可以使用它。寄存器中的实际值不会被更改。`FNCLEX` 指令清空 FPU 状态字中的浮点异常标志位，而不检查错误情况。

52 对于其他 CPU，使用 `FNSAVE`。该指令将 x87 FPU 状态信息（包括数据寄存器）存储在线程中，系统软件可以使用它。它还像 `FINIT` 一样将 FPU 初始化为默认值。`FWAIT` 指令检查并处理挂起的未掩码 x87 FPU 异常。它不像通常那样等待下一条指令。

55 在所有情况下，我们都清空 `task_struct` 字段中的 `PF_USEDFPU` 位。寄存器已经保存，只要该位存在，它们在上下文切换时就不会被保存。

58–62 这是一个封装函数，调用了第 46 行的 `__save_init_fpu()` 并设置了 `CR0` 中的 `TS`。

61 此宏在第 11.10.2.6 节中描述，无论之前是否设置，都会设置 `CR0` 寄存器中的 `TS`。这允许通过仅在需要时交换 FPU 寄存器来加速上下文切换。每当发生上下文切换时，CPU 将其设置为 1。如果被设置为 1，FPU 指令将引发异常。这意味着随后的 FPU 指令将引发“设备不可用”（device not available）异常。理想情况下，如果发生这种情况，信号处理程序将修复线程结构中的保存值，因此“设备不可用”异常的处理程序将从那里重新加载。

### 11.10.2.5 恢复浮点单元寄存器值

图 11.31 来自 `arch/i386/kernel/i387.c` 显示了从当前进程的线程结构恢复 FPU 寄存器的函数。它不是每次上下文切换时都调用，而是在需要时调用。

```c
void restore_fpu(struct task_struct* tsk) {
    if (cpu_has_fxsr) {
        asm volatile("frstor%0")
            :: "m" (tsk->thread.i387.fsave));
    } else {
        asm volatile("frstor%0")
            :: "m" (tsk->thread.i387.fsave));
    }
}
```

> 图 11.31 恢复浮点单元寄存器

78 取决于 CPU 是否具有 `FXSAVE`，它从当前进程的线程结构恢复 FPU 寄存器。它不是每次上下文切换时都调用，而是在需要时调用。

78 它恢复 x87 状态，以及 MMX、XMM 和 `MXCSR` 寄存器的状态。信息被复制到参数 0，即进程的特定架构的线程结构，系统软件可以使用它。

### 11.10.2.6 操作 CR0 寄存器

定义了一些宏来操作 `CR0`。这些在 `<asm-i386/i387.h>` 中。

```c
#define stts() \
    unsigned long _dummy; \
    asm volatile("mov cr0, %0" : "=r" (_dummy)); \
    _dummy |= 0x0000002; \
    asm volatile("mov %0, cr0" : : "r" (_dummy))

#define clts() \
    unsigned long _dummy; \
    asm volatile("mov %0, %0" : : "r" (_dummy)); \
    _dummy &= ~0x0000002; \
    asm volatile("mov %0, cr0" : : "r" (_dummy))

#define readts() \
    unsigned long _dummy; \
    asm volatile("mov cr0, %0" : "=r" (_dummy)); \
    return (_dummy & 0x0000002)
```

> 图 11.32 操作 CR0（等待，OCR 文本在这里乱了，已根据逻辑流重新对齐）

### 用于协处理器错误处理的辅助函数

```c
if (!(regs->eflag & VM_MASK) && !(3 & regs->xcs))
    die(str, regs, errs);
}
```

> 图 11.35 在内核模式下杀死进程

第一个参数是指向错误字符串的指针；第二个参数是存储栈上保存寄存器的指针；第三个参数是错误代码，调用者的判断条件是（不在用户模式下）且（在内核模式下）。如果中断发生时进程处于用户模式或内核模式，则该函数将什么都不做并返回到错误处理程序。`die()` 函数打印一条消息并终止进程（见第 11.10.4 节）。

### 11.10.2 终止进程

图 11.36 显示了来自 `arch/i86/kernel/traps.c` 的打印信息并终止进程的函数。

```c
```
