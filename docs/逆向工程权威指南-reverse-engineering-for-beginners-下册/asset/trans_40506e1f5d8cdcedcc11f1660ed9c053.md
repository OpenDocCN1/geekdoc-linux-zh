
首条指令MOV R3, R0属于冗余指令。即使此处有这条指令，后面的MLA指令直接复用有的寄存器也不会出现任何问题。因为我们没有启用优化选项，所以编译器对没有进行优化。

BL指令程序的控制流将LR寄存器的地址，而且在必要的时候切换处理器的运行模式（Thumb模式和ARM模式之间进行模式切换）。被调用函数f并不知道它会被切换成什么模式的代码，不知道调用函数切换的功能还是必要的。如果它被成了Thumb模式的代码，BX指令将进行跳转，还会把处理器调整为Thumb。如果它被成了ARM模式的指令f[4]调用，就不会进行模式切换。

## 8.3.2 Optimizing GCC (1/3) ARM

```
:00000098 f
:00000098 21 20 20 E0 MLA R0, R1, R2
:0000009C 1E FF 2F E0 BX LR
```

在启用最大限制的优化函数（-O3）之后，前面那条MOV指令被优化了，或者被删除了。MLA直接复用所有寄存器的参数，并将返回值保存在R0寄存器里。调用函数f而从R0寄存器获取取值。

## 8.3.3 Optimizing GCC (1/3) Thumb mode

```
:0000005E 48 43 MULS R0, R1
:00000060 80 18 ADDS R0, R1, R2
:00000062 70 47 BX LR
```

因为Thumb模式的指令集里没有MLA指令，所以编译器将其分为两个指令。第一条MULS指令计算R0和R1的积，将运算结果存储在R0寄存器里。第二条ADDDS计算R1RORR2的，并且计算结果存储在R0寄存器里。

## 8.3.4 ARM64

Optimizing GCC (Linaro) 4/9

ARM64的情况简单一些。MADD指令可以一次进行乘法和加法的混合运算，与此前的MLA指令类似。全部3个参数都用X-头的寄存器的低32传递。这是因为这些参数都是32位整数型。函数的返回值存储在W0寄存器里。

```
f:
	mtmadd w0, w0, w1, w2
main:
	ret
```

```
; save FP and LR to stack frame:
stp x29, x30, [sp, -16]!
mov w2, 3
mov w1, 2
add x29, sp, 0
mov w0, 1
bl f
mov w1, w0
adadrp x0, .LC7
add x0, x0, :lo1l2::LC7
bl printf
; return 0
mov w0, 0
; restore FP and LR
ldp x29, x30, [sp], 16
ret
```

我们来看看参数为64位uint64_t的情况:

```c
#include <stdio.h>
#include <stdint.h>
```

```c
uint64_t f (uint64_t a, uint64_t b, uint64_t c)
{
  return a+b+c;
}
int main() {
  printf("%lld\n", f(0x1122334455667788, 0x1111111112222222222, 0x333333333444444444));
  return 0;
}
f:
  madd x0, x0, x1, x2
  ret
main:
  mov x1, 13396
  adrp x0, .LC8
  stp x29, x30, [sp, -16]!
  movk x1, 0x27d0, lsl 16
  add x0, x0, :lo1l2::LC8
  mov x1, 0x122, lsl 32
  add x29, sp, 0
  movk x1, 0x58be, lsl 48
  bl
  mov w0, 0
  ldp x29, x30, [sp], 16
  ret
```

```assembly
.LC8:.string "%ld\n"
```

这两段代码的f()函数部分相同。在采用64位参数之后，程序使用了整个64位X寄存器。通过两条指令才能把长数据类型的64位值存储到寄存器里。本书在 28.3.1节详细介绍64位数据的有关操作。

Non-optimizing GCC (Linaro) 4.9

在没有优化选项的情况下，编译器生成的代码稍冗长：

```assembly
f:
sub    sp, sp, #16
str    w0, [sp,12]
str    w1, [sp,8]
str    w2, [sp,4]
ldr    w1, [sp,12]
ldr    w0, [sp,8]
mul    w1, w0
ldr    w0, [sp,4]
add    w0, w1, w0
add    sp, sp, #16
```

