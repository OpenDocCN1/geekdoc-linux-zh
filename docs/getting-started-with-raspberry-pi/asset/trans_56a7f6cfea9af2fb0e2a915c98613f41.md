

```
kdb> ld rs_open
0xc01cce00 rs_open:  sub     $0x1c, %esp
0xc01cce03 rs_open+0x03:    mov     $ffffffed, %ecx
...
0xc01cce4b rs_open+0x4b:    call    0xc01ccca0, get_async_struct
...
0xc01cce56 rs_open+0x56:    mov     0xc(%esp,1), %eax
0xc01cce5a rs_open+0x5a:    mov     %eax, 0x9a4(%ebx)
...
```

源代码中的 A 点是一个设置断点的理想位置，因为你可以观察 `tty` 结构和 `info` 结构，以了解正在发生什么。

并排查看源代码和反汇编代码，可以看到 `rs_open+0x5a` 对应于 A 点。注意，如果内核是在未启用优化标志的情况下编译的，这种对应关系的查找会更简单。

在 `rs_open+0x5a`（即地址 `0xc01cce5a`）处设置断点，并通过退出调试器继续执行：

```
kdb> bp rs_open+0x5a → 设置断点
kdb> go → 继续执行
```

现在你需要让内核调用 `rs_open()` 以触发断点。为此，执行一个适当的用户空间程序。在这种情况下，向对应的串行端口（`/dev/ttySX`）回显一些字符：

```
bash> echo "kerala monsoons" > /dev/ttySX
```

这将导致调用 `rs_open()`。断点被触发，kdb 获取控制权：

```
Entering kdb on processor 0 due to Breakpoint @ 0xc01cce5a
kdb>
```

现在我们来看看 `info` 结构的内容。如果你查看反汇编代码，在断点之前的一条指令（`rs_open+0x56`）处，你会发现 EAX 寄存器包含 `info` 结构的地址。让我们查看寄存器的内容：

```
kdb> r → 转储寄存器内容
eax = 0xc1fae680 ebx = 0xce03b000 ecx = 0xc1fae680
...
```

因此，`0xc1fae680` 是 `info` 结构的地址。使用 `md` 命令转储其内容：

```
kdb> md 0xc1fae680 → 内存转储
0xc1fae680 00005301 0000ABC 00000000 10000400
...
```

为了理解这个转储结果，让我们看看对应的结构定义。`info` 在 `include/linux/serialP.h` 中定义为 `struct async_struct`，如下所示：

```
struct async_struct {
    int           magic;    /* 魔数 */
    unsigned long port;     /* I/O 端口 */
    int           hub6;
    /* ... */
};
```

如果你将转储内容与定义进行匹配，`0x5301` 是魔数，而 `0xABC` 是 I/O 端口。哎呀，这很有趣！`0xABC` 看起来不像是一个有效的端口。如果你做过足够的串行端口调试，就会知道对于基于 x86 的硬件，I/O 端口基址和 IRQ 是在 `include/asm-x86/serial.h` 中配置的。将端口定义更改为正确的值，重新编译内核，并继续你的测试！

# 内核 GNU 调试器 (kgdb)

Kgdb 是一个源代码级调试器。它比 kdb 更容易使用，因为你不必花时间将汇编代码与源代码进行对应。然而，设置起来更困难，因为需要一台额外的机器来作为调试的前端。

你必须同时使用 gdb 和 kgdb 来单步执行内核代码。gdb 运行在主机上，而打了 kgdb 补丁的内核（请参阅“下载”部分以获取下载 kgdb 补丁的信息）运行在目标硬件上。主机和目标通过串行直通电缆（null-modem cable）连接，如图 21.1 所示。[1]

[1] 你还可以通过以太网启动 kgdb 调试会话。

![](img/07cc6f9c8c74622020874f66bfb53dc4_558_0.png)

你必须在内核命令行参数中告知内核串行端口的身份和波特率。根据使用的引导加载程序，将以下内核参数添加到 `syslinux.cfg`、`lilo.conf` 或 `grub.conf` 中：

```
kgdbwait kgdb8250=x,115200
```

`kgdbwait` 要求内核等待直到与主机侧的 gdb 建立连接，`x` 是连接到主机的串行端口，而 `115200` 是用于通信的波特率。

现在在主机侧配置相同的波特率：

```
bash> stty speed 115200 < /dev/ttySX
```

