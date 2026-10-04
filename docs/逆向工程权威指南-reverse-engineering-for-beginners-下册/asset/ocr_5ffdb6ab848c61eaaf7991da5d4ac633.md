# 27.4 机器精度

本书在22.2节将介绍机器器精度的具体算法。在这一节里，我们把它编译为如下所示的64位应用程序。

指令清单27.11 Optimizing MSVC 2012 x64

```
v = 8
calculate_machine_epsilon PROC
movdx QWORD PTR v$[rsp], xmm0
movaps xmm1, xmm0
inc QWORD PTR v$[rsp]
movsd xmm0, QWORD PTR v$[rsp]
subsd xmm0, 0
ret
calculate_machine_epsilon ENDP
```

由于INC指令无法对128位的XMM寄存器进行操作，程序首先要把寄存器的值传送到到内存中的某个地址。

然而这并不是必须的。如果在此直接使用ADDSD (Add Scalar Double-Precision Floating-Point Values)令，就能能够对XMM寄存器的低64位进行加法运算，同时保持寄存器的高64位为值。或许，我们不得不说MSVC 2012还有改进的余地。

我们再看看这个程序，在完成减法运算之后，程序把返回值再次传回了XMM寄存器，然后对XMM寄存器进行减法（比较）操作。SUBSD的全部是“Subtract XMM Scalar Double-Precision Floating-Point Values”。它对128位寄存器的低64位进行操作。最后，减法的返回值保存在XMM寄存器中。

# 27.5 仿函数生成程序（续）

现在，我们再次使用MSVC 2012编译指令清单22.1的程序。这个版本的MSVC编译器能够直接分配FP/SIMD指令。

指令清单27.12 Optimizing MSVC 2012

```
_real@3f800000d 03 3f800000r      ; 1

tv128 = -4
tmp$ = -4
?float_@YAMXZ PROC
    push
    ecx
    call ?my_rand@YAIXZ
; EAX=pseudorandom value
```