CMP比较两个值相等/EQ，才会执行该指令；所以，如果RO0寄存器的值为0，则会触发CMP指令之后的两条SUBBEQ指令。其运算结果会被保留在RO寄存器中，迭代结束之后就自然成为函数的返回值。

# ARM64

# Optimizing GCC (Linaro) 4.9

my_strlen:

```
mov    x1, x0
; X1 is now temporary pointer (eos), acting like cursor
```

.L58

```
; load byte from X1 to W2, increment X1 (post-index)
lrdb   w2, [x1],1
```

```
; Compare and Branch if NonZero: compare W2 with 0, jump to
L58 if it is not
```

```
cbnz   w2, .L58
```

```
; calculate difference between initial pointer in X0 and
current address in X1
```

```
sub    x0, x0, x1
; decrement 32-bit of result
```

```
sub    w0, w0, #1
```

```
ret
```

本法的算法与指令清单15.1的算法相同。它计算字符串和终止地址的差异，然后再次减去。指令清单的解释详细介绍了具体的算法方法。不过，我们的程序中：strlen()的返回值是32int型数据，但是它是返回size_t或者另一个64位数据。理论上讲，在64位平台上，strlen()函数的参数可能是4GB以上的内存地址，所以它在64位平台上的返回值应当是64位数据。由于程序存在这个缺陷，所以最后一条SUB指令对寄存器的低32位进行操作，但是倒数第二个SUB指令仍然是对64位寄存器进行减法运算。虽然存在存在，但是是为了演示的目的，我把这个样本保留了下来。

# Non-optimizing GCC (Linaro) 4.9

my_strlen:

```
; function prologue
```

```
sub    sp, sp, #32
```

```
; first argument [str] will be stored in [sp,8]
```

```
str    x0, [sp,8]
```

```
ldr    x0, [sp,8]
```

```
; copy "str" to "eos" variable
```

```
str    x0, [sp,24]
```

.L62:

```
inc++
```

```
ldr    x0, [sp,24];   load "eos" to x0
```