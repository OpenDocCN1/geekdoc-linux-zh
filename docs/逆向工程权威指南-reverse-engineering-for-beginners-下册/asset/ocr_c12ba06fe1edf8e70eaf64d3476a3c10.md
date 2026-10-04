ITLE表示如果“小于或等于(Less or Equal)”的条件成立，则执行then模块的第2条指令，否则（“大于”情况下）执行else模块的第3条。

虽然I-T-E类型的指令可以多个T和多个E，但是编译器还没有聪明到按需分配好排列组合的程序。以“愤怒的小鸟”（iOS俄典版）为例，那么彼的编译器的只能执行“IT, ITTE, ITT, ITTT, TTTT”这几种判断指令。调查IT生成的汇编指令清单可以证明这些点。在生成汇编清单文件的过程中，使用相关指令同步负责对每条指令的字节操作。由于IT的第16位的opcode是0xBF，我们应当使用的Linux分析指令是：

```
cat AngryBirdsClass.lst | grep "BF" | grep "IT" > results.lst
```

另外，如果您使用ARM的语言手动编写Thumb-2模式的应用程序，那么你要在输出判断后添加相应的条件前后，编译器就会自动添加相应的IT验证标志位。

# Non-optimizing Xcode 4.6.3 (LLVM) (ARM mode)

指令清单21 Non-optimizing Xcode 4.6.3 (LLVM) (ARM mode)

```
b = -0x20
a = -0x18
val_to_return = -0x10
saved_R7 = -4

STR R7, [SP,#saved_R7!]
MOV R7, SP
SUB SP, SP, #0x1c
BIC SP, SP, #7
VMOV D16, R2, R3
VMOV D17, R0, R1
STR D17, [SP,#0x20+a]
STR D16, [SP,#0x20+b]
VLDR D16, [SP,#0x20+a]
VLDR D17, [SP,#0x20+b]
VCMP.F64 D16
VMRS APSR,nczv, FPSR
BLE loc_2E08
VLDR D16, [SP,#0x20+a]
VSTR D16, [SP,#0x20+val_to_return]
B
```

```
loc_2E08
VLDR D16, [SP,#0x20+b]
VSTR D16, [SP,#0x20+val_to_return]
```

```
loc_2E10
VLDR D16, [SP,#0x20+val_to_return]
```