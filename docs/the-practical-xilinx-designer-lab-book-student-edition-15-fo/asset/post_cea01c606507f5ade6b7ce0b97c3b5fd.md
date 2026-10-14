
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

Now the question is: With all the new additions and features, will it fit in the FPGA? Here is the utilization of an XC4005XL FPGA when loaded with the version of DWARF containing the ABEL version of the controller:

## Design Summary

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

And here is the utilization of an XC4005XL FPGA when loaded with the version of DWARF containing the VHDL version of the controller:

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

While both versions fit in the XC4005XL FPGA, the VHDL version uses slightly more than half of the FPGA while the ABEL version nearly fills the FPGA.

Now we need a test program for DWARF. A simple program that adds a list of numbers is shown next. Notice that the program starts at address 2, since this is the RAM address where DWARF begins fetching instructions after a reset.

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

The instruction opcodes are stored in file ADDLIST.HEX as follows:

- 0E 0002 40 00 01 40 10 02 40 00 03 29 A0 8B 03 40
- 10 0010 01 A0 89 01 40 FF A0 8A 02 40 FF 92 C8 20 00 0B
- 04 0020 23 6B D0 22
- 10 7F00 01 23 45 67 89 AB CD EF FE DC BA 98 76 54 32 10

The first three lines of ADDLIST.HEX just list the instruction opcodes and operands for the program. These are loaded into DWARF's PROGRAM region starting at hexadecimal address 0x0002. The 16 values on the last line, however, get loaded into the DATA region of DWARF's memory, which starts at hexadecimal address 0x7F00. This will initialize the data list that the program will operate on.

You can download the DWARF microprocessor and the ADDLIST.HEX program to the XS40 Board just like we did for the GNOME microprocessor:

C:\XCPRO\DWARF_40> XSLOAD ADDLIST.HEX DWARF_40.BIT

Then you can use the following command sequences to reset DWARF to the beginning of the program and interrupt it. (We did not load an ISR into DWARF's memory, so an interrupt will not be handled correctly.) You can also single-step DWARF through an instruction cycle. Since different instructions require differing numbers of clock cycles, it is not possible to give a fixed command sequence for single-stepping through an entire instruction. Therefore,
