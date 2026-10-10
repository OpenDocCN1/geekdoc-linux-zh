```
+0xC8      STD      r4,-0x89(sp)      ; save r4
+0xCc      COPY     ret1,r3
+0xD0      STD      dp,-0x80(sp)
+0x14      MEIFA    r1
+0x18      ADDIL    -0x800,r1
+0x1C      LDD      0x76c(r1),r31
+0x20      LDI      0xa,r19               ; i = 10
+0x24      STW      r19,-0x78(sp)         ; store i
+0x28      LDD      -0x78(sp),arg0        ; arg0 = i
+0x2C      BLL      0x1e88,rp             ; call proc()
+0x30      LDO      -0x30(sp),ret1        ; ap = SP-0x30

+0x34      LDD      -0x80(sp),dp
+0x38      STW      ret0,-0x74(sp)
+0x3C      ADDIL    -0x800,dp
+0x40      COPY     r1,ret0
+0x44      LDD      0x760(ret0),r19
+0x48      LDO      -0x74(sp),r20
+0x4C      COPY     r19,arg0
+0x50      COPY     r20,arg1
+0x54      BRL      0x1e78,rp
+0x58      LDO      -0x30(sp),ret1

+0x5C      LDD      -0x80(sp),dp
+0x60      LDD      -0xa0(sp),rp
+0x64      LDD      -0x88(sp),r4
+0x68      BVE      (rp)
+0x6C      LDD_MB   -0x90(sp),r3

proc starting at 0x400000000001e88:
+0x0       NOP
+0x4       STD_MA   r3,0x50(sp)           ; save r3,
+0x8       STD      r4,-0x48(sp)          ; grow stack
+0xC       COPY     ret1,r3               ; save r4
+0x10      NOP                            ; r3 = ap
+0x14      STW      arg0,-0x3c(ret1)      ; save arg0 at
+0x18                                           ; ap-0x3C
+0x1C      LDO      -0x3c(ret1),r19        ; r19 = arg0
+0x20      SHLADD   r19,1,0,r19           ; r19 *= 2
+0x24      STW      r19,-0x38(sp)         ; save r19
+0x28      LDO      -0x38(sp),ret0        ; ret0 = r19
+0x2C      COPY     ret0,ret0
+0x30      LDD      -0x48(sp),r4          ; restore r4
+0x34      BVE      (rp)                  ; branch to rp
+0x38      LDD_MB   -0x50(sp),r3          ; shrink stack,
                                           ; restore r3
```