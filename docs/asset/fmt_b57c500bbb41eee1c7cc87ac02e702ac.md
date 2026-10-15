
// 范围 0..11

```c
const char* get_month(int month) {

    return month1[month];

}
```

### 18.5.1 x64

优化 MSVC 2013 x64

```asm
_DATA SEGMENT

month1 DQ FLAT:January

DQ FLAT:February

DQ FLAT:March

DQ FLAT:April

DQ FLAT:May

DQ FLAT:June

DQ FLAT:July

DQ FLAT:August

DQ FLAT:September

DQ FLAT:October

DQ FLAT:November

DQ FLAT:December

DB 'January', 00H

DB 'February', 00H

DB 'March', 00H

DB 'April', 00H

DB 'May', 00H

DB 'June', 00H

DB 'July', 00H

DB 'August', 00H

DB 'September', 00H

DB 'October', 00H

DB 'November', 00H

DB 'December', 00H

_DATA ENDS

_month = 8 PROC

get_month1

    movsx ra, ecx

    lea rcx, OFFSET FLAT:month1

    mov rax, QWORD PTR [rcx+8]

    ret

get_month1 ENDP
```

上述程序的功能：

- 第一条指令将32 位数值连同其符号扩展（sign-extension）为64 位整数数据，再存储于 `RAX` 寄存器中。`ECX` 存储的“月份”信息是32 位整数。因为后面还要进行64 位运算，所以把输入转换为64 位整数。
- 然后函数把指针的地址存储于 `RCX` 寄存器。
- 最后，函数的输入变量（`month`）的值乘以8，再与指针的地址相加。因为是64 位系统的后缀，每个地址（即指针）的数据用64 位（即8字节）。所以指针表中的每个元素占据8字节空间。因此，最终字符串的地址要加上 `month*8`。`MOV`指令完成了字符串地址的计算，而且完成了指针的查询。在输入值为1 时，函数将返回字符串“February”的指针地址。

编译器的优化结果是直接的：

```asm
movsx rdi, edi

mov rax, QWORD PTR month1[0+8]

ret
```

### 18.5.2 32位MSC

使用32位MSVC 编译器上述程序可以如下所示的指令。

优化 MSVC 2013 x86

```asm
_month = 8

_get_month1 PROC

    mov eax, [esp+4]*4

    mov eax, esp

    ret

get_month1 ENDP
```

32位系统的后缀，每个指针数据4字节。所以指针表中的每个元素占据4字节空间。

### 18.5.3 32位

优化 GCC 4.5 (IDA)

```asm
get_month:

    ; load address of table into $v0:
    la $v0, month

    ; take input value and multiply it by 4:
    sll $a0, 2

    ; sum up address of table and multiplied value:
    addu $a0, $v0

    ; load element at this address into $v0:
    lw $v0, 0($a0)

    return:
    jr $ra
    or $at, $zero ; branch delay slot
```

```asm
.data #rodata.str.rel
.global month
    word january # "January"
    word february # "February"
    word march # "March"
    word april # "April"
    word may # "May"
    word june # "June"
    word july # "July"
    word august # "August"
    word september # "September"
    word october # "October"
    word november # "November"
    word december # "December"
```

```asm
aJanuary:
    .ascii "January"
afebruary:
    .ascii "February"
aMarch:
    .ascii "March"
aApril:
    .ascii "April"
aMay:
    .ascii "May"
aJune:
    .ascii "June"
aJuly:
    .ascii "July"
aAugust:
    .ascii "August"
aSeptember:
    .ascii "September"
aOctober:
    .ascii "October"
November:
    .ascii "November"
December:
    .ascii "December"
```

### 18.5.4 ARM

优化 GCC 4.5 (ARM)

```asm
get_month:
    adrp x1, :month
    add x1, x1, :lo
    ldr w0, [x1, x0, lsl #2]
    ret
```

```asm
.data .rodata.str.rel
.global month
    word january # "January"
    word february # "February"
    word march # "March"
    word april # "April"
    word may # "May"
    word june # "June"
    word july # "July"
    word august # "August"
    word september # "September"
    word october # "October"
    word november # "November"
    word december # "December"
```

```asm
aJanuary:
    .ascii "January"
afebruary:
    .ascii "February"
aMarch:
    .ascii "March"
aApril:
    .ascii "April"
aMay:
    .ascii "May"
aJune:
    .ascii "June"
aJuly:
    .ascii "July"
aAugust:
    .ascii "August"
aSeptember:
    .ascii "September"
aOctober:
    .ascii "October"
November:
    .ascii "November"
December:
    .ascii "December"
```

### 18.5.5 Thumb模式

优化 Xcode 4.6.3 (Thumb-2模式)

```asm
PUSH        [R4-R7,LR]
ADD         R7, SP,#0xC
STR.W       R8, [SP,#0xC+var_10]!
SUB         SP, SP,#0x54
MOVW        R0=#ObjC_mettype, "objc_mettype"
MOVS        R2,#0
MOVT.W      R2,#1
MOVS        R5,#0
ADD         R0, PC
LDR.W       R8, [R0]
LDR.W       R0, [R8]
STR         R0, [SP,#0x64+var_canary]
MOVS        R2,#2
STR         R2, [SP,#0x64+var_64]
STR         R0, [SP,#0x64+var_60]
MOVS        R0,#4
STR         R0, [SP,#0x64+var_5C]
MOVS        R0,#6
STR         R0, [SP,#0x64+var_58]
```
