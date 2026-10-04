b$ = 16

```
PROC
divsd   xmm0, QWORD PTR __real@40091eb851eb851f
mulsd   xmm1, QWORD PTR __real@40106666666666
addsd   xmm0, xmm0
ret
ENDP
```

程序使用XMM0~XMM3传递参数中的前几个浮点数，其余参数都通过栈传递。有关浮点数的参数传递规范，请查阅MSDN：nhttps://msdn.microsoft.com/en-us/library/zthk2dkh.aspx

变量a存储在XMM0寄存器中，变量b存储在XMM1寄存器中。XMM系列寄存器是128位寄存器，双精度double浮点数是64位。这个程序使用了寄存器的低半部分。

DIVSD指令的全称是“Divide Scalar Double-Precision Floating-Point Values”，即标双精度浮点数。DIVSD指令将第一个操作数的低64位的双精度浮点数被除，以第二个操作数的低64位的双精度浮点数进行除法运算，将结果保存到目标地址（第一个操作数）的低64位，目标地址的低64位不变。

在程序中可以看到，编译器使用了IEEE 754格式封装浮点数数量。
MULSD和ADDSD分别是乘法和加法的运算指令。

函数返回的数据类型是double，通过XMM0寄存器返回。

由MSVC编译器进行非优化编译，可以获得如下的代码：

指令清单27.2 MSVC 2012 x64

```
__real@4010666666666666 DQ 0401066666666666r ; 4.1
__real@40091eb851eb851f DQ 04091eb851eb851fr ; 3.14
```

a$ = 8
b$ = 16

```
PROC
movsd   QWORD PTR [rsp+16], xmm1
movsd   QWORD PTR [rsp+8], xmm0
movsd   xmm0, QWORD PTR a[$rsp]
divsd   xmm0, QWORD PTR __real@40091eb851eb851f
movsd   xmm1, QWORD PTR b[$rsp]
mulsd   xmm1, QWORD PTR __real@40106666666666
```