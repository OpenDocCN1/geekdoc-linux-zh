
6 lea edx, [rax+1] ; EDX=EAX+1
7 ; EDX here is a "new version of rt", which will be written into rt
8 variable, if the last bit is 1
9 shr rsi, cl ; RSI=RSI>>CL
10; and esi, 1 ; ESI=ESI&1
11; the last bit is 1? If so, write "new version of rt" into EAX
12 cmov rax, edx
13 add rcx, 1 ; RCX++
14 cmp rcx, 64
15 jne .L3 ; AKAKret
16 rep ret

这段程序简洁又到位。细节在前面介绍过的几个例子中，程序都是比较比较值，但是在这里递增“rt”的值。但是这个程序的顺序有所不同，它先递增再把送到EDI寄存器。这样一来，如果最后的位是1，那么程序将使用CMOVNE[4]指令（等于CMOVNZ[5]）EDI寄存器（rt的候选值）传递EDI寄存器（当前的rt值），它是函数的返回值，从而完成rt的更新。所以，无论输入值是什么，每次递增结束后，循环控制变量的值都需要进行递增，否则它可能会被递加了64次。

由于它有一个条件转移指令（在循环的尾部）所以这种编译方法独特优势。如果要把编译的方式通过机械化，那么程序在递增rt和循环尾部进行两次条件转移。现在的CPU具有分支预测的功能（请参考本书33.1节）在性能方面，本例这类程序的效率更高。

最后一条指令是RET PET（opcode=F3）。它就是MSVC里的FATRET。这个指令是由RET衍生出来的优化指令。AMD建议：如果RET指令的前一个指令是条件转移跳转指令，那么在函数最后的返回时最好用RET 指令。（请参见AMD13b,[6]）

## Optimizing MSVC 2010

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

```
inc      eax      ; rt++
$LN3@f:
    rol      rdx, 1    ; RDX<<1
    dec      r8       ; R8-
    jne      SHORT LL40@
    fatret   0
ENDP
```

在本例中，编译器使用ROL指令替代了SHL指令。ROL的确作用是“rotate left”,SHL的含义则是“shift left”。不过在本例中，它们的效果相同。

有关旋转指令的详细介绍，请参见附录A. 6.3。

R8的值将从64逐渐递减为0，它的变化过程和变量/完全相反。

在程序的执行过程中，寄存器的关系如图所示。

| RDX | R8 |
|---|---|
| 0x0000000000000001 | 64 |
| 0x0000000000000002 | 63 |
| 0x0000000000000004 | 62 |
| 0x0000000000000008 | 61 |
| ...... | ...... |
| 0x4000000000000000 | 2 |
| 0x8000000000000000 | 1 |

程序最后使用了FATRET指令，我们在上一个例子里已经介绍过它了。

## Optimizing MSVC 2012

指令清单19.32 MSVC 2012

```
a$ = 8
f      PROC
; RCX = input value
xor     eax, eax
mov     edx, 1
lea     r8, DWORD PTR [rax+32]
; EDX = i, R8D = 32
pad     5
$LL4:
; pass 1

    test    rdx, rcx
    je      SHORT LN3@f
    eax     ; rt++
$LN3@f:
    rol     rdx, 1 ; RDX=RDX<<1

; pass 2

    test    rdx, rcx
    je      SHORT LN11@f
    eax     ; rt++
$LN11@f:
    rol     rdx, 1 ; RDX=RDX--

    dec     r8          ; R8--
    jne     SHORT $LL4@f
fatret  0
```

MSVC 2012优化编译后的生成的代码与MSVC 2010大体相同。但是MSVC 2012把迭代次数为64次的循环，拆分为两个迭代32次的循环。但坦白，笔者也不清楚中由。或许是循环长度更长一些比较好。总之，我把这个例子记录下来，希望读者注意：编译器可能产生各种事乎所料的代码，但是这些代码的功能仍然会忠于源程序。

## 19.5.3 ARM + Optimizing Xcode 4.6.3 (LLVM) + ARM mode

指令清单19.33 Optimizing Xcode 4.6.3 (LLVM) (ARM mode)

