一种旨在简化原子操作if语句而设计的语法糖[1]。

上面的汇编代码将输入参数a代入了临时的局部变量tv64，其余部分的指令都很好理解。[2]

若用GCC 4.4.1编译器编译这个程序，无论是否启用用其最大程度优化的选项“~03”，生成的汇编代码和MSVC编译出来的代码没有什么区别。

# Optimizing MSVC

经命令行“c1.c /Fm1.asm /Ox”编译上述程序，可得到如下指令：

```
a$    = 8; size = 4
_f PROC.
mov     eax, DWORD PTR _a$[esp-4]
sub     eax, 0
je      SHORT LN4@f
sub     eax, 1
je      SHORT LN3@f
sub     eax, 1
je      SHORT LN2@f
mov     DWORD PTR _a$[esp-4], OFFSET $SG791 ; 'something unknown',
0AH, 00H
jmp     _printf
LN2@f:
mov     DWORD PTR _a$[esp-4], OFFSET $SG789 ; 'two', 0AH, 00H
jmp     _printf
LN3@f:
mov     DWORD PTR _a$[esp-4], OFFSET $SG787 ; 'one', 0AH, 00H
jmp     _printf
LN4@f:
mov     DWORD PTR _a$[esp-4], OFFSET $SG785 ; 'zero', 0AH, 00H
jmp     _printf
_f     ENDP
```

指令清单13.2 MSVC

我们看到，有两处不同：
第一处：把变量存储到EAX寄存器之后，用EAX的值减去零。似乎这样做并没有味道，但是这两条指令可以检查EAX寄存器的值是否为。如果EAX寄存器的值是零，ZF标志位设置为1（就是0=0-1），就可以提前设置ZF标志位），并触发第一条条件跳转指令，使程序跳转到LN4@f，并在屏幕上打印。如果EAX寄存器的值不是零，则会触发第一条跳转指令、做“EAX=EAX-1”的运算，若计算结果为零则做输出；此时EAX寄存器的值仍然不是零，就会再做一次减法操作和条件判断。