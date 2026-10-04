# 3.4.4 Thumb-2下、开启优化选项的Xcode (LLVM)

默认情况下，Xcode 4.6.3 会启用优化模式，并以Thumb-2模式编译源程序。

# 指令清单3.14 Optimizing Xcode 4.6.3 (LLVM) (Thumb-2模式)

```
text:00002B6C                hello_world
__text:00002B6C 80 B5               PUSH           {R7,LR}
__text:00002B6E 41 F2 D8 30    MOV           R0,
#0x13D8
__text:00002B72 6F 46                MOV            R7, SP
__text:00002B74 C0 F2 00 00    MOVT.W         R0, #0
__text:00002B78 78 44                ADD            R0, PC
__text:00002B7A 01 0F 38 EA    BLX            __puts
__text:00002B7E 20 00               MOVS           R0, #0
__text:00002B80 80 BD                POP            {R7,PC}
cstring:00003E70 48 65 6C 6F 20+aHelloWorld "DCB"
word!",0xA,0
```

上文提到，Thumb-2模式下的BLX和BL指令是以两个116位指令的形式出现的。在Thumb-2模式下，BLX和BL指令的伪指令有明显的32位指令特征，其对应的opcode都以0Fx或0xEx开始。

在显示Thumb和Thumb-2模式程序的opcode时，IDA以两个字节为单位进行显示。在显示ARM模式的指令时，IDA以字节为单位、依次逆序显示其opcode。这是字节序的排版差异。

简单来说，在IDA显示ARM平台的指令时，其显示顺序为：

+   * ARM及ARM64模式的指令，opcode以4-3-2-1的顺序显示。
* Thumb模式的指令，opcode以2-1的顺序显示。
* Thumb-2模式的16位指令对，其opcode以2-1-4-3的顺序显示。

在IDA中，我们可观察到上述MOV、MOVT.W、BLX指令都以0Fx开头