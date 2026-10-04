```
add ecx, 1
movzx edx, BYTE PTR [ecx]
test dl, dl
jne .L2:
```

```
pop ebx
ret .L3
```

# 指令清单15.8 Optimizing Keil 6/2013 (ARM mode)

```
f PROC
MOV r1,#0
|L0.4| LDRB r2,[r0#0]
CMP r2,#0
MOVEQ r0,r1
BXEQ lr
CMP r2,#0x20
ADDEQ r1,r1,#1
ADD r0,r0,#1
B |L0.4|
ENDP
```

# 指令清单15.9 Optimizing Keil 6/2013 (Thumb mode)

```
f PROC
MOVS r1,#0
B |L0.12|
|L0.4| CMP r2,#0x20
BNE |L0.10|
ADDS r1,r1,#1
|L0.10| ADDS r0,r0,#1
|L0.12| LDRB r2,[r0#0]
CMP r2,#0
BNE |L0.4|
MOVS r0,r1
BX lr
ENDP
```

# 指令清单15.10 Optimizing GCC 4.9 (ARM64)

```
f: ldrb w1,[x0]
cbz w1,.L4
mov w2,0 .L3:
```

```
cmp w1,32
ldrb w1,[x0,1]!
csinc w2,w2,w2,ne
cbnz w1,.L3
```