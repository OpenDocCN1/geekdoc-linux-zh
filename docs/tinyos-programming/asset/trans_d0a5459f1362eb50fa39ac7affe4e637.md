
(networking buffers)。此外，nesC 程序有时会调用现有的 C 库函数，无论是来自标准 C 库（例如数学函数如 sin）还是来自个人现有的 C 代码库的函数（参见第 3.5.6 节）。

与 C 保持一致，nesC 使用 .h 头文件和 #include 来实现此目的。这还有一个额外的好处，即现有的 C 头文件可以直接重用。例如，TinyOS 的 error_t 类型和错误常量在 TinyError.h 文件中定义：

```
#ifndef TINY_ERROR_H_INCLUDED
#define TINY_ERROR_H_INCLUDED

enum {
  SUCCESS      = 0,
  FAIL         = 1,  // Generic condition; backwards compatible
  ESIZE        = 2,  // Parameter passed in was too big.
  ECANCEL      = 3,  // Operation cancelled by a call.
  EOFF         = 4,  // Subsystem is not active
  EBUSY        = 5,  // The underlying system is busy; retry later
  EINVAL       = 6,  // An invalid parameter was passed
  ERETRY       = 7,  // A rare and transient failure; can retry
  ERESERVE     = 8,  // Reservation required before usage
  EALREADY     = 9,  // The device state you are requesting is already set
};

typedef uint8_t error_t;
#endif
```

Listing 3.33 TinyError.h, a typical nesC header file

像典型的 C 头文件一样，TinyError.h 使用 #ifndef/#define 来避免在文件被多次包含时重新声明错误常量和 error_t。 在组件中包含头文件很简单：

```
#include "TinyError.h"

module BehaviorC { ... }
implementation
{
  error_t ok = FAIL;
}
```

Listing 3.34 Including a header file in a component

正如 C 中一样，#include 只是执行文本文件包含。因此，使用 #include 的位置很重要，即在 interface、module 或 configuration 关键字之前。如果不这样做，你将得不到预期的行为。同样，在 C 中，在函数中间使用 #include <stdio.h> 很可能无法工作。

the Fancy interface:

```
module FancyModule {
  uses interface Fancy;
}

implementation {
  char *name = GLOBAL_NAME;
}
```

Listing 3.37 FancyModule.nc: C preprocessor pitfalls

编译 FancyModule 会报告 GLOBAL_NAME 是一个未知符号。为什么？问题在于编译 FancyModule.nc 的第一步是对其进行预处理。此时，Fancy 接口尚未被看到，因此它尚未被加载，GLOBAL_NAME #define 也是未知的。稍后，当分析 FancyModule 时，Fancy 接口会被看到，Fancy.nc 文件会被加载并且 GLOBAL_NAME 会被 #define。但这对于在 FancyModule.nc 中使用它来说已经太晚了。

可以从中得出两个教训：首先，正如我们已经看到的，在可能的情况下，最好使用 enum 而不是 #define 来定义常量。其次，如果你必须使用 #define，就像在 C 中使用它一样：将你的定义放在使用 #ifndef/#define 保护的头文件中，并在所有使用该 #define 符号的组件和接口中 #include 此头文件。例如，Fancy.nc 和 FancyModule.nc 都应

```
#include "Fancy.h"
```

其中 Fancy.h 包含：

```
#ifndef FANCY_H
#define GLOBAL_NAME "fancy"
#endif
```

Listing 3.38 Fancy.h: the reliable way to use C preprocessor symbols

## Programming Hint 10
ALWAYS #DEFINE A PREPROCESSOR SYMBOL IN A HEADER FILE. USE #INCLUDE TO LOAD THE HEADER FILE IN ALL COMPONENTS AND INTERFACES THAT USE THE SYMBOL.

## 3.5.6 C libraries

访问 C 库很容易。通用 SineSensorC 组件的实现使用了 C 库的 sin 函数，该函数在 math.h 头文件中定义：

```
#include <math.h>
generic module SineSensorC() {
  provides interface Init;
  provides interface Read<uint16_t>;
}
```

```
implementation {
    uint32_t counter;

    void performRead() {
        float val = sin(counter++ / 20.0);
        signal Read.readDone(SUCCESS, val * 32768.0 + 32768.0);
    }
    ...
}
```

Listing 3.39 Using a C library function

与 C 一样，如果你使用库，也需要链接它。在这种情况下，使用 SineSensorC 的 nesC 程序需要通过向 ncc，即 nesC 编译器驱动程序，传递 -lm 选项来链接 math 库。

## 3.6 Exercises

- 1. Send 接口有一个 command send 和一个 event sendDone。你应该能够在 sendDone 处理程序中调用 send，还是应该等到处理程序返回之后？为什么？为两种版本的提供者编写伪代码，并为想要尽可能快地发送数据包的每种版本的用户编写伪代码。
- 2. 扩展 Blink 应用程序，使其显示随机数的低位而不是计数器。从 TinyOS 组件库中的随机数生成器之一生成随机数（RandomMlcgC 或 RandomLfsrC）。
- 3. 编写一个应用程序，在无限循环中递增 32 位计数器。每 N 次递增，应用程序切换 LED 0。选择一个 N 以便可以目视观察切换。尝试将计数器设为平台无关类型。切换变慢了吗？慢多少？尝试 16 位值。
- 4. 编写一个在两个节点上运行的 PingPong 应用程序。当节点启动时，它使用 AMSend 接口发送广播数据包。当它接收到数据包时，它发送一个数据包。每当节点发送数据包时切换 LED。LED 停止切换需要多长时间？尝试不同的距离。如果太快而无法看到，在节点接收到数据包时启动计时器，并在计时器触发时发送回复。你需要使用 AMSenderC 和 AMReceiverC 组件。

