```
rotate_all_with_password+2A ...
mov al, [ebp+1]
inc ebp
test al, al
njnz loop_begin
pop edi
pop esi
pop ebx
exit: ; CODE XREF:
rotate_all_with_password+A
pop ebp
ret

rotate_all_with_password endp
align 10h
========== SUBROUTINE
crypt proc near ; CODE XREF: crypt file+8A
arg_0 = dword ptr 4
arg_4 = dword ptr 8
arg_8 = dword ptr 0Ch
push ebx
mov ebx, [esp+4+arg_0]
push ebp
push esi
push edi
xor ebp, ebp
loc_54126A: ; CODE XREF: crypt+41
mov eax, [esp+10h+arg_8]
cncx, 10h
mov esi, ebx
mov edi, offset cube64
push 1
push eax
rep movsvd
call
rotate_all_with_password
mov eax, [esp+18h+arg_4]
```