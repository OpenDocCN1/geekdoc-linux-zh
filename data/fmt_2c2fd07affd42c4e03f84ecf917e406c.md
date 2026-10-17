
# 为 Linux 编码

“Unix 纪元”开始于世界标准时间 1970 年 1 月 1 日 00:00。每流逝的每一秒都会给这个值加一。当你通过 C 库读取当前时间或日期时，你将获取该数字的当前值。

这个数字被称为 `time_t`。`time_t` 值目前处于 900,000,000 以上，并在 2001 年 9 月 9 日 UTC 时间 7:46:40 翻变为 10 位（自 1970 年 1 月 1 日以来的 10 亿秒）。这不是短期内发生的千年危机式的危险，因为即使是 32 位无符号整数也可以表示超过 20 亿的数量，甚至表示超过 40 亿。此外，实现良好的 C 库根本不会假定这是一个 32 位数值。因此，当整个数值在 2069 年翻转时，我们可能已经在使用至少 64 位的值来表示年份了。如果我们那时还没有彻底解决它，那我们就该死于宇宙学家所预测的宇宙挤缩（Cosmic Crunch）中了。

`time_t` 值仅仅是一个任意的秒数计数，本身并没有告诉你什么，尽管它可能用于计算以秒为单位的通过时间。标准 C 库实现的另一个标准数据类型要有用得多。`tm` 结构（通常称为 `struct`，是 Pascal 语言的人会称之为 `record`）是九个 32 位值的组合，它们以单独且有用的部分表示当前时间和日期，如表 13.3 所示。注意，尽管 `struct`（或 `record`）名义上是不同值的组合，与当前的 x86 Linux 实现中不同，`tm` 值更像是一个数组或数据表，因为所有元素的大小相同，都是 32 位（即 4 字节）。我在表 13.3 中这样描述它，通过包含一个该结构中每个元素相对于结构起始位置的偏移量。这允许你使用指向结构起始的指针和相对于起始的偏移量来定位结构中的任何给定元素。

C 库函数可以将 `time_t` 值转换为 `tm` 值，反之亦然。我在书中涵盖了其中几个函数，但它们都非常直观，一旦你彻底掌握了 C 调用约定，你就应该能够为其中任何一个函数编写出汇语言调用机制。

# 从系统时钟获取时间 t 值

在 Unix 系统中，任何单秒（至少是 1970 年 1 月 1 日之后的秒）都可以用 32 位无符号整数表示。

# 表 13.3 tm 结构中包含的值

| 字节偏移 | C 库名称 | 定义 |
|---|---|---|
| 0 | `tm_sec` | 之后的秒数 |
| 4 | `tm_min` | 小时后的分钟，从 0 开始 |
| 8 | `tm_hour` | 一天的小时，从 0 开始 |
| 12 | `tm_mday` | 月中的日期，从 1 开始 |
| 16 | `tm_mon` | 年中的月份，从 0 开始 |
| 20 | `tm_year` | 自 1900 年以年份，从 0 开始 |
| 24 | `tm_wday` | 自周日以来的几天，从 0 开始 |
| 28 | `tm_yday` | 年中的几天，从 0 开始 |
| 32 | `tm_isdst` | 夏令时标志 |

获取当前时间的值是通过调用 `time` 函数完成的：

```
- push dword 0           ; 压入 0
- call time              ; 在 eax 中返回时间值
- add esp, byte 4         ; 调用后清理栈
- mov [oldtime],eax      ; 将时间值存入内存
```

`time` 函数可能在两个地方返回时间值：`EAX`，或者在某个处的缓冲区中。为了将时间值放在缓冲区，你必须在栈上压入空指针。

```
- push dword 0           ; 压入空指针
- call time              ; 在 eax 中返回时间值
- add esp, byte 4         ; 调用后清理栈
```

这看起来很常规，但这里有一点你必须注意，因为它有点特殊：你传递给 `ctime` 的 `time_t` 值的地址，而不是值本身！你习惯于将 32 位整数值本身压入栈中供 `printf` 显示。这里不是这样。`time_t` 值目前在 Linux 上表示为 4 字节整数，但并没有保证它将永远如此。因此，为了保持灵活性（并确保 Unix 可以继续使用数千年甚至数百万年，天哪），C 库要求当前时间的指针。也许在千年后它将是一个双字……谁知道呢？

# 将 time_t 值转换为格式化字符串

在写本文时，`time_t` 高达 950,000,000。（想到自我高中毕业以来已经过去了这么多秒，真可怕！）光 `time_t` 本身不能告诉你太多信息。C 库包含一个可以返回给定 `time_t` 的格式化字符串指针的函数。这就是 `ctime` 函数。它返回一个指向某处字符串的指针。该字符串格式如下：

```
Thu Dec 2 13:59:20 1999
```

第一个字段是星期的三字符代码，后面是月份的三字符代码和日期的两位字段。时间以 24 小时格式跟随，年份在最后。为了起见（尽管有时这是个麻烦），字符串以换行符结束。

这是你如何使用 `ctime`：

```
push dword oldtime   ; 压入时间值的地址
call ctime              ; 在 eax 中返回 ASCII 时间字符串
add esp, byte 4         ; 调用后清理栈
```

