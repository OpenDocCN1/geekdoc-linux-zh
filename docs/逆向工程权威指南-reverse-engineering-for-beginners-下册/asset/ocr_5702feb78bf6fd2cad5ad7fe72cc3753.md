# 13.1.6 MIPS

# 指令清单13.3 Optimizing GCC 4.4.5(IDA)

f:

```
lui      ( __gnu_local_gp >> 16)
; is it it 2?
       Li      $v0, 1
       beq    $a0, $v0, loc_60
       la      $gp, (__gnu_local_gp & 0xFFFF) ; branch
delay slot
; is it 2?
       Li      $v0, 2
       beq    $a0, $v0, loc_4C
       or      $at, $zero ; branch delay slot, NOP
; jump, if not equal to 0:
       bnez    $a0, loc_38
       at, $zero ; branch delay slot, NOP
; zero case:
       lui    $a0, ($LC0 >> 16) # "zero"
       lw      $t9, (puts & 0xFFFF) ($gp)
       or      $at, $zero ; load delay slot, NOP
       jr      $t9 ; branch delay slot, NOP
       la      $a0, ($LC0 & 0xFFFF) # "zero"; branch
```

delay slot

```
#
loc_38: # CODE XREF: f+1C
loc_4C: # CODE XREF: f+14
       lui    $a0, ($LC3 >> 16) # "something unknown"
       lw      $t9, (puts & 0xFFFF) ($gp)
       or      $at, $zero ; load delay slot, NOP
       jr      $t9
       la      $a0, ($LC3 & 0xFFFF) # "something unknown"
```

delay slot

```
#
       lui    $a0, ($LC2 >> 16) # "two"
       lw      $t9, (puts & 0xFFFF) ($gp)
       or      $at, $zero ; load delay slot, NOP
       jr      $t9
       la      $a0, ($LC2 & 0xFFFF) # "two"; branch
```

delay slot

```
#
       lui    $a0, ($LC1 >> 16) # "one"
       lw      $t9, (puts & 0xFFFF) ($gp)
       or      $at, $zero ; load delay slot, NOP
       jr      $t9
       la      $a0, ($LC1 & 0xFFFF) # "one"; branch
```

在汇编层面，每个分支的最后一条指令都是puts() 函数的指令。而且每一个case分支都通过跳转指令JR (Jump Register)调用