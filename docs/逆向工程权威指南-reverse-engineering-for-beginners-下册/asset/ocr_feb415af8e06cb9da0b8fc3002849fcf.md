# 指令清单17.18 Angry Birds Classic

```
...
ITE NE
VMOVNE      R2, R3, D16
VMOVEQ      R2, R3, D17
BLX         _obj_c_msgSend ; not prefixed
```

“ITE”是“if-then-else”的缩写。这个指令后两条指令:第一条就是then模块，第二条就是else模块。

我们再从“愤怒的小鸟”里找段更为复杂的代码。

# 指令清单17.19 Angry Birds Classic

```
ITTT EQ     R0, R4
MOVEQ       SP, SP, #0x20
ADDEQ       [R8,R10]
POPEQ.W     [R4-R7, PC]
POPEQ
BLX         __stack_chk_fail ; not prefixed
```

ITTT里有4个T，代表语句有4条指令。根据这个信息，IDA给后续的4条指令添加了EQ后缀。

确实有IEEE EQ这种形式的指令，代表“if-then-else-else-else-else”。在解析这条指令后，IDA会给它的5条指令依次添加下述后续:

```
-EQ
-NE
-NE
-NE
```

我们继续分析“愤怒的小鸟”里的其他程序片段。

# 指令清单17.20 Angry Birds Classic

```
...
CMP.W       R0, #0xFFFFFF
ITTLE.W     R10, R0, #1
SUBLE.W     R0, R0
NEGLE       R1, R0
MOVGT       R10, R0
MOVS        R6, #0 ; not prefixed
CBZ         R0, loc_1E7E32 ; not prefixed
...
```