```
MOV     R1, R0
MOV     R0, #0
MOV     R2, #1
MOV     R3, R0
loc_2E
    TST    R1,LSL, R3 ; 根据R1 & (R2<<3)设置标记
    ADD     R3, R3, #1 ; R3++
    ADDNE  R0, #1 ; IF flag is cleared by TST, then R0
CMP R3, #32
BNE loc_2E
BX
```

ARM模式的TST指令相当于x86TEST指令。参见2.1节。ARM模式中没有单独位移指令（参见4.1节）。但是在处理——MOV, TST, ADD, SUB指令中，可以使用数据（如LSL, LSR, ROR）实现位运算。通过“参数调节”进行位运算的方法必须明确位移。此处的TST R1, R2, LSL理解为R1<<(2<<3)。

## 19.5.4 ARM + Optimizing Xcode 4.6.3 (LLVM) & Thumb-2 mode

Thumb-2模式与ARM模式的代码相同。只不过直接在TST指令里使用参数调节，所以使用LSL.W替代了ARM模式下的单条。

```
MOV R1, R0
MOVS R0, #0
MOVS R9, #1
MOVS R3, #0
loc_2F7A
LSL.W R2, R9, R3
TST R2, R1
IT NE
ADDNE R0, #1
CMP R3, #32
BNE loc_2F7A
BX
```

## 19.5.5 ARM64 + Optimizing GCC

本节使用的程序，是2节所示的64版。指令清单19.34 Optimizing GCC (Linaro)

```
f:
mov w2, 0
mov x5, 1
mov w1, w2
L2:
lsl x4, x5, x1 ; w4 = w5<<1
add w3, w2, 1 ; new_rt=rt+1
tst x4, x0 ; (1<<i) & a
add w2, w1, 1 ; i++
; result of TST was non-zero; then w2=new_rt; otherwise: w2=rt (idle operation)
csel w2, w3, w2, ne
cmp w1, #64 ; i <64?
bne L2 ; yes
mov w0, w2 ; return rt
ret
```

## 19.5.6 ARM64 + Non-optimizing GCC

本节再次使用5.2节所示的优化功能，以便编译器生成的代码。由于编译器关闭了优化功能，所以编译器生成的代码很大。指令19.35 Non-optimizing GCC (Linaro)

```
f:
sub sp, sp, #32
str x0, [sp,8] ; store "a" value to Register Save
str wzr, [sp,24] ; rt=0
str wzr, [sp,28] ; i=0
b .L2
.L4:
ldr x0, [sp,28]
mov x1, 1
lsl x0, x1, x0 ; X0 = X1<<X0 = 1<<i
mov x1, x0 ; X1 = 1<<i
ldr x0, [sp,8] ; X0 = a
and x0, x1&x0 ; X0 = X1&X0 = (1<<i) & a
; X0 contain zero? then jump to .L3, skipping "rt" increment
cmp x0, xzr
beq .L3
; rt++
ldr w0, [sp,24]
mov w0, w0, 1
str w0, [sp,24]
.L3:
; i++
ldr w0, [sp,28]
add w0, w0, 1
str w0, [sp,28]
.L2:
; i<=63? jump to .L4
ldr w0, [sp,28]
cmp w0, 63
ble .L4
; return rt
ldr w0, [sp,24]
add sp, sp, 32
ret
```

## 19.5.7 MIPS Non-optimizing GCC

指令清单19.36 Non-optimizing GCC 4.4.5 (IDA)

