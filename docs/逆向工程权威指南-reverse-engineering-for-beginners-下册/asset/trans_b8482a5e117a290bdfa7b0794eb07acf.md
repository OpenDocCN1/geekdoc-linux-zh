

## 第24章 32位系统处理64位数据

32位系统的通用寄存器GPR都只能容纳32位数据，所以这种平台必须64位数据转换为对32位数据才能进行运算。[1]

## 24.1 64位返回值

本节围绕调度程序进行演示。

```c
#include <stdint.h>

uint64_t f() {
    return 0x1234567890ABCDEF;
};
```

### 24.1.1 x86

32位系统用寄存器组合EDX:EAX来回传64位值。

> 指令清单24.1 Optimizing MSVC 2010

```assembly
_f PROC
    mov     eax, -1867788817    ; 90abcdefH
    mov     edx, 305419896     ; 12345678H
    ret             0
_f ENDP
```

### 24.1.2 ARM

ARM系统用寄存器组合R0-R1返回64位值。其中，返回值的高32位存储在R0寄存器中，低32位存储于R1寄存器中。

> 指令清单24.2 Optimizing Keil 6/2013 (ARM mode)

```assembly
||f|| PROC
LDR r0,[L0.12]
LDR r1,[L0.16]
BX lr
ENDP
|L0.12|
|L0.16|
DCD 0x90abcdef
DCD 0x12345678
```

### 24.1.3 MIPS

MIPS系统使用V0-V1 ($2-$3)寄存器返回64位值。其中，返回的高32位存储在V0 ($2)寄存器中，低32位存储于V1 ($3)寄存器中。

> 指令清单24.3 Optimizing GCC 4.4.5 (assembly listing)

```assembly
li $3,-1867841536 #0xffffffff90ab0000
li $2,305397760 #0x12340000
ori $3,$3,0xcdef
j $31
ori $2,$2,0x05678
```

> 指令清单24.4 Optimizing GCC 4.4.5 (IDA)

```assembly
lui $v1,0x90AB
lui $v0,0x1234
li $v1,0x90ABCDEF
jr $ra
li $v0,0x12345678
```

## 24.2 参数传递及加减运算

本节围绕下列程序进行演示。

```c
#include <stdint.h>
uint64_t f_add (uint64_t a, uint64_t b)
{
  return a+b;
}

void f_add_test () {
  #ifdef GNUC
  printf("%lld\n", f_add(12345678901234, 234567889012345));
  #else
  printf("%I64d\n", f_add(12345678901234, 234567889012345));
  #endif
}

uint64_t f_sub(uint64_t a, uint64_t b) {
  return a-b;
}
```

### 24.2.1 x86

使用MSVC 2012 (启用选项/Ox /Gb1) 编译上述程序，可得到如下的代码。

> 指令清单24.5 Optimizing MSVC 2012 /Gb1

```assembly
_a = 8      ; size = 8
_b = 16      ; size = 8
_f_add      PROC
       mov eax, DWORD PTR _a$[esp-4]
       add eax, DWORD PTR _b$[esp-4]
       mov edx, DWORD PTR _a$[esp]
       adc edx, DWORD PTR _b$[esp]
       ret
_f_add      ENDP
```

```assembly
_f_add_test PROC
       push    5461            ; 00001555H
       push    1972608889      ; 75939f79H
       push    2874            ; 00000b3AH
       push    142892530      ; 73ce2ff_subH
       call    f_add
       push    edx
       push    eax
       push    OFFSET $SG1436  ; '%I64d', 0a, 00H
       call _printf
       add esp, 28
       ret
f_add_test ENDP
```

```assembly
_f_sub PROC
mov eax, DWORD PTR _a$[esp-4]
sub eax, DWORD PTR _b$[esp-4]
mov edx, DWORD PTR _a$[esp]
sbb edx, DWORD PTR _b$[esp]
ret
```

