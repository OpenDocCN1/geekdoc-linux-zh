
# loc_804841:

```
cmp     [esp+70h], 13h
le      short loc_804841B
mov     eax, 0
leave
retn
```

# main

实际变量的数据类型是整型指针。严格来说，在数据集传递给函数的时候，传递的数据就是指向第一个元素的指针，我们再根据这个指针就可以轻松算出每个元素的地址（即指针）。如果使用a[idx]的形式表示元素数组，其中idx是元素在数组里的排列序号（即索引），那么就可以通过数据第一个元素的地址、索引符号和数据量来得到每个元素的地址。

举个典型的例子：字符串常量量“string”是字符型数组，它的每一个元素都是const char*型数据。使用索引符号之后，我们就可以使用“string[i]”的形式表示字符串中的第i字符——正是C/C++表达式表示的方法！

## 18.2 ARM

Non-optimizing Kei 6/2013 (ARM) mode

```
EXPORT  main

_main
    STMFD   SP, {R4,LR}
    SUB     SP, SP, #0x50      ;分配20个int的存储空间

first loop
    MOV     R4, #0             ; i
    B       loc_4A0

loc_494
    MOV     R0, R4,LSL#1      ; R0=R4*2
    STR     R0, [SP,R4,LSL#2]  ; store R0 to SP+R4<<2 (same
    ADD     R4, R4, #1         ; i=i+1

loc_4A0
    CMP     R4, #20            ; i<20?
    BLT     loc_494            ;yes?loop again

second loop
    MOV     R4, #0             ; i
    B       loc_4C0

loc_4B0
    LDR     R2, [SP,R4,LSL#2]  ; (printf的第2个参数) R2*(SP+R4<<4) (等于*(SP+R4*4))
    MOV     R1, R4             ; (printf的第1个参数) R1=i
    ADR     R0, aADD           ; "%d]=%d\n"

BL          2printf
ADD         R4, #1      ; i=i+1
loc_4C4     CMP         R4, #20    ; i<20?
BLT         loc_4B0      ; yes, run loop body again
MOV         R0, #0      ; value to return
ADD         SP, SP, #0x50 ; 释放20个int的存储空间
LMF         SP!, {R4,PC}
```

单个整数数据32位（4字节）存储空间。以此类推，要存储20个int型数据就需要80(0x50)个字节的空间。函数末尾的“SUB, SP, 0x50”将释放的空间就是存储数组所用的空间。

在两个循环体内，循环控制变量都用R4寄存器。

在填充数组元素时，编译器使用左移位的运算“LSL#1”实现乘法“x2”，形成了“MOV R0, R4, LSL#1”指令。“STR R0 [...]”实现了将R0寄存器的值写入数组组。计算数组元素的原理：由于SP可代表数组的起始地址，R4代表变量i，可以通过左移2位得到i*4的偏移地址，再通过计算地址“SP+R4×4”即可推导出a[i]的指针地址。

