
6 return;
返回的值为: $2 = 13

GDB 显示：在 `printf()` 后，`EAX` 寄存器的值为 13。这个值是函数打印的字符个数，其结果与 GDB 的结果相同。

GDB 显示出了程序的源代码 "return 0"，它是 `1.c` 文件里第六行的指令。实际上 c 文件在当前目录里，GDB 在源文件中找到了汇编指令对应的源码。GDB 又是如何知道当前的源代码对应的源码哪一行呢？这就要助于编译器所生成的调试信息了。如果启用了保存调试信息的选项，那么编译器在编译程序的时候，会生成源代码行号与对应指令地址之间的关系。

我们一起来检查 `EAX` 寄存器到底是不是 13:

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

默认情况下，GDB 会以 AT&T 语言显示汇编指令。我们可以通过该指令令 GDB 采用 Intel 语：

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

单步调试。此处，用 GDB 符号表示这里是函数的结束部分。

```
(gdb) step 7;
```

在执行 `MOV EAX, E0` 指令之后，EAX 被置零。我们对此进行验证：

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

## 6.1.2 x64: 传递 9 个参数

为了演示，我们再次修改代码，将参数的数量增加到 9 个。其中 8 个参数是 `int` 类型变量，还有一个用于控制输出格式的格式化字符串。

```c
#include <stdio.h>
int main()
{
    printf("a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n", 1, 2, 3, 4, 5, 6, 7, 8);
    return 0;
}
```

### MSVC

前文介绍，Win64 使用 `RCX`、`RDX`、`R8`、`R9` 寄存器传递 4 个参数，使用栈传递剩余参数。我们将在例中观察到这个现象。在下面的例子里，编译器使用了 `MOV` 指令对内存进行直接操作并没有使用 `PUSH` 指令。

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
    END
```

64 位系统中，`int` 类型占用 4 字节。那么，为什么编译器给 `int` 类型分配了 8 字节？其实为了方便，编译器会对数据进行对齐。同样32 位系统为 4 字节。

### GCC

x86-64 系统采用类似 Win64 的方法：优先使用 `RDI`、`RSI`、`RCX`、`R8` 寄存器传递 6 个参数，然后利用栈传递剩余参数。在生成汇编代码时，字符串存储到了 `EDI` 寄存器，而不是完整的 `RDI`。在 2 节例子里，程序在调用 `printf()` 函数前清空了 `EAX` 寄存器。

#### 指令清单 6.4 Optimizing GCC x64

```asm
.L0
    .string "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n"
main:
    sub rsp, 40
    mov r9d, 5
    mov r8d, 4
    mov ecx, 3
    mov edx, 2
    mov edi, .L0
    xor eax, eax
    mov DWORD PTR [rsp+16], 8
    mov DWORD PTR [rsp+8], 7
    mov DWORD PTR [rsp], 6
    call printf
    xor eax, eax
    add rsp, 40
    ret
```

## GCC + GDB

在使用 GDB 调试之前，首先编译源代码：

```bash
$ gcc -g 2.c -o 2
$ gdb
GNU gdb (7.6-ubuntu)
Copyright (C) 2013 Free Foundation, Inc.
License GPL v3 or later - free software: you are free to change and redistribute it.
There is NO WARRANTY, except permitted by law. Type "show warranty" for details.
GDB was configured as "x86_64-linux".
For bug reporting, please see: http://www.gnu.org/software/gdb/
Loading symbols from /home/dennis/2...
```

接下来，我们在 `printf()` 之前设置断点，然后运行程序：

```gdb
(gdb) b printf
Breakpoint 1 at 0x400410
(gdb) run
Starting program: /home/dennis/2

