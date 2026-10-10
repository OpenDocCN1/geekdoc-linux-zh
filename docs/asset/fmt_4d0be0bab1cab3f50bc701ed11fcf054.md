
# 第 8 章 使用指针重构程序

```
adrp x0, 0x420000
add x0, x0, #030          // x0 <- address var1 (0x42030)
adrp x1, 0x420000
add x1, x1, #028          // x1 <- address var2 (0x42028)
str w1, [x0]               // [x0] <- w1
adrp x0, 0x420000
add x0, x0, #038          // x0 <- address var3 (0x42038)
adrp x1, 0x420000
add x1, x1, #02c          // x1 <- address var4 (0x420c)
str w1, [x0]               // [x0] <- w1
adrp x0, 0x420000
add x0, x0, #030          // x0 <- address var1 (0x42030)
ldr x0, [x0]               // x0 <- [x0]
ldr w1, [x0]               // w1 <- [x0]
mov w1, #x1               // w1 <- 1
str w1, [x0]               // [x0] <- w1
adrp x0, 0x420000
add x0, x0, #038          // x0 <- address var3 (0x42038)
ldr x0, [x0]               // x0 <- [x0]
mov w1, #x1               // w1 <- 1
str w1, [x0]               // [x0] <- w1
adrp x0, 0x420000
add x0, x0, #038          // x0 <- address var3 (0x42038)
ldr x0, [x0]               // x0 <- [x0]
adrp x1, 0x420000
add x1, x1, #038          // x1 <- address var3 (0x42038)
ldr x1, [x1]               // x3 <- [x1]
ldr w2, [x1]               // w2 <- [x1]
adrp x1, 0x420000
add x1, x1, #030          // x1 <- address var1 (0x42030)
ldr x1, [x1]               // x1 <- [x1]
ldr w1, [x1]               // w1 <- [x1]
```

`add w1, w2, w1          // w1 <- w2 + w1`

`str w1, [x0]               // [x0] <- w1`

`adrp x0, 0x420000`

`add x0, x0, #030          // x0 <- address var1 (0x42030)`

`ldr x0, [x0]               // x0 <- [x0]`

`ldr w1, [x0]               // w1 <- [x0]`

`add w1, w1, #0x1       // w1 <- w1 + 1`

`str                    // [x0] <- w1`

`add x0, x0, #038          // x0 <- address var3 (0x42038)`

`ldr x0, [x0]               // x0 <- [x0]`

`adrp x1, 0x420000`

`add x1, x1, #038          // x1 <- address var3 (0x42038)`

`ldr x1, [x1]               // x1 <- [x1]`

`ldr w2, [x1]               // w2 <- [x1]`

`adadrp x1, 0x420000`

`add x1, x1, #030          // x1 <- address var1 (0x42030)`

`ldr x1, [x1]               // x1 <- [x1]`

`ldr w1, [x1]               // w1 <- [x1]`

`mul w1, w2, w1         // w1 <- w2 *`

`str w1, [x0]           // [x0] <- w1`

## 重构 C/C++ 代码：部分 2

现在我们将伪代码与可能的混合 C/C++ 和汇编语言等价物分类：

```
x0 <- address var1 (0x420030)  // int *var1;

x1 <- address var2 (0x420028)  // int var2;

x0 <- address var3 (0x420038)  // int *var3;

x1 <- address var4 (0x4202c)  // int var4;
```

# 第 8 章：使用指针重构程序

```
0x0000000000000454 <4>:  add     x0, x1, #028

0x0000000000000458 <8>:  add     x3, x0, #08

0x000000000000045c <12>:  str     w1, [x1#40]

0x0000000000000460 <16>:  mov     w1, #02      // #2

0x0000000000000464 <20>:  add     x2, x0, #018

0x0000000000000468 <24>:  str     w1, [x0#8]

0x000000000000046c <28>:  mov     w1, #04      // #4

0x0000000000000470 <32>:  str     x2, [x0#16]

0x0000000000000474 <36>:  str     w1, [x0#24]

0x0000000000000478 <40>:  mov     w0, #00      // #0

0x000000000000047c <44>:  ret
```

汇编转储（`assembl dump`）。

在这段代码中，我们也看到了格式为 `str regSrc, [regDst, #offset]` 的指令。这意味着偏移量被加到 `regDst` 寄存器中的地址上。来自 `regSrc` 寄存器的值被移动到组合地址 `regDst + offset` 所指向的内存单元中：

```
[regDst + offset] <- regSrc
```
