```
; call puts():
.text:00000014 lw $t9, (puts & 0xFFFF) ($gp)
.text:00000018 lw $a0, ($LC0 >> 16) # "Enter X:"
.text:0000001C jalr $t9
.text:00000020 la $a0, ($LC0 & 0xFFFF) # "Enter
X":; call scanf(); branch delay slot
.text:00000024 lw $gp, 0x28_var_18($sp)
.text:00000028 lui $a0, ($LC1 >> 16) # "%d"
.text:0000002C lw $t9, (__isocec09_scanf & 0xFFFF)
($gp); set 2nd argument of scanf, $al=$sp+24:
.text:00000030 addiu $a1, $sp, 0x28_var_10
.text:00000034 jalr $t9; branch delay slot
.text:00000038 la $a0, ($LC1 & 0xFFFF) # "%d"
; call printf();
.text:0000003C lw $t9, 0x28_var_18($sp)
set 2nd argument of printf;
load word at $sp+24:
.text:00000040 lw $a1, 0x28_var_10($sp)
.text:00000044 lw $t9, (printf & 0xFFFF) ($gp)
.text:00000048 lui $a0, ($LC2 >> 16) # "You entered\d&...\n"; branch delay slot
.text:00000004C jalr $t9
.text:00000050 lw $a0, ($LC2 & 0xFFFF) # "You
function epilogue;
set return value to 0:
.text:00000054 lw $ra, 0x28_var_4($sp)
.text:00000058 move $v0, zero
; return;
return:
.text:0000005C jr $ra
.text:00000060 addiu $a0, $sp, 0x28; branch delay slot
```

#  7.2 全局变量

在前文的那个程序里，如果 $x 不是局部变量而是全局变量，将会发生什么情况？一旦 $x 变成了全局变量，函数内部的指令、以及整个程序中的任何部分都可以访问它。虽然优秀的程序不应当使用全局变量，但是我们应当理解它的技术要点。

```
#include <stdio.h>

//now x is global variable
int x;

int main() {
{
    printf("Enter X:\n
n
```