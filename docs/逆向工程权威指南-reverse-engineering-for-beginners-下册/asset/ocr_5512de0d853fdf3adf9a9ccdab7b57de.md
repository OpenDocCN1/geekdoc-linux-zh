return rt;
);

Non-optimizing GCC 4.8.2

# 指令清单 19.29 Non-optimizing GCC 4.8.2

```
f:

    push    rbp
    mov     rbp, rsp
    mov     QWORD PTR [rbp-24], rdi    ; a
    mov     DWORD PTR [rbp-12], 0     ; rt=0
    mov     QWORD PTR [rbp-8], 0      ; i=0
    jmp     .L4
.L4:
    mov     rax, QWORD PTR [rbp-8]
    mov     rdx, QWORD PTR [rbp-24]
; RAX = 1, RDX = a
    mov     eax, ecx
; ECX = 1
    shr     rdx, cl
; RDX = RDX>>cl = a>>i
    mov     rax, rdx
; RAX = RDX = a>>i
    and     eax, eax; (eax)&1
    test    rax, ra
; the last bit is zero?
; skip the next ADD instruction, if it was so.
    je      .L3
    add     DWORD PTR [rbp-12], 1    ; rt++
.L3:
    add     DWORD PTR [rbp-8], 1     ; i++
.L2:
    cmp     QWORD PTR [rbp-8], 63    ; i < 63?
    jbe     .L4                     ; jump to the loop boday
begin, if so
    mov     eax, DWORD PTR [rbp-12] ; return rt
    pop     rbp
    ret
```

Optimizing GCC 4.8.2

# 指令清单 19.30 Optimizing GCC 4.8.2

```
1 f:
2    xor     eax, eax      ; rt variable will be in EAX
register
3    xor     ecx, ecx      ; i variable will be in ECX
register
4 .L3:
5    mov     rsi, rdi      ; load input value
```