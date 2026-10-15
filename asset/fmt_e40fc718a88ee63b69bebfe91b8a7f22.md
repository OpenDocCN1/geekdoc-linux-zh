
```c
if (ptrace(PTRACE_POKETEXT, pid, symaddr, trap) < 0) {
    perror("PTRACE_POKETEXT");
    exit(-1);
}

h.pt_reg.rip = h.pt_reg.rip + 1; // skip the instruction that caused the trap

if (ptrace(PTRACE_SETREGS, pid, NULL, &h.pt_reg) < 0) {
    perror("PTRACE_SETREGS");
    exit(-1);
}

if (ptrace(PTRACE_SINGLESTEP, pid, NULL, NULL) < 0) {
    perror("PTRACE_SINGLESTEP");
    exit(-1);
}

wait(NULL);

if (WIFEXITED(status)) {
    printf("Completed tracing: %d\n", pid);
    exit(0);
}
```

# Linux 进程追踪

使用 `./tracer`（版本 2），我们现在可以附加到一个已经在运行的进程，然后在所需的函数上设置断点并跟踪执行。这里有一个追踪一个使用 `print_string(char *s)` 循环打印 20 次 Hello 字符串程序的示例：

```
ryan@elfmaster:-$ ./tracer -p "pidof /test2" -f print_string
Beginning analysis of pid: 7075 at 4005bd
Executable ./test2 (pid: 7075) has hit breakpoint 0x4005bd
%rcx: fffffffffffffff
%rdx: 0
%rbx: 0
%rax: 0
%rdi: 4006a4
%rsi: 7ffff93670e0
%r8: 7ffff93671f0
%r9: 0
%r10: 8
%r11: 246
%r12: 4004d0
%r13: 7ffff93673b0
%r14: 0
%r15: 0
%rsp: 7ffff93672b8
nPlease hit any key to continue: c
Executable ./test2 (pid: 7075) has hit breakpoint 0x4005bd
%rcx: fffffffffffffff
%rdx: 0
%rbx: 0
%rax: 0
%rdi: 4006a4
%rsi: 7ffff93670e0
%r8: 7ffff93671f0
%r9: 0
%r10: 8
%r11: 246
%r12 4004d0
%r13 7ffe93673b0
%r14: 0
%r15: 0
%rsp: 7ffe93672b8
%C
Caught SIGINT: Detaching from 7452
```

因此，我们实现了一个简单的调试软件的编码，它既可以运行程序并对其进行追踪，也可以附加到现有进程并对其进行追踪。这展示了 `ptrace` 最常见的用例，而你使用的其他大多数使用 `ptrace` 的程序都是 `tracer.c` 代码中技术的变体。

## 高级函数追踪软件

在 2013 年，我设计了一个追踪函数调用的工具。它与 `strace` 和 `ltrace` 非常相似，它不是追踪 `syscalls` 或库调用，而是追踪从可执行文件发出的每一个函数调用。该工具在第 2 章 ELF 二进制格式中被介绍过，但它与 `ptrace` 主题相关。这是因为它完全依赖于 `ptrace` 并使用控制流监控执行了一些非常厉害的动态分析。源代码可以在 GitHub 上找到：

https://github.com/leviathansecurity/ftrace

## ptrace() 与取证分析

`ptrace()` 命令是常用于用户态内存分析的系统调用。事实上，如果你正在设计一个运行在用户态的取证软件，它访问其他进程的唯一方法是通过 `ptrace` 系统调用，或者通过读取 `proc` 文件系统（除非该程序设置了某种显式的共享内存 IPC）。

> 可能会附加到一个进程，然后通过打开/lseek/read/write `/proc/<pid>/mem` 作为 `ptrace` read/write 语义的替代方案。

## Linux 进程追踪

2011 年，我获得了 DARPA CFT（网络快速通道）计划的合同，设计了一个名为 Linux VMA Monitor 的工具。该软件的目的是检测各种已知和未知的进程内存感染，例如 rootkits 和内存驻病毒。

它本质上使用理解 ELF 执行的特殊启发式方法对每个进程执行自动化智能内存取证分析。它可以发现异常或寄生虫，例如被劫持的函数和通用代码感染。该软件可以分析内存作为主机入侵检测系统，也可以对进程内存快照进行分析。该软件还可以检测并消毒磁盘上感染病毒的 ELF 二进制文件。

