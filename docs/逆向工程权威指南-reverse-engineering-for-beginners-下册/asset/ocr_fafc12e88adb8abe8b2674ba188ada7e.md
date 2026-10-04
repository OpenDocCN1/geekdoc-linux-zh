# 12.3.1 x86

在编译含有条件运算符的语句时, 早期无优化功能的编译器会以编译
“if/else”语句的方法进行处理。

```
指令清单.12.18 Non-optimizing MSVC 2008

$SG746    DB      'it is ten', 00H
$SG747    DB      'it is not ten', 00H

tv65      = -4 ; this will be used as a temporary variable
a$        = 8
_f       PROC
                push
                mov     ebp, esp
                push    ecx
                ; compare input value with 10
                cmp     DWORD PTR _a$[ebp], 10
                ; jump to $LN30f if not equal
                jne     SHORT $LN39f
                ; store pointer to the string into temporary variable:
                mov     DWORD PTR tv65[ebp], OFFSET $SG746 ; 'it is ten'
                ; jump to exit
                jmp     SHORT $LN40f
$LN30f:
                ; store pointer to the string into temporary variable:
                mov     DWORD PTR tv65[ebp], OFFSET $SG747 ; 'it is not ten'
```

```
指令清单.12.19 Optimizing MSVC 2008

$SG792    DB      'it is ten', 00H
$SG793    DB      'it is not ten', 00H

a$        = 8 ; size = 4
_f       PROC
                ; compare input value with 10
                cmp     DWORD PTR _a$[esp-4], 10
                mov     eax, OFFSET $SG792 ; 'it is ten'
                ; jump to $LN40f if equal
                je      SHORT $LN40f
                mov     eax, OFFSET $SG793 ; 'it is not ten'
$LN40f:
                ret     0
```