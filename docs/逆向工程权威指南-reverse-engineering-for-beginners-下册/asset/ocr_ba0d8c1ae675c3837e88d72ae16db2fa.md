# 图17.15 OllyDbg: 执行第二条FLD指令

# Optimizing MSVC 2010

指令清单17.11 Optimizing MSVC 2010

```
a$ = 8              ; size = 8
b$ = 16             ; size = 8
d_max             PROC           
fld                QWORD PTR _b$[esp-4]
fld                QWORD PTR _a$[esp-4]

; current state: ST(0) = _a, ST(1) = _b
fcom               ST(1) ; compare _a and ST(1) = (_b)
fnstsw            ah, 65 ; 00000041H
jne                SHORT $LN5@d_max
; copy ST(0) to ST(1) and pop register
leave (_a) on top
fstp               ST(1)

; current state: ST(0) = _a
ret                0
$LN5@d_max:
; copy ST(0) to ST(0) and pop register
leave (_b) on top
fstp               ST(0)

; current state: ST(0) = _b
ret                0
d_max             END
```

FCOM指令和前面用的FCOMP指令有不同，它不操作FPU。而且本例的操作数也和前文有区别，这里是倒序的。所以，FCOM生成的条件标志位的语义与前例相同。

+   * 如果a>b，对C3、C2、C0的值位为0、0。
* 如果b>a，对应数值为0、1。
* 如果a=b，对应数值为1、0、0。

就是说，“test ah, 65”这条指令仅仅比较两个标志位——C3（第6位/bit）和C0（第0位/bit）。在a=b的情况下，两者都为0：这种情况下，程序不会被触发JE跳转，并且执行后的FST ST(1）指令，将ST（0）的值复制到操作数中，然后从FPU里抛出一个值。换句话，这条指令把