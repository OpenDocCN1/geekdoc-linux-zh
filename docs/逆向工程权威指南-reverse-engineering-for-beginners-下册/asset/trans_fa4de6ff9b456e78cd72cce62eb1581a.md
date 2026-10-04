
"Production"

```
mov ebx, edi      ; EDI=0xb200100
shr ebx, 18h     ; EBX=0xb200100
mov ecx, edi      ; EDI=0xb200100
shr ecx, 14h     ; ECX=0xb200100
and ecx, 0Fh      ; ECX=0xb2
mov edx, edi      ; EDI=0xb200100
shr edx, 0Ch      ; EDX=0xb200100
movzx edx, dl     ; DL=0
mov eax, edi      ; EDI=0xb200100
shr eax, 8        ; EAX=0xb200100
and eax, 0Fh      ; EAX=0xb200100
and edi, 0FFh     ; EDI=0xb200100
push edi          ; EDI=0
mov eax, [ebp+arg_18]; ; [EBP+20h]=0
push eax          ; EAX=1
mov eax, ds:__imp_vsnban;
```

[597D6D8h]=0x65852100, "Oracle Database 11g ✓

+   - 企业版发布版本 %d.%d.%d.%d 和 %s"
  - push edx        ; EDX=0
  - push ecx        ; ECX=2
  - push ebx        ; EBX=0xb
  - mov ebx, [ebp+arg_8]; ; [EBP+10h]=0xcdfe54
  - push eax         ; EAX=0x65852100,"Oracle

+   Database 11g Enterprise Edition ✓
  - Release %d.%d.%d.%d.
    - mov eax, [ebp+Dest]; ; [EBP-10h]=0xce2ffb0
    - push eax
    - mov eax, edi      ; EAX=0xce2ffb0
    - call ds:__imp_sprintf; opl=MSVQCR80.dll!sprintf

+   追踪最大级别 (1) ✓
  - 已到达，跳过此调用
    - add esp, 38h
    - mov dword ptr [eax], 1

```

loc_2CE1192; ; 代码引用: _kqrow+_FB
  ; _kqrow+128 ...    ; EDI=0
test edi, edi
jnz _VInfreq_kqrow
mov esi, [ebp+var_C]; ; [EBP-0Ch]=0xcdfe248
mov edi, [ebp+var_4]; ; [EBP-4]=0xc9c938
mov eax, ebx        ; EBX=0xcdfe554
mov eax, [ebp+var_8]; ; [EBP-8]=0
lea eax, [eax+4];   ; [EAX+4]=0xce2ff0,
```

"NLSRTL 版本 11.2.0.1.0 - 生成环境✓

+   - "Oracle Database 11 Enterprise Edition Release 11.2.0.1 - Production"," "PL/SQL ✓

```
Release 11.2.0.1.0 - Production", "TNS for 32-bit
Windows: Version 11.2.0.1.0 - 
    Production"
```

```
loc_2CE11A8: 代码引用; _kqrow_+29E00F6
    mov     esp, ebp
    pop
    retn                               ; EAX=0x0cdfe558
```

```
loc_2CE11AC: 数据引用; .rdata:0628B0A0
    mov     edx, [ebx+8];      [EBX+8]=0xce2ffb0,
    "Oracle Database 11g Enterprise Version
    Release 11.2.0.1.0 - Production"
    mov     dword ptr [ebx], 2
    mov     [ebx+4], edx      ; EAX=0xce2ffb0,
Oracle Database 11g Enterprise Version
    Release 11.2.0.1.0 - Production"
    push    edx                      ; EAX=0xce2ff0
    call    kvssn               ; 追踪最大级别 (1) 已到达，跳过此调用
    CALL

```
    pop     ecx
    mov     edx, [ebx+4];      [EBX+4]=0xce2ffb0,
