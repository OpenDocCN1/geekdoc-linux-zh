
我使用了 Borland C/C++ V3.1 编译器配合 Borland Turbo 汇编器（Turbo Assembler）对 8086 端口进行了移植和测试。该编译器生成代码并提供可以插入 C 代码中的内联汇编指令。一旦编译后，代码将在 PC 上运行。我在运行微软 Windows 95 操作系统的奔腾 II 级计算机上测试了代码。事实上，我配置编译器生成一个在 DOS 环境下运行的可执行文件。

只要编译器能生成实模式（Real-Mode），该移植版本就可以运行。你可能需要更改一些编译器选项和汇编器指令。

# 9.01 目录与文件

发行版提供的安装程序将在你的硬盘上安装适用于 Intel 8086（实模式、大内存模型）的端口。该端口位于驱动器的 `\SOFTWARE\uCOS-II\x86L` 目录下。该目录名称代表 Intel 8086 实模式大内存模型。该端口的源代码位于以下文件夹中：`OS_CPU`、`OS_CPU_C_C` 和 `OS_CPU_ASM`。

# 9.02 INCLUDES.H

`INCLUDES.H` 是一个主文件（MASTER file），位于所有 `.C` 文件的顶部。`INCLUDES.H` 允许每个 C 文件在编写时无需担心将包含哪个头文件。拥有主包含文件的唯一缺点是，`INCLUDES.H` 可能会包含与实际正在编译的 C 文件不相关的头文件。这意味着每个文件将需要额外的时间来编译。这种不便被代码的可移植性所抵消。你可以编辑 `INCLUDES.H` 来添加你自己的头文件，但你的头文件应该添加到列表末尾。列表 9.1 显示了 8086 端口 `INCLUDES.H` 的内容。

```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <stdlib.h>
#include <conio.h>
#include <dos.h>
#include <setjmp.h>

#include "software/ucos-ii/ix86/os_cpu.h"
#include "os_cfg.h"
#include "software/blocks\pc\source\pc.h"
#include "software/ucos-ii/source/ucos_li.h"
```

# 列表 9.1，常量

# 9.03 OS_CPU.H

`OS_CPU.H` 包含了针对处理器和实现的特定的**定义**常量、宏和类型定义（`typedef`）。

80x86 端口的 `OS_CPU.H` 见列表 9.2。

```c
#ifdef OS_CPU_GLOBALS
#define OS_CPU_EXT
#else
#define OS_CPU_EXT external
#endif

************************************************************************************
/*
                               数据类型
                               (编译器特定)
*/
************************************************************************************

typedef unsigned char  BOOLEAN;    / 无符号 8 位量
typedef unsigned char  INT8U;
typedef signed char     INT8;       / 有符号 8 位量
typedef unsigned int    INT16;      / 无符号 16 位量
typedef signed int      INT16;      / 有符号 16 位量
typedef unsigned long   INT32;      / 无符号 32 位量
typedef signed long     INT32;      / 有符号 32 位量
typedef float          FFT32;      / 单精度浮点
typedef double         FFT64;      / 双精度浮点

typedef unsigned int    OS_STK;     / 每个条目宽度为 16 位

#define BYTE               INT8;       / 用于 UC/xx 的后兼容类型
#define WORD               INT16;      / 实际上不需要
#define LONG               INT32;      / ...
#define ULONG              INT32;      // UC/OS-II.
************************************************************************************
OS_CRITICAL_METHOD   = 1

- *方法 #1：使用简单的禁用/启用中断。在临界区后，中断将被启用。你必须将 `OS_CPU_A.ASM` 中的常量 `OSCtx()` 从 10 改为 8。*
- *方法 #2：通过保存中断状态来禁用/启用中断。也就是说，如果在进入临界区之前禁用了中断，在离开临界区时它们将被禁用。你必须将 `OS_CPU_A.ASM` 中的常量 `OS Cw()` 从 8 改为 10。*
```

```c
************************************************************************************

OS_CRITICAL_METHOD   = 1

#if

#define OS_ENTER_METHOD() asm CLI      / 禁用中断

(2)

#define OS_EXIT_CRITICAL()  asm STI      / 启用中断

#endif
```

```c
#if OS_CRITICAL_METHOD == 2

#define OS_ENTER_CRITICAL() asm (PUSH, CLI)  /* 禁用中断 */

#define OS_EXIT_CRITICAL()    asm POPF               /* 启用中断 */

#endif
```

```c
************************************************************************************

Intel 8086（实模式，大内存模型）杂项

************************************************************************************

/*

(3)    OS_STK_GROWTH      1       /* 8086 上从高向低增长 */

(4)    uCOS               0x80    /* 用于上下文切换的中断向量 */

(5)    OS_TASK_SW()        asm     

OS_CPU_EXT  TickCtr;      /* 每 n 个 tick 调用 DOS 的计数器 */

(6)
```
