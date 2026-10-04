```
my_memcp:
; RDI = destination address
; RSI = source address
; RDX = size of block
test rdx, rdx
je .L41
lea rax, [rdi+16]
cmp rsi, rax
lea rax, [rdi+16]
setae cl
cmp rdi, rax
setae al
or cl, al
je .L13
cmp rdx, 22
jbe .L13
mov rcx, rsi
push rbp
push rbx
neg rcx
and ecx, 15
cmp rcx, rdx
cmova rcx, rdx
xor eax, eax
test rcx, rcx
je .L4
movzx eax, BYTE PTR [rsi]
cmp rcx, 1
mov BYTE PTR [rdi], al
je .L15
movzx eax, BYTE PTR [rsi+1]
cmp rcx, 2
mov BYTE PTR [rdi+1], al
je .L16
movzx eax, BYTE PTR [rsi+2]
cmp rcx, 3
mov BYTE PTR [rdi+2], al
je .L17
movzx eax, BYTE PTR [rsi+3]
cmp rcx, 4
mov BYTE PTR [rdi+3], al
je .L18
movzx eax, BYTE PTR [rsi+4]
cmp rcx, 5
mov BYTE PTR [rdi+4], al
je .L19
movzx eax, BYTE PTR [rsi+5]
cmp rcx, 6
```