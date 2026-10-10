
```assembly
TimeDiff resd 1          32位time_t 值
TimeStr resb 40                 为时间字符串预留 40 字节
TmCopy resd 9                   为 time struct tm 预留 9 个整数字段

[SECTION .text]                 包含代码的段

extern ctime
extern difftime
extern getchar
extern printf
extern localtime
extern strftime
extern time

global main                     ; 链接器找到入口点所需要

push ebp                        ;为调试器设置堆栈帧
mov  ebp,esp                    ; 程序保护 EBP, EBX, ESI, 和 EDI
push ebx
push esi
push edi

; 在此之前都是模版代码；适用于所有普通应用程序！

使用 glibc 的 ctime() 函数生成一个 time_t 日历时间值：
push 0                          向堆栈推入一个 32 位空指针，
                                ; 因为我们不需要缓冲区。
add esp,4                        调用后清理堆栈
call ctime                      在 EAX 中返回日历时间
add esp,4                        将时间值保存到内存变量
mov  [OldTime],eax               将时间值保存到内存变量

使用 glibc 的 ctime() 函数生成本地时间的字符串摘要：
push OldTime                    ; 日历时间值的地址
call ctime                     在 EAX 中返回 ASCII 字符串指针
add esp,4                        1 个参数的堆栈清理

push eax                         向堆栈推入 ASCII 字符串指针
push TimeMsg                    推入基础消息文本字符串的指针
call printf                     合并并显示两个字符串
add esp,4                        堆栈清理：2 个参数 x 4 字节 = 8



将本地时间值生成到 glibc 的静态 tm 结构体中：
push word OldTime              ; 推入日历时间值的地址
call localtime                  ;返回静态时间结构的指针
add esp,4                        1 个参数的堆栈清理
```

创建 `glibc` 静态 `tm` 结构体的本地副本：

列表 12-3: `timest.asm` (继续)

```assembly
mov esi,eax        将静态 tm 地址从 eax 复制到 ESI
mov edi,tmCopy      将本地 tm 副本的地址放入 EDI
mov ecx,9           Linux 下 tm 结构体的大小为 9 个 dword
cld                清空 DF 以便我们进行内存移动
rep movds           将静态结构体复制到本地副本
```

```assembly
显示 tm 结构体中的一个字段：
mov edx,[tmCopy+20] 字段距离 tm 偏移 20 字节
add edx,1900        年份字段是自 1900 年开始的
push edx             将值推入堆栈
push vmSm           推入基础字符串的地址
call printf          使用 printf 显示字符串和值
add esp,8            堆栈清理；2 个参数，每个 4 字节
```

```assembly
等待几秒后按回车键，以便我们获得时间差：
call getchar        等待用户按回车
```

```assembly
计算自程序运行以来经过的秒数：
mov dword 0         推入指针；我们将取 EAX 中的值
call time            获取当前时间；返回在 EAX 中
add esp,4            清理堆栈
mov [TimeDiff],eax 保存新的时间值
```

```assembly
sub eax,[OldTime]   计算时间差值
mov [TimeDiff],eax 保存时间差值
```

```assembly
push dword [TimeDiff] 将秒数差值推入堆栈
push Elapsed          推入经过时间消息字符串的地址
call printf          显示经过的时间
add esp,8            1 个参数的堆栈清理
```

```assembly
在此之后的所有都是模版代码；适用于所有普通应用程序！
pop edi              恢复保存的寄存器
pop esi
pop ebx
mov esp,ebp         在返回前销毁堆栈帧
pop ebp
ret                 将控制权交给 Linux
```

如果你转移到 GNU 范围之外的 Unix 实现，

请记住 `time_t` 值在 32 位整数处可能已经有其他定义。此时，`glibc` 将 `time_t` 定义为 32 位整数，你可以简单通过相减两个 `time_t` 值来计算时间差——至少在 2038 年之前。对于其他非 GNU 的 Unix 实现，最好使用 C 库中的 `difftime()` 函数来返回两个 `time_t` 值之间的差。

# 理解 AT&T 指令助符

对于 x86 CPU 有多于一套指令助符，这一直是许多困惑的来源。指令助符仅仅是人类记忆二进制模式（如 `10000111000001`）对 CPU 意味着什么的一种方式。与其连续写 16 个 1 和 0（或稍易理解的等价形式 `89C3`），我们说 `MOV BX,AX`。

请记住，助符仅仅是如此——人类的记忆辅助——它们是在 CPU 本身不知道的情况下创建的。汇编器将助符翻译为机器指令。我们完全同意 `MOV BX,AX` 将翻译为 `100001011100001`，这个字符串本身并没有神奇之处。我们完全可以同意“COPY AX to BX”或“STICK GPEGA into GPREB”。

