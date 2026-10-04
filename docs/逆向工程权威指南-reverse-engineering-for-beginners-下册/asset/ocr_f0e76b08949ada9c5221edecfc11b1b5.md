```
MOVS r3,r0
MOVS r1,#0
MOVS r2,#1
MOVS r0,r1
|L0.10|
MOVS r4,r3
LRS r4,r4,r1
LSLS r4,r4,#28
LRS r4,r4,#28
MULS r4,r2,r4
ADDS r0,r4,r0
MOVS r4,#0xa
MULS r2,r4,r2
ADDS r1,r1,#4
CMP r1,#0lc
BLE [L0.10]
POP (r4,pc)
```

指令序列1.65 Non-optimizing GCC 4.9 (ARM64)

```
f:
sub sp, sp,#32
str w0, [sp,12]
str wz, [sp,28]
mov w0, 1
str w0, [sp,24]
str wz, [sp,20]
b .L2
```

```
.L3:
ldr w0, [sp,28]
ldr w1, [sp,12]
isr w0, w1,w0
and w1, w0,15
ldr w0, [sp,24]
mul w0, w1,w0
ldr w1, [sp,20]
add w0, w1,w0
str w0, [sp,20]
ldr w0, [sp,28]
add w0, w0,4
str w0, [sp,28]
ldr w1, [sp,24]
mov w0, w1
isl w0, w0,2
add w0, w0,w1
isl w0, w0,1
str w0, [sp,24]
```

```
.L2:
ldr w0, [sp,28]
cmp w0, 28
ble .L3
ldr w0, [sp,20]
```