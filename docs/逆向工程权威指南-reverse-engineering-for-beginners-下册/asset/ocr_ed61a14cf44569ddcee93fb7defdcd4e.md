6 lea edx, [rax+1] ; EDX=EAX+1
7 ; EDX here is a "new version of rt", which will be written into rt
8 variable, if the last bit is 1
9 shr rsi, cl ; RSI=RSI>>CL
10; and esi, 1 ; ESI=ESI&1
11; the last bit is 1? If so, write "new version of rt" into EAX
12 cmov rax, edx
13 add rcx, 1 ; RCX++
14 cmp rcx, 64
15 jne .L3 ; AKAK fatret
16 rep ret

这段程序简洁又到位。细节在前面介绍过的几个例子中，程序都是比较比较值，然后但是在这里递增“rt”的值。但是这个程序的顺序有所不同，它先递增再把送到EDI寄存器。这样一来，如果最后的位是1，那么程序将使用CMOVNE[4]指令（等于CMOVNZ[5]）EDI寄存器（rt的候选值）传递EDI寄存器（当前的rt值），它是函数的返回值，从而完成rt的更新。所以，无论输入值是什么，每次递增结束后，循环控制变量的值都需要进行递增，否则它可能会被递加了64次。

由于它有一个条件转移指令（在循环的尾部）所以这种编译方法独特优势。如果要把编译的方式通过机械化，那么程序在递增rt和循环尾部进行两次条件转移。现在的CPU具有分支预测的功能（请参考本书33.1节）在性能方面，本例这类程序的效率更高。

最后一条指令是RET PET（opcode=F3）。它就是MSVC里的FATRET。这个指令是由RET衍生出来的优化指令。AMD建议：如果RET指令的前一个指令是条件转移跳转指令，那么在函数最后的返回时最好用RET 指令。（请参见AMD13b,[6]）

Optimizing MSVC 2010

指令循环19.31 MSVC 2010

```
a$ = 8
f PROC
; RCX = input value
xor eax, eax
mov edx, 1
lea r8d, QWORD [rax+64]
; RDX=64
pad 5
$LL0:
t rdx, rcx
; there are no such in input value?
; skip the next INC instruction
je SHORT .L30f
```