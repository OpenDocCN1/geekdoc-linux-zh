地复用opcode，从精简opcode的总数。然而并不代表每次运行
MOVE指令时CPU都会进行实际的加法运算。CPU能够这类伪仿
进行优化处理，在运行它们的时候并不会用到ALU (Arithmetic
logic unit)。

第24行的J指令跳转到RA所指向的地址，完成被调用函数返回
调用者函数的操作。还是由于分支预测延迟效应，其后的ADDIU指令会先
由J指令运行，构成函数尾部。

我们再来看IDA生成的指令清单，熟悉一下寄存器的伪名名称。

# 代码清单.39 Optimizing GCC4.4.5(IDA)

```
1 .text:00000000 main:
2 .text:00000000
3 .text:00000000 var_10      = -0x10
4 .text:00000000 var_4       = -4
5 .text:00000000
6 ; function prologue:
7 ; set the GP:
8 .text:00000000
9 >> 16)lui               $gp, (__gnu_local_gp
10 .text:00000004      addiu    $sp, -0x20
11 .text:00000008      la       $gp, (__gnu_local_gp &
0FFFF)
12 ; save the RA to the local stack:
13 .text:0000000C      sw       $ra, 0x20+var_4($sp)
14 ; save the GP to the local stack:
15 ; for some reason, this instruction is missing in the GCC
assembly output:
16 .text:00000010      sw       $gp, 0x20+var_10($sp)
17 ; load the address of the puts() function from the GP to
18 $t9:
19 .text:00000014      lw       $t9, (puts, &0xFFFF)
($gp)
20 ; form the address of the text string in a0:
21 .text:00000018      lui      $a0, ($LC0 >> 16) #
22 "Hello, world!"
23 ; jump to puts(), saving the return address in the link
register:
24 .text:0000001C      jalr     $t9
25 .text:00000020      la       $a0, ($LC0 & 0xFFFF) #
"Hello, world!"
26 ; restore the RA:
27 .text:00000024      sw       $ra, 0x20+var_4($sp)
```