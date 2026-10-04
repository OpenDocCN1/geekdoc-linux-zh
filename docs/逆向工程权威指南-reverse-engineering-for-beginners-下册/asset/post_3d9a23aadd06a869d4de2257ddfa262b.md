
```
; R4=s
BL      strlen      ; strlen() takes "s" value from R0
; R0=str_len
MOV     r3,#0
; R3 will always hold 0
|L0.16|
CMP     r0,#0      ; str_len==0?
ADDNE   r2,r4,r0    ; (if str_len!=0)
R2=R4+R0=s+str_len
LDRNE  r1,[r2,-1]   ; (if str_len!=0) R1=load byte at address R2-1=s+str_len-1
CMP     ; (if str_len==0) compare loaded byte against 0 |L0.56|
BEQ     ; jump to exit if str_len==0 or loaded byte is 0
CMP     r1,#0xa      ; loaded byte '\n'
CMP     r1,#0xa      ; (loaded byte is not '\r')
SUBQ    r0,r0,#1    ; (if loaded byte is '\r' or '\n')
STRBEQ r3,[r2,-1] ; (if loaded byte is '\r' or '\n') store R3 (zero) at address R2-1=s+str_len-1
BEQ     |L0.16|      ; jump to loop begin if loaded byte was '\r' or '\n'
|L0.56|
; return "s"
MOV     r0,r4
POP     {r4,pc}
ENDP
```

## 47.7 ARM:Keil 6/2013 (Thumb模式) 优化

在Thumb模式执行指令的条件执行指令ARM模式指令的少，这种代码更接近x86的指令。但是在程序的22和27行的偏移量0x20和0x1f，会让许多人感到困惑。为什么Keil 编译器会分配这些指令？老实说，很难讲。也许这就是Keil6优化过程的异之处。不管这种代码多么令人费解，整个程序的功能确实忠实于我们的源代码。

指令47.7 Keil 6/2013 (Thumb模式) 优化

```
str_trim PROC
PUSH    {r4,lr}
MOVS    r4,r0
4      ; R4=s
5      BL      strlen      ; strlen() takes "s" value from R0
6      ; R0=str_len
7      MOVS    r3,#0
8      ; R3 will always hold 0
9      B               |L0.24|
10     |L0.12|  
11     CMP     r1,0xd      ; is loaded byte '\r'?
12     BEQ       |L0.20|      ; is loaded byte '\n'?
13     CMP     r1,#0xa
14     BNE       |L0.38|      ; jump to exit, if no
15     |L0.20|  
16     SUBS    r0,r0,#1      ; R0-- or str_len-
17     STRB    r2,[0x1f]    ; store 0 at address R2+0x1F=s+str_len-0x20+0x1F=s+str_len-1
18     |L0.24|  
19     CMP     r0,#0       ; str_len=?
20     BEQ       |L0.38|      ; yes? jump to exit
21     ADDS    r2,r4,r0      ; R2=R4+R0=s+str_len
22     SUBS    r2,r2,#0x20   ; R2=R2-0x20=s+str_len-0x20
23     LDRB    r1,[0x1f]    ; load byte by address+0x1F=s+str_len-0x20+0x1F=s+str_len-1 to R1
24     CMP     r1,#0       ; is loaded byte 0?
25     BNE       |L0.12|      ; jump to loop begin, if its not '0'
26     |L0.38|      ; return "s"
27     MOVS    r0,r4
28     POP     {r4,pc}
29     ENDP
```

## 47.8 MIPS 指令清单 47.8(IDA) GCC 4.4.5优化

