# 指令清单48.5 ARM模式下的Keil 6/2013优化程序

```
toupper PROC
SUB r0,r0,#0x61
CMP r1,#0x19
SUBLS r0,r0,#0x20
ANDLS r0,r0,#xff
BX lr
ENDP
```

从这里的程序我们可以看到，R1的值小于或等于019（十进制的19），那么就会执行SUBLS和ANDLS指令。这两条指令实际执行的是转换大写字母的操作。

而Thumb模式下的Keil优化可以通过比较比较指令进行大写转换。

# 指令清单48.6 Thumb模式下的Keil 6/2013的优化指令

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

最后的两条指令组合（LLS和LRS）的整体作用就是“AND reg.0FF”。用C/C++表示写法的话，就可以表示为“(i<<24)>>24”，也就是先左移动24位。显然，Thumbe模式下的Keil认为，它们这里的2个双字节的指令比“AND reg, 0FF”的运行效率更高（它首先要将00FF载入寄存器，然后做AND（与操作操作）”。

+   48.2.1 ARM64的GCC

# 指令清单48.7 ARM64的非优化GCC 4

```
toupper:
sub sp, sp,#16
strb w0,[sp,15]
ldrb w0,96
bls .L2
ldrb w0,[sp,15]
cmp w0,122
bhi .L2
```