如果主机计算机是一台没有串行端口的笔记本电脑，你可以使用 USB 转串行转换器来进行调试会话。在这种情况下，请使用 usbserial 驱动程序创建的 `/dev/ttyUSBX` 节点，而不是 `/dev/ttySX`。第 6 章“串行驱动程序”中的图 6.4 说明了这种场景。

让我们通过一个有缺陷的内核模块示例来学习 kgdb 的基础知识。模块更容易调试，因为代码更改后无需重新编译整个内核，但请记住在编译模块时使用 -g 选项以生成符号信息。由于模块是动态加载的，调试器需要获知模块包含的符号信息。清单 21.1 包含一个有缺陷的 `trojan_function()`。假设它定义在 `drivers/char/my_module.c` 中。

# **清单 21.1. 有缺陷的函数**

```
char buffer;

int
trojan_function()
{
    int *my_variable = 0xAB, i;

/* ... */
Point A:
i = *my_variable;  /* 内核恐慌；my_variable 指向
                    无效的内存 */
return(i);
}
```

将 `my_module.ko` 插入目标系统，并查看 `/sys/module/my_module/sections/` 以解读 ELF（可执行文件和链接格式）段地址。[2] ELF 文件中的 .text 段包含代码，.data 包含已初始化的变量，.rodata 包含已初始化的只读变量（如字符串），而 .bss 包含启动期间未初始化的变量。如果在内核配置中启用 `CONFIG_KALLSYMS`，这些段的地址会以 `.text`、`.data`、`.rodata` 和 `.bss` 文件的形式位于 `/sys/module/my_module/sections/` 目录下。例如，要获取代码段的地址，请执行以下操作：

> [2] 如果你仍然在使用 2.4 内核，请使用 insmod 的 -m 选项代替来获取段地址：

```
bash> insmod my_module.o -m
Using /lib/modules/2.x.y/kernel/drivers/char/my_module.o
Sections:    Size     Address     Align
.this        00000060  e091a000   2**2
.text        00001ec0  e091a060   2**4
...
.rodata      0000004c  e091d1fc   2**2
.data        00000048  e091d260   2**5
.bss         000000e4  e091d2c0   2**5
...
```

```
bash> cat /sys/module/my_module/sections/.text
0xe091a060
```

更多的模块加载信息可以从 `/proc/modules` 和 `/proc/kallsyms` 中获取。

获取段地址后，在主机侧机器上启动 gdb：

```
bash> gdb vmlinux                 ➔ vmlinux 是非压缩的内核

(gdb) target remote /dev/ttySX  ➔ 连接到目标
```

由于你将 `kgdbwait` 作为内核命令行参数传入，当目标上的内核启动时，gdb 将获取控制权。现在使用 `add-symbol-file` 命令告知 gdb 上述的段地址：

```
(gdb) add-symbol-file drivers/char/mymodule.ko 0xe091a060
      -s .rodata 0xe091d1fc -s .data 0xe091d260 -s .bss 0xe091d2c0

add symbol table from file "drivers/char/my_module.ko" at
    .text_addr = 0xe091a060
    .rodata_addr = 0xe091d1fc
    .data_addr = 0xe091d260
    .bss_addr = 0xe091d2c0
(y or n) y
Reading symbols from drivers/char/my_module.ko ...done.
```

为了调试内核恐慌，让我们为 `trojan_function()` 设置一个断点：

```
(gdb) b trojan_function           ➔ 设置断点
(gdb) c                           ➔ 继续执行
```

当 kgdb 触发断点时，让我们查看堆栈跟踪，单步执行直到 A 点，并显示 `my_variable` 的值：

```
(gdb) bt                          ➔ 回溯（堆栈）跟踪
#0 trojan_function () at my_module.c :124
#1 0xe091a108 in my_parent_function (my_var1=438, my_var2=0xe091d288)
...

(gdb) step                        
➔ 继续单步执行直到
A 点
(gdb) p my_variable
$0 = 0
```

这里有一个明显的 bug。`my_variable` 指向 NULL，因为 `trojan_function()` 忘记为它分配内存了。让我们使用 kgdb 直接分配内存，绕过内核崩溃，并继续测试：

```
(gdb) p &buffer                  ➔ 打印 buffer 的地址
$1 = 0xe091a100 ""
(gdb) set my_variable=0xe091a100 ➔ my_variable = &buffer
```

