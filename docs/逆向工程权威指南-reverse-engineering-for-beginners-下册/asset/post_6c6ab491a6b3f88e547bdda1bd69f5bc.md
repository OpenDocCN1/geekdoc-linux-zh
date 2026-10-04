
```
seg000:01189CC 48 00 00 A4 b exit
seg000:01189D0
seg000:01189D0 loc_1189D0: # CODE XREF:
seg000:01189D0
check3+28oj
seg000:01189D0 # check3+288j
seg000:01189D0 57 A0 06 3E
clrlwi %r0, %r29, 24
seg000:01189D4 28 00 00 02
cmpli %r0, 2
seg000:01189D8 40 82 20 00
bne loc_1189F8
seg000:01189DC 57 E0 06 3F
clrlwi %r0, %r31, 24
seg000:01189E0 41 82 00 01
beq good2
seg000:01189E4 48 00 4C 69
bl sub_11D64C
seg000:01189E8 60 00 00 00
nop
seg000:01189EC 48 00 00 84
exit
seg000:01189F0
seg000:01189F0 good2: # CODE XREF:
check3+2A4j
seg000:01189F0 38 60 00 01
li %r3, 1
seg000:01189F4 48 00 00 7C
exit
seg000:01189F8
seg000:01189F8 loc_1189F8: # CODE XREF:
check3+29cj
seg000:01189F8 80 00 00 00
lw %r6, dword_24B704
seg000:01189FC 38 81 00 38
addi %r4, %sp, 0x50+var_18
seg000:0118A00 38 00 00 05
li %r3, 5
seg000:0118A04 38 00 00 00
li %r5, 0
seg000:0118A08 48 00 BD C1
bl .REREAD
seg000:0118A0C 60 00 00 00
nop
seg000:0118A10 54 60 04 3F
clrlwi %r0, %r3, 16
seg000:0118A14 41 82 00 00
beq loc_118A20
seg000:0118A18 38 60 00 00
li %r3, 0
seg000:0118A1C 48 00 00 54
exit
seg000:0118A20
seg000:0118A20 loc_118A20: # CODE XREF:
check3+2Dbj
seg000:0118A20 0A 01 00 38
lhw %r0, 0x50+var_18 (%sp)
seg000:0118A24 28 00 11 D3
cmpli %r0, 0xD3000
seg000:0118A28 40 82 00 00
bne loc_118A34
seg000:0118A2C 3E 0B 00 01
li %r31, 1
seg000:0118A30 48 00 00 14
bood1
seg000:0118A34
seg000:0118A34 loc_118A34: # CODE XREF:
check3+2ECj
seg000:0118A34 28 00 1A EB
cmpli %r0, 0xEBA1
seg000:0118A38 41 82 00 00
beq good1
seg000:0118A3C 38 60 00 00
li %r3, 0
seg000:0118A40 48 00 00 30
exit
seg000:0118A44
seg000:0118A44 good1: # CODE XREF:
check3+2F4j
seg000:0118A44 # check3+2FC
seg000:0118A44 57 A0 06 3E
clrlwi %r0, %r29, 24
seg000:0118A48 28 00 00 03
cmplwi %r0, 3
seg000:0118A4C 40 82 00 20
bbne error
seg000:0118A50 57 E0 06 3F
clrlwi %r0, %r31, 24
seg000:0118A54 41 82 00 10
beq good
seg000:0118A58 48 00 4B F5
bl sub_11D64C
seg000:0118A5C 60 00 00 00
nop
seg000:0118A60 60 00 01 10
exit
seg000:0118A64
seg000:0118A64 good: # CODE XREF:
check3+318j
seg000:0118A64 38 60 00 01
li %r3, 1
seg000:0118A68 48 00 08 00
be exit
seg000:0118A6C
seg000:0118A6C error: # CODE XREF:
check3+19Cj
# check3+238j
seg000:0118A68 38 60 00 00
li %r3, 0
seg000:0118A70
seg000:0118A70 exit: # CODE XREF:
check3+4Aj
# check3+58j
seg000:0118A70 80 01 00 58
lwz %r0, 0x50+arg_8 (%sp)
seg000:0118A74 38 21 00 50
addi %sp, %sp, 0x50
seg000:0118A78 83 E1 FF FC
lwz %r31, var_4(%sp)
seg000:0118A7C 7C 08 03 A6
mtrl %r0
seg000:0118A80 83 C1 FF F9
lwz %r30, var_8 (%sp)
seg000:0118A84 83 AI FF F4
lwz %r29, var_C(%sp)
seg000:0118A88 4E 80 00 20
blr
seg000:0118A88
# End of function check3
```

