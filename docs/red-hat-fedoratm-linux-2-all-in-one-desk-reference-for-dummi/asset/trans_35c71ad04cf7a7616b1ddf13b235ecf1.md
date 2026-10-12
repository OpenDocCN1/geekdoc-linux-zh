
以及所有必要的数据结构和预处理器常量，都定义在一组标准头文件中。表 2-4 列出了这些标准头文件，并概括了它们的内容。

## 记住

如果你打算用 C 编写应用程序，就必须熟悉许多标准库，因为 C 的许多编程过程都依赖于这些库。如果你正在编写图形应用程序，还必须熟悉其他库，例如 GIMP 工具包。

### 表 2-4 C 语言中的标准头文件

| **头文件** | **用途** |
| :--- | :--- |
| `<assert.h>` | 定义 `assert` 宏。用于程序诊断。 |
| `<ctype.h>` | 声明用于字符分类和转换的函数。 |
| `<errno.h>` | 定义错误条件的宏，`EDOM` 和 `ERANGE`，以及整型变量 `errno`，库函数通过它返回错误代码。 |
| `<float.h>` | 定义可以存储在浮点类型中的数值范围。 |
| `<iso646.h>` | 定义了一些宏，这些宏在编写非英语语言的 C 程序时很有帮助，这些语言可能将诸如 `&` 和 `--` 等字符组合用于其他用途。 |
| `<limits.h>` | 定义所有整型数据类型的极限值。 |
| `<locale.h>` | 声明 `lconv` 结构体和将 C 程序定制为特定区域设置所需的函数。 |
| `<math.h>` | 声明常见的数学函数和 `HUGE_VAL` 宏。 |
| `<setjmp.h>` | 定义 `setjmp` 和 `longjmp` 函数，这些函数可以在不依赖普通函数调用和返回的情况下，将控制权从一个函数转移到另一个函数。还定义了 `setjmp` 和 `longjmp` 使用的 `jmp_buf` 数据类型。 |
| `<signal.h>` | 定义处理异常条件所需的符号和例程。 |
| `<stdarg.h>` | 提供宏，这些宏用于访问接受可变数量参数的函数中未命名的参数。 |
| `<stddef.h>` | 定义标准数据类型 `ptrdiff_t`、`size_t`、`wchar_t`；符号 `NULL`；以及宏 `offsetof`。 |
| `<stdio.h>` | 声明输入和输出操作所需的函数和数据类型。定义 `BUFSIZ`、`EOF`、`SEEK_CUR`、`SEEK_END` 和 `SEEK_SET` 等宏。 |
| `<stdlib.h>` | 声明许多实用函数，如字符串转换例程、随机数生成器、内存分配例程和进程控制例程（如 `abort`、`exit` 和 `system`）。 |
| `<string.h>` | 声明字符串操作例程，如 `strcmp` 和 `strcpy`。 |
| `<time.h>` | 定义数据类型并声明操纵时间的函数。定义类型 `clock_t` 和 `time_t` 以及 `tm` 数据结构。 |
| `<wchar.h>` | 定义数据类型并声明用于处理宽字符数据类型（`wchar_t`）的函数。 |
| `<wctype.h>` | 定义数据类型并声明用于分类和转换宽字符数据类型（`wchar_t`）的函数。 |

### Linux 应用程序中的共享库

大多数 Linux 程序都使用共享库。至少，大多数 C 程序都使用 C 共享库 `libc.so.X`，其中 `X` 是一个版本号。使用共享库是可取的，因为许多可执行程序可以共享同一个共享库——你只需要将共享库的一个副本加载到内存中。此外，*动态链接*（即在运行时程序加载代码模块并与之链接）正变得越来越流行，因为它允许应用程序仅在需要时加载代码块，从而减少应用程序的内存需求。

当程序使用一个或多个共享库时，你需要程序的可执行文件，以及所有的共享库，才能运行该程序。换句话说，如果系统中没有所有的共享库，你的程序就无法运行。

![](img/9f89727199836b0f871f1745838aa8b2_786_0.png)

如果你销售使用共享库的应用程序，请确保所有必要的共享库都随你的软件一起分发。

共享库的主题对 Linux 程序员来说很有趣，因为使用共享库会减小可执行文件的大小。在本节中，我简要描述如何在示例程序中创建和使用共享库。

#### 检查程序使用的共享库

使用 `ldd` 实用程序来确定可执行程序需要哪些共享库。输入以下 `ldd` 命令以查看程序（由 GCC 存储在默认文件 `a.out` 中）使用的共享库：

```
ldd a.out
```

以下是 `ldd` 对典型 C 程序的报告：

```text
libc.so.6 => /lib/tls/libc.so.6 (0x00b0a000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00a0f1000)
```

更复杂的程序，如 GIMP（一个类似 Adobe Photoshop 的程序）使用更多的共享库。要查看其共享库需求，输入以下命令：

```bash
ldd /usr/bin/gimp
```

以下是我的 Fedora Core 系统上显示的列表：

