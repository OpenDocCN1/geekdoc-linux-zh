
```
010C 50    push ax
010D 5A    pop dx
; AX = 11Ch, BX = 140h, DX = 11Ch, SP = FFEh and SS:[FFFE]=214h
010E 58    pop ax
; AX = 214h, BX = 140h, DX = 11Ch and SP = 0
010F 35 34 28 x ax, 2834h
; AX = 97Bh, BX = 140h, DX = 11Ch and SP = 0
0112 29 37    push ax
0113 5E    pop si
; AX = 97Bh, BX = 140h, DX = 11Ch, SI = 97Bh and SP = 0
0114 29 37    sub [bx],si
0116 43    inc bx
0117 43    inc bx
0118 29 37    sub [bx],si
011A 7D 24    short near ptr word_10140
011C 45 49 43 ... db 'EICAR-STANDARD-ANTIVIRUS-TEST-FILE!'
0140 48 2B word_10140 dw 2B48h ; CD 21 (INT 21) will be here
0142 48 2A    dw 2A48h ; CD 20 (INT 20) will be here
0144 0D    db 0Dh
0145 0A    db 0Ah
```

笔者在上述代码里添加了各种注释，以介绍执行指令后各寄存器和栈的状态。

本质上说，这个程序的关键指令（下文称为“核心指令”）只有：

```
B4 09    MOV AH, 9
BA 1C 01    MOV DX, 11Ch
CD 21    INT 21h
CD 20    INT 20h
```

INT 21的第9号功能（AH寄存器）的作用是显示字符串。系统中DS:DX获取字符串的指针，然后把它输出到屏幕上。另外，这种字符串必须以“$”字符结尾。当前的操作操作系统显然继续兼容了这种指令。此过的指令属于CP/M（Control Program for Microcomputers），来自MS-DOS还要古老的磁盘操作系统。

由此可见，EICAR的主要功能是：

-   奇寄存器（AH和DX）传递预定值。
-   在内存中准备INT 21和INT 20的opcode。
-   执行INT 21和INT 20。

严格地讲，核心指令的基本都都不是显示字符。EICAR采用“拼凑”指令的方法，把核心指令拼凑成了可存储在字符串里的显示字符组合。这项“拼凑”技术还通用于shellcode。

有关“用显示字符表示的opcode”，请参见本书附录A. 6. 5。

[1] 请参见https://en.wikipedia.org/wiki/EICAR_test_file。

# 第83章 实例演示

编写Demo程序不仅要求编程人员具备熟练的数学技巧、卓越的计算机绘图水平，而且非常考验他们手写代码的基本功。

```
83.1  10PRINT CH$(20.5+RND(1));:GOTO 10
```

本节介绍的程序都是MS-DOS环境下的COM程序。

在参考资料[a12]里，我们找到了一个非常简单的随机图案生成程序。虽然它的功能只是不停地在屏幕上打印斜杠和反斜杠，但是这两种字符最终构成几种几何图案，如图83.1所示。

图83.1 一种随机图案

在16位的x86平台上，这种算法非常多。

# 83.1.1 Trixter的42字节程序

Trixter在他的网站上[1]公开了具备42字节的程序。笔者把它摘录出来，并标注了自己的注释：

```
00000000:B001      mov       ; set 25 video mode
00000002:CD10      int       10h
00000004:30FF      xor       bh      ; video page for int 10h
00000006:B9D007      mov       cx,07D0  ; 2000 characters to output:
00000009:31C0      xor       ax,al
0000000B:9C        push              ; push flags; get random value from timer chip
0000000C:FA        cli              ; disable interrupts
0000000D:E643      out       043,al      ; write 0 to port 43h; read 16-bit value from port 40h
0000000F:E440      in        al,04
00000011:88C4      mov       ah,al
00000013:E440      in        al,04; restoring IF flag
00000015:9D        popf              ; enable interrupts by
00000016:86C4      mov       ah,al; we have 16-bit pseudorandom value
00000018:D1E8      shr       ax,1
0000001A:D1E8      shr       ax,1;; CF carry second bit from the value
0000001C:B05C      mov       al,05C  ; if CF=1, skip the next instruction
0000001E:7202      jc        0000022  ; if CQ, reload AL register with another character
00000020:B02F      mov       al,02F  ; output character
00000022:B40E      mov       ah,00E
00000024:CD10      int       10h
00000026:E2E1      loop      0000009  ; loop 200 times
00000028:CD20      int       21h       ; exit to DOS
```

实际上的，上述程序中的随机数是Intel 253计时器（硬件）回传过来的。它用了计数器，而时钟决定这个计时器每秒递增一次。向43端口发送零，相当于发送了“通用计数器”“计数器的输出”和“采用二进制（返回二进制）”三条指令。当程序执行POPF时，CPU恢复标识的同时，在使用IN读取数据时，返回值写到寄存器里，所以出现数据交换。

# 83.1.2 笔者对Trixter算法的改进：27字符

这个程序并没有使用计时器查询确切时间，而是用它来生成随机数。因此，我们没有必要屏蔽中断，我们只需要返回的低位数据即可。笔者对Trixter程序稍作修改，把它改为27字符的程序：

```
00000000:B001      mov       cx,07D0 ; limit output to 2000 characters
00000003:31C0      xor       ax,ax ; command to timer chip
00000005:E643      out       043,al ; write 0 to port 43h
00000007:E440      in        al,04  ; read 8-bit of timer
00000009:D1EB      shr       ax,1   ; get second bit to CF
0000000B:D1EB      shr       ax,1   ; CF carry have second bit from the value
0000000D:B05C      mov       al,05C  ; '\'
0000000F:7202      jc        0000013  ; if CF=1, skip the next instruction
00000011:B02F      mov       al,02F  ; '/'
00000013:B40E      mov       ah,00E
00000015:CD10      int       10h
00000017:E2EA      loop      0000000 ; loop 200 times
00000019:CD20      int       21h       ; exit to DOS
```

# 83.1.3 从内存读取随机数

MS-DOS系统完全没有保护机制。换句话，应用程序可以访问内存数据。不仅如此，在使用DSB读取数据的时刻，即使程序没有先设置寄存器，也可以获取数据。

# 83.14 其他

应当注意的是：在DosBox、Windows NT主机、甚至是MS-DOS主机上运行同一个程序，看到的图案都可能是不同的。影响程序结果的因素有：模拟器对Intel 823计时器的模拟，寄存器的不同初始值，以及其他因素。

# 83.2 曼德博集合

多少年来，编程人员不懈地钻研曼德博集合[5]的各种算法。本文将要介绍的，是Sir_Lagslot在2009年发表的曼德博集合的Demo程序[6]。这个程序由30个16位x86指令构成，文件由。
