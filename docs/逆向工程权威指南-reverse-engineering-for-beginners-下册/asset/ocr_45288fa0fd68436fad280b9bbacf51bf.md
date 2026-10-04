```
mov DWORD PTR [esp+8], 1972608889 ; 75939f79H
mov DWORD PTR [esp+12], 5461 ; 00001555H
mov DWORD PTR [esp], 1942892530 ; 73ce2ff_subH
mov DWORD PTR [esp+4], 2874 ; 00000b3aH
call _f_add
mov DWORD PTR [esp+4], eax
mov DWORD PTR [esp+8], edx
mov DWORD PTR [esp+12], OFFSET FLAT:LC0 ; "%11d%12\s"
call _printf
add 28
ret
```

```
_f_sub:
mov eax, DWORD PTR [esp+4]
mov edx, DWORD PTR [esp+8]
sub eax, DWORD PTR [esp+12]
sbb eax
mov edx, DWORD PTR [esp+16]
ret
```

GCC的编译结果和MSVC的编译结果相同。

# 24.2.2 ARM

> 指令清单24.7 Optimizing Keil 6/2013 (ARM mode)

```
f_add PROC
ADDS r0,r0,r2
ADC r1,r1,r3
BX lr
ENDP
```

```
f_sub PROC
SUBS r0,r0,r2
SBC r1,r1,r3
BX lr
ENDP
```

```
f_add_test PROC
PUSH {r4,lr}
LDR r2,[L0.68] ; 0x75939f79
LDR r3,[L0.72] ; 0x00001555
LDR r0,[L0.76] ; 0x73ce2ff2
LDR r1,[L0.80] ; 0x00000b3a
BL f_add
POP {r4,lr}
MOV r2,r0
```