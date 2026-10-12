
/******************************************************************

 *                                     INCLUDES.H

 ******************************************************************

*/

```c
#include <STDIO.H>

#include <STRING.H>

#include <TYPE.H>

#include <STDLIB.H>
```

```c
#include <CONIO.H>

#include <DOS.H>

#include "SOFTWARE\uCOS-II\IX86L\OS_CPU.H"

#include "OS_CFG.H"

#include "SOFTWARE\uCOS-II\SOURCE\uCOS_II.H"
```

列表 10.2，`\C/OS-II INCLUDES.H`

## 10.02 OS_CPU.H

`OS_CPU.H` 包含了特定于实现的 `#define` 常量、宏和 `typedef`。

### 10.02.01 OS_CPU.H，编译器特定类型

为了满足 `\C/OS-II`，我们需要创建六种数据类型：`INT8U`、`INT8S`、`INT16U`、`INT16S`、`INT32U` 和 `INT32S`。它们分别对应无符号和符号的 8、16 和 32 位整数。在 `\C/OS-II` 中，声明的类型是 `UBYTE`、`BYTE`、`UWORD` 和 `LONG`。你只需创建 `\C/OS` 数据类型，并如列表 10.3 所示，将 `UBYTE` 改为 `INT8U`，将 `BYTE` 改为 `INT8S`，将 `UWORD` 改为 `INT16U`。

```
* uC/OS 数据类型:
type unsigned char UBYTE; // 无符号 8位
type char BYTE;         // 有符号 8位
type unsigned int WORD; // 无符号 16位
type int WORD;          // 有符号 16位
type unsigned long LONG;  // 无符号 32位
type long LONG;         // 有符号 32位
* uC/OS-II 数据类型:
type unsigned char INT8U; // 无符号 8位
type char INT8S;        // 有符号 8位
type unsigned int INT16U; // 无符号 16位
type int INT16S;       // 有符号 16位
type unsigned long INT32U; // 无符号 32位
type long INT32S;        // 有符号 32位
```

列表 10.3，μC/OS 和 μC/OS-II 数据类型

μC/OS 的处理器特定代码（即端口）被放在文件名包含处理器名称的文件中。例如，Intel 80x86 实模式模型具有名为 `Ix86L.H`、`Ix86L_C.C` 和 `Ix86L_A.ASM` 的文件。表 10.1 显示了文件名称与旧名称的对应关系。

μC/OS 的处理器特定代码（即端口）被放在文件名包含处理器名称的文件中。

*(此处已去重复内容)*

```
将栈指针保存到 OSTCBur->OSTCBStkPtr；
调用 OSTTaskSwHook();
OSTCBur = OSTCBighRdy;
OSPrioCur = OSPrioHighRdy;
将栈指针加载为 OSTCBighRdy->OSTCBStkPtr；
从栈中弹出所有处理器寄存器；
执行中断返回（Return from Interrupt）指令；
```

列表 10.8，`OSIntCtxSw()` 的伪代码

### 10.03.04 OS_CPU_AASM, OSTickISR()

μC/OS 中此函数的代码与 μC/OS 相同，不应被修改。

### 10.04 OS_CPU_C.C

```
OSTTaskStkInit()
OSTTaskCreateHook()
OSTTaskDelHook()
OSTTaskSwHook()
OSTTaskStatHook()
OSTimeTickHook()
```

一个 μC/OS-II 移植层要求你编写六个简单的函数：

唯一真正需要的函数是 `OSTTaskStkInit()`……其他函数必须声明，但内部不应包含任何代码。

#### 10.04.01 OS_CPU_C.C, OSTTaskStkInit()

在 μC/OS 中，`OSTTaskCreate()` 被认为是一个特定特定的函数。事实证明只有 `OSTTaskCreate()` 的部分实际上是特定特定的。这部分已从 `OSTTaskCreate()` 中提取出来并放在新函数 `OSTTaskStkInit()` 中。

`OSTTaskStkInit()` 只负责设置栈指针，看起来就像发生了中断，并且所有处理器寄存器都推到了任务栈上。列表 10.9 显示了 Intel 806 真实模型的 μC/OS `OSTTaskCreate()` 代码逻辑。列表 10.10 显示了同一处理器用于 μC/OS 的 `OSTTaskStkInit()` 代码。通过对比这两行，你可以看到 L10.9(2) L10.9(18) 已从 `OSTTaskCreate()` 中提取并放入 `OSTTaskStkInit()` 中。换句话说，`OS_EXIT_CRITICAL()` L10.9(1) 和调用 `OSTCBInit()` 之后的所有内容都已移动到 `OSTTaskStkInit()`。

你会注意到 μC/OS-II 的代码使用了新的数据类型（参见节 10.02.01，OS_CPU.H，编译器特定数据类型）。不要将所有处理器寄存器初始化为 0x0000，而是使用一个可以让调试稍微容易一点的值初始化它们。你应该注意当任务不是关键状态时寄存器的初始值。

```
UBYTE OSTTaskCreate(void *task, void *pd, void *pdata, void *pstk, UBYTE
{
UWORD OS_FAR *stk;
UBBYTE
  err;
OS_ENTER_CRITICAL();
if (OSTCBrioTbl[p] == (OS_TCB *) 1) {
  OSTCBrioTbl[p] = (OS_TCB *);
  OS_EXIT_CRITICAL();
  stk = (UWORD OS_FAR *)pstk;
  *-stk = (UWORD FP_OFF (pdata));
  *-stk = (UWORD FF_SEG (task));
  *-stk = (UWORD) FF_OFF (task));
  *-stk = (UWORD) 0x0202;
  *-stk = (UWORD) FF_SEG (task));
  *-stk = (UWORD) FF_OFF (task));
  *-stk = (UWORD) 0x0000;
  *-stk = (UWORD) 0x0000;
  *-stk = (UWORD) 0x0000;
  *-stk = (UWORD) 0x0000;
  *-stk = (UWORD) 0x0000;
  *-stk = (UWORD) 0x0000;
  *-stk = (UWORD) 0x0000;
  *-stk = (UWORD) 0x0000;
  *-stk = (UWORD) 0x0000;
  *-stk = NULL;
  err = OSTCBInit(p, (void *)pstk);
  if (err == OS_NO_ERR) {
    if (OSRunning) {
      OSSched();
    }
  } else {
    OSTCBrioTbl[p] = (OS_TCB *) 0;
  }
  return (err);
} else {
  OS_EXIT_CRITICAL();
  return (OS_PRIO_EXIST);
}
}
```

列表 10.9，μC/OS 的 `OSTTaskCreate()`

```
void *OSTStkInit (*task, *pd, void *pdata, void *ptos, INT16U opt)
{
  INT16U *stk;
  opt = opt;
  stk = (INT16U *)FP_SEG(pdata);
  *stk-- = (INT16U) FP_OFF(pdata);
  *stk-- = (INT16U) FP_SEG(task);
  *stk-- = (INT16U) FP_OFF(task);
  *stk-- = (INT16U) 0x0202;
```
