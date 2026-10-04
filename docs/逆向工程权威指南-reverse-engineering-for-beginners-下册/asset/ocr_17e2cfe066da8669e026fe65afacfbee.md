world"
.text:00000004 06 F0 2E F9 BL _printf
.text:00000008 00 20 MOVS R0, #0
.text:0000000A 10 BD POP {R4, PC}

.000000304 68 65 6C 6C +HelloWorld DCB "hello, world",0
; DATA XREF: main+2

Thumb 程序的指令，每个都对应2个字字节/16位的opcode，
这是Thumb模式程序的特征。但是Thumb模式的跳转指令BL“看上”
占用了4个字的opcode，实际上是由两个字字节组成的。单字节16
opcode传递的信息太有限，不足以调用跳转函数PC和偏移量
信息。所以，上能BL指令全为16位。第一条16位指令是传递
偏移量的高11位。而Thumb模式的
opcode是固定的2个字字符，目标地址最后一位是
0（Thumb模式的opcode的起始地址必须是2，因为高会被省略。在
执行Thumb模式的跳转指令时，处理器会将地址左移1位，形成22
位的偏移量。如果BL跳转指令将无法跳转到奇数地址，且跳转
的取值区间）附
的范围内。

程序函数的其他指令，PUSH和POP工作方式与STMFD/LDMFD相同
。虽然表面上看不出来，但实际上它们也会调整SP指针/ADR指令
与前文的作用。而MOVS指令负责返回值（R0寄存器）零。

# 3.4.3 ARM模式、开启优化选项的Code

如果不启用优化选项，Xcode 6.3将会产生大量的冗余代码，
所以开始启用优化选项，让其生成最优的代码。通过指定生成编译-03，
使用Xcode编译world。这将得到如下所示的汇编代码。

# 3.13 开启优化选项 Xcode 6.3 (LLVM) (ARM模式)

```
.text:000028C4 helloworld
.text:000028C4 80 40 2D E9 STMFD SP!,{R7, LR}
.text:000028C8 86 06 01 E3 MOV R0, #0x186
.text:000028C8 07 70 A0 E1 MOV R7, SP
.text:000028D0 00 00 A3 MOV R0, R7
.text:000028D4 00 00 8F E0 ADD R0, PC, R0
.text:000028D8 C3 05 00 EB BL _puts
.text:000028DC 00 00 A3 MOV R0, #0
```