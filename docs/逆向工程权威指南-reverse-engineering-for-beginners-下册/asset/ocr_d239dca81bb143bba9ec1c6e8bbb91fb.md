```
mov ecx, edx
sub ecx, eax
mov eax, ecx
pop ebp
retn
endp
```

#  41.2 ARM

ARM处理器和其他的RISC处理器一样，“纯洁”不支持硬件级别的除法指令。此外，这种CPU还真难“直接”进行32位常量的乘法运算(32位opcode容纳不下32常量)。因此，在进行除法运算时，编译器会混合加减法和位移运算、变相实现除法运算(详请参阅第19章)。

本节引用参考书Ltd94(第3.3节)的一个例子，介绍“32位除以10”的例子，分别计算商和余数。

```
; takes argument in al
; returns quotient in al, remainder in a2
; cycles could be saved if only divide or remainder is required
SUB a2, a1, #10 ; keep (x-10) for later
SUB al1, al1, al1, lsr #2
ADD al1, al1, al1, lsr #4
ADD al1, al1, al1, lsr #8
ADD al1, al1, al1, lsr #16
MOV al1, al1, lsr #3
ADD a3, a1, asl #2 ; calc (x-10)*10
SUBS a2, a2, a3, asl #1 ; fix-up quotient
ADDPL al1, #1
ADDMI a2, a2, #10 ; fix-up remainder
MOV pc, lr
```

#  41.2.1 ARM模式，采用Xcode 4.6.3(LLVM) 优化

```
__text:00002C58 39 1E 08 E3 18 E3 MOV    R1, 0x38E3E39
__text:00002C60 10 F1 50 E7         SMMUL R0, R0, R1
__text:00002C64 C0 10 A0 E1         MOV    R1, R0,ASR#1
__text:00002C68 A0 0F 81 E0         ADD    R0, R1, 
R0,LSR#31
__text:00002C6C 1E FF 2F E1         BX LR
```