```
str_trim;
; IDA is not aware of local variable names, we gave them manually:
saved_GP      = -0x10
saved_S0      = -8
saved_RA      = -4

lui     $gp, (__gnu_local_gp >> 16)
addiu   $sp, -0x20
la $gp, (__gnu_local_gp & 0xFFFFFF)
sw $ra, 0x20+saved_RA($sp)
sw $s0, 0x20+saved_S0($sp)
sw $gp, 0x20+saved_GP($sp)
; call strlen(). input address is still $a0, will take it from them:
lw $t9, 0xFFFFFF($gp)
or $a0, $zero; load slot
jal $t9; input address is still in $a0, it is to $s0:
move $s0, $a0; result of strlen() (i.e., length of string) is in $v0 now
beq $v0, exit; (i.e., if length of string is 0):
addi $a1, $zero; branch slot
addi $al, $s0,al; $al=s+str_len-1
li $a2, 0xD; skip loop body
li $a3, 0xA; branch slot
loc_5C: load next byte from memory to $a0:
lb $a0, 0($v1)
move $a1, $v1; $al=s+str_len-2
beq $a0, exit; jump to exit if loaded byte is zero:
addi $v1, -1; decrement str_len:
; at this moment, $a0=loaded_byte, $a2=0xD (CR symbol) and $a3=0xA (LF symbol)
beq $a0, $a2, loc_7C
addi $v1, -1 ; branch slot
loc_6C: ; loaded byte is LF? jump to exit if not LF
bne $a0, $a3, exit
nor $a0, $zero ; branch slot
loc_7C: ; loaded byte is CR at this moment jump to loc_5C (loop body) if str_len (in $v0) is not zero:
bnez $v0, loc_5C
simultaneously, store $zero at that place in memory:
sb $zero, 0($al) ; branch slot
; "exit" label was named by me:
lw $ra, 0x20+saved_RA($sp)
move $v0, $s0
lw $s0, 0x20+saved_S0($sp)
jr $ra
addiu $sp, 0x20
```

S头的寄存器就是保存寄存器（saved temporaries）。在调用过程中，保存寄存器的值需要保留（被调用函数保存和恢复），因此$S的值的值保存在帧里，在完成任务后恢复其初始状态。

Linaro是一家开源的基于ARM平台的组织，由多家业内联合成立。其开发了ARM开发工具、Linux内核以及发行版（包括Android及Ubuntu）的主要构建系统。

## 第48章 toupper() 函数

本章讨论的是将小写字符转换成大写字母的toupper() 函数。这是一个比较常见的函数。

```c
char toupper(char c)
{
    if(c>='a' && c<='z')
        return c-'a'+'A';
    else
        return c;
}
```

这里的程序代码中，我们可以看到'a'+'A' 这种表达式是为了增强的可读性。在程序的实际编译过程中，它会被优化为相应的指令。

我们知道，小写的英文字字母a的ASCII码十六进制是61，就是十进制的97；而大写的A的ASCII码的十六进制则是41，相当于十进制的65。很明显，在ASCII码表中，两者的差值是32（0x20）。

实际上，我们从图48所示的这个标准ASCII表格就能更清楚了。

# Characters in the coded character set ascii.

| | 0 1 2 3 4 5 6 7 8 9 A B C D E F |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0x | @ | a | b | c | d | e | f | g | h | TAB | j | k | I | RET | n | o |
| 1x | p | q | r | s | t | u | v | w | x | y | ESC | ] | ^ | | |
| 2x | | " | # | $ | & | ' | ( | ) | * | + | , | / | | | |
| 3x | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | < | = | ? | | |
| 4x | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | |
| 5x | P | Q | R | S | T | U | V | X | Y | Z | | | | | |
| 6x | a | b | c | d | e | f | g | h | i | j | k | l | m | n | o |
| 7x | p | q | r | s | t | u | v | w | x | y | z | DEL | | |

## 48.1 两个比较

非优化的MSVC非常直接：为了转换大写字母的目的，程序首先检查输入的十进制数值是否在97~122范围内，就是小写字母~z的范围内。如果输入满足条件，就会将它的数值减去32，而得到相应的大写字母了。非优化时，编译器会对代码进行处理。

x64的MSVC 非优化程序

```assembly
2 toupper PROC
3  mov PTR [rsp+8], cl
4  movsx eax, PTR [rsp]
5  cmp eax, 97
6  jl SHORT LN2
7  movsx eax, PTR [rsp]
8  cmp eax, 122
9  jpg SHORT LN2
10 movsx eax, PTR [rsp]
11 sub eax, 32
12 jmp SHORT LN3
13 jmp SHORT LN1 ; compiler artifact
14 movzx eax, PTR [rsp] ; unnecessary casting
15 movzx eax, PTR [rsp] ; compiler artifact
16 LN2:
17 LN3:
18 ret
ret: 0
19 toupper ENDP
```

