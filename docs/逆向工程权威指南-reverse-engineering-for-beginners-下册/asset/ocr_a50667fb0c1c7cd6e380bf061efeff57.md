```
push        0
call        DWORD PTR  __imp__exit
$LN9@main:
$LN2@main:
mov         eax, DWORD PTR  _fahr$[esp+8]
add         eax, -32                                     ;
ffff0H
lea         ecx, DWORD PTR [eax+ecx*4]                   ;
mov         eax, 954431777                                     ;
38e839H
im         ecx
sar         edx, 1
mov         eax, edx
shr         eax, 31                                     ;
000001FH
add         eax, edx                                     ;
cmp         eax, -273                                    ;
ffffefH
je         SHORT $LN1@main
push        OFFSET $SG4233                                     ; 'Error: incorrect
tperature!'
call        esi                                             ; call printf()
add         esp, 4
push        0
call        DWORD PTR  __imp__exit
$LN10@main:
$LN1@main:
push        eax
push        OFFSET $SG4234                                     ; 'Celsius: %d
call        esi                                             ; call printf()
add         esp, 8
; return 0 - by C99 standard
xor         eax, eax
pop         esi
pop         ecx
ret         0
$LN8@main:
_main  ENDEP
```

# 必须说明的是：

+   - 程序首先要把printf()函数的内存地址保存到ESI寄存器。在此之后，只要调用“CALL ESI”指令即可调用printf()函数。这是非常常见的编译技术，或许是为了方便后续频繁调用这个函数，或许是因为还有“不用白不用”的空闲寄存器。