```
lsl x4, x5, x1      ; w4 = w5<<wl = 1<<i
add w3, w2, 1       ; new_rt=rt+1
tst x4, x0           ; (1<<i) & a
add w2, w1, 1       ; i++
; result of TST was non-zero;
; then w2=w3 or rt=new_rt;
; otherwise: w2=w0 or rt=rt (idle operation)
csel w2, w3, w2, ne
cmp w1, 64          ; i; < 64?
bne .L2             ; yes
mov w0, w2           ; return rt
ret
```

这个程序与GCC生成的x64程序（请参见指令19.30）十分相似。

其中，CSEL指令的全称是“ConditionalSelect”。它依据TST指令设置的n标志位，相应地从候选的两个操作中选取一个数据并复制给w2。本例
中，它的返回值是w0。

# 19.5.6 ARM64 + Non-optimizing GCC 4.9

本节再次使用19.5.2节中所示的优化功能，以便编译器生成的代码十分大。

由于编译器关闭了优化功能，所以编译器生成的代码十分大。

> 指令19.35 Non-optimizing GCC (Linaro) 4.8

```
f:
sub    sp, sp, #32
str    x0, [sp,8]      ; store "a" value to Register Save
Area
str    wzr, [sp,24]    ; rt=0
str    wzr, [sp,28]    ; i=0
b      .L2
.L4:
ldr    x0, [sp,28]
mov    x1, 1
lsl    x0, x1, x0     ; X0 = X1<<X0 = 1<<i
mov    x1, x0
; X1 = 1<<i
ldr    x0, [sp,8]
; X0 = a
and    x0, x1&x0     ; X0 = X1&X00 = (1<<i) & a
; X0 contain zero? then jump to .L3, skipping "rt" increment
cmp    x0, xzr
beq   .L3
; rt++
ldr    w0, [sp,24]
mov    w0, w0, 1
```