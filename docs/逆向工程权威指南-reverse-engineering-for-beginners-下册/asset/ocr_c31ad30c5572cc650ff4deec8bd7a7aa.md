```
.set var_8, -8
.set var_4, -4
.set arg_8, 8
stw 93 E1 FF FC %r31, var_4(%sp)
mflr 7C 08 02 8A %r0
stw 34 A8 00 00 %nli %r5, 0
stw 93 C1 FF F8 %r30, var_8(%sp)
lwl 43 C2 95 A8 %r30, off_1485E8$ #
dword_24B704
    .using dword_24B704,
stw 93 A1 FF F4 %r29, var_C(%sp)
addi 38 A3 00 00 %r29, %r3, 0
li 38 60 00 00 %r3, 0
stw 95 C0 01 00 %r0, arg_8(%sp)
stwu 94 21 FF 80 %sp, -0x50(%sp)
lwl 86 0E 00 00 %r6, dword_24B704
addi 38 81 01 38 %r4, %r5, 0x50+var_18
bl 76 4C 00 00 .RBEREADE
nop
54 60 04 03F
clrlwi.%r0, %r3, 16
beq 41 82 00 0C loc_118784
li 38 60 00 00 %r3, 0
b 78 02 02 00 exit

loc_118784: # CODE XREF:
check3+30j
A0 01 00 38 lh %r0, 0x50+18(%sp)
28 00 04 B2 cmmplwi %r0, 0x1100
81 82 00 0C beg loc_118798
38 60 00 00 li %r3, 0
48 00 02 DC b exit

loc_118798: # CODE XREF:
check3+50j
00 0E 00 00 lwz %r6, dword_24B704
38 81 01 38 addi %r4, %sp, 0x50+var_18
A38 60 00 00 li %r3, 1
A38 0A 00 00 li %r5, 1
48 00 21 0C bl .RBEREADE
nop
54 60 04 3F clrlwi.%r0, %r3, 16
41 82 00 0C beg loc_1187C0
38 60 00 00 li %r3, 0
48 00 02 B4 b exit

loc_1187C0: # CODE XREF:
check3+78j
```