
在操作数部分中，`a`、`b`、`c`、`d`、`S` 和 `D` 分别代表 `EAX`、`EBX`、`ECX`、`EDX`、`ESI` 和 `EDI` 寄存器。输入操作数约束在执行汇编指令之前将数据从提供的变量复制到指定的寄存器，而输出操作数约束（写成 `=a`, `=b` 等）在执行汇编指令之后将数据从指定的寄存器复制到提供的变量。被破坏的操作数约束要求 `GCC` 假设列出的寄存器不可用。有关 `GCC` 内联汇编语法的更多详细信息，请参阅 `GCC` 内联汇编 `HOWTO` (`www.ibiblio.org/gferg/ldp/GCC-Inline-Assembly-HOWTO.html`)。

我们在示例中使用的 `a` 约束是特定于输入操作数的。这有效地将 `data` 的值复制到 `AL` 寄存器，将 `port` 的值复制到 `DX` 寄存器。在内联汇编中，寄存器名前带有 `%`，因为 `%` 用于引用提供的操作数。`%i` 代表第 `i` 个操作数；因此，如果你想在示例内联汇编片段中引用 `data` 和 `port`，你可以分别使用 `%0` 和 `%1`。

为了更清楚地了解内联汇编转换，让我们查看由编译器生成的对应于前面内联汇编片段的汇编代码，通过向 `GCC` 提供 `-s` 命令行参数。查看每行生成代码中的注释以了解解释：

```assembly
movw  $956,    -2(%ebp)  # 堆栈中 data 的值设置为 0x3BC
movb  $-85,    -3(%ebp)  # 堆栈中 port 的值设置为 0xAB
movb  -3(%ebp), %al     # movb 0xAB, %al
movw  -2(%ebp), %dx     # movw 0x3BC, %dx
#APP
outb  %al,  %dx         # 写入并行口
#NO_APP
```

你也可以从用户模式程序中使用内联汇编。这是一个使用内联汇编编写的应用程序，它调用 `syslog()` 系统调用从内核 `printk()` 环形缓冲区读取最后 128 字节：

```c
#define READ_COMMAND      3     /* syslog() 系统调用的第一个参数 */
#define MSG_LENGTH        128   /* syslog() 的第三个参数 */
```

```c
int
main(int argc, char *argv[]) {
  int syslog_command = READ_COMMAND;
  int bytes_to_read = MSG_LENGTH;
  int retval;
  char buffer[MSG_LENGTH]; /* syslog() 的第二个参数 */
  asm volatile(
    "movl $1, %%ebx\n"  /* READ_COMMAND */
    "movl %2, %%ecx\n"  /* buffer */
    "movl $3, %%edx\n"  /* bytes_to_read */
    "movl $103, %%eax\n"  /* __NR_syslog */
    "int $128\n"  /* 生成系统调用 */
    "movl %%eax, %0"  /* retval */
    :"=m" (retval)
    :"m" (syslog_command), "r" (buffer), "m" (bytes_to_read)
    :"eax", "ebx", "ecx", "edx");
  if (retval > 0) printf("%s\n", buffer);
}
```

正如你在**第 4 章**“奠定基础”中所学到的，`int $128`（或 `int 0x80`）指令会产生一个软件中断，从而陷入系统调用。由于系统调用会导致从用户模式到内核模式的转换，函数参数不是通过用户栈或内核栈传递的，而是通过 CPU 寄存器传递的。系统调用编号（`include/asm-your-arch/unistd.h` 包含完整列表）存储在 `EAX` 寄存器中。对于 `syslog()` 系统调用，此编号为 103。如果你查看 `syslog()` 的手册页，你会发现它接受三个参数：命令、用于保存返回数据的缓冲区地址以及缓冲区的长度。这些参数分别通过寄存器 `EBX`、`ECX` 和 `EDX` 传递。返回值从 `EAX` 转移到 `retval`。内联汇编调用有效地转换为此代码：

```c
retval = syslog(syslog_command, buffer, bytes_to_read);
```

如果你编译并运行该代码，你将看到如下输出，从内核环形缓冲区获取：

