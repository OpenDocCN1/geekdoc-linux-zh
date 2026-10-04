```
mov ecx, DWORD PTR _y$[esp-4]
mov eax, DWORD PTR _x$[esp-4]
lea edx, DWORD PTR [eax+ecx]
imul eax, ecx
mov ecx, DWORD PTR _product$[esp-4]
push esi
mov esi, DWORD PTR _sum$[esp]
mov DWORD PTR [esi], edx
mov DWORD PTR [ecx], eax
pop esi
ret 0
```

```
_main PROC
	push OFFSET _product
	push _sum
	push 456             ; 000001c8H
	push 123             ; 0000007b
	call _f1
	mov eax, DWORD PTR _product
	mov ecx, DWORD PTR _sum
	push eax
	push ecx
	push OFFSET $SG2803
	call DWORD PTR __imp__printf
	add esp, 28          ; 000000cH
	xor eax, eax
	ret 0
_main ENDP
```

如图10.1所示，我们使用OllyDbg调试这个程序。