此函数多次调用了RBREAD()函数。在调用这个函数之后，check3()函数又大量使用CMPWI将返回值与特定的固定值进行比较。由此可见，RBREAD()函数是从内存加密读取的函数。

另外，在调用RBREAD()函数之前，r3寄存器的取值不外0、1、8、0xA、0xB、0xC、0D和4。这很可能是内存地址类的信息。

如果使用google引擎搜索这些函数名，的查询结果多半是Sentinel Eve3加密开发者手册。

其实，在了解其他PowerPC指令的情况下，我们照样可以分析加密有关操作。毕竟凭证数据就是这几个，而且“认证成功”的回值为1，“认证失败”的回值肯定是0。

综合分析，让check1()函数的返回值固定为或其他非零值，即可破解加密认证。但是我并不熟悉PowerPC的指令，所以我决定采取保守的修改方案：修改check2()函数在0001186FC处和000111878处的跳转指令。

我把0001186FC的指令改为0x480，把BEQ指令替换为无条件跳转指令B。即使不查阅IBM的参考手册，我们在程序里找到B指令的opcode。

另外，我把000111878修改为一个0x60和三个字节，将有关改为NOP指令。当然了，这也是从原程序里找的opcode。

进行上述修改之后，在不插入加密的情况下，程序仍然可以正常运行。

总之，借助于IDA部分汇编知识，任何人都可以小规模地修改程序。

# 78.2 例2：SCO OpenServer

本例研究的程序是1997年开发的面向SCO OpenServer的程序。因为年代过于久远，早就找不到开发者了。这款软件的加密驱动是定制程序。“Copyright 1998, Rainbow Technologies, Inc., CA”和“Sentinel Integrated Driver Ver.3.0”字样。在SCO OpenServer上安装驱动之后，硬件将被加载到系统的/dev目录：

/dev/rbs1
/dev/rbs2
/dev/rbs3

如果不插入加密，程序将会报错。而且错误信息不在执行序列里。在IDA加载SCO OpenServer的程序。在IDA里搜索“rsl”，找到了指令：

```
text:00022AB8      public SSQC
text:00022AB8      SSQC        proc near    ; CODE XREF: SSQC+7j
text:00022AB8      var_44      = byte ptr -44h
text:00022AB8      var_29      = byte ptr -29h
text:00022AB8      arg_0       = dword ptr 8
text:00022AB8      push       ebp
text:00022AB9      mov        ebp, esp
text:00022ABB      sub        esp, 44h
text:00022ABE      push       edi
text:00022ABF      mov        edi, offset 4035D0
text:00022AC4      push       esi
text:00022AC5      mov        esi, [ebp+arg_0]
text:00022AC8      push       ebx
text:00022AC9      push       esi
text:00022ACA        call       strlen
text:00022ACF      add        esp, 4
text:00022AD2      cmp        eax, 2
text:00022AD7      jnz        loc_22BA4
text:00022ADD      inc        esi
text:00022ADE      mov        eax, [esi-1]
text:00022AE1      movsx      eax, al
text:00022AE4      cmp        eax, '3'
text:00022AE9      jnz        loc_22B84
text:00022AEF      cmp        eax, '4'
text:00022AF4      jnz        loc_22B94
text:00022AFA      cmp        eax, '5'
text:00022B0      jnz        short loc_22BB
text:00022B01      movsx      ebx, byte ptr [esi]
text:00022B04      sub        ebx, '0'
text:00022B07      mov        eax, 7
text:00022B0C      add        eax, ebx
text:00022B0E      push       esi
text:00022B0F      lea        eax, [ebp+var_44]
text:00022B12      push       offset /dev/sl/d
text:00022B17      push       eax
text:00022B18      call       nl_sprintf
text:00022B1D      push       0                              ; int
```

