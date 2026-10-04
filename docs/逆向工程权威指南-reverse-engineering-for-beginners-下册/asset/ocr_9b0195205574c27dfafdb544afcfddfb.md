```
lea     rcx, [rax+7]
cmp     rdx, rcx
jbe     .L1
movzx   ecx, BYTE PTR [rsi+7+rax]
mov     BYTE PTR [rdi+7+rax], cl
lea     rcx, [rax+8]
cmp     rdx, rcx
jbe     .L1
movzx   ecx, BYTE PTR [rsi+8+rax]
mov     BYTE PTR [rdi+8+rax], cl
lea     rcx, [rax+9]
cmp     rdx, rcx
jbe     .L1
movzx   ecx, BYTE PTR [rsi+9+rax]
mov     BYTE PTR [rdi+9+rax], cl
lea     rcx, [rax+10]
cmp     rdx, rcx
jbe     .L1
movzx   ecx, BYTE PTR [rsi+10+rax]
mov     BYTE PTR [rdi+10+rax], cl
lea     rcx, [rax+11]
cmp     rdx, rcx
jbe     .L1
movzx   ecx, BYTE PTR [rsi+11+rax]
mov     BYTE PTR [rdi+11+rax], cl
lea     rcx, [rax+12]
cmp     rdx, rcx
jbe     .L1
movzx   ecx, BYTE PTR [rsi+12+rax]
mov     BYTE PTR [rdi+12+rax], cl
lea     rcx, [rax+13]
cmp     rdx, rcx
jbe     .L1
movzx   ecx, BYTE PTR [rsi+13+rax]
mov     BYTE PTR [rdi+13+rax], cl
lea     rcx, [rax+14]
cmp     rdx, rcx
jbe     .L1
movzx   edx, BYTE PTR [rsi+14+rax]
mov     BYTE PTR [rdi+14+rax], dl

.L1:
pop     rbx
pop     rbp

.L41:
rep     ret

.L13:
xor     eax, eax

.L3:
```