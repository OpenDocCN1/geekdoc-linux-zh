使用MSVC 2010 (启用/0x选项) 编译上述程序，可得到如下所示的代码。

# 指令清单25.2 Optimizing MSVC 2010

```
mov esp,_pos$75552 = -4      ; size = 4
mov esp,_str = 8               ; size = 4
?strlen_sse2@YAIPBD@Z PROC    ; strlen_sse2

pushebp
mov ebp, esp
and esp, -16                    ; fffffff0H
mov eax, DWORD PTR _str$[ebp]
sub esp, 12                     ; 0000000CH
push esi
mov esi, eax
and esi, -16                    ; fffffff0H
xor edx, edx
mov ecx, eax
cmp esi, eax
je SHORT $LN4@strlen_sse
lea edx, DWORD PTR [eax+1]
pad 3                          ; align next label
$LL11@strlen_sse:
mov cl, BYTE PTR [eax]
inc eax
test cl, cl
jne SHORT $LL11@strlen_sse
sub eax, edx
pop esi
mov esp, ebp
pop ebp
ret
$LN4@strlen_sse:
movdq xmm1, XWORD PTR [eax]
pxor xmm0, xmm0
pcmpeqb xmm1, xmm0
ppmovskb eax, xmm1
test eax, eax
jne SHORT $LN9@strlen_sse
$LL3@strlen_sse:
movdq xmm1, XWORD PTR [ecax+16]
add ecx, 16                     ; 00000010H
pcmpeqb xmm1, xmm0
```