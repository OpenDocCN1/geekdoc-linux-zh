; store ST(0) to ST(0) idle operation, pop value at top of stack,
; leave _b at top
fstp st
jmp short loc_804844A

loc_8048448:
; store _a to ST(1), pop value at top of stack, leave _a at top
fstp st(1)

loc_804844A:
pop ebp
retn
end

优化编译的效果体现在SAHF指令之之后的JA指令上。实际上，依据无符号类型数据的比较结果进行跳转的条件转移指令(JA/JAE, JB/JBE, JE/JZ, JNA/JNA, JNB/JBE, JNE/JNZ)，只检测CF和ZF标志位。

在执行FSTSW/FNSTW指令下，C3/C0标志位的传递给AH寄存器。
AH与Cx的关系是:

| | 6 | 2 | 1 | 0 |
|---|---|---|---|---||
| | C3 | | C2 | C1 | C0 |
| | ZF | | AF | PF | CF |

在执行标志位传递指令SAHF(Store AH into Flags)后，AH寄存器的标志位与CPU的8位对应关系就变成了:

对照两个比较数值的一系列操作后C3和C0标志位的值被发送到ZF和CF标志位，以供后续的条件跳转指令调用。如果CF和ZF都为0，则跳转将会触发。

很显然，FPU的C3/C2/C0状态位上占用寄存器的相应数值，为了把FPU的标志位复制到CPU标志位上，以便进行判断。这多半是有意的为之。

# GCC 4.8.1 - 启用优化选项-03

Intel P6系列[[]]的FPU指令组增加了一组指令。这些指令是
FUOMI(比较操作数并设置主的标志位)和FCMOVcc(相当于处理FPU寄存器