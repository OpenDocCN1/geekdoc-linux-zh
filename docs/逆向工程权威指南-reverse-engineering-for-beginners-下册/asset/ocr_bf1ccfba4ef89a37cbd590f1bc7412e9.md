```
.text:00000000 main:
.text:00000000 var_28 = -0x28
.text:00000000 var_24 = -0x24
.text:00000000 var_20 = -0x20
.text:00000000 var_1C = -0x1C
.text:00000000 var_18 = -0x18
.text:00000000 var_10 = -0x10
.text:00000000 var_8 = -8
.text:00000000 var_4 = -4
.text:00000000
; function prologue:
.text:00000000 addiu $sp, -0x38
.text:00000004 sw $ra, 0x38+var_4($sp)
.text:00000008 sw $fp, var_8($sp)
.text:0000000C move $fp, $sp
.text:00000010 lw $gp, gpu_local_gp
.text:00000018 sw $gp, 0x38+var_10($sp)
.text:0000001C lw $v0, aBBDCDDDEDDFGD #="a"; b=d;
C=d=d; e=d; f=d; g="
; pass 5th argument in stack:
.text:00000024 li $v1, 4
.text:00000028 sw $v1, 0x38+var_28($sp)
; pass 6th argument in stack:
.text:00000032 li $v1, 5
.text:00000036 sw $v1, 0x38+var_24($sp)
; pass 7th argument in stack:
.text:00000034 li $v1, 6
.text:00000038 sw $v1, 0x38+var_20($sp)
; pass 8th argument in stack:
.text:0000003C li $v1, 7
.text:00000040 sw $v1, 0x38+var_1C($sp)
; pass 9th argument in stack:
.text:00000044 li $v1, 8
.text:00000048 sw $v1, 0x38+var_18($sp)
; pass 1st argument in $a0:
.text:0000004C move $a0, $v0
; pass 2nd argument in $a1:
.text:00000050 li $a1, 1
; pass 3rd argument in $a2:
.text:00000054 li $a2, 2
; pass 4th argument in $a3:
.text:00000058 li $a3, 3
; call printf():
.text:0000005C lw $v0, {printf & 0xFFFFFF}($sp)
.text:00000060 or $at, $zero
.text:00000064 move $t9, $v0
.text:00000068 jalr $t9, $zero
.text:0000006C or $at, $zero ; NOP
; function epilogue:
.text:00000070 lw $gp, 0x38+var_10($fp)
; set return value to 0:
.text:00000074 move $v0, $zero
```