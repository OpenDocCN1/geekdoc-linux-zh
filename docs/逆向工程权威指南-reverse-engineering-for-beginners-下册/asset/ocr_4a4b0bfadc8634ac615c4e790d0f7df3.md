在Win32版本的oracle.exe程序里不难发现这个字符串。但是是在Linux平台的文件里，函数名称和全局变量名都会走样。因此，即使在Linux版的Oracle RDBMS里找到了正确的对象（.o）文件，挖掘相应的处理函数会花费更多的时间。

在Linux版本的文件里，包含字符串“V$VERSION”的文件是kqf.o。这个文件在Oracle的库文件目录lib/libserver11.a之中。

kqf.o文件在定义数据表kqfview的时候，调用了字符串“V$VERSION”。

指令查看81.1 kqf.o

```
.rodata:0800C4A0 kqfview dd ; DATA
XREF: kqfchk:loc 8003A6D ;
.rodata:0800C4A0-\nkqfgbn+34
.rodata:0800C4A4 dd offset _2__STRING_10102_0 ;
"GV$WAITSTAT"
.rodata:0800C4A8 dd 4
.rodata:0800C4AC dd offset _2__STRING_10103_0 ;
"NULL"
.rodata:0800C4B0 dd 3
.rodata:0800C4B4 dd 0
.rodata:0800C4B8 dd 195h
.rodata:0800C4BC dd 4
.rodata:0800C4C0 dd 0
.rodata:0800C4C4 dd 0FFFF1CBh
.rodata:0800C4C8 dd 3
.rodata:0800C4CC dd 0
.rodata:0800C4D0 dd 0Ah
.rodata:0800C4D4 dd offset _2__STRING_10104_0 ;
"V$WAITSTAT"
.rodata:0800C4D8 dd 4
.rodata:0800C4DC dd offset _2__STRING_10103_0 ;
"NULL"
.rodata:0800C4E0 dd 3
.rodata:0800C4E4 dd 0
.rodata:0800C4E8 dd 4Eh
.rodata:0800C4EC dd 3
.rodata:0800C4F0 dd 0
.rodata:0800C4F4 dd 0FFFF003h
.rodata:0800C4F8 dd 4
.rodata:0800C4FC dd 0
.rodata:0800C500 dd 5
```