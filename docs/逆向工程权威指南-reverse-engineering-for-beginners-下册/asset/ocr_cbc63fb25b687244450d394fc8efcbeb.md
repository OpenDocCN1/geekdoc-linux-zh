```
fadd s0, s0, s0, s1
fcmp s0, s3
csel w2, w2, w6, pl
subs w3, w3, #1
ben .L5
scvtf s0, w2
str wl1, [x7:lo12::LANCHOR]
fmov d1, 4.0e+0
fcvt d0, s0
fmul d0, d0, d1
ldr d1, .LC0
fdiv d0, d0, d1
fcvt s0, d0
ret
```

```
.LC0:
  .word 0
.V1:
  .word 1093567616
.V2:
  .word 1013904223
.LANCHOR0:
  .word 1664525
v3.3095:
  .word 3054198896
```

# 100.6.6 Optimizing GCC 4.4.5 (MIPS)

指令100.9 Optimizing GCC 4.4.5 (MIPS) (IDA)

```
mov eax, DWORD PTR v1.2084[rip]
imimul eax, eax, 1664525
add eax, eax, 1013904223
mov DWORD PTR v1.2084[rip], eax
and eax, eax, 8388607
or eax, 1073741824
mov DWORD PTR [rsp-4], eax
movss xmm0, DWORD PTR [rsp-4]
subss xmm0, DWORD PTR .LC0[rip]
ret
```

```
push rbp
xor ebp, ebp
push rbx
xor ebx, ebx
sub rsp, 16
ret
L6:
```