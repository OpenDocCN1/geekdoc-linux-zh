
在 Linux 2.6 内核的编译选项中，设定了寄存器选项“mregparm=3”。

这个选项决定编译器首先通过 EAX、EDX 和 ECX 寄存器传递函数所需的 3 个参数，再通过传递剩余的参数。如果参数的总数不足3，它只会用到部分通用寄存器。

在 Ubuntu 的 Linux Kernel 2.6.31 中，并用“make vlinux”指令编译，然后使用 IDA 打开程序，查找函数 `do_fil_open()`。这个函数的开头部分大体是这样的：

# 指令清单19.6 do_fil_open() (Linux kernel 2.6.31)

```
do_fil_open:

    push    ebp
    mov     ebp, esp
    push    edi
    push    esi
    push    ebx
    mov     ebx, ecx
    add     ebx, 1
    sub     esp, [ebp+arg_4] ; acc_mode (5th arg)
    test    bl, 3
    mov     [var_80], eax; dfd (1th arg)
    mov     [var_7C], edx; pathname (2th arg)
    mov     [var_78], ecx; open_flag (3rd arg)
    jnz     short loc_C01EF68
    mov     ebx, ecx
```

函数参数个数就把 3 个寄存器里的值存储在。若如此，之后就会出现寄存器紧张。

我们再来看 `do_fil_open()` 函数的另外一段代码：

# 指令清单19.7 do_fil_open() (Linux kernel 2.6.31)

```
loc_C01EFB4:
    test    bl, 40h ; XREF: do_fil_open+4F
    jnz     loc_C01EF80 ; O_CREAT
    mov     edi, ebx
    shr     edi, 1h
    xor     edi, 1
    and     edi, 1
    test    ebx, 100h
    jz      short loc_C01EF6D
    or      edi, 2
```

`O_CREAT` 的值就是 0x40。`TEST` 指令检查 `open_flag` 是否存在 0x40 标志位。如果是1，则会触发一条 `JNZ` 指令。

## 19.12 ARM

在 Linux Kernel 3.8 系统里，`O_CREAT` 的检查有所不同。

# 指令清单19.8 Linux kernel 3.8

```c
struct file *do_fil_open(int dfd, char *pathname)
{
    ...
    return path_open(dfd, pathname, nd, flags | LOOKUP_RCU);
}
```

```c
static struct file *path_open(int dfd, char *pathname,
    struct nameidata *nd, struct open_flags *op, int flags)
{
    return do_last(nd, op, &opened);
}
static int do_last(struct nameidata *nd, struct path *path,
    struct file *file, struct open_flags *op,
    int *opened, char *name)
{
    if (!(*op & O_CREAT)) {
        ...
        error = lookup_fast(nd, path, &inode);
    } else {
        error = complete_walk(nd);
    }
}
```

使用 IDA 打开 ARM 模式的内核，可以看到 `do_last()` 函数的代码如下。

# 指令清单19.9 do_last() (vmlinux)

```
...
.text:C0169EA8  MOV R9, R3 ; R3 - (4th argument) open_flag
...
.text:C0169ED4  LDR R6, [R9] ; R6 - open_flag
```

...

```
.text:C019F68  TST R6, #040 ; jumpable C019F00 default
.text:C019F6C  BNE loc_C01A128
.text:C019F70  LDR R2, [R4,#0x10]
.text:C019F74  ADD R12, #8
.text:C019F78  LDR R3, [R4,#xC]
.text:C019F7C  MOV R0, R4
.text:C019F80  STR R12, [R11,#var_50]
.text:C019F84  LDRB R3, [R2,R3]
.text:C019F88  MOV R2, R8
.text:C019F9C  CMP R3, #0
.text:C019F90  ORNE R1, #1
.text:C019F94  STNE R1, [R4,#0x24]
.text:C019F98  ANDS R3, #6, #0x200
.text:C019F9C  MOV R1, R2
.text:C019FA00  LDR R3, [R4,#0x24]
.text:C019FA04  ANDNE R3, #1
.text:C019FA08  STRNE R3, [R11,#var_54]
.text:C019FB00  SUB R3, [R11,#var_38]
.text:C019FB04  BL lookup_fast
.text:C016A128 loc_C01A18 ; XREF: do_last+DC
.text:C016A128 MOV R0, R4
.text:: BL complete_walk
```

`TEST` 指令与 x86 平台相同。显而易见，程序在某条件下调用 `lookup_fast()`，而在另一个条件下调用 `complete_walk()`。这种行为 `do_last()` 函数在这里的汇编 `O_CREAT` 等于 0x40。

## 19.2 设置 / 清除

本节围绕这个程序进行：

```c
#include <stdio.h>

#define IS_SET(flag, bit) ((flag) & (bit))
#define SET_BIT(var, bit) ((var) |= (bit))
#define REMOVE_BIT(var, bit) ((var) &= ~(bit))

int f(int a) {
    int rt = a;
    SET_BIT(rt, 0x4000);
    REMOVE_BIT(rt, 0x200);
    return rt;
}
int main() {
    f(0x12340678);
}
```

### 19.2.1 x86 Non-optimizing

经过 MSVC（未优化）编译上述程序，得到所示指令指令清单19.10 MSVC

