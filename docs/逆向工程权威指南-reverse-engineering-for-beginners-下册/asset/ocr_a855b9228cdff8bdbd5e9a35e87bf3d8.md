```
k2 = ctx->KEY[2];
k3 = ctx->KEY[3];
```

```
n = TEA_ROUNDS;
while (n-- > 0) {
    sum += TEA_DELTA;
y += ((z << 4) + k0) ^ (z + sum) ^ ((z >> 5) + 
    z = ((y << 4) + k2) ^ ((y + sum) ^ ((y >> 5) + 
k3);
}
```

```
out[0] = cpu_to_le32(y);
out[1] = cpu_to_le32(z);
```

其详细结果如下所示：

指令清单93.2 Linux Kernel 2.0.4 for Itanium 2 (McKinley)

```
0090|                   tea_encrypt:
0090|08 80 80 41 00 21    adds r16 = 96, r32
// ptr to ctx->KEY[2]
0096|80 02 00 42 00        adds r8 = 88, r32
// ptr to ctx->KEY[0]
009C|00 00 04 00             nop.i 0
00A0|09 18 70 41 00 21    adds r3 = 92, r32
// ptr to ctx->KEY[1]
00A6|F0 20 28 28 00        ld4 r15 = [r34], 4
// load z
00AC|44 06 01 84            adds r32 = 100, r32;;
// ptr to ctx->KEY[3]
00B0|08 98 00 20 10 10    ld4 r19 = [r16]
// r19=k2
00B6|01 00 00 42 40        mov.i r6=0
// r0—是0
00BC|08 CA 00             mov.i r2 = ar.lc
// 保存lc
00C0|05 70 00 44 10 9E EE FF 7F 20    ld4 r14 = [r34]
// load y
00CC|0F2 32 CE 6B            mov.i r17 =
0xFFFFFFFE9E3779B99; // TEA_DELTA
00D0|08 00 00 00 01 00    nop.m 0
00D6|50 01 20 20 20 00    ld4 r21 = [r8]
// r21=k0
00DC|F0 09 2A 00            mov.i ar.lc = 31
//TEA_ROUNDS=32
00E0|0A A0 00 06 10 10    ld4 r20 = [r3];
```