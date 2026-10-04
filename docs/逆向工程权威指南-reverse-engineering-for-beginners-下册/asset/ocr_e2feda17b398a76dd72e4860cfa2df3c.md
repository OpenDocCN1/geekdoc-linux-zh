```
jbe .L6
lea rbp, [rsi+rcx]
xor r9d, r9d
add rcx, rdi
xor ebx, ebx
```

```
.L7:
movdq xmm0, XMMWORD PTR [rbp+r9]
add rbx, 1
movups XMMWORD PTR [rcx+9], xmm0
add r9, 16
cmp rbx, r8
jb .L7
add rax, rll
cmp r10, rll
je .L1
```

```
.L6:
movzx ecx, BYTE PTR [rsi+rax]
mov BYTE PTR [rdi+rax], cl
lea rcx, [rax+1]
cmp rdx, rcx
jbe .L1
movzx ecx, BYTE PTR [rsi+1+rax]
mov BYTE PTR [rdi+1+rax], cl
lea rcx, [rax+2]
cmp rdx, rcx
jbe .L1
movzx ecx, BYTE PTR [rsi+2+rax]
mov BYTE PTR [rdi+2+rax], cl
lea rcx, [rax+3]
cmp rdx, rcx
jbe .L1
movzx ecx, BYTE PTR [rsi+3+rax]
mov BYTE PTR [rdi+3+rax], cl
lea rcx, [rax+4]
cmp rdx, rcx
jbe .L1
movzx ecx, BYTE PTR [rsi+4+rax]
mov BYTE PTR [rdi+4+rax], cl
lea rcx, [rax+5]
cmp rdx, rcx
jbe .L1
movzx ecx, BYTE PTR [rsi+5+rax]
mov BYTE PTR [rdi+5+rax], cl
lea rcx, [rax+6]
cmp rdx, rcx
jbe .L1
movzx ecx, BYTE PTR [rsi+6+rax]
mov BYTE PTR [rdi+6+rax], cl
```