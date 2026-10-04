
```assembly
mov ebx, [esi+ecx*4]
add ebx, [edi+ecx*4]
mov [eax+ecx*4], ebx
inc ecx
cmp ecx, edx
jb short loc_133
jmp short loc_15B

loc_143: ; CODE XREF: f(int,int,*int,*int,*int,*int)+17
    ; f(int,int,*int,*int,*int)+3A ...
mov esi, [esp+10h+1]
mov edi, [esp+10h+2]
xor ecx, ecx

loc_14D: ; CODE XREF: f(int,int,*int,*int,*int,*int)+159
mov ebx, [esi+ecx*4]
add ebx, [edi+ecx*4]
mov [eax+ecx*4], ebx
inc ecx
cmp ecx, edx
jb short loc_14D

loc_15B: ; CODE XREF: f(int,int,*int,*int,*int)+A
    ; f(int,int,*int,*int,*int)+129 ...
xor eax, eax
pop ecx
pop ebx
pop esi
pop edi
retn

loc_162: ; CODE XREF: f(int,int,*int,*int,*int)+8C
    ; f(int,int,*int,*int,*int)+9F
xor ecx, ecx
jmp short loc_127
?f@YAHHPAH0@Z endp
```