`ptrace` 系统在该中被大量使用，并展示了围绕 ELF 二进制和 ELF 运行时感染的相关代码。我还没有发布源代码，因为我想在发布之前提供更接近生产环境的版本。在全文中，我们将涵盖 Linux VMA Monitor 可以检测/消毒几乎所有的感染类型，并讨论和演示用于识别这些感染的启发式方法。

十多年来，黑客一直将复杂的恶意软件隐藏在进程内存中以保持隐性。这可能是共享库注入和 GOT 破坏的结合，或者任何其他技术的组合。系统管理员发现这些内容的几率非常低，特别是因为没有多少公开的软件可以检测到许多此类攻击。

我发布了几个工具，包括但不限于 AVU 和 ECFS，可以在 GitHub 和我的网站 http://bitkeys.org/ 上找到。存在的任何其他此类软件要么是高度专业化且私下使用的，要么根本不存在。同时，一个优秀的取证分析师可以使用调试器或编写自定义软件来检测此类恶意软件，知道你在寻找什么以及为什么是非常重要的。由于本章完全关于 `ptrace`，我想强调的是它是如何与取证分析相互关联的。而且它确实如此，而且极其如此。

## Linux 进程追踪

### 进程的算法

让我们来看可执行文件的重构：

1. 定位可执行文件的基地址（文本段）。这可以通过解析 `/proc/<pid>/maps` 来完成：

[程序 'evil' 的 `/proc/<pid>/maps` 文件的第一行输出]

```
00400000-401000 r-xp /home/ryan/evil
```

使用 `ptrace` 配合 `PEEKTEXT` 请求来读取整个文本段。你可以从前面 `maps` 输出的某行中看到，文本段（标记为 `r-xp`）的范围是 `0x400000` 到 `0x401000`。因此，这就是你的文本段缓冲区应该有多大的原因。由于我们还没有介绍过如何使用 `PTRACE_PEEKTEXT` 一次读取超过 `long` 长度的数据，我写了一个名为 `pid_read()` 的函数，它演示了实现此操作的良好方法。

![](img/10a855ebad6fe689ed3447763aed6bf4_100_0.png)

```c
// pid_read() 函数的源代码
int pid_read(int pid, void *dst, const void *src, size_t len)
{
    unsigned sz = len / sizeof(void);
    unsigned char *s = (unsigned char *)src;
    unsigned char *d = (unsigned char *)dst;
    unsigned long word;
    while (sz!=0) {
        word = ptrace(PTRACE_PEEKTEXT, pid, (long *)s, NULL);
        if (word == -1)
            return 1;
        *(long *)d = word;
        s += sizeof(long);
        d += sizeof(long);
    }
    return 0;
}
```

2. 解析 ELF 文件头（例如 `Elf64_Ehdr`）以定位程序头表：

```c
/* 此处 buffer 是持有文本段的缓冲区 */
Elf64_Ehdr *ehdr = (Elf64_Ehdr *)buffer;
Elf64_Phdr *phdr = (Elf64_Phdr *) &buffer[ehdr->e_phoff];
```

3. 然后解析程序头找到数据段：

```c
for (c = 0; c < ehdr->e_phnum; c++) {
    if (phdr[c].p_type == PT_LOAD && phdr[c].p_offset) {
        dataVaddr = phdr[c].p_vaddr;
        dataSize = phdr[c].p_mems;
        break;
    }
}
pid_read(pid, databuff, dataVaddr, dataSize);
```

4. 将数据段读入缓冲区，并在其中定位动态段，然后从动态段找到 GOT 的 `d_tag` 并将其映射到 GOT：

> 我们在第 2 章《ELF 二进制格式》的动态链接部分讨论过动态段及其标签值。

```c
Elf64_Dyn *dyn;
for (c = 0; c < ehdr->e_phnum; c++) {
    if (phdr[c].p_type == PT_DYNAMIC) {
        dyn = (Elf64_Dyn *) &databuff[c].p_vaddr - dataAddr;
        break;
    }
}
if (dyn) {
    for (c = 0; dyn[c].d_tag != DT_NULL; c++) {
        switch (dyn[c].d_tag) {
            case DT_PLGOT:
                gotAddr = dyn[c].d_un.ptr;
                break;
            case DT_STRTAB:
                /* 获取 .dynstr */
                break;
            case DT_SYMTAB:
                /* 获取 .dynsym */
                break;
        }
    }
}
```

