# 除法运算的余数存储在EDX寄存器中:

```
.text:00541204 sub      edx, 0
.text:00541207 jz       short call_rotatel; if remainder
zero, go to rotatel
.text:00541209 dec      edx
.text:0054120A ja       short call_rotate2; .. if it is 1, go
to rotate2
.text:0054120C dec      edx short next_character_in_password
.text:0054120D jnz      ebx
.text:0054120F test      ebx short next_character_in_password
.text:00541211 jle      ebx
.text:00541213 mov      edi, ebx
```

如果余数为2，就会调用rotate3()。此时，EDI寄存器存储的是rotate_all_with_password()函数的第二个参数。前文介绍了，在加密过程中这个值值为1，在解密过程中这个值值为3。函数进行了循环处理。在解密时，rotate2/3的次数与函数的第一个参数相等。

```
.text:00541215 push      esi
.text:00541215         call      rotate3
.text:00541216         add      esp, 4
.text:0054121B
.text:0054121E         dec      edi
.text:0054121F jnz       short call_rotate3
.text:00541221 jmp       short
next_character_in_password
.text:00541223 call_rotate2:
.text:00541223 test      ebx, ebx
.text:00541225 jle       short
next_character_in_password
.text:00541227
.text:00541229 mov      edi, ebx
.text:00541229 loc_541229: push      esi
_in_password
.text:0054122A         call      rotate2
.text:0054122F         add      esp, 4
.text:00541232         dec      edi
.text:00541233 jnz       short loc_541229
.text:00541235 jmp       short
next_character_in_password
.text:00541237
```