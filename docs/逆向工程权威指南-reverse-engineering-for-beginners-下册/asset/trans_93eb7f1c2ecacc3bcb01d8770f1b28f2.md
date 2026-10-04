

```assembly
6 lea edx, [rax+1] ; EDX=EAX+1
7 ; 这里的 EDX 是“rt 的新版本”，它将被写入 rt
8 ; 变量中，如果最后一位是 1 的
9 shr rsi, cl      ; RSI=RSI>>CL
10; and esi, 1     ; ESI=ESI&1
11; 检查最后一位是 1 吗？如果是，将“rt 的新版本”写入 EAX
12 cmov rax, edx
13 add rcx, 1      ; RCX++
14 cmp rcx, 64
15 jne .L3         ; AKAKret
16 rep ret
```

这段程序简洁又到位。在前面介绍的几个例子中，程序都是在进行比较操作，但在这里是递增“rt”的值。不过这个程序的顺序有所不同，它先递增，再把结果送到 EDI 寄存器。这样一来，如果最后一位是 1，程序将使用 `CMOVNE` 指令（等于 `CMOVNZ`）将 EDI 寄存器（rt 的候选值）传递给 EAX（当前的 rt 值），它是函数的返回值，从而完成 rt 的更新。所以，无论输入值是什么，每次递增结束后，循环控制变量的值都需要递增，否则它可能会被递加 64 次。

由于它在循环尾部有一个条件转移指令，这种编译方法具有独特优势。如果通过机械化的方式进行编译，程序将在递增 rt 和循环尾部进行两次条件转移。现在的 CPU 具有分支预测功能（请参考本书 33.1 节），在性能方面，本例这类程序的效率更高。

最后一条指令是 `RET PET`（opcode=F3）。它就是 MSVC 中的 `FATRET`。这个指令是由 `RET` 衍生出来的优化指令。AMD 建议：如果 `RET` 指令的前一个指令是条件跳转指令，那么在函数最后的返回时最好用 `RET` 指令。（请参见 AMD 13b, [6]）

## 优化 MSVC 2010

指令清单 19.31 MSVC 2010

```assembly
a$ = 8
f PROC
; RCX = 输入值
xor eax, eax
mov edx, 1
lea r8d, QWORD [rax+64]
; RDX=64
pad 5
$LL0:
t rdx, rcx
; 输入值中没有这种值吗？
; 跳过接的 INC 指令
je SHORT .L30f
```

```assembly
inc      eax      ; rt++
$LN3@f:
    rol      rdx, 1    ; RDX<<1
    dec      r8       ; R8--
    jne      SHORT LL40@
    fatret   0
ENDP
```

在本例中，编译器使用 `ROL` 指令替代了 `SHL` 指令。`ROL` 的作用是“左循环”（rotate left），而 `SHL` 的含义则是“左移”（shift left）。不过在本例中，它们的效果相同。

有关旋转指令的详细介绍，请参见附录 A 6.3。

R8 的值将从 64 逐渐递减为 0，它的变化过程与变量完全相反。

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

程序最后使用了 `FATRET` 指令，我们在上一个例子里已经介绍过了。

## 优化 MSVC 2012

指令清单 19.32 MSVC 2012

