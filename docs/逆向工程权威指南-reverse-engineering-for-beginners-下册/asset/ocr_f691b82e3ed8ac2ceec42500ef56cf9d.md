```
18 adrp x0, .LC1
19 add x0, x0, :lol12:.LC1
20 ; form address of x global variable:
21 adrp x1, x
22 add x1, x1, :lol12:x
23 bl _isoc99_scan
24 ; form address of x global variable again:
25 adrp x0, x
26 add x0, x0, :lol12:
27 ; load value from memory at this address:
28 ldr w1, [x0]
29 ; load pointer to the "You entered %d...n" string:
30 adrp x0, .LC2
31 add x0, x0, :lol12:.LC2
32 bl printf
33 ; return 0
34 mov w0, 0
35 ; restore FP and LR:
36 ldp x29, x30, [sp, 16]
37 ret
```

# 7.2.7 MIPS

未初始化变量为全局变量

以未初始化变量为全局变量为例。对于程序，该程序在声明变量x的时候没有对它进行初始化赋值，所以在IDA中变量x出现在，在bss ELF中（请参见3.5.1节的全局指针）。

> 指令清单.7 Optimizing GCC 4.4.5 (IDA)

```
.text:00406C0 main:
.text:00406C0
.text:00406C0 var_10      = -0x10
.text:00406C0 var_4       = -4
.text:00406C0
; function prologue:
.text:00406C0          lui      $gp, 0x42
.text:00406C4          addiu    $sp, -0x20
.text:00406C8          li       $gp, 0x41894
.text:00406CC          sw       $ra, 0x20+var_4($sp)
.text:00406D0          sw       $sw, 0x20+var_10($sp)
; call puts():
.text:00406D4          la       $t9, $sp
.text:00406D8          lui      $a0, 0x40
.text:00406DC          jalr     $t9, $sp
.text:00406E0          la       $a0, aEnterX # "Enter X: "
```