```
rt = -4          ; size = 4
a = 8           ; size = 4
_f PROC
    push    ebp
    mov     ebp, esp
    push    ecx
    mov     eax, PTR [ebp+8]
    mov     [ebp-4], eax
    mov     ecx, PTR [ebp-4]
    or     ecx, ecx ; 0000040H
    mov     eax, PTR [ebp-4]
    mov     eax, efffffff
    and     edx, ed5
    mov     [ebp-4], eax
    mov     eax, PTR [ebp-4]
    mov     esp, ebp
    pop     ebp
    ret
_f END
```

`OR` 指令是逐位或指令，用来指定位置上，如果立即数的某位为 1，`OR` 指令会保留寄存器位的值；如果立即数的某位为 0，`OR` 指令就会把寄存器位设置为 0。按照位掩码（bitmask）的方式理解就会很容易记住这些的作用。

用 OllyDbg 打开程序，可以清楚地看到常量的位：

0x200 的二进制数是 000000000000000100000000，第 9 位是 1。

0x200 的逻辑运算结果是 0xFFFFFFDD（111111111111111101111111）。

0x4000 的第 14 位是 1。图 19.1 所示，输入变量 0x12340678（1001000110100000000100011110000）。

![](img/a13a81a53f80f55074b2e5d2ec754b469_0.png)

图19.1 OllyDbg: 寄存器输入变量执行 OR 指令的情形如图19.2 所示。

# CPU - main thread, module_set_reset

| | | | Registers (FPU) |
|---|---|---|---|
| 00E31000 | 55 | PUSH EAX | ECX: 1244A673 |
| 00E31001 | 8B EC | MOV EAX, ESP | EAX: 00000000 |
| 00E31002 | 51 | PUSH ECX | ESI: F0E7C378 |
| 00E31003 | 89 D4 | MOV EAX, PTR [ebp-C] | ESP: 00000000 |
| 00E31004 | 89 C7 | MOV EDI, PTR [ebp-B] | EBP: 00000000 |
| 00E31005 | 89 C4 | MOV EAX, PTR [ebp-C] | EDI: 00E33378 |
| 00E31006 | 89 D5 | MOV EDI, PTR [ebp-B] | EIP: 00E31013 |
| 00E31007 | B8 FF FF FF | MOV EAX, FFFFFFFF | 00001232 (0xFF) |
| 00E31008 | 89 D4 | MOV EAX, PTR [ebp-C] | 00000232 (0xFFFFFF) |
| 00E31009 | 83 79 00 00 00 | CMP EAX, 0x40000000 | 00000232 (0xFFFFFF) |
| 00E3100A | B8 FF FF FF | MOV EAX, FFFFFFFF | 00000232 (0xFFFFFF) |
| 00E3100B | 89 D4 | MOV EAX, PTR [ebp-C] | 00000232 (0xFFFFFF) |
| 00E3100C | 50 | PUSH EAX | 00000000 ERROR_SUCCESS |
| 00E3100D | 59 | POP EAX | 00000226 (NE/1,A/S) |
| 00E3100E | C3 | RET | |
| 00E3100F | 90 | NOP | ECX=12340678 |

| Address | Hex | ASCII |
|---|---|---|
| 00FFC000 | FF FF FF 01 00 00 39 07 F0 00 | * |
| 00FFC008 | FF FF FF 01 00 00 40 20 53 63 64 00 00 | HI |
| 00FFC010 | 00 00 00 00 48 4A 00 53 64 65 00 00 | J |
| 00FFC018 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | |
| 00FFC020 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | | |
| 00FFC028 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | RETURN from set, |
| 00FFC030 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | | |
| 00FFC038 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | | |
| 00FFC040 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | | | | |
| 00FFC048 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | "null" |
| 00FFC050 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | | | | |
| 00FFC058 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | K |

执行 OR 指令的时候，第 15 位赋值为 1。由于没有优化，程序中有些指令。如图 19.3 所示。

# CPU - main thread, module_set_reset

| | | | Registers (FPU) |
|---|---|---|---|
| 00E31000 | 55 | PUSH EAX | EAX: 1249670 |
| 00E31001 | 8B EC | MOV EBP, ESP | EDX: 1234678 |
| 00E31003 | 89 D4 | MOV EDI, PTR [ebp-C] | EAX: 00000236 |
| 00E31006 | 89 D1 | MOV ESI, PTR [ebp-F] | ESP: 00000236 |
| 00E31009 | 89 F2 | MOV EAX, PTR [ebp-F] | ESI: 00E38878 |
| 00E3100C | 81 09 00 00 00 | AND EDI, DWORD PTR [ebp-C] | EIP: 00E31019 |
| 00E31012 | 89 F5 | MOV EBP, PTR [ebp-C] | | |
| 00E31015 | B2 FF FF FF | PUSH EDI | 00033231 (0xFFFFFF) |
| 00E31018 | 84 FC | TEST EDI, EDI | 00033231 (0xFFFFFF) |
| 00E3101B | 75 D0 | JNE | 00033231 (0xFFFFFF) |
| 00E3101E | 50 | PUSH EBP | |
| 00E31021 | C3 | RET | 00000226 (ERROR_SUCCESS) |

| Address | Hex | ASCII |
|---|---|---|
| 00E30000 | FF FF FF 01 00 00 39 07 F0 00 | * |
| 00E30008 | FF FF FF 01 00 00 40 20 53 63 64 00 00 | HI |
| 00E30010 | 00 00 00 00 48 4A 00 53 64 65 00 00 | J |
