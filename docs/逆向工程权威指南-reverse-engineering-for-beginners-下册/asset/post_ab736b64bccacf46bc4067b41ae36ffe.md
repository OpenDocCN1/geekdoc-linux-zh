
0x400cc处的指令用了$S0寄存器赋值，而后程序用了scanf()函数，紧接着地址为0x4006e8的指令继续用$S0。此我们可以判断。scanf()函数不会变更$S0的值。

## 7.3 scanf() 函数的状态监测

大家都知道scanf()不怎么流行了，但是并不代表它派不上用场了。万一万得已使用这个函数的时候，切记检查函数的退出状态是否正确。例如：

```c
#include <stdio.h>

int main() {
{
    int x;
    printf("Enter X:\n");
    if (scanf("%d", &x)==1) {
        printf("You entered %d...\n", x);
    } else {
        printf("What you entered. Huh?\n");
    }
    return 0;
}
```

根据这个函数的功能规范[3]，scanf()函数在退出时会返回成功值的数量总。

就本例子而言，正常情况下：用户输入一个整型数字时函数返回1；如果没有输入的值存在问题（或为EOF/没有输入数据），scanf()则返回0。

为此我们可以在C程序里添加检查结果的代码，以便出现错误时进行相应的处理。

我们验证一次：

```
C:\...>ex3.exe
Enter X:
123
You entered 123...

C:\...>ex3.exe
Enter X:
ouch
What you entered? Huh?
```

### 7.3.1 MSVC: x86

使用MSVC2010生成的汇编代码如下所示：

```assembly
lea     eax, DWORD PTR _xS[ebp]
push    eax
push    OFFSET $SG3833 ; '%d', 00H
call    scanf
add     esp, 8
cmp     eax, 1
jne     SHORT $LN2@main
mov     ecx, DWORD PTR _xS[ebp]
push    ecax
push    OFFSET $SG3834 ; 'You entered %d... ', 0Ah, 00H
call    printf
add     esp, 1
jmp     SHORT $LN1@main
$LN2@main:
push    ecax, OFFSET $SG3836 ; 'What you entered? Huh?', 0Ah, 00H
call    printf
add     esp, 4
$LN1@main:
xor     eax, eax
```

当被调用函数callee（本例中scanf（函数））使用EAX寄存器值向调用函数caller（本例中jne（函数））传递返回值。

之后，“CMP EAX, 1”指令对返回值进行比对，检查其值是否为1。

JNE是跳转指令，全称是“Jump if Not Equal”。在两个值不同时跳转。

就是，如果EAX寄存器的值不是1，则程序将跳转到JNE所指向的地址（本例中会接到$LN1@main），在将控制权交给这个地址之后，CPU将执行其后的打印指令，显示“What you entered? Huh?”。另一种情况是scanf（函数）成功读取指定数据类型的数据，其返回值为1，此时不会发生跳转，而是继续执行JNE以前的指令，显示“You entered %d... ”和变量x的值。

scanf（函数）成功赋值变量值的情况下，程序一路执行到JMP（无条件跳转）指令。该指令跳转到第二个调用指令printf（函数）的指令，从“XOR EAX, EAX”指令开始，并完成返回0的操作。

可见，“一般地说”是指判断语句中出现的“CMP/Jcc”指令。此处cc是英文“condition code”的缩写。比较两个指令会设置处理器的标志位[44]。Jcc指令会检查标志位，判断是否进行跳转。

但是这种说法容易产生误导，实际CMP指令进行的操作是减法运算。确切地说，不仅是CMP指令所有的“数学/算术计算”指令都会设置标志位。

是的，如果将1与1比较，1-1=0，ZF标志位为“零”标识，最终运算结果是0，将被计算指令设置为1。两个不同的数值进行CMP比较时，ZF标志位的值绝不会是1。JNE指令会根据ZF标志位的判断决定是否需要跳转，实际上两者都是（Jump if Not Zero）的同义。JNE和JNZ的opcode相同。如同即使使用减法运算操作SUB来替换CMP指令，Jcc指令也可以进行正常的跳转。但未在使用SUB指令时，我们还需要使用一个寄存器保存运算结果，而CMP则不需要使用寄存器保存运算结果。

### 7.3.2 MSVC: x86

现在介绍推荐的好习惯。对于初学者来说，使用MSVC编译器的MD/MD值很重要。这个选项要选择“不要链接（Link）函数而是从MSVC* DLL导入这些标准函数。总之，使用/MD选项的好处是一目了然的，我们需要知道它在哪里、调用了哪些标准函数。

在使用IDA分析程序的时候，要充分利用它的标记功能。比如分析这段程序的时候，我们可能会发现错误的时候执行JNE跳转。这时就可以用鼠标点击跳转的JNE指令，按下“n”键，将对应的标签（label）改名为“error”，然后对出错的标签重命名为“exit”。这种改进可以大幅增强代码的可读性。

```text
.text:00401000
.text:00401000 var_4 = dword ptr -4
.text:00401000 argc = dword ptr 8
.text:00401000 argv = dword ptr 8
.text:00401000 envp = dword ptr 10h
.text:00401000
.text:00401000

                   push             ebp
.text:00401001      mov             ebp, esp
.text:00401003      push             ecx
.text:00401004      push             offset Format ; "Enter X: \n"
.text:00401009      call             ds:printf
.text:0040100F      add              esp, 4
.text:00401012      lea             eax, [ebp+var_4]
.text:00401015      push             ecax
.text:00401016      push             offset aD ; "%d"
.text:0040101B      call             ds:scanf
.text:00401021      add              esp, 8
.text:00401024      cmp             eax, 1
.text:00401027      jnz              short error
.text:00401029      mov             ecx, [ebp+var_4]
.text:0040102C      push             ecx
.text:0040102D      push             offset aE ; "You entered...\n"
.text:00401032      call             ds:printf
.text:00401038      add              esp, 8
.text:0040103B      jmp              short exit
```

