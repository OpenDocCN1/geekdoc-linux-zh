

```text
.text:00000000 var_1 = -0x10
.text:00000004 var_4 = -4
.text:00000000
; 函数序言:
.text:00000000 lui $gp, (_gnu_local_gp >> 16)
.text:00000004 addiu $sp, $sp,-0x20
.text:00000008 la $gp, (_gnu_local_gp & 0xFFFFF)
.text:0000000c sw $ra, 0x20+var_4($sp)
.text:00000010 sw $gp, 0x20+var_10($sp)
; 加载 printf() 的地址:
.text:00000014 lw $9, (printf & 0xFFFFF)($gp)
; 加载字符串地址并设置 printf 的第1参数:
.text:00000018 la $a0, $L0 # "a=%d; b=%d; c=%d"
; 设置 printf 的第2个参数:
.text:00000020 li $a1, 1
; 设置 printf 的第3个参数:
.text:00000024 li $a2, 2
; 调用 printf():
.text:00000028 jalr $9
; 设置 printf 的第4个参数 (分支槽位):
.text:0000002c li $a3, 3
; 函数尾声:
.text:00000030 lw $ra, 0x20+var_4($sp)
; 返回值为 0:
.text:00000034 move $v0, $zero
; 返回:
.text:00000038 jr $ra
.text:0000003c addiu $sp, $sp,0x20 ; 分支槽位
```

IDA没有显示0x1C的指令。实际上0x18是“LUI”和“ADDIU”两条指令，IDA把它们显示为单条的指令，占用了8个字节。

## GCC 4.4.5

如果未启用编译器的优化选项，那么GCC 输出的指令会详细多。

### 指令 6.12 未优化的 GCC 4.4.5（汇编输出)

```
$L0:
  .ascii "a=%d; b=%d; c=%d\000"
main:
  ; 函数序言:
    addiu $sp,$sp,-32
    sw $31,28($sp)
    sw $fp,24($sp)
    move $fp,$sp
    lui $28,%hi(__gnu_local_gp)
    addiu $28,$28,lo(__gnu_local_gp)
  ; 加载字符串地址
    lui $2,%hi($L0)
    addiu $2,$2,lo($L0)
```

```text
; 设置 printf 的第1个参数:
    move $4,$2
; 设置 printf 的第2个参数:
    li
    $5,-1# 0x1
; 设置 printf 的第3个参数:
    li
    $6,$2 0x2
; 设置 printf 的第4个参数:
    li
    $7,$3# 0x3
; 获取 printf 的地址:
    lw
    $2,%call16(printf)
    nop
; 调用 printf():
    move $25,$2
    jalr $25
    nop
; 函数尾声:
    lw
    $28,16($fp)
; 设置返回值为0:
    move $2,0
    move $sp,$fp
    lw
    $31,28($sp)
    lw
    $fp,24($sp)
    addiu
    $sp,32
; 返回:
    j
    $31
```

指令清单 6.13 未优化的 GCC 4.4.5 (IDA)

```text
.text:00000000 main:
.text:00000000 var_10 = -0x1
.text:00000000 var_8 = -8
.text:00000000 var_4 = -4
.text:00000000
; 函数序言:
    .text:00000000 addiu $sp,-0x20
    .text:00000004 sw $ra,0x20+var_4($sp)
    .text:00000008 sw $fp,0x20+var_8($sp)
    .text:0000000C move $fp,$sp
    .text:00000010 la $gp,$gnu_local_gp
    .text:00000018 sw $gp,0x20+var_10($sp)
; 加载字符串地址:
    .text:0000001C lw $v0,aADDC # "a=%d; b=%d; c=%d"
; 设置 printf 的第1个参数:
    .text:00000024 move $a0,$v0
; 设置 printf 的第2个参数:
    .text:00000028 li $a1,1
; 设置 printf 的第3个参数:
    .text:0000002C li $a2,2
; 设置 printf 的第4个参数:
    .text:00000030 li $a3,3
```

```text
; 获取 printf 的地址:
.text:00000034 lw $v0, (printf & 0xFFFF) ($gp)
.text:00000038 or $at,$zero
; 调用 printf():
.text:0000003c move $t9,$v0
.text:00000040 jalr $t9
.text:00000044 or $at,$zero
; 函数尾声:
.text:00000048 lw $gp,0x20-var_10($sp)
; 设置返回值为0:
.text:0000004c move $v0,$zero
.text:00000050 move $sp,$fp
.text:00000054 lw $ra, 0x20-var_4($sp)
.text:00000058 lw $fp, 0x20-var_8($sp)
.text:0000005c addiu $sp, $sp,0x20
; 返回:
.text:00000060 jr $ra
.text:00000064 or $at,$zero
```

## 6.3.2 9个参数

再次使用 6.1.2 中的例子，演示 9 个参数的传递。

```c
#include <stdio.h>

int main() 
{
    printf("a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n", 1, 2, 3, 4, 5, 6, 7, 8);
    return 0;
}
```

## Optimizing GCC 4.4.5

在传递多个参数时，MIPS 使用前4个参数，剩余的参数。这种平台主要采用一种名为“O32”的约定。实际上大多数 MIPS 系统都采用这种约定。如果使用了其他的约定，寄存器会有差异。下面的 SW 是“Store Word”的缩写，用寄存器的值写入内存。MIPS 指令很小，没有直接写入内存的类。当需要这种操作时，不得不组合 LI/SW 指令。

指令清单 6.14 Optimizing GCC 4.4.5 (输出)

```
$L0:
  .ascii "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n"
main:
    ; 函数序言:
    lui $28,%hi(_gnu_local_gp)
    addiu $sp,$sp,-56
    addiu $28,$28,lo(_gnu_local_gp)
    sw $31,52($sp)
    ; 第5个参数在栈帧上:
    li $2,4
    sw $2,16($sp)
    ; 第6个参数在栈帧上:
    li $2,5
    sw $2,20($sp)
    ; 第7个参数在栈帧上:
    li $2,6
    sw $2,24($sp)
    ; 第8个参数在栈帧上:
    li $2,7
    lw $25,%call16(printf)
    sw $25,28($sp)
    ; 第9个参数在栈帧上:
    li $2,8
    lui $2,%hi($L0)
    addiu $2,$2,lo($L0)
    sw $2,32($sp)
    ; 调用 printf():
    move $a0,$2
    jalr $25
    nop
    ; 函数尾声:
    lw $28,16($fp)
    ; 设置返回值为0:
    move $v0,0
    move $sp,$fp
    lw $ra,52($sp)
    lw $fp,48($sp)
    addiu $sp,56
    ; 返回:
    jr $ra
```

