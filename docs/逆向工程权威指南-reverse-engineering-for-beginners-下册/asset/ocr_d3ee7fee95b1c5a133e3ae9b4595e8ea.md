```
str wzr, [sp,12]
b   .L2
```

```
str wzr, [sp,8]
b   .L3
```

```
ldr w1, [sp,12]
ldr w0, [sp,8]
mul w3, w1, w0
adrp x0, x0, :lo12:tbl
add x2, x0, tbl
lldrsw x4, [sp,8]
lldrsw x1, [sp,12]
mov x0, x1
lsl x0, x0, 2
add x0, x0, 1
lsl x0, x0, 1
add x0, x0, x4
str w3, [x2,0,lsl 2]
ldr w0, [sp,8]
add w0, w0, 1
str w0, [sp,8]
```

```
ldr w0, [sp,8]
cmp w0, 9
ble .L4
ldr w0, [sp,12]
add w0, w0, 1
str w0, [sp,12]
```

```
ldr w0, [sp,12]
cmp w0, 9
ble .L5
mov w0, 0
add sp, sp, 16
ret
```

指令清单18.62 Non-optimizing GCC 4.4.5 (MIPS) (IDA)

```
main:

var_18      = -0x8
var_10      = -0x10
var_C       = -0xC
var_4       = -4

addiu      $sp, $sp, -0x18
sw          $fp, $sp
move        $fp, $sp
la          $gp, __gnu_local_gp
sw          $gp, 0x18+var_18($sp)
sw          $zero, 0x18+var_C($fp)
bl          loc_A0
```