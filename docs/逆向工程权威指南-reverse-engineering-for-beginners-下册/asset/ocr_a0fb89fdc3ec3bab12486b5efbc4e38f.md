在没有优化功能时，编译器只使用了R-字母寄存器对，没有使用D-字母寄存器。

# 17.6.4 ARM64 + Optimizing GCC (Linaro) 4.9

指令清单17.8 Optimizing GCC (Linaro)

f:

```
stp     x29, x30, [sp, -16]!
add     x29, sp, 0
ldr     d1, .LC1; load 54 into D1
ldr     d0, .LC0; load 32.01 into D0
bl      pow
; result of pow() in do
adrp    x0, .LC2
add     x0, x0, :lo12:.LC2
bl      printf
mov     w0, 0
ldp     x29, x30, [sp], 16
ret
```

.LC0:
; 32.01 in IEEE 754 format
.word  -1374389535
.word  10779936455

.LC1:
; 1.54 in IEEE 754 format
.word  171798692
.word  1073259479

.LC2:
"string.32.01 ^ 1.54 = %f\n"

启用功能化之后，编译器使用D0和D1寄存器加载常量，而继续传递给
pow()函数。pow()函数的运算结果再由D0寄存器传递给printf()函数。由于
printf()函数可以通过X-字母寄存器获取整数数据和指针，而且还可以
直接访问D-字母寄存器获取浮点数参数，所以在传递浮点数时不需要修改或
转移数据。

# 17.6.5 MIPS

指令清单17.9 Optimizing GCC 4.4.5 (IDA)

main:

```
var_10     = -0x1
var_4      = -4
```

```
; function prologue:
lui     $sp, (dword_9C >> 16)
addiu $sp, -0x20
```