5. 一旦定位 GOT，必须恢复到运行之前的状态。最重要的部分是在每个 GOT 条目恢复原始 PLT 存根，延迟绑定在运行时工作。参见第 2 章《ELF 二进制格式》中的动态链接部分：

```
400300403e0 <puts@plt>:
4003e3: ff 25 32 00 20 jmp *0x2003(%rip)
4003e6: 68 00 00 00 ff
4003eb: e9 00 00 00 <init+x28>
```

6. 为 `puts()` 留出的 GOT 条目应该恢复指向栈的 PLT 存根。该地址 `0x4003e6` 在前面的命令给出。确定 GOT 到 PLT 方法的关系留给你练习。

7. 有时重构段头。然后将文本段和数据段（段头表）写入磁盘。

### Quenya 的进程重构

32 位 ELF 可执行文件只需打印 `You can Dump my segments!` 字符串，然后给我们时间重构它。现在，以下代码演示了 Quenya 将进程映像重构为可执行文件：

```
[Quenya v0.1@ELFWorkshop]
rebuild 2497 dumpme.out
+] analysis for reconstruction of process image (pid: 2497)
+] Getting Loadable segment...
+] Found loadable segments: text segment, data segment
Located PLT Vaddr 0x80400
Relevant GOT entries begin at 0x8040c
+] Resolved PLT: 0x804836
PLT Entries: 5
Patch #1 {0xb75f7040} changed to [0x8048346]
Patch #2 {0xb75a7190} changed to [0x8048356]
Patch #3 {0xb75a8366} changed to [0x8048366]
Patch #4 {0xb755a990} changed to [0x8048376]
+] Patched GOT by PLT stubs
Successfully rebuilt ELF object from memory
Output location: dumpme.out
[Quenya v0.1@ELFWorkshop]
quit
```

在这里，我们正在证明输出是正确的：
hacker@ELFWorkshop:/workshop/labs/exercise_9$ .dumpme.out
You can Dump my segments!

Quyena 也为可执行文件创建了最小的段头：
hacker@ELFWorkshop:/workshop/labs/exercise_9$ readelf -S dumpme.out

有七个段头，从偏移量 0x1118 开始，所示：

| | Name | Type | Addr | Off | Size | SRTAB | ES | Lk | Inf | Al |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| [0] | NULL | | 0xb804800 | 000000 | 000000 | | 0 | 0 | 0 | |
| [1] | interp | PROBITS | 0xb8048154 | 000154 | 000013 | AA | A | 0 | 0 | |
| [2] | text | PROBITS | 0xb8048000 | 000000 | 000658 | WA | AX | 0 | 0 | 15 |
| [3] | data | PROBITS | 0xb8049f08 | 000fe8 | 000120 | WA | | 0 | 0 | 4 |
| [4] | dynamic | DYNAMIC | 0xb8049f14 | 0001f4 | 0000e8 | WA | | 0 | 0 | 4 |
| [5] | has | SRTAB | 0xb8049f28 | 000028 | 000014 | WA | | 0 | 0 | |
| [6] | shstr | SRTAB | 0xb8049f28 | 000028 | 000014 | WA | | 0 | 0 | |

## Linux 进程追踪

```c
static inline volatile int evil_open(const char *path, unsigned long flags)
{
    long ret;
    asm __ volatile(
    "mov $0, %%rdi\n"
    "mov $1, %%rsi\n"
    "mov $2, %%rax\n"
    "syscall" : "g"(path), "g"(flags);
    ) asm("mov %%rax, %0" : "=r"(ret));
    return ret;
}
```

```c
static inline volatile void evil_map(void *addr, uint64_t len,
uint64_t prot, uint64_t flags, int64_t fd, uint64_t off)
{
    long mmap_fd = fd;
    unsigned long mmap_off = off;
    unsigned long mmap_flags = flags;
    unsigned long ret;
    asm __ volatile(
    "mov $0, %%rdi\n"
    "mov $1, %%rsi\n"
    "mov $2, %%rdx\n"
    "mov $3, %%r10\n"
    "mov $4, %%r8\n"
    "mov $5, %%r9\n"
    "mov $9, %%rax\n"
    "syscall" : "g"(addr), "g"(len), "g"(prot), "g"(flags),
    "g"(mmap_fd), "g"(mmap_off));
    ) asm("mov %%rax, %0" : "=r"(ret));
    return (void *)ret;
}
```

```c
uint64_t injection_code(void *vaddr)
{
```