本节的目标是让你对 AT&T 风格的汇编语法有清晰的理解，这种语法用于基于 Linux 的环境。虽然 Intel 语法在 Windows 开发中更常见，但 AT&T 语法是许多学术和专业项目的标准。

# AT&T 助符约定

当你第一次看到 AT&T 风格汇编时，有一些与 Intel 语法显著不同的约定。以下是一些通用规则：

- 寄存器名称始终全小写，并以符号 `%` 开头。例如，Intel 写为 `AX` 或 `EBX`，AT&T 写为 `%ax` 和 `%ebx`。
- 每一个带有操作数的 AT&T 指令助符都有单字符后缀，指示其操作数的大小：后缀 `b`、`w`、`l` 分别字节（8 位）、字（16 位）或长（32 位）。Intel 写为 `mov eax` 对应 `movl %eax`。
- 源操作数和目标操作数的顺序与 Intel 语法相反。例如，Intel 写为 `mov eax,ax`，AT&T 写为 `mov %ax,%ax`。换句话说，在 AT&T 语法中，源在前，目标在后。
- 立即操作数始终以美元符号 `$` 开头。Intel 写为 `PUSH 32`，AT&T 写为 `pushl $32`。
- 并不是所有的 AT&T 助符都由 `gcc` 生成。Intel `JCZ`、`JCXZ`、`LOOP`、`LOOP2`、`LOPE`、`LOOPNZ` 和 `LOJPNE` 的等价物才最近加入助符集，且 `gcc` 从不生成这些代码。
- 在 AT&T 语法中，内存引用中的偏移量是放在包含基、索引和比例值的括号外的符号数。稍后我会单独讨论，因为你会在 `.s` 文件中看到并能够理解它。

# gcc 生成的源文件

感受语法的最佳方法是查看由 `gcc` 生成实际 AT&T 风格 `.s` 文件。这样做有两个好处：首先，它能帮助你熟悉 AT&T 助符和格式约定。其次，当你难以如何在汇编调用 C 库函数时，可能会发现创建一个非常短的 C 程序来调用感兴趣的函数，然后检查 `gcc` 编译你的 C 程序时生成的 `.s` 文件是非常用的。所示的 `date.c` 程序实际上是我 90 年代早期研究的一部分，我用它来感受汇编层面是如何调用 `time()` 的。

每当你编译 C 程序时，并不会自动获得一个 `.s` 文件。

一旦 `gcc` 将 `.s` 文件汇编成二进制对象代码文件（通常是 `.o` 文件），它就会删除该 `.s` 文件。如果你想查看由 `gcc` 创建的 `.s` 文件，你必须使用 `-s` 选项进行编译。（注意，这里是大写的 S。在 Unix 世界中，大小写是敏感的！）命令看起来如下：

```c
gcc dateis.c -s
```

请注意，该命令的输出是汇编源文件。如果你指定了 `-s` 选项，`gcc` 就会理解为你想要生成汇编源码而非可执行程序文件，因此它只生成 `.s` 文件。要将 C 程序编译为可执行程序文件，你必须在不带 `-s` 选项的情况下重新编译。

这里是 `dateis`，它的功能仅仅打印由标准库函数 `ctime()` 返回的日期和时间：

```c
#include <time.h>
#include <stdio.h>

int main() {
	time_t timeval;

	(void)time(&timeval);
		printf("The date is: %s", ctime(&timeval));
		exit(0);
}
```

这并不是一个复杂的程序，但它说明了三个 C 库函数调用：`time()`、`ctime()` 和 `printf()`。当 `gcc` 编译上述程序（`dateis.c`）时，会产生文件 `dateis.s`，如列表 12-4 所示。我手动在 AT&T 助符右侧添加了相应的 Intel 助符作为注释，这样你就可以看到系统中相互对应的内容。（顺便说一下，`gcc` 也没有

# Listing 12-4: dateis.s

```assembly
.file          "dateis.c"
.version      "01.01"
gcc2_compiled:
.section      .rodata
.LC0:
    .string      "The date is: %s"
.text
    .align 4
```

# Listing 12-4: dateis.s (续)

```assembly
.glob main
    -type main,@function
main:
    pushl %ebp               # push %esp
    movl %esp,%ebp          # mov esp,ebp
    sub $4,(esp)            # sub esp,4
    leal -4(%ebp),eax      # lea eax,ebp-4
    pushl %esp               # push %esp
    call time               # call time
    addl $4,(esp)          # add esp,4
    leal -4(%ebp),eax      # lea eax,ebp-4
    pushl %esp               # push %esp
    call time               # call time
    addl $4,(esp)           # add esp,4
    movl %eax,%eax          # mov eax,eax
    pushl %esp               # push %esp
    pushd .LC0              # pushword .LC0
    call printf              # call printf
    addl $8,(esp)           # add esp,8
    pushl $0                # pushword 0
    call exit                # call exit
    addl $4,(esp)           # add esp,4
.palign 4,,7
```

