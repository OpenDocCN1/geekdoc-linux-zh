# 指令清单 7.10 Optimizing GCC 4.4.5 (IDA)

```
.text:004006A0   main:
.text:004006A0   var_10      = -0x10
.text:004006A0   var_8       = -8
.text:004006A0   var_4       = -4
.text:004006A0
.text:004006A0               $gp, 0x42
.text:004006A4   addiu      $sp, -0x20
.text:004006A8   lui        $gp, 0x418930
.text:004006AC   sw         $ra, 0x20+var_4($sp)
.text:004006B0   sw         $s0, 0x20+var_8($sp)
.text:004006B4   sw         $gp, 0x20+var_10($sp)
.text:004006B8   la         $t9, putx
.text:004006BC   jalr       $t9
.text:004006C0   lw         $t9, 0x40($sp)
.text:004006C4   la         $a0, (x - 0x410000) # "Enter X:"
.text:004006C8   lw         $gp, 0x20+var_10($sp)
; prepare high part of x address:
.text:004006CC   lui        $s0, 0x40
.text:004006D0   lw         $t9, isoc99_scanf
.text:004006D4   lui        $a0, 0x40
; add low part of x address to Sal:
.text:004006D8               li         $s0, (x - 0x410000)
; now address of x is in Sal:
.text:004006DC   jalr       $t9       ; isoc99_scanf
.text:004006E0   la         $a0, aD # "%d"
.text:004006E4   lw         $gp, 0x20+var_10($sp)
; get a word from memory:
.text:004006E8   lw         $al, x
; value of x is now in Sal:
.text:004006EC   lw         $t9, printf
.text:004006F0   lw         $a0, 0x40
.text:004006F4   jalr       $t9; printf
.text:004006F8   la         $a0, aYouEnteredD__ # "You
entered $d...\n"
.text:004006FC   sw         $ra, 00x20+var_4($sp)
.text:00400700   move       $v0, zero
.text:00400704   lw         $s0, 0x20+var_8($sp)
.text:00400708   jr         $ra
.text:0040070C   addiu      $sp, 0x20
...
.data:00410920               .global x
.data:00410920 x:         .word 0xA
```

为什么它没有了？data段？这可能是受到GCC选项的影响。无论如何，变量x出现在.data段里。这段代码会被加载到常规的通用内存区域，我们可以在这里看到变量的处理方法。

***