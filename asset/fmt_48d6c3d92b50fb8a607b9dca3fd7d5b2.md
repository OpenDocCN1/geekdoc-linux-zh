
图 6.21 获取读取信号量

`LOCK_PREFIX` 宏在第 5.1.4.2 节定义。在多处理器上，它求值得到 `LOCK` 指令，为 `INCL` 指令锁定总线，使其具有原子性。在单处理器上它是一个空操作，指令是原子的。读取者总是增加信号量的值，无论是否需要等待。这种增加意味着默认路径（无锁路径）尽可能短。信号量结构体的指针在 `EAX` 寄存器中（参见第 119 行）。当前行利用了 `count` 字段位于

在信号量结构中，`EAX` 实际上指向计数器（`count`）。`EFLAGS` 寄存器中的符号位设置取决于加法操作的结果。

- 103 如果最高位为 1，则信号量被写者持有，控制跳转到标签 2：第 109 行。由于下一块代码被编译到不同的子节（`subsection`），如果最高位为 0，控制流向汇编代码的末尾并结束函数，此时调用者持有信号量。
- 105–115 这段代码的频率通常比之前的几行低，被编译到子节 1 中。这是为了节省缓存空间而进行的优化。
- 106–108 这些行是给汇编器使用的。`__stringify()` 宏将内核构建版本号（例如 2.4.18）转换为字符串。然后，如果 `_text_lock_buildnumber` 标签不存在，则将其放置在此处的代码中供汇编器使用：注意第 107 行末尾的冒号，表示标签定义。插入此标签有助于调试内核代码。
- 110–111 这些寄存器将被第 112 行调用的例程使用，因此它们被保存并在第 113–114 行恢复。
- 112 该例程如第 6.2.4.2 节所述，调整计数字段并安排进程睡眠。它期望在 `EAX` 寄存器中接收参数。只有当进程获取信号量后它才会返回。
- 113–114 这些行移除了第 110–111 行推入栈中的值。
- 115 在此阶段，进程已获取信号量：它返回主程序代码并退出函数。
- 116 从这里开始的代码被编译到主节（`main section`）。
- 118 此输出参数可能在内存中。`"+"` 表示该操作数被 `INCL` 指令同时读和写。
- 119 此输入参数指针 `sem` 必须在 `EAX` 寄存器中，即 "a"。
- 120 `"memory"` 操作数意味着内存可能会以不可预测的方式被修改。`"cc"` 警告汇编器 `EFLAGS` 寄存器可能会被 `INCL` 指令所改变。

### 6.2.3.2 获取写入信号量

图 6.22 中的函数使用了 `<asm-1386/rwsem.h>`，尝试获取一个读写信号量用于写入。如果任何其他进程（读者或写者）持有该信号量，则调用进程将被置睡眠。

```
static inline void __down_write(struct rw_semaphore *sem)
{
    int tmp;

    tmp = RWSEM_ACTIVE_WRITE_BIAS;
```
```
__asm_volatile_(
"# beginning_down_write\n\t"
LOCK_PREFIX "xadd 	%%0,(%ax)\n\t"
testl 	%%0,0\n\t"
njz 	2f\n\t"
"1:\n\t"
".subsection1\n"
"#ifndef_text_lock__ __stringify(KBUILD_BASENAME) \\n"
_text_lock__ __stringify(KBUILD_BASENAME) : \\n"
".endif\n\t"
"2:\n\t"
pushl 	%%ecx\n\t"
call 	rwsem_down_write_failed\n\t"
popl 	%%ecx\n\t"
jmp 	1b\n\t"
".subsection0\n\t"
"# ending_down_write"
:d+(tmp), "+(sem->count)
:a(sem)
:memory,"cc";
}
```

**图 6.22** 获取写入信号量

局部变量 `tmp` 被初始化为 1 – 00010000，即 FFFF 0001，这表示有一个活跃锁和一个活跃写者。

`LOCK_PREFIX` 宏在第 5.1.4.2 节中定义。在多处理器上，它求值为 `LOCK` 机器指令，锁定总线供随后的 `XADD` 指令使用，使其原子化。在单处理器上它是 NULL，使指令原子化。`XADD` 的第一个参数是 `tmp`（第 148 行）；第二个是信号量结构本身的 `count` 字段。该指令交换值，旧值放入 `tmp`，并将两者的和放入 `count`，因此它增加了总请求数（在 `count` 的低半部分），同时也增加了 `count` 的（负）高位。

为了授予写入权限，`count` 之前必须为 0（即没有读者和写者）。局部变量 `tmp` 拥有 `count` 的旧值，因此在与其比较时，如果值为 0，它将设置 `EFLAGS` 中的零标志位。

如果上一行的测试结果不为 0，则跳转到标签 2：第 141 行。否则，这段代码被编译到不同的节，控制流向汇编代码的末尾并结束函数，调用者持有信号量。在这种情况下，`count` 字段的值始终为 FFFF0001。

这段代码的频率通常比之前的几行低，被编译到子节 1。这是为了节省缓存空间而进行的优化。

参见 6.2.3.1 节的第 106–108 行。

- 142 该寄存器将被第 143 行的例程使用，因此在此保存并在第 144 行恢复。
- 143 该例程如第 6.2.4.3 节所述，调整计数字段并安排进程等待信号量。它期望在 `EAX` 寄存器中接收参数。只有当进程获取信号量后它才会返回。
- 145 返回主程序代码并退出函数。
- 146 从这里开始的代码被编译到主节。
- 148 此输出参数可能在内存中。`"+"` 表示该操作数被 `INCL` 指令同时读和写。
- 149 此输入参数指针 `sem` 必须在 `EAX` 寄存器中，即 "a"。
- 150 `"memory"` 操作数意味着内存可能会以不可预测的方式被修改。`"cc"` 警告汇编器 `EFLAGS` 寄存器可能会被 `INCL` 指令所改变。

### 6.2.3.3 释放信号量

图 23 中的函数使用了 `<asm-1386/rwsem.h>`，尝试获取一个读写信号量用于写入。如果任何其他进程（读者或写者）持有该信号量，调用进程将被置睡眠。

```
static inline void __up_read(struct rw_semaphore *sem)
{
    int tmp;

    tmp = RWSEM_ACTIVE_READ_BIAS;
```
```
__asm_volatile_(
"# beginning_up_read\n\t"
LOCK_PREFIX "xadd 	%%0,(%ax)\n\t"
testl 	%%0,0\n\t"
njz 	2f\n\t"
"1:\n\t"
".subsection1\n"
"#ifndef_text_lock__ __stringify(KBUILD_BASENAME) \\n"
_text_lock__ __stringify(KBUILD_BASENAME) : \\n"
".endif\n\t"
"2:\n\t"
pushl 	%%ecx\n\t"
call 	rwsem_up_read_failed\n\t"
popl 	%%ecx\n\t"
jmp 	1b\n\t"
".subsection0\n\t"
"# ending_up_read"
:d+(tmp), "+(sem->count)
:a(sem)
:memory,"cc";
}
```
