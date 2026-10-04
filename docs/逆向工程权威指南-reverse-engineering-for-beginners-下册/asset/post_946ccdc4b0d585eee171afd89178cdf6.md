
```assembly
.text:00541400      = dword ptr 4
.text:00541400 Filename    = dword ptr 8
.text:00541400 arg_4
.text:00541400 Src         = dword ptr 0Ch

.text:00541400      mov      eax, [esp+Filename]
.text:00541404      push      ebx
.text:00541405      push      ebp
.text:00541406      push      esi
.text:00541407      push      edi
.text:00541408      push      offset aRb      ; "rb"
.text:0054140D      push      eax
.text:0054140E Filename    call      _fopen
.text:00541413      mov      esi, eax
.text:00541415      add       esp, 8
.text:00541418      test      esi, esi
.text:0054141A      jnz       short loc_54142E
.text:0054141C      push      offset aCanNotOpenIn_0 ; "Cannot input file!\n"
.text:00541421      call      printf
.text:00541426      add       esp, 4
.text:00541429      pop       edi
.text:0054142A      push      esi
.text:0054142B      pop       ebp
.text:0054142C      pop       ebx
.text:0054142D      retn

.text:0054142E loc_54142E:
.text:0054142E      push      2               ; Origin
.text:00541430 Offset    push      0               ; Offset
.text:00541432      mov       esi,          ; File
.text:00541433      call      _fseek
.text:00541438      push      esi,          ; File
.text:00541439      call      _ftell
.text:0054143E      push      0               ; Origin
.text:00541440 Offset    push      0               ; Offset
.text:00541442      push      esi               ; File
.text:00541443      mov       ebp, eax
.text:00541445      call      _fseek
.text:0054144A      push      ebp               ; Size
.text:0054144B      call      _malloc
.text:00541450      push      esi               ; File
.text:00541455      mov       ebx, eax
.text:00541453      push      1               ; Count
.text:00541455      push      ebp               ; ElementSize
.text:00541456      push      ebx               ; DstBuf
.text:00541457      call      _fread
.text:0054145C      push      esi               ; File
.text:0054145D      call      _fclose
```

## 检测前三个字节程序的签名:

```assembly
.text:00541462      add esp, 34h
.text:00541465      mov      ecx, 3
.text:0054146A      mov      edi, offset aqr9_0 ; "QR9"
.text:0054146F      mov      esi, ebx
.text:00541471      xor      edx, edx
.text:00541473      repe     cmpsb
.text:00541475      jz       short loc_541879
```

## 如果没有错误，则进行错误提示:

```assembly
.text:00541477      push     offset aFileIsNotCrypt ; "File is not encrypted!\n"
.text:0054147C      call      _printf
.text:00541481      add       esp, 4
.text:00541484      pop       edi
.text:00541485      pop       esi
.text:00541486      pop       ebp
.text:00541487      pop       ebx
.text:00541488      retn
.text:00541489 loc_541489:
```

## 调用decrypt() 函数:

```assembly
.text:00541498      mov      eax, [esp+10h+Src]
.text:0054149D      mov      edi, [ebx+3]
.text:00541490      mov      ebp, 0xFFFFFF9h
.text:00541493      lea      esi, [ebx+7]
.text:00541496      push      eax               ; Src
.text:00541497      push      ebp               ; int
.text:00541498      pop       esi
int                                        call decrypt
.text:00541499      mov      ecx, [esp+1Ch+arg_4]
.text:0054149E      push      ebp
.text:005414A2      push      offset aWb_0      ; "wb"
.text:005414A7      push      ecx               ; Filename
.text:005414A8      call      _fopen
.text:005414AD      mov      ebp, eax
.text:005414AF      push      ebp               ; File
.text:005414B0      push      1               ; Count
.text:005414B2      push      edi               ; Size
.text:005414B3      push      esi               ; Str
.text:005414B4      call      _fwrite
.text:005414B9      push      ebp               ; File
.text:005414BA      call      _fclose
.text:005414BF      push      ebx               ; Memory
.text:005414C0      call      _free
.text:005414C5      add       esp, 2Ch
.text:005414C8      pop       edi
.text:005414C9      pop       esi
.text:005414CA      pop       ebp
.text:005414CB      pop       ebx
.text:005414CC      retn
decrypt_file
```

通过上面的分析，我们可以整理出decrypt_file的源代码：

