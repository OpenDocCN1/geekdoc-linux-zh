(gdb) bprintf
Breakpoint 1 at 0x400410
(gdb) run
Starting program: /home/dennis/polygon/2

Breakpoint 1, printf (format=0x400628 "a=%d; b=%d; c=%d; d=%d; e=%d;
f=%d; g=%d; h=%d") at printf.c:29
29 printf.c: No such file or directory

RSI/RDX/RCX/RBX/R9寄存器的值是传递函数的参数。RIP寄存器应该是函数的首地址。我们可以在GDB里查看各寄存器的值：

```
(gdb) info registers
rax      0x0
rbx      0x0
rcx      0x3
rdx      0x2
rsi      0x1
rdi      0x400628 4195880
rbp      0xfffffffffffd60 0xfffffffffffd60
rsp      0xfffffffffffd38 0xfffffffffffd38
r8       4
9       5
r10     0xfffffffffffffffdce0 140713488346336
r11     0xffffffffffa65f60 140713348263776
r12     0x400440 4195392
r13     0xfffffffffffe04 140713488347200
r14     0x0
r15     0x0
rip     0xffffffffffa65f60
```

(gdb) x/s $rdi
0x400628: "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n"

然后使用x/g指令显示字符中的数值。指令中的ggiant words数据的格式会标识显示出来。

```
(gdb) x/10g $rsp
0xfffffffffffd37 0x0000000000000576 0x0000000000000006
0xfffffffffffd48 0x0000000000000007 0x0000007f00000008
0xfffffffffffd58 0x0000000000000000 0x0000000000000000
0xfffffffffffd68 0x000000007f73a3e5 0x0000000000000000
0xfffffffffffd78 0x000000007ffffffe04 0x0000000100000000
```

64位系统的与32位系统的并没有太大的区别。栈里的第一个值是返回地址RA。接其后的，是三个保存在栈里的参数6、7、8。应该考虑到数值
“8”的高32位地址没有被清零，与之对应的存储空间的值为