得到高16位。LUI指令只能操作16位。不过两个LWC1之前的LUI指令几乎没有意义，笔者给它们注释了吕号。如果哪位读者知道其中玄机，还请联系赛者本人。

MFC1是Move From Coprocessor 1”的缩写。在MIPS系统中，第1号协处理器是FPU。可见，这条指令首先读取处理器的寄存器的值，然后再把这个值复制到CPU通用寄存器GPR。看不出，这条指令把pow()函数的计算运算结果复制到$3和$2寄存器，然后printf()函数从该寄存器里提取对32位数据，再将其输出为64双精度浮点数。

# 17.7 比较说明

本节围绕下程序演示：

```
#include <stdio.h>

double d_max (double a, double b)
{
    if (a>b)
        return a;

    return b;
}

int main() {
    printf("%f\n", d_max(1.2, 3.4));
    printf("%f\n", d_max(5.6, -4));
}

```

虽然这个函数很短，但是它的汇编代码并不简单。

# 17.7.1 x86

Non-optimizing MSVC

指令清单17.10 Non-optimizing MSVC 2010

```
PUBLIC      _d_max
TEXT        SEGMENT
a$ = 8      ; size = 8
b$ = 16     ; size = 8
d_max       PROC

push        ebp
mov         ebp, esp
fld         QWORD PTR, _b[ebp]
```