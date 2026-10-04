# flt_5C    DCFS 1.0

```
main
STMFD  SP!, {R4,LR}
MOV     R0, #0
BL      time
BL      my_srand
MOV     R4, #0x64 ; 'd'
```

```
loc_78
BL      float_rand
;=pseudandom value
LDR     R0, =aF ; "%f"
; convert float type value into double type value (printf())
will need it):
```

```
FCVTDS  D7, S0
; bitwise copy from D7 into R2/R3 pair of registers (for
printf()):
FMRRD   R2, R3, D7
BL      printf
SUBS    R4, R4, #1
BNE     loc_78
MOV     R0, R4
LMFD    SP!,{R4,PC}
```

```
aF DCB "%f",0xA,0
```

通过objdump工具对上程进行分析，看到objdump所显示的FPU指令与IDA所示的指令并不一致。这大概是因为IDA与binutils的研发人员使用的是不同的指令手册。不管原因如何，同一个FPU会有不同对应名称的情况存在。

# 指令清单22.4 Optimizing GCC 4.6.3 (objdump)

```
0000038 <float_rand>:
38:     e92d408c    push {r3, lr}
3c:     ebffffe    bl      10 <my_rand>
40:     ed9f0a05    vldr    s0, [pc,#20] ; 5c
<float_rand+0x24>
44:     e3c034ff    bic     r3, r0, #-16777216
0xff00000
48:     e3c33502    bic     r3, r3, #8388608 ; 0x0800000
4c:     e38335fe    orr     r3, r3, #106535216 ;
0x3f80000
50:     ee073a90    vmov    s15, r13
54:     ee37c0a0    vsub.32  s0, s15, s0
58:     e8bd8008    pop     {r3, pc}
```