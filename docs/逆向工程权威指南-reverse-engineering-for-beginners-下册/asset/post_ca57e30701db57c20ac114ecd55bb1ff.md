
```asm
.text:00022BE8 mov eax, [edi]
.text:00022BEA push eax ; int
.text:00022BEB call _write
.text:00022BF0 add esp, 10h
.text:00022BF3 pop ebx
.text:00022BF4 pop esi
.text:00022BF5 pop edi
.text:00022BF6 mov esp, ebp
.text:00022BF8 pop ebp
.text:00022BF9 retn
.text:00022BFA db 0Eh dup(90h)
.text:00022BFA2 SSQC endp
```

虽然，该程序要和驱动程序通信。

# 而且，只有这个下形转换函数使用了SSQC(C)函数：

```asm
.text:0000DBE8 public SSQ
.text:0000DBE8 SSQ proc near ; CODE XREF: sys_info+A9p
.text:0000DBE8 ; sys_info+CBP...
.text:0000DBE8 arg_0 = dword ptr 8
.text:0000DBE8 push ebp
.text:0000DBE9 mov ebp, esp
.text:0000DBEB mov edx, [ebp+arg_0]
.text:0000DBEE push edx
.text:0000DBEF call SSQC
.text:0000DBF4 add esp, 4
.text:0000DBF7 mov esp, ebp
.text:0000DBF9 pop ebp
.text:0000DBFFA retn
.text:0000DBF82 SSQ endp
```

调用(SSQ)函数的指令至少有两个处：

其中一处是：

```asm
.data:0040169C _51_52_53 dd offset aPressAnyKeyT_0 ; DATA
.data:0040169C init_sys+392r
.data:0040169C ;
sys_info+Air ;
.data:0040169C ;
"PRESS ANY KEY TO CONTINUE: " 
.data:004016A0 dd offset a51 ; "51"
.data:004016A4 dd offset a52 ; "52"
.data:004016A8 dd offset a53 ; "53"
...
```

```asm
.data:004016B8 _3C_or_3E dd offset a3c ; DATA
XREF sys_info:loc_D67Br
.data:004016B8 ; "3C"
.data:004016BC dd offset a3e ; "3E"
```

```asm
; these names we gave to the labels:
.data:004016C0 answers1 dd 6B05h ; DATA
XREF sys_info+E7r
.data:004016C4 dd 3D387h
.data:004016C8 answers2 dd 3CCh ; DATA
XREF sys_info+F2r
.data:004016CC dd 8382h
.data:004016D0 _C_and_B db 0Ch ; DATA
XREF sys_info+F1Bar
.data:004016D0;
sys_info:OKr
.data:004016D1 byte_4016D1 db 0Bh ; DATA
XREF sys_info+F4r
.data:004016D2 db 0
...
```

```asm
.text:0000D652 xor eax, eax
.text:0000D654 mov al, ds:ctl_port
.text:0000D659 mov ecx, _51_52_53[eax*4]
.text:0000D660 push esp
.text:0000D661 call SSQ
.text:0000D666 add esp, 4
.text:0000D669 cmp eax, 0FFFFF
.text:0000D66E jz short loc_DD1
.text:0000D670 xor ebx, ebx
.text:0000D672 mov al, _C_and_B
.text:0000D677 test al, al
.text:0000D679 jz short loc_DC0
.text:0000D67B loc_D7B; CODE XREF: sys_info+106
.text:0000D67B mov eax, _3C_or_3E[eax*4]
.text:0000D682 push eax
.text:0000D683 call SSQ
.text:0000D688 push offset a4 ; "4G"
.text:0000D68D push offset a12345678 ; "012345678"
.text:0000D697 call SSQ
```

“3C”和“3E”看起来很熟：它是私有的、加密哈希函数，用于Rainbow公司的一款内存加密狗。

# 第四章详细介绍哈希函数

就这个程序而言，我们可以据此判断加密狗有无信息。这款加密狗不包含存档；换句话说这个程序向加密狗写数据。连续出现的数字字符就是指令码，由SSQ函数接收和处理。其他字符串的哈希值是用十六进制形式存储在加密狗里。因为厂商的加密算法是私有的，所以编写替换它或者用插件加密的方法通过。但是，“访问加密狗的操作、而找到对应的哈希值”确实麻烦的话，我们还可以模拟程序逻辑、基于私有的哈希函数重建一个软件，而是使用自制软件替代原软件进行加密。

