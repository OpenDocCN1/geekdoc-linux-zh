|L0.40| DCB "%d\n",0

# 指令清单14.30 Optimizing GCC 4.9 (ARM64)

main:

```
stp     x29, x30, [sp, -32]!
add     x29, sp, 0
stp     x19, x20, [sp,16]
adrp    x20, .LC0
mov     w19, 1
add     x20, x20, :lo12::LC0
```

.L2:

```
mov     w19, w19
mov     x0, x20
add     w19, w19, 3
bl     printf
cmp     w19, 100
bne     .L2
ldp     x19, x20, [sp,16]
ldp     x29, x30, [sp], 32
ret
```

.LC0:

```
.string "%d\n"
```

# 指令清单14.31 Optimizing GCC 4.4.5 (MIPS)(IDA)

main:

```
var_18  = -0x18
var_10 = -0x10
var_C   = -0xC
var_8   = -8
var_4   = -4
```

```
lui     $gp, (_gnu_local_gp >> 16)
addiu   $sp, -0x28
la      $gp, (_gnu_local_gp & 0xFFFF)
sw      $ra, 0x28+4($sp)
sw      $s2, 0x28+var_8($sp)
sw      $s1, 0x28+var_C($sp)
sw      $s0, 0x28+var_10($sp)
sw      $gp, 0x28+var_18($sp)
la      $s2, .LC0	# # "%d\n"
```

loc_30:

```
lw      $t9, (printf & 0xFFFF) ($gp)
move    $al1, $s0
move    $a0, $s2
jalr    $t9
addiu   $s0, 3
lw      $gp, 0x28+var_18($sp)
```