| . | . |
| --- | --- |
| .text:0002B1F | push offset /dev/rbs1 ; char * |
| .text:0002B24 | call _access |
| .text:0002B29 | add esp, 14h |
| .text:0002B2C | cmp eax, 0xFFFFFF |
| .text:0002B31 | jz short loc_22B48 |
| .text:0002B33 | lea eax, [ebx+7] |
| .text:0002B36 | push eax |
| .text:0002B37 | lea eax, [ebp+var_44] |
| .text:0002B3A | push offset /dev/rbs1d |
| .text:0002B3F | push eax |
| .text:0002B40 | call nl_sprintf |
| .text:0002B45 | add esp, 0Ch |
| .text:0002B48 | loc_22B48; CODE XREF: SSQC+7j |
| .text:0002B48 | mov edx, edi |
| .text:0002B4A | test edx, edx |
| .text:0002B4C | jle short loc_22B5 |
| .text:0002B4E | push eax ; int |
| .text:0002B4F | call _close |
| .text:0002B54 | add esp, 4 |
| .text:0002B57 | loc_22B57; CODE XREF: SSQC+94j ; int |
| .text:0002B59 | push 2 |
| .text:0002B59 | lea eax, [ebp+var_44] ; char * |
| .text:0002B5C | push eax |
| .text:0002B5D | call _open |
| .text:0002B62 | add esp, 8 |
| .text:0002B65 | test eax, eax |
| .text:0002B67 | mov [eax], eax |
| .text:0002B69 | jge short loc_22B78 |
| .text:0002B6B | mov edx, 0xFFFFFFFF |
| .text:0002B70 | pop eax |
| .text:0002B71 | pop esi |
| .text:0002B72 | mov esp, ebp |
| .text:0002B75 | pop ebp |
| .text:0002B76 | ret |
| .text:0002B78 | loc_22B78; CODE XREF: SSQC+B1j |
| .text:0002B78 | pop eax |
| .text:0002B79 | pop esi |
| .text:0002B7A | xor eax, eax |
| .text:0002B7D | mov esp, ebp |
| .text:0002B7F | pop ebp |
| .text:0002B80 | ret |
| .text:0002B84 | loc_22B84 ; CODE XREF: SSQC+31j |
| .text:0002B84 | mov al, [esi] |
| .text:0002B84 | mov ebx |
| .text:0002B86 | pop esi |
| .text:0002B87 | pop edi |
| .text:0002B88 | pop edi |
| .text:0002B89 | mov ds:byte_40724, al |
| .text:0002B8E | mov esp, ebp (wait, OCR error: mov esp, ebp) |
| .text:0002B90 | xor eax, eax |
| .text:0002B92 | pop ebp |
| .text:0002B93 | ret |
| .text:0002B94 | loc_22B94: CODE XREF: SSQC+3Cj |
| .text:0002B94 | mov al, [esi] |
| .text:0002B96 | mov ebx |
| .text:0002B97 | pop esi |
| .text:0002B98 | pop edi |
| .text:0002B99 | mov ds:byte_40725, al |
| .text:0002B9E | mov esp, ebp |
| .text:0002BA00 | xor eax, eax |
| .text:0002BA02 | pop ebp |
| .text:0002BA03 | ret |
| .text:0002BA04 | loc_22BA4: CODE XREF: SSQC+1Fj |
| .text:0002BA04 | movsx eax, ds:byte_40725 |
| .text:0002BAB push esi |
| .text:0002BAC push eax |
| .text:0002BAD movsx eax, ds:byte_40724 |
| .text:0002BB4 push eax |
| .text:0002BB5 lea eax, [ebp+var_44] |
| .text:0002BB8 offset "%46%c%s%c%s" |
| .text:0002BBD0 push eax |
| .text:0002BBE0 call nl_printf |
| .text:0002BC33 lea eax, [ebp+var_44] |
| .text:0002BC36 push eax |
| .text:0002BC37 call strlen
| .text:0002BCC0 add esp, 18h |
| .text:0002BC3F cmp eax, 1Bh |
| .text:0002BD04 jle short loc_22BDA |
| .text:0002BD06 mov [ebp+var_29], 0 |
| .text:0002BDA0 loc_22BDA: ; CODE XREF: SSQC+1Cj |
| .text:0002BDA0 lea eax, [ebp+var_44] |
| .text:0002BDB0 push eax |
| .text:0002BDE0 call strlen |
| .text:0002BE33 push eax ; unsigned int |
| .text:0002BE34 lea eax, [ebp+var_44] |
| .text:0002BE47 push eax ; void *
```