Breakpoint 1, printf (format=0x400628 "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n") at 2.c:29
29          
```

`RIP` 寄存器应该是函数的首地址。我们可以在 GDB 里查看各寄存器的值：

```gdb
(gdb) info registers
rax      0x0
rbx      0x0
rcx      0x3
rdx      0x2
rsi      0x400628
edi      0x400628
rbp      0xfffffffd60
rsp      0xfffffffd38
r8       4
r9       5
...
```

```gdb
(gdb) x/s $rdi
0x400628: "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n"
```

然后使用 `x/d` 显示栈中的数值。汇编指令中的格式会标识出来：

```gdb
(gdb) x/10d $rsp
0xfffffffd37: 0
0xfffffffd38: 6
0xfffffffd48: 7
0xfffffffd50: 8
...
```

64 位系统与 32 位系统并没有太区别。栈里的第一个值是返回地址。接其后的三个存在栈里的参数 6、7、8。考虑到数值“8”的高 32 位地址被清零，与之对应的存储的值为 `0x0007fff00000008`。因为 `int` 只占用 4 字节，这种存储产生问题。另外，我们认为这个地方的高 32 位是随机数。此后，我们通过以下指令查看 `printf` 函数运行之后的返回地址开始的指令。GDB 将显示 `main` 函数的全部指令。

```gdb
(gdb) set disassembly-intel
(gdb) disas 0x00000000040576
Dump of assembler code for function main:
0x0000000004052d <+20>:  sub rbp
0x0000000004052e <+41>:  mov rbp, rsp
0x00000000040535 <+43>:  sub rsp, 0x20
0x00000000040538 <+58>:  mov DWORD PTR [rsp+0x10], 8
0x0000000004053d <+66>:  mov DWORD PTR [rsp+0x8], 7
0x00000000040545 <+24>:  mov DWORD PTR [rsp], 6
0x0000000004054c <+5c>:  mov r9d, 5
0x0000000004054e <+62>:  mov r8d, 4
0x00000000040558 <+48>:  mov ecx, 3
0x0000000004055d <+48>:  mov edx, 2
0x00000000040562 <+53>:  mov esi, 1
0x00000000040567 <+67>:  mov edi, 0x400628
0x0000000004056c <+6c>:  mov eax, eax
0x00000000040571 <+71>:  call 0x400410 <printf@plt>
0x00000000040576 <+76>:  mov eax, eax
0x0000000004057b <+7b>:  leave
End of assembler dump.
```

接下来，通过 `finish` 指令运行 `printf` 之后的程序。剩下的指令会清空寄存器，注意到此时 `RIP` 已经为空。现在 `RIP` 指向了 `main()` 函数的指令：

```gdb
(gdb) finish
Run till exit from #0x400410
printf (format=0x400628 "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n", a=1, b=2, c=3, d=4, e=5, f=6, g=7, h=8) at test.c:6
Value returned: $2 = 3
(gdb) next
ax      0x0
rbx      0x0
rcx      0x3
rdx      0x2
rsi      0x400628
edi      0x400628
rbp      0xfffffffff
rsp      0xfffffffd40
r8       4
r9       5
...


## 6.2 ARM 模式下传递参数

### 6.2.1 ARM 系统传递参数时，通常会拆分：把前 4 个参数给 `R0`~`R3`，利用栈传递剩余参数。在获取（组装）参数时，遵循的函数调用是 `fastcall` 约定或 Win64 约定。这两种约定的详细介绍，请参照 6.3 节和 6.5.1 节。

#### 指令清单 6.6 非优化的 Keil 2013 (ARM 模式)

```asm
main
    PUSH {R4, LR}
    MOV R3, #3
    MOV R2, #2
    MOV R1, #1
    ADR R0, =\a=%d; b=%d; c=%d"
    BL _printf
    MOV R0, #0 ; return 0
    POP {R4, PC}
```

可见，`R0`~`R3` 寄存器负责传递参数。其中，`R0` 寄存器传递字符串，`R1` 寄存器传递 1，`R2` 寄存器传递 2，`R3` 寄存器传递 3。0x18 处的指令将 `R0` 寄存器赋值 0，对应源代码中的 "return 0"。这段汇编指令执行。即使开启了优化选项，Keil 2013 生成的汇编指令完全相同。

### 开启了优化选项的 Keil 2013 (Thumb 模式)

#### 指令清单 6.7 开启了优化选项的 Keil 2013 (Thumb 模式)

```asm
    B
    PUSH {
    PUSH {R4, LR}
    MOVS R3, #3
    MOVS R2, #2
    MOVS R1, #1
    ADR R0, =\a=%d; b=%d; c=%d"
    BL _printf
    MOVS R0, #0
    POP {R4, PC}
```

这段代码和前面 ARM 程序没有太多的差别。

####开启优化选项的 Keil 2013 (ARM 模式) + 无返回值

我们对源代码略作修改，删除 "return 0" 的语句：

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
    ADR R0, =\a=%d; b=%d; c=%d"
    BL _printf
    MOV R0, #0
    LMDD SP!, {R4,PC}
```
