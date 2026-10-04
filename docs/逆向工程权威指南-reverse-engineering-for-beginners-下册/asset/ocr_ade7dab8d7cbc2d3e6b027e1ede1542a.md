```
beq $a0, locret_94
move $a2, $v0
loc_28:
f+8C    # CODE XREF:
    lb $a0, 0($a2)
    or $at, $zero
    beq $a0, loc_80
    or $at, $zero
    bne $v1, $a0, loc_60
    move $a3, $a1
    addiu loc_60, $a2, 1
loc_48:
f+68    # CODE XREF:
    lb $t1, 0($a3)
    or $at, $zero
    beq $t1, locret_10
    or $at, $zero
    bne $t0, $t1, loc_80
    addiu $a2, 1
loc_60:
f+40    # CODE XREF:
    lb $t0, 0($a2)
    or $at, $zero
    bnez $t0, loc_48
    addiu $a3, 1
    lb $a0, 0($a3)
    or $at, $zero
    beq $a0, locret_10
    or $at, $zero
loc_80:
f+30    # CODE XREF: # f+38 ...
    addiu $v0, 1
    lb $a0, 0($v0)
    or $at, $zero
    bnez $a0, loc_28
    move $a2, $v0
locret_94:
f+20    # CODE XREF:
    jr $ra
    move $v0, $zero
```

# 100.3 练习题2.6

100.3.1 Optimizing MSVC 2010