这看起来很常规，但这里有一点你必须注意，因为它有点特殊：你传递给 `ctime` 的 `time_t` 值的地址，而不是值本身！你习惯于将 32 位整数值本身压入栈中，供 `printf` 显示。这里不是这样。`time_t` 值目前在 Linux 上表示为 4 字节整数，但并没有保证它将永远如此。

# 生成独立的本地时间值

C 库还提供了一个函数，可以将日期和时间的各个部分拆分为单独的值，以便你单独或以各种组合使用。该函数是 `localtime`，给它一个 `time_t` 值，它会将日期和时间拆分为表 13.3 所示的 `tm` 结构字段。

# 汇编语言分步详解

```assembly
push dword oldtime ; 将日历时间值的地址推入栈
call localtime      ; 在 eax 中返回指向静态时间结构的指针
add esp, byte 4    ; 调用后清理栈空间
```

在这里，`oldtime` 是一个 `time_t` 类型的值。给定此值，`localtime` 在 `EAX` 中返回（这种方式类似于 `ctypes`）——一个指向运行时库中某处 `tm` 结构的指针。通过将此指针作为基地址，你可以使用相对于基地址的常量偏移量来访问结构中的字段（此处显示存储在 `EAX` 中）：

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

执行此类复制是 `REP MOVSDS`（重复移动字符串双字）指令的直接用法。`MOVSDS` 几乎是神奇的：一旦你设置了指向想要复制的数据区域以及想要复制到的位置的指针，只需将区域的大小存储在 `ECX` 中，`REP MOVSDS` 会完成其余工作。在一次操作中，它将整个缓冲区从内存中的一个地方复制到另一个地方。

要使用 `MOVSD`，将源数据的地址（即要复制的数据）放入 `ESI`。将目标位置的地址（即要放置数据的地方）放入 `EDI`。将要移动的项目数放入 `ECX`。确保方向标志位（Direction flag）已清零（关于此点的更多信息，请参见第 11 章），然后执行 `REP MOVSD`：

```assembly
mov esi, eax          ; 将 eax 中的静态 tm 地址复制到 esi
mov edi, dword tmcopy ; 将本地 tm 的地址放入 edi
mov ecx, 9           ; 将移动的项目数放入 ecx
cld                   ; 清除方向标志
rep movsd             ; 重复执行 movsd
```

```assembly
mov esi, eax          ; 将 eax 里的静态 tm 地址复制到 esi
mov edi, dword tmcopy ; 将本地 tm 的地址放入 edi
mov ecx, 9           ; 将移动的项目数放入 ecx
cld                   ; 清除方向标志
rep movsd             ; 重复执行 movsd
```

```assembly
mov esi, eax          ; 将 eax 里的静态 tm 地址复制到 esi
mov edi, dword tmcopy ; 将本地 tm 的地址放入 edi
mov ecx, 9           ; 将移动的项目数放入 ecx
cld                   ; 清除方向标志
rep movsd             ; 重复执行 movsd
```

`MOVSD` 将库的 `tm` 结构复制到新分配的缓冲区。正如我在第 11 章中解释的那样，`REP` 前缀在每次移动时递减 `ECX`，直到 `ECX` 变为零。然后它停止。

人们可能会犯的错误是忘记 `ECX` 是要移动的项目数，而不是移动的字节数。

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

## 汇编语言分步详解

```assembly
mov esi, eax            ; 将静态 tm 的地址从 eax 复制到 esi
mov edi, dword tmcopy   ; 将本地 tm 副本地址放入 edi
mov ecx,9               ; 在 Linux 中，结构体的大小为 9 个字
cld                     ; 清零方向位为 0，以便使用向上内存
rep movsd               ; 将静态 tm 结构体复制到 .bss 中的本地副本
```

```assembly
; 显示 tm 结构体中的一个字段=====================
mov edx, dword [tmcopy+20] ; 年值位于偏移 20 字节处
push edx                  ; 将值压入栈
push dword yrmsg          ; 将基础字符串地址压入栈
call printf              ; 使用 printf 显示字符串和年份值
add esp, byte 8          ; 清理栈
```

```assembly
; 等待几秒让用户按回车，以便我们时间差===
call getchar
```

```assembly
; 使用 difftime 计算程序运行以来经过的秒数=======
push dword 0             ; 推入空指针；我们将获取 eax 中的值
call time               ; 获取当前时间值；返回在 eax 中
add esp, byte 4          ; 清理栈
mov [newtime],eax       ; 保存新时间值
```

```assembly
sub eax, [oldtime]      ; 计算时间差
mov [timediff],eax      ; 保存时间差值
```

```assembly
push dword [timediff] ; 将秒差压入栈
push dword elapsed       ; 将已长时间字符串地址压入栈
call printf              ; 显示已长时间
add esp, byte 8          ; 清理栈
```

```assembly
; 之后的所有内容都是模板代码；将其用于所有普通应用！
pop edi                  ; 恢复保存的寄存器
pop esi
pop ebx
mov esp,ebp             ; 返回前销毁栈帧
pop ebp
ret                     ; 返回控制到 Linux
```

```assembly
.data        ; 包含初始化数据的段
```

```assembly
.bss        ; 包含未初始化数据的段
```

```assembly
oldtime res 1   ; 为时间值预留 3 个整数（双精度）
```
