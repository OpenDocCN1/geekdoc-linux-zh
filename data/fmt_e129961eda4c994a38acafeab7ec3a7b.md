
使用 `:` 操作符时，如果目标的修改时间小于 `dependency-list` 中的任何文件，则认为目标已过时。如果操作符是 `!`，则在检查并重新创建 `dependency-list` 中的源文件后，目标始终会被重新创建。使用 `::` 操作符时，如果在 `dependency-list` 中未指定源文件，则目标始终会被重新创建。在 `:` 和 `!` 操作符的情况下，如果 `make` 被中断，目标会被删除，但在 `::` 操作符的情况下则不会。本书中，我们仅使用最常用的 `:` 操作符。

`makefile` 由一组 `make` 规则组成，这些规则描述了用于创建可执行文件的文件之间的依赖关系。`make` 实用程序使用 `makefile` 中的规则来确定构成你的程序的文件中哪些需要重新编译和重新链接以重新创建可执行文件。因此，例如，如果你修改了一个头文件（`.h`），`make` 实用程序会重新编译所有包含该头文件的文件。包含该头文件的文件必须在相应的 `makefile` 中指定。

以下 `makefile` 可用于第 17.5.3 节中讨论的 `power` 程序。

```
% cat makefile
# Sample makefile for the power program
# Remember: each command line starts with a <TAB>
power: power.c
	cc power.c -o power -lm
%
```

如果可执行文件 `power` 存在，并且源文件 `power.c` 自可执行文件创建以来未被修改，运行 `make` 将给出 `power.c` 的可执行文件是最新的消息。因此，`make` 无需重新编译和重新链接 `power.c`。有时，你需要强制重新制作可执行文件，因为例如包含在你的源代码中的系统头文件之一已更改。为了强制重新创建可执行文件，你需要更改最后的更新时间。一种常用的方法是使用 `touch` 命令，然后重新运行 `make`。以下会话说明了这些要点。

```
% make
make: 'power' is up to date.
```

```
% touch power.c
% make
cc power.c -o power -lm
%
```

当你使用 `touch` 命令并将其参数设为一个或多个现有文件时，它会将它们的最后更新时间设置为当前时间。当使用不存在的文件作为参数时，它会创建一个零长度（即空）的文件，其名称与该参数相同。

在下面的章节练习中，你将使用 `make` 命令为单个源文件创建可执行文件。

## EXERCISE 17.3

为 `power.c` 文件中的 C 程序创建可执行代码，并将其放在名为 `XpowerY` 的文件中。使用前面给出的 `makefile`，使用 `make` 实用程序执行此任务。运行 `XpowerY` 以确认程序正常工作。

为了展示 `make` 实用程序的进阶用法，我们将 `power.c` 文件中的 C 程序划分为两个文件：`power.c` 和 `compute.c`。以下会话显示了这些文件的内容。`compute.c` 文件包含 `compute` 函数，该函数由 `power.c` 中的 `main` 函数调用。为了生成 `power` 文件中的可执行文件，我们需要独立编译两个源文件，然后将它们链接起来，如会话末尾的两个 `cc` 命令行所示。

```
% cat power.c
#include <stdio.h>

double compute(double x, double y);
int main()
{
    float   x,y;
    printf ("The program takes x and y from stdin and
    displays x^y.\n");
    printf ("Enter integer x: ");
    scanf ("%f", &x);
    printf ("Enter integer y: ");
    scanf ("%f", &y);
    printf ("x^y is: %6.3f\n", compute(x,y));
}
% cat compute.c
#include <math.h>
double compute (double x, double y)
{
    return (pow ((double) x, (double) y));
}
```

```
% cc -c compute.c power.c
% ls
compute.c compute.o power.c  power.o
% cc compute.o power.o -o power -lm
%
```

在这种情况下，两个源文件的依赖关系相当简单。要创建可执行文件 `power`，我们需要两个目标模块：`power.o` 和 `compute.o`。如果 `power.c` 或 `compute.c` 中的任一文件被更新，可执行文件就需要重新创建。图 17.4 显示了对依赖关系的第一次分析。

因此，对应于此依赖关系的 `make` 规则如下。注意，由于 `compute.c` 文件中的 `compute` 函数使用了该库中的 `pow` 函数，必须链接数学库。

```
power:      power.o compute.o
            cc power.o compute.o -o power -lm
```

我们还知道，目标文件 `power.o` 是由源文件 `power.c` 构建的，而目标文件 `compute.o` 是由源文件 `compute.c` 构建的。图 17.5 显示了对依赖关系的第二次分析。

因此，创建两个目标文件的 `make` 规则为

```
power.o:    power.c
            cc -c power.c
```

![](img/02e070097d401d3bf7de4bf1c470b267_736_0.png)

图 17.4 `make` 依赖树的第一次分析。

![](img/02e070097d401d3bf7de4bf1c470b267_736_1.png)

图 17.5 `make` 依赖树的第二次分析。

```
compute.o: compute.c
	cc -c compute.c
```

最终的 `makefile` 如下所示

```
% cat makefile
power:
	power.o compute.o
	cc power.o compute.o -o power -lm
power.o: power.c
	cc -c power.c
compute.o: compute.c
	cc -c compute.c
%
```

然后我们使用前述的 `makefile` 执行 `make` 工具：

```
% make
cc power.o compute.o -o power -lm
%
```

在下面的章节练习中，你将使用 `make` 工具为划分为两个文件的 C 源代码创建可执行代码。

## EXERCISE 17.4

创建两个源文件 `power.c` 和 `compute.c`，并按照刚才讨论的步骤使用 `make` 工具创建可执行文件 `power`。

我们现在改变该软件的结构，将其划分为六个文件，分别称为 `main.c`、`compute.c`、`input.c`、`compute.h`、`input.h` 和 `main.h`。这些文件的内容在以下会话中显示。注意，`compute.h` 和 `input.h` 文件包含 `compute` 和 `input` 函数的声明（原型），但不包含其定义；定义位于 `compute.c` 和 `input.c` 文件中。`main.h` 文件包含向用户显示的两个提示。图 17.6 显示了新的依赖树。

```
% cat compute.h
/* Declaration/Prototype of the "compute" function */
double compute(double, double);
% cat input.h
/* Declaration/Prototype of the "input" function */
double input (char *);
% cat main.h
/* Declaration of prompts to users */
#define PROMPT1 "Enter the value of x: "
#define PROMPT2 "Enter the value of y: "
```

![](img/02e070097d401d3bf7de4bf1c470b267_738_0.png)

图 17.6 示例 C 软件的 `make` 依赖树。

```
% cat compute.c
#include <math.h>
#include "compute.h"
double compute (double x, double y)
{
    return (pow ((double) x, (double) y));
}
```

```
% cat input.c
#include <stdio.h>
#include "input.h"
double input(char *s)
{
    float x;
    printf ("%s", s);
    scanf ("%f", &x);
    return (x);
}
```
