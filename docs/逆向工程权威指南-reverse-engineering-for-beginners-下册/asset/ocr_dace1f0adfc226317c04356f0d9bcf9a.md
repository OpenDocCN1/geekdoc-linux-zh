```
; EDX=000000cc
push edx
mov eax, DWORD PTR _a$[ebp]
; EAX=dcccbbaa
shr eax, 24
; EAX=000000dd
and eax, 255 ; probably redundant instruction
; EAX=000000dd
push eax
push OFFSET $SG2973 ; '%.d.%d.%d.%d'
call DWORD PTR __imp_printf
add esp, 20
pop ebp
ret 0
_print_as_IP ENDP
```

优化MSVC 2012程序做的和上面一样，但是它不会重新加载输入值。

# 指令清单38.5 优化MSVC 2012 /0b0

```
_a$ = 8
_print_as_IP PROC
mov size = 4
mov ecx, DWORD PTR _a$[esp-4]
; ECX=dcccbbaa
movzx eax, cl
; EAX=000000aa
push eax
mov eax, ecx
; EAX=dcccbbaa
shr eax, 8
; EAX=00ddccbb
and eax, 255
; EAX=000000bb
push eax
mov eax, ecx
; EAX=dcccbbaa
shr eax, 16
; EAX=00000ddcc
and eax, 255
; EAX=000000cc
push eax
; ECX=dcccbbaa
shr ecx, 24
; ECX=000000dd
push ecx
pushush OFFSET $SG3020 ; '%.d.%d.%d.%d'
```