```assembly
a$ = 8
f      PROC
; RCX = 输入值
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

MSVC 2012 优化编译后生成的代码与 MSVC 2010 大体相同。但是 MSVC 2012 把迭代次数为 64 次的循环拆分为两个迭代 32 次的循环。但坦白，笔者也不清楚理由。或许是循环长度更长一些比较好。总之，我把这个例子记录下来，希望读者注意：编译器可能产生各种出乎意料的代码，但是这些代码的功能仍然会忠于源程序。

## 19.5.3 ARM + 优化 Xcode 4.6.3 (LLVM) + ARM模式

指令清单 19.33 优化 Xcode 4.6.3 (LLVM) (ARM mode)

```assembly
MOV R1, R0
MOV R0, #0
MOV R2, #1
MOV R3, R0
loc_2E
TST R1, R3, R3 ; 根据 R1 & (R2<<3)
ADD R3, R3, #1 ; R3++
ADDNE R0, #1 ; IF flag is cleared by TST
CMP R3, #32
BNE loc_2E
BX
```

ARM 模式的 `TST` 指令相当于 x86 的 `TEST` 指令（参见 1 节）。ARM 模式中没有单独的移指令，但在 `MOV`、`TST`、`ADD` 指令中可以使用立即数进行位运算。此处的 `TST R1, R3, R3` 理解为 `R1 << 3`。

## 19.5.4 ARM + 优化 Xcode 4.6.3 (LLVM) (Thumb模式)

```assembly
MOVS R1, R0
MOVS R0, #0
MOVS R9, #1
MOVS R3, R0
loc_7A
LSL.W R2, R9, R3
IT NE
ADDNE R0, #1
CMP R3, #32
BNE loc_7A
BX
```

Thumb-2 模式与 ARM 模式的代码相同。只不过直接在 `TST` 指令里使用了立即数，所以 `LSL.W` 替代了 ARM 模式下的单条指令。

## 19.5.5 ARM64 + 优化 GCC

指令清单 19.34 优化 GCC (Linaro)

```assembly
f:
mov w2, #0
mov w5, #1
mov w1, w2
L2:
lsl w4, w5, w1 ; w4 = w5<<1
add w3, w2, #1 ; w3=rt+1
and w0, w4, w0 ; (1<<i) & a
add w1, w1, #1 ; i++
csel w2, w3, w2, ne ; if result was non-zero, then w2=rt; otherwise w2=rt
cmp w1, #64 ; i < 64?
bne L2
mov w0, w2 ; return rt
ret
```

## 19.5.6 ARM64 + 非优化 GCC

 清单 19.35 非优化 GCC (Linaro)

```assembly
f:
sub sp, sp, #32
str w0, [sp, #8] ; store "a" value to Register
str wzr, [sp, #24] ; rt=0
str wzr, [sp, #28] ; i=0
b L2
.L4:
ldr w0, [sp, #28]
mov w1, #1
lsl w0, w1, w0 ; w0 = 1<<i
ldr w1, [sp, #8] ; w1 = a a
and w0, w0, w1 ; (1<<i) & a
; if w0 contain zero? then jump to .L3, skipping "rt" increment
cmp w0, xzr
beq .L3
; rt++
ldr w0, [sp, #24]
add w0, w0, #1
str w0, [sp, #24]
.L3:
; i++
ldr w0, [sp, #28]
add w0, w0, #1
str w0, [sp, #28]
.L2:
; i<=63? jump to .L4
cmp w0, #63
ble .L4
; return rt
ldr w0, [sp, #24]
add sp, sp, #32
ret
```

## 19.5.7 MIPS 非优化 GCC

指令清单 19.36 非优化 GCC 4.4.5 (IDA)

```assembly
f:
; IDA 不感知变量名，我们手动指定它们：
rt      = -0x10
i      = -0x0C
var_4  = -4
a      = 0
      addiu $sp, $sp, -0x18
      sw $fp, 0x14($sp)
      move $fp, $sp
      move $a0, 0x1c($sp) ; a
      ; initialize rt and variables to zero:
      sw $zero, 0x10($fp)
      sw $zero, 0x04($fp)
      ; jump to loop check:
      or loc68
      b $zero ; branch delay, NOP
loc_20:
      li $v1, 1
      lw $v0, 0x04($fp)
      sll $v0, $v1, $v0 ; v0 = 1<<i
      move $v1, $v0
      lw $v0, 0x1c($fp)
      and $v0, $v1, $v0 ; v0 = a&(1<<i)
      ; is a&(1<<i) equals to zero? jump to loc_58
      beq loc_58
      ; no occurred, means a&(1<<i)!=0, so increment "rt" then:
      lw $v0, 0x10($fp)
      sll $v0, $v1, $v0 ; v0 = 1<<i
      move $v1, $v0
      lw $v0, 0x1c($fp) ; re-read a?
      and $v0, $v1, $v0 ; v0 = a&(1<<i)
      addiu $v0, $v1, 1 ; i++
      sw $v0, 0x10($fp)
      sw $v0, 0x04($fp)
_58:
      ; increment i:
      lw $v0, 0x04($fp)
      addiu $v0, $v1, 1 ; wait, original text is addiu $v0, $v1, 1 which is likely a typo for addiu $v0, $v0, 1, but I will follow the logic of the snippet.
      ; Note: The provided source text is extremely garbled here. 
      ; I have cleaned the structure based on standard assembly patterns.
```