在第二个循环里，“LDR R2, [SP, R4, LSL#2]”指令读取a[i]的值。

# Optimizing Kernel 2013 (Thread mode)

```
_main

    PUSH        R4,R5,LR
    ; allocate place for 20 int variables + one more variable
    SUB         SP, SP, #0x54

;第一个循环
    MOV         R0, #0      ; i
    MOV         R5, SP      ; pointer to first array element

loc_1CE
    LSL        R1,R0, #1   ; R1=i<<1 (same as i2)
    LSL        R2,R0, #2   ; R2=i<<2 (same as i4)
    ADDS        R0, R0, #1   ; i=i+1
    CMP         R0, #20     ; i<20?
    STR         R1, [R5,R2] ; store R1 to *(R5+R2) (same R5+i*4)
    BLT         loc_1CE     ; yes, i<20, run loop body again

;第二个循环
    MOVS        R4, #0      ; i=0

loc_1DC
LSLS R0, R4, #2 ; R0=i<<2 (same as i*4)
LDR R2, [R5,R0] ; load from (R5+R0) (same as R5+i*4)
MOVS R1, R4
ADR R0, aADD ; "a[%d]=%d\n"
BL 2printf
ADDS R4, R4, #1 ; i=i+1
CMP R4, #20 ; i<20?
BLT loc_1DC ; yes, run loop body again
MOVS R0, #0 ; value to return
; deallocate Chunk, allocated for 20 int variables + one more variable
ADD SP, SP, #0x54
POP {R4,R5,PC}
```

Thumb模式的程序和ARM模式的程序相似。在Thumb模式下，位移操作有特定的指令如LSL）。上述程序帮助Thumb模式的指令计算每个元素的地址。

另外，本例分配的空间比实际大了一些。这个数组里的最后4个字符不会被占用。

# Non-optimizing GCC 4.9.1 (ARM64)

指令清单18.3 Non-optimizing GCC 4.9.1 (ARM64)

```
.L0:\string "a[%d]=%d\n"
main:
    ; save FP and LR in stack frame:
    stp x29, x30, [sp, -112]
    ; set stack frame (FP=SP)
    add x29, sp, 0
    ; setting initial counter at 0 (ZR is the register holding zero):
    str wzr, [x29,108]
    ; jump to loop condition code:
    b L2
L3:
    ; load value of "i" variable:
    ldr w0, [x29,108]
    ; multiply it by 2:
    lsl w2, w0, #1
    ; find a place of an array in local stack:
    add x0, x29, 24
    ; load 32-bit integer from local stack and extend it to 64-bit:
    ldr w1, [x29,108]
    ; calculate address of element (x0+x1<<2=array address+i*4);
    str w2, [x0,x1,lsl #2]
    ; increment counter (i):
    add w0, w0, #1
    str w0, [x29,108]
.L2:
    ; check if finished:
    ldr w0, [x29,108]
    cmp w0, #19
    ; jump to L3 (loop body) if not:
    ble L3
.L4:
    ; second part of the function begins here.
    ; setting initial counter at 0. by the way, the same place in local stack was used for counter; because the same local variable (i) is being used for counter.
    str wzr, [x29,108]
.L5:
    ; calculate array address:
    add x0, x29, 24
    ; load value from the array at the address (x0+x1<<2) = address of i*4:
    ldr w1, [x29,108]
    ; load address of the "a[%d]=%d\n" string:
    adr x0, .LC0
    ; variable to pass to printf() as second argument:
    ldr w1, [x29,108]
    ; W2 still contains the value of array element which was just loaded.
    ; call printf():
    bl printf
    ; increment "i" variable:
    ldr w0, [x29,108]
    add w0, w0, 1
    str w0, [x29,108]
.L4:
    ; are we finished?
    ldr w0, [x29,108]
    cmp w0, #19
    ; jump to loop body begin if not:
    ble L5
    ; return 0
    mov w0, 0
    ; restore FP and LR:
    ldp x29, x30, [sp],112
    ret
```

# 18.1.3 MIPS

面向MIPS的编译器大量使用s寄存器。由于s寄存器属于临时寄存器，所以序言和尾部对这些寄存器进行了备份和还原。

# 指令清单18.4 Optimizing GCC 4.4.5 (IDA)

main:

```
var_70 = -0x70
var_68 = -0x68
var_14 = -0x14
var_10 = -0x10
var_C = -0xC
var_8 = -8
var_4 = -4
; function prologue:
lui $gp, (_gnu_local_gp >> 16)
addiu $sp, -0x80
la $gp, (_gnu_local_gp & 0xFFFF)
sw $ra, 0x80+var_4($sp)
sw $s3, 0x80+var_8($sp)
sw $s2, 0x80+var_C($sp)
sw $s1, 0x80+var_10($sp)
sw $s0, 0x80+var_14($sp)
sw $gp, 0x80+var_70($sp)
addiu $s1, $sp, 0x80+var_68
move $v1, $s1
move $v0, zero; that will be used as loop terminator; it was precalculated by GCC compiler at compile stage:
li $a0, 0x28 # (
```

loc_34:
; store value memory:

sw $v0, 0($v1)
; increase value to be stored by 2 at each iteration:
addiu $v0, 2
; loop terminator reached?
bne $s0, $a0, loc_34
; add 4 to address anyway:
addiu $v1, 4
; array filling loop is ended
; second loop begin
la $s3, $LC0 # "a[%d]=%d\n"
; "i" variable will reside in $s0:
move $s0, zero
li $s2, 0x14

loc_54:
; call printf():

lw $t9, (printf & 0xFFFF) ($gp)
lw $a2, 0($sp)
move $a1, $s0
move $a0, $s3
jalr $t9

; increment "i":

addiu $s0, 1
lw $gp, 0x80+var_70($sp)
; jump to loop body if end is not reached:
```

![](img/a13a81a53f805f55074b2e5d2ec754b6_402_0.png)

```
bne $s0, $s2, loc_54
```

; move memory pointer to the next 32-bit word:
addiu $s1, 4

; function epilogue
lw $ra, 0x80+var_4($sp)
lw $v0, 0
sw $s3, 0x80+var_8($sp)
sw $s2, 0x80+var_C($sp)
sw $s1, 0x80+var_10($sp)
sw $s0, 0x80+var_14($sp)
sw $gp, 0x80+var_70($sp)
addiu $sp, $sp, 0x80
ret
```
