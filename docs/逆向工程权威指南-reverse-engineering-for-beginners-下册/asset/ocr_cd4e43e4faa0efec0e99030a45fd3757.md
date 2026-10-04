```
ENDP
|L0.140|
  DCB "error #1\n",0
  DCB 0
  DCB 0
```

```
|L0.152|
  DCB "error #2\n",0
  DCB 0
  DCB 0
```

```
|L0.164|
  DCB 0x405ec000
|L0.168|
  DCB 0x43de0000
```

```
|L0.172|
  DCB "%f\n",0
|L0.176|
  DCB "%c, %d\n",0
```

# 指令清单21.31 Non-optimizing Keil 6/2013 (Thumb mode)

```
PROC
  PUSH {r4-6,r1}
  MOV r4,r0
  LDR r0,[r0,#0x3e8]
  CMP r0,[r4,#]
  ADRLE r0,|L0.140|
  BLE |L0.132|
  LDR r0,[r4,#4]
  CMP r0,#0xa
  ADLS r0,|L0.152|
  BLS |L0.132|
  ADD r0,r4,#0x10
  LDM r0,{r0,r1}
  LDR r3,|L0.164|
  MOV r2,#0
  BL _aeabi_mul
  MOV r5,r0
  MOV r6,r1
  LDR r0,[r4,#8]
  LDR r1,|L0.168|
  BL _aeabi_fmul
  BL _aeabi_f2d
  MOV r2,r5
  MOV r3,r6
  BL _aeabi_dadd
  MOV r2,r0
  MOV r3,r1
  ADR r0,|L0.172|
  BL printf
  LDRB r2,[r4,#0x19]
  LDRB r1,[r4,#0x18]
  POP {r4-6,r1}
  ADR r0,|L0.176|
```