```bash
libgimpwidgets-1.3.so.26 => /usr/lib/libgimpwidgets-1.3.so.26 (0x03783000)
libgimpcolor-1.3.so.26 => /usr/lib/libgimpcolor-1.3.so.26 (0x001ce000)
libgimpmodule-1.3.so.26 => /usr/lib/libgimpmodule-1.3.so.26 (0x001d8000)
libgimpbase-1.3.so.26 => /usr/lib/libgimpbase-1.3.so.26 (0x001a1000)
libgimptuumb-1.3.so.26 => /usr/lib/libgimptuumb-1.3.so.26 (0x00be000)
libgimpbase-1.3.so.26 => /usr/lib/libgimpbase-1.3.so.26 (0x000d7000)
libgtk-x11-2.0.so.0 => /usr/lib/libgtk-x11-2.0.so.0 (0x00448000)
libgdk-x11-2.0.so.0 => /usr/lib/libgdk-x11-2.0.so.0 (0x00762000)
libatk-1.0.so.0 => /usr/lib/libatk-1.0.so.0 (0x0073f000)
libgdk_pixbuf-2.0.so.0 => /usr/lib/libgdk_pixbuf-2.0.so.0 (0x003d5000)
libtcm.so.6 => /lib/tls/libtcm.so.6 (0x00c46000)
libXcursor.so.1 => /usr/lib/lib/libXcursor.so.1 (0x00191000)
libgpgpxo-1.0.so.0 => /usr/lib/libgpgpxo-1.0.so.0 (0x0075b000)
libgpgpxo-1.0.so.0 => /usr/lib/libgpgpxo-1.0.so.0 (0x00731000)
libart_lgpl_2.so.2 => /usr/lib/libart_lgpl_2.so.2 (0x003b0000)
libgpgf2-1.0.so.0 => /usr/lib/libgpgf2-1.0.so.0 (0x003ec000)
libgpg-1.0.so.0 => /usr/lib/libgpg-1.0.so.0 (0x00d12000)
libgobject-2.0.so.0 => /usr/lib/libgobject-2.0.so.0 (0x002a0000)
libgmodule-2.0.so.0 => /usr/lib/libgmodule-2.0.so.0 (0x002e7000)
libdb1-2.0 => /usr/lib/libdb1.so.2 (0x00c6f000)
liblib-2.0.so.0 => /usr/lib/liblib-2.0.so.0 (0x001f5000)
libfontconfig.so.1 => /usr/lib/libfontconfig.so.1 (0x0018e000)
libfreetype.so.6 => /usr/lib/libfreetype.so.6 (0x00101000)
libz.so.1 => /usr/lib/libz.so.1 (0x00d61000)
libpthread.so.0 => /lib/tls/libpthread.so.0 (0x00474000)
libc.so.6 => /lib/tls/libc.so.6 (0x00b0a000)
libX11.so.6 => /usr/lib/libX11.so.6 (0x0c7f1000)
libXrandr.so.2 => /usr/lib/lib/libXrandr.so.2 (0x0019ce000)
libX11.so.6 => /usr/lib/lib/libX11.so.6 (0x00383000)
libext.so.6 => /usr/lib/lib/libext.so.6 (0x0051000)
libXft.so.2 => /usr/lib/lib/libXft.so.2 (0x00d0b000)
libXrender.so.1 => /usr/lib/lib/libXrender.so.1 (0x004f4000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00a0f1000)
libexpat.so.0 => /usr/lib/libexpat.so.0 (0x00a9d000)
```

在这种情况下，该程序使用了许多共享库，包括 X11 库（`libX11.so.6`）、GIMP 工具包（`libgtk-x11-2.0.so.0`）、*通用绘图工具包（GDK）库*（`libgdk-x11-2.0.so.0`）、*数学库*（`libm.so.6`）和 C 库（`libc.so.6`）。

几乎所有的 Linux 应用程序都需要共享库才能运行。

#### 创建共享库

为你自己的应用程序创建共享库相当简单。假设你想以共享库的形式实现一个对象（将对象视为一组代码和数据）。共享库中的一组函数代表对象的接口。要使用该对象，你需要加载其共享库并调用其接口函数。（我将在下一节中展示如何加载库。）

以下是这个作为共享库实现的简单对象的 C 源代码（你也可以称其为*动态链接库*）——将此代码保存在名为 `dynobj.c` 的文件中：

```c
/* ------------------------------------------------------------ */
/* File: dynobj.c
 *
 * Demonstrate use of dynamic linking.
 * Pretend this is an object that can be created by calling
 * init and destroyed by calling destroy.
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/* Data structure for this object */
typedef struct OBJDATA
{
    char *name;
    int version;
} OBJDATA;

/* ------------------------------------------------------------ */
/* init
 *
 * Initialize object (allocate storage).
 */
void* init(char *name)
{
    OBJDATA *data = (OBJDATA*)calloc(1, sizeof(OBJDATA));
    if(name)
        data->name = malloc(strlen(name)+1);
    strcpy(data->name, name);

    printf("Created: %s\n", name);

    return data;
}
/* ------------------------------------------------------------ */
```
