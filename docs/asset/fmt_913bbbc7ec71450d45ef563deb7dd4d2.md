
MSVC的优化编译结果简单懂。其中，`COMISD`的全称是“Compare Scalar Ordered Double-Precision Floating-Point Values and Set EFLAGS”。它是比较双精度标量并设置浮点标志的。

MSVC的非优化编译结果同样并不难阅读，只是程序的效率低了一些。

```assembly
a$ = 8
b$ = 16
d_max:
PROC QWORD PTR [rsp+16], xmm1
  movsd QWORD PTR [rsp+8], xmm0
  movsd xmm0, QWORD PTR a$[rsp]
  comisd xmm0, QWORD PTR b$[rsp]
  jbe SHORT LN1@d_max
  movsd xmm0, QWORD PTR a$[rsp]
  jmp SHORT LN2@d_max
$LN1@d_max:
  movsd xmm0, QWORD PTR b$[rsp]
$LN2@d_max:
  ret 0
d_max:
ENDP
```

然而`GCC` 4.4.6优化更为彻底。它直接使用`MAXSD`指令（Return Maximum Scalar Double-Precision Value），一步就可以完成。

指令清单27.9 Optimizing GCC 4.4.6 x64

```assembly
d_max:
  maxsd xmm0, xmm1
  ret
```

## 27.3.2 x86

使用`MSVC` 2012对上述代码进行优化编译，可以得到如下所示的代码。

指令清单27.10 Optimizing MSVC 2012 x86

```assembly
_a$ = 8          ; size = 8
_b$ = 16         ; size = 8
_d_max PROC
    movsd xmm0, QWORD PTR _a$[esp-4]
    comisd xmm0, QWORD PTR _b$[esp-4]
    je SHORT $LN1@d_max
    fld
    QWORD PTR _a$[esp-4]
    ret
$LN1@d_max:
    fld
    QWORD PTR _b$[esp-4]
    ret
    0
_d_max ENDP
```

这个程序用栈传递函数变量`a`和`b`，并且把函数返回值存储在`ST(0)`寄存器里。除之外它和64位的程序没有区别。

使用`OllyDlg`调试这个程序，则可以观察`COMISD`指令比较数值、设置/清零`CF`/`PF`标识位的具体过程，如图27.6所示。

### CPU - main thread, module d_max

| Address | Opcode | Instruction | Registers | FPU |
| :--- | :--- | :--- | :--- | :--- |
| 00010000 | F0F8342A | MOV EAX, [ESP+42] | | |
| 00010004 | 66F8342A | MOV EAX, [ESP+51] | EAX:00000064 | FPU:init |
| 00010008 | 55 | PUSH EBP | ECX:00000000 | FPU:0 |
| 00010009 | 8B EC | MOV EBP, ESP | EDX:00000000 | FPU:0 |
| 0001000B | C7D44200 | FLD PTR [ESP+42] | ESI:00000000 | FPU:0 |
| 0001000F | 89 EB | MOV ESP, EBP | EDI:00000000 | FPU:0 |
| 00010011 | 89D5 | MOV EBP, EAX | EBX:00000000 | FPU:0 |
| 00010014 | 89C3 | MOV EBX, ECX | ECX:00000000 | FPU:0 |
| 00010016 | 89D2 | MOV EDX, EAX | ECX:00000000 | FPU:0 |
| 00010018 | 89D1 | MOV ECX, EDX | ESI:00000000 | FPU:0 |
| 0001001A | 89D0 | MOV EAX, ECX | EDI:00000000 | FPU:0 |
| 0001001C | 5D | POP EBP | EBX:00000000 | FPU:0 |
| 0001001D | C3 | RET | EBP:00000000 | FPU:0 |
| 00010020 | F0F809D5 | MOV DWORD PTR [0:828000] | | |
| 00010024 | 8B45F68B | MOV EAX, [EBP-16] | | |
| 00010028 | 66F8342A | MOV EAX, [ESP+51] | | |
| 0001002C | F0F809D5 | MOV DWORD PTR [0:828069] | | |
| 00010030 | 8B45F68B | MOV EAX, [EBP-16] | | |
| 00010034 | 66F8342A | MOV EAX, [ESP+51] | | |
| 00010038 | C7D44200 | FLD PTR [ESP+42] | | |
| 0001003C | 89EB | MOV ESP, EBP | | |
| 0001003E | 89D5 | MOV EBP, EAX | | |
| 00010040 | 89C3 | MOV EBX, ECX | | |
| 00010042 | 89D2 | MOV EDX, EAX | | |
| 00010044 | 89D1 | MOV ECX, EDX | | |
| 00010046 | 89D0 | MOV EAX, ECX | | |
| 00010048 | 5D | POP EBP | | |
| 00010049 | C3 | RET | | |
| 00010050 | F0F809D5 | MOV DWORD PTR [0:828031] | | |
| 00010054 | 8B45F68B | MOV EAX, [EBP-16] | | |
| 00010058 | 66F8342A | MOV EAX, [ESP+51] | | |
| 0001005C | F0F809D5 | MOV DWORD PTR [0:828063] | | |
| 00010060 | 8B45F68B | MOV EAX, [EBP-16] | | |
| 00010064 | 66F8342A | MOV EAX, [ESP+51] | | |
| 00010068 | C7D44200 | FLD PTR [ESP+42] | | |
| 0001006C | 89EB | MOV ESP, EBP | | |
| 0001006E | 89D5 | MOV EBP, EAX | | |
| 00010070 | 89C3 | MOV EBX, ECX | | |
| 00010072 | 89D2 | MOV EDX, EAX | | |
| 00010074 | 89D1 | MOV ECX, EDX | | |
| 00010076 | 89D0 | MOV EAX, ECX | | |
| 00010078 | 5D | POP EBP | | |
| 00010079 | C3 | RET | | |
| 00010080 | F0F809D5 | MOV DWORD PTR [0:828024] | | |
| 00010084 | 8B45F68B | MOV EAX, [EBP-16] | | |
| 00010088 | 66F8342A | MOV EAX, [ESP+51] | | |
| 0001008C | F0F809D5 | MOV DWORD PTR [0:828001] | | |
| 00010090 | 8B45F68B | MOV EAX, [EBP-16] | | |
| 00010094 | 66F8342A | MOV EAX, [ESP+51] | | |
| 00010098 | C7D44200 | FLD PTR [ESP+42] | | |
| 0001009C | 89EB | MOV ESP, EBP | | |
| 0001009E | 89D5 | MOV EBP, EAX | | |
| 000100A0 | 89C3 | MOV EBX, ECX | | |
| 000100A2 | 89D2 | MOV EDX, EAX | | |
| 000100A4 | 89D1 | MOV ECX, EDX | | |
| 000100A6 | 89D0 | MOV EAX, ECX | | |
| 000100A8 | 5D | POP EBP | | |
