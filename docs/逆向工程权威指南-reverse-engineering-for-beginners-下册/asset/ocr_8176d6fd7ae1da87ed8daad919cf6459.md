```
jnz short loc_80483F4
mov eax, 0
locret_8048453: leave
retn
endp
```

# 100.2.3 Optimizing Keil (ARM mode)

```
PUSH {r4,lr}
LDRB r2,[r1,#0]
CMP r2,#0
POPEQ {r4,pc}
B |L0.20|
LDRB r12,[r3,#0]
CMP r12,#0
BEQ |L0.64|
LDRB r4,[r2,#0]
CMP r4,#0
POPEQ {r4,pc}
CMP r12,r4
ADDEQ r3,r3,#1
ADDEQ r2,r2,#1
BEQ |L0.20|
B |L0.64|
LDRB r2,[r2,#0]
CMP r2,#0
POPEQ {r4,pc}
ADD r0,r0,#1
LDRB r2,[r0,#0]
CMP r2,#0
MOVNE r3,r0
MOVNE r2,r1
MOVEQ r0,#0
BNE |L0.20|
POP {r4,pc}
```

# 100.2.4 Optimizing Keil (Thumb mode)

```
PUSH {r4,r5,lr}
LDRB r2,[r1,#0]
```