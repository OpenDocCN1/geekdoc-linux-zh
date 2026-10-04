```
.text:0022B8B4 ; CODE XREF: SSQC+31j
.text:0022B8B4 loc_22B8B4 mov al, [esi]
.text:0022B8B4 mov ebx
.text:0022B8B6 pop esi
.text:0022B8B7 pop edi
.text:0022B8B8 pop edi
.text:0022B8B9 mov ds:byte_407224, al
.text:0022B8E8 mov esp, ebp
.text:0022B990 xor eax, eax
.text:0022B992 pop ebp
.text:0022B993 retn
.text:0022B994 loc_22B94: ; CODE XREF: SSQC+3Cj
.text:0022B994 mov al, [esi]
.text:0022B996 mov ebx
.text:0022B997 pop esi
.text:0022B998 pop edi
.text:0022B99 mov ds:byte_407225, al
.text:0022B99E mov esp, ebp
.text:0022BA00 xor eax, eax
.text:0022BA02 pop ebp
.text:0022BA03 retn
.text:0022BA04 loc_22BA4: ; CODE XREF: SSQC+1Fj
.text:0022BA04 movsx eax, ds:byte_407225
.text:0022BAB push esi
.text:0022BAC push eax
.text:0022BAD movsx eax, ds:byte_407224
.text:0022BB4 push eax
.text:0022BB5 lea eax, [ebp+var_44]
.text:0022BB8 offset a66CCS ; "%46%c%s%c%s"
.text:0022BBD0 push eax
.text:0022BBE0 call nl_printf
.text:0022BC33 lea eax, [ebp+var_44]
.text:0022BC36 push eax
.text:0022BC37 call strlen
.text:0022BCC0 add esp, 18h
.text:0022BC3F cmp eax, 1Bh
.text:0022BD04 jle short loc_22BDA
.text:0022BD06 mov [ebp+var_29], 0
.text:0022BDA0 loc_22BDA: ; CODE XREF: SSQC+1Cj
.text:0022BDA0 lea eax, [ebp+var_44]
.text:0022BDB0 push eax
.text:0022BDE0 call strlen
.text:0022BE33 push eax ; unsigned int
.text:0022BE34 lea eax, [ebp+var_44]
.text:0022BE47 push eax ; void *
```