如此一来，这段代码就容易理解了。虽然重命名标签的功能强大，但是每一个指令无疑都是。此外IDA还有一些高级用法。整理代码：标记某段代码后，键盘上的“-号，整段代码将被隐藏，只留下地址和标签。在例子中我隐藏了这两段代码，并对整段代码进行了命名。

```text
.text:00401000 segment for public
.text:00401000 assume cs:text
.text:00401000 jorg 0041000h
.text:00401000 ask for X
.text:00401012 get X
.text:00401024      cmp             eax, 1
.text:00401027      jnz              short error
.text:00401029      mov             ecx, [ebp+var_4]
.text:0040102C      push             ecx
.text:0040102D      push             offset aE ; "You entered...\n"
.text:00401032      call             ds:printf
.text:00401038      add              esp, 8
.text:0040103B      jmp              short exit
.text:0040103D error: ; XREF: _main+27
.text:0040103D      push             offset aF ; "What you entered?\n"
.text:00401042      call             ds:printf
.text:00401048      add              esp, 4
.text:0040104B exit: ; XREF: _main+3B
.text:0040104B      xor             eax, eax
.text:0040104D      mov             esp, ebp
.text:0040104F      pop             ebp
.text:00401050 ret
```

如需显示之前隐藏的代码，可以直接使用数字键盘上的“+号。

## 图解模式

按下空格键，IDA将会进入图解显示方式。其效果如图7.7所示。

```c
int __cdecl main(
_main proc ptr -4
var_4= dword ptr 4
argc= dword ptr 8
argv= dword ptr 0Ch
envp= dword ptr 18h

push ebp
mov ebp, esp
push ecx
push offset Format  ; "Enter X:\n"
call ds:printf
add esp, 4
lea eax, [ebp+var_4]
push eax
push offset a0  ; "%s%d"
call ds:scanf
add esp, 8
cmp eax, 1
jnz short exit
```

![](img/a13a81a53f80f55074b2e5d2ec754b6_140_0.png)

判断语句会分出两个箭头，一条是红色的，一条是绿色的。当判断条件值为真时，程序会采用绿色箭头所示的流程；如果判断条件不成立，程序将采用红色箭头标识的流程。图解模式下，也可以对各节点命名和收缩。图7.8处理了三个模块。

### 7.3.3 MSVC: x86+OllyDbg

我们使用OllyDbg调试刚才的程序，在scanf()返回值的情况下强制其继续运行后续的指令。

在把变量的地址传递给scanf()的时候，变量处于未初始化状态，其值应当随机数据。如图7.9所示，变量的值为0x6E49714。

| Address | CPU - main thread |
| :--- | :--- |
| 00320000 | 55 65 74 65 22 50 38 00 00 25 04 00 00 00 00 |
| 00320010 | 69 7F 68 65 64 74 65 72 24 25 75 6E 74 65 63 |
| 00320020 | 26 30 00 00 57 61 74 65 72 20 78 79 6D 65 6E |
| 00320030 | 65 72 65 34 5F 28 40 78 00 FF FF FF 72 |
| 00320040 | 74 FF 01 00 00 00 00 00 00 00 00 00 88 |
| 00320050 | 69 FF 02 00 00 00 00 00 00 00 00 00 00 | |
| 00320060 | 89 44 24 08 89 44 24 0C 89 44 24 10 89 44 24 14 |
| 00320070 | 74 FF 03 00 00 00 0 0 |
| 00320080 | 69 FF 04 00 00 00 00 00 00 00 00 00 00 00 | |
| 00320090 | 89 44 24 0C 89 44 24 10 00 00 00 00 00 00 00 | |
| 003200A0 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | |
| 003200B0 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | |
| 003200C0 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | |
| 00324000 | 00 00 00 00 (4C 6F 63 6E 65 61 2C 6E 6F 2C 65 67) |
| 00324010 | 00 00 00 00 00 00 00 00 00 00 | |
| 00324020 | 00 00 00 00 00 00 00 00 00 00 | |
| 00324030 | 00 00 00 00 00 00 00 00 00 00 | |
| 00324040 | 00 00 00 00 00 00 00 00 00 00 | |
| 00324050 | 00 00 00 00 00 00 00 00 00 00 | |
| 00324060 | 00 00 00 00 00 00 00 00 00 00 | |
| 00324070 | 7F 70 03 00 00 00 0 0 | |
| 00324080 | 00 00 00 00 00 00 00 00 00 00 | |
| 00324090 | 00 00 00 00 00 00 00 00 00 00 | | | | | | |

![](img/a13a81a53f80f55074b2e5d2ec754b6_142_0.png)

在执行scanf()函数的时候，我们输入非数字的内容，例如“asdasd”。这时scanf()会遇到EAX寄存器返回0，如图7.10所示。这个零意味着scanf()函数遇到错误。

这种解耦模式非常实用。逆工程工作不多的人，可以使用这种方式大幅度地减少他需要处理的信息量。
