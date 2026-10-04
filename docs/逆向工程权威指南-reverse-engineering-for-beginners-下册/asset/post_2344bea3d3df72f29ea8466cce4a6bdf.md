
6 return;
Value returned is: $2 = 13

GDB显示:在printf()后，EAX寄存器的值为13。这个值是函数打印的字符个数，其结果与GDB的结果相同。

GDB显示出了程序的源代码“return 0”，它是1.c文件里第六行的指令。实际上c文件在当前目录里，GDB在源文件中找到了汇编指令对应的源码。GDB又是如何知道当前的源代码对应的源码哪一行呢？这就要得助于编译器所生成的调试信息了。如果启用了保存调试信息的选项，那么编译器在编译程序的时候，会生成源代码的行号与对应的指令地址之间的关系。

我们一起来检查EAX寄存器到底是不是13:

```
(gdb) info registers
eax     0x13
cx     0x0
dx     0x0
ebx     0xb7fc0000       -1208221696
esp     0xffffff120
bp     0xffffff38       0xffffff38
si     0x0
edi     0x0
eip     0x0804844a       <min+45>
```

使用这个指令查看汇编汇总的指令。图中箭头指向的是将来要运行的指令。

```
(gdb) disas
Dump of assembler code for function main:
0x0804841d <+0>:push   %ebp
0x0804841e <+1>:mov    %esp,%ebp
0x08048420 <+3>:and    $0xffffffff,%esp
0x08048423 <+6>:sub    $0x10,$esp
0x08048426 <+9>:movl   %0x3,(esp)
0x0804842e <+17>:movl   %0x2,(esp)
0x08048436 <+25>:movl   $0x1,4(%esp)
0x0804843e <+33>:movl   $0x080484f0,(esp)
0x08048443 <+40>:call   0x0804820 <printf@plt>
0x0804844a <+45>:mov    $0x0,%eax
0x0804844f <+50>:leave
0x08048450 <+51>:ret
End of assembler dump.
```

默认情况下，GDB会以AT&T语言显示汇编指令。我们可以通过该指令，令GDB采用Intel语体：

```
(gdb) set disassembly-flavor intel
(gdb) disas
Dump of assembler code for function main:
0x0808441d <0>: push ebp
0x0808441e <1>: mov ebp, esp
0x08084420 <3>: and esp, 0xffffffff
0x08084423 <6>: sub esp, 0x10
0x08084426 <9>: mov DWORD PTR [esp+0xc],0x3
0x0808442a <17>: mov DWORD PTR [esp+0x],0x2
0x08084436 <25>: mov DWORD PTR [esp+04],0x1
0x0808443e <33>: mov DWORD PTR [esp],0x008084f0
0x08084445 <40>: call 0x080482f0 <printf+plt>
=>0x0808444a <45>: mov eax, 0x
0x0808444f <50>: leave
0x08084450 <51>: ret
End of assembler dump.
```

单步调试。此处，用 GDB符号表示这里是函数的结束部分的。

```
(gdb) step 7;
```

在执行“MOV EAX, E0”指令之后，EAX会被置零。我们对此进行验证：

```
(gdb) info registers

eax 0x0 0
ecx 0x0 0
edx 0x0 0
ebx 0xb7fc0000 -1208226196
esp 0xffffff120 0xffffff120
ebp 0xffffff138 0xffffff138
esi 0x0 0
edi 0x0 0
eip 0x0804844f 0x0804844f <min+50>
```

## 6.1.2 x64: 传递9个参数

为了演示，我们再次修改代码，将参数的数量增加到9个。其中8个参数是int型变量，还有一个用于控制输出格式的格式化字符串。

```c
#include <stdio.h>
int main()
{
    printf("a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n", 1, 2, 3, 4, 5, 6, 7, 8);
    return 0;
}
```

### MSVC

前文介绍，Win64使用RCX、RDX、R8、R9寄存器传递4个参数，使用栈传递剩余参数。我们将在例中观察到这个现象。在下面的例子里，编译器使用了MOV指令对内存进行直接操作并没有使用PUSH指令。

#### 指令清单 6.3 MSVC