代码51/52/53用于选择LPT接口，3/4用于选择相应的加密狗系列。不同类型的加密狗连接在同一个LPT口上，区分加密的工作应当由程序完成。除了字符串“012345678”以外，传递哈希值的都是双字节字符串。然后函数返回的哈希值与系列有效值进行比较。若该值有效，全局变量ctl_model将被赋值为0C或0B。此外，程序还定义了字符串“PRESS KEY TO CONTINUE:”应当通过加密狗认证之后的提示信息。不过整个程序没有调用这个字符串，恐怕属于源程序的bug。

接下来，我们关注全局变量ctl_mode的读取指令。其中一条是：

```asm
.text:00000708 prep_sys proc near ; CODE XREF: init_sys+46A
.text:00000708 var_14 = dword ptr -14h
.text:00000708 var_10 = byte ptr -10h
.text:00000708 var_8 = dword ptr -8h
.text:00000708 var_2 = dword ptr -2h
.text:00000708 push ebp
.text:00000709 mov eax, ds:net_env
.text:0000070E mov ebp, esp
.text:00000710 sub esp, 1Ch
.text:00000713 test eax, eax
jnz short loc_D734
mov al, ds:ctl_model
test al, al
jnz short loc_D77e
mov [ebp-8], offset "I-ceulnvnV\bOK]T"
mov edx, 7
jmp loc_D7E7
```

```asm
loc_D7E7; CODE XREF: prep_sys+24j
push prep_sys+33j
push edx
mov edx, [ebp-8]
push 20h
push edx
push 16h
call err_warn
push offset_station_sem
; 如果0，那么一条经过加密处理的错误信息将被传递到解密程序，从而出现在屏幕上。
call ClosSem
call startup_err
```

这个错误信息的解密方法是非常XOR算法：

```asm
err_warn proc near ; CODE XREF:
prep_sys+E8p
; prep_sys2+2F
var_55 = byte ptr -55h
var_54 = byte ptr -54h
arg_0 = dword ptr 8
arg_4 = dword ptr 0C
arg_8 = dword ptr 10h
arg_C = dword ptr 14h
push ebp
mov ebp, esp
sub esp, 54h
push edi
mov ecx, [ebp+arg_8]
xor edi, edi
```

```asm
.text:0000A448 test ecx, ecx
.text:0000A44A push esi
.text:0000A44B jz loc_A466
.text:0000A44D mov esi, [ebp+arg_C]; key
.text:0000A450 mov edx, [ebp+arg_4]; string
.text:0000A453 loc_A453:           ; CODE
XREF: err_warn+28j
.text:0000A453 xor eax, eax
.text:0000A455 mov al, [edx+edi]; load
crypted byte
.text:0000A458 xor eax, esi; ; decrypt
it
.text:0000A45D add esi, 3; ; change
key for the next byte
.text:0000A45E inc edi
.text:0000A460 cmp edi, [ebp+var_55], al
.text:0000A464 jl short loc_A453
.text:0000A466 loc_A466:         ; CODE
XREF: err_warn+F
.text:0000A466 mov [ebp+var_54], 0
.text:0000A46B mov eax, [ebp+arg_0]
.text:0000A46E cmp eax, 18h
.text:0000A473 jnz short loc_A9C
.text:0000A475 lea eax, [ebp+var_54]
.text:0000A478 push eax
.text:0000A479 call status_line
.text:0000A47E add esp, 4
.text:0000A481 loc_A481:         ; CODE
XREF: err_warn+72j
.text:0000A481 push 50h
.text:0000A483 push 0
.text:0000A485 lea eax, [ebp+var_54]
.text:0000A488 push eax
.text:0000A489 call memset
.text:0000A48E call pcv_refresh
.text:0000A493 add esp, 0Ch
.text:0000A496 pop esi
.text:0000A497 pop edi
.text:0000A498 mov esp, ebp
.text:0000A49A pop ebp
.text:0000A49B retn
.text:0000A49C loc_A49C:         ; CODE
XREF: err_warn+37j
.text:0000A49C push 0
.text:0000A49E lea eax, [ebp+var_54]
.text:0000A4A1 mov edx, [ebp+arg_0]
.text:0000A44 push edx
.text:0000A45 push eax
.text:0000A46 call pcv_luts
.text:0000A4AB add esp, 0Ch
.text:0000A4AE jump short loc_A481
.text:0000A4AE err_warn endp
```

