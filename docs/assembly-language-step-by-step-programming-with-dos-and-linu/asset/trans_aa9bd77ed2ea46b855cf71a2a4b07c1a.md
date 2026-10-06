

# 汇编语言分步详解

```assembly
push dword oldtime ; 将日历时间值的地址推入栈
call localtime      ; 在 eax 中返回指向静态时间结构的指针
add esp, byte 4    ; 调用后清理栈空间
```

在这里，`oldtime` 是一个 `time_t` 类型的值。给定此值，`localtime` 在 EAX 中返回（这种方式类似于 `ctypes`）——一个指向运行时库中某处 `tm` 结构的指针。通过将此指针作为基地址，你可以使用相对于基地址的常量偏移量来访问结构中的字段（此处显示存储在 EAX 中）：

```assembly
mov edx, [eax-20] ; 年份值在 tm 结构偏移 20 字节处
push edx           ; 将值推入栈
push dword timemsg ; 将基础字符串的地址推入栈
call printf         ; 使用 printf 显示字符串和年份
add esp, byte 4    ; 清理栈空间
```

通过使用表 13.3 所示的偏移量，你可以访问 `tm` 结构中所有其他时间和日期组件，这些组件以 32 位整数值的形式存储。

# 未初始化存储与 [.bss]

对于初学者来说，程序中 `[.data]` 段和 `[.bss]` 段之间的区别可能很模糊。两者都用于存放变量……那么，这到底是怎么回事？它是（像计算中的许多其他事物一样）只是更多的……嗯…… `.bss` 吗？

并非如此。同样，区别更多是出于惯例而非其他原因。`[.data]` 段旨在包含已初始化的数据；即你定义的带有初始值的变量。在大多数情况下，这些将是用于数据显示的基础字符串，包含提示信息和其他在程序执行过程中不会改变的字符串数据。有时，你会存储定义输出报告中行数的计数值等。这些值非常 Pascal 语言中定义为 `CONSTANT` 的值。它们在编译时定义，并且不应该发生改变。

在汇编语言中，当然，如果你想改，可以改变它们。对于那些在开始时没有值（即未初始化）但在程序执行过程中会被赋值的变量（这是大多数高级语言语言程序员看待变量的方式），你应该在 `[.bss]` 段中为它们分配内存。

我一直非正式地使用了两组数据定义伪指令。我称之为“定义（defines）”和“预留（reserves）”。

`define` 伪指令为数据项提供名称、大小和值。而 `reserves` 仅提供名称和大小。以下是一些示例：

```assembly
rowcount dd 6
fileop    db 'w',
times    db 'Hey, what time is it? It's %s',10,0
```

```assembly
timediff resd 1 ; 为时间差预留 1 个整数（4字节）
timistr resb 40 ; 为时间字符串预留 40 字节
tmcopy  resd 9 ; 为 struct tm 预留 9 个整数字段
```

第一组是“定义”。你最常用的是 `DD`（定义双字）和 `DB`（定义字节）。`DB` 伪指令的独特之处在于它允许你轻松地定义字符数组，并被用于字符串常量。对于更高级的工作，NASM 提供了 `DW`（定义字）用于 16 位数值，`DQ`（定义四倍双字）用于 64 位数值，以及 `DT`（定义十字节）用于 80 位数值。这些较大的类型用于浮点运算，我不会在书中介绍这些。

第二组是“预留”。它们都以 "RES" 开头，后跟着指示预留项目大小的代码。NASM 定义了 `RESB`、`RESW`、`RESD`、`RESQ` 和 `REST` 分别对应字节、字、双字、四倍双字和十字节。通过在伪指令后指定整数常量，预留允许你分配任何类型的数组。`RESB 40` 分配 40 字节，而 `RESD 9` 在一个连续区域内分配 9 个双字（32 位数值）。

# 使用 MOVSDS 为 club 的 tm 结构制作副本