```asm
db 'a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d'

main PROC
    sub rsp, 8
    mov DWORD PTR [rsp+64], 8
    mov DWORD PTR [rsp+56], 7
    mov DWORD PTR [rsp+48], 6
    mov DWORD PTR [rsp+40], 5
    mov DWORD PTR [rsp+32], 4
    mov r9d, 3
    mov r8d, 2
    mov edx, 1
    lea rcx, OFFSET $
    call printf
    ; return 0
    xor eax, eax
    add rsp, 8
    ret
END
```

在64位系统中，整型数据占用4字节。那么，为什么编译器给整型数据分配了8字节？其实并不是为了方便，而且编译器会对数据进行对齐。所以64位系统为相同类型保留8字节。同样32位系统为相同类型保留4字节。

### GCC

x86-64系统采用Win64类似的方法传递参数。它优先使用RDI、RSI、RCX、R8、R9寄存器传递前六个参数，然后利用栈传递剩余参数。在生成汇编代码时，字符串指针存储到了EDI寄存器，而不是完整的RDI寄存器。在前面的3.2节中GCC生成的汇编代码出现了这个现象。在3.2节那个例子里，程序在调用printf()函数前清空了EAX寄存器。本例存在相同的操作。

#### 指令清单 6.4 Optimizing GCC 4.4 x64

```asm
.L0
    .string "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n"
main:
    sub rsp, 40
    mov r9d, 5
    mov r8d, 4
    mov ecx, 3
    mov edx, 2
    mov esi, 1
    mov edi, OFFSET .L0
    xor eax, eax             # number of registers passed
    mov DWORD PTR [rsp+16], 8
    mov DWORD PTR [rsp+8], 7
    mov DWORD PTR [rsp], 6
    call printf
    xor eax, eax
    add rsp, 40
    ret
```

## GCC + GDB

在使用GDB调试之前，首先要编译源代码：

```
$ gcc -g 2.c -o 2
$ gdb gdb
GNU gdb (GDB) 7.6-ubuntu
Copyright(C) 2013 Free Software Foundation, Inc.
License GPLv3+: GNU GPL3 or later <http://gnu.org/licenses/gpl.html>
This is free software : you are free to change and redistribute it.
There is no WARRANTY, to the extent permitted by law. Type "show copy" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
For bug reporting instructions, please see:
http://www.gnu.org/software/gdb/bugs/...
Reading symbols from /home/dennis/polygon/2...done.
```

接下来，我们在printf()运行之前设置断点，然后运行这个程序：

```
(gdb) bprintf
Breakpoint 1 at 0x400410
(gdb) run
Starting program: /home/dennis/polygon/2

Breakpoint 1, printf (format=0x400628 "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d") at printf.c:29
29 printf.c: No such file or directory
```

RSI/RDX/RCX/RBX/R9寄存器的值是传递函数的参数。RIP寄存器应该是函数的首地址。我们可以在GDB里查看各寄存器的值：

```
(gdb) info registers
rax      0x0
rbx      0x0
rcx      0x3
rdx      0x2
rsi      0x1
rdi      0x400628 4195880
rbp      0xfffffffffffd60 0xfffffffffffd60
rsp      0xfffffffffffd38 0xfffffffd38
r8       4
9       5
10     0xfffffffffffdce0 14071348346336
11     0xffffffffffa65f0 14071348263776
12     0x000440 4195392
13     0xfffffffffffe04 14071348837200
14     0x0
15     0x0
rip     0xffffffffffa65f0
```

```
(gdb) x/s $rdi
0x400628: "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d"
```

然后使用x/d显示字符中的数值。指令中的格式会标识出来。

```
(gdb) x/10d $rsp
0xfffffffffffd37 0x0000000000000576
0xfffffffffffd38 0x0000000000000006
0xfffffffffffd48 0x0000000000000007
0xfffffffffffd50 0x0000000000000008
0xfffffffffffd58 0x0000000000000000
0xfffffffffffd58 0x0000000000000000
0xfffffffffffd68 0x000000007f73a3e5
0xfffffffffffd78 0x000000007ffe04
```

64位系统与32位系统并没有太区别。栈里的第一个值是返回地址。接其后的三个存在栈里的参数6、7、8。考虑到数值“8”的高32位地址被清零，与之对应的存储的值为“0x0007fff00000008”。因为int只占用4字节，这种存储产生问题。另外，我们认为这个地方的高32位是随机数。此后，我们通过以下指令查看printf函数运行之后的返回地址开始的指令。GDB将显示main函数的全部指令。

