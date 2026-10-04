

| 编号 | 名称 | 描述 |
| --- | --- | --- |
| n/a | HI | 专用寄存器或累积的高 32 位，可通过 MFHI 访问 |
| n/a | LO | 专用寄存器或累积的低 32 位，可通过 MFLO 访问 |

## C. 1.2 浮点寄存器 FPR

| 名称 | 描述 |
| --- | --- |
| $F0~$F1 | 函数返回值 |
| $F2~$F3 | 未被使用 |
| $F4~$F11 | 用于临时数据 |
| $F12~$F15 | 函数的前两个参数 |
| $F16~$F19 | 用于临时数据 |
| $F20~$F31 | 用于临时数据，被调用函数必须保全 |

## C. 2 指令

# MIPS 指令分为 3 类：

- R-Type，Register/寄存器类指令。此类指令操作 3 个寄存器，具有以下形式：

指令目标寄存器，源寄存器1，源寄存器2

当两个操作数同时，IDA 可能会以以下形式显示：

指令目标寄存器/源寄存器1，源寄存器2

这种显示风格与 x86 汇语言相似。

- I-Type，Immediate/立即类指令。涉及 2 个寄存器和 1 个立即数。

- J-Type，Jump/转移指令。在 MIPS 指令的 opcode 里，共有 26 位空间。

## 转移指令

实现跳转功能的指令分为 B 开头的（BEQ, B 等）和 J 开头的（JAL, JALR 等）。B 类转移指令属于 I 型指令。也就是说，B 指令的 opcode 里有 16 位立即数（偏移量）。而 J 和 JAL 属于 J 指令，它们的 opcode 里有 26 位立即数。简单来说，B 开头的指令可以将转移条件封装到 opcode 里（B 指令是“BEQ $ZERO,$Label”指令）。

## 附录D GCC 函数

| 名称 | 描述 |
| --- | --- |
| _divdi3 | 有符号数据的除法 |
| _moddi3 | 有符号数据的求模（余数） |
| _udivdi3 | 无符号数据的除法 |
| _umoddi3 | 无符号数据的求模（余数） |

## 附录E MSVC 库函数

| 名称 | 描述 |
| --- | --- |
| alldiv | 有符号数据的除法 |
| allmul | 乘法 |
| allrem | 有符号数据的求余运算 |
| allshl | 左移运算 |
| auldiv | 无符号数据的除法 |
| aulrem | 无符号数据的求余运算 |
| aullshr | 无符号数的右移 |

