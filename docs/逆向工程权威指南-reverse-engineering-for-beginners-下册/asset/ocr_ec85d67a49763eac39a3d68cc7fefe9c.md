```
<http://gnu.nu/licenses/gpl.html>
6 This is free software to change and redistribute it.
7 There is NO WARRANTY, to the extent permitted by law. Type "show
copying"
8 and "show warranty" for details.
9 this GDB was configured as "i686-linux-gnu"
10 For bug reporting instructions, please see:
11 <http://www.gnu.org/software/gdb/bugs/>...
12 Reading symbols from /home/dennis/polygon/d_max...(no debugging
symbols found)...
13 (gdb) b d_max
14 Breakpoint 1 at 0x08048a0
15 (gdb) run
16 Starting program: /home/dennis/polygon/d_max
17
18 Breakpoint 1, 0x080484a0 in d_max ()
19 (gdb) ni
20 0x080484a4 in d_max ()
21 (gdb) disas $
22 Dump of assembler for function d_max
23 0x080484a0<0>: fld 1(%esp)
24 => 0x080484a4<4>: fld 0xc(%esp)
25 0x080484a4<8>: fch st(1)
26 0x080484aa<10>: fucom st(1),st
27 0x080484ac<12>: fcmovbe st(1),st
28 0x080484ae<14>: fstp st(1)
29 0x080484b0<16>: ret
30 End of assembler dump.
31 (gdb) ni
32 0x080484a8 in d_max ()
33 (gdb) info float
34 R7: Valid 0x3fff99999999999980+1.19999999999999956
35 =>R6: Valid 0x400d99999999999980+3.3999999999999911
36 R5: Empty 0x0000000000000000
37 R4: Empty 0x0000000000000000
38 R3: Empty 0x0000000000000000
39 R2: Empty 0x0000000000000000
40 R1: Empty 0x0000000000000000
41 R0: Empty 0x0000000000000000
42
43 Status: 0x3000
44 TOP: 6
45 Control Word: 0x037f IM DM Z OM UM PM
46 PC: Extended Precision (64-bits)
47 RC: Round to nearest
48 Tag Word: 0xfff
49 Instruction Pointer: 0x7b:0x080484a4
50 Operand Pointer: 0x7b:0xbffff18
51 Opcode: 0x0000
52 (gdb) ni
53 0x080484aa in d_max ()
54 (gdb) info float
55 R7: Valid 0x400d99999999999998+3.39999999999999911
```