由于程序对提示信息进行了加密处理（这是常见手段），所以我无法在执行程序里直接找到出错的提示信息。

此外，程序里还有一个调用函数SSQ(Q)的地方。在调试过程中，该程序向调用函数传递了字符串“offln”。后续指令将返回0xFE81和0x12A9。如果两个值不匹配，程序将使用timer()函数（类似于等待用户重新加入），然后在屏幕上显示另一个错误提示信息:

```asm
.text:0000DA55 loc_DA55: ; CODE
XREF: sync_sys+24j
.text:0000DA55 push offset aoffln
"offln"
.text:0000DA5A call SSQ
.text:0000DA5F add esp, 4
.text:0000DA62 mov dl, [ebx]
.text:0000DA64 mov esi, eax
.text:0000DA66 cmp dl, 0Bh
.text:0000DA69 jz short loc_DA83
.text:0000DA6B cmp esi, 0FE81h
.text:0000DA71 jz
.text:0000DA77 cmp esi, 0FFFFFEh
.text:0000DA7D jz
.text:0000DA83 loc_DA83: ; CODE
XREF: sync_sys+201
.text:0000DA83 mov cl, [ebx]
.text:0000DA85 cmp dl, 0Ch
.text:0000DA88 jz short loc_DA9F
.text:0000DA8A cmp esi, 12A9h
.text:0000DA90 jz
.text:0000DA96 cmp esi, 0FFFF5h
.text:0000DA99 jz
.text:0000DA9F loc_DA9F: ; CODE
XREF: sync_sys+220
.text:0000DA9F mov eax, [ebp+var_18]
.text:0000DAA2 test eax, eax
.text:0000DAA4 jz short loc_DAB0
.text:0000DAA6 push 24h
.text:0000DAA8 call timer
.text:0000DAAD add esp, 4
.text:0000DAB0 loc_DAB0: ; CODE
XREF: sync_sys+23j
.text:0000DAB0 inc edi
.text:0000DAB0 edi, 3
.text:00000DAB1 jle short loc_DA55
.text:0000DAB4 mov eax, ds:net_env
.text:0000DAB6 eax
.text:0000DABB test short
.text:0000DABD jz
.text:0000DAF7 error: ; CODE
XREF: sync_sys+255
.text:0000DAF7...
sync_sys+274
.text:0000DAF7 mov [ebp+var_8], offset encrypted_message2
.text:0000DAFE mov [ebp+var_C], 17h ; decrypting key
.text:0000DB05 jmp decrypt_end_print
...
```

```asm
; this name I gave to label:
.text:0000D9B6 decrypt_end_message: ; CODE
XREF: sync_sys+29D
.text:0000D9B6 mov eax, [ebp+var_18]
.text:0000D9B6 test eax, eax
.text:0000D9B9 jnz short loc_D9FB
.text:0000D9BB mov edx, [ebp+var_C] ; key
.text:0000D9BD mov ecx, [ebp+var_8] ; string
.text:0000D9C0 push edx
.text:0000D9C3 push 20h
.text:0000D9C4 push ecx
.text:0000D9C7 push 18h
.text:0000D9C9 call err_warn
.text:0000D9CE push 0Fh
.text:0000D9D0 push 190h
.text:0000D9D5 call sound
```

```asm
.text:0000D9DA mov [ebp+var_18], 1
.text:0000D9E1 add esp, 18h
.text:0000D9E4 call pcv_kbit8
.text:0000D9E9 test eax, eax
.text:0000D9EB jz short loc_D9FB
```

```asm
...

; this name I gave to label:
.data:0401736 encrypted_error_message2 db 74h, 72h, 78h, 43h,
48h, 6, 5Ah, 49h, 4Cl, 2dup(47h)
.data:0401736 db 51h, 4Fh, 47h, 61h, 20h,
22h, 33Ch, 24h, 33h, 76h
.data:0401736 db 33Ab, 33h, 31h, 0Ch, 0, 0Bh,
1F, 7, 1Eh, 1Ah
```

可见，解密加密的工作十分简单：我们只需要找到相关的CMP指令，把后面的跳转替换为无条件跳转指令即可。当然，编写SCOServer驱动程序也不失为一种方法。
