```
ldrw x1, [sp,40]
add x1, x4, x1
lsl x1, x1, 3
ldr x4, [sp,16]
add x4, x4, x1
ldr x1, [x1]
mfov d0, x1
mfov d1, x1
fmul d0, d0, d1
mfov x1, d0
mfov d0, x2
mfov d1, x1
fadd d0, d0, d1
mfov x1, d0
str x1, [rd]
str w0, [sp,36]
ldr w0, w0, 1
add w0, w0, 1
str
.L4:
    ldr w0, [sp,36]
    cmp w0, 199
    ble .L5
    ldr w0, [sp,40]
    add w0, w0, 1
    str
.L3:
    ldr w0, [sp,40]
    cmp w0, 299
    ble .L6
    ldr w0, [sp,44]
    add w0, w0, 1
    str
.L2:
    ldr w0, [sp,44]
    cmp w0, 99
    ble .L7
    add sp, sp, 48
    ret
```

指令清单18.47 Optimizing GCC 4.4.5 (MIPS) (IDA)

```
m:
    li $t5, 0x13880
    move $t4, zero
    li $t1, 0xC8
    li $t3, 0x12C
```

```
loc_14:
    addu $t0, a0, $t4
    addu $a3, a1, $t4
    move $v1, a2
    move $t2, zero
```