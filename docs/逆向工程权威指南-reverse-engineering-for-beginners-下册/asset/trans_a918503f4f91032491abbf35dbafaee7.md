

![](img/a13a81a53f805f55074b2e5d2ec754b6_405_0.png)

这是地址接近数组的数据的值。它的地址距离数组组的起始地址有80 字节。

让我们通过01lyDbg看看这个数据从哪里来。如图18.3所示，使用01lyDbg加载这个程序，找到数组组最后一个值之后的数据。

## CPU - 主线程，模块

| | | | 寄存器 (FPU) |
|---|---|---|---|
| 00401200 | | PUSH EBP | EAX 00000001 |
| 00401203 | 8B 5D E4 | ECX 00000002 |
| 00401206 | 8B 5C E5 | EDX 00000003 |
| 00401209 | 89 AC 00 00 MOV EBP, PTR SS:[LOCAL.210,0] | ESI 00000004 |
| 0040120D | 8B 5D E9 | MOV EBP, PTR SS:[LOCAL.1F8,0] | EDI 00000005 |
| 00401210 | 89 C1 | MOV EAX, ECX | EBP 00000006 | EBP 00000007 |
| 00401213 | 83 C0 01 | ADD EAX, 1 | EBP 00000008 |
| 00401216 | 89 7C AC | MOV [SS:LOCAL.214,0], EAX | EBP 00000009 | |
| 0040121A | 8B 44 14 | MOV EDI, PTR SS:[LOCAL.213,14] | EBP 0000000A |
| 0040121E | 74 F0 | SHORT -14 | EBP 0000000B |
| 00401222 | 8B 45 D0 | MOV EAX, PTR SS:[EBP-0x30] | EBP 0000000C |
| 00401226 | 8B 45 CC | MOV EAX, PTR SS:[EBP-0x34] | EBP 0000000D |
| 0040122A | 8B 45 C8 | MOV EAX, PTR SS:[EBP-0x38] | EBP 0000000E | |
| 0040122E | 89 C7 | MOV EDI, EAX | EBP 0000000F | |
| 00401230 | 55 | PUSH EBP | EBP 00000010 |
| 00401231 | 55 | PUSH EBP | EBP 00000011 |
| 00401232 | 68 00 00 00 00 | PUSH 00000000 | EBP 00000012 |
| 00401237 | E8 42 00 00 00 | CALL D:[0000F0,int] | EBP 00000013 |
| 0040123C | 83 C4 04 | ADD ESP, 4 | EBP 00000014 |
| 0040123F | 5D | LEA EAX, EBP | EBP 00000015 |
| 00401240 | 55 | PUSH EBP | EBP 00000016 |
| 00401241 | 5D | POP EBP | EBP 00000017 |
| 00401242 | C3 | RET | EBP 00000018 |
| 00401243 | 89 D7 | MOV EBX, EBP | EBP 00000019 |
| 00401244 | 68 14 00 00 00 | PUSH 00000014 | EBP 0000001A |
| 00401249 | E8 5B 00 00 00 | CALL D:[0000F0] | EBP 0000001B |
| 0040124E | 83 C4 08 | ADD ESP, 8 | EBP 0000001C |
| 00401251 | 5D | LEA EAX, EBP | EBP 0000001D |
| 00401252 | 55 | PUSH EBP | EBP 0000001E |
| 00401253 | 5D | POP EBP | EBP 0000001F |

| 地址 | 十六进制转储 | ASCII |
|---|---|---|
| 003FF7A0 | 00 00 00 00 00 00 00 00 00 00 00 | ................. |
| ... (省略中间重复数据) | ... | ... |
| 003FF9F0 | 00 00 00 00 00 00 00 00 00 00 00 00 | ................. |

图18.3 OllyDbg: 读取数组中的第20个元素、并使用printf()输出

| C-主线程，模块: | | 寄存器 (FPU) |
|---|---|---|
| 00401000 | | PUSH EBP | EAX 00000000 |
| 00401001 | | MOV EBP, ESP | ECX 75525152 |
| 00401002 | | MOV EAX, ESP | EDX 00000063 |
| 00401003 | | MOV EAX, PTR [EBP-0x10] | ESI 00000000 |
| 00401004 | | EDI 00000001 | EBP 001F08F8 |
| 00401005 | | JMP SHORT 0040A60 | EBP 001F08F8 |
| ... (省略重复数据) | ... | ... |

## 图18.4 OllyDB：还原寄存器的值

到底有没有办法控制数组边界访问问题？如果需要控制数组边界，就要编译器生成的程序检查是否在边界。某些高级语言，如Python和Java，就会边界检查。但是这种控制会影响性能。

## 18.2 向数组之外的写入

向数组之外的写入

既然我们可以“非法地”利用指针读取数组之外的数值，我们也可以向数组之外写入数据呢？可以通过下面的程序验证：

```c
#include <stdio.h>

int main() {
    int a[20];
    int i;

    for (i=0; i<30; i++)
        a[i]=i;

    return 0;
}
```

MSVC编译后得到指令：

```asm
TEXT            SEGMENT
_i = -84         ; size = 4
a = -80          ; size = 80
_main           PROC
            push            ebp
            mov             ebp, esp
            sub             esp, 84
            mov             dword [ebp-0x10], 0
            jmp             short .LN3
.LN2:
            mov             eax, d ptr [ebp-0x10]
            add             eax, 1
            mov             dword [ebp-0x10], eax
.LN3:
            cmp             eax, 0000001E
            jge             short .LN1
.LN1:
            mov             ecx, d ptr [ebp-0x10]
            mov             dword ptr [ebp-80], edx; 这里的可以用ECX 取代x
            jmp             short .LN2
.LN2@main:
            xor             eax, eax
            mov             esp, ebp
            ret
```

运行这个程序的时候，程序崩溃了。我们要研究一下它是哪里崩溃的。使用OllyDbg加载程序，等到写满30个元素，如图18.5所示。

## CPU - 主线程

| | | 寄存器 (FPU) |
|---|---|---|
| 00400000 | 55 | PUSH EBP | EAX 00000000 |
| ... (省略重复数据) | ... | ... |

