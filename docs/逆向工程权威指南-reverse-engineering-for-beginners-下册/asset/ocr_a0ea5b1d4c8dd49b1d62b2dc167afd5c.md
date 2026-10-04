```
CONST SEGMENT
__real@4010666666666666 DQ 0401066666666666r ; 4.1
CONST ENDS
CONST SEGMENT
__real@400091eb85eb851f DQ 040091eb85eb851fr ; 3.14
CONST ENDS
TEXT SEGMENT
a$       = 8          ; size = 8
b$       = 16         ; size = 8
f PROC
    push     ebp
    mov      ebp, esp
    fld      QWORD PTR _a$[ebp]

; current stack state: ST(0) = _a
    fdiv     QWORD PTR _real@400091eb85eb851f

; current stack state: ST(0) = result of _a divided by 3.14
    fld      QWORD PTR b$[ebp]

; current stack state: ST(0) = _b; ST(1) = result of _a divided by 3.14
    fmul     QWORD PTR _real@4010666666666666

; current stack state:
    ST(0) = result of _b * 4.1;
    ST(1) = result of _a divided by 3.14
    faddp    ST(1), ST(0)

; current stack state: ST(0) = result of addition
    pop
    ret      0
ENDP
```

FLD指令从栈中读取8个字节，将这个值转换为FPU寄存器所需的80位数据格式，并存入ST(0)寄存器。

FDIV指令对ST(0)寄存器的值被除数，将参数__real@400091eb85eb851f(3.14)的值当作除数，进行除法运算。因为汇编代码不支持含有小数的浮点立即数，所以程序使用64位IEEE754格式的16进制040091eb85eb851fr表示3.14。

在FDIV运算之后，ST(0)寄存器将保存结果。