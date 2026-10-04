```
; set 1st argument of printf():
    move $4,$2
; set 2nd argument of printf():
    li
    $5,-1# 0x1
; set 3rd argument of printf():
    li
    $6,$2 0x2
; set 4th argument of printf():
    li
    $7,$3# 0x3
; get address of printf():
    lw
    $2,%call16(printf)
    nop
; call printf():
    move $25,$2
    jalr $25
    nop
; function epilogue:
    lw
    $28,16($fp)
; set return value to 0:
    move $2,0
    move $sp,$fp
    lw
    $31,28($sp)
    lw
    $fp,24($sp)
    addiu
    $sp,$sp,32
; return
    j
    #31
```

指令清单6.13 Non-optimizing GCC 4.4.5 (IDA)

```
.text:00000000 main:
.text:00000000
.text:00000000 var_10 = -0x1
.text:00000000 var_8 = -8
.text:00000000 var_4 = -4
.text:00000000
; function prologue:
    .text:00000000 addiu $sp,-0x20
    .text:00000004 sw $ra,0x20+var_4($sp)
    .text:00000008 sw $fp,0x20+var_8($sp)
    .text:0000000C move $fp,$sp
    .text:00000010 la $gp,$gnu_local_gp
    .text:00000018 sw $gp,0x20+var_10($sp)
; load address of the text string:
    .text:0000001C lw $v0,aADDBDC # "a=%d; b=%d; c=%d"
; set 1st argument of printf():
    .text:00000024 move $a0,$v0
; set 2nd argument of printf():
    .text:00000028 li $a1,1
; set 3rd argument of printf():
    .text:0000002C li $a2,2
; set 4th argument of printf():
    .text:00000030 li $a3,3
```