在f_add_test()函数中，每个64位数据都被拆分为32位数据。在内存中，高32位在前（地址），低32位在后。加法运算的方法相同。在进行加法运算时，对低32位相加如果产生了CF位，然后ADC指令对高32位进行运算。此时CF位为1，再把高32位加到结果上。减法运算也是分开进行的。第一次减法运算可能影响CF位。在32位系统中，函数返回64位数据都使用EDX:EAX。对于f_add()返回值传递给printf()函数，就可以清晰地观测到现象。使用GCC 4.8（启用选项-fno-inline）编译上述程序，得到如下的代码。

> 指令清单24.6 GCC 4.8 -fno-inline

```assembly
_f_add:
mov eax, DWORD PTR _a$[esp-4]
mov edx, DWORD PTR _b$[esp-4]
add eax, DWORD PTR _a$[esp]
adc edx, DWORD PTR _b$[esp]
ret
```

```assembly
_f_add_test:
sub esp, 28
mov DWORD PTR [esp+8], 1972608889 ; 75939f79
mov DWORD PTR [esp+12], 5461 ; 00001555
mov DWORD PTR [esp], 142892530 ; 73ce2ff_subH
mov DWORD PTR [esp+4], 2874 ; 0000b3AH
call f_add
mov DWORD PTR [esp+4], eax
mov DWORD PTR [esp+8], edx
mov DWORD PTR [esp+12], "%lld"
call _printf
ret
```

```assembly
_f_sub:
mov eax, DWORD PTR _a$[esp-4]
sub eax, DWORD PTR _b$[esp-4]
mov edx, DWORD PTR _a$[esp]
sbb edx, DWORD PTR _b$[esp]
ret
```

GCC的编译结果和MSVC相同。

### 24.2.2 ARM

> 指令清单24.7 Optimizing Keil 6/2013 (ARM mode)

```assembly
f_add:
ADDS r0,r2
ADC r1,r3
BX lr
```

```assembly
f_sub:
SUBS r0,r2
SBC r1,r3
BX lr
```

```assembly
f_add_test:
PUSH {r4, lr}
LDR r2,[L0.68] ; 0x7593f79
LDR r3,[L0.72] ; 0x00001555
LDR r0,[L0.76] ; 0x73ce2ff
LDR r1,[L0.80] ; 0x0000b3a
BL f_add
POP {r4, lr}
MOV r2,r0
MOV r3,r1
ADR r0,[L0.84] ; "%lld"
```

```assembly
|L0.68|
|L0.72|
|L0.76|
|L0.80|
DCD 0x7593f779
DCD 0x00001555
DCD 0x73ce2ff
DCD 0x0000b3a
```

第一个64位值拆分到R0和R1寄存器，第二个64位值存储于R2和R3寄存器。ARM平台的指令集可以进行加法运算的ADC指令和减法运算的SBC指令。注意的是：对64数据的低32位进行加减运算，需要使用ADDS和SUBS指令。指令名称中的S代表会设置进位（Carry Flag）。它们设置的进位将被高32位运算的ADC/SBC指令读取并纳入结果之中。没有S后的ADD和SUB指令则设置进位位。

### 24.2.3 MIPS

> 指令清单24.8 Optimizing GCC 4.4.5 (IDA)

```assembly
f_add:
; $a0 - high part of a
; $a1 - low part of a
; $a2 - high part of b
; $a3 - low part of b
    addu $v1,$a3,$a1 ; sum up low parts
    addu $a0,$a2,$a0 ; sum up high parts
    ; will carry generated while summing low parts?
    ; if yes, set $v0 to 1
    sltu $v0,$v1,$a3
    jr $ra
    ; add 1 to high part of result if carry should be generated:
    addu $v0,$a0 ; branch delay slot
```

```assembly
f_sub:
; $a0 - high part of a
; $a1 - low part of a
; $a2 - high part of b
; $a3 - low part of b
    subu $v1,$a1,$a3 ; subtract low parts
    subu $v0,$a0,$a2 ; subtract high parts
    ; will carry generated while subtracting low parts?
    ; if yes, set $v0 to 1
    stu $v1,$v1
    jr $ra
    ; subtract 1 from high part of result if carry should be generated:
    addiu $v0,$v0 ; branch delay slot
```

