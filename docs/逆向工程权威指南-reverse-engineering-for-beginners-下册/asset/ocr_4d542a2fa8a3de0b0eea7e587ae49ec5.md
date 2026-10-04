```
rep movsd
movsw
movsb
p edi edinpop esi
ret 0
_memcpy_123 ENDP.
```

GCC分配了一个大型的通用的函数。这个函数适用于任意大小的n内存块复制操作。

# 指令清单43.21 采用GCC 4.8.1优化

```
memcpy_123:
.LFB3:
push edi
mov eax, 123
push esi
mov edx, DWORD PTR [esp+16]
mov esi, DWORD PTR [esp+12]
lea edi, [esp+10]
test edi, 1
jne .L24
test edi, 2
je .L25
```

```
.L7:
mov ecx, eax
xor edx, edx
shr ecx, 2
test al, 2
rep movsd
je .L8
mmovzx eax, WORD PTR [esi]
mov WORD PTR [edi], dx
mov edx, 2
```

```
.L8:
test al, 1
je .L5
movzx eax, BYTE PTR [esi+edx]
mov BYTE PTR [edi+edx], al
```

```
.L5:
pop esi
pop edi
ret
```

```
.L24:
movzx eax, BYTE PTR [esi]
lea edi, [esp+11]
```