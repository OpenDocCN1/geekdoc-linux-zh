```
arg_18      = 0x18
arg_1C      = 0x1C
arg_20      = 0x20
arg_24      = 0x24

lwcl        $f0, arg_14($sp)
add.d       $f2, $f12, $f14
lwcl        $f1, arg_10($sp)
lui        $v0, ($LC0 >> 16)
add.d       $f0, $f2, $f0
lwcl        $f2, arg_1C($sp)
or         $at, $zero
lwcl        $f3, arg_18($sp)
or         $at, $zero
add.d       $f0, $f2
lwcl        $f2, arg_24($sp)
or         $at, $zero
lwcl        $f3, arg_20($sp)
or         $at, $zero
add.d       $f0, $f2
lwcl        $f2, dwarf_6C
or         $at, $zero
lwcl        $f3, $LC0
jr
div.d      $f0, $f2

$LC0:       .word 0x04140000    # DATA XREF: f+C
dword_6C:   .word 0             # DATA XREF: f+3C
```

+   [1] 中文“堆机”或“堆栈结构”。请参见
http://en.wikipedia.org/wiki/Stack_machine.

+   [2] 请参见
http://en.wikipedia.org/wiki/Forth_%22programming_language%29.

+   [3] 当初，为了让FPU的32位计算机（例如80486 SX）兼容其研发的DOOM游戏，John Carmack设计了一套“软”FPU系统。这种系统使用CPU寄存器的高16位存储整数部分、16低位存储浮点数值的小数部分，通过标准32位寄存器即可实现浮点运算。更多详情请参见：
https://en.wikipedia.org/wiki/Fixed-point_arithmetic.

+   [4] 如需详细了解IEEE 754规范，请参见
http://en.wikipedia.org/wiki/IEEE_754-2008.