函数f()传入的参数存在数据里，以防止后期指令占用W0~W2 。这种技术叫做“寄存器保护/Register Save Area [参见ARM13]。但是，本例的被调用函数可以这样保存参数。寄存器保护区与8.2节介绍的十分相似。在启用优化选项后，GCC 4.9 会部分寄存器存储指令。这是因为优化后后续指令就不会操作函数参数，另用W0~W2存储的数据。此外，上述代码使用了MUL/ADD指令，而没有MADD指令。

## 8.4 MIPS

指令清单8.10 Optimizing GCC 4.5

```assembly
.text:00000000 f:
;a0=a
;a1=b
;a2=c
.text:00000000    mult    $a1, $a0
.text:00000004    mflo    $v0
.text:00000008    jr      $ra
.text:0000000C    addu    $v0, $a2, $v0
; result in v0 upon return
.text:00000010 main:
.text:00000010    var_10 = -0x10
.text:00000010    var_4 = -4
.text:00000010    lw      $gp, (__gnu_local_gp) >> 16
.text:00000010    lui     $sp, -0x20
.text:00000014    lw      $gp, (__gnu_local_gp) & 0FFFF)
.text:00000018    la      $ra, 0x20+var_4($sp)
.text:0000001C    sw      $gp, 0x20+var_10($sp)
.text:00000020    sw      $0, -0x20

; set c:
.text:00000024    li      $a2, 3
; set a:
.text:00000028    li      $a0, 1
; set b:
.text:00000030    li      $a2, 2

; result in v0 now
.text:00000034    lw      $v0, 0x20+var_10($sp)
.text:00000038    lui     $a0, ($L0) >> 16
.text:0000003C    jal     $t9, (printf & 0FFFF)
.text:00000040    la      $a0, ($L0) & 0FFFF)
.text:00000044    jal     $t9 ; take result of f()
function(): and pass it as second argument
.text:00000048    move    $a1, $v0
.text:0000004C    lw      $v0, 0x20+var_4($sp)
.text:00000050    move    $v0, $zero
.text:00000054    jr      $ra
.text:00000058    addiu   $sp, 0x20
```

函数所需的前4参数由寄存器传递。MIPS平台有两个特殊的寄存器：HI和LO。用来存储MUL指令计算结果——64位的。只有MFLO指令访问HI和LO。其中MFLO负责低32位。在本例中将低32位存储到v0。由于实例访问高2位，被弃了。我们的程序就是设计的：积是32位的整型数据。最终ADDU (Add Unsigned) 指令计算三个参数的和。

在MIPS平台上，ADD和ADDDU是不同的指令。两者的区别体现在溢出的处理上。ADD指令可以触发溢出，溢出有时候是必要的。C++不支持这种机制，所以本例中使用ADDDU而非ADD指令。

此后寄存器存储了32位运算结果。main()函数使用了JAL（Jump and Link）指令。JAL和JALR指令，前者使用的是相对地址—偏移量，后者跳转到绝对地址。JALR代表寄存器。由于f()函数和main()函数都位于同一个object文件，所以f()函数的相对地址是已知的，可以计算出来。

## 第9章 返回值

# 返回值

在x86系统里，被调用函数返回值通常通过EAX寄存器返回。若返回byte或char数据，则返回值将存储在EAX寄存器的低位——AL寄存器。如果返回值是浮点型数据，那么返回值将存储在FPU的ST(0)寄存器里。ARM系统的情况简单一些，它通常使用R0寄存器返回。

## 9.1 void类型的返回值

函数main()的数据类型通常是void而不是int，程序如何处理返回值？

调用main()有关代码大致是这样的：

```
push envp
push argv
push argc
call main
push eax
call exit
```

将其转换为源代码，也就是：

```c
exit(main(argc, argv, envp));
```

如果声明main()的数据类型是void，则main()函数不会返回任何值（没有return指令）。不过在main()函数退出时，EAX寄存器含有调用函数残留的确定，也就是说此时EAX存储的值应该是上一个函数——puts()函数的返回值。我们将一段bash脚本，观察程序的退出状态（返回值）。

## 指令清单9.2 tst.sh

```bash
#!/bin/sh
./hello_world
echo $?
```

执行上述脚本之后，我们将看到：

```
$ ./tst.sh
Hello, world!
14
```