注意的是：程序第8行的字节的符号扩展到64位。输入值显然占据了8位的位，而高位（从8位到63位）保持不变。我们可以在调试器中看到这个位是随机的数据（也就是随机数）。由于所有指令都将其字节为操作，这种准备方案引发问题。非优化的GCC生成的代码几乎相似。x64的GCC 4.9非优化代码

```assembly
push rbp
mov rsp, edi
mov eax, rsp
mov PTR [rbp-4], al
cmp PTR [rbp-4], 96
jle L2
cmp PTR [rbp-4], 122
jjg L2
movzx eax, PTR [rbp-4]
sub eax, 32
jmp .L3
.L2:
movzx eax, PTR [rbp-4]
.L3:
pop rbp
ret
```

## 48.1.2 一个比较操作

优化的MSVC表现得更好，它只分配一个比较操作。x64的MSVC 优化程序

```assembly
toupper PROC
lea eax, DWORD PTR [rcx-97]
cmp ai, 25
ja SHORT LN2
movsx eax, cl
sub eax, 32
ret 0
LN2:
movzx eax, cl
ret 0
toupper ENDP
```

前面已经解释了，如何用一个比较操作替换两个（参见本书42.2节）。如果使用C/C++重写，对应的代码如下：

```c
int tmp=c-97;
if (tmp>25)
    return c;
else
    return c-32;
```

这里的变量tmp应该是一个有符号数。这里的转换处理了两个减法指令以及一个比较指令。原来的算法是通过两个比较指令加一个减法指令来实现的。优化的GCC编译器更好，它不用跳转指令JUMP，转而采用CMOVcc指令（参见33.1 节）。x64下的GCC 4.9优化程序

```assembly
toupper:
    lea edx, [edi-97] ; 0x61
    lea eax, [edi-32] ; 0x20
    cmp dl, 25
    cmov eax, edx
    ret
```

第三行的代码首先准备了要减的值0x20（十六进制的20，十进制的32），这会给出一个相似的结果，好像执行减法会发生似的。而第五行的指令，在不在进行转换（也就是不执行减法）的时候，原始的输入数据复制给EAX寄存器。可见它在条件不成立的情况下舍弃的值。也就是说，编译器为了避免使用条件转移指令而预进行了减法运算。

## 48.2 ARM

ARM模式的Keil优化也只有一个比较指令。

# 指令清单48.5 ARM模式下的Keil 6/2013优化程序

```assembly
toupper PROC
SUB r0,r0,#0x61
CMP r1,#0x19
SUBLS r0,r0,#0x20
ANDLS r0,r0,#xff
BX lr
ENDP
```

从这里的程序我们可以看到，R1的值小于或等于019（十进制的19），那么就会执行SUBLS和ANDLS指令。这两条指令实际执行的是转换大写的操作。而Thumb模式下的Keil优化可以通过比较指令进行大写转换。

# 指令清单48.6 Thumb模式下的Keil 6/2013优化指令

```
toupper PROC
MOVS r1,r0
SUBS r1,#0x61
CMP r1,#0x19
BHI |L0.14
SUBS r0,r0,#0x20
LLS r0,r0,#24
LRS r0,r0,#24
|L0.14
BX lr
ENDP
```

最后的两条指令组合（LLS和LRS）的整体作用就是“AND reg.0FF”。用C/C++表示写法的话，就可以表示为“(i<<24)>>24”，也就是先左24位。显然，Thumbe模式下的Keil认为，它们这里的2个双字节的指令比“AND reg, 0FF”的运行效率更高（它首先要00FF载入寄存器，然后做AND（与操作）”。

+   48.2.1 ARM64的GCC

# 指令清单48.7 ARM64的非优化GCC 4

```assembly
toupper:
sub sp, sp,#16
strb w0,[sp,15]
ldrb w0,96
bls .L2
ldrb w0,[sp,15]
cmp w0,122
bhi .L2
```