```text
0:0:0:0: Attached scsi removable disk sda
<Snd 0:0:0:0: Attached scsi generic sg0 type 0
<7>usb-storage: device scan complete
...
```

`arch/x86/kernel/entry_32.S` 中的内核系统调用陷阱将所有寄存器内容保存到堆栈中，因此即使用户空间代码通过 CPU 寄存器传递参数，真正的系统调用也在堆栈中看到其参数。为了确保系统调用例程期望在堆栈上接收参数，它们都被标记为 `GCC` 属性 `asmlinkage`。请注意，`asmlinkage` 与用于声明内联汇编的 `asm`（或 `__asm__`）没有任何关系。

让我们通过展示修改基于 PowerPC 主板的 Linux 引导加载程序的示例来结束本节。假设主板上的闪存不支持**后台操作**（BGO）。这意味着引导加载程序代码不能在执行时写入闪存，而这对于例如引导加载程序需要更新驻留在闪存另一部分的内核映像的情况是必需的。一种解决方案是修改引导加载程序，使用于写入和擦除闪存的启动代码完全从*指令缓存*（I-cache）中执行，而数据段驻留在*数据缓存*（D-cache）中。示例

## 调试

要调试实模式内核，你无法使用我们在第 21 章“调试设备驱动程序”中讨论的调试器，例如内核调试器（`kdb`）或内核 `GNU` 调试器（`kgdb`）。一种快速调试内核汇编代码片段的方法是将代码转换为 Intel 风格语法后，使用 `DOS` 调试工具。但是，由于 `debug` 工具是在 16 位时代创建的，因此你无法执行某些操作，例如单步执行初始化 `RAX` 寄存器的代码。你可以在互联网上找到可下载的 32 位调试类免费工具。第 21 章中讨论的 `JTAG` 调试器是一种万能工具，因为单一工具即可用于调试 `BIOS`、引导加载程序、Linux 实模式代码以及内核与 `BIOS` 之间的交互。

## 附录 B. Linux 与 BIOS

`x86` 内核的部分组件，如视频帧缓冲驱动程序（`vesafb`）和高级电源管理（`APM`），显式地使用 `BIOS` 服务来实现特定功能。内核的其他部分，如串行驱动程序，则隐式地依赖 `BIOS` 来初始化 I/O 基址和中断级别。实模式内核代码在启动期间大量使用 `BIOS` 调用来执行诸如组装系统内存映射等任务。[1] 由于某些设备驱动程序直接或间依赖于 `BIOS`，因此让我们学习如何与其交互。

[1] 在无 `BIOS` 的嵌入式架构中，类似的责任（例如在 `ARM` Linux 上从挂起状态唤醒内核）由引导加载程序承担。

### 实模式调用

内核的许多部分在实模式下从 `BIOS` 获取信息，并在保护模式的正常运行期间使用收集到的信息。

实现此目标所需的步骤如下：

- 1. 实模式内核代码调用 `BIOS` 服务，并将返回的信息填充到第一个物理内存页中，该页称为零页（zero page）。这是通过 `arch/x86/boot/` 目录中的源文件完成的。零页的完整布局可在 `Documentation/i386/zero-page.txt` 中找到。
- 2. 在内核切换到保护模式之后、清除零页之前，获取的数据会被保存到内核数据结构中。这是在 `arch/x86/kernel/setup_32.c` 中完成的。
- 3. 保护模式内核在正常运行期间适当地利用已保存的信息。

作为一个示例，让我们了解一下内核如何从 `BIOS` 组装系统内存映射。清单 B.1 是从 2.6.23.1 源码树中的 `arch/x86/boot/memory.c` 中截取的一段代码，它调用了 `BIOS` 的 `int 0x15` 服务以获取系统内存映射。

### 清单 B.1. 获取系统内存映射（`arch/x86/boot/memory.c`）

```c
static int detect_memory_e820(void)
{
    int count = 0;
    u32 next = 0;
    u32 size, id;
    u8 errr;
    /* The boot_params structure contains the zero page */
    struct e820entry *desc = boot_params.e820_map;
    do {
```