有时，能够保留一个 `tm` 结构的独立副本是很有方便的，特别是当你同时处理多个日期/时间值时。因此，在你用 `localtime` 将库的隐藏 `tm` 结构填充了日期/时间值后，你可以将该结构复制到程序 `[bss]` 段中分配的结构中。

执行此类复制是 `REP MOVSDS`（重复移动字符串双字）指令的直接用法。`MOVSDS` 几乎是神奇的：一旦你设置了指向想要复制的数据区域以及想要复制到的位置的指针，只需将区域的大小存储在 ECX 中，`REP MOVSDS` 会完成其余工作。在一次操作中，它将整个缓冲区从内存中的一个地方复制到另一个地方。

要使用 `MOVSD`，将源数据的地址（即要复制的数据）放入 ESI。将目标位置的地址（即要放置数据的地方）放入 EDI。将要移动的项目数放入 ECX。确保方向标志位（Direction flag）已清零（关于此点的更多信息，请参见第 11 章），然后执行 `REP MOVSD`：

```assembly
mov esi, eax          ; 将 eax 中的静态 tm 地址复制到 esi
mov edi, dword tmcopy ; 将本地 tm 的地址放入 edi
mov ecx, 9           ; 将移动的项目数放入 ecx
cld                   ; 清除方向标志
rep movsd             ; 重复执行 movsd
```

mov esi, eax          ; 将 eax 里的静态 tm 地址复制到 esi
mov edi, dword tmcopy ; 将本地 tm 的地址放入 edi
mov ecx, 9           ; 将移动的项目数放入 ecx
cld                   ; 清除方向标志
rep movsd             ; 重复执行 movsd

mov esi, eax          ; 将 eax 里的静态 tm 地址复制到 esi
mov edi, dword tmcopy ; 将本地 tm 的地址放入 edi
mov ecx, 9           ; 将移动的项目数放入 ecx
cld                   ; 清除方向标志
rep movsd             ; 重复执行 movsd

`MOVSD` 将库的 `tm` 结构复制到新分配的缓冲区。正如我在第 11 章中解释的那样，`REP` 前缀在每次移动时递减 ECX，直到 ECX 变为零。然后它停止。

人们可能会犯的错误是忘记 ECX 是要移动的项目数，而不是移动的字节数。

---

## 实现：TIMEST.ASM

```assembly
; 作者：Jeff Duntemann
; ：相关时间函数的演示，使用 NASM
; 使用以下命令编译：
; nasm -f elf timetest.asm
; gcc timetest.o -o timetest

[SECTION .data]
timemsg db "当前时间是: %s",0
oldtime dd 0

[SECTION .bss]
tmcopy resd 9 ; 为 tm 结构预留 9 个整数字段

[SECTION .text]
extern ctime
extern getchar
extern printf
extern localtime
extern time

global main ; 链接器寻找入口点

main:
    push ebp ; 为调试器设置栈帧
    mov ebp,esp
    push ebx ; 程序必须保存 ebp, ebx, esi, edi
    push esi
    push edi

    ; 此之前的所有内容都是模板代码；适用于所有应用程序！

    ; 使用 time 函数生成 time_t 日历值
    push dword 0 ; 向栈推入一个 32 位指针，因为
                 ; 我们不需要缓冲区。时间值
                 ; 返回在 eax。
    call time ; 在 eax 中返回日历时间
    add esp, byte 4 ; 调用后清理栈
    mov [oldtime],eax ; 将时间存在内存变量

    ; 使用 ctime 函数生成本地时间的字符串摘要
    push dword oldtime ; 推入日历时间的地址
    call ctime ; 在 eax 中返回 ASCII 字符串指针
    add esp, byte 4 ; 调用后清理栈

    push eax ; 将 ASCII 字符串指针推入栈
    push dword timemsg ; 推入显示消息的地址
    call printf ; 合并并显示两个字符串
    add esp, byte 8 ; 调用后清理栈

    pop edi
    pop esi
    pop ebx
    pop ebp
    ret
```

