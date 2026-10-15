
```text
.text:1000B509: mov C_Processors,al; uchar
```

从微软下载对应的 PDB 文件之后，调试就能给变量分配正确的名称。我们从调试找到全局变量 `Processors`。传递 `NtQuerySystemInformation` 函数第二个参数（即缓冲区）是 `var_C58`。`var_C20` 和 `var_C58` 的差值是 `0xC58-0xC20=0x38(56)`。根据 MSDN 的官方说明，可知的数据格式如下：

```c
typedef struct _SYSTEM_BASIC_INFORMATION {
    BYTE Reserved[24];
    PVOID Reserved[4];
    CHAR NumberOfProcessors;
} SYSTEM_BASIC_INFORMATION;
```

因为本例是在 x64 系统上的，`VOID` 占用 8 字节。两个 `reserved` 字段占用 24+8=32 字节。这意味着 `var_C20` 可能是 `SYSTEM_BASIC_INFORMATION` 里的 `NumberOfProcessors` 字段。我们将来验证一下。把 `C:\Windows\System32` 里的 `taskmgr.exe` 复制出来，我们在副本上进行修改以防 Windows 补丁机制自动还原。使用 `Hiew` 打开后的文件，找到 74.2 所示的程序地址：

```text
010000b4:4038c258: cmp [rsp+058],ebp
010000b4:fd889054a600100: mov [00000001000255a8],rax
010000b54:nb642458: mov eax,ebp,[rsp+058]
010000b500:0f47c5: cmova eax,ebp
010000b50c:3ac3: mov a1,b1
010000b50e:880574950100: mov [00000001000024a8],a1
010000b514:7645: jbe .000000010000b5b--e3
010000b16:48fb:mov rdi,rbx
010000b19:49bd4:mov rdx,r12
010000b1c:8bcd:mov ecx,ebp
```

图 74.2 `Hiew` 找到修改的点。接下来，替换指令，通过 `MOV` 直接把返回结果改为64（将 CPU 设为64 核）。由于修改后的指令比原始指令短 1 个字节，我们还需要加上一个 `NOP` 指令。如图 74.3 所示。

```text
| 00000A8F8: 4038C258 | cmp [rsp+058],ebp |
| 00000A8FD: 4889054A000100 | mov [00000001000255a8],rax |
| 00000A904: 66B84000 | mov ax,0040 |
| 00000A908: 90 | nop |
```

图 74.3 找到后。

## 第75章 修改彩球游戏

彩球游戏有多个衍生版本。本章采用的是1997年发布的 BallTrix 版。该程序可以从 http://go.yurichev.com/17311 公开下载。它的图形界面如图75.1所示。

![](img/a13a81a53f805f55074b2e5d2ec754b6_1139_0.png)

图75.1 游戏界面

本章关注的是随机生成器以及修改该组件的具体方法。`IDA` 在 `ballrix.exe` 中识别出了标准函数 `_rand`。该函数的地址是 `0x00403DA0`。不仅如此，`IDA` 判断该函数仅会被此处调用。

```text
.text:00402C9C sub_402C9C proc near ; CODE
XREF sub_402ACA+52 ;
.text:00402C9C
sub_402ACA+64 ...
.text:00402C9C
.text:00402C9C arg_0 = dword ptr 8
.text:00402C9C
.text:00402C9C push ebp
.text:00402C9D mov ebp, esp
.text:00402C9F push ebx
.text:00402CA0 push esi
.text:00402CA1 push edi
.text:00402CA2 mov eax, dword_40D430
.text:00402CA7 imul eax, dword_40D440
.text:00402CAE add eax, dword_40D558
.text:00402CB4 mov ecx, 32000
.text:00402CB9 cdq
.text:00402CBA idiv eax
.text:00402CBC mov dword_40D440, edx
.text:00402C22 call _rand_
.text:00402C77 cdq
.text:00402C78 idiv [ebp+arg_0]
.text:00402C7B mov eax, dword_40D430
.text:00402CD1 mov eax, dword_40D430
.text:00402CD6 jmp $+5
.text:00402CDB pop ebp
.text:00402CDC pop esi
.text:00402CDB pop ebx
.text:00402CDE leave
.text:00402CDF retn
.text:00402CFD endp
```

为了方便讨论，我们将调用 `_rand` 函数的函数称为 `random`。在程序中共有三处代码调用了 `random` 函数。

### 调用 `rand` 函数的前两处代码：

```text
.text:00402B16 mov eax, dword_40C03C ; 10 here
.text:00402B1B push eax
.text:00402B1C call random
.text:00402B21 add esp, 4
.text:00402B24 inc eax
```

### 使用随机函数的第三处传参代码：

```text
.text:0002B25 mov [ebp+var_C], eax
.text:0002B28 mov eax, dword_40C040 ; 10 here
.text:0002B2D push eax
.text:0002B2E call random
.text:0002B33 add esp, 4
```

```text
.text:0002BBB mov eax, dword_40C058 ; 5 here
.text:0002BC0 push eax
.text:0002BC1 call random
.text:0002BC6 add esp, 4
```

```text
.text:0002BC9 inc eax
```

综合上述代码，我们可以判定该函数至少带有一个参数。前两次传递的参数是 10，第三次传递的参数是 5。观察游戏界面可知，棋盘是 10×10 的方形，彩球颜色共有5种。此处调用 `random` 的指令用于生成坐标和颜色。标准的 `rand()` 函数会生成 0 到 7FFF 之间的整数，这并不方便。实际上，程序员会编写自己的随机函数以获取区间内的返回值。本例需要的随机数是 0 到 $n-1$ 的整数，其中 $n$ 是函数所需的参数。通过调试器可以验证：本章将修改第三次调用指令，使其永远返回 0。我们将 `PUSH`/`CALL`/`ADD` 这三条指令改为 `NOP`，然后添加 `XOR EAX, EAX` 以清空寄存器。

```text
.text:0002ABB: 83C410 add esp,10
.text:0002BBB: A158C040 mov eax, [0004C58]
.text:0002BC0: 31C0 eax
.text:0002BC2: 90 nop
.text:0002BC3: 90 nop
.text:0002BC4: 90 nop
.text:0002BC5: 90 nop
.text:0002BC6: 90 nop
.text:0002BC7: 90 nop
.text:0002BC8: 90 nop
.text:0002BC9: 40 inc eax, [ebp-8]
.text:0002BCA: 8BDF8 mov ecx, [ecx]*2
.text:0002BCD: D0C49 lea ecx,
.text:0002BD0: 8B15F400 mov [0004D54], eax
```
