```
seg00:001186C4 47 C5 06 3F      rlwi. %r0, %r3, 24
seg00:001186C8 41 82 00 18      beq     loc_1186E0
seg00:001186CC 38 61 00 38      addi   %r3, %sp, 0x50+var_18
seg00:001186D0 80 9F 00 00      lwz     %r4, dword 24B704
seg00:001186D4 48 00 C0 55      b       .RBEFINDNEXT
seg00:001186D8 60 00 00 00      nop
seg00:001186DC 48 00 00 1C      b       loc_1186E0
seg00:001186E0
seg00:001186E0                  loc_1186E0:  # CODE XREF: check2+44j
seg00:001186E0 80 8F 00 00      lwz     %r5, dword_24B704
seg00:001186E4 38 81 00 38      addi   %r4, %sp, 0x50+var_18
seg00:001186E8 36 60 08 02      li      %r3, 0x1234
seg00:001186EC 48 00 BF 99      b       .RBEFINDFIRST
seg00:001186F0 60 00 00 00      nop
seg00:001186F4 3B 00 0C 01      li      %r3, 1
seg00:001186F8
seg00:001186F8                  loc_1186F8:  # CODE XREF: check2+58j
seg00:001186F8 54 60 04 3F      rlwi. %r0, %r3, 16
seg00:001186FC 41 82 00 00      beq     must_jump
seg00:00118700 38 70 00 00      li      %r3, 0               #
error
seg00:00118704 48 00 00 1C      b       exit
seg00:00118708
seg00:00118708                  must_jump:  # CODE XREF: check2+78j
seg00:00118708 7F A3 EB 78      mr      %r3, %r29
seg00:0011870C 48 00 00 31      bl       check3
seg00:00118710 60 00 00 00      nop
seg00:00118714 54 60 06 3F      rlwi. %r0, %r3, 24
seg00:00118718 41 22 FF 0C      beq     skip
seg00:0011871C 38 00 00 01      li      %r3, 1
seg00:00118720
seg00:00118720                  exit:      # CODE XREF: check2+30j
seg00:00118720 80 01 00 58      lwz     %r0, 0x50+arg_8(%sp)
seg00:00118724 38 21 00 50      addi   %r4, %sp, 0x50
seg00:00118728 83 E1 FF 5C      lwz     %r31, var_4(%sp)
seg00:0011872C 7C 08 03 A6      mtrl     %r0
seg00:00118730 83 C1 FF 88      lwz     %r30, var_8(%sp)
seg00:00118733 83 A1 FF F44      lwz     %r29, var_C(%sp)
seg00:00118738 48 20 00 20      blr     # End of function check2
seg00:00118738
```

因为可执行文件保留了部分函数名称，所以分析的难度并不是很高。例如，程序文件中有 .RBEFINDNEXT() 等函数名。这可能是编译器留下的符号。虽然无法确定这种情况的具体原因，但在不了解文件格式的情况下，我们可以参考与类似的PE