```
(gdb) set disassembly-intel
(gdb) disas 0x00000000040576
Dump of assembler code for function main:
0x0000000004052d <20>:  sub rbp
0x0000000004052e <41>:  mov rbp, rsp
0x00000000040535 <43>:  sub rsp, 0x20
0x00000000040538 <58>:  mov PTR [rsp+0x10], 0x8
0x0000000004053d <16>:  mov PTR [rsp+0x8], 0x7
0x00000000040545 <24>:  mov PTR [rsp], 0x6
0x0000000004054c <5c>:  mov r9d, 0x5
0x0000000004054e <62>:  mov r8d, 0x4
0x00000000040558 <48>:  mov ecx, 0x3
0x0000000004055d <48>:  mov edx, 0x2
0x00000000040562 <53>:  mov esi, 0x1
0x00000000040567 <67>:  mov edi, 0x400628
0x0000000004056c <6c>:  mov eax, 0x0
0x00000000040571 <71>:  call 0x400410, <printf@plt>
0x00000000040576 <76>:  mov eax, 0x0
0x0000000004057b <7b>:  leave
0x0000000004057f <7f>:  ret
End assembler dumper
```

接下来，通过“Finish”指令运行printf之后的程序。余下的指令会清空寄存器，可以注意到此时RIP已经为空。现在，RIP指向了main()函数的第二个指令。

```
(gdb) finish
Run till exit from #0 0x400628="a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n" at printf.c:29
a=1;b=2;c=3;d=4;e=5;f=6;g=7;h=8 main at test.c:6
return 0
Value returned is: $2 = 3

```
(gdb) next
ax      0x0
rbx      0x0
cx      0x26 38
rdx      0xfffffffc 140733516684
si      0xfffffffd9 2147483609
edi      0x0
rbp      0xfffffffff 0xfffffffff
rsp      0xfffffffd40 0xfffffffd40
r8       0xffffff7dd26a 1407335185728
r9       0xffffff7d 1407334823968
10     0xfffffffd5b 1407134884496
11     0xfffffffa5900 1407134845875
12     0x000440 4195392
13     0xfffffffffffe04 14071348837200
14     0x0
15     0x0
rip     0x00400057b <min+78>
```

## 6.2 ARM模式下传递参数

### 6.2.1 ARM系统传递参数时，通常会拆分：把前4个参数给R0~R3，利用栈传递剩余参数。在获取（组装）参数时，遵循的函数调用是`fastcall`约定或win64约定。这两种约定的详细介绍，请参照6.3节和6.5.1节。

#### 指令清单 6.6 非优化的Keil 6/2013 (ARM模式)

```asm
main
    PUSH {R4, LR}
    MOV R3, #3
    MOV R2, #2
    MOV R1, #1
    ADR R0, =AADBCCD;="a=%d; b=%d; c=%d"
    BL _printf
    MOV R0, #0 ; return 0
    POP {R4, PC}
```

可见，R0~R3寄存器负责传递参数。其中，R0寄存器传递格式字符串，R1寄存器传递1，R2寄存器传递2，R3寄存器传递3。0x18处的指令将R0寄存器赋值0，对应源代码中的“return 0”。这段汇编指令执行中。即使开启了优化的选项，Keil 6/2013生成的汇编指令完全相同。

### 开启了优化选项的Keil 6/2013 (Thumb模式)

#### 指令清单 6.7 开启了优化选项的Keil 6/2013 (Thumb模式)

```asm
    B
    PUSH {
    PUSH {R4, LR}
    MOVS R3, #3
    MOVS R2, #2
    MOVS R1, #1
    ADR R0, =AADBCCD;="a=%d; b=%d; c=%d"
    BL _printf
    MOVS R0, #0
    POP {R4, PC}
```

这段代码和前面段ARM程序没有太多的差别。

开启优化选项的Keil 6/2013 (ARM模式) + 无返回值

我们对源代码略作修改，删除“return 0”的语句：

```c
#include <stdio.h>

void main() {
    printf("a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n", 1, 2, 3);
}
```

相应的汇编指令将会显著的差别：

```asm
main
    STMFD SP!, {R4,LR}
    MOV R3, #3
    MOV R2, #2
    MOV R1, #1
    ADR R0, =AADBCCD;="a=%d; b=%d; c=%d"
    BL _printf
    MOV R0, #0
    LMDD SP!, {R4,PC}
```