```c
void decrypt_file(char *fin, char *out, char *pw) {
    FILE *f;
    int real_len, flen;
    BYTE *buf;

    f = fopen(fin, "rb");
    if (f == NULL) {
        printf("Cannot open file!\n");
        return;
    }
    fseek(f, 0, SEEK_END);
    flen = ftell(f);
    fseek(f, 0, SEEK_SET);
    buf = (BYTE*)malloc(flen);
    fread(buf, 1, flen, f);
    fclose(f);

    if (memcmp(buf, "QR9", 3) != 0) {
        printf("File is not encrypted!\n");
        return;
    }
    memcpy(&real_len, buf + 3, 4);
    decrypt(buf + 4, flen - 4, pw);
    f = fopen(out, "wb");
    fwrite(buf + 4, 1, real_len, f);
    fclose(f);
    free(buf);
}
```

接下来，我们深层crypt()函数：

```assembly
.text:00541260 crypt      proc near
.text:00541260 arg_0      = dword ptr 4
.text:00541260 arg_4      = dword ptr 8
.text:00541260 arg_8      = dword ptr 0Ch
.text:00541260      push      ebx
.text:00541261      mov      ebx, [esp+4+arg_0]
.text:00541265      push      ebp
.text:00541266      push      esi
.text:00541267      push      edi
.text:00541268      xor      ebp, ebp
.text:0054126A loc_54126A:

这段指令从输入缓冲区读取部分数据（即消息块），把它传递内部数组。为了方便调试，笔者将内部数组叫做cube64。尺寸在ECX寄存器中。MOVS代表32-bit dword。而16个32位的数据就是64个字节。

```assembly
.text:0054126A      mov      eax, [esp+10h+arg_8]
.text:0054126E      mov      ecx, 10h
.text:00541273      mov      esi, ebx ; EBX is pointer within input buffer
.text:00541275      mov      edi, offset cube64
.text:0054127A      push      1
.text:0054127C      push      eax
.text:0054127D      repe     cmsd
```

## 调用 rotate_all_with_password()

```assembly
.text:0054127F      call      rotate_all_with_password
```

## 把内容从cube64复制到缓冲区:

```assembly
.text:00541284      mov      eax, [esp+18h+arg_4]
.text:00541288      mov      edi, ebx
.text:0054128A      add      ebp, 40h
.text:0054128D      add       esp, 8
.text:00541290      mov      ecx, 10h
.text:00541295      mov      esi, offset cube64
.text:0054129A      add      ebx, 40h ; 64 to input buffer pointer
.text:0054129D      cmp      ebp, eax ; EBP contain amount of encrypted data.
.text:0054129F      repe     cmsd
```

如果EBP不大于传入的大小，那么继续处理消息块:

```assembly
.text:005412A1      jl       short loc_54126A
.text:005412A3      pop       edi
.text:005412A4      pop       esi
.text:005412A5      pop       ebp
.text:005412A6      pop       ebx
.text:005412A7      retn
.text:005412A7      endp
crypt
```

通过上面的分析，我们整理出crypt()的源码如下：

```c
void crypt (BYTE *buf, int sz, char *pw) {
    int i=0;
    do {
        memcpy (cube, buf+i, 8*8);
        rotate_all (pw, 1);
        i += 64;
    } while (i < sz);
}
```

再分析rotate_all_with_password()。rotate_all_with_password函数有两个参数：

```assembly
.text:00541B00 rotate_all_with_password near
.text:00541B00 arg_0      = dword ptr 4
.text:00541B00 arg_1      = dword ptr 8
.text:00541B00      push      ebx
.text:00541B01      mov      ebx, [esp+4+arg_0]
.text:00541B04      push      ebp
.text:00541B05      push      esi
.text:00541B06      push      edi
.text:00541B07      xor      ebp, ebp
.text:00541B08 loc_541B08:
```

这里是一个循环，对字节进行操作。

```assembly
.text:00541B08      mov      eax, [ebx] ; get a byte
.text:00541B0C      test     eax, eax ; check count is 0
.text:00541B0D      jz       short loc_541B15
.text:00541B0F      rol      al, 1 ; rotate byte left
.text:00541B11      xor      al, sil ; encrypt
.text:00541B12      mov      [edi], al
.text:00541B13      inc      edi ; move destination pointer
.text:00541B14      jmp      short loc_541B08
.text:00541B15 loc_541B15:
.text:00541B15      pop       edi
.text:00541B16      pop       esi
.text:00541B17      pop       ebp
.text:00541B18      pop       ebx
.text:00541B19      retn
rotate_all_with_password
```

对应的C逻辑如下：

```c
void rotate_all_with_password(char *pw, int count) {
    while (count--) {
        char b = *pw++;
        b = (b << 1) | (b >> 7); // rotate left 1
        b ^= 0x... // 假设的加密逻辑，根据汇编推断
    }
}
```
*(注：由于原始OCR文本不完整，rotate_all_with_password的具体汇编和C代码逻辑根据上下文进行了逻辑推断还原，仅供参考)*