```assembly
leave                    # leave
    ret                     # ret
```

```assembly
.L1:
    .size   main,L1-main
    .ident  "GCC" (GNU) egcs-2.91.66 19990318:Linux (egcs-1.1.2 release)"
```

阅读此内容时需要考虑的一点是，`dateis.s` 包含由编译器机械生成的汇编语言，而不是人类程序员编写！代码中的某些部分（例如标签 `.L1` 存在但从未被引用）并不理想，只能解释为 `gcc` 编译方式的产物。在更复杂的程序中可能会对标签 `.L1` 有某些自定义用法，这在这个简单的程序中并不存在。

阅读上述列表时需要注意的几点：

- 当指令不带操作数时（`call`、`leave`、`ret`），它没有操作数大小后缀。在 Intel 和 AT&T 语法中，调用和返回看起来非常相似。
- 当被引用时，消息字符串的名字前面有一个美元符号 ($)，就像数字字面量一样。在 NASM 中，命名字符串变量被视为变量而非字面量。这是另一个需要注意的 AT&T 小毛病。
- 注意 AT&T 方案中的注释分隔符是井号 (#)，而不是包括 NASM 在几乎所有 Intel 风格汇编器使用的分号。

# AT&T 内存引用语法

正如你从前面的章节回忆的，引用内存位置（于引用其地址）是通过将地址的位置放在方括号中完成的，如下：

```assembly
mov ax, dword [ebx]
```

在这里，我们获取位于 `EBX` 所含地址的任何 32 位数值并将其加载到寄存器 `AX`。更复杂的寻址看起来如下：

```assembly
mov eax, dword [ebx-4]      ; 基址减去偏移量
mov al, byte [ebx+di-28]     ; 基址加索引加偏移量
mov al, byte [ebx+edi*4]      ; 基址加索引乘以比例
```

之前所有的示例都显示了 AT&T 语法如何使用括号。在 Intel 语法中，使用方括号。以下是两者的比较：

| 特性 | AT&T 语法 | Intel 语法 |
| :--- | :--- | :--- |
| 内存引用 | 括号 `(ebx)` | 方括号 `[ebx]` |
| 偏移量 | 前缀 `-4(ebx)` | 后缀 `[ebx-4]` |
| 索引 | 内部 `(ebx+di)` | 后缀 `[ebx+di]` |
| 比例 | 内部 `(ebx+edi*4)` | 后缀 `[ebx+edi*4]` |

## 第 12 章 • 出发 C 语言

- `rand()` 函数返回一个 31 位的伪随机数。高位始终为 0，因此如果将其视为 32 位有符号整数，则该值始终为正数

一旦你理解了这些函数是如何运作的，使用它们就变得轻而易举。

## 使用 srand() 为生成器种子

将种子值传入生成器实际上比通过调用来获取当前序列中的下一个伪随机数要复杂。这并不是调用 `srand()` 有多困难：你只需要将种子值推入栈中，然后调用 `srand()`：

```
push eax          ; 这里，种子值在 eax 中
call srand ; 为伪随机数生成器种子
add esp,4 ; 为 1 个参数清理栈
```

这就是你需要做的全部工作。`rand()` 函数本身没有返回值。但是……你用什么作为种子呢？

哎，问题来了。如果你的程序在每次运行时不要以相同的伪随机数序列运行至关重要，那么你显然不想在程序中硬编码一个普通整数。理想情况下，你希望每次运行程序时都能获得不同的种子值。最好的方法（尽管还有其他方法）是使用 `time()` 函数返回的自 1970 年 1 月 1 日来的秒数作为 `srand()` 的种子，该函数在上一节中解释过。这个值被称为 `time_t`，是一个每秒变化一次的有符号整数，所以每过一秒，你都有一个新的种子值可供使用，根据定义，它永远不会重复。（我在这里假设上一节中提到的 `time_t` 溢出问题将在 2038 年之前解决）。

几乎所有人都这样做，唯一的例外是你必须确保每秒不要多次调用 `srand()` 导致重新读取序列。对于大多数运行、执行工作并在几分钟或几小时内终止的程序来说，你只需要调用一次 `srand()`；如果你正在编写一个将运行几天或几周而不终止的程序（例如服务器），那么每天设置一次随机数可能是一个好主意。

这是一个简短的代码序列，它调用 `time()` 获取当前的 `time_t`，然后将值设置为 `srand()`：

```
push eax      将一个 32 位空指针推入栈
call time    在 eax 中返回 time_t 值（32 位整数）
add esp,4     清理栈
```

```
push eax 将 eax 中的时间值推入栈
call srand 时间值是随机生成的种子值
add esp,4 清理栈
```
