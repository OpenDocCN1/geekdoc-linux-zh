```
push	eax
call	_allmul ; long long multiplication
pop	ebp
ret	0
f_mul	ENDP
```

```
a$ = 8 ; size = 8
b$ = 16 ; size = 8
f_div	PROC
push	ebp
mov	ebp, esp
mov	eax, DWORD PTR _b$[ebp+4]
push	eax
mov	ecx, DWORD PTR _b$[ebp]
push	ecx
mov	edx, DWORD PTR _a$[ebp+4]
push	edx
mov	eax, DWORD PTR _a$[ebp]
push	eax
call	_aulldiv ; unsigned long division
pop	ebp
ret	0
f_div	ENDP
```

```
a$ = 8 ; size = 8
b$ = 16 ; size = 8
f_rem	PROC
push	ebp
mov	ebp, esp
mov	eax, DWORD PTR _b$[ebp+4]
push	eax
mov	ecx, DWORD PTR _b$[ebp]
push	ecx
mov	edx, DWORD PTR _a$[ebp+4]
push	edx
mov	eax, DWORD PTR _a$[ebp]
push	eax
call	_aullrem ; unsigned long long remainder
pop	ebp
ret	0
f_rem	ENDP
```

乘除法运算非常复杂。所以编译器通常借助标准库函数来处理乘除法运算。

如需了解库函数的各种详细信息，请参见附录E。