PL/SQL Release 11.2.0.1.0 - Production"
    movzx ecx, byte ptr [edx] ; [EDX]=0x50
    test ecx, ecx               ; ECX=0x50
    jnz     short loc_2CE112
    mov     edx, [ebp+var_14]
    mov     esi, [ebp+var_C]
    mov     eax, ebx
    mov     ebx, [ebp+var_8]
    mov     ecx, [eax]
    jmp     loc_2CE10F
```

loc_2CE11DB: 数据引用; .rdata:0628A4
    push    0
    push    50h
    mov     edx, [ebx+8];      [EBX+8]=0xce2ff0,
PL/SQL Release 11.2.0.1.0 - Production"
    mov     [ebx+4], edx      ; EAX=0xce2ff0,
PL/SQL Release 11.2.0.1.0 - Production"
    push    edx                      ; EAX=0xce2ff0,
PL/SQL Release 11.2.0.1.0 - Production"
    call    lmx               ; 追踪最大级别 (1) 已到达，跳过此调用

add      esp, 0Ch
mov      dword ptr [ebx], 3
jmp      short loc_2CE192

loc_2CE11F6: 数据引用; .rdata:0628A8
mov      edx, [ebx+8]    ; [EBX+8]=0xce2ffb0
mov      [ebx+var_18], 50h
mov      [ebx+4], edx    ; EAX=0xce2ff0
push     _npini
call     tracing maximum
level (1) reached, skipping this此```

