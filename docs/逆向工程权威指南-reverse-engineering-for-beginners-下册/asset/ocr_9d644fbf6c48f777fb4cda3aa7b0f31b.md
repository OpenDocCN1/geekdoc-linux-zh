与ARM模式编译出的代码相比，这段代码存在明显的Thumb指令的特
证。除此之外，ARM模式和Thumb模式编译出的代码并无实际区别。

# ARM64

Non-optimizing GCC (Linaro) 4.9

指令清单6.9 Non-optimizing GCC (Linaro) 4.9

```
.LC2:
    .string "a=%d;b=%d;c=%d;d=%d;e=%d;f=%d;g=%d;h=%d\n"
; grab space in stack:
    sub sp, sp, #32
; save FP and LR in stack frame:
    stp x29, x30, [sp,16]
; set stack frame (FP=SP):
    add x29, sp, 16
    adp x0, .LC2; "a=%d;b=%d;c=%d;d=%d;e=%d;f=%d;g=%d;h=%d"
    add x0, x0, :lo12::LC2
    mov w1, 8 ; 9th argument
    str w1, [sp] ; store 9th argument in the stack
    mov w1, 1
    mov w2, 2
    mov w3, 3
    mov w4, 4
    mov w5, 5
    mov w6, 6
    mov w7, 7
    bl printf
    sub sp, x29, #16
; restore FP and LR
    ldp x29, x30, [sp,16]
    add sp, sp, 32
    ret
```

X-或W寄存器传递函数的前8个参数 [参见ARM13c]。 字符串指针使用64n位寄存器，它使用整个X寄存器，所有的其他参数都属于32位整数
据，可由寄存器的低32位/ipW寄存器传递。程序使用来传递第九个参数
（数值8）。CPU的寄存器总数有限，所以寄存器往往不足以传递全部参数。

启用优化选项之后，GCC (linaro) 4.9生成的代码与此相同。