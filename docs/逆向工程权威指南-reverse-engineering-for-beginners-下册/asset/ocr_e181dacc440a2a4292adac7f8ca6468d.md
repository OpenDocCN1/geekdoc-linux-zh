里，然后以地址的形式传递给其他函数。

# 指令清单64.11 优化的MSVC 2012（64位）

```
$SG2994 DB    '%ed', 0aH, 00H

a$ = 48
f  PROC
    mov     DWORD PTR [rsp+8], ecx ; save input value in
Shadow Space
    sub     rsp, 40
    lea     rcx, QWORD PTR a$[rsp] ; get address of value
    and pass it to modify_a()
    call    modify_a
    mov     edx, DWORD PTR a$[rsp] ; reload value from
Shadow Space and pass it to printf()
    lea     rcx, OFFSET:$SSG2994 ; '%d'
    call    printf
    add     rsp, 40
    ret
ENDP
```

GCC将输入的数值保存到本地。

# 指令清单64.12 优化的GCC 4.9.1（64位）

```
.LCO:
    .string "%d\n"
f:
    sub     rsp, 24
    mov     DWORD PTR [rsp+12], edi ; store input value
to the local stack
    lea     rdi, [rsp+12] ; take an address of
the value and pass it to modify_a()
    call    modify_a
    mov     edx, DWORD PTR [rsp+12] ; reload value from
the local stack and pass it to printf()
    mov     esi, OFFSET:.LC0 ; '%d'
    mov     edi, 1
    xor     eax, eax
    call    __printf_chk
    add     rsp, 24
    ret
```

ARM64下的GCC也使用了相同的方式传递参数。只是在这个平台上，这个空间被称为“寄存器（内容）保存区（Register Save Area”。