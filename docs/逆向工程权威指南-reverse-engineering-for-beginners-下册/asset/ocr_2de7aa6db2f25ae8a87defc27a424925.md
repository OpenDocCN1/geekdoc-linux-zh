```
main:
  sub rsp, 8
  movd xmm1, QWORD PTR .LC0[rip]
  movd xmm0, QWORD PTR .LC1[rip]
  call pow
  result is now in XMM0
  edi, OFFSET FLAT::.LC2
  mov eax, 1; number of vector registers passed
  call printf
  xor eax, eax
  add rsp, 8
  ret
```

```
.LC0:
  .long 171798692
  .long 1073259474
.LC1:
  .long 2920577761
  .long 1077936455
```

GCC的编译器更容易懂。它使用XMM0寄存器作为printf()函数传递浮点类型参数。此外，在printf()函数传递参数的时候，程序将EAX寄存器的值设置为1。这就相当于告诉函数“有一个参数在矢量寄存器里”。这种特例完全遵循了有关规范（请查阅Mit13）。

# 27.3 浮点数之间的比较

# 27.3.1 x64

指令清单27.7 Optimizing MSVC 2012 x64

```
a$ = 8
b$ = 16
d_max PROC
  comisd xmm0, xmm1
```