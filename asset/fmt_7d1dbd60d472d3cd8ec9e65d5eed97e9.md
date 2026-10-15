
## 734 理解 GNU 许可证的影响

如上一个列表所示，如果我将在调用 `read_input` 之前停止程序，并将变量名 `input` 设置为 `buf`（这是一个有效的字符数组），程序的其余部分就能正常运行。

在 gdb 中找到行行的修复方法后，你可以对源文件进行必要的更改并使修复持久化。

## 理解 GNU 许可证的影响

你必须为 Linux 的慷慨付出代价 —— 为了保护其开发者和用户，Linux 在 GNU GPL（通用公共许可证）下分发，该许可证规定了源代码的分发。

然而，这并不意味着你不能为 Linux 编写想要以二进制形式（无论免费还是付费）分发的商业软件。你可以遵循所有规则并以二进制形式销售你的 Linux 应用。

在为 Linux 编写应用程序时，请注意这些许可证：

- GNU 通用公共许可证 (GPL)，它管理许多 Linux 程序，包括 Linux 内核和 GCC
- GNU 库通用公共许可证 (LGPL)，它涵盖许多 Linux 库

接下来的章节提供了这些许可证的概述，以及关于如何满足它们要求的建议。不过，我不是律师，请不要将书中的任何内容视为法律建议。这些许可证的全文是你的 Red Hat Linux 系统上的文本文件；请将这些许可证展示给你的法律顾问，以获得完整的解释并评估其对你业务的适用性。

### GNU 通用公共许可证

GNU 通用公共许可证 (GPL) 的文本位于 Red Hat Linux 系统各个目录中名为 `COPYING` 的文件中。例如，输入以下命令来读取 GPL：

```
cd /usr/share/doc/gdb*
more COPYING
```

GPL 与你是否对软件收费或免费分发无关；其核心目的是让软件对所有用户免费。GPL 通过要求软件以源代码形式分发，并规定任何用户都可以以源代码形式将软件复制并分发给其他人来实现这一点。此外，每个人都被提醒该软件不提供任何保证。

GPL 涵盖的软件不属于公有领域。受 GPL 涵盖的软件始终受版权保护，且 GPL 规定了对软件复制和分发的限制。从用户的角度来看，GPL 的限制并不是真正的限制；这些限制实际上是有益的，因为用户被保证可以访问源代码。

如果你使用了 GPL 涵盖的任何软件部分，你的应用程序将被视为一个派生作品。这意味着你的应用程序也将受 GPL 涵盖，并且必须分发你程序的源代码。

尽管 GPL 涵盖了 Linux 内核，但 GPL 不涵盖你通过系统调用使用内核的应用程序。这些应用程序被视为对内核的正常使用。

如果你计划以二进制形式分发你的应用程序（大多数商业软件都是这样分发的），你必须确保你的应用程序没有使用 GPL 涵盖的其他软件的任何部分。当你的应用程序调用库中的函数时，可能会使用其他软件的部分，而这些库受不同的 GNU 许可证保护，我将在下一节中描述它们。

你只需要留意少数 GPL 涵盖的库和实用工具程序。GNU dbm (`gdb`) 数据库库是 GPL 涵盖的著名库之一。GNU bison 解析器生成器是另一个 GPL 涵盖的实用工具。如果你允许 bison 生成代码，GPL 就会涵盖这些代码。

## 理解 GNU 许可证的影响 735

# 第 2 章：C 编程

本章内容

- 学习 C 基础
- 学习 C 编程语言的特性
- 总结标准库
- 在 Linux 应用中使用共享库

C 编程语言的组成 —— 一个稀疏的核心加上一个巨大的支持库 ——使其成为开发软件的理想语言。核心提供了良好的数据类型和控制结构，而所有额外任务（包括输入/输出 (I/O)、数学计算和外围设备访问）都被交给函数库。基本上，C 允许你在系统中获取任何想要的东西。在本章中，我将向你介绍 C 编程。我还会简要解释共享库的重要性以及如何创建它。

## C 程序的结构

一个典型的 C 程序组织成一个或多个源文件、模块（图 2-1）。每个文件都有相似的结构，包含注释、预处理器指令、变量和函数的声明以及它们的定义。

某些文件仅仅是一组声明，通过 C 预处理器的 `#include` 指令在其他文件中使用。这些文件通常被称为头文件，以 `.h` 扩展名结尾。在图 2-1 中，`shapes.h` 文件是一个头文件，声明了常见的数据结构和函数。另一个文件 `shapes.c` 定义了这些函数。第三个文件 `test.c` 实现了 `main` 函数 —— 这是 C 程序执行开始的函数。这些以 `.c` 结尾的文件是源文件，你可以在其中定义程序所需的函数。尽管图 2-1 每个源文件只显示了一个函数，但在典型的 C 程序中，一个源文件中有很多函数。

## 738 程序的结构

```c
shapes.h

/* file: shapes.h
 * Header file for data structures */

#ifndef SHAPES_H

#define SHAPES_H

enum shape_type {CIRCLE, RECTANGLE, OTHER};

struct RECTANGLE {

    double x1, y1, x2, y2;

    struct CIRCLE circle;

};

struct CIRCLE {

    double x, y, radius;

    struct RECTANGLE rect;

};

enum shape_type type;

union {

    RECTANGLE r;

    CIRCLE c;

} SHAPE;

/* Function prototypes * */

double compute_area(SHAPE *s);

#endif
```

```c
shapes.c

/* file: shapes.c
 * Function that computes area of shapes */

#include <math.h>
#include "shapes.h"

double compute_area(SHAPE *s) {
    switch(s->type) {
        case CIRCLE:
            CIRCLE *c = &(s->c);
            return M_PI * c->radius * c->radius;
        case RECTANGLE:
            RECTANGLE *r = &(s->r);
            return (r->x2-r->x1) * (r->y2-r->y1);
    }
}
```

图 2-1:
通常，一个 C 程序由多个源文件组成。

```c
shapetest.c

/* file: shapetest.c
 * Main program to test shapes.c */

#include <stdio.h>
#include "shapes.h"

int main(void) {
    SHAPE s;
    s.type = CIRCLE;
    s.c.radius = 50.0;
    s.c.x = s.c.y = 0;
    printf("area of circle = %f\n", compute_area(&s));
    return 0;
}
```

要创建一个可执行的程序，你必须编译并链接源文件。从 C 源文件构建程序的具体步骤取决于编译器和操作系统。例如，在 Red Hat Linux 中，你可以使用以下命令编译并链接图 2-1 所示的文件：

```bash
gcc -o shapetest shapetest.c shapes.c
```

此命令创建了一个名为 `shapetest` 的可执行文件，然后你可以通过命令运行它：

```bash
./shapetest
```
