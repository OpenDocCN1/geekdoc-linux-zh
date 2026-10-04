由此可见，程序不仅向密函数传递了加密后的字符串，而且它传递了加密密钥：

```
.text:0000DAF error               ; CODE XREF:
sync_sys+255j                               ;
.text:0000DAF                               ;
sync_sys+274j                                ...
.text:0000DA7                   mov [ebp+var_8], offset
encrypted_error_message2
.text:0000DAFE                  mov [ebp+var_C], 17h ;
decrypting key                               jmp
.text:0000DB05
decrypt_end_print_message
...
```

```
; this name we gave to label manually:
.text:0000D9B6 decrypt_end_print_message: ; CODE XREF:
sync_sys+29D9
.text:0000D9B6
sync_sys+2ABj                  mov eax, [ebp+var_18]
.text:0000D9B6                  test eax, eax
.text:0000D9B9
.text:0000D9BB                  jnz short loc_D9FB
.text:0000D9BD                  mov edx, [ebp+var_C] ; key
.text:0000D9C0                  mov ecx, [ebp+var_8] ;
string
.text:0000D9C3                  push edx
.text:0000D9C4                  push 20h
.text:0000D9C6                  push ecx
.text:0000D9C7                  push 18h
.text:0000D9C9                  call err_warn
```

这就是简单的XOR算法：每个字节都与密钥进行XOR运算，而且解密一个字符密钥增加33。

为了验证这个猜想，我们专门写了一个Python脚本程序：

```
#!/usr/bin/python
指令清单78.2 Python 3.x
import sys
```

```
msg=[0x74, 0x72, 0x78, 0x43, 0x48, 0x46, 0x65, 0x5A, 0x49, 0x4C, 0x47,
0x51, 0x4F, 0x47, 0x61, 0x20, 0x22, 0x3C, 0x24, 0x33, 0x36,
```