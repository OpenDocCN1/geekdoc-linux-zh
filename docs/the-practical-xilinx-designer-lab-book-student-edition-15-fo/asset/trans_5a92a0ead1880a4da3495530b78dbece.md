

NET DATA<5> LOC=P81;
NET DATA<6> LOC=P80;
NET DATA<7> LOC=P10;
NET CS_ LOC=P65;
NET OE_ LOC=P61;
NET WE_ LOC=P62;
NET OUT_PORT<0> LOC=P25; # S0 LED segment
NET OUT_PORT<1> LOC=P26; # S1 LED segment
NET OUT_PORT<2> LOC=P24; # S2 LED segment
NET OUT_PORT<3> LOC=P20; # S3 LED segment
NET OUT_PORT<4> LOC=P23; # S4 LED segment
NET OUT_PORT<5> LOC=P18; # S5 LED segment
NET OUT_PORT<6> LOC=P19; # S6 LED segment
NET OUT_PORT<7> LOC=P6;
NET IN_PORT<0> LOC=P7;
NET IN_PORT<1> LOC=P8;
NET IN_PORT<2> LOC=P9;
NET IN_PORT<3> LOC=P77;
NET IN_PORT<4> LOC=P70;
NET IN_PORT<5> LOC=P66;
NET IN_PORT<6> LOC=P67;
NET IN_PORT<7> LOC=P69;

现在的问题是：有了所有新的增加和特性，它还能装进 FPGA 吗？以下是装载了包含 ABEL 版本控制器的 DWARF 版本的 XC4005XL FPGA 的利用率：

## 设计摘要

Number of errors: 0
Number of warnings: 14
Number of CLBs: 188 out of 196 95%
CLB Flip Flops: 40
CLB Latches: 0
4 input LUTs: 323 (7 used as route-throughs)
3 input LUTs: 62 (4 used as route-throughs)
Dual Port RAMs: 8
Number of bonded IOBs: 45 out of 65 69%
IOB Flops: 16
IOB Latches: 0
Number of TBUFs: 40 out of 448 8%
Number of BUFGLSs: 1 out of 8 12%
Number of RPM macros: 2
Total equivalent gate count for design: 3784

以下是装载了包含 VHDL 版本控制器的 DWARF 版本的 XC4005XL FPGA 的利用率：

Design Summary
----------------
Number of errors:                  0
Number of warnings:               13
Number of CLBs:                 109 out of   196  55%
  CLB Flip Flops:                40
  CLB Latches:                    0
  4 input LUTs:                 174 (11 used as route-throughs)
  3 input LUTs:                  54 (2 used as route-throughs)
  Dual Port RAMs:                 8
Number of bonded IOBs:           45 out of    65  69%
  IOB Flops:                     16
  IOB Latches:                    0
Number of TBUFs:                 40 out of   448   8%
Number of BUFGLSs:                1 out of     8  12%
Number of RPM macros:             2
Total equivalent gate count for design: 2854

两种版本都能装进 XC4005XL FPGA，但 VHDL 版本使用了略多于一半的 FPGA，而 ABEL 版本几乎填满了 FPGA。

现在我们需要一个用于 DWARF 的测试程序。下面显示了一个简单的程序，它对一组数字进行求和。请注意程序从地址 2 开始，因为这是复位后 DWARF 开始取指令的 RAM 地址。

```
0002 40 00  load #0     ; R1 <- address of start of number
0004 01     store R1    ; list in DATA region
0005 40 10  load #10    ; R2 <- number of items in the list
0007 02     store R2
0008 40 00  load #0     ; R3 <- 0 (clear the sum register)
000A 03     store R3

loop:
000B 29     load (R1)   ; ACC <- the next item on the list
000C A0     clear_c     ; erase previous carry result
000D 88     add R3      ; add sum register to ACC
000E 03     store R3    ; store result back into sum register
000F 40 01  load #1     ; now, increment R1 so it points to
0011 A0     clear_c     ; the next item on the list
0012 B9     add R1
0013 01     store R1
0014 40 FF  load #FF    ; and decrement R2 since we've just
0016 A0     clear_c     ; added one more number
0017 8A      add   R2
0018 02      store R2
0019 40 FF   load  #FF   ; now test R2 to see if it is zero
001B 92      test  R2      ; (i.e., we've finished the list)
001C C8 20   jz    show    ; exit the loop if item counter is 0
001E D0 0B   jump  loop    ; otherwise, keep processing the list
show:
0020 23      load  R3      ; ACC <- sum stored in register R3
0021 6B      out           ; display sum bits on the LED display
halt:
0022 D0 22   jump  halt    ; just loop here forever
```

指令操作码存储在文件 ADDLIST.HEX 中如下：

- 0E 0002 40 00 01 40 10 02 40 00 03 29 A0 8B 03 40
- 10 0010 01 A0 89 01 40 FF A0 8A 02 40 FF 92 C8 20 00 0B
- 04 0020 23 6B D0 22
- 10 7F00 01 23 45 67 89 AB CD EF FE DC BA 98 76 54 32 10

ADDLIST.HEX 的前三行只是列出程序的指令操作码和操作数。这些被加载到 DWARF 的 PROGRAM 区域，从十六进制地址 0x0002 开始。然而，最后那一行上的 16 个值会被加载到 DWARF 内存的 DATA 区域，该区域从十六进制地址 0x7F00 开始。这将初始化程序将操作的数列。

你可以像我们为 GNOME 微处理器所做的那样，将 DWARF 微处理器和 ADDLIST.HEX 程序下载到 XS40 板上：

C:\XCPRO\DWARF_40> XSLOAD ADDLIST.HEX DWARF_40.BIT

然后你可以使用以下命令序列将 DWARF 复位到程序开头并中断它。 （我们没有将 ISR 加载到 DWARF 的内存中，因此中断将不会被正确处理。）你也可以单步执行 DWARF 的一个指令周期。由于不同的指令需要不同的时钟周期数，因此不可能给出一个固定的命令序列来单步执行整个指令。因此，