安装 MSVS 之后，你可以在文件中找到上述函数的源码（VC/crt/*.asm）。

## 附录F 速查表

### F. 1 IDA

| 按键 | 作用 |
| --- | --- |
| 空格 | 切换显示方式 |
| C | 转换为代码 |
| D | 转换为数据 |
| A | 转换为字符 |
| * | 转换为数组 |
| U | 未定义 |
| 键 | 作用 |
| --- | --- |
| 0 | 提取操作数的偏移量 |
| H | 把立即数转换为 1 进制数 |
| R | 把立即数转换为字符 |
| B | 把立即数转换为 2 进制数 |
| Q | 把立即数转换为 16 进制数 |
| N | 为标签重命名 |
| ? | 计算器 |
| G | 跳到地址 |
| : | 添加注释 |
| Ctrl-X | 查看当前函数、标签、变量的参考（显示栈） |
| X | 查看当前函数、变量的参考 |
| Alt-I | 搜索常量 |
| Ctrl-I | 再次搜索常量 |
| Alt-B | 搜索字节序列 |
| Ctrl-B | 再次搜索字节序列 |
| Alt-T | 搜索文本（指令中的文本） |
| Ctrl-T | 再次搜索该文本 |
| Alt-P | 编辑当前函数 |
| Enter | 跳到函数、变量等对象 |
| Esc | 返回 |
| Num — | 收缩（函数代码或区域代码） |
| Num + | 展开 |

IDA 的收缩功能把函数的代码隐藏起来。笔者编写的 IDA 脚本程序（https://github.com/yurichev/IDA_scripts）可以自动隐藏经常使用的内联代码。

### F. 2 OllyDbg

| 快捷键 | 作用 |
| --- | --- |
| F7 | 单步步入/单步调试 |
| F8 | 单步步过 |
| F9 | 执行至断点 |
| Ctrl-F2 | 重新启动程序 |

### F. 3 MSVC 选项

| | 作用 |
| --- | --- |
| /01 | 创建尺寸最小的文件 |
| /Ob0 | 禁止内联展开 |
| /Ox | 启用最大优化 |
| /GS- | 禁用安全检查（缓冲区溢出） |
| /Fa(file) | 创建汇编文件（文件名） |
| /Zi | 生成完整的调试信息 |
| /Zp(n) | 使结构体向 n 字节边界对齐 |
| /MD | 令可执行程序使用 MSCR*.DLL |

有关 MSVC 的详细介绍，请参见本书的 55.1 节。

### F.4 GCC

| 选项 | 作用 |
| --- | --- |
| -Os | 优化目标文件大小 |
| -O2 | 打开所有优化 |
| -regpar= | 设置传递参数的数量 |
| -o file | 指定输出的文件 |
| -g | 产生带调试信息的代码 |
| -S | 仅编译到汇编指令，不进行链接 |
| -masm=intel | 汇编指令采用 intel |
| -fno-inline | 禁止内联函数 |

### F.5 GDB

| 选项 | 作用 |
| --- | --- |
| break filename.c:number | 在源程序 n 行处设置断点 |
| break function | 在函数入口处设置断点 |
| break *address | 在某地设置断点 |
| b variable | 显示变量的值 |
| r | 运行 |
| c | 继续 |
| bt | 打印当前信息 |
| set disassembly-flavor intel | 设置为 intel |
| disas | 查看当前汇编指令 |
| disas function | 查看函数的汇编指令 |
| disas function, +eip | 查看函数的汇编指令，接下来的几条指令 |
| disas registers | 查看寄存器的值 |
| disas function | 查看函数的汇编指令显示寄存器的值 |
| disas locals | 列出局部变量 |
| x/w ... | 读取内存，显示为 word |
| x/w $di | 从指定的地址读取数据，显示为 word |
| x/10w ... | 读取10 个 word |
| x/i ... | 读取内存，显示为字符串 |
| x/10c ... | 读取内存，显示为代码 |
| x/b ... | 读取内存，显示为字符 |
| x/h ... | 读取内存，显示为 byte |
| x/g ... | 读取内存，显示为 word |
| finish | 读取 giant words (64位) |
| next | 执行到函数位置 |
| step | 单条语句，步入函数 |
| step-mode on | 打开步入跟踪模式 |
| frame | 切换栈 |
| del n | 查看断点 |
| set args ... | 删除断点 |

## 附录G 练习答案

### 第3章

题目1
对应章节：3.7 节
```c
Beep(0FFFF); // 一个简单的 beep。如果没有设备，将使用 speaker 生成。
```
题目2
对应章节：3.7 节
```c
#include <unistd.h>

int main()
{
    sleep(2);
}
```

### 第5章

题目1
对应章节：5.5 节
如果启用 MSVC 的优化功能，程序显示的数字分别是 EBP 的值、RA 和 argc。在命令行中执行 main() 函数分配 8 字节空间，所以会有。
题目2
对应章节：5.5 节
这些都是 UNIX 时间程序，源代码如下：
```c
#include <stdio.h>
#include <time.h>

int main(int argc, char* argv[])
{
    time_t vTime = time((time_t*)0);
    printf("%d\n", vTime);
}
```

### 第7章

题目1
对应章节：7.4 节
Linux 下将所有字符串放置到 .rodata 段，它是只读的（“只读数据”）：
```
$ objdump -s 1
```
```
Contents of section .rodata:
400600 0100200 526573756c74 2573a00 Result: %s..
400610 4865c6c 6fc,207f2c64 210a00 Hello, world!..
```

### 第13章

题目1
对应章节：13.5 节
提示：printf() 只会被调用一次。

### 第14章

题目3
对应章节：14.4 节
```c
#include <stdio.h>
int main()
{
    for(int i = 100; i > 0; --i)
    printf("%d\n", i);
}
```
题目4
对应章节：14.4 节
```c
#include <stdio.h>
int main() {
    int i;
    for(i=1; i<100; i++)
    printf("%d\n", i);
}
```

### 第15章

题目1
对应章节：15.2 节
这是一个统计字符串中空格的程序，源代码如下：
```c
int f(const char* aStr)
{
    const char* veos = aStr;
    int vCount = 0;

    for(;veos;veos)
    {
        if (*veos == ' ') ++vCount;
    }
    return vCount;
}
```

### 第16章

题目1
对应章节：16.3 节
```c
int f(int a)
{
    return a;
}
```

### 第17章

题目2
对应章节：17.10 节
计算 5 个双精度浮数的平均值，源代码如下：
```c
double f(double a1, double a2, double a3, double a4, double a5)
{
    return a1*a2*a3*a4*a5 / 5.0;
}
```

### 第18章

题目1
对应章节：18.9 节
两个 100x200 矩阵的双精度加法运算，源代码如下：
```c
#define M 100
#define N 200
void s(double *a, double *b, double *c)
{
    for (int i=0; i<N;i++)
        for (int j=0; j<M;j++)
            *(c+i*M+j)=(a+i*M+j) + *(b+i*M+j);
}
```
题目2
对应章节：18.9 节
两个矩阵（一个是 100x200，另一个是 100x300）的乘法运算，生成一个 100x300 的矩阵。源代码如下：
```c
#define M 100
#define N 200
#define P 300
void m(double *a, double *b, double *c)
{
    for (int i=0; i<M;i++)
        for (int j=0; j<P;j++)
        {
            *(c+i*M+j)=0;
            for (int k=0; k<N;k++) *(c+i*M+j)+=(a+i*M+j) * *(b+i*M+j);
        }
}
```
题目3
对应章节：18.9.3 节
```c
double f(double array[50][120], int x, int y)
{
    return array[x][y];
}
```
题目4
对应章节：18.9.4 节
```c
double f(double array[50][120], int x, int y)
{
    return array[x][y];
}
```
