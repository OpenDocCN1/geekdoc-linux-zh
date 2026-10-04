```
or $at, $zero ; branch delay slot, NOP
; $v0=32-bit pseudandom value
      li $vl, 0x7FFFF
; $vl1=0x7FFFF
      and $vl, $v0, $v1
; $vl1=pseudandom value & 0x7FFFF
      lui $a0, 0x3F80
; $a0=0x3F800000
      or $vl, $a0
; $vl1=pseudandom value & 0x3F800000
; matter of the following instruction is still hard to get:
      lui $v0, ($LC0 >> 16)
; load 1.0 into $f0:
      lwcl $f0, $LC0
; move value from $vl1 to coprocessor 1 (register $f2)
; it behaves like bitwise copy, no conversion done:
      mtcl $vl1, $f2
      lw $ra, 0x20+var_4($sp)
; subtract 1.0. leave result in $f0:
      sub.s $f0, $f2, $f0
      jr $ra
      addiu $sp, 0x20 ; branch delay slot
main:
var_18 = -0x18
var_10 = -0x10
var_C  = -0xC
var_8  = -8
var_4  = -4
      lui $gp, (__gnu_local_gp >> 16)
      addiu $sp, -0x28
      la $gp, (__gnu_local_gp & 0xFFFF)
      sw $ra, 0x28+var_4($sp)
      sw $s2, 0x28+var_8($sp)
      sw $s1, 0x28+var_C($sp)
      sw $s0, 0x28+var_10($sp)
      sw $gp, 0x28-18($sp)
      lw $t9, (time & 0xFFFF) ($gp)
      or $at, $zero ; load delay slot, NOP
      $t9
      jalr $a0, $zero ; branch delay slot
      move $a0
 $s2, ($LC1 >> 16) # "%f\n"
      move $a0, $v0
      la $s2, ($LC1 & 0xFFFF) # "%f\n"
      move $s0, $zero
      jal my_strand
      li $s1, 0x64 # 'd' ; branch delay slot
loc_104:
```