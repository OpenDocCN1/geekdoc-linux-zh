```
VMOV R2, R3, D16
BLX _pow
VMOV D16, R0, FC1
MOV R0, 0xFFC1 ; "32.01 ^ 1.54 = %lf\n"
ADD R0, PC
VMOV R1, R2, D16
BLX _pintf
MOVS R1, R0
STR
MOV R0, [SP,#0xC+var_C]
MOV R0, R1
ADD, SP, #4
POP {R7,PC};
```

```
dbl_2F90    DCDF 0.3201 ; DATA XREF: _main+6
dbl_2F98    DCDF 1.54      ; DATA XREF: _main+E
```

前文介绍，ARM系统可以在借助D字寄存器的情况下，通过一对R字寄存器传递64位浮点数，由于我们没有启用编译器的优化选项，所以它还是D字寄存器传递浮点数。

从可以看出，R0和R1寄存器给_pow函数传递了第一个参数，R2和R3寄存器给函数传递了第二个参数。函数通过计算存储在R0和R1寄存器中的对，而后_pow的运算结果通过D16寄存器传递给R1和R2寄存器，以此类printf()函数传递传递参数。

# 17.6.3 ARM + Non-optimizing Keil 6/2013 (ARM mode)

```
_main
STMFD SP,[R4-R6,LR]
LDR R2,0xA3D70A44      ; y
LDR R3,0x3FF8A3D7      ; x
LDR R0,0xAE147AE1      ; x
LDR R1,0x40400147
BL _pow
MOV R4, R0
MOV R2, R4
MOV R3, R1
ADR R0,a32_011_54Lf    ; "32.01 ^ 1.54 = %lf\n"
BL _2printf
MOV R0,#0
LDMFD SP,[R4-R6,PC];
y                    DCD 0xA3D70A4      ; DATA XREF: _main+4
dword_5200 DCD 0x3FF8A3D7  ; DATA XREF: _main+8
; double x
x                    DCD 0xAE147AE1      ; DATA XREF: _main+C
dword_5288 DCD 0x40400147  ; DATA XREF: _main+10
a32_011_54Lf  DCB "32.01 ^ 1.54 = %lf",0xA,0
                                     ; DATA XREF: _main+24
```