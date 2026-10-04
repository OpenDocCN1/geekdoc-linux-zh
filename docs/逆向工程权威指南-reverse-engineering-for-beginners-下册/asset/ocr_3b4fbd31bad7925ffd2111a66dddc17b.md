# 使用MSVC 2010编译上述程序，可得到如下指令：

```
tv64 = -4      ; size=4
_a$ = 8      ; size = 4
PROC
push          ebp
mov           ebp, esp
push          ecx
mov           eax, DWORD PTR _a$[ebp]
mov           DWORD PTR tv64[ebp], eax
mov           DWORD PTR tv64[ebp], 4
ja            SHORT $LN1f
mov           ecx, DWORD PTR tv64[ebp]
jmp           SHORT $LN11f[ecx*4]
$LN6f:
push          OFFSET $SG739 ; 'zero', 0AHH
call          _printf
add           esp, 4
jmp           SHORT $LN9f
$LN5f:
push          OFFSET $SG741 ; 'one', 0AHH
call          _printf
add           esp, 4
jmp           SHORT $LN9f
$LN4f:
push          OFFSET $SG743 ; 'two', 0AHH
call          _printf
add           esp, 4
jmp           SHORT $LN9f
$LN3f:
push          OFFSET $SG745 ; 'three', 0AHH
call          _printf
add           esp, 4
jmp           SHORT $LN9f
$LN2f:
push          OFFSET $SG747 ; 'four', 0AHH
call          _printf
add           esp, 4
jmp           SHORT $LN9f
$LN1f:
push          OFFSET $SG749 ; 'something unknown', 0AHH
call          _printf
add           esp, 4
$LN9f:
mov           esp, ebp
pop           ebp
ret           0
npad          2; align next label
$LN11f:
DD            $LN6f ; 0
```