```
f:
; IDA is not aware of variable names, we gave them manually:
rt      = -0x10
i      = -0x0C
var_4  = -4
a      = 0
      addiu $sp, -0x18
      sw $fp, 0x18+var_4($sp)
      move $fp, $sp
      move $a0, 0x18+a($fp)
; initialize rt and variables to zero:
      sw $zero, 0x18+rt($fp)
      sw $zero, 0x18+i($fp)
; jump to loop check:
      or loc68
      b $zero ; branch delay, NOP
loc_20:
      li $v1, 1
      lw $v0, 0x18+i($fp)
      sll $v0, $v1, $v0 ; $v0 = 1<<i
      move $v1, $v0
      lw $v0, 0x18+a($fp)
      and $v0, $v1, $v0 ; $v0 = a&(1<<i)
; is a&(1<<i) equals to zero? jump to loc_58
      beq loc_58
; no occurred, means a&(1<<i)!=0, so increment "rt" then:
      lw $v0, 0x18+rt($fp)
      sll $v0, $v1, $v0 ; v0 = 1<<i
      move $v1, $v0
      lw $v0, 0x18+a($fp)
      and $v0, $v1, $v0 ; v0 = a&(1<<i)
      addiu $v0, $v1, 1 ; i++
      sw $v0, 0x18+rt($fp)
      sw $v0, 0x18+i($fp)
;_58:
; increment i:
      lw $v0, 0x18+i($fp)
      add $v0, $v0, 1
      sw $v0, 0x18+i($fp)
loc_68:
; load and compare it with 0x20 (32).jump to loc_20 if it is less than 0x20 (32):
      lw $v0, 0x18+i($fp)
      slt $v0, #20
      bnez loc_20 ; branch delay, NOP
; function epilogue. return rt:
      lw $v0, 0x18+rt($fp)
      move $sp, $fp
      lw $fp, 0x18+var_4($sp)
      addiu $sp, 0x18
      jr $ra ; branch delay, NOP
      nop ; branch delay, NOP
```

这段程序十分直观；程序所有的局部变量存储在栈里。在使用变量，再把它们从栈取出。LLVI指令的全称是“Shift Left Variable”。LLVI指令只能把某个操作位确定的比特（这个位置是固定值），而LLVI从寄存器读取移位的数值。启用功能之后，编译器生成的程序就会简单许多。它使用了2条位指令，非优化编译程序还需要多条位指令。这是为什么？第一LLVI指令可以替换为“跳转到第二个LLVI的无条件跳转”，但是一个函数就需要多个转移指令。而编译器的优化功能会减少这种指令的使用，更多详情参见33.1节。

```
f:
; Sa=a
; rt variable will reside in $v0:
move $v0, $zero
; i variable will reside in $v1:
move $v1, $zero
li $t0, 1
li $a3, 32
sll $a1, $t0, $v1 ; $a1 = $t0<<1 = 1<<i
loc_14:
and $a1, $a0 ; $al = a&(1<<i)
; increment i:
addiu $v1, 1=0
jump to loc_28 if (1<<i)=0 and increment rt:
beq 28
; if BEQZ not triggered, save updated rt into $v0:
addiu $a2, $v0, 1
move $v0, $a2
loc_28:
; if i=32, jump to loc_14 and also prepare next value:
bne $v1, $a3, loc_14
sll $a1, $t0, $v1
; return:
jr $ra ; branch delay, NOP
nop ; branch delay, NOP
```

## 19.6 本小节

与C/++语言中的移位符<<相应，ARM指令中有无符号数的SAR/SHL指令和操作符号的SAR/SHL指令。在ARM平台上，对无符号数移位运算的指令是LSR/LSL，对有符号数移位运算的指令是ASR/LSL。而且，ARM指令还可以通过“参数”的形式使用“后缀型”位运算指令。这类对其他数字运算的指令，又叫做“数据处理指令”。

## 19.6.1 检测特定定位（编译阶段）

对数值的二进制值（即16进制的0x40）进行检测的二进制指令的大体如下：

指令清单19.38 C/C++

```
if (input&0x40)
  ...
```

指令清单19.39 x86
```
TEST REG, 40h
JNZ is_set ; bit is not set
```

指令清单19.40 x86
```
TEST REG, 40h
JZ is_cleared ; bit is not set
```

指令清单19.41 ARM (ARM mode)
```
TST REG, #0x40
BNE is_set ; bit is not set
```

## 19.6.2 检测定位 (runtime阶段)

在C/++代码编译得的程序中，检测定位的指令（右移n位，然后舍弃最低位）大如下。

```
if ((value>>n)&1)
...
```

# 指令清单19.42 C/C++

相应的x86代码如下所示。

# 指令清单19.43 x86
```
REG=input_value
; CL=n
SHR REG, CL
AND REG, 1
```

此外还可以左移n次，逐渐鉴定各位是否为零。

# 指令清单19.44 C/C++

```
if (value & (1<<n))
...
```

上述源程序对应的x86指令如下。

# 指令清单19.45 x86
