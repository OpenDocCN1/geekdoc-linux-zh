# 0DBAF574 0 1
Oracle Database 11g Enterprise Edition Release 11.2.0.1.0 -
Production

...
这个表的字段名中有ADDR和INDEX。

继续使用IDA分析kqf.o的时候，我们会发现在kqftab表里有一个
指向X$u$VERSION字符串的指针。

# 指令清单81.6 kqf.o

```
.rodata:0803CAC0 dd 9
; element number 01f6
.rodata:0803CAC4 dd offset _2__STRING_13113_0
; "X$VERSION"
.rodata:0803CAC8 dd 4
.rodata:0803CACC dd offset _2__STRING_13114_0
; "kqvt"
.rodata:0803CAD0 dd 4
.rodata:0803CAD4 dd 4
.rodata:0803CAD8 dd 0
.rodata:0803ADC dd 4
.rodata:0803CAE0 dd 0Ch
.rodata:0803CAE4 dd 0FFFFC075h
.rodata:0803CAE8 dd 3
.rodata:0803CAEC dd 0
.rodata:0803CAF0 dd 7
.rodata:0803CAF4 dd offset _2__STRING_13115_0
; "X$QFSZ"
.rodata:0803CAF8 dd 5
.rodata:0803CAFC dd offset _2__STRING_13116_0
; "kqfsz"
.rodata:0803CB00 dd 1
.rodata:0803CB04 dd 38h
.rodata:0803CB08 dd 0
.rodata:0803CB0C dd 7
.rodata:0803CB10 dd 0
.rodata:0803CB14 dd 0FFFFC09Dh
.rodata:0803CB18 dd 2
.rodata:0803CB1C dd 0
```

上述指令中有很多处都引用了以X$开头的数据表名称。很显然，这些名字都是Oracle数据库的数据表名称。鉴于公开资料没有这