pop      ecx
test     eax, eax    ; EAX=0
jz      ecx, [ebp+var_14]  ; [EBP-14h]=0xc9938
lea      edx, [ebx+var_18]  ; [EBX-18h]=0x50
push     edx        ; EDX=0x7d69
push     dword ptr [ebx+8]  ; [EBX+8]=0x2ff0
push     dword ptr [ecx+1327h];
[ECX+1327h]=0xacc90
call     nrtsv  ; 最大
 ( (1 skipping this

add      esp, 0Ch

loc_2CE12B: 代码引用: lkvrow+_29E018
mov      dword ptr [ebx], 4
jmp      loc_2CE192

loc_2CE1236: 数据引用; .rdata:0628AC
lea      edx, [ebx+var_7C]  ; [EBX-7Ch]=1
push     edx        ; EDX=0x7dcd8
push     0
mov      esi, [ebx+8]    ; [EBX+8]=0x2ffb0, *TNS
for 32-bit Windows: Version ✓

11.2.0.1.0 - Production"

mov      [ebx+4], esi    ; ESI=0xce2ffb0, *TNS
for

32-bit Windows: Version 11.2.0.1

Production"

mov      ecx, 50h
mov      [ebx+var_18],  ; ECX=0x50
push     ecx        ; ECX=0x50
push     esi        ; ESI=0xce2ffb0, *TNS for

32-bit Windows: Version 11.2.0.1.0 ✓

\ - Production"

call    lxvers              ; 追踪
level (1) reached, skipping this ✓
CALL
add     esp, 10h
mov     edx, [ebp+var_18]  ; [EBP-18h]=0x50
mov     dword ptr [ebx], 5      
test     edx, edx         ; EDX=0x50
jnz     loc_2CE1192
mov     edx, [ebp+var_14]
mov     esi, [ebp+var_C]
mov     eax, ebx        ; EBX=0xcdfe554
mov     ebx, [ebp+var_8]
mov     ecx, 5
jmp    loc_2CE10F

loc_2CE127A: 数据引用; .data:06280B0 ; [ebp+var_14] ; [ebp-14h]=0xc9c938

mov     x, [ebp+var_C]  ; [EBP-0Ch]=0xcdfe248
mov     edi, [ebp+var_4]; ; [EBP-4]=0xc9c938
mov     eax, ebx           ; EBX=0xcdfe554
mov     ebx, [ebp+var_8] ; [EBP-8]=0

loc_2CE288: 代码引用: _kqvvsn+1F

mov     eax, [eax+8]      ; [EAX+8]=0xce2ffb0,
"NLSRTL Version 11.2.0.1.0 - Production"
test    eax, eax          ; EAX=0xce2ffb0,
NLSRTL Version 11.2.0.1.0 - Production"
offset  short loc_2CE27A
push    axkqvvsn   ; "$kqvvsn"
push    ax               ; EAX=0xce2ffb0,
NLSRTL Version 11.2.0.1.0 - Production"
mov     eax, [ebp+arg_C]  ; [EBP+14h]=0x8a17b
push    ax               ; EAX=0x8a17b
push    dword ptr [edx+1094] ;
[EDX+1094h]=0xc9cd8
call           ; 追踪
level (1) reached, skipping this

add     esp, 10h

loc_2CE27A: 代码引用: _kqvvsn+1C
xor     ax, eax
mov     esp, ebp
pop     ebp

retn
; EAX=0
krow_end

看出，该函数从外部获取行号，按照下述返回字符串。

| String |
| :--- |
| 1 Using vsnstr, vsnban, global variables. |
| 2 Calling sprintf(). |
| 3 Calling kkxsn(). |
| 4 Calling npinli(), nrtvs(). |
| 5 Calling lxvers(). 按照上述顺序依次调用函数，从而获取各个模块的版本。

2 X$MLRU表

官方文件《Diagnosing and Resolving Error ORA-0431》[5]特别到了这个数据表:Oracle能够记录内存内强制释放对象的内存占用。负责这种情况的数据表是固定表ksmlru。它用于诊断内存异常导致缓存的具体原因。如果内存里发生了大量对象周期释放的情况，这种问题会增加数据库的响应。而且这些对象再次加载到内存时，这一现象会增加缓存（library cache）互锁的频率。固定表 x$ksmlru具有一个特性：只要检索该表的操作，那么这个表内的数据就会立刻清空。此外，数据只会存储内存最大的几项记录。“查询后清空”的设计是为了掩盖那些不费内存分配情况。也就是，每次检索对应的时间不同的。如此，数据库应当妥善保管该查询结果。换句话，查询这个表不是问题，是查询后它会被立即清空。那么，清表的具体原因是什么？既然kq表和kqft表包含了全部信息，我们可以继续使用前文的oracle_tables进行分析。在oracle_tables的返回里，我们看到：在准备XKSMLRU元素时，oracle调用了ksmlr 函数。

1.10 Result of oracle tables

kqftab_element.name: [KSMLRU]?: [ksmlr] 0x04 0x64 0x11 0xffff0bb 0x05
kqftab_param.name: [ADDR]?: 0x97 0x00 0x00 0x04 0x00
kqftab_param.name: [INDX]?: 0x02 0x00 0x00 0x04 0x00
kqftab_param.name: [INST]?: 0x02 0x00 0x00 0x04 0x00
kqftab_param.name: [KMSLRDI]?: 0x02 0x00 0x00 0x04 0x00
kqftab_param.name: [KMSLRUR]?: 0x02 0x00 0x00 0x04 0x04
kqftab_param.name: [KMSLRPOOL]?: 0x02 0x00 0x00 0x04 0x04
kqftab_param.name: [KSMLRCOM]?: 0x51 0x00 0x00 0x00 0x14
kqftab_param.name: [KMSLRSIJ]?: 0x02 0x00 0x00 0x04 0x20
kqftab_param.name: [KMSLRNJM]?: 0x02 0x00 0x00 0x04 0x24
kqftab_param.name: [KMSLRHOV]?: 0x02 0x00 0x00 0x04 0x48
kqftab_param.name: [KMSLRSEJ]?: 0x17 0x00 0x00 0x04 0x4c
kqftab_param.name: [KMSLRADJ]?: 0x02 0x00 0x00 0x04 0x50
kqftab_param.name: [KMSLRNID]?: 0x02 0x00 0x00 0x04 0x54
kqftab_param.name: [KMSLRNSD]?: 0x02 0x00 0x00 0x04 0x58
kqftab_param.name: [KMSLRNCD]?: 0x02 0x00 0x00 0x04 0x5c
kqftab_param.name: [KMSLRNED]?: 0x02 0x00 0x00 0x04 0x60 0x00
