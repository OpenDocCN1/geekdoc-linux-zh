```
.rodata:0800C504 dd offset _2__STRING_10105 ;
"GV$BH"
.rodata:0800C508 dd 4
.rodata:0800C50C dd offset _2__STRING_10103 ;
"NULL"
.rodata:0800C510 dd 3
.rodata:0800C514 dd 0
.rodata:0800C518 dd 269h
.rodata:0800C51C dd 15h
.rodata:0800C520 dd 0
.rodata:0800C524 dd FFFC1Ed
.rodata:0800C528 dd 8
.rodata:0800C52C dd 0
.rodata:0800C530 dd 4
.rodata:0800C534 dd offset _2__STRING_10106 ;
"V$BH"
.rodata:0800C538 dd 4
.rodata:0800C53C dd offset _2__STRING_10103 ;
"NULL"
.rodata:0800C540 dd 3
.rodata:0800C544 dd 0
.rodata:0800C548 dd 0F5h
.rodata:0800C54C dd 14h
.rodata:0800C550 dd 0
.rodata:0800C554 dd 0FFFC1EEh
.rodata:0800C558 dd 5
.rodata:0800C55C dd 0
```

在分析Oracle DBMS的内部文件时，很多人都会奇怪“为什么函数名称和变量名起得如此异？”这大程度上是因为Oracle是20世纪80年代的很多语言编译器都遵循的ANSI标准；函数名称和变量名不得超过6个字符（linker的局限），即“外部标识符以前6个字符为”的规则。[1]

名字以V$开头的数据视图，多（很多可能是全部）都由这个kafiviews定义的。这些视图都是固定视图（fixed Views）。从表面来看，这些数据具有显著的循环周期。因此，我们可以初步判断，kafiviews表的每个元素都由12位字段构成。借助IDA程序，我们可以轻易地再现这种12字段的数据结构。套用整个数据库表。在Oracle DBMS v11.2里，总共有1023个固定视图。即，这个文件描述了1023个预定义的视图。本章将讨论这个数字。