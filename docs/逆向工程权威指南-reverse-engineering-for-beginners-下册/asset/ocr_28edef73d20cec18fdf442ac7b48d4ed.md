# ADDS r1,r1,#1

```
; correct whole line by subtracting '0' character from it':
SUBS r0,r0,#0x30
ADDS r0,r2,r0
; rt=R2+R0=input character + (rt*10 - '0')
|L0.16;
; load input character to R2
LDR r2,[r1,#0]
; is it zero?
CMP r2,#0
; jump loop body if it is not
BNE |L0.6
; rt variable in R0 now, ready to be used in caller function
BX lr
ENDP
```

很有趣的是，我们以前上学学习到的规则是：加法和减法的运算顺序无所谓先后后，完全可以重排。本例就利用了这一原则：编译器首次计算加/减法的混合运算表达式为‘rt*10- '0’、来得中间差，然后计算输入字符串与中间差的。虽然这种算法的计算结果一定和源代码的计算相同相同但请不要忽视编译器的指令式重排功能。

# 42.5 ARM64下的GCC 4.9.1指令优化

ARM64的编译器可以使用预减量指指令后缀。

> 指令优化42.5 ARM64的GCC 4.9.1指令优化

```
my_atoi:
; load input character into W1
ldr w1,[x0]
mov x2,x0
; X2=address of input string
; is loaded character zero?
; jump to exit if its so
; W1 will contain 0 in this case.
; it will be reloaded into W0 at L4.
cbz w1,w1,L4
; W0 will contain "rt" variable
; initialize it at zero:
mov w0,w0,0
L3:
; subtract 48 or '0' from input variable and put result into
W3:
sub w3,w1,#48
```